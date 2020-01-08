---
title: NuGet 2.6 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 Ecrs를 포함 하 여 WebMatrix 용 NuGet 2.6.1에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5e80965aad4caa69130be31a37b7f5f5ffb12ea6
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384126"
---
# <a name="nuget-26-release-notes"></a>NuGet 2.6 릴리스 정보

[Nuget 2.5 릴리스 정보](../release-notes/nuget-2.5.md) | [WebMatrix 2.6.1 For WebMatrix 릴리스 정보](../release-notes/nuget-2.6.1-for-webmatrix.md)

NuGet 2.6은 2013 년 6 월 26 일에 출시 되었습니다.

## <a name="notable-features-in-the-release"></a>릴리스의 주요 기능

### <a name="support-for-visual-studio-2013"></a>Visual Studio 2013에 대 한 지원

NuGet 2.6는 Visual Studio 2013에 대 한 지원을 제공 하는 첫 번째 릴리스입니다. Visual Studio 2012와 마찬가지로, NuGet 패키지 관리자 확장은 Visual Studio의 모든 버전에 포함 되어 있습니다.

Visual Studio 2010 및 Visual Studio 2012를 모두 지원 하 고 확장 크기를 Visual Studio 2013 가능한 한 작게 유지 하면서 Visual Studio 2013에 대 한 최상의 지원을 제공 하기 위해 원래 확장은 Visual Studio 2010 및 2012를 모두 대상으로 합니다.

NuGet 2.6부터 다음과 같이 두 개의 확장을 게시 합니다.

1. [NuGet 패키지 관리자](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManager) (Visual Studio 2010 및 2012에 적용 됨)
1. [Visual Studio 2013에 대 한 NuGet 패키지 관리자](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2013)

