---
title: aaaPreview Office 365-groepen vervaldatum in Azure Active Directory | Microsoft Docs
description: Hoe tooset up verlooptijd voor Office 365 groepen in Azure Active Directory (preview)
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
ms.openlocfilehash: a8c99961cff3aad3f4d8b0cc1b2eb8e8a4c9ba95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-office-365-groups-expiration-preview"></a><span data-ttu-id="82271-103">Verlooptijd van Office 365-groepen (preview) configureren</span><span class="sxs-lookup"><span data-stu-id="82271-103">Configure Office 365 groups expiration (preview)</span></span>

<span data-ttu-id="82271-104">U kunt nu Hallo levenscyclus van Office 365-groepen beheren door de vervaldatum voor Office 365-groepen die u selecteert.</span><span class="sxs-lookup"><span data-stu-id="82271-104">You can now manage hello lifecycle of Office 365 groups by setting expiration for any Office 365 groups that you select.</span></span> <span data-ttu-id="82271-105">Zodra deze verlooptijd is ingesteld, eigenaars van deze groepen worden gevraagd toorenew als ze nog Hallo groepen moeten de groepen.</span><span class="sxs-lookup"><span data-stu-id="82271-105">Once this expiration is set, owners of those groups are asked toorenew their groups if they still need hello groups.</span></span> <span data-ttu-id="82271-106">Een Office 365-groep die niet wordt verlengd worden, verwijderd.</span><span class="sxs-lookup"><span data-stu-id="82271-106">Any Office 365 group that is not renewed will be deleted.</span></span> <span data-ttu-id="82271-107">Een Office 365-groep is verwijderd, kan door de eigenaars Groepsbeleid Hallo of Hallo beheerder binnen 30 dagen worden hersteld.</span><span class="sxs-lookup"><span data-stu-id="82271-107">Any Office 365 group that was deleted can be restored within 30 days by hello group owners or hello administrator.</span></span>  


> [!NOTE]
> <span data-ttu-id="82271-108">U kunt instellen dat verlopen voor Office 365-groepen.</span><span class="sxs-lookup"><span data-stu-id="82271-108">You can set expiration for only Office 365 groups.</span></span>
>
> <span data-ttu-id="82271-109">Vervaldatum voor O365 groepen is vereist dat een Azure AD Premium-licentie is toegewezen aan</span><span class="sxs-lookup"><span data-stu-id="82271-109">Setting expiration for O365 groups requires that an Azure AD Premium license is assigned to</span></span>
>   - <span data-ttu-id="82271-110">Hallo beheerder Hallo verlopen instellingen voor Hallo tenant configureert</span><span class="sxs-lookup"><span data-stu-id="82271-110">hello administrator who configures hello expiration settings for hello tenant</span></span>
>   - <span data-ttu-id="82271-111">Alle leden van het Hallo-groepen die zijn geselecteerd voor deze instelling</span><span class="sxs-lookup"><span data-stu-id="82271-111">All members of hello groups selected for this setting</span></span>

## <a name="set-office-365-groups-expiration"></a><span data-ttu-id="82271-112">Instellen dat verlopen voor Office 365-groepen</span><span class="sxs-lookup"><span data-stu-id="82271-112">Set Office 365 groups expiration</span></span>

