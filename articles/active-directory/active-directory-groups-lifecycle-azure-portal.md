---
title: Voorbeeld bekijken van verlopen van Office 365-groepen in Azure Active Directory | Microsoft Docs
description: Het instellen van de vervaldatum voor Office 365-groepen in Azure Active Directory (preview)
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: it-pro
ms.openlocfilehash: 8a43df84fd050d7b4bd8d937b8c55e744cb805d3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="configure-office-365-groups-expiration-preview"></a><span data-ttu-id="a415c-103">Verlooptijd van Office 365-groepen (preview) configureren</span><span class="sxs-lookup"><span data-stu-id="a415c-103">Configure Office 365 groups expiration (preview)</span></span>

<span data-ttu-id="a415c-104">U kunt nu de levenscyclus van Office 365-groepen beheren door de vervaldatum voor Office 365-groepen die u selecteert.</span><span class="sxs-lookup"><span data-stu-id="a415c-104">You can now manage the lifecycle of Office 365 groups by setting expiration for any Office 365 groups that you select.</span></span> <span data-ttu-id="a415c-105">Zodra deze verlooptijd is ingesteld, worden eigenaars van die groepen gevraagd voor het vernieuwen van de groepen als ze nog steeds de groepen nodig.</span><span class="sxs-lookup"><span data-stu-id="a415c-105">Once this expiration is set, owners of those groups are asked to renew their groups if they still need the groups.</span></span> <span data-ttu-id="a415c-106">Een Office 365-groep die niet wordt verlengd worden, verwijderd.</span><span class="sxs-lookup"><span data-stu-id="a415c-106">Any Office 365 group that is not renewed will be deleted.</span></span> <span data-ttu-id="a415c-107">Een Office 365-groep is verwijderd, kan door de eigenaars Groepsbeleid of door de beheerder binnen 30 dagen worden hersteld.</span><span class="sxs-lookup"><span data-stu-id="a415c-107">Any Office 365 group that was deleted can be restored within 30 days by the group owners or the administrator.</span></span>  


> [!NOTE]
> <span data-ttu-id="a415c-108">U kunt instellen dat verlopen voor Office 365-groepen.</span><span class="sxs-lookup"><span data-stu-id="a415c-108">You can set expiration for only Office 365 groups.</span></span>
>
> <span data-ttu-id="a415c-109">Vervaldatum voor O365 groepen is vereist dat een Azure AD Premium-licentie is toegewezen aan</span><span class="sxs-lookup"><span data-stu-id="a415c-109">Setting expiration for O365 groups requires that an Azure AD Premium license is assigned to</span></span>
>   - <span data-ttu-id="a415c-110">De beheerder de instellingen van de vervaldatum voor de tenant configureert</span><span class="sxs-lookup"><span data-stu-id="a415c-110">The administrator who configures the expiration settings for the tenant</span></span>
>   - <span data-ttu-id="a415c-111">Alle leden van de groepen die zijn geselecteerd voor deze instelling</span><span class="sxs-lookup"><span data-stu-id="a415c-111">All members of the groups selected for this setting</span></span>

## <a name="set-office-365-groups-expiration"></a><span data-ttu-id="a415c-112">Instellen dat verlopen voor Office 365-groepen</span><span class="sxs-lookup"><span data-stu-id="a415c-112">Set Office 365 groups expiration</span></span>

