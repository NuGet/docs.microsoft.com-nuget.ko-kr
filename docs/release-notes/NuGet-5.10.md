---
title: NuGet 5.10 릴리스 정보
description: 새로운 기능, 버그 수정 및 DCR을 포함하여 NuGet 5.10에 대한 릴리스 정보입니다.
author: zkat
ms.author: kmarchan
ms.date: 6/11/2021
ms.topic: conceptual
ms.openlocfilehash: 80a372074604f5c0073f78927b84de00e78acc74
ms.sourcegitcommit: 5f706c62c97b78bbe3d8c7e95659976535fe486f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/23/2021
ms.locfileid: "122726953"
---
# <a name="nuget-510-release-notes"></a>NuGet 5.10 릴리스 정보

NuGet 배포 차량:

| NuGet 버전 | Visual Studio 버전에서 사용 가능 | .NET SDK에서 사용 가능 |
|:---|:---|:---|
| [**5.10.0**](https://nuget.org/downloads) | [Visual Studio 2019 버전 16.10](https://visualstudio.microsoft.com/downloads/) | [5.0.300](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1</sup> .NET Core 워크로드를 Visual Studio 2019와 함께 설치
  
> [!NOTE]
> Visual Studio 16.10, MSBuild 16.10 및 .NET 5.0.300 이상에는 NuGet.exe 5.10이 필요합니다.

## <a name="summary-whats-new-in-510"></a>요약: 5.10의 새로운 내용

* 서명: dotnet trusted-signers 명령 구현 - [#8053](https://github.com/NuGet/Home/issues/8053)

* Linux에서는 기본 유효성 검사를 사용하지 않도록 설정하지만 Windows 기본적으로 사용하도록 설정 - [#10713](https://github.com/NuGet/Home/issues/10713)

* .NET 5+ Linux/MAC에서 패키지 서명 확인을 위한 ENV 변수 추가 - [#10742](https://github.com/NuGet/Home/issues/10742)

* 대규모 솔루션에 대한 새 패키지 설치 성능 향상 - [#10166](https://github.com/NuGet/Home/issues/10166)

* `nfproj`프로젝트 형식을 Nuget CLI용 supportedProjectExtensions 목록에 추가합니다. - [#10562](https://github.com/NuGet/Home/issues/10562)

### <a name="issues-fixed-in-this-release"></a>이번 릴리스에서 수정된 문제

* 프로젝트를 `<requireLicenseAcceptance>` 패킹할 때 요소 표시 안 함 - [#5133](https://github.com/NuGet/Home/issues/5133)

* [CPVM] 미리 보기 경고가 dotnet cli에 표시되어야 합니다. - [#10226](https://github.com/NuGet/Home/issues/10226)

* PMUI의 배경색 및 전경색 토큰을 CommonDocumentColors - [#10608](https://github.com/NuGet/Home/issues/10608)

* [버그 Bash] PM UI에서 탭 간을 빠르게 전환할 때 오류 목록 창에 "사용자가 취소한 작업" 오류 표시 - [#10671](https://github.com/NuGet/Home/issues/10671)

* PM UI: 솔루션 수준에서 패키지 설치 성능 향상 - [#10210](https://github.com/NuGet/Home/issues/10210)

* GetService를 NuGet 모든 위치에서 GetServiceAsync로 바꿉다. 클라이언트 - [#3784](https://github.com/NuGet/Home/issues/3784)

* 상대 경로의 NuGet.exe 팩 성능 문제 `..` - [#5016](https://github.com/NuGet/Home/issues/5016)

* 원본 경로의 수준이 증가함에 따라 "nuget pack"의 성능이 [저하됩니다. #5706](https://github.com/NuGet/Home/issues/5706)

* NuGet 중복 파일로 nuspec을 패키징할 때 오류가 발생하지 않습니다. - [#6941](https://github.com/NuGet/Home/issues/6941)

* NuGet 팩 "지정된 DateTimeOffset을 Zip 파일 타임스탬프로 변환할 수 없습니다." - [#7001](https://github.com/NuGet/Home/issues/7001)

* 포장된 패키지 파일의 타임스탬프가 timezone - [#7395](https://github.com/NuGet/Home/issues/7395)

* NU1004는 더 많은 실행 가능한 정보를 포함해야 합니다. [- #7696](https://github.com/NuGet/Home/issues/7696)

* [버그 Bash] [테스트 실패] 'dotnet restore --use-lock-file --locked-mode'를 실행할 때는 비어 있거나 형식이 잘못된 잠금 파일을 업데이트해서는 안 [됩니다.](https://github.com/NuGet/Home/issues/8640) - #8640

* NuGetVersionRange를 사용하면 논리적으로 잘못된 범위를 구문 분석할 수 [있습니다. #9145](https://github.com/NuGet/Home/issues/9145)

* PM UI는 선택한 패키지 원본과 가리킨 패키지 원본 간에 구별 가능한 배경색을 표시할 수 [없습니다. - #9538](https://github.com/NuGet/Home/issues/9538)

* 설치할 프로젝트를 선택하기 위한 확인란이 화면 판독기에서 읽지 않음 - [#9578](https://github.com/NuGet/Home/issues/9578)

* 세부 정보 창 버전 드롭다운 기본 선택은 설치/업데이트 탭에서 설치/최신성이어야 합니다. - [#9887](https://github.com/NuGet/Home/issues/9887)

* 일부 .NET 5 SDK 보고서 TargetPlatformMoniker에 대한 해결 방법 계정을 ` ,Version= `  -  [제거합니다#9913](https://github.com/NuGet/Home/issues/9913)

* dotnet nuget verify가 너무 작음 - [#10316](https://github.com/NuGet/Home/issues/10316)

* VersionRange는 한 자리 범위를 구문 분석할 수 없습니다. [- #10342](https://github.com/NuGet/Home/issues/10342)

* VS 솔루션 관리자가 디버깅 중에 에 대해 null 예외를 throw합니다. [- #10352](https://github.com/NuGet/Home/issues/10352)

* CLI 예외 메시지를 문자열 리소스 파일로 이동 - [#10392](https://github.com/NuGet/Home/issues/10392)

* 데드 코드 제거(TabItemButtonAutomationPeer) - [#10435](https://github.com/NuGet/Home/issues/10435)

* 업데이트 상황에 맞는 메뉴가 첫 번째 선택한 항목으로 스크롤되어야 합니다. [- #10498](https://github.com/NuGet/Home/issues/10498)

* 솔루션 PMUI 세부 정보에서 가로 막대가 겹칩니다. [- #10533](https://github.com/NuGet/Home/issues/10533)

* 서명: 인증서가 만료되고 타임스탬프가 신뢰할 수 없는 경우 기본 서명 세부 정보가 표시되지 않음 - [#10535](https://github.com/NuGet/Home/issues/10535)

* 사용하도록 설정된 원본이 없을 경우 PM UI가 표시되지 않습니다. [#10541](https://github.com/NuGet/Home/issues/10541)

* 패키지 메타데이터(세부 정보, 사용 중단)가 CodeSpaces [-](https://github.com/NuGet/Home/issues/10549) #10549 nuget.org 끌어오지 않는 경우가 있습니다.

* 디버그 세션 중 예외로 PMUI 초기화 실패 - [#10559](https://github.com/NuGet/Home/issues/10559)

* nuget 복원으로 big endian 시스템에서 패키지 무결성 검사 실패 - [#10567](https://github.com/NuGet/Home/issues/10567)

* PackagingException 대신 FormatException이 throw됩니다. [- #10595](https://github.com/NuGet/Home/issues/10595)

* CPVM - 그래프 보행 알고리즘의 동시성 문제 - [#10598](https://github.com/NuGet/Home/issues/10598)

* PMC PowerShell 버전 원격 분석 추가 - [#10609](https://github.com/NuGet/Home/issues/10609)

* NuGetVersion 정렬 성능 향상 - [#10611](https://github.com/NuGet/Home/issues/10611)

* 신뢰할 수 있는 서명자 추가에 일치하지 않는 인수가 [있습니다. - #10647](https://github.com/NuGet/Home/issues/10647)

* Vs2019 v16.9.0: NuGet 패키지 관리자 탭을 "업데이트"에서 "설치"로 전환해도 프레임이 업데이트되지 않습니다. - [#10654](https://github.com/NuGet/Home/issues/10654)

* PMUI의 버전 번호에서 "v"를 제거합니다. [- #10677](https://github.com/NuGet/Home/issues/10677)

* INuGetProjectService.GetInstalledPackagesAsync가 CPS 프로젝트 시스템 추천을 받기 전에 throw함 - [#10681](https://github.com/NuGet/Home/issues/10681)

* 포함된 아이콘으로 인해 찾아보기 탭의 원본 "Microsoft Visual Studio 오프라인 패키지"에서 액세스가 거부됩니다. - [#10687](https://github.com/NuGet/Home/issues/10687)

* MSBuildProjectExtensionsPath가 설정되지 않은 경우 INuGetProjectService.GetInstalledPackagesAsync가 throw됩니다. [- #10739](https://github.com/NuGet/Home/issues/10739)

* "dotnet nuget remove source nuget.org"가 처음으로 작동하지 않습니다. [#10745](https://github.com/NuGet/Home/issues/10745)

* Nuget은 UI 스레드에 대한 동기 호출을 만드는 비동기 메서드에서 스레드 풀 스레드를 [차단합니다. #10775](https://github.com/NuGet/Home/issues/10775)

* `PackageLoadContext.GetInstalledAndTransitivePackagesAsync` 는 데드 코드이고 성능이 저하됩니다. [- #10790](https://github.com/NuGet/Home/issues/10790)

* NuGet SDK 패키지에서 포함된 아이콘 사용 - [#10795](https://github.com/NuGet/Home/issues/10795)

* SPDX 라이선스 목록 업데이트 - [#10806](https://github.com/NuGet/Home/issues/10806)

**[이 릴리스에서 해결된 모든 문제 목록 - 5.10](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTY2MTQ)**
  
**[이 릴리스의 커밋 목록 - 5.10.0](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.10.0.7240)**
  
### <a name="community-contributions"></a>커뮤니티 기여

이 NuGet 릴리스를 만드는 데 도움을 주신 모든 기여자에게 감사드립니다.

|대상|Prs|문제|
|----|----|----|
[2018년 10월](https://github.com/louis-z) | [3991](https://github.com/NuGet/NuGet.Client/pull/3991) | VersionRange는 한 자리 범위를 구문 분석할 수 없습니다. [- #10342](https://github.com/NuGet/Home/issues/10342)
[omajid](https://github.com/omajid) | [3860](https://github.com/NuGet/NuGet.Client/pull/3860) | NuGet. 클라이언트 build.sh 손상되었습니다. - [#10139](https://github.com/NuGet/Home/issues/10139)
[Nirmal4G](https://github.com/Nirmal4G) | [3623](https://github.com/NuGet/NuGet.Client/pull/3623) | NuGet. 클라이언트 build.sh 손상되었습니다. - [#10139](https://github.com/NuGet/Home/issues/10139)
[BlackGad](https://github.com/BlackGad) | [3953](https://github.com/NuGet/NuGet.Client/pull/3953) | 원본 경로의 수준이 증가함에 따라 "nuget pack"의 성능이 [저하됩니다. #5706](https://github.com/NuGet/Home/issues/5706)
[BlackGad](https://github.com/BlackGad) | [3953](https://github.com/NuGet/NuGet.Client/pull/3953) | NuGet.exe 팩 성능 문제가 있습니다. 상대 경로 - [#5016](https://github.com/NuGet/Home/issues/5016)
[2016년 10월 20일](https://github.com/marcin-krystianc) | [3940](https://github.com/NuGet/NuGet.Client/pull/3940) | CPVM - 그래프 보행 알고리즘의 동시성 문제 - [#10598](https://github.com/NuGet/Home/issues/10598)
[josesimoes](https://github.com/josesimoes) | [3943](https://github.com/NuGet/NuGet.Client/pull/3943) | nuget CLI용 supportedProjectExtensions 목록에 nfproj 프로젝트 형식을 추가합니다. - [#10562](https://github.com/NuGet/Home/issues/10562)

## <a name="feedback-welcome"></a>피드백 환영

Microsoft는 사용자의 의견을 소중하게 생각합니다.  이 릴리스에 문제가 있는 경우 [GitHub 문제를](https://github.com/NuGet/Home/issues) 확인하고 기존 문제에 대한 개발자 Community [Visual Studio.](https://developercommunity.visualstudio.com/)  NuGet 내의 새로운 문제는 [GitHub 문제를](https://github.com/NuGet/Home/issues/new)보고하세요.
일반적인 NuGet 환경 문제의 경우 도움말 > [문제 보고에서](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) 즐겨 찾는 IDE에 있는 **문제 보고** 옵션을 통해 알려주세요.
