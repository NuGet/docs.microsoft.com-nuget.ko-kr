---
title: NuGet 3.5 RTM 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 Ecrs를 비롯 한 NuGet 3.5에 대 한 릴리스 정보입니다.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 158373fb62f57fe6947fb863a1eef8122399959a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776358"
---
# <a name="nuget-35-release-notes"></a><span data-ttu-id="9ceb2-103">NuGet 3.5 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="9ceb2-103">NuGet 3.5 Release Notes</span></span>

<span data-ttu-id="9ceb2-104">[NuGet 3.5-RC 릴리스 정보](../release-notes/nuget-3.5-RC.md)  |  [NuGet 4.0 RC 릴리스 정보](../release-notes/nuget-4.0-RC.md)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-104">[NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md) | [NuGet 4.0 RC Release Notes](../release-notes/nuget-4.0-RC.md)</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="9ceb2-105">버그 픽스</span><span class="sxs-lookup"><span data-stu-id="9ceb2-105">Bug Fixes</span></span>

* <span data-ttu-id="9ceb2-106">Pack은 mono에서 MSBuild 14.1을 사용 하지 않습니다 [#3550](https://github.com/NuGet/Home/issues/3550)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-106">Pack doesn't use MSBuild 14.1 on mono - [#3550](https://github.com/NuGet/Home/issues/3550)</span></span>

* <span data-ttu-id="9ceb2-107">업데이트 탭에서 업데이트할 최신 버전을 선택 하지 않고 현재 설치 된 버전- [#3498](https://github.com/NuGet/Home/issues/3498) 를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ceb2-107">Update tab doesn't select the latest available version to update instead select current installed version - [#3498](https://github.com/NuGet/Home/issues/3498)</span></span>

* <span data-ttu-id="9ceb2-108">사설 v2 MyGet 피드를 인증 한 후 "x 개 결과 표시 [#3469](https://github.com/NuGet/Home/issues/3469) "를 클릭 하 여 충돌을 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ceb2-108">Fix Crash after authenticating a private v2 MyGet feed and clicking "Show x more results" - [#3469](https://github.com/NuGet/Home/issues/3469)</span></span>

* <span data-ttu-id="9ceb2-109">로그 메시지는 UI [#3446](https://github.com/NuGet/Home/issues/3446) 의 반대 순서로 되어 있는 것 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9ceb2-109">Log messages seem to be in reverse order for UI - [#3446](https://github.com/NuGet/Home/issues/3446)</span></span>

* <span data-ttu-id="9ceb2-110">v 3.4.4-Nuget 복원이 "지정 된 경로의 형식이 지원 되지 않습니다."- [#3442](https://github.com/NuGet/Home/issues/3442)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-110">v3.4.4 - Nuget restore throws "The given path's format is not supported" - [#3442](https://github.com/NuGet/Home/issues/3442)</span></span>

* <span data-ttu-id="9ceb2-111">NuGet 명령줄 3.6 beta는 Prop 구성 = 릴리스- [#3432](https://github.com/NuGet/Home/issues/3432)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-111">NuGet cmdLine 3.6 beta does not honor -Prop Configuration = Release - [#3432](https://github.com/NuGet/Home/issues/3432)</span></span>

* <span data-ttu-id="9ceb2-112">IKVM large project에 느림 설치- [#3428](https://github.com/NuGet/Home/issues/3428)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-112">Nuget IKVM slow install on large project - [#3428](https://github.com/NuGet/Home/issues/3428)</span></span>

* <span data-ttu-id="9ceb2-113">nuget.exe 업데이트-자체 업데이트를 유지 합니다.- [#3395](https://github.com/NuGet/Home/issues/3395)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-113">nuget.exe Update -Self keeps on updating itself - [#3395](https://github.com/NuGet/Home/issues/3395)</span></span>

* <span data-ttu-id="9ceb2-114">3.5 UNC 공유의 설치/복원 3.4.4- [#3355](https://github.com/NuGet/Home/issues/3355) 에서 성능 재발</span><span class="sxs-lookup"><span data-stu-id="9ceb2-114">3.5 install/restore from UNC share has performance Regression from 3.4.4 - [#3355](https://github.com/NuGet/Home/issues/3355)</span></span>

* <span data-ttu-id="9ceb2-115">Net451 프로젝트에 대 한 패키지 관리 UI에서 Moq를 설치 하는 경우 오류- [#3349](https://github.com/NuGet/Home/issues/3349)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-115">Error when installing Moq from the Package management UI for a net451 project - [#3349](https://github.com/NuGet/Home/issues/3349)</span></span>

* <span data-ttu-id="9ceb2-116">솔루션 수준에서 설치 탭은 패키지의 버전 [#3339](https://github.com/NuGet/Home/issues/3339) 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9ceb2-116">Install tab at solution level doesn't show package's version - [#3339](https://github.com/NuGet/Home/issues/3339)</span></span>

* <span data-ttu-id="9ceb2-117">`project.json`설치 된 탭의 xproj 업데이트가 상태를 손실 합니다. [#3303](https://github.com/NuGet/Home/issues/3303)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-117">xproj `project.json` update from Installed tab loses state - [#3303](https://github.com/NuGet/Home/issues/3303)</span></span>

* <span data-ttu-id="9ceb2-118">NuGet pack on에서 `.csproj` 파일의 빈 파일 요소 무시 `.nuspec` - [#3257](https://github.com/NuGet/Home/issues/3257)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-118">NuGet pack on `.csproj` ignores empty files element in `.nuspec` file - [#3257](https://github.com/NuGet/Home/issues/3257)</span></span>

* <span data-ttu-id="9ceb2-119">IIS에서 호스트 되는 웹 사이트 프로젝트는 복원이 실패 하지 않도록 합니다. [#3235](https://github.com/NuGet/Home/issues/3235)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-119">Website projects hosted in IIS should not cause restore to fail - [#3235](https://github.com/NuGet/Home/issues/3235)</span></span>

* <span data-ttu-id="9ceb2-120">V3 끝점이 v2로 리디렉션되는 경우 Nuget.Config에서 자격 증명을 검색 하지 [#3179](https://github.com/NuGet/Home/issues/3179)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-120">Credentials not retrieved from Nuget.Config when v3 endpoint redirects to v2 - [#3179](https://github.com/NuGet/Home/issues/3179)</span></span>

* <span data-ttu-id="9ceb2-121">이식 가능한 어셈블리 메타 데이터를 검색할 때 NuGet 팩이 어셈블리를 확인 하지 못함- [#3128](https://github.com/NuGet/Home/issues/3128)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-121">NuGet pack fails to resolve assembly when retrieving portable assembly metadata - [#3128](https://github.com/NuGet/Home/issues/3128)</span></span>

* <span data-ttu-id="9ceb2-122">Nuget `msbuild.exe` 에서 Mono- [#3085](https://github.com/NuGet/Home/issues/3085) 를 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9ceb2-122">Nuget can't find `msbuild.exe` on Mono - [#3085](https://github.com/NuGet/Home/issues/3085)</span></span>

* <span data-ttu-id="9ceb2-123">nuget.exe 팩은 숫자로 시작 하는 시험판 태그를 허용 하지 않습니다 [#1743](https://github.com/NuGet/Home/issues/1743)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-123">nuget.exe pack doesn't allow a pre-release tag which begins with numbers - [#1743](https://github.com/NuGet/Home/issues/1743)</span></span>

* <span data-ttu-id="9ceb2-124">VS2015E- [#1298](https://github.com/NuGet/Home/issues/1298) 에서 nuget 패키지 설치가 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ceb2-124">nuget package install fails on VS2015E - [#1298](https://github.com/NuGet/Home/issues/1298)</span></span>

* <span data-ttu-id="9ceb2-125">allowedVersions 필터가 솔루션 수준에서 작동 하지 않음- [#333](https://github.com/NuGet/Home/issues/333)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-125">allowedVersions filter not working at solution level - [#333](https://github.com/NuGet/Home/issues/333)</span></span>

* <span data-ttu-id="9ceb2-126">동일한 키가 있는 항목이 이미 추가 된 상태에서 복원이 임의로 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ceb2-126">Restore randomly fails with An item with the same key has already been added.</span></span><span data-ttu-id="9ceb2-127"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-127"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span></span>

* <span data-ttu-id="9ceb2-128">Nuget을 설치할 수 없습니다. `.csproj`  -  [#2635](https://github.com/NuGet/Home/issues/2635) 에 공통 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ceb2-128">Cannot install Nuget.Common in `.csproj` - [#2635](https://github.com/NuGet/Home/issues/2635)</span></span>

* <span data-ttu-id="9ceb2-129">UI를 사용 하 여 V2 소스를 검색 하는 경우 각 ID에 대해 FindPackagesById가 두 번 호출 됩니다 [#2517](https://github.com/NuGet/Home/issues/2517)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-129">When using the UI to search a V2 source, FindPackagesById is called twice for each ID - [#2517](https://github.com/NuGet/Home/issues/2517)</span></span>

* <span data-ttu-id="9ceb2-130">패키지는 프로젝트에 종속 될 수 없습니다.- [#2490](https://github.com/NuGet/Home/issues/2490)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-130">Packages cannot depend on projects - [#2490](https://github.com/NuGet/Home/issues/2490)</span></span>

* <span data-ttu-id="9ceb2-131">nuget.exe 팩-제외는 문서화 되었지만 지원 되지 않음- [#2284](https://github.com/NuGet/Home/issues/2284)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-131">nuget.exe pack -Exclude is documented but not supported - [#2284](https://github.com/NuGet/Home/issues/2284)</span></span>

* <span data-ttu-id="9ceb2-132">의 ' contentFiles ' 섹션이 잘못 된 경우 오류 메시지와 관련 된 문제 `.nuspec` - [#1686](https://github.com/NuGet/Home/issues/1686)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-132">Issues with error messages when 'contentFiles' section of `.nuspec` is invalid - [#1686](https://github.com/NuGet/Home/issues/1686)</span></span>

* <span data-ttu-id="9ceb2-133">Push는 항상 인증 된 패키지 원본으로 전체 패키지를 두 번 보냅니다. [#1501](https://github.com/NuGet/Home/issues/1501)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-133">Push always sends entire package twice with authenticated package sources - [#1501](https://github.com/NuGet/Home/issues/1501)</span></span>

* <span data-ttu-id="9ceb2-134">프로젝트에 #1496 없는 동안 nuget.exe update \* .csproj를 호출할 때 정보가 제공 되지 않았습니다. `packages.config`  -  [](https://github.com/NuGet/Home/issues/1496)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-134">No information was given when calling nuget.exe update \*.csproj while the project does not have a `packages.config` - [#1496](https://github.com/NuGet/Home/issues/1496)</span></span>

* <span data-ttu-id="9ceb2-135">`packages.config` 복원은 V2 원본에서 5xx 상태 코드를 다시 시도 하지 않습니다- [#1217](https://github.com/NuGet/Home/issues/1217)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-135">`packages.config` restore does not retry on 5xx status codes from V2 sources - [#1217](https://github.com/NuGet/Home/issues/1217)</span></span>

* <span data-ttu-id="9ceb2-136">의 파일 src에서 이중 점이 `.nuspec` 작동 하지 않음- [#2947](https://github.com/NuGet/Home/issues/2947)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-136">Double dot in file src in `.nuspec` doesn't work - [#2947](https://github.com/NuGet/Home/issues/2947)</span></span>

* <span data-ttu-id="9ceb2-137">CoreCLR 복원은 암호화를 사용 하 여 피드를 무시 해야 합니다.- [#2942](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-137">CoreCLR restore needs to ignore feeds with encryption - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="9ceb2-138">nuget.exe push 403 처리-자격 증명을 잘못 입력- [#2910](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-138">nuget.exe push 403 handling - Incorrectly prompting for credentials - [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="9ceb2-139">패키지 관리자를 통한 NuGet 업데이트는 #2888에서 속성을 제거 합니다. `project.json`  -  [](https://github.com/NuGet/Home/issues/2888)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-139">NuGet update through package manager removes properties from the `project.json` - [#2888](https://github.com/NuGet/Home/issues/2888)</span></span>

* <span data-ttu-id="9ceb2-140">VisualStudio는 "TeamFoundationServer14"를 로드 하려고 하지만 해당 DLL 이름이 "TeamFoundationServer"- [#2857](https://github.com/NuGet/Home/issues/2857) 로 변경 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9ceb2-140">NuGet.PackageManagement.VisualStudio try to load "NuGet.TeamFoundationServer14", but that DLL name changed to "NuGet.TeamFoundationServer" - [#2857](https://github.com/NuGet/Home/issues/2857)</span></span>

* <span data-ttu-id="9ceb2-141">패키지 관리자 UI에 새로 업데이트 된 버전이 표시 되지 않음- [#2828](https://github.com/NuGet/Home/issues/2828)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-141">Package manager UI doesn't show newly updated version - [#2828](https://github.com/NuGet/Home/issues/2828)</span></span>

* <span data-ttu-id="9ceb2-142">packageid-#2771 대신 버전을 사용 하려고 하는 패키지 패키지입니다. 버전- [](https://github.com/NuGet/Home/issues/2771)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-142">update-package trying to use packageid,version instead of package.version - [#2771](https://github.com/NuGet/Home/issues/2771)</span></span>

* <span data-ttu-id="9ceb2-143">프로젝트에서 nuget (또는)을 사용 하지 않는 경우 nuget 복원 .csproj에서 오류가 발생 `packages.config` `project.json` [#2766](https://github.com/NuGet/Home/issues/2766)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-143">nuget restore csproj should error if the project isn't using nuget (`packages.config` or `project.json`) - [#2766](https://github.com/NuGet/Home/issues/2766)</span></span>

* <span data-ttu-id="9ceb2-144">TFS 오류 "[file]을 (를) 작업 영역에서 찾을 수 없거나, 솔루션/프로젝트가 TFS 원본 제어에 바인딩되어 있을 때 업그레이드 또는 제거 하는 동안" 액세스할 수 있는 권한이 없습니다.- [#2739](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-144">TFS Error "[file]not be found in your workspace, or you do not have permission to access it"  during upgrade or uninstall when solution/project is bound to TFS source control - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="9ceb2-145">업데이트 패키지가 대상이 아닌 패키지에 대 한 종속성을 가져오지 않습니다.- [#2724](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-145">update package doesn't get dependencies for non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="9ceb2-146">Nuget 패키지 관리자 UI 작업에 대 한 로그의 자세한 정도를 설정 하는 방법은 없습니다. [#2705](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-146">There is no way to set logs verbosity level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="9ceb2-147">nuget 구성이 잘못 됨-VS 2015 VSIX (v 3.4.3)- [#2667](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-147">nuget configuration is invalid - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="9ceb2-148">DefaultPushSource in `NuGetDefaults.Config` ( `ProgramData\NuGet` )이 작동 하지 않음- [#2653](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-148">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="9ceb2-149">nuget 3.4.3 release-패키지 빌드에서 값을 가져오는 것은 null 일 수 없습니다.- [#2648](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-149">nuget 3.4.3 release -  getting Value cannot be null on package build - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="9ceb2-150">복원 기능이 VSTS 피드에 대 한 Nuget.Config의 저장 된 자격 증명을 사용 하지 않습니다.- [#2647](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-150">restore is not using stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="9ceb2-151">[dotnet restore]--m은 cmd dir- [#2639](https://github.com/NuGet/Home/issues/2639) 대신 프로젝트 디렉터리를 기준으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ceb2-151">[dotnet restore] --configfile is relative to project dir instead of the cmd dir - [#2639](https://github.com/NuGet/Home/issues/2639)</span></span>

* <span data-ttu-id="9ceb2-152">버전 comparsion 코드 [#2632](https://github.com/NuGet/Home/issues/2632) 의 과도 한 할당</span><span class="sxs-lookup"><span data-stu-id="9ceb2-152">Excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="9ceb2-153">여러 인스턴스가 동시에 동일한 패키지를 설치 하려고 하면 이중 쓰기 [#2628](https://github.com/NuGet/Home/issues/2628) 발생 nuget.exe</span><span class="sxs-lookup"><span data-stu-id="9ceb2-153">Multiple instances of nuget.exe trying to install the same package in parallel causes a double write - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="9ceb2-154">다중 프로젝트 작업의 경우 종속성 정보가 캐시 되지 않습니다. [#2619](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-154">Dependency information is not cached for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="9ceb2-155">패키지 폴더를 먼저 확인 하지 않고 다운로드 패키지를 설치 및 업데이트 합니다. [#2618](https://github.com/NuGet/Home/issues/2618)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-155">Install and update download packages without checking the packages folder first - [#2618](https://github.com/NuGet/Home/issues/2618)</span></span>

* <span data-ttu-id="9ceb2-156">패키지 원본 목록이 비어 있는 경우 UI (NuGet 3.4. x)를 통해 패키지 원본을 추가할 수 없습니다. [#2617](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-156">If package source list is empty, cannot add package source via UI (NuGet 3.4.x) - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="9ceb2-157">디자인 타임 외관에 종속 된 패키지를 설치 하는 동안 오류가 발생 했습니다. [#2594](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-157">Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="9ceb2-158">PackageManager 콘솔에서 "All"을 설정 하 여 패키지를 설치 하면 첫 번째 소스- [#2557](https://github.com/NuGet/Home/issues/2557) 만 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ceb2-158">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="9ceb2-159">최신 beta ModernHttpClient 압축을 푸는 안 함- [#2518](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-159">Latest beta not unzipping ModernHttpClient - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="9ceb2-160">VS2015 3.4.1를 사용 하 여 시작할 때 크래시 방지- [#2419](https://github.com/NuGet/Home/issues/2419)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-160">VS2015 crash at startup with self-built NuGet 3.4.1 - [#2419](https://github.com/NuGet/Home/issues/2419)</span></span>

* <span data-ttu-id="9ceb2-161">업데이트 명령에 대해 확인 하는 경우에는 더 자세한 정보를 확인할 수 있습니다.- [#2418](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-161">Update command might be a bit more verbose if i ask it to be so... - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="9ceb2-162">로컬로 빌드된 VSIX는 CI 빌드와 동일한 Dll 및 파일을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ceb2-162">VSIX built locally should have the same DLLs and files as the CI build.</span></span><span data-ttu-id="9ceb2-163"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-163"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span></span>

* <span data-ttu-id="9ceb2-164">빌드- [#2396](https://github.com/NuGet/Home/issues/2396) 에서 NuGet 다운 그레이드 경고 수정</span><span class="sxs-lookup"><span data-stu-id="9ceb2-164">Fix NuGet downgrade warnings in the build - [#2396](https://github.com/NuGet/Home/issues/2396)</span></span>

* <span data-ttu-id="9ceb2-165">패키지 원본 인증 실패 (3 번)가 영원히 차단 됨- [#2362](https://github.com/NuGet/Home/issues/2362)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-165">Failing to authenticate package source (3 times) is blocked forever - [#2362](https://github.com/NuGet/Home/issues/2362)</span></span>

* <span data-ttu-id="9ceb2-166">패키지에 파일이 포함 된 경우 NoCache를 사용 하 여 nuget v 3.3 + 피드에서 패키지를 설치 하면 패키지 콘텐츠가 제대로 복원 되지 않습니다. `.nupkg` - [#2354](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-166">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="9ceb2-167">모든 패키지 소스와 함께 Nuget을 설치 했지만 원본에서 누락 된 패키지는 실패 [#2322](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-167">Nuget Install with All Package Sources, but package missing from 1 source, fails - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="9ceb2-168">[PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll! VisualStudio. VSMSBuildNuGetProjectSystem + \* l t; &gt; c__DisplayClass_0 + &lt; &lt; addreference &gt; b__ &gt; d. MoveNext- [#2285](https://github.com/NuGet/Home/issues/2285)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-168">[PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll!NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+\*lt;&gt;c__DisplayClass_0+&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)</span></span>

* <span data-ttu-id="9ceb2-169">단일 원본에서 권한 부여에 실패 하는 경우의 설치 차단- [#2034](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-169">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="9ceb2-170">`.nuspec`버전 범위는-IncludeReferencedProjects version- [#1983](https://github.com/NuGet/Home/issues/1983) 를 재정의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ceb2-170">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="9ceb2-171">Update-Package super 느림-"종속성 정보를 수집 하는 중"- [#1909](https://github.com/NuGet/Home/issues/1909)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-171">Update-Package super slow - "Attempting to gather dependencies information" - [#1909](https://github.com/NuGet/Home/issues/1909)</span></span>

* <span data-ttu-id="9ceb2-172">종속성을 일괄 업데이트할 때 NuGet 스텔스 다운 그레이드 패키지- [#1903](https://github.com/NuGet/Home/issues/1903)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-172">NuGet stealth downgrades package when batch updating its dependencies - [#1903](https://github.com/NuGet/Home/issues/1903)</span></span>

* <span data-ttu-id="9ceb2-173">nuget.exe 업데이트는 어셈블리의 강력한 이름 및 Private 특성을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ceb2-173">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="9ceb2-174"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-174"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="9ceb2-175">"DefaultPushSource"의 상대 파일 경로- [#1746](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-175">Relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="9ceb2-176">해결 프로그램 실패 메시지 개선- [#1373](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-176">Improve resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

* <span data-ttu-id="9ceb2-177">지정 된 원본에 없는 패키지와 함께 v3의 업데이트-패키지가 실패 함- [#1013](https://github.com/NuGet/Home/issues/1013)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-177">update-package in v3 fails with packages not in the specified source - [#1013](https://github.com/NuGet/Home/issues/1013)</span></span>

* <span data-ttu-id="9ceb2-178">패키지 원본에 대 한 상대 경로를 사용 하는 것은- [#865](https://github.com/NuGet/Home/issues/865)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-178">Using relative paths for package sources is problematic to use - [#865](https://github.com/NuGet/Home/issues/865)</span></span>

* <span data-ttu-id="9ceb2-179">낮은 버전 요구 사항으로 간접 종속성이 이미 존재 하는 경우 NUPKG에서 종속성이 누락 되었습니다.- [#759](https://github.com/NuGet/Home/issues/759)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-179">Missing dependency in NUPKG-file generated from project if indirect dependency already exists with a lower version requirement - [#759](https://github.com/NuGet/Home/issues/759)</span></span>

* <span data-ttu-id="9ceb2-180">프로젝트를 삭제 하면 해당 UI 창이 닫히지만 프로젝트의 이름을 바꾸면 UI 창의 이름이 바뀌지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9ceb2-180">Deleting a project closes corresponding UI window, but, renaming a project does not rename the UI window.</span></span> <span data-ttu-id="9ceb2-181">PMC는 프로젝트 이름 바꾸기 및 프로젝트 제거 이벤트를 수신 합니다.- [#670](https://github.com/NuGet/Home/issues/670)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-181">Note that PMC listens to project rename and project remove events - [#670](https://github.com/NuGet/Home/issues/670)</span></span>

* <span data-ttu-id="9ceb2-182">[Willow 웹 작업] Razor v3 WSP 중단을 만드는 중- [#3241](https://github.com/NuGet/Home/issues/3241)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-182">[Willow Web Workload] Creating Razor v3 WSP hangs - [#3241](https://github.com/NuGet/Home/issues/3241)</span></span>

* <span data-ttu-id="9ceb2-183">"패키지에 여러 nuspec 파일이 포함 되어 있습니다."와 함께 특정 패키지의 설치/복원이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ceb2-183">Install/restore of a particular package fails with "Package contains multiple nuspec files."</span></span><span data-ttu-id="9ceb2-184"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-184"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="9ceb2-185">소문자 Id & `packages.config` 시나리오- [#3209](https://github.com/NuGet/Home/issues/3209)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-185">Lowercase IDs & `packages.config` scenarios - [#3209](https://github.com/NuGet/Home/issues/3209)</span></span>

* <span data-ttu-id="9ceb2-186">[3.5-beta2] 패키지 복원이 "레거시" 패키지를 복원 하지 못함- [#3208](https://github.com/NuGet/Home/issues/3208)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-186">[3.5-beta2] Package restore fails to restore "legacy" packages - [#3208](https://github.com/NuGet/Home/issues/3208)</span></span>

* <span data-ttu-id="9ceb2-187">nuget 팩은 [#3203](https://github.com/NuGet/Home/issues/3203) 에 관계 없이 콘텐츠 폴더에 .tt 파일을 강제로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ceb2-187">nuget pack forcefully adds .tt files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="9ceb2-188">ASP.NET 웹 앱의 package는 file: source- [#3194](https://github.com/NuGet/Home/issues/3194) 와 관련 된 경고를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ceb2-188">update-package of ASP.NET web app generates warning related to file: source - [#3194](https://github.com/NuGet/Home/issues/3194)</span></span>

* <span data-ttu-id="9ceb2-189">JSON 파일에 pack 옵션과 소유자가 없는 경우 nuget pack .csproj (with `project.json` )이 충돌 합니다. [#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-189">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="9ceb2-190">용 nuget 팩은 `project.json` 요약, 저자, 소유자 등의 패키지 옵션 태그를 무시 [#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-190">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="9ceb2-191">NullReferenceException를 통해 System.resources.resourcemanager.getstream- [#3160](https://github.com/NuGet/Home/issues/3160)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-191">NullReferenceException via NuGet.Packaging.PhysicalPackageFile.GetStream - [#3160](https://github.com/NuGet/Home/issues/3160)</span></span>

* <span data-ttu-id="9ceb2-192">NuGet 팩은 #3145 출력에서 종속성을 무시 `.nuspec` 합니다. `project.json`  -  [](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-192">NuGet pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="9ceb2-193">Rollback을 사용 하 여 여러 패키지를 업데이트 하면 프로젝트가 중단 된 상태로 남게 됩니다 [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-193">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="9ceb2-194">모든 아래 ContentFiles는 netstandard.library 프로젝트에 추가 되지 않습니다. [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-194">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="9ceb2-195">.Net Standard를 올바르게 대상으로 하는 라이브러리를 패키지할 수 없습니다. [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-195">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="9ceb2-196">VS2015 및 Dev15에서 파일 > 새 프로젝트-> 클래스 라이브러리 (이식 가능) 프로젝트가 실패 [#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-196">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="9ceb2-197">nuGet 오류-1.0.0-\*은 올바른 버전 문자열이 아닙니다. [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-197">nuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="9ceb2-198">Find-Package 표시 되지 않지만 Install-Package 작동 [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-198">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="9ceb2-199">Dev15- [#3061](https://github.com/NuGet/Home/issues/3061) 에서 "Install-Package jquery. validation" 오류가 발생 하는 경우 오류</span><span class="sxs-lookup"><span data-stu-id="9ceb2-199">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="9ceb2-200">xproj의 nuget 팩은 잘못 된 대상 경로를 기본적으로 [#3060](https://github.com/NuGet/Home/issues/3060)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-200">nuget pack of xproj is defaulting to invalid target path - [#3060](https://github.com/NuGet/Home/issues/3060)</span></span>

* <span data-ttu-id="9ceb2-201">NuGet 버전을 사용 하는 VS 2015 업데이트 3이 설치 된 경우 3.5.0 오류 발생- [#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-201">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="9ceb2-202">"packages.config에서 차단 됨" `project.json` (UWP, a. a 빌드 통합) 프로젝트- [#3046](https://github.com/NuGet/Home/issues/3046)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-202">"Blocked by packages.config" in `project.json` (UWP, a.k.a build integrated) project - [#3046](https://github.com/NuGet/Home/issues/3046)</span></span>

* <span data-ttu-id="9ceb2-203">빌드 스크립트에 의해 설치 된 dotnet cli를 공식 미리 보기 2 빌드용 미리 보기 2-003121)로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ceb2-203">update dotnet cli installed by build script to preview2-003121, which is the official preview2 build.</span></span><span data-ttu-id="9ceb2-204"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-204"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span></span>

* <span data-ttu-id="9ceb2-205">패키지 관리자 UI: 패키지를 업데이트 한 후 새 버전을 표시 하지 않습니다.- [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-205">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="9ceb2-206">-3.5.0에서 명령줄의 ApiKey를 읽고 보내지 않습니다.-beta- [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-206">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="9ceb2-207">잘못 된 문자열: 안정적인 패키지 릴리스가 시험판 종속성에 포함 되어서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ceb2-207">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="9ceb2-208"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-208"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="9ceb2-209">OptimizedZipPackage cache는 빈 폴더를 남겨 둡니다.- [#3029](https://github.com/NuGet/Home/issues/3029)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-209">OptimizedZipPackage cache leaves empty folders - [#3029](https://github.com/NuGet/Home/issues/3029)</span></span>

* <span data-ttu-id="9ceb2-210">PCL (고 net46 및 windows 10) 프로젝트 만들기 NullRef 예외</span><span class="sxs-lookup"><span data-stu-id="9ceb2-210">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="9ceb2-211"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-211"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="9ceb2-212">상위 버전이 allowedVersions 제약 조건에 의해 제한 되는 경우 Nuget 업데이트는 정보 메시지를 제공 해야 [#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-212">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="9ceb2-213">Nuget v3 복원 문제- [#2891](https://github.com/NuGet/Home/issues/2891)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-213">Nuget v3 restore issues - [#2891](https://github.com/NuGet/Home/issues/2891)</span></span>

* <span data-ttu-id="9ceb2-214">여러 소스가 포함 된 자격 증명 공급자를 사용 하는 경우 자격 증명 플러그 인이 종료 되었습니다. 오류 1/패키지 다운로드 오류- [#2885](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-214">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="9ceb2-215">`project.json` 변경 내용이 없는 경우 nuget 복원으로 인해 다시 컴파일이 발생 [#2817](https://github.com/NuGet/Home/issues/2817)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-215">`project.json` nuget restore causes recompilation when nothing changed - [#2817](https://github.com/NuGet/Home/issues/2817)</span></span>

* <span data-ttu-id="9ceb2-216">기호 패키지는 설치 또는 업데이트- [#2807](https://github.com/NuGet/Home/issues/2807) 에서 사용 하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ceb2-216">Symbols packages should not ever be used in install or update - [#2807](https://github.com/NuGet/Home/issues/2807)</span></span>

* <span data-ttu-id="9ceb2-217">VS는 repositoryPath (nuget.exe)에서 환경 변수를 지원 하지 않습니다 [#2763](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-217">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="9ceb2-218">내게 필요한 [#2745](https://github.com/NuGet/Home/issues/2745) 옵션에 대 한 패키지 관리자 UI에서 레이블이 없는 UIElements 레이블</span><span class="sxs-lookup"><span data-stu-id="9ceb2-218">Label the unlabeled UIElements in Package Manager UI for accessibility - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="9ceb2-219">하이픈이 있는 이식 가능한 프레임 워크는 거부 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ceb2-219">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="9ceb2-220"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-220"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="9ceb2-221">NuGet 패키지 관리자는 패키지 세부 정보의 옵션 목록이에 적용 되지 않는다는 것을 명확 하 게 지정 해야 `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-221">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="9ceb2-222">nuget.exe push/delete는 API 키를 사용 하지 않습니다. [#2627](https://github.com/NuGet/Home/issues/2627)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-222">nuget.exe push/delete won't use API Key  - [#2627](https://github.com/NuGet/Home/issues/2627)</span></span>

* <span data-ttu-id="9ceb2-223">잠금 파일에서 잠긴 속성을 제거 합니다.- [#2379](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-223">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="9ceb2-224">' 추가 제약 조건을 사용 하 여 NuGet 3.3.0 업데이트가 실패 합니다. packages.config에 정의 되어 있으므로이 작업을 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9ceb2-224">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="9ceb2-225"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-225"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="9ceb2-226">존재 하지 않는 로컬 원본에서 패키지를 설치 하면 가짜 메시지가 throw 됩니다. [#1674](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-226">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="9ceb2-227">"업그레이드 가능" 필터는 버전 제약 조건을 위반 하는 업그레이드를 표시 합니다. [#1094](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-227">"Upgrade available" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

* <span data-ttu-id="9ceb2-228">네이티브 패키지를 업데이트할 수 없습니다. [#1291](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-228">Unable to update native packages - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>


## <a name="features"></a><span data-ttu-id="9ceb2-229">기능</span><span class="sxs-lookup"><span data-stu-id="9ceb2-229">Features</span></span>

* <span data-ttu-id="9ceb2-230">NuGet에서 추가 된 참조에 대해 CopyLocal을 false로 설정 하도록 지원 [#329](https://github.com/NuGet/Home/issues/329)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-230">Support setting CopyLocal to false on references added by NuGet - [#329](https://github.com/NuGet/Home/issues/329)</span></span>

* <span data-ttu-id="9ceb2-231">MSBuild 15- [#1937](https://github.com/NuGet/Home/issues/1937) 에 대 한 nuget.exe 지원</span><span class="sxs-lookup"><span data-stu-id="9ceb2-231">nuget.exe support for MSBuild 15 - [#1937](https://github.com/NuGet/Home/issues/1937)</span></span>

* <span data-ttu-id="9ceb2-232">에 대 한 Pack 지원.`csproj`</span><span class="sxs-lookup"><span data-stu-id="9ceb2-232">Pack support for .`csproj`</span></span><span data-ttu-id="9ceb2-233"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-233"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span></span>

* <span data-ttu-id="9ceb2-234">실행 중인 사용자 작업이 있을 때 사용자 작업을 사용 하지 않도록 설정- [#1440](https://github.com/NuGet/Home/issues/1440)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-234">Disable user action when there are user actions being executed - [#1440](https://github.com/NuGet/Home/issues/1440)</span></span>

* <span data-ttu-id="9ceb2-235">NuGet은 #2782에 대 한 지원을 추가 해야 합니다. `runtimes/{rid}/nativeassets/{txm}/`  -  [](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-235">NuGet should add support for `runtimes/{rid}/nativeassets/{txm}/` - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>

* <span data-ttu-id="9ceb2-236">NuGet 2.x (이미 2.x에 있는)에 누락 된 호환성 framework가 추가 되었습니다.- [#2720](https://github.com/NuGet/Home/issues/2720)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-236">Add framework compatibilities missing in NuGet 2.x (which are already in 3.x) - [#2720](https://github.com/NuGet/Home/issues/2720)</span></span>

* <span data-ttu-id="9ceb2-237">대체 패키지 폴더에 대 한 지원- [#2899](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-237">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="9ceb2-238">도구 패키지를 지원 하기 위한 패키지 형식의 개념 디자인 및 구현- [#2476](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-238">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="9ceb2-239">API를 추가 하 여 전역 패키지 폴더에 대 한 경로를 가져옵니다.- [#2403](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-239">Add an API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="9ceb2-240">SemVer 2.0.0 in pack- [#3356](https://github.com/NuGet/Home/issues/3356) 사용</span><span class="sxs-lookup"><span data-stu-id="9ceb2-240">Enable SemVer 2.0.0 in pack - [#3356](https://github.com/NuGet/Home/issues/3356)</span></span>

## <a name="dcrs"></a><span data-ttu-id="9ceb2-241">DCR</span><span class="sxs-lookup"><span data-stu-id="9ceb2-241">DCRs</span></span>

* <span data-ttu-id="9ceb2-242">nuget.exe 푸시 시간 제한 매개 변수가 작동 하지 않습니다.- [#2785](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-242">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="9ceb2-243">패키지 설명 텍스트는 선택 가능 해야 합니다. [#1769](https://github.com/NuGet/Home/issues/1769)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-243">Package Description text should be selectable - [#1769](https://github.com/NuGet/Home/issues/1769)</span></span>

* <span data-ttu-id="9ceb2-244">nuget.exe를 사용 하 `.props` 여 `.targets` 프로젝트에 대 한 및 파일을 생성 `.nuproj` [#2711](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-244">Enable nuget.exe to produce `.props` and `.targets` files for `.nuproj` projects [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="9ceb2-245">확장성 API를 추가 하 여 프레임 워크를 가져오기와 비교 [#2633](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-245">Add extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="9ceb2-246">#2486 사용 시 종속성 옵션 숨기기 `project.json`  -  [](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-246">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="9ceb2-247">자세한 출력에서 nuget.exe 버전 헤더를 출력 합니다. [#1887](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-247">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="9ceb2-248">NuGet은 dotnet tfm 기반 PCL에서 업그레이드/설치 하는 데 [#3138](https://github.com/NuGet/Home/issues/3138) 문제가 발생할 수 있음을 사용자에 게 알릴 필요가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ceb2-248">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="9ceb2-249">Project w/tfm = "dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137) 에 대 한 잘못 된 설치/업그레이드 경고</span><span class="sxs-lookup"><span data-stu-id="9ceb2-249">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="9ceb2-250">ReShaper 및 NuGet 업데이트- [#3044](https://github.com/NuGet/Home/issues/3044) 의 성능 문제 해결</span><span class="sxs-lookup"><span data-stu-id="9ceb2-250">Fix performance issues with ReShaper and NuGet for Update - [#3044](https://github.com/NuGet/Home/issues/3044)</span></span>

* <span data-ttu-id="9ceb2-251">Netcoreapp11 및 netstandard17 지원 추가- [#2998](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-251">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="9ceb2-252">토큰 교체에 AssemblyMetadata 특성 활용 `.nuspec` - [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="9ceb2-252">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>
