# Debuggable-1

> AAAAAAAAAAAAAAAAAAAAAAAAA

## Files

looking at our files we get

```
Dockerfile
run.py

```
The dockerfile isn't really important just makes linux container with the flag at /app/flag.txt

but in run.py we can see that the instance takes in an base64 encoded ELF file loads into gdb and runs the following commands
```
list /app/flag.txt
q
```

# Approach

By adding custom debug symbols to our program we can get the instance to leak the contents of /app/flag.txt. When compiling a program with -g it embeds thepath of the sourcefile into the binary. If we change the path and file to /app/flag.txt gdb will output the contents of the flag


However, ```list``` in gdb only works on functions, so we just have to make a function /app/flag.txt. This means that when gdb lists the source code for the function it will list contents of flag.txt, since we set that as the source file.
