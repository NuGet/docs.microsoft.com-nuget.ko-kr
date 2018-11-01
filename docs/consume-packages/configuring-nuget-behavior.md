---
title: NuGet 동작 구성
description: NuGet.Config 파일은 NuGet의 동작을 전역 및 프로젝트별로 제어하며 nuget config 명령으로 수정됩니다.
author: karann-msft
ms.author: karann
ms.date: 10/25/2017
ms.topic: conceptual
ms.openlocfilehash: c23b464ca39fd8d872f21846a7d6d34edf9dce93
ms.sourcegitcommit: 1bd72dca2f85b4267b9924236f1d23dd7b0ed733
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50088923"
---
# <a name="configuring-nuget-behavior"></a><span data-ttu-id="80ba0-103">NuGet 동작 구성</span><span class="sxs-lookup"><span data-stu-id="80ba0-103">Configuring NuGet behavior</span></span>

<span data-ttu-id="80ba0-104">NuGet의 동작은 프로젝트, 사용자 및 컴퓨터 수준에서 존재할 수 있는 하나 이상의 `NuGet.Config`(XML) 파일에 누적된 설정으로 구동됩니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-104">NuGet's behavior is driven by the accumulated settings in one or more `NuGet.Config` (XML) files that can exist at project-, user-, and computer-wide levels.</span></span> <span data-ttu-id="80ba0-105">특히 전역 `NuGetDefaults.Config` 파일은 패키지 원본도 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-105">A global `NuGetDefaults.Config` file also specifically configures package sources.</span></span> <span data-ttu-id="80ba0-106">설정은 CLI, 패키지 관리자 콘솔 및 패키지 관리자 UI에서 실행되는 모든 명령에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-106">Settings apply to all commands issued in the CLI, the Package Manager Console, and the Package Manager UI.</span></span>

## <a name="config-file-locations-and-uses"></a><span data-ttu-id="80ba0-107">Config 파일 위치 및 사용</span><span class="sxs-lookup"><span data-stu-id="80ba0-107">Config file locations and uses</span></span>

| <span data-ttu-id="80ba0-108">범위</span><span class="sxs-lookup"><span data-stu-id="80ba0-108">Scope</span></span> | <span data-ttu-id="80ba0-109">NuGet.Config 파일 위치</span><span class="sxs-lookup"><span data-stu-id="80ba0-109">NuGet.Config file location</span></span> | <span data-ttu-id="80ba0-110">설명</span><span class="sxs-lookup"><span data-stu-id="80ba0-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="80ba0-111">프로젝트</span><span class="sxs-lookup"><span data-stu-id="80ba0-111">Project</span></span> | <span data-ttu-id="80ba0-112">현재 폴더(프로젝트 폴더) 또는 드라이브 루트까지의 모든 폴더</span><span class="sxs-lookup"><span data-stu-id="80ba0-112">Current folder (aka Project folder) or any folder up to the drive root.</span></span>| <span data-ttu-id="80ba0-113">프로젝트 폴더의 설정은 해당 프로젝트에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-113">In a project folder, settings apply only to that project.</span></span> <span data-ttu-id="80ba0-114">여러 프로젝트 하위 폴더가 있는 부모 폴더의 설정은 해당 하위 폴더의 모든 프로젝트에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-114">In parent folders that contain multiple projects subfolders, settings apply to all projects in those subfolders.</span></span> |
| <span data-ttu-id="80ba0-115">사용자</span><span class="sxs-lookup"><span data-stu-id="80ba0-115">User</span></span> | <span data-ttu-id="80ba0-116">Windows: `%appdata%\NuGet\NuGet.Config`</span><span class="sxs-lookup"><span data-stu-id="80ba0-116">Windows: `%appdata%\NuGet\NuGet.Config`</span></span><br/><span data-ttu-id="80ba0-117">Mac/Linux: `~/.config/NuGet/NuGet.Config` 또는 `~/.nuget/NuGet/NuGet.Config`(OS 배포에 따라 다름)</span><span class="sxs-lookup"><span data-stu-id="80ba0-117">Mac/Linux: `~/.config/NuGet/NuGet.Config` or `~/.nuget/NuGet/NuGet.Config` (varies by OS distribution)</span></span> | <span data-ttu-id="80ba0-118">설정은 모든 작업에 적용되지만, 프로젝트 수준 설정에 따라 재정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-118">Settings apply to all operations, but are overridden by any project-level settings.</span></span> |
| <span data-ttu-id="80ba0-119">컴퓨터</span><span class="sxs-lookup"><span data-stu-id="80ba0-119">Computer</span></span> | <span data-ttu-id="80ba0-120">Windows: `%ProgramFiles(x86)%\NuGet\Config`</span><span class="sxs-lookup"><span data-stu-id="80ba0-120">Windows: `%ProgramFiles(x86)%\NuGet\Config`</span></span><br/><span data-ttu-id="80ba0-121">Mac/Linux: `$XDG_DATA_HOME`.</span><span class="sxs-lookup"><span data-stu-id="80ba0-121">Mac/Linux: `$XDG_DATA_HOME`.</span></span> <span data-ttu-id="80ba0-122">`$XDG_DATA_HOME`이 null이거나 비어 있으면 `~/.local/share` 또는 `/usr/local/share`가 사용됨(OS 배포에 따라 다름)</span><span class="sxs-lookup"><span data-stu-id="80ba0-122">If `$XDG_DATA_HOME` is null or empty, `~/.local/share` or `/usr/local/share` will be used (varies by OS distribution)</span></span>  | <span data-ttu-id="80ba0-123">설정은 컴퓨터의 모든 작업에 적용되지만, 사용자 또는 프로젝트 수준 설정에 따라 재정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-123">Settings apply to all operations on the computer, but are overridden by any user- or project-level settings.</span></span> |

