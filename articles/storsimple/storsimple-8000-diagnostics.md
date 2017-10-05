---
title: Diagnostische hulpprogramma om op te lossen StorSimple 8000 apparaat | Microsoft Docs
description: Beschrijft de modus voor de StorSimple-apparaat en wordt uitgelegd hoe u Windows PowerShell voor StorSimple om de apparatuurmodus te wijzigen.
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
ms.openlocfilehash: 8fae7bb357f8e5e8eff249edfe3a2aaafe04283c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-storsimple-diagnostics-tool-to-troubleshoot-8000-series-device-issues"></a><span data-ttu-id="b4415-103">Gebruik het diagnostisch hulpprogramma van StorSimple 8000 series apparaat problemen kunt oplossen</span><span class="sxs-lookup"><span data-stu-id="b4415-103">Use the StorSimple Diagnostics Tool to troubleshoot 8000 series device issues</span></span>

## <a name="overview"></a><span data-ttu-id="b4415-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="b4415-104">Overview</span></span>

<span data-ttu-id="b4415-105">Het hulpprogramma StorSimple diagnostische gegevens diagnoses problemen met de status van de onderdeel-systeem, prestaties, netwerk en hardware voor een StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="b4415-105">The StorSimple Diagnostics tool diagnoses issues related to system, performance, network, and hardware component health for a StorSimple device.</span></span> <span data-ttu-id="b4415-106">Het diagnostisch hulpprogramma kan worden gebruikt in verschillende scenario's.</span><span class="sxs-lookup"><span data-stu-id="b4415-106">The diagnostics tool can be used in various scenarios.</span></span> <span data-ttu-id="b4415-107">Deze scenario's omvatten werkbelasting planning, implementatie van een StorSimple-apparaat, beoordeling van de netwerkomgeving en bepalen van de prestaties van een operationeel apparaat.</span><span class="sxs-lookup"><span data-stu-id="b4415-107">These scenarios include workload planning, deploying a StorSimple device, assessing the network environment, and determining the performance of an operational device.</span></span> <span data-ttu-id="b4415-108">In dit artikel biedt een overzicht van het hulpprogramma Diagnostische gegevens en beschrijft hoe het hulpprogramma kan worden gebruikt met een StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="b4415-108">This article provides an overview of the diagnostics tool and describes how the tool can be used with a StorSimple device.</span></span>

<span data-ttu-id="b4415-109">Het diagnostisch hulpprogramma is voornamelijk bedoeld voor StorSimple 8000 series on-premises apparaten (8100 en 8600).</span><span class="sxs-lookup"><span data-stu-id="b4415-109">The diagnostics tool is primarily intended for StorSimple 8000 series on-premises devices (8100 and 8600).</span></span>

## <a name="run-diagnostics-tool"></a><span data-ttu-id="b4415-110">Diagnostische hulpprogramma uitvoeren</span><span class="sxs-lookup"><span data-stu-id="b4415-110">Run diagnostics tool</span></span>

<span data-ttu-id="b4415-111">Dit hulpprogramma kan worden uitgevoerd via de Windows PowerShell-interface van uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="b4415-111">This tool can be run via the Windows PowerShell interface of your StorSimple device.</span></span> <span data-ttu-id="b4415-112">Er zijn twee manieren toegang krijgen tot de lokale interface van uw apparaat:</span><span class="sxs-lookup"><span data-stu-id="b4415-112">There are two ways to access the local interface of your device:</span></span>

