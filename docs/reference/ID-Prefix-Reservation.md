---
title: ID 접두사 예약 참조
description: 패키지 ID 접두사 예약 기능 설명 및 작성자 가이드입니다.
author: diverdan92
ms.author: diverdan92
ms.date: 10/09/2017
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 32f83bede42f7643a9a4fed593643eefea0453c1
ms.sourcegitcommit: 09107c5092050f44a0c6abdfb21db73878f78bd0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/03/2018
ms.locfileid: "50981004"
---
# <a name="package-id-prefix-reservation"></a><span data-ttu-id="b49cf-103">패키지 ID 접두사 예약</span><span class="sxs-lookup"><span data-stu-id="b49cf-103">Package ID prefix reservation</span></span>

<span data-ttu-id="b49cf-104">패키지 소유자를 예약 하 고 ID 접두사를 예약 하 여 자신의 id를 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b49cf-104">Package owners can reserve and protect their identity by reserving ID prefixes.</span></span> <span data-ttu-id="b49cf-105">패키지 소비자는 추가 정보를 사용 하 여 패키지를 사용 하는 경우 현재 사용 중인 패키지 없는 해당 식별 속성에서 거짓 제공입니다.</span><span class="sxs-lookup"><span data-stu-id="b49cf-105">Package consumers are provided with additional information when consuming packages that the package they are consuming are not deceptive in their identifying properties.</span></span> 

