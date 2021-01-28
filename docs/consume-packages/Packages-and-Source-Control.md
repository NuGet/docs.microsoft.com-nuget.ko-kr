---
title: NuGet 패키지 및 원본 제어
description: 버전 제어와 소스 제어 시스템 내에서 NuGet 패키지를 처리하는 방법 및 Git과 TFVC를 사용하여 패키지를 생략하는 방법에 대한 고려 사항입니다.
author: JonDouglas
ms.author: jodou
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 9bae65573ca49c68d07250228c1923890e0f14ac
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775009"
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a><span data-ttu-id="81bcc-103">소스 제어 시스템에서 NuGet 패키지 생략</span><span class="sxs-lookup"><span data-stu-id="81bcc-103">Omitting NuGet packages in source control systems</span></span>

<span data-ttu-id="81bcc-104">일반적으로 개발자는 해당 소스 제어 리포지토리에서 NuGet 패키지를 생략하고 대신 [패키지 복원](package-restore.md)을 사용하여 빌드 전에 프로젝트의 종속성을 다시 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="81bcc-104">Developers typically omit NuGet packages from their source control repositories and rely instead on [package restore](package-restore.md) to reinstall a project's dependencies before a build.</span></span>

<span data-ttu-id="81bcc-105">패키지 복원을 사용하는 이유는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="81bcc-105">The reasons for relying on package restore include the following:</span></span>

1. <span data-ttu-id="81bcc-106">Git과 같은 분산 버전 제어 시스템은 리포지토리 내에서 모든 버전의 모든 파일의 전체 복사본을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="81bcc-106">Distributed version control systems, such as Git, include full copies of every version of every file within the repository.</span></span> <span data-ttu-id="81bcc-107">이진 파일이 자주 업데이트되면 리포지토리를 복제하는 데 상당한 블로트가 발생하고 걸리는 시간이 길어집니다.</span><span class="sxs-lookup"><span data-stu-id="81bcc-107">Binary files that are frequently updated lead to significant bloat and lengthens the time it takes to clone the repository.</span></span>
1. <span data-ttu-id="81bcc-108">패키지가 리포지토리에 포함될 때 개발자는 NuGet을 통해 패키지를 참조하지 않고 디스크에서 직접 패키지 내용에 대한 참조를 추가할 수 있습니다. 그러면 프로젝트에서 하드 코딩된 경로 이름으로 이어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81bcc-108">When packages are included in the repository, developers are liable to add references directly to package contents on disk rather than referencing packages through NuGet, which can lead to hard-coded path names in the project.</span></span>
1. <span data-ttu-id="81bcc-109">사용 중인 모든 패키지 폴더를 삭제하지 않았는지 확인해야 하는 경우 사용하지 않는 패키지 폴더의 솔루션을 정리하기가 더 어려워집니다.</span><span class="sxs-lookup"><span data-stu-id="81bcc-109">It becomes harder to clean your solution of any unused package folders, as you need to ensure you don't delete any package folders still in use.</span></span>
1. <span data-ttu-id="81bcc-110">패키지를 생략하여 코드와 종속된 다른 사용자의 패키지 간에 소유권 경계를 명확하게 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="81bcc-110">By omitting packages, you maintain clean boundaries of ownership between your code and the packages from others that you depend upon.</span></span> <span data-ttu-id="81bcc-111">많은 NuGet 패키지는 고유한 소스 제어 리포지토리에서 유지되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81bcc-111">Many NuGet packages are maintained in their own source control repositories already.</span></span>

<span data-ttu-id="81bcc-112">이 문서에 설명된 대로 패키지 복원이 NuGet의 기본 동작이지만 수작업으로 패키지(소스 제어의 프로젝트에 있는 `packages` 폴더)를 생략해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81bcc-112">Although package restore is the default behavior with NuGet, some manual work is necessary to omit packages&mdash;namely, the `packages` folder in your project&mdash;from source control, as described in this article.</span></span>

## <a name="omitting-packages-with-git"></a><span data-ttu-id="81bcc-113">Git를 사용하여 패키지 생략</span><span class="sxs-lookup"><span data-stu-id="81bcc-113">Omitting packages with Git</span></span>

