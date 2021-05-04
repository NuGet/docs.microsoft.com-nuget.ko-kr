---
title: 범위가 지정된 API 키
description: 패키지를 푸시하는 데 사용하는 API 키 제어
author: mikejo5000
ms.author: mikejo
ms.date: 06/04/2019
ms.topic: conceptual
ms.openlocfilehash: a3d2504528249f3545e2eb5d9bce7713029638db
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901592"
---
# <a name="scoped-api-keys"></a><span data-ttu-id="0a6bb-103">범위가 지정된 API 키</span><span class="sxs-lookup"><span data-stu-id="0a6bb-103">Scoped API keys</span></span>

<span data-ttu-id="0a6bb-104">NuGet을 패키지 배포를 위한 보다 안전한 환경으로 만들기 위해 범위를 추가하여 API 키를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-104">To make NuGet a more secure environment for package distribution, you can take control of the API keys by adding scopes.</span></span>

<span data-ttu-id="0a6bb-105">API 키에 범위를 제공하는 기능을 통해 API를 보다 잘 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-105">The ability to provide scope to your API keys give you better control on your APIs.</span></span> <span data-ttu-id="0a6bb-106">다음 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-106">You can:</span></span>

- <span data-ttu-id="0a6bb-107">만료 기간이 다양한 여러 패키지에 사용할 수 있는 범위가 지정된 API 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-107">Create multiple scoped API keys that can be used for different packages with varying expiration timeframes.</span></span>
- <span data-ttu-id="0a6bb-108">API 키를 안전하게 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-108">Obtain API keys securely.</span></span>
- <span data-ttu-id="0a6bb-109">기존 API 키를 편집하여 패키지 적용 가능성을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-109">Edit existing API keys to change package applicability.</span></span>
- <span data-ttu-id="0a6bb-110">다른 키를 사용하는 작업을 방해하지 않고 기존 API 키를 새로 고치거나 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-110">Refresh or delete existing API keys without hampering operations using other keys.</span></span>

## <a name="why-do-we-support-scoped-api-keys"></a><span data-ttu-id="0a6bb-111">범위가 지정된 API 키를 지원하는 이유는?</span><span class="sxs-lookup"><span data-stu-id="0a6bb-111">Why do we support scoped API keys?</span></span>

<span data-ttu-id="0a6bb-112">보다 세분화된 권한을 가질 수 있도록 API 키의 범위를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-112">We support scopes for API keys to allow you to have more fine-grained permissions.</span></span> <span data-ttu-id="0a6bb-113">이전에 NuGet이 계정에 단일 API 키를 제공했지만 해당 방법에는 다음과 같은 몇 가지 단점이 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-113">Previously, NuGet offered a single API key for an account, and that approach had several drawbacks:</span></span>

- <span data-ttu-id="0a6bb-114">**모든 패키지를 제어하는 하나의 API 키**.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-114">**One API key to control all packages**.</span></span> <span data-ttu-id="0a6bb-115">모든 패키지를 관리하는 데 사용되는 단일 API 키를 사용하면 여러 개발자가 서로 다른 패키지와 관련된 경우와 게시자 계정을 공유할 때 키를 안전하게 공유하기가 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-115">With a single API key that is used to manage all packages, it is difficult to securely share the key when multiple developers are involved with different packages, and when they share a publisher account.</span></span>
- <span data-ttu-id="0a6bb-116">**모든 권한 또는 없음**.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-116">**All permissions or none**.</span></span> <span data-ttu-id="0a6bb-117">API 키에 대한 액세스 권한이 있는 모든 사용자는 패키지에 대한 모든 권한(게시, 푸시 및 목록 취소)을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-117">Anyone with access to the API key has all permissions (publish, push and un-list) on the packages.</span></span> <span data-ttu-id="0a6bb-118">이는 여러 팀이 있는 환경에서는 바람직하지 않는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-118">This is often not desirable in environment with multiple teams.</span></span>
- <span data-ttu-id="0a6bb-119">**단일 지점에서 실패**-</span><span class="sxs-lookup"><span data-stu-id="0a6bb-119">**Single point of failure**.</span></span> <span data-ttu-id="0a6bb-120">단일 API 키는 단일 실패 지점을 의미하기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-120">A single API key also means a single point of failure.</span></span> <span data-ttu-id="0a6bb-121">키가 손상되면 계정과 연결된 모든 패키지가 손상될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-121">If the key is compromised, all packages associated with the account could potentially be compromised.</span></span> <span data-ttu-id="0a6bb-122">API 키를 새로 고치는 것만이 누출을 막고 CI/CD 워크플로의 중단을 방지할 수 있는 유일한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-122">Refreshing the API key is the only way to plug the leak and avoid an interruption to your CI/CD workflow.</span></span> <span data-ttu-id="0a6bb-123">또한 개인의 API 키에 대한 액세스 권한을 취소하려는 경우가 있을 수 있습니다(예: 직원이 조직을 떠나는 경우).</span><span class="sxs-lookup"><span data-stu-id="0a6bb-123">In addition, there may be cases when you want to revoke access to the API key for an individual (for example, when an employee leaves the organization).</span></span> <span data-ttu-id="0a6bb-124">현재 이를 깨끗이 처리하는 방법이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-124">There isn’t a clean way to handle this today.</span></span>

