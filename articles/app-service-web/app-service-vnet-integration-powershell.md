---
title: aaaConnect uw app tooyour virtueel netwerk met behulp van PowerShell
description: Instructies over hoe tooconnect tooand werken met virtuele netwerken met behulp van PowerShell
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
ms.openlocfilehash: c9d0fa99d02cab7b2c7211a1b2f7b7d0cd27ee8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-app-tooyour-virtual-network-by-using-powershell"></a><span data-ttu-id="2f375-103">Verbinding maken met uw app tooyour virtueel netwerk met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="2f375-103">Connect your app tooyour virtual network by using PowerShell</span></span>
## <a name="overview"></a><span data-ttu-id="2f375-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="2f375-104">Overview</span></span>
<span data-ttu-id="2f375-105">In Azure App Service kunt u uw app (web, mobiel of API) tooan virtuele Azure-netwerk (VNet) in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="2f375-105">In Azure App Service, you can connect your app (web, mobile, or API) tooan Azure virtual network (VNet) in your subscription.</span></span> <span data-ttu-id="2f375-106">Deze functie is aangeroepen VNet-integratie.</span><span class="sxs-lookup"><span data-stu-id="2f375-106">This feature is called VNet Integration.</span></span> <span data-ttu-id="2f375-107">Verwar Hallo VNet-integratiefunctie niet met de functie App Service-omgeving hello, zodat u toorun een exemplaar van Azure App Service in uw virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="2f375-107">hello VNet Integration feature should not be confused with hello App Service Environment feature, which allows you toorun an instance of Azure App Service in your virtual network.</span></span>

