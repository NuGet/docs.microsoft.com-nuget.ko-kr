---
title: 패키지 트러스트 영역 관리
description: 서명된 NuGet 패키지를 설치하고 패키지 서명 신뢰 설정을 구성하는 프로세스를 설명합니다.
author: JonDouglas
ms.author: jodou
ms.date: 11/29/2018
ms.topic: conceptual
ms.openlocfilehash: 596ce330e434253e6fb200aa59ae4e14d47779ed
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774812"
---
# <a name="manage-package-trust-boundaries"></a>패키지 트러스트 영역 관리

서명된 패키지는 특별한 조치 없이 설치할 수 있지만 패키지가 서명된 이후에 내용이 수정된 경우 설치가 차단되고 [NU3008](../reference/errors-and-warnings/NU3008.md) 오류가 발생합니다.

> [!Warning]
> 신뢰할 수 없는 인증서로 서명된 패키지는 서명되지 않은 것으로 간주되고, 다른 서명되지 않은 패키지처럼 경고나 오류 없이 설치됩니다.

## <a name="configure-package-signature-requirements"></a>패키지 서명 요구 사항 구성

> [!Note]
> Windows에 NuGet 4.9.0+ 및 Visual Studio 버전 15.9 이상 필요

[`nuget config`](../reference/cli-reference/cli-ref-config.md) 명령을 사용하여 [nuget.config](../reference/nuget-config-file.md) 파일에서 `signatureValidationMode`를 `require`로 설정하여 NuGet 클라이언트가 패키지 서명의 유효성을 검사하는 방법을 구성할 수 있습니다.

```cmd
nuget.exe config -set signatureValidationMode=require
```

```xml
  <config>
    <add key="signatureValidationMode" value="require" />
  </config>
```

이 모드는 모든 패키지가 `nuget.config` 파일에서 신뢰할 수 있는 인증서로 서명되었는지 확인합니다. 이 파일을 통해 인증서 지문에 기반하여 신뢰할 수 있는 작성자 및/또는 리포지토리를 지정할 수 있습니다.

### <a name="trust-package-author"></a>패키지 작성자 신뢰

작성자 서명에 기반하여 패키지를 신뢰하려면 [`trusted-signers`](../reference/cli-reference/cli-ref-trusted-signers.md) 명령을 사용하여 nuget.config에서 `author` 속성을 설정합니다.

```cmd
nuget.exe  trusted-signers Add -Name MyCompanyCert -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256
```

```xml
<trustedSigners>
  <author name="MyCompanyCert">
    <certificate fingerprint="CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
  </author>
</trustedSigners>
```

>[!TIP]
>`nuget.exe` [명령 확인](../reference/cli-reference/cli-ref-verify.md)을 사용하여 인증서 지문의 `SHA256` 값을 가져옵니다.


### <a name="trust-all-packages-from-a-repository"></a>리포지토리의 모든 패키지 신뢰

리포지토리 서명에 기반하여 패키지를 신뢰하려면 `repository` 요소를 사용합니다.

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
  </repository>
</trustedSigners>
```

### <a name="trust-package-owners"></a>패키지 소유자 신뢰

리포지토리 서명에는 제출 시 패키지 소유자를 판별하는 추가 메타데이터가 포함됩니다. 소유자 목록에 기반하여 리포지토리에서 패키지를 제한할 수 있습니다.

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
      <owners>microsoft;nuget</owners>
  </repository>
</trustedSigners>
```

패키지에 여러 소유자가 있고 해당 소유자 중 한 명이 신뢰할 수 있는 목록에 있는 경우 패키지 설치가 성공합니다.

### <a name="untrusted-root-certificates"></a>신뢰할 수 없는 루트 인증서

일부 상황에서는 로컬 머신에서 신뢰할 수 있는 루트에 체인되지 않은 인증서를 사용하여 확인을 활성화할 수도 있습니다. `allowUntrustedRoot` 특성을 사용하여 이 동작을 사용자 지정할 수 있습니다.

### <a name="sync-repository-certificates"></a>리포지토리 인증서 동기화

패키지 리포지토리는 [서비스 인덱스](../api/service-index.md)에서 사용하는 인증서를 알려야 합니다. 결과적으로, 리포지토리는 이러한 인증서를 업데이트하게 됩니다(예: 인증서가 만료되는 경우). 이 경우, 특정 정책이 있는 클라이언트는 새로 추가된 인증서를 포함하도록 구성을 업데이트해야 합니다. `nuget.exe` [신뢰할 수 있는 서명자 동기화 명령](../reference/cli-reference/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-name)을 사용하여 리포지토리에 연결된 신뢰할 수 있는 서명자를 쉽게 업그레이드할 수 있씁니다.

### <a name="schema-reference"></a>스키마 참조

클라이언트 정책에 대한 완전한 스키마 참조는 [nuget.config 참조](../reference/nuget-config-file.md#trustedsigners-section)에서 확인할 수 있습니다.

## <a name="related-articles"></a>관련 문서

- [NuGet 패키지 서명](../create-packages/Sign-a-Package.md)
- [서명된 패키지 참조](../reference/Signed-Packages-Reference.md)
