---
title: "NuGet CLI 미러 명령을 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe 미러 명령에 대 한 참조"
keywords: "nuget 미러 참조, 미러 명령"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 80b8f9a3b74030ffd3f1c7b784204d98be67d684
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/14/2018
---
# <a name="mirror-command-nuget-cli"></a>미러 명령 (NuGet CLI)

**적용 대상:** 게시 패키지 &bullet; **지원 되는 버전:** 3.2 +에서 사용 되지 않습니다.

패키지 및 대상 저장소에 지정 된 원본 저장소에서 해당 종속성을 미러링합니다.

> [!NOTE]
> 3.2 전에 NuGet 버전에 대 한이 명령을 사용 하려면로 이동 [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases)안정적인 최신 버전을 다운로드 `NuGet.ServerExtensions.dll` 및 `Nuget-Signed.exe` 로컬 디스크와 이름 바꾸기 `Nuget-Signed.exe` 를 `nuget.exe`.

## <a name="usage"></a>사용법

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

여기서 `<packageID>` 을 미러링 하는 패키지 또는 `<configFilePath>` 식별는 `packages.config` 파일을 미러링 하는 패키지를 나열 합니다.

`<listUrlTarget>` 소스 리포지토리를 지정 하 고 `<publishUrlTarget>` 대상 저장소를 지정 합니다.

대상 저장소에 있으면 `https://machine/repo` 실행 중인 [NuGet.Server](../hosting-packages/nuget-server.md), 목록 및 푸시 url 됩니다 `https://machine/repo/nuget` 및 `https://machine/repo/api/v2/package`각각.

## <a name="options"></a>옵션

| 옵션 | 설명 |
| --- | --- |
| apiKey | 대상 저장소에 대 한 API 키입니다. 없음, 1에 지정 된 경우 *%AppData%\NuGet\NuGet.Config* 사용 됩니다. |
| 도움말 | 도움말의 명령에 대 한 정보를 표시 합니다. |
| NoCache | NuGet 패키지를 사용 하 여 로컬 컴퓨터 캐시에서 방지 합니다. |
| Noop | 기록 수행 기능 하지만; 작업을 수행 하지 않습니다. 푸시 작업에 대 한 성공을 가정합니다. |
| 시험판 | 미러링 작업에 시험판 패키지를 포함합니다. |
| 소스 | 목록으로 미러링 하기 위해 패키지 소스입니다. 것에 정의 된 원본이 지정 된 경우 *%AppData%\NuGet\NuGet.Config* nuget.org를 지정 하지 않으면 기본값으로 사용 됩니다. |
| 시간 제한 | 서버에 밀어 넣는 초 제한 시간을 지정 합니다. 기본값은 300 초 (5 분)입니다. |
| 버전 | 설치할 패키지의 버전입니다. 지정 하지 않으면 최신 버전이 미러 됩니다. |

또한 참조 [환경 변수](cli-ref-environment-variables.md)

## <a name="examples"></a>예제

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
