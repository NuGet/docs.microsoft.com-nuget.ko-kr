---
title: 3.4.4 NuGet 릴리스 정보
description: NuGet 3.4.4 포함에 대 한 릴리스 정보는 문제, 버그 수정, 추가 된 기능 및 Dcr 알려져 있습니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 44a9f21c61f0552fdc21aab24f48eee993654b01
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547475"
---
# <a name="nuget-344-release-notes"></a>3.4.4 NuGet 릴리스 정보

[NuGet 3.4.3 릴리스 정보](../release-notes/nuget-3.4.3.md) | [NuGet 3.5 베타 릴리스 정보](../release-notes/nuget-3.5-Beta.md)

이 릴리스의 주된 초점은 3.4.3의 품질 향상 된 버전의 nuget.exe도 Visual Studio 확장에는 몇 가지 수정 덧붙여야 합니다.

VSIX와 nuget.exe 둘 다를 다운로드할 수 있습니다 [여기](https://dist.nuget.org/index.html)합니다.

## <a name="344-rtmhttpsgithubcomnugetnugetclienttree344-rtm-2016-05-19"></a>[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)

[전체 변경 로그](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[문제 목록](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a>변경 내용

- 팩 향상 된 기능: 향상 된 기호를 압축 하는 것으로 압축 `project.json` 점점 더 많은 [ \#606](https://github.com/NuGet/NuGet.Client/pull/606)
- 업데이트 명령에서 프로젝트를 찾을 수 없습니다. 한 경우 예외를 표시 [\#605] (https://github.com/NuGet/NuGet.Client/pull/605
- 패키지 형식 입력에서 읽은 `.nuspec` 하 고 `project.json` 압축할 때 [ \#603](https://github.com/NuGet/NuGet.Client/pull/603)
- 프로젝트가 아니라 NuGet.Shared를 확인 합니다. [\#602](https://github.com/NuGet/NuGet.Client/pull/602)
- HTTP 응답 시간 제한으로 푸시 제한 시간을 사용 하 여 [ \#599](https://github.com/NuGet/NuGet.Client/pull/599)
- 미래를 사용 하 여 패키지 파일에 사용 되는 해당 시간 것 [ \#597](https://github.com/NuGet/NuGet.Client/pull/597)
- 업데이트 `NuGet.Core.dll` 2.12.0 XML 문제를 해결 하려면 버전 [ \#594](https://github.com/NuGet/NuGet.Client/pull/594)
- 지원./NuGet.CommandLine.XPlat-v \<세부 정보 표시\> \<모드\> [ \#593](https://github.com/NuGet/NuGet.Client/pull/593)
- 오류를 표시 하지 않고 복원 `project.json` 나 `packages.config` [ \#590](https://github.com/NuGet/NuGet.Client/pull/590)
- 필요한 버전 다를 때 종속성 버전을 수정 [ \#559](https://github.com/NuGet/NuGet.Client/pull/559)