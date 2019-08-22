---
title: 프로젝트 형식 식별
description: 프로젝트 형식을 식별하는 방법을 설명합니다.
author: mikejo5000
ms.author: mikejo
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: b151547e40e567b38acc2b0b9ee84c50d85000c9
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488489"
---
# <a name="identify-the-project-format"></a><span data-ttu-id="f8e34-103">프로젝트 형식 식별</span><span class="sxs-lookup"><span data-stu-id="f8e34-103">Identify the project format</span></span>

<span data-ttu-id="f8e34-104">NuGet은 모든 .NET 프로젝트에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="f8e34-104">NuGet works with all .NET projects.</span></span> <span data-ttu-id="f8e34-105">그러나 프로젝트 형식(SDK 스타일 또는 비 SDK 스타일)은 NuGet 패키지를 소비 및 만드는 데 사용해야 하는 일부 도구 및 메서드를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="f8e34-105">However, the project format (SDK-style or non-SDK-style) determines some of the tools and methods that you need to use to consume and create NuGet packages.</span></span> <span data-ttu-id="f8e34-106">Sdk 스타일 프로젝트는 [SDK 특성](/dotnet/core/tools/csproj#additions)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f8e34-106">SDK-style projects use the [SDK attribute](/dotnet/core/tools/csproj#additions).</span></span> <span data-ttu-id="f8e34-107">NuGet 패키지를 소비 및 만드는 데 사용하는 메서드 및 도구는 프로젝트 형식에 따라 달라지므로 프로젝트 형식을 식별하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="f8e34-107">It is important to identify your project type because the methods and tools you use to consume and create NuGet packages are dependent on the project format.</span></span> <span data-ttu-id="f8e34-108">비 SDK 스타일 프로젝트의 경우에는 이러한 메서드 및 도구가 프로젝트를 `PackageReference` 형식으로 마이그레이션했는지 여부에 따라서도 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="f8e34-108">For non-SDK-style projects, the methods and tools are also dependent on whether or not the project has been migrated to `PackageReference` format.</span></span>

<span data-ttu-id="f8e34-109">프로젝트가 SDK 스타일인지 여부는 프로젝트를 만드는 데 사용되는 메서드에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="f8e34-109">Whether your project is SDK-style or not depends on the method used to create the project.</span></span> <span data-ttu-id="f8e34-110">다음 표에서는 Visual Studio 2017 이상 버전을 사용하여 프로젝트를 만들 때 프로젝트의 기본 프로젝트 형식 및 관련 CLI 도구를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f8e34-110">The following table shows the default project format and the associated CLI tool for your project when you create it using Visual Studio 2017 and later versions.</span></span>

| <span data-ttu-id="f8e34-111">프로젝트&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="f8e34-111">Project&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="f8e34-112">기본 프로젝트 형식</span><span class="sxs-lookup"><span data-stu-id="f8e34-112">Default project format</span></span> | <span data-ttu-id="f8e34-113">CLI 도구&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="f8e34-113">CLI tool&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="f8e34-114">참고 사항</span><span class="sxs-lookup"><span data-stu-id="f8e34-114">Notes</span></span> |
|:------------- |:-------------|:-----|:-----|
| <span data-ttu-id="f8e34-115">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="f8e34-115">.NET Standard</span></span> | <span data-ttu-id="f8e34-116">SDK 스타일</span><span class="sxs-lookup"><span data-stu-id="f8e34-116">SDK-style</span></span> | [<span data-ttu-id="f8e34-117">dotnet CLI</span><span class="sxs-lookup"><span data-stu-id="f8e34-117">dotnet CLI</span></span>](../install-nuget-client-tools.md#dotnetexe-cli) | <span data-ttu-id="f8e34-118">Visual Studio 2017 이전 버전으로 만든 프로젝트는 SDK 스타일이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="f8e34-118">Projects created prior to Visual Studio 2017 are non-SDK-style.</span></span> <span data-ttu-id="f8e34-119">`nuget.exe` CLI를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f8e34-119">Use `nuget.exe` CLI.</span></span> |
| <span data-ttu-id="f8e34-120">.NET Core</span><span class="sxs-lookup"><span data-stu-id="f8e34-120">.NET Core</span></span> | <span data-ttu-id="f8e34-121">SDK 스타일</span><span class="sxs-lookup"><span data-stu-id="f8e34-121">SDK-style</span></span> | [<span data-ttu-id="f8e34-122">dotnet CLI</span><span class="sxs-lookup"><span data-stu-id="f8e34-122">dotnet CLI</span></span>](../install-nuget-client-tools.md#dotnetexe-cli) | <span data-ttu-id="f8e34-123">Visual Studio 2017 이전 버전으로 만든 프로젝트는 SDK 스타일이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="f8e34-123">Projects created prior to Visual Studio 2017 are non-SDK-style.</span></span> <span data-ttu-id="f8e34-124">`nuget.exe` CLI를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f8e34-124">Use `nuget.exe` CLI.</span></span> |
| <span data-ttu-id="f8e34-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="f8e34-125">.NET Framework</span></span> | <span data-ttu-id="f8e34-126">비 SDK 스타일</span><span class="sxs-lookup"><span data-stu-id="f8e34-126">Non-SDK-style</span></span> | [<span data-ttu-id="f8e34-127">nuget.exe CLI</span><span class="sxs-lookup"><span data-stu-id="f8e34-127">nuget.exe CLI</span></span>](../install-nuget-client-tools.md#nugetexe-cli) | <span data-ttu-id="f8e34-128">다른 메서드를 사용하여 만든 .NET Framework 프로젝트는 SDK 스타일 프로젝트일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8e34-128">.NET Framework projects created using other methods may be SDK-style projects.</span></span> <span data-ttu-id="f8e34-129">이러한 경우 [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli)를 대신 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f8e34-129">For these, use [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli) instead.</span></span> |
| <span data-ttu-id="f8e34-130">[마이그레이션된](../consume-packages/migrate-packages-config-to-package-reference.md) .NET 프로젝트</span><span class="sxs-lookup"><span data-stu-id="f8e34-130">[Migrated](../consume-packages/migrate-packages-config-to-package-reference.md) .NET project</span></span> | <span data-ttu-id="f8e34-131">비 SDK 스타일</span><span class="sxs-lookup"><span data-stu-id="f8e34-131">Non-SDK-style</span></span>| <span data-ttu-id="f8e34-132">패키지를 만들려면 [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration)을 사용하여 패키지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f8e34-132">To create packages, use [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration) to create packages.</span></span> | <span data-ttu-id="f8e34-133">패키지를 만들려면 `msbuild -t:pack`이 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8e34-133">To create packages, `msbuild -t:pack` is recommended.</span></span> <span data-ttu-id="f8e34-134">그렇지 않은 경우 [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f8e34-134">Otherwise, use the [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli).</span></span> <span data-ttu-id="f8e34-135">마이그레이션된 프로젝트는 SDK 스타일 프로젝트가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="f8e34-135">Migrated projects are not SDK-style projects.</span></span> |

## <a name="check-the-project-format"></a><span data-ttu-id="f8e34-136">프로젝트 형식 확인</span><span class="sxs-lookup"><span data-stu-id="f8e34-136">Check the project format</span></span>

<span data-ttu-id="f8e34-137">프로젝트가 SDK 스타일 형식인지 확실하지 않은 경우 프로젝트 파일의 `<Project>` 요소에서 SDK 특성을 찾습니다(C#의 경우 \*.csproj 파일).</span><span class="sxs-lookup"><span data-stu-id="f8e34-137">If you're unsure whether the project is SDK-style format or not, look for the SDK attribute in the `<Project>` element in the project file (For C#, this is the \*.csproj file).</span></span> <span data-ttu-id="f8e34-138">이 특성이 있으면 프로젝트가 SDK 스타일 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="f8e34-138">If it is present, the project is an SDK-style project.</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <Authors>authorname</Authors>
    <PackageId>mypackageid</PackageId>
    <Company>mycompanyname</Company>
  </PropertyGroup>

</Project>
```

## <a name="check-the-project-format-in-visual-studio"></a><span data-ttu-id="f8e34-139">Visual Studio에서 프로젝트 형식 확인</span><span class="sxs-lookup"><span data-stu-id="f8e34-139">Check the project format in Visual Studio</span></span>

<span data-ttu-id="f8e34-140">Visual Studio에서 작업하는 경우 다음 방법 중 하나를 사용하여 프로젝트 형식을 빠르게 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8e34-140">If you are working in Visual Studio, you can quickly check the project format using one of the following methods:</span></span>

- <span data-ttu-id="f8e34-141">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **myprojectname.csproj 편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f8e34-141">Right-click the project in Solution Explorer and select **Edit myprojectname.csproj**.</span></span>

   <span data-ttu-id="f8e34-142">이 옵션은 SDK 스타일 특성을 사용하는 프로젝트의 경우 Visual Studio 2017부터만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8e34-142">This option is only available starting in Visual Studio 2017 for projects that use the SDK-style attribute.</span></span> <span data-ttu-id="f8e34-143">그렇지 않으면 다른 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f8e34-143">Otherwise, use the other method.</span></span>

   ![프로젝트 파일 편집](media/edit-project-file.png)

   <span data-ttu-id="f8e34-145">Sdk 스타일 프로젝트는 프로젝트 파일에 [SDK 특성](/dotnet/core/tools/csproj#additions)을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f8e34-145">An SDK-style project shows the [SDK attribute](/dotnet/core/tools/csproj#additions) in the project file.</span></span>
   
- <span data-ttu-id="f8e34-146">**프로젝트** 메뉴에서 **프로젝트 언로드**를 선택하거나 프로젝트를 마우스 오른쪽 단추로 클릭하고 **프로젝트 언로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f8e34-146">From the **Project** menu, choose **Unload Project** (or right-click the project and choose **Unload Project**).</span></span>

   <span data-ttu-id="f8e34-147">이 프로젝트의 경우 프로젝트 파일에 SDK 특성이 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f8e34-147">This project will not include the SDK attribute in the project file.</span></span> <span data-ttu-id="f8e34-148">SDK 스타일 프로젝트가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="f8e34-148">It is not an SDK-style project.</span></span>

   ![프로젝트 언로드](media/unload-project.png)

   <span data-ttu-id="f8e34-150">그런 다음, 언로드된 프로젝트를 마우스 오른쪽 단추로 클릭하고 **myprojectname.csproj 편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f8e34-150">Then, right-click the unloaded project and choose **Edit myprojectname.csproj**.</span></span>

## <a name="see-also"></a><span data-ttu-id="f8e34-151">참고 항목</span><span class="sxs-lookup"><span data-stu-id="f8e34-151">See also</span></span>

- [<span data-ttu-id="f8e34-152">dotnet CLI를 사용하여 .NET Standard 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="f8e34-152">Create .NET Standard Packages with dotnet CLI</span></span>](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)
- [<span data-ttu-id="f8e34-153">Visual Studio를 사용하여 .NET Standard 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="f8e34-153">Create .NET Standard Packages with Visual Studio</span></span>](../quickstart/create-and-publish-a-package-using-visual-studio.md)
- [<span data-ttu-id="f8e34-154">.NET Framework 패키지 만들기 및 게시(Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="f8e34-154">Create and publish a .NET Framework package (Visual Studio)</span></span>](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md)
- [<span data-ttu-id="f8e34-155">MSBuild 대상으로서의 NuGet pack 및 restore</span><span class="sxs-lookup"><span data-stu-id="f8e34-155">NuGet pack and restore as MSBuild targets</span></span>](../reference/msbuild-targets.md)
