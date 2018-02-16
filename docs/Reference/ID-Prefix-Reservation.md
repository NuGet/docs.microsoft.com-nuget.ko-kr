---
title: "ID 접두사 예약 참조 | Microsoft Docs"
author: diverdan92
ms.author: diverdan92
manager: unniravindranathan
ms.date: 10/09/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "패키지 ID 접두사 예약 기능 설명 및 만든 가이드입니다."
keywords: "NuGet 패키지 ID, 접두사, 예약"
ms.reviewer:
- ananguar
- karann-msft
- unniravindranathan
ms.openlocfilehash: bee215fcc88b03dbdde6c15d1583898bdf205952
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/14/2018
---
# <a name="package-id-prefix-reservation"></a>패키지 ID 접두사 예약

패키지 소유자는을 예약 하 고 ID 접두사를 예약 하 여 자신의 id를 보호 합니다. 소비자가 패키지에는 추가 정보는 패키지를 사용 하는 경우 사용 하는 패키지 이것 들은 하지 식별 하는 속성이에 제공 됩니다. 

[nuget.org](https://www.nuget.org/) 패키지 전송 하는 예약 된 패키지 ID 접두사와 소유자가 패키지에는 예약 된 ID와 일치 하기만 접두사로 명명 패턴에 대 한 Visual Studio 2017 15.4 이후 버전 시각적 표시기를 표시 합니다. 아래 참조 ID 접두사 예약의 수반, 소유자 ID 접두사에 대 한 적용할 수 있는 방법 및 설명 합니다.

## <a name="id-prefix-reservation-details"></a>ID 접두사 예약 세부 정보

패키지 ID 접두사는 예약 되어에 여러 작업이 수행 된 [nuget.org](https://www.nuget.org/) 갤러리, Visual Studio에서와 같이 합니다. 또한 접두사 하위 집합을 여러 소유자에 게 위임 하는 접두사 'public'로 설정 하는 등 ID 접두사 예약에서 지 원하는 시나리오 고급 됩니다.

### <a name="id-prefix-reservation-on-nugetorg"></a>ID 접두사 nuget.org 예약

접두사에 대해 예약 되는 경우 [nuget.org](https://www.nuget.org/), 다음 작업이 수행 됩니다.

1. 접두사 예약에 연결 된 소유자 또는 소유자 집합이 [nuget.org](https://www.nuget.org/)합니다.

1. 패키지에 제출 된 때마다 [nuget.org](https://www.nuget.org/) 예약 된 ID 접두사와 일치 하는 id, 패키지 ID 접두사를 예약 하는 소유자에서 원본으로 사용 하지 않으면 거부 됩니다.

1. 예약 된 ID 접두사와 일치 하 고 ID 접두사를 예약 하는 소유자에서 발생 하는 모든 패키지와 Visual Studio 2017 15.4 이후 버전에는 시각적 표시기 갖습니다 [nuget.org](https://www.nuget.org/) 에서 관리 하는 패키지를 나타내는 예약 된 ID 접두사입니다. 이것으로 새 패키지 전송의 소유자에서 기존 패키지에 적용 됩니다. **참고:** 단일 피드 패키지 원본으로 선택한 경우에 Visual Studio에서 표시기가 나타납니다.

1. 예약 된 ID 접두사와 일치 하는 모든 이전에 기존 패키지가 하지만 *하지* 예약된 소유자가 소유 하 고 접두사는 변경 되지 것입니다 (목록에 없는, 됩니다 하지만 또한 수는 없습니다는 시각적 표시기). 또한, 이러한 패키지의 소유자 여전히 됩니다 패키지에 새 버전을 제출할 수 있습니다.

이러한 변경 내용은 다음 조건에 따라 결정 되 고 몇 가지 추가 제한 사항이 적용:

- 패키지의 한 명의 소유자 (패키지에 대 한 여러 소유자가 있는)를 표시 하는 시각적 표시기에 대 한 예약 된 접두사에 필요 합니다.

- 하나 이상의 소유자가 예약 된 접두사를 하나 이상의 소유자에 예약 된 접두사가 없는 패키지의 둘 이상의 소유자가 예약 된 접두사가 포함 된 소유자만 예약 된 접두사가 포함 된 다른 소유자를 제거할 수 있습니다. 예약 된 접두사를 갖고 있지 않은 소유자는 예약 된 접두사가 포함 된 소유자를 제거할 수 없습니다. 여전히도 예약 된 접두사를 갖지 않는 다른 소유자를 제거할 수 있습니다.

- 해야 하는 시각적 표시기를 포함 하는 패키지, 일단 *항상* 는 시각적 표시기가 (예약 된 접두사가 포함 된 하나 이상의 해당 소유자를 보장 하는 항상 그대로 소유자)

### <a name="advanced-prefix-reservation-scenarios"></a>고급 접두사 예약 시나리오

몇 가지 고급 접두사 예약 시나리오 subprefix 위임 및 public으로 표시 접두사를 포함 하 여 아래에서 설명 합니다. 다음은 수행할 수 있는 더 많은 고급 접두사 예약입니다. 

- 접두사 예약 하는 동안 소유자가 접두사 하위 집합의 위임 (또는 접두사) 다른 소유자에 게 요청할 수 있습니다. 예를 들어 경우 '[Microsoft](https://www.nuget.org/profiles/microsoft)' 소유 ' Microsoft.\*', 하지만 '[aspnet](https://www.nuget.org/profiles/aspnet)' 예약할 ' Microsoft.AspNet.\*','[Microsoft](https://www.nuget.org/profiles/microsoft)' 수 있습니다 에 위임 하도록 선택할 ' Microsoft.AspNet 합니다. \*'에 [aspnet](https://www.nuget.org/profiles/aspnet) 계정.

- 접두사 예약 하는 동안 접두사를 공개로 설정 하는 소유자 선택할 수 있습니다. 이 계속 해 서 이러한 패키지는 예약 된 접두사에서 시작 하지만 하므로 표시 되는 시각적 표시기 **하지** 모든 소유자에 대 한 접두사에서 이후 패키지 전송을 차단 합니다. 이 많은 참가자와 오픈 소스 프로젝트에 대 한 유용한-위나 코어 참가자, 예약 된 접두사를 가질 수 있습니다 하지만 모든 참가자를 열 수 있습니다. 

### <a name="prefix-reservation-visual-indicator"></a>접두사 예약 시각적 표시기

패키지 예약 된 접두사에 도달할 경우 참조는 아래에서 시각적 표시기는 [nuget.org](https://www.nuget.org/) 갤러리 및 Visual Studio 2017 15.4 이후 버전에서에서:

**nuget.org Gallery**
![nuget.org Gallery](media/nuget-gallery-reserved-prefix.png)

**Visual Studio**
![Visual Studio](media/visual-studio-reserved-prefix.png)

## <a name="id-prefix-reservation-application-process"></a>ID 접두사 예약 응용 프로그램 프로세스

1. 검토 수락 [접두사 ID 예약에 대 한 조건을](#id-prefix-reservation-criteria)합니다.

1. 결정 사항이 추가 예약 하려는 네임 스페이스 [고급 접두사 예약 시나리오](#advanced-prefix-reservation-scenarios) 필요할 수 있습니다.

1. 메일을 보내세요 [ account@nuget.org ](mailto:account@nuget.org) 소유자와 이름에 표시 [nuget.org](https://www.nuget.org/)를 요청 하는 모든 예약 된 접두사 뿐만 아니라 합니다. 여러 소유자에 접두사 하위 집합을 위임한 경우에 모든 소유자 표시 이름을 언급 하 고 접두사 하위 집합에 있는지 확인 합니다.

응용 프로그램을 제출의 수락 또는 거부를 발생 시킨 조건) (으로 거부 메시지가 표시 됩니다. 소유자 확인할 추가 식별 질문 해야 합니다.

### <a name="id-prefix-reservation-criteria"></a>ID 접두사 예약 조건

ID 접두사 예약에 대 한 모든 응용 프로그램을 검토 하는 경우는 [nuget.org](https://www.nuget.org/) 팀에 대해 응용 프로그램을 평가 하는 조건 아래 합니다. 일부 조건 예약할 접두사에 대해 충족 되어야 하지만 응용 프로그램이 없는 경우 (에 제공 하는 설명이) 충족 하는 조건의 상당한 증거 거부 될 수 있습니다.

1. 패키지 ID 접두사를 제대로 하 고 명확 하 게 나타내는 패키지 소유자 무엇입니까?

1. 패키지 ID 접두사에서 소유자가 이미 제출 하는 패키지 수가?

1. 리 패키지 ID 접두사 일반적인 있는 모든 개별 소유자 또는 조직에 속하지 않아야 합니다.

1. *하지* 모호성 및 커뮤니티에 혼동 될 패키지 ID 접두사를 예약?

1. 패키지 ID 접두사 명확 하 고 일관성 (특히 패키지 작성자)와 일치 하는 패키지의 식별 하는 속성이?

## <a name="third-party-feed-provider-scenarios"></a>제 3 자 피드 공급자 시나리오

피드 공급자 제 3 자가 접두사 예약을 제공 하는 자신의 서비스를 구현 하는 데 관심이 있으면 수정 하 여 NuGet V3에서 검색 서비스 공급자를 공급 하도록 할 수 있습니다. 추가 하는 피드 검색 서비스에 추가 *확인* 속성 아래 V3 피드에 대 한 예제를 제공 합니다. NuGet 클라이언트 피드 v 2에서 추가 된 속성을 지원 하지 않습니다.

자세한 내용은 참조는 [API의 검색 서비스에 대 한 설명서](../api/search-query-service-resource.md)합니다.
