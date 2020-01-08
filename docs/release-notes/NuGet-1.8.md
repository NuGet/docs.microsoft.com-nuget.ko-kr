---
title: NuGet 1.8 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 Ecrs를 비롯 한 NuGet 1.8에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 973a2d010cb75eeeb383be94baf2fb17a999dd7c
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383463"
---
# <a name="nuget-18-release-notes"></a><span data-ttu-id="76aa0-103">NuGet 1.8 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="76aa0-103">NuGet 1.8 Release Notes</span></span>

<span data-ttu-id="76aa0-104">Nuget [1.7 릴리스 정보](../release-notes/nuget-1.7.md) | [Nuget 2.0 릴리스 정보](../release-notes/nuget-2.0.md)</span><span class="sxs-lookup"><span data-stu-id="76aa0-104">[NuGet 1.7 Release Notes](../release-notes/nuget-1.7.md) | [NuGet 2.0 Release Notes](../release-notes/nuget-2.0.md)</span></span>

<span data-ttu-id="76aa0-105">NuGet 1.8은 2012 년 5 월 23 일에 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="76aa0-105">NuGet 1.8 was released on May 23, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="76aa0-106">알려진 설치 문제</span><span class="sxs-lookup"><span data-stu-id="76aa0-106">Known Installation Issue</span></span>
<span data-ttu-id="76aa0-107">VS 2010 s p 1을 실행 하는 경우 이전 버전을 설치한 경우 NuGet을 업그레이드 하려고 할 때 설치 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76aa0-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="76aa0-108">해결 방법은 NuGet을 제거한 후 VS 확장 갤러리에서 설치 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="76aa0-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="76aa0-109">자세한 내용은 <https://support.microsoft.com/kb/2581019>을 참조 하거나 [VS 핫픽스로 직접 이동](http://bit.ly/vsixcertfix)합니다.</span><span class="sxs-lookup"><span data-stu-id="76aa0-109">See <https://support.microsoft.com/kb/2581019> for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="76aa0-110">참고: Visual Studio에서 확장을 제거 하는 것을 허용 하지 않는 경우 (제거 단추를 사용할 수 없음) "관리자 권한으로 실행"을 사용 하 여 Visual Studio를 다시 시작 해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76aa0-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="nuget-18-incompatible-with-windows-xp-hotfix-published"></a><span data-ttu-id="76aa0-111">NuGet 1.8 Windows XP와 호환 되지 않음, 게시 된 핫픽스</span><span class="sxs-lookup"><span data-stu-id="76aa0-111">NuGet 1.8 Incompatible with Windows XP, hotfix published</span></span>

<span data-ttu-id="76aa0-112">NuGet 1.8이 출시 되 고 나면 1.8에서 Windows XP의 사용자를 중단 하는 암호화가 변경 되는 것을 알게 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="76aa0-112">Shortly after NuGet 1.8 was released, we learned that a cryptography change in 1.8 broke users on Windows XP.</span></span>

<span data-ttu-id="76aa0-113">이후이 문제를 해결 하는 핫픽스를 출시 했습니다.</span><span class="sxs-lookup"><span data-stu-id="76aa0-113">We have since released a hotfix that addresses this issue.</span></span>  <span data-ttu-id="76aa0-114">Visual Studio 확장 갤러리를 통해 NuGet을 업데이트 하면이 핫픽스를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76aa0-114">By updating NuGet through the Visual Studio Extension Gallery, you receive this hotfix.</span></span>

## <a name="features"></a><span data-ttu-id="76aa0-115">기능</span><span class="sxs-lookup"><span data-stu-id="76aa0-115">Features</span></span>

### <a name="satellite-packages-for-localized-resources"></a><span data-ttu-id="76aa0-116">지역화 된 리소스에 대 한 위성 패키지</span><span class="sxs-lookup"><span data-stu-id="76aa0-116">Satellite Packages for Localized Resources</span></span>
<span data-ttu-id="76aa0-117">이제 NuGet 1.8은 .NET Framework의 위성 어셈블리 기능과 비슷하게 지역화 된 리소스에 대 한 별도의 패키지를 만드는 기능을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="76aa0-117">NuGet 1.8 now supports the ability to create separate packages for localized resources, similar to the satellite assembly capabilities of the .NET Framework.</span></span>  <span data-ttu-id="76aa0-118">위성 패키지는 다음과 같은 몇 가지 규칙을 추가 하 여 다른 NuGet 패키지와 동일한 방식으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="76aa0-118">A satellite package is created in the same way as any other NuGet package with the addition of a few conventions:</span></span>

