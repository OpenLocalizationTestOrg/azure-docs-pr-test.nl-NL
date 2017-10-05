---
title: End-to-end SSL configureren met Azure Application Gateway | Microsoft Docs
description: Dit artikel wordt beschreven hoe u complete SSL configureren met een toepassingsgateway met Azure Resource Manager PowerShell
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
ms.openlocfilehash: 6d969d6a0c649c263e1d5bb99bdbceec484cb9a3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="configure-end-to-end-ssl-with-application-gateway-using-powershell"></a>End-to-end SSL configureren met Application Gateway met behulp van PowerShell

## <a name="overview"></a>Overzicht

Application Gateway biedt ondersteuning voor end-to-end-versleuteling van verkeer. Application Gateway doet dit door de SSL-verbinding bij de toepassingsgateway te beëindigen. De gateway past vervolgens de routeringsregels op het verkeer toe, versleutelt het pakket opnieuw en stuurt het pakket naar de juiste back-end op basis van de gedefinieerde routeringsregels. Reacties van de webserver ondergaan hetzelfde proces terug naar de eindgebruiker.

Een andere functie die toepassingsgateway ondersteunt aangepaste SSL opties definiëren. Application Gateway biedt ondersteuning voor het uitschakelen van de volgende protocolversie; **TLSv1.0**, **TLSv1.1**, en **TLSv1.2** als goed definiëren de die coderingssuites moet gebruiken en de volgorde van voorkeur.  Voor meer informatie over de configureerbare opties voor SSL, gaat u naar [SSL overzicht](application-gateway-SSL-policy-overview.md).

> [!NOTE]
> SSL 2.0 en SSL 3.0 zijn standaard uitgeschakeld en kan niet worden ingeschakeld. Deze worden beschouwd als niet-beveiligd en niet kunnen worden gebruikt met Application Gateway.

![afbeelding van scenario][scenario]

## <a name="scenario"></a>Scenario

In dit scenario wordt informatie over het maken van een toepassingsgateway met end-to-end SSL met behulp van PowerShell.

Dit scenario wordt:

* Maak een resourcegroep met de naam **appgw-rg**
* Maak een virtueel netwerk met de naam **appgwvnet** met een adresruimte van 10.0.0.0/16.
* Maken van twee subnetten aangeroepen **appgwsubnet** en **appsubnet**.
* Maak een kleine toepassingsgateway complete SSL-versleuteling ondersteunen die limieten SSL-protocollen versies en coderingssuites.

## <a name="before-you-begin"></a>Voordat u begint

Voor end-to-end SSL met een application gateway configureert, is een certificaat vereist voor de gateway en certificaten zijn vereist voor de back-endservers. Het gatewaycertificaat wordt gebruikt voor het versleutelen en ontsleutelen van het verkeer dat wordt verzonden via SSL. Het gatewaycertificaat moet zich in de indeling Personal Information Exchange (pfx). Deze bestandsindeling kunt u de persoonlijke sleutel exporteerbaar die voor de toepassingsgateway vereist is om uit te voeren voor de versleuteling en ontsleuteling van verkeer.

Voor end-to-end-SSL-codering moet de back-end goedgekeurde lijst met toepassingsgateway. Dit wordt gedaan door het openbare certificaat van de back-ends uploaden naar de toepassingsgateway. Dit zorgt ervoor dat de toepassingsgateway alleen met bekende back-end-exemplaren communiceert. Dit verdere beveiligt de end-to-end communicatie.

Dit proces wordt beschreven in de volgende stappen:

## <a name="create-the-resource-group"></a>De resourcegroep maken

Deze sectie helpt u bij het maken van een resourcegroep met de toepassingsgateway.

### <a name="step-1"></a>Stap 1

Aanmelden bij uw Azure-Account.

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a>Stap 2

Selecteer het abonnement moet worden gebruikt voor dit scenario.

```powershell
Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
```

### <a name="step-3"></a>Stap 3

Maak een resourcegroep (u kunt deze stap overslaan als u een bestaande resourcegroep gebruikt).

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a>Een virtueel netwerk en een subnet maken voor de toepassingsgateway

Het volgende voorbeeld wordt een virtueel netwerk en twee subnets. Eén subnet wordt gebruikt om de toepassingsgateway. Het andere subnet wordt gebruikt voor de back-ends die als host fungeert voor de webtoepassing.

### <a name="step-1"></a>Stap 1

Een adresbereik toewijzen voor het subnet voor de toepassingsgateway zelf worden gebruikt.

```powershell
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24
```

> [!NOTE]
> Subnetten geconfigureerd voor application gateway moeten correct worden aangepast. Een application gateway kan worden geconfigureerd voor maximaal 10 exemplaren. Elk exemplaar duurt één IP-adres van het subnet. Te klein van een subnet, kan de uitbreiden van een toepassingsgateway nadelig beïnvloeden.
> 
> 

