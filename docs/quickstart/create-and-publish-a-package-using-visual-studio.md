---
title: Windows에서 Visual Studio를 사용하여 .NET Standard NuGet 패키지 만들기 및 게시
description: Windows에서 Visual Studio를 사용하여 .NET Standard NuGet 패키지를 만들고 게시하는 방법에 대한 연습 자습서입니다.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: quickstart
ms.openlocfilehash: 0fc3b15c6d5ffa93eb6e26660f71cea2286ba77d
ms.sourcegitcommit: aed04cc04b0902403612de6736a900d41c265afd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2019
ms.locfileid: "68821427"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a><span data-ttu-id="b2f1d-103">빠른 시작: Visual Studio(.NET Standard, Windows 전용)를 사용하여 NuGet 패키지 만들기 및 게시</span><span class="sxs-lookup"><span data-stu-id="b2f1d-103">Quickstart: Create and publish a NuGet package using Visual Studio (.NET Standard, Windows only)</span></span>

<span data-ttu-id="b2f1d-104">Windows에서 Visual Studio의 .NET Standard 클래스 라이브러리에서 NuGet 패키지를 만들고 CLI 도구를 사용하여 nuget.org에 게시하는 간단한 과정입니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-104">It's a simple process to create a NuGet package from a .NET Standard Class Library in Visual Studio on Windows, and then publish it to nuget.org using a CLI tool.</span></span>

> [!Note]
> <span data-ttu-id="b2f1d-105">Mac용 Visual Studio를 사용하는 경우 NuGet 패키지 생성에 대해 [이 정보](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library)를 참조하거나 [dotnet CLI 도구](create-and-publish-a-package-using-the-dotnet-cli.md)를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-105">If you are using Visual Studio for Mac, refer to [this information](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) on creating a NuGet package, or use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b2f1d-106">전제 조건</span><span class="sxs-lookup"><span data-stu-id="b2f1d-106">Prerequisites</span></span>

