# Advance Filtering w/ `grep`
What we covered in the basics of `grep` is enough for most of he basic use-cases. But when we want to do some advance searching and filtering of information, involving something called expression based evaluation, we need to learn some expressions. These expressions are also classified into different types. They are:
1. Basic Regular Expressions (or BREs)
2. Extended Regular Expressions (or EREs)
3. Perl-Compatible Regular Expressions (or PCREs)

# Regular Expressions (`regex`, for short)
+ A regular expression is a pattern that describes a set of strings.
+ In regex, these special characters have special meaning: `. ? + * {} () | [] \ ^ $` .
+ All other characters are ordinary characters, and each ordinary character is a regular expression that matches itself.
    | Special Character | Description |
    | - | - |
    | **.** (called, a *period*) | it denotes an unspecified character. Any character can take its place. |
    | () | A whole expression may be enclosed in parentheses to override these precedence rules and form a subexpression |
    | **?** | denotes that the precedence item is optional and matched atmost once |

## Fundamentals
1. **Concatenation**: Concatenation is when you place multiple regex elements next to each other to match a sequence of characters. Essentially, the regex engine looks for the characters or patterns in the specified order.
2. **Alternatives**: Alternatives allow you to specify multiple possible matches using the | symbol. It acts like a logical OR, where the regex engine tries to match any of the alternatives.
3. **Repetition**: Repetition lets you specify how many times a pattern should occur. There are several ways to denote repetition:
| _*_ | denotes that the preceding item is matched zero or more times. |
| **+** | denotes that the preceding item is matched one or more times. |
| {n} | denotes that the preceeding item is matched exactly `n` number of times. |
| {n,} | denotes that the preceeding item is matched exactly `n` or more than number of times. |
| {,m} | denotes that the preceeding item is matched at most `m` number of times. |
| {n,m} | denotes that the preceeding item is matched at least `n` number of times, but not more than `m` number of times. |
| \| (called `infix operator`) | Two regular expressions may be joined by the infix operator ‘|’. The resulting regular
expression matches any string matching either of the two expressions, which are called alternatives. |

## Character Classes & Bracket Expressions
+ Character classes in regex allow you to define a set of characters that can match a single position in the input string. They are enclosed in square brackets `[ ]`.
+ A bracket expression is a list of characters enclosed by ‘[’ and ‘]’. It matches any single character in that list. 

### Basic Character Class
+ `[1234567890]` :: this bracket expression will match if there is any single digit number.
+ `[^1234567890]` :: this bracket expression will match non digit characters.

## Range Character Class
+ To create a range based filtration, use hyphens `-` . And it is inclusive in nature.
+ Example: `[a-g]` is similar to `[abcdefg]`

## Negated Character Class
+ If the first character of the list is the caret `^` , then it matches any character that is not present in the list, 
+ Example: `[^a-g]` ; any character that is not in this list `[abcdefg]`

+ `[:alnum:]` : checks for alphanumeric characters. Equivalent to -> `[0-9A-Za-z]`
+ `[:alpha:]` : checks for alphabet characters. Equivalent to -> `[A-Za-z]`
+ `[:blank:]` : checks for spaces and tabs.
+ `[:cntrl:]` : checks for control characters.
+ `[:digit:]` : all the digits. Equivalent to -> `[0-9]`
+ `[:punct:]` : checks for punctuators, which include -> `! " # $ % & ' ( ) * + , - . / : ; < = > ? @ [ \ ] ^ _ ` { | } ~`
+ `[:graph:]` : checks for graphical characters. Equivalent to -> `[:alnum:]` + `[:punct:]`
+ `[:print:]` : checks printable characters. Equivalent to -> `[:alnum:]` + `[:punct:]` + `space`
+ `[:space:]` : checks for all kinds of space characters. They include: tab, newline, vertical tab, form feed, carriage return, and whitespace.
+ `[:lower:]` : checks for all lowercase characters. Equivalent to -> `[a-z]`
+ `[:upper:]` : checks for all uppercase characters. Equivalent to -> `[A-Z]`
+ `[xdigits]` : checks for all the hexadecimal digits. Equivalent to -> `[0-9a-fA-F]`