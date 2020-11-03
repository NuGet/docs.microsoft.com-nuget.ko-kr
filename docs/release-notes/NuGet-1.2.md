---
title: NuGet 1.2 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 Ecrs를 비롯 한 NuGet 1.2에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5d10d6bf27614980a144c30c3af6f9892a109061
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237190"
---
# <a name="nuget-12-release-notes"></a>NuGet 1.2 릴리스 정보

[NuGet 1.0 및 1.1 릴리스 정보](../release-notes/nuget-1.1.md)  |  [NuGet 1.3 릴리스 정보](../release-notes/nuget-1.3.md)

NuGet 1.2은 2011 년 3 월 30 일에 출시 되었습니다.

## <a name="new-features"></a>새로운 기능

### <a name="framework-profile-support"></a>프레임 워크 프로필 지원

처음부터 NuGet은 다른 프레임 워크를 대상으로 하는 라이브러리를 지원 합니다. 그러나 이제 패키지에는 Windows Phone 프로필과 같은 특정 프로필을 대상으로 하는 어셈블리가 포함 될 수 있습니다. 프레임 워크의 특정 프로필을 대상으로 지정 하려면 대시를 추가 하 고 프로필 약어를 추가 합니다. 예를 들어 Windows Phone (즉, Windows Phone 7)에서 실행 되는 SilverLight를 대상으로 하는 경우 다음 스크린샷에 표시 된 것 처럼 sl3-wp 폴더에 어셈블리를 넣을 수 있습니다.

![프레임 워크 프로필 폴더 레이아웃](./media/framework-profile-support.png)

"Wp7"를 모니커로 사용 하도록 선택 하지 않은 이유를 질문할 수 있습니다. 부분적으로 Windows Phone 7은 나중에 최신 버전의 Silverlight를 실행 하는 것이 좋습니다 .이 경우에는 사용자가 대상으로 지정 하는 프레임 워크 프로필에 대 한 정보를 제공 해야 할 수 있습니다.

### <a name="automatically-add-binding-redirects"></a>자동으로 바인딩 리디렉션 추가

강력한 이름의 어셈블리를 사용 하 여 패키지를 설치 하는 경우 NuGet은 프로젝트를 컴파일하여 자동으로 추가 하기 위해 프로젝트에서 구성 파일에 바인딩 리디렉션을 추가 해야 하는 경우를 검색할 수 있습니다. David Ebbo의 블로그 게시물 시리즈의 블로그 게시물 시리즈에 대 한 자세한[내용은이](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)기능의 용도를 설명 하는 NuGet 버전 관리의 블로그 게시물 시리즈를 참조 하세요.

<a name="framework-assembly-refs"></a>

### <a name="specifying-framework-assembly-references-gac"></a>프레임 워크 어셈블리 참조 지정 (GAC)

경우에 따라 패키지는 .NET Framework에 있는 어셈블리에 따라 달라질 수 있습니다. 항상 패키지의 소비자가 프레임 워크 어셈블리를 참조 해야 하는 것은 아닙니다. 그러나 일부 경우에는 개발자가 패키지를 사용 하기 위해 해당 어셈블리의 형식에 대해 코딩 해야 하는 경우와 같은 중요 합니다. `frameworkAssemblies`메타 데이터 요소의 자식 요소인 새 요소를 사용 하면 `frameworkAssembly` GAC의 프레임 워크 어셈블리를 가리키는 요소 집합을 지정할 수 있습니다. 프레임 워크 어셈블리에 대 한 강조를 확인 합니다.
이러한 어셈블리는 .NET Framework의 일부로 모든 컴퓨터에 있는 것으로 간주 되므로 패키지에 포함 되지 않습니다. 다음 표에서는 요소의 특성을 보여 줍니다 `frameworkAssembly` .


|attribute |설명|
|----------------|-----------|
|**assemblyName**|*필수*. 과 같은 어셈블리의 이름입니다 `System.Net` .|
|**targetFramework**|*선택 사항입니다*. 이 프레임 워크 어셈블리가 적용 되는 프레임 워크 및 프로필 이름 (또는 별칭) (예: "net40" 또는 "sl4")을 지정할 수 있습니다. 에서는 [여러 대상 프레임 워크 지원](../create-packages/supporting-multiple-target-frameworks.md)에 설명 된 것과 동일한 형식을 사용 합니다.|

```xml
  <frameworkAssemblies>
    <frameworkAssembly assemblyName="System.ComponentModel.DataAnnotations" targetFramework="net40" />
    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
  </frameworkAssemblies>
```

### <a name="nugetexe-now-is-able-to-store-api-key-credentials"></a>nuget.exe 이제 API 키 자격 증명을 저장할 수 있습니다.

nuget.exe 명령줄 도구를 사용 하는 경우 이제 SetApiKey 명령을 사용 하 여 API 키를 저장할 수 있습니다. 이렇게 하면 패키지를 푸시할 때마다 지정할 필요가 없습니다. nuget.exe를 사용 하 여 API 키를 저장 하는 방법에 대 한 자세한 내용은 [패키지 게시에 대 한 설명서를 참조](../nuget-org/publish-a-package.md)하세요.

### <a name="package-explorer"></a>패키지 탐색기
NuGet 1.2을 지원 하도록 패키지 탐색기를 업데이트 했습니다. 자세한 내용은 [패키지 탐색기 릴리스 정보](http://nuget.codeplex.com/wikipage?title=New%20features%20in%20NuGet%20Package%20Explorer%201.0)를 참조 하세요.

## <a name="other-featuresfixes"></a>기타 기능/수정 사항

이전 목록은 구현한 많은 기능과 수정 된 버그 중 가장 두드러지게 나타납니다. 모두이 릴리스에서는 [59 작업 항목](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.2&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0) 을 구현/수정 했습니다.

## <a name="known-issues"></a>알려진 문제

* **1.2 패키지 비호환** : 최신 버전의 명령줄 도구를 사용 하 여 빌드된 패키지 (nuget.exe (> 1.2)는 이전 버전의 NuGet VS 추가 기능 (예: 1.1)에서 작동 하지 않습니다. 호환 되지 않는 스키마에 대 한 정보를 나타내는 오류 메시지가 표시 되 면이 오류가 발생 합니다. NuGet을 최신 버전으로 업데이트 하세요.
* **Nuget. 서버 비호환** : Nuget. server 프로젝트를 사용 하 여 내부 nuget 피드를 호스팅하는 경우 최신 버전의 Nuget. server로 해당 프로젝트를 업데이트 해야 합니다.
* **서명 불일치 오류** : 서명 불일치에 대 한 메시지를 사용 하 여 업그레이드 하는 동안 오류가 발생 하는 경우 먼저 NuGet을 제거한 후 설치 해야 합니다. 자세한 내용은 [알려진 문제 페이지](../release-notes/known-issues.md) 에 나열 되어 있습니다. 이 문제는 Visual Studio 2010 s p 1을 실행 하는 경우에만 적용 되 고 잘못 서명 된 NuGet 1.0 버전이 설치 되어 있습니다. 이 버전은 CodePlex 웹 사이트에서 잠깐 동안만 사용할 수 있으므로이 문제는 너무 많은 사용자에 게 영향을 주지 않습니다.