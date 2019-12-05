---
title: NuGet 2.5 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 Ecrs를 비롯 한 NuGet 2.5에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 940582d5173f5a53dcd04cf1258fc02a2439af4e
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825289"
---
# <a name="nuget-25-release-notes"></a>NuGet 2.5 릴리스 정보

Nuget [2.2.1 릴리스 정보](../release-notes/nuget-2.2.1.md) | [Nuget 2.6 릴리스 정보](../release-notes/nuget-2.6.md)

NuGet 2.5은 2013 년 4 월 25 일에 출시 되었습니다. 이 릴리스는 너무 하도록 강요 되 버전 2.3 및 2.4를 건너 뛰 세요. 최신 버전은 NuGet에 대해 보유 한 가장 큰 릴리스입니다. 릴리스의 [작업 항목 수가 160](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) 이상입니다.

## <a name="acknowledgements"></a>승인

NuGet 2.5에 대 한 중요 한 기여에 대해 다음과 같은 외부 참가자에 게 감사 하려고 합니다.

1. [Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))
    - [#2847](https://nuget.codeplex.com/workitem/2847) -알려진 대상 프레임 워크 식별자 목록에 MonoAndroid, Monotouch.dialog 및 MonoMac를 추가 합니다.
2. [Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))
    - [#2865](https://nuget.codeplex.com/workitem/2865) -대/소문자를 구분 하는 OS에 대 한 `NuGet.targets`의 맞춤법 수정
3. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - Mono에서 솔루션 빌드를 만듭니다.
4. [Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))
    - Mono에서 실패 한 단위 테스트를 수정 합니다.