<span data-ttu-id="80ba0-124">이전 버전의 NuGet에 대한 참고 사항:</span><span class="sxs-lookup"><span data-stu-id="80ba0-124">Notes for earlier versions of NuGet:</span></span>
- <span data-ttu-id="80ba0-125">NuGet 3.3 및 이전 버전에서는 솔루션 수준 설정에 대해 `.nuget` 폴더를 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-125">NuGet 3.3 and earlier used a `.nuget` folder for solution-wide settings.</span></span> <span data-ttu-id="80ba0-126">NuGet 3.4 이상에서는 이 파일이 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-126">This file is not used in NuGet 3.4+.</span></span>
- <span data-ttu-id="80ba0-127">NuGet 2.6 - 3.x의 경우, Windows의 컴퓨터 수준 구성 파일은 %ProgramData%\NuGet\Config[\\{IDE}[\\{Version}[\\{SKU}]]]\NuGet.Config에 있습니다. 여기서 *{IDE}* 는 *VisualStudio*일 수 있고, *{Version}* 은 *14.0*과 같은 Visual Studio 버전이고, *{SKU}* 는 *Community*, *Pro* 또는 *Enterprise* 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-127">For NuGet 2.6 to 3.x, the computer-level config file on Windows was located in %ProgramData%\NuGet\Config[\\{IDE}[\\{Version}[\\{SKU}]]]\NuGet.Config, where *{IDE}* can be *VisualStudio*, *{Version}* was the Visual Studio version such as *14.0*, and *{SKU}* is either *Community*, *Pro*, or *Enterprise*.</span></span> <span data-ttu-id="80ba0-128">설정을 NuGet 4.0 이상으로 마이그레이션하려면 구성 파일을 %ProgramFiles(x86)%\NuGet\Config에 복사하기만 하면 됩니다. Linux의 경우 이전의 이 위치는 /etc/opt이고, Mac의 경우 /Library/Application Support입니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-128">To migrate settings to NuGet 4.0+, simply copy the config file to %ProgramFiles(x86)%\NuGet\Config. On Linux, this previous location was /etc/opt, and on Mac, /Library/Application Support.</span></span>

## <a name="changing-config-settings"></a><span data-ttu-id="80ba0-129">구성 설정 변경</span><span class="sxs-lookup"><span data-stu-id="80ba0-129">Changing config settings</span></span>

<span data-ttu-id="80ba0-130">`NuGet.Config` 파일은 [NuGet 구성 설정](../reference/nuget-config-file.md) 항목에서 설명한 대로 키/값 쌍을 포함한 간단한 XML 텍스트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-130">A `NuGet.Config` file is a simple XML text file containing key/value pairs as described in the [NuGet Configuration Settings](../reference/nuget-config-file.md) topic.</span></span>

