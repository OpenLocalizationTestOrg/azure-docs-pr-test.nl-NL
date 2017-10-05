---
title: Het beheren van serverfunctie-instellingen voor activering | Microsoft Docs
description: Informatie over het wijzigen van de standaardinstellingen voor bevoegde identiteiten met de extensie Azure Active Directory Privileged Identity Management.
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
ms.openlocfilehash: 23605e89cd1846d2e06e48cb5d3e0191cb9e9b4a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-role-activation-settings-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="b9c67-103">Het beheren van instellingen voor de sitesysteemrol activering in Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="b9c67-103">How to manage role activation settings in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="b9c67-104">Een beheerder met bevoorrechte rol kunt aanpassen Azure AD Privileged Identity Management (PIM) in hun organisatie, inclusief het wijzigen van de ervaring voor een gebruiker die een in aanmerking komende roltoewijzing is geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="b9c67-104">A privileged role administrator can customize Azure AD Privileged Identity Management (PIM) in their organization, including changing the experience for a user who is activating an eligible role assignment.</span></span>

## <a name="manage-the-role-activation-settings"></a><span data-ttu-id="b9c67-105">De instellingen van de activering beheren</span><span class="sxs-lookup"><span data-stu-id="b9c67-105">Manage the role activation settings</span></span>
1. <span data-ttu-id="b9c67-106">Ga naar de [Azure-portal](https://portal.azure.com) en selecteer de **Azure AD Privileged Identity Management** app vanuit het dashboard.</span><span class="sxs-lookup"><span data-stu-id="b9c67-106">Go to the [Azure portal](https://portal.azure.com) and select the **Azure AD Privileged Identity Management** app from the dashboard.</span></span>
2. <span data-ttu-id="b9c67-107">Selecteer **bevoorrechte rollen beheren** > **instellingen** > **bevoorrechte rollen**.</span><span class="sxs-lookup"><span data-stu-id="b9c67-107">Select **Manage privileged roles** > **Settings** > **Privileged Roles**.</span></span>
3. <span data-ttu-id="b9c67-108">Selecteer de rol waarvoor u de instellingen u wilt beheren.</span><span class="sxs-lookup"><span data-stu-id="b9c67-108">Choose the role whose settings you want to manage.</span></span>

<span data-ttu-id="b9c67-109">Er zijn een aantal instellingen die u kunt configureren op de instellingenpagina voor elke rol.</span><span class="sxs-lookup"><span data-stu-id="b9c67-109">On the settings page for each role, there are a number of settings you can configure.</span></span> <span data-ttu-id="b9c67-110">Deze instellingen zijn alleen van invloed op gebruikers die in aanmerking komende beheerders, niet-permanente beheerders zijn.</span><span class="sxs-lookup"><span data-stu-id="b9c67-110">These settings only affect users who are eligible admins, not permanent admins.</span></span>

<span data-ttu-id="b9c67-111">**Activeringen**: de tijd in uren, die een rol actief blijft voordat het verloopt.</span><span class="sxs-lookup"><span data-stu-id="b9c67-111">**Activations**: The time, in hours, that a role stays active before it expires.</span></span> <span data-ttu-id="b9c67-112">Dit kan zijn tussen 1 en 72 uur.</span><span class="sxs-lookup"><span data-stu-id="b9c67-112">This can be between 1 and 72 hours.</span></span>

<span data-ttu-id="b9c67-113">**Meldingen**: U kunt kiezen of het systeem e-mailberichten verzendt naar het admins bevestigen dat ze een rol hebben geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="b9c67-113">**Notifications**: You can choose whether or not the system sends emails to admins confirming that they have activated a role.</span></span> <span data-ttu-id="b9c67-114">Dit kan handig zijn voor het detecteren van niet-geautoriseerde of illegale activeringen zijn.</span><span class="sxs-lookup"><span data-stu-id="b9c67-114">This can be useful for detecting unauthorized or illegitimate activations.</span></span>

<span data-ttu-id="b9c67-115">**Ticket incident/aanvraag**: U kunt al dan niet in aanmerking komende beheerders een Ticketnummer nemen bij het activeren van hun rol nodig.</span><span class="sxs-lookup"><span data-stu-id="b9c67-115">**Incident/Request Ticket**: You can choose whether or not to require eligible admins to include a ticket number when they activate their role.</span></span> <span data-ttu-id="b9c67-116">Dit kan nuttig zijn wanneer u de rol toegang audits uitvoert.</span><span class="sxs-lookup"><span data-stu-id="b9c67-116">This can be useful when you perform role access audits.</span></span>

<span data-ttu-id="b9c67-117">**Multi-Factor Authentication**: U kunt kiezen of gebruikers hun identiteit verifiëren met MFA voordat ze hun rollen kunnen activeren.</span><span class="sxs-lookup"><span data-stu-id="b9c67-117">**Multi-Factor Authentication**: You can choose whether or not to require users to verify their identity with MFA before they can activate their roles.</span></span> <span data-ttu-id="b9c67-118">Ze hebben alleen om te controleren of deze eenmaal per sessie niet elke keer dat ze een rol activeren.</span><span class="sxs-lookup"><span data-stu-id="b9c67-118">They only have to verify this once per session, not every time they activate a role.</span></span> <span data-ttu-id="b9c67-119">Er zijn twee tips rekening moet houden wanneer u MFA inschakelen:</span><span class="sxs-lookup"><span data-stu-id="b9c67-119">There are two tips to keep in mind when you enable MFA:</span></span>

* <span data-ttu-id="b9c67-120">Gebruikers met Microsoft-account voor hun e-mailadressen (meestal @outlook.com, maar niet altijd) kan niet registreren voor Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="b9c67-120">Users who have Microsoft accounts for their email addresses (typically @outlook.com, but not always) cannot register for Azure MFA.</span></span> <span data-ttu-id="b9c67-121">Als u wilt toewijzen van rollen aan gebruikers met Microsoft-accounts, moet u doen permanente beheerders of MFA uitschakelen voor die rol.</span><span class="sxs-lookup"><span data-stu-id="b9c67-121">If you want to assign roles to users with Microsoft accounts, you should either make them permanent admins or disable MFA for that role.</span></span>
* <span data-ttu-id="b9c67-122">U kunt MFA niet uitschakelen voor maximaal bevoorrechte rollen voor Azure AD en Office365.</span><span class="sxs-lookup"><span data-stu-id="b9c67-122">You cannot disable MFA for highly privileged roles for Azure AD and Office365.</span></span> <span data-ttu-id="b9c67-123">Dit is een functie veiligheid omdat deze rollen moeten zorgvuldig worden beveiligd:</span><span class="sxs-lookup"><span data-stu-id="b9c67-123">This is a safety feature because these roles should be carefully protected:</span></span>  
  
  * <span data-ttu-id="b9c67-124">Toepassingsbeheerder</span><span class="sxs-lookup"><span data-stu-id="b9c67-124">Application administrator</span></span>
  * <span data-ttu-id="b9c67-125">Toepassingsbeheerder Proxy server</span><span class="sxs-lookup"><span data-stu-id="b9c67-125">Application Proxy server administrator</span></span>
  * <span data-ttu-id="b9c67-126">Financieel medewerker</span><span class="sxs-lookup"><span data-stu-id="b9c67-126">Billing administrator</span></span>  
  * <span data-ttu-id="b9c67-127">Naleving beheerder</span><span class="sxs-lookup"><span data-stu-id="b9c67-127">Compliance administrator</span></span>  
  * <span data-ttu-id="b9c67-128">CRM-servicebeheerder</span><span class="sxs-lookup"><span data-stu-id="b9c67-128">CRM service administrator</span></span>
  * <span data-ttu-id="b9c67-129">Klant LockBox toegang goedkeurder</span><span class="sxs-lookup"><span data-stu-id="b9c67-129">Customer LockBox access approver</span></span>
  * <span data-ttu-id="b9c67-130">Schrijver van de Directory</span><span class="sxs-lookup"><span data-stu-id="b9c67-130">Directory writer</span></span>  
  * <span data-ttu-id="b9c67-131">Exchange-beheerder</span><span class="sxs-lookup"><span data-stu-id="b9c67-131">Exchange administrator</span></span>  
  * <span data-ttu-id="b9c67-132">Globale beheerder</span><span class="sxs-lookup"><span data-stu-id="b9c67-132">Global administrator</span></span>
  * <span data-ttu-id="b9c67-133">Intune-servicebeheerder</span><span class="sxs-lookup"><span data-stu-id="b9c67-133">Intune service administrator</span></span>
  * <span data-ttu-id="b9c67-134">Postvak beheerder</span><span class="sxs-lookup"><span data-stu-id="b9c67-134">Mailbox administrator</span></span>  
  * <span data-ttu-id="b9c67-135">Partner tier1-ondersteuning</span><span class="sxs-lookup"><span data-stu-id="b9c67-135">Partner tier1 support</span></span>  
  * <span data-ttu-id="b9c67-136">Partner tier2-ondersteuning</span><span class="sxs-lookup"><span data-stu-id="b9c67-136">Partner tier2 support</span></span>  
  * <span data-ttu-id="b9c67-137">Beheerder met bevoorrechte rol</span><span class="sxs-lookup"><span data-stu-id="b9c67-137">Privileged role administrator</span></span>   
  * <span data-ttu-id="b9c67-138">Beveiligingsbeheerder</span><span class="sxs-lookup"><span data-stu-id="b9c67-138">Security administrator</span></span>  
  * <span data-ttu-id="b9c67-139">SharePoint-beheerder</span><span class="sxs-lookup"><span data-stu-id="b9c67-139">SharePoint administrator</span></span>  
  * <span data-ttu-id="b9c67-140">Skype voor Bedrijven-beheerder</span><span class="sxs-lookup"><span data-stu-id="b9c67-140">Skype for Business administrator</span></span>  
  * <span data-ttu-id="b9c67-141">De beheerder van gebruiker</span><span class="sxs-lookup"><span data-stu-id="b9c67-141">User account administrator</span></span>  

<span data-ttu-id="b9c67-142">Zie voor meer informatie over het gebruik van MFA met PIM [hoe MFA vereisen](active-directory-privileged-identity-management-how-to-require-mfa.md).</span><span class="sxs-lookup"><span data-stu-id="b9c67-142">For more information about using MFA with PIM see [How to Require MFA](active-directory-privileged-identity-management-how-to-require-mfa.md).</span></span>

<!--PLACEHOLDER: Need an explanation of what the temporary Global Administrator setting is for.-->

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="b9c67-143">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b9c67-143">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

