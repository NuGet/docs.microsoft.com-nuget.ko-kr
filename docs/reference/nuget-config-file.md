---
title: nuget .config 파일 참조
description: config, bindingRedirects, packageRestore, solution 및 packageSource 섹션이 포함된 NuGet.Config 파일 참조입니다.
author: karann-msft
ms.author: karann
ms.date: 08/13/2019
ms.topic: reference
ms.openlocfilehash: cd321084c46709e3d1d22872c37485edacd33afa
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230528"
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="56e81-103">nuget.exe 참조</span><span class="sxs-lookup"><span data-stu-id="56e81-103">nuget.config reference</span></span>

<span data-ttu-id="56e81-104">NuGet 동작은 [일반적인 nuget 구성](../consume-packages/configuring-nuget-behavior.md)에 설명 된 대로 다른 `NuGet.Config` 또는 `nuget.config` 파일의 설정에 의해 제어 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-104">NuGet behavior is controlled by settings in different `NuGet.Config` or `nuget.config` files as described in [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="56e81-105">`nuget.config`는 최상위 `<configuration>` 노드를 포함하는 XML 파일이며, 이 파일에는 이 항목에서 설명하는 섹션 요소가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-105">`nuget.config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="56e81-106">각 섹션에는 0 개 이상의 항목이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-106">Each section contains zero or more items.</span></span> <span data-ttu-id="56e81-107">[config 파일 예제](#example-config-file)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56e81-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="56e81-108">설정 이름은 대/소문자를 구분하지 않으며, 값에는 [환경 변수](#using-environment-variables)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="56e81-109">config 섹션</span><span class="sxs-lookup"><span data-stu-id="56e81-109">config section</span></span>

<span data-ttu-id="56e81-110">[`nuget config` 명령](../reference/cli-reference/cli-ref-config.md)을 사용하여 설정할 수 있는 기타 구성 설정을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-110">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../reference/cli-reference/cli-ref-config.md).</span></span>

<span data-ttu-id="56e81-111">`dependencyVersion` 및 `repositoryPath` `packages.config`를 사용 하는 프로젝트에만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-111">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="56e81-112">`globalPackagesFolder` PackageReference 형식을 사용 하는 프로젝트에만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-112">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="56e81-113">키</span><span class="sxs-lookup"><span data-stu-id="56e81-113">Key</span></span> | <span data-ttu-id="56e81-114">값</span><span class="sxs-lookup"><span data-stu-id="56e81-114">Value</span></span> |
| --- | --- |
| <span data-ttu-id="56e81-115">dependencyVersion(`packages.config`만)</span><span class="sxs-lookup"><span data-stu-id="56e81-115">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="56e81-116">`DependencyVersion` 스위치가 직접 지정되지 않은 경우 패키지 설치, 복원 및 업데이트에 대한 기본 `-DependencyVersion` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-116">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="56e81-117">이 값은 NuGet 패키지 관리자 UI에서도 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-117">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="56e81-118">값은 `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`입니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-118">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="56e81-119">globalPackagesFolder (PackageReference만 사용 하는 프로젝트)</span><span class="sxs-lookup"><span data-stu-id="56e81-119">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="56e81-120">기본 전역 패키지 폴더의 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-120">The location of the default global packages folder.</span></span> <span data-ttu-id="56e81-121">기본값은 `%userprofile%\.nuget\packages`(Windows) 또는 `~/.nuget/packages`(Mac/Linux)입니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-121">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="56e81-122">상대 경로는 프로젝트별 `nuget.config` 파일에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-122">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="56e81-123">이 설정은 NUGET_PACKAGES 환경 변수에 의해 재정의 되며이는 우선적으로 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-123">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="56e81-124">repositoryPath(`packages.config`만)</span><span class="sxs-lookup"><span data-stu-id="56e81-124">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="56e81-125">기본 `$(Solutiondir)/packages` 폴더 대신 NuGet 패키지를 설치할 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-125">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="56e81-126">상대 경로는 프로젝트별 `nuget.config` 파일에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-126">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="56e81-127">이 설정은 NUGET_PACKAGES 환경 변수에 의해 재정의 되며이는 우선적으로 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-127">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="56e81-128">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="56e81-128">defaultPushSource</span></span> | <span data-ttu-id="56e81-129">작업에 대한 다른 패키지 원본이 없을 때 기본값으로 사용해야 하는 패키지 원본의 URL 또는 경로를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-129">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="56e81-130">http_proxy, http_proxy.user, http_proxy.password, no_proxy</span><span class="sxs-lookup"><span data-stu-id="56e81-130">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="56e81-131">패키지 원본에 연결할 때 사용할 프록시 설정입니다. `http_proxy`는 `http://<username>:<password>@<domain>` 형식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-131">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="56e81-132">암호는 암호화되어 있으며, 수동으로 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-132">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="56e81-133">`no_proxy`의 경우 값은 프록시 서버를 우회하는 도메인의 쉼표로 구분된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-133">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="56e81-134">이러한 값에 대해 http_proxy 및 no_proxy 환경 변수를 번갈아 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-134">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="56e81-135">자세한 내용은 [NuGet 프록시 설정](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html)(skolima.blogspot.com)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56e81-135">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |
| <span data-ttu-id="56e81-136">signatureValidationMode</span><span class="sxs-lookup"><span data-stu-id="56e81-136">signatureValidationMode</span></span> | <span data-ttu-id="56e81-137">패키지 설치 및 복원에 대 한 패키지 서명을 확인 하는 데 사용 되는 유효성 검사 모드를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-137">Specifies the validation mode used to verify package signatures for package install, and restore.</span></span> <span data-ttu-id="56e81-138">값은 `accept``require`입니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-138">Values are `accept`, `require`.</span></span> <span data-ttu-id="56e81-139">기본값은 `accept`입니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-139">Defaults to `accept`.</span></span>

