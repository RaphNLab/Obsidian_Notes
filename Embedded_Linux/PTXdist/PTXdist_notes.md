
## Rule files
Rules files are used by PTXdist to provide information about how a package shall be handled. e.g: How to get package source.
All the rule files are located in the PTXdist **rules/**  directory. These rule files are global (valid for all projects), PTXdist goes through/scans all rule files whatever it is supposed to build.
* If a **rules/** directory exist in  the current project, PTXdist scans them too and add rule files that are not present into the local **rules/** directory.
* If the local **rules/** directory contains the same rules as the once located the the global **rules/**  directory, PTXdist replaces the global rule files.


## Patch series

Some packages may not be valid for cross-compiling, they fail on compile time due to wrong include paths or link against host libraries. To make them run developers must fix the issue by adding patches. This patches are located in the **patches/** folder under the same name as the package itself. 

## How to create a new package

Several steps are required:
1.  Create the rule file for the package
2. Check if all stages are working as expected
3. Select the required parts to get them installed in the target RootFS
4. 

### Create Rule files

```
ptxdist newpackage <package type>
```
If the </package type> is ignored PTXdist will display the list of all available package types.
To add a new package to the target:
```
ptxdist newpakage target
```
Follow the instructions and enter required information respectively.
* **package name:** Archive name e.g: foo-1.1.0.tar.gz or project name if cmake_project e.g: hello_world 
* **version number:** archive/project version
* **URL of basedir:** Tells ptxdist where to download the source archive. If local enter path
* **package author:** the author name will be used in the copyright note
* **package section:** Default value can be used, but still possible to change later on. This causes the packages name to be found on top in the menuconfig


# Use Infrared-Receiver

> ir-keytable -p rc5 (Set protocol to rc5)
> ir-keytable (Prints info about the ir-receiver)

To test: 
> evtest /dev/input/eventX (X represents the input device value, can be 0,1 or 2)


