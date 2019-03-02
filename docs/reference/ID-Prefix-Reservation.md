---
title: ID 접두사 예약 참조
description: 패키지 ID 접두사 예약 기능 설명 및 작성자 가이드입니다.
author: diverdan92
ms.author: diverdan92
ms.date: 10/09/2017
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: e8b902c89427333afb7a27ee9de0eeb99a92f391
ms.sourcegitcommit: 571644118e3c5a2fd818891d305b4b8de8ef21de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/02/2019
ms.locfileid: "57225877"
---
# <a name="package-id-prefix-reservation"></a>패키지 ID 접두사 예약

패키지 소유자를 예약 하 고 ID 접두사를 예약 하 여 자신의 id를 보호할 수 있습니다. 패키지 소비자는 추가 정보를 사용 하 여 패키지를 사용 하는 경우 현재 사용 중인 패키지 없는 해당 식별 속성에서 거짓 제공입니다. 

[nuget.org](https://www.nuget.org/) Visual Studio 2017 버전 15.4 이상 패키지 예약된 ID와 일치 하기만 예약 된 패키지 ID 접두사를 사용 하 여 소유자가 전송 되는 패키지는 명명 패턴 접두사에 대 한 시각적 표시기를 표시 합니다. 아래 참조 ID 접두사 예약 시 어떤 및 소유자 ID 접두사를 적용 하는 방법을 설명 합니다.

## <a name="id-prefix-reservation-details"></a>ID 접두사 예약 세부 정보

여러 작업이 수행 된 패키지 ID 접두사 예약 된 경우는 [nuget.org](https://www.nuget.org/) 갤러리도 Visual Studio와 같이 합니다. 또한 접두사 하위 집합을 여러 소유자에 게 위임으로 'public' 접두사를 설정 하는 등 ID 접두사 예약을 지 원하는 시나리오 고급 됩니다.

### <a name="id-prefix-reservation-on-nugetorg"></a>Nuget.org에서 ID 접두사 예약

접두사는 예약 하는 경우 [nuget.org](https://www.nuget.org/), 다음 현상이 발생 합니다.

1. 접두사 예약에 소유자 또는 소유자의 집합을 사용 하 여 연결 된 [nuget.org](https://www.nuget.org/)합니다.

1. 패키지를 전송할 때마다 [nuget.org](https://www.nuget.org/) 예약된 ID 접두사와 일치 하는 ID를 사용 하 여 패키지 ID 접두사 예약 소유자에서 시작 하지 않으면 거부 됩니다.

1. Visual Studio 2017 버전 15.4 이상에 예약 된 ID 접두사와 일치 하 고 소유자 ID 접두사 예약에서 발생 하는 모든 패키지에서 시각적 표시기를 갖습니다 [nuget.org](https://www.nuget.org/) 에서 패키지를 나타내는 예약된 ID 접두사입니다. 새 패키지 제출 뿐만 아니라 기존 패키지의 소유자에 대 한 마찬가지입니다. **참고:** Visual Studio에서 표시기는 단일 피드 패키지 원본으로 선택한 경우에 나타납니다.

1. 예약된 ID 접두사와 일치 하는 모든 기존 패키지 하지만 됩니다 *하지* 예약된 된 소유자가 소유 하 고 접두사는 그대로 유지 됩니다 (비공개, 되지 것입니다 하지만 됩니다 하지 시각적 표시기). 또한 이러한 패키지의 소유자 패키지에 새 버전을 제출 하는 일을 할 수 있습니다.

이러한 변경 내용은 다음 조건에 기반한 및 몇 가지 추가 제한 사항이 적용 합니다.

- 패키지의 소유자 하나만 표시 (여러 소유자를 사용 하 여 패키지)에 대 한 시각적 표시기에 대 한 예약 된 접두사를가지고 있어야 합니다.

- 하나 이상의 소유자에 예약 된 접두사 없는 있고 하나 이상의 소유자 예약 된 접두사에 있는 패키지의 둘 이상의 소유자가 예약 된 접두사를 사용 하 여 소유자만이 예약된 된 접두사를 사용 하 여 다른 소유자를 제거할 수 있습니다. 예약 된 접두사를 갖고 있지 않은 소유자는 예약 된 접두사를 사용 하 여 소유자를 제거할 수 없습니다. 여전히도 예약 된 접두사를 갖지 않는 다른 소유자를 제거할 수 있습니다.

- 패키지를 시각적 표시기가 되 면 *항상* 시각적 표시기는 (예약 된 접두사를 사용 하 여 하나 이상의 해당 소유자를 보장 하는 항상 남아 소유자)

### <a name="advanced-prefix-reservation-scenarios"></a>고급 접두사 예약 시나리오

몇 가지 고급 접두사 예약 시나리오 subprefix 위임 및 public으로 표시 접두사를 포함 하 여 아래에서 설명 합니다. 다음은 수행할 수 있는 고급 접두사 예약입니다. 

- 접두사 예약 하는 동안 소유자가 접두사 하위의 위임 (또는 접두사) 다른 소유자에 게 요청할 수 있습니다. 예를 들어 경우 '[Microsoft](https://www.nuget.org/profiles/microsoft)' 소유 ' microsoft\*', 있지만 '[aspnet](https://www.nuget.org/profiles/aspnet)' 예약 하려는 ' Microsoft.AspNet.\*','[Microsoft](https://www.nuget.org/profiles/microsoft)' 수 위임 하도록 선택할 ' Microsoft.AspNet 합니다. \*'에 [aspnet](https://www.nuget.org/profiles/aspnet) 계정.

- 접두사 예약 하는 동안 소유자 공용 접두사를 만들 수 있습니다. 이 계속 해 서 이러한 패키지는 예약된 된 접두사에서 시작 되는 것을 보여 주는 시각적 표시기 **하지** 모든 소유자에 대 한 접두사에 패키지의 나중 서브 미션을 차단 합니다. 많은 참가자를 사용 하 여 오픈 소스 프로젝트에 대 한 유용-top 또는 핵심 참가자는 예약 된 접두사를 가질 수 있습니다 하지만 모든 참가자를 열 수 있습니다. 

### <a name="prefix-reservation-visual-indicator"></a>접두사 예약에 대 한 시각적 표시기

예약된 된 접두사에서 패키지 상태가 되 면 표시를 아래에 대 한 시각적 표시기를 [nuget.org](https://www.nuget.org/) 갤러리 및 Visual Studio 2017 버전 15.4 이상에서:

**nuget.org Gallery**
![nuget.org Gallery](media/nuget-gallery-reserved-prefix.png)

**Visual Studio**
![Visual Studio](media/visual-studio-reserved-prefix.png)

## <a name="id-prefix-reservation-application-process"></a>ID 접두사 예약 응용 프로그램 프로세스

1. 승인 검토 [ID 접두사 예약에 대 한 조건을](#id-prefix-reservation-criteria)합니다.

2. 외에도 예약 하려는 접두사를 확인할 [고급 접두사 예약 시나리오](#advanced-prefix-reservation-scenarios) 필요할 수 있습니다.

3. 에 게 메일 보내기 [ account@nuget.org ](mailto:account@nuget.org) 소유자를 사용 하 여 이름에 표시할 [nuget.org](https://www.nuget.org/)를 요청 하는 모든 예약 된 접두사와 합니다. 여러 소유자에 게 접두사 하위 집합을 위임할 경우 모든 소유자 표시 이름을 언급 하 고 접두사 하위 집합에 있는지 확인 합니다.

응용 프로그램을 제출한 후 승인 또는 거부를 발생 시킨 조건) (으로 거부의 알림이 표시 됩니다. 소유자 id를 확인 하려면 추가 식별 질문 해야 합니다.

### <a name="id-prefix-reservation-criteria"></a>ID 접두사 예약 조건

ID 접두사 예약에 대 한 모든 응용 프로그램을 검토할 때 합니다 [nuget.org](https://www.nuget.org/) 팀에 대 한 응용 프로그램을 평가 하는 아래 기준을 합니다. 일부 조건을 접두사 예약 되도록 하기 위해 충족 해야 합니다. 하지만 (지정 된 설명)와 부합 하지 않게 조건의 상당한 증거 없는 경우 응용 프로그램을 거부 될 수 있습니다.

1. 패키지 ID 접두사 제대로 명확 하 게 나타내는 패키지 소유자 무엇입니까?

1. 패키지 ID 접두사 아래 소유자가 이미 제출 하는 패키지의 상당수?

1. 패키지 ID 접두사를 사용 하는 일반적인 모든 개별 소유자 또는 조직에 속하지 않아야 합니까?

1. 것 *되지* 모호성 및 커뮤니티에 대 한 혼동을 일으킬 패키지 ID 접두사 예약?

1. 패키지 ID 접두사 명확 하 고 일관 된 (특히 패키지 작성자)와 일치 하는 패키지를 식별 하는 속성이?

1. 패키지 라이선스가 있는 (사용 하는 [라이선스](https://docs.microsoft.com/en-us/nuget/reference/nuspec#license) 메타 데이터 요소 및 사용이 중단 되는 licenseUrl 하지)?

## <a name="third-party-feed-provider-scenarios"></a>타사 공급자 시나리오를 피드 합니다.

피드 공급자 타사 접두사 예약을 제공 하는 자신의 서비스를 구현 하는 데 관심이 있으면 NuGet V3에서 search 서비스를 수정 하 여 공급자를 피드 하므로 수행할 수 있습니다. 추가 피드 검색 서비스에 추가 하는 것은 *확인* V3 피드 아래에 대 한 예제를 사용 하 여 속성입니다. NuGet 클라이언트는 피드 V2의 추가 속성을 지원 하지 않습니다.

자세한 내용은 참조는 [API의 search 서비스에 대 한 설명서](../api/search-query-service-resource.md)합니다.

## <a name="package-id-prefix-reservation-dispute-policy"></a>패키지 ID 접두사 예약 분쟁 정책
소유자를 생각 [NuGet.org](https://www.nuget.org) 위의 나열 된 조건에 위배 또는 상표권, 저작권 또는 상표에 하세요 전자 메일 침해 하는 패키지 ID 접두사 예약 할당 된 [ support@nuget.org ](mailto:support@nuget.org)해당 ID 접두사, 소유자 ID 접두사와 할당 된 접두사 예약 disputing 이유입니다.

