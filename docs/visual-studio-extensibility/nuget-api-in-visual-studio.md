---
title: Visual Studio의 NuGet API
description: NuGet이 Visual Studio에서 Managed Extensibility Framework를 통해 내보내는 API에 대한 인터페이스 참조입니다.
author: nkolev92
ms.author: nikolev
ms.date: 01/09/2017
ms.topic: reference
ms.openlocfilehash: 3592280d5398e13e71403023fbb361b5e26e7786
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699876"
---
# <a name="nuget-api-in-visual-studio"></a><span data-ttu-id="00256-103">Visual Studio의 NuGet API</span><span class="sxs-lookup"><span data-stu-id="00256-103">NuGet API in Visual Studio</span></span>

<span data-ttu-id="00256-104">Visual Studio의 패키지 관리자 UI 및 콘솔 외에도 NuGet은 [MEF(Managed Extensibility Framework)](/dotnet/framework/mef/index)를 통해 몇 가지 유용한 서비스를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="00256-104">In addition to the Package Manager UI and Console in Visual Studio, NuGet also exports some useful services through the [Managed Extensibility Framework (MEF)](/dotnet/framework/mef/index).</span></span> <span data-ttu-id="00256-105">이 인터페이스를 사용하면 Visual Studio의 다른 구성 요소에서 NuGet과 상호 작용하여 패키지를 설치하거나 제거하고, 설치된 패키지에 대한 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00256-105">This interface allows other components in Visual Studio to interact with NuGet, which can be used to install and uninstall packages, and to obtain information about installed packages.</span></span>

<span data-ttu-id="00256-106">몇 년간 NuGet에서는 모두 `NuGet.VisualStudio.dll` 어셈블리의 `NuGet.VisualStudio` 네임스페이스에 있는 다음과 같은 여러 서비스를 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="00256-106">Over the years, NuGet has added many services all of which reside in the `NuGet.VisualStudio` namespace in the `NuGet.VisualStudio.dll` assembly:</span></span>

<span data-ttu-id="00256-107">NuGet 3.3 이상부터 NuGet에서는 다음을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="00256-107">As of NuGet 3.3+, NuGet exports the following</span></span>

