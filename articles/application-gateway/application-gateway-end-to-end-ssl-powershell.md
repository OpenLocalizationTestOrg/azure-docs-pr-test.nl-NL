---
title: aaaConfigure end tooend SSL met Azure Application Gateway | Microsoft Docs
description: "Dit artikel wordt beschreven hoe tooconfigure tooend SSL met Application Gateway met Azure Resource Manager PowerShell beëindigen"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: e6d80a33-4047-4538-8c83-e88876c8834e
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: 7c280478e143d309e7665219441cbee8c81d9a80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-end-tooend-ssl-with-application-gateway-using-powershell"></a>Einde tooend SSL configureren met Application Gateway met behulp van PowerShell

## <a name="overview"></a>Overzicht

Een toepassing Gateway ondersteunt eindigen tooend codering van verkeer. Toepassingsgateway doet dit door het Hallo-SSL-verbinding op Hallo application gateway wordt beëindigd. Hallo gateway geldt routeringsregels Hallo toohello verkeer, opnieuw versleutelt hello-pakket en stuurt Hallo pakket toohello juiste back-end op basis van Hallo routeringsregels gedefinieerd. Geen antwoord van de webserver Hallo Hallo doorloopt dezelfde back toohello eindgebruiker verwerken.

Een andere functie die toepassingsgateway ondersteunt aangepaste SSL opties definiëren. Toepassingsgateway ondersteunt uitschakelen Hallo na protocolversie; **TLSv1.0**, **TLSv1.1**, en **TLSv1.2** ook definiëren Hallo die cipher suites toouse en Hallo volgorde van voorkeur.  toolearn meer informatie over de configureerbare opties voor SSL, gaat u naar [SSL overzicht](application-gateway-SSL-policy-overview.md).

> [!NOTE]
> SSL 2.0 en SSL 3.0 zijn standaard uitgeschakeld en kan niet worden ingeschakeld. Ze worden als onveilig beschouwd en zijn niet kunnen toobe gebruikt met Application Gateway.

![afbeelding van scenario][scenario]

## <a name="scenario"></a>Scenario

In dit scenario, leert u hoe een application gateway met toocreate tooend SSL eindigen met behulp van PowerShell.

Dit scenario wordt:

* Maak een resourcegroep met de naam **appgw-rg**
* Maak een virtueel netwerk met de naam **appgwvnet** met een adresruimte van 10.0.0.0/16.
* Maken van twee subnetten aangeroepen **appgwsubnet** en **appsubnet**.
* Maak een kleine toepassing gateway ondersteunende end tooend SSL-versleuteling die limieten SSL-protocollen versies en coderingssuites.

## <a name="before-you-begin"></a>Voordat u begint

tooconfigure end tooend SSL met een application gateway, een certificaat is vereist voor het Hallo-gateway en certificaten zijn vereist voor Hallo back-endservers. Hallo gatewaycertificaat is gebruikte tooencrypt en ontsleutelen Hallo verkeer dat wordt verzonden tooit met SSL. Hallo gatewaycertificaat moet toobe Personal Information Exchange (pfx)-indeling. Deze bestandsindeling kunt Hallo persoonlijke sleutel toobe geëxporteerd die vereist wordt door Hallo application gateway tooperform Hallo versleuteling en ontsleuteling van verkeer.

Voor end moet tooend SSL-versleuteling Hallo back-end goedgekeurde lijst met toepassingsgateway. Dit wordt gedaan door het openbare certificaat van Hallo back-ends toohello toepassingsgateway Hallo uploadt. Dit zorgt ervoor dat toepassingsgateway Hallo communiceert alleen met bekende back-end-exemplaren. Dit verdere beveiligt Hallo end tooend communicatie.

Dit proces wordt beschreven in Hallo stappen te volgen:

## <a name="create-hello-resource-group"></a>Hallo resourcegroep maken

Deze sectie helpt u bij het maken van een resourcegroep met Hallo toepassingsgateway.

### <a name="step-1"></a>Stap 1

Meld u bij tooyour Azure-Account.

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a>Stap 2

Selecteer Hallo abonnement toouse voor dit scenario.

```powershell
Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
```

### <a name="step-3"></a>Stap 3

Maak een resourcegroep (u kunt deze stap overslaan als u een bestaande resourcegroep gebruikt).

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a>Een virtueel netwerk en een subnet voor de toepassingsgateway Hallo maken

Hallo volgende voorbeeld wordt een virtueel netwerk en twee subnets. Eén subnet is gebruikte toohold Hallo toepassingsgateway. Hallo wordt andere subnet gebruikt voor Hallo back-ends hosting Hallo-webtoepassing.

### <a name="step-1"></a>Stap 1

Een adresbereik toewijzen voor Hallo subnet voor Application Gateway zelf hello worden gebruikt.

```powershell
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24
```

> [!NOTE]
> Subnetten geconfigureerd voor application gateway moeten correct worden aangepast. Een application gateway kan worden geconfigureerd voor up too10 exemplaren. Elk exemplaar duurt één IP-adres van Hallo subnet. Te klein van een subnet, kan de uitbreiden van een toepassingsgateway nadelig beïnvloeden.
> 
> 

