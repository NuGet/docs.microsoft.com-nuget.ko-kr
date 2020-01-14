---
title: NuGet 패키지 서명
description: 서명된 패키지를 사용하여 콘텐츠 무결성 검사를 활성화하는 방법을 설명합니다.
author: rido-min
ms.author: rmpablos
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 00fe1d5fa81132b5d6826203a0d26e56aa8d4755
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383984"
---
# <a name="signing-nuget-packages"></a>NuGet 패키지 서명

서명된 패키지는 콘텐츠 손상을 방지해 주는 콘텐츠 무결성 확인 검사를 포함합니다. 또한 패키지 서명은 패키지의 실제 원본에 대한 단일 기준 데이터(Single Source of Truth) 역할을 하고 소비자의 패키지 신뢰성을 강화합니다. 이 가이드에서는 이미 [패키지를 만들었다고](creating-a-package.md) 가정합니다.

## <a name="get-a-code-signing-certificate"></a>코드 서명 인증서 가져오기

유효한 인증서는 [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 등의 공용 인증서 기관에서 얻을 수 있으며, Windows에서 신뢰할 수 있는 인증 기관의 전체 목록은 [http://aka.ms/trustcertpartners](https://aka.ms/trustcertpartners)에서 확인할 수 있습니다.

테스트 목적으로 자체 발급된 인증서를 사용할 수 있습니다. 그러나 자체 발급된 인증서를 사용하여 서명된 패키지는 NuGet.org에서 수락되지 않습니다. [테스트 인증서 만들기](#create-a-test-certificate)에 대해 자세히 알아보세요.

## <a name="export-the-certificate-file"></a>인증서 파일 가져오기

* 인증서 내보내기 마법사를 사용하여 기존 인증서를 이진 DER 형식으로 내보낼 수 있습니다.

  ![인증서 내보내기 마법사](../reference/media/CertificateExportWizard.png)

* 또한 [Export-Certificate PowerShell 명령](/powershell/module/pkiclient/export-certificate)을 사용하여 인증서를 내보낼 수도 있습니다.

## <a name="sign-the-package"></a>패키지 서명

> [!note]
> nuget.exe 4.6.0 이상 필요. dotnet.exe 지원 서비스 예정 - [#7939](https://github.com/NuGet/Home/issues/7939)

[nuget sign](../reference/cli-reference/cli-ref-sign.md)을 사용하여 패키지에 서명:

```cli
nuget sign MyPackage.nupkg -CertificatePath <PathToTheCertificate> -Timestamper <TimestampServiceURL>
```

> [!Tip]
> 인증서 공급 기업은 위에서 표시된 `Timestamper` 선택적 인수에 사용할 수 있는 타임스탬프 서버 URL을 제공하는 경우가 많습니다. 공급 기업의 설명서 및/또는 해당 서비스 URL에 대한 지원으로 문의하세요.

* 인증서 저장소에 있는 인증서나 파일의 인증서를 사용할 수 있습니다. [nuget sign](../reference/cli-reference/cli-ref-sign.md)에 대한 CLI 참조를 참조하세요.
* 서명 인증서가 만료된 경우 서명된 패키지에 서명이 유효하다는 것을 확인해 주는 타임스탬프가 포함되어 있어야 합니다. 그렇지 않으면 서명 작업에서 [경고](../reference/errors-and-warnings/NU3002.md)가 발생합니다.
* [nuget verify](../reference/cli-reference/cli-ref-verify.md)를 사용하여 특정 패키지의 서명 정보를 확인할 수 있습니다.

## <a name="register-the-certificate-on-nugetorg"></a>NuGet.org에서 인증서 등록

서명된 패키지를 게시하려면 먼저 NuGet.org를 사용하여 인증서를 등록해야 합니다. 이진 DER 형식의 `.cer` 파일로 인증서가 필요합니다.

1. NuGet.org레 [로그인](https://www.nuget.org/users/account/LogOn?returnUrl=%2F)합니다.
1. `Account settings`(또는 조직 계정으로 인증서를 등록하려는 경우 `Manage Organization` **>** `Edit Organziation`)(으)로 이동합니다.
1. `Certificates` 섹션을 확장하고 `Register new`을 선택합니다.
1. 이전에 내보낸 인증서 파일을 찾아서 선택합니다.
  ![등록된 인증서](../reference/media/registered-certs.png)

**참고:**
* 한 명의 사용자가 여러 인증서를 제출하고 여러 사용자가 동일한 인증서를 등록할 수 있습니다.
* 한 명의 사용자에게 하나의 인증서가 등록되면 이후 모든 패키지 제출 시 이러한 인증서 중 하나로 **반드시** 서명해야 합니다. [NuGet.org에서 패키지에 대한 서명 요구 사항 관리](#manage-signing-requirements-for-your-package-on-nugetorg)를 참조하세요.
* 사용자는 계정에서 등록된 인증서를 제거할 수도 있습니다. 인증서가 제거되면 해당 인증서로 서명한 새 패키지는 제출에 실패합니다. 기존 패키지는 영향을 받지 않습니다.

## <a name="publish-the-package"></a>패키지 게시

이제 NuGet.org에 패키지를 게시할 준비가 되었습니다. [패키지 게시](../nuget-org/Publish-a-package.md)를 참조하세요.

## <a name="create-a-test-certificate"></a>테스트 인증서 만들기

테스트 목적으로 자체 발급된 인증서를 사용할 수 있습니다. 자체 발급된 인증서를 만들려면 [New-SelfSignedCertificate PowerShell 명령](/powershell/module/pkiclient/new-selfsignedcertificate)을 사용하세요.

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

이 명령은 현재 사용자의 개인 인증서 저장소에서 사용할 수 있는 테스트 인증서를 만듭니다. `certmgr.msc`를 실행하여 인증서 저장소를 열어 새로 만든 인증서를 볼 수 있습니다.

> [!Warning]
> NuGet.org는 자체 발급된 인증서로 서명된 패키지를 수락하지 않습니다.

## <a name="manage-signing-requirements-for-your-package-on-nugetorg"></a>NuGet.org에서 패키지에 대한 서명 요구 사항 관리
1. NuGet.org로 [로그인](https://www.nuget.org/users/account/LogOn?returnUrl=%2F)합니다.

1. `Manage Packages` 
   ![패키지 서명자 구성](../reference/media/configure-package-signers.png)으로 이동

* 사용자가 패키지의 유일한 소유자인 경우 필수 서명자입니다. 즉, 등록된 인증서 중 어느 것이나 사용하여 패키지를 서명한 후 NuGet.org로 게시할 수 있습니다.

* 패키지에 여러 소유자가 있는 경우 기본적으로 “임의” 소유자의 인증서를 사용하여 패키지를 서명할 수 있습니다., 패키지의 공동 소유자인 경우 본인 또는 임의의 다른 공동 소유자가 필수 사용자가 되도록 “임의”를 재정의할 수 있습니다. 등록된 인증서가 없는 소유자를 만들면 서명되지 않은 패키지가 허용됩니다. 

* 마찬가지로, 한 명의 소유자에게는 등록된 인증서가 있고 다른 소유자에게는 등록된 인증서가 없는 경우 패키지에 기본 “임의” 옵션을 선택하면 NuGet.org는 소유자 중 한 명이 등록한 서명으로 서명된 패키지 또는 서명되지 않은 패키지를 수락합니다(소유자 중 한 명에게 등록된 인증서가 없으므로).

## <a name="related-articles"></a>관련 문서

- [패키지 트러스트 영역 관리](../consume-packages/installing-signed-packages.md)
- [서명된 패키지 참조](../reference/Signed-Packages-Reference.md)
