---
title: 개별 계정
description: 패키지를 게시하려면 NuGet.org의 개별 계정이 필요합니다.
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: e1e31e0534706dab43f8d7b1b0db059cd6f29b80
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427138"
---
# <a name="individual-accounts"></a><span data-ttu-id="fd684-103">개별 계정</span><span class="sxs-lookup"><span data-stu-id="fd684-103">Individual accounts</span></span>

<span data-ttu-id="fd684-104">NuGet.org에서 패키지를 게시하고 관리하려면 개별 계정을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd684-104">You must create an individual account to publish and manage packages on NuGet.org.</span></span>

## <a name="individual-accounts-vs-organization-accounts"></a><span data-ttu-id="fd684-105">개별 계정 및 조직 계정</span><span class="sxs-lookup"><span data-stu-id="fd684-105">Individual accounts vs. organization accounts</span></span>

<span data-ttu-id="fd684-106">개별(사용자) 계정은 NuGet.org에서 사용자의 ID이며, 여러 조직의 멤버가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd684-106">Your individual (user) account is your identity on NuGet.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="fd684-107">패키지는 개별 계정에 속할 수 있는 것처럼 조직 계정에 속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd684-107">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="fd684-108">패키지 소비자는 개별 계정 또는 조직 계정 간의 차이를 보지 못합니다. 둘 다 패키지 `owners`로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="fd684-108">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

<span data-ttu-id="fd684-109">조직 계정은 구성원으로 하나 이상의 개별 계정을 가지고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd684-109">An organization account has one or more individual accounts as its members.</span></span> <span data-ttu-id="fd684-110">이러한 멤버는 소유권에 대한 단일 ID를 유지 관리하면서 패키지 세트를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd684-110">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

## <a name="add-a-new-individual-account"></a><span data-ttu-id="fd684-111">새 개별 계정 추가</span><span class="sxs-lookup"><span data-stu-id="fd684-111">Add a new individual account</span></span>

<span data-ttu-id="fd684-112">NuGet.org 계정을 만들려면 개인 MSA(Microsoft 계정) 또는 AAD(Azure Active Directory) 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd684-112">To create a NuGet.org account, you need to have a personal Microsoft account (MSA) or an Azure Active Directory (AAD) account.</span></span> <span data-ttu-id="fd684-113">없는 경우 계정을 [만들](https://signup.live.com) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd684-113">If you do not have one, you can [create](https://signup.live.com) one.</span></span> <span data-ttu-id="fd684-114">MSA 또는 AAD 계정이 있는 경우 다음 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="fd684-114">Follow the following steps if you have an MSA or AAD account.</span></span>

1. <span data-ttu-id="fd684-115">[NuGet.org 로그인 페이지](https://www.nuget.org/users/account/LogOn)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="fd684-115">Go to the [NuGet.org login page](https://www.nuget.org/users/account/LogOn).</span></span>

1. <span data-ttu-id="fd684-116">**Microsoft로 로그인** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fd684-116">Click on **Sign in with Microsoft** button.</span></span>

1. <span data-ttu-id="fd684-117">Microsoft 계정 또는 Azure Active Directory 계정 세부 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fd684-117">Enter your Microsoft account or Azure Active Directory account details.</span></span>

1. <span data-ttu-id="fd684-118">**예**를 클릭하여 *NuGet.org* 애플리케이션에 지정된 사용 권한을 수락하세요.</span><span class="sxs-lookup"><span data-stu-id="fd684-118">Please click **Yes** to accept the permissions to be given to the *NuGet.org* application.</span></span>

   ![NuGet.org에 사용 권한 부여](media/nuget-org-permissions.png)

1. <span data-ttu-id="fd684-120">*nuget.org*로 리디렉션되고 사용자 이름을 등록하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd684-120">You will be redirected to *nuget.org*, and asked to register a username.</span></span>

1. <span data-ttu-id="fd684-121">입력 상자에서 사용자 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fd684-121">Specify the username in the input box.</span></span> <span data-ttu-id="fd684-122">사용자 이름은 대/소문자를 구분**하며** 나중에 변경하거나 이름을 바꿀 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fd684-122">Please note that the username **is** case sensitive and cannot be changed or renamed later.</span></span>

   ![NuGet.org에서 사용자 이름 지정](media/nuget-org-register.png) 

1. <span data-ttu-id="fd684-124">**등록** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fd684-124">Click the **Register** button.</span></span>

<span data-ttu-id="fd684-125">이제 NuGet.org 계정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd684-125">You now have a NuGet.org account.</span></span> <span data-ttu-id="fd684-126">[계정 설정](https://www.nuget.org/account) 페이지에서 계정 관리를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd684-126">You can perform account management on the [account settings](https://www.nuget.org/account) page.</span></span>
