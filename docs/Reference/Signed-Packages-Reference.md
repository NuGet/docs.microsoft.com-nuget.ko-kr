---
title: "패키지 참조 서명 | Microsoft Docs"
author: rido-min
ms.author: rido-min
manager: unniravindranathan
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "패키지 기능 설명을 서명합니다."
keywords: "NuGet 패키지 서명, 서명, 인증서"
ms.reviewer:
- ananguar
- karann-msft
- unniravindranathan
ms.openlocfilehash: 9bf9885aaf42bedb681a5d916202fa8b26749a0c
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
---
# <a name="signed-packages"></a>서명 된 패키지

*NuGet 4.6.0+ 및 Visual Studio 2017 15.6 이상 버전*

NuGet 패키지는 변조 된 콘텐츠에 대 한 보호를 제공 하는 디지털 서명을 포함할 수 있습니다. 이 서명은 패키지의 실제 출처에도 정품 증명을 추가 하는 X.509 인증서에서 생성 됩니다.

서명 된 패키지는 가장 강력한 종단 간 유효성 검사를 제공합니다. 만든 서명을 보장 작성자에서 관계 없이 패키지를 서명 후 수정 되지 않은 패키지 저장소 또는 어떤 전송 패키지에서 전달 되는 메서드는 합니다.

잠긴 환경 요구 하는 특정 작성자 인증서로 서명 된 패키지에 필요할 수 있습니다.

또한 패키지 작성자 서명 미리 서명 인증서를 등록 해야 하기 때문에 nuget.org 게시 파이프라인에는 추가 인증 메커니즘을 제공 합니다.

서명된 된 패키지를 만드는 방법에 대 한 세부 정보를 참조 하십시오. [패키지 서명](../create-packages/Sign-a-package.md) 및 [nuget sign 명령](../tools/cli-ref-sign.md)합니다.

> [!Important]
> nuget.org 현재 서명 된 패키지를 받아들이지 않습니다. 사용자 지정 피드를 게시에 대 한 패키지를 서명할 수 있습니다.

## <a name="certificate-requirements"></a>인증서 요구 사항

코드 서명 인증서는 특수 한 유형의에 유효한 인증서를 필요한 패키지를 서명는 `id-kp-codeSigning` 용도 [[RFC 5280 섹션 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. 또한 인증서는 RSA 공개 키 길이가 2048 비트 이상이 있어야 합니다.

## <a name="get-a-code-signing-certificate"></a>코드 서명 인증서를 가져오기

같은 공용 인증 기관에서 유효한 인증서를 구할 수 있습니다.

- [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [DigiCert](https://www.digicert.com/code-signing/)
- [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate)
- [전역 기호](https://www.globalsign.com/en/code-signing-certificate/)
- [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

Windows에서 신뢰할 수 있는 인증 기관의 전체 목록을 가져올 수 있습니다 [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners)합니다.

## <a name="create-a-test-certificate"></a>테스트 인증서 만들기

테스트용으로 자체 발급 된 인증서를 사용할 수 있습니다. 자체 발급 된 인증서를 만들려면 사용는 [New-selfsignedcertificate](https://docs.microsoft.com/en-us/powershell/module/pkiclient/new-selfsignedcertificate) PowerShell 명령입니다.

```ps
New-SelfSignedCertificate -Subject "CN=NuGet Test Developer, OU=Use for testing purposes ONLY" `
                          -FriendlyName "NuGetTestDeveloper" `
                          -Type CodeSigning `
                          -KeyUsage DigitalSignature `
                          -KeyLength 2048 `
                          -KeyAlgorithm RSA `
                          -HashAlgorithm SHA256 `
                          -Provider "Microsoft Enhanced RSA and AES Cryptographic Provider" `
                          -CertStoreLocation "Cert:\CurrentUser\My" 
```

이 명령은 현재 사용자의 개인 인증서 저장소에 사용할 수 있는 테스트 인증서를 만듭니다. 실행 하 여 인증서 저장소를 열 수 `certmgr.msc` 새로 만든된 인증서를 볼 수 있습니다.

## <a name="timestamp-requirements"></a>타임 스탬프 요구 사항

서명 된 패키지는 패키지 서명 인증서의 유효 기간이 초과 서명 유효성을 보장 하도록는 RFC 3161 타임 스탬프를 포함 해야 합니다. 타임 스탬프를 서명에 사용 된 인증서에 대해 유효 해야 합니다.는 `id-kp-timeStamping` 용도 [[RFC 5280 섹션 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. 또한 인증서는 RSA 공개 키 길이가 2048 비트 이상이 있어야 합니다.

추가 기술 세부 정보에서 찾을 수 있습니다는 [패키지 서명을 기술 사양](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).
