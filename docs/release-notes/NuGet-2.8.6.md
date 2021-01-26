---
title: NuGet 2.8.6 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 2.8.6를 포함 하는 NuGet에 대 한 릴리스 정보입니다.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ea291bdf7a5b6cc3ac3bde526030e517db4632d7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776700"
---
# <a name="nuget-286-release-notes"></a><span data-ttu-id="8ed68-103">NuGet 2.8.6 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="8ed68-103">NuGet 2.8.6 Release Notes</span></span>

<span data-ttu-id="8ed68-104">[NuGet 2.8.5 릴리스 정보](../release-notes/nuget-2.8.5.md)  |  [NuGet 2.8.7 릴리스 정보](../release-notes/nuget-2.8.7.md)</span><span class="sxs-lookup"><span data-stu-id="8ed68-104">[NuGet 2.8.5 Release Notes](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md)</span></span>

<span data-ttu-id="8ed68-105">NuGet 2.8.6는 2.8.5 VSIX에 대 한 사소한 업데이트로 2015 년 7 월 20 일에 출시 되었으며, Windows 10 UWP 개발 모델에 대 한 지원과 함께 제공 될 수 있는 패키지를 지원 하기 위해 몇 가지 대상 수정 및 향상 된 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ed68-105">NuGet 2.8.6 was released July 20, 2015 as a minor update to our 2.8.5 VSIX with some targeted fixes and improvements to support packages that may be delivered with support for the Windows 10 UWP development model.</span></span>

<span data-ttu-id="8ed68-106">이 버전의 NuGet 패키지 관리자 확장은 Visual Studio 2013만 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ed68-106">This version of the NuGet package manager extension provides support for Visual Studio 2013 only.</span></span>

<span data-ttu-id="8ed68-107">이 릴리스에서 NuGet 패키지 관리자 대화 상자에는 다음에 대 한 지원이 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8ed68-107">In this release, the NuGet Package Manager dialog had support added for:</span></span>

* <span data-ttu-id="8ed68-108">UAP 대상 프레임 워크 모니커를 도입 하 여 Windows 10 응용 프로그램 개발을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ed68-108">Introduced the UAP Target Framework Moniker to support Windows 10 Application Development.</span></span>
* <span data-ttu-id="8ed68-109">NuGet 프로토콜 버전 3 끝점</span><span class="sxs-lookup"><span data-stu-id="8ed68-109">NuGet protocol version 3 endpoints</span></span>
* <span data-ttu-id="8ed68-110">리포지토리 원본에서 [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion 특성을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ed68-110">Support for [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion attribute on repository sources.</span></span> <span data-ttu-id="8ed68-111">기본값은 "2"입니다.</span><span class="sxs-lookup"><span data-stu-id="8ed68-111">Default value is "2"</span></span>
* <span data-ttu-id="8ed68-112">로컬 캐시에서 필요한 패키지 버전을 사용할 수 없는 경우 원격 리포지토리로 대체</span><span class="sxs-lookup"><span data-stu-id="8ed68-112">Falling back to remote repository if a required package version is not available in the local cache</span></span>