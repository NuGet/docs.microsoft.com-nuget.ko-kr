---
title: Nuget.org에 조직
description: Nuget.org에서 조직을 사용 하면 그룹 또는 팀, 회사 환경에서에서 게시 된 패키지를 관리할 수 있습니다.
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: 7f40654a08ac221c5ec3a90c86387b6760b28994
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/22/2018
ms.locfileid: "34449580"
---
# <a name="organization-on-nugetorg"></a><span data-ttu-id="e8a10-103">Nuget.org에 조직</span><span class="sxs-lookup"><span data-stu-id="e8a10-103">Organization on nuget.org</span></span>

<span data-ttu-id="e8a10-104">조직의는 비즈니스 및 오픈 소스 프로젝트를 단일 nuget.org id를 사용 하 여 패키지에서 공동 작업을 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8a10-104">Organizations enable businesses and open-source projects to collaborate on packages using a single nuget.org identity.</span></span> <span data-ttu-id="e8a10-105">패키지 소비자에 대 한 조직 계정을 nuget.org에 기존 사용자 계정으로 동일한 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="e8a10-105">For a package consumer, an organization account appears same as an existing user account on nuget.org.</span></span>

## <a name="user-accounts-vs-organization-accounts"></a><span data-ttu-id="e8a10-106">조직 계정 및 사용자 계정</span><span class="sxs-lookup"><span data-stu-id="e8a10-106">User accounts vs. organization accounts</span></span>

<span data-ttu-id="e8a10-107">사용자 계정이 nuget.org 본인 이며의 조직에서는 여러의 구성원이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8a10-107">Your user account is your identity on nuget.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="e8a10-108">패키지는 사용자 계정에 속할 수와 같은 조직 계정에 속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8a10-108">A package can belong to an organization account like it can belong to a user account.</span></span> <span data-ttu-id="e8a10-109">패키지 소비자는 사용자 계정 또는 조직 계정 간의 차이점을 표시 하지 않습니다: 패키지로 표시 둘 다 `owners`합니다.</span><span class="sxs-lookup"><span data-stu-id="e8a10-109">Package consumers don't see any difference between an user account or the organization account: both appear as package `owners`.</span></span>

<span data-ttu-id="e8a10-110">조직 계정은 구성원으로 사용자 계정을 하나 이상에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8a10-110">An organization account has one or more user accounts as its members.</span></span> <span data-ttu-id="e8a10-111">이러한 멤버 소유권에 대 한 단일 id를 유지 하면서 패키지의 집합을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8a10-111">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

## <a name="adding-a-new-organization"></a><span data-ttu-id="e8a10-112">새 조직 추가</span><span class="sxs-lookup"><span data-stu-id="e8a10-112">Adding a new organization</span></span>

<span data-ttu-id="e8a10-113">새 조직을 추가 하려면 계정에 nuget.org 선택 하 고 선택 된 **조직 관리...**  메뉴 명령:</span><span class="sxs-lookup"><span data-stu-id="e8a10-113">To add a new organization, select your account on nuget.org, then select the **Manage Organizations...** menu command:</span></span>

![관리자 조직 nuget.org에 메뉴 옵션](media/org-manage-option.png)

<span data-ttu-id="e8a10-115">다음 페이지에서 선택 된 **새 조직 추가** 단추:</span><span class="sxs-lookup"><span data-stu-id="e8a10-115">On the next page, select the **Add new organization** button:</span></span>

![Nuget.org에 새 조직을 만들기 단추](media/org-add-new-option.png)

<span data-ttu-id="e8a10-117">다음 페이지에서 조직 이름 및 전자 메일 주소를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8a10-117">On the next page, provide the organization name and email address.</span></span> <span data-ttu-id="e8a10-118">조직 계정을 사용자 계정으로 동일한 네임 스페이스를 공유 하기 때문에 조직 이름을 다른 기존 조직 또는 사용자 계정에서 달라 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8a10-118">Since organization accounts share the same namespace as user accounts, the organization name must be different from any other existing organization or user accounts.</span></span> <span data-ttu-id="e8a10-119">전자 메일 주소 모든 계정에서 고유 수도 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8a10-119">The email address must also be unique across all accounts.</span></span>

