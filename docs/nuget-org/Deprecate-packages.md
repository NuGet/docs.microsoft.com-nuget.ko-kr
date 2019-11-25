---
title: nuget.org의 패키지 사용 중단
description: 패키지 사용 중단 프로세스 및 클라이언트에서 이 정보를 표시하는 방법에 대한 자세한 설명
author: anangaur
ms.author: anangaur
ms.date: 09/23/2019
ms.topic: conceptual
ms.reviewer: karann-msft
ms.openlocfilehash: 70666ddf9cd7bdc448d29d4235e57bc91e2c003e
ms.sourcegitcommit: 60414a17af65237652c1de9926475a74856b91cc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/14/2019
ms.locfileid: "74096878"
---
# <a name="deprecating-packages"></a>패키지 사용 중단

더 이상 패키지를 유지 관리하지 않거나 패키지 소비자에게 다른 패키지로 이동하도록 권장하려는 경우 패키지를 사용 중단할 수 있습니다. 

패키지 사용 중단은 아래 설명대로 패키지를 **제외**하는 것과 다릅니다.
* 패키지를 **제외**하면 패키지는 검색 결과에서 숨겨지므로 검색되지 않습니다. 
* 패키지를 **사용 중단**하면 기존 소비자는 패키지가 설치되어 있는지 또는 프로젝트에 사용되고 있는지 여부를 확인할 수 있습니다. 또한 사용 중단 이유 및 패키지 게시자가 지정한 대체 권장 패키지를 알 수 있습니다. 패키지를 사용 중단하는 것은 패키지를 제외하는 것이 아닙니다. 

게시자는 패키지 제외와 사용 중단을 둘 다 선택할 수 있습니다.

## <a name="deprecation-workflow"></a>사용 중단 워크플로
1. 패키지를 사용 중단하려면 **패키지 관리**로 이동하여 **사용 중단**을 선택합니다.

    ![패키지 사용 중단 옵션으로 이동](media/deprecation-select-option.png)

2. 사용 중단할 버전을 선택합니다. 모든 버전을 사용 중단하려면 **모든 버전 선택** 옵션을 선택합니다.

    ![사용 중단할 패키지 버전 선택](media/deprecation-select-version.png)

3. 사용 중단 이유를 선택합니다. 패키지가 더 이상 유지 관리되지 않으면 **레거시** 옵션을 선택합니다. 특정 버전에 중요한 버그가 있는 경우 **중요한 버그 있음** 옵션을 선택합니다. 다른 이유인 경우에는 **기타**를 선택합니다. 언제든지 대체 권장 패키지(및 버전) 및 소유자에 대한 사용자 지정 메시지를 지정할 수 있습니다. 

    ![대체 패키지 권장 사항 및 사용자 지정 메시지를 선택합니다.](media/deprecation-save.png)

> [!Note]
> 사용자 지정 메시지는 nuget.org에만 표시되고 클라이언트에서는 표시되지 않습니다. 현재 `dotnet.exe` 및 NuGet 패키지 관리자와 같은 클라이언트는 사용자 지정 메시지를 표시하지 않습니다.

## <a name="client-experience-for-deprecated-packages"></a>사용 중단된 패키지에 대한 클라이언트 환경
패키지가 사용 중단된 경우 해당 고객에게는 사용된 클라이언트에 따라 다음과 같은 방법으로 이에 대한 알림이 표시됩니다.

### <a name="visual-studio"></a>Visual Studio 
*Visual Studio 2019 버전 16.3부터 사용 가능*

Visual Studio는 `Installed` 탭에서 사용되지 않는 패키지의 사용에 대해 경고합니다. 패키지와 사용 중단 정보(사용되지 않는 이유 및 대신 사용할 대체 패키지(있는 경우) 포함)에 대한 경고가 표시됩니다.

   ![패키지 관리자의 Visual Studio 설치 탭에서 사용되지 않는 패키지](media/deprecation-vs.png)

### <a name="dotnetexe"></a>dotnet.exe
*.NET SDK 3.0부터 사용 가능*

dotnet.exe를 사용하는 경우 솔루션 또는 프로젝트 폴더에 대해 `dotnet list package --deprecated` 명령을 실행하여 사용 중단 정보와 함께 사용되지 않는 패키지의 목록을 가져올 수 있습니다.

```
> dotnet list package --deprecated

The following sources were used:
   https://api.nuget.org/v3/index.json

Project `My.Test.Project` has the following deprecated packages
   [netcoreapp3.0]:
   Top-level Package      Resolved   Reason(s)   Alternative
   > My.Sample.Lib        6.0.0      Legacy      My.Awesome.Package

```