<span data-ttu-id="2f375-108">Hallo VNet-integratiefunctie heeft een gebruikersinterface (UI) in de nieuwe portal Hallo dat u toointegrate met virtuele netwerken die zijn geïmplementeerd gebruiken kunt met behulp van het klassieke implementatiemodel Hallo of hello Azure Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="2f375-108">hello VNet Integration feature has a user interface (UI) in hello new portal that you can use toointegrate with virtual networks that are deployed by using either hello classic deployment model or hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="2f375-109">Als u meer informatie over de functie Hallo toolearn wilt, Zie [uw app integreren met een Azure-netwerk](web-sites-integrate-with-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="2f375-109">If you want toolearn more about hello feature, see [Integrate your app with an Azure virtual network](web-sites-integrate-with-vnet.md).</span></span>

<span data-ttu-id="2f375-110">In dit artikel wordt niet over hoe toouse UI hello, maar in plaats daarvan over het tooenable integratie met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2f375-110">This article is not about how toouse hello UI but rather about how tooenable integration by using PowerShell.</span></span> <span data-ttu-id="2f375-111">Omdat het Hallo-opdrachten voor elk implementatiemodel verschillend zijn, heeft dit artikel een sectie voor elke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="2f375-111">Because hello commands for each deployment model are different, this article has a section for each deployment model.</span></span>  

<span data-ttu-id="2f375-112">Controleer voordat u met dit artikel doorgaat, dat u hebt:</span><span class="sxs-lookup"><span data-stu-id="2f375-112">Before you continue with this article, ensure that you have:</span></span>

* <span data-ttu-id="2f375-113">Hallo die nieuwste Azure PowerShell-SDK geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="2f375-113">hello latest Azure PowerShell SDK installed.</span></span> <span data-ttu-id="2f375-114">U kunt dit installeren met de Hallo Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="2f375-114">You can install this with hello Web Platform Installer.</span></span>
* <span data-ttu-id="2f375-115">Een app in Azure App Service wordt uitgevoerd op een Standard of Premium-SKU.</span><span class="sxs-lookup"><span data-stu-id="2f375-115">An app in Azure App Service running in a Standard or Premium SKU.</span></span>

## <a name="classic-virtual-networks"></a><span data-ttu-id="2f375-116">Klassieke virtuele netwerken</span><span class="sxs-lookup"><span data-stu-id="2f375-116">Classic virtual networks</span></span>
<span data-ttu-id="2f375-117">Deze sectie wordt uitgelegd drie taken voor virtuele netwerken die gebruikmaken van het klassieke implementatiemodel Hallo:</span><span class="sxs-lookup"><span data-stu-id="2f375-117">This section explains three tasks for virtual networks that use hello classic deployment model:</span></span>

1. <span data-ttu-id="2f375-118">Uw app tooa bestaande virtueel netwerk verbinden dat een gateway heeft en is geconfigureerd voor punt-naar-site-connectiviteit.</span><span class="sxs-lookup"><span data-stu-id="2f375-118">Connect your app tooa preexisting virtual network that has a gateway and is configured for point-to-site connectivity.</span></span>
2. <span data-ttu-id="2f375-119">Werk uw gegevens van de integratie van virtueel netwerk voor uw app.</span><span class="sxs-lookup"><span data-stu-id="2f375-119">Update your virtual network integration information for your app.</span></span>
3. <span data-ttu-id="2f375-120">Verbreek de verbinding tussen uw app in het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="2f375-120">Disconnect your app from your virtual network.</span></span>

### <a name="connect-an-app-tooa-classic-vnet"></a><span data-ttu-id="2f375-121">Verbinding maken met een app tooa klassieke VNet</span><span class="sxs-lookup"><span data-stu-id="2f375-121">Connect an app tooa classic VNet</span></span>
<span data-ttu-id="2f375-122">tooconnect een app tooa virtueel netwerk, volg deze drie stappen:</span><span class="sxs-lookup"><span data-stu-id="2f375-122">tooconnect an app tooa virtual network, follow these three steps:</span></span>

1. <span data-ttu-id="2f375-123">Declareren toohello web-app of moet deze aan een bepaald virtueel netwerk koppelen.</span><span class="sxs-lookup"><span data-stu-id="2f375-123">Declare toohello web app that it will be joining a particular virtual network.</span></span> <span data-ttu-id="2f375-124">Hallo-app een certificaat dat wordt verleend toohello virtueel netwerk voor punt-naar-site-connectiviteit gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="2f375-124">hello app will generate a certificate that will be given toohello virtual network for point-to-site connectivity.</span></span>
2. <span data-ttu-id="2f375-125">Hallo web app certificaat toohello virtueel netwerk uploaden en vervolgens Hallo punt-naar-site VPN-pakket-URI die worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="2f375-125">Upload hello web app certificate toohello virtual network, and then retrieve hello point-to-site VPN package URI.</span></span>
3. <span data-ttu-id="2f375-126">Hallo van web-app virtueel netwerkverbinding bijwerken met Hallo punt-naar-site de pakket-URI.</span><span class="sxs-lookup"><span data-stu-id="2f375-126">Update hello web app's virtual network connection with hello point-to-site package URI.</span></span>

<span data-ttu-id="2f375-127">Hello eerste en derde stappen zijn volledige scriptondersteuning mogelijk, maar de tweede stap Hallo vereist een eenmalige, handmatige actie via Hallo portal of toegang tooperform **plaatsen** of **PATCH** acties op Hallo virtueel netwerk Azure Resource Manager-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="2f375-127">hello first and third steps are fully scriptable, but hello second step requires a one-time, manual action through hello portal, or access tooperform **PUT** or **PATCH** actions on hello virtual network Azure Resource Manager endpoint.</span></span> <span data-ttu-id="2f375-128">Neem contact op met ondersteuning van Azure toohave dit ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="2f375-128">Contact Azure Support toohave this enabled.</span></span> <span data-ttu-id="2f375-129">Voordat u begint, zorg ervoor dat er een klassiek virtueel netwerk met punt-naar-site-connectiviteit is ingeschakeld en een geïmplementeerde gateway.</span><span class="sxs-lookup"><span data-stu-id="2f375-129">Before you start, make sure that you have a classic virtual network that has point-to-site connectivity already enabled and a deployed gateway.</span></span> <span data-ttu-id="2f375-130">toocreate hello gateway en schakel punt-naar-site-connectiviteit, moet u toouse Hallo portal zoals beschreven op [maken van een VPN-gateway][createvpngateway].</span><span class="sxs-lookup"><span data-stu-id="2f375-130">toocreate hello gateway and enable point-to-site connectivity, you need toouse hello portal as described at [Creating a VPN gateway][createvpngateway].</span></span>

<span data-ttu-id="2f375-131">Hallo klassiek virtueel netwerk moet toobe in Hallo hetzelfde abonnement als uw App-Service die blokkeringen Hallo-app die u integreert met plant.</span><span class="sxs-lookup"><span data-stu-id="2f375-131">hello classic virtual network needs toobe in hello same subscription as your App Service plan that holds hello app that you are integrating with.</span></span>

##### <a name="set-up-azure-powershell-sdk"></a><span data-ttu-id="2f375-132">Instellen van Azure PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="2f375-132">Set up Azure PowerShell SDK</span></span>
<span data-ttu-id="2f375-133">Open een PowerShell-venster en instellen van uw Azure-account en abonnement met behulp van:</span><span class="sxs-lookup"><span data-stu-id="2f375-133">Open a PowerShell window and set up your Azure account and subscription by using:</span></span>

    Login-AzureRmAccount

<span data-ttu-id="2f375-134">Deze opdracht wordt een prompt tooget geopend uw Azure-referenties.</span><span class="sxs-lookup"><span data-stu-id="2f375-134">That command will open a prompt tooget your Azure credentials.</span></span> <span data-ttu-id="2f375-135">Nadat u zich aanmeldt, kunt een van de volgende opdrachten tooselect Hallo abonnement dat u wilt dat toouse hello te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2f375-135">After you sign in, use either of hello following commands tooselect hello subscription that you want toouse.</span></span> <span data-ttu-id="2f375-136">Zorg ervoor dat u van Hallo abonnement die uw virtuele netwerk en de App Service-abonnement gebruikmaakt in.</span><span class="sxs-lookup"><span data-stu-id="2f375-136">Make sure that you are using hello subscription that your virtual network and App Service plan are in.</span></span>

    Select-AzureRmSubscription –SubscriptionName [WebAppSubscriptionName]

<span data-ttu-id="2f375-137">of</span><span class="sxs-lookup"><span data-stu-id="2f375-137">or</span></span>

    Select-AzureRmSubscription –SubscriptionId [WebAppSubscriptionId]

##### <a name="variables-used-in-this-article"></a><span data-ttu-id="2f375-138">Variabelen die in dit artikel worden gebruikt</span><span class="sxs-lookup"><span data-stu-id="2f375-138">Variables used in this article</span></span>
<span data-ttu-id="2f375-139">toosimplify opdrachten, zullen een **$Configuration** PowerShell variabele met de Hallo specifieke configuratie.</span><span class="sxs-lookup"><span data-stu-id="2f375-139">toosimplify commands, we will set a **$Configuration** PowerShell variable with hello specific configuration.</span></span>

<span data-ttu-id="2f375-140">Een variabele als volgt instellen in PowerShell Hello volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="2f375-140">Set a variable as follows in PowerShell with hello following parameters:</span></span>

    $Configuration = @{}
    $Configuration.WebAppResourceGroup = "[Your web app resource group]"
    $Configuration.WebAppName = "[Your web app name]"
    $Configuration.VnetSubscriptionId = "[Your vnet subscription id]"
    $Configuration.VnetResourceGroup = "[Your vnet resource group]"
    $Configuration.VnetName = "[Your vnet name]"

<span data-ttu-id="2f375-141">Hallo app locatie moet Hallo locatie zonder spaties.</span><span class="sxs-lookup"><span data-stu-id="2f375-141">hello app location should be hello location without any spaces.</span></span> <span data-ttu-id="2f375-142">Bijvoorbeeld, is VS-West westus.</span><span class="sxs-lookup"><span data-stu-id="2f375-142">For example, West US is westus.</span></span>

    $Configuration.WebAppLocation = "[Your web app Location]"

<span data-ttu-id="2f375-143">het volgende item Hallo is waar Hallo certificaat moet worden geschreven.</span><span class="sxs-lookup"><span data-stu-id="2f375-143">hello next item is where hello certificate should be written.</span></span> <span data-ttu-id="2f375-144">Deze moet een pad op de lokale computer.</span><span class="sxs-lookup"><span data-stu-id="2f375-144">It should be a writable path on your local computer.</span></span> <span data-ttu-id="2f375-145">Zorg ervoor dat tooinclude .cer Hallo achter.</span><span class="sxs-lookup"><span data-stu-id="2f375-145">Make sure tooinclude .cer at hello end.</span></span>

    $Configuration.GeneratedCertificatePath = "[C:\Path\To\Certificate.cer]"

<span data-ttu-id="2f375-146">toosee ingesteld, type **$Configuration**.</span><span class="sxs-lookup"><span data-stu-id="2f375-146">toosee what you set, type **$Configuration**.</span></span>

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

<span data-ttu-id="2f375-147">Hallo rest van deze sectie wordt ervan uitgegaan dat u een variabele die is gemaakt als NET beschreven hebt.</span><span class="sxs-lookup"><span data-stu-id="2f375-147">hello rest of this section assumes that you have a variable created as just described.</span></span>

##### <a name="declare-hello-virtual-network-toohello-app"></a><span data-ttu-id="2f375-148">Hallo virtueel netwerk toohello app declareren</span><span class="sxs-lookup"><span data-stu-id="2f375-148">Declare hello virtual network toohello app</span></span>
<span data-ttu-id="2f375-149">Gebruik hello volgt opdracht tootell Hallo app dat deze dit bepaalde virtuele netwerk wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="2f375-149">Use hello following command tootell hello app that it will be using this particular virtual network.</span></span> <span data-ttu-id="2f375-150">Hierdoor wordt Hallo app toogenerate benodigde certificaten:</span><span class="sxs-lookup"><span data-stu-id="2f375-150">This will cause hello app toogenerate necessary certificates:</span></span>

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -PropertyObject @{"VnetResourceId" = "/subscriptions/$($Configuration.VnetSubscriptionId)/resourceGroups/$($Configuration.VnetResourceGroup)/providers/Microsoft.ClassicNetwork/virtualNetworks/$($Configuration.VnetName)"} -Location $Configuration.WebAppLocation -ApiVersion 2015-07-01

<span data-ttu-id="2f375-151">Als u deze opdracht is geslaagd, **$vnet** moet een **eigenschappen** in deze variabele.</span><span class="sxs-lookup"><span data-stu-id="2f375-151">If this command succeeds, **$vnet** should have a **Properties** variable in it.</span></span> <span data-ttu-id="2f375-152">Hallo **eigenschappen** variabele moet zowel een certificaat vingerafdruk en Hallo certificaatgegevens bevatten.</span><span class="sxs-lookup"><span data-stu-id="2f375-152">hello **Properties** variable should contain both a certificate thumbprint and hello certificate data.</span></span>

##### <a name="upload-hello-web-app-certificate-toohello-virtual-network"></a><span data-ttu-id="2f375-153">Hallo web app certificaat toohello virtueel netwerk uploaden</span><span class="sxs-lookup"><span data-stu-id="2f375-153">Upload hello web app certificate toohello virtual network</span></span>
<span data-ttu-id="2f375-154">Een handmatige stap eenmalige is vereist voor elk abonnement en de combinatie van het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="2f375-154">A manual, one-time step is required for each subscription and virtual network combination.</span></span> <span data-ttu-id="2f375-155">Dat wil zeggen, als u apps in abonnement een tooVirtual netwerk een verbinding maakt, moet u toodo deze stap slechts eenmaal ongeacht hoeveel apps die u configureert.</span><span class="sxs-lookup"><span data-stu-id="2f375-155">That is, if you are connecting apps in Subscription A tooVirtual Network A, you will need toodo this step only once regardless of how many apps you configure.</span></span> <span data-ttu-id="2f375-156">Als u een nieuw virtueel netwerk van de app-tooanother toevoegt, moet u dit opnieuw toodo.</span><span class="sxs-lookup"><span data-stu-id="2f375-156">If you are adding a new app tooanother virtual network, you'll need toodo this again.</span></span> <span data-ttu-id="2f375-157">Hallo reden hiervoor is dat een set van certificaten wordt gegenereerd tijdens een abonnement in Azure App Service en Hallo set eenmaal voor elk virtueel netwerk dat Hallo apps maakt verbinding met wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="2f375-157">hello reason for this is that a set of certificates is generated at a subscription level in Azure App Service, and hello set is generated once for each virtual network that hello apps will connect to.</span></span>

<span data-ttu-id="2f375-158">Hallo certificaten wordt al zijn ingesteld als u deze stappen hebt gevolgd, of als u een geïntegreerd met Hallo hetzelfde virtuele netwerk met behulp van Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="2f375-158">hello certificates will have already been set if you followed these steps or if you integrated with hello same virtual network by using hello portal.</span></span>

<span data-ttu-id="2f375-159">de eerste stap Hallo is toogenerate Hallo cer-bestand.</span><span class="sxs-lookup"><span data-stu-id="2f375-159">hello first step is toogenerate hello .cer file.</span></span> <span data-ttu-id="2f375-160">de tweede stap Hallo is tooupload Hallo .cer-bestand tooyour virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="2f375-160">hello second step is tooupload hello .cer file tooyour virtual network.</span></span> <span data-ttu-id="2f375-161">toogenerate hello cer-bestand van Hallo API-aanroep in Hallo eerdere stap Hallo volgende opdrachten uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="2f375-161">toogenerate hello .cer file from hello API call in hello earlier step, run hello following commands.</span></span>

    $certBytes = [System.Convert]::FromBase64String($vnet.Properties.certBlob)
    [System.IO.File]::WriteAllBytes("$($Configuration.GeneratedCertificatePath)", $certBytes)

<span data-ttu-id="2f375-162">Hallo-certificaat worden gevonden op locatie Hallo die **$Configuration.GeneratedCertificatePath** bevat.</span><span class="sxs-lookup"><span data-stu-id="2f375-162">hello certificate will be found in hello location that **$Configuration.GeneratedCertificatePath** specifies.</span></span>

<span data-ttu-id="2f375-163">tooupload hello certificaat handmatig hello gebruiken [Azure-portal] [ azureportal] en **bladeren virtueel netwerk (klassiek)** > **VPN-verbindingen**  >  **Punt-naar-site** > **certificaten beheren**.</span><span class="sxs-lookup"><span data-stu-id="2f375-163">tooupload hello certificate manually, use hello [Azure portal][azureportal] and **Browse Virtual Network (classic)** > **VPN connections** > **Point-to-site** > **Manage certificates**.</span></span> <span data-ttu-id="2f375-164">Hier kunt uw certificaat te uploaden.</span><span class="sxs-lookup"><span data-stu-id="2f375-164">From here, upload your certificate.</span></span>

##### <a name="get-hello-point-to-site-package"></a><span data-ttu-id="2f375-165">Hallo punt-naar-site-pakket</span><span class="sxs-lookup"><span data-stu-id="2f375-165">Get hello point-to-site package</span></span>
<span data-ttu-id="2f375-166">Hallo volgende stap bij het instellen van een virtueel netwerkverbinding op een web-app is tooget Hallo punt-naar-site-pakket en geef deze tooyour web-app.</span><span class="sxs-lookup"><span data-stu-id="2f375-166">hello next step in setting up a virtual network connection on a web app is tooget hello point-to-site package and provide it tooyour web app.</span></span>

<span data-ttu-id="2f375-167">Sla Hallo volgende sjabloonbestand tooa aangeroepen GetNetworkPackageUri.json ergens op uw computer, bijvoorbeeld C:\Azure\Templates\GetNetworkPackageUri.json.</span><span class="sxs-lookup"><span data-stu-id="2f375-167">Save hello following template tooa file called GetNetworkPackageUri.json somewhere on your computer, for example, C:\Azure\Templates\GetNetworkPackageUri.json.</span></span>

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


<span data-ttu-id="2f375-168">Invoerparameters instellen:</span><span class="sxs-lookup"><span data-stu-id="2f375-168">Set input parameters:</span></span>

    $parameters = @{"certData" = $vnet.Properties.certBlob ;
    certThumbprint = $vnet.Properties.certThumbprint ;
    "networkName" = $Configuration.VnetName }

<span data-ttu-id="2f375-169">Roep Hallo script:</span><span class="sxs-lookup"><span data-stu-id="2f375-169">Call hello script:</span></span>

    $output = New-AzureRmResourceGroupDeployment -Name unused -ResourceGroupName $Configuration.VnetResourceGroup -TemplateParameterObject $parameters -TemplateFile C:\PATH\TO\GetNetworkPackageUri.json


<span data-ttu-id="2f375-170">Hallo variabele **$output. Outputs.packageUri** bevat nu Hallo pakket URI toobe gegeven tooyour web-app.</span><span class="sxs-lookup"><span data-stu-id="2f375-170">hello variable **$output.Outputs.packageUri** will now contain hello package URI toobe given tooyour web app.</span></span>

##### <a name="upload-hello-point-to-site-package-tooyour-app"></a><span data-ttu-id="2f375-171">Hallo punt-naar-site pakket tooyour app uploaden</span><span class="sxs-lookup"><span data-stu-id="2f375-171">Upload hello point-to-site package tooyour app</span></span>
<span data-ttu-id="2f375-172">de laatste stap Hallo is tooprovide Hallo app met dit pakket.</span><span class="sxs-lookup"><span data-stu-id="2f375-172">hello final step is tooprovide hello app with this package.</span></span> <span data-ttu-id="2f375-173">De volgende opdracht Hallo voert u eenvoudigweg:</span><span class="sxs-lookup"><span data-stu-id="2f375-173">Simply run hello next command:</span></span>

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)/primary" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-07-01 -PropertyObject @{"VnetName" = $Configuration.VnetName ; "VpnPackageUri" = $($output.Outputs.packageUri).Value } -Location $Configuration.WebAppLocation