<span data-ttu-id="81bcc-114">[.gitignore 파일](https://git-scm.com/docs/gitignore)을 사용하여 NuGet 패키지(`.nupkg`), `packages` 폴더 및 `project.assets.json`을 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="81bcc-114">Use the [.gitignore file](https://git-scm.com/docs/gitignore) to ignore NuGet packages (`.nupkg`) the `packages` folder, and `project.assets.json`, among other things.</span></span> <span data-ttu-id="81bcc-115">참조는 [Visual Studio 프로젝트에 대한 샘플 `.gitignore`](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81bcc-115">For reference, see the [sample `.gitignore` for Visual Studio projects](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore):</span></span>

<span data-ttu-id="81bcc-116">`.gitignore` 파일의 중요한 부분은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="81bcc-116">The important parts of the `.gitignore` file are:</span></span>

```gitignore
# Ignore NuGet Packages
*.nupkg

# The packages folder can be ignored because of Package Restore
**/[Pp]ackages/*

# except build/, which is used as an MSBuild target.
!**/[Pp]ackages/build/

# Uncomment if necessary however generally it will be regenerated when needed
#!**/[Pp]ackages/repositories.config

# NuGet v3's project.json files produces more ignorable files
*.nuget.props
*.nuget.targets

# Ignore other intermediate files that NuGet might create. project.lock.json is used in conjunction
# with project.json (NuGet v3); project.assets.json is used in conjunction with the PackageReference
# format (NuGet v4 and .NET Core).
project.lock.json
project.assets.json
```

## <a name="omitting-packages-with-team-foundation-version-control"></a><span data-ttu-id="81bcc-117">Team Foundation 버전 제어를 사용하여 패키지 생략</span><span class="sxs-lookup"><span data-stu-id="81bcc-117">Omitting packages with Team Foundation Version Control</span></span>

> [!Note]
> <span data-ttu-id="81bcc-118">가능한 경우 프로젝트를 소스 제어에 추가하기 *전에* 이러한 지침에 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="81bcc-118">Follow these instructions if possible *before* adding your project to source control.</span></span> <span data-ttu-id="81bcc-119">그렇지 않으면 리포지토리에서 `packages` 폴더를 수동으로 삭제하고 계속하기 전에 해당 변경 내용을 체크 인합니다.</span><span class="sxs-lookup"><span data-stu-id="81bcc-119">Otherwise, manually delete the `packages` folder from your repository and check in that change before continuing.</span></span>

<span data-ttu-id="81bcc-120">선택한 파일에서 TFVC를 사용하여 소스 제어 통합을 사용하지 않으려면:</span><span class="sxs-lookup"><span data-stu-id="81bcc-120">To disable source control integration with TFVC for selected files:</span></span>

1. <span data-ttu-id="81bcc-121">(`.sln` 파일이 있는)솔루션 폴더에서 `.nuget`라는 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="81bcc-121">Create a folder called `.nuget` in your solution folder (where the `.sln` file is).</span></span>
    - <span data-ttu-id="81bcc-122">팁: Windows의 Windows 탐색기에서 이 폴더를 만들려면 후행 점을 ‘포함한’ `.nuget.`이라는 이름을 사용합니다. </span><span class="sxs-lookup"><span data-stu-id="81bcc-122">Tip: on Windows, to create this folder in Windows Explorer, use the name `.nuget.` *with* the trailing dot.</span></span>

1. <span data-ttu-id="81bcc-123">해당 폴더에서 `NuGet.Config`라는 파일을 만들고 편집하기 위해 엽니다.</span><span class="sxs-lookup"><span data-stu-id="81bcc-123">In that folder, create a file named `NuGet.Config` and open it for editing.</span></span>

1. <span data-ttu-id="81bcc-124">최소한 다음 텍스트를 추가합니다. 여기서 [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) 설정을 통해 Visual Studio에서 `packages` 폴더에 있는 모든 항목을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="81bcc-124">Add the following text as a minimum, where the [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) setting instructs Visual Studio to skip everything in the `packages` folder:</span></span>

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
       <solution>
           <add key="disableSourceControlIntegration" value="true" />
       </solution>
   </configuration>
   ```

1. <span data-ttu-id="81bcc-125">TFS 2010 이전 버전을 사용하는 경우 매핑 작업 영역에서 `packages` 폴더를 숨깁니다.</span><span class="sxs-lookup"><span data-stu-id="81bcc-125">If you are using TFS 2010 or earlier, cloak the `packages` folder in your workspace mappings.</span></span>

1. <span data-ttu-id="81bcc-126">[서버에 파일 추가](/vsts/tfvc/add-files-server?view=vsts#tfignore)에 설명된 대로 TFS 2012 이상 또는 Visual Studio Team Services를 사용하여 `.tfignore` 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="81bcc-126">On TFS 2012 or later, or with Visual Studio Team Services, create a `.tfignore` file as described on [Add Files to the Server](/vsts/tfvc/add-files-server?view=vsts#tfignore).</span></span> <span data-ttu-id="81bcc-127">해당 파일에서 리포지토리 수준의 `\packages` 폴더 및 다른 몇 가지 중간 파일에 대한 수정을 명시적으로 무시하려면 아래 내용을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="81bcc-127">In that file, include the content below to explicitly ignore modifications to the `\packages` folder on the repository level and a few other intermediate files.</span></span> <span data-ttu-id="81bcc-128">(후행 점이 있는 `.tfignore.`라는 이름을 사용하여 Windows 탐색기에서 파일을 만들 수 있지만 먼저 "알려진 파일 확장명 숨기기" 옵션을 비활성화해야 합니다.)</span><span class="sxs-lookup"><span data-stu-id="81bcc-128">(You can create the file in Windows Explorer using the name a `.tfignore.` with the trailing dot, but you might need to disable the "Hide known file extensions" option first.):</span></span>

   ```cli
   # Ignore NuGet Packages
   *.nupkg

   # Ignore the NuGet packages folder in the root of the repository. If needed, prefix 'packages'
   # with additional folder names if it's not in the same folder as .tfignore.   
   packages

   # Omit temporary files
   project.lock.json
   project.assets.json
   *.nuget.props
   ```

1. <span data-ttu-id="81bcc-129">`NuGet.Config` 및 `.tfignore`를 소스 제어에 추가하여 변경 내용을 체크 인합니다.</span><span class="sxs-lookup"><span data-stu-id="81bcc-129">Add `NuGet.Config` and `.tfignore` to source control and check in your changes.</span></span>
