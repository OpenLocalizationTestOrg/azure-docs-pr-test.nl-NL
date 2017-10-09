---
title: aaaHealth bewaken in Service Fabric | Microsoft Docs
description: Een inleiding toohello Azure Service Fabric voor health monitoring model biedt bewaking van Hallo-cluster en de toepassingen en services.
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: 1d979210-b1eb-4022-be24-799fd9d8e003
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: oanapl
ms.openlocfilehash: 904f36374ca6ca7e4caa1d43c92584e7e4c50087
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooservice-fabric-health-monitoring"></a>Inleiding tooService Fabric-statuscontrole
Azure Service Fabric introduceert een statusmodel waarmee de uitgebreide, flexibele en uitbreidbare statusevaluatie en rapportage. Hallo model kunnen near-realtime bewaking van Hallo status van Hallo-cluster en Hallo-services in deze wordt uitgevoerd. Kunt u eenvoudig verkrijgen van informatie en corrigeer eventuele problemen voordat ze trapsgewijs en grote storingen veroorzaken. In typische model Hallo services verzenden rapporten op basis van hun lokale weergaven en dat informatie wordt geaggregeerd tooprovide weergave met een algemene clusterniveau.

Service Fabric-onderdelen gebruiken deze uitgebreide health model tooreport hun huidige status. U kunt Hallo van hetzelfde mechanisme tooreport de status van uw toepassingen. Als u investeert in de status van hoge kwaliteit rapportage die uw aangepaste voorwaarden worden vastgelegd, kunt u detecteren en veel gemakkelijker problemen oplossen voor uw toepassing uitgevoerd.

Hallo die volgende Microsoft Virtual Academy video wordt ook beschreven Hallo Service Fabric-statusmodel en hoe deze wordt gebruikt:<center><a target="_blank" href="https://mva.microsoft.com/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tevZw56yC_1906218965">
<img src="./media/service-fabric-health-introduction/HealthIntroVid.png" WIDTH="360" HEIGHT="244">
</a></center>

> [!NOTE]
> We Hallo health subsysteem tooaddress nodig voor upgrades van de bewaakte gestart. Service Fabric bevat bewaakte toepassing en de cluster-upgrades die volledige beschikbaarheid, niets uitvaltijd en toono met minimale tussenkomst van de gebruiker waarborgen. deze doelstellingen, Hallo upgrade controleert de status op basis van tooachieve upgrade beleidsregels hebt geconfigureerd. Een upgrade kunt doorgaan alleen wanneer de status respecteert de gewenste drempelwaarden. Anders Hallo upgrade wordt ofwel automatisch teruggedraaid of onderbroken toogive beheerders een kans toofix Hallo problemen. toolearn meer informatie over toepassingsupgrades, Zie [in dit artikel](service-fabric-application-upgrade.md).
> 
> 

## <a name="health-store"></a>Health store
Hallo health store houdt health-gerelateerde informatie over entiteiten in Hallo cluster voor eenvoudig ophalen en evalueren. Deze is geïmplementeerd als een Service Fabric stateful service tooensure hoge beschikbaarheid en schaalbaarheid persistent. Hallo health store maakt deel uit van Hallo **fabric: / System** toepassing, en is beschikbaar wanneer Hallo cluster actief is en wordt uitgevoerd.

## <a name="health-entities-and-hierarchy"></a>De statusentiteiten en -hiërarchie
Hallo health entiteiten zijn georganiseerd in een logische hiërarchie waarmee interacties en afhankelijkheden tussen verschillende entiteiten wordt vastgelegd. Hallo health store worden automatisch de statusentiteiten en hiërarchie gebaseerd op rapporten ontvangen van Service Fabric-onderdelen bouwt.

Hallo health entiteiten mirror Hallo Service Fabric-entiteiten. (Bijvoorbeeld **health Toepassingsentiteit** overeenkomt met een toepassingsexemplaar geïmplementeerd in Hallo cluster terwijl **health knooppunt entiteit** overeenkomt met een Service Fabric clusterknooppunt.) Hallo health hiërarchie worden vastgelegd Hallo interacties van Hallo systeementiteiten en vormt de basis Hallo voor geavanceerde health evaluatie. U kunt meer informatie over belangrijke concepten voor Service Fabric in [technisch overzicht van Service Fabric](service-fabric-technical-overview.md). Zie voor meer informatie over de toepassing [Service Fabric-toepassingsmodel](service-fabric-application-model.md).

Hallo health entiteiten en hiërarchie toestaan Hallo cluster en toepassingen toobe effectief gerapporteerde fouten opgespoord en bewaakt. Hallo-statusmodel biedt een nauwkeurige *gedetailleerde* weergave van de status van Hallo Hallo veel bewegende stukken in Hallo-cluster.

![Health-entiteiten.][1]
Hallo health entiteiten, geordend in een hiërarchie op basis van relaties bovenliggend-onderliggend.

[1]: ./media/service-fabric-health-introduction/servicefabric-health-hierarchy.png

Hallo health entiteiten zijn:

* **Cluster**. Vertegenwoordigt de status Hallo van een Service Fabric-cluster. Statusrapporten cluster beschrijven voorwaarden die invloed hebben op het hele cluster Hallo. Deze voorwaarden invloed hebben op meerdere entiteiten in Hallo cluster of Hallo cluster zelf. Op basis van Hallo voorwaarde, beperken niet Hallo Rapportagefout Hallo probleem tooone of slecht onderliggende items meer. Voorbeelden zijn Hallo brain van Hallo cluster splitsen vanwege toonetwork partitioneren of communicatie problemen.
* **Knooppunt**. Vertegenwoordigt de status Hallo van een Service Fabric-knooppunt. Statusrapporten knooppunt beschreven voorwaarden die invloed hebben op Hallo knooppunt functionaliteit. Ze doorgaans invloed op alle Hallo geïmplementeerd entiteiten die zijn uitgevoerd. Voorbeelden zijn knooppunt geen schijfruimte meer (of andere eigenschappen van alle computers, zoals geheugen, verbindingen) en wanneer een knooppunt niet actief is. Hallo knooppunt entiteit wordt geïdentificeerd door de naam van het knooppunt hello (tekenreeks).
* **Toepassing**. Vertegenwoordigt de status Hallo van de instantie van een toepassing in Hallo cluster wordt uitgevoerd. Toepassingsstatus rapporten voorwaarden die invloed hebben op Hallo Beschrijf algemene status van de toepassing hello. Ze kunnen niet worden teruggebracht naar beneden tooindividual onderliggende elementen (services of geïmplementeerde toepassingen). Voorbeelden zijn Hallo end-to-end interactie tussen verschillende services in de toepassing hello. Hallo Toepassingsentiteit wordt geïdentificeerd door de naam van de toepassing hello (URI).
* **Service**. Vertegenwoordigt de status Hallo van een service in Hallo cluster wordt uitgevoerd. Servicestatus rapporten voorwaarden die invloed hebben op Hallo Beschrijf algemene status van het Hallo-service. Hallo Rapportagefout kan niet afbakenen Hallo probleem tooan slecht partitie of replica's. Voorbeelden zijn een serviceconfiguratie (zoals poort of een externe bestandsshare) die wordt veroorzaakt door problemen voor alle partities. Hallo service entiteit wordt geïdentificeerd door de naam van de service hello (URI).
* **Partitie**. Vertegenwoordigt de status Hallo van een service-partitie. Statusrapporten partitie worden voorwaarden die invloed hebben op de hele replicaset Hallo beschreven. Voorbeelden zijn wanneer Hallo aantal replica's lager dan het aantal doel is en wanneer een partitie is sprake van quorumverlies. Hallo partitie entiteit wordt geïdentificeerd door Hallo partitie-ID (GUID).
* **Replica**. Hallo-status van de replica van een stateful service of een staatloze service-exemplaar vertegenwoordigt. Hallo-replica is Hallo kleinste eenheid die watchdogs en onderdelen van het systeem kunnen worden weergegeven voor een toepassing. Voorbeelden zijn voor stateful services, een primaire replica die bewerkingen toosecondaries en trage replicatie kan niet worden gerepliceerd. Een stateless exemplaar kan ook rapporteren wanneer deze wordt uitgevoerd onvoldoende resources of problemen met de netwerkverbinding heeft. Hallo replica-entiteit wordt geïdentificeerd door Hallo partitie-ID (GUID) en Hallo replica of het exemplaar-ID (long).
* **DeployedApplication**. Vertegenwoordigt de status van Hallo een *toepassing die wordt uitgevoerd op een knooppunt*. Statusrapporten geïmplementeerde toepassing voorwaarden specifieke toohello toepassing beschrijven op Hallo-knooppunt dat niet kan worden teruggebracht tooservice pakketten die zijn geïmplementeerd op Hallo hetzelfde knooppunt. Voorbeelden zijn fouten bij het toepassingspakket kan niet worden gedownload op dat knooppunt en problemen met het instellen van beveiligings-principals van toepassing op Hallo-knooppunt. Hallo geïmplementeerd toepassing wordt aangeduid met de naam van de toepassing (URI) en de naam van het knooppunt (tekenreeks).
* **DeployedServicePackage**. Hallo-status van een servicepakket uitgevoerd op een knooppunt in de cluster Hallo vertegenwoordigt. Beschrijft voorwaarden specifieke tooa servicepakket die geen invloed op Hallo andere servicepakketten op Hallo hetzelfde knooppunt voor Hallo dezelfde toepassing. Voorbeelden zijn een codepakket in Hallo-servicepakket kan niet worden gestart en een configuratiepakket dat kan niet worden gelezen. Hallo geïmplementeerd servicepakket wordt geïdentificeerd door de naam van de toepassing (URI), knooppuntnaam (tekenreeks), service manifest-naam (tekenreeks) en service pakket activerings-ID (tekenreeks).

Hallo granulatie van Hallo statusmodel maakt het eenvoudig toodetect en oplossen van problemen. Bijvoorbeeld als een service niet reageert, is het mogelijk tooreport die Hallo toepassingsexemplaar is beschadigd. Rapportage op dat niveau niet ideaal, echter is, omdat het Hallo-probleem mogelijk zonder dat alle Hallo services binnen die toepassing. Hallo-rapport moet toegepaste toohello slecht service of tooa specifieke onderliggende partitie, als u meer informatie toothat partitie verwijst. Hallo gegevens automatisch verwerkingsinformatie via Hallo hiërarchie en een slechte status partitie is zichtbaar gemaakt op niveau van de service en toepassing. De aggregatie helpt toopinpoint en Hallo hoofdoorzaak van het probleem Hallo meer snel worden opgelost.

