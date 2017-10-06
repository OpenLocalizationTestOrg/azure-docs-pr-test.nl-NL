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
# <a name="connect-your-app-tooyour-virtual-network-by-using-powershell"></a>Verbinding maken met uw app tooyour virtueel netwerk met behulp van PowerShell
## <a name="overview"></a>Overzicht
In Azure App Service kunt u uw app (web, mobiel of API) tooan virtuele Azure-netwerk (VNet) in uw abonnement. Deze functie is aangeroepen VNet-integratie. Verwar Hallo VNet-integratiefunctie niet met de functie App Service-omgeving hello, zodat u toorun een exemplaar van Azure App Service in uw virtuele netwerk.

Hallo VNet-integratiefunctie heeft een gebruikersinterface (UI) in de nieuwe portal Hallo dat u toointegrate met virtuele netwerken die zijn geïmplementeerd gebruiken kunt met behulp van het klassieke implementatiemodel Hallo of hello Azure Resource Manager-implementatiemodel. Als u meer informatie over de functie Hallo toolearn wilt, Zie [uw app integreren met een Azure-netwerk](web-sites-integrate-with-vnet.md).

In dit artikel wordt niet over hoe toouse UI hello, maar in plaats daarvan over het tooenable integratie met behulp van PowerShell. Omdat het Hallo-opdrachten voor elk implementatiemodel verschillend zijn, heeft dit artikel een sectie voor elke implementatiemodel.  

Controleer voordat u met dit artikel doorgaat, dat u hebt:

* Hallo die nieuwste Azure PowerShell-SDK geïnstalleerd. U kunt dit installeren met de Hallo Web Platform Installer.
* Een app in Azure App Service wordt uitgevoerd op een Standard of Premium-SKU.

## <a name="classic-virtual-networks"></a>Klassieke virtuele netwerken
Deze sectie wordt uitgelegd drie taken voor virtuele netwerken die gebruikmaken van het klassieke implementatiemodel Hallo:

1. Uw app tooa bestaande virtueel netwerk verbinden dat een gateway heeft en is geconfigureerd voor punt-naar-site-connectiviteit.
2. Werk uw gegevens van de integratie van virtueel netwerk voor uw app.
3. Verbreek de verbinding tussen uw app in het virtuele netwerk.

### <a name="connect-an-app-tooa-classic-vnet"></a>Verbinding maken met een app tooa klassieke VNet
tooconnect een app tooa virtueel netwerk, volg deze drie stappen:

1. Declareren toohello web-app of moet deze aan een bepaald virtueel netwerk koppelen. Hallo-app een certificaat dat wordt verleend toohello virtueel netwerk voor punt-naar-site-connectiviteit gegenereerd.
2. Hallo web app certificaat toohello virtueel netwerk uploaden en vervolgens Hallo punt-naar-site VPN-pakket-URI die worden opgehaald.
3. Hallo van web-app virtueel netwerkverbinding bijwerken met Hallo punt-naar-site de pakket-URI.

Hello eerste en derde stappen zijn volledige scriptondersteuning mogelijk, maar de tweede stap Hallo vereist een eenmalige, handmatige actie via Hallo portal of toegang tooperform **plaatsen** of **PATCH** acties op Hallo virtueel netwerk Azure Resource Manager-eindpunt. Neem contact op met ondersteuning van Azure toohave dit ingeschakeld. Voordat u begint, zorg ervoor dat er een klassiek virtueel netwerk met punt-naar-site-connectiviteit is ingeschakeld en een geïmplementeerde gateway. toocreate hello gateway en schakel punt-naar-site-connectiviteit, moet u toouse Hallo portal zoals beschreven op [maken van een VPN-gateway][createvpngateway].

Hallo klassiek virtueel netwerk moet toobe in Hallo hetzelfde abonnement als uw App-Service die blokkeringen Hallo-app die u integreert met plant.

##### <a name="set-up-azure-powershell-sdk"></a>Instellen van Azure PowerShell SDK
Open een PowerShell-venster en instellen van uw Azure-account en abonnement met behulp van:

    Login-AzureRmAccount

