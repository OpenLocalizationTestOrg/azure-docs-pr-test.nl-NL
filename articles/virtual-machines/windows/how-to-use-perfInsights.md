---
title: aaaHow toouse PerfInsights in Microsoft Azure | Microsoft Docs
description: Leert hoe toouse PerfInsights tootroubleshoot Windows VM-prestatieproblemen.
services: virtual-machines-windows'
documentationcenter: 
author: genlin
manager: cshepard
editor: na
tags: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: genli
ms.openlocfilehash: f23ff7708c0c63bd02674b1bdc07753e8a89d9be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-perfinsights"></a>Hoe toouse PerfInsights 

[PerfInsights](http://aka.ms/perfinsightsdownload) is een geautomatiseerd script die handig diagnostische gegevens verzamelt, i/o-intensieve belastingen wordt uitgevoerd en biedt een rapport analyse toohelp oplossen van prestatieproblemen met virtuele machine van Windows in Microsoft Azure. 

Het is raadzaam dat u dit script uitvoert voordat u een ondersteuningsticket met Microsoft om de prestaties van de virtuele machine opent.

## <a name="supported-troubleshooting-scenarios"></a>Ondersteunde scenario's voor het oplossen van problemen

PerfInsights kunt verzamelen en analyseren van verschillende soorten gegevens die zijn gegroepeerd in unieke scenario's.

### <a name="collect-disk-configuration"></a>De schijfconfiguratie verzamelen 

Dit scenario worden verzameld Hallo schijfconfiguratie en andere belangrijke informatie, met inbegrip van Hallo volgende items:

-   Gebeurtenislogboeken

-   De status van het netwerk voor alle binnenkomende en uitgaande verbindingen

-   Netwerk- en firewallinstellingen configuratie-instellingen

-   Lijst met taken voor alle toepassingen die momenteel worden uitgevoerd op Hallo-systeem

-   Informatiebestand gemaakt door msinfo32 voor Hallo virtuele machine (VM)

-   Microsoft SQL Server-database configuratie-instellingen (als Hallo VM wordt geïdentificeerd als een server waarop SQL Server)

-   Opslag betrouwbaarheid prestatiemeteritems

-   Belangrijke hotfixes voor Windows

-   Geïnstalleerde filterstuurprogramma 's

Dit is een passief verzamelen van informatie die mag niet van invloed zijn op Hallo-systeem. 

>[!Note]
>Dit scenario wordt automatisch opgenomen in elk van de volgende scenario's Hallo.

### <a name="benchmarkstorage-performance-test"></a>De prestatietest benchmark/opslag

Dit scenario wordt uitgevoerd Hallo [diskspd](https://github.com/Microsoft/diskspd) benchmark test (IOPS en MBPS) voor alle stations die zijn gekoppeld toohello VM. 

> [!Note]
> Dit scenario kan invloed hebben op Hallo systeem en mag niet worden uitgevoerd op een live productiesysteem. Voer indien nodig in dit scenario in een speciale onderhoudsmodus venster tooavoid problemen. Een grotere werkbelasting die wordt veroorzaakt door een tracering of benchmark-test, kan een nadelige invloed heeft op de prestaties van uw VM Hallo.
>

### <a name="general-vm-slow-analysis"></a>Algemene VM langzaam analyse 

Dit scenario wordt uitgevoerd een [prestatiemeteritem](https://msdn.microsoft.com/library/windows/desktop/aa373083(v=vs.85).aspx) traceren met behulp van Hallo-items die zijn opgegeven in Hallo Generalcounters.txt bestand. Als hello VM wordt geïdentificeerd als een server waarop SQL Server wordt uitgevoerd, wordt een teller prestatietracering uitgevoerd met behulp van Hallo tellers die worden in Hallo Sqlcounters.txt bestand gevonden. Dit omvat ook prestaties Diagnostics-gegevens.

### <a name="vm-slow-analysis-and-benchmark"></a>Trage VM analyse en benchmark

Dit scenario wordt uitgevoerd een [prestatiemeteritem](https://msdn.microsoft.com/library/windows/desktop/aa373083(v=vs.85).aspx) trace die wordt gevolgd door een [diskspd](https://github.com/Microsoft/diskspd) benchmarktest. 

> [!Note]
> Dit scenario kan invloed hebben op Hallo systeem en mag niet worden uitgevoerd op een live productiesysteem. Voer indien nodig in dit scenario in een speciale onderhoudsmodus venster tooavoid problemen. Een grotere werkbelasting die wordt veroorzaakt door een tracering of benchmark-test, kan een nadelige invloed heeft op de prestaties van uw VM Hallo.
>

### <a name="azure-files-analysis"></a>Azure bestanden analyse 

Dit scenario voert een speciale prestaties teller vastleggen samen met een netwerktracering maken. Het vastleggen bevat alle Hallo 'SMB-Client Shares' items. Hallo Hieronder volgen enkele belangrijke SMB-share clientprestatietellers die deel van Hallo vastleggen uitmaken:

| **Type**     | **SMB-client shares teller** |
|--------------|-------------------------------|
| IOPS         | Gegevens aanvragen per seconde             |
|              | Aanvragen per seconde gelezen             |
|              | Schrijven van aanvragen per seconde            |
| Latentie      | Gem. per seconde/gegevensaanvraag         |
|              | Gemiddelde leestijd                 |
|              | Gemiddelde schrijftijd                |
| I/o-grootte      | Gem. Bytes/gegevensaanvraag       |
|              | Gem. Aantal gelezen bytes               |
|              | Gem. Geschreven bytes              |
| Doorvoer   | Gegevens Bytes per seconde                |
|              | Gelezen Bytes per seconde                |
|              | Geschreven Bytes per seconde               |
| Wachtrijlengte | Gem. Wachtrijlengte voor lezen        |
|              | Gem. Wachtrijlengte voor schrijven       |
|              | Gem. Wachtrijlengte van gegevens        |

### <a name="custom-configuration"></a>Aangepaste configuratie 

Wanneer u een aangepaste configuratie hebt uitgevoerd, uitvoert u alle traces (prestatiecontrole, prestatiemeteritems, xperf, netwerk, storport) parallel, afhankelijk van hoeveel andere traceringen zijn geselecteerd. Nadat de tracering is voltooid, wordt in het hulpprogramma Hallo Hallo diskspd benchmark, wordt uitgevoerd als deze optie is geselecteerd. 

> [!Note]
> Dit scenario kan invloed hebben op Hallo systeem en mag niet worden uitgevoerd op een live productiesysteem. Voer indien nodig in dit scenario in een speciale onderhoudsmodus venster tooavoid problemen. Een grotere werkbelasting die wordt veroorzaakt door een tracering of benchmark-test, kan een nadelige invloed heeft op de prestaties van uw VM Hallo.
>

## <a name="what-kind-of-information-is-collected-by-hello-script"></a>Wat voor soort informatie wordt verzameld door Hallo script?

Informatie over de virtuele machine van Windows, schijven of storage pools configuratie, prestatiemeteritems, logboeken en verschillende traceringen worden verzameld, afhankelijk van Hallo prestaties scenario gebruikt:

|Gegevens die worden verzameld                              |  |  | Scenario's voor prestaties |  |  | |
|----------------------------------|----------------------------|------------------------------------|--------------------------|--------------------------------|----------------------|----------------------|
|                              | Schijfconfiguratie verzamelen | Testen van de prestaties van de benchmark/opslag | Algemene VM langzaam analyse | Trage VM analyse en benchmark | Azure bestanden analyse | Aangepaste configuratie |
| Gegevens van gebeurtenislogboeken      | Ja                        | Ja                                | Ja                      | Ja                            | Ja                  | Ja                  |
| Informatie over het bestandssysteem               | Ja                        | Ja                                | Ja                      | Ja                            | Ja                  | Ja                  |
| Volume-kaart                       | Ja                        | Ja                                | Ja                      | Ja                            | Ja                  | Ja                  |
| Schijf-kaart                         | Ja                        | Ja                                | Ja                      | Ja                            | Ja                  | Ja                  |
| Actieve taken                    | Ja                        | Ja                                | Ja                      | Ja                            | Ja                  | Ja                  |
| Opslag betrouwbaarheid prestatiemeteritems     | Ja                        | Ja                                | Ja                      | Ja                            | Ja                  | Ja                  |
| Storage-gegevens              | Ja                        | Ja                                | Ja                      | Ja                            | Ja                  | Ja                  |
| Fsutil uitvoer                    | Ja                        | Ja                                | Ja                      | Ja                            | Ja                  | Ja                  |
| Filterinformatie stuurprogramma               | Ja                        | Ja                                | Ja                      | Ja                            | Ja                  | Ja                  |
| Netstat-uitvoer                   | Ja                        | Ja                                | Ja                      | Ja                            | Ja                  | Ja                  |
| Netwerkconfiguratie            | Ja                        | Ja                                | Ja                      | Ja                            | Ja                  | Ja                  |
| Firewall-configuratie           | Ja                        | Ja                                | Ja                      | Ja                            | Ja                  | Ja                  |
| Configuratie van SQL Server         | Ja                        | Ja                                | Ja                      | Ja                            | Ja                  | Ja                  |
| Prestaties diagnostische traceringen * |                            |                                    | Ja                      |                                |                      | Ja                  |
| Prestatiemeteritem Trace **     |                            |                                    |                          |                                |                      | Ja                  |
| SMB-prestatiemeteritems Trace **             |                            |                                    |                          |                                | Ja                  |                      |
| Teller voor SQL Server Trace **      |                            |                                    |                          |                                |                      | Ja                  |
| XPerf tracering                      |                            |                                    |                          |                                |                      | Ja                  |
| StorPort-tracering                   |                            |                                    |                          |                                |                      | Ja                  |
| Netwerktracering                    |                            |                                    |                          |                                | Ja                  | Ja                  |
| Diskspd Benchmark trace ***      |                            | Ja                                |                          | Ja                            |                      |                      |
|       |                            |                         |                                                   |                      |                      |

### <a name="performance-diagnostics-trace-"></a>Diagnostische traceerlogboeken voor prestaties (*)

Een op regels gebaseerde engine op Hallo toocollect ACHTERGRONDGEGEVENS wordt uitgevoerd en er prestatieproblemen. Hallo volgens de regels worden momenteel ondersteund:

- HighCpuUsage regel: hoog CPU-gebruik perioden detecteert en Hallo hoogste CPU-gebruik consumenten tijdens deze perioden weergegeven.
- HighDiskUsage regel: hoge schijf gebruik punten op fysieke schijven detecteert en toont Hallo bovenste schijf gebruik consumenten tijdens deze perioden.
- HighResolutionDiskMetric regel: toont IOPS, doorvoer en latentie metrische gegevens over i/o per 50 milliseconden voor elke fysieke schijf. Zo kunt u tooquickly schijf beperking perioden identificeren.
- HighMemoryUsage regel: veel geheugen gebruik perioden detecteert en toont Hallo bovenste geheugen gebruik consumenten tijdens deze perioden.

> [!NOTE] 
> Windows-versies die Hallo .NET Framework 3.5 zijn of hoger worden momenteel ondersteund.

### <a name="performance-counter-trace-"></a>Teller prestatietracering (*)

Verzamelt Hallo prestatiemeteritems te volgen:

- \Process, \Processor, \Memory, \Thread, \PhysicalDisk, \LogicalDisk
- \Cache\Dirty pagina's, \Cache\Lazy schrijfbewerkingen per seconde, \Server\Pool wisselbaar, fouten, fouten \Server\Pool wisselbaar geheugen:
- Geselecteerde items onder \Network Interface, \IPv4\Datagrams, \IPv6\Datagrams, \TCPv4\Segments, \TCPv6\Segments, \Network Adapter, \WFPv4\Packets, \WFPv6\Packets, \UDPv4\Datagrams, \UDPv6\Datagrams, \TCPv4\Connection, \TCPv6\Connection, \ QoS-Policy\Packets, \Per Network Interface Card processoractiviteit, \Microsoft Winsock BSP-netwerk

#### <a name="for-sql-server-instances"></a>Voor SQL Server-exemplaren
- Server: bufferbeheer van \sql, \SQLServer:Resource Pool statistieken, \SQLServer:SQL Statistics\
- \SQLServer:locks, \SQLServer:General, statistieken
- \SQLServer:Access methoden

#### <a name="for-azure-files"></a>Voor Azure-bestanden
\SMB Clientshares

### <a name="diskspd-benchmark-trace-"></a>Diskspd Benchmark-tracering (*)
Diskspd IO werkbelasting tests [Besturingssysteemschijf (schrijven) en groep-schijven (lezen/schrijven)]

## <a name="run-hello-perfinsights-on-your-vm"></a>Hallo PerfInsights uitvoeren op de virtuele machine

### <a name="what-do-i-have-tooknow-before-i-run-hello-script"></a>Wat heb ik tooknow voordat ik Hallo-script uitvoeren? 

**Scriptvereisten**

1.  Dit script moet worden uitgevoerd op virtuele machine die het prestatieprobleem Hallo is Hallo. 

2.  Hallo volgende besturingssystemen worden ondersteund: Windows Server 2008 R2, 2012, 2012 R2, 2016; Windows 8.1 en Windows 10.

**Mogelijke problemen wanneer u Hallo script voor productie-virtuele machines uitvoert:**

1.  Hallo script mogelijk nadelig beïnvloeden Hallo Hallo VM als deze wordt gebruikt samen met de Hallo 'Benchmark' of 'Aangepaste'-scenario dat is geconfigureerd met behulp van XPerf of DiskSpd. Wees voorzichtig wanneer u Hallo-script in een productieomgeving uitvoeren.

2.  Wanneer u Hallo script samen met de Hallo 'Benchmark' of 'Aangepaste'-scenario dat wordt geconfigureerd met behulp van DiskSpd gebruiken, moet u dat er geen andere activiteit op de achtergrond Hallo i/o-werkbelasting op Hallo getest schijven verstoort.

3.  Hallo-script gebruikt standaard Hallo tijdelijke opslag station toocollect gegevens. Als u tracering blijft ingeschakeld gedurende een langere periode, kan Hallo hoeveelheid gegevens die worden verzameld relevant zijn. Hierdoor kunnen Hallo beschikbaarheid van de ruimte op de tijdelijke schijf hello, daarom die invloed hebben op alle toepassingen die afhankelijk van dit station is.

### <a name="how-do-i-run-perfinsights"></a>Hoe kan ik PerfInsights uitvoeren? 

toorun Hallo script, als volgt te werk:

1. Download [PerfInsights.zip](http://aka.ms/perfinsightsdownload).

2. Hallo PerfInsights.zip bestand deblokkeren. toodo dit met de rechtermuisknop op Hallo PerfInsights.zip bestand, selecteer **eigenschappen**. In Hallo **algemene** tabblad **blokkering** en selecteer vervolgens **OK**. Hiermee zorgt u ervoor dat het Hallo-script wordt uitgevoerd zonder extra beveiliging wordt gevraagd.  

    ![Hallo zip-bestand te ontgrendelen](media/how-to-use-perfInsights/unlock-file.png)

3.  Hallo gecomprimeerd PerfInsights.zip bestand uitbreiden naar de tijdelijke schijf (standaard is dit doorgaans Hallo D-station). Hallo gecomprimeerd bestand moet bevatten de volgende Hallo bestanden en mappen:

    ![bestanden in Hallo gecomprimeerde map](media/how-to-use-perfInsights/file-folder.png)

4.  Open Windows PowerShell als beheerder en vervolgens Hallo PerfInsights.ps1 script uitvoeren.

    ```
    cd <hello path of PerfInsights folder >
    Powershell.exe -ExecutionPolicy UnRestricted -NoProfile -File .\\PerfInsights.ps1
    ```

    Moet u wellicht tooenter 'y' tooif u worden gevraagd tooconfirm dat u wilt dat toochange Hallo uitvoeringsbeleid.

    Hallo Disclaimer in het dialoogvenster krijgt u Hallo optie tooshare diagnostische gegevens met Microsoft Support. U moet ook toohello license agreement toocontinue toestemming te geven. Selecteer de gewenste opties en klik vervolgens op **-Script uitvoeren**.

    ![Disclaimer vak](media/how-to-use-perfInsights/disclaimer.png)

5.  Indienen aanvraagnummer hello, als deze beschikbaar is wanneer u Hallo-script (dit is voor onze statistieken) uitvoert. Klik vervolgens op **OK**.
    
    ![ondersteunings-ID invoeren](media/how-to-use-perfInsights/enter-support-number.png)

6.  Selecteer het station voor tijdelijke opslag. Hallo Script kunt automatische detectie stationsletter op Hallo van Hallo-station. Als er problemen in deze fase optreden, bent u mogelijk gevraagd tooselect Hallo station (Hallo standaardstation is D). Hier gegenereerde logboeken worden opgeslagen in logboek Hallo\_verzamelingsmap. Nadat u invoert of Hallo stationsletter accepteren, klikt u op **OK**.

    ![Geef station](media/how-to-use-perfInsights/enter-drive.png)

7.  Selecteer een scenario voor het oplossen van problemen in Hallo opgegeven lijst met items.

       ![Scenario's selecteren](media/how-to-use-perfInsights/select-scenarios.png)

8.  U kunt ook PerfInsights zonder gebruikersinterface uitvoeren.

    Hallo volgende opdracht wordt uitgevoerd Hallo 'Algemene VM langzaam analysis' scenario zonder een prompt UI probleemoplossing of vastleggen van gegevens gedurende 30 seconden. Wordt u gevraagd tooconsent toohello dezelfde afwijzing en overeenkomst die worden vermeld in stap 4.

        powershell.exe -ExecutionPolicy UnRestricted -NoProfile -Command ".\\PerfInsights.ps1 -NoGui -Scenario vmslow -TracingDuration 30"

    Als u PerfInsights toorun in stille modus wilt, gebruikt de **- AcceptDisclaimerAndShareDiagnostics** parameter. Gebruik bijvoorbeeld Hallo volgende opdracht:

        powershell.exe -ExecutionPolicy UnRestricted -NoProfile -Command ".\\PerfInsights.ps1 -NoGui -Scenario vmslow -TracingDuration 30 -AcceptDisclaimerAndShareDiagnostics"

### <a name="how-do-i-troubleshoot-issues-while-running-hello-script"></a>Hoe kan ik problemen oplossen tijdens het Hallo-script uitvoeren?

Als het Hallo-script is beëindigd, kunt u opruimen een inconsistente status heeft met een script samen met Hallo Hallo - switch, opruimen, als volgt:

    powershell.exe -ExecutionPolicy UnRestricted -NoProfile -Command ".\\PerfInsights.ps1 -Cleanup"

Als er problemen tijdens de automatische detectie van tijdelijke station Hallo Hallo optreden, bent u mogelijk gevraagd tooselect Hallo station (Hallo standaardstation is D).

![Voer station](media/how-to-use-perfInsights/enter-drive.png)

Hallo-script wordt verwijderd Hallo hulpprogramma's en verwijdert u tijdelijke mappen.

### <a name="troubleshooting-other-script-issues"></a>Andere problemen met het script 

Als er problemen optreden wanneer u Hallo script uitvoert, drukt u op Ctrl + C toointerrupt Hallo script worden uitgevoerd. tooremove tijdelijke objecten, raadpleegt u 'Opschonen na niet normaal beëindigd' Hallo-sectie.

Als u tooexperience fout zelfs na verschillende pogingen doorgaat, raden wij aan Hallo script in 'foutopsporingsmodus' uit te voeren met behulp van Hallo '-fouten opsporen in ' parameteroptie bij het opstarten.

Nadat het Hallo-fout treedt op als kopie Hallo volledige uitvoer van Hallo PowerShell-console, en verzend het toohello Microsoft Support-agent die is die u helpt toohelp Hallo probleem kan oplossen.

### <a name="how-do-i-run-hello-script-in-custom-configuration-mode"></a>Hoe voer ik Hallo script in de modus voor aangepaste configuratie

Door het selecteren van Hallo **aangepaste** configuratie, kunt u verschillende traceringen parallel (Gebruik Shift toomulti selecteren) inschakelen:

![scenario's selecteren](media/how-to-use-perfInsights/select-scenario.png)

Wanneer u prestatiecontrole Hallo selecteert, teller prestatietracering, XPerf Trace, netwerktracering of Storport Trace-scenario's, Hallo-instructies in de dialoogvensters Hallo en probeer tooreproduce Hallo trage prestatieprobleem nadat u Hallo traceringen hebt gestart.

Hallo volgen in het dialoogvenster kunt u een tracering starten:

![Tracering starten](media/how-to-use-perfInsights/start-trace-message.png)

toostop hello traceringen, hebt u tooconfirm Hallo opdracht in een tweede dialoogvenster.

![tracering stoppen](media/how-to-use-perfInsights/stop-trace-message.png)
![tracering stoppen](media/how-to-use-perfInsights/ok-trace-message.png)

Wanneer traceringen Hallo of bewerkingen zijn voltooid, wordt een nieuw bestand gegenereerd in D:\\logboek\_verzameling (of Hallo tijdelijke station) met de naam **CollectedData\_jjjj-MM-dd\_hh\_mm \_ss.zip.** U kunt deze agent bestand toohello ondersteuning voor analyse verzenden.

## <a name="review-hello-diagnostics-report-created-by-perfinsights"></a>Hallo diagnostisch rapport gemaakt door PerfInsights controleren

Binnen Hallo **CollectedData\_jjjj-MM-dd\_hh\_mm\_ss.zip bestand** die is gegenereerd door PerfInsights, vindt u een HTML-rapport waarin wordt uitgelegd Hallo bevindingen van PerfInsights. tooreview Hallo rapport uit, vouw Hallo **CollectedData\_jjjj-MM-dd\_hh\_mm\_ss.zip** bestand en open vervolgens Hallo **PerfInsights Report.html**bestand.

Selecteer Hallo **bevindingen** tabblad.

![tabblad Zoeken](media/how-to-use-perfInsights/findingtab.png)

**Opmerkingen bij de**

-   Berichten in rood bekend configuratieproblemen die prestatieproblemen kunnen veroorzaken.

-   Geel zijn waarschuwingen voor niet-optimale configuraties die niet noodzakelijkerwijs prestatieproblemen veroorzaken.

-   Berichten in blauw zijn alleen informatief instructies.

Bekijk Hallo HTTP-koppelingen voor alle foutberichten in rood tooget meer gedetailleerde informatie over de bevindingen Hallo en hoe deze Hallo prestatie- of aanbevolen procedures voor optimale prestaties van configuraties kunnen beïnvloeden.

### <a name="disk-configuration-tab"></a>Tabblad voor schijf-configuratie

Hallo **overzicht** sectie vindt u verschillende weergaven van de opslagconfiguratie hello, inclusief de gegevens van Diskpart en opslagruimten

Hallo **DiskMap** en **VolumeMap** secties wordt beschreven in een dubbele perspectief logische volumes en fysieke schijven zijn andere gerelateerde tooeach.

In het perspectief van de fysieke schijf (DiskMap) hello ziet Hallo tabel u alle logische volumes die worden uitgevoerd op Hallo schijf. In de Hallo voorbeeld te volgen, voert PhysicalDrive2 2 logische Volumes die zijn gemaakt op meerdere partities (J en H):

![tabblad gegevens](media/how-to-use-perfInsights/disktab.png)

In Hallo Volume perspectief (*VolumeMap*), Hallo tabellen tonen alle fysieke schijven van de Hallo onder elke logische volume. U ziet dat een logisch volume van meerdere fysieke schijven voor RAID/dynamische schijven wordt mogelijk uitgevoerd. In het voorbeeld te volgen Hallo *C:\\koppelen* is van een koppelpunt geconfigureerd als *SpannedDisk* op PhysicalDisks \#2 en \#3:

![tabblad volume](media/how-to-use-perfInsights/volumetab.png)

### <a name="sql-server-tab"></a>SQL Server-tabblad

Als doel Hallo VM als host fungeert voor alle exemplaren van SQL Server, ziet u een extra tabblad in Hallo-rapport met de naam **SQL Server**:

![SQL-tabblad](media/how-to-use-perfInsights/sqltab.png)

Deze sectie bevat een 'overzicht' en aanvullende sub tabbladen voor elk Hallo SQL Server-exemplaren die worden gehost op Hallo VM.

Hallo sectie 'Overzicht' bevat een handig tabel overzicht van alle Hallo fysieke schijven (systeem- en gegevensschijven) die worden uitgevoerd en die een mengeling van gegevensbestanden en transactielogboekbestanden bevatten.

In Hallo bijvoorbeeld na *PhysicalDrive0* (uitgevoerd Hallo C-station) wordt weergegeven, omdat beide Hallo *modeldev* en *modellog* bestanden bevinden zich op station C hello, en ze zijn van verschillende typen (zoals het gegevensbestand en het transactielogboek, respectievelijk):

![LogInfo](media/how-to-use-perfInsights/loginfo.png)

Hallo SQL Server-exemplaar-specifieke tabbladen bevatten een algemene sectie waarin algemene informatie over het geselecteerde exemplaar Hallo en extra secties voor gedetailleerde informatie, waaronder instellingen, configuraties en opties voor gebruikers.

## <a name="references-toohello-external-tools-used"></a>Verwijst naar toohello externe hulpprogramma's gebruikt

### <a name="diskspd"></a>Diskspd

DISKSPD is een opslag laden en prestaties van de generator test hulpprogramma uit Hallo Windows- en Windows Server- en Cloud-serverinfrastructuur engineering-teams. Zie voor meer informatie [Diskspd](https://github.com/Microsoft/diskspd).

### <a name="xperf"></a>XPerf

XPerf is een opdrachtregelprogramma toocapture traceringen van Hallo Windows Performance Tools Kit.

Zie voor meer informatie [Windows prestaties Toolkit – Xperf](https://blogs.msdn.microsoft.com/ntdebugging/2008/04/03/windows-performance-toolkit-xperf/).

## <a name="next-steps"></a>Volgende stappen

### <a name="upload-diagnostics-logs-and-reports-toomicrosoft-support-for-further-review"></a>Uploaden van diagnostische logboeken en rapporten tooMicrosoft ondersteuning om verder te bestuderen

Wanneer u met Hallo Microsoft Support-personeel werkt, hebt u mogelijk aangevraagde tootransmit Hallo uitvoer die wordt gegenereerd door PerfInsights tooassist Hallo procedure voor probleemoplossing.

Hallo ondersteuning agent een werkruimte DTM voor u maakt en u ontvangt een e-mailbericht met een koppeling toohello [DTM portal (https://filetransfer.support.microsoft.com/EFTClient/Account/Login.htm) en een unieke gebruikersnaam en wachtwoord.

Dit bericht wordt verzonden via **CTS Automated Diagnostics Services** (ctsadiag@microsoft.com).

![Voorbeeld van het Hallo-bericht](media/how-to-use-perfInsights/supportemail.png)

Voor extra beveiliging kunt u zich vereist toochange uw wachtwoord op voor het eerst gebruiken.

Nadat u zich aanmeldt tooDTM, vindt u een dialoogvenster vak tooupload hello **CollectedData\_jjjj-MM-dd\_hh\_mm\_ss.zip** -bestand dat is verzameld door PerfInsights.