<span data-ttu-id="0a6bb-125">범위가 지정된 API 키를 사용하여 기존 워크플로가 중단되지 않도록 하면서 이러한 문제를 해결하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-125">With scoped API keys, we try to address these problems while making sure that none of the existing workflows break.</span></span>

## <a name="acquire-an-api-key"></a><span data-ttu-id="0a6bb-126">API 키 획득</span><span class="sxs-lookup"><span data-stu-id="0a6bb-126">Acquire an API key</span></span>

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

## <a name="create-scoped-api-keys"></a><span data-ttu-id="0a6bb-127">범위가 지정된 API 키 만들기</span><span class="sxs-lookup"><span data-stu-id="0a6bb-127">Create scoped API keys</span></span>

<span data-ttu-id="0a6bb-128">요구 사항에 따라 여러 API 키를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-128">You can create multiple API keys based on your requirements.</span></span> <span data-ttu-id="0a6bb-129">API 키는 하나 이상의 패키지에 적용할 수 있고, 특정 권한이 부여된 다양한 범위를 가질 수 있으며, 이와 관련된 만료 날짜가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-129">An API key can apply to one or more packages, have varying scopes that grant specific privileges, and have an expiration date associated with it.</span></span>

<span data-ttu-id="0a6bb-130">다음 예제에서는 특정 `Contoso.Service` 패키지에 대한 패키지를 푸시하는 데 사용할 수 있는 `Contoso service CI`라는 API 키가 있으며 365일 동안 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-130">In the following example, you have an API key named `Contoso service CI` that can be used to push packages for specific `Contoso.Service` packages, and is valid for 365 days.</span></span> <span data-ttu-id="0a6bb-131">이는 동일한 조직 내의 다른 팀이 서로 다른 패키지에 대해 작업하고, 팀 멤버는 작업하고 있는 패키지에 대해서만 권한을 부여하는 키를 제공받는 일반적인 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-131">This is a typical scenario where different teams within the same organization work on different packages, and the members of the team are provided the key that grants them privileges only for the package they are working on.</span></span> <span data-ttu-id="0a6bb-132">만료는 부실하거나 잊어버린 키를 방지하는 메커니즘의 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-132">The expiration serves as a mechanism to prevent stale or forgotten keys.</span></span>

![API 키 만들기](media/scoped-api-keys-create-new.png)

## <a name="use-glob-patterns"></a><span data-ttu-id="0a6bb-134">GLOB 패턴 사용</span><span class="sxs-lookup"><span data-stu-id="0a6bb-134">Use glob patterns</span></span>

<span data-ttu-id="0a6bb-135">여러 패키지에서 작업하고 관리할 패키지 목록이 많은 경우 globbing 패턴을 사용하여 여러 패키지를 함께 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-135">If you are working on multiple packages and have a large list of packages to manage, you can choose to use globbing patterns to select multiple packages together.</span></span> <span data-ttu-id="0a6bb-136">예를 들어 ID가 `Fabrikam.Service`로 시작하는 모든 패키지의 키에 특정 범위를 부여하려는 경우 **Glob 패턴** 텍스트 상자에 `fabrikam.service.*`를 지정하여 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-136">For example, if you wish to grant specific scopes to a key for all packages whose ID starts with `Fabrikam.Service`, you could do this by specifying `fabrikam.service.*` in the **Glob pattern** text box.</span></span>

![API 키 만들기 - 2](media/scoped-api-keys-glob-pattern.png)

<span data-ttu-id="0a6bb-138">GLOB 패턴을 사용하여 API 키 사용 권한을 결정하는 것은 GLOB 패턴과 일치하는 새 패키지에도 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-138">Using glob patterns to determine API key permissions also applies to new packages matching the glob pattern.</span></span> <span data-ttu-id="0a6bb-139">예를 들어 `Fabrikam.Service.Framework`라는 새 패키지를 푸시하려고 하면 패키지가 GLOB 패턴 `fabrikam.service.*`와 일치하므로 이전에 만든 키를 사용하여 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-139">For example, if you try to push a new package named `Fabrikam.Service.Framework`, you can do that with the key created previously, since the package matches the glob pattern `fabrikam.service.*`.</span></span>

