---
title: "NuGet 패키지 만들기에 대한 개요 및 워크플로 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 07/26/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet 패키지를 만들고 게시하는 프로세스를 간략히 설명하며, 프로세스의 다른 특정 부분에 대한 링크가 포함되어 있습니다."
keywords: "NuGet 패키지 만들기, NuGet 만들기 개요, NuGet 만들기 워크플로, 패키지 만들기 워크플로, 패키지 만들기 개요."
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 46d7737d57a91ee7b0434f4695c393423730c7bc
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2018
---
# <a name="package-creation-workflow"></a>패키지 만들기 워크플로

패키지를 만드는 작업은 공용 nuget.org 갤러리 또는 조직 내의 전용 갤러리를 통해 패키지하고 다른 사람들과 공유하려는 컴파일된 코드(일반적으로 .NET 어셈블리)로 시작합니다. 패키지에는 패키지를 설치할 때 표시되는 추가 정보와 같은 추가 파일이 포함될 수 있으며, 특정 프로젝트 파일에 대한 변환이 포함될 수 있습니다.

또한 패키지는 자체의 코드를 포함하지 않고 임의 개수의 다른 종속성만 끌어올 수도 있습니다. 이러한 패키지는 여러 독립적인 패키지로 구성된 SDK를 제공하는 편리한 방법입니다. 다른 경우에는 디버깅을 지원하기 위해 기호(`.pdb`) 파일만 패키지에 포함될 수 있습니다.

> [!Note]
> 다른 개발자가 사용할 패키지를 만드는 경우 개발자가 사용자의 작업에 의존하고 있음을 이해하는 것이 중요합니다. 이와 같이 패키지를 만들고 게시하는 것은 버그를 수정하고 다른 업데이트를 만들거나 최소한 패키지를 오픈 소스로 사용할 수 있게 하여 다른 사람들이 패키지를 유지 관리할 수 있도록 하기 위한 약속을 의미합니다.

어떤 경우이든 패키지를 만드는 작업은 패키지할 어셈블리와 다른 파일을 결정하는 것으로 시작합니다. 그런 다음 식별자, 버전 번호, 저작권 정보, MSBuild props 및 targets와 함께 패키지의 내용을 설명하는 `.nuspec` 파일이라고 하는 매니페스트 파일을 만듭니다.

적절한 폴더에 필요한 모든 파일을 준비하고 적절한 `.nuspec` 파일을 만들었으면 `nuget pack` 명령(또는 [MSBuild pack 대상](../reference/msbuild-targets.md))을 사용하여 모든 파일을 함께 `.nupkg` 파일에 넣습니다. 그러면 다른 개발자가 사용할 수 있는 모든 호스트에 패키지를 배포할 준비가 되었습니다.

> [!Tip]
> `.nupkg` 확장명이 있는 NuGet 패키지는 단순히 ZIP 파일입니다. 패키지의 내용을 쉽게 검사하려면 확장명을 `.zip`으로 변경하고 평소와 같이 해당 내용을 펼쳐봅니다. 호스트에 업로드하기 전에 확장명을 `.nupkg`로 다시 변경해야 합니다.

만들기 프로세스를 알아보고 이해하려면 [패키지 만들기](../create-packages/creating-a-package.md)부터 시작하여 모든 패키지에 공통적인 핵심 프로세스를 안내합니다.

이러한 프로세스에서 패키지에 대한 여러 가지 다른 옵션을 고려할 수 있습니다.

- [여러 대상 프레임워크 지원](../create-packages/supporting-multiple-target-frameworks.md)에서는 다양한 .NET Framework에 대해 여러 변형을 사용하여 패키지를 만드는 방법에 대해 설명합니다.
- [지역화된 패키지 만들기](../create-packages/creating-localized-packages.md)에서는 여러 언어 리소스가 있는 패키지를 구성하는 방법과 별도의 지역화된 위성 패키지를 사용하는 방법에 대해 설명합니다.
- [시험판 패키지](../create-packages/prerelease-packages.md)는 알파, 베타 및 RC 패키지를 관심 있는 고객에게 공개하는 방법을 보여줍니다.
- [원본 및 구성 파일 변환](../create-packages/source-and-config-file-transformations.md)은 프로젝트에 추가된 파일에서 단방향 토큰 대체를 수행하는 방법과 패키지가 제거될 때 취소되는 설정으로 `web.config` 및 `app.config`를 수정하는 방법에 대해 설명합니다.
- [기호 패키지](../create-packages/symbol-packages.md)는 사용자가 코드를 단계별로 실행하면서 디버그할 수 있도록 라이브러리에 대한 기호를 제공하기 위한 지침을 제공합니다.
- [패키지 버전 관리](../reference/package-versioning.md)에서는 종속성을 허용하는 정확한 버전(패키지에서 사용하는 다른 패키지)을 식별하는 방법에 대해 설명합니다.
- [네이티브 패키지](../create-packages/native-packages.md)는 C++ 소비자용 패키지를 만드는 프로세스를 설명합니다.

다음으로 nuget.org에 패키지를 게시할 준비가 되면 [패키지 게시](../create-packages/publish-a-package.md)의 간단한 프로세스를 수행합니다.

nuget.org 대신 개인 피드를 사용하려면 [패키지 호스팅 개요](../hosting-packages/overview.md)를 참조하세요.
