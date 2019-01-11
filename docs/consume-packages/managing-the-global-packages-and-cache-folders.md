---
title: NuGet에서 전역 패키지, 캐시, 임시 폴더를 관리하는 방법
description: 패키지를 설치, 복원 및 업데이트할 때 사용되는 컴퓨터에 있는 전역 패키지 설치 폴더, 패키지 캐시 및 임시 폴더를 관리하는 방법입니다.
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: conceptual
ms.openlocfilehash: c547ae1d46079d040d7c3aa4c7678e70cd199dce
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548015"
---
# <a name="managing-the-global-packages-cache-and-temp-folders"></a><span data-ttu-id="e0f57-103">전역 패키지, 캐시 및 임시 폴더 관리</span><span class="sxs-lookup"><span data-stu-id="e0f57-103">Managing the global packages, cache, and temp folders</span></span>

<span data-ttu-id="e0f57-104">패키지를 설치, 업데이트 또는 복원할 때마다 NuGet은 프로젝트 구조 외부의 여러 폴더에서 패키지 및 패키지 정보를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="e0f57-104">Whenever you install, update, or restore a package, NuGet manages packages and package information in several folders outside of your project structure:</span></span>

| <span data-ttu-id="e0f57-105">name</span><span class="sxs-lookup"><span data-stu-id="e0f57-105">Name</span></span> | <span data-ttu-id="e0f57-106">설명 및 위치(사용자별)</span><span class="sxs-lookup"><span data-stu-id="e0f57-106">Description and Location (per user)</span></span>|
| --- | --- |
| <span data-ttu-id="e0f57-107">global&#8209;packages</span><span class="sxs-lookup"><span data-stu-id="e0f57-107">global&#8209;packages</span></span> | <span data-ttu-id="e0f57-108">*global-packages* 폴더는 NuGet이 다운로드한 패키지를 설치하는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="e0f57-108">The *global-packages* folder is where NuGet installs any downloaded package.</span></span> <span data-ttu-id="e0f57-109">각 패키지는 패키지 식별자 및 버전 번호와 일치하는 하위 폴더로 완전히 확장됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0f57-109">Each package is fully expanded into a subfolder that matches the package identifier and version number.</span></span> <span data-ttu-id="e0f57-110">PackageReference 형식을 사용하는 프로젝트는 항상 이 폴더의 직접 패키지를 직접 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e0f57-110">Projects using the PackageReference format always use packages directly from this folder.</span></span> <span data-ttu-id="e0f57-111">`packages.config`을 사용할 경우 패키지가 *global-packages* 폴더에 설치된 다음, 프로젝트의 `packages` 폴더에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0f57-111">When using the `packages.config`, packages are installed to the *global-packages* folder, then copied into the project's `packages` folder.</span></span><br/><ul><li><span data-ttu-id="e0f57-112">Windows: `%userprofile%\.nuget\packages`</span><span class="sxs-lookup"><span data-stu-id="e0f57-112">Windows: `%userprofile%\.nuget\packages`</span></span></li><li><span data-ttu-id="e0f57-113">Mac/Linux: `~/.nuget/packages`</span><span class="sxs-lookup"><span data-stu-id="e0f57-113">Mac/Linux: `~/.nuget/packages`</span></span></li><li><span data-ttu-id="e0f57-114">NUGET_PACKAGES 환경 변수 `globalPackagesFolder` 또는 `repositoryPath` [구성 설정](../reference/nuget-config-file.md#config-section)(각각 PackageReference 및 `packages.config`를 사용할 경우) 또는 `RestorePackagesPath` MSBuild 속성(MSBuild에만 해당)을 사용하여 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e0f57-114">Override using the NUGET_PACKAGES environment variable, the `globalPackagesFolder` or `repositoryPath` [configuration settings](../reference/nuget-config-file.md#config-section) (when using PackageReference and `packages.config`, respectively), or the `RestorePackagesPath` MSBuild property (MSBuild only).</span></span> <span data-ttu-id="e0f57-115">환경 변수가 구성 설정보다 우선 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0f57-115">The environment variable takes precedence over the configuration setting.</span></span></li></ul> |
| <span data-ttu-id="e0f57-116">http&#8209;cache</span><span class="sxs-lookup"><span data-stu-id="e0f57-116">http&#8209;cache</span></span> | <span data-ttu-id="e0f57-117">Visual Studio 패키지 관리자(NuGet 3.x 이상) 및 `dotnet` 도구는 다운로드한 패키지의 복사본을 이 캐시에 `.dat` 파일로 저장하고, 각 패키지 소스에 대해 하위 폴더를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e0f57-117">The Visual Studio Package Manager (NuGet 3.x+) and the `dotnet` tool store copies of downloaded packages in this cache (saved as `.dat` files), organized into subfolders for each package source.</span></span> <span data-ttu-id="e0f57-118">패키지는 확장되지 않으며 캐시의 만료 시간은 30분입니다.</span><span class="sxs-lookup"><span data-stu-id="e0f57-118">Packages are not expanded, and the cache has an expiration time of 30 minutes.</span></span><br/><ul><li><span data-ttu-id="e0f57-119">Windows: `%localappdata%\NuGet\v3-cache`</span><span class="sxs-lookup"><span data-stu-id="e0f57-119">Windows: `%localappdata%\NuGet\v3-cache`</span></span></li><li><span data-ttu-id="e0f57-120">Mac/Linux: `~/.local/share/NuGet/v3-cache`</span><span class="sxs-lookup"><span data-stu-id="e0f57-120">Mac/Linux: `~/.local/share/NuGet/v3-cache`</span></span></li><li><span data-ttu-id="e0f57-121">NUGET_HTTP_CACHE_PATH 환경 변수를 사용하여 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e0f57-121">Override using the NUGET_HTTP_CACHE_PATH environment variable.</span></span></li></ul> |
| <span data-ttu-id="e0f57-122">temp</span><span class="sxs-lookup"><span data-stu-id="e0f57-122">temp</span></span> | <span data-ttu-id="e0f57-123">NuGet이 다양한 작업을 수행하는 중 임시 파일을 저장하는 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="e0f57-123">A folder where NuGet stores temporary files during its various operations.</span></span><br/><li><span data-ttu-id="e0f57-124">Windows: `%temp%\NuGetScratch`</span><span class="sxs-lookup"><span data-stu-id="e0f57-124">Windows: `%temp%\NuGetScratch`</span></span></li><li><span data-ttu-id="e0f57-125">Mac/Linux: `/tmp/NuGetScratch`</span><span class="sxs-lookup"><span data-stu-id="e0f57-125">Mac/Linux: `/tmp/NuGetScratch`</span></span></li></ul> |
| <span data-ttu-id="e0f57-126">plugins-cache **4.8+**</span><span class="sxs-lookup"><span data-stu-id="e0f57-126">plugins-cache **4.8+**</span></span> | <span data-ttu-id="e0f57-127">NuGet이 작업 클레임 요청의 결과를 저장하는 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="e0f57-127">A folder where NuGet stores the results from the operation claims request.</span></span><br/><ul><li><span data-ttu-id="e0f57-128">Windows: `%localappdata%\NuGet\plugins-cache`</span><span class="sxs-lookup"><span data-stu-id="e0f57-128">Windows: `%localappdata%\NuGet\plugins-cache`</span></span></li><li><span data-ttu-id="e0f57-129">Mac/Linux: `~/.local/share/NuGet/plugins-cache`</span><span class="sxs-lookup"><span data-stu-id="e0f57-129">Mac/Linux: `~/.local/share/NuGet/plugins-cache`</span></span></li><li><span data-ttu-id="e0f57-130">NUGET_PLUGINS_CACHE_PATH 환경 변수를 사용하여 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e0f57-130">Override using the NUGET_PLUGINS_CACHE_PATH environment variable.</span></span></li></ul> |

