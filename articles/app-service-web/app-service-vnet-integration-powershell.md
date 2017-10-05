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
# <a name="connect-your-app-to-your-virtual-network-by-using-powershell"></a>Verbinding met uw app in het virtuele netwerk maken via PowerShell
## <a name="overview"></a>Overzicht
In Azure App Service kunt u uw app (web, mobiel of API) met een Azure virtual network (VNet) in uw abonnement. Deze functie is aangeroepen VNet-integratie. Verwar de VNet-integratiefunctie niet met de functie App Service-omgeving, zodat u kunt een exemplaar van Azure App Service uitvoeren in uw virtuele netwerk.

De VNet-integratiefunctie heeft een gebruikersinterface (UI) in de nieuwe portal die u gebruiken kunt om te integreren met virtuele netwerken die zijn geïmplementeerd met behulp van het klassieke implementatiemodel of het Azure Resource Manager-implementatiemodel. Als u wilt voor meer informatie over de functie, Zie [uw app integreren met een Azure-netwerk](web-sites-integrate-with-vnet.md).

Dit artikel is niet over het gebruik van de gebruikersinterface, maar in plaats daarvan over het inschakelen van integratie met behulp van PowerShell. Omdat de opdrachten voor elk implementatiemodel verschillend zijn, heeft dit artikel een sectie voor elke implementatiemodel.  

Controleer voordat u met dit artikel doorgaat, dat u hebt:

* De nieuwste Azure PowerShell SDK geïnstalleerd. U kunt dit installeren met het Webplatforminstallatieprogramma.
* Een app in Azure App Service wordt uitgevoerd op een Standard of Premium-SKU.

## <a name="classic-virtual-networks"></a>Klassieke virtuele netwerken
Deze sectie wordt uitgelegd drie taken voor virtuele netwerken die gebruikmaken van het klassieke implementatiemodel:

1. Uw app verbinden met een bestaand virtueel netwerk dat een gateway heeft en is geconfigureerd voor punt-naar-site-connectiviteit.
2. Werk uw gegevens van de integratie van virtueel netwerk voor uw app.
3. Verbreek de verbinding tussen uw app in het virtuele netwerk.

### <a name="connect-an-app-to-a-classic-vnet"></a>Een app verbinden met een klassiek VNet
Als u wilt een app koppelen aan een virtueel netwerk, volg deze drie stappen:

1. Declareren in de web-app of moet deze aan een bepaald virtueel netwerk koppelen. De app een certificaat dat wordt verleend aan het virtuele netwerk voor punt-naar-site-connectiviteit gegenereerd.
2. Het certificaat voor web-app uploaden naar het virtuele netwerk en vervolgens de punt-naar-site VPN-pakket URI worden opgehaald.
3. De web-app virtueel netwerkverbinding met de pakket-URI van de punt-naar-site bijwerken.

De eerste en derde stappen volledige scriptondersteuning mogelijk zijn, maar de tweede stap vereist een eenmalige, handmatige actie via de portal of de toegang tot het uitvoeren van **plaatsen** of **PATCH** acties op het virtuele netwerk Azure Resource Manager-eindpunt. Neem contact op met een Azure-ondersteuning als dit is ingeschakeld. Voordat u begint, zorg ervoor dat er een klassiek virtueel netwerk met punt-naar-site-connectiviteit is ingeschakeld en een geïmplementeerde gateway. Als u wilt maken van de gateway en punt-naar-site-connectiviteit inschakelt, moet u de portal te gebruiken, zoals beschreven op [maken van een VPN-gateway][createvpngateway].

Het klassieke virtuele netwerk moet zich in hetzelfde abonnement als uw App Service-abonnement met de app die u integreert.

##### <a name="set-up-azure-powershell-sdk"></a>Instellen van Azure PowerShell SDK
Open een PowerShell-venster en instellen van uw Azure-account en abonnement met behulp van:

    Login-AzureRmAccount

Deze opdracht wordt een prompt voor uw Azure-referenties geopend. Nadat u zich aanmeldt, gebruik een van de volgende opdrachten om het abonnement dat u wilt gebruiken. Zorg ervoor dat u van het abonnement die uw virtuele netwerk en de App Service-abonnement gebruikmaakt in.

    Select-AzureRmSubscription –SubscriptionName [WebAppSubscriptionName]

of

    Select-AzureRmSubscription –SubscriptionId [WebAppSubscriptionId]

##### <a name="variables-used-in-this-article"></a>Variabelen die in dit artikel worden gebruikt
Om te vereenvoudigen opdrachten, stelt we een **$Configuration** PowerShell variabele met de specifieke configuratie.

