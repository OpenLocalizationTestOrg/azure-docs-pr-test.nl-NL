---
title: Licenties toewijzen voor Azure MFA | Microsoft Docs
description: Informatie over hoe u licenties toewijst voor Microsoft Azure Multi-Factor Authentication.
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 514ef423-8ee6-4987-8a4e-80d5dc394cf9
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/13/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ROBOTS: NOINDEX
ms.openlocfilehash: 45522bf526c4aeab1d6ccc8891a55a0436ff9320
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="assigning-an-azure-mfa-azure-ad-premium-or-enterprise-mobility-license-to-users"></a><span data-ttu-id="878fe-103">Een licentie voor Azure MFA, Azure AD Premium of Enterprise Mobility aan gebruikers toewijzen</span><span class="sxs-lookup"><span data-stu-id="878fe-103">Assigning an Azure MFA, Azure AD Premium, or Enterprise Mobility license to users</span></span>
<span data-ttu-id="878fe-104">Als u Azure MFA, Azure AD Premium of Enterprise Mobility Suite licenties hebt aangeschaft, hoeft u geen Multi-Factor Authentication-provider te maken.</span><span class="sxs-lookup"><span data-stu-id="878fe-104">If you have purchased Azure MFA, Azure AD Premium, or Enterprise Mobility Suite licenses, you do not need to create a Multi-Factor Auth provider.</span></span> <span data-ttu-id="878fe-105">Zodra u de licenties aan uw gebruikers hebt toegewezen, kunt u beginnen MFA voor ze in te schakelen.</span><span class="sxs-lookup"><span data-stu-id="878fe-105">Once you assign the licenses to your users, you can begin enabling them for MFA.</span></span>

## <a name="to-assign-a-license"></a><span data-ttu-id="878fe-106">Een licentie toewijzen</span><span class="sxs-lookup"><span data-stu-id="878fe-106">To assign a license</span></span>
1. <span data-ttu-id="878fe-107">Meld u aan als beheerder bij de [klassieke Azure Portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="878fe-107">Sign in to the [Azure classic portal](https://manage.windowsazure.com) as an administrator.</span></span>
2. <span data-ttu-id="878fe-108">Selecteer aan de linkerkant **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="878fe-108">On the left, select **Active Directory**.</span></span>
3. <span data-ttu-id="878fe-109">Dubbelklik vanuit de pagina Active Directory op de adreslijst met de gebruikers die u wilt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="878fe-109">On the Active Directory page, double-click the directory that has the users you wish to enable.</span></span>
4. <span data-ttu-id="878fe-110">Selecteer boven aan de pagina met de adreslijst **Licenties**.</span><span class="sxs-lookup"><span data-stu-id="878fe-110">At the top of the directory page, select **Licenses**.</span></span>
   <span data-ttu-id="878fe-111">![Licenties toewijzen](./media/multi-factor-authentication-get-started-assign-licenses/assign1.png)</span><span class="sxs-lookup"><span data-stu-id="878fe-111">![Assign Licenses](./media/multi-factor-authentication-get-started-assign-licenses/assign1.png)</span></span>
5. <span data-ttu-id="878fe-112">Selecteer op de pagina Licenties **Azure Multi-Factor Authentication**, **Active Directory Premium** of **Enterprise Mobility Suite**.</span><span class="sxs-lookup"><span data-stu-id="878fe-112">On the Licenses page, select **Azure Multi-Factor Authentication**, **Active Directory Premium**, or **Enterprise Mobility Suite**.</span></span>  <span data-ttu-id="878fe-113">Als u er slechts één hebt, zou deze automatisch geselecteerd moeten zijn.</span><span class="sxs-lookup"><span data-stu-id="878fe-113">If you only have one, then it should be selected automatically.</span></span>
6. <span data-ttu-id="878fe-114">Klik onder aan de pagina op **Toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="878fe-114">At the bottom of the page, click **Assign**.</span></span>
   <span data-ttu-id="878fe-115">![Licenties toewijzen](./media/multi-factor-authentication-get-started-assign-licenses/assign3.png)</span><span class="sxs-lookup"><span data-stu-id="878fe-115">![Assign Licenses](./media/multi-factor-authentication-get-started-assign-licenses/assign3.png)</span></span>
7. <span data-ttu-id="878fe-116">In het vak dat wordt weergegeven, klikt u naast de gebruikers of groepen aan wie u licenties wilt toewijzen.</span><span class="sxs-lookup"><span data-stu-id="878fe-116">In the box that comes up, click next to the users or groups you want to assign licenses to.</span></span>  <span data-ttu-id="878fe-117">Er zou een groen vinkje moeten worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="878fe-117">You should see a green check mark appear.</span></span>
8. <span data-ttu-id="878fe-118">Klik op het pictogram met het vinkje om de wijzigingen op te slaan.</span><span class="sxs-lookup"><span data-stu-id="878fe-118">Click the check mark icon to save the changes.</span></span>
   <span data-ttu-id="878fe-119">![Licenties toewijzen](./media/multi-factor-authentication-get-started-assign-licenses/assign4.png)</span><span class="sxs-lookup"><span data-stu-id="878fe-119">![Assign Licenses](./media/multi-factor-authentication-get-started-assign-licenses/assign4.png)</span></span>
9. <span data-ttu-id="878fe-120">U zou een bericht moeten zien dat vermeldt hoeveel licenties er zijn toegewezen en voor hoeveel dat is mislukt.</span><span class="sxs-lookup"><span data-stu-id="878fe-120">You should see a message saying how many licenses were assigned and how many may have failed.</span></span>  <span data-ttu-id="878fe-121">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="878fe-121">Click **Ok**.</span></span>
   <span data-ttu-id="878fe-122">![Licenties toewijzen](./media/multi-factor-authentication-get-started-assign-licenses/assign5.png)</span><span class="sxs-lookup"><span data-stu-id="878fe-122">![Assign Licenses](./media/multi-factor-authentication-get-started-assign-licenses/assign5.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="878fe-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="878fe-123">Next steps</span></span>

- <span data-ttu-id="878fe-124">Zie [What is Microsoft Azure Active Directory licensing?](../active-directory/active-directory-licensing-what-is.md) (Wat is licentieverlening voor Microsoft Azure Active Directory?) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="878fe-124">For more information, see [What is Microsoft Azure Active Directory licensing?](../active-directory/active-directory-licensing-what-is.md)</span></span>
