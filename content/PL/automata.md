---
title: Grammars (Part II)
---

# Automata

An automata is a 5 component object where: 

- T is the alphabet
- Q is a set o states
- S is the initial state
- Z is the final state
- δ is the state transition function

## Non-deterministic Automata (AND)

A non-deterministic automata, its an automata in which the state transition function is given a certain state and a symbol of the alphabet. As a result it shall give us a set of states.

### GSR to AND

Let's consider the following GSR:
```
S → I | E
I → A | ’+’ A | ’-’ A
A → d Z | d A
E → ’+’ F | ’-’ F | F
F → d F | d X1
X1 → ’.’ A
Z → ε
```

Analysing it we can determine the following AND:

![AND](and.png)


## Deterministic Automata (AD)

## AND to AD

## Regex to AND

## 