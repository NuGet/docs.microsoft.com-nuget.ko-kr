---
title: NuGet 패키지 사용에 대한 개요 및 워크플로 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/22/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: 프로젝트에서 NuGet 패키지를 사용하는 프로세스를 간략히 설명하며, 프로세스의 다른 특정 부분에 대한 링크가 포함되어 있습니다.
keywords: NuGet 패키지 사용, NuGet 사용 개요, NuGet 사용 워크플로, 패키지 사용 워크플로, 패키지 사용 개요
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: e79b09fe8131f25c6bbed650e1927425dcc5d409
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="package-consumption-workflow"></a><span data-ttu-id="1772e-104">패키지 사용 워크플로</span><span class="sxs-lookup"><span data-stu-id="1772e-104">Package consumption workflow</span></span>

<span data-ttu-id="1772e-105">nuget.org와 조직에서 설정할 수 있는 개인 패키지 갤러리 사이에는 앱과 서비스에서 사용할 수 있는 매우 유용한 수만 개의 패키지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1772e-105">Between nuget.org and private package galleries that your organization might establish, you can find tens of thousands of highly useful packages to use in your apps and services.</span></span> <span data-ttu-id="1772e-106">그러나 소스와 관계없이 패키지를 사용하는 것은 아래와 같은 일반 워크플로를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="1772e-106">But regardless of the source, consuming a package follows the same general workflow.</span></span>

![패키지 원본으로 이동, 패키지 찾기, 프로젝트에 설치, using 문 및 패키지 API 호출 추가를 수행하는 흐름](media/Overview-01-GeneralFlow.png)

