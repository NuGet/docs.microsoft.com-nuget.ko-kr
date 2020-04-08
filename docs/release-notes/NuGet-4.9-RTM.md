---
title: NuGet 4.9 RTM 릴리스 정보
description: NuGet 4.9에 대한 릴리스 정보(알려진 문제, 버그 수정, 새 기능 및 DCR 포함)
author: karann-msft
ms.author: karann
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: e0dea74fe179c0dce4996f3e498185bb3a491856
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496458"
---
# <a name="nuget-49-release-notes"></a><span data-ttu-id="5c38f-103">NuGet 4.9 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="5c38f-103">NuGet 4.9 Release Notes</span></span>

<span data-ttu-id="5c38f-104">NuGet 배포 차량:</span><span class="sxs-lookup"><span data-stu-id="5c38f-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="5c38f-105">NuGet 버전</span><span class="sxs-lookup"><span data-stu-id="5c38f-105">NuGet version</span></span> | <span data-ttu-id="5c38f-106">Visual Studio 버전에서 사용 가능</span><span class="sxs-lookup"><span data-stu-id="5c38f-106">Available in Visual Studio version</span></span>| <span data-ttu-id="5c38f-107">.NET SDK에서 사용 가능</span><span class="sxs-lookup"><span data-stu-id="5c38f-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="5c38f-108">**4.9.0**</span><span class="sxs-lookup"><span data-stu-id="5c38f-108">**4.9.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="5c38f-109">Visual Studio 2017 버전 15.9.0</span><span class="sxs-lookup"><span data-stu-id="5c38f-109">Visual Studio 2017 version 15.9.0</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="5c38f-110">2.1.500, 2.2.100</span><span class="sxs-lookup"><span data-stu-id="5c38f-110">2.1.500, 2.2.100</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [<span data-ttu-id="5c38f-111">**4.9.1**</span><span class="sxs-lookup"><span data-stu-id="5c38f-111">**4.9.1**</span></span>](https://nuget.org/downloads) | <span data-ttu-id="5c38f-112">N/A</span><span class="sxs-lookup"><span data-stu-id="5c38f-112">n/a</span></span> | <span data-ttu-id="5c38f-113">N/A</span><span class="sxs-lookup"><span data-stu-id="5c38f-113">n/a</span></span> |
| [<span data-ttu-id="5c38f-114">**4.9.2**</span><span class="sxs-lookup"><span data-stu-id="5c38f-114">**4.9.2**</span></span>](https://nuget.org/downloads) |[<span data-ttu-id="5c38f-115">Visual Studio 2017 버전 15.9.4</span><span class="sxs-lookup"><span data-stu-id="5c38f-115">Visual Studio 2017 version 15.9.4</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="5c38f-116">2.1.502, 2.2.101</span><span class="sxs-lookup"><span data-stu-id="5c38f-116">2.1.502, 2.2.101</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [<span data-ttu-id="5c38f-117">**4.9.3**</span><span class="sxs-lookup"><span data-stu-id="5c38f-117">**4.9.3**</span></span>](https://nuget.org/downloads) |[<span data-ttu-id="5c38f-118">Visual Studio 2017 버전 15.9.6</span><span class="sxs-lookup"><span data-stu-id="5c38f-118">Visual Studio 2017 version 15.9.6</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="5c38f-119">2.1.504, 2.2.104</span><span class="sxs-lookup"><span data-stu-id="5c38f-119">2.1.504, 2.2.104</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |


## <a name="summary-whats-new-in-490"></a><span data-ttu-id="5c38f-120">요약: 4.9.0의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="5c38f-120">Summary: What's New in 4.9.0</span></span>

* <span data-ttu-id="5c38f-121">서명: ClientPolicies를 사용하여 NuGet.Config에 나열된 신뢰할 수 있는 작성자 및 리포지토리 사용 요구 - [#6961](https://github.com/NuGet/Home/issues/6961), [블로그 게시물](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)</span><span class="sxs-lookup"><span data-stu-id="5c38f-121">Signing: Enable ClientPolicies to require use of a set of Trusted Authors and Repositories listed in NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961), [blog post](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)</span></span>

* <span data-ttu-id="5c38f-122">“.snupkg” 파일을 만들어 팩에 기호 포함 -- 기호 서버에 대해 snupkg 파일을 수락하는 nuget 프로토콜을 해석하기 위해 푸시 향상 - [#6878](https://github.com/NuGet/Home/issues/6878), [블로그 게시물](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span><span class="sxs-lookup"><span data-stu-id="5c38f-122">create ".snupkg" files to contain symbols in pack -- enhance push to understand nuget protocol to accept snupkg files for symbol server - [#6878](https://github.com/NuGet/Home/issues/6878), [blog post](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span></span>

* <span data-ttu-id="5c38f-123">NuGet 자격 증명 플러그 인 V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span><span class="sxs-lookup"><span data-stu-id="5c38f-123">NuGet credential plugin V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span></span>

* <span data-ttu-id="5c38f-124">자체 포함 NuGet 패키지 - 라이선스 - [#4628](https://github.com/NuGet/Home/issues/4628), [공지](https://github.com/NuGet/Announcements/issues/32)</span><span class="sxs-lookup"><span data-stu-id="5c38f-124">Self-Contained NuGet Packages - License - [#4628](https://github.com/NuGet/Home/issues/4628), [announcement](https://github.com/NuGet/Announcements/issues/32)</span></span>

* <span data-ttu-id="5c38f-125">PackageReference의 옵트인 “GeneratePathProperty” 메타데이터를 사용하여 “Foo.Bar\1.0\" 디렉터리에 패키지별 MSBuild 속성 생성 - [#6949](https://github.com/NuGet/Home/issues/6949)</span><span class="sxs-lookup"><span data-stu-id="5c38f-125">Enable opt-in "GeneratePathProperty" metadata on a PackageReference to generate a per package MSBuild property to "Foo.Bar\1.0\" directory - [#6949](https://github.com/NuGet/Home/issues/6949)</span></span>

* <span data-ttu-id="5c38f-126">NuGet 작업에서 고객 성공 개선 - [#7108](https://github.com/NuGet/Home/issues/7108)</span><span class="sxs-lookup"><span data-stu-id="5c38f-126">Improve customer success with NuGet operations - [#7108](https://github.com/NuGet/Home/issues/7108)</span></span>

* <span data-ttu-id="5c38f-127">잠금 파일을 사용한 반복 가능한 패키지 복원 사용 - [#5602](https://github.com/NuGet/Home/issues/5602), [공지](https://github.com/NuGet/Announcements/issues/28), [블로그 게시물](https://blog.nuget.org/20181217/Enable-repeatable-package-restores-using-a-lock-file.html)</span><span class="sxs-lookup"><span data-stu-id="5c38f-127">Enable repeatable package restores using a lock file - [#5602](https://github.com/NuGet/Home/issues/5602), [announcement](https://github.com/NuGet/Announcements/issues/28), [blog post](https://blog.nuget.org/20181217/Enable-repeatable-package-restores-using-a-lock-file.html)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="5c38f-128">이번 릴리스에서 수정된 문제</span><span class="sxs-lookup"><span data-stu-id="5c38f-128">Issues fixed in this release</span></span>

* <span data-ttu-id="5c38f-129">PackageExtraction에 의해 발생한 오류로 승격된 경고(WarnAsErrors를 통해)가 추출된 패키지를 그대로 두지 않아야 함 - [#7445](https://github.com/NuGet/Home/issues/7445)</span><span class="sxs-lookup"><span data-stu-id="5c38f-129">Warnings elevated to errors (via WarnAsErrors) raised by PackageExtraction should never leave extracted package around - [#7445](https://github.com/NuGet/Home/issues/7445)</span></span>

* <span data-ttu-id="5c38f-130">잘못 서명된 패키지가 전역 패키지 폴더에 있으면 안 됨 - [#7423](https://github.com/NuGet/Home/issues/7423)</span><span class="sxs-lookup"><span data-stu-id="5c38f-130">Badly signed packages should not end up in the global packages folder - [#7423](https://github.com/NuGet/Home/issues/7423)</span></span>

* <span data-ttu-id="5c38f-131">바인딩 리디렉션 생성이 외관 어셈블리를 건너뛰지 않아야 함 - [#7393](https://github.com/NuGet/Home/issues/7393)</span><span class="sxs-lookup"><span data-stu-id="5c38f-131">binding redirect generation should not skip facade assemblies - [#7393](https://github.com/NuGet/Home/issues/7393)</span></span>

* <span data-ttu-id="5c38f-132">VersionRange Equals가 부동 범위를 비교하지 않음 - [#7324](https://github.com/NuGet/Home/issues/7324)</span><span class="sxs-lookup"><span data-stu-id="5c38f-132">VersionRange Equals doesn't compare floating ranges - [#7324](https://github.com/NuGet/Home/issues/7324)</span></span>

* <span data-ttu-id="5c38f-133">복원: 새 .NET Core 2.1 HTTP 스택을 사용하여 성능 저하 - [#7314](https://github.com/NuGet/Home/issues/7314)</span><span class="sxs-lookup"><span data-stu-id="5c38f-133">Restore:  performance regression using new .NET Core 2.1 HTTP stack - [#7314](https://github.com/NuGet/Home/issues/7314)</span></span>

* <span data-ttu-id="5c38f-134">패키지 업데이트가 PackageReference의 PrivateAssets를 수정하지 않아야 함 - [#7285](https://github.com/NuGet/Home/issues/7285)</span><span class="sxs-lookup"><span data-stu-id="5c38f-134">Update of a Package should not modify PrivateAssets of a PackageReference - [#7285](https://github.com/NuGet/Home/issues/7285)</span></span>

* <span data-ttu-id="5c38f-135">서명:  패키지에 항목이 너무 많은 경우(65534개 이상) 서명에 실패함 - [#7248](https://github.com/NuGet/Home/issues/7248)</span><span class="sxs-lookup"><span data-stu-id="5c38f-135">Signing:  signing should fail if a package has too many package entries (>65534) - [#7248](https://github.com/NuGet/Home/issues/7248)</span></span>

* <span data-ttu-id="5c38f-136">“dotnet nuget push” 코드 경로가 새 자격 증명 공급자를 지원해야 함 - [#7233](https://github.com/NuGet/Home/issues/7233)</span><span class="sxs-lookup"><span data-stu-id="5c38f-136">"dotnet nuget push" codepath should support the new credential provider - [#7233](https://github.com/NuGet/Home/issues/7233)</span></span>

* <span data-ttu-id="5c38f-137">고정 문화권에서 플러그 인 실행 지원(docker에서 발생) - [#7223](https://github.com/NuGet/Home/issues/7223)</span><span class="sxs-lookup"><span data-stu-id="5c38f-137">Support executing plugins with invariant culture (as happens in docker) - [#7223](https://github.com/NuGet/Home/issues/7223)</span></span>

* <span data-ttu-id="5c38f-138">nuget 소스가 NuGet.config의 자격 증명을 삭제하지 않아야 함 - [#7200](https://github.com/NuGet/Home/issues/7200)</span><span class="sxs-lookup"><span data-stu-id="5c38f-138">nuget sources add should not delete credentials from NuGet.config - [#7200](https://github.com/NuGet/Home/issues/7200)</span></span>

* <span data-ttu-id="5c38f-139">devDependency PackageReference 설치가 excludeassets=compile로 기본 설정되어야 함 - [#7084](https://github.com/NuGet/Home/issues/7084)</span><span class="sxs-lookup"><span data-stu-id="5c38f-139">installing a devDependency PackageReference should default to excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)</span></span>

* <span data-ttu-id="5c38f-140">마이그레이터 옵션이 모든 프로젝트에 대해 표시되도록 수정하고, 프로젝트가 호환되지 않는 경우 오류 표시 - [#6958](https://github.com/NuGet/Home/issues/6958)</span><span class="sxs-lookup"><span data-stu-id="5c38f-140">fix migrator option to be displayed for all projects and show error if project is incompatible - [#6958](https://github.com/NuGet/Home/issues/6958)</span></span>

* <span data-ttu-id="5c38f-141">“dotnet add package”가 자산 파일에 수행하는 복원을 커밋해야 함 - [#6928](https://github.com/NuGet/Home/issues/6928)</span><span class="sxs-lookup"><span data-stu-id="5c38f-141">"dotnet add package" should commit the restore it performs to the assets file - [#6928](https://github.com/NuGet/Home/issues/6928)</span></span>

* <span data-ttu-id="5c38f-142">서명:  서명 관련 오류 메시지 개선 - [#6906](https://github.com/NuGet/Home/issues/6906)</span><span class="sxs-lookup"><span data-stu-id="5c38f-142">Signing:  improve signing related error messages - [#6906](https://github.com/NuGet/Home/issues/6906)</span></span>

* <span data-ttu-id="5c38f-143">[테스트 실패][zh-TW]“Package Manager Console” 문자열이 패키지 관리자 콘솔에서 지역화되지 않음  - [#6381](https://github.com/NuGet/Home/issues/6381)</span><span class="sxs-lookup"><span data-stu-id="5c38f-143">[Test Failure][zh-TW]String "Package Manager Console" doesn't localize on Package Manager Console  - [#6381](https://github.com/NuGet/Home/issues/6381)</span></span>

* <span data-ttu-id="5c38f-144">“프로젝트 정보를 찾을 수 없음” 오류 메시지가 VS 내에서 좀 더 구체적이어야 함 - [#5350](https://github.com/NuGet/Home/issues/5350)</span><span class="sxs-lookup"><span data-stu-id="5c38f-144">Error message around "Unable to find project information" should be a little more specific inside VS - [#5350](https://github.com/NuGet/Home/issues/5350)</span></span>

* <span data-ttu-id="5c38f-145">nuget 팩의 nuspec 버전 태그를 잘못 사용하면 도움이 되지 않는 오류 메시지가 표시됨 - [#2714](https://github.com/NuGet/Home/issues/2714)</span><span class="sxs-lookup"><span data-stu-id="5c38f-145">Unhelpful error message when incorrectly using nuspec version tag of nuget pack - [#2714](https://github.com/NuGet/Home/issues/2714)</span></span>

* <span data-ttu-id="5c38f-146">DCR - 서명: NuGet 프로토콜 지원: RepositorySignatures/4.9.0 리소스 - [#7421](https://github.com/NuGet/Home/issues/7421)</span><span class="sxs-lookup"><span data-stu-id="5c38f-146">DCR - Signing:  support NuGet protocol: RepositorySignatures/4.9.0 resource - [#7421](https://github.com/NuGet/Home/issues/7421)</span></span>

* <span data-ttu-id="5c38f-147">DCR - 패키지 추출 중 이제 .nupkg.metadata 파일이 생성됨 - “content-hash” 포함 - [#7283](https://github.com/NuGet/Home/issues/7283)</span><span class="sxs-lookup"><span data-stu-id="5c38f-147">DCR - .nupkg.metadata file will now be created during package extraction - contains "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)</span></span>

* <span data-ttu-id="5c38f-148">DCR - Mono에서 실행 중 플러그 인에 대한 authenticode 확인을 건너뜀 - [#7222](https://github.com/NuGet/Home/issues/7222)</span><span class="sxs-lookup"><span data-stu-id="5c38f-148">DCR - Skip authenticode verification for plugins while executing on Mono - [#7222](https://github.com/NuGet/Home/issues/7222)</span></span>

[<span data-ttu-id="5c38f-149">이 릴리스 4.9.0에서 수정된 모든 문제 목록</span><span class="sxs-lookup"><span data-stu-id="5c38f-149">List of all issues fixed in this release 4.9.0</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a><span data-ttu-id="5c38f-150">요약: 4.9.1의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="5c38f-150">Summary: What's New in 4.9.1</span></span>

* <span data-ttu-id="5c38f-151">새 명령 trusted-signers를 통해 nuget.config에 쓰기 읽기에 대한 지원 추가 - [#7480](https://github.com/NuGet/Home/issues/7480)</span><span class="sxs-lookup"><span data-stu-id="5c38f-151">Add support for reading a writing to the nuget.config via a new command trusted-signers - [#7480](https://github.com/NuGet/Home/issues/7480)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="5c38f-152">이번 릴리스에서 수정된 문제</span><span class="sxs-lookup"><span data-stu-id="5c38f-152">Issues fixed in this release</span></span>

* <span data-ttu-id="5c38f-153">라이선스 링크 생성 수정 - [#7515](https://github.com/NuGet/Home/issues/7515)</span><span class="sxs-lookup"><span data-stu-id="5c38f-153">Fix license link generation - [#7515](https://github.com/NuGet/Home/issues/7515)</span></span>

* <span data-ttu-id="5c38f-154">서명 유효성 검사의 오류 코드 재발 - [#7492](https://github.com/NuGet/Home/issues/7492)</span><span class="sxs-lookup"><span data-stu-id="5c38f-154">Error codes regression for validating signatures - [#7492](https://github.com/NuGet/Home/issues/7492)</span></span>

* <span data-ttu-id="5c38f-155">NuGet.Build.Tasks.Pack 패키지에 라이선스 정보가 없음 - [#7379](https://github.com/NuGet/Home/issues/7379)</span><span class="sxs-lookup"><span data-stu-id="5c38f-155">NuGet.Build.Tasks.Pack package does not have license information - [#7379](https://github.com/NuGet/Home/issues/7379)</span></span>

[<span data-ttu-id="5c38f-156">이 릴리스 4.9.1에서 수정된 모든 문제 목록</span><span class="sxs-lookup"><span data-stu-id="5c38f-156">List of all issues fixed in this release 4.9.1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="summary-whats-new-in-492"></a><span data-ttu-id="5c38f-157">요약: 4.9.2의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="5c38f-157">Summary: What's New in 4.9.2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="5c38f-158">이번 릴리스에서 수정된 문제</span><span class="sxs-lookup"><span data-stu-id="5c38f-158">Issues fixed in this release</span></span>

* <span data-ttu-id="5c38f-159">원본 이름에 공백이 포함되면 VS/dotnet.exe/nuget.exe/msbuild.exe 복원에서 자격 증명을 사용하지 않음 - [#7517](https://github.com/NuGet/Home/issues/7517)</span><span class="sxs-lookup"><span data-stu-id="5c38f-159">VS/dotnet.exe/nuget.exe/msbuild.exe restore doesn't use credentials when source name contains a whitespace - [#7517](https://github.com/NuGet/Home/issues/7517)</span></span>

* <span data-ttu-id="5c38f-160">LicenseAcceptanceWindow 및 LicenseFileWindow 접근성 문제 - [#7452](https://github.com/NuGet/Home/issues/7452)</span><span class="sxs-lookup"><span data-stu-id="5c38f-160">LicenseAcceptanceWindow and LicenseFileWindow Accessibility issues - [#7452](https://github.com/NuGet/Home/issues/7452)</span></span>

* <span data-ttu-id="5c38f-161">DateTimeConverter에서 DateTime.Parse의 FormatException 수정 - [#7539](https://github.com/NuGet/Home/issues/7539)</span><span class="sxs-lookup"><span data-stu-id="5c38f-161">Fix FormatException in DateTime.Parse from DateTimeConverter - [#7539](https://github.com/NuGet/Home/issues/7539)</span></span>

[<span data-ttu-id="5c38f-162">이 릴리스 4.9.2에서 수정된 모든 문제 목록</span><span class="sxs-lookup"><span data-stu-id="5c38f-162">List of all issues fixed in this release 4.9.2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

## <a name="summary-whats-new-in-493"></a><span data-ttu-id="5c38f-163">요약: 4.9.3의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="5c38f-163">Summary: What's New in 4.9.3</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="5c38f-164">이번 릴리스에서 수정된 문제</span><span class="sxs-lookup"><span data-stu-id="5c38f-164">Issues fixed in this release</span></span>
#### <a name="repeatable-package-restores-using-a-lock-file-issues"></a><span data-ttu-id="5c38f-165">“잠금 파일을 사용한 반복 가능한 패키지 복원” 문제</span><span class="sxs-lookup"><span data-stu-id="5c38f-165">"Repeatable Package Restores Using a Lock File" Issues</span></span>

* <span data-ttu-id="5c38f-166">이전에 캐시된 패키지의 해시가 잘못 계산되어 잠긴 모드가 작동하지 않음 - [#7682](https://github.com/NuGet/Home/issues/7682)</span><span class="sxs-lookup"><span data-stu-id="5c38f-166">Locked mode not working as hash is calculated incorrectly for previously cached packages - [#7682](https://github.com/NuGet/Home/issues/7682)</span></span>

* <span data-ttu-id="5c38f-167">복원이 `packages.lock.json` 파일에 정의된 것과 다른 버전으로 확인됨 - [#7667](https://github.com/NuGet/Home/issues/7667)</span><span class="sxs-lookup"><span data-stu-id="5c38f-167">Restore resolves to a different version than defined in `packages.lock.json` file - [#7667](https://github.com/NuGet/Home/issues/7667)</span></span>

* <span data-ttu-id="5c38f-168">ProjectReferences가 관련된 경우 ‘--locked-mode / RestoreLockedMode’로 인해 의사 복원 실패 발생 - [#7646](https://github.com/NuGet/Home/issues/7646)</span><span class="sxs-lookup"><span data-stu-id="5c38f-168">'--locked-mode / RestoreLockedMode' causes spurious Restore failures when ProjectReferences are involved - [#7646](https://github.com/NuGet/Home/issues/7646)</span></span>

* <span data-ttu-id="5c38f-169">MSBuild SDK 확인자에서 packages.lock.json을 사용할 때 복원에 실패하는 SDK 패키지용 SHA의 유효성을 검사하려고 함 - [#7599](https://github.com/NuGet/Home/issues/7599)</span><span class="sxs-lookup"><span data-stu-id="5c38f-169">MSBuild SDK resolver tries to validate SHA for a SDK package which fails restore when using packages.lock.json - [#7599](https://github.com/NuGet/Home/issues/7599)</span></span>

#### <a name="lock-down-your-dependencies-using-configurable-trust-policies-issues"></a><span data-ttu-id="5c38f-170">“구성 가능한 트러스트 정책을 사용하여 종속성 잠금” 문제</span><span class="sxs-lookup"><span data-stu-id="5c38f-170">"Lock Down Your Dependencies Using Configurable Trust Policies" Issues</span></span>
* <span data-ttu-id="5c38f-171">서명된 패키지가 지원되지 않는 동안에는 dotnet.exe에서 신뢰할 수 있는 서명자를 평가하지 않아야 함 - [#7574](https://github.com/NuGet/Home/issues/7574)</span><span class="sxs-lookup"><span data-stu-id="5c38f-171">dotnet.exe should not evaluate trusted-signers while signed packages are not supported - [#7574](https://github.com/NuGet/Home/issues/7574)</span></span>

* <span data-ttu-id="5c38f-172">구성 파일의 trustedSigners 순서가 신뢰 평가에 영향을 줌 - [#7572](https://github.com/NuGet/Home/issues/7572)</span><span class="sxs-lookup"><span data-stu-id="5c38f-172">Order of trustedSigners in config file affects trust evaluation - [#7572](https://github.com/NuGet/Home/issues/7572)</span></span>

* <span data-ttu-id="5c38f-173">ISettings를 구현할 수 없음[트러스트 정책 기능을 지원하도록 설정 API 리팩터링으로 인해 발생] - [#7614](https://github.com/NuGet/Home/issues/7614)</span><span class="sxs-lookup"><span data-stu-id="5c38f-173">Can't implement ISettings [Caused by refactoring of settings APIs to support Trust Policies feature] - [#7614](https://github.com/NuGet/Home/issues/7614)</span></span>

#### <a name="improved-debugging-experience-issues"></a><span data-ttu-id="5c38f-174">“향상된 디버깅 환경” 문제</span><span class="sxs-lookup"><span data-stu-id="5c38f-174">"Improved Debugging Experience" Issues</span></span>

* <span data-ttu-id="5c38f-175">.NET Core 전역 도구용 기호 패키지를 게시할 수 없음 - [#7632](https://github.com/NuGet/Home/issues/7632)</span><span class="sxs-lookup"><span data-stu-id="5c38f-175">Cannot publish symbol package for .NET Core Global Tool - [#7632](https://github.com/NuGet/Home/issues/7632)</span></span>

#### <a name="self-contained-nuget-packages---license-issues"></a><span data-ttu-id="5c38f-176">“자체 포함된 NuGet 패키지 - 라이선스” 문제</span><span class="sxs-lookup"><span data-stu-id="5c38f-176">"Self-Contained NuGet Packages - License" Issues</span></span>

* <span data-ttu-id="5c38f-177">포함된 라이선스 파일을 사용할 때 기호 .snupkg 패키지를 빌드하는 중 오류 발생 - [#7591](https://github.com/NuGet/Home/issues/7591)</span><span class="sxs-lookup"><span data-stu-id="5c38f-177">Error building symbol .snupkg package when using embedded license file - [#7591](https://github.com/NuGet/Home/issues/7591)</span></span>

[<span data-ttu-id="5c38f-178">이 릴리스 4.9.3에서 수정된 모든 문제 목록</span><span class="sxs-lookup"><span data-stu-id="5c38f-178">List of all issues fixed in this release 4.9.3</span></span>](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.3")

## <a name="summary-whats-new-in-494"></a><span data-ttu-id="5c38f-179">요약: 4.9.4의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="5c38f-179">Summary: What's New in 4.9.4</span></span>

* <span data-ttu-id="5c38f-180">보안 수정: ~/.nuget 내에서 만든 파일에 대한 권한이 열려 있습니다. [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span><span class="sxs-lookup"><span data-stu-id="5c38f-180">Security Fix: Permissions on files created inside ~/.nuget are too open [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span></span>


## <a name="known-issues"></a><span data-ttu-id="5c38f-181">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="5c38f-181">Known issues</span></span>

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519"></a><span data-ttu-id="5c38f-182">dotnet nuget 푸시 --interactive로 인해 Mac에서 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="5c38f-182">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="5c38f-183"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="5c38f-183"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

#### <a name="issue"></a><span data-ttu-id="5c38f-184">문제점</span><span class="sxs-lookup"><span data-stu-id="5c38f-184">Issue</span></span>
<span data-ttu-id="5c38f-185">`--interactive` 인수가 dotnet CLI에 의해 전달되지 않고 오류가 발생함 `error: Missing value for option 'interactive'`</span><span class="sxs-lookup"><span data-stu-id="5c38f-185">The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`</span></span>

#### <a name="workaround"></a><span data-ttu-id="5c38f-186">해결 방법</span><span class="sxs-lookup"><span data-stu-id="5c38f-186">Workaround</span></span>
<span data-ttu-id="5c38f-187">`dotnet restore --interactive` 같은 대화형 옵션을 사용하여 다른 dotnet 명령을 실행하고 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="5c38f-187">Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="5c38f-188">인증은 자격 증명 공급자에 의해 캐시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c38f-188">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="5c38f-189">그런 다음, `dotnet nuget push`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5c38f-189">Then run `dotnet nuget push`.</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414"></a><span data-ttu-id="5c38f-190">.NET Core SDK로 설치된 FallbackFolders의 패키지는 사용자 지정 설치되며 서명 유효성 검사에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="5c38f-190">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="5c38f-191"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="5c38f-191"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>

#### <a name="issue"></a><span data-ttu-id="5c38f-192">문제점</span><span class="sxs-lookup"><span data-stu-id="5c38f-192">Issue</span></span>
<span data-ttu-id="5c38f-193">netcoreapp 1.x 및 netcoreapp 2.x 다중 대상을 지정하는 프로젝트를 복원하기 위해 dotnet.exe 2.x를 사용하면 대체 폴더가 파일 피드로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c38f-193">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="5c38f-194">즉 복원할 때 NuGet이 대체 폴더에서 패키지를 선택하고 전역 패키지 폴더에 설치하려고 하며 일반적인 서명 유효성 검사를 수행하지만 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="5c38f-194">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>

#### <a name="workaround"></a><span data-ttu-id="5c38f-195">해결 방법</span><span class="sxs-lookup"><span data-stu-id="5c38f-195">Workaround</span></span>
<span data-ttu-id="5c38f-196">`RestoreAdditionalProjectSources`를 nothing으로 설정하여 대체 폴더를 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5c38f-196">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="5c38f-197">`<RestoreAdditionalProjectSources/>` NuGet.org에서 많은 패키지가 다운로드되도록 하므로 주의하여 사용하세요. 그렇지 않으면 대체 폴더에서 복원될 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="5c38f-197">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
