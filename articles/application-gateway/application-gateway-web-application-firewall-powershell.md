---
title: aaaConfigure web application firewall - Azure Application Gateway | Microsoft Docs
description: In dit artikel biedt richtlijnen voor hoe toostart met behulp van web application firewall op een bestaande of nieuwe Application Gateway.
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 670b9732-874b-43e6-843b-d2585c160982
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: gwallace
ms.openlocfilehash: bd2a69901f0ec0d6551d633e2588b74c3ab59a71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway"></a>Web application firewall configureren op een nieuwe of bestaande Application Gateway

> [!div class="op_single_selector"]
> * [Azure Portal](application-gateway-web-application-firewall-portal.md)
> * [PowerShell](application-gateway-web-application-firewall-powershell.md)
> * [Azure-CLI](application-gateway-web-application-firewall-cli.md)

Meer informatie over hoe toocreate web application firewall ingeschakeld voor Application Gateway of web application firewall tooan bestaande toepassingsgateway toevoegen.

Hallo web application firewall (WAF) in Azure Application Gateway beveiligt webtoepassingen van algemene web gebaseerde aanvallen, zoals SQL-injectie, cross-site scripting aanvallen en sessie hijacks.

Azure Application Gateway is een load balancer in laag 7. Het biedt failover, HTTP-aanvragen routeren tussen verschillende servers, ongeacht of deze op Hallo cloud of on-premises. Toepassingsgateway biedt veel levering controller (ADC) toepassingsfuncties zoals HTTP taakverdeling, cookies gebaseerde affiniteit van de sessie laden, secure sockets layer (SSL)-offload, aangepaste statuscontroles, ondersteuning voor meerdere locaties en vele andere. toofind een volledige lijst van ondersteunde functies, gaat u naar: [overzicht van toepassingsgateway](application-gateway-introduction.md).

