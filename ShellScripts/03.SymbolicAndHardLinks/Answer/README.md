### Answer for Exercise 03: Symbolic Links and Hard Links

<br>

#### 1. 목표(Objectives)

`ls -l` 명령으로 현재 디렉토리를 확인했을 때, 다음과 같은 출력이 되도록 파일 또는 디렉토리를 만듭니다.<br>
Create files or directories so that the following output is displayed when you check the current directory using the `ls -l` command.

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

---
#### 2. 예시의 속성 확인 (Check the attributes of the given example)

`ls -l` 명령으로 현재 디렉토리를 확인한 결과를 보았을 때, 디렉토리는 excercise03_00 이고, 나머지는 모두 파일입니다.<br>
When you check the current directory using the `ls -l` command, you will see that the directory is excercise03_00, and the rest are all files.

따라서 excercise03_00 디렉토리는 `mkdir` 명령으로 생성하고, 나머지 파일은 `touch` 명령으로 생성합니다.<br>
Therefore, create the excercise03_00 directory using the `mkdir` command, and create the remaining files using the `touch` command.

하지만 excercise03_01, excercise03_03 파일을 보았을 때 설정된 권한이 동일하며 파일의 사이즈, 타임스탬프 등도 동일하다는 것을 발견할 수 있습니다.<br>
However, when you look at the excercise03_01 and excercise03_03 files, you will notice that the permissions set are the same, and the file size, timestamp, etc. are the same.

결정적으로, 사용자 앞의 숫자 2는 파일의 링크 수를 의미합니다.<br>
Finally, the number 2 in front of the user represents the number of links to the file.<br>

따라서 excercise03_01, excercise03_03 파일은 하나의 `i-node`를 공유하고 있는 하드 링크라 가정할 수 있습니다.<br>
Therefore, you can assume that the excercise03_01 and excercise03_03 files are hard links that share one `i-node`.

> 참고: `i-node`와 관련된 정보는 [이 페이지](https://github.com/garlicvread/Shell_Scripting/tree/main/ShellScripts/03.SymbolicAndHardLinks)를 참고하세요.<br>
> NOTE: For more information on `i-node`, see [this page](https://github.com/garlicvread/Shell_Scripting/tree/main/ShellScripts/03.SymbolicAndHardLinks).<br>

<br>

한편, excercise03_02, excercise03_04 파일 뒤에는 `->` 기호가 붙어있습니다.<br>
On the other hand, there is a `->` symbol behind the excercise03_02 and excercise03_04 files.

이는 excercise03_02, excercise03_04 파일이 심볼릭 링크임을 의미합니다.<br>
This means that the excercise03_02 and excercise03_04 files are symbolic links.<br>

`->` 기호 뒤에는 심볼릭 링크가 가리키는 파일 또는 디렉토리의 경로가 위치합니다.<br>
After the `->` symbol, the path to the file or directory that the symbolic link points to is located.<br>

이 경우, excercise03_02는 excercise03_00 디렉토리를 가리키고 있고, excercise03_04는 excercise03_03 파일을 가리키고 있습니다.<br>
In this case, excercise03_02 is pointing to the excercise03_00 directory, and excercise03_04 is pointing to the excercise03_03 file.<br>

<br>

---
#### 3. 링크 생성(Create links)

지금까지 알아낸 정보를 바탕으로 디렉토리와 파일을 생성해 봅시다.<br>
Now that you have learned the information, let's create the directory and files.<br>

```
$ mkdir excercise03_00
$ touch excercise03_01
$ ln excercise03_01 excercise03_03
$ ln -s excercise03_00 excercise03_02
$ ln -s excercise03_03 excercise03_04
```
<br>

`ln` 명령은 링크를 생성하는 명령입니다.<br>
The `ln` command is a command that creates a link.<br>

`ln` 명령의 기본값은 하드 링크 생성입니다.<br>
The default value of the `ln` command is to create a hard link.<br>

위 예제 코드에서는 excercise03_01, excercise03_03 파일을 하드 링크로 생성했습니다.<br>
In the above example code, we created the excercise03_01 and excercise03_03 files as hard links.<br>

```
$ ln excercise03_01 excercise03_03
```
<br>

`ln` 명령에 `-s` 옵션을 추가하면 심볼릭 링크를 생성할 수 있습니다.<br>
You can create a symbolic link by adding the `-s` option to the `ln` command.<br>

위 예제 코드에서는 excercise03_02, excercise03_04 파일을 심볼릭 링크로 생성했습니다.<br>
In the above example code, we created the excercise03_02 and excercise03_04 files as symbolic links.<br>

```
$ ln -s excercise03_00 excercise03_02
$ ln -s excercise03_03 excercise03_04
```
<br>

---

#### 4. 기타(Others)

* 파일 및 디렉토리의 권한 변경 및 속성 변경은 [Excercise02](https://github.com/garlicvread/Shell_Scripting/tree/main/ShellScripts/02.FileAttributesModification/Answer)에서 다루었습니다.<br>
  File and directory permission and attribute changes were covered in [Excercise02](https://github.com/garlicvread/Shell_Scripting/tree/main/ShellScripts/02.FileAttributesModification/Answer).<br>

<br>

---
### [뒤로(Back)](https://github.com/garlicvread/Shell_Scripting/tree/main/ShellScripts/03.SymbolicAndHardLinks/File)