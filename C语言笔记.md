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
    // 布尔类型，1位，用于表示事件的真假，依赖于整数的0和1
    // 如果误操作使用整型来判断真假
    // 则0代表false
    // 非0代表true
    // 判读游戏胜利的布尔变量
    bool is_game_won = true;
    // 判断游戏失败的布尔变量
    bool is_game_lose = false;
}
```

## 复数和虚数

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

实际写代码的过程中，类型转换的内容非常多，如果在写代码的过程中出现问题，可参考微软文档。

Microsoft C Reference: [赋值转换 | Microsoft Learn](https://learn.microsoft.com/zh-cn/cpp/c-language/assignment-conversions?view=msvc-170)

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

## 计算的优先级和顺序

Microsoft C Reference: [计算的优先级和顺序 | Microsoft Learn](https://learn.microsoft.com/zh-cn/cpp/c-language/precedence-and-order-of-evaluation?view=msvc-170)



# 表达式(expression)和语句(statement)

Question: **What is the difference between expression and statement in functional programming?**

Answer: 

These concepts aren’t specific to functional programming. They apply to imperative programming as well. **A statement is a piece of code that does something. An expression is a piece of code that has a value (and a type in statically-typed languages).** The reason you might hear more about them in functional programming is that in functional languages, pretty much everything that isn’t a declaration is an expression.

Statements in general are either declarations or things that are executed for their side effects. For example (using a C-family-ish syntax):

```
int theAnswer = 42; 
println("Printing is a side effect."); 
```

The first one is a declaration. The second one is a statement that is executed for the side-effect that it creates. Here’s an example of using `if` as a statement.

```
if (someBooleanValue) { 
  theAnswer++; 
} else { 
  theAnswer--; 
} 
```

This `if` statement doesn’t give back a value. We execute it in order to mutate a variable, which is a side effect. In many languages descended from C there is a special operator, the ternary operator, `?:`, that is used to create `if` expressions. Compare this to a more functional language, like Scala, where `if` is an expression. That means you can type something like the following.

```
val theAnswer = if (someBooleanValue) 43 else 41 
```

Note that anything that makes sense to put on the right side of an assignment/declaration needs to be an expression because you are using the value of it.

You actually use expressions all the time in every programming language. For example, consider the following:

```
(5 + x) * y 
```

This is an expression. You’d normally put it someplace in your code that needs that value. The thing I want to point out is that it is a compound expression built from smaller expressions. Literals, like `5`, and variables, like `x` and `y`, are simple expressions. Any sequence of tokens that has a value in the language is an expression.

In functional languages, control structures are also generally expressions. In imperative languages they generally aren’t, they are just statements that execute and do something, but don’t give back a value.

Reference from: https://www.quora.com/What-is-the-difference-between-expression-and-statement-in-functional-programming

Answered by: Mark lewis

Tips: Please note the difference between imperative programming and functional programming.

# 分支与跳转

若有完美，定是谎言。不要想使用程序去满足所有的可能。分支不可能满足全面满足所有可能。

## Example of if-else

**Tips: 在进行逻辑判断时，尽量进行逻辑简化后再写代码。**

### Using logical operator replaces if-else（利用逻辑运算符的短路行为）

```c
#include <stdio.h>
#include <stdint.h>
#include <inttypes.h>
#include <stdbool.h>

int main()
{
    // 天气晴朗和场地可用的情况下，可以举办高尔夫球活动

    // 天气是否晴朗的布尔值
    bool is_weather_sunny;

    // 场地是否可用的布尔值
    bool is_venue_available;

    // 假设天气不晴朗
    is_weather_sunny = false;

    // 假设场地不可用
    is_venue_available = false;

    // // 1. 使用if-else嵌套
    // // 逻辑容易混乱
    // // 后期维护难度大
    // // 若增加判断条件则需要增加if-else嵌套层数
    // if (is_weather_sunny)
    // {
    //     printf("The weather is sunny.\n");
    //     if (is_venue_available)
    //     {
    //         printf("The venue is available.\n");
    //     }
    //     else
    //     {
    //         printf("The venue is unavailable.\n");
    //     }
    // }
    // else
    // {
    //     printf("The weather is not sunny.\n");
    // }

    // 2. 扩展
    // Using logical operators replaces if-else
    // 使用逻辑AND && 来处理if-else的短路行为
    // 类似的
    // 也可以使用逻辑OR || 来处理if-else的短路行为
    if (is_weather_sunny && is_venue_available)
    {
        printf("The game will be played on time.\n");
    }
    else
    {
        printf("The game will be delayed.\n");

        if (!is_weather_sunny)
        {
            printf("Reason: the weather is not sunny.\n");
        }

        if (!is_venue_available)
        {
            printf("Reason: the venue is not available.\n");
        }
    }
}
```

### simulate a game logic

```c
#include <stdio.h>
#include <stdint.h>
#include <inttypes.h>
#include <stdbool.h>

int main()
{
    /*
        玩家可以选择进入不同的房间，每一个房间都有不同的进入条件。

        房间A: 玩家需要有VIP身份
        房间B: 玩家需要至少有10个金币，或者是一个特殊道具
        房间C: 玩家需要有VIP身份，并且金币数量不得少于20
        房间D: 玩家需要有VIP或者特殊道具，并且数量不少于5
    */
    // 玩家属性（在真实程序中可能来自于用户输入或者是游戏逻辑）
    bool is_vip = true;
    bool has_special_item = true;
    uint32_t coins_num = 15;

    // 检查房间A的条件
    // 房间A: 玩家需要有VIP身份
    if (is_vip)
    {
        printf("You have access to Room A.\n");
    }
    else
    {
        printf("You don't have access to Room A.\n");
    }

    // 检查房间B的条件
    // 房间B: 玩家需要至少有10个金币，或者是一个特殊道具
    if (coins_num >= 10 || has_special_item)
    {
        printf("You have access to Room B.\n");
    }
    else
    {
        puts("You don't have access to Room B.\n");
    }

    // 检查房间C的条件
    // 房间C: 玩家需要有VIP身份，并且金币数量不得少于20
    if (is_vip && coins_num >= 20)
    {
        printf("You have access to Room C.\n");
    }
    else
    {
        printf("You don't have access to Room C.\n");
    }

    // 检查房间D的条件
    // 房间D: 玩家需要有VIP或者特殊道具，并且数量不少于5
    if ((is_vip || has_special_item) && coins_num >= 5)
    {
        printf("You have access to Room D.\n");
    }
    else
    {
        printf("You don't have access to Room D.\n");
    }
}
```

### access right

```c
#include <stdio.h>
#include <stdint.h>
#include <stdbool.h>

// 为了区分不同的职位，可以定义一个枚举类型
typedef enum {
    Manager,    // 0
    Employee,   // 1
    Intern      // 2
} Role;

// Equivalent to
// #define Manager 0
// #define Employee 1
// #define Intern 2

int main()
{
    /*
        公司内部权限问题。
        员工可以访问不同的系统资源，这取决于他们的职位和完成数量。权限规则如下：

        1. Manaager 总是可以访问所有资源
        2. Employee 如果完成5个以上的任务以后，则可以访问资源
        3. Intern (实习生) 如果完成10个以上的任务以后，必须经过经理同意才可以访问
    */
    // 身份属性
    Role role = Intern;

    uint8_t completed_tasks = 7;
    
    bool is_manager_approved = false;

    // Plan A
    // if-else
    // 既使用了else if
    // 又嵌套了if
    // 这样不好
    if (role == Manager)
    {
        puts("You have access right. You are manager.");
    }
    else if (role == Employee && completed_tasks > 5)
    {
        puts("You have access right. You are Employee. You have completed 5 tasks.");
    }
    else if (role == Intern && completed_tasks > 10 &&is_manager_approved)
    {
        puts("You have access right. You are Intern. You have completed 10 tasks. You have been allowd to get the access right by manager.");
    }
    else
    {
        puts("You don't have access right.");
    }

    // Plan B
    // Detect whether the access conditions are met
    // 逻辑复杂，降低了代码的可读性
    // 只适用于身份比较少，且有良好的注释
    bool is_access_allowed = (role == Manager) || (role == Employee && completed_tasks > 5) || (role == Intern && completed_tasks > 10 && is_manager_approved);

    if (is_access_allowed)
    {
        puts("You have access right.");
    }
    else
    {
        puts("You don't have access right.");
    }
}
```

## switch-case

```c
#include <stdio.h>
#include <stdint.h>
#include <stdbool.h>

// 为了区分不同的职位，可以定义一个枚举类型
typedef enum {
    Manager,    // 0
    Employee,   // 1
    Intern      // 2
} Role;

