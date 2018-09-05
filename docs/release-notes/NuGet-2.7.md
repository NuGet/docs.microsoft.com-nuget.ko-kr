---
title: NuGet 2.7 릴리스 정보
description: 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr 포함 하 여 NuGet 2.7 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 97d3e5f0238fd6947a54e5eb3229b89b6746f18c
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550967"
---
# <a name="nuget-27-release-notes"></a>NuGet 2.7 릴리스 정보

[WebMatrix 릴리스 정보에 대 한 NuGet 2.6.1](../release-notes/nuget-2.6.1-for-webmatrix.md) | [NuGet 2.7.1 릴리스 정보](../release-notes/nuget-2.7.1.md)

NuGet 2.7은 2013 년 8 월 22 일에 출시 되었습니다.

## <a name="acknowledgements"></a>감사의 글

NuGet 2.7에 대 한 중요 한 기여에 대 한 다음 외부 참가자를 감사 하려고 합니다.

1. [Mike Roth](http://www.codeplex.com/site/users/view/mxrss) ([@mxrss](https://twitter.com/mxrss))
    - 패키지를 나열 하는 자세한 정도 자세히 설명 되어 라이선스 url을 표시 합니다.
2. [Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#1956](http://nuget.codeplex.com/workitem/1956) -developmentDependency 특성을 추가 `packages.config` 만 런타임 패키지를 포함 하도록 pack 명령 사용
3. [Rafael Nicoletti](http://www.codeplex.com/site/users/view/tkrafael) ([@tkrafael](https://twitter.com/tkrafael))
    - Nuget.exe pack 명령에서 중복 속성 키를 방지 합니다.
4. [Ben Phegan](http://www.codeplex.com/site/users/view/benphegan) ([@BenPhegan](https://twitter.com/benphegan))
    - [#2610](http://nuget.codeplex.com/workitem/2610) -200 컴퓨터 캐시 크기를 늘립니다.
5. [Slava Trenogin](http://www.codeplex.com/site/users/view/derigel) ([@derigel](https://twitter.com/derigel))
    - [#3217](http://nuget.codeplex.com/workitem/3217) -잘못 된 탭에서 업데이트를 표시 하는 NuGet 수정 대화 상자
    - 수정 Project.TargetFramework 프로젝트 관리자에서 null 일 수 있습니다.
    - [#3248](http://nuget.codeplex.com/workitem/3248) -해결 SharedPackageRepository FindPackage/FindPackagesById 존재 하지 않는 packageId에서 실패
6. [Kevin Boyle](http://www.codeplex.com/site/users/view/KevinBoyleRG) ([@kevfromireland](https://twitter.com/kevfromireland))
    - [#3234](http://nuget.codeplex.com/workitem/3234) -이주 단계 프로젝트에 대 한 지원을 사용 하도록 설정
7. [Corin Blaikie](http://www.codeplex.com/site/users/view/corinblaikie) ([@corinblaikie](https://twitter.com/corinblaikie))
    - [#3252](http://nuget.codeplex.com/workitem/3252) -파일이 존재 하지 않으면 하는 경우 수정 밀어넣기 명령이 실패 종료 코드 0.
8. [Martin Veselý](http://www.codeplex.com/site/users/view/veselkamartin)
    - [#3226](http://nuget.codeplex.com/workitem/3226) -프로젝트를 데이터베이스 프로젝트를 참조 하는 경우 추가 BindingRedirect 명령 사용 하 여 버그를 수정 합니다.
9. [Miroslav Bajtos](http://www.codeplex.com/site/users/view/miroslavbajtos) ([@bajtos](https://twitter.com/bajtos))
    - [#2891](http://nuget.codeplex.com/workitem/2891) -nuget.pack '제외' 특성에 와일드 카드를 올바르게 구문 분석 중 버그를 수정 합니다.
10. [Justin Dearing](http://www.codeplex.com/site/users/view/zippy1981) ([@zippy1981](https://twitter.com/zippy1981))
     - [#3307](http://nuget.codeplex.com/workitem/3307) -버그 수정 `NuGet.targets` 패키지를 복원 하는 경우 nuget.exe에 $를 전달 하지 않습니다.
11. [Brian Federici](http://www.codeplex.com/site/users/view/benerdin)
     - [#3294](http://nuget.codeplex.com/workitem/3294) -nuget.exe 패키지 명령 이름은 같지만 결국 "항목이 이미 있습니다." 예외를 발생 시키는 다른 대/소문자를 사용 하 여 파일을 추가 하 게 하는 버그를 수정 합니다.
12. [Daniel Cazzulino](http://www.codeplex.com/site/users/view/dcazzulino) ([@kzu](https://twitter.com/kzu))
     - [#2990](http://nuget.codeplex.com/workitem/2990) -버전 추가 속성을 NetPortableProfile 클래스입니다.
13. [David Simner](https://www.codeplex.com/site/users/view/DavidSimner)
     - [#3460](https://nuget.codeplex.com/workitem/3460) -NullReferenceException 버그를 해결할 requireApiKey 사실 이지만 헤더 = X-NUGET-APIKEY 없는
14. [Michael Friis](https://www.codeplex.com/site/users/view/friism) ([@friism](https://twitter.com/friism))
     - [#3278](https://nuget.codeplex.com/workitem/3278) -MonoDevelop에서 올바르게 작동할 수 있도록 수정 NuGet.Build 대상 파일을
15. [Pranav Krishnamoorthy](https://www.codeplex.com/site/users/view/pranavkm) ([@pranav_km](https://twitter.com/pranav_km))
     - 병렬 처리를 늘려 복원 명령은 성능 향상

## <a name="notable-features-in-the-release"></a>릴리스에서 주목할 만한 기능

### <a name="package-restore-by-default-with-implicit-consent"></a>(암시적으로 승인)에 대해 기본적으로 패키지 복원

NuGet 2.7 패키지를 복원 하는 새로운 방식이 소개 하 고 또한 주요 장애물을 극복: 패키지 복원 동의 이제 기본적으로 켜져! 새로운 방식을 암시적 동의 조합 패키지 복원 시나리오를 간소화 현저 하 게 됩니다.

#### <a name="implicit-consent"></a>암시적으로 승인

NuGet 버전 2.0, 2.1, 2.2, 2.5 및 2.6을 사용 하 여 명시적으로 NuGet 시 누락 된 패키지를 다운로드 하도록 허용 하는 데 필요한 사용자 빌드합니다. 이 동의 하지 경우 명시적으로 부여 되어, 패키지 복원 활성화 있던 솔루션은 사용자가 승인 될 때까지 빌드를 실패 합니다.

NuGet 2.7부터, 패키지 복원 동의 기본적으로 설정 되어 사용자가 명시적으로 허용 하는 동안 *옵트아웃* 원한다 면 Visual Studio에서 NuGet의 설정에서 확인란을 사용 하 여 패키지 복원 합니다. 암시적으로 승인에 대 한이 변경에 다음 환경에서 NuGet을 적용 합니다.

* Visual Studio 2013 Preview
* Visual Studio 2012
* Visual Studio 2010
* nuget.exe 명령줄 유틸리티

#### <a name="automatic-package-restore-in-visual-studio"></a>Visual Studio에서 자동 패키지 복원

NuGet 2.7 이상에서는 NuGet 자동으로 다운로드 누락 된 패키지 Visual Studio에서 빌드하는 동안 패키지 복원 되지 않은 솔루션에 대 한 명시적으로 설정 된 경우에 합니다. 이 자동 패키지 복원 하지만 MSBuild가 호출 되기 전에 프로젝트 또는 솔루션을 빌드할 때 Visual Studio에서 수행 합니다. 몇 가지 중요 한 이점 결과가 산출 됩니다.:

1. "NuGet 패키지 복원 사용" 제스처를 사용 하 여 솔루션을 더 이상 필요
1. 프로젝트를 수정할 필요가 없습니다 및 NuGet 패키지 복원 활성화 되어 있는지 확인 하려면 프로젝트에 변경 되지 않습니다.
1. 속성/대상이 파일에 대 한 MSBuild 가져오기를 포함 하는 것을 포함 하는 모든 NuGet 패키지를 복원할 *하기 전에* MSBuild가 호출 되도록 해당 속성/대상이 빌드하는 동안 적절 하 게 인식

Visual Studio에서 자동 패키지 복원 사용 하기 위해 (in) 작업 하나를 수행 해야 합니다.

1. 체크 인 되지에 `packages` 폴더

생략 하는 방법은 여러 가지 프로그램 `packages` 소스 제어에서 폴더입니다. 자세한 내용은 참조는 [패키지 및 소스 제어](../consume-packages/packages-and-source-control.md) 항목입니다.

모든 사용자가 암시적으로 하는 동안 자동 패키지 복원 동의 옵트인 옵트아웃할 수 있습니다 쉽게 Visual Studio에서 패키지 관리자 설정을 통해.

![패키지 관리자 설정](./media/NuGet-2.7/package-manager-settings.png)

#### <a name="simplified-package-restore-from-the-command-line"></a>명령줄에서 간단한 패키지 복원

NuGet 2.7 nuget.exe에 대 한 새 기능이 도입 되었습니다. `nuget.exe restore`

이 새로운 복원 명령이 사용 하면 쉽게 솔루션 파일 또는 폴더를 인수로 허용 하 여 단일 명령 사용 하 여 솔루션에 대 한 모든 패키지를 복원할 수 있습니다. 또한 현재 폴더에서 단일 솔루션만 있으면 해당 인수 포함 됩니다. 즉, 단일 솔루션 파일 (MySolution.sln)를 포함 하는 폴더에서 모든 다음 작동 합니다.

1. nuget.exe restore MySolution.sln
1. nuget.exe 복원 합니다.
1. nuget.exe restore

Restore 명령은 솔루션 파일을 열고 솔루션 내에서 모든 프로젝트를 찾습니다. 여기에서 찾을 수는 `packages.config` 프로젝트 및 패키지의 모든 발견 된 복원의 각 파일에 있습니다. 에 있는 솔루션 수준 패키지를 복원 하기는 `.nuget\packages.config` 파일입니다. 새 Restore 명령에 대 한 자세한 정보를 찾을 수 있습니다 합니다 [명령줄 참조](../tools/cli-ref-restore.md)합니다.

#### <a name="the-new-package-restore-workflow"></a>새 패키지 복원 워크플로

새 워크플로 소개 하는 대로 패키지를 복원 하려면 이러한 변경에 대 한 기대 됩니다. 소스 제어에서 패키지를 생략 하려면 단순히 커밋하지 않을 `packages` 폴더입니다. Visual Studio 사용자를 열고 솔루션을 빌드에 자동으로 복원 된 패키지 표시 됩니다. 명령줄 빌드에 대 한 호출 `nuget.exe restore` 를 호출 하기 전에 `msbuild`입니다. 솔루션에 "NuGet 패키지 복원 사용" 제스처를 사용 해야 하는 더 이상 하 고 더 이상 빌드를 변경 하려면 프로젝트를 수정 해야 합니다. 이 또한 MSBuild 가져오기를 가져오기에 대 한 NuGet의 최신 기능을 통해 추가 위해 특별히 포함 된 패키지에 대 한 훨씬 개선을 생성 [자동으로 가져오기 속성/대상이 파일](../release-notes/nuget-2.5.md#automatic-import-of-msbuild-targets-and-props-files) \build 폴더에서.

직접 수행한 작업을 하는 것 외에도이 새로운 방식은 마무리 하기 위해 몇 가지 중요 한 파트너와도 협력 합니다. 이러한 템플릿 중 하나에 대 한 구체적인 타임 라인이 아직 있는 없지만 각 파트너는 새로운 방법에 대 한 것으로 기대 합니다.

* Team Foundation Service-이러한 통합 하는 작업에 대 한 호출 `nuget.exe restore` 기본 시나리오를 작성 합니다.
* Windows Azure 웹 사이트-작업할 수 있고 Azure에 프로젝트를 밀어 `nuget.exe restore` 웹 사이트를 빌드하기 전에 호출 됩니다.
* TeamCity-TeamCity에 대 한 해당 NuGet 설치 관리자 플러그 인을 업데이트 되는 8.x
* 있고 AppHarbor 리포지토리에 푸시할 수 있도록 작업할 AppHarbor- `nuget.exe restore` 솔루션 빌드를 수행 하기 전에 호출 됩니다.

각 위의 파트너를 사용 하 여 자신의 복사본 nuget.exe 사용할 때 및 솔루션에서 nuget.exe를 수행 해야 합니다.

#### <a name="known-issues"></a>알려진 문제

초기 2.7 릴리스에서 nuget.exe restore 사용 하 여 두 가지 알려진된 문제가 있었습니다 있지만에 대 한 업데이트를 사용 하 여 2013 년 9 월 6/에서 해결 된 것을 [NuGet.CommandLine 패키지](http://www.nuget.org/packages/NuGet.CommandLine/)합니다.  이 업데이트에서 제공 됩니다는 [NuGet 2.7 다운로드 페이지](https://nuget.codeplex.com/releases/view/107605) CodePlex에 있습니다.  실행 `nuget.exe update -self` 를 최신 릴리스로 업데이트 됩니다.

고정 했습니다.

1. [SLN 파일을 사용 하는 경우 Mono에서 새 패키지 복원이 작동 하지 않습니다.](https://nuget.codeplex.com/workitem/3596)
1. [Wix 프로젝트를 사용 하 여 새 패키지 복원이 작동 하지 않습니다.](https://nuget.codeplex.com/workitem/3598)

이기도 새 패키지 복원 워크플로 사용 하 여 알려진된 문제 가능해 집니다 [자동 패키지 복원 솔루션 폴더 아래의 프로젝트에 대 한 작동 하지 않습니다](https://nuget.codeplex.com/workitem/3625)합니다. 이 문제는 NuGet 2.7.1에서에서 수정 되었습니다.

### <a name="project-retargeting-and-upgrade-build-errorswarnings"></a>프로젝트 대상 다시 지정 및 업그레이드에 대 한 빌드 오류/경고

여러 번을 대상 다시 지정 하거나 프로젝트를 업그레이드 한 후 찾아야 일부 NuGet 패키지의 작동이 되지 않습니다. 아쉽게도이 표시가 없습니다 하 고 지침이 없습니다에 문제를 해결 하는 방법입니다. NuGet 2.7의 경우 이제 사용 하 여 일부 Visual Studio 이벤트 대상이 변경 했거나, 설치 된 NuGet 패키지에 영향을 주는 방식으로 프로젝트를 업그레이드 하는 경우를 인식 하도록 합니다.

패키지의 영향을 받았습니다 대상 변경 또는 업그레이드를 검색 하는 경우 즉시 빌드 오류를 알려 주는 도출 됩니다. 즉시 빌드 오류 외에 유지를 `requireReinstallation="true"` 플래그에 `packages.config` 파일 Visual Studio에서 빌드를 대상 변경의 영향 및 각 후속 된 모든 패키지에 대 한 경고가 표시 됩니다 빌드 패키지에 대 한 합니다.

NuGet 영향을 받는 패키지를 다시 설치 하려면 자동 작업을 수행할 수 없습니다,이 표시 바랍니다 및 경고 도움말 안내 합니다. 하지만 패키지 다시 설치 해야 하는 경우 검색할 수 있습니다. 또한 노력 [패키지 다시 설치 지침 설명서](../consume-packages/reinstalling-and-updating-packages.md) 이러한 오류 메시지를 안내 합니다.

### <a name="nuget-configuration-defaults"></a>NuGet 구성 기본값

대부분의 회사 NuGet 내부적으로 사용 하면서 어려움 nuget.org 대신 내부 패키지 소스를 사용 하도록 개발자 안내 했습니다. NuGet 2.7 시스템 수준의 기본값은에 지정할 수 있는 구성 기본값 기능을 제공 합니다.

1. 사용 가능한 패키지 소스
1. 등록 되었지만 사용할 수 없는 패키지 소스
1. Nuget.exe 기본 푸시 소스

에 있는 파일 내에서 이제 구성할 수 있습니다 이러한 각 `%ProgramData%\NuGet\NuGetDefaults.Config`합니다. 패키지 소스를 지정 하는이 구성 파일 경우 기본 nuget.org 패키지 원본이 자동으로 등록 되지 것입니다 및에서 `NuGetDefaults.Config` 대신 등록 됩니다.

회사 배포에이 기능을 사용할 필요 없이 기대 `NuGetDefaults.Config` 그룹 정책을 사용 하 여 파일입니다.

*이 기능은 개발자의 NuGet 설정에서 제거할 패키지 소스를 일으키지 않는 참고 합니다. 즉, 개발자가 이미 NuGet을 사용 하 고 nuget.org 패키지 원본이 따라서 경우 등록 제거 되지 않습니다을 만든 후를 `NuGetDefaults.Config` 파일입니다.*

참조 [구성에서 기본적으로 NuGet](../consume-packages/configuring-nuget-behavior.md#nuget-defaults-file) 이 기능에 대 한 자세한 내용은 합니다.

### <a name="renaming-the-default-package-source"></a>기본 패키지 소스 이름 바꾸기

NuGet에서 항상 "NuGet 공식 패키지 소스 라는" nuget.org를 가리키는 기본 패키지 소스를 등록 해야 합니다. 해당 이름의 세부 정보 표시 되었으며 것도 지정 하지 않은 실제로 가리킨다면 합니다. 이러한 두 가지 문제를 해결 하기 위해 단순히 "nuget.org" ui에서에이 패키지 소스를 바꾸었습니다 했습니다. 패키지 원본에 대 한 URL "www"를 포함 하도록 변경도 되었습니다. 접두사가 있는 번들 ID인 식별자가 있습니다. NuGet 2.7를 사용한 후에 기존 "NuGet 공식 패키지 소스" 자동 업데이트 됩니다을 이름으로 "nuget.org" 및 "<https://www.nuget.org/api/v2/>" 해당 URL로 합니다.

### <a name="performance-improvements"></a>성능 향상

2.7 적은 메모리를 사용, 작은 디스크 사용량 및 더 빠른 패키지 설치를 생성 하는 일부 성능 향상을 했습니다. 또한 더 효율적인 쿼리 하기 위해 전체 페이로드를 줄일 수 있는 OData 기반 피드 적용 했습니다.

### <a name="new-extensibility-apis"></a>새 확장성 Api

이전 버전의 누락 된 기능 차이 맞게 확장 서비스를 몇 가지 새로운 Api를 추가 했습니다.

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

이 기능은 제공한 [Adam Ralph](https://twitter.com/adamralph) 패키지 작성자가 종속성만 개발에 사용 된 시간 및 패키지 종속성 않아도 선언를 허용 하 고 있습니다. 추가 하 여는 `developmentDependency="true"` 에서 패키지를 특성 `packages.config`, `nuget.exe pack` 종속성으로 패키지를 더 이상 포함 됩니다.

### <a name="removed-support-for-visual-studio-2010-express-for-windows-phone"></a>Windows Phone 대 한 Visual Studio 2010 Express에 대 한 지원 제거

2.7의 새 패키지 복원 모델에서는 주요 NuGet VSPackage와 다른 새 vspackage 구현 됩니다. 기술 문제로 인해이 새 VSPackage 하지에서 제대로 작동 합니다 *Visual Studio 2010 Express에 대 한 Windows Phone* SKU 서로 동일한 코드 기반을 공유 지원 되는 Visual Studio Sku. 따라서 NuGet 2.7부터 우리는 삭제에 대 한 지원을 *Visual Studio 2010 Express에 대 한 Windows Phone* 게시 된 확장 프로그램에서 제공 합니다. 에 대 한 지원 *Visual Studio 2010 Express for Web* Visual Studio 확장 갤러리에 게시 된 기본 확장에 여전히 포함 되어 있습니다.

에서는 확실 하지 않은 얼마나 많은 개발자는 해당 버전의 Visual Studio에서 NuGet을 사용한 여전히 있으므로 특히 해당 사용자에 대 한 별도 Visual Studio 확장을 게시 하 고 CodePlex 대신 Visual Studio 확장 갤러리에 게시 . 계속 하는 경우이 영향을 수 있지만 해당 확장을 유지 하지 않으려고 알려주세요 codeplex는 문제를 제출 하 여 합니다.

참조 (Visual Studio 2010 Express에 대 한 Windows Phone)에 대 한 NuGet 패키지 관리자를 다운로드 합니다 [NuGet 2.7 다운로드](https://nuget.codeplex.com/releases/view/107605) 페이지입니다.

### <a name="bug-fixes"></a>버그 수정

이 릴리스의 NuGet에는 이러한 기능 외에 다른 여러 버그 수정도 포함 됩니다. 릴리스에서 해결 97 총 문제가 있었습니다. 작업의 전체 목록은 항목 고정 NuGet 2.7에서 하세요 보기는 [이 릴리스의 NuGet 문제 추적기](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.7&status=all)합니다.
