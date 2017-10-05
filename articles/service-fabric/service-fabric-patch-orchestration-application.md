---
title: Azure Service Fabric-patch orchestration toepassing | Microsoft Docs
description: De toepassing te automatiseren besturingssysteem patchen op een Service Fabric-cluster.
services: service-fabric
documentationcenter: .net
author: novino
manager: timlt
editor: 
ms.assetid: de7dacf5-4038-434a-a265-5d0de80a9b1d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 5/9/2017
ms.author: nachandr
ms.openlocfilehash: 2c5842822e347113e388d570f6ae603a313944d6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="patch-the-windows-operating-system-in-your-service-fabric-cluster"></a>Patch voor het Windows-besturingssysteem in uw Service Fabric-cluster

De patch orchestration-toepassing is een Azure Service Fabric-toepassing die op een Service Fabric-cluster in Azure zonder uitvaltijd patchen besturingssysteem automatiseert.

De patch orchestration-app biedt het volgende:

- **Automatische update besturingssysteeminstallatie**. Besturingssysteem-updates automatisch gedownload en geïnstalleerd. Clusterknooppunten worden opgestart naar behoefte zonder uitvaltijd van de cluster.

- **Clusterbewust patchen en health integratie**. Tijdens het toepassen van updates controleert de patch orchestration app de status van de clusterknooppunten. Clusterknooppunten worden één knooppunt of één upgradedomein tegelijk. Als de status van het cluster als gevolg van de patch-proces uitvalt, is patchen om te voorkomen dat het probleem toegenomen gestopt.

## <a name="internal-details-of-the-app"></a>Interne details van de app.

De patch orchestration app bestaat uit de volgende onderdelen:

- **Service Coordinator**: deze stateful service is verantwoordelijk voor:
    - Coördinatie van de Windows Update-taak op het hele cluster.
    - Het opslaan van het resultaat van de voltooide Windows Update-bewerkingen.
- **Knooppunt-agentservice**: deze staatloze service wordt uitgevoerd op alle clusterknooppunten van de Service Fabric. De service is verantwoordelijk voor:
    - De Agent knooppunt NTService uitvoeren van de bootstrap.
    - Bewaken van de Agent knooppunt NTService.
- **Knooppunt Agent NTService**: deze Windows NT-service wordt uitgevoerd op een hoger niveau van bevoegdheden (systeem). Daarentegen de knooppunt Agent-Service en de coördinator-Service worden uitgevoerd op een lager niveau van bevoegdheden (NETWORK SERVICE). De service is verantwoordelijk voor het uitvoeren van de volgende taken in de Windows Update op alle clusterknooppunten:
    - Het uitschakelen van automatische Windows-updates op het knooppunt.
    - Downloaden en installeren van Windows Update volgens het beleid voor is de gebruiker opgegeven.
    - Opnieuw starten van de computer na installatie van Windows Update.
    - De resultaten van Windows-updates naar de coördinator-Service geüpload.
    - Reporting systeemstatusrapporten voor het geval is mislukt na het toewijzen van alle nieuwe pogingen.

> [!NOTE]
> De patch orchestration-app gebruikmaakt van de Service Fabric reparatie manager service uitschakelen of het inschakelen van het knooppunt en het uitvoeren van statuscontroles. De hersteltaak gemaakt door de patch orchestration app houdt de voortgang van de Windows Update voor elk knooppunt.

## <a name="prerequisites"></a>Vereisten

### <a name="minimum-supported-service-fabric-runtime-version"></a>Minimaal ondersteunde versie van Service Fabric-runtime

#### <a name="azure-clusters"></a>Azure-clusters
De patch orchestration-app moet worden uitgevoerd op Azure clusters met Service Fabric-runtime versie v5.5 of hoger.

#### <a name="standalone-on-premises-clusters"></a>Zelfstandige on-premises Clusters
De patch orchestration-app moet worden uitgevoerd op zelfstandige clusters met Service Fabric-runtime versie v5.6 of hoger.

### <a name="enable-the-repair-manager-service-if-its-not-running-already"></a>De reparatie manager-service inschakelen (indien deze niet al actief)

