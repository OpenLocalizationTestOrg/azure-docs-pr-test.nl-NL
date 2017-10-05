---
title: Web application firewall - Azure Application Gateway configureren | Microsoft Docs
description: In dit artikel biedt richtlijnen voor het gebruik van web application firewall op een bestaande of nieuwe Application Gateway.
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
ms.openlocfilehash: dab489a1c9fb7d4a51b9ccbce543b209bec23575
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway"></a>Web application firewall configureren op een nieuwe of bestaande Application Gateway

> [!div class="op_single_selector"]
> * [Azure Portal](application-gateway-web-application-firewall-portal.md)
> * [PowerShell](application-gateway-web-application-firewall-powershell.md)
> * [Azure-CLI](application-gateway-web-application-firewall-cli.md)

Informatie over het maken van een webtoepassing firewall ingeschakeld Application Gateway of web application firewall toevoegen aan een bestaande Application Gateway.

De web application firewall (WAF) in Azure Application Gateway beveiligt webtoepassingen van algemene web gebaseerde aanvallen, zoals SQL-injectie, cross-site scripting aanvallen en sessie hijacks.

Azure Application Gateway is een load balancer in laag 7. De gateway biedt opties voor failovers en het routeren van HTTP-aanvragen tussen servers (on-premises en in de cloud). Toepassingsgateway biedt veel levering controller (ADC) toepassingsfuncties zoals HTTP taakverdeling, cookies gebaseerde affiniteit van de sessie laden, secure sockets layer (SSL)-offload, aangepaste statuscontroles, ondersteuning voor meerdere locaties en vele andere. Ga voor een volledige lijst met ondersteunde functies naar: [overzicht van toepassingsgateway](application-gateway-introduction.md).

