---
title: Service Fabric-Platform niveau Monitoring aaaAzure | Microsoft Docs
description: Meer informatie over platform niveau gebeurtenissen en logboeken gebruikte toomonitor en onderzoeken van Azure Service Fabric-clusters.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/24/2017
ms.author: dekapur
ms.openlocfilehash: f8fb1c8b546e05c517ae12c91906acc04cd6eaa6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="platform-level-event-and-log-generation"></a>Platform niveau gebeurtenis- en logboekbestanden genereren

## <a name="monitoring-hello-cluster"></a>Hallo-cluster bewaken

Het is belangrijk toomonitor op Hallo platform niveau toodetermine of uw hardware en het cluster gedragen zich zoals verwacht. Hoewel Service Fabric toepassingen die worden uitgevoerd tijdens een hardwarefout kunt behouden, maar u nog steeds toodiagnose moet of een fout in een toepassing of in de onderliggende infrastructuur Hallo optreedt. Ook moet u controleren de clusters toobetter planning van capaciteit, ondersteuning bij het nemen van beslissingen over het toevoegen of verwijderen van de hardware.

Service Fabric bevat vijf verschillende logboek kanalen out-of-the-box die genereren Hallo gebeurtenissen te volgen:

* Operationele kanaal: op hoog niveau bewerkingen wordt uitgevoerd door de Service Fabric en Hallo-cluster, met inbegrip van gebeurtenissen voor een knooppunt is afkomstig van een nieuwe toepassing wordt geïmplementeerd, of een SF upgrade terugdraaien, enzovoort.
* Operationele kanaal - gedetailleerde: statusrapporten en beslissingen voor taakverdeling
* Gegevens & Messaging-kanaal: essentiële logboeken en gebeurtenissen die worden gegenereerd in onze messaging (momenteel alleen hello ReverseProxy) en het pad naar de data (betrouwbare services-modellen)
* Gegevens & Messaging kanaal - gedetailleerde: uitgebreide kanaal waarin alle niet-kritieke Hallo-logboeken van gegevens en berichten in het Hallo-cluster (dit kanaal heeft een zeer groot aantal gebeurtenissen)   
* [Gebeurtenissen van betrouwbare Services](service-fabric-reliable-services-diagnostics.md): programming model specifieke gebeurtenissen
* [Gebeurtenissen van betrouwbare actoren](service-fabric-reliable-actors-diagnostics.md): programming model specifieke gebeurtenissen en prestatiemeteritems
* Ondersteuning voor logboeken: het systeemlogboek in logboeken die worden gegenereerd door de Service Fabric alleen toobe door ons gebruikt wanneer u om ondersteuning te bieden

Deze verschillende kanalen betrekking hebben op de meeste Hallo platform logboekregistratie die wordt aanbevolen. tooimprove platform niveau aan te melden, overweeg investeren in een beter inzicht Hallo statusmodel en aangepaste statusrapporten toe te voegen en het toevoegen aangepaste **prestatiemeteritems** toobuild invloed op een realtime begrip van Hallo uw services en toepassingen op Hallo-cluster.

### <a name="azure-service-fabric-health-and-load-reporting"></a>Azure Service Fabric-status en load reporting

Service Fabric heeft een eigen statusmodel die is beschreven in deze artikelen:
- [Inleiding tooService Fabric-statuscontrole](service-fabric-health-introduction.md)
- [Servicestatus rapporteren en controleren](service-fabric-diagnostics-how-to-report-and-check-service-health.md)
- [Aangepaste Service Fabric-statusrapporten toevoegen](service-fabric-report-health.md)
- [Service Fabric-statusrapporten weergeven](service-fabric-view-entities-aggregated-health.md)

Statuscontrole is kritieke toomultiple aspecten van het besturingssysteem van een service. Statuscontrole is vooral belangrijk bij het Service Fabric een upgrade van de genoemde toepassing voert. Nadat elk upgradedomein van Hallo-service is bijgewerkt en beschikbaar tooyour klanten is, slagen Hallo upgradedomein statuscontroles voordat Hallo implementatie toohello volgende upgradedomein schakelt. Als de status van goede kan niet worden verkregen, wordt Hallo-implementatie teruggedraaid, zodat het Hallo-toepassing bevindt zich in een bekende goede status. Sommige klanten kunnen worden getroffen voordat er Hallo-services worden teruggedraaid, maar de meeste klanten kunnen een probleem won't problemen. Een resolutie vindt ook plaats relatief snel en zonder toowait voor de actie van een menselijke operator. Hallo meer statuscontroles die zijn opgenomen in uw code Hallo toleranter dat uw service wordt toodeployment problemen.

