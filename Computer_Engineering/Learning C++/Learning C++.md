

* A variable is an abstraction for a memory location: This means we use variables to name a memory area where information is stored. This memory location could change if we run the program again but since the name doesn't change we can still use it. The content of the variable may change also.
* It allows programmers to use meaningful names an not memory addresses (Since they can bring confusion)
* A variable has:
	* Type -Their category (integer, real number, string, Person)
	* Value - The content (10, 3.24, "Toto")
* Variable must be declared before they are used
 ![[VariableInMemeory.png]]



# Declaring variables

* Variables can contain letters, numbers and underscores
* Must begin with a letter or underscore
* Cannot begin with a number
* Cannot use C++ reserved keywords
* Cannot re-declare a name in the same scope
* C++ is case sensitive



![[NamingVariables.png]]


# Naming convention

Camel case can be used: The first character of each word shall be upper case (DayOfYear)
Underscore can be used: An underscore is used to separate each work of the variable name (buffer_index)

# C++ Vectors

Vectors are object oriented container defined in the C++ template library. The elements in a vector can grow and shrink in size making it dynamic. The syntax of vectors is similar to arrays. 

## Vector declaration

1. We must include the vector library

```
#include <vector>
using namespace std;

vector <char> vowels;
vector <int> values;
```

+  vectors are initialized to 0 if no initializing value is provided.

```
vector <char> vowels {'a', 'e', 'i', 'o', 'u'}; // The vector vowels is initialized with the values a, e, i, o, u.

vector <int> values {100, 25, 65, 76, 1034}; // The vector values is initialize with the values 100, 25, 65, 76, 1034

vector <double> temperature (380, 45); // This creates a vector of 380 values all initialized to 45.
```


## Accessing vector content

![[Vector_Access.png]]

Using the method **at()** we can have access to the content of specific memory regions by providing the location index as parameter.

NOTE: All the vectors must be the same size.

Using the **vector_name.push_back(element)** function we can add element to the back of a vector.
![[Vector_Push_Back.png]]
## 2D-Vectors


```
vector <vector<int>> 2d_vector
{
	{18, 34, 45, 65},
	{56, 764, 234, 56},
	{34, 56,21,87 ,90}
};
```


## Range based for loop

+ Less error prone for loop because there is no need of checking the boundaries

```
vector <float> temperature {32.5, 55.7, 23,1, 95.3};
for(float temp: temperatur)
	cout << temp << endl;



Outpu: 
32.5
55.7
23,1 
95.3
```

+ It is possible to use the **_auto_** keyword. The compiler is going to figure out the type of the variable itself 
```
vector <int> results {32, 45, 65, 76, 234, 98};

// Result is an array of integer this way res is also from type int.
for (auto res: results) 
	cout << res <<;


Output: 
32
45
65
76
234
98

```