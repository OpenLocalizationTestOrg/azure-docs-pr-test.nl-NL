---
title: Service Fabric-toepassing voor patch orchestration aaaAzure | Microsoft Docs
description: Toepassing tooautomate operationele systeem herstellen op een Service Fabric-cluster.
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
ms.openlocfilehash: fbb89aa2ea418181ee908a01850178c113c462fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="patch-hello-windows-operating-system-in-your-service-fabric-cluster"></a>Patch Hallo Windows-besturingssysteem in uw Service Fabric-cluster

Hallo patch orchestration toepassing is een Azure Service Fabric-toepassing die op een Service Fabric-cluster in Azure zonder uitvaltijd patchen besturingssysteem automatiseert.

Hallo patch orchestration app biedt Hallo volgende:

- **Automatische update besturingssysteeminstallatie**. Besturingssysteem-updates automatisch gedownload en geïnstalleerd. Clusterknooppunten worden opgestart naar behoefte zonder uitvaltijd van de cluster.

- **Clusterbewust patchen en health integratie**. Tijdens het toepassen van updates controleert Hallo patch orchestration app Hallo status van de clusterknooppunten Hallo. Clusterknooppunten worden één knooppunt of één upgradedomein tegelijk. Als Hallo status van de cluster hello uitgeschakeld vanwege toohello patch-proces wordt, is patchen gestopt tooprevent toegenomen Hallo probleem.

## <a name="internal-details-of-hello-app"></a>Interne details van Hallo-app

Hallo patch orchestration app bestaat uit Hallo subonderdelen te volgen:

- **Service Coordinator**: deze stateful service is verantwoordelijk voor:
    - Windows Update-taak van de coördinerende Hallo op Hallo gehele cluster.
    - Het opslaan van Hallo resultaat van de voltooide Windows Update-bewerkingen.
- **Knooppunt-agentservice**: deze staatloze service wordt uitgevoerd op alle clusterknooppunten van de Service Fabric. Hallo-service is verantwoordelijk voor:
    - Uitvoeren van de bootstrap Hallo knooppunt Agent NTService.
    - Hallo knooppunt Agent NTService bewaken.
- **Knooppunt Agent NTService**: deze Windows NT-service wordt uitgevoerd op een hoger niveau van bevoegdheden (systeem). Daarentegen Hallo knooppunt Agent-Service en Hallo Coordinator-Service worden uitgevoerd op een lager niveau van bevoegdheden (NETWORK SERVICE). Hallo-service is verantwoordelijk voor het uitvoeren van Windows Update-taken te volgen op alle clusterknooppunten van Hallo Hallo:
    - Het uitschakelen van automatische updates van Windows op Hallo-knooppunt.
    - Downloaden en installeren van Windows Update is volgens toohello beleid Hallo gebruiker opgegeven.
    - Opnieuw starten van Hallo machine na installatie van Windows Update.
    - Hallo-resultaten van Windows updates toohello Coordinator-Service worden geüpload.
    - Reporting systeemstatusrapporten voor het geval is mislukt na het toewijzen van alle nieuwe pogingen.

> [!NOTE]
> Hallo patch orchestration app gebruikt Hallo Service Fabric manager system service toodisable herstellen of Hallo knooppunt inschakelen en statuscontroles uitvoeren. Hallo hersteltaak gemaakt door Hallo patch orchestration app houdt Hallo Windows Update uitgevoerd voor elk knooppunt.

## <a name="prerequisites"></a>Vereisten

### <a name="minimum-supported-service-fabric-runtime-version"></a>Minimaal ondersteunde versie van Service Fabric-runtime

#### <a name="azure-clusters"></a>Azure-clusters
Hallo patch orchestration app moet worden uitgevoerd op Azure clusters met Service Fabric-runtime versie v5.5 of hoger.

#### <a name="standalone-on-premises-clusters"></a>Zelfstandige on-premises Clusters
Hallo patch orchestration app moet worden uitgevoerd op zelfstandige clusters met Service Fabric-runtime versie v5.6 of hoger.

### <a name="enable-hello-repair-manager-service-if-its-not-running-already"></a>Hallo reparatie manager-service inschakelen (indien deze niet al actief)

