---
title: aaaCreate, openen of verwijderen van een toepassingsgateway | Microsoft Docs
description: Deze pagina vindt u instructies toocreate, configureren, start en een Azure-toepassingsgateway verwijderen
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 577054ca-8368-4fbf-8d53-a813f29dc3bc
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 3efef5b49880c9efdafad8b88d4bce5b749b82af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-start-or-delete-an-application-gateway-with-powershell"></a>Een toepassingsgateway maken, openen of verwijderen met PowerShell 

> [!div class="op_single_selector"]
> * [Azure Portal](application-gateway-create-gateway-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-gateway-arm.md)
> * [Azure Classic PowerShell](application-gateway-create-gateway.md)
> * [Azure Resource Manager-sjabloon](application-gateway-create-gateway-arm-template.md)
> * [Azure CLI](application-gateway-create-gateway-cli.md)

Azure Application Gateway is een load balancer in laag 7. Het biedt failover, HTTP-aanvragen routeren tussen verschillende servers, ongeacht of deze op Hallo cloud of on-premises. Application Gateway bevat veel ADC-functies (Application Delivery Controller), waaronder HTTP-taakverdeling, op cookies gebaseerde sessieaffiniteit, SSL-offload (Secure Sockets Layer), aangepaste statustests en ondersteuning voor meerdere locaties. toofind een volledige lijst van ondersteunde functies, gaat u naar [Application Gateway-overzicht](application-gateway-introduction.md)

Dit artikel begeleidt u bij Hallo stappen toocreate, configureren en start een toepassingsgateway verwijderen.

## <a name="before-you-begin"></a>Voordat u begint

