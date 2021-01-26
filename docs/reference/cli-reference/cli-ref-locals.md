---
title: NuGet CLI 지역 명령
description: nuget.exe 지역 명령에 대 한 참조
author: JonDouglas
ms.author: jodou
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: 25feb29c7b96c47681cedd8208b8595952d3ca49
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779196"
---
# <a name="locals-command-nuget-cli"></a>로컬 명령 (NuGet CLI)

**적용 대상:** 패키지 사용 &bullet; **지원 버전:** 3.3 이상

*Http 캐시*, *전역 패키지* 폴더 및 임시 폴더와 같은 로컬 NuGet 리소스를 지우거 나 나열 합니다. `locals`명령을 사용 하 여 해당 위치의 목록을 표시할 수도 있습니다. 자세한 내용은 [전역 패키지 및 캐시 폴더 관리](../../consume-packages/managing-the-global-packages-and-cache-folders.md)를 참조 하세요.

## <a name="usage"></a>사용량

```cli
nuget locals <folder> [options]
```

여기서 `<folder>` 는 `all` , `http-cache` , `packages-cache` *(3.5 및 이전 버전)*, `global-packages` , `temp` *(3.4 +)* 및 `plugins-cache` *(4.8 +)* 중 하나입니다.

## <a name="options"></a>옵션

- **`-Clear`**

  지정 된 폴더를 지웁니다.

- **`-ConfigFile`**

  적용할 NuGet 구성 파일입니다. 지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` 또는 `~/.config/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.

- **`-ForceEnglishOutput`**

  *(3.5 +)* 고정 된 영어 기반 문화권을 사용 하 여 nuget.exe을 강제로 실행 합니다.

- **`-?|-help`**

  명령에 대 한 도움말 정보를 표시 합니다.

- **`-List`**

  지정 된 폴더의 위치 또는 모든 폴더의 위치를 *모두* 함께 사용할 경우 나열 합니다.

- **`-NonInteractive`**

  사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.

- **`-Verbosity [normal|quiet|detailed]`**

  출력에 표시 되는 세부 정보의 양을 지정 합니다. `normal` (기본값), `quiet` 또는 `detailed` 입니다.

[환경 변수](cli-ref-environment-variables.md) 참조

## <a name="examples"></a>예제

```cli
nuget locals all -list
nuget locals http-cache -clear
```

추가 예제는 [전역 패키지 및 캐시 폴더 관리](../../consume-packages/managing-the-global-packages-and-cache-folders.md)를 참조 하세요.
