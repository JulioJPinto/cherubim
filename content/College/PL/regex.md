---
title: Regex
---

There's not a lot to know about Regex. 

## Regex Rules

### Quantifiers

| Value | Meaning |
| --- | --- |
| `n*`  |  0 or more _n_ |
| `n+`  |   1 or more _n_ |
| `n?`  |  0 or 1 _n_ |
| `n{2}`  |    Exactly 2 _n_ |
| `n{2,}`  |  2 or more _n_ |
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
|`[A-Z0-9]` | Between both A-Z and 0-9 |
| `\n` | nth group/sub pattern|

### Anchors and Character Classes

| Value | Meaning |
| --- | --- |
| `^` | Start of line |
| `$` | End of line |


