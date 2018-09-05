---
title: NuGet CLI 미러 명령
description: Nuget.exe 미러 명령에 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d3a322e16c4ba212a856e9bf4d2eaab2872c31b6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550208"
---
# <a name="mirror-command-nuget-cli"></a>mirror 명령(NuGet CLI)

**적용 대상:** 게시 패키지 &bullet; **지원 되는 버전:** 3.2 이상에서 사용 되지 않음

패키지 및 대상 저장소에 지정 된 소스 리포지토리에서 해당 종속성을 미러링합니다.

> [!NOTE]
> 을 3.2 전에 NuGet 버전에 대해이 명령을 사용 하도록 설정 하려면로 이동 [ https://nuget.codeplex.com/releases ](https://nuget.codeplex.com/releases)다운로드를 안정적인 최신 릴리스를 선택 `NuGet.ServerExtensions.dll` 하 고 `Nuget-Signed.exe` 로컬 디스크 및 이름 바꾸기 `Nuget-Signed.exe` 에 `nuget.exe`입니다.

## <a name="usage"></a>사용법

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

여기서 `<packageID>` 미러, 패키지 또는 `<configFilePath>` 하 게 식별 하는 `packages.config` 미러링 하는 패키지를 나열 하는 파일입니다.

`<listUrlTarget>` 소스 리포지토리를 지정 하 고 `<publishUrlTarget>` 대상 리포지토리를 지정 합니다.

대상 리포지토리에에 있으면 `https://machine/repo` 실행 중인 [NuGet.Server](../hosting-packages/nuget-server.md), 목록 및 푸시 url 됩니다 `https://machine/repo/nuget` 및 `https://machine/repo/api/v2/package`각각.

## <a name="options"></a>옵션

| 옵션 | 설명 |
| --- | --- |
| ApiKey | 대상 리포지토리에 대 한 API 키입니다. 이 헤더가 없으면 구성 파일에 지정 된 사용 됩니다 (`%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)). |
| 도움말 | 도움말의 명령에 대 한 정보를 표시 합니다. |
| NoCache | 캐시 된 패키지를 사용 하 여 NuGet을 방지 합니다. 참조 [전역 패키지 및 캐시 폴더 관리](../consume-packages/managing-the-global-packages-and-cache-folders.md)합니다. |
| Noop | 로그 항목가 수행 되지만; 작업을 수행 하지 않습니다. 푸시 작업에 대 한 성공을 가정합니다. |
| PreRelease | 미러링 작업에 시험판 패키지를 포함합니다. |
| 소스 | 미러 패키지 원본의 목록입니다. 항목에 정의 된 소스 없음이 지정 된 경우 구성 파일 (위의 ApiKey 참조) 되는, 지정 되지 않은 경우 nuget.org에 기본값으로 지정 합니다. |
| 시간 제한 | 서버에 푸시하기 위한 초 제한 시간을 지정 합니다. 기본값은 300 초 (5 분). |
| 버전 | 설치 패키지의 버전입니다. 지정 하지 않으면 최신 버전 미러 됩니다. |

또한 참조 [환경 변수](cli-ref-environment-variables.md)

## <a name="examples"></a>예제

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