<span data-ttu-id="2f375-174">Als een bericht gevraagd tooconfirm dat u een bestaande resource wilt overschrijven, moet u ervoor dat tooallow deze.</span><span class="sxs-lookup"><span data-stu-id="2f375-174">If a message asks you tooconfirm that you are overwriting an existing resource, make sure tooallow it.</span></span>

<span data-ttu-id="2f375-175">Nadat deze opdracht is geslaagd, moet uw app nu verbonden toohello virtueel netwerk zijn.</span><span class="sxs-lookup"><span data-stu-id="2f375-175">After this command succeeds, your app should now be connected toohello virtual network.</span></span> <span data-ttu-id="2f375-176">tooconfirm geslaagd, gaat u tooyour app-console en typt u de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="2f375-176">tooconfirm success, go tooyour app console, and type hello following:</span></span>

    SET WEBSITE_

<span data-ttu-id="2f375-177">Als er een omgevingsvariabele WEBSITE_VNETNAME die heeft een waarde die overeenkomt met de naam Hallo Hallo doel virtueel netwerk genoemd, worden alle configuraties zijn geslaagd.</span><span class="sxs-lookup"><span data-stu-id="2f375-177">If there is an environment variable called WEBSITE_VNETNAME that has a value that matches hello name of hello target virtual network, all configurations have succeeded.</span></span>

