---
title: 개별 계정 - NuGet.org
description: 패키지를 게시하려면 NuGet.org의 개별 계정이 필요합니다.
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 5224a4f5be519e1d72285562c1611d047582f7de
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901566"
---
# <a name="individual-accounts-on-nugetorg"></a><span data-ttu-id="457e1-103">NuGet.org의 개별 계정</span><span class="sxs-lookup"><span data-stu-id="457e1-103">Individual accounts on NuGet.org</span></span>

<span data-ttu-id="457e1-104">NuGet.org에서 패키지를 게시하고 관리하려면 개별 계정을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="457e1-104">You must create an individual account to publish and manage packages on NuGet.org.</span></span>

## <a name="individual-accounts-vs-organization-accounts"></a><span data-ttu-id="457e1-105">개별 계정 및 조직 계정</span><span class="sxs-lookup"><span data-stu-id="457e1-105">Individual accounts vs. organization accounts</span></span>

<span data-ttu-id="457e1-106">개별(사용자) 계정은 NuGet.org에서 사용자의 ID이며, 여러 조직의 멤버가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="457e1-106">Your individual (user) account is your identity on NuGet.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="457e1-107">패키지는 개별 계정에 속할 수 있는 것처럼 조직 계정에 속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="457e1-107">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="457e1-108">패키지 소비자는 개별 계정 또는 조직 계정 간의 차이를 보지 못합니다. 둘 다 패키지 `owners`로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="457e1-108">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

<span data-ttu-id="457e1-109">조직 계정은 구성원으로 하나 이상의 개별 계정을 가지고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="457e1-109">An organization account has one or more individual accounts as its members.</span></span> <span data-ttu-id="457e1-110">이러한 멤버는 소유권에 대한 단일 ID를 유지 관리하면서 패키지 세트를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="457e1-110">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

## <a name="add-a-new-individual-account"></a><span data-ttu-id="457e1-111">새 개별 계정 추가</span><span class="sxs-lookup"><span data-stu-id="457e1-111">Add a new individual account</span></span>