De patch orchestration-app is vereist voor de service manager herstellen moet zijn ingeschakeld op het cluster.

#### <a name="azure-clusters"></a>Azure-clusters

Azure clusters in de laag zilver duurzaamheid hebben de herstel-service manager standaard ingeschakeld. Azure-clusters in de laag goud duurzaamheid mogelijk of beschikt niet over de reparatie manager-service is ingeschakeld, afhankelijk van wanneer deze clusters zijn gemaakt. Azure-clusters in de laag Brons duurzaamheid standaard beschikt niet over de reparatie manager service is ingeschakeld. Als de service al is ingeschakeld, ziet u in het gedeelte van de services system op de Service Fabric Explorer draait.

##### <a name="azure-portal"></a>Azure Portal
U kunt herstel manager vanuit Azure-portal inschakelen op het moment van het instellen van het cluster. Selecteer `Include Repair Manager` onder de optie `Add on features` op het moment van de configuratie van het Cluster.
![Afbeelding van inschakelen van herstel-Manager vanuit Azure-portal](media/service-fabric-patch-orchestration-application/EnableRepairManager.png)

##### <a name="azure-resource-manager-template"></a>Azure Resource Manager-sjabloon
U kunt ook de [Azure Resource Manager-sjabloon](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) zodat de manager-service voor herstel op nieuwe en bestaande Service Fabric-cluster. Haal de sjabloon voor het cluster dat u wilt implementeren. U kunt de voorbeeldsjablonen gebruiken of een aangepaste Resource Manager-sjabloon maken. 

Om in te schakelen reparatie manager service gebruikmaakt [Azure Resource Manager-sjabloon](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm):

1. Controleer eerst of de `apiversion` is ingesteld op `2017-07-01-preview` voor de `Microsoft.ServiceFabric/clusters` resource, zoals wordt weergegeven in het volgende fragment. Als dit afwijkt, moet u bijwerken de `apiVersion` op de waarde `2017-07-01-preview`:

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. Nu de reparatie manager-service inschakelen door het volgende toe te voegen `addonFeatures` sectie na de `fabricSettings` sectie:

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. Nadat u de sjabloon voor het cluster hebt bijgewerkt met deze wijzigingen, worden ze toepassen en kunt u de upgrade voltooien. U ziet nu de reparatie manager systeemservice in uw cluster wordt uitgevoerd. Wordt aangeroepen `fabric:/System/RepairManagerService` in het gedeelte van de services system op de Service Fabric Explorer. 

### <a name="standalone-on-premises-clusters"></a>Zelfstandige lokale clusters

U kunt de [configuratie-instellingen voor Windows-cluster zelfstandige](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest) zodat de reparatie manager-service op de nieuwe en bestaande Service Fabric-cluster.

De reparatie manager-service inschakelen:

