---
title: NuGet 5.1 RTM 릴리스 정보
description: 새 기능, 버그 수정 및 Ecrs를 비롯 한 NuGet 5.1에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 05/21/2019
ms.topic: conceptual
ms.openlocfilehash: 2a94360dc375ba90b90c1045f4acbcfca81fea5b
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699864"
---
# <a name="nuget-51-release-notes"></a>NuGet 5.1 릴리스 정보

NuGet 배포 차량:

| NuGet 버전 | Visual Studio 버전에서 사용 가능| .NET SDK에서 사용 가능|
|:---|:---|:---|
| [**5.1.0**](https://nuget.org/downloads) | [Visual Studio 2019 버전 16.1](https://visualstudio.microsoft.com/downloads/) | [2.1.70 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup> .NET Core 워크 로드와 함께 Visual Studio 2019와 함께 설치 됨 

<sup>2</sup> .NET Core 워크 로드와 함께 Visual Studio 2019을 사용 하 여 선택적으로 설치할 수 있습니다.

## <a name="summary-whats-new-in-51"></a>요약: 5.1의 새로운 기능

* CI/CD 워크플로와의 통합이 가능 하도록 패키지 푸시가 이미 있는 경우이를 건너뛰도록 지원- [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)

* 이제 Visual Studio에서 패키지의 nuget.org 갤러리 페이지에 대 한 편리한 링크를 제공 [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)

* 새 .NET Core 3.0 자산에 대 한 지원 (예: [대상 팩](https://github.com/dotnet/cli/issues/10006) 및 [런타임 팩](https://github.com/dotnet/cli/issues/10007) )
  * FrameworkReferences에서 대상 지정 및 런타임 패키지 참조를 사용할 수 있도록 하는 NuGet 팩 및 복원 지원- [#7342](https://github.com/NuGet/Home/issues/7342)
  * PackageDownload를 사용 하 여 "다운로드 전용" 패키지 시나리오를 지원 [#7339](https://github.com/NuGet/Home/issues/7339)
  * PackageType를 사용 하 여 & 복원 그래프 검색 결과에서 런타임 및 대상 팩을 제외 [#7337](https://github.com/NuGet/Home/issues/7337)

### <a name="issues-fixed-in-this-release"></a>이번 릴리스에서 수정된 문제

**버그**

* 플러그 인: 플러그 인을 만드는 동안 예외 정보 손실- [#8057](https://github.com/NuGet/Home/issues/8057)

* 하한값이 원본 중 하나에 있는 경우에는 하 한이 아닌 PackageReference 범위가 작동 하지 않습니다. - [#8054](https://github.com/NuGet/Home/issues/8054)

* IsPackableFalseError 메시지 개선- [#8021](https://github.com/NuGet/Home/issues/8021)

* 패키지 잠금 파일-프로젝트 그래프가 변경 될 때 잠금 파일 다시 생성- [#8019](https://github.com/NuGet/Home/issues/8019)

* ProjectSystem 버그: 자동으로 제거 되는 Nuget 패키지- [#8017](https://github.com/NuGet/Home/issues/8017)

* CollectPackageDownloads 및 CollectPackageReferences와 유사한 FrameworkReference를 반환 하기 위한 대상을 추가 [#8005](https://github.com/NuGet/Home/issues/8005)

* HTTP 캐시: RepositoryResources 리소스는 버전이 지정 된 방식으로 캐시 되지 않습니다.- [#7997](https://github.com/NuGet/Home/issues/7997)

* 로깅: 예외 호출 스택 상세 세부 정보 표시로 보고 되지 않습니다. [#7955](https://github.com/NuGet/Home/issues/7955)

* 모든 NuGet 문서 Url을 변경 하 여 HTTPS를 사용 합니다. [#7950](https://github.com/NuGet/Home/issues/7950)

* NU3024 경고 메시지 개선- [#7933](https://github.com/NuGet/Home/issues/7933)

* packagereference 제거 될 때 잠금 파일 업데이트 안 함- [#7930](https://github.com/NuGet/Home/issues/7930)

* Nuspec에서 licenseurl 및 license 요소의 유효성을 검사할 때 오류 사례 처리를 향상 시킵니다 [#7915](https://github.com/NuGet/Home/issues/7915)

* PM UI-탭 헤더를 마우스 오른쪽 단추로 클릭 하 고 "파일 위치 열기"를 클릭 하면 오류가 발생 합니다. [#7913](https://github.com/NuGet/Home/issues/7913)

* 플러그 인: 플러그 인 프로세스가 종료 될 때 기록- [#7907](https://github.com/NuGet/Home/issues/7907)

* 플러그 인: datetime 값 로깅의 높은 충돌 률- [#7899](https://github.com/NuGet/Home/issues/7899)

* 매니페스트. [#7894](https://github.com/NuGet/Home/issues/7894) LicenseExpression를 사용 하 여 Nuspec에서 readfrom이 실패 합니다.

* RestoreLockedMode: ProjectReference가 사용자 지정 AssemblyName- [#7889](https://github.com/NuGet/Home/issues/7889) 프로젝트를 참조 하는 경우 예기치 않은 NU1004

* 예외가 발생 하 여 플러그 인 시작이 실패할 경우 더 나은 오류 메시지 [#7857](https://github.com/NuGet/Home/issues/7857)

* NoOp 복원 작업을 수행 하는 경우에는 .dgspec.js[#7854](https://github.com/NuGet/Home/issues/7854) obj 디렉터리에 쓸 필요가 없습니다.

* GeneratePathProperty = true 인 경우 대/소문자 불일치 시 속성이 생성 되지 않습니다.- [#7843](https://github.com/NuGet/Home/issues/7843)

* 설정: 패키지 원본 경로에 잘못 된 문자가 있을 수 있습니다. VS- [#7820](https://github.com/NuGet/Home/issues/7820)

* 잠금 파일이 삭제 된 경우 NoOp- [#7807](https://github.com/NuGet/Home/issues/7807) 에서 잠금 파일을 생성 하지 않습니다.

* 라이선스 URL 및 라이선스 때문에 메타 데이터를 읽는 동안 오류가 발생 했습니다.- [#7547](https://github.com/NuGet/Home/issues/7547)

* V2FeedParser의 처리 되지 않은 예외- [#7523](https://github.com/NuGet/Home/issues/7523)

* 잘못 된 인수에 대 한 nuget.exe 종료 코드 0을 반환 합니다. [#7178](https://github.com/NuGet/Home/issues/7178)

* 서명 관련 시나리오를 반영 하 여 오류 및 경고 문서 업데이트- [#6498](https://github.com/NuGet/Home/issues/6498)

* 자산 파일은 상대 경로를 사용 하 여 프로젝트를 보다 쉽게 이동할 수 있도록 합니다. [#4582](https://github.com/NuGet/Home/issues/4582)

**DCR**

* 플러그 인: 진단 로깅 사용- [#7859](https://github.com/NuGet/Home/issues/7859)

* Tizen 6 map을 NetStandard 2.1로 설정- [#7773](https://github.com/NuGet/Home/issues/7773)

**[이 릴리스에서 해결 된 모든 문제 목록-5.1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**
