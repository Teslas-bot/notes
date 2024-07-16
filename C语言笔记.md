# 第一个程序

```c
#include <stdio.h>
// include 包含: 包括stdio.h	std标准	std io
// input 输入
// output 输出 h head头文件 一种文件格式 .mp4 视频格式		.mp3 .flac 音频格式
// .png .jpg 图片格式
// .c 这个文件就是c语言的代码文件	.h c语言的独特的头文件

// main(主要的) 主函数
// {}中间，函数体body
int main(void)
{
    printf("Hello world!\n");
    // print 打印 f format 格式 格式化输出	\n回车换行(转义字符)
    
    return 0;
}
```

# C Language Reference

Microsoft C Reference: [C Language Reference | Microsoft Learn](https://learn.microsoft.com/en-us/cpp/c-language/c-language-reference?view=msvc-170)

## Elements of C

This section describes the elements of the C programming language, including the names, numbers, and characters used to construct a C program. The ANSI C syntax labels these components tokens.

This section explains how to define tokens and how the compiler evaluates them.

The following topics are discussed:

- [Tokens](https://learn.microsoft.com/en-us/cpp/c-language/c-tokens?view=msvc-170)
- [Comments](https://learn.microsoft.com/en-us/cpp/c-language/c-comments?view=msvc-170)
- [Keywords](https://learn.microsoft.com/en-us/cpp/c-language/c-keywords?view=msvc-170)
- [Identifiers](https://learn.microsoft.com/en-us/cpp/c-language/c-identifiers?view=msvc-170)
- [Constants](https://learn.microsoft.com/en-us/cpp/c-language/c-constants?view=msvc-170)
- [String literals](https://learn.microsoft.com/en-us/cpp/c-language/c-string-literals?view=msvc-170)
- [Punctuation and special characters](https://learn.microsoft.com/en-us/cpp/c-language/punctuation-and-special-characters?view=msvc-170)

### C tokens

Example:

```c
int main(void)
{
    int number = 1;
    
    return 0;
}

// 帮助编译器确定代码的语义和结构
// This is a pencil that is a pen.
// 单词可以类比token, 标点可以类比代码结构的标识符如：() ; {}
```

### White-space Characters

空格、制表符、换行符（创建新行）、回车符、换页符、垂直制表符称为“空白字符”，因为它们与打印页上的单词和行之间的空格一样都是起到方便阅读的作用。 标记由空白字符和其他标记分隔（划分边界），如运算符和标点。 在分析代码时，C 编译器将忽略空白字符，除非您将它们用作分隔符或者字符常量或字符串文本的组成部分。 使用空白字符可以让程序更易于阅读。 请注意，编译器也将注释视为空白。

#### 制表符

* 编辑器的自动缩进
* 可以定制间隔
* 简化编辑
* tab 4space 8space ... os app
* 空格是在单词或句子中创建间隔，而制表符是为了创建结构化和对齐的文本块
* 同一个项目中tab 4space 8space 应提前定义，保持一致性

#### C Identifiers——标识符

相当于起名字。

"Identifiers" or "symbols" are the **names** you supply for variables, types, functions, and labels in your program. Identifier names must differ in spelling and case from any keywords. You can't use keywords (either C or Microsoft) as identifiers; they're reserved for special use. You create an identifier by specifying it in the declaration of a variable, type, or function. In this example, `result` is an identifier for an integer variable, and `main` and `printf` are identifier names for functions.

```c
#include <stdio.h>

int main()
{
    int result;

    if ( result != 0 )
        printf_s( "Bad file handle\n" );
}
```

Once declared, you can use the identifier in later program statements to refer to the associated value.

##### Syntax

*`identifier`*:
 *`nondigit`*
 *`identifier`* *`nondigit`*
 *`identifier`* *`digit`*

*`nondigit`*: one of
 **`_ a b c d e f g h i j k l m n o p q r s t u v w x y z`**
 **`A B C D E F G H I J K L M N O P Q R S T U V W X Y Z`**

*`digit`*: one of
 **`0 1 2 3 4 5 6 7 8 9`**

#### C Keywords

*Keywords* are words that have special meaning to the C compiler. In translation phases 7 and 8, an identifier can't have the same spelling and case as a C keyword. For more information, see [translation phases](https://learn.microsoft.com/en-us/cpp/preprocessor/phases-of-translation?view=msvc-170) in the *Preprocessor Reference*. For more information on identifiers, see [Identifiers](https://learn.microsoft.com/en-us/cpp/c-language/c-identifiers?view=msvc-170).

##### Standard C Keywords

The C language uses the following keywords:

| **`auto`**     | **`extern`**        | **`short`**                                                  | **`while`**                                                  |
| -------------- | ------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **`break`**    | **`float`**         | **`signed`**                                                 | **[`_Alignas`](https://learn.microsoft.com/en-us/cpp/c-language/alignment-c?view=msvc-170#alignas-and-_alignas-c11)** 2, a |
| **`case`**     | **`for`**           | **`sizeof`**                                                 | **[`_Alignof`](https://learn.microsoft.com/en-us/cpp/c-language/alignment-c?view=msvc-170#alignof-and-_alignof-c11)** 2, a |
| **`char`**     | **`goto`**          | **`static`**                                                 | **`_Atomic`** 2, b                                           |
| **`const`**    | **`if`**            | **`struct`**                                                 | **`_Bool`** 1, a                                             |
| **`continue`** | **`inline`** 1, a   | **`switch`**                                                 | **`_Complex`** 1, b                                          |
| **`default`**  | **`int`**           | **`typedef`**                                                | **[`_Generic`](https://learn.microsoft.com/en-us/cpp/c-language/generic-selection?view=msvc-170)** 2, a |
| **`do`**       | **`long`**          | **[`typeof`](https://learn.microsoft.com/en-us/cpp/c-language/typeof-c?view=msvc-170)** | **`_Imaginary`** 1, b                                        |
| **`double`**   | **`register`**      | **[`typeof_unqual`](https://learn.microsoft.com/en-us/cpp/c-language/typeof-unqual-c?view=msvc-170)** | **`_Noreturn`** 2, a                                         |
| **`else`**     | **`restrict`** 1, a | **`union`**                                                  | **`_Static_assert`** 2, a                                    |
| **`enum`**     | **`return`**        | **`unsigned`**                                               | **`_Thread_local`** 2, b                                     |
|                |                     | **`void`**                                                   |                                                              |
|                |                     | **`volatile`**                                               |                                                              |

1 Keywords introduced in ISO C99.
2 Keywords introduced in ISO C11.
a Starting in Visual Studio 2019 version 16.8, these keywords are supported in code compiled as C when the **`/std:c11`** or **`/std:c17`** compiler options are specified.
b Starting in Visual Studio 2019 version 16.8, these keywords are recognized but not supported by the compiler in code compiled as C when the **`/std:c11`** or **`/std:c17`** compiler options are specified.

You can't redefine keywords. However, you can specify text to replace keywords before compilation by using C preprocessor directives.

# 变量

类比推**购物车**去商店买**果汁**、**碳酸饮料**等。

# Format specification syntax: `printf` and `wprintf` functions（格式化输出）

源链接：[Format Specification Syntax: `printf` and `wprintf` Functions | Microsoft Learn](https://learn.microsoft.com/en-us/cpp/c-runtime-library/format-specification-syntax-printf-and-wprintf-functions?view=msvc-170#flags)

```c
int main()
{
    int number = 100;
    
    // 以八进制表示
    printf("Octal:%o", number);
    
    // 以十进制表示
    printf("Decimal:%d", number);
    
    // 以小写十六进制表示
    printf("Hexadecimal(Lowercase):%x", number);
    
    // 以大写十六进制表示
    printf("Hexadecimal(Uppercase):%x", number);
    
    // 以八进制表示并输出
    printf("Octal:%#o\n", number);

    // 以小写十六进制表示并输出
    printf("Hexadecimal(Lowercase):%#x\n", number);

    // 以大写十六进制表示并输出
    printf("Hexadecimal(Uppercase)%#X\n", number);
}
```

A conversion specification consists of optional and required fields in this form:

```c
%[flags][width][.precision][size]type
```

```c
%[标志][宽度][.精度][大小]类型
```

## Type field characters

Expand table

| Type character | Argument                                    | Output format                                                |
| :------------- | :------------------------------------------ | :----------------------------------------------------------- |
| **`c`**        | Character                                   | When used with `printf` functions, specifies a single-byte character; when used with `wprintf` functions, specifies a wide character. |
| **`C`**        | Character                                   | When used with `printf` functions, specifies a wide character; when used with `wprintf` functions, specifies a single-byte character. |
| **`d`**        | Integer                                     | Signed decimal integer.                                      |
| **`i`**        | Integer                                     | Signed decimal integer.                                      |
| **`o`**        | Integer                                     | Unsigned octal integer.                                      |
| **`u`**        | Integer                                     | Unsigned decimal integer.                                    |
| **`x`**        | Integer                                     | Unsigned hexadecimal integer; uses "`abcdef`".               |
| **`X`**        | Integer                                     | Unsigned hexadecimal integer; uses "`ABCDEF`".               |
| **`e`**        | Floating-point                              | Signed value that has the form [`-`]*d.dddd*`e`[`+`|`-`]*dd*[*d*], where *d* is one decimal digit, *dddd* is one or more decimal digits depending on the specified precision, or six by default, and *dd*[*d*] is two or three decimal digits depending on the [output format](https://learn.microsoft.com/en-us/cpp/c-runtime-library/set-output-format?view=msvc-170) and size of the exponent. |
| **`E`**        | Floating-point                              | Identical to the **`e`** format except that **`E`** rather than **`e`** introduces the exponent. |
| **`f`**        | Floating-point                              | Signed value that has the form [`-`]*dddd*`.`*dddd*, where *dddd* is one or more decimal digits. The number of digits before the decimal point depends on the magnitude of the number, and the number of digits after the decimal point depends on the requested precision, or six by default. |
| **`F`**        | Floating-point                              | Identical to the **`f`** format except that infinity and NaN output is capitalized. |
| **`g`**        | Floating-point                              | Signed values are displayed in **`f`** or **`e`** format, whichever is more compact for the given value and precision. The **`e`** format is used only when the exponent of the value is less than -4 or greater than or equal to the *precision* argument. Trailing zeros are truncated, and the decimal point appears only if one or more digits follow it. |
| **`G`**        | Floating-point                              | Identical to the **`g`** format, except that **`E`**, rather than **`e`**, introduces the exponent (where appropriate). |
| **`a`**        | Floating-point                              | Signed hexadecimal double-precision floating-point value that has the form [`-`]`0x`*h.hhhh*`p`[`+`|`-`]*dd*, where *h.hhhh* are the hex digits (using lower case letters) of the mantissa, and *dd* are one or more digits for the exponent. The precision specifies the number of digits after the point. |
| **`A`**        | Floating-point                              | Signed hexadecimal double-precision floating-point value that has the form [`-`]`0X`*h.hhhh*`P`[`+`|`-`]*dd*, where *h.hhhh* are the hex digits (using capital letters) of the mantissa, and *dd* are one or more digits for the exponent. The precision specifies the number of digits after the point. |
| **`n`**        | Pointer to integer                          | Number of characters that are successfully written so far to the stream or buffer. This value is stored in the integer whose address is given as the argument. The size of the integer pointed at can be controlled by an argument size specification prefix. The **`n`** specifier is disabled by default; for information see the important security note. |
| **`p`**        | Pointer type                                | Display the argument as an address in hexadecimal digits.    |
| **`s`**        | String                                      | When used with `printf` functions, specifies a single-byte or multi-byte character string; when used with `wprintf` functions, specifies a wide-character string. Characters are displayed up to the first null character or until the *precision* value is reached. |
| **`S`**        | String                                      | When used with `printf` functions, specifies a wide-character string; when used with `wprintf` functions, specifies a single-byte or multi-byte character string. Characters are displayed up to the first null character or until the *precision* value is reached. |
| **`Z`**        | `ANSI_STRING` or `UNICODE_STRING` structure | **VS 2013 and earlier** When the address of an [`ANSI_STRING`](https://learn.microsoft.com/en-us/windows/win32/api/ntdef/ns-ntdef-string) or [`UNICODE_STRING`](https://learn.microsoft.com/en-us/windows/win32/api/ntdef/ns-ntdef-_unicode_string) structure is passed as the argument, display the string contained in the buffer pointed to by the `Buffer` field of the structure. Use a *size* modifier prefix of **`w`** to specify a `UNICODE_STRING` argument—for example, `%wZ`. The `Length` field of the structure must be set to the length, in bytes, of the string. The `MaximumLength` field of the structure must be set to the length, in bytes, of the buffer.  **Universal C Runtime (UCRT)** There is a known issue in the UCRT that is currently maintained for compatibility. Like the **`S`** specifier, the **`Z`** specifier without a size modifier prefix refers to a `UNICODE_STRING` when using a narrow printing function (like `printf`) and an `ANSI_STRING` when using a wide printing function (like `wprintf`). Instead of **`Z`**, use **`hZ`** to specify an `ANSI_STRING`. **`wZ`** (or **`lZ`**) can still be used to specify a `UNICODE_STRING`.  Typically, the **`Z`** type character is used only in driver debugging functions that use a conversion specification, such as `dbgPrint` and `kdPrint`. |

In Visual Studio 2015 and later versions, if the argument that corresponds to a floating-point conversion specifier (**`a`**, **`A`**, **`e`**, **`E`**, **`f`**, **`F`**, **`g`**, **`G`**) is infinite, indefinite, or NaN, the formatted output conforms to the C99 standard. This table lists the formatted output:

Expand table

| Value          | Output      |
| :------------- | :---------- |
| Infinity       | `inf`       |
| Quiet NaN      | `nan`       |
| Signaling NaN  | `nan(snan)` |
| Indefinite NaN | `nan(ind)`  |

Any of these strings may be prefixed by a sign. If a floating-point *type* conversion specifier character is a capital letter, then the output is also formatted in capital letters. For example, if the format specifier is `%F` instead of `%f`, an infinity is formatted as `INF` instead of `inf`. The `scanf` functions can also parse these strings, so these values can make a round trip through `printf` and `scanf` functions.

Before Visual Studio 2015, the CRT used a different, non-standard format for output of infinite, indefinite, and NaN values:

Expand table

| Value                          | Output                          |
| :----------------------------- | :------------------------------ |
| + Infinity                     | `1.#INF` *random-digits*        |
| - Infinity                     | `-1.#INF` *random-digits*       |
| Indefinite (same as quiet NaN) | *digit* `.#IND` *random-digits* |
| NaN                            | *digit* `.#NAN` *random-digits* |

Any of these strings may have been prefixed by a sign, and may have been formatted differently depending on field width and precision, sometimes with unusual effects. For example, `printf("%.2f\n", INFINITY)` prints `1.#J` because the *#INF* would be "rounded" to two digits of precision.

## Flag directives

The first optional field in a conversion specification contains *flag directives*. This field contains zero or more flag characters that specify output justification and control output of signs, blanks, leading zeros, decimal points, and octal and hexadecimal prefixes. More than one flag directive may appear in a conversion specification, and the flag characters can appear in any order.

### Flag characters

| Flag            | Meaning                                                      | Default                                                      |
| :-------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| **`-`**         | Left align the result within the given field width.          | Right align.                                                 |
| **`+`**         | Use a sign (+ or -) to prefix the output value if it's of a signed type. | Sign appears only for negative signed values (-).            |
| **`0`**         | If *width* is prefixed by **`0`**, leading zeros are added until the minimum width is reached. If both **`0`** and **`-`** appear, the **`0`** is ignored. If **`0`** is specified for an integer format (**`i`**, **`u`**, **`x`**, **`X`**, **`o`**, **`d`**) and a precision specification is also present—for example, `%04.d`—the **`0`** is ignored. If **`0`** is specified for the **`a`** or **`A`** floating-point format, leading zeros are prepended to the mantissa, after the `0x` or `0X` prefix. | No padding.                                                  |
| **blank (' ')** | Use a blank to prefix the output value if it's signed and positive. The blank is ignored if both the blank and + flags appear. | No blank appears.                                            |
| **`#`**         | When it's used with the **`o`**, **`x`**, or **`X`** format, the **`#`** flag uses `0`, `0x`, or `0X`, respectively, to prefix any nonzero output value. | No prefix appears.                                           |
|                 | When it's used with the **`e`**, **`E`**, **`f`**, **`F`**, **`a`**, or **`A`** format, the **`#`** flag forces the output value to contain a decimal point. | Decimal point appears only if digits follow it.              |
|                 | When it's used with the **`g`** or **`G`** format, the **`#`** flag forces the output value to contain a decimal point and prevents the truncation of trailing zeros.  Ignored when used with **`c`**, **`d`**, **`i`**, **`u`**, or **`s`**. | Decimal point appears only if digits follow it. Trailing zeros are truncated. |

## Width specification

In a conversion specification, the optional width specification field appears after any *flags* characters. The *`width`* argument is a non-negative decimal integer that controls the minimum number of characters that are output. If the number of characters in the output value is less than the specified width, blanks are added to the left or the right of the values—depending on whether the left-alignment flag (**`-`**) is specified—until the minimum width is reached. If *`width`* is prefixed by 0, leading zeros are added to integer or floating-point conversions until the minimum width is reached, except when conversion is to an infinity or `NaN`.

The width specification never causes a value to be truncated. If the number of characters in the output value is greater than the specified width, or if *`width`* isn't provided, all characters of the value are output, subject to the precision specification.

If the width specification is an asterisk (`*`), an `int` argument from the argument list supplies the value. The *`width`* argument must precede the value that's being formatted in the argument list, as shown in this example:

```
printf("%0*d", 5, 3); /* 00003 is output */
```

A missing or small *`width`* value in a conversion specification doesn't cause the truncation of an output value. If the result of a conversion is wider than the *`width`* value, the field expands to contain the conversion result.



## Precision specification

In a conversion specification, the third optional field is the precision specification. It consists of a period (`.`) followed by a non-negative decimal integer that, depending on the conversion type, specifies the number of string characters, the number of decimal places, or the number of significant digits to be output.

Unlike the width specification, the precision specification can cause either truncation of the output value or rounding of a floating-point value. If *`precision`* is specified as 0, and the value to be converted is 0, the result is no characters output, as shown in this example:

```
printf( "%.0d", 0 ); /* No characters output */
```

If the precision specification is an asterisk (`*`), an `int` argument from the argument list supplies the value. In the argument list, the *`precision`* argument must precede the value that's being formatted, as shown in this example:

```
printf( "%.*f", 3, 3.14159265 ); /* 3.142 output */
```

The *`type`* character determines either the interpretation of *`precision`* or the default precision when *`precision`* is omitted, as shown in the following table.

### How precision values affect type

Expand table

| Type                                                 | Meaning                                                      | Default                                                      |
| :--------------------------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| **`a`**, **`A`**                                     | The precision specifies the number of digits after the point. | Default precision is 13. If precision is 0, no decimal point is printed unless the **`#`** flag is used. |
| **`c`**, **`C`**                                     | The precision has no effect.                                 | Character is printed.                                        |
| **`d`**, **`i`**, **`o`**, **`u`**, **`x`**, **`X`** | The precision specifies the minimum number of digits to be printed. If the number of digits in the argument is less than *precision*, the output value is padded on the left with zeros. The value isn't truncated when the number of digits exceeds *precision*. | Default precision is 1.                                      |
| **`e`**, **`E`**                                     | The precision specifies the number of digits to be printed after the decimal point. The last printed digit is rounded. | Default precision is 6. If *precision* is 0 or the period (`.`) appears without a number following it, no decimal point is printed. |
| **`f`**, **`F`**                                     | The precision value specifies the number of digits after the decimal point. If a decimal point appears, at least one digit appears before it. The value is rounded to the appropriate number of digits. | Default precision is 6. If *precision* is 0, or if the period (`.`) appears without a number following it, no decimal point is printed. |
| **`g`**, **`G`**                                     | The precision specifies the maximum number of significant digits printed. | Six significant digits are printed, and any trailing zeros are truncated. |
| **`s`**, **`S`**                                     | The precision specifies the maximum number of characters to be printed. Characters in excess of *precision* aren't printed. | Characters are printed until a null character is found.      |

## Argument size specification

In a conversion specification, the *size* field is an argument length modifier for the *type* conversion specifier. The *size* field prefixes to the *type* field—**`hh`**, **`h`**, **`j`**, **`l`** (lowercase L), **`L`**, **`ll`**, **`t`**, **`w`**, **`z`**, **`I`** (uppercase i), **`I32`**, and **`I64`**—specify the "size" of the corresponding argument—long or short, 32-bit or 64-bit, single-byte character or wide character—depending on the conversion specifier that they modify. These size prefixes are used with *type* characters in the `printf` and `wprintf` families of functions to specify the interpretation of argument sizes, as shown in the following table. The *size* field is optional for some argument types. When no size prefix is specified, the formatter consumes integer arguments—for example, signed or unsigned `char`, `short`, `int`, `long`, and enumeration types—as 32-bit `int` types, and `float`, `double`, and `long double` floating-point arguments are consumed as 64-bit `double` types. This behavior matches the default argument promotion rules for variable argument lists. For more information about argument promotion, see Ellipsis and Default Arguments in [Postfix expressions](https://learn.microsoft.com/en-us/cpp/cpp/postfix-expressions?view=msvc-170). On both 32-bit and 64-bit systems, the conversion specification of a 64-bit integer argument must include a size prefix of **`ll`** or **`I64`**. Otherwise, the behavior of the formatter is undefined.

Some types are different sizes in 32-bit and 64-bit code. For example, `size_t` is 32 bits long in code compiled for x86, and 64 bits in code compiled for x64. To create platform-agnostic formatting code for variable-width types, you can use a variable-width argument size modifier. Instead, use a 64-bit argument size modifier and explicitly promote the variable-width argument type to 64 bits. The Microsoft-specific **`I`** (uppercase i) argument size modifier handles variable-width integer arguments, but we recommend the type-specific **`j`**, **`t`**, and **`z`** modifiers for portability.

### Size prefixes for printf and wprintf format-type specifiers

Expand table

| To specify                               | Use prefix                       | With type specifier                                          |
| :--------------------------------------- | :------------------------------- | :----------------------------------------------------------- |
| `char` `unsigned char`                   | **`hh`**                         | **`d`**, **`i`**, **`o`**, **`u`**, **`x`**, or **`X`**      |
| `short int` `short unsigned int`         | **`h`**                          | **`d`**, **`i`**, **`o`**, **`u`**, **`x`**, or **`X`**      |
| `__int32` `unsigned __int32`             | **`I32`**                        | **`d`**, **`i`**, **`o`**, **`u`**, **`x`**, or **`X`**      |
| `__int64` `unsigned __int64`             | **`I64`**                        | **`d`**, **`i`**, **`o`**, **`u`**, **`x`**, or **`X`**      |
| `intmax_t` `uintmax_t`                   | **`j`** or **`I64`**             | **`d`**, **`i`**, **`o`**, **`u`**, **`x`**, or **`X`**      |
| `long double`                            | **`l`** (lowercase L) or **`L`** | **`a`**, **`A`**, **`e`**, **`E`**, **`f`**, **`F`**, **`g`**, or **`G`** |
| `long int` `long unsigned int`           | **`l`** (lowercase L)            | **`d`**, **`i`**, **`o`**, **`u`**, **`x`**, or **`X`**      |
| `long long int` `unsigned long long int` | **`ll`** (lowercase LL)          | **`d`**, **`i`**, **`o`**, **`u`**, **`x`**, or **`X`**      |
| `ptrdiff_t`                              | **`t`** or **`I`** (uppercase i) | **`d`**, **`i`**, **`o`**, **`u`**, **`x`**, or **`X`**      |
| `size_t`                                 | **`z`** or **`I`** (uppercase i) | **`d`**, **`i`**, **`o`**, **`u`**, **`x`**, or **`X`**      |
| Single-byte character                    | **`h`**                          | **`c`** or **`C`**                                           |
| Wide character                           | **`l`** (lowercase L) or **`w`** | **`c`** or **`C`**                                           |
| Single-byte character string             | **`h`**                          | **`s`**, **`S`**, or **`Z`**                                 |
| Wide-character string                    | **`l`** (lowercase L) or **`w`** | **`s`**, **`S`**, or **`Z`**                                 |

The `ptrdiff_t` and `size_t` types are `__int32` or `unsigned __int32` on 32-bit platforms, and `__int64` or `unsigned __int64` on 64-bit platforms. The **`I`** (uppercase i), **`j`**, **`t`**, and **`z`** size prefixes take the correct argument width for the platform.

In Visual C++, although `long double` is a distinct type, it has the same internal representation as `double`.

An **`hc`** or **`hC`** type specifier is synonymous with **`c`** in `printf` functions and with **`C`** in `wprintf` functions. A **`lc`**, **`lC`**, **`wc`**, or **`wC`** type specifier is synonymous with **`C`** in `printf` functions and with **`c`** in `wprintf` functions. An **`hs`** or **`hS`** type specifier is synonymous with **`s`** in `printf` functions and with **`S`** in `wprintf` functions. An **`ls`**, **`lS`**, **`ws`**, or **`wS`** type specifier is synonymous with **`S`** in `printf` functions and with **`s`** in `wprintf` functions.

# 数据类型

## integer

### integer overflow(整型溢出)

#### 有符号上溢

```
0111 1111 1111 1111 1111 1111 1111 1111
```

上面是整型的最大值2,147,483,647，若再+1将溢出。由于计算机中的数据是以补码的形式存储和计算的，我们下面将采用补码的方式进行计算。

上面数据的补码为：

```
0111 1111 1111 1111 1111 1111 1111 1111
```

+1后的补码为：

```
1000 0000 0000 0000 0000 0000 0000 0000
```

这个补码代表的是-2,147,483,648

4位中-1的补码：`1111`
4位中-2的补码：`1110`
以此类推，4位中-8的补码是特殊的：`1000`

故32位(4个字节)中-2^32的补码是特殊的，为：

```
1000 0000 0000 0000 0000 0000 0000 0000
```

#### 有符号下溢

以4位数据为例

-4的补码为：`1100`，-5的补码为：`1011`。二者之和为：`0111`，为7的补码，产生有符号整型下溢。

### Summary of inerger overflow

总结：数据可以认为是循环的，以8位uint类型为例：255 + 1 = 0，0 - 1 = 255。以8位int类型为例：127+1 = -128，-128 - 1 = 0。

### unsigned int(uint)

在使用index等非负数时，一定注意使用`unsigned int`而不是`int`。这是企业中最基本的规范。

### short

`short`类型的范围是-32768~32767，常用于小数据。在嵌入式系统中由于内存空间的珍贵，常使用`short`类型。而在游戏开发中，针对屏幕像素的坐标，常使用`unsigned short`类(4k:3840×2160)。在使用RGB表示色彩时，也常用`unsigned short`类型。甚至是u8。

### long type and long long type

long type: 4 Bytes on x86	8 Bytes on x64	
To be compatible with x86 and x64 architectures

long long type: 8 Bytes

### 查看数据类型所占字节数

C语言中查看类型所占字节数使用`sizeof()`函数，例如`sizeof(int)`是查看`int`类型所占字节数。返回的数据类型为`size_t`类型，是一种专门用于显示数据类型所占字节空间长度的类型。`sizeof()`函数在编译过程中执行，其结果由CPU架构（32位or64位）和操作系统共同决定。

如：在Windows操作系统中，`long`的长度为4个字节（无论32位还是64位）。而在Unix或类Unix操作系统中，`long`的长度在32位系统下为4个字节，在64位系统下为8个字节。

在`printf`的格式化输出中，输出`size_t`数据类型的占位符前需要加修饰前缀`j`,`t`,`z`等。常使用`%zu`作为`size_t`数据类型的占位符。

The `ptrdiff_t` and `size_t` types are `__int32` or `unsigned __int32` on 32-bit platforms, and `__int64` or `unsigned __int64` on 64-bit platforms. The **`I`** (uppercase i), **`j`**, **`t`**, and **`z`** size prefixes take the correct argument width for the platform.

```c
/*  32位 */
typedef unsigned int    size_t;
typedef int             ssite_t;
 
/*  64位 */
typedef unsigned long   size_t;
typedef long            ssize_t;
```

### 查看常见数据类型长度举例

```c
#include <stdio.h>

int main(void)
{
    printf("The size of char is %zu byte(s).\n", sizeof(char));

    printf("The size of short is %zu byte(s).\n", sizeof(short));

    printf("The size of unsigned short is %zu byte(s).\n", sizeof(unsigned short));

    printf("The size of int is %zu byte(s).\n", sizeof(int));

    printf("The size of unsigned int is %zu byte(s).\n", sizeof(unsigned int));

    printf("The size of long is %zu byte(s).\n", sizeof(long));

    printf("The size of unsigned long is %zu byte(s).\n", sizeof(unsigned long));

    printf("The size of long long is %tu byte(s).\n", sizeof(long long));

    printf("The size of unsigned long long is %zu byte(s).\n", sizeof(unsigned long long));
}
```

### `<stdint.h>`Fixed-width integer 跨平台的int标准

由于在不同的操作系统中，`short`, `int`, `long`, `long long`等类型的长度会随 操作系统的改变而改变。故在C99标准后使用引入`<stdint.h>`头文件的方式来避免这个问题。在进行跨平台开发时，应使用`<stdint.h>`中的数据类型，如：`int8_t `, `uint16_t`等等。在这个库的定义中，直接忽略了`long`在不同平台长度不同的问题，避免使用`long`。

示例：

```c
#include <stdio.h>
#include <stdint.h>

int main()
{
    int16_t myInt16 = 32767;
    uint16_t myUInt16 = 65535;

    int32_t myInt32 = 2147483647;
    uint32_t myUInt32 = 4294967295U;

    int64_t myInt64 = 9223372036854775807LL;
    uint64_t myUInt64 = 18446744073709551615ULL;

    printf("Size of int16_t is %zu byte(s).\n", sizeof(myInt16));
    printf("Size of uint16_t is %zu byte(s).\n", sizeof(myUInt16));
    printf("Size of int32_t is %zu byte(s).\n", sizeof(myInt32));
    printf("Size of uint32_t is %zu byte(s).\n", sizeof(myUInt32));
    printf("Size of int64_t is %zu byte(s).\n", sizeof(myInt64));
    printf("Size of uint64_t is %zu byte(s).\n", sizeof(myUInt64));

    printf("myInt16 is %hd.\n", myInt16);
    printf("myUInt16 is %hu.\n", myUInt16);
    printf("myInt32 is %d.\n", myInt32);
    printf("myUInt32 is %u.\n", myUInt32);
    printf("myInt32 is %ld.\n", myInt32);
    printf("myUInt32 is %lu.\n", myUInt32);
    printf("myInt64 is %lld.\n", myInt64);
    printf("myUInt64 is %llu.\n", myUInt64);
}
```

事实上，在考虑使用int等老标准还是使用uint32_t这种新标准时需要综合考虑。使用int等老标准时，给予了操作系统一定的灵活性去处理所需要的长度。而使用uint32_t新标准时，在所有操作系统中都固定了变量的长度。二者各有优势，在需要向下兼容的软件中，例如Linux。为保证在32位、64位、甚至是16位等各种新老设备中都能正常运行，一部分核心代码仍采用int等老标准。而在网络通信这种双方需要对齐变量长度的场景时，uint32_t的新标准则是更好的选择。在无需考虑多设备兼容时，uint32_t的新标准是更好的选择。在现有的软件开发过程中，大都需要确定宽度。如果需要确定宽度，就使用新标准。如果不能确定宽度，就使用老标准。

### Fixed-width integer format output `<inttypes>`

```c
#include <stdio.h>
#include <stdint.h>
#include <inttypes.h>

int main()
{
	int8_t myInt8 = INT8_MAX;
    int16_t myInt16 = INT16_MAX;
    int32_t myInt32 = INT32_MAX;
    int64_t myInt64 = INT64_MAX;
    uint8_t myInt8 = UINT8_MAX;
    uint16_t myUInt16 = UINT16_MAX;
    uint32_t myUInt32 = UINT32_MAX;
    uint64_t myUInt64 = UINT64_MAX;
    
    printf("The maximum of int8 is %" PRId8 ".\n", myInt8);
    printf("The maximum of int16 is %" PRId16 ".\n", myInt16);
    printf("The maximum of int32 is %" PRId32 ".\n", myInt32);
    printf("The maximum of int64 is %" PRId64 ".\n", myInt64);
    printf("The maximum of uint8 is %" PRIu8 ".\n", myUInt8);
    printf("The maximum of uint16 is %" PRIu16 ".\n", myUInt16);
    printf("The maximum of uint32 is %" PRIu32 ".\n", myUInt32);
    printf("The maximum of uint64 is %" PRIu64 ".\n", myUInt64);
}
```

常用的格式化字符如`%d`等这类的字符是可以由程序员自定义的。同时，这种格式化字符可读性不好。使用`<inttypes>`中的宏进行替换显然是更好的选择。

### The use of int_leastX_t and int_fastX_t

```c
#include <stdio.h>
#include <stdint.h>
#include <inttypes.h>

int main()
{
    // 玩家分数初始分
    int_least32_t playerScore = 5000;

    // 初始化像素值
    int_fast32_t pixelValue = 128;
    
    // output of playeerScore
    printf("The score of this player is %" PRIdLEAST32 ".\n", playerScore);

    // output of pixel value
    printf("The value of pixel is %" PRIdFAST32 ".\n", pixelValue);
}
```

### The difference of int_leastX_t, int_fastX_t and intX_t

```c
int_leastX_t number;
```

至少有X位，可能更多，适用于需要保证最小储存容量的可移植代码。

```c
// int_fastX_t 特效 8bit 16bit
```

至少有X位，但是选择运算最快的类型（位数），适用于需要性能且性能敏感的场景。

```c
intX_t number;
```

标准整数类型 -> 固定宽度整数类型

位数固定，不可以越界，适用于需要精确数据大小的场景。

## float

### ouput using function printf()

```c
#include <stdio.h>

int main()
{
    float temperature = 36.6;
	// different output forms using function printf()
    // use %f
    printf("Using %%f: %f\n", temperature);
    // use %e of %E 科学计数法
    printf("Using %%e: %e\n", temperature); 
    printf("Using %%E: %E\n", temperature);
    // use %a of %A 十六进制 p计数法
    printf("Using %%a: %a\n", temperature);
    printf("Using %%A: %A\n", temperature);
    
}
```

### IEEE754标准存储单精度浮点数

Frank视频参考：

1. [032.浮点数IEEE754指数偏移存储原理_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1Ae41117Gd/?p=40)

2. [033.(选修)浮点数计算范围的原理_哔哩哔哩_bilibili
3. [[041-1.补录IEEE754隐含位_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1Ae41117Gd/?p=49&vd_source=0c6e9aa27976c7e534f51b25bcdd53f0)](https://www.bilibili.com/video/BV1Ae41117Gd?p=41&spm_id_from=pageDriver&vd_source=0c6e9aa27976c7e534f51b25bcdd53f0)

参考博客：

1. [IEEE-754单精度浮点类型详解（完结篇）_ieee754单精度浮点数-CSDN博客](https://blog.csdn.net/weixin_45500205/article/details/124332064)

2. [IEEE754规范: 四, 非规格数, ±infinity, NaN - 简书 (jianshu.com)](https://www.jianshu.com/p/cb377fd1a295)

![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-dI4ffSrU-1650547207379)(D:/Desktop/重拾java基础/pic/image-20220321155013940.png)]](https://img-blog.csdnimg.cn/e4235b4b19d444e9808d8dd8be463930.png)

想要将一个十进制小数存储到这32位的小格子中也需要一定存储过程，此存储过程非彼存储过程（不是指数据库的存储过程），我们现在以十进制数8.5为例，一步一步将它“存储”到这32个格子中。

![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-vfSTln2A-1650547207379)(D:/Desktop/重拾java基础/pic/image-20220322083427131.png)]](https://img-blog.csdnimg.cn/4ab3ae6c5d6a41cfb7eaebfc3d1ab92f.png)

#### 符号位存储

 这一步比较简单，前面有有提到过，0表示浮点数为正数，1为负数，我们单凭肉眼就能看出，8.5为正数 所以符号位是0

#### 指数位存储

##### 规范化（normalized）

![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-8czb883f-1650547207379)(D:/Desktop/重拾java基础/pic/image-20220321224345217.png)]](https://img-blog.csdnimg.cn/7b2a4190239846feaac2691b36eb29bc.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAV0VJWUkgb25seV9vbmU=,size_20,color_FFFFFF,t_70,g_se,x_16)


要获取这个浮点类型的指数位，我首先需要将它转换为二进制数，整数“除二进余 取倒序”，小数“乘二取整 取顺序”，8.5的二进制为1000.1，转换为二进制后可以正式进行规范化。将已经转换为二进制小数的1000.1的小数点往左边移动，移动至小数点左边第一位为1为止，这个过程中小数点移动的位数就是这个浮点类型的阶码，1000.1移动3位变成1.0001，1.0001是它的尾数，3就是这个浮点类型的阶码，小数点向左移动其实也是将这个数除以2^向左移动的位数，所以1000.1变成1.0001，其实是除以2的3次方的到的结果，这个过程就是规范化（normalized）。

![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-jerFjqpN-1650547207380)(D:/Desktop/重拾java基础/pic/image-20220325162712340.png)]](https://img-blog.csdnimg.cn/b7be735ab63a44f28d535f11018a8763.png)

规范化也会出现小数反向移动的情况，如果浮点类型没有整数，例如十进制数0.5的二进制形式0.1，此时需要向右边反向移动1位，即为1.0，-1就是它的阶码，移动后的尾数第一位始终为1（因为它是向第一位1的位置开始移动），IEEE-754没有必要将它存储，阶码也不会单独再分配一个的符号位，于是就有了偏移量，单精度浮点类型的偏移量为127，双精度浮点类型为1023，之前提到过指数位只能存储[-127,128]，假设存储一个非常小的单精度浮点类型，规范化时小数点已经需要向右移动127位，即它的指数为-127，加上单精度浮点类型的偏移量127后，也不过是0，它依然是一个整数；所以这个偏移量存在的必要，就是为了确保它在有限的指数位取值范围中保持整数。回归主题，存储阶码为3的浮点类型8.5，它的阶码加上偏移量后(3+127)为130，转换为二进制就是1000 0010；

![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-NI4ZJLNB-1650547207380)(D:/Desktop/重拾java基础/pic/image-20220322101014067.png)]](https://img-blog.csdnimg.cn/8bb7af9ced0041a696c1d7cc1d533e38.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAV0VJWUkgb25seV9vbmU=,size_20,color_FFFFFF,t_70,g_se,x_16)

##### 指数补零

![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-lrYPpdA5-1650547207381)(D:/Desktop/重拾java基础/pic/image-20220322101753950.png)]](https://img-blog.csdnimg.cn/33ea1bfdbdea4c1f84e439fd56049d30.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAV0VJWUkgb25seV9vbmU=,size_15,color_FFFFFF,t_70,g_se,x_16)


指数位只能存八位，其实也会存在计算出的二进制数不足八位的情况，例如119，二进制为1110 111，这是不足八位的，但是也要存储到格子中，所以我们需要补零操作，我们需要在二进制前补零，切记整数二进制后面补零会影响数值，而小数二进制前面补零会影响数值，1110 111补零后为 0111 0111。

#### 尾数位存储

##### 隐藏高位

![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-hMcuPpCv-1650547207381)(D:/Desktop/重拾java基础/pic/image-20220322145835433.png)]](https://img-blog.csdnimg.cn/3498e4721c104d3aabe4b5891d2d1933.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAV0VJWUkgb25seV9vbmU=,size_20,color_FFFFFF,t_70,g_se,x_16)


之前有提到过，规范化后的二进制小数就是它的尾数，1.0001就是尾数，所以一个浮点数主要存储在尾数位，规范化会将小数点左边第一位1移动，所以尾数前面第一位始终都是1.，这个1.是可以省略的，所以尾数又变成了0001

##### 低位补零

![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-tXiftXkq-1650547207381)(D:/Desktop/重拾java基础/pic/image-20220322150019074.png)]](https://img-blog.csdnimg.cn/9c8cba2ddf22484c99aef8dd2272a3cc.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAV0VJWUkgb25seV9vbmU=,size_20,color_FFFFFF,t_70,g_se,x_16)


尾数位占用23位，没有达到23位时，需补足23位，尾数位存储的都是小数，所以它只能在后面补零，

补完之后的尾数是 0001 0000 0000 0000 0000 000

##### Result

![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-tvQc8hqH-1650547207382)(D:/Desktop/重拾java基础/pic/image-20220322083427131.png)]](https://img-blog.csdnimg.cn/c8c7a22e5e264a5c95ebd89891dbaa81.png)

最后再拼接一下

符号位：8.5为整数，所以符号位为 0

指数位：1000.1左移3位变成尾数 1.0001 ，3+127=130，130二进制为 1000 0010

尾数位：尾数位1.0001，藏高补低后为 0001 0000 0000 0000 0000 000

结果：十进制数8.5的单精度浮点类型存储格式为 0 1000 0010 0001 0000 0000 0000 0000 000

### 浮点类型的范围

微软文档参考：[float 类型 | Microsoft Learn](https://learn.microsoft.com/zh-cn/cpp/c-language/type-float?view=msvc-170)

| 类型   | 最小值                     | 最大值                     |
| :----- | :------------------------- | :------------------------- |
| float  | 1.175494351 E - 38         | 3.402823466 E + 38         |
| double | 2.2250738585072014 E - 308 | 1.7976931348623158 E + 308 |

**如果存储比精度更重要，请考虑对浮点变量使用 float 类型。 相反，如果精度是最重要的条件，则使用 double 类型。**

### 丢失精度

由于float的存储方式，float一定存在着丢失精度的问题。存储方式详见IEEE754标准存储单精度浮点数。

### OverFlow and UnderFlow

The reasons of overflow and underflow are detailed in IEEE-754.

#### Example

```c
#include <stdio.h>
#include <float.h>

int main()
{
    // the maximum of float
    float max_of_float = FLT_MAX;

    // OverFlow
    float overflow = max_of_float * 1000.0f;

    // the minimum of float
    float min_of_float = FLT_MIN;

    // UnderFlow
    float underflow = min_of_float / 1000.0f;	

	// the example of overflow and underflow
    printf("Maximum float: %e\n", max_of_float);
    printf("Overflow: %e\n", overflow);
    printf("Minimum float: %e\n", min_of_float);
    printf("Underflow: %e\n", underflow);
}
```

### infinity and Nan

无穷大和Not a number

* Frank视频参考

[037.Infinity与Nan_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1Ae41117Gd?p=45&vd_source=0c6e9aa27976c7e534f51b25bcdd53f0)

* 参考博客：

[C语言调试输出变量为-1.#IND00 -1.#INF00 1.#INF00-CSDN博客](https://blog.csdn.net/x_a_little_story/article/details/104036650)

#### Example

```c
#include <stdio.h>
#include <float.h>
#include <math.h>

int main()
{
    // 正无穷大
    float positive_infinity = INFINITY;
    printf("Positive infinity: %f\n", positive_infinity);

    // 负无穷大
    float negative_infinity = -INFINITY;
    printf("Negative infinity: %f\n", negative_infinity);

    // 除以零产生的无穷大
    float num_1 = 1.0f;
    float infinity = num_1 / 0.0f;
    printf("1.0 / 0.0: %f\n", infinity);

    //Nan   Not a number    0.0 / 0.0
    // In other word    IND Implementation not define
    float num_0 = 0.0f;
    float nan = num_0 / 0.0f;
    printf("0.0 / 0.0: %f\n", nan);

    float negative_sqrt = sqrt(-1.0f);
    printf("sqrt(-1.0f): %f\n", negative_sqrt);
}
```

### 最近偶数舍入——IEEE-754默认舍入规则

Round to nearest, ties to even.

又名银行家舍入

向距离最近的数舍入，如果有两个最近的数，则选择其中的偶数。

* 参考博客：

1. [IEEE 754 的四种舍入方式_LaymanXia不是layman的技术博客_51CTO博客](https://blog.51cto.com/u_8741388/1625404)

#### Example

```c
#include <stdio.h>

int main()
{
    // 默认舍入规则
    // IEEE-754
    // 最近偶数舍入 round to nearest, ties to even
    // 银行家舍入
    
    float number = 3.15;
    
    printf("1-> %.1f\n", number);
	number = 3.25;
    printf("2-> %.1f\n", number);
    
    // 如果尾数的整数部分是奇数，向上舍入，使他变成偶数
    // 如果尾数的整数部分是偶数，向下舍入，因为他已经是偶数
}
```

### double

C语言中有一个小心机，在任意位置使用小数时，若没有定义为float类型，默认为double类型

```
3.14	// double类型
3.14f	// float类型
```

#### 默认参数提升

在使用函数printf()对都变了类型进行输出时。提示符可以使用%f或%lf。其原因是函数printf()在输出float类型时会进行默认参数提升，将float提升到double进行输出。此时提示符为%f或%lf仅改变小数的输出风格（位数）。

```c
#include <stdio.h>

int main()
{
    // double 速度慢，精度高
    // float 速度快，精度低
    // 企业中需要根据不同场合来选择使用float还是double


    /************For example***********/
    /************3D  渲染**************/
    // 3D渲染速度比精度更重要，常用float

    // 科学计算，精度比速度更重要，double是不二之选，甚至可能会使用long double
    double num1 = 123.456;
    double num2 = 76.543;

    double sum = num1 + num2;
    double difference = num1 - num2;
    double product = num1 * num2;
    double quotient = num1 / num2;

    printf("Sum: %f\n", sum);
    printf("Difference: %f\n", difference);
    printf("Product: %f\n", product);
    printf("Quotient: %f\n", quotient);
}
```

### long double

* 参考博客

[【高精浮点】关于long double的使用方法-CSDN博客](https://blog.csdn.net/weixin_51948235/article/details/121196451)

### float和double有效精度对比及计算

根据IEEE-754标准，float有23位位数，double有52位尾数。二者都存在一个隐藏位的1，所以2者的最小精度分别为$2^{-24}$和$2^{-53}$。有效数字分别为$\log_{1/10}2^{-24}$和$\log_{1/10}2^{-53}$，约为7.22和15.95。所以C语言中为了保证安全，定义float和double的有效数字分别为6位和15位。

```c
#include <stdio.h>
#include <float.h>

int main()
{
    float float_num = 1.0f / 3.0f;
    double double_num = 1.0 / 3.0;

    printf("Float precision: %.20f\n", float_num);
    printf("Double precision: %.20lf\n", double_num);

    printf("Defined max precision of float: %d\n", FLT_DIG);
    printf("Defined max precision of double: %d\n", DBL_DIG);
}
```

### decimal（定点数）——C语言中没有

用于保存金融系统里面的余额和钱。

C语言常用于开发操作系统和开发底层程序。

但是在一些大型金融或政要的项目，绝对不能使用double。

例如在MySQL中有关钱的数据一定要使用decimal。

## char

char用于存储字符，但是从技术层面看，char其实是整数类型。C语言采用Ascii编码将整数和字符一一对应起来，完成对字符的编码。

#### ASCII码表

| **ASCII值** | **控制字符** | **ASCII值** | **控制字符** | **ASCII值** | **控制字符** | **ASCII值** | **控制字符** |
| ----------- | ------------ | ----------- | ------------ | ----------- | ------------ | ----------- | ------------ |
| 0           | NUL          | 32          | (space)      | 64          | @            | 96          | 、           |
| 1           | SOH          | 33          | ！           | 65          | A            | 97          | a            |
| 2           | STX          | 34          | ”            | 66          | B            | 98          | b            |
| 3           | ETX          | 35          | #            | 67          | C            | 99          | c            |
| 4           | EOT          | 36          | $            | 68          | D            | 100         | d            |
| 5           | ENQ          | 37          | %            | 69          | E            | 101         | e            |
| 6           | ACK          | 38          | &            | 70          | F            | 102         | f            |
| 7           | BEL          | 39          | '            | 71          | G            | 103         | g            |
| 8           | BS           | 40          | (            | 72          | H            | 104         | h            |
| 9           | HT           | 41          | )            | 73          | I            | 105         | i            |
| 10          | LF           | 42          | *            | 74          | J            | 106         | j            |
| 11          | VT           | 43          | +            | 75          | K            | 107         | k            |
| 12          | FF           | 44          | ,            | 76          | L            | 108         | l            |
| 13          | CR           | 45          | -            | 77          | M            | 109         | m            |
| 14          | SO           | 46          | .            | 78          | N            | 110         | n            |
| 15          | SI           | 47          | /            | 79          | O            | 111         | o            |
| 16          | DLE          | 48          | 0            | 80          | P            | 112         | p            |
| 17          | DCI          | 49          | 1            | 81          | Q            | 113         | q            |
| 18          | DC2          | 50          | 2            | 82          | R            | 114         | r            |
| 19          | DC3          | 51          | 3            | 83          | X            | 115         | s            |
| 20          | DC4          | 52          | 4            | 84          | T            | 116         | t            |
| 21          | NAK          | 53          | 5            | 85          | U            | 117         | u            |
| 22          | SYN          | 54          | 6            | 86          | V            | 118         | v            |
| 23          | TB           | 55          | 7            | 87          | W            | 119         | w            |
| 24          | CAN          | 56          | 8            | 88          | X            | 120         | x            |
| 25          | EM           | 57          | 9            | 89          | Y            | 121         | y            |
| 26          | SUB          | 58          | :            | 90          | Z            | 122         | z            |
| 27          | ESC          | 59          | ;            | 91          | [            | 123         | {            |
| 28          | FS           | 60          | <            | 92          | \            | 124         | \|           |
| 29          | GS           | 61          | =            | 93          | ]            | 125         | }            |
| 30          | RS           | 62          | >            | 94          | ^            | 126         | ~            |
| 31          | US           | 63          | ?            | 95          | —            | 127         | DEL          |

##### ASCII诠释部分

**1.ASCII中的0~31为控制字符；32~126为打印字符；127为Delete(删除)命令。下表为控制字符释义。**

| **十进制** | **十六进制** | **字符**   | **十进制** | **十六进制** | **字符**     |
| ---------- | ------------ | ---------- | ---------- | ------------ | ------------ |
| 0          | 00           | 空         | 16         | 10           | 数据链路转意 |
| 1          | 01           | 头标开始   | 17         | 11           | 设备控制 1   |
| 2          | 02           | 正文开始   | 18         | 12           | 设备控制 2   |
| 3          | 03           | 正文结束   | 19         | 13           | 设备控制 3   |
| 4          | 04           | 传输结束   | 20         | 14           | 设备控制 4   |
| 5          | 05           | 查询       | 21         | 15           | 反确认       |
| 6          | 06           | 确认       | 22         | 16           | 同步空闲     |
| 7          | 07           | 震铃       | 23         | 17           | 传输块结束   |
| 8          | 08           | backspace  | 24         | 18           | 取消         |
| 9          | 09           | 水平制表符 | 25         | 19           | 媒体结束     |
| 10         | 0A           | 换行/新行  | 26         | 1A           | 替换         |
| 11         | 0B           | 竖直制表符 | 27         | 1B           | 转意         |
| 12         | 0C           | 换页/新页  | 28         | 1C           | 文件分隔符   |
| 13         | 0D           | 回车       | 29         | 1D           | 组分隔符     |
| 14         | 0E           | 移出       | 30         | 1E           | 记录分隔符   |
| 15         | 0F           | 移入       | 31         | 1F           | 单元分隔符   |

**2.ASCII扩展字符——（为了适应更多字符）128~255，或者-128~-1,其中，-128对应128，依次递增对应。**

| **十进制** | **十六进制** | **字符** | **十进制** | **十六进制** | **字符** |
| ---------- | ------------ | -------- | ---------- | ------------ | -------- |
| 128        | 80           | Ç        | 192        | C0           | └        |
| 129        | 81           | ü        | 193        | C1           | ┴        |
| 130        | 82           | é        | 194        | C2           | ┬        |
| 131        | 83           | â        | 195        | C3           | ├        |
| 132        | 84           | ä        | 196        | C4           | ─        |
| 133        | 85           | à        | 197        | C5           | ┼        |
| 134        | 86           | å        | 198        | C6           | ╞        |
| 135        | 87           | ç        | 199        | C7           | ╟        |
| 136        | 88           | ê        | 200        | C8           | ╚        |
| 137        | 89           | ë        | 201        | C9           | ╔        |
| 138        | 8A           | è        | 202        | CA           | ╩        |
| 139        | 8B           | ï        | 203        | CB           | ╦        |
| 140        | 8C           | î        | 204        | CC           | ╠        |
| 141        | 8D           | ì        | 205        | CD           | ═        |
| 142        | 8E           | Ä        | 206        | CE           | ╬        |
| 143        | 8F           | Å        | 207        | CF           | ╧        |
| 144        | 90           | É        | 208        | D0           | ╨        |
| 145        | 91           | æ        | 209        | D1           | ╤        |
| 146        | 92           | Æ        | 210        | D2           | ╥        |
| 147        | 93           | ô        | 211        | D3           | ╙        |
| 148        | 94           | ö        | 212        | D4           | Ô        |
| 149        | 95           | ò        | 213        | D5           | ╒        |
| 150        | 96           | û        | 214        | D6           | ╓        |
| 151        | 97           | ù        | 215        | D7           | ╫        |
| 152        | 98           | ÿ        | 216        | D8           | ╪        |
| 153        | 99           | Ö        | 217        | D9           | ┘        |
| 154        | 9A           | Ü        | 218        | DA           | ┌        |
| 155        | 9B           | ¢        | 219        | DB           | █        |
| 156        | 9C           | £        | 220        | DC           | ▄        |
| 157        | 9D           | ¥        | 221        | DD           | ▌        |
| 158        | 9E           | ?        | 222        | DE           | ?        |
| 159        | 9F           | ƒ        | 223        | DF           | ?        |
| 160        | A0           | á        | 224        | E0           | α        |
| 161        | A1           | í        | 225        | E1           | ß        |
| 162        | A2           | ó        | 226        | E2           | Γ        |
| 163        | A3           | ú        | 227        | E3           | π        |
| 164        | A4           | ñ        | 228        | E4           | Σ        |
| 165        | A5           | Ñ        | 229        | E5           | σ        |
| 166        | A6           | ª        | 230        | E6           | µ        |
| 167        | A7           | º        | 231        | E7           | τ        |
| 168        | A8           | ¿        | 232        | E8           | Φ        |
| 169        | A9           | ?        | 233        | E9           | Θ        |
| 170        | AA           | ¬        | 234        | EA           | Ω        |
| 171        | AB           | ½        | 235        | EB           | δ        |
| 172        | AC           | ¼        | 236        | EC           | ∞        |
| 173        | AD           | ¡        | 237        | ED           | φ        |
| 174        | AE           | «        | 238        | EE           | ε        |
| 175        | AF           | »        | 239        | EF           | ∩        |
| 176        | B0           | ?        | 240        | F0           | ≡        |
| 177        | B1           | ?        | 241        | F1           | ±        |
| 178        | B2           | ▓        | 242        | F2           | ≥        |
| 179        | B3           | │        | 243        | F3           | ≤        |
| 180        | B4           | ┤        | 244        | F4           | ?        |
| 181        | B5           | ╡        | 245        | F5           | ?        |
| 182        | B6           | ╢        | 246        | F6           | ÷        |
| 183        | B7           | ╖        | 247        | F7           | ≈        |
| 184        | B8           | ╕        | 248        | F8           | ≈        |
| 185        | B9           | ╣        | 249        | F9           | ?        |
| 186        | BA           | ║        | 250        | FA           | ·        |
| 187        | BB           | ╗        | 251        | FB           | √        |
| 188        | BC           | ╝        | 252        | FC           | ?        |
| 189        | BD           | ╜        | 253        | FD           | ²        |
| 190        | BE           | ╛        | FE         | ■            |          |
| 191        | BF           | ┐        | 255        | FF           | ÿ        |

#### 其他的编码标准

##### Unicode

* Frank参考视频

[042.char与ASCII_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1Ae41117Gd?p=51&spm_id_from=pageDriver&vd_source=0c6e9aa27976c7e534f51b25bcdd53f0)

* 参考博客：

[计算机基础知识之Unicode-彻底弄懂 Unicode 编码-CSDN博客](https://blog.csdn.net/qq_25482087/article/details/117048596)

Unicode包含世界上所有的字符，并且兼容Ascii（前128个字符与Ascii相同）。

### Escape sequence（转义序列）

Micorsoft C Reference: [Escape Sequences | Microsoft Learn](https://learn.microsoft.com/en-us/cpp/c-language/escape-sequences?view=msvc-170)

### Range of char Values

**ANSI 3.2.1.1** Whether a "plain" **`char`** has the same range of values as a **`signed char`** or an **`unsigned char`**

All signed character values range from -128 to 127. All unsigned character values range from 0 to 255.

`unsigned char`和`uint8_t`在存储逻辑上都是用8位的空间存储整数。但是`unsigned char`常用于处理字符等数据，`uint8_t`常用于数值计算。例如log日志就可以用`unsigned char`类型去写，但是使用`uint8_t`就不行。 

## bool

```c
#include <stdio.h>
#include <stdbool.h>

int main()
{
    // 布尔类型，1位，用于表示事无的真假，依赖于整数的0和1
    
    // 判读游戏胜利的布尔变量
    bool is_game_won = true;
    // 判断游戏失败的布尔变量
    bool is_game_lose = false;
}
```

### 复数和虚数

详见`<complex.h>`和`<imaginary.h>`两个头文件。

## 数据类型转换

能使用显式类型转换绝不使用隐式类型转换。

```c
uint32_t mediumNumber = 223;
/********隐式类型转换************/
uint16_t smallNumber = mediumNumber;
/**********显式类型转换**********/
uint16_t smallNumber_1 = (uint16_t)mediumNumber;
```

类型转换是否出错取决于是否超范围。

显式类型转换最显著的优点：极大增强了代码的可读性。

# 常量

例如植物大战僵尸中，向日葵的价格是恒定不变的，这时就应该使用常量进行存储。

* 参考博客：

[const常量与define宏定义的区别_count常量和define宏定义区别-CSDN博客](https://blog.csdn.net/love_gaohz/article/details/7567856)

## const 常量

```c
#include <stdio.h>

int main()
{
    const double PI = 3.14;
    
    printf("PI: %lf\n", PI);
}
```

## #define 宏定义常量

```c
#include <stdio.h>
#define PI 3.14
int main()
{
    printf("PI: %lf\n", 3.14);
}
```

# 运算符(C operators)

指挥左值与右值的一些指令。

```c
#include <stdio.h>
#include <stdint.h>
#include <inttypes.h>

int main()
{
    // 数据对象  data object
    // 左值  Lvalue
    // 右值  Rvalue
    // 运算符  operater
    uint8_t apple_box = 5;
    uint8_t banana_box = 10;

    printf("There are %" PRId8 " apples in apple box.\n", apple_box);
    printf("There are %" PRId8 " bananas in apple box.\n", banana_box);

    uint16_t total_fruit = apple_box + banana_box;
    printf("There are %" PRId16 " fruits in fruit box.\n", total_fruit);
}
```

Microsoft C reference: [C operators | Microsoft Learn](https://learn.microsoft.com/en-us/cpp/c-language/c-operators?view=msvc-170)

The C operators are a subset of the [C++ built-in operators](https://learn.microsoft.com/en-us/cpp/cpp/cpp-built-in-operators-precedence-and-associativity?view=msvc-170).

There are three types of operators. A unary expression consists of either a unary operator followed by an operand, or the **`sizeof`** or **`_Alignof`** keyword followed by an expression. The expression can be either the name of a variable or a cast expression. If the expression is a cast expression, it must be enclosed in parentheses. A binary expression consists of two operands joined by a binary operator. A ternary expression consists of three operands joined by the conditional-expression operator.

C includes the following unary operators:

| Symbol                  | Name                                    |
| :---------------------- | :-------------------------------------- |
| **`-`** **`~`** **`!`** | Negation and complement operators       |
| **`\*`** **`&`**        | Indirection and address-of operators    |
| **`_Alignof`**          | Alignment operator (since C11)          |
| **`sizeof`**            | Size operator                           |
| **`+`**                 | Unary plus operator                     |
| **`++`** **`--`**       | Unary increment and decrement operators |

Binary operators associate from left to right. C provides the following binary operators:

| Symbol                                              | Name                           |
| :-------------------------------------------------- | :----------------------------- |
| **`\*`** **`/`** **`%`**                            | Multiplicative operators       |
| **`+`** **`-`**                                     | Additive operators             |
| **`<<`** **`>>`**                                   | Shift operators                |
| **`<`** **`>`** **`<=`** **`>=`** **`==`** **`!=`** | Relational operators           |
| **`&`** **`|`** **`^`**                             | Bitwise operators              |
| **`&&`** **`||`**                                   | Logical operators              |
| **`,`**                                             | Sequential-evaluation operator |

The base operator (**`:>`**), supported by previous versions of the Microsoft 16-bit C compiler, is described in [C Language syntax summary](https://learn.microsoft.com/en-us/cpp/c-language/c-language-syntax-summary?view=msvc-170).

The conditional-expression operator has lower precedence than binary expressions and differs from them in being right associative.

Expressions with operators also include assignment expressions, which use unary or binary assignment operators. The unary assignment operators are the increment (**`++`**) and decrement (**`--`**) operators; the binary assignment operators are the simple-assignment operator (**`=`**) and the compound-assignment operators. Each compound-assignment operator is a combination of another binary operator with the simple-assignment operator.

## 算术运算符

加减乘除

## 关系运算符

做判断，而不是用来做计算，判断逻辑上的真假。

大于、小于

`==`

### 条件表达式运算符(Conditional-Expression Operators)

```c
#include <stdio.h>

int main()
{
    int score = 90;
    printf("The grade of your score: %s\n", score > 60 ? "True" : "False");
}
```



## 逻辑运算符

与或非



## Bitwise operators(位运算符)

### 按位与(&)

读取标志位，标志位置零

设置特定位，组合标志位

### 按位或(|)

标志位置一

### 按位异或(^)

反转特定位，交换无符号整型变量，检测不同

XOR交换算法参考：

1. [XOR swap algorithm - Wikipedia](https://en.wikipedia.org/wiki/XOR_swap_algorithm)
2. [XOR交换算法_全球百科 (vibaike.com)](https://vibaike.com/163641/#:~:text=在计算机编程中，独占或交换（有时简称为XOR交换）是一种使用独占或位操作来交换两个变量的值的算法，而不使用通常需要的临时变量。,该算法主要是一种新奇的做法，也是展示独占或运算特性的一种方式。 它有时被当作程序优化来讨论，但几乎没有任何情况下，通过排他性操作的交换会比标准的、明显的技术带来好处。)

检测不同：

### 按位取反(~)



### Example

```c
#include <stdio.h>
#include <stdint.h>
#include <inttypes.h>
#include <stdbool.h>

// 此处宏定义用于printf数的二进制形式，参考stackoverflow
// 此处宏定义中同样采用Bitwise operators处理二进制数每一位的读取
// 将读取到的二进制结果逐个输出，从而实现printf二进制数
/*********Hacky but works for me:**********/
#define BYTE_TO_BINARY_PATTERN "%c%c%c%c%c%c%c%c"
#define BYTE_TO_BINARY(byte)  \
  ((byte) & 0x80 ? '1' : '0'), \
  ((byte) & 0x40 ? '1' : '0'), \
  ((byte) & 0x20 ? '1' : '0'), \
  ((byte) & 0x10 ? '1' : '0'), \
  ((byte) & 0x08 ? '1' : '0'), \
  ((byte) & 0x04 ? '1' : '0'), \
  ((byte) & 0x02 ? '1' : '0'), \
  ((byte) & 0x01 ? '1' : '0') 
/*********You need all extra quotes, unfortuately**********/
/*********This approach has the efficiency risks of macors**********/
/*********(don't pass a function as the artument to BYTE_TO_BINARY)**********/
/*********but avoids the memory issues and multiple invocations of strcat in some of other proposals here**********/

int main()
{
    /*********按位与、按位或、按位非等Bitwise operators运用实例********/
    /*********Bitwise operators常用在底层嵌入式开发中**************/
    /*********用于操作寄存器中某些位（置零或置一）**************/
    /*********或用于读取寄存器中某些位**************/


    // 变量类型和名称定义不规范， 仅用作测试
    const uint8_t INITIAL_VALUE = 0b00101110;
    uint8_t byte = INITIAL_VALUE;

    // 输出byte的值
    printf("The value of byte: "BYTE_TO_BINARY_PATTERN"\n", BYTE_TO_BINARY(byte));

    // 读取byte值的第二位
    // 计算结果为4(0b00000100)
    // 取bool类型从而保证取当前位(bit)的值
    bool second_digit_of_byte = byte & (1 << 2);

    // 输出byte值的第二位
    printf("The second digit of byte: %" PRIu8 "\n", second_digit_of_byte);

    // 读取byte值的第四位
    // 计算结果为16(0b00000100)
    // 取bool类型从而保证取当前位(bit)的值
    bool forth_digit_of_byte = byte & (1 << 4);

    // 输出byte值的第四位
    printf("The forth digit of byte: %" PRIu8 "\n", forth_digit_of_byte);

    // 读取byte值的第五位
    // 计算结果为32(0b00100000)
    // 取bool类型从而保证取当前位(bit)的值
    bool fifth_digit_of_byte = byte & (1 << 5);

    // 输出byte值的第五位
    printf("The fifth digit of byte: %" PRIu8 "\n", fifth_digit_of_byte);

    // 将byte的第三位置零（原本为一）
    byte &= ~(1 << 3);

    // 输出byte的值
    printf("Ater setting the third digit to zero, the value of byte: "BYTE_TO_BINARY_PATTERN"\n", BYTE_TO_BINARY(byte));

    // 将byte的第七位置一（原本为零）
    byte |= (1 << 7);

    // 输出byte的值
    printf("After setting the seventh digit to one, the value of byte: "BYTE_TO_BINARY_PATTERN"\n", BYTE_TO_BINARY(byte));

    // 将byte的第零位和第一位翻转
    byte ^= (0b00000011);

    // 输出byte的值
    printf("After flipping the first and second digit, the value of byte: "BYTE_TO_BINARY_PATTERN"\n", BYTE_TO_BINARY(byte));

    // 检测现在的byte与初始值哪几位不一致
    byte ^= INITIAL_VALUE;

    // 输出检测结果(每位为0的表示与初始值相同，为1的表示与初始值不同)
    printf("The result of checking: "BYTE_TO_BINARY_PATTERN"\n", BYTE_TO_BINARY(byte));
}
```

## 赋值运算符

将右值（数值）赋值给（放进）左值（盒子）。

### 多重赋值(Multiple assignments)

```c
#include <stdio.h>
#include <stdint.h>
#include <inttypes.h>

int main()
{
    // 请注意，这里的x,y,z仅仅是测试程序，并无实际意义
    uint8_t x,y,z;

    // 多重赋值
    /****相当于****/
    // z = 10;
    // y = z;
    // x = y;
    x = y = z = 10;

    printf("x: %" PRId8 "\n", x);
    printf("y: %" PRId8 "\n", y);
    printf("z: %" PRId8 "\n", z);
}
```

C语言理论上允许多重赋值，但是实际应用中不使用三重赋值以上的情况。多重赋值又叫做长链式。第一，长链式可读性差。第二，长链式更容易出现拼写错误。在实际开发中，不建议使用多重赋值，也不建议使用多重声明。对于有实际意义的变量，往往使用一行声明一个变量并在上一行进行注释的方式。

## 其他运算符

### sizeof

微软文档参考：[sizeof 运算符 (C) | Microsoft Learn](https://learn.microsoft.com/zh-cn/cpp/c-language/sizeof-operator-c?view=msvc-170)

### 前缀后缀递增递减

在企业当中尽量避免使用这种形式。除了在使用循环变量和定义数组时可能会用到。因为这种递增或者递减的方式是可读性很差的。在考虑效率的情况下，现代编译器中，前缀递增递减比后缀递增递减更有效率。是否选择前缀和后缀的形式，要基于变量的旧值。

```c
result = ++value;
// value = value + 1;
// result = value;

result = value++;
// result = value
// value = value + 1;
```

### 按位移位运算符

微软文档参考：[按位移位运算符 | Microsoft Learn](https://learn.microsoft.com/zh-cn/cpp/c-language/bitwise-shift-operators?view=msvc-170)

```c
#include <stdio.h>
#include <stdint.h>
#include <inttypes.h>

int main()
{
    uint8_t num = 22;
    // 00010110
    // num << 2
    printf("Original number: %" PRIu8 " (binary: 00010110)\n", num);

    // 左移
    // 左移两位相当于 * 2^2
    uint8_t left_shifted = num << 2;
    printf("Left shifted by 2: %" PRIu8 " (binary: 01011000)\n", left_shifted);

    // 右移
    // 右移两位相当于 / 2^2
    uint8_t right_shifted = num >> 2;
    printf("Right shifted by 2: %" PRIu8 " (binary: 00000101)\n", right_shifted);
}
```

位移操作的效果与乘除法类似，但从ALU(Arithmetic&Logic Unit)算数逻辑单元计算的角度来说，进行乘法运算需要经过硬件数字电路中的乘法器进行计算。而位移操作只需要进行移位即可，操作更简单，运算速度更快。

位移操作对于有符号整型和无符号整型的操作是不同的。对于有符号整型，需要特别关注编译器是如何处理右移运算的（对于符号位如何右移）。位移操作可能会导致数据溢出，特别是左移。使用位移操作时一定要写清注释，来表明为什么这样写，这样可以提高代码的可读性。

**在企业当中，位操作符常用于底层代码，主要用于处理设备的配置选项。例如：硬件控制，图形处理，系统权限的设置等。在上述场景下，位操作符使用频繁，并且高效。**

参考博客：[C语言中的位运算：位操作符、位掩码与位字段在实际编程中的应用（一）_使用位运算处理替换位字段-CSDN博客](https://blog.csdn.net/weixin_56154577/article/details/137274524#:~:text=按位逻辑运算符： 1 运算规则 ：对两个操作数的对应二进制位进行逻辑或运算，只要有一个位为1，结果位即为1，只有当两个位都为0时，结果位才为0。 2 示例 ：同样假设 A,：用于设置特定标志位。 例如，要在一个包含多个状态标志的整数变量中置位某个标志，可通过 flags |%3D MASK ，其中 MASK 是对应位为1的掩码。)







# 表达式(expression)和语句(statement)



# 输入需要有输入验证

输入检查和用户提示

# 命名规范

命名规范常用下划线命名法和大（小）驼峰命名法。在一个项目中只使用一种命名方法来达到代码规范的统一。