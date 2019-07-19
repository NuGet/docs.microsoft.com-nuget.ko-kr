---
title: nuget .config 파일 참조
description: config, bindingRedirects, packageRestore, solution 및 packageSource 섹션이 포함된 NuGet.Config 파일 참조입니다.
author: karann-msft
ms.author: karann
ms.date: 10/25/2017
ms.topic: reference
ms.openlocfilehash: b03bb8da0191a679671e5898ac70fff2024d52f2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317213"
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="0e5d7-103">nuget.exe 참조</span><span class="sxs-lookup"><span data-stu-id="0e5d7-103">nuget.config reference</span></span>

<span data-ttu-id="0e5d7-104">Nuget 동작은 [일반적인 nuget 구성](../consume-packages/configuring-nuget-behavior.md)에 설명 된 `NuGet.Config` 대로 다른 파일의 설정에 의해 제어 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-104">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="0e5d7-105">`nuget.config`는 최상위 `<configuration>` 노드를 포함하는 XML 파일이며, 이 파일에는 이 항목에서 설명하는 섹션 요소가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-105">`nuget.config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="0e5d7-106">각 섹션에는 0 개 이상의 항목이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-106">Each section contains zero or more items.</span></span> <span data-ttu-id="0e5d7-107">[config 파일 예제](#example-config-file)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="0e5d7-108">설정 이름은 대/소문자를 구분하지 않으며, 값에는 [환경 변수](#using-environment-variables)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<span data-ttu-id="0e5d7-109">항목 내용</span><span class="sxs-lookup"><span data-stu-id="0e5d7-109">In this topic:</span></span>

- [<span data-ttu-id="0e5d7-110">config 섹션</span><span class="sxs-lookup"><span data-stu-id="0e5d7-110">config section</span></span>](#config-section)
- [<span data-ttu-id="0e5d7-111">bindingRedirects 섹션</span><span class="sxs-lookup"><span data-stu-id="0e5d7-111">bindingRedirects section</span></span>](#bindingredirects-section)
- [<span data-ttu-id="0e5d7-112">packageRestore 섹션</span><span class="sxs-lookup"><span data-stu-id="0e5d7-112">packageRestore section</span></span>](#packagerestore-section)
- [<span data-ttu-id="0e5d7-113">solution 섹션</span><span class="sxs-lookup"><span data-stu-id="0e5d7-113">solution section</span></span>](#solution-section)
- <span data-ttu-id="0e5d7-114">[패키지 원본 섹션](#package-source-sections):</span><span class="sxs-lookup"><span data-stu-id="0e5d7-114">[Package source sections](#package-source-sections):</span></span>
  - [<span data-ttu-id="0e5d7-115">packageSources</span><span class="sxs-lookup"><span data-stu-id="0e5d7-115">packageSources</span></span>](#packagesources)
  - [<span data-ttu-id="0e5d7-116">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="0e5d7-116">packageSourceCredentials</span></span>](#packagesourcecredentials)
  - [<span data-ttu-id="0e5d7-117">apikeys</span><span class="sxs-lookup"><span data-stu-id="0e5d7-117">apikeys</span></span>](#apikeys)
  - [<span data-ttu-id="0e5d7-118">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="0e5d7-118">disabledPackageSources</span></span>](#disabledpackagesources)
  - [<span data-ttu-id="0e5d7-119">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="0e5d7-119">activePackageSource</span></span>](#activepackagesource)
- [<span data-ttu-id="0e5d7-120">해당 서명자 섹션</span><span class="sxs-lookup"><span data-stu-id="0e5d7-120">trustedSigners section</span></span>](#trustedsigners-section)
- [<span data-ttu-id="0e5d7-121">환경 변수 사용</span><span class="sxs-lookup"><span data-stu-id="0e5d7-121">Using environment variables</span></span>](#using-environment-variables)
- [<span data-ttu-id="0e5d7-122">config 파일 예제</span><span class="sxs-lookup"><span data-stu-id="0e5d7-122">Example config file</span></span>](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="0e5d7-123">config 섹션</span><span class="sxs-lookup"><span data-stu-id="0e5d7-123">config section</span></span>

<span data-ttu-id="0e5d7-124">[`nuget config` 명령](../reference/cli-reference/cli-ref-config.md)을 사용하여 설정할 수 있는 기타 구성 설정을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-124">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../reference/cli-reference/cli-ref-config.md).</span></span>

<span data-ttu-id="0e5d7-125">`dependencyVersion`및 `repositoryPath` 는를 사용 하 `packages.config`는 프로젝트에만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-125">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="0e5d7-126">`globalPackagesFolder`PackageReference 형식을 사용 하는 프로젝트에만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-126">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="0e5d7-127">Key</span><span class="sxs-lookup"><span data-stu-id="0e5d7-127">Key</span></span> | <span data-ttu-id="0e5d7-128">값</span><span class="sxs-lookup"><span data-stu-id="0e5d7-128">Value</span></span> |
| --- | --- |
| <span data-ttu-id="0e5d7-129">dependencyVersion(`packages.config`만)</span><span class="sxs-lookup"><span data-stu-id="0e5d7-129">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="0e5d7-130">`-DependencyVersion` 스위치가 직접 지정되지 않은 경우 패키지 설치, 복원 및 업데이트에 대한 기본 `DependencyVersion` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-130">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="0e5d7-131">이 값은 NuGet 패키지 관리자 UI에서도 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-131">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="0e5d7-132">값은 `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`입니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-132">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="0e5d7-133">globalPackagesFolder (PackageReference만 사용 하는 프로젝트)</span><span class="sxs-lookup"><span data-stu-id="0e5d7-133">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="0e5d7-134">기본 전역 패키지 폴더의 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-134">The location of the default global packages folder.</span></span> <span data-ttu-id="0e5d7-135">기본값은 `%userprofile%\.nuget\packages`(Windows) 또는 `~/.nuget/packages`(Mac/Linux)입니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-135">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="0e5d7-136">상대 경로는 프로젝트별 `nuget.config` 파일에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-136">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="0e5d7-137">이 설정은 NUGET_PACKAGES 환경 변수에 의해 재정의 되며이는 우선적으로 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-137">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="0e5d7-138">repositoryPath(`packages.config`만)</span><span class="sxs-lookup"><span data-stu-id="0e5d7-138">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="0e5d7-139">기본 `$(Solutiondir)/packages` 폴더 대신 NuGet 패키지를 설치할 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-139">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="0e5d7-140">상대 경로는 프로젝트별 `nuget.config` 파일에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-140">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="0e5d7-141">이 설정은 NUGET_PACKAGES 환경 변수에 의해 재정의 되며이는 우선적으로 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-141">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="0e5d7-142">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="0e5d7-142">defaultPushSource</span></span> | <span data-ttu-id="0e5d7-143">작업에 대한 다른 패키지 원본이 없을 때 기본값으로 사용해야 하는 패키지 원본의 URL 또는 경로를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-143">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="0e5d7-144">http_proxy, http_proxy.user, http_proxy.password, no_proxy</span><span class="sxs-lookup"><span data-stu-id="0e5d7-144">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="0e5d7-145">패키지 원본에 연결할 때 사용할 프록시 설정입니다. `http_proxy`는 `http://<username>:<password>@<domain>` 형식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-145">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="0e5d7-146">암호는 암호화되어 있으며, 수동으로 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-146">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="0e5d7-147">`no_proxy`의 경우 값은 프록시 서버를 우회하는 도메인의 쉼표로 구분된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-147">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="0e5d7-148">이러한 값에 대해 http_proxy 및 no_proxy 환경 변수를 번갈아 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-148">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="0e5d7-149">자세한 내용은 [NuGet 프록시 설정](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html)(skolima.blogspot.com)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-149">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |
| <span data-ttu-id="0e5d7-150">signatureValidationMode</span><span class="sxs-lookup"><span data-stu-id="0e5d7-150">signatureValidationMode</span></span> | <span data-ttu-id="0e5d7-151">패키지 설치 및 복원에 대 한 패키지 서명을 확인 하는 데 사용 되는 유효성 검사 모드를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-151">Specifies the validation mode used to verify package signatures for package install, and restore.</span></span> <span data-ttu-id="0e5d7-152">값은 `accept`, `require`입니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-152">Values are `accept`, `require`.</span></span> <span data-ttu-id="0e5d7-153">기본값은 `accept`입니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-153">Defaults to `accept`.</span></span>

