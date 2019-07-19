---
title: dotnet CLI NuGet 명령
description: Dotnet 명령줄 인터페이스를 사용 하는 NuGet 관련 명령에 대 한 간단한 참조입니다.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: ff011e60d3de3b0999db56e1e30e97e538bd9fb4
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327490"
---
# <a name="dotnet-cli-commands"></a>dotnet CLI 명령

Windows `dotnet` , Mac OS X 및 Linux에서 실행 되는 CLI (명령줄 인터페이스)는 패키지 설치, 복원 및 게시와 같은 몇 가지 필수 명령을 제공 합니다. Dotnet이 요구를 충족 하는 경우에는를 사용할 `nuget.exe`필요가 없습니다.

이러한 명령을 사용 하 여 패키지를 사용 하는 예제는 [DOTNET CLI를 사용 하 여 패키지 설치 및 관리](../consume-packages/install-use-packages-dotnet-cli.md)를 참조 하세요. 이러한 명령을 사용 하 여 패키지를 만드는 예는 [DOTNET CLI를 사용 하 여 패키지 만들기 및 게시](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)를 참조 하세요.

Cli에 대 `dotnet` 한 전체 명령 참조는 [.net Core cli (명령줄 인터페이스) 도구](/dotnet/core/tools/?tabs=netcore2x)를 참조 하세요.

## <a name="package-consumption"></a>패키지 사용

- [**dotnet 패키지 추가**](/dotnet/core/tools/dotnet-add-package): 패키지 참조를 프로젝트 파일에 추가한 다음를 실행 `dotnet restore` 하 여 패키지를 설치 합니다.
- [**dotnet 패키지 제거**](/dotnet/core/tools/dotnet-remove-package): 프로젝트 파일에서 패키지 참조를 제거 합니다.
- [**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): 프로젝트의 종속성 및 도구를 복원 합니다. NuGet 4.0부터 `nuget restore`와 같은 코드가 실행됩니다.
- [**dotnet nuget 로컬**](/dotnet/core/tools/dotnet-nuget-locals): *전역 패키지*, *http 캐시*및 *임시* 폴더의 위치를 나열 하 고 해당 폴더의 내용을 지웁니다.
- [**dotnet new nugetconfig**](/dotnet/core/tools/dotnet-new): NuGet의 [`nuget.config`](../reference/nuget-config-file.md) 동작을 구성 하는 파일을 만듭니다.

## <a name="package-creation"></a>패키지 만들기

- [**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): 코드를 NuGet 패키지로 압축 합니다.
- [**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): NuGet 서버에 패키지를 게시 합니다. Nuget.org, Azure Artifacts 및 [타사 nuget 서버](../hosting-packages/overview.md)에 적용 됩니다.
- [**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): NuGet 서버에서 패키지를 삭제 하거나 목록에서 제거 합니다. Nuget.org, Azure Artifacts 및 [타사 nuget 서버](../hosting-packages/overview.md)에 적용 됩니다.
