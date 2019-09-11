---
title: NuGet CLI 사양 명령
description: Nuget.exe 사양 명령에 대 한 참조입니다.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: be6e4fdfe127d5582ecf9983a753a41e6760afe2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327570"
---
# <a name="spec-command-nuget-cli"></a>spec 명령 (NuGet CLI)

**적용 대상:** 패키지 만들기 &bullet; **지원 되는 버전:** 모두

새 패키지 `.nuspec` 에 대 한 파일을 생성 합니다. 프로젝트`.csproj`파일 ( `.nuspec` , `.vbproj`, `.fsproj`)과 동일한 폴더에서 실행 되 `spec` 는 경우 토큰화 된 파일을 만듭니다. 자세한 내용은 [패키지 만들기](../../create-packages/creating-a-package.md)를 참조 하세요.

## <a name="usage"></a>사용

```cli
nuget spec [<packageID>] [options]
```

여기서 `<packageID>` 은 `.nuspec` 파일에 저장할 선택적 패키지 식별자입니다.

## <a name="options"></a>변수

| 옵션 | Description |
| --- | --- |
| AssemblyPath | 메타 데이터에 사용할 어셈블리의 경로를 지정 합니다. |
| Force | 기존 `.nuspec` 파일을 덮어씁니다. |
| ForceEnglishOutput | *(3.5 이상)*  현재 언어 설정을 무시하고 영어를 기반으로 nuget.exe를 강제로 실행합니다. |
| Help | 명령어에 대한 도움말을 표시합니다. |
| NonInteractive | 사용자 입력이나 확인에 대한 프롬프트를 표시하지 않습니다. |
| Verbosity | 출력에 표시되는 세부정보의 양을 지정합니다: *정상적인*, *조용한*, *자세한*합니다. |

또한 [환경 변수](cli-ref-environment-variables.md)에 대한 정보를 참조할 수 있습니다.

## <a name="examples"></a>예제

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