Een ander aspect van de status van de service is metrische gegevens van Hallo service reporting. Metrische gegevens zijn belangrijk in Service Fabric omdat ze gebruikte toobalance Resourcegebruik. Metrische gegevens kan ook een indicator van de systeemstatus zijn. Bijvoorbeeld, moet u wellicht een toepassing die veel services heeft en elk exemplaar een aanvragen per tweede (RPS) metriek rapporten. Als een service van meer bronnen dan een andere service gebruikmaakt, Service Fabric service-exemplaren rond Hallo-cluster, verplaatst tootry toomaintain zelfs bronnen beter worden benut. Zie voor een meer gedetailleerde uitleg van de werking van Resourcegebruik [brongebruik te beheren en te laden in Service Fabric met metrische gegevens](service-fabric-cluster-resource-manager-metrics.md).

Metrische gegevens ook kunt bieden u inzicht in hoe uw service wordt uitgevoerd. U kunt metrische gegevens toocheck die Hallo-service wordt uitgevoerd binnen de verwachte parameters gebruiken na verloop van tijd. Bijvoorbeeld, als trends die op 9: 00 uur op maandagochtend Hallo gemiddelde weergeven RPS 1000, wordt u mogelijk een statusrapport die u waarschuwt als hello RPS 500 of meer dan 1500 instellen. Alles wat u mogelijk geen bezwaar, maar er wellicht een goed idee een toobe uiterlijk ervoor dat uw klanten een geweldige ervaring hebben. Uw service kunt een set metrische gegevens die worden gerapporteerd voor de doeleinden van selectievakje, maar die niet van invloed op Hallo resource verdeling van Hallo cluster definiëren. toodo deze, toozero set Hallo metrische gewicht. U wordt aangeraden alle metrische gegevens beginnen met een gewicht van nul en Hallo gewicht niet verhogen tot u zeker weet dat u begrijpt hoe weging Hallo metrische gegevens is van invloed op resourceverdeling voor uw cluster.

> [!TIP]
> Gebruik niet te veel gewogen metrische gegevens. Het kan lastig toounderstand waarom service-exemplaren worden verplaatst rond voor netwerktaakverdeling zijn. Enkele metrische gegevens kan worden achterhaald!

Alle gegevens die kan duiden op Hallo status en prestaties van uw toepassing is geschikt is voor de metrische gegevens en de gezondheid van rapporten. Een CPU-prestatiemeteritem kan aangeven hoe uw knooppunt wordt gebruikt, maar deze niet zien of een bepaalde service is in orde, omdat er meerdere services op één knooppunt kunnen worden uitgevoerd. Metrische gegevens, zoals RPS, items verwerkt, maar alle latentie van aanvraag kan duiden op Hallo van status van een specifieke service.

