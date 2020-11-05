---
title: Windows의 Visual Studio에서 .NET Standard NuGet 패키지 만들기 및 게시
description: Windows에서 Visual Studio를 사용하여 .NET Standard NuGet 패키지를 만들고 게시하는 방법에 대한 연습 자습서입니다.
author: karann-msft
ms.author: karann
ms.date: 08/16/2019
ms.topic: quickstart
ms.openlocfilehash: 32dcc1d233154463e2950b1ce46554b1cb89956e
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237499"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a>빠른 시작: Visual Studio(.NET Standard, Windows 전용)를 사용하여 NuGet 패키지 만들기 및 게시

Windows에서 Visual Studio의 .NET Standard 클래스 라이브러리에서 NuGet 패키지를 만들고 CLI 도구를 사용하여 nuget.org에 게시하는 간단한 과정입니다.

> [!Note]
> Mac용 Visual Studio를 사용하는 경우 NuGet 패키지 생성에 대해 [이 정보](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library)를 참조하거나 [dotnet CLI 도구](create-and-publish-a-package-using-the-dotnet-cli.md)를 사용하세요.

## <a name="prerequisites"></a>사전 요구 사항

1. .NET Core 관련 워크로드를 사용하여 [visualstudio.com](https://www.visualstudio.com/)에서 모든 버전의 Visual Studio 2019를 설치합니다.

1. 아직 설치하지 않은 경우 `dotnet` CLI를 설치합니다.

   `dotnet` CLI의 경우, Visual Studio 2017부터 `dotnet` CLI가 모든 .NET Core 관련 워크로드와 함께 자동으로 설치됩니다. 그렇지 않으면 [.NET Core SDK](https://www.microsoft.com/net/download/)를 설치하여 `dotnet` CLI를 가져옵니다. `dotnet` CLI는 [SDK 스타일 형식](../resources/check-project-format.md)(SDK 특성)을 사용하는 .NET Standard 프로젝트에 필요합니다. 이 문서에서 사용되는 Visual Studio 2017 이상의 기본 .NET Standard 클래스 라이브러리 템플릿은 SDK 특성을 사용합니다.
   
   > [!Important]
   > 비 SDK 스타일 프로젝트를 사용하는 경우 대신 [.NET Framework 패키지(Visual Studio) 만들기 및 게시](create-and-publish-a-package-using-visual-studio-net-framework.md)의 절차에 따라 패키지를 만들고 게시합니다. 이 문서에서는 `dotnet` CLI가 권장됩니다. `nuget.exe` CLI를 사용하여 NuGet 패키지를 게시할 수는 있지만 이 문서의 일부 단계는 SDK 스타일 프로젝트 및 dotnet CLI와 관련이 있습니다. nuget.exe CLI는 [비 SDK 스타일 프로젝트](../resources/check-project-format.md)에 사용됩니다(일반적으로 .NET Framework).

1. 아직 없는 경우 [nuget.org에 체험 계정을 등록](../nuget-org/individual-accounts.md#add-a-new-individual-account)합니다. 새 계정을 만들면 확인 전자 메일을 보냅니다. 패키지를 업로드하려면 먼저 계정을 확인해야 합니다.

## <a name="create-a-class-library-project"></a>클래스 라이브러리 프로젝트 만들기

패키지할 코드에 대해 기존 .NET Standard 클래스 라이브러리 프로젝트를 사용하거나 다음과 같이 간단한 프로젝트를 만듭니다.

1. Visual Studio에서 **파일 > 새로 만들기 > 프로젝트** 를 차례로 선택하고, **Visual C# > .NET Standard** 노드를 펼치고, “클래스 라이브러리(.NET Standard)” 템플릿을 선택하고, 프로젝트 이름을 AppLogger로 지정한 다음, **확인** 을 클릭합니다.

   > [!Tip]
   > 별도로 선택하지 않는 한 .NET Standard는 가장 넓은 범위의 사용하는 프로젝트와 호환되기 때문에 NuGet 패키지의 기본 대상입니다.

1. 결과 프로젝트 파일을 마우스 오른쪽 단추로 클릭하고, **빌드** 를 선택하여 프로젝트가 제대로 만들어졌는지 확인합니다. DLL은 Debug(또는 해당 구성을 대신 빌드하는 경우 Release) 폴더 내에 있습니다.

물론 실제 NuGet 패키지 내에서 다른 사람들이 애플리케이션을 빌드할 수 있는 많은 유용한 기능을 구현할 것입니다. 그러나 이 연습에서는 템플릿의 클래스 라이브러리가 패키지를 만드는 데 충분하므로 추가 코드를 작성하지 않습니다. 그러나 계속 패키지에 대한 함수형 코드를 원하는 경우 다음을 사용하세요.

```cs
namespace AppLogger
{
    public class Logger
    {
        public void Log(string text)
        {
            Console.WriteLine(text);
        }
    }
}
```

## <a name="configure-package-properties"></a>패키지 속성 구성

1. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **속성** 메뉴 명령을 선택한 후 **패키지** 탭을 선택합니다.

   **패키지** 탭은 Microsoft Visual Studio의 SDK 스타일 프로젝트(일반적으로 .NET Standard 또는 .NET Core 클래스 라이브러리 프로젝트)에 대해서만 표시됩니다. 비 SDK 스타일 프로젝트(일반적으로 .NET Framework)를 대상으로 하는 경우, [프로젝트 마이그레이션](../consume-packages/migrate-packages-config-to-package-reference.md)을 수행하거나 단계별 지침 대신 [.NET Framework 패키지 만들기 및 게시](create-and-publish-a-package-using-visual-studio-net-framework.md)를 참조하세요.

    ![Visual Studio 프로젝트의 NuGet 패키지 속성](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > 공용으로 빌드된 패키지의 경우 **태그** 속성에 특히 주의하세요. 태그는 다른 사람들이 패키지를 찾고 그 기능을 이해하는 데 도움이 됩니다.

1. 패키지에 고유 식별자를 제공하고 원하는 다른 모든 속성을 채웁니다. MSBuild 속성(SDK 스타일 프로젝트)을 *.nuspec* 의 속성에 매핑하려면 [대상 압축](../reference/msbuild-targets.md#pack-target)을 참조하세요. 속성 설명은 [.nuspec 파일 참조](../reference/nuspec.md)를 참조하세요. 여기에 있는 모든 속성은 Visual Studio에서 프로젝트에 대해 만드는 `.nuspec` 매니페스트로 이동합니다.

    > [!Important]
    > nuget.org 또는 무엇이든 사용 중인 호스트에서 고유한 식별자를 패키지에 제공해야 합니다. 이 연습에서는 나중 게시 단계에서 패키지를 공개적으로 표시할 수 있도록 이름에 “샘플” 또는 “테스트”를 포함하는 것이 좋습니다(실제로 아무도 사용할 가능성이 없더라도).
    >
    > 이미 존재하는 이름으로 패키지를 게시하려고 시도하면 오류가 표시됩니다.

1. (선택 사항) 프로젝트 파일에서 직접 속성을 보려면 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **AppLogger.csproj 편집** 을 선택합니다.

   이 옵션은 SDK 스타일 특성을 사용하는 프로젝트의 경우 Visual Studio 2017부터만 사용할 수 있습니다. 그렇지 않은 경우 프로젝트를 마우스 오른쪽 단추로 클릭하고 **프로젝트 언로드** 를 선택합니다. 그런 다음, 언로드된 프로젝트를 마우스 오른쪽 단추로 클릭하고 **AppLogger.csproj 편집** 을 선택합니다.

## <a name="run-the-pack-command"></a>pack 명령 실행

1. 구성을 **해제** 로 설정합니다.

1. **솔루션 탐색기** 에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **Pack** 명령을 선택합니다.

    ![Visual Studio 프로젝트 상황에 맞는 메뉴의 NuGet pack 명령](media/qs_create-vs-02-pack-command.png)

    **Pack** 명령이 표시되지 않는 경우 프로젝트는 SDK 스타일 프로젝트가 아닌 것이므로 `nuget.exe` CLI를 사용해야 합니다. [프로젝트를 마이그레이션](../consume-packages/migrate-packages-config-to-package-reference.md)하고 `dotnet` CLI를 사용하거나 단계별 지침 대신 [.NET Framework 패키지 만들기 및 게시](create-and-publish-a-package-using-visual-studio-net-framework.md)를 참조하세요.

1. Visual Studio에서 프로젝트를 빌드하고 `.nupkg` 파일을 만듭니다. **출력** 창에서 패키지 파일의 경로가 포함된 다음과 같은 세부 정보가 있는지 확인합니다. 또한 빌드된 어셈블리는 .NET Standard 2.0 대상에 맞게 `bin\Release\netstandard2.0`에 있습니다.

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="optional-generate-package-on-build"></a>(선택 사항) 빌드 시 패키지 생성

프로젝트를 빌드할 때 NuGet 패키지를 자동으로 생성하도록 Visual Studio를 구성할 수 있습니다.

1. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **속성** 을 선택합니다.

2. **패키지** 탭에서 **빌드 시 NuGet 패키지 생성** 을 선택합니다.

   ![빌드 시 패키지를 자동으로 생성](media/qs_create-vs-05-generate-on-build.png)

> [!NOTE]
> 패키지를 자동으로 생성할 때 압축하는 데 소요되는 시간 때문에 프로젝트의 빌드 시간이 늘어납니다.

### <a name="optional-pack-with-msbuild"></a>(선택 사항) MSBuild를 사용하여 압축

**Pack** 메뉴 명령을 사용하는 대신 프로젝트에 필요한 패키지 데이터가 포함된 경우 NuGet 4.x 이상 및 MSBuild 15.1 이상은 `pack` 대상을 지원합니다. 명령 프롬프트를 열고 프로젝트 폴더로 이동한 후 다음 명령을 실행합니다. (일반적으로 시작 메뉴에서 "Visual Studio용 개발자 명령 프롬프트"를 시작하는 것이 좋습니다. MSBuild에 필요한 모든 경로로 구성되기 때문입니다.)

자세한 내용은 [MSBuild를 사용하여 패키지 만들기](../create-packages/creating-a-package-msbuild.md)를 참조하세요.

## <a name="publish-the-package"></a>패키지 게시

`.nupkg` 파일이 있으면 nuget.org에서 얻은 API 키와 함께 `nuget.exe` CLI 또는 `dotnet.exe` CLI를 사용하여 nuget.org에 게시합니다.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>API 키 얻기

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-the-dotnet-cli-or-nugetexe-cli"></a>dotnet CLI 또는 nuget.exe CLI를 사용하여 게시

**.NET Core CLI** (dotnet CLI) 또는 **NuGet** (nuget.exe CLI) 중에서 CLI 도구용 탭을 하나 선택합니다.

# <a name="net-core-cli"></a>[.NET Core CLI](#tab/netcore-cli)

이 단계는 `nuget.exe`를 사용하는 방법의 대안으로 권장됩니다.

패키지를 게시하려면 먼저 명령줄을 열어야 합니다.

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

# <a name="nuget"></a>[NuGet](#tab/nuget)

`dotnet.exe`를 사용하는 대신 다음 단계를 사용할 수 있습니다.

1. 명령줄을 열고 `.nupkg` 파일을 포함하는 폴더로 변경합니다.

1. 다음 명령을 실행하여 패키지 이름(고유한 패키지 ID)을 지정하고 키 값을 API 키로 바꿉니다.

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. nuget.exe에서 게시 프로세스의 결과를 표시합니다.

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

[nuget push](../reference/cli-reference/cli-ref-push.md)를 참조하세요.

---

### <a name="publish-errors"></a>게시 오류

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>게시된 패키지 관리

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="adding-a-readme-and-other-files"></a>추가 정보 및 기타 파일 추가

패키지에 포함할 파일을 직접 지정하려면 프로젝트 파일을 편집하고 `content` 속성을 사용합니다.

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

그러면 패키지 루트에 있는 `readme.txt`라는 파일이 포함됩니다. Visual Studio에서 패키지를 직접 설치한 직후 해당 파일의 내용을 일반 텍스트로 표시합니다. 종속성으로 설치된 패키지에는 추가 정보 파일이 표시되지 않습니다. 예를 들어 HtmlAgilityPack 패키지에 대한 추가 정보가 다음과 같이 표시됩니다.

![설치 시 NuGet 패키지에 대한 추가 정보 파일 표시](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> 프로젝트 루트에 readme.txt를 단순히 추가하기만 하면 결과 패키지에 포함되지 않습니다.

## <a name="related-video"></a>관련 동영상

> [!Video https://channel9.msdn.com/Series/NuGet-101/Create-and-Publish-a-NuGet-Package-with-Visual-Studio-4-of-5/player]

[Channel 9](https://channel9.msdn.com/Series/NuGet-101) 및 [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_)에서 더 많은 NuGet 비디오를 확인하세요.

## <a name="related-topics"></a>관련 항목

- [패키지 만들기](../create-packages/creating-a-package-dotnet-cli.md)
- [패키지 게시](../nuget-org/publish-a-package.md)
- [시험판 패키지](../create-packages/Prerelease-Packages.md)
- [여러 대상 프레임워크 지원](../create-packages/multiple-target-frameworks-project-file.md)
- [패키지 버전 관리](../concepts/package-versioning.md)
- [지역화된 패키지 만들기](../create-packages/creating-localized-packages.md)
- [.NET Standard 라이브러리 설명서](/dotnet/articles/standard/library)
- [.NET Framework에서 .NET Core로 이식](/dotnet/articles/core/porting/index)
