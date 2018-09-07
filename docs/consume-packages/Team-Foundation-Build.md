---
title: Team Foundation 빌드를 사용하여 NuGet 패키지 복원 연습
description: Team Foundation Build(TFS 및 Visual Studio Team Services)에서 NuGet 패키지를 복원하는 방법의 연습입니다.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 0e69491525fce03e504d9d455bee2718510c83c2
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549887"
---
# <a name="setting-up-package-restore-with-team-foundation-build"></a>Team Foundation 빌드를 사용하여 패키지 복원 설정

이 문서는 [Team Services 빌드](/vsts/build-release/index)의 일환으로 Git 및 Team Services 버전 제어에서 패키지를 복원하는 방법에 대한 자세한 연습을 제공합니다.

Visual Studio Team Services를 사용하는 시나리오에 이 연습이 지정되지만 개념은 다른 버전 제어에도 적용되고 시스템을 빌드합니다.

적용 대상:

- TFS의 모든 버전에서 실행되는 MSBuild 프로젝트 사용자 지정
- Team Foundation Server 2012 이전
- TFS 2013 이상으로 마이그레이션된 Team Foundation 빌드 프로세스 템플릿 사용자 지정
- Nuget 복원 기능이 제거된 프로세스 템플릿 빌드

해당 빌드 프로세스 템플릿에서 Visual Studio Team Services 또는 Team Foundation Server 2013을 사용하는 경우 빌드 프로세스의 일부로 자동 패키지가 복원됩니다.

## <a name="the-general-approach"></a>일반적인 접근 방법

NuGet을 사용하는 경우의 이점은 버전 제어 시스템에 대한 이진 파일을 검사하지 않도록 방지하기 위해 사용할 수 있다는 것입니다.

