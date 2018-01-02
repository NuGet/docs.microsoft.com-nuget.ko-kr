---
title: "Visual Studio 템플릿의 NuGet 패키지 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 2/8/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 0b2cf228-f028-475d-8792-c012dffdb26f
description: "Visual Studio 프로젝트 및 항목 템플릿의 일부로 NuGet 패키지를 포함하는 방법에 대한 지침입니다."
keywords: "Visual Studio의 NuGet, Visual Studio 프로젝트 템플릿, Visual Studio 항목 템플릿, 프로젝트 템플릿의 패키지, 항목 템플릿의 패키지"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 5b2ad7616578b5f54d917c4555e861c847814da9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="packages-in-visual-studio-templates"></a>Visual Studio 템플릿의 패키지

Visual Studio 프로젝트 및 항목 템플릿에서는 프로젝트 또는 항목을 만들 때 특정 패키지가 설치되어 있는지 확인해야 합니다. 예를 들어 ASP.NET MVC 3 템플릿은 jQuery, Modernizr 및 기타 패키지를 설치합니다.

이를 지원하기 위해 템플릿 작성자는 개별 라이브러리가 아닌 필요한 패키지를 설치하도록 NuGet에 지시할 수 있습니다. 그러면 개발자가 나중에 언제든지 해당 패키지를 쉽게 업데이트할 수 있습니다.