<span data-ttu-id="80ba0-131">설정은 NuGet CLI [config 명령](../tools/cli-ref-config.md)을 사용하여 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-131">Settings are managed using the NuGet CLI [config command](../tools/cli-ref-config.md):</span></span>
- <span data-ttu-id="80ba0-132">기본적으로 사용자 수준 구성 파일이 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-132">By default, changes are made to the user-level config file.</span></span>
- <span data-ttu-id="80ba0-133">다른 파일의 설정을 변경하려면 `-configFile` 스위치를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-133">To change settings in a different file, use the `-configFile` switch.</span></span> <span data-ttu-id="80ba0-134">이 경우 파일은 모든 파일 이름을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-134">In this case files can use any filename.</span></span>
- <span data-ttu-id="80ba0-135">키는 항상 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-135">Keys are always case sensitive.</span></span>
- <span data-ttu-id="80ba0-136">컴퓨터 수준 설정 파일의 설정을 변경하려면 권한 상승이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-136">Elevation is required to change settings in the computer-level settings file.</span></span>

> [!Warning]
> <span data-ttu-id="80ba0-137">텍스트 편집기에서 파일을 수정할 수 있지만, NuGet(v3.4.3 이상)은 잘못된 XML(일치하지 않는 태그, 잘못된 인용 부호 등)이 포함된 경우 전체 구성 파일을 자동으로 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-137">Although you can modify the file in any text editor, NuGet (v3.4.3 and later) silently ignores the entire configuration file if it contains malformed XML (mismatched tags, invalid quotation marks, etc.).</span></span> <span data-ttu-id="80ba0-138">따라서 `nuget config`를 사용하여 설정을 관리하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-138">This is why it's preferable to manage setting using `nuget config`.</span></span>

### <a name="setting-a-value"></a><span data-ttu-id="80ba0-139">값 설정</span><span class="sxs-lookup"><span data-stu-id="80ba0-139">Setting a value</span></span>

<span data-ttu-id="80ba0-140">Windows:</span><span class="sxs-lookup"><span data-stu-id="80ba0-140">Windows:</span></span>

```cli
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=c:\packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=c:\packages -configfile c:\my.Config
nuget config -set repositoryPath=c:\packages -configfile .\myApp\NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=c:\packages -configfile %ProgramFiles(x86)%\NuGet\Config\NuGet.Config
```

<span data-ttu-id="80ba0-141">Mac/Linux:</span><span class="sxs-lookup"><span data-stu-id="80ba0-141">Mac/Linux:</span></span>

```cli
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=/home/packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=/home/projects/packages -configfile /home/my.Config
nuget config -set repositoryPath=/home/packages -configfile home/myApp/NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=/home/packages -configfile $XDG_DATA_HOME/NuGet.Config
```

> [!Note]
> <span data-ttu-id="80ba0-142">NuGet 3.4 이상에서는 `repositoryPath=%PACKAGEHOME%`(Windows) 및 `repositoryPath=$PACKAGEHOME`(Mac/Linux)과 같이 모든 값에 환경 변수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-142">In NuGet 3.4 and later you can use environment variables in any value, as in `repositoryPath=%PACKAGEHOME%` (Windows) and `repositoryPath=$PACKAGEHOME` (Mac/Linux).</span></span>

### <a name="removing-a-value"></a><span data-ttu-id="80ba0-143">값 제거</span><span class="sxs-lookup"><span data-stu-id="80ba0-143">Removing a value</span></span>

<span data-ttu-id="80ba0-144">값을 제거하려면 빈 값이 있는 키를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-144">To remove a value, specify a key with an empty value.</span></span>

