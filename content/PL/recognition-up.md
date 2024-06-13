---
title: Recognition Bottom-Up
---
# Recognition Bottom-Up

This method of recognition basis itself in **conclusions**, basically, the interpretation that was give to the string to be analysed. These conclusions will be a sequence of non-terminal and terminal symbols.

To begin with, we have nothing in sequence. When we analyse a new symbol we add it to the conclusions. To this process we call _transaction_. Sometimes we are able to substitute a set of symbols from the conclusions for a non-terminal symbol that represents the set. To this process we call it a _reduction_.

To sum up, this method basis itself in the following actions:
- Transition -> Accepts the next terminal symbol and adds it to the conclusions
- Reduction -> Substitutes a sufix alpha, belonging to the conclusions, for a non-terminal symbol A (A -> alpha)
- Acceptance -> Next symbol => $ and conclusions => <axiom>
- Error -> It's not possible to reduce or transition

## LR0 Automata 

### LR0 Conflicts

## SLR1 Automata

### SLR1 Conflicts Reduce-Reduce

### SLR1 Conflicts Transition-Reduce

## LALR1 Automata

### LALR1 Conditions

### LALR1 Conflicts Reduce-Reduce

### LALR1 Conflicts Transition-Reduce

<hr></hr>

##### Extras: [Exercises](exercises.md)
