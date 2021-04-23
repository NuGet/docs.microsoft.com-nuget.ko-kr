---
title: NuGet 5.0 RTM 릴리스 정보
description: 알려진 문제, 버그 수정, 새로운 기능 및 Ecrs를 비롯 한 NuGet 5.0에 대 한 릴리스 정보입니다.
author: JonDouglas
ms.author: jodou
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: 19173d2be7cd66b65651655385466b40f5e08352
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901748"
---
# <a name="nuget-50-release-notes"></a>NuGet 5.0 릴리스 정보

NuGet 배포 차량:

| NuGet 버전 | Visual Studio 버전에서 사용 가능| .NET SDK에서 사용 가능|
|:---|:---|:---|
| [**5.0.0**](https://nuget.org/downloads) | [Visual Studio 2019 버전 16.0](https://visualstudio.microsoft.com/downloads/) | [2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |
| [**5.0.2**](https://nuget.org/downloads) | [Visual Studio 2019 버전 16.0.4](https://visualstudio.microsoft.com/downloads/) | [2.1.60 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup> .NET Core 워크 로드와 함께 Visual Studio 2019와 함께 설치 됨 

<sup>2</sup> .NET Core 워크 로드와 함께 Visual Studio 2019을 사용 하 여 선택적으로 설치할 수 있습니다.

## <a name="summary-whats-new-in-50"></a>요약: 5.0의 새로운 기능

* Visual Studio 2019에서 [필터링 된 솔루션](/visualstudio/ide/filtered-solutions) 복원 지원- [#5820](https://github.com/NuGet/Home/issues/5820)
* `BuildTransitive` 폴더를 사용 하면 패키지에서 대상/props을 호스트 프로젝트에 전이적으로 적용할 수 있습니다.- [#6091](https://github.com/NuGet/Home/issues/6091)
* NuGet Iv Api [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493) 에서 PackageReference 시나리오에 대 한 지원 향상
* `nuget.exe pack project.json` 사용 되지 않음- [#7928](https://github.com/NuGet/Home/issues/7928)
* Gen 1 자격 증명 공급자 플러그 인이 [gen 2](../reference/extensibility/nuget-cross-platform-authentication-plugin.md) 로 대체 되었으며 곧 사용 되지 않을 예정입니다. [#7819](https://github.com/NuGet/Home/issues/7819)

## <a name="issues-fixed-in-this-release"></a>이번 릴리스에서 수정된 문제

**버그**

* NoOp 복원 작업을 수행 하는 경우에는 .dgspec.js[#7854](https://github.com/NuGet/Home/issues/7854) obj 디렉터리에 쓸 필요가 없습니다.

* ~/.Era 내에서 만든 파일에 대 한 사용 권한이 너무 열려 [#7673](https://github.com/NuGet/Home/issues/7673)

* `dotnet list package --outdated` 인증이 필요한 원본에서 작동 하지 않음- [#7605](https://github.com/NuGet/Home/issues/7605)

* VisualStudio는 PackageReference로 설정 된 경우에도 항상 packages.config를 사용 하 여 패키지 참조가 없는 프로젝트에서 호출 [#7005](https://github.com/NuGet/Home/issues/7005)

* PMC: 목록에 없는 패키지에서 Update-Package 다시 설치에 실패 합니다 ("패키지를 찾을 수 없음"). - [#7268](https://github.com/NuGet/Home/issues/7268)

* 리포지토리 및 VSIX에서 타사 공지를 추가 합니다. [#7409](https://github.com/NuGet/Home/issues/7409)

* VisualStudio. InstallPackage는 지정 [#7493](https://github.com/NuGet/Home/issues/7493) 된 버전이 없는 경우 최신 버전을 설치 해야 합니다.

* --dotnet nuget 푸시 [#7519](https://github.com/NuGet/Home/issues/7519) 에 대 한 대화형 지원

* 잠금 파일을 사용 하 여 복원할 때 NU1603 경고가 발생 하지 않아야 합니다. - [#7529](https://github.com/NuGet/Home/issues/7529)

* NuGet은 최소한의 로깅으로 복원 하는 동안 프로젝트 경로를 인쇄할 수 없습니다.- [#7647](https://github.com/NuGet/Home/issues/7647)

* --dotnet 제거 패키지에 대 한 대화형 지원- [#7727](https://github.com/NuGet/Home/issues/7727)

* TypeForwardedTo [#7768](https://github.com/NuGet/Home/issues/7768) attrs를 사용 하 여 다시 NuGet을 추가 합니다.

* 잘 작동 하려면 더 짧은 경로가 필요 plugins_cache [#7770](https://github.com/NuGet/Home/issues/7770)

* 사용자가 특정 msbuild 버전을 요청 하지 않은 경우 msbuild 검색 경로를 선호 합니다. [#7786](https://github.com/NuGet/Home/issues/7786)

* `nuget.exe /?` 올바른 msbuild 버전을 나열 해야 합니다.- [#7794](https://github.com/NuGet/Home/issues/7794)

* Nuget.exe (498, 5): 오류: ' [#7793](https://github.com/NuGet/Home/issues/7793) /tmp/NuGetScratch '의 경로 부분을 찾을 수 없습니다.

* 복원 불필요 한 모든 버전의 참조 된 패키지의 내용을 컴퓨터 캐시에 열거- [#7639](https://github.com/NuGet/Home/issues/7639)

* MSBuild 자동 검색은 VS 2019 Preview- [#7621](https://github.com/NuGet/Home/issues/7621) 를 설치한 후 항상 16.0을 선택 합니다.

* 솔루션의 dotnet list 패키지는 프레임 워크에 대 한 중복 항목을 출력 합니다.- [#7607](https://github.com/NuGet/Home/issues/7607)

* InstallPackage 이전 프로젝트 및 패키지 폴더에 대해 IVsPackageInstaller를 호출할 때 "빈 경로 이름이 잘못 되었습니다." 예외가 발생 합니다. - [#5936](https://github.com/NuGet/Home/issues/5936)

* msbuild/t: 최소한의 자세한 정도 복원의 경우는 최소 [#4695](https://github.com/NuGet/Home/issues/4695)

* VS 16.0의 NuGet UI에 색 문제로 인 한 읽을 수 없는 탭이 있습니다.- [#7735](https://github.com/NuGet/Home/issues/7735)

* Nuget. 클라이언트는 & License.txt 대 한 설명은 [#7629](https://github.com/NuGet/Home/issues/7629)

* 복원 불필요 하 게 전역 패키지 폴더를 열거 하 여 형식 [#7596](https://github.com/NuGet/Home/issues/7596) 를 확인 합니다.

* 파일 잠금 적용 오류는 오류 목록 창에 표시 됩니다 [#7429](https://github.com/NuGet/Home/issues/7429)

* NuGet.Configuration 문제 해결- [#7326](https://github.com/NuGet/Home/issues/7326)

* 설치 위치를 업데이트 하는 MSBuild에 맞게 조정- [#7325](https://github.com/NuGet/Home/issues/7325)

* Nuget.exe. 작업 팩은 개발 종속성 이어야 합니다. [#7249](https://github.com/NuGet/Home/issues/7249)

* 디버그 기호를 포함 하는 팩 확장 지점 추가- [#7234](https://github.com/NuGet/Home/issues/7234)

* `dotnet pack` 만든 nupkg에서 종속성 버전 범위를 유지 해야 함 (부동 버전이 사용 되는 경우에도)- [#7232](https://github.com/NuGet/Home/issues/7232)

* `dotnet restore`사용자 수준 구성에 소스- [#7209](https://github.com/NuGet/Home/issues/7209) 있는 경우 인증 된 원본에서 실패

* Pack은 콘텐츠 파일에 대 한 BuildActions 집합을 제한 하지 않아야 합니다. [#7155](https://github.com/NuGet/Home/issues/7155)

* AssetTargetFallback가 성공 해야 하는 ProjectReference를 사용 하면 경고가 표시 됩니다. - [#7137](https://github.com/NuGet/Home/issues/7137)

* CPS (CommonProjectSystem)로 호출할 때 스레딩 문제로 인 한 교착 상태- [#7103](https://github.com/NuGet/Home/issues/7103)

* `dotnet add package` 로컬 구성에 지정 된 원본에 대 한 전역 구성의 자격 증명을 사용 하지 않습니다- [#6935](https://github.com/NuGet/Home/issues/6935)

* 비동기 코드 경로에서 호출 되는 MEF의 스레딩 문제- [#6771](https://github.com/NuGet/Home/issues/6771)

* 서명: 오류는 호출 스택 없이 두 번 보고 됩니다. [#6455](https://github.com/NuGet/Home/issues/6455)

* 신뢰할 수 없는 서명 인증서를 사용 하 여 서명 된 패키지를 설치 하면 오류 [#6318](https://github.com/NuGet/Home/issues/6318) 표시 됩니다.

* 두 프로젝트가 obj 디렉터리를 공유 하는 경우 NuGet 복원에 부적절 한 NoOps- [#6114](https://github.com/NuGet/Home/issues/6114)

* `dotnet restore`인증 된 피드의 패키지와 함께 Linux에서 PAT를 사용할 수 없음- [#5651](https://github.com/NuGet/Home/issues/5651)

* 사용 하지 않도록 설정 된 컴퓨터 전체 피드로 인해 dotnet restore 실패 함- [#5410](https://github.com/NuGet/Home/issues/5410)

**DCR**

* 나중에 "dotnet pack project.json"- [#7928](https://github.com/NuGet/Home/issues/7928) 제거에 대 한 경고
 
* Gen1 자격 증명 플러그 인에 대 한 사용 중단 경고 추가- [#7819](https://github.com/NuGet/Home/issues/7819)
 
* 서명: 리포지토리가 RepositorySignatures/5.0.0 리소스- [#7759](https://github.com/NuGet/Home/issues/7759) 를 통해 서명 된 모든 패키지의 클라이언트 확인을 요구 하도록 설정 합니다.

* NuGet.Config- [#4538](https://github.com/NuGet/Home/issues/4538) 를 통해 원본 당 http 요청 수를 제한 합니다.

* NuGet은 Net472 (VSIX의 16.0 빌드를 정리 하기 위해)를 대상으로 해야 합니다.- [#7143](https://github.com/NuGet/Home/issues/7143)

* PMC: OpenPackagePage 명령 제거- [#7384](https://github.com/NuGet/Home/issues/7384)

* Netcoreapp1.0 3.0 map을 NetStandard 2.1로 설정- [#7762](https://github.com/NuGet/Home/issues/7762)

* NuGet. * 패키지에 netstandard 2.0 지원 추가- [#6516](https://github.com/NuGet/Home/issues/6516)

* 패키지 작성자가 빌드 자산 전이적 동작을 정의할 수 있도록 허용- [#6091](https://github.com/NuGet/Home/issues/6091)

* VS 2019 솔루션 필터 기능을 지원 합니다. 는 프로젝트가 솔루션에 없음 또는 언로드된 프로젝트도 지원 합니다. 전체 솔루션을 복원 해야 합니다 (CLI 또는 VS를 통해). 먼저 [#5820](https://github.com/NuGet/Home/issues/5820)

* TFM change를 통해 .NET 4.7.2을 요구 하는 NuGet 5.0 어셈블리- [#7510](https://github.com/NuGet/Home/issues/7510)

* NuGetLicenseData에서 패키징은 공용 형식 이어야 합니다. Spdx에서 라이선스 메타 데이터 수집를 업데이트 합니다. - [#7471](https://github.com/NuGet/Home/issues/7471)

* 사용 되지 않는 설정 Api 제거- [#7294](https://github.com/NuGet/Home/issues/7294)

* 1 개 cpu를 사용 하는 시스템의 복원 시간 제한 해결- [#6742](https://github.com/NuGet/Home/issues/6742)

* NuGet은 자격 증명에 대 한 인증 유형을 필터링 하기 위해 NuGet.config-config 추가 옵션에 자격 증명이 있는 경우에도 NTLM 인증을 선호 [#5286](https://github.com/NuGet/Home/issues/5286)

* PackageReference (Packages.Config 기능 일치)에 대해 EmbedInteropTypes 사용- [#2365](https://github.com/NuGet/Home/issues/2365)

**[이 릴리스에서 해결 된 모든 문제 목록-5.0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**

## <a name="summary-whats-new-in-502"></a>요약: 5.0.2의 새로운 기능

* 보안 (dotnet.exe 또는 mono.exe를 통해 실행)-올바른 권한을 사용 하 여 obj 폴더를 만들어야 [#7908](https://github.com/NuGet/Home/issues/7908)

* 사용자 지정 nuget.config 및 #8011에서 mono/MacOS에 대 한 nuget.exe 복원이 실패 함 `PackageSignatureValidity: False` [](https://github.com/NuGet/Home/issues/8011)


## <a name="known-issues"></a>알려진 문제

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414"></a>.NET Core SDK로 설치된 FallbackFolders의 패키지는 사용자 지정 설치되며 서명 유효성 검사에 실패합니다. - [#7414](https://github.com/NuGet/Home/issues/7414)
#### <a name="issue"></a>문제
netcoreapp 1.x 및 netcoreapp 2.x 다중 대상을 지정하는 프로젝트를 복원하기 위해 dotnet.exe 2.x를 사용하면 대체 폴더가 파일 피드로 처리됩니다. 즉 복원할 때 NuGet이 대체 폴더에서 패키지를 선택하고 전역 패키지 폴더에 설치하려고 하며 일반적인 서명 유효성 검사를 수행하지만 실패합니다.<br>
#### <a name="workaround"></a>해결 방법
을 nothing으로 설정 하 여 대체 폴더를 사용 하지 않도록 설정 합니다 `RestoreAdditionalProjectSources` .

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

대체 폴더에서 복원 되는 패키지가 이제 NuGet.org에서 다운로드 되기 때문에이를 사용 합니다.