// Equivalent to
// #define Manager 0
// #define Employee 1
// #define Intern 2

bool check_access_for_manager();
bool check_access_for_employee(uint8_t completed_tasks);
bool check_access_for_intern(uint8_t completed_tasks, bool is_manager_approved);

int main()
{
    /*
        公司内部权限问题。
        员工可以访问不同的系统资源，这取决于他们的职位和完成数量。权限规则如下：

        1. Manaager 总是可以访问所有资源
        2. Employee 如果完成5个以上的任务以后，则可以访问资源
        3. Intern (实习生) 如果完成10个以上的任务以后，必须经过经理同意才可以访问
    */
    // 身份属性
    Role role = Intern;

    uint8_t completed_tasks = 7;
    
    bool is_manager_approved = false;

    // Plan A
    // if-else
    // 既使用了else if
    // 又嵌套了if
    // 这样不好
    if (role == Manager)
    {
        puts("You have access right. You are manager.");
    }
    else if (role == Employee && completed_tasks > 5)
    {
        puts("You have access right. You are Employee. You have completed 5 tasks.");
    }
    else if (role == Intern && completed_tasks > 10 &&is_manager_approved)
    {
        puts("You have access right. You are Intern. You have completed 10 tasks. You have been allowd to get the access right by manager.");
    }
    else
    {
        puts("You don't have access right.");
    }

    // Plan B
    // Detect whether the access conditions are met
    // 逻辑复杂，降低了代码的可读性
    // 只适用于身份比较少，且有良好的注释
    bool is_access_allowed = (role == Manager) || (role == Employee && completed_tasks > 5) || (role == Intern && completed_tasks > 10 && is_manager_approved);

    if (is_access_allowed)
    {
        puts("You have access right.");
    }
    else
    {
        puts("You don't have access right.");
    }

    // 重置上一个Plan改变的 is_access_allowed 的默认值为 false
    is_access_allowed = false;

    // Plan C
    // switch-case
    switch (role)
    {
        case Manager:
            is_access_allowed = true;
            break;
        
        case Employee:
            if (completed_tasks > 5)
            {
                is_access_allowed = true;
            }
            break;
        case Intern:
            if (completed_tasks > 10 && is_manager_approved)
            {
                is_access_allowed = true;
            }
            break;
        default:
            is_access_allowed = false;
            break; 
    }
    if (is_access_allowed)
    {
        puts("You have access right.");
    }
    else
    {
        puts("You don't have access right.");
    }

    // 重置上一个Plan改变的 is_access_allowed 的默认值为 false
    is_access_allowed = false;

    // Plan D
    // Using function based on Plan C
    switch (role)
    {
        case Manager:
            is_access_allowed = check_access_for_manager();
            break;
        
        case Employee:
                is_access_allowed = check_access_for_employee(completed_tasks);
            break;
        case Intern:
                is_access_allowed = check_access_for_intern(completed_tasks, is_manager_approved);
            break;
        default:
            is_access_allowed = false;
            break; 
    }
    if (is_access_allowed)
    {
        puts("You have access right.");
    }
    else
    {
        puts("You don't have access right.");
    }
}

bool check_access_for_manager()
{
    return true;
}
bool check_access_for_employee(uint8_t completed_tasks)
{
    return completed_tasks > 5;
}
bool check_access_for_intern(uint8_t completed_tasks, bool is_manager_approved)
{
    return completed_tasks > 10 && is_manager_approved;
}
```

### Complete a state machine using switch-case

```c
#include <stdio.h>
#include <stdint.h>

// 枚举
typedef enum
{
    red_light,      // 0
    green_light,    // 1
    yellow_light    // 2
}Traffic_Light;

void traffic_light_control(Traffic_Light traffic_light_state);

int main()
{
    // 状态机
    // 管理复杂状态的转换， 使用switch case

    // 默认状态为红灯
    Traffic_Light traffic_light_state = red_light;

    traffic_light_control(traffic_light_state);
}

void traffic_light_control(Traffic_Light traffic_light_state)
{
    switch (traffic_light_state)
    {
        case red_light:
            puts("红灯");
            traffic_light_state = green_light;
            break;
        case green_light:
            puts("绿灯");
            traffic_light_state = yellow_light;
            break;
        case yellow_light:
            puts("黄灯");
            traffic_light_state = red_light;
            break;
        default:
            puts("What the fuck?");
            break;
    }
}
```

## Using conditional-expression operators replaces if-else

```c
#include <stdio.h>
#include <stdint.h>
#include <inttypes.h>
#include <stdbool.h>

int main()
{
    // ? :
    uint8_t score = 85;

    char grade;

    grade = (score >= 90) ? 'A' :
            (score>= 80) ? 'B' :
            (score >= 70) ? 'C' : 'D';

    printf("Score: %" PRIu8 ", Grade: %c\n", score, grade);

    // the same as:
    // if (score >= 90)
    // {
    //     grade = 'A';
    // }
    // else
    // {
    //     if (score >= 80)
    //     {
    //         grade = 'B';
    //     }
    //     else
    //     {
    //         if (score >= 70)
    //         {
    //             grade = 'C';
    //         }
    //         else
    //         {
    //             grade = 'D';
    //         }
    //     }
    // }
}
```

## guard clauses(卫语句)

卫语句的思想是提前将少数的不能成立的选项排除，并提前return。使用卫语句可以简化if-else的逻辑结构，提高代码的可读性。

如下面的例子所示

```c
#include <stdio.h>
#include <stdint.h>
#include <inttypes.h>
#include <stdbool.h>

void check_car_rent(uint8_t age, uint8_t driving_exp_years);

int main(void)
{
    // 租车案例
    // age >= 21, 驾驶经验一年或一年以上

    uint8_t age = 23;
    uint8_t driving_exp_years = 2;

    check_car_rent(age, driving_exp_years);

    return 0;
}

void check_car_rent(uint8_t age, uint8_t driving_exp_years)
{
    // 卫语句
    if (age < 21)
    {
        puts("You are too young.");

        return;
    }

    if (driving_exp_years < 1)
    {
        puts("You don't have enough experience.");

        return;
    }

    puts("Satisfy all contions.You can rent the car.");
}
```

## switch-case 和 if-else 的根本区别

1. `switch-case` 是根据表达式的值进行判断。这个表达式的类型应是integer。`if-else` 是根据表达式的布尔值进行判断。这个表达式最后的计算出的结果应是bool类型。

如果同样模拟坐电梯去8层，`switch-case` 相当直接按下8层去到8层。`if-else` 相当于一层一层问。是1层吗？不是；是2层吗？不是……是8层吗？是。停止

从这个角度而言，`switch-case` 比 `if-else` 更快。

现如今，由于现代编译器对 `if-else` 的优化，这种差距对于现代的CPU来说变得微乎其微。

2. 二者的默认行为不同。`if-else`可以不写默认行为，但是`switch-case`总要有一个默认的default。

# 循环

程序设计为什么要有循环：

1. 避免代码重复
2. 处理大量的数据
3. 可以控制灵活的行为

循环的作用：

1. 执行重复的任务
2. 构造检查机制
3. 简化代码

在企业中，在处理大量数据和性能敏感的一些应用当中，尽可能在循环体中减少不必要的计算，减少函数的调用。或者在使用数据结构时明确，某些数据结构可能会破坏循环。

循环中要具有代码的可维护性。

while循环需要检查的5项内容

* 初始化
* 循环的判断条件
* 迭代变量是否有在变动

排除循环的问题后。检查循环体内的逻辑判断，检查中最简单的debug方式就是使用printf()将想看的表达式的值输出。

## while

### 自动贩卖机

```C
#include <stdio.h>
#include <stdint.h>
#include <stdbool.h>
#include <inttypes.h>

