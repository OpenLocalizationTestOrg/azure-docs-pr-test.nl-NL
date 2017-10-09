---
title: aaaHow tooperform een onderzoek toegang | Microsoft Docs
description: Meer informatie over hoe tooperform een beoordeling met Azure Privileged Identity Management-toepassing hello.
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 49ee2feb-7d2e-4acf-82c1-40ff23062862
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 301a5e9f97b68fedfbf4954e0bd7dadb7f0fc510
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="80429-103">Hoe tooperform een toegang controleren in Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="80429-103">How tooperform an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="80429-104">Azure Active Directory (AD) Privileged Identity Management vereenvoudigt de manier waarop bedrijven beheert tooresources bevoorrechte toegang in Azure AD en andere Microsoft online services zoals Office 365 of Microsoft Intune.</span><span class="sxs-lookup"><span data-stu-id="80429-104">Azure Active Directory (AD) Privileged Identity Management simplifies how enterprises manage privileged access tooresources in Azure AD and other Microsoft online services like Office 365 or Microsoft Intune.</span></span>  

<span data-ttu-id="80429-105">Als u tooan beheerdersrol is toegewezen, beheerder met bevoorrechte rol van uw organisatie kan u vragen tooregularly bevestigen dat u moet nog steeds die rol voor uw project.</span><span class="sxs-lookup"><span data-stu-id="80429-105">If you are assigned tooan administrative role, your organization's privileged role administrator may ask you tooregularly confirm that you still need that role for your job.</span></span> <span data-ttu-id="80429-106">Krijgt u mogelijk een e-mailbericht een koppeling bevat of gaat u rechte toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="80429-106">You might get an email that includes a link, or you can go straight toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="80429-107">Hallo stappen in dit artikel tooperform een zelf controleren van de toegewezen rollen.</span><span class="sxs-lookup"><span data-stu-id="80429-107">Follow hello steps in this article tooperform a self-review of your assigned roles.</span></span>

