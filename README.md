# std::format cheatsheet

![std::format cheatsheet](https://i.imgur.com/tDqRjOx.png)

If you like this content, you can contact me or follow me on Twitter :+1:

[![Tweet for help](https://img.shields.io/twitter/follow/paulkazusek?label=Tweet%20%40paulkazusek&style=social)](https://twitter.com/paulkazusek/)

## Table of Contents

- [std::format in C++20](#stdformat-in-c20)
	* [Table of contents](#table-of-contents)
	* [Requirement](#Requirement)
	* [Currently ways to formatting in C++](#currently-ways-to-formatting-in-c)
		+ [C-Style printf() from \<cstdio\>](#c-style-printf-from-)
		+ [C++ I/O streams](#c-io-streams)
		+ [Boost Format](#boost-format)
		+ [Fast Format](#fast-format)
		+ [std::format in \<format\>](#stdformat-in-format)
	* [Placeholder](#placeholder)


## Requirement

| compiler | version  |
|:--------:|:-------------:|
| Visual Studio | Version 16.10 / cl 19.29 |
| GCC | ??? |
| clang | ??? |

```cpp
#include <format>
 ```
    
## Currently ways to formatting in C++

### C-Style printf() from \<cstdio\>

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
 
### std::format in \<format\>
 
```cpp
int answer { 42 };

std::cout << std::format( "The answer is {}", answer );
 ```
 
## Placeholder
 
### Brace-delimited replacement fields
 
```cpp
std::cout << std::format( "The answer is {}", 42 );
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
double pi { 3.1415 };
int precision { 2 };
int width { 15 };
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
std::cout << std::format( "{}", c);
```

	
## formating custom types

Seperate parsing anf formatting in extension API

Need to provide a specialization of std::formater\<\> and imlpement

<ul>
 <li>formatter<>::parse()</li>
 <li>formatter<>::fomrat()</li>
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
	const char* parse(std::string_view format)
	{
	
	}
	
	void format( buffer& buf, const Person& person, context& ctx )
	{
	
	}
};
```
