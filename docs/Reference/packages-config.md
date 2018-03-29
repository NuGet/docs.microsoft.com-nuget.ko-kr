---
title: NuGet packages.config 파일 참조 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: 일부 프로젝트 형식에서 packages.config은 프로젝트에 사용된 NuGet 패키지 목록을 유지 관리합니다.
keywords: NuGet packages.config 파일, NuGet 패키지 참조, NuGet 종속성
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 38d4724d25476d372a936cb8ebf08e2b53fcf9f4
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="packagesconfig-reference"></a><span data-ttu-id="f0efa-104">packages.config 참조</span><span class="sxs-lookup"><span data-stu-id="f0efa-104">packages.config reference</span></span>

<span data-ttu-id="f0efa-105">`packages.config` 파일은 프로젝트에서 참조하는 패키지 목록을 유지하기 위해 일부 프로젝트 형식에서 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f0efa-105">The `packages.config` file is used in some project types to maintain the list of packages referenced by the project.</span></span> <span data-ttu-id="f0efa-106">이를 통해 해당하는 모든 패키지 없이 빌드 서버와 같은 다른 컴퓨터에 NuGet 때 프로젝트를 전송할 때 쉽게 프로젝트의 종속성을 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0efa-106">This allows NuGet to easily restore the project's dependencies when the project to be transported to a different machine, such as a build server, without all those packages.</span></span>

## <a name="schema"></a><span data-ttu-id="f0efa-107">스키마</span><span class="sxs-lookup"><span data-stu-id="f0efa-107">Schema</span></span>

<span data-ttu-id="f0efa-108">스키마는 단순합니다. 다음과 같은 표준 XML 헤더는 각 참조에 하나씩 하나 이상의 `<package>` 요소가 포함된 단일 `<packages>` 노드입니다.</span><span class="sxs-lookup"><span data-stu-id="f0efa-108">The schema is simple: following the standard XML header is a single `<packages>` node that contains one or more `<package>` elements, one for each reference.</span></span> <span data-ttu-id="f0efa-109">각 `<package>` 요소에는 다음과 같은 특성이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0efa-109">Each `<package>` element can have the following attributes:</span></span>

