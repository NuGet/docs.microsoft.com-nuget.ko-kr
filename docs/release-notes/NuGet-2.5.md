---
title: NuGet 2.5 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 Ecrs를 비롯 한 NuGet 2.5에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 940582d5173f5a53dcd04cf1258fc02a2439af4e
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825289"
---
# <a name="nuget-25-release-notes"></a><span data-ttu-id="f1e3f-103">NuGet 2.5 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="f1e3f-103">NuGet 2.5 Release Notes</span></span>

<span data-ttu-id="f1e3f-104">Nuget [2.2.1 릴리스 정보](../release-notes/nuget-2.2.1.md) | [Nuget 2.6 릴리스 정보](../release-notes/nuget-2.6.md)</span><span class="sxs-lookup"><span data-stu-id="f1e3f-104">[NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md)</span></span>

<span data-ttu-id="f1e3f-105">NuGet 2.5은 2013 년 4 월 25 일에 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-105">NuGet 2.5 was released on April 25, 2013.</span></span> <span data-ttu-id="f1e3f-106">이 릴리스는 너무 하도록 강요 되 버전 2.3 및 2.4를 건너 뛰 세요.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-106">This release was so big, we felt compelled to skip versions 2.3 and 2.4!</span></span> <span data-ttu-id="f1e3f-107">최신 버전은 NuGet에 대해 보유 한 가장 큰 릴리스입니다. 릴리스의 [작업 항목 수가 160](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) 이상입니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-107">To date, this is the largest release we've had for NuGet, with over [160 work items](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) in the release.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="f1e3f-108">승인</span><span class="sxs-lookup"><span data-stu-id="f1e3f-108">Acknowledgements</span></span>

<span data-ttu-id="f1e3f-109">NuGet 2.5에 대 한 중요 한 기여에 대해 다음과 같은 외부 참가자에 게 감사 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-109">We would like to thank the following external contributors for their significant contributions to NuGet 2.5:</span></span>

