---
title: Voorbereiding voor implementatie van Service Fabric zelfstandige Cluster aaaAzure | Microsoft Docs
description: Documentatie gerelateerd toopreparing Hallo omgeving en voor het maken van de clusterconfiguratie Hallo toobe beschouwd als eerdere toodeploying een cluster dat is bedoeld voor het verwerken van een productie-werkbelasting.
services: service-fabric
documentationcenter: .net
author: maburlik
manager: timlt
editor: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 1/17/2017
ms.author: maburlik;chackdan
ms.openlocfilehash: e503c61a64b408af3f22bd75ab02f1c34ac9f380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
<a id="preparemachines"></a>

## <a name="plan-and-prepare-your-service-fabric-standalone-cluster-deployment"></a>Plannen en voorbereiden van uw implementatie van Service Fabric zelfstandige cluster
Hallo volgende stappen uit voordat u uw cluster maken uitvoeren.

### <a name="step-1-plan-your-cluster-infrastructure"></a>Stap 1: Uw clusterinfrastructuur plannen
U bent over toocreate Service Fabric-cluster op computers die u eigenaar bent, zodat u kunt beslissen welke soorten fouten die u wilt dat cluster toosurvive Hallo. Bijvoorbeeld, moet u de afzonderlijke power regels of Internet-verbindingen opgegeven toothese machines? Overweeg daarnaast Hallo fysieke beveiliging van deze apparaten. Waarbij Hallo machines zich bevinden en die behoefte hebben aan toegang toothem? Nadat u deze beslissingen nemen, kunt u logisch toewijzen Hallo machines toohello verschillende domeinen met fouten (Zie stap 4). Hallo-infrastructuur plannen voor productieclusters is meer betrokken dan voor testclusters.

### <a name="step-2-prepare-hello-machines-toomeet-hello-prerequisites"></a>Stap 2: Bereid Hallo machines toomeet Hallo-vereisten
Vereisten voor elke computer die u wilt dat tooadd toohello cluster:

