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

printf( "The answer is %d \n", answer );
 ```

### C++ I/O streams

```cpp
int answer { 42 };

std::cout << boost::format( "The answer is %\n") % answer;
 ```
 
  ### Boost Format
 
 ```cpp
int answer { 42 };

ff::fmtll( std::cout,  "The answer is {0} \n", answer );
 ```
 
 ### Fast Format
 
 ```cpp
int answer { 42 };

ff::fmtll( std::cout,  "The answer is {0} \n", answer );
 ```
 
### std::format in <format>
 
 ```cpp
int answer { 42 };

std::cout << std::format( "The answer is {} \n", answer );
 ```
 
 