1. <span data-ttu-id="b2f1d-107">.NET Core 관련 워크로드를 사용하여 [visualstudio.com](https://www.visualstudio.com/)에서 Visual Studio 2017 이상 버전을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-107">Install any edition of Visual Studio 2017 or higher from [visualstudio.com](https://www.visualstudio.com/) with a .NET Core related workload.</span></span>

1. <span data-ttu-id="b2f1d-108">아직 설치하지 않은 경우 `dotnet` CLI를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-108">If it's not already installed, install the `dotnet` CLI.</span></span>

   <span data-ttu-id="b2f1d-109">`dotnet` CLI의 경우, Visual Studio 2017부터 `dotnet` CLI가 모든 .NET Core 관련 워크로드와 함께 자동으로 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-109">For the `dotnet` CLI, starting in Visual Studio 2017, the `dotnet` CLI is automatically installed with any .NET Core related workloads.</span></span> <span data-ttu-id="b2f1d-110">그렇지 않으면 [.NET Core SDK](https://www.microsoft.com/net/download/)를 설치하여 `dotnet` CLI를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-110">Otherwise, install the [.NET Core SDK](https://www.microsoft.com/net/download/) to get the `dotnet` CLI.</span></span> <span data-ttu-id="b2f1d-111">`dotnet` CLI는 [SDK 스타일 형식](../resources/check-project-format.md)(SDK 특성)을 사용하는 .NET Standard 프로젝트에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-111">The `dotnet` CLI is required for .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md) (SDK attribute).</span></span> <span data-ttu-id="b2f1d-112">이 문서에서 사용되는 Visual Studio 2017 이상의 기본 클래스 라이브러리 템플릿은 SDK 특성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-112">The default class library template in Visual Studio 2017 and higher, which is used in this article, uses the SDK attribute.</span></span>
   
   > [!Important]
   > <span data-ttu-id="b2f1d-113">이 문서에서는 `dotnet` CLI가 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-113">For this article, the `dotnet` CLI is recommended.</span></span> <span data-ttu-id="b2f1d-114">`nuget.exe` CLI를 사용하여 NuGet 패키지를 게시할 수는 있지만 이 문서의 일부 단계는 SDK 스타일 프로젝트 및 dotnet CLI와 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-114">Although you can publish any NuGet package using the `nuget.exe` CLI, some of the steps in this article are specific to SDK-style projects and the dotnet CLI.</span></span> <span data-ttu-id="b2f1d-115">nuget.exe CLI는 [비 SDK 스타일 프로젝트](../resources/check-project-format.md)에 사용됩니다(일반적으로 .NET Framework).</span><span class="sxs-lookup"><span data-stu-id="b2f1d-115">The nuget.exe CLI is used for [non-SDK-style projects](../resources/check-project-format.md) (typically .NET Framework).</span></span> <span data-ttu-id="b2f1d-116">비 SDK 스타일 프로젝트를 사용하는 경우 [.NET Framework 패키지 만들기 및 게시(Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md)의 절차에 따라 패키지를 만들고 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-116">If you are working with a non-SDK-style project, follow the procedures in [Create and publish a .NET Framework package (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md) to create and publish the package.</span></span>

1. <span data-ttu-id="b2f1d-117">아직 없는 경우 [nuget.org에 체험 계정을 등록](https://docs.microsoft.com/en-us/nuget/nuget-org/individual-accounts#add-a-new-individual-account)합니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-117">[Register for a free account on nuget.org](https://docs.microsoft.com/en-us/nuget/nuget-org/individual-accounts#add-a-new-individual-account) if you don't have one already.</span></span> <span data-ttu-id="b2f1d-118">새 계정을 만들면 확인 전자 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-118">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="b2f1d-119">패키지를 업로드하려면 먼저 계정을 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-119">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="b2f1d-120">클래스 라이브러리 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="b2f1d-120">Create a class library project</span></span>

<span data-ttu-id="b2f1d-121">패키지할 코드에 대해 기존 .NET Standard 클래스 라이브러리 프로젝트를 사용하거나 다음과 같이 간단한 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-121">You can use an existing .NET Standard Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="b2f1d-122">Visual Studio에서 **파일 > 새로 만들기 > 프로젝트**를 차례로 선택하고, **Visual C# > .NET Standard** 노드를 펼치고, “클래스 라이브러리(.NET Standard)” 템플릿을 선택하고, 프로젝트 이름을 AppLogger로 지정한 다음, **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-122">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="b2f1d-123">결과 프로젝트 파일을 마우스 오른쪽 단추로 클릭하고, **빌드**를 선택하여 프로젝트가 제대로 만들어졌는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-123">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="b2f1d-124">DLL은 Debug(또는 해당 구성을 대신 빌드하는 경우 Release) 폴더 내에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-124">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="b2f1d-125">물론 실제 NuGet 패키지 내에서 다른 사람들이 애플리케이션을 빌드할 수 있는 많은 유용한 기능을 구현할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-125">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="b2f1d-126">그러나 이 연습에서는 템플릿의 클래스 라이브러리가 패키지를 만드는 데 충분하므로 추가 코드를 작성하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-126">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="b2f1d-127">그러나 계속 패키지에 대한 함수형 코드를 원하는 경우 다음을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-127">Still, if you'd like some functional code for the package, use the following:</span></span>

```cs
namespace AppLogger
{
    public class Logger
    {
        public void Log(string text)
        {
            Console.WriteLine(text);
        }
    }
}
```

> [!Tip]
> <span data-ttu-id="b2f1d-128">별도로 선택하지 않는 한 .NET Standard는 가장 넓은 범위의 사용하는 프로젝트와 호환되기 때문에 NuGet 패키지의 기본 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-128">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

## <a name="configure-package-properties"></a><span data-ttu-id="b2f1d-129">패키지 속성 구성</span><span class="sxs-lookup"><span data-stu-id="b2f1d-129">Configure package properties</span></span>

1. <span data-ttu-id="b2f1d-130">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **속성** 메뉴 명령을 선택한 후 **패키지** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-130">Right-click the project in Solution Explorer, and choose **Properties** menu command, then select the **Package** tab.</span></span>

   <span data-ttu-id="b2f1d-131">**패키지** 탭은 Visual Studio의 SDK 스타일 프로젝트(일반적으로 .NET Standard 또는 .NET Core 클래스 라이브러리 프로젝트)에 대해서만 표시됩니다. 비 SDK 스타일 프로젝트(일반적으로 .NET Framework)를 대상으로 하는 경우 [프로젝트를 마이그레이션](../reference/migrate-packages-config-to-package-reference.md)하거나 `dotnet` CLI를 사용할 수 있으며, 단계별 지침 대신 [.NET Framework 패키지 만들기 및 게시](create-and-publish-a-package-using-visual-studio-net-framework.md) 또는 [.NET Framework 패키지 만들기 및 게시](create-and-publish-a-package-using-visual-studio-net-framework.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-131">The **Package** tab appears only for SDK-style projects in Visual Studio, typically .NET Standard or .NET Core class library projects; if you are targeting a non-SDK style project (typically .NET Framework), either [migrate the project](../reference/migrate-packages-config-to-package-reference.md) and use `dotnet` CLI, or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead for step-by-step instructions.</span></span>

    ![Visual Studio 프로젝트의 NuGet 패키지 속성](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="b2f1d-133">공용으로 빌드된 패키지의 경우 **태그** 속성에 특히 주의하세요. 태그는 다른 사람들이 패키지를 찾고 그 기능을 이해하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-133">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="b2f1d-134">패키지에 고유 식별자를 제공하고 원하는 다른 모든 속성을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-134">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="b2f1d-135">다른 속성에 대한 설명은 [.nuspec 파일 참조](../reference/nuspec.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-135">For a description of the different properties, see [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="b2f1d-136">여기에 있는 모든 속성은 Visual Studio에서 프로젝트에 대해 만드는 `.nuspec` 매니페스트로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-136">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="b2f1d-137">nuget.org 또는 무엇이든 사용 중인 호스트에서 고유한 식별자를 패키지에 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-137">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="b2f1d-138">이 연습에서는 나중 게시 단계에서 패키지를 공개적으로 표시할 수 있도록 이름에 “샘플” 또는 “테스트”를 포함하는 것이 좋습니다(실제로 아무도 사용할 가능성이 없더라도).</span><span class="sxs-lookup"><span data-stu-id="b2f1d-138">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="b2f1d-139">이미 존재하는 이름으로 패키지를 게시하려고 시도하면 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-139">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="b2f1d-140">선택 사항: 프로젝트 파일에서 직접 속성을 보려면 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **AppLogger.csproj 편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-140">Optional: to see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj**.</span></span>

   <span data-ttu-id="b2f1d-141">이 옵션은 SDK 스타일 특성을 사용하는 프로젝트의 경우 Visual Studio 2017부터만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-141">This option is only available starting in Visual Studio 2017 for projects that use the SDK-style attribute.</span></span> <span data-ttu-id="b2f1d-142">그렇지 않은 경우 프로젝트를 마우스 오른쪽 단추로 클릭하고 **프로젝트 언로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-142">Otherwise, right-click the project and choose **Unload Project**.</span></span> <span data-ttu-id="b2f1d-143">그런 다음, 언로드된 프로젝트를 마우스 오른쪽 단추로 클릭하고 **AppLogger.csproj 편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-143">Then right-click the unloaded project and choose **Edit AppLogger.csproj**.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="b2f1d-144">pack 명령 실행</span><span class="sxs-lookup"><span data-stu-id="b2f1d-144">Run the pack command</span></span>

1. <span data-ttu-id="b2f1d-145">구성을 **해제**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-145">Set the configuration to **Release**.</span></span>

1. <span data-ttu-id="b2f1d-146">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **Pack** 명령을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-146">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Visual Studio 프로젝트 상황에 맞는 메뉴의 NuGet pack 명령](media/qs_create-vs-02-pack-command.png)

    <span data-ttu-id="b2f1d-148">**Pack** 명령이 표시되지 않는 경우 프로젝트는 SDK 스타일 프로젝트가 아닌 것이므로 `nuget.exe` CLI를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-148">If you don't see the **Pack** command, your project is probably not an SDK-style project and you need to use the `nuget.exe` CLI.</span></span> <span data-ttu-id="b2f1d-149">[프로젝트를 마이그레이션](../reference/migrate-packages-config-to-package-reference.md)하고 `dotnet` CLI를 사용하거나 단계별 지침 대신 [.NET Framework 패키지 만들기 및 게시](create-and-publish-a-package-using-visual-studio-net-framework.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-149">Either [migrate the project](../reference/migrate-packages-config-to-package-reference.md) and use `dotnet` CLI, or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead for step-by-step instructions.</span></span>

1. <span data-ttu-id="b2f1d-150">Visual Studio에서 프로젝트를 빌드하고 `.nupkg` 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-150">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="b2f1d-151">**출력** 창에서 패키지 파일의 경로가 포함된 다음과 같은 세부 정보가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-151">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="b2f1d-152">또한 빌드된 어셈블리는 .NET Standard 2.0 대상에 맞게 `bin\Release\netstandard2.0`에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-152">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="optional-generate-package-on-build"></a><span data-ttu-id="b2f1d-153">(선택 사항) 빌드 시 패키지 생성</span><span class="sxs-lookup"><span data-stu-id="b2f1d-153">(Optional) Generate package on build</span></span>

<span data-ttu-id="b2f1d-154">프로젝트를 빌드할 때 NuGet 패키지를 자동으로 생성하도록 Visual Studio를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-154">You can configure Visual Studio to automatically generate the NuGet package when you build the project.</span></span>

1. <span data-ttu-id="b2f1d-155">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-155">In Solution Explorer, right-click the project and choose **Properties**.</span></span>

2. <span data-ttu-id="b2f1d-156">**패키지** 탭에서 **빌드 시 NuGet 패키지 생성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-156">In the **Package** tab, select **Generate NuGet package on build**.</span></span>

   ![빌드 시 패키지를 자동으로 생성](media/qs_create-vs-05-generate-on-build.png)

> [!NOTE]
> <span data-ttu-id="b2f1d-158">패키지를 자동으로 생성할 때 압축하는 데 소요되는 시간 때문에 프로젝트의 빌드 시간이 늘어납니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-158">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="optional-pack-with-msbuild"></a><span data-ttu-id="b2f1d-159">(선택 사항) MSBuild를 사용하여 압축</span><span class="sxs-lookup"><span data-stu-id="b2f1d-159">(Optional) pack with MSBuild</span></span>

<span data-ttu-id="b2f1d-160">**Pack** 메뉴 명령을 사용하는 대신 프로젝트에 필요한 패키지 데이터가 포함된 경우 NuGet 4.x 이상 및 MSBuild 15.1 이상은 `pack` 대상을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-160">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data.</span></span> <span data-ttu-id="b2f1d-161">명령 프롬프트를 열고 프로젝트 폴더로 이동한 후 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-161">Open a command prompt, navigate to your project folder and run the following command.</span></span> <span data-ttu-id="b2f1d-162">(일반적으로 시작 메뉴에서 "Visual Studio용 개발자 명령 프롬프트"를 시작하는 것이 좋습니다. MSBuild에 필요한 모든 경로로 구성되기 때문입니다.)</span><span class="sxs-lookup"><span data-stu-id="b2f1d-162">(You typically want to start the "Developer Command Prompt for Visual Studio" from the Start menu, as it will be configured with all the necessary paths for MSBuild.)</span></span>

<span data-ttu-id="b2f1d-163">자세한 내용은 [MSBuild를 사용하여 패키지 만들기](../create-packages/creating-a-package-msbuild.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-163">For more information, see [Create a package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="b2f1d-164">패키지 게시</span><span class="sxs-lookup"><span data-stu-id="b2f1d-164">Publish the package</span></span>

<span data-ttu-id="b2f1d-165">`.nupkg` 파일이 있으면 nuget.org에서 얻은 API 키와 함께 `nuget.exe` CLI 또는 `dotnet.exe` CLI를 사용하여 nuget.org에 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-165">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="b2f1d-166">API 키 얻기</span><span class="sxs-lookup"><span data-stu-id="b2f1d-166">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push-dotnet-cli"></a><span data-ttu-id="b2f1d-167">dotnet nuget push로 게시(dotnet CLI)</span><span class="sxs-lookup"><span data-stu-id="b2f1d-167">Publish with dotnet nuget push (dotnet CLI)</span></span>

<span data-ttu-id="b2f1d-168">이 단계는 `nuget.exe`를 사용하는 방법의 대안으로 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-168">This step is the recommended alternative to using `nuget.exe`.</span></span>

<span data-ttu-id="b2f1d-169">패키지를 게시하려면 먼저 명령줄을 열어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-169">Before you can publish the package, you must first open a command line.</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-with-nuget-push-nugetexe-cli"></a><span data-ttu-id="b2f1d-170">nuget push로 게시(nuget.exe CLI)</span><span class="sxs-lookup"><span data-stu-id="b2f1d-170">Publish with nuget push (nuget.exe CLI)</span></span>

<span data-ttu-id="b2f1d-171">`dotnet.exe`를 사용하는 대신 다음 단계를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-171">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="b2f1d-172">명령줄을 열고 `.nupkg` 파일을 포함하는 폴더로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-172">Open a command line and change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="b2f1d-173">다음 명령을 실행하여 패키지 이름(고유한 패키지 ID)을 지정하고 키 값을 API 키로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-173">Run the following command, specifying your package name (unique package ID) and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="b2f1d-174">nuget.exe에서 게시 프로세스의 결과를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-174">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="b2f1d-175">[nuget push](../reference/cli-reference/cli-ref-push.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-175">See [nuget push](../reference/cli-reference/cli-ref-push.md).</span></span>

### <a name="publish-errors"></a><span data-ttu-id="b2f1d-176">게시 오류</span><span class="sxs-lookup"><span data-stu-id="b2f1d-176">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="b2f1d-177">게시된 패키지 관리</span><span class="sxs-lookup"><span data-stu-id="b2f1d-177">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="b2f1d-178">추가 정보 및 기타 파일 추가</span><span class="sxs-lookup"><span data-stu-id="b2f1d-178">Adding a readme and other files</span></span>

<span data-ttu-id="b2f1d-179">패키지에 포함할 파일을 직접 지정하려면 프로젝트 파일을 편집하고 `content` 속성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-179">To directly specify files to include in the package, edit the project file and use the `content` property:</span></span>

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

<span data-ttu-id="b2f1d-180">그러면 패키지 루트에 있는 `readme.txt`라는 파일이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-180">This will include a file named `readme.txt` in the package root.</span></span> <span data-ttu-id="b2f1d-181">Visual Studio에서 패키지를 직접 설치한 직후 해당 파일의 내용을 일반 텍스트로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-181">Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="b2f1d-182">종속성으로 설치된 패키지에는 추가 정보 파일이 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-182">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="b2f1d-183">예를 들어 HtmlAgilityPack 패키지에 대한 추가 정보가 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-183">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![설치 시 NuGet 패키지에 대한 추가 정보 파일 표시](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="b2f1d-185">프로젝트 루트에 readme.txt를 단순히 추가하기만 하면 결과 패키지에 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b2f1d-185">Merely adding the readme.txt at the project root will not result in it being included in the resulting package.</span></span>

## <a name="related-topics"></a><span data-ttu-id="b2f1d-186">관련 항목</span><span class="sxs-lookup"><span data-stu-id="b2f1d-186">Related topics</span></span>

- [<span data-ttu-id="b2f1d-187">패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="b2f1d-187">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="b2f1d-188">패키지 게시</span><span class="sxs-lookup"><span data-stu-id="b2f1d-188">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="b2f1d-189">시험판 패키지</span><span class="sxs-lookup"><span data-stu-id="b2f1d-189">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="b2f1d-190">여러 대상 프레임워크 지원</span><span class="sxs-lookup"><span data-stu-id="b2f1d-190">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="b2f1d-191">패키지 버전 관리</span><span class="sxs-lookup"><span data-stu-id="b2f1d-191">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="b2f1d-192">지역화된 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="b2f1d-192">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="b2f1d-193">.NET Standard 라이브러리 설명서</span><span class="sxs-lookup"><span data-stu-id="b2f1d-193">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="b2f1d-194">.NET Framework에서 .NET Core로 이식</span><span class="sxs-lookup"><span data-stu-id="b2f1d-194">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
