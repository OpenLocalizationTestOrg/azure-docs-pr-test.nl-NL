---
title: aaaPublish toepassingen tooindividual gebruikers in een Azure RemoteApp-verzameling (Preview) | Microsoft Docs
description: Meer informatie over hoe u apps tooindividual gebruikers, in plaats van kunt publiceren, afhankelijk van groepen in Azure RemoteApp.
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
ms.openlocfilehash: 87b435552ddbfc2c6d03aeb01d95a44985e71f9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-tooindividual-users-in-an-azure-remoteapp-collection-preview"></a><span data-ttu-id="56279-103">Publiceren van toepassingen tooindividual gebruikers in een Azure RemoteApp-verzameling (Preview)</span><span class="sxs-lookup"><span data-stu-id="56279-103">Publish applications tooindividual users in an Azure RemoteApp collection (Preview)</span></span>
> [!IMPORTANT]
> <span data-ttu-id="56279-104">Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld.</span><span class="sxs-lookup"><span data-stu-id="56279-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="56279-105">Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="56279-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="56279-106">Dit artikel wordt uitgelegd hoe toopublish toepassingen tooindividual gebruikers in een Azure RemoteApp-verzameling.</span><span class="sxs-lookup"><span data-stu-id="56279-106">This article explains how toopublish applications tooindividual users in an Azure RemoteApp collection.</span></span> <span data-ttu-id="56279-107">Dit is nieuwe functionaliteit in Azure RemoteApp, momenteel in Preview-versie private en vroege gebruikers beschikbaar alleen tooselect voor evaluatiedoeleinden.</span><span class="sxs-lookup"><span data-stu-id="56279-107">This is new functionality in Azure RemoteApp, currently in private preview and available only tooselect early adopters for evaluation purposes.</span></span>

<span data-ttu-id="56279-108">Oorspronkelijk Azure RemoteApp slechts op één manier van publicatie van toepassingen ingeschakeld: Hallo beheerder publiceerde apps vanuit Hallo installatiekopie waarna ze zichtbaar tooall gebruikers in Hallo-verzameling.</span><span class="sxs-lookup"><span data-stu-id="56279-108">Originally Azure RemoteApp enabled only one way of publishing applications: hello administrator would publish apps from hello image and they would be visible tooall users in hello collection.</span></span>

<span data-ttu-id="56279-109">Een gebruikelijk scenario is tooinclude veel toepassingen in één installatiekopie en het implementeren van een verzameling in volgorde tooreduce beheerkosten.</span><span class="sxs-lookup"><span data-stu-id="56279-109">A common scenario is tooinclude many applications in a single image and deploy one collection in order tooreduce management costs.</span></span> <span data-ttu-id="56279-110">Vaak zijn niet alle toepassingen zijn relevante tooall gebruikers – beheerders liever toopublish apps tooindividual gebruikers zodat ze geen onnodige toepassingen in hun toepassingsfeed zien.</span><span class="sxs-lookup"><span data-stu-id="56279-110">Oftentimes not all applications are relevant tooall users – administrators would prefer toopublish apps tooindividual users so they don’t see unnecessary applications in their application feed.</span></span>

<span data-ttu-id="56279-111">Dit is nu als een beperkte preview-functie mogelijk in Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="56279-111">This is now possible in Azure RemoteApp – currently as a limited preview feature.</span></span> <span data-ttu-id="56279-112">Hier volgt een korte samenvatting van de nieuwe functionaliteit Hallo:</span><span class="sxs-lookup"><span data-stu-id="56279-112">Here is a brief summary of hello new functionality:</span></span>

1. <span data-ttu-id="56279-113">Een verzameling kan worden ingesteld op een van de volgende twee modi:</span><span class="sxs-lookup"><span data-stu-id="56279-113">A collection can be set into one of two modes:</span></span>
   
   * <span data-ttu-id="56279-114">Hallo oorspronkelijke Verzamelmodus alle gebruikers in een verzameling zien gepubliceerde alle toepassingen.</span><span class="sxs-lookup"><span data-stu-id="56279-114">hello original collection mode, where all users in a collection can see all published applications.</span></span> <span data-ttu-id="56279-115">Dit is de standaardmodus Hallo.</span><span class="sxs-lookup"><span data-stu-id="56279-115">This is hello default mode.</span></span>
   * <span data-ttu-id="56279-116">Hallo nieuwe toepassingsmodus, waar gebruikers alleen de toepassingen zien die expliciet zijn toegewezen toothem</span><span class="sxs-lookup"><span data-stu-id="56279-116">hello new application mode, where users only see applications that have been explicitly assigned toothem</span></span>
2. <span data-ttu-id="56279-117">Hallo momenteel kan Hallo toepassingsmodus alleen worden ingeschakeld met behulp van Azure RemoteApp-PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="56279-117">At hello moment hello application mode can only be enabled using Azure RemoteApp PowerShell cmdlets.</span></span>
   
   * <span data-ttu-id="56279-118">Wanneer de modus instellen voor tooapplication, Gebruikerstoewijzing in Hallo verzameling kan niet worden beheerd via hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="56279-118">When set tooapplication mode, user assignment in hello collection cannot be managed through hello Azure portal.</span></span> <span data-ttu-id="56279-119">Gebruikerstoewijzing heeft toobe beheerd via de PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="56279-119">User assignment has toobe managed through PowerShell cmdlets.</span></span>
