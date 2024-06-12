---
title: Recognition Top-Down
---

# Recognition Top-Down

For top-down recursive recognition we must write a procedure for each symbol (non-terminal and terminal).

For the terminal symbols the recognition basis itself on knowing the next symbol if the next symbol of the string is equal to the terminal symbol that we are looking to recognize.

For each none-terminal symbol A with the following productions: `A -> x1 x2 ... xn | ... | y1 y2 ... ym |`\
We must decide which production we go with. To be able to choose the production we must firstly calculate the set of terminal symbols that correspond to possible derivations for each production. We call theses sets production **lookaheads**.

To calculate these lookaheads that are many ways, but it's more important to know that depending on:
- grammar
- the type of each symbol
- the expresiong f and g to calculate de values of non-terminal symbols
The lookahead will differ.

To generate this recognition there are already many tools, such as YACC, LALR, ELL ...

## Lookahead, First and Follow

To calculate the lookahead we need to also know the first and follow.

### First

First is the way to determine the set of terminal symbols which are the valid beginning of the languague associated to a non-terminal symbol, or a sequence of terminal symbols.

### Follow

Follow is a set of terminal symbols that can folow whatever A derives into. The result of Follow(A) depende in which context A is inserted.

### Lookahead

To determine the lookahead we have the set of terminal symbols that can follow a situation in which we can use a production `A -> rhs`. 

## Tables for Top-Down

| Objective | String | Action | Derivation Tree |
| :---: | :---: | :---: | :---: |
| Exp . | ( + 3 4) . | Prod 2 | Exp |
| ( Fun ) . | ( + 3 4) . | Advance | ( Fun ) |
| Fun ) . | + 3 4 ) . | Prod 3 | |
| + Lis ) . | + 3 4 ) . | Advance | + Lis |
| Lis ) . | 3 4 ) . | Prod 5 | |
| Exp Lis ) . | 3 4 ) . | Prod 1 | Exp Lis | 
| int Lis ) . | 3 4 ) . | Advance | int |
| List ) . | 4 ) . | Prod 5 | |
| Exp Lis ) . | 4 ) . | Prod 1 | Exp Lis | 
| int Lis ) . | 4 ) . | Advance | int |
| Lis ) . | ) . | Prod 6 | |
| ) .  | ).  | Advance | empty |
| . | . | Recognizes | |

## LL Conflicts

### LL1 Conflicts

<hr></hr>

##### Next Chapter: [Recognition Bottom-Up](recognition-up.md)