- <span data-ttu-id="00256-108">[`IRegistryKey`](#iregistrykey-interface): 레지스트리 하위 키에서 값을 검색하는 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="00256-108">[`IRegistryKey`](#iregistrykey-interface): Method to retrieve a value from a registry subkey.</span></span> <span data-ttu-id="00256-109">(3.3 이상)</span><span class="sxs-lookup"><span data-stu-id="00256-109">(3.3+)</span></span>
- <span data-ttu-id="00256-110">[`IVsCredentialProvider`](#ivscredentialprovider-interface) NuGet 작업의 자격 증명을 가져오는 메서드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="00256-110">[`IVsCredentialProvider`](#ivscredentialprovider-interface) Contains methods to get credentials for NuGet operations.</span></span> <span data-ttu-id="00256-111">(4.0 이상)</span><span class="sxs-lookup"><span data-stu-id="00256-111">(4.0+)</span></span>
- <span data-ttu-id="00256-112">[`IVsFrameworkCompatibility`](#ivsframeworkcompatibility-interface) 프레임워크와 프레임워크 간 호환성을 검색하는 메서드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="00256-112">[`IVsFrameworkCompatibility`](#ivsframeworkcompatibility-interface) Contains methods to discover frameworks and compatibility between frameworks.</span></span> <span data-ttu-id="00256-113">(4.0 이상)</span><span class="sxs-lookup"><span data-stu-id="00256-113">(4.0+)</span></span>
- <span data-ttu-id="00256-114">[`IVsFrameworkCompatibility2`](#ivsframeworkcompatibility2-interface) 프레임워크와 프레임워크 간 호환성을 검색하는 메서드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="00256-114">[`IVsFrameworkCompatibility2`](#ivsframeworkcompatibility2-interface) Contains methods to discover frameworks and compatibility between frameworks.</span></span> <span data-ttu-id="00256-115">(4.0 이상)</span><span class="sxs-lookup"><span data-stu-id="00256-115">(4.0+)</span></span>
- <span data-ttu-id="00256-116">[`IVsFrameworkCompatibility3`](#ivsframeworkcompatibility3-interface) 프레임워크와 프레임워크 간 호환성을 검색하는 메서드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="00256-116">[`IVsFrameworkCompatibility3`](#ivsframeworkcompatibility3-interface) Contains methods to discover frameworks and compatibility between frameworks.</span></span> <span data-ttu-id="00256-117">(5.8 이상)</span><span class="sxs-lookup"><span data-stu-id="00256-117">(5.8+)</span></span>
- <span data-ttu-id="00256-118">[`IVsFrameworkParser`](#ivsframeworkparser-interface) 문자열과 [FrameworkName](/dotnet/api/system.runtime.versioning.frameworkname) 간 변환을 처리하는 인터페이스입니다. (4.0 이상)</span><span class="sxs-lookup"><span data-stu-id="00256-118">[`IVsFrameworkParser`](#ivsframeworkparser-interface) An interface for dealing with the conversion between strings and [FrameworkName](/dotnet/api/system.runtime.versioning.frameworkname) (4.0+)</span></span>
- <span data-ttu-id="00256-119">[`IVsFrameworkParser2`](#ivsframeworkparser2-interface) .NET Framework 문자열을 구문 분석하는 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="00256-119">[`IVsFrameworkParser2`](#ivsframeworkparser2-interface) An interface to parse .NET Framework strings.</span></span> <span data-ttu-id="00256-120">[NuGet-IVsFrameworkParser](https://aka.ms/NuGet-IVsFrameworkParser)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00256-120">See [NuGet-IVsFrameworkParser](https://aka.ms/NuGet-IVsFrameworkParser).</span></span> <span data-ttu-id="00256-121">(5.8 이상)</span><span class="sxs-lookup"><span data-stu-id="00256-121">(5.8+)</span></span>
- <span data-ttu-id="00256-122">[`IVsGlobalPackagesInitScriptExecutor`](#ivsglobalpackagesinitscriptexecutor-interface) 솔루션의 패키지에서 PowerShell 스크립트를 실행합니다. (4.0 이상)</span><span class="sxs-lookup"><span data-stu-id="00256-122">[`IVsGlobalPackagesInitScriptExecutor`](#ivsglobalpackagesinitscriptexecutor-interface) Execute powershell scripts from package(s) in a solution (4.0+)</span></span>
- <span data-ttu-id="00256-123">[`IVsNuGetFramework`](#ivsnugetframework-interface) .NET 대상 프레임워크 모니커의 구성 요소를 나타내는 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="00256-123">[`IVsNuGetFramework`](#ivsnugetframework-interface) A type that represents the components of a .NET Target Framework Moniker.</span></span> <span data-ttu-id="00256-124">(5.8 이상)</span><span class="sxs-lookup"><span data-stu-id="00256-124">(5.8+)</span></span>
- <span data-ttu-id="00256-125">[`IVsPackageInstaller`](#ivspackageinstaller-interface): 프로젝트에 NuGet 패키지를 설치하는 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="00256-125">[`IVsPackageInstaller`](#ivspackageinstaller-interface): Methods to install NuGet packages into projects.</span></span> <span data-ttu-id="00256-126">(3.3 이상)</span><span class="sxs-lookup"><span data-stu-id="00256-126">(3.3+)</span></span>
- <span data-ttu-id="00256-127">[\`IVsPackageInstaller2](#ivspackageinstaller2-interface) 현재 솔루션 내의 프로젝트에 단일 패키지의 최신 버전을 설치하는 메서드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="00256-127">[\`IVsPackageInstaller2](#ivspackageinstaller2-interface) Contains method to install latest version of a single package into a project within the current solution.</span></span>
- <span data-ttu-id="00256-128">[`IVsPackageInstallerEvents`](#ivspackageinstallerevents-interface): 패키지를 설치하거나 제거하는 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="00256-128">[`IVsPackageInstallerEvents`](#ivspackageinstallerevents-interface): Events for package install/uninstall.</span></span> <span data-ttu-id="00256-129">(3.3 이상)</span><span class="sxs-lookup"><span data-stu-id="00256-129">(3.3+)</span></span>
- <span data-ttu-id="00256-130">[`IVsPackageInstallerProjectEvents`](#ivspackageinstallerprojectevents-interface): 패키지를 설치하거나 제거하는 일괄 처리 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="00256-130">[`IVsPackageInstallerProjectEvents`](#ivspackageinstallerprojectevents-interface): Batch events for package install/uninstall.</span></span> <span data-ttu-id="00256-131">(3.3 이상)</span><span class="sxs-lookup"><span data-stu-id="00256-131">(3.3+)</span></span>
- <span data-ttu-id="00256-132">[`IVsPackageInstallerServices`](#ivspackageinstallerservices-interface): 현재 솔루션에 설치된 패키지를 검색하고 지정된 패키지가 프로젝트에 설치되어 있는지 확인하는 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="00256-132">[`IVsPackageInstallerServices`](#ivspackageinstallerservices-interface): Methods to retrieve installed packages in the current solution and to check whether a given package is installed in a project.</span></span> <span data-ttu-id="00256-133">(3.3 이상)</span><span class="sxs-lookup"><span data-stu-id="00256-133">(3.3+)</span></span>
- <span data-ttu-id="00256-134">[`IVsPackageManagerProvider`](#ivspackagemanagerprovider-interface): NuGet 패키지에 대한 다른 패키지 관리자 제안을 제공하는 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="00256-134">[`IVsPackageManagerProvider`](#ivspackagemanagerprovider-interface): Methods to provide alternative Package Manager suggestions for a NuGet package.</span></span> <span data-ttu-id="00256-135">(3.3 이상)</span><span class="sxs-lookup"><span data-stu-id="00256-135">(3.3+)</span></span>
- <span data-ttu-id="00256-136">[`IVsPackageMetadata`](#ivspackagemetadata-interface): 설치된 패키지에 대한 정보를 검색하는 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="00256-136">[`IVsPackageMetadata`](#ivspackagemetadata-interface): Methods to retrieve information about an installed package.</span></span> <span data-ttu-id="00256-137">(3.3 이상)</span><span class="sxs-lookup"><span data-stu-id="00256-137">(3.3+)</span></span>
- <span data-ttu-id="00256-138">[`IVsPackageProjectMetadata`](#ivspackageprojectmetadata-interface): NuGet 작업이 실행되는 프로젝트에 대한 정보를 검색하는 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="00256-138">[`IVsPackageProjectMetadata`](#ivspackageprojectmetadata-interface): Methods to retrieve information about a project where NuGet actions are being executed.</span></span> <span data-ttu-id="00256-139">(3.3 이상)</span><span class="sxs-lookup"><span data-stu-id="00256-139">(3.3+)</span></span>
- <span data-ttu-id="00256-140">[`IVsPackageRestorer`](#ivspackagerestorer-interface): 프로젝트에 설치된 패키지를 복원하는 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="00256-140">[`IVsPackageRestorer`](#ivspackagerestorer-interface): Methods to restore packages installed in a project.</span></span> <span data-ttu-id="00256-141">(3.3 이상)</span><span class="sxs-lookup"><span data-stu-id="00256-141">(3.3+)</span></span>
- <span data-ttu-id="00256-142">[`IVsPackageSourceProvider`](#ivspackagesourceprovider-interface): NuGet 패키지 원본 목록을 검색하는 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="00256-142">[`IVsPackageSourceProvider`](#ivspackagesourceprovider-interface): Methods to retrieve a list of NuGet package sources.</span></span> <span data-ttu-id="00256-143">(3.3 이상)</span><span class="sxs-lookup"><span data-stu-id="00256-143">(3.3+)</span></span>
- <span data-ttu-id="00256-144">[`IVsPackageUninstaller`](#ivspackageuninstaller-interface): 프로젝트에서 NuGet 패키지를 제거하는 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="00256-144">[`IVsPackageUninstaller`](#ivspackageuninstaller-interface): Methods to uninstall NuGet packages from projects.</span></span> <span data-ttu-id="00256-145">(3.3 이상)</span><span class="sxs-lookup"><span data-stu-id="00256-145">(3.3+)</span></span>
- <span data-ttu-id="00256-146">[`IVsPathContext`](#ivspathcontext-interface) 현재 컨텍스트(예: 프로젝트 컨텍스트)와 관련된 NuGet 경로 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="00256-146">[`IVsPathContext`](#ivspathcontext-interface) NuGet path information specific to the current context (e.g. project context).</span></span> <span data-ttu-id="00256-147">(4.0 이상)</span><span class="sxs-lookup"><span data-stu-id="00256-147">(4.0+)</span></span>
- <span data-ttu-id="00256-148">[`IVsPathContext2`](#ivspathcontext2-interface) 현재 컨텍스트(예: 프로젝트 컨텍스트)와 관련된 NuGet 경로 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="00256-148">[`IVsPathContext2`](#ivspathcontext2-interface) NuGet path information specific to the current context (e.g. project context).</span></span> <span data-ttu-id="00256-149">(5.0 이상)</span><span class="sxs-lookup"><span data-stu-id="00256-149">(5.0+)</span></span>
- <span data-ttu-id="00256-150">[`IVsPathContextProvider`](#ivspathcontextprovider-interface) [IVsPathContext](#ivspathcontext-interface) 인스턴스를 초기화하는 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="00256-150">[`IVsPathContextProvider`](#ivspathcontextprovider-interface) A factory to initialize [IVsPathContext](#ivspathcontext-interface) instances.</span></span> <span data-ttu-id="00256-151">(4.0 이상)</span><span class="sxs-lookup"><span data-stu-id="00256-151">(4.0+)</span></span>
- <span data-ttu-id="00256-152">[`IVsPathContextProvider2`](#ivspathcontextprovider2-interface) [IVsPathContext2](#ivspathcontext2-interface) 인스턴스를 초기화하는 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="00256-152">[`IVsPathContextProvider2`](#ivspathcontextprovider2-interface) A factory to initialize [IVsPathContext2](#ivspathcontext2-interface) instances.</span></span> <span data-ttu-id="00256-153">(5.0 이상)</span><span class="sxs-lookup"><span data-stu-id="00256-153">(5.0+)</span></span>
- <span data-ttu-id="00256-154">[`IVsProjectJsonToPackageReferenceMigrateResult`](#ivsprojectjsontopackagereferencemigrateresult-interface) 레거시 project.json 프로젝트의 마이그레이션 작업 결과를 포함합니다. (4.3 이상)</span><span class="sxs-lookup"><span data-stu-id="00256-154">[`IVsProjectJsonToPackageReferenceMigrateResult`](#ivsprojectjsontopackagereferencemigrateresult-interface)  Contains the result of the migrate operation on a legacy project.json project (4.3+)</span></span>
- <span data-ttu-id="00256-155">[`IVsProjectJsonToPackageReferenceMigrator`](#ivsprojectjsontopackagereferencemigrator-interface) project.json 기반 레거시 프로젝트를 PackageReference 기반 프로젝트로 마이그레이션하는 메서드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="00256-155">[`IVsProjectJsonToPackageReferenceMigrator`](#ivsprojectjsontopackagereferencemigrator-interface) Contains methods to migrate a project.json based legacy project to PackageReference based project.</span></span> <span data-ttu-id="00256-156">(4.3 이상)</span><span class="sxs-lookup"><span data-stu-id="00256-156">(4.3+)</span></span>
- <span data-ttu-id="00256-157">[`IVsSemanticVersionComparer`](#ivssemanticversioncomparer-interface) 두 불투명 버전 문자열을 NuGet 의미 체계로 처리하여 비교하는 인터페이스입니다. (4.0 이상)</span><span class="sxs-lookup"><span data-stu-id="00256-157">[`IVsSemanticVersionComparer`](#ivssemanticversioncomparer-interface) An interface for comparing two opaque version strings by treating them as NuGet semantic (4.0+)</span></span>
- <span data-ttu-id="00256-158">[`IVsTemplateWizard`](#ivstemplatewizard-interface): 프로젝트/항목 템플릿에서 미리 설치된 패키지를 포함하도록 설계되었습니다. 이 인터페이스는 코드에서 호출할 수 ‘없으며’ 퍼블릭 메서드를 포함하고 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="00256-158">[`IVsTemplateWizard`](#ivstemplatewizard-interface): Designed for project/item templates to include pre-installed packages; this interface is *not* meant to be invoked from code and has no public methods.</span></span> <span data-ttu-id="00256-159">(3.3 이상)</span><span class="sxs-lookup"><span data-stu-id="00256-159">(3.3+)</span></span>

## <a name="using-nuget-services"></a><span data-ttu-id="00256-160">NuGet 서비스 사용</span><span class="sxs-lookup"><span data-stu-id="00256-160">Using NuGet services</span></span>

1. <span data-ttu-id="00256-161">프로젝트에 `NuGet.VisualStudio.dll` 어셈블리가 포함된 [`NuGet.VisualStudio`](https://www.nuget.org/packages/NuGet.VisualStudio) 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="00256-161">Install the [`NuGet.VisualStudio`](https://www.nuget.org/packages/NuGet.VisualStudio) package into your project, which contains the `NuGet.VisualStudio.dll` assembly.</span></span>

    <span data-ttu-id="00256-162">패키지가 설치되면 자동으로 어셈블리 참조의 **Interop 형식 포함** 속성이 **True** 로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="00256-162">When installed, the package automatically sets the **Embed Interop Types** property of the assembly reference to **True**.</span></span> <span data-ttu-id="00256-163">이렇게 하면 사용자가 최신 버전의 NuGet으로 업데이트할 때 버전 변경에 대한 코드를 복원할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="00256-163">This makes your code  resilient against version changes when users update to newer versions of NuGet.</span></span>

> [!Warning]
> <span data-ttu-id="00256-164">코드에서 공용 인터페이스 외에 다른 형식을 사용하지 말고, `NuGet.Core.dll`을 포함하여 다른 NuGet 어셈블리를 참조하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="00256-164">Do not use any other types besides the public interfaces in your code, and do not reference any other NuGet assemblies, including `NuGet.Core.dll`.</span></span>

1. <span data-ttu-id="00256-165">서비스를 사용하려면 [MEF 가져오기 특성](/dotnet/framework/mef/index#imports-and-exports-with-attributes) 또는 [IComponentModel 서비스](/dotnet/api/microsoft.visualstudio.componentmodelhost.icomponentmodel)를 통해 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="00256-165">To use a service, import it through the [MEF Import attribute](/dotnet/framework/mef/index#imports-and-exports-with-attributes), or through the [IComponentModel service](/dotnet/api/microsoft.visualstudio.componentmodelhost.icomponentmodel).</span></span>

    ```cs
    //Using the Import attribute
    [Import(typeof(IVsPackageInstaller2))]
    public IVsPackageInstaller2 packageInstaller;
    packageInstaller.InstallLatestPackage(null, currentProject,
        "Newtonsoft.Json", false, false);

    //Using the IComponentModel service
    var componentModel = (IComponentModel)GetService(typeof(SComponentModel));
    IVsPackageInstallerServices installerServices =
        componentModel.GetService<IVsPackageInstallerServices>();

    var installedPackages = installerServices.GetInstalledPackages();
    ```

<span data-ttu-id="00256-166">참고로, NuGet.VisualStudio에 대한 소스 코드는 [NuGet.Clients 리포지토리](https://github.com/NuGet/NuGet.Client/tree/dev/src/NuGet.Clients/NuGet.VisualStudio)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00256-166">For reference, the source code for NuGet.VisualStudio is contained within the [NuGet.Clients repository](https://github.com/NuGet/NuGet.Client/tree/dev/src/NuGet.Clients/NuGet.VisualStudio).</span></span>

## <a name="iregistrykey-interface"></a><span data-ttu-id="00256-167">IRegistryKey 인터페이스</span><span class="sxs-lookup"><span data-stu-id="00256-167">IRegistryKey interface</span></span>

```cs
/// <summary>
/// Specifies methods for manipulating a key in the Windows registry.
/// </summary>
public interface IRegistryKey
    {
    /// <summary>
    /// Retrieves the specified subkey for read or read/write access.
    /// </summary>
    /// <param name="name">The name or path of the subkey to create or open.</param>
    /// <returns>The subkey requested, or null if the operation failed.</returns>
    IRegistryKey OpenSubKey(string name);


    /// <summary>
    /// Retrieves the value associated with the specified name.
    /// </summary>
    /// <param name="name">The name of the value to retrieve. This string is not case-sensitive.</param>
    /// <returns>The value associated with name, or null if name is not found.</returns>
    object GetValue(string name);


    /// <summary>
    /// Closes the key and flushes it to disk if its contents have been modified.
    /// </summary>
    void Close();
}
```

## <a name="ivscredentialprovider-interface"></a><span data-ttu-id="00256-168">IVsCredentialProvider 인터페이스</span><span class="sxs-lookup"><span data-stu-id="00256-168">IVsCredentialProvider interface</span></span>

```cs
    /// <summary>
    /// Contains methods to get credentials for NuGet operations.
    /// </summary>
    public interface IVsCredentialProvider
    {
        /// <summary>
        /// Get credentials for the supplied package source Uri.
        /// </summary>
        /// <param name="uri">The NuGet package source Uri for which credentials are being requested. Implementors are
        /// expected to first determine if this is a package source for which they can supply credentials.
        /// If not, then Null should be returned.</param>
        /// <param name="proxy">Web proxy to use when comunicating on the network.  Null if there is no proxy
        /// authentication configured.</param>
        /// <param name="isProxyRequest">True if if this request is to get proxy authentication
        /// credentials. If the implementation is not valid for acquiring proxy credentials, then
        /// null should be returned.</param>
        /// <param name="isRetry">True if credentials were previously acquired for this uri, but
        /// the supplied credentials did not allow authorized access.</param>
        /// <param name="nonInteractive">If true, then interactive prompts must not be allowed.</param>
        /// <param name="cancellationToken">This cancellation token should be checked to determine if the
        /// operation requesting credentials has been cancelled.</param>
        /// <returns>Credentials acquired by this provider for the given package source uri.
        /// If the provider does not handle requests for the input parameter set, then null should be returned.
        /// If the provider does handle the request, but cannot supply credentials, an exception should be thrown.</returns>
        Task<ICredentials> GetCredentialsAsync(Uri uri,
            IWebProxy proxy,
            bool isProxyRequest,
            bool isRetry,
            bool nonInteractive,
            CancellationToken cancellationToken);
    }
```

## <a name="ivsframeworkcompatibility-interface"></a><span data-ttu-id="00256-169">IVsFrameworkCompatibility 인터페이스</span><span class="sxs-lookup"><span data-stu-id="00256-169">IVsFrameworkCompatibility interface</span></span>

```cs
    /// <summary>
    /// Contains methods to discover frameworks and compatibility between frameworks.
    /// </summary>
    public interface IVsFrameworkCompatibility
    {
        /// <summary>
        /// Gets all .NETStandard frameworks currently supported, in ascending order by version.
        /// </summary>
        IEnumerable<FrameworkName> GetNetStandardFrameworks();

        /// <summary>
        /// Gets frameworks that support packages of the provided .NETStandard version.
        /// </summary>
        /// <remarks>
        /// The result list is not exhaustive as it is meant to human-readable. For example,
        /// equivalent frameworks are not returned. Additionally, a framework name with version X
        /// in the result implies that framework names with versions greater than or equal to X
        /// but having the same <see cref="FrameworkName.Identifier"/> are also supported.
        /// </remarks>
        /// <param name="frameworkName">The .NETStandard version to get supporting frameworks for.</param>
        IEnumerable<FrameworkName> GetFrameworksSupportingNetStandard(FrameworkName frameworkName);

        /// <summary>
        /// Selects the framework from <paramref name="frameworks"/> that is nearest
        /// to the <paramref name="targetFramework"/>, according to NuGet's framework
        /// compatibility rules. <c>null</c> is returned of none of the frameworks
        /// are compatible.
        /// </summary>
        /// <param name="targetFramework">The target framework.</param>
        /// <param name="frameworks">The list of frameworks to choose from.</param>
        /// <exception cref="ArgumentException">If any of the arguments are <c>null</c>.</exception>
        /// <returns>The nearest framework.</returns>
        FrameworkName GetNearest(FrameworkName targetFramework, IEnumerable<FrameworkName> frameworks);
    }
```

## <a name="ivsframeworkcompatibility2-interface"></a><span data-ttu-id="00256-170">IVsFrameworkCompatibility2 인터페이스</span><span class="sxs-lookup"><span data-stu-id="00256-170">IVsFrameworkCompatibility2 interface</span></span>

```cs
    /// <summary>
    /// Gets all .NETStandard frameworks currently supported, in ascending order by version.
    /// </summary>
    public interface IVsFrameworkCompatibility2 : IVsFrameworkCompatibility
    {
        /// <summary>
        /// Selects the framework from <paramref name="frameworks"/> that is nearest
        /// to the <paramref name="targetFramework"/>, according to NuGet's framework
        /// compatibility rules. <c>null</c> is returned of none of the frameworks
        /// are compatible.
        /// </summary>
        /// <param name="targetFramework">The target framework.</param>
        /// <param name="fallbackTargetFrameworks">
        /// Target frameworks to use if the provided <paramref name="targetFramework"/> is not compatible.
        /// These fallback frameworks are attempted in sequence after <paramref name="targetFramework"/>.
        /// </param>
        /// <param name="frameworks">The list of frameworks to choose from.</param>
        /// <exception cref="ArgumentException">If any of the arguments are <c>null</c>.</exception>
        /// <returns>The nearest framework.</returns>
        FrameworkName GetNearest(
            FrameworkName targetFramework,
            IEnumerable<FrameworkName> fallbackTargetFrameworks,
            IEnumerable<FrameworkName> frameworks);
    }
```

## <a name="ivsframeworkcompatibility3-interface"></a><span data-ttu-id="00256-171">IVsFrameworkCompatibility3 인터페이스</span><span class="sxs-lookup"><span data-stu-id="00256-171">IVsFrameworkCompatibility3 interface</span></span>

```cs
    /// <summary>
    /// Gets all .NETStandard frameworks currently supported, in ascending order by version.
    /// </summary>
    public interface IVsFrameworkCompatibility3
    {
        /// <summary>
        /// Selects the framework from <paramref name="frameworks"/> that is nearest
        /// to the <paramref name="targetFramework"/>, according to NuGet's framework
        /// compatibility rules. <c>null</c> is returned of none of the frameworks
        /// are compatible.
        /// </summary>
        /// <param name="targetFramework">The target framework.</param>
        /// <param name="frameworks">The list of frameworks to choose from.</param>
        /// <exception cref="ArgumentNullException">If any of the arguments are null.</exception>
        /// <exception cref="ArgumentException">If any of the frameworks cannot be parsed.</exception>
        /// <returns>The nearest framework.</returns>
        /// <remarks>This API is <a href="https://github.com/microsoft/vs-threading/blob/9f065f155525c4561257e02ad61e66e93e073886/doc/cookbook_vs.md#how-do-i-effectively-verify-that-my-code-is-fully-free-threaded">free-threaded</a>.</remarks>
        IVsNuGetFramework GetNearest(IVsNuGetFramework targetFramework, IEnumerable<IVsNuGetFramework> frameworks);

        /// <summary>
        /// Selects the framework from <paramref name="frameworks"/> that is nearest
        /// to the <paramref name="targetFramework"/>, according to NuGet's framework
        /// compatibility rules. <c>null</c> is returned of none of the frameworks
        /// are compatible.
        /// </summary>
        /// <param name="targetFramework">The target framework.</param>
        /// <param name="fallbackTargetFrameworks">
        /// Target frameworks to use if the provided <paramref name="targetFramework"/> is not compatible.
        /// These fallback frameworks are attempted in sequence after <paramref name="targetFramework"/>.
        /// </param>
        /// <param name="frameworks">The list of frameworks to choose from.</param>
        /// <exception cref="ArgumentNullException">If any of the arguments are null.</exception>
        /// <exception cref="ArgumentException">If any of the frameworkscannot be parsed.</exception>
        /// <returns>The nearest framework.</returns>
        /// <remarks>This API is <a href="https://github.com/microsoft/vs-threading/blob/9f065f155525c4561257e02ad61e66e93e073886/doc/cookbook_vs.md#how-do-i-effectively-verify-that-my-code-is-fully-free-threaded">free-threaded</a>.</remarks>
        IVsNuGetFramework GetNearest(
            IVsNuGetFramework targetFramework,
            IEnumerable<IVsNuGetFramework> fallbackTargetFrameworks,
            IEnumerable<IVsNuGetFramework> frameworks);
    }
```

## <a name="ivsframeworkparser-interface"></a><span data-ttu-id="00256-172">IVsFrameworkParser 인터페이스</span><span class="sxs-lookup"><span data-stu-id="00256-172">IVsFrameworkParser interface</span></span>

```cs
    /// <summary>
    /// An interface for dealing with the conversion between strings and <see cref="FrameworkName"/>
    /// instances.
    /// </summary>
    public interface IVsFrameworkParser
    {
        /// <summary>
        /// Parses a short framework name (e.g. "net45") or a full framework name
        /// (e.g. ".NETFramework,Version=v4.5") into a <see cref="FrameworkName"/>
        /// instance.
        /// </summary>
        /// <param name="shortOrFullName">The framework string.</param>
        /// <exception cref="ArgumentNullException">If the provided string is null.</exception>
        /// <exception cref="ArgumentException">If the provided string cannot be parsed.</exception>
        /// <returns>The parsed framework.</returns>
        FrameworkName ParseFrameworkName(string shortOrFullName);

        /// <summary>
        /// Gets the shortened version of the framework name from a <see cref="FrameworkName"/>
        /// instance.
        /// </summary>
        /// <remarks>
        /// For example, ".NETFramework,Version=v4.5" is converted to "net45". This is the value
        /// used inside of .nupkg folder structures as well as in project.json files.
        /// </remarks>
        /// <param name="frameworkName">The framework name.</param>
        /// <exception cref="ArgumentNullException">If the input is null.</exception>
        /// <exception cref="ArgumentException">
        /// If the provided framework name cannot be converted to a short name.
        /// </exception>
        /// <returns>The short framework name. </returns>
        string GetShortFrameworkName(FrameworkName frameworkName);
    }
```

## <a name="ivsframeworkparser2-interface"></a><span data-ttu-id="00256-173">IVsFrameworkParser2 인터페이스</span><span class="sxs-lookup"><span data-stu-id="00256-173">IVsFrameworkParser2 interface</span></span>

```cs
    /// <summary>An interface to parse .NET Framework strings. See <a href="http://aka.ms/NuGet-IVsFrameworkParser">http://aka.ms/NuGet-IVsFrameworkParser</a>.</summary>
    public interface IVsFrameworkParser2
    {
        /// <summary>
        /// Parses a short framework name (e.g. "net45") or a full Target Framework Moniker
        /// (e.g. ".NETFramework,Version=v4.5") into a <see cref="IVsNuGetFramework"/>
        /// instance.
        /// </summary>
        /// <param name="input">The framework string</param>
        /// <param name="nuGetFramework">The resulting <see cref="IVsNuGetFramework"/>. If the method returns false, this return NuGet's "Unsupported" framework details.</param>
        /// <returns>A boolean to specify whether the input could be parsed into a valid <see cref="IVsNuGetFramework"/> object.</returns>
        /// <remarks>This API is not needed to get framework information about loaded projects, and should not be used to parse the project's TargetFramework property. See <a href="http://aka.ms/NuGet-IVsFrameworkParser">http://aka.ms/NuGet-IVsFrameworkParser</a>.<br/>
        /// This API is <a href="https://github.com/microsoft/vs-threading/blob/9f065f155525c4561257e02ad61e66e93e073886/doc/cookbook_vs.md#how-do-i-effectively-verify-that-my-code-is-fully-free-threaded">free-threaded</a>.</remarks>
        bool TryParse(string input, out IVsNuGetFramework nuGetFramework);
    }
```

## <a name="ivsglobalpackagesinitscriptexecutor-interface"></a><span data-ttu-id="00256-174">IVsGlobalPackagesInitScriptExecutor 인터페이스</span><span class="sxs-lookup"><span data-stu-id="00256-174">IVsGlobalPackagesInitScriptExecutor interface</span></span>

```cs
    /// <summary>
    /// Execute powershell scripts from package(s) in a solution
    /// </summary>
    /// <remarks>Intended for internal use only.</remarks>
    public interface IVsGlobalPackagesInitScriptExecutor
    {
        /// <summary>
        /// Executes the init script of the given package if available.
        /// 1) If the init.ps1 script has already been executed by the powershell host, it will not be executed again.
        /// True is returned.
        /// 2) If the package is found in the global packages folder it will be used.
        /// If not, it will return false and do nothing.
        /// 3) Also, note if other scripts are executing while this call was made, it will wait for them to complete.
        /// </summary>
        /// <param name="packageId">Id of the package whose init.ps1 will be executed.</param>
        /// <param name="packageVersion">Version of the package whose init.ps1 will be executed.</param>
        /// <returns>Returns true if the script was executed or has been executed already.</returns>
        /// <remarks>This method throws if the init.ps1 being executed throws.</remarks>
        Task<bool> ExecuteInitScriptAsync(string packageId, string packageVersion);
    }
```

## <a name="ivsnugetframework-interface"></a><span data-ttu-id="00256-175">IVsNuGetFramework 인터페이스</span><span class="sxs-lookup"><span data-stu-id="00256-175">IVsNuGetFramework interface</span></span>

```cs
    /// <summary>A type that represents the components of a .NET Target Framework Moniker.</summary>
    /// <remarks><see cref="System.Runtime.Versioning.FrameworkName"/> does not support .NET 5 Target Framework Monikers with a platform, but this type does.</remarks>
    public interface IVsNuGetFramework
    {
        /// <summary>The framework moniker.</summary>
        string TargetFrameworkMoniker { get; }

        /// <summary>The platform moniker.</summary>
        string TargetPlatformMoniker { get; }

        /// <summary>The platform minimum version.</summary>
        /// <remarks>This property is read by <see cref="IVsFrameworkCompatibility3" />, but will always have a null value when returned from <see cref="IVsFrameworkParser2"/>.</remarks>
        string TargetPlatformMinVersion { get; }
    }
```

## <a name="ivspackageinstaller-interface"></a><span data-ttu-id="00256-176">IVsPackageInstaller 인터페이스</span><span class="sxs-lookup"><span data-stu-id="00256-176">IVsPackageInstaller interface</span></span>

```cs
public interface IVsPackageInstaller
{
    /// <summary>
    /// Installs a single package from the specified package source.
    /// </summary>
    /// <param name="source">
    /// The package source to install the package from. This value can be <c>null</c>
    /// to indicate that the user's configured sources should be used. Otherwise,
    /// this should be the source path as a string. If the user has credentials
    /// configured for a source, this value must exactly match the configured source
    /// value.
    /// </param>
    /// <param name="project">The target project for package installation.</param>
    /// <param name="packageId">The package ID of the package to install.</param>
    /// <param name="version">
    /// The version of the package to install. <c>null</c> can be provided to
    /// install the latest version of the package.
    /// </param>
    /// <param name="ignoreDependencies">
    /// A boolean indicating whether or not to ignore the package's dependencies
    /// during installation.
    /// </param>
    void InstallPackage(string source, Project project, string packageId, Version version, bool ignoreDependencies);

    /// <summary>
    /// Installs a single package from the specified package source.
    /// </summary>
    /// <param name="source">
    /// The package source to install the package from. This value can be <c>null</c>
    /// to indicate that the user's configured sources should be used. Otherwise,
    /// this should be the source path as a string. If the user has credentials
    /// configured for a source, this value must exactly match the configured source
    /// value.
    /// </param>
    /// <param name="project">The target project for package installation.</param>
    /// <param name="packageId">The package ID of the package to install.</param>
    /// <param name="version">
    /// The version of the package to install. <c>null</c> can be provided to
    /// install the latest version of the package.
    /// </param>
    /// <param name="ignoreDependencies">
    /// A boolean indicating whether or not to ignore the package's dependencies
    /// during installation.
    /// </param>
    void InstallPackage(string source, Project project, string packageId, string version, bool ignoreDependencies);

    /// <summary>
    /// Installs a single package from the specified package source.
    /// </summary>
    /// <param name="repository">The package repository to install the package from.</param>
    /// <param name="project">The target project for package installation.</param>
    /// <param name="packageId">The package id of the package to install.</param>
    /// <param name="version">
    /// The version of the package to install. <c>null</c> can be provided to
    /// install the latest version of the package.
    /// </param>
    /// <param name="ignoreDependencies">
    /// A boolean indicating whether or not to ignore the package's dependencies
    /// during installation.
    /// </param>
    /// <param name="skipAssemblyReferences">
    /// A boolean indicating if assembly references from the package should be
    /// skipped.
    /// </param>
    void InstallPackage(IPackageRepository repository, Project project, string packageId, string version, bool ignoreDependencies, bool skipAssemblyReferences);

    /// <summary>
    /// Installs one or more packages that exist on disk in a folder defined in the registry.
    /// </summary>
    /// <param name="keyName">
    /// The registry key name (under NuGet's repository key) that defines the folder on disk
    /// containing the packages.
    /// </param>
    /// <param name="isPreUnzipped">
    /// A boolean indicating whether the folder contains packages that are
    /// pre-unzipped.
    /// </param>
    /// <param name="skipAssemblyReferences">
    /// A boolean indicating whether the assembly references from the packages
    /// should be skipped.
    /// </param>
    /// <param name="project">The target project for package installation.</param>
    /// <param name="packageVersions">
    /// A dictionary of packages/versions to install where the key is the package id
    /// and the value is the version.
    /// </param>
    /// <remarks>
    /// If any version of the package is already installed, no action will be taken.
    /// <para>
    /// Dependencies are always ignored.
    /// </para>
    /// </remarks>
    void InstallPackagesFromRegistryRepository(string keyName, bool isPreUnzipped, bool skipAssemblyReferences, Project project, IDictionary<string, string> packageVersions);

    /// <summary>
    /// Installs one or more packages that exist on disk in a folder defined in the registry.
    /// </summary>
    /// <param name="keyName">
    /// The registry key name (under NuGet's repository key) that defines the folder on disk
    /// containing the packages.
    /// </param>
    /// <param name="isPreUnzipped">
    /// A boolean indicating whether the folder contains packages that are
    /// pre-unzipped.
    /// </param>
    /// <param name="skipAssemblyReferences">
    /// A boolean indicating whether the assembly references from the packages
    /// should be skipped.
    /// </param>
    /// <param name="ignoreDependencies">A boolean indicating whether the package's dependencies should be ignored</param>
    /// <param name="project">The target project for package installation.</param>
    /// <param name="packageVersions">
    /// A dictionary of packages/versions to install where the key is the package id
    /// and the value is the version.
    /// </param>
    /// <remarks>
    /// If any version of the package is already installed, no action will be taken.
    /// </remarks>
    void InstallPackagesFromRegistryRepository(string keyName, bool isPreUnzipped, bool skipAssemblyReferences, bool ignoreDependencies, Project project, IDictionary<string, string> packageVersions);

    /// <summary>
    /// Installs one or more packages that are embedded in a Visual Studio Extension Package.
    /// </summary>
    /// <param name="extensionId">The Id of the Visual Studio Extension Package.</param>
    /// <param name="isPreUnzipped">
    /// A boolean indicating whether the folder contains packages that are
    /// pre-unzipped.
    /// </param>
    /// <param name="skipAssemblyReferences">
    /// A boolean indicating whether the assembly references from the packages
    /// should be skipped.
    /// </param>
    /// <param name="project">The target project for package installation</param>
    /// <param name="packageVersions">
    /// A dictionary of packages/versions to install where the key is the package id
    /// and the value is the version.
    /// </param>
    /// <remarks>
    /// If any version of the package is already installed, no action will be taken.
    /// <para>
    /// Dependencies are always ignored.
    /// </para>
    /// </remarks>
    void InstallPackagesFromVSExtensionRepository(string extensionId, bool isPreUnzipped, bool skipAssemblyReferences, Project project, IDictionary<string, string> packageVersions);

    /// <summary>
    /// Installs one or more packages that are embedded in a Visual Studio Extension Package.
    /// </summary>
    /// <param name="extensionId">The Id of the Visual Studio Extension Package.</param>
    /// <param name="isPreUnzipped">
    /// A boolean indicating whether the folder contains packages that are
    /// pre-unzipped.
    /// </param>
    /// <param name="skipAssemblyReferences">
    /// A boolean indicating whether the assembly references from the packages
    /// should be skipped.
    /// </param>
    /// <param name="ignoreDependencies">A boolean indicating whether the package's dependencies should be ignored</param>
    /// <param name="project">The target project for package installation</param>
    /// <param name="packageVersions">
    /// A dictionary of packages/versions to install where the key is the package id
    /// and the value is the version.
    /// </param>
    /// <remarks>
    /// If any version of the package is already installed, no action will be taken.
    /// </remarks>
    void InstallPackagesFromVSExtensionRepository(string extensionId, bool isPreUnzipped, bool skipAssemblyReferences, bool ignoreDependencies, Project project, IDictionary<string, string> packageVersions);
}
```

## <a name="ivspackageinstaller2-interface"></a><span data-ttu-id="00256-177">IVsPackageinstaller2 인터페이스</span><span class="sxs-lookup"><span data-stu-id="00256-177">IVsPackageinstaller2 interface</span></span>

```cs
   [Guid("4F3B122B-A53B-432C-8D85-0FAFB8BE4FF4")]
    public interface IVsPackageInstaller2 : IVsPackageInstaller
    {
        /// <summary>
        /// Installs the latest version of a single package from the specified package source.
        /// </summary>
        /// <param name="source">
        /// The package source to install the package from. This value can be <c>null</c>
        /// to indicate that the user's configured sources should be used. Otherwise,
        /// this should be the source path as a string. If the user has credentials
        /// configured for a source, this value must exactly match the configured source
        /// value.
        /// </param>
        /// <param name="project">The target project for package installation.</param>
        /// <param name="packageId">The package ID of the package to install.</param>
        /// <param name="includePrerelease">
        /// Whether or not to consider prerelease versions when finding the latest version
        /// to install.
        /// </param>
        /// <param name="ignoreDependencies">
        /// A boolean indicating whether or not to ignore the package's dependencies
        /// during installation.
        /// </param>
        /// <exception cref="InvalidOperationException">
        /// Thrown when <see paramref="includePrerelease"/> is <c>false</c> and no stable version
        /// of the package exists.
        /// </exception>
        void InstallLatestPackage(
            string source,
            Project project,
            string packageId,
            bool includePrerelease,
            bool ignoreDependencies);
    }
```

## <a name="ivspackageinstallerevents-interface"></a><span data-ttu-id="00256-178">IVsPackageInstallerEvents 인터페이스</span><span class="sxs-lookup"><span data-stu-id="00256-178">IVsPackageInstallerEvents interface</span></span>

```cs
public interface IVsPackageInstallerEvents
{
    /// <summary>
    /// Raised when a package is about to be installed into the current solution.
    /// </summary>
    event VsPackageEventHandler PackageInstalling;

    /// <summary>
    /// Raised after a package has been installed into the current solution.
    /// </summary>
    event VsPackageEventHandler PackageInstalled;

    /// <summary>
    /// Raised when a package is about to be uninstalled from the current solution.
    /// </summary>
    event VsPackageEventHandler PackageUninstalling;

    /// <summary>
    /// Raised after a package has been uninstalled from the current solution.
    /// </summary>
    event VsPackageEventHandler PackageUninstalled;

    /// <summary>
    /// Raised after a package has been installed into a project within the current solution.
    /// </summary>
    event VsPackageEventHandler PackageReferenceAdded;

    /// <summary>
    /// Raised after a package has been uninstalled from a project within the current solution.
    /// </summary>
    event VsPackageEventHandler PackageReferenceRemoved;
}
```

## <a name="ivspackageinstallerprojectevents-interface"></a><span data-ttu-id="00256-179">IVsPackageInstallerProjectEvents 인터페이스</span><span class="sxs-lookup"><span data-stu-id="00256-179">IVsPackageInstallerProjectEvents interface</span></span>

```cs
public interface IVsPackageInstallerProjectEvents
{
    /// <summary>
    /// Raised before any IVsPackageInstallerEvents events are raised for a project.
    /// </summary>
    event VsPackageProjectEventHandler BatchStart;

    /// <summary>
    /// Raised after all IVsPackageInstallerEvents events are raised for a project.
    /// </summary>
    event VsPackageProjectEventHandler BatchEnd;
}
```

## <a name="ivspackageinstallerservices-interface"></a><span data-ttu-id="00256-180">IVsPackageInstallerServices 인터페이스</span><span class="sxs-lookup"><span data-stu-id="00256-180">IVsPackageInstallerServices interface</span></span>

```cs
public interface IVsPackageInstallerServices
{
    // IMPORTANT: do NOT rearrange the methods here. The order is important to maintain
    // backwards compatibility with clients that were compiled against old versions of NuGet.

    /// <summary>
    /// Get the list of NuGet packages installed in the current solution.
    /// </summary>
    IEnumerable<IVsPackageMetadata> GetInstalledPackages();

    /// <summary>
    /// Checks if a NuGet package with the specified Id is installed in the specified project.
    /// </summary>
    /// <param name="project">The project to check for NuGet package.</param>
    /// <param name="id">The id of the package to check.</param>
    /// <returns><c>true</c> if the package is install. <c>false</c> otherwise.</returns>
    bool IsPackageInstalled(Project project, string id);

    /// <summary>
    /// Checks if a NuGet package with the specified Id and version is installed in the specified project.
    /// </summary>
    /// <param name="project">The project to check for NuGet package.</param>
    /// <param name="id">The id of the package to check.</param>
    /// <param name="version">The version of the package to check.</param>
    /// <returns><c>true</c> if the package is install. <c>false</c> otherwise.</returns>
    bool IsPackageInstalled(Project project, string id, SemanticVersion version);

    /// <summary>
    /// Checks if a NuGet package with the specified Id and version is installed in the specified project.
    /// </summary>
    /// <param name="project">The project to check for NuGet package.</param>
    /// <param name="id">The id of the package to check.</param>
    /// <param name="versionString">The version of the package to check.</param>
    /// <returns><c>true</c> if the package is install. <c>false</c> otherwise.</returns>
    /// <remarks>
    /// The reason this method is named IsPackageInstalledEx, instead of IsPackageInstalled, is that
    /// when client project compiles against this assembly, the compiler would attempt to bind against
    /// the other overload which accepts SemanticVersion and would require client project to reference NuGet.Core.
    /// </remarks>
    bool IsPackageInstalledEx(Project project, string id, string versionString);

    /// <summary>
    /// Get the list of NuGet packages installed in the specified project.
    /// </summary>
    /// <param name="project">The project to get NuGet packages from.</param>
    IEnumerable<IVsPackageMetadata> GetInstalledPackages(Project project);
}
```

## <a name="ivspackagemanagerprovider-interface"></a><span data-ttu-id="00256-181">IVsPackageManagerProvider 인터페이스</span><span class="sxs-lookup"><span data-stu-id="00256-181">IVsPackageManagerProvider interface</span></span>

```cs
public interface IVsPackageManagerProvider
{
    /// <summary>
    /// Localized display package manager name.
    /// </summary>
    string PackageManagerName { get; }

    /// <summary>
    /// Package manager unique id.
    /// </summary>
    string PackageManagerId { get; }

    /// <summary>
    /// The tool tip description for the package
    /// </summary>
    string Description { get; }

    /// <summary>
    /// Check if a recommendation should be surfaced for an alternate package manager.
    /// This code should not rely on slow network calls, and should return rapidly.
    /// </summary>
    /// <param name="packageId">Current package id</param>
    /// <param name="projectName">Unique project name for finding the project through VS dte</param>
    /// <param name="token">Cancellation Token</param>
    /// <returns>return true if need to direct to integrated package manager for this package</returns>
    Task<bool> CheckForPackageAsync(string packageId, string projectName, CancellationToken token);

    /// <summary>
    /// This Action should take the user to the other package manager.
    /// </summary>
    /// <param name="packageId">Current package id</param>
    /// <param name="projectName">Unique project name for finding the project through VS dte</param>
    void GoToPackage(string packageId, string projectName);
}
```

## <a name="ivspackagemetadata-interface"></a><span data-ttu-id="00256-182">IVsPackageMetadata 인터페이스</span><span class="sxs-lookup"><span data-stu-id="00256-182">IVsPackageMetadata interface</span></span>

```cs
public interface IVsPackageMetadata
{
    /// <summary>
    /// Id of the package.
    /// </summary>
    string Id { get; }

    /// <summary>
    /// Version of the package.
    /// </summary>
    /// <remarks>
    /// Do not use this property because it will require referencing NuGet.Core.dll assembly. Use the VersionString
    /// property instead.
    /// </remarks>
    [Obsolete("Do not use this property because it will require referencing NuGet.Core.dll assembly. Use the VersionString property instead.")]
    NuGet.SemanticVersion Version { get; }

    /// <summary>
    /// Title of the package.
    /// </summary>
    string Title { get; }

    /// <summary>
    /// Description of the package.
    /// </summary>
    string Description { get; }

    /// <summary>
    /// The authors of the package.
    /// </summary>
    IEnumerable<string> Authors { get; }

    /// <summary>
    /// The location where the package is installed on disk.
    /// </summary>
    string InstallPath { get; }

    // IMPORTANT: This property must come LAST, because it was added in 2.5. Having it declared
    // LAST will avoid breaking components that compiled against earlier versions which doesn't
    // have this property.
    /// <summary>
    /// The version of the package.
    /// </summary>
    /// <remarks>
    /// Use this property instead of the Version property becase with the type string,
    /// it doesn't require referencing NuGet.Core.dll assembly.
    /// </remarks>
    string VersionString { get; }
}
```

## <a name="ivspackageprojectmetadata-interface"></a><span data-ttu-id="00256-183">IVsPackageProjectMetadata 인터페이스</span><span class="sxs-lookup"><span data-stu-id="00256-183">IVsPackageProjectMetadata interface</span></span>

```cs
public interface IVsPackageProjectMetadata
{
    /// <summary>
    /// Unique batch id for batch start/end events of the project.
    /// </summary>
    string BatchId { get; }

    /// <summary>
    /// Name of the project.
    /// </summary>
    string ProjectName { get; }
}
```

## <a name="ivspackagerestorer-interface"></a><span data-ttu-id="00256-184">IVsPackageRestorer 인터페이스</span><span class="sxs-lookup"><span data-stu-id="00256-184">IVsPackageRestorer interface</span></span>

```cs
public interface IVsPackageRestorer
{
    /// <summary>
    /// Returns a value indicating whether the user consent to download NuGet packages
    /// has been granted.
    /// </summary>
    /// <returns>true if the user consent has been granted; otherwise, false.</returns>
    bool IsUserConsentGranted();

    /// <summary>
    /// Restores NuGet packages installed in the given project within the current solution.
    /// </summary>
    /// <param name="project">The project whose NuGet packages to restore.</param>
    void RestorePackages(Project project);
}
```

## <a name="ivspackagesourceprovider-interface"></a><span data-ttu-id="00256-185">IVsPackageSourceProvider 인터페이스</span><span class="sxs-lookup"><span data-stu-id="00256-185">IVsPackageSourceProvider interface</span></span>

```cs
/// <summary>
/// A public API for retrieving the list of NuGet package sources.
/// </summary>
public interface IVsPackageSourceProvider
{
    /// <summary>
    /// Provides the list of package sources.
    /// </summary>
    /// <param name="includeUnOfficial">Unofficial sources will be included in the results</param>
    /// <param name="includeDisabled">Disabled sources will be included in the results</param>
    /// <remarks>Does not require the UI thread.</remarks>
    /// <exception cref="ArgumentException">Thrown if a NuGet configuration file is invalid.</exception>
    /// <exception cref="ArgumentNullException">Thrown if a NuGet configuration file is invalid.</exception>
    /// <exception cref="InvalidOperationException">Thrown if a NuGet configuration file is invalid.</exception>
    /// <exception cref="InvalidDataException">Thrown if a NuGet configuration file is invalid.</exception>
    /// <returns>Key: source name Value: source URI</returns>
    IEnumerable<KeyValuePair<string, string>> GetSources(bool includeUnOfficial, bool includeDisabled);

    /// <summary>
    /// Raised when sources are added, removed, disabled, or modified.
    /// </summary>
    event EventHandler SourcesChanged;
}
```

## <a name="ivspackageuninstaller-interface"></a><span data-ttu-id="00256-186">IVsPackageUninstaller 인터페이스</span><span class="sxs-lookup"><span data-stu-id="00256-186">IVsPackageUninstaller interface</span></span>

```cs
public interface IVsPackageUninstaller
{
    /// <summary>
    /// Uninstall the specified package from a project and specify whether to uninstall its dependency packages
    /// too.
    /// </summary>
    /// <param name="project">The project from which the package is uninstalled.</param>
    /// <param name="packageId">The package to be uninstalled</param>
    /// <param name="removeDependencies">
    /// A boolean to indicate whether the dependency packages should be
    /// uninstalled too.
    /// </param>
    void UninstallPackage(Project project, string packageId, bool removeDependencies);
}
```

## <a name="ivspathcontext-interface"></a><span data-ttu-id="00256-187">IVsPathContext 인터페이스</span><span class="sxs-lookup"><span data-stu-id="00256-187">IVsPathContext interface</span></span>

```cs
/// <summary>
    /// NuGet path information specific to the current context (e.g. project context).
    /// Represents captured snapshot associated with current project/solution settings.
    /// Should be discarded immediately after all queries are done.
    /// </summary>
    [ComImport]
    [Guid("24A1A187-75EE-4296-A8B3-59F0E0707119")]
    public interface IVsPathContext
    {
        /// <summary>
        /// User package folder directory. The path returned is an absolute path.
        /// </summary>
        string UserPackageFolder { get; }

        /// <summary>
        /// Fallback package folder locations. The paths (if any) in the returned list are absolute paths. If no
        /// fallback package folders are configured, an empty list is returned. The item type of this sequence is
        /// <see cref="string"/>.
        /// </summary>
        IEnumerable FallbackPackageFolders { get; }

        /// <summary>
        /// Fetch a package directory containing the provided asset path.
        /// </summary>
        /// <param name="packageAssetPath">Absolute path to package asset file.</param>
        /// <param name="packageDirectoryPath">Full path to a package directory. 
        /// <code>null</code> if returned falue is <code>false</code>.</param>
        /// <returns>
        /// <code>true</code> when a package containing the given file was found, <code>false</code> - otherwise.
        /// </returns>
        /// <example>
        /// Suppose the project is a packages.config project and the following asset paths are provided:
        /// 
        /// - C:\src\MyProject\packages\NuGet.Versioning.3.5.0-rc1-final\lib\net45\NuGet.Versioning.dll
        /// - C:\path\to\non\package\assembly\Newtonsoft.Json.dll
        /// - C:\src\MyOtherProject\packages\NuGet.Core.2.12.0\lib\net40\NuGet.Core.dll
        /// - C:\src\MyProject\packages\Autofac.3.5.2\lib\net40\Autofac.dll
        /// - C:\src\MyProject\packages\Autofac.3.5.2\lib\net40\Autofac.Fake.dll
        /// 
        /// The result will be:
        /// 
        /// - C:\src\MyProject\packages\NuGet.Versioning.3.5.0-rc1-final
        /// - null
        /// - null
        /// - C:\src\MyProject\packages\Autofac.3.5.2
        /// - C:\src\MyProject\packages\Autofac.3.5.2
        /// </example>
        bool TryResolvePackageAsset(string packageAssetPath, out string packageDirectoryPath);
    }
```

## <a name="ivspathcontext2-interface"></a><span data-ttu-id="00256-188">IVsPathContext2 인터페이스</span><span class="sxs-lookup"><span data-stu-id="00256-188">IVsPathContext2 interface</span></span>

```cs
/// <summary>
    /// NuGet path information specific to the current context (e.g. project context) or solution context
    /// Represents captured snapshot associated with current project/solution settings.
    /// Should be discarded immediately after all queries are done.
    /// </summary>
    public interface IVsPathContext2 : IVsPathContext
    {
        /// <summary>
        /// Solution packages folder directory. This will always be set irrespective if folder actually exists or not.
        /// The path returned is an absolute path.
        /// </summary>
        string SolutionPackageFolder { get; }
    }
```

## <a name="ivspathcontextprovider-interface"></a><span data-ttu-id="00256-189">IVsPathContextProvider 인터페이스</span><span class="sxs-lookup"><span data-stu-id="00256-189">IVsPathContextProvider interface</span></span>

```cs
    /// <summary>
    /// A factory to initialize <see cref="IVsPathContext"/> instances.
    /// </summary>
    public interface IVsPathContextProvider
    {
        /// <summary>
        /// Attempts to create an instance of <see cref="IVsPathContext"/>.
        /// </summary>
        /// <param name="projectUniqueName">
        /// Unique identificator of the project. Should be a full path to project file.
        /// </param>
        /// <param name="context">The path context associated with given project.</param>
        /// <returns>
        /// <code>True</code> if operation has succeeded and context was created.
        /// False, otherwise, e.g. when provided project is not managed by NuGet.
        /// </returns>
        /// <throws>
        /// <code>ArgumentNullException</code> if projectUniqueName is passed as null.
        /// <code>InvalidOperationException</code> when it fails to create a context and return appropriate error message.
        /// </throws>
        bool TryCreateContext(string projectUniqueName, out IVsPathContext context);
    }
```

## <a name="ivspathcontextprovider2-interface"></a><span data-ttu-id="00256-190">IVsPathContextProvider2 인터페이스</span><span class="sxs-lookup"><span data-stu-id="00256-190">IVsPathContextProvider2 interface</span></span>

```cs
    /// <summary>
    /// A factory to initialize <see cref="IVsPathContext2"/> instances.
    /// </summary>
    public interface IVsPathContextProvider2 : IVsPathContextProvider
    {
        /// <summary>
        /// Attempts to create an instance of <see cref="IVsPathContext2"/> for the solution.
        /// </summary>
        /// <param name="context">The path context associated with this solution.</param>
        /// <returns>
        /// <code>True</code> if operation has succeeded and context was created.
        /// <code>False</code> otherwise.
        /// </returns>
        /// <throws>
        /// <code>InvalidOperationException</code> when it fails to create a context and return appropriate error message.
        /// </throws>
        bool TryCreateSolutionContext(out IVsPathContext2 context);

        /// <summary>
        /// Attempts to create an instance of <see cref="IVsPathContext2"/> for the solution.
        /// </summary>
        /// <param name="solutionDirectory">
        /// path to the solution directory. Must be an absolute path.
        /// It will be performant to pass the solution directory if it's available.
        /// </param>
        /// <param name="context">The path context associated with this solution.</param>
        /// <returns>
        /// <code>True</code> if operation has succeeded and context was created.
        /// <code>False</code> otherwise.
        /// </returns>
        /// <throws>
        /// <code>ArgumentNullException</code> if solutionDirectory is passed as null.
        /// <code>InvalidOperationException</code> when it fails to create a context and return appropriate error message.
        /// </throws>
        bool TryCreateSolutionContext(string solutionDirectory, out IVsPathContext2 context);

        /// <summary>
        /// Attempts to create an instance of <see cref="IVsPathContext"/> containing only the user wide and machine wide configurations.
        /// If a solution is loaded, note that the values in the path context might not be the actual effective values for the solution.
        /// If a customer has overriden the `globalPackagesFolder` key or cleared the `fallbackPackageFolders`, these values will be incorrect.
        /// It is important to keep this scenario in mind when working with this path. To predict differences you can call this in combination with <see cref="TryCreateSolutionContext(out IVsPathContext2)"/>.
        /// </summary>
        /// <returns>
        /// <code>True</code> if operation has succeeded and context was created.
        /// <code>False</code> otherwise.
        /// </returns>
        /// <remarks>
        /// This method can be safely invoked from a background thread. Do note that this method might switch to the UI thread internally, so be mindful of blocking the UI thread on this.
        /// </remarks>
        bool TryCreateNoSolutionContext(out IVsPathContext vsPathContext);

```

## <a name="ivsprojectjsontopackagereferencemigrateresult-interface"></a><span data-ttu-id="00256-191">IVsProjectJsonToPackageReferenceMigrateResult 인터페이스</span><span class="sxs-lookup"><span data-stu-id="00256-191">IVsProjectJsonToPackageReferenceMigrateResult interface</span></span>

```cs
    /// <summary>
    /// Contains the result of the migrate operation on a legacy project.json project
    /// </summary>
    public interface IVsProjectJsonToPackageReferenceMigrateResult
    {
        /// <summary>
        /// Returns the success value of the migration operation.
        /// </summary>
        bool IsSuccess { get; }

        /// <summary>
        /// If migrate operation was unsuccessful, stores the error message in the exception.
        /// </summary>
        string ErrorMessage { get; }
    }
```

## <a name="ivsprojectjsontopackagereferencemigrator-interface"></a><span data-ttu-id="00256-192">IVsProjectJsonToPackageReferenceMigrator 인터페이스</span><span class="sxs-lookup"><span data-stu-id="00256-192">IVsProjectJsonToPackageReferenceMigrator interface</span></span>

```cs
    /// <summary>
    /// Contains methods to migrate a project.json based legacy project to PackageReference based project.
    /// </summary>
    public interface IVsProjectJsonToPackageReferenceMigrator
    {
        /// <summary>
        /// Migrates a legacy Project.json based project to Package Reference based project. The result 
        /// should be casted to type <see cref="IVsProjectJsonToPackageReferenceMigrateResult"/>
        /// The backup of the original project file and project.json file is created in the Backup folder
        /// in the root of the project directory.
        /// </summary>
        /// <param name="projectUniqueName">The full path to the project that needs to be migrated</param>
        Task<object> MigrateProjectJsonToPackageReferenceAsync(string projectUniqueName);

    }
```

## <a name="ivssemanticversioncomparer-interface"></a><span data-ttu-id="00256-193">IVsSemanticVersionComparer 인터페이스</span><span class="sxs-lookup"><span data-stu-id="00256-193">IVsSemanticVersionComparer interface</span></span>

```cs
    /// <summary>
    /// An interface for comparing two opaque version strings by treating them as NuGet semantic
    /// versions.
    /// </summary>
    public interface IVsSemanticVersionComparer
    {
        /// <summary>
        /// Compares two version strings as if they were NuGet semantic version
        /// strings. Returns a number less than zero if <paramref name="versionA"/>
        /// is less than <paramref name="versionB"/>. Returns zero if the two versions 
        /// are equivalent. Returns a number greater than zero if <paramref name="versionA"/>
        /// is greater than <paramref name="versionB"/>.
        /// </summary>
        /// <param name="versionA">The first version string.</param>
        /// <param name="versionB">The second version string.</param>
        /// <exception cref="ArgumentNullException">If either version string is null.</exception>
        /// <exception cref="ArgumentException">If either string cannot be parsed.</exception>
        /// <returns>
        /// A standard comparison integer based on the relationship between the
        /// two provided versions.
        /// </returns>
        int Compare(string versionA, string versionB);
    }
```

## <a name="ivstemplatewizard-interface"></a><span data-ttu-id="00256-194">IVsTemplateWizard 인터페이스</span><span class="sxs-lookup"><span data-stu-id="00256-194">IVsTemplateWizard interface</span></span>

```cs
/// <summary>
/// Defines the logic for a template wizard extension.
/// </summary>

public interface IVsTemplateWizard : IWizard
{
}
```