1. Hallo meest recente versie van hello Azure PowerShell-cmdlets installeren met behulp van Hallo Web Platform Installer. U kunt downloaden en installeren van de meest recente versie Hallo van Hallo **Windows PowerShell** sectie Hallo [pagina Downloads](https://azure.microsoft.com/downloads/).
2. Als u een bestaand virtueel netwerk hebt, selecteert u een bestaande lege subnet of een nieuw subnet maken in uw bestaande virtuele netwerk uitsluitend voor gebruik met Hallo toepassingsgateway. U kunt geen Hallo application gateway tooa ander virtueel netwerk implementeren dan Hallo resources u van plan bent toodeploy achter Hallo toepassingsgateway tenzij vnet-peering wordt gebruikt. Ga meer toolearn naar [Vnet-Peering](../virtual-network/virtual-network-peering-overview.md)
3. Controleer of u een werkend virtueel netwerk hebt met een geldig subnet. Zorg ervoor dat er geen virtuele machines en cloudimplementaties die van Hallo subnet gebruikmaken zijn. Hallo toepassingsgateway moet afzonderlijk in een virtueel netwerksubnet.
4. Hallo-servers dat u toouse Hallo toepassingsgateway configureert moeten bestaan of hun eindpunten in het virtuele netwerk hello of een openbaar IP-/ VIP-adres hebben.

## <a name="what-is-required-toocreate-an-application-gateway"></a>Wat is vereist toocreate een application gateway?

Wanneer u Hallo gebruikt `New-AzureApplicationGateway` opdracht toocreate Hallo toepassingsgateway geen configuratie ingesteld op dit moment en resource Hallo nieuw gemaakt zijn geconfigureerd met XML of een configuratieobject.

Hallo-waarden zijn:

* **Back-endserverpool:** Hallo lijst met IP-adressen van Hallo back-endservers. Hallo IP-adressen moeten ofwel deel uitmaken toohello virtueel netwerksubnet ofwel moeten een openbare IP-/ VIP.
* **Back-endserverpoolinstellingen:** elke pool heeft instellingen, zoals voor de poort, het protocol en de op cookies gebaseerde affiniteit. Deze instellingen zijn gebonden tooa servergroep en toegepaste tooall servers binnen de pool Hallo zijn.
* **Front-endpoort:** deze is Hallo openbare poort die in Hallo toepassingsgateway wordt geopend. Verkeer komt binnen via deze poort en vervolgens wordt omgeleid tooone van Hallo back-endservers.
* **Listener:** Hallo listener beschikt over een front-endpoort, een protocol (Http of Https; deze waarden zijn hoofdlettergevoelig), en Hallo SSL-certificaatnaam (als u SSL-offloading configureert).
* **Regel:** Hallo regel verbindt Hallo listener Hallo back-endserverpool en definieert welk verkeer van back-endserver groep Hallo moet gerichte toowhen dit bij een bepaalde listener aankomt.

## <a name="create-an-application-gateway"></a>Een toepassingsgateway maken

toocreate een toepassingsgateway:

1. Maak een toepassingsgatewayresource.
2. Maak een XML-configuratiebestand of een configuratieobject.
3. Doorvoeren Hallo configuratie toohello nieuw gemaakte toepassingsgatewayresource.

> [!NOTE]
> Als u voor uw toepassingsgateway een aangepaste test tooconfigure nodig hebt, raadpleegt u [met PowerShell een toepassingsgateway maken met aangepaste tests](application-gateway-create-probe-classic-ps.md). Bekijk [Custom probes and health monitoring](application-gateway-probe-overview.md) (Aangepaste tests en statusbewaking) voor meer informatie.

![Voorbeeldscenario][scenario]

### <a name="create-an-application-gateway-resource"></a>Een toepassingsgatewayresource maken

Gebruik Hallo-gateway Hallo toocreate `New-AzureApplicationGateway` cmdlet, waarbij Hallo waarden vervangt door uw eigen. Facturering voor Hallo-gateway op dit moment niet worden gestart. Facturering begint met een latere stap Hallo gateway is gestart.

Hallo volgende voorbeeld maakt u een toepassingsgateway met behulp van een virtueel netwerk met de naam 'testvnet1' en een subnet met de naam 'subnet 1':

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

*Description*, *InstanceCount* en *GatewaySize* zijn optionele parameters.

toovalidate die Hallo gateway is gemaakt, kunt u Hallo `Get-AzureApplicationGateway` cmdlet.

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
Name          : AppGwTest
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Stopped
VirtualIPs    : {}
DnsName       :
```

> [!NOTE]
> de standaardwaarde voor Hallo *InstanceCount* is 2 en de maximale waarde is 10. de standaardwaarde voor Hallo *GatewaySize* is normaal. U kunt kiezen tussen Small, Medium en Large.

*VirtualIPs* en *DnsName* leeg worden weergegeven omdat het Hallo-gateway is nog niet gestart. Deze worden nadat Hallo gateway Hallo uitvoeringsstatus is gemaakt.

## <a name="configure-hello-application-gateway"></a>Hallo toepassingsgateway configureren

U kunt Hallo toepassingsgateway configureren met XML of een configuratieobject.

### <a name="configure-hello-application-gateway-by-using-xml"></a>Hallo toepassingsgateway configureren met XML

In Hallo voorbeeld te volgen, gebruiken een XML-bestand tooconfigure alle instellingen voor de toepassingsgateway en ze toohello toepassingsgatewayresource doorvoeren.  

#### <a name="step-1"></a>Stap 1

Kopieer Hallo tekst tooNotepad te volgen.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendPorts>
        <FrontendPort>
            <Name>(name-of-your-frontend-port)</Name>
            <Port>(port number)</Port>
        </FrontendPort>
    </FrontendPorts>
    <BackendAddressPools>
        <BackendAddressPool>
            <Name>(name-of-your-backend-pool)</Name>
            <IPAddresses>
                <IPAddress>(your-IP-address-for-backend-pool)</IPAddress>
                <IPAddress>(your-second-IP-address-for-backend-pool)</IPAddress>
            </IPAddresses>
        </BackendAddressPool>
    </BackendAddressPools>
    <BackendHttpSettingsList>
        <BackendHttpSettings>
            <Name>(backend-setting-name-to-configure-rule)</Name>
            <Port>80</Port>
            <Protocol>[Http|Https]</Protocol>
            <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        </BackendHttpSettings>
    </BackendHttpSettingsList>
    <HttpListeners>
        <HttpListener>
            <Name>(name-of-the-listener)</Name>
            <FrontendPort>(name-of-your-frontend-port)</FrontendPort>
            <Protocol>[Http|Https]</Protocol>
        </HttpListener>
    </HttpListeners>
    <HttpLoadBalancingRules>
        <HttpLoadBalancingRule>
            <Name>(name-of-load-balancing-rule)</Name>
            <Type>basic</Type>
            <BackendHttpSettings>(backend-setting-name-to-configure-rule)</BackendHttpSettings>
            <Listener>(name-of-the-listener)</Listener>
            <BackendAddressPool>(name-of-your-backend-pool)</BackendAddressPool>
        </HttpLoadBalancingRule>
    </HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

Hallo waarden tussen haakjes Hallo voor Hallo configuratie-items bewerken. Hallo-bestand opslaan met de bestandsextensie .xml.

> [!IMPORTANT]
> Hallo protocolitem Http of Https is hoofdlettergevoelig.

Hallo volgende voorbeeld ziet u hoe een configuratie toouse tooset up Hallo toepassingsgateway bestand. Hallo voorbeeld load compromis tussen de HTTP-verkeer via de openbare poort 80 en stuurt netwerkverkeer tooback-endpoort 80 tussen twee IP-adressen.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
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

#### <a name="step-2"></a>Stap 2

Vervolgens stelt u de toepassingsgateway Hallo. Gebruik Hallo `Set-AzureApplicationGatewayConfig` cmdlet uit met een XML-configuratiebestand.

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile "D:\config.xml"
```

### <a name="configure-hello-application-gateway-by-using-a-configuration-object"></a>Hallo toepassingsgateway configureren met behulp van een configuration-object

Hallo volgende voorbeeld ziet u hoe tooconfigure toepassingsgateway Hallo met behulp van configuratie-objecten. Alle configuratie-items moeten afzonderlijk worden geconfigureerd en vervolgens toegevoegd tooan application gateway configuration-object. Nadat Hallo configuration-object is gemaakt, gebruikt u Hallo `Set-AzureApplicationGateway` opdracht toocommit Hallo configuratie toohello eerder gemaakte toepassingsgatewayresource.

> [!NOTE]
> Voordat u een waarde tooeach configuration-object toewijst, moet u toodeclare wat voor soort object PowerShell voor opslag gebruikt. Hallo eerste regel toocreate Hallo afzonderlijke items definieert wat `Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model(object name)` worden gebruikt.

#### <a name="step-1"></a>Stap 1

Maak alle afzonderlijke configuratie-items.

Maak Hallo front-end-IP zoals weergegeven in het volgende voorbeeld Hallo.

```powershell
$fip = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration
$fip.Name = "fip1"
$fip.Type = "Private"
$fip.StaticIPAddress = "10.0.0.5"
```

Maak Hallo front-endpoort zoals weergegeven in het volgende voorbeeld Hallo.

```powershell
$fep = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort
$fep.Name = "fep1"
$fep.Port = 80
```

Hallo back-endserverpool maken.

Hallo IP-adressen die zijn toegevoegd toohello back-endserverpool zoals weergegeven in het volgende voorbeeld Hallo definiëren.

```powershell
$servers = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendServerCollection
$servers.Add("10.0.0.1")
$servers.Add("10.0.0.2")
```

Gebruik Hallo $server object tooadd Hallo waarden toohello back-end-pool object ($pool).

```powershell
$pool = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool
$pool.BackendServers = $servers
$pool.Name = "pool1"
```

Hallo back-endserverpoolinstelling maken.

```powershell
$setting = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings
$setting.Name = "setting1"
$setting.CookieBasedAffinity = "enabled"
$setting.Port = 80
$setting.Protocol = "http"
```

Hallo-listener maken.

```powershell
$listener = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener
$listener.Name = "listener1"
$listener.FrontendPort = "fep1"
$listener.FrontendIP = "fip1"
$listener.Protocol = "http"
$listener.SslCert = ""
```

Hallo-regel maken.

```powershell
$rule = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule
$rule.Name = "rule1"
$rule.Type = "basic"
$rule.BackendHttpSettings = "setting1"
$rule.Listener = "listener1"
$rule.BackendAddressPool = "pool1"
```

#### <a name="step-2"></a>Stap 2

Wijs alle afzonderlijke configuratie-items tooan application gateway configuration-object ($appgwconfig).

Hallo front-end-IP-toohello configuratie toevoegen.

```powershell
$appgwconfig = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.ApplicationGatewayConfiguration
$appgwconfig.FrontendIPConfigurations = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration]"
$appgwconfig.FrontendIPConfigurations.Add($fip)
```

Hallo front-endpoort toohello configuratie toevoegen.

```powershell
$appgwconfig.FrontendPorts = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort]"
$appgwconfig.FrontendPorts.Add($fep)
```
Hallo back-endserver groep toohello configuratie toevoegen.

```powershell
$appgwconfig.BackendAddressPools = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool]"
$appgwconfig.BackendAddressPools.Add($pool)
```

Hallo back-end-pool instelling toohello configuratie toevoegen.

```powershell
$appgwconfig.BackendHttpSettingsList = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings]"
$appgwconfig.BackendHttpSettingsList.Add($setting)
```

Hallo-listener toohello configuratie toevoegen.

```powershell
$appgwconfig.HttpListeners = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener]"
$appgwconfig.HttpListeners.Add($listener)
```

Hallo regel toohello configuratie toevoegen.

```powershell
$appgwconfig.HttpLoadBalancingRules = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule]"
$appgwconfig.HttpLoadBalancingRules.Add($rule)
```

### <a name="step-3"></a>Stap 3
Toepassingsgatewayresource van Hallo configuration-object toohello doorvoeren met behulp van `Set-AzureApplicationGatewayConfig`.

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -Config $appgwconfig
```

## <a name="start-hello-gateway"></a>Hallo gateway starten

Zodra het Hallo-gateway is geconfigureerd, gebruikt u Hallo `Start-AzureApplicationGateway` cmdlet toostart Hallo gateway. Facturering voor een application gateway wordt gestart nadat het Hallo-gateway is gestart.

> [!NOTE]
> Hallo `Start-AzureApplicationGateway` cmdlet toofinish too15-20 minuten kan duren.

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-hello-gateway-status"></a>Controleer of de status van de gateway Hallo

Gebruik Hallo `Get-AzureApplicationGateway` cmdlet toocheck Hallo status van Hallo-gateway. Als `Start-AzureApplicationGateway` is voltooid in de vorige stap Hallo *status* moet worden uitgevoerd, en *Vip* en *DnsName* geldige waarden.

Hallo volgende voorbeeld wordt een toepassingsgateway weergegeven die actief is en gereed tootake verkeer dat is bestemd voor `http://<generated-dns-name>.cloudapp.net`.

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
Vip           : 138.91.170.26
DnsName       : appgw-1b8402e8-3e0d-428d-b661-289c16c82101.cloudapp.net
```

## <a name="delete-hello-application-gateway"></a>Hallo toepassingsgateway verwijderen

toodelete hello toepassingsgateway:

1. Gebruik Hallo `Stop-AzureApplicationGateway` cmdlet toostop Hallo gateway.
2. Gebruik Hallo `Remove-AzureApplicationGateway` cmdlet tooremove Hallo gateway.
3. Controleer of deze Hallo-gateway is verwijderd met behulp van Hallo `Get-AzureApplicationGateway` cmdlet.

Hallo volgende voorbeeld ziet u Hallo `Stop-AzureApplicationGateway` cmdlet uit op de eerste regel hello, gevolgd door Hallo uitvoer.

```powershell
Stop-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 9:49:34 PM - Begin Operation: Stop-AzureApplicationGateway
VERBOSE: 10:10:06 PM - Completed Operation: Stop-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   ce6c6c95-77b4-2118-9d65-e29defadffb8
```

Nadat de toepassingsgateway Hallo gestopt is, gebruikt u Hallo `Remove-AzureApplicationGateway` cmdlet tooremove Hallo-service.

```powershell
Remove-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 10:49:34 PM - Begin Operation: Remove-AzureApplicationGateway
VERBOSE: 10:50:36 PM - Completed Operation: Remove-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   055f3a96-8681-2094-a304-8d9a11ad8301
```

tooverify die Hallo service is verwijderd, kunt u Hallo `Get-AzureApplicationGateway` cmdlet. Deze stap is niet vereist.

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: hello gateway does not exist.
.....
```

## <a name="next-steps"></a>Volgende stappen

Als u tooconfigure SSL-offload wilt, Zie [een toepassingsgateway voor SSL-offload configureren](application-gateway-ssl.md).

Als u wilt dat tooconfigure een toouse application gateway met een interne load balancer, raadpleegt u [een toepassingsgateway maken met een interne load balancer (ILB)](application-gateway-ilb.md).

Als u meer informatie wilt over de algemene opties voor load balancing, raadpleegt u:

* [Azure Load Balancer](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/)

[scenario]: ./media/application-gateway-create-gateway/scenario.png
