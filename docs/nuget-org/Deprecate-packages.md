---
title: nuget.org의 패키지 사용 중단
description: 패키지 사용 중단 프로세스 및 클라이언트에서 이 정보를 표시하는 방법에 대한 자세한 설명
author: anangaur
ms.author: anangaur
ms.date: 09/23/2019
ms.topic: conceptual
ms.reviewer: karann-msft
ms.openlocfilehash: 4a6dbd645cb72b0085fd0347def58ade134fc5ee
ms.sourcegitcommit: 5f706c62c97b78bbe3d8c7e95659976535fe486f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/23/2021
ms.locfileid: "122726966"
---
# <a name="deprecating-packages"></a>패키지 사용 중단

더 이상 패키지를 유지 관리하지 않거나 패키지 소비자에게 다른 패키지로 이동하도록 권장하려는 경우 패키지를 사용 중단할 수 있습니다. 

패키지 사용 중단은 아래 설명대로 패키지를 **제외** 하는 것과 다릅니다.
* 패키지를 **제외** 하면 패키지는 검색 결과에서 숨겨지므로 검색되지 않습니다. 
* 패키지를 **사용 중단** 하면 기존 소비자는 패키지가 설치되어 있는지 또는 프로젝트에 사용되고 있는지 여부를 확인할 수 있습니다. 또한 사용 중단 이유 및 패키지 게시자가 지정한 대체 권장 패키지를 알 수 있습니다. 패키지를 사용 중단하는 것은 패키지를 제외하는 것이 아닙니다. 

게시자는 패키지 제외와 사용 중단을 둘 다 선택할 수 있습니다.

## <a name="deprecation-workflow"></a>사용 중단 워크플로
1. 패키지를 사용 중단하려면 **패키지 관리** 로 이동하여 **사용 중단** 을 선택합니다.

    ![패키지 사용 중단 옵션으로 이동](media/deprecation-select-option.png)

2. 사용 중단할 버전을 선택합니다. 모든 버전을 사용 중단하려면 **모든 버전 선택** 옵션을 선택합니다.

    ![사용 중단할 패키지 버전 선택](media/deprecation-select-version.png)

3. 사용 중단 이유를 선택합니다. 패키지가 더 이상 유지 관리되지 않으면 **레거시** 옵션을 선택합니다. 특정 버전에 중요한 버그가 있는 경우 **중요한 버그 있음** 옵션을 선택합니다. 다른 이유인 경우에는 **기타** 를 선택합니다. 언제든지 대체 권장 패키지(및 버전) 및 소유자에 대한 사용자 지정 메시지를 지정할 수 있습니다. 

    ![대체 패키지 권장 사항 및 사용자 지정 메시지를 선택합니다.](media/deprecation-save.png)

> [!Note]
> 사용자 지정 메시지는 nuget.org에만 표시되고 클라이언트에서는 표시되지 않습니다. 현재 `dotnet.exe` 및 NuGet 패키지 관리자와 같은 클라이언트는 사용자 지정 메시지를 표시하지 않습니다.

## <a name="client-experience-for-deprecated-packages"></a>사용 중단된 패키지에 대한 클라이언트 환경
패키지가 사용 중단된 경우 해당 고객에게는 사용된 클라이언트에 따라 다음과 같은 방법으로 이에 대한 알림이 표시됩니다.

### <a name="visual-studio"></a>Visual Studio 
*Visual Studio 2019 버전 16.3부터 사용 가능*

Visual Studio는 `Installed` 탭에서 사용되지 않는 패키지의 사용에 대해 경고합니다. 패키지와 사용 중단 정보(사용되지 않는 이유 및 대신 사용할 대체 패키지(있는 경우) 포함)에 대한 경고를 표시합니다.

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

## <a name="transfer-popularity-to-a-newer-package"></a>최신 패키지로 인기도 이전

레거시 패키지가 사용 중단되도록 한 패키지 작성자는 “인기도”를 최신 패키지로 이전하여 최신 패키지의 검색 순위를 높일 수 있습니다. 그러면 고객은 사용되지 않는 패키지 대신 최신 패키지를 검색할 수 있습니다.

예를 들어 다음과 같은 두 개의 패키지가 있다고 가정합니다.

* 3백만 번 다운로드된 사용되지 않는 레거시 패키지 `Contoso.Legacy`
* 5번 다운로드된 최신 패키지 `Contoso.Latest`

NuGet.org는 다운로드 횟수/인기도가 더 높은 검색 결과를 선호합니다. 검색 쿼리 “Contoso”가 사용된 경우 검색 결과에서 사용되지 않는 패키지 `Contoso.Legacy`가 최신 패키지 `Contoso.Latest`보다 높은 순위에 위치합니다.

이 문제를 해결하기 위해 사용되지 않는 레거시 패키지의 인기도가 최신 패키지로 이전되도록 신청할 수 있습니다. 그러면 검색 결과에서 `Contoso.Latest`의 순위가 높아지고 `Contoso.Legacy`의 순위는 낮아집니다. 패키지의 내부 인기도 점수에만 영향이 있고 각 패키지의 실제 다운로드 횟수에는 영향이 없습니다.

> [!Note]
> 인기도 이전을 사용하면 소비자가 레거시 패키지를 찾기가 훨씬 더 어렵게 할 수 있습니다.