Hallo health hiërarchie is samengesteld van relaties bovenliggend-onderliggend. Een cluster bestaat uit de knooppunten en toepassingen. Toepassingen hebben services en toepassingen geïmplementeerd. Geïmplementeerde toepassingen heeft servicepakketten geïmplementeerd. Services hebben partities en elke partitie heeft een of meer replica's. Er is een speciale relatie tussen knooppunten en geïmplementeerde entiteiten. Een knooppunt slecht zoals gemeld door de instantie-systeemonderdeel Hallo Failover Manager service is van invloed op toepassingen Hallo geïmplementeerd, servicepakketten en replica's die zijn geïmplementeerd op.

Hallo health hiërarchie vertegenwoordigt de meest recente toestand Hallo van Hallo systeem op basis van het meest recente statusrapporten hello, die is bijna realtime informatie.
Interne en externe watchdogs kunnen rapporteren op Hallo dezelfde entiteiten op basis van toepassingsspecifieke logica of aangepaste bewaakte voorwaarden. Gebruikersrapporten worden gecombineerd met Hallo systeemrapporten.

Plan tooinvest in hoe tooreport en gereageerd had toohealth tijdens Hallo ontwerpen van een grote cloudservice. Deze vooraf investement maakt Hallo service eenvoudiger toodebug, bewaken en beheren.

## <a name="health-states"></a>Statussen
Service Fabric gebruikt drie health-statussen toodescribe of een entiteit beschadigd of niet is: OK, waarschuwing en fout. Elk rapport verzonden toohello health store moet een van deze statussen opgeven. resultaat van evaluatie van Hallo health is een van deze statussen.

