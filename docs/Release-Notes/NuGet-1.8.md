---
title: NuGet 1.8 릴리스 정보
description: 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr를 포함 하 여 NuGet 1.8에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 1801d62b786717c088429fbeca6f1f72f5ab6b4f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-18-release-notes"></a><span data-ttu-id="584b0-103">NuGet 1.8 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="584b0-103">NuGet 1.8 Release Notes</span></span>

<span data-ttu-id="584b0-104">[NuGet 1.7 릴리스 정보](../release-notes/nuget-1.7.md) | [NuGet 2.0 릴리스 정보](../release-notes/nuget-2.0.md)</span><span class="sxs-lookup"><span data-stu-id="584b0-104">[NuGet 1.7 Release Notes](../release-notes/nuget-1.7.md) | [NuGet 2.0 Release Notes](../release-notes/nuget-2.0.md)</span></span>

<span data-ttu-id="584b0-105">NuGet 1.8은 2012 년 5 월 23 일에 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="584b0-105">NuGet 1.8 was released on May 23, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="584b0-106">알려진된 설치 문제</span><span class="sxs-lookup"><span data-stu-id="584b0-106">Known Installation Issue</span></span>
<span data-ttu-id="584b0-107">VS 2010 s p 1을 실행 하는 경우 이전 버전이 설치 되어 있는 경우 NuGet을 업그레이드 하는 동안 설치 오류에 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="584b0-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="584b0-108">해결 하려면 NuGet 제거한 다음 VS 확장 갤러리에서 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="584b0-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="584b0-109">참조 [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) 자세한 내용은 또는 [VS 핫픽스로 직접 이동](http://bit.ly/vsixcertfix)합니다.</span><span class="sxs-lookup"><span data-stu-id="584b0-109">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="584b0-110">참고: Visual Studio 확장 (제거 단추 사용 안 함)을 제거 하도록 허용 하지, 한 후 가능성 하면 "관리자 권한으로 실행"을 사용 하 여 Visual Studio를 다시 시작</span><span class="sxs-lookup"><span data-stu-id="584b0-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="nuget-18-incompatible-with-windows-xp-hotfix-published"></a><span data-ttu-id="584b0-111">Windows XP와 NuGet 1.8 호환 되지 않는 게시 하는 핫픽스</span><span class="sxs-lookup"><span data-stu-id="584b0-111">NuGet 1.8 Incompatible with Windows XP, hotfix published</span></span>

<span data-ttu-id="584b0-112">NuGet 1.8이 출시 된 후에 바로 이전에 배운 것 암호화 변경 1.8에 Windows XP에서 사용자를 중단 합니다.</span><span class="sxs-lookup"><span data-stu-id="584b0-112">Shortly after NuGet 1.8 was released, we learned that a cryptography change in 1.8 broke users on Windows XP.</span></span>

<span data-ttu-id="584b0-113">이 문제를 해결 하는 핫픽스를 릴리스 이후로 했습니다.</span><span class="sxs-lookup"><span data-stu-id="584b0-113">We have since released a hotfix that addresses this issue.</span></span>  <span data-ttu-id="584b0-114">NuGet을 통해 Visual Studio 확장 갤러리를 업데이트 하 여이 핫픽스를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="584b0-114">By updating NuGet through the Visual Studio Extension Gallery, you receive this hotfix.</span></span>

## <a name="features"></a><span data-ttu-id="584b0-115">기능</span><span class="sxs-lookup"><span data-stu-id="584b0-115">Features</span></span>

### <a name="satellite-packages-for-localized-resources"></a><span data-ttu-id="584b0-116">지역화 된 리소스에 대 한 위성 패키지</span><span class="sxs-lookup"><span data-stu-id="584b0-116">Satellite Packages for Localized Resources</span></span>
<span data-ttu-id="584b0-117">NuGet 1.8는 이제.NET Framework의 위성 어셈블리 기능와 유사한 지역화 된 리소스에 대 한 별도 패키지를 만들 수 있는 기능을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="584b0-117">NuGet 1.8 now supports the ability to create separate packages for localized resources, similar to the satellite assembly capabilities of the .NET Framework.</span></span>  <span data-ttu-id="584b0-118">위성 패키지는 동일한 방식으로 몇 가지 규칙을 추가 하 여 다른 NuGet 패키지에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="584b0-118">A satellite package is created in the same way as any other NuGet package with the addition of a few conventions:</span></span>

* <span data-ttu-id="584b0-119">위성 패키지 ID와 파일 이름에는 표준 중 하 나와 일치 하는 접미사 포함 되어 있어야 [.NET Framework에서 사용 되는 문자열을 문화권](http://msdn.microsoft.com/goglobal/bb896001.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="584b0-119">The satellite package ID and file name should include a suffix that matches one of the standard [culture strings used by the .NET Framework](http://msdn.microsoft.com/goglobal/bb896001.aspx).</span></span>
* <span data-ttu-id="584b0-120">에 해당 `.nuspec` 파일을 위성 패키지 ID에 사용할 동일한 문화권 문자열로 언어 요소를 정의 해야</span><span class="sxs-lookup"><span data-stu-id="584b0-120">In its `.nuspec` file, the satellite package should define a language element with the same culture string used in the ID</span></span>
* <span data-ttu-id="584b0-121">위성 패키지의 종속성을 정의 해야 해당 `.nuspec` 단순히 언어 접미사 뺀 동일한 ID 사용 하 여 패키지의 코어 패키지에는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="584b0-121">The satellite package should define a dependency in its `.nuspec` file to its core package, which is simply the package with the same ID minus the language suffix.</span></span>  <span data-ttu-id="584b0-122">코어 패키지 성공적인 설치에 대 한 저장소에 사용할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="584b0-122">The core package needs to be available in the repository for successful installation.</span></span>

<span data-ttu-id="584b0-123">지역화 된 리소스가 포함 된 패키지를 설치 하려면 개발자 저장소에서 지역화 된 패키지 명시적으로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="584b0-123">To install a package with localized resources, a developer explicitly selects the localized package from the repository.</span></span> <span data-ttu-id="584b0-124">현재, NuGet 갤러리는 모든 종류의 위성 패키지에 특별 한 처리를 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="584b0-124">At present, the NuGet gallery does not give any kind of special treatment to satellite packages.</span></span>

![지역화 된 pacakges와 패키지 관리자 대화 상자](./media/dlg-w-loc-packs.png)

<span data-ttu-id="584b0-126">위성 패키지의 코어 패키지에 대 한 종속성 나열, 위성와 코어 패키지 된 NuGet 패키지 폴더에 포함 되며 설치.</span><span class="sxs-lookup"><span data-stu-id="584b0-126">Because the satellite package lists a dependency to its core package, both the satellite and core packages are pulled into the NuGet packages folder and installed.</span></span>

![지역화 된 패키지와 패키지 폴더](./media/fldr-loc-packs.png)

<span data-ttu-id="584b0-128">또한 위성 패키지를 설치 하는 동안 NuGet도 문화권 문자열 명명 규칙을 인식 및 지역화 된 리소스 어셈블리는.NET Framework에서 선택할 수 있도록에 코어 패키지 내에서 올바른 하위 폴더에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="584b0-128">Additionally, while installing the satellite package, NuGet also recognizes the culture string naming convention and then copies the localized resource assembly into the correct subfolder within the core package so that it can be picked by the .NET Framework.</span></span>

![복사한 리소스 폴더와 코어 패키지 폴더](./media/fldr-copied-loc.png)

<span data-ttu-id="584b0-130">위성 패키지와를 하나의 기존 버그는 NuGet을 지역화 된 리소스를 복사 하지 않습니다는 `bin` 웹 사이트 프로젝트에 대 한 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="584b0-130">One existing bug to note with satellite packages is that NuGet does not copy localized resources to the `bin` folder for Web site projects.</span></span>  <span data-ttu-id="584b0-131">이 문제는 NuGet의 다음 릴리스에서 수정 될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="584b0-131">This issue will be fixed in the next release of NuGet.</span></span>

<span data-ttu-id="584b0-132">만들고 위성 패키지를 사용 하는 방법을 보여 주는 전체 샘플을 참조 하십시오. [ https://github.com/NuGet/SatellitePackageSample ](https://github.com/NuGet/SatellitePackageSample)합니다.</span><span class="sxs-lookup"><span data-stu-id="584b0-132">For a complete sample demonstrating how to create and use satellite packages, see [https://github.com/NuGet/SatellitePackageSample](https://github.com/NuGet/SatellitePackageSample).</span></span>

### <a name="package-restore-consent"></a><span data-ttu-id="584b0-133">패키지 복원 동의</span><span class="sxs-lookup"><span data-stu-id="584b0-133">Package Restore Consent</span></span>
<span data-ttu-id="584b0-134">NuGet 1.8에서 म 토대가 패키지 복원 사용자의 개인 정보 보호에 대 한 중요 한 제약 조건을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="584b0-134">In NuGet 1.8, we laid the groundwork for supporting an important constraint on package restore to protect user privacy.</span></span> <span data-ttu-id="584b0-135">이 제약 조건에서는 프로젝트 및 패키지를 복원 패키지 복원에 명시적으로 동의를 사용 하 여 솔루션을 빌드하는 개발자의 구성 된 패키지 소스에서 패키지를 다운로드 하려면 온라인으로 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="584b0-135">This constraint requires developers building projects and solutions that are using package restore to explicitly consent to package restore’s going online to download packages from configured package sources.</span></span>

<span data-ttu-id="584b0-136">두 가지 방법으로이 동의 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="584b0-136">There are 2 ways to provide this consent.</span></span> <span data-ttu-id="584b0-137">패키지 관리자 구성 대화 상자에서 아래와 같이 첫 번째를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="584b0-137">The first can be found in the package manager configuration dialog as shown below.</span></span>  <span data-ttu-id="584b0-138">이 메서드는 개발자 컴퓨터에 대 한 주로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="584b0-138">This method is primarily intended for developer machines.</span></span>

![패키지 관리자 구성 대화 상자](./media/pr-consent-configdlg.png)

<span data-ttu-id="584b0-140">두 번째 방법은 환경을 변수 "EnableNuGetPackageRestore" 값 "true 로" 설정 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="584b0-140">The second method is to set the environment variable “EnableNuGetPackageRestore” to the value “true”.</span></span>  <span data-ttu-id="584b0-141">이 메서드를 사용 하 여 CI 또는 빌드 서버와 같이 무인된 컴퓨터에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="584b0-141">This method is intended for unattended machines such as CI or build servers.</span></span>

<span data-ttu-id="584b0-142">이제 위에서 설명한 대로 우리는 토대가이 기능에 대 한 NuGet 1.8에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="584b0-142">Now, as stated above, we have only laid the groundwork for this feature in NuGet 1.8.</span></span>  <span data-ttu-id="584b0-143">실제로,이 모든 기능을 사용 하려면 논리를 추가 했습니다 하는 동안 현재는 아님 적용이 버전에서 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="584b0-143">Practically, this means that while we’ve added all of the logic to enable the feature, it's not currently enforced in this version.</span></span> <span data-ttu-id="584b0-144">그러나 사용할 수 있게, 동의 제약 조건을 적용 버전의 NuGet 이해 하 고 가능한 한 빨리 따라서 영향을 받지 시작할 때 및 사용자 환경을 적절 하 게 구성할 수 있도록 주고자 하므로 다음에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="584b0-144">It will be enabled, however, in the next release of NuGet, so we wanted to make you aware of it as soon as possible so that you can configure your environments appropriately and therefore not be impacted when we start enforce the consent constraint.</span></span>

<span data-ttu-id="584b0-145">자세한 내용은 참조 하십시오는 [팀 블로그 게시물](http://blog.nuget.org/20120518/package-restore-and-consent.html) 이 기능에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="584b0-145">For more details, please see the [team blog post](http://blog.nuget.org/20120518/package-restore-and-consent.html) on this feature.</span></span>

### <a name="nugetexe-performance-improvements"></a><span data-ttu-id="584b0-146">nuget.exe 성능 향상</span><span class="sxs-lookup"><span data-stu-id="584b0-146">nuget.exe Performance Improvements</span></span>
<span data-ttu-id="584b0-147">다운로드 하 고 동시에 패키지를 설치 하려면 설치 명령줄을 수정 하 여 NuGet 1.8 nuget.exe – 및 확장 패키지를 복원 하 여 성능을 크게 향상을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="584b0-147">By modifying the install command to download and install packages in parallel, NuGet 1.8 brings dramatic performance improvements to nuget.exe – and by extension package restore.</span></span>  <span data-ttu-id="584b0-148">높은 수준의 테스트 NuGet 1.8에서 35 %6 패키지를 프로젝트에 설치를 위한 성능 향상을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="584b0-148">High level testing shows that performance for installing 6 packages into a project improves by about 35% in NuGet 1.8.</span></span>  <span data-ttu-id="584b0-149">25로 패키지 수를 늘리면 약 60%의 성능 향상을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="584b0-149">Increasing the number of packages to 25 shows a performance gain of about 60%.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="584b0-150">버그 수정</span><span class="sxs-lookup"><span data-stu-id="584b0-150">Bug Fixes</span></span>
<span data-ttu-id="584b0-151">1.8 NuGet 패키지 복원 동 및 Windows 8 Express 통합 관련이 있기 때문에 특히 패키지 관리자 콘솔 및 패키지 복원 워크플로에 중점을 두어 많은 버그 수정 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="584b0-151">NuGet 1.8 includes quite a few bug fixes with an emphasis on the package manager console and package restore workflow, particularly as it relates to package restore consent and Windows 8 Express integration.</span></span>
<span data-ttu-id="584b0-152">작업의 전체 목록은 항목 고정 NuGet 1.8에서 하십시오 보기는 [이 릴리스에 대 한 NuGet 문제 추적기](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)합니다.</span><span class="sxs-lookup"><span data-stu-id="584b0-152">For a full list of work items fixed in NuGet 1.8, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
