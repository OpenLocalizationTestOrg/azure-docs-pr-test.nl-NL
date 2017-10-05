---
title: Een verwijderde Office 365-groep in Azure Active Directory herstellen | Microsoft Docs
description: Het herstellen van een verwijderde groep, terug te zetten groepen weergeven en verwijderen van permamnently een groep in Azure Active Directory
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cc5f232a-1e77-45c2-b28b-1fcb4621725c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: curtand
ms.openlocfilehash: 32d36ae96797a59bb47bf782ab038f21f231f046
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="restore-a-deleted-office-365-group-in-azure-active-directory"></a><span data-ttu-id="51d7f-103">Een verwijderde Office 365-groep in Azure Active Directory herstellen</span><span class="sxs-lookup"><span data-stu-id="51d7f-103">Restore a deleted Office 365 group in Azure Active Directory</span></span>

<span data-ttu-id="51d7f-104">Wanneer u verwijdert een Office 365-groep in de Azure Active Directory (Azure AD), is de verwijderde groep behouden, maar niet zichtbaar voor 30 dagen van de datum van verwijdering.</span><span class="sxs-lookup"><span data-stu-id="51d7f-104">When you delete an Office 365 group in the Azure Active Directory (Azure AD), the deleted group is retained but not visible for 30 days from the deletion date.</span></span> <span data-ttu-id="51d7f-105">Dit is zodat de groep en de inhoud ervan kunnen worden hersteld indien nodig.</span><span class="sxs-lookup"><span data-stu-id="51d7f-105">This is so that the group and its contents can be restored if needed.</span></span> <span data-ttu-id="51d7f-106">Deze functionaliteit is beperkt uitsluitend tot Office 365-groepen in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="51d7f-106">This functionality is restricted exclusively to Office 365 groups in Azure AD.</span></span> <span data-ttu-id="51d7f-107">Het is niet beschikbaar voor beveiligingsgroepen en distributiegroepen.</span><span class="sxs-lookup"><span data-stu-id="51d7f-107">It is not available for security groups and distribution groups.</span></span>

> [!NOTE] 
> <span data-ttu-id="51d7f-108">Gebruik geen `Remove-MsolGroup` omdat deze de groep permanent worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="51d7f-108">Don't use `Remove-MsolGroup` because it purges the group permanently.</span></span> <span data-ttu-id="51d7f-109">Gebruik altijd `Remove-AzureADMSGroup` een O365-groep verwijderen.</span><span class="sxs-lookup"><span data-stu-id="51d7f-109">Always use `Remove-AzureADMSGroup` to delete an O365 group.</span></span> 

<span data-ttu-id="51d7f-110">De vereiste machtigingen voor het herstellen van een groep kunnen een van de volgende zijn:</span><span class="sxs-lookup"><span data-stu-id="51d7f-110">The permissions required to restore a group can be any of the following:</span></span>

<span data-ttu-id="51d7f-111">Rol</span><span class="sxs-lookup"><span data-stu-id="51d7f-111">Role</span></span>  | <span data-ttu-id="51d7f-112">Machtigingen</span><span class="sxs-lookup"><span data-stu-id="51d7f-112">Permissions</span></span> 
--------- | ---------
<span data-ttu-id="51d7f-113">Bedrijfsbeheerder, Partner Tier2 ondersteuning en beheerders van InTune-Service</span><span class="sxs-lookup"><span data-stu-id="51d7f-113">Company Administrator, Partner Tier2 support, and InTune Service Admins</span></span> | <span data-ttu-id="51d7f-114">Een verwijderde groep voor Office 365 kunt herstellen</span><span class="sxs-lookup"><span data-stu-id="51d7f-114">Can restore any deleted Office 365 group</span></span> 
<span data-ttu-id="51d7f-115">Ondersteuning voor de beheerder van gebruiker en Partner Tier1</span><span class="sxs-lookup"><span data-stu-id="51d7f-115">User Account Administrator and Partner Tier1 support</span></span> | <span data-ttu-id="51d7f-116">Een verwijderde groep Office 365, behalve de toegewezen aan de Company Administrator-rol kunt herstellen</span><span class="sxs-lookup"><span data-stu-id="51d7f-116">Can restore any deleted Office 365 group except those assigned to the Company Administrator role</span></span> 
<span data-ttu-id="51d7f-117">Gebruiker</span><span class="sxs-lookup"><span data-stu-id="51d7f-117">User</span></span> | <span data-ttu-id="51d7f-118">Een verwijderde Office 365-groep waarvan ze eigenaar kunt herstellen</span><span class="sxs-lookup"><span data-stu-id="51d7f-118">Can restore any deleted Office 365 group that they owned</span></span> 


