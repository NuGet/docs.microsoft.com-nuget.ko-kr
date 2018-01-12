---
title: "Visual Studio 프로젝트 시스템에 대한 NuGet 지원 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 9d7fa7f6-82ed-4df6-9734-f43a3d8e3b98
description: "타사 프로젝트 형식에서 Visual Studio 프로젝트 시스템에 NuGet을 통합합니다."
keywords: "Visual Studio의 NuGet, 프로젝트 형식 사용자 지정, Visual Studio 프로젝트"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 9c8cad46f18578bec41bd9280985e42972a9b3c1
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/05/2018
---
# <a name="nuget-support-for-the-visual-studio-project-system"></a><span data-ttu-id="068a0-104">Visual Studio 프로젝트 시스템에 대한 NuGet 지원</span><span class="sxs-lookup"><span data-stu-id="068a0-104">NuGet support for the Visual Studio project system</span></span>

<span data-ttu-id="068a0-105">Visual Studio에서 타사 프로젝트 형식을 지원하려면 NuGet 3.x 이상이 [CPS(일반 프로젝트 시스템)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md)을 지원하고 NuGet 3.2 이상이 비 CPS 프로젝트 시스템을 지원해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="068a0-105">To support third-party project types in Visual Studio, NuGet 3.x+ supports the [Common Project System (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md), and NuGet 3.2+ supports non-CPS project systems as well.</span></span>

<span data-ttu-id="068a0-106">NuGet과 통합하려면 프로젝트 시스템은 이 항목에서 설명된 모든 프로젝트 기능에 대한 고유한 지원을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="068a0-106">To integrate with NuGet, a project system must advertise its own support for all the project capabilities described in this topic.</span></span>


> [!NOTE]
> <span data-ttu-id="068a0-107">프로젝트에서 설치할 패키지를 사용하기 위해 프로젝트에 실제로 없는 기능을 선언하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="068a0-107">Do not declare capabilities that your project does not actually have for the sake of enabling packages to install in your project.</span></span> <span data-ttu-id="068a0-108">Visual Studio 및 기타 확장명의 여러 기능은 NuGet 클라이언트 외에도 프로젝트 기능에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="068a0-108">Many features of Visual Studio and other extensions depend on project capabilities besides the NuGet client.</span></span> <span data-ttu-id="068a0-109">프로젝트의 기능을 거짓으로 보급하면 이러한 구성 요소에 오작동이 발생하고 사용자의 환경이 저하될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="068a0-109">Falsely advertising capabilities of your project can lead these components to malfunction and your users' experience to degrade.</span></span>

## <a name="advertise-project-capabilities"></a><span data-ttu-id="068a0-110">프로젝트 기능 보급</span><span class="sxs-lookup"><span data-stu-id="068a0-110">Advertise project capabilities</span></span>

<span data-ttu-id="068a0-111">NuGet 클라이언트는 다음 표에 설명된 대로 [프로젝트의 기능](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md)에 따라 프로젝트 형식과 호환 가능한 패키지를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="068a0-111">The NuGet client determines which packages are compatible with your project type based on the [project's capabilities](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), as described in the following table.</span></span>


|<span data-ttu-id="068a0-112">기능</span><span class="sxs-lookup"><span data-stu-id="068a0-112">Capability</span></span>|<span data-ttu-id="068a0-113">설명</span><span class="sxs-lookup"><span data-stu-id="068a0-113">Description</span></span>|
|----------------|-----------|
|<span data-ttu-id="068a0-114">AssemblyReferences</span><span class="sxs-lookup"><span data-stu-id="068a0-114">AssemblyReferences</span></span>|<span data-ttu-id="068a0-115">프로젝트가 어셈블리 참조를 지원함을 나타냅니다(WinRTReferences와 구별).</span><span class="sxs-lookup"><span data-stu-id="068a0-115">Indicates that the project supports assembly references (distinct from WinRTReferences)</span></span>|
|<span data-ttu-id="068a0-116">DeclaredSourceItems</span><span class="sxs-lookup"><span data-stu-id="068a0-116">DeclaredSourceItems</span></span>|<span data-ttu-id="068a0-117">프로젝트가 (폴더의 모든 파일을 컴파일의 일부로 가정하는 `project.json` 파일이 아닌) 프로젝트 자체에서 소스 항목을 선언하는 (DNX가 아닌) 일반적인 MSBuild 프로젝트임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="068a0-117">Indicates that the project is a typical MSBuild project (not DNX) in that it declares source items in the project itself (rather than a `project.json` file that assumes all files in the folder are part of a compilation).</span></span>|
|<span data-ttu-id="068a0-118">UserSourceItems</span><span class="sxs-lookup"><span data-stu-id="068a0-118">UserSourceItems</span></span>|<span data-ttu-id="068a0-119">사용자가 해당 프로젝트에 임의 파일을 추가할 수 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="068a0-119">Indicates that the user is allowed to add arbitrary files to their project.</span></span>|

<span data-ttu-id="068a0-120">CPS 기반 프로젝트 시스템의 경우 이 섹션의 나머지 부분에서 설명한 프로젝트 기능에 대한 구현 세부 사항이 수행되었습니다.</span><span class="sxs-lookup"><span data-stu-id="068a0-120">For CPS-based project systems, the implementation details for project capabilities described in the rest of this section have been done for you.</span></span> <span data-ttu-id="068a0-121">[CPS 프로젝트에서 프로젝트 기능 선언](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="068a0-121">See [declaring project capabilities in CPS projects](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).</span></span>

## <a name="implementing-vsprojectcapabilitiespresencechecker"></a><span data-ttu-id="068a0-122">VsProjectCapabilitiesPresenceChecker 구현</span><span class="sxs-lookup"><span data-stu-id="068a0-122">Implementing VsProjectCapabilitiesPresenceChecker</span></span>

<span data-ttu-id="068a0-123">`VsProjectCapabilitiesPresenceChecker` 클래스는 다음과 같이 정의되는 `IVsBooleanSymbolPresenceChecker` 인터페이스를 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="068a0-123">The `VsProjectCapabilitiesPresenceChecker` class must implement the `IVsBooleanSymbolPresenceChecker` interface, which is defined as follows:</span></span>

```cs
public interface IVsBooleanSymbolPresenceChecker
{
    /// <summary>
    /// Checks whether the symbols defined may have changed since the last time
    /// this method was called.
    /// </summary>
    /// <param name="versionObject">
    /// The response version object assigned at the last call.
    /// May be null to get the initial version.
    /// At the conclusion of this method call, the reference may be changed so that on a subsequent call
    /// we know what version was last observed. The caller should treat this value as an opaque object,
    /// and should not assume any significance from whether the pointer changed or not.
    /// </param>
    /// <returns>
    /// <c>true</c> if the symbols defined may have changed since the last call to this method
    /// or if <paramref name="versionObject"/> was <c>null</c> upon entering this method.
    /// <c>false</c> if the responses would all be the same.
    /// </returns>
    bool HasChangedSince(ref object versionObject);

    /// <summary>
    /// Checks for the presence of a given symbol.
    /// </summary>
    /// <param name="symbol">The symbol to check for.</param>
    /// <returns><c>true</c> if the symbol is present; <c>false</c> otherwise.</returns>
    bool IsSymbolPresent(string symbol);
}
```


<span data-ttu-id="068a0-124">그런 다음 이 인터페이스의 샘플 구현은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="068a0-124">A sample implementation of this interface would then be:</span></span>
    
```cs
class VsProjectCapabilitiesPresenceChecker : IVsBooleanSymbolPresenceChecker
{
    /// <summary>
    /// The set of capabilities this project system actually has.
    /// This should be kept current, and honestly reflect what the project can do.
    /// </summary>
    private static readonly HashSet<string> ActualProjectCapabilities = new HashSet<string>(StringComparer.OrdinalIgnoreCase)
        {
            "AssemblyReferences",
            "DeclaredSourceItems",
            "UserSourceItems",
        };

    public bool HasChangedSince(ref object versionObject)
    {
        // If your project capabilities do not change over time while the project is open,
        // you may simply `return false;` from your `HasChangedSince` method.
        return false;
    }

    public bool IsSymbolPresent(string symbol)
    {
        return ActualProjectCapabilities.Contains(symbol);
    }
}
```

<span data-ttu-id="068a0-125">프로젝트 시스템이 실제로 지원하는 기능에 따라 `ActualProjectCapabilities` 집합에서 기능을 추가/제거합니다.</span><span class="sxs-lookup"><span data-stu-id="068a0-125">Remember to add/remove capabilities from the `ActualProjectCapabilities` set based on what your project system actually supports.</span></span> <span data-ttu-id="068a0-126">자세한 설명은 [프로젝트 기능 설명서](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="068a0-126">See the [project capabilities documentation](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) for full descriptions.</span></span>

## <a name="responding-to-queries"></a><span data-ttu-id="068a0-127">쿼리에 응답</span><span class="sxs-lookup"><span data-stu-id="068a0-127">Responding to queries</span></span>

<span data-ttu-id="068a0-128">프로젝트는 `IVsHierarchy::GetProperty`를 통해 `VSHPROPID_ProjectCapabilitiesChecker` 속성을 지원하여 이 기능을 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="068a0-128">A project declares this capability by supporting the  `VSHPROPID_ProjectCapabilitiesChecker` property through the `IVsHierarchy::GetProperty`.</span></span> <span data-ttu-id="068a0-129">`Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` 어셈블리에 정의된 `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`라는 인스턴스를 반환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="068a0-129">It should return an instance of `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, which is defined in the `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` assembly.</span></span> <span data-ttu-id="068a0-130">[NuGet 패키지](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime)를 설치하여 이 어셈블리를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="068a0-130">Reference this assembly by installing the [its NuGet package](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).</span></span>

<span data-ttu-id="068a0-131">예를 들어 다음 `case` 문을 `IVsHierarchy::GetProperty` 메서드의 `switch` 문에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="068a0-131">For example, you might add the following `case` statement to your `IVsHierarchy::GetProperty` method's `switch` statement:</span></span>

```cs
case __VSHPROPID8.VSHPROPID_ProjectCapabilitiesChecker:
    propVal = new VsProjectCapabilitiesPresenceChecker();
    return VSConstants.S_OK;
```

## <a name="dte-support"></a><span data-ttu-id="068a0-132">DTE 지원</span><span class="sxs-lookup"><span data-stu-id="068a0-132">DTE Support</span></span>

<span data-ttu-id="068a0-133">NuGet에서는 프로젝트 시스템을 최상위 Visual Studio 자동화 인터페이스인 [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017)로 호출하여 참조, 콘텐츠 항목 및 MSBuild 가져오기를 추가하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="068a0-133">NuGet drives the project system to add references, content items, and MSBuild imports by calling into [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017), which is the top-level Visual Studio automation interface.</span></span> <span data-ttu-id="068a0-134">DTE는 구현할 수 있는 COM 인터페이스의 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="068a0-134">DTE is a set of COM interfaces that you may already implement.</span></span>

<span data-ttu-id="068a0-135">프로젝트 형식이 CPS에 기반하는 경우 DTE는 자동으로 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="068a0-135">If your project type is based on CPS, DTE is implemented for you.</span></span>
