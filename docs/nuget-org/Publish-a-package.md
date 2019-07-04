---
title: NuGet 패키지를 게시하는 방법
description: NuGet 패키지를 nuget.org 또는 개인 피드에 게시하는 방법 및 nuget.org에서 패키지 소유권을 관리하는 방법에 대한 자세한 지침입니다.
author: karann-msft
ms.author: karann
ms.date: 05/18/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 6d183100a8319b517347567f34d276e94eb4e15d
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427188"
---
# <a name="publishing-packages"></a><span data-ttu-id="4142d-103">패키지 게시</span><span class="sxs-lookup"><span data-stu-id="4142d-103">Publishing packages</span></span>

<span data-ttu-id="4142d-104">패키지를 만들고 `.nupkg` 파일이 준비되면 공용 또는 개인용으로 다른 개발자가 사용할 수 있도록 하는 간단한 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="4142d-104">Once you have created a package and have your `.nupkg` file in hand, it's a simple process to make it available to other developers, either publicly or privately:</span></span>

- <span data-ttu-id="4142d-105">공용 패키지는 이 문서에 설명된 대로 모든 개발자가 [nuget.org](https://www.nuget.org/packages/manage/upload)를 통해 전역적으로 사용할 수 있습니다(NuGet 4.1.0 이상 필요).</span><span class="sxs-lookup"><span data-stu-id="4142d-105">Public packages are made available to all developers globally through [nuget.org](https://www.nuget.org/packages/manage/upload) as described in this article (requires NuGet 4.1.0+).</span></span>
- <span data-ttu-id="4142d-106">개인 패키지는 파일 공유, 개인 NuGet 서버, [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish) 또는 타사 리포지토리(myget, ProGet, Nexus Repository 및 Artifactory)를 호스트하여 팀 또는 조직에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4142d-106">Private packages are available to only a team or organization, by hosting them either a file share, a private NuGet server, [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish), or a third-party repository such as myget, ProGet, Nexus Repository, and Artifactory.</span></span> <span data-ttu-id="4142d-107">자세한 내용은 [패키지 개요 호스트](../hosting-packages/overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4142d-107">For additional details, see [Hosting Packages Overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="4142d-108">이 문서에서는 nuget.org에 대한 게시를 다룹니다. Azure Artifacts에 게시하는 방법은 [패키지 관리](https://www.visualstudio.com/docs/package/nuget/publish)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4142d-108">This article covers publishing to nuget.org; for publishing to Azure Artifacts, see [Package Management](https://www.visualstudio.com/docs/package/nuget/publish).</span></span>

## <a name="publish-to-nugetorg"></a><span data-ttu-id="4142d-109">nuget.org에 게시</span><span class="sxs-lookup"><span data-stu-id="4142d-109">Publish to nuget.org</span></span>

<span data-ttu-id="4142d-110">nuget.org의 경우 계정을 Microsoft 계정으로 로그인해야 하며, 이 경우 nuget.org에 계정을 등록하라는 메시지가 표시됩니다. 이전 버전의 포털을 사용하여 만든 nuget.org 계정으로 로그인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4142d-110">For nuget.org, you must sign in with a Microsoft account, with which you'll be asked to register the account with nuget.org. You can also sign in with a nuget.org account created using older versions of the portal.</span></span>

![NuGet 로그인 위치](media/publish_NuGetSignIn.png)

<span data-ttu-id="4142d-112">다음으로, 다음 섹션에 설명된 대로 nuget.org 웹 포털을 통해 패키지를 업로드하거나, 명령줄(`nuget.exe` 4.1.0 이상 필요)에서 nuget.org에 푸시하거나, Azure DevOps Services를 통해 CI/CD 프로세스의 일부로 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4142d-112">Next, you can either upload the package through the nuget.org web portal, push to nuget.org from the command line (requires `nuget.exe` 4.1.0+) , or publish as part of a CI/CD process through Azure DevOps Services, as described in the following sections.</span></span>

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a><span data-ttu-id="4142d-113">웹 포털: nuget.org에 패키지 업로드 탭 사용</span><span class="sxs-lookup"><span data-stu-id="4142d-113">Web portal: use the Upload Package tab on nuget.org</span></span>

1. <span data-ttu-id="4142d-114">nuget.org의 상단 메뉴에서 **업로드**를 선택하고 패키지 위치를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="4142d-114">Select **Upload** on the top menu of nuget.org and browse to the package location.</span></span>

    ![nuget.org에 패키지 업로드](media/publish_UploadYourPackage.PNG)

1. <span data-ttu-id="4142d-116">nuget.org는 패키지 이름을 사용할 수 있는 경우 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4142d-116">nuget.org tells you if the package name is available.</span></span> <span data-ttu-id="4142d-117">그렇지 않으면 프로젝트에서 패키지 식별자를 변경하고 다시 빌드한 다음, 업로드를 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="4142d-117">If it isn't, change the package identifier in your project, rebuild, and try the upload again.</span></span>

1. <span data-ttu-id="4142d-118">패키지 이름을 사용할 수 있는 경우 nuget.org는 패키지 매니페스트에서 메타데이터를 검토할 수 있는 **확인** 섹션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4142d-118">If the package name is available, nuget.org opens a **Verify** section in which you can review the metadata from the package manifest.</span></span> <span data-ttu-id="4142d-119">메타데이터를 변경하려면 프로젝트(프로젝트 파일 또는 `.nuspec` 파일)을 편집하고, 다시 빌드하고, 패키지를 다시 만들고, 다시 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="4142d-119">To change any of the metadata, edit your project (project file or `.nuspec` file), rebuild, recreate the package, and upload again.</span></span>

1. <span data-ttu-id="4142d-120">**설명서 가져오기**에서 Markdown을 붙여넣거나, URL로 문서를 가리키거나, 설명서 파일을 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4142d-120">Under **Import Documentation** you can paste Markdown, point to your docs with a URL, or upload a documentation file.</span></span>

1. <span data-ttu-id="4142d-121">모든 정보가 준비되면 **제출** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4142d-121">When all the information is ready, select the **Submit** button</span></span>

### <a name="command-line"></a><span data-ttu-id="4142d-122">명령줄</span><span class="sxs-lookup"><span data-stu-id="4142d-122">Command line</span></span>

<span data-ttu-id="4142d-123">nuget.org에 패키지를 푸시하려면 [nuget.exe v4.1.0 이상](https://www.nuget.org/downloads)을 사용해야 합니다. 여기서는 필수 [NuGet 프로토콜](../api/nuget-protocols.md)을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="4142d-123">To push packages to nuget.org you must use [nuget.exe v4.1.0 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span> <span data-ttu-id="4142d-124">nuget.org에서 만든 API 키도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4142d-124">You also need an API key, which is created on nuget.org.</span></span>

#### <a name="create-api-keys"></a><span data-ttu-id="4142d-125">API 키 만들기</span><span class="sxs-lookup"><span data-stu-id="4142d-125">Create API keys</span></span>

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

#### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="4142d-126">dotnet nuget push로 게시</span><span class="sxs-lookup"><span data-stu-id="4142d-126">Publish with dotnet nuget push</span></span>

[!INCLUDE [publish-dotnet](../quickstart/includes/publish-dotnet.md)]

#### <a name="publish-with-nuget-push"></a><span data-ttu-id="4142d-127">nuget push로 게시</span><span class="sxs-lookup"><span data-stu-id="4142d-127">Publish with nuget push</span></span>

1. <span data-ttu-id="4142d-128">명령 프롬프트에서 다음 명령을 실행합니다. 이때 `<your_API_key>`는 nuget.org에서 가져온 키로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4142d-128">At a command prompt, run the following command, replacing `<your_API_key>` with the key obtained from nuget.org:</span></span>

    ```cli
    nuget setApiKey <your_API_key>
    ```

    <span data-ttu-id="4142d-129">이 명령은 NuGet 구성에 API 키를 저장하므로 동일한 컴퓨터에서 이 단계를 다시 반복해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4142d-129">This command stores your API key in your NuGet configuration so that you need repeat this step again on the same computer.</span></span>

1. <span data-ttu-id="4142d-130">다음 명령을 사용하여 NuGet 갤러리에 패키지를 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="4142d-130">Push your package to NuGet Gallery using the following command:</span></span>

    ```cli
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

#### <a name="publish-signed-packages"></a><span data-ttu-id="4142d-131">서명된 패키지 게시</span><span class="sxs-lookup"><span data-stu-id="4142d-131">Publish signed packages</span></span>

<span data-ttu-id="4142d-132">서명된 패키지를 제출하려면 먼저 패키지 서명에 사용된 [인증서를 등록](../create-packages/Sign-a-Package.md#register-the-certificate-on-nugetorg)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4142d-132">To submit signed packages, you must first [register the certificate](../create-packages/Sign-a-Package.md#register-the-certificate-on-nugetorg) used for signing the packages.</span></span> 

> [!Warning]
> <span data-ttu-id="4142d-133">nuget.org는 [서명된 패키지 요구 사항](../reference/Signed-Packages-Reference.md#signature-requirements-on-nugetorg)을 충족하지 않는 패키지를 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="4142d-133">nuget.org rejects packages that don't satisfy the [signed package requirements](../reference/Signed-Packages-Reference.md#signature-requirements-on-nugetorg).</span></span>

### <a name="package-validation-and-indexing"></a><span data-ttu-id="4142d-134">패키지 유효성 검사 및 인덱싱</span><span class="sxs-lookup"><span data-stu-id="4142d-134">Package validation and indexing</span></span>

<span data-ttu-id="4142d-135">nuget.org에 푸시된 패키지는 바이러스 검사와 같은 여러 유효성 검사를 거칩니다.</span><span class="sxs-lookup"><span data-stu-id="4142d-135">Packages pushed to nuget.org undergo several validations, such as virus checks.</span></span> <span data-ttu-id="4142d-136">(nuget.org의 모든 패키지는 정기적으로 검사됩니다.)</span><span class="sxs-lookup"><span data-stu-id="4142d-136">(All packages on nuget.org are periodically scanned.)</span></span>

<span data-ttu-id="4142d-137">패키지가 모든 유효성 검사를 통과하면 인덱싱되는 동안 시간이 걸릴 수 있으며 검색 결과에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4142d-137">When the package has passed all validation checks, it might take a while for it to be indexed and appear in search results.</span></span> <span data-ttu-id="4142d-138">인덱싱이 완료되면 패키지를 성공적으로 게시했는지 확인하는 전자 메일을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4142d-138">Once indexing is complete, you receive an email confirming that the package was successfully published.</span></span> <span data-ttu-id="4142d-139">패키지가 유효성 검사에 실패하면 패키지 세부 정보 페이지는 관련 오류를 표시하도록 업데이트되고 이를 알리는 전자 메일을 받을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4142d-139">If the package fails a validation check, the package details page will update to display the associated error and you also receive an email notifying you about it.</span></span>

<span data-ttu-id="4142d-140">패키지 유효성 검사 및 인덱싱은 일반적으로 15분이 걸리지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4142d-140">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="4142d-141">패키지 게시가 예상보다 오래 걸리면 [status.nuget.org](https://status.nuget.org/)를 방문하여 nuget.org에 중단이 발생했는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4142d-141">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if nuget.org is experiencing any interruptions.</span></span> <span data-ttu-id="4142d-142">모든 시스템이 모두 제대로 작동하고 패키지가 1시간 내에 성공적으로 게시되지 않은 경우 nuget.org에 로그인하고 패키지 페이지에서 지원 문의 링크를 사용하여 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="4142d-142">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package page.</span></span>

<span data-ttu-id="4142d-143">패키지 상태를 보려면 nuget.org의 계정 이름 아래에서 **패키지 관리**를 선택합니다. 유효성 검사가 완료되면 확인 전자 메일을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4142d-143">To see the status of a package, select **Manage packages** under your account name on nuget.org. You receive a confirmation email when validation is complete.</span></span>

<span data-ttu-id="4142d-144">패키지를 인덱싱하고 다른 사용자가 찾을 수 있는 검색 결과에 표시하는 데 시간이 걸릴 수 있습니다. 이 시간 동안 패키지 페이지에 다음과 같은 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4142d-144">Note that it might take a while for your package to be indexed and appear in search results where others can find it, during which time you see the following message on your package page:</span></span>

![패키지가 아직 게시되지 않았다는 메시지](media/publish_NotYetIndexed.png)

### <a name="azure-devops-services-cicd"></a><span data-ttu-id="4142d-146">Azure DevOps Services(CI/CD)</span><span class="sxs-lookup"><span data-stu-id="4142d-146">Azure DevOps Services (CI/CD)</span></span>

<span data-ttu-id="4142d-147">지속적인 통합 및 배포 프로세스의 일부로 Azure DevOps를 사용하여 nuget.org에 패키지를 푸시하는 경우 NuGet 작업에서 `nuget.exe` 4.1 이상을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4142d-147">If you push packages to nuget.org using Azure DevOps Services as part of your Continuous Integration/Deployment process, you must use `nuget.exe` 4.1 or above in the NuGet tasks.</span></span> <span data-ttu-id="4142d-148">자세한 내용은 [빌드에서 최신 NuGet을 사용하는 방법](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/)(Microsoft DevOps 블로그)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4142d-148">Details can be found on [Using the latest NuGet in your build](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Microsoft DevOps blog).</span></span>

## <a name="managing-package-owners-on-nugetorg"></a><span data-ttu-id="4142d-149">nuget.org에서 패키지 소유자 관리</span><span class="sxs-lookup"><span data-stu-id="4142d-149">Managing package owners on nuget.org</span></span>

<span data-ttu-id="4142d-150">각 NuGet 패키지의 `.nuspec` 파일이 패키지의 작성자를 정의하지만 nuget.org 갤러리는 소유권을 정의하는 데 해당 메타데이터를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4142d-150">Although each NuGet package's `.nuspec` file defines the package's authors, the nuget.org gallery does not use that metadata to define ownership.</span></span> <span data-ttu-id="4142d-151">대신 nuget.org는 패키지를 게시하는 사용자에게 초기 소유권을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="4142d-151">Instead, nuget.org assigns initial ownership to the person who publishes the package.</span></span> <span data-ttu-id="4142d-152">nuget.org UI 통해 패키지를 업로드한 로그인 사용자 또는 `nuget SetApiKey`이나 `nuget push`에서 해당 API 키를 사용한 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="4142d-152">This is either the logged-in user who uploaded the package through the nuget.org UI, or the users whose API key was used with `nuget SetApiKey` or `nuget push`.</span></span>

<span data-ttu-id="4142d-153">모든 패키지 소유자는 다른 소유자 추가와 제거 및 업데이트 게시를 포함하여 패키지에 대한 모든 권한을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="4142d-153">All package owners have full permissions for the package, including adding and removing other owners, and publishing updates.</span></span>

<span data-ttu-id="4142d-154">패키지의 소유권을 변경하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4142d-154">To change ownership of a package, do the following:</span></span>

1. <span data-ttu-id="4142d-155">패키지의 현재 소유자인 계정을 사용하여 nuget.org에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="4142d-155">Sign in to nuget.org with the account that is the current owner of the package.</span></span>
1. <span data-ttu-id="4142d-156">계정 이름을 선택하고 **패키지 관리**를 선택한 후 **게시된 패키지**를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="4142d-156">Select your account name, select **Manage packages**, and expand **Published Packages**.</span></span>
1. <span data-ttu-id="4142d-157">관리할 패키지를 선택한 다음, 오른쪽에서 **소유자 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4142d-157">Select on the package you want to manage, then on the right side select **Manage owners**.</span></span>

<span data-ttu-id="4142d-158">여기부터 다음과 같은 몇 가지 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4142d-158">From here you have several options:</span></span>

1. <span data-ttu-id="4142d-159">**현재 소유자** 아래에 나열된 모든 소유자를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="4142d-159">Remove any owner listed under **Current Owners**.</span></span>
1. <span data-ttu-id="4142d-160">사용자 이름, 메시지를 입력하고 **추가**를 선택하여 **소유자 추가** 아래에 소유자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4142d-160">Add an owner under **Add Owner** by entering their user name, a message, and selecting **Add**.</span></span> <span data-ttu-id="4142d-161">그러면 새로운 공동 소유자에게 확인 링크를 포함한 전자 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="4142d-161">This action sends an email to that new co-owner with a confirmation link.</span></span> <span data-ttu-id="4142d-162">확인하면 해당 사용자에게는 소유자를 추가하고 제거하는 모든 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4142d-162">Once confirmed, that person has full permissions to add and remove owners.</span></span> <span data-ttu-id="4142d-163">(확인될 때까지 **현재 소유자** 섹션에서는 해당 사용자가 승인 보류 중으로 표시됩니다.)</span><span class="sxs-lookup"><span data-stu-id="4142d-163">(Until confirmed, the **Current Owners** section indicates pending approval for that person.)</span></span>
1. <span data-ttu-id="4142d-164">소유권을 이전하려면(잘못된 계정에서 소유권이 변경되거나 패키지가 게시될 경우) 새 소유자를 추가합니다. 소유권을 확인하면 목록에서 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4142d-164">To transfer ownership (as when ownership changes or a package was published under the wrong account), add the new owner, and once they've confirmed ownership they can remove you from the list.</span></span>

<span data-ttu-id="4142d-165">회사 또는 그룹에 소유권을 할당하려면 적절한 팀 멤버에 전달되는 전자 메일 별칭을 사용하여 nuget.org 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4142d-165">To assign ownership to a company or group, create a nuget.org account using an email alias that is forwarded to the appropriate team members.</span></span> <span data-ttu-id="4142d-166">예를 들어 다양한 Microsoft ASP.NET 패키지는 단순히 해당 별칭인 [microsoft](http://nuget.org/profiles/microsoft) 및 [aspnet](http://nuget.org/profiles/aspnet) 계정에서 공동 소유합니다.</span><span class="sxs-lookup"><span data-stu-id="4142d-166">For example, various Microsoft ASP.NET packages are co-owned by the [microsoft](http://nuget.org/profiles/microsoft) and [aspnet](http://nuget.org/profiles/aspnet) accounts, which simply such aliases.</span></span>

### <a name="recovering-package-ownership"></a><span data-ttu-id="4142d-167">패키지 소유권 복구</span><span class="sxs-lookup"><span data-stu-id="4142d-167">Recovering package ownership</span></span>

<span data-ttu-id="4142d-168">경우에 따라 패키지에는 활성 소유자가 없을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4142d-168">Occasionally, a package may not have an active owner.</span></span> <span data-ttu-id="4142d-169">예를 들어 원래 소유자는 회사가 패키지를 생성하거나, nuget.org 자격 증명을 손실하거나, 갤러리의 이전 버그 패키지를 소유하지 않도록 둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4142d-169">For example, the original owner may have left the company that produces the package, nuget.org credentials are lost, or earlier bugs in the gallery left a package ownerless.</span></span>

<span data-ttu-id="4142d-170">사용자가 패키지의 정당한 소유자이고 소유권을 다시 가져와야 하는 경우 nuget.org에서 [연락처 양식](https://www.nuget.org/policies/Contact)을 사용하여 NuGet 팀에 상황을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4142d-170">If you are the rightful owner of a package and need to regain ownership, use the [contact form](https://www.nuget.org/policies/Contact) on nuget.org to explain your situation to the NuGet team.</span></span> <span data-ttu-id="4142d-171">그런 다음 패키지의 프로젝트 URL, Twitter, 전자 메일 또는 다른 수단을 통해 기존 소유자를 찾는 작업을 포함하여 패키지의 소유권을 확인하는 프로세스를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="4142d-171">We then follow a process to verify your ownership of the package, including trying to locate the existing owner through the package's Project URL, Twitter, email, or other means.</span></span> <span data-ttu-id="4142d-172">하지만 모든 작업에 실패하면 소유자가 되도록 새로운 초대장을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4142d-172">But if all else fails, we can send you a new invite to become an owner.</span></span>
