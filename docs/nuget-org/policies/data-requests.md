---
title: 사용자 데이터 요청
description: 사용자 데이터 내보내기 및 삭제 요청에 대한 정책
author: karann-msft
ms.author: karann
ms.date: 05/01/2018
ms.topic: conceptual
ms.openlocfilehash: ef054f741755bccf56eedfd462915b8e9fd6931a
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/07/2020
ms.locfileid: "67426988"
---
# <a name="user-data-requests"></a><span data-ttu-id="d64fb-103">사용자 데이터 요청</span><span class="sxs-lookup"><span data-stu-id="d64fb-103">User Data Requests</span></span>

<span data-ttu-id="d64fb-104">nuget.org 사용자는 [nuget.org](https://www.nuget.org)를 통해 정보 삭제 요청 및 정보 내보내기 요청을 제출할 수 있습니다. 두 유형 모두 지원 요청의 형태로 제출되며 30일 이내에 nuget.org 관리자가 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d64fb-104">nuget.org users can submit information delete requests and information export requests through [nuget.org](https://www.nuget.org). Both types are submitted in the form of support requests and are be executed by the nuget.org administrators within 30 days.</span></span>

<span data-ttu-id="d64fb-105">다음 사용자 데이터는 nuget.org를 통해 직접 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d64fb-105">The following user data is directly accessible through nuget.org:</span></span>

* <span data-ttu-id="d64fb-106">이메일 주소, 로그인 계정, 프로필 사진 및 이메일 알림 설정과 같은 계정 관련 데이터</span><span class="sxs-lookup"><span data-stu-id="d64fb-106">Account related data such as email address, login account, profile picture, and email notification settings</span></span>
* <span data-ttu-id="d64fb-107">소유 API 키</span><span class="sxs-lookup"><span data-stu-id="d64fb-107">Owned API Keys</span></span>
* <span data-ttu-id="d64fb-108">소유 패키지 목록</span><span class="sxs-lookup"><span data-stu-id="d64fb-108">List of owned packages</span></span>

<span data-ttu-id="d64fb-109">이 데이터는 지원 요청을 통해 내보낸 데이터에 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d64fb-109">This data is not included in data exported through the support request.</span></span>

## <a name="identifying-customer-data"></a><span data-ttu-id="d64fb-110">고객 데이터 식별</span><span class="sxs-lookup"><span data-stu-id="d64fb-110">Identifying customer data</span></span>

<span data-ttu-id="d64fb-111">고객 데이터는 nuget.org 사용자 계정 이름으로 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d64fb-111">Customer data can be identified as nuget.org user account names.</span></span>

## <a name="deleting-customer-data"></a><span data-ttu-id="d64fb-112">고객 데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="d64fb-112">Deleting customer data</span></span>

<span data-ttu-id="d64fb-113">nuget.org에서 사용자 데이터 삭제를 요청하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d64fb-113">To request deleting user data from nuget.org:</span></span>

1. <span data-ttu-id="d64fb-114">사용자가 [nuget.org](https://www.nuget.org)에 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d64fb-114">The user must sign-in to [nuget.org](https://www.nuget.org)</span></span>
1. <span data-ttu-id="d64fb-115">사용자가 [nuget.org/account/delete](https://www.nuget.org/account/delete)에서 삭제할 해당 계정에 대한 요청을 제출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d64fb-115">The user must submit a request for their account to be deleted [nuget.org/account/delete](https://www.nuget.org/account/delete)</span></span>

<span data-ttu-id="d64fb-116">패키지의 유일한 소유자인 사용자는 자신의 계정 삭제를 요청하기 전에 새 소유자를 찾는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d64fb-116">Users that are sole owners of packages are encouraged to find new owners before asking to have their account deleted.</span></span> <span data-ttu-id="d64fb-117">패키지 소유권이 전송되지 않으면 NuGet 패키지가 삭제되어 결과적으로 Visual Studio 또는 nuget.org 웹 사이트에서 검색 쿼리에 사용할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d64fb-117">If package ownership is not transferred, the NuGet package is unlisted and, as a result, it is no longer available in search queries in Visual Studio or on the nuget.org website.</span></span> <span data-ttu-id="d64fb-118">계정을 삭제하기 전에 nuget.org 관리자는 사용자와 함께 소유한 패키지에 대한 새 소유자를 찾는 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d64fb-118">Before deleting the account, the nuget.org administrators work with the user to find new owners for the packages they own.</span></span>

<span data-ttu-id="d64fb-119">계정 삭제 작업은 요청한 날짜로부터 30일 안에 nuget.org 관리자가 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="d64fb-119">The account delete action is completed by the nuget.org administrator within 30 days from the date of the request.</span></span>

<span data-ttu-id="d64fb-120">계정 삭제 시 사용자의 모든 데이터가 nuget.org 시스템에서 제거되고 다음 동작이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="d64fb-120">Upon account deletion, all of the user's data is be removed from the nuget.org system and the following actions are taken:</span></span>

* <span data-ttu-id="d64fb-121">삭제된 계정이 nuget.org에서 등록 취소됨</span><span class="sxs-lookup"><span data-stu-id="d64fb-121">The deleted account becomes unregistered with nuget.org</span></span>
* <span data-ttu-id="d64fb-122">모든 소유 API 키가 삭제됨</span><span class="sxs-lookup"><span data-stu-id="d64fb-122">All owned API Keys are deleted</span></span>
* <span data-ttu-id="d64fb-123">모든 예약된 네임스페이스가 릴리스됨</span><span class="sxs-lookup"><span data-stu-id="d64fb-123">All reserved namespaces are released</span></span>
* <span data-ttu-id="d64fb-124">모든 패키지 소유권이 제거됨</span><span class="sxs-lookup"><span data-stu-id="d64fb-124">Any package ownership are removed</span></span>

<span data-ttu-id="d64fb-125">소유된 패키지는 삭제되지 *않습니다*.</span><span class="sxs-lookup"><span data-stu-id="d64fb-125">The owned packages are *not* deleted.</span></span> <span data-ttu-id="d64fb-126">검색 결과에 나열되지 않은 경우라도 이에 종속된 프로젝트로의 패키지 복원을 통해 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d64fb-126">Though unlisted from search results, they remain available through package restore to projects that depend on them.</span></span>

## <a name="exporting-customer-data"></a><span data-ttu-id="d64fb-127">고객 데이터 내보내기</span><span class="sxs-lookup"><span data-stu-id="d64fb-127">Exporting customer data</span></span>

<span data-ttu-id="d64fb-128">nuget.org에 로그인한 후 사용자는 [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact)를 통해 내보내기 요청을 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d64fb-128">After sign-in to nuget.org, a user can submit an export request through [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact)</span></span>

<span data-ttu-id="d64fb-129">내보낸 데이터는 사용자가 48시간 동안 Azure Blob을 통해 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d64fb-129">The data exported is made available for 48 hours to the user for download through an Azure Blob.</span></span> <span data-ttu-id="d64fb-130">48시간 후에는 액세스가 만료되고 사용자는 필요에 따라 새 내보내기 요청을 제출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d64fb-130">After 48 hours, access expires and the user must submit a new export request as needed.</span></span>

<span data-ttu-id="d64fb-131">내보낸 데이터에는 다음 항목이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d64fb-131">The exported data includes:</span></span>

* <span data-ttu-id="d64fb-132">사용자의 지원 요청</span><span class="sxs-lookup"><span data-stu-id="d64fb-132">The user's support requests</span></span>
* <span data-ttu-id="d64fb-133">감사 로그에 유지된 사용자의 작업(패키지 게시, 계정 만들기)</span><span class="sxs-lookup"><span data-stu-id="d64fb-133">The user's actions (publish package, create account) as persisted in the audit logs</span></span>
* <span data-ttu-id="d64fb-134">IIS 로그에 유지된 사용자 정보</span><span class="sxs-lookup"><span data-stu-id="d64fb-134">Any user information as persisted in the IIS logs</span></span>