### <a name="update-classic-vnet-integration-information"></a><span data-ttu-id="2f375-178">Klassieke VNet integratie-informatie bijwerken</span><span class="sxs-lookup"><span data-stu-id="2f375-178">Update classic VNet integration information</span></span>
<span data-ttu-id="2f375-179">tooupdate of uw gegevens synchroniseren, herhaalt Hallo stappen die u tijdens het maken van Hallo-integratie in de eerste plaats Hallo gevolgd.</span><span class="sxs-lookup"><span data-stu-id="2f375-179">tooupdate or resync your information, simply repeat hello steps that you followed when you created hello integration in hello first place.</span></span> <span data-ttu-id="2f375-180">Deze stappen zijn:</span><span class="sxs-lookup"><span data-stu-id="2f375-180">Those steps are:</span></span>

1. <span data-ttu-id="2f375-181">Definieer uw configuratie-informatie.</span><span class="sxs-lookup"><span data-stu-id="2f375-181">Define your configuration information.</span></span>
2. <span data-ttu-id="2f375-182">Hallo virtueel netwerk toohello app declareren.</span><span class="sxs-lookup"><span data-stu-id="2f375-182">Declare hello virtual network toohello app.</span></span>
3. <span data-ttu-id="2f375-183">Hallo punt-naar-site package ophalen.</span><span class="sxs-lookup"><span data-stu-id="2f375-183">Get hello point-to-site package.</span></span>
4. <span data-ttu-id="2f375-184">Hallo punt-naar-site pakket tooyour app uploaden.</span><span class="sxs-lookup"><span data-stu-id="2f375-184">Upload hello point-to-site package tooyour app.</span></span>

### <a name="disconnect-your-app-from-a-classic-vnet"></a><span data-ttu-id="2f375-185">Verbreek de verbinding tussen uw app een klassiek VNet</span><span class="sxs-lookup"><span data-stu-id="2f375-185">Disconnect your app from a classic VNet</span></span>
<span data-ttu-id="2f375-186">toodisconnect hello app, moet u Hallo configuratie-informatie die is ingesteld tijdens de integratie van virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="2f375-186">toodisconnect hello app, you need hello configuration information that was set during virtual network integration.</span></span> <span data-ttu-id="2f375-187">Deze gegevens niet gebruiken, zich vervolgens één opdracht toodisconnect uw app uit het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="2f375-187">Using that information, there is then one command toodisconnect your app from your virtual network.</span></span>

    $vnet = Remove-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-07-01

## <a name="resource-manager-virtual-networks"></a><span data-ttu-id="2f375-188">Virtuele netwerken van Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2f375-188">Resource Manager virtual networks</span></span>
<span data-ttu-id="2f375-189">Virtuele netwerken van Resource Manager hebben Azure Resource Manager-API's die bepaalde processen in vergelijking met het klassieke virtuele netwerken vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="2f375-189">Resource Manager virtual networks have Azure Resource Manager APIs, which simplify some processes when compared with classic virtual networks.</span></span> <span data-ttu-id="2f375-190">Wij hebben een script dat u kunt Hallo volgende taken voltooien:</span><span class="sxs-lookup"><span data-stu-id="2f375-190">We have a script that will help you complete hello following tasks:</span></span>

* <span data-ttu-id="2f375-191">Een virtueel netwerk van Resource Manager maken en uw app integreren.</span><span class="sxs-lookup"><span data-stu-id="2f375-191">Create a Resource Manager virtual network and integrate your app with it.</span></span>
* <span data-ttu-id="2f375-192">Maken van een gateway, punt-naar-site-connectiviteit in een bestaande Resource Manager virtueel netwerk configureren en vervolgens uw app integreren met het.</span><span class="sxs-lookup"><span data-stu-id="2f375-192">Create a gateway, configure point-to-site connectivity in a preexisting Resource Manager virtual network, and then integrate your app with it.</span></span>
* <span data-ttu-id="2f375-193">Uw app integreren met een bestaand virtueel netwerk voor Resource Manager, dat een gateway en een punt-naar-site-connectiviteit ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="2f375-193">Integrate your app with a preexisting Resource Manager virtual network that has a gateway and point-to-site connectivity enabled.</span></span>
* <span data-ttu-id="2f375-194">Verbreek de verbinding tussen uw app in het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="2f375-194">Disconnect your app from your virtual network.</span></span>