```cli
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a><span data-ttu-id="80ba0-145">새 구성 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="80ba0-145">Creating a new config file</span></span>

<span data-ttu-id="80ba0-146">아래 템플릿을 새 파일에 복사한 다음 `nuget config -configFile <filename>`을 사용하여 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-146">Copy the template below into the new file and then use `nuget config -configFile <filename>` to set values:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

## <a name="how-settings-are-applied"></a><span data-ttu-id="80ba0-147">설정 적용 방법</span><span class="sxs-lookup"><span data-stu-id="80ba0-147">How settings are applied</span></span>

<span data-ttu-id="80ba0-148">여러 `NuGet.Config` 파일을 사용하면 설정을 다른 위치에 저장하여 단일 프로젝트, 프로젝트 그룹 또는 모든 프로젝트에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-148">Multiple `NuGet.Config` files allow you to store settings in different locations so that they apply to a single project, a group of projects, or all projects.</span></span> <span data-ttu-id="80ba0-149">이러한 설정은 명령줄 또는 Visual Studio에서 호출된 모든 NuGet 작업에 일괄적으로 적용되며, 프로젝트 또는 현재 폴더에 "가장 가까운" 설정이 우선 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-149">These settings collectively apply to any NuGet operation invoked from the command line or from Visual Studio, with settings that exist "closest" to a project or the current folder taking precedence.</span></span>

<span data-ttu-id="80ba0-150">특히 NuGet은 다음과 같은 순서로 다른 구성 파일의 설정을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-150">Specifically, NuGet loads settings from the different config files in the following order:</span></span>

1. <span data-ttu-id="80ba0-151">[NuGetDefaults.Config 파일](#nuget-defaults-file)(패키지 원본에만 관련된 설정이 포함되어 있음)</span><span class="sxs-lookup"><span data-stu-id="80ba0-151">The [NuGetDefaults.Config file](#nuget-defaults-file), which contains settings related only to package sources.</span></span>
1. <span data-ttu-id="80ba0-152">컴퓨터 수준 파일</span><span class="sxs-lookup"><span data-stu-id="80ba0-152">The computer-level file.</span></span>
1. <span data-ttu-id="80ba0-153">사용자 수준 파일</span><span class="sxs-lookup"><span data-stu-id="80ba0-153">The user-level file.</span></span>
1. <span data-ttu-id="80ba0-154">`-configFile`로 지정된 파일</span><span class="sxs-lookup"><span data-stu-id="80ba0-154">The file specified with `-configFile`.</span></span>
1. <span data-ttu-id="80ba0-155">드라이브 루트에서 현재 폴더(nuget.exe가 호출되는 위치 또는 Visual Studio 프로젝트가 포함된 폴더)까지에 이르는 경로의 모든 폴더에 있는 파일 -</span><span class="sxs-lookup"><span data-stu-id="80ba0-155">Files found in every folder in the path from the drive root to the current folder (where nuget.exe is invoked or the folder containing the Visual Studio project).</span></span> <span data-ttu-id="80ba0-156">예를 들어 명령이 c:\A\B\C에서 호출되면 NuGet은 c:\,, c:\A, c:\A\B 및 마지막으로 c:\A\B\C에서 구성 파일을 찾아 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-156">For example, if a command is invoked in c:\A\B\C, NuGet looks for and loads config files in c:\, then c:\A, then c:\A\B, and finally c:\A\B\C.</span></span>

<span data-ttu-id="80ba0-157">NuGet은 이러한 파일에서 설정을 찾으면 다음과 같이 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-157">As NuGet finds settings in these files, they are applied as follows:</span></span>

1. <span data-ttu-id="80ba0-158">단일 항목 요소의 경우 NuGet은 동일한 키에 대해 이전에 찾은 값을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-158">For single-item elements, NuGet replaced any previously-found value for the same key.</span></span> <span data-ttu-id="80ba0-159">즉 현재 폴더 또는 프로젝트에 "가장 가까운" 설정이 이전에 찾은 다른 설정을 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-159">This means that settings that are "closest" to the current folder or project override any others found earlier.</span></span> <span data-ttu-id="80ba0-160">예를 들어 `NuGetDefaults.Config`의 `defaultPushSource` 설정은 다른 설정 파일에 있는 경우 재정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-160">For example, the `defaultPushSource` setting in `NuGetDefaults.Config` is overridden if it exists in any other config file.</span></span>

1. <span data-ttu-id="80ba0-161">컬렉션 요소(예: `<packageSources>`)의 경우 NuGet은 모든 구성 파일의 값을 단일 컬렉션으로 결합합니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-161">For collection elements (such as `<packageSources>`), NuGet combines the values from all configuration files into a single collection.</span></span>

1. <span data-ttu-id="80ba0-162">지정된 노드에 대해 `<clear />`가 있으면 NuGet은 해당 노드에 대해 이전에 정의된 구성 값을 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-162">When `<clear />` is present for a given node, NuGet ignores previously defined configuration values for that node.</span></span>

### <a name="settings-walkthrough"></a><span data-ttu-id="80ba0-163">설정 연습</span><span class="sxs-lookup"><span data-stu-id="80ba0-163">Settings walkthrough</span></span>

<span data-ttu-id="80ba0-164">두 개의 개별 드라이브에 다음과 같은 폴더 구조가 있다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-164">Let's say you have the following folder structure on two separate drives:</span></span>

    disk_drive_1
        User
    disk_drive_2
       Project1
         Source
       Project2
         Source
       tmp

<span data-ttu-id="80ba0-165">다음으로, 지정된 내용이 포함된 4개의 `NuGet.Config` 파일이 다음 위치에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-165">You then have four `NuGet.Config` files in the following locations with the given content.</span></span> <span data-ttu-id="80ba0-166">(컴퓨터 수준 파일은 이 예제에 포함되어 있지 않지만 사용자 수준 파일과 비슷하게 작동합니다.)</span><span class="sxs-lookup"><span data-stu-id="80ba0-166">(The computer-level file is not included in this example, but would behave similarly to the user-level file.)</span></span>

<span data-ttu-id="80ba0-167">파일 A - 사용자 수준 파일(Windows의 경우 `%appdata%\NuGet\NuGet.Config`, Mac/Linux의 경우 `~/.config/NuGet/NuGet.Config`):</span><span class="sxs-lookup"><span data-stu-id="80ba0-167">File A. User-level file, (`%appdata%\NuGet\NuGet.Config` on Windows, `~/.config/NuGet/NuGet.Config` on Mac/Linux):</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <activePackageSource>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
    </activePackageSource>
</configuration>
```

