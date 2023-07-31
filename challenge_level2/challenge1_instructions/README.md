# Challenge 2 Instructions
## Design Bug

![challenge2_1](https://github.com/vyomasystems-lab/riscv-ctb-challenge-garv208/assets/84724429/4c1e2bd2-6442-40e1-bcba-b0bbf4051050)

On running makefile for challenge Two Instruction,  an error, as shown above, pop-ups, as there is an error with ISA instructions that are being executed

```
  rel_rv32m: 0
  rel_rv64m: 10
  rel_rv32a: 0
```

## Design Fix
In rvi.yaml file for AAPG testing, The isa-instruction distribution , which determine what kind of intruction will be executed in the proportion by the relative number, but in this rel_rv64m: 10 is set as 10 , that means it will also 
execute intruction from risc v ISA64M , but since the core that is under test support only ISA32, as a result it through error of unrecongized opcode bu changing rel_rv64m value to 0 from 10 , the problem is fixed.

```
  rel_rv32m: 0
  rel_rv64m: 0
  rel_rv32a: 0
```
![challenge2_1_fix](https://github.com/vyomasystems-lab/riscv-ctb-challenge-garv208/assets/84724429/4b2cf39e-1e2b-466e-bca1-1b86b20a6d1a)