Hallo volgende artikel laat zien hoe te[web application firewall tooan bestaande toepassingsgateway toevoegen](#add-web-application-firewall-to-an-existing-application-gateway) en [maken van een toepassingsgateway die gebruikmaakt van web application firewall](#create-an-application-gateway-with-web-application-firewall).

![afbeelding van scenario][scenario]

## <a name="waf-configuration-differences"></a>WAF configuratie verschillen

Als u hebt gelezen [een toepassingsgateway maken met PowerShell](application-gateway-create-gateway-arm.md), u begrijpt Hallo SKU instellingen tooconfigure bij het maken van een toepassingsgateway. WAF biedt extra instellingen toodefine bij het configureren van Hallo SKU voor een toepassingsgateway. Er zijn geen aanvullende wijzigingen die u op Hallo Application Gateway zelf aanbrengt.

| **Instelling** | **Details**
|---|---|
|**SKU** |Een normale toepassingsgateway zonder WAF ondersteunt **standaard\_kleine**, **standaard\_gemiddeld**, en **standaard\_grote** grootten. Dankzij de introductie van de Hallo van WAF, er zijn twee extra SKU's **WAF\_gemiddeld** en **WAF\_grote**. WAF wordt niet ondersteund op kleine Toepassingsgateways.|
|**Laag** | Hallo beschikbare waarden zijn **standaard** of **WAF**. Bij gebruik van web application firewall, **WAF** moeten worden gekozen.|
|**Modus** | Deze instelling is Hallo-modus van WAF. toegestane waarden zijn **detectie** en **preventie**. Wanneer WAF is ingesteld in de modus voor detectie, worden alle bedreigingen opgeslagen in een logboekbestand. Gebeurtenissen worden nog wel geregistreerd in '-modus, maar Hallo aanvaller 403 onbevoegde-antwoord van Hallo Application Gateway ontvangt.|

## <a name="add-web-application-firewall-tooan-existing-application-gateway"></a>Web application firewall tooan bestaande toepassingsgateway toevoegen

Zorg ervoor dat u van Hallo meest recente versie van Azure PowerShell gebruikmaakt. Zie [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Windows PowerShell gebruiken met Resource Manager) voor meer informatie.

1. Meld u bij tooyour Azure-Account.

    ```powershell
    Login-AzureRmAccount
    ```

2. Selecteer Hallo abonnement toouse voor dit scenario.

    ```powershell
    Select-AzureRmSubscription -SubscriptionName "<Subscription name>"
    ```

3. Hallo-gateway die u web application firewall om te toevoegen wilt worden opgehaald.

    ```powershell
    $gw = Get-AzureRmApplicationGateway -Name "AdatumGateway" -ResourceGroupName "MyResourceGroup"
    ```

1. Hallo web application firewall sku configureren. Hallo beschikbare grootten zijn **WAF\_grote** en **WAF\_gemiddeld**. Bij gebruik van web application firewall Hallo laag moet **WAF**, Hallo capaciteit moet worden bevestigd bij het instellen van Hallo sku.

    ```powershell
    $gw | Set-AzureRmApplicationGatewaySku -Name WAF_Large -Tier WAF -Capacity 2
    ```

1. Hallo WAF instellingen te configureren zoals gedefinieerd in het volgende voorbeeld Hallo:

   Voor **FirewallMode**, Hallo beschikbare waarden zijn preventie en detectie.

    ```powershell
    $gw | Set-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode Prevention
    ```

1. Hallo Application Gateway met Hallo-instellingen die zijn gedefinieerd in de voorgaande stap Hallo bijgewerkt.

    ```powershell
    Set-AzureRmApplicationGateway -ApplicationGateway $gw
    ```

Met deze opdracht werkt Hallo Application Gateway met web application firewall. Ga naar [Application Gateway diagnostics](application-gateway-diagnostics.md) toounderstand hoe tooview voor uw toepassingsgateway registreert. Vervaldatum toohello aard van de beveiliging van WAF beoordeeld logboeken moeten toobe regelmatig toounderstand Hallo-beveiligingsstatus van uw webtoepassingen.

## <a name="create-an-application-gateway-with-web-application-firewall"></a>Een toepassingsgateway maken met web application firewall

Hallo gaat volgende stappen u door de hele proces Hallo van begin tooend voor het maken van een toepassingsgateway met web application firewall.

Zorg ervoor dat u van Hallo meest recente versie van Azure PowerShell gebruikmaakt. Zie [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Windows PowerShell gebruiken met Resource Manager) voor meer informatie.

1. Meld u bij tooAzure door het uitvoeren van `Login-AzureRmAccount`, u tooauthenticate na vragen aan gebruiker zich met uw referenties.

1. Hallo-abonnementen voor Hallo account controleren door te voeren`Get-AzureRmSubscription`

1. Kies welke van uw Azure-abonnementen toouse.

    ```powershell
    Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
    ```

### <a name="create-a-resource-group"></a>Een resourcegroep maken

Maak een resourcegroep voor Hallo Application Gateway.

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

Azure Resource Manager vereist dat er voor alle resourcegroepen een locatie wordt opgegeven. Deze locatie wordt gebruikt als Hallo standaardlocatie voor resources in die resourcegroep. Zorg ervoor dat alle opdrachten die gebruikmaakt van toocreate een toepassingsgateway dezelfde resourcegroep Hallo.

In Hallo voorgaande voorbeeld, er gemaakt met een resourcegroep genaamd "Appgw-RG' en de locatie 'VS-West."

> [!NOTE]
> Als u voor uw toepassingsgateway een aangepaste test tooconfigure nodig hebt, raadpleegt u [met PowerShell een toepassingsgateway maken met aangepaste tests](application-gateway-create-probe-ps.md). Bekijk [Custom probes and health monitoring](application-gateway-probe-overview.md) (Aangepaste tests en statusbewaking) voor meer informatie.

### <a name="configure-virtual-network"></a>Virtueel netwerk configureren

Toepassingsgateway vereist een subnet van een eigen. In deze stap maakt u een virtueel netwerk met een adresruimte van 10.0.0.0/16 en twee subnetten, één voor Application Gateway Hallo en één voor de back-end-groepsleden.

```powershell
# Create a subnet configuration object for hello Application Gateway subnet. A subnet for an application should have a minimum of 28 mask bits. This value leaves 10 available addresses in hello subnet for Application Gateway instances. With a smaller subnet, you may not be able tooadd more instance of your Application Gateway in hello future.
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24

# Create a subnet configuration object for hello backend pool members subnet
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24

# Create hello virtual network with hello previous created subnets
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="configure-public-ip-address"></a>Openbare IP-adres configureren

Application Gateway vereist in volgorde toohandle externe aanvragen, een openbare IP-adres. Dit openbare IP-adres mag niet hebben een `DomainNameLabel` toobe die wordt gebruikt door Hallo Application Gateway gedefinieerd.

```powershell
# Create a public IP address for use with hello Application Gateway. Defining hello domainnamelabel during creation is not supported for use with Application Gateway
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name 'appgwpip' -Location "West US" -AllocationMethod Dynamic
```

### <a name="configure-hello-application-gateway"></a>Hallo Application Gateway configureren

```powershell
# Create a IP configuration. This configures what subnet hello Application Gateway uses. When Application Gateway starts, it picks up an IP address from hello subnet configured and routes network traffic toohello IP addresses in hello back-end IP pool.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet

# Create a backend pool toohold hello addresses or NICs for hello application that Application Gateway is protecting.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3

# Upload hello authenication certificate that will be used toocommunicate with hello backend servers
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile <full path too.cer file>

# Conifugre hello backend HTTP settings toobe used toodefine how traffic is routed toohello backend pool. hello authenication certificate used in hello previous step is added toohello backend http settings.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert

# Create a frontend port toobe used by hello listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443

# Create a frontend IP configuration tooassociate hello public IP address with hello Application Gateway
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip

# Configure hello certificate for hello Application Gateway. This certificate is used toodecrypt and re-encrypt hello traffic on hello Application Gateway.
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path too.pfx file> -Password <password for certificate file>

# Create hello HTTP listener for hello Application Gateway. Assign hello front-end ip configuration, port, and ssl certificate toouse.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert

#Create a load balancer routing rule that configures hello load balancer behavior. In this example, a basic round robin rule is created.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Configure hello SKU of hello Application Gateway
$sku = New-AzureRmApplicationGatewaySku -Name WAF_Medium -Tier WAF -Capacity 2

# Define hello SSL policy toouse
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S

#Configure hello waf configuration settings.
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"

# Create hello Application Gateway utilizing all hello previously created configuration objects
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert
```

> [!NOTE]
> Toepassingsgateways gemaakt met de Hallo basic web application firewall-configuratie zijn geconfigureerd met CRS 3.0 voor beveiliging.

## <a name="get-application-gateway-dns-name"></a>Ophalen van Application Gateway DNS-naam

Zodra Hallo gateway is gemaakt, is de volgende stap Hallo tooconfigure Hallo front-end voor communicatie. Wanneer u een openbaar IP-adres, vereist de toepassingsgateway een dynamisch toegewezen DNS-naam, geen beschrijvende is. tooensure eindgebruikers Hallo Application Gateway kan worden bereikt, een CNAME-record kan gebruikte toopoint toohello openbaar eindpunt Hallo Application Gateway. [Een aangepaste domeinnaam configureren voor in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md). een alias tooconfigure ophalen van gegevens van Hallo Application Gateway en de bijbehorende IP-en DNS-naam op Hallo PublicIPAddress element gekoppeld toohello Application Gateway met. Hallo Application Gateway DNS-naam moet gebruikte toocreate een CNAME-record punten Hallo twee web applications toothis DNS-naam. Hallo-gebruik van A-records wordt niet aanbevolen omdat Hallo VIP bij opnieuw opstarten van toepassingsgateway mag wijzigen.

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

Meer informatie over hoe tooconfigure Diagnostische logboekregistratie, toolog Hallo gebeurtenissen die zijn gedetecteerd of voorkomen met web application firewall in via [Application Gateway Diagnostics](application-gateway-diagnostics.md)

[scenario]: ./media/application-gateway-web-application-firewall-powershell/scenario.png
