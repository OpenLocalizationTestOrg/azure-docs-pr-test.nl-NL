---
title: Verbinding met uw app in het virtuele netwerk maken via PowerShell
description: Instructies voor het verbinding maken met en werken met virtuele netwerken met behulp van PowerShell
services: app-service
documentationcenter: 
author: ccompy
manager: erikre
editor: cephalin
ms.assetid: a5c76e77-972a-431c-b14b-3611dae1631b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/29/2016
ms.author: ccompy
ms.openlocfilehash: 6fae6a6c162fa326161d2b47a259b3151d6e3dd0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-app-to-your-virtual-network-by-using-powershell"></a><span data-ttu-id="65db9-103">Verbinding met uw app in het virtuele netwerk maken via PowerShell</span><span class="sxs-lookup"><span data-stu-id="65db9-103">Connect your app to your virtual network by using PowerShell</span></span>
## <a name="overview"></a><span data-ttu-id="65db9-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="65db9-104">Overview</span></span>
<span data-ttu-id="65db9-105">In Azure App Service kunt u uw app (web, mobiel of API) met een Azure virtual network (VNet) in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="65db9-105">In Azure App Service, you can connect your app (web, mobile, or API) to an Azure virtual network (VNet) in your subscription.</span></span> <span data-ttu-id="65db9-106">Deze functie is aangeroepen VNet-integratie.</span><span class="sxs-lookup"><span data-stu-id="65db9-106">This feature is called VNet Integration.</span></span> <span data-ttu-id="65db9-107">Verwar de VNet-integratiefunctie niet met de functie App Service-omgeving, zodat u kunt een exemplaar van Azure App Service uitvoeren in uw virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="65db9-107">The VNet Integration feature should not be confused with the App Service Environment feature, which allows you to run an instance of Azure App Service in your virtual network.</span></span>

