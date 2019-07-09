---
title: 프로젝트에서 참조하는 어셈블리 선택
description: 모든 어셈블리를 런타임에 사용할 수 있는 동안 패키지의 어셈블리 하위 집합을 컴파일러에서 사용할 수 있도록 합니다.
author: zivkan
ms.author: zivkan
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: b32075c3f2c06c15c07d36602bdabdaee8b9405a
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427478"
---
# <a name="select-assemblies-referenced-by-projects"></a><span data-ttu-id="037ca-103">프로젝트에서 참조하는 어셈블리 선택</span><span class="sxs-lookup"><span data-stu-id="037ca-103">Select Assemblies Referenced By Projects</span></span>

<span data-ttu-id="037ca-104">모든 어셈블리를 런타임에 사용할 수 있는 동안 명시적 어셈블리 참조는 IntelliSense 및 컴파일에 사용되는 어셈블리의 하위 집합을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="037ca-104">Explicit assembly references allows a subset of assemblies to be used for IntelliSense and compiling, while all assemblies are available at run-time.</span></span> <span data-ttu-id="037ca-105">`PackageReference` 및 `packages.config`는 다르게 작동하며, 결과적으로 패키지 작성자는 두 프로젝트 유형 모두와 호환되도록 패키지를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="037ca-105">`PackageReference` and `packages.config` work differently, and as a result package authors need to take care to create the package to be compatible with both project types.</span></span>

> [!Note]
> <span data-ttu-id="037ca-106">명시적 어셈블리 참조는 .NET 어셈블리와 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="037ca-106">Explicit assembly references are related to .NET assemblies.</span></span> <span data-ttu-id="037ca-107">관리 어셈블리에 의해 P/호출된 네이티브 어셈블리를 배포하는 메서드가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="037ca-107">It is not a method to distribute native assemblies that are P/Invoked by a managed assembly.</span></span>

## <a name="packagereference-support"></a><span data-ttu-id="037ca-108">`PackageReference` 지원</span><span class="sxs-lookup"><span data-stu-id="037ca-108">`PackageReference` support</span></span>

<span data-ttu-id="037ca-109">프로젝트가 `PackageReference`가 있는 패키지를 사용하고 패키지에 `ref\<tfm>\` 디렉터리가 포함된 경우, NuGet은 해당 어셈블리를 컴파일 타임 자산으로 분류하고 `lib\<tfm>\` 어셈블리는 런타임 자산으로 분류합니다.</span><span class="sxs-lookup"><span data-stu-id="037ca-109">When a project uses a package with `PackageReference` and the package contains a `ref\<tfm>\` directory, NuGet will classify those assembles as compile-time assets, while the `lib\<tfm>\` assemblies are classified as runtime assets.</span></span> <span data-ttu-id="037ca-110">`ref\<tfm>\`의 어셈블리는 런타임 시 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="037ca-110">Assemblies in `ref\<tfm>\` are not used at runtime.</span></span> <span data-ttu-id="037ca-111">즉, `ref\<tfm>\`의 모든 어셈블리에는 `lib\<tfm>\` 또는 관련 `runtime\` 디렉터리에 일치하는 어셈블리가 있어야 합니다. 그렇지 않으면 런타임 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="037ca-111">This means it is necessary for any assembly in `ref\<tfm>\` to have a matching assembly in either `lib\<tfm>\` or a relevant `runtime\` directory, otherwise runtime errors will likely occur.</span></span> <span data-ttu-id="037ca-112">`ref\<tfm>\`의 어셈블리는 런타임에 사용되지 않으므로 패키지 크기를 줄이기 위한 [메타데이터 전용 어셈블리](https://github.com/dotnet/roslyn/blob/master/docs/features/refout.md)일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="037ca-112">Since assemblies in `ref\<tfm>\` are not used at runtime, they may be [metadata-only assemblies](https://github.com/dotnet/roslyn/blob/master/docs/features/refout.md) to reduce package size.</span></span>

> [!Important]
> <span data-ttu-id="037ca-113">패키지에 nuspec `<references>` 요소(`packages.config`에서 사용됨, 아래 참조)가 있고 `ref\<tfm>\`의 어셈블리가 포함되어 있지 않은 경우, NuGet은 nuspec `<references>` 요소에 나열된 어셈블리를 컴파일 및 런타임 자산으로 보급합니다.</span><span class="sxs-lookup"><span data-stu-id="037ca-113">If a package contains the nuspec `<references>` element (used by `packages.config`, see below) and does not contain assemblies in `ref\<tfm>\`, NuGet will advertise the assemblies listed in the nuspec `<references>` element as both the compile and runtime assets.</span></span> <span data-ttu-id="037ca-114">이는 참조된 어셈블리가 `lib\<tfm>\` 디렉터리에 다른 어셈블리를 로드해야 하는 경우 런타임 예외가 있음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="037ca-114">This means there will be runtime exceptions when the referenced assemblies need to load any other assembly in the `lib\<tfm>\` directory.</span></span>

> [!Note]
> <span data-ttu-id="037ca-115">패키지에 `runtime\` 디렉터리가 포함된 경우 NuGet은 `lib\` 디렉터리의 자산을 사용하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="037ca-115">If the package contains a `runtime\` directory, NuGet may not use the assets in the `lib\` directory.</span></span>

## <a name="packagesconfig-support"></a><span data-ttu-id="037ca-116">`packages.config` 지원</span><span class="sxs-lookup"><span data-stu-id="037ca-116">`packages.config` support</span></span>

<span data-ttu-id="037ca-117">`packages.config`를 사용하여 NuGet 패키지를 관리하는 프로젝트는 일반적으로 `lib\<tfm>\` 디렉터리의 모든 어셈블리에 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="037ca-117">Projects using `packages.config` to manage NuGet packages normally add references to all assemblies in the `lib\<tfm>\` directory.</span></span> <span data-ttu-id="037ca-118">`ref\` 디렉터리는 `PackageReference`를 지원하기 위해 추가되었으므로 `packages.config` 사용 시 고려되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="037ca-118">The `ref\` directory was added to support `PackageReference` and therefore isn't considered when using `packages.config`.</span></span> <span data-ttu-id="037ca-119">`packages.config`를 사용하는 프로젝트에 대해 참조되는 어셈블리를 명시적으로 설정하려면 패키지에서 [nuspec 파일의 `<references>` 요소](../reference/nuspec.md#explicit-assembly-references)를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="037ca-119">To explicitly set which assemblies are referenced for projects using `packages.config`, the package must use the [`<references>` element in the nuspec file](../reference/nuspec.md#explicit-assembly-references).</span></span> <span data-ttu-id="037ca-120">예:</span><span class="sxs-lookup"><span data-stu-id="037ca-120">For example:</span></span>

```xml
<references>
    <group targetFramework="net45">
        <reference file="MyLibrary.dll" />
    </group>