## <a name="view-the-deleted-office-365-groups-that-are-available-to-restore"></a><span data-ttu-id="51d7f-119">De verwijderde Office 365-groepen die beschikbaar zijn voor het herstellen weergeven</span><span class="sxs-lookup"><span data-stu-id="51d7f-119">View the deleted Office 365 groups that are available to restore</span></span>
<span data-ttu-id="51d7f-120">De volgende cmdlets kunnen worden gebruikt om de verwijderde groepen om te controleren dat de een- of die u geïnteresseerd bent in zijn niet nog permanent verwijderd.</span><span class="sxs-lookup"><span data-stu-id="51d7f-120">The following cmdlets can be used to view the deleted groups to verify that the one or ones you're interested in have not yet been permanently purged.</span></span> <span data-ttu-id="51d7f-121">Deze cmdlets deel uitmaken van de [Azure AD PowerShell-module](https://www.powershellgallery.com/packages/AzureAD/).</span><span class="sxs-lookup"><span data-stu-id="51d7f-121">These cmdlets are part of the [Azure AD PowerShell module](https://www.powershellgallery.com/packages/AzureAD/).</span></span> <span data-ttu-id="51d7f-122">Meer informatie over deze module kunt u vinden de [Azure Active Directory PowerShell versie 2](/powershell/azure/install-adv2?view=azureadps-2.0) artikel.</span><span class="sxs-lookup"><span data-stu-id="51d7f-122">More information about this module can be found in the [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0) article.</span></span>

1.  <span data-ttu-id="51d7f-123">Voer de volgende cmdlet als u wilt weergeven van alle verwijderde Office 365-groepen in uw tenant die nog steeds beschikbaar zijn om te herstellen.</span><span class="sxs-lookup"><span data-stu-id="51d7f-123">Run the following cmdlet to display all deleted Office 365 groups in your tenant that are still available to restore.</span></span>
  ```
  Get-AzureADMSDeletedGroup
  ```

2.  <span data-ttu-id="51d7f-124">Als u de object-id van een specifieke groep weet (en u dit van de cmdlet in stap 1 downloaden kunt) Voer ook de volgende cmdlet om te controleren of de specifieke verwijderde groep is niet nog is permanent verwijderd.</span><span class="sxs-lookup"><span data-stu-id="51d7f-124">Alternately, if you know the objectID of a specific group (and you can get it from the cmdlet in step 1), run the following cmdlet to verify that the specific deleted group has not yet been permanently purged.</span></span>
  ```
  Get-AzureADMSDeletedGroup –Id <objectId>
  ```



## <a name="how-to-restore-your-deleted-office-365-group"></a><span data-ttu-id="51d7f-125">Het herstellen van de verwijderde Office 365-groep</span><span class="sxs-lookup"><span data-stu-id="51d7f-125">How to restore your deleted Office 365 group</span></span>
<span data-ttu-id="51d7f-126">Zodra u hebt gecontroleerd of de groep nog steeds beschikbaar om te herstellen, herstelt u de verwijderde groep met een van de volgende stappen uit.</span><span class="sxs-lookup"><span data-stu-id="51d7f-126">Once you have verified that the group is still available to restore, restore the deleted group with one of the following steps.</span></span> <span data-ttu-id="51d7f-127">Als de groep documenten, SP sites of andere permanente objecten bevat, duurt het tot 24 uur voor herstellen van een groep en de inhoud ervan.</span><span class="sxs-lookup"><span data-stu-id="51d7f-127">If the group contains documents, SP sites, or other persistent objects, it might take up to 24 hours to fully restore a group and its contents.</span></span>

