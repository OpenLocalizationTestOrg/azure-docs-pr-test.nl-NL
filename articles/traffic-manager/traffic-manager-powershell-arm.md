---
title: aaaUsing PowerShell toomanage Traffic Manager in Azure | Microsoft Docs
description: Met behulp van PowerShell voor Traffic Manager met Azure Resource Manager
services: traffic-manager
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: bc247448-1d2e-4104-ac03-42b59ebde065
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: kumud
ms.openlocfilehash: 018c37db63beb82fdad54cfd7e13ab3cb645723a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-powershell-toomanage-traffic-manager"></a>Met behulp van PowerShell toomanage Traffic Manager

Azure Resource Manager is Hallo voorkeursbeheerpunten interface voor services in Azure. Azure Traffic Manager-profielen kunnen worden beheerd met Azure Resource Manager gebaseerde API's en hulpprogramma's.

## <a name="resource-model"></a>Resourcemodel

Azure Traffic Manager is geconfigureerd met behulp van een verzameling instellingen voor een Traffic Manager-profiel wordt aangeroepen. Dit profiel bevat DNS-instellingen, instellingen voor verkeersroutering, eindpunt controle-instellingen en een lijst met de service-eindpunten toowhich verkeer wordt gerouteerd.

Elke Traffic Manager-profiel wordt vertegenwoordigd door een resource van het type 'TrafficManagerProfiles'. Op Hallo REST-API-niveau is Hallo URI voor elk profiel als volgt uit:

    https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Network/trafficManagerProfiles/{profile-name}?api-version={api-version}

## <a name="setting-up-azure-powershell"></a>Instellen van Azure PowerShell

Deze instructies Microsoft Azure PowerShell gebruiken. Hallo volgende artikel wordt uitgelegd hoe tooinstall Azure PowerShell en configureren.

* [Hoe tooinstall Azure PowerShell en configureren](/powershell/azure/overview)

Hallo-voorbeelden in dit artikel wordt ervan uitgegaan dat u een bestaande resourcegroep hebt. U kunt een resourcegroep met behulp van de volgende opdracht Hallo maken:

```powershell
New-AzureRmResourceGroup -Name MyRG -Location "West US"
```

> [!NOTE]
> Azure Resource Manager vereist dat alle resourcegroepen een locatie. Deze locatie wordt gebruikt als Hallo standaard voor resources in die resourcegroep hebt gemaakt. Echter, aangezien Traffic Manager-profiel-resources globaal en niet regionaal zijn, Hallo keuze van de locatie voor resourcegroep heeft geen invloed op Azure Traffic Manager.

## <a name="create-a-traffic-manager-profile"></a>Een Traffic Manager-profiel maken

toocreate Traffic Manager-profiel gebruiken Hallo `New-AzureRmTrafficManagerProfile` cmdlet:

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName contoso -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
```

Hallo volgende tabel beschrijft Hallo parameters:

| Parameter | Beschrijving |
| --- | --- |
| Naam |Hallo-resourcenaam voor Hallo resource van Traffic Manager-profiel. Profielen in Hallo dezelfde resourcegroep moet unieke namen hebben. Deze naam is gescheiden van Hallo DNS-naam gebruikt voor DNS-query's. |
| resourceGroupName |Hallo-naam van Hallo resource groep met Hallo profiel resource. |
| TrafficRoutingMethod |Hiermee geeft u Hallo verkeersroutering methode gebruikt toodetermine welk eindpunt wordt geretourneerd als antwoord een DNS-query. Mogelijke waarden zijn 'Prestaties', 'Gewogen' of 'Prioriteit'. |
| RelativeDnsName |Hiermee geeft u een gedeelte van de Hallo hostname van Hallo DNS-naam op die door dit Traffic Manager-profiel. Deze waarde wordt gecombineerd met Hallo DNS-naam die wordt gebruikt door Azure Traffic Manager tooform Hallo volledig gekwalificeerde domeinnaam (FQDN) van Hallo-profiel. Hallo-waarde van 'contoso' wordt bijvoorbeeld 'contoso.trafficmanager.net'. |
| TTL |Hiermee geeft u Hallo DNS Time-to-Live (TTL), in seconden. Deze TTL informeert Hallo lokale DNS-resolvers en DNS-clients hoe lang toocache DNS-antwoorden voor dit Traffic Manager-profiel. |
| MonitorProtocol |Hiermee geeft u Hallo protocol toouse toomonitor eindpunt health. Mogelijke waarden zijn 'HTTP' en 'HTTPS'. |
| MonitorPort |Hiermee geeft u op Hallo TCP-poort gebruikt toomonitor eindpunt health. |
| MonitorPath |Geeft aan Hallo pad relatief toohello endpoint-domeinnaam tooprobe voor eindpunt health gebruikt. |

Hallo-cmdlet een Traffic Manager-profiel maakt in Azure en een bijbehorende profiel object tooPowerShell retourneert. Hallo profiel bevat geen eindpunten op dit moment geen. Zie voor meer informatie over het toevoegen van eindpunten tooa Traffic Manager-profiel [Traffic Manager-eindpunten toe te voegen](#adding-traffic-manager-endpoints).

## <a name="get-a-traffic-manager-profile"></a>Een Traffic Manager-profiel ophalen

een bestaand Traffic Manager-profiel te object tooretrieve gebruiken Hallo `Get-AzureRmTrafficManagerProfle` cmdlet:

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
```