![새 조직 페이지 nuget.org에 추가](media/org-add-new-page.png)

<span data-ttu-id="e8a10-121">조직 계정이 만들어지면 관리자 및 조직에 대 한 패키지를 전송 하 고 추가할 수 조직 구성원.</span><span class="sxs-lookup"><span data-stu-id="e8a10-121">Once the organization account is created, you are the administrator and can submit packages for the organization and add organization members.</span></span>

### <a name="transform-existing-account-to-an-organization"></a><span data-ttu-id="e8a10-122">조직에 기존 계정 변환</span><span class="sxs-lookup"><span data-stu-id="e8a10-122">Transform existing account to an organization</span></span>

> [!Warning]
> <span data-ttu-id="e8a10-123">계정 변환과 취소할 수 없습니다: 조직의 사용자 계정으로 다시 변환할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e8a10-123">Account conversion is irreversible: you cannot transform an organization back to a user account.</span></span>

<span data-ttu-id="e8a10-124">단일 사용자 계정을 사용 하 여 팀으로 패키지를 관리 하 고 해당 계정을 사용 하 여 조직으로 변환 하려고 하는 경우는 **조직 계정을 변환** 옵션에 **관리 조직** 페이지:</span><span class="sxs-lookup"><span data-stu-id="e8a10-124">If you're managing packages as a team using a single user account and would like to convert that account into an organization, use the **Transform your account to an organization** option on the **Manage Organizations** page:</span></span>

![조직에 기존 계정을 변환할 nuget.org에 옵션](media/org-transform-option.png)

<span data-ttu-id="e8a10-126">다음 페이지에서 조직의 관리자로 할당 한 다음를 선택 하는 데 다른 사용자 계정을 지정 **변환**합니다.</span><span class="sxs-lookup"><span data-stu-id="e8a10-126">On the next page, specify different user account to assign as the administrator of the organization, then select **Transform**.</span></span>

![조직에 사용자 계정을 변환에 대 한 정보를 입력 합니다.](media/org-transform-page.png)

## <a name="managing-organization-members"></a><span data-ttu-id="e8a10-128">조직 멤버 관리</span><span class="sxs-lookup"><span data-stu-id="e8a10-128">Managing organization members</span></span>

<span data-ttu-id="e8a10-129">조직 관리자 권한으로 각 멤버의 nuget.org를 제공 하 여 멤버를 추가할 수 있습니다 *사용자 계정 이름*; 전자 메일 주소를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e8a10-129">As the organization administrator, you can add members by providing each member's nuget.org *user account name*; email addresses cannot be used.</span></span> <span data-ttu-id="e8a10-130">협력자 또는 다음 사용 권한 가진 관리자가 각 멤버를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e8a10-130">You then mark each member as a collaborator or administrator with the following permissions:</span></span>

