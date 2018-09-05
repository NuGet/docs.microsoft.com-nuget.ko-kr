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

다양 한 nuget.exe 컴퓨터 전체의 사용자에 영향을 주거나 수준을 처리 하는 환경 변수를 통해 nuget.exe CLI의 동작을 구성할 수 있습니다. 환경 변수는 항상 모든 설정을 무시 `NuGet.Config` 모든 파일을 수정 하지 않고 적절 한 설정을 변경 하려면 서버를 구축 하는 파일을 허용 합니다.

일반적으로 명령줄에서 직접 또는 NuGet 구성 파일에 지정 된 옵션이 우선 순위를이 밖에도 몇 가지 예외와 같은 *FORCE_NUGET_EXE_INTERACTIVE*합니다. Nuget.exe는 여러 컴퓨터 간에 다르게를 찾은 경우 환경 변수 원인일 수 있습니다. 예를 들어 Azure 웹 앱 Kudu (배포 하는 동안 사용 됨)에 *NUGET_XMLDOC_MODE* 로 설정 *건너뛸* 패키지 복원 성능을 가속화 하 고 디스크 공간을 절약 합니다.

| 변수 | 설명 | 설명 |
| --- | --- | --- |
| http_proxy | NuGet HTTP 작업에 사용 되는 http 프록시입니다. | 으로 지정 될이 `http://<username>:<password>@proxy.com`합니다. |
| no_proxy | 프록시를 사용 하 여 사용 하지 않으려면 도메인을 구성 합니다. | 쉼표 (,)로 구분 하는 도메인으로 지정 합니다. |
| EnableNuGetPackageRestore | NuGet는 암시적으로 동의 부여 하는 경우 패키지 복원에 필요한 경우에 대 한 플래그입니다. | 지정 된 플래그는 취급 *true* 또는 *1*, 플래그로 처리 하는 다른 모든 값이 설정 되지 않은. |
| NUGET_EXE_NO_PROMPT | 자격 증명 프롬프트에 대 한 exe를 방지 합니다. | Null 또는 빈 문자열로 취급 됩니다 점을 제외 하 고 값이 플래그를 설정/true. |
| FORCE_NUGET_EXE_INTERACTIVE | 대화형 모드를 적용 하려면 전역 환경 변수입니다. | Null 또는 빈 문자열로 취급 됩니다 점을 제외 하 고 값이 플래그를 설정/true. |
| NUGET_PACKAGES | 에 사용할 경로 *전역 패키지* 에 설명 된 대로 폴더 [전역 패키지 및 캐시 폴더 관리](../consume-packages/managing-the-global-packages-and-cache-folders.md)합니다. | 절대 경로로 지정 합니다. |
| NUGET_FALLBACK_PACKAGES | 대체 (fallback) 전역 패키지 폴더입니다. | 절대 폴더 경로 세미콜론 (;)으로 구분 합니다. |
| NUGET_HTTP_CACHE_PATH | 에 사용할 경로 *http 캐시* 에 설명 된 대로 폴더 [전역 패키지 및 캐시 폴더 관리](../consume-packages/managing-the-global-packages-and-cache-folders.md)합니다. | 절대 경로로 지정 합니다. |
| NUGET_PERSIST_DG | Dg (MSBuild에서 수집 된 데이터) 파일을 유지 해야 하는 경우를 나타내는 플래그입니다. | 로 지정 된 *true* 하거나 *false* (기본값) 이면 NUGET_PERSIST_DG_PATH 설정 되지 않은 경우 임시 디렉터리 (현재 환경 임시 디렉터리에 NuGetScratch 폴더)에 저장 됩니다. |
| NUGET_PERSIST_DG_PATH | Dg 파일을 유지 하려면 경로입니다. | 이 옵션은 절대 경로로 지정에 사용 되는 경우에만 *NUGET_PERSIST_DG* 설정할지 true로 합니다. |
| NUGET_RESTORE_MSBUILD_ARGS | 추가 MSBuild 인수를 설정합니다. | |
| NUGET_RESTORE_MSBUILD_VERBOSITY | MSBuild 로그의 자세한 정도 설정합니다. | 기본값은 *quiet* ("/ v: q"). 가능한 값 *q [uiet]*, *m [inimal]* 를 *n [ormal]* 를 *d [etailed]*, 및 *diag [nostic]* 합니다. |
| NUGET_SHOW_STACK | 전체 예외 스택 추적 등을 사용자에 게 표시할지 여부를 결정 합니다. | 로 지정 된 *true* 하거나 *false* (기본값). |
| NUGET_XMLDOC_MODE | 어셈블리 XML 설명서 파일 압축 풀기 처리 방법을 결정 합니다. | 지원 되는 모드를 *건너뜁니다* (XML 문서 파일을 추출 하지 않습니다) *압축* (zip 보관 파일로 XML 문서 파일을 저장 합니다.) 또는 *none* (기본값, XML 문서 파일을 일반으로 취급 파일)입니다. |
| NUGET_CERT_REVOCATION_MODE | 패키지 서명에 사용 되는 인증서의 해지 상태를 확인 하는 방법 결정를 pefromed 서명 된 패키지를 설치 또는 복원 된 경우. 설정 하지 않으면 기본값은 `online`합니다.| 가능한 값 *online* (기본값) 이면 *오프 라인*합니다.  관련 된 [NU3028](../reference/errors-and-warnings/NU3028.md) |