1. <span data-ttu-id="a415c-113">Open de [Azure AD-beheercentrum](https://aad.portal.azure.com) met een account dat een globale beheerder in uw Azure AD-tenant.</span><span class="sxs-lookup"><span data-stu-id="a415c-113">Open the [Azure AD admin center](https://aad.portal.azure.com) with an account that is a global administrator in your Azure AD tenant.</span></span>

2. <span data-ttu-id="a415c-114">Open Azure AD, selecteer **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="a415c-114">Open Azure AD, select **Users and groups**.</span></span>

3. <span data-ttu-id="a415c-115">Selecteer **groepsinstellingen** en selecteer vervolgens **verlopen** om de verloopdatum-instellingen te openen.</span><span class="sxs-lookup"><span data-stu-id="a415c-115">Select **Group settings** and then select **Expiration** to open the expiration settings.</span></span>
  
  ![Blade verlopen](./media/active-directory-groups-lifecycle-azure-portal/expiration-settings.png)

4. <span data-ttu-id="a415c-117">Op de **verlopen** blade kunt u:</span><span class="sxs-lookup"><span data-stu-id="a415c-117">On the **Expiration** blade, you can:</span></span>

  * <span data-ttu-id="a415c-118">De levensduur van de groep in dagen ingesteld.</span><span class="sxs-lookup"><span data-stu-id="a415c-118">Set the group lifetime in days.</span></span> <span data-ttu-id="a415c-119">U kunt een van de vooraf gedefinieerde waarden, of een aangepaste waarde (moet 31 dagen of meer) selecteren.</span><span class="sxs-lookup"><span data-stu-id="a415c-119">You could select one of the preset values, or a custom value (should be 31 days or more).</span></span> 
  * <span data-ttu-id="a415c-120">Geef een e-mailadres waar de vernieuwing en verlopen-meldingen moeten worden verzonden wanneer een groep geen eigenaar heeft.</span><span class="sxs-lookup"><span data-stu-id="a415c-120">Specify an email address where the renewal and expiration notifications should be sent when a group has no owner.</span></span> 
  * <span data-ttu-id="a415c-121">Selecteer welke groepen door Office 365 verloopt.</span><span class="sxs-lookup"><span data-stu-id="a415c-121">Select which Office 365 groups expire.</span></span> <span data-ttu-id="a415c-122">U kunt de vervaldatum voor inschakelen **alle** Office 365-groepen, kunt u een van de Office 365-groepen selecteren of u selecteert **geen** verlopen voor alle groepen uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="a415c-122">You can enable expiration for **All** Office 365 groups, you can select from among the Office 365 groups, or you select **None** to disable expiration for all groups.</span></span>
  * <span data-ttu-id="a415c-123">Uw instellingen opslaan als u bent met het selecteren van klaar **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="a415c-123">Save your settings when you're done by selecting **Save**.</span></span>

<span data-ttu-id="a415c-124">Zie voor instructies over het downloaden en installeren van de Microsoft PowerShell-module voor het configureren van de vervaldatum voor Office 365-groepen via PowerShell [Azure Active Directory V2 PowerShell-Module - openbare Preview-versie 2.0.0.137](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.137).</span><span class="sxs-lookup"><span data-stu-id="a415c-124">For instructions on how to download and install the Microsoft PowerShell module to configure expiration for Office 365 groups via PowerShell, see [Azure Active Directory V2 PowerShell Module - Public Preview Release 2.0.0.137](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.137).</span></span>

<span data-ttu-id="a415c-125">E-mailmeldingen zoals deze zijn verzonden naar de Office 365-eigenaars Groepsbeleid 30 dagen, 15 dagen en 1 dag vóór de vervaldatum van de groep.</span><span class="sxs-lookup"><span data-stu-id="a415c-125">Email notifications such as this one are sent to the Office 365 group owners 30 days, 15 days, and 1 day prior to expiration of the group.</span></span>

![Verlopen van e-mailmeldingen](./media/active-directory-groups-lifecycle-azure-portal/expiration-notification.png)

<span data-ttu-id="a415c-127">De Groepseigenaar kunt selecteren **vernieuwen groep** voor het vernieuwen van de Office 365 groep, of kunt selecteren **gaat u naar de groep** om te zien van de leden en andere details over de groep.</span><span class="sxs-lookup"><span data-stu-id="a415c-127">The group owner can then select **Renew group** to renew the Office 365 group, or can select **Go to group** to see the members and other details about the group.</span></span>

<span data-ttu-id="a415c-128">Wanneer een groep is verlopen, kan de groep één dag na de vervaldatum is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="a415c-128">When a group expires, the group is deleted one day after the expiration date.</span></span> <span data-ttu-id="a415c-129">Een e-mailmelding zoals deze wordt verzonden naar de Office 365-groepseigenaren waarin ze worden geïnformeerd over de vervaldatum en de volgende verwijdering van hun Office 365-groep.</span><span class="sxs-lookup"><span data-stu-id="a415c-129">An email notification such as this one is sent to the Office 365 group owners informing them about the expiration and subsequent deletion of their Office 365 group.</span></span>

![E-mailmeldingen in verwijderen](./media/active-directory-groups-lifecycle-azure-portal/deletion-notification.png)

<span data-ttu-id="a415c-131">De groep kan worden hersteld door het selecteren van **groepsbeleidsobject herstellen** of met behulp van PowerShell-cmdlets, zoals beschreven in [terugzetten van een verwijderde Office 365-groep in Azure Active Directory] (https://docs.microsoft.com/azure/active-directory/ Active-Directory-Groups-Restore-Azure-Portal).</span><span class="sxs-lookup"><span data-stu-id="a415c-131">The group can be restored by selecting **Restore group** or by using PowerShell cmdlets, as described in [Restore a deleted Office 365 group in Azure Active Directory] (https://docs.microsoft.com/azure/active-directory/active-directory-groups-restore-azure-portal).</span></span>
    
<span data-ttu-id="a415c-132">Als de groep die u terugzet documenten, SharePoint-sites of andere permanente objecten bevat, kan deze volledig herstellen van de groep en de inhoud ervan tot 24 uur duren.</span><span class="sxs-lookup"><span data-stu-id="a415c-132">If the group you're restoring contains documents, SharePoint sites, or other persistent objects, it might take up to 24 hours to fully restore the group and its contents.</span></span>

> [!NOTE]
> * <span data-ttu-id="a415c-133">Wanneer u de instellingen voor verlooptijd implementeert, is er mogelijk bepaalde groepen die ouder dan het venster verloopt zijn.</span><span class="sxs-lookup"><span data-stu-id="a415c-133">When deploying the expiration settings, there might be some groups that are older than the expiration window.</span></span> <span data-ttu-id="a415c-134">Deze groepen worden niet onmiddellijk verwijderd, maar zijn ingesteld op 30 dagen tot vervaldatum.</span><span class="sxs-lookup"><span data-stu-id="a415c-134">These groups are not be immediately deleted, but are set to 30 days until expiration.</span></span> <span data-ttu-id="a415c-135">De eerste verlenging meldingse-mail wordt verzonden binnen een dag.</span><span class="sxs-lookup"><span data-stu-id="a415c-135">The first renewal notification email is sent out within a day.</span></span> <span data-ttu-id="a415c-136">Bijvoorbeeld, groep A 400 dagen geleden is gemaakt en het Vervalinterval opgegeven is ingesteld op 180 dagen.</span><span class="sxs-lookup"><span data-stu-id="a415c-136">For example, Group A was created 400 days ago, and the expiration interval is set to 180 days.</span></span> <span data-ttu-id="a415c-137">Wanneer u instellingen voor verlooptijd toepast, heeft groep A 30 dagen voordat deze wordt verwijderd, tenzij de eigenaar deze vernieuwt.</span><span class="sxs-lookup"><span data-stu-id="a415c-137">When you apply expiration settings, Group A has 30 days before it is deleted, unless the owner renews it.</span></span>
> * <span data-ttu-id="a415c-138">Wanneer een dynamische groep is verwijderd en hersteld, wordt gezien als een nieuwe groep en opnieuw volgens de regel is ingevuld.</span><span class="sxs-lookup"><span data-stu-id="a415c-138">When a dynamic group is deleted and restored, it is seen as a new group and re-populated according to the rule.</span></span> <span data-ttu-id="a415c-139">Dit proces kan 24 uur duren.</span><span class="sxs-lookup"><span data-stu-id="a415c-139">This process might take up to 24 hours.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a415c-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a415c-140">Next steps</span></span>
<span data-ttu-id="a415c-141">Deze artikelen bevatten aanvullende informatie over Azure AD-groepen.</span><span class="sxs-lookup"><span data-stu-id="a415c-141">These articles provide additional information on Azure AD groups.</span></span>

* [<span data-ttu-id="a415c-142">Zie de bestaande groepen</span><span class="sxs-lookup"><span data-stu-id="a415c-142">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="a415c-143">Instellingen van een groep beheren</span><span class="sxs-lookup"><span data-stu-id="a415c-143">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="a415c-144">Leden van een groep beheren</span><span class="sxs-lookup"><span data-stu-id="a415c-144">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="a415c-145">Lidmaatschap van een groep beheren</span><span class="sxs-lookup"><span data-stu-id="a415c-145">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="a415c-146">Dynamische regels voor gebruikers in een groep beheren</span><span class="sxs-lookup"><span data-stu-id="a415c-146">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
