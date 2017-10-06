---
title: aaaHow toomanage rolinstellingen activering | Microsoft Docs
description: Meer informatie over hoe toochange standaardinstellingen voor bevoegde identiteiten Hallo Hello Azure Active Directory Privileged Identity Management-extensie.
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: f6cbcb6a-8a89-4077-afd8-06c94a64f4aa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 453bb6f8f8e0fd2598cb073ef86c1dd55458dc72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-role-activation-settings-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="9489e-103">Hoe toomanage rolinstellingen activering in Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="9489e-103">How toomanage role activation settings in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="9489e-104">Een beheerder met bevoorrechte rol kunt aanpassen Azure AD Privileged Identity Management (PIM) in hun organisatie, inclusief wijzigen Hallo ervaring voor een gebruiker die een in aanmerking komende roltoewijzing is geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="9489e-104">A privileged role administrator can customize Azure AD Privileged Identity Management (PIM) in their organization, including changing hello experience for a user who is activating an eligible role assignment.</span></span>

## <a name="manage-hello-role-activation-settings"></a><span data-ttu-id="9489e-105">Hallo rol activeringsinstellingen beheren</span><span class="sxs-lookup"><span data-stu-id="9489e-105">Manage hello role activation settings</span></span>
1. <span data-ttu-id="9489e-106">Ga toohello [Azure-portal](https://portal.azure.com) en selecteer Hallo **Azure AD Privileged Identity Management** app vanuit Hallo-dashboard.</span><span class="sxs-lookup"><span data-stu-id="9489e-106">Go toohello [Azure portal](https://portal.azure.com) and select hello **Azure AD Privileged Identity Management** app from hello dashboard.</span></span>
2. <span data-ttu-id="9489e-107">Selecteer **bevoorrechte rollen beheren** > **instellingen** > **bevoorrechte rollen**.</span><span class="sxs-lookup"><span data-stu-id="9489e-107">Select **Manage privileged roles** > **Settings** > **Privileged Roles**.</span></span>
3. <span data-ttu-id="9489e-108">Kies Hallo rol waarvan u de instellingen u wilt dat toomanage.</span><span class="sxs-lookup"><span data-stu-id="9489e-108">Choose hello role whose settings you want toomanage.</span></span>

<span data-ttu-id="9489e-109">Er zijn een aantal instellingen die u kunt configureren op Hallo instellingenpagina voor elke rol.</span><span class="sxs-lookup"><span data-stu-id="9489e-109">On hello settings page for each role, there are a number of settings you can configure.</span></span> <span data-ttu-id="9489e-110">Deze instellingen zijn alleen van invloed op gebruikers die in aanmerking komende beheerders, niet-permanente beheerders zijn.</span><span class="sxs-lookup"><span data-stu-id="9489e-110">These settings only affect users who are eligible admins, not permanent admins.</span></span>

<span data-ttu-id="9489e-111">**Activeringen**: Hallo tijd, in uren, die een rol actief blijft voordat het verloopt.</span><span class="sxs-lookup"><span data-stu-id="9489e-111">**Activations**: hello time, in hours, that a role stays active before it expires.</span></span> <span data-ttu-id="9489e-112">Dit kan zijn tussen 1 en 72 uur.</span><span class="sxs-lookup"><span data-stu-id="9489e-112">This can be between 1 and 72 hours.</span></span>

<span data-ttu-id="9489e-113">**Meldingen**: U kunt kiezen of Hallo verzendt het afdruksysteem van e-mailberichten tooadmins bevestigen dat ze een rol hebben geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="9489e-113">**Notifications**: You can choose whether or not hello system sends emails tooadmins confirming that they have activated a role.</span></span> <span data-ttu-id="9489e-114">Dit kan handig zijn voor het detecteren van niet-geautoriseerde of illegale activeringen zijn.</span><span class="sxs-lookup"><span data-stu-id="9489e-114">This can be useful for detecting unauthorized or illegitimate activations.</span></span>

<span data-ttu-id="9489e-115">**Ticket incident/aanvraag**: U kunt kiezen of toorequire in aanmerking komende admins tooinclude een ticket number wanneer ze hun rol activeert.</span><span class="sxs-lookup"><span data-stu-id="9489e-115">**Incident/Request Ticket**: You can choose whether or not toorequire eligible admins tooinclude a ticket number when they activate their role.</span></span> <span data-ttu-id="9489e-116">Dit kan nuttig zijn wanneer u de rol toegang audits uitvoert.</span><span class="sxs-lookup"><span data-stu-id="9489e-116">This can be useful when you perform role access audits.</span></span>

<span data-ttu-id="9489e-117">**Multi-Factor Authentication**: U kunt kiezen of toorequire gebruikers tooverify hun identiteit met MFA voordat ze hun rollen kunnen activeren.</span><span class="sxs-lookup"><span data-stu-id="9489e-117">**Multi-Factor Authentication**: You can choose whether or not toorequire users tooverify their identity with MFA before they can activate their roles.</span></span> <span data-ttu-id="9489e-118">Ze alleen hebben tooverify deze eenmaal per sessie niet elke keer dat ze een rol activeren.</span><span class="sxs-lookup"><span data-stu-id="9489e-118">They only have tooverify this once per session, not every time they activate a role.</span></span> <span data-ttu-id="9489e-119">Er zijn twee tips tookeep in rekening wanneer u MFA inschakelen:</span><span class="sxs-lookup"><span data-stu-id="9489e-119">There are two tips tookeep in mind when you enable MFA:</span></span>

* <span data-ttu-id="9489e-120">Gebruikers met Microsoft-account voor hun e-mailadressen (meestal @outlook.com, maar niet altijd) kan niet registreren voor Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="9489e-120">Users who have Microsoft accounts for their email addresses (typically @outlook.com, but not always) cannot register for Azure MFA.</span></span> <span data-ttu-id="9489e-121">Als u tooassign rollen toousers met Microsoft-accounts wilt, moet u doen permanente beheerders of MFA uitschakelen voor die rol.</span><span class="sxs-lookup"><span data-stu-id="9489e-121">If you want tooassign roles toousers with Microsoft accounts, you should either make them permanent admins or disable MFA for that role.</span></span>
* <span data-ttu-id="9489e-122">U kunt MFA niet uitschakelen voor maximaal bevoorrechte rollen voor Azure AD en Office365.</span><span class="sxs-lookup"><span data-stu-id="9489e-122">You cannot disable MFA for highly privileged roles for Azure AD and Office365.</span></span> <span data-ttu-id="9489e-123">Dit is een functie veiligheid omdat deze rollen moeten zorgvuldig worden beveiligd:</span><span class="sxs-lookup"><span data-stu-id="9489e-123">This is a safety feature because these roles should be carefully protected:</span></span>  
  
  * <span data-ttu-id="9489e-124">Toepassingsbeheerder</span><span class="sxs-lookup"><span data-stu-id="9489e-124">Application administrator</span></span>
  * <span data-ttu-id="9489e-125">Toepassingsbeheerder Proxy server</span><span class="sxs-lookup"><span data-stu-id="9489e-125">Application Proxy server administrator</span></span>
  * <span data-ttu-id="9489e-126">Financieel medewerker</span><span class="sxs-lookup"><span data-stu-id="9489e-126">Billing administrator</span></span>  
  * <span data-ttu-id="9489e-127">Naleving beheerder</span><span class="sxs-lookup"><span data-stu-id="9489e-127">Compliance administrator</span></span>  
  * <span data-ttu-id="9489e-128">CRM-servicebeheerder</span><span class="sxs-lookup"><span data-stu-id="9489e-128">CRM service administrator</span></span>
  * <span data-ttu-id="9489e-129">Klant LockBox toegang goedkeurder</span><span class="sxs-lookup"><span data-stu-id="9489e-129">Customer LockBox access approver</span></span>
  * <span data-ttu-id="9489e-130">Schrijver van de Directory</span><span class="sxs-lookup"><span data-stu-id="9489e-130">Directory writer</span></span>  
  * <span data-ttu-id="9489e-131">Exchange-beheerder</span><span class="sxs-lookup"><span data-stu-id="9489e-131">Exchange administrator</span></span>  
  * <span data-ttu-id="9489e-132">Globale beheerder</span><span class="sxs-lookup"><span data-stu-id="9489e-132">Global administrator</span></span>
  * <span data-ttu-id="9489e-133">Intune-servicebeheerder</span><span class="sxs-lookup"><span data-stu-id="9489e-133">Intune service administrator</span></span>
  * <span data-ttu-id="9489e-134">Postvak beheerder</span><span class="sxs-lookup"><span data-stu-id="9489e-134">Mailbox administrator</span></span>  
  * <span data-ttu-id="9489e-135">Partner tier1-ondersteuning</span><span class="sxs-lookup"><span data-stu-id="9489e-135">Partner tier1 support</span></span>  
  * <span data-ttu-id="9489e-136">Partner tier2-ondersteuning</span><span class="sxs-lookup"><span data-stu-id="9489e-136">Partner tier2 support</span></span>  
  * <span data-ttu-id="9489e-137">Beheerder met bevoorrechte rol</span><span class="sxs-lookup"><span data-stu-id="9489e-137">Privileged role administrator</span></span>   
  * <span data-ttu-id="9489e-138">Beveiligingsbeheerder</span><span class="sxs-lookup"><span data-stu-id="9489e-138">Security administrator</span></span>  
  * <span data-ttu-id="9489e-139">SharePoint-beheerder</span><span class="sxs-lookup"><span data-stu-id="9489e-139">SharePoint administrator</span></span>  
  * <span data-ttu-id="9489e-140">Skype voor Bedrijven-beheerder</span><span class="sxs-lookup"><span data-stu-id="9489e-140">Skype for Business administrator</span></span>  
  * <span data-ttu-id="9489e-141">De beheerder van gebruiker</span><span class="sxs-lookup"><span data-stu-id="9489e-141">User account administrator</span></span>  

<span data-ttu-id="9489e-142">Zie voor meer informatie over het gebruik van MFA met PIM [hoe tooRequire MFA](active-directory-privileged-identity-management-how-to-require-mfa.md).</span><span class="sxs-lookup"><span data-stu-id="9489e-142">For more information about using MFA with PIM see [How tooRequire MFA](active-directory-privileged-identity-management-how-to-require-mfa.md).</span></span>

<!--PLACEHOLDER: Need an explanation of what hello temporary Global Administrator setting is for.-->

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="9489e-143">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9489e-143">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

