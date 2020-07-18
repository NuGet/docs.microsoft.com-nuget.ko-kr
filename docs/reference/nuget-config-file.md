---
title: nuget.config 파일 참조
description: config, bindingRedirects, packageRestore, solution 및 packageSource 섹션이 포함된 NuGet.Config 파일 참조입니다.
author: karann-msft
ms.author: karann
ms.date: 08/13/2019
ms.topic: reference
ms.openlocfilehash: 760bf09cb03608275e2c5406474f572a407a7379
ms.sourcegitcommit: f29fa9b93fd59e679fab50d7413bbf67da3ea5b3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2020
ms.locfileid: "86451127"
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="a1cf1-103">nuget.config 참조</span><span class="sxs-lookup"><span data-stu-id="a1cf1-103">nuget.config reference</span></span>

<span data-ttu-id="a1cf1-104">NuGet 동작은 `NuGet.Config` `nuget.config` [일반적인 nuget 구성](../consume-packages/configuring-nuget-behavior.md)에 설명 된 대로 다른 또는 파일의 설정에 의해 제어 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-104">NuGet behavior is controlled by settings in different `NuGet.Config` or `nuget.config` files as described in [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="a1cf1-105">`nuget.config`는 최상위 `<configuration>` 노드를 포함하는 XML 파일이며, 이 파일에는 이 항목에서 설명하는 섹션 요소가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-105">`nuget.config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="a1cf1-106">각 섹션에는 0 개 이상의 항목이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-106">Each section contains zero or more items.</span></span> <span data-ttu-id="a1cf1-107">[config 파일 예제](#example-config-file)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="a1cf1-108">설정 이름은 대/소문자를 구분하지 않으며, 값에는 [환경 변수](#using-environment-variables)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="a1cf1-109">config 섹션</span><span class="sxs-lookup"><span data-stu-id="a1cf1-109">config section</span></span>

<span data-ttu-id="a1cf1-110">에는 [ `nuget config` 명령을](../reference/cli-reference/cli-ref-config.md)사용 하 여 설정할 수 있는 기타 구성 설정이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-110">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../reference/cli-reference/cli-ref-config.md).</span></span>

<span data-ttu-id="a1cf1-111">`dependencyVersion`및는 `repositoryPath` 를 사용 하는 프로젝트에만 적용 `packages.config` 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-111">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="a1cf1-112">`globalPackagesFolder`PackageReference 형식을 사용 하는 프로젝트에만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-112">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="a1cf1-113">키</span><span class="sxs-lookup"><span data-stu-id="a1cf1-113">Key</span></span> | <span data-ttu-id="a1cf1-114">값</span><span class="sxs-lookup"><span data-stu-id="a1cf1-114">Value</span></span> |
| --- | --- |
| <span data-ttu-id="a1cf1-115">dependencyVersion(`packages.config`만)</span><span class="sxs-lookup"><span data-stu-id="a1cf1-115">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="a1cf1-116">`-DependencyVersion` 스위치가 직접 지정되지 않은 경우 패키지 설치, 복원 및 업데이트에 대한 기본 `DependencyVersion` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-116">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="a1cf1-117">이 값은 NuGet 패키지 관리자 UI에서도 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-117">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="a1cf1-118">값은 `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`입니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-118">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="a1cf1-119">globalPackagesFolder (PackageReference만 사용 하는 프로젝트)</span><span class="sxs-lookup"><span data-stu-id="a1cf1-119">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="a1cf1-120">기본 전역 패키지 폴더의 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-120">The location of the default global packages folder.</span></span> <span data-ttu-id="a1cf1-121">기본값은 `%userprofile%\.nuget\packages`(Windows) 또는 `~/.nuget/packages`(Mac/Linux)입니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-121">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="a1cf1-122">상대 경로는 프로젝트별 `nuget.config` 파일에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-122">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="a1cf1-123">이 설정은 NUGET_PACKAGES 환경 변수에 의해 재정의 되며이는 우선적으로 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-123">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="a1cf1-124">repositoryPath(`packages.config`만)</span><span class="sxs-lookup"><span data-stu-id="a1cf1-124">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="a1cf1-125">기본 `$(Solutiondir)/packages` 폴더 대신 NuGet 패키지를 설치할 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-125">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="a1cf1-126">상대 경로는 프로젝트별 `nuget.config` 파일에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-126">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="a1cf1-127">이 설정은 NUGET_PACKAGES 환경 변수에 의해 재정의 되며이는 우선적으로 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-127">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="a1cf1-128">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="a1cf1-128">defaultPushSource</span></span> | <span data-ttu-id="a1cf1-129">작업에 대한 다른 패키지 원본이 없을 때 기본값으로 사용해야 하는 패키지 원본의 URL 또는 경로를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-129">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="a1cf1-130">http_proxy, http_proxy.user, http_proxy.password, no_proxy</span><span class="sxs-lookup"><span data-stu-id="a1cf1-130">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="a1cf1-131">패키지 원본에 연결할 때 사용할 프록시 설정입니다. `http_proxy`는 `http://<username>:<password>@<domain>` 형식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-131">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="a1cf1-132">암호는 암호화되어 있으며, 수동으로 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-132">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="a1cf1-133">`no_proxy`의 경우 값은 프록시 서버를 우회하는 도메인의 쉼표로 구분된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-133">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="a1cf1-134">이러한 값에 대해 http_proxy 및 no_proxy 환경 변수를 번갈아 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-134">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="a1cf1-135">자세한 내용은 [NuGet 프록시 설정](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html)(skolima.blogspot.com)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-135">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |
| <span data-ttu-id="a1cf1-136">서명 Validationmode</span><span class="sxs-lookup"><span data-stu-id="a1cf1-136">signatureValidationMode</span></span> | <span data-ttu-id="a1cf1-137">패키지 설치 및 복원에 대 한 패키지 서명을 확인 하는 데 사용 되는 유효성 검사 모드를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-137">Specifies the validation mode used to verify package signatures for package install, and restore.</span></span> <span data-ttu-id="a1cf1-138">값은 `accept` , `require` 입니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-138">Values are `accept`, `require`.</span></span> <span data-ttu-id="a1cf1-139">기본값은 `accept`입니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-139">Defaults to `accept`.</span></span>

