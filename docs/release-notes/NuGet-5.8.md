---
title: NuGet 5.8 릴리스 정보
description: 새 기능, 버그 수정 및 Ecrs를 비롯 한 NuGet 5.8에 대 한 릴리스 정보입니다.
author: dominofire
ms.author: feaguila
ms.date: 11/9/2020
ms.topic: conceptual
ms.openlocfilehash: 7f641c669cdb0cc979d698f6b219cbb4f2692a2e
ms.sourcegitcommit: 323a107c345c7cb4e344a6e6d8de42c63c5188b7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/15/2021
ms.locfileid: "98235752"
---
# <a name="nuget-58-release-notes"></a>NuGet 5.8 릴리스 정보

NuGet 배포 차량:

| NuGet 버전 | Visual Studio 버전에서 사용 가능 | .NET SDK에서 사용 가능 |
|:---|:---|:---|
| [**5.8**](https://nuget.org/downloads) | [Visual Studio 2019 버전 16.8](https://visualstudio.microsoft.com/downloads/) | [5.0](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |
| [**5.8.1**](https://nuget.org/downloads) | [Visual Studio 2019 버전 16.8.4](https://visualstudio.microsoft.com/downloads/) | |

<sup>1</sup> .net Core 워크 로드와 함께 Visual Studio 2019와 함께 설치 됨
  
> [!NOTE]
> Visual Studio 16.8, MSBuild 16.8 및 .NET 5.0에는 NuGet.exe 5.8 이상이 필요 합니다.


## <a name="summary-whats-new-in-58"></a>요약: 5.8의 새로운 기능
🎉 **.net 5.0를 대상으로 하는 NuGet 패키지에 대 한 전체 작성 및 복원 지원을 제공 하기 위한 첫 번째 릴리스입니다** 🎉

* Mmap/Createfilemapping에서 [#9807](https://github.com/NuGet/Home/issues/9807) 를 사용 하 여 nupkg 추출 가속화

* 패키지 관리자 UI 패키지 정보 창에서 패키지 취약성 세부 정보 표시- [#9850](https://github.com/NuGet/Home/issues/9850)

* 새 명령으로 서명 된 NuGet 패키지 확인 [`dotnet nuget verify`](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-verify) - [#8051](https://github.com/NuGet/Home/issues/8051)

* [`dotnet add package`](https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package#:~:text=dotnet%20add%20package%201%20Name%202%20Synopsis%203,when%20targeting%20a%20specific%20framework.%20...%206%20Examples)`--prerelease`시험판 버전을 포함 하 여 최신 버전의 패키지를 추가 하는 옵션을 지원 [#4699](https://github.com/NuGet/Home/issues/4699)

* CLI에서 명령을 사용 하 여 패키지 검색 [`nuget.exe search`](https://docs.microsoft.com/nuget/reference/cli-reference/cli-ref-search) [#9704](https://github.com/NuGet/Home/issues/9704)

* [`dotnet list package`](https://docs.microsoft.com/dotnet/core/tools/dotnet-list-package) 명령에서 `--verbosity` 옵션을 지원 [#9600](https://github.com/NuGet/Home/issues/9600)

* Visual Studio에서 .csproj 스타일의 PackageReference 기반 프로젝트에 대 한 빠른 No-Op 복원 최적화를 사용 합니다.- [#9565](https://github.com/NuGet/Home/issues/9565)

* 패키지 설치 및 업데이트와 같은 솔루션 수준 패키지 관리자 UI 작업은 더 빠르게 10 배 수 있습니다 [#6010](https://github.com/NuGet/Home/issues/6010)

* Visual Studio- [#9982](https://github.com/NuGet/Home/issues/9982), [#9984](https://github.com/NuGet/Home/issues/9984), [#10052](https://github.com/NuGet/Home/issues/10052), [#9903](https://github.com/NuGet/Home/issues/9903) 의 여러 NuGet 성능 향상


### <a name="issues-fixed-in-this-release"></a>이번 릴리스에서 수정된 문제

**Dcr**

* .NET 5.0 TFM: 프레임 워크 선행 규칙- [#9436](https://github.com/NuGet/Home/issues/9436)

* TargetFramework를 구문 분석할 때 NuGet에서 도트 플랫폼 버전을 유추할 수 없습니다. [#9842](https://github.com/NuGet/Home/issues/9842)

* 개별 TFI, TFV, TFI, TFI 속성을 사용 하는 대신 TargetFrameworkMoniker & TargetPlatformMoniker를 사용 하 여 프레임 워크를 유추 합니다. [#9895](https://github.com/NuGet/Home/issues/9895)

* `GetReferenceNearestTargetFrameworkTask()`플랫폼을 사용 하 여 대상 프레임 워크를 지원 하도록 업데이트 (예: net 5.0-windows)- [#9894](https://github.com/NuGet/Home/issues/9894)

* .NET 5.0 Visual Studio Api- [#9650](https://github.com/NuGet/Home/issues/9650)

* 패키지 관리자 UI: 패키지 통합 또는 업데이트 작업은 오류 (패키지 다운 그레이드 등)로 인해 차단 되지 않아야 합니다.- [#9224](https://github.com/NuGet/Home/issues/9224)

* 기능이 있는 프로젝트에 대해 NuGet 기능이 강화 되어야 합니다. "PackageReferences"- [#9957](https://github.com/NuGet/Home/issues/9957)

* Visual Studio에서 No-Op 복원 메시지 표시 안 함- [#6384](https://github.com/NuGet/Home/issues/6384)

**미**

* OutputWindowTextWriter 생성자는 백그라운드 스레드에서 호출 되지 않아야 합니다. [#9764](https://github.com/NuGet/Home/issues/9764)

* 빅 Endian Cpu에서 서명 된 패키지 복원- [#9547](https://github.com/NuGet/Home/issues/9547)

* OutputConsoleLogger는 MEF 생성자에서 선호도가 설정 메서드를 호출 하면 안 됩니다.- [#9591](https://github.com/NuGet/Home/issues/9591)

* Nuget.exe의 버그. 콘솔 `PrintJustified()` 메서드- [#9737](https://github.com/NuGet/Home/issues/9737)

* 잘못 된 바인딩으로 인해 패키지 메타 데이터가 가비지 수집 되는 경우 패키지 관리자 UI 메모리가 누수 [#9757](https://github.com/NuGet/Home/issues/9757)

* 서명 패키지 관리자 UI에서 packages.config 형식의 서명 된 패키지를 설치 하는 경우 오류 목록에 경고가 표시 되지 않습니다. [#9798](https://github.com/NuGet/Home/issues/9798)

* XPlat에는 공용 Api를 사용할 수 없습니다.- [#9821](https://github.com/NuGet/Home/issues/9821)

* #9822로 스레드 풀 스레드를 차단 하 여 발생 하는 솔루션 로드 시간에 리소스 경합을 줄입니다. `BlockingCollection.Take()`  -  [](https://github.com/NuGet/Home/issues/9822)

* 다중 대상 프로젝트를 사용 하는 명령줄 복원에서는 NuGet이 내부 빌드에서 대상 프레임 워크 관련 정보를 읽어야 [#9869](https://github.com/NuGet/Home/issues/9869)

* TargetFrameworkInformation 항목을 통해 런타임 식별자 그래프 읽기- [#9874](https://github.com/NuGet/Home/issues/9874)

* Visual Studio 및 일반 MSBuild evaluation 복원과 비교할 때 CrossTargeting 속성과 관련 하 여 정적 그래프 복원은 일관 되지 않습니다. [#9881](https://github.com/NuGet/Home/issues/9881)

* 정적 그래프 복원에서 다중 대상 프로젝트를 사용 하는 경우 NuGet은 내부 빌드에서 대상 프레임 워크 관련 정보를 읽어야 합니다. - [#9870](https://github.com/NuGet/Home/issues/9870)

* `net5.0-platform`Visual Studio에서 프로젝트를 로드 하 고 복원할 수 있도록 허용- [#9863](https://github.com/NuGet/Home/issues/9863)

* 패키지 관리자 UI에서 확인 된 버전 표시- [#9826](https://github.com/NuGet/Home/issues/9826)

* 패키지 관리자 UI: 솔루션 탐색기에 모든 NuGet 패키지 종속성이 표시 되지 않습니다. [#9898](https://github.com/NuGet/Home/issues/9898)

* SPDX 라이선스 목록 업데이트- [#9946](https://github.com/NuGet/Home/issues/9946)

* NuGet 패키지 관리를 연 후 VS 2019 충돌이 발생 함: 아이콘이 이미지 conversio에서 처리 되지 않은 예외를 발생 시킵니다 [#9696](https://github.com/NuGet/Home/issues/9696)

* Ilmerge는 온- [#9966](https://github.com/NuGet/Home/issues/9966) Newtonsoft.Js제외 해야 합니다.

* 오류가 없으면 ContinuePackingAfterGeneratingNuspec = false로 압축 하지 않아야 합니다.- [#9786](https://github.com/NuGet/Home/issues/9786)

* 패키지 관리자 UI: 아이콘이 색을 제대로 반전 하지 않음- [#10017](https://github.com/NuGet/Home/issues/10017)

* 복원 시 최신 및 No-Op 프로젝트에 대 한 프로젝트 수가 잘못 되었습니다. [#10026](https://github.com/NuGet/Home/issues/10026)

* `/p:RestoreUseStaticGraphEvaluation=true`값에 결과를 사용 하는 것은 Null 일 수 없습니다 [#9280](https://github.com/NuGet/Home/issues/9280)

* `dotnet pack` WPF 라이브러리 프로젝트에 대 한 별칭을 잘못 사용 합니다.- [#10020](https://github.com/NuGet/Home/issues/10020)

* 패키지 관리자 UI: 서명 유효성 검사에 실패 하면 NullReferenceException- [#10042](https://github.com/NuGet/Home/issues/10042)

* Codespaces: `object` 프로젝트 메타 데이터 값에 형식을 사용 하지 않습니다.- [#10055](https://github.com/NuGet/Home/issues/10055)

* Codespaces: 도구 옵션에 패키지 원본을 저장 하면 자격 증명을 덮어씁니다. [#9711](https://github.com/NuGet/Home/issues/9711)


**[이 릴리스에서 해결 된 모든 문제 목록-5.8](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f03519b777e78b4ffb2edeb)**

**[이 릴리스의 문제 목록-5.8](https://github.com/NuGet/NuGet.Client/compare/5.7.0.6726...5.8.0.6930)**

### <a name="community-contributions"></a>커뮤니티 기여

이 NuGet 릴리스를 위해 도움을 주는 모든 참가자에 게 감사 합니다.

|대상|Pr|문제|
|----|----|----|
[omajid](https://github.com/omajid) | [3437](https://github.com/NuGet/NuGet.Client/pull/3437) | 오류 메시지에 오타가 있습니다. "administrator" 대신 "관리자로"- [#9662](https://github.com/NuGet/Home/issues/9662)
[odalet](https://github.com/odalet) | [3341](https://github.com/NuGet/NuGet.Client/pull/3341) | AssemblyInformationalVersion 보고서가 잘못 된 NuGet 팩이 "설명이 필요 합니다."- [#5548](https://github.com/NuGet/Home/issues/5548)
[campersau](https://github.com/campersau) | [3501](https://github.com/NuGet/NuGet.Client/pull/3501) | `RepositoryMetadata.Equals()` 분기 및 커밋 속성을 고려 하지 않습니다.- [#9613](https://github.com/NuGet/Home/issues/9613)
[Youssef1313](https://github.com/Youssef1313) | [3599](https://github.com/NuGet/NuGet.Client/pull/3599) | Visual Studio 오류 목록 창에서 뉴 코드를 클릭 하면로 이동 해야 https://docs.microsoft.com/nuget/reference/errors-and-warnings/  -  [#9934](https://github.com/NuGet/Home/issues/9934)
[ChrisMaddock](https://github.com/ChrisMaddock) | [3624](https://github.com/NuGet/NuGet.Client/pull/3624) | Visual Studio 옵션을 통해 새 패키지 소스를 추가할 때 ' https://'를 사용 합니다.- [#9974](https://github.com/NuGet/Home/issues/9974)
[Zzok](https://github.com/Therzok) | [3636](https://github.com/NuGet/NuGet.Client/pull/3636) | `RuntimeEnvironmentHelper.IsRunningOnVisualStudio`Mono- [#9989](https://github.com/NuGet/Home/issues/9989) 의 성능 문제
[thomaslevesque](https://github.com/thomaslevesque) | [3442](https://github.com/NuGet/NuGet.Client/pull/3442) | SemanticVersion 클래스에 대 한 TypeConverter 추가- [#9125](https://github.com/NuGet/Home/issues/9125)

## <a name="summary-whats-new-in-581"></a>요약: 5.8.1의 새로운 기능

* package.lock.jspackages.config 5.8- [#10257](https://github.com/NuGet/Home/issues/10257) 에서 잘못 된 대상 프레임 워크를 사용 합니다.

* 5.8 + 16.8 PackageReference 및 packages.config를 혼합할 때 전이적 프로젝트 종속성을 확인할 수 없습니다 [#10326](https://github.com/NuGet/Home/issues/10326)

**[이 릴리스에서 수정 된 모든 문제 목록-5.8.1](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5ff7aeae16150e3b19910391)**

**[이 릴리스의 커밋 목록-5.8.1](https://github.com/NuGet/NuGet.Client/compare/5.8.0.6930...5.8.1.7021)**

## <a name="feedback-welcome"></a>사용자 의견 환영

Microsoft는 사용자의 의견을 소중하게 생각합니다.  이 릴리스에 문제가 있는 경우 [GitHub 문제](https://github.com/NuGet/Home/issues) 및 [Visual Studio 개발자 커뮤니티](https://developercommunity.visualstudio.com/) 에서 기존 문제를 확인 하세요.  NuGet 내의 새로운 문제에 대 한 자세한 내용은 [GitHub 문제](https://github.com/NuGet/Home/issues/new)를 보고 하세요.
일반적인 NuGet 환경 문제에 대 한 자세한 내용은 **문제 보고 > 도움말** 에서 즐겨 사용 하는 IDE의 [문제 보고](https://docs.microsoft.com/visualstudio/ide/how-to-report-a-problem-with-visual-studio) 옵션을 통해 알려주세요.
