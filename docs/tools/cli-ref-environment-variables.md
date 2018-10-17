---
title: NuGet CLI 환경 변수
description: Nuget.exe 환경 변수에 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: fd5824d1c5e05df08301dac1cf656ba1d5ca75cd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551740"
---
# <a name="nuget-cli-environment-variables"></a>NuGet CLI 환경 변수

nuget.exe를 통해 많은 작업이나, 사용자, 컴퓨터 전체에 영향을 주는 많은 환경 변수를 수정할 수 있습니다. 환경 변수는 `NuGet.Config` 파일 내부의 구성 값을 무시하고 어떠한 파일도 수정하지 않고 빌드 서버가 적절한 환경으로 바뀌는 것을 허용할 수 있습니다.

*FORCE_NUGET_EXE_INTERACTIVE*와 같은 몇몇 예외를 제외하고 명령줄에 직접 주어진 옵션이나, NuGet 구성 파일 내부의 값이 항상 우선값을 갖습니다. Nuget.exe가 여러 컴퓨터에서 다르게 작동할 경우, 환경 변수가 문제일 수 있습니다. 예를 들어 배포 중에 사용되는 Azure 웹앱인 Kudu는 *NUGET_XMLDOC_MODE* 설정을 패키지 복원 *성능을* 가속화하고, 저장 공간을 절약하기 위해 사용됩니다.

| 변수 | 설명 | 설명 |
| --- | --- | --- |
| http_proxy | NuGet HTTP 작업에 사용되는 http 프록시입니다. | `http://<username>:<password>@proxy.com` 등으로 지정할 수 있습니다. |
| no_proxy | 프록시를 사용하지 않고 도메인을 구성하는 방법입니다. | 여러 도메인을 쉼표(,)로 구분하여 사용할 수 있습니다. |
| EnableNuGetPackageRestore | 패키지 복원에 필요한 경우 NuGet이 암시적으로 동의하는지에 대한 플래그입니다. | *true* 또는 *1*이 동의하는 플래그로 간주되고, 다른 모든 값은 동의하지 않음으로 간주됩니다. |
| NUGET_EXE_NO_PROMPT | exe의 자격 증명 프롬프트가 뜨지 않도록 막습니다. | Null과 빈 문자열만 제외하고 다른 값은 모두 참으로 간주합니다. |
| FORCE_NUGET_EXE_INTERACTIVE | 대화형 모드를 사용할지에 대한 전역 환경 변수입니다. | Null과 빈 문자열만 제외하고 다른 값은 모두 참으로 간주합니다. |
| NUGET_PACKAGES | [전역 패키지 및 캐시 폴더 관리](../consume-packages/managing-the-global-packages-and-cache-folders.md)에 정의된 *전역 패키지* 폴더에 대한 경로를 지정합니다. | 절대 경로로 지정합니다. |
| NUGET_FALLBACK_PACKAGES | 대체(fallback) 전역 패키지 폴더입니다. | 여러 절대 경로를 세미콜론(;)으로 구분하여 사용할 수 있습니다. |
| NUGET_HTTP_CACHE_PATH | [전역 패키지 및 캐시 폴더 관리](../consume-packages/managing-the-global-packages-and-cache-folders.md)에 정의된 *http 캐시에* 대한 경로를 지정합니다. | 절대 경로로 지정합니다. |
| NUGET_PERSIST_DG | Dg (MSBuild에서 수집된 데이터) 파일을 유지할 것인지 결정하는 플래그입니다. | *false*가 기본값이고 *true* 또는 *false*로 지정할 수 있습니다. NUGET_PERSIST_DG_PATH 설정되지 않은 경우 임시 디렉터리(환경 변수에서 지정한 임시 디렉터리 내부의 NuGetScratch 폴더)에 저장됩니다. |
| NUGET_PERSIST_DG_PATH | Dg 파일을 저장할 경로입니다. | 이 옵션은 절대 경로로 지정해야 하며 *NUGET_PERSIST_DG* 값이 true일 때만 사용됩니다. |
| NUGET_RESTORE_MSBUILD_ARGS | 추가 MSBuild 인수를 설정합니다. | |
| NUGET_RESTORE_MSBUILD_VERBOSITY | MSBuild 로그의 출력 레벨을 설정합니다. | 기본값은 *quiet* ("/ v: q")이고, 가능한 값은 *q [uiet]*, *m [inimal]*, *n [ormal]*, *d [etailed]* 및 *diag [nostic]* 입니다. |
| NUGET_SHOW_STACK | 사용자에게 스택 추적을 비롯한 예외 전체를 보여줄지 결정합니다. | *false*가 기본이며 *true*나 *false*로 지정할 수 있습니다. |
| NUGET_XMLDOC_MODE | 어셈블리 XML 설명서 파일 압축 풀기 처리 방법을 결정합니다. | 지원되는 모드는 XML 파일을 추출하지 않는 *건너뛰기*, XML 문서 파일을 zip 형식으로 압축하여 저장하는 *압축* 또는 XML 문서 파일을 일반적인 파일로 취급하는 *none* 입니다. |
| NUGET_CERT_REVOCATION_MODE | 패키지 서명에 사용되는 인증서의 해지 상태를 확인하는 방법 결정을 pefromed 서명된 패키지를 설치 또는 복원한 경우. 설정하지 않으면 기본값은 `online`으로 합니다.| 기본값은 *온라인*이고 가능한 값은 *온라인*과 *오프라인*입니다.  [NU3028](../reference/errors-and-warnings/NU3028.md)과 관련이 있습니다. |
