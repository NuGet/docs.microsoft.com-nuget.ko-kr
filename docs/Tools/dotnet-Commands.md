---
title: "dotNet NuGet 명령을 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Dotnet 명령줄 인터페이스를 사용 하 여 NuGet 관련 명령에 대 한 간단한 참조 합니다."
keywords: "dotnet NuGet 명령, dotnet 팩, dotnet 복원, dotnet nuget 지역, dotnet nuget 푸시, dotnet nuget 삭제"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: d06e4590ab87b68e7846a13b2eba0f59eb9529d6
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="dotnet-commands"></a><span data-ttu-id="d9266-104">dotNet 명령</span><span class="sxs-lookup"><span data-stu-id="d9266-104">dotNet commands</span></span>

<span data-ttu-id="d9266-105">Windows, Mac OS X, 및 Linux에서 실행 되는 DotNet 명령줄 인터페이스를 아래에 나열 된 필수 nuget.exe 명령의 수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9266-105">The DotNet command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="d9266-106">Dotnet 원하는 명령을 제공 하는 경우 nuget.exe 다운로드할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d9266-106">Where dotnet provides the desired commands, it's not necessary to download nuget.exe.</span></span>

- <span data-ttu-id="d9266-107">[**dotnet 팩**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): NuGet 패키지에는 코드를 압축 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9266-107">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="d9266-108">동일한 코드를 실행이 NuGet 4.0 이후의 `nuget pack`합니다.</span><span class="sxs-lookup"><span data-stu-id="d9266-108">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="d9266-109">[**dotnet 복원**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): 종속성과 프로젝트의 도구를 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9266-109">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="d9266-110">동일한 코드를 실행이 NuGet 4.0 이후의 `nuget restore`합니다.</span><span class="sxs-lookup"><span data-stu-id="d9266-110">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="d9266-111">[**dotnet nuget 지역**](/dotnet/core/tools/dotnet-nuget-locals):-요청 http와 같은 로컬 NuGet 리소스를 나열 하거나 선택을 취소 캐시, 임시 캐시 또는 시스템 수준의 글로벌 packages 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="d9266-111">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Clears or lists local NuGet resources such as http the -request cache, temporary cache, or machine-wide global packages folder.</span></span>
- <span data-ttu-id="d9266-112">[**dotnet nuget 푸시**](/dotnet/core/tools/dotnet-nuget-push): 서버에 패키지를 푸시를 게시, nuget.org, Visual Studio Team Services 또는 타사 NuGet 서버에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9266-112">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, or any third-party NuGet servers.</span></span>
- <span data-ttu-id="d9266-113">[**dotnet nuget 삭제**](/dotnet/core/tools/dotnet-nuget-delete): 하거나 unlists nuget.org, Visual Studio Team Services 또는 타사 NuGet 서버에 적용할 수 있는 서버에서 패키지를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9266-113">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a  server, applicable to nuget.org, Visual Studio Team Services, or any third-party NuGet servers.</span></span>
