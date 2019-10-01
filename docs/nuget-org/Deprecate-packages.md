---
title: nuget.org의 패키지 사용 중단
description: 패키지 사용 중단 프로세스 및 클라이언트에서 이 정보를 표시하는 방법에 대한 자세한 설명
author: anangaur
ms.author: anangaur
ms.date: 09/23/2019
ms.topic: conceptual
ms.reviewer: karann-msft
ms.openlocfilehash: 120b463fda856fe9dd407b6eba32d60e0918f763
ms.sourcegitcommit: 188ade66b7ac807ba1667c77cfb9325bf89a8a4a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71248884"
---
# <a name="deprecating-packages"></a><span data-ttu-id="d0614-103">패키지 사용 중단</span><span class="sxs-lookup"><span data-stu-id="d0614-103">Deprecating packages</span></span>

<span data-ttu-id="d0614-104">더 이상 패키지를 유지 관리하지 않거나 패키지 소비자에게 다른 패키지로 이동하도록 권장하려는 경우 패키지를 사용 중단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0614-104">You can deprecate a package if you no longer maintain a package or if would like to encourage your package's consumers to move to another package.</span></span> 

<span data-ttu-id="d0614-105">패키지 사용 중단은 아래 설명대로 패키지를 **제외**하는 것과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="d0614-105">Package deprecation is different than **unlisting** your package as explained below:</span></span>
* <span data-ttu-id="d0614-106">패키지를 **제외**하면 패키지는 검색 결과에서 숨겨지므로 검색되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d0614-106">**Unlisting** a package prevents its discovery because it is hidden in search results.</span></span> 
* <span data-ttu-id="d0614-107">패키지를 **사용 중단**하면 기존 소비자는 패키지가 설치되어 있는지 또는 프로젝트에 사용되고 있는지 여부를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0614-107">**Deprecating** a package lets your package's existing consumers find out if they have it installed or used in their projects.</span></span> <span data-ttu-id="d0614-108">또한 사용 중단 이유 및 패키지 게시자가 지정한 대체 권장 패키지를 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0614-108">It also lets them know the reason for deprecation and an alternate recommended package as specified by you (the package publisher).</span></span> <span data-ttu-id="d0614-109">패키지를 사용 중단하는 것은 패키지를 제외하는 것이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="d0614-109">Deprecating a package does not unlist the package.</span></span> 

<span data-ttu-id="d0614-110">게시자는 패키지 제외와 사용 중단을 둘 다 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0614-110">As a publisher, you may choose to both unlist as well as deprecate packages.</span></span>

## <a name="deprecation-workflow"></a><span data-ttu-id="d0614-111">사용 중단 워크플로</span><span class="sxs-lookup"><span data-stu-id="d0614-111">Deprecation workflow</span></span>
1. <span data-ttu-id="d0614-112">패키지를 사용 중단하려면 **패키지 관리**로 이동하여 **사용 중단**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d0614-112">To deprecate a package, go to **Manage packages** and select **Deprecation**:</span></span>

    ![패키지 사용 중단 옵션으로 이동](media/deprecation-select-option.png)

2. <span data-ttu-id="d0614-114">사용 중단할 버전을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d0614-114">Select the version you would like to deprecate.</span></span> <span data-ttu-id="d0614-115">모든 버전을 사용 중단하려면 **모든 버전 선택** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d0614-115">If you want to deprecate all version, choose **Select all versions** option.</span></span>

    ![사용 중단할 패키지 버전 선택](media/deprecation-select-version.png)