1. Controleer eerst of de `apiversion` in [algemene clusterconfiguraties](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest#general-cluster-configurations) is ingesteld op `04-2017` of hoger:

    ```json
    {
        "name": "SampleCluster",
        "clusterConfigurationVersion": "1.0.0",
        "apiVersion": "04-2017",
        ...
    }
    ```

2. Nu reparatie manager-service inschakelen door het volgende toe te voegen `addonFeaturres` sectie na de `fabricSettings` sectie zoals hieronder wordt weergegeven:

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. Uw clustermanifest bijwerken met deze wijzigingen, met behulp van de bijgewerkte clustermanifest [Maak een nieuw cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-for-windows-server) of [upgrade van de clusterconfiguratie](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-upgrade-windows-server#Upgrade-the-cluster-configuration). Zodra het cluster wordt uitgevoerd met bijgewerkte clustermanifest, zoals u ziet de reparatie manager systeemservice in het cluster die is aangeroepen met `fabric:/System/RepairManagerService`onder sectie in Service Fabric explorer van systeemservices.

### <a name="disable-automatic-windows-update-on-all-nodes"></a>Automatische Update van Windows op alle knooppunten uitschakelen

Automatische Windows-updates kunnen leiden tot verlies van beschikbaarheid omdat meerdere clusterknooppunten tegelijkertijd kunnen opnieuw worden opgestart. De patch orchestration-app probeert standaard, u de automatische Update van Windows op elk clusterknooppunt uitschakelen. Echter, als de instellingen worden beheerd door een beheerder of Groepsbeleid, raden wij aan het beleid van Windows Update naar 'Waarschuwen voordat downloaden' expliciet instellen.

### <a name="optional-enable-azure-diagnostics"></a>Optioneel: Azure diagnostische gegevens inschakelen

Clusters met Service Fabric-runtime-versie `5.6.220.9494` en registreert hierboven verzamelen patch orchestration app Logboeken als onderdeel van Service Fabric.
U kunt deze stap overslaan als het cluster wordt uitgevoerd op de Service Fabric-runtime-versie `5.6.220.9494` en hoger.

Voor clusters met Service Fabric-runtime-versie lager dan `5.6.220.9494`, logboeken voor de orchestration patch app lokaal worden verzameld op elk van de clusterknooppunten.
Het is raadzaam dat u Azure Diagnostics om te uploaden van Logboeken van alle knooppunten op een centrale locatie configureren.

Zie voor meer informatie over het inschakelen van Azure Diagnostics [logboeken verzamelen met behulp van Azure Diagnostics](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-how-to-setup-wad).

Logboeken voor de orchestration-app patch worden gegenereerd op de volgende vaste provider id's:

- e39b723c-590c-4090-abb0-11e3e6616346
- fc0028ff-bfdc-499f-80dc-ed922c52c5e9
- 24afa313-0d3b-4c7c-b485-1047fd964b60
- 05dc046c-60e9-4ef7-965e-91660adffa68

In het Resource Manager-sjabloon goto `EtwEventSourceProviderConfiguration` onder sectie `WadCfg` en voeg de volgende items:

```json
  {
    "provider": "e39b723c-590c-4090-abb0-11e3e6616346",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
      "eventDestination": "PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "fc0028ff-bfdc-499f-80dc-ed922c52c5e9",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "24afa313-0d3b-4c7c-b485-1047fd964b60",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "05dc046c-60e9-4ef7-965e-91660adffa68",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  }
```

> [!NOTE]
> Als uw Service Fabric-cluster typen met meerdere knooppunten heeft, wordt de vorige sectie moet worden toegevoegd voor alle de `WadCfg` secties.

## <a name="download-the-app-package"></a>Download het apppakket

Downloaden van de toepassing van de [downloadkoppeling](https://go.microsoft.com/fwlink/P/?linkid=849590).

## <a name="configure-the-app"></a>De app configureren

Het gedrag van de patch orchestration-app kan worden geconfigureerd om te voldoen aan uw behoeften. De standaardwaarden overschrijven door door te geven in de parameter van de toepassing tijdens het maken van de toepassing of update. Parameters voor de toepassing kunnen worden opgegeven door te geven `ApplicationParameter` naar de `Start-ServiceFabricApplicationUpgrade` of `New-ServiceFabricApplication` cmdlets.

|**Parameter**        |**Type**                          | **Details**|
|:-|-|-|
|MaxResultsToCache    |Lang                              | Maximum aantal resultaten van de Windows Update, die in de cache moet worden opgeslagen. <br>Standaardwaarde is 3000 ervan uitgaande dat de: <br> -Het aantal knooppunten is 20. <br> -Het aantal updates dat op een knooppunt per maand gebeurt is vijf. <br> -Het aantal resultaten per bewerking is 10. <br> -Resultaten voor de afgelopen drie maanden moeten worden opgeslagen. |
|TaskApprovalPolicy   |Enum <br> {NodeWise, UpgradeDomainWise}                          |TaskApprovalPolicy geeft aan het beleid dat moet worden gebruikt door de coördinator-Service voor het installeren van Windows-updates over de clusterknooppunten Service Fabric.<br>                         Toegestane waarden zijn: <br>                                                           <b>NodeWise</b>. Windows Update is geïnstalleerd, één knooppunt tegelijk. <br>                                                           <b>UpgradeDomainWise</b>. Windows Update is geïnstalleerd, één upgradedomein tegelijk. (Het maximum is bereikt, alle knooppunten van een upgradedomein gaan voor Windows Update.)
|LogsDiskQuotaInMB   |Lang  <br> (Standaard: 1024)               |Maximale grootte van de patch orchestration app registreert in MB, hetgeen kan lokaal op knooppunten worden gehandhaafd.
| WUQuery               | Tekenreeks<br>(Standaard: ' IsInstalled = 0 ")                | De query voor het ophalen van Windows-updates. Zie voor meer informatie [WuQuery.](https://msdn.microsoft.com/library/windows/desktop/aa386526(v=vs.85).aspx)
| InstallWindowsOSOnlyUpdates | BOOL <br> (standaard: True)                 | Deze vlag kan updates voor Windows-besturingssysteem moet worden geïnstalleerd.            |
| WUOperationTimeOutInMinutes | int <br>(Standaard: 90).                   | Hiermee geeft u de time-out voor een Windows Update-bewerking (zoeken of downloaden of installeren). Als de bewerking is niet voltooid binnen de opgegeven time-out, wordt het afgebroken.       |
| WURescheduleCount     | int <br> (Standaard: 5).                  | Het maximum aantal keren dat de service opnieuw gepland voor de Windows update als een bewerking blijft mislukken.          |
| WURescheduleTimeInMinutes | int <br>(Standaard: 30). | Het interval waarmee de service wordt automatisch opnieuw gepland Windows update als de fout zich blijft voordoen. |
| WUFrequency           | Door komma's gescheiden tekenreeks (standaard: "Wekelijks, woensdag, 7:00:00")     | De frequentie voor het installeren van Windows Update. De indeling en de mogelijke waarden zijn: <br>-Maandelijks, DD: mm: ss, bijvoorbeeld, maandelijks, 5, 12: 22:32. <br> -Per week, dag,: mm: ss, voor bijvoorbeeld wekelijks, dinsdag, 12:22:32.  <br> -Dagelijks: mm: ss, bijvoorbeeld dagelijks, 12:22:32.  <br> -Geen geeft aan dat de Windows Update mag niet worden uitgevoerd.  <br><br> Houd er rekening mee dat alle tijden in UTC zijn.|
| AcceptWindowsUpdateEula | BOOL <br>(Standaard: true) | Deze vlag instelt, wordt in de toepassing de eindgebruiker-licentie voor Windows Update accepteert namens de eigenaar van de machine.              |

> [!TIP]
> Als u Windows Update gebeurt onmiddellijk wilt, stelt `WUFrequency` ten opzichte van de tijd van de implementatie van toepassing. Stel bijvoorbeeld dat u hebt een testcluster met vijf knooppunten en plan de implementatie van de app op ongeveer 5:00 uur UTC. Als u wordt ervan uitgegaan dat de upgrade van de toepassing of implementatie 30 minuten maximaal duurt, ingesteld op de WUFrequency "Dagelijks, 17:30:00."

## <a name="deploy-the-app"></a>De app implementeren

1. Voltooi de vereiste stappen voor het voorbereiden van het cluster.
2. Implementeer de patch orchestration-app als elke andere Service Fabric-app. U kunt de app implementeren met behulp van PowerShell. Volg de stappen in [implementeren en verwijderen van toepassingen via PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).
3. De toepassing configureren op het moment van implementatie, de `ApplicationParamater` naar de `New-ServiceFabricApplication` cmdlet. We bieden het script Deploy.ps1 samen met de toepassing voor uw gemak. Het script gebruiken:

    - Verbinding maken met een Service Fabric-cluster met `Connect-ServiceFabricCluster`.
    - Voer het PowerShell-script Deploy.ps1 met de juiste `ApplicationParameter` waarde.

> [!NOTE]
> Houd het script en de map application PatchOrchestrationApplication in dezelfde map.

## <a name="upgrade-the-app"></a>De app bijwerken

Als u een bestaande app van de patch-orchestration upgraden met behulp van PowerShell, volg de stappen in [upgrade van de Service Fabric-toepassing met behulp van PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-upgrade-tutorial-powershell).

## <a name="remove-the-app"></a>De app verwijderen

Volg de stappen in de toepassing te verwijderen, [implementeren en verwijderen van toepassingen via PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).

We bieden het script Undeploy.ps1 samen met de toepassing voor uw gemak. Het script gebruiken:

  - Verbinding maken met een Service Fabric-cluster met ```Connect-ServiceFabricCluster```.

  - Voer het PowerShell-script Undeploy.ps1.

> [!NOTE]
> Houd het script en de map application PatchOrchestrationApplication in dezelfde map.

## <a name="view-the-windows-update-results"></a>Bekijk de resultaten van Windows Update

De patch orchestration app beschrijft de REST-API's om de historische resultaten voor de gebruiker weer te geven. Een voorbeeld van het resultaat JSON:
```json
[
  {
    "NodeName": "_stg1vm_1",
    "WindowsUpdateOperationResults": [
      {
        "OperationResult": 0,
        "NodeName": "_stg1vm_1",
        "OperationTime": "2017-05-21T11:46:52.1953713Z",
        "UpdateDetails": [
          {
            "UpdateId": "7392acaf-6a85-427c-8a8d-058c25beb0d6",
            "Title": "Cumulative Security Update for Internet Explorer 11 for Windows Server 2012 R2 (KB3185319)",
            "Description": "A security issue has been identified in a Microsoft software product that could affect your system. You can help protect your system by installing this update from Microsoft. For a complete listing of the issues that are included in this update, see the associated Microsoft Knowledge Base article. After you install this update, you may have to restart your system.",
            "ResultCode": 0
          }
        ],
        "OperationType": 1,
        "WindowsUpdateQuery": "IsInstalled=0",
        "WindowsUpdateFrequency": "Daily,10:00:00",
        "RebootRequired": false
      }
    ]
  },
  ...
]
```
Als er geen update nog is gepland, is het resultaat JSON is leeg.

Meld u aan bij het cluster om de query Windows Update resultaten. Vervolgens weten het adres van de replica voor de primaire van de Service Coordinator en klik op de URL van de browser: http://&lt;REPLICA-IP-&gt;:&lt;ApplicationPort&gt;/PatchOrchestrationApplication/v1/GetWindowsUpdateResults.

De REST-eindpunt voor de coördinator-Service heeft een dynamische poort. Als u wilt de exacte URL controleren, raadpleegt u de Service Fabric Explorer. Bijvoorbeeld, de resultaten zijn beschikbaar op `http://10.0.0.7:20000/PatchOrchestrationApplication/v1/GetWindowsUpdateResults`.

![Afbeelding van REST-eindpunt](media/service-fabric-patch-orchestration-application/Rest_Endpoint.png)


Als de omgekeerde proxy is ingeschakeld op het cluster, kunt u de URL van buiten het cluster ook openen.
Het eindpunt dat moet worden bereikt is http://&lt;SERVERURL&gt;:&lt;REVERSEPROXYPORT&gt;/PatchOrchestrationApplication/CoordinatorService/v1/GetWindowsUpdateResults.

Volg de stappen in zodat de omgekeerde proxy op het cluster [omgekeerde proxy in Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy). 

> 
> [!WARNING]
> Nadat de omgekeerde proxy is geconfigureerd, zijn alle micro services in het cluster die een HTTP-eindpunt adresseerbare van buiten het cluster.

## <a name="diagnosticshealth-events"></a>Diagnostische gegevens/health-gebeurtenissen

### <a name="collect-patch-orchestration-app-logs"></a>Collect patch orchestration applogboeken

Patch orchestration app logboeken worden verzameld als onderdeel van Service Fabric-logboeken van de runtimeversie `5.6.220.9494` en hoger.
Voor clusters met Service Fabric-runtime-versie lager dan `5.6.220.9494`, logboeken kunnen worden verzameld met behulp van een van de volgende methoden.

#### <a name="locally-on-each-node"></a>Lokaal op elk knooppunt

Logboeken worden verzameld lokaal op elk clusterknooppunt Service Fabric als Service Fabric-runtime-versie is minder dan `5.6.220.9494`. De locatie voor toegang tot de logboeken is \[Service Fabric\_installatie\_station\]:\\PatchOrchestrationApplication\\Logboeken.

Als Service Fabric is geïnstalleerd op station D, het pad is bijvoorbeeld D:\\PatchOrchestrationApplication\\Logboeken.

#### <a name="central-location"></a>Centrale locatie

Als Azure Diagnostics is geconfigureerd als onderdeel van de vereiste stappen, zijn logboeken voor de orchestration-app patch beschikbaar in Azure Storage.

### <a name="health-reports"></a>Statusrapporten

De patch orchestration-app publiceert ook statusrapporten op basis van de coördinator-Service of de Agent-Service van het knooppunt in de volgende gevallen:

#### <a name="a-windows-update-operation-failed"></a>Een Windows Update-bewerking is mislukt

Als een Windows Update-bewerking is mislukt op een knooppunt, wordt een statusrapport gegenereerd op basis van de Agent-Service van het knooppunt. Details van het statusrapport bevatten problematisch knooppuntnaam.

Nadat patching is voltooid op het knooppunt problematisch, wordt het rapport automatisch gewist.

#### <a name="the-node-agent-ntservice-is-down"></a>De Agent knooppunt NTService is niet beschikbaar

Als de Agent knooppunt NTService niet actief op een knooppunt is, wordt een waarschuwing het niveau statusrapport gegenereerd op basis van de Agent-Service van het knooppunt.

#### <a name="the-repair-manager-service-is-not-enabled"></a>De reparatie manager-service is niet ingeschakeld

Als de reparatie manager-service niet in het cluster gevonden is, wordt een waarschuwing het niveau statusrapport gegenereerd voor de coördinator-Service.

## <a name="frequently-asked-questions"></a>Veelgestelde vragen

Q. **Waarom zie ik mijn cluster in een foutstatus wanneer de patch orchestration-app wordt uitgevoerd?**

A. Tijdens het installatieproces de patch orchestration-app wordt uitgeschakeld of opnieuw wordt opgestart knooppunten, die tijdelijk leiden tot de status van het cluster tijdelijk niet kunnen beschikbaar.

Op basis van het beleid voor de toepassing, ofwel een knooppunt kan uitvallen tijdens een bewerking van de toepassing van patches *of* een hele upgradedomein tegelijkertijd kan uitvallen.

Aan het einde van de Windows Update-installatie, de knooppunten zijn ingeschakeld boeken opnieuw opstarten.

In het volgende voorbeeld wordt het cluster is verzonden naar een foutstatus tijdelijk omdat twee knooppunten zijn en het beleid MaxPercentageUnhealthNodes is geschonden. De fout is tijdelijk totdat de toepassing van patches bewerking uitgevoerd wordt.

![Afbeelding van slecht cluster](media/service-fabric-patch-orchestration-application/MaxPercentage_causing_unhealthy_cluster.png)

Als het probleem zich blijft voordoen, raadpleegt u de sectie probleemoplossing.

Q. **Patch orchestration app heeft de waarschuwingsstatus**

A. Controleer of een statusrapport geplaatst voor de toepassing de hoofdoorzaak is. De waarschuwing bevat meestal, details van het probleem. Als het probleem tijdelijke is, wordt de toepassing automatisch herstellen van deze status verwacht.

Q. **Wat moet ik doen als mijn cluster beschadigd is en moet ik doen urgente besturingssysteem bijwerken?**

A. De patch orchestration app terwijl het cluster niet in orde is niet geïnstalleerd met updates. Probeer uw cluster naar een goede status om de blokkering van de patch orchestration app werkstroom te brengen.

Q. **Waarom patchen tussen verschillende clusters duurt te lang om uit te voeren?**

A. De tijd die nodig is door de patch orchestration-app is voornamelijk afhankelijk van de volgende factoren:

- Het beleid van de coördinator-Service. 
  - Het standaardbeleid `NodeWise`, resulteert in het patchen slechts één knooppunt tegelijk. Met name in het geval van grotere clusters, wordt aangeraden dat u de `UpgradeDomainWise` beleid sneller patchen tussen verschillende clusters.
- Het aantal beschikbare updates voor het downloaden en installeren. 
- De gemiddelde tijd die nodig zijn voor een update downloaden en installeren die mag niet meer dan een paar uur.
- De prestaties van de virtuele machine en de netwerkbandbreedte.

Q. **Waarom zie ik bepaalde updates in de Windows Update-resultaten die zijn verkregen via de REST-api, maar niet onder de geschiedenis van Windows Update op de machine?**

A. Sommige productupdates moeten worden gecontroleerd in de geschiedenis van hun respectieve update/patch. Bijvoorbeeld: Windows Defender-updates worden niet weergegeven in de geschiedenis van Windows Update op Windows Server 2016.

## <a name="disclaimers"></a>Disclaimers

- De patch orchestration app accepteert de eindgebruiker-licentie van Windows Update namens de gebruiker. Eventueel kunt u de instelling ingeschakeld uitschakelen in de configuratie van de toepassing.

- De patch orchestration app verzamelt telemetrie om informatie over het gebruik en prestaties te houden. De toepassing telemetrie volgt de instelling van de Service Fabric-runtime telemetrie (die standaard is ingeschakeld).

## <a name="troubleshooting"></a>Problemen oplossen

### <a name="a-node-is-not-coming-back-to-up-state"></a>Een knooppunt afkomstig niet is back-up maken van status

**Het knooppunt kan blijven steken in een status uitschakelen omdat**:

Er is een veiligheidscontrole in behandeling. U lost deze situatie, zorg ervoor dat er voldoende knooppunten beschikbaar in een foutloze toestand bevindt zijn.

**Het knooppunt kan blijven steken uitgeschakeld omdat**:

- Het knooppunt is handmatig uitgeschakeld.
- Het knooppunt is uitgeschakeld vanwege een lopende Azure-infrastructuur.
- Het knooppunt is tijdelijk uitgeschakeld door de app patch orchestration patch van het knooppunt.

**Het knooppunt kan blijven steken in een status Omlaag omdat**:

- Het knooppunt is geplaatst in een status Omlaag handmatig.
- Het knooppunt is momenteel door een herstart (die kan worden geactiveerd door de patch orchestration app).
- Het knooppunt is niet beschikbaar vanwege een defecte VM of verbindingsproblemen machine of het netwerk.

### <a name="updates-were-skipped-on-some-nodes"></a>Updates zijn op sommige knooppunten overgeslagen

De patch orchestration app probeert te installeren van een Windows-update volgens het nieuwe beleid. De service probeert te herstellen van het knooppunt en overslaan van de update volgens het toepassingenbeleid.

In dat geval wordt een waarschuwing het niveau statusrapport gegenereerd op basis van de Agent-Service van het knooppunt. Het resultaat voor Windows Update bevat ook de mogelijke reden voor de fout.

### <a name="the-health-of-the-cluster-goes-to-error-while-the-update-installs"></a>De status van het cluster overschakelt naar de fout tijdens de update is geïnstalleerd

Een defecte Windows update kunt u de status van een toepassing of het cluster op een bepaald knooppunt of upgradedomein zetten. De patch orchestration app stoppen eventuele latere Windows Update-bewerking totdat het cluster weer in orde is.

Er moet een beheerder ingrijpen en bepalen waarom de toepassing of het cluster beschadigd vanwege Windows Update is.

## <a name="release-notes-"></a>Release-opmerkingen:

### <a name="version-110"></a>Versie 1.1.0
- Openbare versie

### <a name="version-111"></a>Versie 1.1.1
- Een bug vast entrypoint van NodeAgentService waardoor de installatie van NodeAgentNTService.

### <a name="version-120-latest"></a>Versie 1.2.0 (laatste)

- Werkstroom van oplossingen voor problemen rond systeem opnieuw starten.
- Fout te herstellen bij het maken van de RM-taken als gevolg van welke status selectievakje tijdens herstel taken voorbereiden is niet plaatsvinden, zoals verwacht.
- De opstartmodus gewijzigd voor windows service POANodeSvc van automatische vertraagd automatisch.
