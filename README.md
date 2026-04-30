# Ground Stratified Inductive Definitions in Abella
The proofs in this repository are formalizations in the 
[Abella](https://abella-prover.org/index.html) proof assistant
which show strong normalizability for the Simply Typed 
Lambda Calculus (STLC) and System T.
This development complements the paper *Ground Stratified Inductive Definitions* that appears in the proceedings
of the 2026 edition of the Formal Structures in Computation and Deduction (FSCD) conference.
In particular, this elaborates the formalizations outlined in that paper
which make use of ground stratified inductive definitions to define reducibility.
We remark that Abella 1.0.8, with which these scripts have been tested, does not intrinsically support
ground stratification. Instead, it outputs a warning which asserts that the definition in question
is not stratified in the strict sense as outlined in the paper. However, we assert that the
use of ground stratification in the development corresponds to that in the paper.


The inductive version of the reducibility predicate may be summarized as follows:
$${\color{blue}\mathrm{red}}\ {\color{purple}{\mathrm{unit}}}\ {\color{purple}{\star}} {\stackrel{\mathclap{{\mu}}}{:=}}\ \top$$
$${\color{blue}\mathrm{red}}\ ({\color{purple}{\mathrm{arr}}}\ A\ B)\ ({\color{purple}{\mathrm{lam}}}\ S) {\stackrel{\mathclap{{\mu}}}{:=}} \forall u.({\color{blue}\mathrm{red}}\ A\ u)\supset({\color{blue}\mathrm{red}}\ B\ (S\ u))$$
$${\color{blue}\mathrm{red}}\ A\ T {\stackrel{\mathclap{{{\mu}}}}{:=}} {\color{blue}\mathrm{neutral}}\ T\wedge\forall u.({\color{blue}\mathrm{step}}\ T\ u)\supset({\color{blue}\mathrm{red}}\ A\ u)$$


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