<span data-ttu-id="a1cf1-140">**예**:</span><span class="sxs-lookup"><span data-stu-id="a1cf1-140">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="a1cf1-141">bindingRedirects 섹션</span><span class="sxs-lookup"><span data-stu-id="a1cf1-141">bindingRedirects section</span></span>

<span data-ttu-id="a1cf1-142">패키지가 설치될 때 NuGet에서 자동 바인딩 리디렉션을 수행할지 여부를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-142">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="a1cf1-143">키</span><span class="sxs-lookup"><span data-stu-id="a1cf1-143">Key</span></span> | <span data-ttu-id="a1cf1-144">값</span><span class="sxs-lookup"><span data-stu-id="a1cf1-144">Value</span></span> |
| --- | --- |
| <span data-ttu-id="a1cf1-145">skip</span><span class="sxs-lookup"><span data-stu-id="a1cf1-145">skip</span></span> | <span data-ttu-id="a1cf1-146">자동 바인딩 리디렉션을 건너뛸지 여부를 나타내는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-146">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="a1cf1-147">기본값은 false입니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-147">The default is false.</span></span> |

<span data-ttu-id="a1cf1-148">**예**:</span><span class="sxs-lookup"><span data-stu-id="a1cf1-148">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="a1cf1-149">packageRestore 섹션</span><span class="sxs-lookup"><span data-stu-id="a1cf1-149">packageRestore section</span></span>

<span data-ttu-id="a1cf1-150">빌드하는 동안의 패키지 복원을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-150">Controls package restore during builds.</span></span>

| <span data-ttu-id="a1cf1-151">키</span><span class="sxs-lookup"><span data-stu-id="a1cf1-151">Key</span></span> | <span data-ttu-id="a1cf1-152">값</span><span class="sxs-lookup"><span data-stu-id="a1cf1-152">Value</span></span> |
| --- | --- |
| <span data-ttu-id="a1cf1-153">사용</span><span class="sxs-lookup"><span data-stu-id="a1cf1-153">enabled</span></span> | <span data-ttu-id="a1cf1-154">NuGet에서 자동 복원을 수행할 수 있는지 여부를 나타내는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-154">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="a1cf1-155">config 파일에서 이 키를 설정하는 대신 `EnableNuGetPackageRestore` 환경 변수를 `True` 값으로 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-155">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="a1cf1-156">automatic</span><span class="sxs-lookup"><span data-stu-id="a1cf1-156">automatic</span></span> | <span data-ttu-id="a1cf1-157">NuGet에서 빌드하는 동안 누락된 패키지를 확인해야 하는지 여부를 나타내는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-157">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="a1cf1-158">**예**:</span><span class="sxs-lookup"><span data-stu-id="a1cf1-158">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="a1cf1-159">solution 섹션</span><span class="sxs-lookup"><span data-stu-id="a1cf1-159">solution section</span></span>

