---
title: aaaUse PowerShell-cmdlets met Azure RemoteApp | Microsoft Docs
description: Meer informatie over hoe toouse Windows PowerShell-cmdlets in Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: guscatalano
manager: mbaldwin
editor: 
ms.assetid: 7d3d5ded-6f73-4de6-a8ac-c1d622e842a2
ms.service: remoteapp
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: a09cae2093e2c3a4a2ed673b5d148a22ceb935f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-windows-powershell-cmdlets-with-azure-remoteapp"></a><span data-ttu-id="ad89f-103">Windows PowerShell-cmdlets gebruiken met Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="ad89f-103">Use Windows PowerShell cmdlets with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ad89f-104">Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld.</span><span class="sxs-lookup"><span data-stu-id="ad89f-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="ad89f-105">Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ad89f-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

 <span data-ttu-id="ad89f-106">U kunt hello Azure RemoteApp-PowerShell-cmdlets tooadminister gebruiken en onderhouden van uw verzamelingen.</span><span class="sxs-lookup"><span data-stu-id="ad89f-106">You can use hello Azure RemoteApp PowerShell cmdlets tooadminister and maintain your collections.</span></span> <span data-ttu-id="ad89f-107">Hallo informatie tooget gestart na gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ad89f-107">Use hello following information tooget started.</span></span>