int main(void)
{
    /*
        自动贩卖机
        
        这个机器只支持硬币

        假设只卖一种饮料，每瓶价格是$5
    
        怎样才能给客户饮料呢？

        用户需要一直投币，直到金额足够，这样机器才可以提供饮料哦

        只接受$1, $2, $5的币种
    */

    // 1. 初始化

    // 饮料的价格 常量
    const uint32_t PRICE = 5;
    printf("%" PRIu32 "\n", PRICE);

    // 用户当前投入的金额总数 迭代(每次增加)
    uint32_t balance = 0;
    
    // 每次投入的硬币
    uint32_t coin;

    // 用戶使用提示
    puts("欢迎使用自动贩卖机！本机器只提供一种饮料，价格是$5");
    puts("请投币（只接受$1, $2, $5面值的三种硬币）");

    // 2. 处理循环的条件
    // 什么情况下会一直投币？
    // balance < PRICE
    while (balance < PRICE)
    {
        puts("余额不足, 请投币: 只接受1，2，5三种硬币");

        // 模拟投币，假设用户输入的金额就是投币
        scanf("%d", &coin);

        // 检查每次投币是否有效 1,2,5
        if (coin == 1 || coin == 2 || coin == 5)
        {
            balance += coin;
        }
        else
        {
            printf("对不起，我们不接受%" PRIu32 "面值的硬币，请重新投币\n", coin);
        }
    }
    // 找零
    if (balance > PRICE)
    {
        printf("剩余的$%" PRIu32 "已退回，请收好您的零钱", balance - PRICE);
    }
    
    puts("谢谢惠顾，请取走您的饮料。");
}
```

自动贩售机实例中如果把所有的uint32_t都换成uint8_t。并且把相应的输出的格式也改变一下。那么在scanf("%" PRIu8, &coin);这条语句执行过后，PRICE这个常量的值会变成0。具体原因可能和内存的分配有关，uint8_t占一个字节，而`"%"PRIu8`实则为`%u`，其占4个字节。所以在更改coin的值的时候，更改了4个字节，从而向上更改了常量`BALANCE`的值。

### 计算输入数字的加和并处理字符和字符串的退出检测问题

```c
#include <stdio.h>
#include <stdint.h>
#include <stdbool.h>
#include <inttypes.h>
#include <stdlib.h>
#include <errno.h>

int main(void)
{
    // 初始化数字的和，初始时和为0
    int32_t sum = 0;

    // 输入的字符数组（字符串）
    char input[50];

    // 用户的输入提示信息
    puts("请输入一系列数字(不超过50位)，用回车隔开，我们将会计算他们的和，输入q结束求和程序");

    // input数组的尾部指针
    // 用于做strtol()函数的参数输入
    char* end;
    // 死循环，直到用户输入q，break出循环，退出程序
    while (true)
    {
        // 每次循环开始将错误提示信息重置清零
        errno = 0;

        // 提示用户应该输入数字了
        puts("请输入一个数字或输入q退出");

        // scanf重新赋值，将input字符数组重新赋值
        scanf("%49s", &input);

        if (input[0] == 'q' && input[1] == '\0')
        {
            puts("程序退出");
            break;
        }

        // strtol()函数可以检查是否存在错误(非数字，数字和字符混合等)
        // 但是不能检查输入是否超范围
        long number = strtol(input, &end, 10);

        // 非法输入检查
        if (end == input || *end != '\0')
        {
            puts("无效输入，请输入一个数字或'q'");
            
            // 无效输入，需要重新输入，循环重新开始
            continue;
        }
        // 超出范围检查
        if (errno == ERANGE )
        {
            printf("数字超出范围，请输入一个大于等于%" PRId32 "小于等于%" PRId32 "的整数\n", INT32_MIN, INT32_MAX);

            // 超出范围，需要重新输入，循环重新开始
            continue;
        }

        // 经过两道检查都没问题后，执行加和操作
        sum += (int32_t) number;
    }
    printf("The summary is %" PRId32 "\n", sum);
}
```

## do-while

```c
#include <stdio.h>
#include <stdint.h>
#include <inttypes.h>
#include <stdbool.h>

int main(void)
{
    // 跑步的总圈数
    const uint32_t TOTAL_LAPS = 10;

    // 当前跑的圈数
    // 初始值为0
    uint32_t current_laps = 0;

    // while循环模拟跑步
    // 先检查圈数是否足够，不够再跑
    while (current_laps < TOTAL_LAPS)
    {
        current_laps++;
        printf("当前圈数: %" PRIu32 "\n", current_laps);
    }

    // 为do-while循环模拟，将圈数清零
    current_laps = 0;

    // do-while循环模拟跑步
    // 先跑一圈再说
    do
    {
        current_laps++;
        printf("当前圈数: %" PRIu32 "\n", current_laps);
    } while (false);
    // 发现即使条件是false也会先跑一圈

    return 0;
}
```

### Difference between while and do-while

* `while` 在执行之前判断是否满足循环条件，不满足不执行循环体。
* `do-while` 在执行过一次之后才判断是否满足循环条件，无论是否满足条件，都会执行循环体一次。

### Apply do-while to achieve a menu

```c
#include <stdio.h>
#include <stdint.h>
#include <inttypes.h>
#include <stdbool.h>

int main(void)
{
    uint8_t choice;
    // 游戏菜单模拟
    do 
    {
        // 显示菜单
        puts("****主菜单****");
        puts("1. 新游戏");
        puts("2. 载入游戏");
        puts("3. 退出");
        puts("****请选择一个选项****");

        // 严谨的程序应该有输入检查，这里是案例，暂不做检查功能了
        scanf("%" PRIu8, &choice);

        // 处理用户的选择
        switch (choice)
        {
            case 1:
                puts("新游戏已经启动");
                // 新游戏的逻辑
                // TODO
                break;
            case 2:
                puts("载入游戏中");
                // 载入游戏的逻辑
                // TODO
                break;
            case 3:
                puts("感谢游玩，再见");
                break;
            default:
                puts("无效选项，请重新选择");
                break;
        }
    } while (choice != 3);  // 只要用户不输入3就一直循环
}
```

### Apply do-while to achieve a guess random number game

```c
#include <stdio.h>
#include <stdint.h>
#include <inttypes.h>
#include <time.h>
#include <stdlib.h>

int main(void)
{
    // 随机生成的随机数，用于给用户猜测
    uint32_t secret_num;

    // 用户的猜测值
    uint32_t guess;

    // 生成随机数
    srand(time(NULL));
    // 生成1-100的随机数
    secret_num = rand() % 100 + 1;

    puts("猜猜我想的是哪一个数(1-100)?");

    do
    {
        puts("请输入你的猜测:");
        scanf("%" PRIu32, &guess);

        // TODO 输入检查
        if (guess < secret_num)
        {
            puts("太小了，再试试看吧");
        }
        else if (guess > secret_num)
        {
            puts("太大了，再试试看吧");
        }
    } while (guess != secret_num);

    puts("你猜对了，很棒！");
}
```

## for

```c
#include <stdio.h>
#include <stdint.h>
#include <inttypes.h>
#include <stdbool.h>
#include <math.h>

int main(void)
{
    /*
        用户输入一个数
        
        判断是否是素数并返回结果
    */

    // 用户输入的数
    uint32_t num;
    
    // 是否为素数的bool值，默认为true
    bool is_prime = true;

    // 用户输入提示
    puts("请输入一个大于等于二的正整数，我们将判断它是否为素数，并返回结果");

    // 用户输入，结果存入num
    scanf("%" SCNu32, &num);

    // 输入检查 TODO


    if (num <= 1)
    {
        // 因为没有做输入检查
        // 用户输入小于1的数，默认不是素数
        is_prime = false;
        
        // 提示用户输入的数不合规
        puts("This number is not a legal number.");
        return 0;
    }

    // 素数判断
    // 将一个数分成两个数的乘积
    // 其中一个一定 >= 原数的平方根，另一个一定 <= 原数的平方根
    // 所以只需要循环到sqrt(num)即可
    // 即 index <= sqrt(num)
    // sqrt(num) 是一个double类型的数据
    // 在C语言中，开平方是一个比较费时的操作
    // 为了提高效率，可将开平方操作改写成乘方操作
    // 即 index * index <= num
    // 在循环中，不要使用sqrt()操作
    for(uint32_t index = 2; index * index <= num; index++)
    {
        if (num % index == 0)
        {
            is_prime = false;
            break;
        }
    }
    
    // 输出判断结果
    if (is_prime)
    {
        puts("This number is a prime number.");
    }
    else
    {
        puts("This number is not a prime number.");
    }
}
```

### practice pyramid

```c
#include <stdio.h>
#include <stdint.h>
#include <inttypes.h>

int main(void)
{
    // 金字塔的层数
    uint32_t level;

    // 提示用户输入金字塔层数
    puts("请输入金字塔的层数");

    // 用户输入
    scanf("%" PRIu32, &level);

    // 输入检查 TODO

    // 输出提示
    puts("得到的金字塔如下");

    for (uint32_t raw = 1; raw <= level; raw++)
    {
        // 计算并提前存储每一层的空格
        uint32_t spaces_num = level - raw;

        // 金字塔前面的空格
        for (uint32_t index = 1; index <= spaces_num; index++)
        {
            printf("  ");
        }

        // 金字塔前半边数字
        for (uint32_t index = 1; index <= raw; index++)
        {
            printf("%" PRIu32" ", index);
        }

        // 金字塔后半边数字
        for(uint32_t index = raw - 1; index >= 1; index--)
        {
            printf("%" PRIu32" ", index);
        }
        
        // 金字塔后面的空格
        for (uint32_t index = 1; index <= spaces_num; index++)
        {
            printf("  ");
        }

        // 一行输出完成后换行
        printf("\n");
    }

    // TODO 
    // 多次使用printf造成了性能的浪费
    // 未来可以进一步优化
}
```

### apply for to simulate a progress bar

```c
#include <stdio.h>
#include <stdint.h>

