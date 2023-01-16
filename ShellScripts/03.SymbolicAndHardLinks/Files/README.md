# Exercise 03: Symbolic Links and Hard Links

---

## Basic Information

| Exercise 03                    |
|--------------------------------|
| Files to create : links.tar			 |
| Allowed functions : None				   |
| Notes : n/a							             |

<br>

---

### TODO

* `ls -l` 명령으로 현재 디렉토리를 확인했을 때, 다음과 같은 출력이 되도록 파일 또는 디렉토리를 만드시오.<br>
    Create files or directories so that the following output is displayed when you check the current directory using the `ls -l` command.<br>

> 예시 (Example)
```
$ ls -l
total 16
drwxr-xr-x  2 raymond  staff   64 Jan  1 12:34 excercise03_00
-rw-r--r--  2 raymond  staff  120 Mar  3  2023 excercise03_01
lrwxr-xr-x  1 raymond  staff   14 Jan 15 21:17 excercise03_02 -> excercise03_00
-rw-r--r--  2 raymond  staff  120 Mar  3  2023 excercise03_03
lrwxrwxrwx  1 raymond  staff   14 Jan 15 21:13 excercise03_04 -> excercise03_03
```
<br>

* 위와 같이 파일 또는 디렉토리를 생성했다면, `tar` 명령으로 `links.tar` 파일을 생성하시오.<br>
  If you have created files or directories as above, create the `links.tar` file using the `tar` command.<br><br>

* 이 때, 파일 및 디렉토리의 권한을 유지하시오.<br>
  Preserve the permissions of the files and directories when `tar` the targets.

<br>

---
* [여기](https://github.com/garlicvread/Shell_Scripting/tree/main/ShellScripts/03.SymbolicAndHardLinks/Answer)에서 해설을 확인할 수 있습니다.<br>
  You can read the explanation [here](https://github.com/garlicvread/Shell_Scripting/tree/main/ShellScripts/03.SymbolicAndHardLinks/Answer).<br><br>

* [여기](https://github.com/garlicvread/Shell_Scripting/tree/main/ShellScripts/03.SymbolicAndHardLinks)에서 이 연습에 필요한 기본 정보를 확인할 수 있습니다.<br>
  You can read the basic information related this excercise [here](https://github.com/garlicvread/Shell_Scripting/tree/main/ShellScripts/03.SymbolicAndHardLinks).