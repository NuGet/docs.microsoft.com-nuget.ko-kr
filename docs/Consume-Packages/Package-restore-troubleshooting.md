---
title: Visual Studio에서 NuGet 패키지 복원 문제 해결 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/16/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Visual Studio의 일반적인 NuGet 복원 오류 및 해당 오류를 해결하는 방법의 설명입니다.
keywords: NuGet 패키지 복원, 패키지 복원, 문제 해결, 문제 해결
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 27a43ceaefdf3a7842183a64ea57d05416d6cb02
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="troubleshooting-package-restore-errors"></a>패키지 복원 오류 문제 해결

이 아티클에서는 패키지를 복원할 때 일반적인 오류 및 해당 문제를 해결하는 단계를 집중적으로 살펴봅니다. 패키지 복원에 대한 자세한 내용은 [패키지 복원](../consume-packages/package-restore.md#enabling-and-disabling-package-restore)을 참조하세요.

이 지침으로 문제가 해결되지 않을 경우 귀하의 시나리오를 더 면밀히 살펴볼 수 있도록 [GitHub에서 문제를 제출](https://github.com/NuGet/docs.microsoft.com-nuget/issues)해 주세요. 이 페이지에 표시되는 "이 페이지가 도움이 되었나요?" 컨트롤은 사용하지 마세요. Microsoft에서 귀하에게 연락하여 자세한 내용을 확인할 수 없기 때문입니다.

## <a name="quick-solution-for-visual-studio-users"></a>Visual Studio 사용자를 위한 빠른 해결책

Visual Studio를 사용하는 경우 먼저 다음과 같이 패키지 복원을 활성화합니다. 그러지 않을 경우 다음에 나오는 섹션으로 이동합니다.

1. **도구 > NuGet 패키지 관리자 > 패키지 관리자 설정** 메뉴 명령을 선택합니다.
1. **패키지 복원**에서 두 옵션을 설정합니다.
1. **확인**을 선택합니다.
1. 프로젝트를 다시 빌드합니다.

![도구/옵션에서 NuGet 패키지 복원 활성화](../consume-packages/media/restore-01-autorestoreoptions.png)

이러한 설정은 `NuGet.config` 파일에서도 변경할 수 있습니다. [동의](#consent) 섹션을 참조하세요.

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a>이 프로젝트는 이 컴퓨터에 없는 NuGet 패키지를 참조합니다.

전체 오류 메시지:

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

이 오류는 하나 이상의 NuGet 패키지에 대한 참조를 포함하는 프로젝트를 빌드하려고 시도할 때 해당 패키지가 컴퓨터 또는 프로젝트에 현재 설치되지 않은 경우에 발생합니다.

- PackageReference 관리 형식을 사용할 경우 이 오류는 [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md)(글로벌 패키지 및 캐시 폴더 관리)에 설명된 대로 패키지가 *global-packages* 폴더에 설치되지 않았음을 나타냅니다.
- `packages.config`를 사용할 경우 이 오류는 패키지가 솔루션 루트의 `packages` 폴더에 설치되어 있지 않음을 의미합니다.

이러한 상황은 일반적으로 소스 제어 또는 다른 다운로드에서 프로젝트의 소스 코드를 가져올 때 발생합니다. 패키지는 nuget.org 같은 패키지 피드에서 복원할 수 있으므로 일반적으로 소스 제어 또는 다운로드에는 패키지가 없습니다([패키지 및 소스 제어](Packages-and-Source-Control.md) 참조). 그렇지 않고 이를 포함할 경우 리포지토리가 블로트되거나 불필요하게 큰 .zip 파일이 생성됩니다.

패키지를 복원하려면 다음 방법 중 하나를 사용하세요.

- Visual Studio에서 **도구 > NuGet 패키지 관리자 > 패키지 관리자 설정** 메뉴 명령을 선택하고 **패키지 복원**에서 두 옵션을 설정하고 **확인**을 선택하여 패키지 복원을 활성화합니다. 그런 다음, 솔루션을 다시 빌드합니다.
- .NET Core 프로젝트의 경우 `dotnet restore` 또는 `dotnet build`를 실행합니다(복원이 자동으로 실행됨).
- 명령줄에서 `nuget restore`를 실행합니다(단, `dotnet`을 사용하여 만든 프로젝트의 경우에는 `dotnet restore` 사용).
- PackageReference 형식을 사용하는 프로젝트의 경우 명령줄에서 `msbuild /t:restore`를 실행합니다.

복원되면 패키지가 *global-packages* 폴더에 있어야 합니다. PackageReference를 사용하는 프로젝트의 경우 복원에서 `obj/project.assets.json` 파일을 다시 만들어야 하고, `packages.config`를 사용하는 프로젝트의 경우 패키지가 프로젝트의 `packages` 폴더에 표시되어야 합니다. 이제 프로젝트가 성공적으로 빌드됩니다. 그렇지 않을 경우 후속 조치를 위해 [GitHub에서 문제를 제출](https://github.com/NuGet/docs.microsoft.com-nuget/issues)해 주세요.

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a>자산 파일 project.assets.json을 찾을 수 없음

전체 오류 메시지:

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

`project.assets.json` 파일은 PackageReference 관리 형식을 사용할 때 프로젝트의 종속성 그래프를 유지하며, 필요한 모든 패키지가 컴퓨터에 설치되어 있는지 확인하는 데 사용됩니다. 이 파일은 패키지 복원을 통해 동적으로 생성되므로 일반적으로 소스 제어에는 추가되지 않습니다. 따라서 이 오류는 패키지를 자동으로 복원하지 않는 `msbuild`와 같은 도구를 사용하여 프로젝트를 빌드할 때 발생합니다.

이 경우 `msbuild /t:restore` 및 `msbuild`를 차례로 실행하거나 `dotnet build`를 사용합니다(그러면 패키지가 자동으로 복원됨). [이전 섹션](#missing)에서는 원하는 패키지 복원 방법을 사용할 수도 있습니다.

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a>하나 이상의 NuGet 패키지를 복원해야 하지만 동의하지 않았기 때문에 그럴 수 없음

전체 오류 메시지:

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

이 오류는 NuGet 구성에 패키지 복원이 비활성화되었음을 나타냅니다.

앞서 [Visual Studio 사용자를 위한 빠른 해결책](#quick-solution-for-visual-studio-users)에서 설명한 것처럼 Visual Studio의 해당 설정을 변경할 수 있습니다.

또한 해당 `nuget.config` 파일에서 이러한 설정을 바로 편집할 수도 있습니다(일반적으로 Windows의 경우 `%AppData%\NuGet\NuGet.Config`, Mac/Linux의 경우 `~/.nuget/NuGet/NuGet.Config`). `packageRestore` 아래의 `enabled` 및 `automatic` 키가 True로 설정되었는지 확인합니다.

```xml
<!-- Package restore is enabled -->
<configuration>
    <packageRestore>
        <add key="enabled" value="True" />
        <add key="automatic" value="True" />
    </packageRestore>
</configuration>
```

> [!Important]
> `nuget.config`에서 `packageRestore` 설정을 바로 편집할 경우 Visual Studio를 다시 시작해야 옵션 대화 상자에 최신 값이 표시됩니다.

## <a name="other-potential-conditions"></a>다른 잠재적 상태

- 파일이 없을 경우 NuGet 복원을 사용하려면 해당 파일을 다운로드하라는 메시지와 함께 빌드 오류가 발생할 수 있습니다. 하지만 복원을 실행할 때 "모든 패키지가 이미 설치되어 있으며 복원할 항목이 없습니다"라는 메시지가 나타날 수 있습니다. 이 경우 `packages` 폴더(`packages.config` 사용 시) 또는 `obj/project.assets.json` 파일(PackageReference 사용 시)을 삭제하고 복원을 다시 실행하세요. 그래도 오류가 지속되면 명령줄에서 [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md)(전역 패키지 및 캐시 폴더 관리)에 설명된 대로 `nuget locals all -clear` 또는 `dotnet locals all --clear`를 사용하여 *global-packages* 및 캐시 폴더를 지웁니다.

- 소스 제어에서 프로젝트를 가져올 때 프로젝트 폴더가 읽기 전용으로 설정되어 있을 수 있습니다. 폴더 사용 권한을 변경하고 패키지를 다시 복원해 보세요.

- 이전 버전의 NuGet를 사용 중일 수 있습니다. [nuget.org/downloads](https://www.nuget.org/downloads)에서 최신 권장 버전을 확인하세요. Visual Studio 2015의 경우 3.6.0을 권장합니다.

다른 문제가 발생할 경우 자세한 내용을 확인할 수 있도록 [GitHub에서 문제를 제출](https://github.com/NuGet/docs.microsoft.com-nuget/issues)해 주세요.