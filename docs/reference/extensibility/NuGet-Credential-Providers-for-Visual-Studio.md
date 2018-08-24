---
title: Visual Studio 용 NuGet 자격 증명 공급자
description: NuGet 자격 증명 공급자는 Visual Studio 확장에서 IVsCredentialProvider 인터페이스를 구현 하 여 피드를 사용 하 여 인증 합니다.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: e8d8ae22300b55b93badb65864163d959105dca2
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/23/2018
ms.locfileid: "42793905"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a>NuGet 자격 증명 공급자를 사용 하 여 Visual Studio에서 피드를 인증합니다.

NuGet Visual Studio 확장 3.6 이상 인증 된 피드를 사용 하는 NuGet을 사용 하도록 설정 된 자격 증명 공급자를 지원 합니다.
Visual Studio 용 NuGet 자격 증명 공급자를 설치 하면 NuGet Visual Studio 확장을 자동으로 획득를 필요에 따라 인증 된 피드에 대 한 자격 증명 새로 고침 합니다.

샘플 구현에서 찾을 수 있습니다 [VsCredentialProvider 샘플](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)합니다.

4.8 이상부터 Visual Studio의 NuGet도 새 플랫폼 간 인증 플러그인을 지원 하지만 성능상의 이유로 권장 되지 수도 있습니다.

> [!Note]
> Visual Studio 용 NuGet 자격 증명 공급자는 일반 Visual Studio 확장으로 설치 하 고 해야 [Visual Studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe) 이상.
>
> Visual Studio 용 NuGet 자격 증명 공급자 (나타나지 dotnet restore 또는 nuget.exe) Visual Studio 에서만 작동합니다. Nuget.exe 사용 하 여 자격 증명 공급자를 참조 하세요 [nuget.exe 자격 증명 공급자](nuget-exe-Credential-providers.md)합니다.
> Dotnet msbuild에 공급자 자격 증명에 대 한 참조 [플러그 인 플랫폼 간 NuGet](nuget-cross-platform-authentication-plugin.md)

## <a name="available-nuget-credential-providers-for-visual-studio"></a>Visual Studio 용 NuGet 자격 증명 공급자를 사용할 수 있습니다

Visual Studio Team Services를 지원 하기 위해 Visual Studio NuGet 확장에 내장 된 자격 증명 공급자가 있습니다.

내부 NuGet Visual Studio 확장을 사용 하 여 `VsCredentialProviderImporter` 또한 플러그 인 자격 증명 공급자에 대 한 검색입니다. 이러한 플러그 인 자격 증명 공급자는 형식의 MEF 내보내기를으로 검색이 가능 해야 합니다. `IVsCredentialProvider`합니다.

사용 가능한 플러그 인 자격 증명 공급자는 다음과 같습니다.

- [MyGet Credential Provider for Visual Studio 2017](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a>Visual Studio 용 NuGet 자격 증명 공급자 만들기

NuGet Visual Studio 확장 3.6 이상 자격 증명을 획득 하는 데 사용 되는 내부 CredentialService를 구현 합니다. CredentialService에 기본 제공 및 플러그 인 자격 증명 공급자의 목록이 있습니다. 각 공급자는 자격 증명을 획득 될 때까지 순차적으로 시도 됩니다.

자격 증명 획득 하는 동안 자격 증명 서비스 자격 증명을 획득 하는 즉시 중지를 다음 순서 대로 자격 증명 공급자를 시도 합니다.

1. NuGet 구성 파일에서 인출 되는 자격 증명 (기본 제공을 사용 하 여 `SettingsCredentialProvider`).
1. Visual Studio Team Services에서 패키지 원본이 있으면는 `VisualStudioAccountProvider` 사용 됩니다.
1. 다른 모든 플러그 인 Visual Studio 자격 증명 공급자는 순차적으로 시도 합니다.
1. 순차적으로 플랫폼 자격 증명 공급자 간 모든 NuGet을 사용 하려고 합니다.
1. 자격 증명 없이 아직 획득 하는 경우 표준 기본 인증 대화 상자를 사용 하 여 자격 증명에 대 한 사용자 라는 메시지가 표시 됩니다.

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a>IVsCredentialProvider.GetCredentialsAsync 구현

Visual Studio 용 NuGet 자격 증명 공급자를 만들려면 공개 MEF 내보내기 구현 하는 노출 하는 Visual Studio 확장을 `IVsCredentialProvider` 를 입력 하 고 아래에 설명 된 원칙을 준수 합니다.

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

샘플 구현에서 찾을 수 있습니다 [VsCredentialProvider 샘플](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)합니다.

Visual Studio 용 NuGet 자격 증명 공급자 각 수행 해야합니다.

1. 여부를 제공할 수 있습니다 자격 증명을 대상으로 지정 된 URI에 대 한 자격 증명 획득을 시작 하기 전에 확인 합니다. 공급자를 대상으로 지정 된 원본에 대 한 자격 증명을 제공할 수 없는 경우 반환할 `null`합니다.
1. 공급자는 대상된 URI에 대 한 요청을 처리 하는 자격 증명을 제공할 수 없습니다. 하지만 경우 예외가 throw 됩니다.

Visual Studio에 대 한 사용자 지정 NuGet 자격 증명 공급자를 구현 해야 합니다는 `IVsCredentialProvider` 에서 사용할 수 있는 인터페이스를 [참고로, NuGet.VisualStudio 패키지](https://www.nuget.org/packages/NuGet.VisualStudio/)합니다.

#### <a name="getcredentialasync"></a>GetCredentialAsync

| 매개 변수를 입력 합니다. |설명|
| ----------------|-----------|
| Uri uri | 패키지 원본에 자격 증명이 요청 되는 Uri입니다.|
| IWebProxy 프록시 | 네트워크에서 통신할 때 사용할 웹 프록시입니다. 구성 된 프록시 인증이 없는 경우 null입니다. |
| bool isProxyRequest | 이 요청은 프록시 인증 자격 증명을 가져오는 경우 true입니다. 구현에서는 프록시 자격 증명을 획득 하기 위해 유효 하지 않은, 경우에 null은 반환 되어야 합니다. |
| bool isRetry | 이 Uri에 대 한 자격 증명 이전에 요청한 하지만 제공된 된 자격 증명 권한 있는 액세스를 허용 하지 않은 경우 true입니다. |
| 비 대화형 bool | True 인 경우 자격 증명 공급자를 모든 사용자 프롬프트를 표시 하지 않으려면를 업데이트 하 고 기본 값을 대신 사용 해야 합니다. |
| CancellationToken cancellationToken | 이 취소 토큰은 작업 자격 증명을 요청 취소 되었습니다 결정할 선택 되어야 합니다. |

**값 반환**: 구현 하는 자격 증명 개체를 [ `System.Net.ICredentials` 인터페이스](/dotnet/api/system.net.icredentials?view=netstandard-2.0)합니다.
