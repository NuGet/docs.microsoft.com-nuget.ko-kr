---
title: NuGet 패키지 사용에 대한 개요 및 워크플로
description: 프로젝트에서 NuGet 패키지를 사용하는 프로세스를 간략히 설명하며, 프로세스의 다른 특정 부분에 대한 링크가 포함되어 있습니다.
author: JonDouglas
ms.author: jodou
ms.date: 03/22/2018
ms.topic: conceptual
ms.openlocfilehash: d1d6df3bcc36d8a78fcee97099b301c9ffc440d9
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323637"
---
# <a name="package-consumption-workflow"></a>패키지 사용 워크플로

nuget.org와 조직에서 설정할 수 있는 개인 패키지 갤러리 사이에는 앱과 서비스에서 사용할 수 있는 매우 유용한 수만 개의 패키지가 있습니다. 그러나 소스와 관계없이 패키지를 사용하는 것은 아래와 같은 일반 워크플로를 따릅니다.

![패키지 원본으로 이동, 패키지 찾기, 프로젝트에 설치, using 문 및 패키지 API 호출 추가를 수행하는 흐름](media/Overview-01-GeneralFlow.png)

\* _Visual Studio `dotnet.exe` 에만 해당합니다. `nuget install` 명령은 프로젝트 파일 또는 `packages.config` 파일을 수정하지 않습니다. 이러한 항목은 수동으로 관리해야 합니다._

자세한 내용은 [패키지 찾기 및 선택](../consume-packages/finding-and-choosing-packages.md) 및 [패키지를 설치하면 어떻게 되나요?](../concepts/package-installation-process.md)를 참조하세요.

NuGet은 설치된 각 패키지의 ID와 버전 번호를 기억하여 프로젝트 형식과 NuGet 버전에 따라 프로젝트 파일([PackageReference](../consume-packages/package-references-in-project-files.md)) 또는 [`packages.config`](../reference/packages-config.md)에 기록합니다. NuGet 4.0 이상에서는 Visual Studio에서 [패키지 관리자 UI](install-use-packages-visual-studio.md)를 통해 구성할 수는 있지만 PackageReference를 사용하는 것이 좋습니다. 어떤 경우이든 언제든지 적절한 파일을 확인하여 프로젝트에 대한 전체 종속성 목록을 볼 수 있습니다.

> [!Tip]
> 소프트웨어에서 사용하려는 각 패키지의 라이선스를 항상 확인하는 것이 좋습니다. nuget.org에서는 각 패키지의 설명 페이지 오른쪽에 **라이선스 정보** 링크가 있습니다. 패키지에서 사용 조건을 지정하지 않은 경우 패키지 페이지의 **연락처 소유자** 링크를 사용하여 패키지 소유자에게 직접 문의해 보세요. Microsoft는 타사 패키지 공급자로부터 사용자에게 지적 재산권을 부여하지 않으며 타사에서 제공한 정보에 대해 책임을 지지 않습니다.

패키지를 설치할 때 NuGet은 일반적으로 해당 캐시에서 패키지를 이미 사용할 수 있는지 확인합니다. [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md)(전역 패키지 및 캐시 폴더 관리)에서 설명한 대로 명령줄에서 이 캐시를 수동으로 지울 수 있습니다.

