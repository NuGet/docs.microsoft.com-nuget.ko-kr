---
title: NuGet 플랫폼 간 인증 플러그 인
description: Nuget .exe, dotnet, msbuild.exe 및 Visual Studio 용 NuGet 크로스 플랫폼 인증 플러그 인
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: a716737343ea826d28da6de46c32ca73aef590bd
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317273"
---
# <a name="nuget-cross-platform-authentication-plugin"></a>NuGet 플랫폼 간 인증 플러그 인

버전 4.8 +에서 모든 NuGet 클라이언트 (Nuget.exe, Visual Studio, dotnet 및 Msbuild.exe)는 [nuget 플랫폼 간 플러그 인](NuGet-Cross-Platform-Plugins.md) 모델을 기반으로 구축 된 인증 플러그 인을 사용할 수 있습니다.

## <a name="authentication-in-dotnetexe"></a>Dotnet의 인증

Visual Studio 및 Nuget.exe는 기본적으로 대화형입니다. Nuget.exe에는 [비 대화형](../nuget-exe-CLI-Reference.md)으로 만드는 스위치가 포함 되어 있습니다.
또한 Nuget.exe 및 Visual Studio 플러그 인에서 사용자에 게 입력 하 라는 메시지를 표시 합니다.
Dotnet에서 프롬프트가 표시 되지 않으며 기본값은 비 대화형입니다.

Dotnet의 인증 메커니즘은 장치 흐름입니다. 복원 또는 패키지 추가 작업이 대화형으로 실행 되는 경우 사용자에 대 한 작업 블록과 지침이 명령줄에서 제공 됩니다.
사용자가 인증을 완료 하면 작업이 계속 됩니다.

작업을 대화형으로 만들려면 한 번 통과 `--interactive`해야 합니다.
현재 명시적 `dotnet restore` 및 `dotnet add package` 명령만 대화형 스위치를 지원 합니다.
`dotnet build` 및`dotnet publish`에는 대화형 스위치가 없습니다.

## <a name="authentication-in-msbuild"></a>MSBuild의 인증

Sc.exe와 마찬가지로 Msbuild.exe는 기본적으로 비 대화형입니다. Msbuild.exe 인증 메커니즘은 장치 흐름입니다.
복원을 일시 중지 하 고 인증을 대기 하려면를 사용 하 여 `msbuild -t:restore -p:NuGetInteractive="true"`restore를 호출 합니다.

## <a name="creating-a-cross-platform-authentication-plugin"></a>플랫폼 간 인증 플러그 인 만들기

샘플 구현은 [Microsoft 자격 증명 공급자 플러그 인](https://github.com/Microsoft/artifacts-credprovider)에서 찾을 수 있습니다.

플러그 인이 NuGet 클라이언트 도구에 의해 설정 된 보안 요구 사항을 준수 하는 것이 매우 중요 합니다.
플러그 인에 대 한 플러그 인에 필요한 최소 버전은 *2.0.0*입니다.
NuGet은 플러그 인 및 지원 되는 작업 클레임에 대 한 쿼리를 사용 하 여 핸드셰이크를 수행 합니다.
특정 메시지에 대 한 자세한 내용은 NuGet 플랫폼 간 플러그 인 [프로토콜 메시지](NuGet-Cross-Platform-Plugins.md#protocol-messages-index) 를 참조 하세요.

NuGet은 로그 수준을 설정 하 고 해당 하는 경우 플러그 인에 프록시 정보를 제공 합니다.
Nuget 콘솔에 로깅은 NuGet에서 로그 수준을 플러그 인으로 설정한 후에만 사용할 수 있습니다.

- .NET Framework 플러그 인 인증 동작

.NET Framework 플러그 인은 대화 상자 형식으로 사용자에 게 입력 하 라는 메시지를 표시할 수 있습니다.

- .NET Core 플러그 인 인증 동작

.NET Core에서는 대화 상자를 표시할 수 없습니다. 플러그 인은 장치 흐름을 사용 하 여 인증 해야 합니다.
플러그 인은 사용자에 게 지침을 포함 하 여 NuGet에 로그 메시지를 보낼 수 있습니다.
로그 수준이 플러그 인으로 설정 된 후에는 로깅을 사용할 수 있습니다.
NuGet은 명령줄에서 대화형 입력을 사용 하지 않습니다.

클라이언트에서 Get Authentication 자격 증명을 사용 하 여 플러그 인을 호출 하는 경우 플러그 인은 대화형 스위치를 준수 하 고 대화 상자 스위치를 준수 해야 합니다. 

다음 표에는 플러그 인이 모든 조합에 대해 어떻게 동작 하는지 요약 되어 있습니다.

| IsNonInteractive 대화형 | CanShowDialog | 플러그 인 동작 |
| ---------------- | ------------- | --------------- |
| true | true | IsNonInteractive 대화형 스위치는 대화 상자 스위치 보다 우선적으로 적용 됩니다. 플러그 인에서 대화 상자를 표시할 수 없습니다. 이 조합은 .NET Framework 플러그 인에만 유효 합니다. |
| true | false | IsNonInteractive 대화형 스위치는 대화 상자 스위치 보다 우선적으로 적용 됩니다. 플러그 인을 차단할 수 없습니다. 이 조합은 .NET Core 플러그인에만 유효 합니다. |
| false | true | 플러그 인은 대화 상자를 표시 해야 합니다. 이 조합은 .NET Framework 플러그 인에만 유효 합니다. |
| false | false | 플러그 인은 대화 상자를 표시할 수 없습니다. 플러그 인은로 거를 통해 명령 메시지를 기록 하 여 인증 하려면 장치 흐름을 사용 해야 합니다. 이 조합은 .NET Core 플러그인에만 유효 합니다. |

플러그 인을 작성 하기 전에 다음 사양을 참조 하십시오.

- [NuGet 패키지 다운로드 플러그 인](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [NuGet 교차 cross-plat 인증 플러그 인](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)
