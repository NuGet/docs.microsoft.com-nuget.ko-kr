---
title: "NuGet 정의 및 기능 | Microsoft 문서"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/26/2017
ms.topic: hero-article
ms.prod: nuget
ms.technology: 
ms.assetid: c3faf278-4cbf-4733-96f6-9ee9f7203af9
description: "NuGet의 정의와 기능에 대해 포괄적으로 소개합니다."
keywords: "NuGet 패키지 관리자, 사용, 패키지 만들기, 패키지 호스팅"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 29dcedf33a54e249fe0b6acf588e4aafde28304f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="an-introduction-to-nuget"></a>NuGet 소개

모든 최신 개발 플랫폼에 필수적인 도구는 개발자가 유용한 코드 라이브러리를 작성, 공유 및 사용할 수 있는 메커니즘입니다. 이러한 라이브러리는 컴파일된 코드(DLL) 및 해당 라이브러리를 사용하는 프로젝트에 필요할 수 있는 다른 콘텐츠를 포함할 수 있기 때문에 일반적으로 "패키지"라고 합니다.

.NET의 경우 코드를 공유하는 메커니즘은 **NuGet**이며, 이는 .NET용 패키지를 만들고 호스팅하고 사용하는 방법을 정의하고 각 역할에 대한 도구를 제공합니다. 

간단히 말해, NuGet 패키지는 컴파일된 코드(DLL), 해당 코드와 관련된 다른 파일 및 패키지의 버전 번호와 같은 정보를 포함한 설명적 매니페스트가 포함된 `.nupkg` 확장명의 단일 ZIP 파일입니다. 라이브러리 개발자는 패키지 파일을 만들어 호스트에 게시합니다. 패키지 소비자는 이러한 패키지를 받고, 프로젝트에 추가한 다음, 프로젝트 코드에서 해당 라이브러리의 기능을 호출합니다. 그런 다음 NuGet 자체에서 모든 중간 세부 정보를 처리합니다.

## <a name="the-flow-of-packages-between-creators-hosts-and-consumers"></a>작성자, 호스트 및 소비자 간의 패키지 흐름

