---
title: instellingen voor aaaChange Azure Service Fabric-cluster | Microsoft Docs
description: Dit artikel wordt beschreven Hallo fabric-instellingen en Hallo fabric Upgradebeleid die u kunt aanpassen.
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: 
ms.assetid: 7ced36bf-bd3f-474f-a03a-6ebdbc9677e2
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/15/2017
ms.author: chackdan
ms.openlocfilehash: a8b125f7b4a02547cf4bcf2c936d0c7f1686c1a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="customize-service-fabric-cluster-settings-and-fabric-upgrade-policy"></a>Instellingen voor Service Fabric-cluster en het beleid voor Fabric-Upgrade aanpassen
Dit document leest u hoe toocustomize Hallo verschillende fabric-instellingen en beleid Hallo fabric-upgrade gebruiken voor uw Service Fabric-cluster. U kunt deze aanpassen op Hallo portal of met een Azure Resource Manager-sjabloon.

> [!NOTE]
> Niet alle instellingen zijn mogelijk niet beschikbaar via het Hallo-portal. Als een instelling hieronder vermelde niet beschikbaar via de portal Hallo aanpassen met behulp van een Azure Resource Manager-sjabloon.
> 

## <a name="customizing-service-fabric-cluster-settings-using-azure-resource-manager-templates"></a>Instellingen voor Service Fabric-cluster met behulp van Azure Resource Manager-sjablonen aanpassen
Hallo onderstaande stappen laten zien hoe een nieuwe instelling tooadd *MaxDiskQuotaInMB* toohello *Diagnostics* sectie.

1. Ga toohttps://resources.azure.com
2. Navigeer tooyour abonnement door het uitbreiden van abonnementen-resource groepen -> > Microsoft.ServiceFabric -> uw Cluster-naam
3. Selecteer in de rechterbovenhoek Hallo ' Lezen/schrijven'
4. Selecteer bewerken en bijwerken Hallo `fabricSettings` JSON-element en een nieuw element toevoegen

```
      {
        "name": "Diagnostics",
        "parameters": [
          {
            "name": "MaxDiskQuotaInMB",
            "value": "65536"
          }
        ]
      }
```

## <a name="fabric-settings-that-you-can-customize"></a>Fabric-instellingen die u kunt aanpassen
Hier volgen Hallo Fabric-instellingen die u kunt aanpassen:

### <a name="section-name-diagnostics"></a>Sectienaam: diagnostische gegevens
| **Parameter** | **Toegestane waarden** | **Hulp of korte beschrijving** |
| --- | --- | --- |
| ConsumerInstances |Tekenreeks |Hallo-lijst van DCA consumer exemplaren. |
| ProducerInstances |Tekenreeks |Hallo-lijst van DCA producent exemplaren. |
| AppEtwTraceDeletionAgeInDays |Int, de standaardwaarde is 3 |Aantal dagen waarna we oude ETL-bestanden met ETW toepassingstraceringen verwijderen. |
| AppDiagnosticStoreAccessRequiresImpersonation |BOOL, de standaardwaarde is true |Imitatie wel of niet is vereist wanneer toegang tot diagnostische namens Hallo-toepassing opslaat. |
| MaxDiskQuotaInMB |Int, de standaardwaarde is 65536 |Schijfquota in MB voor Windows Fabric-logboekbestanden. |
| DiskFullSafetySpaceInMB |Int, standaard is 1024 |Resterende schijfruimte in MB tooprotect niet wordt gebruikt door DCA. |
| ApplicationLogsFormatVersion |Int, de standaardwaarde is 0 |Versie voor de toepassing Logboeken indeling. Ondersteunde waarden zijn 0 en 1. Versie 1 bevat meer velden van record voor ETW-gebeurtenis Hallo dan versie 0. |
| ClusterId |Tekenreeks |Hallo unieke id van Hallo-cluster. Dit wordt gegenereerd wanneer het Hallo-cluster is gemaakt. |
| EnableTelemetry |BOOL, de standaardwaarde is true |Dit gaat tooenable of telemetrie uitschakelen. |
| EnableCircularTraceSession |BOOL, de standaardwaarde is ONWAAR |Vlag geeft aan of cirkelvormige traceersessies moeten worden gebruikt. |

### <a name="section-name-traceetw"></a>De naam van de sectie: Trace/Etw
| **Parameter** | **Toegestane waarden** | **Hulp of korte beschrijving** |
| --- | --- | --- |
| Niveau |Int, de standaardwaarde is 4 |Traceerniveau etw kan duren voordat de waarden 1, 2, 3, 4. toobe ondersteund Hallo traceerniveau moet blijven op 4 |

### <a name="section-name-performancecounterlocalstore"></a>Sectienaam: PerformanceCounterLocalStore
| **Parameter** | **Toegestane waarden** | **Hulp of korte beschrijving** |
| --- | --- | --- |
| IsEnabled |BOOL, de standaardwaarde is true |Vlag wordt aangegeven of het verzamelen van prestatiemeteritems op het lokale knooppunt is ingeschakeld. |
| SamplingIntervalInSeconds |Int, de standaardwaarde is 60 |Steekproefinterval voor prestatiemeteritems worden verzameld. |
| Prestatiemeteritems |Tekenreeks |Door komma's gescheiden lijst van de prestaties van items toocollect. |
| MaxCounterBinaryFileSizeInMB |Int, de standaardwaarde is 1 |Maximale grootte (in MB) voor elk prestaties prestatiemeteritems binaire bestand. |
| NewCounterBinaryFileCreationIntervalInMinutes |Int, de standaardwaarde is 10 |Maximale interval (in seconden) waarna een nieuw prestaties prestatiemeteritems binaire bestand is gemaakt. |

### <a name="section-name-setup"></a>Sectienaam: Setup
| **Parameter** | **Toegestane waarden** | **Hulp of korte beschrijving** |
| --- | --- | --- |
| FabricDataRoot |Tekenreeks |Hoofdmap voor service Fabric-gegevens. Standaard voor Azure d:\svcfab is |
| FabricLogRoot |Tekenreeks |Hoofdmap voor service fabric-logboek. Dit is waar SF-logboeken en traceringen worden geplaatst. |
| ServiceRunAsAccountName |Tekenreeks |Hallo-accountnaam onder welke toorun fabric host-service. |
| ServiceStartupType |Tekenreeks |Opstarttype van de fabric-hostservice Hallo Hallo. |
| SkipFirewallConfiguration |BOOL, de standaardwaarde is ONWAAR |Hiermee geeft u aan als firewall-instellingen toobe moeten door Hallo systeem ingesteld of niet. Dit geldt alleen als u windows firewall gebruikt. Als u firewalls van derden gebruikt, moet vervolgens u Hallo poorten openen voor het systeem en de toepassingen toouse Hallo |

### <a name="section-name-transactionalreplicator"></a>Sectienaam: TransactionalReplicator
| **Parameter** | **Toegestane waarden** | **Hulp of korte beschrijving** |
| --- | --- | --- |
| MaxCopyQueueSize |Uint, de standaardwaarde is 16384 |Dit is de maximale waarde Hallo Hallo begingrootte voor Hallo wachtrij die replicatiebewerkingen onderhoudt definieert. Houd er rekening mee dat deze een macht van 2 moet. Als tijdens runtime Hallo wachtrij groeit wordt toothis grootte operations beperkt tussen de primaire en secundaire replicaties Hallo. |
| BatchAcknowledgementInterval | Tijd in seconden, de standaardwaarde is 0,015 | Geef de interval in seconden. Hiermee wordt bepaald Hallo hoeveelheid tijd die Hallo replicator wacht nadat een bewerking voor het verzenden van een bevestiging is ontvangen. Andere bewerkingen zijn ontvangen tijdens deze periode hebben hun bevestigingen terug in een enkel bericht verzonden -> netwerkverkeer verminderen, maar mogelijk verminderen Hallo doorvoer van Hallo replicator. |
| MaxReplicationMessageSize |Uint, de standaardwaarde is 52428800 | Maximale berichtgrootte van replicatiebewerkingen. Standaardwaarde is 50MB. |
| ReplicatorAddress |tekenreeks, default is 'localhost:0' | Hallo-eindpunt in de vorm van een tekenreeks-'IP: poort, die wordt gebruikt door Hallo Windows Fabric Replicator tooestablish verbindingen met andere replica's in volgorde toosend/ontvangen bewerkingen. |
| InitialPrimaryReplicationQueueSize |Uint, de standaardwaarde is 64 | Deze waarde bepaalt Hallo begingrootte voor Hallo wachtrij die Hallo replicatiebewerkingen op Hallo primaire onderhoudt. Houd er rekening mee dat deze een macht van 2 moet.|
| MaxPrimaryReplicationQueueSize |Uint, de standaardwaarde is 8192 |Dit is maximum aantal bewerkingen die kunnen bestaan in de primaire replicatiewachtrij Hallo Hallo. Houd er rekening mee dat deze een macht van 2 moet. |
| MaxPrimaryReplicationQueueMemorySize |Uint, de standaardwaarde is 0 |Dit is de maximale waarde Hallo Hallo primaire replicatiewachtrij in bytes. |
| InitialSecondaryReplicationQueueSize |Uint, de standaardwaarde is 64 |Deze waarde bepaalt Hallo begingrootte voor Hallo wachtrij die Hallo replicatiebewerkingen op Hallo secundaire onderhoudt. Houd er rekening mee dat deze een macht van 2 moet. |
| MaxSecondaryReplicationQueueSize |Uint, de standaardwaarde is 16384 |Dit is maximum aantal bewerkingen die kunnen bestaan in de secundaire replicatiewachtrij Hallo Hallo. Houd er rekening mee dat deze een macht van 2 moet. |
| MaxSecondaryReplicationQueueMemorySize |Uint, de standaardwaarde is 0 |Dit is de maximale waarde Hallo Hallo secundaire replicatiewachtrij in bytes. |
| SecondaryClearAcknowledgedOperations |BOOL, de standaardwaarde is ONWAAR |BOOL die bepaalt of het Hallo-bewerkingen op de secundaire replicator Hallo gewist zodra ze zijn bevestigd toohello primaire (leeggemaakte toohello schijf). Instellingen voor die deze tooTRUE tot extra leesbewerkingen op de nieuwe primaire Hallo leiden kan tijdens het afvangen van replica's na een failover. |
| MaxMetadataSizeInKB |Int, de standaardwaarde is 4 |Maximale grootte van de metagegevens van het Hallo synchronisatielogboek stroom. |
| MaxRecordSizeInKB |Uint, standaard is 1024 | Maximale grootte van een stroom logboekrecord. |
| CheckpointThresholdInMB |Int, de standaardwaarde is 50 |Een controlepunt wordt gestart wanneer Hallo logboek Gebruik deze waarde overschrijdt. |
| MaxAccumulatedBackupLogSizeInMB |Int, de standaardwaarde is 800 |Maximale verzameld grootte (in MB) van de back-uplogboeken in een keten van de opgegeven back-uplogboek. Een incrementele back-aanvragen mislukt als Hallo incrementele back-up een back-uplogboek waardoor back-uplogboeken Hallo die zijn verzameld sinds Hallo relevante volledige back-up toobe groter is dan deze genereert. In dergelijke gevallen is de gebruiker vereist tootake een volledige back-up. |
| MaxWriteQueueDepthInKB |Int, de standaardwaarde is 0 | Int voor maximum schrijven wachtrijdiepte die Hallo core Berichtenlogboek kunt gebruiken zoals opgegeven in kilobytes voor Hallo-log dat is gekoppeld aan deze replica. Deze waarde is Hallo kunt u het maximum aantal bytes dat in behandeling tijdens het bijwerken van de core berichtenlogboek zijn kan. Kan het zijn 0 voor Hallo core berichtenlogboek toocompute een geschikte waarde of een meervoud van 4. |
| SharedLogId |Tekenreeks |Gedeelde logboek-id. Dit is een guid en moet uniek zijn voor elke gedeelde logboek. |
| SharedLogPath |Tekenreeks |Pad toohello gedeelde logboek. Hallo standaard gedeelde logboek wordt gebruikt als deze waarde leeg is. |
| SlowApiMonitoringDuration |Tijd in seconden, is standaard 300 | Duur voor api opgeven voordat de waarschuwing health gebeurtenis wordt geactiveerd.|
| MinLogSizeInMB |Int, de standaardwaarde is 0 |De minimumgrootte van Hallo transactionele logboek. Hallo logboek worden niet mogen tootruncate tooa grootte dan deze instelling. 0 geeft aan dat replicator Hallo Hallo minimale logboekgrootte volgens tooother instellingen wordt bepaald. Deze waarde verhoogt, Hallo mogelijkheid gedeeltelijke kopie en incrementele back-ups te doen omdat de kans op relevante logboekrecords worden afgekapt wordt verlaagd. |