### <a name="step-2"></a>Stap 2

Een adresbereik moet worden gebruikt voor de back-end-adresgroep toewijzen.

```powershell
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24
```

### <a name="step-3"></a>Stap 3

Een virtueel netwerk maken met de subnetten die is gedefinieerd in de voorgaande stappen hebt uitgevoerd.

```powershell
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="step-4"></a>Stap 4

Ophalen van de resource van virtueel netwerk en bronnen van het subnet moet worden gebruikt in de volgende stappen:

```powershell
$vnet = Get-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg
$gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -VirtualNetwork $vnet
$nicSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appsubnet' -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a>Een openbaar IP-adres maken voor de front-endconfiguratie

Een openbaar IP-bron moet worden gebruikt voor de toepassingsgateway maken. Dit openbare IP-adres wordt gebruikt een volgende stap.

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name 'publicIP01' -Location "West US" -AllocationMethod Dynamic
```

> [!IMPORTANT]
> Toepassingsgateway biedt geen ondersteuning voor het gebruik van een openbaar IP-adres dat is gemaakt met een domein etiket is gedefinieerd. Alleen een openbaar IP-adres met een domeinlabel dynamisch gemaakte wordt ondersteund. Als u een beschrijvende DNS-naam voor de toepassingsgateway vereist, wordt het aanbevolen een CNAME-record gebruiken als een alias.

## <a name="create-an-application-gateway-configuration-object"></a>Een configuratieobject voor de toepassingsgateway maken

Alle configuratie-items zijn ingesteld voordat u de toepassingsgateway maakt. Volg de onderstaande stappen om de configuratie-items te maken die nodig zijn voor een toepassingsgatewayresource.

### <a name="step-1"></a>Stap 1

Toepassingsgateway een IP-configuratie maken, deze instelling configureert welke subnet maakt gebruik van de toepassingsgateway. Wanneer de toepassingsgateway wordt geopend, neemt over een IP-adres van het geconfigureerde subnet en routeert netwerkverkeer naar de IP-adressen in de back-end-IP-adresgroep. Onthoud dat elk exemplaar één IP-adres gebruikt.

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet
```

### <a name="step-2"></a>Stap 2

Maak een front-end-IP-configuratie, deze instelling wordt een persoonlijke of openbare IP-adres toegewezen aan de front-end van de toepassingsgateway. De volgende stap koppelt het openbare IP-adres in de vorige stap aan de front-end-IP-configuratie.

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip
```

### <a name="step-3"></a>Stap 3

De backend-IP-adresgroep configureren met de IP-adressen van de back-end-webservers. Deze IP-adressen zijn de IP-adressen die het netwerkverkeer ontvangen dat afkomstig is van het front-end-IP-eindpunt. U vervangen de volgende IP-adressen voor het toevoegen van uw eigen toepassing IP-adreseindpunten.

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3
```

> [!NOTE]
> Een volledig gekwalificeerde domeinnaam (FQDN) is ook een geldige waarde in plaats van een IP-adres voor de back-endservers met de schakeloptie - BackendFqdns. 

### <a name="step-4"></a>Stap 4

Configureer de front-end-IP-poort voor het openbare IP-eindpunt. Dit is de poort waarmee gebruikers verbinding maken.

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443
```

### <a name="step-5"></a>Stap 5

Configureer het certificaat voor de toepassingsgateway. Dit certificaat wordt gebruikt om te ontsleutelen en opnieuw versleutelen van het verkeer in de toepassingsgateway.

```powershell
$cert = New-AzureRmApplicationGatewaySSLCertificate -Name cert01 -CertificateFile <full path to .pfx file> -Password <password for certificate file>
```

> [!NOTE]
> Hiermee configureert u het certificaat dat wordt gebruikt voor de SSL-verbinding. Het certificaat moet de indeling .pfx hebben en het wachtwoord moet uit 4-12 tekens bestaan.

### <a name="step-6"></a>Stap 6

De HTTP-listener voor de toepassingsgateway maken. Toewijzen aan de front-end-IP-configuratie, de poort en de SSL-certificaat te gebruiken.

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SSLCertificate $cert
```

### <a name="step-7"></a>Stap 7

Het uploaden van het certificaat moet worden gebruikt op het SSL-resources in de back-end ingeschakeld.

