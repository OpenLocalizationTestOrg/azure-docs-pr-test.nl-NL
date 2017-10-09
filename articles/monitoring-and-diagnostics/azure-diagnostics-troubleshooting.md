---
title: aaaTroubleshooting Azure Diagnostics | Microsoft Docs
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
ms.openlocfilehash: daaf9fa4c40982eb9ba04030d7e8ea1ad9fe085b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-troubleshooting"></a>Azure Diagnostics probleemoplossing
Het oplossen van informatie relevante toousing Azure Diagnostics. Zie voor meer informatie over Azure diagnostics [overzicht van Azure Diagnostics](azure-diagnostics.md).

## <a name="logical-components"></a>Logische onderdelen
**Starten van de invoegtoepassing Diagnostics (DiagnosticsPluginLauncher.exe)**: hello Azure Diagnostics uitbreiding wordt gestart. Fungeert als Hallo post wijst proces.

**Diagnostics-invoegtoepassing (DiagnosticsPlugin.exe)**: Main-proces dat is gestart door Hallo launcher bovenstaande en Hallo Monitoring Agent configureert, start deze en beheert de levensduur. 

**Monitoring Agent (MonAgent\*.exe processen)**: deze processen bulksgewijs Hallo werk Hallo; dat wil zeggen, bewaking, verzameling en overdracht van Hallo diagnostics-gegevens.  

## <a name="logartifact-paths"></a>Logboek/artefact paden
Hier volgen Hallo paden toosome belangrijke logboeken en -artefacten. We houden toothese in de rest Hallo van Hallo document verwijzen:
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
Azure Diagnostics biedt een aantal metrische gegevens die kunnen worden weergegeven in Azure-portal. Als u problemen met het bekijken van deze gegevens in de portal hebt, opslagaccount voor diagnostische gegevens van selectievakje Hallo -> WADMetrics\* toosee tabel als Hallo bijbehorende metrische gegevens er zijn. Hier Hallo PartitionKey van Hallo-tabel is Hallo bron-ID van de virtuele machine of virtuele-machineschaalset en Hallo RowKey Hallo metrische naam dat wil zeggen prestatiemeternaam is.

Als Hallo resource-ID onjuist is, Controleer configuratie van diagnostische -> metrische gegevens ResourceId toosee -> als Hallo resource-ID juist is ingesteld.

Als er geen gegevens voor de specifieke metrische gegevens hello,-controle van configuratie van diagnostische PerformanceCounter toosee > als Hallo metriek (prestatiemeteritem) is opgenomen. We inschakelen Hallo prestatiemeteritems te volgen standaard.
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

Als Hallo configuratie correct is ingesteld, maar nog steeds Hallo metrische gegevens niet weergegeven, voert u de richtlijnen Hallo hieronder voor verder onderzoek Hallo.


## <a name="azure-diagnostics-is-not-starting"></a>Azure Diagnostics is niet gestart.
Bekijk **DiagnosticsPluginLauncher.log** en **DiagnosticsPlugin.log** bestanden van de locatie Hallo Hallo logboekbestanden opgegeven hierboven voor meer informatie over waarom diagnostics is niet toostart. 

Als deze logboeken aangeven `Monitoring Agent not reporting success after launch`, betekent dit er is een fout opgetreden bij het starten van MonAgentHost.exe. Bekijkt hello logboeken voor die op Hallo locatie voor de `MonAgentHost log file` bij Hallo hierboven.

laatste regel van de logboekbestanden Hallo Hallo bevat Hallo afsluitcode.  

