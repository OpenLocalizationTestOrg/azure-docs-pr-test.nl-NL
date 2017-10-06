---
title: Azure Application Gateway met interne Load Balancer aaaUsing | Microsoft Docs
description: Deze pagina vindt u instructies tooconfigure een Azure-toepassingsgateway met een eindpunt interne met gelijke taakverdeling
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 7403d28e-909f-46a2-b282-43a8e942f53c
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 272ef84a02f92a8521c35aad6f1d9f9bf1675718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb"></a>Een Application Gateway maken met een Internal Load Balancer (ILB)

> [!div class="op_single_selector"]
> * [Azure Classic PowerShell](application-gateway-ilb.md)
> * [Azure Resource Manager PowerShell](application-gateway-ilb-arm.md)

Application Gateway kan worden geconfigureerd met een internetgericht virtueel IP-adres of met een interne eindpunt niet blootgesteld toohello internet, ook wel bekend als interne Load Balancer (ILB)-eindpunt. Hallo-gateway configureren met een ILB is nuttig voor toointernet interne line-of-business-toepassingen niet weergegeven. Het is ook nuttig voor servicecategorieën binnen een toepassing met meerdere lagen, die bevindt zich in een grens niet blootgesteld beveiliging toointernet, maar er wel round-robin verdeling, sessiepersistentie of SSL-beëindiging. Dit artikel begeleidt u bij Hallo stappen tooconfigure een toepassingsgateway met een ILB.

## <a name="before-you-begin"></a>Voordat u begint

