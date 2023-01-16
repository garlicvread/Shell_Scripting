### Answer for Exercise 02: Basic File Attributes Modification

<br>

#### 1. 목표(Objectives)

`ls -l` 명령어로 확인했을 때 다음과 같은 결과를 얻을 수 있도록 파일의 속성을 변경합니다.<br>
Modify the file attributes so that the result of the command `ls -l` is as follows.

```
$ ls -l
total 1
-r--r-xr-x 1 login wheel 40 Jan 1 12:34 createdFile
$
```
<br>

---
#### 2. 파일 속성 변경(Change file attributes)
[chmod](https://ko.wikipedia.org/wiki/Chmod) (Korean wiki) 명령어를 이용하면 파일 또는 디렉토리의 속성을 변경할 수 있습니다.<br>
The [chmod](https://en.wikipedia.org/wiki/Chmod) (English wiki) command can be used to change the attributes of a file or directory.

`chmod` 명령어를 사용하려면 어떤 권한을 타겟 파일 또는 디렉토리에 부여할 것인지를 결정해야 합니다.<br>
Before using the `chmod` command, you must decide what permissions you want to grant to the target file or directory.<br>

위에 제시된 예시를 보면 -r--r-xr-x 라고 되어 있는데, 이는 다음과 같이 네 개의 부분으로 나눌 수 있습니다.<br>
If you look at the example above, you can see that it is divided into four parts as follows.<br>

```
   -     r--         r-x         r-x
   ⬆️    ⬆️          ⬆️          ⬆️
   type  permission  permission  permission
         of user     of group    of others
```
<br>

type 부분은 해당 타겟이 파일인지 디렉토리인지를 나타냅니다.<br>
The type part indicates whether the target is a file or a directory.<br>

해당 타겟이 파일이라면 `-`가, 디렉토리라면 `d`가 나타납니다.<br>
If the target is a file, `-` will appear, and if it is a directory, `d` will appear.<br>

permission 부분은 각각 해당 타겟의 소유자, 그룹, 그 외의 사용자에게 부여할 권한을 나타냅니다.<br>
The permission part indicates the permissions to be granted to the owner, group, and other users of the target.<br>

`r`은 read(읽기) 권한, `w`는 write(쓰기) 권한, `x`는 execute(실행) 권한을 나타냅니다.<br>
`r` means read permission, `w` means write permission, and `x` means execute permission.<br>

> 참고: 실행 권한이란 읽기, 쓰기 외에 해당 파일을 실행할 수 있는 권한을 의미합니다.<br>
> NOTE: The execution permission means that you have permission to execute the file in addition to reading and writing.<br>
> 
> 이때 실행의 의미가 이해하기 어려울 수 있는데, 우리가 파일 내부에 쓸 수 있는 것은 단순한 문자나 숫자뿐 아니라 어떤 프로그램일 수도 있다는 점을 생각해 보시는 것이 좋습니다.<br>
It may be difficult to understand the meaning of execution, but it is better to think about the fact that we can write not only simple characters and numbers but also programs inside the file.<br>
>
> 즉, 실행 권한이란 파일 내부에 적혀 있는 여러 명령어, 쉽게 말해 프로그램으로써의 파일을 실행할 수 있는 권한을 의미합니다.<br>
In other words, execution permission is the permission to run a program that takes the form of a file.

<br>

각각의 권한은 2진수로 표현할 수 있습니다.<br>
Each permission can be represented in binary.<br>

```
   r    w    x
   -    -    -
   ⬆️   ⬆️   ⬆️
   2^2  2^1  2^0
```
<br>

`r` 권한은 2진법의 $2^2$ 자리에 1을, `w` 권한은 $2^1$ 자리에 1을, `x` 권한은 $2^0$ 자리에 1을 더한 값을 가집니다.<br>
The `r` permission has a value of 1 in the $2^2$ place of the binary number, the `w` permission has a value of 1 in the $2^1$ place, and the `x` permission has a value of 1 in the $2^0$ place.<br>

예컨대 rwx 권한은 $2^2 + 2^1 + 2^0 = 7$ 이므로 2진법으로 111이 됩니다.<br>
For example, rwx permission is $2^2 + 2^1 + 2^0 = 7$, so it becomes 111 in binary.<br>

이렇듯, 권한을 표시하는 방법에는 `r`, `w`, `x`라는 영문자를 이용한 방법과 2진법을 이용한 방법 두 가지가 있습니다.<br>
As you can see, there are two ways to display permissions: one using the English letters r, w, and x, and the other using binary.<br>

그래서 권한을 더하고 뺄 때 사용할 수 있는 방법도 `r`, `w`, `x`를 이용한 방법과 2진법을 이용한 방법 두 가지가 있습니다.<br>
So there are two ways to add and subtract permissions: one using the English letters r, w, and x, and the other using binary.<br>

다음은 권한의 종류를 나타내는 표입니다.<br>
The following table shows the types of permissions.<br>
<br>

|  #  |       Permission        | bin | rwx |
|:---:|:-----------------------:|:---:|:---:|
|  7  | read, write and execute | 111 | rwx |
|  6  | read and write			| 110 | rw- |
|  5  | read and execute		| 101 | r-x |
|  4  | read only				| 100 | r-- |
|  3  | write and execute		| 011 | -wx |
|  2  | write only				| 010 | -w- |
|  1  | execute only			| 001 | --x |
|  0  | none					| 000 | --- |
<br>

하지만 2진법을 이용한 방법이 보편적으로 더 많이 사용되는 편이기 때문에 여기서는 2진법을 이용하여 파일 또는 디렉토리에 대한 권한을 변경하는 방법을 알아보겠습니다.<br>
However, since the binary method is more commonly used, we will look at how to change the permissions of a file or directory using the binary method here.<br>

`chmod` 명령의 사용 방법은 아주 간단합니다.<br>
The way to use `chmod` command is very simple.<br>

파일에 접근할 수 있는 모든 사용자에게 rwx 권한을 부여하고 싶다면 다음과 같이 입력하면 됩니다.<br>
If you want to give rwx permission to all users who can access the file, just type the following.<br>

```
$ chmod 777 file_name
```
<br>

이렇게 하면 file_name 파일에 대한 권한이 777이 되어 모든 사용자가 읽고(4), 쓰고(2), 실행(1)할 수 있게 됩니다.<br>
This will make the permission for the file_name file 777, so that all users can read (4), write (2), and execute (1).<br>

만일 샤용자는 읽기, 쓰기만 가능하고, 그룹은 읽기만 가능하고, 다른 사용자는 아무것도 할 수 없도록 하고 싶다면 다음과 같이 입력하면 됩니다.<br>
If you want the user to be able to read and write, the group to be able to read, and no one else to be able to do anything, just type the following.<br>

```
$ chmod 640 file_name
```
<br>

더 자세한 내용은 `man` 명령으로 `chmod`의 매뉴얼을 참고하시기 바랍니다.<br>
For more detail read `man` entry of `chmod`:
```
$ man chmod
```

<br>

---
#### 3. 파일 사이즈 변경(Change the file size): 40 bytes

`ls -l` 명령을 실행한 결과를 살펴보면, `createdFile`의 파일 사이즈가 40 바이트라고 나옵니다.<br>
If you run the `ls -l` command, you will see that the file size of `createdFile` is 40 bytes.<br>

파일 사이즈를 40 바이트로 맞추려면, 원하는 텍스트 에디터에서 파일을 열고, 40 바이트 만큼 아무 문자나 집어 넣으면 됩니다.<br>
To make the file size 40 bytes, just open the file in the text editor of your choice and insert any character 40 bytes.<br>

이때, 공백도 하나의 문자로 취급되기 때문에, 공백을 적당히 넣어도 됩니다.<br>
Since a space is also considered a character, you can also insert a space.<br>

다만, 운영체제(OS)에서 파일 끝에 개행 문자를 추가하기 때문에, 파일 안에 입력할 문자는 39개 까지만 넣어야 합니다.<br>
However, since the operating system (OS) adds a newline character at the end of the file, you can only enter 39 characters in the file.<br>

> 예시(Example)<br>
> sdfsdfsdfsdfsdfsdfsdfsdfsdfsdfsdfsdfsdf, 총 39개의 문자를 입력합니다.<br>
> sdfsdfsdfsdfsdfsdfsdfsdfsdfsdfsdfsdfsdf, enter 39 characters in total.<br>

```
$ cat -e createdFile
sdfsdfsdfsdfsdfsdfsdfsdfsdfsdfsdfsdfsdf$
```
<br>

`cat -e` 명령으로 파일 끝에 개행 문자 `$`가 추가되었음을 확인할 수 있습니다.<br>
You can see that the newline character `$` is added at the end of the file using the `cat -e` command.<br>

<br>

---
#### 4. 타임스탬프 바꾸기(Change the timestamp)

파일을 만들 때 사용했던 [touch](https://linux.die.net/man/1/touch) 명령어를 이용하여 타임스탬프를 바꿀 수 있습니다.<br>
You can change the timestamp using the [touch](https://linux.die.net/man/1/touch) command that we used to create the file.<br>

단, `ctime`, 즉 파일을 생성한 시간은 바꿀 수 ***없습니다***.<br>
However, `ctime`, that is, the time the file was created, ***cannot*** be changed.<br>

일단, touch 명령을 다음과 같이 사용하면 파일의 타임스탬프를 바꿀 수 있습니다.<br>
First, if you use the touch command as follows, you can change the timestamp of the file.<br>

```
$ touch -a -m -t 202301011234.00 file_name.ext
```
<br>

이 때 `touch` 와 함께 사용된 옵션은 다음과 같은 의미를 갖습니다.<br>
The options used with `touch` have the following meanings.<br>
```
-a = accessed(접근한) time
-m = modified(수정한) time
-t = timestamp(타임스탬프) - [[CC]YY]MMDDhhmm[.ss] 형식.
```
<br>

예시에서 보았던 Jan 1 12:23 createdFile 을 얻으려면 다음과 같이 입력하면 됩니다.<br>
To get the Jan 1 12:23 createdFile that we saw in the example, just enter the following.<br>

```
$ touch -a -m -t 202301011223.00 createdFile
```
<br>

결과는 다음과 비슷한 형태로 나옵니다.<br>
The result is similar to the following.<br>

```
$ ls -l createdFile
total 8
-rw-r--r--  1 raymond  staff     0 Jan  1 12:34 createdFile
```
<br>

`ctime`이 변화되었는지 확인하려면 `stat` 명령을 사용하면 됩니다.<br>
To check if `ctime` has changed, use the `stat` command.<br>

`stat` 명령은 파일의 상태를 보여주는 명령입니다.<br>
The `stat` command shows the status of the file.<br>

```
$ stat createdFile
16777229 4899738 -r--r-xr-x 1 raymond staff 0 0 "Jan  1 12:34:00 2023" "Jan  1 12:34:00 2023" "Jan 15 16:07:19 2023" "Jan  1 12:34:00 2023" 4096 0 0x40 createdFile
```
<br>

> 참고: 일반적인 방법으로는 `ctime`을 변경할 수 없는데, 이것은 의도된 것입니다.<br>
> NOTE: We cannot change the `ctime` by ordinary means, and this is something designed. 
>
>`ctime`은 파일의 메타데이터를 변경할 때 항상 최신으로 업데이트되며, 다른 `ctime`을 적용할 방법이 없습니다.<br>
> `ctime` is always updated to the current when you change any of the file's metadata, and there is no way to apply a different `ctime`.<br>
>
> 파일의 `ctime`을 변경하려면 다음 중 하나를 수행해야 합니다.<br>
> To change the `ctime` of a file, you need to do one of the followings.<br>
> 1. 원하는 `ctime`으로 시스템 시간을 설정한 다음 `touch` 명령으로 파일을 수정하고, 다시 시스템 시간을 재설정합니다.<br>
> Set the system time to the ctime you want to impose, then touch the file, then reset the system time.<br>
> 
> 2. 커널을 수정하여 `ctime`을 변경하는 인터페이스를 추가합니다.
> Modify the kernel to add an interface to change the `ctime`.<br>
> 3. `debugfs` 명령 등을 사용하여 디스크 이미지에 직접 접근해서 디스크의 비트를 조정합니다(파일 시스템이 마운트된 동안 수행하면 안 됨).<br>
> Use `debugfs` or similar command to access the disk image directly and adjust the bits on the disk (do not do this while the file system is mounted).

<br>

---
#### 5. 파일 tar 하기(Compressing files with `tar`)

`tar` 는 `tape archiver`의 약자로, 과거 테이프가 저장장치로 사용되던 시절, 자기 테이프에 파일을 백업하기 위해 만들어진 명령입니다.<br>
The `tar` command is an abbreviation of `tape archiver`, and it was created to back up files to magnetic tape in the days when tape was used as a storage device.<br>

`tar` 명령은 파일을 압축하거나 압축을 풀어주는 명령입니다.<br>
The `tar` command compresses or decompresses files.<br>

조금 더 정확히 말하자면, `tar` 명령은 파일을 하나의 파일로 묶어주는 명령으로, `gzip`이나 `bzip2` 등의 압축 프로그램과 함께 사용할 수도 있습니다.<br>
To be more precise, the `tar` command groups files into a single file, and even can be used with `gzip` or `bzip2` compression programs.<br>

사용법은 간단해서, 다음과 같이 `tar` 명령 다음 아카이빙할 파일을 나열하면 됩니다.<br>
The usage is simple, so you can just list the files you want to archive after the `tar` command.<br>

> 예시 (Example)
```
$ tar -cf archive.tar file1 file2 file3 ...
```
<br>

`tar` 명령의 옵션(flags)은 다음과 같습니다.<br>
The options(flags) of the `tar` command are as follows.<br>

| 필수 옵션(Required Flags) | 설명(Description)                                                                                                                                                                                                                                                                                                                                                                        |
|:---------------------:|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         `-c`          | 아카이빙할 파일을 하나의 파일로 묶어줌<br>Groups files to be archived into a single file.                                                                                                                                                                                                                                                                                                               |
|         `-f`          | 아카이빙할 파일을 지정함<br>Specifies the file to be archived.                                                                                                                                                                                                                                                                                                                                    |
|         `-t`          | 아카이빙된 파일의 목록을 보여줌<br>Shows the list of archived files.                                                                                                                                                                                                                                                                                                                                 |
|         `-u`          | 파일이 아카이브에 없거나, 아카이브에 기록된 이후 수정된 경우에 한해 한 개 이상의 파일 매개변수를 아카이브 맨 끝에 추가함<br>Adds the files specified by one or more File parameters to the end of the archive only if the files are not in the archive already, or if they have been modified since being written to the archive.<br><br>~~큰 의미는 없지만~~ 실제 테이프에 저장할 때는 사용할 수 없다<br>You cannot use this flag when actually storing to tape. |
|         `-U`          | 파일 및 디렉토리의 속성(attributes)을 아카이빙하거나 추출할 수 있게 함<br>Allows archival and extraction of Extended Attributes<br><br>이 속성(Extended attributes)에는 접근 제어 목록(ACL; Access control list)가 포함된다.<br>The Extended Attributes include Access control list (ACL) also.                                                                                                                                 |
|         `-x`          | 아카이빙된 파일을 풀어줌<br>Decompresses the archived file.                                                                                                                                                                                                                                                                                                                                       |

<br>

일반적으로 `tar` 명령의 기본 옵션은 -cf 옵션입니다.<br>
The default option of the `tar` command is the -cf option.<br>

즉, `-c` 옵션으로 아카이빙할 파일 또는 디렉토리를을 하나의 파일로 묶겠다고 선언하고, `-f` 옵션으로 아카이빙할 파일을 지정하는 것입니다.<br>
That is, it declares that it will group the files or directories to be archived into a single file with the `-c` option, and specifies the file to be archived with the `-f` option.<br>

그러나 `-cf` 옵션만으로 아카이빙하는 경우, 아카이빙의 대상이 되는 파일 또는 디렉토리의 속성이 유지되지 않습니다.<br>
However, if you archive only with the `-cf` option, the attributes of the files or directories to be archived are not preserved.<br>

이때 중요한 것이 위 표에 없는 `-p` 옵션입니다.<br>
At this time, the important thing is the `-p` option that is not in the table above.<br>

`-p` 옵션은 옵셔널 옵션으로, 아카이빙할 때 또는 아카이브를 추출할 때 파일 또는 디렉토리의 속성을 유지하겠다는 옵션입니다.<br>
The `-p` option is an optional option that preserves the attributes of files or directories when archiving or extracting the archive.<br>

따라서, 파일 또는 디렉토리가 갖고 있던 속성을 유지하면서 아카이빙하려면 `-cf` 옵션에 `-p` 옵션을 추가해야 합니다.<br>
Therefore, if you want to archive while preserving the attributes of the files or directories, you must add the `-p` option to the `-cf` option.<br>

`tar`로 아카이브에서 파일과 디렉토리를 추출할 때는 `-x` 옵션을 사용합니다.<br>
When extracting files and directories from an archive with `tar`, use the `-x` option.<br>

즉, `tar` 명령의 추출시 기본 옵션은 `-xf`입니다.<br>
The default option for extracting with the `tar` command is `-xf`.<br>

아카이브에서 추출할 때 파일과 디렉토리의 속성을 유지한 채 추출하려면 아카이빙할 떄와 마찬가지로 `-p` 옵션을 추가하면 됩니다.<br>
To extract the attributes of the files and directories while extracting from the archive, just add the `-p` option as you did when archiving.<br>

그 외에, 아카이빙/추출 과정에서 대상 파일 및 디렉토리를 표시하기 위한 `-v` 옵션도 자주 사용됩니다.<br>
In addition, the `-v` option is often used to display the target files and directories during archiving / extraction.<br>

그래서 보통 사용하는 옵션 조합은 아카이빙할 때라면 `-cvpf`, 추출할 때라면 `-xvpf`입니다.<br>
So the usual option combination is `-cvpf` when archiving and `-xvpf` when extracting.<br>

> 참고: 자세한 옵션은 `man tar` 명령으로 확인할 수도 있고, [여기](https://www.ibm.com/docs/en/aix/7.1?topic=t-tar-command)에서 확인할 수도 있습니다.<br>
> NOTE: You can also check the options in the `man tar` command, or you can check it [here](https://www.ibm.com/docs/en/aix/7.1?topic=t-tar-command).<br>

<br>

---
### [뒤로(Back)](https://github.com/garlicvread/Shell_Scripting/tree/main/ShellScripts/02.FileAttributesModification/File)