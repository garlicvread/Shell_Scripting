# Excercise 04 : Diff Command and Patch Command

### Basic Information

| Exercise 04                    |
|--------------------------------|
| Files to turn in : result					 |
| Allowed functions : None				   |
| Notes : n/a							             |

<br>

---
### TO-DO

<br>

#### 1. `diff` 명령과 `patch` 명령 (`diff` Command and `patch` Command)

여기서는 `diff` 명령과 `patch` 명령의 사용법을 알아보겠습니다.<br>
Now, we will learn how to use `diff` command and `patch` command.

`diff` 명령과 `patch` 명령은 텍스트 파일에 사용할 수 있는 명령입니다.<br>
`diff` command and `patch` command are commands that can be used on text files.<br>

따라서 바이너리 파일이라든지 특수한 목적을 달성하기 위해 만들어진 응용프로그램에서 사용되는 파일, 예컨대 .doc, .pdf, .xlsx, .wav 등의 파일에 사용할 수는 있지만 잘 동작하지 않습니다.<br>
Therefore, although it can be used on files such as binary files or files that are used in applications that are made to achieve special purposes(purpose-built), such as .doc, .pdf, .xlsx, .wav, etc., it does not work well.

아무튼, 두 명령은 따로따로 쓰일 수도 있지만, 보통 하나의 패키지처럼 같이 묶어서 학습하는 경우가 많습니다.<br>
Anyways, both commands can be used separately, but they are usually learned together something like a package.<br>

`diff` 명령은 두 파일을 행을 기준으로 비교(또는 계산)하여 서로 다른 부분을 보여줍니다.<br>
`diff` command compares (or calculates) two files based on rows and shows the differences between them.<br>

이때 두 파일의 다른 점을 `patch` 라고 합니다.<br>
Here, the difference between the two files is called `patch`.<br>

방금 이야기한 `patch`는 명령어 `patch`와는 다르니 앞으로 혼란이 없도록 차이점이라 하겠습니다.<br>
The `patch` just mentioned is different from the `patch` command, so I will call it a difference from now on to avoid confusion.<br>

우리가 `diff` 명령으로 찾아낸 두 파일 간의 차이점인 `patch`를 `patch` 명령으로 다른 파일에 적용할 수 있습니다.<br>
We can apply the `patch`, which is the difference between the two files found by the `diff` command, to another file using the `patch` command.<br>

이 과정을 그림으로 표현하면 다음과 같습니다.<br>
This process can be represented by the following figure.<br>

┌───────────┐   ┌───────────┐   ┌───────────┐
│ Version A │ + │   Patch   │ = │ Version B │
└───────────┘   └───────────┘   └───────────┘

그리고 패치 파일은 다음과 같이 만들어진다고 생각하면 기억하기 쉽습니다.<br>
And you can remember that the patch file is created as follows.<br>

┌───────────┐   ┌───────────┐   ┌───────────┐
│ Version B │ - │ Version A │ = │   Patch   │
└───────────┘   └───────────┘   └───────────┘

적용된 패치를 제거하는 과정은 다음과 같이 생각하면 좋습니다.<br>
The process of removing the applied patch is as follows.<br>

┌───────────┐   ┌───────────┐   ┌───────────┐
│ Version B │ - │   Patch   │ = │ Version A │
└───────────┘   └───────────┘   └───────────┘

<br>

---

#### 2. `diff` 명령과 `patch` 명령을 사용하는 이유 (Reasons of using `diff` and `patch` command)

그렇다면 왜 `diff` 명령과 `patch` 명령을 사용할까요?<br>
Then, why do we use `diff` command and `patch` command?

여러 이유가 있겠지만, 다음과 같은 이점이 있습니다.<br>
There are many reasons, but the following benefits are available.

* 첫째, `diff` 명령은 두 개의 파일을 비교하여 그 차이점을 보여주므로, `patch` 명령 없이 사용한다고 하더라도 파일 간의 차이점을 확인하는 데 유용합니다.<br>
  First, `diff` command compares two files and shows the differences, so even if you use it without `patch` command, it is useful to check the differences between files.<br><br>

* 둘째, 종종 서드 파티로부터 패치를 제공받는 경우가 있을 수 있는데, 이 때 `patch` 명령을 사용하여 패치를 적용할 수 있습니다.<br>
  Second, you may receive patches from third parties, and in this case you can apply the patch using the `patch` command.<br><br>

  특히 패치의 크기는 크지만 실제 변경된 분량이 상대적으로 작은 경우, `patch` 명령을 사용하여 패치를 적용하는 것이 패치 파일 전부를 적용하는 것보다 더 효율적인 경우가 많습니다.<br>
  Especially when the patch size is large but the actual number of change is relatively small, it is often more efficient to apply the patch using the `patch` command than to apply the entire patch file.<br><br>

* 셋째, `diff` 명령을 적용했던 원본 파일과 완벽하게 일치하지 않는 파일에 패치를 적용할 수 있습니다.<br>
  Third, you can apply a patch to a file that does not perfectly match the original file to which the `diff` command was applied exactly.<br><br>

  예컨대, 우리가 CMS(Contents Management System)를 사용하고 있고, CMS 관리를 configuraion 파일을 통해 하고 있다고 가정해 봅시다.<br>
  For example, let's assume that we are using CMS (Contents Management System) and managing CMS through configuration file.<br><br>

  보통 CMS 공급업체가 버전 업그레이드를 하는 경우, 새로운 버전의 CMS를 설치하고 기존의 configuration 파일을 새로운 버전의 CMS에 적용하는 방식으로 업그레이드를 진행합니다.<br>
  Usually, when the CMS supplier upgrades the version, the new version of CMS is installed and the existing configuration file is applied to the new version of CMS.<br><br>

  이 configuration 파일에 로컬 수정분이 있는 경우, 새로운 버전의 CMS를 적용하면 기존에 우리가 작업했던 로컬 변경 사항이 사라지게 됩니다.<br>
  In this case, if there are local changes in the configuration file, and if we apply the new version of CMS, it will delete the local changes we worked on.<br><br>

  이 경우, `diff` 명령을 사용하여 기존의 configuration 파일과 로컬에서 수정한 configuration 파일의 차이점을 확인한 후, `patch` 명령을 사용하여 로컬에서 수정한 configuration 파일에 적용하면 기존의 configuration 파일에 우리가 작업했던 로컬 변경 사항을 잃지 않고 CMS 공급 업체의 최신 버전 CMS를 적용할 수 있습니다.<br>
  In this case, you can apply the latest version of CMS from CMS supplier without losing the local changes we worked on by using the `patch` command to apply the local configuration file after checking the differences between the original configuration file and the local configuration file using the `diff` command.

<br>

---
* [여기](https://github.com/garlicvread/Shell_Scripting/tree/main/ShellScripts/04.DiffAndPatch/Files)에서 `diff 명령과 patch 명령`의 내용을 확인할 수 있습니다.<br>
  You can read the content of `Excercise 04 - Diff and Patch` [here](https://github.com/garlicvread/Shell_Scripting/tree/main/ShellScripts/04.DiffAndPatch/Files).