// #define __STDC_FORMAT_MACROS 1

#include <inttypes.h>
#include <windows.h>


int main(void)
{
    // 模拟总数据量
    const uint32_t total_steps = 100;

    // 模拟提示信息
    puts("处理中，请稍后");

    // 模拟进度条
    for (uint32_t index = 0; index <= total_steps; index++)
    {
        printf("\r[");

        // 打印进度条的完整部分
        for (uint32_t completed_index = 0; completed_index < index; completed_index++)
        {
            printf("#");
        }

        // 打印进度条未完成的部分
        for (uint32_t uncompleted_index = index; uncompleted_index < total_steps; uncompleted_index++)
        {
            printf(" ");
        }

        printf("] %" PRIu32 "%%", index * 100 / total_steps);
        // (已经传输的数据量 / 文件总大小) * 100

        // 确保进度条及时显示
        fflush(stdout);

        // 模拟程序运行过程
        Sleep(100);
    }

    // 处理完成提示信息
    puts("\n处理完成");

}
```

# 数组

多个数据和变量如何处理？

1. 数据组织		结构体
2. 资源管理		数据结构
3. 性能优化		算法

数组是最基础的数据组织，资源管理方式。

术语说明

1. `numbers[0]`		下标为0的数组
2. 元素		里面的东西

注意事项

1. 数组定义时下标必须是常量。
   * 这个常量必须是宏定义常量，而不能是const常量
   * const常量在编译时仍然以变量身份出现，所以使用const常量无法通过编译

2. 数组使用前必须要初始化。

   * `uint32_t numbers[5];` 这种形式只能叫做声明。
   * `uint32_t numbers[5] = {1, 2, 3, 4, 6};` 这种形式才能叫做初始化。

3. 简单初始化：

   * `uint32_t numbers[5] = {0};` 所有数组都初始化值为0。

   * `uint32_t numbers[5] = {1};` 除下标为0的数组值为1，剩下的都为0。

4. 常见错误

   1. 越界访问

      ```c
      uint32_t numbers[5] = {0};
      printf("%" PRIu32"\n", numbers[6]);
      ```

   2. 未初始化数组

      ```c
      uint32_t uninit_array[5];
      printf("%" PRIu32 "\n", uninit_array[5]);
      ```

   3. 数组大小错误

      ```c
      uint32_t wrone_size_array[-1];
      ```

5. 常见警告

   1. 部分初始化

      ```c
      uint32_t part_init_array[SIZE] = {1, 2};
      ```

6. 提示：总是初始化数组

   ```c
   uint32_t numbers[SIZE] = {0};
   ```

数组的内存分布：

​	以 `uint32_t array[10] = {0};` 为例，这将在内存中开辟一块4bytes × 10的地址连续内存空间，用于存放数组中所有数据的值。

遍历

排序

查询

增删改查(CRUD)	数据结构	算法 优解

边界(Boundary)

动态数组

C11新特性动态数组

## 隐式初始化说明

```c
// 参数列表中传入的matrix[][3]也是固定列数不固定行书的二维数组
void processMatrix(int matrix[][3], int rows);

// 隐式确定数组大小初始化
int arr[] = {1, 2, 3, 4, 5};

char greeting[] = "Hello";

// 行号无所谓，列必须固定下来
int matrix[][3] = {
    {1, 2, 3}, 
    {4, 5, 6},
    {7, 9, 0},
    {3, 2, 5}
};
```



## 实例——计算平均分

```c
#include <stdio.h>
#include <stdint.h>
#include <inttypes.h>

// 学生的数量 
#define STUDENTS_NUMBER 5

int main(void)
{
    /*
        假如我们有五个学生的成绩，我们需要计算平均成绩，找出最高分、最低分
    */


    // 定义一个数组存储所有学生的成绩
    uint32_t grades[STUDENTS_NUMBER] = {85, 93, 78, 90, 99};

    // 所有学生成绩的和
    uint32_t sum = 0;

    // 最高分
    uint32_t max_grade = grades[0];

    // 最低分
    uint32_t min_grade = grades[0];

    // 平均分
    double average_score;

    // 提示信息
    puts("所有人的成绩单如下:");

    for (uint32_t index = 0; index < STUDENTS_NUMBER; index++)
    {
        printf("%" PRIu32 "号学生的成绩为: %" PRIu32 "\n", index + 1, grades[index]);

        // 计算加和
        sum += grades[index];

        // 寻找最高分
        if (grades[index] > max_grade)
        {
            max_grade = grades[index];
        }

        // 寻找最低分
        if (grades[index] < min_grade)
        {
            min_grade = grades[index];
        }
    }
    // 计算平均分
    average_score = (double) sum / STUDENTS_NUMBER;

    // 输出平均分
    printf("The average score is %lf.\n", average_score);

    // 输出最高分
    printf("最高分: %" PRIu32 "\n", max_grade);

    // 输出最低分
    printf("最低分: %" PRIu32 "\n", min_grade);
}
```

## 实例——计算字符串中每个字符出现的频率

```c
#include <stdio.h>
#include <stdint.h>
#include <inttypes.h>
#include <ctype.h>

#define LETTER_COUNT 26

int main(void)
{
    // size: 26 每一个格子代表一个字母出现的频率
    uint32_t letters_frequency[LETTER_COUNT] = {0};
    
    // 给定一段需要统计的字符串
    char text[] = "Example text for frequency analysis.";

    // 统计每个字母出现的次数
    for (uint32_t index = 0; text[index] != '\0'; index++)
    {
        // 将读取到的字母转化为小写
        char ch = tolower(text[index]);

        // 将读取到的字母对应的数组的值+1
        // 忽略空格等非26个字母的情况
        if (ch >= 'a' && ch <= 'z')
        {
            letters_frequency[ch - 'a']++;
        }
    }

    // 输出频率数组
    for (uint32_t i = 0; i < LETTER_COUNT; i++)
    {
        printf("The frequency of %c is %" PRIu32 ".\n", i + 'a', letters_frequency[i]);
    }
}
```

# Function 函数

函数可以理解为需要重复使用的代码块。将这部分代码单独起一个名字方便重复使用。

函数编写要领

1. 明确函数目的，明确它的功能将帮助你决定哪些输入是必须的（形式参数、模板），以及如何报告它的工作结果。
2. 识别所需要的输入
3. 确定函数的输出
4. 使用适当的数据类型
5. 函数的命名清晰，并且先声明后定义

## 全局变量和局部变量

局部变量：函数内的变量，作用域在函数内。

全局变量：函数外的变量，作用域在整个文件。

## 企业规范之使用void作为函数参数的必要性

### Example——function()

```c
#include <stdio.h>
#include <stdint.h>
#include <inttypes.h>

void greet();

int main(void)
{
    uint32_t n = 45;
    
    greet(n);
}

void greet()
{
    puts("Hello world!");
}
```

上述情况gcc不会提示任何的报错信息，且能够正常执行。

### Example——function(void)

```c
#include <stdio.h>
#include <stdint.h>
#include <inttypes.h>

// void greet();

void greet(void);

int main(void)
{
    uint32_t n = 45;
    
    greet(n);
}

// void greet()
// {
//     puts("Hello world!");
// }

void greet(void)
{
    puts("Hello world!");
}
```

gcc 提示 error 信息

```c
main.c: In function 'main':
main.c:13:5: error: too many arguments to function 'greet'
     greet(n);
     ^~~~~
main.c:7:6: note: declared here
 void greet(void);
      ^~~~~
```

## 函数的注释

```c
#include <stdio.h>
#include <inttypes.h>

int32_t add_two_numbers(int32_t num1, int32_t num2);

int main(void)
{
    int32_t result = add_two_numbers(5, 10);
    printf("The sum is: %" PRId32 "\n", result);

}

/**
 * Calculates the sum of two integers.
 * 
 * Parameters:
 * - num1: The first integer for the sum.
 * - num2: The second integer for the sum.
 * 
 * Returns:
 * - The sum of num1 and num2 as an int32_t.
 * 
 * Notes:
 * - The function uses int32_t to ensure the calculation is compatiable across different platforms.
 * - This is a basic example intended for beginners who are not yet familiar with pointer.
 */
int32_t add_two_numbers(int32_t num1, int32_t num2)
{
    return num1 + num2;
}