Deze cmdlet retourneert het object van een Traffic Manager-profiel.

## <a name="update-a-traffic-manager-profile"></a>Een Traffic Manager-profiel bijwerken

Wijzigen van Traffic Manager-profielen, volgt een 3-proces:

1. Met behulp ophalen Hallo profiel `Get-AzureRmTrafficManagerProfile` of gebruik Hallo profiel geretourneerd door `New-AzureRmTrafficManagerProfile`.
2. Hallo-profiel wijzigen. U kunt toevoegen en verwijderen van eindpunten of wijzigt u de parameters voor het eindpunt of profiel. Deze wijzigingen zijn offline bewerkingen. Wijzigt u alleen lokale Hallo-object in het geheugen dat Hallo profiel vertegenwoordigt.
3. Uw wijzigingen met behulp van Hallo `Set-AzureRmTrafficManagerProfile` cmdlet.

Alle eigenschappen van het profiel kunnen worden gewijzigd, met uitzondering van het profiel Hallo RelativeDnsName. toochange Hallo RelativeDnsName, verwijdert u profiel en een nieuw profiel met een nieuwe naam.

Hallo volgende voorbeeld laat zien hoe toochange Hallo TTL van profiel:

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
$profile.Ttl = 300
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

Er zijn drie soorten Traffic Manager-eindpunten:

1. **Azure-eindpunten** zijn services die worden gehost in Azure
2. **Externe eindpunten** worden services die buiten Azure worden gehost
3. **Genest eindpunten** gebruikte tooconstruct genest hiërarchieën van Traffic Manager-profielen. Geneste eindpunten inschakelen geavanceerde verkeersroutering configuraties voor complexe toepassingen.

In alle drie gevallen kunnen eindpunten worden toegevoegd op twee manieren:

1. Met behulp van een proces 3-stappen die hierboven is beschreven. Hallo voordeel van deze methode is dat enkele eindpunt kan worden gewijzigd in één update.
2. Hallo nieuw AzureRmTrafficManagerEndpoint cmdlet gebruikt. Deze cmdlet voegt een eindpunt tooan bestaand Traffic Manager-profiel in één bewerking.

## <a name="adding-azure-endpoints"></a>Azure-eindpunten toevoegen

Azure-eindpunten verwijzen naar services die worden gehost in Azure. Twee soorten Azure-eindpunten worden ondersteund:

1. Azure Web Apps
2. Azure PublicIpAddress-resources (die kunnen worden aangesloten tooa load balancer of een virtuele machine NIC). Hallo PublicIpAddress moet een DNS-naam toegewezen toobe gebruikt in Traffic Manager hebben.

In elk geval:

* Hallo-service is opgegeven met de parameter 'targetResourceId' Hallo van `Add-AzureRmTrafficManagerEndpointConfig` of `New-AzureRmTrafficManagerEndpoint`.
* Hallo 'Target' en 'EndpointLocation' zijn impliciete door Hallo TargetResourceId.
* Hallo opgeven is 'Gewicht' optioneel. Gewicht worden alleen gebruikt als Hallo profiel geconfigureerde toouse Hallo 'Gewogen' verkeersroutering methode. Anders worden genegeerd. Indien opgegeven, is het Hallo-waarde moet een getal tussen 1 en 1000. Hallo-standaardwaarde is '1'.
* Het opgeven van Hallo 'Prioriteit' is optioneel. Prioriteiten worden alleen gebruikt als Hallo profiel geconfigureerde toouse Hallo 'Prioriteit' verkeersroutering methode. Anders worden genegeerd. Geldige waarden liggen tussen 1 too1000 met lagere waarden die wijzen op een hogere prioriteit. Als voor één eindpunt opgegeven, moeten ze worden opgegeven voor alle eindpunten. Als u dit weglaat, wordt standaardwaarden vanaf '1' worden toegepast in Hallo volgorde worden Hallo-eindpunten weergegeven.

