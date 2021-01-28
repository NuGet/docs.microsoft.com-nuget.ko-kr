---
title: Visual Studio 프로젝트 시스템에 대한 NuGet 지원
description: 타사 프로젝트 형식에서 Visual Studio 프로젝트 시스템에 NuGet을 통합합니다.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2017
ms.topic: reference
ms.openlocfilehash: 7af330f88b47352666933598719d9c8f8cb66a78
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779413"
---
# <a name="nuget-support-for-the-visual-studio-project-system"></a>Visual Studio 프로젝트 시스템에 대한 NuGet 지원

Visual Studio에서 타사 프로젝트 형식을 지원하려면 NuGet 3.x 이상이 [CPS(일반 프로젝트 시스템)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md)을 지원하고 NuGet 3.2 이상이 비 CPS 프로젝트 시스템을 지원해야 합니다.

NuGet과 통합하려면 프로젝트 시스템은 이 항목에서 설명된 모든 프로젝트 기능에 대한 고유한 지원을 제공해야 합니다.

> [!Note]
> 프로젝트에서 설치할 패키지를 사용하기 위해 프로젝트에 실제로 없는 기능을 선언하지 마세요. Visual Studio 및 기타 확장명의 여러 기능은 NuGet 클라이언트 외에도 프로젝트 기능에 따라 달라집니다. 프로젝트의 기능을 거짓으로 보급하면 이러한 구성 요소에 오작동이 발생하고 사용자의 환경이 저하될 수 있습니다.

## <a name="advertise-project-capabilities"></a>프로젝트 기능 보급

NuGet 클라이언트는 다음 표에 설명된 대로 [프로젝트의 기능](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md)에 따라 프로젝트 형식과 호환 가능한 패키지를 결정합니다.

| 기능 | Description |
| --- | --- |
| AssemblyReferences | 프로젝트가 어셈블리 참조를 지원함을 나타냅니다(WinRTReferences와 구별). |
| DeclaredSourceItems | 프로젝트가 프로젝트 자체에서 소스 항목을 선언하는 (DNX가 아닌) 일반적인 MSBuild 프로젝트임을 나타냅니다. |
| UserSourceItems|사용자가 해당 프로젝트에 임의 파일을 추가할 수 있음을 나타냅니다. |

CPS 기반 프로젝트 시스템의 경우 이 섹션의 나머지 부분에서 설명한 프로젝트 기능에 대한 구현 세부 사항이 수행되었습니다. [CPS 프로젝트에서 프로젝트 기능 선언](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project)을 참조하세요.

## <a name="implementing-vsprojectcapabilitiespresencechecker"></a>VsProjectCapabilitiesPresenceChecker 구현

`VsProjectCapabilitiesPresenceChecker` 클래스는 다음과 같이 정의되는 `IVsBooleanSymbolPresenceChecker` 인터페이스를 구현해야 합니다.

```cs
public interface IVsBooleanSymbolPresenceChecker
{
    /// <summary>
    /// Checks whether the symbols defined may have changed since the last time
    /// this method was called.
    /// </summary>
    /// <param name="versionObject">
    /// The response version object assigned at the last call.
    /// May be null to get the initial version.
    /// At the conclusion of this method call, the reference may be changed so that on a subsequent call
    /// we know what version was last observed. The caller should treat this value as an opaque object,
    /// and should not assume any significance from whether the pointer changed or not.
    /// </param>
    /// <returns>
    /// <c>true</c> if the symbols defined may have changed since the last call to this method
    /// or if <paramref name="versionObject"/> was <c>null</c> upon entering this method.
    /// <c>false</c> if the responses would all be the same.
    /// </returns>
    bool HasChangedSince(ref object versionObject);

    /// <summary>
    /// Checks for the presence of a given symbol.
    /// </summary>
    /// <param name="symbol">The symbol to check for.</param>
    /// <returns><c>true</c> if the symbol is present; <c>false</c> otherwise.</returns>
    bool IsSymbolPresent(string symbol);
}
```

그런 다음 이 인터페이스의 샘플 구현은 다음과 같습니다.

```cs
class VsProjectCapabilitiesPresenceChecker : IVsBooleanSymbolPresenceChecker
{
    /// <summary>
    /// The set of capabilities this project system actually has.
    /// This should be kept current, and honestly reflect what the project can do.
    /// </summary>
    private static readonly HashSet<string> ActualProjectCapabilities = new HashSet<string>(StringComparer.OrdinalIgnoreCase)
        {
            "AssemblyReferences",
            "DeclaredSourceItems",
            "UserSourceItems",
        };

    public bool HasChangedSince(ref object versionObject)
    {
        // If your project capabilities do not change over time while the project is open,
        // you may simply `return false;` from your `HasChangedSince` method.
        return false;
    }

    public bool IsSymbolPresent(string symbol)
    {
        return ActualProjectCapabilities.Contains(symbol);
    }
}
```

프로젝트 시스템이 실제로 지원하는 기능에 따라 `ActualProjectCapabilities` 집합에서 기능을 추가/제거합니다. 자세한 설명은 [프로젝트 기능 설명서](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md)를 참조하세요.

## <a name="responding-to-queries"></a>쿼리에 응답

프로젝트는 `IVsHierarchy::GetProperty`를 통해 `VSHPROPID_ProjectCapabilitiesChecker` 속성을 지원하여 이 기능을 선언합니다. `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` 어셈블리에 정의된 `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`라는 인스턴스를 반환해야 합니다. [NuGet 패키지](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime)를 설치하여 이 어셈블리를 참조합니다.

예를 들어 다음 `case` 문을 `IVsHierarchy::GetProperty` 메서드의 `switch` 문에 추가할 수 있습니다.

```cs
case __VSHPROPID8.VSHPROPID_ProjectCapabilitiesChecker:
    propVal = new VsProjectCapabilitiesPresenceChecker();
    return VSConstants.S_OK;
```

## <a name="dte-support"></a>DTE 지원

NuGet에서는 프로젝트 시스템을 최상위 Visual Studio 자동화 인터페이스인 [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017)로 호출하여 참조, 콘텐츠 항목 및 MSBuild 가져오기를 추가하도록 합니다. DTE는 구현할 수 있는 COM 인터페이스의 집합입니다.

프로젝트 형식이 CPS에 기반하는 경우 DTE는 자동으로 구현됩니다.