Hallo patch orchestration app vereist Hallo reparatie manager system service toobe is ingeschakeld op het Hallo-cluster.

#### <a name="azure-clusters"></a>Azure-clusters

Azure clusters in Hallo zilver duurzaamheid laag hebben Hallo herstellen manager-service is standaard ingeschakeld. Azure-clusters in Hallo gold duurzaamheid laag mogelijk of mogelijk geen Hallo manager-service voor herstel is ingeschakeld, afhankelijk van wanneer deze clusters zijn gemaakt. Azure-clusters in de laag Brons duurzaamheid hello, standaard geen Hallo herstellen manager-service is ingeschakeld. Als het Hallo-service al is ingeschakeld, ziet u draait in Hallo system services gedeelte op Hallo Service Fabric Explorer.

##### <a name="azure-portal"></a>Azure Portal
U kunt herstel manager vanuit Azure-portal op Hallo tijd voor het instellen van van cluster inschakelen. Selecteer `Include Repair Manager` onder de optie `Add on features` op Hallo tijdstip van de configuratie van het Cluster.
![Afbeelding van inschakelen van herstel-Manager vanuit Azure-portal](media/service-fabric-patch-orchestration-application/EnableRepairManager.png)

##### <a name="azure-resource-manager-template"></a>Azure Resource Manager-sjabloon
U kunt ook hello gebruiken [Azure Resource Manager-sjabloon](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) tooenable Hallo reparatie manager-service op de nieuwe en bestaande Service Fabric-clusters. Hallo sjabloon ophalen voor Hallo-cluster dat u wilt dat toodeploy. U kunt voorbeeldsjablonen hello gebruiken of een aangepaste Resource Manager-sjabloon maken. 

tooenable hello reparatie manager service met behulp van [Azure Resource Manager-sjabloon](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm):

1. Controleer eerst of Hallo `apiversion` te is ingesteld,`2017-07-01-preview` voor Hallo `Microsoft.ServiceFabric/clusters` resource, zoals wordt weergegeven in het volgende codefragment Hallo. Als dit afwijkt, moet u tooupdate hello `apiVersion` toohello waarde `2017-07-01-preview`:

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. Nu Hallo reparatie manager-service inschakelen door toe te voegen Hallo volgende `addonFeatures` sectie na Hallo `fabricSettings` sectie:

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. Nadat u de sjabloon voor het cluster hebt bijgewerkt met deze wijzigingen, ze toepassen en laten Hallo upgrade voltooien. U ziet nu Hallo reparatie manager system-service in uw cluster wordt uitgevoerd. Wordt aangeroepen `fabric:/System/RepairManagerService` in Hallo system services gedeelte op Hallo Service Fabric Explorer. 

### <a name="standalone-on-premises-clusters"></a>Zelfstandige lokale clusters

U kunt Hallo [configuratie-instellingen voor Windows-cluster zelfstandige](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest) tooenable Hallo reparatie manager-service op de nieuwe en bestaande Service Fabric-cluster.

tooenable hello reparatie manager-service:

