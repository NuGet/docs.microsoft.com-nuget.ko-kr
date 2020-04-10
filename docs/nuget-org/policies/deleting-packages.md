---
title: nuget.org에서 NuGet 패키지 삭제
description: nuget.org에서 패키지를 제외하는 정책; 패키지가 다른 정책을 위반하는 경우를 제외하고 영구 삭제가 지원되지 않습니다.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 3abe809d76e75801c2f936aba129d27ba7b64913
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/07/2020
ms.locfileid: "80581275"
---
# <a name="deleting-packages"></a><span data-ttu-id="32f95-103">패키지 삭제</span><span class="sxs-lookup"><span data-stu-id="32f95-103">Deleting packages</span></span>

<span data-ttu-id="32f95-104">nuget.org에서는 패키지를 영구적으로 삭제하도록 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="32f95-104">nuget.org does not support permanent deletion of packages.</span></span> <span data-ttu-id="32f95-105">이렇게 하면 특히 패키지 복원을 포함하는 빌드 워크플로를 사용하여 패키지의 사용 가능성에 따라 모든 프로젝트를 중단합니다.</span><span class="sxs-lookup"><span data-stu-id="32f95-105">Doing so would break every project depending on the availability of the package, especially with build workflows that involve package restore.</span></span>

<span data-ttu-id="32f95-106">nuget.org에서는 [패키지를 제외](#unlisting-a-package)하도록 지원합니다. 이 기능은 웹 사이트의 패키지 관리 페이지에서 수행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32f95-106">nuget.org does supports [unlisting a package](#unlisting-a-package), which can be done in the package management page on the web site.</span></span> <span data-ttu-id="32f95-107">제외된 패키지는 nuget.org 또는 Visual Studio UI에 표시되지 않으며 검색 결과에도 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="32f95-107">Unlisted packages don't appear on nuget.org or in the Visual Studio UI, and do not appear in search results.</span></span> <span data-ttu-id="32f95-108">그러나 패키지 복원을 지원하는 정확한 버전 번호를 사용하여 제외된 패키지를 다운로드하고 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32f95-108">Unlisted packages, however, can still be downloaded and installed by using an exact version number, which supports package restore.</span></span> <span data-ttu-id="32f95-109">또한 다음과 같은 특정 시나리오에서 제외된 패키지를 계속 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32f95-109">In addition, unlisted packages may still be discovered in the following specific scenarios:</span></span>

- <span data-ttu-id="32f95-110">버전 또는 종속성 제약 조건과 일치하는 최신 사용 가능한 패키지가 제외된 패키지인 경우 부동 버전을 사용하는 패키지 복원(예: `1.0.0-*`)</span><span class="sxs-lookup"><span data-stu-id="32f95-110">Package restore using floating versions (for example, `1.0.0-*`), if the latest available package matching the version or dependency constraints is an unlisted package.</span></span>
- <span data-ttu-id="32f95-111">카탈로그를 통한 패키지의 복제(카탈로그에 제외된 패키지가 포함된 경우)</span><span class="sxs-lookup"><span data-stu-id="32f95-111">Replication of packages through the catalog (as the catalog also contains unlisted packages).</span></span>

## <a name="exceptions"></a><span data-ttu-id="32f95-112">예외</span><span class="sxs-lookup"><span data-stu-id="32f95-112">Exceptions</span></span>

<span data-ttu-id="32f95-113">저작권 침해 및 잠재적으로 위험한 콘텐츠와 같은 예외적인 상황에 NuGet 팀에서 패키지를 수동으로 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32f95-113">In exceptional situations such as copyright infringement and potentially harmful content, packages can be deleted manually by the NuGet team.</span></span> <span data-ttu-id="32f95-114">NuGet.org 패키지 세부 정보 페이지의 "신고하기" 단추를 사용하여 패키지를 보고할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32f95-114">You can report a package using the "Report abuse" button on the NuGet.org package details page.</span></span> <span data-ttu-id="32f95-115">패키지 소유자인 경우 NuGet.org 계정에 로그인하여 NuGet.org 패키지 세부 정보 페이지의 "지원 문의" 단추를 사용하여 NuGet 지원팀에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="32f95-115">If you are the package owner, login to your NuGet.org account to reach NuGet support using the "Contact support" button on the NuGet.org package details page.</span></span>

## <a name="prohibited-use"></a><span data-ttu-id="32f95-116">사용 금지</span><span class="sxs-lookup"><span data-stu-id="32f95-116">Prohibited use</span></span>

<span data-ttu-id="32f95-117">패키지가 다음 조건 중 하나를 충족하는 경우 공용 NuGet 갤러리에서 허용되지 않으며 토론 없이 즉시 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="32f95-117">Packages that meet any of the following criteria are not allowed on the public NuGet gallery and will be immediately removed without discussion.</span></span> <span data-ttu-id="32f95-118">그러나 패키지 소유자는 제거되었다는 알림을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="32f95-118">Package owners will, however, be notified of the removal.</span></span>

- <span data-ttu-id="32f95-119">맬웨어, 애드웨어 또는 어떠한 종류의 스파이웨어가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="32f95-119">Contains malware, adware, or any kind of spyware.</span></span>
- <span data-ttu-id="32f95-120">개발자의 워크스테이션 또는 해당 조직을 손상시키도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="32f95-120">Are designed to harm a developer's workstation or their organization.</span></span>
- <span data-ttu-id="32f95-121">저작권을 침해하거나 라이선스를 위반합니다.</span><span class="sxs-lookup"><span data-stu-id="32f95-121">Infringes copyrights or violates licenses.</span></span>
- <span data-ttu-id="32f95-122">위법 콘텐츠가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="32f95-122">Contains illegal content.</span></span>
- <span data-ttu-id="32f95-123">생산성 0인 콘텐츠가 있는 패키지를 포함하여 패키지 식별자를 점유하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="32f95-123">Are being used to squat on package identifiers, including packages that have zero productive content.</span></span> <span data-ttu-id="32f95-124">패키지에는 코드가 포함되어야 합니다. 또는 소유자는 실제로 제품을 제공할 사람에게 식별자를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="32f95-124">Packages must contain code or the owners must concede the identifier to someone who actually has a product to ship.</span></span>
- <span data-ttu-id="32f95-125">갤러리가 수행하도록 명시적으로 설계되지 않은 작업을 수행하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="32f95-125">Attempt to make the gallery do something that it's not explicitly designed to do.</span></span>

<span data-ttu-id="32f95-126">이러한 항목에 위반되는 패키지를 찾는 경우 패키지 세부 정보 페이지에서 **신고하기** 링크를 클릭하고 보고서를 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="32f95-126">If you find a package that is in violation of any of these items, click the **Report Abuse** link on the package details page and submit a report.</span></span>

<span data-ttu-id="32f95-127">NuGet 팀 및 .NET Foundation은 언제든지 이러한 조건을 변경할 권리를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="32f95-127">Note that the NuGet team and the .NET Foundation reserves the right to change these criteria at any time.</span></span>

## <a name="unlisting-a-package"></a><span data-ttu-id="32f95-128">패키지 제외</span><span class="sxs-lookup"><span data-stu-id="32f95-128">Unlisting a package</span></span>
<span data-ttu-id="32f95-129">패키지 버전을 제외하면 검색 및 nuget.org 패키지 정보 페이지에서 해당 버전이 숨겨집니다.</span><span class="sxs-lookup"><span data-stu-id="32f95-129">Unlisting a package version hides it from search and from nuget.org package details page.</span></span> <span data-ttu-id="32f95-130">이 경우 패키지의 기존 사용자가 해당 패키지 버전을 계속 사용할 수 있지만 패키지가 검색에 표시되지 않기 때문에 새로운 채택이 감소합니다.</span><span class="sxs-lookup"><span data-stu-id="32f95-130">This allows existing users of the package to continue using it but reduces new adoption since the package is not visible in search.</span></span>

<span data-ttu-id="32f95-131">패키지를 제외하는 단계:</span><span class="sxs-lookup"><span data-stu-id="32f95-131">Steps to unlist a package:</span></span>

1. <span data-ttu-id="32f95-132">`Your account name` (오른쪽 위 모서리) >`Manage packages` > `Published packages` 선택</span><span class="sxs-lookup"><span data-stu-id="32f95-132">Select `Your account name` (at the top right corner) >`Manage packages` > `Published packages`</span></span>
1. <span data-ttu-id="32f95-133">“패키지 관리” 아이콘 선택</span><span class="sxs-lookup"><span data-stu-id="32f95-133">Select the "Manage package" icon</span></span>
1. <span data-ttu-id="32f95-134">“목록” 섹션을 확장하고 패키지 버전 선택</span><span class="sxs-lookup"><span data-stu-id="32f95-134">Expand the "Listing" section and select the package version</span></span>
1. <span data-ttu-id="32f95-135">“검색 결과 목록”을 선택 취소하고 “저장” 선택</span><span class="sxs-lookup"><span data-stu-id="32f95-135">Uncheck “List in search results” and select "Save"</span></span>

<span data-ttu-id="32f95-136">이제 특정 패키지 버전이 제외되었습니다.</span><span class="sxs-lookup"><span data-stu-id="32f95-136">The specific package version has now been unlisted.</span></span> <span data-ttu-id="32f95-137">이를 확인하려면 계정에서 로그아웃하고 패키지 페이지(버전 부분 제외)로 이동합니다(예: https://www.nuget.org/packages/YOUR-PACKAGE-NAME/ ).</span><span class="sxs-lookup"><span data-stu-id="32f95-137">In order to verify this, logout of your account and navigate to the package page (without the version part) e.g.: https://www.nuget.org/packages/YOUR-PACKAGE-NAME/.</span></span> <span data-ttu-id="32f95-138">제외되지 **않은** 패키지의 모든 버전이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="32f95-138">You will see all versions of that package that have **not** been unlisted.</span></span> <span data-ttu-id="32f95-139">그러나 패키지 소유자는 로그인하면 모든 버전 및 해당 목록 상태를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32f95-139">However, the package owner, when logged in, can see all versions and their listing status.</span></span>

<span data-ttu-id="32f95-140">패키지 버전을 삭제할 수 없다면 더 이상 사용하지 못할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32f95-140">It's also possible to deprecate a package version (in case you can't delete a package version).</span></span> <span data-ttu-id="32f95-141">패키지 버전 사용 중단에 대한 자세한 내용은 [패키지 사용 중단](../deprecate-packages.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="32f95-141">For more information about deprecating package versions, see [Deprecating packages](../deprecate-packages.md).</span></span>