<span data-ttu-id="a1cf1-160">솔루션의 `packages` 폴더가 원본 제어에 포함되는지 여부를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-160">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="a1cf1-161">이 섹션은 솔루션 폴더의 `nuget.config` 파일에서만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-161">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="a1cf1-162">키</span><span class="sxs-lookup"><span data-stu-id="a1cf1-162">Key</span></span> | <span data-ttu-id="a1cf1-163">값</span><span class="sxs-lookup"><span data-stu-id="a1cf1-163">Value</span></span> |
| --- | --- |
| <span data-ttu-id="a1cf1-164">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="a1cf1-164">disableSourceControlIntegration</span></span> | <span data-ttu-id="a1cf1-165">원본 제어로 작업할 때 패키지 폴더를 무시할지 여부를 나타내는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-165">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="a1cf1-166">기본값은 False입니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-166">The default value is false.</span></span> |

<span data-ttu-id="a1cf1-167">**예**:</span><span class="sxs-lookup"><span data-stu-id="a1cf1-167">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="a1cf1-168">패키지 원본 섹션</span><span class="sxs-lookup"><span data-stu-id="a1cf1-168">Package source sections</span></span>

<span data-ttu-id="a1cf1-169">`packageSources`,, `packageSourceCredentials` `apikeys` , 및 `activePackageSource` 는 `disabledPackageSources` `trustedSigners` 모두 함께 작동 하 여 설치, 복원 및 업데이트 작업 중에 NuGet이 패키지 리포지토리와 함께 작동 하는 방식을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-169">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` and `trustedSigners` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="a1cf1-170">명령은 [ `nuget sources` 명령을](../reference/cli-reference/cli-ref-sources.md) `apikeys` 사용 하 여 관리 되 [ `nuget setapikey` ](../reference/cli-reference/cli-ref-setapikey.md)고 `trustedSigners` [ `nuget trusted-signers` 명령을](../reference/cli-reference/cli-ref-trusted-signers.md)사용 하 여 관리 되는를 제외 하 고는 일반적으로 이러한 설정을 관리 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-170">The [`nuget sources` command](../reference/cli-reference/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md), and `trustedSigners` which is managed using the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="a1cf1-171">nuget.org에 대한 원본 URL은 `https://api.nuget.org/v3/index.json`입니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-171">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="a1cf1-172">packageSources</span><span class="sxs-lookup"><span data-stu-id="a1cf1-172">packageSources</span></span>

