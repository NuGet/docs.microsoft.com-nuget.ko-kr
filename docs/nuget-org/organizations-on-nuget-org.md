---
title: NuGet.org의 조직
description: NuGet.org의 조직은 그룹 또는 팀, 회사 환경에서 게시된 패키지를 관리하는 데 도움을 줍니다.
author: anangaur
ms.author: anangaur
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: 152de360bfa31a0c8c60fac0b12149748773b13e
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427078"
---
# <a name="your-organization-on-nugetorg"></a><span data-ttu-id="28d24-103">NuGet.org의 조직</span><span class="sxs-lookup"><span data-stu-id="28d24-103">Your organization on NuGet.org</span></span>

<span data-ttu-id="28d24-104">조직은 단일 NuGet.org ID를 사용하여 비즈니스와 오픈 소스 프로젝트가 패키지로 협업할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="28d24-104">Organizations enable businesses and open-source projects to collaborate on packages using a single NuGet.org identity.</span></span> <span data-ttu-id="28d24-105">패키지 소비자의 경우 조직 계정은 NuGet.org의 기존 사용자 계정과 동일하게 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="28d24-105">For a package consumer, an organization account appears same as an existing user account on NuGet.org.</span></span>

## <a name="organization-accounts-vs-individual-accounts"></a><span data-ttu-id="28d24-106">조직 계정 및 개별 계정</span><span class="sxs-lookup"><span data-stu-id="28d24-106">Organization accounts vs. individual accounts</span></span>

<span data-ttu-id="28d24-107">조직 계정은 구성원으로 하나 이상의 개별(사용자) 계정을 가지고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28d24-107">An organization account has one or more individual (user) accounts as its members.</span></span> <span data-ttu-id="28d24-108">이러한 멤버는 소유권에 대한 단일 ID를 유지 관리하면서 패키지 세트를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28d24-108">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

<span data-ttu-id="28d24-109">개별 계정은 NuGet.org에서 사용자의 ID이며, 여러 조직의 멤버가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28d24-109">Your individual account is your identity on NuGet.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="28d24-110">패키지는 개별 계정에 속할 수 있는 것처럼 조직 계정에 속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28d24-110">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="28d24-111">패키지 소비자는 개별 계정 또는 조직 계정 간의 차이를 보지 못합니다. 둘 다 패키지 `owners`로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="28d24-111">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

## <a name="adding-a-new-organization"></a><span data-ttu-id="28d24-112">새 조직 추가</span><span class="sxs-lookup"><span data-stu-id="28d24-112">Adding a new organization</span></span>

<span data-ttu-id="28d24-113">새 조직을 추가하려면 NuGet.org에서 계정을 선택한 다음, **조직 관리...**  메뉴 명령을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="28d24-113">To add a new organization, select your account on NuGet.org, then select the **Manage Organizations...** menu command:</span></span>

![관리자 조직에 대한 NuGet.org의 메뉴 옵션](media/org-manage-option.png)

<span data-ttu-id="28d24-115">다음 페이지에서 **새 조직 추가** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="28d24-115">On the next page, select the **Add new organization** button:</span></span>

![NuGet.org에서 새 조직을 만드는 단추](media/org-add-new-option.png)

<span data-ttu-id="28d24-117">다음 페이지에서 조직 이름과 이메일 주소를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="28d24-117">On the next page, provide the organization name and email address.</span></span> <span data-ttu-id="28d24-118">조직 계정은 사용자 계정과 동일한 네임스페이스를 공유하므로 조직 이름은 기존의 다른 조직 또는 사용자 계정과 달라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28d24-118">Since organization accounts share the same namespace as user accounts, the organization name must be different from any other existing organization or user accounts.</span></span> <span data-ttu-id="28d24-119">또한 이메일 주소는 모든 계정에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28d24-119">The email address must also be unique across all accounts.</span></span>

![NuGet.org에 새 조직 페이지 추가](media/org-add-new-page.png)

<span data-ttu-id="28d24-121">조직 계정이 생성되면 관리자가 되어 조직에 대한 패키지를 제출하고 조직 멤버를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28d24-121">Once the organization account is created, you are the administrator and can submit packages for the organization and add organization members.</span></span>

### <a name="transform-existing-account-to-an-organization"></a><span data-ttu-id="28d24-122">기존 계정을 조직으로 변환</span><span class="sxs-lookup"><span data-stu-id="28d24-122">Transform existing account to an organization</span></span>

> [!Warning]
> <span data-ttu-id="28d24-123">계정 변환은 되돌릴 수 없습니다. 조직을 사용자 계정으로 다시 변환할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="28d24-123">Account conversion is irreversible: you cannot transform an organization back to a user account.</span></span>

<span data-ttu-id="28d24-124">단일 사용자 계정을 사용하여 팀으로 패키지를 관리하고 해당 계정을 조직으로 변환하려는 경우 **조직 관리** 페이지에서 **조직으로 계정 변환**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="28d24-124">If you're managing packages as a team using a single user account and would like to convert that account into an organization, use the **Transform your account to an organization** option on the **Manage Organizations** page:</span></span>