3. <span data-ttu-id="56279-120">Gebruikers zien alleen Hallo toepassingen rechtstreeks toothem gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="56279-120">Users will only see hello applications published directly toothem.</span></span> <span data-ttu-id="56279-121">Echter nog steeds mogelijk voor een gebruiker toolaunch andere toepassingen die beschikbaar zijn op de installatiekopie Hallo Hallo door deze rechtstreeks in Hallo-besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="56279-121">However, it may still be possible for a user toolaunch hello other applications available on hello image by accessing them directly in hello operating system.</span></span>
   
   * <span data-ttu-id="56279-122">Deze functie biedt geen veilige vergrendeling van toepassingen. beperkt alleen de zichtbaarheid in Hallo toepassingsfeed.</span><span class="sxs-lookup"><span data-stu-id="56279-122">This feature does not provide a secure lockdown of applications; it only limits visibility in hello application feed.</span></span>
   * <span data-ttu-id="56279-123">Als u gebruikers tooisolate van toepassingen moet, moet u toouse afzonderlijke verzamelingen voor die.</span><span class="sxs-lookup"><span data-stu-id="56279-123">If you need tooisolate users from applications, you will need toouse separate collections for that.</span></span>

## <a name="how-tooget-azure-remoteapp-powershell-cmdlets"></a><span data-ttu-id="56279-124">Hoe tooget Azure RemoteApp-PowerShell-cmdlets</span><span class="sxs-lookup"><span data-stu-id="56279-124">How tooget Azure RemoteApp PowerShell cmdlets</span></span>
<span data-ttu-id="56279-125">tootry hello nieuwe preview-functionaliteit, moet u toouse Azure PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="56279-125">tootry hello new preview functionality, you will need toouse Azure PowerShell cmdlets.</span></span> <span data-ttu-id="56279-126">Het is momenteel niet mogelijk toouse hello Azure Management portal tooenable Hallo nieuwe toepassingspublicatiemodus.</span><span class="sxs-lookup"><span data-stu-id="56279-126">It is currently not possible toouse hello Azure Management portal tooenable hello new application publishing mode.</span></span>

<span data-ttu-id="56279-127">Controleer eerst of er Hallo [Azure PowerShell-module](/powershell/azure/overview) geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="56279-127">First, make sure you have hello [Azure PowerShell module](/powershell/azure/overview) installed.</span></span>

<span data-ttu-id="56279-128">Start vervolgens Hallo PowerShell-console in de beheerdersmodus en Voer Hallo volgende cmdlet:</span><span class="sxs-lookup"><span data-stu-id="56279-128">Then launch hello PowerShell console in administrator mode and run hello following cmdlet:</span></span>

        Add-AzureAccount

<span data-ttu-id="56279-129">U wordt gevraagd naar uw Azure-gebruikersnaam en -wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="56279-129">It will prompt you for your Azure user name and password.</span></span> <span data-ttu-id="56279-130">Nadat u bent aangemeld, kunt u zich kunt toorun Azure RemoteApp-cmdlets op basis van uw Azure-abonnementen.</span><span class="sxs-lookup"><span data-stu-id="56279-130">Once signed in, you will be able toorun Azure RemoteApp cmdlets against your Azure subscriptions.</span></span>

## <a name="how-toocheck-which-mode-a-collection-is-in"></a><span data-ttu-id="56279-131">Hoe toocheck welke modus een verzameling bevindt zich in</span><span class="sxs-lookup"><span data-stu-id="56279-131">How toocheck which mode a collection is in</span></span>
<span data-ttu-id="56279-132">Voer Hallo volgende cmdlet:</span><span class="sxs-lookup"><span data-stu-id="56279-132">Run hello following cmdlet:</span></span>

        Get-AzureRemoteAppCollection <collectionName>

![Hallo Verzamelmodus controleren](./media/remoteapp-perapp/araacllelvel.png)

<span data-ttu-id="56279-134">Hallo eigenschap AclLevel kan Hallo volgende waarden hebben:</span><span class="sxs-lookup"><span data-stu-id="56279-134">hello AclLevel property can have hello following values:</span></span>

* <span data-ttu-id="56279-135">Verzameling: Hallo oorspronkelijke publicatiemodus.</span><span class="sxs-lookup"><span data-stu-id="56279-135">Collection: hello original publishing mode.</span></span> <span data-ttu-id="56279-136">Alle gebruikers zien alle gepubliceerde apps.</span><span class="sxs-lookup"><span data-stu-id="56279-136">All users see all published apps.</span></span>
* <span data-ttu-id="56279-137">Toepassing: Hallo nieuwe publicatiemodus.</span><span class="sxs-lookup"><span data-stu-id="56279-137">Application: hello new publishing mode.</span></span> <span data-ttu-id="56279-138">Gebruikers zien alleen de apps Hallo rechtstreeks toothem gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="56279-138">Users see only hello apps published directly toothem.</span></span>