<span data-ttu-id="56e81-140">**예**:</span><span class="sxs-lookup"><span data-stu-id="56e81-140">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="56e81-141">bindingRedirects 섹션</span><span class="sxs-lookup"><span data-stu-id="56e81-141">bindingRedirects section</span></span>

<span data-ttu-id="56e81-142">패키지가 설치될 때 NuGet에서 자동 바인딩 리디렉션을 수행할지 여부를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-142">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="56e81-143">키</span><span class="sxs-lookup"><span data-stu-id="56e81-143">Key</span></span> | <span data-ttu-id="56e81-144">값</span><span class="sxs-lookup"><span data-stu-id="56e81-144">Value</span></span> |
| --- | --- |
| <span data-ttu-id="56e81-145">skip</span><span class="sxs-lookup"><span data-stu-id="56e81-145">skip</span></span> | <span data-ttu-id="56e81-146">자동 바인딩 리디렉션을 건너뛸지 여부를 나타내는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-146">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="56e81-147">기본값은 false입니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-147">The default is false.</span></span> |

<span data-ttu-id="56e81-148">**예**:</span><span class="sxs-lookup"><span data-stu-id="56e81-148">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="56e81-149">packageRestore 섹션</span><span class="sxs-lookup"><span data-stu-id="56e81-149">packageRestore section</span></span>

<span data-ttu-id="56e81-150">빌드하는 동안의 패키지 복원을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-150">Controls package restore during builds.</span></span>

| <span data-ttu-id="56e81-151">키</span><span class="sxs-lookup"><span data-stu-id="56e81-151">Key</span></span> | <span data-ttu-id="56e81-152">값</span><span class="sxs-lookup"><span data-stu-id="56e81-152">Value</span></span> |
| --- | --- |
| <span data-ttu-id="56e81-153">사용</span><span class="sxs-lookup"><span data-stu-id="56e81-153">enabled</span></span> | <span data-ttu-id="56e81-154">NuGet에서 자동 복원을 수행할 수 있는지 여부를 나타내는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-154">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="56e81-155">config 파일에서 이 키를 설정하는 대신 `EnableNuGetPackageRestore` 환경 변수를 `True` 값으로 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-155">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="56e81-156">automatic</span><span class="sxs-lookup"><span data-stu-id="56e81-156">automatic</span></span> | <span data-ttu-id="56e81-157">NuGet에서 빌드하는 동안 누락된 패키지를 확인해야 하는지 여부를 나타내는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-157">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="56e81-158">**예**:</span><span class="sxs-lookup"><span data-stu-id="56e81-158">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="56e81-159">solution 섹션</span><span class="sxs-lookup"><span data-stu-id="56e81-159">solution section</span></span>

