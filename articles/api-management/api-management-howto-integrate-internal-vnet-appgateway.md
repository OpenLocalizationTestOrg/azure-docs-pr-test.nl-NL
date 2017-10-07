---
title: aaaHow toouse Azure API Management in virtueel netwerk met Application Gateway | Microsoft Docs
description: Meer informatie over hoe toosetup en Azure API Management in een intern virtueel netwerk met Application Gateway (WAF) als FrontEnd configureren
services: api-management
documentationcenter: 
author: solankisamir
manager: kjoshi
editor: antonba
ms.assetid: a8c982b2-bca5-4312-9367-4a0bbc1082b1
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/16/2017
ms.author: sasolank
ms.openlocfilehash: 74303a2ee8a10db633ab1740ec7267728eacb473
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-api-management-in-an-internal-vnet-with-application-gateway"></a>API Management in een interne VNET integreren met Application Gateway 

##<a name="overview"></a> Overzicht
 
Hallo API Management-service kan worden geconfigureerd in een virtueel netwerk in de interne modus waardoor alleen toegankelijk vanuit Hallo virtueel netwerk. Azure Application Gateway is een PAAS-Service die voorziet in een load balancer van laag 7. Het fungeert als een reverse proxy-service en biedt tussen het aanbieden van een Web Application Firewall (WAF).

Combineren van API Management ingericht in een interne VNET met Hallo Application Gateway frontend kunt Hallo volgen scenario's:

* Gebruik dezelfde Hallo API Management-resource voor verbruik door consumenten interne en externe gebruikers.
* Gebruik één API Management-resource en hebt u een subset van API's die zijn gedefinieerd in API Management beschikbaar voor externe gebruikers.
* Bieden een directe manier tooswitch toegang tooAPI Management van Hallo openbare Internet in- of uitschakelen. 

##<a name="scenario"></a> Scenario
In dit artikel wordt uitgelegd hoe toouse één API-Management-service voor zowel interne als externe consumenten en fungeren als een enkel frontend voor zowel on-premises en in de cloud-API's. U ziet ook hoe tooexpose slechts een subset van uw API's (per Hallo zoals ze zijn gemarkeerd in het groen) voor extern verbruik met Hallo PathBasedRouting functionaliteit beschikbaar zijn in de toepassingsgateway.

Uw API's worden in de eerste installatie voorbeeld Hallo beheerd alleen vanuit binnen het virtuele netwerk. Interne consumenten (gemarkeerd in oranje) hebben toegang tot alle uw interne en externe API's. Verkeer wordt nooit wordt gedeeld tooInternet die wordt geleverd met een hoge prestaties via Express Route-circuits.

![URL-route](./media/api-management-howto-integrate-internal-vnet-appgateway/api-management-howto-integrate-internal-vnet-appgateway.png)

## <a name="before-you-begin"></a> Voordat u begint