### <a name="resource-manager-vnet-app-service-integration-script"></a><span data-ttu-id="2f375-195">Script voor Resource Manager VNet-App Service-integratie</span><span class="sxs-lookup"><span data-stu-id="2f375-195">Resource Manager VNet App Service integration script</span></span>
<span data-ttu-id="2f375-196">Hallo volgende script en sla het bestand tooa kopiëren.</span><span class="sxs-lookup"><span data-stu-id="2f375-196">Copy hello following script and save it tooa file.</span></span> <span data-ttu-id="2f375-197">Als u niet dat toouse Hallo script wilt, kunt u gratis toolearn hieruit toosee hoe tooset mogelijkheden van met een virtueel netwerk van Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2f375-197">If you don’t want toouse hello script, feel free toolearn from it toosee how tooset things up with a Resource Manager virtual network.</span></span>

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

        Write-Host "Adding a root certificate toothis VNET"
        $root = New-AzureRmVpnClientRootCertificate -Name "AppServiceCertificate.cer" -PublicCertData $certificateData

        Write-Host "Creating Azure VNET Gateway. This may take up tooan hour."
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
            Write-Host "Currently, I will create a VNET with hello following settings:"
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
            $changeRequested = PromptYesNo "" "Do you wish toochange these settings?" 1

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

        # We create hello virtual network and add it here. hello way this works is:
        # 1) Add hello VNET association toohello App. This allows hello App toogenerate certificates, etc. for hello VNET.
        # 2) Create hello VNET and VNET gateway, add hello certificates, create hello public IP, etc., required for hello gateway
        # 3) Get hello VPN package from hello gateway and pass it back toohello App.

        $webApp = Get-AzureRmResource -ResourceName $webAppName -ResourceType "Microsoft.Web/sites" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup
        $location = $webApp.Location

        Write-Host "Creating App association tooVNET"
        $propertiesObject = @{
         "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($resourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnetName)"
        }
        $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnetName)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup -Force

        CreateVnet $resourceGroupName $vnetName $vnetAddressSpace $vnetGatewayAddressSpace $location

        CreateVnetGateway $resourceGroupName $vnetName $vnetIpName $location $vnetIpConfigName $vnetGatewayName $virtualNetwork.Properties.CertBlob $vnetPointToSiteAddressSpace

        Write-Host "Retrieving VPN Package and supplying tooApp"
        $packageUri = Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName -VirtualNetworkGatewayName $vnetGatewayName -ProcessorArchitecture Amd64
        
        # $packageUri may contain literal double-quotes at hello start and hello end of hello URL
        if($packageUri.Length -gt 0 -and $packageUri.Substring(0, 1) -eq '"' -and $packageUri.Substring($packageUri.Length - 1, 1) -eq '"')
        {
            $packageUri = $packageUri.Substring(1, $packageUri.Length - 2)
        }

        # Put hello VPN client configuration package onto hello App
        $PropertiesObject = @{
        "vnetName" = $VirtualNetworkName; "vpnPackageUri" = $packageUri
        }

        New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnetName)/primary" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup -Force

        Write-Host "Finished!"
    }

    function AddExistingVnet($subscriptionId, $resourceGroupName, $webAppName)
    {
        $ErrorActionPreference = "Stop";

        # At this point, hello gateway should be able toobe joined tooan App, but may require some minor tweaking. We will declare toohello App now toouse this VNET
        Write-Host "Getting App information"
        $webApp = Get-AzureRmResource -ResourceName $webAppName -ResourceType "Microsoft.Web/sites" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $location = $webApp.Location

        $webAppConfig = Get-AzureRmResource -ResourceName "$($webAppName)/web" -ResourceType "Microsoft.Web/sites/config" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $currentVnet = $webAppConfig.Properties.VnetName
        if($currentVnet -ne $null -and $currentVnet -ne "")
        {
            Write-Host "Currently connected tooVNET $currentVnet"
        }

        # Display existing vnets
        $vnets = Get-AzureRmVirtualNetwork
        $vnetNames = @()
        foreach($vnet in $vnets)
        {
            $vnetNames += $vnet.Name
        }

        Write-Host
        $vnet = PromptCustom "Select a VNET toointegrate with" $vnets $vnetNames

        # We need toocheck if this VNET is able toobe joined tooa App, based on following criteria
            # If there is no gateway, we can create one.
            # If there is a gateway:
                # It must be of type Vpn
                # It must be of VpnType RouteBased
                # If it doesn't have hello right certificate, we will need tooadd it.
                # If it doesn't have a point-to-site range, we will need tooadd it.

        $gatewaySubnet = $vnet.Subnets | Where-Object { $_.Name -eq "GatewaySubnet" }

        if($gatewaySubnet -eq $null -or $gatewaySubnet.IpConfigurations -eq $null -or $gatewaySubnet.IpConfigurations.Count -eq 0)
        {
            $ErrorActionPreference = "Continue";
            # There is no gateway. We need toocreate one.
            Write-Host "This Virtual Network has no gateway. I will need toocreate one."

            $vnetName = $vnet.Name
            $vnetGatewayName="$($vnetName)-gateway"
            $vnetIpName="$($vnetName)-ip"
            $vnetIpConfigName="$($vnetName)-ipconf"

            # Virtual Network settings
            $vnetAddressSpace="10.0.0.0/8"
            $vnetGatewayAddressSpace="10.5.0.0/16"
            $vnetPointToSiteAddressSpace="172.16.0.0/16"

            $changeRequested = 0

            Write-Host "Your VNET is in hello address space $($vnet.AddressSpace.AddressPrefixes), with hello following Subnets:"
            foreach($subnet in $vnet.Subnets)
            {
                Write-Host "$($subnet.Name): $($subnet.AddressPrefix)"
            }

            $vnetGatewayAddressSpace = Read-Host "Please choose a GatewaySubnet address space"

            while($changeRequested -eq 0)
            {
                Write-Host
                Write-Host "Currently, I will create a VNET gateway with hello following settings:"
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
                $changeRequested = PromptYesNo "" "Do you wish toochange these settings?" 1

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

            Write-Host "Creating App association tooVNET"
            $propertiesObject = @{
             "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($vnet.ResourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnetName)"
            }

            $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

            # If there is no gateway subnet, we need toocreate one.
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
                Write-Error "This gateway is not of hello Vpn type. It cannot be joined tooan App."
                return
            }

            if($gateway.VpnType -ne "RouteBased")
            {
                Write-Error "This gateways Vpn type is not RouteBased. It cannot be joined tooan App."
                return
            }

            if($gateway.VpnClientConfiguration -eq $null -or $gateway.VpnClientConfiguration.VpnClientAddressPool -eq $null)
            {
                Write-Host "This gateway does not have a Point-to-site Address Range. Please specify one in CIDR notation, e.g. 10.0.0.0/8"
                $pointToSiteAddress = Read-Host "Point-To-Site Address Space"
                Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $gateway.Name -VpnClientAddressPool $pointToSiteAddress
            }

            Write-Host "Creating App association tooVNET"
            $propertiesObject = @{
             "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($vnet.ResourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnet.Name)"
            }

            $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

            # We need toocheck if hello certificate here exists in hello gateway.
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

        # Now finish joining by getting hello VPN package and giving it toohello App
        Write-Host "Retrieving VPN Package and supplying tooApp"
        $packageUri = Get-AzureRmVpnClientPackage -ResourceGroupName $vnet.ResourceGroupName -VirtualNetworkGatewayName $gateway.Name -ProcessorArchitecture Amd64
        
        # $packageUri may contain literal double-quotes at hello start and hello end of hello URL
        if($packageUri.Length -gt 0 -and $packageUri.Substring(0, 1) -eq '"' -and $packageUri.Substring($packageUri.Length - 1, 1) -eq '"')
        {
            $packageUri = $packageUri.Substring(1, $packageUri.Length - 2)
        }

        # Put hello VPN client configuration package onto hello App
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
            Write-Host "Currently connected tooVNET $currentVnet"

            Remove-AzureRmResource -ResourceName "$($webAppName)/$($currentVnet)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        }
            else
        {
            Write-Host "Not connected tooa VNET."
        }
    }

    Write-Host "Please Login"
    Login-AzureRmAccount

    # Choose subscription. If there's only one we will choose automatically

    $subs = Get-AzureRmSubscription
    $subscriptionId = ""

    if($subs.Length -eq 0)
    {
        Write-Error "No subscriptions bound toothis account."
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

    $resourceGroup = Read-Host "Please enter hello Resource Group of your App"

    $appName = Read-Host "Please enter hello Name of your App"

    $options = @("Add a NEW Virtual Network tooan App", "Add an EXISTING Virtual Network tooan App", "Remove a Virtual Network from an App");
    $optionValues = @(0, 1, 2)
    $option = PromptCustom "What do you want toodo?" $optionValues $options

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

<span data-ttu-id="2f375-198">Sla een kopie van het Hallo-script.</span><span class="sxs-lookup"><span data-stu-id="2f375-198">Save a copy of hello script.</span></span> <span data-ttu-id="2f375-199">In dit artikel V2VnetAllinOne.ps1 wordt aangeroepen, maar u kunt een andere naam.</span><span class="sxs-lookup"><span data-stu-id="2f375-199">In this article, it is called V2VnetAllinOne.ps1, but you can use another name.</span></span> <span data-ttu-id="2f375-200">Er zijn geen argumenten voor dit script.</span><span class="sxs-lookup"><span data-stu-id="2f375-200">There are no arguments for this script.</span></span> <span data-ttu-id="2f375-201">U gewoon uitvoeren het.</span><span class="sxs-lookup"><span data-stu-id="2f375-201">You simply run it.</span></span> <span data-ttu-id="2f375-202">Hallo eerst te beginnen Hallo script doet u toosign in gevraagd is.</span><span class="sxs-lookup"><span data-stu-id="2f375-202">hello first thing hello script will do is prompt you toosign in.</span></span> <span data-ttu-id="2f375-203">Nadat u zich aanmeldt, wordt Hallo script haalt gegevens over uw account en retourneert een lijst met abonnementen.</span><span class="sxs-lookup"><span data-stu-id="2f375-203">After you sign in, hello script gets details about your account and returns a list of subscriptions.</span></span> <span data-ttu-id="2f375-204">Hallo-aanvraag voor uw referenties niet meegerekend, uitziet Hallo initiële scriptuitvoering:</span><span class="sxs-lookup"><span data-stu-id="2f375-204">Not counting hello request for your credentials, hello initial script execution looks like this:</span></span>

    PS C:\Users\ccompy\Documents\VNET> .\V2VnetAllInOne.ps1
    Please Login

    Environment           : AzureCloud
    Account               : ccompy@microsoft.com
    TenantId              : 722278f-fef1-499f-91ab-2323d011db47
    SubscriptionId        : af5358e1-acac-2c90-a9eb-722190abf47a
    CurrentStorageAccount :

    Choose a subscription

    1) <span data-ttu-id="2f375-205">Demo-abonnement (af5358e1-acac-2c90-a9eb-722190abf47a)</span><span class="sxs-lookup"><span data-stu-id="2f375-205">Demo Subscription (af5358e1-acac-2c90-a9eb-722190abf47a)</span></span>
    2) <span data-ttu-id="2f375-206">MS-Test (a5350f55-dd5a-41ec-2ddb-ff7b911bb2ef)</span><span class="sxs-lookup"><span data-stu-id="2f375-206">MS Test (a5350f55-dd5a-41ec-2ddb-ff7b911bb2ef)</span></span>
    3) <span data-ttu-id="2f375-207">Paarse Demo-abonnement (2d4c99a4-57f9-4d5e-a0a1-0034c52db59d)</span><span class="sxs-lookup"><span data-stu-id="2f375-207">Purple Demo Subscription (2d4c99a4-57f9-4d5e-a0a1-0034c52db59d)</span></span>

    <span data-ttu-id="2f375-208">Kies een optie: 3</span><span class="sxs-lookup"><span data-stu-id="2f375-208">Choose an option: 3</span></span>

    <span data-ttu-id="2f375-209">Account: ccompy@microsoft.com omgeving: AzureCloud abonnement: 2d4c99a4-57f9-4d5e-a0a1-0034c52db59d Tenant: 722278f-fef1-499f-91ab-2323d011db47</span><span class="sxs-lookup"><span data-stu-id="2f375-209">Account      : ccompy@microsoft.com Environment  : AzureCloud Subscription : 2d4c99a4-57f9-4d5e-a0a1-0034c52db59d Tenant       : 722278f-fef1-499f-91ab-2323d011db47</span></span>

    <span data-ttu-id="2f375-210">Voer Hallo resourcegroep van uw App: hcdemo rg Voer Hallo naam van uw App: v2vnetpowershell wat wilt u wilt dat toodo?</span><span class="sxs-lookup"><span data-stu-id="2f375-210">Please enter hello Resource Group of your App: hcdemo-rg Please enter hello Name of your App: v2vnetpowershell What do you want toodo?</span></span>

    1) <span data-ttu-id="2f375-211">Een nieuw virtueel netwerk tooan App toevoegen</span><span class="sxs-lookup"><span data-stu-id="2f375-211">Add a NEW Virtual Network tooan App</span></span>
    2) <span data-ttu-id="2f375-212">Een bestaand virtueel netwerk tooan App toevoegen</span><span class="sxs-lookup"><span data-stu-id="2f375-212">Add an EXISTING Virtual Network tooan App</span></span>
    3) <span data-ttu-id="2f375-213">Een virtueel netwerk verwijderen uit een App</span><span class="sxs-lookup"><span data-stu-id="2f375-213">Remove a Virtual Network from an App</span></span>

