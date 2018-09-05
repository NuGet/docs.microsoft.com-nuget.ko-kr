---
title: NuGet CLI 긴 경로 지원
description: Nuget.exe 긴 경로 지원에 대 한 참조
author: zhili1208
ms.author: lzhi
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 7cd387e3eb05d149da9a88cc1c76dc08588d04b5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547828"
---
# <a name="long-path-support-nuget-cli"></a><span data-ttu-id="be1ce-103">긴 경로 지원 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="be1ce-103">Long Path Support (NuGet CLI)</span></span>

<span data-ttu-id="be1ce-104">**적용 대상:** 모든 &bullet; **지원 되는 버전:** 4.8 이상</span><span class="sxs-lookup"><span data-stu-id="be1ce-104">**Applies to:** all &bullet; **Supported versions:** 4.8+</span></span>

<span data-ttu-id="be1ce-105">팩, 복원, 설치 및 파일 경로 해야 하는 대부분의 시나리오를 같은 파일에 대 한 NuGet.exe 4.8 이상을 지원 긴 경로 및 시나리오에 대 한 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="be1ce-105">NuGet.exe 4.8 and later support long paths for files and directories for scenarios like Pack, Restore, Install, and most other scenarios that need file paths.</span></span>

## <a name="required-operating-system"></a><span data-ttu-id="be1ce-106">필수 운영 체제</span><span class="sxs-lookup"><span data-stu-id="be1ce-106">Required Operating System</span></span>

-   <span data-ttu-id="be1ce-107">Windows 10 (버전 1607 이상)</span><span class="sxs-lookup"><span data-stu-id="be1ce-107">Windows 10 (version 1607 or later)</span></span>
-   <span data-ttu-id="be1ce-108">Windows 10 (2015 년 7 월 릴리스 또는 버전 1511).NET Framework 버전 4.6.2로 업그레이드 하는 경우 이상.</span><span class="sxs-lookup"><span data-stu-id="be1ce-108">Windows 10 (July 2015 release or version 1511) if you upgrade .NET Framework to versions 4.6.2 or later.</span></span>
-   <span data-ttu-id="be1ce-109">Windows Server 2016 (모든 버전)</span><span class="sxs-lookup"><span data-stu-id="be1ce-109">Windows Server 2016 (all versions)</span></span>

## <a name="enable-win32-long-paths-group-policy"></a><span data-ttu-id="be1ce-110">"Win32 긴 경로" 그룹 정책을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="be1ce-110">Enable "Win32 Long Paths" Group Policy</span></span>

<span data-ttu-id="be1ce-111">그룹 정책을 설정 하 여 해당 시스템에 긴 경로 지원을 사용 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="be1ce-111">One needs to enable long path support on those systems by setting a group policy.</span></span>

<span data-ttu-id="be1ce-112">단계:</span><span class="sxs-lookup"><span data-stu-id="be1ce-112">Steps:</span></span>
1. <span data-ttu-id="be1ce-113">시작할 **그룹 정책 편집기** -시작 검색 표시줄에서 "그룹 정책 편집"을 입력 하거나 실행 명령 (Windows-R)에서 "gpedit.msc"를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="be1ce-113">Launch **Group Policy Editor** - Type "Edit group policy" in the Start search bar or Run "gpedit.msc" from the Run command (Windows-R).</span></span>
2. <span data-ttu-id="be1ce-114">에 **로컬 그룹 정책 편집기**, 사용 "로컬 컴퓨터 정책/컴퓨터 구성/관리 템플릿/모든 책갈피 사용 설정/Win32 긴 경로"입니다.</span><span class="sxs-lookup"><span data-stu-id="be1ce-114">In the **Local Group Policy Editor**, enable "Local Computer Policy/Computer Configuration/Administrative Templates/All Settings/Enable Win32 long paths".</span></span>

![긴 경로 정책](media/LongPathPolicy.png)


> [!Note]
> <span data-ttu-id="be1ce-116">긴 경로 지원 하기 위해 다른 NuGet 도구를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="be1ce-116">Enabling Other NuGet Tools to Support Long Paths</span></span>
>
> -   <span data-ttu-id="be1ce-117">Dotnet CLI 버전 또는 운영 체제에 관계 없이 긴 경로 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="be1ce-117">Dotnet CLI supports long paths regardless of the operating system or version.</span></span>
> -   <span data-ttu-id="be1ce-118">Visual Studio 또는 msbuild /t: restore가 긴 경로 아직 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="be1ce-118">Visual Studio or msbuild /t:restore does not yet support long paths.</span></span>
> -   <span data-ttu-id="be1ce-119">NuGet 라이브러리를 사용 하 여 복원 및 다른 명령을 실행 하는 소프트웨어는 지원 긴 경로 동일한 시스템에서 NuGet.exe에서 작동 하는 설정 하는 경우 창에 longPathAware 매니페스트 하 고 UseLegacyPathHandling App.Config통해false로구성[ 자세한 내용은 참조 하세요.](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)</span><span class="sxs-lookup"><span data-stu-id="be1ce-119">Software that uses NuGet Libraries to execute restore and other commands, will support long paths on the same systems that NuGet.exe works on, if they also set longPathAware in their windows manifest and configure UseLegacyPathHandling to false via App.Config [See more information](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)</span></span>

