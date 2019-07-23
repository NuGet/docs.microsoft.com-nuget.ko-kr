---
title: NuGet 패키지 만들기에 대한 개요 및 워크플로
description: NuGet 패키지를 만들고 게시하는 프로세스를 간략히 설명하며, 프로세스의 다른 특정 부분에 대한 링크가 포함되어 있습니다.
author: karann-msft
ms.author: karann
ms.date: 07/26/2017
ms.topic: conceptual
ms.openlocfilehash: 58ad05cb854c8f7233d90d03c1b320f8797ca2ab
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842394"
---
# <a name="package-creation-workflow"></a>패키지 만들기 워크플로

패키지를 만드는 작업은 공용 nuget.org 갤러리 또는 조직 내의 전용 갤러리를 통해 패키지하고 다른 사람들과 공유하려는 컴파일된 코드(일반적으로 .NET 어셈블리)로 시작합니다. 패키지에는 패키지를 설치할 때 표시되는 추가 정보와 같은 추가 파일이 포함될 수 있으며, 특정 프로젝트 파일에 대한 변환이 포함될 수 있습니다.

또한 패키지는 자체의 코드를 포함하지 않고 임의 개수의 다른 종속성만 끌어올 수도 있습니다. 이러한 패키지는 여러 독립적인 패키지로 구성된 SDK를 제공하는 편리한 방법입니다. 다른 경우에는 디버깅을 지원하기 위해 기호(`.pdb`) 파일만 패키지에 포함될 수 있습니다.

> [!Note]
> 다른 개발자가 사용할 패키지를 만드는 경우 개발자가 사용자의 작업에 의존하고 있음을 이해하는 것이 중요합니다. 이와 같이 패키지를 만들고 게시하는 것은 버그를 수정하고 다른 업데이트를 만들거나 최소한 패키지를 오픈 소스로 사용할 수 있게 하여 다른 사람들이 패키지를 유지 관리할 수 있도록 하기 위한 약속을 의미합니다.

어떤 경우든 패키지 만들기는 해당 식별자, 버전 번호, 라이선스, 저작권 정보 및 기타 필요한 콘텐츠를 결정하는 것부터 시작됩니다. 완료되면 "pack" 명령을 사용하여 모든 항목을 `.nupkg` 파일에 포함할 수 있습니다. 이 파일은 nuget.org와 같은 NuGet 피드에 게시할 수 있습니다.

> [!Tip]
> `.nupkg` 확장명이 있는 NuGet 패키지는 단순히 ZIP 파일입니다. 패키지의 내용을 쉽게 검사하려면 확장명을 `.zip`으로 변경하고 평소와 같이 해당 내용을 펼쳐봅니다. 호스트에 업로드하기 전에 확장명을 `.nupkg`로 다시 변경해야 합니다.

만들기 프로세스를 알아보고 이해하려면 [패키지 만들기](../create-packages/creating-a-package.md)부터 시작하여 모든 패키지에 공통적인 핵심 프로세스를 안내합니다.

이러한 프로세스에서 패키지에 대한 여러 가지 다른 옵션을 고려할 수 있습니다.

- [여러 대상 프레임워크 지원](../create-packages/supporting-multiple-target-frameworks.md)에서는 다양한 .NET Framework에 대해 여러 변형을 사용하여 패키지를 만드는 방법에 대해 설명합니다.
- [지역화된 패키지 만들기](../create-packages/creating-localized-packages.md)에서는 여러 언어 리소스가 있는 패키지를 구성하는 방법과 별도의 지역화된 위성 패키지를 사용하는 방법에 대해 설명합니다.
- [시험판 패키지](../create-packages/prerelease-packages.md)는 알파, 베타 및 RC 패키지를 관심 있는 고객에게 공개하는 방법을 보여줍니다.
- [원본 및 구성 파일 변환](../create-packages/source-and-config-file-transformations.md)은 프로젝트에 추가된 파일에서 단방향 토큰 대체를 수행하는 방법과 패키지가 제거될 때 취소되는 설정으로 `web.config` 및 `app.config`를 수정하는 방법에 대해 설명합니다.
- [기호 패키지](../create-packages/symbol-packages-snupkg.md)는 사용자가 코드를 단계별로 실행하면서 디버그할 수 있도록 라이브러리에 대한 기호를 제공하기 위한 지침을 제공합니다.
- [패키지 버전 관리](../reference/package-versioning.md)에서는 종속성을 허용하는 정확한 버전(패키지에서 사용하는 다른 패키지)을 식별하는 방법에 대해 설명합니다.
- [네이티브 패키지](../create-packages/native-packages.md)는 C++ 소비자용 패키지를 만드는 프로세스를 설명합니다.
- [패키지 서명](../create-packages/sign-a-package.md)에서는 패키지에 디지털 서명을 추가하는 프로세스를 설명합니다.

다음으로 nuget.org에 패키지를 게시할 준비가 되면 [패키지 게시](../nuget-org/publish-a-package.md)의 간단한 프로세스를 수행합니다.

nuget.org 대신 개인 피드를 사용하려면 [패키지 호스팅 개요](../hosting-packages/overview.md)를 참조하세요.
