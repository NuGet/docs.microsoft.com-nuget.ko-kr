---
title: nuget.config 파일 참조
description: config, bindingRedirects, packageRestore, solution 및 packageSource 섹션이 포함된 NuGet.Config 파일 참조입니다.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 10/25/2017
ms.topic: reference
ms.openlocfilehash: e57d17c5bf393a05b8915b9a1a7af0b659a04716
ms.sourcegitcommit: 055248d790051774c892b220eca12015babbd668
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2018
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="3d372-103">nuget.config 참조</span><span class="sxs-lookup"><span data-stu-id="3d372-103">nuget.config reference</span></span>

<span data-ttu-id="3d372-104">NuGet 동작은 [NuGet 동작 구성](../consume-packages/configuring-nuget-behavior.md)에서 설명한 대로 여러 `NuGet.Config` 파일의 설정으로 제어됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-104">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="3d372-105">`nuget.config`는 최상위 `<configuration>` 노드를 포함하는 XML 파일이며, 이 파일에는 이 항목에서 설명하는 섹션 요소가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-105">`nuget.config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="3d372-106">각 섹션에는 `key` 및 `value` 특성이 있는 0개 이상의 `<add>` 요소가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-106">Each section contains zero or more `<add>` elements with `key` and `value` attributes.</span></span> <span data-ttu-id="3d372-107">[config 파일 예제](#example-config-file)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d372-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="3d372-108">설정 이름은 대/소문자를 구분하지 않으며, 값에는 [환경 변수](#using-environment-variables)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<span data-ttu-id="3d372-109">항목 내용:</span><span class="sxs-lookup"><span data-stu-id="3d372-109">In this topic:</span></span>

- [<span data-ttu-id="3d372-110">config 섹션</span><span class="sxs-lookup"><span data-stu-id="3d372-110">config section</span></span>](#config-section)
- [<span data-ttu-id="3d372-111">bindingRedirects 섹션</span><span class="sxs-lookup"><span data-stu-id="3d372-111">bindingRedirects section</span></span>](#bindingredirects-section)
- [<span data-ttu-id="3d372-112">packageRestore 섹션</span><span class="sxs-lookup"><span data-stu-id="3d372-112">packageRestore section</span></span>](#packagerestore-section)
- [<span data-ttu-id="3d372-113">solution 섹션</span><span class="sxs-lookup"><span data-stu-id="3d372-113">solution section</span></span>](#solution-section)
- <span data-ttu-id="3d372-114">[패키지 원본 섹션](#package-source-sections):</span><span class="sxs-lookup"><span data-stu-id="3d372-114">[Package source sections](#package-source-sections):</span></span>
  - [<span data-ttu-id="3d372-115">packageSources</span><span class="sxs-lookup"><span data-stu-id="3d372-115">packageSources</span></span>](#packagesources)
  - [<span data-ttu-id="3d372-116">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="3d372-116">packageSourceCredentials</span></span>](#packagesourcecredentials)
  - [<span data-ttu-id="3d372-117">apikeys</span><span class="sxs-lookup"><span data-stu-id="3d372-117">apikeys</span></span>](#apikeys)
  - [<span data-ttu-id="3d372-118">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="3d372-118">disabledPackageSources</span></span>](#disabledpackagesources)
  - [<span data-ttu-id="3d372-119">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="3d372-119">activePackageSource</span></span>](#activepackagesource)
- [<span data-ttu-id="3d372-120">환경 변수 사용</span><span class="sxs-lookup"><span data-stu-id="3d372-120">Using environment variables</span></span>](#using-environment-variables)
- [<span data-ttu-id="3d372-121">config 파일 예제</span><span class="sxs-lookup"><span data-stu-id="3d372-121">Example config file</span></span>](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="3d372-122">config 섹션</span><span class="sxs-lookup"><span data-stu-id="3d372-122">config section</span></span>

<span data-ttu-id="3d372-123">[`nuget config` 명령](../tools/cli-ref-config.md)을 사용하여 설정할 수 있는 기타 구성 설정을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-123">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../tools/cli-ref-config.md).</span></span>

<span data-ttu-id="3d372-124">`dependencyVersion` 및 `repositoryPath` 사용 하 여 프로젝트에만 적용 `packages.config`합니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-124">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="3d372-125">`globalPackagesFolder` PackageReference 형식을 사용 하 여 프로젝트에만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-125">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="3d372-126">Key</span><span class="sxs-lookup"><span data-stu-id="3d372-126">Key</span></span> | <span data-ttu-id="3d372-127">값</span><span class="sxs-lookup"><span data-stu-id="3d372-127">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3d372-128">dependencyVersion(`packages.config`만)</span><span class="sxs-lookup"><span data-stu-id="3d372-128">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="3d372-129">`-DependencyVersion` 스위치가 직접 지정되지 않은 경우 패키지 설치, 복원 및 업데이트에 대한 기본 `DependencyVersion` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-129">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="3d372-130">이 값은 NuGet 패키지 관리자 UI에서도 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-130">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="3d372-131">값은 `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`입니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-131">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="3d372-132">globalPackagesFolder (프로젝트만 PackageReference를 사용 하 여)</span><span class="sxs-lookup"><span data-stu-id="3d372-132">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="3d372-133">기본 전역 패키지 폴더의 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-133">The location of the default global packages folder.</span></span> <span data-ttu-id="3d372-134">기본값은 `%userprofile%\.nuget\packages`(Windows) 또는 `~/.nuget/packages`(Mac/Linux)입니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-134">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="3d372-135">상대 경로는 프로젝트별 `nuget.config` 파일에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-135">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="3d372-136">NUGET_PACKAGES 환경 변수로 선행 하는이 설정이 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-136">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="3d372-137">repositoryPath(`packages.config`만)</span><span class="sxs-lookup"><span data-stu-id="3d372-137">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="3d372-138">기본 `$(Solutiondir)/packages` 폴더 대신 NuGet 패키지를 설치할 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-138">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="3d372-139">상대 경로는 프로젝트별 `nuget.config` 파일에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-139">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="3d372-140">NUGET_PACKAGES 환경 변수로 선행 하는이 설정이 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-140">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="3d372-141">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="3d372-141">defaultPushSource</span></span> | <span data-ttu-id="3d372-142">작업에 대한 다른 패키지 원본이 없을 때 기본값으로 사용해야 하는 패키지 원본의 URL 또는 경로를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-142">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="3d372-143">http_proxy, http_proxy.user, http_proxy.password, no_proxy</span><span class="sxs-lookup"><span data-stu-id="3d372-143">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="3d372-144">패키지 원본에 연결할 때 사용할 프록시 설정입니다. `http_proxy`는 `http://<username>:<password>@<domain>` 형식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-144">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="3d372-145">암호는 암호화되어 있으며, 수동으로 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-145">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="3d372-146">`no_proxy`의 경우 값은 프록시 서버를 우회하는 도메인의 쉼표로 구분된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-146">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="3d372-147">이러한 값에 대해 http_proxy 및 no_proxy 환경 변수를 번갈아 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-147">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="3d372-148">자세한 내용은 [NuGet 프록시 설정](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html)(skolima.blogspot.com)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d372-148">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |

<span data-ttu-id="3d372-149">**예제**:</span><span class="sxs-lookup"><span data-stu-id="3d372-149">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="3d372-150">bindingRedirects 섹션</span><span class="sxs-lookup"><span data-stu-id="3d372-150">bindingRedirects section</span></span>

<span data-ttu-id="3d372-151">패키지가 설치될 때 NuGet에서 자동 바인딩 리디렉션을 수행할지 여부를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-151">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="3d372-152">Key</span><span class="sxs-lookup"><span data-stu-id="3d372-152">Key</span></span> | <span data-ttu-id="3d372-153">값</span><span class="sxs-lookup"><span data-stu-id="3d372-153">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3d372-154">skip</span><span class="sxs-lookup"><span data-stu-id="3d372-154">skip</span></span> | <span data-ttu-id="3d372-155">자동 바인딩 리디렉션을 건너뛸지 여부를 나타내는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-155">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="3d372-156">기본값은 false입니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-156">The default is false.</span></span> |

<span data-ttu-id="3d372-157">**예제**:</span><span class="sxs-lookup"><span data-stu-id="3d372-157">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="3d372-158">packageRestore 섹션</span><span class="sxs-lookup"><span data-stu-id="3d372-158">packageRestore section</span></span>

<span data-ttu-id="3d372-159">빌드하는 동안의 패키지 복원을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-159">Controls package restore during builds.</span></span>

