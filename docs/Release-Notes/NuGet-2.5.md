---
title: NuGet 2.5 릴리스 정보 | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr를 포함 하 여 NuGet 2.5에 대 한 릴리스 정보입니다.
keywords: NuGet 2.5 릴리스 정보, 버그 수정, 알려진 문제, 추가 기능을 Dcr
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 4495e1ea9cc4ec13ef330e56d12de1320cf10b24
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-25-release-notes"></a>NuGet 2.5 릴리스 정보

[NuGet 2.2.1 릴리스 정보](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 릴리스 정보](../release-notes/nuget-2.6.md)

NuGet 2.5는 2013 년 4 월 25 일에 출시 되었습니다. 이 릴리스가 크기가 매우 커서, 버전 2.3 및 2.4 건너뛸 해야 한다면 더 쉬워집니다. 지금까지 있었던 NuGet에 대 한 가장 큰 릴리스는이 통해 [160 작업 항목](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) 릴리스에서 합니다.

## <a name="acknowledgements"></a>감사의 글

NuGet 2.5로의 중요 한 기여에 대 한 다음과 같은 외부 참가자를 감사 하 고 싶습니다.

1. [이 Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))
    - [#2847](https://nuget.codeplex.com/workitem/2847) -추가 MonoAndroid, MonoTouch, 및 MonoMac 알려진된 대상 프레임 워크 식별자 목록에 있습니다.
1. [Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))
    - [#2865](https://nuget.codeplex.com/workitem/2865) -의 철자를 수정 `NuGet.targets` 대/소문자 구분 OS에 대 한
1. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - 솔루션 모노에서 빌드를 확인 합니다.
1. [Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))
    - 모노에서 실패 하는 단위 테스트를 수정 합니다.