| <span data-ttu-id="e8a10-131">사용 권한</span><span class="sxs-lookup"><span data-stu-id="e8a10-131">Permission</span></span> | <span data-ttu-id="e8a10-132">공동 작업자</span><span class="sxs-lookup"><span data-stu-id="e8a10-132">Collaborator</span></span> | <span data-ttu-id="e8a10-133">관리자</span><span class="sxs-lookup"><span data-stu-id="e8a10-133">Administrator</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e8a10-134">조직의 패키지 관리</span><span class="sxs-lookup"><span data-stu-id="e8a10-134">Manage the organization's packages</span></span><br/><span data-ttu-id="e8a10-135">(새 패키지를 전송, 업데이트 또는 기존 패키지를 unlist)</span><span class="sxs-lookup"><span data-stu-id="e8a10-135">(submit new packages, update or unlist existing packages)</span></span> | <span data-ttu-id="e8a10-136">예</span><span class="sxs-lookup"><span data-stu-id="e8a10-136">Yes</span></span> | <span data-ttu-id="e8a10-137">예</span><span class="sxs-lookup"><span data-stu-id="e8a10-137">Yes</span></span> |
| <span data-ttu-id="e8a10-138">변경 내용 조직 메타 데이터</span><span class="sxs-lookup"><span data-stu-id="e8a10-138">Change organization metadata</span></span><br/><span data-ttu-id="e8a10-139">(전자 메일 주소를 알림 설정)</span><span class="sxs-lookup"><span data-stu-id="e8a10-139">(email address, notification settings)</span></span> | <span data-ttu-id="e8a10-140">아니요</span><span class="sxs-lookup"><span data-stu-id="e8a10-140">No</span></span> | <span data-ttu-id="e8a10-141">예</span><span class="sxs-lookup"><span data-stu-id="e8a10-141">Yes</span></span> |
| <span data-ttu-id="e8a10-142">조직 멤버 관리</span><span class="sxs-lookup"><span data-stu-id="e8a10-142">Manage organization members</span></span> | <span data-ttu-id="e8a10-143">아니요</span><span class="sxs-lookup"><span data-stu-id="e8a10-143">No</span></span> | <span data-ttu-id="e8a10-144">예</span><span class="sxs-lookup"><span data-stu-id="e8a10-144">Yes</span></span> |
| <span data-ttu-id="e8a10-145">요청 또는 관련 조직 패키지에 대 한 co-ownership 요청 작업</span><span class="sxs-lookup"><span data-stu-id="e8a10-145">Request or act on co-ownership requests for organization packages</span></span> | <span data-ttu-id="e8a10-146">아니요</span><span class="sxs-lookup"><span data-stu-id="e8a10-146">No</span></span> | <span data-ttu-id="e8a10-147">예</span><span class="sxs-lookup"><span data-stu-id="e8a10-147">Yes</span></span> |

## <a name="managing-packages"></a><span data-ttu-id="e8a10-148">패키지 관리</span><span class="sxs-lookup"><span data-stu-id="e8a10-148">Managing packages</span></span>