Een variabele als volgt instellen in PowerShell met de volgende parameters:

    $Configuration = @{}
    $Configuration.WebAppResourceGroup = "[Your web app resource group]"
    $Configuration.WebAppName = "[Your web app name]"
    $Configuration.VnetSubscriptionId = "[Your vnet subscription id]"
    $Configuration.VnetResourceGroup = "[Your vnet resource group]"
    $Configuration.VnetName = "[Your vnet name]"

De locatie van de app moet de locatie zonder spaties. Bijvoorbeeld, is VS-West westus.

    $Configuration.WebAppLocation = "[Your web app Location]"

Het volgende item is waar het certificaat moet worden geschreven. Deze moet een pad op de lokale computer. Zorg ervoor dat .cer aan het einde.

    $Configuration.GeneratedCertificatePath = "[C:\Path\To\Certificate.cer]"

Typ om te zien wat u hebt ingesteld, **$Configuration**.

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

De rest van deze sectie wordt ervan uitgegaan dat u een variabele die is gemaakt als NET beschreven hebt.

##### <a name="declare-the-virtual-network-to-the-app"></a>Het virtuele netwerk naar de app declareren
Gebruik de volgende opdracht om te controleren van de app dat deze dit bepaalde virtuele netwerk wordt gebruikt. Dit zorgt ervoor dat de app voor het genereren van de benodigde certificaten:

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -PropertyObject @{"VnetResourceId" = "/subscriptions/$($Configuration.VnetSubscriptionId)/resourceGroups/$($Configuration.VnetResourceGroup)/providers/Microsoft.ClassicNetwork/virtualNetworks/$($Configuration.VnetName)"} -Location $Configuration.WebAppLocation -ApiVersion 2015-07-01

Als u deze opdracht is geslaagd, **$vnet** moet een **eigenschappen** in deze variabele. De **eigenschappen** variabele moet zowel een vingerafdruk van het certificaat en de gegevens van het certificaat bevatten.

##### <a name="upload-the-web-app-certificate-to-the-virtual-network"></a>Het certificaat voor web-app uploaden naar het virtuele netwerk
Een handmatige stap eenmalige is vereist voor elk abonnement en de combinatie van het virtuele netwerk. Dat wil zeggen, als u apps in abonnement een verbinding met een virtueel netwerk, moet u doen in deze stap slechts eenmaal ongeacht hoeveel apps die u configureert. Als u een nieuwe app aan een ander virtueel netwerk toevoegt, moet u dit opnieuw te doen. De reden hiervoor is dat een set van certificaten wordt gegenereerd tijdens een abonnement in Azure App Service en de set eenmaal voor elk virtueel netwerk dat de apps die verbinding met maakt wordt gegenereerd.

De certificaten wordt al zijn ingesteld als u deze stappen hebt uitgevoerd of als u geïntegreerd met hetzelfde virtuele netwerk met behulp van de portal.

De eerste stap is het cer-bestand genereren. De tweede stap is het cer-bestand uploaden naar uw virtuele netwerk. Voor het genereren van het cer-bestand van de API-aanroep in de vorige stap, voer de volgende opdrachten.

    $certBytes = [System.Convert]::FromBase64String($vnet.Properties.certBlob)
    [System.IO.File]::WriteAllBytes("$($Configuration.GeneratedCertificatePath)", $certBytes)

Het certificaat wordt gevonden op de locatie die **$Configuration.GeneratedCertificatePath** bevat.

Het certificaat handmatig uploaden, gebruiken de [Azure-portal] [ azureportal] en **bladeren virtueel netwerk (klassiek)** > **VPN-verbindingen** > **punt-naar-site** > **certificaten beheren**. Hier kunt uw certificaat te uploaden.

##### <a name="get-the-point-to-site-package"></a>Het pakket voor punt-naar-site
De volgende stap bij het instellen van een virtueel netwerkverbinding op een web-app is het ophalen van het pakket voor punt-naar-site en het weer doorgeeft aan uw web-app.

De volgende sjabloon opslaan in een bestand met de naam van de GetNetworkPackageUri.json ergens op uw computer, bijvoorbeeld C:\Azure\Templates\GetNetworkPackageUri.json.

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

Roept het script:

    $output = New-AzureRmResourceGroupDeployment -Name unused -ResourceGroupName $Configuration.VnetResourceGroup -TemplateParameterObject $parameters -TemplateFile C:\PATH\TO\GetNetworkPackageUri.json


De variabele **$output. Outputs.packageUri** bevat nu de pakket-URI die moet worden besteed aan uw web-app.

