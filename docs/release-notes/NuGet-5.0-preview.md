---
title: NuGet 5.0 preview 릴리스 정보
description: 알려진된 문제, 버그 수정, 새로운 기능 및 Dcr 포함 하는 NuGet 5.0 미리 보기에 대 한 릴리스 정보입니다.
author: anangaur
ms.author: anangaur
ms.date: 1/25/2019
ms.topic: conceptual
ms.openlocfilehash: ed3294f88ff99d5e26f630bdbca03aa8446b6e7f
ms.sourcegitcommit: 0cb4c9853cde3647291062eadee2298dd273311e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2019
ms.locfileid: "55084939"
---
# <a name="nuget-50-preview-release-notes"></a>NuGet 5.0 미리 보기 릴리스 정보

## <a name="summary-whats-new-in-50-preview-2"></a>요약: 5.0 미리 보기 2의에서 새로운 기능

### <a name="issues-fixed-in-this-release"></a>이번 릴리스에서 수정된 문제

#### <a name="bugs"></a>버그:

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

#### <a name="dcrs"></a>DCR

* .NET 4.7.2 (TFM 변경)-를 통해 할 NuGet 5.0 어셈블리 [#7510](https://github.com/NuGet/Home/issues/7510)

* NuGetLicenseData NuGet.Packaging에서 공용 유형 이어야 합니다. Spdx에서 수집 하는 라이선스 메타 데이터를 업데이트 합니다. - [#7471](https://github.com/NuGet/Home/issues/7471)

* 사용 되지 않는 설정을 Api-제거 [#7294](https://github.com/NuGet/Home/issues/7294)

* 해결 방법 복원 시간 제한이 1 사용 하 여 시스템에서 cpu- [#6742](https://github.com/NuGet/Home/issues/6742)

* NuGet.config에서 자격 증명이 있는 경우에 NuGet에서 NTLM 인증-자격 증명에 대 한 인증 유형을 필터링 하기 구성 옵션을 추가 [#5286](https://github.com/NuGet/Home/issues/5286)

* Packagereference (일치 하는 Packages.Config 기능)-EmbedInteropTypes 사용 [#2365](https://github.com/NuGet/Home/issues/2365)

[이 릴리스 5.0.0-preview2에서 해결 된 모든 문제 목록](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")


## <a name="known-issues"></a>알려진 문제

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a>dotnet nuget 푸시 --interactive로 인해 Mac에서 오류가 발생합니다. - [#7519](https://github.com/NuGet/Home/issues/7519)

#### <a name="issue"></a>문제
`--interactive` 인수가 dotnet CLI에 의해 전달되지 않고 오류가 발생함 `error: Missing value for option 'interactive'`

#### <a name="workaround"></a>해결 방법
`dotnet restore --interactive` 같은 대화형 옵션을 사용하여 다른 dotnet 명령을 실행하고 인증합니다. 인증은 자격 증명 공급자에 의해 캐시될 수 있습니다. 그런 다음, `dotnet nuget push`를 실행합니다.

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a>.NET Core SDK로 설치된 FallbackFolders의 패키지는 사용자 지정 설치되며 서명 유효성 검사에 실패합니다. - [#7414](https://github.com/NuGet/Home/issues/7414)

#### <a name="issue"></a>문제
netcoreapp 1.x 및 netcoreapp 2.x 다중 대상을 지정하는 프로젝트를 복원하기 위해 dotnet.exe 2.x를 사용하면 대체 폴더가 파일 피드로 처리됩니다. 즉 복원할 때 NuGet이 대체 폴더에서 패키지를 선택하고 전역 패키지 폴더에 설치하려고 하며 일반적인 서명 유효성 검사를 수행하지만 실패합니다.

#### <a name="workaround"></a>해결 방법
`RestoreAdditionalProjectSources`를 nothing으로 설정하여 대체 폴더를 사용하지 않도록 설정합니다. `<RestoreAdditionalProjectSources/>` NuGet.org에서 많은 패키지가 다운로드되도록 하므로 주의하여 사용하세요. 그렇지 않으면 대체 폴더에서 복원될 패키지입니다.
