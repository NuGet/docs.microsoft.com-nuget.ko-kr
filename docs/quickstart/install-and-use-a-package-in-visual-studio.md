---
title: Visual Studio 내에서 NuGet 패키지 사용에 대한 소개 가이드
description: Visual Studio 프로젝트에서 NuGet 패키지를 설치하고 사용하는 프로세스에 대한 연습 자습서입니다.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 15268ae33d56042a765420e5076dac49db6cce04
ms.sourcegitcommit: 1591bb230e106b94162a87dd1d86fe427366730a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/30/2018
ms.locfileid: "52671177"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio"></a>빠른 시작: Visual Studio에서 패키지 설치 및 사용

NuGet 패키지는 다른 개발자가 프로젝트에서 사용하기 위해 제공하는 다시 사용할 수 있는 코드를 포함합니다. 배경 지식은 [NuGet이란?](../What-is-NuGet.md)을 참조하세요. 패키지는 패키지 관리자 UI 또는 패키지 관리자 콘솔을 사용하여 Visual Studio 프로젝트에 설치됩니다. 이 문서에서는 널리 사용되는 [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) 패키지 및 UWP(유니버설 Windows 플랫폼) 프로젝트를 사용하는 프로세스를 보여줍니다. 같은 프로세스가 다른 .NET 또는 .NET Core 프로젝트에 모두에 적용됩니다.

패키지가 설치되면 `using <namespace>`를 사용하여 코드에서 패키지를 참조합니다. 여기서 \<네임스페이스\>는 사용 중인 패키지에 특정됩니다. 일단 참조를 만들면 해당 API를 통해 패키지를 호출할 수 있습니다.

> [!Tip]
> **nuget.org 시작**: nuget.org 검색은 일반적으로 .NET 개발자가 고유의 응용 프로그램에서 다시 사용할 수 있는 구성 요소를 찾는 방법입니다. nuget.org를 직접 검색하거나 이 문서에 표시된 대로 Visual Studio 내에서 패키지를 설치할 수 있습니다.

## <a name="prerequisites"></a>전제 조건

- Visual Studio 2017(유니버설 Windows 플랫폼 개발 워크로드 포함) 또는
- Visual Studio 2015 업데이트 3(유니버설 Windows 앱용 도구 포함).

[visualstudio.com](https://www.visualstudio.com/)에서 추가 비용 없이 2017 Community 버전을 설치하거나 Professional 또는 Enterprise 버전을 사용할 수 있습니다.

## <a name="create-a-project"></a>프로젝트 만들기

NuGet 패키지는 패키지가 프로젝트와 동일한 대상 프레임워크를 지원하는 경우 어느 .NET 프로젝트에나 설치할 수 있습니다.

이 연습에서는 간단한 유니버설 Windows(UWP) 앱을 사용합니다. **파일 > 새 프로젝트...** 를 사용하고 **Windows 유니버설 > 빈 앱(유니버설 Windows)** 을 선택하여 Visual Studio에서 프로젝트를 만듭니다. 메시지가 표시되면 대상 버전 및 최소 버전에 대한 기본값을 적용합니다.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Newtonsoft.Json NuGet 패키지 추가

패키지를 설치하는 데는 패키지 관리자 UI 또는 패키지 관리자 콘솔을 사용할 수 있습니다. 패키지를 설치하면 NuGet에서 프로젝트 파일 또는 `packages.config` 파일에 종속성을 기록합니다. 자세한 내용은 [패키지 소비 개요 및 워크플로](../consume-packages/Overview-and-Workflow.md)를 참조하세요.

### <a name="package-manager-ui"></a>패키지 관리자 UI

1. 솔루션 탐색기에서 **참조**를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리**를 선택합니다.

    ![프로젝트 참조에 대한 NuGet 패키지 관리 명령](media/QS_Use-02-ManageNuGetPackages.png)

1. "nuget.org"를 **패키지 원본**으로 선택하고, **찾아보기** 탭을 선택하고, **Newtonsoft.Json**을 검색하고, 목록에서 해당 패키지를 선택하고, **설치**를 선택합니다.

    ![Newtonsoft.Json 패키지 찾기](media/QS_Use-03-NewtonsoftJson.png)

1. 라이선스 프롬프트를 수락합니다.

1. (Visual Studio 2017) 패키지 관리 형식을 선택하라는 메시지가 표시되면 **프로젝트 파일에서 PackageReference**를 선택합니다.

    ![패키지 관리 형식 선택](media/QS_Use-03b-SelectFormat.png)

1. 변경 내용을 검토하라는 메시지가 표시되면 **확인**을 선택합니다.

### <a name="package-manager-console"></a>패키지 관리자 콘솔

1. **도구 > NuGet 패키지 관리자 > 패키지 관리자 콘솔** 메뉴 명령을 선택합니다.

1. 콘솔이 열리면 **기본 프로젝트** 드롭다운 목록에 패키지를 설치할 프로젝트가 표시되는지 확인합니다. 솔루션에 단일 프로젝트가 있는 경우 이미 선택되어 있습니다.

    ![Newtonsoft.Json 패키지 찾기](media/QS_Use-08-Console1.png)

1. `Install-Package Newtonsoft.Json` 명령을 입력합니다([Install-Package](../tools/ps-ref-install-package.md) 참조). 콘솔 창은 명령에 대한 출력을 표시합니다. 일반적으로 오류는 패키지가 프로젝트의 대상 프레임워크와 호환되지 않음을 나타냅니다.

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>앱에서 Newtonsoft.Json API 사용

프로젝트의 Newtonsoft.Json 패키지에서 해당 `JsonConvert.SerializeObject` 메서드를 호출하여 개체를 사람이 인식할 수 있는 문자열로 변환할 수 있습니다.

1. `MainPage.xaml`을 열고 기존 `Grid` 요소를 다음과 같이 바꿉니다.

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. `MainPage.xaml.cs` 파일(`MainPage.xaml` 노드 아래의 솔루션 탐색기에 있음)을 열고 `MainPage` 생성자 내부에 다음 코드를 삽입합니다.

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }

    private void Button_Click(object sender, RoutedEventArgs e)
    {
        Account account = new Account
        {
            Name = "John Doe",
            Email = "john@microsoft.com",
            DOB = new DateTime(1980, 2, 20, 0, 0, 0, DateTimeKind.Utc),
        };
        string json = JsonConvert.SerializeObject(account, Formatting.Indented);
        TextBlock.Text = json;
    }
    ```

1. Newtonsoft.Json 패키지를 프로젝트에 추가했더라도 코드 파일 맨 위에 `using` 문이 필요한 경우 `JsonConvert` 아래에 빨간색 물결선이 나타납니다.

    ```cs
    using Newtonsoft.Json;
    ```

1. F5 키를 누르거나 **디버그 > 디버깅 시작**을 선택하여 앱을 빌드하고 실행합니다.

    ![UWP 앱의 초기 출력](media/QS_Use-06-AppStart.png)

1. JSON 텍스트로 바꾼 텍스트 블록의 내용을 보려면 단추를 선택합니다.

    ![단추를 선택한 후 UWP 앱의 출력](media/QS_Use-07-AppEnd.png)

## <a name="related-articles"></a>관련 문서

- [패키지 사용 개요 및 워크플로](../consume-packages/overview-and-workflow.md)
- [패키지 찾기 및 선택](../consume-packages/finding-and-choosing-packages.md)
- [패키지 설치 방법](../consume-packages/ways-to-install-a-package.md)
- [NuGet 동작 구성](../consume-packages/configuring-nuget-behavior.md)
