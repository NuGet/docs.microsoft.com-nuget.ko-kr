---
title: NuGet 2.7 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 Ecrs를 비롯 한 NuGet 2.7에 대 한 릴리스 정보입니다.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 70600e3c563e357663b4a2f24139d2fc25f75fdf
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780392"
---
# <a name="nuget-27-release-notes"></a>NuGet 2.7 릴리스 정보

[WebMatrix 릴리스 정보](../release-notes/nuget-2.6.1-for-webmatrix.md)  |  에 대 한 NuGet 2.6.1 [NuGet 2.7.1 릴리스 정보](../release-notes/nuget-2.7.1.md)

NuGet 2.7은 2013 년 8 월 22 일에 출시 되었습니다.

## <a name="acknowledgements"></a>감사의 말

NuGet 2.7에 대 한 중요 한 기여에 대해 다음과 같은 외부 참가자에 게 감사 하려고 합니다.

1. [Mike Roth](http://www.codeplex.com/site/users/view/mxrss) ( [@mxrss](https://twitter.com/mxrss) )
    - 패키지 나열 및 자세한 정도를 자세히 설명 하는 경우 라이선스 url을 표시 합니다.
2. [Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ( [@adamralph](https://twitter.com/adamralph) )
    - [#1956](http://nuget.codeplex.com/workitem/1956) -developmentDependency 특성을에 추가 하 `packages.config` 고 pack 명령에 사용 하 여 런타임 패키지만 포함 합니다.
3. [Rafael Nicoletti](http://www.codeplex.com/site/users/view/tkrafael) ( [@tkrafael](https://twitter.com/tkrafael) )
    - nuget.exe pack 명령에서 중복 된 속성 키를 사용 하지 마십시오.
4. [이혜준 Phegan](http://www.codeplex.com/site/users/view/benphegan) ( [@BenPhegan](https://twitter.com/benphegan) )
    - [#2610](http://nuget.codeplex.com/workitem/2610) -컴퓨터 캐시 크기를 200로 늘립니다.
5. [Slava Trenogin](http://www.codeplex.com/site/users/view/derigel) ( [@derigel](https://twitter.com/derigel) )
    - [#3217](http://nuget.codeplex.com/workitem/3217) -잘못 된 탭의 업데이트를 표시 하는 NuGet 대화 상자 수정
    - 프로젝트를 수정 합니다. ProjectManager에서 TargetFramework가 null 일 수 있습니다.
    - [#3248](http://nuget.codeplex.com/workitem/3248) -SharedPackageRepository findpackage/FindPackagesById는 존재 하지 않는 packageId에서 실패 합니다.
6. [Kevin Boyle](http://www.codeplex.com/site/users/view/KevinBoyleRG) ( [@kevfromireland](https://twitter.com/kevfromireland) )
    - [#3234](http://nuget.codeplex.com/workitem/3234) -Nomad 프로젝트에 대 한 지원 사용
7. [Corin Blaikie](http://www.codeplex.com/site/users/view/corinblaikie) ( [@corinblaikie](https://twitter.com/corinblaikie) )
    - [#3252](http://nuget.codeplex.com/workitem/3252) -파일이 없으면 종료 코드 0을 사용 하 여 push command를 수정 하지 못합니다.
8. [Martin Veselý](http://www.codeplex.com/site/users/view/veselkamartin)
    - [#3226](http://nuget.codeplex.com/workitem/3226) -프로젝트에서 데이터베이스 프로젝트를 참조할 때 Add-BindingRedirect 명령을 사용 하 여 버그를 수정 합니다.
9. [Miroslav Bajtos](http://www.codeplex.com/site/users/view/miroslavbajtos) ( [@bajtos](https://twitter.com/bajtos) )
    - [#2891](http://nuget.codeplex.com/workitem/2891) -nuget의 버그를 수정 합니다. ' exclude ' 특성에서 와일드 카드를 구문 분석 합니다.
10. [Justin Dearing](http://www.codeplex.com/site/users/view/zippy1981) ( [@zippy1981](https://twitter.com/zippy1981) )
     - [#3307](http://nuget.codeplex.com/workitem/3307) 수정 버그 `NuGet.targets` 는 패키지를 복원할 때 $ (Platform)를 nuget.exe에 전달 하지 않습니다.
11. [Federici](http://www.codeplex.com/site/users/view/benerdin)
     - [#3294](http://nuget.codeplex.com/workitem/3294) -이름은 같지만 대/소문자가 다른 파일을 추가할 수 있는 nuget.exe 패키지 명령의 버그를 수정 합니다. 결과적으로 "항목이 이미 있습니다." 예외가 발생 합니다.
12. [Daniel Cazzulino](http://www.codeplex.com/site/users/view/dcazzulino) ( [@kzu](https://twitter.com/kzu) )
     - [#2990](http://nuget.codeplex.com/workitem/2990) -버전 속성을 NetPortableProfile 클래스에 추가 합니다.
13. [David Simner](https://www.codeplex.com/site/users/view/DavidSimner)
     - [#3460](https://nuget.codeplex.com/workitem/3460) -requireapikey = true 인 경우에는 버그 NullReferenceException를 수정 하지만 헤더 X NUGET-apikey는 없습니다.
14. [Michael Friis](https://www.codeplex.com/site/users/view/friism) ( [@friism](https://twitter.com/friism) )
     - [#3278](https://nuget.codeplex.com/workitem/3278) -MonoDevelop에서 제대로 작동 하도록 NuGet 빌드 대상 파일을 수정 합니다.
15. [Pranav Krishnamoorthy](https://www.codeplex.com/site/users/view/pranavkm) [@pranav_km](https://twitter.com/pranav_km)
     - 병렬화를 높여 복원 명령 성능 향상

## <a name="notable-features-in-the-release"></a>릴리스의 주요 기능

### <a name="package-restore-by-default-with-implicit-consent"></a>기본적으로 패키지 복원 (암시적 동의 포함)

NuGet 2.7은 패키지 복원에 대 한 새로운 접근 방식을 소개 하 고 주요 장애물을 극복 합니다. 이제 패키지 복원 동의가 기본적으로 설정 되어 있습니다. 새 접근 방법과 암시적 동의의 조합은 패키지 복원 시나리오를 크게 간소화 합니다.

#### <a name="implicit-consent"></a>암시적 동의

NuGet 버전 2.0, 2.1, 2.2, 2.5 및 2.6을 사용 하는 경우 사용자는 NuGet이 빌드하는 동안 누락 된 패키지를 다운로드 하도록 명시적으로 허용 해야 합니다. 이 동의가 명시적으로 제공 되지 않은 경우에는 사용자에 게 동의가 부여 될 때까지 패키지 복원을 사용 하도록 설정한 솔루션이 빌드되지 않습니다.

NuGet 2.7부터 패키지 복원 동의가 기본적으로 설정 되어 있으며, 원하는 경우 Visual Studio의 NuGet 설정에서 확인란을 사용 하 여 사용자가 패키지 복원을 명시적으로 *옵트아웃 (opt out* ) 할 수 있습니다. 암시적 동의의 이러한 변경은 다음 환경의 NuGet에 영향을 줍니다.

* Visual Studio 2013 Preview
* Visual Studio 2012
* Visual Studio 2010
* nuget.exe Command-Line 유틸리티

#### <a name="automatic-package-restore-in-visual-studio"></a>Visual Studio에서 자동 패키지 복원

NuGet 2.7부터 NuGet은 솔루션에 대해 패키지 복원이 명시적으로 사용 하도록 설정 되지 않은 경우에도 Visual Studio에서 빌드하는 동안 누락 된 패키지를 자동으로 다운로드 합니다. 이 자동 패키지 복원은 프로젝트 또는 솔루션을 빌드할 때 Visual Studio에서 발생 하지만 MSBuild를 호출 하기 전에 발생 합니다. 이 경우 다음과 같은 몇 가지 중요 한 이점이 있습니다.

1. 솔루션에서 "NuGet 패키지 복원 사용" 제스처를 사용할 필요가 없습니다.
1. 프로젝트를 수정할 필요가 없으며, NuGet이 프로젝트를 변경 하 여 패키지 복원을 사용할 수 있도록 합니다.
1. Msbuild를 호출 하기 전에이를 포함 하는 모든 NuGet 패키지는 msbuild를 호출 *하기 전에* 복원 되어 해당 props/대상이 빌드 중에 올바르게 인식 되도록 합니다.

Visual Studio에서 자동 패키지 복원을 사용 하려면 다음 작업을 수행 해야 합니다.

1. 폴더를 체크 인 하지 않음 `packages`

소스 제어에서 폴더를 생략 하는 방법에는 여러 가지가 있습니다 `packages` . 자세한 내용은 [패키지 및 소스 제어](../consume-packages/packages-and-source-control.md) 항목을 참조 하세요.

모든 사용자가 암시적으로 자동 패키지 복원 동의에 옵트인 하는 동안 Visual Studio의 패키지 관리자 설정을 통해 쉽게 옵트아웃 (opt out) 할 수 있습니다.

![패키지 관리자 설정](./media/NuGet-2.7/package-manager-settings.png)

#### <a name="simplified-package-restore-from-the-command-line"></a>Command-Line에서 간소화 된 패키지 복원

NuGet 2.7에는 nuget.exe에 대 한 새로운 기능이 도입 되었습니다. `nuget.exe restore`

이 새 복원 명령을 사용 하면 솔루션 파일 또는 폴더를 인수로 수락 하 여 단일 명령으로 솔루션에 대 한 모든 패키지를 쉽게 복원할 수 있습니다. 또한이 인수는 현재 폴더에 솔루션을 하나만 포함 하는 경우에만 적용 됩니다. 즉, 다음은 모두 단일 솔루션 파일 (MySolution .sln)이 포함 된 폴더에서 작동 한다는 것을 의미 합니다.

1. nuget.exe 복원 MySolution .sln
1. 복원 nuget.exe
1. 복원 nuget.exe

복원 명령은 솔루션 파일을 열고 솔루션 내의 모든 프로젝트를 찾습니다. 여기에서 `packages.config` 각 프로젝트에 대 한 파일을 찾고 찾은 모든 패키지를 복원 합니다. 또한 파일에 있는 솔루션 수준 패키지도 복원 `.nuget\packages.config` 합니다. 새 복원 명령에 대 한 자세한 내용은 [명령줄 참조](../reference/cli-reference/cli-ref-restore.md)에서 찾을 수 있습니다.

#### <a name="the-new-package-restore-workflow"></a>새 패키지 복원 워크플로

새 워크플로를 도입 하기 때문에 패키지 복원에 대 한 이러한 변경 사항에 대해 기쁘게 생각 합니다. 원본 제어에서 패키지를 생략 하려면 간단히 폴더를 커밋하지 마세요 `packages` . 솔루션을 열고 빌드하는 Visual Studio 사용자는 패키지가 자동으로 복원 되는 것을 볼 수 있습니다. 명령줄 빌드의 경우를 호출 하기 전에를 호출 하면 됩니다 `nuget.exe restore` `msbuild` . 솔루션에서 "NuGet 패키지 복원 사용" 제스처를 사용 하는 것이 더 이상 기억나지 않아도 되므로 빌드를 변경 하기 위해 프로젝트를 수정할 필요가 없습니다. 또한 MSBuild 가져오기를 포함 하는 패키지에 대해 훨씬 향상 된 환경을 제공 합니다. 특히, \build 폴더에서 [자동으로 props/targets 파일을 가져오기](../release-notes/nuget-2.5.md#automatic-import-of-msbuild-targets-and-props-files) 위해 NuGet의 최근 기능을 통해 추가 된 가져오기에 대해 훨씬 향상 된 환경을 제공 합니다.

지금까지 수행한 작업 외에도 몇 가지 중요 한 파트너를 사용 하 여이 새로운 접근 방법을 왕복 하 고 있습니다. 이러한 방법에 대 한 구체적인 타임 라인은 없지만 각 파트너는 새 접근 방식에 대 한 것 만큼 기쁘게 생각 합니다.

* Team Foundation Service-에 대 한 호출을 기본 빌드 시나리오로 통합 하기 위해 작업 중 `nuget.exe restore` 입니다.
* Microsoft Azure 웹 사이트-프로젝트를 Azure에 푸시할 수 있도록 하 고 `nuget.exe restore` 웹 사이트가 빌드되기 전에 호출 됩니다.
* TeamCity-TeamCity .x 용 NuGet 설치 관리자 플러그 인을 업데이트 하는 중입니다.
* AppHarbor-리포지토리를 AppHarbor로 푸시하는 데 사용 되며 `nuget.exe restore` 솔루션이 빌드 전에 호출 됩니다.

위의 각 파트너는 자신의 nuget.exe 복사본을 사용 하 고 솔루션에 nuget.exe를 전달할 필요가 없습니다.

#### <a name="known-issues"></a>알려진 문제

초기 2.7 릴리스와 함께 nuget.exe 복원에는 두 가지 알려진 문제가 있었지만, [nuget.exe 패키지](http://www.nuget.org/packages/NuGet.CommandLine/)에 대 한 업데이트로 9/6/2013에서 수정 되었습니다.  이 업데이트는 CodePlex의 [NuGet 2.7 다운로드 페이지](https://nuget.codeplex.com/releases/view/107605) 에서도 사용할 수 있습니다.  를 실행 `nuget.exe update -self` 하면 최신 릴리스로 업데이트 됩니다.

수정 된는 다음과 같습니다.

1. [SLN 파일을 사용 하는 경우 Mono에서 새 패키지 복원이 작동 하지 않음](https://nuget.codeplex.com/workitem/3596)
1. [새 패키지 복원이 Wix 프로젝트에서 작동 하지 않음](https://nuget.codeplex.com/workitem/3598)

[솔루션 폴더의 프로젝트에 대해 자동 패키지 복원이 작동 하지 않는](https://nuget.codeplex.com/workitem/3625)새 패키지 복원 워크플로에도 알려진 문제가 있습니다. 이 문제는 NuGet 2.7.1에서 수정 되었습니다.

### <a name="project-retargeting-and-upgrade-build-errorswarnings"></a>프로젝트 대상 다시 지정 및 업그레이드 빌드 오류/경고

프로젝트의 대상을 변경 하거나 프로젝트를 업그레이드 한 후에는 일부 NuGet 패키지가 제대로 작동 하지 않는 것을 확인할 수 있습니다. 아쉽게도이에 대해서는 설명 하지 않으며이를 해결 하는 방법에 대 한 지침은 없습니다. NuGet 2.7을 사용 하면 설치 된 NuGet 패키지에 영향을 주는 방식으로 프로젝트의 대상을 변경 하거나 업그레이드 한 경우 일부 Visual Studio 이벤트를 사용 하 여 인식 됩니다.

대상 사용자 또는 업그레이드의 영향을 받는 패키지가 있으면 즉시 알 수 있도록 빌드 오류를 생성 합니다. 즉시 빌드 오류 외에도 `requireReinstallation="true"` `packages.config` 파일에서 대상 변경의 영향을 받는 모든 패키지에 대 한 플래그를 유지 하 고 Visual Studio의 각 후속 빌드에서 해당 패키지에 대 한 빌드 경고를 발생 시킵니다.

NuGet은 영향을 받는 패키지를 다시 설치 하기 위해 자동 작업을 수행할 수 없지만,이를 통해 패키지를 다시 설치 해야 하는 경우를 검색 하는 데 도움이 될 것입니다. 또한 이러한 오류 메시지가 표시 되는 [패키지 다시 설치 지침 설명서](../consume-packages/reinstalling-and-updating-packages.md) 를 사용 하 고 있습니다.

### <a name="nuget-configuration-defaults"></a>NuGet 구성 기본값

대부분의 회사에서는 내부적으로 NuGet을 사용 하지만 개발자가 nuget.org 대신 내부 패키지 원본을 사용 하도록 안내 합니다. NuGet 2.7에는에 대해 시스템 차원의 기본값을 지정할 수 있도록 하는 구성 기본값 기능이 도입 되었습니다.

1. 패키지 원본 사용
1. 등록 되었지만 사용 하지 않도록 설정 된 패키지 소스
1. 기본 nuget.exe 푸시 원본

이제 이러한 각을에 있는 파일 내에서 구성할 수 있습니다 `%ProgramData%\NuGet\NuGetDefaults.Config` . 이 구성 파일에서 패키지 소스를 지정 하는 경우 기본 nuget.org 패키지 원본이 자동으로 등록 되지 않고의 해당 원본 항목이 `NuGetDefaults.Config` 등록 됩니다.

이 기능을 사용 하는 데 필요 하지는 않지만 회사에서 `NuGetDefaults.Config` 그룹 정책를 사용 하 여 파일을 배포할 것으로 간주 합니다.

*이 기능을 통해 개발자의 NuGet 설정에서 패키지 소스가 제거 되지는 않습니다. 즉, 개발자가 이미 NuGet을 사용 하 고 있으므로 nuget.org 패키지 소스가 등록 된 경우 파일을 만든 후에는 제거 되지 않습니다 `NuGetDefaults.Config` .*

이 기능에 대 한 자세한 내용은 [NuGet 구성 기본값](../consume-packages/configuring-nuget-behavior.md#nuget-defaults-file) 을 참조 하세요.

### <a name="renaming-the-default-package-source"></a>기본 패키지 원본 이름 바꾸기

NuGet은 항상 nuget.org를 가리키는 "NuGet 공식 패키지 원본" 이라는 기본 패키지 원본을 등록 했습니다. 이 이름은 verbose 이며 실제로 가리키는 위치도 지정 하지 않았습니다. 이러한 두 문제를 해결 하기 위해 UI에서이 패키지 소스의 이름을 "nuget.org"로 변경 했습니다. 패키지 원본에 대 한 URL도 "www"를 포함 하도록 변경 되었습니다. 찾습니다. NuGet 2.7을 사용 하면 기존 "NuGet 공식 패키지 원본"이 자동으로 "nuget.org"로 이름으로 업데이트 되 고 " <https://www.nuget.org/api/v2/> "가 URL로 업데이트 됩니다.

### <a name="performance-improvements"></a>성능 향상

2.7에서 약간의 성능이 향상 되어 메모리 사용 공간이 줄어들고, 디스크 사용이 줄어들고, 패키지 설치 속도가 빨라집니다. 또한 전체 페이로드를 줄이는 OData 기반 피드에 대해 더 현명한 쿼리를 만들었습니다.

### <a name="new-extensibility-apis"></a>새 확장성 Api

이전 릴리스에서 누락 된 기능의 차이를 채우도록 확장성 서비스에 몇 가지 새로운 Api를 추가 했습니다.

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

### <a name="development-only-dependencies"></a>Development-Only 종속성

이 기능은 [Adam Ralph](https://twitter.com/adamralph) 에서 제공 했으며 패키지 작성자는 개발 시에만 사용 되었으며 패키지 종속성이 필요 하지 않은 종속성을 선언할 수 있습니다. `developmentDependency="true"`에서 패키지에 특성을 추가 하면에서 `packages.config` `nuget.exe pack` 더 이상 해당 패키지를 종속성으로 포함 하지 않습니다.

### <a name="removed-support-for-visual-studio-2010-express-for-windows-phone"></a>Windows Phone Visual Studio 2010 Express에 대 한 지원이 제거 되었습니다.

2.7의 새 패키지 복원 모델은 기본 NuGet VSPackage와 다른 새 VSPackage에 의해 구현 됩니다. 기술적 문제로 인해이 새로운 VSPackage는 다른 지원 되는 Visual Studio Sku와 동일한 코드 베이스를 공유 하는 *Windows Phone SKU 용 Visual studio 2010 Express* 에서 제대로 작동 하지 않습니다. 따라서 NuGet 2.7 부터는 게시 된 확장의 *Windows Phone에 대 한 Visual Studio 2010 Express* 에 대 한 지원이 삭제 됩니다. Visual studio *2010 Express For Web* 에 대 한 지원은 Visual Studio 확장 갤러리에 게시 된 기본 확장에도 포함 되어 있습니다.

Visual Studio의 해당 버전/버전에서 아직 NuGet을 사용 하는 개발자 수를 확실히 알 수 있기 때문에 해당 사용자를 위한 별도의 Visual Studio 확장을 게시 하 고 Visual Studio 확장 갤러리가 아닌 CodePlex에 게시 합니다. 해당 확장을 계속 유지 관리 하지는 않지만이에 영향을 주는 경우 CodePlex에서 문제를 신고 하 여 알려주세요.

NuGet 패키지 관리자 (Visual Studio 2010 Express for Windows Phone)를 다운로드 하려면 [nuget 2.7 다운로드](https://nuget.codeplex.com/releases/view/107605) 페이지를 방문 하세요.

### <a name="bug-fixes"></a>버그 픽스

이러한 기능 외에도이 NuGet 릴리스에는 다른 많은 버그 수정이 포함 되어 있습니다. 릴리스에서 해결 된 총 97 개의 문제가 있습니다. NuGet 2.7에서 수정 된 작업 항목의 전체 목록은 [이 릴리스에 대 한 Nuget 문제 추적기](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.7&status=all)를 확인 하세요.
