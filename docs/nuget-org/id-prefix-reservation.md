---
title: ID 접두사 예약
description: 패키지 ID 접두사 예약 기능 설명 및 작성자 가이드.
author: karann-msft
ms.author: karann
ms.date: 09/07/2019
ms.topic: reference
ms.reviewer: karann
ms.openlocfilehash: da464cc44d8c874e13c0cdfab871f31e643b577f
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/07/2020
ms.locfileid: "73610508"
---
# <a name="package-id-prefix-reservation"></a><span data-ttu-id="9d412-103">패키지 ID 접두사 예약</span><span class="sxs-lookup"><span data-stu-id="9d412-103">Package ID prefix reservation</span></span>

<span data-ttu-id="9d412-104">패키지 소유자는 ID 접두사를 예약하여 해당 ID를 예약하고 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d412-104">Package owners can reserve and protect their identity by reserving ID prefixes.</span></span> <span data-ttu-id="9d412-105">패키지 소비자는 사용하는 패키지가 식별되는 속성에서 기만적이지 않을 때 추가 정보를 제공받습니다.</span><span class="sxs-lookup"><span data-stu-id="9d412-105">Package consumers are provided with additional information when the packages that they are consuming are not deceptive in their identifying properties.</span></span> 

<span data-ttu-id="9d412-106">[nuget.org](https://www.nuget.org/) 및 Visual Studio 2017 버전 15.4 이상에서는 패키지가 예약된 ID 접두사 명명 패턴과 일치하는 한 예약된 패키지 ID 접두사가 있는 소유자가 제출한 패키지에 대한 시각적 표시기를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="9d412-106">[nuget.org](https://www.nuget.org/) and Visual Studio 2017 version 15.4 or later show a visual indicator for packages that are submitted by owners with a reserved package ID prefix, as long as the package matches the reserved ID prefix naming pattern.</span></span> <span data-ttu-id="9d412-107">아래 참조에서는 ID 접두사 예약 시 내용과 소유자가 ID 접두사에 대한 적용 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9d412-107">The below reference explains what the ID prefix reservation entails, and how an owner can apply for an ID prefix.</span></span>

## <a name="id-prefix-reservation-details"></a><span data-ttu-id="9d412-108">ID 접두사 예약 세부 정보</span><span class="sxs-lookup"><span data-stu-id="9d412-108">ID prefix reservation details</span></span>

<span data-ttu-id="9d412-109">패키지 ID 접두사가 예약되면 [nuget.org](https://www.nuget.org/) 갤러리와 Visual Studio에서 여러 가지 일이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="9d412-109">When a package ID prefix is reserved, several things happen on the [nuget.org](https://www.nuget.org/) gallery, as well as in Visual Studio.</span></span> <span data-ttu-id="9d412-110">또한 접두사를 'public'으로 설정하고 접두사를 여러 소유자에게 위임하는 등 ID 접두사 예약에 의해 지원되는 고급 시나리오가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d412-110">In addition, there are advanced scenarios that are supported by ID prefix reservations, such as setting a prefix as 'public', delegating prefix subsets to multiple owners.</span></span>

### <a name="id-prefix-reservation-on-nugetorg"></a><span data-ttu-id="9d412-111">nuget.org에 ID 접두사 예약</span><span class="sxs-lookup"><span data-stu-id="9d412-111">ID prefix reservation on nuget.org</span></span>

<span data-ttu-id="9d412-112">접두사가 [nuget.org](https://www.nuget.org/)에 예약되어 있으면 다음과 같은 현상이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="9d412-112">When a prefix is reserved on [nuget.org](https://www.nuget.org/), the following will happen:</span></span>

1. <span data-ttu-id="9d412-113">접두사 예약은 [nuget.org](https://www.nuget.org/)의 소유자 또는 소유자 세트와 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d412-113">A prefix reservation is associated with an owner or set of owners on [nuget.org](https://www.nuget.org/).</span></span>

1. <span data-ttu-id="9d412-114">예약된 ID 접두사와 일치하는 ID가 있는 패키지를 [nuget.org](https://www.nuget.org/)에 제출할 때마다 해당 패키지가 ID 접두사를 예약한 소유자로부터 생성되지 않은 한 거부됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d412-114">Whenever a package is submitted to [nuget.org](https://www.nuget.org/) with an ID that matches the reserved ID prefix, the package is rejected unless it originates from the owner(s) that reserved the ID prefix.</span></span>

1. <span data-ttu-id="9d412-115">예약된 ID 접두사와 일치하고 ID 접두사를 예약한 소유자로부터 생성된 모든 패키지는 Visual Studio 2017 버전 15.4 이상 및 [nuget.org](https://www.nuget.org/)에 패키지가 예약된 ID 접두사 아래에 있음을 나타내는 시각적 표시시가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d412-115">Any package that matches the reserved ID prefix and originates from the owner(s) that reserved the ID prefix will have a visual indicator in Visual Studio 2017 version 15.4 or later, and on [nuget.org](https://www.nuget.org/) indicating that the package is under a reserved ID prefix.</span></span> <span data-ttu-id="9d412-116">이는 소유자의 기존 패키지뿐만 아니라 새 패키지 제출 모두에 해당됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d412-116">This is true for both new package submissions as well as existing packages under the owner(s).</span></span> <span data-ttu-id="9d412-117">**참고:** Visual Studio의 표시기는 단일 피드를 패키지 원본으로 선택한 경우에만 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="9d412-117">**Note:** The indicator in Visual Studio appears only if a single feed is selected as the package source.</span></span>

1. <span data-ttu-id="9d412-118">예약된 ID 접두사와 일치하지만 예약된 접두사 소유자가 소유하지 *않은* 기존의 모든 패키지는 변경되지 않은 상태로 유지됩니다(비공개는 아니지만 시각적 표시기가 없을 수도 있음).</span><span class="sxs-lookup"><span data-stu-id="9d412-118">All previously existing packages that match the reserved ID prefix, but are *not* owned by the owner of the reserved prefix will remain unchanged (they will not be unlisted, but they will also not have the visual indicator).</span></span> <span data-ttu-id="9d412-119">또한 이러한 패키지의 소유자는 패키지에 새 버전을 계속 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d412-119">In addition, owners of these packages will still be able to submit new versions to the package.</span></span>

<span data-ttu-id="9d412-120">이러한 변경 내용은 다음 조건을 기반으로 몇 가지 추가 제한 사항이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d412-120">These changes are based on the following conditions and impose several additional restrictions:</span></span>

- <span data-ttu-id="9d412-121">패키지의 한 소유자만 시각적 표시기가 표시되도록 예약된 접두사를 가져야 합니다(여러 소유자가 있는 패키지의 경우).</span><span class="sxs-lookup"><span data-stu-id="9d412-121">Only one owner of a package needs to have the reserved prefix for the visual indicator to appear (for packages with multiple-owners).</span></span>

- <span data-ttu-id="9d412-122">하나 이상의 소유자가 예약된 접두사를 가지고 있고, 하나 이상의 소유자가 예약된 접두사를 가지고 있지 않은 패키지의 소유자가 둘 이상이 있는 경우, 예약된 접두사를 가진 소유자만 예약된 접두사를 가진 다른 소유자를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d412-122">If there is more than one owner of a package where one or more owners has the reserved prefix and one or more owners does not have the reserved prefix, then only the owner(s) with the reserved prefix can remove other owner(s) with a reserved prefix.</span></span> <span data-ttu-id="9d412-123">예약된 접두사가 없는 소유자는 해당 접두사가 예약된 소유자를 제거할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9d412-123">The owners who do not have the prefix reserved cannot remove owners with the prefix reserved.</span></span> <span data-ttu-id="9d412-124">예약된 접두사를 갖고 있지 않은 다른 소유자를 여전히 제거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d412-124">They can still remove other owners that also do not have the prefix reserved.</span></span>

- <span data-ttu-id="9d412-125">패키지에 시각적 표시기가 있으면 *항상* 시각적 표시기가 있어야 합니다(예약된 접두사를 가진 하나 이상의 소유자가 항상 소유자로 남아 있음을 보장함).</span><span class="sxs-lookup"><span data-stu-id="9d412-125">Once a package has the visual indicator, it should *always* have the visual indicator (guaranteeing that at least one owner with the reserved prefix will always remain an owner)</span></span>

### <a name="advanced-prefix-reservation-scenarios"></a><span data-ttu-id="9d412-126">고급 접두사 예약 시나리오</span><span class="sxs-lookup"><span data-stu-id="9d412-126">Advanced prefix reservation scenarios</span></span>

<span data-ttu-id="9d412-127">하위 접두사 위임 및 접두사를 공용으로 표시하는 것을 포함하여 아래에 설명된 몇 가지 고급 접두사 예약 시나리오가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d412-127">There are several more advanced prefix reservation scenarios described below, including subprefix delegation, and marking prefixes as public.</span></span> <span data-ttu-id="9d412-128">다음은 수행할 수 있는 고급 접두사 예약입니다.</span><span class="sxs-lookup"><span data-stu-id="9d412-128">Below are the more advanced prefix reservations that can be made.</span></span> 

- <span data-ttu-id="9d412-129">접두사 예약 중에 소유자는 다른 소유자에게 접두사 하위 집합(또는 접두사)의 위임을 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d412-129">During prefix reservation, the owner can request delegation of prefix subsets (or the prefix) to other owners.</span></span> <span data-ttu-id="9d412-130">예를 들어 '[Microsoft](https://www.nuget.org/profiles/microsoft)'가 'Microsoft를 소유\*'하지만 '[aspnet](https://www.nuget.org/profiles/aspnet)이 'Microsoft.AspNet \*'을 예약하려는 경우, '[Microsoft](https://www.nuget.org/profiles/microsoft)'는 'Microsoft.AspNet.\*'을 [aspnet](https://www.nuget.org/profiles/aspnet) 계정에 위임하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d412-130">For example, if '[Microsoft](https://www.nuget.org/profiles/microsoft)' owns 'Microsoft.\*', but '[aspnet](https://www.nuget.org/profiles/aspnet)' wants to reserve 'Microsoft.AspNet.\*', '[Microsoft](https://www.nuget.org/profiles/microsoft)' can choose to delegate 'Microsoft.AspNet.\*' to the [aspnet](https://www.nuget.org/profiles/aspnet) account.</span></span>

- <span data-ttu-id="9d412-131">접두사 예약 중에 소유자는 접두사를 공개하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d412-131">During prefix reservation, the owner can choose to make a prefix public.</span></span> <span data-ttu-id="9d412-132">이렇게 하면 패키지가 예약된 접두사에서 시작되는 것을 보여주는 시각적 표시기가 제공되지만 소유자에 대한 접두사의 향후 패키지 제출을 차단하지는 **않습니다**.</span><span class="sxs-lookup"><span data-stu-id="9d412-132">This will still give them the visual indicator showing that the package originates from a reserved prefix, but it will **not** block future package submissions on the prefix for any owner.</span></span> <span data-ttu-id="9d412-133">이는 많은 기여자가 있는 오픈 소스 프로젝트에 유용합니다. 상위 또는 핵심 기여자는 접두사를 예약할 수 있지만 모든 기여자에게 계속 공개될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d412-133">This is useful for open source projects with many contributors - the top or core contributors can have the prefix reserved, but it can still be open to all contributors.</span></span> 

### <a name="prefix-reservation-visual-indicator"></a><span data-ttu-id="9d412-134">접두사 예약 시각적 표시기</span><span class="sxs-lookup"><span data-stu-id="9d412-134">Prefix reservation visual indicator</span></span>

<span data-ttu-id="9d412-135">예약된 접두사에서 패키지를 가져오는 경우 [nuget.org](https://www.nuget.org/) 갤러리 및 Visual Studio 2017 버전 15.4 이상에서 다음 시각적 표시기가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="9d412-135">When a package comes from a reserved prefix, you see the below visual indicators on the [nuget.org](https://www.nuget.org/) gallery and in Visual Studio 2017 version 15.4 or later:</span></span>

<span data-ttu-id="9d412-136">**nuget.org 갤러리**
![nuget.org 갤러리](media/nuget-gallery-reserved-prefix.png)</span><span class="sxs-lookup"><span data-stu-id="9d412-136">**nuget.org Gallery**
![nuget.org Gallery](media/nuget-gallery-reserved-prefix.png)</span></span>

<span data-ttu-id="9d412-137">**Visual Studio**
![Visual Studio](media/visual-studio-reserved-prefix.png)</span><span class="sxs-lookup"><span data-stu-id="9d412-137">**Visual Studio**
![Visual Studio](media/visual-studio-reserved-prefix.png)</span></span>

## <a name="id-prefix-reservation-application-process"></a><span data-ttu-id="9d412-138">ID 접두사 예약 애플리케이션 프로세스</span><span class="sxs-lookup"><span data-stu-id="9d412-138">ID prefix reservation application process</span></span>

1. <span data-ttu-id="9d412-139">[ID 접두사 예약에 대한 기준](#id-prefix-reservation-criteria) 허용을 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="9d412-139">Review the acceptance [criteria for prefix ID reservation](#id-prefix-reservation-criteria).</span></span>

2. <span data-ttu-id="9d412-140">필요할 수 있는 [고급 접두사 예약 시나리오](#advanced-prefix-reservation-scenarios) 외에도 예약할 접두사를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="9d412-140">Determine the prefixes you want to reserve, in addition to any [advanced prefix reservation scenarios](#advanced-prefix-reservation-scenarios) you may require.</span></span>

3. <span data-ttu-id="9d412-141">이메일을 요청 중인 예약된 접두사뿐만 아니라 [nuget.org](https://www.nuget.org/)의 소유자 표시 이름이 있는 [account@nuget.org](mailto:account@nuget.org)로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9d412-141">Send a mail to [account@nuget.org](mailto:account@nuget.org) with the owner display name on [nuget.org](https://www.nuget.org/), as well as any reserved prefixes you are requesting.</span></span> <span data-ttu-id="9d412-142">여러 소유자에게 접두사 하위 집합을 위임하는 경우 모든 소유자 표시 이름과 접두사 하위 집합을 언급했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9d412-142">If you are delegating prefix subsets to multiple owners, make sure you mention all owner display names and prefix subsets.</span></span>

<span data-ttu-id="9d412-143">애플리케이션을 제출한 후 승인 또는 거부(거부를 초래한 기준 포함)에 대한 통보를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="9d412-143">After the application is submitted, you are notified of acceptance or rejection (with the criteria that caused rejection).</span></span> <span data-ttu-id="9d412-144">소유자 ID를 확인하기 위해 추가적인 식별 질문을 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d412-144">We may need to ask additional identifying questions to confirm owner identity.</span></span>

### <a name="id-prefix-reservation-criteria"></a><span data-ttu-id="9d412-145">ID 접두사 예약 조건</span><span class="sxs-lookup"><span data-stu-id="9d412-145">ID prefix reservation criteria</span></span>

<span data-ttu-id="9d412-146">ID 접두사 예약에 대한 모든 애플리케이션을 검토할 때 [nuget.org](https://www.nuget.org/) 팀은 아래 기준에 따라 애플리케이션을 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="9d412-146">When reviewing any application for ID prefix reservation, the [nuget.org](https://www.nuget.org/) team will evaluate the application against the below criteria.</span></span> <span data-ttu-id="9d412-147">접두사를 예약하기 위해 모든 기준을 충족해야 하는 것은 아니지만, 충족되는 기준에 대한 실질적인 증거가 없는 경우 애플리케이션은 거부될 수 있습니다(지정된 설명 포함).</span><span class="sxs-lookup"><span data-stu-id="9d412-147">Not all criteria needs to be met for a prefix to be reserved, but the application may be denied if there is not substantial evidence of the criteria being met (with an explanation given):</span></span>

1. <span data-ttu-id="9d412-148">패키지 ID 접두사가 제대로 되어 있으며 패키지 소유자를 명확하게 식별하나요?</span><span class="sxs-lookup"><span data-stu-id="9d412-148">Does the package ID prefix properly and clearly identify the package owner?</span></span>

1. <span data-ttu-id="9d412-149">패키지 소유자가 [NuGet.org 계정에서 2FA를 활성화했나요](individual-accounts.md#enable-two-factor-authentication-2fa)?</span><span class="sxs-lookup"><span data-stu-id="9d412-149">Has the package owner [enabled 2FA for their NuGet.org account](individual-accounts.md#enable-two-factor-authentication-2fa)?</span></span>

1. <span data-ttu-id="9d412-150">소유자가 이미 제출한 패키지의 상당수가 패키지 ID 접두사 아래에 있나요?</span><span class="sxs-lookup"><span data-stu-id="9d412-150">Are a significant number of the packages that have already been submitted by the owner under the package ID prefix?</span></span>

1. <span data-ttu-id="9d412-151">패키지 ID 접두사는 개별 소유자 또는 조직에 속하면 안되는 공통적인 것인가요?</span><span class="sxs-lookup"><span data-stu-id="9d412-151">Is the package ID prefix something common that should not belong to any individual owner or organization?</span></span>

1. <span data-ttu-id="9d412-152">패키지 ID 접두사를 예약하지 *않으면* 커뮤니티에 모호함과 혼동을 일으키나요?</span><span class="sxs-lookup"><span data-stu-id="9d412-152">Would *not* reserving the package ID prefix cause ambiguity and confusion for the community?</span></span>

1. <span data-ttu-id="9d412-153">패키지 ID 접두사와 일치하는 패키지의 식별 속성이 명확하고 일관적인가요(특히 패키지 작성자)?</span><span class="sxs-lookup"><span data-stu-id="9d412-153">Are the identifying properties of the packages that match the package ID prefix clear and consistent (especially the package author)?</span></span>

1. <span data-ttu-id="9d412-154">패키지에 라이선스가 있나요([라이선스](../reference/nuspec.md#license) 메타데이터 요소를 사용하고 사용이 중단된 licenseUrl은 사용하지 않음)?</span><span class="sxs-lookup"><span data-stu-id="9d412-154">Do the packages have a license (using the [license](../reference/nuspec.md#license) metadata element and NOT licenseUrl which is being deprecated)?</span></span>

1. <span data-ttu-id="9d412-155">패키지에 아이콘이 있는 경우, [아이콘](../reference/nuspec.md#icon) 메타데이터 요소(iconUrl을 제거하는 데 필수 요소 아님)를 사용하고 있나요?</span><span class="sxs-lookup"><span data-stu-id="9d412-155">If the packages have an icon (using the iconUrl metadata element), are they also using the [icon](../reference/nuspec.md#icon) metadata element (it is not a requirement to remove the iconUrl)?</span></span>

## <a name="third-party-feed-provider-scenarios"></a><span data-ttu-id="9d412-156">타사 피드 공급자 시나리오</span><span class="sxs-lookup"><span data-stu-id="9d412-156">Third party feed provider scenarios</span></span>

<span data-ttu-id="9d412-157">타사 피드 공급자가 접두사 예약을 제공하기 위해 자체 서비스를 구현하려는 경우, NuGet V3 피드 공급자에서 검색 서비스를 수정하여 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d412-157">If a third party feed provider is interested in implementing their own service to provide prefix reservations, they can do so by modifying the search service in the NuGet V3 feed providers.</span></span> <span data-ttu-id="9d412-158">피드 검색 서비스를 변경하려면 `verified` 속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9d412-158">The change in the feed search service is to add the `verified` property.</span></span> <span data-ttu-id="9d412-159">NuGet 클라이언트는 V2 피드에 추가된 속성을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9d412-159">The NuGet client will not support the added property in the V2 feed.</span></span>

<span data-ttu-id="9d412-160">자세한 내용은 [API의 검색 서비스에 대한 설명서](../api/search-query-service-resource.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9d412-160">For more information, see the [documentation about the API's search service](../api/search-query-service-resource.md).</span></span>

## <a name="package-id-prefix-reservation-dispute-policy"></a><span data-ttu-id="9d412-161">패키지 ID 접두사 예약 분쟁 정책</span><span class="sxs-lookup"><span data-stu-id="9d412-161">Package ID Prefix Reservation Dispute Policy</span></span>
<span data-ttu-id="9d412-162">[NuGet.org](https://www.nuget.org)의 소유자에게 위에 나열된 기준에 위배되는 패키지 ID 접두사 예약이 할당되었거나 상표 또는 저작권을 침해했다고 판단되는 경우, 해당 ID 접두사, ID 접두사의 소유자 및 할당된 접두사 예약에 대해 이의를 제기하는 이유를 이메일 [support@nuget.org](mailto:support@nuget.org)로 보내주세요.</span><span class="sxs-lookup"><span data-stu-id="9d412-162">If you believe an owner on [NuGet.org](https://www.nuget.org) was assigned a package ID prefix reservation that goes against the above listed criteria, or infringes on any trademarks or copyrights, please email [support@nuget.org](mailto:support@nuget.org) with the ID prefix in question, the owner of the ID prefix, and the reason for disputing the assigned prefix reservation.</span></span>

