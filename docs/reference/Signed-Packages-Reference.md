---
title: 서명 된 패키지
description: NuGet 패키지를 서명 하는 것에 대 한 요구 사항입니다.
author: rido-min
ms.author: rmpablos
manager: unnir
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 72fb1a87c13160c53f632d2ef87a12a4e9bc02a3
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/22/2018
ms.locfileid: "34449593"
---
# <a name="signed-packages"></a>서명 된 패키지

*NuGet 4.6.0+ 및 Visual Studio 2017 15.6 이상 버전*

NuGet 패키지는 변조 된 콘텐츠에 대 한 보호를 제공 하는 디지털 서명을 포함할 수 있습니다. 이 서명은 패키지의 실제 출처에도 정품 증명을 추가 하는 X.509 인증서에서 생성 됩니다.

서명 된 패키지는 가장 강력한 종단 간 유효성 검사를 제공합니다. 만든 서명을 보장 작성자에서 관계 없이 패키지를 서명 후 수정 되지 않은 패키지 저장소 또는 어떤 전송 패키지에서 전달 되는 메서드는 합니다.

또한 패키지 작성자 서명 미리 서명 인증서를 등록 해야 하기 때문에 nuget.org 게시 파이프라인에는 추가 인증 메커니즘을 제공 합니다. 자세한 내용은 참조 [인증서 등록](#register-certificate-on-nugetorg)합니다.

서명된 된 패키지를 만드는 방법에 대 한 세부 정보를 참조 하십시오. [패키지 서명](../create-packages/Sign-a-package.md) 및 [nuget sign 명령](../tools/cli-ref-sign.md)합니다.

> [!Important]
> 패키지 서명에 Windows에서 nuget.exe를 사용 하는 경우에 현재 지원 됩니다. 서명 된 패키지 유효성 검사는 현재 Windows에서 nuget.exe 또는 Visual Studio를 사용 하는 경우에 지원 됩니다.

## <a name="certificate-requirements"></a>인증서 요구 사항

코드 서명 인증서는 특수 한 유형의에 유효한 인증서를 필요한 패키지를 서명는 `id-kp-codeSigning` 용도 [[RFC 5280 섹션 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. 또한 인증서는 RSA 공개 키 길이가 2048 비트 이상이 있어야 합니다.

## <a name="get-a-code-signing-certificate"></a>코드 서명 인증서를 가져오기

와 같은 공용 인증 기관에서 유효한 인증서를 구할 수 있습니다.

- [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [DigiCert](https://www.digicert.com/code-signing/)
- [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate)
- [전역 기호](https://www.globalsign.com/en/code-signing-certificate/)
- [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

Windows에서 신뢰할 수 있는 인증 기관의 전체 목록을 가져올 수 있습니다 [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners)합니다.

## <a name="create-a-test-certificate"></a>테스트 인증서 만들기

테스트용으로 자체 발급 된 인증서를 사용할 수 있습니다. 자체 발급 된 인증서를 만들려면 사용는 [New-selfsignedcertificate PowerShell 명령을](/powershell/module/pkiclient/new-selfsignedcertificate.md)합니다.

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

> [!Warning]
> nuget.org에 패키지를 사용할 수 없습니다 자체 발급 된 인증서로 서명 합니다.

## <a name="timestamp-requirements"></a>타임 스탬프 요구 사항

서명 된 패키지는 패키지 서명 인증서의 유효 기간이 초과 서명 유효성을 보장 하도록는 RFC 3161 타임 스탬프를 포함 해야 합니다. 타임 스탬프를 서명에 사용 된 인증서에 대해 유효 해야 합니다.는 `id-kp-timeStamping` 용도 [[RFC 5280 섹션 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. 또한 인증서는 RSA 공개 키 길이가 2048 비트 이상이 있어야 합니다.

추가 기술 세부 정보에서 찾을 수 있습니다는 [패키지 서명을 기술 사양](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).

## <a name="signature-requirements-on-nugetorg"></a>Nuget.org에 서명 요구 사항

nuget.org에는 서명 된 패키지를 적용 하기 위한 추가 요구 사항이 있습니다.

- 주 서명이 작성자 서명 해야 합니다.
- 주 서명이 유효한 타임 스탬프도 하나 있어야 합니다.
- 작성자 서명 및 타임 스탬프 시그니처에 모두에 대 한 X.509 인증서:
  - 2048 비트 RSA 공개 키 있어야 큽니다.
  - Nuget.org에 패키지 유효성 검사 시 현재 UTC 시간 마다 있으며 유효 기간 이내 여야 합니다.
  - Windows에서 기본적으로 신뢰할 수 있는 신뢰할 수 있는 루트 인증 기관에 연결 되어야 합니다. 자체 발급 된 인증서로 서명 된 패키지는 거부 됩니다.
  - 유효 해야의 용도 대 한: 
    - 만든이 서명 인증서를 코드 서명에 유효 해야 합니다.
    - 타임 스탬프 인증서 타임 스탬프에 대 한 유효 해야 합니다.
  - 서명할 때 해지할 수 해야 합니다. (이 아닐 수도 제출 시 knowable 있으므로 nuget.org 해지 상태를 주기적으로 다시 검사).

## <a name="register-certificate-on-nugetorg"></a>Nuget.org에 인증서 등록

서명된 된 패키지를 전송 하려면 먼저 nuget.org에 인증서를 등록 해야 합니다. 으로 인증서가 필요는 `.cer` 이진 DER 형식의 파일입니다. 인증서 내보내기 마법사를 사용 하 여 기존 인증서는 이진 DER 형식으로 내보낼 수 있습니다.

![인증서 내보내기 마법사](media/CertificateExportWizard.png)

고급 사용자를 사용 하 여 인증서를 내보낼 수는 [내보내기 인증서 PowerShell 명령을](/powershell/module/pkiclient/export-certificate.md)합니다.

인증서에 nuget.org를 등록 하려면로 이동 `Certificates` 섹션에서 `Account settings` 페이지 (또는 회사의 설정 페이지)를 선택 하 고 `Register new certificate`합니다.

![등록 된 인증서](media/registered-certs.png)

> [!Tip]
> 한 명의 사용자가 여러 사용자가 여러 인증서와 동일한 인증서를 등록할 수 있습니다을 제출할 수 있습니다.

사용자 인증서 등록, 모든 향후 패키지 전송 **해야** 인증서 중 하나를 사용 하 여 서명 합니다.

사용자 계정에서 등록 된 인증서를 제거할 수도 있습니다. 인증서가 제거 되 면 해당 인증서로 서명 하는 패키지 전송에 실패 합니다. 기존 패키지 영향을 받지 않습니다.

## <a name="configure-package-signing-requirements"></a>패키지 서명 요구 사항을 구성합니다

패키지의 유일한 소유자 인 경우 필요한 서명자 됩니다. 즉, 패키지를 서명 및 nuget.org를 제출 하는 등록 된 인증서를 사용할 수 있습니다.

기본적으로 여러 소유자를 포함 하는 패키지, 경우 "임의" 소유자의 인증서 패키지 서명에 사용할 수 있습니다. 패키지의 공동 소유자는 자신과 "Any" 또는 다른 공동 소유자 필요한 서명자를 재정의할 수 있습니다. 등록 된 모든 인증서가 없는 소유자를 만들면 서명 되지 않은 패키지 허용 됩니다. 

마찬가지로, 한 명의 소유자에 인증서가 등록 된 패키지와 다른 소유자에 대해 "Any" 옵션을 선택 하는 기본 등록 된 모든 인증서가 없으면 다음 nuget.org 허용는 서명 된 패키지 소유자 중 하나에 의해 등록 서명을 사용 하 여 또는 서명 되지 않은 패키지 (소유자 중 하나에 없으므로 등록 된 모든 인증서).

![패키지 서명자를 구성 합니다.](media/configure-package-signers.png)