<span data-ttu-id="80ba0-168">파일 B - disk_drive_2/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="80ba0-168">File B. disk_drive_2/NuGet.Config:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <add key="repositoryPath" value="disk_drive_2/tmp" />
    </config>
    <packageRestore>
        <add key="enabled" value="True" />
    </packageRestore>
</configuration>
```

<span data-ttu-id="80ba0-169">파일 C - disk_drive_2/Project1/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="80ba0-169">File C. disk_drive_2/Project1/NuGet.Config:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <add key="repositoryPath" value="External/Packages" />
        <add key="defaultPushSource" value="https://MyPrivateRepo/ES/api/v2/package" />
    </config>
    <packageSources>
        <clear /> <!-- ensure only the sources defined below are used -->
        <add key="MyPrivateRepo - ES" value="https://MyPrivateRepo/ES/nuget" />
    </packageSources>
</configuration>
```

<span data-ttu-id="80ba0-170">파일 D - disk_drive_2/Project2/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="80ba0-170">File D. disk_drive_2/Project2/NuGet.Config:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <packageSources>
        <!-- Add this repository to the list of available repositories -->
        <add key="MyPrivateRepo - DQ" value="https://MyPrivateRepo/DQ/nuget" />
    </packageSources>
</configuration>
```

<span data-ttu-id="80ba0-171">그런 다음 NuGet은 호출된 위치에 따라 다음과 같이 설정을 로드하고 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-171">NuGet then loads and applies settings as follows, depending on where it's invoked:</span></span>

- <span data-ttu-id="80ba0-172">**disk_drive_1/users에서 호출됨**: disk_drive_1에 있는 유일한 파일이기 때문에 사용자 수준 구성 파일(A)에 나열된 기본 리포지토리만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-172">**Invoked from disk_drive_1/users**: Only the default repository listed in the user-level configuration file (A) is used, because that's the only file found on disk_drive_1.</span></span>

- <span data-ttu-id="80ba0-173">**disk_drive_2/ or disk_drive_/tmp에서 호출됨**: 사용자 수준 파일(A)이 먼저 로드된 다음, NuGet에서 disk_drive_2의 루트로 이동하여 파일(B)을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-173">**Invoked from disk_drive_2/ or disk_drive_/tmp**: The user-level file (A) is loaded first, then NuGet goes to the root of disk_drive_2 and finds file (B).</span></span> <span data-ttu-id="80ba0-174">또한 NuGet은 /tmp에 있는 구성 파일을 찾지만 하나도 찾을 수가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-174">NuGet also looks for a configuration file in /tmp but does not find one.</span></span> <span data-ttu-id="80ba0-175">따라서 nuget.org의 기본 리포지토리가 사용되고, 패키지 복원을 사용하도록 설정되고, 패키지가 disk_drive_2/tmp로 확장됩니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-175">As a result, the default repository on nuget.org is used, package restore is enabled, and packages get expanded in disk_drive_2/tmp.</span></span>

- <span data-ttu-id="80ba0-176">**disk_drive_2/Project1 또는 disk_drive_2/Project1/Source에서 호출됨**: 사용자 수준 파일(A)이 먼저 로드된 다음, NuGet에서 disk_drive_2의 루트에서 (B), (C) 파일을 차례로 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-176">**Invoked from disk_drive_2/Project1 or disk_drive_2/Project1/Source**: The user-level file (A) is loaded first, then NuGet loads file (B) from the root of disk_drive_2, followed by file (C).</span></span> <span data-ttu-id="80ba0-177">(C)의 설정은 (B) 및 (A)의 설정을 재정의하므로 패키지가 설치되는 `repositoryPath`는 *disk_drive_2/tmp* 대신 disk_drive_2/Project1/External/Packages입니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-177">Settings in (C) override those in (B) and (A), so the `repositoryPath` where packages get installed is disk_drive_2/Project1/External/Packages instead of *disk_drive_2/tmp*.</span></span> <span data-ttu-id="80ba0-178">또한 (C)에서 `<packageSources>`를 지우므로 `https://MyPrivateRepo/ES/nuget`만 남아 있는 nuget.org는 더 이상 원본으로 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-178">Also, because (C) clears `<packageSources>`, nuget.org is no longer available as a source leaving only `https://MyPrivateRepo/ES/nuget`.</span></span>