Hallo mogelijk [statussen](https://docs.microsoft.com/dotnet/api/system.fabric.health.healthstate) zijn:

* **OK**. Hallo entiteit is in orde. Er zijn geen bekende problemen die zijn gerapporteerd bij het of het onderliggende (indien van toepassing).
* **Waarschuwing**. Hallo entiteit heeft enkele problemen, maar deze nog steeds correct kan werken. Bijvoorbeeld, treedt vertraging, maar ze zorgen niet voor eventuele problemen met de functionele nog. In sommige gevallen kan de waarschuwingsvoorwaarde voor Hallo zelf oplossen zonder tussenkomst van de externe. In dergelijke gevallen statusrapporten bewustzijn en bieden inzicht in wat er gebeurt. In andere gevallen kan Hallo waarschuwingsvoorwaarde afnemen in een ernstig probleem zonder tussenkomst van de gebruiker.
* **Fout**. Hallo entiteit is beschadigd. Actie moet worden gehouden worden toofix Hallo status van de entiteit hello, omdat deze niet juist werken.
* **Onbekende**. Hallo entiteit bestaat niet in Hallo health store. Dit resultaat kan worden verkregen van Hallo gedistribueerde query's die samen de resultaten van meerdere onderdelen. Bijvoorbeeld, Hallo get knooppunt lijstquery gaat te**FailoverManager**, **ClusterManager**, en **HealthManager**; ophalen van de toepassing lijstquery gaat te **ClusterManager** en **HealthManager**. Deze query's samenvoegen resultaten van meerdere onderdelen van het systeem. Als onderdeel van een andere een entiteit die niet aanwezig zijn in health store retourneert, hello samengevoegde resultaat bevat een onbekende status. Een entiteit is niet in de store omdat statusrapporten nog niet zijn verwerkt of Hallo entiteit na verwijdering is opgeschoond.

## <a name="health-policies"></a>Statusbeleid
Hallo health store geldt health beleid toodetermine of een entiteit in orde op basis van de rapporten ervan en de onderliggende items is.

> [!NOTE]
> Statusbeleid kunnen worden opgegeven in het clustermanifest hello (voor cluster en het knooppunt statusevaluatie) of in het toepassingsmanifest hello (voor toepassingsevaluatie en alle onderliggende). Health evaluatie aanvragen kunnen ook worden doorgegeven in aangepaste evaluatie statusbeleid alleen voor deze evaluatie gebruikt worden.
> 
> 

Standaard geldt Service Fabric strikte regels (alles wat u moet zich in orde) voor het Hallo-hiërarchische relatie bovenliggend-onderliggend. Zelfs een Hallo onderliggende items heeft een slechte gebeurtenis, Hallo bovenliggende worden beschouwd als niet in orde.

### <a name="cluster-health-policy"></a>Cluster statusbeleid
Hallo [cluster statusbeleid](https://docs.microsoft.com/dotnet/api/system.fabric.health.clusterhealthpolicy) gebruikte tooevaluate Hallo cluster health statussen knooppunt en de status is. Hallo-beleid kan worden gedefinieerd in het clustermanifest Hallo. Als niet aanwezig is, wordt het standaardbeleid hello (nul verdragen fouten) gebruikt.
Hallo cluster statusbeleid bevat:

* [ConsiderWarningAsError](https://docs.microsoft.com/dotnet/api/system.fabric.health.clusterhealthpolicy.considerwarningaserror). Hiermee geeft u op of tootreat waarschuwing health als fouten tijdens de statusevaluatie. Standaard: false.
* [MaxPercentUnhealthyApplications](https://docs.microsoft.com/dotnet/api/system.fabric.health.clusterhealthpolicy.maxpercentunhealthyapplications). Hiermee geeft u maximaal Hallo verdragen percentage van de toepassingen die niet in orde zijn mag voordat het Hallo-cluster wordt beschouwd als fout.
* [MaxPercentUnhealthyNodes](https://docs.microsoft.com/dotnet/api/system.fabric.health.clusterhealthpolicy.maxpercentunhealthynodes). Hiermee geeft u maximaal Hallo verdragen percentage van de knooppunten die niet in orde zijn mag voordat het Hallo-cluster wordt beschouwd als fout. In grote clusters sommige knooppunten zijn altijd omlaag of uit voor reparaties, dus dit percentage moet geconfigureerde tootolerate die.
* [Applicationtypehealthpolicymap; deze](https://docs.microsoft.com/dotnet/api/system.fabric.health.clusterhealthpolicy.applicationtypehealthpolicymap). Hallo type health beleid toepassingstoewijzing kan worden gebruikt tijdens cluster health evaluatie toodescribe speciale toepassingstypen. Standaard worden alle toepassingen in een pool geplaatst en geëvalueerd, MaxPercentUnhealthyApplications. Als sommige toepassingtypen anders moeten worden behandeld, kunnen ze worden uitgevoerd buiten de algemene groep Hallo. In plaats daarvan worden ze tegen Hallo percentages die zijn gekoppeld aan de naam van het toepassingstype in kaart Hallo geëvalueerd. Bijvoorbeeld in een cluster zijn er duizenden toepassingen met verschillende typen en enkele exemplaren van een besturingselement toepassing van een speciale toepassingstype. Hallo besturingselement toepassingen moet nooit fout. U kunt globale MaxPercentUnhealthyApplications too20% tootolerate opgeven in sommige gevallen, maar voor Hallo toepassingstype 'ControlApplicationType' hello MaxPercentUnhealthyApplications too0 ingesteld. Als sommige Hallo veel toepassingen niet in orde zijn, maar onder Hallo slecht percentage globale, Hallo cluster wordt geëvalueerd tooWarning. Upgraden van cluster is niet van invloed op een waarschuwingsstatus of andere bewaking geactiveerd op basis van de status fout. Maar zelfs één besturingselement toepassing in fout zouden cluster slechte, die terugdraaifase activeert of Hallo clusterupgrades, afhankelijk van de upgrade Hallo-configuratie wordt onderbroken.
  Voor Hallo toepassingstypen gedefinieerd in Hallo-kaart, worden alle exemplaren van een toepassing genomen buiten Hallo algemene groep van toepassingen. Ze worden geëvalueerd op basis van het totale aantal aanvragen van het type van de toepassing hello hello, Hallo met specifieke MaxPercentUnhealthyApplications van Hallo toewijzen. Alle Hallo rest Hallo toepassingen blijven in de algemene groep Hallo en met MaxPercentUnhealthyApplications worden geëvalueerd.

Hallo volgende voorbeeld is een fragment uit een clustermanifest van de. vermeldingen in de toepassing hello toodefine Typ voorvoegsel Hallo parameternaam met 'ApplicationTypeMaxPercentUnhealthyApplications-', gevolgd door de naam van het toepassingstype Hallo kaart.

```xml
<FabricSettings>
  <Section Name="HealthManager/ClusterHealthPolicy">
    <Parameter Name="ConsiderWarningAsError" Value="False" />
    <Parameter Name="MaxPercentUnhealthyApplications" Value="20" />
    <Parameter Name="MaxPercentUnhealthyNodes" Value="20" />
    <Parameter Name="ApplicationTypeMaxPercentUnhealthyApplications-ControlApplicationType" Value="0" />
  </Section>
</FabricSettings>
```

### <a name="application-health-policy"></a>Statusbeleid voor de toepassing
Hallo [statusbeleid voor de toepassing](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthpolicy) wordt beschreven hoe Hallo evaluatie van gebeurtenissen en onderliggende statussen aggregatie wordt uitgevoerd voor toepassingen en onderliggende items. Het kan worden gedefinieerd in het toepassingsmanifest hello, **ApplicationManifest.xml**, in het toepassingspakket Hallo. Als er geen beleidsregels zijn opgegeven, Service Fabric wordt ervan uitgegaan dat Hallo entiteit slecht wanneer er een statusrapport of een onderliggend element op de status waarschuwing of fout Hallo.
Hallo configureerbare beleidsregels zijn:

* [ConsiderWarningAsError](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthpolicy.considerwarningaserror.aspx). Hiermee geeft u op of tootreat waarschuwing health als fouten tijdens de statusevaluatie. Standaard: false.
* [MaxPercentUnhealthyDeployedApplications](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthpolicy.maxpercentunhealthydeployedapplications). Hiermee geeft u Hallo maximaal toegestaan percentage van de geïmplementeerde toepassingen die beschadigd worden kunnen voordat de toepassing hello wordt beschouwd als fout. Dit percentage wordt berekend door het aantal beschadigde geïmplementeerde toepassingen Hallo delen via Hallo aantal knooppunten dat Hallo toepassingen momenteel zijn geïmplementeerd op in het Hallo-cluster. Hallo berekening rondt af naar boven tootolerate een storing op een klein aantal knooppunten. Percentage standaard: nul.
* [DefaultServiceTypeHealthPolicy](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthpolicy.defaultservicetypehealthpolicy). Hiermee geeft u Hallo standaard service type statusbeleid, die Hallo standaard statusbeleid voor alle servicetypen in de toepassing hello vervangt.
* [Servicetypehealthpolicymap; deze](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthpolicy.servicetypehealthpolicymap). Geeft een overzicht van service statusbeleid per servicetype. Deze beleidsregels vervangen Hallo service type health standaardbeleidsregels voor elk type opgegeven service. Bijvoorbeeld, als een toepassing een servicetype staatloze gateway en een servicetype stateful-engine heeft, kunt u configureren Hallo statusbeleid voor de evaluatie anders. Wanneer u beleid per servicetype opgeeft, kunt u gedetailleerde controle van status van de Hallo van Hallo-service toegang.

### <a name="service-type-health-policy"></a>Statusbeleid voor service type
Hallo [service type statusbeleid](https://docs.microsoft.com/dotnet/api/system.fabric.health.servicetypehealthpolicy) geeft aan hoe tooevaluate en statistische Hallo services en Hallo onderliggende elementen van services. Hallo beleid bevat:

* [MaxPercentUnhealthyPartitionsPerService](https://docs.microsoft.com/dotnet/api/system.fabric.health.servicetypehealthpolicy.maxpercentunhealthypartitionsperservice). Hiermee geeft u Hallo maximaal toegestaan percentage van slecht partities voordat een service wordt beschouwd als niet in orde. Percentage standaard: nul.
* [MaxPercentUnhealthyReplicasPerPartition](https://docs.microsoft.com/dotnet/api/system.fabric.health.servicetypehealthpolicy.maxpercentunhealthyreplicasperpartition). Hiermee geeft u Hallo maximaal toegestaan percentage van slecht replica's voordat u een partitie is in orde beschouwd. Percentage standaard: nul.
* [MaxPercentUnhealthyServices](https://docs.microsoft.com/dotnet/api/system.fabric.health.servicetypehealthpolicy.maxpercentunhealthyservices). Hiermee geeft u Hallo maximaal toegestaan percentage van slecht services voordat de toepassing hello wordt beschouwd als niet in orde. Percentage standaard: nul.

Hallo volgende voorbeeld is een fragment uit een manifest van de toepassing:

```xml
    <Policies>
        <HealthPolicy ConsiderWarningAsError="true" MaxPercentUnhealthyDeployedApplications="20">
            <DefaultServiceTypeHealthPolicy
                   MaxPercentUnhealthyServices="0"
                   MaxPercentUnhealthyPartitionsPerService="10"
                   MaxPercentUnhealthyReplicasPerPartition="0"/>
            <ServiceTypeHealthPolicy ServiceTypeName="FrontEndServiceType"
                   MaxPercentUnhealthyServices="0"
                   MaxPercentUnhealthyPartitionsPerService="20"
                   MaxPercentUnhealthyReplicasPerPartition="0"/>
            <ServiceTypeHealthPolicy ServiceTypeName="BackEndServiceType"
                   MaxPercentUnhealthyServices="20"
                   MaxPercentUnhealthyPartitionsPerService="0"
                   MaxPercentUnhealthyReplicasPerPartition="0">
            </ServiceTypeHealthPolicy>
        </HealthPolicy>
    </Policies>
```

## <a name="health-evaluation"></a>De statusevaluatie
Gebruikers en geautomatiseerde services kunnen de status voor een entiteit op elk gewenst moment evalueren. tooevaluate van een entiteit health, Hallo health store aggregeert alle health rapporten over Hallo entiteit en evalueert alle onderliggende (indien van toepassing). Hallo health aggregatie algoritme maakt gebruik van statusbeleid die opgeeft hoe tooevaluate systeemstatusrapporten en hoe tooaggregate onderliggende statussen (indien van toepassing).

### <a name="health-report-aggregation"></a>Aggregatie van Health-rapport
Een entiteit kan meerdere statusrapporten verzonden door verschillende rapporteurs (onderdelen van het systeem of watchdogs) op verschillende eigenschappen hebben. Hallo aggregatie gebruikt Hallo gekoppeld statusbeleid, met name ConsiderWarningAsError lid is van toepassing hello of cluster statusbeleid. ConsiderWarningAsError geeft aan hoe tooevaluate waarschuwingen.

Hallo geaggregeerde status wordt geactiveerd Hallo *slechtste* systeemstatusrapporten op Hallo entiteit. Als er ten minste één fout statusrapport, is hello geaggregeerde status een fout opgetreden.

![Aggregatie voor Health rapport met een foutenrapport.][2]

Een health-entiteit die een of meer fout statusrapporten heeft wordt geëvalueerd als de fout. Hallo geldt voor een verlopen statusrapport, ongeacht de status.

[2]: ./media/service-fabric-health-introduction/servicefabric-health-report-eval-error.png

Als er geen foutenrapporten en een of meer waarschuwingen, is hello geaggregeerde status waarschuwing of fout, afhankelijk van Hallo ConsiderWarningAsError beleid vlag.

![Aggregatie voor Health rapport met een rapport van de waarschuwing en ConsiderWarningAsError false.][3]

Aggregatie voor het rapport met een rapport van de waarschuwing en ConsiderWarningAsError Health ingesteld toofalse (standaard).

[3]: ./media/service-fabric-health-introduction/servicefabric-health-report-eval-warning.png

### <a name="child-health-aggregation"></a>Onderliggende health aggregatie
Hallo weerspiegelt cumulatieve status van een entiteit Hallo onderliggende statussen (indien van toepassing). Hallo-algoritme voor het verzamelen van statussen onderliggende hello health beleidsregels die van toepassing op basis van het entiteitstype Hallo gebruikt.

![Onderliggende entiteiten health aggregatie.][4]

Onderliggende aggregatie op basis van het statusbeleid.

[4]: ./media/service-fabric-health-introduction/servicefabric-health-hierarchy-eval.png

Nadat het Hallo health store heeft alle Hallo onderliggende geëvalueerd, aggregeert het hun statussen op basis van maximumpercentage van slecht kinderen Hallo geconfigureerd. Dit percentage wordt overgenomen uit op basis van de entiteit en het onderliggende type Hallo Hallo-beleid.

* Als alle onderliggende items OK statussen hebt, is Hallo onderliggende geaggregeerd status in orde.
* Als de onderliggende elementen OK en statussen van de waarschuwing hebt, wordt de status van de Hallo-onderliggende geaggregeerd waarschuwing.
* Als er onderliggende elementen met fout statussen die bieden geen ondersteuning voor Hallo maximaal toegestaan percentage van slecht kinderen, is hello geaggregeerde status een fout opgetreden.
* Als Hallo kinderen fout statussen opzicht Hello maximaal toegestaan percentage van slecht kinderen Hallo wordt de geaggregeerde status waarschuwing.

## <a name="health-reporting"></a>Health rapportage
Onderdelen van het systeem, systeem-Fabric-toepassingen en interne of externe watchdogs kunnen rapporteren Service Fabric-entiteiten. Hallo-rapporteurs maken *lokale* bepalingen van Hallo status van de entiteiten Hallo bewaakt, op basis van Hallo voorwaarden ze bewaken. Ze hoeft geen toolook in de globale status of samenvoegen van gegevens. Hallo gewenste gedrag toohave eenvoudige rapporteurs en geen complexe organismen die toolook op veel dingen tooinfer welke toosend informatie nodig.

toosend health toohello health gegevensarchief, een Rapportagefout moet tooidentify Hallo van invloed op een entiteit en een statusrapport maken. toosend hello rapport, gebruik Hallo [FabricClient.HealthClient.ReportHealth](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.reporthealth) API, rapport health API's beschikbaar worden gesteld op Hallo `Partition` of `CodePackageActivationContext` objecten, PowerShell-cmdlets of REST.

### <a name="health-reports"></a>Statusrapporten
Hallo [statusrapporten](https://docs.microsoft.com/dotnet/api/system.fabric.health.healthreport) bevatten voor elk Hallo entiteiten in de cluster Hallo Hallo volgende informatie:

* **SourceId**. Een tekenreeks die een unieke identificatie van Hallo Rapportagefout van Hallo health gebeurtenis.
* **Entiteit-id**. Identificeert Hallo entiteit waarin Hallo rapport is toegepast. Op basis van Hallo verschilt [entiteitstype](service-fabric-health-introduction.md#health-entities-and-hierarchy):
  
  * Het cluster. Geen.
  * Knooppunt. Naam van knooppunt (tekenreeks).
  * de toepassing. Toepassingsnaam (URI). Hallo-naam van Hallo toepassingsexemplaar geïmplementeerd in Hallo cluster vertegenwoordigt.
  * De service. Service-naam (URI). Vertegenwoordigt de naam Hallo van Hallo service-exemplaar in de cluster Hallo geïmplementeerd.
  * Partitie. Partitie-ID (GUID). Hallo partitie unieke id vertegenwoordigt.
  * De replica. Hallo stateful service replica-ID of Hallo staatloze service-exemplaar-ID (INT64).
  * DeployedApplication. Toepassingsnaam (URI) en de naam van het knooppunt (tekenreeks).
  * DeployedServicePackage. Toepassingsnaam (URI), de naam van het knooppunt (tekenreeks) en de service manifest naam (tekenreeks).
* **De eigenschap**. Een *tekenreeks* (geen vaste opsomming) waarmee Hallo Rapportagefout toocategorize Hallo health gebeurtenis voor een bepaalde eigenschap van entiteit Hallo. Bijvoorbeeld, Rapportagefout A Hallo status van de eigenschap 'Opslag' hello Node01 kan rapporteren en Rapportagefout B Hallo status van de eigenschap 'Connectiviteit' hello Node01 kan rapporteren. Deze rapporten worden in Hallo health store behandeld als afzonderlijke health-gebeurtenissen voor Hallo Node01 entiteit.
* **Beschrijving**. Een tekenreeks waarmee een Rapportagefout tooprovide gedetailleerde informatie over Hallo statusgebeurtenis. **SourceId**, **eigenschap**, en **HealthState** Hallo rapport moet volledig worden beschreven. Hallo beschrijving leesbare informatie over Hallo rapport toegevoegd. de tekst Hello gemakkelijker voor beheerders en gebruikers toounderstand Hallo statusrapport.
* **HealthState**. Een [opsomming](service-fabric-health-introduction.md#health-states) die Hallo-status van Hallo rapport beschrijft. Hallo geaccepteerd waarden zijn OK, waarschuwing en fout.
* **TimeToLive**. Een TimeSpan-waarde die hoe lang Hallo statusrapport aangeeft is geldig. In combinatie met **RemoveWhenExpired**, kunt Hallo health store weten hoe tooevaluate gebeurtenissen verlopen. Standaard Hallo-waarde is oneindig en Hallo rapport permanent ongeldig is.
* **RemoveWhenExpired**. Een Booleaanse waarde. Als tootrue ingesteld, verlopen health Hallo rapport wordt automatisch verwijderd uit health store voor Hallo en Hallo rapport heeft geen invloed op entiteit de statusevaluatie. Gebruikt bij het Hallo-rapport is geldig voor een opgegeven periode slechts eenmaal en Hallo Rapportagefout nodig niet tooexplicitly schakelt u het uit. Het is ook toodelete rapporten uit Hallo health store gebruikt (bijvoorbeeld een watchdog is gewijzigd en stopt met het verzenden van rapporten met vorige bron en de eigenschap). Het verzenden van een rapport met een korte TimeToLive samen met RemoveWhenExpired tooclear van een eerdere status uit Hallo health store. Als Hallo-waarde is ingesteld toofalse, wordt hello verlopen rapport beschouwd als een fout op Hallo de statusevaluatie. Hallo onware waarde signalen toohello health store dat die Hallo-bron moet periodiek verslag voor deze eigenschap. Als dit niet het geval is, moet er iets mis met Hallo watchdog. Hallo watchdog van health wordt door rekening te houden Hallo gebeurtenis als een fout vastgelegd.
* **SequenceNumber**. Een positief geheel getal dat toobe groeiende moet, vertegenwoordigt het Hallo-volgorde van Hallo-rapporten. Deze wordt gebruikt door Hallo store toodetect verlopen statusrapporten dat vertraagd vanwege vertragingen in het netwerk of andere problemen worden ontvangen. Een rapport wordt geweigerd als Hallo volgnummer kleiner dan of gelijk is toohello meest recent toegepast nummer voor Hallo dezelfde entiteits-, bron- en eigenschap. Als deze niet is opgegeven, wordt het volgnummer Hallo automatisch gegenereerd. Dit is nodig tooput in Hallo volgnummer alleen als reporting verloopgebeurtenissen bij statuswijzigingen. In dit geval moet Hallo bron tooremember welke rapporten op deze verzonden en Hallo-informatie voor herstel op failover te houden.

Deze vier onderdelen van informatie--SourceId, entiteits-id-eigenschap en HealthState--zijn vereist voor elke statusrapport. Hallo SourceId tekenreeks is niet toegestaan voor toostart met Hallo voorvoegsel '**System.**', die is gereserveerd voor systeemrapporten. Voor Hallo dezelfde entiteit is er slechts één rapport voor Hallo dezelfde bron- en eigenschap. Meerdere rapporten voor dezelfde bron Hallo en eigenschap overschrijven elkaar op Hallo health clientzijde (als ze in batch worden opgenomen) of op Hallo health store aan clientzijde. Hallo vervanging is gebaseerd op volgnummers; nieuwere rapporten (met hogere volgnummers) vervangt oudere rapporten.

### <a name="health-events"></a>Health-gebeurtenissen
Intern Hallo health store houdt [gebeurtenissen health](https://docs.microsoft.com/dotnet/api/system.fabric.health.healthevent), die alle Hallo gegevens uit het Hallo-rapporten en aanvullende metagegevens bevatten. Hallo metagegevens bevat Hallo tijd Hallo rapport toohello health client is opgegeven en Hallo die het aan de serverzijde Hallo is gewijzigd. Hallo health gebeurtenissen worden geretourneerd door [statusquery's](service-fabric-view-entities-aggregated-health.md#health-queries).

Hallo toegevoegde metagegevens is bevat:

* **SourceUtcTimestamp**. Hallo tijd Hallo rapport kreeg toohello health client (Coordinated Universal Time).
* **LastModifiedUtcTimestamp**. Hallo tijd Hallo rapport voor het laatst is gewijzigd op Hallo serverzijde (Coordinated Universal Time).
* **IsExpired**. Een tooindicate vlag die aangeeft of Hallo rapport is verlopen wanneer Hallo query werd uitgevoerd door Hallo health store. Een gebeurtenis kan zijn verlopen alleen als RemoveWhenExpired ingesteld op false is. Anders Hallo-gebeurtenis niet wordt geretourneerd door de query en wordt verwijderd uit het Hallo-store.
* **LastOkTransitionAt**, **LastWarningTransitionAt**, **LastErrorTransitionAt**. Hallo tijdstip van laatste voor OK/waarschuwing/fout overgangen. Deze velden geven Hallo geschiedenis van Hallo health van statusovergangen voor Hallo-gebeurtenis.

Hallo status overgang velden kunnen worden gebruikt voor slimmer waarschuwingen of 'historische' health gebeurtenisgegevens. Deze inschakelen scenario's zoals:

* Een melding wanneer een eigenschap is al op waarschuwing/fout voor meer dan X minuten. Hallo-voorwaarde voor een bepaalde periode controleren, voorkomt waarschuwingen op tijdelijke omstandigheden. Bijvoorbeeld, een waarschuwing als het Hallo-status heeft meer dan vijf minuten is waarschuwing kan worden vertaald naar (HealthState waarschuwings- en nu - LastWarningTransitionTime == > 5 minuten).
* Melding van de voorwaarden die die zijn gewijzigd in Hallo laatste X minuten. Als een rapport, al fout is voordat Hallo tijd opgegeven, kan worden genegeerd omdat deze al eerder is gesignaleerd.
* Als een eigenschap is schakelen tussen waarschuwingen en fouten, moet u bepalen hoe lang het is niet in orde (dat wil zeggen, niet OK). Bijvoorbeeld, een waarschuwing als Hallo-eigenschap niet in orde meer dan vijf minuten is kan worden vertaald naar (HealthState! = Ok en nu - LastOkTransitionTime > 5 minuten).

## <a name="example-report-and-evaluate-application-health"></a>Voorbeeld: Rapporteren en evalueren van de toepassingsstatus
Hallo volgende voorbeeld verzendt een statusrapport via PowerShell over de toepassing hello **fabric: / WordCount** van Hallo bron **MyWatchdog**. Hallo-statusrapport bevat informatie over Hallo health-eigenschap 'beschikbaarheid' in een foutstatus met oneindige TimeToLive. Vervolgens wordt de status van de toepassing hello, opgevraagd welke retourneert health status fouten en Hallo geaggregeerd gerapporteerd health gebeurtenissen in de lijst Hallo van health-gebeurtenissen.

```powershell
PS C:\> Send-ServiceFabricApplicationHealthReport –ApplicationName fabric:/WordCount –SourceId "MyWatchdog" –HealthProperty "Availability" –HealthState Error

PS C:\> Get-ServiceFabricApplicationHealth fabric:/WordCount -ExcludeHealthStatistics


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            :
                                  Error event: SourceId='MyWatchdog', Property='Availability'.

ServiceHealthStates             :
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Error

                                  ServiceName           : fabric:/WordCount/WordCountWebService
                                  AggregatedHealthState : Ok

DeployedApplicationHealthStates :
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_0
                                  AggregatedHealthState : Ok

                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_2
                                  AggregatedHealthState : Ok

                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_3
                                  AggregatedHealthState : Ok

                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_4
                                  AggregatedHealthState : Ok

                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_1
                                  AggregatedHealthState : Ok

HealthEvents                    :
                                  SourceId              : System.CM
                                  Property              : State
                                  HealthState           : Ok
                                  SequenceNumber        : 360
                                  SentAt                : 3/22/2016 7:56:53 PM
                                  ReceivedAt            : 3/22/2016 7:56:53 PM
                                  TTL                   : Infinite
                                  Description           : Application has been created.
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Error->Ok = 3/22/2016 7:56:53 PM, LastWarning = 1/1/0001 12:00:00 AM

                                  SourceId              : MyWatchdog
                                  Property              : Availability
                                  HealthState           : Error
                                  SequenceNumber        : 131032204762818013
                                  SentAt                : 3/23/2016 3:27:56 PM
                                  ReceivedAt            : 3/23/2016 3:27:56 PM
                                  TTL                   : Infinite
                                  Description           :
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Ok->Error = 3/23/2016 3:27:56 PM, LastWarning = 1/1/0001 12:00:00 AM
```

## <a name="health-model-usage"></a>Gebruik van de gezondheid van modellen
Hallo-statusmodel kan cloudservices en Hallo onderliggende Service Fabric-platform tooscale omdat bewaking en health bepalingen zijn verdeeld over verschillende monitors Hallo binnen Hallo-cluster.
Andere systemen hebben een gecentraliseerde service op clusterniveau Hallo die kan worden geparseerd alle Hallo *mogelijk* nuttige informatie verzonden door de services. Deze aanpak is het lastig hun schaalbaarheid. Deze ook kan geen toocollect specifieke informatie toohelp problemen en potentiële problemen identificeren als de hoofdoorzaak sluiten toohello mogelijk.

Hallo-statusmodel wordt intensief gebruikt voor controle en diagnose, voor het evalueren van de gezondheid van cluster en de toepassing en voor upgrades van de bewaakte. Andere services gebruiken health gegevens tooperform automatisch herstelt, statusgeschiedenis van cluster maken en uitgeven van waarschuwingen op bepaalde voorwaarden.

## <a name="next-steps"></a>Volgende stappen
[Service Fabric-statusrapporten weergeven](service-fabric-view-entities-aggregated-health.md)

[Systeemstatusrapporten gebruiken voor het oplossen van problemen](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)

[Hoe tooreport en controleer health service](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[Aangepaste Service Fabric-statusrapporten toevoegen](service-fabric-report-health.md)

[Controle en diagnose van lokaal services](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Upgrade van de service Fabric-toepassing](service-fabric-application-upgrade.md)