### <a name="example-1-adding-web-app-endpoints-using-add-azurermtrafficmanagerendpointconfig"></a>Voorbeeld 1: Toe te voegen met behulp van Web-App-eindpunten`Add-AzureRmTrafficManagerEndpointConfig`

In dit voorbeeld wordt een Traffic Manager-profiel maken en toevoegen van eindpunten van Web-App, met behulp van Hallo `Add-AzureRmTrafficManagerEndpointConfig` cmdlet.

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$webapp1 = Get-AzureRMWebApp -Name webapp1
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp1ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp1.Id -EndpointStatus Enabled
$webapp2 = Get-AzureRMWebApp -Name webapp2
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp2ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp2.Id -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```
### <a name="example-2-adding-a-publicipaddress-endpoint-using-new-azurermtrafficmanagerendpoint"></a>Voorbeeld 2: Toevoegen van een publicIpAddress-eindpunt met`New-AzureRmTrafficManagerEndpoint`

In dit voorbeeld wordt een openbare IP-adres resource toohello Traffic Manager-profiel toegevoegd. Hallo openbaar IP-adres moet een DNS-naam zijn geconfigureerd, en kan worden beide toohello NIC van een virtuele machine of tooa load balancer is gebonden.

```powershell
$ip = Get-AzureRmPublicIpAddress -Name MyPublicIP -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name MyIpEndpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type AzureEndpoints -TargetResourceId $ip.Id -EndpointStatus Enabled
```

## <a name="adding-external-endpoints"></a>Externe eindpunten toevoegen

Traffic Manager maakt gebruik van externe eindpunten toodirect verkeer tooservices buiten Azure worden gehost. Als u met Azure-eindpunten, externe eindpunten kunnen worden toegevoegd, met behulp van `Add-AzureRmTrafficManagerEndpointConfig` gevolgd door `Set-AzureRmTrafficManagerProfile`, of `New-AzureRMTrafficManagerEndpoint`.

Wanneer u externe eindpunten opgeeft:

* Hallo eindpunt domeinnaam moet worden opgegeven met de parameter 'Target' Hallo
* Als Hallo 'Prestaties' verkeersroutering methode wordt gebruikt, is 'EndpointLocation' hello vereist. Anders is optioneel. Hallo-waarde moet een [geldig Azure-regionaam](https://azure.microsoft.com/regions/).
* Hallo 'Gewicht' en 'Prioriteit' zijn optioneel.

### <a name="example-1-adding-external-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a>Voorbeeld 1: Externe eindpunten met toevoegen `Add-AzureRmTrafficManagerEndpointConfig` en`Set-AzureRmTrafficManagerProfile`

In dit voorbeeld wordt een Traffic Manager-profiel maken, twee externe eindpunten toevoegen en Hallo wijzigingen doorvoeren.

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName eu-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointLocation "North Europe" -EndpointStatus Enabled
Add-AzureRmTrafficManagerEndpointConfig -EndpointName us-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-us.contoso.com -EndpointLocation "Central US" -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-adding-external-endpoints-using-new-azurermtrafficmanagerendpoint"></a>Voorbeeld 2: Externe eindpunten met toevoegen`New-AzureRmTrafficManagerEndpoint`

In dit voorbeeld voegen we een bestaand profiel voor externe eindpunt tooan. Hallo-profiel is opgegeven met behulp van namen Hallo profiel en de resource.

```powershell
New-AzureRmTrafficManagerEndpoint -Name eu-endpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointStatus Enabled
```

## <a name="adding-nested-endpoints"></a>'Nested' eindpunten toevoegen

Elke Traffic Manager-profiel geeft één verkeersroutering methode. Er zijn echter scenario's waarvoor meer geavanceerde voor verkeersroutering dan Hallo routering geleverd door een enkele Traffic Manager-profiel. U kunt het Traffic Manager profielen toocombine Hallo voordelen van meer dan één methode voor verkeersroutering nesten. Geneste profielen kunnen u toooverride Hallo standaard Traffic Manager gedrag toosupport grotere en complexere implementaties van toepassingen. Zie voor meer voorbeelden, [genest Traffic Manager-profielen](traffic-manager-nested-profiles.md).

Geneste eindpunten zijn geconfigureerd op Hallo bovenliggende profiel met een specifieke eindpunt-type 'NestedEndpoints'. Bij het opgeven van geneste eindpunten:

* Hallo-eindpunt moet worden opgegeven met de parameter 'targetResourceId' Hallo
* Als Hallo 'Prestaties' verkeersroutering methode wordt gebruikt, is 'EndpointLocation' hello vereist. Anders is optioneel. Hallo-waarde moet een [geldig Azure-regionaam](http://azure.microsoft.com/regions/).
* Hallo 'Gewicht' en 'Prioriteit' zijn optioneel, als voor de Azure-eindpunten.
* Hallo 'MinChildEndpoints'-parameter is optioneel. Hallo-standaardwaarde is '1'. Als het aantal beschikbare eindpunten Hallo kleiner is dan deze drempelwaarde, beschouwt Hallo bovenliggende profiel Hallo onderliggende profiel 'Gedegradeerd' en verkeer toohello andere eindpunten in Hallo bovenliggende profiel zorgt.

### <a name="example-1-adding-nested-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a>Voorbeeld 1: Toe te voegen geneste eindpunten met `Add-AzureRmTrafficManagerEndpointConfig` en`Set-AzureRmTrafficManagerProfile`

In dit voorbeeld we nieuwe Traffic Manager onderliggende en bovenliggende profielen maken, Hallo onderliggende toevoegen als een geneste eindpunt toohello bovenliggende en Hallo wijzigingen doorvoeren.

```powershell
$child = New-AzureRmTrafficManagerProfile -Name child -ResourceGroupName MyRG -TrafficRoutingMethod Priority -RelativeDnsName child -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$parent = New-AzureRmTrafficManagerProfile -Name parent -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName parent -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName child-endpoint -TrafficManagerProfile $parent -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

