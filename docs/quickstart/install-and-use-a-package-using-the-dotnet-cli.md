---
title: dotnet CLI를 사용하여 NuGet 패키지 설치 및 사용
description: .NET Core 프로젝트에서 NuGet 패키지를 설치하고 사용하는 프로세스에 대한 연습 자습서입니다.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 006fff8360ac62393e4b88c1a253514591d22f4c
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231280"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a>빠른 시작: dotnet CLI를 사용하여 패키지 설치 및 사용

NuGet 패키지는 다른 개발자가 프로젝트에서 사용하기 위해 제공하는 다시 사용할 수 있는 코드를 포함합니다. 배경 지식은 [NuGet이란?](../What-is-NuGet.md)을 참조하세요. 패키지는 이 문서에 설명된 대로 널리 사용되는 `dotnet add package`Newtonsoft.Json[ 패키지에 대해 ](https://www.nuget.org/packages/Newtonsoft.Json/) 명령을 사용하여 .NET Core 프로젝트에 설치됩니다.

패키지가 설치되면 `using <namespace>`를 사용하여 코드에서 패키지를 참조합니다. 여기서 \<네임스페이스\>는 사용 중인 패키지에 특정됩니다. 그런 다음, 패키지의 API를 사용할 수 있습니다.

> [!Tip]
> **nuget.org 시작**: nuget.org 검색은 일반적으로 .NET 개발자가 고유의 애플리케이션에서 다시 사용할 수 있는 구성 요소를 찾는 방법입니다. nuget.org를 직접 검색하거나 이 문서에 표시된 대로 Visual Studio 내에서 패키지를 설치할 수 있습니다.

## <a name="prerequisites"></a>사전 요구 사항

- [ 명령줄 도구를 제공하는 ](https://www.microsoft.com/net/download/).NET Core SDK`dotnet`. Visual Studio 2017부터 dotnet CLI는 모든 .NET Core 관련 워크로드와 함께 자동으로 설치됩니다.

## <a name="create-a-project"></a>프로젝트 만들기

NuGet 패키지는 일종의 .NET 프로젝트에 설치할 수 있습니다. 이 연습에서는 다음과 같이 간단한 .NET Core 콘솔 프로젝트를 만듭니다.

1. 프로젝트의 폴더를 만듭니다.

1. 명령 프롬프트를 열고 새 폴더로 전환합니다.

1. 다음 명령을 사용하여 프로젝트를 만듭니다.

    ```dotnetcli
    dotnet new console
    ```

1. `dotnet run`을 사용하여 앱이 제대로 만들어졌는지 테스트합니다.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Newtonsoft.Json NuGet 패키지 추가

1. 다음 명령을 사용하여 `Newtonsoft.json` 패키지를 설치합니다.

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

2. 명령이 완료된 후 `.csproj` 파일을 열어 추가된 참조를 확인합니다.

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>앱에서 Newtonsoft.Json API 사용

1. `Program.cs` 파일을 열고 파일 맨 위에 다음 줄을 추가합니다.

    ```cs
    using Newtonsoft.Json;
    ```

1. `class Program` 줄 앞에 다음 코드를 추가합니다.

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. `Main` 함수를 다음과 같이 바꿉니다.

    ```cs
    static void Main(string[] args)
    {
        Account account = new Account
        {
            Name = "John Doe",
            Email = "john@nuget.org",
            DOB = new DateTime(1980, 2, 20, 0, 0, 0, DateTimeKind.Utc),
        };

        string json = JsonConvert.SerializeObject(account, Formatting.Indented);
        Console.WriteLine(json);
    }
    ```

1. `dotnet run` 명령을 사용하여 앱을 빌드하고 실행합니다. 출력은 코드에서 `Account` 개체의 JSON 표현이어야 합니다.

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```
## <a name="related-video"></a>관련 동영상

> [!Video https://channel9.msdn.com/Series/NuGet-101/Install-and-Use-a-NuGet-Package-with-the-NET-CLI-3-of-5/player]

[Channel 9](https://channel9.msdn.com/Series/NuGet-101) 및 [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_)에서 더 많은 NuGet 비디오를 확인하세요.

## <a name="next-steps"></a>다음 단계

첫 번째 NuGet 패키지를 설치하고 사용하시게 된 것을 축하드립니다.

> [!div class="nextstepaction"]
> [dotnet CLI를 사용하여 패키지 설치 및 사용](../consume-packages/install-use-packages-dotnet-cli.md)

NuGet에서 제공하는 다른 기능을 탐색하려면 아래 링크를 선택합니다.

- [패키지 사용 개요 및 워크플로](../consume-packages/overview-and-workflow.md)
- [패키지 찾기 및 선택](../consume-packages/finding-and-choosing-packages.md)
- [프로젝트 파일의 패키지 참조](../consume-packages/package-references-in-project-files.md)
