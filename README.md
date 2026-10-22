# NFA ⇄ DFA Converter

A single-file web tool for the Compiler Design course. Enter an automaton as a transition table and the tool converts it between an NFA and a DFA, working out the **subset construction** row by row. ε-moves are handled.

**Authors:** Parth Kanade and Pranabh Agrawal

## Features

- **NFA → DFA** using the subset construction, with ε-closure
- **DFA → NFA** by rewriting the transition function with sets
- Plain-text input, so states and the alphabet are read from the transition lines
- Step-by-step subset construction table showing which NFA states each DFA state stands for
- State diagrams for the input machine and the result, with a start arrow and double rings for accepting states
- Formal definition of the resulting DFA (Q′, Σ, q0′, F′)
- String tester that runs the input on the NFA and the DFA together and shows the set of states after each symbol
- Built-in examples, an option to show the dead state ∅, and line-by-line input error messages

## How to run

No installation is needed. Download `index.html` and open it in any web browser.

An internet connection is only used to load fonts. Without it the tool still works with fallback fonts.

## Input format

Enter one transition per line:

```
q0, a -> q0, q1
q0, b -> q0
q1, b -> q2
q2, b -> q3
```

- Write ε as `eps`
- Give the start state and the accepting states in their own boxes
- Start a line with `#` to comment it out

This example is the NFA for `(a|b)*abb`. Converting it gives a 4-state DFA, and the string `ababb` is accepted.

## How it works

1. **ε-closure(S):** all NFA states reachable from S using only ε-moves.
2. **move(S, a):** all NFA states reachable from S by reading symbol `a`.
3. **Subset construction:** start from ε-closure of the start state. For each new set and each symbol, compute ε-closure(move(S, a)). Each distinct set becomes a DFA state, and the process repeats until no new sets appear.
4. A DFA state is accepting if its set contains any NFA accepting state.

In the worst case an NFA with n states can give a DFA with 2ⁿ states.

## Related project

Regex → NFA → DFA is a companion tool that starts from a regular expression, builds the NFA with Thompson's construction, and then does this conversion.
