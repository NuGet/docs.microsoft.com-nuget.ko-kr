---
title: 2.8.6 NuGet 릴리스 정보
description: NuGet 2.8.6 포함에 대 한 릴리스 정보는 문제, 버그 수정, 추가 된 기능 및 Dcr 알려져 있습니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d57c658999ed3c79b962de84fd973276833ef3fd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546493"
---
# <a name="nuget-286-release-notes"></a><span data-ttu-id="4e69d-103">2.8.6 NuGet 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="4e69d-103">NuGet 2.8.6 Release Notes</span></span>

<span data-ttu-id="4e69d-104">[2.8.5 NuGet 릴리스 정보](../release-notes/nuget-2.8.5.md) | [2.8.7 NuGet 릴리스 정보](../release-notes/nuget-2.8.7.md)</span><span class="sxs-lookup"><span data-stu-id="4e69d-104">[NuGet 2.8.5 Release Notes](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md)</span></span>

<span data-ttu-id="4e69d-105">NuGet 2.8.6 릴리스된 2015 년 7 월 20, 한 부분 업데이트는 2.8.5 VSIX 일부를 사용 하 여 대상 수정 및 향상 된 Windows 10 UWP 개발 모델에 대 한 지원으로 배달할 수 있는 패키지를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e69d-105">NuGet 2.8.6 was released July 20, 2015 as a minor update to our 2.8.5 VSIX with some targeted fixes and improvements to support packages that may be delivered with support for the Windows 10 UWP development model.</span></span>

<span data-ttu-id="4e69d-106">이 버전의 NuGet 패키지 관리자 확장명을 Visual Studio 2013에 대 한 지원만 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4e69d-106">This version of the NuGet package manager extension provides support for Visual Studio 2013 only.</span></span>

<span data-ttu-id="4e69d-107">이 릴리스에서 NuGet 패키지 관리자 대화 상자에 대 한 추가 지원을 했습니다.</span><span class="sxs-lookup"><span data-stu-id="4e69d-107">In this release, the NuGet Package Manager dialog had support added for:</span></span>

* <span data-ttu-id="4e69d-108">Windows 10 응용 프로그램 개발을 지 원하는 UAP 대상 프레임 워크 모니커를 도입 했습니다.</span><span class="sxs-lookup"><span data-stu-id="4e69d-108">Introduced the UAP Target Framework Moniker to support Windows 10 Application Development.</span></span>
* <span data-ttu-id="4e69d-109">NuGet 프로토콜 버전 3 끝점</span><span class="sxs-lookup"><span data-stu-id="4e69d-109">NuGet protocol version 3 endpoints</span></span>
* <span data-ttu-id="4e69d-110">에 대 한 지원 [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) 리포지토리 원본 protocolVersion 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="4e69d-110">Support for [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion attribute on repository sources.</span></span> <span data-ttu-id="4e69d-111">기본값은 "2"</span><span class="sxs-lookup"><span data-stu-id="4e69d-111">Default value is "2"</span></span>
* <span data-ttu-id="4e69d-112">대체 원격 리포지토리에 로컬 캐시에 필요한 패키지 버전을 사용할 수 없는 경우</span><span class="sxs-lookup"><span data-stu-id="4e69d-112">Falling back to remote repository if a required package version is not available in the local cache</span></span>