# std::format in C++20

## Requirement

| compiler | version  |
|:--------:|:-------------:|
| Visual Studio | 16.10 / 19.29 |
| GCC | ??? |
| clang | ??? |

```cpp
#include <format>
 ```
    
## Currently ways to formatting in C++

### C-Style printf() from <cstdio>

```cpp
int answer { 42 };

printf( "The answer is %d ", answer );
 ```

### C++ I/O streams

```cpp
int answer { 42 };

std::cout << "The answer is " << answer << "\n";
 ```
 
  ### Boost Format
 
 ```cpp
int answer { 42 };

std::cout << boost::format( "The answer is %") % answer;
 ```
 
 ### Fast Format
 
 ```cpp
int answer { 42 };

ff::fmtll( std::cout,  "The answer is {0}", answer );
 ```
 
### std::format in <format>
 
 ```cpp
int answer { 42 };

std::cout << std::format( "The answer is {}", answer );
 ```
 
 ## Placeholder
 
Format string contains placeholders { }
 
```cpp
std::cout << std::format( "The answer is {}", 42 );
 ```
 
Can contains argument index
 
 ```cpp
std::cout << std::format( "The answer is {0}", 42 );
 ```
 
curly braces in output
 
 ```cpp
std::cout << std::format( "The answer is {{ }}", 42 );
 ```
 
## Format specifiers
 
Placeholder can contains a format specifiers. It starts with a colon: {[index]:[format specifiers]}
 
[[fill]align][sign][#][0][width][.precision][type]
 
### [width]
 
minimum desired field width

```cpp
std::cout << std::format( "{:5}", 42 );
 ```
 
```cpp
std::cout << std::format( "{:{}}", 42, 5 );
 ```
 ### [fill]align]
 
Specifies optional characters and aligment
 
* < left
* > right
* ^ center
 
 
<ul>
<li><p>< left</p></li>
<li><p>> right</p></li>
<li><p>^ center</p></li>
</ul>
