---
title: "Visual Studio에 대 한 자격 증명 공급자 NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/09/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "자격 증명 공급자 NuGet 피드 Visual Studio 확장에 IVsCredentialProvider 인터페이스를 구현 하 여 인증 합니다."
keywords: "NuGet 자격 증명 공급자 피드를 사용 하 여 인증, 갤러리, NuGet visual studio 확장을 사용 하 여 인증"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ff143526c814c69f1a133a62c1ad1a8f5fbedd60
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a>Visual Studio에서 NuGet 자격 증명 공급자를 사용한 피드 인증

NuGet Visual Studio 확장 3.6 이상 인증 된 피드를 사용 하는 NuGet을 사용 하도록 설정 된 자격 증명 공급자를 지원 합니다.
Visual Studio 용 NuGet 자격 증명 공급자를 설치한 후 Visual Studio 확장 자동으로 확보 하 고 필요에 따라 인증 된 피드에 대 한 자격 증명을 새로 고칩니다.

샘플 구현을 찾을 수 있습니다 [VsCredentialProvider 샘플](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)합니다.

> [!Note]
> Visual Studio에 대 한 자격 증명 공급자 NuGet 일반 Visual Studio 확장으로 설치 되어 있어야 하며 내용의 [Visual Studio 2017](https://aka.ms/vs/15/preview/vs_enterprise) (현재 미리 보기)에 이상.
>
> Visual Studio 용 NuGet 자격 증명 공급자 (에 없는 dotnet 복원 또는 nuget.exe) Visual Studio 에서만 작동합니다. Nuget.exe와 자격 증명 공급자를 참조 하십시오. [nuget.exe 자격 증명 공급자](nuget-exe-Credential-providers.md)합니다.

## <a name="available-nuget-credential-providers-for-visual-studio"></a>Visual Studio 용 NuGet 자격 증명 공급자를 사용할 수 있는

Visual Studio Team Services를 지원 하기 위해 Visual Studio NuGet 확장에 기본 제공 자격 증명 공급자가 있습니다.

Visual Studio Extension NuGet를 사용 하 여 내부 `VsCredentialProviderImporter` 도 플러그 인 자격 증명 공급자 검색입니다. 이러한 플러그 인 자격 증명 공급자는 형식의 MEF 내보낼 처럼 검색이 가능 해야 합니다. `IVsCredentialProvider`합니다.

사용 가능한 플러그 인 자격 증명 공급자는 다음과 같습니다.

- [MyGet Credential Provider for Visual Studio 2017](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a>Visual Studio 용 NuGet 자격 증명 공급자 만들기

NuGet Visual Studio 확장 3.6 +는 자격 증명을 획득 하는 데 사용 되는 내부 CredentialService을 구현 합니다. CredentialService에 기본 제공 및 플러그 인 자격 증명 공급자의 목록이 있습니다. 각 공급자는 자격 증명 획득 될 때까지 순차적으로 시도 됩니다.

자격 증명 획득 하는 동안 자격 증명 서비스 자격 증명 공급자 자격 증명 획득 되는 즉시 중지 하는 다음 순서 대로 시도 합니다.

1. NuGet 구성 파일에서 인출 되는 자격 증명 (기본 제공을 사용 하 여 `SettingsCredentialProvider`).
1. 패키지 원본이 Visual Studio Team Services에 있으면는 `VisualStudioAccountProvider` 사용 됩니다.
1. 다른 모든 플러그 인 자격 증명 공급자를 순차적으로 시도 합니다.
1. 자격 증명이 없는 아직 획득 하는 경우 자격 증명 표준 기본 인증 대화 상자를 사용 하 여 사용자를 입력 합니다.

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a>IVsCredentialProvider.GetCredentialsAsync 구현

Visual Studio 용 NuGet 자격 증명 공급자를 만들려면 공용 MEF 내보내기 구현 하는 노출 하는 Visual Studio 확장을 만듭니다는 `IVsCredentialProvider` 를 입력 하 고 아래에서 설명 하는 원칙을 준수 합니다.

```cs
public interface IVsCredentialProvider
{
    Task<ICredentials> GetCredentialsAsync(
        Uri uri,
        IWebProxy proxy,
        bool isProxyRequest,
        bool isRetry,
        bool nonInteractive,
        CancellationToken cancellationToken);
}
```

샘플 구현을 찾을 수 있습니다 [VsCredentialProvider 샘플](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)합니다.

Visual Studio 용 NuGet 자격 증명 공급자 각 수행 해야합니다.

1. 있는지 여부를 제공할 수 있습니다 자격 증명의 대상된 URI에 대 한 자격 증명 획득을 시작 하기 전에 확인 합니다. 공급자 대상으로 지정 된 원본에 대 한 자격 증명을 제공할 수 없는 경우 다음을 반환 해야 `null`합니다.
1. 대상된 URI에 대 한 요청을 처리 하는 공급자 자격 증명을 제공할 수 없는 경우 예외가 throw 해야 합니다.

Visual Studio에 대 한 사용자 지정 NuGet 자격 증명 공급자를 구현 해야는 `IVsCredentialProvider` 에서 사용할 수 있는 인터페이스는 [NuGet.VisualStudio 패키지](https://www.nuget.org/packages/NuGet.VisualStudio/)합니다.

#### <a name="getcredentialasync"></a>GetCredentialAsync

| 입력된 매개 변수 |설명|
| ----------------|-----------|
| Uri uri | 패키지 원본에 자격 증명이 요청 Uri입니다.|
| IWebProxy 프록시 | 네트워크에서 통신에 사용할 웹 프록시입니다. 구성 된 프록시 인증이 없는 경우 null입니다. |
| bool isProxyRequest | True 이면이 요청은 프록시 인증 자격 증명을 가져옵니다. 프록시 자격 증명을 얻는 데 유효 하지 않으면 구현 하는 경우 null 반환 합니다. |
| bool isRetry | True 자격 증명 이전에이 Uri에 대해 요청 된 있지만 제공 된 자격 증명 권한이 부여 된 액세스를 허용 하지 않았습니다. |
| 비 대화형 bool | True 인 경우, 자격 증명 공급자는 모든 사용자 프롬프트를 표시 하지 않는 하 고 기본값을 대신 사용 해야 합니다. |
| CancellationToken cancellationToken | 이 취소 토큰을 선택 하 여를 작업 요청 자격 증명 취소 되었습니다 결정 해야 합니다. |

**반환 값**: 구현 하는 자격 증명 개체는 [ `System.Net.ICredentials` 인터페이스](/dotnet/api/system.net.icredentials?view=netstandard-2.0)합니다.