Voor beknopt alternatief bevat in dit voorbeeld heeft we andere eindpunten toohello onderliggende of bovenliggende profielen niet toevoegen.

### <a name="example-2-adding-nested-endpoints-using-new-azurermtrafficmanagerendpoint"></a>Voorbeeld 2: Geneste eindpunten toevoegen`New-AzureRmTrafficManagerEndpoint`

In dit voorbeeld toevoegen we een bestaand profiel van de onderliggende als een geneste eindpunt tooan bestaande bovenliggende profiel. Hallo-profiel is opgegeven met behulp van namen Hallo profiel en de resource.

```powershell
$child = Get-AzureRmTrafficManagerEndpoint -Name child -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name child-endpoint -ProfileName parent -ResourceGroupName MyRG -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
```

## <a name="update-a-traffic-manager-endpoint"></a>Bijwerken van een Traffic Manager-eindpunt

Er zijn twee manieren tooupdate een bestaand Traffic Manager-eindpunt:

1. Ophalen met behulp Hallo Traffic Manager profiel `Get-AzureRmTrafficManagerProfile`Hallo eindpunt eigenschappen binnen Hallo profiel bijwerken en Hallo wijzigingen met behulp van `Set-AzureRmTrafficManagerProfile`. Deze methode heeft Hallo voordeel kunnen tooupdate wordt meer dan één eindpunt in één bewerking.
2. Hallo Traffic Manager-eindpunt met behulp ophalen `Get-AzureRmTrafficManagerEndpoint`Hallo eindpunt eigenschappen bijwerken en Hallo wijzigingen met behulp van `Set-AzureRmTrafficManagerEndpoint`. Deze methode is eenvoudiger, aangezien hoeven niet te indexeren bij Hallo eindpunten matrix in Hallo-profiel.

### <a name="example-1-updating-endpoints-using-get-azurermtrafficmanagerprofile-and-set-azurermtrafficmanagerprofile"></a>Voorbeeld 1: Bijwerken met behulp van eindpunten `Get-AzureRmTrafficManagerProfile` en`Set-AzureRmTrafficManagerProfile`

In dit voorbeeld wijzigen we Hallo-prioriteit op twee eindpunten in een bestaand profiel.

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG
$profile.Endpoints[0].Priority = 2
$profile.Endpoints[1].Priority = 1
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-updating-an-endpoint-using-get-azurermtrafficmanagerendpoint-and-set-azurermtrafficmanagerendpoint"></a>Voorbeeld 2: Bijwerken van een eindpunt met `Get-AzureRmTrafficManagerEndpoint` en`Set-AzureRmTrafficManagerEndpoint`