> [!Note]
> <span data-ttu-id="e0f57-131">NuGet 3.5 이전에서는 `%localappdata%\NuGet\Cache`에 있는 *http-cache* 대신 *packages-cache*를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e0f57-131">NuGet 3.5 and earlier uses *packages-cache* instead of the *http-cache*, which is located in `%localappdata%\NuGet\Cache`.</span></span>

<span data-ttu-id="e0f57-132">NuGet은 캐시 및 *global-packages* 폴더를 사용하여 일반적으로 컴퓨터에 있는 이미 있는 패키지 다운로드를 방지하여 설치, 업데이트 및 복원 작업의 성능을 개선합니다.</span><span class="sxs-lookup"><span data-stu-id="e0f57-132">By using the cache and *global-packages* folders, NuGet generally avoids downloading packages that already exist on the computer, improving the performance of install, update, and restore operations.</span></span> <span data-ttu-id="e0f57-133">PackageReference를 사용하는 경우 *global-packages* 폴더는 다운로드한 패키지를 프로젝트 폴더 내에 보관하는 것도 막아 이러한 패키지가 소스 제어에 실수로 추가될 수 있는 문제를 방지하고 NuGet이 컴퓨터 스토리지에 미치는 전반적인 영향도 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="e0f57-133">When using PackageReference, the *global-packages* folder also avoids keeping downloaded packages inside project folders, where they might be inadvertently added to source control, and reduces NuGet's overall impact on computer storage.</span></span>

