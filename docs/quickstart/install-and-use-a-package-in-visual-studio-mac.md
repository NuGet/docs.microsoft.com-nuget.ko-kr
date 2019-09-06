---
title: Mac용 Visual Studio에서 NuGet 패키지 설치 및 사용
description: Mac용 Visual Studio 프로젝트에서 NuGet 패키지를 설치하고 사용하는 프로세스에 대한 연습 자습서입니다.
author: jmatthiesen
ms.author: jomatthi
ms.date: 08/14/2019
ms.topic: quickstart
ms.openlocfilehash: 6f3fd4f2ffec0037a48aec845fddee258b5c1e7f
ms.sourcegitcommit: ac9a00ccaf90e539a381e92b650074910b21eb0d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/03/2019
ms.locfileid: "70238479"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-for-mac"></a>빠른 시작: Mac용 Visual Studio에서 패키지 설치 및 사용

NuGet 패키지는 다른 개발자가 프로젝트에서 사용하기 위해 제공하는 다시 사용할 수 있는 코드를 포함합니다. 배경 지식은 [NuGet이란?](../What-is-NuGet.md)을 참조하세요. 패키지는 NuGet 패키지 관리자를 사용하여 Mac용 Visual Studio 프로젝트에 설치됩니다. 이 문서에서는 널리 사용되는 [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) 패키지 및.NET Core 콘솔 프로젝트를 사용하는 프로세스를 보여줍니다. 기타 모든 Xamarin 또는 .NET Core 프로젝트에 같은 프로세스가 적용됩니다.

패키지가 설치되면 `using <namespace>`를 사용하여 코드에서 패키지를 참조합니다. 여기서 \<네임스페이스\>는 사용 중인 패키지에 특정됩니다. 일단 참조를 만들면 해당 API를 통해 패키지를 호출할 수 있습니다.

> [!Tip]
> **nuget.org 시작**: *nuget.org* 검색은 일반적으로 .NET 개발자가 고유의 애플리케이션에서 다시 사용할 수 있는 구성 요소를 찾는 방법입니다. *nuget.org*를 직접 검색하거나 이 문서에 표시된 대로 Visual Studio 내에서 패키지를 설치할 수 있습니다. 일반 정보는 [NuGet 패키지 찾기 및 평가](../consume-packages/finding-and-choosing-packages.md)를 참조하세요.

## <a name="prerequisites"></a>전제 조건

- Mac용 Visual Studio 2019.

[visualstudio.com](https://www.visualstudio.com/)에서 추가 비용 없이 2019 Community 버전을 설치하거나 Professional 또는 Enterprise 버전을 사용할 수 있습니다.

Windows에서 Visual Studio를 사용하는 경우 [Visual Studio에서 패키지 설치 및 사용(Windows만 해당)](install-and-use-a-package-in-visual-studio.md)을 참조하세요.

## <a name="create-a-project"></a>프로젝트 만들기

NuGet 패키지는 패키지가 프로젝트와 동일한 대상 프레임워크를 지원하는 경우 어느 .NET 프로젝트에나 설치할 수 있습니다.

이 연습에서는 간단한 .NET Core 콘솔 앱을 사용합니다. Mac용 Visual Studio에서 **파일 > 새 솔루션**을 클릭하여 프로젝트를 만들고 **.NET Core > 앱 > 콘솔 응용 프로그램** 템플릿을 선택합니다. **다음**을 클릭합니다. 메시지가 표시되면 **대상 프레임워크**의 기본값을 그대로 적용합니다.

Visual Studio에서 프로젝트를 만들고 솔루션 탐색기에서 열립니다.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Newtonsoft.Json NuGet 패키지 추가

패키지를 설치하려면 NuGet 패키지 관리자를 사용합니다. 패키지를 설치하면 NuGet에서 프로젝트 파일 또는 `packages.config` 파일에 종속성을 기록합니다(프로젝트 형식에 따라). 자세한 내용은 [패키지 소비 개요 및 워크플로](../consume-packages/Overview-and-Workflow.md)를 참조하세요.

### <a name="nuget-package-manager"></a>NuGet 패키지 관리자

1. 솔루션 탐색기에서 **종속성**을 마우스 오른쪽 단추로 클릭하고 **패키지 추가**를 선택합니다.

    ![프로젝트 참조에 대한 NuGet 패키지 관리 명령](media/QS_Use_Mac-02-ManageNuGetPackages.png)

1. 대화 상자의 왼쪽 위 모서리에서 **패키지 원본**으로 "nuget.org"를 선택하고 **Newtonsoft.Json**을 검색하여 목록에서 해당 패키지를 선택한 다음 **패키지 추가**를 선택합니다.

    ![Newtonsoft.Json 패키지 찾기](media/QS_Use_Mac-03-NewtonsoftJson.png)

    NuGet 패키지 관리자에 대한 자세한 내용은 [Mac용 Visual Studio를 사용하여 패키지 설치 및 관리](../consume-packages/install-use-packages-visual-studio.md)를 참조하세요.

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>앱에서 Newtonsoft.Json API 사용

프로젝트의 Newtonsoft.Json 패키지에서 해당 `JsonConvert.SerializeObject` 메서드를 호출하여 개체를 사람이 인식할 수 있는 문자열로 변환할 수 있습니다.

1. `Program.cs` 파일(Solution Pad에 있음)을 열고 파일 내용을 다음 코드로 바꿉니다.

    ```cs
    using System;
    using Newtonsoft.Json;

    namespace NuGetDemo
    {
        public class Account
        {
            public string Name { get; set; }
            public string Email { get; set; }
            public DateTime DOB { get; set; }
        }
    
        class Program
        {
            static void Main(string[] args)
            {
                Account account = new Account()
                {
                    Name = "Joe Doe",
                    Email = "joe@test.com",
                    DOB = new DateTime(1976, 3, 24)
                };
                string json = JsonConvert.SerializeObject(account);
                Console.WriteLine(json);
            }
        }
    }
    ```

1. **실행 > 디버깅 시작**을 선택하여 앱을 빌드하고 실행합니다.

1. 앱이 실행되면 직렬화된 JSON 출력이 콘솔에 표시됩니다.

  ![콘솔 앱의 출력](media/QS_Use_Mac-06-AppStart.png)

## <a name="next-steps"></a>다음 단계
첫 번째 NuGet 패키지를 설치하고 사용하시게 된 것을 축하드립니다.

> [!div class="nextstepaction"]
> [Mac용 Visual Studio를 사용하여 패키지 설치 및 관리](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json)

NuGet에서 제공하는 다른 기능을 탐색하려면 아래 링크를 선택합니다.

- [패키지 사용 개요 및 워크플로](../consume-packages/overview-and-workflow.md)
- [프로젝트 파일의 패키지 참조](../consume-packages/package-references-in-project-files.md)
