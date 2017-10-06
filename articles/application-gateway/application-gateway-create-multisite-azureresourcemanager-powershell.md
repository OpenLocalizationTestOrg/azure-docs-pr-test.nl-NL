---
title: een toepassingsgateway voor het hosten van meerdere sites aaaCreate | Microsoft Docs
description: Deze pagina vindt u instructies toocreate, het configureren van een toepassingsgateway voor het hosten van meerdere webtoepassingen op Hallo dezelfde gateway.
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: b107d647-c9be-499f-8b55-809c4310c783
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/12/2016
ms.author: amsriva
ms.openlocfilehash: bad9a76be0a73a7026a770630fa7156f6e5940c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-for-hosting-multiple-web-applications"></a>Een toepassingsgateway voor het hosten van meerdere webtoepassingen maken

> [!div class="op_single_selector"]
> * [Azure Portal](application-gateway-create-multisite-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-multisite-azureresourcemanager-powershell.md)

Meerdere hosting-site kunt u toodeploy meer dan één webtoepassing op Hallo dezelfde toepassingsgateway. Is afhankelijk van de aanwezigheid van de host-header in Hallo inkomende HTTP-aanvraag, toodetermine welke listener verkeer ontvangt. Hallo-listener stuurt vervolgens verkeer tooappropriate back-endpool zoals geconfigureerd in de definitie van de gateway Hallo Hallo. In webtoepassingen SSL is ingeschakeld, is de toepassingsgateway afhankelijk van Hallo indicatie voor Server-naam (SNI) extensie toochoose Hallo juist listener voor internetverkeer Hallo. Vaak gebruikt voor het hosten van meerdere site is van aanvragen verdelen over tooload voor verschillende web domeinen toodifferent back-end-servergroepen. Op dezelfde manier Hallo meerdere subdomeinen Hallo dezelfde hoofddomein kan ook worden gehost op dezelfde toepassingsgateway.

## <a name="scenario"></a>Scenario

In de Hallo voorbeeld te volgen, toepassingsgateway verkeer voor contoso.com en fabrikam.com bedient met twee back-endserver van toepassingen: contoso-servergroep en fabrikam-servergroep. Vergelijkbare installatie wordt mogelijk gebruikt toohost subdomeinen zoals app.contoso.com en blog.contoso.com.

![imageURLroute](./media/application-gateway-create-multisite-azureresourcemanager-powershell/multisite.png)

## <a name="before-you-begin"></a>Voordat u begint

