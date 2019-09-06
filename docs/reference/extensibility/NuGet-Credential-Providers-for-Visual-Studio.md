---
title: Visual Studio용 NuGet 자격 증명 공급 기업
description: NuGet 자격 증명 공급자는 Visual Studio 확장에서 IVsCredentialProvider 인터페이스를 구현 하 여 피드에 인증 합니다.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 4e781a2462871bceeb1c7f02220320daabdab98a
ms.sourcegitcommit: a0807671386782021acb7588741390e6f07e94e1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/05/2019
ms.locfileid: "70384426"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a>NuGet 자격 증명 공급자를 사용 하 여 Visual Studio에서 피드 인증

NuGet Visual Studio 확장 3.6 +는 NuGet이 인증 된 피드에 사용할 수 있도록 하는 자격 증명 공급자를 지원 합니다.
Visual Studio 용 NuGet 자격 증명 공급자를 설치 하면 NuGet Visual Studio 확장에서 필요한 경우 인증 된 피드에 대 한 자격 증명을 자동으로 획득 하 고 새로 고칩니다.

샘플 구현은 [VsCredentialProvider 샘플](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)에서 찾을 수 있습니다.

Visual Studio에서 4.8 + NuGet 부터는 새로운 플랫폼 간 인증 플러그 인도 지원 하지만 성능상의 이유로 권장 되는 방법은 아닙니다.

> [!Note]
> Visual Studio 용 NuGet 자격 증명 공급자는 일반 Visual Studio 확장으로 설치 해야 하며 [Visual studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe) 이상이 필요 합니다.
>
> Visual Studio 용 NuGet 자격 증명 공급자는 Visual Studio 에서만 작동 합니다 (dotnet restore 또는 nuget.exe는 아님). Nuget.exe를 사용 하는 자격 증명 공급자는 [Nuget.exe 자격 증명 공급자](nuget-exe-Credential-providers.md)를 참조 하세요.
> Dotnet 및 msbuild의 자격 증명 공급자의 경우 [NuGet 플랫폼 간 플러그 인](nuget-cross-platform-authentication-plugin.md) 을 참조 하세요.

## <a name="available-nuget-credential-providers-for-visual-studio"></a>Visual Studio 용 사용 가능한 NuGet 자격 증명 공급자

Visual Studio Team Services를 지원 하기 위해 Visual Studio NuGet 확장에 기본 제공 되는 자격 증명 공급자가 있습니다.

NuGet Visual Studio 확장은 플러그 인 자격 `VsCredentialProviderImporter` 증명 공급자도 검색 하는 내부를 사용 합니다. 이러한 플러그 인 자격 증명 공급자는 형식의 `IVsCredentialProvider`MEF 내보내기로 검색할 수 있어야 합니다.

사용 가능한 플러그 인 자격 증명 공급자는 다음과 같습니다.

- [Visual Studio 용 MyGet 자격 증명 공급자](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a>Visual Studio 용 NuGet 자격 증명 공급자 만들기

NuGet Visual Studio 확장 3.6 +는 자격 증명을 획득 하는 데 사용 되는 내부 CredentialService를 구현 합니다. CredentialService에는 기본 제공 및 플러그 인 자격 증명 공급자 목록이 있습니다. 각 공급자는 자격 증명을 가져올 때까지 순차적으로 시도 됩니다.

자격 증명을 획득 하는 동안 자격 증명 서비스는 다음 순서로 자격 증명 공급자를 시도 합니다. 자격 증명을 획득 하는 즉시 중지 됩니다.

1. 기본 제공 `SettingsCredentialProvider`을 사용 하 여 NuGet 구성 파일에서 자격 증명을 인출 합니다.
1. 패키지 소스가 Visual Studio Team Services `VisualStudioAccountProvider` 에 있는 경우가 사용 됩니다.
1. 다른 모든 플러그 인 Visual Studio 자격 증명 공급자는 순차적으로 시도 됩니다.
1. 모든 NuGet 교차 플랫폼 자격 증명 공급자를 순차적으로 사용 하려고 합니다.
1. 자격 증명을 아직 가져오지 않은 경우 표준 기본 인증 대화 상자를 사용 하 여 자격 증명을 입력 하 라는 메시지가 표시 됩니다.

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a>IVsCredentialProvider GetCredentialsAsync를 구현 합니다.

Visual studio 용 NuGet 자격 증명 공급자를 만들려면 `IVsCredentialProvider` 형식을 구현 하는 공용 MEF 내보내기를 제공 하는 visual studio 확장을 만들고 아래에 설명 된 원칙을 따릅니다.

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

샘플 구현은 [VsCredentialProvider 샘플](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)에서 찾을 수 있습니다.

각 Visual Studio 용 NuGet 자격 증명 공급자는 다음을 수행 해야 합니다.

1. 자격 증명 획득을 시작 하기 전에 대상 URI에 대 한 자격 증명을 제공할 수 있는지 여부를 확인 합니다. 공급자가 대상 소스에 대 한 자격 증명을 제공할 수 없는 경우를 `null`반환 해야 합니다.
1. 공급자가 대상 URI에 대 한 요청을 처리 하지만 자격 증명을 제공할 수 없는 경우 예외가 throw 됩니다.

Visual Studio 용 사용자 지정 nuget 자격 증명 공급자는 `IVsCredentialProvider` [VisualStudio 패키지](https://www.nuget.org/packages/NuGet.VisualStudio/)에서 사용할 수 있는 인터페이스를 구현 해야 합니다.

#### <a name="getcredentialasync"></a>GetCredentialAsync

| 입력 매개 변수 |설명|
| ----------------|-----------|
| Uri uri | 자격 증명을 요청 하는 패키지 원본 Uri입니다.|
| IWebProxy 프록시 | 네트워크에서 통신할 때 사용할 웹 프록시입니다. 프록시 인증을 구성 하지 않은 경우 Null입니다. |
| bool isProxyRequest | 이 요청이 프록시 인증 자격 증명을 가져오는 경우 True입니다. 구현이 프록시 자격 증명을 획득 하는 데 적합 하지 않은 경우 null이 반환 됩니다. |
| bool isRetry | 이 Uri에 대해 이전에 자격 증명을 요청 했지만 제공 된 자격 증명에서 권한 있는 액세스를 허용 하지 않은 경우 True입니다. |
| bool 비 대화형 | True 이면 자격 증명 공급자가 모든 사용자 프롬프트를 표시 하지 않고 대신 기본값을 사용 해야 합니다. |
| CancellationToken cancellationToken | 자격 증명을 요청 하는 작업이 취소 되었는지 확인 하려면이 취소 토큰을 확인 해야 합니다. |

**반환 값**: [ `System.Net.ICredentials` 인터페이스](/dotnet/api/system.net.icredentials?view=netstandard-2.0)를 구현 하는 자격 증명 개체입니다.