<span data-ttu-id="0e5d7-154">**예제**:</span><span class="sxs-lookup"><span data-stu-id="0e5d7-154">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="0e5d7-155">bindingRedirects 섹션</span><span class="sxs-lookup"><span data-stu-id="0e5d7-155">bindingRedirects section</span></span>

<span data-ttu-id="0e5d7-156">패키지가 설치될 때 NuGet에서 자동 바인딩 리디렉션을 수행할지 여부를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-156">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="0e5d7-157">Key</span><span class="sxs-lookup"><span data-stu-id="0e5d7-157">Key</span></span> | <span data-ttu-id="0e5d7-158">값</span><span class="sxs-lookup"><span data-stu-id="0e5d7-158">Value</span></span> |
| --- | --- |
| <span data-ttu-id="0e5d7-159">skip</span><span class="sxs-lookup"><span data-stu-id="0e5d7-159">skip</span></span> | <span data-ttu-id="0e5d7-160">자동 바인딩 리디렉션을 건너뛸지 여부를 나타내는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-160">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="0e5d7-161">기본값은 false입니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-161">The default is false.</span></span> |

<span data-ttu-id="0e5d7-162">**예제**:</span><span class="sxs-lookup"><span data-stu-id="0e5d7-162">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="0e5d7-163">packageRestore 섹션</span><span class="sxs-lookup"><span data-stu-id="0e5d7-163">packageRestore section</span></span>