1. Hallo meest recente versie van hello Azure PowerShell-cmdlets installeren met behulp van Hallo Web Platform Installer. U kunt downloaden en installeren van de meest recente versie Hallo van Hallo **Windows PowerShell** sectie Hallo [pagina Downloads](https://azure.microsoft.com/downloads/).
2. Maak een virtueel netwerk en maak afzonderlijke subnetten voor API Management en Application Gateway. 
3. Als u van plan een aangepaste DNS-server voor het virtuele netwerk Hallo toocreate bent, doen voordat u Hallo implementatie start. Controleer die het werkt door te zorgen voor een virtuele machine gemaakt in een nieuw subnet in Hallo virtueel netwerk kunt omzetten en toegang tot alle Azure-service-eindpunten.

## <a name="what-is-required-toocreate-an-integration-between-api-management-and-application-gateway"></a>Wat is vereist toocreate een integratie tussen API Management en Application Gateway?

* **Back-endserverpool:** dit Hallo interne virtuele IP-adres van Hallo API Management-service is.
* **Back-endserverpoolinstellingen:** elke pool heeft instellingen, zoals voor de poort, het protocol en de op cookies gebaseerde affiniteit. Deze instellingen zijn toegepast tooall servers binnen Hallo van toepassingen.
* **Front-endpoort:** dit Hallo openbare poort die in Hallo toepassingsgateway wordt geopend is. Roept het verkeer opgehaald omgeleide tooone Hallo back-endservers.
* **Listener:** Hallo listener beschikt over een front-endpoort, een protocol (Http of Https; deze waarden zijn hoofdlettergevoelig), en Hallo SSL-certificaatnaam (als u SSL-offloading configureert).
* **Regel:** Hallo regel een listener tooa back-endserverpool wordt gebonden.
* **Aangepaste Health test:** Application Gateway maakt standaard gebruik van IP-adres op basis van tests toofigure uit welke servers in Hallo BackendAddressPool actief zijn. Hallo API Management-service reageert alleen toorequests waarvoor de juiste host-header hello, daarom Hallo standaard tests is mislukt. Een aangepaste health test moet toobe gedefinieerd toohelp toepassingsgateway bepalen dat Hallo-service actief is en moet deze aanvragen worden doorgestuurd.
* **Aangepaste Domeincertificaat:** tooaccess API Management van Hallo internet, moet u een CNAME-toewijzing van de hostnaam toohello Application Gateway front-DNS-naam toocreate. Dit zorgt ervoor dat Hallo hostname-header en het certificaat dat is verzonden tooApplication Gateway die wordt doorgestuurd tooAPI Management is een die APIM als geldige herkennen kan.

## <a name="overview-steps"></a> Stappen die nodig zijn voor het integreren van API Management en Application Gateway 

1. Maak een resourcegroep voor Resource Manager.
2. Maak een virtueel netwerk, subnet en openbaar IP-adres voor Hallo Application Gateway. Maak een ander subnet voor API Management.
3. Maak een API Management-service binnen Hallo VNET subnet die eerder is gemaakt en zorg ervoor dat u interne Hallo-modus.
4. Het instellen van de aangepaste domeinnaam Hallo in Hallo API Management-service.
5. Maak een configuratieobject voor de toepassingsgateway.
6. Een Application Gateway-resource maken.
7. Maak een CNAME van Hallo openbare DNS-naam van Hallo Application Gateway toohello API Management proxy hostnaam.

## <a name="create-a-resource-group-for-resource-manager"></a>Een resourcegroep maken voor Resource Manager

Zorg ervoor dat u van Hallo meest recente versie van Azure PowerShell gebruikmaakt. Zie [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Windows PowerShell gebruiken met Resource Manager) voor meer informatie.

### <a name="step-1"></a>Stap 1

Meld u bij tooAzure

```powershell
Login-AzureRmAccount
```

Verifiëren met uw referenties.<BR>

### <a name="step-2"></a>Stap 2

Controleer de abonnementen Hallo voor Hallo-account en selecteer deze.

```powershell
Get-AzureRmSubscription -Subscriptionid "GUID of subscription" | Select-AzureRmSubscription
```

### <a name="step-3"></a>Stap 3

Maak een resourcegroep (u kunt deze stap overslaan als u een bestaande resourcegroep gebruikt).

```powershell
New-AzureRmResourceGroup -Name "apim-appGw-RG" -Location "West US"
```
Azure Resource Manager vereist dat er voor alle resourcegroepen een locatie wordt opgegeven. Dit wordt gebruikt als Hallo standaardlocatie voor resources in die resourcegroep. Zorg ervoor dat alle opdrachten toocreate een application gateway gebruik Hallo dezelfde resourcegroep.

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a>Een virtueel netwerk en een subnet voor de toepassingsgateway Hallo maken

Hallo volgende voorbeeld ziet u hoe een virtueel netwerk met toocreate Hallo resourcemanager.

### <a name="step-1"></a>Stap 1

Hallo adres adresbereik 10.0.0.0/24 toohello subnet variabele toobe gebruikt voor toepassingsgateway tijdens het maken van een virtueel netwerk toewijzen.

```powershell
$appgatewaysubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim01" -AddressPrefix "10.0.0.0/24"
```

### <a name="step-2"></a>Stap 2

Hallo adresbereik 10.0.1.0/24 toohello subnet variabele toobe gebruikt voor API Management tijdens het maken van een virtueel netwerk toewijzen.

```powershell
$apimsubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim02" -AddressPrefix "10.0.1.0/24"
```

### <a name="step-3"></a>Stap 3

Maak een virtueel netwerk met de naam **appgwvnet** in de resourcegroep **apim-appGw-RG** voor de regio VS-West Hallo Hallo voorvoegsel 10.0.0.0/16 met met subnetten 10.0.0.0/24 en 10.0.1.0/24.

```powershell
$vnet = New-AzureRmVirtualNetwork -Name "appgwvnet" -ResourceGroupName "apim-appGw-RG" -Location "West US" -AddressPrefix "10.0.0.0/16" -Subnet $appgatewaysubnet,$apimsubnet
```

### <a name="step-4"></a>Stap 4

Wijs een subnetvariabele toe voor de volgende stappen Hallo

```powershell
$appgatewaysubnetdata=$vnet.Subnets[0]
$apimsubnetdata=$vnet.Subnets[1]
```
## <a name="create-an-api-management-service-inside-a-vnet-configured-in-internal-mode"></a>Maak een API Management-service binnen een VNET dat is geconfigureerd in de interne modus

Hallo volgende voorbeeld ziet u hoe toocreate een API Management-service in een VNET geconfigureerd voor interne toegang alleen.

### <a name="step-1"></a>Stap 1
Maakt een virtueel netwerk van API Management-object met behulp van Hallo subnet $apimsubnetdata die eerder is gemaakt.

```powershell
$apimVirtualNetwork = New-AzureRmApiManagementVirtualNetwork -Location "West US" -SubnetResourceId $apimsubnetdata.Id
```
### <a name="step-2"></a>Stap 2
Maak een API Management-service binnen Hallo virtueel netwerk.

```powershell
$apimService = New-AzureRmApiManagement -ResourceGroupName "apim-appGw-RG" -Location "West US" -Name "ContosoApi" -Organization "Contoso" -AdminEmail "admin@contoso.com" -VirtualNetwork $apimVirtualNetwork -VpnType "Internal" -Sku "Developer"
```
Raadpleeg nadat Hallo hierboven opdracht is geslaagd te[DNS-configuratie vereist tooaccess interne VNET API Management-service](api-management-using-with-internal-vnet.md#apim-dns-configuration) tooaccess deze.

## <a name="set-up-a-custom-domain-name-in-api-management"></a>Installatie van een aangepaste domeinnaam in API Management

### <a name="step-1"></a>Stap 1
Upload het Hallo-certificaat met persoonlijke sleutel voor Hallo domein. In dit voorbeeld worden `*.contoso.net`. 

```powershell
$certUploadResult = Import-AzureRmApiManagementHostnameCertificate -ResourceGroupName "apim-appGw-RG" -Name "ContosoApi" -HostnameType "Proxy" -PfxPath <full path too.pfx file> -PfxPassword <password for certificate file> -PassThru
```

### <a name="step-2"></a>Stap 2
Zodra het Hallo-certificaat is geüpload, een configuratieobject voor de hostnaam voor Hallo proxy maken met een hostnaam van `api.contoso.net`, zoals Hallo voorbeeld certificaat autoriteit voor Hallo biedt `*.contoso.net` domein. 

```powershell
$proxyHostnameConfig = New-AzureRmApiManagementHostnameConfiguration -CertificateThumbprint $certUploadResult.Thumbprint -Hostname "api.contoso.net"
$result = Set-AzureRmApiManagementHostnames -Name "ContosoApi" -ResourceGroupName "apim-appGw-RG" -ProxyHostnameConfiguration $proxyHostnameConfig
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>Een openbaar IP-adres voor de front-endconfiguratie Hallo maken

Maak een openbare IP-resource **publicIP01** in de resourcegroep **apim-appGw-RG** voor de regio VS-West Hallo.

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -name "publicIP01" -location "West US" -AllocationMethod Dynamic
```

Een IP-adres is toohello toepassingsgateway toegewezen wanneer Hallo-service wordt gestart.

## <a name="create-application-gateway-configuration"></a>De gatewayconfiguratie toepassing maken

Alle configuratie-items moeten worden ingesteld voordat u de toepassingsgateway Hallo maakt. Hallo volgt Hallo configuratie-items maken die nodig zijn voor een toepassingsgatewayresource.

### <a name="step-1"></a>Stap 1

Maak voor de toepassingsgateway een IP-configuratie en geef deze de naam **gatewayIP01**. Wanneer de toepassingsgateway wordt geopend, een IP-adres van de geconfigureerde Hallo subnet opneemt en routeren netwerkverkeer toohello IP-adressen in Hallo backend-IP-adresgroep. Onthoud dat elk exemplaar één IP-adres gebruikt.

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name "gatewayIP01" -Subnet $appgatewaysubnetdata
```

### <a name="step-2"></a>Stap 2

Hallo front-end-IP-poort voor het openbare IP-eindpunt Hallo configureren. Dit is Hallo-poort waarmee gebruikers verbinding maken.

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "port01"  -Port 443
```
### <a name="step-3"></a>Stap 3

Hallo front-end-IP-met openbare IP-eindpunt configureren.

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-4"></a>Stap 4

Hallo-certificaat configureren voor hello Application Gateway gebruikt toodecrypt en Hallo-verkeer te doorlopen opnieuw versleutelen.

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name "cert01" -CertificateFile <full path too.pfx file> -Password <password for certificate file>
```

### <a name="step-5"></a>Stap 5

Hallo HTTP-listener voor Hallo toepassingsgateway maken. Hallo front-end-IP-configuratie, poort en ssl-certificaat tooit toewijzen.

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol "Https" -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -SslCertificate $cert
```

### <a name="step-6"></a>Stap 6

Maken van een aangepaste test toohello API Management-service `ContosoApi` proxy domein eindpunt. Hallo pad `/status-0123456789abcdef` is een standaardeindpunt health gehost op alle Hallo API Management-services. Stel `api.contoso.net` als een aangepaste test hostnaam toosecure met SSL-certificaat.

> [!NOTE]
> hostname Hallo `contosoapi.azure-api.net` is Hallo standaard proxy hostnaam geconfigureerd als een service met de naam `contosoapi` in openbare Azure is gemaakt. 
> 

```powershell
$apimprobe = New-AzureRmApplicationGatewayProbeConfig -Name "apimproxyprobe" -Protocol "Https" -HostName "api.contoso.net" -Path "/status-0123456789abcdef" -Interval 30 -Timeout 120 -UnhealthyThreshold 8
```

### <a name="step-7"></a>Stap 7

Upload het Hallo-certificaat toobe gebruikt op Hallo resources in de back-end SSL zijn ingeschakeld. Dit is Hallo hetzelfde certificaat dat u hebt opgegeven in stap 4 hierboven.

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name "whitelistcert1" -CertificateFile <full path too.cer file>
```

### <a name="step-8"></a>Stap 8

HTTP-back-end-instellingen voor Application Gateway Hallo configureren. Dit omvat het instellen van een time-out optreedt voor de back-end-aanvraag waarna ze worden geannuleerd. Deze waarde verschilt van Hallo test time.

```powershell
$apimPoolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "apimPoolSetting" -Port 443 -Protocol "Https" -CookieBasedAffinity "Disabled" -Probe $apimprobe -AuthenticationCertificates $authcert -RequestTimeout 180
```

### <a name="step-9"></a>Stap 9

Configureer een backend-IP-adresgroep met de naam **apimbackend** met Hallo interne virtuele IP-adres van Hallo API Management-service die eerder is gemaakt.

```powershell
$apimProxyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "apimbackend" -BackendIPAddresses $apimService.StaticIPs[0]
```

### <a name="step-10"></a>Stap 10

Instellingen maken voor een dummy (niet-bestaand) back-end. Aanvragen tooAPI paden die we niet wilt tooexpose van API Management via Application Gateway wordt bereikt deze back-end en 404 retourneren.

HTTP-instellingen configureren voor Hallo dummy back-end.

```powershell
$dummyBackendSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "dummySetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

Configureer een dummy back-end **dummyBackendPool**, die tooa FQDN-adres wijst **dummybackend.com**. Dit adres FQDN bestaat niet in het virtuele netwerk Hallo.

```powershell
$dummyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "dummyBackendPool" -BackendFqdns "dummybackend.com"
```

Maak een regel instellen die Hallo Application Gateway gebruikt standaard die toohello niet-bestaande back-end wijst **dummybackend.com** in Hallo virtueel netwerk.

```powershell
$dummyPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "nonexistentapis" -Paths "/*" -BackendAddressPool $dummyBackendPool -BackendHttpSettings $dummyBackendSetting
```

### <a name="step-11"></a>Stap 11

URL-regel paden voor back-end-adresgroepen Hallo configureren. Hierdoor kunnen alleen enkele Hallo-API's van API Management voor wordt blootgesteld toohello openbaar. Bijvoorbeeld, als er `Echo API` (/ echo /), `Calculator API` (/calc/) enz. Controleer alleen `Echo API` toegankelijk is vanaf Internet). 

Hallo wordt volgende voorbeeld een eenvoudige regel voor Hallo '/ echo /' pad routering verkeer toohello back-end 'apimProxyBackendPool'.

```powershell
$echoapiRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "externalapis" -Paths "/echo/*" -BackendAddressPool $apimProxyBackendPool -BackendHttpSettings $apimPoolSetting
```

Als Hallo pad komt niet overeen met de Hallo pad regels willen we tooenable van API Management, Hallo regel pad kaart configuratie configureert ook een standaard-back-end-adresgroep met de naam **dummyBackendPool**. Bijvoorbeeld: http://api.contoso.net/calc/ * gaat te**dummyBackendPool** zoals deze is gedefinieerd als de standaardgroep Hallo voor niet-overeenkomende verkeer.

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $echoapiRule, $dummyPathRule -DefaultBackendAddressPool $dummyBackendPool -DefaultBackendHttpSettings $dummyBackendSetting
```

Hallo hierboven stap zorgt ervoor dat alleen aanvragen voor Hallo pad '/ echo' via Hallo Application Gateway zijn toegestaan. Aanvragen tooother API's die zijn geconfigureerd in API Management genereert 404-fouten van Application Gateway wanneer deze vanuit Hallo Internet. 

### <a name="step-12"></a>Stap 12

Maak een instelling voor Hallo Application Gateway toouse URL-pad gebaseerde routering.

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-13"></a>Stap 13

Hallo aantal exemplaren en de grootte voor Hallo Application Gateway configureren. We gebruiken hier Hallo [WAF SKU](../application-gateway/application-gateway-webapplicationfirewall-overview.md) voor een betere beveiliging Hallo API Management-resource.

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "WAF_Medium" -Tier "WAF" -Capacity 2
```

### <a name="step-14"></a>Stap 14

WAF toobe configureren in de modus 'Preventie'.
```powershell
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"
```

## <a name="create-application-gateway"></a>Toepassingsgateway maken

Een toepassingsgateway met alle Hallo configuratie-objecten uit de vorige stappen Hallo maken.

```powershell
$appgw = New-AzureRmApplicationGateway -Name $applicationGatewayName -ResourceGroupName $resourceGroupName  -Location $location -BackendAddressPools $apimProxyBackendPool, $dummyBackendPool -BackendHttpSettingsCollection $apimPoolSetting, $dummyBackendSetting  -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert -Probes $apimprobe
```

## <a name="cname-hello-api-management-proxy-hostname-toohello-public-dns-name-of-hello-application-gateway-resource"></a>CNAME Hallo API Management proxy hostnaam toohello openbare DNS-naam van Hallo Application Gateway resource

Zodra Hallo gateway is gemaakt, is de volgende stap Hallo tooconfigure Hallo front-end voor communicatie. Wanneer u een openbaar IP-adres, vereist Application Gateway een dynamisch toegewezen DNS-naam die gemakkelijk toouse niet mogelijk. 

Hallo toepassingsgateway van DNS-naam moet gebruikte toocreate een CNAME-record die Hallo APIM proxyhostnaam wijst (bijvoorbeeld `api.contoso.net` in bovenstaande Hallo voorbeelden) toothis DNS-naam. Hallo-details van Hallo Application Gateway en de bijbehorende IP-en DNS-naam met behulp van Hallo PublicIPAddress element tooconfigure Hallo frontend IP CNAME-record, worden opgehaald. Hallo-gebruik van A-records wordt niet aanbevolen omdat Hallo VIP kan worden gewijzigd bij opnieuw opstarten van de gateway.

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -Name "publicIP01"
```

##<a name="summary"></a> Samenvatting
Azure API Management geconfigureerd in een VNET biedt een interface één gateway voor alle geconfigureerde API's, ongeacht of deze gehoste on-premises of in Hallo cloud. Integratie van Application Gateway met API Management flexibel Hallo van bepaalde API's toobe toegankelijk is op Internet Hallo selectief inschakelen, evenals bieden een Web Application Firewall als een frontend tooyour API Management-exemplaar.

##<a name="next-steps"></a> Volgende stappen
* Meer informatie over Azure Application Gateway
  * [Overzicht van Application Gateway](../application-gateway/application-gateway-introduction.md)
  * [Application Gateway Web Application Firewall](../application-gateway/application-gateway-webapplicationfirewall-overview.md)
  * [Application Gateway met behulp van Routing op basis van het pad](../application-gateway/application-gateway-create-url-route-arm-ps.md)
* Meer informatie over API Management en VNETs
  * [Met behulp van API Management is alleen beschikbaar in Hallo VNET](api-management-using-with-internal-vnet.md)
  * [Met behulp van API Management in VNET](api-management-using-with-vnet.md)
