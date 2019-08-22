---
ms.openlocfilehash: 7ebe3c0f75b8de158879119bce4df26217849251
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488961"
---
패키지 식별자와 버전 번호는 패키지에 포함된 정확한 코드를 고유하게 식별하므로 프로젝트에서 가장 중요한 두 가지 값입니다.

**패키지 식별자에 대한 모범 사례:**

- **고유성**: 식별자는 nuget.org 또는 패키지를 호스팅하는 모든 갤러리에서 고유해야 합니다. 식별자를 결정하기 전에 해당 갤러리를 검색하여 해당 이름이 이미 사용 중인지 확인합니다. 충돌을 방지하기 위한 좋은 패턴은 회사 이름을 식별자의 첫 번째 부분(예: `Contoso.`)으로 사용하는 것입니다.
- **네임스페이스 형식의 이름**: 하이픈 대신 점 표기법을 사용하여 .NET의 네임스페이스와 비슷한 패턴을 따릅니다. 예를 들어 `Contoso-Utility-UsefulStuff` 또는 `Contoso_Utility_UsefulStuff` 대신 `Contoso.Utility.UsefulStuff`를 사용합니다. 패키지 식별자가 코드에 사용된 네임스페이스와 일치할 때 소비자가 이 형식의 이름이 유용하다는 것을 알게 됩니다.
- **샘플 패키지**: 다른 패키지를 사용하는 방법을 보여 주는 샘플 코드 패키지를 생성하는 경우 `Contoso.Utility.UsefulStuff.Sample`(와)과 같이 `.Sample`을(를) 접미사로 식별자에 붙입니다. (물론 샘플 패키지에는 다른 패키지에 대한 종속성이 있습니다.) 샘플 패키지를 만들 때는 `contentFiles`의 `<IncludeAssets>`값을 사용합니다. `content` 폴더에서 `\Samples\Contoso.Utility.UsefulStuff.Sample`과 같이 `\Samples\<identifier>`라는 폴더에 샘플 코드를 정렬합니다.

**패키지 버전에 대한 모범 사례:**

- 일반적으로 반드시 필요한 것은 아니지만 프로젝트(또는 어셈블리)의 버전과 일치하도록 패키지의 버전을 설정합니다. 이는 패키지를 단일 어셈블리로 제한할 때는 간단합니다. 전반적으로 NuGet 자체는 종속성을 확인할 때 어셈블리 버전이 아니라 패키지 버전을 처리합니다.
- 비표준 버전 구성표를 사용하는 경우 [패키지 버전 관리](../../concepts/package-versioning.md)에서 설명한 대로 NuGet 버전 관리 규칙을 고려해야 합니다. NuGet은 대부분 [semver 2와 호환](../../concepts/package-versioning.md#semantic-versioning-200)됩니다.

> 종속성 확인에 대한 자세한 내용은 [PackageReference를 사용하여 종속성 확인](../../concepts/dependency-resolution.md#dependency-resolution-with-packagereference)을 참조하세요. 버전 관리를 보다 잘 이해하는 데 도움이 될 수 있는 이전 정보는 다음의 블로그 게시물 시리지를 참조하세요.
>
> - [1부: DLL 지옥에서 가져오기](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [2부: 핵심 알고리즘](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [3부: 바인딩 리디렉션을 통한 통합](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)