<span data-ttu-id="65db9-108">De VNet-integratiefunctie heeft een gebruikersinterface (UI) in de nieuwe portal die u gebruiken kunt om te integreren met virtuele netwerken die zijn geïmplementeerd met behulp van het klassieke implementatiemodel of het Azure Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="65db9-108">The VNet Integration feature has a user interface (UI) in the new portal that you can use to integrate with virtual networks that are deployed by using either the classic deployment model or the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="65db9-109">Als u wilt voor meer informatie over de functie, Zie [uw app integreren met een Azure-netwerk](web-sites-integrate-with-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="65db9-109">If you want to learn more about the feature, see [Integrate your app with an Azure virtual network](web-sites-integrate-with-vnet.md).</span></span>

<span data-ttu-id="65db9-110">Dit artikel is niet over het gebruik van de gebruikersinterface, maar in plaats daarvan over het inschakelen van integratie met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="65db9-110">This article is not about how to use the UI but rather about how to enable integration by using PowerShell.</span></span> <span data-ttu-id="65db9-111">Omdat de opdrachten voor elk implementatiemodel verschillend zijn, heeft dit artikel een sectie voor elke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="65db9-111">Because the commands for each deployment model are different, this article has a section for each deployment model.</span></span>  

<span data-ttu-id="65db9-112">Controleer voordat u met dit artikel doorgaat, dat u hebt:</span><span class="sxs-lookup"><span data-stu-id="65db9-112">Before you continue with this article, ensure that you have:</span></span>

* <span data-ttu-id="65db9-113">De nieuwste Azure PowerShell SDK geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="65db9-113">The latest Azure PowerShell SDK installed.</span></span> <span data-ttu-id="65db9-114">U kunt dit installeren met het Webplatforminstallatieprogramma.</span><span class="sxs-lookup"><span data-stu-id="65db9-114">You can install this with the Web Platform Installer.</span></span>
* <span data-ttu-id="65db9-115">Een app in Azure App Service wordt uitgevoerd op een Standard of Premium-SKU.</span><span class="sxs-lookup"><span data-stu-id="65db9-115">An app in Azure App Service running in a Standard or Premium SKU.</span></span>

## <a name="classic-virtual-networks"></a><span data-ttu-id="65db9-116">Klassieke virtuele netwerken</span><span class="sxs-lookup"><span data-stu-id="65db9-116">Classic virtual networks</span></span>
<span data-ttu-id="65db9-117">Deze sectie wordt uitgelegd drie taken voor virtuele netwerken die gebruikmaken van het klassieke implementatiemodel:</span><span class="sxs-lookup"><span data-stu-id="65db9-117">This section explains three tasks for virtual networks that use the classic deployment model:</span></span>

1. <span data-ttu-id="65db9-118">Uw app verbinden met een bestaand virtueel netwerk dat een gateway heeft en is geconfigureerd voor punt-naar-site-connectiviteit.</span><span class="sxs-lookup"><span data-stu-id="65db9-118">Connect your app to a preexisting virtual network that has a gateway and is configured for point-to-site connectivity.</span></span>
2. <span data-ttu-id="65db9-119">Werk uw gegevens van de integratie van virtueel netwerk voor uw app.</span><span class="sxs-lookup"><span data-stu-id="65db9-119">Update your virtual network integration information for your app.</span></span>
3. <span data-ttu-id="65db9-120">Verbreek de verbinding tussen uw app in het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="65db9-120">Disconnect your app from your virtual network.</span></span>

### <a name="connect-an-app-to-a-classic-vnet"></a><span data-ttu-id="65db9-121">Een app verbinden met een klassiek VNet</span><span class="sxs-lookup"><span data-stu-id="65db9-121">Connect an app to a classic VNet</span></span>
<span data-ttu-id="65db9-122">Als u wilt een app koppelen aan een virtueel netwerk, volg deze drie stappen:</span><span class="sxs-lookup"><span data-stu-id="65db9-122">To connect an app to a virtual network, follow these three steps:</span></span>

1. <span data-ttu-id="65db9-123">Declareren in de web-app of moet deze aan een bepaald virtueel netwerk koppelen.</span><span class="sxs-lookup"><span data-stu-id="65db9-123">Declare to the web app that it will be joining a particular virtual network.</span></span> <span data-ttu-id="65db9-124">De app een certificaat dat wordt verleend aan het virtuele netwerk voor punt-naar-site-connectiviteit gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="65db9-124">The app will generate a certificate that will be given to the virtual network for point-to-site connectivity.</span></span>
2. <span data-ttu-id="65db9-125">Het certificaat voor web-app uploaden naar het virtuele netwerk en vervolgens de punt-naar-site VPN-pakket URI worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="65db9-125">Upload the web app certificate to the virtual network, and then retrieve the point-to-site VPN package URI.</span></span>
3. <span data-ttu-id="65db9-126">De web-app virtueel netwerkverbinding met de pakket-URI van de punt-naar-site bijwerken.</span><span class="sxs-lookup"><span data-stu-id="65db9-126">Update the web app's virtual network connection with the point-to-site package URI.</span></span>

<span data-ttu-id="65db9-127">De eerste en derde stappen volledige scriptondersteuning mogelijk zijn, maar de tweede stap vereist een eenmalige, handmatige actie via de portal of de toegang tot het uitvoeren van **plaatsen** of **PATCH** acties op het virtuele netwerk Azure Resource Manager-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="65db9-127">The first and third steps are fully scriptable, but the second step requires a one-time, manual action through the portal, or access to perform **PUT** or **PATCH** actions on the virtual network Azure Resource Manager endpoint.</span></span> <span data-ttu-id="65db9-128">Neem contact op met een Azure-ondersteuning als dit is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="65db9-128">Contact Azure Support to have this enabled.</span></span> <span data-ttu-id="65db9-129">Voordat u begint, zorg ervoor dat er een klassiek virtueel netwerk met punt-naar-site-connectiviteit is ingeschakeld en een geïmplementeerde gateway.</span><span class="sxs-lookup"><span data-stu-id="65db9-129">Before you start, make sure that you have a classic virtual network that has point-to-site connectivity already enabled and a deployed gateway.</span></span> <span data-ttu-id="65db9-130">Als u wilt maken van de gateway en punt-naar-site-connectiviteit inschakelt, moet u de portal te gebruiken, zoals beschreven op [maken van een VPN-gateway][createvpngateway].</span><span class="sxs-lookup"><span data-stu-id="65db9-130">To create the gateway and enable point-to-site connectivity, you need to use the portal as described at [Creating a VPN gateway][createvpngateway].</span></span>

<span data-ttu-id="65db9-131">Het klassieke virtuele netwerk moet zich in hetzelfde abonnement als uw App Service-abonnement met de app die u integreert.</span><span class="sxs-lookup"><span data-stu-id="65db9-131">The classic virtual network needs to be in the same subscription as your App Service plan that holds the app that you are integrating with.</span></span>

##### <a name="set-up-azure-powershell-sdk"></a><span data-ttu-id="65db9-132">Instellen van Azure PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="65db9-132">Set up Azure PowerShell SDK</span></span>
<span data-ttu-id="65db9-133">Open een PowerShell-venster en instellen van uw Azure-account en abonnement met behulp van:</span><span class="sxs-lookup"><span data-stu-id="65db9-133">Open a PowerShell window and set up your Azure account and subscription by using:</span></span>

    Login-AzureRmAccount

<span data-ttu-id="65db9-134">Deze opdracht wordt een prompt voor uw Azure-referenties geopend.</span><span class="sxs-lookup"><span data-stu-id="65db9-134">That command will open a prompt to get your Azure credentials.</span></span> <span data-ttu-id="65db9-135">Nadat u zich aanmeldt, gebruik een van de volgende opdrachten om het abonnement dat u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="65db9-135">After you sign in, use either of the following commands to select the subscription that you want to use.</span></span> <span data-ttu-id="65db9-136">Zorg ervoor dat u van het abonnement die uw virtuele netwerk en de App Service-abonnement gebruikmaakt in.</span><span class="sxs-lookup"><span data-stu-id="65db9-136">Make sure that you are using the subscription that your virtual network and App Service plan are in.</span></span>

    Select-AzureRmSubscription –SubscriptionName [WebAppSubscriptionName]

<span data-ttu-id="65db9-137">of</span><span class="sxs-lookup"><span data-stu-id="65db9-137">or</span></span>

    Select-AzureRmSubscription –SubscriptionId [WebAppSubscriptionId]

##### <a name="variables-used-in-this-article"></a><span data-ttu-id="65db9-138">Variabelen die in dit artikel worden gebruikt</span><span class="sxs-lookup"><span data-stu-id="65db9-138">Variables used in this article</span></span>
<span data-ttu-id="65db9-139">Om te vereenvoudigen opdrachten, stelt we een **$Configuration** PowerShell variabele met de specifieke configuratie.</span><span class="sxs-lookup"><span data-stu-id="65db9-139">To simplify commands, we will set a **$Configuration** PowerShell variable with the specific configuration.</span></span>

<span data-ttu-id="65db9-140">Een variabele als volgt instellen in PowerShell met de volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="65db9-140">Set a variable as follows in PowerShell with the following parameters:</span></span>

    $Configuration = @{}
    $Configuration.WebAppResourceGroup = "[Your web app resource group]"
    $Configuration.WebAppName = "[Your web app name]"
    $Configuration.VnetSubscriptionId = "[Your vnet subscription id]"
    $Configuration.VnetResourceGroup = "[Your vnet resource group]"
    $Configuration.VnetName = "[Your vnet name]"

<span data-ttu-id="65db9-141">De locatie van de app moet de locatie zonder spaties.</span><span class="sxs-lookup"><span data-stu-id="65db9-141">The app location should be the location without any spaces.</span></span> <span data-ttu-id="65db9-142">Bijvoorbeeld, is VS-West westus.</span><span class="sxs-lookup"><span data-stu-id="65db9-142">For example, West US is westus.</span></span>

    $Configuration.WebAppLocation = "[Your web app Location]"

<span data-ttu-id="65db9-143">Het volgende item is waar het certificaat moet worden geschreven.</span><span class="sxs-lookup"><span data-stu-id="65db9-143">The next item is where the certificate should be written.</span></span> <span data-ttu-id="65db9-144">Deze moet een pad op de lokale computer.</span><span class="sxs-lookup"><span data-stu-id="65db9-144">It should be a writable path on your local computer.</span></span> <span data-ttu-id="65db9-145">Zorg ervoor dat .cer aan het einde.</span><span class="sxs-lookup"><span data-stu-id="65db9-145">Make sure to include .cer at the end.</span></span>

    $Configuration.GeneratedCertificatePath = "[C:\Path\To\Certificate.cer]"

<span data-ttu-id="65db9-146">Typ om te zien wat u hebt ingesteld, **$Configuration**.</span><span class="sxs-lookup"><span data-stu-id="65db9-146">To see what you set, type **$Configuration**.</span></span>

    > $Configuration

    Name                           Value
    ----                           -----
    GeneratedCertificatePath       C:\vnetcert.cer
    VnetSubscriptionId             efc239a4-88f9-2c5e-a9a1-3034c21ad496
    WebAppResourceGroup            vnetdemo-rg
    VnetResourceGroup              testase1-rg
    VnetName                       TestNetwork
    WebAppName                     vnetintdemoapp
    WebAppLocation                 centralus

<span data-ttu-id="65db9-147">De rest van deze sectie wordt ervan uitgegaan dat u een variabele die is gemaakt als NET beschreven hebt.</span><span class="sxs-lookup"><span data-stu-id="65db9-147">The rest of this section assumes that you have a variable created as just described.</span></span>

##### <a name="declare-the-virtual-network-to-the-app"></a><span data-ttu-id="65db9-148">Het virtuele netwerk naar de app declareren</span><span class="sxs-lookup"><span data-stu-id="65db9-148">Declare the virtual network to the app</span></span>
<span data-ttu-id="65db9-149">Gebruik de volgende opdracht om te controleren van de app dat deze dit bepaalde virtuele netwerk wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="65db9-149">Use the following command to tell the app that it will be using this particular virtual network.</span></span> <span data-ttu-id="65db9-150">Dit zorgt ervoor dat de app voor het genereren van de benodigde certificaten:</span><span class="sxs-lookup"><span data-stu-id="65db9-150">This will cause the app to generate necessary certificates:</span></span>

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -PropertyObject @{"VnetResourceId" = "/subscriptions/$($Configuration.VnetSubscriptionId)/resourceGroups/$($Configuration.VnetResourceGroup)/providers/Microsoft.ClassicNetwork/virtualNetworks/$($Configuration.VnetName)"} -Location $Configuration.WebAppLocation -ApiVersion 2015-07-01

<span data-ttu-id="65db9-151">Als u deze opdracht is geslaagd, **$vnet** moet een **eigenschappen** in deze variabele.</span><span class="sxs-lookup"><span data-stu-id="65db9-151">If this command succeeds, **$vnet** should have a **Properties** variable in it.</span></span> <span data-ttu-id="65db9-152">De **eigenschappen** variabele moet zowel een vingerafdruk van het certificaat en de gegevens van het certificaat bevatten.</span><span class="sxs-lookup"><span data-stu-id="65db9-152">The **Properties** variable should contain both a certificate thumbprint and the certificate data.</span></span>

##### <a name="upload-the-web-app-certificate-to-the-virtual-network"></a><span data-ttu-id="65db9-153">Het certificaat voor web-app uploaden naar het virtuele netwerk</span><span class="sxs-lookup"><span data-stu-id="65db9-153">Upload the web app certificate to the virtual network</span></span>
<span data-ttu-id="65db9-154">Een handmatige stap eenmalige is vereist voor elk abonnement en de combinatie van het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="65db9-154">A manual, one-time step is required for each subscription and virtual network combination.</span></span> <span data-ttu-id="65db9-155">Dat wil zeggen, als u apps in abonnement een verbinding met een virtueel netwerk, moet u doen in deze stap slechts eenmaal ongeacht hoeveel apps die u configureert.</span><span class="sxs-lookup"><span data-stu-id="65db9-155">That is, if you are connecting apps in Subscription A to Virtual Network A, you will need to do this step only once regardless of how many apps you configure.</span></span> <span data-ttu-id="65db9-156">Als u een nieuwe app aan een ander virtueel netwerk toevoegt, moet u dit opnieuw te doen.</span><span class="sxs-lookup"><span data-stu-id="65db9-156">If you are adding a new app to another virtual network, you'll need to do this again.</span></span> <span data-ttu-id="65db9-157">De reden hiervoor is dat een set van certificaten wordt gegenereerd tijdens een abonnement in Azure App Service en de set eenmaal voor elk virtueel netwerk dat de apps die verbinding met maakt wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="65db9-157">The reason for this is that a set of certificates is generated at a subscription level in Azure App Service, and the set is generated once for each virtual network that the apps will connect to.</span></span>

<span data-ttu-id="65db9-158">De certificaten wordt al zijn ingesteld als u deze stappen hebt uitgevoerd of als u geïntegreerd met hetzelfde virtuele netwerk met behulp van de portal.</span><span class="sxs-lookup"><span data-stu-id="65db9-158">The certificates will have already been set if you followed these steps or if you integrated with the same virtual network by using the portal.</span></span>

<span data-ttu-id="65db9-159">De eerste stap is het cer-bestand genereren.</span><span class="sxs-lookup"><span data-stu-id="65db9-159">The first step is to generate the .cer file.</span></span> <span data-ttu-id="65db9-160">De tweede stap is het cer-bestand uploaden naar uw virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="65db9-160">The second step is to upload the .cer file to your virtual network.</span></span> <span data-ttu-id="65db9-161">Voor het genereren van het cer-bestand van de API-aanroep in de vorige stap, voer de volgende opdrachten.</span><span class="sxs-lookup"><span data-stu-id="65db9-161">To generate the .cer file from the API call in the earlier step, run the following commands.</span></span>

    $certBytes = [System.Convert]::FromBase64String($vnet.Properties.certBlob)
    [System.IO.File]::WriteAllBytes("$($Configuration.GeneratedCertificatePath)", $certBytes)

<span data-ttu-id="65db9-162">Het certificaat wordt gevonden op de locatie die **$Configuration.GeneratedCertificatePath** bevat.</span><span class="sxs-lookup"><span data-stu-id="65db9-162">The certificate will be found in the location that **$Configuration.GeneratedCertificatePath** specifies.</span></span>

<span data-ttu-id="65db9-163">Het certificaat handmatig uploaden, gebruiken de [Azure-portal] [ azureportal] en **bladeren virtueel netwerk (klassiek)** > **VPN-verbindingen** > **punt-naar-site** > **certificaten beheren**.</span><span class="sxs-lookup"><span data-stu-id="65db9-163">To upload the certificate manually, use the [Azure portal][azureportal] and **Browse Virtual Network (classic)** > **VPN connections** > **Point-to-site** > **Manage certificates**.</span></span> <span data-ttu-id="65db9-164">Hier kunt uw certificaat te uploaden.</span><span class="sxs-lookup"><span data-stu-id="65db9-164">From here, upload your certificate.</span></span>

##### <a name="get-the-point-to-site-package"></a><span data-ttu-id="65db9-165">Het pakket voor punt-naar-site</span><span class="sxs-lookup"><span data-stu-id="65db9-165">Get the point-to-site package</span></span>
<span data-ttu-id="65db9-166">De volgende stap bij het instellen van een virtueel netwerkverbinding op een web-app is het ophalen van het pakket voor punt-naar-site en het weer doorgeeft aan uw web-app.</span><span class="sxs-lookup"><span data-stu-id="65db9-166">The next step in setting up a virtual network connection on a web app is to get the point-to-site package and provide it to your web app.</span></span>

<span data-ttu-id="65db9-167">De volgende sjabloon opslaan in een bestand met de naam van de GetNetworkPackageUri.json ergens op uw computer, bijvoorbeeld C:\Azure\Templates\GetNetworkPackageUri.json.</span><span class="sxs-lookup"><span data-stu-id="65db9-167">Save the following template to a file called GetNetworkPackageUri.json somewhere on your computer, for example, C:\Azure\Templates\GetNetworkPackageUri.json.</span></span>

    {
        "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "certData": {
                "type": "string"
            },
            "certThumbprint": {
                "type": "string"
            },
            "networkName": {
                "type": "string"
            }
        },
        "variables": {
            "legacyVnetName": "[concat('Group ', resourceGroup().name, ' ', parameters('networkName'))]"
            },
            "resources": [
            ],
        "outputs" : {
            "PackageUri" :
            {
            "value" : "[listPackage(resourceId('Microsoft.ClassicNetwork/virtualNetworks/gateways/clientRootCertificates', parameters('networkName'), 'primary', parameters('certThumbprint')), '2014-06-01').packageUri]", "type" : "string"
            }
        }
    }


