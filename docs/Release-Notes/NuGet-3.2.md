---
title: "NuGet 3.2 릴리스 정보 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 70316f35-f046-4f72-98e0-736de172e918
description: "알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr를 포함 하 여 NuGet 3.2에 대 한 릴리스 정보입니다."
keywords: "NuGet 3.2 릴리스 정보, 버그 수정, 알려진 문제, 추가 기능을 Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 551a54482f83803a2e5e5b6ba57a1bf3dd06db8a
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/05/2018
---
# <a name="nuget-32-release-notes"></a><span data-ttu-id="0ecaa-104">NuGet 3.2 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="0ecaa-104">NuGet 3.2 Release Notes</span></span>

<span data-ttu-id="0ecaa-105">[NuGet 3.2 RC 릴리스 정보](../release-notes/nuget-3.2-RC.md) | [NuGet 3.2.1 릴리스 정보](../release-notes/nuget-3.2.1.md)</span><span class="sxs-lookup"><span data-stu-id="0ecaa-105">[NuGet 3.2-RC Release Notes](../release-notes/nuget-3.2-RC.md) | [NuGet 3.2.1 Release Notes](../release-notes/nuget-3.2.1.md)</span></span>

<span data-ttu-id="0ecaa-106">NuGet 3.2 릴리스된 개선 사항 및는 3.1.1에 대 한 수정 된 컬렉션으로 2015 년 9 월 16 일 놓은 둘 다에서 사용할 수 [dist.nuget.org](http://dist.nuget.org/index.html) 및 [Visual Studio 갤러리](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2015)합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecaa-106">NuGet 3.2 was released September 16, 2015 as a collection of improvements and fixes for the 3.1.1 release and is available from both [dist.nuget.org](http://dist.nuget.org/index.html) and the [Visual Studio Gallery](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2015).</span></span>

## <a name="new-features"></a><span data-ttu-id="0ecaa-107">새 기능</span><span class="sxs-lookup"><span data-stu-id="0ecaa-107">New Features</span></span>

* <span data-ttu-id="0ecaa-108">동일한 폴더에 거주 하는 프로젝트를 서로 다른 점이 이제 `project.json` 각 프로젝트에 해당 폴더의 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="0ecaa-108">Projects that live in the same folder can now have different `project.json` files in that folder specific to each project.</span></span>  <span data-ttu-id="0ecaa-109">각 프로젝트에 대 한 이름을 `project.json` 파일 `{ProjectName}.project.json` NuGet 각 프로젝트에 대 한 해당 구성에 우선 순위를 적절 하 게 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ecaa-109">For each project, name the `project.json` file `{ProjectName}.project.json` and NuGet will give preference to that configuration for each project appropriately.</span></span>  <span data-ttu-id="0ecaa-110">이 Windows 10 도구 v 1.1이 설치를 지원만 [1102](https://github.com/NuGet/Home/issues/1102)</span><span class="sxs-lookup"><span data-stu-id="0ecaa-110">This is only supported with Windows 10 Tools v1.1 installed -  [1102](https://github.com/NuGet/Home/issues/1102)</span></span>
* <span data-ttu-id="0ecaa-111">NuGet 클라이언트에 사용 되는 공유 전역 패키지 폴더의 위치를 지정 하는 전역 NUGET_PACKAGES 환경 변수를 지정 하는 지원 `project.json` Windows 10 도구 v 1.1 사용 하 여 프로젝트를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecaa-111">NuGet clients support specifying a global NUGET_PACKAGES environment variable to specify the location of the shared global packages folder used in `project.json` managed projects with Windows 10 tools v1.1.</span></span>

## <a name="command-line-updates"></a><span data-ttu-id="0ecaa-112">명령줄 업데이트</span><span class="sxs-lookup"><span data-stu-id="0ecaa-112">Command-line updates</span></span>

<span data-ttu-id="0ecaa-113">이 첫 번째 버전의 NuGet v3 서버를 지 원하는 nuget.exe 클라이언트 및 관리 되는 프로젝트에 대 한 패키지를 복원 하는 `project.json` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="0ecaa-113">This is the first version of the nuget.exe client that supports the NuGet v3 servers and restoring packages for projects managed with a `project.json` file.</span></span>

<span data-ttu-id="0ecaa-114">다양 한 클라이언트와 상호 작용을 개선 하기 위해이 릴리스에서 주소가 지정 된 인증 된 피드 문제가 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="0ecaa-114">There were a number of authenticated feed issues that were addressed in this release to improve interactions with the client.</span></span>

* <span data-ttu-id="0ecaa-115">설치 / 복원 상호 작용-인증 된 피드를 초기 요청에 대 한 자격 증명을 제출만 [1300](https://github.com/NuGet/Home/issues/1300), [456](https://github.com/NuGet/Home/issues/456)</span><span class="sxs-lookup"><span data-stu-id="0ecaa-115">Install / restore interactions only submit credentials for the initial request to the authenticated feed - [1300](https://github.com/NuGet/Home/issues/1300), [456](https://github.com/NuGet/Home/issues/456)</span></span>
* <span data-ttu-id="0ecaa-116">푸시 명령에서 구성-자격 증명을 해결 되지 않으면 [1248](https://github.com/NuGet/Home/issues/1248)</span><span class="sxs-lookup"><span data-stu-id="0ecaa-116">Push command does not resolve credentials from configuration - [1248](https://github.com/NuGet/Home/issues/1248)</span></span>
* <span data-ttu-id="0ecaa-117">사용자 에이전트 및 헤더 통계 추적-에 도움이 되도록 NuGet 리포지토리에서에 제출 이제 [929](https://github.com/NuGet/Home/issues/929)</span><span class="sxs-lookup"><span data-stu-id="0ecaa-117">User agent and headers are now submitted to NuGet repositories to help with statistics tracking - [929](https://github.com/NuGet/Home/issues/929)</span></span>

<span data-ttu-id="0ecaa-118">원격 NuGet 리포지토리를 사용 하는 동안 네트워크 오류 처리 하기 위해 향상 된 기능이 다양을 내렸습니다.</span><span class="sxs-lookup"><span data-stu-id="0ecaa-118">We made a number of improvements to better handle network failures while attempting to work with a remote NuGet repository:</span></span>

* <span data-ttu-id="0ecaa-119">-원격 피드에 연결할 수 없는 경우 오류 메시지가 개선 [1238](https://github.com/NuGet/Home/issues/1238)</span><span class="sxs-lookup"><span data-stu-id="0ecaa-119">Improved error messages when unable to connect to remote feeds - [1238](https://github.com/NuGet/Home/issues/1238)</span></span>
* <span data-ttu-id="0ecaa-120">제대로-에 오류 조건이 발생 하는 경우 1을 반환 하려면 NuGet 복원 명령을 수정 [1186](https://github.com/NuGet/Home/issues/1186)</span><span class="sxs-lookup"><span data-stu-id="0ecaa-120">Corrected NuGet restore command to properly return a 1 when an error condition occurs - [1186](https://github.com/NuGet/Home/issues/1186)</span></span>
* <span data-ttu-id="0ecaa-121">이제 네트워크 연결을 다시 시도 최대 HTTP 5xx 오류-시 5 회 시도 대 한 모든 200ms [1120](https://github.com/NuGet/Home/issues/1120)</span><span class="sxs-lookup"><span data-stu-id="0ecaa-121">Now retrying network connections every 200ms for a maximum of 5 attempts in the case of HTTP 5xx failures - [1120](https://github.com/NuGet/Home/issues/1120)</span></span>
* <span data-ttu-id="0ecaa-122">서버 리디렉션 응답을 처리 중 밀어넣기 명령-향상 된 [1051](https://github.com/NuGet/Home/issues/1051)</span><span class="sxs-lookup"><span data-stu-id="0ecaa-122">Improved handling of server redirect responses during a push command - [1051](https://github.com/NuGet/Home/issues/1051)</span></span>
* <span data-ttu-id="0ecaa-123">`nuget install -source`이제-인수로 Nuget.Config에서 URL 이나 리포지토리 이름을 지원 [1046](https://github.com/NuGet/Home/issues/1046)</span><span class="sxs-lookup"><span data-stu-id="0ecaa-123">`nuget install -source` now supports either URL or repository name from Nuget.Config as an argument - [1046](https://github.com/NuGet/Home/issues/1046)</span></span>
* <span data-ttu-id="0ecaa-124">누락 된 패키지를 복원 하는 동안 저장소에 배치 되지 않은 경고 대신 오류로 보고 이제 [1038](https://github.com/NuGet/Home/issues/1038)</span><span class="sxs-lookup"><span data-stu-id="0ecaa-124">Missing packages that were not located on a repository during a restore are now reported as errors instead of warnings [1038](https://github.com/NuGet/Home/issues/1038)</span></span>
* <span data-ttu-id="0ecaa-125">Unix/Linux 시나리오-\r\n multipartwebrequest 처리 수정 [776](https://github.com/NuGet/Home/issues/776)</span><span class="sxs-lookup"><span data-stu-id="0ecaa-125">Corrected multipartwebrequest handling of \r\n for Unix/Linux scenarios - [776](https://github.com/NuGet/Home/issues/776)</span></span>

<span data-ttu-id="0ecaa-126">다양 한 명령 사용 하 여 문제를 수정 프로그램의 여러 가지:</span><span class="sxs-lookup"><span data-stu-id="0ecaa-126">There are a number of fixes to issues with various commands:</span></span>

* <span data-ttu-id="0ecaa-127">Push 명령이 수행 하는 GET-패키지 소스에 대해 PUT 하기 전에 더 이상 [1237](https://github.com/NuGet/Home/issues/1237)</span><span class="sxs-lookup"><span data-stu-id="0ecaa-127">Push command no longer does a GET before a PUT against a package source - [1237](https://github.com/NuGet/Home/issues/1237)</span></span>
* <span data-ttu-id="0ecaa-128">버전 번호를 더 이상 반복 하는 목록 표시 명령 [1185](https://github.com/NuGet/Home/issues/1185)</span><span class="sxs-lookup"><span data-stu-id="0ecaa-128">List command no longer repeats version numbers - [1185](https://github.com/NuGet/Home/issues/1185)</span></span>
* <span data-ttu-id="0ecaa-129">팩-빌드 인수와 함께 이제 제대로 지원 C# 6.0- [1107](https://github.com/NuGet/Home/issues/1107)</span><span class="sxs-lookup"><span data-stu-id="0ecaa-129">Pack with the -build argument now properly supports C# 6.0 - [1107](https://github.com/NuGet/Home/issues/1107)</span></span>
* <span data-ttu-id="0ecaa-130">F # 프로젝트를 압축할 수정 된 문제는 Visual Studio 2015-를 사용 하 여 빌드한 [1048](https://github.com/NuGet/Home/issues/1048)</span><span class="sxs-lookup"><span data-stu-id="0ecaa-130">Corrected issues attempting to pack an F# project built with Visual Studio 2015 - [1048](https://github.com/NuGet/Home/issues/1048)</span></span>
* <span data-ttu-id="0ecaa-131">패키지는 이미 존재-때 지금 아니요 ops 복원 [1040](https://github.com/NuGet/Home/issues/1040)</span><span class="sxs-lookup"><span data-stu-id="0ecaa-131">Restore now no-ops when packages already exist - [1040](https://github.com/NuGet/Home/issues/1040)</span></span>
* <span data-ttu-id="0ecaa-132">경우 향상 된 오류 메시지를 `packages.config` 파일 형식이 잘못 되었습니다- [1034](https://github.com/NuGet/Home/issues/1034)</span><span class="sxs-lookup"><span data-stu-id="0ecaa-132">Improved error messages when `packages.config` file is malformed - [1034](https://github.com/NuGet/Home/issues/1034)</span></span>
* <span data-ttu-id="0ecaa-133">상대 경로-작업-SolutionDirectory 스위치와 함께 복원 명령을 수정 [992](https://github.com/NuGet/Home/issues/992)</span><span class="sxs-lookup"><span data-stu-id="0ecaa-133">Corrected restore command with -SolutionDirectory switch to work with relative paths - [992](https://github.com/NuGet/Home/issues/992)</span></span>
* <span data-ttu-id="0ecaa-134">솔루션의 전반적인 업데이트-지원 하도록 업데이트 명령을 향상 [924](https://github.com/NuGet/Home/issues/924)</span><span class="sxs-lookup"><span data-stu-id="0ecaa-134">Improved Updated command to support solution-wide update - [924](https://github.com/NuGet/Home/issues/924)</span></span>

<span data-ttu-id="0ecaa-135">이 릴리스에서 해결 된 문제의 전체 목록은 NuGet GitHub에서 있습니다 [명령줄 마일스 톤](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate)합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecaa-135">A complete list of issues addressed in this release can be found in the NuGet GitHub [Command-Line milestone](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate).</span></span>

## <a name="visual-studio-extension-updates"></a><span data-ttu-id="0ecaa-136">Visual Studio 확장명 업데이트</span><span class="sxs-lookup"><span data-stu-id="0ecaa-136">Visual Studio extension updates</span></span>

### <a name="new-features-in-visual-studio"></a><span data-ttu-id="0ecaa-137">Visual Studio의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="0ecaa-137">New Features in Visual Studio</span></span>

* <span data-ttu-id="0ecaa-138">패키지는 솔루션을 구축 하지 않고도 복원할 수를 허용 하는 솔루션 노드에서 솔루션 탐색기에 새로운 상황에 맞는 메뉴 항목이 추가 되었습니다 ([1274](https://github.com/NuGet/Home/issues/1274)).</span><span class="sxs-lookup"><span data-stu-id="0ecaa-138">A new context menu item was added to the Solution Explorer on the solution node that allows packages to be restored without building the solution ([1274](https://github.com/NuGet/Home/issues/1274)).</span></span>

![새 '패키지를 복원' 상황에 맞는 메뉴 항목](./media/NuGet-3.2/newContextMenu.png)

### <a name="updates-and-fixes-in-visual-studio"></a><span data-ttu-id="0ecaa-140">업데이트 및 Visual Studio에서 수정</span><span class="sxs-lookup"><span data-stu-id="0ecaa-140">Updates and Fixes in Visual Studio</span></span>

<span data-ttu-id="0ecaa-141">인증 된 피드에 대 한 수정 사항 롤업 였으며도 확장에서 해결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ecaa-141">The fixes for authenticated feeds were rolled up and addressed in the extension as well.</span></span>  <span data-ttu-id="0ecaa-142">다음 인증 항목 확장에도 해결 않은:</span><span class="sxs-lookup"><span data-stu-id="0ecaa-142">The following authentication items were also addressed in the extension:</span></span>

* <span data-ttu-id="0ecaa-143">이제 피드를 적절 하 게 인증 NuGet v3를 올바르게 처리 하는 방법 대신 v2 피드-인증 된 것으로 [1216](https://github.com/NuGet/Home/issues/1216)</span><span class="sxs-lookup"><span data-stu-id="0ecaa-143">Now correctly treating NuGet v3 authenticated feeds properly, instead of as v2 authenticated feeds - [1216](https://github.com/NuGet/Home/issues/1216)</span></span>
* <span data-ttu-id="0ecaa-144">사용 하 여 프로젝트에서 인증 자격 증명에 대 한 수정 된 요청 `project.json` 및 v2 피드-와 통신 [1082](https://github.com/NuGet/Home/issues/1082)</span><span class="sxs-lookup"><span data-stu-id="0ecaa-144">Corrected request for authentication credentials in projects using `project.json` and communicating with v2 feeds - [1082](https://github.com/NuGet/Home/issues/1082)</span></span>

<span data-ttu-id="0ecaa-145">네트워크 연결에 Visual Studio의 사용자 인터페이스에 영향을 받는 하 고 다음 수정 프로그램으로이 주소를 지정 했습니다.</span><span class="sxs-lookup"><span data-stu-id="0ecaa-145">Network connectivity had affected the user interface in Visual Studio, and we addressed this with the following fixes:</span></span>

* <span data-ttu-id="0ecaa-146">패키지 버전-컴퓨터의 로컬 캐시에 유지 관리를 향상 [1096](https://github.com/NuGet/Home/issues/1096)</span><span class="sxs-lookup"><span data-stu-id="0ecaa-146">Improved the maintenance of the local cache of package versions - [1096](https://github.com/NuGet/Home/issues/1096)</span></span>
* <span data-ttu-id="0ecaa-147">피드를-v2 피드로 처리 하려는 시도가 더 이상 v3에 연결할 때 실패 동작을 변경 [1253](https://github.com/NuGet/Home/issues/1253)</span><span class="sxs-lookup"><span data-stu-id="0ecaa-147">Changed the failure behavior when connecting to a v3 feed to no longer attempt to treat it as a v2 feed - [1253](https://github.com/NuGet/Home/issues/1253)</span></span>
* <span data-ttu-id="0ecaa-148">여러 패키지 소스가-포함 된 패키지를 설치할 때 설치 오류를 방지 이제 [1183](https://github.com/NuGet/Home/issues/1183)</span><span class="sxs-lookup"><span data-stu-id="0ecaa-148">Now preventing install failures when installing a package with multiple package sources - [1183](https://github.com/NuGet/Home/issues/1183)</span></span>

<span data-ttu-id="0ecaa-149">빌드 작업와의 상호 작용의 처리를 개선 했습니다.</span><span class="sxs-lookup"><span data-stu-id="0ecaa-149">We improved handling of interactions with build operations:</span></span>

* <span data-ttu-id="0ecaa-150">단일 프로젝트 실패-에 대 한 패키지를 복원 하는 경우 프로젝트를 작성을 이제 [1169](https://github.com/NuGet/Home/issues/1169)</span><span class="sxs-lookup"><span data-stu-id="0ecaa-150">Now continuing to build projects if restoring packages for a single project fails - [1169](https://github.com/NuGet/Home/issues/1169)</span></span>
* <span data-ttu-id="0ecaa-151">솔루션 다시 빌드-강제로 패키지를 설치 하면 솔루션의 다른 프로젝트에 의존 하는 프로젝트에 [981](https://github.com/NuGet/Home/issues/981)</span><span class="sxs-lookup"><span data-stu-id="0ecaa-151">Installing a package into a project that is depended on by another project in the solution forces a solution rebuild - [981](https://github.com/NuGet/Home/issues/981)</span></span>
* <span data-ttu-id="0ecaa-152">제대로 변경 내용을 롤백하고 프로젝트-실패 한 패키지 설치를 수정 했습니다. [1265](https://github.com/NuGet/Home/issues/1265)</span><span class="sxs-lookup"><span data-stu-id="0ecaa-152">Corrected failed package installs to properly rollback changes to a project - [1265](https://github.com/NuGet/Home/issues/1265)</span></span>
* <span data-ttu-id="0ecaa-153">실수로 제거 수정 된 `developmentDependency` 특성에서 패키지에 `packages.config`  -  [1263](https://github.com/NuGet/Home/issues/1263)</span><span class="sxs-lookup"><span data-stu-id="0ecaa-153">Corrected inadvertent removal of the `developmentDependency` attribute on a package in `packages.config` - [1263](https://github.com/NuGet/Home/issues/1263)</span></span>
* <span data-ttu-id="0ecaa-154">에 대 한 호출이 `install.ps1` 적절 한 생깁니다 `$package.AssemblyReferences` -전달 된 개체가 [1245](https://github.com/NuGet/Home/issues/1245)</span><span class="sxs-lookup"><span data-stu-id="0ecaa-154">Calls to `install.ps1` now have a proper `$package.AssemblyReferences` object passed - [1245](https://github.com/NuGet/Home/issues/1245)</span></span>
* <span data-ttu-id="0ecaa-155">-잘못 된 상태에는 프로젝트를 UWP 프로젝트에서 패키지의 제거 인해 더 이상 [1128](https://github.com/NuGet/Home/issues/1128)</span><span class="sxs-lookup"><span data-stu-id="0ecaa-155">No longer preventing uninstalls of packages in UWP projects while the project is in a bad state - [1128](https://github.com/NuGet/Home/issues/1128)</span></span>
* <span data-ttu-id="0ecaa-156">혼합 되어 있는 솔루션 `packages.config` 및 `project.json` 프로젝트가 제대로 두 번째 요구 하지 않고 빌드 이제 빌드 작업- [1122](https://github.com/NuGet/Home/issues/1122)</span><span class="sxs-lookup"><span data-stu-id="0ecaa-156">Solutions containing a mix of `packages.config` and `project.json` projects are now properly built without requiring a second build operation - [1122](https://github.com/NuGet/Home/issues/1122)</span></span>
* <span data-ttu-id="0ecaa-157">링크 되는지 아니면 다른 폴더-에 있는 경우 app.config 파일을 제대로 찾기 [1111](https://github.com/NuGet/Home/issues/1111), [894](https://github.com/NuGet/Home/issues/894)</span><span class="sxs-lookup"><span data-stu-id="0ecaa-157">Properly locating app.config files if they are linked or located in a different folder - [1111](https://github.com/NuGet/Home/issues/1111), [894](https://github.com/NuGet/Home/issues/894)</span></span>
* <span data-ttu-id="0ecaa-158">UWP 프로젝트에서는 이제-목록에 없는 패키지를 설치할 수 [1109](https://github.com/NuGet/Home/issues/1109)</span><span class="sxs-lookup"><span data-stu-id="0ecaa-158">UWP projects can now install unlisted packages - [1109](https://github.com/NuGet/Home/issues/1109)</span></span>
* <span data-ttu-id="0ecaa-159">패키지를 복원이 허용 되지-저장 된 상태의 솔루션이 없을 때 [1081](https://github.com/NuGet/Home/issues/1081)</span><span class="sxs-lookup"><span data-stu-id="0ecaa-159">Package restore is now allowed while a solution is not in a saved state - [1081](https://github.com/NuGet/Home/issues/1081)</span></span>

<span data-ttu-id="0ecaa-160">파일 수정 된 구성에 대 한 업데이트를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ecaa-160">Handling updates to configuration files were corrected:</span></span>

* <span data-ttu-id="0ecaa-161">이후 빌드 패키지에서 배달 대상 파일을 제거 하는 더 이상는 `project.json` 관리 되는 프로젝트- [1288](https://github.com/NuGet/Home/issues/1288)</span><span class="sxs-lookup"><span data-stu-id="0ecaa-161">No longer removing a targets file delivered from a package on subsequent builds of a `project.json` managed project - [1288](https://github.com/NuGet/Home/issues/1288)</span></span>
* <span data-ttu-id="0ecaa-162">ASP.NET 5 솔루션 빌드-중 Nuget.Config 파일을 더 이상 수정 [1201](https://github.com/NuGet/Home/issues/1201)</span><span class="sxs-lookup"><span data-stu-id="0ecaa-162">No longer modifying Nuget.Config files during ASP.NET 5 solution build - [1201](https://github.com/NuGet/Home/issues/1201)</span></span>
* <span data-ttu-id="0ecaa-163">패키지 업데이트-중 버전 제약 조건을 더 이상 변경할 수 [1130](https://github.com/NuGet/Home/issues/1130)</span><span class="sxs-lookup"><span data-stu-id="0ecaa-163">No longer changing allowed versions constraint during package update - [1130](https://github.com/NuGet/Home/issues/1130)</span></span>
* <span data-ttu-id="0ecaa-164">잠금 파일을 계속 잠긴-빌드하는 동안 [1127](https://github.com/NuGet/Home/issues/1127)</span><span class="sxs-lookup"><span data-stu-id="0ecaa-164">Lock files now remain locked during build - [1127](https://github.com/NuGet/Home/issues/1127)</span></span>
* <span data-ttu-id="0ecaa-165">이제 수정 `packages.config` 하지 업데이트-중 다시 작성해 [585](https://github.com/NuGet/Home/issues/585)</span><span class="sxs-lookup"><span data-stu-id="0ecaa-165">Now modifying `packages.config` and not rewriting it during updates - [585](https://github.com/NuGet/Home/issues/585)</span></span>

<span data-ttu-id="0ecaa-166">TFS 소스 제어와의 상호 작용에 맞게 개선 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ecaa-166">Interactions with TFS source control are improved:</span></span>

* <span data-ttu-id="0ecaa-167">-TFS에 연결 된 패키지에 대 한 설치를 더 이상 실패 [1164](https://github.com/NuGet/Home/issues/1164), [980](https://github.com/NuGet/Home/issues/980)</span><span class="sxs-lookup"><span data-stu-id="0ecaa-167">No longer failing installs for packages that are bound to TFS - [1164](https://github.com/NuGet/Home/issues/1164), [980](https://github.com/NuGet/Home/issues/980)</span></span>
* <span data-ttu-id="0ecaa-168">TFS 2013 통합-수 있도록 수정 된 NuGet 사용자 인터페이스 [1071](https://github.com/NuGet/Home/issues/1071)</span><span class="sxs-lookup"><span data-stu-id="0ecaa-168">Corrected NuGet user interface to allow TFS 2013 integration - [1071](https://github.com/NuGet/Home/issues/1071)</span></span>
* <span data-ttu-id="0ecaa-169">패키지를 제대로 패키지 폴더-에서 온 것으로 복원에 대 한 참조를 수정 했습니다. [1004](https://github.com/NuGet/Home/issues/1004)</span><span class="sxs-lookup"><span data-stu-id="0ecaa-169">Corrected references to packages restored to properly come from a packages folder - [1004](https://github.com/NuGet/Home/issues/1004)</span></span>

<span data-ttu-id="0ecaa-170">마지막으로, 우리 향상 되었습니다. 이러한 항목:</span><span class="sxs-lookup"><span data-stu-id="0ecaa-170">Finally, we also improved these items:</span></span>

* <span data-ttu-id="0ecaa-171">에 대 한 로그 메시지의 자세한 정도 감소 `project.json` 관리 되는 프로젝트- [1163](https://github.com/NuGet/Home/issues/1163)</span><span class="sxs-lookup"><span data-stu-id="0ecaa-171">Verbosity of log messages reduced for `project.json` managed projects - [1163](https://github.com/NuGet/Home/issues/1163)</span></span>
* <span data-ttu-id="0ecaa-172">이제 사용자 인터페이스-에 설치 된 버전의 패키지를 제대로 표시 [1061](https://github.com/NuGet/Home/issues/1061)</span><span class="sxs-lookup"><span data-stu-id="0ecaa-172">Now properly displaying the installed version of a package in the user interface - [1061](https://github.com/NuGet/Home/issues/1061)</span></span>
* <span data-ttu-id="0ecaa-173">이제 해당 nuspec에 지정 된 종속성 범위를 사용 하 여 패키지 설치에 대 한 안정적인 패키지 버전-해당 종속성을 시험판 버전을 보유 [1304](https://github.com/NuGet/Home/issues/1304)</span><span class="sxs-lookup"><span data-stu-id="0ecaa-173">Packages with dependency ranges specified in their nuspec now have pre-release versions of those dependencies installed for a stable package version - [1304](https://github.com/NuGet/Home/issues/1304)</span></span>

<span data-ttu-id="0ecaa-174">Visual Studio extension NuGet GitHub에서 찾을 수 있습니다에 대 한 처리 문제의 전체 목록은 [3.2 마일스 톤](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2)</span><span class="sxs-lookup"><span data-stu-id="0ecaa-174">A complete list of issues addressed for the Visual Studio extension can be found in the NuGet GitHub [3.2 milestone](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2)</span></span>

## <a name="known-issues"></a><span data-ttu-id="0ecaa-175">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="0ecaa-175">Known Issues</span></span>

<span data-ttu-id="0ecaa-176">찾을 수 있는 GitHub 문제 목록에서 문제를 추적 하려면 계속 하기: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="0ecaa-176">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>