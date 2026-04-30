# Ground Stratified Inductive Definitions in Abella
This repository illustrates the usefulness of ground stratified inductive definitions in a logic of 
definitions via a formalization of strong normalizability for the Simply Typed Lambda Calculus and System T 
in the 
[Abella](https://abella-prover.org/index.html) proof assistant.
More specifically, it complements the paper entitled *Ground Stratified Inductive Definitions* that appears in 
the proceedings of the 2026 edition of the *Formal Structures in Computation and Deduction* (FSCD) conference 
by providing a complete development of the examples sketched out in that paper. 
These proofs have been tested with Abella version 1.0.8. Although this version of Abella is based on 
a logic that doesn't not permit inductive definitions that are ground stratified, it allows them to
be used with a warning in developments. The work in the related paper provides partial justification
for eliding the warning.

The critical idea underlying the proof of strong normalizability is the use of a logical relations style
definition of a reducibility predicate for the terms in the object language. Limiting the language to 
that of STLC, this predicate is defined as follows:

$${\color{blue}\mathrm{red}}\ {\color{purple}{\mathrm{unit}}}\ {\color{purple}{\star}} {\stackrel{\mathclap{{\mu}}}{:=}}\ \top$$
$${\color{blue}\mathrm{red}}\ ({\color{purple}{\mathrm{arr}}}\ A\ B)\ ({\color{purple}{\mathrm{lam}}}\ S) {\stackrel{\mathclap{{\mu}}}{:=}} \forall u.({\color{blue}\mathrm{red}}\ A\ u)\supset({\color{blue}\mathrm{red}}\ B\ (S\ u))$$
$${\color{blue}\mathrm{red}}\ A\ T {\stackrel{\mathclap{{{\mu}}}}{:=}} {\color{blue}\mathrm{neutral}}\ T\wedge\forall u.({\color{blue}\mathrm{step}}\ T\ u)\supset({\color{blue}\mathrm{red}}\ A\ u)$$

Here, $unit$ represents a constant of the sole atomic type $*$ and $step$ is a predicate that encodes
a &beta;-contraction step. This definition is not stratified under an ordering of atomic formulas that 
is based only on their predicate heads, a condition referred to as *strict stratification*. However, 
it is stratified under a weaker notion called *ground stratification*, where the measure associated 
with ground atomic formulas can depend also on their arguments. The interesting aspect of our examples 
is that this definition needs to be interpreted *inductively* and not just as a fixed-point definition.


## Simply Typed Lambda Calculus

The syntax and typing rules for STLC
are respectively specified in [stlc.sig](./STLC/stlc.sig) 
and [stlc.mod](./STLC/stlc.mod).

The file [stlc-simplified.thm](./STLC/stlc-simplified.thm) describes
a proof that the ground-stratified inductive version of reducibility implies 
strong normalizability in the simplified case in which a constant 
is introduced to simulate variables.

The file [stlc.thm](./STLC/stlc.thm) describes a strong normalization
proof for STLC using the ground-stratified inductive version of reducibility.

## System T

The syntax and typing rules for System T are respectively specified in 
[systemT.sig](./systemT/systemT.sig) and [systemT.mod](./systemT/systemT.mod).

The file [systemT-partial.thm](./systemT/systemT-partial.thm) describes
a strong normalization proof for System T using the ground-stratified inductive
version of the reducibility predicate. In this file, we restrict the reduction 
rules for simplicity.

The file [systemT.thm](./systemT/systemT.thm) describes
a strong normalization proof for System T using the ground-stratified inductive 
version of the reducibility predicate. The reduction rules in this file are 
identical to those presented in Girard, Lafont, and Taylor's *Proof and Types*.


## Checking the proofs

The proofs can be checked with Abella 2.0.8. To check a file, 
run the command 
```shell
abella *.thm
```