- <span data-ttu-id="80ba0-179">**disk_drive_2/Project2 또는 disk_drive_2/Project2/Source에서 호출됨**: 사용자 수준 파일(A)이 먼저 로드된 다음, 파일(B) 및 파일(D)이 차례로 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-179">**Invoked from disk_drive_2/Project2 or disk_drive_2/Project2/Source**: The user-level file (A) is loaded first followed by file (B) and file (D).</span></span> <span data-ttu-id="80ba0-180">`packageSources`를 지우지 않으므로 `nuget.org`와 `https://MyPrivateRepo/DQ/nuget`은 모두 원본으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-180">Because `packageSources` is not cleared, both `nuget.org` and `https://MyPrivateRepo/DQ/nuget` are available as sources.</span></span> <span data-ttu-id="80ba0-181">패키지는 (B)에서 지정한 대로 disk_drive_2/mp로 확장됩니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-181">Packages get expanded in disk_drive_2/tmp as specified in (B).</span></span>

## <a name="nuget-defaults-file"></a><span data-ttu-id="80ba0-182">NuGet 기본 파일</span><span class="sxs-lookup"><span data-stu-id="80ba0-182">NuGet defaults file</span></span>

<span data-ttu-id="80ba0-183">패키지가 설치되고 업데이트되는 패키지 원본을 지정하고 `nuget push`를 사용하여 패키지를 게시하기 위한 기본 대상을 제어하기 위해 `NuGetDefaults.Config` 파일이 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-183">The `NuGetDefaults.Config` file exists to specify package sources from which packages are installed and updated, and to control the default target for publishing packages with `nuget push`.</span></span> <span data-ttu-id="80ba0-184">관리자는 개발자와 빌드 컴퓨터에 일관된 `NuGetDefaults.Config` 파일을 편리하게(예: 그룹 정책 사용) 배포할 수 있으므로, 조직의 모든 사용자가 nuget.org가 아닌 올바른 패키지 원본을 사용하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-184">Because administrators can conveniently (using Group Policy, for example) deploy consistent `NuGetDefaults.Config` files to developer and build machines, they can ensuring that everyone in the organization is using the correct package sources rather than nuget.org.</span></span>

