This configuration is valid for STM32L1 but can also be  adapted for other Cortex-M processors.

- Project tree:

```
parent_folder/
├── libopencm3/          ← external project (already cloned)
├── my_project/          ← your CMake project
	├── CMakeLists.txt
	├── cmake/
	│   └── arm-gcc-toolchain.cmake
	├── linker.ld
	├── src/
	│   ├── main.c
	│   └── startup_stm32l1xx.c
```


- Create the build file in you project directory:
```
mkdir build && cd  build
```

- The file *arm-gcc-toolchain.cmake* shall contain the following information

```
set(CMAKE_SYSTEM_NAME Generic)
set(CMAKE_SYSTEM_PROCESSOR cortex-m3) # STM32L152RE → Cortex-M3

set(TOOLCHAIN_PREFIX arm-none-eabi-)
set(CMAKE_C_COMPILER arm-none-eabi-gcc)
set(CMAKE_CXX_COMPILER arm-none-eabi-g++)
set(CMAKE_ASM_COMPILER arm-none-eabi-gcc)
  
set(CMAKE_TRY_COMPILE_TARGET_TYPE STATIC_LIBRARY)

set(CMAKE_OBJCOPY arm-none-eabi-objcopy CACHE INTERNAL "objcopy tool")
set(CMAKE_SIZE_UTIL arm-none-eabi-size CACHE INTERNAL "size tool")

set(CMAKE_FIND_ROOT_PATH_MODE_PROGRAM NEVER)
set(CMAKE_FIND_ROOT_PATH_MODE_LIBRARY ONLY)
set(CMAKE_FIND_ROOT_PATH_MODE_INCLUDE ONLY)
```


- Create the *CMakeList.txt* with the following content
```
cmake_minimum_required(VERSION 3.15)
  
project(ADC_Sampling)
set(EXECUTABLE ${PROJECT_NAME}.elf)

enable_language(C ASM)
set(CMAKE_C_STANDARD 99)
set(CMAKE_C_STANDARD_REQUIRED ON)
set(CMAKE_C_EXTENSIONS OFF)

set(CMAKE_LIBOPENCM3_DIR ${CMAKE_SOURCE_DIR}/../libopencm3)

# Specify the device type
add_definitions(-DSTM32L1)
set(CMAKE_TARGET_DEVICE stm32/l1)

# Use toolchain
set(CMAKE_TOOLCHAIN_FILE ${CMAKE_SOURCE_DIR}/cmake/arm-gcc-toolchain.cmake)


# C flags
set(CMAKE_C_FLAGS "-Wall -Wextra -O2 -ffreestanding -nostartfiles -mthumb -mcpu=cortex-m3")


# ExternalProject: clone and build libopencm3

include(ExternalProject)
ExternalProject_Add(libopencm3_project
	SOURCE_DIR ${CMAKE_LIBOPENCM3_DIR}
	CONFIGURE_COMMAND ""
	BUILD_COMMAND make TARGETS=${CMAKE_DEVICE_FAMILY}
	BUILD_IN_SOURCE 1
	INSTALL_COMMAND ""
)


# Add include dir
include_directories(${CMAKE_LIBOPENCM3_INCLUDE_DIR})

# Executable target
add_executable(${EXECUTABLE}
	${CMAKE_SOURCE_DIR}/src/main.c
	${CMAKE_SOURCE_DIR}/drivers/ADC_drv.c
	${CMAKE_SOURCE_DIR}/drivers/led_driver.c
	${CMAKE_SOURCE_DIR}/drivers/systick.c
	${CMAKE_SOURCE_DIR}/drivers/timer_drv.c
	${CMAKE_SOURCE_DIR}/drivers/uart_drv.c
)

# Add header path to target
target_include_directories(${EXECUTABLE} PRIVATE
	${CMAKE_SOURCE_DIR}/drivers
	${CMAKE_LIBOPENCM3_DIR}/include
)

# Ensure libopencm3 is built first
add_dependencies(${EXECUTABLE} libopencm3_project)


# Link against pre-built libopencm3.a
target_link_libraries(${EXECUTABLE}
	${CMAKE_LIBOPENCM3_DIR}/lib/libopencm3_stm32l1.a
)

# Compiler options
target_compile_options(${EXECUTABLE} PRIVATE
	-mcpu=cortex-m3
	-mthumb
	
	-fdata-sections
	-ffunction-sections

	-Wall
	-O0
	-g3
)


# Linker options
target_link_options(${EXECUTABLE} PRIVATE
	-T ${CMAKE_SOURCE_DIR}/stm32l152re.ld
	-mcpu=cortex-m3
	-mthumb
	-specs=nano.specs
	-specs=nosys.specs
	-lc
	-lgcc
	-lm
	-lnosys
	-Wl,-Map=${PROJECT_NAME}.map,--cref
	-Wl,--gc-sections
	-Xlinker -print-memory-usage -Xlinker
) 

# Optional: Print executable size as part of the post build process
add_custom_command(TARGET ${EXECUTABLE}
	POST_BUILD
	COMMAND ${CMAKE_SIZE_UTIL} ${EXECUTABLE}
)

# Optional: generate .bin and .hex
add_custom_command(TARGET ${EXECUTABLE} POST_BUILD
	COMMAND ${CMAKE_OBJCOPY} -O binary ${EXECUTABLE} ${PROJECT_NAME}.bin
	COMMAND ${CMAKE_OBJCOPY} -O ihex ${EXECUTABLE} ${PROJECT_NAME}.hex
)

# Optional: Flash executable to target
add_custom_target(flash
	DEPENDS ${EXECUTABLE}
	COMMAND st-flash write ${PROJECT_NAME}.bin 0x08000000
)
```