```

# 地址和指针

地址：唯一标识内存中存储数据的位置。

为什么需要地址

* 可以快速查看这个东西（内存）的内容（值）。甚至可以不用知道这个东西的名字（变量名）。

指针：不存具体的数据，只存变量的地址。

## Practice

```c
#include <stdio.h>
#include <stdbool.h>
#include <stdint.h>
#include <inttypes.h>

int main(void)
{
    uint32_t building_floors[5] = {101, 102, 103, 104, 105};

    // 快递员需要寻找的目标住户
    uint32_t target_floor = 103;

    // ptr_floor_103 -> (指向) &building_floors[2]
    uint32_t *ptr_floor_103 = &building_floors[2];
    printf("ptr_floor_103指针变量保存的是: %p\n", ptr_floor_103);
    printf("ptr_floor_103指针变量指向的值是: %" PRIu32 "\n", *ptr_floor_103);
    printf("快递员通过*(指针相当于一个地图工具), 他带着ptr_floor_103这个指针变量去寻找....\n");
    printf("于是他找到了业主的门牌号%" PRIu32 "\n", *ptr_floor_103);

    // 快递员找到你了。。。你要求快递员: 我们这边门牌号发生变化了，我现在的门牌号是106
    int* ptr_new_106 = ptr_floor_103;

    *ptr_new_106 = 106;

    // 门牌号发生改变
    printf("building_floors[2] = %" PRIu32 "\n", building_floors[2]);

    // 尝试使用错误类型的指针去指向uint32_t的数据
    char *ptr_floor_103_char = &building_floors[2];
    
    // 尝试读取错误指针类型中存放的地址
    printf("ptr_floor_103_char指针变量保存的是: %p\n", ptr_floor_103);
    
    // 尝试用错误的输出类型输出错误指针中存储地址中存放的值。
    printf("ptr_floor_103_char指针变量指向的值是: %c\n", *ptr_floor_103);

    bool is_found = false;

    printf("快递员开始在大楼中寻找 %" PRIu32 "...\n", target_floor);

    for (uint32_t i = 0; i < 5; i++)
    {
        printf("用户%" PRIu32 "的地址: %p\n", building_floors[i], &building_floors[i]);

        if (building_floors[i] == target_floor)
        {
            printf("快递员找到了住户%" PRIu32 "的地址: %p", target_floor, (void*)&building_floors[i]);

            is_found = true;
            break;
        }
    }

    if (! is_found)
    {
        puts("快递员没有找到该住户");
    }

    return 0;
}

```

## 指针星号的企业风格规范以及容易引发的问题

```c
int* p;		// 微软写法，int*，表明强调这个变量是一个int*(整型指针)类型的变量
int *p;		// 更强调这个变量实际上是一个指针

int* p, q;	// 避免一行定义多个变量
int *p, *q;		// 非得一行定义多个指针
int* p, * q;	// 微软一行定义多个指针的写法

// 相当于
int* p;
int q;
```

## 野指针

野指针：指向了一个无效的内存地址或是已经释放的内存地址的指针。

非常危险。

野指针会访问一个不可描述的内存空间，会导致不可预测的行为。

野指针非常危险，程序员必须对野指针做出处理。

## 空指针

空指针：通常没有指向任何有效内存地址的指针。

```c
#include <stdio.h>
#include <stdint.h>

int main(void)
{
    // 空指针，没有指向任何楼层的地址
    uint32_t* ptr_to_floor = NULL;

    // 尝试通过空指针访问数据
    if (ptr_to_floor == NULL)
    {
        printf("没有指定楼层的地址！\n");
        // shortcut 不做任何处理，即双击没有反应
    }
    else
    {
        printf("楼层的地址是: %p, 楼层号: %d\n", (void*) ptr_to_floor, *ptr_to_floor);
    }

    return 0;
}
```

## 数组的首地址与指针的算数运算与比较运用

```c
#include <stdio.h>
#include <stdint.h>

int main(void)
{
    // 指针的算数运算

    /*********数组的首地址 **********/
    // int
    int numbers[] = {10 ,20 ,30, 40, 50, 60, 70, 80, 90};

    int* ptr = numbers;     // &numbers[0]
    // 数组在内存中是连续的
    // 0 -> 0000000000009000
    // 所以只需要一个首地址就可以找到整个数组在哪。

    // 计算数组的大小
    int size = sizeof(numbers) / sizeof(numbers[0]);
    // sizeof(numbers) 这个部分会计算整个数组所占用的内存的大小，单位是字节。
    // sizeof(numbers) 这个部分会返回给我一个整个数组的空间所占的大小。

    printf("size = %d\n", size);

    printf("数组原始数据\nnumbers[] = { ");
    for (int i = 0; i < size; ++i)
    {
        printf("%d ", numbers[i]);
    }
    printf("}\n\n");

    /**********指针的加减法 **********/

    // 使用指针加法移动指针
    // 由于ptr在声明时是一个指向int类型的指针
    // 而int类型是占4个字节的
    // 所以ptr在 +1 之后会向后跳 4 个字节
    // 也就是说
    // 指针的加法、减法移动的地址的单位取决于指针的类型
   
    // 此时指针将从指向数组下标为0的数据 10 变为指向数组下标为1的数据 20
    ptr += 1;
    
    printf("numbers[ptr += 1] : %d\n\n", *ptr);

    // 使用指针剑法回到第一个元素
    ptr -= 1;

    printf("回到第一个元素numbers[ptr -= 1] : %d\n\n", *ptr);

    // 指针之间的减法，计算距离
    int* start_ptr = &numbers[0];
    int* end_ptr = &numbers[size - 1];

    // 输出数组首位地址之家距离的字节数
    printf("数组首尾之间的距离是: %td\n\n", end_ptr - start_ptr);

    // end_ptr - start_ptr 的类型: ptrdiff_t
    // ptrdiff_t 的类型
    // 在32位操作系统中。这个类型一般是占4个字节: int 类型
    // 在64位操作系统中，这个类型一般是占8个字节: long int 类型

    
    /***********  指针之间的比较 *********/
    puts("比较指针指向的元素: ");
    
    if (start_ptr < end_ptr)
    {
        puts("start_ptr 指向的元素在 end_ptr 所指向的元素之前");
    }

    // 使用指针遍历数组
    printf("使用指针遍历数组\n *p 外部指针遍历 {");
    for (int* p = start_ptr; p <= end_ptr; p++)
    {
        printf("%d ", *p);
    }
    printf(" }\n\n");

    // 使用指针加法逐个访问数组中的每个元素的反向顺序
    printf("使用指针减法逐个访问数组中的每个元素的反向顺序\n*p = {");
    for (int* p = end_ptr; p >= start_ptr; p--)
    {
        printf("%d ", *p);
    }
    printf(" }\n\n");

    /********** 指针加减整数访问特定元素 **********/
    puts("指针加简整数访问特定元素: ");
    int offset = 3;
    printf("第四个元素(使用加法): *（start_ptr + offset) = %d\n\n", (start_ptr + offset));

    // 回退到第三个元素
    printf("回退到第三个元素(从第四个元素开始回退) * (start_ptr + offset - 1) = %d\n\n", *(start_ptr + offset - 1));

    /********** 比较两个指针 *********/
    int* middle_ptr = &numbers[size / 2];   // 指向数组中的元素

    printf("比较两个指针指向的位置:\n");

    if (start_ptr < middle_ptr)
    {
        puts("start_ptr 指向的元素在 end_ptr 所指向的元素之前\n");
    }

    if (end_ptr > middle_ptr)
    {
        puts("end_ptr 指向的元素在 middle_ptr 所指向的元素之后");
    }
    return 0;
}

```

## 数组的地址与数组的第一个元素地址（数组首地址）

如果我们有一个数组`uint32_t array[] = {10, 20, 30, 40, 50, 60, 70, 80, 90}`

其数组地址可表示为`&array`

其数组首地址可表示为`array`

二者之间的区别在哪呢？

1. `&array` 表示的是整个数组的地址，对`&array` +1 -> `&array + 1` 会跳跃整个数组长度*类型长度的字节，在这个例子中就是跳跃36个字节。
2. `array` 表示的是数组中第一个元素的地址，对`array` +1 -> `array + 1` 会跳跃类型长度的字节，在这个例子中就是跳跃4个字节。

这也对应了二者的数据类型的不同

1. 这个例子中，`&array` 的数据类型是 `uint32_t (*)[9]`，这个 ’9‘ 取决于数组的长度。
2. 这个例子中，`array` 的数据类型是 `uint32_t*` 

## Example——指针查找特定元素的的索引并返回

```c
#include <stdio.h>
#include <inttypes.h>
#include <stdbool.h>