개발자가 로컬로 작업을 시작하기 전에 전체 기록을 포함하여 전체 리포지토리를 복제해야 하기 때문에 Git과 같은 [분산 버전 제어](http://en.wikipedia.org/wiki/Distributed_revision_control) 시스템을 사용 중인 경우에 특히 흥미롭습니다. 이진 파일을 체크 인하면 이진 파일이 델타 압축 없이 일반적으로 저장되므로 상당한 리포지토리 블로트가 발생할 수 있습니다.

NuGet은 오랜 시간 동안 빌드의 일부로 [패키지를 복원](../consume-packages/package-restore.md)하도록 지원했습니다. 프로젝트를 빌드하는 동안 NuGet이 패키지를 복원했기 때문에 이전 구현은 빌드 프로세스 확장하려는 패키지에서 '닭이 먼저냐, 달걀이 먼저냐'와 같은 문제가 있었습니다. 그러나 MSBuild는 빌드 중에 빌드를 확장할 수 없습니다. 따라서 MSBuild에 문제가 있다고 주장할 수 있지만 근본적인 문제라고 생각합니다. 확장해야 하는 측면에 따라 패키지를 복원할 때에는 등록하기가 너무 늦을 수 있습니다.

이 문제를 수정하려면 빌드 프로세스에서 첫 번째 단계로 패키지를 복원했는지 확인합니다.

```cli
nuget restore path\to\solution.sln
```

코드를 빌드하기 전에 프로세스 복원 패키지를 빌드하는 경우 `.targets` 파일을 체크 인할 필요가 없습니다

> [!Note]
> Visual Studio에서 로드를 허용하도록 패키지를 작성해야 합니다. 그렇지 않으면 다른 개발자가 먼저 패키지를 복원하지 않고도 쉽게 솔루션을 열 수 있도록 `.targets` 파일을 체크 인하는 것이 좋습니다.

다음 데모 프로젝트는 `packages` 폴더 및 `.targets` 파일을 체크 인할 필요가 없는 방식으로 빌드를 설정하는 방법을 보여줍니다. 또한 이 샘플 프로젝트에서 Team Foundation Service에 자동화된 빌드를 설정하는 방법을 보여줍니다.

## <a name="repository-structure"></a>리포지토리 구조

이 데모 프로젝트는 Bing을 쿼리하는 데 명령줄 인수를 사용하는 간단한 명령줄 도구입니다. .NET Framework 4를 대상으로 지정하고 [BCL 패키지](http://www.nuget.org/profiles/dotnetframework/)를 사용합니다([Microsoft.Net.Http](http://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](http://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](http://www.nuget.org/packages/Microsoft.Bcl.Async) 및 [Microsoft.Bcl.Build](http://www.nuget.org/packages/Microsoft.Bcl.Build)).

리포지토리의 구조는 다음과 같습니다.

    <Project>
        │   .gitignore
        │   .tfignore
        │   build.proj
        │
        ├───src
        │   │   BingSearcher.sln
        │   │
        │   └───BingSearcher
        │       │   App.config
        │       │   BingSearcher.csproj
        │       │   packages.config
        │       │   Program.cs
        │       │
        │       └───Properties
        │               AssemblyInfo.cs
        │
        └───tools
            └───NuGet
                    nuget.exe

`packages` 폴더나 `.targets` 파일을 아직 체크 인하지 않은 것을 확인할 수 있습니다.

그러나 빌드 중에 필요한 경우 `nuget.exe`을 체크 인했습니다. 다음은 공유 `tools` 폴더 아래에서 체크 인한 규칙을 광범위하게 사용했습니다.

소스 코드는 `src` 폴더 아래에 있습니다. 데모에서 단일 솔루션만을 사용하지만 이 폴더에 하나 이상의 솔루션이 포함되어 있다고 쉽게 상상할 수 있습니다.

### <a name="ignore-files"></a>파일 무시

> [!Note]
> 현재 클라이언트를 버전 제어에 대한 `packages` 폴더에 추가하는 [NuGet 클라이언트의 알려진 버그](https://nuget.codeplex.com/workitem/4072)가 있습니다. 해결 방법은 소스 제어 통합을 사용하지 않도록 설정하는 것입니다. 이를 수행하려면 솔루션에 병렬되는 `.nuget` 폴더에 `Nuget.Config ` 파일이 필요합니다. 이 폴더가 아직 존재하지 않으면 만들어야 합니다. [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md)에서 다음 콘텐츠를 추가합니다.

```xml
<configuration>
    <solution>
        <add key="disableSourceControlIntegration" value="true" />
    </solution>
</configuration>
```

**패키지** 폴더를 체크 인하지 않으려는 버전 제어에 통신하기 위해 TF 버전 제어(`.tfignore`)뿐만 아니라 두 Git(`.gitignore`)에 무시 파일을 추가했습니다. 이러한 파일은 체크 인하지 않으려는 파일의 패턴을 설명합니다.

`.gitignore` 파일은 다음과 같습니다.

    syntax: glob
    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

`.gitignore` 파일은 [매우 강력](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html)합니다. 예를 들어, 일반적으로 `packages` 폴더의 콘텐츠를 체크 인하지 않지만 `.targets` 파일을 체크인하는 이전 지침으로 이동하려는 경우 대신 다음 규칙이 있을 수 있습니다.

    packages
    !packages/**/*.targets

이렇게 하면 모든 `packages` 폴더를 제외하지만 포함된 모든 `.targets` 파일을 다시 포함합니다. Visual Studio 개발자의 요구를 위해 특별히 조정된 `.gitignore` 파일의 템플릿을 [여기](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore)에서 찾을 수 있습니다.

TF 버전 제어는 [.tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) 파일을 통해 매우 유사한 메커니즘을 지원합니다. 구문은 거의 동일합니다.

    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

## <a name="buildproj"></a>build.proj

이 데모에서는 빌드 프로세스 매우 단순합니다. 솔루션을 빌드하기 전에 패키지가 복원되었는지 확인하는 동안 모든 솔루션을 빌드하는 MSBuild 프로젝트를 만듭니다.

이 프로젝트에는 기존의 세 가지 대상인 `Clean`, `Build` 및 `Rebuild`뿐만 아니라 새 대상 `RestorePackages`가 있습니다.

- `Build` 및 `Rebuild` 대상은 둘 다 `RestorePackages`에 따라 달라집니다. 이렇게 하면 `Build` 및 `Rebuild` 둘 다를 실행하고 복원되는 패키지를 사용할 수 있습니다.
- `Clean`, `Build` 및 `Rebuild`는 모든 솔루션 파일에서 해당하는 MSBuild 대상을 호출합니다.
- `RestorePackages` 대상은 각 솔루션 파일의 `nuget.exe`를 호출합니다. [MSBuild 일괄 처리 기능](/visualstudio/msbuild/msbuild-batching)을 사용하여 수행합니다.

결과는 다음과 같습니다.

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project ToolsVersion="4.0"
            DefaultTargets="Build"
            xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <PropertyGroup>
    <OutDir Condition=" '$(OutDir)'=='' ">$(MSBuildThisFileDirectory)bin\</OutDir>
    <Configuration Condition=" '$(Configuration)'=='' ">Release</Configuration>
    <SourceHome Condition=" '$(SourceHome)'=='' ">$(MSBuildThisFileDirectory)src\</SourceHome>
    <ToolsHome Condition=" '$(ToolsHome)'=='' ">$(MSBuildThisFileDirectory)tools\</ToolsHome>
    </PropertyGroup>

    <ItemGroup>
    <Solution Include="$(SourceHome)*.sln">
        <AdditionalProperties>OutDir=$(OutDir);Configuration=$(Configuration)</AdditionalProperties>
    </Solution>
    </ItemGroup>

    <Target Name="RestorePackages">
    <Exec Command="&quot;$(ToolsHome)NuGet\nuget.exe&quot; restore &quot;%(Solution.Identity)&quot;" />
    </Target>

    <Target Name="Clean">
    <MSBuild Targets="Clean"
                Projects="@(Solution)" />
    </Target>

    <Target Name="Build" DependsOnTargets="RestorePackages">
    <MSBuild Targets="Build"
                Projects="@(Solution)" />
    </Target>

    <Target Name="Rebuild" DependsOnTargets="RestorePackages">
    <MSBuild Targets="Rebuild"
                Projects="@(Solution)" />
    </Target>
</Project>
```

## <a name="configuring-team-build"></a>팀 빌드 구성

팀 빌드에서는 다양한 프로세스 템플릿을 제공합니다. 이 데모에서는 Team Foundation Service를 사용합니다. 하지만 TFS의 온-프레미스 설치는 매우 유사합니다.

Git 및 TF 버전 제어에는 다른 팀 빌드 템플릿이 있으므로 다음 단계는 사용하는 버전 제어 시스템에 따라 다릅니다. 두 경우에 빌드하려는 프로젝트로 build.proj를 선택하기만 하면 됩니다.

먼저 Git에 대한 프로세스 템플릿을 살펴보겠습니다. Git 기반 템플릿에서 `Solution to build` 속성을 통해 빌드를 선택합니다.

![Git의 빌드 프로세스](media/PackageRestoreTeamBuildGit.png)

이 속성은 리포지토리에 위치합니다. `build.proj`가 루트에 있으므로 `build.proj`를 사용했습니다. `tools`이라는 폴더 아래에서 빌드 파일을 배치하는 경우 값은 `tools\build.proj`입니다.

TF 버전 컨트롤 템플릿에서 `Projects` 속성을 통해 프로젝트를 선택합니다.

![TFVC의 빌드 프로세스](media/PackageRestoreTeamBuildTFVC.png)

Git 기반 템플릿과 달리 TF 버전 제어는 선택기(세 개의 점이 있는 오른쪽의 단추)를 지원합니다. 따라서 입력 오류를 방지하기 위해 프로젝트를 선택하는 데 사용하는 것이 좋습니다.
