---
description: >-
  My notes from reading the book 'Learn Bash the Hard Way' by Ian Miell. This is
  a great hands-on practical book that explains all the main concepts to work
  with bash. Highly recommended.
icon: square-terminal
---

# Bash

## Basic understanding of Command Line

Appendix A: [Command Line Crash Course](https://learnpythonthehardway.org/book/appendixa.html)

**1. Commands - Index cards**

| Linux      |                                                                                     | Windows         |
| ---------- | ----------------------------------------------------------------------------------- | --------------- |
| `pwd`      | print working directory                                                             | `pwd`           |
| `hostname` | my computer's network hostname                                                      | `hostname`      |
| `mkdir`    | make a new directory                                                                | `mkdir`         |
| `cd`       | change directory                                                                    | `cd`            |
| `ls`       | list directory                                                                      | `ls`            |
| `rmdir`    | remove directory                                                                    | `rmdir`         |
| `pushd`    | push directory                                                                      | `pushd`         |
| `popd`     | pop directory                                                                       | `popd`          |
| `cp`       | copy a file or directory                                                            | `cp`            |
| `mv`       | move a file or directory                                                            | `mv`            |
| `rm`       | remove a file                                                                       |                 |
| `less`     | page through a file                                                                 | `more`          |
| `cat`      | print the whole file                                                                | `type`          |
| `xargs`    | execute arguments                                                                   | ---             |
| `find`     | find files                                                                          | `dir -r`        |
| `grep`     | find things inside files                                                            | `select-string` |
| `man`      | read a manual page                                                                  | `help`          |
| `apropos`  | find what man page is appropriate                                                   | `helpctr`       |
| `env`      | <p>look at your environment<br>prints all the environment variables</p>             | ---             |
| `echo`     | prints some arguments                                                               | `echo`          |
| `export`   | export/set an environment variable                                                  | `set`           |
| `exit`     | exit the shell                                                                      | `exit`          |
| `sudo`     | {DANGER} become super user                                                          | `runas`         |
| ---        | run a command on many file                                                          | `forfiles`      |
|            |                                                                                     |                 |
| `ps`       | Show all running static processes                                                   |                 |
| `kill`     | <p>Kills the process with a given id<br><code>kill -9 40458</code> violent kill</p> |                 |
|            |                                                                                     |                 |

**2. Paths, folder, directories**

```sh
$ pwd
/Users/ann # MacOS
/home/ann  # Linux
```

**3. If you get lost**

`pwd` tells you where you are. `cd ~` takes you home.

```sh
$ pwd
$ cd ~
```

**4. Make a directory**

`mkdir` creates a directory. `mkdir -p` creates directories that don't exist in the given path

```sh
$ mkdir temp
$ mkdir temp/apple/pear
mkdir: temp/apple: No such file or directory

$ mkdir -p temp/apple/pear
# success
```

On Linux and macOS, `mkdir` with an existing directory will throw an error. If you have give `mkdir -p`, it stays silent.

```sh
$ mkdir temp

# Linux / MacOS
$ mkdir teamp
mkdir: cannot create directory ‘temp’: File exists
$ mkdir -p temp
$ # no error
```

If you give whitespace between the arguments of `mkdir`, it will create multiple directories. If you want to create a directory with spaces in it, enclose it in " "

```sh
$ mkdir this is fun
# creates 3 directories - this, is, fun

$ mkdir "this is fun"
# created 1 directory this is fun
```

**5. Change directory**

`cd` changes directory. `cd -` takes you the previous directory you were in.

```sh
$ pwd
/Users/ann

$ cd temp/apple/pear
$ pwd
/Users/ann/temp/apple/pear
$ cd ..
# ~/temp/apple
$ cd ~

$ cd temp/something
cd: no such file or directory: temp/something
```

If you give whitespace between arguments of `cd`, it would give error that there are too many arguments. If you want to navigate to a directory with whitespace, use `\` . Or enclose it in " "

```sh
$ mkdir "this is fun"
$ cd "this is fun"
# navigates to the folder

$ cd ..
$ cd this\ is\ fun
```

**6. List directory ls**

`ls` lists the contents of the directory

```sh
$ pwd
/Users/ann/dev/learn-bash/temp

$ ls
apple    carrot

$ ls apple
orange   pear
```

`ls -lR` shows the contents in recursive fashion.

```sh
$pwd
/Users/ann/dev/learn-bash/temp

$ ls -lR
total 0
drwxr-xr-x@ 4 ann  staff  128 Mar 14 21:52 apple
drwxr-xr-x@ 3 ann  staff   96 Mar 14 21:52 carrot

./apple:
total 0
drwxr-xr-x@ 2 ann  staff  64 Mar 14 21:52 orange
drwxr-xr-x@ 2 ann  staff  64 Mar 14 19:08 pear

./apple/orange:
total 0

./apple/pear:
total 0

./carrot:
total 0
drwxr-xr-x@ 2 ann  staff  64 Mar 14 21:52 potato

./carrot/potato:
total 0
```

**7. Remove directory**

`rmdir` deleted empty directory. If the directory is not empty, it throws an error.

```sh
$pwd
/Users/ann/dev/learn-bash/temp
$ ls
apple carrot

$ cd apple
$ rmdir pear
$ ls apple
orange

$cd ..
$ rmdir apple
rmdir: apple: Directory not empty

$ rmdir apple/orange
$ rmdir apple
# no error

$ ls
carrot
```

**8. Moving around - pushd, popd**

`pushd` lets you go to a new location **after saving** your current location. It's like saying _remember where I am, then go here_.`popd` - you can return to your saved location. It's like saying, _the last directory I saved, pop it and take me there._

```sh
➜  apple cd ..
➜  temp ll
total 0
drwxr-xr-x@ 3 ann  staff    96B Mar 14 22:13 apple
drwxr-xr-x@ 3 ann  staff    96B Mar 14 22:08 i

➜  temp$ pushd i/like/icecream
~/dev/learn-bash/temp/i/like/icecream ~/dev/learn-bash/temp ~/dev/learn-bash/temp/apple
➜  icecream$ popd
~/dev/learn-bash/temp ~/dev/learn-bash/temp/apple
➜  temp$ pwd
/Users/ann/dev/learn-bash/temp
➜  temp$ pushd i/like
~/dev/learn-bash/temp/i/like ~/dev/learn-bash/temp ~/dev/learn-bash/temp/apple
➜  like$ pwd
/Users/ann/dev/learn-bash/temp/i/like
➜  like$ pushd icecream
~/dev/learn-bash/temp/i/like/icecream ~/dev/learn-bash/temp/i/like ~/dev/learn-bash/temp ~/dev/learn-bash/temp/apple
➜  icecream$ pwd
/Users/ann/dev/learn-bash/temp/i/like/icecream
➜  icecream$ popd
~/dev/learn-bash/temp/i/like ~/dev/learn-bash/temp ~/dev/learn-bash/temp/apple
➜  like$ pwd
/Users/ann/dev/learn-bash/temp/i/like
➜  like$ popd
~/dev/learn-bash/temp ~/dev/learn-bash/temp/apple
➜  temp$ pwd
/Users/ann/dev/learn-bash/temp

➜  temp$ pushd i/like/icecream
~/dev/learn-bash/temp/i/like/icecream ~/dev/learn-bash/temp ~/dev/learn-bash/temp/apple
➜  icecream$ pushd
~/dev/learn-bash/temp ~/dev/learn-bash/temp/i/like/icecream ~/dev/learn-bash/temp/apple
➜  temp$ pwd
/Users/ann/dev/learn-bash/temp

➜  temp$ popd
~/dev/learn-bash/temp/i/like/icecream ~/dev/learn-bash/temp/apple
➜  icecream$ popd
~/dev/learn-bash/temp/apple
➜  apple$ popd
popd: directory stack empty
➜  apple$
```

If you run `pushd` without any arguments, then it will remember the current directory into the stack. Then you can go anywhere and do `popd`, it will take you to the previous directory.

**9. Make empty files touchd**

`touchd` makes an empty file with the given name.

```sh
$ pwd
~/learn-bash
$ touch me.txt
$ ls
me.txt
```

**10. Copy a file**

```sh
$ cp me.txt you.txt
$ ls
me.txt  you.txt
$ mkdir yours
$ cp you.txt yours/
$ ls
me.txt   yours
```

`cp -r` copies sub-directories with files in them.

```sh
$ ls
foo/
$ cp foo bar
cp: foo is a directory (not copied).
$ cp -r foo bar
$ ls
bar   foo
```

**11. Moving a file (mv)**

`mv` moves a file from location to another. It also renames a file. Works for files or directories:

```sh
$ ls foo
a.txt
$ mv foo/a.txt foo/b.txt
$ls foo
b.txt

$ mv foo foo-2
$ ls
foo-2
```

**12. View a file (less)**

`less` displays the contents of a file page by page\
Use (spacebar) to scroll down and `w` to scroll up. To get out, press `q`.

```bash
$ less myfile.txt
# displays contents of the file
```

**13. Stream a file (cat)**

`cat` just dumps the whole file to the terminal - with no paging or stopping.

```sh
$ cat a.txt
# file a contents

$ cat b.txt
# file b contents

$ cat a.txt b.txt
# file a contents file b contents
```

**14. Removing a file (rm)**

`rm` deletes a file or directory. To remove recursively all the contents of a directory, use `rm -r` or `rm -rf`

* `rm -f`: force deletion of file
* `rm -r foo`: deletes the folder foo
* `rm -i`: asks for confirmation to delete each file
* `rm -r *`: deletes all folders in the current folder
* `rm -r *.*`: deletes only the files directly in the current folder (not the inner folders or files)
* `rm -R` works the same as `rm -r`\
  Be careful when running recursive remove on files `rm -rf`.

```sh
$ test ls
a.txt b.txt
$ test rm a.txt
$ test ls
b.txt

$ cd ..
$ ls
foo bar test
$ rmdir test
rmdir: test: Directory not empty

$ rm -r test
$ ls
foo bar
```

**15. Exiting your terminal**

Use the `exit` command.

## Part 1 - Core Bash

Page 1 - 34

### What is Bash

Bash is a shell program. **Shell program** is an executable binary (file that contains program instructions) that takes the commands that you type and when you hit return translates those commands into system calls to the OS API.\
Other shell programs - sh, csh, tcsh zsh .... You can run other shells from one another, eg: `tcsh` from `bash`

_Bash_ (1987) stands for _Bourne-Again_, the descendant of the Bourne shell (1977). _Zsh_ originates in 1990.

#### History of Bash

!\[\[Pasted image 20250316222032.png|800]]

**Exercises**

1. Run `sh` from a bash command line. What happens? Ans: It shows sh-3.2 and starts the `sh` shell.
2. Which commands does NOT work in `sh` - Examples: `ll`, `la` do not work. But `ls`, `echo`, `mkdir`, `touch` etc. work.

### Globbing and Quoting

#### Globbing

`ls *` - lists the files in the folder matching \* , i.e. all files`echo *` also lists all files in the folder`*` stands for 'all' - it is one of the **globbing** primitives.

#### Quoting

You can enclose `*` in single or double quotes to escape it.

```sh
$ ls '*'
ls: *:No such file or directory

$ echo '*'
*
```

#### Other glob characters

* `?` - matches single character
* `[abd]` - matches any character from a, b or d
* `[a-d]` - matches any character from a, b, c, or d

```sh
$ ls
a     ab    abc   b     bb    cc    dd    file1 file2 file3
$ ls [ab]
a b
$ ls [ab]b
ab bb
$ ls [ab]*
a   ab  abc b   bb

$ ls file[0-9]
file1 file2 file3
$ [a-c]*
a   ab  abc b   bb  cc
```

#### Dotfiles

Their names starts with a dot `.`. They are hidden files and don't show up with `ls`. You must use `la` to see them.

```sh
$ mkdir .hidden
$ touch .hidden/.a.txt

$ ls
# does not show .hidden folder
$ ls .hidden
# empty output

$ la
.hidden
$ la .hidden
.a.txt
```

Single dot folder - `.` is a file that represents the current folder. Double dot folder `..` is a special folder that represents the parent folder.

#### Differences to regular expressions

Globs look like regular expressions, but are used in different contexts.`*` character in the context of regex is used a suffix to `.`, eg: `rename -n '-s/(.*)/new$1/'` renames all files to have the prefix `new`\
since the `*` character is enclosed in quotes, it is NOT interpreted by the shell.

#### Exercises

* [x] Create a folder with files with similar names and use globs to list them
* [x] Find how `grep` works

### Variables

_(2025-03-16 11pm, Faircrest home)_

#### Basic variables

You create a variable by giving it a name, followed by `=` and then the value of the variable. eg: `FOO=bar`. You can see the value of the variable using `echo` and `$` then the variable name.\
Variable names are capitalized by convention, but not required. You can use quotes `"` to group multiple words into the value

```sh
$ FOO=bar
$ echo $FOO
bar

$ MULTI="two words"
$ echo $MULTI
two words
```

#### Quoting variables

You can embed variables in each other. However, if you enclose them in double-quotes `" "`, bash will translate the variable into its value. If you enclose it is single quotes `' '`, it will NOT translate it.

```sh
$ OUTER="this has $FOO in it"
$ echo $OUTER
this has bar in it

$ OUTER_SINGLE='this has $FOO in it'
$ echo $OUTER_SINGLE
this has $FOO in it
```

#### Quoting and globs

This does not happen with globbing - globs (eg: `*`) in variables are not expanded when in single or double quotes.

#### Shell variables

These are shell variables that are set up when bash starts, eg `PPID` is bash's parent process. It is a readonly variable.

```sh
$ echo $PPID
50599

$ PPID=nonsense
zsh: read-only variable: PPID
```

Variables made with the `export` command persist across bash restarts. The new bash session inherits the value set in the previous session.\
Note - this happens only in the bash sessions started by the running shell. So if you open a new terminal and type that variable, it will be empty.

```sh
# regular variable
$ FOO=bar
$ echo FOO
bar
$ bash
$ echo $FOO
# empty

# shell variable
$ export NEW_FOO=bar
$ echo $NEW_FOO
bar
$ bash
$ echo $NEW_FOO
bar # value persists
```

#### env and export commands

If you want to see all the variables exported to processes that you start in the shell, use `env` command.

#### Simple arrays

Bash treats array in a special way. You can access arrays only by its index, that too encloses in . Example - `BASH_VERSINFO` returns an array with 6 elements (0 - 5).

```sh
$ bash --version
GNU bash, version 3.2.57(1)-release (arm64-apple-darwin24)
Copyright (C) 2007 Free Software Foundation, Inc.

bash-3.2$ echo $BASH_VERSINFO
3
bash-3.2$ echo ${BASH_VERSINFO[0]}
3
bash-3.2$ echo ${BASH_VERSINFO[1]}
2
bash-3.2$ echo ${BASH_VERSINFO[2]}
57
bash-3.2$ echo ${BASH_VERSINFO[3]}
1
bash-3.2$ echo ${BASH_VERSINFO[4]}
release
bash-3.2$ echo ${BASH_VERSINFO[5]}
arm64-apple-darwin24
bash-3.2$ echo ${BASH_VERSINFO[6]}
# empty
```

### Functions

You can have functions in bash. There is no type checking, it just works.\
Functions can have 'local' variables that are viewed and accessed from within the function. Variables defined outside can be accessed inside too. `local` can be used only inside a function.

```sh
$ function foo {
> echo Hello world
> }
$ foo
Hello world

$ function foo {
> echo $1
> echo $2
> }
$ echo "Hello Ann"
Hello Ann
$ echo Hello Ann
Hello Ann
```

```sh
$ function bar {
> local loc="hello"
> echo $loc
> }
$ bar
hello

$ local loc="ddd"
bash: local: can only be used in a function
```

Commands can be one of these - _builtins_, _functions_, _programs_ or _aliases_.

#### Builtins

Commands that come out of the box in bash. eg: `builtin pwd`.

* there is a special `type` builtin which tells how a command will be interpreted by the shell. eg: `type ls` returns `ls is hashed (/bin/ls)`, `type cd` => `cd is a shell builtin`
* `source` is also a builtin**Programs** - executable files. You can see where the binary is by typing `which cd` returns `/usr/bin/cd`**Aliases** - alternate names given to commands.

```sh
$ alias cd=something
$ cd
nothing: command not found
$ unalias cd
$ cd
# ok now
```

### Pipes and redirects

#### Basic redirects

Redirect takes the output from the preceding command and sends it to a file you specify. The redirect operator is `>`.

```sh
$ echo "simple content" > a.txt
$ cat a.txt
simple content
```

#### Basic pipes

Pipe takes output of one command and passes it as input to another command. `|` is the pipe operator.

```sh
$ echo "line one
> line two
> line three
> line two again
> line three again" > b.txt

$ cat b.txt | grep two
line two
line two again
```

#### File descriptors

In Unix, everything is a file - when you push/pull data to/from things - whether you write to the terminal or an actual file or network interface. This gives a common interface to send data into - this is a _sink_, an entity that you can _push data into_.\
If you want to write to a terminal, you 'open' the file that corresponds to the terminal and get back a **file descriptor**. It is a number associated with the process that represents that file. You can write to that file descriptor and the OS will send the data to the right place.

Each process gets three file descriptors by default:

* `0` is _standard input_
* `1` is _standard output_ which is linked to the terminal by default. So the output of all commands eg: `cat b.txt` is sent to the terminal and you see it there.
* `2` is _standard error_ which is also linked to the terminal by default. So the output of all commands eg: `cat some.txt` which is an error is sent to the terminal and you see it there.

The pipe operator `|` sends _only the stdout data_ of the left command to the right command. It does _NOT capture data sent to the stderr_.

* So if the left command succeeds, then the data in stdout is passed onto the right command
* if the left command fails, then the data is in stderr, not stdout. So it is NOT passed to the right command. Instead it is just displayed in the default descriptor of stderr, which is the terminal.\
  The same applies to the redirect operator `>`. It send only the stdout data to the file. stderr data is not sent to the file.

If you want a specific output to a specific sink you can use the `n>` syntax where `n` is the file descriptor id.\
Let's understand this by running a command that does not exist, eg: `blah` and throws an error.\
By default, stderr is sent to the terminal, so you see it in the terminal.\
If you redirect it to a file, then nothing will be written in the file (because > does not send stderr data to the file)

```sh
$ blah
bash: blah: command not found

$ blah > err.txt
bash: blah: command not found
$ cat err.txt
# file is empty
```

If you want to send the error to a file, then use `2>` as the redirect option. Remember `2` is the file descriptor for standard error.\
If you want to ignore the error (i.e not show in the terminal), then redirect it to the 'black hole' file `/dev/null`.

```sh
$ blah 2> err.txt
$ cat err.txt
bash: blah: command not found

$ blah 2> /dev/null
# no error displayed here
```

If you use `2>&1` it means stderror data (`2` is stderror) must go to wherever stdout was going at that time (`1` is stdout)\
Note: _the order of the redirect operator matters._

```sh
# by default stdout goes to terminal
$ blah 2>&1 > aa.txt
bash: blah: command not found  # the error is displayed in the terminal because stdout was set to terminal by default.
$ aa.txt
# empty because the error was shown in the terminal

# now let's flip the order of the commands
$ blah > bb.txt > 2>&1   # here, we are first setting the stodout to go to bb.txt, then setting stderr to go where stdout goes (so it goes to bb.txt)
# no error in the terminal because stderr went to where stdout was set (in this case bb.txt)
$ cat bb.txt
bash: blah: command not found
```

#### Standard out vs. standard error

* _pipe_ operator passes standard _output_ of one command as the standard _input_ of the next command
* _redirect_ operator sends file descriptor (could be stdout or stderr as we saw above) to a file.

The following three commands produce the same result.

```sh
# set up the file
$ echo "line one
> line two
> line three
> line two again" > a.txt

$ grep two a.txt
line two
line two again

$ cat a.txt | grep two
line two
line two again

$ grep two < a.txt
line two
line two again
```

Double redirect `>>` appends the text to the end of the file. Single `>` overwrites the file if it exists.

```sh

# use > operator (overwrites the file)
$ echo hello > c.txt
$ cat c.txt
hello
$ echo world > c.txt
$ cat c.txt
world

# use >> operator (appends to the file)
$ echo hello > c.txt
$ echo world >> c.txt
$ cat c.txt
hello
world
```

### Basic bash scripting

**Shell script** is a collection of shell commands that can be run non-interactively.\
Note - in the command below, you must use single quotes `' '` instead of double quotes `" "`, otherwise you get the error "bash: !/bin/bash": event not found"

```sh
$ echo '#!/bin/bash' > my_script
$ echo 'echo I am a script' >> my_script
$ ls
my_script

$ ./my_script
bash: ./my_script: Permission denied
```

The script failed because it is not marked as an executable. To correct this, use `chmod` to give exec permission to the script.

```sh
$ chmod +x my_script
$ ./my_script
I am a script
```

If you run the script as `my_script` without the prefix `./`, it would fail because the current directory is not in the `PATH` variable. (this is where bash looks through to find commands)

```sh
$ my_script
bash: my_script: command not found
$ echo $PATH
/usr/sbin:/usr/bin

$ PATH=${PATH}:.
$ echo $PATH
/usr/sbin:/usr/bin:.

$ my_script
I am a script
```

#### Startup scripts

When bash starts up, it runs a series of files to set up the environment that you see at the terminal. It follows a sequence of paths depending on various conditions

* **normal** vs.\*\* **remote**. **normal** - you start with `bash` command - the default terminal. **remote** - running under `ssh / rsh`
* **login vs. non-login**. login - you started by logging in with username/password/keys/ non-login - you started with no credentials
* **interactive vs. non-interactive**. interactive: you can type things in. non-interactive: running as a script
* Files loaded in **bash**
  * /etc/profile, /ets/bash.bashrc, \~/.bash\_profile, \~/.bash\_login, \~/.bashrc, Environment variable $BASH\_ENV, runs bash, then at the end \~/.bash\_logout
* Files loaded in **zsh**
  * /etc/zshenv, \~/.zshenv, \~/.zprofile, \~/.zshrc, \~/.zlogin, runs bash, then at the end of session \~/.zlogout

If you want to avoid any startup scripts from running, do `env -i bash --noprofile --norc`

* `--noprofile` asks bash not to source system-wide startup files
* `--norc` asks bash not to source the user-specific startup files

#### source builtin

`source` runs the script within the context of the current shell. So, any variables defined in the current shell are available inside the script. If you don't use `source`, then those variables will not be available to the script.

```sh
$ FOO=bar
$ echo 'echo $FOO' > scr.sh
$ chmod +x scr.sh

$ ./scr.sh
$      # empty because the variable FOO is not available inside the script

$ source ./src.sh
bar  # now the variable FOO is available
```

## Part 2 - Scripting Bash

Page 35 - 73

#### Command substitution

It allows you to place the standard output of one commands into the script as you manually wrote it there. Use `$( )` or the backquotes for this.\
Note - if you use single quotes `' '`, it will ignore the meaning of `$` and will print it verbatim. So use double quotes `" "`\
It is better to use the `$( )` because the backtick option requires backticks to be escaped when you want to nest them

```sh
$ hostname
Mac.lan
$ echo 'My hostname is $(hostname)'
My hostname is $(hostname)

# use double-quotes - with $() or ``
$ echo "My hostname is $(hostname)"
My hostname is Mac.lan
$ echo "My hostname is `hostname`"
My hostname is Mac.lan
```

#### Exit codes

A variable that tells you the result of a command (or function or built-in). It is like the HTTP error code.\
You can get the exit code using the command `$?`.

| Exit code | Meaning                                                                                                                                                           |
| --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0         | OK. No Error                                                                                                                                                      |
| 1         | <p>Generic Error (used when there is no specific error code for the command).<br>A <code>grep</code> command that does not see matching text has exit code 1.</p> |
| 126       | Cannot execute due to permission issue                                                                                                                            |
| 127       | Command not found (no file found for the command)                                                                                                                 |
| 128+n     | Process killed with a signal 'n'. Eg: 130 = process killed with Ctrl-C (signal 2)                                                                                 |
| 3 - 125   | not reserved. Available for everyone. Use `exit` builtin followed by the code.                                                                                    |

```sh
$ ls
$ echo $?  # 0

$ fsdsgdg
$ echo $?  # 127 command not found

$ exit 100
$ echo $? #100
```

Special parameters:

* `$?` - exit code of the last executed command
* `$$` - process id of the shell
* `$!` - process id of the job placed in background
* `$0` - the name of the shell\
  All params - https://www.gnu.org/software/bash/manual/html\_node/Special-Parameters.html

```sh
$ echo $$
56103

$ echo $0
-zsh
```

#### Tests

Bash tests are constructs that allow you to do conditional expressions. Enclosed within square brackets with whitespace on either side (very important).\
The test utility evaluates the expression and, if it evaluates to _true_, returns a _zero (true)_ exit status; otherwise it _returns 1 (false)_.

```sh
$ [ 1 = 1 ]
$ echo $?
0

$ [ 1 = 0 ]
$ echo $?
1

# these are invalid uses of [  ]
$ [1=1] # error because there are no whitespaces around [ and ]
bash: [1=1]: command not found

$ [ 1=3 ] # no error, but the result is always 0
0
```

You can compare values with a variable too.

```sh
$ a=20
$ [ $a == 20 ]
$ echo $?
0

$ [ $a == 5 ]
$ echo $?
1
```

**Logical operators**

`!` means `no`. `||` means `or`. `&&` means `and`.

**\[\[ operator**

It tolerates variables that don't exist and treat it as empty string.

```sh
$ [ $nothing = 2 ]
bash: [: =: unary operator expected

$ [[ $nothing = 2 ]]
$ echo $?
1  # exit code 1 (comparison is '' = 2)
```

**Unary operators**

* `-z` returns true only if the argument is an empty string
* `-a` returns true if the argument is a _file or directory_ and it exists
* `-d` returns true if the argument is a _directory_

```sh
$ FOO=bar
$ [ -z "$FOO" ]
$ echo $?
1

$ unset FOO
$ [ -z "$FOO" ]
$ echo $?
0

$ ls
dir		file.txt
$ [ -a file.txt ]   # 0
$ [ -a dir ]   #0
$ [ -a something.txt ] #1

$ [ -d dir ]  #0
$ [ -d file.txt ] #1
```

**if statements**

`if` statements consist of a test (enclosed in `[[` and `]]`), followed by `then` and the commands to run if that conditions evaluates to `true`.\
There can be an optional `elif` that is executed if the condition evaluates to `false`. You end the if block with `fi`

```sh
$ if [[ 10 -gt 2 ]]
> then
>   echo "10 is greater than 2"
> elif [[ 10 -lt 2 ]]
> then
>   echo "10 is less than 2"
> else
>   echo "They are equal"
```

`if` can be followed by any command. It will compare the exit code of the command to true/false

```sh
$ if grep not_there /dev/null
> then
>    echo found not_there
> else
>    echo not_there is missing
> fi
not_there is missing
```

#### Loops

**for loops**

The `for` loops is like the regular c-style loop. You need to use `do` and `done`

```sh
$ for (( i=0; i<3; i++ ))
> do
>    echo $i
> done
$ 0 1 2 
```

You can use the `for in` construct too.

```sh
$ ls
1.txt	2.txt	3.txt

$ for f in $(ls *txt)
> do
>   echo "File $f contains: $(cat $f)"
> done
File 1.txt contains: one
File 2.txt contains: two
File 3.txt contains: three
```

Bash has `while` and `until` too. Use `do` and `done` too.

**case statements**

```sh
$ cat script.sh
#!/bin/bash

echo "user input: $1"
a=$1
case "$a" in
1) echo 'a is 1';;
2) echo 'a is 2';;
*) echo 'a is not 1 or 2';;
esac

$ ./script.sh 23
user input: 23
a is not 1 or 2

$ ./script.sh 1
user input: 1
a is 1

$ ./script.sh 2
user input: 2
a is 2
```

Case statements are often used to process command-line options. The helper builtin `getopts` is very useful here.

#### set command

`set` is a builtin that shows all the variables and functions set in your environment. You can run is `$ set`\
Note - `env` shows the _exported_ variables only.

#### File substitution

We saw command substitution operator `$(....)` which substitutes the output of the process contained in it to the command\
File substitution operator `<()` does the same for file, i.e. it substitutes a file containing the output of the process contained within it

```sh
$ mkdir a b
$ echo a1 > a/1.txt
$ echo b2 > b/2.txt
$ diff <(ls a) <(ls b)
1c1
< 1.txt
---
> 2.txt
```

#### Subshells

It is a shell that inherits variables from the parent shell. It starts when you open a parentheses `(` and the running is delayed until the parentheses is closed with `)`

```sh
$ OUTER=10
$ (
> echo "OUTER value: ${OUTER}"
> echo "in the subshell"
> INNER=20
> )

ABC value: 10
in the subshell

$ echo "INNER value: ${INNER}" 
INNER value:    # value is empty since the variable from the subshell is not available here
$ echo "OUTER value: ${OUTER}"
10
```

When you change folder when inside a subshell, then that folder change applies only within the subshell. This will help you avoid multiple `cd` `cd -` when you are in scripting mode.

```sh
$ ls
abc	xyz

$ pwd
/Users/ann/dev/learn-bash

$ (
> pwd
> cd abc/
> pwd
> )
/Users/ann/dev/learn-bash
/Users/ann/dev/learn-bash/abc

$ pwd
/Users/ann/dev/learn-bash
```

#### Internal field separator (IFS)

This is a variable that specifies the separator character for file names. By default it is (whitespace),  and .

```sh
But it can be modified. This is particularly helpful to prevent the common bug when filenames have spaces in them.
$ touch "file with spaces.txt"
$ set | grep IFS
IFS=$' \t\n'

$ for f in $(ls)
> do
>   echo $f
> done
file
with
spaces.txt

# change the internal file seprator - remove the space character
IFS=$'\t\n'
$ for f in $(ls)
> do
>   echo $f
> done
file with spaces.txt
```
