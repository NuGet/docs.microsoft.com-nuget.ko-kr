---
title: NuGet CLI 환경 변수
description: nuget.exe 환경 변수에 대 한 참조
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: a688382420633916e81a000ba6095ff83e036cf9
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779375"
---
# <a name="nuget-cli-environment-variables"></a>NuGet CLI 환경 변수

nuget.exe CLI 동작은 컴퓨터 전체, 사용자 또는 프로세스 수준에 영향을 nuget.exe 주는 여러 가지 환경 변수를 통해 구성할 수 있습니다. 환경 변수는 항상 파일의 설정을 재정의 `NuGet.Config` 하 여 빌드 서버가 파일을 수정 하지 않고 적절 한 설정을 변경할 수 있도록 합니다.

일반적으로 명령줄 또는 NuGet 구성 파일에 직접 지정 된 옵션은 우선적으로 적용 되지만 *FORCE_NUGET_EXE_INTERACTIVE* 와 같은 몇 가지 예외가 있습니다. 여러 컴퓨터 간에 nuget.exe 다르게 동작 하는 경우 환경 변수가 원인일 수 있습니다. 예를 들어 배포 중에 사용 되는 Azure Web Apps Kudu는 패키지 복원 성능을 가속화 하 고 디스크 공간을 절약 하기 위해 *skip* 으로 설정 *NUGET_XMLDOC_MODE* .

NuGet CLI는 MSBuild를 사용 하 여 프로젝트 파일을 읽습니다. 모든 환경 변수는 MSBuild를 평가 하는 동안 [속성](/visualstudio/msbuild/msbuild-command-line-reference) 으로 사용할 수 있습니다.
[MSBuild 대상으로 서의 NuGet pack 및 restore](../msbuild-targets.md#restore-properties) 에 설명 된 속성의 목록을 환경 변수로 설정할 수도 있습니다.

| 변수 | Description | 설명 |
| --- | --- | --- |
| http_proxy | NuGet HTTP 작업에 사용 되는 http 프록시입니다. | 이는로 지정 됩니다 `http://<username>:<password>@proxy.com` . |
| no_proxy | 프록시를 사용 하 여 우회할 도메인을 구성 합니다. | 쉼표로 구분 된 도메인으로 지정 됩니다 (,). |
| EnableNuGetPackageRestore | NuGet이 복원 시 패키지에 필요한 경우 명시적으로 동의를 부여 해야 하는 경우에 대 한 플래그입니다. | 지정 된 플래그는 *true* 또는 *1* 로 처리 되 고 다른 모든 값은 플래그로 설정 되지 않습니다. |
| NUGET_EXE_NO_PROMPT | Exe에서 자격 증명을 묻는 메시지를 표시 하지 않도록 합니다. | Null 또는 빈 문자열을 제외한 모든 값은이 플래그 설정/true로 처리 됩니다. |
| FORCE_NUGET_EXE_INTERACTIVE | 대화형 모드를 적용 하는 전역 환경 변수입니다. | Null 또는 빈 문자열을 제외한 모든 값은이 플래그 설정/true로 처리 됩니다. |
| NUGET_PACKAGES | 전역 [패키지 및 캐시 폴더 관리](../../consume-packages/managing-the-global-packages-and-cache-folders.md)에 설명 된 대로 *전역 패키지* 폴더에 사용할 경로입니다. | 절대 경로로 지정 됩니다. |
| NUGET_FALLBACK_PACKAGES | 전역 대체 패키지 폴더. | 세미콜론으로 구분 된 절대 폴더 경로 (;)입니다. |
| NUGET_HTTP_CACHE_PATH | [전역 패키지 및 캐시 폴더 관리](../../consume-packages/managing-the-global-packages-and-cache-folders.md)에 설명 된 대로 *http 캐시* 폴더에 사용할 경로입니다. | 절대 경로로 지정 됩니다. |
| NUGET_PERSIST_DG | Dg 파일 (MSBuild에서 수집 된 데이터)을 유지할지 여부를 나타내는 플래그입니다. | *True* 또는 *false* (기본값)로 지정 합니다. NUGET_PERSIST_DG_PATH 설정 하지 않으면 임시 디렉터리 (현재 환경 임시 디렉터리의 NuGetScratch 폴더)에 저장 됩니다. |
| NUGET_PERSIST_DG_PATH | Dg 파일을 유지할 경로입니다. | 절대 경로로 지정 됩니다 .이 옵션은 *NUGET_PERSIST_DG* 이 true로 설정 된 경우에만 사용 됩니다. |
| NUGET_RESTORE_MSBUILD_ARGS | 추가 MSBuild 인수를 설정 합니다. | 인수를 msbuild.exe 전달 하는 방법과 동일 하 게 전달 합니다. 명령줄에서 값 막대로 프로젝트 속성 Foo를 설정 하는 예제는/p: Foo = Bar입니다. |
| NUGET_RESTORE_MSBUILD_VERBOSITY | MSBuild 로그의 자세한 정도를 설정 합니다. | 기본값은 *quiet* ("/v: q")입니다. 가능한 값 *q [uiet]*, *m [inimal]*, *n [ormal]*, *d [etailed]* 및 *diag [nostic]*. |
| NUGET_SHOW_STACK | 전체 예외 (스택 추적 포함)를 사용자에 게 표시할지 여부를 결정 합니다. | *True* 또는 *false* (기본값)로 지정 됩니다. |
| NUGET_XMLDOC_MODE | 어셈블리 XML 문서 파일 추출을 처리 하는 방법을 결정 합니다. | 지원 되는 모드는 *skip* (xml 문서 파일을 추출 하지 않음), *압축* (xml doc 파일을 zip 보관 파일로 저장) 또는 *없음* (기본값은 xml 문서 파일을 일반 파일로 처리)입니다. |
| NUGET_CERT_REVOCATION_MODE | 서명 된 패키지를 설치 하거나 복원할 때 패키지에 서명 하는 데 사용 되는 인증서의 해지 상태 검사가 수행 되는 방법을 결정 합니다. 설정 하지 않으면 기본적으로로 설정 `online` 됩니다.| *온라인* (기본값), *오프 라인* 값을 사용할 수 있습니다.  [NU3028](../errors-and-warnings/NU3028.md) 관련 |

