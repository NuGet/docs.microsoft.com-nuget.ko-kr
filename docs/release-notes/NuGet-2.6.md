---
title: NuGet 2.6 릴리스 정보
description: 2.6.1의 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr 포함 하 여 WebMatrix 용 NuGet에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f011a8db7ac2067a2ed7db67849d63f7dd40d1ce
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551945"
---
# <a name="nuget-26-release-notes"></a>NuGet 2.6 릴리스 정보

[NuGet 2.5 릴리스 정보](../release-notes/nuget-2.5.md) | [NuGet 2.6.1 WebMatrix 릴리스 정보](../release-notes/nuget-2.6.1-for-webmatrix.md)

NuGet 2.6은 2013 년 6 월 26 일에 출시 되었습니다.

## <a name="notable-features-in-the-release"></a>릴리스에서 주목할 만한 기능

### <a name="support-for-visual-studio-2013"></a>Visual Studio 2013에 대 한 지원

NuGet 2.6은 Visual Studio 2013에 대 한 지원을 제공 하는 첫 번째 릴리스입니다. 및 Visual Studio 2012와 같은 NuGet 패키지 관리자 확장을 Visual Studio의 모든 버전에 포함 합니다.

여전히 Visual Studio 2010 및 Visual Studio 2012를 지원 하 고 확장 크기를 가능한 한 작게 유지 하는 동안 Visual Studio 2013에 대 한 최상의 지원을 제공 하기 위해 것을 생성 하는 동안 Visual Studio 2013에 대 한 별도 확장이 합니다 Visual Studio 2010 및 2012를 대상으로 계속 원래 확장 합니다.

NuGet 2.6 이상에서는 아래와 같이 두 가지 확장 게시 됩니다.

1. [NuGet 패키지 관리자](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManager) (Visual Studio 2010 및 2012에 적용)
1. [Visual Studio 2013 용 NuGet 패키지 관리자](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2013)