* <span data-ttu-id="b4415-113">[PuTTY gebruiken om verbinding maken met de seriële console van het apparaat](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="b4415-113">[Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
* <span data-ttu-id="b4415-114">[Externe toegang tot het hulpprogramma via de Windows PowerShell voor StorSimple](storsimple-remote-connect.md).</span><span class="sxs-lookup"><span data-stu-id="b4415-114">[Remotely access the tool via the Windows PowerShell for StorSimple](storsimple-remote-connect.md).</span></span>

<span data-ttu-id="b4415-115">In dit artikel gaan we ervan uit dat u hebt verbonden met de seriële console van het apparaat via de PuTTY.</span><span class="sxs-lookup"><span data-stu-id="b4415-115">In this article, we assume that you have connected to the device serial console via PuTTY.</span></span>

#### <a name="to-run-the-diagnostics-tool"></a><span data-ttu-id="b4415-116">Het diagnostisch hulpprogramma uitvoeren</span><span class="sxs-lookup"><span data-stu-id="b4415-116">To run the diagnostics tool</span></span>

<span data-ttu-id="b4415-117">Zodra u hebt gekoppeld aan de Windows PowerShell-interface van het apparaat, moet u de volgende stappen om te worden uitgevoerd van de cmdlet uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="b4415-117">Once you have connected to the Windows PowerShell interface of the device, perform the following steps to run the cmdlet.</span></span>
1. <span data-ttu-id="b4415-118">Meld u aan bij de seriële console van het apparaat door de stappen in [PuTTY gebruiken om verbinding maken met de seriële console van het apparaat](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="b4415-118">Log on to the device serial console by following the steps in [Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>

2. <span data-ttu-id="b4415-119">Typ de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="b4415-119">Type the following command:</span></span>

    `Invoke-HcsDiagnostics`

    <span data-ttu-id="b4415-120">Als de scope-parameter niet is opgegeven, wordt de diagnostische tests uitgevoerd door de cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b4415-120">If the scope parameter is not specified, the cmdlet executes all the diagnostic tests.</span></span> <span data-ttu-id="b4415-121">Deze tests omvatten system, status voor hardware-onderdeel, netwerk en prestaties.</span><span class="sxs-lookup"><span data-stu-id="b4415-121">These tests include system, hardware component health, network, and performance.</span></span> 
    
    <span data-ttu-id="b4415-122">Geef voor het uitvoeren van alleen specifieke test, de scope-parameter.</span><span class="sxs-lookup"><span data-stu-id="b4415-122">To run only a specific test, specify the scope parameter.</span></span> <span data-ttu-id="b4415-123">Bijvoorbeeld, u alleen de Netwerktest uitvoeren te typen</span><span class="sxs-lookup"><span data-stu-id="b4415-123">For instance, to run only the network test, type</span></span>

    `Invoke-HcsDiagnostics -Scope Network`

3. <span data-ttu-id="b4415-124">Selecteer en kopieer de uitvoer van het venster PuTTY naar een tekstbestand voor verdere analyse.</span><span class="sxs-lookup"><span data-stu-id="b4415-124">Select and copy the output from the PuTTY window into a text file for further analysis.</span></span>

## <a name="scenarios-to-use-the-diagnostics-tool"></a><span data-ttu-id="b4415-125">Scenario's met het hulpprogramma voor diagnostische gegevens</span><span class="sxs-lookup"><span data-stu-id="b4415-125">Scenarios to use the diagnostics tool</span></span>

<span data-ttu-id="b4415-126">Gebruik het diagnostisch hulpprogramma oplossen van problemen met de status van het netwerk, prestaties, systeem en hardware van het systeem.</span><span class="sxs-lookup"><span data-stu-id="b4415-126">Use the diagnostics tool to troubleshoot the network, performance, system, and hardware health of the system.</span></span> <span data-ttu-id="b4415-127">Hier volgen enkele mogelijke scenario's:</span><span class="sxs-lookup"><span data-stu-id="b4415-127">Here are some possible scenarios:</span></span>

* <span data-ttu-id="b4415-128">**Apparaat offline** -uw StorSimple 8000 series apparaat offline is.</span><span class="sxs-lookup"><span data-stu-id="b4415-128">**Device offline** - Your StorSimple 8000 series device is offline.</span></span> <span data-ttu-id="b4415-129">Echter, uit de Windows PowerShell-interface het lijkt erop dat beide domeincontrollers actief en werkend zijn.</span><span class="sxs-lookup"><span data-stu-id="b4415-129">However, from the Windows PowerShell interface, it seems that both the controllers are up and running.</span></span>
    * <span data-ttu-id="b4415-130">Dit hulpprogramma kunt u vervolgens de netwerk-status te bepalen.</span><span class="sxs-lookup"><span data-stu-id="b4415-130">You can use this tool to then determine the network state.</span></span>
         
         > [!NOTE]
         > <span data-ttu-id="b4415-131">Gebruik dit hulpprogramma niet om u te evalueren prestatie- en instellingen op een apparaat voordat u de registratie (of configureren via de wizard setup).</span><span class="sxs-lookup"><span data-stu-id="b4415-131">Do not use this tool to assess performance and network settings on a device before the registration (or configuring via setup wizard).</span></span> <span data-ttu-id="b4415-132">Een geldig IP-adres is toegewezen aan het apparaat tijdens de wizard setup en registratie.</span><span class="sxs-lookup"><span data-stu-id="b4415-132">A valid IP is assigned to the device during setup wizard and registration.</span></span> <span data-ttu-id="b4415-133">U kunt deze cmdlet uitvoeren op een apparaat dat niet is geregistreerd voor de status van de hardware- en systeem.</span><span class="sxs-lookup"><span data-stu-id="b4415-133">You can run this cmdlet, on a device that is not registered, for hardware health and system.</span></span> <span data-ttu-id="b4415-134">Gebruik bijvoorbeeld de bereikparameter:</span><span class="sxs-lookup"><span data-stu-id="b4415-134">Use the scope parameter, for example:</span></span>
         >
         > `Invoke-HcsDiagnostics -Scope Hardware`
         >
         > `Invoke-HcsDiagnostics -Scope System`

* <span data-ttu-id="b4415-135">**Problemen met de permanente apparaat** -u ondervindt problemen met apparaten die goed lijken te behouden.</span><span class="sxs-lookup"><span data-stu-id="b4415-135">**Persistent device issues** - You are experiencing device issues that seem to persist.</span></span> <span data-ttu-id="b4415-136">Bijvoorbeeld, de registratie is mislukt.</span><span class="sxs-lookup"><span data-stu-id="b4415-136">For instance, registration is failing.</span></span> <span data-ttu-id="b4415-137">U kan ook worden ondervindt problemen met apparaat nadat het apparaat is geregistreerd en operationeel een tijdje is.</span><span class="sxs-lookup"><span data-stu-id="b4415-137">You could also be experiencing device issues after the device is successfully registered and operational for a while.</span></span>
    * <span data-ttu-id="b4415-138">In dit geval moet u dit hulpprogramma gebruiken voor voorlopige probleemoplossing voordat u zich een serviceaanvraag met Microsoft Support aanmeldt.</span><span class="sxs-lookup"><span data-stu-id="b4415-138">In this case, use this tool for preliminary troubleshooting before you log a service request with Microsoft Support.</span></span> <span data-ttu-id="b4415-139">U wordt aangeraden dat u dit hulpprogramma uitvoeren en vastleggen van de uitvoer van dit hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="b4415-139">We recommend that you run this tool and capture the output of this tool.</span></span> <span data-ttu-id="b4415-140">U kunt vervolgens deze uitvoer bieden ondersteuning voor snellere het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="b4415-140">You can then provide this output to Support to expedite troubleshooting.</span></span>
    * <span data-ttu-id="b4415-141">Als er een onderdeel of het cluster hardwarefouten, moet u een ondersteuningsaanvraag aanmelden.</span><span class="sxs-lookup"><span data-stu-id="b4415-141">If there are any hardware component or cluster failures, you should log in a Support request.</span></span>

* <span data-ttu-id="b4415-142">**Lage Apparaatprestaties** -uw StorSimple-apparaat traag is.</span><span class="sxs-lookup"><span data-stu-id="b4415-142">**Low device performance** - Your StorSimple device is slow.</span></span>
    * <span data-ttu-id="b4415-143">In dit geval moet u deze cmdlet uitvoeren met bereikparameter ingesteld op prestaties.</span><span class="sxs-lookup"><span data-stu-id="b4415-143">In this case, run this cmdlet with scope parameter set to performance.</span></span> <span data-ttu-id="b4415-144">Analyseer de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="b4415-144">Analyze the output.</span></span> <span data-ttu-id="b4415-145">Krijgt u de cloud lezen-schrijven latenties.</span><span class="sxs-lookup"><span data-stu-id="b4415-145">You get the cloud read-write latencies.</span></span> <span data-ttu-id="b4415-146">De gerapporteerde latenties gebruiken als het doel van maximale haalbare, rekening te houden in enige overhead voor het verwerken van de interne gegevens en vervolgens implementeert u de werkbelasting op het systeem.</span><span class="sxs-lookup"><span data-stu-id="b4415-146">Use the reported latencies as maximum achievable target, factor in some overhead for the internal data processing, and then deploy the workloads on the system.</span></span> <span data-ttu-id="b4415-147">Ga voor meer informatie naar [de Netwerktest gebruiken om op te lossen Apparaatprestaties](#network-test).</span><span class="sxs-lookup"><span data-stu-id="b4415-147">For more information, go to [Use the network test to troubleshoot device performance](#network-test).</span></span>


## <a name="diagnostics-test-and-sample-outputs"></a><span data-ttu-id="b4415-148">Diagnostische test en voorbeeld-uitvoer</span><span class="sxs-lookup"><span data-stu-id="b4415-148">Diagnostics test and sample outputs</span></span>

### <a name="hardware-test"></a><span data-ttu-id="b4415-149">Hardwaretest</span><span class="sxs-lookup"><span data-stu-id="b4415-149">Hardware test</span></span>

<span data-ttu-id="b4415-150">Deze test bepaalt de status van de hardware-onderdelen, het USM firmware en de firmware van de schijf op het systeem uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b4415-150">This test determines the status of the hardware components, the USM firmware, and the disk firmware running on your system.</span></span>

* <span data-ttu-id="b4415-151">De hardwareonderdelen die zijn gerapporteerd, zijn deze onderdelen die de test mislukt of zijn niet aanwezig in het systeem.</span><span class="sxs-lookup"><span data-stu-id="b4415-151">The hardware components reported are those components that failed the test or are not present in the system.</span></span>
* <span data-ttu-id="b4415-152">De USM firmware- en firmware-versies worden gerapporteerd voor de Controller 0, 1 van de domeincontroller, en gedeelde onderdelen in uw systeem.</span><span class="sxs-lookup"><span data-stu-id="b4415-152">The USM firmware and disk firmware versions are reported for the Controller 0, Controller 1, and shared components in your system.</span></span> <span data-ttu-id="b4415-153">Voor een volledige lijst van hardware-onderdelen, gaat u naar:</span><span class="sxs-lookup"><span data-stu-id="b4415-153">For a complete list of hardware components, go to:</span></span>

    * [<span data-ttu-id="b4415-154">Primaire behuizing-onderdelen</span><span class="sxs-lookup"><span data-stu-id="b4415-154">Components in primary enclosure</span></span>](storsimple-monitor-hardware-status.md#component-list-for-primary-enclosure-of-storsimple-device)
    * [<span data-ttu-id="b4415-155">EBOD behuizing-onderdelen</span><span class="sxs-lookup"><span data-stu-id="b4415-155">Components in EBOD enclosure</span></span>](storsimple-monitor-hardware-status.md#component-list-for-ebod-enclosure-of-storsimple-device)

> [!NOTE]
> <span data-ttu-id="b4415-156">Als de hardwaretest niet functionerende onderdelen, rapporteert [Meld u bij een serviceaanvraag met Microsoft Support](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="b4415-156">If the hardware test reports failed components, [log in a service request with Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>

#### <a name="sample-output-of-hardware-test-run-on-an-8100-device"></a><span data-ttu-id="b4415-157">Voorbeeld van uitvoer van de hardwaretest uitgevoerd op een 8100-apparaat</span><span class="sxs-lookup"><span data-stu-id="b4415-157">Sample output of hardware test run on an 8100 device</span></span>

<span data-ttu-id="b4415-158">Hier volgt een voorbeeld van uitvoer van een StorSimple 8100-apparaat.</span><span class="sxs-lookup"><span data-stu-id="b4415-158">Here is a sample output from a StorSimple 8100 device.</span></span> <span data-ttu-id="b4415-159">De behuizing EBOD is niet aanwezig in het model 8100-apparaat.</span><span class="sxs-lookup"><span data-stu-id="b4415-159">In the 8100 model device, the EBOD enclosure is not present.</span></span> <span data-ttu-id="b4415-160">Daarom worden de onderdelen van de domeincontroller EBOD niet gemeld.</span><span class="sxs-lookup"><span data-stu-id="b4415-160">Hence, the EBOD controller components are not reported.</span></span>

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

### <a name="system-test"></a><span data-ttu-id="b4415-161">Systeem-test</span><span class="sxs-lookup"><span data-stu-id="b4415-161">System test</span></span>

<span data-ttu-id="b4415-162">Deze test rapporteert de systeeminformatie, de updates die beschikbaar zijn, de clustergegevens en de gegevens van de service voor uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="b4415-162">This test reports the system information, the updates available, the cluster information, and the service information for your device.</span></span>

* <span data-ttu-id="b4415-163">De systeeminformatie omvat het model, apparaatserienummer tijdzone, status van de domeincontroller en de versie van de gedetailleerde software op het systeem.</span><span class="sxs-lookup"><span data-stu-id="b4415-163">The system information includes the model, device serial number, time zone, controller status, and the detailed software version running on the system.</span></span> <span data-ttu-id="b4415-164">Voor informatie over de verschillende parameters voor het gerapporteerd als de uitvoer, gaat u naar [systeemgegevens interpreteren](#appendix-interpreting-system-information).</span><span class="sxs-lookup"><span data-stu-id="b4415-164">To understand the various system parameters reported as the output, go to [Interpreting system information](#appendix-interpreting-system-information).</span></span>

* <span data-ttu-id="b4415-165">De beschikbaarheid van de rapporten of de reguliere en onderhoud modi beschikbaar zijn en de namen van de bijbehorende pakket.</span><span class="sxs-lookup"><span data-stu-id="b4415-165">The update availability reports whether the regular and maintenance modes are available and their associated package names.</span></span> <span data-ttu-id="b4415-166">Als `RegularUpdates` en `MaintenanceModeUpdates` zijn `false`, dit geeft aan dat de updates niet beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="b4415-166">If `RegularUpdates` and `MaintenanceModeUpdates` are `false`, this indicates that the updates are not available.</span></span> <span data-ttu-id="b4415-167">Uw apparaat is bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="b4415-167">Your device is up-to-date.</span></span>
* <span data-ttu-id="b4415-168">De cluster-informatie bevat de informatie over de verschillende logische onderdelen van de groepen voor de cluster HCS en hun respectieve statussen.</span><span class="sxs-lookup"><span data-stu-id="b4415-168">The cluster information contains the information on various logical components of all the HCS cluster groups and their respective statuses.</span></span> <span data-ttu-id="b4415-169">Als u een offline clustergroep in deze sectie van het rapport ziet [contact op met Microsoft Support](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="b4415-169">If you see an offline cluster group in this section of the report, [contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>
* <span data-ttu-id="b4415-170">De service-informatie bevat de namen en de status van alle HCS en CiS services uitgevoerd op uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="b4415-170">The service information includes the names and statuses of all the HCS and CiS services running on your device.</span></span> <span data-ttu-id="b4415-171">Deze informatie is nuttig voor het Microsoft Support bij het oplossen van het probleem van het apparaat.</span><span class="sxs-lookup"><span data-stu-id="b4415-171">This information is helpful for the Microsoft Support in troubleshooting the device issue.</span></span>

#### <a name="sample-output-of-system-test-run-on-an-8100-device"></a><span data-ttu-id="b4415-172">Voorbeeld van uitvoer van systeem test uitgevoerd op een 8100-apparaat</span><span class="sxs-lookup"><span data-stu-id="b4415-172">Sample output of system test run on an 8100 device</span></span>

<span data-ttu-id="b4415-173">Hier volgt een voorbeeld van uitvoer van de systeem-test uitvoeren op een 8100-apparaat.</span><span class="sxs-lookup"><span data-stu-id="b4415-173">Here is a sample output of the system test run on an 8100 device.</span></span>

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

### <a name="network-test"></a><span data-ttu-id="b4415-174">Netwerktest</span><span class="sxs-lookup"><span data-stu-id="b4415-174">Network test</span></span>

<span data-ttu-id="b4415-175">Deze test controleert de status van de netwerkinterfaces, poorten, DNS- en NTP serververbindingen, SSL-certificaat, opslagaccountreferenties, verbinding met de Update-servers en web proxy connectiviteit op uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="b4415-175">This test validates the status of the network interfaces, ports, DNS and NTP server connectivity, SSL certificate, storage account credentials, connectivity to the Update servers, and web proxy connectivity on your StorSimple device.</span></span>

#### <a name="sample-output-of-network-test-when-only-data0-is-enabled"></a><span data-ttu-id="b4415-176">Voorbeeld van uitvoer van het netwerk testen wanneer alleen DATA0 is ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="b4415-176">Sample output of network test when only DATA0 is enabled</span></span>

<span data-ttu-id="b4415-177">Hier volgt een voorbeeld van uitvoer van het 8100-apparaat.</span><span class="sxs-lookup"><span data-stu-id="b4415-177">Here is a sample output of the 8100 device.</span></span> <span data-ttu-id="b4415-178">U kunt zien in de uitvoer die:</span><span class="sxs-lookup"><span data-stu-id="b4415-178">You can see in the output that:</span></span>
* <span data-ttu-id="b4415-179">Alleen DATA 0 en 1 gegevens netwerkinterfaces zijn ingeschakeld en geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="b4415-179">Only DATA 0 and DATA 1 network interfaces are enabled and configured.</span></span>
* <span data-ttu-id="b4415-180">GEGEVENS-2-5 zijn niet ingeschakeld in de portal.</span><span class="sxs-lookup"><span data-stu-id="b4415-180">DATA 2 - 5 are not enabled in the portal.</span></span>
* <span data-ttu-id="b4415-181">De configuratie van DNS-server is geldig en het apparaat verbinding kan maken via de DNS-server.</span><span class="sxs-lookup"><span data-stu-id="b4415-181">The DNS server configuration is valid and the device can connect via the DNS server.</span></span>
* <span data-ttu-id="b4415-182">De connectiviteit NTP-server is ook geen probleem.</span><span class="sxs-lookup"><span data-stu-id="b4415-182">The NTP server connectivity is also fine.</span></span>
* <span data-ttu-id="b4415-183">Poorten 80 en 443 zijn geopend.</span><span class="sxs-lookup"><span data-stu-id="b4415-183">Ports 80 and 443 are open.</span></span> <span data-ttu-id="b4415-184">Poort 9354 is geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="b4415-184">However, port 9354 is blocked.</span></span> <span data-ttu-id="b4415-185">Op basis van de [netwerk systeemvereisten](storsimple-system-requirements.md), moet u deze poort voor de service bus-communicatie te openen.</span><span class="sxs-lookup"><span data-stu-id="b4415-185">Based on the [system network requirements](storsimple-system-requirements.md), you need to open this port for the service bus communication.</span></span>
* <span data-ttu-id="b4415-186">Het SSL-certificaat is ongeldig.</span><span class="sxs-lookup"><span data-stu-id="b4415-186">The SSL certification is valid.</span></span>
* <span data-ttu-id="b4415-187">Het apparaat verbinding kan maken met de opslagaccount: _myss8000storageacct_.</span><span class="sxs-lookup"><span data-stu-id="b4415-187">The device can connect to the storage account: _myss8000storageacct_.</span></span>
* <span data-ttu-id="b4415-188">De verbinding met de Update-servers is ongeldig.</span><span class="sxs-lookup"><span data-stu-id="b4415-188">The connectivity to Update servers is valid.</span></span>
* <span data-ttu-id="b4415-189">De webproxy is niet geconfigureerd op dit apparaat.</span><span class="sxs-lookup"><span data-stu-id="b4415-189">The web proxy is not configured on this device.</span></span>

#### <a name="sample-output-of-network-test-when-data0-and-data1-are-enabled"></a><span data-ttu-id="b4415-190">Voorbeeld van uitvoer van Netwerktest wanneer DATA0 en bestand1 zijn ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="b4415-190">Sample output of network test when DATA0 and DATA1 are enabled</span></span>

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

### <a name="performance-test"></a><span data-ttu-id="b4415-191">Prestatietest</span><span class="sxs-lookup"><span data-stu-id="b4415-191">Performance test</span></span>

<span data-ttu-id="b4415-192">Deze test rapporteert de prestaties van de cloud via de cloud lezen-schrijven latenties voor uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="b4415-192">This test reports the cloud performance via the cloud read-write latencies for your device.</span></span> <span data-ttu-id="b4415-193">Dit hulpprogramma kan worden gebruikt om een basislijn voor de prestaties van de cloud die u met StorSimple bereiken kunt stand te brengen.</span><span class="sxs-lookup"><span data-stu-id="b4415-193">This tool can be used to establish a baseline of the cloud performance that you can achieve with StorSimple.</span></span> <span data-ttu-id="b4415-194">Het hulpprogramma rapporteert de maximale prestaties (beste scenario voor lezen-schrijven latenties) die u voor de verbinding ophalen kunt.</span><span class="sxs-lookup"><span data-stu-id="b4415-194">The tool reports the maximum performance (best case scenario for read-write latencies) that you can get for your connection.</span></span>

<span data-ttu-id="b4415-195">Als het hulpprogramma de maximale haalbare prestaties meldt, kunnen we de gerapporteerde latenties voor lezen-schrijven gebruiken als doelen bij het implementeren van de werkbelastingen.</span><span class="sxs-lookup"><span data-stu-id="b4415-195">As the tool reports the maximum achievable performance, we can use the reported read-write latencies as targets when deploying the workloads.</span></span>

<span data-ttu-id="b4415-196">De test simuleert de grootte van de blob die is gekoppeld aan de typen ander volume op het apparaat.</span><span class="sxs-lookup"><span data-stu-id="b4415-196">The test simulates the blob sizes associated with the different volume types on the device.</span></span> <span data-ttu-id="b4415-197">Gewone lagen en back-ups van lokaal vastgemaakte volumes met een blob-grootte van 64 KB.</span><span class="sxs-lookup"><span data-stu-id="b4415-197">Regular tiered and backups of locally pinned volumes use a 64 KB blob size.</span></span> <span data-ttu-id="b4415-198">Gelaagde volumes met archief-optie ingeschakeld gebruiken blob-gegevensgrootte 512 KB.</span><span class="sxs-lookup"><span data-stu-id="b4415-198">Tiered volumes with archive option checked use 512 KB blob data size.</span></span> <span data-ttu-id="b4415-199">Als het apparaat heeft gelaagde en lokaal vastgemaakte volumes geconfigureerd, alleen de test die overeenkomt met de blob van 64 KB gegevensgrootte wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b4415-199">If your device has tiered and locally pinned volumes configured, only the test corresponding to 64 KB blob data size is run.</span></span>

<span data-ttu-id="b4415-200">Om dit hulpprogramma, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="b4415-200">To use this tool, perform the following steps:</span></span>

1.  <span data-ttu-id="b4415-201">Maak eerst een combinatie van gelaagde volumes en gelaagde volumes met gearchiveerde optie ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="b4415-201">First, create a mix of tiered volumes and tiered volumes with archived option checked.</span></span> <span data-ttu-id="b4415-202">Deze actie zorgt ervoor dat het hulpprogramma voor de tests voor 64 KB en 512 KB grootten van de blob.</span><span class="sxs-lookup"><span data-stu-id="b4415-202">This action ensures that the tool runs the tests for both 64 KB and 512 KB blob sizes.</span></span>

2. <span data-ttu-id="b4415-203">De cmdlet uitvoeren nadat u hebt gemaakt en de volumes geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="b4415-203">Run the cmdlet after you have created and configured the volumes.</span></span> <span data-ttu-id="b4415-204">Type:</span><span class="sxs-lookup"><span data-stu-id="b4415-204">Type:</span></span>

    `Invoke-HcsDiagnostics -Scope Performance`

3. <span data-ttu-id="b4415-205">Noteer de latenties lezen-schrijven is gemeld door het hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="b4415-205">Make a note of the read-write latencies reported by the tool.</span></span> <span data-ttu-id="b4415-206">Deze test kan enige tijd duren om uit te voeren voordat het rapporteert de resultaten.</span><span class="sxs-lookup"><span data-stu-id="b4415-206">This test can take several minutes to run before it reports the results.</span></span>

4. <span data-ttu-id="b4415-207">Als de verbinding latenties allemaal onder het verwachte bereik zijn, kunnen klikt u vervolgens de latenties gemeld door het hulpprogramma worden gebruikt als maximale haalbare doel bij het implementeren van de werkbelastingen.</span><span class="sxs-lookup"><span data-stu-id="b4415-207">If the connection latencies are all under the expected range, then the latencies reported by the tool can be used as maximum achievable target when deploying the workloads.</span></span> <span data-ttu-id="b4415-208">Rekening te houden in enige overhead voor interne gegevensverwerking.</span><span class="sxs-lookup"><span data-stu-id="b4415-208">Factor in some overhead for internal data processing.</span></span>

    <span data-ttu-id="b4415-209">Als de latenties lezen-schrijven is gemeld door het diagnostisch hulpprogramma hoog zijn:</span><span class="sxs-lookup"><span data-stu-id="b4415-209">If the read-write latencies reported by the diagnostics tool are high:</span></span>

    1. <span data-ttu-id="b4415-210">Storage Analytics voor blob-services configureren en analyseren van de uitvoer voor inzicht in de latenties voor de Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="b4415-210">Configure Storage Analytics for blob services and analyze the output to understand the latencies for the Azure storage account.</span></span> <span data-ttu-id="b4415-211">Ga voor gedetailleerde instructies naar [inschakelen en configureren van opslag Analytics](../storage/common/storage-enable-and-view-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="b4415-211">For detailed instructions, go to [enable and configure Storage Analytics](../storage/common/storage-enable-and-view-metrics.md).</span></span> <span data-ttu-id="b4415-212">Als deze latenties ook hoge en vergelijkbaar is met de getallen die u hebt ontvangen van het hulpprogramma StorSimple diagnostische gegevens, moet u een serviceaanvraag registreren met Azure storage.</span><span class="sxs-lookup"><span data-stu-id="b4415-212">If those latencies are also high and comparable to the numbers you received from the StorSimple Diagnostics tool, then you need to log a service request with Azure storage.</span></span>

    2. <span data-ttu-id="b4415-213">De storage-account latenties lage neemt contact op met de netwerkbeheerder om te onderzoeken latentieproblemen in uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="b4415-213">If the storage account latencies are low, contact your network administrator to investigate any latency issues in your network.</span></span>

#### <a name="sample-output-of-performance-test-run-on-an-8100-device"></a><span data-ttu-id="b4415-214">Voorbeeld van uitvoer van de prestatietest uitvoeren op een 8100-apparaat</span><span class="sxs-lookup"><span data-stu-id="b4415-214">Sample output of performance test run on an 8100 device</span></span>

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

## <a name="appendix-interpreting-system-information"></a><span data-ttu-id="b4415-215">Bijlage: systeemgegevens interpreteren</span><span class="sxs-lookup"><span data-stu-id="b4415-215">Appendix: interpreting system information</span></span>

<span data-ttu-id="b4415-216">Hier volgt een tabel met een beschrijving van wat de verschillende Windows PowerShell-parameters in het systeem informatie toegewezen aan.</span><span class="sxs-lookup"><span data-stu-id="b4415-216">Here is a table describing what the various Windows PowerShell parameters in the system information map to.</span></span> 

| <span data-ttu-id="b4415-217">PowerShell-Parameter</span><span class="sxs-lookup"><span data-stu-id="b4415-217">PowerShell Parameter</span></span>    | <span data-ttu-id="b4415-218">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b4415-218">Description</span></span>  |
|-------------------------|------------------|
| <span data-ttu-id="b4415-219">Exemplaar-id</span><span class="sxs-lookup"><span data-stu-id="b4415-219">Instance ID</span></span>             | <span data-ttu-id="b4415-220">Elke domeincontroller heeft een unieke id of een GUID die is gekoppeld aan.</span><span class="sxs-lookup"><span data-stu-id="b4415-220">Every controller has a unique identifier or a GUID associated with it.</span></span>|
| <span data-ttu-id="b4415-221">Naam</span><span class="sxs-lookup"><span data-stu-id="b4415-221">Name</span></span>                    | <span data-ttu-id="b4415-222">De beschrijvende naam van het apparaat zoals geconfigureerd via de Azure portal tijdens de implementatie van het apparaat.</span><span class="sxs-lookup"><span data-stu-id="b4415-222">The friendly name of the device as configured through the Azure portal during device deployment.</span></span> <span data-ttu-id="b4415-223">De beschrijvende naam van de standaard is het serienummer van het apparaat.</span><span class="sxs-lookup"><span data-stu-id="b4415-223">The default friendly name is the device serial number.</span></span> |
| <span data-ttu-id="b4415-224">Model</span><span class="sxs-lookup"><span data-stu-id="b4415-224">Model</span></span>                   | <span data-ttu-id="b4415-225">Het model van uw StorSimple 8000 serie-apparaat.</span><span class="sxs-lookup"><span data-stu-id="b4415-225">The model of your StorSimple 8000 series device.</span></span> <span data-ttu-id="b4415-226">Het model is 8100 of 8600.</span><span class="sxs-lookup"><span data-stu-id="b4415-226">The model can be 8100 or 8600.</span></span>|
| <span data-ttu-id="b4415-227">Serienummer</span><span class="sxs-lookup"><span data-stu-id="b4415-227">SerialNumber</span></span>            | <span data-ttu-id="b4415-228">Het serienummer van het apparaat in de fabriek is toegewezen en 15 tekens lang is.</span><span class="sxs-lookup"><span data-stu-id="b4415-228">The device serial number is assigned at the factory and is 15 characters long.</span></span> <span data-ttu-id="b4415-229">Bijvoorbeeld: 8600 SHX0991003G44HT Hiermee wordt aangegeven:</span><span class="sxs-lookup"><span data-stu-id="b4415-229">For instance, 8600-SHX0991003G44HT indicates:</span></span><br> <span data-ttu-id="b4415-230">8600 – is het model.</span><span class="sxs-lookup"><span data-stu-id="b4415-230">8600 – Is the device model.</span></span><br><span data-ttu-id="b4415-231">SHX – Is de productie-site.</span><span class="sxs-lookup"><span data-stu-id="b4415-231">SHX – Is the manufacturing site.</span></span><br> <span data-ttu-id="b4415-232">0991003 - is een specifiek product.</span><span class="sxs-lookup"><span data-stu-id="b4415-232">0991003 - Is a specific product.</span></span> <br> <span data-ttu-id="b4415-233">G44HT--de laatste 5 cijfers voor het maken van unieke serienummers worden verhoogd.</span><span class="sxs-lookup"><span data-stu-id="b4415-233">G44HT- the last 5 digits are incremented to create unique serial numbers.</span></span> <span data-ttu-id="b4415-234">Dit kan niet een sequentiële set zijn.</span><span class="sxs-lookup"><span data-stu-id="b4415-234">This may not be a sequential set.</span></span>|
| <span data-ttu-id="b4415-235">Tijdzone</span><span class="sxs-lookup"><span data-stu-id="b4415-235">TimeZone</span></span>                | <span data-ttu-id="b4415-236">De apparaat-tijdzone zoals geconfigureerd in de Azure-portal tijdens de implementatie van het apparaat.</span><span class="sxs-lookup"><span data-stu-id="b4415-236">The device time zone as configured in the Azure portal during device deployment.</span></span>|
| <span data-ttu-id="b4415-237">CurrentController</span><span class="sxs-lookup"><span data-stu-id="b4415-237">CurrentController</span></span>       | <span data-ttu-id="b4415-238">De controller waaraan u via de Windows PowerShell-interface van uw StorSimple-apparaat verbonden bent.</span><span class="sxs-lookup"><span data-stu-id="b4415-238">The controller that you are connected to through the Windows PowerShell interface of your StorSimple device.</span></span>|
| <span data-ttu-id="b4415-239">ActiveController</span><span class="sxs-lookup"><span data-stu-id="b4415-239">ActiveController</span></span>        | <span data-ttu-id="b4415-240">De domeincontroller die actief is op uw apparaat en alle bewerkingen van de netwerk- en beheerd.</span><span class="sxs-lookup"><span data-stu-id="b4415-240">The controller that is active on your device and is controlling all the network and disk operations.</span></span> <span data-ttu-id="b4415-241">Dit kan zijn Controller 0 of 1 van de domeincontroller.</span><span class="sxs-lookup"><span data-stu-id="b4415-241">This can be Controller 0 or Controller 1.</span></span>  |
| <span data-ttu-id="b4415-242">Controller0Status</span><span class="sxs-lookup"><span data-stu-id="b4415-242">Controller0Status</span></span>       | <span data-ttu-id="b4415-243">De status van de Controller 0 op uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="b4415-243">The status of Controller 0 on your device.</span></span> <span data-ttu-id="b4415-244">De status van de domeincontroller kan normale in herstelmodus is of niet bereikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="b4415-244">The controller status can be normal, in recovery mode, or unreachable.</span></span>|
| <span data-ttu-id="b4415-245">Controller1Status</span><span class="sxs-lookup"><span data-stu-id="b4415-245">Controller1Status</span></span>       | <span data-ttu-id="b4415-246">De status van de Controller 1 op uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="b4415-246">The status of Controller 1 on your device.</span></span>  <span data-ttu-id="b4415-247">De status van de domeincontroller kan normale in herstelmodus is of niet bereikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="b4415-247">The controller status can be normal, in recovery mode, or unreachable.</span></span>|
| <span data-ttu-id="b4415-248">SystemMode</span><span class="sxs-lookup"><span data-stu-id="b4415-248">SystemMode</span></span>              | <span data-ttu-id="b4415-249">De algehele status van uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="b4415-249">The overall status of your StorSimple device.</span></span> <span data-ttu-id="b4415-250">Status van het apparaat kan worden normaal, onderhoud, of buiten gebruik gestelde (komt overeen met gedeactiveerd in de Azure portal).</span><span class="sxs-lookup"><span data-stu-id="b4415-250">The device status can be normal, maintenance, or decommissioned (corresponds to deactivated in the Azure portal).</span></span>|
| <span data-ttu-id="b4415-251">FriendlySoftwareVersion</span><span class="sxs-lookup"><span data-stu-id="b4415-251">FriendlySoftwareVersion</span></span> | <span data-ttu-id="b4415-252">De beschrijvende tekenreeks die overeenkomt met de versie van de software apparaat.</span><span class="sxs-lookup"><span data-stu-id="b4415-252">The friendly string that corresponds to the device software version.</span></span> <span data-ttu-id="b4415-253">Voor een systeem met Update 4, is de beschrijvende softwareversie StorSimple 8000 Series Update 4.0.</span><span class="sxs-lookup"><span data-stu-id="b4415-253">For a system running Update 4, the friendly software version would be StorSimple 8000 Series Update 4.0.</span></span>|
| <span data-ttu-id="b4415-254">HcsSoftwareVersion</span><span class="sxs-lookup"><span data-stu-id="b4415-254">HcsSoftwareVersion</span></span>      | <span data-ttu-id="b4415-255">De versie van de HCS software is uitgevoerd op uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="b4415-255">The HCS software version running on your device.</span></span> <span data-ttu-id="b4415-256">Bijvoorbeeld, wordt de softwareversie HCS die overeenkomt met de StorSimple 8000 Series Update 4.0 6.3.9600.17820.</span><span class="sxs-lookup"><span data-stu-id="b4415-256">For instance, the HCS software version corresponding to StorSimple 8000 Series Update 4.0 is 6.3.9600.17820.</span></span> |
| <span data-ttu-id="b4415-257">ApiVersion</span><span class="sxs-lookup"><span data-stu-id="b4415-257">ApiVersion</span></span>              | <span data-ttu-id="b4415-258">De softwareversie van de Windows PowerShell-API van het apparaat HCS.</span><span class="sxs-lookup"><span data-stu-id="b4415-258">The software version of the Windows PowerShell API of the HCS device.</span></span>|
| <span data-ttu-id="b4415-259">VhdVersion</span><span class="sxs-lookup"><span data-stu-id="b4415-259">VhdVersion</span></span>              | <span data-ttu-id="b4415-260">De softwareversie van de factory-installatiekopie die met het apparaat is verzonden.</span><span class="sxs-lookup"><span data-stu-id="b4415-260">The software version of the factory image that the device was shipped with.</span></span> <span data-ttu-id="b4415-261">Als u uw apparaat opnieuw op de standaardwaarden, voert deze de softwareversie van deze.</span><span class="sxs-lookup"><span data-stu-id="b4415-261">If you reset your device to factory defaults, then it runs this software version.</span></span>|
| <span data-ttu-id="b4415-262">OSVersion</span><span class="sxs-lookup"><span data-stu-id="b4415-262">OSVersion</span></span>               | <span data-ttu-id="b4415-263">De softwareversie van het besturingssysteem Windows Server wordt uitgevoerd op het apparaat.</span><span class="sxs-lookup"><span data-stu-id="b4415-263">The software version of the Windows Server operating system running on the device.</span></span> <span data-ttu-id="b4415-264">Het StorSimple-apparaat is gebaseerd op Windows Server 2012 R2 die overeenkomt met 6.3.9600.</span><span class="sxs-lookup"><span data-stu-id="b4415-264">The StorSimple device is based off the Windows Server 2012 R2 that corresponds to 6.3.9600.</span></span>|
| <span data-ttu-id="b4415-265">CisAgentVersion</span><span class="sxs-lookup"><span data-stu-id="b4415-265">CisAgentVersion</span></span>         | <span data-ttu-id="b4415-266">De versie voor uw configuratie-items agent wordt uitgevoerd op uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="b4415-266">The version for your Cis agent running on your StorSimple device.</span></span> <span data-ttu-id="b4415-267">Deze agent kan communiceren met de StorSimple Manager-service worden uitgevoerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="b4415-267">This agent helps communicate with the StorSimple Manager service running in Azure.</span></span>|
| <span data-ttu-id="b4415-268">MdsAgentVersion</span><span class="sxs-lookup"><span data-stu-id="b4415-268">MdsAgentVersion</span></span>         | <span data-ttu-id="b4415-269">De versie die overeenkomt met de Mds-agent uitgevoerd op uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="b4415-269">The version corresponding to the Mds agent running on your StorSimple device.</span></span> <span data-ttu-id="b4415-270">Deze agent verplaatst gegevens naar de controle en diagnostische gegevens Service (MDS).</span><span class="sxs-lookup"><span data-stu-id="b4415-270">This agent moves data to the Monitoring and Diagnostics Service (MDS).</span></span>|
| <span data-ttu-id="b4415-271">Lsisas2Version</span><span class="sxs-lookup"><span data-stu-id="b4415-271">Lsisas2Version</span></span>          | <span data-ttu-id="b4415-272">De versie die overeenkomt met de LSI stuurprogramma's op uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="b4415-272">The version corresponding to the LSI drivers on your StorSimple device.</span></span>|
| <span data-ttu-id="b4415-273">Capaciteit</span><span class="sxs-lookup"><span data-stu-id="b4415-273">Capacity</span></span>                | <span data-ttu-id="b4415-274">De totale capaciteit van het apparaat in bytes.</span><span class="sxs-lookup"><span data-stu-id="b4415-274">The total capacity of the device in bytes.</span></span>|
| <span data-ttu-id="b4415-275">RemoteManagementMode</span><span class="sxs-lookup"><span data-stu-id="b4415-275">RemoteManagementMode</span></span>    | <span data-ttu-id="b4415-276">Hiermee wordt aangegeven of het apparaat kan extern worden beheerd via de Windows PowerShell-interface.</span><span class="sxs-lookup"><span data-stu-id="b4415-276">Indicates whether the device can be remotely managed via its Windows PowerShell interface.</span></span> |
| <span data-ttu-id="b4415-277">FipsMode</span><span class="sxs-lookup"><span data-stu-id="b4415-277">FipsMode</span></span>                | <span data-ttu-id="b4415-278">Hiermee wordt aangegeven of de Verenigde Staten Federal Information Processing Standard (FIPS)-modus is ingeschakeld op uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="b4415-278">Indicates whether the United States Federal Information Processing Standard (FIPS) mode is enabled on your device.</span></span> <span data-ttu-id="b4415-279">De FIPS 140-standaard definieert cryptografische algoritmen die zijn goedgekeurd voor gebruik door ons Federal government computersystemen voor de bescherming van gevoelige gegevens.</span><span class="sxs-lookup"><span data-stu-id="b4415-279">The FIPS 140 standard defines cryptographic algorithms approved for use by US Federal government computer systems for the protection of sensitive data.</span></span> <span data-ttu-id="b4415-280">FIPS-modus is standaard ingeschakeld voor apparaten met Update 4 of hoger is.</span><span class="sxs-lookup"><span data-stu-id="b4415-280">For devices running Update 4 or later, FIPS mode is enabled by default.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b4415-281">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b4415-281">Next steps</span></span>

* <span data-ttu-id="b4415-282">Meer informatie over de [syntaxis van de cmdlet Invoke-HcsDiagnostics](https://technet.microsoft.com/library/mt795371.aspx).</span><span class="sxs-lookup"><span data-stu-id="b4415-282">Learn the [syntax of the Invoke-HcsDiagnostics cmdlet](https://technet.microsoft.com/library/mt795371.aspx).</span></span>

* <span data-ttu-id="b4415-283">Meer informatie over het [implementatieproblemen oplossen](storsimple-troubleshoot-deployment.md) op uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="b4415-283">Learn more about how to [troubleshoot deployment issues](storsimple-troubleshoot-deployment.md) on your StorSimple device.</span></span>
