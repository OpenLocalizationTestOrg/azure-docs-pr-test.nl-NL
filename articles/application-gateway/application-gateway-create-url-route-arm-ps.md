---
title: Een application gateway met behulp van regels voor het doorsturen van URL | Microsoft Docs
description: Deze pagina vindt u instructies voor het maken, configureren van een toepassingsgateway met behulp van regels voor het doorsturen van URL
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: d141cfbb-320a-4fc9-9125-10001c6fa4cf
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: gwallace
ms.openlocfilehash: ba756d3262b9780c5701e69faad860ba32bba08b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-application-gateway-using-path-based-routing"></a>Een toepassingsgateway met pad gebaseerde routering maken

> [!div class="op_single_selector"]
> * [Azure Portal](application-gateway-create-url-route-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-url-route-arm-ps.md)
> * [Azure CLI 2.0](application-gateway-create-url-route-cli.md)

URL-pad gebaseerde routering, kunt u de routes op basis van het URL-pad van een Http-aanvraag koppelen. Het controleren of er een route naar een back-end-adresgroep geconfigureerd voor de URL die zijn gepresenteerd in de toepassingsgateway. Deze stuurt vervolgens het netwerkverkeer naar de gedefinieerde back-end-pool. Vaak gebruikt voor het doorsturen van op basis van een URL is voor andere typen inhoud aan andere back-endserver groepen van aanvragen verdelen over.

URL gebaseerde routering introduceert een nieuwe regel-type dat aan de toepassingsgateway. Toepassingsgateway heeft twee regeltypen: basic en PathBasedRouting. Basic regeltype biedt een round robin-service voor de back-end-adresgroepen tijdens PathBasedRouting naast round robin distributie, ook rekening wordt gehouden pad patroon van de aanvraag-URL tijdens de back-endpool te kiezen.

## <a name="scenario"></a>Scenario

In het volgende voorbeeld Application Gateway verkeer voor contoso.com bedient met twee back-endserver van toepassingen: video servergroep en image-servergroep.

Aanvragen voor http://contoso.com/image * worden doorgestuurd naar de installatiekopie servergroep (pool1) en http://contoso.com/video * worden doorgestuurd naar video servergroep (pool2). Als geen van de pad-patronen overeenkomen, kan een standaardgroep server (pool1) is geselecteerd.

![URL-route](./media/application-gateway-create-url-route-arm-ps/figure1.png)

## <a name="before-you-begin"></a>Voordat u begint