<span data-ttu-id="0e5d7-164">빌드하는 동안의 패키지 복원을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-164">Controls package restore during builds.</span></span>

| <span data-ttu-id="0e5d7-165">Key</span><span class="sxs-lookup"><span data-stu-id="0e5d7-165">Key</span></span> | <span data-ttu-id="0e5d7-166">값</span><span class="sxs-lookup"><span data-stu-id="0e5d7-166">Value</span></span> |
| --- | --- |
| <span data-ttu-id="0e5d7-167">사용</span><span class="sxs-lookup"><span data-stu-id="0e5d7-167">enabled</span></span> | <span data-ttu-id="0e5d7-168">NuGet에서 자동 복원을 수행할 수 있는지 여부를 나타내는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-168">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="0e5d7-169">config 파일에서 이 키를 설정하는 대신 `EnableNuGetPackageRestore` 환경 변수를 `True` 값으로 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-169">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="0e5d7-170">자동</span><span class="sxs-lookup"><span data-stu-id="0e5d7-170">automatic</span></span> | <span data-ttu-id="0e5d7-171">NuGet에서 빌드하는 동안 누락된 패키지를 확인해야 하는지 여부를 나타내는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-171">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="0e5d7-172">**예제**:</span><span class="sxs-lookup"><span data-stu-id="0e5d7-172">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="0e5d7-173">solution 섹션</span><span class="sxs-lookup"><span data-stu-id="0e5d7-173">solution section</span></span>

<span data-ttu-id="0e5d7-174">솔루션의 `packages` 폴더가 원본 제어에 포함되는지 여부를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-174">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="0e5d7-175">이 섹션은 솔루션 폴더의 `nuget.config` 파일에서만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-175">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="0e5d7-176">Key</span><span class="sxs-lookup"><span data-stu-id="0e5d7-176">Key</span></span> | <span data-ttu-id="0e5d7-177">값</span><span class="sxs-lookup"><span data-stu-id="0e5d7-177">Value</span></span> |
| --- | --- |
| <span data-ttu-id="0e5d7-178">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="0e5d7-178">disableSourceControlIntegration</span></span> | <span data-ttu-id="0e5d7-179">원본 제어로 작업할 때 패키지 폴더를 무시할지 여부를 나타내는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-179">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="0e5d7-180">기본값은 false입니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-180">The default value is false.</span></span> |

<span data-ttu-id="0e5d7-181">**예제**:</span><span class="sxs-lookup"><span data-stu-id="0e5d7-181">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="0e5d7-182">패키지 원본 섹션</span><span class="sxs-lookup"><span data-stu-id="0e5d7-182">Package source sections</span></span>

