---
title: NuGet CLI 지역 명령
description: Nuget.exe 지역 명령에 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: b02360c38ad66c95bbe3c7d403ef4a959112c91a
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327810"
---
# <a name="locals-command-nuget-cli"></a>locals 명령(NuGet CLI)

**적용 대상:** 패키지 &bullet; 사용 **지원 버전:** 3.3+

*Http 캐시*, *전역 패키지* 폴더 및 임시 폴더와 같은 로컬 NuGet 리소스를 지우거 나 나열 합니다. `locals` 명령을 사용 하 여 해당 위치의 목록을 표시할 수도 있습니다. 자세한 내용은 [전역 패키지 및 캐시 폴더 관리](../../consume-packages/managing-the-global-packages-and-cache-folders.md)를 참조 하세요.

## <a name="usage"></a>사용법

```cli
nuget locals <folder> [options]
```

여기서 `<folder>` 는 `all` `global-packages` `temp` , `plugins-cache`    , (3.5 및 이전 버전),, (3.4 +) 및 (4.8 +) 중 하나입니다. `packages-cache` `http-cache`

## <a name="options"></a>변수

| 옵션 | Description |
| --- | --- |
| Clear | 지정 된 폴더를 지웁니다. |
| ConfigFile | 적용할 NuGet 설정 파일입니다. 지정하지 않으면 기본적으로 Windows에서는 `%AppData%\NuGet\NuGet.Config`, Mac이나 Linux에서는 `~/.nuget/NuGet/NuGet.Config`가 사용됩니다.|
| ForceEnglishOutput | *(3.5 이상)*  현재 언어 설정을 무시하고 영어를 기반으로 nuget.exe를 강제로 실행합니다. |
| Help | 명령어에 대한 도움말을 표시합니다. |
| List | 지정 된 폴더의 위치 또는 모든 폴더의 위치를 *모두*함께 사용할 경우 나열 합니다. |
| NonInteractive | 사용자 입력이나 확인에 대한 프롬프트를 표시하지 않습니다. |
| Verbosity | 출력에 표시되는 세부정보의 양을 지정합니다: *정상적인*, *조용한*, *자세한*합니다. |

또한 [환경 변수](cli-ref-environment-variables.md)에 대한 정보를 참조할 수 있습니다.

## <a name="examples"></a>예

```cli
nuget locals all -list
nuget locals http-cache -clear
```

추가 예제는 [전역 패키지 및 캐시 폴더 관리](../../consume-packages/managing-the-global-packages-and-cache-folders.md)를 참조 하세요.