Deze opdracht wordt een prompt tooget geopend uw Azure-referenties. Nadat u zich aanmeldt, kunt een van de volgende opdrachten tooselect Hallo abonnement dat u wilt dat toouse hello te gebruiken. Zorg ervoor dat u van Hallo abonnement die uw virtuele netwerk en de App Service-abonnement gebruikmaakt in.

    Select-AzureRmSubscription –SubscriptionName [WebAppSubscriptionName]

of

    Select-AzureRmSubscription –SubscriptionId [WebAppSubscriptionId]

##### <a name="variables-used-in-this-article"></a>Variabelen die in dit artikel worden gebruikt
toosimplify opdrachten, zullen een **$Configuration** PowerShell variabele met de Hallo specifieke configuratie.

Een variabele als volgt instellen in PowerShell Hello volgende parameters:

    $Configuration = @{}
    $Configuration.WebAppResourceGroup = "[Your web app resource group]"
    $Configuration.WebAppName = "[Your web app name]"
    $Configuration.VnetSubscriptionId = "[Your vnet subscription id]"
    $Configuration.VnetResourceGroup = "[Your vnet resource group]"
    $Configuration.VnetName = "[Your vnet name]"

Hallo app locatie moet Hallo locatie zonder spaties. Bijvoorbeeld, is VS-West westus.

    $Configuration.WebAppLocation = "[Your web app Location]"

het volgende item Hallo is waar Hallo certificaat moet worden geschreven. Deze moet een pad op de lokale computer. Zorg ervoor dat tooinclude .cer Hallo achter.

    $Configuration.GeneratedCertificatePath = "[C:\Path\To\Certificate.cer]"

toosee ingesteld, type **$Configuration**.

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

Hallo rest van deze sectie wordt ervan uitgegaan dat u een variabele die is gemaakt als NET beschreven hebt.

##### <a name="declare-hello-virtual-network-toohello-app"></a>Hallo virtueel netwerk toohello app declareren
Gebruik hello volgt opdracht tootell Hallo app dat deze dit bepaalde virtuele netwerk wordt gebruikt. Hierdoor wordt Hallo app toogenerate benodigde certificaten:

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -PropertyObject @{"VnetResourceId" = "/subscriptions/$($Configuration.VnetSubscriptionId)/resourceGroups/$($Configuration.VnetResourceGroup)/providers/Microsoft.ClassicNetwork/virtualNetworks/$($Configuration.VnetName)"} -Location $Configuration.WebAppLocation -ApiVersion 2015-07-01

Als u deze opdracht is geslaagd, **$vnet** moet een **eigenschappen** in deze variabele. Hallo **eigenschappen** variabele moet zowel een certificaat vingerafdruk en Hallo certificaatgegevens bevatten.

##### <a name="upload-hello-web-app-certificate-toohello-virtual-network"></a>Hallo web app certificaat toohello virtueel netwerk uploaden
Een handmatige stap eenmalige is vereist voor elk abonnement en de combinatie van het virtuele netwerk. Dat wil zeggen, als u apps in abonnement een tooVirtual netwerk een verbinding maakt, moet u toodo deze stap slechts eenmaal ongeacht hoeveel apps die u configureert. Als u een nieuw virtueel netwerk van de app-tooanother toevoegt, moet u dit opnieuw toodo. Hallo reden hiervoor is dat een set van certificaten wordt gegenereerd tijdens een abonnement in Azure App Service en Hallo set eenmaal voor elk virtueel netwerk dat Hallo apps maakt verbinding met wordt gegenereerd.

Hallo certificaten wordt al zijn ingesteld als u deze stappen hebt gevolgd, of als u een geïntegreerd met Hallo hetzelfde virtuele netwerk met behulp van Hallo-portal.

de eerste stap Hallo is toogenerate Hallo cer-bestand. de tweede stap Hallo is tooupload Hallo .cer-bestand tooyour virtueel netwerk. toogenerate hello cer-bestand van Hallo API-aanroep in Hallo eerdere stap Hallo volgende opdrachten uitvoeren.

    $certBytes = [System.Convert]::FromBase64String($vnet.Properties.certBlob)
    [System.IO.File]::WriteAllBytes("$($Configuration.GeneratedCertificatePath)", $certBytes)

