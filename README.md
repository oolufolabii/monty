# The Monty language

Monty 0.98 is a scripting language that is first compiled into Monty byte codes (Just like Python). It relies on a unique stack, with specific instructions to manipulate it. The goal of this project is to create an interpreter for Monty ByteCodes files.

```
julien@ubuntu:~/monty$ cat -e bytecodes/000.m
push 0$
push 1$
push 2$
push 3$
				pall    $
push 4$
	push 5    $
	push    6        $
pall$
julien@ubuntu:~/monty$
```

Monty byte code files can contain blank lines (empty or made of spaces only, and any additional text after the opcode or its required argument is not taken into account:

```
julien@ubuntu:~/monty$ cat -e bytecodes/001.m
push 0 Push 0 onto the stack$
push 1 Push 1 onto the stack$
$
push 2$
  push 3$
                   pall    $
$
$
                           $
push 4$
$
    push 5    $
      push    6        $
$
pall This is the end of our program. Monty is awesome!$
julien@ubuntu:~/monty$
```

### The monty program

---

- Usage: monty file

  - where file is the path to the file containing Monty byte code

- If the user does not give any file or more than one argument to your program, print the error message USAGE: monty file, followed by a new line, and exit with the status EXIT_FAILURE

- If, for any reason, it’s not possible to open the file, print the error message Error: Can't open file <file>, followed by a new line, and exit with the status EXIT_FAILURE
  
  - where <file> is the name of the file

- If the file contains an invalid instruction, print the error message L<line_number>: unknown instruction <opcode>, followed by a new line, and exit with the status EXIT_FAILURE
  
  - where is the line number where the instruction appears.
  
  - Line numbers always start at 1

- The monty program runs the bytecodes line by line and stop if either:
  
  - it executed properly every line of the file
  - it finds an error in the file
  - an error occured

- If you can’t malloc anymore, print the error message Error: malloc failed, followed by a new line, and exit with status EXIT_FAILURE.

- You have to use malloc and free and are not allowed to use any other function from man malloc (realloc, calloc, …)

## Supported Opcodes

| Name | Description |
|:--:|:--|
| push | Pushes an element to the stack. Usage: `push integer` |
| pall | Prints all the values on the stack, starting from the top of the stack |
| pint | Prints the value at the top of the stack, followed by a new line |
| pop | Removes the top element of the stack |
| swap | Swaps the top two elements of the stack |
| add | Adds the top two elements of the stack |
| nop | Does nothing |
| sub | Subtracts the top element of the stack from the second top element of the stack |
| div | Divides the second top element of the stack by the top element of the stack |
| mul | Multiplies the second top element of the stack with the top element of the stack |
| mod | Computes the rest of the division of the second top element of the stack by the top element of the stack |
| pchar | Prints the char at the top of the stack, followed by a new line |
| pstr | Prints the string starting at the top of the stack, followed by a new line |
| rotl | Rotates the stack to the top |
| rotr | Rotates the stack to the bottom |
| stack | Sets the format of the data to a stack (LIFO). This is the default behavior of the program |
| queue| Sets the format of the data to a queue (FIFO) |
