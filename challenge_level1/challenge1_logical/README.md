# Challenge 1 Logical
## Design Bug

![error](https://github.com/vyomasystems-lab/riscv-ctb-challenge-garv208/assets/84724429/670df964-7051-4ae8-bf1f-047829bf2c82)

On running makefile for challenge one logical,  an error, as shown above, pop-ups, as there is an error with ISA instructions

```
test.S:15855: Error: illegal operands `and s7,ra,z4'
test.S:25584: Error: illegal operands `andi s5,t1,s0'
```

## Design Fix
We can see both are illegal instructions as in first, register z4, which is used, is not defined in RISC V ISA32I set, Thus replacing with temporary register t4.
For the second instruction, addi (add immediate), we need to provide immediate value, but instead, s0 is mentioned, thus resulting in an illegal operation, so changing addi to add. 

```
and s7,ra,t4
and s5,t1,s0
```
![challenge1_1_fix](https://github.com/vyomasystems-lab/riscv-ctb-challenge-garv208/assets/84724429/977923c6-7a4d-418d-b689-eeb50a19e98b)
