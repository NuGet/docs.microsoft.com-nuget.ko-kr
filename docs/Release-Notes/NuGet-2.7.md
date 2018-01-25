---
title: "NuGet 2.7 릴리스 정보 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr를 포함 하 여 NuGet 2.7에 대 한 릴리스 정보입니다."
keywords: "NuGet 2.7 릴리스 정보, 버그 수정, 알려진 문제, 추가 기능을 Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b0e12f7e2cffa6e721dd13c117b7b3727cfcb5d7
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-27-release-notes"></a>NuGet 2.7 릴리스 정보

[2.6.1 WebMatrix 릴리스 정보에 대 한 NuGet](../release-notes/nuget-2.6.1-for-webmatrix.md) | [NuGet 2.7.1 릴리스 정보](../release-notes/nuget-2.7.1.md)

NuGet 2.7는 2013 년 8 월 22 일에 출시 되었습니다.

## <a name="acknowledgements"></a>감사의 글

NuGet 2.7로의 중요 한 기여에 대 한 다음과 같은 외부 참가자를 감사 하 고 싶습니다.

1. [Mike Roth](http://www.codeplex.com/site/users/view/mxrss) ([@mxrss](https://twitter.com/mxrss))
    - 패키지를 나열 하는 자세한 정도 자세히 설명 되어 라이선스 url을 표시 합니다.
1. [Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#1956](http://nuget.codeplex.com/workitem/1956) -developmentDependency 특성을 추가할 `packages.config` 런타임 패키지 포함 하도록 팩 명령에 사용 하 고
1. [Rafael Nicoletti](http://www.codeplex.com/site/users/view/tkrafael) ([@tkrafael](https://twitter.com/tkrafael))
    - Nuget.exe 팩 명령에 중복 속성 키를 하지 마십시오.
1. [Ben Phegan](http://www.codeplex.com/site/users/view/benphegan) ([@BenPhegan](https://twitter.com/benphegan))
    - [#2610](http://nuget.codeplex.com/workitem/2610) -200 컴퓨터 캐시 크기를 늘리세요.
1. [Slava Trenogin](http://www.codeplex.com/site/users/view/derigel) ([@derigel](https://twitter.com/derigel))
    - [#3217](http://nuget.codeplex.com/workitem/3217) -해결 NuGet 대화 업데이트에 잘못 된 탭 표시
    - 수정 프로그램 Project.TargetFramework 프로젝트 관리자에는 null 일 수 있습니다.
    - [#3248](http://nuget.codeplex.com/workitem/3248) -해결 SharedPackageRepository FindPackage/FindPackagesById가 존재 하지 않는 packageId에서 실패
1. [Kevin Boyle](http://www.codeplex.com/site/users/view/KevinBoyleRG) ([@kevfromireland](https://twitter.com/kevfromireland))
    - [#3234](http://nuget.codeplex.com/workitem/3234) -이주 단계 프로젝트에 대 한 지원을 사용 하도록 설정
1. [Corin Blaikie](http://www.codeplex.com/site/users/view/corinblaikie) ([@corinblaikie](https://twitter.com/corinblaikie))
    - [#3252](http://nuget.codeplex.com/workitem/3252) -파일이 존재 하지 않는 경우 수정 푸시 명령이 실패 종료 코드 0입니다.
1. [Martin Veselý](http://www.codeplex.com/site/users/view/veselkamartin)
    - [#3226](http://nuget.codeplex.com/workitem/3226) -프로젝트는 데이터베이스 프로젝트를 참조 하는 경우 추가 BindingRedirect 명령 사용 하 여 버그 수정.
1. [Miroslav Bajtos](http://www.codeplex.com/site/users/view/miroslavbajtos) ([@bajtos](https://twitter.com/bajtos))
    - [#2891](http://nuget.codeplex.com/workitem/2891) -nuget.pack '제외' 특성에 와일드 카드를 잘못 구문 분석의 버그 수정.
1. [Justin Dearing](http://www.codeplex.com/site/users/view/zippy1981) ([@zippy1981](https://twitter.com/zippy1981))
    - [#3307](http://nuget.codeplex.com/workitem/3307) -버그 수정 프로그램 `NuGet.targets` 패키지를 복원 하는 경우 nuget.exe에 $(Platform)를 전달 하지 않습니다.
1. [Brian Federici](http://www.codeplex.com/site/users/view/benerdin)
    - [#3294](http://nuget.codeplex.com/workitem/3294) -nuget.exe 패키지 명령 이름은 같지만 "항목이 이미 있습니다." 예외를 일으키는 결국 다른 대/소문자를 사용 하 여 파일을 추가할 수 있는 버그 수정.
1. [이 Cazzulino](http://www.codeplex.com/site/users/view/dcazzulino) ([@kzu](https://twitter.com/kzu))
    - [#2990](http://nuget.codeplex.com/workitem/2990) -NetPortableProfile 클래스에 추가 버전 속성입니다.
1. [David Simner](https://www.codeplex.com/site/users/view/DavidSimner)
    - [#3460](https://nuget.codeplex.com/workitem/3460) -경우에 NullReferenceException 버그를 수정 requireApiKey = true 인데 헤더 X-NUGET-APIKEY 존재 하지
1. [Michael Friis](https://www.codeplex.com/site/users/view/friism) ([@friism](https://twitter.com/friism))
    - [#3278](https://nuget.codeplex.com/workitem/3278) -MonoDevelop에서 제대로 작동 되도록 수정 NuGet.Build 대상 파일을
1. [Pranav Krishnamoorthy](https://www.codeplex.com/site/users/view/pranavkm) ([@pranav_km](https://twitter.com/pranav_km))
    - 병렬 처리를 늘려 복원 명령 성능을 향상합니다

## <a name="notable-features-in-the-release"></a>릴리스에서 주목할 만한 기능

### <a name="package-restore-by-default-with-implicit-consent"></a>암시적으로 승인) (함께 기본적으로 패키지를 복원

2.7 NuGet 패키지를 복원 하는 새로운 접근 방식을 소개 하 고도 주요 장애물을 극복: 패키지 복원 동의 이제 기본적으로 켜져! 암시적으로 승인 하 고 새로운 접근 방식을 조합해 패키지 복원 시나리오를 간소화 현저 하 게 됩니다.

#### <a name="implicit-consent"></a>암시적으로 승인

NuGet 버전 2.0, 2.1, 2.2, 2.5, 및 2.6에서는 사용자가 명시적으로 하는 동안 누락 된 패키지를 다운로드 하려면 NuGet을 허용 하는 데 필요한 빌드합니다. 이 있으면이 동의 하지 명시적으로 부여 되어, 솔루션 패키지를 복원 활성화 있던 사용자가을 승인 될 때까지 만들려는 실패 합니다.

NuGet 2.7 부터는 패키지 복원 동의 기본적으로 켜져 하므로 사용자를 명시적으로 *옵트아웃* 의 확인란을 사용 하 여 Visual Studio에서 NuGet의 설정에 필요한 경우 패키지를 복원 합니다. 암시적으로 승인에 대 한이 변경 내용은 다음과 같은 환경에서 NuGet을 결정 합니다.

* Visual Studio 2013 Preview
* Visual Studio 2012
* Visual Studio 2010
* nuget.exe Command-Line Utility

#### <a name="automatic-package-restore-in-visual-studio"></a>Visual Studio에서 자동 패키지 복원

NuGet 2.7부터 NuGet은 자동으로 누락 된 패키지를 빌드 시 다운로드 Visual Studio에서 솔루션에 대 한 패키지를 복원 되지 않은 명시적으로 설정 하는 경우에 합니다. 이 자동 패키지를 복원 하지만 MSBuild를 호출 하기 전에 프로젝트 또는 솔루션을 빌드할 때 Visual Studio에서 수행 합니다. 이 통해 몇 가지 중요 한 이점:

1. "NuGet 패키지 복원을 사용" 제스처를 사용 하 여 솔루션을 더 이상 필요
1. 프로젝트를 수정할 필요가 없습니다 및 NuGet 패키지 복원을 사용할 수 있도록 프로젝트에 변경 되지 않습니다.
1. Props/대상 파일에 대 한 MSBuild 가져오기 포함을 포함 하는 모든 NuGet 패키지를 복원할 *전에* MSBuild가 호출 빌드하는 동안 해당 props/대상이 적절 하 게 인식 확인

자동 패키지 복원에서 사용 하려면 Visual Studio (in) 작업 하나를 수행 하기만 하면:

1. 선택 하지 마세요 프로그램 `packages` 폴더

여러 가지 방법으로 생략 하 여 `packages` 소스 제어에서 폴더입니다. 자세한 내용은 참조는 [패키지 및 소스 제어](../consume-packages/packages-and-source-control.md) 항목입니다.

모든 사용자가 암시적으로 자동 패키지 복원 동의 옵트인 옵트아웃할 수 있습니다 쉽게 통해 Visual Studio의 패키지 관리자 설정 합니다.

![패키지 관리자 설정](./media/NuGet-2.7/package-manager-settings.png)

#### <a name="simplified-package-restore-from-the-command-line"></a>명령줄에서 간단한 패키지를 복원

NuGet 2.7 nuget.exe는 새로운 기능이 도입 되었습니다.`nuget.exe restore`

이 새로운 복원 명령에는 솔루션 파일 또는 폴더를 인수로 사용 하 여 하나의 명령으로 솔루션에 대 한 모든 패키지를 쉽게 복원할 수 있습니다. 또한 인수에 지정 된 현재 폴더에 있는 단일 솔루션만 있을 때 포함 됩니다. 즉, 단일 솔루션 파일 (MySolution.sln)를 포함 하는 폴더에서 모든 다음 작동 합니다.

1. nuget.exe restore MySolution.sln
1. nuget.exe 복원 작업입니다.
1. nuget.exe 복원

Restore 명령 솔루션 파일을 엽니다 되며 솔루션 내의 모든 프로젝트를 찾습니다. 여기에서 찾을 수는 `packages.config` 프로젝트 및 패키지의 모든 발견 된 복원의 각 파일에 있습니다. 에 솔루션 수준의 패키지를 복원 하기는 `.nuget\packages.config` 파일입니다. 새 복원 명령에 대 한 자세한 정보를 찾을 수는 [Command-Line Reference](../tools/cli-ref-restore.md)합니다.

#### <a name="the-new-package-restore-workflow"></a>새 패키지 복원 워크플로

새 워크플로 소개 하는 대로 되어 패키지 복원에 변경 내용을이 적용 하는 방법에 대 한 기쁘게 생각 합니다. 소스 제어에서 패키지를 생략할 경우 단순히 커밋하지 않을 `packages` 폴더입니다. Visual Studio 사용자에 게 솔루션을 빌드합니다를 열고 패키지를 자동으로 복원 표시 됩니다. 명령줄 빌드에 대 한 호출 `nuget.exe restore` 호출 하기 전에 `msbuild`합니다. 더 이상 "NuGet 패키지 복원을 사용" 제스처를 사용 하 여 솔루션을를 하며 더 이상을 빌드를 변경 하 여 프로젝트를 수정 해야 합니다. NuGet의 최근 기능을 통해 추가 된 가져오기에 대 한 특히 MSBuild 가져오기, 포함 된 패키지에 대 한 매우 향상 된 경험을 생성이 [자동으로 가져오기 props/대상 파일](../release-notes/nuget-2.5.md#automatic-import-of-msbuild-targets-and-props-files) \build 폴더에서 합니다.

직접 수행한 작업 외에 최선을 다하고를이 새로운 접근 방식은 몇 가지 중요 한 파트너와 함께 합니다. 구체적인 타임 라인 이들에 대해 아직 없지만 각 파트너는 새로운 접근 방식에 대 한 것과 같이 기쁘게 생각 합니다.

* 에 대 한 호출을 통합 하려면 작업 중인 team Foundation Service- `nuget.exe restore` 기본값에 시나리오를 작성 합니다.
* Windows Azure 웹 사이트-작업할 하 고 Azure에 프로젝트를 푸시 하도록 할 수 있도록 `nuget.exe restore` 웹 사이트를 빌드하기 전에 호출 합니다.
* TeamCity-TeamCity에 대 한 자신의 NuGet 설치 관리자 플러그 인을 업데이트 하 이러한 8.x
* 하 고 AppHarbor에 대 한 사용자의 리포지토리 푸시 하도록 할 수 있도록 작업 AppHarbor- `nuget.exe restore` 솔루션 빌드를 수행 하기 전에 호출 됩니다.

각 위의 파트너 nuget.exe의 자체 복사본을 사용할 때와 nuget.exe 솔루션에서 수행 해야 합니다.

#### <a name="known-issues"></a>알려진 문제

Nuget.exe 복원 초기 2.7 릴리스에서 알려진된 문제 두 개가 있지만에 대 한 업데이트 된 2013 년 9 월 6 일에 수정 된는 [NuGet.CommandLine 패키지](http://www.nuget.org/packages/NuGet.CommandLine/)합니다.  이 업데이트에서 제공 됩니다는 [NuGet 2.7 다운로드 페이지](https://nuget.codeplex.com/releases/view/107605) CodePlex에 있습니다.  실행 `nuget.exe update -self` 최신 버전으로 업데이트 됩니다.

고정 된:

1. [SLN 파일을 사용 하는 경우 새 패키지를 복원 모노에서 작동 하지 않습니다.](https://nuget.codeplex.com/workitem/3596)
1. [새 패키지를 복원 Wix 프로젝트와 함께 작동 하지 않습니다.](https://nuget.codeplex.com/workitem/3598)

이기도 새 패키지 복원 워크플로 알려진된 문제가 그에 따라 [자동 패키지 복원 되지 않을 솔루션 폴더 아래의 프로젝트에 대 한](https://nuget.codeplex.com/workitem/3625)합니다. 이 문제는 2.7.1 NuGet에서 수정 되었습니다.

### <a name="project-retargeting-and-upgrade-build-errorswarnings"></a>프로젝트 대상 다시 지정 및 업그레이드에 대 한 빌드 오류/경고

여러 번을 대상 다시 지정 하거나 프로젝트를 업그레이드 한 후 알게 일부 NuGet 패키지가 제대로 작동 되지 않습니다. 안타깝게도,의이 표시 되지 않으며 다음는 지침은 없으며 문제를 해결 하는 방법에입니다. NuGet 2.7와에서는 이제 사용 하 여 일부 Visual Studio 이벤트 대상이 변경 하거나 설치 된 NuGet 패키지에 영향을 주는 방식으로 프로젝트를 업그레이드 한 경우를 인식 합니다.

패키지는 사용자의 영향을 받았습니다 대상 변경 또는 업그레이드를 검색 하는 경우를 알려 주는 즉시 빌드 오류 도출 합니다. 즉시 빌드 오류 외에도에서는 또한 유지는 `requireReinstallation="true"` 에 대 한 플래그가 프로그램 `packages.config` 파일 모든 패키지는 대상에 의해 영향을 하 고 각 후속를 Visual Studio에서 빌드에 대 한 경고가 표시 됩니다 빌드 해당 패키지에 대 한 합니다.

NuGet 영향을 받는 패키지를 다시 설치 하려면 자동 작업을 수행할 수 없습니다, 경험을 이러한 지표 및 경고 도움말 안내 있지만 패키지를 다시 설치 해야 하는 경우 검색할 수 있습니다. 또한 작업 [재설치 지침 문서 패키지](../consume-packages/reinstalling-and-updating-packages.md) 는 이러한 오류 메시지 하 라고 지시 합니다.

### <a name="nuget-configuration-defaults"></a>NuGet 구성 기본값

많은 회사 NuGet 내부적으로 사용 하면서 어려워 nuget.org 대신 내부 패키지 소스를 사용 하도록 하는 개발자에 안내 했습니다. NuGet 2.7 시스템 수준의 기본값에 대해 지정할 수 있는 구성 기본값 기능이 도입 되었습니다.

1. 사용 가능한 패키지 소스
1. 등록 패키지를 사용할 수 없는 소스 되었지만
1. 기본 nuget.exe 푸시 소스

이러한 각 항목을 구성할 수 있습니다에 있는 파일 내에서 `%ProgramData%\NuGet\NuGetDefaults.Config`합니다. 이 구성 파일은 패키지 소스를 지정 하는 경우 다음 기본 nuget.org 패키지 소스를 자동으로 등록 되지 것입니다 및에서 `NuGetDefaults.Config` 대신 등록 됩니다.

배포 하는 회사 작업도 수행 하지 않아도이 기능을 사용 하려면, 동안 `NuGetDefaults.Config` 그룹 정책을 사용 하 여 파일입니다.

*이 기능은 개발자의 NuGet 설정에서 제거할 패키지 소스를 일으키지 않는 유의 합니다. 즉, 하는 경우 개발자가 이미 NuGet을 사용 하 고 때문에 nuget.org 패키지 소스를 등록 하는 제거 되지 않습니다를 만든 후는 `NuGetDefaults.Config` 파일입니다.*

참조 [NuGet 구성 기본값](../consume-packages/configuring-nuget-behavior.md#nuget-defaults-file) 이 기능에 대 한 자세한 내용은 합니다.

### <a name="renaming-the-default-package-source"></a>기본 패키지 소스 이름 바꾸기

NuGet에 항상 "NuGet 공식 패키지 소스 라는" nuget.org를 가리키는 기본 패키지 소스를 등록 했습니다. 해당 이름이 verbose 고 것도 지정 하지 않은 가리키는 실제로 되었습니다. 이러한 두 가지 문제를 해결 하기 위해이 패키지 소스를 단순히 "nuget.org" UI에 이름을 했습니다. 패키지 원본에 대 한 URL은 "www"를 포함 하도록 변경 수 또한 접두사입니다. NuGet 2.7를 사용한 후에 기존 "NuGet 공식 패키지 소스" 이름으로 "nuget.org" 및 "https://www.nuget.org/api/v2/" url을 업데이트 자동으로 됩니다.

### <a name="performance-improvements"></a>성능 향상

2.7 생성 합니다. 더 작은 메모리 사용 공간, 적은 디스크 사용 및 더 빠른 패키지 설치의에서 일부 성능 향상을 만들었습니다. 또한 더 효율적인 쿼리는 전체 페이로드를 줄일 수 있는 OData 기반 피드를 변경 합니다.

### <a name="new-extensibility-apis"></a>새 확장성 Api

이전 릴리스에서 누락 된 기능 격차를 채울 확장성 서비스 몇 가지 새로운 Api를 추가 했습니다.

#### <a name="ivspackageinstallerservices"></a>IVsPackageInstallerServices

    ```cs
    // Checks if a NuGet package with the specified Id and version is installed in the specified project.
    bool IsPackageInstalledEx(Project project, string id, string versionString);

    // Get the list of NuGet packages installed in the specified project.
    IEnumerable<IVsPackageMetadata> GetInstalledPackages(Project project);
    ```

#### <a name="ivspackageinstaller"></a>IVsPackageInstaller

    ```cs
    // Installs one or more packages that exist on disk in a folder defined in the registry.
    void InstallPackagesFromRegistryRepository(string keyName, bool isPreUnzipped, bool skipAssemblyReferences, Project project, IDictionary<string, string> packageVersions);

    // Installs one or more packages that are embedded in a Visual Studio Extension Package.
    void InstallPackagesFromVSExtensionRepository(string extensionId, bool isPreUnzipped, bool skipAssemblyReferences, Project project, IDictionary<string, string> packageVersions);
    ```

### <a name="development-only-dependencies"></a>개발 전용 종속성

이 기능은가 제공 했습니다 [Adam Ralph](https://twitter.com/adamralph) 패키지 작성자 종속성만 개발에 사용 된 시간 및 패키지 종속 파일을 요구 하지 선언할 수 있습니다. 추가 하 여 한 `developmentDependency="true"` 를 패키지에 특성 `packages.config`, `nuget.exe pack` 종속성으로 해당 패키지를 더 이상 포함 됩니다.

### <a name="removed-support-for-visual-studio-2010-express-for-windows-phone"></a>Windows Phone 대 한 Visual Studio 2010 Express에 대 한 지원을 제거

2.7에서 새 패키지 복원 모델 주 NuGet VSPackage와에서 다른 새 VSPackage에서 구현 됩니다. 기술적 문제로 인해이 새 VSPackage 작동 하지 않는 제대로 *Visual Studio 2010 Express에 대 한 Windows Phone* SKU 다른 동일한 코드 베이스을 공유 하는 것 처럼 지원 Visual Studio Sku. 따라서 NuGet 2.7부터에서는 삭제 하 고에 대 한 지원을 *Visual Studio 2010 Express에 대 한 Windows Phone* 게시 된 확장 프로그램에서 제공 합니다. 에 대 한 지원 *웹용 Visual Studio 2010 Express* Visual Studio 확장 갤러리에 게시 된 기본 확장에 여전히 포함 되어 있습니다.

해당 사용자에 대 한 구체적으로 별도 Visual Studio 확장을 게시 하 고 CodePlex (Visual Studio 확장 갤러리 아님)에 게시 했습니다 확실 하지 않은 수의 개발자가 해당 버전/버전의 Visual Studio에서 NuGet을 여전히 사용 되, 이후 . 이 영향을 줍니다 있습니다 하지만 해당 확장명을 유지 하기 위해 계속 하지 않으려고 알려 주시면 codeplex는 문제를 제출 하 여 합니다.

(Visual Studio 2010 Express에 대 한 Windows Phone)에 대 한 NuGet 패키지 관리자를 다운로드 하려면 방문는 [NuGet 2.7 다운로드](https://nuget.codeplex.com/releases/view/107605) 페이지.

### <a name="bug-fixes"></a>버그 수정

이러한 기능 외에도이 버전의 NuGet 다른 많은 버그 수정 포함 되어 있습니다. 97 총 문제는 릴리스에서 해결 했습니다. 작업의 전체 목록은 항목에서에서 수정 된 NuGet 2.7 하십시오 보기는 [이 릴리스에 대 한 NuGet 문제 추적기](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.7&status=all)합니다.
