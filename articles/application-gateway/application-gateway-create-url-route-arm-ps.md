---
title: een toepassingsgateway met URL-routering regels aaaCreate | Microsoft Docs
description: Deze pagina vindt u instructies toocreate, een Azure-toepassingsgateway met behulp van regels voor URL-routering configureren
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
ms.openlocfilehash: 54fcccc39e48a933576968ce3d8160518c0d0b7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-using-path-based-routing"></a>Een toepassingsgateway met pad gebaseerde routering maken

> [!div class="op_single_selector"]
> * [Azure Portal](application-gateway-create-url-route-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-url-route-arm-ps.md)
> * [Azure CLI 2.0](application-gateway-create-url-route-cli.md)

URL-pad gebaseerde routering, kunt u tooassociate routes op basis van Hallo URL-pad van een Http-aanvraag. Het controleren of er een route tooa back-end-adresgroep geconfigureerd voor Hallo-URL die zijn gepresenteerd in Hallo Application Gateway. Vervolgens stuurt Hallo netwerkverkeer toohello gedefinieerd back-end-pool. Vaak gebruikt voor het doorsturen van op basis van een URL is tooload van aanvragen verdelen over voor andere typen inhoud toodifferent back-end-servergroepen.

URL gebaseerde routering introduceert een nieuwe regel type tooapplication gateway. Toepassingsgateway heeft twee regeltypen: basic en PathBasedRouting. Basic regeltype biedt round robin-service voor Hallo back-end opslaggroepen tijdens PathBasedRouting bovendien tooround robin distributie, ook rekening wordt gehouden pad patroon van de aanvraag-URL Hallo daarbij Hallo back-endpool.

## <a name="scenario"></a>Scenario

In de Hallo voorbeeld te volgen, Application Gateway verkeer voor contoso.com bedient met twee back-endserver van toepassingen: video servergroep en image-servergroep.

Aanvragen voor http://contoso.com/image * worden gerouteerd servergroep tooimage (pool1) en http://contoso.com/video * worden gerouteerd servergroep toovideo (pool2). Als geen van Hallo pad patronen overeenkomen, kan een standaardgroep server (pool1) is geselecteerd.

![URL-route](./media/application-gateway-create-url-route-arm-ps/figure1.png)

## <a name="before-you-begin"></a>Voordat u begint