<span data-ttu-id="2f375-214">Hallo rest van dit gedeelte wordt elk van deze drie opties.</span><span class="sxs-lookup"><span data-stu-id="2f375-214">hello rest of this section explains each of those three options.</span></span>

### <a name="create-a-resource-manager-vnet-and-integrate-with-it"></a><span data-ttu-id="2f375-215">Een Resource Manager VNet maken en integreren met het</span><span class="sxs-lookup"><span data-stu-id="2f375-215">Create a Resource Manager VNet and integrate with it</span></span>
<span data-ttu-id="2f375-216">selecteert u een nieuw virtueel netwerk dat gebruik Hallo Resource Manager-implementatiemodel en met uw app integreren toocreate **1) Voeg een nieuw virtueel netwerk tooan App**.</span><span class="sxs-lookup"><span data-stu-id="2f375-216">toocreate a new virtual network that uses hello Resource Manager deployment model and integrate it with your app, select **1) Add a NEW Virtual Network tooan App**.</span></span> <span data-ttu-id="2f375-217">Hiermee wordt u gevraagd voor naam van het virtuele netwerk Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="2f375-217">This will prompt you for hello name of hello virtual network.</span></span> <span data-ttu-id="2f375-218">In mijn geval, zoals u in Hallo ziet-instellingen, volgende ik Hallo naam gebruikt, v2pshell.</span><span class="sxs-lookup"><span data-stu-id="2f375-218">In my case, as you can see in hello following settings, I used hello name, v2pshell.</span></span>

