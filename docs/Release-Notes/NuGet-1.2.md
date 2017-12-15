---
title: "NuGet 1.2 릴리스 정보 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 48f23141-b2ad-4cdf-8d81-7bb6b9419aa6
description: "알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr를 포함 하 여 NuGet 1.2에 대 한 릴리스 정보입니다."
keywords: "NuGet 1.2 릴리스 정보, 버그 수정, 알려진 문제, 추가 기능을 Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: d69a65352d42025b61df9068473ddedffc5f1663
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-12-release-notes"></a>NuGet 1.2 릴리스 정보

[NuGet 1.0 및 1.1 릴리스 정보](../release-notes/nuget-1.1.md) | [NuGet 1.3 릴리스 정보](../release-notes/nuget-1.3.md)

NuGet 1.2 2011 년 3 월 30 일에 출시 되었습니다.

## <a name="new-features"></a>새 기능

### <a name="framework-profile-support"></a>프레임 워크 프로필 지원

처음부터 NuGet 지원 해 다른 프레임 워크를 대상 하는 라이브러리입니다. 하지만 이제 패키지는 Windows Phone 프로필 같은 특정 프로필을 대상으로 하는 어셈블리를 포함 될 수 있습니다. 특정 프레임 워크의 프로필을 대상으로 대시 프로필 약어에는 다음을 추가 합니다. 예를 들어 Windows Phone (즉, Windows Phone 7)에서 실행 되는 SilverLight를 대상으로 다음 스크린샷에 표시 된 대로 sl3 wp 폴더에 어셈블리를 넣을 수 있습니다.

![프레임 워크 프로필 폴더 레이아웃](./media/framework-profile-support.png)

"Wp7" 모니커도 사용 하도록 방금 선택 하지 않은 이유를 요청할 수 있습니다. 부분적으로 Windows Phone 7은 최신 버전의 Silverlight 나중에 실행 될 수 있습니다, 대상으로 하는 경우에 프레임 워크 프로필에 대 한 더 정확 하 게 할 수를 예측 하는 것입니다.

### <a name="automatically-add-binding-redirects"></a>바인딩 리디렉션을 자동으로 추가

강력한 이름의 어셈블리와 패키지를 설치할 때 NuGet에 프로젝트에 필요한 바인딩 리디렉션을 컴파일하고 자동으로 추가 하려면 프로젝트에 대 한 순서 대로 구성 파일에 추가 될 경우를 이제 감지할 수 있습니다. NuGet 버전 관리 권한을 부여 받은 David Ebbo 블로그 게시물 시리즈의 일부 3 "[리디렉션합니다 바인딩을 통해 통합](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)"에서 자세한 내용을 보려면이 기능의 용도 설명 합니다.

<a name="framework-assembly-refs"></a>

### <a name="specifying-framework-assembly-references-gac"></a>프레임 워크 어셈블리 참조 (GAC)를 지정합니다.

경우에 따라 패키지는.NET Framework에 있는 어셈블리에 따라 달라질 수 있습니다. 엄격히 말해서, 항상 필요 없는 패키지의 소비자의 프레임 워크 어셈블리를 참조 합니다. 하지만 일부 경우에는 개발자가 패키지를 사용 하려면 해당 어셈블리의 형식에 대해 코딩 해야 하는 경우 같은 중요 한 쉽습니다. 새 `frameworkAssemblies` 요소, 메타 데이터 요소의 자식 요소 집합을 지정할 수 있습니다 `frameworkAssembly` GAC에 프레임 워크 어셈블리를 가리키는 요소입니다. 프레임 워크 어셈블리에 중점을 두를 note 합니다.
이러한 어셈블리.NET Framework의 일부로 모든 컴퓨터에 있는 것으로 간주 됩니다 대로 패키지에 포함 되지 않습니다. 다음 표에서 특성을 나열는 `frameworkAssembly` 요소입니다.


|특성 |설명|
|----------------|-----------|
|**assemblyName**|*필요한*합니다. 와 같은 어셈블리의 이름 `System.Net`합니다.|
|**targetFramework**|*선택적*합니다. 프레임 워크 및 프로필 이름 (또는 별칭)을 지정할 수 있도록 "net40" 또는 "sl4" 등이 프레임 워크 어셈블리에 적용 되는 합니다. 에 설명 된 동일한 형식을 사용 하 여 [여러 대상 프레임 워크를 지 원하는](../create-packages/supporting-multiple-target-frameworks.md)합니다.|

```xml
  <frameworkAssemblies>
    <frameworkAssembly assemblyName="System.ComponentModel.DataAnnotations" targetFramework="net40" />
    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
  </frameworkAssemblies>
```

### <a name="nugetexe-now-is-able-to-store-api-key-credentials"></a>nuget.exe 이제 API 키 자격 증명을 저장할 수는

Nuget.exe 명령줄 도구를 사용할 때는 API 키를 저장할 SetApiKey 명령 이제 사용할 수 있습니다. 이런 방식으로 패키지를 누를 때마다 지정할 필요가 없습니다. Nuget.exe를 사용 하 여 API 키를 저장 하는 대 한 자세한 내용은 [는 패키지를 게시 하는 데에 대 한 설명서를 읽을](../create-packages/publish-a-package.md)합니다.

### <a name="package-explorer"></a>패키지 탐색기
패키지 탐색기 NuGet 1.2를 지원 하도록 업데이트 되었습니다. 자세한 내용은 참조는 [패키지 탐색기 릴리스 정보](http://nuget.codeplex.com/wikipage?title=New%20features%20in%20NuGet%20Package%20Explorer%201.0)합니다.

## <a name="other-featuresfixes"></a>다른 기능/수정

이전 목록에서 가장 눈에 띄는 많은 기능을 구현 했습니다 및 버그를 해결 했습니다. 무엇 보다도 구현/해결 [59 작업 항목](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.2&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0) 이 릴리스에서 합니다.

## <a name="known-issues"></a>알려진 문제

* **1.2 패키지의 비 호환성**: 최신 버전의 명령줄 도구를 사용 하 여 패키지 작성, nuget.exe (> 1.2) 이전 버전의 NuGet VS에서 추가 기능 (예: 1.1)와 작동 하지 것입니다. 호환 되지 않는 스키마에 대 한 정보를 나타내는 오류 메시지를 실행 하면이 오류를 실행 합니다. NuGet을 최신 버전으로 업데이트 하세요.
* **NuGet.Server 비 호환성**:는 내부 NuGet NuGet.Server 프로젝트를 사용 하 여 피드를 호스팅하는 경우 NuGet.Server의 최신 버전으로 해당 프로젝트를 업데이트 해야 합니다.
* **서명 불일치 오류**: 서명 불일치 하는 방법에 대 한 메시지와 함께 업그레이드 하는 동안 오류가 발생 하면, 해야 NuGet를 먼저 제거한 다음 설치 합니다. 이 테이블은 표시에 우리의 [알려진 문제 페이지](../release-notes/Known-Issues.md) 추가 정보가 제공 됩니다. 문제만 Visual Studio 2010 s p 1을 실행 하는 것 미치며 잘못 서명 설치 된 NuGet 1.0이 설치 되어 있습니다. 이 버전만으로 제공 된 CodePlex 웹 사이트에서 짧은 기간 동안이 문제에 너무 많은 사람들이 영향을 하지 않아야 합니다.