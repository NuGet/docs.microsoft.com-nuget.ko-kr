---
title: "NuGet 패키지 사용에 대한 소개 가이드 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/04/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: f31f8259-20a8-4617-880e-5819299372d2
description: "프로젝트에서 NuGet 패키지를 설치하고 사용하는 프로세스에 대한 연습 자습서입니다."
keywords: "NuGet 설치, NuGet 패키지 사용, NuGet 패키지 설치, NuGet 패키지 참조, NuGet 패키지 사용"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: bcccc7139de31a8d07e9ed52abfd12fe9e6d687b
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="install-and-use-a-package"></a>패키지 설치 및 사용

[!INCLUDE [install-methods](../includes/install-methods.md)]

패키지가 설치되면 `using <namespace>`를 사용하여 코드에서 패키지를 참조합니다. 여기서 \<네임스페이스\>는 사용 중인 패키지에 특정됩니다. 일단 참조를 만들면 해당 API를 통해 패키지를 호출할 수 있습니다.

이 항목의 나머지 부분에서는 패키지 관리자 UI를 사용하여 UWP(유니버설 Windows 플랫폼)에서 널리 사용되는 [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) 패키지를 설치하는 프로세스를 설명합니다. 그런 다음 패키지를 사용하는 예를 보여줍니다. 프로젝트에서 사용한 거의 모든 NuGet 패키지에 유사하고 동일한 워크플로를 사용합니다.

- [필수 구성 요소 설치](#install-pre-requisites)
- [프로젝트 만들기](#create-a-project)
- [Newtonsoft.Json NuGet 패키지 추가](#add-the-newtonsoftjson-nuget-package)
- [앱에서 Newtonsoft.Json API 사용](#use-the-newtonsoftjson-api-in-the-app)

> [!Tip]
> **nuget.org 시작**: nuget.org에서 패키지를 설치하는 작업은 .NET 개발자가 고유의 응용 프로그램에서 다시 사용할 수 있는 구성 요소를 찾는 데 사용하는 일반적인 워크플로입니다. 항상 nuget.org를 직접 검색하거나 이 항목에 표시된 대로 Visual Studio 내에서 패키지를 설치할 수 있습니다.

## <a name="install-pre-requisites"></a>필수 구성 요소 설치

이 자습서에는 유니버설 Windows 앱용 도구와 함께 Visual Studio 2015 업데이트 3 또는 유니버설 Windows 플랫폼 개발 워크로드와 함께 Visual Studio 2017이 필요합니다. Visual Studio가 이미 설치되어 있으면 설치 프로그램을 다시 실행하여 UWP 도구를 추가할 수 있습니다.

[visualstudio.com](https://www.visualstudio.com/)에서 추가 비용 없이 Community 버전을 설치하거나 Professional 또는 Enterprise 버전을 사용할 수 있습니다. 

## <a name="create-a-project"></a>프로젝트 만들기

NuGet 패키지를 설치하려면 Visual Studio에서 일부 .NET 기반 프로젝트가 필요합니다. 이 연습에서는 간단한 WPF(Windows Presentation Foundation) 또는 UWP(유니버설 Windows) 앱을 사용할 수 있습니다.

- WPF(Windows 7 이상)의 경우 **파일 > 새로 만들기 > 프로젝트**를 선택하고, **Visual C#**을 확장하고, **Windows 클래식 데스크톱 > WPF 앱(.NET Framework)**을 선택하고, **확인**을 선택합니다.
- UWP(Windows 10)의 경우 대신 **Windows 유니버설 > 비어 있는 앱(유니버설 Windows)**을 사용합니다. 메시지가 표시되면 대상 버전 및 최소 버전에 대한 기본값을 적용합니다.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Newtonsoft.Json NuGet 패키지 추가

1. 솔루션 탐색기에서 **참조**를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리**를 선택합니다.

    ![프로젝트 참조에 대한 NuGet 패키지 관리 명령](media/QS_Use-02-ManageNuGetPackages.png)

1. "nuget.org"를 **패키지 원본**으로 선택하고, **찾아보기** 탭을 선택하고, **Newtonsoft.Json**을 검색하고, 목록에서 해당 패키지를 선택하고, **설치**를 선택합니다.

    ![Newtonsoft.Json 패키지 찾기](media/QS_Use-03-NewtonsoftJson.png)

1. 패키지 관리 형식을 선택하라는 메시지가 표시되면 PackageReference(권장)와 `packages.config` 중에서 선택합니다.

    ![패키지 참조 형식 선택](media/QS_Use-03b-SelectFormat.png)

1. 변경 내용을 검토하라는 메시지가 표시되면 **확인**을 선택합니다.

1. 솔루션 탐색기에서 솔루션을 마우스 오른쪽 단추로 클릭하고 **솔루션 빌드**를 선택합니다. 이렇게 하면 **참조** 아래에 나열된 NuGet 패키지를 복원합니다. 자세한 내용은 [패키지 복원](../consume-packages/package-restore.md)을 참조하세요.

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>앱에서 Newtonsoft.Json API 사용

프로젝트의 Newtonsoft.Json 패키지에서 해당 `JsonConvert.SerializeObject` 메서드를 호출하여 개체를 사람이 인식할 수 있는 문자열로 변환할 수 있습니다.

1. `MainWindow.xaml`(WPF) 또는 `MainPage.xaml`(UWP)을 열고 기존 `Grid` 요소를 다음으로 바꿉니다.

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. 솔루션 탐색기에서 `MainWindow.xaml`(WPF) 또는 `MainPage.xaml`(UWP) 노드를 확장하고, `.cs` 파일을 열고, `MainWindow` 또는 `MainPage` 클래스 내의 생성자 뒤에 다음 코드를 삽입합니다.

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

1. Newtonsoft.Json 패키지를 프로젝트에 추가했더라도 `using` 문이 필요한 경우 `JsonConvert` 아래에 빨간색 물결선이 나타납니다. 밑줄이 그어진 `JsonConvert` 위로 마우스를 가져가면 전구 및 **잠재적 수정 사항 표시**에 대한 옵션이 표시됩니다.

    ![잠재적 수정 사항 표시 명령이 포함된 전구](media/QS_Use-04-ShowPotentialFixes.png)


1. **잠재적 수정 사항 표시**(또는 전구)를 클릭하고 첫 번째 제안된 수정 사항 `using Newtonsoft.Json;`을 선택합니다. 그러면 이 파일의 맨 위에 필요한 줄을 추가합니다.

    ![using 문을 추가하는 옵션을 제공하는 전구](media/QS_Use-05-AddUsing.png)

1. F5 키를 누르거나 **디버그 > 디버깅 시작**(여기에 표시된 UWP, WPF는 유사함)을 선택하여 앱을 빌드하고 실행합니다.

    ![UWP 앱의 초기 출력](media/QS_Use-06-AppStart.png)

1. JSON 텍스트로 바꾼 텍스트 블록의 내용을 보려면 단추를 선택합니다.

    ![단추를 선택한 후 UWP 앱의 출력](media/QS_Use-07-AppEnd.png)

## <a name="related-topics"></a>관련 항목

- [패키지 사용 개요 및 워크플로](../consume-packages/overview-and-workflow.md)
- [패키지 찾기 및 선택](../consume-packages/finding-and-choosing-packages.md)
- [NuGet 동작 구성](../consume-packages/configuring-nuget-behavior.md)
