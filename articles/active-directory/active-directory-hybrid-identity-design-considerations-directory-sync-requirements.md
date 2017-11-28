---
title: Azure Active Directory hybride identiteit ontwerpoverwegingen - directory-synchronisatievereisten bepalen | Microsoft Docs
description: Identificeren welke vereisten nodig zijn voor het synchroniseren van alle gebruikers tussen on = eigen locatie en cloud voor de onderneming.
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 593eaa71-17eb-4c16-8c98-43cc62987e65
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 5ef87e606f055359ca325befd6048353ce57ca2b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="determine-directory-synchronization-requirements"></a><span data-ttu-id="89cdd-103">Vereisten voor directory-synchronisatie bepalen</span><span class="sxs-lookup"><span data-stu-id="89cdd-103">Determine directory synchronization requirements</span></span>
<span data-ttu-id="89cdd-104">Synchronisatie is alles over een identiteit in de cloud op basis van hun on-premises identiteits zodat gebruikers beschikken.</span><span class="sxs-lookup"><span data-stu-id="89cdd-104">Synchronization is all about providing users an identity in the cloud based on their on-premises identity.</span></span> <span data-ttu-id="89cdd-105">Of ze gesynchroniseerde account wordt gebruikt voor verificatie of federatieve verificatie, of niet wordt nog steeds de gebruikers moeten een identiteit hebben in de cloud.</span><span class="sxs-lookup"><span data-stu-id="89cdd-105">Whether or not they will use synchronized account for authentication or federated authentication, the users will still need to have an identity in the cloud.</span></span>  <span data-ttu-id="89cdd-106">Deze identiteit moet worden behouden en regelmatig bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="89cdd-106">This identity will need to be maintained and updated periodically.</span></span>  <span data-ttu-id="89cdd-107">De updates kunnen vele vormen aannemen, wijzigingen van de titel aan wachtwoord te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="89cdd-107">The updates can take many forms, from title changes to password changes.</span></span>  

<span data-ttu-id="89cdd-108">Begin met het evalueren van de organisaties on-premises identity-oplossing en de gebruiker vereisten.</span><span class="sxs-lookup"><span data-stu-id="89cdd-108">Start by evaluating the organizations on-premises identity solution and user requirements.</span></span> <span data-ttu-id="89cdd-109">Deze evaluatie is belangrijk om te definiëren van de technische vereisten voor hoe gebruikers-id's worden gemaakt en onderhouden in de cloud.</span><span class="sxs-lookup"><span data-stu-id="89cdd-109">This evaluation is important to define the technical requirements for how user identities will be created and maintained in the cloud.</span></span>  <span data-ttu-id="89cdd-110">De meeste organisaties, Active Directory is lokale en de on-premises adreslijst dat gebruikers worden door gesynchroniseerd uit, maar in sommige gevallen dit niet het geval zal zijn.</span><span class="sxs-lookup"><span data-stu-id="89cdd-110">For a majority of organizations, Active Directory is on-premises and will be the on-premises directory that users will by synchronized from, however in some cases this will not be the case.</span></span>  

<span data-ttu-id="89cdd-111">Zorg ervoor dat de volgende vragen beantwoorden:</span><span class="sxs-lookup"><span data-stu-id="89cdd-111">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="89cdd-112">Hebt u één AD-forest, meerdere of geen?</span><span class="sxs-lookup"><span data-stu-id="89cdd-112">Do you have one AD forest, multiple, or none?</span></span>
  
  * <span data-ttu-id="89cdd-113">Hoeveel Azure AD-mappen wordt u synchroniseren met?</span><span class="sxs-lookup"><span data-stu-id="89cdd-113">How many Azure AD directories will you be synchronizing to?</span></span>
    
    1. <span data-ttu-id="89cdd-114">U gebruikt voor het filteren?</span><span class="sxs-lookup"><span data-stu-id="89cdd-114">Are you using filtering?</span></span>
    2. <span data-ttu-id="89cdd-115">Hebt u meerdere Azure AD Connect-servers gepland?</span><span class="sxs-lookup"><span data-stu-id="89cdd-115">Do you have multiple Azure AD Connect servers planned?</span></span>
* <span data-ttu-id="89cdd-116">Op dit moment hebt u een synchronisatie lokale hulpprogramma?</span><span class="sxs-lookup"><span data-stu-id="89cdd-116">Do you currently have a synchronization tool on-premises?</span></span>
  
  * <span data-ttu-id="89cdd-117">Zo ja, biedt uw gebruikers als gebruikers beschikken over een virtuele map/integratie van identiteiten?</span><span class="sxs-lookup"><span data-stu-id="89cdd-117">If yes, does your users if users have a virtual directory/integration of identities?</span></span>
