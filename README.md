# std::format cheatsheet

![std::format cheatsheet](https://i.imgur.com/tDqRjOx.png)

If you like this content, or if it helps you, leave a ⭐!

## Introduction

### What is std::format?

`std::format` is a text formatting library introduced in **C++20**, offering a **safe** and **extensible** alternative to the `printf` family of functions. It aims to complement the existing C++ I/O streams library by reusing some of its infrastructure, such as overloaded insertion operators for user-defined types.

Prior to C++20, formatting text in C++ was often **error-prone** and **inconsistent**, relying on functions like `printf` or stream-based formatting. `std::format` was introduced to provide a **safer**, **more consistent**, and **modern** approach to text formatting.

Unlike `printf`, `std::format` offers:

- ✅ **Type safety**
- ✅ **Compile-time format string checking**
- ✅ **A clean, modern syntax**
- ✅ **Integration with user-defined types** through overloaded insertion operators

### Formatting functions

#### std::format

```cpp
std::string result = std::format(format_string, args...);
```

**Description**: Formats the given arguments (args...) according to the format_string and returns the result as a std::string.

[cppreference.com: std::format](https://en.cppreference.com/w/cpp/utility/format/format)

#### std::format_to

```cpp
auto it = std::format_to(output_iterator, format_string, args...);
```

**Description**: Formats the arguments just like std::format, but writes the result directly to an output buffer using an output iterator.

[cppreference.com: std::format_to](https://en.cppreference.com/w/cpp/utility/format/format_to)

#### std::format_to_n

```cpp
auto result = std::format_to_n(output_iterator, n, format_string, args...);
```

**Description**: Like format_to, but limits the output to a maximum of n characters. Returns a pair consisting of an output iterator pointing past the last written character and the number of characters that would have been written.

[cppreference.com: std::format_to_n](https://en.cppreference.com/w/cpp/utility/format/format_to_n)

#### std::formatted_size

```cpp
size_t size = std::formatted_size(format_string, args...);
```

**Description**: Returns the number of characters that would be produced by std::format (without actually formatting or allocating memory). Useful for pre-allocating buffers.

[cppreference.com: std::format_size](https://en.cppreference.com/w/cpp/utility/format/formatted_size)

## Table of Contents

- [std::format in C++20](#stdformat-in-c20)
	* [Introduction](#introduction)
		+ [What is std::format?](#what-is-stdformat)
		+ [Formatting functions](#formatting-functions) 
	* [Table of contents](#table-of-contents)
	* [Requirement](#Requirement)
	* [Currently ways to formatting in C++](#currently-ways-to-formatting-in-c)
		+ [C-Style printf() from \<cstdio\>](#c-style-printf-from-)
		+ [C++ I/O streams](#c-io-streams)
		+ [Boost Format](#boost-format)
		+ [Fast Format](#fast-format)
		+ [std::format in \<format\>](#stdformat-in-format)
	* [Placeholder](#placeholder)
		+ [Brace-delimited replacement fields](#brace-delimited-replacement-fields)
  	* [Format specifiers](#format-specifiers)


## Requirement

```cpp
#include <format>
 ```

| compiler support | Text Formatting (C++20)  | status |
|:--------:|:-------------:|:-------------:|
| Visual Studio | [VS 2019 16.10 / cl 19.29](https://learn.microsoft.com/en-us/cpp/overview/visual-cpp-language-conformance?view=msvc-170#c-standard-library-features) | completed |
| GCC | [13.1](https://gcc.gnu.org/onlinedocs/libstdc++/manual/status.html#status.iso.2020) | completed |
| clang | [14](https://libcxx.llvm.org/Status/Cxx20.html) | completed |

Source: [cppreference](https://en.cppreference.com/w/cpp/20)
   
## Currently ways to formatting in C++

### printf() function inherited from C

```cpp
#include <cstdio>	// C library for Input/Output operations
 ```

```cpp
const int answer { 42 };

printf( "The answer is %d ", answer );
 ```

### C++ I/O streams

```cpp
const int answer { 42 };

std::cout << "The answer is " << answer << "\n";
 ```
 
### Boost Format
 
```cpp
const int answer { 42 };

std::cout << boost::format( "The answer is %") % answer;
 ```

[www.boost.org](https://www.boost.org/doc/libs/1_77_0/libs/format/doc/format.html)
 
### Fast Format
 
```cpp
const int answer { 42 };

ff::fmtll( std::cout,  "The answer is {0}", answer );
 ```

[www.fastformat.org](http://www.fastformat.org/) or [github.com/synesissoftware/FastFormat](https://github.com/synesissoftware/FastFormat)
 
### std::format in \<format\>
 
```cpp
const int answer { 42 };

std::cout << std::format( "The answer is {}", answer );
 ```
 
## Placeholder

The {} indicates a replacement field like % in printf. 
 
### Brace-delimited replacement fields
 
```cpp
std::cout << std::format( "The answer is {}", 42 );
 ```
Writes the following output:

```bash
The answer is 42
 ```
 
### Positional arguments
 
 ```cpp
std::cout << std::format( "I'd rather be {1} than {0}", "right", "happy" );
 ```
 
### curly braces in output
 
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
 ### [[fill]align]
 
Specifies optional characters and aligment

### Aligment
<ul>
 <li><p>< left</p></li>
 <li><p>> right</p></li>
 <li><p>^ center</p></li>
</ul>

```cpp
std::cout << std::format( "{:<20}", "left");
 ```
 
```cpp
std::cout << std::format( "{:>20}", "right");
 ```
 
```cpp
std::cout << std::format( "{:^20}", "centered");
 ```
 ### Fill and aligment
 
 ```cpp
std::cout << std::format( "{:-^20}", "centered");
 ```
 
### [sign]
 
<ul>
 <li><p>- sign only for negative numbers (default)</p></li>
 <li><p>+ sign for negative and positive numbers</p></li>
 <li><p>scape display minus sign for negative numbers, a space for positive numbers</p></li>
</ul>

```cpp
std::cout << std::format( "{:<5}", 42 );
 ```

```cpp
std::cout << std::format( "{:<+5}", 42 );
 ```

```cpp
std::cout << std::format( "{:< 5}", 42 );
 ```
 
```cpp
std::cout << std::format( "{:< 5}", -42 );
 ```

### [#]
 
<ul>
 <li><p>enabled alternative formatting rules</p></li>
 <li><p>integral types</p>
  <ul>
     <li>Hexadecimal format: inserts 0x or 0X at font</li>
     <li>Binray format: inserts 0b or 0B at font</li>
     <li>Octal format: inserts 0</li>
    </ul>
 </li>
 <li><p>floating-points types</p>
  <ul>
   <li>always show decimal separator, even without following digits</li>
  </ul>
 </li>
</ul>

```cpp
std::cout << std::format( "{:15d}", 42 );
 ```

```cpp
std::cout << std::format( "{:15b}", 42 );
 ```
 
```cpp
std::cout << std::format( "{:#15b}", 42 );
 ```
 
```cpp
std::cout << std::format( "{:15X}", 42 );
 ```

```cpp
std::cout << std::format( "{:#15X}", 42 );
 ```
 
### [type]

#### integer types
#### floating-points types
#### booleans
#### characters
#### strings
#### pointers


### [.precision]
 
only for floating-points types and strings types

```cpp
const double pi { 3.1415 };
const int precision { 2 };
const int width { 15 };
 ```
 
```cpp
std::cout << std::format( "{:15.2f}", pi );
 ```

```cpp
std::cout << std::format( "{:15.{}f}", pi, precision );
 ```

```cpp
std::cout << std::format( "{:{}.{}f}", pi, width, precision );
 ```

```cpp
std::cout << std::format( "{0:{1}.{2}f}", pi, width, precision );
 ```

## Localization
	
std::locale is supported in std::format 
 
> **Note:** Use `:L` to enable locale specific formatting for an argument.
 
```cpp
#include <locale>
```

```cpp
std::cout << std::format( locale( "en_US.UTF-8" ), "{:L}", 1024 );
 ```

```cpp
std::cout << std::format( locale( "zh_CN.UTF-8" ), "{:L}", 1024 );
 ```
 
```cpp
std::cout << std::format( locale( "de_DE.UTF-8" ), "{:L}", 1024 );
 ```

## formating std::chrono
 
```cpp
#include <chrono>
```

### Example 1

```cpp
std::cout << std::format( "{:%d.%m.%Y}.", std::chrono::system_clock::now() ) << "\n";
```

### Example 2

```cpp
void print_happy_birthday( const std::string_view& name, const std::chrono::year_month_day& birthday )
{
	std::cout << std::format( "{0}'s birthday is {1:%Y-%m-%d}.", name, birthday ) << "\n";
}
```
	
```cpp
using namespace std::chrono;
year_month_day birthday { 1976y / February / 1 };
std::string name { "Max Mustermann" };

print_happy_birthday( name , birthday );
```
	
## formating std::complex
	
```cpp
#include <complex>
```

```cpp
std::complex<double> c { 4.0, 8.0 };
```

```cpp
std::cout << std::format( "{}", c );
```

	
## formating custom types

Seperate parsing and formatting in extension API

Need to provide a specialization of std::formater\<\> and imlpement

<ul>
 <li>formatter<>::parse()</li>
 <li>formatter<>::format()</li>
</ul>

### Example Person

```cpp
class Person
{
public:
	Person() = delete;
	Person( unsigned long long id, const std::string& firstName, const std::string& lastName ) noexcept
		: _id( id ), _firstName( firstName ), _lastName( lastName ) {}

	auto getId() const noexcept -> unsigned long long
	{
		return _id;
	}
	auto getFirstName() const noexcept -> const std::string&
	{
		return _firstName;
	}
	auto getLastName() const noexcept -> const std::string&
	{
		return _lastName;
	}

private:
	unsigned long long _id;
	std::string _firstName;
	std::string _lastName;
};
```

```cpp
template<>
class std::formatter<Person>
{
public:
	constexpr auto parse( auto& context )
	{
	
	}
	
	auto format( const Person& person, auto& context )
	{
	
	}
};
```

## Enum to String Formatting

```cpp
#include <format>
#include <iostream>
#include <string_view>

enum class Direction { North, East, South, West };

std::string_view to_string( Direction direction ) {
    switch (direction) {
	using enum Direction;
        case North: return "north";
        case East:  return "east";
        case South: return "south";
        case West:  return "west";
        default:    return "unknown";
    }
}

template<>
struct std::formatter<Direction> : std::formatter<std::string_view> {
    auto format( Direction direction, auto& context ) const {
        return std::formatter<std::string_view>::format( to_string( direction ), context );
    }
};

int main() {
    Direction direction = Direction::East;
    std::cout << std::format( "Direction: {}", direction ) << '\n';
}
```

[View example on Godbolt](https://godbolt.org/#z:OYLghAFBqd5QCxAYwPYBMCmBRdBLAF1QCcAaPECAMzwBtMA7AQwFtMQByARg9KtQYEAysib0QXACx8BBAKoBnTAAUAHpwAMvAFYTStJg1DIApACYAQuYukl9ZATwDKjdAGFUtAK4sGIM1ykrgAyeAyYAHI%2BAEaYxBLSAA6oCoRODB7evv6ByamOAqHhUSyx8VK2mPYFDEIETMQEmT5%2BAZXV6XUNBEWRMXEJtvWNzdltCsM9YX2lA1IAlLaoXsTI7BzmAMxhyN5YANQmm278xCxMBEfYJhoAgls7e5iHx04TxJisVzf3ZtsMuy8ByObneYWAAH0AG54TAAd2%2Bdx%2BjB8%2B12TAUCn2ABE8B8HOlDgB2Cz7CIkAgIUj7bAYgjUoTLSnUgDqmAmxOxRysSLuE3QIBAYKM0NhcP2RAhwuAEBxeMwBIE%2B3w%2BJq%2B3mxJ5t32Ov2CjhhGQCH2EBVCpqGpMJJ%2Butt%2By8qSM%2BxRLDlqvS3Jtdp1oiUZIpSH2HwIKwYhzMZgYAfMZk9d29Poxz1pExAOuDofDZk%2BExjce1Cd9z0ZXkpaYzxDDMYUTIQec2WoTaKT%2BzZqfTmBDlazcPZlwj%2BabWCoTC8tAIad1FarEa8DAA1lG4Qx643dVauUiiZv7ncCJgWIkDPuQYjbu8vA49QQBSBTucCPviCDce6BFd9mn%2BYL7xcnyDvyFAhiHBUV4Q/K01x1UciH2X8CFlV9zUJM1FQYakYNQcwADY0VkTBVAIdU8IYDlIK9b1p2vW94P/Y5AOlMCEU2bAfxIB9ZUlaVZVQtVFhI/dCPVQd123H4N3zH4wiI84wggS1rXjXUkLQ5V5VUo5sTdZDnBAFNLgbCjqMFNBSxeNwQWMu92IuWUYxUmo03IsSI2pXjCUtY5LLADYAFY3AYHzJO3DhFloThfN4PwOC0UhUE4CzLGsPVllWZ4th4UgJxi0LFnnEBfLMAA6LgAgADi4IkzCJSQNDK%2BqiX0ThJCizReHijheAUEANCytrFjgWAYEQFBUEPOg4nISg0HG%2Bh4mAKQzD4Ogn26iBoja0hojCBoAE9OEy7bmGIXaAHlom0c0Dt4Ga2EEU6GFofactILBoi8YA3DEWhuu4XgsHOIxxBe9yoXZTaCIVUt1li6Sqk22g8GiYg9o8LBNuAvAWE2sHiGiFJMGxA9DGARGjH6vgDGABQADUxVOxJGGumRBBEMR2AqfhBEUFR1Be3RAgMcnTCSyx9CR7rIEWVBEhqX79gAWn5TSRasSwzA0RXTsy1BcZArBJfk9odL8CBXFGPxAhCaYSjKPQ8jSAQLftlJHYYXpbbmY20K6EZPBaPQ7BN32pmKfpyiGbpncCCZug98OJEWGsVjWROmo4SLSGi2KOv2VQyuwhXsMkfZgGQZB9ikIqzBNXBCBIcNNi4eZeGyrR5kWBBPiweIjfyyRiskTZNmL7DfKJDRfI0SQKnCjgWtIbGapKswyoATjKyQh7MNeuE2aqs82jqup6vqcoG4aICQJlElLKaIBmxIJuICJWHWfPC%2BL0vy8ryRq94TA%2BAiD6z0FzYQohxCc1kDzNQm0BakDhCjRI10woRVai9Dqp1Sy3yIqgKgecC5FxLmXCuVca4QA8LNOIjdm6t36p3buAwjZzwXtjMwvkiplSJFwDQXBfK%2BWwhPAuRJNiHwwZwE%2BvU265VIP3IknCiQVTKtVdhu8uB73TpsdBOcJFn3bqgjgZhtHtV0dIjupBcapGcJIIAA%3D%3D%3D)