1. <span data-ttu-id="f1e3f-110">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span><span class="sxs-lookup"><span data-stu-id="f1e3f-110">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span></span>
    - <span data-ttu-id="f1e3f-111">[#2847](https://nuget.codeplex.com/workitem/2847) -알려진 대상 프레임 워크 식별자 목록에 MonoAndroid, Monotouch.dialog 및 MonoMac를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-111">[#2847](https://nuget.codeplex.com/workitem/2847) - Add MonoAndroid, MonoTouch, and MonoMac to the list of known target framework identifiers.</span></span>
2. <span data-ttu-id="f1e3f-112">[Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span><span class="sxs-lookup"><span data-stu-id="f1e3f-112">[Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span></span>
    - <span data-ttu-id="f1e3f-113">[#2865](https://nuget.codeplex.com/workitem/2865) -대/소문자를 구분 하는 OS에 대 한 `NuGet.targets`의 맞춤법 수정</span><span class="sxs-lookup"><span data-stu-id="f1e3f-113">[#2865](https://nuget.codeplex.com/workitem/2865) - Fix spelling of `NuGet.targets` for a case-sensitive OS</span></span>
3. <span data-ttu-id="f1e3f-114">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span><span class="sxs-lookup"><span data-stu-id="f1e3f-114">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span></span>
    - <span data-ttu-id="f1e3f-115">Mono에서 솔루션 빌드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-115">Make the solution build on Mono.</span></span>
4. <span data-ttu-id="f1e3f-116">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span><span class="sxs-lookup"><span data-stu-id="f1e3f-116">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span></span>
    - <span data-ttu-id="f1e3f-117">Mono에서 실패 한 단위 테스트를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-117">Fix unit tests failing on Mono.</span></span>
5. <span data-ttu-id="f1e3f-118">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span><span class="sxs-lookup"><span data-stu-id="f1e3f-118">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span></span>
    - <span data-ttu-id="f1e3f-119">[#2920](https://nuget.codeplex.com/workitem/2920) -nuget.exe Pack 명령은 속성을 MSBuild에 전파 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-119">[#2920](https://nuget.codeplex.com/workitem/2920) - nuget.exe pack command does not propagate Properties to MSBuild</span></span>
6. <span data-ttu-id="f1e3f-120">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span><span class="sxs-lookup"><span data-stu-id="f1e3f-120">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span></span>
    - <span data-ttu-id="f1e3f-121">서식 지정을 유지 하기 위해 [#1511](https://nuget.codeplex.com/workitem/1511) 수정 된 XML 처리 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-121">[#1511](https://nuget.codeplex.com/workitem/1511) - Modified XML handling code to preserve formatting.</span></span>
7. <span data-ttu-id="f1e3f-122">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span><span class="sxs-lookup"><span data-stu-id="f1e3f-122">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span></span>
    - <span data-ttu-id="f1e3f-123">사용자 지정 사전에 인식할 수 있는 단어를 추가 하 여 빌드 .cmd가 성공 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-123">Added recognized words to custom dictionary to allow build.cmd to succeed.</span></span>
8. [<span data-ttu-id="f1e3f-124">Bruno Roggeri</span><span class="sxs-lookup"><span data-stu-id="f1e3f-124">Bruno Roggeri</span></span>](https://www.codeplex.com/site/users/view/broggeri)
    - <span data-ttu-id="f1e3f-125">지역화 된 VS에서 실행 될 때 단위 테스트 수정</span><span class="sxs-lookup"><span data-stu-id="f1e3f-125">Fix unit tests when running in localized VS.</span></span>
9. [<span data-ttu-id="f1e3f-126">Gareth Evans</span><span class="sxs-lookup"><span data-stu-id="f1e3f-126">Gareth Evans</span></span>](https://www.codeplex.com/site/users/view/garethevans)
    - <span data-ttu-id="f1e3f-127">PackageService에서 추출 된 인터페이스</span><span class="sxs-lookup"><span data-stu-id="f1e3f-127">Extracted interface from PackageService</span></span>
10. <span data-ttu-id="f1e3f-128">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span><span class="sxs-lookup"><span data-stu-id="f1e3f-128">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span></span>
     - <span data-ttu-id="f1e3f-129">압축 시 프로젝트 종속성 [#936](https://nuget.codeplex.com/workitem/936) 처리</span><span class="sxs-lookup"><span data-stu-id="f1e3f-129">[#936](https://nuget.codeplex.com/workitem/936) - Handle project dependencies when packing</span></span>
11. <span data-ttu-id="f1e3f-130">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span><span class="sxs-lookup"><span data-stu-id="f1e3f-130">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span></span>
     - <span data-ttu-id="f1e3f-131">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) -nuget에 패키지 원본 자격 증명을 저장할 때 일반 텍스트 암호를 지원 합니다. cofig 파일</span><span class="sxs-lookup"><span data-stu-id="f1e3f-131">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) - Support Clear Text Password when storing package source credentials in nuget.cofig files</span></span>
12. <span data-ttu-id="f1e3f-132">[James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span><span class="sxs-lookup"><span data-stu-id="f1e3f-132">[James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span></span>
     - <span data-ttu-id="f1e3f-133">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) -패키지 다운로드 도움말 설명</span><span class="sxs-lookup"><span data-stu-id="f1e3f-133">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) - Fix Get-Package help description</span></span>

<span data-ttu-id="f1e3f-134">또한 최종 릴리스 전에 승인 되 고 수정 된 NuGet 2.5 베타/RC를 사용 하 여 버그를 찾기 위해 다음 개인이 감사 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-134">We also appreciate the following individuals for finding bugs with NuGet 2.5 Beta/RC that were approved and fixed before the final release:</span></span>

1. <span data-ttu-id="f1e3f-135">[Tony 벽](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span><span class="sxs-lookup"><span data-stu-id="f1e3f-135">[Tony Wall](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span></span>
    - <span data-ttu-id="f1e3f-136">최신 NuGet 2.4 및 2.5 빌드를 사용 하 여 [#3200](https://nuget.codeplex.com/workitem/3200) -MSTest 손상</span><span class="sxs-lookup"><span data-stu-id="f1e3f-136">[#3200](https://nuget.codeplex.com/workitem/3200) - MSTest broken with lastest NuGet 2.4 and 2.5 builds</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="f1e3f-137">릴리스의 주요 기능</span><span class="sxs-lookup"><span data-stu-id="f1e3f-137">Notable features in the release</span></span>

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a><span data-ttu-id="f1e3f-138">사용자가 이미 존재 하는 콘텐츠 파일을 덮어쓸 수 있도록 허용</span><span class="sxs-lookup"><span data-stu-id="f1e3f-138">Allow users to overwrite content files that already exist</span></span>

<span data-ttu-id="f1e3f-139">모든 시간에서 가장 많이 요청 되는 기능 중 하나는 NuGet 패키지에 포함 될 때 이미 디스크에 있는 콘텐츠 파일을 덮어쓰는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-139">One of the most requested features of all time has been the ability to overwrite content files that already exist on disk when included in a NuGet package.</span></span> <span data-ttu-id="f1e3f-140">NuGet 2.5부터 이러한 충돌을 식별 하 고 파일을 덮어쓸지 묻는 메시지가 표시 되는 반면 이전에는 이러한 파일을 항상 건너뛰었습니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-140">Starting with NuGet 2.5, these conflicts are identified and you are prompted to overwrite the files, whereas previously these files were always skipped.</span></span>

![콘텐츠 파일 덮어쓰기](./media/NuGet-2.5/overwrite-file.png)

<span data-ttu-id="f1e3f-142">' nuget.exe 업데이트 ' 및 ' 설치-패키지 '에는 이제 명령줄 시나리오에 대 한 기본값을 설정할 수 있는 새 옵션인 '-FileConflictAction '가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-142">'nuget.exe update' and 'Install-Package' now both have a new option '-FileConflictAction' to set some default for command-line scenarios.</span></span>

<span data-ttu-id="f1e3f-143">패키지의 파일이 대상 프로젝트에 이미 있는 경우 기본 동작을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-143">Set a default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="f1e3f-144">항상 파일을 덮어쓰려면 ' 덮어쓰기 '로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-144">Set to 'Overwrite' to always overwrite files.</span></span> <span data-ttu-id="f1e3f-145">파일을 건너뛰려면 ' 무시 '로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-145">Set to 'Ignore' to skip files.</span></span> <span data-ttu-id="f1e3f-146">지정 하지 않으면 충돌 하는 각 파일에 대 한 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-146">If not specified, it will prompt for each conflicting file.</span></span>

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a><span data-ttu-id="f1e3f-147">MSBuild 대상 및 props 파일 자동 가져오기</span><span class="sxs-lookup"><span data-stu-id="f1e3f-147">Automatic import of MSBuild targets and props files</span></span>

<span data-ttu-id="f1e3f-148">NuGet 패키지의 최상위 수준에서 새 기본 폴더를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-148">A new conventional folder has been created at the top level of the NuGet package.</span></span>  <span data-ttu-id="f1e3f-149">`\lib`, `\content`및 `\tools`에 대 한 피어로 이제 패키지에 `\build` 폴더를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-149">As a peer to `\lib`, `\content`, and `\tools`, you can now include a `\build` folder in your package.</span></span>  <span data-ttu-id="f1e3f-150">이 폴더 아래에 고정 이름을 사용 하 여 `{packageid}.targets` 또는 `{packageid}.props`두 파일을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-150">Under this folder, you can place two files with fixed names, `{packageid}.targets` or `{packageid}.props`.</span></span> <span data-ttu-id="f1e3f-151">이러한 두 파일은 다른 폴더와 마찬가지로 `build` 바로 아래에 있거나 프레임 워크 별 폴더에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-151">These two files can be either directly under `build` or under framework-specific folders just like the other folders.</span></span> <span data-ttu-id="f1e3f-152">가장 일치 하는 프레임 워크 폴더를 선택 하는 규칙은 정확히 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-152">The rule for picking the best-matched framework folder is exactly the same as in those.</span></span>

<span data-ttu-id="f1e3f-153">NuGet은 \build 파일이 포함 된 패키지를 설치 하는 경우 프로젝트 파일에서 `.targets` 및 `.props` 파일을 가리키는 MSBuild `<Import>` 요소를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-153">When NuGet installs a package with \build files, it will add an MSBuild `<Import>` element in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="f1e3f-154">`.props` 파일은 맨 위에 추가 되는 반면 `.targets` 파일은 맨 아래에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-154">The `.props` file is added at the top, whereas the `.targets` file is added to the bottom.</span></span>

### <a name="specify-different-references-per-platform-using-references-element"></a><span data-ttu-id="f1e3f-155">`<References/>` 요소를 사용 하 여 플랫폼별로 다른 참조 지정</span><span class="sxs-lookup"><span data-stu-id="f1e3f-155">Specify different references per platform using `<References/>` element</span></span>

<span data-ttu-id="f1e3f-156">2\.5 이전에 `.nuspec` 파일에서는 사용자가 모든 프레임 워크에 대해 추가할 참조 파일만 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-156">Before 2.5, in `.nuspec` file, user can only specify the reference files, to be added for all framework.</span></span> <span data-ttu-id="f1e3f-157">이제 2.5의이 새로운 기능을 사용 하 여 지원 되는 각 플랫폼에 대 한 `<reference/>` 요소를 작성할 수 있습니다. 예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-157">Now with this new feature in 2.5, user can author the `<reference/>` element for each of the supported platform, for example:</span></span>

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

<span data-ttu-id="f1e3f-158">NuGet이 `.nuspec` 파일을 기반으로 하는 프로젝트에 참조를 추가 하는 흐름은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-158">Here is the flow for how NuGet adds references to projects based on the `.nuspec` file:</span></span>

1. <span data-ttu-id="f1e3f-159">대상 프레임 워크에 적합 한 `lib` 폴더를 찾고 해당 폴더에서 어셈블리 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-159">Find the `lib` folder that is appropriate for the target framework and get the list of assemblies from that folder</span></span>
1. <span data-ttu-id="f1e3f-160">대상 프레임 워크에 적합 한 참조 그룹을 별도로 찾고 해당 그룹에서 어셈블리 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-160">Separately find the references group that is appropriate for the target framework and get the list of assemblies from that group.</span></span> <span data-ttu-id="f1e3f-161">지정 된 대상 프레임 워크가 없는 참조 그룹은 대체 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-161">Reference group without target framework specified is the fallback group.</span></span>
1. <span data-ttu-id="f1e3f-162">두 목록의 교집합을 찾아 추가할 참조로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-162">Find the intersection of the two lists, and use that as the references to add</span></span>

<span data-ttu-id="f1e3f-163">이 새로운 기능을 사용 하면 패키지 작성자가 여러 `lib` 폴더에 중복 어셈블리를 전달 해야 하는 경우 참조 기능을 사용 하 여 어셈블리의 하위 집합을 다른 프레임 워크에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-163">This new feature will allow package authors to use the References feature to apply subsets of assemblies to different frameworks when they would otherwise need to carry duplicate assemblies in multiple `lib` folders.</span></span>

<span data-ttu-id="f1e3f-164">참고: 현재 nuget.exe pack을 사용 하 여이 기능을 사용 해야 합니다. NuGet 패키지 탐색기는 아직 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-164">Note: you must presently use nuget.exe pack to use this feature; NuGet Package Explorer does not yet support it.</span></span>

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a><span data-ttu-id="f1e3f-165">모든 패키지를 한 번에 업데이트할 수 있도록 모든 단추를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-165">Update All button to allow updating all packages at once</span></span>

<span data-ttu-id="f1e3f-166">모든 패키지를 업데이트 하는 "업데이트 패키지" PowerShell cmdlet에 대해 알고 있어야 합니다. 이제 UI를 통해이 작업을 수행 하는 쉬운 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-166">Many of you know about the "Update-Package" PowerShell cmdlet to update all of your packages; now there's an easy way to do this through the UI as well.</span></span>

<span data-ttu-id="f1e3f-167">이 기능을 사용해 보려면 다음을 수행 하십시오.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-167">To try this feature out:</span></span>

1. <span data-ttu-id="f1e3f-168">새 ASP.NET MVC 애플리케이션 만들기</span><span class="sxs-lookup"><span data-stu-id="f1e3f-168">Create a new ASP.NET MVC application</span></span>
1. <span data-ttu-id="f1e3f-169">' NuGet 패키지 관리 ' 대화 상자를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-169">Launch the 'Manage NuGet Packages' dialog</span></span>
1. <span data-ttu-id="f1e3f-170">' 업데이트 '를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-170">Select 'Updates'</span></span>
1. <span data-ttu-id="f1e3f-171">' 모두 업데이트 ' 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-171">Click the 'Update All' button</span></span>

![대화 상자의 모두 업데이트 단추](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a><span data-ttu-id="f1e3f-173">Nuget.exe Pack에 대 한 향상 된 프로젝트 참조 지원</span><span class="sxs-lookup"><span data-stu-id="f1e3f-173">Improved project reference support for nuget.exe Pack</span></span>

<span data-ttu-id="f1e3f-174">이제 nuget.exe pack 명령은 다음 규칙을 사용 하 여 참조 된 프로젝트를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-174">Now nuget.exe pack command processes referenced projects with the following rules:</span></span>

1. <span data-ttu-id="f1e3f-175">참조 된 프로젝트에 해당 하는 `.nuspec` 파일이 있는 경우 (예: `proj1.csproj`와 동일한 폴더에 `proj1.nuspec` 라는 파일이 있는 경우)이 프로젝트는 `.nuspec` 파일에서 읽은 id와 버전을 사용 하 여 패키지에 대 한 종속성으로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-175">If the referenced project has corresponding `.nuspec` file, e.g. there is a file called `proj1.nuspec` in the same folder as `proj1.csproj`, then this project is added as a dependency to the package, using the id and version read from the `.nuspec` file.</span></span>
1. <span data-ttu-id="f1e3f-176">그렇지 않으면 참조 된 프로젝트의 파일이 패키지에 번들로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-176">Otherwise, the files of the referenced project are bundled into the package.</span></span> <span data-ttu-id="f1e3f-177">그런 다음이 프로젝트에서 참조 하는 프로젝트가 재귀적으로 sames 규칙을 사용 하 여 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-177">Then projects referenced by this project will be processed using the sames rules recursively.</span></span>
1. <span data-ttu-id="f1e3f-178">모든 DLL, `.pdb`및 `.exe` 파일이 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-178">All DLL, `.pdb`, and `.exe` files are added.</span></span>
1. <span data-ttu-id="f1e3f-179">다른 모든 콘텐츠 파일이 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-179">All other content files are added.</span></span>
1. <span data-ttu-id="f1e3f-180">모든 종속성이 병합 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-180">All dependencies are merged.</span></span>

<span data-ttu-id="f1e3f-181">이를 통해 `.nuspec` 파일이 있는 경우 참조 된 프로젝트를 종속성으로 처리할 수 있습니다. 그렇지 않으면 패키지의 일부가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-181">This allows a referenced project to be treated as a dependency if there is a `.nuspec` file, otherwise, it becomes part of the package.</span></span>

<span data-ttu-id="f1e3f-182">자세한 내용은 다음을 참조 하세요. [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span><span class="sxs-lookup"><span data-stu-id="f1e3f-182">More details here: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span></span>

### <a name="add-a-minimum-nuget-version-property-to-packages"></a><span data-ttu-id="f1e3f-183">패키지에 ' 최소 NuGet 버전 ' 속성 추가</span><span class="sxs-lookup"><span data-stu-id="f1e3f-183">Add a 'Minimum NuGet Version' property to packages</span></span>

<span data-ttu-id="f1e3f-184">이제 ' minClientVersion ' 라는 새 메타 데이터 특성은 패키지를 사용 하는 데 필요한 최소 NuGet 클라이언트 버전을 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-184">A new metadata attribute called 'minClientVersion' can now indicate the minimum NuGet client version required to consume a package.</span></span>

<span data-ttu-id="f1e3f-185">이 기능을 사용 하면 패키지 작성자가 특정 버전의 NuGet 이후에만 패키지를 사용할 수 있도록 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-185">This feature helps package author to specify that a package will work only after a particular version of NuGet.</span></span> <span data-ttu-id="f1e3f-186">새 `.nuspec` 기능이 NuGet 2.5 후에 추가 되 면 패키지는 최소 NuGet 버전을 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-186">As new `.nuspec` features are added after NuGet 2.5, packages will be able to claim a minimum NuGet version.</span></span>

```xml
<metadata minClientVersion="2.6">
```

<span data-ttu-id="f1e3f-187">사용자에 게 NuGet 2.5이 설치 되어 있고 패키지가 2.6을 요구 하는 것으로 식별 되 면 패키지를 설치할 수 없다는 시각적 표시가 사용자에 게 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-187">If the user has NuGet 2.5 installed and a package is identified as requiring 2.6, visual cues will be given to the user indicating the package will not be installable.</span></span> <span data-ttu-id="f1e3f-188">그런 다음 사용자는 NuGet 버전을 업데이트 하도록 안내 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-188">The user will then be guided to update their version of NuGet.</span></span>

<span data-ttu-id="f1e3f-189">이렇게 하면 패키지를 설치 하기 시작 하지만 인식할 수 없는 스키마 버전이 식별 되었음을 나타내는 오류가 발생 하는 기존 환경을 개선 하 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-189">This will improve upon the existing experience where packages begin to install but then fail indicating an unrecognized schema version was identified.</span></span>

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a><span data-ttu-id="f1e3f-190">패키지를 설치 하는 동안 종속성이 더 이상 불필요 하 게 업데이트 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-190">Dependencies are no longer unnecessarily updated during package installation</span></span>

<span data-ttu-id="f1e3f-191">NuGet 2.5 이전에 프로젝트에 이미 설치 된 패키지에 종속 된 패키지를 설치 하는 경우 기존 버전에서 종속성이 충족 되더라도 종속성이 새 설치의 일부로 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-191">Before NuGet 2.5, when a package was installed that depended on a package already installed in the project, the dependency would be updated as part of the new installation, even if the existing version satisfied the dependency.</span></span>

<span data-ttu-id="f1e3f-192">NuGet 2.5부터 종속성 버전이 이미 충족 된 경우 다른 패키지를 설치 하는 동안 종속성이 업데이트 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-192">Starting with NuGet 2.5, if a dependency version is already satisfied, the dependency will not be updated during other package installations.</span></span>

<span data-ttu-id="f1e3f-193">**시나리오는 다음과 같습니다.**</span><span class="sxs-lookup"><span data-stu-id="f1e3f-193">**The scenario:**</span></span>

1. <span data-ttu-id="f1e3f-194">원본 리포지토리에는 버전 1.0.0 및 1.0.2가 포함 된 B 패키지가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-194">The source repository contains package B with version 1.0.0 and 1.0.2.</span></span> <span data-ttu-id="f1e3f-195">B에 대 한 종속성이 있는 패키지 A도 포함 합니다 (> = 1.0.0).</span><span class="sxs-lookup"><span data-stu-id="f1e3f-195">It also contains package A which has a dependency on B (>= 1.0.0).</span></span>
1. <span data-ttu-id="f1e3f-196">현재 프로젝트에 이미 package B 버전 1.0.0이 설치 되어 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-196">Assume that the current project already has package B version 1.0.0 installed.</span></span> <span data-ttu-id="f1e3f-197">이제 패키지 A를 설치 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-197">Now you want to install package A.</span></span>

<span data-ttu-id="f1e3f-198">**NuGet 2.2 이전 버전:**</span><span class="sxs-lookup"><span data-stu-id="f1e3f-198">**In NuGet 2.2 and older:**</span></span>

* <span data-ttu-id="f1e3f-199">Package A를 설치 하면 기존 버전 1.0.0이 이미 > = 1.0.0 인 종속성 버전 제약 조건을 충족 하더라도 NuGet은 B를 1.0.2로 자동 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-199">When installing package A, NuGet will auto-update B to 1.0.2, even though the existing version 1.0.0 already satisfies the dependency version constraint, which is >= 1.0.0.</span></span>

<span data-ttu-id="f1e3f-200">**NuGet 2.5 이상:**</span><span class="sxs-lookup"><span data-stu-id="f1e3f-200">**In NuGet 2.5 and newer:**</span></span>

* <span data-ttu-id="f1e3f-201">NuGet은 기존 버전 1.0.0이 종속성 버전 제약 조건을 충족 하는 것을 감지 하므로 더 이상 B를 업데이트 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-201">NuGet will no longer update B, because it detects that the existing version 1.0.0 satisfies the dependency version constraint.</span></span>

<span data-ttu-id="f1e3f-202">이러한 변경에 대 한 자세한 배경 정보는 관련 [토론 스레드](http://nuget.codeplex.com/discussions/436712)뿐만 아니라 자세한 [작업 항목](http://nuget.codeplex.com/workitem/1681) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-202">For more background on this change, read the detailed [work item](http://nuget.codeplex.com/workitem/1681) as well as the related [discussion thread](http://nuget.codeplex.com/discussions/436712).</span></span>

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a><span data-ttu-id="f1e3f-203">nuget.exe는 자세한 자세한 정보 표시를 포함 하는 http 요청을 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-203">nuget.exe outputs http requests with detailed verbosity</span></span>

<span data-ttu-id="f1e3f-204">Nuget.exe 문제를 해결 하거나 작업 중에 수행 되는 HTTP 요청에 대 한 정보를 확인 하는 경우 '-자세한 정보 ' 스위치는 이제 모든 HTTP 요청을 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-204">If you are troubleshooting nuget.exe or just curious what HTTP requests are made during operations, the '-verbosity detailed' switch will now output all HTTP requests made.</span></span>

![Nuget.exe의 HTTP 출력](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a><span data-ttu-id="f1e3f-206">이제 nuget.exe push에서 UNC 및 폴더 소스를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-206">nuget.exe push now supports UNC and folder sources</span></span>

<span data-ttu-id="f1e3f-207">NuGet 2.5 이전에는 UNC 경로 또는 로컬 폴더를 기반으로 하는 패키지 원본에 대해 ' nuget.exe push '를 실행 하려고 하면 푸시가 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-207">Before NuGet 2.5, if you attempted to run 'nuget.exe push' to a package source based on a UNC path or local folder, the push would fail.</span></span> <span data-ttu-id="f1e3f-208">최근에 추가 된 계층적 구성 기능을 사용 하는 경우에는 nuget.exe에서 UNC/폴더 원본 또는 HTTP 기반 NuGet 갤러리를 대상으로 해야 하는 것이 일반적 이었습니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-208">With the recently added hierarchical configuration feature, it had become common for nuget.exe to need to target either a UNC/folder source, or an HTTP-based NuGet Gallery.</span></span>

<span data-ttu-id="f1e3f-209">NuGet 2.5부터 nuget.exe에서 UNC/폴더 원본을 식별 하는 경우 원본으로 파일 복사를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-209">Starting with NuGet 2.5, if nuget.exe identifies a UNC/folder source, it will perform the file copy to the source.</span></span>

<span data-ttu-id="f1e3f-210">이제 다음 명령이 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-210">The following command will now work:</span></span>

```cli
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a><span data-ttu-id="f1e3f-211">nuget.exe는 명시적으로 지정 된 구성 파일을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-211">nuget.exe supports explicitly-specified Config files</span></span>

<span data-ttu-id="f1e3f-212">구성에 액세스 하는 nuget.exe 명령 (' spec ' 및 ' pack ' 제외)은 이제 새로운 '-000' 옵션을 지원 합니다 .이 옵션을 사용 하면 특정 구성 파일 을%Appdata%\nuget\nuget.config의 기본 구성 파일 대신 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-212">nuget.exe commands that access configuration (all except 'spec' and 'pack') now support a new '-ConfigFile' option, which forces a specific config file to be used in place of the default config file at %AppData%\nuget\Nuget.Config.</span></span>

<span data-ttu-id="f1e3f-213">예:</span><span class="sxs-lookup"><span data-stu-id="f1e3f-213">Example:</span></span>

```cli
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a><span data-ttu-id="f1e3f-214">네이티브 프로젝트에 대 한 지원</span><span class="sxs-lookup"><span data-stu-id="f1e3f-214">Support for Native projects</span></span>

<span data-ttu-id="f1e3f-215">NuGet 2.5을 사용 하면 이제 Visual Studio의 네이티브 프로젝트에서 NuGet 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-215">With NuGet 2.5, the NuGet tooling is now available for Native projects in Visual Studio.</span></span> <span data-ttu-id="f1e3f-216">대부분의 네이티브 패키지는 [coapp 프로젝트](http://coapp.org)에서 만든 도구를 사용 하 여 위의 MSBuild 가져오기 기능을 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-216">We expect most native packages will utilize the MSBuild imports feature above, using a tool created by the [CoApp project](http://coapp.org).</span></span> <span data-ttu-id="f1e3f-217">자세한 내용은 coapp.org 웹 사이트의 [도구에 대 한 세부](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) 정보를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-217">For more information, read [the details about the tool](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) on the coapp.org website.</span></span>

<span data-ttu-id="f1e3f-218">패키지를 네이티브 프로젝트에 설치할 때 패키지에 대해 \build, \build 및 \tools 파일을 포함 하는 패키지에 대해 대상 프레임 워크 이름 "native"가 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-218">The target framework name of "native" is introduced for packages to include files in \build, \content, and \tools when the package is installed into a native project.</span></span>  <span data-ttu-id="f1e3f-219">\`lib의 폴더는 네이티브 프로젝트에 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f1e3f-219">The \`lib\` folder is not used for native projects.</span></span>
