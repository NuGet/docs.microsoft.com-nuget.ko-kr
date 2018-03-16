---
title: "dotnet CLI를 통한 NuGet 패키지 사용에 대한 소개 가이드 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: ".NET Core 프로젝트에서 NuGet 패키지를 설치하고 사용하는 프로세스에 대한 연습 자습서입니다."
keywords: "NuGet 설치, NuGet 패키지 사용, NuGet 패키지 설치, NuGet 패키지 참조, NuGet 패키지 사용"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: accc6d7bb5abff43ffaa083fa55c13cd5b10ce10
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/08/2018
---
# <a name="install-and-use-a-package-using-the-dotnet-cli"></a><span data-ttu-id="3a7cb-104">dotnet CLI를 사용하여 패키지 설치 및 사용</span><span class="sxs-lookup"><span data-stu-id="3a7cb-104">Install and use a package using the dotnet CLI</span></span>

<span data-ttu-id="3a7cb-105">NuGet 패키지는 다른 개발자가 프로젝트에서 사용하기 위해 제공하는 다시 사용할 수 있는 코드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="3a7cb-105">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="3a7cb-106">배경 지식은 [NuGet이란?](../What-is-NuGet.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3a7cb-106">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="3a7cb-107">패키지는 이 문서에 설명된 대로 널리 사용되는 [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) 패키지에 대해 `dotnet add package` 명령을 사용하여 .NET Core 프로젝트에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a7cb-107">Packages are installed into a .NET Core project using the `dotnet add package` command as described in this article for the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package.</span></span>

<span data-ttu-id="3a7cb-108">패키지가 설치되면 `using <namespace>`를 사용하여 코드에서 패키지를 참조합니다. 여기서 \<네임스페이스\>는 사용 중인 패키지에 특정됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a7cb-108">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="3a7cb-109">일단 참조를 만들면 해당 API를 통해 패키지를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a7cb-109">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="3a7cb-110">**nuget.org 시작**: nuget.org 검색은 일반적으로 .NET 개발자가 고유의 응용 프로그램에서 다시 사용할 수 있는 구성 요소를 찾는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="3a7cb-110">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="3a7cb-111">nuget.org를 직접 검색하거나 이 문서에 표시된 대로 Visual Studio 내에서 패키지를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a7cb-111">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3a7cb-112">전제 조건</span><span class="sxs-lookup"><span data-stu-id="3a7cb-112">Prerequisites</span></span>

- <span data-ttu-id="3a7cb-113">`dotnet` 명령줄 도구를 제공하는 [.NET Core SDK](https://www.microsoft.com/net/download/).</span><span class="sxs-lookup"><span data-stu-id="3a7cb-113">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="3a7cb-114">프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="3a7cb-114">Create a project</span></span>

<span data-ttu-id="3a7cb-115">NuGet 패키지는 일종의 .NET 프로젝트에 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a7cb-115">NuGet packages can be installed into a .NET project of some kind.</span></span> <span data-ttu-id="3a7cb-116">이 연습에서는 다음과 같이 간단한 .NET Core 콘솔 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3a7cb-116">For this walkthrough, create a simple .NET Core console project as follows:</span></span>

1. <span data-ttu-id="3a7cb-117">프로젝트의 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3a7cb-117">Create a folder for the project.</span></span>

1. <span data-ttu-id="3a7cb-118">다음 명령을 사용하여 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3a7cb-118">Create the project using the following command:</span></span>

    ```cli
    dotnet new console
    ```

1. <span data-ttu-id="3a7cb-119">`dotnet run`을 사용하여 앱이 제대로 만들어졌는지 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="3a7cb-119">Use `dotnet run` to test that the app has been created properly.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="3a7cb-120">Newtonsoft.Json NuGet 패키지 추가</span><span class="sxs-lookup"><span data-stu-id="3a7cb-120">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="3a7cb-121">다음 명령을 사용하여 `Newtonsoft.json` 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="3a7cb-121">Use the following command to install the `Newtonsoft.json` package:</span></span>

    ```cli
    dotnet add package Newtonsoft.Json
    ```

1. <span data-ttu-id="3a7cb-122">명령이 완료된 후 `.csproj` 파일을 열어 추가된 참조를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3a7cb-122">After the command completes, open the `.csproj` file to see the added reference:</span></span>

    ```xml
  <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="10.0.3" />
  </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="3a7cb-123">앱에서 Newtonsoft.Json API 사용</span><span class="sxs-lookup"><span data-stu-id="3a7cb-123">Use the Newtonsoft.Json API in the app</span></span>

1. <span data-ttu-id="3a7cb-124">`Program.cs` 파일을 열고 파일 맨 위에 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3a7cb-124">Open the `Program.cs` file and add the following line at the top of the file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="3a7cb-125">`class Program` 줄 앞에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3a7cb-125">Add the following code before the `class Program` line:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. <span data-ttu-id="3a7cb-126">`Main` 함수를 다음과 같이 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3a7cb-126">Replace the `Main` function with the following:</span></span>

    ```cs
    static void Main(string[] args)
    {
        Account account = new Account
        {
            Name = "John Doe",
            Email = "john@nuget.org",
            DOB = new DateTime(1980, 2, 20, 0, 0, 0, DateTimeKind.Utc),
        };

        string json = JsonConvert.SerializeObject(account, Formatting.Indented);
        Console.WriteLine(json);
    }
    ```

1. <span data-ttu-id="3a7cb-127">`dotnet run` 명령을 사용하여 앱을 빌드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3a7cb-127">Build and run the app by using the `dotnet run` command.</span></span> <span data-ttu-id="3a7cb-128">출력은 코드에서 `Account` 개체의 JSON 표현이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a7cb-128">The output should be the JSON representation of the `Account` object in the code:</span></span>

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```

## <a name="related-articles"></a><span data-ttu-id="3a7cb-129">관련 문서</span><span class="sxs-lookup"><span data-stu-id="3a7cb-129">Related articles</span></span>

- [<span data-ttu-id="3a7cb-130">패키지 사용 개요 및 워크플로</span><span class="sxs-lookup"><span data-stu-id="3a7cb-130">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="3a7cb-131">패키지 찾기 및 선택</span><span class="sxs-lookup"><span data-stu-id="3a7cb-131">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="3a7cb-132">패키지 설치 방법</span><span class="sxs-lookup"><span data-stu-id="3a7cb-132">Ways to install a package</span></span>](../consume-packages/ways-to-install-a-package.md)
- [<span data-ttu-id="3a7cb-133">NuGet 동작 구성</span><span class="sxs-lookup"><span data-stu-id="3a7cb-133">Configuring NuGet Behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)