### <a name="step-2"></a>Stap 2

Een adresbereik toobe gebruikt voor back-endadresgroep Hallo toewijzen.

```powershell
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24
```

### <a name="step-3"></a>Stap 3

Een virtueel netwerk maken met gedefinieerd in de vorige stappen Hallo Hallo-subnetten.

```powershell
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="step-4"></a>Stap 4

Hallo virtueel netwerk resource en subnet resources toobe gebruikt in de volgende stappen uit Hallo ophalen:

```powershell
$vnet = Get-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg
$gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -VirtualNetwork $vnet
$nicSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appsubnet' -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>Een openbaar IP-adres voor de front-endconfiguratie Hallo maken

Maak een openbare IP-resource toobe gebruikt voor toepassingsgateway Hallo. Dit openbare IP-adres wordt gebruikt een volgende stap.

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name 'publicIP01' -Location "West US" -AllocationMethod Dynamic
```

> [!IMPORTANT]
> Toepassingsgateway biedt geen ondersteuning voor Hallo gebruik van een openbaar IP-adres dat is gemaakt met een domein etiket is gedefinieerd. Alleen een openbaar IP-adres met een domeinlabel dynamisch gemaakte wordt ondersteund. Als u een beschrijvende DNS-naam voor de toepassingsgateway Hallo vereist, is het raadzaam toouse een CNAME-record als een alias.

## <a name="create-an-application-gateway-configuration-object"></a>Een configuratieobject voor de toepassingsgateway maken

Alle configuratie-items worden ingesteld voordat u de toepassingsgateway Hallo maakt. Hallo volgt Hallo configuratie-items maken die nodig zijn voor een toepassingsgatewayresource.

### <a name="step-1"></a>Stap 1

Toepassingsgateway een IP-configuratie maken, deze instelling configureert welke subnet Hallo application gateway gebruikt. Wanneer de toepassingsgateway wordt geopend, een IP-adres van de geconfigureerde Hallo subnet opneemt en netwerkverkeer toohello IP-adressen van routes in Hallo backend-IP-adresgroep. Onthoud dat elk exemplaar één IP-adres gebruikt.

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet
```

### <a name="step-2"></a>Stap 2

Maak een front-end-IP-configuratie, deze instelling wordt een persoonlijke of openbare IP-adres toohello front-end van de toepassingsgateway Hallo toegewezen. Hallo stap koppelt Hallo openbaar IP-adres in de voorgaande stap met het front-end-IP-configuratie Hallo Hallo.

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip
```

### <a name="step-3"></a>Stap 3

Hallo backend-IP-adresgroep configureren met Hallo IP-adressen van Hallo back-end-webservers. Deze IP-adressen zijn Hallo IP-adressen die ontvangen netwerkverkeer op Hallo van Hallo front-end-IP-eindpunt binnenkomt. U vervangen Hallo IP-adressen tooadd na uw eigen toepassing IP-adreseindpunten.

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3
```

> [!NOTE]
> Een volledig gekwalificeerde domeinnaam (FQDN) is ook een geldige waarde in plaats van een IP-adres voor de back-endservers Hallo door middel van Hallo - BackendFqdns switch. 

### <a name="step-4"></a>Stap 4

Hallo front-end-IP-poort voor het openbare IP-eindpunt Hallo configureren. Dit is Hallo-poort waarmee gebruikers verbinding maken.

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443
```

### <a name="step-5"></a>Stap 5

Hallo-certificaat voor de toepassingsgateway Hallo configureren. Dit certificaat wordt gebruikt toodecrypt en Hallo-verkeer in de toepassingsgateway Hallo opnieuw versleutelen.

```powershell
$cert = New-AzureRmApplicationGatewaySSLCertificate -Name cert01 -CertificateFile <full path too.pfx file> -Password <password for certificate file>
```

> [!NOTE]
> Dit voorbeeld configureert Hallo gebruikte certificaat voor SSL-verbinding. Hallo-certificaat moet toobe in PFX-indeling en Hallo wachtwoord moet tussen 4 too12 tekens.

### <a name="step-6"></a>Stap 6

Hallo HTTP-listener voor de toepassingsgateway Hallo maken. Hallo front-end-IP-configuratie, poort en SSL-certificaat toouse toewijzen.

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SSLCertificate $cert
```

### <a name="step-7"></a>Stap 7

Upload het Hallo-certificaat toobe gebruikt op Hallo SSL ingeschakeld resources in de back-end.

