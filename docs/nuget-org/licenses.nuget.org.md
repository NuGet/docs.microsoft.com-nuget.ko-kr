---
title: licenses.nuget.org
author: agr
ms.date: 02/22/2019
ms.openlocfilehash: 717cf8c47335c620410be71300b07de82799e1d3
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427118"
---
# <a name="licensesnugetorg"></a>licenses.nuget.org

## <a name="rationale"></a>설명

[라이선스 식](../reference/nuspec.md#license)의 도입으로 인해 개별 라이선스 식별자, 예외 식별자 또는 라이선스 식에 대한 참조 텍스트를 제공하는 신뢰할 수 있는 서비스를 갖추어야 하는 요구 사항이 대두되었습니다.
이 서비스에 대한 추가 요구 사항은 링크 손실에 취약하지 않은 안정적인 URL 스키마를 갖추어 오래된 클라이언트에 대해 이전 버전과의 호환성을 제공하여 안전하게 사용할 수 있도록 하는 것입니다.

Licenses.nuget.org는 해당 역할을 수행합니다. Nuget.org는 이를 통해 라이선스 식을 사용하여 라이선스를 지정하는 패키지에 대한 라이선스 텍스트 참조를 제공합니다. `nuget pack` 또는 다른 [클라이언트 도구](../install-nuget-client-tools.md)로 패킹하여 [`licenseUrl`](../reference/nuspec.md#licenseurl) 요소가 licenses.nuget.org를 가리키도록 설정하여 `license` 요소가 지원되지 않은 오래된 클라이언트에게 이전 버전과의 호환성을 제공합니다.

## <a name="protocol"></a>프로토콜

Licenses.nuget.org는 브라우저에 있는 사용자가 볼 수 있도록 고안되었으며, 머신이 읽을 수 있는 응답은 제공되지 않습니다.
HTTPS 프로토콜을 사용해야 하며 요청은 특정 방법으로 구성되어야 합니다. `GET` 요청만 지원합니다.
아래에 지정된 방법으로 라이선스 식 또는 라이선스 예외 식별자를 입력으로 허용합니다. 라이선스 식의 모든 요소는 대/소문자를 구분하므로 licenses.nuget.org에 대한 모든 입력도 대/소문자를 구분한다는 점에 유의하세요.

### <a name="license-expressions"></a>라이선스 식

#### <a name="request"></a>요청

라이선스 식(식은 단일 라이선스로 구성되는 간단한 사례 포함)은 [URL로 인코딩](https://tools.ietf.org/html/rfc3986#section-2.1)되어야 하며 licenses.nuget.org에 대한 요청의 경로로 사용해야 합니다.

| 라이선스 식 | 사용할 URL |
|:---|:---|
| MIT                                                | <https://licenses.nuget.org/MIT> |
| (MIT)                                              | <https://licenses.nuget.org/(MIT)> |
| (FLTK 예외가 있는 LGPL 2.0 전용 OR Apache-2.0+) | <https://licenses.nuget.org/(LGPL-2.0-only%20WITH%20FLTK-exception%20OR%20Apache-2.0+)> |

이 서비스는 nuget.org에서 허용되는 라이선스 식별자와 예외 식별자만 지원합니다. 지원되지 않는 라이선스 식별자 또는 라이선스 예외 식별자를 포함하거나 라이선스 식 구문을 준수하지 않는 모든 라이선스 식은 유효하지 않은 것으로 간주됩니다.

#### <a name="response"></a>응답

Licenses.nuget.org는 HTTP 200 상태 코드와 함께 유효한 라이선스 식을 포함하는 요청 및 라이선스 식에 대한 설명이 포함된 웹 페이지에 응답합니다.

* 제공된 라이선스 식에 단일 라이선스 식별자가 포함된 경우 라이선스 참조 텍스트가 포함된 웹 페이지가 반환됩니다.
* 제공된 라이선스 식이 복합 라이선스 식인 경우 개별 라이선스 또는 라이선스 예외 참조에 대한 링크와 함께 라이선스 식이 포함된 웹 페이지가 반환됩니다.

잘못된 라이선스 식을 포함하는 모든 요청은 HTTP 404 응답을 발생시킵니다.

### <a name="license-exceptions"></a>라이선스 예외

#### <a name="request"></a>요청

라이선스 예외 식별자는 URL로 인코딩되어 licenses.nuget.org에 대한 요청의 경로로 사용되어야 합니다. 단일 라이선스 예외 식별자만 단일 요청으로 제공할 수 있습니다. 라이선스 예외 식별자 외에도 추가 문자는 URL의 경로 부분에 없을 수 있습니다.

| 라이선스 예외 식별자 | 사용할 URL |
|:---|:---|
|FLTK 예외            | <https://licenses.nuget.org/FLTK-exception> |
|openvpn-openssl-exception | <https://licenses.nuget.org/openvpn-openssl-exception> |

#### <a name="response"></a>응답

Licenses.nuget.org는 알려진 라이선스 예외 식별자가 있는 요청에 대해 HTTP 200 응답 및 지정된 라이선스 예외에 대한 참조 텍스트가 포함된 웹 페이지로 응답합니다.

지원되지 않는 라이선스 예외 식별자를 포함하는 모든 요청은 HTTP 404 응답을 발생시킵니다.