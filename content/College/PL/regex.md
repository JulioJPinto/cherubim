---
title: Regex
---

# Regex Rules
There's not a lot to know about the rules behind Regex. 


### Quantifiers

| Value | Meaning |
| --- | --- |
| `n*`  |  0 or more _n_ |
| `n+`  |   1 or more _n_ |
| `n?`  |  0 or 1 _n_ |
| `n{2}`  |    Exactly 2 _n_ |
| `n{2,}`  |  2 or more _n_ |
| `n{,2}`  |  2 or less _n_ |
| `n{2,4}`   |  2, 3 or 4 _n_ |

### Ranges

| Value | Meaning |
| --- | --- |
| `.` | Any character except new line|
|`(A\|B)` | A or B |
|`(...)` | Group |
| `[ABC]` | Range (A, B or C)|
| `[^ABC]` | Not A, B or C |
|`[A-Z]` | Between A and Z |
| `[0-9]` | Between 0 and 9 |
|`[A-Z0-9]` | Between left-sidebarboth A-Z and 0-9 |
| `\n` | nth group/sub pattern|

### Anchors and Character Classes

| Value | Meaning |
| --- | --- |
| `^` | Start of line |
| `$` | End of line |
| `\w` | Any word (includes underscore) |
| `\W`| Non-word|
| `\d` | Digit |
| `\D` | Non-digit |
| `\s` | Whitespace |
| `\S` | Not whitespace |
| `\b` | Match at the beginning or end |
| `\B` | Do not match at beginning or end |
| `\0` | Nul character |
| `\n` | New line |

## Regex Algebra

Some stuff can be represented in many ways, here are a few.

1. `(a + b) + y = a + (b + y)`
2. `a + b = b + a`
3. `a + o = o + a = a`
4. `a + a = a`
5. `(a . b) . y = a . (b . y)`
6. `a . ε = ε . a = a`
7. `a . (b + y) = (a . b) + (a . y)`
8. `a+ = a . a* = a* . a`
9. `a* = ε + a+`
10. `(a + ε)+ = (a + ε)* = a*`
11. if `X = b + a . X` then `X = a* . b`
12. if `X = b + X . a` then `X = b . a*`

## RE Module

In class we used the `re` module from Python. 
You can find the docs [here](https://docs.python.org/3/library/re.html) but I will put a small explination below.

About Python's regex module, we had to use the following functions.

- 


