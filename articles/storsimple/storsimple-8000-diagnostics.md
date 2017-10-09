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
# <a name="use-hello-storsimple-diagnostics-tool-tootroubleshoot-8000-series-device-issues"></a><span data-ttu-id="edae9-103">Hallo StorSimple diagnostische hulpprogramma tootroubleshoot 8000 series problemen apparaten gebruiken</span><span class="sxs-lookup"><span data-stu-id="edae9-103">Use hello StorSimple Diagnostics Tool tootroubleshoot 8000 series device issues</span></span>

## <a name="overview"></a><span data-ttu-id="edae9-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="edae9-104">Overview</span></span>

<span data-ttu-id="edae9-105">Hallo StorSimple diagnostische hulpprogramma diagnoses gerelateerde toosystem problemen, prestaties, netwerk en status van de hardware-onderdeel voor een StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="edae9-105">hello StorSimple Diagnostics tool diagnoses issues related toosystem, performance, network, and hardware component health for a StorSimple device.</span></span> <span data-ttu-id="edae9-106">Hallo diagnostische hulpprogramma kan worden gebruikt in verschillende scenario's.</span><span class="sxs-lookup"><span data-stu-id="edae9-106">hello diagnostics tool can be used in various scenarios.</span></span> <span data-ttu-id="edae9-107">Deze scenario's omvatten werkbelasting planning, implementatie van een StorSimple-apparaat, beoordeling van de netwerkomgeving Hallo en Hallo prestaties van een operationeel apparaat bepalen.</span><span class="sxs-lookup"><span data-stu-id="edae9-107">These scenarios include workload planning, deploying a StorSimple device, assessing hello network environment, and determining hello performance of an operational device.</span></span> <span data-ttu-id="edae9-108">In dit artikel biedt een overzicht van diagnostische Hallo en beschrijft hoe Hallo-hulpprogramma kan worden gebruikt met een StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="edae9-108">This article provides an overview of hello diagnostics tool and describes how hello tool can be used with a StorSimple device.</span></span>

<span data-ttu-id="edae9-109">Hallo diagnostische hulpprogramma is voornamelijk bedoeld voor StorSimple 8000 series on-premises apparaten (8100 en 8600).</span><span class="sxs-lookup"><span data-stu-id="edae9-109">hello diagnostics tool is primarily intended for StorSimple 8000 series on-premises devices (8100 and 8600).</span></span>

## <a name="run-diagnostics-tool"></a><span data-ttu-id="edae9-110">Diagnostische hulpprogramma uitvoeren</span><span class="sxs-lookup"><span data-stu-id="edae9-110">Run diagnostics tool</span></span>

<span data-ttu-id="edae9-111">Dit hulpprogramma kan worden uitgevoerd via Windows PowerShell-interface Hallo van uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="edae9-111">This tool can be run via hello Windows PowerShell interface of your StorSimple device.</span></span> <span data-ttu-id="edae9-112">Er zijn twee manieren tooaccess Hallo lokale interface van uw apparaat:</span><span class="sxs-lookup"><span data-stu-id="edae9-112">There are two ways tooaccess hello local interface of your device:</span></span>