> [!Important]
> <span data-ttu-id="80ba0-185">`NuGetDefaults.Config` 파일은 개발자의 NuGet 구성에서 패키지 원본이 제거되지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-185">The `NuGetDefaults.Config` file never causes a package source to be removed from a developer's NuGet configuration.</span></span> <span data-ttu-id="80ba0-186">즉 개발자가 이미 NuGet을 사용하고 있고 이에 따라 등록된 nuget.org 패키지 원본이 있는 경우 `NuGetDefaults.Config` 파일을 만든 후에도 패키지 원본이 제거되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-186">That means if the developer has already used NuGet and therefore has the nuget.org package source registered, it won't be removed after the creation of a `NuGetDefaults.Config` file.</span></span>
>
> <span data-ttu-id="80ba0-187">또한 NuGet의 `NuGetDefaults.Config` 또는 다른 메커니즘도 nuget.org와 같은 패키지 원본에 대한 액세스를 차단할 수 없습니다. 조직이 이러한 액세스를 차단하려는 경우 방화벽과 같은 다른 방법을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-187">Furthermore, neither `NuGetDefaults.Config` nor any other mechanism in NuGet can prevent access to package sources like nuget.org. If an organization wishes to block such access, it must use other means such as firewalls to do so.</span></span>

### <a name="nugetdefaultsconfig-location"></a><span data-ttu-id="80ba0-188">NuGetDefaults.Config 위치</span><span class="sxs-lookup"><span data-stu-id="80ba0-188">NuGetDefaults.Config location</span></span>

<span data-ttu-id="80ba0-189">다음 표에서는 대상 OS에 따라 `NuGetDefaults.Config` 파일을 저장해야 하는 위치를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-189">The following table describes where the `NuGetDefaults.Config` file should be stored, depending on the target OS:</span></span>

| <span data-ttu-id="80ba0-190">OS 플랫폼</span><span class="sxs-lookup"><span data-stu-id="80ba0-190">OS Platform</span></span>  | <span data-ttu-id="80ba0-191">NuGetDefaults.Config 위치</span><span class="sxs-lookup"><span data-stu-id="80ba0-191">NuGetDefaults.Config Location</span></span> |
| --- | --- |
| <span data-ttu-id="80ba0-192">Windows</span><span class="sxs-lookup"><span data-stu-id="80ba0-192">Windows</span></span>      | <span data-ttu-id="80ba0-193">**Visual Studio 2017 또는 NuGet 4.x 이상:** `%ProgramFiles(x86)%\NuGet\Config`</span><span class="sxs-lookup"><span data-stu-id="80ba0-193">**Visual Studio 2017 or NuGet 4.x+:** `%ProgramFiles(x86)%\NuGet\Config`</span></span> <br /><span data-ttu-id="80ba0-194">**Visual Studio 2015 이하 또는 NuGet 3.x 이하:** `%PROGRAMDATA%\NuGet`</span><span class="sxs-lookup"><span data-stu-id="80ba0-194">**Visual Studio 2015 and earlier or NuGet 3.x and earlier:** `%PROGRAMDATA%\NuGet`</span></span> |
| <span data-ttu-id="80ba0-195">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="80ba0-195">Mac/Linux</span></span>    | <span data-ttu-id="80ba0-196">`$XDG_DATA_HOME`(일반적으로 OS 배포에 따라 `~/.local/share` 또는 `/usr/local/share`)</span><span class="sxs-lookup"><span data-stu-id="80ba0-196">`$XDG_DATA_HOME` (typically `~/.local/share` or `/usr/local/share`, depending on OS distribution)</span></span>|

### <a name="nugetdefaultsconfig-settings"></a><span data-ttu-id="80ba0-197">NuGetDefaults.Config 설정</span><span class="sxs-lookup"><span data-stu-id="80ba0-197">NuGetDefaults.Config settings</span></span>