> [!NOTE]
> Hallo standaard test krijgt Hallo openbare sleutel van Hallo **standaard** SSL-binding op Hallo back-end van IP-adres en vergelijkt Hallo waarde de openbare sleutel toohello waarde de openbare sleutel u hier opgeeft, wordt ontvangen. Hallo opgehaalde openbare sleutel mag niet per se zijn bedoeld Hallo site toowhich verkeersstromen **als** u hostheaders en SNI op Hallo back-end gebruikt. Als u twijfelt, gaat u naar https://127.0.0.1/ op Hallo back-ends van tooconfirm welk certificaat wordt gebruikt voor Hallo **standaard** SSL-binding. Hallo openbare sleutel van deze aanvraag gebruikt in deze sectie. Als u van hostheaders en SNI op HTTPS-bindingen gebruikmaakt en niet u een antwoord en het certificaat van een handmatige browser aanvraag toohttps://127.0.0.1/ op Hallo back-ends ontvangt, moet u een standaard SSL-binding op back-ends van Hallo instellen. Als u niet doet dit, mislukt de tests en Hallo back-end is niet wilt plaatsen.

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile C:\users\gwallace\Desktop\cert.cer
```

> [!NOTE]
> Hallo certificaat dat is opgegeven in deze stap moet Hallo openbare sleutel van het Hallo pfx-certificaat aanwezig is op Hallo back-end. Exporteer Hallo certificaat (geen basiscertificaat Hallo) op Hallo back-endserver in. CER indeling en deze gebruiken in deze stap. Deze stap whitelists Hallo backend met Hallo toepassingsgateway.

### <a name="step-8"></a>Stap 8

Hallo application gateway back-end-HTTP-instellingen configureren. Hallo-certificaat geüpload in de voorgaande stap toohello HTTP-instellingen Hallo toewijzen.

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert
```

### <a name="step-9"></a>Stap 9

Maak een load balancer-routeringsregel waarmee het gedrag van Hallo load balancer worden geconfigureerd. In dit voorbeeld wordt wordt een eenvoudige round robinregel gemaakt.

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

### <a name="step-10"></a>Stap 10

Hallo exemplaargrootte van de toepassingsgateway Hallo configureren.  Hallo beschikbare grootten zijn **standaard\_kleine**, **standaard\_gemiddeld**, en **standaard\_grote**.  Hallo beschikbare waarden zijn, de capaciteit van 1 t/m 10.

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

> [!NOTE]
> Een aantal exemplaren van 1 worden gekozen voor testdoeleinden. Het is belangrijk dat elke instantie onder twee exemplaren tellen tooknow niet wordt gedekt door Hallo SLA en worden daarom niet aanbevolen. Kleine gateways worden gebruikt voor het ontwikkelen testen en niet voor productiedoeleinden toobe.

### <a name="step-11"></a>Stap 11

Hallo SSL beleid toobe gebruikt op Hallo toepassingsgateway configureren. Hallo mogelijkheid tooset minimaal versie biedt ondersteuning voor toepassingsgateway voor SSL-protocol versie.

Hallo zijn volgende waarden een lijst met protocolversies die kunnen worden gedefinieerd.

* **TLSv1_0**
* **TLSv1_1**
* **TLSv1_2**

Sets Hallo minimale protocolversie te**TLSv1_2** en schakelt **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_ SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, en **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** alleen.

```powershell
$SSLPolicy = New-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion TLSv1_2 -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256"
```

## <a name="create-hello-application-gateway"></a>Hallo toepassingsgateway maken

Maak met alle Hallo vorige stappen Hallo Application Gateway. Hallo maken van Hallo gateway is een langdurige proces.

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgateway -SSLCertificates $cert -ResourceGroupName "appgw-rg" -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SSLPolicy $SSLPolicy -AuthenticationCertificates $authcert -Verbose
```

## <a name="limit-ssl-protocol-versions-on-an-existing-application-gateway"></a>SSL-protocol versie op een bestaande toepassingsgateway beperken

Hallo voorgaande stappen nemen u bij het maken van een toepassing met einde tooend SSL- en uitschakelen van bepaalde versies van SSL-protocol. Hallo volgende voorbeeld wordt uitgeschakeld bepaalde beleidsregels SSL op een bestaande toepassingsgateway.

### <a name="step-1"></a>Stap 1

Hallo application gateway tooupdate ophalen.

```powershell
$gw = Get-AzureRmApplicationGateway -Name AdatumAppGateway -ResourceGroupName AdatumAppGatewayRG
```

### <a name="step-2"></a>Stap 2

Definieer een SSL-beleid. In Hallo voorbeeld te volgen, TLSv1.0 TLSv1.1 zijn uitgeschakeld en de coderingssuites Hallo **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256** , **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, en  **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** Hallo enigen toegestaan zijn.

```powershell
Set-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion -PolicyType Custom -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256" -ApplicationGateway $gw

```

### <a name="step-3"></a>Stap 3

Tot slot werkt Hallo-gateway. Het is belangrijk toonote dat deze laatste stap een langlopende taak is. Wanneer dit wordt gedaan, eindigen tooend die SSL op Hallo application gateway is geconfigureerd.

```powershell
$gw | Set-AzureRmApplicationGateway
```

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

Meer informatie over het beperken van Hallo beveiliging van uw webtoepassingen met Web Application Firewall via Application Gateway in via [Web Application Firewall-overzicht](application-gateway-webapplicationfirewall-overview.md)

[scenario]: ./media/application-gateway-end-to-end-SSL-powershell/scenario.png
