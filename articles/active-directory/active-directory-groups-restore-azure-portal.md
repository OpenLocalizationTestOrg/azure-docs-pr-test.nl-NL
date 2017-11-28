---
title: aaaRestore een verwijderde Office 365-groep in Azure Active Directory | Microsoft Docs
description: Hoe een verwijderde groep toorestore terug te zetten groepen weergeven en permamnently een groep in Azure Active Directory verwijderen
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
ms.openlocfilehash: 4e6650d64aa19f0c909f1c511f48681de8032f63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-deleted-office-365-group-in-azure-active-directory"></a><span data-ttu-id="1427f-103">Een verwijderde Office 365-groep in Azure Active Directory herstellen</span><span class="sxs-lookup"><span data-stu-id="1427f-103">Restore a deleted Office 365 group in Azure Active Directory</span></span>

<span data-ttu-id="1427f-104">Wanneer u een Office 365-groep in Azure Active Directory (Azure AD) Hallo verwijdert, is Hallo verwijderde groep behouden, maar niet zichtbaar voor 30 dagen van de datum van verwijdering Hallo.</span><span class="sxs-lookup"><span data-stu-id="1427f-104">When you delete an Office 365 group in hello Azure Active Directory (Azure AD), hello deleted group is retained but not visible for 30 days from hello deletion date.</span></span> <span data-ttu-id="1427f-105">Dit is zodat Hallo groep en de inhoud ervan kunnen worden hersteld indien nodig.</span><span class="sxs-lookup"><span data-stu-id="1427f-105">This is so that hello group and its contents can be restored if needed.</span></span> <span data-ttu-id="1427f-106">Deze functionaliteit is beperkt uitsluitend tooOffice 365 groepen in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1427f-106">This functionality is restricted exclusively tooOffice 365 groups in Azure AD.</span></span> <span data-ttu-id="1427f-107">Het is niet beschikbaar voor beveiligingsgroepen en distributiegroepen.</span><span class="sxs-lookup"><span data-stu-id="1427f-107">It is not available for security groups and distribution groups.</span></span>

> [!NOTE] 
> <span data-ttu-id="1427f-108">Gebruik geen `Remove-MsolGroup` omdat het Hallo-groep permanent worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="1427f-108">Don't use `Remove-MsolGroup` because it purges hello group permanently.</span></span> <span data-ttu-id="1427f-109">Gebruik altijd `Remove-AzureADMSGroup` toodelete een O365-groep.</span><span class="sxs-lookup"><span data-stu-id="1427f-109">Always use `Remove-AzureADMSGroup` toodelete an O365 group.</span></span> 

<span data-ttu-id="1427f-110">Hallo machtigingen vereist toorestore een groep mag geen van de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="1427f-110">hello permissions required toorestore a group can be any of hello following:</span></span>

<span data-ttu-id="1427f-111">Rol</span><span class="sxs-lookup"><span data-stu-id="1427f-111">Role</span></span>  | <span data-ttu-id="1427f-112">Machtigingen</span><span class="sxs-lookup"><span data-stu-id="1427f-112">Permissions</span></span> 
--------- | ---------
<span data-ttu-id="1427f-113">Bedrijfsbeheerder, Partner Tier2 ondersteuning en beheerders van InTune-Service</span><span class="sxs-lookup"><span data-stu-id="1427f-113">Company Administrator, Partner Tier2 support, and InTune Service Admins</span></span> | <span data-ttu-id="1427f-114">Een verwijderde groep voor Office 365 kunt herstellen</span><span class="sxs-lookup"><span data-stu-id="1427f-114">Can restore any deleted Office 365 group</span></span> 
<span data-ttu-id="1427f-115">Ondersteuning voor de beheerder van gebruiker en Partner Tier1</span><span class="sxs-lookup"><span data-stu-id="1427f-115">User Account Administrator and Partner Tier1 support</span></span> | <span data-ttu-id="1427f-116">Een verwijderde groep Office 365, behalve die toegewezen toohello Company Administrator-rol kunt herstellen</span><span class="sxs-lookup"><span data-stu-id="1427f-116">Can restore any deleted Office 365 group except those assigned toohello Company Administrator role</span></span> 
<span data-ttu-id="1427f-117">Gebruiker</span><span class="sxs-lookup"><span data-stu-id="1427f-117">User</span></span> | <span data-ttu-id="1427f-118">Een verwijderde Office 365-groep waarvan ze eigenaar kunt herstellen</span><span class="sxs-lookup"><span data-stu-id="1427f-118">Can restore any deleted Office 365 group that they owned</span></span> 


