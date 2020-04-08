---
title: NuGet.org의 개요
description: NuGet.org의 개요
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 9a75ecbc589afa664e5684005e077b02913e8039
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427018"
---
# <a name="overview-of-nugetorg"></a>NuGet.org의 개요

NuGet.org는 매일 수백만 명의 .NET 및 .NET Core 개발자가 이용하는 NuGet 패키지의 공용 호스트입니다.

## <a name="role-of-nugetorg-in-the-nuget-ecosystem"></a>NuGet 에코시스템에서의 NuGet.org의 역할

공용 호스트로서의 역할에서 NuGet.org 자체는 [nuget.org](https://www.nuget.org)에 100,000개가 넘는 고유한 패키지의 중앙 리포지토리를 유지 관리합니다. NuGet.org는 패키지의 유일한 호스트가 아닙니다. 또한 NuGet 기술을 사용하면 클라우드(예:Azure DevOps), 프라이빗 네트워크 또는 로컬 파일 시스템에서도 패키지를 전용으로 호스팅할 수 있습니다. 다른 호스트 또는 호스팅 옵션에 관심이 있다면 [사용자 고유의 NuGet 피드 호스팅](../hosting-packages/overview.md)을 참조하세요.

NuGet.org는 NuGet 패키지의 호스트와 마찬가지로 패키지 *작성자*와 패키지 *소비자* 사이의 연결 지점 역할을 합니다. 작성자는 유용한 NuGet 패키지를 빌드하고 게시합니다. 그런 다음 소비자는 액세스할 수 있는 호스트에서 유용하고 호환 가능한 패키지를 검색하고 해당 패키지를 다운로드하여 프로젝트에 포함합니다. 프로젝트에 설치되면 패키지의 API는 프로젝트 코드의 나머지 부분에서 사용할 수 있습니다.

![패키지 작성자, 패키지 호스트 및 패키지 소비자 간의 관계](media/nuget-roles.png)

## <a name="accounts"></a>계정

NuGet.org에 패키지를 게시하려면 먼저 [개별(사용자) 계정](individual-accounts.md)을 만듭니다. 이는 NuGet.org에서 사용자 ID가 됩니다.

NuGet.org에서는 [조직 계정](organizations-on-nuget-org.md)을 만들 수도 있습니다. 조직 계정은 구성원으로 하나 이상의 개별 계정을 가지고 있습니다. 멤버는 소유권에 대한 단일 ID를 유지 관리하면서 패키지 세트를 관리할 수 있습니다. 개별 계정을 통해 여러 조직의 멤버가 될 수 있습니다.

패키지는 개별 계정에 속할 수 있는 것처럼 조직 계정에 속할 수 있습니다. 패키지 소비자는 개별 계정 또는 조직 계정 간의 차이를 보지 못합니다. 둘 다 패키지 `owners`로 나타납니다.

## <a name="api-keys"></a>API 키

게시할 NuGet 패키지( *.nupkg* 파일)가 있으면 NuGet.org에서 얻은 [API 키](scoped-api-keys.md)와 함께 nuget.exe CLI 또는 dotnet.exe CLI를 사용하여 NuGet.org에 게시합니다.

[패키지를 게시](../create-packages/creating-a-package.md)하면 CLI 명령에 API 키 값이 포함됩니다.

## <a name="id-prefixes"></a>ID 접두사

패키지를 게시할 때 [ID 접두사를 예약](id-prefix-reservation.md)하여 ID를 예약 및 보호할 수 있습니다. 패키지를 설치할 때 패키지 소비자는 사용하는 패키지가 식별되는 속성에서 기만적이지 않음을 나타내는 추가 정보를 제공받습니다.

## <a name="api-endpoint-for-nugetorg"></a>NuGet.org에 대한 API 엔드포인트

NuGet 클라이언트에서 NuGet.org를 패키지 리포지토리로 사용하려면 다음과 같은 V3 API 엔드포인트를 사용해야 합니다. 

`https://api.nuget.org/v3/index.json`

이전 버전의 클라이언트는 V2 프로토콜을 사용하여 NuGet.org에 연결할 수 있습니다. 그러나 NuGet 클라이언트 3.0 이상에는 V2 프로토콜을 사용하는 느리고 신뢰할 수 없는 서비스가 포함됩니다.

`https://www.nuget.org/api/v2`(**V2 프로토콜은 더 이상 사용되지 않습니다!** )