인기도 이전이 “Contoso” 쿼리의 검색 순위에 영향을 미치는 방식을 구체적으로 파악하려면 아래 표를 참조하세요.

| 검색 순위    | 인기도 이전 전        | 인기도 이전 후         |
|----------------   |--------------------------------   |--------------------------------   |
| 1                 | Contoso.Legacy, 3백만 번 다운로드됨    | Contoso.Latest, 5번 다운로드됨     |
| 2                 | Contoso.Scanner, 2백만 번 다운로드됨     | Contoso.Scanner, 2백만 번 다운로드됨     |
| 3                 | Contoso.Core, 150만 번 다운로드됨     | Contoso.Core, 150만 번 다운로드됨     |
| 4                 | Contoso.UI, 1백만 번 다운로드됨          | Contoso.UI, 1백만 번 다운로드됨          |
| ...               | ...                               | ...                               |
| 20                | Contoso.Latest, 5번 다운로드됨     | Contoso.Legacy, 3백만 번 다운로드됨    |

### <a name="popularity-transfer-application-process"></a>인기도 이전 신청 프로세스

1. [인기도 이전 요구 사항](#popularity-transfer-requirements)을 검토합니다.
2. 인기도를 이전해야 하는 사용되지 않는 패키지와 인기도 이전을 받아야 하는 안정적인 패키지의 목록을 포함하여 [account@nuget.org](mailto:account@nuget.org)로 전자 메일을 보냅니다.

신청이 제출된 후에는 신청의 승인 또는 거부에 대해 알려드립니다(거부하게 된 기준 포함). 소유자 ID를 확인하기 위해 추가적인 식별 질문을 할 수도 있습니다.

#### <a name="popularity-transfer-requirements"></a>인기도 이전 요구 사항

* 레거시 패키지와 새 패키지가 모든 소유자를 공유해야 합니다.
* 새 패키지는 명명 및 기능(즉, 개선 또는 차세대) 측면에서 레거시 패키지와 명확하게 관련되어야 합니다.
* 모든 버전의 레거시 패키지는 더 이상 사용되지 않으며 이전을 받는 새 패키지를 가리켜야 합니다.
* 인기도 이전은 NuGet 사용자의 혼동을 일으키거나 NuGet 검색 환경을 악화시키지 않아야 합니다.
* 새 패키지에는 안정적인 버전이 포함되어야 합니다.
* 레거시 패키지는 사용되지 않는 다른 패키지의 인기도 이전을 받아서는 안 됩니다.

### <a name="advanced-popularity-transfer-scenarios"></a>고급 인기도 이전 시나리오

#### <a name="package-consolidations"></a>패키지 통합

사용되지 않는 여러 패키지의 인기도를 단일 새 패키지로 이전할 수 있습니다. 예를 들어 다음과 같은 3개의 패키지가 있다고 가정합니다.

* 사용되지 않는 첫 번째 레거시 패키지 `Contoso.Legacy1`
* 사용되지 않는 두 번째 레거시 패키지 `Contoso.Legacy2`
* 새 통합 패키지 `Contoso.Latest`

`Contoso.Legacy1`과 `Contoso.Legacy2`를 사용 중단되도록 한 후 `Contoso.Latest`로 인기도가 이전되도록 신청할 수 있습니다.

#### <a name="package-splits"></a>패키지 분할

사용되지 않는 패키지의 인기도는 최대 5개의 최신 패키지로 이전 및 분할할 수 있습니다. 이 기능은 사용되지 않는 패키지의 기능이 여러 새 패키지 간에 분할된 경우에 유용합니다. 예를 들어 다음과 같은 3개의 패키지가 있다고 가정합니다.

* 사용되지 않는 레거시 패키지 `Contoso.Legacy`
* 첫 번째 새 패키지 `Contoso.Web`
* 두 번째 새 패키지 `Contoso.Cloud`

`Contoso.Legacy`에는 웹 기능과 클라우드 기능이 모두 포함되어 있지만, 차세대의 경우 해당 기능을 여러 패키지로 분리하기로 했습니다. `Contoso.Legacy`를 사용 중단되도록 한 후 해당 인기도가 `Contoso.Web`과 `Contoso.Cloud` 둘 다에 이전되도록 신청할 수 있습니다.

> [!Warning]
> 이전된 인기도는 모든 새 패키지 간에 균등하게 분할됩니다. 따라서 사용되지 않는 패키지의 인기도를 가능한 한 적은 수의 패키지로 이전하는 것이 좋습니다.

#### <a name="popularity-transfer-chains"></a>인기도 이전 체인

사용되지 않는 패키지가 사용되지 않는 다른 패키지의 인기도를 이미 받고 있는 경우 해당 인기도를 이전할 수 없습니다. 예를 들어 다음과 같은 3개의 패키지가 있다고 가정합니다.

* 사용되지 않는 레거시 패키지 `Contoso.First`
* 사용되지 않는 레거시 패키지 `Contoso.Second`
* 새 패키지 `Contoso.Latest`

`Contoso.First`의 인기도를 `Contoso.Second,`로 이전하면 `Contoso.Second`의 인기도를 `Contoso.Latest`로 이전할 수 없습니다. 대신 [패키지 통합](#package-consolidations) 시나리오에 따라 `Contoso.First`와 `Contoso.Second` 둘 다의 인기도를 `Contoso.Latest`로 이전하는 것이 좋습니다.