* Minimaal 16 GB RAM-geheugen wordt aanbevolen.
* Een minimum van 40 GB beschikbare schijfruimte wordt aanbevolen.
* Een core 4 of hoger CPU wordt aanbevolen.
* Connectiviteit tooa beveiligd netwerk of netwerken voor alle machines.
* Windows Server 2012 R2 of WindowsServer 2016. 
* [.NET framework 4.5.1 of hoger](https://www.microsoft.com/download/details.aspx?id=40773), volledige installatie.
* [Windows PowerShell 3.0](https://msdn.microsoft.com/powershell/scripting/setup/installing-windows-powershell).
* Hallo [RemoteRegistry service](https://technet.microsoft.com/library/cc754820) moet worden uitgevoerd op alle Hallo-machines.

Hallo Clusterbeheer implementeren en configureren van Hallo cluster moet hebben [administrator-bevoegdheden](https://social.technet.microsoft.com/wiki/contents/articles/13436.windows-server-2012-how-to-add-an-account-to-a-local-administrator-group.aspx) op elk van Hallo-machines. U kunt Service Fabric niet installeren op een domeincontroller.

### <a name="step-3-determine-hello-initial-cluster-size"></a>Stap 3: De eerste clustergrootte Hallo bepalen
Elk knooppunt in een zelfstandige Service Fabric-cluster heeft Hallo Service Fabric-runtime geïmplementeerd en is een lid van Hallo-cluster. In een standaard productie-implementatie is het een knooppunt per besturingssysteemexemplaar (fysiek of virtueel). Hallo clustergrootte wordt bepaald door uw bedrijfsbehoeften. U moet echter een minimale clustergrootte van drie knooppunten (machines of virtuele machines) hebben.
U kunt meer dan één knooppunt voor ontwikkelingsdoeleinden hebben op een bepaalde computer. Service Fabric biedt ondersteuning voor slechts één knooppunt per fysieke of virtuele machine in een productieomgeving.

### <a name="step-4-determine-hello-number-of-fault-domains-and-upgrade-domains"></a>Stap 4: Het aantal foutdomeinen Hallo bepalen en domeinen upgraden
Een *foutdomein* (FD) is een fysieke eenheid van de fout en is direct gerelateerd toohello fysieke infrastructuur in Hallo datacenters. Een foutdomein bestaat uit de hardwareonderdelen (computers, switches, netwerken en meer) die delen van een potentieel risico. Hoewel er geen 1:1-toewijzing tussen domeinen met fouten en rekken, kan los spreken elk rack worden overwogen een domein met fouten. Wanneer u overweegt Hallo knooppunten in het cluster, wordt aangeraden dat Hallo knooppunten worden verdeeld over ten minste drie domeinen met fouten.

Wanneer u FDs in ClusterConfig.json opgeeft, kunt u Hallo naam op voor elke FD. Service Fabric ondersteunt hiërarchische FDs zodat u kunt de infrastructuurtopologie van uw erin spiegelen.  Bijvoorbeeld, zijn Hallo volgende FDs geldig:

* 'faultDomain': ' fd: / Rack1-Room1/Machine1 '
* 'faultDomain': ' fd: / FD1 '
* 'faultDomain': ' fd: / Room1/Rack1/PDU1/M1 '

Een *upgradedomein* (UD) is een logische eenheid van knooppunten. Tijdens upgrades van de Service Fabric gedirigeerd (een upgrade van de toepassing of het upgraden van een cluster), worden alle knooppunten in een UD offline gezet tooperform Hallo upgrade terwijl knooppunten in andere UDs beschikbaar tooserve aanvragen blijven. Hallo firmware bijwerken u op uw computers uitvoeren komen niet inwilligen UDs, dus moet u ze een doen machines tegelijk.

Hallo eenvoudigste manier toothink over deze concepten is tooconsider FDs als eenheid Hallo van niet-geplande storingen en UDs Hallo eenheid gepland onderhoud.

Wanneer u UDs in ClusterConfig.json opgeeft, kunt u Hallo naam op voor elke UD. Hallo na namen zijn bijvoorbeeld geldig:

* 'upgradeDomain': 'UD0'
* 'upgradeDomain': 'UD1A'
* 'upgradeDomain': 'DomainRed'
* "upgradeDomain": "Blue"

Zie voor meer informatie over upgradedomeinen en domeinen met fouten, [met een beschrijving van een Service Fabric-cluster](service-fabric-cluster-resource-manager-cluster-description.md).

### <a name="step-5-download-hello-service-fabric-standalone-package-for-windows-server"></a>Stap 5: Hallo Service Fabric zelfstandige pakket voor Windows Server downloaden
[Windows-Server - Service Fabric zelfstandige Package - koppeling downloaden](http://go.microsoft.com/fwlink/?LinkId=730690) en pak Hallo pakket, de implementatie van beide tooa machine die geen deel uit van de cluster Hallo of tooone Hallo-machines die een deel van uw cluster zal zijn.

### <a name="step-6-modify-cluster-configuration"></a>Stap 6: Configuratie van het cluster wijzigen
een zelfstandige cluster toocreate hebt toocreate een zelfstandige cluster ClusterConfig.json configuratiebestand, waarin wordt beschreven Hallo-specificatie van het Hallo-cluster. U kunt baseren Hallo-configuratiebestand op Hallo sjablonen gevonden op Hallo onderstaande koppeling. <br>
[Zelfstandige clusterconfiguraties](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)

Zie voor informatie over de secties in dit bestand hello, [configuratie-instellingen voor Windows-cluster zelfstandige](service-fabric-cluster-manifest.md).

Open een Hallo ClusterConfig.json bestanden uit Hallo pakket die u hebt gedownload en Hallo volgende instellingen wijzigen:
| **Configuratie-instelling** | **Beschrijving** |
| --- | --- |
| **NodeTypes** |Knooppunttypen kunnen u tooseparate uw clusterknooppunten in verschillende groepen. Een cluster moet ten minste één NodeType hebben. Alle knooppunten in een groep hebt Hallo gemeenschappelijke kenmerken te volgen: <br> **Naam** -dit Hallo knooppunt typenaam is. <br>**Eindpuntpoorten** - deze heten verschillende eindpunten (poorten) die gekoppeld aan dit knooppunttype zijn. U kunt een ander poortnummer die u wenst, zolang ze geen conflict met iets anders in dit manifest veroorzaken en zijn niet al in gebruik door een andere toepassing die wordt uitgevoerd op Hallo VM-machine. <br> **Plaatsingseigenschappen** -deze beschrijving van eigenschappen voor dit knooppunttype dat u als plaatsingsbeperkingen voor systeemservices Hallo of uw services gebruikt. Deze eigenschappen zijn de gebruiker gedefinieerde sleutel/waarde-paren die extra meta-gegevens voor een bepaald knooppunt bieden. Voorbeelden van eigenschappen van het knooppunt is of Hallo knooppunt heeft een harde schijf of videokaart, Hallo aantal aandrijfassen in de harde schijf, kernen en andere fysieke eigenschappen. <br> **Capaciteitswaarden** -knooppunt capaciteiten Hallo naam en een bepaalde bron hoeveelheid definiëren dat een bepaald knooppunt beschikbaar voor verbruik is. Een knooppunt kan bijvoorbeeld dat er capaciteit voor een metriek 'MemoryInMb' genoemd en 2048 MB beschikbare schijfruimte heeft standaard definiëren. Deze capaciteit worden op runtime tooensure dat services waarvoor bepaalde hoeveelheden resources worden geplaatst op Hallo knooppunten dat deze bronnen beschikbaar zijn in Hallo bedragen vereist gebruikt.<br>**IsPrimary** - als er meer dan een NodeType gedefinieerd ervoor te zorgen dat slechts één tooprimary met Hallo-waarde is ingesteld *true*, namelijk waarin Hallo systeemservices uitvoeren. Alle andere knooppunttypen toohello waarde moeten worden ingesteld *false* |
| **Knooppunten** |Dit zijn Hallo details voor elke Hallo knooppunten die deel van het Hallo-cluster (knooppunttype, naam van het knooppunt IP-adres, foutdomein en upgradedomein van Hallo knooppunt uitmaken). Hallo machines u Hallo cluster toobe gemaakt op de noodzaak toobe hier vermeld met hun IP-adressen. <br> Als u Hallo hetzelfde IP-adres voor alle knooppunten van hello, wordt een 1-box-cluster is gemaakt, die u gebruiken kunt voor testdoeleinden gebruiken. Gebruik geen 1-box-clusters voor het implementeren van productie-workloads. |

Nadat de configuratie van het cluster Hallo heeft alle geconfigureerde instellingen toohello omgeving, kan het worden getest tegen Hallo clusteromgeving (stap 7).

<a id="environmentsetup"></a>

### <a name="step-7-environment-setup"></a>Stap 7. Omgeving instellen

Wanneer een Clusterbeheerder een zelfstandige Service Fabric-cluster configureert, is Hallo omgeving moet toobe instellen met de volgende criteria Hallo: <br>
1. Hallo-gebruiker maken Hallo cluster hebt beheerder beveiligingsniveau bevoegdheden tooall machines die worden vermeld als knooppunten in het configuratiebestand Hallo-cluster.
2. Machine uit welke Hallo cluster is gemaakt, evenals op elke machine cluster-knooppunt moet:
* Service Fabric SDK verwijderd hebben
* Service Fabric-runtime verwijderd hebben 
* Hebben hello Windows firewallservice (mpsvc) ingeschakeld
* Hallo Remote Registry-Service (remoteregistry) ingeschakeld
* Bestand die delen (SMB) ingeschakeld
* Hebt u nodig poorten die worden geopend, op basis van poorten voor cluster-configuratie
* Nodig poorten zijn geopend voor Windows SMB en Remote Registry-service: 135, 137, 138, 139 en 445
* Network connectivity tooone hebben een ander
3. Geen Hallo cluster knooppunt machines moet een domeincontroller.
4. Valideren Hallo noodzakelijke beveiliging vereiste onderdelen zijn plaats en tegen Hallo configuratie correct zijn geconfigureerd als een beveiligde cluster Hallo cluster toobe geïmplementeerd is.
5. Als de clustermachines Hallo niet toegankelijk is via het internet, clusterconfiguratie set Hallo volgende in Hallo:
* Telemetrie uitschakelen: onder *eigenschappen* ingesteld *'enableTelemetry': false*
* Uitschakelen van automatische meldingen die Hallo huidige cluster versie nadert ondersteuning eindigt & downloaden van de Fabric-versie: onder *eigenschappen* ingesteld *'fabricClusterAutoupgradeEnabled': false*
* U kunt ook als internet toegang tot het netwerk beperkte toowhite vermeld domeinen is, Hallo-domeinen die hieronder zijn vereist voor automatische upgrade: go.microsoft.com download.microsoft.com

6. Toepasselijke antivirussoftware Service Fabric-uitsluitingen instellen:

| **Antivirussoftware uitgesloten mappen** |
| --- |
| Program Files\Microsoft Service Fabric |
| FabricDataRoot (van de configuratie van het cluster) |
| FabricLogRoot (van de configuratie van het cluster) |

| **Antivirussoftware uitgesloten processen** |
| --- |
| Fabric.exe |
| FabricHost.exe |
| FabricInstallerService.exe |
| FabricSetup.exe |
| FabricDeployer.exe |
| ImageBuilder.exe |
| FabricGateway.exe |
| FabricDCA.exe |
| FabricFAS.exe |
| FabricUOS.exe |
| FabricRM.exe |
| FileStoreService.exe |

### <a name="step-8-validate-environment-using-testconfiguration-script"></a>Stap 8. Omgeving met TestConfiguration script valideren
Hallo TestConfiguration.ps1 script vindt u in Hallo zelfstandige pakket. Het is gebruikt als een Best Practices Analyzer toovalidate enkele Hallo criteria bovenstaande en moet worden gebruikt als een selectievakje sanity toovalidate of een cluster kan worden geïmplementeerd op een bepaalde omgeving. Als er een storing, Raadpleeg de lijst onder toohello [omgeving in te stellen](service-fabric-cluster-standalone-deployment-preparation.md) voor het oplossen van problemen. 

Dit script kan worden uitgevoerd op een machine met de beheerder toegang tooall Hallo machines die worden vermeld als knooppunten in het configuratiebestand Hallo-cluster. Hallo-machine die op dit script wordt uitgevoerd heeft geen toobe onderdeel van Hallo-cluster.

```powershell
PS C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer> .\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json
Trace folder already exists. Traces will be written tooexisting trace folder: C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer\DeploymentTraces
Running Best Practices Analyzer...
Best Practices Analyzer completed successfully.


LocalAdminPrivilege        : True
IsJsonValid                : True
IsCabValid                 : True
RequiredPortsOpen          : True
RemoteRegistryAvailable    : True
FirewallAvailable          : True
RpcCheckPassed             : True
NoConflictingInstallations : True
FabricInstallable          : True
Passed                     : True
```

Momenteel wordt deze configuratie testen module Beveiligingsconfiguratie Hallo niet gevalideerd, zodat dit toobe afzonderlijk gedaan heeft.  

> [!NOTE]
> Voortdurend maken we verbeteringen toomake deze module krachtiger, dus als er een beschadigd is of ontbreekt in dat geval u denkt dat niet is momenteel door TestConfiguration opgepikt, laat ons weten via onze [ondersteunen kanalen](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).   
> 
> 

## <a name="next-steps"></a>Volgende stappen
* [Een zelfstandige cluster met Windows Server maken](service-fabric-cluster-creation-for-windows-server.md)
