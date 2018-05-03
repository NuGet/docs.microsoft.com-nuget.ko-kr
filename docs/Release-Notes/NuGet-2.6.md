---
title: NuGet 2.6 릴리스 정보
description: 2.6.1의 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr를 포함 하 여 WebMatrix 용 NuGet에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 39ce6ac3d36464d26966b0dabb0893f09ad4afdc
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-26-release-notes"></a>NuGet 2.6 릴리스 정보

[NuGet 2.5 릴리스 정보](../release-notes/nuget-2.5.md) | [NuGet 2.6.1 WebMatrix 릴리스 정보](../release-notes/nuget-2.6.1-for-webmatrix.md)

NuGet 2.6는 2013 년 6 월 26 일에 출시 되었습니다.

## <a name="notable-features-in-the-release"></a>릴리스에서 주목할 만한 기능

### <a name="support-for-visual-studio-2013"></a>Visual Studio 2013에 대 한 지원

2.6 NuGet은 Visual Studio 2013에 대 한 지원을 제공 하는 첫 번째 릴리스입니다. 및 Visual Studio 2012와 같은 NuGet 패키지 관리자 확장은 모든 버전의 Visual Studio에 포함 되어 있습니다.

Visual Studio 2010 및 Visual Studio 2012를 지원 하 고 가능한 한 작게 확장 크기를 유지 하면서 Visual Studio 2013에 대 한 가능한 최상의 지원을 제공 하기 위해 우리을 생성 하는 동안 Visual Studio 2013에 대 한 별도 확장명은 Visual Studio 2010 및 2012를 대상으로 원래 확장명 계속 됩니다.

NuGet 2.6 이상에서는 아래와 같이 두 가지 확장 발표 합니다.

1. [NuGet 패키지 관리자](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManager) (Visual Studio 2010 및 2012에 적용)
1. [Visual Studio 2013 용 NuGet 패키지 관리자](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2013)

