---
title: dotnet NuGet 명령
description: Dotnet 명령줄 인터페이스를 사용 하 여 NuGet 관련 명령에 대 한 간단한 참조입니다.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: conceptual
ms.openlocfilehash: 88e058be674ecddc500665bfa3517f19acde0cd7
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546318"
---
# <a name="dotnet-commands"></a><span data-ttu-id="a6418-103">dotnet 명령</span><span class="sxs-lookup"><span data-stu-id="a6418-103">dotnet commands</span></span>

<span data-ttu-id="a6418-104">`dotnet` Windows, Mac OS X 및 Linux에서 실행 되는 명령줄 인터페이스를 아래에 나열 된 필수 nuget.exe 명령의 수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6418-104">The `dotnet` command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="a6418-105">사용할 필요가 없는 사용자의 요구를 충족 하는 dotnet 경우 `nuget.exe`합니다.</span><span class="sxs-lookup"><span data-stu-id="a6418-105">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="a6418-106">에 대 한 자세한 `dotnet`를 참조 하세요 [.NET Core CLI (명령줄 인터페이스) 도구](/dotnet/core/tools/?tabs=netcore2x)합니다.</span><span class="sxs-lookup"><span data-stu-id="a6418-106">For complete information on `dotnet`, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="a6418-107">패키지 사용</span><span class="sxs-lookup"><span data-stu-id="a6418-107">Package consumption</span></span>

- <span data-ttu-id="a6418-108">[**dotnet 패키지 추가**](/dotnet/core/tools/dotnet-add-package): 프로젝트 파일에 대 한 패키지 참조를 추가한 다음 실행 `dotnet restore` 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6418-108">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="a6418-109">[**패키지를 제거 하는 dotnet**](/dotnet/core/tools/dotnet-remove-package): 프로젝트 파일에서 패키지 참조를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6418-109">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="a6418-110">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): 종속성 및 프로젝트의 도구를 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6418-110">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="a6418-111">NuGet 4.0부터 같은 코드 실행이 `nuget restore`합니다.</span><span class="sxs-lookup"><span data-stu-id="a6418-111">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="a6418-112">[**dotnet nuget 지역**](/dotnet/core/tools/dotnet-nuget-locals): 위치를 나열 합니다 *전역 패키지*를 *http 캐시*, 및 *temp* 폴더의 내용을 지우고 및 해당 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="a6418-112">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Lists locations of the *global-packages*, *http-cache*, and *temp* folders and clears the contents of those folders.</span></span>

## <a name="package-creation"></a><span data-ttu-id="a6418-113">패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="a6418-113">Package creation</span></span>

- <span data-ttu-id="a6418-114">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): 코드를 NuGet 패키지로 압축 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6418-114">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="a6418-115">NuGet 4.0부터 같은 코드 실행이 `nuget pack`합니다.</span><span class="sxs-lookup"><span data-stu-id="a6418-115">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="a6418-116">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): 서버에 패키지를 푸시하고 게시, nuget.org, Visual Studio Team Services 및 타사 NuGet 서버에 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6418-116">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
- <span data-ttu-id="a6418-117">[**dotnet nuget 삭제할**](/dotnet/core/tools/dotnet-nuget-delete): 삭제 패키지 하거나 목록에서 호스트에서 nuget.org, Visual Studio Team Services 및 타사 NuGet 서버에 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6418-117">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a host, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
