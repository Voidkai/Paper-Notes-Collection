# Zero knowledge technique used in static analysis

| Title                                  | Year | Author                                                   | Conference | Paper Link                                                 | Code Link | Notes |
| -------------------------------------- | ---- | -------------------------------------------------------- | ---------- | ---------------------------------------------------------- | --------- | ----- |
| Zero Knowledge Static Program Analysis | 2021 | Zhiyong Fang, David Darais, Joseph P. Near, Yupeng Zhang | CCS        | [Link](https://dl.acm.org/doi/abs/10.1145/3460120.3484795) |           |       |

## Summary
 This paper introduces the concept of **zero-knowledge static analysis(ZK-SA)**. This is a method where a prover constructs a zero-knowledge proof about the outcome of the static analysis without revealing the program's source code.

The authors present novel zero-knowledge proof schemes(ZKAI) for **intra- and inter-procedural abstract interpretation(AI)**. Their schemes are significantly more efficient than the naive translation of the corresponding static analysis algorithms using existing schemes.

## Workflow of ZK-SA

the imperative PL in this paper is:
> stmt ::= x=a
    | if x then stmt else stmt end
    | while x do stmt end
a ::= x | n | $op_1$ x |  $x_1$ $op_2$ $x_2$
$op_1$ ::= not
$op_2$ ::= +|-|*|/| and | or|

the workflow of zk- abstract interpretion is:
1. Commit a program.
2. Analysis and Prove properties of the program.
3. Proof generation.

### Commitment of program
The owner of the program commits to the program by computing a commitment of the program. The commitment is a hash of the program. The commitment is sent to public, which is public verifiable.

In order to commit a program, how to represent a pragram in arithmetic method is a important question. In ZKAI, the arithmetic representation of a program is a table structure.

| Stmt                         | Stmt Code | Line No. | a   | Line No.(else) | Line No.(end) | variable ID (x) |
| ---------------------------- | --------- | -------- | --- | -------------- | ------------- | --------------- |
| x=a                          | 1         |          |     | /              | /             |                 |
| if x then stmt else stmt end | 2         |          | /   |                |               |                 |
| while x do stmt end          | 3         |          | /   | /              |               |                 |

For each type of statment
1. A unique 'Stmt code' is assigned.
2. 'Line No' stores the line number of the statement in this program, for loop and if-else statement, the line number is the line number of the first statement. else and end also have Line No for upper-bounded the number of outgoing edges in CFG construction.
3. variable ID is the ID of the variable in the program.

Expression table is similar to statement table.
| Expression a       | Expression Code | Variable ID($x_1$) | Variable ID($x_2$) | Value | Op Code |
| ------------------ | --------------- | ------------------ | ------------------ | ----- | ------- |
| x                  | 1               |                    | /                  | /     | /       |
| n                  | 2               | /                  | /                  |       | /       |
| $op_1$ x           | 3               |                    | /                  | /     |         |
| $x_1$ $op_2$ $x_2$ | 4               |                    |                    | /     |         |


### Analysis the source code

worklist algorthim is the analysis state transfer algorithm used in this paper. The algorithm is as follows:


### Proving Intra-procedure Analysis

This paper divides proof of intra-procedure analysis into several parts:
- **Control flow graph consistnecy** (By using characteristic function to check the equality of two set (CFG set and source code table presentation's set))
- **Correct execution of the iteration**(the interation is in the worklist algorithm for traversal CFG to get the stable state of variable in source code)
- **Memory consistency check**
- **Lattice operation and transfer functions**