![NuGet.org에서 기존 계정을 조직으로 변환하는 옵션](media/org-transform-option.png)

<span data-ttu-id="28d24-126">다음 페이지에서 조직의 관리자로 할당할 다른 사용자 계정을 지정한 다음, **변환**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="28d24-126">On the next page, specify different user account to assign as the administrator of the organization, then select **Transform**.</span></span>

![사용자 계정을 조직으로 변환하기 위한 정보 입력](media/org-transform-page.png)

## <a name="managing-organization-members"></a><span data-ttu-id="28d24-128">조직 멤버 관리</span><span class="sxs-lookup"><span data-stu-id="28d24-128">Managing organization members</span></span>

<span data-ttu-id="28d24-129">조직 관리자는 각 멤버의 NuGet.org *사용자 계정 이름*을 제공하여 멤버를 추가할 수 있으며, 이메일 주소는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="28d24-129">As the organization administrator, you can add members by providing each member's NuGet.org *user account name*; email addresses cannot be used.</span></span> <span data-ttu-id="28d24-130">그런 다음, 각 멤버를 다음 사용 권한으로 협력자 또는 관리자로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="28d24-130">You then mark each member as a collaborator or administrator with the following permissions:</span></span>

| <span data-ttu-id="28d24-131">사용 권한</span><span class="sxs-lookup"><span data-stu-id="28d24-131">Permission</span></span> | <span data-ttu-id="28d24-132">협력자</span><span class="sxs-lookup"><span data-stu-id="28d24-132">Collaborator</span></span> | <span data-ttu-id="28d24-133">관리자</span><span class="sxs-lookup"><span data-stu-id="28d24-133">Administrator</span></span> |
| --- | --- | --- |
| <span data-ttu-id="28d24-134">조직의 패키지 관리</span><span class="sxs-lookup"><span data-stu-id="28d24-134">Manage the organization's packages</span></span><br/><span data-ttu-id="28d24-135">(새 패키지 제출, 기존 패키지 업데이트 또는 나열 취소)</span><span class="sxs-lookup"><span data-stu-id="28d24-135">(submit new packages, update or unlist existing packages)</span></span> | <span data-ttu-id="28d24-136">yes</span><span class="sxs-lookup"><span data-stu-id="28d24-136">Yes</span></span> | <span data-ttu-id="28d24-137">yes</span><span class="sxs-lookup"><span data-stu-id="28d24-137">Yes</span></span> |
| <span data-ttu-id="28d24-138">조직 메타데이터 변경</span><span class="sxs-lookup"><span data-stu-id="28d24-138">Change organization metadata</span></span><br/><span data-ttu-id="28d24-139">(이메일 주소, 알림 설정)</span><span class="sxs-lookup"><span data-stu-id="28d24-139">(email address, notification settings)</span></span> | <span data-ttu-id="28d24-140">예</span><span class="sxs-lookup"><span data-stu-id="28d24-140">No</span></span> | <span data-ttu-id="28d24-141">yes</span><span class="sxs-lookup"><span data-stu-id="28d24-141">Yes</span></span> |
| <span data-ttu-id="28d24-142">조직 멤버 관리</span><span class="sxs-lookup"><span data-stu-id="28d24-142">Manage organization members</span></span> | <span data-ttu-id="28d24-143">예</span><span class="sxs-lookup"><span data-stu-id="28d24-143">No</span></span> | <span data-ttu-id="28d24-144">yes</span><span class="sxs-lookup"><span data-stu-id="28d24-144">Yes</span></span> |
| <span data-ttu-id="28d24-145">조직 패키지에 대한 공동 소유권 요청 또는 작업</span><span class="sxs-lookup"><span data-stu-id="28d24-145">Request or act on co-ownership requests for organization packages</span></span> | <span data-ttu-id="28d24-146">예</span><span class="sxs-lookup"><span data-stu-id="28d24-146">No</span></span> | <span data-ttu-id="28d24-147">yes</span><span class="sxs-lookup"><span data-stu-id="28d24-147">Yes</span></span> |

## <a name="managing-packages"></a><span data-ttu-id="28d24-148">패키지 관리</span><span class="sxs-lookup"><span data-stu-id="28d24-148">Managing packages</span></span>