1. Hallo meest recente versie van hello Azure PowerShell-cmdlets installeren met behulp van Hallo Web Platform Installer. U kunt downloaden en installeren van de meest recente versie Hallo van Hallo **Windows PowerShell** sectie Hallo [pagina Downloads](https://azure.microsoft.com/downloads/).
2. Hallo-servers toegevoegd toohello back-end-pool toouse Hallo application gateway moet al bestaan of hebt gemaakt hun eindpunten in Hallo virtueel netwerk in een apart subnet of een openbaar IP-/ VIP-adres toegewezen.

## <a name="requirements"></a>Vereisten

* **Back-endserverpool:** Hallo lijst met IP-adressen van Hallo back-endservers. Hallo IP-adressen moeten ofwel deel uitmaken toohello virtueel netwerksubnet ofwel moeten een openbare IP-/ VIP. FQDN-naam kan ook worden gebruikt.
* **Back-endserverpoolinstellingen:** elke pool heeft instellingen, zoals voor de poort, het protocol en de op cookies gebaseerde affiniteit. Deze instellingen zijn gebonden tooa servergroep en toegepaste tooall servers binnen de pool Hallo zijn.
* **Front-endpoort:** deze is Hallo openbare poort die in Hallo toepassingsgateway wordt geopend. Verkeer komt binnen via deze poort en vervolgens wordt omgeleid tooone van Hallo back-endservers.
* **Listener:** Hallo listener beschikt over een front-endpoort, een protocol (Http of Https; deze waarden zijn hoofdlettergevoelig), en Hallo SSL-certificaatnaam (als u SSL-offloading configureert). Voor meerdere locaties ingeschakeld Toepassingsgateways, hostnaam en SNI indicatoren ook worden toegevoegd.
* **Regel:** Hallo regel verbindt Hallo listener, Hallo back-endserverpool, en definieert naar welke back-endserver groep Hallo verkeer moet gerichte toowhen dit bij een bepaalde listener aankomt. Regels worden verwerkt op Hallo volgorde die ze worden weergegeven en verkeer wordt omgeleid via Hallo eerste regel die overeenkomt met ongeacht specifieke karakter. Bijvoorbeeld, als u een regel met een basic-listener en een regel met meerdere sites listener beide op dezelfde poort, regel met Hallo Hallo hebt moet Hallo multi-site-listener worden weergegeven voordat Hallo regel met Hallo basic listener om Hallo multi-site regel toofunction als Er werd verwacht.

## <a name="create-an-application-gateway"></a>Een toepassingsgateway maken

Hallo hieronder vindt u Hallo stappen nodig toocreate een toepassingsgateway:

1. Maak een resourcegroep voor Resource Manager.
2. Maak een virtueel netwerk, subnetten en openbare IP-adres voor de toepassingsgateway Hallo.
3. Maak een configuratieobject voor de toepassingsgateway.
4. Maak een toepassingsgatewayresource.

## <a name="create-a-resource-group-for-resource-manager"></a>Een resourcegroep maken voor Resource Manager

Zorg ervoor dat u van Hallo meest recente versie van Azure PowerShell gebruikmaakt. Meer informatie vindt u op [Windows PowerShell gebruiken met Resource Manager](../powershell-azure-resource-manager.md).

### <a name="step-1"></a>Stap 1

Meld u bij tooAzure

```powershell
Login-AzureRmAccount
```
Vraag tooauthenticate bent u met uw referenties.

### <a name="step-2"></a>Stap 2

Controleer de abonnementen Hallo voor Hallo-account.

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a>Stap 3

Kies welke van uw Azure-abonnementen toouse.

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a>Stap 4

Maak een resourcegroep (u kunt deze stap overslaan als u een bestaande resourcegroep gebruikt).

```powershell
New-AzureRmResourceGroup -Name appgw-RG -location "West US"
```

U kunt ook ook labels voor een resourcegroep voor de toepassingsgateway maken:

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway multiple site"}
```

Azure Resource Manager vereist dat er voor alle resourcegroepen een locatie wordt opgegeven. Deze locatie wordt gebruikt als Hallo standaardlocatie voor resources in die resourcegroep. Zorg ervoor dat alle opdrachten toocreate een application gateway gebruik Hallo dezelfde resourcegroep.

In Hallo bovenstaande voorbeeld is er een resourcegroep aangeroepen gemaakt **appgw-RG** met een locatie van **VS-West**.

> [!NOTE]
> Als u voor uw toepassingsgateway een aangepaste test tooconfigure nodig hebt, raadpleegt u [met PowerShell een toepassingsgateway maken met aangepaste tests](application-gateway-create-probe-ps.md). Ga naar [aangepaste tests en statuscontrole](application-gateway-probe-overview.md) voor meer informatie.

## <a name="create-a-virtual-network-and-subnets"></a>Een virtueel netwerk en subnetten maken

Hallo volgende voorbeeld wordt getoond hoe toocreate een virtueel netwerk met Resource Manager. Twee subnetten worden gemaakt in deze stap. het eerste subnet Hallo is voor de toepassingsgateway Hallo zelf. Toepassingsgateway vereist een eigen subnet toohold de exemplaren. Alleen andere toepassingsgateways kunnen worden geïmplementeerd in dat subnet. het tweede subnet Hallo is gebruikte toohold Hallo toepassing back-endservers.

### <a name="step-1"></a>Stap 1

Hallo adres adresbereik 10.0.0.0/24 toohello subnet variabele toobe gebruikte toohold Hallo toepassingsgateway toewijzen.

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -AddressPrefix 10.0.0.0/24
```
### <a name="step-2"></a>Stap 2

Hallo adresbereik 10.0.1.0/24 toohello subnet2 variabele toobe gebruikt voor back-endpools Hallo toewijzen.

```powershell
$subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -AddressPrefix 10.0.1.0/24
```

### <a name="step-3"></a>Stap 3

Maak een virtueel netwerk met de naam **appgwvnet** in de resourcegroep **appgw-rg** voor de regio VS-West Hallo Hallo voorvoegsel 10.0.0.0/16 met het subnet 10.0.0.0/24 met en 10.0.1.0/24.

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet,$subnet2
```

### <a name="step-4"></a>Stap 4

Wijs een subnetvariabele toe voor de volgende stappen hello, waarmee u een toepassingsgateway maakt.

```powershell
$appgatewaysubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -VirtualNetwork $vnet
$backendsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>Een openbaar IP-adres voor de front-endconfiguratie Hallo maken

Maak een openbare IP-resource **publicIP01** in de resourcegroep **appgw-rg** voor de regio VS-West Hallo.

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

Een IP-adres is toohello toepassingsgateway toegewezen wanneer Hallo-service wordt gestart.

## <a name="create-application-gateway-configuration"></a>De gatewayconfiguratie toepassing maken

U hebt tooset van alle configuratie-items voordat u de toepassingsgateway Hallo maakt. Hallo volgt Hallo configuratie-items maken die nodig zijn voor een toepassingsgatewayresource.

### <a name="step-1"></a>Stap 1

Maak voor de toepassingsgateway een IP-configuratie en geef deze de naam **gatewayIP01**. Wanneer de toepassingsgateway wordt geopend, een IP-adres van de geconfigureerde Hallo subnet opneemt en routeren netwerkverkeer toohello IP-adressen in Hallo backend-IP-adresgroep. Onthoud dat elk exemplaar één IP-adres gebruikt.

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $appgatewaysubnet
```

### <a name="step-2"></a>Stap 2

Configureer Hallo backend-IP-adresgroep met de naam **pool01** en **pool2** met IP-adressen **134.170.185.46**, **134.170.188.221**, **134.170.185.50** voor **pool1** en **134.170.186.46**, **134.170.189.221**, **134.170.186.50**  voor **pool2**.

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.0.1.100, 10.0.1.101, 10.0.1.102
$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 10.0.1.103, 10.0.1.104, 10.0.1.105
```

In dit voorbeeld zijn er twee back-end-adresgroepen tooroute-netwerkverkeer op basis van de gevraagde website Hallo. Één groep verkeer ontvangt van de site 'contoso.com' en andere toepassingen verkeer van site 'fabrikam.com' ontvangt. U hebt tooreplace Hallo IP-adressen tooadd voorafgaand aan uw eigen toepassing IP-adres-eindpunten. In plaats van interne IP-adressen kan u openbare IP-adressen, FQDN-naam of NIC van een virtuele machine ook gebruiken voor back-end-exemplaren. toospecify FQDN-namen in plaats van IP-adressen in het gebruik van PowerShell '-BackendFQDNs ' parameter.

### <a name="step-3"></a>Stap 3

Configureren van de instelling voor application gateway **poolsetting01** en **poolsetting02** voor Hallo taakverdeling netwerkverkeer in Hallo back-endpool. In dit voorbeeld kunt u instellingen van de andere back-end-adresgroep voor Hallo back-end-adresgroepen configureren. Elke back-endpool kan een eigen instelling van de back-endpool hebben.

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120
$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a>Stap 4

Hallo front-end-IP-met openbare IP-eindpunt configureren.

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a>Stap 5

Hallo front-endpoort voor een toepassingsgateway configureren.

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 443
```

### <a name="step-6"></a>Stap 6

Configureer twee SSL-certificaten voor Hallo twee websites gaan we toosupport in dit voorbeeld. Er is één certificaat voor contoso.com verkeer en Hallo andere voor fabrikam.com verkeer. Deze certificaten moeten een certificeringsinstantie uitgegeven certificaten voor uw websites. Zelfondertekende certificaten worden ondersteund, maar niet aanbevolen voor productie-verkeer.

```powershell
$cert01 = New-AzureRmApplicationGatewaySslCertificate -Name contosocert -CertificateFile <file path> -Password <password>
$cert02 = New-AzureRmApplicationGatewaySslCertificate -Name fabrikamcert -CertificateFile <file path> -Password <password>
```

### <a name="step-7"></a>Stap 7

Configureer twee listeners voor twee websites Hallo in dit voorbeeld. Deze stap configureert Hallo listeners voor openbare IP-adres, poort en host tooreceive binnenkomend verkeer gebruikt. HostName-parameter is vereist voor ondersteuning voor meerdere site en moet toohello juiste website instellen voor welke Hallo verkeer wordt ontvangen. RequireServerNameIndication-parameter moet worden ingesteld als tootrue voor websites die ondersteuning voor SSL in een scenario voor meerdere host nodig. Als u ondersteuning voor SSL is vereist, moet u ook toospecify Hallo SSL certificaat namelijk gebruikte toosecure verkeer voor deze webtoepassing. Hallo combinatie van FrontendIPConfiguration FrontendPort en HostName moet unieke tooa listener. Elke listener kan één certificaat ondersteunen.

```powershell
$listener01 = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "contoso11.com" -RequireServerNameIndication true  -SslCertificate $cert01
$listener02 = New-AzureRmApplicationGatewayHttpListener -Name "listener02" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "fabrikam11.com" -RequireServerNameIndication true -SslCertificate $cert02
```

### <a name="step-8"></a>Stap 8

Maak twee regel instellen voor Hallo twee webtoepassingen in dit voorbeeld. Een regel verbindt samen listeners, back-endpools en HTTP-instellingen. Deze stap configureert u Hallo application gateway toouse Basic routeringsregel, één voor elke website. Verkeer tooeach website wordt ontvangen door de geconfigureerde listener en wordt vervolgens omgeleid tooits back-endpool met behulp van Hallo-eigenschappen die zijn opgegeven in Hallo BackendHttpSettings geconfigureerd.

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule01" -RuleType Basic -HttpListener $listener01 -BackendHttpSettings $poolSetting01 -BackendAddressPool $pool1
$rule02 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule02" -RuleType Basic -HttpListener $listener02 -BackendHttpSettings $poolSetting02 -BackendAddressPool $pool2
```

### <a name="step-9"></a>Stap 9

Hallo aantal exemplaren en de grootte voor de toepassingsgateway Hallo configureren.

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Medium" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a>Toepassingsgateway maken

Een toepassingsgateway met alle configuratie-objecten uit de vorige stappen Hallo maken.

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener01, $listener02 -RequestRoutingRules $rule01, $rule02 -Sku $sku -SslCertificates $cert01, $cert02
```

> [!IMPORTANT]
> Inrichting van Application Gateway is een langdurige bewerking en sommige toocomplete tijd kan duren.
> 
> 

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

Meer informatie over hoe tooprotect uw websites met [Application Gateway - Web Application Firewall](application-gateway-webapplicationfirewall-overview.md)