<span data-ttu-id="56e81-160">솔루션의 `packages` 폴더가 원본 제어에 포함되는지 여부를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-160">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="56e81-161">이 섹션은 솔루션 폴더의 `nuget.config` 파일에서만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-161">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="56e81-162">키</span><span class="sxs-lookup"><span data-stu-id="56e81-162">Key</span></span> | <span data-ttu-id="56e81-163">값</span><span class="sxs-lookup"><span data-stu-id="56e81-163">Value</span></span> |
| --- | --- |
| <span data-ttu-id="56e81-164">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="56e81-164">disableSourceControlIntegration</span></span> | <span data-ttu-id="56e81-165">원본 제어로 작업할 때 패키지 폴더를 무시할지 여부를 나타내는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-165">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="56e81-166">기본값은 False입니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-166">The default value is false.</span></span> |

<span data-ttu-id="56e81-167">**예**:</span><span class="sxs-lookup"><span data-stu-id="56e81-167">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="56e81-168">패키지 원본 섹션</span><span class="sxs-lookup"><span data-stu-id="56e81-168">Package source sections</span></span>

<span data-ttu-id="56e81-169">`packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` 및 `trustedSigners` 모두 함께 작동 하 여 설치, 복원 및 업데이트 작업 중에 NuGet이 패키지 리포지토리와 함께 작동 하는 방식을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-169">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` and `trustedSigners` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="56e81-170">[`nuget sources` 명령은](../reference/cli-reference/cli-ref-sources.md) 일반적으로 [`nuget setapikey` 명령을](../reference/cli-reference/cli-ref-setapikey.md)사용 하 여 관리 되는 `apikeys`를 제외 하 고 이러한 설정을 관리 하는 데 사용 되며 [`nuget trusted-signers` 명령을](../reference/cli-reference/cli-ref-trusted-signers.md)사용 하 여 관리 되는 `trustedSigners`.</span><span class="sxs-lookup"><span data-stu-id="56e81-170">The [`nuget sources` command](../reference/cli-reference/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md), and `trustedSigners` which is managed using the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="56e81-171">nuget.org에 대한 원본 URL은 `https://api.nuget.org/v3/index.json`입니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-171">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="56e81-172">packageSources</span><span class="sxs-lookup"><span data-stu-id="56e81-172">packageSources</span></span>

<span data-ttu-id="56e81-173">알려진 모든 패키지 원본을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-173">Lists all known package sources.</span></span> <span data-ttu-id="56e81-174">PackageReference 형식을 사용 하는 모든 프로젝트와 복원 작업 중에 순서는 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-174">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="56e81-175">NuGet은 `packages.config`를 사용 하 여 프로젝트를 사용 하 여 설치 및 업데이트 작업을 위한 원본 순서를 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-175">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="56e81-176">키</span><span class="sxs-lookup"><span data-stu-id="56e81-176">Key</span></span> | <span data-ttu-id="56e81-177">값</span><span class="sxs-lookup"><span data-stu-id="56e81-177">Value</span></span> |
| --- | --- |
| <span data-ttu-id="56e81-178">(패키지 원본에 할당할 이름)</span><span class="sxs-lookup"><span data-stu-id="56e81-178">(name to assign to the package source)</span></span> | <span data-ttu-id="56e81-179">패키지 원본의 경로 또는 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-179">The path or URL of the package source.</span></span> |