<span data-ttu-id="65db9-168">Invoerparameters instellen:</span><span class="sxs-lookup"><span data-stu-id="65db9-168">Set input parameters:</span></span>

    $parameters = @{"certData" = $vnet.Properties.certBlob ;
    certThumbprint = $vnet.Properties.certThumbprint ;
    "networkName" = $Configuration.VnetName }

<span data-ttu-id="65db9-169">Roept het script:</span><span class="sxs-lookup"><span data-stu-id="65db9-169">Call the script:</span></span>

    $output = New-AzureRmResourceGroupDeployment -Name unused -ResourceGroupName $Configuration.VnetResourceGroup -TemplateParameterObject $parameters -TemplateFile C:\PATH\TO\GetNetworkPackageUri.json


<span data-ttu-id="65db9-170">De variabele **$output. Outputs.packageUri** bevat nu de pakket-URI die moet worden besteed aan uw web-app.</span><span class="sxs-lookup"><span data-stu-id="65db9-170">The variable **$output.Outputs.packageUri** will now contain the package URI to be given to your web app.</span></span>

##### <a name="upload-the-point-to-site-package-to-your-app"></a><span data-ttu-id="65db9-171">Uploaden van het pakket punt-naar-site naar uw app</span><span class="sxs-lookup"><span data-stu-id="65db9-171">Upload the point-to-site package to your app</span></span>
<span data-ttu-id="65db9-172">De laatste stap is om te voorzien van de app dit pakket.</span><span class="sxs-lookup"><span data-stu-id="65db9-172">The final step is to provide the app with this package.</span></span> <span data-ttu-id="65db9-173">Alleen uitvoeren de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="65db9-173">Simply run the next command:</span></span>

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)/primary" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-07-01 -PropertyObject @{"VnetName" = $Configuration.VnetName ; "VpnPackageUri" = $($output.Outputs.packageUri).Value } -Location $Configuration.WebAppLocation

<span data-ttu-id="65db9-174">Als een bericht u gevraagd te bevestigen wordt dat u een bestaande resource wilt overschrijven, moet u mogelijk te maken.</span><span class="sxs-lookup"><span data-stu-id="65db9-174">If a message asks you to confirm that you are overwriting an existing resource, make sure to allow it.</span></span>

<span data-ttu-id="65db9-175">Nadat deze opdracht is geslaagd, moet u uw app nu verbonden aan het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="65db9-175">After this command succeeds, your app should now be connected to the virtual network.</span></span> <span data-ttu-id="65db9-176">Om te bevestigen geslaagd, gaat u naar uw app-console en typ het volgende:</span><span class="sxs-lookup"><span data-stu-id="65db9-176">To confirm success, go to your app console, and type the following:</span></span>

    SET WEBSITE_

<span data-ttu-id="65db9-177">Als er een omgevingsvariabele WEBSITE_VNETNAME die heeft een waarde die overeenkomt met de naam van het virtuele doelnetwerk genoemd, worden alle configuraties zijn geslaagd.</span><span class="sxs-lookup"><span data-stu-id="65db9-177">If there is an environment variable called WEBSITE_VNETNAME that has a value that matches the name of the target virtual network, all configurations have succeeded.</span></span>

