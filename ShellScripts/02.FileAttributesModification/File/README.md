# Ex02: Basic File modification

## File attributes

|              Exercise 02              |
|---------------------------------------|
| Files to create : createdFile.tar     |
| Allowed functions : None              |
| Notes : n/a                           |

### TODO

* 프로젝트 디렉토리에 `createdFile` 이라는 파일을 생성하시오.<br>
  Create a file called createdFile in your project directory.<br>
<br>

* 다음과 같은 결과물을 만들어낼 수 있는 방안을 강구할 것(total 1 부분은 제외):<br>
  Figure out a way for the output to look like this(except for the “total 1” line):<br>

```
$ ls -l
total 1
-r--r-xr-x  1 login wheel  40 Jun 1 12:34 createdFile
$
```

* 파일을 만들고 파일 속성을 변경했으면 `tar` 명령을 사용하여 `.tar` 파일로 변환하시오.<br>
  Once you have created your file and changed the attributes of the file, turn it into a `.tar` file using the `tar` command.

> Notes:
> 1. 파일의 타임스탬프에 12:34의 시간 대신 연도가 표시되어도 무방함.<br>
     A year will be accepted instead of the time 12:34, on the timestamp of the file.<br>
> 2. UNIX 기반 시스템에서 파일을 생성하는 방법을 모르는 경우 이 [문서](https://www.quora.com/How-do-I-create-a-file-in-a-directory-in-Unix)를 참조할 것.<br>
     If you find yourself without knowing how to create a file in UNIX-based systems, you can read this [article](https://www.quora.com/How-do-I-create-a-file-in-a-directory-in-Unix).