<span data-ttu-id="0e5d7-183">`packageSources` ,`packageSourceCredentials`, ,`trustedSigners` 및는 모두 함께 작동 하 여 설치, 복원 및 업데이트 작업 중에 NuGet이 패키지 리포지토리와 함께 작동 하는 방식을 구성 합니다. `activePackageSource` `apikeys` `disabledPackageSources`</span><span class="sxs-lookup"><span data-stu-id="0e5d7-183">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` and `trustedSigners` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="0e5d7-184">[명령은 명령을 사용 하 여`nuget setapikey` ](../reference/cli-reference/cli-ref-setapikey.md)관리 되 고 `apikeys` `trustedSigners` [명령을 사용 하 여 관리 되는를 제외 하 고는 일반적으로 이러한 설정을 관리 하는 `nuget trusted-signers` ](../reference/cli-reference/cli-ref-trusted-signers.md)데 사용 됩니다. [ `nuget sources` ](../reference/cli-reference/cli-ref-sources.md)</span><span class="sxs-lookup"><span data-stu-id="0e5d7-184">The [`nuget sources` command](../reference/cli-reference/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md), and `trustedSigners` which is managed using the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="0e5d7-185">nuget.org에 대한 원본 URL은 `https://api.nuget.org/v3/index.json`입니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-185">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="0e5d7-186">packageSources</span><span class="sxs-lookup"><span data-stu-id="0e5d7-186">packageSources</span></span>

<span data-ttu-id="0e5d7-187">알려진 모든 패키지 원본을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-187">Lists all known package sources.</span></span> <span data-ttu-id="0e5d7-188">PackageReference 형식을 사용 하는 모든 프로젝트와 복원 작업 중에 순서는 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-188">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="0e5d7-189">NuGet은를 사용 하 여 `packages.config`프로젝트에 대 한 설치 및 업데이트 작업의 소스 순서를 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-189">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="0e5d7-190">Key</span><span class="sxs-lookup"><span data-stu-id="0e5d7-190">Key</span></span> | <span data-ttu-id="0e5d7-191">값</span><span class="sxs-lookup"><span data-stu-id="0e5d7-191">Value</span></span> |
| --- | --- |
| <span data-ttu-id="0e5d7-192">(패키지 원본에 할당할 이름)</span><span class="sxs-lookup"><span data-stu-id="0e5d7-192">(name to assign to the package source)</span></span> | <span data-ttu-id="0e5d7-193">패키지 원본의 경로 또는 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-193">The path or URL of the package source.</span></span> |

<span data-ttu-id="0e5d7-194">**예제**:</span><span class="sxs-lookup"><span data-stu-id="0e5d7-194">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="0e5d7-195">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="0e5d7-195">packageSourceCredentials</span></span>

<span data-ttu-id="0e5d7-196">원본에 대한 사용자 이름과 암호를 저장하며, 일반적으로 `nuget sources`와 함께 `-username` 및 `-password` 스위치로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-196">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="0e5d7-197">또한 `-storepasswordincleartext` 옵션을 사용하지 않는 한 암호는 기본적으로 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-197">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="0e5d7-198">Key</span><span class="sxs-lookup"><span data-stu-id="0e5d7-198">Key</span></span> | <span data-ttu-id="0e5d7-199">값</span><span class="sxs-lookup"><span data-stu-id="0e5d7-199">Value</span></span> |
| --- | --- |
| <span data-ttu-id="0e5d7-200">사용자 이름</span><span class="sxs-lookup"><span data-stu-id="0e5d7-200">username</span></span> | <span data-ttu-id="0e5d7-201">일반 텍스트 형식의 원본에 대한 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-201">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="0e5d7-202">password</span><span class="sxs-lookup"><span data-stu-id="0e5d7-202">password</span></span> | <span data-ttu-id="0e5d7-203">원본에 대한 암호화된 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-203">The encrypted password for the source.</span></span> |
| <span data-ttu-id="0e5d7-204">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="0e5d7-204">cleartextpassword</span></span> | <span data-ttu-id="0e5d7-205">원본에 대한 암호화되지 않은 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-205">The unencrypted password for the source.</span></span> |

<span data-ttu-id="0e5d7-206">**예제:**</span><span class="sxs-lookup"><span data-stu-id="0e5d7-206">**Example:**</span></span>

<span data-ttu-id="0e5d7-207">config 파일에서 `<packageSourceCredentials>` 요소에는 적용 가능한 원본 이름 각각에 대한 자식 노드가 포함됩니다(이름에 포함된 공백은 `_x0020_`로 바뀜).</span><span class="sxs-lookup"><span data-stu-id="0e5d7-207">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="0e5d7-208">즉 "Contoso" 및 "Test Source"라는 원본의 경우 암호화된 암호를 사용하면 config 파일에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-208">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="0e5d7-209">암호화되지 않은 암호를 사용하는 경우:</span><span class="sxs-lookup"><span data-stu-id="0e5d7-209">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="0e5d7-210">apikeys</span><span class="sxs-lookup"><span data-stu-id="0e5d7-210">apikeys</span></span>

