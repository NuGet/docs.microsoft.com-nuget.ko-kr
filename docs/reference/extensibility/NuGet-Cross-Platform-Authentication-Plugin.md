---
title: NuGet 교차 플랫폼 인증 플러그 인
description: NuGet은 NuGet.exe "," dotnet.exe "," msbuild.exe "및" Visual Studio에 대 한 인증 플러그 인 플랫폼 간
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: b76fab1028ec9a4172d2390083fbf9adb4290a6c
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453509"
---
# <a name="nuget-cross-platform-authentication-plugin"></a>NuGet 교차 플랫폼 인증 플러그 인

4.8 이상, 클라이언트 (NuGet.exe를 Visual Studio, dotnet.exe 및 MSBuild.exe) 기반으로 구축 하는 인증 플러그 인을 사용할 수 있습니다 하는 모든 NuGet 버전에는 [플러그 인 플랫폼 간 NuGet](NuGet-Cross-Platform-Plugins.md) 모델입니다.

## <a name="authentication-in-dotnetexe"></a>Dotnet.exe에 인증

Visual Studio NuGet.exe와 기본적으로 대화형입니다. NuGet.exe 있도록 스위치를 포함 [비 대화형](../../tools/nuget-exe-CLI-Reference.md)합니다.
또한 NuGet.exe 및 Visual Studio 플러그 인 묻는 메시지를 입력 합니다.
Dotnet.exe에 메시지가 표시 되지 않습니다 되며 기본값은 비 대화형.

Dotnet.exe에 인증 메커니즘은 장치 흐름입니다. 때 복원 하거나 패키지 작업을 대화형으로 실행 하 고 작업이 차단 하는 방법에 전체 인증이 제공 됩니다 명령줄에서 사용자에 게 지침을 추가 합니다.
사용자 인증을 완료 하는 경우 작업이 계속 됩니다.

대화형 작업을 하려면 하나를 전달 해야 `--interactive`합니다.
현재는 명시적인 `dotnet restore` 및 `dotnet add package` 명령을 대화형 스위치를 지원 합니다.
대화형 스위치가 없을 `dotnet build` 고 `dotnet publish`입니다.

## <a name="authentication-in-msbuild"></a>MSBuild에서 인증

MSBuild.exe는 기본적으로 비 대화형 MSBuild.exe 인증 메커니즘은 장치 흐름 dotnet.exe 마찬가지로입니다.
일시 중지 하 고 인증에 대 한 대기에 대 한 복원을 허용 하려면 복원 호출 `msbuild -t:restore -p:NuGetInteractive="true"`합니다.

## <a name="creating-a-cross-platform-authentication-plugin"></a>플랫폼 간 인증 플러그 인 만들기

샘플 구현에서 찾을 수 있습니다 [Microsoft 자격 증명 공급자 플러그 인](https://github.com/Microsoft/artifacts-credprovider)합니다.

것 플러그 인 NuGet 클라이언트 도구에서 제시한 보안 요구 사항을 준수 하는지 매우 중요 합니다.
인증 하는 플러그 인을 되도록 플러그 인에 대 한 버전이 필요한 최소 *2.0.0*합니다.
NuGet 지원 되는 작업이 클레임에 대 한 플러그 인 및 쿼리를 사용 하 여 핸드셰이크를 수행 합니다.
플러그 인 플랫폼 간 NuGet을 참조 하십시오 [메시지 프로토콜](NuGet-Cross-Platform-Plugins.md#protocol-messages-index) 특정 메시지에 대 한 자세한 내용은 합니다.

NuGet 로그 수준을 설정 하 고 해당 하는 경우 플러그 인에 대 한 프록시 정보를 제공 합니다.
NuGet에 로깅 콘솔은만 허용 NuGet 플러그 인에는 로그 수준을 설정한 후입니다.

- .NET framework 플러그 인 인증 동작

.NET framework에서 플러그 인 대화의 형태로 입력에 대 한 사용자에 게 수 있습니다.

- .NET core 플러그 인 인증 동작

.NET Core에서 대화 상자를 표시할 수 없습니다. 플러그 인은 장치 흐름 인증을 사용 해야 합니다.
플러그 인을 사용자에 게 지침을 사용 하 여 nuget 로그 메시지를 보낼 수 있습니다.
로그 수준을 설정한 후에 플러그 인 로깅을 사용할 수 있는지 참고 합니다.
NuGet은 명령줄에서 대화형 입력을 적용 되지 않습니다.

클라이언트 가져오기 인증 자격 증명을 사용 하 여 플러그 인을 호출할 때 플러그 인 상호 작용 스위치를 준수 하 고 대화 스위치를 준수 해야 합니다. 

다음 표에서 모든 조합에 대 한 플러그 인 작동 해야 하는 방법을 보여 줍니다.

| IsNonInteractive | CanShowDialog | 플러그 인 동작 |
| ---------------- | ------------- | --------------- |
| true | true | IsNonInteractive 스위치 대화 스위치 보다 우선합니다. 대화 상자를 표시 하는 플러그 인 허용 되지 않습니다. 이 조합은.NET Framework 플러그 인에만 유효. |
| true | False | IsNonInteractive 스위치 대화 스위치 보다 우선합니다. 플러그 인을 차단 하도록 허용 되지 않습니다. 이 조합은.NET 핵심 플러그 인에만 유효. |
| False | true | 플러그 인 대화 상자가 표시 됩니다. 이 조합은.NET Framework 플러그 인에만 유효. |
| False | False | 플러그 인 해야 수는 대화 상자를 표시 합니다. 플러그 인으로 거를 통해 명령 메시지를 로깅에 의해 인증 장치 흐름을 사용 해야 합니다. 이 조합은.NET 핵심 플러그 인에만 유효. |

플러그 인을 작성 하기 전에 다음 사양을 참조 하세요.

- [NuGet 패키지 다운로드 플러그 인](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [구획 인증 플러그 인 간 NuGet](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)
