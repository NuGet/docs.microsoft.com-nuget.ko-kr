---
title: "NuGet 2.5 릴리스 정보 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr를 포함 하 여 NuGet 2.5에 대 한 릴리스 정보입니다."
keywords: "NuGet 2.5 릴리스 정보, 버그 수정, 알려진 문제, 추가 기능을 Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c2c6cf85b9ebccf200be9ef4a2bf96802cffcaea
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-25-release-notes"></a><span data-ttu-id="37237-104">NuGet 2.5 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="37237-104">NuGet 2.5 Release Notes</span></span>

<span data-ttu-id="37237-105">[NuGet 2.2.1 릴리스 정보](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 릴리스 정보](../release-notes/nuget-2.6.md)</span><span class="sxs-lookup"><span data-stu-id="37237-105">[NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md)</span></span>

<span data-ttu-id="37237-106">NuGet 2.5는 2013 년 4 월 25 일에 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="37237-106">NuGet 2.5 was released on April 25, 2013.</span></span> <span data-ttu-id="37237-107">이 릴리스가 크기가 매우 커서, 버전 2.3 및 2.4 건너뛸 해야 한다면 더 쉬워집니다.</span><span class="sxs-lookup"><span data-stu-id="37237-107">This release was so big, we felt compelled to skip versions 2.3 and 2.4!</span></span> <span data-ttu-id="37237-108">지금까지 있었던 NuGet에 대 한 가장 큰 릴리스는이 통해 [160 작업 항목](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) 릴리스에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="37237-108">To date, this is the largest release we've had for NuGet, with over [160 work items](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) in the release.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="37237-109">감사의 글</span><span class="sxs-lookup"><span data-stu-id="37237-109">Acknowledgements</span></span>

<span data-ttu-id="37237-110">NuGet 2.5로의 중요 한 기여에 대 한 다음과 같은 외부 참가자를 감사 하 고 싶습니다.</span><span class="sxs-lookup"><span data-stu-id="37237-110">We would like to thank the following external contributors for their significant contributions to NuGet 2.5:</span></span>

