---
title: NuGet CLI 환경 변수
description: Nuget.exe 환경 변수에 대 한 참조
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 50bf8b469eda423db7665323823a2daf3f3aa41d
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817075"
---
# <a name="nuget-cli-environment-variables"></a>NuGet CLI 환경 변수

다양 한 컴퓨터 전체의 사용자에 nuget.exe에 영향을 주거나 수준을 처리 하는 환경 변수를 통해 CLI nuget.exe의 동작을 구성할 수 있습니다. 환경 변수는 항상 모든 설정을 무시 `NuGet.Config` 파일을 선택할 모든 파일을 수정 하지 않고 적절 한 설정을 변경 하려면 서버를 구축 합니다.

일반적으로 명령줄에서 직접 또는 NuGet 구성 파일에 지정 된 옵션 순위가 되지만 몇 가지 예외가 같은 *FORCE_NUGET_EXE_INTERACTIVE*합니다. 서로 다른 컴퓨터 사이 다르게 해당 nuget.exe를 찾을 경우 환경 변수는 원인이 될 수 있습니다. 예를 들어 Azure 웹 앱 Kudu (배포 하는 동안 사용 됨)에 *NUGET_XMLDOC_MODE* 로 설정 *건너뛸* 속도를 높이려면 패키지 복원 성능을 디스크 공간을 절약 합니다.

| 변수 | 설명 | 설명 |
| --- | --- | --- |
| http_proxy | Http 프록시 NuGet HTTP 작업에 사용 됩니다. | 이로 지정할 수는 `http://<username>:<password>@proxy.com`합니다. |
| no_proxy | 프록시를 사용 하 여 무시 하는 도메인을 구성 합니다. | 쉼표 (,)로 구분 하는 도메인으로 지정 합니다. |
| EnableNuGetPackageRestore | NuGet 해야 암시적으로 동의 허용할 경우 복원 시 패키지에서 필요한 경우에 대 한 플래그입니다. | 지정 된 플래그가로 처리 됩니다 *true* 또는 *1*, 플래그도 처리 하는 다른 모든 값이 설정 되지 됩니다. |
| NUGET_EXE_NO_PROMPT | 자격 증명을 확인 하기 위해 exe를 방지 합니다. | 모든 값으로 null 또는 빈 문자열로 취급 됩니다 점을 제외 하 고이 플래그 집합/true입니다. |
| FORCE_NUGET_EXE_INTERACTIVE | 대화형 모드를 강제로 전역 환경 변수입니다. | 모든 값으로 null 또는 빈 문자열로 취급 됩니다 점을 제외 하 고이 플래그 집합/true입니다. |
| NUGET_PACKAGES | 에 사용할 경로 *전역 패키지* 폴더에 설명 된 대로 [전역 패키지 및 캐시 폴더 관리](../consume-packages/managing-the-global-packages-and-cache-folders.md)합니다. | 절대 경로로 지정 합니다. |
| NUGET_FALLBACK_PACKAGES | 폴더를 패키지 하는 전역 대체 됩니다. | 세미콜론 (;)으로 구분 된 절대 폴더 경로입니다. |
| NUGET_HTTP_CACHE_PATH | 에 사용할 경로 *http 캐시* 폴더에 설명 된 대로 [전역 패키지 및 캐시 폴더 관리](../consume-packages/managing-the-global-packages-and-cache-folders.md)합니다. | 절대 경로로 지정 합니다. |
| NUGET_PERSIST_DG | Dg (MSBuild에서 수집 된 데이터) 파일을 유지 해야 하는 경우를 나타내는 플래그입니다. | 로 지정 된 *true* 또는 *false* (기본값) 이면 NUGET_PERSIST_DG_PATH 설정 하지는 임시 디렉터리 (현재 환경 임시 디렉터리에 NuGetScratch 폴더)에 저장 됩니다. |
| NUGET_PERSIST_DG_PATH | Dg 파일을 유지 하는 경로입니다. | 이 옵션은 절대 경로로 지정, 경우에만 사용된 *NUGET_PERSIST_DG* 설정을 true로 합니다. |
| NUGET_RESTORE_MSBUILD_ARGS | 추가 MSBuild 인수를 설정합니다. | |
| NUGET_RESTORE_MSBUILD_VERBOSITY | MSBuild 로그의 자세한 정도 설정합니다. | 기본값은 *quiet* ("/ v: q"). 가능한 값 *q [uiet]*, *m [inimal]*, *n [ormal]*, *d [etailed]*, 및 *앞에 diag [nostic]* 합니다. |
| NUGET_SHOW_STACK | 전체 예외 스택 추적 등을 사용자에 게 표시 해야 하는지를 결정 합니다. | 로 지정 된 *true* 또는 *false* (기본값). |
| NUGET_XMLDOC_MODE | 어셈블리 XML 설명서 파일 압축 풀기 처리 되는 방법을 결정 합니다. | 지원 되는 모드는 *건너뛸* (XML 문서 파일을 추출 하지 말고) *압축* (zip 보관 파일로 XML 문서 파일을 저장할) 또는 *none* (기본, XML 문서 파일을 일반으로 취급 파일)입니다. |
