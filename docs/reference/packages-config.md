---
title: NuGet packages.config 파일 참조
description: 일부 프로젝트 형식에서 packages.config은 프로젝트에 사용된 NuGet 패키지 목록을 유지 관리합니다.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/21/2018
ms.topic: reference
ms.openlocfilehash: 2019ce5961a8237fbda855cd7d5b42948808be3a
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817839"
---
# <a name="packagesconfig-reference"></a>packages.config 참조

`packages.config` 파일은 프로젝트에서 참조하는 패키지 목록을 유지하기 위해 일부 프로젝트 형식에서 사용합니다. 이를 통해 해당하는 모든 패키지 없이 빌드 서버와 같은 다른 컴퓨터에 NuGet 때 프로젝트를 전송할 때 쉽게 프로젝트의 종속성을 복원할 수 있습니다.

을 사용 하는 경우 `packages.config` 일반적으로 프로젝트 루트에 배치 됩니다. 첫 번째 NuGet 작업을 실행 하지만 같은 모든 명령을 실행 하기 전에 수동으로 만들 수도 있습니다 때 자동으로 만들어집니다 `nuget restore`합니다.

사용 하는 프로젝트 [PackageReference](../consume-packages/Package-References-in-Project-Files.md) 사용 하지 않는 `packages.config`합니다.

## <a name="schema"></a>스키마

스키마는 단순합니다. 다음과 같은 표준 XML 헤더는 각 참조에 하나씩 하나 이상의 `<package>` 요소가 포함된 단일 `<packages>` 노드입니다. 각 `<package>` 요소에는 다음과 같은 특성이 있을 수 있습니다.

| 특성 | 필수 | 설명 |
| --- | --- | --- |
| ID | 예 | Newtonsoft.json 또는 Microsoft.AspNet.Mvc와 같은 패키지의 식별자입니다. | 
| 버전 | 예 | 3.1.1 또는 4.2.5.11-beta 등 설치할 정확한 버전의 패키지입니다. 버전 문자열에는 3개 이상의 번호가 있어야 합니다. 네 번째는 시험판 접미사로써 선택 사항입니다. 범위는 허용되지 않습니다. | 
| targetFramework | 아니요 | 패키지를 설치하는 경우 적용할 [TFM(대상 프레임워크 모니커)](target-frameworks.md)입니다. 패키지를 설치할 때 처음부터 프로젝트의 대상으로 설정됩니다. 결과적으로 다른 `<package>` 요소에는 다른 TFM가 있을 수 있습니다. 예를 들어 .NET 4.5.2를 대상으로 하는 프로젝트를 만드는 경우 해당 시점에 설치된 패키지는 net452라는 TFM을 사용합니다. 나중에 프로젝트 대상을 .NET 4.6으로 다시 지정하고 추가 패키지를 추가하는 경우 net46이라는 TFM를 사용합니다. 프로젝트의 대상과 `targetFramework` 특성 간에 불일치는 경고를 생성합니다. 이 경우에 영향을 받는 패키지를 다시 설치할 수 있습니다. | 
| allowedVersions | 아니요 | 패키지 업데이트 중에 적용되는 이 패키지에 허용된 버전의 범위입니다([업그레이드 버전 포함](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions) 참조). 설치 또는 복원 작업 중에 설치할 패키지에 영향을 주지 *않습니다*. 구문은 [패키지 버전 관리](../reference/package-versioning.md#version-ranges-and-wildcards)를 참조하세요. 또한 PackageManager UI는 허용되지 않는 모든 버전을 사용하지 않습니다. | 
| developmentDependency | 아니요 | 사용 중인 프로젝트 자체에서 NuGet 패키지를 만드는 경우 종속성을 위해 이 값을 `true`로 설정하면 사용 중인 패키지를 만들 때 해당 패키지를 포함하지 않도록 방지합니다. 기본값은 `false`입니다. | 

## <a name="examples"></a>예제

다음과 같은 `packages.config`은 두 개의 종속성을 가리킵니다.

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="jQuery" version="3.1.1" targetFramework="net46" />
  <package id="NLog" version="4.3.10" targetFramework="net46" />
</packages>
```

다음과 같은 `packages.config`는 9개의 패키지를 참조하지만 `developmentDependency` 특성 때문에 사용 중인 패키지를 빌드할 때 `Microsoft.Net.Compilers`가 포함되지 않습니다. 또한 Newtonsoft.Json에 대한 참조는 8.x 및 9.x 버전에 대한 업데이트를 제한합니다.

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="Microsoft.CodeDom.Providers.DotNetCompilerPlatform" version="1.0.0" targetFramework="net46" />
  <package id="Microsoft.Net.Compilers" version="1.0.0" targetFramework="net46" developmentDependency="true" />
  <package id="Microsoft.Web.Infrastructure" version="1.0.0.0" targetFramework="net46" />
  <package id="Microsoft.Web.Xdt" version="2.1.1" targetFramework="net46" />
  <package id="Newtonsoft.Json" version="8.0.3" allowedVersions="[8,10)" targetFramework="net46" />
  <package id="NuGet.Core" version="2.11.1" targetFramework="net46" />
  <package id="NuGet.Server" version="2.11.2" targetFramework="net46" />
  <package id="RouteMagic" version="1.3" targetFramework="net46" />
  <package id="WebActivatorEx" version="2.1.0" targetFramework="net46" />
</packages>
```