</references>
```

> [!Note]
> <span data-ttu-id="037ca-121">`packages.config` 프로젝트는 [ResolveAssemblyReference](https://github.com/Microsoft/msbuild/blob/master/documentation/wiki/ResolveAssemblyReference.md)라는 프로세스를 사용하여 어셈블리를 `bin\<configuration>\` 출력 디렉터리에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="037ca-121">`packages.config` project use a process called [ResolveAssemblyReference](https://github.com/Microsoft/msbuild/blob/master/documentation/wiki/ResolveAssemblyReference.md) to copy assemblies to the `bin\<configuration>\` output directory.</span></span> <span data-ttu-id="037ca-122">프로젝트의 어셈블리가 복사된 다음, 빌드 시스템이 참조된 어셈블리에 대한 어셈블리 매니페스트를 살펴본 후, 해당 어셈블리를 복사하고 모든 어셈블리에 대해 재귀적으로 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="037ca-122">Your project's assembly is copied, then the build system looks at the assembly manifest for referenced assemblies, then copies those assemblies and recursively repeats for all assemblies.</span></span> <span data-ttu-id="037ca-123">즉, `lib\<tfm>\` 디렉터리에 있는 어셈블리가 다른 어셈블리의 매니페스트에 종속성으로 나열되지 않은 경우(`Assembly.Load`, MEF 또는 다른 종속성 주입 프레임워크를 사용하여 런타임 시 어셈블리가 로드된 경우), `bin\<tfm>\`에 있더라도 프로젝트의 `bin\<configuration>\` 출력 디렉터리에 복사되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="037ca-123">This means that if any of the assemblies in your `lib\<tfm>\` directory are not listed in any other assembly's manifest as a dependency (if the assembly is loaded at runtime using `Assembly.Load`, MEF or another dependency injection framework), then it may not be copied to your project's `bin\<configuration>\` output directory despite being in `bin\<tfm>\`.</span></span>

## <a name="example"></a><span data-ttu-id="037ca-124">예</span><span class="sxs-lookup"><span data-stu-id="037ca-124">Example</span></span>

<span data-ttu-id="037ca-125">내 패키지에는 .NET Framework 4.7.2를 대상으로 하는 세 개의 어셈블리 `MyLib.dll`, `MyHelpers.dll` 및 `MyUtilities.dll`이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="037ca-125">My package will contain three assemblies, `MyLib.dll`, `MyHelpers.dll` and `MyUtilities.dll`, which are targeting the .NET Framework 4.7.2.</span></span> <span data-ttu-id="037ca-126">`MyUtilities.dll`에는 다른 두 어셈블리에서만 사용할 수 있는 클래스가 포함되어 있으므로 IntelliSense에서 또는 패키지를 사용하여 프로젝트를 컴파일할 때 해당 클래스를 사용할 수 없도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="037ca-126">`MyUtilities.dll` contains classes intended to be used only by the other two assemblies, so I don't want to make those classes available in IntelliSense or at compile time to projects using my package.</span></span> <span data-ttu-id="037ca-127">내 `nuspec` 파일에 다음 XML 요소가 포함되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="037ca-127">My `nuspec` file needs to contain the following XML elements:</span></span>

```xml
<references>
    <group targetFramework="net472">
        <reference file="MyLib.dll" />
        <reference file="MyHelpers.dll" />
    </group>
</references>
```

<span data-ttu-id="037ca-128">패키지의 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="037ca-128">and the files in the package will be:</span></span>

```text
lib\net472\MyLib.dll
lib\net472\MyHelpers.dll
lib\net472\MyUtilities.dll
ref\net472\MyLib.dll
ref\net472\MyHelpers.dll
```
