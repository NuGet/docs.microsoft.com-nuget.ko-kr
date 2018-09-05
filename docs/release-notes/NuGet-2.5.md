---
title: NuGet 2.5 릴리스 정보
description: NuGet 2.5의 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr 포함에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 29d0b33714a574281680e110b967269699afbaf1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550485"
---
# <a name="nuget-25-release-notes"></a>NuGet 2.5 릴리스 정보

[NuGet 2.2.1 릴리스 정보](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 릴리스 정보](../release-notes/nuget-2.6.md)

NuGet 2.5는 2013 년 4 월 25 년에 출시 되었습니다. 이 릴리스에서 큰 숫자를 버전 2.3 및 2.4를 건너뛰기 해야 한다면 판단 했습니다! 이것은 사용 하 여 NuGet에 대 한 했으므로 가장 큰 릴리스입니다까지 위로 [160 작업 항목](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) 릴리스에서 합니다.

## <a name="acknowledgements"></a>감사의 글

NuGet 2.5에 대 한 중요 한 기여에 대 한 다음 외부 참가자를 감사 하려고 합니다.

1. [Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))
    - [#2847](https://nuget.codeplex.com/workitem/2847) -추가 MonoAndroid, MonoTouch, 및 MonoMac 알려진된 대상 프레임 워크 식별자 목록에 있습니다.
2. [Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))
    - [#2865](https://nuget.codeplex.com/workitem/2865) -의 철자를 수정 `NuGet.targets` 대/소문자 구분 os
3. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - Mono를 토대로 솔루션을 확인 합니다.
4. [Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))
    - Mono에서 실패 하는 단위 테스트를 수정 합니다.