1. <span data-ttu-id="82271-113">Open Hallo [Azure AD-beheercentrum](https://aad.portal.azure.com) met een account dat een globale beheerder in uw Azure AD-tenant.</span><span class="sxs-lookup"><span data-stu-id="82271-113">Open hello [Azure AD admin center](https://aad.portal.azure.com) with an account that is a global administrator in your Azure AD tenant.</span></span>

2. <span data-ttu-id="82271-114">Open Azure AD, selecteer **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="82271-114">Open Azure AD, select **Users and groups**.</span></span>

3. <span data-ttu-id="82271-115">Selecteer **groepsinstellingen** en selecteer vervolgens **verlopen** tooopen Hallo verlopen instellingen.</span><span class="sxs-lookup"><span data-stu-id="82271-115">Select **Group settings** and then select **Expiration** tooopen hello expiration settings.</span></span>
  
  ![Blade verlopen](./media/active-directory-groups-lifecycle-azure-portal/expiration-settings.png)

4. <span data-ttu-id="82271-117">Op Hallo **verlopen** blade kunt u:</span><span class="sxs-lookup"><span data-stu-id="82271-117">On hello **Expiration** blade, you can:</span></span>

  * <span data-ttu-id="82271-118">Hallo groep levensduur in dagen ingesteld.</span><span class="sxs-lookup"><span data-stu-id="82271-118">Set hello group lifetime in days.</span></span> <span data-ttu-id="82271-119">U kunt een van selecteren Hallo vooraf ingestelde waarden of een aangepaste waarde (moet 31 dagen of meer).</span><span class="sxs-lookup"><span data-stu-id="82271-119">You could select one of hello preset values, or a custom value (should be 31 days or more).</span></span> 
  * <span data-ttu-id="82271-120">Geef een e-mailadres waar Hallo vernieuwing en verlopen-meldingen moeten worden verzonden wanneer een groep geen eigenaar heeft.</span><span class="sxs-lookup"><span data-stu-id="82271-120">Specify an email address where hello renewal and expiration notifications should be sent when a group has no owner.</span></span> 
  * <span data-ttu-id="82271-121">Selecteer welke groepen door Office 365 verloopt.</span><span class="sxs-lookup"><span data-stu-id="82271-121">Select which Office 365 groups expire.</span></span> <span data-ttu-id="82271-122">U kunt de vervaldatum voor inschakelen **alle** Office 365-groepen die u kunt selecteren uit Hallo Office 365-groepen of u selecteert **geen** verlopen voor alle groepen uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="82271-122">You can enable expiration for **All** Office 365 groups, you can select from among hello Office 365 groups, or you select **None** to disable expiration for all groups.</span></span>
  * <span data-ttu-id="82271-123">Uw instellingen opslaan als u bent met het selecteren van klaar **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="82271-123">Save your settings when you're done by selecting **Save**.</span></span>

<span data-ttu-id="82271-124">Zie voor instructies over hoe toodownload en installeer Microsoft PowerShell-module tooconfigure verlooptijd voor Office 365-groepen via PowerShell hello, [Azure Active Directory V2 PowerShell-Module - openbare Preview-versie 2.0.0.137](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.137).</span><span class="sxs-lookup"><span data-stu-id="82271-124">For instructions on how toodownload and install hello Microsoft PowerShell module tooconfigure expiration for Office 365 groups via PowerShell, see [Azure Active Directory V2 PowerShell Module - Public Preview Release 2.0.0.137](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.137).</span></span>

<span data-ttu-id="82271-125">E-mailmeldingen zoals deze worden verzonden toohello Office 365-groepeigenaren 30 dagen, 15 dagen en 1 dag voorafgaande tooexpiration van Hallo-groep.</span><span class="sxs-lookup"><span data-stu-id="82271-125">Email notifications such as this one are sent toohello Office 365 group owners 30 days, 15 days, and 1 day prior tooexpiration of hello group.</span></span>

![Verlopen van e-mailmeldingen](./media/active-directory-groups-lifecycle-azure-portal/expiration-notification.png)

<span data-ttu-id="82271-127">Groepseigenaar Hallo kunt selecteren **vernieuwen groep** toorenew Hallo Office 365-groep, of kunt selecteren **gaat toogroup** toosee Hallo leden en andere details over Hallo groep.</span><span class="sxs-lookup"><span data-stu-id="82271-127">hello group owner can then select **Renew group** toorenew hello Office 365 group, or can select **Go toogroup** toosee hello members and other details about hello group.</span></span>

<span data-ttu-id="82271-128">Wanneer een groep is verlopen, is één dag na de verloopdatum Hallo door Hallo-groep verwijderd.</span><span class="sxs-lookup"><span data-stu-id="82271-128">When a group expires, hello group is deleted one day after hello expiration date.</span></span> <span data-ttu-id="82271-129">Een e-mailmelding zoals deze wordt verzonden toohello Office 365-groepeigenaren mededeling over Hallo is verlopen en latere verwijdering van hun Office 365-groep.</span><span class="sxs-lookup"><span data-stu-id="82271-129">An email notification such as this one is sent toohello Office 365 group owners informing them about hello expiration and subsequent deletion of their Office 365 group.</span></span>

![E-mailmeldingen in verwijderen](./media/active-directory-groups-lifecycle-azure-portal/deletion-notification.png)

<span data-ttu-id="82271-131">Hallo-groep kan worden hersteld door het selecteren van **groepsbeleidsobject herstellen** of met behulp van PowerShell-cmdlets, zoals beschreven in [terugzetten van een verwijderde Office 365-groep in Azure Active Directory] (https://docs.microsoft.com/azure/active-directory/ Active-Directory-Groups-Restore-Azure-Portal).</span><span class="sxs-lookup"><span data-stu-id="82271-131">hello group can be restored by selecting **Restore group** or by using PowerShell cmdlets, as described in [Restore a deleted Office 365 group in Azure Active Directory] (https://docs.microsoft.com/azure/active-directory/active-directory-groups-restore-azure-portal).</span></span>
    
<span data-ttu-id="82271-132">Als u terugzet Hallo-groep documenten, SharePoint-sites of andere permanente objecten bevat, duurt het mogelijk up too24 uren toofully terugzetten Hallo groep en de inhoud ervan.</span><span class="sxs-lookup"><span data-stu-id="82271-132">If hello group you're restoring contains documents, SharePoint sites, or other persistent objects, it might take up too24 hours toofully restore hello group and its contents.</span></span>

> [!NOTE]
> * <span data-ttu-id="82271-133">Wanneer u instellingen voor verlooptijd Hallo implementeert, is er mogelijk bepaalde groepen die ouder dan Hallo verlopen venster zijn.</span><span class="sxs-lookup"><span data-stu-id="82271-133">When deploying hello expiration settings, there might be some groups that are older than hello expiration window.</span></span> <span data-ttu-id="82271-134">Deze groepen worden niet onmiddellijk verwijderd, maar zijn too30 dagen tot vervaldatum instellen.</span><span class="sxs-lookup"><span data-stu-id="82271-134">These groups are not be immediately deleted, but are set too30 days until expiration.</span></span> <span data-ttu-id="82271-135">Hallo eerste verlenging e-mailmelding wordt verzonden binnen een dag.</span><span class="sxs-lookup"><span data-stu-id="82271-135">hello first renewal notification email is sent out within a day.</span></span> <span data-ttu-id="82271-136">Bijvoorbeeld groep A 400 dagen geleden is gemaakt en hello verlopen-interval is ingesteld too180 dagen.</span><span class="sxs-lookup"><span data-stu-id="82271-136">For example, Group A was created 400 days ago, and hello expiration interval is set too180 days.</span></span> <span data-ttu-id="82271-137">Wanneer u instellingen voor verlooptijd toepast, heeft groep A 30 dagen voordat deze wordt verwijderd tenzij Hallo eigenaar wordt verlengd.</span><span class="sxs-lookup"><span data-stu-id="82271-137">When you apply expiration settings, Group A has 30 days before it is deleted, unless hello owner renews it.</span></span>
> * <span data-ttu-id="82271-138">Wanneer een dynamische groep is verwijderd en hersteld, wordt het gezien als een nieuwe groep en opnieuw ingevuld volgens toohello regel.</span><span class="sxs-lookup"><span data-stu-id="82271-138">When a dynamic group is deleted and restored, it is seen as a new group and re-populated according toohello rule.</span></span> <span data-ttu-id="82271-139">Too24 uur kan duren voordat dit proces.</span><span class="sxs-lookup"><span data-stu-id="82271-139">This process might take up too24 hours.</span></span>

## <a name="next-steps"></a><span data-ttu-id="82271-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="82271-140">Next steps</span></span>
<span data-ttu-id="82271-141">Deze artikelen bevatten aanvullende informatie over Azure AD-groepen.</span><span class="sxs-lookup"><span data-stu-id="82271-141">These articles provide additional information on Azure AD groups.</span></span>

* [<span data-ttu-id="82271-142">Zie de bestaande groepen</span><span class="sxs-lookup"><span data-stu-id="82271-142">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="82271-143">Instellingen van een groep beheren</span><span class="sxs-lookup"><span data-stu-id="82271-143">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="82271-144">Leden van een groep beheren</span><span class="sxs-lookup"><span data-stu-id="82271-144">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="82271-145">Lidmaatschap van een groep beheren</span><span class="sxs-lookup"><span data-stu-id="82271-145">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="82271-146">Dynamische regels voor gebruikers in een groep beheren</span><span class="sxs-lookup"><span data-stu-id="82271-146">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