* <span data-ttu-id="76aa0-119">위성 패키지 ID 및 파일 이름에는 [.NET Framework에서 사용](https://docs.microsoft.com/openspecs/windows_protocols/ms-lcid/a9eac961-e77d-41a6-90a5-ce1a8b0cdb9c)하는 표준 문화권 문자열 중 하 나와 일치 하는 접미사가 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76aa0-119">The satellite package ID and file name should include a suffix that matches one of the standard [culture strings used by the .NET Framework](https://docs.microsoft.com/openspecs/windows_protocols/ms-lcid/a9eac961-e77d-41a6-90a5-ce1a8b0cdb9c).</span></span>
* <span data-ttu-id="76aa0-120">`.nuspec` 파일에서 위성 패키지는 ID에 사용 된 것과 동일한 문화권 문자열을 사용 하 여 언어 요소를 정의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76aa0-120">In its `.nuspec` file, the satellite package should define a language element with the same culture string used in the ID</span></span>
* <span data-ttu-id="76aa0-121">위성 패키지는 해당 `.nuspec` 파일의 종속성을 핵심 패키지에 정의 해야 합니다 .이는 단순히 동일한 ID를 가진 패키지는 언어 접미사를 뺀 것입니다.</span><span class="sxs-lookup"><span data-stu-id="76aa0-121">The satellite package should define a dependency in its `.nuspec` file to its core package, which is simply the package with the same ID minus the language suffix.</span></span>  <span data-ttu-id="76aa0-122">설치에 성공 하려면 저장소에서 핵심 패키지를 사용할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76aa0-122">The core package needs to be available in the repository for successful installation.</span></span>

<span data-ttu-id="76aa0-123">지역화 된 리소스를 사용 하 여 패키지를 설치 하기 위해 개발자는 리포지토리에서 지역화 된 패키지를 명시적으로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="76aa0-123">To install a package with localized resources, a developer explicitly selects the localized package from the repository.</span></span> <span data-ttu-id="76aa0-124">현재 NuGet 갤러리는 위성 패키지에 어떠한 종류의 특별 한 처리도 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="76aa0-124">At present, the NuGet gallery does not give any kind of special treatment to satellite packages.</span></span>

![지역화 된 pacakges가 있는 패키지 관리자 대화 상자](./media/dlg-w-loc-packs.png)

<span data-ttu-id="76aa0-126">위성 패키지에는 코어 패키지에 대 한 종속성이 나열 되므로 위성 패키지와 핵심 패키지는 모두 NuGet 패키지 폴더로 끌어오고 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76aa0-126">Because the satellite package lists a dependency to its core package, both the satellite and core packages are pulled into the NuGet packages folder and installed.</span></span>

![지역화 된 패키지가 있는 패키지 폴더](./media/fldr-loc-packs.png)

<span data-ttu-id="76aa0-128">또한 위성 패키지를 설치 하는 동안 NuGet은 문화권 문자열 명명 규칙도 인식 한 다음 .NET Framework에서 선택할 수 있도록 지역화 된 리소스 어셈블리를 핵심 패키지 내의 올바른 하위 폴더에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="76aa0-128">Additionally, while installing the satellite package, NuGet also recognizes the culture string naming convention and then copies the localized resource assembly into the correct subfolder within the core package so that it can be picked by the .NET Framework.</span></span>

![복사 된 리소스 폴더를 포함 하는 핵심 패키지 폴더](./media/fldr-copied-loc.png)

<span data-ttu-id="76aa0-130">위성 패키지를 사용 하는 기존 버그 하나는 NuGet에서 웹 사이트 프로젝트의 `bin` 폴더에 지역화 된 리소스를 복사 하지 않는다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="76aa0-130">One existing bug to note with satellite packages is that NuGet does not copy localized resources to the `bin` folder for Web site projects.</span></span>  <span data-ttu-id="76aa0-131">이 문제는 NuGet의 다음 릴리스에서 수정 될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="76aa0-131">This issue will be fixed in the next release of NuGet.</span></span>

<span data-ttu-id="76aa0-132">위성 패키지를 만들고 사용 하는 방법을 보여 주는 전체 샘플은 [https://github.com/NuGet/SatellitePackageSample](https://github.com/NuGet/SatellitePackageSample)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="76aa0-132">For a complete sample demonstrating how to create and use satellite packages, see [https://github.com/NuGet/SatellitePackageSample](https://github.com/NuGet/SatellitePackageSample).</span></span>

### <a name="package-restore-consent"></a><span data-ttu-id="76aa0-133">패키지 복원 동의</span><span class="sxs-lookup"><span data-stu-id="76aa0-133">Package Restore Consent</span></span>
<span data-ttu-id="76aa0-134">NuGet 1.8에서는 사용자 개인 정보를 보호 하기 위해 패키지 복원에 대 한 중요 한 제약 조건을 지원 하기 위한 토대를 제공 했습니다.</span><span class="sxs-lookup"><span data-stu-id="76aa0-134">In NuGet 1.8, we laid the groundwork for supporting an important constraint on package restore to protect user privacy.</span></span> <span data-ttu-id="76aa0-135">이 제약 조건을 사용 하려면 패키지 복원을 사용 하는 프로젝트와 솔루션을 빌드하는 개발자가 패키지 복원의 온라인에서 패키지를 다운로드 하 여 구성 된 패키지 원본에서 패키지를 다운로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76aa0-135">This constraint requires developers building projects and solutions that are using package restore to explicitly consent to package restore’s going online to download packages from configured package sources.</span></span>

<span data-ttu-id="76aa0-136">이러한 동의를 제공 하는 방법에는 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76aa0-136">There are 2 ways to provide this consent.</span></span> <span data-ttu-id="76aa0-137">첫 번째는 아래와 같이 패키지 관리자 구성 대화 상자에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76aa0-137">The first can be found in the package manager configuration dialog as shown below.</span></span>  <span data-ttu-id="76aa0-138">이 메서드는 주로 개발자 컴퓨터를 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="76aa0-138">This method is primarily intended for developer machines.</span></span>

![패키지 관리자 구성 대화 상자](./media/pr-consent-configdlg.png)

<span data-ttu-id="76aa0-140">두 번째 방법은 환경 변수 "EnableNuGetPackageRestore"를 값 "true"로 설정 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="76aa0-140">The second method is to set the environment variable “EnableNuGetPackageRestore” to the value “true”.</span></span>  <span data-ttu-id="76aa0-141">이 방법은 CI 또는 빌드 서버와 같은 무인 컴퓨터를 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="76aa0-141">This method is intended for unattended machines such as CI or build servers.</span></span>

<span data-ttu-id="76aa0-142">이제 위에서 설명한 대로 NuGet 1.8에서이 기능에 대 한 토대를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="76aa0-142">Now, as stated above, we have only laid the groundwork for this feature in NuGet 1.8.</span></span>  <span data-ttu-id="76aa0-143">즉,이 기능을 사용 하도록 설정 하는 모든 논리를 추가 했지만 현재이 버전에는 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="76aa0-143">Practically, this means that while we’ve added all of the logic to enable the feature, it's not currently enforced in this version.</span></span> <span data-ttu-id="76aa0-144">그러나 NuGet의 다음 릴리스에서는 사용 하도록 설정 되어 있으므로, 환경을 적절 하 게 구성할 수 있으므로 동의 제약 조건 적용을 시작할 때 영향을 받지 않도록 가능한 한 빨리이를 인식 하고자 합니다.</span><span class="sxs-lookup"><span data-stu-id="76aa0-144">It will be enabled, however, in the next release of NuGet, so we wanted to make you aware of it as soon as possible so that you can configure your environments appropriately and therefore not be impacted when we start enforce the consent constraint.</span></span>

<span data-ttu-id="76aa0-145">자세한 내용은이 기능에 대 한 [팀 블로그 게시물](http://blog.nuget.org/20120518/package-restore-and-consent.html) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="76aa0-145">For more details, please see the [team blog post](http://blog.nuget.org/20120518/package-restore-and-consent.html) on this feature.</span></span>

### <a name="nugetexe-performance-improvements"></a><span data-ttu-id="76aa0-146">nuget.exe 성능 향상</span><span class="sxs-lookup"><span data-stu-id="76aa0-146">nuget.exe Performance Improvements</span></span>
<span data-ttu-id="76aa0-147">설치 명령을 수정 하 여 동시에 패키지를 다운로드 하 고 설치 하면 NuGet 1.8은 nuget.exe 및 확장 패키지 복원을 통해 성능이 크게 향상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76aa0-147">By modifying the install command to download and install packages in parallel, NuGet 1.8 brings dramatic performance improvements to nuget.exe – and by extension package restore.</span></span>  <span data-ttu-id="76aa0-148">높은 수준의 테스트는 프로젝트에 6 개의 패키지를 설치 하는 성능이 NuGet 1.8에서 약 35%까지 향상 됨을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="76aa0-148">High level testing shows that performance for installing 6 packages into a project improves by about 35% in NuGet 1.8.</span></span>  <span data-ttu-id="76aa0-149">패키지 수를 25로 늘려도 약 60%의 성능 향상이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76aa0-149">Increasing the number of packages to 25 shows a performance gain of about 60%.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="76aa0-150">버그 수정</span><span class="sxs-lookup"><span data-stu-id="76aa0-150">Bug Fixes</span></span>
<span data-ttu-id="76aa0-151">NuGet 1.8에는 패키지 복원 동의 및 Windows 8 Express 통합과 관련 하 여 특히 패키지 관리자 콘솔과 패키지 복원 워크플로를 강조 하는 몇 가지 버그 수정이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76aa0-151">NuGet 1.8 includes quite a few bug fixes with an emphasis on the package manager console and package restore workflow, particularly as it relates to package restore consent and Windows 8 Express integration.</span></span>
<span data-ttu-id="76aa0-152">NuGet 1.8에서 수정 된 작업 항목의 전체 목록은 [이 릴리스에 대 한 Nuget 문제 추적기](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)를 확인 하세요.</span><span class="sxs-lookup"><span data-stu-id="76aa0-152">For a full list of work items fixed in NuGet 1.8, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