## <a name="obtain-api-keys-securely"></a><span data-ttu-id="0a6bb-140">API 키를 안전하게 얻기</span><span class="sxs-lookup"><span data-stu-id="0a6bb-140">Obtain API keys securely</span></span>

<span data-ttu-id="0a6bb-141">보안을 위해 새로 만든 키는 화면에 표시되지 않으며 **복사** 단추를 통해서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-141">For security, a newly created key is never shown on the screen and is only available using the **Copy** button.</span></span> <span data-ttu-id="0a6bb-142">마찬가지로 페이지를 새로 고친 후에는 키에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-142">Similarly, the key is not accessible after the page is refreshed.</span></span>

![API 키 만들기 - 3](media/scoped-api-keys-obtain-keys.png)

## <a name="edit-existing-api-keys"></a><span data-ttu-id="0a6bb-144">기존 API 키 편집</span><span class="sxs-lookup"><span data-stu-id="0a6bb-144">Edit existing API keys</span></span>

<span data-ttu-id="0a6bb-145">키 자체를 변경하지 않고 키 사용 권한 및 범위를 업데이트할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-145">You may also want to update the key permissions and scopes without changing the key itself.</span></span> <span data-ttu-id="0a6bb-146">단일 패키지에 대해 특정 범위의 키가 있는 경우 하나 이상의 다른 패키지에 동일한 범위를 적용하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-146">If you have a key with specific scope(s) for a single package, you can choose to apply the same scope(s) on one or many other packages.</span></span>

![API 키 만들기 - 4](media/scoped-api-keys-edit.png)

## <a name="refresh-or-delete-existing-api-keys"></a><span data-ttu-id="0a6bb-148">기존 API 키 새로 고침 또는 삭제</span><span class="sxs-lookup"><span data-stu-id="0a6bb-148">Refresh or delete existing API keys</span></span>

<span data-ttu-id="0a6bb-149">계정 소유자는 키를 새로 고치도록 선택할 수 있습니다. 이 경우 사용 권한(패키지), 범위 및 만료는 그대로 유지되지만, 새 키가 발급되어 이전 키를 사용할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-149">The account owner can choose to refresh the key, in which case the permission (on packages), scope, and expiry remain the same, but a new key is issued making the old key unusable.</span></span> <span data-ttu-id="0a6bb-150">이는 부실한 키를 관리하거나 API 키 누출 가능성이 있는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-150">This is helpful in managing stale keys or where there is any potential for an API key leakage.</span></span>

![API 키 만들기 - 5](media/scoped-api-keys-refresh.png)

<span data-ttu-id="0a6bb-152">이러한 키가 더 이상 필요하지 않은 경우 삭제할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-152">You may also choose to delete these keys if they are not needed anymore.</span></span> <span data-ttu-id="0a6bb-153">키를 삭제하면 키가 제거되어 사용할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-153">Deleting a key removes the key and makes it unusable.</span></span>

## <a name="faqs"></a><span data-ttu-id="0a6bb-154">FAQ(질문과 대답)</span><span class="sxs-lookup"><span data-stu-id="0a6bb-154">FAQs</span></span>

### <a name="what-happens-to-my-old-legacy-api-key"></a><span data-ttu-id="0a6bb-155">내 이전(레거시) API 키는 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="0a6bb-155">What happens to my old (legacy) API key?</span></span>

