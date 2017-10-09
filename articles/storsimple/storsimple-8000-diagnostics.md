---
title: aaaDiagnostics hulpprogramma tootroubleshoot StorSimple 8000 apparaat | Microsoft Docs
description: Beschrijving van de modi van Hallo StorSimple-apparaat en wordt uitgelegd hoe toouse Windows PowerShell voor StorSimple toochange Hallo apparaatmodus.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2017
ms.author: alkohli
ms.openlocfilehash: e8b7fdbc44d2533973b63da841335ba73ba0014b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-diagnostics-tool-tootroubleshoot-8000-series-device-issues"></a>Hallo StorSimple diagnostische hulpprogramma tootroubleshoot 8000 series problemen apparaten gebruiken

## <a name="overview"></a>Overzicht

Hallo StorSimple diagnostische hulpprogramma diagnoses gerelateerde toosystem problemen, prestaties, netwerk en status van de hardware-onderdeel voor een StorSimple-apparaat. Hallo diagnostische hulpprogramma kan worden gebruikt in verschillende scenario's. Deze scenario's omvatten werkbelasting planning, implementatie van een StorSimple-apparaat, beoordeling van de netwerkomgeving Hallo en Hallo prestaties van een operationeel apparaat bepalen. In dit artikel biedt een overzicht van diagnostische Hallo en beschrijft hoe Hallo-hulpprogramma kan worden gebruikt met een StorSimple-apparaat.

Hallo diagnostische hulpprogramma is voornamelijk bedoeld voor StorSimple 8000 series on-premises apparaten (8100 en 8600).

## <a name="run-diagnostics-tool"></a>Diagnostische hulpprogramma uitvoeren

Dit hulpprogramma kan worden uitgevoerd via Windows PowerShell-interface Hallo van uw StorSimple-apparaat. Er zijn twee manieren tooaccess Hallo lokale interface van uw apparaat:

* [Gebruik PuTTY tooconnect toohello de seriële console apparaat](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).
* [Externe toegang tot Hallo-hulpprogramma via Hallo Windows PowerShell voor StorSimple](storsimple-remote-connect.md).

In dit artikel gaan we ervan uit dat u de seriële console van toohello apparaat via de PuTTY hebt verbonden.

#### <a name="toorun-hello-diagnostics-tool"></a>toorun hello diagnostische hulpprogramma

Wanneer u toohello Windows PowerShell-interface van Hallo-apparaat hebt gekoppeld, worden uitgevoerd Hallo stappen toorun Hallo cmdlet te volgen.
1. Meld u bij de seriële console van toohello apparaat Hallo stappen in [PuTTY gebruiken tooconnect toohello de seriële console apparaat](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).

2. Type Hallo volgende opdracht:

    `Invoke-HcsDiagnostics`

    Als de bereikparameter Hallo niet is opgegeven, voert Hallo cmdlet alle Hallo diagnostische tests. Deze tests omvatten system, status voor hardware-onderdeel, netwerk en prestaties. 
    
    alleen een specifieke test toorun Hallo scope-parameter opgeven. Bijvoorbeeld: toorun alleen Hallo Netwerktest, type

    `Invoke-HcsDiagnostics -Scope Network`

3. Selecteer en kopieer Hallo uitvoer van Hallo PuTTY venster in een tekstbestand voor verdere analyse.

## <a name="scenarios-toouse-hello-diagnostics-tool"></a>Scenario's toouse Hallo diagnostische hulpprogramma

Hallo diagnostische hulpprogramma tootroubleshoot Hallo netwerk, prestaties, systeem en hardware status van Hallo system gebruiken. Hier volgen enkele mogelijke scenario's:

* **Apparaat offline** -uw StorSimple 8000 series apparaat offline is. Echter van Windows PowerShell-interface hello, het lijkt erop dat beide domeincontrollers Hallo actief zijn.
    * U kunt dit hulpprogramma toothen Hallo netwerk status bepalen.
         
         > [!NOTE]
         > Gebruik dit hulpprogramma tooassess prestatie- en netwerkinstellingen niet op een apparaat voordat het Hallo-registratie (of configureren via de wizard setup). Een geldig IP-adres wordt toohello apparaat tijdens de wizard setup en de registratie toegewezen. U kunt deze cmdlet uitvoeren op een apparaat dat niet is geregistreerd voor de status van de hardware- en systeem. Gebruik bereikparameter hello, bijvoorbeeld:
         >
         > `Invoke-HcsDiagnostics -Scope Hardware`
         >
         > `Invoke-HcsDiagnostics -Scope System`

* **Problemen met de permanente apparaat** -apparaat problemen die toopersist lijken zich voordoen. Bijvoorbeeld, de registratie is mislukt. U kan ook worden ondervindt problemen met apparaat nadat het Hallo-apparaat is geregistreerd en operationele voor even wordt.
    * In dit geval moet u dit hulpprogramma gebruiken voor voorlopige probleemoplossing voordat u zich een serviceaanvraag met Microsoft Support aanmeldt. Het is raadzaam dat u deze hulpprogramma's en vastleggen Hallo-uitvoer van dit hulpprogramma uitvoert. Vervolgens kunt u bieden deze uitvoer tooSupport tooexpedite probleemoplossing.
    * Als er een onderdeel of het cluster hardwarefouten, moet u een ondersteuningsaanvraag aanmelden.

