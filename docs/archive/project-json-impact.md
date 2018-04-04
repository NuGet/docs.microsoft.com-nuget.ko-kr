---
title: NuGet 패키지 작성자에게 미치는 project.json 영향 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: NuGet 3.x에서 project.json의 구현이 지원되지 않는 기능, 콘텐츠 및 패키지 형식 등 패키지 작성자에 영향을 주는 방법에 대한 세부 정보입니다.
keywords: NuGet 및 project.json, project.json 영향, 패키지 작성 고려 사항, project.json 기능
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 6e8af98504a2866106e84943989aeb91f2e9c1fb
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="impact-of-projectjson-when-creating-packages"></a>패키지를 만들 때 project.json의 영향

> [!Important]
> 이 콘텐츠는 더 이상 사용되지 않습니다. 프로젝트는 `packages.config` 또는 PackageReference 형식을 사용해야 합니다.

NuGet 3+에서 사용되는 `project.json` 시스템은 다음 섹션에 설명된 대로 여러 가지 방법으로 패키지 작성자에 영향을 줍니다.

## <a name="changes-affecting-existing-packages-usage"></a>기존 패키지 사용에 영향을 주는 변경 내용

기존의 NuGet 패키지는 전이적 권역으로 이전되지 않는 기능 집합을 지원합니다.

### <a name="install-and-uninstall-scripts-are-ignored"></a>스크립트 설치 및 제거 무시

[종속성 확인](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference)에 설명된 전이적 복원 모델에는 "패키지 설치 시간"이라는 개념이 없습니다. 패키지가 표시되거나 표시되지 않지만 패키지를 설치할 때 발생하는 일관된 프로세스가 없습니다.

또한 스크립트 설치가 Visual Studio에서만 지원되었습니다. 기타 IDE는 이러한 스크립트를 지원하려는 Visual Studio 확장성 API를 거절했으므로 일반적인 편집기 및 명령줄 도구에서 지원을 사용할 수 없었습니다.

### <a name="content-transforms-are-not-supported"></a>콘텐츠 변환이 지원되지 않습니다.

스크립트 설치와 마찬가지로 변환은 패키지 설치에서 실행되며 일반적으로 idempotent가 아닙니다. 더 이상 설치 시간이 없으므로 XDT 변환 및 비슷한 기능이 지원되지 않으며 이러한 패키지가 전이적 시나리오에서 사용되는 경우 무시됩니다.

### <a name="content"></a>콘텐츠

기존 NuGet 패키지는 소스 코드 및 구성 파일 등의 콘텐츠 파일을 제공합니다. 일반적으로 두 가지 시나리오에서 사용됩니다.

1. 초기 파일은 사용자가 나중에 편집할 수 있도록 프로젝트에 삭제되었습니다. 일반적인 예제는 기본 구성 파일입니다.

1. 콘텐츠 파일은 프로젝트에 설치된 어셈블리에 대한 추가 기능으로 사용됩니다. 다음 예제는 어셈블리에서 사용하는 로고 이미지입니다.

스크립트 및 변환에서 비슷한 이유로 콘텐츠에 대한 지원을 현재 사용할 수 없지만 콘텐츠에 대한 지원을 설계하려고 노력하고 있습니다.

콘텐츠 파일은 패키지 내에서 계속 수행될 수 있으며 현재 무시되지만 최종 사용자는 해당 파일을 여전히 올바른 위치에 복사합니다.

콘텐츠 파일을 가져오는 제안 중 하나를 참조하여 다음에서 진행을 따를 수 있습니다. [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)

## <a name="impact-for-package-authors"></a>패키지 작성자에 대한 영향

위의 기능을 사용하는 패키지는 다른 메커니즘을 사용해야 합니다. 이를 위한 가장 일반적으로 유용한 메커니즘은 계속 완벽하게 지원되는 MSBuild 대상/props일 수 있습니다. 빌드 시스템에서는 패키지의 다른 규칙을 선택할 수 있습니다. Roslyn 분석기뿐만 아니라 MSBuild 대상이 지원되는 방식입니다. `packages.config` 및 `project.json` 시나리오에서 대상 및 분석기를 지원하는 패키지를 빌드할 수 있습니다.

일반적으로 쉽게 시작하도록 프로젝트를 수정하려고 하는 패키지는 매우 제한된 일련의 시나리오에서 작동하며 대신 패키지를 사용하는 방법에 대한 추가 정보 또는 지침을 제공해야 합니다.

대부분의 기존 패키지는 아래에 설명된 패키지 형식을 사용할 필요가 없습니다.

이 형식은 네이티브 콘텐츠를 최고 수준의 시나리오로 활성화합니다. 즉, 대상 플랫폼을 기반으로 하여 관리되는 어셈블리와 함께 이진 구현을 제공하도록 하드웨어 구현에 가까운 관리되는 어셈블리를 사용합니다. 예를 들어 System.IO.Compression 패키지는 이 기술을 활용합니다. [https://www.nuget.org/packages/System.IO.Compression](https://www.nuget.org/packages/System.IO.Compression)

요약에서 위의 기능이 반드시 필요하지 않은 경우 여기에 설명된 형식이 NuGet 3.x+에서만 지원되므로 기존 패키지 형식을 사용하는 것이 좋습니다.

shim을 통해 `packages.config` 및 `project.json`를 통해 시나리오 둘 다에서 작동하도록 패키지를 빌드할 수 있지만 종종 위에서 언급한 사용되지 않는 기능 없이 전통적인 방법으로 패키지를 구성하는 것이 더 간단합니다.

## <a name="3x-package-format"></a>3.x 패키지 형식

3.x 패키지 형식은 NuGet 2.x 이외에 몇 가지 추가 기능에서 허용됩니다.

1. 다른 플랫폼/장치에서 런타임에 사용되는 컴파일 및 일련의 구현 어셈블리에 사용되는 참조 어셈블리를 정의합니다. 그러면 소비자에게 일반적인 노출 영역을 제공하면서 플랫폼 특정 API를 활용할 수 있습니다. 그러면 특히 중간 이식 가능한 라이브러리를 쉽게 작성할 수 있습니다.

1. 패키지가 플랫폼(예: 운영 체제 또는 CPU 아키텍처)에서 피벗할 수 있습니다.

1. 플랫폼 특정 구현을 구분하기 위해 추가 기능 패키지를 허용합니다.

1. 네이티브 종속성을 1급 객체로 지원합니다.