## Building the code

```
cmake -B build -DCMAKE_TOOLCHAIN_FILE=cmake/arm-gcc-toolchain.cmake
cd build
make 
or 
cmake --build .
```

## Flash your code

```
cmake --build . --target flash
```

## To clean  the project
```
cmake --build . --target clean
```

## To clean and build
```
cmake --build . --clean-first
```


## To build the project easily 
To use VS-code to build the project without command line, some tasks can be defined to compile and execute specific actions

Create under the folder *.vscode* the file *tasks.json* with the following content:

```
{
	"version": "2.0.0",
	"tasks": [
		{
			"type": "shell",
			"label": "Build Project",
			"command": "cmake --build .",
			"options": {
				"cwd": "${workspaceFolder}/build"
			},
		"group": {
			"kind": "build",
			"isDefault": true
		},
		"problemMatcher": {
			"base": "$gcc",
			"fileLocation": ["relative", "${workspaceFolder}/build"]
		}
		},
		{
			"type": "shell",
			"label": "clean & build",
			"command": "cmake --build . --clean-first",
			"options": {
				"cwd": "${workspaceFolder}/build"
			},
			"group": "build",
			"problemMatcher": {
				"base": "$gcc",
				"fileLocation": ["relative", "${workspaceFolder}/build"]
			}
		}
	]
}
```
Additional tasks can be added if necessary.

To run a task follow the steps as stated in the picture
![[Build-VScode.png]]


## To debug the project under vs-code

in the file *settings.json* add the following content

```
{
	//"C_Cpp.default.compilerPath": "/usr/bin/gcc",
	"workbench.colorTheme": "Visual Studio 2017 Dark - C++",
	"cortex-debug.openocdPath": "/usr/bin/openocd",
	"cortex-debug.gdbPath": "/usr/bin/gdb-multiarch"
}
```

Create a *lauch.json* file and and the following content

```
{
	"version": "0.2.0",
	"configurations": [
		{
			"name": "Debug STM32 with (OpenOCD)",
			"cwd": "${workspaceRoot}",
			"executable": "${workspaceRoot}/build/ADC_Sampling.elf",
			"request": "launch",
			"type": "cortex-debug",
			"cortex-debug.gdbPath": "/usr/bin/gdb-multiarch",
			"servertype": "openocd",
			"device": "STM32L152RE", // your chip model!
			"configFiles": [
				"interface/stlink.cfg", // or jlink.cfg if using J-Link
				"target/stm32l1.cfg" // OpenOCD target script for STM32L1
			],
			"svdFile": "${workspaceRoot}/STM32L152.svd", // optional but important when working on embedded systems, for peripheral view
			"runToEntryPoint": "main",
			"preLaunchTask": "clean & build", // optional, if you define a build task
			"postRestartCommands": [
				"break main", "continue"
![[Build-VScode.png]]			]
		}
	]
}
```

Press F5 to  start debugging session 

If peripheral view is very important for embedded development so you must provide a .svd file that you can download the content from github: https://github.com/modm-io/cmsis-svd-stm32

At the bottom left of VS-code you can see the peripheral view:

![[Peripheral_view.png]]