<span data-ttu-id="56e81-180">**예**:</span><span class="sxs-lookup"><span data-stu-id="56e81-180">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

> [!Tip]
> <span data-ttu-id="56e81-181">지정된 노드에 대해 `<clear />`가 있으면 NuGet은 해당 노드에 대해 이전에 정의된 구성 값을 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-181">When `<clear />` is present for a given node, NuGet ignores previously defined configuration values for that node.</span></span> <span data-ttu-id="56e81-182">[설정이 적용 되는 방법에 대해 자세히](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied)알아보세요.</span><span class="sxs-lookup"><span data-stu-id="56e81-182">[Read more about how settings are applied](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).</span></span>

### <a name="packagesourcecredentials"></a><span data-ttu-id="56e81-183">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="56e81-183">packageSourceCredentials</span></span>

<span data-ttu-id="56e81-184">원본에 대한 사용자 이름과 암호를 저장하며, 일반적으로 `-username`와 함께 `-password` 및 `nuget sources` 스위치로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-184">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="56e81-185">또한 `-storepasswordincleartext` 옵션을 사용하지 않는 한 암호는 기본적으로 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-185">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="56e81-186">키</span><span class="sxs-lookup"><span data-stu-id="56e81-186">Key</span></span> | <span data-ttu-id="56e81-187">값</span><span class="sxs-lookup"><span data-stu-id="56e81-187">Value</span></span> |
| --- | --- |
| <span data-ttu-id="56e81-188">사용자 이름</span><span class="sxs-lookup"><span data-stu-id="56e81-188">username</span></span> | <span data-ttu-id="56e81-189">일반 텍스트 형식의 원본에 대한 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-189">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="56e81-190">password</span><span class="sxs-lookup"><span data-stu-id="56e81-190">password</span></span> | <span data-ttu-id="56e81-191">원본에 대한 암호화된 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-191">The encrypted password for the source.</span></span> |
| <span data-ttu-id="56e81-192">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="56e81-192">cleartextpassword</span></span> | <span data-ttu-id="56e81-193">원본에 대한 암호화되지 않은 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-193">The unencrypted password for the source.</span></span> |

<span data-ttu-id="56e81-194">**예:**</span><span class="sxs-lookup"><span data-stu-id="56e81-194">**Example:**</span></span>

<span data-ttu-id="56e81-195">config 파일에서 `<packageSourceCredentials>` 요소에는 적용 가능한 원본 이름 각각에 대한 자식 노드가 포함됩니다(이름에 포함된 공백은 `_x0020_`로 바뀜).</span><span class="sxs-lookup"><span data-stu-id="56e81-195">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="56e81-196">즉 "Contoso" 및 "Test Source"라는 원본의 경우 암호화된 암호를 사용하면 config 파일에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-196">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="56e81-197">암호화되지 않은 암호를 사용하는 경우:</span><span class="sxs-lookup"><span data-stu-id="56e81-197">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="56e81-198">apikeys</span><span class="sxs-lookup"><span data-stu-id="56e81-198">apikeys</span></span>

<span data-ttu-id="56e81-199">[`nuget setapikey` 명령](../reference/cli-reference/cli-ref-setapikey.md)으로 설정된 대로 API 키 인증을 사용하는 원본에 대한 키를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-199">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="56e81-200">키</span><span class="sxs-lookup"><span data-stu-id="56e81-200">Key</span></span> | <span data-ttu-id="56e81-201">값</span><span class="sxs-lookup"><span data-stu-id="56e81-201">Value</span></span> |
| --- | --- |
| <span data-ttu-id="56e81-202">(원본 URL)</span><span class="sxs-lookup"><span data-stu-id="56e81-202">(source URL)</span></span> | <span data-ttu-id="56e81-203">암호화된 API 키입니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-203">The encrypted API key.</span></span> |

<span data-ttu-id="56e81-204">**예**:</span><span class="sxs-lookup"><span data-stu-id="56e81-204">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="56e81-205">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="56e81-205">disabledPackageSources</span></span>