Hallo-certificaat worden gevonden op locatie Hallo die **$Configuration.GeneratedCertificatePath** bevat.

tooupload hello certificaat handmatig hello gebruiken [Azure-portal] [ azureportal] en **bladeren virtueel netwerk (klassiek)** > **VPN-verbindingen**  >  **Punt-naar-site** > **certificaten beheren**. Hier kunt uw certificaat te uploaden.

##### <a name="get-hello-point-to-site-package"></a>Hallo punt-naar-site-pakket
Hallo volgende stap bij het instellen van een virtueel netwerkverbinding op een web-app is tooget Hallo punt-naar-site-pakket en geef deze tooyour web-app.

Sla Hallo volgende sjabloonbestand tooa aangeroepen GetNetworkPackageUri.json ergens op uw computer, bijvoorbeeld C:\Azure\Templates\GetNetworkPackageUri.json.

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


Invoerparameters instellen:

    $parameters = @{"certData" = $vnet.Properties.certBlob ;
    certThumbprint = $vnet.Properties.certThumbprint ;
    "networkName" = $Configuration.VnetName }

Roep Hallo script:

    $output = New-AzureRmResourceGroupDeployment -Name unused -ResourceGroupName $Configuration.VnetResourceGroup -TemplateParameterObject $parameters -TemplateFile C:\PATH\TO\GetNetworkPackageUri.json


Hallo variabele **$output. Outputs.packageUri** bevat nu Hallo pakket URI toobe gegeven tooyour web-app.

##### <a name="upload-hello-point-to-site-package-tooyour-app"></a>Hallo punt-naar-site pakket tooyour app uploaden
de laatste stap Hallo is tooprovide Hallo app met dit pakket. De volgende opdracht Hallo voert u eenvoudigweg:

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)/primary" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-07-01 -PropertyObject @{"VnetName" = $Configuration.VnetName ; "VpnPackageUri" = $($output.Outputs.packageUri).Value } -Location $Configuration.WebAppLocation

Als een bericht gevraagd tooconfirm dat u een bestaande resource wilt overschrijven, moet u ervoor dat tooallow deze.

Nadat deze opdracht is geslaagd, moet uw app nu verbonden toohello virtueel netwerk zijn. tooconfirm geslaagd, gaat u tooyour app-console en typt u de volgende Hallo:

    SET WEBSITE_

Als er een omgevingsvariabele WEBSITE_VNETNAME die heeft een waarde die overeenkomt met de naam Hallo Hallo doel virtueel netwerk genoemd, worden alle configuraties zijn geslaagd.

### <a name="update-classic-vnet-integration-information"></a>Klassieke VNet integratie-informatie bijwerken
tooupdate of uw gegevens synchroniseren, herhaalt Hallo stappen die u tijdens het maken van Hallo-integratie in de eerste plaats Hallo gevolgd. Deze stappen zijn:

1. Definieer uw configuratie-informatie.
2. Hallo virtueel netwerk toohello app declareren.
3. Hallo punt-naar-site package ophalen.
4. Hallo punt-naar-site pakket tooyour app uploaden.

### <a name="disconnect-your-app-from-a-classic-vnet"></a>Verbreek de verbinding tussen uw app een klassiek VNet
toodisconnect hello app, moet u Hallo configuratie-informatie die is ingesteld tijdens de integratie van virtueel netwerk. Deze gegevens niet gebruiken, zich vervolgens één opdracht toodisconnect uw app uit het virtuele netwerk.

    $vnet = Remove-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-07-01

## <a name="resource-manager-virtual-networks"></a>Virtuele netwerken van Resource Manager
Virtuele netwerken van Resource Manager hebben Azure Resource Manager-API's die bepaalde processen in vergelijking met het klassieke virtuele netwerken vereenvoudigen. Wij hebben een script dat u kunt Hallo volgende taken voltooien:

* Een virtueel netwerk van Resource Manager maken en uw app integreren.
* Maken van een gateway, punt-naar-site-connectiviteit in een bestaande Resource Manager virtueel netwerk configureren en vervolgens uw app integreren met het.
* Uw app integreren met een bestaand virtueel netwerk voor Resource Manager, dat een gateway en een punt-naar-site-connectiviteit ingeschakeld.
* Verbreek de verbinding tussen uw app in het virtuele netwerk.

### <a name="resource-manager-vnet-app-service-integration-script"></a>Script voor Resource Manager VNet-App Service-integratie
Hallo volgende script en sla het bestand tooa kopiëren. Als u niet dat toouse Hallo script wilt, kunt u gratis toolearn hieruit toosee hoe tooset mogelijkheden van met een virtueel netwerk van Resource Manager.

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

Sla een kopie van het Hallo-script. In dit artikel V2VnetAllinOne.ps1 wordt aangeroepen, maar u kunt een andere naam. Er zijn geen argumenten voor dit script. U gewoon uitvoeren het. Hallo eerst te beginnen Hallo script doet u toosign in gevraagd is. Nadat u zich aanmeldt, wordt Hallo script haalt gegevens over uw account en retourneert een lijst met abonnementen. Hallo-aanvraag voor uw referenties niet meegerekend, uitziet Hallo initiële scriptuitvoering:

    PS C:\Users\ccompy\Documents\VNET> .\V2VnetAllInOne.ps1
    Please Login

    Environment           : AzureCloud
    Account               : ccompy@microsoft.com
    TenantId              : 722278f-fef1-499f-91ab-2323d011db47
    SubscriptionId        : af5358e1-acac-2c90-a9eb-722190abf47a
    CurrentStorageAccount :

    Choose a subscription

    1) Demo-abonnement (af5358e1-acac-2c90-a9eb-722190abf47a)
    2) MS-Test (a5350f55-dd5a-41ec-2ddb-ff7b911bb2ef)
    3) Paarse Demo-abonnement (2d4c99a4-57f9-4d5e-a0a1-0034c52db59d)

    Kies een optie: 3

    Account: ccompy@microsoft.com omgeving: AzureCloud abonnement: 2d4c99a4-57f9-4d5e-a0a1-0034c52db59d Tenant: 722278f-fef1-499f-91ab-2323d011db47

    Voer Hallo resourcegroep van uw App: hcdemo rg Voer Hallo naam van uw App: v2vnetpowershell wat wilt u wilt dat toodo?

    1) Een nieuw virtueel netwerk tooan App toevoegen
    2) Een bestaand virtueel netwerk tooan App toevoegen
    3) Een virtueel netwerk verwijderen uit een App

Hallo rest van dit gedeelte wordt elk van deze drie opties.

### <a name="create-a-resource-manager-vnet-and-integrate-with-it"></a>Een Resource Manager VNet maken en integreren met het
selecteert u een nieuw virtueel netwerk dat gebruik Hallo Resource Manager-implementatiemodel en met uw app integreren toocreate **1) Voeg een nieuw virtueel netwerk tooan App**. Hiermee wordt u gevraagd voor naam van het virtuele netwerk Hallo Hallo. In mijn geval, zoals u in Hallo ziet-instellingen, volgende ik Hallo naam gebruikt, v2pshell.

Hallo-script geeft Hallo informatie over Hallo virtueel netwerk dat wordt gemaakt. Als ik wil, kan ik Hallo waarden wijzigen. In dit voorbeeld wordt uitgevoerd, moet ik een virtueel netwerk met Hallo volgende instellingen gemaakt:

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

Als u toochange Hallo waarden wilt, typ **Y** en Hallo wijzigingen aanbrengen. Wanneer u tevreden over virtuele-netwerkinstellingen hello bent, typt u **N** of drukt u op Enter wanneer u wordt gevraagd over het Hallo-instellingen wijzigen. Vanaf dat moment tot voltooiing, Hallo script vertelt u enkele van wat de it' i's doen totdat deze toocreate Hallo virtuele netwerkgateway wordt gestart. Deze stap kan tooan uur duren. Er is geen voortgangsindicator tijdens deze fase, maar Hallo script kunt u weten wanneer Hallo gateway is gemaakt.