<span data-ttu-id="e0f57-134">패키지를 검색하라는 요청을 받으면 NuGet은 먼저 *global-packages* 폴더를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e0f57-134">When asked to retrieve a package, NuGet first looks in the *global-packages* folder.</span></span> <span data-ttu-id="e0f57-135">정확한 버전의 패키지가 없는 경우 NuGet은 모든 비 HTTP 패키지 소스를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e0f57-135">If the exact version of package is not there, then NuGet checks all non-HTTP package sources.</span></span> <span data-ttu-id="e0f57-136">그래도 패키지를 못 찾으면 NuGet은 `dotnet.exe` 명령에 `--no-cache` 또는 `nuget.exe` 명령에 `-NoCache`를 지정하지 않은 경우 *http-cache*에서 패키지를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e0f57-136">If the package is still not found, NuGet looks for the package in the *http-cache* unless you specify `--no-cache` with `dotnet.exe` commands or `-NoCache` with `nuget.exe` commands.</span></span> <span data-ttu-id="e0f57-137">패키지가 캐시에 없거나 캐시가 사용되지 않는 경우에는 NuGet은 HTTP를 통해 패키지를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="e0f57-137">If the package is not in the cache, or the cache isn't used, NuGet then retrieves the package over HTTP .</span></span>

<span data-ttu-id="e0f57-138">자세한 내용은 [패키지를 설치하면 어떻게 되나요?](ways-to-install-a-package.md#what-happens-when-a-package-is-installed)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0f57-138">For more information, see [What happens when a package is installed](ways-to-install-a-package.md#what-happens-when-a-package-is-installed).</span></span>

## <a name="viewing-folder-locations"></a><span data-ttu-id="e0f57-139">폴더 위치 보기</span><span class="sxs-lookup"><span data-stu-id="e0f57-139">Viewing folder locations</span></span>

<span data-ttu-id="e0f57-140">[nuget locals 명령](../tools/cli-ref-locals.md)을 사용하여 위치를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0f57-140">You can view locations using the [nuget locals command](../tools/cli-ref-locals.md):</span></span>

```cli
# Display locals for all folders: global-packages, http cache, temp and plugins cache
nuget locals all -list
```

<span data-ttu-id="e0f57-141">일반적인 출력(Windows. “user1”은 현재 사용자 이름):</span><span class="sxs-lookup"><span data-stu-id="e0f57-141">Typical output (Windows; "user1" is the current username):</span></span>

```output
http-cache: C:\Users\user1\AppData\Local\NuGet\v3-cache
global-packages: C:\Users\user1\.nuget\packages\
temp: C:\Users\user1\AppData\Local\Temp\NuGetScratch
plugins-cache: C:\Users\user1\AppData\Local\NuGet\plugins-cache
```

<span data-ttu-id="e0f57-142">(`package-cache`는 NuGet 2.x에서 사용되며 NuGet 3.5 이전 버전에서 표시됩니다. )</span><span class="sxs-lookup"><span data-stu-id="e0f57-142">(`package-cache` is used in NuGet 2.x and appears with NuGet 3.5 and earlier.)</span></span>

<span data-ttu-id="e0f57-143">[dotnet nuget locals 명령](/dotnet/core/tools/dotnet-nuget-locals)을 사용하여 폴더 위치를 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0f57-143">You can also view folder locations using the [dotnet nuget locals command](/dotnet/core/tools/dotnet-nuget-locals):</span></span>

```cli
dotnet nuget locals all --list
```

<span data-ttu-id="e0f57-144">일반적인 출력(Mac/Linux. “user1”은 현재 사용자 이름):</span><span class="sxs-lookup"><span data-stu-id="e0f57-144">Typical output (Mac/Linux; "user1" is the current username):</span></span>

```output
info : http-cache: /home/user1/.local/share/NuGet/v3-cache
info : global-packages: /home/user1/.nuget/packages/
info : temp: /tmp/NuGetScratch
info : plugins-cache: /home/user1/.local/share/NuGet/plugins-cache
```

<span data-ttu-id="e0f57-145">단일 폴더의 위치를 표시하려면 `all` 대신`http-cache`, `global-packages`, `temp` 또는 `plugins-cache`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e0f57-145">To display the location of a single folder, use `http-cache`, `global-packages`, `temp`, or `plugins-cache` instead of `all`.</span></span>

## <a name="clearing-local-folders"></a><span data-ttu-id="e0f57-146">로컬 폴더 지우기</span><span class="sxs-lookup"><span data-stu-id="e0f57-146">Clearing local folders</span></span>

<span data-ttu-id="e0f57-147">패키지 설치 문제가 발생하는 경우 또는 원격 갤러리의 패키지를 설치하려는 경우 `locals --clear`(dotnet.exe) 또는 `locals -clear`(nuget.exe) 옵션을 사용하여 지울 폴더를 지정하거나 `all`을 사용하여 모든 폴더를 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="e0f57-147">If you encounter package installation problems or otherwise want to ensure that you're installing packages from a remote gallery, use the `locals --clear` option (dotnet.exe) or `locals -clear` (nuget.exe), specifying the folder to clear, or `all` to clear all folders:</span></span>

```cli
# Clear the 3.x+ cache (use either command)
dotnet nuget locals http-cache --clear
nuget locals http-cache -clear

# Clear the 2.x cache (NuGet CLI 3.5 and earlier only)
nuget locals packages-cache -clear

# Clear the global packages folder (use either command)
dotnet nuget locals global-packages --clear
nuget locals global-packages -clear

# Clear the temporary cache (use either command)
dotnet nuget locals temp --clear
nuget locals temp -clear

# Clear the plugins cache (use either command)
dotnet nuget locals plugins-cache --clear
nuget locals plugins-cache -clear

# Clear all caches (use either command)
dotnet nuget locals all --clear
nuget locals all -clear
```

<span data-ttu-id="e0f57-148">현재 Visual Studio에서 열려 있는 프로젝트에서 사용되는 모든 패키지는 *global-packages* 폴더에서 지워지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e0f57-148">Any packages used by projects that are currently open in Visual Studio are not cleared from the *global-packages* folder.</span></span>

<span data-ttu-id="e0f57-149">Visual Studio 2017에서 **도구 > NuGet 패키지 관리자 > 패키지 관리자 설정** 메뉴 명령을 사용한 다음, **모든 NuGet 캐시 지우기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e0f57-149">In Visual Studio 2017, use the **Tools > NuGet Package Manager > Package Manager Settings** menu command, then select **Clear All NuGet Cache(s)**.</span></span> <span data-ttu-id="e0f57-150">캐시 관리는 현재 패키지 관리자 콘솔을 통해 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e0f57-150">Managing the cache isn't presently available through the Package Manager Console.</span></span> <span data-ttu-id="e0f57-151">Visual Studio 2015에서 CLI 명령을 대신 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e0f57-151">In Visual Studio 2015, use the CLI commands instead.</span></span>

![캐시를 지우기 위한 NuGet 옵션 명령](media/options-clear-caches.png)

## <a name="troubleshooting-errors"></a><span data-ttu-id="e0f57-153">오류 문제 해결</span><span class="sxs-lookup"><span data-stu-id="e0f57-153">Troubleshooting errors</span></span>

<span data-ttu-id="e0f57-154">`nuget locals` 또는 `dotnet nuget locals`를 사용하는 경우 다음과 같은 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0f57-154">The following errors can occur when using `nuget locals` or `dotnet nuget locals`:</span></span>

- <span data-ttu-id="e0f57-155">‘오류: <package> 파일은 다른 프로세스에서 사용 중이므로 프로세스에서 이 파일에 액세스할 수 없습니다’ 또는 ‘로컬 리소스 지우기 실패: 하나 이상의 파일을 삭제할 수 없습니다’</span><span class="sxs-lookup"><span data-stu-id="e0f57-155">*Error: The process cannot access the file <package> because it is being used by another process* or *Clearing local resources failed: Unable to delete one or more files*</span></span>

    <span data-ttu-id="e0f57-156">폴더에 있는 하나 이상의 파일이 다른 프로세스에서 사용 중입니다. 예를 들어 *global-packages* 폴더의 패키지를 참조하는 Visual Studio 프로젝트가 열려 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0f57-156">One or more files in the folder are in use by another process; for example, a Visual Studio project is open that refers to packages in the *global-packages* folder.</span></span> <span data-ttu-id="e0f57-157">해당 프로세스를 닫고 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="e0f57-157">Close those processes and try again.</span></span>

- <span data-ttu-id="e0f57-158">*오류: <path> 경로에 대한 액세스가 거부되었습니다’ 또는 ‘디렉터리가 비어 있지 않습니다’*</span><span class="sxs-lookup"><span data-stu-id="e0f57-158">*Error: Access to the path <path> is denied* or *The directory is not empty*</span></span>

    <span data-ttu-id="e0f57-159">캐시에서 파일을 삭제할 수 있는 권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e0f57-159">You don't have permission to delete files in the cache.</span></span> <span data-ttu-id="e0f57-160">가능한 경우 폴더 권한을 변경하고 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="e0f57-160">Change the folder permissions, if possible, and try again.</span></span> <span data-ttu-id="e0f57-161">또는 시스템 관리자에게 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="e0f57-161">Otherwise, contact your system administrator.</span></span>

- <span data-ttu-id="e0f57-162">*오류: 지정된 경로, 파일 이름 중 하나 또는 둘 다가 너무 깁니다. 정규화된 파일 이름은 260자 미만이어야 하며 디렉터리 이름은 248자 미만이어야 합니다.*</span><span class="sxs-lookup"><span data-stu-id="e0f57-162">*Error: The specified path, file name, or both are too long. The fully qualified file name must be less than 260 characters, and the directory name must be less than 248 characters.*</span></span>

    <span data-ttu-id="e0f57-163">폴더 이름을 줄이고 다시 시도하세요.</span><span class="sxs-lookup"><span data-stu-id="e0f57-163">Shorten the folder names and try again.</span></span>