이 분할을 사용 하 여는 [nuget.org](https://nuget.org) 홈 페이지의 "Install NuGet" 단추를 사용 하면 합니다 [NuGet 설치](../install-nuget-client-tools.md) 페이지에서 다른 NuGet 클라이언트를 설치 하는 방법에 대 한 자세한 정보를 찾을 수 있습니다.

<a name="xdt"></a>

### <a name="xdt-webconfig-transformation-support"></a>XDT Web.config 변환 지원

NuGet 클라이언트에 대 한 가장 높은 요청 된 기능 중 하나는 Visual Studio 빌드 구성 변환에 사용 되는 XDT 변환 엔진을 사용 하 여 더 강력한 XML 변환을 지원 하도록 했습니다.

2013 년 4 월 XDT에 대 한 NuGet 지원에 대 한 두 개의 큰 발표를 했습니다. XDT 라이브러리 자체 자체 되는 첫 번째 되었습니다 [NuGet 패키지로 릴리스](https://nuget.org/packages/Microsoft.Web.Xdt) 하 고 [CodePlex의 오픈 소스](http://xdt.codeplex.com/)합니다. 이 단계에서 NuGet 클라이언트를 포함 하 여 다른 오픈 소스 소프트웨어를 자유롭게 사용할 XDT 엔진을 사용할 수 있습니다. 두 번째 NuGet 클라이언트에서의 변형 XDT 엔진의 사용을 지원 하려면 계획 이었습니다. NuGet 2.6이이 통합을 포함합니다.

#### <a name="how-it-works"></a>작동 방법

NuGet의 XDT 지원을 활용 하려면 메커니즘의와 비슷하게 표시 합니다 [현재 구성 변환 기능](../create-packages/source-and-config-file-transformations.md)합니다.
변환 파일은 패키지의 콘텐츠 폴더에 추가 됩니다. 그러나 설치 및 제거에 모두에 대 한 단일 파일을 사용 하는 구성 변환, XDT 변환 두 다음 파일을 사용 하 여이 프로세스를 세부적으로 제어를 사용:

- Web.config.install.xdt
- Web.config.uninstall.xdt

또한 NuGet 패키지 기존 web.config.transforms를 사용 하 여 계속 작동 하므로 변환에 대 한 실행 하는 엔진을 확인 하려면 파일 접미사를 사용 합니다. XDT 변환 XML 파일 (뿐 아니라 web.config)을 적용할 수도 있습니다를 활용할 수 있도록이 다른 응용 프로그램에 대 한 프로젝트에서.

#### <a name="what-you-can-do-with-xdt"></a>XDT를 사용 하 여 수행할 수 있는 작업

XDT의 가장 큰 장점 중 하나는 해당 [간단 하지만 강력한 구문](http://msdn.microsoft.com/library/dd465326.aspx) 구조는 XML dom을 조작 하기 위한 단순히 다른 구조체에 하나의 고정된 문서 구조를 오버레이, 대신 XDT는 요소에서 다양 한 방법으로 전체 XPath 지원에 간단한 특성 이름 일치에서 일치 하는 컨트롤을 제공 합니다. 즉, 추가, 업데이트 또는 특성을 제거, 특정 위치에 새 요소를 배치 하거나 대체 또는 전체를 제거 하는지 여부를 XDT의 요소를 조작 하기 위한 다양 한 함수 집합이 제공 일치 하는 요소 또는 요소 집합을 발견 되 면 요소와 해당 자식 요소입니다.

### <a name="machine-wide-configuration"></a>시스템 수준의 구성

NuGet의 훌륭한 장점 중 하나는 그렇지 않은 경우 큰 실행 파일 또는 라이브러리를 하지 않을 수 있는 통합 된 가장 중요 한 유지 관리 및 버전 독립적으로 모듈식 구성 요소 집합을 다운에 중단 하는 것입니다. 한 가지 부작용이 것 인데, 제품 또는 제품군의 기본 개념 보다 조각화 잠재적으로 됩니다.
NuGet의 사용자 지정 패키지 원본 기능 제공 패키지를 구성 하는 한 가지 방법은 그러나 사용자 지정 패키지 원본을 자체적으로 검색할 수 없는 합니다.

NuGet 2.6 ProgramData%/NuGet/Config % 경로 아래의 폴더 계층 구조를 검색 하 여 NuGet 구성에 대 한 논리를 확장 합니다. 제품 설치 관리자 제품에 대 한 사용자 지정 패키지 원본을 등록 하려면이 폴더 아래에 있는 사용자 지정 NuGet 구성 파일을 추가할 수 있습니다. 또한 폴더 구조는 제품, 버전 및 ide도 SKU에 대 한 의미 체계를 지원합니다. 이러한 디렉터리에서 설정은 "wins"에서 마지막으로 우선 전략을 사용 하 여 다음과 같은 순서로 적용 됩니다.

1. %ProgramData%\NuGet\Config\*.config
2. %ProgramData%\NuGet\Config\{IDE}\*.config
3. %ProgramData%\NuGet\Config\{IDE}\{Version}\*.config
4. %ProgramData%\NuGet\Config\{IDE}\{Version}\{SKU}\*.config

이 목록에 {IDE} 자리 표시자 이므로 NuGet 실행 되는 IDE에 특정 Visual Studio의 경우 "visual Studio" 됩니다. {Version} 및 {SKU} 자리 표시자에서 제공 하는 IDE (예: "11.0" 및 "WDExpress", "VWDExpress" 및 "전문가" 각각). 다음 폴더에는 많은 다른 *.config 파일 포함 될 수 있습니다.
따라서 ACME 구성 요소 회사, 해당 제품 설치 관리자의 일부로 소스를 추가할 수 사용자 지정 패키지 파일 경로 만들어 Visual Studio 2012 Professional 및 Ultimate 버전에만 표시 됩니다.

%ProgramData%\NuGet\Config\VisualStudio\11.0\Pro\acme.config

패키지 원본으로 등록에 사용할 수 있도록 NuGet 구성 대화 상자 폴더 구조를 사용 하면 NuGet의 구성은 컴퓨터 전체 패키지 소스를 추가할 소프트웨어 설치 관리자와 같은 프로그램에 대 한 간단한에 업데이트 (예: %AppData%/NuGet/NuGet.Config 등록 됨) 하거나 사용자 고유의 또는 컴퓨터에 적용 합니다.

이 기능 파일에 설치 되어 있는 Visual Studio 2013을 활용 합니다.

%ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config

이 파일 내에서 ".NET Framework 패키지" 라고 하는 새 패키지 원본 구성 됩니다.

![NuGet Config 파일 컴퓨터 너비 설정](./media/NuGet-Config-File-Machine-Wide.png)

### <a name="contextualizing-search"></a>검색 맥락 화

NuGet 갤러리에서 제공 하는 패키지 수가 계속는 기하급수적으로 증가, NuGet 우선 순위 목록의 맨 위에 있는 적이 남아 검색 개선 합니다. 상황별 검색, NuGet은 정보를 사용 버전 및 SKU의 Visual Studio 사용 중인 현재 작성 중인 프로젝트의 형식에 대 한 조건으로 잠재적인 검색 관련성을 결정 하는 것에 대 한 의미는 NuGet에 대 한 계획 된 기능 중 하나 결과입니다.

NuGet 2.6부터 패키지를 설치할 때마다 설치에 대 한 컨텍스트는 기록 설치 작업 데이터의 일부로.  검색 상황에 맞는 설치 추세에서 검색 결과 향상 시키는 NuGet 갤러리를 사용 하면 동일한 컨텍스트 정보를 보낼 수도 있습니다.  NuGet 갤러리의 이후 업데이트는이 상황에 맞는 관련성 향상을 사용 하도록 설정 합니다.

### <a name="tracking-direct-installs-vs-dependency-installs"></a>추적 vs 직접 설치 합니다. 종속성 설치

패키지 작성자에 더 의존 합니다 [패키지 통계](http://blog.nuget.org/20130226/Introducing-Package-Statistics.html) NuGet 갤러리에서 제공 합니다.  중요 한 누락 된 데이터 요소 작성자가 묻는 하나는 직접 패키지 설치 및 종속성 설치 간의 차이점입니다.  지금 까지는 NuGet 클라이언트는 개발자는 패키지를 직접 설치 여부 또는 종속성을 충족 하기 위해 설치 된 경우에 대 한 설치 작업 중심으로 컨텍스트를 보내지 않았습니다.
설치 작업에 대 한 데이터 이제 전송 되지 않는다는 NuGet 2.6을 사용 하 여 시작 합니다.  NuGet 갤러리에 대 한 패키지 통계를 사용 하 여 별도 설치 작업으로 해당 데이터에 노출 됩니다는 "-종속성" 접미사.

* 설치
* 종속성 설치
* 업데이트
* 업데이트 종속성
* 다시 설치
* 종속성을 다시 설치

다른 작업 이름 외에도 종속 패키지 id는 설치에 대 한 기록 됩니다.  NuGet 갤러리의 이후 업데이트는 패키지 작성자가 개발자는 해당 패키지를 설치 하는 방법을 완전히 이해 하는 보고서 내에서 해당 데이터를 노출 합니다.

## <a name="bug-fixes"></a>버그 수정

NuGet 2.6에는 여러 버그 수정도 포함 됩니다. 작업의 전체 목록은 항목 고정 NuGet 2.6에서 하세요 보기는 [이 릴리스의 NuGet 문제 추적기](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.6&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)합니다.