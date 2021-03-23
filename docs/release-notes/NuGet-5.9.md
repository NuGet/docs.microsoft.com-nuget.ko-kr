---
title: NuGet 5.9 릴리스 정보
description: 새 기능, 버그 수정 및 Ecrs를 비롯 한 NuGet 5.9에 대 한 릴리스 정보입니다.
author: erdembayar
ms.author: eryondon
ms.date: 3/11/2021
ms.topic: conceptual
ms.openlocfilehash: 24933ebb51851da2583b03e7fd3e55fade5e8a18
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859539"
---
# <a name="nuget-59-release-notes"></a>NuGet 5.9 릴리스 정보

NuGet 배포 차량:

| NuGet 버전 | Visual Studio 버전에서 사용 가능 | .NET SDK에서 사용 가능 |
|:---|:---|:---|
| [**5.9**](https://nuget.org/downloads) | [Visual Studio 2019 버전 16.9](https://visualstudio.microsoft.com/downloads/) | [5.0](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1</sup> .net Core 워크 로드와 함께 Visual Studio 2019와 함께 설치 됨
  
> [!NOTE]
> Visual Studio 16.9, MSBuild 16.9 및 .NET 5.0.3 +에 NuGet.exe 5.9 이상이 필요 합니다.

## <a name="summary-whats-new-in-59"></a>요약: 5.9의 새로운 기능

* 업데이트를 위해 미리 선택 된 패키지와 함께 패키지 관리자 UI를 시작 하는 패키지 종속성에 대 한 "업데이트" 상황에 맞는 메뉴 항목 추가 [#10378](https://github.com/NuGet/Home/issues/10378)

    ![패키지 "업데이트" 환경을 마우스 오른쪽 단추로 클릭](media/releasenotes-59-update.png)

* 솔루션 수준 패키지 관리자 UI에서 프로젝트 목록의 "버전" 열에 요청한 버전 (부동 버전 또는 버전 범위 요청 포함)을 표시 합니다. [#9827](https://github.com/NuGet/Home/issues/9827)

    ![솔루션 수준 패키지 관리자 UI에서 요청 된 버전](media/releasenotes-59-requested-version.png)

* A/B 테스트로 출시 된 패키지 관리자 UI 찾아보기 탭의 IntelliCode 패키지 제안- [#10053](https://github.com/NuGet/Home/issues/10053)

* `.nupkg.metadata`설치 원본을 포함 하도록 파일을 확장 합니다.- [#10354](https://github.com/NuGet/Home/issues/10354)

* Pack 작업 중에 특정 Tfm에 대 한 빌드 출력을 제외 하는 새 msbuild 속성을 소개 합니다.- [#10396](https://github.com/NuGet/Home/issues/10396)

### <a name="issues-fixed-in-this-release"></a>이번 릴리스에서 수정된 문제

**6Crs (디자인 변경 요청):**

* 최신 패키지 버전이 설치 된 경우 다운 아이콘 아이콘은 직관적이 지 않습니다. 이전 녹색 눈금이 완벽 하 게 [#9789](https://github.com/NuGet/Home/issues/9789)

* Nuget 디버그의 자세한 정도는 패키지를에서 가져온 위치를 표시 해야 합니다. [#3055](https://github.com/NuGet/Home/issues/3055)

* NuGet 팩은 버전 번호- [#9215](https://github.com/NuGet/Home/issues/9215) 를 생략 하 고 잘못 된 점을 catch 해야 합니다.

* [CPVM] 중앙 전이적 종속성의 고정을 사용 하지 않도록 설정- [#10132](https://github.com/NuGet/Home/issues/10132)

* net5 TFM: TPV [#9441](https://github.com/NuGet/Home/issues/9441) 누락 된 경우 오류를 생성 합니다.

* 복원 하는 동안 로그 패키지 contenthash (추출 중)- [#10384](https://github.com/NuGet/Home/issues/10384)

* 솔루션 열기에서 복원을 호출 하는 레거시 PR 프로젝트에 대 한 사전 등록 메커니즘 구현 [#9986](https://github.com/NuGet/Home/issues/9986)

* 패키지 관리자에서 둘 이상의 소스를 선택 하면 NuGet 패키지 추천 작동 합니다.- [#10433](https://github.com/NuGet/Home/issues/10433)

* 정상적으로 복원 하는 경우 패키지를 복원할 원본- [#10461](https://github.com/NuGet/Home/issues/10461)

**미**

* INuGetPackageFileService-Codespaces에 연결 되 고 독립 실행형- [#10151](https://github.com/NuGet/Home/issues/10151) 에 대 한 이미지 및 포함 라이선스를 가져옵니다.

* VS OE: IProjectMetadataContextInfo 누락 포맷터- [#10079](https://github.com/NuGet/Home/issues/10079)

* [CPVM-성능] CentralTransitiveDependencyGroups에 기록 된 정보 줄이기- [#10002](https://github.com/NuGet/Home/issues/10002)

* 로드 되지 않는 프로젝트로 인해 발생 하는 복원 작업은 `NoOp` 원격 분석에서로 보고 됩니다 [#9985](https://github.com/NuGet/Home/issues/9985)

* 특정 색 pallets 아이콘을 사용 하면 PM UI에서 충돌 VS- [#10037](https://github.com/NuGet/Home/issues/10037)

* [CPVM-성능] CPVM 정보를 추가할 때 PackageSpec 클론 줄이기- [#10003](https://github.com/NuGet/Home/issues/10003)

* PM UI-asyncify 아이콘 로드- [#10009](https://github.com/NuGet/Home/issues/10009)

* PM UI에서 아이콘 Url을 로드할 때 UI 지연이 발생 [#8505](https://github.com/NuGet/Home/issues/8505)

* BitmapSource 및 WPF UI 스레드의 스레드 선호도- [#9161](https://github.com/NuGet/Home/issues/9161)

* Targetframework NU5128를 사용 하는 packastool 경우 경고에 대 한 경고- [#10097](https://github.com/NuGet/Home/issues/10097)

* 사용자 지정 된 빌드의 Pack 대상에서 OutputPath 논리가 제대로 작동 하지 않음- [#9234](https://github.com/NuGet/Home/issues/9234)

* VS OE: 클라이언트의 cache IServiceBroker 인스턴스- [#10141](https://github.com/NuGet/Home/issues/10141)

* PM UI에서 제거 하기 위한 NuGetProjectActions 만들기 병렬 작업- [#9956](https://github.com/NuGet/Home/issues/9956)

* 성능: 레거시 프로젝트 및 비 PR 프로젝트에 대 한 GetPackageSpecsAsync의 UIDelays 줄이기- [#9953](https://github.com/NuGet/Home/issues/9953)

* ``dotnet nuget push *.nupkg`` 둘 이상의 파일을 푸시 하지 않습니다.- [#4393](https://github.com/NuGet/Home/issues/4393)

* 리디렉션된 경우 macOS에서 출력이 80 문자로 래핑됩니다 [#10198](https://github.com/NuGet/Home/issues/10198)

* -원본 #9406 복원 실패 <Relative Path>  -  [](https://github.com/NuGet/Home/issues/9406)

* netcoreapp1.0 5.0-windows는 왕복 하지 않으며 플랫폼 정보를 구문 분석 하지 않습니다. [#10177](https://github.com/NuGet/Home/issues/10177)

* 사용자 지정 CPS 프로젝트를 복원 하려면 AssemblyReferences 프로젝트 기능이 필요 합니다. - [#8071](https://github.com/NuGet/Home/issues/8071)

* 라이선스 및 아이콘 파일 존재 검사는 항상 대/소문자를 구분 하는 비교를 사용 해야 합니다. [#9817](https://github.com/NuGet/Home/issues/9817)

* DotnetCLiToolReference 복원은 op 프로젝트 수/ [#10038](https://github.com/NuGet/Home/issues/10038) uptodateprojectscount에 대 한 이유를 이해 하기 어렵습니다.

* 어두운 테마의 "NuGet 패키지 관리자 형식 선택" 대화 상자를 통해 탭 하 여 탐색할 때 패키지 형식의 대시-줄 상자가 표시 되지 않는 경우- [#9729](https://github.com/NuGet/Home/issues/9729)

* #10314에서 전이적 프레임 워크 참조를 제외 합니다. `CollectFrameworkReferences`  -  [](https://github.com/NuGet/Home/issues/10314)

* 비교자 정적 속성은 [#10339](https://github.com/NuGet/Home/issues/10339) idempotent 이어야 합니다.

* 내부 계약 어셈블리 로드 해결 (RPS 수정 또는 예외 가져오기)- [#9919](https://github.com/NuGet/Home/issues/9919)

* GetService을 GetServiceAsync, 1 부- [#10362](https://github.com/NuGet/Home/issues/10362) 로 바꿉니다.

* CLI 설치는 나열 되지 않은 패키지를 설치 하면 안 됩니다.- [#7466](https://github.com/NuGet/Home/issues/7466)

* 정적 msbuild 그래프 복원-MSBuildStartupDirectory에 대 한 필요한 로깅 [unnnecessary](https://github.com/NuGet/Home/issues/10335)

* PrivateAssets로 표시 된 ProjectReferences의 프로젝트 종속성은 최신 상태로 파일 잠금 검사에 포함 되어서는 안 됩니다 [#8565](https://github.com/NuGet/Home/issues/8565)

* VS [#10406](https://github.com/NuGet/Home/issues/10406) 의 복원 오류를 표시 하지 않는 데이터가 잘못 된 SDK 프로젝트

* NU1004를 사용 하 여 cmd 줄에서 레거시 및 netstandard2 프로젝트가 혼합 된 솔루션을 복원 하는 경우- [#9623](https://github.com/NuGet/Home/issues/9623)

* Pack에는 종속성 패키지를 통해 현재 프로젝트의 패키지로 가져온 콘텐츠가 포함 됩니다 (SDK 기반 프로젝트에만 해당). [#8867](https://github.com/NuGet/Home/issues/8867)

* NuGet의 VS 확장성 API 오류에 대 한 원격 분석 추가- [#10062](https://github.com/NuGet/Home/issues/10062)

* Debugability을 개선 하기 위해 정적 그래프 복원에 GenerateRestoreGraphFile를 추가 합니다.  - [#10365](https://github.com/NuGet/Home/issues/10365)

* NuGet 패키지 관리자를 열 수 없습니다.- [#10336](https://github.com/NuGet/Home/issues/10336)

* NVDA/내레이터가 "Apache-2.0" 링크- [#10425](https://github.com/NuGet/Home/issues/10425) 에 대 한 "라이선스" 레이블을 읽지 않습니다.

* 최신 상태 표시줄 메시지가 VS- [#9402](https://github.com/NuGet/Home/issues/9402) 에 적합 하지 않습니다.

* 에서 package.lock.jspackages.config 잘못 된 대상 프레임 [#10257](https://github.com/NuGet/Home/issues/10257) 워크를 사용 합니다.

* Codespaces: #10439에서 원격 분석을 수정 합니다. https://github.com/NuGet/NuGet.Client/pull/3786  -  [](https://github.com/NuGet/Home/issues/10439)

* "RestoreLockedMode"를 사용 하도록 설정한 후 솔루션을 빌드할 때 오류 NU1004이 사라집니다.- [#8973](https://github.com/NuGet/Home/issues/8973)

* 역방향에서 PMUI를 통한 탭 이동은 앞 방향으로 대칭 이동 해야 합니다. [#10234](https://github.com/NuGet/Home/issues/10234)

* 실험적 인스턴스에서 PMUI를 디버깅 하는 경우에는 InvalidCastException가 솔루션 보기에서 [projectview](https://github.com/NuGet/Home/issues/10416) view로의을 throw 합니다.

* 찾아보기 탭에서 사용 되지 않는 패키지를 클릭 한 후 기본 버전이 null 인 경우 [#10380](https://github.com/NuGet/Home/issues/10380)

* 포커스를 다시 사용할 때 Visual Studio의 NuGet 관리자가 다시 로드 됨- [#4176](https://github.com/NuGet/Home/issues/4176)

* IPackageSourceProvider2 및 관련 형식 제거- [#10098](https://github.com/NuGet/Home/issues/10098)

* ' NameOfPackage ' 패키지는 프로젝트 [#5127](https://github.com/NuGet/Home/issues/5127) 의 ' 모든 ' 프레임 워크와 호환 되지 않습니다.

* CreateVersionsAsync는 불필요 한 NuGetVersion 비교- [#10436](https://github.com/NuGet/Home/issues/10436)

* NuGet. 클라이언트는 ManagedImageMonikers를 KnownMonikers 사용 하 여 대체 해야 합니다.- [#9977](https://github.com/NuGet/Home/issues/9977)

* 사용 되지 않는 아이콘은 찾아보기 탭에서 사용 되지 않는 패키지의 버전과 겹칩니다 [#10452](https://github.com/NuGet/Home/issues/10452)

* PackageReference NU1604 error 처리는 VS와 명령줄에서 서로 다릅니다 (Restore & Package Manager UI). [#9289](https://github.com/NuGet/Home/issues/9289)

* Codespaces: 필요한 포맷터가 등록 되지 않음- [#10467](https://github.com/NuGet/Home/issues/10467)

* Net45를 대상 프레임 워크로 서 제거 합니다.- [#10470](https://github.com/NuGet/Home/issues/10470)

* 구현-PMC 및 Powershell 사용량과 관련 된 이벤트를 추적 하는 새 원격 분석를 추가 합니다. - [#10142](https://github.com/NuGet/Home/issues/10142)

* 패키지 관리자 UI에서 업데이트할 수 있는 여러 패키지가 있는 경우 변경 내용 미리 보기 창에는 하나의 패키지만 표시 됩니다 [#10483](https://github.com/NuGet/Home/issues/10483)

* Multitargeted 프로젝트를 압축 하는 경우 빈 frameworkReferences 그룹을 생성 해야 합니다.- [#10218](https://github.com/NuGet/Home/issues/10218)

* ' 업데이트 ' 탭에서 패키지의 체크 상자는 파란색/파랑 (추가 대비)/밝은 테마에서 탭을 탐색할 때 대시 선 상자를 사용 하 여 볼 수 있습니다. [#8963](https://github.com/NuGet/Home/issues/8963)

* 화면 판독기에서 업데이트 탭 확인란이 제대로 작동 하지 않음- [#10449](https://github.com/NuGet/Home/issues/10449)

* PMUI에서 업데이트 하면 개체 참조가 개체의 인스턴스로 설정 되지 않습니다. [#9882](https://github.com/NuGet/Home/issues/9882)

* 구현-PMC 및 Powershell 사용에 관련 된 이벤트를 추적 하는 새 원격 분석 추가 후속 작업입니다. - [#10478](https://github.com/NuGet/Home/issues/10478)

* V2FeedPackageInfo- [#10480](https://github.com/NuGet/Home/issues/10480) 의 복사-붙여넣기 오류

* NuGetPackageFileService fix-삭제 가능 memorystream에 using 사용- [#10503](https://github.com/NuGet/Home/issues/10503)


**[이 릴리스에서 수정 된 모든 문제 목록-5.9.0](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f6be8c10485c0236b7ef889)**

**[이 릴리스의 커밋 목록-5.9.0](https://github.com/NuGet/NuGet.Client/compare/5.8.1.7021...5.9.0.7134)**

### <a name="community-contributions"></a>커뮤니티 기여

이 NuGet 릴리스를 위해 도움을 주는 모든 참가자에 게 감사 합니다.

|대상|Pr|문제|
|----|----|----|
[omajid](https://github.com/omajid) | [3865](https://github.com/NuGet/NuGet.Client/pull/3865) | V2FeedPackageInfo- [#10480](https://github.com/NuGet/Home/issues/10480) 의 복사-붙여넣기 오류
[krystianc](https://github.com/marcin-krystianc) | [3812](https://github.com/NuGet/NuGet.Client/pull/3812) | PrivateAssets = "All" 특성- [#10397](https://github.com/NuGet/Home/issues/10397) 를 사용 하 여 패키지를 참조 하는 경우에 대 한 테스트가 없습니다.
[krystianc](https://github.com/marcin-krystianc) | [3739](https://github.com/NuGet/NuGet.Client/pull/3739) | 여러 패키지 푸시에 대 한 지원 추가- [#4393](https://github.com/NuGet/Home/issues/4393)
[krystianc](https://github.com/marcin-krystianc) | [3723](https://github.com/NuGet/NuGet.Client/pull/3723) | 어셈블리 서명을 사용 하지 않도록 설정 하면 NuGet 라이브러리 빌드가 중단 됨- [#10173](https://github.com/NuGet/Home/issues/10173)
[kant2002](https://github.com/kant2002) | [3807](https://github.com/NuGet/NuGet.Client/pull/3807) | 기여 하는 문서 정리- [#10399](https://github.com/NuGet/Home/issues/10399)
[PathogenDavid](https://github.com/PathogenDavid) | [3754](https://github.com/NuGet/NuGet.Client/pull/3754) | 라이선스 및 아이콘 파일 존재 검사는 항상 대/소문자를 구분 하는 비교를 사용 해야 합니다. [#9817](https://github.com/NuGet/Home/issues/9817)
[campersau](https://github.com/campersau) | [3677](https://github.com/NuGet/NuGet.Client/pull/3677) | [#10037](https://github.com/NuGet/Home/issues/10037) DecodePixelWidth를 사용 하는 경우 BitmapCreateOptions. IgnoreColorProfile를 사용 하 여 WPF 문제를 해결 합니다.
[bjorkstromm](https://github.com/bjorkstromm) | [3697](https://github.com/NuGet/NuGet.Client/pull/3697) | NuGet에서 Windows SDK 10 링크가 손상 되었습니다. 클라이언트 기여 가이드- [#10099](https://github.com/NuGet/Home/issues/10099)
[bjorkstromm](https://github.com/bjorkstromm) | [3696](https://github.com/NuGet/NuGet.Client/pull/3696) | NuGet에서 상대 링크가 손상 되었습니다. 클라이언트 디버깅 가이드- [#10100](https://github.com/NuGet/Home/issues/10100)
[Nirmal4G](https://github.com/Nirmal4G) | [3637](https://github.com/NuGet/NuGet.Client/pull/3637) | 테스트 설비 및 관련 코드 개선- [#9996](https://github.com/NuGet/Home/issues/9996)
[rolfbjarne](https://github.com/rolfbjarne) | [3743](https://github.com/NuGet/NuGet.Client/pull/3743) | 리디렉션된 경우 macOS에서 출력이 80 문자로 래핑됩니다 [#10198](https://github.com/NuGet/Home/issues/10198)
[xen2](https://github.com/xen2) | [2861](https://github.com/NuGet/NuGet.Client/pull/2861) | NuGet. PackageManagement를 .NET Standard 패키지로 사용할 수 있도록 설정- [#6150](https://github.com/NuGet/Home/issues/6150)
[Anipik](https://github.com/Anipik) | [3810](https://github.com/NuGet/NuGet.Client/pull/3810) | Pack 작업 중에 특정 tfm에 대 한 빌드 출력을 제외 하는 새 msbuild 속성을 소개 합니다.- [#10396](https://github.com/NuGet/Home/issues/10396)

## <a name="feedback-welcome"></a>사용자 의견 환영

Microsoft는 사용자의 의견을 소중하게 생각합니다.  이 릴리스에 문제가 있는 경우 [GitHub 문제](https://github.com/NuGet/Home/issues) 및 [Visual Studio 개발자 커뮤니티](https://developercommunity.visualstudio.com/) 에서 기존 문제를 확인 하세요.  NuGet 내의 새로운 문제에 대 한 자세한 내용은 [GitHub 문제](https://github.com/NuGet/Home/issues/new)를 보고 하세요.
일반적인 NuGet 환경 문제에 대 한 자세한 내용은 **문제 보고 > 도움말** 에서 즐겨 사용 하는 IDE의 [문제 보고](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) 옵션을 통해 알려주세요.
