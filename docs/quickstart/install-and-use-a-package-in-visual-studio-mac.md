---
title: Mac용 Visual Studio에서 NuGet 패키지 설치 및 사용
description: Mac용 Visual Studio 프로젝트에서 NuGet 패키지를 설치하고 사용하는 프로세스에 대한 연습 자습서입니다.
author: jmatthiesen
ms.author: jomatthi
ms.date: 08/14/2019
ms.topic: quickstart
ms.openlocfilehash: 6f3fd4f2ffec0037a48aec845fddee258b5c1e7f
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/07/2020
ms.locfileid: "70238479"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-for-mac"></a><span data-ttu-id="ae516-103">빠른 시작: Mac용 Visual Studio에서 패키지 설치 및 사용</span><span class="sxs-lookup"><span data-stu-id="ae516-103">Quickstart: Install and use a package in Visual Studio for Mac</span></span>

<span data-ttu-id="ae516-104">NuGet 패키지는 다른 개발자가 프로젝트에서 사용하기 위해 제공하는 다시 사용할 수 있는 코드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ae516-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="ae516-105">배경 지식은 [NuGet이란?](../What-is-NuGet.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae516-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="ae516-106">패키지는 NuGet 패키지 관리자를 사용하여 Mac용 Visual Studio 프로젝트에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae516-106">Packages are installed into a Visual Studio for Mac project using the NuGet Package Manager.</span></span> <span data-ttu-id="ae516-107">이 문서에서는 널리 사용되는 [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) 패키지 및.NET Core 콘솔 프로젝트를 사용하는 프로세스를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="ae516-107">This article demonstrates the process using the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a .NET Core console project.</span></span> <span data-ttu-id="ae516-108">기타 모든 Xamarin 또는 .NET Core 프로젝트에 같은 프로세스가 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae516-108">The same process applies to any other Xamarin or .NET Core project.</span></span>

<span data-ttu-id="ae516-109">패키지가 설치되면 `using <namespace>`를 사용하여 코드에서 패키지를 참조합니다. 여기서 \<네임스페이스\>는 사용 중인 패키지에 특정됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae516-109">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="ae516-110">일단 참조를 만들면 해당 API를 통해 패키지를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae516-110">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="ae516-111">**nuget.org 시작**: *nuget.org* 검색은 일반적으로 .NET 개발자가 고유의 애플리케이션에서 다시 사용할 수 있는 구성 요소를 찾는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="ae516-111">**Start with nuget.org**: Browsing *nuget.org* is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="ae516-112">*nuget.org*를 직접 검색하거나 이 문서에 표시된 대로 Visual Studio 내에서 패키지를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae516-112">You can search *nuget.org* directly or find and install packages within Visual Studio as shown in this article.</span></span> <span data-ttu-id="ae516-113">일반 정보는 [NuGet 패키지 찾기 및 평가](../consume-packages/finding-and-choosing-packages.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae516-113">For general information, see [Find and evaluate NuGet packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ae516-114">사전 요구 사항</span><span class="sxs-lookup"><span data-stu-id="ae516-114">Prerequisites</span></span>

- <span data-ttu-id="ae516-115">Mac용 Visual Studio 2019.</span><span class="sxs-lookup"><span data-stu-id="ae516-115">Visual Studio 2019 for Mac.</span></span>

<span data-ttu-id="ae516-116">[visualstudio.com](https://www.visualstudio.com/)에서 추가 비용 없이 2019 Community 버전을 설치하거나 Professional 또는 Enterprise 버전을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae516-116">You can install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

<span data-ttu-id="ae516-117">Windows에서 Visual Studio를 사용하는 경우 [Visual Studio에서 패키지 설치 및 사용(Windows만 해당)](install-and-use-a-package-in-visual-studio.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae516-117">If you're using Visual Studio on Windows, see [Install and use a package in Visual Studio (Windows Only)](install-and-use-a-package-in-visual-studio.md).</span></span>

## <a name="create-a-project"></a><span data-ttu-id="ae516-118">프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="ae516-118">Create a project</span></span>

<span data-ttu-id="ae516-119">NuGet 패키지는 패키지가 프로젝트와 동일한 대상 프레임워크를 지원하는 경우 어느 .NET 프로젝트에나 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae516-119">NuGet packages can be installed into any .NET project, provided that the package supports the same target framework as the project.</span></span>

<span data-ttu-id="ae516-120">이 연습에서는 간단한 .NET Core 콘솔 앱을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ae516-120">For this walkthrough, use a simple .NET Core Console app.</span></span> <span data-ttu-id="ae516-121">Mac용 Visual Studio에서 **파일 > 새 솔루션**을 클릭하여 프로젝트를 만들고 **.NET Core > 앱 > 콘솔 응용 프로그램** 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ae516-121">Create a project in Visual Studio for Mac using **File > New Solution...**, select the **.NET Core > App > Console Application** template.</span></span> <span data-ttu-id="ae516-122">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ae516-122">Click **Next**.</span></span> <span data-ttu-id="ae516-123">메시지가 표시되면 **대상 프레임워크**의 기본값을 그대로 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="ae516-123">Accept the default values for **Target Framework** when prompted.</span></span>

<span data-ttu-id="ae516-124">Visual Studio에서 프로젝트를 만들고 솔루션 탐색기에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="ae516-124">Visual Studio creates the project, which opens in Solution Explorer.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="ae516-125">Newtonsoft.Json NuGet 패키지 추가</span><span class="sxs-lookup"><span data-stu-id="ae516-125">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="ae516-126">패키지를 설치하려면 NuGet 패키지 관리자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ae516-126">To install the package, you use the NuGet Package Manager.</span></span> <span data-ttu-id="ae516-127">패키지를 설치하면 NuGet에서 프로젝트 파일 또는 `packages.config` 파일에 종속성을 기록합니다(프로젝트 형식에 따라).</span><span class="sxs-lookup"><span data-stu-id="ae516-127">When you install a package, NuGet records the dependency in  either your project file or a `packages.config` file (depending on the project format).</span></span> <span data-ttu-id="ae516-128">자세한 내용은 [패키지 소비 개요 및 워크플로](../consume-packages/Overview-and-Workflow.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae516-128">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="nuget-package-manager"></a><span data-ttu-id="ae516-129">NuGet 패키지 관리자</span><span class="sxs-lookup"><span data-stu-id="ae516-129">NuGet Package Manager</span></span>

1. <span data-ttu-id="ae516-130">솔루션 탐색기에서 **종속성**을 마우스 오른쪽 단추로 클릭하고 **패키지 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ae516-130">In Solution Explorer, right-click **Dependencies** and choose **Add Packages...**.</span></span>

    ![프로젝트 참조에 대한 NuGet 패키지 관리 명령](media/QS_Use_Mac-02-ManageNuGetPackages.png)

1. <span data-ttu-id="ae516-132">대화 상자의 왼쪽 위 모서리에서 **패키지 원본**으로 "nuget.org"를 선택하고 **Newtonsoft.Json**을 검색하여 목록에서 해당 패키지를 선택한 다음 **패키지 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ae516-132">Choose "nuget.org" as the **Package source** in the top left corner of the dialog, and search for **Newtonsoft.Json**, select that package in the list, and select **Add Packages...**:</span></span>

    ![Newtonsoft.Json 패키지 찾기](media/QS_Use_Mac-03-NewtonsoftJson.png)

    <span data-ttu-id="ae516-134">NuGet 패키지 관리자에 대한 자세한 내용은 [Mac용 Visual Studio를 사용하여 패키지 설치 및 관리](../consume-packages/install-use-packages-visual-studio.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae516-134">If you want more information on the NuGet Package Manager, see [Install and manage packages using Visual Studio for Mac](../consume-packages/install-use-packages-visual-studio.md).</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="ae516-135">앱에서 Newtonsoft.Json API 사용</span><span class="sxs-lookup"><span data-stu-id="ae516-135">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="ae516-136">프로젝트의 Newtonsoft.Json 패키지에서 해당 `JsonConvert.SerializeObject` 메서드를 호출하여 개체를 사람이 인식할 수 있는 문자열로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae516-136">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="ae516-137">`Program.cs` 파일(Solution Pad에 있음)을 열고 파일 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ae516-137">Open the `Program.cs` file (located in the Solution Pad) and replace the file contents with the following code:</span></span>

    ```cs
    using System;
    using Newtonsoft.Json;

    namespace NuGetDemo
    {
        public class Account
        {
            public string Name { get; set; }
            public string Email { get; set; }
            public DateTime DOB { get; set; }
        }
    
        class Program
        {
            static void Main(string[] args)
            {
                Account account = new Account()
                {
                    Name = "Joe Doe",
                    Email = "joe@test.com",
                    DOB = new DateTime(1976, 3, 24)
                };
                string json = JsonConvert.SerializeObject(account);
                Console.WriteLine(json);
            }
        }
    }
    ```

1. <span data-ttu-id="ae516-138">**실행 > 디버깅 시작**을 선택하여 앱을 빌드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ae516-138">Build and run the app by selecting **Run > Start Debugging**:</span></span>

1. <span data-ttu-id="ae516-139">앱이 실행되면 직렬화된 JSON 출력이 콘솔에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae516-139">Once the app runs, you'll see the serialized JSON output appear in the console:</span></span>

  ![콘솔 앱의 출력](media/QS_Use_Mac-06-AppStart.png)

## <a name="next-steps"></a><span data-ttu-id="ae516-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ae516-141">Next steps</span></span>
<span data-ttu-id="ae516-142">첫 번째 NuGet 패키지를 설치하고 사용하시게 된 것을 축하드립니다.</span><span class="sxs-lookup"><span data-stu-id="ae516-142">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ae516-143">Mac용 Visual Studio를 사용하여 패키지 설치 및 관리</span><span class="sxs-lookup"><span data-stu-id="ae516-143">Install and manage packages using Visual Studio for Mac</span></span>](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json)

<span data-ttu-id="ae516-144">NuGet에서 제공하는 다른 기능을 탐색하려면 아래 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ae516-144">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="ae516-145">패키지 사용 개요 및 워크플로</span><span class="sxs-lookup"><span data-stu-id="ae516-145">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="ae516-146">프로젝트 파일의 패키지 참조</span><span class="sxs-lookup"><span data-stu-id="ae516-146">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