## <a name="view-hello-deleted-office-365-groups-that-are-available-toorestore"></a><span data-ttu-id="1427f-119">Weergave Hallo Office 365-groepen die beschikbaar toorestore zijn verwijderd</span><span class="sxs-lookup"><span data-stu-id="1427f-119">View hello deleted Office 365 groups that are available toorestore</span></span>
<span data-ttu-id="1427f-120">Hallo cmdlets volgen kan gebruikte tooview Hallo verwijderd groepen tooverify die een Hallo of toepassingsgroepen die u geïnteresseerd bent in zijn niet nog permanent verwijderd.</span><span class="sxs-lookup"><span data-stu-id="1427f-120">hello following cmdlets can be used tooview hello deleted groups tooverify that hello one or ones you're interested in have not yet been permanently purged.</span></span> <span data-ttu-id="1427f-121">Deze cmdlets deel uitmaken van Hallo [Azure AD PowerShell-module](https://www.powershellgallery.com/packages/AzureAD/).</span><span class="sxs-lookup"><span data-stu-id="1427f-121">These cmdlets are part of hello [Azure AD PowerShell module](https://www.powershellgallery.com/packages/AzureAD/).</span></span> <span data-ttu-id="1427f-122">Meer informatie over deze module vindt u in Hallo [Azure Active Directory PowerShell versie 2](/powershell/azure/install-adv2?view=azureadps-2.0) artikel.</span><span class="sxs-lookup"><span data-stu-id="1427f-122">More information about this module can be found in hello [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0) article.</span></span>

1.  <span data-ttu-id="1427f-123">Hallo volgende cmdlet toodisplay verwijderd Office 365-groepen in uw tenant die nog steeds beschikbaar toorestore zijn uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1427f-123">Run hello following cmdlet toodisplay all deleted Office 365 groups in your tenant that are still available toorestore.</span></span>
  ```
  Get-AzureADMSDeletedGroup
  ```

2.  <span data-ttu-id="1427f-124">Ook als u Hallo objectID van een specifieke groep weet (en u dit van de cmdlet Hallo in stap 1 downloaden kunt) heeft Voer Hallo volgende cmdlet tooverify die specifieke verwijderde groep Hallo niet nog is permanent verwijderd.</span><span class="sxs-lookup"><span data-stu-id="1427f-124">Alternately, if you know hello objectID of a specific group (and you can get it from hello cmdlet in step 1), run hello following cmdlet tooverify that hello specific deleted group has not yet been permanently purged.</span></span>
  ```
  Get-AzureADMSDeletedGroup –Id <objectId>
  ```



## <a name="how-toorestore-your-deleted-office-365-group"></a><span data-ttu-id="1427f-125">Hoe toorestore uw verwijderde Office 365-groep</span><span class="sxs-lookup"><span data-stu-id="1427f-125">How toorestore your deleted Office 365 group</span></span>
<span data-ttu-id="1427f-126">Zodra u hebt gecontroleerd dat die groep Hallo toorestore nog steeds beschikbaar is, moet u Hallo verwijderd groep herstellen met een Hallo stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="1427f-126">Once you have verified that hello group is still available toorestore, restore hello deleted group with one of hello following steps.</span></span> <span data-ttu-id="1427f-127">Als Hallo groep documenten, SP sites of andere permanente objecten bevat, kan het too24 uren toofully terugzetten duren een groep en de inhoud ervan.</span><span class="sxs-lookup"><span data-stu-id="1427f-127">If hello group contains documents, SP sites, or other persistent objects, it might take up too24 hours toofully restore a group and its contents.</span></span>