* <span data-ttu-id="89cdd-118">Hebt u een andere directory lokale die u wilt synchroniseren (bijvoorbeeld LDAP-adreslijst, HR-database, enzovoort)?</span><span class="sxs-lookup"><span data-stu-id="89cdd-118">Do you have any other directory on-premises that you want to synchronize (e.g. LDAP Directory, HR database, etc)?</span></span>
  * <span data-ttu-id="89cdd-119">Gaat u een GALSync doen?</span><span class="sxs-lookup"><span data-stu-id="89cdd-119">Are you going to be doing any GALSync?</span></span>
  * <span data-ttu-id="89cdd-120">Wat is de huidige status van de UPN's in uw organisatie?</span><span class="sxs-lookup"><span data-stu-id="89cdd-120">What is the current state of UPNs in your organization?</span></span> 
  * <span data-ttu-id="89cdd-121">Hebt u een andere map die het authenticeren van gebruikers?</span><span class="sxs-lookup"><span data-stu-id="89cdd-121">Do you have a different directory that users authenticate against?</span></span>
  * <span data-ttu-id="89cdd-122">Maakt uw bedrijf gebruik van Microsoft Exchange?</span><span class="sxs-lookup"><span data-stu-id="89cdd-122">Does your company use Microsoft Exchange?</span></span>
    * <span data-ttu-id="89cdd-123">Wel ze van plan bent een hybride implementatie voor exchange hebben?</span><span class="sxs-lookup"><span data-stu-id="89cdd-123">Do they plan of having a hybrid exchange deployment?</span></span>

