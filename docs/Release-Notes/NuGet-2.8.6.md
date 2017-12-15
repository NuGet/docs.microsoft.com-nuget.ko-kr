---
title: "NuGet 2.8.6 릴리스 정보 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 920c551c-18a7-40f4-a32b-ce84de6ea766
description: "NuGet 2.8.6 포함에 대 한 릴리스 정보는 문제, 버그 수정, 추가 된 기능 및 Dcr 알려져 있습니다."
keywords: "NuGet 2.8.6 릴리스 정보, 버그 수정, 알려진 문제, 추가 기능을 Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f33c1edd3ef703a8cd97b7bdd97c37e12426aafa
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-286-release-notes"></a><span data-ttu-id="03261-104">NuGet 2.8.6 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="03261-104">NuGet 2.8.6 Release Notes</span></span>

<span data-ttu-id="03261-105">[NuGet 2.8.5 릴리스 정보](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 릴리스 정보](../release-notes/nuget-2.8.7.md)</span><span class="sxs-lookup"><span data-stu-id="03261-105">[NuGet 2.8.5 Release Notes](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md)</span></span>

<span data-ttu-id="03261-106">NuGet 2.8.6 릴리스된 우리의 2.8.5에 사소한 업데이트로 2015 년 7 월 20 일 일부와 VSIX 대상 수정 및 Windows 10 UWP 개발 모델에 대 한 지원과 함께 제공 될 수 있습니다 하는 패키지를 지원 하도록 개선 합니다.</span><span class="sxs-lookup"><span data-stu-id="03261-106">NuGet 2.8.6 was released July 20, 2015 as a minor update to our 2.8.5 VSIX with some targeted fixes and improvements to support packages that may be delivered with support for the Windows 10 UWP development model.</span></span>

<span data-ttu-id="03261-107">NuGet 패키지 관리자 확장이 버전에만 Visual Studio 2013에 대 한 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="03261-107">This version of the NuGet package manager extension provides support for Visual Studio 2013 only.</span></span>

<span data-ttu-id="03261-108">이 릴리스에서 NuGet 패키지 관리자 대화 상자에 대 한 추가 지원을 했습니다.</span><span class="sxs-lookup"><span data-stu-id="03261-108">In this release, the NuGet Package Manager dialog had support added for:</span></span>

* <span data-ttu-id="03261-109">Windows 10 응용 프로그램 개발을 지 원하는 UAP 대상 프레임 워크 모니커 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="03261-109">Introduced the UAP Target Framework Moniker to support Windows 10 Application Development.</span></span>
* <span data-ttu-id="03261-110">NuGet의 프로토콜 버전 3 끝점</span><span class="sxs-lookup"><span data-stu-id="03261-110">NuGet protocol version 3 endpoints</span></span>
* <span data-ttu-id="03261-111">에 대 한 지원 [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) 리포지토리 소스에서 protocolVersion 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="03261-111">Support for [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion attribute on repository sources.</span></span> <span data-ttu-id="03261-112">기본값은 "2"</span><span class="sxs-lookup"><span data-stu-id="03261-112">Default value is "2"</span></span>
* <span data-ttu-id="03261-113">로컬 캐시에서 필요한 패키지 버전을 사용할 수 없으면 원격 리포지토리에 대체</span><span class="sxs-lookup"><span data-stu-id="03261-113">Falling back to remote repository if a required package version is not available in the local cache</span></span>