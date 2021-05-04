---
title: NuGet.org의 패키지 추가 정보
description: NuGet.org의 추가 정보 파일이 렌더링되는 방법 및 문제가 발생할 경우 수행할 작업에 대한 자세한 설명입니다.
author: chgill-MSFT
ms.author: chgill
ms.date: 02/23/2021
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: a5d68329128c9e9d047fe10e08ce41f1ae0895b4
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2021
ms.locfileid: "107902229"
---
# <a name="package-readme-on-nugetorg"></a>NuGet.org의 패키지 추가 정보

사용자에게 더 풍부하고 자세한 패키지 세부 정보를 제공하기 위해 [NuGet 패키지에 추가 정보 파일을 포함합니다](https://docs.microsoft.com/nuget/reference/msbuild-targets#packagereadmefile).

이는 사용자가 NuGet.org에서 패키지 세부 정보 페이지를 볼 때 첫 번째로 표시되는 요소 중 하나이며 좋은 인상을 주는 데 필수적입니다!

> [!IMPORTANT]
> NuGet.org는 [Markdown](https://daringfireball.net/projects/markdown/) 및 제한된 도메인 집합의 이미지에 있는 추가 정보 파일만 지원합니다. NuGet.org에서 추가 정보가 올바르게 렌더링되도록 [이미지](#allowed-domains-for-images-and-badges) 및 [지원되는 Markdown 기능](#supported-markdown-features)에 대해 허용된 도메인을 참조합니다.

## <a name="what-should-my-readme-include"></a>추가 정보에는 무엇이 포함되나요?

추가 정보에 다음 항목을 포함하는 것이 좋습니다.
* 패키지의 정의 및 기능 소개 - 어떤 문제를 해결할 수 있나요?
* 패키지를 시작하는 방법 - 특정 요구 사항이 있나요?
* 추가 정보에 포함되지 않은 경우 보다 포괄적인 설명서에 대한 링크.
* 최소 몇 가지 코드 조각/샘플 또는 예제 이미지.
* 프로젝트 문제, Twitter, 버그 추적기 또는 기타 플랫폼에 대한 링크와 같은 피드백을 남기는 위치 및 방법.
* 해당하는 경우 기여하는 방법.

고품질 추가 정보는 다양한 형식, 형태 및 크기로 구성될 수 있습니다! NuGet.org에서 사용할 수 있는 패키지가 이미 있는 경우, NuGet.org 세부 정보 페이지에 추가될 수 있는 `readme.md` 또는 다른 문서 파일이 리포지토리에 이미 있을 수 있습니다.

## <a name="preview-your-readme"></a>추가 정보 미리 보기

NuGet.org에 출시되기 전에 추가 정보 파일을 미리 보려면 [NuGet.org에서 업로드 패키지 웹 포털](https://docs.microsoft.com/nuget/nuget-org/publish-a-package#web-portal-use-the-upload-package-tab-on-nugetorg)을 사용하여 패키지를 업로드하고 메타데이터 미리 보기의 ‘추가 정보 파일’ 섹션으로 스크롤합니다. 다음과 같이 표시됩니다.

![추가 정보 파일 미리 보기](media\readme-upload-preview.PNG)

잠재적 사용자에게 강한 첫 인상을 줄 수 있도록 [이미지 규정 준수](#allowed-domains-for-images-and-badges) 및 [지원되는 형식](#supported-markdown-features)에 대한 추가 정보 파일을 검토하고 미리 보는 것을 고려하세요! 패키지 추가 정보를 NuGet.org에 게시한 후 수정하려면 수정 사항을 적용한 업데이트된 패키지 버전을 푸시해야 합니다. 모든 사항이 제대로 표시되는지 미리 확인하면 잠재적인 문제를 피할 수 있습니다.
## <a name="allowed-domains-for-images-and-badges"></a>이미지 및 배지에 대해 허용된 도메인

보안 및 개인 정보 문제로 인해 NuGet.org는 이미지 및 배지를 신뢰할 수 있는 호스트로 렌더링할 수 있는 도메인으로 제한합니다. 

NuGet.org를 사용하면 다음 신뢰할 수 있는 도메인에서 배지를 비롯한 모든 이미지를 렌더링할 수 있습니다.
* api.bintray.com
* api.codacy.com
* api.codeclimate.com
* api.dependabot.com
* api.travis-ci.com
* api.travis-ci.org
* app.fossa.io
* badge.fury.io
* badgen.net
* badges.gitter.im
* bettercodehub.com
* buildstats.info
* camo.githubusercontent.com
* ci.appveyor.com
* circleci.com
* codecov.io
* codefactor.io
* coveralls.io
* dev.azure.com
* github.com/.../workflows/.../badge.svg
* gitlab.com
* img.shields.io
* isitmaintained.com
* opencollective.com
* raw.github.com
* raw.githubusercontent.com
* snyk.io
* sonarcloud.io
* user-images.githubusercontent.com

다른 도메인을 허용 목록에 추가해야 하는 경우 [문제를 제출하면](https://github.com/NuGet/NuGetGallery/issues) 엔지니어링 팀에서 개인 정보 보호 및 보안 규정 준수에 대해 검토합니다. 상대적인 로컬 경로의 이미지와 지원되지 않는 도메인에서 호스트된 이미지는 렌더링되지 않으며 패키지 소유자에게만 표시되는 추가 정보 파일 미리 보기 및 패키지 세부 정보 페이지에서 경고를 생성합니다.

## <a name="supported-markdown-features"></a>지원되는 Markdown 기능
[Markdown](https://daringfireball.net/projects/markdown/)은 일반 텍스트 서식 구문을 사용하는 경량 생성 언어입니다. NuGet.org 추가 정보는 [Markdig](https://github.com/lunet-io/markdig) 구문 분석 엔진을 통해 [CommonMark](https://commonmark.org/) 규격 Markdown을 지원합니다.

NuGet.org는 현재 다음 Markdown 기능을 지원합니다.
* [헤더](https://spec.commonmark.org/0.29/#atx-headings)
* [이미지](https://spec.commonmark.org/0.29/#images)
* [추가 강조](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmphasisExtraSpecs.md)
* [목록](https://spec.commonmark.org/0.29/#lists)
* [연결](https://spec.commonmark.org/0.29/#links)
* [블록 따옴표](https://spec.commonmark.org/0.29/#block-quotes)
* [백슬래시 이스케이프](https://spec.commonmark.org/0.29/#backslash-escapes)
* [코드 범위](https://spec.commonmark.org/0.29/#code-spans)
* [작업 목록](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/TaskListSpecs.md)
* [테이블](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/PipeTableSpecs.md)
* [이모지](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmojiSpecs.md)
* [자동 링크](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/AutoLinks.md)

