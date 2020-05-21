---
title: NuGet 5.6 릴리스 정보
description: 새 기능, 버그 수정 및 Ecrs를 비롯 한 NuGet 5.6에 대 한 릴리스 정보입니다.
author: chgill-msft
ms.author: chgill
ms.date: 05/19/2020
ms.topic: conceptual
ms.openlocfilehash: e8d80a247da1cd18b53b35c51fb3d3dcf1cf68fa
ms.sourcegitcommit: 3529348ed394595d0fa01271486b831af9c97597
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/21/2020
ms.locfileid: "83727808"
---
# <a name="nuget-56-release-notes"></a>NuGet 5.6 릴리스 정보

NuGet 배포 차량:

| NuGet 버전 | Visual Studio 버전에서 사용 가능| .NET SDK에서 사용 가능|
|:---|:---|:---|
| [**5.6.0**](https://nuget.org/downloads) | [Visual Studio 2019 버전 16.6](https://visualstudio.microsoft.com/downloads/) | [3.1.300](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup> .NET Core 워크 로드와 함께 Visual Studio 2019와 함께 설치 됨

## <a name="summary-whats-new-in-56"></a>요약: 5.6의 새로운 기능

* 부동 버전이 포함 된 시험판 패키지를 지원 합니다. `Version="*-*"``Version="1.*-*"`지정 된 범위 내에서 시험판 버전을 포함 하 여, 및 유사한 float를 최신 버전으로 [#912](https://github.com/NuGet/Home/issues/912)

### <a name="issues-fixed-in-this-release"></a>이번 릴리스에서 수정된 문제

**미**

* `nuget push *.nupkg`snupkg가 없는 경우 실패- [#8148](https://github.com/NuGet/Home/issues/8148)

* Pack 및 기타 일부 코드 경로는 로캘에 따라 다릅니다. System.text.regularexpressions.regexoptions 사용 Regexoptions.cultureinvariant- [#8246](https://github.com/NuGet/Home/issues/8246)

* 성능: 언로드된 프로젝트 시나리오에 대 한 DG 사양은 미리 보기 복원으로 작성할 수 없습니다.- [#8793](https://github.com/NuGet/Home/issues/8793)

* 복원: 솔루션 종속성을 캐싱하여 성능을 향상 시킵니다. [#9201](https://github.com/NuGet/Home/issues/9201)

* Pm 콘솔을 사용 하 여 패키지를 설치한 후에는 PM UI가 SDK 스타일 프로젝트에서 작동 하지 않음- [#9203](https://github.com/NuGet/Home/issues/9203)

* /Vs에 따라 로컬 패키지 피드가 포함 된 PM UI에 포함 아이콘을 표시할 수 없습니다. [#9225](https://github.com/NuGet/Home/issues/9225)

* NuGetVersion. TryParseStrict ()는 구문 분석에 실패 하는 경우 false를 반환 합니다. [#9255](https://github.com/NuGet/Home/issues/9255)

* `nuget.exe push`에 대 한 도움말 `-source` 은 원본 URL이 아닌 원본 이름 사용을 제안 해야 합니다. [#9265](https://github.com/NuGet/Home/issues/9265)

* `dotnet nuget add package SourceUri`잘못 된 기본 패키지 원본 이름을 만듭니다. [#9277](https://github.com/NuGet/Home/issues/9277)

* 화면 읽기 프로그램에서 "검색 중 ..."을 알리지 않습니다. 탭 전환 시 메시지- [#9307](https://github.com/NuGet/Home/issues/9307)

* 접근성: 포커스 사각형 색은 진한 테마의 PM UI 탭에 액세스할 수 없습니다.- [#9336](https://github.com/NuGet/Home/issues/9336)

* nuget .exe 5.5이 MSBuild 14 또는 아래 [#9458](https://github.com/NuGet/Home/issues/9458) 으로 복원 되지 않습니다.

* 복원 메시지에서 밀리초 번 기록 안 함- [#8977](https://github.com/NuGet/Home/issues/8977)

* IOutputConsole 비동기 작업 [#9268](https://github.com/NuGet/Home/issues/9268)

* MSBuild 버전 선택은 일부 영어가 아닌 문화권에서 제대로 작동 하지 않습니다. [#9322](https://github.com/NuGet/Home/issues/9322)

* #9337에 대 한 누락 된 서식 기본값 `dotnet nuget list source`  -  [#9337](https://github.com/NuGet/Home/issues/9337)

* Perf: RestoreOperationLogger에 불필요 한 스레드 선호도가 있습니다. [#9288](https://github.com/NuGet/Home/issues/9288)

* 명령에 대 한 docs 자동 생성 `dotnet nuget` - [#9146](https://github.com/NuGet/Home/issues/9146)

* 기본 자세한 정도는 각 프로젝트의 noop 복원 [#8792](https://github.com/NuGet/Home/issues/8792) 보고 하지 않아야 합니다.

* `-DependencyVersion` `NuGet.exe update` 설치 명령- [#7694](https://github.com/NuGet/Home/issues/7694) 와 유사한의 지원 매개 변수


**Dcr**

* Net 5.0 대상 프레임 워크에 대 한 초기 지원 추가- [#9584](https://github.com/NuGet/Home/issues/9584)

* PM UI의 업데이트 탭에서 ID 별로 패키지 정렬- [#9278](https://github.com/NuGet/Home/issues/9278)


**[이 릴리스에서 해결 된 모든 문제 목록-5.6](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e3b2080c4b30708e48bf9f3)**
