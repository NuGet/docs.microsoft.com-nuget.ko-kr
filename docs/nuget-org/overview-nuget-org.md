---
title: NuGet.org의 개요
description: NuGet.org의 개요
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 9a75ecbc589afa664e5684005e077b02913e8039
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427018"
---
# <a name="overview-of-nugetorg"></a><span data-ttu-id="1dbac-103">NuGet.org의 개요</span><span class="sxs-lookup"><span data-stu-id="1dbac-103">Overview of NuGet.org</span></span>

<span data-ttu-id="1dbac-104">NuGet.org는 매일 수백만 명의 .NET 및 .NET Core 개발자가 이용하는 NuGet 패키지의 공용 호스트입니다.</span><span class="sxs-lookup"><span data-stu-id="1dbac-104">NuGet.org is a public host of NuGet packages that are employed by millions of .NET and .NET Core developers every day.</span></span>

## <a name="role-of-nugetorg-in-the-nuget-ecosystem"></a><span data-ttu-id="1dbac-105">NuGet 에코시스템에서의 NuGet.org의 역할</span><span class="sxs-lookup"><span data-stu-id="1dbac-105">Role of NuGet.org in the NuGet ecosystem</span></span>

<span data-ttu-id="1dbac-106">공용 호스트로서의 역할에서 NuGet.org 자체는 [nuget.org](https://www.nuget.org)에 100,000개가 넘는 고유한 패키지의 중앙 리포지토리를 유지 관리합니다. NuGet.org는 패키지의 유일한 호스트가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="1dbac-106">In its role as a public host, NuGet.org itself maintains the central repository of over 100,000 unique packages at [nuget.org](https://www.nuget.org). NuGet.org is not the only possible host for packages.</span></span> <span data-ttu-id="1dbac-107">또한 NuGet 기술을 사용하면 클라우드(예:Azure DevOps), 프라이빗 네트워크 또는 로컬 파일 시스템에서도 패키지를 전용으로 호스팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dbac-107">The NuGet technology also enables you to host packages privately in the cloud (such as on Azure DevOps), on a private network, or even on just your local file system.</span></span> <span data-ttu-id="1dbac-108">다른 호스트 또는 호스팅 옵션에 관심이 있다면 [사용자 고유의 NuGet 피드 호스팅](../hosting-packages/overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1dbac-108">If you are interested in a different host or hosting option, see [Hosting your own NuGet feeds](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="1dbac-109">NuGet.org는 NuGet 패키지의 호스트와 마찬가지로 패키지 *작성자*와 패키지 *소비자* 사이의 연결 지점 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dbac-109">NuGet.org, like any host for NuGet packages, serves as the point of connection between package *creators* and package *consumers*.</span></span> <span data-ttu-id="1dbac-110">작성자는 유용한 NuGet 패키지를 빌드하고 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="1dbac-110">Creators build useful NuGet packages and publish them.</span></span> <span data-ttu-id="1dbac-111">그런 다음 소비자는 액세스할 수 있는 호스트에서 유용하고 호환 가능한 패키지를 검색하고 해당 패키지를 다운로드하여 프로젝트에 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1dbac-111">Consumers then search for useful and compatible packages on accessible hosts, downloading and including those packages in their projects.</span></span> <span data-ttu-id="1dbac-112">프로젝트에 설치되면 패키지의 API는 프로젝트 코드의 나머지 부분에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dbac-112">Once installed in a project, the packages' APIs are available to the rest of the project code.</span></span>

![패키지 작성자, 패키지 호스트 및 패키지 소비자 간의 관계](media/nuget-roles.png)

## <a name="accounts"></a><span data-ttu-id="1dbac-114">계정</span><span class="sxs-lookup"><span data-stu-id="1dbac-114">Accounts</span></span>

<span data-ttu-id="1dbac-115">NuGet.org에 패키지를 게시하려면 먼저 [개별(사용자) 계정](individual-accounts.md)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1dbac-115">To publish packages on NuGet.org, you first create an [individual (user) account](individual-accounts.md).</span></span> <span data-ttu-id="1dbac-116">이는 NuGet.org에서 사용자 ID가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1dbac-116">This becomes your identity on NuGet.org.</span></span>

<span data-ttu-id="1dbac-117">NuGet.org에서는 [조직 계정](organizations-on-nuget-org.md)을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dbac-117">NuGet.org also allows you to create an [organization account](organizations-on-nuget-org.md).</span></span> <span data-ttu-id="1dbac-118">조직 계정은 구성원으로 하나 이상의 개별 계정을 가지고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dbac-118">An organization account has one or more individual accounts as its members.</span></span> <span data-ttu-id="1dbac-119">멤버는 소유권에 대한 단일 ID를 유지 관리하면서 패키지 세트를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dbac-119">Members can manage a set of packages while maintaining a single identity for ownership.</span></span> <span data-ttu-id="1dbac-120">개별 계정을 통해 여러 조직의 멤버가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dbac-120">Through your individual account, you can be a member of any number of organizations.</span></span>

<span data-ttu-id="1dbac-121">패키지는 개별 계정에 속할 수 있는 것처럼 조직 계정에 속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dbac-121">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="1dbac-122">패키지 소비자는 개별 계정 또는 조직 계정 간의 차이를 보지 못합니다. 둘 다 패키지 `owners`로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="1dbac-122">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

## <a name="api-keys"></a><span data-ttu-id="1dbac-123">API 키</span><span class="sxs-lookup"><span data-stu-id="1dbac-123">API keys</span></span>

<span data-ttu-id="1dbac-124">게시할 NuGet 패키지( *.nupkg* 파일)가 있으면 NuGet.org에서 얻은 [API 키](scoped-api-keys.md)와 함께 nuget.exe CLI 또는 dotnet.exe CLI를 사용하여 NuGet.org에 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="1dbac-124">Once you have a NuGet package (*.nupkg* file) to publish, you publish it to NuGet.org using either the nuget.exe CLI or the dotnet.exe CLI, along with an [API key](scoped-api-keys.md) acquired from NuGet.org.</span></span>

<span data-ttu-id="1dbac-125">[패키지를 게시](../create-packages/creating-a-package.md)하면 CLI 명령에 API 키 값이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1dbac-125">When you [publish a package](../create-packages/creating-a-package.md), you include the API key value in the CLI command.</span></span>

## <a name="id-prefixes"></a><span data-ttu-id="1dbac-126">ID 접두사</span><span class="sxs-lookup"><span data-stu-id="1dbac-126">ID prefixes</span></span>

<span data-ttu-id="1dbac-127">패키지를 게시할 때 [ID 접두사를 예약](id-prefix-reservation.md)하여 ID를 예약 및 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dbac-127">When you publish packages, you can reserve and protect your identity by [reserving ID prefixes](id-prefix-reservation.md).</span></span> <span data-ttu-id="1dbac-128">패키지를 설치할 때 패키지 소비자는 사용하는 패키지가 식별되는 속성에서 기만적이지 않음을 나타내는 추가 정보를 제공받습니다.</span><span class="sxs-lookup"><span data-stu-id="1dbac-128">When installing a package, package consumers are provided with additional information indicating that the package they are consuming is not deceptive in its identifying properties.</span></span>

## <a name="api-endpoint-for-nugetorg"></a><span data-ttu-id="1dbac-129">NuGet.org에 대한 API 엔드포인트</span><span class="sxs-lookup"><span data-stu-id="1dbac-129">API endpoint for NuGet.org</span></span>

<span data-ttu-id="1dbac-130">NuGet 클라이언트에서 NuGet.org를 패키지 리포지토리로 사용하려면 다음과 같은 V3 API 엔드포인트를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dbac-130">To use NuGet.org as a package repository with NuGet clients, you should use the following V3 API endpoint:</span></span> 

`https://api.nuget.org/v3/index.json`

<span data-ttu-id="1dbac-131">이전 버전의 클라이언트는 V2 프로토콜을 사용하여 NuGet.org에 연결할 수 있습니다. 그러나 NuGet 클라이언트 3.0 이상에는 V2 프로토콜을 사용하는 느리고 신뢰할 수 없는 서비스가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1dbac-131">Older clients can still use the V2 protocol to reach NuGet.org. However, please note, NuGet clients 3.0 or later will have slower and less reliable service using the V2 protocol:</span></span>

<span data-ttu-id="1dbac-132">`https://www.nuget.org/api/v2`(**V2 프로토콜은 더 이상 사용되지 않습니다!** )</span><span class="sxs-lookup"><span data-stu-id="1dbac-132">`https://www.nuget.org/api/v2` (**The V2 prototcol is deprecated!**)</span></span>