* <span data-ttu-id="edae9-113">[Gebruik PuTTY tooconnect toohello de seriële console apparaat](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="edae9-113">[Use PuTTY tooconnect toohello device serial console](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
* <span data-ttu-id="edae9-114">[Externe toegang tot Hallo-hulpprogramma via Hallo Windows PowerShell voor StorSimple](storsimple-remote-connect.md).</span><span class="sxs-lookup"><span data-stu-id="edae9-114">[Remotely access hello tool via hello Windows PowerShell for StorSimple](storsimple-remote-connect.md).</span></span>

<span data-ttu-id="edae9-115">In dit artikel gaan we ervan uit dat u de seriële console van toohello apparaat via de PuTTY hebt verbonden.</span><span class="sxs-lookup"><span data-stu-id="edae9-115">In this article, we assume that you have connected toohello device serial console via PuTTY.</span></span>

#### <a name="toorun-hello-diagnostics-tool"></a><span data-ttu-id="edae9-116">toorun hello diagnostische hulpprogramma</span><span class="sxs-lookup"><span data-stu-id="edae9-116">toorun hello diagnostics tool</span></span>

<span data-ttu-id="edae9-117">Wanneer u toohello Windows PowerShell-interface van Hallo-apparaat hebt gekoppeld, worden uitgevoerd Hallo stappen toorun Hallo cmdlet te volgen.</span><span class="sxs-lookup"><span data-stu-id="edae9-117">Once you have connected toohello Windows PowerShell interface of hello device, perform hello following steps toorun hello cmdlet.</span></span>
1. <span data-ttu-id="edae9-118">Meld u bij de seriële console van toohello apparaat Hallo stappen in [PuTTY gebruiken tooconnect toohello de seriële console apparaat](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="edae9-118">Log on toohello device serial console by following hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>

2. <span data-ttu-id="edae9-119">Type Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="edae9-119">Type hello following command:</span></span>

    `Invoke-HcsDiagnostics`

    <span data-ttu-id="edae9-120">Als de bereikparameter Hallo niet is opgegeven, voert Hallo cmdlet alle Hallo diagnostische tests.</span><span class="sxs-lookup"><span data-stu-id="edae9-120">If hello scope parameter is not specified, hello cmdlet executes all hello diagnostic tests.</span></span> <span data-ttu-id="edae9-121">Deze tests omvatten system, status voor hardware-onderdeel, netwerk en prestaties.</span><span class="sxs-lookup"><span data-stu-id="edae9-121">These tests include system, hardware component health, network, and performance.</span></span> 
    
    <span data-ttu-id="edae9-122">alleen een specifieke test toorun Hallo scope-parameter opgeven.</span><span class="sxs-lookup"><span data-stu-id="edae9-122">toorun only a specific test, specify hello scope parameter.</span></span> <span data-ttu-id="edae9-123">Bijvoorbeeld: toorun alleen Hallo Netwerktest, type</span><span class="sxs-lookup"><span data-stu-id="edae9-123">For instance, toorun only hello network test, type</span></span>

    `Invoke-HcsDiagnostics -Scope Network`

3. <span data-ttu-id="edae9-124">Selecteer en kopieer Hallo uitvoer van Hallo PuTTY venster in een tekstbestand voor verdere analyse.</span><span class="sxs-lookup"><span data-stu-id="edae9-124">Select and copy hello output from hello PuTTY window into a text file for further analysis.</span></span>

## <a name="scenarios-toouse-hello-diagnostics-tool"></a><span data-ttu-id="edae9-125">Scenario's toouse Hallo diagnostische hulpprogramma</span><span class="sxs-lookup"><span data-stu-id="edae9-125">Scenarios toouse hello diagnostics tool</span></span>

<span data-ttu-id="edae9-126">Hallo diagnostische hulpprogramma tootroubleshoot Hallo netwerk, prestaties, systeem en hardware status van Hallo system gebruiken.</span><span class="sxs-lookup"><span data-stu-id="edae9-126">Use hello diagnostics tool tootroubleshoot hello network, performance, system, and hardware health of hello system.</span></span> <span data-ttu-id="edae9-127">Hier volgen enkele mogelijke scenario's:</span><span class="sxs-lookup"><span data-stu-id="edae9-127">Here are some possible scenarios:</span></span>

* <span data-ttu-id="edae9-128">**Apparaat offline** -uw StorSimple 8000 series apparaat offline is.</span><span class="sxs-lookup"><span data-stu-id="edae9-128">**Device offline** - Your StorSimple 8000 series device is offline.</span></span> <span data-ttu-id="edae9-129">Echter van Windows PowerShell-interface hello, het lijkt erop dat beide domeincontrollers Hallo actief zijn.</span><span class="sxs-lookup"><span data-stu-id="edae9-129">However, from hello Windows PowerShell interface, it seems that both hello controllers are up and running.</span></span>
    * <span data-ttu-id="edae9-130">U kunt dit hulpprogramma toothen Hallo netwerk status bepalen.</span><span class="sxs-lookup"><span data-stu-id="edae9-130">You can use this tool toothen determine hello network state.</span></span>
         
         > [!NOTE]
         > <span data-ttu-id="edae9-131">Gebruik dit hulpprogramma tooassess prestatie- en netwerkinstellingen niet op een apparaat voordat het Hallo-registratie (of configureren via de wizard setup).</span><span class="sxs-lookup"><span data-stu-id="edae9-131">Do not use this tool tooassess performance and network settings on a device before hello registration (or configuring via setup wizard).</span></span> <span data-ttu-id="edae9-132">Een geldig IP-adres wordt toohello apparaat tijdens de wizard setup en de registratie toegewezen.</span><span class="sxs-lookup"><span data-stu-id="edae9-132">A valid IP is assigned toohello device during setup wizard and registration.</span></span> <span data-ttu-id="edae9-133">U kunt deze cmdlet uitvoeren op een apparaat dat niet is geregistreerd voor de status van de hardware- en systeem.</span><span class="sxs-lookup"><span data-stu-id="edae9-133">You can run this cmdlet, on a device that is not registered, for hardware health and system.</span></span> <span data-ttu-id="edae9-134">Gebruik bereikparameter hello, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="edae9-134">Use hello scope parameter, for example:</span></span>
         >
         > `Invoke-HcsDiagnostics -Scope Hardware`
         >
         > `Invoke-HcsDiagnostics -Scope System`

* <span data-ttu-id="edae9-135">**Problemen met de permanente apparaat** -apparaat problemen die toopersist lijken zich voordoen.</span><span class="sxs-lookup"><span data-stu-id="edae9-135">**Persistent device issues** - You are experiencing device issues that seem toopersist.</span></span> <span data-ttu-id="edae9-136">Bijvoorbeeld, de registratie is mislukt.</span><span class="sxs-lookup"><span data-stu-id="edae9-136">For instance, registration is failing.</span></span> <span data-ttu-id="edae9-137">U kan ook worden ondervindt problemen met apparaat nadat het Hallo-apparaat is geregistreerd en operationele voor even wordt.</span><span class="sxs-lookup"><span data-stu-id="edae9-137">You could also be experiencing device issues after hello device is successfully registered and operational for a while.</span></span>
    * <span data-ttu-id="edae9-138">In dit geval moet u dit hulpprogramma gebruiken voor voorlopige probleemoplossing voordat u zich een serviceaanvraag met Microsoft Support aanmeldt.</span><span class="sxs-lookup"><span data-stu-id="edae9-138">In this case, use this tool for preliminary troubleshooting before you log a service request with Microsoft Support.</span></span> <span data-ttu-id="edae9-139">Het is raadzaam dat u deze hulpprogramma's en vastleggen Hallo-uitvoer van dit hulpprogramma uitvoert.</span><span class="sxs-lookup"><span data-stu-id="edae9-139">We recommend that you run this tool and capture hello output of this tool.</span></span> <span data-ttu-id="edae9-140">Vervolgens kunt u bieden deze uitvoer tooSupport tooexpedite probleemoplossing.</span><span class="sxs-lookup"><span data-stu-id="edae9-140">You can then provide this output tooSupport tooexpedite troubleshooting.</span></span>
    * <span data-ttu-id="edae9-141">Als er een onderdeel of het cluster hardwarefouten, moet u een ondersteuningsaanvraag aanmelden.</span><span class="sxs-lookup"><span data-stu-id="edae9-141">If there are any hardware component or cluster failures, you should log in a Support request.</span></span>

* <span data-ttu-id="edae9-142">**Lage Apparaatprestaties** -uw StorSimple-apparaat traag is.</span><span class="sxs-lookup"><span data-stu-id="edae9-142">**Low device performance** - Your StorSimple device is slow.</span></span>
    * <span data-ttu-id="edae9-143">In dit geval moet u deze cmdlet uitvoeren met de scope-parameter set tooperformance.</span><span class="sxs-lookup"><span data-stu-id="edae9-143">In this case, run this cmdlet with scope parameter set tooperformance.</span></span> <span data-ttu-id="edae9-144">Analyseer het Hallo-uitvoer.</span><span class="sxs-lookup"><span data-stu-id="edae9-144">Analyze hello output.</span></span> <span data-ttu-id="edae9-145">U krijgt Hallo cloud lezen-schrijven latenties.</span><span class="sxs-lookup"><span data-stu-id="edae9-145">You get hello cloud read-write latencies.</span></span> <span data-ttu-id="edae9-146">Gebruik Hallo gerapporteerd latenties maximale haalbare TARGET rekening te houden in enige overhead voor interne gegevensverwerking Hallo en vervolgens implementeren Hallo werkbelastingen op Hallo-systeem.</span><span class="sxs-lookup"><span data-stu-id="edae9-146">Use hello reported latencies as maximum achievable target, factor in some overhead for hello internal data processing, and then deploy hello workloads on hello system.</span></span> <span data-ttu-id="edae9-147">Voor meer informatie gaat te[Hallo test tootroubleshoot apparaat netwerkprestaties gebruiken](#network-test).</span><span class="sxs-lookup"><span data-stu-id="edae9-147">For more information, go too[Use hello network test tootroubleshoot device performance](#network-test).</span></span>


## <a name="diagnostics-test-and-sample-outputs"></a><span data-ttu-id="edae9-148">Diagnostische test en voorbeeld-uitvoer</span><span class="sxs-lookup"><span data-stu-id="edae9-148">Diagnostics test and sample outputs</span></span>

### <a name="hardware-test"></a><span data-ttu-id="edae9-149">Hardwaretest</span><span class="sxs-lookup"><span data-stu-id="edae9-149">Hardware test</span></span>

<span data-ttu-id="edae9-150">Deze test bepaalt Hallo status van de hardwareonderdelen hello, Hallo USM firmware en Hallo schijf firmware die wordt uitgevoerd op uw systeem.</span><span class="sxs-lookup"><span data-stu-id="edae9-150">This test determines hello status of hello hardware components, hello USM firmware, and hello disk firmware running on your system.</span></span>

* <span data-ttu-id="edae9-151">Hallo hardwareonderdelen gerapporteerd mislukte Hallo test van deze onderdelen zijn of zijn niet aanwezig in het Hallo-systeem.</span><span class="sxs-lookup"><span data-stu-id="edae9-151">hello hardware components reported are those components that failed hello test or are not present in hello system.</span></span>
* <span data-ttu-id="edae9-152">Hallo USM firmware- en firmware-versies zijn gerapporteerd voor Hallo Controller 0, 1 van de domeincontroller, en gedeelde onderdelen in uw systeem.</span><span class="sxs-lookup"><span data-stu-id="edae9-152">hello USM firmware and disk firmware versions are reported for hello Controller 0, Controller 1, and shared components in your system.</span></span> <span data-ttu-id="edae9-153">Voor een volledige lijst van hardware-onderdelen, gaat u naar:</span><span class="sxs-lookup"><span data-stu-id="edae9-153">For a complete list of hardware components, go to:</span></span>

    * [<span data-ttu-id="edae9-154">Primaire behuizing-onderdelen</span><span class="sxs-lookup"><span data-stu-id="edae9-154">Components in primary enclosure</span></span>](storsimple-monitor-hardware-status.md#component-list-for-primary-enclosure-of-storsimple-device)
    * [<span data-ttu-id="edae9-155">EBOD behuizing-onderdelen</span><span class="sxs-lookup"><span data-stu-id="edae9-155">Components in EBOD enclosure</span></span>](storsimple-monitor-hardware-status.md#component-list-for-ebod-enclosure-of-storsimple-device)

> [!NOTE]
> <span data-ttu-id="edae9-156">Als Hallo hardwaretest niet functionerende onderdelen, rapporteert [Meld u bij een serviceaanvraag met Microsoft Support](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="edae9-156">If hello hardware test reports failed components, [log in a service request with Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>

#### <a name="sample-output-of-hardware-test-run-on-an-8100-device"></a><span data-ttu-id="edae9-157">Voorbeeld van uitvoer van de hardwaretest uitgevoerd op een 8100-apparaat</span><span class="sxs-lookup"><span data-stu-id="edae9-157">Sample output of hardware test run on an 8100 device</span></span>

<span data-ttu-id="edae9-158">Hier volgt een voorbeeld van uitvoer van een StorSimple 8100-apparaat.</span><span class="sxs-lookup"><span data-stu-id="edae9-158">Here is a sample output from a StorSimple 8100 device.</span></span> <span data-ttu-id="edae9-159">Hallo EBOD behuizing is niet aanwezig in Hallo 8100 model-apparaat.</span><span class="sxs-lookup"><span data-stu-id="edae9-159">In hello 8100 model device, hello EBOD enclosure is not present.</span></span> <span data-ttu-id="edae9-160">Hallo EBOD controller onderdelen worden daarom niet gemeld.</span><span class="sxs-lookup"><span data-stu-id="edae9-160">Hence, hello EBOD controller components are not reported.</span></span>

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

### <a name="system-test"></a><span data-ttu-id="edae9-161">Systeem-test</span><span class="sxs-lookup"><span data-stu-id="edae9-161">System test</span></span>

<span data-ttu-id="edae9-162">Deze test rapporten systeemgegevens hello, Hallo updates die beschikbaar zijn, Hallo clustergegevens en Hallo service-informatie voor uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="edae9-162">This test reports hello system information, hello updates available, hello cluster information, and hello service information for your device.</span></span>

* <span data-ttu-id="edae9-163">Hallo systeemgegevens bevat Hallo model, apparaatserienummer tijdzone, status van de domeincontroller en gedetailleerde softwareversie Hallo Hallo systeem waarop.</span><span class="sxs-lookup"><span data-stu-id="edae9-163">hello system information includes hello model, device serial number, time zone, controller status, and hello detailed software version running on hello system.</span></span> <span data-ttu-id="edae9-164">toounderstand hello verschillende parameters voor het gerapporteerd als Hallo-uitvoer te gaan[systeemgegevens interpreteren](#appendix-interpreting-system-information).</span><span class="sxs-lookup"><span data-stu-id="edae9-164">toounderstand hello various system parameters reported as hello output, go too[Interpreting system information](#appendix-interpreting-system-information).</span></span>

* <span data-ttu-id="edae9-165">beschikbaarheid van de Hallo rapporten of Hallo regular en onderhoud modi beschikbaar zijn en de namen van de bijbehorende pakket.</span><span class="sxs-lookup"><span data-stu-id="edae9-165">hello update availability reports whether hello regular and maintenance modes are available and their associated package names.</span></span> <span data-ttu-id="edae9-166">Als `RegularUpdates` en `MaintenanceModeUpdates` zijn `false`, wordt hiermee Hallo updates zijn niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="edae9-166">If `RegularUpdates` and `MaintenanceModeUpdates` are `false`, this indicates that hello updates are not available.</span></span> <span data-ttu-id="edae9-167">Uw apparaat is bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="edae9-167">Your device is up-to-date.</span></span>
* <span data-ttu-id="edae9-168">Hallo clustergegevens bevat Hallo informatie over verschillende logische onderdelen van de Hallo HCS clustergroepen en hun respectieve statussen.</span><span class="sxs-lookup"><span data-stu-id="edae9-168">hello cluster information contains hello information on various logical components of all hello HCS cluster groups and their respective statuses.</span></span> <span data-ttu-id="edae9-169">Als u een offline clustergroep in deze sectie van het Hallo-rapport ziet [contact op met Microsoft Support](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="edae9-169">If you see an offline cluster group in this section of hello report, [contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>
* <span data-ttu-id="edae9-170">Hallo service informatie omvat Hallo namen en status van alle Hallo HCS en CiS services die worden uitgevoerd op uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="edae9-170">hello service information includes hello names and statuses of all hello HCS and CiS services running on your device.</span></span> <span data-ttu-id="edae9-171">Deze informatie is nuttig voor Hallo Microsoft Support op Hallo apparaat probleem op te lossen.</span><span class="sxs-lookup"><span data-stu-id="edae9-171">This information is helpful for hello Microsoft Support in troubleshooting hello device issue.</span></span>

#### <a name="sample-output-of-system-test-run-on-an-8100-device"></a><span data-ttu-id="edae9-172">Voorbeeld van uitvoer van systeem test uitgevoerd op een 8100-apparaat</span><span class="sxs-lookup"><span data-stu-id="edae9-172">Sample output of system test run on an 8100 device</span></span>

<span data-ttu-id="edae9-173">Hier volgt een voorbeeld van uitvoer van Hallo system test uitgevoerd op een 8100-apparaat.</span><span class="sxs-lookup"><span data-stu-id="edae9-173">Here is a sample output of hello system test run on an 8100 device.</span></span>

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

### <a name="network-test"></a><span data-ttu-id="edae9-174">Netwerktest</span><span class="sxs-lookup"><span data-stu-id="edae9-174">Network test</span></span>

<span data-ttu-id="edae9-175">Deze test valideert Hallo status van netwerkinterfaces hello, poorten, DNS- en NTP serververbindingen, SSL-certificaat, opslagaccountreferenties, connectiviteit toohello Update-servers en web proxy connectiviteit op uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="edae9-175">This test validates hello status of hello network interfaces, ports, DNS and NTP server connectivity, SSL certificate, storage account credentials, connectivity toohello Update servers, and web proxy connectivity on your StorSimple device.</span></span>

#### <a name="sample-output-of-network-test-when-only-data0-is-enabled"></a><span data-ttu-id="edae9-176">Voorbeeld van uitvoer van het netwerk testen wanneer alleen DATA0 is ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="edae9-176">Sample output of network test when only DATA0 is enabled</span></span>

<span data-ttu-id="edae9-177">Hier volgt een voorbeeld van uitvoer van Hallo 8100-apparaat.</span><span class="sxs-lookup"><span data-stu-id="edae9-177">Here is a sample output of hello 8100 device.</span></span> <span data-ttu-id="edae9-178">U kunt zien in de uitvoer Hallo die:</span><span class="sxs-lookup"><span data-stu-id="edae9-178">You can see in hello output that:</span></span>
* <span data-ttu-id="edae9-179">Alleen DATA 0 en 1 gegevens netwerkinterfaces zijn ingeschakeld en geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="edae9-179">Only DATA 0 and DATA 1 network interfaces are enabled and configured.</span></span>
* <span data-ttu-id="edae9-180">GEGEVENS-2-5 zijn niet ingeschakeld in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="edae9-180">DATA 2 - 5 are not enabled in hello portal.</span></span>
* <span data-ttu-id="edae9-181">configuratie van Hallo DNS-server is geldig en Hallo apparaat verbinding kan maken via Hallo DNS-server.</span><span class="sxs-lookup"><span data-stu-id="edae9-181">hello DNS server configuration is valid and hello device can connect via hello DNS server.</span></span>
* <span data-ttu-id="edae9-182">Hallo NTP-serververbindingen is ook geen probleem.</span><span class="sxs-lookup"><span data-stu-id="edae9-182">hello NTP server connectivity is also fine.</span></span>
* <span data-ttu-id="edae9-183">Poorten 80 en 443 zijn geopend.</span><span class="sxs-lookup"><span data-stu-id="edae9-183">Ports 80 and 443 are open.</span></span> <span data-ttu-id="edae9-184">Poort 9354 is geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="edae9-184">However, port 9354 is blocked.</span></span> <span data-ttu-id="edae9-185">Op basis van Hallo [netwerk systeemvereisten](storsimple-system-requirements.md), moet u tooopen deze poort voor Hallo service bus-communicatie.</span><span class="sxs-lookup"><span data-stu-id="edae9-185">Based on hello [system network requirements](storsimple-system-requirements.md), you need tooopen this port for hello service bus communication.</span></span>
* <span data-ttu-id="edae9-186">Hallo SSL-certificaat is geldig.</span><span class="sxs-lookup"><span data-stu-id="edae9-186">hello SSL certification is valid.</span></span>
* <span data-ttu-id="edae9-187">Hallo apparaat verbinding kan maken toohello storage-account: _myss8000storageacct_.</span><span class="sxs-lookup"><span data-stu-id="edae9-187">hello device can connect toohello storage account: _myss8000storageacct_.</span></span>
* <span data-ttu-id="edae9-188">Hallo connectiviteit tooUpdate servers is ongeldig.</span><span class="sxs-lookup"><span data-stu-id="edae9-188">hello connectivity tooUpdate servers is valid.</span></span>
* <span data-ttu-id="edae9-189">Hallo webproxy is niet geconfigureerd op dit apparaat.</span><span class="sxs-lookup"><span data-stu-id="edae9-189">hello web proxy is not configured on this device.</span></span>

#### <a name="sample-output-of-network-test-when-data0-and-data1-are-enabled"></a><span data-ttu-id="edae9-190">Voorbeeld van uitvoer van Netwerktest wanneer DATA0 en bestand1 zijn ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="edae9-190">Sample output of network test when DATA0 and DATA1 are enabled</span></span>

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

### <a name="performance-test"></a><span data-ttu-id="edae9-191">Prestatietest</span><span class="sxs-lookup"><span data-stu-id="edae9-191">Performance test</span></span>

<span data-ttu-id="edae9-192">Deze test rapporten Hallo cloud prestaties via Hallo cloud lezen-schrijven latenties voor uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="edae9-192">This test reports hello cloud performance via hello cloud read-write latencies for your device.</span></span> <span data-ttu-id="edae9-193">Dit hulpprogramma kan worden gebruikt tooestablish een basislijn van prestaties van een Hallo cloud die u met StorSimple bereiken kunt.</span><span class="sxs-lookup"><span data-stu-id="edae9-193">This tool can be used tooestablish a baseline of hello cloud performance that you can achieve with StorSimple.</span></span> <span data-ttu-id="edae9-194">Hallo hulpprogramma rapporten Hallo maximale prestaties (beste scenario voor lezen-schrijven latenties) die u voor de verbinding ophalen kunt.</span><span class="sxs-lookup"><span data-stu-id="edae9-194">hello tool reports hello maximum performance (best case scenario for read-write latencies) that you can get for your connection.</span></span>

<span data-ttu-id="edae9-195">Als Hallo hulpprogramma Hallo maximale haalbare prestaties meldt, gebruiken we Hallo lezen-schrijven latenties als doelen bij het implementeren van Hallo werkbelastingen gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="edae9-195">As hello tool reports hello maximum achievable performance, we can use hello reported read-write latencies as targets when deploying hello workloads.</span></span>

<span data-ttu-id="edae9-196">Hallo test simuleert Hallo blob grootten Hallo ander volumetypen op Hallo apparaat gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="edae9-196">hello test simulates hello blob sizes associated with hello different volume types on hello device.</span></span> <span data-ttu-id="edae9-197">Gewone lagen en back-ups van lokaal vastgemaakte volumes met een blob-grootte van 64 KB.</span><span class="sxs-lookup"><span data-stu-id="edae9-197">Regular tiered and backups of locally pinned volumes use a 64 KB blob size.</span></span> <span data-ttu-id="edae9-198">Gelaagde volumes met archief-optie ingeschakeld gebruiken blob-gegevensgrootte 512 KB.</span><span class="sxs-lookup"><span data-stu-id="edae9-198">Tiered volumes with archive option checked use 512 KB blob data size.</span></span> <span data-ttu-id="edae9-199">Als het apparaat heeft gelaagde en lokaal vastgemaakte volumes geconfigureerd, alleen Hallo test bijbehorende too64 KB blob gegevensgrootte wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="edae9-199">If your device has tiered and locally pinned volumes configured, only hello test corresponding too64 KB blob data size is run.</span></span>

<span data-ttu-id="edae9-200">toouse dit hulpprogramma uitvoeren Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="edae9-200">toouse this tool, perform hello following steps:</span></span>

1.  <span data-ttu-id="edae9-201">Maak eerst een combinatie van gelaagde volumes en gelaagde volumes met gearchiveerde optie ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="edae9-201">First, create a mix of tiered volumes and tiered volumes with archived option checked.</span></span> <span data-ttu-id="edae9-202">Deze actie zorgt ervoor dat hulpprogramma Hallo Hallo tests voor 64 KB en 512 KB grootten van de blob.</span><span class="sxs-lookup"><span data-stu-id="edae9-202">This action ensures that hello tool runs hello tests for both 64 KB and 512 KB blob sizes.</span></span>

2. <span data-ttu-id="edae9-203">Hallo-cmdlet uitvoeren nadat u hebt gemaakt en geconfigureerd Hallo volumes.</span><span class="sxs-lookup"><span data-stu-id="edae9-203">Run hello cmdlet after you have created and configured hello volumes.</span></span> <span data-ttu-id="edae9-204">Type:</span><span class="sxs-lookup"><span data-stu-id="edae9-204">Type:</span></span>

    `Invoke-HcsDiagnostics -Scope Performance`

3. <span data-ttu-id="edae9-205">Noteer Hallo lezen-schrijven latenties gemeld door het Hallo-hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="edae9-205">Make a note of hello read-write latencies reported by hello tool.</span></span> <span data-ttu-id="edae9-206">Deze test kunt toorun van enkele minuten duren voordat Hallo resultaten gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="edae9-206">This test can take several minutes toorun before it reports hello results.</span></span>

4. <span data-ttu-id="edae9-207">Als Hallo verbinding latenties zijn onder Hallo verwacht bereik en hello latenties gemeld door het Hallo-hulpprogramma kunnen worden gebruikt als maximale haalbare doel bij het implementeren van Hallo werkbelastingen.</span><span class="sxs-lookup"><span data-stu-id="edae9-207">If hello connection latencies are all under hello expected range, then hello latencies reported by hello tool can be used as maximum achievable target when deploying hello workloads.</span></span> <span data-ttu-id="edae9-208">Rekening te houden in enige overhead voor interne gegevensverwerking.</span><span class="sxs-lookup"><span data-stu-id="edae9-208">Factor in some overhead for internal data processing.</span></span>

    <span data-ttu-id="edae9-209">Als Hallo lezen-schrijven latenties gerapporteerd door Hallo diagnostische hulpprogramma hoog zijn:</span><span class="sxs-lookup"><span data-stu-id="edae9-209">If hello read-write latencies reported by hello diagnostics tool are high:</span></span>

    1. <span data-ttu-id="edae9-210">Storage Analytics voor blob-services configureren en analyseren van Hallo uitvoer toounderstand Hallo latenties voor hello Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="edae9-210">Configure Storage Analytics for blob services and analyze hello output toounderstand hello latencies for hello Azure storage account.</span></span> <span data-ttu-id="edae9-211">Voor gedetailleerde instructies gaat te[inschakelen en configureren van opslag Analytics](../storage/common/storage-enable-and-view-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="edae9-211">For detailed instructions, go too[enable and configure Storage Analytics](../storage/common/storage-enable-and-view-metrics.md).</span></span> <span data-ttu-id="edae9-212">Als deze latenties ook hoge en vergelijkbare toohello cijfers die u hebt ontvangen van Hallo StorSimple diagnostische hulpprogramma, moet u toolog een serviceaanvraag met Azure storage.</span><span class="sxs-lookup"><span data-stu-id="edae9-212">If those latencies are also high and comparable toohello numbers you received from hello StorSimple Diagnostics tool, then you need toolog a service request with Azure storage.</span></span>

    2. <span data-ttu-id="edae9-213">Hallo storage account latenties lage neemt contact op met uw netwerk beheerder tooinvestigate eventuele latentie in uw netwerk problemen.</span><span class="sxs-lookup"><span data-stu-id="edae9-213">If hello storage account latencies are low, contact your network administrator tooinvestigate any latency issues in your network.</span></span>

#### <a name="sample-output-of-performance-test-run-on-an-8100-device"></a><span data-ttu-id="edae9-214">Voorbeeld van uitvoer van de prestatietest uitvoeren op een 8100-apparaat</span><span class="sxs-lookup"><span data-stu-id="edae9-214">Sample output of performance test run on an 8100 device</span></span>

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

## <a name="appendix-interpreting-system-information"></a><span data-ttu-id="edae9-215">Bijlage: systeemgegevens interpreteren</span><span class="sxs-lookup"><span data-stu-id="edae9-215">Appendix: interpreting system information</span></span>

<span data-ttu-id="edae9-216">Hier volgt een tabel met een beschrijving van wat Hallo verschillende Windows PowerShell-parameters in Hallo systeemgegevens toewijzen aan.</span><span class="sxs-lookup"><span data-stu-id="edae9-216">Here is a table describing what hello various Windows PowerShell parameters in hello system information map to.</span></span> 

| <span data-ttu-id="edae9-217">PowerShell-Parameter</span><span class="sxs-lookup"><span data-stu-id="edae9-217">PowerShell Parameter</span></span>    | <span data-ttu-id="edae9-218">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="edae9-218">Description</span></span>  |
|-------------------------|------------------|
| <span data-ttu-id="edae9-219">Exemplaar-id</span><span class="sxs-lookup"><span data-stu-id="edae9-219">Instance ID</span></span>             | <span data-ttu-id="edae9-220">Elke domeincontroller heeft een unieke id of een GUID die is gekoppeld aan.</span><span class="sxs-lookup"><span data-stu-id="edae9-220">Every controller has a unique identifier or a GUID associated with it.</span></span>|
| <span data-ttu-id="edae9-221">Naam</span><span class="sxs-lookup"><span data-stu-id="edae9-221">Name</span></span>                    | <span data-ttu-id="edae9-222">Hallo beschrijvende naam van Hallo apparaat zoals geconfigureerd via hello Azure-portal tijdens de implementatie van het apparaat.</span><span class="sxs-lookup"><span data-stu-id="edae9-222">hello friendly name of hello device as configured through hello Azure portal during device deployment.</span></span> <span data-ttu-id="edae9-223">Hallo standaard beschrijvende naam is serienummer Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="edae9-223">hello default friendly name is hello device serial number.</span></span> |
| <span data-ttu-id="edae9-224">Model</span><span class="sxs-lookup"><span data-stu-id="edae9-224">Model</span></span>                   | <span data-ttu-id="edae9-225">Hallo-model van uw StorSimple 8000 serie-apparaat.</span><span class="sxs-lookup"><span data-stu-id="edae9-225">hello model of your StorSimple 8000 series device.</span></span> <span data-ttu-id="edae9-226">Hallo-model is 8100 of 8600.</span><span class="sxs-lookup"><span data-stu-id="edae9-226">hello model can be 8100 or 8600.</span></span>|
| <span data-ttu-id="edae9-227">Serienummer</span><span class="sxs-lookup"><span data-stu-id="edae9-227">SerialNumber</span></span>            | <span data-ttu-id="edae9-228">Hallo apparaatserienummer op Hallo factory is toegewezen en 15 tekens lang is.</span><span class="sxs-lookup"><span data-stu-id="edae9-228">hello device serial number is assigned at hello factory and is 15 characters long.</span></span> <span data-ttu-id="edae9-229">Bijvoorbeeld: 8600 SHX0991003G44HT Hiermee wordt aangegeven:</span><span class="sxs-lookup"><span data-stu-id="edae9-229">For instance, 8600-SHX0991003G44HT indicates:</span></span><br> <span data-ttu-id="edae9-230">8600 – is Hallo-Apparaatmodel.</span><span class="sxs-lookup"><span data-stu-id="edae9-230">8600 – Is hello device model.</span></span><br><span data-ttu-id="edae9-231">SHX – Is Hallo productie-site.</span><span class="sxs-lookup"><span data-stu-id="edae9-231">SHX – Is hello manufacturing site.</span></span><br> <span data-ttu-id="edae9-232">0991003 - is een specifiek product.</span><span class="sxs-lookup"><span data-stu-id="edae9-232">0991003 - Is a specific product.</span></span> <br> <span data-ttu-id="edae9-233">Laatste 5 cijfers zijn G44HT-Hallo toocreate unieke serienummers verhoogd.</span><span class="sxs-lookup"><span data-stu-id="edae9-233">G44HT- hello last 5 digits are incremented toocreate unique serial numbers.</span></span> <span data-ttu-id="edae9-234">Dit kan niet een sequentiële set zijn.</span><span class="sxs-lookup"><span data-stu-id="edae9-234">This may not be a sequential set.</span></span>|
| <span data-ttu-id="edae9-235">Tijdzone</span><span class="sxs-lookup"><span data-stu-id="edae9-235">TimeZone</span></span>                | <span data-ttu-id="edae9-236">Hallo apparaat tijdzone zoals geconfigureerd in hello Azure-portal tijdens de implementatie van het apparaat.</span><span class="sxs-lookup"><span data-stu-id="edae9-236">hello device time zone as configured in hello Azure portal during device deployment.</span></span>|
| <span data-ttu-id="edae9-237">CurrentController</span><span class="sxs-lookup"><span data-stu-id="edae9-237">CurrentController</span></span>       | <span data-ttu-id="edae9-238">Hallo-controller dat u verbonden toothrough Hallo Windows PowerShell-interface van uw StorSimple-apparaat bent.</span><span class="sxs-lookup"><span data-stu-id="edae9-238">hello controller that you are connected toothrough hello Windows PowerShell interface of your StorSimple device.</span></span>|
| <span data-ttu-id="edae9-239">ActiveController</span><span class="sxs-lookup"><span data-stu-id="edae9-239">ActiveController</span></span>        | <span data-ttu-id="edae9-240">Hallo-controller die actief is op uw apparaat en alle bewerkingen van Hallo netwerk- en beheerd.</span><span class="sxs-lookup"><span data-stu-id="edae9-240">hello controller that is active on your device and is controlling all hello network and disk operations.</span></span> <span data-ttu-id="edae9-241">Dit kan zijn Controller 0 of 1 van de domeincontroller.</span><span class="sxs-lookup"><span data-stu-id="edae9-241">This can be Controller 0 or Controller 1.</span></span>  |
| <span data-ttu-id="edae9-242">Controller0Status</span><span class="sxs-lookup"><span data-stu-id="edae9-242">Controller0Status</span></span>       | <span data-ttu-id="edae9-243">Hallo-status van de Controller 0 op uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="edae9-243">hello status of Controller 0 on your device.</span></span> <span data-ttu-id="edae9-244">Hallo controller status kan worden normaal uitgevoerd in de herstelmodus of niet bereikbaar.</span><span class="sxs-lookup"><span data-stu-id="edae9-244">hello controller status can be normal, in recovery mode, or unreachable.</span></span>|
| <span data-ttu-id="edae9-245">Controller1Status</span><span class="sxs-lookup"><span data-stu-id="edae9-245">Controller1Status</span></span>       | <span data-ttu-id="edae9-246">Hallo de status van de Controller 1 op uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="edae9-246">hello status of Controller 1 on your device.</span></span>  <span data-ttu-id="edae9-247">Hallo controller status kan worden normaal uitgevoerd in de herstelmodus of niet bereikbaar.</span><span class="sxs-lookup"><span data-stu-id="edae9-247">hello controller status can be normal, in recovery mode, or unreachable.</span></span>|
| <span data-ttu-id="edae9-248">SystemMode</span><span class="sxs-lookup"><span data-stu-id="edae9-248">SystemMode</span></span>              | <span data-ttu-id="edae9-249">Hallo algehele status van uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="edae9-249">hello overall status of your StorSimple device.</span></span> <span data-ttu-id="edae9-250">de apparaatstatus Hallo normaal, kan worden onderhoud, of buiten gebruik gestelde (komt overeen toodeactivated in hello Azure-portal).</span><span class="sxs-lookup"><span data-stu-id="edae9-250">hello device status can be normal, maintenance, or decommissioned (corresponds toodeactivated in hello Azure portal).</span></span>|
| <span data-ttu-id="edae9-251">FriendlySoftwareVersion</span><span class="sxs-lookup"><span data-stu-id="edae9-251">FriendlySoftwareVersion</span></span> | <span data-ttu-id="edae9-252">Hallo beschrijvende tekenreeks die overeenkomt met softwareversie toohello-apparaat.</span><span class="sxs-lookup"><span data-stu-id="edae9-252">hello friendly string that corresponds toohello device software version.</span></span> <span data-ttu-id="edae9-253">Voor een systeem met Update 4, is de beschrijvende softwareversie Hallo StorSimple 8000 Series Update 4.0.</span><span class="sxs-lookup"><span data-stu-id="edae9-253">For a system running Update 4, hello friendly software version would be StorSimple 8000 Series Update 4.0.</span></span>|
| <span data-ttu-id="edae9-254">HcsSoftwareVersion</span><span class="sxs-lookup"><span data-stu-id="edae9-254">HcsSoftwareVersion</span></span>      | <span data-ttu-id="edae9-255">Hallo HCS software-versie is uitgevoerd op uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="edae9-255">hello HCS software version running on your device.</span></span> <span data-ttu-id="edae9-256">Bijvoorbeeld: Hallo HCS software versie bijbehorende tooStorSimple 8000 Series Update versie 4.0 is 6.3.9600.17820.</span><span class="sxs-lookup"><span data-stu-id="edae9-256">For instance, hello HCS software version corresponding tooStorSimple 8000 Series Update 4.0 is 6.3.9600.17820.</span></span> |
| <span data-ttu-id="edae9-257">ApiVersion</span><span class="sxs-lookup"><span data-stu-id="edae9-257">ApiVersion</span></span>              | <span data-ttu-id="edae9-258">Hallo softwareversie van Windows PowerShell-API van Hallo HCS apparaat Hallo.</span><span class="sxs-lookup"><span data-stu-id="edae9-258">hello software version of hello Windows PowerShell API of hello HCS device.</span></span>|
| <span data-ttu-id="edae9-259">VhdVersion</span><span class="sxs-lookup"><span data-stu-id="edae9-259">VhdVersion</span></span>              | <span data-ttu-id="edae9-260">Hallo softwareversie van Hallo fabrieksimage die Hallo apparaat is bij geleverd.</span><span class="sxs-lookup"><span data-stu-id="edae9-260">hello software version of hello factory image that hello device was shipped with.</span></span> <span data-ttu-id="edae9-261">Als u de standaardinstellingen van uw apparaat toofactory opnieuw instelt, voert deze de softwareversie van deze.</span><span class="sxs-lookup"><span data-stu-id="edae9-261">If you reset your device toofactory defaults, then it runs this software version.</span></span>|
| <span data-ttu-id="edae9-262">OSVersion</span><span class="sxs-lookup"><span data-stu-id="edae9-262">OSVersion</span></span>               | <span data-ttu-id="edae9-263">Hallo softwareversie van Hallo besturingssysteem Windows Server op Hallo apparaat uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="edae9-263">hello software version of hello Windows Server operating system running on hello device.</span></span> <span data-ttu-id="edae9-264">Hallo StorSimple-apparaat is gebaseerd op Windows Server 2012 R2 die overeenkomt met too6.3.9600 Hallo.</span><span class="sxs-lookup"><span data-stu-id="edae9-264">hello StorSimple device is based off hello Windows Server 2012 R2 that corresponds too6.3.9600.</span></span>|
| <span data-ttu-id="edae9-265">CisAgentVersion</span><span class="sxs-lookup"><span data-stu-id="edae9-265">CisAgentVersion</span></span>         | <span data-ttu-id="edae9-266">Hallo-versie voor uw configuratie-items agent wordt uitgevoerd op uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="edae9-266">hello version for your Cis agent running on your StorSimple device.</span></span> <span data-ttu-id="edae9-267">Deze agent kan communiceren met de Hallo StorSimple Manager-service worden uitgevoerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="edae9-267">This agent helps communicate with hello StorSimple Manager service running in Azure.</span></span>|
| <span data-ttu-id="edae9-268">MdsAgentVersion</span><span class="sxs-lookup"><span data-stu-id="edae9-268">MdsAgentVersion</span></span>         | <span data-ttu-id="edae9-269">Hallo versie bijbehorende toohello Mds agent wordt uitgevoerd op uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="edae9-269">hello version corresponding toohello Mds agent running on your StorSimple device.</span></span> <span data-ttu-id="edae9-270">Deze agent wordt verplaatst gegevens toohello controle en diagnostische gegevens Service (MDS).</span><span class="sxs-lookup"><span data-stu-id="edae9-270">This agent moves data toohello Monitoring and Diagnostics Service (MDS).</span></span>|
| <span data-ttu-id="edae9-271">Lsisas2Version</span><span class="sxs-lookup"><span data-stu-id="edae9-271">Lsisas2Version</span></span>          | <span data-ttu-id="edae9-272">Hallo versie overeenkomstige toohello LSI stuurprogramma's op uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="edae9-272">hello version corresponding toohello LSI drivers on your StorSimple device.</span></span>|
| <span data-ttu-id="edae9-273">Capaciteit</span><span class="sxs-lookup"><span data-stu-id="edae9-273">Capacity</span></span>                | <span data-ttu-id="edae9-274">Hallo totale capaciteit van Hallo-apparaat in bytes.</span><span class="sxs-lookup"><span data-stu-id="edae9-274">hello total capacity of hello device in bytes.</span></span>|
| <span data-ttu-id="edae9-275">RemoteManagementMode</span><span class="sxs-lookup"><span data-stu-id="edae9-275">RemoteManagementMode</span></span>    | <span data-ttu-id="edae9-276">Hiermee wordt aangegeven of Hallo apparaat op afstand worden beheerd via de Windows PowerShell-interface.</span><span class="sxs-lookup"><span data-stu-id="edae9-276">Indicates whether hello device can be remotely managed via its Windows PowerShell interface.</span></span> |
| <span data-ttu-id="edae9-277">FipsMode</span><span class="sxs-lookup"><span data-stu-id="edae9-277">FipsMode</span></span>                | <span data-ttu-id="edae9-278">Hiermee wordt aangegeven of de Hallo Verenigde Staten Federal Information Processing Standard (FIPS) modus is ingeschakeld op uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="edae9-278">Indicates whether hello United States Federal Information Processing Standard (FIPS) mode is enabled on your device.</span></span> <span data-ttu-id="edae9-279">Hallo FIPS 140-standaard definieert cryptografische algoritmen die zijn goedgekeurd voor gebruik door ons Federal government computersystemen voor Hallo bescherming van gevoelige gegevens.</span><span class="sxs-lookup"><span data-stu-id="edae9-279">hello FIPS 140 standard defines cryptographic algorithms approved for use by US Federal government computer systems for hello protection of sensitive data.</span></span> <span data-ttu-id="edae9-280">FIPS-modus is standaard ingeschakeld voor apparaten met Update 4 of hoger is.</span><span class="sxs-lookup"><span data-stu-id="edae9-280">For devices running Update 4 or later, FIPS mode is enabled by default.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="edae9-281">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="edae9-281">Next steps</span></span>

* <span data-ttu-id="edae9-282">Meer informatie over Hallo [syntaxis van de cmdlet Invoke-HcsDiagnostics hello](https://technet.microsoft.com/library/mt795371.aspx).</span><span class="sxs-lookup"><span data-stu-id="edae9-282">Learn hello [syntax of hello Invoke-HcsDiagnostics cmdlet](https://technet.microsoft.com/library/mt795371.aspx).</span></span>

* <span data-ttu-id="edae9-283">Meer informatie over het te[implementatieproblemen oplossen](storsimple-troubleshoot-deployment.md) op uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="edae9-283">Learn more about how too[troubleshoot deployment issues](storsimple-troubleshoot-deployment.md) on your StorSimple device.</span></span>