> [!NOTE]
> De standaard-test haalt de openbare sleutel van de **standaard** SSL-binding op de back-end-IP-adres en vergelijkt de waarde voor openbare sleutel wordt ontvangen aan de waarde van de openbare sleutel u hier opgeeft. De opgehaalde openbare sleutel kan niet de gewenste site naar welke verkeersstromen **als** u hostheaders en SNI gebruikt op de back-end. Als u twijfelt, gaat u naar https://127.0.0.1/ op de back-ends om te controleren welk certificaat wordt gebruikt voor de **standaard** SSL-binding. Gebruik de openbare sleutel van de aanvraag die in deze sectie. Als u van hostheaders en SNI op HTTPS-bindingen gebruikmaakt en niet u een antwoord en het certificaat van een aanvraag voor een handmatige browser naar https://127.0.0.1/ op de back-ends ontvangt, moet u een standaard SSL-binding op de back-ends instellen. Als u niet doet dit, mislukt de tests en de back-end is niet wilt plaatsen.

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile C:\users\gwallace\Desktop\cert.cer
```

> [!NOTE]
> Het certificaat dat is opgegeven in deze stap moet de openbare sleutel van het pfx-certificaat dat aanwezig is op de back-end. Exporteer het certificaat (niet het basiscertificaat) geïnstalleerd op de back-endserver in. CER indeling en deze gebruiken in deze stap. Deze stap whitelists de back-end met de toepassingsgateway.

### <a name="step-8"></a>Stap 8

De back-end-HTTP-instellingen voor de toepassingsgateway configureren. Toewijzen van het certificaat dat is geüpload in de vorige stap in de http-instellingen.

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert
```

### <a name="step-9"></a>Stap 9

Maak een load balancer-routeringsregel waarmee het gedrag van de load balancer worden geconfigureerd. In dit voorbeeld wordt wordt een eenvoudige round robinregel gemaakt.

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

### <a name="step-10"></a>Stap 10

Configureer de exemplaargrootte van de toepassingsgateway.  De beschikbare grootten zijn **standaard\_kleine**, **standaard\_gemiddeld**, en **standaard\_grote**.  De capaciteit zijn de beschikbare waarden 1 tot en met 10.

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

> [!NOTE]
> Een aantal exemplaren van 1 worden gekozen voor testdoeleinden. Het is belangrijk te weten dat alle exemplaren onder twee exemplaren niet wordt gedekt door de SLA en worden daarom niet aanbevolen. Er zijn kleine gateways moet worden gebruikt voor het ontwikkelen testen en niet voor productiedoeleinden.

### <a name="step-11"></a>Stap 11

Configureer het SSL-beleid moet worden gebruikt in de toepassingsgateway. Application Gateway ondersteunt de mogelijkheid om in te stellen de minimumversie voor SSL-protocol versie.

De volgende waarden zijn een lijst met protocolversies die kunnen worden gedefinieerd.

* **TLSv1_0**
* **TLSv1_1**
* **TLSv1_2**

De minimale protocolversie stelt op **TLSv1_2** en schakelt **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, en **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** alleen.

```powershell
$SSLPolicy = New-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion TLSv1_2 -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256"
```

## <a name="create-the-application-gateway"></a>De toepassingsgateway maken

Met de bovenstaande stappen maakt u de toepassingsgateway. Het maken van de gateway is een langdurige proces.

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgateway -SSLCertificates $cert -ResourceGroupName "appgw-rg" -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SSLPolicy $SSLPolicy -AuthenticationCertificates $authcert -Verbose
```

## <a name="limit-ssl-protocol-versions-on-an-existing-application-gateway"></a>SSL-protocol versie op een bestaande toepassingsgateway beperken

De voorgaande stappen gaat u door het maken van een toepassing met end-to-end-SSL- en uitschakelen van bepaalde versies van SSL-protocol. Bepaalde beleidsregels SSL op een bestaande toepassingsgateway Hiermee schakelt u het volgende voorbeeld.

### <a name="step-1"></a>Stap 1

Ophalen van de toepassingsgateway om bij te werken.

```powershell
$gw = Get-AzureRmApplicationGateway -Name AdatumAppGateway -ResourceGroupName AdatumAppGatewayRG
```

### <a name="step-2"></a>Stap 2

Definieer een SSL-beleid. In het volgende voorbeeld TLSv1.0 en TLSv1.1 zijn uitgeschakeld en de coderingssuites **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, en **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** zijn de enigen toegestaan.

```powershell
Set-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion -PolicyType Custom -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256" -ApplicationGateway $gw

```

### <a name="step-3"></a>Stap 3

Tot slot werkt de gateway. Het is belangrijk te weten dat deze laatste stap een langlopende taak is. Wanneer deze is voltooid, wordt end-to-end-SSL geconfigureerd in de toepassingsgateway.

```powershell
$gw | Set-AzureRmApplicationGateway
```

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

Meer informatie over het beperken van de beveiliging van uw webtoepassingen met Web Application Firewall via Application Gateway in via [Web Application Firewall-overzicht](application-gateway-webapplicationfirewall-overview.md)

[scenario]: ./media/application-gateway-end-to-end-SSL-powershell/scenario.png
