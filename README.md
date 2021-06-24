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

### C-Style printf() from stdio

```cpp
int answer { 42 };

// C-Style printf()
printf( "The answer is %d \n", answer );
 ```
