---
title: Het uitvoeren van een onderzoek toegang | Microsoft Docs
description: Informatie over het uitvoeren van een overzicht met de Azure Privileged Identity Management-toepassing.
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
ms.openlocfilehash: a98ed60221eeba1d9c92df846aeae2deafb8ae60
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-perform-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="6f5c2-103">Het uitvoeren van een onderzoek toegang in Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="6f5c2-103">How to perform an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="6f5c2-104">Azure Active Directory (AD) Privileged Identity Management vereenvoudigt de manier waarop bedrijven bevoorrechte toegang tot resources in Azure AD en andere Microsoft online services zoals Office 365 of Microsoft Intune beheert.</span><span class="sxs-lookup"><span data-stu-id="6f5c2-104">Azure Active Directory (AD) Privileged Identity Management simplifies how enterprises manage privileged access to resources in Azure AD and other Microsoft online services like Office 365 or Microsoft Intune.</span></span>  

<span data-ttu-id="6f5c2-105">Als u zijn toegewezen aan een administratieve rol, kan u regelmatig bevestigen dat u nog die rol bij uw werk moet door beheerder met bevoorrechte rol van uw organisatie vragen.</span><span class="sxs-lookup"><span data-stu-id="6f5c2-105">If you are assigned to an administrative role, your organization's privileged role administrator may ask you to regularly confirm that you still need that role for your job.</span></span> <span data-ttu-id="6f5c2-106">Krijgt u mogelijk een e-mailbericht een koppeling bevat of u kunt dan direct door naar de [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6f5c2-106">You might get an email that includes a link, or you can go straight to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="6f5c2-107">Volg de stappen in dit artikel om uit te voeren met een zelf controleren van de toegewezen rollen.</span><span class="sxs-lookup"><span data-stu-id="6f5c2-107">Follow the steps in this article to perform a self-review of your assigned roles.</span></span>