### <a name="update-classic-vnet-integration-information"></a><span data-ttu-id="65db9-178">Klassieke VNet integratie-informatie bijwerken</span><span class="sxs-lookup"><span data-stu-id="65db9-178">Update classic VNet integration information</span></span>
<span data-ttu-id="65db9-179">Als u wilt bijwerken of uw gegevens synchroniseren, herhaalt u de stappen die u hebt gevolgd wanneer u de integratie in eerste instantie gemaakt.</span><span class="sxs-lookup"><span data-stu-id="65db9-179">To update or resync your information, simply repeat the steps that you followed when you created the integration in the first place.</span></span> <span data-ttu-id="65db9-180">Deze stappen zijn:</span><span class="sxs-lookup"><span data-stu-id="65db9-180">Those steps are:</span></span>

1. <span data-ttu-id="65db9-181">Definieer uw configuratie-informatie.</span><span class="sxs-lookup"><span data-stu-id="65db9-181">Define your configuration information.</span></span>
2. <span data-ttu-id="65db9-182">Het virtuele netwerk naar de app declareren.</span><span class="sxs-lookup"><span data-stu-id="65db9-182">Declare the virtual network to the app.</span></span>
3. <span data-ttu-id="65db9-183">Ophalen van de punt-naar-site-pakket.</span><span class="sxs-lookup"><span data-stu-id="65db9-183">Get the point-to-site package.</span></span>
4. <span data-ttu-id="65db9-184">Upload het pakket punt-naar-site naar uw app.</span><span class="sxs-lookup"><span data-stu-id="65db9-184">Upload the point-to-site package to your app.</span></span>

### <a name="disconnect-your-app-from-a-classic-vnet"></a><span data-ttu-id="65db9-185">Verbreek de verbinding tussen uw app een klassiek VNet</span><span class="sxs-lookup"><span data-stu-id="65db9-185">Disconnect your app from a classic VNet</span></span>
<span data-ttu-id="65db9-186">Als u wilt verbreken van de app, moet u de configuratiegegevens die is ingesteld tijdens de integratie van virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="65db9-186">To disconnect the app, you need the configuration information that was set during virtual network integration.</span></span> <span data-ttu-id="65db9-187">Deze gegevens niet gebruiken, is er vervolgens één opdracht uw app ontkoppelt van het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="65db9-187">Using that information, there is then one command to disconnect your app from your virtual network.</span></span>

    $vnet = Remove-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-07-01

## <a name="resource-manager-virtual-networks"></a><span data-ttu-id="65db9-188">Virtuele netwerken van Resource Manager</span><span class="sxs-lookup"><span data-stu-id="65db9-188">Resource Manager virtual networks</span></span>
<span data-ttu-id="65db9-189">Virtuele netwerken van Resource Manager hebben Azure Resource Manager-API's die bepaalde processen in vergelijking met het klassieke virtuele netwerken vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="65db9-189">Resource Manager virtual networks have Azure Resource Manager APIs, which simplify some processes when compared with classic virtual networks.</span></span> <span data-ttu-id="65db9-190">Wij hebben een script waarmee u de volgende taken uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="65db9-190">We have a script that will help you complete the following tasks:</span></span>

* <span data-ttu-id="65db9-191">Een virtueel netwerk van Resource Manager maken en uw app integreren.</span><span class="sxs-lookup"><span data-stu-id="65db9-191">Create a Resource Manager virtual network and integrate your app with it.</span></span>
* <span data-ttu-id="65db9-192">Maken van een gateway, punt-naar-site-connectiviteit in een bestaande Resource Manager virtueel netwerk configureren en vervolgens uw app integreren met het.</span><span class="sxs-lookup"><span data-stu-id="65db9-192">Create a gateway, configure point-to-site connectivity in a preexisting Resource Manager virtual network, and then integrate your app with it.</span></span>
* <span data-ttu-id="65db9-193">Uw app integreren met een bestaand virtueel netwerk voor Resource Manager, dat een gateway en een punt-naar-site-connectiviteit ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="65db9-193">Integrate your app with a preexisting Resource Manager virtual network that has a gateway and point-to-site connectivity enabled.</span></span>
* <span data-ttu-id="65db9-194">Verbreek de verbinding tussen uw app in het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="65db9-194">Disconnect your app from your virtual network.</span></span>