```
DiagnosticsPluginLauncher.exe Information: 0 : [4/16/2016 6:24:15 AM] DiagnosticPlugin exited with code 0
```
Als u vindt een **negatieve** afsluitcode, raadpleeg dan toohello [afsluiten codetabel](#azure-diagnostics-plugin-exit-codes) in Hallo [verwijzingen](#references).

## <a name="diagnostics-data-is-not-logged-tooazure-storage"></a>Diagnostics-gegevens is niet geregistreerd tooAzure opslag
Bepalen of er zijn geen gegevens, wordt weergegeven of slechts enkele Hallo gegevens wordt niet weergegeven.

### <a name="diagnostics-infrastructure-logs"></a>Diagnostische gegevens infrastructuur Logboeken
Diagnostische gegevens infrastructuur Logboeken is waarin eventuele fouten die wordt uitgevoerd in de logboekbestanden worden azure diagnostics. Zorg ervoor dat u hebt ingeschakeld ([hoe?](#how-to-check-diagnostics-extension-configuration)) vast te leggen van infrastructuur diagnostische logboeken in uw configuratie en snel zoek naar eventuele relevante fouten die worden weergegeven in Hallo `DiagnosticInfrastructureLogsTable` tabel in uw geconfigureerde storage-account.

### <a name="no-data-is-showing-up"></a>Er zijn geen gegevens, wordt weergegeven
Hallo meest voorkomende oorzaak van gebeurtenisgegevens volledig ontbreekt is niet goed gedefinieerde opslag accountgegevens.

Oplossing: Los van de configuratie van diagnostische en opnieuw installeren van diagnostische gegevens.

Als Hallo storage-account correct geconfigureerde, extern is bureaublad in Hallo-machine en zorg ervoor dat DiagnosticsPlugin.exe en MonAgentCore.exe worden uitgevoerd. Als ze niet worden uitgevoerd, voert u de [Azure Diagnostics is niet gestart](#azure-diagnostics-is-not-starting). Als het Hallo-processen worden uitgevoerd, te gaan[gegevens ophalen van lokaal vastgelegd](#is-data-getting-captured-locally) en deze handleiding vanaf daar volgen op.

### <a name="part-of-hello-data-is-missing"></a>Deel van de gegevens Hallo ontbreekt
Als u bepaalde gegevens wel, maar geen andere. Dit betekent dat de gegevensverzameling Hallo-overdracht pijplijn correct is ingesteld. Ga als volgt Hallo subsecties hier toonarrow omlaag welk probleem Hallo is:
#### <a name="is-collection-configured"></a>Is een verzameling geconfigureerd: 
Configuratie van diagnostische bevat Hallo gedeelte zodat voor een bepaald type gegevens toobe verzameld. [Controleer de configuratie van uw](#how-to-check-diagnostics-extension-configuration) toomake zeker dat u niet zoekt gegevens u niet hebt geconfigureerd voor de verzameling.
#### <a name="is-hello-host-generating-data"></a>Hallo host gegevens genereert:
- **Prestatiemeteritems**: perfmon opent en controleert u Hallo teller.
- **Traceerlogboeken**: extern bureaublad in Hallo VM en voeg een TextWriterTraceListener toohello-app-configuratiebestand.  Zie http://msdn.microsoft.com/library/sk36c28t.aspx tooset Hallo tekst-listener geïnstalleerd.  Zorg ervoor dat Hallo `<trace>` element heeft `<trace autoflush="true">`.<br />
Als u logboeken met traceringen ophalen gegenereerd niet ziet, voert u de [meer over Trace logboeken ontbreekt](#more-about-trace-logs-missing).
- **ETW-traceringen**: extern bureaublad in Hallo VM en installeer PerfView.  In uitvoering File -> PerfView-opdracht User > Listen etwprovder1, etwprovider2, enzovoort.  Houd er rekening mee dat Hallo luister-opdracht hoofdlettergevoelig is en kan niet spaties tussen Hallo door komma's gescheiden lijst met ETW-providers worden.  Als Hallo opdracht toorun mislukt, kunt u klikken Hallo 'Log' in hello rechtsonder in Hallo Perfview hulpprogramma toosee die wat zijn geprobeerde toorun en welke Hallo resultaat was.  Ervan uitgaande dat Hallo invoer juist dat vervolgens een nieuw venster wordt weergegeven en in een paar seconden is nu begint u ETW traceringen te zien.
- **Gebeurtenislogboeken**: extern bureaublad in Hallo VM. Open `Event Viewer` en zorg ervoor dat Hallo gebeurtenissen bestaan.
#### <a name="is-data-getting-captured-locally"></a>Is gegevens lokaal ophalen vastgelegd:
Zorg naast Hallo gegevens wordt lokaal ophalen vastgelegd.
Hallo-gegevens worden lokaal opgeslagen in `*.tsf` bestanden in [Hallo lokale archief voor diagnostische gegevens](#log-artifacts-path). Verschillende soorten logboeken ophalen die zijn verzameld in andere `.tsf` bestanden. Hallo-namen zijn vergelijkbaar toohello tabelnamen in azure-opslag. Bijvoorbeeld `Performance Counters` ophalen die worden verzameld in `PerformanceCountersTable.tsf`, gebeurtenislogboeken ophalen verzameld in `WindowsEventLogsTable.tsf`. Gebruik Hallo-instructies in [lokale logboek extractie](#local-log-extraction) sectie tooopen Hallo lokale verzamelingsbestanden en zorg ervoor dat u ze op de schijf ophalen verzameld zien.

Als u geen Raadpleeg Logboeken lokaal ophalen verzameld en al hebt geverifieerd dat Hallo host genereren van gegevens, hebt u waarschijnlijk een configuratieprobleem. Controleer uw configuratie voor de bijbehorende sectie Hallo zorgvuldig. Bekijk ook Hallo configuratie gegenereerd voor MonitoringAgent [MaConfig.xml](#log-artifacts-path) en zorg ervoor dat er een gedeelte beschrijven Hallo relevante logboek bron- en niet gaat verloren in de conversie van azure diagnostics-configuratie en agentconfiguratie van de bewaking.
#### <a name="is-data-getting-transferred"></a>Worden de gegevens ophalen van verzonden:
Als u hebt gecontroleerd Hallo gegevens wordt lokaal ophalen vastgelegd, maar nog steeds deze niet wordt weergegeven in uw opslagaccount: 
- Allereerst omdat Zorg dat u een juiste storage-account hebt opgegeven en dat u hebt niet overgeschakeld sleutels etc.for Hallo storage-account opgegeven. Voor cloud-services, soms zien we dat mensen niet bijwerken hun `useDevelopmentStorage=true`.
- Als de opgegeven storage-account juist is. Zorg ervoor dat u hebt geen enkele netwerkbeperkingen die niet toestaan Hallo onderdelen tooreach openbare opslag eindpunten. Eenzijdige toodo die tooremote bureaublad in Hallo machine en probeer het toowrite iets toohello dezelfde opslag account zelf.
- Ten slotte kunt u proberen en zien welk probleem zijn gemeld door Monitoring Agent. Bewakingsagent schrijft de logboeken `maeventtable.tsf` zich in [Hallo lokale archief voor diagnostische gegevens](#log-artifacts-path). Volg de instructies in [lokale logboek extractie](#local-log-extraction) sectie tooopen dit bestand en probeer het en nagaan of er zijn `errors` fouten tooread lokale bestanden die aangeeft of toostorage schrijven.

### <a name="capturing--archiving-logs"></a>Vastleggen / logboeken archiveren
Hallo bovenstaande stappen doorlopen, maar kan niet achterhalen wat is onjuist en nadenken over contact opnemen met ondersteuning zijn. Allereerst Hallo die kunnen ze u vragen is toocollect Logboeken vanaf uw computer. U kunt tijd besparen door dit zelf doen. Voer Hallo `CollectGuestLogs.exe` hulpprogramma op [pad naar het logboek verzameling hulpprogramma](#log-artifacts-path) en genereert een zip-bestand met alle relevante azure Logboeken in Hallo dezelfde map.

## <a name="diagnostics-data-tables-not-found"></a>Diagnostische gegevens tabellen niet gevonden
Hallo-tabellen in Azure storage ETW-gebeurtenissen die worden benoemd met behulp van de volgende code Hallo:

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

### <a name="how-toocheck-diagnostics-extension-configuration"></a>Hoe toocheck configuratie voor uitbreiding van diagnostische gegevens
Hallo gemakkelijkste manier toocheck uw configuratie voor de uitbreiding is toonavigate toohttp://resources.azure.com, gaat u toohello virtuele machine of cloud-service op welke hello Azure Diagnostics-extensie (IaaSDiagnostics / PaaDiagnostics) is mogelijk geschonden.

U kunt ook extern bureaublad in Hallo-machine en bekijkt hello Azure Diagnostics-configuratiebestand beschreven in de bijbehorende sectie Hallo [hier](#log-artifacts-path).

In beide hoofdlettergevoelig zoeken naar **Microsoft.Azure.Diagnostics** vervolgens voor Hallo **xmlCfg** of **WadCfg** veld. 

In geval van virtuele machines als Hallo WadCfg veld aanwezig is, betekent dit dat Hallo config in JSON. Als Hallo xmlCfg veld aanwezig is, betekent dit Hallo config in XML en base64-gecodeerd is. U moet te[dit decoderen](http://www.bing.com/search?q=base64+decoder) toosee Hallo XML-bestand dat is geladen door diagnostische gegevens.

Voor de rol van de Cloudservice, als u de configuratie van de schijf, Hallo kiest Hallo gegevens is met base64 gecodeerd en u te moet[dit decoderen](http://www.bing.com/search?q=base64+decoder) toosee Hallo XML-bestand dat is geladen door diagnostische gegevens.

### <a name="azure-diagnostics-plugin-exit-codes"></a>Afsluitcodes van Azure Diagnostics-invoegtoepassing
Hallo-invoegtoepassing retourneert Hallo afsluitcodes te volgen:

| Afsluitcode | Beschrijving |
| --- | --- |
| 0 |Geslaagd. |
| -1 |Algemene fout. |
| -2 |Kan geen tooload Hallo rcf bestand.<p>Deze interne fout moet alleen gebeuren als Hallo guest agent invoegtoepassing launcher is handmatig wordt aangeroepen, onjuist op Hallo VM. |
| -3 |Kan de Hallo Diagnostics-configuratiebestand niet laden.<p><p>Oplossing: Veroorzaakt door een configuratiebestand niet schemavalidatie wordt doorgegeven. Hallo-oplossing is tooprovide een configuratiebestand dat aan het Hallo-schema voldoet. |
| -4 |Hallo lokale resource directory wordt al gebruikt door een ander exemplaar van Hallo bewakingsagent diagnostische gegevens.<p><p>Oplossing: Geef een andere waarde voor **LocalResourceDirectory**. |
| -6 |Hallo guest agent invoegtoepassing launcher geprobeerd toolaunch diagnostische gegevens met een opdrachtregel ongeldig is.<p><p>Deze interne fout moet alleen gebeuren als Hallo guest agent invoegtoepassing launcher is handmatig wordt aangeroepen, onjuist op Hallo VM. |
| -10 |Hallo Diagnostics invoegtoepassing is afgesloten met een niet-verwerkte uitzondering. |
| -11 |Hallo guest-agent is verantwoordelijk voor het starten en het Hallo bewakingsagent bewaking niet kan toocreate Hallo-proces.<p><p>Oplossing: Controleer of voldoende systeembronnen beschikbaar toolaunch nieuwe processen.<p> |
| -101 |Ongeldige argumenten bij het aanroepen van Hallo-invoegtoepassing voor diagnostische gegevens.<p><p>Deze interne fout moet alleen gebeuren als Hallo guest agent invoegtoepassing launcher is handmatig wordt aangeroepen, onjuist op Hallo VM. |
| -102 |Hallo-invoegtoepassing proces is tooinitialize zelf.<p><p>Oplossing: Controleer of voldoende systeembronnen beschikbaar toolaunch nieuwe processen. |
| -103 |Hallo-invoegtoepassing proces is tooinitialize zelf. Het is speciaal niet kan toocreate Hallo berichtenlogboek object.<p><p>Oplossing: Controleer of voldoende systeembronnen beschikbaar toolaunch nieuwe processen. |
| -104 |Kan geen tooload Hallo rcf bestand dat is opgegeven door Hallo guest-agent.<p><p>Deze interne fout moet alleen gebeuren als Hallo guest agent invoegtoepassing launcher is handmatig wordt aangeroepen, onjuist op Hallo VM. |
| -105 |Hallo Diagnostics invoegtoepassing kan Hallo Diagnostics-configuratiebestand niet openen.<p><p>Deze interne fout moet alleen gebeuren als Hallo Diagnostics invoegtoepassing is handmatig wordt aangeroepen, onjuist op Hallo VM. |
| -106 |Kan de Hallo Diagnostics-configuratiebestand niet lezen.<p><p>Oplossing: Veroorzaakt door een configuratiebestand niet schemavalidatie wordt doorgegeven. Hallo-oplossing is daarom tooprovide een configuratiebestand dat aan het Hallo-schema voldoet. Zie [hoe toocheck configuratie van diagnostische extensie](#how-to-check-diagnostics-extension-configuration). |
| -107 |Hallo resource directory pass toohello bewakingsagent is ongeldig.<p><p>Deze interne fout moet alleen gebeuren als Hallo monitoring agent is handmatig wordt aangeroepen, onjuist op Hallo VM.</p> |
| -108 |Kan geen tooconvert Hallo Diagnostics configuratiebestand in Hallo monitoring agent-configuratiebestand.<p><p>Deze interne fout moet alleen gebeuren als Hallo Diagnostics invoegtoepassing handmatig wordt aangeroepen met een ongeldig configuratiebestand. |
| -110 |Algemene Diagnostics configuratiefout.<p><p>Deze interne fout moet alleen gebeuren als Hallo Diagnostics invoegtoepassing handmatig wordt aangeroepen met een ongeldig configuratiebestand. |
| -111 |Kan geen toostart Hallo monitoring agent.<p><p>Oplossing: Controleer of er voldoende systeembronnen beschikbaar zijn. |
| -112 |Algemene fout |

### <a name="local-log-extraction"></a>Uitpakken van de lokale logboek
Hallo monitoring agent verzamelt logboeken en artefacten zoals `.tsf` bestanden. `.tsf`bestand kan niet worden gelezen, maar u kunt converteren naar een `.csv` als volgt: 

```
<Azure diagnostics extension package>\Monitor\x64\table2csv.exe <relevantLogFile>.tsf
```
Een nieuw bestand genaamd `<relevantLogFile>.csv` worden aangemaakt in Hallo hetzelfde pad als Hallo overeenkomt `.tsf` bestand.

**Opmerking**: U hoeft alleen toorun dit hulpprogramma tegen Hallo belangrijkste tsf-bestand (bijvoorbeeld PerformanceCountersTable.tsf). Hallo bijbehorende bestanden (bijv, PerformanceCountersTables_\*\*001.tsf, PerformanceCountersTables_\*\*002. tsf enz.) wordt automatisch verwerkt.

### <a name="more-about-trace-logs-missing"></a>Meer informatie over traceerlogboeken ontbreekt

**Opmerking:** dit geldt vooral toocloud services alleen tenzij u Hallo DiagnosticsMonitorTraceListener op een toepassing die wordt uitgevoerd op uw IaaS VM hebt geconfigureerd. 

- Zorg ervoor dat Hallo die diagnosticmonitortracelistener is geconfigureerd in Hallo web.config of app.config.  Dit is standaard in cloudserviceprojecten geconfigureerd, maar sommige klanten een reactie op het out waardoor Hallo trace-instructies toonot via diagnostische gegevens worden verzameld. 
- Als Logboeken niet ophalen van van Hallo OnStart of voer methode geschreven zorgt u ervoor Hallo die diagnosticmonitortracelistener bevindt zich in Hallo app.config.  Standaard is dit in het bestand web.config hello, maar die alleen van toepassing toocode uitgevoerd binnen w3wp.exe; zodat u deze in app.config toocapture traceringen uitgevoerd in de WaIISHost.exe nodig.
- Zorg ervoor dat u in plaats van Diagnostics.Debug.WriteXXX Diagnostics.Trace.TraceXXX gebruikt.  Hallo foutopsporingsinstructies wordt verwijderd uit een Release-build.
- Zorg ervoor dat Hallo gecompileerde code daadwerkelijk Hallo Diagnostics.Trace regels (Routereflector, ildasm of ILSpy tooverify gebruiken).  Diagnostics.Trace opdrachten zijn verwijderd van de binaire gegevens Hallo gecompileerd, tenzij u Hallo TRACE voorwaardelijke compilatie symbool.  Als msbuild toobuild Hallo project is dit een algemene probleem toorun in.

## <a name="known-issues-and-mitigations"></a>Bekende problemen en oplossingen
Hier volgt een lijst met bekende problemen met bekende oplossingen:

**1. .NET 4.5-afhankelijkheid:**

AF heeft een runtime-afhankelijkheid op framework .NET 4.5 of hoger. Op moment van schrijven van dit Hallo alle machines die zijn ingericht voor cloud-services, evenals alle officiële azure virtuele Machine basisinstallatiekopieën .NET 4.5 of hoger geïnstalleerd. Het is echter nog steeds mogelijk tooland in een situatie waarin u probeert toorun af op een computer die geen .NET 4.5 of hoger. Dit gebeurt wanneer u de computer afmeldt bij een oude afbeelding of momentopname; maken of uw eigen aangepaste schijf zetten.

Dit in het algemeen als een afsluitcode manifesten **255** bij het uitvoeren van DiagnosticsPluginLauncher.exe. Fout gebeurt vanwege toohello niet-verwerkte uitzondering: 
```
System.IO.FileLoadException: Could not load file or assembly 'System.Threading.Tasks, Version=1.5.11.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a' or one of its dependencies
```

**Risicobeperking:** .NET 4.5 of hoger op uw computer installeren.

**2. Prestatiemeteritems prestatiegegevens beschikbaar in de opslag, maar niet worden weergegeven in de portal**

Portal-ervaring van virtuele machines worden bepaalde prestatiemeteritems standaard weergegeven. Als u deze niet ziet, en u Hallo-gegevens ophalen van gegenereerd weet omdat beschikbaar in de opslag is. Controleren:
- Als de namen van prestatiemeteritems Hallo-gegevens in de opslag heeft in het Engels. Als Hallo itemnamen niet in het Engels, portal metrische grafiek toorecognize kunnen niet worden deze.
- Als u jokertekens (\*) in de namen van prestatiemeteritems, Hallo portal niet meer worden kunnen toocorrelate Hallo geconfigureerd en prestatiemeteritems worden verzameld.

**Risicobeperking**: van Hallo machine taal tooEnglish voor systeemaccounts wijzigen. Configuratiescherm -> regio -> Beheersjablonen -> Instellingen -> Schakel het selectievakje 'Welkom en systeemaccounts' zodat Hallo aangepaste taal geen is account toosystem toegepast. Controleer ook of dat u geen jokertekens gebruiken als u wilt dat portal toobe uw ervaring primaire verbruik.