<span data-ttu-id="2f375-219">Hallo-script geeft Hallo informatie over Hallo virtueel netwerk dat wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2f375-219">hello script gives hello details about hello virtual network that's being created.</span></span> <span data-ttu-id="2f375-220">Als ik wil, kan ik Hallo waarden wijzigen.</span><span class="sxs-lookup"><span data-stu-id="2f375-220">If I want, I can change any of hello values.</span></span> <span data-ttu-id="2f375-221">In dit voorbeeld wordt uitgevoerd, moet ik een virtueel netwerk met Hallo volgende instellingen gemaakt:</span><span class="sxs-lookup"><span data-stu-id="2f375-221">In this example execution, I created a virtual network that has hello following settings:</span></span>

    Virtual Network Name:         v2pshell
    Resource Group Name:          hcdemo-rg
    Gateway Name:                 v2pshell-gateway
    Vnet IP name:                 v2pshell-ip
    Vnet IP config name:          v2pshell-ipconf
    Address Space:                10.0.0.0/8
    Gateway Address Space:        10.5.0.0/16
    Point-To-Site Address Space:  172.16.0.0/12

    Do you wish toochange these settings?
    [Y] Yes  [N] No  [?] Help (default is "N"):

<span data-ttu-id="2f375-222">Als u toochange Hallo waarden wilt, typ **Y** en Hallo wijzigingen aanbrengen.</span><span class="sxs-lookup"><span data-stu-id="2f375-222">If you want toochange any of hello values, type **Y** and make hello changes.</span></span> <span data-ttu-id="2f375-223">Wanneer u tevreden over virtuele-netwerkinstellingen hello bent, typt u **N** of drukt u op Enter wanneer u wordt gevraagd over het Hallo-instellingen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="2f375-223">When you are happy with hello virtual network settings, type **N** or simply press Enter when prompted about changing hello settings.</span></span> <span data-ttu-id="2f375-224">Vanaf dat moment tot voltooiing, Hallo script vertelt u enkele van wat de it' i's doen totdat deze toocreate Hallo virtuele netwerkgateway wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="2f375-224">From there on until completion, hello script will tell you some of what it' i's doing until it starts toocreate hello virtual network gateway.</span></span> <span data-ttu-id="2f375-225">Deze stap kan tooan uur duren.</span><span class="sxs-lookup"><span data-stu-id="2f375-225">That step can take up tooan hour.</span></span> <span data-ttu-id="2f375-226">Er is geen voortgangsindicator tijdens deze fase, maar Hallo script kunt u weten wanneer Hallo gateway is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2f375-226">There is no progress indicator during this phase, but hello script will let you know when hello gateway has been created.</span></span>

<span data-ttu-id="2f375-227">Wanneer het Hallo-script is voltooid, wordt er **voltooid**.</span><span class="sxs-lookup"><span data-stu-id="2f375-227">When hello script finishes, it will say **Finished**.</span></span> <span data-ttu-id="2f375-228">Op dit moment hebt u een virtueel netwerk van Resource Manager met naam Hallo en instellingen die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="2f375-228">At this point, you will have a Resource Manager virtual network that has hello name and settings that you selected.</span></span> <span data-ttu-id="2f375-229">Deze nieuwe virtuele netwerk wordt ook worden geïntegreerd met uw app.</span><span class="sxs-lookup"><span data-stu-id="2f375-229">This new virtual network will also be integrated with your app.</span></span>

### <a name="integrate-your-app-with-a-preexisting-resource-manager-vnet"></a><span data-ttu-id="2f375-230">Uw app integreren met een bestaande Resource Manager VNet</span><span class="sxs-lookup"><span data-stu-id="2f375-230">Integrate your app with a preexisting Resource Manager VNet</span></span>
<span data-ttu-id="2f375-231">Wanneer u met een bestaand virtueel netwerk, integreren bent als u een Resource Manager virtueel netwerk dat geen gateway of punt-naar-site-connectiviteit bieden, wordt Hallo script ingesteld die.</span><span class="sxs-lookup"><span data-stu-id="2f375-231">When you're integrating with a preexisting virtual network, if you provide a Resource Manager virtual network that doesn’t have a gateway or point-to-site connectivity, hello script will set that up.</span></span> <span data-ttu-id="2f375-232">Als Hallo VNET al deze dingen instellen, gaat het Hallo-script rechte toohello app-integratie.</span><span class="sxs-lookup"><span data-stu-id="2f375-232">If hello VNET already has those things set up, hello script goes straight toohello app integration.</span></span> <span data-ttu-id="2f375-233">toostart dit proces gewoon Selecteer **2) Voeg een bestaand virtueel netwerk tooan App**.</span><span class="sxs-lookup"><span data-stu-id="2f375-233">toostart this process, simply select **2) Add an EXISTING Virtual Network tooan App**.</span></span>

<span data-ttu-id="2f375-234">Deze optie werkt alleen als u een bestaand virtueel netwerk voor Resource Manager, in Hallo hetzelfde abonnement als uw app.</span><span class="sxs-lookup"><span data-stu-id="2f375-234">This option works only if you have a preexisting Resource Manager virtual network that is in hello same subscription as your app.</span></span> <span data-ttu-id="2f375-235">Nadat u Hallo-optie selecteert, wordt er verschijnt een lijst met uw virtuele netwerken van Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2f375-235">After you select hello option, you will be presented with a list of your Resource Manager virtual networks.</span></span>   

    Select a VNET toointegrate with

    1) <span data-ttu-id="2f375-236">v2demonetwork</span><span class="sxs-lookup"><span data-stu-id="2f375-236">v2demonetwork</span></span>
    2) <span data-ttu-id="2f375-237">v2pshell</span><span class="sxs-lookup"><span data-stu-id="2f375-237">v2pshell</span></span>
    3) <span data-ttu-id="2f375-238">v2vnetintdemo</span><span class="sxs-lookup"><span data-stu-id="2f375-238">v2vnetintdemo</span></span>
    4) <span data-ttu-id="2f375-239">v2asenetwork</span><span class="sxs-lookup"><span data-stu-id="2f375-239">v2asenetwork</span></span>
    5) <span data-ttu-id="2f375-240">v2pshell2</span><span class="sxs-lookup"><span data-stu-id="2f375-240">v2pshell2</span></span>

    <span data-ttu-id="2f375-241">Kies een optie: 5</span><span class="sxs-lookup"><span data-stu-id="2f375-241">Choose an option: 5</span></span>

