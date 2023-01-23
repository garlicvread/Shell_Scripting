### Answer for Exercise 04: Diff command and Patch command

<br>

#### 1. 목표(Objectives)

우리는 `source` 파일과 `patch.patch` 파일을 참고하여 `result` 파일을 생성하는 것이 목표입니다.<br>
The goal is to create `result` file based on the given `source` file and `patch` file.<br>

ShellScripts/04.DiffAndPatch/Files 디렉토리에는 `source` 파일이 있습니다.<br>
There is a `source` file in ShellScripts/04.DiffAndPatch/Files directory.

`source` 파일을 다운로드 받아 `cat` 명령으로 살펴보면, 다음과 같은 내용이 들어 있습니다.<br>
Download the `source` file and check the content using `cat` command. The content is as follows.<br>

```
	The Fellowship of the Ring


Three Rings for the Elven-kings under the sky,
seven for the Dwarf-lords in their halls of stone,
Nine for Mortal Men doomed to die,
One for the Dark Lord on his dark throne
In the Land of Mordor where the Shadows lie.
One Ring to rule them all, One Ring to find them,
One Ring to bring them all and in the darkness bind them
In the Land of Mordor where the Shadows lie.


	Chapter 1

A LONG-EXPECTED PARTY

When Mr. Bilbo Baggins of Bag End announced that he would shortly be celebrating his eleventy-first birthday with a party of special magnificence, there was much talk and excitement in Hobbiton.
```

<br>

하지만 `cat` 명령의 기본 옵션으로는 파일의 내용을 자세히 확인할 수 없습니다.<br>
However, you cannot check the content of the file in detail using `cat` command with its default options.<br>

`source` 파일을 자세히 확인하고 싶으면 `cat` 명령에 여러 옵션을 추가해야 합니다.<br>
If you want to check the content of the `source` file in detail, you need to add several options to the `cat` command.<br>

예를 들어, 개행 문자가 있는지 확인하려면 `-e` 옵션을 추가해야 합니다.<br>
For example, if you want to check if there is a newline character, you need to add `-e` option.<br>

또, 탭 문자가 있는지 확인하려면 `-t` 옵션을 추가해야 합니다.<br>
Also, if you want to check if there is a tab character, you need to add `-t` option.<br>

문서의 줄 번호를 확인하려면 `-n` 옵션을 추가해야 합니다.<br>
If you want to check the line number of the document, you need to add `-n` option.<br>

이 명령을 모두 조합하여 `source` 파일의 내용을 확인하면 다음과 같습니다.<br>
If you combine all these commands to check the content of the `source` file, it will be as follows.<br>

```
cat -n -e -t source
     1	^IThe Fellowship of the Ring$
     2	$
     3	$
     4	Three Rings for the Elven-kings under the sky,$
     5	seven for the Dwarf-lords in their halls of stone,$
     6	Nine for Mortal Men doomed to die,$
     7	One for the Dark Lord on his dark throne$
     8	In the Land of Mordor where the Shadows lie.$
     9	One Ring to rule them all, One Ring to find them,$
    10	One Ring to bring them all and in the darkness bind them$
    11	In the Land of Mordor where the Shadows lie.$
    12	$
    13	$
    14	^IChapter 1$
    15	$
    16	A LONG-EXPECTED PARTY$
    17	$
    18	When Mr. Bilbo Baggins of Bag End announced that he would shortly be celebrating his eleventy-first birthday with a party of special magnificence, there was much talk and excitement in Hobbiton.$
    19	$
    20	$
    21	$
```

<br>

위 결과에서 `^I`는 탭 문자를 나타내고, `$`는 개행 문자를 나타냅니다.<br>
In the above result, `^I` represents a tab character, and `$` represents a newline character.<br>

이렇게 일일이 옵션을 추가하여 파일의 내용을 확인한 다음 다른 파일과의 차이점을 비교할 수도 있지만 아무래도 번거롭겠죠?<br>
You can check the content of the file by adding options one by one like above and then compare the differences with other files, but it will be a bit tedious, right?<br>

이 때 우리가 사용할 수 있는 다른 선택지가 바로 `diff` 명령과 `patch` 명령을 적절히 조합하는 방법입니다.<br>
In this case, another option we can use is to combine `diff` command and `patch` command appropriately.<br>