1. <span data-ttu-id="37237-111">[이 Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span><span class="sxs-lookup"><span data-stu-id="37237-111">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span></span>
    - <span data-ttu-id="37237-112">[#2847](https://nuget.codeplex.com/workitem/2847) -추가 MonoAndroid, MonoTouch, 및 MonoMac 알려진된 대상 프레임 워크 식별자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37237-112">[#2847](https://nuget.codeplex.com/workitem/2847) - Add MonoAndroid, MonoTouch, and MonoMac to the list of known target framework identifiers.</span></span>
1. <span data-ttu-id="37237-113">[Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span><span class="sxs-lookup"><span data-stu-id="37237-113">[Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span></span>
    - <span data-ttu-id="37237-114">[#2865](https://nuget.codeplex.com/workitem/2865) -의 철자를 수정 `NuGet.targets` 대/소문자 구분 OS에 대 한</span><span class="sxs-lookup"><span data-stu-id="37237-114">[#2865](https://nuget.codeplex.com/workitem/2865) - Fix spelling of `NuGet.targets` for a case-sensitive OS</span></span>
1. <span data-ttu-id="37237-115">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span><span class="sxs-lookup"><span data-stu-id="37237-115">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span></span>
    - <span data-ttu-id="37237-116">솔루션 모노에서 빌드를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="37237-116">Make the solution build on Mono.</span></span>
1. <span data-ttu-id="37237-117">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span><span class="sxs-lookup"><span data-stu-id="37237-117">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span></span>
    - <span data-ttu-id="37237-118">모노에서 실패 하는 단위 테스트를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="37237-118">Fix unit tests failing on Mono.</span></span>
1. <span data-ttu-id="37237-119">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span><span class="sxs-lookup"><span data-stu-id="37237-119">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span></span>
    - <span data-ttu-id="37237-120">[#2920](https://nuget.codeplex.com/workitem/2920) -nuget.exe 팩 명령 속성을 MSBuild 전파 하지 않습니다</span><span class="sxs-lookup"><span data-stu-id="37237-120">[#2920](https://nuget.codeplex.com/workitem/2920) - nuget.exe pack command does not propagate Properties to MSBuild</span></span>
1. <span data-ttu-id="37237-121">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span><span class="sxs-lookup"><span data-stu-id="37237-121">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span></span>
    - <span data-ttu-id="37237-122">[#1511](https://nuget.codeplex.com/workitem/1511) -수정 하는 XML 처리 코드를 서식 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="37237-122">[#1511](https://nuget.codeplex.com/workitem/1511) - Modified XML handling code to preserve formatting.</span></span>
1. <span data-ttu-id="37237-123">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span><span class="sxs-lookup"><span data-stu-id="37237-123">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span></span>
    - <span data-ttu-id="37237-124">성공 하려면 build.cmd 수 있도록 사용자 지정 사전에 인식 된 단어를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="37237-124">Added recognized words to custom dictionary to allow build.cmd to succeed.</span></span>
1. [<span data-ttu-id="37237-125">Bruno Roggeri</span><span class="sxs-lookup"><span data-stu-id="37237-125">Bruno Roggeri</span></span>](https://www.codeplex.com/site/users/view/broggeri)
    - <span data-ttu-id="37237-126">지역화 된 VS에서 실행할 때 단위 테스트를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="37237-126">Fix unit tests when running in localized VS.</span></span>
1. [<span data-ttu-id="37237-127">Gareth Evans</span><span class="sxs-lookup"><span data-stu-id="37237-127">Gareth Evans</span></span>](https://www.codeplex.com/site/users/view/garethevans)
    - <span data-ttu-id="37237-128">PackageService에서 추출 된 인터페이스</span><span class="sxs-lookup"><span data-stu-id="37237-128">Extracted interface from PackageService</span></span>
1. <span data-ttu-id="37237-129">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span><span class="sxs-lookup"><span data-stu-id="37237-129">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span></span>
    - <span data-ttu-id="37237-130">[#936](https://nuget.codeplex.com/workitem/936) -압축 하는 경우 프로젝트 종속성을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="37237-130">[#936](https://nuget.codeplex.com/workitem/936) - Handle project dependencies when packing</span></span>
1. <span data-ttu-id="37237-131">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span><span class="sxs-lookup"><span data-stu-id="37237-131">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span></span>
    - <span data-ttu-id="37237-132">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) -지원 일반 텍스트 암호 nuget.cofig 파일에 패키지 원본 자격 증명을 저장할 때</span><span class="sxs-lookup"><span data-stu-id="37237-132">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) - Support Clear Text Password when storing package source credentials in nuget.cofig files</span></span>
1. <span data-ttu-id="37237-133">[James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span><span class="sxs-lookup"><span data-stu-id="37237-133">[James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span></span>
    - <span data-ttu-id="37237-134">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) -패키지 가져오기 해결 도움말 설명</span><span class="sxs-lookup"><span data-stu-id="37237-134">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) - Fix Get-Package help description</span></span>

<span data-ttu-id="37237-135">또한와 NuGet 2.5 베타/RC 승인 또는 최종 릴리스 전에 해결 된 버그를 발견 하는 것에 대 한 다음 개인을 보내주셔서 감사:</span><span class="sxs-lookup"><span data-stu-id="37237-135">We also appreciate the following individuals for finding bugs with NuGet 2.5 Beta/RC that were approved and fixed before the final release:</span></span>

1. <span data-ttu-id="37237-136">[Tony 벽](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span><span class="sxs-lookup"><span data-stu-id="37237-136">[Tony Wall](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span></span>
    - <span data-ttu-id="37237-137">[#3200](https://nuget.codeplex.com/workitem/3200) -2.5 빌드되고 최신 NuGet 2.4 끊어진 MSTest</span><span class="sxs-lookup"><span data-stu-id="37237-137">[#3200](https://nuget.codeplex.com/workitem/3200) - MSTest broken with lastest NuGet 2.4 and 2.5 builds</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="37237-138">릴리스에서 주목할 만한 기능</span><span class="sxs-lookup"><span data-stu-id="37237-138">Notable features in the release</span></span>

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a><span data-ttu-id="37237-139">사용자가 이미 있는 콘텐츠 파일을 덮어쓸 수 있도록</span><span class="sxs-lookup"><span data-stu-id="37237-139">Allow users to overwrite content files that already exist</span></span>

<span data-ttu-id="37237-140">모든 시간을 가장 많이 요청한 기능 중 하나는 NuGet 패키지에 포함 하는 경우 디스크에 이미 있는 콘텐츠 파일을 덮어쓸 수 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="37237-140">One of the most requested features of all time has been the ability to overwrite content files that already exist on disk when included in a NuGet package.</span></span> <span data-ttu-id="37237-141">NuGet 2.5 부터는 이러한 충돌은 식별 되며 메시지가 표시 됩니다는 파일을 덮어쓸지 반면 이전에 이러한 파일을 항상 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="37237-141">Starting with NuGet 2.5, these conflicts are identified and you will be prompted to overwrite the files, whereas previously these files were always skipped.</span></span>

![콘텐츠 파일 덮어쓰기](./media/NuGet-2.5/overwrite-file.png)

<span data-ttu-id="37237-143">'nuget.exe 업데이트' 및 ' Install-package ' 새 옵션을 둘 다 이제 '-FileConflictAction' 명령줄 시나리오에 대 한 몇 가지 기본 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37237-143">'nuget.exe update' and 'Install-Package' now both have a new option '-FileConflictAction' to set some default for command-line scenarios.</span></span>

<span data-ttu-id="37237-144">패키지에서 파일 대상 프로젝트에 이미 있는 경우 기본 동작을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="37237-144">Set a default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="37237-145">항상 파일을 덮어쓰려면 '덮어쓰기'로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="37237-145">Set to 'Overwrite' to always overwrite files.</span></span> <span data-ttu-id="37237-146">파일을 건너 뛰을 '무시'로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="37237-146">Set to 'Ignore' to skip files.</span></span> <span data-ttu-id="37237-147">지정 하지 않으면 각 충돌 하는 파일에 대 한 라는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="37237-147">If not specified, it will prompt for each conflicting file.</span></span>

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a><span data-ttu-id="37237-148">MSBuild 대상 및 props 파일이 자동으로 가져오도록</span><span class="sxs-lookup"><span data-stu-id="37237-148">Automatic import of MSBuild targets and props files</span></span>

<span data-ttu-id="37237-149">NuGet 패키지의 최상위 수준에서 새 규칙에 따른 폴더 생성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="37237-149">A new conventional folder has been created at the top level of the NuGet package.</span></span>  <span data-ttu-id="37237-150">피어로 `\lib`, `\content`, 및 `\tools`, 이제 포함할 수 있습니다는 `\build` 패키지에는 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="37237-150">As a peer to `\lib`, `\content`, and `\tools`, you can now include a `\build` folder in your package.</span></span>  <span data-ttu-id="37237-151">이 폴더 아래에 고정 된 이름 가진 두 개의 파일을 배치할 수 있습니다 `{packageid}.targets` 또는 `{packageid}.props`합니다.</span><span class="sxs-lookup"><span data-stu-id="37237-151">Under this folder, you can place two files with fixed names, `{packageid}.targets` or `{packageid}.props`.</span></span> <span data-ttu-id="37237-152">이 두 일 수 직접 아래 `build` 보드나 다른 폴더 처럼 프레임 워크별 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="37237-152">These two files can be either directly under `build` or under framework-specific folders just like the other folders.</span></span> <span data-ttu-id="37237-153">가장 일치 하는 프레임 워크 폴더를 선택 하는 데 규칙은 정확히 동일 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="37237-153">The rule for picking the best-matched framework folder is exactly the same as in those.</span></span>

<span data-ttu-id="37237-154">MSBuild를 추가 합니다 \build 파일과 함께 NuGet 패키지는 설치 될 때 `<Import>` 가리키는 프로젝트 파일의 요소는 `.targets` 및 `.props` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="37237-154">When NuGet installs a package with \build files, it will add an MSBuild `<Import>` element in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="37237-155">`.props` 반면 맨 위에 있는 파일이 추가 되는 `.targets` 파일 맨 아래에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="37237-155">The `.props` file is added at the top, whereas the `.targets` file is added to the bottom.</span></span>

### <a name="specify-different-references-per-platform-using-references-element"></a><span data-ttu-id="37237-156">사용 하 여 플랫폼 마다 다른 참조를 지정 `<References/>` 요소</span><span class="sxs-lookup"><span data-stu-id="37237-156">Specify different references per platform using `<References/>` element</span></span>

<span data-ttu-id="37237-157">2.5에서는 이전에 `.nuspec` 파일인 사용자 추가할 모든 프레임 워크에 대 한 참조 파일을 지정할만 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37237-157">Before 2.5, in `.nuspec` file, user can only specify the reference files, to be added for all framework.</span></span> <span data-ttu-id="37237-158">2.5의이 새로운 기능, 사용자를 작성할 수 이제는 `<reference/>` 각 예제에 대 한 지원 되는 플랫폼에 대 한 요소:</span><span class="sxs-lookup"><span data-stu-id="37237-158">Now with this new feature in 2.5, user can author the `<reference/>` element for each of the supported platform, for example:</span></span>

```xml
<references>
    <group targetFramework="net45">
        <reference file="a.dll" />
    </group>
    <group targetFramework="netcore45">
        <reference file="b.dll" />
    </group>
    <group>
        <reference file="c.dll" />
    </group>
</references>
```

<span data-ttu-id="37237-159">NuGet에 따라 프로젝트에 대 한 참조를 추가 하는 방법에 대 한의 흐름이 고 `.nuspec` 파일:</span><span class="sxs-lookup"><span data-stu-id="37237-159">Here is the flow for how NuGet adds references to projects based on the `.nuspec` file:</span></span>

1. <span data-ttu-id="37237-160">찾기의 `lib` 대상 프레임 워크에 대 한 적합 하 고 해당 폴더에서 어셈블리의 목록을 가져올 수 있는 폴더</span><span class="sxs-lookup"><span data-stu-id="37237-160">Find the `lib` folder that is appropriate for the target framework and get the list of assemblies from that folder</span></span>
1. <span data-ttu-id="37237-161">대상 프레임 워크에 대 한 적절 한 포함 된 참조 그룹을 찾아 해당 그룹에서 어셈블리의 목록을 가져올 별도로 합니다.</span><span class="sxs-lookup"><span data-stu-id="37237-161">Separately find the references group that is appropriate for the target framework and get the list of assemblies from that group.</span></span> <span data-ttu-id="37237-162">지정 된 대상 프레임 워크 없이 참조 그룹은 대체 (fallback) 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="37237-162">Reference group without target framework specified is the fallback group.</span></span>
1. <span data-ttu-id="37237-163">두 목록의 교차를 찾아 추가할 참조로 사용 하는</span><span class="sxs-lookup"><span data-stu-id="37237-163">Find the intersection of the two lists, and use that as the references to add</span></span>

<span data-ttu-id="37237-164">이 새로운 기능을 사용 하면 패키지에서 여러 중복 어셈블리를 수행 하 고, 그렇지는 경우 어셈블리의 하위 집합 다양 한 프레임 워크에 적용할 참조 기능을 사용 하는 작성자 `lib` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="37237-164">This new feature will allow package authors to use the References feature to apply subsets of assemblies to different frameworks when they would otherwise need to carry duplicate assemblies in multiple `lib` folders.</span></span>

<span data-ttu-id="37237-165">참고: 현재 사용 해야 nuget.exe 팩;이 기능을 사용 하려면 NuGet 패키지 탐색기 아직 없으므로 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="37237-165">Note: you must presently use nuget.exe pack to use this feature; NuGet Package Explorer does not yet support it.</span></span>

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a><span data-ttu-id="37237-166">모든 패키지를 한 번에 업데이트를 허용 하는 모든 단추 업데이트</span><span class="sxs-lookup"><span data-stu-id="37237-166">Update All button to allow updating all packages at once</span></span>

<span data-ttu-id="37237-167">여러분 중 많은 알고 "업데이트 패키지" PowerShell cmdlet에 대 한 모든 패키지; 업데이트 이제 쉽게도 UI를 통해이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37237-167">Many of you know about the "Update-Package" PowerShell cmdlet to update all of your packages; now there's an easy way to do this through the UI as well.</span></span>

<span data-ttu-id="37237-168">이 기능을 사용해 보세요 하:</span><span class="sxs-lookup"><span data-stu-id="37237-168">To try this feature out:</span></span>

1. <span data-ttu-id="37237-169">새 ASP.NET MVC 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="37237-169">Create a new ASP.NET MVC application</span></span>
1. <span data-ttu-id="37237-170">NuGet 패키지 관리 ' 대화 상자를 시작</span><span class="sxs-lookup"><span data-stu-id="37237-170">Launch the 'Manage NuGet Packages' dialog</span></span>
1. <span data-ttu-id="37237-171">'업데이트'를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="37237-171">Select 'Updates'</span></span>
1. <span data-ttu-id="37237-172">' 업데이트 모두 ' 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="37237-172">Click the 'Update All' button</span></span>

![대화 상자에서 모든 단추 업데이트](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a><span data-ttu-id="37237-174">Nuget.exe 팩에 대 한 향상 된 프로젝트 참조 지원</span><span class="sxs-lookup"><span data-stu-id="37237-174">Improved project reference support for nuget.exe Pack</span></span>

<span data-ttu-id="37237-175">이제 nuget.exe 팩 명령 프로세스는 다음 규칙을 사용 하 여 프로젝트를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="37237-175">Now nuget.exe pack command processes referenced projects with the following rules:</span></span>

1. <span data-ttu-id="37237-176">참조 된 프로젝트에 해당 하는 경우 `.nuspec` 파일, 예를 들어 라는 파일은 `proj1.nuspec` 와 같은 폴더에 `proj1.csproj`, 그런 다음이 프로젝트 id를 사용 하 여 패키지를 종속성으로 추가 됩니다 및 버전에서 읽을 `.nuspec` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="37237-176">If the referenced project has corresponding `.nuspec` file, e.g. there is a file called `proj1.nuspec` in the same folder as `proj1.csproj`, then this project is added as a dependency to the package, using the id and version read from the `.nuspec` file.</span></span>
1. <span data-ttu-id="37237-177">그렇지 않은 경우 참조 된 프로젝트의 파일이 패키지에 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="37237-177">Otherwise, the files of the referenced project are bundled into the package.</span></span> <span data-ttu-id="37237-178">Sames 규칙 재귀적으로 사용 하 여이 프로젝트에서 참조 하는 프로젝트를 처리 한 다음 됩니다.</span><span class="sxs-lookup"><span data-stu-id="37237-178">Then projects referenced by this project will be processed using the sames rules recursively.</span></span>
1. <span data-ttu-id="37237-179">모든 DLL `.pdb`, 및 `.exe` 파일이 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="37237-179">All DLL, `.pdb`, and `.exe` files are added.</span></span>
1. <span data-ttu-id="37237-180">다른 모든 콘텐츠 파일이 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="37237-180">All other content files are added.</span></span>
1. <span data-ttu-id="37237-181">모든 종속성 병합 됩니다.</span><span class="sxs-lookup"><span data-stu-id="37237-181">All dependencies are merged.</span></span>

<span data-ttu-id="37237-182">이렇게 하면 참조 된 프로젝트가 없는 경우 종속 항목으로 간주 한 `.nuspec` 파일, 그렇지 않으면 패키지의 일부가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="37237-182">This allows a referenced project to be treated as a dependency if there is a `.nuspec` file, otherwise, it becomes part of the package.</span></span>

<span data-ttu-id="37237-183">자세한 내용은 여기: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span><span class="sxs-lookup"><span data-stu-id="37237-183">More details here: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span></span>

### <a name="add-a-minimum-nuget-version-property-to-packages"></a><span data-ttu-id="37237-184">패키지에 '는 최소 NuGet 버전 ' 속성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="37237-184">Add a 'Minimum NuGet Version' property to packages</span></span>

<span data-ttu-id="37237-185">새 메타 데이터 특성 'minClientVersion' 라는 패키지를 사용 하는 데 필요한 최소 NuGet 클라이언트 버전을 나타낼 이제 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37237-185">A new metadata attribute called 'minClientVersion' can now indicate the minimum NuGet client version required to consume a package.</span></span>

<span data-ttu-id="37237-186">이 기능을 사용 하면 패키지를 만든 후에 특정 버전의 NuGet 패키지 작동 하는지 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37237-186">This feature helps package author to specify that a package will work only after a particular version of NuGet.</span></span> <span data-ttu-id="37237-187">새 `.nuspec` NuGet 2.5 후 패키지를 최소 NuGet 버전 요청할 됩니다 하는 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="37237-187">As new `.nuspec` features are added after NuGet 2.5, packages will be able to claim a minimum NuGet version.</span></span>

```xml
<metadata minClientVersion="2.6">
```

<span data-ttu-id="37237-188">사용자에 게 NuGet 2.5가 설치 되어 있고 2.6 필요한 것으로 식별 되는 패키지, 시각 신호를 패키지를 설치할 수는 사용자에 게 주어 집니다.</span><span class="sxs-lookup"><span data-stu-id="37237-188">If the user has NuGet 2.5 installed and a package is identified as requiring 2.6, visual cues will be given to the user indicating the package will not be installable.</span></span> <span data-ttu-id="37237-189">사용자가 해당 버전의 NuGet이를 업데이트 하려면 다음 안내 됩니다.</span><span class="sxs-lookup"><span data-stu-id="37237-189">The user will then be guided to update their version of NuGet.</span></span>

<span data-ttu-id="37237-190">이 패키지를 설치 하 고 다음 인식할 수 없는 스키마 버전 확인 됨을 나타내는 실패 시작 하는 위치는 기존 환경을 보다 개선 됩니다.</span><span class="sxs-lookup"><span data-stu-id="37237-190">This will improve upon the existing experience where packages begin to install but then fail indicating an unrecognized schema version was identified.</span></span>

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a><span data-ttu-id="37237-191">종속성은 패키지를 설치 하는 동안 불필요 하 게 더 이상 업데이트</span><span class="sxs-lookup"><span data-stu-id="37237-191">Dependencies are no longer unnecessarily updated during package installation</span></span>

<span data-ttu-id="37237-192">NuGet 2.5 하기 전에 패키지는 프로젝트에 이미 설치 된 패키지에 의존 하는 설치 될 때 종속성 업데이트 됩니다 새 설치의 일부로 기존 버전의 종속성을 충족 하는 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="37237-192">Before NuGet 2.5, when a package was installed that depended on a package already installed in the project, the dependency would be updated as part of the new installation, even if the existing version satisfied the dependency.</span></span>

<span data-ttu-id="37237-193">종속성의 버전을 충족 하는 이미 없으면 NuGet 2.5 부터는 종속성 업데이트 되지 않습니다 다른 패키지 설치 중입니다.</span><span class="sxs-lookup"><span data-stu-id="37237-193">Starting with NuGet 2.5, if a dependency version is already satisfied, the dependency will not be updated during other package installations.</span></span>

<span data-ttu-id="37237-194">**시나리오:**</span><span class="sxs-lookup"><span data-stu-id="37237-194">**The scenario:**</span></span>

1. <span data-ttu-id="37237-195">소스 저장소 B 패키지 버전 1.0.0 및 1.0.2 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37237-195">The source repository contains package B with version 1.0.0 and 1.0.2.</span></span> <span data-ttu-id="37237-196">패키지 A가 B에 종속 된도 포함 되어 (> = 1.0.0).</span><span class="sxs-lookup"><span data-stu-id="37237-196">It also contains package A which has a dependency on B (>= 1.0.0).</span></span>
1. <span data-ttu-id="37237-197">현재 프로젝트에 이미 B 패키지 버전 1.0.0 설치 되어 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="37237-197">Assume that the current project already has package B version 1.0.0 installed.</span></span> <span data-ttu-id="37237-198">이제 1. 패키지를 설치</span><span class="sxs-lookup"><span data-stu-id="37237-198">Now you want to install package A.</span></span>

<span data-ttu-id="37237-199">**에 NuGet 2.2 및 이전 버전:**</span><span class="sxs-lookup"><span data-stu-id="37237-199">**In NuGet 2.2 and older:**</span></span>

* <span data-ttu-id="37237-200">패키지 A를 설치할 때 NuGet는 자동 업데이트 B 1.0.2 1.0.0 기존 버전에는 이미 되는 종속성 버전 제약 조건을 만족 하는 경우에 > 1.0.0 = 합니다.</span><span class="sxs-lookup"><span data-stu-id="37237-200">When installing package A, NuGet will auto-update B to 1.0.2, even though the existing version 1.0.0 already satisfies the dependency version constraint, which is >= 1.0.0.</span></span>

<span data-ttu-id="37237-201">**에 NuGet 2.5 이상 버전:**</span><span class="sxs-lookup"><span data-stu-id="37237-201">**In NuGet 2.5 and newer:**</span></span>

* <span data-ttu-id="37237-202">기존 버전 1.0.0 종속성 버전 제약 조건을 만족 하는 것이 있기 때문 NuGet 더 이상 B를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="37237-202">NuGet will no longer update B, because it detects that the existing version 1.0.0 satisfies the dependency version constraint.</span></span>

<span data-ttu-id="37237-203">이러한 변경 사항에 자세한 배경을 알고 싶으면, 자세한 읽기 [작업 항목](http://nuget.codeplex.com/workitem/1681) 관련 뿐만 아니라 [토론 스레드](http://nuget.codeplex.com/discussions/436712)합니다.</span><span class="sxs-lookup"><span data-stu-id="37237-203">For more background on this change, read the detailed [work item](http://nuget.codeplex.com/workitem/1681) as well as the related [discussion thread](http://nuget.codeplex.com/discussions/436712).</span></span>

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a><span data-ttu-id="37237-204">nuget.exe 출력의 자세한 정도 http 요청</span><span class="sxs-lookup"><span data-stu-id="37237-204">nuget.exe outputs http requests with detailed verbosity</span></span>

<span data-ttu-id="37237-205">Nuget.exe 문제를 해결 하거나 just 하는 경우 자세한 내용을 보려면 어떤 HTTP 요청이 작업 중 수행 되는 '-자세한 세부 정보 표시 ' 스위치 이제 만든 모든 HTTP 요청을 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="37237-205">If you are troubleshooting nuget.exe or just curious what HTTP requests are made during operations, the '-verbosity detailed' switch will now output all HTTP requests made.</span></span>

![HTTP output from nuget.exe](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a><span data-ttu-id="37237-207">nuget.exe 푸시 UNC 및 폴더 원본 지원</span><span class="sxs-lookup"><span data-stu-id="37237-207">nuget.exe push now supports UNC and folder sources</span></span>

<span data-ttu-id="37237-208">NuGet 2.5 하기 전에 로컬 폴더 또는 UNC 경로 기반으로 하는 패키지 소스에 'nuget.exe 푸시'를 실행 하려고 하는 경우 push 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="37237-208">Before NuGet 2.5, if you attempted to run 'nuget.exe push' to a package source based on a UNC path or local folder, the push would fail.</span></span> <span data-ttu-id="37237-209">최근에 추가 된 계층적 구성 기능을 사용 하면 nuget.exe를 대상으로 지정 된 UNC/폴더 원본 또는 HTTP 기반 NuGet 갤러리를 일반화 했습니다.</span><span class="sxs-lookup"><span data-stu-id="37237-209">With the recently added hierarchical configuration feature, it had become common for nuget.exe to need to target either a UNC/folder source, or an HTTP-based NuGet Gallery.</span></span>

<span data-ttu-id="37237-210">Nuget.exe UNC/폴더 소스를 식별 하는 경우 NuGet 2.5 부터는 파일 복사는 소스를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="37237-210">Starting with NuGet 2.5, if nuget.exe identifies a UNC/folder source, it will perform the file copy to the source.</span></span>

<span data-ttu-id="37237-211">다음 명령은 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="37237-211">The following command will now work:</span></span>

```
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a><span data-ttu-id="37237-212">nuget.exe은 명시적으로 지정 된 구성 파일을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="37237-212">nuget.exe supports explicitly-specified Config files</span></span>

<span data-ttu-id="37237-213">이제 구성 ('사양' 및 '팩'를 제외한 모든)에 액세스 하는 nuget.exe 명령을 새 지원 '-ConfigFile' 옵션을 강제로 특정 config 파일을 %AppData%\nuget\Nuget.Config 기본 구성 파일 대신 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37237-213">nuget.exe commands that access configuration (all except 'spec' and 'pack') now support a new '-ConfigFile' option, which forces a specific config file to be used in place of the default config file at %AppData%\nuget\Nuget.Config.</span></span>

<span data-ttu-id="37237-214">예제:</span><span class="sxs-lookup"><span data-stu-id="37237-214">Example:</span></span>

```
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a><span data-ttu-id="37237-215">네이티브 프로젝트에 대 한 지원</span><span class="sxs-lookup"><span data-stu-id="37237-215">Support for Native projects</span></span>

<span data-ttu-id="37237-216">NuGet 2.5로 NuGet 도구 Visual Studio의 네이티브 프로젝트에 대 한 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="37237-216">With NuGet 2.5, the NuGet tooling is now available for Native projects in Visual Studio.</span></span> <span data-ttu-id="37237-217">작업도 수행 하지 가장 네이티브 패키지는 위의 MSBuild 가져오기 기능을 사용 하 여 만든 도구를 사용 하 여 [CoApp 프로젝트](http://coapp.org)합니다.</span><span class="sxs-lookup"><span data-stu-id="37237-217">We expect most native packages will utilize the MSBuild imports feature above, using a tool created by the [CoApp project](http://coapp.org).</span></span> <span data-ttu-id="37237-218">자세한 내용은 [도구에 대 한 세부 정보](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) coapp.org 웹사이트에서.</span><span class="sxs-lookup"><span data-stu-id="37237-218">For more information, read [the details about the tool](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) on the coapp.org website.</span></span>

<span data-ttu-id="37237-219">네이티브 프로젝트에 패키지를 설치할 때 \build, \content, 및 \tools에 파일을 포함 하는 패키지에 대 한 "기본"의 대상 프레임 워크 이름을 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="37237-219">The target framework name of "native" is introduced for packages to include files in \build, \content, and \tools when the package is installed into a native project.</span></span>  <span data-ttu-id="37237-220">\`lib' 폴더는 네이티브 프로젝트에 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="37237-220">The \`lib` folder is not used for native projects.</span></span>