<span data-ttu-id="0e5d7-211">[`nuget setapikey` 명령](../reference/cli-reference/cli-ref-setapikey.md)으로 설정된 대로 API 키 인증을 사용하는 원본에 대한 키를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-211">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="0e5d7-212">Key</span><span class="sxs-lookup"><span data-stu-id="0e5d7-212">Key</span></span> | <span data-ttu-id="0e5d7-213">값</span><span class="sxs-lookup"><span data-stu-id="0e5d7-213">Value</span></span> |
| --- | --- |
| <span data-ttu-id="0e5d7-214">(원본 URL)</span><span class="sxs-lookup"><span data-stu-id="0e5d7-214">(source URL)</span></span> | <span data-ttu-id="0e5d7-215">암호화된 API 키입니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-215">The encrypted API key.</span></span> |

<span data-ttu-id="0e5d7-216">**예제**:</span><span class="sxs-lookup"><span data-stu-id="0e5d7-216">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="0e5d7-217">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="0e5d7-217">disabledPackageSources</span></span>

<span data-ttu-id="0e5d7-218">현재 사용할 수 없는 원본을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-218">Identified currently disabled sources.</span></span> <span data-ttu-id="0e5d7-219">비어 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-219">May be empty.</span></span>

| <span data-ttu-id="0e5d7-220">Key</span><span class="sxs-lookup"><span data-stu-id="0e5d7-220">Key</span></span> | <span data-ttu-id="0e5d7-221">값</span><span class="sxs-lookup"><span data-stu-id="0e5d7-221">Value</span></span> |
| --- | --- |
| <span data-ttu-id="0e5d7-222">(원본 이름)</span><span class="sxs-lookup"><span data-stu-id="0e5d7-222">(name of source)</span></span> | <span data-ttu-id="0e5d7-223">원본을 사용할 수 없는지 여부를 나타내는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-223">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="0e5d7-224">**예제:**</span><span class="sxs-lookup"><span data-stu-id="0e5d7-224">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="0e5d7-225">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="0e5d7-225">activePackageSource</span></span>

