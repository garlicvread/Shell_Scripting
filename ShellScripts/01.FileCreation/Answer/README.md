### Answer for Exercise 01: Basic File Creation

터미널에서 직접 파일을 만들려면 `touch` 명령어를 사용합니다.<br>
To create a file directly in the terminal, use the `touch` command.

먼저 터미널을 실행한 뒤, `mkdir`명령, 즉 make directory 명령으로 `ex01` 이라는디렉토리를 먼저 만들고, `cd` 명령으로 `ex01` 디렉토리로 이동합니다.<br>
First, run the terminal, then use the `mkdir` command, that is, the make directory command to create a directory called `ex01` first, and use the `cd` command to move to the `ex01` directory.

```bash
$ mkdir ex01
$ cd ex01
```
<br>

현재 디렉토리에 어떤 파일 또는 디렉토리가 있는지 `ls` 명령어로 확인합니다.<br>
Check what files or directories are in the current directory using the `ls` command.

```bash
$ ls
```
<br>

터미널 창에 아무 결과물이 출력되지 않으면 현재 디렉토리에 아무 파일이 없다는 것을 의미합니다.<br>
If nothing is displayed in the terminal window, it means that there are no files in the current directory.<br>

이제 `touch` 명령어를 사용하여 `a`라는 파일을 만들어 봅시다.<br>
Now, let's use the `touch` command to create a file called `a`.<br>

```bash
$ touch a
```
<br>

`cat` 명령어를 사용하여 `a`라는 파일의 내용을 확인합니다.<br>
Use the `cat` command to check the contents of the `a` file.<br>

먼저 `cat` 명령어의 매뉴얼을 확인해 봅시다.<br>
First, let's check out the manual for the `cat` command.<br>

```
man cat
```
<br>

`cat` 명령어의 매뉴얼을 열어 보면 다음과 같은 내용을 읽을 수 있습니다.<br>

```
CAT(1)                                              General Commands Manual                                              CAT(1)

NAME
     cat – concatenate and print files

SYNOPSIS
     cat [-belnstuv] [file ...]

DESCRIPTION
     The cat utility reads files sequentially, writing them to the standard output.  The file operands are processed in
     command-line order.  If file is a single dash (‘-’) or absent, cat reads from the standard input.  If file is a UNIX
     domain socket, cat connects to it and then reads it until EOF.  This complements the UNIX domain binding capability
     available in inetd(8).

     The options are as follows:

     -b      Number the non-blank output lines, starting at 1.

     -e      Display non-printing characters (see the -v option), and display a dollar sign (‘$’) at the end of each line.
     ...
```
<br>

`cat` 명령의 매뉴얼을 열면 이 명령이 *"파일을 연결하고 표준 출력으로 인쇄"* 하기 위한 것임을 알 수 있습니다.<br>
When you open the manual of the `cat` command, you can find that this command *"concatenate files and print on the standard output"*.<br>

즉, `cat` 명령은 대상 파일(이 경우 **a**)에 담겨 있는 모든 내용을 화면에 나타내 줍니다.<br>
In other words, the `cat` command will print whatever you put inside the target file, which is **a** in this case.<br>

문자 A를 반환하려면 간단히 **a** 파일에 문자 **A**를 넣고, 저장하면 됩니다.<br>
To return the letter A, simply type the letter **A** into the **a** file and save it.<br>

이제 파일의 크기를 확인해 봅시다.<br>
Now, let's check the size of the file you've created.

파일의 크기를 보려면 `ls -l` 명령을 실행해 보세요.<br>
Try running the `ls -l` command to see the size of the file.<br>

`-l` 의 의미는 **long** 이며, 이 옵션은 파일의 상세한 정보를 보고 싶을 때 사용합니다.<br>
The meaning of `-l` is **long**, and this option is used when you want to see detailed information about the file.<br>

그러면 다음과 같은 화면이 보일 거에요.<br>
Then you can see your screen something similar with the following.<br>

```
$ ls -l
total 8
-rw-r--r--  1 raymond  staff    0 Jan 15 09:30 a
```
<br>

그럼 문자 **A**를 파일 **a** 에 저장해 봅시다.<br>
So let's save the character **A** to the file **a**.<br>

다시 `ls -l` 명령으로 파일의 크기를 확인해 보면, 글자 **A** 하나, 즉 1 바이트 크기의 데이터를 넣었을 뿐인데 파일의 크기가 2 바이트가 된 것을 볼 수 있습니다.<br>
If you check the size of the file with the `ls -l` command once again, you will see that the size of the file has become 2 bytes even though you have only inserted one letter **A**, that is, 1 byte of data.<br>

```
total 16
-rw-r--r--  1 raymond  staff    2 Jan 15 09:40 a
```
<br>

이는 파일에 정보가 입력되면 운영체제(OS)에서 그 파일의 가장 마지막에 개행 문자(줄바꿈 문자)를 하나 자동으로 추가하기 때문입니다.<br>
This is because when information is entered into a file, the OS(Operating System) automatically adds a new line character to the end of the file.<br>

개행 문자가 들어가 있는지 여부는 `cat -e` 명령으로 확인할 수 있습니다.<br>
You can check whether a newline character is included with the `cat -e` command.<br>

```
$ cat -e a
A$
```
<br>

그러면 글자 **A** 뒤에 개행 문자 **$** 가 자동으로 추가된 것을 볼 수 있습니다.<br>
Then you will see that a newline character **$** is automatically added after the letter **A**.<br>

> 참고: 개행 문자 **$** 는 터미널 종류와 운영체제(OS)에 따라 다를 수 있습니다.<br>
> NOTE: The newline character **$** may differ depending on the type of terminal and OS(Operating System).<br>
---
### [뒤로(Back)](https://github.com/garlicvread/Shell_Scripting/tree/main/ShellScripts/01.FileCreation/File)