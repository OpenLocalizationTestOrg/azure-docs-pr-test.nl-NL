---
title: PowerShell-cmdlets gebruiken met Azure RemoteApp | Microsoft Docs
description: Informatie over het gebruik van Windows PowerShell-cmdlets in Azure RemoteApp.
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
ms.openlocfilehash: 699b20a4dadd4ecaff57e2cc80355fe545360663
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="use-windows-powershell-cmdlets-with-azure-remoteapp"></a><span data-ttu-id="3ef97-103">Windows PowerShell-cmdlets gebruiken met Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="3ef97-103">Use Windows PowerShell cmdlets with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3ef97-104">Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld.</span><span class="sxs-lookup"><span data-stu-id="3ef97-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="3ef97-105">Lees de [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3ef97-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

 <span data-ttu-id="3ef97-106">U kunt de Azure RemoteApp-PowerShell-cmdlets gebruiken voor het beheren en onderhouden van uw verzamelingen.</span><span class="sxs-lookup"><span data-stu-id="3ef97-106">You can use the Azure RemoteApp PowerShell cmdlets to administer and maintain your collections.</span></span> <span data-ttu-id="3ef97-107">Gebruik de volgende informatie om te beginnen.</span><span class="sxs-lookup"><span data-stu-id="3ef97-107">Use the following information to get started.</span></span>

## <a name="get-the-cmdlets"></a><span data-ttu-id="3ef97-108">De cmdlets ophalen</span><span class="sxs-lookup"><span data-stu-id="3ef97-108">Get the cmdlets</span></span>
- - -
<span data-ttu-id="3ef97-109">Downloadt u eerst de Azure Powershell-cmdlets [hier](http://go.microsoft.com/?linkid=9811175), de RemoteApp-cmdlets in is opgenomen.</span><span class="sxs-lookup"><span data-stu-id="3ef97-109">First download the Azure Powershell cmdlets [here](http://go.microsoft.com/?linkid=9811175), the RemoteApp cmdlets are included in it.</span></span> 

<span data-ttu-id="3ef97-110">Bekijk de [help van cmdlet voor Azure RemoteApp](/powershell/module/azure?view=azuresmps-3.7.0).</span><span class="sxs-lookup"><span data-stu-id="3ef97-110">Check out the [Azure RemoteApp cmdlet help](/powershell/module/azure?view=azuresmps-3.7.0).</span></span>

## <a name="configure-azure-cmdlets-to-use-your-subscription"></a><span data-ttu-id="3ef97-111">Azure-cmdlets voor het gebruik van uw abonnement configureren</span><span class="sxs-lookup"><span data-stu-id="3ef97-111">Configure Azure cmdlets to use your subscription</span></span>
- - -
<span data-ttu-id="3ef97-112">Ga als volgt [in deze handleiding](/powershell/azure/overview) zodat u de cmdlets op basis van uw Azure-abonnement gebruiken kunt.</span><span class="sxs-lookup"><span data-stu-id="3ef97-112">Follow [this guide](/powershell/azure/overview) so you can use the cmdlets against your Azure subscription.</span></span>

<span data-ttu-id="3ef97-113">Volg deze stappen kunt u snel aan de slag:</span><span class="sxs-lookup"><span data-stu-id="3ef97-113">You can use these steps to get started quickly:</span></span>

1. <span data-ttu-id="3ef97-114">Download en installeer de [Azure PowerShell-cmdlets](http://go.microsoft.com/?linkid=9811175).</span><span class="sxs-lookup"><span data-stu-id="3ef97-114">Download and install the [Azure PowerShell cmdlets](http://go.microsoft.com/?linkid=9811175).</span></span>
2. <span data-ttu-id="3ef97-115">Start Microsoft Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3ef97-115">Launch Microsoft Azure PowerShell.</span></span>
3. <span data-ttu-id="3ef97-116">Voer **Add-AzureAccount** om uw Azure-abonnement te verifiëren.</span><span class="sxs-lookup"><span data-stu-id="3ef97-116">Run **Add-AzureAccount** to authenticate to your Azure subscription.</span></span> <span data-ttu-id="3ef97-117">Wanneer u wordt gevraagd, typt u de dezelfde gebruikersnaam en wachtwoord dat u aan te melden bij Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="3ef97-117">When prompted, enter the same user name and password that you use to sign in to Azure portal.</span></span>  
4. <span data-ttu-id="3ef97-118">Voer **Get-AzureSubscription** voor een lijst met de abonnementen die zijn gekoppeld aan uw gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="3ef97-118">Run **Get-AzureSubscription** to list the subscriptions associated with your user account.</span></span> 
5. <span data-ttu-id="3ef97-119">Voer **Select-AzureSubscription - SubscriptionName &lt;abonnementsnaam&gt;**  of **Select-AzureSubscription - SubscriptionId &lt;abonnements-ID&gt;**  om op te geven van het abonnement te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3ef97-119">Run **Select-AzureSubscription -SubscriptionName &lt;subscription name&gt;** or **Select-AzureSubscription -SubscriptionId &lt;subscription ID&gt;** to specify the subscription to use.</span></span>

<span data-ttu-id="3ef97-120">Gefeliciteerd, uw Azure PowerShell-console is geconfigureerd en klaar voor gebruik.</span><span class="sxs-lookup"><span data-stu-id="3ef97-120">Congratulations, your Azure PowerShell console is configured and ready to use.</span></span> <span data-ttu-id="3ef97-121">Houd er rekening mee dat u wilt herhaalt stappen 2 t/m 5 telkens wanneer u start de Azure PowerShell-console.</span><span class="sxs-lookup"><span data-stu-id="3ef97-121">Be aware that you'll need to repeate steps 2 through 5 each time you start the the Azure PowerShell console.</span></span>  


## <a name="list-all-collections"></a><span data-ttu-id="3ef97-122">Lijst van alle verzamelingen</span><span class="sxs-lookup"><span data-stu-id="3ef97-122">List all collections</span></span>
- - -
     <span data-ttu-id="3ef97-123">Get-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="3ef97-123">Get-AzureRemoteAppCollection</span></span>

## <a name="delete-a-collection"></a><span data-ttu-id="3ef97-124">Een verzameling verwijderen</span><span class="sxs-lookup"><span data-stu-id="3ef97-124">Delete a collection</span></span>
- - -
    <span data-ttu-id="3ef97-125">Verwijder AzureRemoteAppCollection<enter collection name></span><span class="sxs-lookup"><span data-stu-id="3ef97-125">Remove-AzureRemoteAppCollection <enter collection name></span></span>

<span data-ttu-id="3ef97-126">Voorbeeld: `Remove-AzureRemoteAppCollection ContosoProduction`.</span><span class="sxs-lookup"><span data-stu-id="3ef97-126">Example:  `Remove-AzureRemoteAppCollection ContosoProduction`.</span></span>

## <a name="create-a-cloud-collection"></a><span data-ttu-id="3ef97-127">Een cloudverzameling maken</span><span class="sxs-lookup"><span data-stu-id="3ef97-127">Create a cloud collection</span></span>
- - -
<span data-ttu-id="3ef97-128">Het is eenvoudig, voer de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="3ef97-128">It's simple, run the following command:</span></span>

    New-AzureRemoteAppCollection -Collectionname RAppO365Col1 -ImageName "Office 365 ProPlus (Subscription required)" -Plan Basic -Location "West US" - Description "Office 365 Collection."

<span data-ttu-id="3ef97-129">De bovenstaande opdracht publiceert automatisch Microsoft Office 365-toepassingen (Excel, OneNote, Outlook, PowerPoint, Visio en Word).</span><span class="sxs-lookup"><span data-stu-id="3ef97-129">The above command automatically publishes Microsoft Office 365 applications (Excel, OneNote, Outlook, PowerPoint, Visio and Word).</span></span>

<span data-ttu-id="3ef97-130">Maken van een siteverzameling kan 30 minuten duren of langer duren.</span><span class="sxs-lookup"><span data-stu-id="3ef97-130">Collection creation can take 30 minutes or longer to complete.</span></span> <span data-ttu-id="3ef97-131">Deze opdracht retourneert daarom een tracerings-ID die u kunt als volgt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="3ef97-131">Therefore, this command returns a tracking ID that you can use as follows:</span></span>

    Get-AzureRemoteAppOperationResult -TrackingId xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

<span data-ttu-id="3ef97-132">Nadat de verzameling is voltooid, kunt u gebruikers kunt toevoegen aan de verzameling met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="3ef97-132">After the collection is done, you can add users to the collection with the following command:</span></span>

    Add-AzureRemoteAppUser -CollectionName RAppO365Col1 -Type microsoftAccount -UserUpn someone@domain.com

<span data-ttu-id="3ef97-133">En u klaar bent!</span><span class="sxs-lookup"><span data-stu-id="3ef97-133">And you're done!</span></span> <span data-ttu-id="3ef97-134">Deze gebruiker moet verbinding maken met de toepassing met behulp van de Azure RemoteApp-client gevonden [hier](https://www.remoteapp.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="3ef97-134">That user should be able to connect to the application using the Azure RemoteApp client found [here](https://www.remoteapp.windowsazure.com/).</span></span>

## <a name="available-cmdlets"></a><span data-ttu-id="3ef97-135">Beschikbare cmdlets</span><span class="sxs-lookup"><span data-stu-id="3ef97-135">Available cmdlets</span></span>
<span data-ttu-id="3ef97-136">Er zijn veel andere opdrachten die we hebben, de documentatie voor hen wordt binnenkort wel binnenkort:</span><span class="sxs-lookup"><span data-stu-id="3ef97-136">There are lots of other commands that we have, the documentation for them will be coming shortly:</span></span>

<span data-ttu-id="3ef97-137">Basic RemoteApp-collectie cmdlets:</span><span class="sxs-lookup"><span data-stu-id="3ef97-137">Basic RemoteApp Collection cmdlets:</span></span> 

* <span data-ttu-id="3ef97-138">New-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="3ef97-138">New-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="3ef97-139">Get-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="3ef97-139">Get-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="3ef97-140">Set-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="3ef97-140">Set-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="3ef97-141">Update-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="3ef97-141">Update-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="3ef97-142">Remove-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="3ef97-142">Remove-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="3ef97-143">Add-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="3ef97-143">Add-AzureRemoteAppUser</span></span>
* <span data-ttu-id="3ef97-144">Get-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="3ef97-144">Get-AzureRemoteAppUser</span></span>
* <span data-ttu-id="3ef97-145">Remove-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="3ef97-145">Remove-AzureRemoteAppUser</span></span>
* <span data-ttu-id="3ef97-146">Get-AzureRemoteAppSession</span><span class="sxs-lookup"><span data-stu-id="3ef97-146">Get-AzureRemoteAppSession</span></span>
* <span data-ttu-id="3ef97-147">Disconnect-AzureRemoteAppSession</span><span class="sxs-lookup"><span data-stu-id="3ef97-147">Disconnect-AzureRemoteAppSession</span></span>
* <span data-ttu-id="3ef97-148">Invoke-AzureRemoteAppSessionLogoff</span><span class="sxs-lookup"><span data-stu-id="3ef97-148">Invoke-AzureRemoteAppSessionLogoff</span></span>
* <span data-ttu-id="3ef97-149">Send-AzureRemoteAppSessionMessage</span><span class="sxs-lookup"><span data-stu-id="3ef97-149">Send-AzureRemoteAppSessionMessage</span></span>
* <span data-ttu-id="3ef97-150">Get-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="3ef97-150">Get-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="3ef97-151">Get-AzureRemoteAppStartMenuProgram</span><span class="sxs-lookup"><span data-stu-id="3ef97-151">Get-AzureRemoteAppStartMenuProgram</span></span>
* <span data-ttu-id="3ef97-152">Publish-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="3ef97-152">Publish-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="3ef97-153">Unpublish-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="3ef97-153">Unpublish-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="3ef97-154">Get-AzureRemoteAppCollectionUsageDetails</span><span class="sxs-lookup"><span data-stu-id="3ef97-154">Get-AzureRemoteAppCollectionUsageDetails</span></span>
* <span data-ttu-id="3ef97-155">Get-AzureRemoteAppCollectionUsageSummary</span><span class="sxs-lookup"><span data-stu-id="3ef97-155">Get-AzureRemoteAppCollectionUsageSummary</span></span>
* <span data-ttu-id="3ef97-156">Get-AzureRemoteAppPlan</span><span class="sxs-lookup"><span data-stu-id="3ef97-156">Get-AzureRemoteAppPlan</span></span>

<span data-ttu-id="3ef97-157">RemoteApp-cmdlets voor virtueel netwerk:</span><span class="sxs-lookup"><span data-stu-id="3ef97-157">RemoteApp virtual network cmdlets:</span></span>

* <span data-ttu-id="3ef97-158">New-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="3ef97-158">New-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="3ef97-159">Get-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="3ef97-159">Get-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="3ef97-160">Set-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="3ef97-160">Set-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="3ef97-161">Remove-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="3ef97-161">Remove-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="3ef97-162">Get-AzureRemoteAppVpnDevice</span><span class="sxs-lookup"><span data-stu-id="3ef97-162">Get-AzureRemoteAppVpnDevice</span></span>
* <span data-ttu-id="3ef97-163">Get--AzureRemoteAppVpnDeviceConfigScript</span><span class="sxs-lookup"><span data-stu-id="3ef97-163">Get-- AzureRemoteAppVpnDeviceConfigScript</span></span>
* <span data-ttu-id="3ef97-164">Reset-AzureRemoteAppVpnSharedKey</span><span class="sxs-lookup"><span data-stu-id="3ef97-164">Reset-AzureRemoteAppVpnSharedKey</span></span>

<span data-ttu-id="3ef97-165">RemoteApp-sjabloon installatiekopie cmdlets:</span><span class="sxs-lookup"><span data-stu-id="3ef97-165">RemoteApp template image cmdlets:</span></span>

* <span data-ttu-id="3ef97-166">New-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="3ef97-166">New-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="3ef97-167">Get-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="3ef97-167">Get-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="3ef97-168">Rename-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="3ef97-168">Rename-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="3ef97-169">Remove-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="3ef97-169">Remove-AzureRemoteAppTemplateImage</span></span>

<span data-ttu-id="3ef97-170">Andere RemoteApp-cmdlets:</span><span class="sxs-lookup"><span data-stu-id="3ef97-170">Other RemoteApp cmdlets:</span></span>

* <span data-ttu-id="3ef97-171">Get-AzureRemoteAppLocation</span><span class="sxs-lookup"><span data-stu-id="3ef97-171">Get-AzureRemoteAppLocation</span></span>
* <span data-ttu-id="3ef97-172">Get-AzureRemoteAppWorkspace</span><span class="sxs-lookup"><span data-stu-id="3ef97-172">Get-AzureRemoteAppWorkspace</span></span>
* <span data-ttu-id="3ef97-173">Set-AzureRemoteAppWorkspace</span><span class="sxs-lookup"><span data-stu-id="3ef97-173">Set-AzureRemoteAppWorkspace</span></span>
* <span data-ttu-id="3ef97-174">Get-AzureRemoteAppOperationResult</span><span class="sxs-lookup"><span data-stu-id="3ef97-174">Get-AzureRemoteAppOperationResult</span></span>