1.  <span data-ttu-id="51d7f-128">Voer de volgende cmdlet voor het herstellen van de groep en de inhoud ervan.</span><span class="sxs-lookup"><span data-stu-id="51d7f-128">Run the following cmdlet to restore the group and its contents.</span></span>
  
  ```
  Restore-AzureADMSDeletedDirectoryObject –Id <objectId>
  ``` 

<span data-ttu-id="51d7f-129">U kunt ook kan de volgende cmdlet worden uitgevoerd als permanent wilt verwijderen de verwijderde groep.</span><span class="sxs-lookup"><span data-stu-id="51d7f-129">Alternatively, the following cmdlet can be run to permanently remove the deleted group.</span></span>
  ```
  Remove-AzureADMSDeletedDirectoryObject –Id <objectId>
  ```

## <a name="how-do-you-know-this-worked"></a><span data-ttu-id="51d7f-130">Hoe weet u Hiermee gewerkte?</span><span class="sxs-lookup"><span data-stu-id="51d7f-130">How do you know this worked?</span></span>
<span data-ttu-id="51d7f-131">Om te bevestigen dat u hebt een Office 365-groep is hersteld, voer de `Get-AzureADGroup –ObjectId <objectId>` cmdlet om informatie over de groep weer te geven.</span><span class="sxs-lookup"><span data-stu-id="51d7f-131">To verify that you’ve successfully restored an Office 365 group, run the `Get-AzureADGroup –ObjectId <objectId>` cmdlet to display information about the group.</span></span> <span data-ttu-id="51d7f-132">Na het terugzetten van de is aanvraag voltooid:</span><span class="sxs-lookup"><span data-stu-id="51d7f-132">After the restore request is completed:</span></span>
- <span data-ttu-id="51d7f-133">De groep wordt weergegeven in de linkernavigatiebalk op Exchange</span><span class="sxs-lookup"><span data-stu-id="51d7f-133">The group will appear in the Left nav bar on Exchange</span></span>
- <span data-ttu-id="51d7f-134">Het plan voor de groep wordt weergegeven in de Planner</span><span class="sxs-lookup"><span data-stu-id="51d7f-134">The plan for the group will appear in Planner</span></span>
- <span data-ttu-id="51d7f-135">Alle Sharepoint-sites en de bijbehorende inhoud is beschikbaar</span><span class="sxs-lookup"><span data-stu-id="51d7f-135">Any Sharepoint sites and all of their contents will be available</span></span>
- <span data-ttu-id="51d7f-136">De groep kan worden geopend vanuit een van de Exchange-eindpunten en andere Office 365-werkbelastingen die ondersteuning bieden voor Office 365-groepen</span><span class="sxs-lookup"><span data-stu-id="51d7f-136">The group can be accessed from any of the Exchange endpoints and other Office 365 workloads that support Office 365 groups</span></span>


## <a name="next-steps"></a><span data-ttu-id="51d7f-137">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="51d7f-137">Next steps</span></span>
<span data-ttu-id="51d7f-138">Deze artikelen bevatten aanvullende informatie over Azure Active Directory-groepen.</span><span class="sxs-lookup"><span data-stu-id="51d7f-138">These articles provide additional information on Azure Active Directory groups.</span></span>

* [<span data-ttu-id="51d7f-139">Zie de bestaande groepen</span><span class="sxs-lookup"><span data-stu-id="51d7f-139">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="51d7f-140">Instellingen van een groep beheren</span><span class="sxs-lookup"><span data-stu-id="51d7f-140">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="51d7f-141">Leden van een groep beheren</span><span class="sxs-lookup"><span data-stu-id="51d7f-141">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="51d7f-142">Lidmaatschap van een groep beheren</span><span class="sxs-lookup"><span data-stu-id="51d7f-142">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="51d7f-143">Dynamische regels voor gebruikers in een groep beheren</span><span class="sxs-lookup"><span data-stu-id="51d7f-143">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