### <a name="resource-manager-vnet-app-service-integration-script"></a><span data-ttu-id="65db9-195">Script voor Resource Manager VNet-App Service-integratie</span><span class="sxs-lookup"><span data-stu-id="65db9-195">Resource Manager VNet App Service integration script</span></span>
<span data-ttu-id="65db9-196">Kopieer het volgende script en sla deze op een bestand.</span><span class="sxs-lookup"><span data-stu-id="65db9-196">Copy the following script and save it to a file.</span></span> <span data-ttu-id="65db9-197">Als u niet dat het script te gebruiken wilt, u kunt meer uit om te zien hoe dingen instellen met een virtueel netwerk van Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="65db9-197">If you don’t want to use the script, feel free to learn from it to see how to set things up with a Resource Manager virtual network.</span></span>

    function ReadHostWithDefault($message, $default)
    {
        $result = Read-Host "$message [$default]"
        if($result -eq "")
        {
            $result = $default
        }
            return $result
        }

    function PromptCustom($title, $optionValues, $optionDescriptions)
    {
        Write-Host $title
        Write-Host
        $a = @()
        for($i = 0; $i -lt $optionValues.Length; $i++){
            Write-Host "$($i+1))" $optionDescriptions[$i]
        }
        Write-Host

        while($true)
        {
            Write-Host "Choose an option: "
            $option = Read-Host
            $option = $option -as [int]

            if($option -ge 1 -and $option -le $optionValues.Length)
            {
                return $optionValues[$option-1]
            }
        }
    }

    function PromptYesNo($title, $message, $default = 0)
    {
        $yes = New-Object System.Management.Automation.Host.ChoiceDescription "&Yes", ""
        $no = New-Object System.Management.Automation.Host.ChoiceDescription "&No", ""
        $options = [System.Management.Automation.Host.ChoiceDescription[]]($yes, $no)
        $result = $host.ui.PromptForChoice($title, $message, $options, $default)
        return $result
    }

    function CreateVnet($resourceGroupName, $vnetName, $vnetAddressSpace, $vnetGatewayAddressSpace, $location)
    {
        Write-Host "Creating a new VNET"
        $gatewaySubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix $vnetGatewayAddressSpace
        New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroupName -Location $location -AddressPrefix $vnetAddressSpace -Subnet $gatewaySubnet
    }

    function CreateVnetGateway($resourceGroupName, $vnetName, $vnetIpName, $location, $vnetIpConfigName, $vnetGatewayName, $certificateData, $vnetPointToSiteAddressSpace)
    {
        $vnet = Get-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroupName
        $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet

        Write-Host "Creating a public IP address for this VNET"
        $pip = New-AzureRmPublicIpAddress -Name $vnetIpName -ResourceGroupName $resourceGroupName -Location $location -AllocationMethod Dynamic
        $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $vnetIpConfigName -Subnet $subnet -PublicIpAddress $pip

        Write-Host "Adding a root certificate to this VNET"
        $root = New-AzureRmVpnClientRootCertificate -Name "AppServiceCertificate.cer" -PublicCertData $certificateData

        Write-Host "Creating Azure VNET Gateway. This may take up to an hour."
        New-AzureRmVirtualNetworkGateway -Name $vnetGatewayName -ResourceGroupName $resourceGroupName -Location $location -IpConfigurations $ipconf -GatewayType Vpn -VpnType RouteBased -EnableBgp $false -GatewaySku Basic -VpnClientAddressPool $vnetPointToSiteAddressSpace -VpnClientRootCertificates $root
    }

    function AddNewVnet($subscriptionId, $webAppResourceGroup, $webAppName)
    {
        Write-Host "Adding a new Vnet"
        Write-Host
        $vnetName = Read-Host "Specify a name for this Virtual Network"

        $vnetGatewayName="$($vnetName)-gateway"
        $vnetIpName="$($vnetName)-ip"
        $vnetIpConfigName="$($vnetName)-ipconf"

        # Virtual Network settings
        $vnetAddressSpace="10.0.0.0/8"
        $vnetGatewayAddressSpace="10.5.0.0/16"
        $vnetPointToSiteAddressSpace="172.16.0.0/16"

        $changeRequested = 0
        $resourceGroupName = $webAppResourceGroup

        while($changeRequested -eq 0)
        {
            Write-Host
            Write-Host "Currently, I will create a VNET with the following settings:"
            Write-Host
            Write-Host "Virtual Network Name: $vnetName"
            Write-Host "Resource Group Name:  $resourceGroupName"
            Write-Host "Gateway Name: $vnetGatewayName"
            Write-Host "Vnet IP name: $vnetIpName"
            Write-Host "Vnet IP config name:  $vnetIpConfigName"
            Write-Host "Address Space:$vnetAddressSpace"
            Write-Host "Gateway Address Space:$vnetGatewayAddressSpace"
            Write-Host "Point-To-Site Address Space:  $vnetPointToSiteAddressSpace"
            Write-Host
            $changeRequested = PromptYesNo "" "Do you wish to change these settings?" 1

            if($changeRequested -eq 0)
            {
                $vnetName = ReadHostWithDefault "Virtual Network Name" $vnetName
                $resourceGroupName = ReadHostWithDefault "Resource Group Name" $resourceGroupName
                $vnetGatewayName = ReadHostWithDefault "Vnet Gateway Name" $vnetGatewayName
                $vnetIpName = ReadHostWithDefault "Vnet IP name" $vnetIpName
                $vnetIpConfigName = ReadHostWithDefault "Vnet IP configuration name" $vnetIpConfigName
                $vnetAddressSpace = ReadHostWithDefault "Vnet Address Space" $vnetAddressSpace
                $vnetGatewayAddressSpace = ReadHostWithDefault "Vnet Gateway Address Space" $vnetGatewayAddressSpace
                $vnetPointToSiteAddressSpace = ReadHostWithDefault "Vnet Point-to-site Address Space" $vnetPointToSiteAddressSpace
            }
        }

        $ErrorActionPreference = "Stop";

        # We create the virtual network and add it here. The way this works is:
        # 1) Add the VNET association to the App. This allows the App to generate certificates, etc. for the VNET.
        # 2) Create the VNET and VNET gateway, add the certificates, create the public IP, etc., required for the gateway
        # 3) Get the VPN package from the gateway and pass it back to the App.

        $webApp = Get-AzureRmResource -ResourceName $webAppName -ResourceType "Microsoft.Web/sites" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup
        $location = $webApp.Location

        Write-Host "Creating App association to VNET"
        $propertiesObject = @{
         "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($resourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnetName)"
        }
        $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnetName)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup -Force

        CreateVnet $resourceGroupName $vnetName $vnetAddressSpace $vnetGatewayAddressSpace $location

        CreateVnetGateway $resourceGroupName $vnetName $vnetIpName $location $vnetIpConfigName $vnetGatewayName $virtualNetwork.Properties.CertBlob $vnetPointToSiteAddressSpace

        Write-Host "Retrieving VPN Package and supplying to App"
        $packageUri = Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName -VirtualNetworkGatewayName $vnetGatewayName -ProcessorArchitecture Amd64
        
        # $packageUri may contain literal double-quotes at the start and the end of the URL
        if($packageUri.Length -gt 0 -and $packageUri.Substring(0, 1) -eq '"' -and $packageUri.Substring($packageUri.Length - 1, 1) -eq '"')
        {
            $packageUri = $packageUri.Substring(1, $packageUri.Length - 2)
        }

        # Put the VPN client configuration package onto the App
        $PropertiesObject = @{
        "vnetName" = $VirtualNetworkName; "vpnPackageUri" = $packageUri
        }

        New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnetName)/primary" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup -Force

        Write-Host "Finished!"
    }

    function AddExistingVnet($subscriptionId, $resourceGroupName, $webAppName)
    {
        $ErrorActionPreference = "Stop";

        # At this point, the gateway should be able to be joined to an App, but may require some minor tweaking. We will declare to the App now to use this VNET
        Write-Host "Getting App information"
        $webApp = Get-AzureRmResource -ResourceName $webAppName -ResourceType "Microsoft.Web/sites" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $location = $webApp.Location

        $webAppConfig = Get-AzureRmResource -ResourceName "$($webAppName)/web" -ResourceType "Microsoft.Web/sites/config" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $currentVnet = $webAppConfig.Properties.VnetName
        if($currentVnet -ne $null -and $currentVnet -ne "")
        {
            Write-Host "Currently connected to VNET $currentVnet"
        }

        # Display existing vnets
        $vnets = Get-AzureRmVirtualNetwork
        $vnetNames = @()
        foreach($vnet in $vnets)
        {
            $vnetNames += $vnet.Name
        }

        Write-Host
        $vnet = PromptCustom "Select a VNET to integrate with" $vnets $vnetNames

        # We need to check if this VNET is able to be joined to a App, based on following criteria
            # If there is no gateway, we can create one.
            # If there is a gateway:
                # It must be of type Vpn
                # It must be of VpnType RouteBased
                # If it doesn't have the right certificate, we will need to add it.
                # If it doesn't have a point-to-site range, we will need to add it.

        $gatewaySubnet = $vnet.Subnets | Where-Object { $_.Name -eq "GatewaySubnet" }

        if($gatewaySubnet -eq $null -or $gatewaySubnet.IpConfigurations -eq $null -or $gatewaySubnet.IpConfigurations.Count -eq 0)
        {
            $ErrorActionPreference = "Continue";
            # There is no gateway. We need to create one.
            Write-Host "This Virtual Network has no gateway. I will need to create one."

            $vnetName = $vnet.Name
            $vnetGatewayName="$($vnetName)-gateway"
            $vnetIpName="$($vnetName)-ip"
            $vnetIpConfigName="$($vnetName)-ipconf"

            # Virtual Network settings
            $vnetAddressSpace="10.0.0.0/8"
            $vnetGatewayAddressSpace="10.5.0.0/16"
            $vnetPointToSiteAddressSpace="172.16.0.0/16"

            $changeRequested = 0

            Write-Host "Your VNET is in the address space $($vnet.AddressSpace.AddressPrefixes), with the following Subnets:"
            foreach($subnet in $vnet.Subnets)
            {
                Write-Host "$($subnet.Name): $($subnet.AddressPrefix)"
            }

            $vnetGatewayAddressSpace = Read-Host "Please choose a GatewaySubnet address space"

            while($changeRequested -eq 0)
            {
                Write-Host
                Write-Host "Currently, I will create a VNET gateway with the following settings:"
                Write-Host
                Write-Host "Virtual Network Name: $vnetName"
                Write-Host "Resource Group Name:  $($vnet.ResourceGroupName)"
                Write-Host "Gateway Name: $vnetGatewayName"
                Write-Host "Vnet IP name: $vnetIpName"
                Write-Host "Vnet IP config name:  $vnetIpConfigName"
                Write-Host "Address Space:$($vnet.AddressSpace.AddressPrefixes)"
                Write-Host "Gateway Address Space:$vnetGatewayAddressSpace"
                Write-Host "Point-To-Site Address Space:  $vnetPointToSiteAddressSpace"
                Write-Host
                $changeRequested = PromptYesNo "" "Do you wish to change these settings?" 1

                if($changeRequested -eq 0)
                {
                    $vnetGatewayName = ReadHostWithDefault "Vnet Gateway Name" $vnetGatewayName
                    $vnetIpName = ReadHostWithDefault "Vnet IP name" $vnetIpName
                    $vnetIpConfigName = ReadHostWithDefault "Vnet IP configuration name" $vnetIpConfigName
                    $vnetGatewayAddressSpace = ReadHostWithDefault "Vnet Gateway Address Space" $vnetGatewayAddressSpace
                    $vnetPointToSiteAddressSpace = ReadHostWithDefault "Vnet Point-to-site Address Space" $vnetPointToSiteAddressSpace
                }
            }

            $ErrorActionPreference = "Stop";

            Write-Host "Creating App association to VNET"
            $propertiesObject = @{
             "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($vnet.ResourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnetName)"
            }

            $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

            # If there is no gateway subnet, we need to create one.
            if($gatewaySubnet -eq $null)
            {
                $gatewaySubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix $vnetGatewayAddressSpace
                $vnet.Subnets.Add($gatewaySubnet);
                Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
            }

            CreateVnetGateway $vnet.ResourceGroupName $vnetName $vnetIpName $location $vnetIpConfigName $vnetGatewayName $virtualNetwork.Properties.CertBlob $vnetPointToSiteAddressSpace

            $gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $vnet.ResourceGroupName -Name $vnetGatewayName
        }
        else
        {
            $uriParts = $gatewaySubnet.IpConfigurations[0].Id.Split('/')
            $gatewayResourceGroup = $uriParts[4]
            $gatewayName = $uriParts[8]

            $gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $vnet.ResourceGroupName -Name $gatewayName

            # validate gateway types, etc.
            if($gateway.GatewayType -ne "Vpn")
            {
                Write-Error "This gateway is not of the Vpn type. It cannot be joined to an App."
                return
            }

            if($gateway.VpnType -ne "RouteBased")
            {
                Write-Error "This gateways Vpn type is not RouteBased. It cannot be joined to an App."
                return
            }

            if($gateway.VpnClientConfiguration -eq $null -or $gateway.VpnClientConfiguration.VpnClientAddressPool -eq $null)
            {
                Write-Host "This gateway does not have a Point-to-site Address Range. Please specify one in CIDR notation, e.g. 10.0.0.0/8"
                $pointToSiteAddress = Read-Host "Point-To-Site Address Space"
                Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $gateway.Name -VpnClientAddressPool $pointToSiteAddress
            }

            Write-Host "Creating App association to VNET"
            $propertiesObject = @{
             "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($vnet.ResourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnet.Name)"
            }

            $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

            # We need to check if the certificate here exists in the gateway.
            $certificates = $gateway.VpnClientConfiguration.VpnClientRootCertificates

            $certFound = $false
            foreach($certificate in $certificates)
            {
                if($certificate.PublicCertData -eq $virtualNetwork.Properties.CertBlob)
                {
                    $certFound = $true
                    break
                }
            }

            if(-not $certFound)
            {
                Write-Host "Adding certificate"
                Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName "AppServiceCertificate.cer" -PublicCertData $virtualNetwork.Properties.CertBlob -VirtualNetworkGatewayName $gateway.Name
            }
        }

        # Now finish joining by getting the VPN package and giving it to the App
        Write-Host "Retrieving VPN Package and supplying to App"
        $packageUri = Get-AzureRmVpnClientPackage -ResourceGroupName $vnet.ResourceGroupName -VirtualNetworkGatewayName $gateway.Name -ProcessorArchitecture Amd64
        
        # $packageUri may contain literal double-quotes at the start and the end of the URL
        if($packageUri.Length -gt 0 -and $packageUri.Substring(0, 1) -eq '"' -and $packageUri.Substring($packageUri.Length - 1, 1) -eq '"')
        {
            $packageUri = $packageUri.Substring(1, $packageUri.Length - 2)
        }

        # Put the VPN client configuration package onto the App
        $PropertiesObject = @{
        "vnetName" = $vnet.Name; "vpnPackageUri" = $packageUri
        }

        New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)/primary" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

        Write-Host "Finished!"
    }

    function RemoveVnet($subscriptionId, $resourceGroupName, $webAppName)
    {
        $webAppConfig = Get-AzureRmResource -ResourceName "$($webAppName)/web" -ResourceType "Microsoft.Web/sites/config" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $currentVnet = $webAppConfig.Properties.VnetName
        if($currentVnet -ne $null -and $currentVnet -ne "")
        {
            Write-Host "Currently connected to VNET $currentVnet"

            Remove-AzureRmResource -ResourceName "$($webAppName)/$($currentVnet)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        }
            else
        {
            Write-Host "Not connected to a VNET."
        }
    }

    Write-Host "Please Login"
    Login-AzureRmAccount

    # Choose subscription. If there's only one we will choose automatically

    $subs = Get-AzureRmSubscription
    $subscriptionId = ""

    if($subs.Length -eq 0)
    {
        Write-Error "No subscriptions bound to this account."
        return
    }

    if($subs.Length -eq 1)
    {
        $subscriptionId = $subs[0].SubscriptionId
    }
    else
    {
        $subscriptionChoices = @()
        $subscriptionValues = @()

        foreach($subscription in $subs){
        $subscriptionChoices += "$($subscription.SubscriptionName) ($($subscription.SubscriptionId))";
        $subscriptionValues += ($subscription.SubscriptionId);
        }

        $subscriptionId = PromptCustom "Choose a subscription" $subscriptionValues $subscriptionChoices
    }

    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    $resourceGroup = Read-Host "Please enter the Resource Group of your App"

    $appName = Read-Host "Please enter the Name of your App"

    $options = @("Add a NEW Virtual Network to an App", "Add an EXISTING Virtual Network to an App", "Remove a Virtual Network from an App");
    $optionValues = @(0, 1, 2)
    $option = PromptCustom "What do you want to do?" $optionValues $options

    if($option -eq 0)
    {
        AddNewVnet $subscriptionId $resourceGroup $appName
    }
    if($option -eq 1)
    {
        AddExistingVnet $subscriptionId $resourceGroup $appName
    }
    if($option -eq 2)
    {
        RemoveVnet $subscriptionId $resourceGroup $appName
    }

<span data-ttu-id="65db9-198">Sla een kopie van het script.</span><span class="sxs-lookup"><span data-stu-id="65db9-198">Save a copy of the script.</span></span> <span data-ttu-id="65db9-199">In dit artikel V2VnetAllinOne.ps1 wordt aangeroepen, maar u kunt een andere naam.</span><span class="sxs-lookup"><span data-stu-id="65db9-199">In this article, it is called V2VnetAllinOne.ps1, but you can use another name.</span></span> <span data-ttu-id="65db9-200">Er zijn geen argumenten voor dit script.</span><span class="sxs-lookup"><span data-stu-id="65db9-200">There are no arguments for this script.</span></span> <span data-ttu-id="65db9-201">U gewoon uitvoeren het.</span><span class="sxs-lookup"><span data-stu-id="65db9-201">You simply run it.</span></span> <span data-ttu-id="65db9-202">Het eerste wat dat het script doet is gevraagd u aan te melden.</span><span class="sxs-lookup"><span data-stu-id="65db9-202">The first thing the script will do is prompt you to sign in.</span></span> <span data-ttu-id="65db9-203">Nadat u zich aanmeldt, wordt het script haalt gegevens over uw account en retourneert een lijst met abonnementen.</span><span class="sxs-lookup"><span data-stu-id="65db9-203">After you sign in, the script gets details about your account and returns a list of subscriptions.</span></span> <span data-ttu-id="65db9-204">De aanvraag om uw referenties niet meegerekend, weergegeven uitvoering van het oorspronkelijke script als volgt:</span><span class="sxs-lookup"><span data-stu-id="65db9-204">Not counting the request for your credentials, the initial script execution looks like this:</span></span>

    PS C:\Users\ccompy\Documents\VNET> .\V2VnetAllInOne.ps1
    Please Login

    Environment           : AzureCloud
    Account               : ccompy@microsoft.com
    TenantId              : 722278f-fef1-499f-91ab-2323d011db47
    SubscriptionId        : af5358e1-acac-2c90-a9eb-722190abf47a
    CurrentStorageAccount :

    Choose a subscription

    1) <span data-ttu-id="65db9-205">Demo-abonnement (af5358e1-acac-2c90-a9eb-722190abf47a)</span><span class="sxs-lookup"><span data-stu-id="65db9-205">Demo Subscription (af5358e1-acac-2c90-a9eb-722190abf47a)</span></span>
    2) <span data-ttu-id="65db9-206">MS-Test (a5350f55-dd5a-41ec-2ddb-ff7b911bb2ef)</span><span class="sxs-lookup"><span data-stu-id="65db9-206">MS Test (a5350f55-dd5a-41ec-2ddb-ff7b911bb2ef)</span></span>
    3) <span data-ttu-id="65db9-207">Paarse Demo-abonnement (2d4c99a4-57f9-4d5e-a0a1-0034c52db59d)</span><span class="sxs-lookup"><span data-stu-id="65db9-207">Purple Demo Subscription (2d4c99a4-57f9-4d5e-a0a1-0034c52db59d)</span></span>

    <span data-ttu-id="65db9-208">Kies een optie: 3</span><span class="sxs-lookup"><span data-stu-id="65db9-208">Choose an option: 3</span></span>

    <span data-ttu-id="65db9-209">Account: ccompy@microsoft.com omgeving: AzureCloud abonnement: 2d4c99a4-57f9-4d5e-a0a1-0034c52db59d Tenant: 722278f-fef1-499f-91ab-2323d011db47</span><span class="sxs-lookup"><span data-stu-id="65db9-209">Account      : ccompy@microsoft.com Environment  : AzureCloud Subscription : 2d4c99a4-57f9-4d5e-a0a1-0034c52db59d Tenant       : 722278f-fef1-499f-91ab-2323d011db47</span></span>

    <span data-ttu-id="65db9-210">Geef de resourcegroep van uw App: Geef de naam van uw App hcdemo rg: v2vnetpowershell wat wilt u doen?</span><span class="sxs-lookup"><span data-stu-id="65db9-210">Please enter the Resource Group of your App: hcdemo-rg Please enter the Name of your App: v2vnetpowershell What do you want to do?</span></span>

    1) <span data-ttu-id="65db9-211">Een nieuw virtueel netwerk toevoegen aan een App</span><span class="sxs-lookup"><span data-stu-id="65db9-211">Add a NEW Virtual Network to an App</span></span>
    2) <span data-ttu-id="65db9-212">Een bestaand virtueel netwerk toevoegen aan een App</span><span class="sxs-lookup"><span data-stu-id="65db9-212">Add an EXISTING Virtual Network to an App</span></span>
    3) <span data-ttu-id="65db9-213">Een virtueel netwerk verwijderen uit een App</span><span class="sxs-lookup"><span data-stu-id="65db9-213">Remove a Virtual Network from an App</span></span>