<span data-ttu-id="56e81-206">현재 사용할 수 없는 원본을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-206">Identified currently disabled sources.</span></span> <span data-ttu-id="56e81-207">비어 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-207">May be empty.</span></span>

| <span data-ttu-id="56e81-208">키</span><span class="sxs-lookup"><span data-stu-id="56e81-208">Key</span></span> | <span data-ttu-id="56e81-209">값</span><span class="sxs-lookup"><span data-stu-id="56e81-209">Value</span></span> |
| --- | --- |
| <span data-ttu-id="56e81-210">(원본 이름)</span><span class="sxs-lookup"><span data-stu-id="56e81-210">(name of source)</span></span> | <span data-ttu-id="56e81-211">원본을 사용할 수 없는지 여부를 나타내는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-211">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="56e81-212">**예:**</span><span class="sxs-lookup"><span data-stu-id="56e81-212">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="56e81-213">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="56e81-213">activePackageSource</span></span>

<span data-ttu-id="56e81-214">*(2.x만, 3.x 이상에서는 사용되지 않음)*</span><span class="sxs-lookup"><span data-stu-id="56e81-214">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="56e81-215">현재 활성 중인 원본을 식별하거나 모든 원본의 집계를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-215">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="56e81-216">키</span><span class="sxs-lookup"><span data-stu-id="56e81-216">Key</span></span> | <span data-ttu-id="56e81-217">값</span><span class="sxs-lookup"><span data-stu-id="56e81-217">Value</span></span> |
| --- | --- |
| <span data-ttu-id="56e81-218">(원본 이름) 또는 `All`</span><span class="sxs-lookup"><span data-stu-id="56e81-218">(name of source) or `All`</span></span> | <span data-ttu-id="56e81-219">키가 원본의 이름이면 값은 원본 경로 또는 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-219">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="56e81-220">`All`이면 값은 `(Aggregate source)`여야 하며, 그렇지 않으면 사용할 수 없는 모든 패키지 원본이 결합됩니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-220">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="56e81-221">**예**:</span><span class="sxs-lookup"><span data-stu-id="56e81-221">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="trustedsigners-section"></a><span data-ttu-id="56e81-222">해당 서명자 섹션</span><span class="sxs-lookup"><span data-stu-id="56e81-222">trustedSigners section</span></span>

<span data-ttu-id="56e81-223">설치 또는 복원 중 패키지를 허용 하는 데 사용 되는 신뢰할 수 있는 서명자를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-223">Stores trusted signers used to allow package while installing or restoring.</span></span> <span data-ttu-id="56e81-224">사용자가 `require``signatureValidationMode` 설정 하면이 목록은 비워 둘 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-224">This list cannot be empty when the user sets `signatureValidationMode` to `require`.</span></span> 

<span data-ttu-id="56e81-225">이 섹션은 [`nuget trusted-signers` 명령을](../reference/cli-reference/cli-ref-trusted-signers.md)사용 하 여 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-225">This section can be updated with the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="56e81-226">**스키마**:</span><span class="sxs-lookup"><span data-stu-id="56e81-226">**Schema**:</span></span>

<span data-ttu-id="56e81-227">신뢰할 수 있는 서명자는 지정 된 서명자를 식별 하는 모든 인증서를 등록 하는 `certificate` 항목의 컬렉션을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-227">A trusted signer has a collection of `certificate` items that enlist all the certificates that identify a given signer.</span></span> <span data-ttu-id="56e81-228">신뢰할 수 있는 서명자는 `Author` 또는 `Repository`일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-228">A trusted signer can be either an `Author` or a `Repository`.</span></span>

<span data-ttu-id="56e81-229">또한 신뢰할 수 있는 *리포지토리* 는 유효한 `https` uri 여야 하는 리포지토리에 대 한 `serviceIndex`를 지정 하 고 선택적으로 세미콜론으로 구분 된 `owners` 목록을 지정 하 여 해당 특정 리포지토리에서 신뢰할 수 있는 사용자를 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-229">A trusted *repository* also specifies the `serviceIndex` for the repository (which has to be a valid `https` uri) and can optionally specify a semi-colon delimited list of `owners` to restrict even more who is trusted from that specific repository.</span></span>