호스트로서의 역할에서 NuGet 자체는 [nuget.org](https://www.nuget.org)에 60,000개가 넘는 고유하고 공개적으로 사용할 수 있는 패키지의 중앙 리포지토리를 유지 관리합니다. 이러한 패키지는 매일 수백만 명의 .NET 개발자가 사용합니다. 또한 NuGet을 사용하면 클라우드, 사설 네트워크 또는 로컬 파일 시스템에서도 패키지를 전용으로 호스팅할 수 있습니다. 이렇게 함으로써 해당 패키지는 특정 조직 또는 고객 그룹 내의 개발자만 사용할 수 있습니다. 옵션은 [자체 NuGet 피드 호스팅](Hosting-Packages/Overview.md)에서 설명하고 있습니다.

특성이 무엇이든 간에 호스트는 패키지 *작성자*와 패키지 *소비자* 사이의 연결 지점 역할을 합니다. 작성자는 유용한 NuGet 패키지를 빌드하고 호스트에 게시합니다. 그런 다음 소비자는 액세스할 수 있는 호스트에서 유용하고 호환 가능한 패키지를 검색하고 해당 패키지를 다운로드하여 프로젝트에 포함합니다. 프로젝트에 설치되면 패키지의 API는 프로젝트 코드의 나머지 부분에서 사용할 수 있습니다.

![패키지 작성자, 패키지 호스트 및 패키지 소비자 간의 관계](media/nuget-roles.png)

이 경우 "호환" 패키지는 사용 프로젝트의 대상 프레임워크와 호환되는 하나 이상의 대상 .NET 프레임워크용으로 빌드된 어셈블리가 포함되어 있음을 의미합니다. 패키지가 광범위하게 호환되도록 하기 위해 작성자는 다양한 대상 프레임워크에 대해 별도의 어셈블리를 컴파일하고 동일한 패키지에 모두 포함합니다. 소비자가 해당 패키지를 설치하면 NuGet에서 프로젝트에 필요한 어셈블리만 추출합니다. 이렇게 하면 최종 응용 프로그램 및/또는 해당 프로젝트에서 생성한 어셈블리의 패키지 공간이 최소화됩니다.

## <a name="nuget-tools"></a>NuGet 도구

NuGet은 호스팅 지원 외에도 작성자와 소비자 모두가 사용하는 다양한 도구를 제공합니다.

| 도구 | 플랫폼 | 적용 가능한 시나리오 | 설명 |
| --- | --- | --- | --- |
| [nuget.exe CLI](Tools/nuget-exe-CLI-Reference.md) | 모두 | 만들기, 사용 | 모든 NuGet 기능을 제공합니다. 일부 명령은 패키지 작성자에게만 적용되고, 일부는 소비자에게만 적용되고, 다른 일부는 둘 다에 적용됩니다. 예를 들어 패키지 작성자는 `nuget pack` 명령을 사용하여 다양한 어셈블리 및 관련 파일에서 패키지를 만들고, 패키지 소비자는 `nuget install`을 사용하여 프로젝트에 패키지를 포함하고, 모든 사용자는 `nuget config`를 사용하여 NuGet 구성 변수를 설정합니다.  |
| [패키지 관리자 UI](Tools/Package-Manager-UI.md) | Windows의 Visual Studio | 사용 | .NET 프로젝트에서 패키지를 설치하고 관리하는 데 사용하기 쉬운 UI를 제공합니다. | 
| [NuGet UI 관리](https://docs.microsoft.com/visualstudio/mac/nuget-walkthrough) | Visual Studio for Mac | 사용 | .NET 프로젝트에서 패키지를 설치하고 관리하는 데 사용하기 쉬운 UI를 제공합니다. |
| [패키지 관리자 콘솔](Tools/Package-Manager-Console.md) | Windows의 Visual Studio | 사용 | .NET 프로젝트에서 패키지를 설치하고 관리하기 위한 [PowerShell 명령](Tools/Powershell-Reference.md)을 제공합니다. | 
| [dotnet CLI](Tools/dotnet-Commands.md) | 모두 | 만들기, 사용 | .NET Core 도구 체인 내에서 특정 NuGet CLI 기능을 직접 제공합니다. |
| [MSBuild](Schema/msbuild-targets.md) | Windows | 만들기, 사용 | MSBuild 도구 체인을 통해 프로젝트에서 사용되는 패키지를 직접 만들고 복원할 수 있는 기능을 제공합니다. |

여기서 볼 수 있듯이 NuGet으로 작업하는 도구는 패키지를 만들고 게시하는지, 패키지를 사용하는지 및 작업 중인 플랫폼에 따라 크게 달라집니다. 더 구체적인 세부 정보는 [패키지 만들기 워크플로](Create-Packages/Overview-and-Workflow.md) 및 [패키지 사용 워크플로](Consume-Packages/Overview-and-Workflow.md) 항목과 해당 섹션의 다른 항목에서 찾을 수 있습니다. 

또한 패키지 작성자는 일반적으로 다른 NuGet 패키지에 있는 기능을 기반으로 하므로 소비자이기도 합니다. 물론 이러한 패키지는 다른 패키지에도 종속될 수 있습니다.

## <a name="managing-dependencies"></a>종속성 관리

다른 사용자의 작업을 쉽게 작성할 수 있는 능력은 패키지 관리 시스템을 매우 강력하게 만드는 요소 중 하나입니다. 따라서 NuGet에서 수행하는 작업 대부분은 프로젝트를 대신하여 종속성 트리 또는 "그래프"를 관리하는 것입니다. 간단히 말해, 프로젝트에서 직접 사용하는 패키지에만 집중하면 됩니다. 이러한 패키지 자체에서 다른 패키지(패키지를 사용할 수 있음)를 사용하는 경우 NuGet은 모든 하위 수준 종속성을 처리합니다.

다음 이미지에서는 다섯 개의 패키지에 종속된 프로젝트를 보여 주며, 이러한 다섯 개의 패키지도 여러 개의 다른 패키지에 종속됩니다.  

![.NET 프로젝트에 대한 NuGet 종속성 그래프 예제](media/dependency-graph.png)

일부 패키지는 종속성 그래프에 여러 번 표시됩니다. 예를 들어 B 패키지의 서로 다른 세 가지 소비자가 있으며, 각 소비자는 해당 패키지에 대해 다른 버전을 지정할 수도 있습니다(표시되지 않음). 이러한 경우는 일반적이므로 다행스럽게도 NuGet에서 모든 소비자를 충족하는 B 패키지의 정확한 버전을 확인하기 위한 모든 작업을 수행합니다. 그런 다음 NuGet에서 종속성 그래프의 세부 수준에 관계없이 다른 모든 패키지에 대해 동일한 작업을 수행합니다.

NuGet에서 이 서비스를 수행하는 방법에 대한 자세한 내용은 [종속성 확인](Consume-Packages/Dependency-Resolution.md)을 참조하세요.

## <a name="tracking-references-and-restoring-packages"></a>참조 추적 및 패키지 복원

프로젝트는 개발자 컴퓨터, 원본 제어 리포지토리, 빌드 서버 등 간에 쉽게 이동할 수 있기 때문에 프로젝트에 직접 바인딩된 NuGet 패키지에서 이진 어셈블리를 유지하는 것은 매우 실용적이지 않습니다. 이렇게 하면 프로젝트의 모든 복사본에서 수행해야 하기 때문에 프로젝트의 각 복사본이 불필요하게 너무 확장될 뿐만 아니라(이에 따라 원본 제어 리포지토리의 공간이 낭비될 수 있음), 패키지 이진 파일을 최신 버전으로 업데이트하는 것도 매우 어렵게 만듭니다. 

대신 NuGet은 간단히 프로젝트가 종속된 패키지(최상위 및 하위 수준 종속성 모두 포함)의 참조 목록을 유지 관리하고, [패키지 복원](Consume-Packages/Package-Restore.md)에서 설명한 대로 요청 시 참조된 모든 패키지를 복원할 수 있는 방법을 제공합니다. 즉 어떤 호스트에서 프로젝트로 패키지를 설치할 때마다 NuGet은 패키지 식별자와 버전 번호를 이 참조 목록에 기록합니다. (물론 패키지를 제거하면 해당 패키지가 목록에서 제거됩니다.) 

![NuGet 참조 목록은 패키지 설치 시 만들어지며, 다른 위치에서 패키지를 복원하는 데 사용할 수 있습니다.](media/nuget-restore.png)

NuGet은 나중에 언제든지 참조 목록만 사용하여 공용 및/또는 사설 호스트에서 해당 패키지 모두를 다시 설치, 즉 복원할 수 있습니다. (이러한 이유로 nuget.org에서는 게시된 패키지를 영구적으로 삭제할 수 없지만 숨길 수는 있습니다([패키지 삭제](Policies/deleting-packages.md) 참조)) 프로젝트를 원본 제어에 커밋하거나 다른 방식으로 공유하는 경우, 참조 목록만 포함하면 되고 패키지 이진 파일은 포함할 필요가 없습니다([패키지 및 원본 제어](Consume-Packages/Packages-and-Source-Control.md) 참조).

자동화된 배포 시스템의 일부로 프로젝트의 복사본을 얻는 빌드 서버와 같이 프로젝트를 받는 컴퓨터는 필요할 때마다 NuGet에서 종속성을 복원하도록 요청하기만 하면 됩니다. Visual Studio Team Services와 같은 빌드 시스템은 이와 같은 정확한 목적을 위해 "NuGet restore" 단계를 제공합니다. 마찬가지로 개발자가 프로젝트의 복사본을 얻는 경우(예: 리포지토리 복제 시) Visual Studio에서 프로젝트를 열고 빌드를 실행하면 Visual Studio에서 자동으로 필요한 NuGet 패키지를 복원합니다. 또한 개발자는 패키지 관리자 콘솔의 `nuget restore` CLI 명령 또는 `Install-Package` cmdlet을 사용하여 언제든지 패키지를 복원하도록 NuGet에 지시할 수도 있습니다.

그런 다음 개발자가 염려하는 NuGet의 주 역할은 분명히 프로젝트를 대신하여 참조 목록을 유지 관리하고, 참조된 패키지를 효율적으로 복원(및 업데이트)할 수 있는 방법을 제공하는 것입니다.

이러한 작업을 정확히 수행하는 방법이 여러 버전의 NuGet에 걸쳐 발전하면서 다음과 같은 몇 가지 *패키지 관리 형식*이 만들어졌습니다.

- [`packages.config`](Schema/packages-config.md): *(NuGet 1.0 이상)* 설치된 다른 패키지의 종속성을 포함하여 프로젝트의 모든 종속성에 대한 단순 목록을 유지 관리하는 XML 파일입니다. 
- [`project.json`](Schema/project-json.md): *(NuGet 3.0 이상)* 연결된 `project.lock.json` 파일의 전체 패키지 그래프와 함께 프로젝트의 종속성 목록을 유지 관리하는 JSON 파일입니다. 이 구조는 전이적 복원을 포함하여 [종속성 확인](Consume-Packages/Dependency-Resolution.md)에서 설명한 대로 `packages.config`에 대한 향상된 성능을 제공하지만, 일반적으로 아래의 PackageReference로 대체되었습니다.
- [프로젝트 파일의 패키지 참조](Consume-Packages/Package-References-in-Project-Files.md)("PackageReference"라고도 함) | *(NuGet 4.0 이상)* 프로젝트 파일 내에서 프로젝트의 최상위 종속성에 대한 목록을 직접 유지 관리하므로 별도의 파일이 필요하지 않습니다. 연결된 `project.assets.json` 파일은 `project.lock.json`처럼 동적으로 생성되어 전체 종속성 그래프를 관리합니다.

특정 프로젝트에서 사용되는 패키지 관리 형식은 프로젝트 형식과 NuGet 및 Visual Studio의 사용 가능한 버전에 따라 다릅니다. 사용되는 형식을 확인하려면 첫 번째 패키지를 설치한 후 프로젝트 루트에서 `packages.config` 또는 `project.json`을 찾기만 하면 됩니다. 두 파일 중 하나가 표시되지 않으면 프로젝트 파일에서 직접 &lt;PackageReference&gt; 요소를 찾습니다.

예를 들어 Visual Studio 2017에서 대부분의 프로젝트 형식은 PackageReference를 사용하는 UWP C# 및 .NET Core 프로젝트를 제외하고는 `packages.config`를 사용합니다. 

## <a name="what-else-does-nuget-do"></a>기타 NuGet 작업

지금까지 설명한 내용을 요약하자면, NuGet은 중앙 nuget.org 리포지토리를 제공하고(호스팅 역할에서) 사설 호스팅을 지원합니다. NuGet에서는 개발자가 패키지를 만들고, 게시하고, 사용하는 데 필요한 도구를 제공합니다. NuGet이 프로젝트에서 사용되는 패키지의 참조 목록 및 해당 목록에서 해당 패키지를 복원하고 업데이트할 수 있는 기능을 유지 관리한다는 것이 가장 중요합니다.

이러한 프로세스를 효율적으로 수행하기 위해 NuGet에서 몇 가지 백그라운드 최적화를 수행합니다. 특히 NuGet은 컴퓨터 전체 및 프로젝트별 패키지 캐시를 모두 간단한 설치 및 다시 설치에 맞게 관리합니다. 컴퓨터 전체 캐시와 관련된 경우 프로젝트에서 다운로드하여 설치하는 모든 패키지가 캐시에 저장되므로, 동일한 패키지를 다른 프로젝트에 설치하면 다시 다운로드할 필요가 없습니다. 이는 빌드 서버에서와 같이 더 많은 수의 패키지를 자주 복원하는 경우에 매우 유용합니다. 메커니즘 및 작업 방식에 대한 자세한 내용은 [NuGet 캐시 관리](Consume-Packages/Managing-the-Nuget-Cache.md)를 참조하세요.

개별 프로젝트 내에서 NuGet은 전체 종속성 그래프를 관리하기 위해 많은 작업을 수행합니다. (`project.json` 또는 &lt;PackageReference&gt;를 사용하는 경우 NuGet은 해당 정보를 `project.lock.json` 및 `project.assets.json`이라는 보조 파일에 각각 보관합니다.) 이렇게 하면 동일한 패키지의 서로 다른 버전에 대한 여러 참조를 확인하는 작업이 다시 포함됩니다.

즉 프로젝트에서 자체적으로 종속성이 동일한 하나 이상의 패키지에 대한 종속성을 사용하는 것이 매우 일반적입니다. 예를 들어 nuget.org에서 가장 유용한 유틸리티 패키지 중 일부는 다른 많은 패키지에서 사용됩니다. 10개의 전체 종속성 그래프에서 동일한 패키지의 서로 다른 버전에 대해 10개의 다른 참조를 쉽게 갖출 수 있습니다. 그러나 해당 패키지의 여러 버전을 응용 프로그램 자체에 가져오지 않으려고 하므로 NuGet에서는 모든 사람이 사용할 수 있는 단일 버전을 정렬합니다. (이 주제에 대한 자세한 내용은 [종속성 확인](Consume-Packages/Dependency-Resolution.md)을 참조하세요.)

그 외에도 NuGet은 패키지를 구성하는 방법([지역화](Create-Packages/Creating-Localized-Packages.md) 및 [디버그 기호](Create-Packages/Symbol-Packages.md) 포함) 및 참조하는 방법([버전 범위](reference/package-versioning.md#version-ranges-and-wildcards) 및 [시험판 버전](create-packages/Prerelease-Packages.md) 포함)과 관련된 모든 사양을 유지 관리합니다. 또한 NuGet은 자격 증명 공급자(사설 호스트 액세스용)를 위한 API 및 Visual Studio 확장과 프로젝트 템플릿을 작성하는 개발자를 위한 API도 제공합니다.

잠시 시간을 내어 이 설명서의 목차를 살펴보면 NuGet의 초기 버전까지에 해당하는 릴리스 정보와 함께 이러한 모든 기능이 나와 있습니다.

## <a name="comments-contributions-and-issues"></a>의견, 참여 및 문제

마지막으로 이 설명서에 대한 의견과 참여를 매우 환영합니다. 아무 페이지에서 **의견** 및 **편집** 명령을 선택하거나 GitHub의 [문서 리포지토리](https://github.com/NuGet/docs.microsoft.com-nuget/) 및 [문서 문제 목록](https://github.com/NuGet/docs.microsoft.com-nuget/issues)을 방문하세요.

또한 [다양한 GitHub 리포지토리](https://github.com/NuGet/Home)를 통해 NuGet에 직접 참여하는 것도 환영합니다. NuGet 문제는 [https://github.com/NuGet/home/issues](https://github.com/NuGet/home/issues)에서 확인할 수 있습니다.

여러분의 NuGet 경험을 즐겨보세요!