<span data-ttu-id="457e1-112">NuGet.org 계정을 만들려면 개인 MSA(Microsoft 계정) 또는 AAD(Azure Active Directory) 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="457e1-112">To create a NuGet.org account, you need to have a personal Microsoft account (MSA) or an Azure Active Directory (AAD) account.</span></span> <span data-ttu-id="457e1-113">없는 경우 계정을 [만들](https://signup.live.com) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="457e1-113">If you do not have one, you can [create](https://signup.live.com) one.</span></span> <span data-ttu-id="457e1-114">MSA 또는 AAD 계정이 있는 경우 다음 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="457e1-114">Follow the following steps if you have an MSA or AAD account.</span></span>

1. <span data-ttu-id="457e1-115">[NuGet.org 로그인 페이지](https://www.nuget.org/users/account/LogOn)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="457e1-115">Go to the [NuGet.org login page](https://www.nuget.org/users/account/LogOn).</span></span>

1. <span data-ttu-id="457e1-116">**Microsoft로 로그인** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="457e1-116">Click on **Sign in with Microsoft** button.</span></span>

1. <span data-ttu-id="457e1-117">Microsoft 계정 또는 Azure Active Directory 계정 세부 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="457e1-117">Enter your Microsoft account or Azure Active Directory account details.</span></span>

1. <span data-ttu-id="457e1-118">**예** 를 클릭하여 *NuGet.org* 애플리케이션에 지정된 사용 권한을 수락하세요.</span><span class="sxs-lookup"><span data-stu-id="457e1-118">Please click **Yes** to accept the permissions to be given to the *NuGet.org* application.</span></span>

   ![NuGet.org에 사용 권한 부여](media/nuget-org-permissions.png)

1. <span data-ttu-id="457e1-120">*nuget.org* 로 리디렉션되고 사용자 이름을 등록하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="457e1-120">You will be redirected to *nuget.org*, and asked to register a username.</span></span>

1. <span data-ttu-id="457e1-121">입력 상자에서 사용자 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="457e1-121">Specify the username in the input box.</span></span> <span data-ttu-id="457e1-122">사용자 이름은 대/소문자를 구분 **하며** 나중에 변경하거나 이름을 바꿀 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="457e1-122">Please note that the username **is** case sensitive and cannot be changed or renamed later.</span></span>

   ![NuGet.org에서 사용자 이름 지정](media/nuget-org-register.png) 

1. <span data-ttu-id="457e1-124">**등록** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="457e1-124">Click the **Register** button.</span></span>

<span data-ttu-id="457e1-125">이제 NuGet.org 계정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="457e1-125">You now have a NuGet.org account.</span></span> <span data-ttu-id="457e1-126">[계정 설정](https://www.nuget.org/account) 페이지에서 계정 관리를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="457e1-126">You can perform account management on the [account settings](https://www.nuget.org/account) page.</span></span>

## <a name="enable-two-factor-authentication-2fa"></a><span data-ttu-id="457e1-127">2FA(2단계 인증) 사용</span><span class="sxs-lookup"><span data-stu-id="457e1-127">Enable two-factor authentication (2FA)</span></span>

<span data-ttu-id="457e1-128">2FA(2단계 인증)는 웹 사이트나 앱에 로그인할 때 사용되는 추가 보안 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="457e1-128">Two-factor authentication, or 2FA, is an extra layer of security used when logging into websites or apps.</span></span> <span data-ttu-id="457e1-129">2FA를 사용하면 MSA(Microsoft 계정)로 로그인하고 사용자만 알고 있거나 액세스할 수 있는 다른 형식의 인증을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="457e1-129">With 2FA, you have to log in with your Microsoft Account (MSA) and provide another form of authentication that only you know or have access to.</span></span> <span data-ttu-id="457e1-130">계정을 더 잘 보호하려면 2단계 인증을 사용하도록 설정합니다(권장).</span><span class="sxs-lookup"><span data-stu-id="457e1-130">To better protect your account, enable two-factor authentication (recommended).</span></span>

1. <span data-ttu-id="457e1-131">계정에 로그인한 경우 프로필을 열고 **로그인 계정** 에서 **사용** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="457e1-131">When logged into your account, open your profile and choose **Enable** under **Login Account**.</span></span>

   ![2FA 사용](media/nuget-org-register-2fa.png)

   <span data-ttu-id="457e1-133">다음에 nuget.org 에 로그인 할 때 추가 자격 증명을 묻는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="457e1-133">You will see a message that tells you that the next time you sign in to *nuget.org*, you will be asked for additional credentials.</span></span>

2. <span data-ttu-id="457e1-134">지금 인증을 완료하려면 로그아웃했다가 다시 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="457e1-134">To complete the authentication at this time, sign out and then sign in again.</span></span>

3. <span data-ttu-id="457e1-135">로그인할 때 두 번째 인증 형식으로 문자 또는 메일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="457e1-135">When you sign in, choose either text or e-mail as a second form of authentication.</span></span>

   <span data-ttu-id="457e1-136">Microsoft 계정에 이미 연결되어 있는 전화 번호 또는 메일을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="457e1-136">Verify the phone number or e-mail that is already associated with your Microsoft account.</span></span> <span data-ttu-id="457e1-137">계정의 새 전화 번호 또는 메일을 입력해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="457e1-137">You may need to enter a new phone number or e-mail for your account.</span></span> <span data-ttu-id="457e1-138">필요한 경우 지침에 따라 필요한 정보를 입력하고 **다음** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="457e1-138">If so, enter the required information as instructed, and click **Next**.</span></span>

   ![2FA 사용 및 전화 입력](media/nuget-org-sign-in-2fa.png)

4. <span data-ttu-id="457e1-140">디바이스 또는 메일 계정을 확인하고 방금 받은 코드를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="457e1-140">Check your device or e-mail account, and enter the code that you were just sent.</span></span>

   ![2FA 사용 및 코드 입력](media/nuget-org-enter-code-2fa.png)

5. <span data-ttu-id="457e1-142">추가 지침에 따라 2단계 인증을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="457e1-142">Follow any additional instructions to complete Two-factor authentication.</span></span>

> [!Tip]
> <span data-ttu-id="457e1-143">NuGet.org 계정에 대해 2FA를 사용하도록 설정해도 NuGet.org에 로그인하는 데 사용하는 Microsoft 계정에 연결될 수 있는 다른 계정 또는 서비스의 인증 설정에는 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="457e1-143">Enabling 2FA for your NuGet.org account does not impact authentication settings for other accounts or services that may be linked to the Microsoft account you use to login to NuGet.org.</span></span>

## <a name="delete-a-nugetorg-account"></a><span data-ttu-id="457e1-144">NuGet.org 계정 삭제</span><span class="sxs-lookup"><span data-stu-id="457e1-144">Delete a NuGet.org account</span></span>

<span data-ttu-id="457e1-145">NuGet.org 계정 삭제처럼 추가 계정 관련 작업에 대해서는 [NuGet.org 계정 관리](nuget-org-faq.md#nugetorg-account-management)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="457e1-145">For help with additional account-related tasks, such as deleting a NuGet.org account, see [NuGet.org account management](nuget-org-faq.md#nugetorg-account-management).</span></span>
