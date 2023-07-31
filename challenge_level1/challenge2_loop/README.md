# Challenge 1 loop
## Design Bug

![challenge1_2](https://github.com/vyomasystems-lab/riscv-ctb-challenge-garv208/assets/84724429/e7dcebc9-c238-45e8-9794-cee187a86818)
On running makefile for challenge one loop, the execution takes time and cannot complete.

```
Loop:
  lw t1, (t0)
  lw t2, 4(t0)
  lw t3, 8(t0)
  add t4, t1, t2
  addi t0, t0, 12
  beq t3, t4, loop        # check if sum is correct
  j fail

```

## Design Fix
The problem is in the loop as shown above, the loop should run three times, but it keeps on running as there are no instructions for exiting the loop. By using the t5 register, which is loaded with value 3; the programme can be modified to exit loop after three-time
```
loop:
  addi t5, t5, -1 # subtracting one from t5 
	lw t1, (t0)
  lw t2, 4(t0)
  lw t3, 8(t0)
  add t4, t1, t2
  addi t0, t0, 12
  beq t5, zero, test_end  #jumping out of loop after t5 become 0.
  beq t3, t4, loop        # check if sum is correct
  j fail

```

![challenge1_2_fix](https://github.com/vyomasystems-lab/riscv-ctb-challenge-garv208/assets/84724429/53031057-8c16-4d67-9cbd-448add26ed08)
