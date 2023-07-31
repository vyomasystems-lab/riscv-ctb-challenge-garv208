# Challenge 1 illegal 
## Design Bug

![challenge1_3](https://github.com/vyomasystems-lab/riscv-ctb-challenge-garv208/assets/84724429/95ecada4-0d1b-432f-ba80-ca6c42936fe2)

On running makefile for challenge one illegal, the execution takes time and cannot complete.

```
li TESTNUM, 2
illegal_instruction:
  .word 0              
  j fail

TEST_PASSFAIL

  .align 8
  .global mtvec_handler
mtvec_handler:
  li t1, CAUSE_ILLEGAL_INSTRUCTION
  csrr t0, mcause
  bne t0, t1, fail
  csrr t0, mepc
  mret

```

## Design fix
As in the execution, illegal instruction is present, exemptions occur, and  the exception handler is started execution, the mret result is the program counter to back where the exception occurred, but as it goes back, it reencounters the exception. As a result, an infinite loop is created due to this process. To stop the loop, we can jump to the location after illegal instruction, which will solve the loop problem.

```
li TESTNUM, 2
illegal_instruction:
  .word 0              
  j fail

 test:
TEST_PASSFAIL

  .align 8
  .global mtvec_handler
mtvec_handler:
  li t1, CAUSE_ILLEGAL_INSTRUCTION
  csrr t0, mcause
  bne t0, t1, fail
  csrr t0, mepc
  j test
  mret

```
![challenge1_3_fix](https://github.com/vyomasystems-lab/riscv-ctb-challenge-garv208/assets/84724429/5a46f43b-6584-4804-81e6-e82c6900de33)