<span data-ttu-id="56e81-230">인증서 지문에 사용 되는 지원 되는 해시 알고리즘은 `SHA256`, `SHA384` 및 `SHA512`입니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-230">The supported hash algorithms used for a certificate fingerprint are `SHA256`, `SHA384` and `SHA512`.</span></span>

<span data-ttu-id="56e81-231">`certificate` `true` `allowUntrustedRoot` 지정 된 경우 서명 확인의 일부로 인증서 체인을 빌드하는 동안 지정 된 인증서를 신뢰할 수 없는 루트에 체인으로 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-231">If a `certificate` specifies `allowUntrustedRoot` as `true` the given certificate is allowed to chain to an untrusted root while building the certificate chain as part of the signature verification.</span></span>

<span data-ttu-id="56e81-232">**예**:</span><span class="sxs-lookup"><span data-stu-id="56e81-232">**Example**:</span></span>

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

## <a name="fallbackpackagefolders-section"></a><span data-ttu-id="56e81-233">fallbackPackageFolders 섹션</span><span class="sxs-lookup"><span data-stu-id="56e81-233">fallbackPackageFolders section</span></span>

<span data-ttu-id="56e81-234">*(3.5 +)* 는 패키지가 대체 폴더에 있는 경우 작업을 수행 하지 않아도 되도록 패키지를 사전 설치 하는 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-234">*(3.5+)* Provides a way to preinstall packages so that no work needs to be done if the package is found in the fallback folders.</span></span> <span data-ttu-id="56e81-235">대체 패키지 폴더는 전역 패키지 폴더와 정확히 같은 폴더 및 파일 구조를 포함 합니다. *. nupkg* 가 있고 모든 파일이 추출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-235">Fallback package folders have the exact same folder and file structure as the global package folder: *.nupkg* is present, and all files are extracted.</span></span>

<span data-ttu-id="56e81-236">이 구성에 대 한 조회 논리는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-236">The lookup logic for this configuration is:</span></span>

- <span data-ttu-id="56e81-237">전역 패키지 폴더를 확인 하 여 패키지/버전이 이미 다운로드 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-237">Look in global package folder to see if the package/version is already downloaded.</span></span>

- <span data-ttu-id="56e81-238">대체 폴더에서 패키지/버전 일치를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-238">Look in the fallback folders for a package/version match.</span></span>

<span data-ttu-id="56e81-239">조회 중 하나가 성공 하면 다운로드가 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-239">If either lookup is successful, then no download is necessary.</span></span>

<span data-ttu-id="56e81-240">일치 항목을 찾을 수 없는 경우 NuGet은 파일 원본 및 http 원본을 확인 한 다음 패키지를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-240">If a match is not found, then NuGet checks file sources, and then http sources, and then it downloads the packages.</span></span>

| <span data-ttu-id="56e81-241">키</span><span class="sxs-lookup"><span data-stu-id="56e81-241">Key</span></span> | <span data-ttu-id="56e81-242">값</span><span class="sxs-lookup"><span data-stu-id="56e81-242">Value</span></span> |
| --- | --- |
| <span data-ttu-id="56e81-243">(대체 폴더 이름)</span><span class="sxs-lookup"><span data-stu-id="56e81-243">(name of fallback folder)</span></span> | <span data-ttu-id="56e81-244">대체 폴더의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-244">Path to fallback folder.</span></span> |

<span data-ttu-id="56e81-245">**예**:</span><span class="sxs-lookup"><span data-stu-id="56e81-245">**Example**:</span></span>

```xml
<fallbackPackageFolders>
   <add key="XYZ Offline Packages" value="C:\somePath\someFolder\"/>
</fallbackPackageFolders>
```

