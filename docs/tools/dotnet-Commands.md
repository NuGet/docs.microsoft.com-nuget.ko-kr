---
title: dotnet NuGet CLI 명령
description: Dotnet 명령줄 인터페이스를 사용 하 여 NuGet 관련 명령에 대 한 간단한 참조입니다.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: ff011e60d3de3b0999db56e1e30e97e538bd9fb4
ms.sourcegitcommit: 2a9d149bc6f5ff76b0b657324820bd0429cddeef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2019
ms.locfileid: "67496474"
---
# <a name="dotnet-cli-commands"></a><span data-ttu-id="d9f53-103">dotnet CLI 명령</span><span class="sxs-lookup"><span data-stu-id="d9f53-103">dotnet CLI commands</span></span>

<span data-ttu-id="d9f53-104">`dotnet` CLI (명령줄 인터페이스), Windows, Mac OS X 및 Linux에서 실행 되는 다양 한 설치, 복원, 패키지 및 게시와 같은 필수 명령 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9f53-104">The `dotnet` command-line interface (CLI), which runs on Windows, Mac OS X, and Linux, provides a number of essential commands such as installing, restoring, and publishing packages.</span></span> <span data-ttu-id="d9f53-105">사용할 필요가 없는 사용자의 요구를 충족 하는 dotnet 경우 `nuget.exe`합니다.</span><span class="sxs-lookup"><span data-stu-id="d9f53-105">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="d9f53-106">이러한 명령을 사용 하 여 패키지의 예제를 참조 하세요 [설치 및 dotnet CLI를 사용 하 여 패키지를 관리](../consume-packages/install-use-packages-dotnet-cli.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d9f53-106">For examples of using these commands to consume packages, see [Install and manage packages using the dotnet CLI](../consume-packages/install-use-packages-dotnet-cli.md).</span></span> <span data-ttu-id="d9f53-107">다음이 명령을 사용 하 여 패키지 예제를 참조 하세요 [만들기 dotnet CLI를 사용 하 여 패키지 및 게시](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d9f53-107">For examples of using these commands to create packages, see [Create and publish a package using the dotnet CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).</span></span>

<span data-ttu-id="d9f53-108">전체 명령 참조 `dotnet` CLI 참조 [.NET Core CLI (명령줄 인터페이스) 도구](/dotnet/core/tools/?tabs=netcore2x)합니다.</span><span class="sxs-lookup"><span data-stu-id="d9f53-108">For the complete command reference on `dotnet` CLI, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="d9f53-109">패키지 사용</span><span class="sxs-lookup"><span data-stu-id="d9f53-109">Package consumption</span></span>

- <span data-ttu-id="d9f53-110">[**패키지를 추가 하는 dotnet**](/dotnet/core/tools/dotnet-add-package): 프로젝트 파일에 대 한 패키지 참조를 추가한 다음 실행 `dotnet restore` 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9f53-110">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="d9f53-111">[**패키지를 제거 하는 dotnet**](/dotnet/core/tools/dotnet-remove-package): 프로젝트 파일에서 패키지 참조를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="d9f53-111">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="d9f53-112">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): 종속성 및 프로젝트의 도구를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="d9f53-112">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="d9f53-113">NuGet 4.0부터 같은 코드 실행이 `nuget restore`합니다.</span><span class="sxs-lookup"><span data-stu-id="d9f53-113">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="d9f53-114">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): 위치를 나열 합니다 *전역 패키지*를 *http 캐시*, 및 *temp* 폴더 및 해당 폴더의 내용 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="d9f53-114">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Lists locations of the *global-packages*, *http-cache*, and *temp* folders and clears the contents of those folders.</span></span>
- <span data-ttu-id="d9f53-115">[**dotnet new nugetconfig**](/dotnet/core/tools/dotnet-new): 만듭니다는 [ `nuget.config` ](../reference/nuget-config-file.md) NuGet의 동작을 구성 하는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d9f53-115">[**dotnet new nugetconfig**](/dotnet/core/tools/dotnet-new): Creates a [`nuget.config`](../reference/nuget-config-file.md) file to configure NuGet's behavior.</span></span>

## <a name="package-creation"></a><span data-ttu-id="d9f53-116">패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="d9f53-116">Package creation</span></span>

- <span data-ttu-id="d9f53-117">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): 코드를 NuGet 패키지로 압축합니다.</span><span class="sxs-lookup"><span data-stu-id="d9f53-117">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span>
- <span data-ttu-id="d9f53-118">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): NuGet 서버에 패키지를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="d9f53-118">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Publishes a package to a NuGet server.</span></span> <span data-ttu-id="d9f53-119">Nuget.org에 Azure 아티팩트에 적용 하 고 [타사 NuGet 서버](../hosting-packages/overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d9f53-119">Applicable to nuget.org, Azure Artifacts, and [third-party NuGet servers](../hosting-packages/overview.md).</span></span>
- <span data-ttu-id="d9f53-120">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): 삭제 하거나 NuGet 서버의 패키지 목록.</span><span class="sxs-lookup"><span data-stu-id="d9f53-120">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a NuGet server.</span></span> <span data-ttu-id="d9f53-121">Nuget.org에 Azure 아티팩트에 적용 하 고 [타사 NuGet 서버](../hosting-packages/overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d9f53-121">Applicable to nuget.org, Azure Artifacts, and [third-party NuGet servers](../hosting-packages/overview.md).</span></span>
