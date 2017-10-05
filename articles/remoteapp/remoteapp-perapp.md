---
title: Toepassingen publiceren naar afzonderlijke gebruikers in een Azure RemoteApp-verzameling (Preview) | Microsoft Docs
description: Lees hoe u in Azure RemoteApp apps naar afzonderlijke gebruikers kunt publiceren, in plaats van afhankelijk van groepen.
services: remoteapp-preview
documentationcenter: 
author: piotrci
manager: mbaldwin
editor: 
ms.assetid: 1fd0539d-fa65-4ea5-a98e-0be0cf580690
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 11/23/2016
ms.author: piotrci
ms.openlocfilehash: c94ffffdec3e46ed08d941ee58dcf17b432e1dad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="publish-applications-to-individual-users-in-an-azure-remoteapp-collection-preview"></a><span data-ttu-id="0ca09-103">Toepassingen publiceren naar afzonderlijke gebruikers in een Azure RemoteApp-verzameling (Preview)</span><span class="sxs-lookup"><span data-stu-id="0ca09-103">Publish applications to individual users in an Azure RemoteApp collection (Preview)</span></span>
> [!IMPORTANT]
> <span data-ttu-id="0ca09-104">Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld.</span><span class="sxs-lookup"><span data-stu-id="0ca09-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="0ca09-105">Lees de [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="0ca09-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="0ca09-106">In dit artikel wordt uitgelegd hoe u toepassingen publiceert voor afzonderlijke gebruikers in een Azure RemoteApp-verzameling.</span><span class="sxs-lookup"><span data-stu-id="0ca09-106">This article explains how to publish applications to individual users in an Azure RemoteApp collection.</span></span> <span data-ttu-id="0ca09-107">Dit is nieuwe functionaliteit in Azure RemoteApp, momenteel als Private Preview-versie beschikbaar voor vroege gebruikers (alleen voor evaluatiedoeleinden).</span><span class="sxs-lookup"><span data-stu-id="0ca09-107">This is new functionality in Azure RemoteApp, currently in private preview and available only to select early adopters for evaluation purposes.</span></span>

<span data-ttu-id="0ca09-108">Oorspronkelijk konden toepassingen in Azure RemoteApp slechts op één manier worden gepubliceerd: de beheerder publiceerde apps vanuit de installatiekopie waarna ze zichtbaar waren voor alle gebruikers in de verzameling.</span><span class="sxs-lookup"><span data-stu-id="0ca09-108">Originally Azure RemoteApp enabled only one way of publishing applications: the administrator would publish apps from the image and they would be visible to all users in the collection.</span></span>

<span data-ttu-id="0ca09-109">Een veelvoorkomend scenario is het opnemen van veel toepassingen in één installatiekopie en de implementatie van één verzameling om managementkosten te verlagen.</span><span class="sxs-lookup"><span data-stu-id="0ca09-109">A common scenario is to include many applications in a single image and deploy one collection in order to reduce management costs.</span></span> <span data-ttu-id="0ca09-110">Vaak zijn niet alle toepassingen relevant voor alle gebruikers, en zouden beheerders liever apps publiceren naar afzonderlijke gebruikers, zodat deze geen onnodige toepassingen in hun toepassingsfeed zien.</span><span class="sxs-lookup"><span data-stu-id="0ca09-110">Oftentimes not all applications are relevant to all users – administrators would prefer to publish apps to individual users so they don’t see unnecessary applications in their application feed.</span></span>

<span data-ttu-id="0ca09-111">Dit is nu als een beperkte preview-functie mogelijk in Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="0ca09-111">This is now possible in Azure RemoteApp – currently as a limited preview feature.</span></span> <span data-ttu-id="0ca09-112">Hier volgt een korte samenvatting van de nieuwe functionaliteit:</span><span class="sxs-lookup"><span data-stu-id="0ca09-112">Here is a brief summary of the new functionality:</span></span>

1. <span data-ttu-id="0ca09-113">Een verzameling kan worden ingesteld op een van de volgende twee modi:</span><span class="sxs-lookup"><span data-stu-id="0ca09-113">A collection can be set into one of two modes:</span></span>
   
   * <span data-ttu-id="0ca09-114">De oorspronkelijke verzamelmodus, waarbij alle gebruikers in een verzameling alle gepubliceerde toepassingen zien.</span><span class="sxs-lookup"><span data-stu-id="0ca09-114">the original collection mode, where all users in a collection can see all published applications.</span></span> <span data-ttu-id="0ca09-115">Dit is de standaardmodus.</span><span class="sxs-lookup"><span data-stu-id="0ca09-115">This is the default mode.</span></span>
   * <span data-ttu-id="0ca09-116">De nieuwe toepassingsmodus, waarin gebruikers alleen de toepassingen zien die aan hen zijn toegewezen</span><span class="sxs-lookup"><span data-stu-id="0ca09-116">the new application mode, where users only see applications that have been explicitly assigned to them</span></span>
