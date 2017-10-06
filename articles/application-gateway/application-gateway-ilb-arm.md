---
title: Azure Application Gateway met interne Load Balancer - PowerShell aaaUsing | Microsoft Docs
description: Deze pagina vindt u instructies toocreate, configureren, starten en verwijderen van een toepassingsgateway met interne load balancer (ILB) voor Azure Resource Manager
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 75cfd5a2-e378-4365-99ee-a2b2abda2e0d
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: dd0d7e954b1fa219ae6ebe42cb4b479dbcf08653
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb-by-using-azure-resource-manager"></a>Een toepassingsgateway met een interne load balancer (ILB) maken met behulp van Azure Resource Manager

> [!div class="op_single_selector"]
> * [Azure Classic PowerShell](application-gateway-ilb.md)
> * [Azure Resource Manager PowerShell](application-gateway-ilb-arm.md)

Azure Application Gateway kan worden geconfigureerd met een internetgerichte VIP of met een intern eindpunt dat geen zichtbare toohello Internet, ook wel bekend als een interne load balancer (ILB)-eindpunt. Hallo-gateway configureren met een ILB is nuttig voor interne line-of-business-toepassingen die niet blootgestelde toohello Internet. Het is ook handig voor services en lagen gebruikt in een toepassing met meerdere lagen die zich bevinden in een beveiligingsgrens die geen zichtbare toohello Internet maar er wel round robin laden distributie, sessiepersistentie of beëindiging van Secure Sockets Layer (SSL).

Dit artikel begeleidt u bij Hallo stappen tooconfigure een toepassingsgateway met een ILB.

## <a name="before-you-begin"></a>Voordat u begint

