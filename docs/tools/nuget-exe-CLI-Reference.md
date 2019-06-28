---
title: NuGet CLI (명령줄 인터페이스) 참조
description: Nuget.exe CLI에 대 한 명령줄 참조 인덱스
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: reference
ms.openlocfilehash: a257dbbd9d56b5989e050ed4096d096cd1036184
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426020"
---
# <a name="nuget-cli-reference"></a>NuGet CLI 참조

NuGet 명령줄 인터페이스 (CLI) `nuget.exe`, 설치, 만들기, 게시 및 프로젝트 파일을 변경 하지 않고 패키지를 관리 하는 NuGet 기능 전체 범위를 제공 합니다.

모든 명령을 사용 하려면 명령 창 또는 bash 셸을 열고 실행 `nuget` 뒤에 명령 및 적절 한 옵션을 같은 `nuget help pack` (도움말을 보려면 pack 명령에서).

이 설명서는 최신 버전의 NuGet CLI를 반영합니다. 사용 중인 모든 지정 된 버전에 대 한 정확한 세부 정보에 대 한 실행 `nuget help` 원하는 명령에 대 한 합니다.

함께 기본 명령을 사용 하는 방법을 알아보려면 합니다 `nuget.exe` CLI 참조 [설치 nuget.exe CLI를 사용 하 여 패키지를 사용 하 여](../consume-packages/install-use-packages-nuget-cli.md)입니다.

## <a name="installing-nugetexe"></a>Nuget.exe를 설치합니다.

[!INCLUDE [install-cli](../includes/install-cli.md)]

> [!Tip]
> NuGet CLI를 사용할 수 있도록 패키지 관리자 콘솔 내에서 Visual Studio에서를 참조 하세요 [콘솔에서 nuget.exe CLI를 사용 하 여](package-manager-console.md#using-the-nugetexe-cli-in-the-console)입니다.

## <a name="availability"></a>가용성

참조 [기능 가용성](../install-nuget-client-tools.md#feature-availability) 정확한 세부 정보에 대 한 합니다.

- Windows에서 모든 명령을 사용할 수 있습니다.
- Nuget.exe에 대 한 지정 된 경우를 제외 하 고 Mono에서 실행 중인 모든 명령이 작동 `pack`, `restore`, 및 `update`합니다.
- 합니다 `pack`, `restore`를 `delete`를 `locals`, 및 `push` 명령을 dotnet CLI 통해 Mac 및 Linux에서 사용할 수 있습니다.

## <a name="commands-and-applicability"></a>명령 및 적용 가능성

사용 가능한 명령 및 적용 가능성 패키지 만들기, 패키지 사용 및/또는 호스트에 패키지를 게시 합니다.

| 일반적인 명령 | 해당 하는 역할 | NuGet 버전 | 설명 |
| --- | --- | --- | --- |
| [pack](cli-ref-pack.md) | 만들기 | 2.7+ | NuGet 패키지를 만들어는 `.nuspec` 또는 프로젝트 파일입니다. Mono에서 실행 하는 경우 프로젝트 파일에서 패키지를 만드는 지원 되지 않습니다. |
| [push](cli-ref-push.md) | 게시 | 모두 | 패키지 원본에 패키지를 게시합니다. |
| [config](cli-ref-config.md) | 모두 | 모두 | NuGet 구성 값을 불러오거나 설정할 수 있습니다. |
| [help or ?](cli-ref-help.md) | 모두 | 모두 | 도움말 정보 또는 명령에 대 한 도움말을 표시 합니다. |
| [locals](cli-ref-locals.md) | 사용 | 3.3+ | 위치를 나열 합니다 *전역 패키지*를 *http 캐시*, 및 *temp* 폴더 및 해당 폴더의 내용 지웁니다. |
| [restore](cli-ref-restore.md) | 사용 | 2.7+ | 사용 중인 패키지 관리 형식에서 참조 하는 모든 패키지를 복원 합니다. Mono에서 실행 하는 경우 PackageReference 형식을 사용 하 여 패키지 복원 지원 되지 않습니다. |
| [setapikey](cli-ref-setapikey.md) | 게시와 소비 | 모두 | 해당 패키지 원본에 대 한 액세스 키가 필요 하면 지정 된 패키지 소스에 대 한 API 키를 저장 합니다. |
| [spec](cli-ref-spec.md) | 만들기 | 모두 | 생성을 `.nuspec` 파일을 Visual Studio 프로젝트에서 파일을 생성 하는 경우 토큰을 사용 합니다. |

| 보조 명령 | 해당 하는 역할 | NuGet 버전 | 설명 |
| --- | --- | --- | --- |
| [add](cli-ref-add.md) | 게시 | 3.3+ | 계층형 레이아웃을 사용 하 여 비 HTTP 패키지 소스에 패키지를 추가 합니다. HTTP 원본에 대해 *푸시*합니다. |
| [delete](cli-ref-delete.md) | 게시 | 모두 | 제거 하거나 패키지 소스에서 패키지 목록에서 제거 합니다. |
| [init](cli-ref-init.md) | 만들기 | 3.3+ | 계층형 레이아웃을 사용 하 여 패키지 원본 폴더에서 패키지를 추가 합니다. |
| [install](cli-ref-install.md) | 사용 | 모두 | 현재 패키지 설치 프로젝트 하지만 프로젝트를 수정 하거나 파일을 참조할지 않습니다. |
| [list](cli-ref-list.md) | 아마도 게시 사용 | 모두 | 지정된 된 원본에서 패키지를 표시합니다. |
| [mirror](cli-ref-mirror.md) | 게시 | 3\.2 이상에서 사용 되지 않음 | 패키지 및 대상 리포지토리를 원본에서 해당 종속성을 미러링합니다. |
| [sources](cli-ref-sources.md) | 소비, 게시 | 모두 | 구성 파일에서 패키지 소스를 관리합니다. |
| [update](cli-ref-update.md) | 사용 | 모두 | 사용 가능한 최신 버전을 프로젝트의 패키지를 업데이트합니다. Mono에서 실행 하는 경우 지원 되지 않습니다. |

다른 명령을 확인 다양 한 활용 [환경 변수](cli-ref-environment-variables.md)합니다.

해당 하는 역할에서 NuGet CLI 명령:

| 역할 | 명령 |
| --- | --- |
| 사용 | `config`, `help`, `install`, `list`, `locals`, `restore`, `setapikey`, `sources`, `update` |
| 만들기 | `config`, `help`, `init`, `pack`, `spec` |
| 게시 | `add`, `config`, `delete`, `help`, `list`, `push`, `setapikey`, `sources` |

예를 들어, 패키지 사용에 관련된 개발자는 NuGet 명령 하위 집합을 파악만 필요 합니다.

> [!Note]
> 명령 옵션 이름은 대/소문자를 구분 하지 않습니다. 사용 되지 않는 옵션에에서 포함 되지 않은이 참조와 같은 `NoPrompt` (바뀝니다 `NonInteractive`) 및 `Verbose` (바뀝니다 `Verbosity`).