Wanneer het Hallo-script is voltooid, wordt er **voltooid**. Op dit moment hebt u een virtueel netwerk van Resource Manager met naam Hallo en instellingen die u hebt geselecteerd. Deze nieuwe virtuele netwerk wordt ook worden geïntegreerd met uw app.

### <a name="integrate-your-app-with-a-preexisting-resource-manager-vnet"></a>Uw app integreren met een bestaande Resource Manager VNet
Wanneer u met een bestaand virtueel netwerk, integreren bent als u een Resource Manager virtueel netwerk dat geen gateway of punt-naar-site-connectiviteit bieden, wordt Hallo script ingesteld die. Als Hallo VNET al deze dingen instellen, gaat het Hallo-script rechte toohello app-integratie. toostart dit proces gewoon Selecteer **2) Voeg een bestaand virtueel netwerk tooan App**.

Deze optie werkt alleen als u een bestaand virtueel netwerk voor Resource Manager, in Hallo hetzelfde abonnement als uw app. Nadat u Hallo-optie selecteert, wordt er verschijnt een lijst met uw virtuele netwerken van Resource Manager.   

    Select a VNET toointegrate with

    1) v2demonetwork
    2) v2pshell
    3) v2vnetintdemo
    4) v2asenetwork
    5) v2pshell2

    Kies een optie: 5

Hallo virtueel netwerk dat u wilt dat toointegrate met eenvoudig kunt selecteren. Als u al een gateway die voor punt-naar-site-connectiviteit is ingeschakeld, wordt Hallo script gewoon uw app integreren met het virtuele netwerk. Als u een gateway niet hebt, moet u toospecify hello gatewaysubnet. Het gatewaysubnet moet in de adresruimte van uw virtuele netwerk en deze kan niet in een ander subnet. Als u een virtueel netwerk zonder een gateway hebt en deze stap uitvoert, dingen moeten uitzien:

    This Virtual Network has no gateway. I will need toocreate one.
    Your VNET is in hello address space 172.16.0.0/16, with hello following Subnets:
    default: 172.16.0.0/24
    Please choose a GatewaySubnet address space: 172.16.1.0/26

In dit voorbeeld gemaakt ik een virtuele netwerkgateway met Hallo volgende instellingen:

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

Als u toochange deze instellingen wilt, kunt u dit doet. Anders, druk op Enter en Hallo script wordt gemaakt van uw gateway en uw app tooyour virtueel netwerk koppelen. Aanmaaktijd Hallo-gateway is echter nog steeds een uur, dus zorg ervoor dat u die rekening houden. Als alles is voltooid, Hallo script dicteert **voltooid**.

### <a name="disconnect-your-app-from-a-resource-manager-vnet"></a>Verbreek de verbinding tussen uw app een Resource Manager VNet
Het virtuele netwerk van uw app verbreken niet noteren Hallo gateway of punt-naar-site-connectiviteit uitschakelen. U, nadat alle gebruikt deze voor iets anders. Deze wordt ook niet verbroken deze van alle andere apps dan Hallo een die u hebt opgegeven. tooperform deze actie, selecteer **3) een virtueel netwerk verwijderen uit een App**. Als u doet dit, ziet u ongeveer het volgende:

    Currently connected tooVNET v2pshell

    Confirm
    Are you sure you want toodelete hello following resource:
    /subscriptions/edcc99a4-b7f9-4b5e-a9a1-3034c51db496/resourceGroups/hcdemo-rg/providers/Microsoft.Web/sites/v2vnetpowers
    hell/virtualNetworkConnections/v2pshell
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):

Hoewel Hallo script verwijderen staat, verwijdert Hallo virtueel netwerk niet meer. Het worden Hallo-integratie alleen verwijderd. Nadat u bevestigen dat dit is wat u wilt toodo, Hallo opdracht erg snel wordt verwerkt en vertelt u **True** wanneer het is voltooid.

<!--Links-->
[createvpngateway]: http://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/
[azureportal]: http://portal.azure.com