### <a name="section-name-fabricclient"></a>Sectienaam: FabricClient
| **Parameter** | **Toegestane waarden** | **Hulp of korte beschrijving** |
| --- | --- | --- |
| NodeAddresses |tekenreeks, standaardwaarde is "" |Een verzameling van adressen (verbindingsreeksen) op verschillende knooppunten die gebruikt toocommunicate Hallo Hello Naming Service worden kunnen. In eerste instantie hello die client verbinding maakt met het selecteren van een van de adressen Hallo willekeurig. Als meer dan een verbindingsreeks wordt verstrekt en een verbinding is mislukt vanwege een communicatie- of time-outfout; Hallo overschakelt Client toouse Hallo volgende adres sequentieel worden verwerkt. Zie Hallo serviceadres Naming opnieuw sectie voor meer informatie over de semantiek voor nieuwe pogingen. |
| ConnectionInitializationTimeout |Tijd in seconden, de standaardwaarde is 2 |Geef de interval in seconden. Time-outinterval voor elke client tijd verbinding probeert een verbinding toohello gateway tooopen. |
| Partitionlocationcachelimit op |Int, de standaardwaarde is 100000 |Aantal partities in de cache opgeslagen voor de omzetting van de service (ingesteld too0 geen limiet). |
| ServiceChangePollInterval |Tijd in seconden, de standaardwaarde is 120 |Geef de interval in seconden. Hallo-interval tussen opeenvolgende polls voor service verandert van Hallo client toohello gateway voor meldingen retouraanroepen van geregistreerde service wijzigen. |
| KeepAliveIntervalInSeconds |Int, de standaardwaarde is 20 |Hallo-interval op welke Hallo FabricClient transport keepalive-berichten toohello gateway verzendt. Voor 0; keepAlive is uitgeschakeld. Moet een positieve waarde zijn. |
| HealthOperationTimeout |Tijd in seconden, de standaardwaarde is 120 |Geef de interval in seconden. Hallo-out voor een rapportbericht tooHealth Manager verzonden. |
| HealthReportSendInterval |Tijd in seconden, de standaardwaarde is 30 |Geef de interval in seconden. Hello-interval op welke Rapportonderdeel verzendt health geteld tooHealth Manager rapporteert. |
| HealthReportRetrySendInterval |Tijd in seconden, de standaardwaarde is 30 |Geef de interval in seconden. Hello-interval op welke Rapportonderdeel health opnieuw verzendt geteld tooHealth Manager rapporteert. |
| RetryBackoffInterval |Tijd in seconden, de standaardwaarde is 3 |Geef de interval in seconden. Hello back-off-interval alvorens Hallo opnieuw te proberen. |
| MaxFileSenderThreads |Uint, de standaardwaarde is 10 |Hallo maximum aantal bestanden die parallel worden overgedragen. |

### <a name="section-name-common"></a>Sectienaam: algemene
| **Parameter** | **Toegestane waarden** | **Hulp of korte beschrijving** |
| --- | --- | --- |
| PerfMonitorInterval |Tijd in seconden, de standaardwaarde is 1 |Geef de interval in seconden. Prestaties controle-interval. Instelling too0 of een negatieve waarde wordt de bewaking uitgeschakeld. |

### <a name="section-name-healthmanager"></a>Sectienaam: HealthManager
| **Parameter** | **Toegestane waarden** | **Hulp of korte beschrijving** |
| --- | --- | --- |
| EnableApplicationTypeHealthEvaluation |BOOL, de standaardwaarde is ONWAAR |Het statusbeleid voor de evaluatie van het cluster: per toepassing type health evaluatie inschakelen. |

### <a name="section-name-fabricnode"></a>Sectienaam: FabricNode
| **Parameter** | **Toegestane waarden** | **Hulp of korte beschrijving** |
| --- | --- | --- |
| StateTraceInterval |Tijd in seconden, is standaard 300 |Geef de interval in seconden. Hallo-interval voor de traceringsstatus knooppunt op elk knooppunt en van knooppunten op FM/FMM. |

### <a name="section-name-nodedomainids"></a>Sectienaam: NodeDomainIds
| **Parameter** | **Toegestane waarden** | **Hulp of korte beschrijving** |
| --- | --- | --- |
| UpgradeDomainId |tekenreeks, standaardwaarde is "" |Beschrijft een knooppunt tot een behoort Hallo-upgradedomein. |
| PropertyGroup |NodeFaultDomainIdCollection |Hierin wordt beschreven in domeinen met fouten Hallo die een knooppunt tot een behoort. Hallo foutdomein wordt gedefinieerd via een URI die Hallo-locatie van knooppunt Hallo in Hallo datacenter beschrijft.  Fout met betrekking tot domein URI's zijn Hallo opmaken fd: / fd/gevolgd door een padsegment URI.|

### <a name="section-name-nodeproperties"></a>Sectienaam: NodeProperties
| **Parameter** | **Toegestane waarden** | **Hulp of korte beschrijving** |
| --- | --- | --- |
| PropertyGroup |NodePropertyCollectionMap |Een verzameling van tekenreeks sleutel-waardeparen voor eigenschappen van het knooppunt. |

### <a name="section-name-nodecapacities"></a>Sectienaam: NodeCapacities
| **Parameter** | **Toegestane waarden** | **Hulp of korte beschrijving** |
| --- | --- | --- |
| PropertyGroup |NodeCapacityCollectionMap |Een verzameling van knooppunt capaciteitswaarden voor andere metrische gegevens. |

### <a name="section-name-fabricnode"></a>Sectienaam: FabricNode
| **Parameter** | **Toegestane waarden** | **Hulp of korte beschrijving** |
| --- | --- | --- |
| StartApplicationPortRange |Int, de standaardwaarde is 0 |Hallo toepassing poorten die worden beheerd door het subsysteem voor hosting is gestart. Vereist als EndpointFilteringEnabled ingesteld op true in Hosting is. |
| EndApplicationPortRange |Int, de standaardwaarde is 0 |Einde (geen inclusief) van Hallo toepassing poorten die worden beheerd door de hosting-subsysteem. Vereist als EndpointFilteringEnabled ingesteld op true in Hosting is. |
| ClusterX509StoreName |tekenreeks, standaardwaarde is "Mijn" |Naam van het X.509-certificaatarchief dat cluster certificaat voor het beveiligen van communicatie binnen het cluster bevat. |
| ClusterX509FindType |tekenreeks, default is 'FindByThumbprint' |Geeft aan hoe toosearch voor cluster certificaat in archief Hallo opgegeven door de waarden ClusterX509StoreName ondersteund: 'FindByThumbprint'; 'Findbysubjectname zijn' met 'Findbysubjectname zijn'; Wanneer er meerdere overeenkomsten; Hallo met Hallo verst verloop wordt gebruikt. |
| ClusterX509FindValue |tekenreeks, standaardwaarde is "" |De filterwaarde zoeken toolocate cluster certificaat gebruikt. |
| ClusterX509FindValueSecondary |tekenreeks, standaardwaarde is "" |De filterwaarde zoeken toolocate cluster certificaat gebruikt. |
| ServerAuthX509StoreName |tekenreeks, standaardwaarde is "Mijn" |Naam van het X.509-certificaatarchief die het servercertificaat voor entrée service bevat. |
| ServerAuthX509FindType |tekenreeks, default is 'FindByThumbprint' |Geeft aan hoe toosearch voor servercertificaat in archief Hallo opgegeven door de waarde ServerAuthX509StoreName ondersteund: FindByThumbprint; Findbysubjectname zijn. |
| ServerAuthX509FindValue |tekenreeks, standaardwaarde is "" |De filterwaarde zoeken gebruikt toolocate-servercertificaat. |
| ServerAuthX509FindValueSecondary |tekenreeks, standaardwaarde is "" |De filterwaarde zoeken gebruikt toolocate-servercertificaat. |
| ClientAuthX509StoreName |tekenreeks, standaardwaarde is "Mijn" |Naam van het certificaatarchief van Hallo x.509-certificaat voor de rol van standaard admin FabricClient met. |
| ClientAuthX509FindType |tekenreeks, default is 'FindByThumbprint' |Hiermee wordt aangegeven hoe toosearch voor certificaat in archief Hallo opgegeven door de waarde ClientAuthX509StoreName ondersteund: FindByThumbprint; Findbysubjectname zijn. |
| ClientAuthX509FindValue |tekenreeks, standaardwaarde is "" | Filter zoekwaarde toolocate certificaat voor standaard beheerdersrol FabricClient gebruikt. |
| ClientAuthX509FindValueSecondary |tekenreeks, standaardwaarde is "" |Filter zoekwaarde toolocate certificaat voor standaard beheerdersrol FabricClient gebruikt. |
| UserRoleClientX509StoreName |tekenreeks, standaardwaarde is "Mijn" |Naam van het certificaatarchief van Hallo x.509-certificaat voor de standaardgebruikersrol FabricClient met. |
| UserRoleClientX509FindType |tekenreeks, default is 'FindByThumbprint' |Hiermee wordt aangegeven hoe toosearch voor certificaat in archief Hallo opgegeven door de waarde UserRoleClientX509StoreName ondersteund: FindByThumbprint; Findbysubjectname zijn. |
| UserRoleClientX509FindValue |tekenreeks, standaardwaarde is "" |Filter zoekwaarde toolocate certificaat voor standaardgebruikersrol FabricClient gebruikt. |
| UserRoleClientX509FindValueSecondary |tekenreeks, standaardwaarde is "" |Filter zoekwaarde toolocate certificaat voor standaardgebruikersrol FabricClient gebruikt. |

### <a name="section-name-paas"></a>Sectienaam: Paas
| **Parameter** | **Toegestane waarden** | **Hulp of korte beschrijving** |
| --- | --- | --- |
| ClusterId |tekenreeks, standaardwaarde is "" |X509 archief wordt gebruikt voor de infrastructuur voor de beveiliging van de configuratie-certificaat. |

### <a name="section-name-fabrichost"></a>Sectienaam: FabricHost
| **Parameter** | **Toegestane waarden** | **Hulp of korte beschrijving** |
| --- | --- | --- |
| StopTimeout |Tijd in seconden, is standaard 300 |Geef de interval in seconden. Hallo-out voor activering van de gehoste service. deactivering en upgrade. |
| StartTimeout |Tijd in seconden, is standaard 300 |Geef de interval in seconden. Time-out voor fabricactivationmanager starten. |
| ActivationRetryBackoffInterval |Tijd in seconden, de standaardwaarde is 5 |Geef de interval in seconden. Backoff-interval op om de activering is mislukt; op elke continue activering fout Hallo systeem wordt opnieuw geprobeerd Hallo activering voor up toohello MaxActivationFailureCount. Hallo-interval voor opnieuw proberen op elke probeer is een product van continue activering mislukt en Hallo activering back-off-interval. |
| ActivationMaxRetryInterval |Tijd in seconden, is standaard 300 |Geef de interval in seconden. Interval voor maximum aantal nieuwe pogingen voor activering. Op elke Hallo continue fout opnieuw wordt interval berekend als Min (ActivationMaxRetryInterval; Continue foutentelling * ActivationRetryBackoffInterval). |
| ActivationMaxFailureCount |Int, de standaardwaarde is 10 |Dit is de maximale telling Hallo waarvoor systeem opnieuw wordt geprobeerd mislukte activering van wordt gegeven. |
| EnableServiceFabricAutomaticUpdates |BOOL, de standaardwaarde is ONWAAR |Dit is tooenable fabric automatische update via Windows Update. |
| EnableServiceFabricBaseUpgrade |BOOL, de standaardwaarde is ONWAAR |Dit is tooenable base update voor de server. |
| EnableRestartManagement |BOOL, de standaardwaarde is ONWAAR |Dit is tooenable server opnieuw worden opgestart. |