<span data-ttu-id="a1cf1-173">알려진 모든 패키지 원본을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-173">Lists all known package sources.</span></span> <span data-ttu-id="a1cf1-174">PackageReference 형식을 사용 하는 모든 프로젝트와 복원 작업 중에 순서는 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-174">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="a1cf1-175">NuGet은를 사용 하 여 프로젝트에 대 한 설치 및 업데이트 작업의 소스 순서를 고려 합니다 `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="a1cf1-175">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="a1cf1-176">키</span><span class="sxs-lookup"><span data-stu-id="a1cf1-176">Key</span></span> | <span data-ttu-id="a1cf1-177">값</span><span class="sxs-lookup"><span data-stu-id="a1cf1-177">Value</span></span> |
| --- | --- |
| <span data-ttu-id="a1cf1-178">(패키지 원본에 할당할 이름)</span><span class="sxs-lookup"><span data-stu-id="a1cf1-178">(name to assign to the package source)</span></span> | <span data-ttu-id="a1cf1-179">패키지 원본의 경로 또는 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-179">The path or URL of the package source.</span></span> |

<span data-ttu-id="a1cf1-180">**예**:</span><span class="sxs-lookup"><span data-stu-id="a1cf1-180">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

> [!Tip]
> <span data-ttu-id="a1cf1-181">지정된 노드에 대해 `<clear />`가 있으면 NuGet은 해당 노드에 대해 이전에 정의된 구성 값을 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-181">When `<clear />` is present for a given node, NuGet ignores previously defined configuration values for that node.</span></span> <span data-ttu-id="a1cf1-182">[설정이 적용 되는 방법에 대해 자세히](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied)알아보세요.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-182">[Read more about how settings are applied](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).</span></span>

### <a name="packagesourcecredentials"></a><span data-ttu-id="a1cf1-183">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="a1cf1-183">packageSourceCredentials</span></span>

<span data-ttu-id="a1cf1-184">원본에 대한 사용자 이름과 암호를 저장하며, 일반적으로 `nuget sources`와 함께 `-username` 및 `-password` 스위치로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-184">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="a1cf1-185">또한 `-storepasswordincleartext` 옵션을 사용하지 않는 한 암호는 기본적으로 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-185">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="a1cf1-186">키</span><span class="sxs-lookup"><span data-stu-id="a1cf1-186">Key</span></span> | <span data-ttu-id="a1cf1-187">값</span><span class="sxs-lookup"><span data-stu-id="a1cf1-187">Value</span></span> |
| --- | --- |
| <span data-ttu-id="a1cf1-188">사용자 이름</span><span class="sxs-lookup"><span data-stu-id="a1cf1-188">username</span></span> | <span data-ttu-id="a1cf1-189">일반 텍스트 형식의 원본에 대한 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-189">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="a1cf1-190">password</span><span class="sxs-lookup"><span data-stu-id="a1cf1-190">password</span></span> | <span data-ttu-id="a1cf1-191">원본에 대한 암호화된 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-191">The encrypted password for the source.</span></span> <span data-ttu-id="a1cf1-192">암호화 된 암호는 Windows 에서만 지원 되며 동일한 컴퓨터에서 사용 하는 경우와 원래 암호화와 동일한 사용자를 통해 암호를 해독할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-192">Encrypted passwords are only supported on Windows, and only can be decrypted when used on the same machine and via the same user as the original encryption.</span></span> |
| <span data-ttu-id="a1cf1-193">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="a1cf1-193">cleartextpassword</span></span> | <span data-ttu-id="a1cf1-194">원본에 대한 암호화되지 않은 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-194">The unencrypted password for the source.</span></span> <span data-ttu-id="a1cf1-195">참고: 환경 변수를 사용 하 여 보안을 향상 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-195">Note: environment variables can be used for improved security.</span></span> |

<span data-ttu-id="a1cf1-196">**예제:**</span><span class="sxs-lookup"><span data-stu-id="a1cf1-196">**Example:**</span></span>

<span data-ttu-id="a1cf1-197">config 파일에서 `<packageSourceCredentials>` 요소에는 적용 가능한 원본 이름 각각에 대한 자식 노드가 포함됩니다(이름에 포함된 공백은 `_x0020_`로 바뀜).</span><span class="sxs-lookup"><span data-stu-id="a1cf1-197">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="a1cf1-198">즉 "Contoso" 및 "Test Source"라는 원본의 경우 암호화된 암호를 사용하면 config 파일에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-198">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="a1cf1-199">환경 변수에 저장 된 암호화 되지 않은 암호를 사용 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="a1cf1-199">When using unencrypted passwords stored in an environment variable:</span></span>

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="ClearTextPassword" value="%ContosoPassword%" />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="ClearTextPassword" value="%TestSourcePassword%" />
    </Test_x0020_Source>
</packageSourceCredentials>
```

<span data-ttu-id="a1cf1-200">암호화되지 않은 암호를 사용하는 경우:</span><span class="sxs-lookup"><span data-stu-id="a1cf1-200">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="a1cf1-201">apikeys</span><span class="sxs-lookup"><span data-stu-id="a1cf1-201">apikeys</span></span>

<span data-ttu-id="a1cf1-202">[ `nuget setapikey` 명령](../reference/cli-reference/cli-ref-setapikey.md)으로 설정 된 대로 API 키 인증을 사용 하는 원본에 대 한 키를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-202">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="a1cf1-203">키</span><span class="sxs-lookup"><span data-stu-id="a1cf1-203">Key</span></span> | <span data-ttu-id="a1cf1-204">값</span><span class="sxs-lookup"><span data-stu-id="a1cf1-204">Value</span></span> |
| --- | --- |
| <span data-ttu-id="a1cf1-205">(원본 URL)</span><span class="sxs-lookup"><span data-stu-id="a1cf1-205">(source URL)</span></span> | <span data-ttu-id="a1cf1-206">암호화된 API 키입니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-206">The encrypted API key.</span></span> |

