---
title: NuGet 질문과 대답
description: 명령줄 및 Visual Studio에서 NuGet을 사용하고 NuGet 갤러리에서 작업하는 경우와 관련된 일반적인 질문과 대답입니다.
author: shishirx34
ms.author: shishirh
ms.date: 01/15/2019
ms.topic: conceptual
ms.openlocfilehash: 1c838116f9737b01ea3f9ca17f5d5002f6548044
ms.sourcegitcommit: 85bf94e0efcfcee1f914650bdc142309ef3e06d9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57196215"
---
# <a name="nuget-frequently-asked-questions"></a>NuGet 질문과 대답

**NuGet을 실행하는 데 필요한 것은 무엇인가요?**

UI 및 명령줄 도구에 관한 모든 정보는 [설치 가이드](../install-nuget-client-tools.md)에서 사용할 수 있습니다.

**NuGet은 Mono를 지원하나요?**

`nuget.exe` 명령줄 도구는 Mono 3.2 이상에서 빌드하고 실행되며, Mono에서 패키지를 만들 수 있습니다.

`nuget.exe`는 Windows에서 완벽하게 작동하지만, Linux 및 OS X에서는 알려진 문제가 있습니다. GitHub의 [Mono 문제](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono)를 참조하세요.

[그래픽 클라이언트](https://github.com/mrward/monodevelop-nuget-addin)는 MonoDevelop용 추가 기능으로 사용할 수 있습니다.

**패키지에 포함된 내용과 애플리케이션에 안정적이고 유용한 지 여부를 확인하려면 어떻게 해야 할까요?**

패키지 학습에 대한 기본 소스는 nuget.org(또는 다른 개인 피드)의 목록 페이지입니다. nuget.org의 각 패키지 페이지에는 패키지에 대한 설명, 해당 버전 기록 및 사용 통계가 포함되어 있습니다. 또한 패키지 페이지의 **정보** 섹션에는 프로젝트의 웹 사이트에 대한 링크가 포함되어 있으며, 여기서 패키지를 사용하는 방법을 알아보는 데 도움이 되는 많은 예제와 기타 문서를 찾을 수 있습니다.

자세한 내용은 [패키지 찾기 및 선택](../consume-packages/finding-and-choosing-packages.md)을 참조하세요.

## <a name="nuget-in-visual-studio"></a>Visual Studio의 NuGet

**다른 Visual Studio 제품에서는 NuGet을 어떻게 지원하나요?**

- Windows에서 Visual Studio는 [패키지 관리자 UI](../tools/package-manager-ui.md)와 [패키지 관리자 콘솔](../tools/package-manager-console.md)을 지원합니다.
- Mac용 Visual Studio에는 [프로젝트에 NuGet 패키지 포함](/visualstudio/mac/nuget-walkthrough)에서 설명한 대로 NuGet 기능이 기본적으로 제공됩니다.
- Visual Studio Code(모든 플랫폼)에는 직접적인 NuGet 통합이 없습니다. [NuGet CLI](../tools/nuget-exe-cli-reference.md) 또는 [dotnet CLI](../tools/dotnet-commands.md)를 사용하세요.
- Azure DevOps는 [NuGet 패키지를 복원하는 빌드 단계](/vsts/build-release/tasks/package/nuget)를 제공합니다. 또한 [Azure DevOps에서 전용 NuGet 패키지 피드를 호스팅](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish)할 수도 있습니다.

**설치된 NuGet 도구의 정확한 버전을 확인하려면 어떻게 할까요?**

Visual Studio에서 **도움말 > Microsoft Visual Studio 정보** 명령을 사용하고 **NuGet 패키지 관리자** 옆에 표시된 버전을 확인합니다.

또는 패키지 관리자 콘솔(**도구 > NuGet 패키지 관리자 > 패키지 관리자 콘솔**)을 시작하고, `$host`를 입력하여 버전을 포함한 NuGet 관련 정보를 확인합니다.

**NuGet에서 지원하는 프로그래밍 언어는 무엇인가요?**

NuGet은 일반적으로 .NET 언어에서 작동하며, .NET 라이브러리를 프로젝트에 가져오도록 설계되었습니다. 또한 일부 프로젝트 형식에서 MSBuild 및 Visual Studio 자동화를 지원하므로 다른 프로젝트와 언어를 다양한 수준으로 지원합니다.

최신 버전의 NuGet은 C#, Visual Basic, F#, WiX 및 C++을 지원합니다.

**NuGet에서 지원하는 프로젝트 템플릿은 무엇인가요??**

NuGet은 Windows, 웹, 클라우드, SharePoint, Wix 등과 같은 다양한 프로젝트 템플릿을 완벽하게 지원합니다.

**Visual Studio 템플릿의 일부인 패키지를 업데이트하려면 어떻게 할까요?**

패키지 관리자 UI에서 **업데이트** 탭으로 이동하여 **모두 업데이트**를 선택하거나, 패키지 관리자 콘솔에서 [`Update-Package` 명령](../tools/ps-ref-update-package.md)을 사용합니다.

템플릿 자체를 업데이트하려면 템플릿 리포지토리를 수동으로 업데이트해야 합니다. 이 주제에 대한 [Xavier Decoster의 블로그](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages)를 참조하세요. 모든 종속성의 최신 버전이 서로 호환되지 않을 경우 수동으로 업데이트하면 템플릿이 손상될 수 있으므로 이 작업은 사용자의 책임 하에 수행해야 합니다.

**Visual Studio 외부에서 NuGet을 사용할 수 있나요?**

예, NuGet은 명령줄에서 직접 작동합니다. [설치 가이드](../install-nuget-client-tools.md) 및 [CLI 참조](../tools/nuget-exe-cli-reference.md)를 참조하세요.

## <a name="nuget-command-line"></a>NuGet 명령줄

**최신 버전의 NuGet 명령줄 도구를 가져오려면 어떻게 할까요?**

[설치 가이드](../install-nuget-client-tools.md)를 참조하세요.

**nuget.exe에 대한 라이선스는 무엇인가요?**

MIT 라이선스 조건 하에 nuget.exe를 재배포할 수 있습니다. 재배포하도록 선택한 nuget.exe의 복사본을 업데이트하고 제공해야 합니다.

**NuGet 명령줄 도구는 확장할 수 있나요?**

예, [Rob Reynold의 게시물](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx)에서 설명한 대로 사용자 지정 명령을 `nuget.exe`에 추가하면 됩니다.

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a>NuGet 패키지 관리자 콘솔(Windows의 Visual Studio)

**패키지 관리자 콘솔에서 DTE 개체에 액세스하려면 어떻게 할까요?**

Visual Studio 자동화 개체 모델의 최상위 개체를 DTE(개발 도구 환경) 개체라고 합니다. 콘솔에서 `$DTE`라는 변수를 통해 이 개체를 제공합니다. 자세한 내용은 Visual Studio 확장성 설명서에서 [자동화 모델 개요](/visualstudio/extensibility/internals/automation-model-overview)를 참조하세요.

**$DTE 변수를 DTE2 형식으로 캐스팅하려고 하지만 오류가 발생합니다. "EnvDTE.DTEClass" 형식의 "EnvDTE.DTEClass" 값을 "EnvDTE80.DTE2" 형식으로 변환할 수 없습니다. 무엇이 문제인가요?**

이는 PowerShell이 COM 개체와 상호 작용하는 방법과 관련하여 알려진 문제입니다. 다음과 같이 수행해 보세요.

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

`Get-Interface`는 NuGet PowerShell 호스트에서 추가한 도우미 함수입니다.

## <a name="creating-and-publishing-packages"></a>패키지 만들기 및 게시

**내 패키지를 피드에 나열하려면 어떻게 할까요?**

[패키지 만들기 및 게시](../quickstart/create-and-publish-a-package.md)를 참조하세요.

**다른 버전의 .NET Framework를 대상으로 하는 여러 버전의 라이브러리가 있습니다. 이를 지원하는 단일 패키지를 빌드하려면 어떻게 할까요?**

[여러 .NET Framework 버전 지원](../create-packages/supporting-multiple-target-frameworks.md)을 참조하세요.

**내 리포지토리 또는 피드를 설정하려면 어떻게 할까요?**

[패키지 호스팅 개요](../hosting-packages/overview.md)를 참조하세요.

**NuGet 피드에 패키지를 대량으로 업로드하려면 어떻게 해야 할까요?**

[NuGet 패키지 대량 게시](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx)(jeffhandly.com)를 참조하세요.

## <a name="working-with-packages"></a>패키지 작업

**프로젝트 수준 패키지와 솔루션 수준 패키지의 차이점은 무엇인가요?**

솔루션 수준 패키지(NuGet 3.x 이상)는 솔루션에 한 번만 설치되며 솔루션의 모든 프로젝트에서 사용할 수 있습니다. 프로젝트 수준 패키지는 이를 사용하는 각 프로젝트에 설치됩니다. 또한 솔루션 수준 패키지는 패키지 관리자 콘솔 내에서 호출할 수 있는 새 명령을 설치할 수도 있습니다.

**인터넷 연결 없이 NuGet 패키지를 설치할 수 있나요?**

예, Scott Hanselman의 블로그 게시물인 [nuget.org가 다운되었을 때(또는 비행기에 탑승한 경우) NuGet에 액세스하는 방법](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx)(hanselman.com)을 참조하세요.

**기본 패키지 폴더와 다른 위치에 패키지를 설치하려면 어떻게 할까요?**

`nuget config -set repositoryPath=<path>`를 사용하여 `Nuget.Config`의 [`repositoryPath`](../reference/nuget-config-file.md#config-section) 설정을 지정합니다.

**NuGet 패키지 폴더를 원본 제어에 추가하지 않도록 방지하려면 어떻게 할까요?**

`Nuget.Config`의 [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section)을 `true`로 설정합니다. 이 키는 솔루션 수준에서 작동하므로 `$(Solutiondir)\.nuget\Nuget.Config` 파일에 추가해야 합니다. Visual Studio에서 패키지 복원을 사용하면 이 파일이 자동으로 만들어집니다.

**패키지 복원을 해제하려면 어떻게 할까요?**

[패키지 복원 사용 설정/해제](../consume-packages/package-restore.md#enabling-and-disabling-package-restore)를 참조하세요.

**원격 종속성이 있는 로컬 패키지를 설치할 때 "종속성을 확인할 수 없습니다."라는 오류 메시지가 표시되는 이유는 무엇인가요?**

프로젝트에 로컬 패키지를 설치할 때 **모든** 원본을 선택해야 합니다. 이렇게 하면 하나만 사용하는 대신 모든 피드를 집계합니다. 이 오류가 나타나는 이유는 로컬 리포지토리의 사용자가 기업 정책으로 인해 실수로 원격 패키지를 설치하지 않도록 하려는 경우가 많기 때문입니다.

**동일한 폴더에 여러 프로젝트가 있습니다. 각 프로젝트마다 별도의 packages.config 파일을 사용하려면 어떻게 해야 할까요?**

개별 프로젝트가 별도의 폴더에 있는 대부분의 프로젝트에서는 NuGet이 각 프로젝트의 `packages.config` 파일을 식별하므로 문제가 되지 않습니다. 동일한 폴더에 NuGet 3.3 이상 및 여러 프로젝트가 있는 경우, `packages.{project-name}.config` 패턴을 사용하는 `packages.config` 파일 이름에 프로젝트 이름을 삽입할 수 있으며, NuGet에서 해당 파일을 사용합니다.

이는 PackageReference를 사용할 때 각 프로젝트 파일에 자체의 종속성 목록이 포함되므로 문제가 되지 않습니다.

**내 리포지토리 목록에 nuget.org가 표시되지 않습니다. 다시 가져오려면 어떻게 할까요?**

- 원본 목록에 `https://api.nuget.org/v3/index.json`을 추가합니다. 또는
- `%appdata%\.nuget\NuGet.Config`(Windows) 또는 `~/.nuget/NuGet/NuGet.Config`(Mac/Linux)를 삭제하고 NuGet에서 다시 만들도록 합니다.

**패키지에서 특정 라이선스 정보를 제공하지 않는 경우 기본 사용 조건은 무엇인가요?**

각 패키지는 패키지에 포함된 사용 조건이 적용됩니다. 패키지를 액세스, 다운로드 또는 획득하기 전에 해당 사용 조건을 검토해야 합니다. nuget.org의 패키지 페이지에 있는 **라이선스 정보** 링크를 사용합니다.

패키지에서 사용 조건을 지정하지 않은 경우 nuget.org 패키지 페이지의 **연락처 소유자** 링크를 사용하여 패키지 소유자에게 직접 문의해 보세요. Microsoft는 타사 패키지 공급자로부터 사용자에게 지적 재산권을 부여하지 않으며 타사에서 제공한 정보에 대해 책임을 지지 않습니다.

## <a name="managing-packages-on-nugetorg"></a>NuGet.org의 패키지 관리

**패키지 메타데이터를 업로드한 후에 편집할 수 있나요?**

NuGet은 모든 패키지에 서명을 권장합니다. 패키지 서명의 디자인 원칙은 nuspec을 포함한 서명된 패키지 콘텐츠를 변경할 수 없다는 것입니다. 패키지 메타데이터를 편집하면 nuspec이 변경되고 기존 서명이 무효화됩니다. 패키지를 만든 후에 패키지 메타데이터를 편집할 필요가 없도록 기존 워크플로를 수정하는 것이 좋습니다.

패키지에 대해 나열된 종속성은 패키지 자체에서 자동으로 생성되며 편집할 수 없습니다.

또한 [int.nugettest.org](https://int.nugettest.org)에 패키지를 업로드하는 것은 공용 갤러리에서 패키지를 사용하지 않고도 패키지를 테스트하고 유효성을 검사할 수 있는 좋은 방법입니다. API 엔드포인트: https://apiint.nugettest.org/v3/index.json

**NuGet.org에 게시된 패키지를 삭제할 수 있나요?**

일반적으로 NuGet.org에 게시된 패키지 삭제를 지원하지 않습니다. [패키지 삭제에 대한 정책](../policies/deleting-packages)에 대해 자세히 알아보세요.

**나중에 게시되는 패키지의 이름을 예약할 수 있나요?**

예. 계정에 대한 패키지 ID 접두사를 요청하여 [nuget.org](https://www.nuget.org/)에서 패키지 ID를 예약할 수 있습니다. 패키지 ID 접두사를 요청하려면 [설명서](https://docs.microsoft.com/nuget/reference/id-prefix-reservation)의 지침을 따르세요.

**패키지 소유권을 주장하려면 어떻게 할까요?**

[nuget.org에서 패키지 소유자 관리](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg)를 참조하세요.

**소프트웨어 라이선스를 위반하는 패키지 소유자를 처리하려면 어떻게 할까요?**

NuGet 커뮤니티에서 패키지 소유자와 다른 소프트웨어 소유자 간에 발생할 수 있는 분쟁을 해결하기 위해 함께 노력하는 것이 좋습니다. nuget.org 관리자에게 중재를 요청하기 전에 따라야 할 [분쟁 해결 절차](../policies/dispute-resolution.md)가 마련되어 있습니다.

**내 테스트 패키지를 nuget.org에 업로드하는 것이 좋을까요?**

테스트를 위해 [int.nugettest.org](https://int.nugettest.org) 또는 대체 공용 NuGet 서버(예: [myget.org](https://myget.org) 또는 [Azure DevOps](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/))를 사용할 수 있습니다.

int.nugettest.org에 업로드된 패키지는 유지되지 않을 수 있습니다.

**nuget.org에 업로드할 수 있는 패키지의 최대 크기는 무엇인가요?**

nuget.org는 최대 250MB의 패키지를 허용하지만, 가능한 한 패키지를 1MB 미만으로 유지하고 종속성을 사용하여 패키지를 함께 연결하는 것이 좋습니다. 경험상 패키지는 충돌을 방지하기 위해 하나의 어셈블리만 포함합니다.

NuGet은 HTTP를 사용하여 패키지를 다운로드하므로, 큰 패키지는 작은 패키지보다 설치에 실패할 가능성이 높습니다.

여러 패키지 간에 종속성을 공유하여 NuGet 패키지의 소비자에 대한 전체 다운로드 크기를 줄일 수 있습니다.

종속성은 대부분 정적이며 변경되지 않습니다. 코드에서 버그를 수정하는 경우 종속성을 업데이트할 필요가 없을 수도 있습니다. 종속성을 번들로 제공하면 매번 더 큰 패키지를 다시 전달하게 됩니다. NuGet 패키지를 관련 종속성으로 분할하면 패키지 소비자가 훨씬 더 세부적으로 업그레이드할 수 있습니다.

## <a name="nugetorg-not-accessible"></a>nuget.org에 액세스할 수 없음

**nuget.org에서 패키지를 다운로드하거나 업로드할 수 없는 이유는 무엇인가요?**

먼저 최신 버전의 NuGet을 사용하고 있는지 확인합니다. 해당 버전이 계속 실패하면 [지원 부서에 문의](https://www.nuget.org/policies/Contact)하여 다음을 포함한 추가 연결 문제 해결 정보를 제공합니다.

- 사용 중인 NuGet 버전
- 사용 중인 패키지 원본
- 자세한 세부 정보가 있는 복원 로그
- MTR 또는 Fiddler 추적(아래 참조)
- 사용자의 지리적 지역
- 머신이 프록시 또는 방화벽 뒤에 있는지 여부는?
- 머신이 클라우드 공급 기업의 데이터 센터(Azure, AWS 등)에 위치해 있나요? 그렇다면 공급 기업 및 지역의 이름을 제공하세요.

*MTR을 캡처하려면:*

- [http://winmtr.net/download/](http://winmtr.net/)에서 WinMTR 다운로드
- 호스트 이름으로 `api.nuget.org`를 입력하고 **시작**을 클릭합니다.
- **보냄** 열이 100개 이상이 될 때까지 기다립니다.

    ![캡처 중인 MTR](media/mtr.png)

- 클립보드에 텍스트를 복사합니다.

*Fiddler를 캡처하려면:*

- 최신 버전의 [Fiddler](http://www.telerik.com/download/fiddler)를 설치합니다.
- Fiddler를 시작하고 **파일 > 트래픽 캡처** 메뉴를 사용하여 트래픽 캡처를 사용하지 않도록 설정합니다.
- 모든 세션을 제거합니다(목록에서 모든 항목을 선택하고 **삭제** 키를 누름).
- **도구 > Fiddler 옵션...** 메뉴의 **HTTPS** 탭에서 **HTTPS 트래픽 해독**을 선택하여 HTTPS 트래픽을 캡처하도록 Fiddler를 구성합니다.
- Visual Studio를 닫습니다.
- **파일 > 트래픽 캡처** 메뉴를 활성화합니다.
- Visual Studio 또는 nuget.exe .exe를 시작하고 작동하지 않는 작업을 수행합니다. 이러한 작업으로 생성된 트래픽이 Fiddler에 표시됩니다.
- 작업이 실행되면 **파일 > 저장 > 모든 세션**을 사용하여 캡처된 세션을 저장합니다.

참고: Fiddler를 통해 NuGet 트래픽을 라우팅하기 위해 `HTTP_PROXY` 환경 변수를 `http://127.0.0.1:8888`로 설정해야 할 수도 있습니다.

실패하면 [StackOverflow 게시물에서 언급한 팁](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall)을 사용해 보세요.

## <a name="what-is-the-api-endpoint-for-nugetorg"></a>nuget.org에 대한 API 엔드포인트는 무엇인가요?

NuGet 클라이언트에서 nuget.org를 패키지 리포지토리로 사용하려면 다음과 같은 V3 API 엔드포인트를 사용해야 합니다. 

**`https://api.nuget.org/v3/index.json`**

이전 버전의 클라이언트는 V2 프로토콜을 사용하여 nuget.org에 연결할 수 있습니다. 그러나 NuGet 클라이언트 3.0 이상에는 V2 프로토콜을 사용하는 느리고 신뢰할 수 없는 서비스가 포함됩니다.

`https://www.nuget.org/api/v2`(사용되지 않음) **참고:** 최고의 안정성을 위해 "www."를 사용합니다.

## <a name="nugetorg-account-management"></a>nuget.org 계정 관리

### <a name="how-to-create-a-new-nugetorg-account"></a>새 nuget.org 계정을 만들려면 어떻게 하나요?

nuget.org 계정을 만들려면 개인 MSA(Microsoft 계정) 또는 AAD(Azure Active Directory) 계정이 있어야 합니다. 없는 경우 계정을 [만들](https://signup.live.com) 수 있습니다. MSA 또는 AAD 계정이 있는 경우 다음 단계를 따릅니다.
1. [nuget.org 로그인 페이지](https://www.nuget.org/users/account/LogOn)로 이동합니다.
1. **Microsoft로 로그인** 단추를 클릭합니다.
1. MSA/AAD 계정 세부 정보를 입력합니다.
1. *NuGet.org* 애플리케이션에 지정된 사용 권한을 수락하세요.
1. nuget.org로 리디렉션되고 사용자 이름을 등록하라는 메시지가 표시됩니다.
1. 입력 상자에서 사용자 이름을 지정합니다. 사용자 이름은 대/소문자를 구분**하며** 나중에 변경/이름을 바꿀 수 없습니다.
1. **등록** 단추를 클릭합니다.

이제 nuget.org 계정이 있습니다. [계정 설정](https://www.nuget.org/account) 페이지에서 계정 관리를 수행할 수 있습니다.

### <a name="how-to-recover-nugetorg-password-login"></a>nuget.org 암호 로그인을 복구하려면 어떻게 하나요?

[nuget.org 암호 로그인이 지원되지 않습니다](https://blog.nuget.org/20180515/NuGet.org-will-only-support-MSA-AAD-starting-June.html). nuget.org에 로그인하는 유일한 방법은 개인 MSA(Microsoft 계정) 또는 AAD(Azure Active Directory) 계정을 사용하는 것입니다. 그러나 연결된 MSA/AAD 계정에 액세스할 수 없는 경우 nuget.org 계정을 복구하려면 암호 로그인을 사용해야 합니다. 이 경우 다음 단계를 따릅니다.
- **요구 사항:** 암호를 복구해야 하는 계정과 연결된 이메일에 대한 액세스 권한이 있어야 합니다.
- [암호 찾기 페이지](https://www.nuget.org/account/ForgotPassword)로 이동합니다.
- 복구하려는 nuget.org 계정과 연결된 **이메일** 주소를 입력합니다.
- **보내기** 단추를 클릭합니다.
- 암호를 재설정하는 링크를 사용하여 지정된 이메일 주소 계정으로 이메일을 받을 수 있습니다. 이 링크를 클릭하고 새 암호를 설정합니다. 메일을 찾을 수 없으면 "스팸" 폴더를 확인합니다.
- 완료되면 NuGet에서 사용자 이름/암호로 로그인할 수 있습니다.
- 사용자 이름/암호로 로그인하려면 [nuget.org 로그인 페이지](https://www.nuget.org/users/account/LogOn)에서 **Nuget.org 계정을 통해 로그인** 링크를 사용합니다.

### <a name="which-microsoft-account-is-linked-to-my-nugetorg-account"></a>어떤 Microsoft 계정이 내 nuget.org 계정에 연결되어 있나요?

nuget.org 계정과 연결된 Microsoft 계정을 잊어버린 경우 아래 단계를 따르면 지원을 받을 수 있습니다.
1. [nuget.org 로그인 페이지](https://www.nuget.org/users/account/LogOn)로 이동하여 **로그인하는 데 도움이 필요하나요?** 링크를 클릭합니다.
1. 그러면 지원에 대한 팝업 대화 상자가 표시됩니다. nuget.org 계정에 대해 연결된 Microsoft 계정을 이해하려면 이 대화 상자의 단계를 따릅니다.

### <a name="how-to-change-the-microsoft-account-i-use-for-nugetorg-login"></a>nuget.org 로그인에 사용된 Microsoft 계정을 변경하려면 어떻게 하나요?
nuget.org 사용자에 대한 Microsoft 계정을 변경하려는 경우 다음 단계를 따릅니다. `account1@outlook.com` 이메일을 사용한 Microsoft 계정이 사용자 이름을 사용한 nuget.org 계정 `MyNuGetAccount`와 연결되어 있다고 가정합니다. `account2@outlook.com` 이메일을 사용하여 다른 Microsoft 계정으로 로그인을 변경하려면
1. **Microsoft로 로그인**을 클릭한 후 [로그인 페이지](https://www.nuget.org/users/account/LogOn)에서 **현재 연결된 Microsoft 계정** 즉, `account1@outlook.com`을 사용하여 로그인하세요.
1. 로그인하면 [계정 설정](https://www.nuget.org/account) 페이지로 이동합니다.
1. **로그인 계정**의 섹션을 확장합니다. **계정 변경** 단추를 클릭합니다.
1. 이제 Microsoft 로그인 페이지로 리디렉션됩니다. 연결을 `account2@outlook.com`으로 변경하려는 계정을 사용하여 로그인하세요. **참고**: 다른 Microsoft 계정으로 로그인할 수 있으려면 로그인 흐름 중에 **다른 계정으로 로그인 및 로그아웃**을 클릭해야 할 수 있습니다.
1. 아래와 같은 오류가 표시되는 경우 자세한 내용은 [Microsoft 계정이 다른 nuget.org 계정과 연결되어 있습니다](#microsoft-account-is-linked-with-another-nugetorg-account)를 참조하세요.
    >_'account2 <account2@outlook.com>'을 사용하여 Microsoft 계정을 업데이트하지 못했습니다. 다른 NuGet 계정에 이미 연결되어 있는 경우 이런 오류가 발생할 수 있습니다. 자세한 내용은 고객 지원팀에 문의하세요._

1. 두 번째 계정으로 로그인에 성공했으면 nuget.org 계정 설정 페이지로 다시 리디렉션되고 이제 로그인 계정으로 연결된 새 Microsoft 계정이 표시되어야 합니다. 앞으로는 nuget.org에 로그인할 때 이 계정을 사용해야 합니다.

### <a name="microsoft-account-is-linked-with-another-nugetorg-account"></a>Microsoft 계정이 다른 nuget.org 계정에 연결되어 있습니다.

Microsoft 로그인을 변경했는데 아래 오류가 나타난 경우:
> _'account2 <account2@outlook.com>'을 사용하여 Microsoft 계정을 업데이트하지 못했습니다. 다른 NuGet 계정에 이미 연결되어 있는 경우 이런 오류가 발생할 수 있습니다. 자세한 내용은 고객 지원팀에 문의하세요._

Microsoft 계정 로그인을 `MyNuGetAccount1` 사용자 이름을 사용한 nuget.org 사용자에 대한 `account1@outlook.com`에서 `account2@outlook.com` 이메일을 사용한 다른 Microsoft 계정으로 변경했다고 가정합니다. 그러면 위의 오류가 발생합니다.

**위의 오류가 의미하는 것은 무엇인가요?**

위의 예제에서 `MyNuGetAccount2` 사용자 이름을 사용한 다른 nuget.org 계정과 연결된 `<account2@outlook.com>` 이메일을 사용하는 Microsoft 계정으로 변경하려는 Microsoft 계정과 연결된 다른 nuget.org 계정이 있다는 의미입니다.

다른 nuget.org 계정에 연결된 Microsoft 계정과 연결된 로그인을 변경할 수 없습니다.

**다른 nuget.org 계정이 있다는 것을 잊은 경우 nuget.org 계정을 확인하려면 어떻게 하나요?**

[로그인 페이지](https://www.nuget.org/users/account/LogOn?returnUrl=%2F# "로그인 페이지")에서 두 번째 Microsoft 계정으로 로그인합니다. 그러면 현재 두 번째 Microsoft 계정과 연결된 nuget.org 계정에 로그인할 수 있습니다. 그런 다음, 업로드된 패키지를 확인하고 이 계정에서 계정 관리를 수행할 수 있습니다.

**이 두 번째 nuget.org 계정에 대해 신경쓰지 않고, 첫 번째 nuget.org 계정에 대한 내 로그인을 두 번째 Microsoft 계정으로 변경하려고 합니다. 어떻게 해야 하나요?**

두 번째 nuget.org 계정에 대해 신경쓰지 않으면서 `account2@outlook.com` 이메일과 연결된 Microsoft 계정을 다시 사용하려는 경우. 

nuget.org 계정을 삭제하여 Microsoft 계정 및 nuget.org 계정 간 연결을 해제할 수 있습니다.
1. 이 단계에 따라 `MyNuGetAccount2` 두 번째 nuget.org 계정의 [사용자를 삭제](#how-to-delete-my-nugetorg-account)합니다. 
1. 이 계정이 삭제되면 이 단계를 다시 시도하여 [Microsoft 계정 로그인을 변경](#how-to-change-the-microsoft-account-i-use-for-nugetorg-login)할 수 있습니다.

**잠깐. 이 두 번째 계정에도 관심이 있습니다. 이 계정은 손실되지만 첫 번째 계정에 대한 내 연결된 계정 로그인을 변경하지 않겠습니다.**

`account3@outlook.com` 이메일을 사용한 세 번째 Microsoft 계정을 만들어야/사용해야 합니다. 
1. 먼저 nuget.org에서 `account2@outlook.com`을 사용하는 두 번째 Microsoft 계정으로 로그인해야 합니다. 위의 단계에 따라 연결된 로그인을 변경하고 이 nuget.org 계정과 세 번째 Microsoft 계정을 연결합니다.
1. 완료되면 `account2@outlook.com` 이메일을 사용한 두 번째 Microsoft 계정은 자유롭게 `MyNuGetAccount1` 첫 번째 nuget.org 계정에 연결될 수 있습니다. 위의 동일한 단계에 따라 두 번째 Microsoft 계정에 대한 Microsoft 로그인을 변경합니다.

### <a name="signing-in-with-microsoft-account-shows-me-my-email-is-linked-to-another-microsoft-account"></a>Microsoft 계정으로 로그인하면 내 이메일이 다른 Microsoft 계정에 연결됐는지 표시됨
`account1@outlook.com` 이메일을 사용한 Microsoft 계정으로 로그인을 시도했는데 아래와 같은 오류가 발생한 경우:
> _'account1@outlook.com' 이메일을 사용한 계정이 다른 Microsoft 계정에 연결돼 있습니다._
>
> _연결된 Microsoft 계정을 업데이트하려는 경우 계정 설정 페이지에서 업데이트할 수 있습니다._

**위의 오류가 의미하는 것은 무엇인가요?**

nuget.org에서 계정을 만드는 경우 해당 계정과 연결된 통신 이메일 주소가 있습니다. 일반적으로 이 주소는 연결된 Microsoft 계정에 사용되는 이메일 주소와 동일합니다. 그러나 통신용으로 다른 이메일 주소를 지정하는 것은 선택할 수 있습니다. 따라서 기술적으로 다른 Microsoft 계정 즉, 통신 이메일 주소로 `account1@outlook.com`을 사용하여 nuget.org 계정에 연결하는 `account2@outlook.com`이 있을 수 있습니다.

위의 오류는 `account1@outlook.com` 통신 이메일 주소를 사용하는 nuget.org 계정이 이미 있지만 `account1@outlook.com`이 **아닌** 이메일을 사용하여 다른 Microsoft 계정과 연결되어 있다는 것을 의미합니다.

**이 nuget.org 계정에 어떤 Microsoft 계정이 연결되어 있는지 알려면 어떻게 하나요?**

`account1@outlook.com` 이메일 주소를 사용한 nuget.org 계정에 어떤 Microsoft 계정이 연결돼 있는지 파악하려면 [로그인 지원](#which-microsoft-account-is-linked-to-my-nugetorg-account) 흐름을 사용해야 합니다.

**해당 계정을 내 Microsoft 계정으로 재정의하려 함**

기존 nuget.org 계정을 사용하여 Microsoft 계정과 연결하려면 [Microsoft 로그인을 사용할 수 없는 경우 내 nuget.org 계정을 복구하려면 어떻게 하나요?](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account) 섹션의 단계를 따릅니다.

### <a name="unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account"></a>Microsoft 로그인을 사용할 수 없는 경우 내 nuget.org 계정을 복구하려면 어떻게 하나요?

[로그인 지원](#which-microsoft-account-is-linked-to-my-nugetorg-account)을 사용하려는데 nuget.org 계정과 연결된 Microsoft 계정에 액세스할 수 없는 경우 nuget.org 계정에 새 Microsoft 계정을 연결하려면 다음 단계를 따르세요.
1. **요구 사항**: 기존의 모든 nuget.org 계정과 연결되지 않은 Microsoft 계정에 액세스해야 합니다. 없는 경우 계정을 [만들](https://signup.live.com) 수 있습니다.
2. 암호 로그인이 있는 경우 [암호 로그인 복구 단계](#how-to-recover-nugetorg-password-login)를 따라 이 단계를 건너 뜁니다.
3. 사용자 이름/암호 로그인을 사용하여 [nuget.org에 로그인](https://www.nuget.org/users/account/LogOnNuGetAccount)합니다.
4. 로그인하면 아래와 같은 팝업 대화 상자가 표시됩니다. 이 대화 상자는 암호 중지 대화 상자입니다.
5. **참고**: 지정된 Microsoft 계정으로 로그인하라는 지침을 무시하세요. 이제 기타 모든 Microsoft 로그인에 nuget.org 계정을 연결할 수 있습니다.
6. 1단계에서 설명한 것처럼 **Microsoft로 로그인** 단추를 클릭하고 액세스 권한이 있는 Microsoft 계정으로 로그인합니다.
7. 이제 사용자 계정은 앞으로 nuget.org에 로그인하는 데 사용할 수 있는 새 Microsoft 계정에 연결됩니다.

    ![MSA 연결 대화 상자](media/link-msa-dialog.png)

### <a name="how-to-transform-my-nugetorg-account-to-an-organization"></a>내 nuget.org 계정을 조직 계정으로 변환하려면 어떻게 하나요?

사용자 계정을 조직 계정으로 변환하려는 경우 이 계정이 이미 Microsoft 계정 로그인과 연결되어 있으면 [nuget.org의 조직](https://docs.microsoft.com/en-us/nuget/reference/organizations-on-nuget-org)에 대한 설명서에 표시된 단계를 따릅니다.

그러나 nuget.org 계정이 Microsoft 계정과 연결되어 있지 않은 경우 이 계정을 조직 계정으로 변환하려면 다음 단계를 따르면 됩니다.
1. **요구 사항**: 조직 계정의 관리자로 사용할 nuget.org에서 처음 만든 개별 계정이 있어야 합니다. 없으면 [새 nuget.org 계정을 만듭니다](#how-to-create-a-nugetorg-account).
2. nuget.org 계정에 대한 암호 로그인이 없는 경우 해당 계정에 대한 [암호 로그인 복구 단계](#how-to-recover-nugetorg-password-login)를 따릅니다. 그러나 있는 경우 이 단계를 건너 뜁니다.
3. 사용자 이름/암호 로그인을 사용하여 [nuget.org에 로그인](https://www.nuget.org/users/account/LogOnNuGetAccount)합니다.
4. 로그인하면 아래와 같은 팝업 대화 상자가 표시됩니다. 이 대화 상자는 암호 중지 대화 상자입니다. 
    > [!Important]
    > 이 대화 상자를 무시하고 **Microsoft로 로그인** 단추를 클릭하지 **마세요**.

5. [https://www.nuget.org/account/transform](https://www.nuget.org/account/transform)으로 이동합니다. 그러면 Microsoft 계정에 연결하지 않고서 nuget.org 계정을 조직 계정으로 변환할 수 있습니다.
6. 1단계에서 만든 개인 nuget.org 계정/해당 계정에 관리 사용자 이름을 지정합니다.
7. 조직 계정으로 이 계정의 변환을 완료하려면 지침을 따릅니다.

    ![MSA 연결 대화 상자](media/link-msa-dialog.png)

### <a name="nugetorg-login-issues-for-aad-accounts-with-unmanaged-tenant"></a>관리되지 않는 테넌트로 AAD 계정에 대한 nuget.org 로그인 문제는?

이메일 계정 도메인(@yourdomain.com)으로 로그인 흐름 도중 아래와 같은 오류가 표시되는 경우 nuget.org 계정을 복구하려면 다음 단계를 참조하세요.

<p align="center">
    <img src="media/unmanaged-aad-tenant.png" />
</p>

**로그인 도중 이 관리되지 않는 상태란? 이런 일이 일어나는 이유는 무엇인가요?** 

사용자 계정이 이전에 개인 Microsoft 계정으로 등록된 것으로 보이고 문제 없이 작동했지만, 지금은 해당 계정이 Azure Active Directory에 "관리되지 않는" 테넌트로 등록된 것으로 보입니다(Microsoft 계정을 인증하는 데 사용하는 ID 서비스). 

@yourdomain.com 이메일 주소를 사용하는 조직의 누군가 또는 사용자가 AAD 통합 서비스에 등록했거나, [Azure Active Directory에 셀프 서비스 등록](https://docs.microsoft.com/en-us/azure/active-directory/users-groups-roles/directory-self-service-signup)하여 사용한 Microsoft 계정 도메인에 이러한 "관리되지 않는" 테넌트를 만든 경우 이런 일이 발생할 수 있습니다(사용자의 경우 @yourdomain.com). 

**내 계정을 복구하려면 어떻게 해야 하나요?**

현재 nuget.org에는 Azure Active directory에서 이러한 "관리되지 않는" 테넌트 계정을 사용하여 계정을 인증하는 방법이 없습니다. 지금은 이러한 계정을 인증하는 더 나은 방법을 찾아보고 있습니다.

Microsof 계정(@yourdomain.com)으로 nuget.org에 로그인하려는 경우 사용자(또는 사용자 회사의 관리자)는 "@yourdomain.com" 이메일 주소를 사용하여 사용자를 인증하려면 DNS 유효성 검사를 수행하여 AAD의 소유권을 주장해야 합니다. Azure Active Directory에서 설명된 [도메인 관리자 인수](https://docs.microsoft.com/en-us/azure/active-directory/users-groups-roles/domains-admin-takeover)에 대한 단계를 따릅니다. 이 작업이 완료되면 일반적인 로그인으로 작업이 시작되어야 합니다.

**이상 모든 작업을 수행하지 않으려는 경우 내 계정을 복구하는 다른 방법은?**

@yourdomain.com과 연결**되지 않은** 이메일을 사용하여 새 Microsoft 계정을 [만들](https://www.microsoft.com/en-us/account) 수 있습니다. [nuget.org 계정 복구](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account) 섹션에 설명된 단계를 따릅니다.

### <a name="how-do-i-change-my-nugetorg-account-username"></a>내 nuget.org 계정 사용자 이름을 변경하려면 어떻게 하나요?

변경할 수 없습니다. 정책상 사용자 이름 변경이 아직 허용되지 않습니다. 사용자 이름을 변경하는 유일한 방법은 원하는 사용자 이름으로 새 계정을 만드는 것입니다. 새 계정을 만들기 전에 기존 계정을 삭제하는 것이 좋습니다. 그렇지 않은 경우 등록된 Microsoft 계정을 다시 사용할 수 없습니다.
> [!Important]
> 사용자를 삭제하면 여전히 `username`을 **예약**할 수 있습니다. 다시 동일한 사용자 이름을 재사용할 수 없습니다. **여기에는 대/소문자 변경도 포함됩니다**. 예를 들어 `mycoolname` 사용자 이름으로 사용자를 만든 다음, `MyCoolName`(대/소문자 변경)으로 변경하려는 경우 사용자를 삭제한 후에는 변경할 수 없습니다.

올바른 사용자 이름으로 [새 계정을 등록](#how-to-create-a-new-nugetorg-account)하려면 [nuget.org 계정 삭제](#how-to-delete-my-nugetorg-account) 섹션에서 설명된 단계를 따릅니다.

### <a name="how-to-delete-my-nugetorg-account"></a>내 nuget.org 계정을 삭제하려면 어떻게 하나요?

계정을 삭제하려면 사용자가 유일한 소유자인 모든 패키지의 소유권을 양도하는 것이 좋습니다. 소유권을 양도하는 방법은 [패키지 소유자 관리](https://docs.microsoft.com/en-us/nuget/create-packages/publish-a-package#managing-package-owners-on-nugetorg)를 참조할 수 있습니다. 그러면 요청을 신속하게 처리하는 데도 도움이 됩니다.

> [!Important]
> 사용자를 삭제하면 다음과 같이 됩니다.
>  1. 연결된 API 키를 취소합니다. 
>  2. 모든 자식 패키지의 소유자로서 계정을 제거합니다.
>  3. 이 계정과 기존의 모든 ID 접두사 예약을 분리합니다.
>  4. 모든 조직의 구성원으로서 계정을 제거합니다.
>  5. 사용자 이름이 예약되면 누구도 사용 권한 없이는 이를 다시 사용할 수 없습니다.

계정 삭제를 진행하려면 다음 단계를 따릅니다.
1. 삭제하려는 계정으로 [nuget.org에 로그인](https://www.nuget.org/users/account/LogOn)합니다.
2. 이 URL [https://www.nuget.org/account/delete](https://www.nuget.org/account/delete)를 클릭하고 계정 삭제 요청을 제출하는 단계를 따릅니다.

그러면 본사의 고객 지원팀은 이 요청을 처리하고 계정 삭제를 수행합니다.
