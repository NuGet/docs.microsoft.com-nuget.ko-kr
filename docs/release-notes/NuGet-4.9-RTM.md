---
title: NuGet 4.9 RTM 릴리스 정보
description: NuGet 4.9에 대한 릴리스 정보(알려진 문제, 버그 수정, 새 기능 및 DCR 포함)
author: karann-msft
ms.author: karann
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: 3da1056f64b76f27afa662d879ef9f85868e2a07
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453779"
---
# <a name="nuget-49-release-notes"></a><span data-ttu-id="76b5b-103">NuGet 4.9 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="76b5b-103">NuGet 4.9 Release Notes</span></span>

<span data-ttu-id="76b5b-104">[Visual Studio 2017 15.9.0 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes)는 NuGet 4.9.0 기능과 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="76b5b-104">[Visual Studio 2017 15.9.0 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.9.0 functionality.</span></span>


<span data-ttu-id="76b5b-105">동일한 기능의 명령줄 버전도 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="76b5b-105">Command line versions of the same functionality are also available:</span></span>
* <span data-ttu-id="76b5b-106">NuGet.exe 4.9.x - [nuget.org/downloads](https://nuget.org/downloads)</span><span class="sxs-lookup"><span data-stu-id="76b5b-106">NuGet.exe 4.9.x - [nuget.org/downloads](https://nuget.org/downloads)</span></span>
* <span data-ttu-id="76b5b-107">dotnet.exe - [.NET Core SDK 2.1.500](https://www.microsoft.com/net/download/visual-studio-sdks)</span><span class="sxs-lookup"><span data-stu-id="76b5b-107">dotnet.exe - [.NET Core SDK 2.1.500](https://www.microsoft.com/net/download/visual-studio-sdks)</span></span>


## <a name="summary-whats-new-in-490"></a><span data-ttu-id="76b5b-108">요약: 4.9.0의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="76b5b-108">Summary: What's New in 4.9.0</span></span>

* <span data-ttu-id="76b5b-109">서명: ClientPolicies를 사용하여 NuGet.Config에 나열된 신뢰할 수 있는 작성자 및 리포지토리 사용 요구 - [#6961](https://github.com/NuGet/Home/issues/6961)</span><span class="sxs-lookup"><span data-stu-id="76b5b-109">Signing: Enable ClientPolicies to require use of a set of Trusted Authors and Repositories listed in NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961)</span></span>

* <span data-ttu-id="76b5b-110">“.snupkg” 파일을 만들어 팩에 기호 포함 -- 기호 서버에 대해 snupkg 파일을 수락하는 nuget 프로토콜을 해석하기 위해 푸시 향상 - [#6878](https://github.com/NuGet/Home/issues/6878)</span><span class="sxs-lookup"><span data-stu-id="76b5b-110">create ".snupkg" files to contain symbols in pack -- enhance push to understand nuget protocol to accept snupkg files for symbol server - [#6878](https://github.com/NuGet/Home/issues/6878)</span></span>

* <span data-ttu-id="76b5b-111">NuGet 자격 증명 플러그 인 V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span><span class="sxs-lookup"><span data-stu-id="76b5b-111">NuGet credential plugin V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span></span>

* <span data-ttu-id="76b5b-112">자체 포함된 NuGet 패키지 - 라이선스 - [#4628](https://github.com/NuGet/Home/issues/4628)</span><span class="sxs-lookup"><span data-stu-id="76b5b-112">Self-Contained NuGet Packages - License - [#4628](https://github.com/NuGet/Home/issues/4628)</span></span>

* <span data-ttu-id="76b5b-113">PackageReference의 옵트인 “GeneratePathProperty” 메타데이터를 사용하여 “Foo.Bar\1.0” 디렉터리에 패키지별 MSBuild 속성 생성 - [#6949](https://github.com/NuGet/Home/issues/6949)</span><span class="sxs-lookup"><span data-stu-id="76b5b-113">Enable opt-in "GeneratePathProperty" metadata on a PackageReference to generate a per package MSBuild property to "Foo.Bar\1.0\" directory - [#6949](https://github.com/NuGet/Home/issues/6949)</span></span>

* <span data-ttu-id="76b5b-114">NuGet 작업에서 고객 성공 개선 - [#7108](https://github.com/NuGet/Home/issues/7108)</span><span class="sxs-lookup"><span data-stu-id="76b5b-114">Improve customer success with NuGet operations - [#7108](https://github.com/NuGet/Home/issues/7108)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="76b5b-115">이번 릴리스에서 수정된 문제</span><span class="sxs-lookup"><span data-stu-id="76b5b-115">Issues fixed in this release</span></span>

* <span data-ttu-id="76b5b-116">PackageExtraction에 의해 발생한 오류로 승격된 경고(WarnAsErrors를 통해)가 추출된 패키지를 그대로 두지 않아야 함 - [#7445](https://github.com/NuGet/Home/issues/7445)</span><span class="sxs-lookup"><span data-stu-id="76b5b-116">Warnings elevated to errors (via WarnAsErrors) raised by PackageExtraction should never leave extracted package around - [#7445](https://github.com/NuGet/Home/issues/7445)</span></span>

* <span data-ttu-id="76b5b-117">잘못 서명된 패키지가 전역 패키지 폴더에 있으면 안 됨 - [#7423](https://github.com/NuGet/Home/issues/7423)</span><span class="sxs-lookup"><span data-stu-id="76b5b-117">Badly signed packages should not end up in the global packages folder - [#7423](https://github.com/NuGet/Home/issues/7423)</span></span>

* <span data-ttu-id="76b5b-118">바인딩 리디렉션 생성이 외관 어셈블리를 건너뛰지 않아야 함 - [#7393](https://github.com/NuGet/Home/issues/7393)</span><span class="sxs-lookup"><span data-stu-id="76b5b-118">binding redirect generation should not skip facade assemblies - [#7393](https://github.com/NuGet/Home/issues/7393)</span></span>

* <span data-ttu-id="76b5b-119">VersionRange Equals가 부동 범위를 비교하지 않음 - [#7324](https://github.com/NuGet/Home/issues/7324)</span><span class="sxs-lookup"><span data-stu-id="76b5b-119">VersionRange Equals doesn't compare floating ranges - [#7324](https://github.com/NuGet/Home/issues/7324)</span></span>

* <span data-ttu-id="76b5b-120">복원: 새 .NET Core 2.1 HTTP 스택을 사용하여 성능 저하 - [#7314](https://github.com/NuGet/Home/issues/7314)</span><span class="sxs-lookup"><span data-stu-id="76b5b-120">Restore:  performance regression using new .NET Core 2.1 HTTP stack - [#7314](https://github.com/NuGet/Home/issues/7314)</span></span>

* <span data-ttu-id="76b5b-121">패키지 업데이트가 PackageReference의 PrivateAssets를 수정하지 않아야 함 - [#7285](https://github.com/NuGet/Home/issues/7285)</span><span class="sxs-lookup"><span data-stu-id="76b5b-121">Update of a Package should not modify PrivateAssets of a PackageReference - [#7285](https://github.com/NuGet/Home/issues/7285)</span></span>

* <span data-ttu-id="76b5b-122">서명:  패키지에 항목이 너무 많은 경우(65534개 이상) 서명에 실패함 - [#7248](https://github.com/NuGet/Home/issues/7248)</span><span class="sxs-lookup"><span data-stu-id="76b5b-122">Signing:  signing should fail if a package has too many package entries (>65534) - [#7248](https://github.com/NuGet/Home/issues/7248)</span></span>

* <span data-ttu-id="76b5b-123">“dotnet nuget push” 코드 경로가 새 자격 증명 공급자를 지원해야 함 - [#7233](https://github.com/NuGet/Home/issues/7233)</span><span class="sxs-lookup"><span data-stu-id="76b5b-123">"dotnet nuget push" codepath should support the new credential provider - [#7233](https://github.com/NuGet/Home/issues/7233)</span></span>

* <span data-ttu-id="76b5b-124">고정 문화권에서 플러그 인 실행 지원(docker에서 발생) - [#7223](https://github.com/NuGet/Home/issues/7223)</span><span class="sxs-lookup"><span data-stu-id="76b5b-124">Support executing plugins with invariant culture (as happens in docker) - [#7223](https://github.com/NuGet/Home/issues/7223)</span></span>

* <span data-ttu-id="76b5b-125">nuget 소스가 NuGet.config의 자격 증명을 삭제하지 않아야 함 - [#7200](https://github.com/NuGet/Home/issues/7200)</span><span class="sxs-lookup"><span data-stu-id="76b5b-125">nuget sources add should not delete credentials from NuGet.config - [#7200](https://github.com/NuGet/Home/issues/7200)</span></span>

* <span data-ttu-id="76b5b-126">devDependency PackageReference 설치가 excludeassets=compile로 기본 설정되어야 함 - [#7084](https://github.com/NuGet/Home/issues/7084)</span><span class="sxs-lookup"><span data-stu-id="76b5b-126">installing a devDependency PackageReference should default to excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)</span></span>

* <span data-ttu-id="76b5b-127">마이그레이터 옵션이 모든 프로젝트에 대해 표시되도록 수정하고, 프로젝트가 호환되지 않는 경우 오류 표시 - [#6958](https://github.com/NuGet/Home/issues/6958)</span><span class="sxs-lookup"><span data-stu-id="76b5b-127">fix migrator option to be displayed for all projects and show error if project is incompatible - [#6958](https://github.com/NuGet/Home/issues/6958)</span></span>

* <span data-ttu-id="76b5b-128">“dotnet add package”가 자산 파일에 수행하는 복원을 커밋해야 함 - [#6928](https://github.com/NuGet/Home/issues/6928)</span><span class="sxs-lookup"><span data-stu-id="76b5b-128">"dotnet add package" should commit the restore it performs to the assets file - [#6928](https://github.com/NuGet/Home/issues/6928)</span></span>

* <span data-ttu-id="76b5b-129">서명:  서명 관련 오류 메시지 개선 - [#6906](https://github.com/NuGet/Home/issues/6906)</span><span class="sxs-lookup"><span data-stu-id="76b5b-129">Signing:  improve signing related error messages - [#6906](https://github.com/NuGet/Home/issues/6906)</span></span>

* <span data-ttu-id="76b5b-130">[테스트 실패][zh-TW]“Package Manager Console” 문자열이 패키지 관리자 콘솔에서 지역화되지 않음  - [#6381](https://github.com/NuGet/Home/issues/6381)</span><span class="sxs-lookup"><span data-stu-id="76b5b-130">[Test Failure][zh-TW]String "Package Manager Console" doesn't localize on Package Manager Console  - [#6381](https://github.com/NuGet/Home/issues/6381)</span></span>

* <span data-ttu-id="76b5b-131">“프로젝트 정보를 찾을 수 없음” 오류 메시지가 VS 내에서 좀 더 구체적이어야 함 - [#5350](https://github.com/NuGet/Home/issues/5350)</span><span class="sxs-lookup"><span data-stu-id="76b5b-131">Error message around "Unable to find project information" should be a little more specific inside VS - [#5350](https://github.com/NuGet/Home/issues/5350)</span></span>

* <span data-ttu-id="76b5b-132">nuget 팩의 nuspec 버전 태그를 잘못 사용하면 도움이 되지 않는 오류 메시지가 표시됨 - [#2714](https://github.com/NuGet/Home/issues/2714)</span><span class="sxs-lookup"><span data-stu-id="76b5b-132">Unhelpful error message when incorrectly using nuspec version tag of nuget pack - [#2714](https://github.com/NuGet/Home/issues/2714)</span></span>

* <span data-ttu-id="76b5b-133">DCR - 서명:  NuGet 프로토콜 지원: RepositorySignatures/4.9.0 리소스 - [#7421](https://github.com/NuGet/Home/issues/7421)</span><span class="sxs-lookup"><span data-stu-id="76b5b-133">DCR - Signing:  support NuGet protocol: RepositorySignatures/4.9.0 resource - [#7421](https://github.com/NuGet/Home/issues/7421)</span></span>

* <span data-ttu-id="76b5b-134">DCR - 패키지 추출 중 이제 .nupkg.metadata 파일이 생성됨 - “content-hash” 포함 - [#7283](https://github.com/NuGet/Home/issues/7283)</span><span class="sxs-lookup"><span data-stu-id="76b5b-134">DCR - .nupkg.metadata file will now be created during package extraction - contains "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)</span></span>

* <span data-ttu-id="76b5b-135">DCR - Mono에서 실행 중 플러그 인에 대한 authenticode 확인을 건너뜀 - [#7222](https://github.com/NuGet/Home/issues/7222)</span><span class="sxs-lookup"><span data-stu-id="76b5b-135">DCR - Skip authenticode verification for plugins while executing on Mono - [#7222](https://github.com/NuGet/Home/issues/7222)</span></span>

[<span data-ttu-id="76b5b-136">이 릴리스 4.9.0에서 수정된 모든 문제 목록</span><span class="sxs-lookup"><span data-stu-id="76b5b-136">List of all issues fixed in this release 4.9.0</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a><span data-ttu-id="76b5b-137">요약: 4.9.1의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="76b5b-137">Summary: What's New in 4.9.1</span></span>

* <span data-ttu-id="76b5b-138">새 명령 trusted-signers를 통해 nuget.config에 쓰기 읽기에 대한 지원 추가 - [#7480](https://github.com/NuGet/Home/issues/7480)</span><span class="sxs-lookup"><span data-stu-id="76b5b-138">Add support for reading a writing to the nuget.config via a new command trusted-signers - [#7480](https://github.com/NuGet/Home/issues/7480)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="76b5b-139">이번 릴리스에서 수정된 문제</span><span class="sxs-lookup"><span data-stu-id="76b5b-139">Issues fixed in this release</span></span>

* <span data-ttu-id="76b5b-140">라이선스 링크 생성 수정 - [#7515](https://github.com/NuGet/Home/issues/7515)</span><span class="sxs-lookup"><span data-stu-id="76b5b-140">Fix license link generation - [#7515](https://github.com/NuGet/Home/issues/7515)</span></span>

* <span data-ttu-id="76b5b-141">서명 유효성 검사의 오류 코드 재발 - [#7492](https://github.com/NuGet/Home/issues/7492)</span><span class="sxs-lookup"><span data-stu-id="76b5b-141">Error codes regression for validating signatures - [#7492](https://github.com/NuGet/Home/issues/7492)</span></span>

* <span data-ttu-id="76b5b-142">NuGet.Build.Tasks.Pack 패키지에 라이선스 정보가 없음 - [#7379](https://github.com/NuGet/Home/issues/7379)</span><span class="sxs-lookup"><span data-stu-id="76b5b-142">NuGet.Build.Tasks.Pack package does not have license information - [#7379](https://github.com/NuGet/Home/issues/7379)</span></span>

[<span data-ttu-id="76b5b-143">이 릴리스 4.9.1에서 수정된 모든 문제 목록</span><span class="sxs-lookup"><span data-stu-id="76b5b-143">List of all issues fixed in this release 4.9.1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="known-issues"></a><span data-ttu-id="76b5b-144">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="76b5b-144">Known issues</span></span>

### <a name="dotnetexenugetexe-doesnt-use-credentials-when-source-name-contains-a-whitespace---7517httpsgithubcomnugethomeissues7517"></a><span data-ttu-id="76b5b-145">소스 이름에 공백이 포함되면 dotnet.exe/nuget.exe가 자격 증명을 사용하지 않음 - [#7517](https://github.com/NuGet/Home/issues/7517)</span><span class="sxs-lookup"><span data-stu-id="76b5b-145">dotnet.exe/nuget.exe doesn't use credentials when source name contains a whitespace - [#7517](https://github.com/NuGet/Home/issues/7517)</span></span>

#### <a name="issue"></a><span data-ttu-id="76b5b-146">문제</span><span class="sxs-lookup"><span data-stu-id="76b5b-146">Issue</span></span>
<span data-ttu-id="76b5b-147">소스 이름에 공백이 있으면 nuget.exe가 `The ' ' character, hexadecimal value 0x20, cannot be included in a name.` 같은 오류를 throw함</span><span class="sxs-lookup"><span data-stu-id="76b5b-147">When there is a whitespace in the source name, nuget.exe throws an error like `The ' ' character, hexadecimal value 0x20, cannot be included in a name.`</span></span>

#### <a name="workaround"></a><span data-ttu-id="76b5b-148">해결 방법</span><span class="sxs-lookup"><span data-stu-id="76b5b-148">Workaround</span></span>
<span data-ttu-id="76b5b-149">소스 이름에 공백이 포함되지 않도록 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="76b5b-149">Change the name of the source to not contain a whitespace.</span></span>

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a><span data-ttu-id="76b5b-150">dotnet nuget 푸시 --interactive로 인해 Mac에서 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="76b5b-150">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="76b5b-151"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="76b5b-151"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

#### <a name="issue"></a><span data-ttu-id="76b5b-152">문제</span><span class="sxs-lookup"><span data-stu-id="76b5b-152">Issue</span></span>
<span data-ttu-id="76b5b-153">`--interactive` 인수가 dotnet CLI에 의해 전달되지 않고 오류가 발생함 `error: Missing value for option 'interactive'`</span><span class="sxs-lookup"><span data-stu-id="76b5b-153">The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`</span></span>

#### <a name="workaround"></a><span data-ttu-id="76b5b-154">해결 방법</span><span class="sxs-lookup"><span data-stu-id="76b5b-154">Workaround</span></span>
<span data-ttu-id="76b5b-155">`dotnet restore --interactive` 같은 대화형 옵션을 사용하여 다른 dotnet 명령을 실행하고 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="76b5b-155">Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="76b5b-156">인증은 자격 증명 공급자에 의해 캐시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76b5b-156">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="76b5b-157">그런 다음, `dotnet nuget push`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="76b5b-157">Then run `dotnet nuget push`.</span></span>

### <a name="licenseacceptancewindow-and-licensefilewindow-accessibility-issues---7452httpsgithubcomnugethomeissues7452"></a><span data-ttu-id="76b5b-158">LicenseAcceptanceWindow 및 LicenseFileWindow 접근성 문제 - [#7452](https://github.com/NuGet/Home/issues/7452)</span><span class="sxs-lookup"><span data-stu-id="76b5b-158">LicenseAcceptanceWindow and LicenseFileWindow Accessibility issues - [#7452](https://github.com/NuGet/Home/issues/7452)</span></span>

#### <a name="issue"></a><span data-ttu-id="76b5b-159">문제</span><span class="sxs-lookup"><span data-stu-id="76b5b-159">Issue</span></span>
<span data-ttu-id="76b5b-160">화면 읽기 프로그램 및 JAWS를 사용한 내레이션 및 키보드 탐색과 관련해서 라이선스 동의 창 및 라이선스 파일 창에 접근성 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76b5b-160">The license acceptance window and license file window have accessibility issues with keyboard navigation and narration with screen reader and JAWS.</span></span>

#### <a name="workaround"></a><span data-ttu-id="76b5b-161">해결 방법</span><span class="sxs-lookup"><span data-stu-id="76b5b-161">Workaround</span></span>
<span data-ttu-id="76b5b-162">해결 방법이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="76b5b-162">No workaround.</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="76b5b-163">.NET Core SDK로 설치된 FallbackFolders의 패키지는 사용자 지정 설치되며 서명 유효성 검사에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="76b5b-163">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="76b5b-164"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="76b5b-164"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>

#### <a name="issue"></a><span data-ttu-id="76b5b-165">문제</span><span class="sxs-lookup"><span data-stu-id="76b5b-165">Issue</span></span>
<span data-ttu-id="76b5b-166">netcoreapp 1.x 및 netcoreapp 2.x 다중 대상을 지정하는 프로젝트를 복원하기 위해 dotnet.exe 2.x를 사용하면 대체 폴더가 파일 피드로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="76b5b-166">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="76b5b-167">즉 복원할 때 NuGet이 대체 폴더에서 패키지를 선택하고 전역 패키지 폴더에 설치하려고 하며 일반적인 서명 유효성 검사를 수행하지만 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="76b5b-167">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>

#### <a name="workaround"></a><span data-ttu-id="76b5b-168">해결 방법</span><span class="sxs-lookup"><span data-stu-id="76b5b-168">Workaround</span></span>
<span data-ttu-id="76b5b-169">`RestoreAdditionalProjectSources`를 nothing으로 설정하여 대체 폴더를 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="76b5b-169">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="76b5b-170">`<RestoreAdditionalProjectSources/>` NuGet.org에서 많은 패키지가 다운로드되도록 하므로 주의하여 사용하세요. 그렇지 않으면 대체 폴더에서 복원될 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="76b5b-170">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