<span data-ttu-id="0a6bb-156">이전 API 키(레거시)는 계속 작동하며 원하는 만큼 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-156">Your old API key (legacy) continues to work and can work as long as you want it to work.</span></span> <span data-ttu-id="0a6bb-157">그러나 이러한 키는 패키지를 푸시하는 데 365일을 초과하여 사용되지 않은 경우 폐기됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-157">However, these keys will be retired if they have not been used for more than 365 days to push a package.</span></span> <span data-ttu-id="0a6bb-158">자세한 내용은 블로그 게시물 [만료되는 API 키 변경](https://blog.nuget.org/20160825/Changes-to-Expiring-API-Keys.html)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-158">For more details, see the blog post [Changes to expiring API keys](https://blog.nuget.org/20160825/Changes-to-Expiring-API-Keys.html).</span></span> <span data-ttu-id="0a6bb-159">더 이상 이 키를 새로 고칠 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-159">You can no longer refresh this key.</span></span> <span data-ttu-id="0a6bb-160">레거시 키를 삭제하고 대신 새 범위가 지정된 키를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-160">You need to delete the legacy key and create a new scoped key instead.</span></span>

> [!NOTE]
> <span data-ttu-id="0a6bb-161">이 키는 모든 패키지에 대한 모든 권한을 가지고 있으며 만료되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-161">This key has all permissions on all the packages and it never expires.</span></span> <span data-ttu-id="0a6bb-162">이 키를 삭제하고 범위가 지정된 사용 권한과 만료 기간이 확실한 새 키를 만드는 것을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-162">You should consider deleting this key and creating new keys with scoped permissions and definite expiry.</span></span>

### <a name="how-many-api-keys-can-i-create"></a><span data-ttu-id="0a6bb-163">몇 개의 API 키를 만들 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="0a6bb-163">How many API keys can I create?</span></span>

<span data-ttu-id="0a6bb-164">만들 수 있는 API 키의 수에는 제한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-164">There is no limit on the number of API keys you can create.</span></span> <span data-ttu-id="0a6bb-165">그러나 어디서 누가 사용하고 있는지에 대해 알지 못하는 많은 오래된 키를 가지고 있지 않도록 관리하기 쉬운 수로 유지하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-165">However, we advise you to keep it to a manageable count so that you do not end up having many stale keys with no knowledge of where and who is using them.</span></span>

### <a name="can-i-delete-my-legacy-api-key-or-discontinue-using-now"></a><span data-ttu-id="0a6bb-166">지금 내 레거시 API 키를 삭제하거나 사용을 중지할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="0a6bb-166">Can I delete my legacy API key or discontinue using now?</span></span>

<span data-ttu-id="0a6bb-167">예.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-167">Yes.</span></span> <span data-ttu-id="0a6bb-168">레거시 API 키를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-168">You can--and you probably should--delete your legacy API key.</span></span>

### <a name="can-i-get-back-my-api-key-that-i-deleted-by-mistake"></a><span data-ttu-id="0a6bb-169">실수로 삭제한 내 API 키를 되돌릴 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="0a6bb-169">Can I get back my API key that I deleted by mistake?</span></span>

<span data-ttu-id="0a6bb-170">아니요.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-170">No.</span></span> <span data-ttu-id="0a6bb-171">삭제되면 새 키만 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-171">Once deleted, you can only create new keys.</span></span> <span data-ttu-id="0a6bb-172">실수로 삭제된 키는 복구할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-172">There is no recovery possible for accidentally deleted keys.</span></span>

### <a name="does-the-old-api-key-continue-to-work-upon-api-key-refresh"></a><span data-ttu-id="0a6bb-173">API 키 새로 고침 시 이전 API 키가 계속 작동하고 있나요?</span><span class="sxs-lookup"><span data-stu-id="0a6bb-173">Does the old API key continue to work upon API key refresh?</span></span>

<span data-ttu-id="0a6bb-174">아니요.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-174">No.</span></span> <span data-ttu-id="0a6bb-175">키를 새로 고치면 이전 키와 범위, 사용 권한 및 만료 기간이 동일한 새 키가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-175">Once you refresh a key, a new key gets generated that has the same scope, permission, and expiry as the old one.</span></span> <span data-ttu-id="0a6bb-176">이전 키는 사라집니다.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-176">The old key ceases to exist.</span></span>

### <a name="can-i-give-more-permissions-to-an-existing-api-key"></a><span data-ttu-id="0a6bb-177">기존 API 키에 추가 권한을 부여할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="0a6bb-177">Can I give more permissions to an existing API key?</span></span>

<span data-ttu-id="0a6bb-178">범위를 수정할 수 없지만 적용 가능한 패키지 목록을 편집할 수는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-178">You cannot modify the scope, but you can edit the package list it is applicable to.</span></span>

### <a name="how-do-i-know-if-any-of-my-keys-expired-or-are-getting-expired"></a><span data-ttu-id="0a6bb-179">내 키가 만료되었거나 만료되는지 확인하는 방법은?</span><span class="sxs-lookup"><span data-stu-id="0a6bb-179">How do I know if any of my keys expired or are getting expired?</span></span>

<span data-ttu-id="0a6bb-180">키가 만료되면 페이지 맨 위에 있는 경고 메시지를 통해 알려드립니다.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-180">If any key expires, we will let you know through a warning message at the top of the page.</span></span> <span data-ttu-id="0a6bb-181">또한 사전에 잘 대처할 수 있도록 키가 만료되기 10일 전에 계정 소유자에게 경고 이메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="0a6bb-181">We also send a warning e-mail to the account holder ten days before the expiration of the key so that you can act on it well in advance.</span></span>