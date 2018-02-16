---
title: "지역화된 NuGet 패키지를 만드는 방법 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "단일 패키지에서 모든 어셈블리를 포함하거나 별도 어셈블리를 게시하여 지역화된 NuGet 패키지를 만드는 두 가지 방법에 대한 자세한 내용입니다."
keywords: "NuGet 패키지 지역화, NuGet 위성 어셈블리, 지역화된 패키지 만들기, NuGet 지역화 규칙"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 1ce8cff07bf629fcdeeaace901a185f2446b077a
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/14/2018
---
# <a name="creating-localized-nuget-packages"></a><span data-ttu-id="7a8b5-104">지역화된 NuGet 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="7a8b5-104">Creating localized NuGet packages</span></span>

<span data-ttu-id="7a8b5-105">두 가지 방법으로 라이브러리의 지역화된 버전을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-105">There are two ways to create localized versions of a library:</span></span>

1. <span data-ttu-id="7a8b5-106">단일 패키지에 모든 지역화된 리소스 어셈블리를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-106">Include all localized resources assemblies in a single package.</span></span>
1. <span data-ttu-id="7a8b5-107">엄격한 규칙 집합에 따라 별도의 지역화된 위성 패키지(NuGet 1.8 이상)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-107">Create separate localized satellite packages (NuGet 1.8 and later), by following a strict set of conventions.</span></span>

<span data-ttu-id="7a8b5-108">두 방법에는 다음 섹션에서 설명된 장점과 단점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-108">Both methods have their advantages and disadvantages, as described in the following sections.</span></span>

## <a name="localized-resource-assemblies-in-a-single-package"></a><span data-ttu-id="7a8b5-109">단일 패키지의 모든 지역화된 리소스 어셈블리</span><span class="sxs-lookup"><span data-stu-id="7a8b5-109">Localized resource assemblies in a single package</span></span>

<span data-ttu-id="7a8b5-110">단일 패키지에서 지역화된 리소스 어셈블리를 포함하는 작업은 일반적으로 가장 단순한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-110">Including localized resource assemblies in a single package is typically the simplest approach.</span></span> <span data-ttu-id="7a8b5-111">이렇게 하려면 패키지 기본값 이외의 지원되는 언어에서 `lib` 내에 폴더를 만듭니다(en-us로 간주).</span><span class="sxs-lookup"><span data-stu-id="7a8b5-111">To do this, create folders within `lib` for supported language other than the package default (assumed to be en-us).</span></span> <span data-ttu-id="7a8b5-112">이러한 폴더에 리소스 어셈블리와 지역화된 IntelliSense XML 파일을 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-112">In these folders you can place resource assemblies and localized IntelliSense XML files.</span></span>

<span data-ttu-id="7a8b5-113">예를 들어 다음 폴더 구조는 독일어(de), 이탈리아어(it), 일본어(ja), 러시아어(ru), 중국어(간체)(zh-Hans) 및 중국어(번체)(zh-Hant)를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-113">For example, the following folder structure supports, German (de), Italian (it), Japanese (ja), Russian (ru), Chinese (Simplified) (zh-Hans), and Chinese (Traditional) (zh-Hant):</span></span>

    lib
    └───net40
        │   Contoso.Utilities.dll
        │   Contoso.Utilities.xml
        │
        ├───de
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───it
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───ja
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───ru
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───zh-Hans
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        └───zh-Hant
                Contoso.Utilities.resources.dll
                Contoso.Utilities.xml

<span data-ttu-id="7a8b5-114">언어가 모두 `net40` 대상 프레임워크 폴더 아래에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-114">You can see that the languages are all listed underneath the `net40` target framework folder.</span></span> <span data-ttu-id="7a8b5-115">사용자가 [여러 프레임워크를 지원하는](../create-packages/supporting-multiple-target-frameworks.md) 경우 `lib` 아래에 각 변형에 대한 폴더가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-115">If you're [supporting multiple frameworks](../create-packages/supporting-multiple-target-frameworks.md), then you have a folder under `lib` for each variant.</span></span>