<span data-ttu-id="a1cf1-207">**예**:</span><span class="sxs-lookup"><span data-stu-id="a1cf1-207">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="a1cf1-208">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="a1cf1-208">disabledPackageSources</span></span>

<span data-ttu-id="a1cf1-209">현재 사용할 수 없는 원본을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-209">Identified currently disabled sources.</span></span> <span data-ttu-id="a1cf1-210">비어 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-210">May be empty.</span></span>

| <span data-ttu-id="a1cf1-211">키</span><span class="sxs-lookup"><span data-stu-id="a1cf1-211">Key</span></span> | <span data-ttu-id="a1cf1-212">값</span><span class="sxs-lookup"><span data-stu-id="a1cf1-212">Value</span></span> |
| --- | --- |
| <span data-ttu-id="a1cf1-213">(원본 이름)</span><span class="sxs-lookup"><span data-stu-id="a1cf1-213">(name of source)</span></span> | <span data-ttu-id="a1cf1-214">원본을 사용할 수 없는지 여부를 나타내는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-214">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="a1cf1-215">**예제:**</span><span class="sxs-lookup"><span data-stu-id="a1cf1-215">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="a1cf1-216">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="a1cf1-216">activePackageSource</span></span>

<span data-ttu-id="a1cf1-217">*(2.x만, 3.x 이상에서는 사용되지 않음)*</span><span class="sxs-lookup"><span data-stu-id="a1cf1-217">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="a1cf1-218">현재 활성 중인 원본을 식별하거나 모든 원본의 집계를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-218">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="a1cf1-219">키</span><span class="sxs-lookup"><span data-stu-id="a1cf1-219">Key</span></span> | <span data-ttu-id="a1cf1-220">값</span><span class="sxs-lookup"><span data-stu-id="a1cf1-220">Value</span></span> |
| --- | --- |
| <span data-ttu-id="a1cf1-221">(원본 이름) 또는 `All`</span><span class="sxs-lookup"><span data-stu-id="a1cf1-221">(name of source) or `All`</span></span> | <span data-ttu-id="a1cf1-222">키가 원본의 이름이면 값은 원본 경로 또는 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-222">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="a1cf1-223">`All`이면 값은 `(Aggregate source)`여야 하며, 그렇지 않으면 사용할 수 없는 모든 패키지 원본이 결합됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-223">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="a1cf1-224">**예**:</span><span class="sxs-lookup"><span data-stu-id="a1cf1-224">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="trustedsigners-section"></a><span data-ttu-id="a1cf1-225">해당 서명자 섹션</span><span class="sxs-lookup"><span data-stu-id="a1cf1-225">trustedSigners section</span></span>

<span data-ttu-id="a1cf1-226">설치 또는 복원 중 패키지를 허용 하는 데 사용 되는 신뢰할 수 있는 서명자를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-226">Stores trusted signers used to allow package while installing or restoring.</span></span> <span data-ttu-id="a1cf1-227">사용자가로 설정 된 경우에는이 목록을 비워 둘 수 없습니다 `signatureValidationMode` `require` .</span><span class="sxs-lookup"><span data-stu-id="a1cf1-227">This list cannot be empty when the user sets `signatureValidationMode` to `require`.</span></span> 

<span data-ttu-id="a1cf1-228">이 섹션은 [ `nuget trusted-signers` 명령을](../reference/cli-reference/cli-ref-trusted-signers.md)사용 하 여 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-228">This section can be updated with the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="a1cf1-229">**스키마**:</span><span class="sxs-lookup"><span data-stu-id="a1cf1-229">**Schema**:</span></span>

<span data-ttu-id="a1cf1-230">신뢰할 수 있는 서명자는 지정 된 `certificate` 서명자를 식별 하는 모든 인증서를 등록 하는 항목의 컬렉션을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-230">A trusted signer has a collection of `certificate` items that enlist all the certificates that identify a given signer.</span></span> <span data-ttu-id="a1cf1-231">신뢰할 수 있는 서명자는 또는 일 수 있습니다 `Author` `Repository` .</span><span class="sxs-lookup"><span data-stu-id="a1cf1-231">A trusted signer can be either an `Author` or a `Repository`.</span></span>