### <a name="section-name-failovermanager"></a>Sectienaam: FailoverManager
| **Parameter** | **Toegestane waarden** | **Hulp of korte beschrijving** |
| --- | --- | --- |
| UserReplicaRestartWaitDuration |Tijd in seconden, de standaardwaarde is 60,0 * 30 |Geef de interval in seconden. Wanneer een persistente replica afneemt; Windows Fabric wacht voor deze duur voor Hallo replica toocome back-up maken van nieuwe vervanging replica's (die een kopie van de status van de Hallo vereist). |
| QuorumLossWaitDuration |Tijd in seconden, de standaardwaarde is MaxValue |Geef de interval in seconden. Dit is de maximumduur Hallo waarvoor we een toobe partitie in een status van quorumverlies toestaan. Als Hallo partitie nog steeds in quorumverlies na deze duur is; Hallo-partitie is hersteld van quorumverlies door te letten Hallo omlaag replica's als verloren. Houd er rekening mee dat dit mogelijk gegevensverlies kan tot. |
| UserStandByReplicaKeepDuration |Tijd in seconden, de standaardwaarde is 3600.0 * 24 * 7 |Geef de interval in seconden. Wanneer een persistente replica keert u terug uit een inactief; mogelijk is deze al vervangen. Deze timer bepaalt hoe lang Hallo FM Hallo standby-replica eerst behoudt. |
| UserMaxStandByReplicaCount |Int, de standaardwaarde is 1 |Hallo standaard maximum aantal StandBy-replica's die Hallo systeem voor services van de gebruiker houdt. |

