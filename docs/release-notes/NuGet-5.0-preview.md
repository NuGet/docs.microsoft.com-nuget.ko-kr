---
title: NuGet 5.0 preview 릴리스 정보
description: 알려진된 문제, 버그 수정, 새로운 기능 및 Dcr 포함 하는 NuGet 5.0 미리 보기에 대 한 릴리스 정보입니다.
author: anangaur
ms.author: anangaur
ms.date: 1/25/2019
ms.topic: conceptual
ms.openlocfilehash: 5889ea52f993fa8fe841f8eb83b6da659cdede93
ms.sourcegitcommit: 1ab750ff17e55c763d646c50e7630138804ce8b8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/14/2019
ms.locfileid: "56247661"
---
# <a name="nuget-50-preview-release-notes"></a>NuGet 5.0 미리 보기 릴리스 정보

## <a name="nuget-50-preview-releases"></a>NuGet 5.0 미리 보기 릴리스

* 2019 년 2 월 13- [NuGet 5.0 미리 보기 3](#summary-whats-new-in-50-preview-3)
* 2019 년 1 월 23- [NuGet 5.0 미리 보기 2](#summary-whats-new-in-50-preview-2)

## <a name="summary-whats-new-in-nuget-50-preview-3"></a>요약: NuGet 5.0 미리 보기 3의에서 새로운 기능

### <a name="issues-fixed-in-this-release"></a>이번 릴리스에서 수정된 문제 

**버그:**

* nuget.exe /? 올바른 msbuild 버전을 나열 해야 [#7794](https://github.com/NuGet/Home/issues/7794)

* NuGet.targets(498,5): 오류: 경로의 일부를 찾을 수 없습니다 ' / tmp/NuGetScratch--mono에서 [#7793](https://github.com/NuGet/Home/issues/7793)

* 복원에는 불필요 하 게 컴퓨터 캐시-참조 되는 패키지의 모든 버전의 내용을 열거 [#7639](https://github.com/NuGet/Home/issues/7639)

* 설치 및 2019 미리 보기로 제공 후 항상 MSBuild 자동 검색 16.0 선택 [#7621](https://github.com/NuGet/Home/issues/7621)

* 솔루션에서 dotnet 목록 패키지 프레임 워크-에 대 한 중복 항목을 출력 [#7607](https://github.com/NuGet/Home/issues/7607)

* 예외 "빈 경로 이름이 잘못 되었습니다." 이전에 호출 IVsPackageInstaller.InstallPackage 프로젝트 및 패키지 폴더 때 존재 하지 않습니다. - [#5936](https://github.com/NuGet/Home/issues/5936)

* msbuild /t: restore가 최소 자세한 정도-최소화 해야 [#4695](https://github.com/NuGet/Home/issues/4695)

**DCRs**

* 빌드 자산 전이적 동작을 정의 하는 패키지 작성자 허용 [#6091](https://github.com/NuGet/Home/issues/6091)

* 프로젝트를 솔루션의 일부가 아닌 또는 로드 되지 않지만 이전에 복원한-경우에 성공 하도록 VS에서 복원을 사용 하도록 설정 [#5820](https://github.com/NuGet/Home/issues/5820)


## <a name="summary-whats-new-in-50-preview-2"></a>요약: 5.0 미리 보기 2의에서 새로운 기능

### <a name="issues-fixed-in-this-release"></a>이번 릴리스에서 수정된 문제

**버그:**

* VS 16.0의 NuGet UI에 읽을 수 없는 탭 색-문제로 [#7735](https://github.com/NuGet/Home/issues/7735)

* NuGet.Core 및 NuGet.Clients License.txt 설명이- [#7629](https://github.com/NuGet/Home/issues/7629)

* 복원 유형-확인 하려고 시도할 때 전역 패키지 폴더를 불필요 하 게 열거 [#7596](https://github.com/NuGet/Home/issues/7596)

* 잠금 파일 적용에서 오류-오류 목록 창에 표시 해야 [#7429](https://github.com/NuGet/Home/issues/7429)

* NuGet.Configuration 문제 해결 [#7326](https://github.com/NuGet/Home/issues/7326)

* MSBuild 업데이트에 맞게의 설치 위치입니다.  - [#7325](https://github.com/NuGet/Home/issues/7325)

* NuGet.Build.Tasks.Pack 개발 종속성-해야 [#7249](https://github.com/NuGet/Home/issues/7249)

* 포함에 대 한 팩 확장 지점을 추가할 디버그 기호- [#7234](https://github.com/NuGet/Home/issues/7234)

* dotnet pack에서 만든된 nupkg 종속성 버전 범위를 보존 해야 합니다. (짝수 부동 버전을 사용 하는 경우)- [#7232](https://github.com/NuGet/Home/issues/7232)

* 사용자 수준 구성도 원본이-하는 경우 인증 된 원본에서 dotnet restore가 실패 [#7209](https://github.com/NuGet/Home/issues/7209)

* 팩 콘텐츠 파일에 대 한 BuildActions 집합이 제한 하지 [#7155](https://github.com/NuGet/Home/issues/7155)

* 되려면 AssetTargetFallback 해야 하는 projectreference를 사용 하 게 경고 해야 합니다. - [#7137](https://github.com/NuGet/Home/issues/7137)

* CPS (CommonProjectSystem-)를 호출 하는 경우 스레딩 문제로 인해 교착 상태가 [#7103](https://github.com/NuGet/Home/issues/7103)

* dotnet 패키지 로컬 config-에 지정 된 원본에 대 한 전역 구성에서 자격 증명을 사용 하지 않습니다 추가 [#6935](https://github.com/NuGet/Home/issues/6935)

* 스레딩 문제 MEF는 비동기 없게-호출 [#6771](https://github.com/NuGet/Home/issues/6771)

* 서명: 오류가 보고 되는 두 번 및 호출 스택을-없이 [#6455](https://github.com/NuGet/Home/issues/6455)

* 신뢰할 수 없는 서명 인증서를 사용 하 여 서명된 된 패키지를 설치 오류-표시할지 [#6318](https://github.com/NuGet/Home/issues/6318)

* 2 프로젝트 obj 디렉터리를 공유 하는 경우 NuGet 복원 괜찮음 부적절 하 게 [#6114](https://github.com/NuGet/Home/issues/6114)

* PAT-인증 된 피드의 패키지를 사용 하 여 Linux에서 dotnet restore를 사용 하 여 사용할 수 없습니다 [#5651](https://github.com/NuGet/Home/issues/5651)

* 사용할 수 없는 컴퓨터 와이드 피드-인해 dotnet restore가 실패 [#5410](https://github.com/NuGet/Home/issues/5410)

**DCRs**

* .NET 4.7.2 (TFM 변경)-를 통해 할 NuGet 5.0 어셈블리 [#7510](https://github.com/NuGet/Home/issues/7510)

* NuGetLicenseData NuGet.Packaging에서 공용 유형 이어야 합니다. Spdx에서 수집 하는 라이선스 메타 데이터를 업데이트 합니다. - [#7471](https://github.com/NuGet/Home/issues/7471)

* 사용 되지 않는 설정을 Api-제거 [#7294](https://github.com/NuGet/Home/issues/7294)

* 해결 방법 복원 시간 제한이 1 사용 하 여 시스템에서 cpu- [#6742](https://github.com/NuGet/Home/issues/6742)

* NuGet.config에서 자격 증명이 있는 경우에 NuGet에서 NTLM 인증-자격 증명에 대 한 인증 유형을 필터링 하기 구성 옵션을 추가 [#5286](https://github.com/NuGet/Home/issues/5286)

* Packagereference (일치 하는 Packages.Config 기능)-EmbedInteropTypes 사용 [#2365](https://github.com/NuGet/Home/issues/2365)

[이 릴리스 5.0.0-preview2에서 해결 된 모든 문제 목록](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

### <a name="known-issues"></a>알려진 문제

#### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a>dotnet nuget 푸시 --interactive로 인해 Mac에서 오류가 발생합니다. - [#7519](https://github.com/NuGet/Home/issues/7519)
**문제** 는 `--interactive` 인수는 dotnet cli를 통해 전달 되지 않습니다 및 오류 발생 `error: Missing value for option 'interactive'` 
 **해결** 같은대화형옵션을사용하여다른dotnet명령실행`dotnet restore --interactive` 하 고 인증 합니다. 인증은 자격 증명 공급자에 의해 캐시될 수 있습니다. 그런 다음, `dotnet nuget push`를 실행합니다.

#### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a>.NET Core SDK로 설치된 FallbackFolders의 패키지는 사용자 지정 설치되며 서명 유효성 검사에 실패합니다. - [#7414](https://github.com/NuGet/Home/issues/7414)
**문제** dotnet.exe를 사용 하는 경우 해당 다중 대상 netcoreapp 프로젝트를 복원 하려면 2.x 1.x 및 netcoreapp 2.x, 대체 폴더 피드 파일로 처리 됩니다. 즉 복원할 때 NuGet이 대체 폴더에서 패키지를 선택하고 전역 패키지 폴더에 설치하려고 하며 일반적인 서명 유효성 검사를 수행하지만 실패합니다.
**해결 방법** 대체 폴더의 사용을 설정 하 여 비활성화 된 `RestoreAdditionalProjectSources` nothing으로 합니다. `<RestoreAdditionalProjectSources/>` NuGet.org에서 많은 패키지가 다운로드되도록 하므로 주의하여 사용하세요. 그렇지 않으면 대체 폴더에서 복원될 패키지입니다.