<span data-ttu-id="a1cf1-232">또한 신뢰할 수 있는 *리포지토리* 는 `serviceIndex` 유효한 uri 여야 하는 리포지토리의를 지정 하며, `https` 선택적으로 세미콜론으로 구분 된 목록을 지정 하 여 `owners` 해당 특정 리포지토리에서 신뢰할 수 있는 사용자를 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-232">A trusted *repository* also specifies the `serviceIndex` for the repository (which has to be a valid `https` uri) and can optionally specify a semi-colon delimited list of `owners` to restrict even more who is trusted from that specific repository.</span></span>

<span data-ttu-id="a1cf1-233">인증서 지문에 사용 되는 지원 되는 해시 알고리즘은 `SHA256` , `SHA384` 및 `SHA512` 입니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-233">The supported hash algorithms used for a certificate fingerprint are `SHA256`, `SHA384` and `SHA512`.</span></span>

<span data-ttu-id="a1cf1-234">가 `certificate` `allowUntrustedRoot` `true` 서명 확인의 일부로 인증서 체인을 빌드하는 동안 지정 된 인증서를 신뢰할 수 없는 루트에 체인으로 연결할 수 있는 것으로 지정 하면입니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-234">If a `certificate` specifies `allowUntrustedRoot` as `true` the given certificate is allowed to chain to an untrusted root while building the certificate chain as part of the signature verification.</span></span>

<span data-ttu-id="a1cf1-235">**예**:</span><span class="sxs-lookup"><span data-stu-id="a1cf1-235">**Example**:</span></span>

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

## <a name="fallbackpackagefolders-section"></a><span data-ttu-id="a1cf1-236">fallbackPackageFolders 섹션</span><span class="sxs-lookup"><span data-stu-id="a1cf1-236">fallbackPackageFolders section</span></span>

<span data-ttu-id="a1cf1-237">*(3.5 +)* 는 패키지가 대체 폴더에 있는 경우 작업을 수행 하지 않아도 되도록 패키지를 사전 설치 하는 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-237">*(3.5+)* Provides a way to preinstall packages so that no work needs to be done if the package is found in the fallback folders.</span></span> <span data-ttu-id="a1cf1-238">대체 패키지 폴더는 전역 패키지 폴더와 정확히 같은 폴더 및 파일 구조를 포함 합니다. *. nupkg* 가 있고 모든 파일이 추출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-238">Fallback package folders have the exact same folder and file structure as the global package folder: *.nupkg* is present, and all files are extracted.</span></span>

<span data-ttu-id="a1cf1-239">이 구성에 대 한 조회 논리는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-239">The lookup logic for this configuration is:</span></span>

- <span data-ttu-id="a1cf1-240">전역 패키지 폴더를 확인 하 여 패키지/버전이 이미 다운로드 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-240">Look in global package folder to see if the package/version is already downloaded.</span></span>

- <span data-ttu-id="a1cf1-241">대체 폴더에서 패키지/버전 일치를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-241">Look in the fallback folders for a package/version match.</span></span>

<span data-ttu-id="a1cf1-242">조회 중 하나가 성공 하면 다운로드가 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-242">If either lookup is successful, then no download is necessary.</span></span>

<span data-ttu-id="a1cf1-243">일치 항목을 찾을 수 없는 경우 NuGet은 파일 원본 및 http 원본을 확인 한 다음 패키지를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-243">If a match is not found, then NuGet checks file sources, and then http sources, and then it downloads the packages.</span></span>

| <span data-ttu-id="a1cf1-244">키</span><span class="sxs-lookup"><span data-stu-id="a1cf1-244">Key</span></span> | <span data-ttu-id="a1cf1-245">값</span><span class="sxs-lookup"><span data-stu-id="a1cf1-245">Value</span></span> |
| --- | --- |
| <span data-ttu-id="a1cf1-246">(대체 폴더 이름)</span><span class="sxs-lookup"><span data-stu-id="a1cf1-246">(name of fallback folder)</span></span> | <span data-ttu-id="a1cf1-247">대체 폴더의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-247">Path to fallback folder.</span></span> |

<span data-ttu-id="a1cf1-248">**예**:</span><span class="sxs-lookup"><span data-stu-id="a1cf1-248">**Example**:</span></span>

```xml
<fallbackPackageFolders>
   <add key="XYZ Offline Packages" value="C:\somePath\someFolder\"/>
</fallbackPackageFolders>
```

