---
title: NuGet CLI 사양 명령
description: Nuget.exe 사양 명령에 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 68b165751ab6794d2a01d7e466619b1ce4d7ed72
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546451"
---
# <a name="spec-command-nuget-cli"></a>사양 명령 (NuGet CLI)

**적용 대상:** 패키지 만들기 &bullet; **지원 되는 버전:** 모든

생성 된 `.nuspec` 새 패키지에 대 한 파일입니다. 프로젝트 파일과 동일한 폴더에서 실행 하는 경우 (`.csproj`, `.vbproj`, `.fsproj`), `spec` 토큰화를 만들고 `.nuspec` 파일입니다. 자세한 내용은 참조 하세요. [패키지를 만드는](../create-packages/creating-a-package.md)합니다.

## <a name="usage"></a>사용법

```cli
nuget spec [<packageID>] [options]
```

여기서 `<packageID>` 에 저장 하는 선택적 패키지 식별자를 `.nuspec` 파일입니다.

## <a name="options"></a>옵션

| 옵션 | 설명 |
| --- | --- |
| AssemblyPath | 메타 데이터에 사용할 어셈블리의 경로 지정 합니다. |
| Force | 기존 덮어씁니다 `.nuspec` 파일입니다. |
| ForceEnglishOutput | *(3.5 이상)*  고정 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다. |
| 도움말 | 도움말의 명령에 대 한 정보를 표시 합니다. |
| NonInteractive | 사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다. |
| 자세한 정도 | 출력에 표시 되는 세부 정보의 양을 지정: *정상적인*, *quiet*, *자세한*합니다. |

또한 참조 [환경 변수](cli-ref-environment-variables.md)

## <a name="examples"></a>예제

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