* **Lage Apparaatprestaties** -uw StorSimple-apparaat traag is.
    * In dit geval moet u deze cmdlet uitvoeren met de scope-parameter set tooperformance. Analyseer het Hallo-uitvoer. U krijgt Hallo cloud lezen-schrijven latenties. Gebruik Hallo gerapporteerd latenties maximale haalbare TARGET rekening te houden in enige overhead voor interne gegevensverwerking Hallo en vervolgens implementeren Hallo werkbelastingen op Hallo-systeem. Voor meer informatie gaat te[Hallo test tootroubleshoot apparaat netwerkprestaties gebruiken](#network-test).


## <a name="diagnostics-test-and-sample-outputs"></a>Diagnostische test en voorbeeld-uitvoer

### <a name="hardware-test"></a>Hardwaretest

Deze test bepaalt Hallo status van de hardwareonderdelen hello, Hallo USM firmware en Hallo schijf firmware die wordt uitgevoerd op uw systeem.

* Hallo hardwareonderdelen gerapporteerd mislukte Hallo test van deze onderdelen zijn of zijn niet aanwezig in het Hallo-systeem.
* Hallo USM firmware- en firmware-versies zijn gerapporteerd voor Hallo Controller 0, 1 van de domeincontroller, en gedeelde onderdelen in uw systeem. Voor een volledige lijst van hardware-onderdelen, gaat u naar:

    * [Primaire behuizing-onderdelen](storsimple-monitor-hardware-status.md#component-list-for-primary-enclosure-of-storsimple-device)
    * [EBOD behuizing-onderdelen](storsimple-monitor-hardware-status.md#component-list-for-ebod-enclosure-of-storsimple-device)

> [!NOTE]
> Als Hallo hardwaretest niet functionerende onderdelen, rapporteert [Meld u bij een serviceaanvraag met Microsoft Support](storsimple-contact-microsoft-support.md).

#### <a name="sample-output-of-hardware-test-run-on-an-8100-device"></a>Voorbeeld van uitvoer van de hardwaretest uitgevoerd op een 8100-apparaat

Hier volgt een voorbeeld van uitvoer van een StorSimple 8100-apparaat. Hallo EBOD behuizing is niet aanwezig in Hallo 8100 model-apparaat. Hallo EBOD controller onderdelen worden daarom niet gemeld.

```
Controller0>Invoke-HcsDiagnostics -Scope Hardware
Running hardware diagnostics ...
--------------------------------------------------
Hardware components failed or not present
----------------------

           Type           State      Controller           Index     EnclosureId
           ----           -----      ----------           -----     -----------
...rVipResource      NotPresent            None               1            None
...rVipResource      NotPresent            None               2            None
...rVipResource      NotPresent            None               3            None
...rVipResource      NotPresent            None               4            None
...rVipResource      NotPresent            None               5            None
...rVipResource      NotPresent            None               6            None
...rVipResource      NotPresent            None               7            None
...rVipResource      NotPresent            None               8            None
...rVipResource      NotPresent            None               9            None
...rVipResource      NotPresent            None              10            None
...rVipResource      NotPresent            None              11            None

Firmware information
----------------------
TalladegaController : ActiveBIOS:0.45.0010
                      BackupBIOS:0.45.0006
                      MainCPLD:17.0.000b
                      ActiveBMCRoot:2.0.001F
                      BackupBMCRoot:2.0.001F
                      BMCBoot:2.0.0002
                      LsiFirmware:20.00.04.00
                      LsiBios:07.37.00.00
                      Battery1Firmware:06.2C
                      Battery2Firmware:06.2C
                      DomFirmware:X231600
                      CanisterFirmware:3.5.0.56
                      CanisterBootloader:5.03
                      CanisterConfigCRC:0x9134777A
                      CanisterVPDStructure:0x06
                      CanisterGEMCPLD:0x19
                      CanisterVPDCRC:0x142F7DC2
                      MidplaneVPDStructure:0x0C
                      MidplaneVPDCRC:0xA6BD4F64
                      MidplaneCPLD:0x10
                      PCM1Firmware:1.00|1.05
                      PCM1VPDStructure:0x05
                      PCM1VPDCRC:0x41BEF99C
                      PCM2Firmware:1.00|1.05
                      PCM2VPDStructure:0x05
                      PCM2VPDCRC:0x41BEF99C

EbodController      :
DisksFirmware       : SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08

TalladegaController : ActiveBIOS:0.45.0010
                      BackupBIOS:0.45.0006
                      MainCPLD:17.0.000b
                      ActiveBMCRoot:2.0.001F
                      BackupBMCRoot:2.0.001F
                      BMCBoot:2.0.0002
                      LsiFirmware:20.00.04.00
                      LsiBios:07.37.00.00
                      Battery1Firmware:06.2C
                      Battery2Firmware:06.2C
                      DomFirmware:X231600
                      CanisterFirmware:3.5.0.56
                      CanisterBootloader:5.03
                      CanisterConfigCRC:0x9134777A
                      CanisterVPDStructure:0x06
                      CanisterGEMCPLD:0x19
                      CanisterVPDCRC:0x142F7DC2
                      MidplaneVPDStructure:0x0C
                      MidplaneVPDCRC:0xA6BD4F64
                      MidplaneCPLD:0x10
                      PCM1Firmware:1.00|1.05
                      PCM1VPDStructure:0x05
                      PCM1VPDCRC:0x41BEF99C
                      PCM2Firmware:1.00|1.05
                      PCM2VPDStructure:0x05
                      PCM2VPDCRC:0x41BEF99C

EbodController      :
DisksFirmware       : SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08

--------------------------------------------------
```

### <a name="system-test"></a>Systeem-test

Deze test rapporten systeemgegevens hello, Hallo updates die beschikbaar zijn, Hallo clustergegevens en Hallo service-informatie voor uw apparaat.

* Hallo systeemgegevens bevat Hallo model, apparaatserienummer tijdzone, status van de domeincontroller en gedetailleerde softwareversie Hallo Hallo systeem waarop. toounderstand hello verschillende parameters voor het gerapporteerd als Hallo-uitvoer te gaan[systeemgegevens interpreteren](#appendix-interpreting-system-information).

* beschikbaarheid van de Hallo rapporten of Hallo regular en onderhoud modi beschikbaar zijn en de namen van de bijbehorende pakket. Als `RegularUpdates` en `MaintenanceModeUpdates` zijn `false`, wordt hiermee Hallo updates zijn niet beschikbaar. Uw apparaat is bijgewerkt.
* Hallo clustergegevens bevat Hallo informatie over verschillende logische onderdelen van de Hallo HCS clustergroepen en hun respectieve statussen. Als u een offline clustergroep in deze sectie van het Hallo-rapport ziet [contact op met Microsoft Support](storsimple-contact-microsoft-support.md).
* Hallo service informatie omvat Hallo namen en status van alle Hallo HCS en CiS services die worden uitgevoerd op uw apparaat. Deze informatie is nuttig voor Hallo Microsoft Support op Hallo apparaat probleem op te lossen.

#### <a name="sample-output-of-system-test-run-on-an-8100-device"></a>Voorbeeld van uitvoer van systeem test uitgevoerd op een 8100-apparaat

Hier volgt een voorbeeld van uitvoer van Hallo system test uitgevoerd op een 8100-apparaat.

```
Controller0>Invoke-HcsDiagnostics -Scope System
Running system diagnostics ...
--------------------------------------------------

System information
----------------------
Controller0:

InstanceId              : 7382407f-a56b-4622-8f3f-756fe04cfd38
Name                    : 8100-SHX0991003G467K
Model                   : 8100
SerialNumber            : SHX0991003G467K
TimeZone                : (UTC-08:00) Pacific Time (US & Canada)
CurrentController       : Controller0
ActiveController        : Controller0
Controller0Status       : Normal
Controller1Status       : Normal
SystemMode              : Normal
FriendlySoftwareVersion : StorSimple 8000 Series Update 4.0
HcsSoftwareVersion      : 6.3.9600.17820
ApiVersion              : 9.0.0.0
VhdVersion              : 6.3.9600.17759
OSVersion               : 6.3.9600.0
CisAgentVersion         : 1.0.9441.0
MdsAgentVersion         : 35.2.2.0
Lsisas2Version          : 2.0.78.0
Capacity                : 219902325555200
RemoteManagementMode    : Disabled
FipsMode                : Enabled

Controller1:
InstanceId              : 7382407f-a56b-4622-8f3f-756fe04cfd38
Name                    : 8100-SHX0991003G467K
Model                   : 8100
SerialNumber            : SHX0991003G467K
TimeZone                :
CurrentController       : Controller0
ActiveController        : Controller0
Controller0Status       : Normal
Controller1Status       : Normal
SystemMode              : Normal
FriendlySoftwareVersion : StorSimple 8000 Series Update 4.0
HcsSoftwareVersion      : 6.3.9600.17820
ApiVersion              : 9.0.0.0
VhdVersion              : 6.3.9600.17759
OSVersion               : 6.3.9600.0
CisAgentVersion         : 1.0.9441.0
MdsAgentVersion         : 35.2.2.0
Lsisas2Version          : 2.0.78.0
Capacity                : 219902325555200
RemoteManagementMode    : HttpsAndHttpEnabled
FipsMode                : Enabled

Update availability
----------------------
RegularUpdates              : False
MaintenanceModeUpdates      : False
RegularUpdatesTitle         : {}
MaintenanceModeUpdatesTitle : {}

Cluster information
----------------------
Name                          State OwnerGroup
----                          ----- ----------
ApplicationHostRLUA           Online HCS Cluster Group
Data0v4                       Online HCS Cluster Group
HCS Vnic Resource             Online HCS Cluster Group
hcs_cloud_connectivity_...    Online HCS Cluster Group
hcs_controller_replacement    Online HCS Cluster Group
hcs_datapath_service          Online HCS Cluster Group
hcs_management_servic         Online HCS Cluster Group
hcs_nvram_service             Online HCS Cluster Group
hcs_passive_datapath          Online HCS Passive Cluster Group
hcs_platform_service          Online HCS Cluster Group
hcs_saas_agent_service        Online HCS Cluster Group
HddDataClusterDisk            Online HCS Cluster Group
HddMgmtClusterDisk            Online HCS Cluster Group
HddReplClusterDisk            Online HCS Cluster Group
iSCSI Target Server           Online HCS Cluster Group
NvramClusterDisk              Online HCS Cluster Group
SSAdminRLUA                   Online HCS Cluster Group
SsdDataClusterDisk            Online HCS Cluster Group
SsdNvramClusterDisk           Online HCS Cluster Group

Service information
----------------------
Name                                          Status DisplayName
----                                          ------ -----------
CiSAgentSvc                                   Stopped CiS Service Agent
hcs_cloud_connectivity_...                    Running hcs_cloud_connectivity...
hcs_controller_replacement                    Running HCS Controller Replace...
hcs_datapath_service                          Running HCS Datapath Service
hcs_management_service                        Running HCS Management Service
hcs_minishell                                 Running hcs_minishell
HCS_NVRAM_Service                             Running HCS NVRAM Service
hcs_passive_datapath                          Stopped HCS Passive Datapath S...
hcs_platform_service                          Running HCS Platform Monitor S...
hcs_saas_agent_service                        Running hcs_saas_agent_service
hcs_startup                                   Stopped hcs_startup
--------------------------------------------------
```

### <a name="network-test"></a>Netwerktest

Deze test valideert Hallo status van netwerkinterfaces hello, poorten, DNS- en NTP serververbindingen, SSL-certificaat, opslagaccountreferenties, connectiviteit toohello Update-servers en web proxy connectiviteit op uw StorSimple-apparaat.

#### <a name="sample-output-of-network-test-when-only-data0-is-enabled"></a>Voorbeeld van uitvoer van het netwerk testen wanneer alleen DATA0 is ingeschakeld

Hier volgt een voorbeeld van uitvoer van Hallo 8100-apparaat. U kunt zien in de uitvoer Hallo die:
* Alleen DATA 0 en 1 gegevens netwerkinterfaces zijn ingeschakeld en geconfigureerd.
* GEGEVENS-2-5 zijn niet ingeschakeld in Hallo-portal.
* configuratie van Hallo DNS-server is geldig en Hallo apparaat verbinding kan maken via Hallo DNS-server.
* Hallo NTP-serververbindingen is ook geen probleem.
* Poorten 80 en 443 zijn geopend. Poort 9354 is geblokkeerd. Op basis van Hallo [netwerk systeemvereisten](storsimple-system-requirements.md), moet u tooopen deze poort voor Hallo service bus-communicatie.
* Hallo SSL-certificaat is geldig.
* Hallo apparaat verbinding kan maken toohello storage-account: _myss8000storageacct_.
* Hallo connectiviteit tooUpdate servers is ongeldig.
* Hallo webproxy is niet geconfigureerd op dit apparaat.

#### <a name="sample-output-of-network-test-when-data0-and-data1-are-enabled"></a>Voorbeeld van uitvoer van Netwerktest wanneer DATA0 en bestand1 zijn ingeschakeld

```
Controller0>Invoke-HcsDiagnostics -Scope Network
Running network diagnostics ....
--------------------------------------------------
Validating networks .....
Name                Entity              Result              Details
----                ------              ------              -------
Network interface   Data0               Valid
Network interface   Data1               Valid
Network interface   Data2               Not enabled
Network interface   Data3               Not enabled
Network interface   Data4               Not enabled
Network interface   Data5               Not enabled
DNS                 10.222.118.154      Valid
NTP                 time.windows.com    Valid
Port                80                  Open
Port                443                 Open
Port                9354                Blocked
SSL certificate     https://myss8000... Valid
Storage account ... myss8000storageacct Valid
URL                 http://download.... Valid
URL                 http://download.... Valid
Web proxy                               Not enabled         Web proxy is not...
--------------------------------------------------
```

### <a name="performance-test"></a>Prestatietest

Deze test rapporten Hallo cloud prestaties via Hallo cloud lezen-schrijven latenties voor uw apparaat. Dit hulpprogramma kan worden gebruikt tooestablish een basislijn van prestaties van een Hallo cloud die u met StorSimple bereiken kunt. Hallo hulpprogramma rapporten Hallo maximale prestaties (beste scenario voor lezen-schrijven latenties) die u voor de verbinding ophalen kunt.

Als Hallo hulpprogramma Hallo maximale haalbare prestaties meldt, gebruiken we Hallo lezen-schrijven latenties als doelen bij het implementeren van Hallo werkbelastingen gerapporteerd.

Hallo test simuleert Hallo blob grootten Hallo ander volumetypen op Hallo apparaat gekoppeld. Gewone lagen en back-ups van lokaal vastgemaakte volumes met een blob-grootte van 64 KB. Gelaagde volumes met archief-optie ingeschakeld gebruiken blob-gegevensgrootte 512 KB. Als het apparaat heeft gelaagde en lokaal vastgemaakte volumes geconfigureerd, alleen Hallo test bijbehorende too64 KB blob gegevensgrootte wordt uitgevoerd.

toouse dit hulpprogramma uitvoeren Hallo stappen te volgen:

1.  Maak eerst een combinatie van gelaagde volumes en gelaagde volumes met gearchiveerde optie ingeschakeld. Deze actie zorgt ervoor dat hulpprogramma Hallo Hallo tests voor 64 KB en 512 KB grootten van de blob.

2. Hallo-cmdlet uitvoeren nadat u hebt gemaakt en geconfigureerd Hallo volumes. Type:

    `Invoke-HcsDiagnostics -Scope Performance`

3. Noteer Hallo lezen-schrijven latenties gemeld door het Hallo-hulpprogramma. Deze test kunt toorun van enkele minuten duren voordat Hallo resultaten gerapporteerd.

4. Als Hallo verbinding latenties zijn onder Hallo verwacht bereik en hello latenties gemeld door het Hallo-hulpprogramma kunnen worden gebruikt als maximale haalbare doel bij het implementeren van Hallo werkbelastingen. Rekening te houden in enige overhead voor interne gegevensverwerking.

    Als Hallo lezen-schrijven latenties gerapporteerd door Hallo diagnostische hulpprogramma hoog zijn:

    1. Storage Analytics voor blob-services configureren en analyseren van Hallo uitvoer toounderstand Hallo latenties voor hello Azure storage-account. Voor gedetailleerde instructies gaat te[inschakelen en configureren van opslag Analytics](../storage/common/storage-enable-and-view-metrics.md). Als deze latenties ook hoge en vergelijkbare toohello cijfers die u hebt ontvangen van Hallo StorSimple diagnostische hulpprogramma, moet u toolog een serviceaanvraag met Azure storage.

    2. Hallo storage account latenties lage neemt contact op met uw netwerk beheerder tooinvestigate eventuele latentie in uw netwerk problemen.

#### <a name="sample-output-of-performance-test-run-on-an-8100-device"></a>Voorbeeld van uitvoer van de prestatietest uitvoeren op een 8100-apparaat

```
Controller0>Invoke-HcsDiagnostics -Scope Performance
Running performance diagnostics...
--------------------------------------------------
Cloud performance: writing blobs
Cloud write latency: 194 ms using credential 'myss8000storageacct', blob size '64KB'
Cloud performance: reading blobs..
Cloud read latency: 544 ms using credential 'myss8000storageacct', blob size '64KB'
Cloud performance: writing blobs.
Cloud write latency: 369 ms using credential 'myss8000storageacct', blob size '512KB'
Cloud performance: reading blobs...
Cloud read latency: 4924 ms using credential 'myss8000storageacct', blob size '512KB'
--------------------------------------------------
Controller0>
```

## <a name="appendix-interpreting-system-information"></a>Bijlage: systeemgegevens interpreteren

Hier volgt een tabel met een beschrijving van wat Hallo verschillende Windows PowerShell-parameters in Hallo systeemgegevens toewijzen aan. 

| PowerShell-Parameter    | Beschrijving  |
|-------------------------|------------------|
| Exemplaar-id             | Elke domeincontroller heeft een unieke id of een GUID die is gekoppeld aan.|
| Naam                    | Hallo beschrijvende naam van Hallo apparaat zoals geconfigureerd via hello Azure-portal tijdens de implementatie van het apparaat. Hallo standaard beschrijvende naam is serienummer Hallo-apparaat. |
| Model                   | Hallo-model van uw StorSimple 8000 serie-apparaat. Hallo-model is 8100 of 8600.|
| Serienummer            | Hallo apparaatserienummer op Hallo factory is toegewezen en 15 tekens lang is. Bijvoorbeeld: 8600 SHX0991003G44HT Hiermee wordt aangegeven:<br> 8600 – is Hallo-Apparaatmodel.<br>SHX – Is Hallo productie-site.<br> 0991003 - is een specifiek product. <br> Laatste 5 cijfers zijn G44HT-Hallo toocreate unieke serienummers verhoogd. Dit kan niet een sequentiële set zijn.|
| Tijdzone                | Hallo apparaat tijdzone zoals geconfigureerd in hello Azure-portal tijdens de implementatie van het apparaat.|
| CurrentController       | Hallo-controller dat u verbonden toothrough Hallo Windows PowerShell-interface van uw StorSimple-apparaat bent.|
| ActiveController        | Hallo-controller die actief is op uw apparaat en alle bewerkingen van Hallo netwerk- en beheerd. Dit kan zijn Controller 0 of 1 van de domeincontroller.  |
| Controller0Status       | Hallo-status van de Controller 0 op uw apparaat. Hallo controller status kan worden normaal uitgevoerd in de herstelmodus of niet bereikbaar.|
| Controller1Status       | Hallo de status van de Controller 1 op uw apparaat.  Hallo controller status kan worden normaal uitgevoerd in de herstelmodus of niet bereikbaar.|
| SystemMode              | Hallo algehele status van uw StorSimple-apparaat. de apparaatstatus Hallo normaal, kan worden onderhoud, of buiten gebruik gestelde (komt overeen toodeactivated in hello Azure-portal).|
| FriendlySoftwareVersion | Hallo beschrijvende tekenreeks die overeenkomt met softwareversie toohello-apparaat. Voor een systeem met Update 4, is de beschrijvende softwareversie Hallo StorSimple 8000 Series Update 4.0.|
| HcsSoftwareVersion      | Hallo HCS software-versie is uitgevoerd op uw apparaat. Bijvoorbeeld: Hallo HCS software versie bijbehorende tooStorSimple 8000 Series Update versie 4.0 is 6.3.9600.17820. |
| ApiVersion              | Hallo softwareversie van Windows PowerShell-API van Hallo HCS apparaat Hallo.|
| VhdVersion              | Hallo softwareversie van Hallo fabrieksimage die Hallo apparaat is bij geleverd. Als u de standaardinstellingen van uw apparaat toofactory opnieuw instelt, voert deze de softwareversie van deze.|
| OSVersion               | Hallo softwareversie van Hallo besturingssysteem Windows Server op Hallo apparaat uitgevoerd. Hallo StorSimple-apparaat is gebaseerd op Windows Server 2012 R2 die overeenkomt met too6.3.9600 Hallo.|
| CisAgentVersion         | Hallo-versie voor uw configuratie-items agent wordt uitgevoerd op uw StorSimple-apparaat. Deze agent kan communiceren met de Hallo StorSimple Manager-service worden uitgevoerd in Azure.|
| MdsAgentVersion         | Hallo versie bijbehorende toohello Mds agent wordt uitgevoerd op uw StorSimple-apparaat. Deze agent wordt verplaatst gegevens toohello controle en diagnostische gegevens Service (MDS).|
| Lsisas2Version          | Hallo versie overeenkomstige toohello LSI stuurprogramma's op uw StorSimple-apparaat.|
| Capaciteit                | Hallo totale capaciteit van Hallo-apparaat in bytes.|
| RemoteManagementMode    | Hiermee wordt aangegeven of Hallo apparaat op afstand worden beheerd via de Windows PowerShell-interface. |
| FipsMode                | Hiermee wordt aangegeven of de Hallo Verenigde Staten Federal Information Processing Standard (FIPS) modus is ingeschakeld op uw apparaat. Hallo FIPS 140-standaard definieert cryptografische algoritmen die zijn goedgekeurd voor gebruik door ons Federal government computersystemen voor Hallo bescherming van gevoelige gegevens. FIPS-modus is standaard ingeschakeld voor apparaten met Update 4 of hoger is. |

## <a name="next-steps"></a>Volgende stappen

* Meer informatie over Hallo [syntaxis van de cmdlet Invoke-HcsDiagnostics hello](https://technet.microsoft.com/library/mt795371.aspx).

* Meer informatie over het te[implementatieproblemen oplossen](storsimple-troubleshoot-deployment.md) op uw StorSimple-apparaat.
