---
title: NuGet 정의 및 기능
description: NuGet의 정의와 기능에 대해 포괄적으로 소개합니다.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/10/2018
ms.topic: overview
ms.openlocfilehash: 7237db8f3be3d9a1d46b9e6be41bff5c06593a20
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="an-introduction-to-nuget"></a>NuGet 소개

모든 최신 개발 플랫폼에 필수적인 도구는 개발자가 유용한 코드를 작성, 공유 및 사용할 수 있는 메커니즘입니다. 대부분 이러한 코드는 이러한 패키지를 사용하는 프로젝트에 필요한 다른 내용과 함께 컴파일된 코드를 포함하는(DLL로) “패키지”로 제공됩니다.

.NET(.NET Core 포함)의 경우 코드를 공유하는 Microsoft 지원 메커니즘은 **NuGet**이며, 이는 .NET용 패키지를 만들고 호스트하고 사용하는 방법을 정의하고 각 역할에 대한 도구를 제공합니다.

간단히 말해, NuGet 패키지는 컴파일된 코드(DLL), 해당 코드와 관련된 다른 파일 및 패키지의 버전 번호와 같은 정보를 포함한 설명적 매니페스트가 포함된 `.nupkg` 확장명의 단일 ZIP 파일입니다. 공유할 코드를 가진 개발자는 패키지 파일을 만들어 공용 또는 전용 호스트에 게시합니다. 패키지 소비자는 적합한 호스트에서 이러한 패키지를 받고, 프로젝트에 추가한 다음, 프로젝트 코드에서 패키지 기능을 호출합니다. 그런 다음 NuGet 자체에서 모든 중간 세부 정보를 처리합니다.

NuGet은 공용 nuget.org 호스트와 함께 전용 호스트를 지원하기 때문에 NuGet 패키지를 사용하여 조직 또는 작업 그룹에 독점적인 코드를 공유할 수 있습니다. 고유한 코드를 고유한 프로젝트에서만 사용하도록 팩터링하는 편리한 방법으로 NuGet 패키지를 사용할 수도 있습니다. 간단히 말하면 NuGet 패키지는 공유 가능한 코드 단위이지만, 특정 공유 방법을 필요로 하거나 의미하지 않습니다.

## <a name="the-flow-of-packages-between-creators-hosts-and-consumers"></a>작성자, 호스트 및 소비자 간의 패키지 흐름