// 将目标代码写成函数
// 查找特定元素的索引，返回是否找到，以及元素的索引
bool find_index_of_value(const uint32_t* array, size_t size, uint32_t target_value, size_t* target_index);

int main(void)
{
    uint32_t values[] = {10, 20, 30, 40, 50, 60, 70, 80, 90};

    uint32_t target_value = 40; 

    uint32_t* start_ptr = values;

    size_t values_size = sizeof(values) / sizeof(values[0]);

    size_t target_index = 0;

    bool is_found = find_index_of_value(values, values_size, target_value, &target_index);

    // bool is_found = false;

    // for (size_t i = 0; i < values_size; ++i)
    // {
    //     if (*(start_ptr + i) == target_value)
    //     {
    //         // 找到目标的下标
    //         target_index = i;
    //         is_found = true;
    //         break;
    //     }
    // }

    if (is_found)
    {
        printf("找到了%" PRIu32 " 的索引值为: %zu", target_value, target_index);
    }
    else
    {
        printf("没有找到%" PRIu32 "的索引值", target_value);
    }
}

bool find_index_of_value(const uint32_t* array, size_t size, uint32_t target_value, size_t* target_index)
{
    for (size_t i = 0; i < size; ++i)
    {
        if (*(array + i) == target_value)
        {
            *target_index = i;
            return true;
        }
    }

    return false;
}
```

## Example——指针访问多维数组

```c
#include <stdio.h>
#include <inttypes.h>
#include <stdbool.h>

int main(void)
{
    int matrix[2][3] = {
        {1, 2, 3}, 
        {4 ,5, 6}
    };

    // 一个指向长度为3的一维数组的指针
    int(*ptr)[3] = matrix;

    // int(*ptr)[3] : ptr是一个指针，它指向一个包含3个int元素的一维数组的指针

    // int* ptr[3] : ptr是一个指针数组，它里面包含3个指向int类型数据的指针
    
    for (int i = 0; i < 2; i++)
    {
        for (int j = 0; j < 3; j++)
        {
            printf("%d ", ptr[i][j]);
        }
        printf("\n");
    }
    printf("\n");

    int numbers[] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};

    int* ptr_numbers = numbers;

    for (int i = 0; i < 10; ++i)
    {
        printf("%d ", ptr_numbers[i]);
    }
}
```

## 思考：数组和指针本质是一样的

通过上一个例子可以看出，对于一个名为 `numbers` 的一维数组，我们可以使用它的首地址 `number` 来声明一个指针：

```c
int numbers[] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
int* ptr_numbers = numbers;
```

此时，使用 `numbers[i]` 和 `ptr_numbers[i]` 去访问数组中的元素将会得到同样的结果。

```c
for (int i = 0; i < 10; ++i)
{
    // printf("%d ", numbers[i]);
    printf("%d ", ptr_numbers[i]);
}
```

输出结果均为：

```shell
1 2 3 4 5 6 7 8 9 10
```

## 函数的值传递和地址引用传递

函数的传递方式有三种：值传递、指针传递、引用传递。

参考博客：

1. [值传递、指针传递、引用传递：深入理解函数参数传递方式_函数 值传递 指针传递-CSDN博客](https://blog.csdn.net/Hamdh/article/details/133881214)
2. [C语言传递指针参数的陷阱 | BraveY](https://bravey.github.io/2020-12-12-C语言传递指针参数的陷阱)

```c
#include <stdio.h>
#include <inttypes.h>
#include <stdbool.h>

void add_ten_by_value(int32_t* value);

int main(void)
{
    int32_t my_value = 5;
    printf("原本的值: %" PRId32 "\n", my_value);

    // 指针作为函数参数的使用
    add_ten_by_value(&my_value);

    printf("已经调用add_ten_by_value之后的值: %" PRId32 "\n", my_value);
}

void add_ten_by_value(int32_t* value)
{
    *value += 10;
}
```

## Example——员工薪资系统



## const int、const int *、int *cosnt、const int * const、const int &的区别

一、const int
在定义变量的时候必须初始化，否则报错。

```c
#include "stdafx.h"


int _tmain(int argc, _TCHAR* argv[])
{
	const int i = 0;
	//i = 4;             //error C3892: “i”: 不能给常量赋值

	//error C2734: “k”: 如果不是外部的，则必须初始化常量对象
	//const int k;       
	//k = 3;             //error C3892: “k”: 不能给常量赋值
	return 0;
}

```

二、const int *
1、声明该指针变量指向的是常量，即该指针变量的内容可以改变，但是该内容指向的内容不可改变！

```c
#include "stdafx.h"


int _tmain(int argc, _TCHAR* argv[])
{
	const char *p = "Hello world!";
	//p[3] = '3';  //error C3892: “p”: 不能给常量赋值
	p = "Hi!";
	return 0;
}

```

2、虽然指向的内容不可改写，但是delete则是可以的。例子：

```c
	const int *p = new int[3];
	delete []p;
	p = nullptr;
```

因为**delete**只是告诉系统，现在p所指向的这块内存已还给自由存储区，不再被使用，可以被其他程序改写。而此时p依旧指向这块不可使用的内存，故需要对p进行清零。

三、int *const
声明该指针变量为常变量，即指针变量里面的内容不可改变，但是该内容指向的内容可以改变！

```c
#include "stdafx.h"


int _tmain(int argc, _TCHAR* argv[])
{
	char *const p = "Hello world!";
	p[3] = '3';  
	//p = "Hi!";  error C3892: “p”: 不能给常量赋值
	return 0;
}

```

四、const int * cosnt
声明该指针变量里面的内容不可改变，同时该内容指向的内容亦不可改变。

```c
#include "stdafx.h"


int _tmain(int argc, _TCHAR* argv[])
{
	const char *const p = "Hello world!";
	//p[3] = '3';  //error C3892: “p”: 不能给常量赋值
	//p = "Hi!";   //error C3892: “p”: 不能给常量赋值
	return 0;
}

```

五、const int &
在引用前面加上const，代表该引用为常引用，即被引用的对象不可改变。若是在形参中使用，则不可达到在函数里面修改变量值的目的。

```c
#include "stdafx.h"
#include <iostream>
using namespace std;

int add (const int &a,int &k)
{
	//a += 7;  //error C3892: “a”: 不能给常量赋值
	k += 8;
	return (a+k);
}

int _tmain(int argc, _TCHAR* argv[])
{
	int a = 5;
	int k = 9;
	const int &b = a;
	//b = 7;  //error C3892: “b”: 不能给常量赋值
	int t = add(a,k);
	cout<<"a = "<<a<<endl;
	cout<<"b = "<<b<<endl;
	cout<<"t = "<<t<<endl;
	cin.get();
	return 0;
}

```

# 结构体

## 定义和初始化

```c
#include <stdio.h>
#include <inttypes.h>

// 结构体(Structures)
// 数据类型
// 在单文件编程时，结构体一般定义在函数外
// 在多文件编程时，结构体定义一般放在单独的文件中

// 说白了，我们想要定义什么类型？
// 我们定义了一个表示日期的结构体 Date
// 其中，整个结构体包含了三个int类型的成员
// 显示定义结构体
typedef struct Date {
    uint32_t day;
    uint32_t month;
    uint32_t year;
} Date;

// 创建结构体
struct Person
{
    char name[50];
    uint32_t age;
    float height;
    // ...
};


int main(void)
{
    Date today = {30, 7, 2024};

    // 初始化结构体变量
    struct Person frank = {"frank", 30, 2.83f};

    // 通过.访问成员
    printf("Today's date is: %" PRIu32 "-%" PRIu32 "-%" PRIu32 " (print by .)\n", today.year, today.month, today. day);    

    // 通过指针访问成员
    Date* date_ptr = &today;
    printf("Today's date is %" PRIu32 "-%" PRIu32 "-%" PRIu32 " (print by ptr)\n", date_ptr->year, date_ptr->month, date_ptr->day);

    printf("%s is %" PRIu32 " years old and %.2f feet tall.\n", frank.name, frank.age, frank.height);
}
```

## 匿名结构体，函数参数为结构体

```c
#include <stdio.h>
#include <inttypes.h>

// 匿名结构体
typedef struct {
    char name[50];
    uint32_t id;
    float score;
} Student;

void print_stu(Student stu);

void update_score_by_value(Student stu, float new_score);

void update_score_by_ptr(Student* stu, float new_score);

int main(void)
{
    Student stu = {"John Doe", 123, 89.5f};

    puts("Before update:\n");

    print_stu(stu);

    update_score_by_value(stu, 100.0f);
    
    puts("After update by value:");

    print_stu(stu);

    update_score_by_ptr(&stu, 100.f);

    puts("After update by ptr:");

    print_stu(stu);
}

