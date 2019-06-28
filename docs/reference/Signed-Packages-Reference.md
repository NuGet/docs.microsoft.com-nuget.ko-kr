---
title: 서명 된 패키지
description: NuGet 패키지를 서명 하는 것에 대 한 요구 사항입니다.
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 952256a24246543ecd4c37285cd001622aa2bc46
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426171"
---
# <a name="signed-packages"></a>서명된 패키지

*NuGet 4.6.0+ 및 Visual Studio 2017 버전 15.6 이상*

NuGet 패키지는 변조 된 콘텐츠에 대 한 보호를 제공 하는 디지털 서명을 포함 될 수 있습니다. 이 서명은 신뢰성 증명 패키지의 실제 원본에 추가 하는 X.509 인증서에서 생성 됩니다.

서명 된 패키지는 가장 강력한 종단 간 유효성 검사를 제공 합니다. 두 가지 유형의 NuGet 서명 가지
- **서명 작성**합니다. 작성자 서명 보장 작성자에서 든 관계 없이 패키지를 서명 후 수정 되지 않은 패키지 리포지토리 또는 패키지에 전달 되는 메서드를 전송 하는 합니다. 또한 작성자 서명 된 패키지 서명 인증서를 미리 등록 되어 있어야 하기 때문에 nuget.org 게시 파이프라인에 추가 인증 메커니즘을 제공 합니다. 자세한 내용은 [인증서 등록](#signature-requirements-on-nugetorg)합니다.
- **리포지토리 서명**합니다. 저장소에 대 한 무결성 보장을 서명은 **모든** 패키지만 있었던 원래 저장소와 다른 위치에서 가져온 경우에 작성자 부호가 있거나 없는 되었든 관계 없이 리포지토리에서 패키지 서명.   

작성자 서명 된 패키지를 만드는 방법에 대 한 세부 정보를 참조 하세요 [패키지 서명](../create-packages/Sign-a-package.md) 하며 [nuget 서명 명령](../tools/cli-ref-sign.md)입니다.

> [!Important]
> 패키지 서명에 Windows에서 nuget.exe를 사용 하는 경우에 현재 지원 됩니다. 서명 된 패키지 확인은 현재 Windows에서 Visual Studio 또는 nuget.exe를 사용 하는 경우에 지원 됩니다.

## <a name="certificate-requirements"></a>인증서 요구 사항

코드 서명 인증서에 유효한 인증서의 특수 형식에 필요한 패키지를 서명 합니다 `id-kp-codeSigning` 용도 [[RFC 5280 섹션 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. 또한 인증서에는 RSA 공개 키 길이가 2048 비트 이상 있어야 합니다.

## <a name="timestamp-requirements"></a>타임 스탬프 요구 사항

서명 된 패키지는 패키지 서명 인증서의 유효 기간이 초과 서명 유효성을 확인할 RFC 3161 타임 스탬프를 포함 해야 합니다. 타임 스탬프를 로그인에 사용 된 인증서에 대해 유효 해야 합니다 `id-kp-timeStamping` 용도 [[RFC 5280 섹션 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. 또한 인증서에는 RSA 공개 키 길이가 2048 비트 이상 있어야 합니다.

추가 기술 세부 정보에서 확인할 수 있습니다 합니다 [패키지 서명을 기술 사양은](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).

## <a name="signature-requirements-on-nugetorg"></a>NuGet.org에서 서명 요구 사항

nuget.org에는 서명 된 패키지를 적용 하기 위한 추가 요구 사항이 있습니다.

- 주 서명이 작성자 서명이 있어야 합니다.
- 주 서명이 유효한 타임 스탬프를 단일 있어야 합니다.
- 작성자 시그니처와 해당 타임 스탬프 서명을 모두에 대 한 X.509 인증서:
  - RSA 공개 키 2048 비트 있어야 합니다. 이상.
  - Nuget.org의 패키지 유효성 검사의 시간이 현재 UTC 시간 당 유효 기간 내에 있어야 합니다.
  - Windows에서 기본적으로 신뢰할 수 있는 신뢰할 수 있는 루트 기관에 연결 해야 합니다. 자체 발급 된 인증서로 서명 된 패키지 거부 됩니다.
  - 용도 맞는 해야 유효 합니다. 
    - 인증서 서명 작성자 코드 서명에 적합 해야 합니다.
    - 타임 스탬프 인증서 타임 스탬프에 대 한 유효 해야 합니다.
  - 서명할 때 취소할 수 있어야 합니다. (이 아닐 수도 제출 시 knowable 있으므로 nuget.org 해지 상태를 주기적으로 다시).
  
  
## <a name="related-articles"></a>관련 문서

- [NuGet 패키지 서명](../create-packages/Sign-a-Package.md)
- [패키지 트러스트 관리](../consume-packages/installing-signed-packages.md)