5. [Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))
    - [#2920](https://nuget.codeplex.com/workitem/2920) -nuget.exe Pack 명령은 속성을 MSBuild에 전파 하지 않습니다.
6. [Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))
    - 서식 지정을 유지 하기 위해 [#1511](https://nuget.codeplex.com/workitem/1511) 수정 된 XML 처리 코드입니다.
7. [Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - 사용자 지정 사전에 인식할 수 있는 단어를 추가 하 여 빌드 .cmd가 성공 하도록 합니다.
8. [Bruno Roggeri](https://www.codeplex.com/site/users/view/broggeri)
    - 지역화 된 VS에서 실행 될 때 단위 테스트 수정
9. [Gareth Evans](https://www.codeplex.com/site/users/view/garethevans)
    - PackageService에서 추출 된 인터페이스
10. [Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))
     - 압축 시 프로젝트 종속성 [#936](https://nuget.codeplex.com/workitem/936) 처리
11. [Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))
     - [#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) -nuget에 패키지 원본 자격 증명을 저장할 때 일반 텍스트 암호를 지원 합니다. cofig 파일
12. [James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))
     - [#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) -패키지 다운로드 도움말 설명

또한 최종 릴리스 전에 승인 되 고 수정 된 NuGet 2.5 베타/RC를 사용 하 여 버그를 찾기 위해 다음 개인이 감사 합니다.

1. [Tony 벽](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))
    - 최신 NuGet 2.4 및 2.5 빌드를 사용 하 여 [#3200](https://nuget.codeplex.com/workitem/3200) -MSTest 손상

## <a name="notable-features-in-the-release"></a>릴리스의 주요 기능

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a>사용자가 이미 존재 하는 콘텐츠 파일을 덮어쓸 수 있도록 허용

모든 시간에서 가장 많이 요청 되는 기능 중 하나는 NuGet 패키지에 포함 될 때 이미 디스크에 있는 콘텐츠 파일을 덮어쓰는 기능입니다. NuGet 2.5부터 이러한 충돌을 식별 하 고 파일을 덮어쓸지 묻는 메시지가 표시 되는 반면 이전에는 이러한 파일을 항상 건너뛰었습니다.

![콘텐츠 파일 덮어쓰기](./media/NuGet-2.5/overwrite-file.png)

' nuget.exe 업데이트 ' 및 ' 설치-패키지 '에는 이제 명령줄 시나리오에 대 한 기본값을 설정할 수 있는 새 옵션인 '-FileConflictAction '가 있습니다.

패키지의 파일이 대상 프로젝트에 이미 있는 경우 기본 동작을 설정 합니다. 항상 파일을 덮어쓰려면 ' 덮어쓰기 '로 설정 합니다. 파일을 건너뛰려면 ' 무시 '로 설정 합니다. 지정 하지 않으면 충돌 하는 각 파일에 대 한 메시지가 표시 됩니다.

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a>MSBuild 대상 및 props 파일 자동 가져오기

NuGet 패키지의 최상위 수준에서 새 기본 폴더를 만들었습니다.  `\lib`, `\content`및 `\tools`에 대 한 피어로 이제 패키지에 `\build` 폴더를 포함할 수 있습니다.  이 폴더 아래에 고정 이름을 사용 하 여 `{packageid}.targets` 또는 `{packageid}.props`두 파일을 저장할 수 있습니다. 이러한 두 파일은 다른 폴더와 마찬가지로 `build` 바로 아래에 있거나 프레임 워크 별 폴더에 있을 수 있습니다. 가장 일치 하는 프레임 워크 폴더를 선택 하는 규칙은 정확히 일치 합니다.

NuGet은 \build 파일이 포함 된 패키지를 설치 하는 경우 프로젝트 파일에서 `.targets` 및 `.props` 파일을 가리키는 MSBuild `<Import>` 요소를 추가 합니다. `.props` 파일은 맨 위에 추가 되는 반면 `.targets` 파일은 맨 아래에 추가 됩니다.

### <a name="specify-different-references-per-platform-using-references-element"></a>`<References/>` 요소를 사용 하 여 플랫폼별로 다른 참조 지정

2\.5 이전에 `.nuspec` 파일에서는 사용자가 모든 프레임 워크에 대해 추가할 참조 파일만 지정할 수 있습니다. 이제 2.5의이 새로운 기능을 사용 하 여 지원 되는 각 플랫폼에 대 한 `<reference/>` 요소를 작성할 수 있습니다. 예를 들면 다음과 같습니다.

```xml
<references>
    <group targetFramework="net45">
        <reference file="a.dll" />
    </group>
    <group targetFramework="netcore45">
        <reference file="b.dll" />
    </group>
    <group>
        <reference file="c.dll" />
    </group>
</references>
```

NuGet이 `.nuspec` 파일을 기반으로 하는 프로젝트에 참조를 추가 하는 흐름은 다음과 같습니다.

1. 대상 프레임 워크에 적합 한 `lib` 폴더를 찾고 해당 폴더에서 어셈블리 목록을 가져옵니다.
1. 대상 프레임 워크에 적합 한 참조 그룹을 별도로 찾고 해당 그룹에서 어셈블리 목록을 가져옵니다. 지정 된 대상 프레임 워크가 없는 참조 그룹은 대체 그룹입니다.
1. 두 목록의 교집합을 찾아 추가할 참조로 사용 합니다.

이 새로운 기능을 사용 하면 패키지 작성자가 여러 `lib` 폴더에 중복 어셈블리를 전달 해야 하는 경우 참조 기능을 사용 하 여 어셈블리의 하위 집합을 다른 프레임 워크에 적용할 수 있습니다.

참고: 현재 nuget.exe pack을 사용 하 여이 기능을 사용 해야 합니다. NuGet 패키지 탐색기는 아직 지원 하지 않습니다.

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a>모든 패키지를 한 번에 업데이트할 수 있도록 모든 단추를 업데이트 합니다.

모든 패키지를 업데이트 하는 "업데이트 패키지" PowerShell cmdlet에 대해 알고 있어야 합니다. 이제 UI를 통해이 작업을 수행 하는 쉬운 방법이 있습니다.

이 기능을 사용해 보려면 다음을 수행 하십시오.

1. 새 ASP.NET MVC 애플리케이션 만들기
1. ' NuGet 패키지 관리 ' 대화 상자를 시작 합니다.
1. ' 업데이트 '를 선택 합니다.
1. ' 모두 업데이트 ' 단추를 클릭 합니다.

![대화 상자의 모두 업데이트 단추](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a>Nuget.exe Pack에 대 한 향상 된 프로젝트 참조 지원

이제 nuget.exe pack 명령은 다음 규칙을 사용 하 여 참조 된 프로젝트를 처리 합니다.

1. 참조 된 프로젝트에 해당 하는 `.nuspec` 파일이 있는 경우 (예: `proj1.csproj`와 동일한 폴더에 `proj1.nuspec` 라는 파일이 있는 경우)이 프로젝트는 `.nuspec` 파일에서 읽은 id와 버전을 사용 하 여 패키지에 대 한 종속성으로 추가 됩니다.
1. 그렇지 않으면 참조 된 프로젝트의 파일이 패키지에 번들로 제공 됩니다. 그런 다음이 프로젝트에서 참조 하는 프로젝트가 재귀적으로 sames 규칙을 사용 하 여 처리 됩니다.
1. 모든 DLL, `.pdb`및 `.exe` 파일이 추가 됩니다.
1. 다른 모든 콘텐츠 파일이 추가 됩니다.
1. 모든 종속성이 병합 됩니다.

이를 통해 `.nuspec` 파일이 있는 경우 참조 된 프로젝트를 종속성으로 처리할 수 있습니다. 그렇지 않으면 패키지의 일부가 됩니다.

자세한 내용은 다음을 참조 하세요. [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)

### <a name="add-a-minimum-nuget-version-property-to-packages"></a>패키지에 ' 최소 NuGet 버전 ' 속성 추가

이제 ' minClientVersion ' 라는 새 메타 데이터 특성은 패키지를 사용 하는 데 필요한 최소 NuGet 클라이언트 버전을 나타낼 수 있습니다.

이 기능을 사용 하면 패키지 작성자가 특정 버전의 NuGet 이후에만 패키지를 사용할 수 있도록 지정할 수 있습니다. 새 `.nuspec` 기능이 NuGet 2.5 후에 추가 되 면 패키지는 최소 NuGet 버전을 요청할 수 있습니다.

```xml
<metadata minClientVersion="2.6">
```

사용자에 게 NuGet 2.5이 설치 되어 있고 패키지가 2.6을 요구 하는 것으로 식별 되 면 패키지를 설치할 수 없다는 시각적 표시가 사용자에 게 제공 됩니다. 그런 다음 사용자는 NuGet 버전을 업데이트 하도록 안내 됩니다.

이렇게 하면 패키지를 설치 하기 시작 하지만 인식할 수 없는 스키마 버전이 식별 되었음을 나타내는 오류가 발생 하는 기존 환경을 개선 하 게 됩니다.

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a>패키지를 설치 하는 동안 종속성이 더 이상 불필요 하 게 업데이트 되지 않습니다.

NuGet 2.5 이전에 프로젝트에 이미 설치 된 패키지에 종속 된 패키지를 설치 하는 경우 기존 버전에서 종속성이 충족 되더라도 종속성이 새 설치의 일부로 업데이트 됩니다.

NuGet 2.5부터 종속성 버전이 이미 충족 된 경우 다른 패키지를 설치 하는 동안 종속성이 업데이트 되지 않습니다.

**시나리오는 다음과 같습니다.**

1. 원본 리포지토리에는 버전 1.0.0 및 1.0.2가 포함 된 B 패키지가 포함 되어 있습니다. B에 대 한 종속성이 있는 패키지 A도 포함 합니다 (> = 1.0.0).
1. 현재 프로젝트에 이미 package B 버전 1.0.0이 설치 되어 있다고 가정 합니다. 이제 패키지 A를 설치 하려고 합니다.

**NuGet 2.2 이전 버전:**

* Package A를 설치 하면 기존 버전 1.0.0이 이미 > = 1.0.0 인 종속성 버전 제약 조건을 충족 하더라도 NuGet은 B를 1.0.2로 자동 업데이트 합니다.

**NuGet 2.5 이상:**

* NuGet은 기존 버전 1.0.0이 종속성 버전 제약 조건을 충족 하는 것을 감지 하므로 더 이상 B를 업데이트 하지 않습니다.

이러한 변경에 대 한 자세한 배경 정보는 관련 [토론 스레드](http://nuget.codeplex.com/discussions/436712)뿐만 아니라 자세한 [작업 항목](http://nuget.codeplex.com/workitem/1681) 을 참조 하세요.

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a>nuget.exe는 자세한 자세한 정보 표시를 포함 하는 http 요청을 출력 합니다.

Nuget.exe 문제를 해결 하거나 작업 중에 수행 되는 HTTP 요청에 대 한 정보를 확인 하는 경우 '-자세한 정보 ' 스위치는 이제 모든 HTTP 요청을 출력 합니다.

![Nuget.exe의 HTTP 출력](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a>이제 nuget.exe push에서 UNC 및 폴더 소스를 지원 합니다.

NuGet 2.5 이전에는 UNC 경로 또는 로컬 폴더를 기반으로 하는 패키지 원본에 대해 ' nuget.exe push '를 실행 하려고 하면 푸시가 실패 합니다. 최근에 추가 된 계층적 구성 기능을 사용 하는 경우에는 nuget.exe에서 UNC/폴더 원본 또는 HTTP 기반 NuGet 갤러리를 대상으로 해야 하는 것이 일반적 이었습니다.

NuGet 2.5부터 nuget.exe에서 UNC/폴더 원본을 식별 하는 경우 원본으로 파일 복사를 수행 합니다.

이제 다음 명령이 작동 합니다.

```cli
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a>nuget.exe는 명시적으로 지정 된 구성 파일을 지원 합니다.

구성에 액세스 하는 nuget.exe 명령 (' spec ' 및 ' pack ' 제외)은 이제 새로운 '-000' 옵션을 지원 합니다 .이 옵션을 사용 하면 특정 구성 파일 을%Appdata%\nuget\nuget.config의 기본 구성 파일 대신 사용할 수 있습니다.

예:

```cli
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a>네이티브 프로젝트에 대 한 지원

NuGet 2.5을 사용 하면 이제 Visual Studio의 네이티브 프로젝트에서 NuGet 도구를 사용할 수 있습니다. 대부분의 네이티브 패키지는 [coapp 프로젝트](http://coapp.org)에서 만든 도구를 사용 하 여 위의 MSBuild 가져오기 기능을 활용 합니다. 자세한 내용은 coapp.org 웹 사이트의 [도구에 대 한 세부](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) 정보를 참조 하세요.

패키지를 네이티브 프로젝트에 설치할 때 패키지에 대해 \build, \build 및 \tools 파일을 포함 하는 패키지에 대해 대상 프레임 워크 이름 "native"가 도입 되었습니다.  \`lib의 폴더는 네이티브 프로젝트에 사용 되지 않습니다.
