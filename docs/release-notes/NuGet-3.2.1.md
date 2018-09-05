---
title: NuGet 3.2.1 릴리스 정보
description: 다음을 포함 하 여 NuGet 3.2.1 릴리스 정보는 문제, 버그 수정, 추가 된 기능 및 Dcr 알려져 있습니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e5ddbb8aa52ef85c823404364a3aca79fd16f3b1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548192"
---
# <a name="nuget-321-release-notes"></a>NuGet 3.2.1 릴리스 정보

[NuGet 3.2 릴리스 정보](../release-notes/nuget-3.2.md) | [NuGet 3.3 릴리스 정보](../release-notes/nuget-3.3.md)

명령줄 용 NuGet 3.2.1에 적은 수의 최적화 및 3.2 릴리스에 대 한 픽스를 사용 하 여 2015 년 10 월 12 일에 릴리스 되었으며에서 사용할 수 있습니다 [dist.nuget.org](http://dist.nuget.org/index.html)합니다.

## <a name="improvements"></a>향상 된 기능

* NuGet의 원래 대/소문자를 사용 하 여 구성 파일을 이제 사용 `NuGet.Config`합니다.  이 대/소문자 구분 운영 체제에서 중요 [1427](https://github.com/NuGet/Home/issues/1427)
* NuGet 복원은 이제 dnx 프로젝트를 무시 (`*.xproj`)를 사용 하 여 처리할지 `dnu` [1227](https://github.com/NuGet/Home/issues/1227)
* 작업할 때 네트워크 사용률을 최적화 `index.json` 등록 데이터를 패키지 하 고 [1426](https://github.com/NuGet/Home/issues/1426)
* V2 서비스를 사용 하 여 더 강력한 것으로 처리 하는 향상 된 리소스 다운로드 [1448](https://github.com/NuGet/Home/issues/1448)

## <a name="fixes"></a>수정

* NuGet 업데이트를 올바로 업데이트 `.csproj` / `.vcxproj` 참조 [1483](https://github.com/NuGet/Home/issues/1483)
* 이제 로컬.nuget 폴더는 SpecialFolders.UserProfile 찾을 수 없는 경우 만들지 못하도록 방지 [1531](https://github.com/NuGet/Home/issues/1531)
* 로컬 캐시에 다운로드 하는 동안 손상 되는 패키지의 처리를 개선 [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)

명령줄 및 Visual Studio 확장을 NuGet GitHub에서 확인할 수 있습니다 해결 된 문제 목록은 [3.2.1 마일스 톤](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)

## <a name="known-issues"></a>알려진 문제

찾을 수 있는 GitHub 문제 목록에서 문제를 추적 하려면 계속 합니다. [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)