1. Controleer eerst of Hallo `apiversion` in [algemene clusterconfiguraties](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest#general-cluster-configurations) te is ingesteld,`04-2017` of hoger:

    ```json
    {
        "name": "SampleCluster",
        "clusterConfigurationVersion": "1.0.0",
        "apiVersion": "04-2017",
        ...
    }
    ```

2. Nu reparatie manager-service inschakelen door toe te voegen Hallo volgende `addonFeaturres` sectie na Hallo `fabricSettings` sectie zoals hieronder wordt weergegeven:

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. Uw clustermanifest bijwerken met deze wijzigingen, met behulp van het clustermanifest Hallo bijgewerkt [Maak een nieuw cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-for-windows-server) of [upgrade Hallo clusterconfiguratie](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-upgrade-windows-server#Upgrade-the-cluster-configuration). Zodra het Hallo-cluster wordt uitgevoerd met bijgewerkte clustermanifest, nu ziet u Hallo reparatie manager systeemservice in uw cluster, heet `fabric:/System/RepairManagerService`onder sectie in Hallo Service Fabric explorer van systeemservices.

### <a name="disable-automatic-windows-update-on-all-nodes"></a>Automatische Update van Windows op alle knooppunten uitschakelen

Automatische updates voor Windows tooavailability gegevensverlies kunnen leiden omdat meerdere clusterknooppunten op Hallo dezelfde opstarten kunnen tijd. Hallo patch orchestration app standaard pogingen toodisable Hallo automatische Windows-updates op elk clusterknooppunt. Als het Hallo-instellingen worden beheerd door een beheerder of Groepsbeleid, raden wij echter instelling Hallo Windows Update-beleid te 'waarschuwen voordat downloaden' expliciet.

### <a name="optional-enable-azure-diagnostics"></a>Optioneel: Azure diagnostische gegevens inschakelen

Clusters met Service Fabric-runtime-versie `5.6.220.9494` en registreert hierboven verzamelen patch orchestration app Logboeken als onderdeel van Service Fabric.
U kunt deze stap overslaan als het cluster wordt uitgevoerd op de Service Fabric-runtime-versie `5.6.220.9494` en hoger.

Voor clusters met Service Fabric-runtime-versie lager dan `5.6.220.9494`, logboeken voor Hallo patch orchestration app lokaal op elk van de clusterknooppunten Hallo zijn verzameld.
Het is raadzaam dat u Azure Diagnostics tooupload logboeken van alle knooppunten tooa centrale locatie configureren.

Zie voor meer informatie over het inschakelen van Azure Diagnostics [logboeken verzamelen met behulp van Azure Diagnostics](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-how-to-setup-wad).

Logboeken voor Hallo patch orchestration app worden gegenereerd op Hallo vaste provider id's te volgen:

- e39b723c-590c-4090-abb0-11e3e6616346
- fc0028ff-bfdc-499f-80dc-ed922c52c5e9
- 24afa313-0d3b-4c7c-b485-1047fd964b60
- 05dc046c-60e9-4ef7-965e-91660adffa68

In het Resource Manager-sjabloon goto `EtwEventSourceProviderConfiguration` onder sectie `WadCfg` en Hallo volgende vermeldingen toe te voegen:

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
> Als uw Service Fabric-cluster typen met meerdere knooppunten heeft, wordt de vorige sectie Hallo moet worden toegevoegd voor alle Hallo `WadCfg` secties.

## <a name="download-hello-app-package"></a>Hallo-app downloaden

Hallo-toepassing downloaden van Hallo [downloadkoppeling](https://go.microsoft.com/fwlink/P/?linkid=849590).

## <a name="configure-hello-app"></a>Hallo-app configureren

gedrag van Hallo patch orchestration app Hallo geconfigureerde toomeet uw behoeften kunt worden. Hallo-standaardwaarden overschrijven door door te geven in de parameter toepassing hello tijdens het maken van de toepassing of update. Parameters voor de toepassing kunnen worden opgegeven door te geven `ApplicationParameter` toohello `Start-ServiceFabricApplicationUpgrade` of `New-ServiceFabricApplication` cmdlets.

|**Parameter**        |**Type**                          | **Details**|
|:-|-|-|
|MaxResultsToCache    |Lang                              | Maximum aantal resultaten van de Windows Update, die in de cache moet worden opgeslagen. <br>Standaardwaarde is 3000 ervan uitgaande dat de: <br> -Het aantal knooppunten is 20. <br> -Het aantal updates dat op een knooppunt per maand gebeurt is vijf. <br> -Het aantal resultaten per bewerking is 10. <br> -Resultaten voor de afgelopen drie maanden Hallo moeten worden opgeslagen. |
|TaskApprovalPolicy   |Enum <br> {NodeWise, UpgradeDomainWise}                          |TaskApprovalPolicy geeft Hallo-beleid dat wordt gebruikt door Hallo Service Coordinator tooinstall Windows-updates via Service Fabric-clusterknooppunten Hallo toobe.<br>                         Toegestane waarden zijn: <br>                                                           <b>NodeWise</b>. Windows Update is geïnstalleerd, één knooppunt tegelijk. <br>                                                           <b>UpgradeDomainWise</b>. Windows Update is geïnstalleerd, één upgradedomein tegelijk. (Op Hallo maximale, alle Hallo knooppunten die behoren tooan upgradedomein gaan voor Windows Update.)
|LogsDiskQuotaInMB   |Lang  <br> (Standaard: 1024)               |Maximale grootte van de patch orchestration app registreert in MB, hetgeen kan lokaal op knooppunten worden gehandhaafd.
| WUQuery               | Tekenreeks<br>(Standaard: ' IsInstalled = 0 ")                | Query tooget Windows-updates. Zie voor meer informatie [WuQuery.](https://msdn.microsoft.com/library/windows/desktop/aa386526(v=vs.85).aspx)
| InstallWindowsOSOnlyUpdates | BOOL <br> (standaard: True)                 | Deze vlag kan Windows-besturingssysteem system updates toobe geïnstalleerd.            |
| WUOperationTimeOutInMinutes | int <br>(Standaard: 90).                   | Hiermee geeft u Hallo de time-out voor alle Windows Update-bewerking (zoeken of downloaden of installeren). Als het Hallo-bewerking is niet voltooid in Hallo opgegeven time-out, deze wordt afgebroken.       |
| WURescheduleCount     | int <br> (Standaard: 5).                  | Hallo kunt u het maximum aantal keren Hallo-service wordt automatisch opnieuw gepland Hallo Windows update als een bewerking blijft mislukken.          |
| WURescheduleTimeInMinutes | int <br>(Standaard: 30). | Hallo-interval op welke Hallo service wordt automatisch opnieuw gepland Hallo Windows update als de fout zich blijft voordoen. |
| WUFrequency           | Door komma's gescheiden tekenreeks (standaard: "Wekelijks, woensdag, 7:00:00")     | Hallo-frequentie voor het installeren van Windows Update. Hallo-indeling en de mogelijke waarden zijn: <br>-Maandelijks, DD: mm: ss, bijvoorbeeld, maandelijks, 5, 12: 22:32. <br> -Per week, dag,: mm: ss, voor bijvoorbeeld wekelijks, dinsdag, 12:22:32.  <br> -Dagelijks: mm: ss, bijvoorbeeld dagelijks, 12:22:32.  <br> -Geen geeft aan dat de Windows Update mag niet worden uitgevoerd.  <br><br> Houd er rekening mee dat alle Hallo tijden in UTC zijn.|
| AcceptWindowsUpdateEula | BOOL <br>(Standaard: true) | Deze vlag instelt, accepteert Hallo toepassing hello eindgebruiker licentie overeenkomst voor Windows Update namens Hallo-eigenaar van het Hallo-machine.              |

> [!TIP]
> Als u Windows Update toohappen onmiddellijk wilt, stelt `WUFrequency` implementatietijd relatieve toohello-toepassing. Stel bijvoorbeeld dat u hebt een vijf knooppunten test-cluster en plan toodeploy Hallo-app op ongeveer 5:00 uur UTC. Als u wordt ervan uitgegaan dat de upgrade van de toepassing hello of implementatie duurt voordat 30 minuten op Hallo maximale, stel Hallo WUFrequency als "Dagelijks, 17:30:00."

## <a name="deploy-hello-app"></a>Hallo-app implementeren

1. Voltooi alle Hallo vereiste stappen tooprepare Hallo-cluster.
2. Hallo patch orchestration app als elke andere Service Fabric-app implementeren. U kunt het Hallo-app implementeren met behulp van PowerShell. Volg de stappen Hallo in [implementeren en verwijderen van toepassingen via PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).
3. tooconfigure hello toepassing tijdens het Hallo van implementatie en pass Hallo `ApplicationParamater` toohello `New-ServiceFabricApplication` cmdlet. We bieden Hallo script Deploy.ps1 samen met de Hallo-toepassing voor uw gemak. toouse hello script:

    - Verbinding maken met tooa Service Fabric-cluster met behulp van `Connect-ServiceFabricCluster`.
    - Hallo PowerShell-script Deploy.ps1 Hello juiste uitvoeren `ApplicationParameter` waarde.

> [!NOTE]
> Houd Hallo script en de map van de toepassing hello PatchOrchestrationApplication Hallo dezelfde directory.

## <a name="upgrade-hello-app"></a>Hallo-app bijwerken

een bestaande patch orchestration-app met behulp van PowerShell, tooupgrade Hallo stappen in [upgrade van de Service Fabric-toepassing met behulp van PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-upgrade-tutorial-powershell).

## <a name="remove-hello-app"></a>Hallo-app verwijderen

Volg de stappen Hallo in-toepassing hello tooremove [implementeren en verwijderen van toepassingen via PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).

We bieden Hallo script Undeploy.ps1 samen met de Hallo-toepassing voor uw gemak. toouse hello script:

  - Verbinding maken met tooa Service Fabric-cluster met behulp van ```Connect-ServiceFabricCluster```.

  - Hallo PowerShell-script Undeploy.ps1 uitvoeren.

> [!NOTE]
> Houd Hallo script en de map van de toepassing hello PatchOrchestrationApplication Hallo dezelfde directory.

## <a name="view-hello-windows-update-results"></a>Hallo Windows Update-resultaten weergeven

Hallo patch orchestration app beschrijft de REST-API's toodisplay Hallo historische resultaten toohello gebruiker. Een voorbeeld van resultaat Hallo JSON:
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
            "Description": "A security issue has been identified in a Microsoft software product that could affect your system. You can help protect your system by installing this update from Microsoft. For a complete listing of hello issues that are included in this update, see hello associated Microsoft Knowledge Base article. After you install this update, you may have toorestart your system.",
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
Als er geen update nog is gepland, is Hallo resultaat JSON leeg.

Meld u bij toohello cluster tooquery Windows Update resultaten. Vervolgens weten Hallo replica adres voor de primaire Hallo Hallo Coordinator-Service en Hallo URL vanuit de browser Hallo bereikt: http://&lt;REPLICA-IP-&gt;:&lt;ApplicationPort&gt;/PatchOrchestrationApplication/v1 / GetWindowsUpdateResults.

Hallo REST-eindpunt voor Hallo Coordinator-Service heeft een dynamische poort. toocheck exacte URL hello, raadpleeg dan toohello Service Fabric Explorer. Bijvoorbeeld, Hallo resultaten zijn beschikbaar op `http://10.0.0.7:20000/PatchOrchestrationApplication/v1/GetWindowsUpdateResults`.

![Afbeelding van REST-eindpunt](media/service-fabric-patch-orchestration-application/Rest_Endpoint.png)


Als omgekeerde proxy Hallo op Hallo-cluster is ingeschakeld, kunt u Hallo URL uit buiten Hallo cluster ook openen.
Hallo-eindpunt dat toobe moet treffer is http://&lt;SERVERURL&gt;:&lt;REVERSEPROXYPORT&gt;/PatchOrchestrationApplication/CoordinatorService/v1/GetWindowsUpdateResults.

tooenable hello omgekeerde proxy op Hallo cluster Hallo stappen in [omgekeerde proxy in Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy). 

> 
> [!WARNING]
> Nadat Hallo omgekeerde proxy is geconfigureerd, kunnen alle micro services in Hallo cluster die een HTTP-eindpunt worden opgevraagd uit buiten Hallo-cluster.

## <a name="diagnosticshealth-events"></a>Diagnostische gegevens/health-gebeurtenissen

### <a name="collect-patch-orchestration-app-logs"></a>Collect patch orchestration applogboeken

Patch orchestration app logboeken worden verzameld als onderdeel van Service Fabric-logboeken van de runtimeversie `5.6.220.9494` en hoger.
Voor clusters met Service Fabric-runtime-versie lager dan `5.6.220.9494`, logboeken kunnen worden verzameld met behulp van een van de volgende methoden Hallo.

#### <a name="locally-on-each-node"></a>Lokaal op elk knooppunt

Logboeken worden verzameld lokaal op elk clusterknooppunt Service Fabric als Service Fabric-runtime-versie is minder dan `5.6.220.9494`. Hallo locatie tooaccess Hallo Logboeken is \[Service Fabric\_installatie\_station\]:\\PatchOrchestrationApplication\\Logboeken.

Als Service Fabric is geïnstalleerd op station D, Hallo pad is bijvoorbeeld D:\\PatchOrchestrationApplication\\Logboeken.

#### <a name="central-location"></a>Centrale locatie

Als Azure Diagnostics is geconfigureerd als onderdeel van de vereiste stappen, zijn logboeken voor Hallo patch orchestration app beschikbaar in Azure Storage.

### <a name="health-reports"></a>Statusrapporten

Hallo patch orchestration app publiceert ook statusrapporten tegen Hallo Service Coordinator of Hallo knooppunt Agent-Service in de volgende gevallen Hallo:

#### <a name="a-windows-update-operation-failed"></a>Een Windows Update-bewerking is mislukt

Als een Windows Update-bewerking is mislukt op een knooppunt, wordt een statusrapport gegenereerd op basis van Hallo knooppunt Agent-Service. Details van het statusrapport Hallo bevatten Hallo problematisch knooppuntnaam.

Nadat patching is voltooid op Hallo problematisch knooppunt, wordt Hallo rapport automatisch gewist.

#### <a name="hello-node-agent-ntservice-is-down"></a>Hallo knooppunt Agent NTService is niet beschikbaar

Als Hallo knooppunt Agent NTService niet actief op een knooppunt is, wordt een waarschuwing het niveau statusrapport gegenereerd tegen Hallo knooppunt Agent-Service.

#### <a name="hello-repair-manager-service-is-not-enabled"></a>Hallo reparatie manager-service is niet ingeschakeld

Als Hallo reparatie manager-service niet op cluster hello gevonden is, wordt een waarschuwing het niveau statusrapport gegenereerd voor Hallo Coordinator-Service.

## <a name="frequently-asked-questions"></a>Veelgestelde vragen

Q. **Waarom zie ik mijn cluster in een foutstatus wanneer Hallo patch orchestration app wordt uitgevoerd?**

A. Tijdens het installatieproces Hallo Hallo patch orchestration app wordt uitgeschakeld of opnieuw wordt opgestart knooppunten, die tijdelijk leiden tot Hallo status van Hallo cluster tijdelijk niet kunnen beschikbaar.

Op basis van beleid voor de toepassing hello hello, ofwel een knooppunt kan uitvallen tijdens een bewerking van de toepassing van patches *of* een hele upgradedomein tegelijkertijd kan uitvallen.

Hallo knooppunten zijn ingeschakeld boeken door Hallo van Hallo Windows Update-installatie, opnieuw opstarten.

In de Hallo voorbeeld te volgen, Hallo-cluster is gegaan tooan foutstatus tijdelijk omdat twee knooppunten niet actief zijn en Hallo MaxPercentageUnhealthNodes beleid is geschonden. Hallo-fout is tijdelijk totdat Hallo patchen bewerking uitgevoerd wordt.

![Afbeelding van slecht cluster](media/service-fabric-patch-orchestration-application/MaxPercentage_causing_unhealthy_cluster.png)

Als Hallo probleem zich blijft voordoen, raadpleegt u de sectie Probleemoplossing toohello.

Q. **Patch orchestration app heeft de waarschuwingsstatus**

A. Controleer de toosee als een statusrapport geboekt tegen Hallo toepassing hello hoofdoorzaak. Hallo-waarschuwing bevat meestal, details van probleem Hallo. Als Hallo probleem tijdelijke is, is toepassing hello verwachte tooauto-herstellen van deze status.

Q. **Wat moet ik doen als mijn cluster beschadigd is en ik toodo urgente besturingssysteem bijwerken moet?**

A. Hallo patch orchestration app installeert updates niet tijdens het Hallo-cluster is beschadigd. Probeer toobring uw cluster tooa status in orde toounblock Hallo patch orchestration app werkstroom.

Q. **Waarom patchen tussen verschillende clusters duurt te lang waardoor toorun?**

A. Hallo-tijd die nodig is door Hallo patch orchestration app is voornamelijk afhankelijk van de volgende factoren Hallo:

- Hallo beleid Hallo Coordinator-Service. 
  - het standaardbeleid Hallo `NodeWise`, resulteert in het patchen slechts één knooppunt tegelijk. Met name in geval van grotere clusters hello wordt aangeraden dat u Hallo `UpgradeDomainWise` beleid tooachieve sneller patchen tussen verschillende clusters.
- Hallo aantal updates beschikbaar voor download en installatie. 
- gemiddelde tijd die nodig is toodownload Hallo en installeren van een update, wat mag niet meer dan een paar uur.
- Hallo-prestaties van de VM en netwerkbandbreedte Hallo.

Q. **Waarom zie ik bepaalde updates in Windows Update-resultaten die zijn verkregen via de REST-api, maar niet onder Hallo geschiedenis van Windows Update op de machine?**

A. Sommige productupdates moeten toobe in de geschiedenis van hun respectieve update/patch gecontroleerd. Bijvoorbeeld: Windows Defender-updates worden niet weergegeven in de geschiedenis van Windows Update op Windows Server 2016.

## <a name="disclaimers"></a>Disclaimers

- Hallo patch orchestration app accepteert Hallo eindgebruiker License Agreement van Windows Update namens de gebruiker Hallo. In de configuratie van de toepassing hello Hallo kan eventueel Hallo-instelling is uitgeschakeld.

- Hallo patch orchestration app verzamelt telemetrie tootrack gebruik en prestaties. Hallo toepassingstelemetrie volgt Hallo-instelling van Hallo Service Fabric-runtime van telemetrie (die standaard is ingeschakeld).

## <a name="troubleshooting"></a>Problemen oplossen

### <a name="a-node-is-not-coming-back-tooup-state"></a>Een knooppunt is niet terugkomen tooup status

**Hallo-knooppunt kan blijven steken in een status uitschakelen omdat**:

Er is een veiligheidscontrole in behandeling. tooremedy deze situatie Zorg dat er voldoende knooppunten beschikbaar in een foutloze toestand bevindt zijn.

**Hallo-knooppunt kan blijven steken uitgeschakeld omdat**:

- Hallo knooppunt is handmatig uitgeschakeld.
- Hallo-knooppunt is uitgeschakeld vanwege tooan lopende Azure-infrastructuur taak.
- Hallo-knooppunt is tijdelijk uitgeschakeld door Hallo patch orchestration app toopatch Hallo-knooppunt.

**Hallo knooppunt kan blijven steken in een status Omlaag omdat**:

- Hallo-knooppunt is geplaatst in een status Omlaag handmatig.
- Hallo-knooppunt is momenteel door een herstart (die kan worden geactiveerd door Hallo patch orchestration app).
- Hallo knooppunt vervalt tooa defecte VM of machine of het netwerk verbindingsproblemen.

### <a name="updates-were-skipped-on-some-nodes"></a>Updates zijn op sommige knooppunten overgeslagen

Hallo patch orchestration app probeert tooinstall een Windows update volgens toohello nieuwe beleid. Hallo-service probeert toorecover Hallo knooppunt en Hallo update volgens toohello toepassingsbeleid overslaan.

In dat geval wordt een waarschuwing het niveau statusrapport gegenereerd tegen Hallo knooppunt Agent-Service. Hallo-resultaat voor Windows Update bevat tevens Hallo mogelijke reden voor het Hallo-fout.

### <a name="hello-health-of-hello-cluster-goes-tooerror-while-hello-update-installs"></a>Hallo-status van Hallo cluster gaat tooerror terwijl het Hallo-update installeert

Een defecte Windows update kunt naar beneden Hallo status van een toepassing of het cluster op een bepaald knooppunt of upgradedomein brengen. Hallo patch orchestration app stoppen eventuele latere Windows Update-bewerking totdat Hallo cluster weer in orde is.

Moet een beheerder ingrijpen en bepalen waarom Hallo toepassing of het cluster is geworden vanwege onjuiste tooWindows Update.

## <a name="release-notes-"></a>Release-opmerkingen:

### <a name="version-110"></a>Versie 1.1.0
- Openbare versie

### <a name="version-111"></a>Versie 1.1.1
- Een bug vast entrypoint van NodeAgentService waardoor de installatie van NodeAgentNTService.

### <a name="version-120-latest"></a>Versie 1.2.0 (laatste)

- Werkstroom van oplossingen voor problemen rond systeem opnieuw starten.
- Fix fout bij het maken van RM taken toowhich statuscontrole tijdens het voorbereiden herstellen taken is niet zoals verwacht gebeurt.
- Gewijzigde Hallo opstartmodus voor windows-service POANodeSvc van automatische toodelayed-auto.