## <a name="packagemanagement-section"></a><span data-ttu-id="56e81-246">packageManagement 섹션</span><span class="sxs-lookup"><span data-stu-id="56e81-246">packageManagement section</span></span>

<span data-ttu-id="56e81-247">기본 패키지 관리 형식 ( *PackageReference 또는* )을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-247">Sets the default package management format, either *packages.config* or PackageReference.</span></span> <span data-ttu-id="56e81-248">SDK 스타일 프로젝트는 항상 PackageReference을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-248">SDK-style projects always use PackageReference.</span></span>

| <span data-ttu-id="56e81-249">키</span><span class="sxs-lookup"><span data-stu-id="56e81-249">Key</span></span> | <span data-ttu-id="56e81-250">값</span><span class="sxs-lookup"><span data-stu-id="56e81-250">Value</span></span> |
| --- | --- |
| <span data-ttu-id="56e81-251">format</span><span class="sxs-lookup"><span data-stu-id="56e81-251">format</span></span> | <span data-ttu-id="56e81-252">기본 패키지 관리 형식을 나타내는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-252">A Boolean indicating the default package management format.</span></span> <span data-ttu-id="56e81-253">`1`경우 format은 PackageReference입니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-253">If `1`, format is PackageReference.</span></span> <span data-ttu-id="56e81-254">`0`경우 format은 *패키지 .config*입니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-254">If `0`, format is *packages.config*.</span></span> |
| <span data-ttu-id="56e81-255">disabled</span><span class="sxs-lookup"><span data-stu-id="56e81-255">disabled</span></span> | <span data-ttu-id="56e81-256">첫 번째 패키지를 설치할 때 기본 패키지 형식을 선택 하 라는 메시지를 표시할지 여부를 나타내는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-256">A Boolean indicating whether to show the prompt to select a default package format on first package install.</span></span> <span data-ttu-id="56e81-257">`False`는 프롬프트를 숨깁니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-257">`False` hides the prompt.</span></span> |

<span data-ttu-id="56e81-258">**예**:</span><span class="sxs-lookup"><span data-stu-id="56e81-258">**Example**:</span></span>

```xml
<packageManagement>
   <add key="format" value="1" />
   <add key="disabled" value="False" />
</packageManagement>
```

## <a name="using-environment-variables"></a><span data-ttu-id="56e81-259">환경 변수 사용</span><span class="sxs-lookup"><span data-stu-id="56e81-259">Using environment variables</span></span>

<span data-ttu-id="56e81-260">`nuget.config` 값(NuGet 3.4 이상)의 환경 변수를 사용하여 런타임에 설정을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-260">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="56e81-261">예를 들어 Windows의 `HOME` 환경 변수가 `c:\users\username`으로 설정되면 구성 파일의 `%HOME%\NuGetRepository` 값이 `c:\users\username\NuGetRepository`로 해석됩니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-261">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="56e81-262">Windows 스타일 환경 변수를 사용 해야 합니다 (시작 및 종료%). Mac/Linux 에서도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-262">Note that you have to use Windows-style environment variables (starts and ends with %) even on Mac/Linux.</span></span> <span data-ttu-id="56e81-263">구성 파일에 `$HOME/NuGetRepository` 하는 것은 확인 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-263">Having `$HOME/NuGetRepository` in a configuration file will not resolve.</span></span> <span data-ttu-id="56e81-264">Mac/Linux에서 `%HOME%\NuGetRepository` 값이 `/home/myStuff/NuGetRepository`으로 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-264">On Mac/Linux the value of `%HOME%\NuGetRepository` will resolve to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="56e81-265">환경 변수가 없으면 NuGet에서 구성 파일의 리터럴 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-265">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="56e81-266">config 파일 예제</span><span class="sxs-lookup"><span data-stu-id="56e81-266">Example config file</span></span>

<span data-ttu-id="56e81-267">다음은 선택적 항목을 비롯 한 다양 한 설정을 보여 주는 예제 `nuget.config` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="56e81-267">Below is an example `nuget.config` file that illustrates a number of settings including optional ones:</span></span>

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
