---
title: "NuGet 패키지 만들기 및 게시를 위한 입문서 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/3/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 91781ed6-da5c-49f0-b973-16dd8ad84229
description: "nuget.exe 명령줄 인터페이스와 Visual Studio를 모두 사용하여 NuGet 패키지를 만들고 게시하기 위한 연습 자습서입니다."
keywords: "NuGet 패키지 만들기, NuGet 패키지 게시, NuGet 자습서"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 36a7c2b1d056dddf07a59737de1c3e94294689ac
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="create-and-publish-a-package"></a><span data-ttu-id="f85d3-104">패키지 만들기 및 게시</span><span class="sxs-lookup"><span data-stu-id="f85d3-104">Create and publish a package</span></span>

<span data-ttu-id="f85d3-105">.NET 클래스 라이브러리에서 NuGet 패키지를 만들고 nuget.org에 게시하는 간단한 과정입니다. 다음 단계는 NuGet CLI(명령줄 인터페이스) 및 Visual Studio를 사용하는 프로세스를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="f85d3-105">It's a simple process to create a NuGet package from a .NET Class Library and publish it to nuget.org. The following steps walk you through the process using the NuGet command-line interface (CLI) and Visual Studio:</span></span>

- [<span data-ttu-id="f85d3-106">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="f85d3-106">Pre-requisites</span></span>](#install-pre-requisites)
- [<span data-ttu-id="f85d3-107">.nuspec 패키지 매니페스트 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="f85d3-107">Create the .nuspec package manifest file</span></span>](#create-the-nuspec-package-manifest-file)
- [<span data-ttu-id="f85d3-108">pack 명령 실행</span><span class="sxs-lookup"><span data-stu-id="f85d3-108">Run the pack command</span></span>](#run-the-pack-command)
- [<span data-ttu-id="f85d3-109">패키지 게시</span><span class="sxs-lookup"><span data-stu-id="f85d3-109">Publish the package</span></span>](#publish-the-package)

## <a name="pre-requisites"></a><span data-ttu-id="f85d3-110">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="f85d3-110">Pre-requisites</span></span>

1. <span data-ttu-id="f85d3-111">[visualstudio.com](https://www.visualstudio.com/)에서 모든 버전의 Visual Studio 2017을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f85d3-111">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/).</span></span>

1. <span data-ttu-id="f85d3-112">[nuget.org/downloads](https://nuget.org/downloads)에서 최신 버전의 `nuget.exe`를 다운로드하고 PATH에 있는 위치에 `.exe`를 저장하여 `nuget.exe` NuGet CLI 도구를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f85d3-112">Install the NuGet CLI tool, `nuget.exe`, by downloading the latest version of `nuget.exe` from [nuget.org/downloads](https://nuget.org/downloads), and saving the `.exe` to a location in your PATH.</span></span> <span data-ttu-id="f85d3-113">다운로드는 설치 관리자가 아니라 *도구 자체입니다*.</span><span class="sxs-lookup"><span data-stu-id="f85d3-113">Note that the download *is* the tool itself, not an installer.</span></span>

1. <span data-ttu-id="f85d3-114">패키지하려는 코드에 적합한 .NET 클래스 라이브러리 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f85d3-114">Create a suitable .NET Class Library project for the code you want to package.</span></span> <span data-ttu-id="f85d3-115">아직 프로젝트가 없는 경우 다음과 같이 간단한 프로젝트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f85d3-115">If you don't already have a project, you can create a simple one as follows:</span></span>
    1. <span data-ttu-id="f85d3-116">Visual Studio에서 **파일 > 새로 만들기 > 프로젝트**를 차례로 선택하고, **Visual C# > Windows** 노드를 펼치고, "클래스 라이브러리" 템플릿을 선택하고, 프로젝트 이름을 AppLogger로 지정한 다음, **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f85d3-116">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > Windows** node, select the "Class Library" template, name the project AppLogger, and click **OK**.</span></span>
    1. <span data-ttu-id="f85d3-117">결과 프로젝트 파일을 마우스 오른쪽 단추로 클릭하고, **빌드**를 선택하여 프로젝트가 제대로 만들어졌는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f85d3-117">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="f85d3-118">DLL은 Debug(또는 해당 구성을 대신 빌드하는 경우 Release) 폴더 내에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f85d3-118">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

    <span data-ttu-id="f85d3-119">물론 실제 NuGet 패키지 내에서 다른 사람들이 응용 프로그램을 빌드할 수 있는 많은 유용한 기능을 구현할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f85d3-119">Within a real NuGet package, of course, you'll implement many useful features upon which others can build applications.</span></span> <span data-ttu-id="f85d3-120">그러나 이 연습에서는 템플릿의 클래스 라이브러리가 패키지를 만드는 데 충분하므로 추가 코드를 작성하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f85d3-120">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span>

## <a name="create-the-nuspec-package-manifest-file"></a><span data-ttu-id="f85d3-121">.nuspec 패키지 매니페스트 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="f85d3-121">Create the .nuspec package manifest file</span></span>

<span data-ttu-id="f85d3-122">모든 NuGet 패키지에는 내용과 종속성을 설명하는 매니페스트(`.nuspec` 파일)가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f85d3-122">Every NuGet package needs a manifest&mdash;a `.nuspec` file&mdash;to describe its contents and its dependencies.</span></span> <span data-ttu-id="f85d3-123">`nuget spec` 명령은 이 파일을 만든 다음 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f85d3-123">The `nuget spec` command creates this file for you, which you then customize.</span></span> <span data-ttu-id="f85d3-124">다음 예제에서는 프로젝트 파일에서 `.nuspec`을 만듭니다. 또한 [패키지 만들기](../create-packages/creating-a-package.md)에서 설명한 대로 다른 방법을 통해 매니페스트를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f85d3-124">In this example you create the `.nuspec` from a project file; you can also create the manifest through other means as described on [Create a Package](../create-packages/creating-a-package.md).</span></span>

1. <span data-ttu-id="f85d3-125">명령 프롬프트를 열고 프로젝트 파일(`.csproj`)이 있는 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f85d3-125">Open a command prompt and navigate to the folder containing your project file (`.csproj`).</span></span>

1. <span data-ttu-id="f85d3-126">`spec` NuGet CLI 명령을 실행하여 `AppLogger.nuspec`과 같이 프로젝트의 이름을 붙인 매니페스트를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="f85d3-126">Run the NuGet CLI `spec` command to generate the manifest, which is named after your project, such as `AppLogger.nuspec`:</span></span>

    ```
    nuget spec
    ```

1. <span data-ttu-id="f85d3-127">텍스트 편집기에서 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f85d3-127">Open the file in a text editor.</span></span> <span data-ttu-id="f85d3-128">매니페스트는 패키징 프로세스 중에 *$`<token>`$* 형식의 토큰이 프로젝트의 Properties/AssemblyInfo.cs 파일의 값으로 대체되는 아래 코드와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="f85d3-128">The manifest looks something like the code below, where tokens in the form *$`<token>`$* are be replaced during the packaging process with values from the project's Properties/AssemblyInfo.cs file.</span></span> <span data-ttu-id="f85d3-129">토큰에 대한 자세한 내용은 [.nuspec 파일 만들기](../create-packages/creating-a-package.md#creating-the-nuspec-file)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f85d3-129">For more details on tokens, see [Creating a .nuspec file](../create-packages/creating-a-package.md#creating-the-nuspec-file).</span></span>

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>
        <id>$id$</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>$author$</authors>
        <owners>$author$</owners>
        <licenseUrl>http://LICENSE_URL_HERE_OR_DELETE_THIS_LINE</licenseUrl>
        <projectUrl>http://PROJECT_URL_HERE_OR_DELETE_THIS_LINE</projectUrl>
        <iconUrl>http://ICON_URL_HERE_OR_DELETE_THIS_LINE</iconUrl>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>$description$</description>
        <releaseNotes>Summary of changes made in this release of the package.</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>Tag1 Tag2</tags>
        </metadata>
    </package>
    ```

1. <span data-ttu-id="f85d3-130">nuget.org에서 고유한 패키지 ID를 선택합니다. [패키지 만들기](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)에서 설명한 명명 규칙을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f85d3-130">Select a package ID that is unique across nuget.org. We recommend using the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="f85d3-131">작성자 및 설명 태그를 업데이트해야 합니다. 그렇지 않으면 다음 단계에서 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="f85d3-131">Be sure to update the author and description tags or you get an error in the next step.</span></span> <span data-ttu-id="f85d3-132">다음은 업데이트된 `.nuspec` 파일의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="f85d3-132">Here's an updated `.nuspec` file as an example:</span></span>

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>
        <id>MyCompanyName.MyProductName.MyPackageName</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>kraigb</authors>
        <owners>kraigb</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>application app logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Note]
> <span data-ttu-id="f85d3-133">공용으로 빌드된 패키지의 경우 `<tags>` 요소에 특히 주의하세요. 이러한 태그는 다른 사람들이 패키지를 찾고 그 기능을 이해하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f85d3-133">For packages built for public consumption, pay special attention to the `<tags>` element, as these tags help others find your package and understand what it does.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="f85d3-134">pack 명령 실행</span><span class="sxs-lookup"><span data-stu-id="f85d3-134">Run the pack command</span></span>

<span data-ttu-id="f85d3-135">프로젝트에서 NuGet 패키지(`.nupkg` 파일)를 빌드하려면 `pack` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f85d3-135">To build a NuGet package (a `.nupkg` file) from a project, run the `pack` command:</span></span>

```
nuget pack AppLogger.csproj
```

<span data-ttu-id="f85d3-136">이 명령은 `.nuspec` 파일의 패키지 이름과 버전 번호를 사용하여 `AppLogger.1.0.0.0.nupkg`를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f85d3-136">This command creates `AppLogger.1.0.0.0.nupkg` using the package name and version number from the `.nuspec` file.</span></span> <span data-ttu-id="f85d3-137">`.nuspec` 파일의 다양한 필드를 기본값에서 업데이트하지 않으면 명령에서 경고를 발생시킵니다.</span><span class="sxs-lookup"><span data-stu-id="f85d3-137">The command issues warnings if you haven't updated various fields in the `.nuspec` file from their default values.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="f85d3-138">패키지 게시</span><span class="sxs-lookup"><span data-stu-id="f85d3-138">Publish the package</span></span>

<span data-ttu-id="f85d3-139">`.nupkg` 파일이 있으면 `push` 명령을 사용하여 nuget.org에 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="f85d3-139">Once you have a `.nupkg` file, you publish it to nuget.org using the `push` command.</span></span> <span data-ttu-id="f85d3-140">또는 [nuget.org 게시 워크플로](../create-packages/publish-a-package.md#publish-to-nugetorg)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f85d3-140">(Alternately, you can use the [nuget.org publishing workflow](../create-packages/publish-a-package.md#publish-to-nugetorg).</span></span>

> [!Warning]
> <span data-ttu-id="f85d3-141">nuget.org에 게시한 패키지는 다른 개발자에게 공개적으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f85d3-141">The packages you publish to nuget.org are publicly visible to other developers.</span></span> <span data-ttu-id="f85d3-142">패키지를 개인적으로 호스팅하려면 [패키지 호스팅](../hosting-packages/overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f85d3-142">To host packages privately, see [Hosting packages](../hosting-packages/overview.md).</span></span>


1. <span data-ttu-id="f85d3-143">[nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F)에 체험 계정을 만듭니다. 해당 계정이 이미 있으면 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f85d3-143">Create a free account on [nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), or log in if you already have one.</span></span> <span data-ttu-id="f85d3-144">새 계정을 만들면 확인 전자 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="f85d3-144">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="f85d3-145">패키지를 업로드하려면 먼저 계정을 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f85d3-145">You must confirm the account before you can upload a package.</span></span>

1. <span data-ttu-id="f85d3-146">로그인되면 사용자 이름(오른쪽 위)을 선택한 다음 **API 키**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f85d3-146">Once logged in, select your user name (on the upper right), then select **API Keys**.</span></span>

1. <span data-ttu-id="f85d3-147">**만들기**를 선택하고, 키 이름을 제공하고, **API 키** 아래에서 **범위 선택 > 푸시**를 차례로 선택하고, **GLOB 패턴**에 대해 *를 입력한 다음, **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f85d3-147">Select **Create**, provide a name for your key, select **Select Scopes > Push**Under **API Key**, enter * for **Glob pattern**, then select **Create**.</span></span>

1. <span data-ttu-id="f85d3-148">키가 만들어지면 **복사**를 선택하여 CLI에서 필요한 액세스 키를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f85d3-148">Once the key is created, select **Copy** to retrieve the access key you'll need in the CLI:</span></span>

    ![클립보드에 API 키 복사](media/QS_Create-02-APIKey.png)

    > [!Warning]
    > <span data-ttu-id="f85d3-150">키를 안전한 위치에 저장하고 비밀로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="f85d3-150">Save your key in a secure location and keep is a secret.</span></span> <span data-ttu-id="f85d3-151">키가 실수로 노출되는 경우 언제든지 키를 다시 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f85d3-151">If your key is accidentally revealed, you can always regenerate it at any time.</span></span> <span data-ttu-id="f85d3-152">CLI를 통해 더 이상 패키지를 푸시하지 않으려는 경우 API 키를 제거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f85d3-152">You can also remove the API key if you no longer want to push packages via the CLI.</span></span>

1. <span data-ttu-id="f85d3-153">명령 프롬프트에서 다음 명령을 실행하여 패키지 이름을 지정하고 키를 4단계에서 복사한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f85d3-153">At a command prompt, run the following command, specifying your package name and replacing the key with the value copied in step 4:</span></span>

    ```
    nuget push AppLogger.1.0.0.0.nupkg 47be3377-c434-4c29-8576-af7f6993a54b -Source https://api.nuget.org/v3/index.json
    ```
    
1. <span data-ttu-id="f85d3-154">nuget.exe에서 게시 프로세스의 결과를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f85d3-154">nuget.exe displays the results of the publishing process:</span></span>

    ```
    Pushing AppLogger.1.0.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed. 
    ```

1. <span data-ttu-id="f85d3-155">nuget.org의 프로필에서 **패키지 관리**를 선택하여 방금 게시한 패키지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f85d3-155">From your profile on nuget.org, Select **Manage Packages** to see the one you just published.</span></span> <span data-ttu-id="f85d3-156">또한 확인 전자 메일을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f85d3-156">You also receive a confirmation email.</span></span> <span data-ttu-id="f85d3-157">패키지가 인덱싱되어 다른 사용자가 찾을 수 있는 검색 결과에 표시되는 데 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f85d3-157">Note that it might take a while for your package to be indexed and appear in search results where others can find it.</span></span> <span data-ttu-id="f85d3-158">그 동안 아래 메시지가 패키지 페이지에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f85d3-158">During that time your package page shows the message below:</span></span>

    ![이 패키지는 아직 인덱싱되지 않았습니다.](media/QS_Create-03-NotIndexed.png)

> [!Note]
> <span data-ttu-id="f85d3-161">**바이러스 검사**: nuget.org에 업로드된 모든 패키지에 대해 바이러스를 검사하고 바이러스가 발견되면 해당 패키지가 거부됩니다.</span><span class="sxs-lookup"><span data-stu-id="f85d3-161">**Virus scanning**: All packages uploaded to nuget.org are scanned for viruses and rejected if any viruses are found.</span></span> <span data-ttu-id="f85d3-162">nuget.org에 나열된 모든 패키지도 정기적으로 검사됩니다.</span><span class="sxs-lookup"><span data-stu-id="f85d3-162">All packages listed on nuget.org are also scanned periodically.</span></span>

<span data-ttu-id="f85d3-163">됐습니다!</span><span class="sxs-lookup"><span data-stu-id="f85d3-163">And that's it!</span></span> <span data-ttu-id="f85d3-164">방금 첫 번째 NuGet 패키지를 [nuget.org](https://www.nuget.org/)에 게시했으므로 다른 개발자가 자신의 프로젝트에서 이 패키지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f85d3-164">You've just published your first NuGet package to [nuget.org](https://www.nuget.org/), that other developers can use in their own projects.</span></span>

## <a name="related-topics"></a><span data-ttu-id="f85d3-165">관련 항목</span><span class="sxs-lookup"><span data-stu-id="f85d3-165">Related topics</span></span>

- [<span data-ttu-id="f85d3-166">패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="f85d3-166">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="f85d3-167">패키지 게시</span><span class="sxs-lookup"><span data-stu-id="f85d3-167">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="f85d3-168">여러 대상 프레임워크 지원</span><span class="sxs-lookup"><span data-stu-id="f85d3-168">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="f85d3-169">패키지 버전 관리</span><span class="sxs-lookup"><span data-stu-id="f85d3-169">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="f85d3-170">지역화된 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="f85d3-170">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