| <span data-ttu-id="f0efa-110">특성</span><span class="sxs-lookup"><span data-stu-id="f0efa-110">Attribute</span></span> | <span data-ttu-id="f0efa-111">필수</span><span class="sxs-lookup"><span data-stu-id="f0efa-111">Required</span></span> | <span data-ttu-id="f0efa-112">설명</span><span class="sxs-lookup"><span data-stu-id="f0efa-112">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f0efa-113">ID</span><span class="sxs-lookup"><span data-stu-id="f0efa-113">id</span></span> | <span data-ttu-id="f0efa-114">예</span><span class="sxs-lookup"><span data-stu-id="f0efa-114">Yes</span></span> | <span data-ttu-id="f0efa-115">Newtonsoft.json 또는 Microsoft.AspNet.Mvc와 같은 패키지의 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="f0efa-115">The identifier of the package, such as Newtonsoft.json or Microsoft.AspNet.Mvc.</span></span> | 
| <span data-ttu-id="f0efa-116">버전</span><span class="sxs-lookup"><span data-stu-id="f0efa-116">version</span></span> | <span data-ttu-id="f0efa-117">예</span><span class="sxs-lookup"><span data-stu-id="f0efa-117">Yes</span></span> | <span data-ttu-id="f0efa-118">3.1.1 또는 4.2.5.11-beta 등 설치할 정확한 버전의 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="f0efa-118">The exact version of the package to install, such as 3.1.1 or 4.2.5.11-beta.</span></span> <span data-ttu-id="f0efa-119">버전 문자열에는 3개 이상의 번호가 있어야 합니다. 네 번째는 시험판 접미사로써 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="f0efa-119">A version string must have at least three numbers; a fourth is optional, as is a pre-release suffix.</span></span> <span data-ttu-id="f0efa-120">범위는 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f0efa-120">Ranges are not allowed.</span></span> | 
| <span data-ttu-id="f0efa-121">targetFramework</span><span class="sxs-lookup"><span data-stu-id="f0efa-121">targetFramework</span></span> | <span data-ttu-id="f0efa-122">아니요</span><span class="sxs-lookup"><span data-stu-id="f0efa-122">No</span></span> | <span data-ttu-id="f0efa-123">패키지를 설치하는 경우 적용할 [TFM(대상 프레임워크 모니커)](target-frameworks.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="f0efa-123">The [target framework moniker (TFM)](target-frameworks.md) to apply when installing the package.</span></span> <span data-ttu-id="f0efa-124">패키지를 설치할 때 처음부터 프로젝트의 대상으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0efa-124">This is initially set to the project's target when a package is installed.</span></span> <span data-ttu-id="f0efa-125">결과적으로 다른 `<package>` 요소에는 다른 TFM가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0efa-125">As a result, different `<package>` elements can have different TFMs.</span></span> <span data-ttu-id="f0efa-126">예를 들어 .NET 4.5.2를 대상으로 하는 프로젝트를 만드는 경우 해당 시점에 설치된 패키지는 net452라는 TFM을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f0efa-126">For example, if you create a project targeting .NET 4.5.2, packages installed at that point will use the TFM of net452.</span></span> <span data-ttu-id="f0efa-127">나중에 프로젝트 대상을 .NET 4.6으로 다시 지정하고 추가 패키지를 추가하는 경우 net46이라는 TFM를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f0efa-127">If you ;later retarget the project to .NET 4.6 and add more packages, those will use TFM of net46.</span></span> <span data-ttu-id="f0efa-128">프로젝트의 대상과 `targetFramework` 특성 간에 불일치는 경고를 생성합니다. 이 경우에 영향을 받는 패키지를 다시 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0efa-128">A mismatch between the project's target and `targetFramework` attributes will generate warnings, in which case you can reinstall the affected packages.</span></span> | 
| <span data-ttu-id="f0efa-129">allowedVersions</span><span class="sxs-lookup"><span data-stu-id="f0efa-129">allowedVersions</span></span> | <span data-ttu-id="f0efa-130">아니요</span><span class="sxs-lookup"><span data-stu-id="f0efa-130">No</span></span> | <span data-ttu-id="f0efa-131">패키지 업데이트 중에 적용되는 이 패키지에 허용된 버전의 범위입니다([업그레이드 버전 포함](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions) 참조).</span><span class="sxs-lookup"><span data-stu-id="f0efa-131">A range of allowed versions for this package applied during package update (see [Constraining upgrade versions](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span></span> <span data-ttu-id="f0efa-132">설치 또는 복원 작업 중에 설치할 패키지에 영향을 주지 *않습니다*.</span><span class="sxs-lookup"><span data-stu-id="f0efa-132">It does *not* affect what package is installed during an install or restore operation.</span></span> <span data-ttu-id="f0efa-133">구문은 [패키지 버전 관리](../reference/package-versioning.md#version-ranges-and-wildcards)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f0efa-133">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for syntax.</span></span> <span data-ttu-id="f0efa-134">또한 PackageManager UI는 허용되지 않는 모든 버전을 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f0efa-134">The PackageManager UI also disables all versions outside the allowed range.</span></span> | 
| <span data-ttu-id="f0efa-135">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="f0efa-135">developmentDependency</span></span> | <span data-ttu-id="f0efa-136">아니요</span><span class="sxs-lookup"><span data-stu-id="f0efa-136">No</span></span> | <span data-ttu-id="f0efa-137">사용 중인 프로젝트 자체에서 NuGet 패키지를 만드는 경우 종속성을 위해 이 값을 `true`로 설정하면 사용 중인 패키지를 만들 때 해당 패키지를 포함하지 않도록 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="f0efa-137">If the consuming project itself creates a NuGet package, setting this to `true` for a dependency prevents that package from being included when the consuming package is created.</span></span> <span data-ttu-id="f0efa-138">기본값은 `false`입니다.</span><span class="sxs-lookup"><span data-stu-id="f0efa-138">The default is `false`.</span></span> | 

## <a name="examples"></a><span data-ttu-id="f0efa-139">예제</span><span class="sxs-lookup"><span data-stu-id="f0efa-139">Examples</span></span>

<span data-ttu-id="f0efa-140">다음과 같은 `packages.config`은 두 개의 종속성을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="f0efa-140">The following `packages.config` refers to two dependencies:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="jQuery" version="3.1.1" targetFramework="net46" />
  <package id="NLog" version="4.3.10" targetFramework="net46" />
</packages>
```

<span data-ttu-id="f0efa-141">다음과 같은 `packages.config`는 9개의 패키지를 참조하지만 `developmentDependency` 특성 때문에 사용 중인 패키지를 빌드할 때 `Microsoft.Net.Compilers`가 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f0efa-141">The following `packages.config` refers to nine packages, but `Microsoft.Net.Compilers` will not be included when building the consuming package because of the `developmentDependency` attribute.</span></span> <span data-ttu-id="f0efa-142">또한 Newtonsoft.Json에 대한 참조는 8.x 및 9.x 버전에 대한 업데이트를 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="f0efa-142">The reference to Newtonsoft.Json also restricts updates to 8.x and 9.x versions only.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="Microsoft.CodeDom.Providers.DotNetCompilerPlatform" version="1.0.0" targetFramework="net46" />
  <package id="Microsoft.Net.Compilers" version="1.0.0" targetFramework="net46" developmentDependency="true" />
  <package id="Microsoft.Web.Infrastructure" version="1.0.0.0" targetFramework="net46" />
  <package id="Microsoft.Web.Xdt" version="2.1.1" targetFramework="net46" />
  <package id="Newtonsoft.Json" version="8.0.3" allowedVersions="[8,10)" targetFramework="net46" />
  <package id="NuGet.Core" version="2.11.1" targetFramework="net46" />
  <package id="NuGet.Server" version="2.11.2" targetFramework="net46" />
  <package id="RouteMagic" version="1.3" targetFramework="net46" />
  <package id="WebActivatorEx" version="2.1.0" targetFramework="net46" />
</packages>
```
