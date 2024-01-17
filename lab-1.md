#Lab 1

## The `cd` Command

**With No Arguments**
```
[user@sahara ~/lecture1]$ pwd
/home/lecture1
[user@sahara ~/lecture1]$ cd
[user@sahara ~]$ pwd
/home
```
Before running the command, my working directory was `/home/lecture1`. 
Running it produced no outputs, but the command changed my working directory to `/home`.
This is becuase when no arguments are given, the `cd` command always changes your working directory to `/home`.
This is not an error.

**With a Path to a Directory as an Argument**
```
[user@sahara ~]$ pwd
/home
[user@sahara ~]$ cd lecture1
[user@sahara ~/lecture1]$ pwd
/home/lecture1
```
Before running the command, my working directory was `/home`.
Like before, running it produced no output.
But, this time it changed my working directory to `/home/lecture1` as specified by the argument `lecture1`.
Note how `lecture1` is a directory within the original working directory. 
This is not an error.

**With a Path to a File as an Argument**
```
[user@sahara ~/lecture1]$ pwd
/home/lecture1
[user@sahara ~/lecture1]$ ls
Hello.class  Hello.java  messages  README
[user@sahara ~/lecture1]$ cd README
bash: cd: README: Not a directory
[user@sahara ~/lecture1]$ pwd
/home/lecture1
```
Before running the command, my working directory was `/home/lecture1`.
`README` is a file within this directory.
Unlike in the last two examples, the command produced an output, `bash: cd: README: Not a directory`.
It also did not change my working directory.
This output indicates an error, and it occured becuase the `cd` command requires a path as argument if an argument is supplied.
After all, its purpose it to change the working directory. Using a file as an argument does not make much sense.

## The `ls` Command

**With No Arguments**
```
[user@sahara ~/lecture1]$ ls
Hello.class  Hello.java  messages  README
```
Before and after running the command, my working directory was `/home/lecture1`.
The command produced the output `Hello.class  Hello.java  messages  README`, the list of files and directories within the current working directory. The list appears to be in alphabetical order.
The exclusion of arguments caused the command to list the files and directories within the working directory rather than a specified one and not list them in a given order.
This is not an error.

**With a Path to a Directory as an Argument**
```
[user@sahara ~/lecture1]$ pwd
/home/lecture1
[user@sahara ~/lecture1]$ ls messages
en-us.txt  es-mx.txt  fr.txt  zh-cn.txt
```
Before and after running the command, my working directory was `/home/lecture1`. 
The command produced the output `en-us.txt  es-mx.txt  fr.txt  zh-cn.txt`, the list of files within the directory `/home/lecture1/messages` specified by the argument `messages`.
Note that `messages` is a directory in the working directory.
Like before, an order was not specified in the arguments, and the list is in alphabetical order.
This is not an error.

**With a Path to a File as an Argument**
```
[user@sahara ~/lecture1/messages]$ pwd
/home/lecture1/messages
[user@sahara ~/lecture1/messages]$ ls en-us.txt
en-us.txt
```
Before and after running the command, my working directory was `/home/lecture1/messages`.
`en-us.txt` is contained in this directory.
The command produced the outpit `en-us.txt`, the name of the file specified by the argument `en-us.txt`.
This is because the `ls` command just prints the name of a file when a file is given as its argument.
This is not an error.

## The `cat` Command

**With No Arguments**
```
[user@sahara ~]$ pwd
/home
[user@sahara ~]$ cat
testing123
testing123
hello there
hello there
```
Before and after running the command, my working directory was `/home`.
No output was produced, and the prompt disappeared.
Entering any text caused it to be repeated back to the terminal.
This is becuase not specifiying any arguments causes the command to read from the terminal rather than a file.
This is not an error.

**With a Path to a Directory as an Argument**
```
[user@sahara ~]$ pwd
/home
[user@sahara ~]$ cat lecture1
cat: lecture1: Is a directory
```
Before and after running the command, my working directory was `/home`.
`lecture1` is a directory in this directory.
The command produced the output `cat: lecture1: Is a directory`.
This output indicates an error, and it occured becuase the `cat` command requires files as arguments (if they are supplied).
This is because the `cat` command reads files, concatenates, and displays them.
Using a directory as an argument does not make much sense in this context.

**With a Path to a File as an Argument**
```
[user@sahara ~/lecture1]$ pwd
/home/lecture1
[user@sahara ~/lecture1]$ cat Hello.java
import java.io.IOException;
import java.nio.charset.StandardCharsets;
import java.nio.file.Files;
import java.nio.file.Path;

public class Hello {
  public static void main(String[] args) throws IOException {
    String content = Files.readString(Path.of(args[0]), StandardCharsets.UTF_8);    
    System.out.println(content);
  }
```
Before and after running the command, my working directory was `/home/lecture1`.
The command printed out the contents of `Hello.java`, a file contained in the working directory and specified by the argument `Hello.java`.
Since just one argument was supplied, the `cat` did not concatenate the contents of two files but just printed out the contents of one.
This is not an error.