<span data-ttu-id="e8a10-149">계정 및는 구성원 인 모든 조직에서 모든 패키지를 볼 수는 [패키지 관리](https://www.nuget.org/account/Packages) 페이지.</span><span class="sxs-lookup"><span data-stu-id="e8a10-149">You can view all the packages across your account and all organizations of which you're a member on the [Manage Packages](https://www.nuget.org/account/Packages) page.</span></span> <span data-ttu-id="e8a10-150">특정 조직 또는 계정 관련 패키지를 보려면 계정을 필터 상단 사용 하 여 페이지의 오른쪽입니다.</span><span class="sxs-lookup"><span data-stu-id="e8a10-150">To view the packages specific to your account or any specific organization, use the accounts filter on the top right of the page.</span></span>

![계정 필터를 사용 하 여 패키지를 관리](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a><span data-ttu-id="e8a10-152">조직에 패키지를 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="e8a10-152">Transferring packages to an organization</span></span>
<span data-ttu-id="e8a10-153">새로 만든된 조직에 패키지의 일부를 전송 하려는 경우 패키지를 공동 소유 조직 계정을 요청 하 고 소유자를 제거 하는 사용자가 직접 그렇게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8a10-153">If you wish to transfer some of your packages to a newly created organization, you can do so by requesting the organization account to co-own the package and then removing yourself as the owner.</span></span> <span data-ttu-id="e8a10-154">조직의 관리자 인 경우 소유권에 동의 하는 데 필요한 확인 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e8a10-154">If you are an administrator of the organization, there is no confirmation required to accept the ownership.</span></span> <span data-ttu-id="e8a10-155">그러나 공동 작업자 인 경우 조직 소유자로 추가의 소유권을 수락 하도록 관리자가 하나 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8a10-155">However, if you are a collaborator, adding the organization as an owner requires one of the administrators to accept the ownership.</span></span>

## <a name="publishing-packages"></a><span data-ttu-id="e8a10-156">패키지 게시</span><span class="sxs-lookup"><span data-stu-id="e8a10-156">Publishing packages</span></span>

<span data-ttu-id="e8a10-157">사용자 계정에 패키지를 게시할와 같은 조직에 패키지를 게시할: 직접 nuget.org를 패키지를 업로드 하 여 또는 패키지를 통해 푸시하여는 `nuget push` 또는 `dotnet nuget push` CLI 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="e8a10-157">You publish packages to an organization like you publish packages to a user account: by directly uploading the package to nuget.org or by pushing the package through the `nuget push` or `dotnet nuget push` CLI commands.</span></span>

### <a name="uploading-packages"></a><span data-ttu-id="e8a10-158">패키지를 업로드 하는 중</span><span class="sxs-lookup"><span data-stu-id="e8a10-158">Uploading packages</span></span>

<span data-ttu-id="e8a10-159">직접 업로드 하는 경우 새 패키지에는 [nuget.org 업로드](https://www.nuget.org/packages/manage/upload) 사용자 또는 조직 계정에 패키지 소유자를 할당 페이지:</span><span class="sxs-lookup"><span data-stu-id="e8a10-159">When you directly upload a new package on the [nuget.org Upload](https://www.nuget.org/packages/manage/upload) page, you assign the package owner to a user or organization account :</span></span>

![계정 옵션을 사용 하 여 패키지를 업로드 합니다.](media/org-upload-option.png)

### <a name="using-api-keys"></a><span data-ttu-id="e8a10-161">API 키를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="e8a10-161">Using API keys</span></span>

<span data-ttu-id="e8a10-162">통해 패키지를 푸시하는 `nuget push` 또는 `dotnet nuget push` CLI 명령을 해당 명령을 사용 하 여 필요한 API 키를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8a10-162">To push a package through the `nuget push` or `dotnet nuget push` CLI commands, you must obtain an API key needed by those commands.</span></span> <span data-ttu-id="e8a10-163">자세한 내용은 참조 [패키지 게시](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package)합니다.</span><span class="sxs-lookup"><span data-stu-id="e8a10-163">For details, see [Publish a package](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).</span></span>

<span data-ttu-id="e8a10-164">새 API 키를 만들 때 적절 한 조직에서 선택 된 **패키지 소유자** 드롭 다운 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8a10-164">When creating a new API key, select the appropriate organization in the **Package Owner** drop down.</span></span> <span data-ttu-id="e8a10-165">모든 API 키를 만들면 선택한 조직에만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8a10-165">Any API key you create is applicable only to the chosen organization:</span></span>

![계정 옵션을 사용 하 여 API 키](media/org-apikey-option.png)

## <a name="removing-an-organization"></a><span data-ttu-id="e8a10-167">조직 제거</span><span class="sxs-lookup"><span data-stu-id="e8a10-167">Removing an organization</span></span>

<span data-ttu-id="e8a10-168">사용자를 제거할 수 있습니다 직접 조직에서 선택 하 여는 `X` 조직 구성원에 의해 표시 된 단추:</span><span class="sxs-lookup"><span data-stu-id="e8a10-168">As a user, you can remove yourself from an organization by selecting the `X` button shown by your organization membership:</span></span>

![조직에서 사용자 계정 제거](media/org-remove-self-option.png)

<span data-ttu-id="e8a10-170">관리자는 다른 관리자를 포함 하 여 조직에서 모든 구성원을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8a10-170">Administrators can remove any member from the organization, including other administrators.</span></span> <span data-ttu-id="e8a10-171">조직에 대 한 유일한 관리자 인 경우 관리자 권한으로 다른 멤버를 추가 하지 않으면 사용자가 직접 제거할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e8a10-171">If you're the sole administrator for an organization, you cannot remove yourself unless you add another member as an administrator.</span></span>

### <a name="deleting-an-organization-account"></a><span data-ttu-id="e8a10-172">조직 계정 삭제</span><span class="sxs-lookup"><span data-stu-id="e8a10-172">Deleting an organization account</span></span>

<span data-ttu-id="e8a10-173">이 기능은 곧 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8a10-173">This feature is coming soon.</span></span>