### <a name="section-name-namingservice"></a>Sectienaam: NamingService
| **Parameter** | **Toegestane waarden** | **Hulp of korte beschrijving** |
| --- | --- | --- |
| TargetReplicaSetSize |Int, de standaardwaarde is 7 |Hallo aantal replica's wordt ingesteld voor elke partitie van Hallo Naming Service store. Hallo replica sets toeneemt Hallo niveau van betrouwbaarheid bij het Hallo-informatie in Hallo Naming Service Store; aantal te verhogen Hallo wijzigen die informatie Hallo verlagen niet verloren als gevolg van knooppuntfouten; met een waarde van de toegenomen belasting op de Windows Fabric en Hallo tijd duurt het tooperform updates toohello naming gegevens.|
|MinReplicaSetSize | Int, de standaardwaarde is 3 | minimum aantal replica's Naming Service Hallo vereist toowrite in toocomplete een update. Als er minder replica's dan weigert deze actief is in Hallo system Hallo betrouwbaarheid System updates toohello Naming Service Store totdat de replica's zijn hersteld. Deze waarde moet nooit meer dan Hallo TargetReplicaSetSize. |
|ReplicaRestartWaitDuration | Tijd in seconden, de standaardwaarde is (60,0 * 30)| Geef de interval in seconden. Wanneer een replica Naming Service uitvalt; Deze timer wordt gestart.  Wanneer het Hallo FM verloopt begint tooreplace Hallo replica's die zijn niet beschikbaar (deze niet nog beschouwt ze verloren). |
|QuorumLossWaitDuration | Tijd in seconden, de standaardwaarde is MaxValue | Geef de interval in seconden. Wanneer een Naming Service opgehaald in quorumverlies; Deze timer wordt gestart.  Wanneer het Hallo FM verlopen worden beschouwd als Hallo omlaag replica's als verloren. en proberen toorecover quorum. Niet of dit tot verlies van gegevens leiden kan. |
|StandByReplicaKeepDuration | Tijd in seconden, de standaardwaarde is 3600.0 * 2 | Geef de interval in seconden. Wanneer een replica Naming Service keert u terug uit een inactief; mogelijk is deze al vervangen.  Deze timer bepaalt hoe lang Hallo FM Hallo standby-replica eerst behoudt. |
|PlacementConstraints | tekenreeks, standaardwaarde is "" | Beperking voor plaatsing Hallo Naming Service. |
|ServiceDescriptionCacheLimit | Int, de standaardwaarde is 0 | maximum aantal vermeldingen behouden in Hallo LRU-beschrijving servicecache op Hallo Hallo Naming Store-Service (ingesteld too0 geen limiet). |
|RepairInterval | Tijd in seconden, de standaardwaarde is 5 | Geef de interval in seconden. Interval in welke Hallo naming inconsistentie herstel tussen Hallo autoriteit eigenaar en de van de naameigenaar wordt gestart. |
|MaxNamingServiceHealthReports | Int, de standaardwaarde is 10 | maximum aantal trage bewerkingen die Naming opslaan Hallo service rapporten niet in orde in één keer. Als u 0; alle trage bewerkingen worden verzonden. |
| MaxMessageSize |Int, de standaardwaarde is 4*1024*1024 |Hallo maximale berichtgrootte voor clientcommunicatie van knooppunt bij gebruik van naamgeving. DOS-aanval verlichting; standaardwaarde is 4MB. |
| MaxFileOperationTimeout |Tijd in seconden, de standaardwaarde is 30 |Geef de interval in seconden. de maximale time-out Hallo toegestaan voor bestandsbewerking store-service. Het opgeven van een hogere time-out aanvragen worden geweigerd. |
| MaxOperationTimeout |Tijd in seconden, de standaardwaarde is 600 |Geef de interval in seconden. de maximale time-out Hallo toegestaan voor de clientbewerkingen. Het opgeven van een hogere time-out aanvragen worden geweigerd. |
| MaxClientConnections |Int, de standaardwaarde is 1000 |Hallo maximaal toegestane aantal clientverbindingen per gateway. |
| ServiceNotificationTimeout |Tijd in seconden, de standaardwaarde is 30 |Geef de interval in seconden. Hallo-out die wordt gebruikt voor het leveren van service meldingen toohello client. |
| MaxOutstandingNotificationsPerClient |Int, de standaardwaarde is 1000 |maximum aantal openstaande meldingen voordat een clientregistratie Hallo is geforceerd gesloten door Hallo-gateway. |
| MaxIndexedEmptyPartitions |Int, de standaardwaarde is 1000 |maximum aantal lege partities die blijft Hallo geïndexeerd in Hallo melding cache voor het herstellen van verbindingen clients synchroniseren. Lege partities boven dit nummer wordt verwijderd uit het Hallo-index in oplopende volgorde van lookup-versie. Opnieuw verbinding te maken van clients kunt synchroniseren en ontvangen van updates voor gemiste lege partitie; maar Hallo synchronisatieprotocol duurder wordt. |
| GatewayServiceDescriptionCacheLimit |Int, de standaardwaarde is 0 |maximum aantal vermeldingen behouden in Hallo LRU-beschrijving servicecache op Hallo Hallo Naming Gateway (ingesteld too0 geen limiet). |
| PartitionCount |Int, de standaardwaarde is 3 |Hallo aantal partities van Hallo Naming Service store toobe gemaakt. Elke partitie eigenaar is van een enkele partitie-sleutel die overeenkomt met de index tooits; in dat geval partitiesleutels [0; PartitionCount) bestaat. Toenemende Hallo aantal Naming Service partities toeneemt Hallo schaal die Naming Service Hallo op uitvoeren kunt door te verlagen Hallo gemiddelde hoeveelheid gegevens die zijn opgeslagen door de replica van een back-ups maken ingesteld. met een waarde van de toename in het gebruik van bronnen (sinds het PartitionCount * ReplicaSetSize service replica's moeten worden onderhouden).|

### <a name="section-name-runas"></a>Sectienaam: RunAs
| **Parameter** | **Toegestane waarden** | **Hulp of korte beschrijving** |
| --- | --- | --- |
| RunAsAccountName |tekenreeks, standaardwaarde is "" |Hiermee wordt aangegeven Hallo RunAs-accountnaam. Dit is alleen nodig voor account 'DomainUser' of 'ManagedServiceAccount' type. Geldige waarden zijn 'domein\gebruiker' of 'user@domain'. |
|RunAsAccountType|tekenreeks, standaardwaarde is "" |Hiermee wordt aangegeven Hallo Run as-accounttype. Dit is nodig voor alle geldige waarden voor RunAs-sectie ' DomainUser/NetworkService/ManagedServiceAccount/LocalSystem' zijn.|
|Wachtwoord|tekenreeks, standaardwaarde is "" |Hiermee wordt aangegeven Hallo wachtwoord voor RunAs-account. Dit is alleen nodig voor accounttype 'DomainUser'. |

### <a name="section-name-runasfabric"></a>Sectienaam: RunAs_Fabric
| **Parameter** | **Toegestane waarden** | **Hulp of korte beschrijving** |
| --- | --- | --- |
| RunAsAccountName |tekenreeks, standaardwaarde is "" |Hiermee wordt aangegeven Hallo RunAs-accountnaam. Dit is alleen nodig voor account 'DomainUser' of 'ManagedServiceAccount' type. Geldige waarden zijn 'domein\gebruiker' of 'user@domain'. |
|RunAsAccountType|tekenreeks, standaardwaarde is "" |Hiermee wordt aangegeven Hallo Run as-accounttype. Dit is nodig voor alle geldige waarden voor RunAs-sectie ' Lokalegebruiker/DomainUser/NetworkService/ManagedServiceAccount/LocalSystem' zijn. |
|Wachtwoord|tekenreeks, standaardwaarde is "" |Hiermee wordt aangegeven Hallo wachtwoord voor RunAs-account. Dit is alleen nodig voor accounttype 'DomainUser'. |

### <a name="section-name-runashttpgateway"></a>Sectienaam: RunAs_HttpGateway
| **Parameter** | **Toegestane waarden** | **Hulp of korte beschrijving** |
| --- | --- | --- |
| RunAsAccountName |tekenreeks, standaardwaarde is "" |Hiermee wordt aangegeven Hallo RunAs-accountnaam. Dit is alleen nodig voor account 'DomainUser' of 'ManagedServiceAccount' type. Geldige waarden zijn 'domein\gebruiker' of 'user@domain'. |
|RunAsAccountType|tekenreeks, standaardwaarde is "" |Hiermee wordt aangegeven Hallo Run as-accounttype. Dit is nodig voor alle geldige waarden voor RunAs-sectie ' Lokalegebruiker/DomainUser/NetworkService/ManagedServiceAccount/LocalSystem' zijn. |
|Wachtwoord|tekenreeks, standaardwaarde is "" |Hiermee wordt aangegeven Hallo wachtwoord voor RunAs-account. Dit is alleen nodig voor accounttype 'DomainUser'. |

### <a name="section-name-runasdca"></a>Sectienaam: RunAs_DCA
| **Parameter** | **Toegestane waarden** | **Hulp of korte beschrijving** |
| --- | --- | --- |
| RunAsAccountName |tekenreeks, standaardwaarde is "" |Hiermee wordt aangegeven Hallo RunAs-accountnaam. Dit is alleen nodig voor account 'DomainUser' of 'ManagedServiceAccount' type. Geldige waarden zijn 'domein\gebruiker' of 'user@domain'. |
|RunAsAccountType|tekenreeks, standaardwaarde is "" |Hiermee wordt aangegeven Hallo Run as-accounttype. Dit is nodig voor alle geldige waarden voor RunAs-sectie ' Lokalegebruiker/DomainUser/NetworkService/ManagedServiceAccount/LocalSystem' zijn. |
|Wachtwoord|tekenreeks, standaardwaarde is "" |Hiermee wordt aangegeven Hallo wachtwoord voor RunAs-account. Dit is alleen nodig voor accounttype 'DomainUser'. |

### <a name="section-name-httpgateway"></a>Sectienaam: HttpGateway
| **Parameter** | **Toegestane waarden** | **Hulp of korte beschrijving** |
| --- | --- | --- |
|IsEnabled|BOOL, de standaardwaarde is ONWAAR | Hiermee wordt en uitgeschakeld Hallo httpgateway. Httpgateway is standaard uitgeschakeld en deze configuratie moet toobe set tooenable deze. |
|ActiveListeners |Uint, de standaardwaarde is 50 | Het aantal leesbewerkingen toopost toohello HTTP-server-wachtrij. Hiermee bepaalt u het aantal gelijktijdige aanvragen op dat kan worden voldaan door Hallo HttpGateway Hallo. |
|MaxEntityBodySize |Uint, de standaardwaarde is 4194304 |  Geeft de maximale grootte Hallo van Hallo-instantie die een http-aanvraag kan worden verwacht. Standaardwaarde is 4MB. Httpgateway een aanvraag mislukt als er een instantie van de grootte van > deze waarde. Minimale lezen chunkgrootte is 4096 bytes. Zodat dit toobe heeft > = 4096. |
|HttpGatewayHealthReportSendInterval |Tijd in seconden, de standaardwaarde is 30 | Geef de interval in seconden. Hallo interval welke Hallo HTTP-Gateway verzendt geteld health rapporten tooHealth Manager. |

### <a name="section-name-ktllogger"></a>Sectienaam: KtlLogger
| **Parameter** | **Toegestane waarden** | **Hulp of korte beschrijving** |
| --- | --- | --- |
|AutomaticMemoryConfiguration |Int, de standaardwaarde is 1 | Vlag waarmee wordt aangegeven als Hallo geheugeninstellingen moeten worden automatisch en dynamisch geconfigureerd. Als nul vervolgens Hallo geheugen configuratie-instellingen rechtstreeks worden gebruikt en niet op basis van het systeem voorwaarden wijzigen. Als er een vervolgens Hallo geheugen instellingen worden automatisch geconfigureerd en kunnen worden gewijzigd op basis van systeem voorwaarden. |
|WriteBufferMemoryPoolMinimumInKB |Int, de standaardwaarde is 8388608 |Hallo aantal KB tooinitially voor Hallo schrijven buffergroep geheugen toewijzen. Gebruik 0 tooindicate geen limiet standaard moet consistent zijn met SharedLogSizeInMB hieronder. |
|WriteBufferMemoryPoolMaximumInKB | Int, de standaardwaarde is 0 |het aantal KB tooallow Hallo Hallo schrijven buffer geheugen groep toogrow tot. Gebruik 0 tooindicate geen limiet. |
|MaximumDestagingWriteOutstandingInKB | Int, de standaardwaarde is 0 | aantal KB tooallow Hallo Hallo gedeeld logboek tooadvance tevoren Hallo toegewezen logboek. Gebruik 0 tooindicate geen limiet.
|SharedLogPath |tekenreeks, standaardwaarde is "" | Pad en naam toolocation tooplace gedeelde logboek container. Gebruik ' ' voor het gebruik van standaardpad onder fabric-gegevenshoofdmap. |
|SharedLogId |tekenreeks, standaardwaarde is "" |De unieke guid voor gedeelde logboek-container. Gebruik ' ' als standaardpad onder fabric-gegevenshoofdmap gebruikt. |
|SharedLogSizeInMB |Int, de standaardwaarde is 8192 | Hallo aantal MB tooallocate in Hallo gedeelde logboek container. |

### <a name="section-name-applicationgatewayhttp"></a>De naam van de sectie: ApplicationGateway/Http
| **Parameter** | **Toegestane waarden** | **Hulp of korte beschrijving** |
| --- | --- | --- |
|IsEnabled |BOOL, de standaardwaarde is ONWAAR | Hiermee wordt en uitgeschakeld Hallo HttpApplicationGateway. HttpApplicationGateway is standaard uitgeschakeld en deze configuratie moet toobe set tooenable deze. |
|NumberOfParallelOperations | Uint, de standaardwaarde is 5000 | Het aantal leesbewerkingen toopost toohello HTTP-server-wachtrij. Hiermee bepaalt u het aantal gelijktijdige aanvragen op dat kan worden voldaan door Hallo HttpGateway Hallo. |
|DefaultHttpRequestTimeout |Tijd in seconden. de standaardwaarde is 120 |Geef de interval in seconden.  Biedt Hallo standaard aanvraag time-out voor Hallo http-aanvragen worden verwerkt in Hallo HTTP-app-gateway. |
|ResolveServiceBackoffInterval |Tijd in seconden, de standaardwaarde is 5 |Geef de interval in seconden.  Hallo back-off standaardinterval biedt voordat u probeert een mislukte omzettingsbewerking service. |
|BodyChunkSize |Uint, de standaardwaarde is 16384 |  Biedt Hallo grootte van voor Hallo chunk in bytes gebruikt tooread Hallo hoofdtekst. |
|GatewayAuthCredentialType |tekenreeks, default is 'None' | Hiermee geeft u Hallo type beveiliging referenties toouse op Hallo http app gateway eindpunt geldige waarden zijn ' geen / X 509. |
|GatewayX509CertificateStoreName |tekenreeks, standaardwaarde is "Mijn" | Naam van het X.509-certificaatarchief dat certificaat voor HTTP-app gateway bevat. |
|GatewayX509CertificateFindType |tekenreeks, default is 'FindByThumbprint' | Hiermee wordt aangegeven hoe toosearch voor certificaat in archief Hallo opgegeven door de waarde GatewayX509CertificateStoreName ondersteund: FindByThumbprint; Findbysubjectname zijn. |
|GatewayX509CertificateFindValue | tekenreeks, standaardwaarde is "" | Filter zoekwaarde gebruikt certificaat voor gateway-toolocate Hallo HTTP-app. Dit certificaat is geconfigureerd op Hallo https-eindpunt en gebruikte tooverify Hallo identiteit van de app Hallo kan ook worden indien nodig door Hallo-services. FindValue wordt opgezocht eerste; en als dat niet bestaat; FindValueSecondary wordt opgezocht. |
|GatewayX509CertificateFindValueSecondary | tekenreeks, standaardwaarde is "" |Filter zoekwaarde gebruikt certificaat voor gateway-toolocate Hallo HTTP-app. Dit certificaat is geconfigureerd op Hallo https-eindpunt en gebruikte tooverify Hallo identiteit van de app Hallo kan ook worden indien nodig door Hallo-services. FindValue wordt opgezocht eerste; en als dat niet bestaat; FindValueSecondary wordt opgezocht.|

### <a name="section-name-management"></a>Sectienaam: Management
| **Parameter** | **Toegestane waarden** | **Hulp of korte beschrijving** |
| --- | --- | --- |
| ImageStoreConnectionString |SecureString | Verbinding tekenreeks toohello toegangspunt voor de Installatiekopieopslag. |
| ImageStoreMinimumTransferBPS | Int, standaard is 1024 |Hallo minimale overdrachtssnelheid tussen Hallo-cluster en de Installatiekopieopslag. Deze waarde is gebruikte toodetermine Hallo time-out bij het openen van externe Installatiekopieopslag Hallo. Wijzig deze waarde alleen als de Hallo latentie tussen Hallo-cluster en de Installatiekopieopslag hoge tooallow meer tijd voor Hallo cluster toodownload van externe Installatiekopieopslag Hallo. |
|AzureStorageMaxWorkerThreads | Int, de standaardwaarde is 25 | Hallo maximum aantal werkthreads parallel. |
|AzureStorageMaxConnections | Int, de standaardwaarde is 5000 | Hallo maximum aantal gelijktijdige verbindingen tooazure opslag. |
|AzureStorageOperationTimeout | Tijd in seconden, de standaardwaarde is 6000 | Geef de interval in seconden. Time-out voor xstore bewerking toocomplete. |
|ImageCachingEnabled | BOOL, de standaardwaarde is true | Deze configuratie kan wij tooenable of cache uitschakelen. |
|DisableChecksumValidation | BOOL, de standaardwaarde is ONWAAR | Deze configuratie kunnen we tooenable- of uitschakelen van controlesomvalidatie tijdens het inrichten van de toepassing. |
|DisableServerSideCopy | BOOL, de standaardwaarde is ONWAAR | Deze configuratie schakelt of serverkopie van het toepassingspakket op Hallo Installatiekopieopslag tijdens het inrichten van de toepassing. |

### <a name="section-name-healthmanagerclusterhealthpolicy"></a>De naam van de sectie: HealthManager/ClusterHealthPolicy
| **Parameter** | **Toegestane waarden** | **Hulp of korte beschrijving** |
| --- | --- | --- |
| ConsiderWarningAsError |BOOL, de standaardwaarde is ONWAAR |Het statusbeleid voor de evaluatie van het cluster: waarschuwingen als fouten worden behandeld. |
| MaxPercentUnhealthyNodes | Int, de standaardwaarde is 0 |Het statusbeleid voor de evaluatie van het cluster: maximumpercentage van slecht knooppunten toegestaan voor Hallo cluster toobe in orde. |
| MaxPercentUnhealthyApplications | Int, de standaardwaarde is 0 |Het statusbeleid voor de evaluatie van het cluster: maximale percentage van de beschadigde toepassingen toegestaan voor Hallo cluster toobe in orde. |
|MaxPercentDeltaUnhealthyNodes | Int, de standaardwaarde is 10 |Upgrade van het statusbeleid voor de evaluatie van het cluster: maximale percentage van de delta slecht knooppunten toegestaan voor Hallo cluster toobe in orde. |
|MaxPercentUpgradeDomainDeltaUnhealthyNodes | Int, de standaardwaarde is 15 |Upgrade van het statusbeleid voor de evaluatie van het cluster: maximale percentage van de delta van beschadigde knooppunten in een upgradedomein toegestaan voor Hallo cluster toobe in orde.|

### <a name="section-name-faultanalysisservice"></a>Sectienaam: FaultAnalysisService
| **Parameter** | **Toegestane waarden** | **Hulp of korte beschrijving** |
| --- | --- | --- |
| TargetReplicaSetSize |Int, de standaardwaarde is 0 |NOT_PLATFORM_UNIX_START hello TargetReplicaSetSize voor FaultAnalysisService. |
| MinReplicaSetSize |Int, de standaardwaarde is 0 |Hello MinReplicaSetSize voor FaultAnalysisService. |
| ReplicaRestartWaitDuration |Tijd in seconden, de standaardwaarde is 60 minuten|Geef de interval in seconden. Hello ReplicaRestartWaitDuration voor FaultAnalysisService. |
| QuorumLossWaitDuration | Tijd in seconden, de standaardwaarde is MaxValue |Geef de interval in seconden. Hello QuorumLossWaitDuration voor FaultAnalysisService. |
| StandByReplicaKeepDuration| Tijd in seconden, de standaardwaarde is (60*24*7) minuten |Geef de interval in seconden. Hello StandByReplicaKeepDuration voor FaultAnalysisService. |
| PlacementConstraints | tekenreeks, standaardwaarde is ""| Hello PlacementConstraints voor FaultAnalysisService. |
| StoredActionCleanupIntervalInSeconds | Int, de standaardwaarde is 3600 |Dit is hoe vaak hello store worden opgeschoond.  Alleen acties in een definitieve status; en die ten minste voltooid CompletedActionKeepDurationInSeconds geleden worden verwijderd. |
| CompletedActionKeepDurationInSeconds | Int, de standaardwaarde is 604800 | Dit is ongeveer hoe lang tookeep acties die zich in een definitieve status.  Dit is ook afhankelijk StoredActionCleanupIntervalInSeconds; Aangezien Hallo werk toocleanup wordt alleen uitgevoerd op dat interval. 604800 is 7 dagen. |
| StoredChaosEventCleanupIntervalInSeconds | Int, de standaardwaarde is 3600 |Dit is hoe vaak hello store worden gecontroleerd voor opschoning; Als het aantal gebeurtenissen Hallo meer dan 30000 is; Hallo opschonen wordt kick in. |

### <a name="section-name-filestoreservice"></a>Sectienaam: FileStoreService
| **Parameter** | **Toegestane waarden** | **Hulp of korte beschrijving** |
| --- | --- | --- |
| NamingOperationTimeout |Tijd in seconden, de standaardwaarde is 60 |Geef de interval in seconden. Hallo-out voor de naamgeving bewerking. |
| QueryOperationTimeout | Tijd in seconden, de standaardwaarde is 60 |Geef de interval in seconden. Hallo-out voor de querybewerking opnieuw uitvoeren. |
| MaxCopyOperationThreads | Uint, de standaardwaarde is 0 | Hallo kunt u het maximale aantal parallelle bestanden die secundaire kunt kopiëren vanaf primaire. "0" == aantal kernen. |
| MaxFileOperationThreads | Uint, de standaardwaarde is 100 | Hallo maximale aantal parallelle threads toegestane tooperform FileOperations (kopiëren of verplaatsen) in de primaire Hallo. "0" == aantal kernen. |
| MaxStoreOperations | Uint, de standaardwaarde is 4096 |Hallo maximale aantal parallelle store transacties bewerkingen op de primaire toegestaan. "0" == aantal kernen. |
| MaxRequestProcessingThreads | Uint, de standaardwaarde is 200 |Hallo kunt u het maximale aantal parallelle threads toegestaan tooprocess aanvragen in Hallo primaire. "0" == aantal kernen. |
| MaxSecondaryFileCopyFailureThreshold | Uint, de standaardwaarde is 25| Hallo maximumaantal bestand kopiëren nieuwe pogingen bereikt op Hallo secundaire voordat geeft. |
| AnonymousAccessEnabled | BOOL, de standaardwaarde is true |Anonieme toegang toohello die filestoreservice deelt inschakelen/uitschakelen. |
| PrimaryAccountType | tekenreeks, standaardwaarde is "" |Hallo primaire AccountType Hallo principal tooACL Hallo FileStoreService deelt. |
| PrimaryAccountUserName | tekenreeks, standaardwaarde is "" |Hallo hoofdaccount gebruikersnaam van Hallo principal tooACL hello FileStoreService shares. |
| PrimaryAccountUserPassword | SecureString, de standaardwaarde is leeg |Hallo primaire accountwachtwoord Hallo principal tooACL Hallo FileStoreService deelt. |
| FileStoreService | PrimaryAccountNTLMPasswordSecret | SecureString, de standaardwaarde is leeg | Hallo wachtwoord geheim dat als seed toogenerated hetzelfde gebruikt wachtwoord bij gebruik van NTLM-verificatie. |
| PrimaryAccountNTLMX509StoreLocation | tekenreeks, default is 'LocalMachine'| Hallo archieflocatie van Hallo X509 certificaat gebruikt toogenerate HMAC op Hallo PrimaryAccountNTLMPasswordSecret bij gebruik van NTLM-verificatie. |
| PrimaryAccountNTLMX509StoreName | tekenreeks is de standaardwaarde is "Mijn"| de Opslagnaam Hallo Hallo X509 certificaat gebruikt toogenerate HMAC op Hallo PrimaryAccountNTLMPasswordSecret bij gebruik van NTLM-verificatie. |
| PrimaryAccountNTLMX509Thumbprint | tekenreeks, standaardwaarde is ""|Hallo vingerafdruk van certificaat Hallo X509 gebruikt toogenerate HMAC op Hallo PrimaryAccountNTLMPasswordSecret bij gebruik van NTLM-verificatie. |
| SecondaryAccountType | tekenreeks, standaardwaarde is ""| Hallo secundaire AccountType Hallo principal tooACL Hallo FileStoreService deelt. |
| SecondaryAccountUserName | tekenreeks, standaardwaarde is ""| Hallo secundaire account gebruikersnaam van Hallo principal tooACL hello FileStoreService shares. |
| SecondaryAccountUserPassword | SecureString, de standaardwaarde is leeg |Hallo secundaire accountwachtwoord Hallo principal tooACL Hallo FileStoreService deelt.  |
| SecondaryAccountNTLMPasswordSecret | SecureString, de standaardwaarde is leeg | Hallo wachtwoord geheim dat als seed toogenerated hetzelfde gebruikt wachtwoord bij gebruik van NTLM-verificatie. |
| SecondaryAccountNTLMX509StoreLocation | tekenreeks, default is 'LocalMachine' |Hallo archieflocatie van Hallo X509 certificaat gebruikt toogenerate HMAC op Hallo SecondaryAccountNTLMPasswordSecret bij gebruik van NTLM-verificatie. |
| SecondaryAccountNTLMX509StoreName | tekenreeks is de standaardwaarde is "Mijn" |de Opslagnaam Hallo Hallo X509 certificaat gebruikt toogenerate HMAC op Hallo SecondaryAccountNTLMPasswordSecret bij gebruik van NTLM-verificatie. |
| SecondaryAccountNTLMX509Thumbprint | tekenreeks, standaardwaarde is ""| Hallo vingerafdruk van certificaat Hallo X509 gebruikt toogenerate HMAC op Hallo SecondaryAccountNTLMPasswordSecret bij gebruik van NTLM-verificatie. |

### <a name="section-name-imagestoreservice"></a>Sectienaam: ImageStoreService
| **Parameter** | **Toegestane waarden** | **Hulp of korte beschrijving** |
| --- | --- | --- |
| Ingeschakeld |BOOL, de standaardwaarde is ONWAAR |de vlag ingeschakeld voor ImageStoreService Hello. |
| TargetReplicaSetSize | Int, de standaardwaarde is 7 |Hello TargetReplicaSetSize voor ImageStoreService. |
| MinReplicaSetSize | Int, de standaardwaarde is 3 |Hello MinReplicaSetSize voor ImageStoreService. |
| ReplicaRestartWaitDuration | Tijd in seconden, de standaardwaarde is 60,0 * 30 | Geef de interval in seconden. Hello ReplicaRestartWaitDuration voor ImageStoreService. |
| QuorumLossWaitDuration | Tijd in seconden, de standaardwaarde is MaxValue | Geef de interval in seconden. Hello QuorumLossWaitDuration voor ImageStoreService. |
| StandByReplicaKeepDuration | Tijd in seconden, de standaardwaarde is 3600.0 * 2 | Geef de interval in seconden. Hello StandByReplicaKeepDuration voor ImageStoreService. |
| PlacementConstraints | tekenreeks, standaardwaarde is "" | Hello PlacementConstraints voor ImageStoreService. |
| ClientUploadTimeout | Tijd in seconden, de standaardwaarde is 1800 |Geef de interval in seconden. Time-outwaarde voor het uploaden van het hoogste niveau aanvragen tooImage Store-Service. |
| ClientCopyTimeout | Tijd in seconden, de standaardwaarde is 1800 | Geef de interval in seconden. Time-outwaarde voor de site op het hoogste kopie aanvragen tooImage Store-Service. |
| ClientDownloadTimeout | Tijd in seconden, de standaardwaarde is 1800 | Geef de interval in seconden. Time-outwaarde voor downloaden op het hoogste niveau aanvragen tooImage Store-Service |
| ClientListTimeout | Tijd in seconden, de standaardwaarde is 600 | Geef de interval in seconden. Time-outwaarde voor de lijst op het hoogste niveau aanvragen tooImage Store-Service. |
| ClientDefaultTimeout | Tijd in seconden, is standaard 180 | Geef de interval in seconden. Time-outwaarde voor alle aanvragen voor niet-uploaden/niet-download (bijvoorbeeld bestaat; verwijderen) tooImage Store-Service. |

### <a name="section-name-imagestoreclient"></a>Sectienaam: ImageStoreClient
| **Parameter** | **Toegestane waarden** | **Hulp of korte beschrijving** |
| --- | --- | --- |
| ClientUploadTimeout |Tijd in seconden, de standaardwaarde is 1800 | Geef de interval in seconden. Time-outwaarde voor het uploaden van het hoogste niveau aanvragen tooImage Store-Service. |
| ClientCopyTimeout | Tijd in seconden, de standaardwaarde is 1800 | Geef de interval in seconden. Time-outwaarde voor de site op het hoogste kopie aanvragen tooImage Store-Service. |
|ClientDownloadTimeout | Tijd in seconden, de standaardwaarde is 1800 | Geef de interval in seconden. Time-outwaarde voor downloaden op het hoogste niveau aanvragen tooImage Store-Service. |
|ClientListTimeout | Tijd in seconden, de standaardwaarde is 600 |Geef de interval in seconden. Time-outwaarde voor de lijst op het hoogste niveau aanvragen tooImage Store-Service. |
|ClientDefaultTimeout | Tijd in seconden, is standaard 180 | Geef de interval in seconden. Time-outwaarde voor alle aanvragen voor niet-uploaden/niet-download (bijvoorbeeld bestaat; verwijderen) tooImage Store-Service. |

### <a name="section-name-tokenvalidationservice"></a>Sectienaam: TokenValidationService
| **Parameter** | **Toegestane waarden** | **Hulp of korte beschrijving** |
| --- | --- | --- |
| Providers |tekenreeks, default is 'DSTS' |Door komma's gescheiden lijst met providers tooenable van validatie van tokens (geldig providers zijn: DSTS; AAD). Op dit moment slechts één provider kan worden ingeschakeld op elk gewenst moment. |

### <a name="section-name-upgradeorchestrationservice"></a>Sectienaam: UpgradeOrchestrationService
| **Parameter** | **Toegestane waarden** | **Hulp of korte beschrijving** |
| --- | --- | --- |
| TargetReplicaSetSize |Int, de standaardwaarde is 0 |Hello TargetReplicaSetSize voor UpgradeOrchestrationService. |
| MinReplicaSetSize |Int, de standaardwaarde is 0 | Hello MinReplicaSetSize voor UpgradeOrchestrationService.
| ReplicaRestartWaitDuration | Tijd in seconden, de standaardwaarde is 60 minuten| Geef de interval in seconden. Hello ReplicaRestartWaitDuration voor UpgradeOrchestrationService. |
| QuorumLossWaitDuration | Tijd in seconden, de standaardwaarde is MaxValue | Geef de interval in seconden. Hello QuorumLossWaitDuration voor UpgradeOrchestrationService. |
| StandByReplicaKeepDuration | Tijd in seconden, de standaardwaarde is 60*24*7 minuten | Geef de interval in seconden. Hello StandByReplicaKeepDuration voor UpgradeOrchestrationService. |
| PlacementConstraints | tekenreeks, standaardwaarde is "" | Hello PlacementConstraints voor UpgradeOrchestrationService. |
| AutoupgradeEnabled | BOOL, de standaardwaarde is true | Automatische polling en upgrade-actie op basis van een doel-toestandbestand. |
| UpgradeApprovalRequired | BOOL, de standaardwaarde is ONWAAR | Instelling toomake code upgrade nodig goedkeuring door beheerder voordat u doorgaat. |

### <a name="section-name-upgradeservice"></a>Sectienaam: UpgradeService
| **Parameter** | **Toegestane waarden** | **Hulp of korte beschrijving** |
| --- | --- | --- |
| PlacementConstraints |tekenreeks, standaardwaarde is "" |Hello PlacementConstraints voor de Upgrade-service. |
| TargetReplicaSetSize | Int, de standaardwaarde is 3 | Hello TargetReplicaSetSize voor UpgradeService. |
| MinReplicaSetSize | Int, de standaardwaarde is 2 | Hello MinReplicaSetSize voor UpgradeService. |
| CoordinatorType | tekenreeks, default is 'WUTest'| Hello CoordinatorType voor UpgradeService. |
| BaseUrl | tekenreeks, standaardwaarde is "" |BaseUrl voor UpgradeService. |
| ClusterId | tekenreeks, standaardwaarde is "" | ClusterId voor UpgradeService. |
| X509StoreName | tekenreeks, standaardwaarde is "Mijn"| X509StoreName voor UpgradeService. |
| X509StoreLocation | tekenreeks, standaardwaarde is "" | X509StoreLocation voor UpgradeService. |
| X509FindType | tekenreeks, standaardwaarde is ""| X509FindType voor UpgradeService. |
| X509FindValue | tekenreeks, standaardwaarde is "" | X509FindValue voor UpgradeService. |
| X509SecondaryFindValue | tekenreeks, standaardwaarde is "" | X509SecondaryFindValue voor UpgradeService. |
| OnlyBaseUpgrade | BOOL, de standaardwaarde is ONWAAR | OnlyBaseUpgrade voor UpgradeService. |
| TestCabFolder | tekenreeks, standaardwaarde is "" | TestCabFolder voor UpgradeService. |

### <a name="section-name-securityclientaccess"></a>De naam van de sectie: Beveiliging/ClientAccess
| **Parameter** | **Toegestane waarden** | **Hulp of korte beschrijving** |
| --- | --- | --- |
| CreateName |tekenreeks, default is 'Admin' |Beveiligingsconfiguratie voor het maken van naamgevings-URI. |
| DeleteName |tekenreeks, default is 'Admin' |Beveiligingsconfiguratie voor verwijdering naamgevings-URI. |
| PropertyWriteBatch |tekenreeks, default is 'Admin' |Beveiligingsconfiguratie voor de eigenschap Naming schrijfbewerkingen. |
| CreateService |tekenreeks, default is 'Admin' | Beveiligingsconfiguratie voor het maken van de service. |
| CreateServiceFromTemplate |tekenreeks, default is 'Admin' |Beveiligingsconfiguratie voor het maken van een service van sjabloon. |
| UpdateService |tekenreeks, default is 'Admin' |Beveiligingsconfiguratie voor service-updates. |
| DeleteService  |tekenreeks, default is 'Admin' |Beveiligingsconfiguratie voor verwijdering van de service. |
| ProvisionApplicationType |tekenreeks, default is 'Admin' | Beveiligingsconfiguratie voor het inrichten van de toepassing-type. |
| SubmitMetadata |tekenreeks, default is 'Admin' | Beveiligingsconfiguratie voor het maken van de toepassing. |
| DeleteApplication |tekenreeks, default is 'Admin' | Beveiligingsconfiguratie voor verwijdering van de toepassing. |
| UpgradeApplication |tekenreeks, default is 'Admin' | Beveiligingsconfiguratie voor het starten of toepassingsupgrades onderbreken. |
| RollbackApplicationUpgrade |tekenreeks, default is 'Admin' | Beveiligingsconfiguratie voor toepassingsupgrades worden teruggedraaid. |
| UnprovisionApplicationType |tekenreeks, default is 'Admin' | Beveiligingsconfiguratie voor de toepassing type hierbij. |
| MoveNextUpgradeDomain |tekenreeks, default is 'Admin' | Beveiligingsconfiguratie voor toepassingsupgrades met een expliciete Upgrade domein wordt hervat. |
| ReportUpgradeHealth |tekenreeks, default is 'Admin' | Beveiligingsconfiguratie voor toepassingsupgrades met de huidige upgradevoortgang Hallo hervatten. |
| ReportHealth |tekenreeks, default is 'Admin' | Beveiligingsconfiguratie voor het melden van health. |
| ProvisionFabric |tekenreeks, default is 'Admin' | Beveiligingsconfiguratie voor MSI en de clusternaambron Manifest inrichten. |
| UpgradeFabric |tekenreeks, default is 'Admin' | Beveiligingsconfiguratie voor het starten van de cluster-upgrades. |
| RollbackFabricUpgrade |tekenreeks, default is 'Admin' | Beveiligingsconfiguratie voor de cluster-upgrades worden teruggedraaid. |
| UnprovisionFabric |tekenreeks, default is 'Admin' | Beveiligingsconfiguratie voor MSI en de clusternaambron Manifest ongedaan maken inrichting. |
| MoveNextFabricUpgradeDomain |tekenreeks, default is 'Admin' | Beveiligingsconfiguratie voor het hervatten van de cluster-upgrades met een expliciet is het upgraden van domein. |
| ReportFabricUpgradeHealth |tekenreeks, default is 'Admin' | Beveiligingsconfiguratie voor de cluster-upgrades met de huidige upgradevoortgang Hallo hervatten. |
| StartInfrastructureTask |tekenreeks, default is 'Admin' | Beveiligingsconfiguratie voor infrastructuurtaken starten. |
| FinishInfrastructureTask |tekenreeks, default is 'Admin' | Beveiligingsconfiguratie voor bijna afgelopen infrastructuurtaken. |
| ActivateNode |tekenreeks, default is 'Admin' | Beveiligingsconfiguratie voor activering van een knooppunt. |
| DeactivateNode |tekenreeks, default is 'Admin' | Beveiligingsconfiguratie voor het deactiveren van een knooppunt. |
| DeactivateNodesBatch |tekenreeks, default is 'Admin' | Beveiligingsconfiguratie voor het deactiveren van meerdere knooppunten. |
| RemoveNodeDeactivations |tekenreeks, default is 'Admin' | Beveiligingsconfiguratie voor omzetten deactivering op meerdere knooppunten. |
| GetNodeDeactivationStatus |tekenreeks, default is 'Admin' | Beveiligingsconfiguratie voor deactivering van de status controleren. |
| NodeStateRemoved |tekenreeks, default is 'Admin' | Beveiligingsconfiguratie voor het melden van status van het knooppunt verwijderd. |
| RecoverPartition |tekenreeks, default is 'Admin' | Beveiligingsconfiguratie voor het herstellen van een partitie. |
| RecoverPartitions |tekenreeks, default is 'Admin' | Beveiligingsconfiguratie voor herstel van partities. |
| RecoverServicePartitions |tekenreeks, default is 'Admin' | Beveiligingsconfiguratie voor herstel van servicepartities. |
| RecoverSystemPartitions |tekenreeks, default is 'Admin' | Beveiligingsconfiguratie voor herstel van partities voor systeem-service. |
| ReportFault |tekenreeks, default is 'Admin' | Beveiligingsconfiguratie voor rapportage van fouten. |
| InvokeInfrastructureCommand |tekenreeks, default is 'Admin' | Beveiligingsconfiguratie voor infrastructuur-opdrachten voor het beheer van taak. |
| FileContent |tekenreeks, default is 'Admin' | Beveiligingsconfiguratie voor de installatiekopie opslaan client bestandsoverdracht (externe toocluster). |
| FileDownload |tekenreeks, default is 'Admin' | Beveiligingsconfiguratie voor de image store client bestand downloaden Inleiding (externe toocluster). |
| InternalList |tekenreeks, default is 'Admin' | Beveiligingsconfiguratie voor de installatiekopie van bestand lijst clientbewerking (intern) opslaan. |
| Verwijderen |tekenreeks, default is 'Admin' | Beveiligingsconfiguratie voor de installatiekopie opslaan client delete-bewerking. |
| Uploaden |tekenreeks, default is 'Admin' | Beveiligingsconfiguratie voor de installatiekopie van het uploaden van clientbewerking opslaan. |
| GetStagingLocation |tekenreeks, default is 'Admin' | Beveiligingsconfiguratie voor de installatiekopie opslaan client tijdelijke locatie ophalen. |
| GetStoreLocation |tekenreeks, default is 'Admin' | Beveiligingsconfiguratie voor de installatiekopie opslaan client store locatie ophalen. |
| NodeControl |tekenreeks, default is 'Admin' | Beveiligingsconfiguratie voor gestart; wordt gestopt... en opnieuw starten van de knooppunten. |
| CodePackageControl |tekenreeks, default is 'Admin' | Beveiligingsconfiguratie voor pakketten van de code opnieuw te starten. |
| UnreliableTransportControl |tekenreeks, default is 'Admin' | Onbetrouwbaar Transport voor het toevoegen en verwijderen van gedrag. |
| MoveReplicaControl |tekenreeks, default is 'Admin' | Verplaats de replica. |
| PredeployPackageToNode |tekenreeks, default is 'Admin' | Deze api. |
| StartPartitionDataLoss |tekenreeks, default is 'Admin' | Induceert verlies van gegevens op een partitie. |
| StartPartitionQuorumLoss |tekenreeks, default is 'Admin' | Induceert quorumverlies op een partitie. |
| StartPartitionRestart |tekenreeks, default is 'Admin' | Sommige of alle Hallo-replica's van een partitie tegelijk opnieuw is opgestart. |
| CancelTestCommand |tekenreeks, default is 'Admin' | Hiermee annuleert u een specifieke TestCommand - als tijdens de vlucht. |
| StartChaos |tekenreeks, default is 'Admin' | Start Chaos - als deze nog niet is gestart. |
| StopChaos |tekenreeks, default is 'Admin' | Stopt Chaos - als deze is gestart. |
| StartNodeTransition |tekenreeks, default is 'Admin' | Beveiligingsconfiguratie voor de overgang van een knooppunt wordt gestart. |
| StartClusterConfigurationUpgrade |tekenreeks, default is 'Admin' | Induceert StartClusterConfigurationUpgrade op een partitie. |
| GetUpgradesPendingApproval |tekenreeks, default is 'Admin' | Induceert GetUpgradesPendingApproval op een partitie. |
| StartApprovedUpgrades |tekenreeks, default is 'Admin' | Induceert StartApprovedUpgrades op een partitie. |
| Ping |tekenreeks, de standaardwaarde is "Admin\|\|Gebruiker' | Beveiligingsconfiguratie voor client-pings. |
| Query’s uitvoeren |tekenreeks, de standaardwaarde is "Admin\|\|Gebruiker' | Beveiligingsconfiguratie voor query's. |
| NameExists |tekenreeks, de standaardwaarde is "Admin\|\|Gebruiker' | Beveiligingsconfiguratie voor naamgevings-URI bestaan controleert. |
| EnumerateSubnames |tekenreeks, de standaardwaarde is "Admin\|\|Gebruiker' | Beveiligingsconfiguratie voor naamgevings-URI-opsomming. |
| EnumerateProperties |tekenreeks, de standaardwaarde is "Admin\|\|Gebruiker' | Beveiligingsconfiguratie voor de naamgeving van de eigenschap opsomming. |
| PropertyReadBatch |tekenreeks, de standaardwaarde is "Admin\|\|Gebruiker' | Beveiligingsconfiguratie voor de eigenschap Naming leesbewerkingen. |
| GetServiceDescription |tekenreeks, de standaardwaarde is "Admin\|\|Gebruiker' | Beveiligingsconfiguratie voor de lange polling servicemeldingen en servicebeschrijvingen te lezen. |
| ResolveService |tekenreeks, de standaardwaarde is "Admin\|\|Gebruiker' | Beveiligingsconfiguratie voor de omzetting van de service op basis van een compatibel is. |
| ResolveNameOwner |tekenreeks, de standaardwaarde is "Admin\|\|Gebruiker' | Beveiligingsconfiguratie voor het oplossen van de eigenaar van de naamgevings-URI. |
| ResolvePartition |tekenreeks, de standaardwaarde is "Admin\|\|Gebruiker' | Beveiligingsconfiguratie voor het oplossen van systeemservices. |
| ServiceNotifications |tekenreeks, de standaardwaarde is "Admin\|\|Gebruiker' | Beveiligingsconfiguratie voor servicemeldingen op basis van gebeurtenissen. |
| PrefixResolveService |tekenreeks, de standaardwaarde is "Admin\|\|Gebruiker' | Beveiligingsconfiguratie voor de omzetting van de service op basis van een compatibele voorvoegsel. |
| GetUpgradeStatus |tekenreeks, de standaardwaarde is "Admin\|\|Gebruiker' | Beveiligingsconfiguratie voor polling upgradestatus van toepassing. |
| GetFabricUpgradeStatus |tekenreeks, de standaardwaarde is "Admin\|\|Gebruiker' | Beveiligingsconfiguratie voor polling upgradestatus van het cluster. |
| InvokeInfrastructureQuery |tekenreeks, de standaardwaarde is "Admin\|\|Gebruiker' | Beveiligingsconfiguratie voor het uitvoeren van query's infrastructuurtaken. |
| Lijst |tekenreeks, de standaardwaarde is "Admin\|\|Gebruiker' | Beveiligingsconfiguratie voor de installatiekopie opslaan clientbewerking bestand lijst. |
| ResetPartitionLoad |tekenreeks, de standaardwaarde is "Admin\|\|Gebruiker' | Beveiligingsconfiguratie voor de werklast opnieuw instellen voor een failoverUnit. |
| ToggleVerboseServicePlacementHealthReporting | tekenreeks, de standaardwaarde is "Admin\|\|Gebruiker' | Beveiligingsconfiguratie voor uitgebreide ServicePlacement HealthReporting schakelen. |
| GetPartitionDataLossProgress | tekenreeks, de standaardwaarde is "Admin\|\|Gebruiker' | Haalt Hallo uitgevoerd voor een api-aanroep van invoke gegevens verloren gaan. |
| GetPartitionQuorumLossProgress | tekenreeks, de standaardwaarde is "Admin\|\|Gebruiker' | Haalt Hallo uitgevoerd voor een api-aanroep van invoke quorum verloren gaan. |
| GetPartitionRestartProgress | tekenreeks, de standaardwaarde is "Admin\|\|Gebruiker' | Haalt Hallo uitgevoerd voor de api-aanroep voor een opnieuw opstarten. |
| GetChaosReport | tekenreeks, de standaardwaarde is "Admin\|\|Gebruiker' | Haalt status Hallo dank binnen een bepaald tijdsbereik. |
| GetNodeTransitionProgress | tekenreeks, de standaardwaarde is "Admin\|\|Gebruiker' | Beveiligingsconfiguratie voor het ophalen van de voortgang van een knooppunt overgang-opdracht. |
| GetClusterConfigurationUpgradeStatus | tekenreeks, de standaardwaarde is "Admin\|\|Gebruiker' | Induceert GetClusterConfigurationUpgradeStatus op een partitie. |
| GetClusterConfiguration | tekenreeks, de standaardwaarde is "Admin\|\|Gebruiker' | Induceert GetClusterConfiguration op een partitie. |

### <a name="section-name-reconfigurationagent"></a>Sectienaam: ReconfigurationAgent
| **Parameter** | **Toegestane waarden** | **Hulp of korte beschrijving** |
| --- | --- | --- |
| ApplicationUpgradeMaxReplicaCloseDuration | Tijd in seconden, de standaardwaarde is 900 |Geef de interval in seconden. Hallo duur voor welke Hallo systeem wachten moet alvorens de servicehosts die replica's die zijn achtergebleven in de sluiten wordt beëindigd. |
| ServiceApiHealthDuration | Tijd in seconden, de standaardwaarde is 30 minuten | Geef de interval in seconden. ServiceApiHealthDuration definieert hoe lang we wachten op een service API toorun voordat we het slecht rapporteren. |
| ServiceReconfigurationApiHealthDuration | Tijd in seconden, de standaardwaarde is 30 | Geef de interval in seconden. ServiceReconfigurationApiHealthDuration definieert hoe lang Hallo voordat een service in herconfiguratie als beschadigd is gemeld. |
| PeriodicApiSlowTraceInterval | Tijd in seconden, de standaardwaarde is 5 minuten | Geef de interval in seconden. PeriodicApiSlowTraceInterval definieert waarover wordt traag API-aanroepen worden ververst door Hallo API monitor hello-interval. |
| NodeDeactivationMaxReplicaCloseDuration | Tijd in seconden, de standaardwaarde is 900 | Geef de interval in seconden. Hallo maximumtijd toowait voordat een ServiceHost die deactivering van het knooppunt blokkeert wordt beëindigd. |
| FabricUpgradeMaxReplicaCloseDuration | Tijd in seconden, de standaardwaarde is 900 | Geef de interval in seconden. Hallo maximumduur RA moet wachten alvorens de ServiceHost van replica dat niet wordt gesloten wordt beëindigd. |
| IsDeactivationInfoEnabled | BOOL, de standaardwaarde is true | Hiermee wordt bepaald of RA deactivering info gebruiken voor het uitvoeren van de primaire opnieuw keuze voor nieuwe clusters voor deze configuratie moet worden ingesteld op tootrue voor bestaande clusters die worden geüpgraded Raadpleeg de releaseopmerkingen Hallo tooenable dit. |

### <a name="section-name-placementandloadbalancing"></a>Sectienaam: PlacementAndLoadBalancing
| **Parameter** | **Toegestane waarden** | **Hulp of korte beschrijving** |
| --- | --- | --- |
| TraceCRMReasons |BOOL, de standaardwaarde is true |Hiermee geeft u op of tootrace redenen voor CRM verplaatsingen toohello operationele gebeurtenissen kanaal uitgegeven. |
| ValidatePlacementConstraint | BOOL, de standaardwaarde is true | Hiermee geeft u op of Hallo PlacementConstraint-expressie voor een service wordt gevalideerd wanneer een service ServiceDescription wordt bijgewerkt. |
| PlacementConstraintValidationCacheSize | Int, de standaardwaarde is 10000 | Limieten Hallo grootte van de tabel Hallo gebruikt voor de snelle validatie en in cache plaatsen van plaatsing beperking expressies. |
|VerboseHealthReportLimit | Int, de standaardwaarde is 20 | Hiermee definieert u Hallo aantal keren dat een replica niet-geplaatste toogo heeft voordat een waarschuwing wordt gemeld voor (als uitgebreide health reporting is ingeschakeld). |
|ConstraintViolationHealthReportLimit | Int, de standaardwaarde is 50 | Definieert Hallo aantal keren beperking schenden replica toobe blijft niet-opgeloste heeft voordat diagnostische gegevens worden uitgevoerd, en statusrapporten worden verzonden. |
|DetailedConstraintViolationHealthReportLimit | Int, de standaardwaarde is 200 | Definieert Hallo aantal keren beperking schenden replica toobe blijft niet-opgeloste heeft voordat diagnostische gegevens worden uitgevoerd en gedetailleerde statusrapporten worden verzonden. |
|DetailedVerboseHealthReportLimit | Int, de standaardwaarde is 200 | Hiermee definieert u Hallo aantal keren dat een niet-geplaatste replica heeft toobe blijft niet-geplaatste voordat de gezondheid van gedetailleerde rapporten worden verzonden. |
|ConsecutiveDroppedMovementsHealthReportLimit | Int, de standaardwaarde is 20 | Hiermee definieert u Hallo vaak achter elkaar dat ResourceBalancer uitgegeven verplaatsingen zijn verwijderd voordat diagnostische gegevens worden uitgevoerd en waarschuwingen worden gegenereerd. Negatief: Er zijn geen waarschuwingen verzonden onder deze voorwaarde. |
|DetailedNodeListLimit | Int, de standaardwaarde is 15 | Definieert het aantal knooppunten per beperking tooinclude voordat afkapping Hallo in Hallo die replica niet-geplaatste rapporten. |
|DetailedPartitionListLimit | Int, de standaardwaarde is 15 | Aantal partities per diagnostische vermelding voor een beperking tooinclude voordat afkapping Hallo definieert in diagnostische gegevens. |
|DetailedDiagnosticsInfoListLimit | Int, de standaardwaarde is 15 | Hiermee definieert u Hallo aantal diagnose-items (met gedetailleerde informatie) per beperking tooinclude voordat moet worden afgekapt in diagnostische gegevens.|
|PLBRefreshGap | Tijd in seconden, de standaardwaarde is 1 | Geef de interval in seconden. Hallo minimale hoeveelheid tijd die moet worden gewacht voordat de PLB wordt vernieuwd status opnieuw definieert. |
|MinPlacementInterval | Tijd in seconden, de standaardwaarde is 1 | Geef de interval in seconden. Minimale hoeveelheid tijd die voordat u twee opeenvolgende plaatsing patronen verstrijken moet Hallo definieert. |
|MinConstraintCheckInterval | Tijd in seconden, de standaardwaarde is 1 | Geef de interval in seconden. Minimale hoeveelheid tijd die moet worden gewacht voordat er twee opeenvolgende beperking controleren Rondt Hallo definieert. |
|MinLoadBalancingInterval | Tijd in seconden, de standaardwaarde is 5 | Geef de interval in seconden. Minimale hoeveelheid tijd die voordat u twee opeenvolgende taakverdeling patronen verstrijken moet Hallo definieert. |
|BalancingDelayAfterNodeDown | Tijd in seconden, de standaardwaarde is 120 |Geef de interval in seconden. Start niet balancing activiteiten binnen deze periode na een knooppunt omlaag gebeurtenis. |
|BalancingDelayAfterNewNode | Tijd in seconden, de standaardwaarde is 120 |Geef de interval in seconden. Start niet balancing activiteiten binnen deze periode na het toevoegen van een nieuw knooppunt. |
|ConstraintFixPartialDelayAfterNodeDown | Tijd in seconden, de standaardwaarde is 120 | Geef de interval in seconden. Geen herstel FaultDomain en UpgradeDomain schendingen van plaatsingsbeperkingen binnen deze periode na een knooppunt omlaag gebeurtenis doen. |
|ConstraintFixPartialDelayAfterNewNode | Tijd in seconden, de standaardwaarde is 120 | Geef de interval in seconden. DDo FaultDomain niet oplossen en schendingen van plaatsingsbeperkingen UpgradeDomain binnen deze periode na het toevoegen van een nieuw knooppunt. |
|GlobalMovementThrottleThreshold | Uint, de standaardwaarde is 1000 | Maximum aantal verplaatsingen van het type toegestaan in Balancing fase in de afgelopen Hallo Hallo interval wordt aangegeven door GlobalMovementThrottleCountingInterval. |
|GlobalMovementThrottleThresholdForPlacement | Uint, de standaardwaarde is 0 | Maximum aantal verplaatsingen van het type toegestaan in de fase van de plaatsing in Hallo afgelopen interval aangegeven door GlobalMovementThrottleCountingInterval.0 geeft geen limiet.|
|GlobalMovementThrottleThresholdForBalancing | Uint, de standaardwaarde is 0 | Maximum aantal verplaatsingen van het type toegestaan in de fase Netwerktaakverdeling in Hallo afgelopen interval wordt aangegeven door GlobalMovementThrottleCountingInterval. 0 geeft geen limiet. |
|GlobalMovementThrottleCountingInterval | Tijd in seconden, de standaardwaarde is 600 | Geef de interval in seconden. Hallo-lengte van Hallo geven voorbij interval voor welke tootrack per domein replica verplaatsingen (gebruikt samen met GlobalMovementThrottleThreshold). Kan worden too0 tooignore globale beperking helemaal niet ingesteld. |
|MovementPerPartitionThrottleThreshold | Uint, de standaardwaarde is 50 | Geen balancing gerelateerde verkeer wordt uitgevoerd voor een partitie als Hallo aantal balancing gerelateerde verplaatsingen voor replica's van de betreffende partitie heeft bereikt of overschreden MovementPerFailoverUnitThrottleThreshold in Hallo afgelopen interval wordt aangegeven door MovementPerPartitionThrottleCountingInterval. |
|MovementPerPartitionThrottleCountingInterval | Tijd in seconden, de standaardwaarde is 600 | Geef de interval in seconden. Hallo-lengte van Hallo geven voorbij interval voor welke tootrack replica verplaatsingen voor elke partitie (gebruikt samen met MovementPerPartitionThrottleThreshold). |
|PlacementSearchTimeout | Tijd in seconden, de standaardwaarde is 0,5 | Geef de interval in seconden. Bij het plaatsen van services; zoeken naar maximaal deze lang voordat een resultaat te retourneren. |
|UseMoveCostReports | BOOL, de standaardwaarde is ONWAAR | Hiermee geeft u Hallo LB tooignore Hallo kostenelement Hallo score berekenen voor de functie; resulterende potentieel grote aantal om betere taakverdeling plaatsing verplaatsen. |
|PreventTransientOvercommit | BOOL, de standaardwaarde is ONWAAR | Hiermee wordt bepaald moet PLB onmiddellijk worden geteld voor resources die worden vrijgemaakt door Hallo geïnitieerd verplaatst. Standaard; PLB kunt verplaatsen uit Start en op hetzelfde knooppunt wat kan leiden tot tijdelijke overcommit Hallo in verplaatsen. Instelling voor deze parameter tootrue voorkomt u dat de soort overcommits en op aanvraag defragmentatie (aka placementWithMove) wordt uitgeschakeld. |
|InBuildThrottlingEnabled | BOOL, de standaardwaarde is ONWAAR | Bepalen of het Hallo-build-beperking is ingeschakeld. |
|InBuildThrottlingAssociatedMetric | tekenreeks, standaardwaarde is "" | Hallo gekoppelde metrische naam op voor deze beperking. |
|InBuildThrottlingGlobalMaxValue | Int, de standaardwaarde is 0 |maximale aantal Hallo van-build-replica's globaal toegestaan. |
|SwapPrimaryThrottlingEnabled | BOOL, de standaardwaarde is ONWAAR| Bepalen of Hallo swap-primaire beperking is ingeschakeld. |
|SwapPrimaryThrottlingAssociatedMetric | tekenreeks, standaardwaarde is ""| Hallo gekoppelde metrische naam op voor deze beperking. |
|SwapPrimaryThrottlingGlobalMaxValue | Int, de standaardwaarde is 0 | Hallo maximale aantal van de wisseling primaire replica's globaal toegestaan. |
|PlacementConstraintPriority | Int, de standaardwaarde is 0 | Bepaalt de prioriteit Hallo van plaatsing beperking: 0: vaste; 1: zachte; negatieve: negeren. |
|PreferredLocationConstraintPriority | Int, de standaardwaarde is 2| Bepaalt de prioriteit van voorkeur locatiebeperking Hallo: 0: vaste; 1: zachte; 2: optimalisatie; negatieve: negeren |
|CapacityConstraintPriority | Int, de standaardwaarde is 0 | Bepaalt de prioriteit Hallo van capaciteit beperking: 0: vaste; 1: zachte; negatieve: negeren. |
|AffinityConstraintPriority | Int, de standaardwaarde is 0 | Bepaalt de prioriteit Hallo van affiniteit beperking: 0: vaste; 1: zachte; negatieve: negeren. |
|FaultDomainConstraintPriority | Int, de standaardwaarde is 0 | Bepaalt de prioriteit Hallo van fouttolerantie domeinbeperking: 0: vaste; 1: zachte; negatieve: negeren. |
|UpgradeDomainConstraintPriority | Int, de standaardwaarde is 1| Bepaalt de prioriteit Hallo van upgradedomein beperking: 0: vaste; 1: zachte; negatieve: negeren. |
|ScaleoutCountConstraintPriority | Int, de standaardwaarde is 0 | Bepaalt de prioriteit Hallo van scaleout aantal beperking: 0: vaste; 1: zachte; negatieve: negeren. |
|ApplicationCapacityConstraintPriority | Int, de standaardwaarde is 0 | Bepaalt de prioriteit Hallo van capaciteit beperking: 0: vaste; 1: zachte; negatieve: negeren. |
|MoveParentToFixAffinityViolation | BOOL, de standaardwaarde is ONWAAR | Instelling die bepaalt of de bovenliggende replica's kunnen worden verplaatst toofix affiniteit beperkingen.|
|MoveExistingReplicaForPlacement | BOOL, de standaardwaarde is true |Instelling die bepaalt of de bestaande replica toomove tijdens de plaatsing. |
|UseSeparateSecondaryLoad | BOOL, de standaardwaarde is true | Instelling die bepaalt of andere secundaire load gebruiken. |
|PlaceChildWithoutParent | BOOL, de standaardwaarde is true | Instelling die bepaalt of de onderliggende service replica kan worden geplaatst als er geen bovenliggende replica actief is. |
|PartiallyPlaceServices | BOOL, de standaardwaarde is true | Bepaalt of alle service-replica's in het cluster wordt geplaatst als 'Alles of niets' gegeven beperkt geschikte knooppunten voor hen.|
|InterruptBalancingForAllFailoverUnitUpdates | BOOL, de standaardwaarde is ONWAAR | Bepaalt of elk type failover-eenheid update moet snel interrupt of traag Netwerktaakverdeling uitvoeren. Met de opgegeven 'false' Netwerktaakverdeling uitvoeren wordt onderbroken als FailoverUnit: is gemaakt/verwijderd; ontbrekende replica's; locatie van de primaire replica of gewijzigde aantal replica's worden gewijzigd. Netwerktaakverdeling uitvoeren wordt niet onderbroken in andere gevallen - als FailoverUnit: heeft extra replica's; een replica-vlag; gewijzigd alleen de versie van de partitie of ander gewijzigd. |

### <a name="section-name-security"></a>Sectienaam: beveiliging
| **Parameter** | **Toegestane waarden** | **Hulp of korte beschrijving** |
| --- | --- | --- |
| ClusterProtectionLevel |Geen of EncryptAndSign |Geen (standaard) voor de niet-beveiligde clusters, EncryptAndSign voor beveiligde clusters. |

### <a name="section-name-hosting"></a>Sectienaam: die als host fungeert
| **Parameter** | **Toegestane waarden** | **Hulp of korte beschrijving** |
| --- | --- | --- |
| ServiceTypeRegistrationTimeout |Tijd in seconden, is standaard 300 |Maximale tijd waarbinnen Hallo ServiceType toobe geregistreerd met fabric |
| ServiceTypeDisableFailureThreshold |Geheel getal van de standaardwaarde is 1 |Dit is Hallo drempelwaarde voor hello aantal mislukte waarna FailoverManager (FM) is een melding toodisable Hallo servicetype op dat knooppunt en probeer een ander knooppunt voor plaatsing. |
| ActivationRetryBackoffInterval |Tijd in seconden, de standaardwaarde is 5 |Backoff interval op om de activering is mislukt; Op elke continue activeringsfout Hallo Hallo system pogingen activering voor up toohello MaxActivationFailureCount. Hallo-interval voor opnieuw proberen op elke probeer is een product van continue activering mislukt en Hallo activering back-off-interval. |
| ActivationMaxRetryInterval |Tijd in seconden, is standaard 300 |Op elke continue activeringsfout Hallo Hallo system pogingen activering voor up tooActivationMaxFailureCount. ActivationMaxRetryInterval bevat de tijdsinterval wacht voordat u opnieuw proberen na elke activering is mislukt |
| ActivationMaxFailureCount |Geheel getal van de standaardwaarde is 10 |Hoe vaak system pogingen activering voordat geeft mislukt |

### <a name="section-name-failovermanager"></a>Sectienaam: FailoverManager
| **Parameter** | **Toegestane waarden** | **Hulp of korte beschrijving** |
| --- | --- | --- |
| PeriodicLoadPersistInterval |Tijd in seconden, de standaardwaarde is 10 |Hiermee wordt bepaald hoe vaak Hallo FM controleren op nieuwe load-rapporten |

### <a name="section-name-federation"></a>Sectienaam: Federation
| **Parameter** | **Toegestane waarden** | **Hulp of korte beschrijving** |
| --- | --- | --- |
| LeaseDuration |Tijd in seconden, de standaardwaarde is 30 |De duur die een lease tussen een knooppunt en de bijbehorende neighbors duurt. |
| LeaseDurationAcrossFaultDomain |Tijd in seconden, de standaardwaarde is 30 |De duur die een lease tussen een knooppunt en de bijbehorende neighbors tussen domeinen met fouten duurt. |

### <a name="section-name-clustermanager"></a>Sectienaam: ClusterManager
| **Parameter** | **Toegestane waarden** | **Hulp of korte beschrijving** |
| --- | --- | --- |
| UpgradeStatusPollInterval |Tijd in seconden, de standaardwaarde is 60 |Hallo frequentie van polling voor de upgradestatus van toepassing. Deze waarde bepaalt de snelheid van de update voor elke aanroep GetApplicationUpgradeProgress Hallo |
| UpgradeHealthCheckInterval |Tijd in seconden, de standaardwaarde is 60 |Hallo frequentie van de status controleert tijdens een upgrades van de bewaakte toepassingen |
| FabricUpgradeStatusPollInterval |Tijd in seconden, de standaardwaarde is 60 |Hallo frequentie van polling voor Fabric-upgrade-status. Deze waarde bepaalt de snelheid van de update voor elke aanroep GetFabricUpgradeProgress Hallo |
| FabricUpgradeHealthCheckInterval |Tijd in seconden, de standaardwaarde is 60 |Hallo frequentie van de statuscontrole tijdens een bewaakte Fabric-upgrade |
|InfrastructureTaskProcessingInterval | Tijd in seconden, de standaardwaarde is 10 |Geef de interval in seconden. Hallo verwerkingsinterval door Hallo infrastructuur taakverwerking statusmachine gebruikt. |
|TargetReplicaSetSize |Int, de standaardwaarde is 7 |Hello TargetReplicaSetSize voor ClusterManager. |
|MinReplicaSetSize |Int, de standaardwaarde is 3 |Hello MinReplicaSetSize voor ClusterManager. |
|ReplicaRestartWaitDuration |Tijd in seconden, de standaardwaarde is (60,0 * 30)|Geef de interval in seconden. Hello ReplicaRestartWaitDuration voor ClusterManager. |
|QuorumLossWaitDuration |Tijd in seconden, de standaardwaarde is MaxValue | Geef de interval in seconden. Hello QuorumLossWaitDuration voor ClusterManager. |
|StandByReplicaKeepDuration | Tijd in seconden, de standaardwaarde is (3600.0 * 2)|Geef de interval in seconden. Hello StandByReplicaKeepDuration voor ClusterManager. |
|PlacementConstraints | tekenreeks, standaardwaarde is "" |Hello PlacementConstraints voor ClusterManager. |
|SkipRollbackUpdateDefaultService | BOOL, de standaardwaarde is ONWAAR |Hallo CM wordt omzetten bijgewerkte standaardservices overslaan tijdens de upgrade terugdraaien van de toepassing. |
|EnableDefaultServicesUpgrade | BOOL, de standaardwaarde is ONWAAR |Upgraden standaardservices inschakelen tijdens de upgrade van de toepassing. Beschrijvingen van de standaardservice zou na de upgrade worden overschreven. |
|InfrastructureTaskHealthCheckWaitDuration |Tijd in seconden, de standaardwaarde is 0| Geef de interval in seconden. Hallo hoeveelheid tijd toowait voordat u begint statuscontroles na het verwerken van een taak infrastructuur na. |
|InfrastructureTaskHealthCheckStableDuration | Tijd in seconden, de standaardwaarde is 0| Geef de interval in seconden. Hallo hoeveelheid tijd tooobserve opeenvolgende doorgegeven health controleert voordat na verwerking van de taak van een infrastructuur met succes voltooid wordt. Een mislukte statuscontrole geobserveerd, wordt deze timer opnieuw ingesteld. |
|InfrastructureTaskHealthCheckRetryTimeout | Tijd in seconden, de standaardwaarde is 60 |Geef de interval in seconden. Hallo hoeveelheid tijd toospend opnieuw uit te voeren tijdens het verwerken van een taak infrastructuur na een mislukte statuscontroles. Doorgegeven statuscontrole geobserveerd, wordt deze timer opnieuw ingesteld. |
|ImageBuilderTimeoutBuffer |Tijd in seconden, de standaardwaarde is 3 |Geef de interval in seconden. Hallo hoeveelheid tijd tooallow voor Image Builder opgegeven time-out fouten tooreturn toohello client. Als deze buffer te klein is. Hallo-client wordt vervolgens een time-out optreedt voordat de Hallo en opgehaald van een algemene time-outfout. |
|MinOperationTimeout | Tijd in seconden, de standaardwaarde is 60 |Geef de interval in seconden. Hallo minimale globale time-out voor intern verwerkingen op ClusterManager. |
|MaxOperationTimeout |Tijd in seconden, de standaardwaarde is MaxValue | Geef de interval in seconden. Hallo maximale algemene time-out voor intern verwerkingen op ClusterManager. |
|MaxTimeoutRetryBuffer | Tijd in seconden, de standaardwaarde is 600 |Geef de interval in seconden. time-out voor maximale bewerking Hallo als opnieuw intern wordt uitgevoerd vanwege tootimeouts is <Original Timeout>  +  <MaxTimeoutRetryBuffer>. Aanvullende time-out wordt in stappen van MinOperationTimeout toegevoegd. |
|MaxCommunicationTimeout |Tijd in seconden, de standaardwaarde is 600 |Geef de interval in seconden. Hallo maximale time-out voor interne communicatie tussen ClusterManager en andere systeemservices (dat wil zeggen; Naamgevingsservice; Failover Manager en enzovoort). Deze time-out moet kleiner zijn dan globale MaxOperationTimeout (zoals het is mogelijk meerdere communicatie tussen onderdelen van het systeem voor elke clientbewerking). |
|MaxDataMigrationTimeout |Tijd in seconden, de standaardwaarde is 600 |Geef de interval in seconden. Hallo maximale time-out voor data recovery migratiebewerkingen nadat een Fabric-upgrade heeft plaatsgevonden. |
|MaxOperationRetryDelay |Tijd in seconden, de standaardwaarde is 5| Geef de interval in seconden. Hallo maximale vertraging voor interne pogingen wanneer er fouten zijn opgetreden. |
|ReplicaSetCheckTimeoutRollbackOverride |Tijd in seconden, is standaard 1200 | Geef de interval in seconden. Als ReplicaSetCheckTimeout toohello maximale DWORD-waarde; is ingesteld vervolgens wordt deze overschreven met Hallo-waarde van deze configuratie voor de toepassing hello terugdraaiactie heeft plaatsgevonden. Hallo-waarde gebruikt voor het vooruitrollen is nooit genegeerd. |
|ImageBuilderJobQueueThrottle |Int, de standaardwaarde is 10 |Aantal versnelling voor Image Builder proxy taakwachtrij van toepassingsaanvragen thread. |

## <a name="next-steps"></a>Volgende stappen
Lees deze artikelen voor meer informatie over het Clusterbeheer:

[Toevoegen, overschakelen, certificaten uit uw Azure-cluster verwijderen](service-fabric-cluster-security-update-certs-azure.md) 