##### <a name="upload-the-point-to-site-package-to-your-app"></a>Uploaden van het pakket punt-naar-site naar uw app
De laatste stap is om te voorzien van de app dit pakket. Alleen uitvoeren de volgende opdracht:

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)/primary" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-07-01 -PropertyObject @{"VnetName" = $Configuration.VnetName ; "VpnPackageUri" = $($output.Outputs.packageUri).Value } -Location $Configuration.WebAppLocation

Als een bericht u gevraagd te bevestigen wordt dat u een bestaande resource wilt overschrijven, moet u mogelijk te maken.

Nadat deze opdracht is geslaagd, moet u uw app nu verbonden aan het virtuele netwerk. Om te bevestigen geslaagd, gaat u naar uw app-console en typ het volgende:

    SET WEBSITE_

Als er een omgevingsvariabele WEBSITE_VNETNAME die heeft een waarde die overeenkomt met de naam van het virtuele doelnetwerk genoemd, worden alle configuraties zijn geslaagd.

### <a name="update-classic-vnet-integration-information"></a>Klassieke VNet integratie-informatie bijwerken
Als u wilt bijwerken of uw gegevens synchroniseren, herhaalt u de stappen die u hebt gevolgd wanneer u de integratie in eerste instantie gemaakt. Deze stappen zijn:

1. Definieer uw configuratie-informatie.
2. Het virtuele netwerk naar de app declareren.
3. Ophalen van de punt-naar-site-pakket.
4. Upload het pakket punt-naar-site naar uw app.

### <a name="disconnect-your-app-from-a-classic-vnet"></a>Verbreek de verbinding tussen uw app een klassiek VNet
Als u wilt verbreken van de app, moet u de configuratiegegevens die is ingesteld tijdens de integratie van virtueel netwerk. Deze gegevens niet gebruiken, is er vervolgens één opdracht uw app ontkoppelt van het virtuele netwerk.

    $vnet = Remove-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-07-01

## <a name="resource-manager-virtual-networks"></a>Virtuele netwerken van Resource Manager
Virtuele netwerken van Resource Manager hebben Azure Resource Manager-API's die bepaalde processen in vergelijking met het klassieke virtuele netwerken vereenvoudigen. Wij hebben een script waarmee u de volgende taken uitvoeren:

* Een virtueel netwerk van Resource Manager maken en uw app integreren.
* Maken van een gateway, punt-naar-site-connectiviteit in een bestaande Resource Manager virtueel netwerk configureren en vervolgens uw app integreren met het.
* Uw app integreren met een bestaand virtueel netwerk voor Resource Manager, dat een gateway en een punt-naar-site-connectiviteit ingeschakeld.
* Verbreek de verbinding tussen uw app in het virtuele netwerk.

### <a name="resource-manager-vnet-app-service-integration-script"></a>Script voor Resource Manager VNet-App Service-integratie
Kopieer het volgende script en sla deze op een bestand. Als u niet dat het script te gebruiken wilt, u kunt meer uit om te zien hoe dingen instellen met een virtueel netwerk van Resource Manager.

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

Sla een kopie van het script. In dit artikel V2VnetAllinOne.ps1 wordt aangeroepen, maar u kunt een andere naam. Er zijn geen argumenten voor dit script. U gewoon uitvoeren het. Het eerste wat dat het script doet is gevraagd u aan te melden. Nadat u zich aanmeldt, wordt het script haalt gegevens over uw account en retourneert een lijst met abonnementen. De aanvraag om uw referenties niet meegerekend, weergegeven uitvoering van het oorspronkelijke script als volgt:

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

    Geef de resourcegroep van uw App: Geef de naam van uw App hcdemo rg: v2vnetpowershell wat wilt u doen?

    1) Een nieuw virtueel netwerk toevoegen aan een App
    2) Een bestaand virtueel netwerk toevoegen aan een App
    3) Een virtueel netwerk verwijderen uit een App

De rest van dit gedeelte wordt elk van deze drie opties.

### <a name="create-a-resource-manager-vnet-and-integrate-with-it"></a>Een Resource Manager VNet maken en integreren met het
Voor het maken van een nieuwe virtuele netwerk dat gebruikmaakt van het implementatiemodel van Resource Manager en het integreren met uw app, selecteer **1) een nieuw virtueel netwerk toevoegen aan een App**. Hiermee wordt u gevraagd om de naam van het virtuele netwerk. In mijn geval, zoals u in de volgende instellingen ziet gebruikt ik de naam van de v2pshell.