이 분할은 [nuget.org](https://nuget.org) 홈 페이지의 "설치 NuGet" 단추를 사용 하면는 [NuGet 설치](../install-nuget-client-tools.md) 페이지에서 다른 NuGet 클라이언트를 설치 하는 방법에 대 한 자세한 정보를 찾을 수 있습니다.

<a name="xdt"></a>

### <a name="xdt-webconfig-transformation-support"></a>XDT Web.config 변환 지원

NuGet 클라이언트에 대 한 가장 높은 요청 된 기능 중 하나는 Visual Studio 빌드 구성 변환에 사용 되는 XDT 변환 엔진을 사용 하 여 강력한 XML 변환을 지 원하는 데 되었습니다.

2013 년 4 월 XDT에 대 한 NuGet 지원에 대 한 두 개의 큰 공고가 만들었습니다. XDT 라이브러리 자체 자체 되는 첫 번째가 [NuGet 패키지로 릴리스](https://nuget.org/packages/Microsoft.Web.Xdt) 및 [CodePlex의 오픈 소싱](http://xdt.codeplex.com/)합니다. 이 단계는 NuGet 클라이언트를 포함 하 여 다른 오픈 소스 소프트웨어에서 자유롭게 사용할 XDT 엔진을 사용할 수 있습니다. 두 번째는 NuGet 클라이언트에서의 변환 XDT 엔진 사용을 지원 하도록 계획 이었습니다. NuGet 2.6이 통합이 포함 되어 있습니다.

#### <a name="how-it-works"></a>작동 방법

NuGet의 XDT 지원을 활용 하려면 메커니즘 형식은의 인수와 비슷합니다는 [현재 config 변환 기능](../create-packages/source-and-config-file-transformations.md)합니다.
변환 파일은 패키지의 콘텐츠 폴더에 추가 됩니다. 그러나 구성 변환, 설치 및 제거 모두에 대 한 단일 파일을 사용할 XDT 변환을 제어할 수 있도록 세분화 된 이러한 두 프로세스는 다음 파일을 사용 하 여:

- Web.config.install.xdt
- Web.config.uninstall.xdt

또한 NuGet 파일 접미사를 사용 하 여 기존 web.config.transforms를 사용 하 여 패키지는 계속 작동 하므로 변환에 대 한 실행 엔진을 결정 합니다. 모든 XML 파일 (뿐 아니라 web.config)에 XDT 변환을 적용할 수 활용할 수 있습니다이 다른 응용 프로그램에 대 한 프로젝트에 있도록 합니다.

#### <a name="what-you-can-do-with-xdt"></a>XDT으로 수행할 수 있습니다

XDT의 가장 큰 장점 중 하나는 해당 [간단 하지만 강력한 구문](http://msdn.microsoft.com/library/dd465326.aspx) XML dom 구조를 조작 하기 위한 다른 구조체에 하나의 고정된 문서 구조를 겹치게 단순히, 대신 XDT 일치 하는 다양 한 방식으로 완벽 하 게 XPath 지원에 일치 하는 간단한 특성 이름에서의 요소에 대 한 컨트롤을 제공 합니다. 즉, 추가, 업데이트 또는 특성을 제거, 특정 위치에 새 요소를 추가 또는 교체 또는 전체를 제거할 수 있는지 여부를 XDT의 요소를 조작 하기 위한 다양 한 기능 제공 일치 하는 요소 또는 요소 집합이 발견 되 면 요소와 해당 자식 요소입니다.

### <a name="machine-wide-configuration"></a>시스템 수준의 구성

NuGet의 훌륭한 장점 중 하나는 그렇지 않은 경우 큰 실행 파일 또는 라이브러리 하지 않을 수 있는 통합, 및 가장 중요 하 게 유지 되 고 버전 독립적으로 모듈식 구성 요소 집합으로 아래로 중단 하는 것입니다. 그러나이 한 가지 부작용이는 기존 개념 제품이 나 제품군의 잠재적으로 조각화가 심해질 수록는.
NuGet의 사용자 지정 패키지 소스 기능은; 패키지를 구성 하는 한 가지 방법은 제공 그러나 사용자 지정 패키지 원본을 모두 자체적으로 검색할 수 없습니다.

NuGet 2.6 ProgramData%/NuGet/Config % 경로 아래의 폴더 계층 구조를 검색 하 여 NuGet을 구성 하기 위한 논리를 확장 합니다. 제품 설치 관리자 제품에 대 한 사용자 지정 패키지 소스를 등록 하려면이 폴더 아래에 사용자 지정 NuGet 구성 파일을 추가할 수 있습니다. 또한 폴더 구조는 제품, 버전 및 IDE의도 SKU에 대 한 의미 체계를 지원합니다. 이러한 디렉터리에서 설정은 "마지막으로 업데이트" 우선 순위 전략에 다음 순서 대로 적용 됩니다.

1. %ProgramData%\NuGet\Config\*.config
2. %ProgramData%\NuGet\Config\{IDE}\*.config
3. %ProgramData%\NuGet\Config\{IDE}\{Version}\*.config
4. %ProgramData%\NuGet\Config\{IDE}\{Version}\{SKU}\*.config

이 목록에 {IDE} 자리 표시자 이므로 NuGet 실행 되는 IDE에 특정 Visual Studio의 경우 "visual Studio" 됩니다. {버전} 및 {SKU} 자리 표시자는 IDE에서 표시 됩니다 (예: "11.0" 및 "WDExpress", "VWDExpress" 및 "Pro" 각각). 다음 폴더에는 많은 다른 *.config 파일 포함 될 수 있습니다.
따라서 ACME 구성 요소 회사, 해당 제품 설치 관리자의 일부로 추가할 수 파일 경로 만들어 Visual Studio 2012 Professional 및 Ultimate 버전 에서만 볼 수 있는 사용자 지정 패키지 소스:

%ProgramData%\NuGet\Config\VisualStudio\11.0\Pro\acme.config

NuGet 구성 대화 상자 등록으로 패키지 소스에 사용할 수 있도록 업데이트도 폴더 구조를 사용 하면 NuGet의 구성에 시스템 수준의 패키지 소스를 추가할 소프트웨어 설치 관리자와 같은 프로그램에 대 한 간단한, 사용자 특정 (예: AppData%/NuGet/NuGet.Config %에 등록 됨) 중 하나 또는 전체 컴퓨터.

이 기능은 파일에 설치 되어 있는 Visual Studio 2013에서 활용 합니다.

%ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config

이 파일 내에서 ".NET Framework 패키지" 라고 하는 새 패키지 소스 구성 됩니다.

![NuGet Config 파일 컴퓨터 전체 설정](./media/NuGet-Config-File-Machine-Wide.png)

### <a name="contextualizing-search"></a>Contextualizing 검색

NuGet 갤러리에서 제공 하는 패키지 수가 계속 지 수 속도로 증가 하는 것을 NuGet 우선 순위 목록 맨 위에 있는 적이 남아 검색 개선 합니다. NuGet에 대 한 계획 된 기능 중 하나는 NuGet으로 사용 하 여 SKU의 Visual Studio를 사용 하는 버전 및 작성 하는 프로젝트의 유형에 대 한 정보 조건 잠재적 검색의 관련성을 확인 하기 위한 의미 하는 상황에 맞는 검색 결과입니다.

NuGet 2.6 이상에서는 패키지 설치 될 때마다 설치에 대 한 컨텍스트도 기록 됩니다 설치 작업 데이터의 일부입니다.  검색 상황에 맞는 설치 추세 하 여 검색 결과 향상 시키기 위한은 NuGet 갤러리를 사용 하면 같은 컨텍스트 정보를 보낼 수도 있습니다.  NuGet 갤러리에 대 한 이후 업데이트 하면이 상황에 맞는 관련성을 향상 시키는 수 있습니다.

### <a name="tracking-direct-installs-vs-dependency-installs"></a>Vs 직접 설치를 추적 합니다. 종속성 설치

패키지 작성자에 더 의존 됩니다는 [패키지 통계](http://blog.nuget.org/20130226/Introducing-Package-Statistics.html) 은 NuGet 갤러리에서 제공 합니다.  중요 한 누락 된 데이터 요소에 대 한 작성자 되었으며 요구 해 왔습니다 하나는 직접 패키지 설치 및 종속성 설치 간의 차이입니다.  지금까지 NuGet 클라이언트 개발자 패키지를 직접 설치 여부 또는 종속성을 충족 하기 위해 설치 된 경우의 설치 작업이 관련 된 컨텍스트를 보내지 않았습니다.
데이터가 설치 작업에 대 한 전송 되지 않음 NuGet 2.6로 시작 합니다.  NuGet 갤러리에 대 한 패키지 통계와 별도 설치 작업으로 해당 데이터에 노출 됩니다는 "-종속성" 접미사입니다.

* 설치
* 설치 종속성
* 업데이트
* 업데이트 종속성
* 다시 설치
* 종속성을 다시 설치

다른 작업 이름 외에도 종속 패키지 id는 설치에 대 한 기록 됩니다.  NuGet 갤러리에 대 한 이후 업데이트는 패키지 작성자가 개발자가 해당 패키지 설치 하는 방법을 완전히 이해 하는 보고서 내에서 해당 데이터를 노출 합니다.

## <a name="bug-fixes"></a>버그 수정

NuGet 2.6에는 다양 한 버그 수정 사항이 포함 되어 있습니다. 작업의 전체 목록은 항목에서에서 수정 된 NuGet 2.6 하십시오 보기는 [이 릴리스에 대 한 NuGet 문제 추적기](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.6&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)합니다.