1. Hallo meest recente versie van hello Azure PowerShell-cmdlets installeren met behulp van Hallo Web Platform Installer. U kunt downloaden en installeren van de meest recente versie Hallo van Hallo **Windows PowerShell** sectie Hallo [pagina Downloads](https://azure.microsoft.com/downloads/).
2. Maakt u een virtueel netwerk en subnet voor Application Gateway. Zorg ervoor dat er geen virtuele machines en cloudimplementaties die van Hallo subnet gebruikmaken zijn. Hallo toepassingsgateway moet afzonderlijk in een virtueel netwerksubnet.
3. Hallo-servers toegevoegd toohello back-end-pool toouse Hallo application gateway moet al bestaan of hebben hun eindpunten gemaakt in het virtuele netwerk hello of een openbaar IP-/ VIP-adres toegewezen.

## <a name="what-is-required-toocreate-an-application-gateway"></a>Wat is vereist toocreate een application gateway?

* **Back-endserverpool:** Hallo lijst met IP-adressen van Hallo back-endservers. Hallo IP-adressen moeten ofwel deel uitmaken toohello virtueel netwerksubnet ofwel moeten een openbare IP-/ VIP.
* **Back-endserverpoolinstellingen:** elke pool heeft instellingen, zoals voor de poort, het protocol en de op cookies gebaseerde affiniteit. Deze instellingen zijn gebonden tooa servergroep en toegepaste tooall servers binnen de pool Hallo zijn.
* **Front-endpoort:** deze is Hallo openbare poort die in Hallo toepassingsgateway wordt geopend. Verkeer komt binnen via deze poort en vervolgens wordt omgeleid tooone van Hallo back-endservers.
* **Listener:** Hallo listener beschikt over een front-endpoort, een protocol (Http of Https; deze waarden zijn hoofdlettergevoelig), en Hallo SSL-certificaatnaam (als u SSL-offloading configureert).
* **Regel:** Hallo regel verbindt Hallo listener, Hallo back-endserverpool en definieert naar welke back-endserver groep Hallo verkeer moet gerichte toowhen dit bij een bepaalde listener aankomt.

## <a name="create-an-application-gateway"></a>Een toepassingsgateway maken

Hallo verschil tussen het gebruik van Azure Classic en Azure Resource Manager is Hallo volgorde waarin u de toepassingsgateway Hallo en Hallo-items die u toobe geconfigureerd moet maken.

Met Resource Manager worden alle items waaruit een toepassingsgateway worden afzonderlijk geconfigureerd en deze vervolgens samen toocreate hello toepassingsgatewayresource.

Hier volgen Hallo stappen nodig toocreate een toepassingsgateway zijn:

1. Maak een resourcegroep voor Resource Manager.
2. Maak een virtueel netwerk, subnet en openbaar IP-adres voor de toepassingsgateway Hallo.
3. Maak een configuratieobject voor de toepassingsgateway.
4. Maak een toepassingsgatewayresource.

## <a name="create-a-resource-group-for-resource-manager"></a>Een resourcegroep maken voor Resource Manager

Zorg ervoor dat u van Hallo meest recente versie van Azure PowerShell gebruikmaakt. Zie [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Windows PowerShell gebruiken met Resource Manager) voor meer informatie.

### <a name="step-1"></a>Stap 1

Meld u bij tooAzure

```powershell
Login-AzureRmAccount
```

Vraag tooauthenticate bent u met uw referenties.<BR>

### <a name="step-2"></a>Stap 2

Controleer de abonnementen Hallo voor Hallo-account.

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a>Stap 3

Kies welke van uw Azure-abonnementen toouse. <BR>

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

Azure Resource Manager vereist dat er voor alle resourcegroepen een locatie wordt opgegeven. Deze resourcegroep wordt gebruikt als Hallo standaardlocatie voor resources in die resourcegroep. Zorg ervoor dat alle opdrachten toocreate een application gateway gebruik Hallo dezelfde resourcegroep.

Wij gemaakt een resourcegroep met de naam 'appgw-RG' en de locatie 'West ons' hello bovenstaande voorbeeld.

> [!NOTE]
> Als u voor uw toepassingsgateway een aangepaste test tooconfigure nodig hebt, raadpleegt u [met PowerShell een toepassingsgateway maken met aangepaste tests](application-gateway-create-probe-ps.md). Bekijk [Custom probes and health monitoring](application-gateway-probe-overview.md) (Aangepaste tests en statusbewaking) voor meer informatie.
> 
> 

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a>Een virtueel netwerk en een subnet voor de toepassingsgateway Hallo maken

Hallo volgende voorbeeld wordt getoond hoe toocreate een virtueel netwerk met Resource Manager. In dit voorbeeld maakt een VNET voor Hallo Application Gateway. Toepassingsgateway vereist een eigen subnet, om deze reden Hallo-subnet voor Application Gateway Hallo gemaakt kleiner dan VNET-adresruimte Hallo is. Hiermee kunt u andere resources, met inbegrip van maar niet beperkt tooweb servers toobe dat is geconfigureerd in Hallo hetzelfde VNET.

### <a name="step-1"></a>Stap 1

Hallo adres adresbereik 10.0.0.0/24 toohello subnet variabele toobe gebruikt toocreate een virtueel netwerk toewijzen.  Hiermee maakt u Hallo subnet configuration-object voor Application Gateway die wordt gebruikt in het volgende voorbeeld Hallo Hallo.

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

### <a name="step-2"></a>Stap 2

Maak een virtueel netwerk met de naam **appgwvnet** in de resourcegroep **appgw-rg** voor de regio VS-West Hallo met Hallo voorvoegsel 10.0.0.0/16 met het subnet 10.0.0.0/24. Deze configuratie Hallo Hallo VNET met één subnet voor Hallo Application Gateway tooreside is voltooid.

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

### <a name="step-3"></a>Stap 3

Toewijzen Hallo subnetvariabele toe voor Hallo Vervolgstappen, dit wordt doorgegeven toohello `New-AzureRMApplicationGateway` cmdlet in een toekomstige stap.

```powershell
$subnet=$vnet.Subnets[0]
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>Een openbaar IP-adres voor de front-endconfiguratie Hallo maken

Maak een openbare IP-resource **publicIP01** in de resourcegroep **appgw-rg** voor de regio VS-West Hallo. Toepassingsgateway kunt een openbaar IP-adres, interne IP-adres of beide aanvragen tooreceive gebruiken voor taakverdeling.  In dit voorbeeld wordt er alleen een openbaar IP-adres gebruikt. Hallo voorbeeld te volgen, wordt geen DNS-naam voor het maken van Hallo openbare IP-adres geconfigureerd.  Application Gateway biedt geen ondersteuning voor aangepaste DNS-namen voor openbare IP-adressen.  Als u een aangepaste naam is vereist voor Hallo openbaar eindpunt, moet een CNAME-record toopoint toohello automatisch gegenereerd DNS-naam voor het openbare IP-adres Hallo worden gemaakt.

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

Een IP-adres is toohello toepassingsgateway toegewezen wanneer Hallo-service wordt gestart.

## <a name="create-application-gateway-configuration"></a>De gatewayconfiguratie toepassing maken

Alle configuratie-items moeten worden ingesteld voordat u de toepassingsgateway Hallo maakt. Hallo volgt Hallo configuratie-items maken die nodig zijn voor een toepassingsgatewayresource.

### <a name="step-1"></a>Stap 1

Maak voor de toepassingsgateway een IP-configuratie en geef deze de naam **gatewayIP01**. Wanneer de toepassingsgateway wordt geopend, een IP-adres van de geconfigureerde Hallo subnet opneemt en routeren netwerkverkeer toohello IP-adressen in Hallo backend-IP-adresgroep. Onthoud dat elk exemplaar één IP-adres gebruikt.

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

### <a name="step-2"></a>Stap 2

Configureer Hallo backend-IP-adresgroep met de naam **pool01** en **pool2** met IP-adressen voor **pool1** en **pool2**. Deze IP-adressen zijn IP-adressen Hallo Hallo-resources die als Hallo web application toobe beveiligd door Hallo toepassingsgateway host. Deze back-end-groepsleden zijn alle gevalideerde toobe orde door de tests, ongeacht of deze eenvoudige tests of aangepaste tests.  Verkeer wordt vervolgens omgeleid toothem wanneer aanvragen Hallo toepassingsgateway binnenkomen. Back-endpools kunnen worden gebruikt door meerdere regels, binnen de toepassingsgateway hello, wat betekent dat één back endadresgroep kan worden gebruikt voor meerdere webtoepassingen die zich op Hallo dezelfde bevinden host.

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 134.170.186.47, 134.170.189.222, 134.170.186.51
```

In dit voorbeeld zijn er twee back-end-adresgroepen tooroute-netwerkverkeer op basis van Hallo URL-pad. Een pool ontvangt verkeer vanuit het URL-pad '/video' en andere pool ontvangt verkeer vanuit het pad '/image'. Vervang Hallo IP-adressen tooadd voorafgaand aan uw eigen toepassing IP-adres-eindpunten. 

### <a name="step-3"></a>Stap 3

Configureren van de instelling voor application gateway **poolsetting01** en **poolsetting02** voor Hallo taakverdeling netwerkverkeer in Hallo back-endpool. In dit voorbeeld kunt u instellingen van de andere back-end-adresgroep voor Hallo back-end-adresgroepen configureren. Elke back-endpool kan een eigen instelling van de back-endpool hebben.  Back-end-HTTP-instellingen worden gebruikt door regels tooroute verkeer toohello juiste back-end-groepsleden. Hiermee bepaalt u het Hallo-protocol en poort die wordt gebruikt bij het verzenden van verkeer toohello back-end-groepsleden. Op basis van het cookie sessies worden ook bepaald door Hallo back-end-HTTP-instellingen.  Bij inschakeling sessie cookies gebaseerde affiniteit verkeer toohello verzendt dezelfde back-end als de vorige aanvragen voor elk pakket.

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120

$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a>Stap 4

Hallo front-end-IP-met openbare IP-eindpunt configureren. Hallo front-end-IP-configuratie van object wordt gebruikt door een listener toorelate Hallo passieve internetgerichte IP-adres met Hallo listener.

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a>Stap 5

Hallo front-endpoort voor een toepassingsgateway configureren. Hallo front-endpoort configuration-object wordt gebruikt door een listener toodefine wat Hallo Application Gateway luistert naar verkeer op Hallo listener-poort.

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 80
```

### <a name="step-6"></a>Stap 6

Hallo-listener configureren. Deze stap configureert u Hallo-listener voor Hallo openbaar IP-adres en poort gebruikt tooreceive binnenkomend netwerkverkeer. Hallo volgt duurt Hallo eerder geconfigureerde front-end-IP-configuratie, front-endpoort configuratie en een protocol (http of https) en Hallo listener configureert. Hallo-listener luistert in dit voorbeeld tooHTTP verkeer op poort 80 voor het openbare IP-adres hello, dat eerder is gemaakt.

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Http -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01
```

### <a name="step-7"></a>Stap 7

URL-regel paden voor back-end-adresgroepen Hallo configureren. Deze stap Hallo relatief pad gebruikt door de toepassingsgateway configureert en definieert Hallo toewijzing tussen Hallo URL-pad en Hallo back-end-pool toohandle Hallo binnenkomend verkeer is toegewezen.

> [!IMPORTANT]
> Elk pad moet beginnen met / en Hallo enige plaats waar een '\*' is toegestaan, Hallo einde. Voorbeelden van geldige zijn/xyz, /xyz* of xyz / *. Hallo tekenreeks ingevoerd toohello pad matcher heeft geen tekst bevatten na Hallo eerst '? ' of '#' en deze tekens zijn niet toegestaan. 

Hallo volgende voorbeeld maakt u twee regels: één voor het '/ afbeelding /' pad routering verkeer tooback-end 'pool1' en een andere voor '/ video /' pad routering verkeer tooback-end 'pool2'. Deze regels ervoor dat verkeer voor elke set van URL's gerouteerde toohello back-end. Bijvoorbeeld: http://contoso.com/image/figure1.jpg gaat toopool1 en http://contoso.com/video/example.mp4 toopool2 gaat.

```powershell
$imagePathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule1" -Paths "/image/*" -BackendAddressPool $pool1 -BackendHttpSettings $poolSetting01

$videoPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule2" -Paths "/video/*" -BackendAddressPool $pool2 -BackendHttpSettings $poolSetting02
```

Als het pad Hallo komt niet overeen met de vooraf gedefinieerde padregels hello, configureert pad Hallo-kaart regelconfiguratie ook een standaard back-end-adresgroep. Http://contoso.com/shoppingcart/test.html geldt bijvoorbeeld toopool1 zoals deze is gedefinieerd als de standaardgroep Hallo voor niet-overeenkomende verkeer.

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $videoPathRule, $imagePathRule -DefaultBackendAddressPool $pool1 -DefaultBackendHttpSettings $poolSetting02
```

### <a name="step-8"></a>Stap 8

De instelling van een regel maken. Deze stap configureert u Hallo application gateway toouse URL-pad gebaseerde routering. Hallo `$urlPathMap` variabele gedefinieerd in Hallo eerdere stap is nu gebruikte toocreate Hallo pad op basis van een regel. In deze stap koppelen we Hallo regel met een listener en Hallo url-padtoewijzing eerder hebt gemaakt.

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-9"></a>Stap 9

Hallo aantal exemplaren en de grootte voor de toepassingsgateway Hallo configureren.

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Small" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a>Toepassingsgateway maken

Een toepassingsgateway met alle configuratie-objecten uit de vorige stappen Hallo maken.

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku
```

## <a name="get-application-gateway-dns-name"></a>DNS-naam van toepassingsgateway verkrijgen

Zodra Hallo gateway is gemaakt, is de volgende stap Hallo tooconfigure Hallo front-end voor communicatie. Wanneer u een openbare IP gebruikt, heeft de toepassingsgateway een dynamisch toegewezen DNS-naam nodig. Dit is niet gebruiksvriendelijk. eindgebruikers tooensure kunt Hallo toepassingsgateway bereikt, een CNAME-record kan gebruikte toopoint toohello openbaar eindpunt van de toepassingsgateway Hallo. [Een aangepaste domeinnaam configureren voor in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md). tooconfigure hello frontend IP CNAME-record, ophalen van gegevens van de toepassingsgateway Hallo en de bijbehorende IP-en DNS-naam op Hallo PublicIPAddress element gekoppelde toohello application gateway met. Hallo application gateway DNS-naam moet gebruikte toocreate een CNAME-record. Hallo-gebruik van A-records wordt niet aanbevolen omdat Hallo VIP bij opnieuw opstarten van toepassingsgateway mag wijzigen.

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

Als u toolearn Secure Sockets Layer (SSL)-offload wilt, Zie [een toepassingsgateway voor SSL-offload configureren](application-gateway-ssl-arm.md).

