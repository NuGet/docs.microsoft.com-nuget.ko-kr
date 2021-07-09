---
title: dotnet CLI를 사용하여 NuGet 패키지 설치 및 관리
description: dotnet CLI를 사용하여 NuGet 패키지를 작업하기 위한 지침입니다.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 62c05aad388c25120d5b9f5143017a2f4f3b276b
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323611"
---
# <a name="install-and-manage-packages-using-the-dotnet-cli"></a>dotnet CLI를 사용하여 패키지 설치 및 관리

CLI 도구를 사용하면 프로젝트 및 솔루션에서 NuGet 패키지를 쉽게 설치, 제거 및 업데이트할 수 있습니다. Windows, Mac OS X 및 Linux에서 실행됩니다.

dotnet CLI는 .NET Core, .NET Standard 프로젝트(SDK 스타일 프로젝트 형식) 및 기타 모든 SDK 스타일 프로젝트(예: .NET Framework를 대상으로 하는 SDK 스타일 프로젝트)에서 사용하기 위한 것입니다. 자세한 내용은 [SDK 특성](/dotnet/core/tools/csproj#additions)을 참조하세요.

이 문서에서는 가장 일반적인 몇 가지 dotnet CLI 명령에 대한 기본 사용법을 보여줍니다. 이러한 명령의 대부분의 경우 CLI 도구는 프로젝트 파일이 명령에 지정되지 않는 한 현재 디렉터리에서 프로젝트 파일을 찾습니다(프로젝트 파일은 선택적 스위치임). 사용할 수 있는 명령 및 인수의 전체 목록은 [.NET Core CLI (명령줄 인터페이스) 도구](../reference/dotnet-commands.md)를 참조하세요.

## <a name="prerequisites"></a>사전 요구 사항

- `dotnet` 명령줄 도구를 제공하는 [.NET Core SDK](https://www.microsoft.com/net/download/). Visual Studio 2017부터 dotnet CLI는 모든 .NET Core 관련 워크로드와 함께 자동으로 설치됩니다.

## <a name="install-a-package"></a>패키지 설치

[dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x)는 패키지 참조를 프로젝트 파일에 추가한 다음, `dotnet restore`를 추가하여 패키지를 설치합니다.

1. 명령줄을 열고 프로젝트 파일이 포함된 디렉터리로 전환합니다.

2. 다음 명령을 사용하여 NuGet 패키지를 설치합니다.

    ```dotnetcli
    dotnet add package <PACKAGE_NAME>
    ```

    예를 들어 `Newtonsoft.Json` 패키지를 설치하려면 다음 명령을 사용합니다.

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

3. 명령이 완료된 후 프로젝트 파일을 보고 패키지가 설치되었는지 확인합니다.

   `.csproj` 파일을 열어 추가된 참조를 볼 수 있습니다.

    ```xml
    <ItemGroup>
      <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
    </ItemGroup>
    ```

## <a name="install-a-specific-version-of-a-package"></a>특정 버전의 패키지 설치

버전이 지정되지 않은 경우 NuGet은 패키지의 최신 버전을 설치합니다. [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) 명령을 사용하여 특정 버전의 NuGet 패키지를 설치할 수도 있습니다.

```dotnetcli
dotnet add package <PACKAGE_NAME> --version <VERSION>
```

예를 들어 `Newtonsoft.Json` 패키지의 버전 12.0.1을 추가하려면 다음 명령을 사용합니다.

```dotnetcli
dotnet add package Newtonsoft.Json --version 12.0.1
```

## <a name="list-package-references"></a>패키지 참조 나열

[dotnet 목록 패키지](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) 명령을 사용하여 프로젝트의 패키지 참조를 나열할 수 있습니다.

```dotnetcli
dotnet list package
```

## <a name="remove-a-package"></a>패키지 제거

[dotnet remove package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) 명령을 사용하여 프로젝트 파일에서 패키지 참조를 제거합니다.

```dotnetcli
dotnet remove package <PACKAGE_NAME>
```

예를 들어 `Newtonsoft.Json` 패키지를 제거하려면 다음 명령을 사용합니다.

```dotnetcli
dotnet remove package Newtonsoft.Json
```

## <a name="update-a-package"></a>패키지 업데이트

패키지 버전을 지정하지 않는 한 `dotnet add package` 명령을 사용할 때 NuGet은 패키지의 최신 버전을 설치합니다(`-v` 스위치).

## <a name="restore-packages"></a>패키지 복원

[!INCLUDE [restore-dotnet-cli](includes/restore-dotnet-cli.md)]