2. <span data-ttu-id="0ca09-117">Op het moment kan de toepassingsmodus alleen worden ingeschakeld met PowerShell-cmdlets van Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="0ca09-117">At the moment the application mode can only be enabled using Azure RemoteApp PowerShell cmdlets.</span></span>
   
   * <span data-ttu-id="0ca09-118">Als de verzameling is ingesteld op de toepassingsmodus, kan gebruikerstoewijzing in de verzameling niet worden beheerd via de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="0ca09-118">When set to application mode, user assignment in the collection cannot be managed through the Azure portal.</span></span> <span data-ttu-id="0ca09-119">Gebruikerstoewijzing moet worden beheerd via de PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="0ca09-119">User assignment has to be managed through PowerShell cmdlets.</span></span>
3. <span data-ttu-id="0ca09-120">Gebruikers zien alleen de toepassingen die rechtstreeks aan hen zijn gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="0ca09-120">Users will only see the applications published directly to them.</span></span> <span data-ttu-id="0ca09-121">Een gebruiker heeft echter nog steeds de mogelijkheid om de andere toepassingen te starten die beschikbaar zijn in de installatiekopie, door deze rechtstreeks in het besturingssysteem te starten.</span><span class="sxs-lookup"><span data-stu-id="0ca09-121">However, it may still be possible for a user to launch the other applications available on the image by accessing them directly in the operating system.</span></span>
   
   * <span data-ttu-id="0ca09-122">Deze functie biedt geen veilige vergrendeling van toepassingen maar beperkt alleen de zichtbaarheid in de toepassingsfeed.</span><span class="sxs-lookup"><span data-stu-id="0ca09-122">This feature does not provide a secure lockdown of applications; it only limits visibility in the application feed.</span></span>
   * <span data-ttu-id="0ca09-123">Als u gebruikers van toepassingen wilt isoleren, moet u daar afzonderlijke verzamelingen voor gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0ca09-123">If you need to isolate users from applications, you will need to use separate collections for that.</span></span>

## <a name="how-to-get-azure-remoteapp-powershell-cmdlets"></a><span data-ttu-id="0ca09-124">PowerShell-cmdlets van Azure RemoteApp ophalen</span><span class="sxs-lookup"><span data-stu-id="0ca09-124">How to get Azure RemoteApp PowerShell cmdlets</span></span>
<span data-ttu-id="0ca09-125">Als u de nieuwe preview-functionaliteit wilt uitproberen, moet u Azure PowerShell-cmdlets gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0ca09-125">To try the new preview functionality, you will need to use Azure PowerShell cmdlets.</span></span> <span data-ttu-id="0ca09-126">Het is momenteel niet mogelijk om de nieuwe toepassingspublicatiemodus in te schakelen met Azure Management Portal.</span><span class="sxs-lookup"><span data-stu-id="0ca09-126">It is currently not possible to use the Azure Management portal to enable the new application publishing mode.</span></span>

<span data-ttu-id="0ca09-127">Controleer eerst of de [Azure PowerShell-module](/powershell/azure/overview) is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="0ca09-127">First, make sure you have the [Azure PowerShell module](/powershell/azure/overview) installed.</span></span>

<span data-ttu-id="0ca09-128">Start daarna de PowerShell-console in de beheerdersmodus en voer de volgende cmdlet uit:</span><span class="sxs-lookup"><span data-stu-id="0ca09-128">Then launch the PowerShell console in administrator mode and run the following cmdlet:</span></span>

        Add-AzureAccount

<span data-ttu-id="0ca09-129">U wordt gevraagd naar uw Azure-gebruikersnaam en -wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="0ca09-129">It will prompt you for your Azure user name and password.</span></span> <span data-ttu-id="0ca09-130">Wanneer u bent aangemeld, kunt u Azure RemoteApp-cmdlets uitvoeren binnen uw Azure-abonnementen.</span><span class="sxs-lookup"><span data-stu-id="0ca09-130">Once signed in, you will be able to run Azure RemoteApp cmdlets against your Azure subscriptions.</span></span>

## <a name="how-to-check-which-mode-a-collection-is-in"></a><span data-ttu-id="0ca09-131">Controleren welke modus voor een verzameling is ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="0ca09-131">How to check which mode a collection is in</span></span>
<span data-ttu-id="0ca09-132">Voer de volgende cmdlet uit:</span><span class="sxs-lookup"><span data-stu-id="0ca09-132">Run the following cmdlet:</span></span>

        Get-AzureRemoteAppCollection <collectionName>

![De verzamelmodus controleren](./media/remoteapp-perapp/araacllelvel.png)

<span data-ttu-id="0ca09-134">De eigenschap AclLevel kan de volgende waarden hebben:</span><span class="sxs-lookup"><span data-stu-id="0ca09-134">The AclLevel property can have the following values:</span></span>

* <span data-ttu-id="0ca09-135">Verzameling: De oorspronkelijke publicatiemodus.</span><span class="sxs-lookup"><span data-stu-id="0ca09-135">Collection: the original publishing mode.</span></span> <span data-ttu-id="0ca09-136">Alle gebruikers zien alle gepubliceerde apps.</span><span class="sxs-lookup"><span data-stu-id="0ca09-136">All users see all published apps.</span></span>
* <span data-ttu-id="0ca09-137">Toepassing: De nieuwe publicatiemodus.</span><span class="sxs-lookup"><span data-stu-id="0ca09-137">Application: the new publishing mode.</span></span> <span data-ttu-id="0ca09-138">Gebruikers zien alleen de apps die rechtstreeks naar hen zijn gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="0ca09-138">Users see only the apps published directly to them.</span></span>

