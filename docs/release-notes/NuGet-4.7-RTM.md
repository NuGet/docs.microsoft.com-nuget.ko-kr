---
title: NuGet 4.7 RTM 릴리스 정보
description: NuGet 4.7.0에 대한 릴리스 정보(알려진 문제, 버그 수정, 추가된 기능 및 DCR 포함)
author: JonDouglas
ms.author: jodou
ms.date: 5/14/2018
ms.topic: conceptual
ms.openlocfilehash: 143781cf0a95c6a156d4afcd83ad277f3e227711
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780163"
---
# <a name="nuget-47-release-notes"></a>NuGet 4.7 릴리스 정보

[Visual Studio 2017 15.7 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes)는 [NuGet 4.7.0](https://dist.nuget.org/win-x86-commandline/v4.7.0/nuget.exe)과 함께 제공됩니다.

## <a name="summary-whats-new-in-470"></a>요약: 4.7.0의 새로운 기능

* [리포지토리 서명 패키지](https://github.com/NuGet/Home/wiki/Repository-Signatures)를 사용하도록 패키지 서명을 확대했습니다.

* Visual Studio 버전 15.7에서는 [PackageReference를 사용하기 위해 packages.config 형식을 사용하는 기존 프로젝트를 마이그레이션하는 ](../consume-packages/migrate-packages-config-to-package-reference.md) 기능을 대신 도입했습니다.

## <a name="summary-whats-new-in-472"></a>요약: 4.7.2의 새로운 기능

* 보안 수정: ~/.nuget 내에서 만든 파일에 대한 권한이 열려 있습니다. [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)

## <a name="summary-whats-new-in-473"></a>요약: 4.7.3의 새로운 기능

* 보안 수정: NUPKG 내부에 있는 파일에는 NUPKG 디렉터리 위의 상대 경로가 포함될 수 있습니다. [#7906](https://github.com/NuGet/Home/issues/7906)

## <a name="known-issues"></a>알려진 문제

### <a name="the-migrate-packagesconfig-to-packagereference-option-is-not-available-in-the-right-click-context-menu"></a>`Migrate packages.config to PackageReference...` 옵션을 오른쪽 클릭 상황에 맞는 메뉴에서 사용할 수 없습니다.

#### <a name="issue"></a>문제점

프로젝트를 처음 열면 NuGet 작업이 수행될 때까지 NuGet을 초기화할 수 없습니다. 이로 인해 마이그레이션 옵션이 `packages.config` 또는 `References`의 오른쪽 클릭 상황에 맞는 메뉴에 표시되지 않습니다.

#### <a name="workaround"></a>해결 방법

다음 NuGet 작업 중 하나를 수행합니다.
* 패키지 관리자 UI 열기 - `References`를 마우스 오른쪽 단추로 클릭하고 `Manage NuGet Packages...`를 선택합니다.
* 패키지 관리자 콘솔 열기 - `Tools > NuGet Package Manager`에서 `Package Manager Console`을 선택합니다.
* NuGet 복원 실행 - 솔루션 탐색기에서 솔루션 노드를 마우스 오른쪽 단추로 클릭하고 `Restore NuGet Packages`를 선택합니다.
* NuGet 복원을 트리거하는 프로젝트 빌드

이제 마이그레이션 옵션이 표시됩니다. 이 옵션은 지원되지 않으며 ASP.NET 및 C++ 프로젝트 형식에 대해 표시되지 않습니다.

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>.NET Framework 및 NuGet이 포함된 .NET Standard 2.0 관련 문제

.NET Standard 및 해당 도구는 .NET Framework 4.6.1을 대상으로 하는 프로젝트에서 .NET Standard 2.0 또는 이전 버전을 대상으로 하는 NuGet 패키지 및 프로젝트를 사용할 수 있도록 설계되었습니다. [이 문서](https://github.com/dotnet/standard/issues/481)에서는 해당 시나리오와 관련된 문제, 문제를 해결하기 위한 계획 및 현재의 도구 상태로 배포할 수 있는 해결 방법을 요약하고 있습니다.

## <a name="top-issues-fixed-in-this-release"></a>이번 릴리스에서 해결된 주요 문제

### <a name="bugs"></a>버그

* NuGet이 .NET Core 프로젝트 시스템(새 회귀)에서 교착 상태로 실행됩니다. - [#6733](https://github.com/NuGet/Home/issues/6733)
* 팩: TfmSpecificPackageFile이 와일드카드 사용 경로와 함께 사용되는 경우 PackagePath가 잘못 구성됩니다. - [#6726](https://github.com/NuGet/Home/issues/6726)
* 팩: ispackable이 명시적으로 설정되지 않으면 Web API 프로젝트에서 패키지를 만들 수 없습니다. - [#6156](https://github.com/NuGet/Home/issues/6156)
* VS UI 및 PMC에서 새 패키지를 표시하는 데 30분이 걸림(nuget.exe는 바로 표시됨) - [#6657](https://github.com/NuGet/Home/issues/6657)
* 서명:  SignatureUtility.GetCertificateChain(...)이 모든 체인 상태를 확인하지 않습니다. - [#6565](https://github.com/NuGet/Home/issues/6565)
* 서명: DER GeneralizedTime 처리 개선 - [#6564](https://github.com/NuGet/Home/issues/6564)
* 서명: 변경된 패키지를 설치할 때 VS가 NU3002 오류를 표시하지 않습니다. - [#6337](https://github.com/NuGet/Home/issues/6337)
* lockFile.GetLibrary가 대소문자를 구분함 - [#6500](https://github.com/NuGet/Home/issues/6500)
* 설치/업데이트 복원 코드 및 복원 코드 경로가 일치하지 않음 - [#3471](https://github.com/NuGet/Home/issues/3471)
* 솔루션 패키지 관리자 버전 콤보 상자가 키보드를 통해 구분 기호를 선택할 수 있음 - [#2606](https://github.com/NuGet/Home/issues/2606)
* 원본에 대한 서비스 인덱스를 로드할 수 없습니다. `https://www.myget.org/F/<id>` ---> System.Net.Http.HttpRequestException: 응답 상태 코드가 성공을 나타내지 않습니다. 403(사용할 수 없음) - [#2530](https://github.com/NuGet/Home/issues/2530)

### <a name="dcrs"></a>DCR

* 요청 간 상관 관계를 지정하기 위해 X-NuGet-Session-Id 헤더를 내보냄 [기능 제안] - [#5330](https://github.com/NuGet/Home/issues/5330)
* IV API를 통해 Visual Studio에서 실행 중인 복원 작업 실행을 대기하는 방법을 보여줍니다. - [#6029](https://github.com/NuGet/Home/issues/6029)
* NuGet.exe -NoServiceEndpoint가 서비스 URL 접미사를 추가하지 못하게 함 - [#6586](https://github.com/NuGet/Home/issues/6586)
* 정보 버전에 커밋 해시 추가 - [#6492](https://github.com/NuGet/Home/issues/6492)
* 서명: 리포지토리 서명/연대 서명 제거 사용 - [#6646](https://github.com/NuGet/Home/issues/6646)
* 서명:  리포지토리 서명/연대 서명을 제거하기 위한 API - [#6589](https://github.com/NuGet/Home/issues/6589)
* VS에서 소스 정보 로그 - [#6527](https://github.com/NuGet/Home/issues/6527)
* TFM 및 RID에서만 /tools를 필터링하여 설정 XML을 /tools 폴더에 넣을 수 있음 - [#6197](https://github.com/NuGet/Home/issues/6197)
* 팩 명령이 .로 시작하는 파일을 제외할 때 경고함  - [#3308](https://github.com/NuGet/Home/issues/3308)

[이번 릴리스에서 수정된 모든 문제 목록](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.7")