Het script geeft de informatie over het virtuele netwerk dat wordt gemaakt. Als ik wil, kan ik een van de waarden te wijzigen. In dit voorbeeld wordt uitgevoerd, moet ik een virtueel netwerk met de volgende instellingen gemaakt:

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

Als u wijzigen van de waarden wilt, typt u **Y** en wijzigingen aanbrengen. Wanneer u tevreden over de instellingen van het virtuele netwerk bent, typt u **N** of drukt u op Enter wanneer u wordt gevraagd over het wijzigen van de instellingen. Vanaf dat moment tot voltooiing, het script vertelt u enkele van wat de it' i's doen totdat het begint te maken van de virtuele netwerkgateway. Deze stap kan een uur duren. Er is geen voortgangsindicator tijdens deze fase, maar het script kunt u weten wanneer de gateway is gemaakt.

Wanneer het script is voltooid, wordt er **voltooid**. Op dit moment hebt u een Resource Manager virtueel netwerk met de naam en de instellingen die u hebt geselecteerd. Deze nieuwe virtuele netwerk wordt ook worden geïntegreerd met uw app.

### <a name="integrate-your-app-with-a-preexisting-resource-manager-vnet"></a>Uw app integreren met een bestaande Resource Manager VNet
Wanneer u met een bestaand virtueel netwerk, integreren bent als u een Resource Manager virtueel netwerk dat geen gateway of punt-naar-site-connectiviteit bieden, wordt het script ingesteld die. Als het VNET al deze dingen instellen, gaat het script meteen naar de app-integratie. Om te starten, selecteert u de **2) een bestaand virtueel netwerk toevoegen aan een App**.

Deze optie werkt alleen als u een bestaand virtueel netwerk voor Resource Manager, dat zich in hetzelfde abonnement als uw app. Nadat u de optie selecteert, wordt er verschijnt een lijst met uw virtuele netwerken van Resource Manager.   

    Select a VNET to integrate with

    1) v2demonetwork
    2) v2pshell
    3) v2vnetintdemo
    4) v2asenetwork
    5) v2pshell2

    Kies een optie: 5

Het virtuele netwerk dat u integreren wilt met eenvoudig kunt selecteren. Als u al een gateway die voor punt-naar-site-connectiviteit is ingeschakeld, wordt het script gewoon uw app integreren met het virtuele netwerk. Als u een gateway niet hebt, moet u het gatewaysubnet opgeven. Het gatewaysubnet moet in de adresruimte van uw virtuele netwerk en deze kan niet in een ander subnet. Als u een virtueel netwerk zonder een gateway hebt en deze stap uitvoert, dingen moeten uitzien:

    This Virtual Network has no gateway. I will need to create one.
    Your VNET is in the address space 172.16.0.0/16, with the following Subnets:
    default: 172.16.0.0/24
    Please choose a GatewaySubnet address space: 172.16.1.0/26

In dit voorbeeld moet ik een virtuele netwerkgateway met de volgende instellingen gemaakt:

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

Als u een van deze instellingen wijzigt wilt, kunt u dit doet. Anders, druk op Enter en het script wordt gemaakt van uw gateway en uw app koppelen aan het virtuele netwerk. De aanmaaktijd van de gateway is echter nog steeds een uur, dus zorg ervoor dat u die rekening houden. Als alles is voltooid, het script dicteert **voltooid**.

### <a name="disconnect-your-app-from-a-resource-manager-vnet"></a>Verbreek de verbinding tussen uw app een Resource Manager VNet
Het virtuele netwerk van uw app verbreken niet noteren de gateway of punt-naar-site-connectiviteit uitschakelen. U, nadat alle gebruikt deze voor iets anders. Deze wordt ook niet verbroken deze van alle andere apps dan die u hebt opgegeven. Om deze actie niet uitvoeren, selecteert u **3) een virtueel netwerk verwijderen uit een App**. Als u doet dit, ziet u ongeveer het volgende:

    Currently connected to VNET v2pshell

    Confirm
    Are you sure you want to delete the following resource:
    /subscriptions/edcc99a4-b7f9-4b5e-a9a1-3034c51db496/resourceGroups/hcdemo-rg/providers/Microsoft.Web/sites/v2vnetpowers
    hell/virtualNetworkConnections/v2pshell
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):

Hoewel het script verwijderen staat, verwijdert het virtuele netwerk niet meer. Het worden zojuist de integratie verwijderd. Nadat u bevestigen dat dit is wat u wilt doen, de opdracht erg snel wordt verwerkt en vertelt u **True** wanneer het is voltooid.

<!--Links-->
[createvpngateway]: http://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/
[azureportal]: http://portal.azure.com
