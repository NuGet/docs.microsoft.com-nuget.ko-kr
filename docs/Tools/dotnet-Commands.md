---
title: "dotNet NuGet 명령을 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Dotnet 명령줄 인터페이스를 사용 하 여 NuGet 관련 명령에 대 한 간단한 참조 합니다."
keywords: "dotnet NuGet 명령, dotnet 팩, dotnet 복원, dotnet nuget 지역, dotnet nuget 푸시, dotnet nuget 삭제"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2851938cd43b35454d8e4ad595fbd93229d4dd72
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/20/2018
---
# <a name="dotnet-commands"></a><span data-ttu-id="d21e0-104">dotNet 명령</span><span class="sxs-lookup"><span data-stu-id="d21e0-104">dotNet commands</span></span>

<span data-ttu-id="d21e0-105">`dotnet` 아래와 같이 명령줄 인터페이스에서 Windows, Mac OS X, 및 Linux에서 실행 되는 다양 한 필수 nuget.exe 명령을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d21e0-105">The `dotnet` command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="d21e0-106">사용할 필요가 없다는 사용자의 요구를 충족 하는 dotnet 경우 `nuget.exe`합니다.</span><span class="sxs-lookup"><span data-stu-id="d21e0-106">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="d21e0-107">대 한 자세한 내용은 `dotnet`, 참조 [.NET Core CLI (명령줄 인터페이스) 도구](/dotnet/core/tools/?tabs=netcore2x)합니다.</span><span class="sxs-lookup"><span data-stu-id="d21e0-107">For complete information on `dotnet`, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="d21e0-108">패키지 사용</span><span class="sxs-lookup"><span data-stu-id="d21e0-108">Package consumption</span></span>

- <span data-ttu-id="d21e0-109">[**패키지를 추가 하는 dotnet**](/dotnet/core/tools/dotnet-add-package): 실행 한 후 프로젝트 파일에 대 한 패키지 참조 추가 `dotnet restore` 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="d21e0-109">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="d21e0-110">[**패키지를 제거 하는 dotnet**](/dotnet/core/tools/dotnet-remove-package): 프로젝트 파일에서 패키지 참조를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="d21e0-110">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="d21e0-111">[**dotnet 복원**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): 종속성과 프로젝트의 도구를 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="d21e0-111">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="d21e0-112">동일한 코드를 실행이 NuGet 4.0 이후의 `nuget restore`합니다.</span><span class="sxs-lookup"><span data-stu-id="d21e0-112">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="d21e0-113">[**dotnet nuget 지역**](/dotnet/core/tools/dotnet-nuget-locals): http 요청 캐시, 임시 캐시 및 시스템 수준의 글로벌 패키지 폴더와 같은 로컬 NuGet 리소스를 나열 하거나 선택을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="d21e0-113">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Clears or lists local NuGet resources such as the http-request cache, the temporary cache, and the machine-wide global packages folder.</span></span>

## <a name="package-creation"></a><span data-ttu-id="d21e0-114">패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="d21e0-114">Package creation</span></span>

- <span data-ttu-id="d21e0-115">[**dotnet 팩**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): NuGet 패키지에는 코드를 압축 합니다.</span><span class="sxs-lookup"><span data-stu-id="d21e0-115">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="d21e0-116">동일한 코드를 실행이 NuGet 4.0 이후의 `nuget pack`합니다.</span><span class="sxs-lookup"><span data-stu-id="d21e0-116">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="d21e0-117">[**dotnet nuget 푸시**](/dotnet/core/tools/dotnet-nuget-push): 서버에 패키지를 푸시를 게시, nuget.org, Visual Studio Team Services 및 제 3 자 NuGet 서버에 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d21e0-117">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
- <span data-ttu-id="d21e0-118">[**dotnet nuget 삭제**](/dotnet/core/tools/dotnet-nuget-delete): nuget.org, Visual Studio Team Services 및 제 3 자 NuGet 서버에 적용 되는 호스트에서 패키지를 unlists 하거나 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="d21e0-118">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a host, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
