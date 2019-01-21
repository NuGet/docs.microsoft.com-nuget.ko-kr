---
title: NuGet 4.8 RTM 릴리스 정보
description: NuGet 4.8.1에 대한 릴리스 정보(알려진 문제, 버그 수정, 추가된 기능 및 DCR 포함)
author: karann-msft
ms.author: karann
ms.date: 5/14/2018
ms.topic: conceptual
ms.openlocfilehash: cf15c4f6a2e3e9f6ce7b6acb2304648041043685
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324827"
---
# <a name="nuget-48-rtm-release-notes"></a>NuGet 4.8 RTM 릴리스 정보

[Visual Studio 2017 15.8 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes)는 NuGet 4.8 기능과 함께 제공됩니다.


동일한 기능의 명령줄 버전도 사용 가능합니다.
* NuGet.exe 4.8 - [nuget.org/downloads](https://nuget.org/downloads)
* DotNet.exe - [.NET Core SDK 2.1.400](https://www.microsoft.com/net/download/visual-studio-sdks)


## <a name="summary-whats-new-in-this-release"></a>요약: 이번 릴리스의 새로운 기능
* NuGet.exe는 Windows 10에서 longfilenames를 지원합니다. [#6937](https://github.com/NuGet/Home/issues/6937)
* 인증 플러그인이 이제 플랫폼 간을 포함하여 MsBuild, DotNet.exe, NuGet.exe 및 Visual Studio에서 작동합니다. 인증 플러그인을 처음 생성하는 것은 MsBuild, DotNet.exe에서 지원되지 않습니다. 참고: VS 2017 15.9 Preview 빌드에는 VSTS 인증 플러그 인이 포함되어 있습니다. [#6486](https://github.com/NuGet/Home/issues/6486)
* MsBuild의 SDK 확인자는 이제 NuGet의 일부로 빌드되고 VS용 NuGet 도구로 설치됩니다. 이렇게 하면 버전이 동기화되지 않습니다. [#6799](https://github.com/NuGet/Home/issues/6799)
* PackageReference는 이제 DevelopmentDependency 메타데이터를 지원합니다. [#4125](https://github.com/NuGet/Home/issues/4125)

## <a name="known-issues"></a>알려진 문제
### <a name="installing-signed-packages-on-a-ci-machine-or-in-an-offline-environment-takes-longer-than-usual"></a>CI 머신 또는 오프라인 환경에 서명된 패키지를 설치하는 데 평소보다 오래 걸립니다.

#### <a name="issue"></a>문제
머신에서 인터넷 액세스가 제한된 경우(예: CI/CD 시나리오의 빌드 머신) 해지 서버에 도달할 수 없으므로 서명된 NuGet 패키지 설치/복원 시 경고([NU3028](https://docs.microsoft.com/en-us/nuget/reference/errors-and-warnings/nu3028))가 발생합니다. 이는 정상적입니다. 그러나 일부 경우에는 패키지 설치/복원에 평소보다 오래 걸리는 등의 의도하지 않은 결과가 발생할 수 있습니다.

#### <a name="workaround"></a>해결 방법
해지 확인 모드를 전환하는 환경 변수가 도입된 Visual Studio 15.8.4 및 NuGet.exe 4.8.1로 업데이트합니다.
`NUGET_CERT_REVOCATION_MODE` 환경 변수를 `offline`으로 설정하면 NuGet은 캐시된 인증서 해지 목록과 비교하여 인증서의 해지 상태를 확인하기만 하고 해지 서버에 연결하려고 시도하지 않습니다. 해지 확인 모드가 `offline`으로 설정된 경우 경고가 정보로 다운그레이드됩니다.

> [!Warning]
> 일반적인 상황에서 해지 확인 모드를 오프라인으로 전환하는 것은 권장되지 않습니다. 이렇게 전환하면 NuGet이 온라인 해지 확인을 건너뛰고 오래되었을 수 있는 캐시된 인증서 해지 목록과 비교하여 오프라인 해지 확인만 수행합니다. 그러면 서명 인증서가 해지되었을 수도 있는 패키지가 계속해서 설치/복원됩니다. 그렇지 않으면 해지 확인에 실패하고 설치되지 않습니다.

### <a name="the-migrate-packagesconfig-to-packagereference-option-is-not-available-in-the-right-click-context-menu"></a>`Migrate packages.config to PackageReference...` 옵션을 오른쪽 클릭 상황에 맞는 메뉴에서 사용할 수 없습니다.

#### <a name="issue"></a>문제

프로젝트를 처음 열면 NuGet 작업이 수행될 때까지 NuGet을 초기화할 수 없습니다. 이로 인해 마이그레이션 옵션이 `packages.config` 또는 `References`의 오른쪽 클릭 상황에 맞는 메뉴에 표시되지 않습니다.

#### <a name="workaround"></a>해결 방법

다음 NuGet 작업 중 하나를 수행합니다.
* 패키지 관리자 UI 열기 - `References`를 마우스 오른쪽 단추로 클릭하고 `Manage NuGet Packages...`를 선택합니다.
* 패키지 관리자 콘솔 열기 - `Tools > NuGet Package Manager`에서 `Package Manager Console`을 선택합니다.
* NuGet 복원 실행 - 솔루션 탐색기에서 솔루션 노드를 마우스 오른쪽 단추로 클릭하고 `Restore NuGet Packages`를 선택합니다.
* NuGet 복원을 트리거하는 프로젝트 빌드

이제 마이그레이션 옵션이 표시됩니다. 이 옵션은 지원되지 않으며 ASP.NET 및 C++ 프로젝트 형식에 대해 표시되지 않습니다.
참고: 이는 VS 2017 15.9 Preview 3에서 수정되었습니다.

## <a name="issues-fixed-in-this-release"></a>이번 릴리스에서 수정된 문제

### <a name="bugs"></a>버그
#### <a name="signing"></a>서명
* 서명: 오프라인 환경에서 서명된 패키지 설치 [#7008](https://github.com/NuGet/Home/issues/7008) - 4.8.1에서 수정됨
* 서명: 잘못된 URL 확인 [#7174](https://github.com/NuGet/Home/issues/7174)
* 서명: 패키지가 연대 서명된 리포지토리인 경우 RepositorySignatureVerifier에서 패키지 무결성 확인 [#6926](https://github.com/NuGet/Home/issues/6926)
* “패키지 무결성 검사에 실패했습니다.” 메시지(및 오류 코드)에 패키지 ID가 있어야 합니다. [#6944](https://github.com/NuGet/Home/issues/6944)
* 리포지토리 서명 패키지 확인을 사용하면 다른 인증서로 패키지를 서명할 수 있습니다. [#6884](https://github.com/NuGet/Home/issues/6884)
* NuGet - 서명 - 타임스탬프 URL은 https:// ?일 수 없습니다. - [#6871](https://github.com/NuGet/Home/issues/6871)
* NuSpec 압축 시나리오에서 NullRef를 수행하지 않으며 옵션이 개선되었습니다. [#6866](https://github.com/NuGet/Home/issues/6866)
* 연대 서명에 타임스탬프를 추가할 때 서명자 정보를 업데이트하는 동안 메모리가 잘못되었습니다. [#6840](https://github.com/NuGet/Home/issues/6840)
* 서명: CTL 예외 제거 [#6794](https://github.com/NuGet/Home/issues/6794)
* 서명: contentUrl은 HTTPS여야 합니다. [#6777](https://github.com/NuGet/Home/issues/6777)
* 서명:  SignedPackageVerifierSettings.VSClientDefaultPolicy가 사용되지 않습니다. [#6601](https://github.com/NuGet/Home/issues/6601)


#### <a name="pack"></a>압축
* nuspec를 압축하는 데 dotnet.exe를 사용하는 경우 복원 및 빌드가 필요하지 않습니다. [#6866](https://github.com/NuGet/Home/issues/6866)
* NuspecProperties에서 빈 대체 토큰이 허용됩니다. [#6722](https://github.com/NuGet/Home/issues/6722)
* NuspecProperties가 지정되지 않은 경우 PackTask에서 NullReferenceException이 발생합니다. [#4649](https://github.com/NuGet/Home/issues/4649)

#### <a name="accessibility"></a>액세스 가능성
* [액세스 가능성] PM UI에서 패키지 단추 아래의 ‘시험판’ 문자열이 패키지 설명에 가려집니다. [#4504](https://github.com/NuGet/Home/issues/4504)
* [액세스 가능성] PM UI에서 ‘Microsoft Visual Studio 오프라인 패키지’를 선택할 때 패키지 소스 드롭다운 및 설정 단추가 잘립니다. [#4502](https://github.com/NuGet/Home/issues/4502)

#### <a name="powershell-management-console-pmc"></a>PMC(Powershell 관리 콘솔)
* `Update-Package`가 PackageReference 버전 범위를 무시합니다. [#6775](https://github.com/NuGet/Home/issues/6775)
* `Update-Package -reinstall` 솔루션 전반의 문제 [#3127](https://github.com/NuGet/Home/issues/3127)
* `Update-Package [packagename] -reinstall`이 이름 지정된 패키지 대신 모든 패키지를 다시 설치합니다. [#737](https://github.com/NuGet/Home/issues/737)
* 패키지 관리자 콘솔에서 나열되지 않은 NuGet 패키지로 업데이트할 수 있습니다. [#4553](https://github.com/NuGet/Home/issues/4553)

#### <a name="misc"></a>기타
* `NuGet update self` NuGet.Commandline을 수정하려면 nupkg가 semver2.0이 아니어야 함 [#7116](https://github.com/NuGet/Home/issues/7116)
* NU1107 설치 실패 경험 개선 [#7107](https://github.com/NuGet/Home/issues/7107)
* GetAuthenticationCredentialRequest의 serialization이 올바르지 않습니다. [#6983](https://github.com/NuGet/Home/issues/6983)
* UI 스레드에서 초기화하는 경우 NuGet Visual Studio AsyncPackage를 로드할 수 없습니다. [#6976](https://github.com/NuGet/Home/issues/6976)
* 복원 시 project.json이 필요하다는 잘못된 오류를 보고합니다. [#6959](https://github.com/NuGet/Home/issues/6959)
* 패키지 관리자 UI: 미리 보기 변경 사항, 확인 단추가 키보드에서 자동으로 사용 가능하지 않습니다. [#6893](https://github.com/NuGet/Home/issues/6893)
* p2p 참조가 있는 프로젝트에서 RestoreSources가 무시됩니다. [#6776](https://github.com/NuGet/Home/issues/6776)
* .NET Framework 템플릿을 사용하여 단위 테스트 프로젝트를 만들면 packages.config가 포함된 이전 프로젝트 모델이 열립니다. [#6736](https://github.com/NuGet/Home/issues/6736)
* 프로젝트 참조가 패키지 종속성을 재정의하도록 허용합니다. [#6536](https://github.com/NuGet/Home/issues/6536)
* MSBuild 작업에 NoDefaultExcludes를 노출합니다. [#6450](https://github.com/NuGet/Home/issues/6450)
* 창 크기 조정 시 “모든 NuGet 캐시 지우기”에 대한 상태 메시지를 숨길 수 없습니다. [#5938](https://github.com/NuGet/Home/issues/5938)


[이번 릴리스에서 수정된 모든 문제 목록](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.8")