공용 호스트로서의 역할에서 NuGet 자체는 [nuget.org](https://www.nuget.org)에 100,000개가 넘는 고유한 패키지의 중앙 리포지토리를 유지 관리합니다. 이러한 패키지는 매일 수백만 명의 .NET/.NET Core 개발자가 사용합니다. 또한 NuGet을 사용하면 클라우드(예: Visual Studio Team Services), 사설 네트워크 또는 로컬 파일 시스템에서도 패키지를 전용으로 호스트할 수 있습니다. 이렇게 하면 호스트에 액세스할 수 있는 개발자만 해당 패키지를 사용할 수 있으므로 특정 소비자 그룹이 패키지를 사용할 수 있도록 설정하는 기능이 제공됩니다. 옵션은 [자체 NuGet 피드 호스팅](hosting-packages/overview.md)에서 설명하고 있습니다. 구성 옵션을 통해 주어진 컴퓨터에서 액세스할 수 있는 호스트를 정확히 제어할 수 있으므로 nuget.org 같은 공용 리포지토리가 아닌 특정 소스에서 패키지를 가져오게 됩니다.

특성이 무엇이든 간에 호스트는 패키지 *작성자*와 패키지 *소비자* 사이의 연결 지점 역할을 합니다. 작성자는 유용한 NuGet 패키지를 빌드하고 호스트에 게시합니다. 그런 다음 소비자는 액세스할 수 있는 호스트에서 유용하고 호환 가능한 패키지를 검색하고 해당 패키지를 다운로드하여 프로젝트에 포함합니다. 프로젝트에 설치되면 패키지의 API는 프로젝트 코드의 나머지 부분에서 사용할 수 있습니다.

![패키지 작성자, 패키지 호스트 및 패키지 소비자 간의 관계](media/nuget-roles.png)

## <a name="package-targeting-compatibility"></a>패키지 대상 지정 호환성

“호환” 패키지는 사용 프로젝트의 대상 프레임워크와 호환되는 하나 이상의 대상 .NET 프레임워크용으로 빌드된 어셈블리가 포함되어 있음을 의미합니다. 개발자는 UWP 컨트롤을 사용하는 것처럼 하나의 프레임워크에 고유한 패키지를 만들거나 광범위한 대상을 지원할 수 있습니다. 패키지 호환성을 최대화하기 위해 개발자는 모든 .NET 및 /.NET Core 프로젝트에서 사용할 수 있는 [.NET Standard](/dotnet/standard/net-standard)를 대상으로 지정합니다. 단일 패키지(일반적으로 단일 어셈블리 포함)는 모든 소비 프로젝트에서 작동하므로 이 방법은 작성자 및 소비자에게 모두 가장 효율적인 방법입니다.

한편, .NET Standard 외부의 API가 필요한 패키지 개발자는 지원하려는 대상 프레임워크의 개별 어셈블리를 만들고 동일한 패키지에 해당하는 모든 어셈블리를 포함합니다(“멀티 타기팅”이라고 함). 소비자가 해당 패키지를 설치하면 NuGet에서 프로젝트에 필요한 어셈블리만 추출합니다. 이렇게 하면 최종 응용 프로그램 및/또는 해당 프로젝트에서 생성한 어셈블리의 패키지 공간이 최소화됩니다. 멀티 타기팅 패키지는 물론 작성자가 유지 관리하기가 더 어렵습니다.

> [!Note]
> 다양한 PCL(이식 가능한 클래스 라이브러리) 대상을 사용하는 이전 방법 대신 .NET Standard를 대상으로 지정하는 방법이 사용됩니다. 따라서 이 문서에서는 .NET Standard에 대한 패키지를 만드는 데 중점을 둡니다.

## <a name="nuget-tools"></a>NuGet 도구

NuGet은 호스팅 지원 외에도 작성자와 소비자 모두가 사용하는 다양한 도구를 제공합니다. 특정 도구를 가져오는 방법은 [NuGet 클라이언트 도구 설치](install-nuget-client-tools.md)를 참조하세요.

| 도구 | 플랫폼 | 적용 가능한 시나리오 | 설명 |
| --- | --- | --- | --- |
| [nuget.exe CLI](tools/nuget-exe-cli-reference.md) | 모두 | 만들기, 사용 | 모든 NuGet 기능을 제공합니다. 일부 명령은 패키지 작성자에게만 적용되고, 일부는 소비자에게만 적용되고, 다른 일부는 둘 다에 적용됩니다. 예를 들어 패키지 작성자는 `nuget pack` 명령을 사용하여 다양한 어셈블리 및 관련 파일에서 패키지를 만들고, 패키지 소비자는 `nuget install`을 사용하여 프로젝트 폴더에 패키지를 포함하고, 모든 사용자는 `nuget config`를 사용하여 NuGet 구성 변수를 설정합니다. 플랫폼 제약 없는 도구인 NuGet CLI는 Visual Studio 프로젝트와 상호 작용하지 않습니다. |
| [dotnet CLI](tools/dotnet-Commands.md) | 모두 | 만들기, 사용 | .NET Core 도구 체인 내에서 특정 NuGet CLI 기능을 직접 제공합니다. NuGet CLI와 같이 dotnet CLI는 Visual Studio 프로젝트와 상호 작용하지 않습니다. |
| [패키지 관리자 콘솔](tools/package-manager-console.md) | Windows의 Visual Studio | 사용 | Visual Studio 프로젝트에서 패키지를 설치하고 관리하기 위한 [PowerShell 명령](tools/Powershell-Reference.md)을 제공합니다. |
| [패키지 관리자 UI](tools/package-manager-ui.md) | Windows의 Visual Studio | 사용 | Visual Studio 프로젝트에서 패키지를 설치하고 관리하기 위한 사용하기 쉬운 UI를 제공합니다. |
| [NuGet UI 관리](/visualstudio/mac/nuget-walkthrough) | Visual Studio for Mac | 사용 | Mac용 Visual Studio 프로젝트에서 패키지를 설치하고 관리하기 위한 사용하기 쉬운 UI를 제공합니다. |
| [MSBuild](reference/msbuild-targets.md) | Windows | 만들기, 사용 | MSBuild 도구 체인을 통해 프로젝트에서 사용되는 패키지를 직접 만들고 복원할 수 있는 기능을 제공합니다. |

여기서 볼 수 있듯이 사용하는 NuGet 도구는 패키지를 만드는지, 사용하는지 또는 게시하는지 여부뿐 아니라 작업 중인 플랫폼에 따라 크게 달라집니다. 또한 패키지 작성자는 일반적으로 다른 NuGet 패키지에 있는 기능을 기반으로 하므로 소비자이기도 합니다. 물론 이러한 패키지는 다른 패키지에도 종속될 수 있습니다.

자세한 내용은 먼저 [패키지 만들기 워크플로](create-packages/Overview-and-Workflow.md) 및 [패키지 사용 워크플로](consume-packages/Overview-and-Workflow.md) 문서를 참조하세요.

## <a name="managing-dependencies"></a>종속성 관리

다른 항목의 작업을 쉽게 빌드하는 기능은 패키지 관리 시스템의 가장 강력한 기능 중 하나입니다. 따라서 NuGet에서 수행하는 작업 대부분은 프로젝트를 대신하여 종속성 트리 또는 “그래프”를 관리하는 것입니다. 간단히 말해, 프로젝트에서 직접 사용하는 패키지에만 집중하면 됩니다. 이러한 패키지 자체에서 다른 패키지(이 패키지도 다른 패키지를 사용할 수 있음)를 사용하는 경우 NuGet은 모든 하위 수준 종속성을 처리합니다.

다음 이미지에서는 다섯 개의 패키지에 종속된 프로젝트를 보여 주며, 이러한 다섯 개의 패키지도 여러 개의 다른 패키지에 종속됩니다.

![.NET 프로젝트에 대한 NuGet 종속성 그래프 예제](media/dependency-graph.png)

일부 패키지는 종속성 그래프에 여러 번 표시됩니다. 예를 들어 B 패키지의 서로 다른 세 가지 소비자가 있으며, 각 소비자는 해당 패키지에 대해 다른 버전을 지정할 수도 있습니다(표시되지 않음). 이 경우는 특히 널리 사용되는 패키지에 대해 일반적입니다. 다행스럽게도 NuGet에서 모든 소비자를 충족하는 B 패키지의 정확한 버전을 확인하기 위한 모든 작업을 수행합니다. 그런 다음 NuGet에서 종속성 그래프의 세부 수준에 관계없이 다른 모든 패키지에 대해 동일한 작업을 수행합니다.

NuGet에서 이 서비스를 수행하는 방법에 대한 자세한 내용은 [종속성 확인](consume-packages/dependency-resolution.md)을 참조하세요.

## <a name="tracking-references-and-restoring-packages"></a>참조 추적 및 패키지 복원

프로젝트는 개발자 컴퓨터, 소스 제어 리포지토리, 빌드 서버 등 간에 쉽게 이동할 수 있기 때문에 프로젝트에 직접 바인딩된 NuGet 패키지의 이진 어셈블리를 유지하는 것은 매우 실용적이지 않습니다. 이렇게 하면 프로젝트의 각 복사본이 불필요하게 너무 확장됩니다(이에 따라 소스 제어 리포지토리의 공간이 낭비될 수 있음). 또한 프로젝트의 모든 복사본에서 적용해야 하기 때문에 패키지 이진 파일을 최신 버전으로 업데이트하는 것도 매우 어려워집니다.

대신 NuGet은 프로젝트가 종속된 패키지(최상위 및 하위 수준 종속성 모두 포함)의 간단한 참조 목록을 유지 관리합니다. 즉, 어떤 호스트에서 프로젝트로 패키지를 설치할 때마다 NuGet은 패키지 식별자와 버전 번호를 참조 목록에 기록합니다. (물론 패키지를 제거하면 해당 패키지가 목록에서 제거됩니다.) 그런 다음 NuGet은 [패키지 복원](consume-packages/package-restore.md)에서 설명한 대로 요청 시 참조된 모든 패키지를 복원할 수 있는 방법을 제공합니다.

![NuGet 참조 목록은 패키지 설치 시 만들어지며, 다른 위치에서 패키지를 복원하는 데 사용할 수 있습니다.](media/nuget-restore.png)

NuGet은 나중에 언제든지 참조 목록만 사용하여 공용 및/또는 사설 호스트에서 해당 패키지 모두를 다시 설치, 즉 *복원*할 수 있습니다.&mdash;&mdash; 프로젝트를 소스 제어에 커밋하거나 다른 방식으로 공유하는 경우, 참조 목록만 포함하고 패키지 이진 파일은 제외합니다([패키지 및 소스 제어](consume-packages/packages-and-source-control.md) 참조).

자동화된 배포 시스템의 일부로 프로젝트의 복사본을 얻는 빌드 서버와 같이 프로젝트를 받는 컴퓨터는 필요할 때마다 NuGet에서 종속성을 복원하도록 요청하기만 하면 됩니다. Visual Studio Team Services와 같은 빌드 시스템은 이와 같은 정확한 목적을 위해 "NuGet restore" 단계를 제공합니다. 마찬가지로 개발자가 프로젝트의 복사본을 얻는 경우(예: 리포지토리 복제 시) `nuget restore`(NuGet CLI), `dotnet restore`(dotnet CLI) 또는 `Install-Package`(패키지 관리자 콘솔) 같은 명령을 호출하여 모든 필요한 패키지를 얻습니다. Visual Studio 자체로서는 [패키지 복원](consume-packages/package-restore.md)에 설명된 대로 자동 복원을 사용하도록 설정한 경우 프로젝트를 빌드할 때 패키지를 자동으로 복원합니다.

그런 다음 개발자가 염려하는 NuGet의 주 역할은 분명히 프로젝트를 대신하여 참조 목록을 유지 관리하고, 참조된 패키지를 효율적으로 복원(및 업데이트)할 수 있는 방법을 제공하는 것입니다. 이 목록은 두 가지 *패키지 관리 형식* 중 하나로 유지 관리됩니다(호출 시).

- [`packages.config`](reference/packages-config.md): *(NuGet 1.0 이상)* 설치된 다른 패키지의 종속성을 포함하여 프로젝트의 모든 종속성에 대한 단순 목록을 유지 관리하는 XML 파일입니다. 설치되거나 복원된 패키지는 `packages` 폴더에 저장됩니다.

- [PackageReference](consume-packages/package-references-in-project-files.md)(또는 “프로젝트 파일의 패키지 참조”) | *(NuGet 4.0+)* 프로젝트 파일 내에서 프로젝트의 최상위 종속성에 대한 목록을 직접 유지 관리하므로 별도의 파일이 필요하지 않습니다. 연결된 파일 `obj/project.assets.json`이 동적으로 생성되어 프로젝트가 모든 하위 수준 종속성과 함께 사용하는 패키지의 전체 종속성 그래프를 관리합니다. PackageReference는 .NET Core 프로젝트에서 항상 사용됩니다.

특정 프로젝트에서 사용되는 패키지 관리 형식은 프로젝트 형식과 NuGet 및/또는 Visual Studio의 사용 가능한 버전에 따라 다릅니다. 사용되는 형식을 확인하려면 첫 번째 패키지를 설치한 후 프로젝트 루트에서 `packages.config`를 찾기만 하면 됩니다. 해당 파일이 없으면 프로젝트 파일에서 직접 \<PackageReference\> 요소를 찾습니다.

선택할 수 있는 경우 PackageReference를 사용하는 것이 좋습니다. `packages.config`은 레거시용으로 유지되며 더 이상 실제로 개발되지 않습니다.

> [!Tip]
> `nuget install`과 같은 다양한 `nuget.exe` CLI 명령은 패키지를 참조 목록에 자동으로 추가하지 않습니다. 이 목록은 Visual Studio 패키지 관리자(UI 또는 콘솔) 및 `dotnet.exe` CLI를 사용하여 패키지를 설치할 때 업데이트됩니다.

## <a name="what-else-does-nuget-do"></a>기타 NuGet 작업

지금까지는 NuGet의 다음 특징을 알아보았습니다.

- NuGet은 전용 호스팅을 지원하는 중앙 nuget.org 리포지토리를 제공합니다.
- NuGet에서는 개발자가 패키지를 만들고, 게시하고, 사용하는 데 필요한 도구를 제공합니다.
- NuGet이 프로젝트에서 사용되는 패키지의 참조 목록 및 해당 목록에서 해당 패키지를 복원하고 업데이트할 수 있는 기능을 유지 관리한다는 것이 가장 중요합니다.

이러한 프로세스를 효율적으로 수행하기 위해 NuGet에서 몇 가지 백그라운드 최적화를 수행합니다. 특히, NuGet은 패키지 캐시와 전역 패키지 폴더를 관리하여 설치 및 다시 설치의 바로 가기를 지정합니다. 캐시는 컴퓨터에 이미 설치된 패키지 다운로드를 방지합니다. 전역 패키지 폴더를 사용하면 여러 프로젝트가 동일한 설치된 패키지를 공유할 수 있으므로 컴퓨터에서 NuGet의 전체 설치 공간이 감소합니다. 캐시 및 전역 패키지 폴더는 빌드 서버에서처럼 많은 수의 패키지를 자주 복원하는 경우에도 매우 유용합니다. 이러한 메커니즘에 대한 자세한 내용은 [Managing the global packages and cache folders](consume-packages/managing-the-global-packages-and-cache-folders.md)(전역 패키지 및 캐시 폴더 관리)를 참조하세요.

개별 프로젝트 내에서 NuGet은 전체 종속성 그래프를 관리하며, 여기에는 동일한 패키지의 서로 다른 버전에 대한 여러 참조를 확인하는 작업이 다시 포함됩니다. 프로젝트에서 자체적으로 종속성이 동일한 하나 이상의 패키지에 대한 종속성을 사용하는 것이 매우 일반적입니다. nuget.org에서 가장 유용한 유틸리티 패키지 중 일부는 다른 많은 패키지에서 사용됩니다. 10개의 전체 종속성 그래프에서 동일한 패키지의 서로 다른 버전에 대해 10개의 다른 참조를 쉽게 갖출 수 있습니다. 해당 패키지의 여러 버전을 응용 프로그램 자체에 가져오지 않기 위해 NuGet은 모든 소비자가 사용할 수 있는 단일 버전을 정렬합니다. (자세한 내용은 [종속성 확인](consume-packages/dependency-resolution.md)을 참조하세요.)

그 외에도 NuGet은 패키지를 구성하는 방법([지역화](create-packages/creating-localized-packages.md) 및 [디버그 기호](create-packages/symbol-packages.md) 포함) 및 참조하는 방법([버전 범위](reference/package-versioning.md#version-ranges-and-wildcards) 및 [시험판 버전](create-packages/prerelease-packages.md) 포함)과 관련된 모든 사양을 유지 관리합니다. 또한 NuGet은 서비스에서 프로그래밍 방식으로 작동하는 다양한 API를 제공하며 Visual Studio 확장 및 프로젝트 템플릿을 작성하는 개발자를 위한 지원을 제공합니다.

잠시 시간을 내어 이 설명서의 목차를 살펴보면 NuGet의 시작까지 거슬러 올라가는 릴리스 정보와 함께 이러한 모든 기능이 목차에 나와 있습니다.

## <a name="comments-contributions-and-issues"></a>의견, 참여 및 문제

마지막으로 이 설명서에 대한 의견과 참여를 매우 환영합니다. &mdash;아무 페이지 위쪽에서 **피드백** 및 **편집** 명령을 선택하거나 GitHub의 [문서 리포지토리](https://github.com/NuGet/docs.microsoft.com-nuget/) 및 [문서 문제 목록](https://github.com/NuGet/docs.microsoft.com-nuget/issues)을 방문하세요.

또한 [다양한 GitHub 리포지토리](https://github.com/NuGet/Home)를 통해 NuGet에 직접 참여하는 것도 환영합니다. NuGet 문제는 [https://github.com/NuGet/home/issues](https://github.com/NuGet/home/issues)에서 확인할 수 있습니다.

여러분의 NuGet 경험을 즐겨보세요!