<span data-ttu-id="89cdd-124">Nu u een idee hebt over de synchronisatievereisten van uw, moet u bepalen welke hulpprogramma is het juiste project aan deze vereisten voldoet.</span><span class="sxs-lookup"><span data-stu-id="89cdd-124">Now that you have an idea about your synchronization requirements, you need to determine which tool is the correct one to meet these requirements.</span></span>  <span data-ttu-id="89cdd-125">Microsoft biedt verschillende hulpmiddelen voor het uitvoeren van Active directory-integratie en synchronisatie.</span><span class="sxs-lookup"><span data-stu-id="89cdd-125">Microsoft provides several tools to accomplish directory integration and synchronization.</span></span>  <span data-ttu-id="89cdd-126">Zie de [extra vergelijkingstabel voor hybride identiteit directory-integratie](active-directory-hybrid-identity-design-considerations-tools-comparison.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="89cdd-126">See the [Hybrid Identity directory integration tools comparison table](active-directory-hybrid-identity-design-considerations-tools-comparison.md) for more information.</span></span> 

<span data-ttu-id="89cdd-127">Nu u uw synchronisatievereisten en het hulpprogramma dat u dit voor uw bedrijf doen hebt, moet u evalueren van de toepassingen die gebruikmaken van deze directoryservices.</span><span class="sxs-lookup"><span data-stu-id="89cdd-127">Now that you have your synchronization requirements and the tool that will accomplish this for your company, you need to evaluate the applications that use these directory services.</span></span> <span data-ttu-id="89cdd-128">Deze evaluatie is belangrijk om te definiëren van de technische vereisten voor het integreren van deze toepassingen naar de cloud.</span><span class="sxs-lookup"><span data-stu-id="89cdd-128">This evaluation is important to define the technical requirements to integrate these applications to the cloud.</span></span> <span data-ttu-id="89cdd-129">Zorg ervoor dat de volgende vragen beantwoorden:</span><span class="sxs-lookup"><span data-stu-id="89cdd-129">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="89cdd-130">Deze toepassingen worden verplaatst naar de cloud en gebruikt de directory?</span><span class="sxs-lookup"><span data-stu-id="89cdd-130">Will these applications be moved to the cloud and use the directory?</span></span>
* <span data-ttu-id="89cdd-131">Zijn er speciale kenmerken die worden gesynchroniseerd met de cloud moeten, zodat deze toepassingen kunnen worden gebruikt met succes?</span><span class="sxs-lookup"><span data-stu-id="89cdd-131">Are there special attributes that need to be synchronized to the cloud so these applications can use them successfully?</span></span>
* <span data-ttu-id="89cdd-132">Deze toepassingen moet opnieuw worden geschreven om te profiteren van cloud-verificatie?</span><span class="sxs-lookup"><span data-stu-id="89cdd-132">Will these applications need to be re-written to take advantage of cloud auth?</span></span>
* <span data-ttu-id="89cdd-133">Blijven deze toepassingen lokale live terwijl gebruikers toegang krijgen tot deze met de cloudidentiteit van de?</span><span class="sxs-lookup"><span data-stu-id="89cdd-133">Will these applications continue to live on-premises while users access them using the cloud identity?</span></span>

<span data-ttu-id="89cdd-134">U moet ook de beveiliging vereisten en beperkingen adreslijstsynchronisatie bepalen.</span><span class="sxs-lookup"><span data-stu-id="89cdd-134">You also need to determine the security requirements and constraints directory synchronization.</span></span> <span data-ttu-id="89cdd-135">Deze evaluatie is belangrijk om een lijst met de vereisten die nodig zijn om te kunnen maken en beheren van gebruikers-id's in de cloud.</span><span class="sxs-lookup"><span data-stu-id="89cdd-135">This evaluation is important to get a list of the requirements that will be needed in order to create and maintain user’s identities in the cloud.</span></span> <span data-ttu-id="89cdd-136">Zorg ervoor dat de volgende vragen beantwoorden:</span><span class="sxs-lookup"><span data-stu-id="89cdd-136">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="89cdd-137">Waar de synchronisatieserver komen te staan?</span><span class="sxs-lookup"><span data-stu-id="89cdd-137">Where will the synchronization server be located?</span></span>
* <span data-ttu-id="89cdd-138">Kan het zijn verbonden met het domein?</span><span class="sxs-lookup"><span data-stu-id="89cdd-138">Will it be domain joined?</span></span>
* <span data-ttu-id="89cdd-139">De server bevindt zich in een beperkte netwerk achter een firewall, zoals een Perimeternetwerk?</span><span class="sxs-lookup"><span data-stu-id="89cdd-139">Will the server be located on a restricted network behind a firewall, such as a DMZ?</span></span>
  * <span data-ttu-id="89cdd-140">U mag de vereiste firewallpoorten ter ondersteuning van synchronisatie openen?</span><span class="sxs-lookup"><span data-stu-id="89cdd-140">Will you be able to open the required firewall ports to support synchronization?</span></span>
* <span data-ttu-id="89cdd-141">Hebt u een noodherstelplan voor de synchronisatieserver?</span><span class="sxs-lookup"><span data-stu-id="89cdd-141">Do you have a disaster recovery plan for the synchronization server?</span></span>
* <span data-ttu-id="89cdd-142">Hebt u een account met de juiste machtigingen voor alle forests die u wilt synchroniseren met?</span><span class="sxs-lookup"><span data-stu-id="89cdd-142">Do you have an account with the correct permissions for all forests you want to synch with?</span></span>
  * <span data-ttu-id="89cdd-143">Als uw bedrijf kan het antwoord voor deze vraag niet weet, Raadpleeg de sectie 'Machtigingen voor Wachtwoordsynchronisatie' in het artikel [installeren van de Azure Active Directory-synchronisatieservice](https://msdn.microsoft.com/library/azure/dn757602.aspx#BKMK_CreateAnADAccountForTheSyncService) en bepalen of u al een account met deze machtigingen hebt of als u wilt maken.</span><span class="sxs-lookup"><span data-stu-id="89cdd-143">If your company doesn’t know the answer for this question, review the section “Permissions for password synchronization” in the article [Install the Azure Active Directory Sync Service](https://msdn.microsoft.com/library/azure/dn757602.aspx#BKMK_CreateAnADAccountForTheSyncService) and determine if you already have an account with these permissions or if you need to create one.</span></span>
* <span data-ttu-id="89cdd-144">Als u synchronisatie zijn forest kan de synchronisatieserver ophalen voor elk forest?</span><span class="sxs-lookup"><span data-stu-id="89cdd-144">If you have mutli-forest sync is the sync server able to get to each forest?</span></span>

> [!NOTE]
> <span data-ttu-id="89cdd-145">Zorg ervoor dat elk antwoord noteert de logica achter het antwoord begrijpt.</span><span class="sxs-lookup"><span data-stu-id="89cdd-145">Make sure to take notes of each answer and understand the rationale behind the answer.</span></span> <span data-ttu-id="89cdd-146">[Vereisten voor respons op incidenten bepalen](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) gaat over de beschikbare opties.</span><span class="sxs-lookup"><span data-stu-id="89cdd-146">[Determine incident response requirements](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) will go over the options available.</span></span> <span data-ttu-id="89cdd-147">Moet door deze vragen die u selecteert welke optie het beste past bij uw bedrijf te beantwoorden.</span><span class="sxs-lookup"><span data-stu-id="89cdd-147">By having answered those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="89cdd-148">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="89cdd-148">Next steps</span></span>
[<span data-ttu-id="89cdd-149">Vereisten multi-factor authentication bepalen</span><span class="sxs-lookup"><span data-stu-id="89cdd-149">Determine multi-factor authentication requirements</span></span>](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md)

## <a name="see-also"></a><span data-ttu-id="89cdd-150">Zie ook</span><span class="sxs-lookup"><span data-stu-id="89cdd-150">See also</span></span>
[<span data-ttu-id="89cdd-151">Overzicht ontwerpoverwegingen</span><span class="sxs-lookup"><span data-stu-id="89cdd-151">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