- <span data-ttu-id="80ba0-198">`packageSources`: 이 컬렉션은 일반 설정 파일에서 `packageSources`와 동일한 의미를 가지며, 기본 원본을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-198">`packageSources`: this collection has the same meaning as `packageSources` in regular config files and specifies the default sources.</span></span> <span data-ttu-id="80ba0-199">NuGet은 `packages.config` 관리 형식을 사용하는 프로젝트에서 패키지를 설치하거나 업데이트할 때 소스를 순서대로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-199">NuGet uses the sources in order when installing or updating packages in projects using the `packages.config` management format.</span></span> <span data-ttu-id="80ba0-200">PackageReference 형식을 사용하는 프로젝트의 경우, NuGet은 구성 파일의 순서에 관계없이 로컬 소스를 먼저 사용하고, 네트워크 공유의 소스를 사용한 후, HTTP 소스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-200">For projects using the PackageReference format, NuGet uses local sources first, then sources on network shares, then HTTP sources, regardless of the order in the configuration files.</span></span> <span data-ttu-id="80ba0-201">NuGet은 복원 작업에서 소스 순서를 항상 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-201">NuGet always ignores the order of sources with restore operations.</span></span>

- <span data-ttu-id="80ba0-202">`disabledPackageSources`: 이 컬렉션은 `NuGet.Config` 파일과 동일한 의미를 가지며, 영향을 받는 각 원본이 이름 및 사용하지 않도록 설정되어 있는지 여부를 나타내는 true/false 값으로 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-202">`disabledPackageSources`: this collection also has the same meaning as in `NuGet.Config` files, where each affected source is listed by its name and a true/false value indicating whether it's disabled.</span></span> <span data-ttu-id="80ba0-203">이렇게 하면 원본 이름과 URL이 기본적으로 설정되지 않고 `packageSources`에 남아 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-203">This allows the source name and URL to remain in `packageSources` without having it turned on by default.</span></span> <span data-ttu-id="80ba0-204">개별 개발자는 올바른 URL을 다시 찾지 않고도 다른 `NuGet.Config` 파일에서 원본의 값을 false로 설정하여 원본을 사용하도록 다시 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-204">Individual developers can then re-enable the source by setting the source's value to false in other `NuGet.Config` files without having to find the correct URL again.</span></span> <span data-ttu-id="80ba0-205">또한 이는 기본적으로 개별 팀의 원본만 사용하도록 설정하면서 개발자에게 조직의 내부 원본 URL에 대한 전체 목록을 제공하는 데에도 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-205">This is also useful to supply developers with a full list of internal source URLs for an organization while enabling only an individual team's source by default.</span></span>

- <span data-ttu-id="80ba0-206">`defaultPushSource`: `nuget push` 작업에 대한 기본 대상을 지정하여 nuget.org의 기본 제공된 기본값을 재정의합니다. 개발자는 특별히 `nuget push -Source`를 사용하여 nuget.org에 게시해야 하므로, 관리자가 이 설정을 배포하여 실수로 내부 패키지를 공용 nuget.org에 게시하지 않도록 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80ba0-206">`defaultPushSource`: specifies the default target for `nuget push` operations, overriding the built-in default of nuget.org. Administrators can deploy this setting to avoid publishing internal packages to the public nuget.org by accident, as developers specifically need to use `nuget push -Source` to publish to nuget.org.</span></span>

### <a name="example-nugetdefaultsconfig-and-application"></a><span data-ttu-id="80ba0-207">예제 NuGetDefaults.Config 및 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="80ba0-207">Example NuGetDefaults.Config and application</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
    <!-- defaultPushSource key works like the 'defaultPushSource' key of NuGet.Config files. -->
    <!-- This can be used by administrators to prevent accidental publishing of packages to nuget.org. -->
    <config>
        <add key="defaultPushSource" value="https://contoso.com/packages/" />
    </config>

    <!-- Default Package Sources; works like the 'packageSources' section of NuGet.Config files. -->
    <!-- This collection cannot be deleted or modified but can be disabled/enabled by users. -->
    <packageSources>
        <add key="Contoso Package Source" value="https://contoso.com/packages/" />
        <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />
    </packageSources>

    <!-- Default Package Sources that are disabled by default. -->
    <!-- Works like the 'disabledPackageSources' section of NuGet.Config files. -->
    <!-- Sources cannot be modified or deleted either but can be enabled/disabled by users. -->
    <disabledPackageSources>
        <add key="nuget.org" value="true" />
    </disabledPackageSources>
</configuration>
```