<span data-ttu-id="65db9-214">De rest van dit gedeelte wordt elk van deze drie opties.</span><span class="sxs-lookup"><span data-stu-id="65db9-214">The rest of this section explains each of those three options.</span></span>

### <a name="create-a-resource-manager-vnet-and-integrate-with-it"></a><span data-ttu-id="65db9-215">Een Resource Manager VNet maken en integreren met het</span><span class="sxs-lookup"><span data-stu-id="65db9-215">Create a Resource Manager VNet and integrate with it</span></span>
<span data-ttu-id="65db9-216">Voor het maken van een nieuwe virtuele netwerk dat gebruikmaakt van het implementatiemodel van Resource Manager en het integreren met uw app, selecteer **1) een nieuw virtueel netwerk toevoegen aan een App**.</span><span class="sxs-lookup"><span data-stu-id="65db9-216">To create a new virtual network that uses the Resource Manager deployment model and integrate it with your app, select **1) Add a NEW Virtual Network to an App**.</span></span> <span data-ttu-id="65db9-217">Hiermee wordt u gevraagd om de naam van het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="65db9-217">This will prompt you for the name of the virtual network.</span></span> <span data-ttu-id="65db9-218">In mijn geval, zoals u in de volgende instellingen ziet gebruikt ik de naam van de v2pshell.</span><span class="sxs-lookup"><span data-stu-id="65db9-218">In my case, as you can see in the following settings, I used the name, v2pshell.</span></span>