<span data-ttu-id="7a8b5-116">이러한 폴더가 준비되면 `.nuspec`에 있는 모든 파일을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-116">With these folders in place, you then reference all the files in your `.nuspec`:</span></span>

```xml
<?xml version="1.0"?>
<package>
    <metadata>...
    </metadata>
    <files>
    <file src="lib\**" target="lib" />
    </files>
</package>
```

<span data-ttu-id="7a8b5-117">이 방법을 사용하는 하나의 예제 패키지는 [Microsoft.Data.OData 5.4.0](http://nuget.org/packages/Microsoft.Data.OData/5.4.0)입니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-117">One example package that uses this approach is [Microsoft.Data.OData 5.4.0](http://nuget.org/packages/Microsoft.Data.OData/5.4.0).</span></span>

### <a name="advantages-and-disadvantages-localized-resource-assemblies"></a><span data-ttu-id="7a8b5-118">장점 및 단점(지역화된 리소스 어셈블리)</span><span class="sxs-lookup"><span data-stu-id="7a8b5-118">Advantages and disadvantages (localized resource assemblies)</span></span>

<span data-ttu-id="7a8b5-119">단일 패키지에서 모든 언어를 번들하면 몇 가지 단점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-119">Bundling all languages in a single package has a few disadvantages:</span></span>

1. <span data-ttu-id="7a8b5-120">**공유 메타데이터**: NuGet 패키지에 단일 `.nuspec` 파일만이 포함될 수 있기 때문에 단일 언어에 대한 메타데이터를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-120">**Shared metadata**: Because a NuGet package can only contain a single `.nuspec` file, you can provide metadata for only a single language.</span></span> <span data-ttu-id="7a8b5-121">즉, NuGet에서는 지역화된 메타데이터를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-121">That is, NuGet does not present support localized metadata.</span></span>
1. <span data-ttu-id="7a8b5-122">**패키지 크기**: 지원하는 언어 수에 따라 라이브러리는 상당히 커질 수 있습니다. 그러면 패키지를 설치하고 복원하는 작업이 느려집니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-122">**Package size**: Depending on the number of languages you support, the library can become considerably large, which slows installing and restoring the package.</span></span>
1. <span data-ttu-id="7a8b5-123">**동시 릴리스**: 지역화된 파일을 단일 패키지로 번들하려면 각 지역화를 개별적으로 릴리스하는 대신 해당 패키지에 있는 모든 자산을 동시에 릴리스해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-123">**Simultaneous releases**: Bundling localized files into a single package requires that you release all assets in that package simultaneously, rather than being able to release each localization separately.</span></span> <span data-ttu-id="7a8b5-124">또한 하나의 지역화에 대한 업데이트에는 새 버전의 전체 패키지가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-124">Furthermore, any update to any one localization requires a new version of the entire package.</span></span>

<span data-ttu-id="7a8b5-125">그러나 몇 가지 이점도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-125">However, it also has a few benefits:</span></span>

1. <span data-ttu-id="7a8b5-126">**단순성**: 패키지의 소비자가 각 언어를 별도로 설치하는 것이 아니라 단일 설치에서 지원되는 모든 언어를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-126">**Simplicity**: Consumers of the package get all supported languages in a single install, rather than having to install each language separately.</span></span> <span data-ttu-id="7a8b5-127">단일 패키지를 nuget.org에서 쉽게 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-127">A single package is also easier to find on nuget.org.</span></span>
1. <span data-ttu-id="7a8b5-128">**결합 버전**: 모든 리소스 어셈블리가 기본 어셈블리와 동일한 패키지에 있기 때문에 동일한 버전 번호를 공유하고 잘못 분리될 위험성이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-128">**Coupled versions**: Because all of the resource assemblies are in the same package as the primary assembly, they all share the same version number and don't run a risk of getting erroneously decoupled.</span></span>

## <a name="localized-satellite-packages"></a><span data-ttu-id="7a8b5-129">지역화된 위성 패키지</span><span class="sxs-lookup"><span data-stu-id="7a8b5-129">Localized satellite packages</span></span>

<span data-ttu-id="7a8b5-130">.NET Framework에서 위성 어셈블리를 지원하는 방법과 마찬가지로 이 메서드는 지역화된 리소스 및 IntelliSense XML 파일을 위성 패키지로 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-130">Similar to how .NET Framework supports satellite assemblies, this method separates localized resources and IntelliSense XML files into satellite packages.</span></span>

<span data-ttu-id="7a8b5-131">이렇게 하려면 기본 패키지는 `{identifier}.{version}.nupkg` 명명 규칙을 사용하고 기본 언어(예: en-US)에 대한 어셈블리를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-131">Do to this, your primary package uses the naming convention `{identifier}.{version}.nupkg` and contains the assembly for the default language (such as en-US).</span></span> <span data-ttu-id="7a8b5-132">예를 들어 `ContosoUtilities.1.0.0.nupkg`에는 다음과 같은 구조가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-132">For example, `ContosoUtilities.1.0.0.nupkg` would contain the following structure:</span></span>

    lib
    └───net40
            ContosoUtilities.dll
            ContosoUtilities.xml

<span data-ttu-id="7a8b5-133">그런 다음 위성 어셈블리는 `{identifier}.{language}.{version}.nupkg` 명명 규칙(예: `ContosoUtilities.de.1.0.0.nupkg`)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-133">A satellite assembly then uses the naming convention `{identifier}.{language}.{version}.nupkg`, such as `ContosoUtilities.de.1.0.0.nupkg`.</span></span> <span data-ttu-id="7a8b5-134">식별자는 기본 패키지의 식별자와 정확하게 일치**해야** 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-134">The identifier **must** exactly match that of the primary package.</span></span>

<span data-ttu-id="7a8b5-135">이것이 별도 패키지이기 때문에 지역화된 메타데이터가 포함된 고유의 `.nuspec` 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-135">Because this is a separate package, it has its own `.nuspec` file that contains localized metadata.</span></span> <span data-ttu-id="7a8b5-136">`.nuspec`의 언어는 파일 이름에서 사용되는 언어와 일치**해야** 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-136">Be mindful that the language in the `.nuspec` **must** match the one used in the filename.</span></span>

<span data-ttu-id="7a8b5-137">또한 위성 어셈블리는 [] 버전 표기법을 사용하여 정확한 버전의 기본 패키지를 종속성으로 선언**해야** 합니다([패키지 버전 관리](../reference/package-versioning.md) 참조).</span><span class="sxs-lookup"><span data-stu-id="7a8b5-137">The satellite assembly **must** also declare an exact version of the primary package as a dependency, using the [] version notation (see [Package versioning](../reference/package-versioning.md)).</span></span> <span data-ttu-id="7a8b5-138">예를 들어 `ContosoUtilities.de.1.0.0.nupkg`는 `ContosoUtilities.1.0.0.nupkg`에서 `[1.0.0]` 표기법을 사용하여 종속성을 선언해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-138">For example, `ContosoUtilities.de.1.0.0.nupkg` must declare a dependency on `ContosoUtilities.1.0.0.nupkg` using the `[1.0.0]` notation.</span></span> <span data-ttu-id="7a8b5-139">물론 위성 패키지에는 기본 패키지와 다른 버전 번호가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-139">The satellite package can, of course, have a different version number than the primary package.</span></span>

<span data-ttu-id="7a8b5-140">그런 다음 위성 패키지의 구조에는 패키지 파일 이름에서 `{language}`와 일치하는 하위 폴더에 있는 리소스 어셈블리 및 XML IntelliSense 파일이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-140">The satellite package's structure must then include the resource assembly and XML IntelliSense file in a subfolder that matches `{language}` in the package filename:</span></span>

    lib
    └───net40
        └───de
                ContosoUtilities.resources.dll
                ContosoUtilities.xml

<span data-ttu-id="7a8b5-141">**참고**: `ja-JP`와 같은 특정 하위 문화권이 필요하지 않으면 항상 `ja`와 같은 개략적인 언어 식별자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-141">**Note**: unless specific subcultures such as `ja-JP` are necessary, always use the higher level language identifier, like `ja`.</span></span>

<span data-ttu-id="7a8b5-142">위성 어셈블리에서 NuGet은 파일 이름에서 `{language}`와 일치하는 해당 폴더에 있는 해당 파일**만**을 인식합니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-142">In a satellite assembly, NuGet will recognize **only** those files in the folder that matches the `{language}` in the filename.</span></span> <span data-ttu-id="7a8b5-143">다른 특성은 모두 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-143">All others are ignored.</span></span>

<span data-ttu-id="7a8b5-144">이러한 규칙을 모두 충족할 경우 NuGet은 패키지를 위성 패키지로 인식하고, 원래 번들되었던 것처럼 기본 패키지의 `lib` 폴더에 지역화된 파일을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-144">When all of these conventions are met, NuGet will recognize the package as a satellite package and install the localized files into the primary package's `lib` folder, as if they had been originally bundled.</span></span> <span data-ttu-id="7a8b5-145">위성 패키지를 제거하면 동일한 폴더에서 해당 파일이 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-145">Uninstalling the satellite package will remove its files from that same folder.</span></span>

<span data-ttu-id="7a8b5-146">지원되는 각 언어에 대해 같은 방법으로 추가 위성 어셈블리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-146">You would create additional satellite assemblies in the same way for each supported language.</span></span> <span data-ttu-id="7a8b5-147">예를 들어 ASP.NET MVC 패키지 집합을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-147">For an example, examine the set of ASP.NET MVC packages:</span></span>

- <span data-ttu-id="7a8b5-148">[Microsoft.AspNet.Mvc](http://nuget.org/packages/Microsoft.AspNet.Mvc)(영어 기본)</span><span class="sxs-lookup"><span data-stu-id="7a8b5-148">[Microsoft.AspNet.Mvc](http://nuget.org/packages/Microsoft.AspNet.Mvc) (English primary)</span></span>
- <span data-ttu-id="7a8b5-149">[Microsoft.AspNet.Mvc.de](http://nuget.org/packages/Microsoft.AspNet.Mvc.de)(독일어)</span><span class="sxs-lookup"><span data-stu-id="7a8b5-149">[Microsoft.AspNet.Mvc.de](http://nuget.org/packages/Microsoft.AspNet.Mvc.de) (German)</span></span>
- <span data-ttu-id="7a8b5-150">[Microsoft.AspNet.Mvc.ja](http://nuget.org/packages/Microsoft.AspNet.Mvc.ja)(일본어)</span><span class="sxs-lookup"><span data-stu-id="7a8b5-150">[Microsoft.AspNet.Mvc.ja](http://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (Japanese)</span></span>
- <span data-ttu-id="7a8b5-151">[Microsoft.AspNet.Mvc.zh-Hans](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans)(중국어(간체))</span><span class="sxs-lookup"><span data-stu-id="7a8b5-151">[Microsoft.AspNet.Mvc.zh-Hans](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (Chinese (Simplified))</span></span>
- <span data-ttu-id="7a8b5-152">[Microsoft.AspNet.Mvc.zh-Hant](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant)(중국어(번체))</span><span class="sxs-lookup"><span data-stu-id="7a8b5-152">[Microsoft.AspNet.Mvc.zh-Hant](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (Chinese (Traditional))</span></span>

### <a name="summary-of-required-conventions"></a><span data-ttu-id="7a8b5-153">필수 규칙 요약</span><span class="sxs-lookup"><span data-stu-id="7a8b5-153">Summary of required conventions</span></span>

- <span data-ttu-id="7a8b5-154">기본 패키지 이름을 `{identifier}.{version}.nupkg`로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-154">Primary package must be named `{identifier}.{version}.nupkg`</span></span>
- <span data-ttu-id="7a8b5-155">위성 패키지 이름을 `{identifier}.{language}.{version}.nupkg`로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-155">A satellite package must be named `{identifier}.{language}.{version}.nupkg`</span></span>
- <span data-ttu-id="7a8b5-156">위성 패키지의 `.nuspec`는 파일 이름에 맞는 해당 언어를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-156">A satellite package's `.nuspec` must specify its language to match the filename.</span></span>
- <span data-ttu-id="7a8b5-157">위성 패키지는 해당 `.nuspec` 파일에서 [] 표기법을 사용하여 정확한 버전의 기본 패키지에서 종속성을 선언해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-157">A satellite package must declare a dependency on an exact version of the primary using the [] notation in its `.nuspec` file.</span></span> <span data-ttu-id="7a8b5-158">범위는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-158">Ranges are not supported.</span></span>
- <span data-ttu-id="7a8b5-159">위성 패키지는 파일 이름에서 `{language}`와 정확히 일치하는 `lib\[{framework}\]{language}` 폴더에 파일을 배치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-159">A satellite package must place files in the `lib\[{framework}\]{language}` folder that exactly matches `{language}` in the filename.</span></span>

### <a name="advantages-and-disadvantages-satellite-packages"></a><span data-ttu-id="7a8b5-160">장점 및 단점(위성 패키지)</span><span class="sxs-lookup"><span data-stu-id="7a8b5-160">Advantages and disadvantages (satellite packages)</span></span>

<span data-ttu-id="7a8b5-161">위성 패키지를 사용하면 몇 가지 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-161">Using satellite packages has a few benefits:</span></span>

1. <span data-ttu-id="7a8b5-162">**패키지 크기**: 기본 패키지의 전체 공간을 최소화하며 소비자는 사용하려는 언어의 비용만을 지불합니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-162">**Package size**: The overall footprint of the primary package is minimized, and consumers only incur the costs of each language they want to use.</span></span>
1. <span data-ttu-id="7a8b5-163">**별도 메타데이터**: 각 위성 패키지에는 고유의 `.nuspec` 파일이 있으므로 고유의 지역화된 메타데이터도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-163">**Separate metadata**: Each satellite package has its own `.nuspec` file and thus its own localized metadata because.</span></span> <span data-ttu-id="7a8b5-164">따라서 일부 소비자는 지역화된 단어를 포함한 nuget.org를 검색하여 패키지를 보다 쉽게 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-164">This can allow some consumers to find packages more easily by searching nuget.org with localized terms.</span></span>
1. <span data-ttu-id="7a8b5-165">**릴리스 분리**: 위성 어셈블리는 한 번이 아니라 시간이 지남에 따라 릴리스될 수 있으며 이를 통해 지역화 작업을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-165">**Decoupled releases**: Satellite assemblies can be released over time, rather than all at once, allowing you to spread out your localization efforts.</span></span>

<span data-ttu-id="7a8b5-166">그러나 위성 패키지에는 각자 단점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-166">However, satellite packages have their own set of disadvantages:</span></span>

1. <span data-ttu-id="7a8b5-167">**잡동사니**: 단일 패키지 대신 nuget.org에서 복잡한 검색 결과 및 Visual Studio 프로젝트에서 긴 참조 목록을 초래할 수 있는 많은 패키지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-167">**Clutter**: Instead of a single package, you have many packages that can lead to cluttered search results on nuget.org and a long list of references in a Visual Studio project.</span></span>
1. <span data-ttu-id="7a8b5-168">**엄격한 규칙**</span><span class="sxs-lookup"><span data-stu-id="7a8b5-168">**Strict conventions**.</span></span> <span data-ttu-id="7a8b5-169">위성 패키지가 규칙을 정확하게 따르지 않으면 적합한 지역화된 버전을 선택할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-169">Satellite packages must follow the conventions exactly or the localized versions won't be picked up properly.</span></span>
1. <span data-ttu-id="7a8b5-170">**버전 관리**: 각 위성 패키지에는 기본 패키지에 대한 정확한 버전 종속성이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-170">**Versioning**: Each satellite package must have an exact version dependency on the primary package.</span></span> <span data-ttu-id="7a8b5-171">즉, 기본 패키지를 업데이트하면 리소스가 변경되지 않은 경우에도 모든 위성 패키지를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a8b5-171">This means that updating the primary package may require updating all satellite packages as well, even if the resources didn't change.</span></span>
