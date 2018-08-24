---
title: NuGet CLI locals 명령
description: Nuget.exe locals 명령에 대 한 참조
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: 38d8b9366fb2749b77c987c950da3aa9e7f029fc
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/23/2018
ms.locfileid: "42794137"
---
# <a name="locals-command-nuget-cli"></a>locals 명령(NuGet CLI)

**적용 대상:** 소비 패키지 &bullet; **지원 되는 버전:** 3.3 이상

같은 로컬 NuGet 리소스를 나열 하거나 선택을 취소 합니다 *http 캐시*를 *전역 패키지* 폴더 및 임시 폴더입니다. `locals` 해당 위치의 목록을 표시 하려면 명령을 사용할 수도 있습니다. 자세한 내용은 [전역 패키지 및 캐시 폴더 관리](../consume-packages/managing-the-global-packages-and-cache-folders.md)합니다.

## <a name="usage"></a>사용법

```cli
nuget locals <folder> [options]
```

여기서 `<folder>` 중 하나인 `all`를 `http-cache`, `packages-cache` *(3.5 및 이전 버전)* 를 `global-packages`를 `temp` *(3.4 이상)*, 및 `plugins-cache` *(4.8 이상)* 합니다.

## <a name="options"></a>옵션

| 옵션 | 설명 |
| --- | --- |
| 지우기 | 지정된 된 폴더를 지웁니다. |
| ConfigFile | NuGet 구성 파일을 적용 합니다. 지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.|
| ForceEnglishOutput | *(3.5 이상)*  고정 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다. |
| 도움말 | 도움말의 명령에 대 한 정보를 표시 합니다. |
| 목록 | 지정된 된 폴더의 위치 또는 함께 사용할 경우 모든 폴더의 위치 나열 *모든*합니다. |
| NonInteractive | 사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다. |
| 자세한 정도 | 출력에 표시 되는 세부 정보의 양을 지정: *정상적인*, *quiet*, *자세한*합니다. |

또한 참조 [환경 변수](cli-ref-environment-variables.md)

## <a name="examples"></a>예제

```cli
nuget locals all -list
nuget locals http-cache -clear
```

추가 예제를 보려면 [전역 패키지 및 캐시 폴더 관리](../consume-packages/managing-the-global-packages-and-cache-folders.md)합니다.
