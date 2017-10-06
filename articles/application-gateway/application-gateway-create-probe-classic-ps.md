---
title: een aangepaste test - Azure Application Gateway - PowerShell-klassiek aaaCreate | Microsoft Docs
description: Meer informatie over hoe toocreate een aangepaste test voor Application Gateway met behulp van PowerShell in het klassieke implementatiemodel Hallo
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 338a7be1-835c-48e9-a072-95662dc30f5e
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: 68332367c99328bd6456b0c339923765637be986
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-probe-for-azure-application-gateway-classic-by-using-powershell"></a>Maak een aangepaste test voor Azure Application Gateway (klassiek) met behulp van PowerShell

> [!div class="op_single_selector"]
> * [Azure Portal](application-gateway-create-probe-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-probe-ps.md)
> * [Azure Classic PowerShell](application-gateway-create-probe-classic-ps.md)

In dit artikel voegt u een aangepaste test tooan bestaande application gateway met PowerShell. Aangepaste tests zijn handig voor toepassingen die de pagina controle van een specifieke status hebben, of voor toepassingen die een geslaagde reactie op Hallo standaardwebtoepassing geen bieden.

> [!IMPORTANT]
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../azure-resource-manager/resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken. Meer informatie over hoe te[u deze stappen uitvoert met behulp van de Resource Manager-model Hallo](application-gateway-create-probe-ps.md).

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway"></a>Een toepassingsgateway maken

toocreate een toepassingsgateway:

1. Maak een toepassingsgatewayresource.
2. Maak een XML-configuratiebestand of een configuratieobject.
3. Doorvoeren Hallo configuratie toohello nieuw gemaakte toepassingsgatewayresource.

### <a name="create-an-application-gateway-resource-with-a-custom-probe"></a>Een toepassingsgatewayresource maken met een aangepaste test

Gebruik Hallo-gateway Hallo toocreate `New-AzureApplicationGateway` cmdlet, waarbij Hallo waarden vervangt door uw eigen. Facturering voor Hallo-gateway op dit moment niet worden gestart. Facturering begint met een latere stap Hallo gateway is gestart.

Hallo volgende voorbeeld wordt een application gateway met behulp van een virtueel netwerk 'testvnet1' en een subnet met de naam 'subnet 1' genoemd.

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

toovalidate die Hallo gateway is gemaakt, kunt u Hallo `Get-AzureApplicationGateway` cmdlet.

```powershell
Get-AzureApplicationGateway AppGwTest
```

> [!NOTE]
> de standaardwaarde voor Hallo *InstanceCount* is 2 en de maximale waarde is 10. de standaardwaarde voor Hallo *GatewaySize* is normaal. U kunt kiezen tussen een klein, middelgroot en groot.
> 
> 

*VirtualIPs* en *DnsName* leeg worden weergegeven omdat het Hallo-gateway is nog niet gestart. Deze waarden worden gemaakt nadat Hallo gateway Hallo status actief is.

### <a name="configure-an-application-gateway-by-using-xml"></a>Een toepassingsgateway configureren met XML

In Hallo voorbeeld te volgen, gebruiken een XML-bestand tooconfigure alle instellingen voor de toepassingsgateway en ze toohello toepassingsgatewayresource doorvoeren.  

Kopieer Hallo tekst tooNotepad te volgen.