void print_stu(Student stu)
{
    printf("Student Name: %s\n", stu.name);
    printf("Student ID: %" PRIu32 "\n", stu.id);
    printf("Student Score: %.2f\n", stu.score);
}

void update_score_by_value(Student stu, float new_score)
{
    stu.score = new_score;
}

void update_score_by_ptr(Student* stu, float new_score)
{
    stu->score = new_score;
}
```

## 值语义初始化结构体变量

[Value semantics - Wikipedia](https://en.wikipedia.org/wiki/Value_semantics)

## 结构体数组

```c
#include <stdio.h>

// 匿名结构体
typedef struct {
    int x;
    int y;
} Point;
int main(void)
{
    Point point_array[3] = {
        {1, 2},
        {2, 3},
        {12, 10}
    };
}
```

## 结构体嵌套

```c
#include <stdio.h>

typedef struct
{
    char street[50];
    char city[50];
    char country[50];
} Address;

typedef struct
{
    char name[50];
    int age;
    Address address;
} Person;

int main(void)
{
    Person frank = {
        "Frank",
        190,
        {"SAIOJOIFIS ST", "SSXXXXXX", "CANDA"}
    };
    
    Person* ptr = &frank;
    
    printf("Name: %s\n", frank.name);
    printf("Address: %s, %s, %s\n", frank.address.street, frank.address.city, frank.address.country);
    printf("Address: %s, %s, %s\n", ptr->address.street, ptr->address,city, ptr->address.country);
}
```

# 枚举

```c
#include <stdio.h>

typedef enum
{
    MONDAY,     // 0
    TUESDAY,    // 1
    WEDNESDAY,  // 2
    THURSDAY,   // 3
    FRIDAY,     // 4
    SATURDAY,   // 5
    SUNDAY      // 6
} Weekday;

int main(void)
{
    Weekday day = SATURDAY;

    printf("%d\n", day);
    printf("%d\n", FRIDAY);
}
```

# 字符串 TODO



# 输入输出 TODO



# math.h TODO



# 表驱动法

像所有查找表一样，直接访问表取代了更复杂的逻辑控制结构。它们是“直接访问”，因为您不必跳过任何复杂的步骤即可在表中查找所需的信息。

## Example——成绩评分系统

```c
#include <stdio.h>
#include <stdint.h>
#include <inttypes.h>
#include <stdlib.h>
#include <stdbool.h>

char get_credits(uint32_t grade);

int main(void)
{
    uint32_t grade;

    // 输入提示信息
    puts("请输入你的成绩(0-100)，我们会给出你的评级");

    // 输入成绩
    scanf("%" SCNu32, &grade);

    printf("你的成绩等级是:%c\n", get_credits(grade));

}

char get_credits(uint32_t grade)
{
    // 多个if-else, 逻辑过于复杂
    // if (grade >= 90)
    // {
    //     return 'A';
    // }
    // else if (grade >= 80)
    // {
    //     return 'B';
    // }
    // else if (grade >= 70)
    // {
    //     return 'C';
    // }
    // else if (grade >= 60)
    // {
    //     return 'D';
    // }
    // else 
    // {
    //     return 'F';
    // }

    // 表驱动法
    // 非显式数组
    char grades[] = {'F', 'F', 'F', 'F', 'F', 'F', 'D', 'C', 'B', 'A'}; 
    return grades[grade / 10];
}
```



## 规则映射

```c
#include <stdio.h>
#include <stdint.h>
#include <inttypes.h>
#include <time.h>
#include <stdlib.h>

// 游戏选项
#define ROCK 1
#define PAPER 2
#define SCISSIORS 3

// 函数声明
void print_instrucions();
uint32_t get_player_move();
uint32_t get_computer_move();
void determine_winner(uint32_t player_move, uint32_t computer_move);
void print_choice(uint32_t choice);


int main(void)
{
    // 初始化随机数生成器
    srand(time(NULL));

    // 打印游戏说明
    print_instrucions();

    // 获取玩家和计算机的选择
    uint32_t computer_move = get_computer_move();
    uint32_t player_move = get_player_move();

    // 展示玩家和计算机的选择
    puts("你选择了");
    print_choice(player_move);
    puts("计算机选择了");
    print_choice(computer_move);

    // 获取游戏结果
    determine_winner(player_move, computer_move);

}

void print_instrucions()
{
    // 打印游戏说明
    puts("石头，剪刀，布，游戏开始！");
    puts("规则：输入数字，确定猜拳。1 (石头) > 3 (剪刀) > 2 (布)");
}

uint32_t get_player_move()
{
    uint32_t choice;

    scanf("%" SCNu32, &choice);

    // 输入范围检查
    while (choice < ROCK ||choice > SCISSIORS)
    {
        puts("输出无效，请重新输入");
        scanf("%" SCNu32, &choice);
    }

    return choice;
}
uint32_t get_computer_move()
{
    return (rand() % (SCISSIORS - ROCK + 1) + ROCK); 
}

void determine_winner(uint32_t player_move, uint32_t computer_move)
{
    /* 使用规则映射的方法判断赢家 */
    // 卫语句判读平局
    if (player_move == computer_move)
    {
        puts("平局");
    }

    // 定义一个胜利的规则映射，其中键是玩家的移动，值是玩家移动可以打败计算机的移动
    // 玩家的数组为 players[4] = {0, ROCK, PAPER, SCISSIORS};
    // 即是{0, 1, 2, 3}
    // 而玩家想要对应获胜，应为 {0, SCISSIORS, ROCK, PAPER};
    // 0是占位符
    uint32_t winner_moves[4] = {0, SCISSIORS, ROCK, PAPER};

    if (computer_move == winner_moves[player_move])
    {
        puts("你赢了");
    }
    else
    {
        puts("你输了");
    }
}
void print_choice(uint32_t choice)
{
    switch (choice)
    {
        case 1:
            puts("石头");
            break;
        case 2:
            puts("布");
            break;
        case 3:
            puts("剪刀");
            break;
        default:
            break;
    }
    
}
```

# 递归与尾递归(recursion and tail_recursive)

* Frank视频参考：

[141.为什么不建议使用递归以及递归和尾递归用途区别_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1Ae41117Gd?p=151&spm_id_from=pageDriver&vd_source=0c6e9aa27976c7e534f51b25bcdd53f0)

* 参考博客

[递归和尾递归的区别和原理-CSDN博客](https://blog.csdn.net/zcyzsy/article/details/77151709)

如果递归深度特别大，那会存在着栈溢出的风险。此时可以考虑使用尾递归来替代递归，来规避栈溢出的风险。同时，一般情况下，尾递归的效率要高于递归。尾递归的实现依赖于编译器的参数传递，所以不同的编译器对尾递归的实现方式不同。良好的尾递归的实现是依赖编译器的。

企业中使用递归和尾递归是很慎重的，原因：

1. 效率低
2. 内存开销大
3. 难以理解，代码不易于维护

## 递归实现阶乘

```c
#include <stdio.h>
#include <stdint.h>
#include <inttypes.h>

uint32_t factorial(uint32_t n);

int main(void)
{
    uint32_t number = 5;
    
    printf("%" PRIu32 "的阶乘是%" PRIu32 "\n", number, factorial(number));
}

uint32_t factorial(uint32_t n)
{
    if (n == 0)
    {
        return 1;
    }
    else
    {
        return n * factorial(n - 1);
    }
}
```



## 尾递归实现阶乘

```c
#include <stdio.h>
#include <stdint.h>
#include <inttypes.h>

uint32_t factorial(uint32_t n, uint32_t acc);
int main(void)
{
    uint32_t number = 5;
    
    printf("%" PRIu32 "的阶乘是%" PRIu32 "\n", number, factorial(number, 1));
}

uint32_t factorial(uint32_t n, uint32_t acc)
{
    if (n == 1)
    {
        return n * acc;
    }
    else
    {
        return factorial(n - 1, n * acc);
    }
}
```

## 企业使用迭代来代替递归

```c
#include <stdio.h>
#include <stdint.h>
#include <inttypes.h>

// 递归求解斐波那契数列的第n项
uint32_t fibonacci_recusion(uint32_t n);

// 尾递归求解斐波那契数列的第n项
uint32_t fibonacci_tail_recusive(uint32_t n, uint32_t fib_n_minus_2, uint32_t fib_n_minus_1);

// 迭代求解斐波那契数列的第n项
uint32_t fibonacci_loop(uint32_t n);

int main(void)
{
    uint32_t n = 45;

    printf("尾递归实现的斐波那契数列第%" PRIu32 "的值为 %" PRIu32 "\n", n, fibonacci_tail_recusive(n, 1, 1));

    printf("递归实现的斐波那契数列第%" PRIu32 "的值为 %" PRIu32 "\n", n, fibonacci_recusion(n));

    printf("循环迭代实现的斐波那契数列第%" PRIu32 "的值为 %" PRIu32 "\n", n, fibonacci_loop(n));
}

