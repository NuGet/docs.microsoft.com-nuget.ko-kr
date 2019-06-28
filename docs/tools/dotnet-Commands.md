---
title: dotnet NuGet CLI 명령
description: Dotnet 명령줄 인터페이스를 사용 하 여 NuGet 관련 명령에 대 한 간단한 참조입니다.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: cc99b327c0edb4aeb573dfa8c2f9b9dba7b8cc38
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426012"
---
# <a name="dotnet-cli-commands"></a>dotnet CLI 명령

`dotnet` CLI (명령줄 인터페이스), Windows, Mac OS X 및 Linux에서 실행 되는 다양 한 설치, 복원, 패키지 및 게시와 같은 필수 명령 제공 합니다. 사용할 필요가 없는 사용자의 요구를 충족 하는 dotnet 경우 `nuget.exe`합니다.

이러한 명령을 사용 하 여 패키지의 예제를 참조 하세요 [설치 및 dotnet CLI를 사용 하 여 패키지를 관리](../consume-packages/install-use-packages-dotnet-cli.md)합니다. 다음이 명령을 사용 하 여 패키지 예제를 참조 하세요. [만들기 dotnet CLI를 사용 하 여 패키지 및 게시]... / quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).

전체 명령 참조 `dotnet` CLI 참조 [.NET Core CLI (명령줄 인터페이스) 도구](/dotnet/core/tools/?tabs=netcore2x)합니다.

## <a name="package-consumption"></a>패키지 사용

- [**패키지를 추가 하는 dotnet**](/dotnet/core/tools/dotnet-add-package): 프로젝트 파일에 대 한 패키지 참조를 추가한 다음 실행 `dotnet restore` 패키지를 설치 합니다.
- [**패키지를 제거 하는 dotnet**](/dotnet/core/tools/dotnet-remove-package): 프로젝트 파일에서 패키지 참조를 제거합니다.
- [**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): 종속성 및 프로젝트의 도구를 복원합니다. NuGet 4.0부터 같은 코드 실행이 `nuget restore`합니다.
- [**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): 위치를 나열 합니다 *전역 패키지*를 *http 캐시*, 및 *temp* 폴더 및 해당 폴더의 내용 지웁니다.

## <a name="package-creation"></a>패키지 만들기

- [**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): 코드를 NuGet 패키지로 압축합니다. NuGet 4.0부터 같은 코드 실행이 `nuget pack`합니다.
- [**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): 서버에 패키지를 푸시하고 게시, nuget.org, Visual Studio Team Services 및 타사 NuGet 서버에 적용 합니다.
- [**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): 삭제 하거나 호스트에서 nuget.org, Visual Studio Team Services 및 타사 NuGet 서버에 적용 된 패키지 목록.
