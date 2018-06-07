---
title: dotnet NuGet 명령
description: Dotnet 명령줄 인터페이스를 사용 하 여 NuGet 관련 명령에 대 한 간단한 참조 합니다.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/23/2018
ms.topic: conceptual
ms.openlocfilehash: dd30c5d5e29ff7ef7c6622a9b93c32b908198d52
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817023"
---
# <a name="dotnet-commands"></a>dotnet 명령

`dotnet` 아래와 같이 명령줄 인터페이스에서 Windows, Mac OS X, 및 Linux에서 실행 되는 다양 한 필수 nuget.exe 명령을 제공 합니다. 사용할 필요가 없다는 사용자의 요구를 충족 하는 dotnet 경우 `nuget.exe`합니다.

대 한 자세한 내용은 `dotnet`, 참조 [.NET Core CLI (명령줄 인터페이스) 도구](/dotnet/core/tools/?tabs=netcore2x)합니다.

## <a name="package-consumption"></a>패키지 사용

- [**패키지를 추가 하는 dotnet**](/dotnet/core/tools/dotnet-add-package): 실행 한 후 프로젝트 파일에 대 한 패키지 참조 추가 `dotnet restore` 패키지를 설치 합니다.
- [**패키지를 제거 하는 dotnet**](/dotnet/core/tools/dotnet-remove-package): 프로젝트 파일에서 패키지 참조를 제거 합니다.
- [**dotnet 복원**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): 종속성과 프로젝트의 도구를 복원 합니다. 동일한 코드를 실행이 NuGet 4.0 이후의 `nuget restore`합니다.
- [**dotnet nuget 지역**](/dotnet/core/tools/dotnet-nuget-locals):의 위치를 나열는 *전역 패키지*, *http 캐시*, 및 *temp* 폴더의 내용을 지웁니다. 이러한 폴더입니다.

## <a name="package-creation"></a>패키지 만들기

- [**dotnet 팩**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): NuGet 패키지에는 코드를 압축 합니다. 동일한 코드를 실행이 NuGet 4.0 이후의 `nuget pack`합니다.
- [**dotnet nuget 푸시**](/dotnet/core/tools/dotnet-nuget-push): 서버에 패키지를 푸시를 게시, nuget.org, Visual Studio Team Services 및 제 3 자 NuGet 서버에 적용 합니다.
- [**dotnet nuget 삭제**](/dotnet/core/tools/dotnet-nuget-delete): nuget.org, Visual Studio Team Services 및 제 3 자 NuGet 서버에 적용 되는 호스트에서 패키지를 unlists 하거나 삭제 합니다.