<span data-ttu-id="65db9-219">Het script geeft de informatie over het virtuele netwerk dat wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="65db9-219">The script gives the details about the virtual network that's being created.</span></span> <span data-ttu-id="65db9-220">Als ik wil, kan ik een van de waarden te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="65db9-220">If I want, I can change any of the values.</span></span> <span data-ttu-id="65db9-221">In dit voorbeeld wordt uitgevoerd, moet ik een virtueel netwerk met de volgende instellingen gemaakt:</span><span class="sxs-lookup"><span data-stu-id="65db9-221">In this example execution, I created a virtual network that has the following settings:</span></span>

    Virtual Network Name:         v2pshell
    Resource Group Name:          hcdemo-rg
    Gateway Name:                 v2pshell-gateway
    Vnet IP name:                 v2pshell-ip
    Vnet IP config name:          v2pshell-ipconf
    Address Space:                10.0.0.0/8
    Gateway Address Space:        10.5.0.0/16
    Point-To-Site Address Space:  172.16.0.0/12

    Do you wish to change these settings?
    [Y] Yes  [N] No  [?] Help (default is "N"):

<span data-ttu-id="65db9-222">Als u wijzigen van de waarden wilt, typt u **Y** en wijzigingen aanbrengen.</span><span class="sxs-lookup"><span data-stu-id="65db9-222">If you want to change any of the values, type **Y** and make the changes.</span></span> <span data-ttu-id="65db9-223">Wanneer u tevreden over de instellingen van het virtuele netwerk bent, typt u **N** of drukt u op Enter wanneer u wordt gevraagd over het wijzigen van de instellingen.</span><span class="sxs-lookup"><span data-stu-id="65db9-223">When you are happy with the virtual network settings, type **N** or simply press Enter when prompted about changing the settings.</span></span> <span data-ttu-id="65db9-224">Vanaf dat moment tot voltooiing, het script vertelt u enkele van wat de it' i's doen totdat het begint te maken van de virtuele netwerkgateway.</span><span class="sxs-lookup"><span data-stu-id="65db9-224">From there on until completion, the script will tell you some of what it' i's doing until it starts to create the virtual network gateway.</span></span> <span data-ttu-id="65db9-225">Deze stap kan een uur duren.</span><span class="sxs-lookup"><span data-stu-id="65db9-225">That step can take up to an hour.</span></span> <span data-ttu-id="65db9-226">Er is geen voortgangsindicator tijdens deze fase, maar het script kunt u weten wanneer de gateway is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="65db9-226">There is no progress indicator during this phase, but the script will let you know when the gateway has been created.</span></span>

<span data-ttu-id="65db9-227">Wanneer het script is voltooid, wordt er **voltooid**.</span><span class="sxs-lookup"><span data-stu-id="65db9-227">When the script finishes, it will say **Finished**.</span></span> <span data-ttu-id="65db9-228">Op dit moment hebt u een Resource Manager virtueel netwerk met de naam en de instellingen die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="65db9-228">At this point, you will have a Resource Manager virtual network that has the name and settings that you selected.</span></span> <span data-ttu-id="65db9-229">Deze nieuwe virtuele netwerk wordt ook worden geïntegreerd met uw app.</span><span class="sxs-lookup"><span data-stu-id="65db9-229">This new virtual network will also be integrated with your app.</span></span>

### <a name="integrate-your-app-with-a-preexisting-resource-manager-vnet"></a><span data-ttu-id="65db9-230">Uw app integreren met een bestaande Resource Manager VNet</span><span class="sxs-lookup"><span data-stu-id="65db9-230">Integrate your app with a preexisting Resource Manager VNet</span></span>
<span data-ttu-id="65db9-231">Wanneer u met een bestaand virtueel netwerk, integreren bent als u een Resource Manager virtueel netwerk dat geen gateway of punt-naar-site-connectiviteit bieden, wordt het script ingesteld die.</span><span class="sxs-lookup"><span data-stu-id="65db9-231">When you're integrating with a preexisting virtual network, if you provide a Resource Manager virtual network that doesn’t have a gateway or point-to-site connectivity, the script will set that up.</span></span> <span data-ttu-id="65db9-232">Als het VNET al deze dingen instellen, gaat het script meteen naar de app-integratie.</span><span class="sxs-lookup"><span data-stu-id="65db9-232">If the VNET already has those things set up, the script goes straight to the app integration.</span></span> <span data-ttu-id="65db9-233">Om te starten, selecteert u de **2) een bestaand virtueel netwerk toevoegen aan een App**.</span><span class="sxs-lookup"><span data-stu-id="65db9-233">To start this process, simply select **2) Add an EXISTING Virtual Network to an App**.</span></span>

