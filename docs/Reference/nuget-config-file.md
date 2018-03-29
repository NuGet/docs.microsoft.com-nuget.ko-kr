---
title: NuGet.Config 파일 참조 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/25/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: config, bindingRedirects, packageRestore, solution 및 packageSource 섹션이 포함된 NuGet.Config 파일 참조입니다.
keywords: NuGet.Config 파일, NuGet 구성 참조, NuGet 구성 옵션
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: e2a9d4f10ac6af4e5bc7386d4f78e18c2a5752c4
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="98711-104">NuGet.Config 참조</span><span class="sxs-lookup"><span data-stu-id="98711-104">NuGet.Config reference</span></span>

<span data-ttu-id="98711-105">NuGet 동작은 [NuGet 동작 구성](../consume-packages/configuring-nuget-behavior.md)에서 설명한 대로 여러 `NuGet.Config` 파일의 설정으로 제어됩니다.</span><span class="sxs-lookup"><span data-stu-id="98711-105">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="98711-106">`NuGet.Config`는 최상위 `<configuration>` 노드를 포함하는 XML 파일이며, 이 파일에는 이 항목에서 설명하는 섹션 요소가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98711-106">`NuGet.Config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="98711-107">각 섹션에는 `key` 및 `value` 특성이 있는 0개 이상의 `<add>` 요소가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98711-107">Each section contains zero or more `<add>` elements with `key` and `value` attributes.</span></span> <span data-ttu-id="98711-108">[config 파일 예제](#example-config-file)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="98711-108">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="98711-109">설정 이름은 대/소문자를 구분하지 않으며, 값에는 [환경 변수](#using-environment-variables)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98711-109">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<span data-ttu-id="98711-110">항목 내용:</span><span class="sxs-lookup"><span data-stu-id="98711-110">In this topic:</span></span>

- [<span data-ttu-id="98711-111">config 섹션</span><span class="sxs-lookup"><span data-stu-id="98711-111">config section</span></span>](#config-section)
- [<span data-ttu-id="98711-112">bindingRedirects 섹션</span><span class="sxs-lookup"><span data-stu-id="98711-112">bindingRedirects section</span></span>](#bindingredirects-section)
- [<span data-ttu-id="98711-113">packageRestore 섹션</span><span class="sxs-lookup"><span data-stu-id="98711-113">packageRestore section</span></span>](#packagerestore-section)
- [<span data-ttu-id="98711-114">solution 섹션</span><span class="sxs-lookup"><span data-stu-id="98711-114">solution section</span></span>](#solution-section)
- <span data-ttu-id="98711-115">[패키지 원본 섹션](#package-source-sections):</span><span class="sxs-lookup"><span data-stu-id="98711-115">[Package source sections](#package-source-sections):</span></span>
  - [<span data-ttu-id="98711-116">packageSources</span><span class="sxs-lookup"><span data-stu-id="98711-116">packageSources</span></span>](#packagesources)
  - [<span data-ttu-id="98711-117">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="98711-117">packageSourceCredentials</span></span>](#packagesourcecredentials)
  - [<span data-ttu-id="98711-118">apikeys</span><span class="sxs-lookup"><span data-stu-id="98711-118">apikeys</span></span>](#apikeys)
  - [<span data-ttu-id="98711-119">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="98711-119">disabledPackageSources</span></span>](#disabledpackagesources)
  - [<span data-ttu-id="98711-120">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="98711-120">activePackageSource</span></span>](#activepackagesource)
- [<span data-ttu-id="98711-121">환경 변수 사용</span><span class="sxs-lookup"><span data-stu-id="98711-121">Using environment variables</span></span>](#using-environment-variables)
- [<span data-ttu-id="98711-122">config 파일 예제</span><span class="sxs-lookup"><span data-stu-id="98711-122">Example config file</span></span>](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="98711-123">config 섹션</span><span class="sxs-lookup"><span data-stu-id="98711-123">config section</span></span>

<span data-ttu-id="98711-124">[`nuget config` 명령](../tools/cli-ref-config.md)을 사용하여 설정할 수 있는 기타 구성 설정을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="98711-124">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../tools/cli-ref-config.md).</span></span>

<span data-ttu-id="98711-125">`dependencyVersion` 및 `repositoryPath` 사용 하 여 프로젝트에만 적용 `packages.config`합니다.</span><span class="sxs-lookup"><span data-stu-id="98711-125">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="98711-126">`globalPackagesFolder` PackageReference 형식을 사용 하 여 프로젝트에만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98711-126">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="98711-127">Key</span><span class="sxs-lookup"><span data-stu-id="98711-127">Key</span></span> | <span data-ttu-id="98711-128">값</span><span class="sxs-lookup"><span data-stu-id="98711-128">Value</span></span> |
| --- | --- |
| <span data-ttu-id="98711-129">dependencyVersion(`packages.config`만)</span><span class="sxs-lookup"><span data-stu-id="98711-129">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="98711-130">`-DependencyVersion` 스위치가 직접 지정되지 않은 경우 패키지 설치, 복원 및 업데이트에 대한 기본 `DependencyVersion` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="98711-130">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="98711-131">이 값은 NuGet 패키지 관리자 UI에서도 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="98711-131">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="98711-132">값은 `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`입니다.</span><span class="sxs-lookup"><span data-stu-id="98711-132">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="98711-133">globalPackagesFolder (프로젝트만 PackageReference를 사용 하 여)</span><span class="sxs-lookup"><span data-stu-id="98711-133">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="98711-134">기본 전역 패키지 폴더의 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="98711-134">The location of the default global packages folder.</span></span> <span data-ttu-id="98711-135">기본값은 `%userprofile%\.nuget\packages`(Windows) 또는 `~/.nuget/packages`(Mac/Linux)입니다.</span><span class="sxs-lookup"><span data-stu-id="98711-135">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="98711-136">상대 경로는 프로젝트별 `Nuget.Config` 파일에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98711-136">A relative path can be used in project-specific `Nuget.Config` files.</span></span> <span data-ttu-id="98711-137">NUGET_PACKAGES 환경 변수로 선행 하는이 설정이 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98711-137">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="98711-138">repositoryPath(`packages.config`만)</span><span class="sxs-lookup"><span data-stu-id="98711-138">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="98711-139">기본 `$(Solutiondir)/packages` 폴더 대신 NuGet 패키지를 설치할 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="98711-139">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="98711-140">상대 경로는 프로젝트별 `Nuget.Config` 파일에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98711-140">A relative path can be used in project-specific `Nuget.Config` files.</span></span> <span data-ttu-id="98711-141">NUGET_PACKAGES 환경 변수로 선행 하는이 설정이 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98711-141">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="98711-142">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="98711-142">defaultPushSource</span></span> | <span data-ttu-id="98711-143">작업에 대한 다른 패키지 원본이 없을 때 기본값으로 사용해야 하는 패키지 원본의 URL 또는 경로를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="98711-143">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="98711-144">http_proxy, http_proxy.user, http_proxy.password, no_proxy</span><span class="sxs-lookup"><span data-stu-id="98711-144">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="98711-145">패키지 원본에 연결할 때 사용할 프록시 설정입니다. `http_proxy`는 `http://<username>:<password>@<domain>` 형식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98711-145">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="98711-146">암호는 암호화되어 있으며, 수동으로 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="98711-146">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="98711-147">`no_proxy`의 경우 값은 프록시 서버를 우회하는 도메인의 쉼표로 구분된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="98711-147">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="98711-148">이러한 값에 대해 http_proxy 및 no_proxy 환경 변수를 번갈아 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98711-148">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="98711-149">자세한 내용은 [NuGet 프록시 설정](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html)(skolima.blogspot.com)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="98711-149">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |

<span data-ttu-id="98711-150">**예제**:</span><span class="sxs-lookup"><span data-stu-id="98711-150">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="98711-151">bindingRedirects 섹션</span><span class="sxs-lookup"><span data-stu-id="98711-151">bindingRedirects section</span></span>

<span data-ttu-id="98711-152">패키지가 설치될 때 NuGet에서 자동 바인딩 리디렉션을 수행할지 여부를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="98711-152">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="98711-153">Key</span><span class="sxs-lookup"><span data-stu-id="98711-153">Key</span></span> | <span data-ttu-id="98711-154">값</span><span class="sxs-lookup"><span data-stu-id="98711-154">Value</span></span> |
| --- | --- |
| <span data-ttu-id="98711-155">skip</span><span class="sxs-lookup"><span data-stu-id="98711-155">skip</span></span> | <span data-ttu-id="98711-156">자동 바인딩 리디렉션을 건너뛸지 여부를 나타내는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="98711-156">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="98711-157">기본값은 false입니다.</span><span class="sxs-lookup"><span data-stu-id="98711-157">The default is false.</span></span> |

<span data-ttu-id="98711-158">**예제**:</span><span class="sxs-lookup"><span data-stu-id="98711-158">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="98711-159">packageRestore 섹션</span><span class="sxs-lookup"><span data-stu-id="98711-159">packageRestore section</span></span>

<span data-ttu-id="98711-160">빌드하는 동안의 패키지 복원을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="98711-160">Controls package restore during builds.</span></span>

| <span data-ttu-id="98711-161">Key</span><span class="sxs-lookup"><span data-stu-id="98711-161">Key</span></span> | <span data-ttu-id="98711-162">값</span><span class="sxs-lookup"><span data-stu-id="98711-162">Value</span></span> |
| --- | --- |
| <span data-ttu-id="98711-163">사용</span><span class="sxs-lookup"><span data-stu-id="98711-163">enabled</span></span> | <span data-ttu-id="98711-164">NuGet에서 자동 복원을 수행할 수 있는지 여부를 나타내는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="98711-164">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="98711-165">config 파일에서 이 키를 설정하는 대신 `EnableNuGetPackageRestore` 환경 변수를 `True` 값으로 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98711-165">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="98711-166">자동</span><span class="sxs-lookup"><span data-stu-id="98711-166">automatic</span></span> | <span data-ttu-id="98711-167">NuGet에서 빌드하는 동안 누락된 패키지를 확인해야 하는지 여부를 나타내는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="98711-167">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="98711-168">**예제**:</span><span class="sxs-lookup"><span data-stu-id="98711-168">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="98711-169">solution 섹션</span><span class="sxs-lookup"><span data-stu-id="98711-169">solution section</span></span>

<span data-ttu-id="98711-170">솔루션의 `packages` 폴더가 원본 제어에 포함되는지 여부를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="98711-170">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="98711-171">이 섹션은 솔루션 폴더의 `Nuget.Config` 파일에서만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="98711-171">This section works only in `Nuget.Config` files in a solution folder.</span></span>

| <span data-ttu-id="98711-172">Key</span><span class="sxs-lookup"><span data-stu-id="98711-172">Key</span></span> | <span data-ttu-id="98711-173">값</span><span class="sxs-lookup"><span data-stu-id="98711-173">Value</span></span> |
| --- | --- |
| <span data-ttu-id="98711-174">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="98711-174">disableSourceControlIntegration</span></span> | <span data-ttu-id="98711-175">원본 제어로 작업할 때 패키지 폴더를 무시할지 여부를 나타내는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="98711-175">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="98711-176">기본값은 false입니다.</span><span class="sxs-lookup"><span data-stu-id="98711-176">The default value is false.</span></span> |

<span data-ttu-id="98711-177">**예제**:</span><span class="sxs-lookup"><span data-stu-id="98711-177">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="98711-178">패키지 원본 섹션</span><span class="sxs-lookup"><span data-stu-id="98711-178">Package source sections</span></span>

<span data-ttu-id="98711-179">`packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource` 및 `disabledPackageSources` 모두가 함께 작동하여 NuGet에서 설치, 복원 및 업데이트 작업 중에 패키지 리포지토리와 함께 작동하는 방식을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="98711-179">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, and `disabledPackageSources` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="98711-180">[`nuget setapikey` 명령](../tools/cli-ref-setapikey.md)을 사용하여 관리되는 `apikeys`를 제외하고는 일반적으로 [`nuget sources` 명령](../tools/cli-ref-sources.md)이 이러한 설정을 관리하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="98711-180">The [`nuget sources` command](../tools/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

<span data-ttu-id="98711-181">nuget.org에 대한 원본 URL은 `https://api.nuget.org/v3/index.json`입니다.</span><span class="sxs-lookup"><span data-stu-id="98711-181">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="98711-182">packageSources</span><span class="sxs-lookup"><span data-stu-id="98711-182">packageSources</span></span>

<span data-ttu-id="98711-183">알려진 모든 패키지 원본을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="98711-183">Lists all known package sources.</span></span> <span data-ttu-id="98711-184">복원 작업 중 및 PackageReference 형식을 사용 하 여 모든 프로젝트와 순서는 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98711-184">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="98711-185">NuGet 설치 원본 순서를 적용 및 업데이트 작업을 사용 하 여 프로젝트와 함께 `packages.config`합니다.</span><span class="sxs-lookup"><span data-stu-id="98711-185">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="98711-186">Key</span><span class="sxs-lookup"><span data-stu-id="98711-186">Key</span></span> | <span data-ttu-id="98711-187">값</span><span class="sxs-lookup"><span data-stu-id="98711-187">Value</span></span> |
| --- | --- |
| <span data-ttu-id="98711-188">(패키지 원본에 할당할 이름)</span><span class="sxs-lookup"><span data-stu-id="98711-188">(name to assign to the package source)</span></span> | <span data-ttu-id="98711-189">패키지 원본의 경로 또는 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="98711-189">The path or URL of the package source.</span></span> |

<span data-ttu-id="98711-190">**예제**:</span><span class="sxs-lookup"><span data-stu-id="98711-190">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="98711-191">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="98711-191">packageSourceCredentials</span></span>

<span data-ttu-id="98711-192">원본에 대한 사용자 이름과 암호를 저장하며, 일반적으로 `nuget sources`와 함께 `-username` 및 `-password` 스위치로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="98711-192">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="98711-193">또한 `-storepasswordincleartext` 옵션을 사용하지 않는 한 암호는 기본적으로 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="98711-193">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="98711-194">Key</span><span class="sxs-lookup"><span data-stu-id="98711-194">Key</span></span> | <span data-ttu-id="98711-195">값</span><span class="sxs-lookup"><span data-stu-id="98711-195">Value</span></span> |
| --- | --- |
| <span data-ttu-id="98711-196">사용자 이름</span><span class="sxs-lookup"><span data-stu-id="98711-196">username</span></span> | <span data-ttu-id="98711-197">일반 텍스트 형식의 원본에 대한 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="98711-197">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="98711-198">암호</span><span class="sxs-lookup"><span data-stu-id="98711-198">password</span></span> | <span data-ttu-id="98711-199">원본에 대한 암호화된 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="98711-199">The encrypted password for the source.</span></span> |
| <span data-ttu-id="98711-200">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="98711-200">cleartextpassword</span></span> | <span data-ttu-id="98711-201">원본에 대한 암호화되지 않은 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="98711-201">The unencrypted password for the source.</span></span> |

<span data-ttu-id="98711-202">**예제:**</span><span class="sxs-lookup"><span data-stu-id="98711-202">**Example:**</span></span>

<span data-ttu-id="98711-203">config 파일에서 `<packageSourceCredentials>` 요소에는 적용 가능한 원본 이름 각각에 대한 자식 노드가 포함됩니다(이름에 포함된 공백은 `_x0020_`로 바뀜).</span><span class="sxs-lookup"><span data-stu-id="98711-203">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="98711-204">즉 "Contoso" 및 "Test Source"라는 원본의 경우 암호화된 암호를 사용하면 config 파일에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="98711-204">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="98711-205">암호화되지 않은 암호를 사용하는 경우:</span><span class="sxs-lookup"><span data-stu-id="98711-205">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="98711-206">apikeys</span><span class="sxs-lookup"><span data-stu-id="98711-206">apikeys</span></span>

<span data-ttu-id="98711-207">[`nuget setapikey` 명령](../tools/cli-ref-setapikey.md)으로 설정된 대로 API 키 인증을 사용하는 원본에 대한 키를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="98711-207">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="98711-208">Key</span><span class="sxs-lookup"><span data-stu-id="98711-208">Key</span></span> | <span data-ttu-id="98711-209">값</span><span class="sxs-lookup"><span data-stu-id="98711-209">Value</span></span> |
| --- | --- |
| <span data-ttu-id="98711-210">(원본 URL)</span><span class="sxs-lookup"><span data-stu-id="98711-210">(source URL)</span></span> | <span data-ttu-id="98711-211">암호화된 API 키입니다.</span><span class="sxs-lookup"><span data-stu-id="98711-211">The encrypted API key.</span></span> |

<span data-ttu-id="98711-212">**예제**:</span><span class="sxs-lookup"><span data-stu-id="98711-212">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="98711-213">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="98711-213">disabledPackageSources</span></span>

<span data-ttu-id="98711-214">현재 사용할 수 없는 원본을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="98711-214">Identified currently disabled sources.</span></span> <span data-ttu-id="98711-215">비어 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98711-215">May be empty.</span></span>

| <span data-ttu-id="98711-216">Key</span><span class="sxs-lookup"><span data-stu-id="98711-216">Key</span></span> | <span data-ttu-id="98711-217">값</span><span class="sxs-lookup"><span data-stu-id="98711-217">Value</span></span> |
| --- | --- |
| <span data-ttu-id="98711-218">(원본 이름)</span><span class="sxs-lookup"><span data-stu-id="98711-218">(name of source)</span></span> | <span data-ttu-id="98711-219">원본을 사용할 수 없는지 여부를 나타내는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="98711-219">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="98711-220">**예제:**</span><span class="sxs-lookup"><span data-stu-id="98711-220">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="98711-221">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="98711-221">activePackageSource</span></span>

<span data-ttu-id="98711-222">*(2.x만, 3.x 이상에서는 사용되지 않음)*</span><span class="sxs-lookup"><span data-stu-id="98711-222">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="98711-223">현재 활성 중인 원본을 식별하거나 모든 원본의 집계를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="98711-223">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="98711-224">Key</span><span class="sxs-lookup"><span data-stu-id="98711-224">Key</span></span> | <span data-ttu-id="98711-225">값</span><span class="sxs-lookup"><span data-stu-id="98711-225">Value</span></span> |
| --- | --- |
| <span data-ttu-id="98711-226">(원본 이름) 또는 `All`</span><span class="sxs-lookup"><span data-stu-id="98711-226">(name of source) or `All`</span></span> | <span data-ttu-id="98711-227">키가 원본의 이름이면 값은 원본 경로 또는 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="98711-227">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="98711-228">`All`이면 값은 `(Aggregate source)`여야 하며, 그렇지 않으면 사용할 수 없는 모든 패키지 원본이 결합됩니다.</span><span class="sxs-lookup"><span data-stu-id="98711-228">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="98711-229">**예제**:</span><span class="sxs-lookup"><span data-stu-id="98711-229">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="using-environment-variables"></a><span data-ttu-id="98711-230">환경 변수 사용</span><span class="sxs-lookup"><span data-stu-id="98711-230">Using environment variables</span></span>

<span data-ttu-id="98711-231">`NuGet.Config` 값(NuGet 3.4 이상)의 환경 변수를 사용하여 런타임에 설정을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98711-231">You can use environment variables in `NuGet.Config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="98711-232">예를 들어 Windows의 `HOME` 환경 변수가 `c:\users\username`으로 설정되면 구성 파일의 `%HOME%\NuGetRepository` 값이 `c:\users\username\NuGetRepository`로 해석됩니다.</span><span class="sxs-lookup"><span data-stu-id="98711-232">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="98711-233">마찬가지로, Mac/Linux의 `HOME`이 `/home/myStuff`로 설정되면 구성 파일의 `$HOME/NuGetRepository`가 `/home/myStuff/NuGetRepository`로 해석됩니다.</span><span class="sxs-lookup"><span data-stu-id="98711-233">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `$HOME/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="98711-234">환경 변수가 없으면 NuGet에서 구성 파일의 리터럴 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="98711-234">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="98711-235">config 파일 예제</span><span class="sxs-lookup"><span data-stu-id="98711-235">Example config file</span></span>

<span data-ttu-id="98711-236">아래는 몇 가지 설정을 보여 주는 `NuGet.Config` 파일의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="98711-236">Below is an example `NuGet.Config` file that illustrates a number of settings:</span></span>

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
