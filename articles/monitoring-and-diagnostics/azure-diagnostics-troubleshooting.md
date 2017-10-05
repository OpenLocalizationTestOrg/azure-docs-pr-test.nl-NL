---
title: Het oplossen van Azure Diagnostics | Microsoft Docs
description: Problemen oplossen bij het gebruik van Azure diagnostics in Azure Virtual Machines, Service Fabric of Cloud Services.
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: 66469bce-d457-4d1e-b550-a08d2be4d28c
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/12/2017
ms.author: robb
ms.openlocfilehash: a0cb529836b14df71e83616f4f625a002c535b7b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-diagnostics-troubleshooting"></a>Azure Diagnostics probleemoplossing
Het oplossen van informatie die relevant zijn voor het gebruik van Azure Diagnostics. Zie voor meer informatie over Azure diagnostics [overzicht van Azure Diagnostics](azure-diagnostics.md).

## <a name="logical-components"></a>Logische onderdelen
**Starten van de invoegtoepassing Diagnostics (DiagnosticsPluginLauncher.exe)**: Hiermee start u de extensie Azure Diagnostics. Fungeert als de vermelding wijst proces.

**Diagnostics-invoegtoepassing (DiagnosticsPlugin.exe)**: Main-proces dat is gestart door de bovenstaande linksboven en configureert u de Monitoring Agent, deze wordt gestart en beheert de levensduur. 

**Monitoring Agent (MonAgent\*.exe processen)**: deze processen doen het grootste deel van het werk; dat wil zeggen, bewaking, verzameling en de overdracht van de diagnostics-gegevens.  

## <a name="logartifact-paths"></a>Logboek/artefact paden
Hier volgen de paden naar een aantal belangrijke logboeken en artefacten. We houden verwijzen naar deze in de rest van het document:
### <a name="cloud-services"></a>Cloudservices
| Artefacten | Pad |
| --- | --- |
| **Azure Diagnostics-configuratiebestand** | %SYSTEMDRIVE%\Packages\Plugins\Microsoft.Azure.Diagnostics.PaaSDiagnostics\<versie > \Config.txt |
| **Logboekbestanden** | C:\Logs\Plugins\Microsoft.Azure.Diagnostics.PaaSDiagnostics\<versie > \ |
| **Lokale archief voor diagnostische gegevens** | C:\Resources\Directory\<CloudServiceDeploymentID >.\< RoleName >. DiagnosticStore\WAD0107\Tables |
| **Monitoring Agent-configuratiebestand** | C:\Resources\Directory\<CloudServiceDeploymentID >.\< RoleName >. DiagnosticStore\WAD0107\Configuration\MaConfig.xml |
| **Azure diagnostics-extensie-pakket** | %SYSTEMDRIVE%\Packages\Plugins\Microsoft.Azure.Diagnostics.PaaSDiagnostics\<versie > |
| **Pad naar het logboek verzameling hulpprogramma** | %SYSTEMDRIVE%\Packages\GuestAgent\ |
| **Logboekbestand MonAgentHost** | C:\Resources\Directory\<CloudServiceDeploymentID >.\< RoleName >. DiagnosticStore\WAD0107\Configuration\MonAgentHost. < seq_num > .log |

### <a name="virtual-machines"></a>Virtuele machines
| Artefacten | Pad |
| --- | --- |
| **Azure Diagnostics-configuratiebestand** | C:\Packages\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<versie > \RuntimeSettings |
| **Logboekbestanden** | C:\Packages\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<versie > \Logs\ |
| **Lokale archief voor diagnostische gegevens** | C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<DiagnosticsVersion > \WAD0107\Tables |
| **Monitoring Agent-configuratiebestand** | C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<DiagnosticsVersion > \WAD0107\Configuration\MaConfig.xml |
| **Statusbestand** | C:\Packages\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<versie > \Status |
| **Azure diagnostics-extensie-pakket** | C:\Packages\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<DiagnosticsVersion >|
| **Pad naar het logboek verzameling hulpprogramma** | C:\WindowsAzure\Packages |
| **Logboekbestand MonAgentHost** | C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<DiagnosticsVersion > \WAD0107\Configuration\MonAgentHost. < seq_num > .log |

