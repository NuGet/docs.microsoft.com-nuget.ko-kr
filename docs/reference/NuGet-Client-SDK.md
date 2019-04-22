---
title: NuGet 클라이언트 SDK
description: API가 진화 하 고 아직 문서화 하지도 예제 Dave Glick 블로그에서 사용할 수 있습니다.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 8f96bf289e8121fd25262fb95c2f36dfc89045c5
ms.sourcegitcommit: 573af6133a39601136181c1d98c09303f51a1ab2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "58911038"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="1fc1e-103">NuGet 클라이언트 SDK</span><span class="sxs-lookup"><span data-stu-id="1fc1e-103">NuGet Client SDK</span></span>

> [!Note]
> <span data-ttu-id="1fc1e-104">혼동 해서는 합니다 [NuGet *웹* API](https://docs.microsoft.com/en-us/nuget/api/overview)</span><span class="sxs-lookup"><span data-stu-id="1fc1e-104">Not to be confused with the [NuGet *Web* API](https://docs.microsoft.com/en-us/nuget/api/overview)</span></span>

<span data-ttu-id="1fc1e-105">합니다 *NuGet 클라이언트 SDK* 중심으로 하는.NET 라이브러리 그룹을 가리키는 [NuGet.Commands](https://www.nuget.org/packages/NuGet.Commands)를 [Nuget.Packaging](https://www.nuget.org/packages/NuGet.Packaging), 및 [NuGet.Protocol](https://www.nuget.org/packages/NuGet.Protocol).</span><span class="sxs-lookup"><span data-stu-id="1fc1e-105">The *NuGet Client SDK* refers to a group of .NET libraries centered around [NuGet.Commands](https://www.nuget.org/packages/NuGet.Commands), [Nuget.Packaging](https://www.nuget.org/packages/NuGet.Packaging), and [NuGet.Protocol](https://www.nuget.org/packages/NuGet.Protocol).</span></span> <span data-ttu-id="1fc1e-106">이러한 패키지는 이전 바꿉니다 [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/) 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="1fc1e-106">These packages replace the earlier [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/) library.</span></span>

<span data-ttu-id="1fc1e-107">곧 설명 되어 있습니다 노출 영역을 안정적으로 노력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc1e-107">We are working on having a stable surface area that we can document soon.</span></span>

## <a name="source-code"></a><span data-ttu-id="1fc1e-108">소스 코드</span><span class="sxs-lookup"><span data-stu-id="1fc1e-108">Source code</span></span>

<span data-ttu-id="1fc1e-109">소스 코드 프로젝트에서 GitHub에 게시 됩니다 [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client)합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc1e-109">The source code is published on GitHub in the project [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client).</span></span>

## <a name="third-party-documentation"></a><span data-ttu-id="1fc1e-110">공급 업체의 설명서</span><span class="sxs-lookup"><span data-stu-id="1fc1e-110">Third-party documentation</span></span>

<span data-ttu-id="1fc1e-111">Dave Glick, 2016을 게시 하 여 다음 블로그 시리즈의 예제 및 API의 일부에 대 한 설명서를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fc1e-111">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="1fc1e-112">NuGet v3 라이브러리, 1 부를 탐색 합니다. 소개 및 개념</span><span class="sxs-lookup"><span data-stu-id="1fc1e-112">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="1fc1e-113">NuGet v3 라이브러리, 2 부를 탐색 합니다. 패키지에 대 한 검색</span><span class="sxs-lookup"><span data-stu-id="1fc1e-113">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="1fc1e-114">NuGet v3 라이브러리, 3 부를 탐색 합니다. 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="1fc1e-114">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="1fc1e-115">직후 작성 된 다음 블로그 게시물을 **3.4.3** 클라이언트 SDK 패키지 새로 릴리스된 NuGet의 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="1fc1e-115">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="1fc1e-116">최신 버전의 패키지를 블로그 게시물의 정보를 사용 하 여 호환 되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fc1e-116">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="1fc1e-117">Martin Björkström NuGet 클라이언트 SDK를 사용 하 여 NuGet 패키지를 설치 하는 것에 대 한 다른 접근 방법이 도입 되었습니다 그 위치 Dave Glick 블로그 시리즈를 후속 블로그 게시물을 수행 했습니다.</span><span class="sxs-lookup"><span data-stu-id="1fc1e-117">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK for installing NuGet packages:</span></span>

- [<span data-ttu-id="1fc1e-118">NuGet v3 라이브러리를 다시 방문</span><span class="sxs-lookup"><span data-stu-id="1fc1e-118">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
