---
title: 네이티브 NuGet 패키지 만들기
description: 관리 코드 대신 C++ 프로젝트에서 사용할 C++ 코드가 포함된 네이티브 NuGet 패키지를 만드는 방법에 대한 세부 정보입니다.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 2a95fca2ce5496512627e913273e5b66128e34c7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774206"
---
# <a name="creating-native-packages"></a>네이티브 패키지 만들기

네이티브 패키지에는 관리형 어셈블리 대신 C++(또는 유사한) 프로젝트 내에서 사용할 수 있도록 하는 네이티브 이진 파일이 포함됩니다. (사용 섹션에서 [네이티브 C++ 패키지](../consume-packages/finding-and-choosing-packages.md#native-c-packages)를 참조하세요.)

C++ 프로젝트에서 사용할 수 있으려면 패키지는 `native` 프레임워크를 대상으로 지정해야 합니다. NuGet이 모든 C++ 프로젝트를 동일하게 처리하므로 현재 이 프레임워크와 연결된 버전 번호가 없습니다.

> [!Note]
> 다른 개발자가 해당 태그를 검색하여 패키지를 찾을 수 있도록 `.nuspec`의 `<tags>` 섹션에 *네이티브* 를 포함해야 합니다.

그러면 `native`를 대상으로 지정한 네이티브 NuGet 패키지는 `\build`, `\content` 및 `\tools` 폴더에 파일을 제공합니다. `\lib`은 이 경우에 사용되지 않습니다(NuGet은 C++ 프로젝트에 직접 참조를 추가할 수 없음). NuGet에서 패키지를 사용하는 프로젝트에 자동으로 가져오는 `\build`의 대상 및 props 파일이 패키지에 포함될 수도 있습니다. `.targets` 및/또는 `.props` 확장명으로 패키지 ID와 동일하게 해당 파일의 이름을 지정해야 합니다. 예를 들어 [cpprestsdk](https://nuget.org/packages/cpprestsdk/) 패키지에는 해당 `\build` 폴더에 있는 `cpprestsdk.targets` 파일이 포함됩니다.

네이티브 패키지뿐만 아니라 모든 NuGet 패키지에 `\build` 폴더를 사용할 수 있습니다. `\build` 폴더는 `\content`, `\lib` 및 `\tools` 폴더와 같은 대상 프레임워크를 그대로 보존합니다. 즉, `\build\net40` 폴더 및 `\build\net45` 폴더를 만들 수 있습니다. 또한 NuGet에서는 적절한 props 및 대상 파일을 프로젝트로 가져옵니다. (MSBuild 대상을 가져오기 위해 PowerShell 스크립트를 사용하지 않아도 됩니다.)