<span data-ttu-id="65db9-234">Deze optie werkt alleen als u een bestaand virtueel netwerk voor Resource Manager, dat zich in hetzelfde abonnement als uw app.</span><span class="sxs-lookup"><span data-stu-id="65db9-234">This option works only if you have a preexisting Resource Manager virtual network that is in the same subscription as your app.</span></span> <span data-ttu-id="65db9-235">Nadat u de optie selecteert, wordt er verschijnt een lijst met uw virtuele netwerken van Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="65db9-235">After you select the option, you will be presented with a list of your Resource Manager virtual networks.</span></span>   

    Select a VNET to integrate with

    1) <span data-ttu-id="65db9-236">v2demonetwork</span><span class="sxs-lookup"><span data-stu-id="65db9-236">v2demonetwork</span></span>
    2) <span data-ttu-id="65db9-237">v2pshell</span><span class="sxs-lookup"><span data-stu-id="65db9-237">v2pshell</span></span>
    3) <span data-ttu-id="65db9-238">v2vnetintdemo</span><span class="sxs-lookup"><span data-stu-id="65db9-238">v2vnetintdemo</span></span>
    4) <span data-ttu-id="65db9-239">v2asenetwork</span><span class="sxs-lookup"><span data-stu-id="65db9-239">v2asenetwork</span></span>
    5) <span data-ttu-id="65db9-240">v2pshell2</span><span class="sxs-lookup"><span data-stu-id="65db9-240">v2pshell2</span></span>

    <span data-ttu-id="65db9-241">Kies een optie: 5</span><span class="sxs-lookup"><span data-stu-id="65db9-241">Choose an option: 5</span></span>

<span data-ttu-id="65db9-242">Het virtuele netwerk dat u integreren wilt met eenvoudig kunt selecteren.</span><span class="sxs-lookup"><span data-stu-id="65db9-242">Simply select the virtual network that you want to integrate with.</span></span> <span data-ttu-id="65db9-243">Als u al een gateway die voor punt-naar-site-connectiviteit is ingeschakeld, wordt het script gewoon uw app integreren met het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="65db9-243">If you already have a gateway that has point-to-site connectivity enabled, the script will simply integrate your app with your virtual network.</span></span> <span data-ttu-id="65db9-244">Als u een gateway niet hebt, moet u het gatewaysubnet opgeven.</span><span class="sxs-lookup"><span data-stu-id="65db9-244">If you do not have a gateway, you will need to specify the gateway subnet.</span></span> <span data-ttu-id="65db9-245">Het gatewaysubnet moet in de adresruimte van uw virtuele netwerk en deze kan niet in een ander subnet.</span><span class="sxs-lookup"><span data-stu-id="65db9-245">Your gateway subnet must be in your virtual network address space, and it cannot be in any other subnet.</span></span> <span data-ttu-id="65db9-246">Als u een virtueel netwerk zonder een gateway hebt en deze stap uitvoert, dingen moeten uitzien:</span><span class="sxs-lookup"><span data-stu-id="65db9-246">If you have a virtual network without a gateway and run this step, things look like this:</span></span>

    This Virtual Network has no gateway. I will need to create one.
    Your VNET is in the address space 172.16.0.0/16, with the following Subnets:
    default: 172.16.0.0/24
    Please choose a GatewaySubnet address space: 172.16.1.0/26

<span data-ttu-id="65db9-247">In dit voorbeeld moet ik een virtuele netwerkgateway met de volgende instellingen gemaakt:</span><span class="sxs-lookup"><span data-stu-id="65db9-247">In this example, I created a virtual network gateway that has the following settings:</span></span>

    Virtual Network Name:         v2pshell2
    Resource Group Name:          vnetdemo-rg
    Gateway Name:                 v2pshell2-gateway
    Vnet IP name:                 v2pshell2-ip
    Vnet IP config name:          v2pshell2-ipconf
    Address Space:                172.16.0.0/16
    Gateway Address Space:        172.16.1.0/26
    Point-To-Site Address Space:  172.16.0.0/12

    Do you wish to change these settings?
    [Y] Yes  [N] No  [?] Help (default is "N"):
    Creating App association to VNET

<span data-ttu-id="65db9-248">Als u een van deze instellingen wijzigt wilt, kunt u dit doet.</span><span class="sxs-lookup"><span data-stu-id="65db9-248">If you want to change any of those settings, you can do so.</span></span> <span data-ttu-id="65db9-249">Anders, druk op Enter en het script wordt gemaakt van uw gateway en uw app koppelen aan het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="65db9-249">Otherwise, press Enter and the script will create your gateway and attach your app to your virtual network.</span></span> <span data-ttu-id="65db9-250">De aanmaaktijd van de gateway is echter nog steeds een uur, dus zorg ervoor dat u die rekening houden.</span><span class="sxs-lookup"><span data-stu-id="65db9-250">The gateway creation time is still an hour, though, so make sure you keep that in mind.</span></span> <span data-ttu-id="65db9-251">Als alles is voltooid, het script dicteert **voltooid**.</span><span class="sxs-lookup"><span data-stu-id="65db9-251">When everything is finished, the script will say **Finished**.</span></span>

### <a name="disconnect-your-app-from-a-resource-manager-vnet"></a><span data-ttu-id="65db9-252">Verbreek de verbinding tussen uw app een Resource Manager VNet</span><span class="sxs-lookup"><span data-stu-id="65db9-252">Disconnect your app from a Resource Manager VNet</span></span>
<span data-ttu-id="65db9-253">Het virtuele netwerk van uw app verbreken niet noteren de gateway of punt-naar-site-connectiviteit uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="65db9-253">Disconnecting your app from your virtual network does not take down the gateway or disable point-to-site connectivity.</span></span> <span data-ttu-id="65db9-254">U, nadat alle gebruikt deze voor iets anders.</span><span class="sxs-lookup"><span data-stu-id="65db9-254">You might, after all, be using it for something else.</span></span> <span data-ttu-id="65db9-255">Deze wordt ook niet verbroken deze van alle andere apps dan die u hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="65db9-255">It also does not disconnect it from any other apps other than the one you provided.</span></span> <span data-ttu-id="65db9-256">Om deze actie niet uitvoeren, selecteert u **3) een virtueel netwerk verwijderen uit een App**.</span><span class="sxs-lookup"><span data-stu-id="65db9-256">To perform this action, select **3) Remove a Virtual Network from an App**.</span></span> <span data-ttu-id="65db9-257">Als u doet dit, ziet u ongeveer het volgende:</span><span class="sxs-lookup"><span data-stu-id="65db9-257">When you do so, you will see something like this:</span></span>

    Currently connected to VNET v2pshell

    Confirm
    Are you sure you want to delete the following resource:
    /subscriptions/edcc99a4-b7f9-4b5e-a9a1-3034c51db496/resourceGroups/hcdemo-rg/providers/Microsoft.Web/sites/v2vnetpowers
    hell/virtualNetworkConnections/v2pshell
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):

<span data-ttu-id="65db9-258">Hoewel het script verwijderen staat, verwijdert het virtuele netwerk niet meer.</span><span class="sxs-lookup"><span data-stu-id="65db9-258">Although the script says delete, it does not delete the virtual network.</span></span> <span data-ttu-id="65db9-259">Het worden zojuist de integratie verwijderd.</span><span class="sxs-lookup"><span data-stu-id="65db9-259">It’s just removing the integration.</span></span> <span data-ttu-id="65db9-260">Nadat u bevestigen dat dit is wat u wilt doen, de opdracht erg snel wordt verwerkt en vertelt u **True** wanneer het is voltooid.</span><span class="sxs-lookup"><span data-stu-id="65db9-260">After you confirm that this is what you want to do, the command is processed quite quickly and tells you **True** when it is done.</span></span>

<!--Links-->
[createvpngateway]: http://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/
[azureportal]: http://portal.azure.com
