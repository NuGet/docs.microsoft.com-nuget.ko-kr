---
title: NuGet 5.0 RTM 릴리스 정보
description: 알려진된 문제, 버그 수정, 새로운 기능 및 Dcr 포함 하 여 NuGet 5.0에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: 5e48ff19ea5c4908d7eb0a3cb19a31b738e348eb
ms.sourcegitcommit: 573af6133a39601136181c1d98c09303f51a1ab2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "58921587"
---
# <a name="nuget-50-release-notes"></a>NuGet 5.0 릴리스 정보

NuGet 배포 차량:

| NuGet 버전 | Visual Studio 버전에서 사용 가능| .NET SDK에서 사용 가능|
|:---|:---|:---|
| [**5.0.0**](https://nuget.org/downloads) | [Visual Studio 2019 버전 16.0](https://visualstudio.microsoft.com/downloads/) | [2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup>.NET Core 워크 로드를 사용 하 여 Visual Studio 2019와 함께 설치 

<sup>2</sup>.NET Core 워크 로드를 사용 하 여 Visual Studio 2019를 사용 하 여 설치를 선택적으로 사용 가능

## <a name="summary-whats-new-in-50"></a>요약: 5.0의 새로운 기능

* 복원에 대 한 지원을 [솔루션을 필터링](https://docs.microsoft.com/en-us/visualstudio/ide/filtered-solutions?view=vs-2019) 에서 Visual Studio 2019- [#5820](https://github.com/NuGet/Home/issues/5820)
* `BuildTransitive` 폴더에 패키지를 호스트 프로젝트에 대상/props를 전이적으로 적용할 수 있도록 [#6091](https://github.com/NuGet/Home/issues/6091)
* NuGet Iv api-PackageReference 시나리오에 대 한 지원 향상 [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)
* `nuget.exe pack project.json` 사용 되지 않습니다- [#7928](https://github.com/NuGet/Home/issues/7928)
* Gen 1 자격 증명 공급자 플러그 인으로 대체 되었습니다 [Gen 2](https://aka.ms/nuget-cross-platform-authentication-plugin) 되며 곧 사용 되지 않음- [#7819](https://github.com/NuGet/Home/issues/7819)

## <a name="issues-fixed-in-this-release"></a>이번 릴리스에서 수정된 문제

**버그**

* 방지 NoOp 복원 작업을 수행 하는 경우 *. obj 디렉터리-dgspec.json 쓰기 [#7854](https://github.com/NuGet/Home/issues/7854)

* ~/.Nuget 내에서 생성 된 파일에 대 한 권한이 너무 열려- [#7673](https://github.com/NuGet/Home/issues/7673)

* `dotnet list package --outdated` 인증-는 소스를 사용 하 여 작동 하지 않습니다 [#7605](https://github.com/NuGet/Home/issues/7605)

* NuGet.VisualStudio.IVsPackageInstaller-없는 패키지를 사용 하 여 프로젝트에 대 한 호출 참조 항상 사용 하 여 packages.config를 PackageReference-기본값은 설정 하는 경우에 [#7005](https://github.com/NuGet/Home/issues/7005)

* PMC: 업데이트 패키지 목록 패키지에 실패 하면 ("패키지를 찾을 수 없음")를 다시 설치 합니다. - [#7268](https://github.com/NuGet/Home/issues/7268)

* 리포지토리 및-VSIX에 제 3 자 통지 추가 [#7409](https://github.com/NuGet/Home/issues/7409)

* -지정 된 버전이 없는 경우 최신 버전을 설치 해야 하는 NuGet.VisualStudio.IVsPackageInstaller.InstallPackage [#7493](https://github.com/NuGet/Home/issues/7493)

* -dotnet nuget push 대화형 지원- [#7519](https://github.com/NuGet/Home/issues/7519)

* 잠금 파일을 사용 하 여 복원 NU1603 경고 발생 하지 않아야 합니다. - [#7529](https://github.com/NuGet/Home/issues/7529)

* NuGet은 최소 로깅으로-복원 하는 동안 프로젝트 경로 인쇄 하지 [#7647](https://github.com/NuGet/Home/issues/7647)

* -dotnet 용 대화형 지원 패키지를 제거 하는 데 사용- [#7727](https://github.com/NuGet/Home/issues/7727)

* 추가 NuGet.Packaging.Core TypeForwardedTo 기록 속성-를 사용 하 여 다시 [#7768](https://github.com/NuGet/Home/issues/7768)

* plugins_cache 해야도 작동 하려면 더 짧은 경로 [#7770](https://github.com/NuGet/Home/issues/7770)

* 사용자 특정 msbuild 버전-요청 하지 않은 경우 msbuild 검색에 대 한 경로 선호 [#7786](https://github.com/NuGet/Home/issues/7786)

* `nuget.exe /?` 올바른 msbuild 버전을 나열 해야 [#7794](https://github.com/NuGet/Home/issues/7794)

* NuGet.targets(498,5): 오류: 경로의 일부를 찾을 수 없습니다 ' / tmp/NuGetScratch--mono에서 [#7793](https://github.com/NuGet/Home/issues/7793)

* 복원에는 불필요 하 게 컴퓨터 캐시-참조 되는 패키지의 모든 버전의 내용을 열거 [#7639](https://github.com/NuGet/Home/issues/7639)

* 설치 및 2019 미리 보기로 제공 후 항상 MSBuild 자동 검색 16.0 선택 [#7621](https://github.com/NuGet/Home/issues/7621)

* 솔루션에서 dotnet 목록 패키지 프레임 워크-에 대 한 중복 항목을 출력 [#7607](https://github.com/NuGet/Home/issues/7607)

* 예외 "빈 경로 이름이 잘못 되었습니다." 이전에 호출 IVsPackageInstaller.InstallPackage 프로젝트 및 패키지 폴더 때 존재 하지 않습니다. - [#5936](https://github.com/NuGet/Home/issues/5936)

* msbuild /t: restore가 최소 자세한 정도-최소화 해야 [#4695](https://github.com/NuGet/Home/issues/4695)

* VS 16.0의 NuGet UI에 읽을 수 없는 탭 색-문제로 [#7735](https://github.com/NuGet/Home/issues/7735)

* NuGet.Core 및 NuGet.Clients License.txt 설명이- [#7629](https://github.com/NuGet/Home/issues/7629)

* 복원 유형-확인 하려고 시도할 때 전역 패키지 폴더를 불필요 하 게 열거 [#7596](https://github.com/NuGet/Home/issues/7596)

* 잠금 파일 적용에서 오류-오류 목록 창에 표시 해야 [#7429](https://github.com/NuGet/Home/issues/7429)

* NuGet.Configuration 문제 해결 [#7326](https://github.com/NuGet/Home/issues/7326)

* MSBuild 해당 설치 업데이트를 적용할 위치- [#7325](https://github.com/NuGet/Home/issues/7325)

* NuGet.Build.Tasks.Pack 개발 종속성-해야 [#7249](https://github.com/NuGet/Home/issues/7249)

* 포함에 대 한 팩 확장 지점을 추가할 디버그 기호- [#7234](https://github.com/NuGet/Home/issues/7234)

* `dotnet pack` (짝수 부동 버전을 사용 하는 경우)-nupkg 생성된에서 종속성 버전 범위를 유지 해야 [#7232](https://github.com/NuGet/Home/issues/7232)

* `dotnet restore` 인증된 원본 소스-역시 사용자 수준 구성 하는 경우에 실패 [#7209](https://github.com/NuGet/Home/issues/7209)

* 팩 콘텐츠 파일에 대 한 BuildActions 집합이 제한 하지 [#7155](https://github.com/NuGet/Home/issues/7155)

* 되려면 AssetTargetFallback 해야 하는 ProjectReference를 사용 하 게 경고 해야 합니다. - [#7137](https://github.com/NuGet/Home/issues/7137)

* CPS (CommonProjectSystem-)를 호출 하는 경우 스레딩 문제로 인해 교착 상태가 [#7103](https://github.com/NuGet/Home/issues/7103)

* `dotnet add package` 로컬 구성-에 지정 된 원본에 대 한 전역 구성에서 자격 증명을 사용 하지 않습니다 [#6935](https://github.com/NuGet/Home/issues/6935)

* 비동기에서 호출 되는 MEF 사용 하 여 스레딩 문제 코드 경로- [#6771](https://github.com/NuGet/Home/issues/6771)

* 서명: 오류가 보고 되는 두 번 및 호출 스택을-없이 [#6455](https://github.com/NuGet/Home/issues/6455)

* 신뢰할 수 없는 서명 인증서를 사용 하 여 서명된 된 패키지를 설치 오류-표시할지 [#6318](https://github.com/NuGet/Home/issues/6318)

* 2 프로젝트 obj 디렉터리를 공유 하는 경우 NuGet 복원 괜찮음 부적절 하 게 [#6114](https://github.com/NuGet/Home/issues/6114)

* 사용 하 여 PAT를 사용할 수 없습니다 `dotnet restore` -인증 된 피드의 패키지를 사용 하 여 Linux에서 [#5651](https://github.com/NuGet/Home/issues/5651)

* 사용할 수 없는 컴퓨터 와이드 피드-인해 dotnet restore가 실패 [#5410](https://github.com/NuGet/Home/issues/5410)

**DCRs**

* "Dotnet 팩 project.json"-향후 제거의 경고 [#7928](https://github.com/NuGet/Home/issues/7928)
 
* Gen1 자격 증명 플러그 인-에 대 한 사용 중단 경고가 추가 [#7819](https://github.com/NuGet/Home/issues/7819)
 
* 서명: RepositorySignatures/5.0.0 리소스를 통해 모든 패키지의 리포지토리로 클라이언트 인증을 요구 하는 사용된 리포지토리 서명 [#7759](https://github.com/NuGet/Home/issues/7759)

* 원본당 NuGet.Config-를 통해 http 요청 수를 제한 [#4538](https://github.com/NuGet/Home/issues/4538)

* NuGet (하는 데 VSIX의 16.0 빌드 정리) Net472-대상으로 지정 해야 [#7143](https://github.com/NuGet/Home/issues/7143)

* PMC: Remove OpenPackagePage command - [#7384](https://github.com/NuGet/Home/issues/7384)

* 확인 NetCoreApp 3.0 매핑할 NetStandard 2.1- [#7762](https://github.com/NuGet/Home/issues/7762)

* NuGet.* 패키지-netstandard2.0 지원을 추가할 [#6516](https://github.com/NuGet/Home/issues/6516)

* 빌드 자산 전이적 동작을 정의 하는 패키지 작성자 허용 [#6091](https://github.com/NuGet/Home/issues/6091)

* VS 2019 솔루션 필터 기능을 지원 합니다. 또한 솔루션에 없는 프로젝트 또는 언로드된 프로젝트를 지원합니다. (CLI 또는 VS)를 통해 완전 한 솔루션을 먼저 복원 해야 [#5820](https://github.com/NuGet/Home/issues/5820)

* .NET 4.7.2 (TFM 변경)-를 통해 할 NuGet 5.0 어셈블리 [#7510](https://github.com/NuGet/Home/issues/7510)

* NuGetLicenseData NuGet.Packaging에서 공용 유형 이어야 합니다. Spdx에서 수집 하는 라이선스 메타 데이터를 업데이트 합니다. - [#7471](https://github.com/NuGet/Home/issues/7471)

* 사용 되지 않는 설정을 Api-제거 [#7294](https://github.com/NuGet/Home/issues/7294)

* 해결 방법 복원 시간 제한이 1 사용 하 여 시스템에서 cpu- [#6742](https://github.com/NuGet/Home/issues/6742)

* NuGet.config에서 자격 증명이 있는 경우에 NuGet에서 NTLM 인증-자격 증명에 대 한 인증 유형을 필터링 하기 구성 옵션을 추가 [#5286](https://github.com/NuGet/Home/issues/5286)

* Packagereference (일치 하는 Packages.Config 기능)-EmbedInteropTypes 사용 [#2365](https://github.com/NuGet/Home/issues/2365)

**[이 릴리스-5.0 RTM에서에서 수정 된 모든 문제 목록](https://github.com/NuGet/Home/milestone/84?closed=1)**

## <a name="known-issues"></a>알려진 문제

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a>.NET Core SDK로 설치된 FallbackFolders의 패키지는 사용자 지정 설치되며 서명 유효성 검사에 실패합니다. - [#7414](https://github.com/NuGet/Home/issues/7414)
#### <a name="issue"></a>문제
netcoreapp 1.x 및 netcoreapp 2.x 다중 대상을 지정하는 프로젝트를 복원하기 위해 dotnet.exe 2.x를 사용하면 대체 폴더가 파일 피드로 처리됩니다. 즉 복원할 때 NuGet이 대체 폴더에서 패키지를 선택하고 전역 패키지 폴더에 설치하려고 하며 일반적인 서명 유효성 검사를 수행하지만 실패합니다.<br>
#### <a name="workaround"></a>해결 방법
대체 폴더의 사용을 설정 하 여 비활성화 된 `RestoreAdditionalProjectSources` nothing으로:

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

대체 (fallback) 폴더에서 복원할 수는 패키지는 NuGet.org에서 다운로드 하는 대로 주의 해 서 사용 합니다.