<span data-ttu-id="6f5c2-108">Als u een beheerder met bevoorrechte rol geïnteresseerd in toegang revisies, vraag meer details op [starten een onderzoek toegang](active-directory-privileged-identity-management-how-to-start-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="6f5c2-108">If you're a privileged role administrator interested in access reviews, get more details at [How to start an access review](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span>

## <a name="add-the-privileged-identity-management-application"></a><span data-ttu-id="6f5c2-109">De Privileged Identity Management-toepassing toevoegen</span><span class="sxs-lookup"><span data-stu-id="6f5c2-109">Add the Privileged Identity Management application</span></span>
<span data-ttu-id="6f5c2-110">U kunt de toepassing Azure AD Privileged Identity Management (PIM) in de [Azure-portal](https://portal.azure.com/) om uit te voeren van uw beoordeling.</span><span class="sxs-lookup"><span data-stu-id="6f5c2-110">You can use the Azure AD Privileged Identity Management (PIM) application in the [Azure portal](https://portal.azure.com/) to perform your review.</span></span>  <span data-ttu-id="6f5c2-111">Als u niet de Azure AD Privileged Identity Management-toepassing op uw portal hebt, als volgt te werk om te beginnen.</span><span class="sxs-lookup"><span data-stu-id="6f5c2-111">If you don't have the Azure AD Privileged Identity Management application on your portal, follow these steps to get started.</span></span>

1. <span data-ttu-id="6f5c2-112">Meld u aan bij [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="6f5c2-112">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="6f5c2-113">Selecteer uw gebruikersnaam in de rechterbovenhoek van het Azure-portal en selecteer de map waar u wilt dat u werkt.</span><span class="sxs-lookup"><span data-stu-id="6f5c2-113">Select your username in the upper right-hand corner of the Azure portal, and select the directory where you will you be operating.</span></span>
3. <span data-ttu-id="6f5c2-114">Selecteer **Meer services** en gebruik het tekstvak Filteren om te zoeken naar **Azure AD Privileged Identity Management**.</span><span class="sxs-lookup"><span data-stu-id="6f5c2-114">Select **More services** and use the Filter textbox to search for **Azure AD Privileged Identity Management**.</span></span>
4. <span data-ttu-id="6f5c2-115">Schakel **Vastmaken aan dashboard** in en klik op de knop **Maken**.</span><span class="sxs-lookup"><span data-stu-id="6f5c2-115">Check **Pin to dashboard** and then click **Create**.</span></span> <span data-ttu-id="6f5c2-116">De Privileged Identity Management-toepassing wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="6f5c2-116">The Privileged Identity Management application will open.</span></span>

## <a name="approve-or-deny-access"></a><span data-ttu-id="6f5c2-117">Goedkeuren of weigeren van toegang</span><span class="sxs-lookup"><span data-stu-id="6f5c2-117">Approve or deny access</span></span>
<span data-ttu-id="6f5c2-118">Wanneer u goedkeuren of weigeren van toegang, u hebt zojuist zorgt ervoor dat de revisor of u deze rol of niet.</span><span class="sxs-lookup"><span data-stu-id="6f5c2-118">When you approve or deny access, you're just telling the reviewer whether you still use this role or not.</span></span> <span data-ttu-id="6f5c2-119">Kies **goedkeuren** als u wilt blijven in de rol of **weigeren** als u de toegang niet meer nodig.</span><span class="sxs-lookup"><span data-stu-id="6f5c2-119">Choose **Approve** if you want to stay in the role, or **Deny** if you don't need the access anymore.</span></span> <span data-ttu-id="6f5c2-120">De status niet meteen gewijzigd totdat de revisor van toepassing de resultaten is.</span><span class="sxs-lookup"><span data-stu-id="6f5c2-120">Your status won't change right away, until the reviewer applies the results.</span></span>
<span data-ttu-id="6f5c2-121">Volg deze stappen om te zoeken en voltooien van de controle van toegang:</span><span class="sxs-lookup"><span data-stu-id="6f5c2-121">Follow these steps to find and complete the access review:</span></span>

1. <span data-ttu-id="6f5c2-122">Selecteer in de toepassing PIM **revisie bevoegde toegang**.</span><span class="sxs-lookup"><span data-stu-id="6f5c2-122">In the PIM application, select **Review privileged access**.</span></span> <span data-ttu-id="6f5c2-123">Als u geen beoordelingen die in behandeling toegang hebt, wordt deze weergegeven in de blade van Azure AD Access beoordelingen.</span><span class="sxs-lookup"><span data-stu-id="6f5c2-123">If you have any pending access reviews, they appear in the Azure AD Access reviews blade.</span></span>
2. <span data-ttu-id="6f5c2-124">Selecteer de revisie die u wilt voltooien.</span><span class="sxs-lookup"><span data-stu-id="6f5c2-124">Select the review you want to complete.</span></span>
3. <span data-ttu-id="6f5c2-125">Tenzij u de controle hebt gemaakt, wordt u worden weergegeven als de enige gebruiker in de evaluatie.</span><span class="sxs-lookup"><span data-stu-id="6f5c2-125">Unless you created the review, you appear as the only user in the review.</span></span> <span data-ttu-id="6f5c2-126">Selecteer het selectievakje naast uw naam.</span><span class="sxs-lookup"><span data-stu-id="6f5c2-126">Select the check mark next to your name.</span></span>
4. <span data-ttu-id="6f5c2-127">Kies een **goedkeuren** of **weigeren**.</span><span class="sxs-lookup"><span data-stu-id="6f5c2-127">Choose either **Approve** or **Deny**.</span></span> <span data-ttu-id="6f5c2-128">Mogelijk moet u een reden voor uw beslissing in omvatten de **een reden opgeven** in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="6f5c2-128">You may need to include a reason for your decision in the **Provide a reason** text box.</span></span>  
5. <span data-ttu-id="6f5c2-129">Sluit de **revisie Azure AD-rollen** blade.</span><span class="sxs-lookup"><span data-stu-id="6f5c2-129">Close the **Review Azure AD roles** blade.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="6f5c2-130">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6f5c2-130">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
