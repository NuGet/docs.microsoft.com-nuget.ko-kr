---
title: NuGet CLI 명령 추가
description: Nuget.exe에 대 한 참조 추가 명령
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7a72186e1dece082cd200a03849a0b12c751a645
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545836"
---
# <a name="add-command-nuget-cli"></a>add 명령(NuGet CLI)

**적용 대상**: 게시 패키지 &bullet; **지원 되는 버전**: 3.3 이상

비 HTTP 패키지 원본 (폴더 또는 UNC 경로)에 패키지 ID와 버전 번호에 대 한 폴더가 만들어지고 여기서 계층형 레이아웃으로 지정 된 패키지를 추가 합니다. 예를 들어:

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

복원 하거나 패키지 원본에 대 한 업데이트를 계층형 레이아웃 훨씬 더 나은 성능을 제공 합니다.

대상 패키지 원본에는 패키지의 모든 파일을 확장 하려면 사용 된 `-Expand` 전환 합니다. 일반적으로 이렇게 추가 하위 폴더와 같은 대상에 나타나는 `tools` 고 `lib`입니다.

## <a name="usage"></a>사용법

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

여기서 `<packagePath>` 에 추가 하려면 패키지에 경로 이름 및 `<sourcePath>` 패키지를 추가할 폴더 기반 패키지 원본을 지정 합니다. HTTP 소스는 지원 되지 않습니다.

## <a name="options"></a>옵션

| 옵션 | 설명 |
| --- | --- |
| ConfigFile | NuGet 구성 파일을 적용 합니다. 지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.|
| Expand | 패키지의 패키지 원본에 있는 모든 파일을 추가합니다. |
| ForceEnglishOutput | *(3.5 이상)*  고정 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다. |
| 도움말 | 도움말의 명령에 대 한 정보를 표시 합니다. |
| NonInteractive | 사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다. |
| 자세한 정도 | 출력에 표시 되는 세부 정보의 양을 지정: *정상적인*, *quiet*, *자세한*합니다. |

또한 참조 [환경 변수](cli-ref-environment-variables.md)

## <a name="examples"></a>예제

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
