---
title: "\"NuGet 패키지 이름 분쟁 확인 | Microsoft Docs\""
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 6d664378-3f7b-426e-aef3-2254d745fe60
description: "브랜딩과 관련된 NuGet 패키지 게시자, 상표 및 기타 충돌 상황 간에 분쟁을 해결하기 위한 프로세스입니다."
keywords: "NuGet 패키지 분쟁, NuGet 분쟁 해결, 분쟁 해결 프로세스"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 32f5f766a49a2e4254a81978757d973fc5353db1
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="resolving-disputes-over-nuget-package-names"></a><span data-ttu-id="ba436-104">NuGet 패키지 이름 분쟁 해결</span><span class="sxs-lookup"><span data-stu-id="ba436-104">Resolving disputes over NuGet package names</span></span>

<span data-ttu-id="ba436-105">이 문서는 커뮤니티 구성원에 대해 다른 NuGet 게시자와의 분쟁을 해결하도록 해결 프로세스를 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="ba436-105">This document is a recommended resolution process for community members to resolve disputes with other NuGet publishers.</span></span>  

<span data-ttu-id="ba436-106">예를 들어 Northwind Traders가 해당 웹 사이트에서 다운로드 가능한 MSI로 클라이언트 드라이버를 제공하도록 CRM 시스템을 만든다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="ba436-106">For example, suppose that Northwind Traders makes a CRM system for which they provide client drivers as a downloadable MSI from their website.</span></span> <span data-ttu-id="ba436-107">독자적 개발자인 Nancy는 보다 쉽게 Northwind의 클라이언트 라이브러리를 사용할 수 있도록 하고 `NorthwindTraders.Client`라는 NuGet 패키지로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="ba436-107">Nancy, an independent developer, wants to make it easier to use Northwind's client library, and turns it into a NuGet package called `NorthwindTraders.Client`.</span></span> <span data-ttu-id="ba436-108">나중에 Northwind에서는 해당 클라이언트 라이브러리에서 고유한 공식 NuGet 패키지를 생성하고 따라서 패키지 이름에 대한 Nancy의 소유권에 대한 분쟁이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="ba436-108">Later, Northwind wants to produce an official NuGet package of their own for their client library, and would thus like to dispute Nancy's ownership of the package name.</span></span>

<span data-ttu-id="ba436-109">이 시나리오에서 Nancy는 나쁜 의도를 가진 것으로 보이지 않지만 대신 고유한 시간 및 코드를 제공하여 Northwind의 도구 및 고객을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ba436-109">In this scenario, Nancy does not appear to be acting with bad intentions, but is rather supporting Northwind's tools and customers by contributing her own time and code.</span></span> <span data-ttu-id="ba436-110">동시에 Northwind는 Northwind 이름의 정당한 소유자입니다.</span><span class="sxs-lookup"><span data-stu-id="ba436-110">At the same time, Northwind is the legitimate owner of the Northwind name.</span></span>

<span data-ttu-id="ba436-111">Northwind 및 Nancy는 둘 다 개발자 커뮤니티를 제공하는 데 관심이 있기 때문에 아래 프로세스를 수행하여 적합한 해결 방법을 함께 모색합니다.</span><span class="sxs-lookup"><span data-stu-id="ba436-111">By following the process below, Northwind and Nancy can work together to a suitable resolution, because both are interested in serving the developer community.</span></span> <span data-ttu-id="ba436-112">일반적으로 NuGet 팀이 관련될 필요는 없습니다. 공동 작업은 일반적으로 뛰어난 결과를 발생시킵니다.</span><span class="sxs-lookup"><span data-stu-id="ba436-112">It's typically not necessary for the NuGet team to become involved; collaboration usually works out best.</span></span> <span data-ttu-id="ba436-113">사실 NuGet 팀이 날짜에 주의하도록 만드는 모든 분쟁은 팀이 판단을 미루지 않고 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ba436-113">In fact, every dispute brought to the NuGet team's attention to date has been worked out without the team needing to pass judgment.</span></span>


## <a name="process"></a><span data-ttu-id="ba436-114">프로세스</span><span class="sxs-lookup"><span data-stu-id="ba436-114">Process</span></span>

1. <span data-ttu-id="ba436-115">패키지 세부 정보 페이지에서 **연락처 소유자** 링크를 사용하여 분쟁이 발생한 패키지의 소유자에게 연락합니다.</span><span class="sxs-lookup"><span data-stu-id="ba436-115">Contact the owners of the package you have the dispute with using the **Contact Owners** link on the package details page.</span></span> <span data-ttu-id="ba436-116">직접 친절하게 문제를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ba436-116">Explain your issue in a kind and direct manner.</span></span>
2. <span data-ttu-id="ba436-117">해당 NuGet 및 .NET Foundation이 분쟁을 인식하도록 [support@nuget.org](mailto:support@nuget.org)에 메시지의 복사본을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="ba436-117">Send a copy of your message to [support@nuget.org](mailto:support@nuget.org) so that NuGet and the .NET Foundation are aware of your dispute.</span></span>
3. <span data-ttu-id="ba436-118">[support@nuget.org](mailto:support@nuget.org)에 다시 알린 후에 해결을 위해 최대 30일 동안 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="ba436-118">Wait a maximum of 30 days for a resolution, after which notify [support@nuget.org](mailto:support@nuget.org) again.</span></span> <span data-ttu-id="ba436-119">nuget.org 지원팀이 참여하고 두 당사자와 분쟁을 해결하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba436-119">The nuget.org support team will get involved and try to work through the dispute with both parties.</span></span>