<span data-ttu-id="80429-108">Als u een beheerder met bevoorrechte rol geïnteresseerd in toegang revisies, vraag meer details op [hoe toostart een toegang controleren](active-directory-privileged-identity-management-how-to-start-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="80429-108">If you're a privileged role administrator interested in access reviews, get more details at [How toostart an access review](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span>

## <a name="add-hello-privileged-identity-management-application"></a><span data-ttu-id="80429-109">Hallo Privileged Identity Management-toepassing toevoegen</span><span class="sxs-lookup"><span data-stu-id="80429-109">Add hello Privileged Identity Management application</span></span>
<span data-ttu-id="80429-110">U kunt hello Azure AD Privileged Identity Management (PIM)-toepassing hello [Azure-portal](https://portal.azure.com/) tooperform gecontroleerd.</span><span class="sxs-lookup"><span data-stu-id="80429-110">You can use hello Azure AD Privileged Identity Management (PIM) application in hello [Azure portal](https://portal.azure.com/) tooperform your review.</span></span>  <span data-ttu-id="80429-111">Als u geen hello Azure AD Privileged Identity Management-toepassing op uw portal hebt, volgt u deze stappen tooget gestart.</span><span class="sxs-lookup"><span data-stu-id="80429-111">If you don't have hello Azure AD Privileged Identity Management application on your portal, follow these steps tooget started.</span></span>

1. <span data-ttu-id="80429-112">Meld u aan toohello [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="80429-112">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="80429-113">Selecteer uw gebruikersnaam in Hallo rechterbovenhoek van hello Azure-portal en selecteer Hallo directory waar wilt u werkt.</span><span class="sxs-lookup"><span data-stu-id="80429-113">Select your username in hello upper right-hand corner of hello Azure portal, and select hello directory where you will you be operating.</span></span>
3. <span data-ttu-id="80429-114">Selecteer **meer services** en gebruik Hallo Filter textbox toosearch voor **Azure AD Privileged Identity Management**.</span><span class="sxs-lookup"><span data-stu-id="80429-114">Select **More services** and use hello Filter textbox toosearch for **Azure AD Privileged Identity Management**.</span></span>
4. <span data-ttu-id="80429-115">Controleer **pincode toodashboard** en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="80429-115">Check **Pin toodashboard** and then click **Create**.</span></span> <span data-ttu-id="80429-116">Hallo Privileged Identity Management-toepassing wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="80429-116">hello Privileged Identity Management application will open.</span></span>

## <a name="approve-or-deny-access"></a><span data-ttu-id="80429-117">Goedkeuren of weigeren van toegang</span><span class="sxs-lookup"><span data-stu-id="80429-117">Approve or deny access</span></span>
<span data-ttu-id="80429-118">Wanneer u goedkeuren of weigeren van toegang, hebt u zojuist vertellen Hallo revisor of u deze rol of niet.</span><span class="sxs-lookup"><span data-stu-id="80429-118">When you approve or deny access, you're just telling hello reviewer whether you still use this role or not.</span></span> <span data-ttu-id="80429-119">Kies **goedkeuren** als u wilt dat toostay in Hallo-rol of **weigeren** als u niet nodig Hallo toegang meer.</span><span class="sxs-lookup"><span data-stu-id="80429-119">Choose **Approve** if you want toostay in hello role, or **Deny** if you don't need hello access anymore.</span></span> <span data-ttu-id="80429-120">De status niet meteen, gewijzigd totdat Hallo revisor is van toepassing hello resultaten.</span><span class="sxs-lookup"><span data-stu-id="80429-120">Your status won't change right away, until hello reviewer applies hello results.</span></span>
<span data-ttu-id="80429-121">Volg deze stappen toofind en Hallo toegang beoordeling voltooien:</span><span class="sxs-lookup"><span data-stu-id="80429-121">Follow these steps toofind and complete hello access review:</span></span>

1. <span data-ttu-id="80429-122">Selecteer in de PIM-toepassing hello, **revisie bevoegde toegang**.</span><span class="sxs-lookup"><span data-stu-id="80429-122">In hello PIM application, select **Review privileged access**.</span></span> <span data-ttu-id="80429-123">Als u geen beoordelingen die in behandeling toegang hebt, weergegeven deze in hello dat Azure AD Access blade beoordeelt.</span><span class="sxs-lookup"><span data-stu-id="80429-123">If you have any pending access reviews, they appear in hello Azure AD Access reviews blade.</span></span>
2. <span data-ttu-id="80429-124">Selecteer Hallo revisie gewenste toocomplete.</span><span class="sxs-lookup"><span data-stu-id="80429-124">Select hello review you want toocomplete.</span></span>
3. <span data-ttu-id="80429-125">Tenzij u Hallo revisie hebt gemaakt, weergegeven als alleen de gebruiker gecontroleerd Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="80429-125">Unless you created hello review, you appear as hello only user in hello review.</span></span> <span data-ttu-id="80429-126">Selecteer Hallo vinkje volgende tooyour naam.</span><span class="sxs-lookup"><span data-stu-id="80429-126">Select hello check mark next tooyour name.</span></span>
4. <span data-ttu-id="80429-127">Kies een **goedkeuren** of **weigeren**.</span><span class="sxs-lookup"><span data-stu-id="80429-127">Choose either **Approve** or **Deny**.</span></span> <span data-ttu-id="80429-128">Mogelijk moet u een reden voor uw beslissing in Hallo tooinclude **een reden opgeven** in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="80429-128">You may need tooinclude a reason for your decision in hello **Provide a reason** text box.</span></span>  
5. <span data-ttu-id="80429-129">Sluit Hallo **revisie Azure AD-rollen** blade.</span><span class="sxs-lookup"><span data-stu-id="80429-129">Close hello **Review Azure AD roles** blade.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="80429-130">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="80429-130">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
