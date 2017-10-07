---
title: aaaConfigure SSL-offload - Azure Application Gateway - PowerShell-klassiek | Microsoft Docs
description: In dit artikel bevat instructies toocreate een toepassingsgateway met SSL-offload met behulp van hello Azure klassieke implementatiemodel.
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 63f28d96-9c47-410e-97dd-f5ca1ad1b8a4
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 5cb128015747ed4b71802cf751c80b60634601a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-hello-classic-deployment-model"></a>Een toepassingsgateway voor SSL-offload configureren met behulp van het klassieke implementatiemodel Hallo

> [!div class="op_single_selector"]
> * [Azure Portal](application-gateway-ssl-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-ssl-arm.md)
> * [Azure Classic PowerShell](application-gateway-ssl.md)
> * [Azure CLI 2.0](application-gateway-ssl-cli.md)

Azure Application Gateway kan worden geconfigureerd tooterminate Hallo Secure Sockets Layer (SSL)-sessie op Hallo gateway tooavoid kostbare SSL ontsleuteling taken toohappen op Hallo-webfarm. SSL-offload vereenvoudigt ook Hallo front-end-server instellen en beheren van Hallo-webtoepassing.

## <a name="before-you-begin"></a>Voordat u begint

1. Hallo meest recente versie van hello Azure PowerShell-cmdlets installeren met behulp van Hallo Web Platform Installer. U kunt downloaden en installeren van de meest recente versie Hallo van Hallo **Windows PowerShell** sectie Hallo [pagina Downloads](https://azure.microsoft.com/downloads/).
2. Controleer of u een werkend virtueel netwerk hebt met een geldig subnet. Zorg ervoor dat er geen virtuele machines en cloudimplementaties die van Hallo subnet gebruikmaken zijn. Hallo toepassingsgateway moet afzonderlijk in een virtueel netwerksubnet.
3. Hallo-servers dat u toouse Hallo toepassingsgateway configureert moeten bestaan of hun eindpunten in het virtuele netwerk hello of een openbaar IP-/ VIP-adres hebben.

tooconfigure SSL offload op een toepassingsgateway, Hallo stappen te volgen in Hallo volgorde:

1. [Een toepassingsgateway maken](#create-an-application-gateway)
2. [SSL-certificaten uploaden](#upload-ssl-certificates)
3. [Hallo-gateway configureren](#configure-the-gateway)
4. [De configuratie van een set Hallo-gateway](#set-the-gateway-configuration)
5. [Hallo gateway starten](#start-the-gateway)
6. [Controleer of de status van de gateway Hallo](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a>Een toepassingsgateway maken

Gebruik Hallo-gateway Hallo toocreate `New-AzureApplicationGateway` cmdlet, waarbij Hallo waarden vervangt door uw eigen. Facturering voor Hallo-gateway op dit moment niet worden gestart. Facturering begint met een latere stap Hallo gateway is gestart.

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

toovalidate die Hallo gateway is gemaakt, kunt u Hallo `Get-AzureApplicationGateway` cmdlet.

In voorbeeld Hallo *beschrijving*, *InstanceCount*, en *GatewaySize* zijn optionele parameters. de standaardwaarde voor Hallo *InstanceCount* is 2 en de maximale waarde is 10. de standaardwaarde voor Hallo *GatewaySize* is normaal. Kleine en grote andere beschikbare waarden zijn. *VirtualIPs* en *DnsName* leeg worden weergegeven omdat het Hallo-gateway is nog niet gestart. Deze waarden worden gemaakt nadat Hallo gateway Hallo status actief is.

```powershell
Get-AzureApplicationGateway AppGwTest
```

## <a name="upload-ssl-certificates"></a>SSL-certificaten uploaden

Gebruik `Add-AzureApplicationGatewaySslCertificate` tooupload Hallo-servercertificaat in *pfx* indeling toohello toepassingsgateway. Hallo certificaatnaam is de naam van een gebruiker zijn gekozen en moet uniek zijn binnen de toepassingsgateway Hallo. Dit certificaat is waarnaar wordt verwezen tooby deze naam in alle certificaat beheerbewerkingen op Hallo toepassingsgateway.

Deze volgende voorbeeld toont Hallo-cmdlet Hallo-waarden in Hallo voorbeeld vervangen door uw eigen.

```powershell
Add-AzureApplicationGatewaySslCertificate  -Name AppGwTest -CertificateName GWCert -Password <password> -CertificateFile <full path toopfx file>
```

Vervolgens valideren Hallo-certificaat uploaden. Gebruik Hallo `Get-AzureApplicationGatewayCertificate` cmdlet.

Dit voorbeeld toont Hallo cmdlet op de eerste regel hello, gevolgd door Hallo uitvoer.

```powershell
Get-AzureApplicationGatewaySslCertificate AppGwTest
```

```
VERBOSE: 5:07:54 PM - Begin Operation: Get-AzureApplicationGatewaySslCertificate
VERBOSE: 5:07:55 PM - Completed Operation: Get-AzureApplicationGatewaySslCertificate
Name           : SslCert
SubjectName    : CN=gwcert.app.test.contoso.com
Thumbprint     : AF5ADD77E160A01A6......EE48D1A
ThumbprintAlgo : sha1RSA
State..........: Provisioned
```

> [!NOTE]
> Hallo certificaatwachtwoord heeft toobe tussen 4 too12 tekens, letters of cijfers. Speciale tekens worden niet geaccepteerd.

## <a name="configure-hello-gateway"></a>Hallo-gateway configureren

Een toepassingsgateway configuratie bestaat uit meerdere waarden. Hallo-waarden kunnen worden gekoppeld samen tooconstruct Hallo configuratie.

Hallo-waarden zijn:

* **Back-endserverpool:** Hallo lijst met IP-adressen van Hallo back-endservers. Hallo IP-adressen moeten ofwel deel uitmaken toohello virtueel netwerksubnet ofwel moeten een openbare IP-/ VIP.
* **Back-endserverpoolinstellingen:** elke pool heeft instellingen, zoals voor de poort, het protocol en de op cookies gebaseerde affiniteit. Deze instellingen zijn gebonden tooa servergroep en toegepaste tooall servers binnen de pool Hallo zijn.
* **Front-endpoort:** deze is Hallo openbare poort die in Hallo toepassingsgateway wordt geopend. Verkeer komt binnen via deze poort en vervolgens wordt omgeleid tooone van Hallo back-endservers.
* **Listener:** Hallo listener beschikt over een front-endpoort, een protocol (Http of Https; deze waarden zijn hoofdlettergevoelig), en Hallo SSL-certificaatnaam (als u SSL-offloading configureert).
* **Regel:** Hallo regel verbindt Hallo listener Hallo back-endserverpool en definieert welk verkeer van back-endserver groep Hallo moet gerichte toowhen dit bij een bepaalde listener aankomt. Op dit moment alleen Hallo *basic* regel wordt ondersteund. Hallo *basic* regel is round-robinbelastingverdeling.

**Aanvullende configuratieopmerkingen**

Hallo-protocol in voor de configuratie van SSL-certificaten, **HttpListener** moet ook wijzigen*Https* (hoofdlettergevoelig). Hallo **SslCert** element te toegevoegd**HttpListener** Hello waarde ingesteld toohello dezelfde naam als in Hallo laden van de voorgaande sectie voor SSL-certificaten gebruikt. Hallo front-endpoort moet bijgewerkte too443.

**tooenable cookies gebaseerde affiniteit**: een application gateway kan worden geconfigureerd tooensure is een aanvraag van een clientsessie altijd gerichte toohello dezelfde virtuele machine in de webfarm Hallo. Dit scenario wordt gedaan door het injecteren van een sessiecookie waarmee Hallo gateway toodirect verkeer op de juiste wijze. tooenable cookies gebaseerde affiniteit ingesteld **CookieBasedAffinity** te*ingeschakeld* in Hallo **BackendHttpSettings** element.

U kunt de configuratie maken door het maken van een configuratieobject of met behulp van een XML-configuratiebestand.
uw configuratie met behulp van een configuratie-XML-bestand, gebruikt u tooconstruct Hallo volgende voorbeeld:

**Configuratie-XML-voorbeeld**

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendIPConfigurations />
    <FrontendPorts>
        <FrontendPort>
            <Name>FrontendPort1</Name>
            <Port>443</Port>
        </FrontendPort>
    </FrontendPorts>
    <BackendAddressPools>
        <BackendAddressPool>
            <Name>BackendPool1</Name>
            <IPAddresses>
                <IPAddress>10.0.0.1</IPAddress>
                <IPAddress>10.0.0.2</IPAddress>
            </IPAddresses>
        </BackendAddressPool>
    </BackendAddressPools>
    <BackendHttpSettingsList>
        <BackendHttpSettings>
            <Name>BackendSetting1</Name>
            <Port>80</Port>
            <Protocol>Http</Protocol>
            <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        </BackendHttpSettings>
    </BackendHttpSettingsList>
    <HttpListeners>
        <HttpListener>
            <Name>HTTPListener1</Name>
            <FrontendPort>FrontendPort1</FrontendPort>
            <Protocol>Https</Protocol>
            <SslCert>GWCert</SslCert>
        </HttpListener>
    </HttpListeners>
    <HttpLoadBalancingRules>
        <HttpLoadBalancingRule>
            <Name>HttpLBRule1</Name>
            <Type>basic</Type>
            <BackendHttpSettings>BackendSetting1</BackendHttpSettings>
            <Listener>HTTPListener1</Listener>
            <BackendAddressPool>BackendPool1</BackendAddressPool>
        </HttpLoadBalancingRule>
    </HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

## <a name="set-hello-gateway-configuration"></a>De configuratie van een set Hallo-gateway

Vervolgens stelt u de toepassingsgateway Hallo. U kunt Hallo `Set-AzureApplicationGatewayConfig` cmdlet met een configuratieobject of met een XML-configuratiebestand.

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

## <a name="start-hello-gateway"></a>Hallo gateway starten

Zodra het Hallo-gateway is geconfigureerd, gebruikt u Hallo `Start-AzureApplicationGateway` cmdlet toostart Hallo gateway. Facturering voor een application gateway wordt gestart nadat het Hallo-gateway is gestart.

> [!NOTE]
> Hallo `Start-AzureApplicationGateway` cmdlet toofinish too15-20 minuten kan duren.
>
>

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-hello-gateway-status"></a>Controleer of de status van de gateway Hallo

Gebruik Hallo `Get-AzureApplicationGateway` cmdlet toocheck Hallo status van Hallo-gateway. Als `Start-AzureApplicationGateway` is voltooid in de vorige stap Hallo *status* moet worden uitgevoerd, en *VirtualIPs* en *DnsName* geldige waarden.

Dit voorbeeld wordt een application gateway die wordt weergegeven, wordt uitgevoerd, en is klaar tootake verkeer.

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
Name          : AppGwTest2
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Running
VirtualIPs    : {23.96.22.241}
DnsName       : appgw-4c960426-d1e6-4aae-8670-81fd7a519a43.cloudapp.net
```

## <a name="next-steps"></a>Volgende stappen

Als u meer informatie wilt over de algemene opties voor load balancing, raadpleegt u:

* [Azure Load Balancer](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/)

