---
title: "dotNet NuGet 명령을 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 0c81dbc4-2c14-4ec8-b87a-b802a899c3ea
description: "Dotnet 명령줄 인터페이스를 사용 하 여 NuGet 관련 명령에 대 한 간단한 참조 합니다."
keywords: "dotnet NuGet 명령, dotnet 팩, dotnet 복원, dotnet nuget 지역, dotnet nuget 푸시, dotnet nuget 삭제"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7ff4779f46db102f1384650d82118b34fedd4413
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="dotnet-commands"></a><span data-ttu-id="c776f-104">dotNet 명령</span><span class="sxs-lookup"><span data-stu-id="c776f-104">dotNet commands</span></span>

<span data-ttu-id="c776f-105">Windows, Mac OS X, 및 Linux에서 실행 되는 DotNet 명령줄 인터페이스를 아래에 나열 된 필수 nuget.exe 명령의 수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c776f-105">The DotNet command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="c776f-106">Dotnet 원하는 명령을 제공 하는 경우 nuget.exe 다운로드할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c776f-106">Where dotnet provides the desired commands, it is not necessary to download nuget.exe.</span></span>

- <span data-ttu-id="c776f-107">[**dotnet 팩**](https://docs.microsoft.com/dotnet/core/tools/dotnet-pack?tabs=netcore2x): 팩 코드 NETCore SDK에 대 한 프로젝트 NuGet 패키지에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c776f-107">[**dotnet pack**](https://docs.microsoft.com/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs code for NETCore SDK projects into a NuGet package.</span></span> <span data-ttu-id="c776f-108">다른 모든 프로젝트 유형에 사용 해야[`nuget pack`](cli-ref-pack.md)</span><span class="sxs-lookup"><span data-stu-id="c776f-108">All other project types should use [`nuget pack`](cli-ref-pack.md)</span></span>
- <span data-ttu-id="c776f-109">[**dotnet 복원**](https://docs.microsoft.com/dotnet/core/tools/dotnet-restore?tabs=netcore2x): 종속성과 프로젝트의 도구를 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="c776f-109">[**dotnet restore**](https://docs.microsoft.com/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="c776f-110">동일한 코드를 실행이 NuGet 4.0 이후의 `nuget restore`합니다.</span><span class="sxs-lookup"><span data-stu-id="c776f-110">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="c776f-111">[**dotnet nuget 지역**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-locals):-요청 http와 같은 로컬 NuGet 리소스를 나열 하거나 선택을 취소 캐시, 임시 캐시 또는 시스템 수준의 글로벌 packages 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="c776f-111">[**dotnet nuget locals**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-locals): Clears or lists local NuGet resources such as http the -request cache, temporary cache, or machine-wide global packages folder.</span></span>
- <span data-ttu-id="c776f-112">[**dotnet nuget 푸시**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-push): 서버에 패키지를 푸시를 게시, nuget.org, Visual Studio Team Services 또는 타사 NuGet 서버에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c776f-112">[**dotnet nuget push**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, or any third-party NuGet servers.</span></span>
- <span data-ttu-id="c776f-113">[**dotnet nuget 삭제**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-delete): 하거나 unlists nuget.org, Visual Studio Team Services 또는 타사 NuGet 서버에 적용할 수 있는 서버에서 패키지를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="c776f-113">[**dotnet nuget delete**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a  server, applicable to nuget.org, Visual Studio Team Services, or any third-party NuGet servers.</span></span>
