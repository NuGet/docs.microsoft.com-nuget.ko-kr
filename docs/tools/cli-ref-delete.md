---
title: NuGet CLI 삭제 명령
description: Nuget.exe delete 명령에 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 11eea6e806d7bfe364587db9c7ef8374da1819f9
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548512"
---
# <a name="delete-command-nuget-cli"></a>delete 명령 (NuGet CLI)

**적용 대상:** 게시 패키지 &bullet; **지원 되는 버전:** 모든

삭제 하거나 패키지 소스에서 패키지 목록에서 제거 합니다. Nuget.org를 delete 명령에 대 한 [패키지 목록](../policies/deleting-packages.md)합니다.

## <a name="usage"></a>사용법

```cli
nuget delete <packageID> <packageVersion> [options]
```

여기서 `<packageID>` 및 `<packageVersion>` 정확한 패키지 나열을 취소 하거나 삭제를 식별 합니다. 정확한 동작은 원본에 따라 달라 집니다. 로컬 폴더에 대 한 예를 들어 패키지를 삭제 합니다. nuget.org 패키지 나열 하지 않습니다.

## <a name="options"></a>옵션

| 옵션 | 설명 |
| --- | --- |
| ApiKey | 대상 리포지토리에 대 한 API 키입니다. 없는 경우 구성 파일에 지정 된 사용 됩니다. |
| ConfigFile | NuGet 구성 파일을 적용 합니다. 지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.|
| ForceEnglishOutput | *(3.5 이상)*  고정 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다. |
| 도움말 | 도움말의 명령에 대 한 정보를 표시 합니다. |
| NonInteractive | 사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다. |
| 소스 | 서버 URL을 지정합니다. Nuget.org에 대 한 URL은 `https://api.nuget.org/v3/index.json`합니다. 개인 피드를 대체 호스트 이름, 예를 들어 *%hostname%/api/v3*합니다. |
| 자세한 정도 | 출력에 표시 되는 세부 정보의 양을 지정: *정상적인*, *quiet*, *자세한*합니다. |

또한 참조 [환경 변수](cli-ref-environment-variables.md)

## <a name="examples"></a>예제

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
