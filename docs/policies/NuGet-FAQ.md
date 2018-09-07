---
title: NuGet 질문과 대답
description: 명령줄 및 Visual Studio에서 NuGet을 사용하고 NuGet 갤러리에서 작업하는 경우와 관련된 일반적인 질문과 대답입니다.
author: karann-msft
ms.author: karann
ms.date: 01/11/2018
ms.topic: conceptual
ms.openlocfilehash: 8c63abc9971623e0732ae8d973fafcd04c5d9f48
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548806"
---
# <a name="nuget-frequently-asked-questions"></a>NuGet 질문과 대답

**NuGet을 실행하는 데 필요한 것은 무엇인가요?**

UI 및 명령줄 도구에 관한 모든 정보는 [설치 가이드](../install-nuget-client-tools.md)에서 사용할 수 있습니다.

**NuGet은 Mono를 지원하나요?**

`nuget.exe` 명령줄 도구는 Mono 3.2 이상에서 빌드하고 실행되며, Mono에서 패키지를 만들 수 있습니다.

`nuget.exe`는 Windows에서 완벽하게 작동하지만, Linux 및 OS X에서는 알려진 문제가 있습니다. GitHub의 [Mono 문제](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono)를 참조하세요.

[그래픽 클라이언트](https://github.com/mrward/monodevelop-nuget-addin)는 MonoDevelop용 추가 기능으로 사용할 수 있습니다.

**패키지에 포함된 내용과 응용 프로그램에 안정적이고 유용한 지 여부를 확인하려면 어떻게 해야 할까요?**

패키지 학습에 대한 기본 소스는 nuget.org(또는 다른 개인 피드)의 목록 페이지입니다. nuget.org의 각 패키지 페이지에는 패키지에 대한 설명, 해당 버전 기록 및 사용 통계가 포함되어 있습니다. 또한 패키지 페이지의 **정보** 섹션에는 프로젝트의 웹 사이트에 대한 링크가 포함되어 있으며, 여기서 패키지를 사용하는 방법을 알아보는 데 도움이 되는 많은 예제와 기타 문서를 찾을 수 있습니다.

자세한 내용은 [패키지 찾기 및 선택](../consume-packages/finding-and-choosing-packages.md)을 참조하세요.

## <a name="nuget-in-visual-studio"></a>Visual Studio의 NuGet

**다른 Visual Studio 제품에서는 NuGet을 어떻게 지원하나요?**

- Windows에서 Visual Studio는 [패키지 관리자 UI](../tools/package-manager-ui.md)와 [패키지 관리자 콘솔](../tools/package-manager-console.md)을 지원합니다.
- Mac용 Visual Studio에는 [프로젝트에 NuGet 패키지 포함](/visualstudio/mac/nuget-walkthrough)에서 설명한 대로 NuGet 기능이 기본적으로 제공됩니다.
- Visual Studio Code(모든 플랫폼)에는 직접적인 NuGet 통합이 없습니다. [NuGet CLI](../tools/nuget-exe-cli-reference.md) 또는 [dotnet CLI](../tools/dotnet-commands.md)를 사용하세요.
- Visual Studio Team Services는 [NuGet 패키지를 복원하는 빌드 단계](/vsts/build-release/tasks/package/nuget)를 제공합니다. 또한 [Team Services에서 전용 NuGet 패키지 피드를 호스팅](https://www.visualstudio.com/docs/package/nuget/publish)할 수도 있습니다.

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

**$DTE 변수를 DTE2 형식으로 캐스팅하려고 했지만 ""EnvDTE.DTEClass" 형식의 "EnvDTE.DTEClass" 값을 "EnvDTE80.DTE2" 형식으로 변환할 수 없습니다."라는 오류가 발생합니다. 무엇이 문제인가요?**

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

## <a name="managing-packages-on-nugetorg"></a>nuget.org의 패키지 관리

**패키지 메타데이터를 업로드한 후에 편집할 수 있나요?**

NuGet은 모든 패키지에 서명을 권장합니다. 패키지 서명의 디자인 원칙은 nuspec을 포함한 서명된 패키지 콘텐츠를 변경할 수 없다는 것입니다. 패키지 메타데이터를 편집하면 nuspec이 변경되고 기존 서명이 무효화됩니다. 패키지를 만든 후에 패키지 메타데이터를 편집할 필요가 없도록 기존 워크플로를 수정하는 것이 좋습니다.

패키지에 대해 나열된 종속성은 패키지 자체에서 자동으로 생성되며 편집할 수 없습니다.

또한 [staging.nuget.org](http://staging.nuget.org)에 패키지를 업로드하는 것은 공용 갤러리에서 패키지를 사용하지 않고도 패키지를 테스트하고 유효성을 검사할 수 있는 좋은 방법입니다.

**나중에 게시되는 패키지의 이름을 예약할 수 있나요?**

예. 계정에 대한 패키지 ID 접두사를 요청하여 [nuget.org](https://www.nuget.org/)에서 패키지 ID를 예약할 수 있습니다. 패키지 ID 접두사를 요청하려면 [설명서](https://docs.microsoft.com/nuget/reference/id-prefix-reservation)의 지침을 따르세요.

**패키지 소유권을 주장하려면 어떻게 할까요?**

[nuget.org에서 패키지 소유자 관리](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg)를 참조하세요.

**소프트웨어 라이선스를 위반하는 패키지 소유자를 처리하려면 어떻게 할까요?**

NuGet 커뮤니티에서 패키지 소유자와 다른 소프트웨어 소유자 간에 발생할 수 있는 분쟁을 해결하기 위해 함께 노력하는 것이 좋습니다. nuget.org 관리자에게 중재를 요청하기 전에 따라야 할 [분쟁 해결 절차](../policies/dispute-resolution.md)가 마련되어 있습니다.

**내 테스트 패키지를 nuget.org에 업로드하는 것이 좋을까요?**

테스트를 위해 [staging.nuget.org](http://staging.nuget.org) 또는 대체 공용 NuGet 서버(예: [myget.org](https://myget.org) 또는 [Visual Studio Team Services](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/))를 사용할 수 있습니다.

staging.nuget.org에 업로드된 패키지는 유지되지 않을 수 있습니다. [Goodbye preview](http://blog.nuget.org/20130419/goodbye-preview.html)를 참조하세요.

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
- 운영 체제 버전
- 컴퓨터 구성(CPU, 네트워크, 하드 드라이브)
- 머신이 프록시 또는 방화벽을 사용하는지 여부
- 컴퓨터에 설치된 .NET 버전
- 사용 중인 플랫폼 간 도구(예: .NET CLI 또는 DNU)의 버전

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

**nuget.org에 대한 API 엔드포인트는 무엇인가요?**

V3: `https://api.nuget.org/v3/index.json` V2: `https://www.nuget.org/api/v2/`(V2 API는 더 이상 사용되지 않으며 NuGet 4 이상에서 작동하지 않습니다.)