<span data-ttu-id="b49cf-106">[nuget.org](https://www.nuget.org/) Visual Studio 2017 버전 15.4 이상 패키지 예약된 ID와 일치 하기만 예약 된 패키지 ID 접두사를 사용 하 여 소유자가 전송 되는 패키지는 명명 패턴 접두사에 대 한 시각적 표시기를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b49cf-106">[nuget.org](https://www.nuget.org/) and Visual Studio 2017 version 15.4 or later show a visual indicator for packages that are submitted by owners with a reserved package ID prefix, as long as the package matches the reserved ID prefix naming pattern.</span></span> <span data-ttu-id="b49cf-107">아래 참조 ID 접두사 예약 시 어떤 및 소유자 ID 접두사를 적용 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b49cf-107">The below reference explains what the ID prefix reservation entails, and how an owner can apply for an ID prefix.</span></span>

## <a name="id-prefix-reservation-details"></a><span data-ttu-id="b49cf-108">ID 접두사 예약 세부 정보</span><span class="sxs-lookup"><span data-stu-id="b49cf-108">ID prefix reservation details</span></span>

<span data-ttu-id="b49cf-109">여러 작업이 수행 된 패키지 ID 접두사 예약 된 경우는 [nuget.org](https://www.nuget.org/) 갤러리도 Visual Studio와 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="b49cf-109">When a package ID prefix is reserved, several things happen on the [nuget.org](https://www.nuget.org/) gallery, as well as in Visual Studio.</span></span> <span data-ttu-id="b49cf-110">또한 접두사 하위 집합을 여러 소유자에 게 위임으로 'public' 접두사를 설정 하는 등 ID 접두사 예약을 지 원하는 시나리오 고급 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b49cf-110">In addition, there are advanced scenarios that are supported by ID prefix reservations, such as setting a prefix as 'public', delegating prefix subsets to multiple owners.</span></span>

### <a name="id-prefix-reservation-on-nugetorg"></a><span data-ttu-id="b49cf-111">Nuget.org에서 ID 접두사 예약</span><span class="sxs-lookup"><span data-stu-id="b49cf-111">ID prefix reservation on nuget.org</span></span>

<span data-ttu-id="b49cf-112">접두사는 예약 하는 경우 [nuget.org](https://www.nuget.org/), 다음 현상이 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="b49cf-112">When a prefix is reserved on [nuget.org](https://www.nuget.org/), the following will happen:</span></span>

1. <span data-ttu-id="b49cf-113">접두사 예약에 소유자 또는 소유자의 집합을 사용 하 여 연결 된 [nuget.org](https://www.nuget.org/)합니다.</span><span class="sxs-lookup"><span data-stu-id="b49cf-113">A prefix reservation is associated with an owner or set of owners on [nuget.org](https://www.nuget.org/).</span></span>

1. <span data-ttu-id="b49cf-114">패키지를 전송할 때마다 [nuget.org](https://www.nuget.org/) 예약된 ID 접두사와 일치 하는 ID를 사용 하 여 패키지 ID 접두사 예약 소유자에서 시작 하지 않으면 거부 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b49cf-114">Whenever a package is submitted to [nuget.org](https://www.nuget.org/) with an ID that matches the reserved ID prefix, the package is rejected unless it originates from the owner(s) that reserved the ID prefix.</span></span>

1. <span data-ttu-id="b49cf-115">Visual Studio 2017 버전 15.4 이상에 예약 된 ID 접두사와 일치 하 고 소유자 ID 접두사 예약에서 발생 하는 모든 패키지에서 시각적 표시기를 갖습니다 [nuget.org](https://www.nuget.org/) 에서 패키지를 나타내는 예약된 ID 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="b49cf-115">Any package that matches the reserved ID prefix and originates from the owner(s) that reserved the ID prefix will have a visual indicator in Visual Studio 2017 version 15.4 or later, and on [nuget.org](https://www.nuget.org/) indicating that the package is under a reserved ID prefix.</span></span> <span data-ttu-id="b49cf-116">새 패키지 제출 뿐만 아니라 기존 패키지의 소유자에 대 한 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="b49cf-116">This is true for both new package submissions as well as existing packages under the owner(s).</span></span> <span data-ttu-id="b49cf-117">**참고:** 표시기 Visual Studio에서 패키지 원본을 단일 피드를 선택 하는 경우에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b49cf-117">**Note:** The indicator in Visual Studio appears only if a single feed is selected as the package source.</span></span>

1. <span data-ttu-id="b49cf-118">예약된 ID 접두사와 일치 하는 모든 기존 패키지 하지만 됩니다 *하지* 예약된 된 소유자가 소유 하 고 접두사는 그대로 유지 됩니다 (비공개, 되지 것입니다 하지만 됩니다 하지 시각적 표시기).</span><span class="sxs-lookup"><span data-stu-id="b49cf-118">All previously existing packages that match the reserved ID prefix, but are *not* owned by the owner of the reserved prefix will remain unchanged (they will not be unlisted, but they will also not have the visual indicator).</span></span> <span data-ttu-id="b49cf-119">또한 이러한 패키지의 소유자 패키지에 새 버전을 제출 하는 일을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b49cf-119">In addition, owners of these packages will still be able to submit new versions to the package.</span></span>

<span data-ttu-id="b49cf-120">이러한 변경 내용은 다음 조건에 기반한 및 몇 가지 추가 제한 사항이 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b49cf-120">These changes are based on the following conditions and impose several additional restrictions:</span></span>

- <span data-ttu-id="b49cf-121">패키지의 소유자 하나만 표시 (여러 소유자를 사용 하 여 패키지)에 대 한 시각적 표시기에 대 한 예약 된 접두사를가지고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b49cf-121">Only one owner of a package needs to have the reserved prefix for the visual indicator to appear (for packages with multiple-owners).</span></span>

- <span data-ttu-id="b49cf-122">하나 이상의 소유자에 예약 된 접두사 없는 있고 하나 이상의 소유자 예약 된 접두사에 있는 패키지의 둘 이상의 소유자가 예약 된 접두사를 사용 하 여 소유자만이 예약된 된 접두사를 사용 하 여 다른 소유자를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b49cf-122">If there is more than one owner of a package where one or more owners has the reserved prefix and one or more owners does not have the reserved prefix, then only the owner(s) with the reserved prefix can remove other owner(s) with a reserved prefix.</span></span> <span data-ttu-id="b49cf-123">예약 된 접두사를 갖고 있지 않은 소유자는 예약 된 접두사를 사용 하 여 소유자를 제거할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b49cf-123">The owners who do not have the prefix reserved cannot remove owners with the prefix reserved.</span></span> <span data-ttu-id="b49cf-124">여전히도 예약 된 접두사를 갖지 않는 다른 소유자를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b49cf-124">They can still remove other owners that also do not have the prefix reserved.</span></span>

- <span data-ttu-id="b49cf-125">패키지를 시각적 표시기가 되 면 *항상* 시각적 표시기는 (예약 된 접두사를 사용 하 여 하나 이상의 해당 소유자를 보장 하는 항상 남아 소유자)</span><span class="sxs-lookup"><span data-stu-id="b49cf-125">Once a package has the visual indicator, it should *always* have the visual indicator (guaranteeing that at least one owner with the reserved prefix will always remain an owner)</span></span>

### <a name="advanced-prefix-reservation-scenarios"></a><span data-ttu-id="b49cf-126">고급 접두사 예약 시나리오</span><span class="sxs-lookup"><span data-stu-id="b49cf-126">Advanced prefix reservation scenarios</span></span>

<span data-ttu-id="b49cf-127">몇 가지 고급 접두사 예약 시나리오 subprefix 위임 및 public으로 표시 접두사를 포함 하 여 아래에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b49cf-127">There are several more advanced prefix reservation scenarios described below, including subprefix delegation, and marking prefixes as public.</span></span> <span data-ttu-id="b49cf-128">다음은 수행할 수 있는 고급 접두사 예약입니다.</span><span class="sxs-lookup"><span data-stu-id="b49cf-128">Below are the more advanced prefix reservations that can be made.</span></span> 

- <span data-ttu-id="b49cf-129">접두사 예약 하는 동안 소유자가 접두사 하위의 위임 (또는 접두사) 다른 소유자에 게 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b49cf-129">During prefix reservation, the owner can request delegation of prefix subsets (or the prefix) to other owners.</span></span> <span data-ttu-id="b49cf-130">예를 들어 경우 '[Microsoft](https://www.nuget.org/profiles/microsoft)' 소유 ' microsoft\*', 있지만 '[aspnet](https://www.nuget.org/profiles/aspnet)' 예약 하려는 ' Microsoft.AspNet.\*','[Microsoft](https://www.nuget.org/profiles/microsoft)' 수 위임 하도록 선택할 ' Microsoft.AspNet 합니다. \*'에 [aspnet](https://www.nuget.org/profiles/aspnet) 계정.</span><span class="sxs-lookup"><span data-stu-id="b49cf-130">For example, if '[Microsoft](https://www.nuget.org/profiles/microsoft)' owns 'Microsoft.\*', but '[aspnet](https://www.nuget.org/profiles/aspnet)' wants to reserve 'Microsoft.AspNet.\*', '[Microsoft](https://www.nuget.org/profiles/microsoft)' can choose to delegate 'Microsoft.AspNet.\*' to the [aspnet](https://www.nuget.org/profiles/aspnet) account.</span></span>

- <span data-ttu-id="b49cf-131">접두사 예약 하는 동안 소유자 공용 접두사를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b49cf-131">During prefix reservation, the owner can choose to make a prefix public.</span></span> <span data-ttu-id="b49cf-132">이 계속 해 서 이러한 패키지는 예약된 된 접두사에서 시작 되는 것을 보여 주는 시각적 표시기 **하지** 모든 소유자에 대 한 접두사에 패키지의 나중 서브 미션을 차단 합니다.</span><span class="sxs-lookup"><span data-stu-id="b49cf-132">This will still give them the visual indicator showing that the package originates from a reserved prefix, but it will **not** block future package submissions on the prefix for any owner.</span></span> <span data-ttu-id="b49cf-133">많은 참가자를 사용 하 여 오픈 소스 프로젝트에 대 한 유용-top 또는 핵심 참가자는 예약 된 접두사를 가질 수 있습니다 하지만 모든 참가자를 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b49cf-133">This is useful for open source projects with many contributors - the top or core contributors can have the prefix reserved, but it can still be open to all contributors.</span></span> 

### <a name="prefix-reservation-visual-indicator"></a><span data-ttu-id="b49cf-134">접두사 예약에 대 한 시각적 표시기</span><span class="sxs-lookup"><span data-stu-id="b49cf-134">Prefix reservation visual indicator</span></span>

<span data-ttu-id="b49cf-135">예약된 된 접두사에서 패키지 상태가 되 면 표시를 아래에 대 한 시각적 표시기를 [nuget.org](https://www.nuget.org/) 갤러리 및 Visual Studio 2017 버전 15.4 이상에서:</span><span class="sxs-lookup"><span data-stu-id="b49cf-135">When a package comes from a reserved prefix, you see the below visual indicators on the [nuget.org](https://www.nuget.org/) gallery and in Visual Studio 2017 version 15.4 or later:</span></span>

<span data-ttu-id="b49cf-136">**nuget.org Gallery**
![nuget.org Gallery](media/nuget-gallery-reserved-prefix.png)</span><span class="sxs-lookup"><span data-stu-id="b49cf-136">**nuget.org Gallery**
![nuget.org Gallery](media/nuget-gallery-reserved-prefix.png)</span></span>

<span data-ttu-id="b49cf-137">**Visual Studio**
![Visual Studio](media/visual-studio-reserved-prefix.png)</span><span class="sxs-lookup"><span data-stu-id="b49cf-137">**Visual Studio**
![Visual Studio](media/visual-studio-reserved-prefix.png)</span></span>

## <a name="id-prefix-reservation-application-process"></a><span data-ttu-id="b49cf-138">ID 접두사 예약 응용 프로그램 프로세스</span><span class="sxs-lookup"><span data-stu-id="b49cf-138">ID prefix reservation application process</span></span>

1. <span data-ttu-id="b49cf-139">승인 검토 [ID 접두사 예약에 대 한 조건을](#id-prefix-reservation-criteria)합니다.</span><span class="sxs-lookup"><span data-stu-id="b49cf-139">Review the acceptance [criteria for prefix ID reservation](#id-prefix-reservation-criteria).</span></span>

2. <span data-ttu-id="b49cf-140">외에도 예약 하려는 접두사를 확인할 [고급 접두사 예약 시나리오](#advanced-prefix-reservation-scenarios) 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b49cf-140">Determine the prefixes you want to reserve, in addition to any [advanced prefix reservation scenarios](#advanced-prefix-reservation-scenarios) you may require.</span></span>

3. <span data-ttu-id="b49cf-141">에 게 메일 보내기 [ account@nuget.org ](mailto:account@nuget.org) 소유자를 사용 하 여 이름에 표시할 [nuget.org](https://www.nuget.org/)를 요청 하는 모든 예약 된 접두사와 합니다.</span><span class="sxs-lookup"><span data-stu-id="b49cf-141">Send a mail to [account@nuget.org](mailto:account@nuget.org) with the owner display name on [nuget.org](https://www.nuget.org/), as well as any reserved prefixes you are requesting.</span></span> <span data-ttu-id="b49cf-142">여러 소유자에 게 접두사 하위 집합을 위임할 경우 모든 소유자 표시 이름을 언급 하 고 접두사 하위 집합에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b49cf-142">If you are delegating prefix subsets to multiple owners, make sure you mention all owner display names and prefix subsets.</span></span>

<span data-ttu-id="b49cf-143">응용 프로그램을 제출한 후 승인 또는 거부를 발생 시킨 조건) (으로 거부의 알림이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b49cf-143">After the application is submitted, you are notified of acceptance or rejection (with the criteria that caused rejection).</span></span> <span data-ttu-id="b49cf-144">소유자 id를 확인 하려면 추가 식별 질문 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b49cf-144">We may need to ask additional identifying questions to confirm owner identity.</span></span>

### <a name="id-prefix-reservation-criteria"></a><span data-ttu-id="b49cf-145">ID 접두사 예약 조건</span><span class="sxs-lookup"><span data-stu-id="b49cf-145">ID prefix reservation criteria</span></span>

<span data-ttu-id="b49cf-146">ID 접두사 예약에 대 한 모든 응용 프로그램을 검토할 때 합니다 [nuget.org](https://www.nuget.org/) 팀에 대 한 응용 프로그램을 평가 하는 아래 기준을 합니다.</span><span class="sxs-lookup"><span data-stu-id="b49cf-146">When reviewing any application for ID prefix reservation, the [nuget.org](https://www.nuget.org/) team will evaluate the application against the below criteria.</span></span> <span data-ttu-id="b49cf-147">일부 조건을 접두사 예약 되도록 하기 위해 충족 해야 합니다. 하지만 (지정 된 설명)와 부합 하지 않게 조건의 상당한 증거 없는 경우 응용 프로그램을 거부 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b49cf-147">Not all criteria needs to be met for a prefix to be reserved, but the application may be denied if there is not substantial evidence of the criteria being met (with an explanation given):</span></span>

1. <span data-ttu-id="b49cf-148">패키지 ID 접두사 제대로 명확 하 게 나타내는 패키지 소유자 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="b49cf-148">Does the package ID prefix properly and clearly identify the package owner?</span></span>

1. <span data-ttu-id="b49cf-149">패키지 ID 접두사 아래 소유자가 이미 제출 하는 패키지의 상당수?</span><span class="sxs-lookup"><span data-stu-id="b49cf-149">Are a significant number of the packages that have already been submitted by the owner under the package ID prefix?</span></span>

1. <span data-ttu-id="b49cf-150">패키지 ID 접두사를 사용 하는 일반적인 모든 개별 소유자 또는 조직에 속하지 않아야 합니까?</span><span class="sxs-lookup"><span data-stu-id="b49cf-150">Is the package ID prefix something common that should not belong to any individual owner or organization?</span></span>

1. <span data-ttu-id="b49cf-151">것 *되지* 모호성 및 커뮤니티에 대 한 혼동을 일으킬 패키지 ID 접두사 예약?</span><span class="sxs-lookup"><span data-stu-id="b49cf-151">Would *not* reserving the package ID prefix cause ambiguity and confusion for the community?</span></span>

1. <span data-ttu-id="b49cf-152">패키지 ID 접두사 명확 하 고 일관 된 (특히 패키지 작성자)와 일치 하는 패키지를 식별 하는 속성이?</span><span class="sxs-lookup"><span data-stu-id="b49cf-152">Are the identifying properties of the packages that match the package ID prefix clear and consistent (especially the package author)?</span></span>

## <a name="third-party-feed-provider-scenarios"></a><span data-ttu-id="b49cf-153">타사 공급자 시나리오를 피드 합니다.</span><span class="sxs-lookup"><span data-stu-id="b49cf-153">Third party feed provider scenarios</span></span>

<span data-ttu-id="b49cf-154">피드 공급자 타사 접두사 예약을 제공 하는 자신의 서비스를 구현 하는 데 관심이 있으면 NuGet V3에서 search 서비스를 수정 하 여 공급자를 피드 하므로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b49cf-154">If a third party feed provider is interested in implementing their own service to provide prefix reservations, you can do so by modifying the search service in the NuGet V3 feed providers.</span></span> <span data-ttu-id="b49cf-155">추가 피드 검색 서비스에 추가 하는 것은 *확인* V3 피드 아래에 대 한 예제를 사용 하 여 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="b49cf-155">The addition in the feed search service is to add the *verified* property, with examples for the V3 feeds below.</span></span> <span data-ttu-id="b49cf-156">NuGet 클라이언트는 피드 V2의 추가 속성을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b49cf-156">The NuGet client will not support the added property in the V2 feed.</span></span>

<span data-ttu-id="b49cf-157">자세한 내용은 참조는 [API의 search 서비스에 대 한 설명서](../api/search-query-service-resource.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b49cf-157">For more information, see the [documentation about the API's search service](../api/search-query-service-resource.md).</span></span>

## <a name="package-id-prefix-reservation-dispute-policy"></a><span data-ttu-id="b49cf-158">패키지 ID 접두사 예약 분쟁 정책</span><span class="sxs-lookup"><span data-stu-id="b49cf-158">Package ID Prefix Reservation Dispute Policy</span></span>
<span data-ttu-id="b49cf-159">소유자를 생각 [NuGet.org](https://www.nuget.org) 위의 나열 된 조건에 위배 또는 상표권, 저작권 또는 상표에 하세요 전자 메일 침해 하는 패키지 ID 접두사 예약 할당 된 [ support@nuget.org ](mailto:support@nuget.org)해당 ID 접두사, 소유자 ID 접두사와 할당 된 접두사 예약 disputing 이유입니다.</span><span class="sxs-lookup"><span data-stu-id="b49cf-159">If you believe an owner on [NuGet.org](https://www.nuget.org) was assigned a package ID prefix reservation that goes against the above listed criteria, or infringes on any trademarks or copyrights, please email [support@nuget.org](mailto:support@nuget.org) with the ID prefix in question, the owner of the ID prefix, and the reason for disputing the assigned prefix reservation.</span></span>

