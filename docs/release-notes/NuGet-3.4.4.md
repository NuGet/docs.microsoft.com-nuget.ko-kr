---
title: NuGet 3.4.4 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 3.4.4를 포함 하는 NuGet에 대 한 릴리스 정보입니다.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4e5e635432147afba4809562035bc8c762d31af4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780221"
---
# <a name="nuget-344-release-notes"></a>NuGet 3.4.4 릴리스 정보

[NuGet 3.4.3 릴리스 정보](../release-notes/nuget-3.4.3.md)  |  [NuGet 3.5-베타 릴리스 정보](../release-notes/nuget-3.5-Beta.md)

이 릴리스의 주요 초점은 Visual Studio 확장에 대 한 몇 가지 수정 사항이 포함 된 nuget.exe 3.4.3 버전의 품질 향상 이었습니다.

VSIX를 다운로드 하 고 [여기](https://dist.nuget.org/index.html)에서 nuget.exe 수 있습니다.

## <a name="344-rtm-2016-05-19"></a>[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)

[전체 변경 로그](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[문제 목록](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a>변경

- 팩의 향상 된 기능: 기호를 압축 하 `project.json` 고, 및 [ \# 606](https://github.com/NuGet/NuGet.Client/pull/606) 를 사용 하 여 압축
- 업데이트 명령 [605]에서 프로젝트를 찾을 수 없는 경우 예외를 표시 합니다. \#https://github.com/NuGet/NuGet.Client/pull/605
- 입력에서 패키지 유형을 읽고 `.nuspec` , `project.json` [ \# 603](https://github.com/NuGet/NuGet.Client/pull/603) 를 압축 하는 경우
- NuGet을 만듭니다. 프로젝트는 공유 되지 않습니다. [\#602](https://github.com/NuGet/NuGet.Client/pull/602)
- HTTP 응답 시간 제한 [ \# 599](https://github.com/NuGet/NuGet.Client/pull/599) 로 푸시 제한 시간을 사용 합니다.
- 이후 시간에 패키지 파일의 시간이 사용 되지 않습니다. [ \# 597](https://github.com/NuGet/NuGet.Client/pull/597)
- `NuGet.Core.dll`XML 문제 [ \# 594](https://github.com/NuGet/NuGet.Client/pull/594) 을 해결 하기 위해 버전을 2.12.0로 업데이트 하는 중
- /NuGet.CommandLine.XPlat-v \<verbosity\> \<mode\> [ \# 593](https://github.com/NuGet/NuGet.Client/pull/593)
- `project.json`또는 `packages.config` [ \# 590](https://github.com/NuGet/NuGet.Client/pull/590) 를 사용 하지 않고 오류 복원 표시
- 필요한 버전이 다른 경우 종속성 버전 수정 [ \# 559](https://github.com/NuGet/NuGet.Client/pull/559)