```xml
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
<FrontendIPConfigurations>
    <FrontendIPConfiguration>
        <Name>fip1</Name>
        <Type>Private</Type>
    </FrontendIPConfiguration>
</FrontendIPConfigurations>
<FrontendPorts>
    <FrontendPort>
        <Name>port1</Name>
        <Port>80</Port>
    </FrontendPort>
</FrontendPorts>
<Probes>
    <Probe>
        <Name>Probe01</Name>
        <Protocol>Http</Protocol>
        <Host>contoso.com</Host>
        <Path>/path/custompath.htm</Path>
        <Interval>15</Interval>
        <Timeout>15</Timeout>
        <UnhealthyThreshold>5</UnhealthyThreshold>
    </Probe>
    </Probes>
    <BackendAddressPools>
    <BackendAddressPool>
        <Name>pool1</Name>
        <IPAddresses>
            <IPAddress>1.1.1.1</IPAddress>
            <IPAddress>2.2.2.2</IPAddress>
        </IPAddresses>
    </BackendAddressPool>
</BackendAddressPools>
<BackendHttpSettingsList>
    <BackendHttpSettings>
        <Name>setting1</Name>
        <Port>80</Port>
        <Protocol>Http</Protocol>
        <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        <RequestTimeout>120</RequestTimeout>
        <Probe>Probe01</Probe>
    </BackendHttpSettings>
</BackendHttpSettingsList>
<HttpListeners>
    <HttpListener>
        <Name>listener1</Name>
        <FrontendIP>fip1</FrontendIP>
    <FrontendPort>port1</FrontendPort>
        <Protocol>Http</Protocol>
    </HttpListener>
</HttpListeners>
<HttpLoadBalancingRules>
    <HttpLoadBalancingRule>
        <Name>lbrule1</Name>
        <Type>basic</Type>
        <BackendHttpSettings>setting1</BackendHttpSettings>
        <Listener>listener1</Listener>
        <BackendAddressPool>pool1</BackendAddressPool>
    </HttpLoadBalancingRule>
</HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

Hallo waarden tussen haakjes Hallo voor Hallo configuratie-items bewerken. Hallo-bestand opslaan met de bestandsextensie .xml.

Hallo volgende voorbeeld ziet u hoe een configuration file tooset up Hallo application gateway tooload toouse saldo HTTP-verkeer via de openbare poort 80 en netwerkverkeer tooback-endpoort 80 tussen twee IP-adressen met behulp van een aangepaste test verzenden.

> [!IMPORTANT]
> Hallo protocolitem Http of Https is hoofdlettergevoelig.

Een nieuwe configuratie-item \<Probe\> tooconfigure aangepaste tests wordt toegevoegd.

Hallo-configuratieparameters zijn:

|Parameter|Beschrijving|
|---|---|
|**Naam** |De referentienaam voor aangepaste test. |
* **Protocol** | Protocol dat wordt gebruikt (mogelijke waarden zijn HTTP of HTTPS).|
| **Host** en **pad** | Volledige URL-pad dat wordt opgeroepen door Hallo gateway toodetermine Hallo toepassingsstatus van het Hallo-exemplaar. Als u een http://contoso.com/ website hebt en vervolgens de aangepaste test Hallo kan worden geconfigureerd voor controleert 'http://contoso.com/path/custompath.htm' voor de test toohave geslaagde HTTP-antwoord.|
| **Interval** | Hiermee configureert u Hallo test interval controles in seconden.|
| **Time-out** | Hiermee definieert u Hallo test time-outwaarde voor de controle van een HTTP-antwoord.|
| **UnhealthyThreshold** | aantal mislukte HTTP-antwoorden Hallo nodig tooflag Hallo backend-exemplaar als *slecht*.|

naam van de test Hello wordt verwezen in Hallo \<BackendHttpSettings\> configuratie tooassign welke back-end-pool aangepaste test-instellingen gebruikt.

## <a name="add-a-custom-probe-tooan-existing-application-gateway"></a>Een aangepaste test tooan bestaande toepassingsgateway toevoegen

Veranderende Hallo huidige configuratie van een toepassingsgateway zijn drie stappen vereist: ophalen van huidige XML-configuratiebestand hello, toohave een aangepaste test wijzigen en Hallo-toepassingsgateway met Hallo nieuwe XML-instellingen configureren.

1. Hallo XML-bestand ophalen met behulp van `Get-AzureApplicationGatewayConfig`. Deze cmdlet uitvoer Hallo configuration XML toobe gewijzigd tooadd testinstelling.

  ```powershell
  Get-AzureApplicationGatewayConfig -Name "<application gateway name>" -Exporttofile "<path toofile>"
  ```

1. Hallo XML-bestand openen in een teksteditor. Voeg een `<probe>` sectie na `<frontendport>`.

  ```xml
<Probes>
    <Probe>
        <Name>Probe01</Name>
        <Protocol>Http</Protocol>
        <Host>contoso.com</Host>
        <Path>/path/custompath.htm</Path>
        <Interval>15</Interval>
        <Timeout>15</Timeout>
        <UnhealthyThreshold>5</UnhealthyThreshold>
    </Probe>
</Probes>
  ```

  Voeg in Hallo backendHttpSettings sectie Hallo XML Hallo test naam zoals weergegeven in het volgende voorbeeld Hallo:

  ```xml
    <BackendHttpSettings>
        <Name>setting1</Name>
        <Port>80</Port>
        <Protocol>Http</Protocol>
        <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        <RequestTimeout>120</RequestTimeout>
        <Probe>Probe01</Probe>
    </BackendHttpSettings>
  ```

  Hallo XML-bestand opslaan.

1. Update Hallo toepassingsgateway configuratie met Hallo nieuwe XML-bestand met behulp van `Set-AzureApplicationGatewayConfig`. Deze cmdlet werkt uw toepassingsgateway met een nieuwe configuratie Hallo.

```powershell
Set-AzureApplicationGatewayConfig -Name "<application gateway name>" -Configfile "<path toofile>"
```

## <a name="next-steps"></a>Volgende stappen

Als u tooconfigure Secure Sockets Layer (SSL)-offload wilt, Zie [een toepassingsgateway voor SSL-offload configureren](application-gateway-ssl.md).

Als u wilt dat tooconfigure een toouse application gateway met een interne load balancer, raadpleegt u [een toepassingsgateway maken met een interne load balancer (ILB)](application-gateway-ilb.md).

