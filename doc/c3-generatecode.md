# :r4 Compiler

## Generate code for x86

There are a basic code generator, very simple. Every basic word can be translate to assembly and simple concatenate this instruction the code is ready.
This generator is in:

```
compiler/r4-asmcode86-0.txt
```

The compiler generate code for add to a simple framework, this create a graphic windows andd keep track about event in the windows OS, the keyboard, the mouse and some inteface to API calls.

The data stack is simulated, EAX is the value of top os stack, the stack is in memory in DATASTK definition, EBP point to next to data stack.

The return stack is the normal ESP return stack.

ESI and EDI are the A and B registers.

The compile generate two files, code.asm and data.asm and put in the r4asm/ folder, here the framework called r4asm.asm include this files for make an executable.

The assembly is done with the FASM compiler [FlatAssembler](https://flatassembler.net/)













