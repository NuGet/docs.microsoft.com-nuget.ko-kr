---
title: ID 접두사 예약
description: 패키지 ID 접두사 예약 기능 설명 및 작성자 가이드.
author: JonDouglas
ms.author: jodou
ms.date: 09/07/2019
ms.topic: reference
ms.reviewer: karann
ms.openlocfilehash: af9969df33c6bf7a62709e6e3535b8b886376e3e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775926"
---
# <a name="package-id-prefix-reservation"></a>패키지 ID 접두사 예약

패키지 소유자는 ID 접두사를 예약하여 해당 ID를 예약하고 보호할 수 있습니다. 패키지 소비자는 사용하는 패키지가 식별되는 속성에서 기만적이지 않을 때 추가 정보를 제공받습니다. 

[nuget.org](https://www.nuget.org/) 및 Visual Studio 2017 버전 15.4 이상에서는 패키지가 예약된 ID 접두사 명명 패턴과 일치하는 한 예약된 패키지 ID 접두사가 있는 소유자가 제출한 패키지에 대한 시각적 표시기를 보여줍니다. 아래 참조에서는 ID 접두사 예약 시 내용과 소유자가 ID 접두사에 대한 적용 방법을 설명합니다.

## <a name="id-prefix-reservation-details"></a>ID 접두사 예약 세부 정보

패키지 ID 접두사가 예약되면 [nuget.org](https://www.nuget.org/) 갤러리와 Visual Studio에서 여러 가지 일이 발생합니다. 또한 접두사를 'public'으로 설정하고 접두사를 여러 소유자에게 위임하는 등 ID 접두사 예약에 의해 지원되는 고급 시나리오가 있습니다.

### <a name="id-prefix-reservation-on-nugetorg"></a>nuget.org에 ID 접두사 예약

접두사가 [nuget.org](https://www.nuget.org/)에 예약되어 있으면 다음과 같은 현상이 발생합니다.

1. 접두사 예약은 [nuget.org](https://www.nuget.org/)의 소유자 또는 소유자 세트와 연결됩니다.

1. 예약된 ID 접두사와 일치하는 ID가 있는 패키지를 [nuget.org](https://www.nuget.org/)에 제출할 때마다 해당 패키지가 ID 접두사를 예약한 소유자로부터 생성되지 않은 한 거부됩니다.

1. 예약된 ID 접두사와 일치하고 ID 접두사를 예약한 소유자로부터 생성된 모든 패키지는 Visual Studio 2017 버전 15.4 이상 및 [nuget.org](https://www.nuget.org/)에 패키지가 예약된 ID 접두사 아래에 있음을 나타내는 시각적 표시시가 있습니다. 이는 소유자의 기존 패키지뿐만 아니라 새 패키지 제출 모두에 해당됩니다. **참고:** Visual Studio의 표시기는 단일 피드를 패키지 원본으로 선택한 경우에만 나타납니다.

1. 예약된 ID 접두사와 일치하지만 예약된 접두사 소유자가 소유하지 *않은* 기존의 모든 패키지는 변경되지 않은 상태로 유지됩니다(비공개는 아니지만 시각적 표시기가 없을 수도 있음). 또한 이러한 패키지의 소유자는 패키지에 새 버전을 계속 제출할 수 있습니다.

이러한 변경 내용은 다음 조건을 기반으로 몇 가지 추가 제한 사항이 적용됩니다.

- 패키지의 한 소유자만 시각적 표시기가 표시되도록 예약된 접두사를 가져야 합니다(여러 소유자가 있는 패키지의 경우).

- 하나 이상의 소유자가 예약된 접두사를 가지고 있고, 하나 이상의 소유자가 예약된 접두사를 가지고 있지 않은 패키지의 소유자가 둘 이상이 있는 경우, 예약된 접두사를 가진 소유자만 예약된 접두사를 가진 다른 소유자를 제거할 수 있습니다. 예약된 접두사가 없는 소유자는 해당 접두사가 예약된 소유자를 제거할 수 없습니다. 예약된 접두사를 갖고 있지 않은 다른 소유자를 여전히 제거할 수도 있습니다.

- 패키지에 시각적 표시기가 있으면 *항상* 시각적 표시기가 있어야 합니다(예약된 접두사를 가진 하나 이상의 소유자가 항상 소유자로 남아 있음을 보장함).

### <a name="advanced-prefix-reservation-scenarios"></a>고급 접두사 예약 시나리오

하위 접두사 위임 및 접두사를 공용으로 표시하는 것을 포함하여 아래에 설명된 몇 가지 고급 접두사 예약 시나리오가 있습니다. 다음은 수행할 수 있는 고급 접두사 예약입니다. 

- 접두사 예약 중에 소유자는 다른 소유자에게 접두사 하위 집합(또는 접두사)의 위임을 요청할 수 있습니다. 예를 들어 '[Microsoft](https://www.nuget.org/profiles/microsoft)'가 'Microsoft를 소유\*'하지만 '[aspnet](https://www.nuget.org/profiles/aspnet)이 'Microsoft.AspNet \*'을 예약하려는 경우, '[Microsoft](https://www.nuget.org/profiles/microsoft)'는 'Microsoft.AspNet.\*'을 [aspnet](https://www.nuget.org/profiles/aspnet) 계정에 위임하도록 선택할 수 있습니다.

- 접두사 예약 중에 소유자는 접두사를 공개하도록 선택할 수 있습니다. 이렇게 하면 패키지가 예약된 접두사에서 시작되는 것을 보여주는 시각적 표시기가 제공되지만 소유자에 대한 접두사의 향후 패키지 제출을 차단하지는 **않습니다**. 이는 많은 기여자가 있는 오픈 소스 프로젝트에 유용합니다. 상위 또는 핵심 기여자는 접두사를 예약할 수 있지만 모든 기여자에게 계속 공개될 수 있습니다. 

### <a name="prefix-reservation-visual-indicator"></a>접두사 예약 시각적 표시기

예약된 접두사에서 패키지를 가져오는 경우 [nuget.org](https://www.nuget.org/) 갤러리 및 Visual Studio 2017 버전 15.4 이상에서 다음 시각적 표시기가 나타납니다.

**nuget.org 갤러리**
![nuget.org 갤러리](media/nuget-gallery-reserved-prefix.png)

**Visual Studio**
![Visual Studio](media/visual-studio-reserved-prefix.png)

## <a name="id-prefix-reservation-application-process"></a>ID 접두사 예약 애플리케이션 프로세스

1. [ID 접두사 예약에 대한 기준](#id-prefix-reservation-criteria) 허용을 검토하세요.

2. 필요할 수 있는 [고급 접두사 예약 시나리오](#advanced-prefix-reservation-scenarios) 외에도 예약할 접두사를 확인하세요.

3. 이메일을 요청 중인 예약된 접두사뿐만 아니라 [nuget.org](https://www.nuget.org/)의 소유자 표시 이름이 있는 [account@nuget.org](mailto:account@nuget.org)로 보냅니다. 여러 소유자에게 접두사 하위 집합을 위임하는 경우 모든 소유자 표시 이름과 접두사 하위 집합을 언급했는지 확인합니다.

애플리케이션을 제출한 후 승인 또는 거부(거부를 초래한 기준 포함)에 대한 통보를 받습니다. 소유자 ID를 확인하기 위해 추가적인 식별 질문을 할 수도 있습니다.

### <a name="id-prefix-reservation-criteria"></a>ID 접두사 예약 조건

ID 접두사 예약에 대한 모든 애플리케이션을 검토할 때 [nuget.org](https://www.nuget.org/) 팀은 아래 기준에 따라 애플리케이션을 평가합니다. 접두사를 예약하기 위해 모든 기준을 충족해야 하는 것은 아니지만, 충족되는 기준에 대한 실질적인 증거가 없는 경우 애플리케이션은 거부될 수 있습니다(지정된 설명 포함).

1. 패키지 ID 접두사가 제대로 되어 있으며 패키지 소유자를 명확하게 식별하나요?

1. 패키지 소유자가 [NuGet.org 계정에서 2FA를 활성화했나요](individual-accounts.md#enable-two-factor-authentication-2fa)?

1. 소유자가 이미 제출한 패키지의 상당수가 패키지 ID 접두사 아래에 있나요?

1. 패키지 ID 접두사는 개별 소유자 또는 조직에 속하면 안되는 공통적인 것인가요?

1. 패키지 ID 접두사를 예약하지 *않으면* 커뮤니티에 모호함과 혼동을 일으키나요?

1. 패키지 ID 접두사와 일치하는 패키지의 식별 속성이 명확하고 일관적인가요(특히 패키지 작성자)?

1. 패키지에 라이선스가 있나요([라이선스](../reference/nuspec.md#license) 메타데이터 요소를 사용하고 사용이 중단된 licenseUrl은 사용하지 않음)?

1. 패키지에 아이콘이 있는 경우, [아이콘](../reference/nuspec.md#icon) 메타데이터 요소(iconUrl을 제거하는 데 필수 요소 아님)를 사용하고 있나요?

## <a name="third-party-feed-provider-scenarios"></a>타사 피드 공급자 시나리오

타사 피드 공급자가 접두사 예약을 제공하기 위해 자체 서비스를 구현하려는 경우, NuGet V3 피드 공급자에서 검색 서비스를 수정하여 제공할 수 있습니다. 피드 검색 서비스를 변경하려면 `verified` 속성을 추가합니다. NuGet 클라이언트는 V2 피드에 추가된 속성을 지원하지 않습니다.

자세한 내용은 [API의 검색 서비스에 대한 설명서](../api/search-query-service-resource.md)를 참조하세요.

## <a name="package-id-prefix-reservation-dispute-policy"></a>패키지 ID 접두사 예약 분쟁 정책
[NuGet.org](https://www.nuget.org)의 소유자에게 위에 나열된 기준에 위배되는 패키지 ID 접두사 예약이 할당되었거나 상표 또는 저작권을 침해했다고 판단되는 경우, 해당 ID 접두사, ID 접두사의 소유자 및 할당된 접두사 예약에 대해 이의를 제기하는 이유를 이메일 [support@nuget.org](mailto:support@nuget.org)로 보내주세요.