<span data-ttu-id="2f375-242">Hallo virtueel netwerk dat u wilt dat toointegrate met eenvoudig kunt selecteren.</span><span class="sxs-lookup"><span data-stu-id="2f375-242">Simply select hello virtual network that you want toointegrate with.</span></span> <span data-ttu-id="2f375-243">Als u al een gateway die voor punt-naar-site-connectiviteit is ingeschakeld, wordt Hallo script gewoon uw app integreren met het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="2f375-243">If you already have a gateway that has point-to-site connectivity enabled, hello script will simply integrate your app with your virtual network.</span></span> <span data-ttu-id="2f375-244">Als u een gateway niet hebt, moet u toospecify hello gatewaysubnet.</span><span class="sxs-lookup"><span data-stu-id="2f375-244">If you do not have a gateway, you will need toospecify hello gateway subnet.</span></span> <span data-ttu-id="2f375-245">Het gatewaysubnet moet in de adresruimte van uw virtuele netwerk en deze kan niet in een ander subnet.</span><span class="sxs-lookup"><span data-stu-id="2f375-245">Your gateway subnet must be in your virtual network address space, and it cannot be in any other subnet.</span></span> <span data-ttu-id="2f375-246">Als u een virtueel netwerk zonder een gateway hebt en deze stap uitvoert, dingen moeten uitzien:</span><span class="sxs-lookup"><span data-stu-id="2f375-246">If you have a virtual network without a gateway and run this step, things look like this:</span></span>

    This Virtual Network has no gateway. I will need toocreate one.
    Your VNET is in hello address space 172.16.0.0/16, with hello following Subnets:
    default: 172.16.0.0/24
    Please choose a GatewaySubnet address space: 172.16.1.0/26

<span data-ttu-id="2f375-247">In dit voorbeeld gemaakt ik een virtuele netwerkgateway met Hallo volgende instellingen:</span><span class="sxs-lookup"><span data-stu-id="2f375-247">In this example, I created a virtual network gateway that has hello following settings:</span></span>

    Virtual Network Name:         v2pshell2
    Resource Group Name:          vnetdemo-rg
    Gateway Name:                 v2pshell2-gateway
    Vnet IP name:                 v2pshell2-ip
    Vnet IP config name:          v2pshell2-ipconf
    Address Space:                172.16.0.0/16
    Gateway Address Space:        172.16.1.0/26
    Point-To-Site Address Space:  172.16.0.0/12

    Do you wish toochange these settings?
    [Y] Yes  [N] No  [?] Help (default is "N"):
    Creating App association tooVNET

<span data-ttu-id="2f375-248">Als u toochange deze instellingen wilt, kunt u dit doet.</span><span class="sxs-lookup"><span data-stu-id="2f375-248">If you want toochange any of those settings, you can do so.</span></span> <span data-ttu-id="2f375-249">Anders, druk op Enter en Hallo script wordt gemaakt van uw gateway en uw app tooyour virtueel netwerk koppelen.</span><span class="sxs-lookup"><span data-stu-id="2f375-249">Otherwise, press Enter and hello script will create your gateway and attach your app tooyour virtual network.</span></span> <span data-ttu-id="2f375-250">Aanmaaktijd Hallo-gateway is echter nog steeds een uur, dus zorg ervoor dat u die rekening houden.</span><span class="sxs-lookup"><span data-stu-id="2f375-250">hello gateway creation time is still an hour, though, so make sure you keep that in mind.</span></span> <span data-ttu-id="2f375-251">Als alles is voltooid, Hallo script dicteert **voltooid**.</span><span class="sxs-lookup"><span data-stu-id="2f375-251">When everything is finished, hello script will say **Finished**.</span></span>

### <a name="disconnect-your-app-from-a-resource-manager-vnet"></a><span data-ttu-id="2f375-252">Verbreek de verbinding tussen uw app een Resource Manager VNet</span><span class="sxs-lookup"><span data-stu-id="2f375-252">Disconnect your app from a Resource Manager VNet</span></span>
<span data-ttu-id="2f375-253">Het virtuele netwerk van uw app verbreken niet noteren Hallo gateway of punt-naar-site-connectiviteit uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="2f375-253">Disconnecting your app from your virtual network does not take down hello gateway or disable point-to-site connectivity.</span></span> <span data-ttu-id="2f375-254">U, nadat alle gebruikt deze voor iets anders.</span><span class="sxs-lookup"><span data-stu-id="2f375-254">You might, after all, be using it for something else.</span></span> <span data-ttu-id="2f375-255">Deze wordt ook niet verbroken deze van alle andere apps dan Hallo een die u hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="2f375-255">It also does not disconnect it from any other apps other than hello one you provided.</span></span> <span data-ttu-id="2f375-256">tooperform deze actie, selecteer **3) een virtueel netwerk verwijderen uit een App**.</span><span class="sxs-lookup"><span data-stu-id="2f375-256">tooperform this action, select **3) Remove a Virtual Network from an App**.</span></span> <span data-ttu-id="2f375-257">Als u doet dit, ziet u ongeveer het volgende:</span><span class="sxs-lookup"><span data-stu-id="2f375-257">When you do so, you will see something like this:</span></span>

    Currently connected tooVNET v2pshell

    Confirm
    Are you sure you want toodelete hello following resource:
    /subscriptions/edcc99a4-b7f9-4b5e-a9a1-3034c51db496/resourceGroups/hcdemo-rg/providers/Microsoft.Web/sites/v2vnetpowers
    hell/virtualNetworkConnections/v2pshell
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):

<span data-ttu-id="2f375-258">Hoewel Hallo script verwijderen staat, verwijdert Hallo virtueel netwerk niet meer.</span><span class="sxs-lookup"><span data-stu-id="2f375-258">Although hello script says delete, it does not delete hello virtual network.</span></span> <span data-ttu-id="2f375-259">Het worden Hallo-integratie alleen verwijderd.</span><span class="sxs-lookup"><span data-stu-id="2f375-259">It’s just removing hello integration.</span></span> <span data-ttu-id="2f375-260">Nadat u bevestigen dat dit is wat u wilt toodo, Hallo opdracht erg snel wordt verwerkt en vertelt u **True** wanneer het is voltooid.</span><span class="sxs-lookup"><span data-stu-id="2f375-260">After you confirm that this is what you want toodo, hello command is processed quite quickly and tells you **True** when it is done.</span></span>

<!--Links-->
[createvpngateway]: http://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/
[azureportal]: http://portal.azure.com
