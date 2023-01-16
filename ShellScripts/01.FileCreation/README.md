# 01. File Creation

## Basic Information

| Exercise 01              |
|--------------------------|
| Files to create : a      |
| Allowed functions : None |
| Notes : n/a              |

<br>

---
### TO-DO

<br>

여기서는 기본적인 파일의 생성 방법에 대해 알아봅니다.<br>
Here, you will learn basic how-to-dos to create a file.<br>

명령어를 어떻게 사용해야 하는지는 인터넷 검색도 유용하지만, 기본적으로 내장되어 있는 매뉴얼이 더 도움이 되는 경우도 있습니다.<br>
Searching the Internet for how to utilize the command is a good choice for sure, but in some cases, the built-in manual is more helpful.<br>

많은 경우, 명령어의 매뉴얼은 다음과 같이 `man` 명령어로 볼 수 있습니다.<br>
Usually, the manual of a command can be viewed using the `man` command as follows.<br><br>

> 예시(Example):
```
$ man ls
```
<br>

위와 같이 `man` `ls` 를 터미널에 입력하면 리스트 명령어의 매뉴얼을 보여달라는 뜻입니다.<br>
As above, if you enter `man` `ls` in the terminal, it means you ordered your computer to show the manual of the list command.<br>

리턴 키를 눌러 명령을 실행하면 다음과 같은 화면이 출력됩니다.<br>
If you execute the command by hitting the return key, the following screen will be displayed.<br>

공간에 제약이 있어 다 보여드리지는 않고, 윗 부분만 일부 발췌하여 보여드립니다.<br>
Due to space constraints, I won't show everything but will show some excerpts from the top.<br>

```
NAME
     ls – list directory contents

SYNOPSIS
     ls [-@ABCFGHILOPRSTUWabcdefghiklmnopqrstuvwxy1%,] [--color=when]
        [-D format] [file ...]

DESCRIPTION
     For each operand that names a file of a type other than directory, ls
     displays its name as well as any requested, associated information.  For
     each operand that names a file of type directory, ls displays the names
     of files contained within that directory, as well as any requested,
     associated information.

     If no operands are given, the contents of the current directory are
     displayed.  If more than one operand is given, non-directory operands are
     ...
```
<br>

---
* [여기](https://github.com/garlicvread/Shell_Scripting/tree/main/ShellScripts/01.FileCreation/Files)에서 `파일 만들기 연습`의 내용을 확인할 수 있습니다.<br>
  You can find the contents of `Exercise 01 : A - Basic File Creation` [here](https://github.com/garlicvread/Shell_Scripting/tree/main/ShellScripts/01.FileCreation/Files).