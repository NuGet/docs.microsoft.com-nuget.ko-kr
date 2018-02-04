---
title: "NuGet CLI 명령을 추가 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "nuget.exe에 대 한 참조 추가 명령"
keywords: "nuget 참조를 추가, 패키지 명령 추가"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 70c86f8d240bd308224f6b7887b630cc1e953bf8
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/02/2018
---
# <a name="add-command-nuget-cli"></a>명령 (NuGet CLI)를 추가 합니다.

**적용 대상**: 게시 패키지 &bullet; **지원 되는 버전**: 3.3 +

패키지 ID 및 버전 번호에 대 한 폴더가 만들어지고 여기서 계층적 레이아웃에서 HTTP가 아닌 패키지 소스 (폴더 또는 UNC 경로)에 지정 된 패키지를 추가 합니다. 예:

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

을 복원 하거나 패키지 소스에 대해 업데이트 하는 경우 계층 레이아웃 훨씬 더 나은 성능을 제공 합니다.

패키지에 있는 모든 파일을 확장 하 고 대상 패키지 원본에 사용 된 `-Expand` 전환 합니다. 일반적으로 추가 하위 폴더와 같은 대상에 나타나는 결과 `tools` 및 `lib`합니다.

## <a name="usage"></a>사용법

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

여기서 `<packagePath>` 를 추가 하려면 패키지에 경로 이름 및 `<sourcePath>` 패키지를 추가할 폴더 기반 패키지 소스를 지정 합니다. HTTP 원본은 지원 되지 않습니다.

## <a name="options"></a>옵션

| 옵션 | 설명 |
| --- | --- |
| ConfigFile | 적용할 NuGet 구성 파일입니다. 지정 하지 않으면 *%AppData%\NuGet\NuGet.Config* 사용 됩니다.| 
| Expand | 패키지의 패키지 원본에 있는 모든 파일을 추가합니다. |
| ForceEnglishOutput | *(3.5 +)*  고정, 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다. |
| 도움말 | 도움말의 명령에 대 한 정보를 표시 합니다. |
| NonInteractive | 사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다. |
| 자세한 정도 | 출력에 표시 되는 세부 정보 수준을 지정: *일반*, *quiet*, *자세한*합니다. |

또한 참조 [환경 변수](cli-ref-environment-variables.md)

## <a name="examples"></a>예제

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