1. Installeer de nieuwste versie van de Azure PowerShell-cmdlets via het webplatforminstallatieprogramma. U kunt de nieuwste versie downloaden en installeren via het gedeelte **Windows PowerShell** op de pagina [Downloads](https://azure.microsoft.com/downloads/).
2. Maakt u een virtueel netwerk en subnet voor Application Gateway. Zorg ervoor dat er geen virtuele machines en cloudimplementaties zijn die gebruikmaken van het subnet. De toepassingsgateway moet afzonderlijk in een subnet van een virtueel netwerk staan.
3. De servers toegevoegd aan de groep back-end gebruiken van de toepassingsgateway moeten bestaan of hebben hun eindpunten gemaakt in het virtuele netwerk of een openbaar IP-/ VIP-adres toegewezen.

## <a name="what-is-required-to-create-an-application-gateway"></a>Wat is er vereist om een toepassingsgateway te maken?

* **Back-endserverpool:** de lijst met IP-adressen van de back-endservers. De IP-adressen moeten ofwel deel uitmaken van het subnet van het virtuele netwerk, ofwel openbare IP-/VIP-adressen zijn.
* **Back-endserverpoolinstellingen:** elke pool heeft instellingen, zoals voor de poort, het protocol en de op cookies gebaseerde affiniteit. Deze instellingen zijn gekoppeld aan een pool en worden toegepast op alle servers in de pool.
* **Front-endpoort:** dit is de openbare poort die in de toepassingsgateway wordt geopend. Het verkeer komt binnen via deze poort en wordt vervolgens omgeleid naar een van de back-endservers.
* **Listener:** de listener beschikt over een front-endpoort, een protocol (Http of Https; deze waarden zijn hoofdlettergevoelig) en de SSL-certificaatnaam (als u SSL-offloading configureert).
* **Regel:** de regel verbindt de listener met de back-endserverpool en definieert naar welke back-endserverpool het verkeer moet worden omgeleid wanneer dit bij een bepaalde listener aankomt.

## <a name="create-an-application-gateway"></a>Een toepassingsgateway maken

Het verschil tussen het gebruik van Azure Classic en Azure Resource Manager zit hem in de volgorde waarin u de toepassingsgateway maakt en in de items die u moet configureren.

Met Resource Manager worden alle items waaruit een toepassingsgateway bestaat, afzonderlijk geconfigureerd en vervolgens samengesteld om de toepassingsgatewayresource te maken.

Dit zijn de stappen voor het maken van een toepassingsgateway:

1. Maak een resourcegroep voor Resource Manager.
2. Maak een virtueel netwerk, subnet en openbaar IP-adres voor de toepassingsgateway.
3. Maak een configuratieobject voor de toepassingsgateway.
4. Maak een toepassingsgatewayresource.

## <a name="create-a-resource-group-for-resource-manager"></a>Een resourcegroep maken voor Resource Manager

Zorg ervoor dat u de nieuwste versie van Azure PowerShell gebruikt. Zie [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Windows PowerShell gebruiken met Resource Manager) voor meer informatie.

### <a name="step-1"></a>Stap 1

Meld u aan bij Azure.

```powershell
Login-AzureRmAccount
```

U wordt gevraagd om u te verifiëren met uw referenties.<BR>

### <a name="step-2"></a>Stap 2

Controleer de abonnementen voor het account.

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a>Stap 3

Kies welk Azure-abonnement u wilt gebruiken. <BR>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a>Stap 4

Maak een resourcegroep (u kunt deze stap overslaan als u een bestaande resourcegroep gebruikt).

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US"
```

U kunt ook ook labels voor een resourcegroep voor de toepassingsgateway maken:

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway URL routing"} 
```

Azure Resource Manager vereist dat er voor alle resourcegroepen een locatie wordt opgegeven. Deze resourcegroep wordt gebruikt als de standaardlocatie voor resources in die resourcegroep. Zorg ervoor dat alle opdrachten voor het maken van een toepassingsgateway dezelfde resourcegroep gebruikt.

In het bovenstaande voorbeeld is er een resourcegroep gemaakt met de naam appgw-RG en de locatie VS - west.

> [!NOTE]
> Als u voor uw toepassingsgateway een aangepaste test moet configureren, raadpleegt u [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md) (Met PowerShell een toepassingsgateway maken met aangepaste tests). Bekijk [Custom probes and health monitoring](application-gateway-probe-overview.md) (Aangepaste tests en statusbewaking) voor meer informatie.
> 
> 

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a>Een virtueel netwerk en een subnet maken voor de toepassingsgateway

In het volgende voorbeeld ziet u hoe u een virtueel netwerk maakt met Resource Manager. In dit voorbeeld wordt er een VNET gemaakt voor Application Gateway. Toepassingsgateway vereist een eigen subnet, om deze reden het subnet dat is gemaakt voor de toepassingsgateway kleiner dan de VNET-adresruimte is. Hierdoor kunnen andere resources, inclusief maar niet beperkt tot webservers moet worden geconfigureerd in hetzelfde VNET.

### <a name="step-1"></a>Stap 1

Wijs het adresbereik 10.0.0.0/24 toe aan de subnetvariabele die u gaat gebruiken om een virtueel netwerk te maken.  Hiermee maakt u het configuratieobject subnet voor de toepassingsgateway, die wordt gebruikt in het volgende voorbeeld.

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

### <a name="step-2"></a>Stap 2

Maak een virtueel netwerk met de naam **appgwvnet** in de resourcegroep **appgw-rg**. Doe dit voor de regio VS - west. Gebruik het voorvoegsel 10.0.0.0/16 met het subnet 10.0.0.0/24. Hiermee wordt de configuratie van het VNET met één subnet voor de toepassingsgateway zich bevinden.

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

### <a name="step-3"></a>Stap 3

Toewijzen van de variabele subnet voor de volgende stappen, dit wordt doorgegeven aan de `New-AzureRMApplicationGateway` cmdlet in een toekomstige stap.

```powershell
$subnet=$vnet.Subnets[0]
```

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a>Een openbaar IP-adres maken voor de front-endconfiguratie

Maak de openbare IP-resource **publicIP01** in de resourcegroep **appgw-rg** voor de regio VS - west. Voor Application Gateway kan een openbaar IP-adres, een intern IP-adres of beide worden gebruikt om aanvragen voor de taakverdeling te ontvangen.  In dit voorbeeld wordt er alleen een openbaar IP-adres gebruikt. In het volgende voorbeeld is er geen DNS-naam geconfigureerd voor het maken van het openbare IP-adres.  Application Gateway biedt geen ondersteuning voor aangepaste DNS-namen voor openbare IP-adressen.  Als er een aangepaste naam is vereist voor het openbare eindpunt, moet er een CNAME-record worden gemaakt die verwijst naar de automatisch gegenereerde DNS-naam voor het openbare IP-adres.

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

Er wordt een IP-adres toegewezen aan de toepassingsgateway wanneer de service wordt gestart.

## <a name="create-application-gateway-configuration"></a>De gatewayconfiguratie toepassing maken

Alle configuratie-items moeten zijn ingesteld voordat u de toepassingsgateway maakt. Volg de onderstaande stappen om de configuratie-items te maken die nodig zijn voor een toepassingsgatewayresource.

### <a name="step-1"></a>Stap 1

Maak voor de toepassingsgateway een IP-configuratie en geef deze de naam **gatewayIP01**. Wanneer de toepassingsgateway wordt geopend, wordt er een IP-adres opgehaald via het geconfigureerde subnet en wordt het netwerkverkeer omgeleid naar de IP-adressen in de back-end-IP-pool. Onthoud dat elk exemplaar één IP-adres gebruikt.

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

### <a name="step-2"></a>Stap 2

Configureer de backend-IP-adresgroep met de naam **pool01** en **pool2** met IP-adressen voor **pool1** en **pool2**. Deze IP-adressen zijn de IP-adressen van de resources waarop de webtoepassing wordt gehost die moet worden beveiligd door de toepassingsgateway. Aan de hand van basistests of aangepaste tests wordt gecontroleerd of alle back-endpoolleden in orde zijn.  Vervolgens wordt verkeer hiernaartoe doorgestuurd wanneer er aanvragen binnenkomen in de toepassingsgateway. Back-endpools kunnen worden gebruikt door meerdere regels in de toepassingsgateway. Dit betekent dat een back-endpool kan worden gebruikt voor meerdere webtoepassingen die zich op dezelfde host bevinden.

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 134.170.186.47, 134.170.189.222, 134.170.186.51
```

In dit voorbeeld zijn er twee back-endpools voor het verzenden van netwerkverkeer op basis van het URL-pad. Een pool ontvangt verkeer vanuit het URL-pad '/video' en andere pool ontvangt verkeer vanuit het pad '/image'. Vervang de bovenstaande IP-adressen door de IP-adreseindpunten van uw eigen toepassing. 

### <a name="step-3"></a>Stap 3

Configureren van de instelling voor application gateway **poolsetting01** en **poolsetting02** voor het netwerkverkeer van taakverdeling in de groep back-end. In dit voorbeeld configureert u de instellingen van de andere back-end-adresgroep voor de back-end-adresgroepen. Elke back-endpool kan een eigen instelling van de back-endpool hebben.  Back-end-HTTP-instellingen worden gebruikt door regels om verkeer te verzenden naar de juiste back-endpoolleden. Hiermee bepaalt u het protocol en de poort die wordt gebruikt bij het verzenden van verkeer op de leden van de groep back-end. Sessies op basis van cookies worden ook bepaald door de back-end-HTTP-instellingen.  Als sessieaffiniteit op basis van cookies is ingeschakeld, wordt verkeer verzonden naar dezelfde back-end als bij de vorige aanvragen voor elk pakket.

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120

$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a>Stap 4

Configureer het front-end-IP-adres met openbaar IP-eindpunt. Het configuratie-object front-end-IP-adres wordt gebruikt door een listener om het uitgaande IP-adres te koppelen aan de listener.

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a>Stap 5

Configureer de front-endpoort voor een toepassingsgateway. Het configuratieobject front-endpoort wordt gebruikt door een listener om te definiëren via welke poort Application Gateway naar verkeer op de listener luistert.

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 80
```

### <a name="step-6"></a>Stap 6

Configureer de listener. In deze stap wordt de listener voor het openbare IP-adres en de poort voor het ontvangen van binnenkomend netwerkverkeer geconfigureerd. Het volgende voorbeeld wordt de eerder geconfigureerde front-end-IP-configuratie, front-endpoort configuratie en een protocol (http of https) en configureert de listener. In dit voorbeeld luistert de listener luistert naar HTTP-verkeer op poort 80 voor het openbare IP-adres dat eerder is gemaakt.

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Http -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01
```

### <a name="step-7"></a>Stap 7

URL-paden regel voor de back-end-adresgroepen configureren. Deze stap configureert u het relatieve pad gebruikt door de toepassingsgateway en definieert de toewijzing tussen het URL-pad en de back-end-pool die is toegewezen aan de binnenkomend verkeer verwerken.

> [!IMPORTANT]
> Elk pad moet beginnen met / en de enige plaats waar een '\*' is toegestaan, wordt aan het einde. Voorbeelden van geldige zijn/xyz, /xyz* of xyz / *. De tekenreeks die is ingevoerd in het pad matcher geen tekst bevatten na de eerste '? ' of '#' en deze tekens zijn niet toegestaan. 

Het volgende voorbeeld maakt u twee regels: één voor '/ afbeelding /' pad routeren van verkeer naar de back-end 'pool1' en een andere voor '/ video /' pad routeren van verkeer naar de back-end 'pool2'. Deze regels ervoor zorgen dat verkeer voor elke set van URL's wordt doorgestuurd naar de back-end. Bijvoorbeeld: http://contoso.com/image/figure1.jpg gaat naar pool1 en http://contoso.com/video/example.mp4 gaat dan naar pool2.

```powershell
$imagePathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule1" -Paths "/image/*" -BackendAddressPool $pool1 -BackendHttpSettings $poolSetting01

$videoPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule2" -Paths "/video/*" -BackendAddressPool $pool2 -BackendHttpSettings $poolSetting02
```

Als het pad komt niet met de vooraf gedefinieerde padregels overeen, configureert de regel pad kaart configuratie ook een standaard back-end-adresgroep. Bijvoorbeeld: http://contoso.com/shoppingcart/test.html gaat u naar pool1 zoals deze is gedefinieerd als de standaardgroep voor niet-overeenkomende verkeer.

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $videoPathRule, $imagePathRule -DefaultBackendAddressPool $pool1 -DefaultBackendHttpSettings $poolSetting02
```

### <a name="step-8"></a>Stap 8

De instelling van een regel maken. Deze stap configureert u de toepassingsgateway als URL-pad gebaseerde routering wilt gebruiken. De `$urlPathMap` variabele gedefinieerd in de vorige stap nu gebruikt voor het maken van de regel op basis van het pad. In deze stap wordt de regel koppelen aan een listener en de toewijzing van de url-pad eerder hebt gemaakt.

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-9"></a>Stap 9

Configureer het aantal exemplaren en de grootte voor de toepassingsgateway.

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Small" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a>Toepassingsgateway maken

Een toepassingsgateway maken met alle configuratie-objecten uit de bovenstaande stappen.

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku
```

## <a name="get-application-gateway-dns-name"></a>DNS-naam van toepassingsgateway verkrijgen

Wanneer de gateway is gemaakt, gaat u in de volgende stap de front-end voor communicatie configureren. Wanneer u een openbare IP gebruikt, heeft de toepassingsgateway een dynamisch toegewezen DNS-naam nodig. Dit is niet gebruiksvriendelijk. Om ervoor te zorgen dat eindgebruikers de toepassingsgateway kunnen bereiken, kan een CNAME-record worden gebruikt die verwijst naar het openbare eindpunt van de toepassingsgateway. [Een aangepaste domeinnaam configureren voor in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md). Voor het configureren van de frontend-IP-CNAME-record ophalen van gegevens van de toepassingsgateway en de bijbehorende IP-en DNS-naam met behulp van de PublicIPAddress-element dat is gekoppeld aan de toepassingsgateway. De toepassingsgateway DNS-naam moet worden gebruikt voor het maken van een CNAME-record. Het gebruik van A-records wordt niet aanbevolen, omdat het VIP kan veranderen wanneer de toepassingsgateway opnieuw wordt gestart.

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

Als u weten van Secure Sockets Layer (SSL)-offload wilt, Zie [een toepassingsgateway voor SSL-offload configureren](application-gateway-ssl-arm.md).