| <span data-ttu-id="3d372-160">Key</span><span class="sxs-lookup"><span data-stu-id="3d372-160">Key</span></span> | <span data-ttu-id="3d372-161">값</span><span class="sxs-lookup"><span data-stu-id="3d372-161">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3d372-162">사용</span><span class="sxs-lookup"><span data-stu-id="3d372-162">enabled</span></span> | <span data-ttu-id="3d372-163">NuGet에서 자동 복원을 수행할 수 있는지 여부를 나타내는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-163">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="3d372-164">config 파일에서 이 키를 설정하는 대신 `EnableNuGetPackageRestore` 환경 변수를 `True` 값으로 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-164">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="3d372-165">자동</span><span class="sxs-lookup"><span data-stu-id="3d372-165">automatic</span></span> | <span data-ttu-id="3d372-166">NuGet에서 빌드하는 동안 누락된 패키지를 확인해야 하는지 여부를 나타내는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-166">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="3d372-167">**예제**:</span><span class="sxs-lookup"><span data-stu-id="3d372-167">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="3d372-168">solution 섹션</span><span class="sxs-lookup"><span data-stu-id="3d372-168">solution section</span></span>

<span data-ttu-id="3d372-169">솔루션의 `packages` 폴더가 원본 제어에 포함되는지 여부를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-169">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="3d372-170">이 섹션은 솔루션 폴더의 `nuget.config` 파일에서만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-170">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="3d372-171">Key</span><span class="sxs-lookup"><span data-stu-id="3d372-171">Key</span></span> | <span data-ttu-id="3d372-172">값</span><span class="sxs-lookup"><span data-stu-id="3d372-172">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3d372-173">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="3d372-173">disableSourceControlIntegration</span></span> | <span data-ttu-id="3d372-174">원본 제어로 작업할 때 패키지 폴더를 무시할지 여부를 나타내는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-174">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="3d372-175">기본값은 false입니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-175">The default value is false.</span></span> |

<span data-ttu-id="3d372-176">**예제**:</span><span class="sxs-lookup"><span data-stu-id="3d372-176">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="3d372-177">패키지 원본 섹션</span><span class="sxs-lookup"><span data-stu-id="3d372-177">Package source sections</span></span>

