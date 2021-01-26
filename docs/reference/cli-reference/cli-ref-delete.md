---
title: NuGet CLI delete 명령
description: nuget.exe delete 명령에 대 한 참조
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 96c75366ae69b34f5cd1f55feb53087b5d0ea324
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775949"
---
# <a name="delete-command-nuget-cli"></a>delete 명령 (NuGet CLI)

**적용 대상:** 패키지 게시 &bullet; **지원 버전:** 모두

패키지 원본에서 패키지를 삭제 하거나 목록에서 제거 합니다. Nuget.org의 경우 delete 명령은 [패키지를 나열](../../nuget-org/policies/deleting-packages.md)하지 않습니다.

## <a name="usage"></a>사용량

```cli
nuget delete <packageID> <packageVersion> [options]
```

여기서 `<packageID>` 및 `<packageVersion>` 은 삭제할 정확한 패키지를 식별 합니다. 정확한 동작은 원본에 따라 달라 집니다. 예를 들어 로컬 폴더의 경우 패키지는 삭제 됩니다. nuget.org의 경우 패키지가 나열 되지 않습니다.

## <a name="options"></a>옵션

- **`-ApiKey`**

  대상 리포지토리의 API 키입니다. 존재 하지 않는 경우 구성 파일에 지정 된 항목을 사용 합니다.

- **`-ConfigFile`**

  적용할 NuGet 구성 파일입니다. 지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` 또는 `~/.config/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.

- **`-ForceEnglishOutput`**

  *(3.5 +)* 고정 된 영어 기반 문화권을 사용 하 여 nuget.exe을 강제로 실행 합니다.

- **`-?|-help`**

  명령에 대 한 도움말 정보를 표시 합니다.

- **`-NonInteractive`**

  사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.

 - **`-np|-NoPrompt`**

   삭제할 때 메시지를 표시 하지 않습니다.

 - **`-NoServiceEndpoint`** "Api/v2/패키지"를 원본 URL에 추가 하지 않습니다.

- **`-src|-Source`**

  서버 URL을 지정합니다. Nuget.org의 URL은 `https://api.nuget.org/v3/index.json` 입니다. 개인 피드의 경우 호스트 이름 (예: *% hostname%/api/v3*)을 대체 합니다.

- **`-Verbosity [normal|quiet|detailed]`**

  출력에 표시 되는 세부 정보의 양을 지정 합니다. `normal` (기본값), `quiet` 또는 `detailed` 입니다.

[환경 변수](cli-ref-environment-variables.md) 참조

## <a name="examples"></a>예

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