1. [Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))
    - [#2920](https://nuget.codeplex.com/workitem/2920) -nuget.exe 팩 명령 속성을 MSBuild 전파 하지 않습니다
1. [Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))
    - [#1511](https://nuget.codeplex.com/workitem/1511) -수정 하는 XML 처리 코드를 서식 유지 합니다.
1. [Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - 성공 하려면 build.cmd 수 있도록 사용자 지정 사전에 인식 된 단어를 추가 합니다.
1. [Bruno Roggeri](https://www.codeplex.com/site/users/view/broggeri)
    - 지역화 된 VS에서 실행할 때 단위 테스트를 수정 합니다.
1. [Gareth Evans](https://www.codeplex.com/site/users/view/garethevans)
    - PackageService에서 추출 된 인터페이스
1. [Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))
    - [#936](https://nuget.codeplex.com/workitem/936) -압축 하는 경우 프로젝트 종속성을 처리 합니다.
1. [Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))
    - [#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) -지원 일반 텍스트 암호 nuget.cofig 파일에 패키지 원본 자격 증명을 저장할 때
1. [James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))
    - [#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) -패키지 가져오기 해결 도움말 설명

또한와 NuGet 2.5 베타/RC 승인 또는 최종 릴리스 전에 해결 된 버그를 발견 하는 것에 대 한 다음 개인을 보내주셔서 감사:

1. [Tony 벽](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))
    - [#3200](https://nuget.codeplex.com/workitem/3200) -2.5 빌드되고 최신 NuGet 2.4 끊어진 MSTest

## <a name="notable-features-in-the-release"></a>릴리스에서 주목할 만한 기능

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a>사용자가 이미 있는 콘텐츠 파일을 덮어쓸 수 있도록

모든 시간을 가장 많이 요청한 기능 중 하나는 NuGet 패키지에 포함 하는 경우 디스크에 이미 있는 콘텐츠 파일을 덮어쓸 수 되었습니다. NuGet 2.5 부터는 이러한 충돌은 식별 되며 이러한 파일을 항상 건너뜁니다 이전에 있지만 파일을 덮어쓸지 묻는.

![콘텐츠 파일 덮어쓰기](./media/NuGet-2.5/overwrite-file.png)

'nuget.exe 업데이트' 및 ' Install-package ' 새 옵션을 둘 다 이제 '-FileConflictAction' 명령줄 시나리오에 대 한 몇 가지 기본 설정할 수 있습니다.

패키지에서 파일 대상 프로젝트에 이미 있는 경우 기본 동작을 설정 합니다. 항상 파일을 덮어쓰려면 '덮어쓰기'로 설정 합니다. 파일을 건너 뛰을 '무시'로 설정 합니다. 지정 하지 않으면 각 충돌 하는 파일에 대 한 라는 메시지가 나타납니다.

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a>MSBuild 대상 및 props 파일이 자동으로 가져오도록

NuGet 패키지의 최상위 수준에서 새 규칙에 따른 폴더 생성 되었습니다.  피어로 `\lib`, `\content`, 및 `\tools`, 이제 포함할 수 있습니다는 `\build` 패키지에는 폴더입니다.  이 폴더 아래에 고정 된 이름 가진 두 개의 파일을 배치할 수 있습니다 `{packageid}.targets` 또는 `{packageid}.props`합니다. 이 두 일 수 직접 아래 `build` 보드나 다른 폴더 처럼 프레임 워크별 폴더입니다. 가장 일치 하는 프레임 워크 폴더를 선택 하는 데 규칙은 정확히 동일 하는 것입니다.

MSBuild를 추가 합니다 \build 파일과 함께 NuGet 패키지는 설치 될 때 `<Import>` 가리키는 프로젝트 파일의 요소는 `.targets` 및 `.props` 파일입니다. `.props` 반면 맨 위에 있는 파일이 추가 되는 `.targets` 파일 맨 아래에 추가 됩니다.

### <a name="specify-different-references-per-platform-using-references-element"></a>사용 하 여 플랫폼 마다 다른 참조를 지정 `<References/>` 요소

2.5에서는 이전에 `.nuspec` 파일인 사용자 추가할 모든 프레임 워크에 대 한 참조 파일을 지정할만 수 있습니다. 2.5의이 새로운 기능, 사용자를 작성할 수 이제는 `<reference/>` 각 예제에 대 한 지원 되는 플랫폼에 대 한 요소:

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

NuGet에 따라 프로젝트에 대 한 참조를 추가 하는 방법에 대 한의 흐름이 고 `.nuspec` 파일:

1. 찾기의 `lib` 대상 프레임 워크에 대 한 적합 하 고 해당 폴더에서 어셈블리의 목록을 가져올 수 있는 폴더
1. 대상 프레임 워크에 대 한 적절 한 포함 된 참조 그룹을 찾아 해당 그룹에서 어셈블리의 목록을 가져올 별도로 합니다. 지정 된 대상 프레임 워크 없이 참조 그룹은 대체 (fallback) 그룹입니다.
1. 두 목록의 교차를 찾아 추가할 참조로 사용 하는

이 새로운 기능을 사용 하면 패키지에서 여러 중복 어셈블리를 수행 하 고, 그렇지는 경우 어셈블리의 하위 집합 다양 한 프레임 워크에 적용할 참조 기능을 사용 하는 작성자 `lib` 폴더입니다.

참고: 현재 사용 해야 nuget.exe 팩;이 기능을 사용 하려면 NuGet 패키지 탐색기 아직 없으므로 해당 합니다.

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a>모든 패키지를 한 번에 업데이트를 허용 하는 모든 단추 업데이트

여러분 중 많은 알고 "업데이트 패키지" PowerShell cmdlet에 대 한 모든 패키지; 업데이트 이제 쉽게도 UI를 통해이 작업을 수행할 수 있습니다.

이 기능을 사용해 보세요 하:

1. 새 ASP.NET MVC 응용 프로그램 만들기
1. NuGet 패키지 관리 ' 대화 상자를 시작
1. '업데이트'를 선택 합니다.
1. ' 업데이트 모두 ' 단추를 클릭 합니다.

![대화 상자에서 모든 단추 업데이트](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a>Nuget.exe 팩에 대 한 향상 된 프로젝트 참조 지원

이제 nuget.exe 팩 명령 프로세스는 다음 규칙을 사용 하 여 프로젝트를 참조합니다.

1. 참조 된 프로젝트에 해당 하는 경우 `.nuspec` 파일, 예를 들어 라는 파일은 `proj1.nuspec` 와 같은 폴더에 `proj1.csproj`, 그런 다음이 프로젝트 id를 사용 하 여 패키지를 종속성으로 추가 됩니다 및 버전에서 읽을 `.nuspec` 파일입니다.
1. 그렇지 않은 경우 참조 된 프로젝트의 파일이 패키지에 제공 됩니다. Sames 규칙 재귀적으로 사용 하 여이 프로젝트에서 참조 하는 프로젝트를 처리 한 다음 됩니다.
1. 모든 DLL `.pdb`, 및 `.exe` 파일이 추가 됩니다.
1. 다른 모든 콘텐츠 파일이 추가 됩니다.
1. 모든 종속성 병합 됩니다.

이렇게 하면 참조 된 프로젝트가 없는 경우 종속 항목으로 간주 한 `.nuspec` 파일, 그렇지 않으면 패키지의 일부가 됩니다.

자세한 내용은 여기: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)

### <a name="add-a-minimum-nuget-version-property-to-packages"></a>패키지에 '는 최소 NuGet 버전 ' 속성을 추가 합니다.

새 메타 데이터 특성 'minClientVersion' 라는 패키지를 사용 하는 데 필요한 최소 NuGet 클라이언트 버전을 나타낼 이제 수 있습니다.

이 기능을 사용 하면 패키지를 만든 후에 특정 버전의 NuGet 패키지 작동 하는지 지정할 수 있습니다. 새 `.nuspec` NuGet 2.5 후 패키지를 최소 NuGet 버전 요청할 됩니다 하는 기능을 추가 합니다.

```xml
<metadata minClientVersion="2.6">
```

사용자에 게 NuGet 2.5가 설치 되어 있고 2.6 필요한 것으로 식별 되는 패키지, 시각 신호를 패키지를 설치할 수는 사용자에 게 주어 집니다. 사용자가 해당 버전의 NuGet이를 업데이트 하려면 다음 안내 됩니다.

이 패키지를 설치 하 고 다음 인식할 수 없는 스키마 버전 확인 됨을 나타내는 실패 시작 하는 위치는 기존 환경을 보다 개선 됩니다.

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a>종속성은 패키지를 설치 하는 동안 불필요 하 게 더 이상 업데이트

NuGet 2.5 하기 전에 패키지는 프로젝트에 이미 설치 된 패키지에 의존 하는 설치 될 때 종속성 업데이트 됩니다 새 설치의 일부로 기존 버전의 종속성을 충족 하는 경우에 합니다.

종속성의 버전을 충족 하는 이미 없으면 NuGet 2.5 부터는 종속성 업데이트 되지 않습니다 다른 패키지 설치 중입니다.

**시나리오:**

1. 소스 저장소 B 패키지 버전 1.0.0 및 1.0.2 포함 되어 있습니다. 패키지 A가 B에 종속 된도 포함 되어 (> = 1.0.0).
1. 현재 프로젝트에 이미 B 패키지 버전 1.0.0 설치 되어 있다고 가정 합니다. 이제 1. 패키지를 설치

**에 NuGet 2.2 및 이전 버전:**

* 패키지 A를 설치할 때 NuGet는 자동 업데이트 B 1.0.2 1.0.0 기존 버전에는 이미 되는 종속성 버전 제약 조건을 만족 하는 경우에 > 1.0.0 = 합니다.

**에 NuGet 2.5 이상 버전:**

* 기존 버전 1.0.0 종속성 버전 제약 조건을 만족 하는 것이 있기 때문 NuGet 더 이상 B를 업데이트 합니다.

이러한 변경 사항에 자세한 배경을 알고 싶으면, 자세한 읽기 [작업 항목](http://nuget.codeplex.com/workitem/1681) 관련 뿐만 아니라 [토론 스레드](http://nuget.codeplex.com/discussions/436712)합니다.

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a>nuget.exe 출력의 자세한 정도 http 요청

Nuget.exe 문제를 해결 하거나 just 하는 경우 자세한 내용을 보려면 어떤 HTTP 요청이 작업 중 수행 되는 '-자세한 세부 정보 표시 ' 스위치 이제 만든 모든 HTTP 요청을 출력 합니다.

![HTTP output from nuget.exe](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a>nuget.exe 푸시 UNC 및 폴더 원본 지원

NuGet 2.5 하기 전에 로컬 폴더 또는 UNC 경로 기반으로 하는 패키지 소스에 'nuget.exe 푸시'를 실행 하려고 하는 경우 push 실패 합니다. 최근에 추가 된 계층적 구성 기능을 사용 하면 nuget.exe를 대상으로 지정 된 UNC/폴더 원본 또는 HTTP 기반 NuGet 갤러리를 일반화 했습니다.

Nuget.exe UNC/폴더 소스를 식별 하는 경우 NuGet 2.5 부터는 파일 복사는 소스를 수행 합니다.

다음 명령은 작동 하지 않습니다.

```
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a>nuget.exe은 명시적으로 지정 된 구성 파일을 지원합니다.

이제 구성 ('사양' 및 '팩'를 제외한 모든)에 액세스 하는 nuget.exe 명령을 새 지원 '-ConfigFile' 옵션을 강제로 특정 config 파일을 %AppData%\nuget\Nuget.Config 기본 구성 파일 대신 사용할 수 있습니다.

예제:

```
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a>네이티브 프로젝트에 대 한 지원

NuGet 2.5로 NuGet 도구 Visual Studio의 네이티브 프로젝트에 대 한 출시 되었습니다. 작업도 수행 하지 가장 네이티브 패키지는 위의 MSBuild 가져오기 기능을 사용 하 여 만든 도구를 사용 하 여 [CoApp 프로젝트](http://coapp.org)합니다. 자세한 내용은 [도구에 대 한 세부 정보](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) coapp.org 웹사이트에서.

네이티브 프로젝트에 패키지를 설치할 때 \build, \content, 및 \tools에 파일을 포함 하는 패키지에 대 한 "기본"의 대상 프레임 워크 이름을 도입 되었습니다.  \`lib' 폴더는 네이티브 프로젝트에 사용 되지 않습니다.