## <a name="how-tooswitch-tooapplication-publishing-mode"></a><span data-ttu-id="56279-139">Hoe tooswitch tooapplication publicatiemodus</span><span class="sxs-lookup"><span data-stu-id="56279-139">How tooswitch tooapplication publishing mode</span></span>
<span data-ttu-id="56279-140">Voer Hallo volgende cmdlet:</span><span class="sxs-lookup"><span data-stu-id="56279-140">Run hello following cmdlet:</span></span>

        Set-AzureRemoteAppCollection -CollectionName -AclLevel Application

<span data-ttu-id="56279-141">Toepassingspublicatiestatus blijft behouden: in eerste instantie zien alle gebruikers alle oorspronkelijke gepubliceerde apps Hallo.</span><span class="sxs-lookup"><span data-stu-id="56279-141">Application publishing state will be preserved: initially all users will see all of hello original published apps.</span></span>

## <a name="how-toolist-users-who-can-see-a-specific-application"></a><span data-ttu-id="56279-142">Hoe toolist-gebruikers die een specifieke toepassing kunnen zien</span><span class="sxs-lookup"><span data-stu-id="56279-142">How toolist users who can see a specific application</span></span>
<span data-ttu-id="56279-143">Voer Hallo volgende cmdlet:</span><span class="sxs-lookup"><span data-stu-id="56279-143">Run hello following cmdlet:</span></span>

        Get-AzureRemoteAppUser -CollectionName <collectionName> -Alias <appAlias>

<span data-ttu-id="56279-144">Hiermee worden alle gebruikers die de toepassing hello kunnen zien.</span><span class="sxs-lookup"><span data-stu-id="56279-144">This lists all users who can see hello application.</span></span>

<span data-ttu-id="56279-145">Opmerking: U kunt Hallo toepassingsaliassen ('app alias' in de bovenstaande syntaxis voor Hallo genoemd) zien door het uitvoeren van Get-AzureRemoteAppProgram - CollectionName <collectionName>.</span><span class="sxs-lookup"><span data-stu-id="56279-145">Note: You can see hello application aliases (called "app alias" in hello syntax above) by running Get-AzureRemoteAppProgram -CollectionName <collectionName>.</span></span>

## <a name="how-tooassign-an-application-tooa-user"></a><span data-ttu-id="56279-146">Hoe een gebruiker van toepassing tooa tooassign</span><span class="sxs-lookup"><span data-stu-id="56279-146">How tooassign an application tooa user</span></span>
<span data-ttu-id="56279-147">Voer Hallo volgende cmdlet:</span><span class="sxs-lookup"><span data-stu-id="56279-147">Run hello following cmdlet:</span></span>

        Add-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

<span data-ttu-id="56279-148">Hallo gebruiker ziet nu de toepassing hello in hello Azure RemoteApp-client en kunnen tooconnect tooit zijn.</span><span class="sxs-lookup"><span data-stu-id="56279-148">hello user will now see hello application in hello Azure RemoteApp client and will be able tooconnect tooit.</span></span>

## <a name="how-tooremove-an-application-from-a-user"></a><span data-ttu-id="56279-149">Hoe een toepassing van een gebruiker tooremove</span><span class="sxs-lookup"><span data-stu-id="56279-149">How tooremove an application from a user</span></span>
<span data-ttu-id="56279-150">Voer Hallo volgende cmdlet:</span><span class="sxs-lookup"><span data-stu-id="56279-150">Run hello following cmdlet:</span></span>

        Remove-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

## <a name="providing-feedback"></a><span data-ttu-id="56279-151">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="56279-151">Providing feedback</span></span>
<span data-ttu-id="56279-152">We waarderen uw feedback en suggesties met betrekking tot deze preview-functie.</span><span class="sxs-lookup"><span data-stu-id="56279-152">We appreciate your feedback and suggestions regarding this preview feature.</span></span> <span data-ttu-id="56279-153">Vul Hallo [enquête](http://www.instant.ly/s/FDdrb) toolet ons weten wat u denkt.</span><span class="sxs-lookup"><span data-stu-id="56279-153">Please fill out hello [survey](http://www.instant.ly/s/FDdrb) toolet us know what you think.</span></span>

## <a name="havent-had-a-chance-tootry-hello-preview-feature"></a><span data-ttu-id="56279-154">Dit nog niet hebt gehad kans tootry Hallo preview-functie?</span><span class="sxs-lookup"><span data-stu-id="56279-154">Haven't had a chance tootry hello preview feature?</span></span>
<span data-ttu-id="56279-155">Als u nog niet hebt deelgenomen Hallo Preview nog, gebruik dit [enquête](http://www.instant.ly/s/AY83p) toorequest toegang.</span><span class="sxs-lookup"><span data-stu-id="56279-155">If you have not participated in hello preview yet, please use this [survey](http://www.instant.ly/s/AY83p) toorequest access.</span></span>