Het volgende artikel toont hoe [web application firewall toevoegen aan een bestaande toepassingsgateway](#add-web-application-firewall-to-an-existing-application-gateway) en [maken van een toepassingsgateway die gebruikmaakt van web application firewall](#create-an-application-gateway-with-web-application-firewall).

![afbeelding van scenario][scenario]

## <a name="waf-configuration-differences"></a>WAF configuratie verschillen

Als u hebt gelezen [een toepassingsgateway maken met PowerShell](application-gateway-create-gateway-arm.md), u inzicht in de SKU-instellingen bij het maken van een toepassingsgateway configureren. WAF biedt aanvullende instellingen op te geven bij het configureren van de SKU voor een toepassingsgateway. Er zijn geen aanvullende wijzigingen die u in de toepassingsgateway zelf aanbrengt.

| **Instelling** | **Details**
|---|---|
|**SKU** |Een normale toepassingsgateway zonder WAF ondersteunt **standaard\_kleine**, **standaard\_gemiddeld**, en **standaard\_grote** grootten. Dankzij de introductie van WAF, er zijn twee extra SKU's **WAF\_gemiddeld** en **WAF\_grote**. WAF wordt niet ondersteund op kleine Toepassingsgateways.|
|**Laag** | De beschikbare waarden zijn **standaard** of **WAF**. Bij gebruik van web application firewall, **WAF** moeten worden gekozen.|
|**Modus** | Deze instelling wordt de modus van WAF. toegestane waarden zijn **detectie** en **preventie**. Wanneer WAF is ingesteld in de modus voor detectie, worden alle bedreigingen opgeslagen in een logboekbestand. Gebeurtenissen worden nog wel geregistreerd in de modus te voorkomen, maar de aanvaller ontvangt een niet-geautoriseerde 403-antwoord van de toepassingsgateway.|

## <a name="add-web-application-firewall-to-an-existing-application-gateway"></a>Web application firewall toevoegen aan een bestaande Application Gateway

Zorg ervoor dat u de nieuwste versie van Azure PowerShell gebruikt. Zie [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Windows PowerShell gebruiken met Resource Manager) voor meer informatie.

1. Aanmelden bij uw Azure-Account.

    ```powershell
    Login-AzureRmAccount
    ```

2. Selecteer het abonnement moet worden gebruikt voor dit scenario.

    ```powershell
    Select-AzureRmSubscription -SubscriptionName "<Subscription name>"
    ```

3. De gateway die u web application firewall om te toevoegen wilt worden opgehaald.

    ```powershell
    $gw = Get-AzureRmApplicationGateway -Name "AdatumGateway" -ResourceGroupName "MyResourceGroup"
    ```

1. De sku van web application firewall configureren. De beschikbare grootten zijn **WAF\_grote** en **WAF\_gemiddeld**. Als u web application firewall gebruikt de laag moet **WAF**, de capaciteit moet worden bevestigd bij het instellen van de sku.

    ```powershell
    $gw | Set-AzureRmApplicationGatewaySku -Name WAF_Large -Tier WAF -Capacity 2
    ```

1. Configureer de instellingen WAF zoals gedefinieerd in het volgende voorbeeld:

   Voor **FirewallMode**, de beschikbare waarden zijn preventie en detectie.

    ```powershell
    $gw | Set-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode Prevention
    ```

1. De toepassingsgateway bijwerken met de instellingen die zijn gedefinieerd in de vorige stap.

    ```powershell
    Set-AzureRmApplicationGateway -ApplicationGateway $gw
    ```

Deze opdracht werkt u de toepassingsgateway met web application firewall. Ga naar [Application Gateway diagnostics](application-gateway-diagnostics.md) om te begrijpen hoe logboeken bekijken voor uw toepassingsgateway. Vanwege de aard van de beveiliging van WAF moeten Logboeken regelmatig worden gecontroleerd om te begrijpen van de beveiligingsstatus van uw webtoepassingen.

## <a name="create-an-application-gateway-with-web-application-firewall"></a>Een toepassingsgateway maken met web application firewall

De volgende stappen gaat u door het hele proces van begin tot eind voor het maken van een toepassingsgateway met web application firewall.

Zorg ervoor dat u de nieuwste versie van Azure PowerShell gebruikt. Zie [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Windows PowerShell gebruiken met Resource Manager) voor meer informatie.

1. Meld u aan bij Azure door het uitvoeren van `Login-AzureRmAccount`, u wordt gevraagd te verifiëren met uw referenties.

1. Controleer de abonnementen voor het account door te voeren`Get-AzureRmSubscription`

1. Kies welk Azure-abonnement u wilt gebruiken.

    ```powershell
    Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
    ```

### <a name="create-a-resource-group"></a>Een resourcegroep maken

Een resourcegroep maken voor de toepassingsgateway.

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

Azure Resource Manager vereist dat er voor alle resourcegroepen een locatie wordt opgegeven. Deze locatie wordt gebruikt als de standaardlocatie voor resources in die resourcegroep. Zorg ervoor dat alle opdrachten voor het maken van een toepassingsgateway dezelfde resourcegroep gebruikt.

In het voorgaande voorbeeld is er een resourcegroep met de naam 'appgw-RG' en de locatie 'VS-West.' gemaakt

> [!NOTE]
> Als u een aangepaste test voor uw toepassingsgateway configureren moet, Zie [met PowerShell een toepassingsgateway maken met aangepaste tests](application-gateway-create-probe-ps.md). Bekijk [Custom probes and health monitoring](application-gateway-probe-overview.md) (Aangepaste tests en statusbewaking) voor meer informatie.

### <a name="configure-virtual-network"></a>Virtueel netwerk configureren

Toepassingsgateway vereist een subnet van een eigen. In deze stap maakt u een virtueel netwerk met een adresruimte van 10.0.0.0/16 en twee subnetten, één voor de toepassingsgateway en één voor de back-end-groepsleden.

```powershell
# Create a subnet configuration object for the Application Gateway subnet. A subnet for an application should have a minimum of 28 mask bits. This value leaves 10 available addresses in the subnet for Application Gateway instances. With a smaller subnet, you may not be able to add more instance of your Application Gateway in the future.
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24

# Create a subnet configuration object for the backend pool members subnet
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24

# Create the virtual network with the previous created subnets
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="configure-public-ip-address"></a>Openbare IP-adres configureren

Application Gateway vereist om te kunnen verwerken van externe aanvragen, een openbare IP-adres. Dit openbare IP-adres mag niet hebben een `DomainNameLabel` gedefinieerd die worden gebruikt door de toepassingsgateway.

```powershell
# Create a public IP address for use with the Application Gateway. Defining the domainnamelabel during creation is not supported for use with Application Gateway
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name 'appgwpip' -Location "West US" -AllocationMethod Dynamic
```

### <a name="configure-the-application-gateway"></a>De toepassingsgateway configureren

```powershell
# Create a IP configuration. This configures what subnet the Application Gateway uses. When Application Gateway starts, it picks up an IP address from the subnet configured and routes network traffic to the IP addresses in the back-end IP pool.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet

# Create a backend pool to hold the addresses or NICs for the application that Application Gateway is protecting.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3

# Upload the authenication certificate that will be used to communicate with the backend servers
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile <full path to .cer file>

# Conifugre the backend HTTP settings to be used to define how traffic is routed to the backend pool. The authenication certificate used in the previous step is added to the backend http settings.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert

# Create a frontend port to be used by the listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443

# Create a frontend IP configuration to associate the public IP address with the Application Gateway
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip

# Configure the certificate for the Application Gateway. This certificate is used to decrypt and re-encrypt the traffic on the Application Gateway.
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path to .pfx file> -Password <password for certificate file>

# Create the HTTP listener for the Application Gateway. Assign the front-end ip configuration, port, and ssl certificate to use.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert

#Create a load balancer routing rule that configures the load balancer behavior. In this example, a basic round robin rule is created.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Configure the SKU of the Application Gateway
$sku = New-AzureRmApplicationGatewaySku -Name WAF_Medium -Tier WAF -Capacity 2

# Define the SSL policy to use
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S

#Configure the waf configuration settings.
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"

# Create the Application Gateway utilizing all the previously created configuration objects
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert
```

> [!NOTE]
> Toepassingsgateways gemaakt met de basic web application firewall-configuratie zijn geconfigureerd met CRS 3.0 voor beveiliging.

## <a name="get-application-gateway-dns-name"></a>Ophalen van Application Gateway DNS-naam

Wanneer de gateway is gemaakt, gaat u in de volgende stap de front-end voor communicatie configureren. Wanneer u een openbaar IP-adres, vereist de toepassingsgateway een dynamisch toegewezen DNS-naam, geen beschrijvende is. Om ervoor te zorgen eindgebruikers kunnen de toepassingsgateway bereikt, kan een CNAME-record worden gebruikt om te verwijzen naar het openbare eindpunt van de toepassingsgateway. [Een aangepaste domeinnaam configureren voor in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md). Voor het configureren van een alias ophalen van gegevens van de toepassingsgateway en de bijbehorende IP-en DNS-naam met behulp van de PublicIPAddress-element dat is gekoppeld aan de toepassingsgateway. De toepassingsgateway DNS-naam moet worden gebruikt voor het maken van een CNAME-record die de twee webtoepassingen aan deze DNS-naam wijst. Het gebruik van A-records wordt niet aanbevolen, omdat het VIP bij opnieuw opstarten van toepassingsgateway mag wijzigen.

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

Informatie over het configureren van diagnostische gegevens vastleggen voor de gebeurtenissen die zijn gedetecteerd of voorkomen met web application firewall logboekregistratie in via [Application Gateway Diagnostics](application-gateway-diagnostics.md)

[scenario]: ./media/application-gateway-web-application-firewall-powershell/scenario.png