<span data-ttu-id="3d372-178">`packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource` 및 `disabledPackageSources` 모두가 함께 작동하여 NuGet에서 설치, 복원 및 업데이트 작업 중에 패키지 리포지토리와 함께 작동하는 방식을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-178">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, and `disabledPackageSources` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="3d372-179">[`nuget setapikey` 명령](../tools/cli-ref-setapikey.md)을 사용하여 관리되는 `apikeys`를 제외하고는 일반적으로 [`nuget sources` 명령](../tools/cli-ref-sources.md)이 이러한 설정을 관리하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-179">The [`nuget sources` command](../tools/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

<span data-ttu-id="3d372-180">nuget.org에 대한 원본 URL은 `https://api.nuget.org/v3/index.json`입니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-180">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="3d372-181">packageSources</span><span class="sxs-lookup"><span data-stu-id="3d372-181">packageSources</span></span>

<span data-ttu-id="3d372-182">알려진 모든 패키지 원본을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-182">Lists all known package sources.</span></span> <span data-ttu-id="3d372-183">복원 작업 중 및 PackageReference 형식을 사용 하 여 모든 프로젝트와 순서는 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-183">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="3d372-184">NuGet 설치 원본 순서를 적용 및 업데이트 작업을 사용 하 여 프로젝트와 함께 `packages.config`합니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-184">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="3d372-185">Key</span><span class="sxs-lookup"><span data-stu-id="3d372-185">Key</span></span> | <span data-ttu-id="3d372-186">값</span><span class="sxs-lookup"><span data-stu-id="3d372-186">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3d372-187">(패키지 원본에 할당할 이름)</span><span class="sxs-lookup"><span data-stu-id="3d372-187">(name to assign to the package source)</span></span> | <span data-ttu-id="3d372-188">패키지 원본의 경로 또는 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-188">The path or URL of the package source.</span></span> |

<span data-ttu-id="3d372-189">**예제**:</span><span class="sxs-lookup"><span data-stu-id="3d372-189">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="3d372-190">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="3d372-190">packageSourceCredentials</span></span>

<span data-ttu-id="3d372-191">원본에 대한 사용자 이름과 암호를 저장하며, 일반적으로 `nuget sources`와 함께 `-username` 및 `-password` 스위치로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-191">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="3d372-192">또한 `-storepasswordincleartext` 옵션을 사용하지 않는 한 암호는 기본적으로 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-192">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="3d372-193">Key</span><span class="sxs-lookup"><span data-stu-id="3d372-193">Key</span></span> | <span data-ttu-id="3d372-194">값</span><span class="sxs-lookup"><span data-stu-id="3d372-194">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3d372-195">사용자 이름</span><span class="sxs-lookup"><span data-stu-id="3d372-195">username</span></span> | <span data-ttu-id="3d372-196">일반 텍스트 형식의 원본에 대한 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-196">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="3d372-197">암호</span><span class="sxs-lookup"><span data-stu-id="3d372-197">password</span></span> | <span data-ttu-id="3d372-198">원본에 대한 암호화된 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-198">The encrypted password for the source.</span></span> |
| <span data-ttu-id="3d372-199">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="3d372-199">cleartextpassword</span></span> | <span data-ttu-id="3d372-200">원본에 대한 암호화되지 않은 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-200">The unencrypted password for the source.</span></span> |

<span data-ttu-id="3d372-201">**예제:**</span><span class="sxs-lookup"><span data-stu-id="3d372-201">**Example:**</span></span>

<span data-ttu-id="3d372-202">config 파일에서 `<packageSourceCredentials>` 요소에는 적용 가능한 원본 이름 각각에 대한 자식 노드가 포함됩니다(이름에 포함된 공백은 `_x0020_`로 바뀜).</span><span class="sxs-lookup"><span data-stu-id="3d372-202">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="3d372-203">즉 "Contoso" 및 "Test Source"라는 원본의 경우 암호화된 암호를 사용하면 config 파일에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-203">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="Password" value="..." />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="Password" value="..." />
    </Test_x0020_Source>
</packageSourceCredentials>
```

<span data-ttu-id="3d372-204">암호화되지 않은 암호를 사용하는 경우:</span><span class="sxs-lookup"><span data-stu-id="3d372-204">When using unencrypted passwords:</span></span>

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="ClearTextPassword" value="33f!!lloppa" />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="ClearTextPassword" value="hal+9ooo_da!sY" />
    </Test_x0020_Source>
</packageSourceCredentials>
```

### <a name="apikeys"></a><span data-ttu-id="3d372-205">apikeys</span><span class="sxs-lookup"><span data-stu-id="3d372-205">apikeys</span></span>

<span data-ttu-id="3d372-206">[`nuget setapikey` 명령](../tools/cli-ref-setapikey.md)으로 설정된 대로 API 키 인증을 사용하는 원본에 대한 키를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-206">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="3d372-207">Key</span><span class="sxs-lookup"><span data-stu-id="3d372-207">Key</span></span> | <span data-ttu-id="3d372-208">값</span><span class="sxs-lookup"><span data-stu-id="3d372-208">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3d372-209">(원본 URL)</span><span class="sxs-lookup"><span data-stu-id="3d372-209">(source URL)</span></span> | <span data-ttu-id="3d372-210">암호화된 API 키입니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-210">The encrypted API key.</span></span> |

<span data-ttu-id="3d372-211">**예제**:</span><span class="sxs-lookup"><span data-stu-id="3d372-211">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="3d372-212">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="3d372-212">disabledPackageSources</span></span>

<span data-ttu-id="3d372-213">현재 사용할 수 없는 원본을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-213">Identified currently disabled sources.</span></span> <span data-ttu-id="3d372-214">비어 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-214">May be empty.</span></span>

| <span data-ttu-id="3d372-215">Key</span><span class="sxs-lookup"><span data-stu-id="3d372-215">Key</span></span> | <span data-ttu-id="3d372-216">값</span><span class="sxs-lookup"><span data-stu-id="3d372-216">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3d372-217">(원본 이름)</span><span class="sxs-lookup"><span data-stu-id="3d372-217">(name of source)</span></span> | <span data-ttu-id="3d372-218">원본을 사용할 수 없는지 여부를 나타내는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-218">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="3d372-219">**예제:**</span><span class="sxs-lookup"><span data-stu-id="3d372-219">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="3d372-220">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="3d372-220">activePackageSource</span></span>

<span data-ttu-id="3d372-221">*(2.x만, 3.x 이상에서는 사용되지 않음)*</span><span class="sxs-lookup"><span data-stu-id="3d372-221">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="3d372-222">현재 활성 중인 원본을 식별하거나 모든 원본의 집계를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-222">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="3d372-223">Key</span><span class="sxs-lookup"><span data-stu-id="3d372-223">Key</span></span> | <span data-ttu-id="3d372-224">값</span><span class="sxs-lookup"><span data-stu-id="3d372-224">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3d372-225">(원본 이름) 또는 `All`</span><span class="sxs-lookup"><span data-stu-id="3d372-225">(name of source) or `All`</span></span> | <span data-ttu-id="3d372-226">키가 원본의 이름이면 값은 원본 경로 또는 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-226">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="3d372-227">`All`이면 값은 `(Aggregate source)`여야 하며, 그렇지 않으면 사용할 수 없는 모든 패키지 원본이 결합됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-227">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="3d372-228">**예제**:</span><span class="sxs-lookup"><span data-stu-id="3d372-228">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="using-environment-variables"></a><span data-ttu-id="3d372-229">환경 변수 사용</span><span class="sxs-lookup"><span data-stu-id="3d372-229">Using environment variables</span></span>

<span data-ttu-id="3d372-230">`nuget.config` 값(NuGet 3.4 이상)의 환경 변수를 사용하여 런타임에 설정을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-230">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="3d372-231">예를 들어 Windows의 `HOME` 환경 변수가 `c:\users\username`으로 설정되면 구성 파일의 `%HOME%\NuGetRepository` 값이 `c:\users\username\NuGetRepository`로 해석됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-231">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="3d372-232">마찬가지로, Mac/Linux의 `HOME`이 `/home/myStuff`로 설정되면 구성 파일의 `%HOME%/NuGetRepository`가 `/home/myStuff/NuGetRepository`로 해석됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-232">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `%HOME%/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="3d372-233">환경 변수가 없으면 NuGet에서 구성 파일의 리터럴 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-233">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="3d372-234">config 파일 예제</span><span class="sxs-lookup"><span data-stu-id="3d372-234">Example config file</span></span>

<span data-ttu-id="3d372-235">아래는 몇 가지 설정을 보여 주는 `nuget.config` 파일의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="3d372-235">Below is an example `nuget.config` file that illustrates a number of settings:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <!--
            Used to specify the default location to expand packages.
            See: nuget.exe help install
            See: nuget.exe help update

            In this example, %PACKAGEHOME% is an environment variable. On Mac/Linux,
            use $PACKAGE_HOME/External as the value.
        -->
        <add key="repositoryPath" value="%PACKAGEHOME%\External" />

        <!--
            Used to specify default source for the push command.
            See: nuget.exe help push
        -->

        <add key="defaultPushSource" value="https://MyRepo/ES/api/v2/package" />

        <!-- Proxy settings -->
        <add key="http_proxy" value="host" />
        <add key="http_proxy.user" value="username" />
        <add key="http_proxy.password" value="encrypted_password" />
    </config>

    <packageRestore>
        <!-- Allow NuGet to download missing packages -->
        <add key="enabled" value="True" />

        <!-- Automatically check for missing packages during build in Visual Studio -->
        <add key="automatic" value="True" />
    </packageRestore>

    <!--
        Used to specify the default Sources for list, install and update.
        See: nuget.exe help list
        See: nuget.exe help install
        See: nuget.exe help update
    -->
    <packageSources>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
        <add key="MyRepo - ES" value="https://MyRepo/ES/nuget" />
    </packageSources>

    <!-- Used to store credentials -->
    <packageSourceCredentials />

    <!-- Used to disable package sources  -->
    <disabledPackageSources />

    <!--
        Used to specify default API key associated with sources.
        See: nuget.exe help setApiKey
        See: nuget.exe help push
        See: nuget.exe help mirror
    -->
    <apikeys>
        <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
    </apikeys>
</configuration>
```