<br>

---

#### 2. `diff` 명령

`diff` 명령은 두 개의 파일을 비교하여 그 차이점을 보여줍니다.<br>
`diff` command compares two files and shows the differences.<br>

`diff` 명령의 기본 사용법은 다음과 같습니다.<br>
The basic usage of `diff` command is as follows.<br>

```
diff [opiton(flag)] file1 file2
```

<br>

예를 들어 `source` 파일과 `target` 파일의 차이점을 확인하려면 다음과 같이 명령을 실행합니다.<br>
For example, if you want to check the differences between `source` file and `target` file, run the command as follows.<br>

`target` 파일의 내용이 다음과 같다고 가정해 봅시다.<br>
Let's assume that the content of the `target` file is as follows.<br>

```
cat -e -t target
The Fellowship of the Ring$
$
$
Three Rings for the Elven-kings under the sky,$
Six for the Dwarf-lords in their halls of stone,$
Nine for Mortal Men doomed to die,$
^I * Feat. Korean traditional board game 3-6-9 lol *$
One for the Dark Lord on his dark throne$
In the Land of Mordor where the Shadows lie.$
One Ring to rule them all, One Ring to find them,$
One Ring to bring them all and in the darkness bind them$
In the Land of Mordor where the Shadows lie.$
$
$
Chapter One$
$
A LONG-EXPECTED PARTY$
$
When Mr. Bilbo Baggins of Bag End announced that he would shortly be celebrating his eleventy-first birthday with a party of special magnificence, there was much talk and excitement in Hobbiton.$
```

<br>

이제 `diff` 명령을 사용하여 `source` 파일과 `target` 파일의 차이점을 확인해 봅시다.<br>
Now let's use `diff` command to check the differences between `source` file and `target` file.<br>

```
diff source target
1c1
< 	The Fellowship of the Ring
---
> The Fellowship of the Ring
5c5
< seven for the Dwarf-lords in their halls of stone,
---
> Six for the Dwarf-lords in their halls of stone,
6a7
> 	 * Feat. Korean traditional board game 3-6-9 lol *
14c15
< 	Chapter 1
---
> Chapter One
19,21d19
<
<
<
```

<br>

위 결과에서 각 라인 맨 처음에 `<` 또는 `>` 기호를 발견할 수 있습니다.<br>
In the above result, you can find `<` or `>` symbol at the beginning of each line.<br>

`<` 기호는 `source` 파일에만 존재하는 내용을, `>` 기호는 `target` 파일에만 존재하는 내용을 나타냅니다.<br>
`<` symbol represents the content that only exists in `source` file, and `>` symbol represents the content that only exists in `target` file.<br>

1c1, 5c5, 6a7, 14c15, 19,21d19 등의 표기는 각각 다음과 같은 의미를 가집니다.<br>
1c1, 5c5, 6a7, 14c15, 19,21d19 and other notations mean the following.<br>

- 1c1 : 1번째 라인의 내용이 다름 (Contents of the first line are different)
- 5c5 : 5번째 라인의 내용이 다름 (Contents of the fifth line are different)
- 6a7 : 6번째 라인에 7번째 라인의 내용이 추가됨 (Contents of the seventh line are added to the sixth line)
- 14c15 : 14번째 라인의 내용이 다름 (Contents of the fourteenth line are different)
- 19,21d19 : 19번째 라인부터 21번째 라인까지 삭제됨 (Lines from the nineteenth line to the twenty-first line are deleted)

<br>

위 결과를 `patch.patch` 파일로 저장합시다.<br>
Let's save the above result as a `patch.patch` file.<br>

```
diff source target > patch.patch
```

<br>

---
#### 2. `patch` 명령을 사용하여 `target` 파일을 복구하기

이제 `target` 파일이 없고, `source` 파일과 `patch.patch` 파일만 존재한다고 가정해 봅시다.<br>
Now let's assume that `target` file does not exist and only `source` file and `patch` file exist.<br>

만일 우리가 `target` 파일을 실수로 삭제한 경우, `patch.patch` 파일을 사용하여 `target` 파일을 복구할 수 있습니다.<br>
If we accidentally deleted the `target` file, we can restore the `target` file using the `patch` file.<br>

