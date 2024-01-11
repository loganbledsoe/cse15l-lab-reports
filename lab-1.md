# The `cd` Command

## With No Arguments
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

## With a Path to a Directory as an Argument
```
[user@sahara ~]$ pwd
/home
[user@sahara ~]$ cd lecture1
[user@sahara ~/lecture1]$ pwd
/home/lecture1
```
Before running the command, my working directory was `/home`.
Like before, running it produced no output.
But, this time it changed my working directory to the directory argument I specified, `/home/lecture1`.
This is not an error.

## With a Path to a File as an Argument
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
Unlike in the last two examples, the command produced an output, `bash: cd: README: Not a directory`.
It also did not change my working directory.
This output indicates an error, and it occured becuase the `cd` command requires a path as argument if an argument is supplied.
After all, its purpose it to change the working directory. Using a file as an argument does not make much sense.

# The `ls` command

## With no arguments
```
[user@sahara ~/lecture1]$ ls
Hello.class  Hello.java  messages  README
```
Before and after running the command, my working directory was `/home/lecture1`.
The command produced the output `Hello.class  Hello.java  messages  README`, the list of files and directories within the current working directory. The list appears to be in alphabetical order.
The exclusion of arguments caused the command to list the files and directories within the working directory rather than a specified one and not list them in a given order.
This is not an error.

## With a Path to a Directory as an Argument
```
[user@sahara ~/lecture1]$ pwd
/home/lecture1
[user@sahara ~/lecture1]$ ls messages
en-us.txt  es-mx.txt  fr.txt  zh-cn.txt
```
Before and after running the command, my working directory was `/home/lecture1`. 
The command produced the output `en-us.txt  es-mx.txt  fr.txt  zh-cn.txt`, the list of files within the directory `/home/lecture1/messages` specified by the argument `messages`.
Like before, an order was not specified in the arguments, and the list is in alphabetical order.
This is not an error.

## With a Path to a File as an Argument
```
[user@sahara ~/lecture1/messages]$ pwd
/home/lecture1/messages
[user@sahara ~/lecture1/messages]$ ls en-us.txt
en-us.txt
```
Before and after running the command, my working directory was `/home/lecture1/messages`.
The command produced the outpit `en-us.txt`, the name of the file specified by the argument `en-us.txt`.
This is because the `ls` command just prints the name of a file when a file is given as its argument.
This is not an error.
