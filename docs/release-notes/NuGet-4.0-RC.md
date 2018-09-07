---
title: NuGet 4.0 RC 릴리스 정보
description: NuGet 4.0 RC에 대한 릴리스 정보(알려진 문제, 버그 수정, 추가된 기능 및 DCR 포함)
author: karann-msft
ms.author: karann
ms.date: 02/03/2017
ms.topic: conceptual
ms.reviewer: ananguar
ms.openlocfilehash: 2d0bb6356c0a20843bdc884b68f5f61838b82e73
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549248"
---
# <a name="nuget-40-rc-release-notes"></a>NuGet 4.0 RC 릴리스 정보

[NuGet 3.5 RTM 릴리스 정보](../release-notes/nuget-3.5-RTM.md)

[Visual Studio 2017용 NuGet 4.0 RC](http://blog.nuget.org/20161121/introducing-nuget4.0)는 .NET Core 시나리오에 대한 지원 추가, 주요 고객 의견 처리 및 다양한 시나리오의 성능 향상에 중점을 둡니다. 이 릴리스에는 PackageReference 지원, MSBuild 대상 NuGet 명령, 백그라운드 패키지 복원 등과 같이 향상된 몇 가지 기능이 제공됩니다.

## <a name="bug-fixes"></a>버그 수정

- `dotnet pack --version-suffix foo` 동작 변경 - [#3838](https://github.com/NuGet/Home/issues/3838)

- VS "15" 컴퓨터에서만 nuget.exe restore가 실패합니다. - [#3834](https://github.com/NuGet/Home/issues/3834)

- .NETCore 파일 - 새 프로젝트를 복원하는 동안 빌드를 차단해야 합니다. - [#3780](https://github.com/NuGet/Home/issues/3780)

- VS2015에서 VS "15"로 마이그레이션된 ASP.NET Core 웹앱을 복원할 수 없습니다. - [#3773](https://github.com/NuGet/Home/issues/3773)

- [테스트 실패] PM UI에서 'jQuery 유효성 검사' 패키지를 제거할 수 없습니다. - [#3755](https://github.com/NuGet/Home/issues/3755)

- 패키지가 UWP `project.json`에 설치되면 부모 프로젝트도 복원해야 합니다. - [#3731](https://github.com/NuGet/Home/issues/3731)

- NuGet 대상을 수정하여 패키지 원본을 보통 대신 높은 수준의 세부 정보 표시로 기록합니다. - [#3719](https://github.com/NuGet/Home/issues/3719)

- dotnet
  - dotnetcore pack3에는 기본적으로 XML 문서가 포함되어야 합니다. - [#3698](https://github.com/NuGet/Home/issues/3698)

- 패키지가 없는 원본이 처음이고 모든 원본이 선택되면 UI에서 일괄 업데이트가 실패합니다. - [#3696](https://github.com/NuGet/Home/issues/3696)

- Nuget pack 명령에 모든 파일이 포함되지 않습니다. - [#3678](https://github.com/NuGet/Home/issues/3678)

- OOM 문제 - [#3661](https://github.com/NuGet/Home/issues/3661)

- 자산 파일의 ProjectFileDependencyGroups 섹션에는 프로젝트의 라이브러리 이름을 사용해야 합니다. - [#3611](https://github.com/NuGet/Home/issues/3611)

- "dotnet restore" 및 디렉터리 재귀 - [#3517](https://github.com/NuGet/Home/issues/3517)

- Restore3 실패는 오류 대신 경고로 기록됩니다. - [#3503](https://github.com/NuGet/Home/issues/3503)

- TFS 문제: 작업 영역에서 [file] 항목을 찾을 수 없거나 사용자에게 해당 항목에 액세스할 수 있는 권한이 없습니다. - [#2805](https://github.com/NuGet/Home/issues/2805)

- VS 빠른 시작 검색 상자에 "nuget <packagename>"을 입력하면 "nuget " 접두사가 유지됩니다. - [#2719](https://github.com/NuGet/Home/issues/2719)

- System.Xml.XmlException: Core Properties 파트에 인식할 수 없는 루트 요소가 있습니다. 줄 2, 위치 2 - [#2718](https://github.com/NuGet/Home/issues/2718)

- 텍스트 필드에 이스케이프된 &lt; 또는 &gt;가 있는 `.nuspec`은 더 이상 빌드되지 않습니다. - [#2651](https://github.com/NuGet/Home/issues/2651)

- nuget.exe delete는 자격 증명을 묻지 않습니다(비대화형 모드입니다) - [#2626](https://github.com/NuGet/Home/issues/2626)

- nuget.exe delete는 의미가 없더라도 로컬 원본에 대한 API 키에 대해 경고합니다. - [#2625](https://github.com/NuGet/Home/issues/2625)

- EF -pre 패키지를 설치할 때 오류 경험이 부족합니다. - [#2566](https://github.com/NuGet/Home/issues/2566)

- 패키지 관리자에서 선택 항목을 변경한 후 시도하면 Visual Studio에서 작동이 중단됩니다. - [#2551](https://github.com/NuGet/Home/issues/2551)

- dotnet
  - 유동적인 버전이 사용되는 경우 dotnetcore restore에서 단순 목록 로컬 리포지토리에 대해 대/소문자를 구분하는 ID 조회를 수행합니다. - [#2516](https://github.com/NuGet/Home/issues/2516)

- V2 피드에 대한 nuget.exe delete가 중단됩니다. - [#2509](https://github.com/NuGet/Home/issues/2509)

- nuget.exe push 시간 제한에 더 나은 오류 메시지가 필요합니다. - [#2503](https://github.com/NuGet/Home/issues/2503)

- 적절한 가져오기가 없는 도구 복원이 자동으로 실패합니다. - [#2462](https://github.com/NuGet/Home/issues/2462)

- nuget.org에서 설치하는 경우에도 개인 피드가 있을 때 NuGet에서 자격 증명을 입력하라는 메시지가 표시됩니다. - [#2346](https://github.com/NuGet/Home/issues/2346)

- ApplicationInsights 2.0 패키지가 나열되었지만 아직 존재하지 않습니다. - [#2317](https://github.com/NuGet/Home/issues/2317)

- VS "15" 미리 보기 5 분기의 UIDelay - [#3500](https://github.com/NuGet/Home/issues/3500)

- UWP 빌드 시 복원에 대한 첫 번째 OnBuild 이벤트가 누락되어 있습니다. - [#3489](https://github.com/NuGet/Home/issues/3489)

- PowerShell5에서 EntityFramework 설치가 중단됩니까? - [#3312](https://github.com/NuGet/Home/issues/3312)

- 자세한 로깅에 원본을 추가합니다(3.5에 대한 고려 사항) - [#3294](https://github.com/NuGet/Home/issues/3294)

- NoCache 매개 변수가 NuGet 클라이언트 버전 3.4 이상에서 적용되지 않습니다. - [#3074](https://github.com/NuGet/Home/issues/3074)

- 자격 증명 공급자가 VS에서 로드하지 못하는 경우 NuGet을 중단하면 안됩니다. - [#2422](https://github.com/NuGet/Home/issues/2422)

## <a name="features"></a>기능

- x86을 실행하도록 CI를 설정합니다. - [#3868](https://github.com/NuGet/Home/issues/3868)

- 자동 복구 3/3: UI를 차단하지 않습니다. - [#3658](https://github.com/NuGet/Home/issues/3658)

- 자동 복원 2/3: 지정에 대한 백그라운드 복원을 수행합니다. - [#3657](https://github.com/NuGet/Home/issues/3657)

- 빌드 동작과 일치하도록 프로젝트 참조를 복원합니다(recurse). - [#3615](https://github.com/NuGet/Home/issues/3615)

- VS "15"에서 DPL - minbar를 지원합니다. - [#3614](https://github.com/NuGet/Home/issues/3614)

- 설정 파일을 Program Files 폴더로 이동합니다. - [#3613](https://github.com/NuGet/Home/issues/3613)

- 생성된 props 및 targets 복원에는 대상 간 참가 지원이 필요합니다. - [#3496](https://github.com/NuGet/Home/issues/3496)

- PackageTargetFallback에 대해 NuGet 복원(종종 imports라고 함)을 지원합니다. - [#3494](https://github.com/NuGet/Home/issues/3494)

- ToolsRef 구현 - [#3472](https://github.com/NuGet/Home/issues/3472)

- RID에 대한 restore3 - [#3465](https://github.com/NuGet/Home/issues/3465)

- PackageRefs 추가/제거/업데이트를 지원하는 NuGet UI - [#3457](https://github.com/NuGet/Home/issues/3457)

- 자동 복원 1/3: 프로젝트 복원 캐싱 정보를 통해 지정 API를 구현합니다. - [#3456](https://github.com/NuGet/Home/issues/3456)

- [0] NuGet restore 작업 및 대상 - [#2994](https://github.com/NuGet/Home/issues/2994)

- [1] MSBuild에서 솔루션 수준 복원 사용 - [#2993](https://github.com/NuGet/Home/issues/2993)

- Visual Studio에서 자격 증명 공급자 공용 확장성 지원 - [#2909](https://github.com/NuGet/Home/issues/2909)

- 재귀적 nuget restore - [#2533](https://github.com/NuGet/Home/issues/2533)

- dev15에서 Microsoft.TeamFoundation.Client를 로드할 수 없습니다. VS "15" 미리 보기에서 Microsoft.TeamFoundation.Client 버전을 15.0으로 업데이트해야 합니다. - [#2392](https://github.com/NuGet/Home/issues/2392)

- VS "15" 미리 보기에서 C++ UWP 프로젝트에 C++ 패키지를 설치할 수 없습니다. - [#2369](https://github.com/NuGet/Home/issues/2369)

- Nupkg에서 \buildCrossTargeting\ 폴더를 지원하고 "대상으로 교차 지정된(crosstargeting)" MSBuild 범위에 대한 `.targets` / `.props`를 가져와야 합니다. - [#3499](https://github.com/NuGet/Home/issues/3499)

- ToolsReference 디자인 - [#3462](https://github.com/NuGet/Home/issues/3462)

- `.csproj`에서 PackageReferences를 통한 복원을 지원하도록 NuGet UI를 수정합니다. - [#3455](https://github.com/NuGet/Home/issues/3455)

- VS 패키지 관리자 설정에 캐시 지우기 단추를 추가합니다. - [#3289](https://github.com/NuGet/Home/issues/3289)

## <a name="dcrs"></a>DCR

- 자동 복원이 수행되는 동안 솔루션 복원이 차단되어야 합니다. - [#3797](https://github.com/NuGet/Home/issues/3797)

- NuGet 패키지 관리자 UI에서 설치한 NetCore는 패키지에서 지원하는 UI 대신 모든 TFM에 설치됩니다. - [#3721](https://github.com/NuGet/Home/issues/3721)

- 복원 지정자 API도 DotNetCliToolsReferences를 지원해야 합니다. - [#3702](https://github.com/NuGet/Home/issues/3702)

- VS "15" vsix를 SystemComponent로 표시합니다. - [#3700](https://github.com/NuGet/Home/issues/3700)

- 참조하는 MS.VS.Services.Client에서 MS.VS.Services.Client.Interactive로 마이그레이션합니다. - [#3670](https://github.com/NuGet/Home/issues/3670)

- $(RestoreLegacyPackagesDirectory)는 복원을 통해 프로젝트 수준에서 적용되어야 합니다. - [#3618](https://github.com/NuGet/Home/issues/3618)

- 단일 TargetFramework를 사용하여 프로젝트를 복원하는 경우 props 조건이 되어서는 안됩니다. - [#3588](https://github.com/NuGet/Home/issues/3588)

- dotnet
  - dotnetcore restore3 foo.csproj는 projectref 종속성을 따르고 이를 복원해야 합니다. 빌드하는 경우도 마찬가지입니다. - [#3577](https://github.com/NuGet/Home/issues/3577)

- "type": "platform" 종속성이 잠금 파일에서 "type":"package"로 표시됩니다. - [#2695](https://github.com/NuGet/Home/issues/2695)

- nuget.exe 자세한 정보 표시 모드에 다운로드 URL이 표시되어야 합니다. - [#2629](https://github.com/NuGet/Home/issues/2629)

- NuGet xplat을 Microsoft.NetCore.App 및 netcoreapp1.0으로 이동합니다. - [#2483](https://github.com/NuGet/Home/issues/2483)

- push - 명령줄에서 푸시할 때 기호 서버를 재정의할 수 있어야 합니다. - [#2348](https://github.com/NuGet/Home/issues/2348)

- 전역 패키지 경로를 찾는 코드를 통합합니다. - [#2296](https://github.com/NuGet/Home/issues/2296)

- suppressParent보다 더 나은 이름이 필요합니다. - [#2196](https://github.com/NuGet/Home/issues/2196)

- MSBuild 프로젝트에 사용할 `project.json` 종속성 이름을 결정합니다. - [#1914](https://github.com/NuGet/Home/issues/1914)

- NuGet.Core에 SemVer 2.0.0 지원을 추가합니다. - [#3383](https://github.com/NuGet/Home/issues/3383)

- `.targets`가 있는 NuPkg 전이적 종속성을 MSBuild에서 사용할 수 있도록 허용합니다. - [#3342](https://github.com/NuGet/Home/issues/3342)

- 명령줄의 NuGet restore는 VS보다 훨씬 느립니다. - [#3330](https://github.com/NuGet/Home/issues/3330)

- 패키지 ID 및 버전 비교에서 대/소문자를 구분하지 않습니다. - [#2522](https://github.com/NuGet/Home/issues/2522)

- NoCache 옵션이 `packages.config` 기반 복원/설치(GlobalPackagesFolder)에서 작동하지 않습니다. - [#1406](https://github.com/NuGet/Home/issues/1406)

- FindPackageByIdResource 리소스에는 기본 캐시 컨텍스트와 로거가 필요합니다. - [#1357](https://github.com/NuGet/Home/issues/1357)