## <a name="get-hello-cmdlets"></a><span data-ttu-id="ad89f-108">Hallo-cmdlets ophalen</span><span class="sxs-lookup"><span data-stu-id="ad89f-108">Get hello cmdlets</span></span>
- - -
<span data-ttu-id="ad89f-109">Eerst hello Azure Powershell-cmdlets downloaden [hier](http://go.microsoft.com/?linkid=9811175), Hallo RemoteApp-cmdlets in is opgenomen.</span><span class="sxs-lookup"><span data-stu-id="ad89f-109">First download hello Azure Powershell cmdlets [here](http://go.microsoft.com/?linkid=9811175), hello RemoteApp cmdlets are included in it.</span></span> 

<span data-ttu-id="ad89f-110">Bekijk Hallo [help van cmdlet voor Azure RemoteApp](/powershell/module/azure?view=azuresmps-3.7.0).</span><span class="sxs-lookup"><span data-stu-id="ad89f-110">Check out hello [Azure RemoteApp cmdlet help](/powershell/module/azure?view=azuresmps-3.7.0).</span></span>

## <a name="configure-azure-cmdlets-toouse-your-subscription"></a><span data-ttu-id="ad89f-111">Uw abonnement voor Azure-cmdlets toouse configureren</span><span class="sxs-lookup"><span data-stu-id="ad89f-111">Configure Azure cmdlets toouse your subscription</span></span>
- - -
<span data-ttu-id="ad89f-112">Ga als volgt [in deze handleiding](/powershell/azure/overview) zodat u Hallo-cmdlets op basis van uw Azure-abonnement gebruiken kunt.</span><span class="sxs-lookup"><span data-stu-id="ad89f-112">Follow [this guide](/powershell/azure/overview) so you can use hello cmdlets against your Azure subscription.</span></span>

<span data-ttu-id="ad89f-113">U kunt deze stappen tooget snel aan de slag:</span><span class="sxs-lookup"><span data-stu-id="ad89f-113">You can use these steps tooget started quickly:</span></span>

1. <span data-ttu-id="ad89f-114">Download en installeer Hallo [Azure PowerShell-cmdlets](http://go.microsoft.com/?linkid=9811175).</span><span class="sxs-lookup"><span data-stu-id="ad89f-114">Download and install hello [Azure PowerShell cmdlets](http://go.microsoft.com/?linkid=9811175).</span></span>
2. <span data-ttu-id="ad89f-115">Start Microsoft Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ad89f-115">Launch Microsoft Azure PowerShell.</span></span>
3. <span data-ttu-id="ad89f-116">Voer **Add-AzureAccount** tooauthenticate tooyour Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="ad89f-116">Run **Add-AzureAccount** tooauthenticate tooyour Azure subscription.</span></span> <span data-ttu-id="ad89f-117">Wanneer u wordt gevraagd, typt u Hallo dezelfde gebruikersnaam en wachtwoord toosign in tooAzure portal te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ad89f-117">When prompted, enter hello same user name and password that you use toosign in tooAzure portal.</span></span>  
4. <span data-ttu-id="ad89f-118">Voer **Get-AzureSubscription** toolist Hallo abonnementen die zijn gekoppeld aan uw gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="ad89f-118">Run **Get-AzureSubscription** toolist hello subscriptions associated with your user account.</span></span> 
5. <span data-ttu-id="ad89f-119">Voer **Select-AzureSubscription - SubscriptionName &lt;abonnementsnaam&gt;**  of **Select-AzureSubscription - SubscriptionId &lt;abonnements-ID&gt;**  toospecify Hallo abonnement toouse.</span><span class="sxs-lookup"><span data-stu-id="ad89f-119">Run **Select-AzureSubscription -SubscriptionName &lt;subscription name&gt;** or **Select-AzureSubscription -SubscriptionId &lt;subscription ID&gt;** toospecify hello subscription toouse.</span></span>

<span data-ttu-id="ad89f-120">Gefeliciteerd, uw Azure PowerShell-console is geconfigureerd en klaar toouse.</span><span class="sxs-lookup"><span data-stu-id="ad89f-120">Congratulations, your Azure PowerShell console is configured and ready toouse.</span></span> <span data-ttu-id="ad89f-121">Let erop dat u moet toorepeate stappen 2 t/m 5 telkens wanneer die u Hallo hello Azure PowerShell-console start.</span><span class="sxs-lookup"><span data-stu-id="ad89f-121">Be aware that you'll need toorepeate steps 2 through 5 each time you start hello hello Azure PowerShell console.</span></span>  


## <a name="list-all-collections"></a><span data-ttu-id="ad89f-122">Lijst van alle verzamelingen</span><span class="sxs-lookup"><span data-stu-id="ad89f-122">List all collections</span></span>
- - -
     <span data-ttu-id="ad89f-123">Get-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="ad89f-123">Get-AzureRemoteAppCollection</span></span>

## <a name="delete-a-collection"></a><span data-ttu-id="ad89f-124">Een verzameling verwijderen</span><span class="sxs-lookup"><span data-stu-id="ad89f-124">Delete a collection</span></span>
- - -
    <span data-ttu-id="ad89f-125">Verwijder AzureRemoteAppCollection<enter collection name></span><span class="sxs-lookup"><span data-stu-id="ad89f-125">Remove-AzureRemoteAppCollection <enter collection name></span></span>

<span data-ttu-id="ad89f-126">Voorbeeld: `Remove-AzureRemoteAppCollection ContosoProduction`.</span><span class="sxs-lookup"><span data-stu-id="ad89f-126">Example:  `Remove-AzureRemoteAppCollection ContosoProduction`.</span></span>

## <a name="create-a-cloud-collection"></a><span data-ttu-id="ad89f-127">Een cloudverzameling maken</span><span class="sxs-lookup"><span data-stu-id="ad89f-127">Create a cloud collection</span></span>
- - -
<span data-ttu-id="ad89f-128">Het is eenvoudig, Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="ad89f-128">It's simple, run hello following command:</span></span>

    New-AzureRemoteAppCollection -Collectionname RAppO365Col1 -ImageName "Office 365 ProPlus (Subscription required)" -Plan Basic -Location "West US" - Description "Office 365 Collection."

<span data-ttu-id="ad89f-129">Hallo hierboven opdracht publiceert automatisch Microsoft Office 365-toepassingen (Excel, OneNote, Outlook, PowerPoint, Visio en Word).</span><span class="sxs-lookup"><span data-stu-id="ad89f-129">hello above command automatically publishes Microsoft Office 365 applications (Excel, OneNote, Outlook, PowerPoint, Visio and Word).</span></span>

<span data-ttu-id="ad89f-130">Maken van een siteverzameling duurt 30 minuten of langer toocomplete.</span><span class="sxs-lookup"><span data-stu-id="ad89f-130">Collection creation can take 30 minutes or longer toocomplete.</span></span> <span data-ttu-id="ad89f-131">Deze opdracht retourneert daarom een tracerings-ID die u kunt als volgt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="ad89f-131">Therefore, this command returns a tracking ID that you can use as follows:</span></span>

    Get-AzureRemoteAppOperationResult -TrackingId xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

<span data-ttu-id="ad89f-132">Nadat Hallo verzameling is voltooid, kunt u gebruikers toohello verzameling kunt toevoegen met de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="ad89f-132">After hello collection is done, you can add users toohello collection with hello following command:</span></span>

    Add-AzureRemoteAppUser -CollectionName RAppO365Col1 -Type microsoftAccount -UserUpn someone@domain.com

<span data-ttu-id="ad89f-133">En u klaar bent!</span><span class="sxs-lookup"><span data-stu-id="ad89f-133">And you're done!</span></span> <span data-ttu-id="ad89f-134">Deze gebruiker moet kunnen tooconnect toohello toepassing hello Azure RemoteApp-client gevonden met [hier](https://www.remoteapp.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="ad89f-134">That user should be able tooconnect toohello application using hello Azure RemoteApp client found [here](https://www.remoteapp.windowsazure.com/).</span></span>

## <a name="available-cmdlets"></a><span data-ttu-id="ad89f-135">Beschikbare cmdlets</span><span class="sxs-lookup"><span data-stu-id="ad89f-135">Available cmdlets</span></span>
<span data-ttu-id="ad89f-136">Er zijn veel andere opdrachten die we hebben, Hallo-documentatie voor ze is binnenkort binnenkort:</span><span class="sxs-lookup"><span data-stu-id="ad89f-136">There are lots of other commands that we have, hello documentation for them will be coming shortly:</span></span>

<span data-ttu-id="ad89f-137">Basic RemoteApp-collectie cmdlets:</span><span class="sxs-lookup"><span data-stu-id="ad89f-137">Basic RemoteApp Collection cmdlets:</span></span> 

* <span data-ttu-id="ad89f-138">New-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="ad89f-138">New-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="ad89f-139">Get-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="ad89f-139">Get-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="ad89f-140">Set-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="ad89f-140">Set-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="ad89f-141">Update-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="ad89f-141">Update-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="ad89f-142">Remove-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="ad89f-142">Remove-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="ad89f-143">Add-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="ad89f-143">Add-AzureRemoteAppUser</span></span>
* <span data-ttu-id="ad89f-144">Get-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="ad89f-144">Get-AzureRemoteAppUser</span></span>
* <span data-ttu-id="ad89f-145">Remove-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="ad89f-145">Remove-AzureRemoteAppUser</span></span>
* <span data-ttu-id="ad89f-146">Get-AzureRemoteAppSession</span><span class="sxs-lookup"><span data-stu-id="ad89f-146">Get-AzureRemoteAppSession</span></span>
* <span data-ttu-id="ad89f-147">Disconnect-AzureRemoteAppSession</span><span class="sxs-lookup"><span data-stu-id="ad89f-147">Disconnect-AzureRemoteAppSession</span></span>
* <span data-ttu-id="ad89f-148">Invoke-AzureRemoteAppSessionLogoff</span><span class="sxs-lookup"><span data-stu-id="ad89f-148">Invoke-AzureRemoteAppSessionLogoff</span></span>
* <span data-ttu-id="ad89f-149">Send-AzureRemoteAppSessionMessage</span><span class="sxs-lookup"><span data-stu-id="ad89f-149">Send-AzureRemoteAppSessionMessage</span></span>
* <span data-ttu-id="ad89f-150">Get-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="ad89f-150">Get-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="ad89f-151">Get-AzureRemoteAppStartMenuProgram</span><span class="sxs-lookup"><span data-stu-id="ad89f-151">Get-AzureRemoteAppStartMenuProgram</span></span>
* <span data-ttu-id="ad89f-152">Publish-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="ad89f-152">Publish-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="ad89f-153">Unpublish-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="ad89f-153">Unpublish-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="ad89f-154">Get-AzureRemoteAppCollectionUsageDetails</span><span class="sxs-lookup"><span data-stu-id="ad89f-154">Get-AzureRemoteAppCollectionUsageDetails</span></span>
* <span data-ttu-id="ad89f-155">Get-AzureRemoteAppCollectionUsageSummary</span><span class="sxs-lookup"><span data-stu-id="ad89f-155">Get-AzureRemoteAppCollectionUsageSummary</span></span>
* <span data-ttu-id="ad89f-156">Get-AzureRemoteAppPlan</span><span class="sxs-lookup"><span data-stu-id="ad89f-156">Get-AzureRemoteAppPlan</span></span>

<span data-ttu-id="ad89f-157">RemoteApp-cmdlets voor virtueel netwerk:</span><span class="sxs-lookup"><span data-stu-id="ad89f-157">RemoteApp virtual network cmdlets:</span></span>

* <span data-ttu-id="ad89f-158">New-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="ad89f-158">New-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="ad89f-159">Get-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="ad89f-159">Get-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="ad89f-160">Set-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="ad89f-160">Set-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="ad89f-161">Remove-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="ad89f-161">Remove-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="ad89f-162">Get-AzureRemoteAppVpnDevice</span><span class="sxs-lookup"><span data-stu-id="ad89f-162">Get-AzureRemoteAppVpnDevice</span></span>
* <span data-ttu-id="ad89f-163">Get--AzureRemoteAppVpnDeviceConfigScript</span><span class="sxs-lookup"><span data-stu-id="ad89f-163">Get-- AzureRemoteAppVpnDeviceConfigScript</span></span>
* <span data-ttu-id="ad89f-164">Reset-AzureRemoteAppVpnSharedKey</span><span class="sxs-lookup"><span data-stu-id="ad89f-164">Reset-AzureRemoteAppVpnSharedKey</span></span>

<span data-ttu-id="ad89f-165">RemoteApp-sjabloon installatiekopie cmdlets:</span><span class="sxs-lookup"><span data-stu-id="ad89f-165">RemoteApp template image cmdlets:</span></span>

* <span data-ttu-id="ad89f-166">New-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="ad89f-166">New-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="ad89f-167">Get-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="ad89f-167">Get-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="ad89f-168">Rename-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="ad89f-168">Rename-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="ad89f-169">Remove-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="ad89f-169">Remove-AzureRemoteAppTemplateImage</span></span>

<span data-ttu-id="ad89f-170">Andere RemoteApp-cmdlets:</span><span class="sxs-lookup"><span data-stu-id="ad89f-170">Other RemoteApp cmdlets:</span></span>

* <span data-ttu-id="ad89f-171">Get-AzureRemoteAppLocation</span><span class="sxs-lookup"><span data-stu-id="ad89f-171">Get-AzureRemoteAppLocation</span></span>
* <span data-ttu-id="ad89f-172">Get-AzureRemoteAppWorkspace</span><span class="sxs-lookup"><span data-stu-id="ad89f-172">Get-AzureRemoteAppWorkspace</span></span>
* <span data-ttu-id="ad89f-173">Set-AzureRemoteAppWorkspace</span><span class="sxs-lookup"><span data-stu-id="ad89f-173">Set-AzureRemoteAppWorkspace</span></span>
* <span data-ttu-id="ad89f-174">Get-AzureRemoteAppOperationResult</span><span class="sxs-lookup"><span data-stu-id="ad89f-174">Get-AzureRemoteAppOperationResult</span></span>