템플릿을 직접 작성하는 방법에 대한 자세한 내용은 [Visual Studio에서 프로젝트 및 항목 템플릿 만들기](https://msdn.microsoft.com/library/s365byhx.aspx) 또는 [Visual Studio SDK를 사용하여 사용자 지정 프로젝트 및 항목 템플릿 만들기](https://msdn.microsoft.com/library/ff527340.aspx)를 참조하세요.

이 섹션의 나머지 부분에서는 NuGet 패키지가 제대로 포함되도록 템플릿을 작성할 때 수행할 특정 단계에 대해 설명합니다.

- [템플릿에 패키지 추가](#adding-packages-to-a-template)
- [모범 사례](#best-practices)

예를 들어 [NuGetInVsTemplates 샘플](https://bitbucket.org/marcind/nugetinvstemplates)을 참조하세요.


## <a name="adding-packages-to-a-template"></a>템플릿에 패키지 추가

템플릿이 인스턴스화되면 [템플릿 마법사](https://msdn.microsoft.com/library/ms185301.aspx)가 호출되어 패키지 설치 위치에 대한 정보와 함께 설치할 패키지 목록을 로드합니다. 패키지는 VSIX 또는 템플릿에 포함되어 있거나 로컬 하드 드라이브에 있을 수 있습니다. 이 경우 레지스트리 키를 사용하여 파일 경로를 참조합니다. 이러한 위치에 대한 자세한 내용은 이 섹션의 뒷부분에서 설명합니다.

미리 설치된 패키지는 [템플릿 마법사](http://msdn.microsoft.com/library/ms185301.aspx)를 사용하여 작동합니다. 템플릿이 인스턴스화될 때 특별한 마법사가 호출됩니다. 마법사는 설치해야 할 패키지 목록을 로드하고 해당 정보를 적절한 NuGet API에 전달합니다.

템플릿에 패키지를 포함하는 단계:

1. `vstemplate` 파일에 [`WizardExtension`](http://msdn.microsoft.com/library/ms171411.aspx) 요소를 추가하여 NuGet 템플릿 마법사에 대한 참조를 추가합니다.

    ```xml
    <WizardExtension>
        <Assembly>NuGet.VisualStudio.Interop, Version=1.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a</Assembly>
        <FullClassName>NuGet.VisualStudio.TemplateWizard</FullClassName>
    </WizardExtension>
    ```

    `NuGet.VisualStudio.Interop.dll`은 `TemplateWizard` 클래스만 포함하는 어셈블리이며, `NuGet.VisualStudio.dll`의 실제 구현을 호출하는 간단한 래퍼입니다. 프로젝트/항목 템플릿이 새 버전의 NuGet에서 계속 작동할 수 있도록 어셈블리 버전은 변경되지 않습니다.

1. 프로젝트에 설치할 패키지의 목록을 추가합니다.

    ```xml
    <WizardData>
        <packages>
            <package id="jQuery" version="1.6.2" />
        </packages>
    </WizardData>
    ```

    *(NuGet 2.2.1 이상)* 마법사는 여러 `<package>` 요소를 지원하여 여러 패키지 원본을 지원합니다. `id` 및 `version` 특성은 모두 필요합니다. 즉 최신 버전을 사용할 수 있는 경우에도 특정 버전의 패키지가 설치됩니다. 이렇게 하면 패키지 업데이트로 인해 템플릿이 손상되지 않도록 방지하고, 템플릿을 사용하여 개발자에게 패키지를 업데이트하도록 선택할 수 있게 합니다.


1. 다음 섹션에서 설명한 대로 NuGet에서 패키지를 찾을 수 있는 리포지토리를 지정합니다.

### <a name="vsix-package-repository"></a>VSIX 패키지 리포지토리

Visual Studio 프로젝트/항목 템플릿을 배포하는 데 권장되는 방법은 [VSIX 확장](http://msdn.microsoft.com/library/ff363239.aspx)에 있습니다. 이를 통해 여러 프로젝트/항목 템플릿을 함께 패키지할 수 있고 개발자가 VS 확장 관리자 또는 Visual Studio 갤러리를 사용하여 템플릿을 쉽게 검색할 수 있기 때문입니다. 또한 확장에 대한 업데이트는 [Visual Studio 확장 관리자 자동 업데이트 메커니즘](http://msdn.microsoft.com/library/dd997169.aspx)을 사용하여 쉽게 배포할 수 있습니다.

VSIX 자체는 다음과 같이 템플릿에 필요한 패키지의 원본으로 사용할 수 있습니다.

1. `.vstemplate` 파일의 `<packages>` 요소를 다음과 같이 수정합니다.

    ```xml
    <packages repository="extension" repositoryId="MyTemplateContainerExtensionId">
        <!-- ... -->
    </packages>
    ```

    `repository` 특성은 리포지토리의 유형을 `extension`으로 지정하고, `repositoryId`는 VSIX 자체의 고유 식별자입니다(이 값은 확장의 `vsixmanifest` 파일에 있는 [`ID` 특성](http://msdn.microsoft.com/library/dd393688.aspx)의 값임).

1. `nupkg` 파일을 VSIX 내의 `Packages`라는 폴더에 배치합니다.
1. [사용자 지정 확장 콘텐츠](http://msdn.microsoft.com/library/dd393737.aspx)로 필요한 패키지 파일을 `source.extension.vsixmanifest` 파일에 추가합니다. 2.0 스키마를 사용하는 경우 다음과 같이 표시됩니다.

    ```xml
    <Asset Type="Moq.4.0.10827.nupkg" d:Source="File" Path="Packages\Moq.4.0.10827.nupkg" d:VsixSubPath="Packages" />
    ```

    1.0 스키마를 사용하는 경우 다음과 같이 표시됩니다.

    ```xml
    <CustomExtension Type="Moq.4.0.10827.nupkg">
        packages/Moq.4.0.10827.nupkg
    </CustomExtension>
    ```

1. 프로젝트 템플릿과 동일한 VSIX에 패키지를 전달할 수 있거나 시나리오에 적합한 경우 별도의 VSIX에 배치할 수 있습니다. 그러나 해당 확장을 변경하면 템플릿이 손상될 수 있으므로 제어 권한이 없는 VSIX는 참조하지 않습니다.


### <a name="template-package-repository"></a>템플릿 패키지 리포지토리

단일 프로젝트/항목 템플릿만 배포하고 여러 템플릿을 함께 패키지할 필요가 없으면, 프로젝트/항목 템플릿 ZIP 파일에 직접 패키지를 포함하는 간단하지만 더 제한적인 방법을 사용할 수 있습니다.

1. `.vstemplate` 파일의 `<packages>` 요소를 다음과 같이 수정합니다.

    ```xml
    <packages repository="template"">
        <!-- ... -->
    </packages>
    ```

    `repository` 특성의 값은 `template`이며, `repositoryId` 특성은 필요하지 않습니다.

1. 프로젝트/항목 템플릿 ZIP 파일의 루트 폴더에 패키지를 배치합니다.

여러 템플릿이 포함된 VSIX에 이 방법을 사용하는 경우 하나 이상의 패키지가 템플릿에 공통적으로 포함되면 불필요한 블로트가 발생합니다. 이러한 경우 이전 섹션에서 설명한 대로 [VSIX를 리포지토리로](#vsix-package-repository) 사용합니다.


### <a name="registry-specified-folder-path"></a>레지스트리에 지정된 폴더 경로

MSI를 사용하여 설치된 SDK는 개발자의 컴퓨터에 NuGet 패키지를 직접 설치할 수 있습니다. 이렇게 하면 프로젝트 또는 항목 템플릿을 사용하는 경우 해당 시간에 추출하지 않고도 패키지를 바로 사용할 수 있습니다. ASP.NET 템플릿은 이 방법을 사용합니다.

1. MSI에서 패키지를 컴퓨터에 설치하도록 합니다. `.nupkg` 파일만 설치하거나 확장된 내용과 함께 해당 파일을 설치할 수도 있습니다. 그러면 템플릿을 사용할 때 추가 단계가 저장됩니다. 이 경우 `.nupkg` 파일이 루트 폴더에 있는 NuGet의 표준 폴더 구조를 따르고, 각 패키지에는 ID/버전 쌍이 하위 폴더 이름인 하위 폴더가 있습니다.

1. 패키지 위치를 식별하는 레지스트리 키를 작성합니다.

    - 키 위치: 컴퓨터 수준에서는 `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository`를 사용하고, 사용자별로 설치된 템플릿 및 패키지인 경우 `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`를 사용합니다.
    - 키 이름: 고유한 이름을 사용합니다. 예를 들어 VS 2012용 ASP.NET MVC 4 템플릿인 경우 `AspNetMvc4VS11`을 사용합니다.
    - 값: packages 폴더에 대한 전체 경로입니다.

1. `.vstemplate` 파일의 `<packages>` 요소에 `repository="registry"` 특성을 추가하고, `keyName` 특성에 레지스트리 키 이름을 지정합니다.

    - 패키지의 압축을 미리 푼 경우 `isPreunzipped="true"` 특성을 사용합니다.
    - *(NuGet 3.2 이상)*  패키지 설치의 끝에서 디자인 타임 빌드를 강제로 수행하려면 `forceDesignTimeBuild="true"` 특성을 추가합니다.
    - 필요한 참조가 템플릿 자체에 이미 포함되어 있으므로 최적화를 위해 `skipAssemblyReferences="true"`를 추가합니다.

        ```xml
        <packages repository="registry" keyName="AspNetMvc4VS11" isPreunzipped="true">
            <package id="EntityFramework" version="5.0.0" skipAssemblyReferences="true" />
            <-- ... -->
        </packages>
        ```

## <a name="best-practices"></a>모범 사례

1. NuGet VSIX에 대한 참조를 VSIX 매니페스트에 추가하여 NuGet VSIX에 대한 종속성을 선언합니다.

    ```xml
    <Reference Id="NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5" MinVersion="1.7.30402.9028">
        <Name>NuGet Package Manager</Name>
        <MoreInfoUrl>http://docs.microsoft.com/nuget/</MoreInfoUrl>
    </Reference>
    <!-- ... -->
    ```

1. 프로젝트/항목 템플릿을 만들 때 저장하도록 `.vstemplate` 파일에서 [`<PromptForSaveOnCreation>`](http://msdn.microsoft.com/library/twfxayz5.aspx)을 설정해야 합니다.

1. `packages.config` 또는 `project.json` 파일을 템플릿에 포함하지 않고, NuGet 패키지를 설치할 때 추가될 참조 또는 내용을 포함하지 않습니다.