1.  <span data-ttu-id="1427f-128">Voer hello volgende cmdlet toorestore Hallo groep en de inhoud ervan.</span><span class="sxs-lookup"><span data-stu-id="1427f-128">Run hello following cmdlet toorestore hello group and its contents.</span></span>
  
  ```
  Restore-AzureADMSDeletedDirectoryObject –Id <objectId>
  ``` 

<span data-ttu-id="1427f-129">U kunt ook kan hello volgende cmdlet worden uitgevoerd groep voor toopermanently verwijderen Hallo verwijderd.</span><span class="sxs-lookup"><span data-stu-id="1427f-129">Alternatively, hello following cmdlet can be run toopermanently remove hello deleted group.</span></span>
  ```
  Remove-AzureADMSDeletedDirectoryObject –Id <objectId>
  ```

## <a name="how-do-you-know-this-worked"></a><span data-ttu-id="1427f-130">Hoe weet u Hiermee gewerkte?</span><span class="sxs-lookup"><span data-stu-id="1427f-130">How do you know this worked?</span></span>
<span data-ttu-id="1427f-131">tooverify dat u hebt een Office 365-groep Hallo uitvoeren is hersteld `Get-AzureADGroup –ObjectId <objectId>` cmdlet toodisplay informatie over het Hallo-groep.</span><span class="sxs-lookup"><span data-stu-id="1427f-131">tooverify that you’ve successfully restored an Office 365 group, run hello `Get-AzureADGroup –ObjectId <objectId>` cmdlet toodisplay information about hello group.</span></span> <span data-ttu-id="1427f-132">Na het terugzetten van Hallo is aanvraag voltooid:</span><span class="sxs-lookup"><span data-stu-id="1427f-132">After hello restore request is completed:</span></span>
- <span data-ttu-id="1427f-133">Hallo-groep wordt weergegeven in de linkernavigatiebalk Hallo op Exchange</span><span class="sxs-lookup"><span data-stu-id="1427f-133">hello group will appear in hello Left nav bar on Exchange</span></span>
- <span data-ttu-id="1427f-134">Hallo-plan voor Hallo groep wordt weergegeven in de Planner</span><span class="sxs-lookup"><span data-stu-id="1427f-134">hello plan for hello group will appear in Planner</span></span>
- <span data-ttu-id="1427f-135">Alle Sharepoint-sites en de bijbehorende inhoud is beschikbaar</span><span class="sxs-lookup"><span data-stu-id="1427f-135">Any Sharepoint sites and all of their contents will be available</span></span>
- <span data-ttu-id="1427f-136">Hallo groep toegankelijk zijn vanaf elke Hallo Exchange eindpunten en andere Office 365-werkbelastingen die ondersteuning bieden voor Office 365-groepen</span><span class="sxs-lookup"><span data-stu-id="1427f-136">hello group can be accessed from any of hello Exchange endpoints and other Office 365 workloads that support Office 365 groups</span></span>


## <a name="next-steps"></a><span data-ttu-id="1427f-137">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1427f-137">Next steps</span></span>
<span data-ttu-id="1427f-138">Deze artikelen bevatten aanvullende informatie over Azure Active Directory-groepen.</span><span class="sxs-lookup"><span data-stu-id="1427f-138">These articles provide additional information on Azure Active Directory groups.</span></span>

* [<span data-ttu-id="1427f-139">Zie de bestaande groepen</span><span class="sxs-lookup"><span data-stu-id="1427f-139">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="1427f-140">Instellingen van een groep beheren</span><span class="sxs-lookup"><span data-stu-id="1427f-140">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="1427f-141">Leden van een groep beheren</span><span class="sxs-lookup"><span data-stu-id="1427f-141">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="1427f-142">Lidmaatschap van een groep beheren</span><span class="sxs-lookup"><span data-stu-id="1427f-142">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="1427f-143">Dynamische regels voor gebruikers in een groep beheren</span><span class="sxs-lookup"><span data-stu-id="1427f-143">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
