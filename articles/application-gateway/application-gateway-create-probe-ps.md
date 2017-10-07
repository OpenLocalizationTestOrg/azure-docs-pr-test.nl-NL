---
title: een aangepaste aaaCreate probe - Azure Application Gateway - PowerShell | Microsoft Docs
description: Meer informatie over hoe toocreate een aangepaste test voor Application Gateway met behulp van PowerShell in Resource Manager
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 68feb660-7fa4-4f69-a7e4-bdd7bdc474db
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: 44c9ffa75401d6d0db023e66fa82c701fb0cf8bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-probe-for-azure-application-gateway-by-using-powershell-for-azure-resource-manager"></a>Maken van een aangepaste test voor Azure Application Gateway met behulp van PowerShell voor Azure Resource Manager

> [!div class="op_single_selector"]
> * [Azure Portal](application-gateway-create-probe-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-probe-ps.md)
> * [Azure Classic PowerShell](application-gateway-create-probe-classic-ps.md)

In dit artikel voegt u een aangepaste test tooan bestaande application gateway met PowerShell. Aangepaste tests zijn handig voor toepassingen die de pagina controle van een specifieke status hebben, of voor toepassingen die een geslaagde reactie op Hallo standaardwebtoepassing geen bieden.

> [!NOTE]
> Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../azure-resource-manager/resource-manager-deployment-model.md).  In dit artikel wordt beschreven hoe u Hallo Resource Manager-implementatiemodel, die Microsoft voor de meeste nieuwe implementaties in plaats van Hallo aanbeveelt [klassieke implementatiemodel](application-gateway-create-probe-classic-ps.md).

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway-with-a-custom-probe"></a>Een toepassingsgateway maken met een aangepaste test

### <a name="sign-in-and-create-resource-group"></a>Aanmelden en resourcegroep maken

1. Gebruik `Login-AzureRmAccount` tooauthenticate.

  ```powershell
  Login-AzureRmAccount
  ```

1. Hallo-abonnementen voor Hallo account krijgen.

  ```powershell
  Get-AzureRmSubscription
  ```

1. Kies welke van uw Azure-abonnementen toouse.

  ```powershell
  Select-AzureRmSubscription -Subscriptionid '{subscriptionGuid}'
  ```

1. Maak een resourcegroep. Als u een bestaande resourcegroep hebt, kunt u deze stap overslaan.

  ```powershell
  New-AzureRmResourceGroup -Name appgw-rg -Location 'West US'
  ```

Azure Resource Manager vereist dat er voor alle resourcegroepen een locatie wordt opgegeven. Deze locatie wordt gebruikt als Hallo standaardlocatie voor resources in die resourcegroep. Zorg ervoor dat alle opdrachten toocreate een application gateway gebruik Hallo dezelfde resourcegroep.

In Hallo voorgaande voorbeeld, is er een resourcegroep aangeroepen gemaakt **appgw-RG** op locatie **VS-West**.

### <a name="create-a-virtual-network-and-a-subnet"></a>Een virtueel netwerk en een subnet maken

Hallo volgende voorbeeld wordt een virtueel netwerk en een subnet voor de toepassingsgateway Hallo. Toepassingsgateway vereist een eigen subnet voor gebruik. Om deze reden moet Hallo subnet gemaakt voor de toepassingsgateway Hallo kleiner zijn dan de adresruimte Hallo van Hallo VNET tooallow voor andere subnetten toobe gemaakt en gebruikt.

```powershell
# Assign hello address range 10.0.0.0/24 tooa subnet variable toobe used toocreate a virtual network.
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24

# Create a virtual network named appgwvnet in resource group appgw-rg for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24.
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $subnet

# Assign a subnet variable for hello next steps, which create an application gateway.
$subnet = $vnet.Subnets[0]
```

### <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>Een openbaar IP-adres voor de front-endconfiguratie Hallo maken

Maak een openbare IP-resource **publicIP01** in de resourcegroep **appgw-rg** voor de regio VS-West Hallo. Dit voorbeeld wordt een openbaar IP-adres voor front-end-IP-adres van de toepassingsgateway Hallo Hallo.  Toepassingsgateway Hallo openbare IP-adres toohave een dynamisch gemaakte DNS-naam Hallo daarom vereist `-DomainNameLabel` tijdens het maken van Hallo Hallo openbare IP-adres kan niet worden opgegeven.

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name publicIP01 -Location 'West US' -AllocationMethod Dynamic
```

### <a name="create-an-application-gateway"></a>Een toepassingsgateway maken

U instellen alle configuratie-items voordat u de toepassingsgateway Hallo maakt. Hallo maakt volgende voorbeeld Hallo configuratie-items die nodig zijn voor een toepassingsgatewayresource.

| **Onderdeel** | **Beschrijving** |
|---|---|
| **Toepassingsgateway IP-configuratie** | Een IP-configuratie voor een toepassingsgateway.|
| **Back-endpool** | Een pool van IP-adressen, FQDN's of NIC's die zijn toohello toepassingsservers die als host Hallo-webtoepassing fungeren|
| **De statuscontrole** | Een aangepaste test toomonitor Hallo status van de back-end-groepsleden Hallo gebruikt|
| **HTTP-instellingen** | Een verzameling met inbegrip van instellingen, poort, protocol, cookies gebaseerde affiniteit, test en time-out.  Deze instellingen bepalen hoe verkeer wordt gerouteerd toohello back-end-groepsleden|
| **Front-endpoort** | Hallo-poort die Hallo toepassingsgateway luistert voor verkeer op|
| **Listener** | Een combinatie van een protocol, de frontend-IP-configuratie en de frontend-poort. Dit is wat luistert naar binnenkomende aanvragen.
|**Regel**| Routes Hallo verkeer toohello juiste back-end op basis van HTTP-instellingen.|

```powershell
# Creates a application gateway Frontend IP configuration named gatewayIP01
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet

#Creates a back-end IP address pool named pool01 with IP addresses 134.170.185.46, 134.170.188.221, 134.170.185.50.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

# Creates a probe that will check health at http://contoso.com/path/path.htm
$probe = New-AzureRmApplicationGatewayProbeConfig -Name probe01 -Protocol Http -HostName 'contoso.com' -Path '/path/path.htm' -Interval 30 -Timeout 120 -UnhealthyThreshold 8

# Creates hello backend http settings toobe used. This component references hello $probe created in hello previous command.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Disabled -Probe $probe -RequestTimeout 80

# Creates a frontend port for hello application gateway toolisten on port 80 that will be used by hello listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01 -Port 80

# Creates a frontend IP configuration. This associates hello $publicip variable defined previously with hello front-end IP that will be used by hello listener.
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip

# Creates hello listener. hello listener is a combination of protocol and hello frontend IP configuration $fipconfig and frontend port $fp created in previous steps.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp

# Creates hello rule that routes traffic toohello backend pools.  In this example we create a basic rule that uses hello previous defined http settings and backend address pool.  It also associates hello listener toohello rule
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Sets hello SKU of hello application gateway, in this example we create a small standard application gateway with 2 instances.
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2

# hello final step creates hello application gateway with all hello previously defined components.
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location 'West US' -BackendAddressPools $pool -Probes $probe -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

## <a name="add-a-probe-tooan-existing-application-gateway"></a>Een test tooan bestaande toepassingsgateway toevoegen

Hallo voegt volgende codefragment een test tooan bestaande toepassingsgateway.

```powershell
# Load hello application gateway resource into a PowerShell variable by using Get-AzureRmApplicationGateway.
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg

# Create hello probe object that will check health at http://contoso.com/path/path.htm
$getgw = Add-AzureRmApplicationGatewayProbeConfig -ApplicationGateway $getgw -Name probe01 -Protocol Http -HostName 'contoso.com' -Path '/path/custompath.htm' -Interval 30 -Timeout 120 -UnhealthyThreshold 8

# Set hello backend HTTP settings toouse hello new probe
$getgw = Set-AzureRmApplicationGatewayBackendHttpSettings -ApplicationGateway $getgw -Name $getgw.BackendHttpSettingsCollection.name -Port 80 -Protocol Http -CookieBasedAffinity Disabled -Probe $probe -RequestTimeout 120

# Save hello application gateway with hello configuration changes
Set-AzureRmApplicationGateway -ApplicationGateway $getgw
```

## <a name="remove-a-probe-from-an-existing-application-gateway"></a>Een test uit een bestaande toepassingsgateway verwijderen

Hallo volgende codefragment verwijdert een test van een bestaande toepassingsgateway.

```powershell
# Load hello application gateway resource into a PowerShell variable by using Get-AzureRmApplicationGateway.
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg

# Remove hello probe from hello application gateway configuration object
$getgw = Remove-AzureRmApplicationGatewayProbeConfig -ApplicationGateway $getgw -Name $getgw.Probes.name

# Set hello backend HTTP settings tooremove hello reference toohello probe. hello backend http settings now use hello default probe
$getgw = Set-AzureRmApplicationGatewayBackendHttpSettings -ApplicationGateway $getgw -Name $getgw.BackendHttpSettingsCollection.name -Port 80 -Protocol http -CookieBasedAffinity Disabled

# Save hello application gateway with hello configuration changes
Set-AzureRmApplicationGateway -ApplicationGateway $getgw
```

## <a name="get-application-gateway-dns-name"></a>DNS-naam van toepassingsgateway verkrijgen

Zodra Hallo gateway is gemaakt, is de volgende stap Hallo tooconfigure Hallo front-end voor communicatie. Wanneer u een openbare IP gebruikt, heeft de toepassingsgateway een dynamisch toegewezen DNS-naam nodig. Dit is niet gebruiksvriendelijk. tooensure eindgebruikers Hallo toepassingsgateway een CNAME-record kan worden gebruikt. Druk toopoint toohello openbaar eindpunt van de toepassingsgateway Hallo. [Een aangepaste domeinnaam configureren voor in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md). toodo deze, details ophalen van de toepassingsgateway Hallo en de bijbehorende IP-en DNS-naam op Hallo PublicIPAddress element gekoppelde toohello application gateway met. Hallo application gateway DNS-naam moet gebruikte toocreate een CNAME-record punten Hallo twee web applications toothis DNS-naam. Hallo-gebruik van A-records wordt niet aanbevolen omdat Hallo VIP bij opnieuw opstarten van toepassingsgateway mag wijzigen.

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -Name publicIP01
```

```
Name                     : publicIP01
ResourceGroupName        : appgw-RG
Location                 : westus
Id                       : /subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/publicIPAddresses/publicIP01
Etag                     : W/"00000d5b-54ed-4907-bae8-99bd5766d0e5"
ResourceGuid             : 00000000-0000-0000-0000-000000000000
ProvisioningState        : Succeeded
Tags                     : 
PublicIpAllocationMethod : Dynamic
IpAddress                : xx.xx.xxx.xx
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : {
                                "Id": "/subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/applicationGateways/appgwtest/frontendIP
                            Configurations/frontend1"
                            }
DnsSettings              : {
                                "Fqdn": "00000000-0000-xxxx-xxxx-xxxxxxxxxxxx.cloudapp.net"
                            }
```

## <a name="next-steps"></a>Volgende stappen

Meer informatie over tooconfigure SSL-offloading in via: [SSL-Offload configureren](application-gateway-ssl-arm.md)