또한 NuGet은 패키지에서 지원하는 대상 프레임워크가 프로젝트와 호환되는지 확인합니다. 패키지에 호환되는 어셈블리가 없으면 NuGet에서 오류를 표시합니다. [호환되지 않는 패키지 오류 해결](../concepts/dependency-resolution.md#resolving-incompatible-package-errors)을 참조하세요.

원본 리포지토리에 프로젝트 코드를 추가할 때는 일반적으로 NuGet 패키지가 포함되지 않습니다. 나중에 리포지토리를 복제하거나 Visual Studio Team Services와 같은 시스템의 빌드 에이전트를 포함하여 프로젝트를 가져오는 사용자는 빌드를 실행하기 전에 필요한 패키지를 복원해야 합니다.

![리포지토리를 복제하고 restore 명령 중 하나를 사용하여 NuGet 패키지를 복원하는 흐름](media/Overview-02-RestoreFlow.png)

[패키지 복원](../consume-packages/package-restore.md)은 프로젝트 파일 또는 `packages.config`의 정보를 사용하여 모든 종속성을 다시 설치합니다. [종속성 확인](../concepts/dependency-resolution.md)에서 설명한 대로 관련된 프로세스에는 차이점이 있습니다. 또한 위의 다이어그램에는 패키지 관리자 콘솔의 복원 명령은 표시되어 있지 않습니다. 이는 이미 Visual Studio 컨텍스트에 있는 콘솔을 사용 중이기 때문이며, 이 콘솔에서는 일반적으로 패키지를 자동으로 복원하고 표시된 솔루션 수준 명령을 제공합니다.

때로는 이미 프로젝트에 포함되어 있는 패키지를 다시 설치해야 하며, 종속성을 다시 설치할 수도 있습니다. 이 작업은 `nuget reinstall` 명령이나 NuGet 패키지 관리자 콘솔을 사용하여 쉽게 수행할 수 있습니다. 자세한 내용은 [패키지 다시 설치 및 업데이트](../consume-packages/reinstalling-and-updating-packages.md)를 참조하세요.

마지막으로 NuGet의 동작은 `NuGet.Config` 파일로 구동됩니다. [NuGet 동작 구성](../consume-packages/configuring-nuget-behavior.md)에서 설명한 대로 여러 파일을 사용하여 서로 다른 수준의 특정 설정을 중앙 집중화할 수 있습니다.

## <a name="ways-to-install-a-nuget-package"></a>NuGet 패키지를 설치하는 방법

다음 표의 방법 중 하나를 사용하여 NuGet 패키지를 다운로드하고 설치합니다.

| 도구 | 플랫폼 | 설명 |
| --- | --- | --- |
| [dotnet CLI](install-use-packages-dotnet-cli.md) | 모두 | .NET Core 및 .NET Standard 라이브러리와 .NET Framework를 대상으로 하는 SDK 스타일 프로젝트를 위한 CLI 도구입니다([SDK 특성](/dotnet/core/tools/csproj#additions) 참조). \<package_name\>으로 식별된 패키지를 검색하고 프로젝트 파일에 참조를 추가합니다. 종속성도 검색하고 설치합니다. |
| Visual Studio | Windows 및 Mac | 지정된 패키지 소스에서 패키지와 종속성을 찾아서 선택하고 프로젝트에 설치할 수 있는 UI를 제공합니다. 설치된 패키지에 대한 참조를 프로젝트 파일에 추가합니다.<ul><li>[Visual Studio를 사용하여 패키지 설치 및 관리](install-use-packages-visual-studio.md)</li><li>[프로젝트에 NuGet 패키지 포함(Mac)](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| [패키지 관리자 콘솔(Visual Studio)](install-use-packages-powershell.md) | Windows만 | 선택한 소스에서 \<package_name\>으로 식별되는 패키지를 검색하여 솔루션의 지정된 프로젝트에 설치하고 참조를 프로젝트 파일에 추가합니다. 종속성도 검색하고 설치합니다. |
| [nuget.exe CLI](install-use-packages-nuget-cli.md) | 모두 | .NET Framework 라이브러리와 .NET Standard 라이브러리를 대상으로 하는 SDK 스타일이 아닌 프로젝트를 위한 CLI 도구입니다. \<package_name\>으로 식별되는 패키지를 검색하고 해당 콘텐츠를 현재 디렉터리의 폴더로 확장합니다. `packages.config` 파일에 나열된 모든 패키지를 검색할 수도 있습니다. 종속성도 검색하고 설치하지만 프로젝트 파일 또는 `packages.config`는 변경하지 않습니다. |
