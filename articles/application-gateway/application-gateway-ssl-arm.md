---
title: aaaConfigure SSL-offload - Azure Application Gateway - PowerShell | Microsoft Docs
description: Deze pagina vindt u instructies toocreate een toepassingsgateway met SSL-offload met Azure Resource Manager
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
ms.openlocfilehash: c2855d8d3caaa97ec05475c67ff0f8dce72ef2a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-azure-resource-manager"></a>Een toepassingsgateway configureren voor SSL-offload met Azure Resource Manager

> [!div class="op_single_selector"]
> * [Azure Portal](application-gateway-ssl-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-ssl-arm.md)
> * [Azure Classic PowerShell](application-gateway-ssl.md)
> * [Azure CLI 2.0](application-gateway-ssl-cli.md)

Azure Application Gateway kan worden geconfigureerd tooterminate Hallo Secure Sockets Layer (SSL)-sessie op Hallo gateway tooavoid kostbare SSL ontsleuteling taken toohappen op Hallo-webfarm. SSL-offload vereenvoudigt ook Hallo front-end-server instellen en beheren van Hallo-webtoepassing.

## <a name="before-you-begin"></a>Voordat u begint

1. Hallo meest recente versie van hello Azure PowerShell-cmdlets installeren met behulp van Hallo Web Platform Installer. U kunt downloaden en installeren van de meest recente versie Hallo van Hallo **Windows PowerShell** sectie Hallo [pagina Downloads](https://azure.microsoft.com/downloads/).
2. U maakt een virtueel netwerk en een subnet voor de toepassingsgateway Hallo. Zorg ervoor dat er geen virtuele machines en cloudimplementaties die van Hallo subnet gebruikmaken zijn. De toepassingsgateway moet afzonderlijk in een subnet van een virtueel netwerk staan.
3. Hallo-servers configureren van toouse Hallo toepassingsgateway moeten bestaan of hebben hun eindpunten gemaakt in het virtuele netwerk hello of een openbaar IP-/ VIP-adres toegewezen.

## <a name="what-is-required-toocreate-an-application-gateway"></a>Wat is vereist toocreate een application gateway?

* **Back-endserverpool:** Hallo lijst met IP-adressen van Hallo back-endservers. Hallo IP-adressen moeten ofwel deel uitmaken toohello virtueel netwerksubnet ofwel moeten een openbare IP-/ VIP.
* **Back-endserverpoolinstellingen:** elke pool heeft instellingen, zoals voor de poort, het protocol en de op cookies gebaseerde affiniteit. Deze instellingen zijn gebonden tooa servergroep en toegepaste tooall servers binnen de pool Hallo zijn.
* **Front-endpoort:** deze is Hallo openbare poort die in Hallo toepassingsgateway wordt geopend. Verkeer komt binnen via deze poort en vervolgens wordt omgeleid tooone van Hallo back-endservers.
* **Listener:** Hallo listener beschikt over een front-endpoort, een protocol (Http of Https; deze instellingen zijn hoofdlettergevoelig), en Hallo SSL-certificaatnaam (als u SSL-offloading configureert).
* **Regel:** Hallo regel verbindt Hallo listener Hallo back-endserverpool en definieert welk verkeer van back-endserver groep Hallo moet gerichte toowhen dit bij een bepaalde listener aankomt. Op dit moment alleen Hallo *basic* regel wordt ondersteund. Hallo *basic* regel is round-robinbelastingverdeling.

**Aanvullende configuratieopmerkingen**

Hallo-protocol in voor de configuratie van SSL-certificaten, **HttpListener** moet ook wijzigen*Https* (hoofdlettergevoelig). Hallo **SslCertificate** element te toegevoegd**HttpListener** met Hallo variabele waarde die is geconfigureerd voor SSL-certificaat Hallo. Hallo front-endpoort moet bijgewerkte too443.

**tooenable cookies gebaseerde affiniteit**: een application gateway kan worden geconfigureerd tooensure is een aanvraag van een clientsessie altijd gerichte toohello dezelfde virtuele machine in de webfarm Hallo. Dit scenario wordt gedaan door het injecteren van een sessiecookie waarmee Hallo gateway toodirect verkeer op de juiste wijze. tooenable cookies gebaseerde affiniteit ingesteld **CookieBasedAffinity** te*ingeschakeld* in Hallo **BackendHttpSettings** element.

## <a name="create-an-application-gateway"></a>Een toepassingsgateway maken

Hallo verschil tussen het gebruik van de klassieke Azure-implementatiemodel Hallo en Azure Resource Manager is Hallo volgorde die u maakt een application gateway en Hallo de items die u moet toobe geconfigureerd.

Met Resource Manager worden alle onderdelen van een toepassingsgateway worden afzonderlijk geconfigureerd en vervolgens samen toocreate een toepassingsgatewayresource.

Hier volgen Hallo stappen die nodig zijn toocreate een toepassingsgateway:

1. Een resourcegroep maken voor Resource Manager
2. Virtueel netwerk, subnet en openbaar IP-adres voor de toepassingsgateway Hallo maken
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

Maak een resourcegroep (u kunt deze stap overslaan als u een bestaande resourcegroep gebruikt).

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

Azure Resource Manager vereist dat er voor alle resourcegroepen een locatie wordt opgegeven. Deze instelling wordt gebruikt als Hallo standaardlocatie voor resources in die resourcegroep. Zorg ervoor dat alle opdrachten toocreate maakt gebruik van een toepassingsgateway Hallo dezelfde resourcegroep.

In Hallo bovenstaande voorbeeld is er een resourcegroep aangeroepen gemaakt **appgw-RG** en locatie **VS-West**.

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a>Een virtueel netwerk en een subnet voor de toepassingsgateway Hallo maken

Hallo volgende voorbeeld wordt getoond hoe toocreate een virtueel netwerk met Resource Manager:

### <a name="step-1"></a>Stap 1

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

Dit voorbeeld wordt een virtueel netwerk toegewezen Hallo adres adresbereik 10.0.0.0/24 tooa subnet variabele toobe gebruikt toocreate.

### <a name="step-2"></a>Stap 2

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

In dit voorbeeld wordt een virtueel netwerk met de naam **appgwvnet** in de resourcegroep **appgw-rg** voor de regio VS-West Hallo met Hallo voorvoegsel 10.0.0.0/16 met het subnet 10.0.0.0/24.

### <a name="step-3"></a>Stap 3

```powershell
$subnet = $vnet.Subnets[0]
```

Dit voorbeeld wordt Hallo subnet object toovariable $subnet voor de volgende stappen Hallo toegewezen.

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>Een openbaar IP-adres voor de front-endconfiguratie Hallo maken

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

In dit voorbeeld wordt een openbare IP-resource **publicIP01** in de resourcegroep **appgw-rg** voor de regio VS-West Hallo.

## <a name="create-an-application-gateway-configuration-object"></a>Een configuratieobject voor de toepassingsgateway maken

### <a name="step-1"></a>Stap 1

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

In dit voorbeeld wordt een toepassingsgateway een IP-configuratie met de naam **gatewayIP01**. Wanneer de toepassingsgateway wordt geopend, een IP-adres van de geconfigureerde Hallo subnet opneemt en routeren netwerkverkeer toohello IP-adressen in Hallo backend-IP-adresgroep. Onthoud dat elk exemplaar één IP-adres gebruikt.

### <a name="step-2"></a>Stap 2

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221,134.170.185.50
```

Dit voorbeeld configureert Hallo backend-IP-adresgroep met de naam **pool01** met IP-adressen **134.170.185.46**, **134.170.188.221**, **134.170.185.50** . Deze waarden zijn Hallo IP-adressen die ontvangen netwerkverkeer op Hallo van Hallo front-end-IP-eindpunt binnenkomt. Hallo IP-adressen uit het voorgaande voorbeeld met Hallo IP-adressen van uw web-eindpunten toepassing hello vervangen.

### <a name="step-3"></a>Stap 3

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Enabled
```

Dit voorbeeld configureert u de instelling voor application gateway **poolsetting01** tooload netwerkverkeer in Hallo back-endpool.

### <a name="step-4"></a>Stap 4

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 443
```

Dit voorbeeld configureert u Hallo front-end-IP-poort met de naam **frontendport01** voor Hallo openbare IP-eindpunt.

### <a name="step-5"></a>Stap 5

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path for certificate file> -Password "<password>"
```

Dit voorbeeld configureert Hallo gebruikte certificaat voor SSL-verbinding. Hallo-certificaat moet toobe in PFX-indeling en Hallo wachtwoord moet tussen 4 too12 tekens.

### <a name="step-6"></a>Stap 6

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip
```

In dit voorbeeld wordt Hallo front-end-IP-configuratie met de naam **fipconfig01** en gekoppeld Hallo openbaar IP-adres met Hallo front-end-IP-configuratie.

### <a name="step-7"></a>Stap 7

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert
```

In dit voorbeeld wordt de naam van de beschikbaarheidsgroeplistener hello **listener01** en gekoppeld Hallo front-endpoort toohello front-end-IP-configuratie en het certificaat.

### <a name="step-8"></a>Stap 8

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

In dit voorbeeld wordt Hallo load balancer-routeringsregel met de naam **rule01** die het gedrag van Hallo load balancer configureert.

### <a name="step-9"></a>Stap 9

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

Dit voorbeeld configureert Hallo exemplaargrootte van de toepassingsgateway Hallo.

> [!NOTE]
> de standaardwaarde voor Hallo *InstanceCount* is 2 en de maximale waarde is 10. de standaardwaarde voor Hallo *GatewaySize* is normaal. U kunt kiezen tussen Standard_Small, Standard_Medium en Standard_Large.

### <a name="step-10"></a>Stap 10

```powershell
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S
```

Deze stap definieert Hallo SSL beleid toouse op Hallo toepassingsgateway. Ga naar [SSL configureren voor versies en coderingssuites in toepassingsgateway](application-gateway-configure-ssl-policy-powershell.md) toolearn meer.

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a>Een toepassingsgateway maken met behulp van New-AzureApplicationGateway

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SslCertificates $cert -SslPolicy $policy
```

Dit voorbeeld maakt een toepassingsgateway met alle configuratie-items uit de vorige stappen Hallo. In voorbeeld Hallo Hallo toepassingsgateway heet **appgwtest**.

## <a name="get-application-gateway-dns-name"></a>DNS-naam van toepassingsgateway verkrijgen

Zodra Hallo gateway is gemaakt, is de volgende stap Hallo tooconfigure Hallo front-end voor communicatie. Wanneer u een openbare IP gebruikt, heeft de toepassingsgateway een dynamisch toegewezen DNS-naam nodig. Dit is niet gebruiksvriendelijk. eindgebruikers tooensure kunt Hallo toepassingsgateway bereikt, een CNAME-record kan gebruikte toopoint toohello openbaar eindpunt van de toepassingsgateway Hallo. [Een aangepaste domeinnaam configureren voor in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md). toodo deze, details ophalen van de toepassingsgateway Hallo en de bijbehorende IP-en DNS-naam op Hallo PublicIPAddress element gekoppelde toohello application gateway met. Hallo application gateway DNS-naam moet gebruikte toocreate een CNAME-record punten Hallo twee web applications toothis DNS-naam. Hallo-gebruik van A-records wordt niet aanbevolen omdat Hallo VIP bij opnieuw opstarten van toepassingsgateway mag wijzigen.


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

Als u wilt tooconfigure een toouse application gateway met een interne load balancer (ILB), Zie [een toepassingsgateway maken met een interne load balancer (ILB)](application-gateway-ilb.md).

Als u meer informatie wilt over de algemene opties voor load balancing, raadpleegt u:

* [Azure Load Balancer](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/)

