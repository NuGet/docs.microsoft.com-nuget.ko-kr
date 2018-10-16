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

**모든 버전에서 모두 지원됩니다.**

패키지 소스 또는 패키지 목록에서 삭제합니다. Nuget.org에서 delete 명령어는 [패키지 목록에서 삭제](../policies/deleting-packages.md)의 의미를 갖습니다.

## <a name="usage"></a>사용법

```cli
nuget delete <packageID> <packageVersion> [options]
```

여기서 `<packageID>` 및 `<packageVersion>` 는 패키지를 삭제하거나 목록에서 지울 특정 패키지를 지정하는데 사용합니다. 패키지 원본에 따라 동작이 달라질 수 있습니다. 예를 들어, 로컬 폴더 내부에서 사용할 경우에는 패키지를 삭제하지만, nuget.org의 패키지에서 사용할 경우에는 목록에서 지우는 기능을 수행합니다.

## <a name="options"></a>옵션

| 옵션 | 설명 |
| --- | --- |
| ApiKey | 대상 리포지토리에 대한 API 키입니다. 키가 없는 경우 구성 파일에 지정된 값이 사용됩니다. |
| ConfigFile | 수정할 NuGet 구성 파일입니다. 지정하지 않으면 기본적으로 Windows에서는 `%AppData%\NuGet\NuGet.Config`, Mac이나 Linux에서는 `~/.nuget/NuGet/NuGet.Config`가 사용됩니다.| 
| ForceEnglishOutput | *(3.5 이상)* 현재 언어 설정을 무시하고 영어를 기반으로 nuget.exe를 강제로 실행합니다. |
| 도움말 | 명령어에 대한 도움말을 표시합니다. |
| NonInteractive | 사용자 입력이나 확인에 대한 프롬프트를 표시하지 않습니다. |
| 소스 | 서버 URL을 지정합니다. Nuget.org에 대한 URL은 `https://api.nuget.org/v3/index.json`입니다. 개인적인 피드의 경우 예를 들어 *%hostname%/api/v3*와 같이 호스트 이름을 대체합니다. |
| 자세한 정도 | 출력에 표시 되는 세부 정보의 양을 지정: *정상적인*, *quiet*, *자세한*합니다. |

또한 [환경 변수](cli-ref-environment-variables.md)에 대한 정보를 참조할 수 있습니다.

## <a name="examples"></a>예제

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