<span data-ttu-id="28d24-149">[패키지 관리](https://www.nuget.org/account/Packages) 페이지의 멤버로서 계정과 모든 조직의 모든 패키지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28d24-149">You can view all the packages across your account and all organizations of which you're a member on the [Manage Packages](https://www.nuget.org/account/Packages) page.</span></span> <span data-ttu-id="28d24-150">계정 또는 특정 조직별 패키지를 보려면 페이지 오른쪽 위에 있는 계정 필터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="28d24-150">To view the packages specific to your account or any specific organization, use the accounts filter on the top right of the page.</span></span>

![계정 필터를 사용하여 패키지를 관리](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a><span data-ttu-id="28d24-152">조직에 패키지 전송</span><span class="sxs-lookup"><span data-stu-id="28d24-152">Transferring packages to an organization</span></span>
<span data-ttu-id="28d24-153">일부 패키지를 새로 만든 조직으로 전송하려는 경우 조직 계정에 패키지를 공동 소유하도록 요청한 다음, 소유자에서 자신을 제거하여 패키지를 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28d24-153">If you wish to transfer some of your packages to a newly created organization, you can do so by requesting the organization account to co-own the package and then removing yourself as the owner.</span></span> <span data-ttu-id="28d24-154">조직의 관리자인 경우 소유권을 허용하는 데 필요한 확인이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="28d24-154">If you are an administrator of the organization, there is no confirmation required to accept the ownership.</span></span> <span data-ttu-id="28d24-155">그러나 협력자인 경우 조직을 소유자로 추가하려면 소유권을 허용할 관리자 중 한 명이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="28d24-155">However, if you are a collaborator, adding the organization as an owner requires one of the administrators to accept the ownership.</span></span>

## <a name="publishing-packages"></a><span data-ttu-id="28d24-156">패키지 게시</span><span class="sxs-lookup"><span data-stu-id="28d24-156">Publishing packages</span></span>

<span data-ttu-id="28d24-157">패키지를 NuGet.org에 직접 업로드하거나 `nuget push` 또는 `dotnet nuget push` CLI 명령을 통해 패키지를 푸시하여 사용자 계정에 패키지를 게시하는 등의 방법으로 패키지를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="28d24-157">You publish packages to an organization like you publish packages to a user account: by directly uploading the package to NuGet.org or by pushing the package through the `nuget push` or `dotnet nuget push` CLI commands.</span></span>

### <a name="uploading-packages"></a><span data-ttu-id="28d24-158">패키지 업로드</span><span class="sxs-lookup"><span data-stu-id="28d24-158">Uploading packages</span></span>

<span data-ttu-id="28d24-159">[NuGet.org 업로드](https://www.nuget.org/packages/manage/upload) 페이지에 새 패키지를 직접 업로드할 때 패키지 소유자를 사용자 또는 조직 계정에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="28d24-159">When you directly upload a new package on the [NuGet.org Upload](https://www.nuget.org/packages/manage/upload) page, you assign the package owner to a user or organization account :</span></span>

![계정 옵션을 사용하여 패키지 업로드](media/org-upload-option.png)

### <a name="using-api-keys"></a><span data-ttu-id="28d24-161">API 키 사용</span><span class="sxs-lookup"><span data-stu-id="28d24-161">Using API keys</span></span>

<span data-ttu-id="28d24-162">`nuget push` 또는 `dotnet nuget push` CLI 명령을 통해 패키지를 푸시하려면 해당 명령에 필요한 API 키를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28d24-162">To push a package through the `nuget push` or `dotnet nuget push` CLI commands, you must obtain an API key needed by those commands.</span></span> <span data-ttu-id="28d24-163">자세한 내용은 [패키지 게시](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="28d24-163">For details, see [Publish a package](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).</span></span>

<span data-ttu-id="28d24-164">새 API 키를 만들 때 **패키지 소유자** 드롭다운에서 적절한 조직을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="28d24-164">When creating a new API key, select the appropriate organization in the **Package Owner** drop down.</span></span> <span data-ttu-id="28d24-165">생성한 모든 API 키는 선택한 조직에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="28d24-165">Any API key you create is applicable only to the chosen organization:</span></span>

![계정 옵션이 있는 API 키](media/org-apikey-option.png)

## <a name="removing-an-organization"></a><span data-ttu-id="28d24-167">조직 제거</span><span class="sxs-lookup"><span data-stu-id="28d24-167">Removing an organization</span></span>

<span data-ttu-id="28d24-168">사용자는 조직 멤버 자격에 표시된 **X** 단추를 선택하여 조직에서 자신을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28d24-168">As a user, you can remove yourself from an organization by selecting the **X** button shown by your organization membership:</span></span>

![조직에서 사용자 계정 제거](media/org-remove-self-option.png)

<span data-ttu-id="28d24-170">관리자는 다른 관리자를 비롯하여 조직에서 모든 멤버를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28d24-170">Administrators can remove any member from the organization, including other administrators.</span></span> <span data-ttu-id="28d24-171">조직의 유일한 관리자인 경우 다른 멤버를 관리자로 추가하지 않는 한 자신을 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="28d24-171">If you're the sole administrator for an organization, you cannot remove yourself unless you add another member as an administrator.</span></span>

### <a name="deleting-an-organization-account"></a><span data-ttu-id="28d24-172">조직 계정 삭제</span><span class="sxs-lookup"><span data-stu-id="28d24-172">Deleting an organization account</span></span>

<span data-ttu-id="28d24-173">조직 페이지에 표시된 **삭제** 단추를 클릭하여 조직 계정을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28d24-173">You can delete an organization account by clicking the **Delete** button shown in your organization page.</span></span>

![조직 삭제](media/org-delete-option.png)

<span data-ttu-id="28d24-175">조직을 삭제하려면 **조직 삭제** 확인 단추를 클릭하여 조직 삭제를 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28d24-175">To delete the organizaiton, you must confirm it by clicking the **Delete organization** confirmation button.</span></span>