uint32_t fibonacci_recusion(uint32_t n)
{
    switch (n)
    {
    case 0:
        return 0;
        break;

    case 1:
        return 1;
        break;

    default:
        return fibonacci_recusion(n - 1) + fibonacci_recusion(n - 2);
    }
}

uint32_t fibonacci_tail_recusive(uint32_t n, uint32_t fib_n_minus_2, uint32_t fib_n_minus_1)
{
    switch (n)
    {
        case 1: 
            return 1;
            break;
        case 2:
            return 2;
            break;
        case 3:
            return fib_n_minus_2 + fib_n_minus_1;
            break;
        default:
            return fibonacci_tail_recusive(n - 1, fib_n_minus_1, fib_n_minus_2 + fib_n_minus_1);
            break;
    }
}

uint32_t fibonacci_loop(uint32_t n)
{
    uint32_t first = 1;
    uint32_t second = 1;
    uint32_t third;

    for (uint32_t i = 2; i < n; i++)
    {
        third = first + second;
        first = second;
        second = third;
    }

    return third;
}
```

# 作用域(Scope)与生命周期(Lifetime)

```c
#include <stdio.h>
#include <stdint.h>
#include <inttypes.h>

// 全局变量，全局作用域
// 生命周期从程序开始到程序结束
int32_t g_global_var = 10;

void demoFunction(void);

int main(void)
{
    // 作用域(Scope)
    // 一个函数内，一个文件内，整个程序内(配置文件)
    
    // 一个函数内的变量有效范围：局部作用域 Local Scope
    // 一个函数内有效范围的变量，或者局部作用域内的变量：局部变量
    
    demoFunction();
    
    // 尝试访问local_var将导致编译错误，因为它的作用域仅限于demoFunction内
    // local_var的生命周期将只在demoFunction执行的过程中，所以此时其生命周期已经结束
    // 所以尝试访问local_car会导致编译错误
    // printf("In main, Local var = %" PRId32 "\n", local_var);
    
    
    printf("In main, Global var = %" PRId32 "\n", g_global_var);
    
    // 全局变量的生命周期将在程序执行结束时结束
    return 0;
}

void demoFunction(void)
{
    // 局部变量，局部作用域
    int32_t local_var = 5;
    
    printf("Inside demoFunction, Local var = %" PRId32 "\n", local_var);
    
    printf("Inside domoFunction, Global var = %" PRId32 "\n", g_global_var);
    
    // 局部变量的生命周期在函数返回时结束
}
```

生命周期管理不当可能会导致的问题：

1. 内存泄漏
2. 访问已经被销毁的变量(悬挂引用)
3. 过度消耗资源

## 局部变量(Local Variables)

1. 作用域限定

2. 自动存储期

3. 初始值未定义

   * 在分配内存时，局部变量会被默认分配在栈上。此时内存默认的初始值是不会改变的。所以在定义局部变量时，应该在定义时即进行初始化。

   ```c
   void demonstrateLocalVariable(void)
   {
       // 局部变量声明
       // 声明时即定义
       int32_t local_var = 100;
       
       printf("Local variable inside function: %" PRId32 "\n", local_var);
   }
   ```

## 全局变量(Global Variables)

全局变量的一个重要功能是可以跨越函数边界，共享数据；从而可以减少传递给函数的参数数量，简化调用。

1. 程序范围内的可见性
2. 静态存储期
3. 默认初始化
   * 整型默认初始化为0，指针默认初始化为NULL

缺点：

1. 使用过多的全局变量会降低代码的可读性。
2. 会增加出错的风险。
3. 线程安全问题：在多线程环境中，未加锁的全局变量可能会导致数据竞争和不一致的问题。

## 静态局部变量(Static Local Variables)

```c
#include <stdio.h>
#include <stdint.h>
#include <inttypes.h>

void increment_counter(void);

int main(void)
{
    // 静态变量 static  variables

    for (uint32_t i = 0; i < 4; i++)
    {
        increment_counter();
    }

    // 静态局部变量的可见性只在它声明的函数当中
    // 在main函数中访问在increment_counter()函数中声明的counter变量的值是找不到的
    printf("The value of counter: %" PRIu32 "\n", counter);

    return 0;
}

void increment_counter(void)
{
    // 静态局部变量
    static uint32_t counter = 0;
    // 静态变量在函数内部声明，并且程序期间只初始化一次。即使函数执行结束，它的值也不会消失，而是保持到下次函数的调用。跨函数保持着状态和计数，直到程序结束。

    counter++;

    printf("Counter: %" PRIu32 "\n", counter);
}
```

## 静态全局变量(Static Global Variables)

静态全局变量仅在本文件中可见。

run_app.c

```c
#include <stdio.h>
#include <stdint.h>
#include <inttypes.h>
#include "helper.h"

// 静态全局变量仅能在本文件中可见
// 如果g_static_var这个全局变量被声明成静态全局变量
// 则helper.c中的try_access_g()函数会因为无法访问g_static_var这个变量而报错
// 此时即使在helper.c在文件中使用extern关键字声明g_static_var变量为外部全局变量也不行
static uint32_t g_static_var = 10;

void access_g (void);

int main(void)
{
    printf("Main before: %" PRId32 "\n", g_static_var);
    access_g();
    try_access_g();
}

void access_g (void)
{
    g_static_var += 5;
    printf("Inside access_g: %" PRId32 "\n", g_static_var);
}
```

helper.c

```c
#include <stdio.h>
#include <stdint.h>
#include <inttypes.h>

// 通过extern关键字声明对外部文件全局变量的访问
extern uint32_t g_static_var;

void try_access_g(void)
{
    g_static_var += 10;
    printf("Inside helper.c try_access_g: %" PRIu32 "\n", g_static_var);
}
```

## 块作用域和链接性

块作用域：{}最近的内{}即为变量的块作用域

链接性：外部链接性(外部文件也可用)，内部链接性（只在当前文件内部可用），无链接性（文件内部局部可用）

```c
#include <stdio.h>

void demo(int x);

int main(void)
{
    return 0;
}

// 函数作用域
// 'x'具有函数作用域
void demo(int x)
{
    // 作用域(Scope)
    // 链接性(Linkage)
    
    // 块作用域(Block Scope)
    int a = 10;		// 'a'具有块作用域，仅在demo()中可见
    if (a > 5)
    {
        int b = a + 5;	// 'b'具有块作用域，仅在if语句中可见
    }
    // 'i' 具有块作用域，仅在for中可见
    for (int i = 0; i < 100; i++)
    {
        
    }
}
```



# register寄存器声明

**寄存器**(Register) 是中央处理器内用来暂存指令、数据和地址的电脑存储器。寄存器的存贮容量有限，读写速度非常快。在计算机体系结构里，寄存器储存在已知时间点所作计算的中间结果，通过快速访问数据来加速计算机程序的执行。

```c
#include <stdio.h>

void demo_reg_var(void);

int main(void)
{
    demo_reg_var();

    return 0;
}

void demo_reg_var(void)
{
    // 声明寄存器变量
    // 我们建议编译器，尽可能将counter放在寄存器中
    register int counter;
    // 不能使用 &counter 获取counter的地址
    // 因为counter不在内存中，没有地址
    // 在现代编译器良好的优化下，已经很少有场景需要程序员主动告诉编译器需要将某个变量放在寄存器中，大部分情况下，编译器会做出良好的判断。

    for (counter = 0; counter < 10; counter++)
    {
        printf("%d\n", counter);
    }
}
```



# 输入需要有输入检查验证

输入检查和用户提示。

## scanf的简单使用

```c
#include <stdio.h>
#include <stdint.h>

int main(void)
{
    uint32_t number1;
    
    uint32_t number2;
    
    uint32_t number3;
    
    // 要求用户从键盘上输入，与我们交互
    // scan 扫描
    // "%d,%d,%d"代表了写入规则
    // 规则表示三个int值中间应用,隔开
    // 规则怎样定义，用户怎样输入。
    scanf("%d,%d,%d", &number1, &number2, &number3);
}
```

CSDN博客详解：

* [C语言总结-printf/scanf详细总结-CSDN博客](https://blog.csdn.net/runafterhit/article/details/106310833)

* [2.4 详解 scanf：格式、原理、返回值与混合数据处理-CSDN博客](https://blog.csdn.net/qq_53139964/article/details/140386269)

# 命名规范

命名规范常用下划线命名法和大（小）驼峰命名法。在一个项目中只使用一种命名方法来达到代码规范的统一。