In dit voorbeeld wijzigen we Hallo gewicht van één eindpunt in een bestaand profiel.

```powershell
$endpoint = Get-AzureRmTrafficManagerEndpoint -Name myendpoint -ProfileName myprofile -ResourceGroupName MyRG -Type ExternalEndpoints
$endpoint.Weight = 20
Set-AzureRmTrafficManagerEndpoint -TrafficManagerEndpoint $endpoint
```

## <a name="enabling-and-disabling-endpoints-and-profiles"></a>Eindpunten en -profielen inschakelen en uitschakelen

Traffic Manager kunt afzonderlijke eindpunten toobe ingeschakelde en uitgeschakelde, evenals inschakelen en uitschakelen van volledige profielen toestaan.
Deze wijzigingen kunnen worden aangebracht door ophalen/bijwerken/instelling Hallo eindpunt of profiel resources. toostreamline deze algemene bewerkingen worden ook ondersteund via exclusieve cmdlets.

### <a name="example-1-enabling-and-disabling-a-traffic-manager-profile"></a>Voorbeeld 1: Inschakelen en uitschakelen van een Traffic Manager-profiel

tooenable Traffic Manager-profiel gebruiken `Enable-AzureRmTrafficManagerProfile`. Hallo-profiel kan worden opgegeven met behulp van een object van een profiel. Hallo profile-object kan worden doorgegeven via de pijplijn Hallo of met behulp van Hallo '-TrafficManagerProfile' parameter. In dit voorbeeld geeft we Hallo profiel door Hallo profiel en resource groepsnaam.

```powershell
Enable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

toodisable een Traffic Manager-profiel:

```powershell
Disable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

Hallo uitschakelen AzureRmTrafficManagerProfile cmdlet vraagt om bevestiging. Dit bericht kan worden onderdrukt met Hallo '-Force' parameter.

### <a name="example-2-enabling-and-disabling-a-traffic-manager-endpoint"></a>Voorbeeld 2: Inschakelen en uitschakelen van een Traffic Manager-eindpunt

tooenable Traffic Manager-eindpunt gebruik `Enable-AzureRmTrafficManagerEndpoint`. Er zijn twee manieren toospecify Hallo-eindpunt

1. Met behulp van een TrafficManagerEndpoint-object doorgegeven via de pijplijn Hallo of via Hallo '-TrafficManagerEndpoint' parameter
2. Met behulp van eindpuntnaam hello, eindpunttype profielnaam en de naam van resourcegroep:

```powershell
Enable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

Op deze manier toodisable een Traffic Manager-eindpunt:

```powershell
Disable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG -Force
```

Net als bij `Disable-AzureRmTrafficManagerProfile`, Hallo `Disable-AzureRmTrafficManagerEndpoint` cmdlet vraagt om bevestiging. Dit bericht kan worden onderdrukt met Hallo '-Force' parameter.

## <a name="delete-a-traffic-manager-endpoint"></a>Een Traffic Manager-eindpunt verwijderen

tooremove afzonderlijke eindpunten, gebruik Hallo `Remove-AzureRmTrafficManagerEndpoint` cmdlet:

```powershell
Remove-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

Deze cmdlet vraagt om bevestiging. Dit bericht kan worden onderdrukt met Hallo '-Force' parameter.

## <a name="delete-a-traffic-manager-profile"></a>Een Traffic Manager-profiel verwijderen

toodelete Traffic Manager-profiel gebruiken Hallo `Remove-AzureRmTrafficManagerProfile` geven namen Hallo profiel en de resource-cmdlet:

```powershell
Remove-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG [-Force]
```

Deze cmdlet vraagt om bevestiging. Dit bericht kan worden onderdrukt met Hallo '-Force' parameter.

Hallo profiel toobe verwijderd kan ook worden opgegeven met behulp van een object van een profiel:

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
Remove-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile [-Force]
```

Deze reeks kan ook worden doorgesluisd:

```powershell
Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG | Remove-AzureRmTrafficManagerProfile [-Force]
```

## <a name="next-steps"></a>Volgende stappen

[Traffic Manager-controle](traffic-manager-monitoring.md)

[Prestatieoverwegingen voor Traffic Manager](traffic-manager-performance-considerations.md)
