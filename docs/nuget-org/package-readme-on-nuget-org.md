---
title: NuGet.org의 패키지 추가 정보
description: NuGet.org의 추가 정보 파일이 렌더링되는 방법 및 문제가 발생할 경우 수행할 작업에 대한 자세한 설명입니다.
author: chgill-MSFT
ms.author: chgill
ms.date: 02/23/2021
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: a5d68329128c9e9d047fe10e08ce41f1ae0895b4
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2021
ms.locfileid: "107902229"
---
# <a name="package-readme-on-nugetorg"></a><span data-ttu-id="492cf-103">NuGet.org의 패키지 추가 정보</span><span class="sxs-lookup"><span data-stu-id="492cf-103">Package readme on NuGet.org</span></span>

<span data-ttu-id="492cf-104">사용자에게 더 풍부하고 자세한 패키지 세부 정보를 제공하기 위해 [NuGet 패키지에 추가 정보 파일을 포함합니다](https://docs.microsoft.com/nuget/reference/msbuild-targets#packagereadmefile).</span><span class="sxs-lookup"><span data-stu-id="492cf-104">[Include a readme file in your NuGet package](https://docs.microsoft.com/nuget/reference/msbuild-targets#packagereadmefile) to make your package details richer and more informative for your users!</span></span>

<span data-ttu-id="492cf-105">이는 사용자가 NuGet.org에서 패키지 세부 정보 페이지를 볼 때 첫 번째로 표시되는 요소 중 하나이며 좋은 인상을 주는 데 필수적입니다!</span><span class="sxs-lookup"><span data-stu-id="492cf-105">This is likely one of the first elements users will see when they view your package details page on NuGet.org and is essential to making a good impression!</span></span>

> [!IMPORTANT]
> <span data-ttu-id="492cf-106">NuGet.org는 [Markdown](https://daringfireball.net/projects/markdown/) 및 제한된 도메인 집합의 이미지에 있는 추가 정보 파일만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="492cf-106">NuGet.org only supports readme files in [Markdown](https://daringfireball.net/projects/markdown/) and images from a limited set of domains.</span></span> <span data-ttu-id="492cf-107">NuGet.org에서 추가 정보가 올바르게 렌더링되도록 [이미지](#allowed-domains-for-images-and-badges) 및 [지원되는 Markdown 기능](#supported-markdown-features)에 대해 허용된 도메인을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="492cf-107">See our [allowed domains for images](#allowed-domains-for-images-and-badges) and [supported Markdown features](#supported-markdown-features) to ensure your readme renders correctly on NuGet.org.</span></span>

## <a name="what-should-my-readme-include"></a><span data-ttu-id="492cf-108">추가 정보에는 무엇이 포함되나요?</span><span class="sxs-lookup"><span data-stu-id="492cf-108">What should my readme include?</span></span>

<span data-ttu-id="492cf-109">추가 정보에 다음 항목을 포함하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="492cf-109">Consider including the following items in your readme:</span></span>
* <span data-ttu-id="492cf-110">패키지의 정의 및 기능 소개 - 어떤 문제를 해결할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="492cf-110">An introduction to what your package is and does - what problems does it solve?</span></span>
* <span data-ttu-id="492cf-111">패키지를 시작하는 방법 - 특정 요구 사항이 있나요?</span><span class="sxs-lookup"><span data-stu-id="492cf-111">How to get started with your package - are there any specific requirements?</span></span>
* <span data-ttu-id="492cf-112">추가 정보에 포함되지 않은 경우 보다 포괄적인 설명서에 대한 링크.</span><span class="sxs-lookup"><span data-stu-id="492cf-112">Links to more comprehensive documentation if not included in the readme itself.</span></span>
* <span data-ttu-id="492cf-113">최소 몇 가지 코드 조각/샘플 또는 예제 이미지.</span><span class="sxs-lookup"><span data-stu-id="492cf-113">At least a few code snippets/samples or example images.</span></span>
* <span data-ttu-id="492cf-114">프로젝트 문제, Twitter, 버그 추적기 또는 기타 플랫폼에 대한 링크와 같은 피드백을 남기는 위치 및 방법.</span><span class="sxs-lookup"><span data-stu-id="492cf-114">Where and how to leave feedback such as link to the project issues, Twitter, bug tracker, or other platform.</span></span>
* <span data-ttu-id="492cf-115">해당하는 경우 기여하는 방법.</span><span class="sxs-lookup"><span data-stu-id="492cf-115">How to contribute, if applicable.</span></span>

<span data-ttu-id="492cf-116">고품질 추가 정보는 다양한 형식, 형태 및 크기로 구성될 수 있습니다!</span><span class="sxs-lookup"><span data-stu-id="492cf-116">Keep in mind, high quality readmes can come in a wide variety of formats, shapes, and sizes!</span></span> <span data-ttu-id="492cf-117">NuGet.org에서 사용할 수 있는 패키지가 이미 있는 경우, NuGet.org 세부 정보 페이지에 추가될 수 있는 `readme.md` 또는 다른 문서 파일이 리포지토리에 이미 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="492cf-117">If you already have a package available on NuGet.org, chances are that you already have a `readme.md` or other documentation file in your repository that would be a great addition to your NuGet.org details page.</span></span>

## <a name="preview-your-readme"></a><span data-ttu-id="492cf-118">추가 정보 미리 보기</span><span class="sxs-lookup"><span data-stu-id="492cf-118">Preview your readme</span></span>

<span data-ttu-id="492cf-119">NuGet.org에 출시되기 전에 추가 정보 파일을 미리 보려면 [NuGet.org에서 업로드 패키지 웹 포털](https://docs.microsoft.com/nuget/nuget-org/publish-a-package#web-portal-use-the-upload-package-tab-on-nugetorg)을 사용하여 패키지를 업로드하고 메타데이터 미리 보기의 ‘추가 정보 파일’ 섹션으로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="492cf-119">To preview your readme file before it's live on NuGet.org, upload your package using the [Upload Package web portal on NuGet.org](https://docs.microsoft.com/nuget/nuget-org/publish-a-package#web-portal-use-the-upload-package-tab-on-nugetorg) and scroll down to the "Readme File" section of the metadata preview.</span></span> <span data-ttu-id="492cf-120">다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="492cf-120">It should look something like this:</span></span>

![추가 정보 파일 미리 보기](media\readme-upload-preview.PNG)

<span data-ttu-id="492cf-122">잠재적 사용자에게 강한 첫 인상을 줄 수 있도록 [이미지 규정 준수](#allowed-domains-for-images-and-badges) 및 [지원되는 형식](#supported-markdown-features)에 대한 추가 정보 파일을 검토하고 미리 보는 것을 고려하세요!</span><span class="sxs-lookup"><span data-stu-id="492cf-122">Consider taking time to review and preview your readme file for [image compliance](#allowed-domains-for-images-and-badges) and [supported formatting](#supported-markdown-features) to make sure it gives a great first impression to potential users!</span></span> <span data-ttu-id="492cf-123">패키지 추가 정보를 NuGet.org에 게시한 후 수정하려면 수정 사항을 적용한 업데이트된 패키지 버전을 푸시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="492cf-123">To correct mistakes on your package readme once it's published to NuGet.org, you will need to push an updated package version with the fix.</span></span> <span data-ttu-id="492cf-124">모든 사항이 제대로 표시되는지 미리 확인하면 잠재적인 문제를 피할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="492cf-124">Making sure everything looks good in advance may save you headache down the road.</span></span>
## <a name="allowed-domains-for-images-and-badges"></a><span data-ttu-id="492cf-125">이미지 및 배지에 대해 허용된 도메인</span><span class="sxs-lookup"><span data-stu-id="492cf-125">Allowed domains for images and badges</span></span>

<span data-ttu-id="492cf-126">보안 및 개인 정보 문제로 인해 NuGet.org는 이미지 및 배지를 신뢰할 수 있는 호스트로 렌더링할 수 있는 도메인으로 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="492cf-126">Due to security and privacy concerns, NuGet.org restricts the domains from which images and badges can be rendered to trusted hosts.</span></span> 

<span data-ttu-id="492cf-127">NuGet.org를 사용하면 다음 신뢰할 수 있는 도메인에서 배지를 비롯한 모든 이미지를 렌더링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="492cf-127">NuGet.org allows all images, including badges, from the following trusted domains to be rendered:</span></span>
* <span data-ttu-id="492cf-128">api.bintray.com</span><span class="sxs-lookup"><span data-stu-id="492cf-128">api.bintray.com</span></span>
* <span data-ttu-id="492cf-129">api.codacy.com</span><span class="sxs-lookup"><span data-stu-id="492cf-129">api.codacy.com</span></span>
* <span data-ttu-id="492cf-130">api.codeclimate.com</span><span class="sxs-lookup"><span data-stu-id="492cf-130">api.codeclimate.com</span></span>
* <span data-ttu-id="492cf-131">api.dependabot.com</span><span class="sxs-lookup"><span data-stu-id="492cf-131">api.dependabot.com</span></span>
* <span data-ttu-id="492cf-132">api.travis-ci.com</span><span class="sxs-lookup"><span data-stu-id="492cf-132">api.travis-ci.com</span></span>
* <span data-ttu-id="492cf-133">api.travis-ci.org</span><span class="sxs-lookup"><span data-stu-id="492cf-133">api.travis-ci.org</span></span>
* <span data-ttu-id="492cf-134">app.fossa.io</span><span class="sxs-lookup"><span data-stu-id="492cf-134">app.fossa.io</span></span>
* <span data-ttu-id="492cf-135">badge.fury.io</span><span class="sxs-lookup"><span data-stu-id="492cf-135">badge.fury.io</span></span>
* <span data-ttu-id="492cf-136">badgen.net</span><span class="sxs-lookup"><span data-stu-id="492cf-136">badgen.net</span></span>
* <span data-ttu-id="492cf-137">badges.gitter.im</span><span class="sxs-lookup"><span data-stu-id="492cf-137">badges.gitter.im</span></span>
* <span data-ttu-id="492cf-138">bettercodehub.com</span><span class="sxs-lookup"><span data-stu-id="492cf-138">bettercodehub.com</span></span>
* <span data-ttu-id="492cf-139">buildstats.info</span><span class="sxs-lookup"><span data-stu-id="492cf-139">buildstats.info</span></span>
* <span data-ttu-id="492cf-140">camo.githubusercontent.com</span><span class="sxs-lookup"><span data-stu-id="492cf-140">camo.githubusercontent.com</span></span>
* <span data-ttu-id="492cf-141">ci.appveyor.com</span><span class="sxs-lookup"><span data-stu-id="492cf-141">ci.appveyor.com</span></span>
* <span data-ttu-id="492cf-142">circleci.com</span><span class="sxs-lookup"><span data-stu-id="492cf-142">circleci.com</span></span>
* <span data-ttu-id="492cf-143">codecov.io</span><span class="sxs-lookup"><span data-stu-id="492cf-143">codecov.io</span></span>
* <span data-ttu-id="492cf-144">codefactor.io</span><span class="sxs-lookup"><span data-stu-id="492cf-144">codefactor.io</span></span>
* <span data-ttu-id="492cf-145">coveralls.io</span><span class="sxs-lookup"><span data-stu-id="492cf-145">coveralls.io</span></span>
* <span data-ttu-id="492cf-146">dev.azure.com</span><span class="sxs-lookup"><span data-stu-id="492cf-146">dev.azure.com</span></span>
* <span data-ttu-id="492cf-147">github.com/.../workflows/.../badge.svg</span><span class="sxs-lookup"><span data-stu-id="492cf-147">github.com/.../workflows/.../badge.svg</span></span>
* <span data-ttu-id="492cf-148">gitlab.com</span><span class="sxs-lookup"><span data-stu-id="492cf-148">gitlab.com</span></span>
* <span data-ttu-id="492cf-149">img.shields.io</span><span class="sxs-lookup"><span data-stu-id="492cf-149">img.shields.io</span></span>
* <span data-ttu-id="492cf-150">isitmaintained.com</span><span class="sxs-lookup"><span data-stu-id="492cf-150">isitmaintained.com</span></span>
* <span data-ttu-id="492cf-151">opencollective.com</span><span class="sxs-lookup"><span data-stu-id="492cf-151">opencollective.com</span></span>
* <span data-ttu-id="492cf-152">raw.github.com</span><span class="sxs-lookup"><span data-stu-id="492cf-152">raw.github.com</span></span>
* <span data-ttu-id="492cf-153">raw.githubusercontent.com</span><span class="sxs-lookup"><span data-stu-id="492cf-153">raw.githubusercontent.com</span></span>
* <span data-ttu-id="492cf-154">snyk.io</span><span class="sxs-lookup"><span data-stu-id="492cf-154">snyk.io</span></span>
* <span data-ttu-id="492cf-155">sonarcloud.io</span><span class="sxs-lookup"><span data-stu-id="492cf-155">sonarcloud.io</span></span>
* <span data-ttu-id="492cf-156">user-images.githubusercontent.com</span><span class="sxs-lookup"><span data-stu-id="492cf-156">user-images.githubusercontent.com</span></span>

<span data-ttu-id="492cf-157">다른 도메인을 허용 목록에 추가해야 하는 경우 [문제를 제출하면](https://github.com/NuGet/NuGetGallery/issues) 엔지니어링 팀에서 개인 정보 보호 및 보안 규정 준수에 대해 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="492cf-157">If you feel that another domain should be added to the allow-list, please feel free to [file an issue](https://github.com/NuGet/NuGetGallery/issues) and it will be reviewed by our engineering team for privacy and security compliance.</span></span> <span data-ttu-id="492cf-158">상대적인 로컬 경로의 이미지와 지원되지 않는 도메인에서 호스트된 이미지는 렌더링되지 않으며 패키지 소유자에게만 표시되는 추가 정보 파일 미리 보기 및 패키지 세부 정보 페이지에서 경고를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="492cf-158">Images with relative local paths and images hosted from unsupported domains will not be rendered and will produce a warning on the readme file preview and package details page that is only visible to the package owners.</span></span>

## <a name="supported-markdown-features"></a><span data-ttu-id="492cf-159">지원되는 Markdown 기능</span><span class="sxs-lookup"><span data-stu-id="492cf-159">Supported Markdown features</span></span>
<span data-ttu-id="492cf-160">[Markdown](https://daringfireball.net/projects/markdown/)은 일반 텍스트 서식 구문을 사용하는 경량 생성 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="492cf-160">[Markdown](https://daringfireball.net/projects/markdown/) is a lightweight markup language with plain text formatting syntax.</span></span> <span data-ttu-id="492cf-161">NuGet.org 추가 정보는 [Markdig](https://github.com/lunet-io/markdig) 구문 분석 엔진을 통해 [CommonMark](https://commonmark.org/) 규격 Markdown을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="492cf-161">NuGet.org readmes support [CommonMark](https://commonmark.org/) compliant Markdown through the [Markdig](https://github.com/lunet-io/markdig) parsing engine.</span></span>

<span data-ttu-id="492cf-162">NuGet.org는 현재 다음 Markdown 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="492cf-162">NuGet.org currently supports the following Markdown features:</span></span>
* [<span data-ttu-id="492cf-163">헤더</span><span class="sxs-lookup"><span data-stu-id="492cf-163">Headers</span></span>](https://spec.commonmark.org/0.29/#atx-headings)
* [<span data-ttu-id="492cf-164">이미지</span><span class="sxs-lookup"><span data-stu-id="492cf-164">Images</span></span>](https://spec.commonmark.org/0.29/#images)
* [<span data-ttu-id="492cf-165">추가 강조</span><span class="sxs-lookup"><span data-stu-id="492cf-165">Extra emphasis</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmphasisExtraSpecs.md)
* [<span data-ttu-id="492cf-166">목록</span><span class="sxs-lookup"><span data-stu-id="492cf-166">Lists</span></span>](https://spec.commonmark.org/0.29/#lists)
* [<span data-ttu-id="492cf-167">연결</span><span class="sxs-lookup"><span data-stu-id="492cf-167">Links</span></span>](https://spec.commonmark.org/0.29/#links)
* [<span data-ttu-id="492cf-168">블록 따옴표</span><span class="sxs-lookup"><span data-stu-id="492cf-168">Block quotes</span></span>](https://spec.commonmark.org/0.29/#block-quotes)
* [<span data-ttu-id="492cf-169">백슬래시 이스케이프</span><span class="sxs-lookup"><span data-stu-id="492cf-169">Backslash escapes</span></span>](https://spec.commonmark.org/0.29/#backslash-escapes)
* [<span data-ttu-id="492cf-170">코드 범위</span><span class="sxs-lookup"><span data-stu-id="492cf-170">Code spans</span></span>](https://spec.commonmark.org/0.29/#code-spans)
* [<span data-ttu-id="492cf-171">작업 목록</span><span class="sxs-lookup"><span data-stu-id="492cf-171">Task lists</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/TaskListSpecs.md)
* [<span data-ttu-id="492cf-172">테이블</span><span class="sxs-lookup"><span data-stu-id="492cf-172">Tables</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/PipeTableSpecs.md)
* [<span data-ttu-id="492cf-173">이모지</span><span class="sxs-lookup"><span data-stu-id="492cf-173">Emojis</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmojiSpecs.md)
* [<span data-ttu-id="492cf-174">자동 링크</span><span class="sxs-lookup"><span data-stu-id="492cf-174">Auto-links</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/AutoLinks.md)