## <a name="how-to-switch-to-application-publishing-mode"></a><span data-ttu-id="0ca09-139">Overschakelen naar toepassingspublicatiemodus</span><span class="sxs-lookup"><span data-stu-id="0ca09-139">How to switch to application publishing mode</span></span>
<span data-ttu-id="0ca09-140">Voer de volgende cmdlet uit:</span><span class="sxs-lookup"><span data-stu-id="0ca09-140">Run the following cmdlet:</span></span>

        Set-AzureRemoteAppCollection -CollectionName -AclLevel Application

<span data-ttu-id="0ca09-141">Toepassingspublicatiestatus blijft behouden: in eerste instantie zien alle gebruikers alle oorspronkelijke gepubliceerde apps.</span><span class="sxs-lookup"><span data-stu-id="0ca09-141">Application publishing state will be preserved: initially all users will see all of the original published apps.</span></span>

## <a name="how-to-list-users-who-can-see-a-specific-application"></a><span data-ttu-id="0ca09-142">Een lijst weergeven van gebruikers die een specifieke toepassing kunnen zien</span><span class="sxs-lookup"><span data-stu-id="0ca09-142">How to list users who can see a specific application</span></span>
<span data-ttu-id="0ca09-143">Voer de volgende cmdlet uit:</span><span class="sxs-lookup"><span data-stu-id="0ca09-143">Run the following cmdlet:</span></span>

        Get-AzureRemoteAppUser -CollectionName <collectionName> -Alias <appAlias>

<span data-ttu-id="0ca09-144">Hiermee wordt een lijst weergegeven van alle gebruikers die de toepassing kunnen zien.</span><span class="sxs-lookup"><span data-stu-id="0ca09-144">This lists all users who can see the application.</span></span>

<span data-ttu-id="0ca09-145">Opmerking: u kunt de toepassingsaliassen (in de bovenstaande syntaxis 'app alias' genoemd) zien door Get-AzureRemoteAppProgram - CollectionName <collectionName> uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="0ca09-145">Note: You can see the application aliases (called "app alias" in the syntax above) by running Get-AzureRemoteAppProgram -CollectionName <collectionName>.</span></span>

## <a name="how-to-assign-an-application-to-a-user"></a><span data-ttu-id="0ca09-146">Een toepassing toewijzen aan een gebruiker</span><span class="sxs-lookup"><span data-stu-id="0ca09-146">How to assign an application to a user</span></span>
<span data-ttu-id="0ca09-147">Voer de volgende cmdlet uit:</span><span class="sxs-lookup"><span data-stu-id="0ca09-147">Run the following cmdlet:</span></span>

        Add-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

<span data-ttu-id="0ca09-148">De gebruiker ziet nu de toepassing in de Azure RemoteApp-client en kan hiermee verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="0ca09-148">The user will now see the application in the Azure RemoteApp client and will be able to connect to it.</span></span>

## <a name="how-to-remove-an-application-from-a-user"></a><span data-ttu-id="0ca09-149">Een toepassing verwijderen van een gebruiker</span><span class="sxs-lookup"><span data-stu-id="0ca09-149">How to remove an application from a user</span></span>
<span data-ttu-id="0ca09-150">Voer de volgende cmdlet uit:</span><span class="sxs-lookup"><span data-stu-id="0ca09-150">Run the following cmdlet:</span></span>

        Remove-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

## <a name="providing-feedback"></a><span data-ttu-id="0ca09-151">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="0ca09-151">Providing feedback</span></span>
<span data-ttu-id="0ca09-152">We waarderen uw feedback en suggesties met betrekking tot deze preview-functie.</span><span class="sxs-lookup"><span data-stu-id="0ca09-152">We appreciate your feedback and suggestions regarding this preview feature.</span></span> <span data-ttu-id="0ca09-153">Zou u de [enquête](http://www.instant.ly/s/FDdrb) willen invullen om ons te laten weten wat u ervan vindt?</span><span class="sxs-lookup"><span data-stu-id="0ca09-153">Please fill out the [survey](http://www.instant.ly/s/FDdrb) to let us know what you think.</span></span>

## <a name="havent-had-a-chance-to-try-the-preview-feature"></a><span data-ttu-id="0ca09-154">Hebt u nog geen gelegenheid gehad om de preview-functie uit te proberen?</span><span class="sxs-lookup"><span data-stu-id="0ca09-154">Haven't had a chance to try the preview feature?</span></span>
<span data-ttu-id="0ca09-155">Als u nog niet hebt deelgenomen aan de preview, kunt u deze [enquête](http://www.instant.ly/s/AY83p) gebruiken om toegang aan te vragen.</span><span class="sxs-lookup"><span data-stu-id="0ca09-155">If you have not participated in the preview yet, please use this [survey](http://www.instant.ly/s/AY83p) to request access.</span></span>

