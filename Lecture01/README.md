# Exercises 1: Course overview + the shell
2. Create a new directory called missing under /tmp.</br>
```
mkdir /tmp/missing
```
NOTE: We do not need to go into a directory to create a file in that directory. Simply use an absolute path.</br>

3. Look up the `touch` program. The `man` program is your friend.</br>
```
man touch
```

4. Use `touch` to create a new file called `semester` in `missing`.</br>
```
cd /tmp/missing
mkdir semester

```
NOTE: Here we could use `mkdir /tmp/missing/semester` but since we need to modify the content of the newly created file, it's easiler to move to the directory.<br>

5. Write the following into that file, one line at a time:</br>
```
#!/bin/sh
curl --head --silent https://missing.csail.mit.edu
```
The first line might be tricky to get working. It’s helpful to know that `#` starts a comment in Bash, and `!` has a special meaning even within double-quoted (`"`) strings. Bash treats single-quoted strings (`'`) differently: they will do the trick in this case. See the Bash _quoting_ manual page for more information.</br>
```
echo '#!/bin/sh' > semester
echo 'curl --head --silent https://missing.csail.mit.edu' >> semester
```
6. Try to execute the file, i.e. type the path to the script (`./semester`) into your shell and press enter. Understand why it doesn’t work by consulting the output of `ls` (hint: look at the permission bits of the file).
```
./semester
zsh: permission denied: ./semester
```
By typing `/tmp % ls -l` we can example the files in `/tmp` and the owner of the file does not have permission to execute it.

7. Run the command by explicitly starting the `sh` interpreter, and giving it the file `semester` as the first argument, i.e. `sh semester`. Why does this work, while `./semester` didn’t?

NOTE: The `sh` utility is a command language interpreter that shall execute commands read from a command line string, the standard input, or a specified file. The application shall ensure that the commands to be executed are expressed in the language described in Shell Command Language .

8. Look up the `chmod` program.
```
man chmod
```

9. Use `chmod` to make it possible to run the command `./semester` rather than having to type `sh semester`. How does your shell know that the file is supposed to be interpreted using `sh`? See this page on the [*shebang*](https://en.wikipedia.org/wiki/Shebang_(Unix)) line for more information.

```
chmod u+x semester
./semester
```
or 
```
chmod 774 semester
./semester
```
There are two main approaches to change the read-write-execute permission using `chmod`, see this [video](https://youtu.be/fWCnQbwFUuo).

10. Use `|` and `>` to write the “last modified” date output by `semester` into a file called `last-modified.txt` in your home directory.
```
date -r ./semester | cat > ~/last-modified.text
```
Note:
- A pipe `|` - lets you “chain” programs such that the output of the left is the input of the program on its right.
- When giving only one argument, `cat` prints the content of the argument file to its output stream.
- `>` rewires the output stream.
- Tilde `~` means the home directory. 