---
title: Configureren van SSL-offload - Azure Application Gateway - PowerShell | Microsoft Docs
description: Op deze pagina vindt u instructies voor het maken van een toepassingsgateway met SSL-offload met behulp van Azure Resource Manager
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 3c3681e0-f928-4682-9d97-567f8e278e13
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: ededabc7c665d6bb05b91e4d21d01fb1379add32
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-azure-resource-manager"></a>Een toepassingsgateway configureren voor SSL-offload met Azure Resource Manager

> [!div class="op_single_selector"]
> * [Azure Portal](application-gateway-ssl-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-ssl-arm.md)
> * [Azure Classic PowerShell](application-gateway-ssl.md)
> * [Azure CLI 2.0](application-gateway-ssl-cli.md)

Azure Application Gateway kan zodanig worden geconfigureerd dat de Secure Sockets Layer-sessie (SSL) wordt beëindigd bij de gateway om kostbare SSL-ontsleutelingstaken te voorkomen die worden uitgevoerd in de webfarm. Met SSL-offload worden ook het instellen van de front-endserver en het beheer van de webtoepassing eenvoudiger.

## <a name="before-you-begin"></a>Voordat u begint

1. Installeer de nieuwste versie van de Azure PowerShell-cmdlets via het webplatforminstallatieprogramma. U kunt de nieuwste versie downloaden en installeren via het gedeelte **Windows PowerShell** op de pagina [Downloads](https://azure.microsoft.com/downloads/).
2. Maak een virtueel netwerk en een subnet voor de toepassingsgateway. Zorg ervoor dat er geen virtuele machines en cloudimplementaties zijn die gebruikmaken van het subnet. De toepassingsgateway moet afzonderlijk in een subnet van een virtueel netwerk staan.
3. De servers die u voor gebruik van de toepassingsgateway configureert, moeten al bestaan in het virtuele netwerk of hier hun eindpunten hebben. Een andere optie is om er een openbaar IP- of VIP-adres aan toe te wijzen.

## <a name="what-is-required-to-create-an-application-gateway"></a>Wat is er vereist om een toepassingsgateway te maken?

* **Back-endserverpool:** de lijst met IP-adressen van de back-endservers. De IP-adressen moeten ofwel deel uitmaken van het subnet van het virtuele netwerk, ofwel openbare IP-/VIP-adressen zijn.
* **Back-endserverpoolinstellingen:** elke pool heeft instellingen, zoals voor de poort, het protocol en de op cookies gebaseerde affiniteit. Deze instellingen zijn gekoppeld aan een pool en worden toegepast op alle servers in de pool.
* **Front-endpoort:** dit is de openbare poort die in de toepassingsgateway wordt geopend. Het verkeer komt binnen via deze poort en wordt vervolgens omgeleid naar een van de back-endservers.
* **Listener:** de listener beschikt over een front-endpoort, een protocol (Http of Https; deze instellingen zijn hoofdlettergevoelig) en de SSL-certificaatnaam (als u SSL-offloading configureert).
* **Regel:** de regel verbindt de listener met de back-endserverpool en definieert naar welke back-endserverpool het verkeer moet worden omgeleid wanneer dit bij een bepaalde listener aankomt. Momenteel wordt alleen de regel *basic* ondersteund. De regel *basic* is een vorm van round-robinbelastingverdeling.

**Aanvullende configuratieopmerkingen**

Voor het configureren van SSL-certificaten moet het protocol in **HttpListener** worden gewijzigd in *Https* (hoofdlettergevoelig). Het element **SslCertificate** wordt toegevoegd aan **HttpListener**, waarbij de waarde van de variabele moet worden geconfigureerd voor het SSL-certificaat. De front-endpoort moet worden bijgewerkt naar 443.

**Op cookies gebaseerde affiniteit inschakelen**: u kunt een toepassingsgateway zodanig configureren dat u zeker weet dat aanvragen vanuit clientsessies altijd worden omgeleid naar dezelfde virtuele machine in de webfarm. Dit wordt gedaan door het injecteren van een sessiecookie waarmee de gateway het verkeer correct kan omleiden. Als u op cookies gebaseerde affiniteit wilt inschakelen, stelt u **CookieBasedAffinity** in op *Enabled* in het element **BackendHttpSettings**.

## <a name="create-an-application-gateway"></a>Een toepassingsgateway maken

Het verschil tussen het gebruik van het klassieke Azure-implementatiemodel en Azure Resource Manager zit hem in de volgorde waarin u een toepassingsgateway maakt en in de items die u moet configureren.

Met Resource Manager worden alle componenten van een toepassingsgateway afzonderlijk geconfigureerd en vervolgens samengesteld om een toepassingsgatewayresource te maken.

Dit zijn de stappen voor het maken van een toepassingsgateway:

1. Een resourcegroep maken voor Resource Manager
2. Een virtueel netwerk, subnet en openbaar IP-adres maken voor de toepassingsgateway
3. Een configuratieobject voor de toepassingsgateway maken
4. Een toepassingsgatewayresource maken

## <a name="create-a-resource-group-for-resource-manager"></a>Een resourcegroep maken voor Resource Manager

Zorg ervoor dat u overschakelt naar de PowerShell-modus om de Azure Resource Manager-cmdlets te gebruiken. Zie [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Windows PowerShell gebruiken met Resource Manager) voor meer informatie.

### <a name="step-1"></a>Stap 1

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a>Stap 2

Controleer de abonnementen voor het account.

```powershell
Get-AzureRmSubscription
```

U wordt gevraagd om u te verifiëren met uw referenties.

### <a name="step-3"></a>Stap 3

Kies welk Azure-abonnement u wilt gebruiken.

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a>Stap 4

Maak een resourcegroep (u kunt deze stap overslaan als u een bestaande resourcegroep gebruikt).

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

Azure Resource Manager vereist dat er voor alle resourcegroepen een locatie wordt opgegeven. Deze instelling wordt gebruikt als de standaardlocatie voor resources in die resourcegroep. Zorg ervoor dat bij alle opdrachten voor het maken van een toepassingsgateway dezelfde resourcegroep wordt gebruikt.

In het bovenstaande voorbeeld is er een resourcegroep gemaakt met de naam **appgw-RG** en de locatie **VS - west**.

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a>Een virtueel netwerk en een subnet maken voor de toepassingsgateway

In het volgende voorbeeld ziet u hoe u een virtueel netwerk maakt met Resource Manager:

### <a name="step-1"></a>Stap 1

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

Hiermee wijst u het adresbereik 10.0.0.0/24 toe aan de subnetvariabele die u gaat gebruiken om een virtueel netwerk te maken.

### <a name="step-2"></a>Stap 2

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

In dit voorbeeld wordt een virtueel netwerk met de naam **appgwvnet** in de resourcegroep **appgw-rg** voor de regio VS-West is met het voorvoegsel 10.0.0.0/16 met het subnet 10.0.0.0/24.

### <a name="step-3"></a>Stap 3

```powershell
$subnet = $vnet.Subnets[0]
```

Hiermee wijst u het subnetobject toe aan de variabele $subnet voor gebruik in de volgende stappen.

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a>Een openbaar IP-adres maken voor de front-endconfiguratie

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

In dit voorbeeld wordt een openbare IP-resource **publicIP01** in de resourcegroep **appgw-rg** voor de regio VS-West.

## <a name="create-an-application-gateway-configuration-object"></a>Een configuratieobject voor de toepassingsgateway maken

### <a name="step-1"></a>Stap 1

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

In dit voorbeeld wordt een toepassingsgateway een IP-configuratie met de naam **gatewayIP01**. Wanneer de toepassingsgateway wordt geopend, wordt er een IP-adres opgehaald via het geconfigureerde subnet en wordt het netwerkverkeer omgeleid naar de IP-adressen in de back-end-IP-pool. Onthoud dat elk exemplaar één IP-adres gebruikt.

### <a name="step-2"></a>Stap 2

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221,134.170.185.50
```

Dit voorbeeld configureert de backend-IP-adresgroep met de naam **pool01** met IP-adressen **134.170.185.46**, **134.170.188.221**, **134.170.185.50**. Deze waarden zijn de IP-adressen waardoor het netwerkverkeer van het front-end-IP-eindpunt binnenkomt. Vervang de IP-adressen uit het voorbeeld hierboven door de IP-adressen van de eindpunten van uw webtoepassing.

### <a name="step-3"></a>Stap 3

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Enabled
```

Dit voorbeeld configureert u de instelling voor application gateway **poolsetting01** voor taakverdeling van netwerkverkeer in de groep back-end.

### <a name="step-4"></a>Stap 4

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 443
```

Dit voorbeeld configureert u de front-end-IP-poort met de naam **frontendport01** voor het openbare IP-eindpunt.

### <a name="step-5"></a>Stap 5

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path for certificate file> -Password "<password>"
```

Hiermee configureert u het certificaat dat wordt gebruikt voor de SSL-verbinding. Het certificaat moet de indeling .pfx hebben en het wachtwoord moet uit 4-12 tekens bestaan.

### <a name="step-6"></a>Stap 6

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip
```

In dit voorbeeld wordt de front-end-IP-configuratie met de naam **fipconfig01** en koppelt u het openbare IP-adres aan de front-end-IP-configuratie.

### <a name="step-7"></a>Stap 7

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert
```

In dit voorbeeld wordt de naam van de listener **listener01** en koppelt u de front-endpoort aan de front-end-IP-configuratie en het certificaat.

### <a name="step-8"></a>Stap 8

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

In dit voorbeeld wordt de load balancer-routeringsregel met de naam **rule01** die het gedrag van de load balancer configureert.

### <a name="step-9"></a>Stap 9

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

Hiermee configureert u de exemplaargrootte van de toepassingsgateway.

> [!NOTE]
> De standaardwaarde voor *InstanceCount* is 2 en de maximale waarde is 10. De standaardwaarde voor *GatewaySize* is Medium. U kunt kiezen tussen Standard_Small, Standard_Medium en Standard_Large.

### <a name="step-10"></a>Stap 10

```powershell
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S
```

Deze stap definieert de SSL-beleid gebruiken in de toepassingsgateway. Ga naar [SSL configureren voor versies en coderingssuites in toepassingsgateway](application-gateway-configure-ssl-policy-powershell.md) voor meer informatie.

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a>Een toepassingsgateway maken met behulp van New-AzureApplicationGateway

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SslCertificates $cert -SslPolicy $policy
```

In dit voorbeeld wordt een toepassingsgateway gemaakt met alle configuratie-items uit de bovenstaande stappen. In het voorbeeld wordt de toepassingsgateway wordt aangeroepen **appgwtest**.

## <a name="get-application-gateway-dns-name"></a>DNS-naam van toepassingsgateway verkrijgen

Wanneer de gateway is gemaakt, gaat u in de volgende stap de front-end voor communicatie configureren. Wanneer u een openbare IP gebruikt, heeft de toepassingsgateway een dynamisch toegewezen DNS-naam nodig. Dit is niet gebruiksvriendelijk. Om ervoor te zorgen dat eindgebruikers de toepassingsgateway kunnen bereiken, kan een CNAME-record worden gebruikt die verwijst naar het openbare eindpunt van de toepassingsgateway. [Een aangepaste domeinnaam configureren voor in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md). Daartoe haalt u details van de toepassingsgateway en de bijbehorende IP-/ DNS-naam op met het PublicIPAddress-element gekoppeld aan de toepassingsgateway. De DNS-naam van de toepassingsgateway moet worden gebruikt om een CNAME-record te maken die de twee webtoepassingen naar deze DNS-naam wijst. Het gebruik van A-records wordt niet aanbevolen, omdat het VIP kan veranderen wanneer de toepassingsgateway opnieuw wordt gestart.


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

Als u een toepassingsgateway wilt configureren voor gebruik met een interne load balancer, raadpleegt u [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md) (Een toepassingsgateway met een interne load balancer (ILB) maken).

Als u meer informatie wilt over de algemene opties voor load balancing, raadpleegt u:

* [Azure Load Balancer](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/)