## <a name="packagemanagement-section"></a><span data-ttu-id="a1cf1-249">packageManagement 섹션</span><span class="sxs-lookup"><span data-stu-id="a1cf1-249">packageManagement section</span></span>

<span data-ttu-id="a1cf1-250">*packages.config* 또는 PackageReference의 기본 패키지 관리 형식을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-250">Sets the default package management format, either *packages.config* or PackageReference.</span></span> <span data-ttu-id="a1cf1-251">SDK 스타일 프로젝트는 항상 PackageReference을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-251">SDK-style projects always use PackageReference.</span></span>

| <span data-ttu-id="a1cf1-252">키</span><span class="sxs-lookup"><span data-stu-id="a1cf1-252">Key</span></span> | <span data-ttu-id="a1cf1-253">값</span><span class="sxs-lookup"><span data-stu-id="a1cf1-253">Value</span></span> |
| --- | --- |
| <span data-ttu-id="a1cf1-254">format</span><span class="sxs-lookup"><span data-stu-id="a1cf1-254">format</span></span> | <span data-ttu-id="a1cf1-255">기본 패키지 관리 형식을 나타내는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-255">A Boolean indicating the default package management format.</span></span> <span data-ttu-id="a1cf1-256">이면 `1` format은 PackageReference입니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-256">If `1`, format is PackageReference.</span></span> <span data-ttu-id="a1cf1-257">이면 `0` format이 *packages.config*됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-257">If `0`, format is *packages.config*.</span></span> |
| <span data-ttu-id="a1cf1-258">disabled</span><span class="sxs-lookup"><span data-stu-id="a1cf1-258">disabled</span></span> | <span data-ttu-id="a1cf1-259">첫 번째 패키지를 설치할 때 기본 패키지 형식을 선택 하 라는 메시지를 표시할지 여부를 나타내는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-259">A Boolean indicating whether to show the prompt to select a default package format on first package install.</span></span> <span data-ttu-id="a1cf1-260">`False`프롬프트를 숨깁니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-260">`False` hides the prompt.</span></span> |

<span data-ttu-id="a1cf1-261">**예**:</span><span class="sxs-lookup"><span data-stu-id="a1cf1-261">**Example**:</span></span>

```xml
<packageManagement>
   <add key="format" value="1" />
   <add key="disabled" value="False" />
</packageManagement>
```

## <a name="using-environment-variables"></a><span data-ttu-id="a1cf1-262">환경 변수 사용</span><span class="sxs-lookup"><span data-stu-id="a1cf1-262">Using environment variables</span></span>

<span data-ttu-id="a1cf1-263">`nuget.config` 값(NuGet 3.4 이상)의 환경 변수를 사용하여 런타임에 설정을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-263">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="a1cf1-264">예를 들어 Windows의 `HOME` 환경 변수가 `c:\users\username`으로 설정되면 구성 파일의 `%HOME%\NuGetRepository` 값이 `c:\users\username\NuGetRepository`로 해석됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-264">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="a1cf1-265">Windows 스타일 환경 변수를 사용 해야 합니다 (시작 및 종료%). Mac/Linux 에서도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-265">Note that you have to use Windows-style environment variables (starts and ends with %) even on Mac/Linux.</span></span> <span data-ttu-id="a1cf1-266">`$HOME/NuGetRepository`구성 파일에 있는 것은 확인 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-266">Having `$HOME/NuGetRepository` in a configuration file will not resolve.</span></span> <span data-ttu-id="a1cf1-267">Mac/Linux에서 값은 `%HOME%\NuGetRepository` 로 확인 됩니다 `/home/myStuff/NuGetRepository` .</span><span class="sxs-lookup"><span data-stu-id="a1cf1-267">On Mac/Linux the value of `%HOME%\NuGetRepository` will resolve to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="a1cf1-268">환경 변수가 없으면 NuGet에서 구성 파일의 리터럴 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-268">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="a1cf1-269">config 파일 예제</span><span class="sxs-lookup"><span data-stu-id="a1cf1-269">Example config file</span></span>

<span data-ttu-id="a1cf1-270">다음은 `nuget.config` 선택적 항목을 비롯 한 다양 한 설정을 보여 주는 예제 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf1-270">Below is an example `nuget.config` file that illustrates a number of settings including optional ones:</span></span>

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
