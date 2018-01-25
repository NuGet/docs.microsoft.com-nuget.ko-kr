---
title: "NuGet 3.5 베타 릴리스 정보 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr를 포함 하 여 NuGet 3.5에 대 한 릴리스 정보입니다."
keywords: "NuGet 3.5 릴리스 정보, 버그 수정, 알려진 문제, 추가 기능을 Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ee78ceb2ff032c05c0f8ef9a6623b94cc56ee0a9
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-35-release-notes"></a><span data-ttu-id="12e4e-104">NuGet 3.5 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="12e4e-104">NuGet 3.5 Release Notes</span></span>

<span data-ttu-id="12e4e-105">[NuGet 3.5 RC 릴리스 정보](../release-notes/nuget-3.5-RC.md) | [NuGet 4.0 RC 릴리스 정보](../release-notes/nuget-4.0-RC.md)</span><span class="sxs-lookup"><span data-stu-id="12e4e-105">[NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md) | [NuGet 4.0 RC Release Notes](../release-notes/nuget-4.0-RC.md)</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="12e4e-106">버그 수정</span><span class="sxs-lookup"><span data-stu-id="12e4e-106">Bug Fixes</span></span>

* <span data-ttu-id="12e4e-107">팩 모노-에 MSBuild 14.1를 사용 하지 않는 [#3550](https://github.com/NuGet/Home/issues/3550)</span><span class="sxs-lookup"><span data-stu-id="12e4e-107">Pack doesn't use MSBuild 14.1 on mono - [#3550](https://github.com/NuGet/Home/issues/3550)</span></span>

* <span data-ttu-id="12e4e-108">업데이트 탭 선택 현재 설치 된 버전-대신 업데이트할 사용 가능한 최신 버전을 선택 하지 않습니다 [#3498](https://github.com/NuGet/Home/issues/3498)</span><span class="sxs-lookup"><span data-stu-id="12e4e-108">Update tab doesn't select the latest available version to update instead select current installed version - [#3498](https://github.com/NuGet/Home/issues/3498)</span></span>

* <span data-ttu-id="12e4e-109">MyGet 피드에 개인 v2를 인증 하 고 "더 많은 결과 x 표시"를 클릭 한 후 충돌 해결- [#3469](https://github.com/NuGet/Home/issues/3469)</span><span class="sxs-lookup"><span data-stu-id="12e4e-109">Fix Crash after authenticating a private v2 MyGet feed and clicking "Show x more results" - [#3469](https://github.com/NuGet/Home/issues/3469)</span></span>

* <span data-ttu-id="12e4e-110">로그 메시지 UI에 대 한 반대 순서로 것 같습니다 [#3446](https://github.com/NuGet/Home/issues/3446)</span><span class="sxs-lookup"><span data-stu-id="12e4e-110">Log messages seem to be in reverse order for UI - [#3446](https://github.com/NuGet/Home/issues/3446)</span></span>

* <span data-ttu-id="12e4e-111">"지정한 경로 형식은 지원 되지 않습니다"-v3.4.4-Nuget 복원 throw [#3442](https://github.com/NuGet/Home/issues/3442)</span><span class="sxs-lookup"><span data-stu-id="12e4e-111">v3.4.4 - Nuget restore throws "The given path's format is not supported" - [#3442](https://github.com/NuGet/Home/issues/3442)</span></span>

* <span data-ttu-id="12e4e-112">NuGet cmdLine 3.6 베타 기준으로 하지 않는-Prop 구성 릴리스-= [#3432](https://github.com/NuGet/Home/issues/3432)</span><span class="sxs-lookup"><span data-stu-id="12e4e-112">NuGet cmdLine 3.6 beta does not honor -Prop Configuration = Release - [#3432](https://github.com/NuGet/Home/issues/3432)</span></span>

* <span data-ttu-id="12e4e-113">-대규모 프로젝트에 Nuget IKVM 느린 설치 [#3428](https://github.com/NuGet/Home/issues/3428)</span><span class="sxs-lookup"><span data-stu-id="12e4e-113">Nuget IKVM slow install on large project - [#3428](https://github.com/NuGet/Home/issues/3428)</span></span>

* <span data-ttu-id="12e4e-114">nuget.exe 셀프 유지에 업데이트 자체-업데이트 [#3395](https://github.com/NuGet/Home/issues/3395)</span><span class="sxs-lookup"><span data-stu-id="12e4e-114">nuget.exe Update -Self keeps on updating itself - [#3395](https://github.com/NuGet/Home/issues/3395)</span></span>

* <span data-ttu-id="12e4e-115">UNC 공유에서 3.5 설치/복원에 3.4.4-에서 회귀 성능 [#3355](https://github.com/NuGet/Home/issues/3355)</span><span class="sxs-lookup"><span data-stu-id="12e4e-115">3.5 install/restore from UNC share has performance Regression from 3.4.4 - [#3355](https://github.com/NuGet/Home/issues/3355)</span></span>

* <span data-ttu-id="12e4e-116">Moq net451 프로젝트-에 대 한 패키지 관리 UI에서에서 설치 하는 동안 오류가 발생 했습니다. [#3349](https://github.com/NuGet/Home/issues/3349)</span><span class="sxs-lookup"><span data-stu-id="12e4e-116">Error when installing Moq from the Package management UI for a net451 project - [#3349](https://github.com/NuGet/Home/issues/3349)</span></span>

* <span data-ttu-id="12e4e-117">솔루션 수준에서 설치 탭은 패키지의 버전-표시 되지 않습니다 [#3339](https://github.com/NuGet/Home/issues/3339)</span><span class="sxs-lookup"><span data-stu-id="12e4e-117">Install tab at solution level doesn't show package's version - [#3339](https://github.com/NuGet/Home/issues/3339)</span></span>

* <span data-ttu-id="12e4e-118">xproj `project.json` 설치 됨 탭에서 업데이트 상태-손실 [#3303](https://github.com/NuGet/Home/issues/3303)</span><span class="sxs-lookup"><span data-stu-id="12e4e-118">xproj `project.json` update from Installed tab loses state - [#3303](https://github.com/NuGet/Home/issues/3303)</span></span>

* <span data-ttu-id="12e4e-119">에 NuGet 팩 `.csproj` 에 빈 파일 요소를 무시 `.nuspec` 파일- [#3257](https://github.com/NuGet/Home/issues/3257)</span><span class="sxs-lookup"><span data-stu-id="12e4e-119">NuGet pack on `.csproj` ignores empty files element in `.nuspec` file - [#3257](https://github.com/NuGet/Home/issues/3257)</span></span>

* <span data-ttu-id="12e4e-120">IIS에서 호스팅되는 웹 사이트 프로젝트 실패-복원 하면 [#3235](https://github.com/NuGet/Home/issues/3235)</span><span class="sxs-lookup"><span data-stu-id="12e4e-120">Website projects hosted in IIS should not cause restore to fail - [#3235](https://github.com/NuGet/Home/issues/3235)</span></span>

* <span data-ttu-id="12e4e-121">자격 증명 v3 끝점에서 v 2-리디렉션하면 Nuget.Config에서 검색 되지 [#3179](https://github.com/NuGet/Home/issues/3179)</span><span class="sxs-lookup"><span data-stu-id="12e4e-121">Credentials not retrieved from Nuget.Config when v3 endpoint redirects to v2 - [#3179](https://github.com/NuGet/Home/issues/3179)</span></span>

* <span data-ttu-id="12e4e-122">NuGet 팩 휴대용 어셈블리 메타 데이터-검색할 때 어셈블리 해결 되지 않은 [#3128](https://github.com/NuGet/Home/issues/3128)</span><span class="sxs-lookup"><span data-stu-id="12e4e-122">NuGet pack fails to resolve assembly when retrieving portable assembly metadata - [#3128](https://github.com/NuGet/Home/issues/3128)</span></span>

* <span data-ttu-id="12e4e-123">Nuget을 찾을 수 없습니다 `msbuild.exe` 모노-에 [#3085](https://github.com/NuGet/Home/issues/3085)</span><span class="sxs-lookup"><span data-stu-id="12e4e-123">Nuget can't find `msbuild.exe` on Mono - [#3085](https://github.com/NuGet/Home/issues/3085)</span></span>

* <span data-ttu-id="12e4e-124">nuget.exe 팩 번호-로 시작 하는 시험판 태그를 허용 하지 않습니다. [#1743](https://github.com/NuGet/Home/issues/1743)</span><span class="sxs-lookup"><span data-stu-id="12e4e-124">nuget.exe pack doesn't allow a pre-release tag which begins with numbers - [#1743](https://github.com/NuGet/Home/issues/1743)</span></span>

* <span data-ttu-id="12e4e-125">VS2015E-에서 nuget 패키지 설치 실패 [#1298](https://github.com/NuGet/Home/issues/1298)</span><span class="sxs-lookup"><span data-stu-id="12e4e-125">nuget package install fails on VS2015E - [#1298](https://github.com/NuGet/Home/issues/1298)</span></span>

* <span data-ttu-id="12e4e-126">allowedversions가 필터링-솔루션 수준에서 작동 하지 [#333](https://github.com/NuGet/Home/issues/333)</span><span class="sxs-lookup"><span data-stu-id="12e4e-126">allowedVersions filter not working at solution level - [#333](https://github.com/NuGet/Home/issues/333)</span></span>

* <span data-ttu-id="12e4e-127">Restore는 임의로 동일한 항목와 함께 실패 키가 이미 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="12e4e-127">Restore randomly fails with An item with the same key has already been added.</span></span><span data-ttu-id="12e4e-128"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span><span class="sxs-lookup"><span data-stu-id="12e4e-128"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span></span>

* <span data-ttu-id="12e4e-129">Nuget.Common에 설치할 수 없습니다. `.csproj`  -  [#2635](https://github.com/NuGet/Home/issues/2635)</span><span class="sxs-lookup"><span data-stu-id="12e4e-129">Cannot install Nuget.Common in `.csproj` - [#2635](https://github.com/NuGet/Home/issues/2635)</span></span>

* <span data-ttu-id="12e4e-130">-각 ID에 대해 두 번 FindPackagesById 라고 V2 원본을 검색 하려면 UI를 사용 하는 경우 [#2517](https://github.com/NuGet/Home/issues/2517)</span><span class="sxs-lookup"><span data-stu-id="12e4e-130">When using the UI to search a V2 source, FindPackagesById is called twice for each ID - [#2517](https://github.com/NuGet/Home/issues/2517)</span></span>

* <span data-ttu-id="12e4e-131">패키지는 프로젝트-에 종속 될 수 없습니다 [#2490](https://github.com/NuGet/Home/issues/2490)</span><span class="sxs-lookup"><span data-stu-id="12e4e-131">Packages cannot depend on projects - [#2490](https://github.com/NuGet/Home/issues/2490)</span></span>

* <span data-ttu-id="12e4e-132">nuget.exe 팩-Exclude 문서화 되어 있지만 지원 되지 않습니다- [#2284](https://github.com/NuGet/Home/issues/2284)</span><span class="sxs-lookup"><span data-stu-id="12e4e-132">nuget.exe pack -Exclude is documented but not supported - [#2284](https://github.com/NuGet/Home/issues/2284)</span></span>

* <span data-ttu-id="12e4e-133">오류와 함께 문제 때 메시지의 '콘텐츠 ' 파일 섹션 `.nuspec` 잘못 되었습니다. [#1686](https://github.com/NuGet/Home/issues/1686)</span><span class="sxs-lookup"><span data-stu-id="12e4e-133">Issues with error messages when 'contentFiles' section of `.nuspec` is invalid - [#1686](https://github.com/NuGet/Home/issues/1686)</span></span>

* <span data-ttu-id="12e4e-134">푸시 전체 패키지 두 번으로 인증 된 패키지 소스에 항상 보냅니다 [#1501](https://github.com/NuGet/Home/issues/1501)</span><span class="sxs-lookup"><span data-stu-id="12e4e-134">Push always sends entire package twice with authenticated package sources - [#1501](https://github.com/NuGet/Home/issues/1501)</span></span>

* <span data-ttu-id="12e4e-135">프로젝트 nuget.exe 업데이트 \*.csproj 호출에 없을 때 제공한 없습니다 정보가 `packages.config`  -  [#1496](https://github.com/NuGet/Home/issues/1496)</span><span class="sxs-lookup"><span data-stu-id="12e4e-135">No information was given when calling nuget.exe update \*.csproj while the project does not have a `packages.config` - [#1496](https://github.com/NuGet/Home/issues/1496)</span></span>

* <span data-ttu-id="12e4e-136">`packages.config`복원-V2 원본의 5xx 상태 코드에 다시 시도 하지 [#1217](https://github.com/NuGet/Home/issues/1217)</span><span class="sxs-lookup"><span data-stu-id="12e4e-136">`packages.config` restore does not retry on 5xx status codes from V2 sources - [#1217](https://github.com/NuGet/Home/issues/1217)</span></span>

* <span data-ttu-id="12e4e-137">파일 src에 이중 점 `.nuspec` 작동 하지 않는- [#2947](https://github.com/NuGet/Home/issues/2947)</span><span class="sxs-lookup"><span data-stu-id="12e4e-137">Double dot in file src in `.nuspec` doesn't work - [#2947](https://github.com/NuGet/Home/issues/2947)</span></span>

* <span data-ttu-id="12e4e-138">CoreCLR 복원-암호화를 사용한 피드를 무시 하는 데 필요한 [#2942](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="12e4e-138">CoreCLR restore needs to ignore feeds with encryption - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="12e4e-139">nuget.exe 푸시-올바르게 하지 자격 증명을 물을-403 처리 [#2910](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="12e4e-139">nuget.exe push 403 handling - Incorrectly prompting for credentials - [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="12e4e-140">NuGet 패키지 관리자를 통해이 업데이트에서 속성을 제거는 `project.json`  -  [#2888](https://github.com/NuGet/Home/issues/2888)</span><span class="sxs-lookup"><span data-stu-id="12e4e-140">NuGet update through package manager removes properties from the `project.json` - [#2888](https://github.com/NuGet/Home/issues/2888)</span></span>

* <span data-ttu-id="12e4e-141">NuGet.PackageManagement.VisualStudio "NuGet.TeamFoundationServer14" 하지만 DLL 이름이 "NuGet.TeamFoundationServer-"으로 변경 되었음을 로드 하려고 [#2857](https://github.com/NuGet/Home/issues/2857)</span><span class="sxs-lookup"><span data-stu-id="12e4e-141">NuGet.PackageManagement.VisualStudio try to load "NuGet.TeamFoundationServer14", but that DLL name changed to "NuGet.TeamFoundationServer" - [#2857](https://github.com/NuGet/Home/issues/2857)</span></span>

* <span data-ttu-id="12e4e-142">UI 새로 표시 되지 않으면 패키지 관리자 버전-업데이트 [#2828](https://github.com/NuGet/Home/issues/2828)</span><span class="sxs-lookup"><span data-stu-id="12e4e-142">Package manager UI doesn't show newly updated version - [#2828](https://github.com/NuGet/Home/issues/2828)</span></span>

* <span data-ttu-id="12e4e-143">업데이트 패키지, 패키지 id를 사용 하려는 package.version-대신 버전 [#2771](https://github.com/NuGet/Home/issues/2771)</span><span class="sxs-lookup"><span data-stu-id="12e4e-143">update-package trying to use packageid,version instead of package.version - [#2771](https://github.com/NuGet/Home/issues/2771)</span></span>

* <span data-ttu-id="12e4e-144">nuget 복원 csproj 프로젝트 nuget를 사용할 수 없는 경우 오류 해야 (`packages.config` 또는 `project.json`)- [#2766](https://github.com/NuGet/Home/issues/2766)</span><span class="sxs-lookup"><span data-stu-id="12e4e-144">nuget restore csproj should error if the project isn't using nuget (`packages.config` or `project.json`) - [#2766](https://github.com/NuGet/Home/issues/2766)</span></span>

* <span data-ttu-id="12e4e-145">TFS 오류 "[파일] 작업 영역에서 찾을 수 없거나 액세스할 수 있는 권한이 없습니다" 하는 동안 업그레이드 또는 제거할 솔루션/프로젝트-TFS 소스 제어에 바인딩되어 있을 때 [#2739](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="12e4e-145">TFS Error "[file]not be found in your workspace, or you do not have permission to access it"  during upgrade or uninstall when solution/project is bound to TFS source control - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="12e4e-146">업데이트 패키지에는--대상 패키지의 종속성을 이해 하지 못합니다 [#2724](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="12e4e-146">update package doesn't get dependencies for non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="12e4e-147">Nuget 패키지 관리자 UI 작업-에 대 한 로그 자세한 표시 수준을 설정할 수 없으므로 [#2705](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="12e4e-147">There is no way to set logs verbosity level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="12e4e-148">nuget 구성이 잘못 되었습니다. VS 2015 VSIX (v3.4.3)- [#2667](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="12e4e-148">nuget configuration is invalid - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="12e4e-149">DefaultPushSource `NuGetDefaults.Config` (`ProgramData\NuGet`) 작동 하지 않는- [#2653](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="12e4e-149">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="12e4e-150">nuget 3.4.3 릴리스-패키지 빌드-에서 null 일 수 없습니다 값을 가져오는 [#2648](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="12e4e-150">nuget 3.4.3 release -  getting Value cannot be null on package build - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="12e4e-151">VSTS 피드-에 대 한 복원 Nuget.Config에서 저장 된 자격 증명을 사용 하지 않는 [#2647](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="12e4e-151">restore is not using stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="12e4e-152">[dotnet 복원]-configfile는 대신 cmd dir-프로젝트 디렉터리에 상대적 [#2639](https://github.com/NuGet/Home/issues/2639)</span><span class="sxs-lookup"><span data-stu-id="12e4e-152">[dotnet restore] --configfile is relative to project dir instead of the cmd dir - [#2639](https://github.com/NuGet/Home/issues/2639)</span></span>

* <span data-ttu-id="12e4e-153">버전 비교 코드-의 과도 한 할당 [#2632](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="12e4e-153">Excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="12e4e-154">이중 쓰기-병렬 원인에 동일한 설치 하는 동안 nuget.exe의 여러 인스턴스 패키지 [#2628](https://github.com/NuGet/Home/issues/2628)</span><span class="sxs-lookup"><span data-stu-id="12e4e-154">Multiple instances of nuget.exe trying to install the same package in parallel causes a double write - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="12e4e-155">-다중 프로젝트 작업에 대 한 종속성 정보가 캐시 되지 않으면 [#2619](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="12e4e-155">Dependency information is not cached for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="12e4e-156">설치 및 다운로드 패키지의 패키지 폴더를 먼저-확인 하지 않고 업데이트 [#2618](https://github.com/NuGet/Home/issues/2618)</span><span class="sxs-lookup"><span data-stu-id="12e4e-156">Install and update download packages without checking the packages folder first - [#2618](https://github.com/NuGet/Home/issues/2618)</span></span>

* <span data-ttu-id="12e4e-157">패키지 소스 목록에 수식이 있으면 UI 통해 패키지 소스를 추가할 수 없습니다 (NuGet 3.4.x)- [#2617](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="12e4e-157">If package source list is empty, cannot add package source via UI (NuGet 3.4.x) - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="12e4e-158">디자인 타임 외관-에 의존 하는 패키지를 설치 하려고 하면 오류가 있을 경우 잘못 해석 [#2594](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="12e4e-158">Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="12e4e-159">첫 번째 소스-시도 PackageManager "All"을 설정 하는 콘솔에서 패키지를 설치 [#2557](https://github.com/NuGet/Home/issues/2557)</span><span class="sxs-lookup"><span data-stu-id="12e4e-159">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="12e4e-160">압축을 푼 하지 최신 베타 ModernHttpClient- [#2518](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="12e4e-160">Latest beta not unzipping ModernHttpClient - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="12e4e-161">3.4.1-빌드된 자체 NuGet이 포함 된 시작 시 VS2015 크래시 [#2419](https://github.com/NuGet/Home/issues/2419)</span><span class="sxs-lookup"><span data-stu-id="12e4e-161">VS2015 crash at startup with self-built NuGet 3.4.1 - [#2419](https://github.com/NuGet/Home/issues/2419)</span></span>

* <span data-ttu-id="12e4e-162">Update 명령은 i 수 이므로...-하도록 요청 하는 경우 좀 더 자세한 정보 수 [#2418](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="12e4e-162">Update command might be a bit more verbose if i ask it to be so... - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="12e4e-163">로컬에서 빌드한 VSIX CI 빌드와 동일한 Dll 및 파일 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="12e4e-163">VSIX built locally should have the same DLLs and files as the CI build.</span></span><span data-ttu-id="12e4e-164"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span><span class="sxs-lookup"><span data-stu-id="12e4e-164"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span></span>

* <span data-ttu-id="12e4e-165">빌드-에 NuGet 다운 그레이드 경고를 수정 [#2396](https://github.com/NuGet/Home/issues/2396)</span><span class="sxs-lookup"><span data-stu-id="12e4e-165">Fix NuGet downgrade warnings in the build - [#2396](https://github.com/NuGet/Home/issues/2396)</span></span>

* <span data-ttu-id="12e4e-166">영구적으로 차단 된 패키지 소스 (3 시간) 인증에 실패할 [#2362](https://github.com/NuGet/Home/issues/2362)</span><span class="sxs-lookup"><span data-stu-id="12e4e-166">Failing to authenticate package source (3 times) is blocked forever - [#2362](https://github.com/NuGet/Home/issues/2362)</span></span>

* <span data-ttu-id="12e4e-167">패키지 콘텐츠 인수와 함께 피드 nuget v3.3 +에서 패키지를 설치할 때 제대로 복원 되지-NoCache 패키지에 포함 된 경우 `.nupkg` 파일- [#2354](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="12e4e-167">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="12e4e-168">모든 패키지 소스 하지만 1 원본에서 누락 된 패키지와 함께 Nuget 설치 실패- [#2322](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="12e4e-168">Nuget Install with All Package Sources, but package missing from 1 source, fails - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="12e4e-169">[PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll!NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+\*lt;&gt;c__DisplayClass_0+&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)</span><span class="sxs-lookup"><span data-stu-id="12e4e-169">[PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll!NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+\*lt;&gt;c__DisplayClass_0+&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)</span></span>

* <span data-ttu-id="12e4e-170">단일 소스 권한 부여-에 실패 하는 경우 블록 설치 [#2034](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="12e4e-170">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="12e4e-171">`.nuspec`범위는-IncludeReferencedProjects 버전-를 재정의 해야 하는 버전 [#1983](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="12e4e-171">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="12e4e-172">업데이트 패키지는 super-"를 수집 하려는 종속성 정보"-느린 [#1909](https://github.com/NuGet/Home/issues/1909)</span><span class="sxs-lookup"><span data-stu-id="12e4e-172">Update-Package super slow - "Attempting to gather dependencies information" - [#1909](https://github.com/NuGet/Home/issues/1909)</span></span>

* <span data-ttu-id="12e4e-173">날카로운 다운 그레이드 NuGet 패키지 될 때 일괄 처리의 종속성-업데이트 [#1903](https://github.com/NuGet/Home/issues/1903)</span><span class="sxs-lookup"><span data-stu-id="12e4e-173">NuGet stealth downgrades package when batch updating its dependencies - [#1903](https://github.com/NuGet/Home/issues/1903)</span></span>

* <span data-ttu-id="12e4e-174">nuget.exe 업데이트 어셈블리의 강력한 이름 및 개인 특성을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="12e4e-174">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="12e4e-175"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="12e4e-175"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="12e4e-176">"DefaultPushSource"-에 대 한 상대 파일 경로 [#1746](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="12e4e-176">Relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="12e4e-177">해결 프로그램 실패 메시지-개선 [#1373](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="12e4e-177">Improve resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

* <span data-ttu-id="12e4e-178">v 3에서 업데이트 패키지-지정된 된 소스에 없는 패키지와 함께 실패 [#1013](https://github.com/NuGet/Home/issues/1013)</span><span class="sxs-lookup"><span data-stu-id="12e4e-178">update-package in v3 fails with packages not in the specified source - [#1013](https://github.com/NuGet/Home/issues/1013)</span></span>

* <span data-ttu-id="12e4e-179">패키지 원본에 대 한 상대 경로 사용 하는 것은 사용 하지 않으려면-문제가 [#865](https://github.com/NuGet/Home/issues/865)</span><span class="sxs-lookup"><span data-stu-id="12e4e-179">Using relative paths for package sources is problematic to use - [#865](https://github.com/NuGet/Home/issues/865)</span></span>

* <span data-ttu-id="12e4e-180">간접 종속성으로 더 낮은 버전 요구 사항-이미 있는 경우 프로젝트에서 생성 한 NUPKG 파일에 대 한 종속성이 없습니다 [#759](https://github.com/NuGet/Home/issues/759)</span><span class="sxs-lookup"><span data-stu-id="12e4e-180">Missing dependency in NUPKG-file generated from project if indirect dependency already exists with a lower version requirement - [#759](https://github.com/NuGet/Home/issues/759)</span></span>

* <span data-ttu-id="12e4e-181">프로젝트를 삭제 하면 해당 UI 창 닫지만, 프로젝트 이름 바꾸기 UI 창 바뀌지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="12e4e-181">Deleting a project closes corresponding UI window, but, renaming a project does not rename the UI window.</span></span> <span data-ttu-id="12e4e-182">프로젝트 이름 바꾸기 및 프로젝트 제거 이벤트-PMC 수신 대기 하도록 참고 [#670](https://github.com/NuGet/Home/issues/670)</span><span class="sxs-lookup"><span data-stu-id="12e4e-182">Note that PMC listens to project rename and project remove events - [#670](https://github.com/NuGet/Home/issues/670)</span></span>

* <span data-ttu-id="12e4e-183">[버드 웹 작업] Razor v3 WSP 만들기 중단- [#3241](https://github.com/NuGet/Home/issues/3241)</span><span class="sxs-lookup"><span data-stu-id="12e4e-183">[Willow Web Workload] Creating Razor v3 WSP hangs - [#3241](https://github.com/NuGet/Home/issues/3241)</span></span>

* <span data-ttu-id="12e4e-184">"패키지에 여러 nuspec 파일이 들어 있습니다."와 함께 특정 패키지의 설치/복원 실패</span><span class="sxs-lookup"><span data-stu-id="12e4e-184">Install/restore of a particular package fails with "Package contains multiple nuspec files."</span></span><span data-ttu-id="12e4e-185"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="12e4e-185"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="12e4e-186">Id 소문자로 & `packages.config` 시나리오- [#3209](https://github.com/NuGet/Home/issues/3209)</span><span class="sxs-lookup"><span data-stu-id="12e4e-186">Lowercase IDs & `packages.config` scenarios - [#3209](https://github.com/NuGet/Home/issues/3209)</span></span>

* <span data-ttu-id="12e4e-187">[beta2 3.5] 패키지 복원이 실패-"레거시" 패키지를 복원 하도록 [#3208](https://github.com/NuGet/Home/issues/3208)</span><span class="sxs-lookup"><span data-stu-id="12e4e-187">[3.5-beta2] Package restore fails to restore "legacy" packages - [#3208](https://github.com/NuGet/Home/issues/3208)</span></span>

* <span data-ttu-id="12e4e-188">nuget 팩.tt 파일 어떠한-콘텐츠 폴더에 강제적으로 추가 [#3203](https://github.com/NuGet/Home/issues/3203)</span><span class="sxs-lookup"><span data-stu-id="12e4e-188">nuget pack forcefully adds .tt files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="12e4e-189">파일에 관련 경고를 생성 하는 ASP.NET 웹 앱의 업데이트 패키지: 소스- [#3194](https://github.com/NuGet/Home/issues/3194)</span><span class="sxs-lookup"><span data-stu-id="12e4e-189">update-package of ASP.NET web app generates warning related to file: source - [#3194](https://github.com/NuGet/Home/issues/3194)</span></span>

* <span data-ttu-id="12e4e-190">nuget 팩 csproj (으로 `project.json`) packOptions 및 소유자-JSON 파일에 없는 경우 충돌 [#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="12e4e-190">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="12e4e-191">에 대 한 nuget 팩 `project.json` 요약, 작성자, 등-소유자와 같은 packOptions 태그를 무시 [#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="12e4e-191">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="12e4e-192">NullReferenceException via NuGet.Packaging.PhysicalPackageFile.GetStream - [#3160](https://github.com/NuGet/Home/issues/3160)</span><span class="sxs-lookup"><span data-stu-id="12e4e-192">NullReferenceException via NuGet.Packaging.PhysicalPackageFile.GetStream - [#3160](https://github.com/NuGet/Home/issues/3160)</span></span>

* <span data-ttu-id="12e4e-193">출력에서 종속성을 무시 하는 NuGet 팩 `.nuspec` 에 대 한 `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="12e4e-193">NuGet pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="12e4e-194">프로젝트 손상된 상태로-남게 되므로 롤백으로 여러 패키지를 업데이트할 [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="12e4e-194">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="12e4e-195">Netstandard 프로젝트-에 대 한 콘텐츠 파일에서 추가 되지 않습니다 [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="12e4e-195">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="12e4e-196">.NET을 대상으로 하는 라이브러리 패키지할 수 없습니다. 표준 올바르게- [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="12e4e-196">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="12e4e-197">파일-새 프로젝트 > v s 2015 및 Dev15-클래스 라이브러리 (이식 가능) 프로젝트 실패-> [#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="12e4e-197">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="12e4e-198">NuGet 오류-1.0.0-\*-올바른 버전 문자열이 아닙니다. [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="12e4e-198">nuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="12e4e-199">Find-package 실패를 표시 하지만 Install-package works- [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="12e4e-199">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="12e4e-200">오류 때 dev15-에 "Install-package jquery.validation" [#3061](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="12e4e-200">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="12e4e-201">잘못 된 대상 경로-xproj nuget 팩이 선택은 기본값인 [#3060](https://github.com/NuGet/Home/issues/3060)</span><span class="sxs-lookup"><span data-stu-id="12e4e-201">nuget pack of xproj is defaulting to invalid target path - [#3060](https://github.com/NuGet/Home/issues/3060)</span></span>

* <span data-ttu-id="12e4e-202">설치 된 VS 2015 업데이트 3 버전 3.5.0 오류가 발생 합니다. NuGet을 사용 하는 VS에서 [#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="12e4e-202">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="12e4e-203">"Packages.config에 의해 차단" `project.json` (UWP, 통합 하는 사항 빌드) 프로젝트- [#3046](https://github.com/NuGet/Home/issues/3046)</span><span class="sxs-lookup"><span data-stu-id="12e4e-203">"Blocked by packages.config" in `project.json` (UWP, a.k.a build integrated) project - [#3046](https://github.com/NuGet/Home/issues/3046)</span></span>

* <span data-ttu-id="12e4e-204">dotnet cli preview2 003121 공식 preview2 빌드는 빌드 스크립트에서 설치를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="12e4e-204">update dotnet cli installed by build script to preview2-003121, which is the official preview2 build.</span></span><span data-ttu-id="12e4e-205"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span><span class="sxs-lookup"><span data-stu-id="12e4e-205"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span></span>

* <span data-ttu-id="12e4e-206">패키지 관리자 UI: 패키지를 업데이트 한 후 새 버전을 표시 하지 않는- [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="12e4e-206">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="12e4e-207">Delete 명령줄에-ApiKey 읽기/에서 전송 되지 않습니다 3.5.0-beta- [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="12e4e-207">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="12e4e-208">잘못 된 문자열: 안정판 패키지에는 시험판 종속성 없어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="12e4e-208">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="12e4e-209"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="12e4e-209"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="12e4e-210">OptimizedZipPackage 캐시-빈 폴더를 둡니다 [#3029](https://github.com/NuGet/Home/issues/3029)</span><span class="sxs-lookup"><span data-stu-id="12e4e-210">OptimizedZipPackage cache leaves empty folders - [#3029](https://github.com/NuGet/Home/issues/3029)</span></span>

* <span data-ttu-id="12e4e-211">(Net46 및 windows 10) PCL 프로젝트 get NullRef 예외를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="12e4e-211">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="12e4e-212"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="12e4e-212"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="12e4e-213">더 높은 버전 allowedversions가 제약 조건-에 의해 제한 되는 경우 Nuget 업데이트 알림 메시지를 제공 해야 [#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="12e4e-213">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="12e4e-214">Nuget v3 복원 문제- [#2891](https://github.com/NuGet/Home/issues/2891)</span><span class="sxs-lookup"><span data-stu-id="12e4e-214">Nuget v3 restore issues - [#2891](https://github.com/NuGet/Home/issues/2891)</span></span>

* <span data-ttu-id="12e4e-215">자격 증명 플러그 인) 종료 되었습니다 (오류-1 /-여러 소스가 포함 된 자격 증명 공급자를 사용 하는 경우 패키지 오류 다운로드 [#2885](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="12e4e-215">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="12e4e-216">`project.json`nuget 복원 하면 변경-항목이 없을 경우 다시 컴파일이 [#2817](https://github.com/NuGet/Home/issues/2817)</span><span class="sxs-lookup"><span data-stu-id="12e4e-216">`project.json` nuget restore causes recompilation when nothing changed - [#2817](https://github.com/NuGet/Home/issues/2817)</span></span>

* <span data-ttu-id="12e4e-217">기호 패키지가 현재까지 여야 설치 또는 업데이트-에서 사용할 [#2807](https://github.com/NuGet/Home/issues/2807)</span><span class="sxs-lookup"><span data-stu-id="12e4e-217">Symbols packages should not ever be used in install or update - [#2807](https://github.com/NuGet/Home/issues/2807)</span></span>

* <span data-ttu-id="12e4e-218">VS repositoryPath의 환경 변수를 지원 하지 않습니다 (nuget.exe은)- [#2763](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="12e4e-218">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="12e4e-219">내게 필요한 옵션 기능에 대 한 패키지 관리자 UI에서 레이블이 지정 되지 않은 Uielement 레이블을 [#2745](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="12e4e-219">Label the unlabeled UIElements in Package Manager UI for accessibility - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="12e4e-220">하이픈으로 연결 된 프로필을 통해 휴대용 프레임 워크는 거부 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12e4e-220">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="12e4e-221"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="12e4e-221"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="12e4e-222">NuGet 패키지 관리자를 수행 하는 세부 정보에 적용 되지 않는 패키지에 해당 옵션 목록 지우기 `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="12e4e-222">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="12e4e-223">nuget.exe 푸시/delete-API 키를 사용 하지 않으며 [#2627](https://github.com/NuGet/Home/issues/2627)</span><span class="sxs-lookup"><span data-stu-id="12e4e-223">nuget.exe push/delete won't use API Key  - [#2627](https://github.com/NuGet/Home/issues/2627)</span></span>

* <span data-ttu-id="12e4e-224">잠금 파일이-에서 잠긴된 속성을 제거 [#2379](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="12e4e-224">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="12e4e-225">NuGet 3.3.0 업데이트와 함께 실패 '... 추가 제약 조건에 정의 된 packages.config이이 작업을 방지 합니다.'</span><span class="sxs-lookup"><span data-stu-id="12e4e-225">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="12e4e-226"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="12e4e-226"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="12e4e-227">잘못 된 메시지-throw 존재 하지 않는 로컬 원본의 패키지 설치 [#1674](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="12e4e-227">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="12e4e-228">"업그레이드 가능" 필터 표시-버전 제약 조건을 위반 하는 업그레이드 [#1094](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="12e4e-228">"Upgrade available" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

* <span data-ttu-id="12e4e-229">-기본 패키지를 업데이트할 수 없습니다 [#1291](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="12e4e-229">Unable to update native packages - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>


## <a name="features"></a><span data-ttu-id="12e4e-230">기능</span><span class="sxs-lookup"><span data-stu-id="12e4e-230">Features</span></span>

* <span data-ttu-id="12e4e-231">Nuget-추가한 참조에 false로 설정 CopyLocal 지원 [#329](https://github.com/NuGet/Home/issues/329)</span><span class="sxs-lookup"><span data-stu-id="12e4e-231">Support setting CopyLocal to false on references added by NuGet - [#329](https://github.com/NuGet/Home/issues/329)</span></span>

* <span data-ttu-id="12e4e-232">MSBuild 15-에 대 한 지원 nuget.exe [#1937](https://github.com/NuGet/Home/issues/1937)</span><span class="sxs-lookup"><span data-stu-id="12e4e-232">nuget.exe support for MSBuild 15 - [#1937](https://github.com/NuGet/Home/issues/1937)</span></span>

* <span data-ttu-id="12e4e-233">팩 지원 합니다.`csproj`</span><span class="sxs-lookup"><span data-stu-id="12e4e-233">Pack support for .`csproj`</span></span><span data-ttu-id="12e4e-234"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span><span class="sxs-lookup"><span data-stu-id="12e4e-234"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span></span>

* <span data-ttu-id="12e4e-235">사용자 작업을 실행 중인 경우 사용자 작업 사용 안 함- [#1440](https://github.com/NuGet/Home/issues/1440)</span><span class="sxs-lookup"><span data-stu-id="12e4e-235">Disable user action when there are user actions being executed - [#1440](https://github.com/NuGet/Home/issues/1440)</span></span>

* <span data-ttu-id="12e4e-236">NuGet에 대 한 지원을 추가 해야 `runtimes/{rid}/nativeassets/{txm}/`  -  [#2782](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="12e4e-236">NuGet should add support for `runtimes/{rid}/nativeassets/{txm}/` - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>

* <span data-ttu-id="12e4e-237">NuGet에 누락 된 프레임 워크 호환성 추가 (이미에 있는 3.x) 2.x- [#2720](https://github.com/NuGet/Home/issues/2720)</span><span class="sxs-lookup"><span data-stu-id="12e4e-237">Add framework compatibilities missing in NuGet 2.x (which are already in 3.x) - [#2720](https://github.com/NuGet/Home/issues/2720)</span></span>

* <span data-ttu-id="12e4e-238">-대체 패키지 폴더에 대 한 지원 [#2899](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="12e4e-238">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="12e4e-239">디자인 및 구현-도구 패키지를 지원 하기 위해 패키지 형식의 개념 [#2476](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="12e4e-239">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="12e4e-240">경로를 가져오는 전역 패키지 폴더에 API 추가 [#2403](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="12e4e-240">Add an API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="12e4e-241">팩-SemVer 2.0.0을 사용 하도록 설정 [#3356](https://github.com/NuGet/Home/issues/3356)</span><span class="sxs-lookup"><span data-stu-id="12e4e-241">Enable SemVer 2.0.0 in pack - [#3356](https://github.com/NuGet/Home/issues/3356)</span></span>

## <a name="dcrs"></a><span data-ttu-id="12e4e-242">DCR</span><span class="sxs-lookup"><span data-stu-id="12e4e-242">DCRs</span></span>

* <span data-ttu-id="12e4e-243">nuget.exe 푸시-timeout 매개 변수 작동 하지 않는- [#2785](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="12e4e-243">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="12e4e-244">패키지 설명 텍스트를 선택할-수 [#1769](https://github.com/NuGet/Home/issues/1769)</span><span class="sxs-lookup"><span data-stu-id="12e4e-244">Package Description text should be selectable - [#1769](https://github.com/NuGet/Home/issues/1769)</span></span>

* <span data-ttu-id="12e4e-245">활성화 되려면 nuget.exe `.props` 및 `.targets` 파일에 대 한 `.nuproj` 프로젝트 [#2711](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="12e4e-245">Enable nuget.exe to produce `.props` and `.targets` files for `.nuproj` projects [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="12e4e-246">확장성 가져오기-프레임 워크를 비교 하는 API 추가 [#2633](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="12e4e-246">Add extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="12e4e-247">종속성 옵션을 사용 하는 경우 숨기기 `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="12e4e-247">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="12e4e-248">인쇄 결과물에 자세한 출력-버전 헤더 nuget.exe [#1887](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="12e4e-248">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="12e4e-249">사용자는 업그레이드/설치 기반 dotnet tfm PCL 발생할 수 문제-알 수 있도록 필요한 NuGet [#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="12e4e-249">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="12e4e-250">잘못 된 설치/업그레이드 tfm w / 프로젝트에 대 한 경고 "dotnet"-= [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="12e4e-250">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="12e4e-251">-업데이트에 대 한 ReShaper 및 NuGet의 성능 문제를 해결 [#3044](https://github.com/NuGet/Home/issues/3044)</span><span class="sxs-lookup"><span data-stu-id="12e4e-251">Fix performance issues with ReShaper and NuGet for Update - [#3044](https://github.com/NuGet/Home/issues/3044)</span></span>

* <span data-ttu-id="12e4e-252">Netcoreapp11 및 netstandard17 지원-추가 [#2998](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="12e4e-252">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="12e4e-253">에 대 한 활용 AssemblyMetadata 특성 `.nuspec` 토큰 바꾸기를- [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="12e4e-253">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>
