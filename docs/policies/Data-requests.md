---
title: 사용자 데이터 요청
description: 사용자 데이터 내보내기 및 삭제 요청에 대한 정책
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/01/2018
ms.topic: conceptual
ms.openlocfilehash: 595a47da59c9b2672a10fc0f19e528c36a790134
ms.sourcegitcommit: 68c8a494a11c892ac671fec3170ba7be97fb044d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33086210"
---
# <a name="user-data-requests"></a>사용자 데이터 요청

nuget.org 사용자는 [nuget.org](https://www.nuget.org)를 통해 정보 삭제 요청 및 정보 내보내기 요청을 제출할 수 있습니다. 두 유형 모두 지원 요청의 형태로 제출되며 30일 이내에 nuget.org 관리자가 실행합니다.

다음 사용자 데이터는 nuget.org를 통해 직접 액세스할 수 있습니다.

* 이메일 주소, 로그인 계정, 프로필 사진 및 이메일 알림 설정과 같은 계정 관련 데이터
* 소유 API 키
* 소유 패키지 목록

이 데이터는 지원 요청을 통해 내보낸 데이터에 포함되지 않습니다.

## <a name="identifying-customer-data"></a>고객 데이터 식별

고객 데이터는 nuget.org 사용자 계정 이름으로 식별할 수 있습니다.

## <a name="deleting-customer-data"></a>고객 데이터 삭제

nuget.org에서 사용자 데이터 삭제를 요청하려면 다음을 수행합니다.

1. 사용자가 [nuget.org](https://www.nuget.org)에 로그인해야 합니다.
1. 사용자가 [nuget.org/account/delete](https://www.nuget.org/account/delete)에서 삭제할 해당 계정에 대한 요청을 제출해야 합니다.

패키지의 유일한 소유자인 사용자는 자신의 계정 삭제를 요청하기 전에 새 소유자를 찾는 것이 좋습니다. 패키지 소유권이 전송되지 않으면 NuGet 패키지가 삭제되어 결과적으로 Visual Studio 또는 nuget.org 웹 사이트에서 검색 쿼리에 사용할 수 없게 됩니다. 계정을 삭제하기 전에 nuget.org 관리자는 사용자와 함께 소유한 패키지에 대한 새 소유자를 찾는 작업을 수행합니다.

계정 삭제 작업은 요청한 날짜로부터 30일 안에 nuget.org 관리자가 완료합니다.

계정 삭제 시 사용자의 모든 데이터가 nuget.org 시스템에서 제거되고 다음 동작이 수행됩니다.

* 삭제된 계정이 nuget.org에서 등록 취소됨
* 모든 소유 API 키가 삭제됨
* 모든 예약된 네임스페이스가 릴리스됨
* 모든 패키지 소유권이 제거됨

소유된 패키지는 삭제되지 *않습니다*. 검색 결과에 나열되지 않은 경우라도 이에 종속된 프로젝트로의 패키지 복원을 통해 계속 사용할 수 있습니다.

## <a name="exporting-customer-data"></a>고객 데이터 내보내기

nuget.org에 로그인한 후 사용자는 [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact)를 통해 내보내기 요청을 제출할 수 있습니다.

내보낸 데이터는 사용자가 48시간 동안 Azure Blob을 통해 다운로드할 수 있습니다. 48시간 후에는 액세스가 만료되고 사용자는 필요에 따라 새 내보내기 요청을 제출해야 합니다.

내보낸 데이터에는 다음 항목이 포함되어 있습니다.

* 사용자의 지원 요청
* 감사 로그에 유지된 사용자의 작업(패키지 게시, 계정 만들기)
* IIS 로그에 유지된 사용자 정보
