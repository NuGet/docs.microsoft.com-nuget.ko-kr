---
title: NuGet 3.5 베타 릴리스 정보
description: 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr 포함 하는 NuGet 3.5에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d8df2cb51ddcc03fb3922d9e9def17b39fccc661
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550686"
---
# <a name="nuget-35-release-notes"></a>NuGet 3.5 릴리스 정보

[NuGet 3.5 RC 릴리스 정보](../release-notes/nuget-3.5-RC.md) | [NuGet 4.0 RC 릴리스 정보](../release-notes/nuget-4.0-RC.md)

## <a name="bug-fixes"></a>버그 수정

* 팩 mono-에서 MSBuild 14.1를 사용 하지 않는 [#3550](https://github.com/NuGet/Home/issues/3550)

* 업데이트 탭 선택 현재 설치 된 버전-대신 업데이트를 사용 가능한 최신 버전을 선택 하지 않을 [#3498](https://github.com/NuGet/Home/issues/3498)

* MyGet 피드에 개인 v2를 인증 하 고 "x 더 많은 결과 표시"를 클릭 한 후 충돌 해결- [#3469](https://github.com/NuGet/Home/issues/3469)

* 로그 메시지를 찾을 UI-에 대 한 반대 순서로 수 [#3446](https://github.com/NuGet/Home/issues/3446)

* "지정된 된 경로 형식은 지원 되지 않습니다"-v3.4.4-Nuget 복원 throw [#3442](https://github.com/NuGet/Home/issues/3442)

* NuGet 명령줄 3.6 베타는 인식 하지-Prop 구성 = 릴리스- [#3432](https://github.com/NuGet/Home/issues/3432)

* 대규모 프로젝트에서 Nuget IKVM 느린 설치 [#3428](https://github.com/NuGet/Home/issues/3428)

* nuget.exe-자체 유지에 자체적으로 업데이트-업데이트 [#3395](https://github.com/NuGet/Home/issues/3395)

* UNC 공유에서 설치/복원 3.5 성능이 회귀 3.4.4-에서 [#3355](https://github.com/NuGet/Home/issues/3355)

* Moq net451 프로젝트용-패키지 관리 UI에서에서 설치 하는 동안 오류가 발생 했습니다. [#3349](https://github.com/NuGet/Home/issues/3349)

* 솔루션 수준에서 설치 탭 패키지의 버전을 표시 하지 않습니다 [#3339](https://github.com/NuGet/Home/issues/3339)

* xproj `project.json` 설치 됨 탭에서 업데이트 상태가-손실 [#3303](https://github.com/NuGet/Home/issues/3303)

* NuGet pack `.csproj` 에서 빈 파일 요소를 무시 `.nuspec` 파일- [#3257](https://github.com/NuGet/Home/issues/3257)

* IIS에서 호스팅되는 웹 사이트 프로젝트 실패-복원 하면 [#3235](https://github.com/NuGet/Home/issues/3235)

* 자격 증명 v2-v3 엔드포인트 리디렉션할 때 Nuget.Config에서 검색 되지 [#3179](https://github.com/NuGet/Home/issues/3179)

* NuGet 팩 이식 가능한 어셈블리 메타 데이터-검색할 때 어셈블리를 해결 하지 못하는 [#3128](https://github.com/NuGet/Home/issues/3128)

* Nuget에서 찾을 수 없습니다 `msbuild.exe` Mono-에서 [#3085](https://github.com/NuGet/Home/issues/3085)

* nuget.exe 팩 번호-로 시작 하는 시험판 태그를 허용 하지 않습니다 [#1743](https://github.com/NuGet/Home/issues/1743)

* VS2015E-에서 nuget 패키지 설치 실패 [#1298](https://github.com/NuGet/Home/issues/1298)

* allowedVersions 필터링-솔루션 수준에서 작업 하지 [#333](https://github.com/NuGet/Home/issues/333)

* 동일한 항목을 사용 하 여 임의로 실패 하면 복원 키가 이미 추가 되었습니다. - [#2646](https://github.com/NuGet/Home/issues/2646)

* Nuget.Common에서 설치할 수 없습니다 `.csproj`  -  [#2635](https://github.com/NuGet/Home/issues/2635)

* FindPackagesById V2 원본을 검색 하려면 UI를 사용 하는 경우 각 ID에 대 한 두 번 라고 [#2517](https://github.com/NuGet/Home/issues/2517)

* 패키지 프로젝트-종속 될 수 없습니다 [#2490](https://github.com/NuGet/Home/issues/2490)

* -제외 설명 하지만 지원 되지-nuget.exe 팩 [#2284](https://github.com/NuGet/Home/issues/2284)

* 오류 문제가 때 메시지의 'contentFiles' 섹션 `.nuspec` 잘못 되었습니다 [#1686](https://github.com/NuGet/Home/issues/1686)

* 전체 패키지 두 번 사용 하 여 인증 된 패키지 소스-푸시 항상 보냅니다 [#1501](https://github.com/NuGet/Home/issues/1501)

* 정보가 없는 nuget.exe 업데이트 *.csproj 프로젝트 하는 동안 호출에 없는 경우 지정 된 된 `packages.config`  -  [#1496](https://github.com/NuGet/Home/issues/1496)

* `packages.config` 복원-V2 원본의 5xx 상태 코드에 다시 시도 하지 않습니다 [#1217](https://github.com/NuGet/Home/issues/1217)

* 파일 src에서 두 개의 점 `.nuspec` 작동 하지 않음- [#2947](https://github.com/NuGet/Home/issues/2947)

* 암호화를 사용 하 여 피드를 무시 해야 하는 CoreCLR 복원 [#2942](https://github.com/NuGet/Home/issues/2942)

* nuget.exe push-올바르게 하지 자격 증명을 물을-403 처리 [#2910](https://github.com/NuGet/Home/issues/2910)

* 패키지 관리자를 통해 NuGet 업데이트의 속성을 제거 합니다 `project.json`  -  [#2888](https://github.com/NuGet/Home/issues/2888)

* NuGet.PackageManagement.VisualStudio "NuGet.TeamFoundationServer14" 하지만 DLL 이름이 "NuGet.TeamFoundationServer"-로 변경 하는 로드 하려고 [#2857](https://github.com/NuGet/Home/issues/2857)

* 패키지 관리자 UI 새로 표시 되지 않으면 업데이트 된 버전- [#2828](https://github.com/NuGet/Home/issues/2828)

* packageid, 사용 하려는 업데이트 패키지 버전 package.version-대신 [#2771](https://github.com/NuGet/Home/issues/2771)

* nuget 복원 csproj 프로젝트는 nuget을 사용 하지 않는 경우 오류를 해야 합니다 (`packages.config` 나 `project.json`)- [#2766](https://github.com/NuGet/Home/issues/2766)

* TFS 오류 "[파일] 작업 영역에서 찾을 수 없거나 액세스할 수 있는 권한이 없습니다" 하는 동안 업그레이드 또는 제거 솔루션/프로젝트-TFS 소스 제어에 바인딩되어 있을 때 [#2739](https://github.com/NuGet/Home/issues/2739)

* 업데이트 패키지에는--대상 패키지에 대 한 종속성 오지 [#2724](https://github.com/NuGet/Home/issues/2724)

* Nuget 패키지 관리자 UI 작업에 대 한 로그의 자세한 정도 수준을 설정할 수 없으므로 [#2705](https://github.com/NuGet/Home/issues/2705)

* nuget 구성이 올바르지 않음-VS 2015 VSIX (v3.4.3)- [#2667](https://github.com/NuGet/Home/issues/2667)

* 에 DefaultPushSource `NuGetDefaults.Config` (`ProgramData\NuGet`) 작동 하지 않음- [#2653](https://github.com/NuGet/Home/issues/2653)

* nuget 3.4.3 릴리스에 패키지 빌드-null 일 수 없습니다 가치를 창출 [#2648](https://github.com/NuGet/Home/issues/2648)

* VSTS 피드-에 대 한 복원 Nuget.Config에서 저장 된 자격 증명을 사용 하지 않는 [#2647](https://github.com/NuGet/Home/issues/2647)

* [dotnet 복원]-configfile cmd dir-대신 프로젝트 디렉터리에 상대적입니다 [#2639](https://github.com/NuGet/Home/issues/2639)

* 버전 비교 코드에서 과도 한 할당이 [#2632](https://github.com/NuGet/Home/issues/2632)

* Double 쓰기-병렬 원인에 동일한 설치 하려고 합니다. nuget.exe의 여러 인스턴스 패키지 [#2628](https://github.com/NuGet/Home/issues/2628)

* 다중 프로젝트 작업-에 대 한 종속성 정보가 캐시 되지 않으면 [#2619](https://github.com/NuGet/Home/issues/2619)

* 설치 하 고 패키지 폴더를 먼저 검사 하지 않고 다운로드 패키지를 업데이트할 [#2618](https://github.com/NuGet/Home/issues/2618)

* 패키지 원본 목록이 비어 있으면 UI 통해 패키지 소스를 추가할 수 없습니다 (NuGet 3.4.x)- [#2617](https://github.com/NuGet/Home/issues/2617)

* 디자인 타임 외관-종속 된 패키지를 설치 하려고 할 때 오류를 잘못 된 [#2594](https://github.com/NuGet/Home/issues/2594)

* 첫 번째 소스만-시도 PackageManager "All"을 설정 하는 콘솔에서 패키지를 설치 [#2557](https://github.com/NuGet/Home/issues/2557)

* 압축을 푸는 하지 최신 베타 버전 ModernHttpClient- [#2518](https://github.com/NuGet/Home/issues/2518)

* 시작할 때 자체 기본 제공 nuget 3.4.1-VS2015 크래시 [#2419](https://github.com/NuGet/Home/issues/2419)

* 업데이트 명령은 i 이므로...-되도록 요청 하는 경우에 다소 복잡 수 [#2418](https://github.com/NuGet/Home/issues/2418)

* CI 빌드 동일한 Dll 및 파일을 로컬에서 빌드한 VSIX 있어야 합니다. - [#2401](https://github.com/NuGet/Home/issues/2401)

* -빌드에서 NuGet 다운 그레이드 경고 해결 [#2396](https://github.com/NuGet/Home/issues/2396)

* -영원히 차단 됩니다 (3 시간) 패키지 원본 인증에 실패 하 [#2362](https://github.com/NuGet/Home/issues/2362)

* 인수를 사용 하 여 피드 nuget v3.3 이상에서 패키지를 설치 하는 경우 패키지 콘텐츠가 제대로 복원 되지 않습니다-패키지에 포함 된 경우 NoCache `.nupkg` 파일- [#2354](https://github.com/NuGet/Home/issues/2354)

* 모든 패키지 원본을 하지만 1 원본에서 누락 된 패키지를 사용 하 여 Nuget 설치 실패- [#2322](https://github.com/NuGet/Home/issues/2322)

* [PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll!NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+*lt;&gt;c__DisplayClass_0+&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)

* 단일 소스 권한-확인에 실패할 경우 요소를 설치 [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` 범위는-IncludeReferencedProjects 버전을 재정의 해야 하는 버전 [#1983](https://github.com/NuGet/Home/issues/1983)

* Update-package-"를 가져오는 동안 종속성 정보"-매우 느린 [#1909](https://github.com/NuGet/Home/issues/1909)

* 다운 그레이드 은폐 하는 NuGet 패키지 될 때 일괄 처리 종속성-업데이트 [#1903](https://github.com/NuGet/Home/issues/1903)

* nuget.exe 업데이트 어셈블리 강력한 이름 및 개인 특성을 삭제합니다. - [#1778](https://github.com/NuGet/Home/issues/1778)

* "DefaultPushSource"-에 대 한 상대 파일 경로 [#1746](https://github.com/NuGet/Home/issues/1746)

* 확인자 오류 메시지 개선 [#1373](https://github.com/NuGet/Home/issues/1373)

* v3에서 업데이트 패키지에 지정 된 원본에 없는 패키지를 사용 하 여 실패 [#1013](https://github.com/NuGet/Home/issues/1013)

* 패키지 원본에 대 한 상대 경로 사용 하는 것은 사용 하도록 문제가 [#865](https://github.com/NuGet/Home/issues/865)

* 더 낮은 버전 요구 사항-간접 종속성 이미 있는 경우 프로젝트에서 생성 한 NUPKG 파일에서 종속성 누락 [#759](https://github.com/NuGet/Home/issues/759)

* 프로젝트를 삭제 하면 해당 UI 창 닫지만, 프로젝트 이름 바꾸기 UI 창 바뀌지 않습니다. PMC 프로젝트 이름 바꾸기-프로젝트 제거 이벤트를 수신 대기 하는 참고 [#670](https://github.com/NuGet/Home/issues/670)

* [버드 웹 작업] 만들기 Razor v3 WSP 중단- [#3241](https://github.com/NuGet/Home/issues/3241)

* 특정 패키지의 설치/복원 "패키지 여러 nuspec 파일을 포함 합니다."와 함께 실패 - [#3231](https://github.com/NuGet/Home/issues/3231)

* Id에 소문자 & `packages.config` 시나리오- [#3209](https://github.com/NuGet/Home/issues/3209)

* [3.5-beta2] 패키지 복원 실패-"레거시" 패키지를 복원 하려면 [#3208](https://github.com/NuGet/Home/issues/3208)

* nuget 팩 어떤-콘텐츠 폴더에.tt 파일을 강제로 추가 [#3203](https://github.com/NuGet/Home/issues/3203)

* 파일 관련 경고를 생성 하는 ASP.NET 웹 앱의 업데이트 패키지: 소스- [#3194](https://github.com/NuGet/Home/issues/3194)

* nuget 팩 csproj (사용 하 여 `project.json`) packOptions 및 JSON 파일의 소유자 없는 경우 충돌 [#3180](https://github.com/NuGet/Home/issues/3180)

* 에 대 한 nuget 팩 `project.json` 요약, 작성자, 소유자 등-packOptions 태그를 무시 [#3161](https://github.com/NuGet/Home/issues/3161)

* NullReferenceException NuGet.Packaging.PhysicalPackageFile.GetStream-통해 [#3160](https://github.com/NuGet/Home/issues/3160)

* 출력의 종속성을 무시 하는 NuGet 팩 `.nuspec` 에 대 한 `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* 손상된 된 상태로-프로젝트 유지 rollback을 사용 하 여 여러 패키지를 업데이트 [#3139](https://github.com/NuGet/Home/issues/3139)

* Netstandard 프로젝트-에 대 한 ContentFiles에서 추가 되지 않습니다 [#3118](https://github.com/NuGet/Home/issues/3118)

* .NET을 대상으로 하는 라이브러리를 패키지할 수 없습니다 표준 제대로 [#3108](https://github.com/NuGet/Home/issues/3108)

* 파일-> 새 프로젝트-Dev15 VS2015에서 클래스 라이브러리 (이식 가능) 프로젝트 실패-> [#3094](https://github.com/NuGet/Home/issues/3094)

* nuGet 오류-1.0.0-* 문자열이 아닙니다. 유효한 버전- [#3070](https://github.com/NuGet/Home/issues/3070)

* Find-package 실패를 표시 하지만 Install-package 작동- [#3068](https://github.com/NuGet/Home/issues/3068)

* 오류 때-dev15에서 "Install-package jquery.validation" [#3061](https://github.com/NuGet/Home/issues/3061)

* xproj의 nuget pack은 잘못 된 대상 경로-기본값으로 [#3060](https://github.com/NuGet/Home/issues/3060)

* 설치 된 VS 2015 업데이트 3 버전 3.5.0 오류 발생-NuGet을 사용 하는 VS에서 [#3053](https://github.com/NuGet/Home/issues/3053)

* "에 의해 차단 packages.config" `project.json` (UWP, 통합 또는 빌드) 프로젝트- [#3046](https://github.com/NuGet/Home/issues/3046)

* dotnet cli preview2 003121 공식 preview2 빌드는 빌드 스크립트에서 설치를 업데이트 합니다. - [#3045](https://github.com/NuGet/Home/issues/3045)

* 패키지 관리자 UI: 패키지를 업데이트 한 후 새 버전이 표시 되지 않습니다- [#3041](https://github.com/NuGet/Home/issues/3041)

* -ApiKey 삭제 명령줄에서 읽기/에서 전송 되지 않습니다 3.5.0-beta- [#3037](https://github.com/NuGet/Home/issues/3037)

* 잘못 된 문자열: 패키지의 안정적인 릴리스 시험판 종속성에 없어야 합니다. - [#3030](https://github.com/NuGet/Home/issues/3030)

* OptimizedZipPackage 캐시 유지 빈 폴더- [#3029](https://github.com/NuGet/Home/issues/3029)

* PCL (net46 및 windows 10) 프로젝트 get NullRef 예외를 만드는 중입니다. - [#3014](https://github.com/NuGet/Home/issues/3014)

* 더 높은 버전 allowedVersions 제약 조건으로 제한 되 면 Nuget 업데이트 알림 메시지를 제공 해야 [#3013](https://github.com/NuGet/Home/issues/3013)

* Nuget v3 복원 문제- [#2891](https://github.com/NuGet/Home/issues/2891)

* 오류-1 사용 하 여 자격 증명 플러그 인 종료 / 여러 소스를 사용 하 여 자격 증명 공급자를 사용 하는 경우 패키지 다운로드 중 오류 발생 [#2885](https://github.com/NuGet/Home/issues/2885)

* `project.json` nuget 복원-변경 된 항목이 없을 경우 컴파일을 발생 시킬 [#2817](https://github.com/NuGet/Home/issues/2817)

* 기호 패키지 적이 있어야 설치 또는 업데이트-사용할 [#2807](https://github.com/NuGet/Home/issues/2807)

* VS repositoryPath에서 환경 변수를 지원 하지 않습니다 (nuget.exe 않습니다)- [#2763](https://github.com/NuGet/Home/issues/2763)

* 내게 필요한 옵션 기능에 대 한 패키지 관리자 UI에서 레이블이 지정 되지 않은 Uielement 레이블을 [#2745](https://github.com/NuGet/Home/issues/2745)

* 하이픈으로 연결 된 프로필을 사용 하 여 이식 가능한 프레임 워크 거부 됩니다. - [#2734](https://github.com/NuGet/Home/issues/2734)

* NuGet 패키지 관리자를 사용 해야 패키지 세부 정보에 적용 되지 않는 옵션 목록 명확히 `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* nuget.exe push/삭제 API 키를 사용 하지 않습니다 [#2627](https://github.com/NuGet/Home/issues/2627)

* 잠금 파일에서 잠긴된 속성을 제거 [#2379](https://github.com/NuGet/Home/issues/2379)

* NuGet 3.3.0 업데이트 실패 '...는 추가 제약 조건에 정의 된 packages.config이이 작업을 방지 합니다.' - [#1816](https://github.com/NuGet/Home/issues/1816)

* 잘못 된 메시지-throw 존재 하지 않는 로컬 원본에서 패키지를 설치 [#1674](https://github.com/NuGet/Home/issues/1674)

* "업그레이드 가능" 필터 버전 제약 조건 위반 하는 업그레이드를 보여 줍니다. [#1094](https://github.com/NuGet/Home/issues/1094)

* 네이티브 패키지-업데이트할 수 없습니다 [#1291](https://github.com/NuGet/Home/issues/1291)


## <a name="features"></a>기능

* NuGet-에서 추가 된 참조에서 false로 설정 CopyLocal 지원 [#329](https://github.com/NuGet/Home/issues/329)

* MSBuild 15-nuget.exe 지원 [#1937](https://github.com/NuGet/Home/issues/1937)

* 팩을 지원 합니다.`csproj` + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)

* 사용자 작업을 실행 중인 경우 사용자 작업을 사용 하지 않도록 설정- [#1440](https://github.com/NuGet/Home/issues/1440)

* NuGet에 대 한 지원을 추가할지 `runtimes/{rid}/nativeassets/{txm}/`  -  [#2782](https://github.com/NuGet/Home/issues/2782)

* NuGet에서 누락 된 프레임 워크 호환성 추가 (3.x에 포함 되어)는 2.x- [#2720](https://github.com/NuGet/Home/issues/2720)

* -대체 패키지 폴더에 대 한 지원을 [#2899](https://github.com/NuGet/Home/issues/2899)

* 디자인 및 구현-도구 패키지를 지원 하기 위해 패키지 형식의 개념 [#2476](https://github.com/NuGet/Home/issues/2476)

* 전역 패키지 폴더 경로 이동 하려면 API 추가 [#2403](https://github.com/NuGet/Home/issues/2403)

* SemVer 2.0.0-팩에서을 사용 하도록 설정 [#3356](https://github.com/NuGet/Home/issues/3356)

## <a name="dcrs"></a>DCR

* nuget.exe push-시간 제한 매개 변수 작동 하지 않음- [#2785](https://github.com/NuGet/Home/issues/2785)

* 패키지 설명 텍스트를 선택할-수 [#1769](https://github.com/NuGet/Home/issues/1769)

* 생성 하기 위해 nuget.exe를 사용 하도록 설정 `.props` 하 고 `.targets` 파일에 대 한 `.nuproj` 프로젝트 [#2711](https://github.com/NuGet/Home/issues/2711)

* 확장성 API 가져오기-프레임 워크를 비교할 추가 [#2633](https://github.com/NuGet/Home/issues/2633)

* 사용 하는 경우 종속성 옵션 숨기기 `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* Nuget.exe 자세한 출력-버전 헤더 출력 [#1887](https://github.com/NuGet/Home/issues/1887)

* 사용자를 기반으로 하는 dotnet tfm에서 업그레이드/설치 PCL 문제가 발생할 수 있습니다-알 수 있도록 필요한 NuGet [#3138](https://github.com/NuGet/Home/issues/3138)

* Tfm (포함)는 프로젝트에 대 한 잘못 된 설치/업그레이드 경고 = "dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)

* 업데이트-ReShaper 및 NuGet을 사용 하 여 성능 문제를 해결 [#3044](https://github.com/NuGet/Home/issues/3044)

* Netcoreapp11 및 netstandard17 지원-추가 [#2998](https://github.com/NuGet/Home/issues/2998)

* AssemblyMetadata 특성 활용 `.nuspec` 대체-토큰 [#2851](https://github.com/NuGet/Home/issues/2851)
