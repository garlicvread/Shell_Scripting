# Exercise 03: Symbolic and Hard Links

---

## Basic Information

| Exercise 03                    |
|--------------------------------|
| Files to create : links.tar			 |
| Allowed functions : None				   |
| Notes : n/a							             |

---

<br>

여기서는 `Symbolic Link`와 `Hard Link`에 대해 알아봅니다.<br>
Here, you will learn about `Symbolic Link` and `Hard Link`.<br>

파일 시스템 아래에서 파일은 `i-node`로 표시됩니다.<br>
Files are represented by `i-nodes` in the file system.<br>

디렉토리는 그럼 파일과 다른가? 할 수 있는데, 유닉스 계열의 운영체제에서는 ***디렉토리도 파일로 간주합니다***.<br>
You may wonder if directories are different from files. In Unix-like operating systems, ***directories are also considered as files***.<br>

심지어 네트워크도 파일이라고 볼 수 있습니다.<br>
Even network can be considered as a file.<br>

그리고 유닉스의 파일 시스템의 파일은 기본적으로 `i-node`에 대한 링크입니다.<br>
And files in Unix file system are basically links to `i-nodes`.<br>

>참고: `i-node`는 `ls -i` 명령으로 확인할 수 있습니다.<br>
> NOTE: You can check `i-node` with `ls -i` command.

<br>

하드 링크는 동일한 `i-node`에 대한 링크가 있는 다른 파일을 생성합니다.<br>
A hard link creates another file that has a link to the same underlying `i-node`.<br>

하드 링크가 만들어지면 링크는 동일한 `i-node`에 연결됩니다.<br>
When a hard link is created, the link is connected to the same `i-node`.<br>

원본 파일을 삭제하거나 이름을 바꾸거나 이동해도 하드 링크는 원래의 `i-node`에 연결되어 있으므로 아무런 영향을 받지 않습니다.<br>
Even if you delete, rename, or move the original file, the hard link is still connected to the original `i-node`, so it will not be affected.<br>

`i-node`의 데이터에 대한 모든 변경 사항은 해당 `i-node`를 참조하는 모든 파일에 반영됩니다.<br>
Any changes to the data on the `i-node` are reflected in all files that refer to that `i-node`.<br>

즉, 하드 링크가 생성되면 원본 파일과 하드 링크는 동일한 `i-node`를 참조하므로, 원본 파일의 내용을 변경하면 하드 링크의 내용도 변경됩니다.<br>
In other words, when a hard link is created, the original file and the hard link refer to the same `i-node`, so if you change the contents of the original file, the contents of the hard link will also be changed.<br>

파일을 삭제하면 `i-node`에 대한 링크 하나가 제거됩니다.<br>
When a file is deleted, one link to the `i-node` is removed.<br>

만일 그 `i-node`에 대한 모든 링크가 삭제되면 비로소 그 `i-node`가 삭제됩니다.<br>
The `i-node` is only deleted(or deletable/over-writable) when all links to the `i-node` are deleted.<br>

한편, 심볼릭 링크는 파일 시스템 내부에 존재하는 다른 이름에 대한 링크입니다.<br>
On the other hand, a symbolic link is a link to another name in the file system.<br>

요컨대, 심볼릭 링크는 윈도우에서의 바로 가기와 비슷하다고 볼 수 있습니다.<br>
In other words, a symbolic link can be considered as a shortcut in Windows system.<br>

> 참고: 하드 링크는 파일끼리만 생성할 수 있습니다.<br>
> Note: Hard links can only be created between files.<br>
>
> 그러나 심볼릭 링크는 단순히 다른 파일의 이름일 뿐이기 때문에 디렉토리를 대상으로도 생성할 수 있습니다.<br>
> However, symbolic links can be created on directories as well, because they are simply another name for a target.<br>

<br>

---
* [여기](https://github.com/garlicvread/Shell_Scripting/tree/main/ShellScripts/03.SymbolicAndHardLinks/File)에서 `심볼릭 링크와 하드 링크 연습`의 내용을 확인할 수 있습니다.<br>
  You can read the content of `Excercise 03 - Symbolic(soft) Links and Hard Links` [here](https://github.com/garlicvread/Shell_Scripting/tree/main/ShellScripts/03.SymbolicAndHardLinks/File).