## <a name="metric-data-doesnt-show-in-azure-portal"></a>Metrische gegevens wordt niet weergegeven in Azure-portal
Azure Diagnostics biedt een aantal metrische gegevens die kunnen worden weergegeven in Azure-portal. Als u problemen met het bekijken van deze gegevens in de portal hebt, Controleer de opslagaccount voor diagnostische gegevens -> WADMetrics\* tabel om te zien als de bijbehorende metrische gegevens er zijn. Hier de PartitionKey van de tabel is de resource-ID van de virtuele machine of virtuele-machineschaalset en de RowKey is de naam van de meetwaarde dat wil zeggen prestatiemeternaam.

Als de resource-ID onjuist is, Controleer configuratie van diagnostische-Metrics > -> ResourceId om te zien als de resource-ID correct is ingesteld.

Als er geen gegevens voor de specifieke metrische gegevens,-controle van configuratie van diagnostische > PerformanceCounter om te zien als de metriek (prestatiemeteritem) opgenomen is. We de volgende prestatiemeteritems standaard ingeschakeld.
- \Processor(_Total)\% Processor Time
- \Memory\Available Bytes
- \ASP.NET toepassingen (__totale__) \Requests/Sec
- \ASP.NET toepassingen (__totale__) \Errors aantal bytes per seconde
- \ASP.NET\Requests in de wachtrij
- \ASP.NET\Requests geweigerd
- \Processor(W3wp)\% processortijd
- \Process (w3wp) \Private Bytes
- \Process(WaIISHost)\% processortijd
- \Process (WaIISHost) \Private Bytes
- \Process(WaWorkerHost)\% processortijd
- \Process (WaWorkerHost) \Private Bytes
- \Memory\Page fouten per seconde
- \.NET CLR-geheugen (_globale_)\% tijd in %
- \LogicalDisk (C:) \Disk geschreven Bytes per seconde
- \LogicalDisk (C:) \Disk gelezen Bytes per seconde
- \LogicalDisk (D:) \Disk geschreven Bytes per seconde
- \LogicalDisk (D:) \Disk gelezen Bytes per seconde

Als de configuratie correct is ingesteld, maar nog steeds de metrische gegevens niet weergegeven, volg de richtlijnen hieronder voor verder onderzoek.


## <a name="azure-diagnostics-is-not-starting"></a>Azure Diagnostics is niet gestart.
Bekijk **DiagnosticsPluginLauncher.log** en **DiagnosticsPlugin.log** bestanden van de locatie van de logboekbestanden van hierboven voor meer informatie over waarom diagnostics is niet gestart. 

Als deze logboeken aangeven `Monitoring Agent not reporting success after launch`, betekent dit er is een fout opgetreden bij het starten van MonAgentHost.exe. Bekijk de logboeken voor die op de locatie voor de `MonAgentHost log file` in de bovenstaande sectie.

De laatste regel van de logboekbestanden bevat de afsluitcode.  