1. Installeer de nieuwste versie van Hallo Hallo Web Platform Installer met Azure PowerShell-cmdlets. U kunt downloaden en installeren van de meest recente versie Hallo van Hallo **Windows PowerShell** sectie Hallo [downloadpagina](https://azure.microsoft.com/downloads/).
2. Controleer of u een werkend virtueel netwerk met een geldig subnetmasker.
3. Controleer of u back-endservers in het virtuele netwerk hello of een openbaar IP-/ VIP-adres toegewezen.

een toepassingsgateway toocreate Hallo stappen te volgen in volgorde van Hallo uitvoeren. 

1. [Een toepassingsgateway maken](#create-a-new-application-gateway)
2. [Hallo-gateway configureren](#configure-the-gateway)
3. [De configuratie van een set Hallo-gateway](#set-the-gateway-configuration)
4. [Hallo gateway starten](#start-the-gateway)
5. [Controleer of de gateway Hallo](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a>Een toepassingsgateway maken:

**toocreate hello gateway**, gebruik Hallo `New-AzureApplicationGateway` cmdlet, waarbij Hallo waarden vervangt door uw eigen. Houd er rekening mee dat facturering voor Hallo gateway niet op dit moment wordt gestart. Facturering begint met een latere stap Hallo gateway is gestart.

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

```
VERBOSE: 4:31:35 PM - Begin Operation: New-AzureApplicationGateway 
VERBOSE: 4:32:37 PM - Completed Operation: New-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   55ef0460-825d-2981-ad20-b9a8af41b399
```

**toovalidate** dat Hallo gateway is gemaakt, kunt u Hallo `Get-AzureApplicationGateway` cmdlet. 

In voorbeeld Hallo *beschrijving*, *InstanceCount*, en *GatewaySize* zijn optionele parameters. de standaardwaarde voor Hallo *InstanceCount* is 2 en de maximale waarde is 10. de standaardwaarde voor Hallo *GatewaySize* is normaal. Kleine en grote andere beschikbare waarden zijn. *VIP* en *DnsName* leeg worden weergegeven omdat het Hallo-gateway is nog niet gestart. Deze worden nadat Hallo gateway Hallo uitvoeringsstatus is gemaakt. 

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 4:39:39 PM - Begin Operation:
Get-AzureApplicationGateway VERBOSE: 4:39:40 PM - Completed 
Operation: Get-AzureApplicationGateway
Name: AppGwTest    
Description: 
VnetName: testvnet1 
Subnets: {Subnet-1} 
InstanceCount: 2 
GatewaySize: Medium 
State: Stopped 
VirtualIPs: 
DnsName:
```

## <a name="configure-hello-gateway"></a>Hallo-gateway configureren
Een toepassingsgateway configuratie bestaat uit meerdere waarden. Hallo-waarden kunnen worden gekoppeld samen tooconstruct Hallo configuratie.

Hallo-waarden zijn:

* **Back-end-servergroep:** Hallo lijst met IP-adressen van Hallo back-endservers. Hallo IP-adressen moeten ofwel deel uitmaken toohello VNet subnet, ofwel moeten een openbare IP-/ VIP. 
* **Back-endserverpoolinstellingen:** elke pool heeft instellingen, zoals voor de poort, het protocol en de op cookies gebaseerde affiniteit. Deze instellingen zijn gebonden tooa servergroep en toegepaste tooall servers binnen de pool Hallo zijn.
* **Front-Endpoort:** dit is de openbare poort Hallo in Hallo toepassingsgateway geopend. Het verkeer komt binnen via deze poort en vervolgens wordt omgeleid tooone van Hallo back-endservers.
* **Listener:** Hallo listener beschikt over een front-endpoort, een protocol (Http of Https; deze zijn hoofdlettergevoelig), en Hallo SSL-certificaatnaam (als u SSL-offloading configureert). 
* **Regel:** Hallo regel verbindt Hallo listener Hallo back-end-servergroep en bepaalt welke back-end server groep Hallo verkeer gerichte toowhen dit bij een bepaalde listener aankomt. Op dit moment alleen Hallo *basic* regel wordt ondersteund. Hallo *basic* regel is round-robinbelastingverdeling.

U kunt de configuratie maken door het maken van een configuratieobject of met behulp van een XML-configuratiebestand. tooconstruct uw configuratie met behulp van een XML-configuratiebestand, gebruik Hallo voorbeeld hieronder.

Let op Hallo volgende:

* Hallo *FrontendIPConfigurations* element worden Hallo ILB details relevant zijn voor het configureren van Application Gateway met een ILB beschreven. 
* Hallo Frontend-IP- *Type* too'Private moet worden ingesteld '
* Hallo *StaticIPAddress* toohello gewenst intern IP-adres op welke Hallo gateway verkeer ontvangt moet worden ingesteld. Houd er rekening mee dat Hallo *StaticIPAddress* element is optioneel. Als dat niet is ingesteld, een beschikbare interne IP-adres uit Hallo geïmplementeerd subnet is gekozen. 
* waarde van Hallo Hallo *naam* opgegeven element in *FrontendIPConfiguration* moet worden gebruikt in Hallo HTTPListener van *FrontendIP* element toorefer toohello FrontendIPConfiguration.
  
  **Configuratie-XML-voorbeeld**
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendIPConfigurations>
        <FrontendIPConfiguration>
            <Name>fip1</Name> 
            <Type>Private</Type> 
            <StaticIPAddress>10.0.0.10</StaticIPAddress> 
        </FrontendIPConfiguration>
    </FrontendIPConfigurations>
    <FrontendPorts>
        <FrontendPort>
            <Name>FrontendPort1</Name>
            <Port>80</Port>
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
            <FrontendIP>fip1</FrontendIP>
            <FrontendPort>FrontendPort1</FrontendPort>
            <Protocol>Http</Protocol>
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

```
VERBOSE: 7:54:59 PM - Begin Operation: Set-AzureApplicationGatewayConfig 
VERBOSE: 7:55:32 PM - Completed Operation: Set-AzureApplicationGatewayConfig
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   9b995a09-66fe-2944-8b67-9bb04fcccb9d
```

## <a name="start-hello-gateway"></a>Hallo gateway starten

Zodra het Hallo-gateway is geconfigureerd, gebruikt u Hallo `Start-AzureApplicationGateway` cmdlet toostart Hallo gateway. Facturering voor een application gateway wordt gestart nadat het Hallo-gateway is gestart. 

> [!NOTE]
> Hallo `Start-AzureApplicationGateway` cmdlet toocomplete too15-20 minuten kan duren. 
> 
> 

```powershell
Start-AzureApplicationGateway AppGwTest 
```

```
VERBOSE: 7:59:16 PM - Begin Operation: Start-AzureApplicationGateway 
VERBOSE: 8:05:52 PM - Completed Operation: Start-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   fc592db8-4c58-2c8e-9a1d-1c97880f0b9b
```

## <a name="verify-hello-gateway-status"></a>Controleer of de status van de gateway Hallo

Gebruik Hallo `Get-AzureApplicationGateway` cmdlet toocheck Hallo status van gateway. Als `Start-AzureApplicationGateway` is voltooid in de vorige stap hello, Hallo status moet worden *met*, en Hallo Vip en DnsName moet geldige vermeldingen hebben. Dit voorbeeld toont Hallo cmdlet op de eerste regel hello, gevolgd door Hallo uitvoer. In dit voorbeeld Hallo gateway wordt uitgevoerd en is klaar tootake verkeer. 

> [!NOTE]
> Hallo application gateway is geconfigureerd tooaccept-verkeer bij Hallo ILB-eindpunt van de 10.0.0.10 geconfigureerd in dit voorbeeld.

```powershell
Get-AzureApplicationGateway AppGwTest 
```

```
VERBOSE: 8:09:28 PM - Begin Operation: Get-AzureApplicationGateway 
VERBOSE: 8:09:30 PM - Completed Operation: Get-AzureApplicationGateway
Name          : AppGwTest
Description   : 
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Running
VirtualIPs    : {10.0.0.10}
DnsName       : appgw-b2a11563-2b3a-4172-a4aa-226ee4c23eed.cloudapp.net
```

## <a name="next-steps"></a>Volgende stappen
Als u meer informatie wilt over de algemene opties voor load balancing, raadpleegt u:

* [Azure Load Balancer](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/)

