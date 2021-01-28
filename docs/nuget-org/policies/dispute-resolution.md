---
title: NuGet 패키지 이름 분쟁 해결
description: 브랜딩과 관련된 NuGet 패키지 게시자, 상표 및 기타 충돌 상황 간에 분쟁을 해결하기 위한 프로세스입니다.
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: d9ed7de95a1f38ea2c288b28958519b1dff0e595
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775653"
---
# <a name="resolving-disputes-over-nuget-package-names"></a>NuGet 패키지 이름 분쟁 해결

이 문서는 커뮤니티 구성원에 대해 다른 NuGet 게시자와의 분쟁을 해결하도록 권장 해결 프로세스를 제공합니다.

예를 들어 Northwind Traders가 해당 웹 사이트에서 다운로드 가능한 MSI로 클라이언트 드라이버를 제공하도록 CRM 시스템을 만든다고 가정합니다. 독자적 개발자인 Nancy는 보다 쉽게 Northwind의 클라이언트 라이브러리를 사용할 수 있도록 하고 `NorthwindTraders.Client`라는 NuGet 패키지로 변환합니다. 나중에 Northwind에서는 해당 클라이언트 라이브러리에서 고유한 공식 NuGet 패키지를 생성하고 따라서 패키지 이름에 대한 Nancy의 소유권에 대한 분쟁이 발생합니다.

이 시나리오에서 Nancy는 나쁜 의도를 가진 것으로 보이지 않지만 대신 고유한 시간 및 코드를 제공하여 Northwind의 도구 및 고객을 지원합니다. 동시에 Northwind는 Northwind 이름의 정당한 소유자입니다.

Northwind 및 Nancy는 둘 다 개발자 커뮤니티를 제공하는 데 관심이 있기 때문에 아래 프로세스를 수행하여 적합한 해결 방법을 함께 모색합니다. 일반적으로 NuGet 팀이 관련될 필요는 없습니다. 협업은 일반적으로 뛰어난 결과를 발생시킵니다.

## <a name="process"></a>프로세스

1. 패키지 세부 정보 페이지에서 **연락처 소유자** 링크를 사용하여 분쟁이 발생한 패키지의 소유자에게 연락합니다. 직접 친절하게 문제를 설명합니다.
2. 해당 NuGet 및 .NET Foundation이 분쟁을 인식하도록 [support@nuget.org](mailto:support@nuget.org)에 메시지의 복사본을 보냅니다.
3. 해결을 위해 최대 30일 동안 대기한 다음 [support@nuget.org](mailto:support@nuget.org)에 다시 알립니다. nuget.org 지원팀이 참여하고 두 당사자와 분쟁을 해결하려고 합니다.