1. Hallo meest recente versie van hello Azure PowerShell-cmdlets installeren met behulp van Hallo Web Platform Installer. U kunt downloaden en installeren van de meest recente versie Hallo van Hallo **Windows PowerShell** sectie Hallo [pagina Downloads](https://azure.microsoft.com/downloads/).
2. U maakt een virtueel netwerk en een subnet voor de toepassingsgateway. Zorg ervoor dat er geen virtuele machines en cloudimplementaties die van Hallo subnet gebruikmaken zijn. De toepassingsgateway moet afzonderlijk in een subnet van een virtueel netwerk staan.
3. Hallo-servers dat u toouse Hallo toepassingsgateway configureert moeten bestaan of hun eindpunten in het virtuele netwerk hello of een openbaar IP-/ VIP-adres hebben.

## <a name="what-is-required-toocreate-an-application-gateway"></a>Wat is vereist toocreate een application gateway?

* **Back-endserverpool:** Hallo lijst met IP-adressen van Hallo back-endservers. Hallo IP-adressen moeten ofwel deel uitmaken toohello virtueel netwerk, maar in een ander subnet voor de toepassingsgateway hello of een openbare IP-/ VIP moet zijn.
* **Back-endserverpoolinstellingen:** elke pool heeft instellingen, zoals voor de poort, het protocol en de op cookies gebaseerde affiniteit. Deze instellingen zijn gebonden tooa servergroep en toegepaste tooall servers binnen de pool Hallo zijn.
* **Front-endpoort:** deze is Hallo openbare poort die in Hallo toepassingsgateway wordt geopend. Verkeer komt binnen via deze poort en vervolgens wordt omgeleid tooone van Hallo back-endservers.
* **Listener:** Hallo listener beschikt over een front-endpoort, een protocol (Http of Https; deze zijn hoofdlettergevoelig), en Hallo SSL-certificaatnaam (als u SSL-offloading configureert).
* **Regel:** Hallo regel verbindt Hallo listener Hallo back-endserverpool en definieert welk verkeer van back-endserver groep Hallo moet gerichte toowhen dit bij een bepaalde listener aankomt. Op dit moment alleen Hallo *basic* regel wordt ondersteund. Hallo *basic* regel is round-robinbelastingverdeling.

## <a name="create-an-application-gateway"></a>Een toepassingsgateway maken

Hallo verschil tussen het gebruik van Azure Classic en Azure Resource Manager is Hallo volgorde waarin u de toepassingsgateway Hallo en Hallo-items die u toobe geconfigureerd moet maken.
Met Resource Manager worden alle items waaruit een toepassingsgateway afzonderlijk geconfigureerd en deze vervolgens samen toocreate hello toepassingsgatewayresource.

Hier volgen Hallo stappen nodig toocreate een toepassingsgateway zijn:

1. Een resourcegroep maken voor Resource Manager
2. Een virtueel netwerk en een subnet voor de toepassingsgateway Hallo maken
3. Een configuratieobject voor de toepassingsgateway maken
4. Een toepassingsgatewayresource maken

## <a name="create-a-resource-group-for-resource-manager"></a>Een resourcegroep maken voor Resource Manager

Zorg ervoor dat u overschakelt naar PowerShell modus toouse hello Azure Resource Manager-cmdlets. Zie [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Windows PowerShell gebruiken met Resource Manager) voor meer informatie.

### <a name="step-1"></a>Stap 1

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a>Stap 2

Controleer de abonnementen Hallo voor Hallo-account.

```powershell
Get-AzureRmSubscription
```

Vraag tooauthenticate bent u met uw referenties.

### <a name="step-3"></a>Stap 3

Kies welke van uw Azure-abonnementen toouse.

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a>Stap 4

Maak een nieuwe resourcegroep (u kunt deze stap overslaan als u een bestaande resourcegroep gebruikt).

```powershell
New-AzureRmResourceGroup -Name appgw-rg -location "West US"
```

Azure Resource Manager vereist dat er voor alle resourcegroepen een locatie wordt opgegeven. Dit wordt gebruikt als Hallo standaardlocatie voor resources in die resourcegroep. Zorg ervoor dat alle opdrachten toocreate maakt gebruik van een toepassingsgateway Hallo dezelfde resourcegroep.

In Hallo voorgaande voorbeeld, wij een resourcegroep 'Appgw-rg' en de locatie 'VS-West' genoemd.

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a>Een virtueel netwerk en een subnet voor de toepassingsgateway Hallo maken

Hallo volgende voorbeeld wordt getoond hoe toocreate een virtueel netwerk met Resource Manager:

### <a name="step-1"></a>Stap 1

```powershell
$subnetconfig = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

Deze stap wijst Hallo adres adresbereik 10.0.0.0/24 tooa subnet variabele toobe gebruikt toocreate een virtueel netwerk.

### <a name="step-2"></a>Stap 2

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnetconfig
```

Deze stap maakt een virtueel netwerk met de naam 'appgwvnet' in de resourcegroep 'appgw-rg' voor de regio VS-West Hallo met Hallo voorvoegsel 10.0.0.0/16 met het subnet 10.0.0.0/24.

### <a name="step-3"></a>Stap 3

```powershell
$subnet = $vnet.subnets[0]
```

Deze stap wijst Hallo subnet object toovariable $subnet voor de volgende stappen Hallo.

## <a name="create-an-application-gateway-configuration-object"></a>Een configuratieobject voor de toepassingsgateway maken

### <a name="step-1"></a>Stap 1

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

Deze stap maakt toepassingsgateway een IP-configuratie met de naam 'gatewayIP01'. Wanneer de toepassingsgateway wordt geopend, een IP-adres van de geconfigureerde Hallo subnet opneemt en routeren netwerkverkeer toohello IP-adressen in Hallo backend-IP-adresgroep. Onthoud dat elk exemplaar één IP-adres gebruikt.

### <a name="step-2"></a>Stap 2

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.1.1.8,10.1.1.9,10.1.1.10
```

Deze stap configureert u Hallo backend-IP-adresgroep met de naam 'pool01' met IP-adressen '10.1.1.8, 10.1.1.9, 10.1.1.10'. Hallo IP-adressen die Hallo netwerkverkeer ontvangen dat afkomstig van de front-end-IP-eindpunt Hallo is zijn. U vervangen Hallo IP-adressen tooadd voorafgaand aan uw eigen toepassing IP-adreseindpunten.

### <a name="step-3"></a>Stap 3

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

Deze stap configureert application gateway-instelling 'poolsetting01' voor Hallo load balanced netwerkverkeer op Hallo back-end-pool.

### <a name="step-4"></a>Stap 4

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 80
```

Deze stap configureert u Hallo front-end-IP-poort is met de naam 'frontendport01' hello ILB.

### <a name="step-5"></a>Stap 5

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -Subnet $subnet
```

Deze stap Hallo front-end-IP-configuratie met de naam 'fipconfig01' maakt en koppelt u deze aan een particuliere IP-adres van de huidige virtuele netwerksubnet Hallo.

### <a name="step-6"></a>Stap 6

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp
```

Deze stap Hallo listener met de naam 'listener01' maakt en koppelt u Hallo front-endpoort toohello front-end-IP-configuratie.

### <a name="step-7"></a>Stap 7

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

Deze stap maakt Hallo load balancer-routeringsregel genaamd 'rule01' hello load balancer-gedrag te configureren.

### <a name="step-8"></a>Stap 8

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

Deze stap configureert u Hallo exemplaargrootte van de toepassingsgateway Hallo.

> [!NOTE]
> de standaardwaarde voor Hallo *InstanceCount* is 2 en de maximale waarde is 10. de standaardwaarde voor Hallo *GatewaySize* is normaal. U kunt kiezen tussen Standard_Small, Standard_Medium en Standard_Large.

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a>Een toepassingsgateway maken met behulp van New-AzureApplicationGateway

Hiermee maakt een toepassingsgateway met alle configuratie-items uit de vorige stappen Hallo. In dit voorbeeld wordt de toepassingsgateway Hallo 'appgwtest' genoemd.

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

Deze stap maakt een toepassingsgateway met alle configuratie-items uit de vorige stappen Hallo. In voorbeeld Hallo Hallo toepassingsgateway 'appgwtest' genoemd.

## <a name="delete-an-application-gateway"></a>Een toepassingsgateway verwijderen

een toepassingsgateway toodelete, moet u toodo Hallo stappen te volgen in de volgorde:

1. Gebruik Hallo `Stop-AzureRmApplicationGateway` cmdlet toostop Hallo gateway.
2. Gebruik Hallo `Remove-AzureRmApplicationGateway` cmdlet tooremove Hallo gateway.
3. Controleer of deze Hallo-gateway is verwijderd met behulp van Hallo `Get-AzureApplicationGateway` cmdlet.

### <a name="step-1"></a>Stap 1

Hallo application gateway-object ophalen en koppelt u deze variabele tooa '$getgw'.

```powershell
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

### <a name="step-2"></a>Stap 2

Gebruik `Stop-AzureRmApplicationGateway` toostop Hallo toepassingsgateway. Dit voorbeeld wordt Hallo `Stop-AzureRmApplicationGateway` cmdlet uit op de eerste regel hello, gevolgd door Hallo uitvoer.

```powershell
Stop-AzureRmApplicationGateway -ApplicationGateway $getgw  
```

```
VERBOSE: 9:49:34 PM - Begin Operation: Stop-AzureApplicationGateway
VERBOSE: 10:10:06 PM - Completed Operation: Stop-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   ce6c6c95-77b4-2118-9d65-e29defadffb8
```

Nadat de toepassingsgateway Hallo gestopt is, gebruikt u Hallo `Remove-AzureRmApplicationGateway` cmdlet tooremove Hallo-service.

```powershell
Remove-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Force
```

```
VERBOSE: 10:49:34 PM - Begin Operation: Remove-AzureApplicationGateway
VERBOSE: 10:50:36 PM - Completed Operation: Remove-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   055f3a96-8681-2094-a304-8d9a11ad8301
```

> [!NOTE]
> Hallo **-force** switch kan worden gebruikt toosuppress Hallo bevestigingsbericht voor verwijdering.

tooverify die Hallo service is verwijderd, kunt u Hallo `Get-AzureRmApplicationGateway` cmdlet. Deze stap is niet vereist.

```powershell
Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: hello gateway does not exist.
```

## <a name="next-steps"></a>Volgende stappen

Als u tooconfigure SSL-offload wilt, Zie [een toepassingsgateway voor SSL-offload configureren](application-gateway-ssl.md).

Als u wilt dat tooconfigure een toouse application gateway met een ILB, raadpleegt u [een toepassingsgateway maken met een interne load balancer (ILB)](application-gateway-ilb.md).

Als u meer informatie wilt over de algemene opties voor load balancing, raadpleegt u:

* [Azure Load Balancer](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/)