5. [Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))
    - [#2920](https://nuget.codeplex.com/workitem/2920) -nuget.exe pack 명령 MSBuild 속성을 전파 하지 않습니다
6. [Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))
    - [#1511](https://nuget.codeplex.com/workitem/1511) -수정 XML 처리 코드 서식 지정을 유지 합니다.
7. [Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - Build.cmd 성공할 수 있도록 사용자 지정 사전에 인식 된 단어를 추가 합니다.
8. [Bruno Roggeri](https://www.codeplex.com/site/users/view/broggeri)
    - 지역화 된 VS에서 실행할 때 단위 테스트를 수정 합니다.
9. [Gareth Evans](https://www.codeplex.com/site/users/view/garethevans)
    - PackageService에서 추출 된 인터페이스
10. [Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))
     - [#936](https://nuget.codeplex.com/workitem/936) -압축할 때 프로젝트 종속성을 처리 합니다.
11. [Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))
     - [#2991](https://nuget.codeplex.com/workitem/2991)하십시오 [#3164](https://nuget.codeplex.com/workitem/3164) -지원 일반 텍스트 암호 nuget.cofig 파일에서 패키지 원본 자격 증명을 저장 하는 경우
12. [James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))
     - [#3190](http://nuget.codeplex.com/workitem/3190)하십시오 [#3191](http://nuget.codeplex.com/workitem/3191) -패키지 가져오기 수정 되는 도움말 설명

또한 사용 하 여 NuGet 2.5 Beta/RC 승인 하 고 최종 릴리스 전에 수정 된 버그 찾기에 대 한 개인 감사:

1. [Tony 벽](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))
    - [#3200](https://nuget.codeplex.com/workitem/3200) -MSTest 최신 NuGet 2.4 및 2.5 빌드를 사용 하 여 분할

## <a name="notable-features-in-the-release"></a>릴리스에서 주목할 만한 기능

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a>이미 존재 하는 콘텐츠 파일을 덮어쓰기 할 수 있습니다.

모든 시간을 가장 많이 요청 된 기능 중 하나는 NuGet 패키지에 포함 하는 경우 디스크에 이미 있는 콘텐츠 파일을 덮어쓰는 기능이 되었습니다. NuGet 2.5부터 이러한 충돌은 식별 하 고 이전에 이러한 파일을 건너뜁니다 항상 반면 파일을 덮어쓸지 묻는 합니다.

![콘텐츠 파일 덮어쓰기](./media/NuGet-2.5/overwrite-file.png)

'nuget.exe 업데이트' 및 ' Install-package ' 새 옵션이 모두 이제 '-FileConflictAction' 명령줄 시나리오에 대 한 몇 가지 기본값을 설정 합니다.

패키지에서 파일을 대상 프로젝트에 이미 있는 경우에 기본 동작을 설정 합니다. 항상 파일을 덮어쓰려면 '덮어쓰기'로 설정 합니다. 파일 건너뛰기 '무시'로 설정 합니다. 지정 하지 않으면 각 충돌 하는 파일에 대 한 라는 메시지가 나타납니다.

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a>MSBuild targets 및 props 파일의 자동 가져오기

NuGet 패키지의 최상위 수준에서 새 기본 폴더를 만들었습니다.  에 대 한 피어 `\lib`, `\content`, 및 `\tools`, 이제 포함할 수 있습니다는 `\build` 패키지에는 폴더입니다.  이 폴더 아래에 있는 고정 된 이름 가진 두 개의 파일을 배치할 수 있습니다 `{packageid}.targets` 또는 `{packageid}.props`합니다. 이 두 파일에서 하거나 직접 수 `build` 또는 다른 폴더와 마찬가지로 프레임 워크별 폴더입니다. 가장 일치 하는 프레임 워크 폴더를 선택 하는 것에 대 한 규칙 것 처럼 정확히 동일 합니다.

NuGet에서 \build 파일이 포함 된 패키지를 설치할 때 MSBuild 추가 `<Import>` 가리키는 프로젝트 파일의 요소를 `.targets` 고 `.props` 파일. 합니다 `.props` 반면 맨 위에 있는 파일이 추가 되는 `.targets` 파일 맨 아래에 추가 됩니다.

### <a name="specify-different-references-per-platform-using-references-element"></a>사용 하 여 플랫폼 마다 다른 참조 지정 `<References/>` 요소

2.5에서는 이전에 `.nuspec` 파일을 지정할 수 있습니다만 모든 프레임 워크에 대 한 추가 참조 파일입니다. 이제 2.5에서이 새로운 기능을 사용 하 여 사용자를 작성할 수는 `<reference/>` 의 예를 들어 지원 되는 플랫폼의 각 요소:

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

다음은 NuGet 기반으로 프로젝트에 대 한 참조를 추가 하는 방법에 대 한 흐름을 `.nuspec` 파일:

1. 찾기는 `lib` 적합 한 대상 프레임 워크는 해당 폴더에서 어셈블리의 목록을 가져올 폴더
1. 대상 프레임 워크에 적절 한 참조 그룹 찾아 개별적으로 해당 그룹에서 어셈블리의 목록을 가져옵니다. 대상 프레임 워크를 지정 하지 않고 참조 그룹은 대체 (fallback) 그룹입니다.
1. 두 목록에서의 교집합을 찾습니다를 사용 하는 참조로 추가

이 새로운 기능을 사용 하면 여러에서 중복 어셈블리를 전달할 그렇지 않은 경우는 필요할 때 다른 프레임 워크 어셈블리의 하위 집합을 적용 하려면 참조 기능을 사용 하려면 패키지 작성자 `lib` 폴더입니다.

참고: 현재 사용 해야 nuget.exe 팩이이 기능을 사용 하려면 NuGet 패키지 탐색기는 아직 지원 하지.

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a>모든 패키지를 한 번에 업데이트를 허용 하도록 모든 단추를 업데이트 합니다.

많은 "Update-package" PowerShell cmdlet에 대 한를 업데이트 해야 한다고 모든 패키지 있습니다. 이제 쉽게도 UI를 통해이 작업을 수행할 수 있습니다.

이 기능을 사용해:

1. 새 ASP.NET MVC 응용 프로그램 만들기
1. NuGet 패키지 관리 ' 대화 상자를 시작 합니다.
1. '업데이트'를 선택 합니다.
1. ' 모두 업데이트 ' 단추를 클릭 합니다.

![업데이트 대화 상자에서 모든 단추](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a>Nuget.exe 팩에 대 한 향상 된 프로젝트 참조 지원

이제 nuget.exe 팩 명령 프로세스에는 다음 규칙을 사용 하 여 프로젝트 참조:

1. 참조 된 프로젝트에 해당 하는 경우 `.nuspec` 파일, 예를 들어 라는 파일 `proj1.nuspec` 와 같은 폴더에 `proj1.csproj`, 한 다음이 프로젝트의 id를 사용 하 여 패키지를 종속성으로 추가 됩니다 및 버전에서 읽기를 `.nuspec` 파일입니다.
1. 그렇지 않으면 참조 된 프로젝트의 파일은 패키지에 제공 됩니다. 그대로 계속 규칙 재귀적으로 사용 하 여이 프로젝트에서 참조 된 프로젝트를 처리 한 다음 됩니다.
1. 모든 DLL `.pdb`, 및 `.exe` 파일이 추가 됩니다.
1. 다른 모든 콘텐츠 파일이 추가 됩니다.
1. 모든 종속성에 병합 됩니다.

이렇게 하면 참조 된 프로젝트가 없는 경우 종속성으로 간주는 `.nuspec` 파일, 그렇지 않으면 패키지의 일부가 됩니다.

자세한 내용은 여기서: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)

### <a name="add-a-minimum-nuget-version-property-to-packages"></a>패키지에 ' 최소 NuGet 버전 ' 속성을 추가 합니다.

'MinClientVersion' 라는 새 메타 데이터 특성을 패키지를 사용 하는 데 필요한 최소 NuGet 클라이언트 버전을 나타낼 이제 수 있습니다.

이 기능을 사용 하면 패키지를 만든 후에 특정 버전의 NuGet은 패키지를 작동 되도록 합니다. 새 `.nuspec` NuGet 2.5 후 패키지를 최소 NuGet 버전을 클레임 할 수 하는 기능을 추가 합니다.

```xml
<metadata minClientVersion="2.6">
```

사용자에 게 NuGet 2.5를 설치 하는 경우 패키지 2.6 필요한 것으로 식별 되는 패키지를 설치할 수 없음을 나타내는 사용자에 게 시각 신호 제공 됩니다. NuGet의 해당 버전을 업데이트 하려면 사용자를 안내 합니다.

이 패키지를 인식할 수 없는 스키마 버전 확인 됨을 나타내는 실패 하지만 설치를 시작 하는 위치는 기존 환경으로 향상 됩니다.

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a>종속성이 불필요 하 게 더 이상 패키지 설치 중 업데이트

NuGet 2.5 하기 전에 프로젝트에 이미 설치 된 패키지에 종속 된 패키지를 설치할 때 종속성 업데이트 됩니다 새 설치의 일부로 기존 버전의 종속성을 충족 하는 경우에 합니다.

종속성 버전이 이미 충족 된 경우 NuGet 2.5부터 종속성 업데이트 되지 않습니다 하는 동안 다른 패키지를 설치 합니다.

**시나리오:**

1. 소스 리포지토리에 B 패키지 버전 1.0.0 및 1.0.2를 포함합니다. B에 종속 된 A 패키지도 포함 (> = 1.0.0).
1. 현재 프로젝트에 이미 B 패키지 버전 1.0.0 설치 되어 있다고 가정 합니다. 이제 1. 패키지를 설치

**Nuget 2.2 이상:**

* 패키지는 설치할 때 NuGet은 자동 업데이트 B 1.0.2 되는 종속성 버전 제약 조건을 이미 충족 하는 기존 버전 1.0.0도 > 1.0.0 =.

**Nuget 2.5 이상:**

* 기존 버전 1.0.0 종속성 버전 제약 조건을 충족 함을 감지한 때문에 NuGet 더 이상 B를 업데이트 합니다.

이러한 변경 사항에 자세한 배경 정보를 보려면 읽을 [작업 항목](http://nuget.codeplex.com/workitem/1681) 관련 뿐만 [토론 스레드](http://nuget.codeplex.com/discussions/436712)합니다.

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a>nuget.exe 자세한 세부 정보 표시를 사용 하 여 http 요청을 출력

방금 nuget.exe 문제를 해결 하는 경우 궁금한 점이 있으면 어떤 HTTP 요청 작업 중의 '-자세한 세부 정보 표시 ' 스위치 이제 모든 HTTP 요청을 출력 합니다.

![Nuget.exe에서 HTTP 출력](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a>nuget.exe push가 이제 UNC 및 폴더 원본

NuGet 2.5 하기 전에 로컬 폴더 또는 UNC 경로에 따라 패키지 소스에 'nuget.exe push'를 실행 하려는 경우 푸시 실패 합니다. 최근에 추가 된 계층적 구성 기능을 사용 하 여 UNC/폴더 원본에서 또는 HTTP 기반 NuGet 갤러리를 대상으로 해야 하는 nuget.exe 보편화 했습니다.

NuGet 2.5부터 nuget.exe UNC/폴더 소스를 식별 하는 경우 원본에 파일 복사를 수행 합니다.

다음 명령은 작동 합니다.

```
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a>nuget.exe는 명시적으로 지정 된 구성 파일을 지원합니다.

이제 구성 ('사양' 및 '팩' 제외 하 고 모두)에 액세스 하는 nuget.exe 명령을 지원 새 '-ConfigFile' %AppData%\nuget\Nuget.Config 기본 구성 파일 대신 사용할 특정 구성 파일을 강제로 수행 하는 옵션입니다.

예제:

```
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a>네이티브 프로젝트에 대 한 지원

NuGet 2.5를 사용 하 여 NuGet 도구는 Visual Studio에서 네이티브 프로젝트에 대 한 출시 되었습니다. 기대 가장 네이티브 패키지는 위의 MSBuild 가져오기 기능을 활용 하 여 만든 도구를 사용 하 여 [CoApp 프로젝트](http://coapp.org)합니다. 자세한 내용은 [도구에 대 한 세부 정보](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) coapp.org 웹 사이트입니다.

대상 프레임 워크 이름은 "네이티브"는 네이티브 프로젝트에 패키지를 설치할 때 \build, \content 및 \tools에서 파일을 포함 하려면 패키지에 대 한 도입 되었습니다.  \`lib' 폴더의 네이티브 프로젝트는 사용 되지 않습니다.