<span data-ttu-id="0e5d7-226">*(2.x만, 3.x 이상에서는 사용되지 않음)*</span><span class="sxs-lookup"><span data-stu-id="0e5d7-226">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="0e5d7-227">현재 활성 중인 원본을 식별하거나 모든 원본의 집계를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-227">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="0e5d7-228">Key</span><span class="sxs-lookup"><span data-stu-id="0e5d7-228">Key</span></span> | <span data-ttu-id="0e5d7-229">값</span><span class="sxs-lookup"><span data-stu-id="0e5d7-229">Value</span></span> |
| --- | --- |
| <span data-ttu-id="0e5d7-230">(원본 이름) 또는 `All`</span><span class="sxs-lookup"><span data-stu-id="0e5d7-230">(name of source) or `All`</span></span> | <span data-ttu-id="0e5d7-231">키가 원본의 이름이면 값은 원본 경로 또는 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-231">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="0e5d7-232">`All`이면 값은 `(Aggregate source)`여야 하며, 그렇지 않으면 사용할 수 없는 모든 패키지 원본이 결합됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-232">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="0e5d7-233">**예제**:</span><span class="sxs-lookup"><span data-stu-id="0e5d7-233">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```
## <a name="trustedsigners-section"></a><span data-ttu-id="0e5d7-234">해당 서명자 섹션</span><span class="sxs-lookup"><span data-stu-id="0e5d7-234">trustedSigners section</span></span>

<span data-ttu-id="0e5d7-235">설치 또는 복원 중 패키지를 허용 하는 데 사용 되는 신뢰할 수 있는 서명자를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-235">Stores trusted signers used to allow package while installing or restoring.</span></span> <span data-ttu-id="0e5d7-236">사용자가로 설정 `signatureValidationMode` 된 경우에 `require`는이 목록을 비워 둘 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-236">This list cannot be empty when the user sets `signatureValidationMode` to `require`.</span></span> 

<span data-ttu-id="0e5d7-237">이 섹션은 [ `nuget trusted-signers` 명령을](../reference/cli-reference/cli-ref-trusted-signers.md)사용 하 여 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-237">This section can be updated with the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="0e5d7-238">**스키마**:</span><span class="sxs-lookup"><span data-stu-id="0e5d7-238">**Schema**:</span></span>

<span data-ttu-id="0e5d7-239">신뢰할 수 있는 서명자는 지정 된 `certificate` 서명자를 식별 하는 모든 인증서를 등록 하는 항목의 컬렉션을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-239">A trusted signer has a collection of `certificate` items that enlist all the certificates that identify a given signer.</span></span> <span data-ttu-id="0e5d7-240">신뢰할 수 있는 서명자는 `Author` `Repository`또는 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-240">A trusted signer can be either an `Author` or a `Repository`.</span></span>

<span data-ttu-id="0e5d7-241">또한 신뢰할 수 있는 *리포지토리* 는 `serviceIndex` 유효한 `https` uri 여야 하는 리포지토리에 대 한을 지정 하 고, 선택적으로 세미콜론으로 구분 된 목록을 `owners` 지정 하 여 해당 특정에서 신뢰할 수 있는 사용자를 제한할 수 있습니다. 리포지토리로.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-241">A trusted *repository* also specifies the `serviceIndex` for the repository (which has to be a valid `https` uri) and can optionally specify a semi-colon delimited list of `owners` to restrict even more who is trusted from that specific repository.</span></span>

<span data-ttu-id="0e5d7-242">인증서 지문에 사용 되는 지원 되는 해시 `SHA256`알고리즘 `SHA384` 은 `SHA512`, 및입니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-242">The supported hash algorithms used for a certificate fingerprint are `SHA256`, `SHA384` and `SHA512`.</span></span>

<span data-ttu-id="0e5d7-243">가 `certificate` 서명 확인의 `true` 일부로 인증서 체인을 빌드하는 동안 지정 된 인증서를 신뢰할 수 없는 루트에 체인으로 연결할 수 있는 것으로 지정 `allowUntrustedRoot` 하면입니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-243">If a `certificate` specifies `allowUntrustedRoot` as `true` the given certificate is allowed to chain to an untrusted root while building the certificate chain as part of the signature verification.</span></span>

<span data-ttu-id="0e5d7-244">**예제**:</span><span class="sxs-lookup"><span data-stu-id="0e5d7-244">**Example**:</span></span>

```xml
<trustedSigners>
    <author name="microsoft">
        <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
    </author>
    <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
        <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <owners>microsoft;aspnet;nuget</owners>
    </repository>
</trustedSigners>
```

## <a name="using-environment-variables"></a><span data-ttu-id="0e5d7-245">환경 변수 사용</span><span class="sxs-lookup"><span data-stu-id="0e5d7-245">Using environment variables</span></span>

<span data-ttu-id="0e5d7-246">`nuget.config` 값(NuGet 3.4 이상)의 환경 변수를 사용하여 런타임에 설정을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-246">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="0e5d7-247">예를 들어 Windows의 `HOME` 환경 변수가 `c:\users\username`으로 설정되면 구성 파일의 `%HOME%\NuGetRepository` 값이 `c:\users\username\NuGetRepository`로 해석됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-247">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="0e5d7-248">마찬가지로, Mac/Linux의 `HOME`이 `/home/myStuff`로 설정되면 구성 파일의 `%HOME%/NuGetRepository`가 `/home/myStuff/NuGetRepository`로 해석됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-248">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `%HOME%/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="0e5d7-249">환경 변수가 없으면 NuGet에서 구성 파일의 리터럴 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-249">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="0e5d7-250">config 파일 예제</span><span class="sxs-lookup"><span data-stu-id="0e5d7-250">Example config file</span></span>

<span data-ttu-id="0e5d7-251">아래는 몇 가지 설정을 보여 주는 `nuget.config` 파일의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="0e5d7-251">Below is an example `nuget.config` file that illustrates a number of settings:</span></span>

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

    <!--
        Used to specify trusted signers to allow during signature verification.
        See: nuget.exe help trusted-signers
    -->
    <trustedSigners>
        <author name="microsoft">
            <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        </author>
        <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
            <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
            <owners>microsoft;aspnet;nuget</owners>
        </repository>
    </trustedSigners>
</configuration>
```
