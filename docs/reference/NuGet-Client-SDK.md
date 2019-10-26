---
title: NuGet 클라이언트 SDK
description: API는 아직 문서화 되지 않고 진화 하 고 있지만 예제는 Dave Glick 위한 블로그에서 사용할 수 있습니다.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 873bde467a39653b818b49173d53bc983e99d1b9
ms.sourcegitcommit: f9645fc5f49c18978e12a292a3f832e162e069d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/25/2019
ms.locfileid: "72924611"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="60cc7-103">NuGet 클라이언트 SDK</span><span class="sxs-lookup"><span data-stu-id="60cc7-103">NuGet Client SDK</span></span>

<span data-ttu-id="60cc7-104">Nuget *클라이언트 SDK* 는 Nuget. [명령](https://www.nuget.org/packages/NuGet.Commands), [nuget. 패키징](https://www.nuget.org/packages/NuGet.Packaging)및 [nuget. 프로토콜](https://www.nuget.org/packages/NuGet.Protocol)을 중심으로 하는 nuget 패키지 그룹을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="60cc7-104">The *NuGet Client SDK* refers to a group of NuGet packages centered around [NuGet.Commands](https://www.nuget.org/packages/NuGet.Commands), [NuGet.Packaging](https://www.nuget.org/packages/NuGet.Packaging), and [NuGet.Protocol](https://www.nuget.org/packages/NuGet.Protocol).</span></span> <span data-ttu-id="60cc7-105">이러한 패키지는 이전 [NuGet. 핵심](https://www.nuget.org/packages/NuGet.Core/) 라이브러리를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="60cc7-105">These packages replace the earlier [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/) library.</span></span>

> [!Note]
>  <span data-ttu-id="60cc7-106">NuGet 서버 프로토콜에 대 한 설명서는 [Nuget 서버 API](~/api/overview.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="60cc7-106">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="source-code"></a><span data-ttu-id="60cc7-107">소스 코드</span><span class="sxs-lookup"><span data-stu-id="60cc7-107">Source code</span></span>

<span data-ttu-id="60cc7-108">소스 코드는 GitHub의 프로젝트 [nuget/NuGet. 클라이언트](https://github.com/NuGet/NuGet.Client)에서 게시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="60cc7-108">The source code is published on GitHub in the project [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client).</span></span>

## <a name="third-party-documentation"></a><span data-ttu-id="60cc7-109">타사 설명서</span><span class="sxs-lookup"><span data-stu-id="60cc7-109">Third-party documentation</span></span>

<span data-ttu-id="60cc7-110">다음 블로그 시리즈의 일부 API에 대 한 예제 및 설명서는 2016 게시에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60cc7-110">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="60cc7-111">NuGet v3 라이브러리 탐색, 1 부: 소개 및 개념</span><span class="sxs-lookup"><span data-stu-id="60cc7-111">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="60cc7-112">NuGet v3 라이브러리 탐색, 2 부: 패키지 검색</span><span class="sxs-lookup"><span data-stu-id="60cc7-112">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="60cc7-113">NuGet v3 라이브러리 탐색, 3 부: 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="60cc7-113">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="60cc7-114">이러한 블로그 게시물은 NuGet 클라이언트 SDK 패키지의 **3.4.3** 버전이 릴리스된 직후에 작성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="60cc7-114">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="60cc7-115">최신 버전의 패키지가 블로그 게시물의 정보와 호환 되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60cc7-115">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="60cc7-116">Martin Björkström는 nuget 패키지 설치에 NuGet 클라이언트 SDK를 사용 하는 다른 방법을 소개 하는 Dave Glick의 블로그 시리즈에 대 한 후속 블로그 게시물을 제공 했습니다.</span><span class="sxs-lookup"><span data-stu-id="60cc7-116">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK for installing NuGet packages:</span></span>

- [<span data-ttu-id="60cc7-117">NuGet v3 라이브러리를 방문 합니다.</span><span class="sxs-lookup"><span data-stu-id="60cc7-117">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