이 분할을 사용 하면 [nuget.org](https://nuget.org) 홈 페이지의 "nuget 설치" 단추를 클릭 하 여 [nuget 설치](../install-nuget-client-tools.md) 페이지로 이동 하 여 다른 nuget 클라이언트를 설치 하는 방법에 대 한 자세한 정보를 찾을 수 있습니다.

<a name="xdt"></a>

### <a name="xdt-webconfig-transformation-support"></a>Web.config 변환 지원 XDT

NuGet 클라이언트에 대해 가장 많이 요청 되는 기능 중 하나는 Visual Studio 빌드 구성 변환에 사용 되는 XDT 변환 엔진을 사용 하 여 더 강력한 XML 변환을 지원 하기 위한 것입니다.

2013 년 4 월에는 NuGet 지원과 관련 하 여 XDT에 대 한 두 가지 큰 공지를 만들었습니다. 첫 번째는 XDT 라이브러리 자체가 [NuGet 패키지로 릴리스](https://nuget.org/packages/Microsoft.Web.Xdt) 되었으며 [CodePlex에서 오픈](http://xdt.codeplex.com/)소스 였습니다. 이 단계를 통해 NuGet 클라이언트를 비롯 한 다른 오픈 소스 소프트웨어에서 자유롭게 XDT 엔진을 사용할 수 있습니다. 두 번째 알림은 NuGet 클라이언트의 변환에 XDT 엔진을 사용할 수 있도록 지 원하는 계획 이었습니다. NuGet 2.6은 이러한 통합을 포함 합니다.

#### <a name="how-it-works"></a>작동 방법

NuGet의 XDT 지원 기능을 활용 하기 위해 메커니즘은 [현재 구성 변환 기능과](../create-packages/source-and-config-file-transformations.md)유사 합니다.
변환 파일은 패키지의 콘텐츠 폴더에 추가 됩니다. 그러나 구성 변환에서 설치 및 제거에 대해 단일 파일을 사용 하는 동안 XDT 변환은 다음 파일을 사용 하 여 이러한 두 프로세스를 세부적으로 제어할 수 있도록 합니다.

- Web.config.install.xdt
- Web.config.uninstall.xdt

또한 NuGet은 파일 접미사를 사용 하 여 변환에 대해 실행할 엔진을 결정 하므로 기존 web.config 변환을 사용 하는 패키지는 계속 작동 합니다. XDT 변환은 web.config 뿐 아니라 모든 XML 파일에도 적용할 수 있으므로 프로젝트의 다른 응용 프로그램에도 사용할 수 있습니다.

#### <a name="what-you-can-do-with-xdt"></a>XDT로 수행할 수 있는 작업

XDT의 가장 큰 장점 중 하나는 XML DOM의 구조를 조작 하기 위한 [간단 하지만 강력한 구문](https://docs.microsoft.com/previous-versions/aspnet/dd465326(v=vs.110)) 입니다. XDT는 하나의 고정 된 문서 구조를 다른 구조에 간단 하 게 겹치게 하는 대신, 단순 특성 이름 일치에서 전체 XPath 지원과 같은 다양 한 방식으로 요소를 일치 시키기 위한 컨트롤을 제공 합니다. 일치 하는 요소 또는 요소 집합을 찾으면 XDT는 요소를 조작 하는 다양 한 함수 집합을 제공 합니다. 즉, 특성을 추가, 업데이트 또는 제거 하거나, 특정 위치에 새 요소를 배치 하거나, 전체를 바꾸거나 제거 합니다. 요소와 해당 자식 요소입니다.

### <a name="machine-wide-configuration"></a>시스템 수준 구성

NuGet의 가장 큰 장점 중 하나는 다른 방법으로는 큰 실행 파일 또는 라이브러리를 통합할 수 있는 모듈식 구성 요소 집합으로 분할 하 고, 대부분은 독립적으로 유지 관리 및 버전 관리 하는 것입니다. 그러나이 경우에는 제품 또는 제품군에 대 한 기존 아이디어가 잠재적으로 더 조각화 될 수 있습니다.
NuGet의 사용자 지정 패키지 원본 기능은 패키지를 구성 하는 한 가지 방법을 제공 합니다. 그러나 사용자 지정 패키지 원본은 자체에서 검색할 수 없습니다.

NuGet 2.6 은% ProgramData%/NuGet/Config. 경로에서 폴더 계층 구조를 검색 하 여 NuGet을 구성 하기 위한 논리를 확장 합니다. 제품 설치 관리자는이 폴더에 사용자 지정 NuGet 구성 파일을 추가 하 여 해당 제품에 대 한 사용자 지정 패키지 원본을 등록할 수 있습니다. 또한 폴더 구조는 제품, 버전 및 IDE의 SKU에 대 한 의미 체계를 지원 합니다. 이러한 디렉터리의 설정은 "last in wins" 선행 전략을 사용 하 여 다음과 같은 순서로 적용 됩니다.

1. %ProgramData%\NuGet\Config\*.config
2. %ProgramData%\NuGet\Config\{IDE}\*.config
3. %ProgramData%\NuGet\Config\{IDE}\{Version}\*.config
4. %ProgramData%\NuGet\Config\{IDE}\{Version}\{SKU}\*.config

이 목록에서 {IDE} 자리 표시자는 NuGet이 실행 되는 IDE와 관련 되어 있으므로 Visual Studio의 경우에는 "VisualStudio"이 됩니다. {Version} 및 {SKU} 자리 표시 자가 IDE에서 제공 됩니다 (예: "11.0", "WDExpress", "VWDExpress" 및 "Pro"). 이 폴더에는 다양 한 * .config 파일이 포함 될 수 있습니다.
따라서 ACME 구성 요소 회사는 제품 설치 관리자의 일부로 서 다음 파일 경로를 만들어 Visual Studio 2012 Professional 및 Ultimate 버전 에서만 볼 수 있는 사용자 지정 패키지 소스를 추가할 수 있습니다.

%ProgramData%\NuGet\Config\VisualStudio\11.0\Pro\acme.config

폴더 구조를 사용 하면 소프트웨어 설치 관리자 같은 프로그램에서 NuGet의 구성에 컴퓨터 수준 패키지 원본을 추가 하는 것이 가능 하지만, 패키지 원본 (예:% AppData%/NuGet/NuGet.Config에 등록 됨) 또는 컴퓨터 전체를 등록 하기 위해 NuGet 구성 대화 상자도 업데이트 되었습니다.

이 기능은 다음 위치에 파일이 설치 된 Visual Studio 2013에서 활용 됩니다.

%ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config

이 파일에는 ".NET Framework 패키지" 라는 새 패키지 원본이 구성 되어 있습니다.

![NuGet 구성 파일 컴퓨터 전체 설정](./media/NuGet-Config-File-Machine-Wide.png)

### <a name="contextualizing-search"></a>Contextualizing 검색

NuGet 갤러리에서 제공 하는 패키지 수가 지 수 속도로 계속 증가 함에 따라 검색 기능이 향상 되어 NuGet 우선 순위 목록의 맨 위에 남아 있습니다. NuGet에 대해 계획 된 기능 중 하나는 상황별 검색입니다. 즉, NuGet은 사용 중인 Visual Studio의 버전 및 SKU에 대 한 정보를 사용 하 고, 빌드 중인 프로젝트의 형식을 잠재적 검색의 관련성을 결정 하기 위한 조건으로 사용 합니다. 검색.

NuGet 2.6부터 패키지를 설치할 때마다 설치의 컨텍스트가 설치 작업 데이터의 일부로 기록 됩니다.  또한 검색은 동일한 컨텍스트 정보를 보내며,이를 통해 NuGet 갤러리에서 상황별 설치 추세에 따라 검색 결과를 높일 수 있습니다.  NuGet 갤러리에 대 한 향후 업데이트를 통해이 상황에 맞는 관련성을 향상 시킬 수 있습니다.

### <a name="tracking-direct-installs-vs-dependency-installs"></a>직접 설치 및 종속성 설치 추적

패키지 작성자는 NuGet 갤러리에 제공 된 [패키지 통계](http://blog.nuget.org/20130226/Introducing-Package-Statistics.html) 에 더 많은 의존 합니다.  작성자가 요청한 중요 한 데이터 요소 중 하나는 직접 패키지 설치와 종속성 설치 간의 차이점입니다.  지금까지 NuGet 클라이언트는 개발자가 패키지를 직접 설치 했는지 아니면 종속성을 충족 하기 위해 설치 되었는지에 대 한 설치 작업 관련 컨텍스트를 보내지 않았습니다.
NuGet 2.6 부터는 이제 설치 작업을 위해 해당 데이터가 전송 됩니다.  NuGet 갤러리의 패키지 통계는 해당 데이터를 "-종속성" 접미사가 포함 된 별도의 설치 작업으로 노출 합니다.

* 설치
* 설치-종속성
* 업데이트
* 업데이트-종속성
* 다시 설치
* 다시 설치-종속성

다른 작업 이름 외에도 설치를 위해 종속 패키지 id가 기록 됩니다.  NuGet 갤러리에 대 한 향후 업데이트는 패키지 작성자가 개발자가 패키지를 설치 하는 방식을 완전히 이해할 수 있도록 보고서 내에 해당 데이터를 노출 합니다.

## <a name="bug-fixes"></a>버그 수정

NuGet 2.6에도 여러 버그 수정이 포함 되어 있습니다. NuGet 2.6에서 수정 된 작업 항목의 전체 목록은 [이 릴리스에 대 한 Nuget 문제 추적기](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.6&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)를 확인 하세요.