3. <span data-ttu-id="d0614-117">사용 중단 이유를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d0614-117">Choose a reason for deprecation.</span></span> <span data-ttu-id="d0614-118">패키지가 더 이상 유지 관리되지 않으면 **레거시** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d0614-118">If the package is no longer maintained, choose the **Legacy** option.</span></span> <span data-ttu-id="d0614-119">특정 버전에 중요한 버그가 있는 경우 **중요한 버그 있음** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d0614-119">If the specific version has a critical bug, choose the **has critical bugs** option.</span></span> <span data-ttu-id="d0614-120">다른 이유인 경우에는 **기타**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d0614-120">For any other reason, select **Other**.</span></span> <span data-ttu-id="d0614-121">언제든지 대체 권장 패키지(및 버전) 및 소유자에 대한 사용자 지정 메시지를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0614-121">You can always specify an alternate recommended package (and version) and a custom message to the owners.</span></span> 

    ![대체 패키지 권장 사항 및 사용자 지정 메시지를 선택합니다.](media/deprecation-save.png)

> [!Note]
> <span data-ttu-id="d0614-123">사용자 지정 메시지는 nuget.org에만 표시되고 클라이언트에서는 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d0614-123">Custom message is only shown on nuget.org but not from the clients.</span></span> <span data-ttu-id="d0614-124">현재 `dotnet.exe` 및 NuGet 패키지 관리자와 같은 클라이언트는 사용자 지정 메시지를 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d0614-124">Currently, clients such as `dotnet.exe` and the NuGet Package Manager do not show the custom message.</span></span>

## <a name="client-experience-for-deprecated-packages"></a><span data-ttu-id="d0614-125">사용 중단된 패키지에 대한 클라이언트 환경</span><span class="sxs-lookup"><span data-stu-id="d0614-125">Client experience for deprecated packages</span></span>
<span data-ttu-id="d0614-126">패키지가 사용 중단된 경우 해당 고객에게는 사용된 클라이언트에 따라 다음과 같은 방법으로 이에 대한 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0614-126">Once a package has been deprecated, its consumers are notified about it in the following ways (depending upon the client used).</span></span>

### <a name="visual-studio"></a><span data-ttu-id="d0614-127">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d0614-127">Visual Studio</span></span> 
<span data-ttu-id="d0614-128">*Visual Studio 2019 버전 16.3부터 사용 가능*</span><span class="sxs-lookup"><span data-stu-id="d0614-128">*Available starting in Visual Studio 2019 version 16.3*</span></span>

<span data-ttu-id="d0614-129">Visual Studio는 `Installed` 탭에서 사용되지 않는 패키지의 사용에 대한 경고를 표시합니다. 패키지와 사용 중단 정보(사용되지 않는 이유 및 대신 사용할 대체 패키지가 있는 경우 포함)로 안내됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0614-129">Visual Studio warns about a deprecated package's usage on the `Installed` tab.It will lead you to the package and its deprecation information (including the reason it was deprecated and the alternate package to use instead, if present).</span></span>

   ![패키지 관리자의 Visual Studio 설치 탭에서 사용되지 않는 패키지](media/deprecation-vs.png)

### <a name="dotnetexe"></a><span data-ttu-id="d0614-131">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="d0614-131">dotnet.exe</span></span>
<span data-ttu-id="d0614-132">*.NET SDK 3.0부터 사용 가능*</span><span class="sxs-lookup"><span data-stu-id="d0614-132">*Available starting with .NET SDK 3.0*</span></span>

<span data-ttu-id="d0614-133">dotnet.exe를 사용하는 경우 솔루션 또는 프로젝트 폴더에 대해 `dotnet list package --deprecated` 명령을 실행하여 사용 중단 정보와 함께 사용되지 않는 패키지의 목록을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0614-133">If you use dotnet.exe, you can run the command `dotnet list package --deprecated` on the solution or project folder to get a list of deprecated packages along with the deprecation information:</span></span>

```
> dotnet list package --deprecated

The following sources were used:
   https://api.nuget.org/v3/index.json

Project `My.Test.Project` has the following deprecated packages
   [netcoreapp3.0]:
   Top-level Package      Resolved   Reason(s)   Alternative
   > My.Sample.Lib        6.0.0      Legacy      My.Awesome.Package

```