<span data-ttu-id="1772e-108">\*  _Visual Studio 및 dotnet.exe에만 해당합니다. nuget install 명령은 프로젝트 파일 또는 packages.config를 수정하지 않습니다. 이러한 항목은 수동으로 관리해야 합니다._</span><span class="sxs-lookup"><span data-stu-id="1772e-108">\* _Visual Studio and dotnet.ex\` only. The nuget install command does not modify project files or packages.config; entries must be managed manually._</span></span>

<span data-ttu-id="1772e-109">자세한 내용은 [패키지 찾기 및 선택](../consume-packages/finding-and-choosing-packages.md) 및 [NuGet 패키지를 설치하는 다양한 방법](ways-to-install-a-package.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1772e-109">For further details, see [Finding and Choosing Packages](../consume-packages/finding-and-choosing-packages.md) and [Different ways to install a NuGet package](ways-to-install-a-package.md).</span></span>

<span data-ttu-id="1772e-110">NuGet은 설치된 각 패키지의 ID와 버전 번호를 기억하여 프로젝트 형식과 NuGet 버전에 따라 [`packages.config`](../reference/packages-config.md) 또는 프로젝트 파일([PackageReference](../consume-packages/package-references-in-project-files.md) 사용)에 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="1772e-110">NuGet remembers the identity and version number of each installed package, recording it in either [`packages.config`](../reference/packages-config.md) or the project file (using [PackageReference](../consume-packages/package-references-in-project-files.md)), depending on project type and your version of NuGet.</span></span> <span data-ttu-id="1772e-111">NuGet 4.0 이상에서는 Visual Studio에서 [패키지 관리자 UI 옵션](../tools/package-manager-ui.md)을 통해 구성할 수는 있지만 PackageReference를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1772e-111">With NuGet 4.0+, PackageReference is preferred, although this is configurable in Visual Studio through the [Package Manager UI options](../tools/package-manager-ui.md).</span></span> <span data-ttu-id="1772e-112">어떤 경우이든 언제든지 적절한 파일을 확인하여 프로젝트에 대한 전체 종속성 목록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1772e-112">In any case, you can look in the appropriate file at any time to see the full list of dependencies for your project.</span></span>

> [!Tip]
> <span data-ttu-id="1772e-113">소프트웨어에서 사용하려는 각 패키지의 라이선스를 항상 확인하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1772e-113">It's prudent to always check the license for each package you intend to use in your software.</span></span> <span data-ttu-id="1772e-114">nuget.org에서는 각 패키지의 설명 페이지 오른쪽에 **라이선스 정보** 링크가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1772e-114">On nuget.org, you find a **License Info** link on the right side of each package's description page.</span></span> <span data-ttu-id="1772e-115">패키지에서 사용 조건을 지정하지 않은 경우 패키지 페이지의 **연락처 소유자** 링크를 사용하여 패키지 소유자에게 직접 문의해 보세요.</span><span class="sxs-lookup"><span data-stu-id="1772e-115">If a package does not specify license terms, contact the package owner directly using the **Contact owners** link on the package page.</span></span> <span data-ttu-id="1772e-116">Microsoft는 타사 패키지 공급자로부터 사용자에게 지적 재산권을 부여하지 않으며 타사에서 제공한 정보에 대해 책임을 지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1772e-116">Microsoft does not license any intellectual property to you from third party package providers and is not responsible for information provided by third parties.</span></span>

<span data-ttu-id="1772e-117">패키지를 설치할 때 NuGet은 일반적으로 해당 캐시에서 패키지를 이미 사용할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1772e-117">When installing packages, NuGet typically checks if the package is already available from its cache.</span></span> <span data-ttu-id="1772e-118">[Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md)(전역 패키지 및 캐시 폴더 관리)에서 설명한 대로 명령줄에서 이 캐시를 수동으로 지울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1772e-118">You can manually clear this cache from the command line, as described on [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

<span data-ttu-id="1772e-119">또한 NuGet은 패키지에서 지원하는 대상 프레임워크가 프로젝트와 호환되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1772e-119">NuGet also makes sure that the target frameworks supported by the package are compatible with your project.</span></span> <span data-ttu-id="1772e-120">패키지에 호환되는 어셈블리가 없으면 NuGet에서 오류를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="1772e-120">If the package does not contain compatible assemblies, NuGet displays an error.</span></span> <span data-ttu-id="1772e-121">[호환되지 않는 패키지 오류 해결](dependency-resolution.md#resolving-incompatible-package-errors)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1772e-121">See [Resolving incompatible package errors](dependency-resolution.md#resolving-incompatible-package-errors).</span></span>

<span data-ttu-id="1772e-122">원본 리포지토리에 프로젝트 코드를 추가할 때는 일반적으로 NuGet 패키지가 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1772e-122">When adding project code to a source repository, you typically don't include NuGet packages.</span></span> <span data-ttu-id="1772e-123">나중에 리포지토리를 복제하거나 Visual Studio Team Services와 같은 시스템의 빌드 에이전트를 포함하여 프로젝트를 가져오는 사용자는 빌드를 실행하기 전에 필요한 패키지를 복원해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1772e-123">Those who later clone the repository or otherwise acquire the project, including build agents on systems like Visual Studio Team Services, must restore the necessary packages prior to running a build:</span></span>

![리포지토리를 복제하고 restore 명령 중 하나를 사용하여 NuGet 패키지를 복원하는 흐름](media/Overview-02-RestoreFlow.png)

<span data-ttu-id="1772e-125">[패키지 복원](../consume-packages/package-restore.md)은 프로젝트 파일 또는 `packages.config`의 정보를 사용하여 모든 종속성을 다시 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="1772e-125">[Package Restore](../consume-packages/package-restore.md) uses the information in the project file or `packages.config` to reinstall all dependencies.</span></span> <span data-ttu-id="1772e-126">[종속성 확인](../consume-packages/dependency-resolution.md)에서 설명한 대로 관련된 프로세스에는 차이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1772e-126">Note that there are differences in the process involved, as described in [Dependency Resolution](../consume-packages/dependency-resolution.md).</span></span> <span data-ttu-id="1772e-127">또한 위의 다이어그램에는 패키지 관리자 콘솔의 복원 명령은 표시되어 있지 않습니다. 이는 이미 Visual Studio 컨텍스트에 있는 콘솔을 사용 중이기 때문이며, 이 콘솔에서는 일반적으로 패키지를 자동으로 복원하고 표시된 솔루션 수준 명령을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1772e-127">Also, the diagram above does not show a restore command for the Package Manager Console because you're with the Console you're already in the context of Visual Studio, which typically restores packages automatically and provides the solution-level command as shown.</span></span>

<span data-ttu-id="1772e-128">때로는 이미 프로젝트에 포함되어 있는 패키지를 다시 설치해야 하며, 종속성을 다시 설치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1772e-128">Occasionally it's necessary to reinstall packages that are already included in a project, which may also reinstall dependencies.</span></span> <span data-ttu-id="1772e-129">이 작업은 `nuget reinstall` 명령이나 NuGet 패키지 관리자 콘솔을 사용하여 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1772e-129">This is easy to do using the `nuget reinstall` command or the NuGet Package Manager Console.</span></span> <span data-ttu-id="1772e-130">자세한 내용은 [패키지 다시 설치 및 업데이트](../consume-packages/reinstalling-and-updating-packages.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1772e-130">For details, see [Reinstalling and Updating Packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span>

<span data-ttu-id="1772e-131">마지막으로 NuGet의 동작은 `Nuget.Config` 파일로 구동됩니다.</span><span class="sxs-lookup"><span data-stu-id="1772e-131">Finally, NuGet's behavior is driven by `Nuget.Config` files.</span></span> <span data-ttu-id="1772e-132">[NuGet 동작 구성](../consume-packages/configuring-nuget-behavior.md)에서 설명한 대로 여러 파일을 사용하여 서로 다른 수준의 특정 설정을 중앙 집중화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1772e-132">Multiple files can be used to centralize certain settings at different levels, as explained in [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="1772e-133">NuGet 패키지를 사용하여 효율적인 코딩을 즐겨보세요!</span><span class="sxs-lookup"><span data-stu-id="1772e-133">Enjoy your productive coding with NuGet packages!</span></span>