tooreport health, gebruik code vergelijkbare toothis:

  ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportInstanceHealth(healthInformation);
    }
  ```

tooreport een metriek vergelijkbare toothis code gebruiken:

  ```csharp
    this.Partition.ReportLoad(new List<LoadMetric> { new LoadMetric("MemoryInMb", 1234), new LoadMetric("metric1", 42) });
  ```

### <a name="service-fabric-support-logs"></a>Logboeken voor service Fabric-ondersteuning

Als u toocontact Microsoft ondersteuning voor hulp nodig bij uw Azure Service Fabric-cluster, zijn bijna altijd Ondersteuningslogboeken vereist. Als uw cluster wordt gehost in Azure, worden logboeken automatisch geconfigureerd en verzameld als onderdeel van het maken van een cluster. Hallo-logboeken worden opgeslagen in een speciaal opslagaccount in de resourcegroep voor uw cluster. Hallo storage-account beschikt niet over een vaste naam, maar in Hallo-account, ziet u de blob-containers en tabellen met namen die met beginnen *fabric*. Zie voor meer informatie over het instellen van logboekverzamelingen voor een zelfstandige cluster [maken en beheren van een zelfstandige Azure Service Fabric-cluster](service-fabric-cluster-creation-for-windows-server.md) en [configuratie-instellingen voor een zelfstandige Windows cluster](service-fabric-cluster-manifest.md). Voor zelfstandige Service Fabric instanties worden Hallo logboeken gestuurd tooa lokale bestandsshare. U bent **vereist** toohave deze logboeken voor ondersteuning, maar ze zijn niet bedoeld toobe bruikbare door personen buiten Hallo Microsoft customer support team.

## <a name="enabling-diagnostics-for-a-cluster"></a>Diagnostische gegevens inschakelen voor een cluster

In de volgorde tootake profiteren van deze logboeken, is het raadzaam tijdens het maken van het cluster ' diagnostische gegevens ' is ingeschakeld. Door het inschakelen van diagnostische gegevens, wanneer Hallo cluster wordt geïmplementeerd, Windows Azure Diagnostics is kunnen tooacknowledge Hallo operationele Reliable Services en Reliable actors kanalen en gegevens op te slaan Hallo uitgelegd verder in [gebeurtenissen met samenvoegen Azure Diagnostics](service-fabric-diagnostics-event-aggregation-wad.md).

Zoals hierboven, is er ook een optioneel veld tooadd een instrumentatiesleutel Application Insights (AI). Als u ervoor toouse AI voor een analyse van gebeurtenis kiest (voor meer informatie over dit op [analyse van gebeurtenis met Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md)), hier Hallo AppInsights resource instrumentationKey (GUID) bevatten.


Als u toodeploy containers tooyour cluster gaat, schakelt u af toopick up docker-statistieken door deze tooyour 'WadCfg > DiagnosticMonitorConfiguration' toe te voegen:

```json
"DockerSources": {
    "Stats": {
        "enabled": true,
        "sampleRate": "PT1M"
    }
},

```

## <a name="measuring-performance"></a>Meten van de prestaties

Prestaties van uw cluster meten en helpt u begrijpen hoe kunnen toohandle laden en het station beslissingen rond het schalen van uw cluster (Zie voor meer informatie over het schalen van een cluster [op Azure](service-fabric-cluster-scale-up-down.md), of [lokale](service-fabric-cluster-windows-server-add-remove-nodes.md)). Prestatiegegevens is ook handig wanneer vergeleken tooactions u of uw toepassingen en services kunnen hebt uitgevoerd, bij het analyseren van Logboeken in Hallo toekomstige. 

Zie voor een lijst van prestaties tellers toocollect bij gebruik van Service Fabric [prestatiemeters in Service Fabric](service-fabric-diagnostics-event-generation-perf.md)

Hier zijn twee algemene manieren waarop u kunt instellen voor het verzamelen van prestatiegegevens voor het cluster:

* Met behulp van een agent: dit Hallo voorkeur manier van het verzamelen van prestaties van een virtuele machine is, omdat er agents hebben meestal een lijst met mogelijke prestaties metrische gegevens die kunnen worden verzameld en is een relatief gemakkelijk toochoose Hallo procesgegevens of wilt u toocollect wijzigen . Meer informatie over [hoe tooconfigure OMS Hallo voor Service Fabric](service-fabric-diagnostics-event-analysis-oms.md) en [Hallo OMS-Agent voor Windows instellen](../log-analytics/log-analytics-windows-agents.md) artikelen toolearn meer over Hallo OMS-agent, die een dergelijke bewakingsagent of kunnen toopick actief is prestatiegegevens voor het cluster virtuele machines en geïmplementeerde containers.

* Configureren van diagnostische gegevens toowrite prestaties tooa tabel prestatiemeteritems: voor clusters op Azure, dit betekent het wijzigen van hello Azure Diagnostics configuratie toopick van de relevante prestatiemeteritems Hallo van Hallo VM's in het cluster en toopick up inschakelen docker-statistieken als u geen containers wilt implementeren. Meer informatie over het configureren van [prestatiemeters in af](service-fabric-diagnostics-event-aggregation-wad.md) in Service Fabric-tooset van het verzamelen van prestatiemeteritems.

## <a name="next-steps"></a>Volgende stappen

Uw logboeken en gebeurtenissen moeten toobe geaggregeerd voordat ze kunnen worden verzonden tooany analysis platform. Meer informatie over [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) en [af](service-fabric-diagnostics-event-aggregation-wad.md) toobetter weet Hallo aanbevolen opties.