```
DiagnosticsPluginLauncher.exe Information: 0 : [4/16/2016 6:24:15 AM] DiagnosticPlugin exited with code 0
```
Als u vindt een **negatieve** afsluitcode, raadpleeg dan de [afsluiten codetabel](#azure-diagnostics-plugin-exit-codes) in de [verwijzingen](#references).

## <a name="diagnostics-data-is-not-logged-to-azure-storage"></a>Diagnostics-gegevens is niet geregistreerd in Azure Storage
Bepalen of er zijn geen gegevens, wordt weergegeven of slechts enkele van de gegevens wordt niet weergegeven.

### <a name="diagnostics-infrastructure-logs"></a>Diagnostische gegevens infrastructuur Logboeken
Diagnostische gegevens infrastructuur Logboeken is waarin eventuele fouten die wordt uitgevoerd in de logboekbestanden worden azure diagnostics. Zorg ervoor dat u hebt ingeschakeld ([hoe?](#how-to-check-diagnostics-extension-configuration)) vast te leggen van infrastructuur diagnostische logboeken in uw configuratie en snel zoek naar eventuele relevante fouten die worden weergegeven in de `DiagnosticInfrastructureLogsTable` tabel in uw geconfigureerde storage-account.

### <a name="no-data-is-showing-up"></a>Er zijn geen gegevens, wordt weergegeven
De meest voorkomende oorzaak van de gebeurtenis volledig ontbrekende gegevens onjuist is gedefinieerd accountgegevens voor opslag.

Oplossing: Los van de configuratie van diagnostische en opnieuw installeren van diagnostische gegevens.

Als het opslagaccount juist geconfigureerde, extern is bureaublad in de machine en controleer of DiagnosticsPlugin.exe en MonAgentCore.exe worden uitgevoerd. Als ze niet worden uitgevoerd, voert u de [Azure Diagnostics is niet gestart](#azure-diagnostics-is-not-starting). Als de processen worden uitgevoerd, Ga naar [gegevens ophalen van lokaal vastgelegd](#is-data-getting-captured-locally) en deze handleiding vanaf daar volgen op.

### <a name="part-of-the-data-is-missing"></a>Deel van de gegevens ontbreekt
Als u bepaalde gegevens wel, maar geen andere. Dit betekent dat de gegevensverzameling-overdracht pijplijn correct is ingesteld. Ga als volgt de subsecties hier om te beperken wat het probleem is:
#### <a name="is-collection-configured"></a>Is een verzameling geconfigureerd: 
Configuratie van diagnostische bevat het deel zodat voor een bepaald type van de gegevens worden verzameld. [Controleer de configuratie van uw](#how-to-check-diagnostics-extension-configuration) om ervoor te zorgen dat u niet op zoek naar gegevens die u niet hebt geconfigureerd voor de verzameling.
#### <a name="is-the-host-generating-data"></a>De host gegevens genereert:
- **Prestatiemeteritems**: perfmon openen en controleren van de teller.
- **Traceerlogboeken**: extern bureaublad in de virtuele machine en een TextWriterTraceListener toevoegen aan het configuratiebestand van de app.  Zie http://msdn.microsoft.com/library/sk36c28t.aspx voor het instellen van de listener tekst.  Zorg ervoor dat de `<trace>` element heeft `<trace autoflush="true">`.<br />
Als u logboeken met traceringen ophalen gegenereerd niet ziet, voert u de [meer over Trace logboeken ontbreekt](#more-about-trace-logs-missing).
- **ETW-traceringen**: extern bureaublad in de virtuele machine en installeer de PerfView.  In uitvoering File -> PerfView-opdracht User > Listen etwprovder1, etwprovider2, enzovoort.  Houd er rekening mee dat de Listen-opdracht hoofdlettergevoelig is en kan niet spaties tussen de door komma's gescheiden lijst met ETW-providers worden.  Als de opdracht niet kan worden uitgevoerd, kunt u de knop 'Log' in de rechtsonder in het hulpprogramma Perfview om te zien wat er is geprobeerd om uit te voeren en wat het resultaat was.  Ervan uitgaande dat de invoer juist dat vervolgens een nieuw venster wordt weergegeven en in een paar seconden die nu begint u ETW traceringen te zien is.
- **Gebeurtenislogboeken**: extern bureaublad in de virtuele machine. Open `Event Viewer` en zorg ervoor dat de gebeurtenissen bestaan.
#### <a name="is-data-getting-captured-locally"></a>Is gegevens lokaal ophalen vastgelegd:
Zorg vervolgens dat lokaal worden de gegevens ophalen van omgezet.
De gegevens worden lokaal opgeslagen `*.tsf` bestanden in [het lokale archief voor diagnostische gegevens](#log-artifacts-path). Verschillende soorten logboeken ophalen die zijn verzameld in andere `.tsf` bestanden. De namen zijn vergelijkbaar met de tabelnamen van de in azure-opslag. Bijvoorbeeld `Performance Counters` ophalen die worden verzameld in `PerformanceCountersTable.tsf`, gebeurtenislogboeken ophalen verzameld in `WindowsEventLogsTable.tsf`. Volg de instructies in [lokale logboek extractie](#local-log-extraction) sectie aan de lokale verzamelingsbestanden openen en zorg ervoor dat u ze op de schijf ophalen verzameld zien.

Als u Logboeken lokaal ophalen verzameld niet ziet en al hebt gecontroleerd dat de host van gegevens genereren, hebt u waarschijnlijk een configuratieprobleem. Controleer uw configuratie zorgvuldig controleert op voor het desbetreffende gedeelte. Bekijk ook de configuratie die is gegenereerd voor MonitoringAgent [MaConfig.xml](#log-artifacts-path) en zorg ervoor dat er is een aantal sectie met een beschrijving van de bron van de relevante logboekbestanden en dat deze niet in de vertaling af tussen azure diagnostics configuratie gaat verloren en de agentconfiguratie van de bewaking.
#### <a name="is-data-getting-transferred"></a>Worden de gegevens ophalen van verzonden:
Als u de gegevens wordt lokaal ophalen vastgelegd, maar nog steeds deze niet wordt weergegeven in uw opslagaccount hebt gecontroleerd: 
- Allereerst omdat Zorg dat u een juiste storage-account hebt opgegeven en dat u hebt niet teruggedraaid via sleutels etc.for het opgegeven opslagaccount. Voor cloud-services, soms zien we dat mensen niet bijwerken hun `useDevelopmentStorage=true`.
- Als de opgegeven storage-account juist is. Zorg ervoor dat u hebt geen enkele netwerkbeperkingen die de onderdelen te bereiken openbare opslag eindpunten niet toestaan. Een manier om u te doen is met extern bureaublad verbinding met de machine en probeer schrijven iets naar hetzelfde opslagaccount zelf.
- Ten slotte kunt u proberen en zien welk probleem zijn gemeld door Monitoring Agent. Bewakingsagent schrijft de logboeken `maeventtable.tsf` zich in [het lokale archief voor diagnostische gegevens](#log-artifacts-path). Volg de instructies in [lokale logboek extractie](#local-log-extraction) sectie om dit bestand openen en te achterhalen of er zijn `errors` die wijzen op mislukte lokale bestanden lezen of schrijven naar de opslag.

### <a name="capturing--archiving-logs"></a>Vastleggen / logboeken archiveren
De bovenstaande stappen doorlopen, maar kan niet achterhalen wat is onjuist en nadenken over contact opnemen met ondersteuning zijn. Het eerste wat dat kunnen ze u vragen is voor het verzamelen van Logboeken vanaf uw computer. U kunt tijd besparen door dit zelf doen. Voer de `CollectGuestLogs.exe` hulpprogramma op [pad naar het logboek verzameling hulpprogramma](#log-artifacts-path) en genereert een zip-bestand met alle relevante azure Logboeken in dezelfde map.

## <a name="diagnostics-data-tables-not-found"></a>Diagnostische gegevens tabellen niet gevonden
De tabellen in Azure storage ETW-gebeurtenissen die worden benoemd met de volgende code:

```C#
        if (String.IsNullOrEmpty(eventDestination)) {
            if (e == "DefaultEvents")
                tableName = "WADDefault" + MD5(provider);
            else
                tableName = "WADEvent" + MD5(provider) + eventId;
        }
        else
            tableName = "WAD" + eventDestination;
```

Hier volgt een voorbeeld:

```XML
        <EtwEventSourceProviderConfiguration provider="prov1">
          <Event id="1" />
          <Event id="2" eventDestination="dest1" />
          <DefaultEvents />
        </EtwEventSourceProviderConfiguration>
        <EtwEventSourceProviderConfiguration provider="prov2">
          <DefaultEvents eventDestination="dest2" />
        </EtwEventSourceProviderConfiguration>
```
```JSON
"EtwEventSourceProviderConfiguration": [
    {
        "provider": "prov1",
        "Event": [
            {
                "id": 1
            },
            {
                "id": 2,
                "eventDestination": "dest1"
            }
        ],
        "DefaultEvents": {
            "eventDestination": "DefaultEventDestination",
            "sinks": ""
        }
    },
    {
        "provider": "prov2",
        "DefaultEvents": {
            "eventDestination": "dest2"
        }
    }
]
```
Die 4 tabellen genereert:

| Gebeurtenis | De tabelnaam van de |
| --- | --- |
| provider = 'prov1' &lt;gebeurtenis-id = "1" /&gt; |WADEvent + MD5("prov1") + '1' |
| provider = 'prov1' &lt;gebeurtenis-id = "2" eventDestination = "dest1" /&gt; |WADdest1 |
| provider = 'prov1' &lt;DefaultEvents /&gt; |WADDefault+MD5("prov1") |
| provider = 'prov2' &lt;DefaultEvents eventDestination = "dest2" /&gt; |WADdest2 |

## <a name="references"></a>Verwijzingen

### <a name="how-to-check-diagnostics-extension-configuration"></a>Configuratie van diagnostische-extensie controleren
De eenvoudigste manier om te controleren van uw configuratie voor de uitbreiding is om te navigeren naar http://resources.azure.com, gaat u naar de virtuele machine of service in de cloud waarin de extensie Azure Diagnostics (IaaSDiagnostics / PaaDiagnostics) is mogelijk geschonden.

U kunt ook extern bureaublad in de machine en bekijk het configuratiebestand van Azure Diagnostics wordt beschreven in het desbetreffende gedeelte [hier](#log-artifacts-path).

In beide hoofdlettergevoelig zoeken naar **Microsoft.Azure.Diagnostics** vervolgens voor de **xmlCfg** of **WadCfg** veld. 

In geval van virtuele machines, als het veld WadCfg aanwezig is, betekent dit dat de configuratie in JSON. Als het veld xmlCfg aanwezig is, betekent dit config in XML en base64-gecodeerd is. U moet [dit decoderen](http://www.bing.com/search?q=base64+decoder) om te zien van de XML-bestand dat is geladen door diagnostische gegevens.

Voor de rol van de Cloudservice, als u de configuratie van de schijf, kiest de gegevens is met base64 gecodeerd dus u moet [dit decoderen](http://www.bing.com/search?q=base64+decoder) om te zien van de XML-bestand dat is geladen door diagnostische gegevens.

### <a name="azure-diagnostics-plugin-exit-codes"></a>Afsluitcodes van Azure Diagnostics-invoegtoepassing
De invoegtoepassing wordt de volgende afsluitcodes geretourneerd:

| Afsluitcode | Beschrijving |
| --- | --- |
| 0 |Geslaagd. |
| -1 |Algemene fout. |
| -2 |De rcf kan bestand niet laden.<p>Deze interne fout vindt alleen plaats als u de guest agent invoegtoepassing launcher is handmatig wordt aangeroepen, onjuist op de virtuele machine. |
| -3 |Kan het configuratiebestand van de diagnostische gegevens niet laden.<p><p>Oplossing: Veroorzaakt door een configuratiebestand niet schemavalidatie wordt doorgegeven. De oplossing is om een configuratiebestand die voldoet aan het schema. |
| -4 |De lokale resource-map wordt al gebruikt door een ander exemplaar van de bewakingsagent diagnostische gegevens.<p><p>Oplossing: Geef een andere waarde voor **LocalResourceDirectory**. |
| -6 |De Gast-agent invoegtoepassing launcher geprobeerd diagnostische gegevens starten met een opdrachtregel ongeldig is.<p><p>Deze interne fout vindt alleen plaats als u de guest agent invoegtoepassing launcher is handmatig wordt aangeroepen, onjuist op de virtuele machine. |
| -10 |De Diagnostics-invoegtoepassing is afgesloten met een niet-verwerkte uitzondering. |
| -11 |De gastagent kon het proces is verantwoordelijk voor het starten en het controleren van de bewakingsagent gemaakt.<p><p>Oplossing: Controleer of voldoende systeembronnen beschikbaar zijn voor het nieuwe processen te starten.<p> |
| -101 |Ongeldige argumenten bij het aanroepen van de Diagnostics-invoegtoepassing.<p><p>Deze interne fout vindt alleen plaats als u de guest agent invoegtoepassing launcher is handmatig wordt aangeroepen, onjuist op de virtuele machine. |
| -102 |Het proces van de invoegtoepassing is niet geïnitialiseerd.<p><p>Oplossing: Controleer of voldoende systeembronnen beschikbaar zijn voor het nieuwe processen te starten. |
| -103 |Het proces van de invoegtoepassing is niet geïnitialiseerd. Het is speciaal kan het berichtenlogboek-object niet maken.<p><p>Oplossing: Controleer of voldoende systeembronnen beschikbaar zijn voor het nieuwe processen te starten. |
| -104 |Kan niet laden van de rcf-bestand dat is opgegeven door de gastagent.<p><p>Deze interne fout vindt alleen plaats als u de guest agent invoegtoepassing launcher is handmatig wordt aangeroepen, onjuist op de virtuele machine. |
| -105 |De Diagnostics-invoegtoepassing kan het configuratiebestand van de diagnostische gegevens niet openen.<p><p>Deze interne fout vindt alleen plaats als de Diagnostics-invoegtoepassing is handmatig wordt aangeroepen, onjuist op de virtuele machine. |
| -106 |Kan het configuratiebestand van de diagnostische gegevens niet lezen.<p><p>Oplossing: Veroorzaakt door een configuratiebestand niet schemavalidatie wordt doorgegeven. De oplossing is daarom een configuratiebestand die voldoet aan het schema te leveren. Zie [het controleren van de configuratie van diagnostische extensie](#how-to-check-diagnostics-extension-configuration). |
| -107 |De bron directory op te geven met de monitoring agent is ongeldig.<p><p>Deze interne fout vindt alleen plaats als monitoring agent is handmatig wordt aangeroepen, onjuist op de virtuele machine.</p> |
| -108 |Kan niet converteren van het configuratiebestand van de diagnostische gegevens naar het monitoring agent-configuratiebestand.<p><p>Deze interne fout vindt alleen plaats als de Diagnostics-invoegtoepassing handmatig wordt aangeroepen met een ongeldig configuratiebestand. |
| -110 |Algemene Diagnostics configuratiefout.<p><p>Deze interne fout vindt alleen plaats als de Diagnostics-invoegtoepassing handmatig wordt aangeroepen met een ongeldig configuratiebestand. |
| -111 |Kan niet starten van de bewakingsagent.<p><p>Oplossing: Controleer of er voldoende systeembronnen beschikbaar zijn. |
| -112 |Algemene fout |

### <a name="local-log-extraction"></a>Uitpakken van de lokale logboek
De monitoring agent verzamelt logboeken en artefacten zoals `.tsf` bestanden. `.tsf`bestand kan niet worden gelezen, maar u kunt converteren naar een `.csv` als volgt: 

```
<Azure diagnostics extension package>\Monitor\x64\table2csv.exe <relevantLogFile>.tsf
```
Een nieuw bestand genaamd `<relevantLogFile>.csv` wordt gemaakt in hetzelfde pad hebben als de bijbehorende `.tsf` bestand.

**Opmerking**: U hoeft dit hulpprogramma uitvoeren op basis van de belangrijkste tsf-bestand (bijvoorbeeld PerformanceCountersTable.tsf). De bijbehorende bestanden (bijv, PerformanceCountersTables_\*\*001.tsf, PerformanceCountersTables_\*\*002. tsf enz.) wordt automatisch verwerkt.

### <a name="more-about-trace-logs-missing"></a>Meer informatie over traceerlogboeken ontbreekt

**Opmerking:** dit voornamelijk geldt voor cloud-services alleen tenzij u de DiagnosticsMonitorTraceListener op een toepassing die wordt uitgevoerd op uw IaaS VM hebt geconfigureerd. 

- Zorg ervoor dat de DiagnosticMonitorTraceListener is geconfigureerd in web.config of app.config.  Dit is standaard in cloudserviceprojecten geconfigureerd, maar sommige klanten commentaar af dat hierdoor de trace-instructies moeten niet worden verzameld door diagnostische gegevens. 
- Als u Logboeken niet ophalen van geschreven door de methode OnStart of voer Zorg ervoor dat de DiagnosticMonitorTraceListener in het app.config.  Standaard is dit in het bestand web.config, maar die alleen van toepassing op code die wordt uitgevoerd binnen w3wp.exe; Daarom moet u deze in app.config voor het vastleggen van traces in WaIISHost.exe uitgevoerd.
- Zorg ervoor dat u in plaats van Diagnostics.Debug.WriteXXX Diagnostics.Trace.TraceXXX gebruikt.  De foutopsporingsinstructies wordt verwijderd uit een Release-build.
- Zorg ervoor dat de gecompileerde code daadwerkelijk Diagnostics.Trace regels (gebruik Routereflector, ildasm of ILSpy controleren).  Diagnostics.Trace opdrachten worden verwijderd van de gecompileerde binary, tenzij u het symbool TRACE-voorwaardelijke compilatie.  Als u msbuild voor het bouwen van het project is dit een veelvoorkomend probleem te maken.

## <a name="known-issues-and-mitigations"></a>Bekende problemen en oplossingen
Hier volgt een lijst met bekende problemen met bekende oplossingen:

**1. .NET 4.5-afhankelijkheid:**

AF heeft een runtime-afhankelijkheid op framework .NET 4.5 of hoger. Op het moment van schrijven van dit alle machines die zijn ingericht voor cloud-services, evenals alle officiële azure virtuele Machine basisinstallatiekopieën .NET 4.5 of hoger geïnstalleerd. Het is nog steeds echter mogelijk te terechtkomen in een situatie waarin u probeert uit te voeren af op een computer die geen .NET 4.5 of hoger. Dit gebeurt wanneer u de computer afmeldt bij een oude afbeelding of momentopname; maken of uw eigen aangepaste schijf zetten.

Dit in het algemeen als een afsluitcode manifesten **255** bij het uitvoeren van DiagnosticsPluginLauncher.exe. Fout gebeurt vanwege de niet-verwerkte uitzondering: 
```
System.IO.FileLoadException: Could not load file or assembly 'System.Threading.Tasks, Version=1.5.11.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a' or one of its dependencies
```

**Risicobeperking:** .NET 4.5 of hoger op uw computer installeren.

**2. Prestatiemeteritems prestatiegegevens beschikbaar in de opslag, maar niet worden weergegeven in de portal**

Portal-ervaring van virtuele machines worden bepaalde prestatiemeteritems standaard weergegeven. Als u deze niet ziet en u weet dat de gegevens ophalen van gegenereerd omdat deze in de opslagruimte beschikbaar is. Controleren:
- Als de gegevens in de opslag itemnamen in het Engels heeft. Als de namen van prestatiemeteritems niet in het Engels, kunnen portal metrische grafiek zich niet wordt herkend.
- Als u jokertekens (\*) in de namen van prestatiemeteritems, de portal kan niet worden met elkaar correleren van de teller geconfigureerd en die worden verzameld.

**Risicobeperking**: de taal van de machine naar het Engels voor systeemaccounts wijzigen. Het Configuratiescherm -> regio -> Beheersjablonen -> Instellingen -> Schakel het selectievakje 'Welkom en systeemaccounts' zodat de aangepaste taal niet op het systeem-account toegepast wordt. Controleer ook of dat u geen jokertekens gebruiken als u wilt dat de portal om te worden van uw ervaring primaire verbruik.
