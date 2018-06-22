---
title: NuGet 3.5 베타 릴리스 정보
description: 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr를 포함 하 여 NuGet 3.5에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cdb540229cae0e6e952ac2a0c00c8801ccbbb28d
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822593"
---
# <a name="nuget-35-release-notes"></a>NuGet 3.5 릴리스 정보

[NuGet 3.5 RC 릴리스 정보](../release-notes/nuget-3.5-RC.md) | [NuGet 4.0 RC 릴리스 정보](../release-notes/nuget-4.0-RC.md)

## <a name="bug-fixes"></a>버그 수정

* 팩 모노-에 MSBuild 14.1를 사용 하지 않는 [#3550](https://github.com/NuGet/Home/issues/3550)

* 업데이트 탭 선택 현재 설치 된 버전-대신 업데이트할 사용 가능한 최신 버전을 선택 하지 않습니다 [#3498](https://github.com/NuGet/Home/issues/3498)

* MyGet 피드에 개인 v2를 인증 하 고 "더 많은 결과 x 표시"를 클릭 한 후 충돌 해결- [#3469](https://github.com/NuGet/Home/issues/3469)

* 로그 메시지 UI에 대 한 반대 순서로 것 같습니다 [#3446](https://github.com/NuGet/Home/issues/3446)

* "지정한 경로 형식은 지원 되지 않습니다"-v3.4.4-Nuget 복원 throw [#3442](https://github.com/NuGet/Home/issues/3442)

* NuGet cmdLine 3.6 베타 기준으로 하지 않는-Prop 구성 릴리스-= [#3432](https://github.com/NuGet/Home/issues/3432)

* -대규모 프로젝트에 Nuget IKVM 느린 설치 [#3428](https://github.com/NuGet/Home/issues/3428)

* nuget.exe 셀프 유지에 업데이트 자체-업데이트 [#3395](https://github.com/NuGet/Home/issues/3395)

* UNC 공유에서 3.5 설치/복원에 3.4.4-에서 회귀 성능 [#3355](https://github.com/NuGet/Home/issues/3355)

* Moq net451 프로젝트-에 대 한 패키지 관리 UI에서에서 설치 하는 동안 오류가 발생 했습니다. [#3349](https://github.com/NuGet/Home/issues/3349)

* 솔루션 수준에서 설치 탭은 패키지의 버전-표시 되지 않습니다 [#3339](https://github.com/NuGet/Home/issues/3339)

* xproj `project.json` 설치 됨 탭에서 업데이트 상태-손실 [#3303](https://github.com/NuGet/Home/issues/3303)

* 에 NuGet 팩 `.csproj` 에 빈 파일 요소를 무시 `.nuspec` 파일- [#3257](https://github.com/NuGet/Home/issues/3257)

* IIS에서 호스팅되는 웹 사이트 프로젝트 실패-복원 하면 [#3235](https://github.com/NuGet/Home/issues/3235)

* 자격 증명 v3 끝점에서 v 2-리디렉션하면 Nuget.Config에서 검색 되지 [#3179](https://github.com/NuGet/Home/issues/3179)

* NuGet 팩 휴대용 어셈블리 메타 데이터-검색할 때 어셈블리 해결 되지 않은 [#3128](https://github.com/NuGet/Home/issues/3128)

* Nuget을 찾을 수 없습니다 `msbuild.exe` 모노-에 [#3085](https://github.com/NuGet/Home/issues/3085)

* nuget.exe 팩 번호-로 시작 하는 시험판 태그를 허용 하지 않습니다. [#1743](https://github.com/NuGet/Home/issues/1743)

* VS2015E-에서 nuget 패키지 설치 실패 [#1298](https://github.com/NuGet/Home/issues/1298)

* allowedversions가 필터링-솔루션 수준에서 작동 하지 [#333](https://github.com/NuGet/Home/issues/333)

* Restore는 임의로 동일한 항목와 함께 실패 키가 이미 추가 되었습니다. - [#2646](https://github.com/NuGet/Home/issues/2646)

* Nuget.Common에 설치할 수 없습니다. `.csproj`  -  [#2635](https://github.com/NuGet/Home/issues/2635)

* -각 ID에 대해 두 번 FindPackagesById 라고 V2 원본을 검색 하려면 UI를 사용 하는 경우 [#2517](https://github.com/NuGet/Home/issues/2517)

* 패키지는 프로젝트-에 종속 될 수 없습니다 [#2490](https://github.com/NuGet/Home/issues/2490)

* nuget.exe 팩-Exclude 문서화 되어 있지만 지원 되지 않습니다- [#2284](https://github.com/NuGet/Home/issues/2284)

* 오류와 함께 문제 때 메시지의 '콘텐츠 ' 파일 섹션 `.nuspec` 잘못 되었습니다. [#1686](https://github.com/NuGet/Home/issues/1686)

* 푸시 전체 패키지 두 번으로 인증 된 패키지 소스에 항상 보냅니다 [#1501](https://github.com/NuGet/Home/issues/1501)

* 프로젝트 nuget.exe 업데이트 *.csproj 호출에 없을 때 제공한 없습니다 정보가 `packages.config`  -  [#1496](https://github.com/NuGet/Home/issues/1496)

* `packages.config` 복원-V2 원본의 5xx 상태 코드에 다시 시도 하지 [#1217](https://github.com/NuGet/Home/issues/1217)

* 파일 src에 이중 점 `.nuspec` 작동 하지 않는- [#2947](https://github.com/NuGet/Home/issues/2947)

* CoreCLR 복원-암호화를 사용한 피드를 무시 하는 데 필요한 [#2942](https://github.com/NuGet/Home/issues/2942)

* nuget.exe 푸시-올바르게 하지 자격 증명을 물을-403 처리 [#2910](https://github.com/NuGet/Home/issues/2910)

* NuGet 패키지 관리자를 통해이 업데이트에서 속성을 제거는 `project.json`  -  [#2888](https://github.com/NuGet/Home/issues/2888)

* NuGet.PackageManagement.VisualStudio "NuGet.TeamFoundationServer14" 하지만 DLL 이름이 "NuGet.TeamFoundationServer-"으로 변경 되었음을 로드 하려고 [#2857](https://github.com/NuGet/Home/issues/2857)

* UI 새로 표시 되지 않으면 패키지 관리자 버전-업데이트 [#2828](https://github.com/NuGet/Home/issues/2828)

* 업데이트 패키지, 패키지 id를 사용 하려는 package.version-대신 버전 [#2771](https://github.com/NuGet/Home/issues/2771)

* nuget 복원 csproj 프로젝트 nuget를 사용할 수 없는 경우 오류 해야 (`packages.config` 또는 `project.json`)- [#2766](https://github.com/NuGet/Home/issues/2766)

* TFS 오류 "[파일] 작업 영역에서 찾을 수 없거나 액세스할 수 있는 권한이 없습니다" 하는 동안 업그레이드 또는 제거할 솔루션/프로젝트-TFS 소스 제어에 바인딩되어 있을 때 [#2739](https://github.com/NuGet/Home/issues/2739)

* 업데이트 패키지에는--대상 패키지의 종속성을 이해 하지 못합니다 [#2724](https://github.com/NuGet/Home/issues/2724)

* Nuget 패키지 관리자 UI 작업-에 대 한 로그 자세한 표시 수준을 설정할 수 없으므로 [#2705](https://github.com/NuGet/Home/issues/2705)

* nuget 구성이 잘못 되었습니다. VS 2015 VSIX (v3.4.3)- [#2667](https://github.com/NuGet/Home/issues/2667)

* DefaultPushSource `NuGetDefaults.Config` (`ProgramData\NuGet`) 작동 하지 않는- [#2653](https://github.com/NuGet/Home/issues/2653)

* nuget 3.4.3 릴리스-패키지 빌드-에서 null 일 수 없습니다 값을 가져오는 [#2648](https://github.com/NuGet/Home/issues/2648)

* VSTS 피드-에 대 한 복원 Nuget.Config에서 저장 된 자격 증명을 사용 하지 않는 [#2647](https://github.com/NuGet/Home/issues/2647)

* [dotnet 복원]-configfile는 대신 cmd dir-프로젝트 디렉터리에 상대적 [#2639](https://github.com/NuGet/Home/issues/2639)

* 버전 비교 코드-의 과도 한 할당 [#2632](https://github.com/NuGet/Home/issues/2632)

* 이중 쓰기-병렬 원인에 동일한 설치 하는 동안 nuget.exe의 여러 인스턴스 패키지 [#2628](https://github.com/NuGet/Home/issues/2628)

* -다중 프로젝트 작업에 대 한 종속성 정보가 캐시 되지 않으면 [#2619](https://github.com/NuGet/Home/issues/2619)

* 설치 및 다운로드 패키지의 패키지 폴더를 먼저-확인 하지 않고 업데이트 [#2618](https://github.com/NuGet/Home/issues/2618)

* 패키지 소스 목록에 수식이 있으면 UI 통해 패키지 소스를 추가할 수 없습니다 (NuGet 3.4.x)- [#2617](https://github.com/NuGet/Home/issues/2617)

* 디자인 타임 외관-에 의존 하는 패키지를 설치 하려고 하면 오류가 있을 경우 잘못 해석 [#2594](https://github.com/NuGet/Home/issues/2594)

* 첫 번째 소스-시도 PackageManager "All"을 설정 하는 콘솔에서 패키지를 설치 [#2557](https://github.com/NuGet/Home/issues/2557)

* 압축을 푼 하지 최신 베타 ModernHttpClient- [#2518](https://github.com/NuGet/Home/issues/2518)

* 3.4.1-빌드된 자체 NuGet이 포함 된 시작 시 VS2015 크래시 [#2419](https://github.com/NuGet/Home/issues/2419)

* Update 명령은 i 수 이므로...-하도록 요청 하는 경우 좀 더 자세한 정보 수 [#2418](https://github.com/NuGet/Home/issues/2418)

* 로컬에서 빌드한 VSIX CI 빌드와 동일한 Dll 및 파일 있어야 합니다. - [#2401](https://github.com/NuGet/Home/issues/2401)

* 빌드-에 NuGet 다운 그레이드 경고를 수정 [#2396](https://github.com/NuGet/Home/issues/2396)

* 영구적으로 차단 된 패키지 소스 (3 시간) 인증에 실패할 [#2362](https://github.com/NuGet/Home/issues/2362)

* 패키지 콘텐츠 인수와 함께 피드 nuget v3.3 +에서 패키지를 설치할 때 제대로 복원 되지-NoCache 패키지에 포함 된 경우 `.nupkg` 파일- [#2354](https://github.com/NuGet/Home/issues/2354)

* 모든 패키지 소스 하지만 1 원본에서 누락 된 패키지와 함께 Nuget 설치 실패- [#2322](https://github.com/NuGet/Home/issues/2322)

* [PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll!NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+*lt;&gt;c__DisplayClass_0+&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)

* 단일 소스 권한 부여-에 실패 하는 경우 블록 설치 [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` 범위는-IncludeReferencedProjects 버전-를 재정의 해야 하는 버전 [#1983](https://github.com/NuGet/Home/issues/1983)

* 업데이트 패키지는 super-"를 수집 하려는 종속성 정보"-느린 [#1909](https://github.com/NuGet/Home/issues/1909)

* 날카로운 다운 그레이드 NuGet 패키지 될 때 일괄 처리의 종속성-업데이트 [#1903](https://github.com/NuGet/Home/issues/1903)

* nuget.exe 업데이트 어셈블리의 강력한 이름 및 개인 특성을 삭제합니다. - [#1778](https://github.com/NuGet/Home/issues/1778)

* "DefaultPushSource"-에 대 한 상대 파일 경로 [#1746](https://github.com/NuGet/Home/issues/1746)

* 해결 프로그램 실패 메시지-개선 [#1373](https://github.com/NuGet/Home/issues/1373)

* v 3에서 업데이트 패키지-지정된 된 소스에 없는 패키지와 함께 실패 [#1013](https://github.com/NuGet/Home/issues/1013)

* 패키지 원본에 대 한 상대 경로 사용 하는 것은 사용 하지 않으려면-문제가 [#865](https://github.com/NuGet/Home/issues/865)

* 간접 종속성으로 더 낮은 버전 요구 사항-이미 있는 경우 프로젝트에서 생성 한 NUPKG 파일에 대 한 종속성이 없습니다 [#759](https://github.com/NuGet/Home/issues/759)

* 프로젝트를 삭제 하면 해당 UI 창 닫지만, 프로젝트 이름 바꾸기 UI 창 바뀌지 않습니다. 프로젝트 이름 바꾸기 및 프로젝트 제거 이벤트-PMC 수신 대기 하도록 참고 [#670](https://github.com/NuGet/Home/issues/670)

* [버드 웹 작업] Razor v3 WSP 만들기 중단- [#3241](https://github.com/NuGet/Home/issues/3241)

* "패키지에 여러 nuspec 파일이 들어 있습니다."와 함께 특정 패키지의 설치/복원 실패 - [#3231](https://github.com/NuGet/Home/issues/3231)

* Id 소문자로 & `packages.config` 시나리오- [#3209](https://github.com/NuGet/Home/issues/3209)

* [beta2 3.5] 패키지 복원이 실패-"레거시" 패키지를 복원 하도록 [#3208](https://github.com/NuGet/Home/issues/3208)

* nuget 팩.tt 파일 어떠한-콘텐츠 폴더에 강제적으로 추가 [#3203](https://github.com/NuGet/Home/issues/3203)

* 파일에 관련 경고를 생성 하는 ASP.NET 웹 앱의 업데이트 패키지: 소스- [#3194](https://github.com/NuGet/Home/issues/3194)

* nuget 팩 csproj (으로 `project.json`) packOptions 및 소유자-JSON 파일에 없는 경우 충돌 [#3180](https://github.com/NuGet/Home/issues/3180)

* 에 대 한 nuget 팩 `project.json` 요약, 작성자, 등-소유자와 같은 packOptions 태그를 무시 [#3161](https://github.com/NuGet/Home/issues/3161)

* NullReferenceException NuGet.Packaging.PhysicalPackageFile.GetStream-통해 [#3160](https://github.com/NuGet/Home/issues/3160)

* 출력에서 종속성을 무시 하는 NuGet 팩 `.nuspec` 에 대 한 `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* 프로젝트 손상된 상태로-남게 되므로 롤백으로 여러 패키지를 업데이트할 [#3139](https://github.com/NuGet/Home/issues/3139)

* Netstandard 프로젝트-에 대 한 콘텐츠 파일에서 추가 되지 않습니다 [#3118](https://github.com/NuGet/Home/issues/3118)

* .NET을 대상으로 하는 라이브러리 패키지할 수 없습니다. 표준 올바르게- [#3108](https://github.com/NuGet/Home/issues/3108)

* 파일-새 프로젝트 > v s 2015 및 Dev15-클래스 라이브러리 (이식 가능) 프로젝트 실패-> [#3094](https://github.com/NuGet/Home/issues/3094)

* NuGet 오류-1.0.0-*-올바른 버전 문자열이 아닙니다. [#3070](https://github.com/NuGet/Home/issues/3070)

* Find-package 실패를 표시 하지만 Install-package works- [#3068](https://github.com/NuGet/Home/issues/3068)

* 오류 때 dev15-에 "Install-package jquery.validation" [#3061](https://github.com/NuGet/Home/issues/3061)

* 잘못 된 대상 경로-xproj nuget 팩이 선택은 기본값인 [#3060](https://github.com/NuGet/Home/issues/3060)

* 설치 된 VS 2015 업데이트 3 버전 3.5.0 오류가 발생 합니다. NuGet을 사용 하는 VS에서 [#3053](https://github.com/NuGet/Home/issues/3053)

* "Packages.config에 의해 차단" `project.json` (UWP, 통합 하는 사항 빌드) 프로젝트- [#3046](https://github.com/NuGet/Home/issues/3046)

* dotnet cli preview2 003121 공식 preview2 빌드는 빌드 스크립트에서 설치를 업데이트 합니다. - [#3045](https://github.com/NuGet/Home/issues/3045)

* 패키지 관리자 UI: 패키지를 업데이트 한 후 새 버전을 표시 하지 않는- [#3041](https://github.com/NuGet/Home/issues/3041)

* Delete 명령줄에-ApiKey 읽기/에서 전송 되지 않습니다 3.5.0-beta- [#3037](https://github.com/NuGet/Home/issues/3037)

* 잘못 된 문자열: 안정판 패키지에는 시험판 종속성 없어야 합니다. - [#3030](https://github.com/NuGet/Home/issues/3030)

* OptimizedZipPackage 캐시-빈 폴더를 둡니다 [#3029](https://github.com/NuGet/Home/issues/3029)

* (Net46 및 windows 10) PCL 프로젝트 get NullRef 예외를 만듭니다. - [#3014](https://github.com/NuGet/Home/issues/3014)

* 더 높은 버전 allowedversions가 제약 조건-에 의해 제한 되는 경우 Nuget 업데이트 알림 메시지를 제공 해야 [#3013](https://github.com/NuGet/Home/issues/3013)

* Nuget v3 복원 문제- [#2891](https://github.com/NuGet/Home/issues/2891)

* 자격 증명 플러그 인) 종료 되었습니다 (오류-1 /-여러 소스가 포함 된 자격 증명 공급자를 사용 하는 경우 패키지 오류 다운로드 [#2885](https://github.com/NuGet/Home/issues/2885)

* `project.json` nuget 복원 하면 변경-항목이 없을 경우 다시 컴파일이 [#2817](https://github.com/NuGet/Home/issues/2817)

* 기호 패키지가 현재까지 여야 설치 또는 업데이트-에서 사용할 [#2807](https://github.com/NuGet/Home/issues/2807)

* VS repositoryPath의 환경 변수를 지원 하지 않습니다 (nuget.exe은)- [#2763](https://github.com/NuGet/Home/issues/2763)

* 내게 필요한 옵션 기능에 대 한 패키지 관리자 UI에서 레이블이 지정 되지 않은 Uielement 레이블을 [#2745](https://github.com/NuGet/Home/issues/2745)

* 하이픈으로 연결 된 프로필을 통해 휴대용 프레임 워크는 거부 됩니다. - [#2734](https://github.com/NuGet/Home/issues/2734)

* NuGet 패키지 관리자를 수행 하는 세부 정보에 적용 되지 않는 패키지에 해당 옵션 목록 지우기 `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* nuget.exe 푸시/delete-API 키를 사용 하지 않으며 [#2627](https://github.com/NuGet/Home/issues/2627)

* 잠금 파일이-에서 잠긴된 속성을 제거 [#2379](https://github.com/NuGet/Home/issues/2379)

* NuGet 3.3.0 업데이트와 함께 실패 '... 추가 제약 조건에 정의 된 packages.config이이 작업을 방지 합니다.' - [#1816](https://github.com/NuGet/Home/issues/1816)

* 잘못 된 메시지-throw 존재 하지 않는 로컬 원본의 패키지 설치 [#1674](https://github.com/NuGet/Home/issues/1674)

* "업그레이드 가능" 필터 표시-버전 제약 조건을 위반 하는 업그레이드 [#1094](https://github.com/NuGet/Home/issues/1094)

* -기본 패키지를 업데이트할 수 없습니다 [#1291](https://github.com/NuGet/Home/issues/1291)


## <a name="features"></a>기능

* Nuget-추가한 참조에 false로 설정 CopyLocal 지원 [#329](https://github.com/NuGet/Home/issues/329)

* MSBuild 15-에 대 한 지원 nuget.exe [#1937](https://github.com/NuGet/Home/issues/1937)

* 팩 지원 합니다.`csproj` + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)

* 사용자 작업을 실행 중인 경우 사용자 작업 사용 안 함- [#1440](https://github.com/NuGet/Home/issues/1440)

* NuGet에 대 한 지원을 추가 해야 `runtimes/{rid}/nativeassets/{txm}/`  -  [#2782](https://github.com/NuGet/Home/issues/2782)

* NuGet에 누락 된 프레임 워크 호환성 추가 (이미에 있는 3.x) 2.x- [#2720](https://github.com/NuGet/Home/issues/2720)

* -대체 패키지 폴더에 대 한 지원 [#2899](https://github.com/NuGet/Home/issues/2899)

* 디자인 및 구현-도구 패키지를 지원 하기 위해 패키지 형식의 개념 [#2476](https://github.com/NuGet/Home/issues/2476)

* 경로를 가져오는 전역 패키지 폴더에 API 추가 [#2403](https://github.com/NuGet/Home/issues/2403)

* 팩-SemVer 2.0.0을 사용 하도록 설정 [#3356](https://github.com/NuGet/Home/issues/3356)

## <a name="dcrs"></a>DCR

* nuget.exe 푸시-timeout 매개 변수 작동 하지 않는- [#2785](https://github.com/NuGet/Home/issues/2785)

* 패키지 설명 텍스트를 선택할-수 [#1769](https://github.com/NuGet/Home/issues/1769)

* 활성화 되려면 nuget.exe `.props` 및 `.targets` 파일에 대 한 `.nuproj` 프로젝트 [#2711](https://github.com/NuGet/Home/issues/2711)

* 확장성 가져오기-프레임 워크를 비교 하는 API 추가 [#2633](https://github.com/NuGet/Home/issues/2633)

* 종속성 옵션을 사용 하는 경우 숨기기 `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* 인쇄 결과물에 자세한 출력-버전 헤더 nuget.exe [#1887](https://github.com/NuGet/Home/issues/1887)

* 사용자는 업그레이드/설치 기반 dotnet tfm PCL 발생할 수 문제-알 수 있도록 필요한 NuGet [#3138](https://github.com/NuGet/Home/issues/3138)

* 잘못 된 설치/업그레이드 tfm w / 프로젝트에 대 한 경고 "dotnet"-= [#3137](https://github.com/NuGet/Home/issues/3137)

* -업데이트에 대 한 ReShaper 및 NuGet의 성능 문제를 해결 [#3044](https://github.com/NuGet/Home/issues/3044)

* Netcoreapp11 및 netstandard17 지원-추가 [#2998](https://github.com/NuGet/Home/issues/2998)

* 에 대 한 활용 AssemblyMetadata 특성 `.nuspec` 토큰 바꾸기를- [#2851](https://github.com/NuGet/Home/issues/2851)
