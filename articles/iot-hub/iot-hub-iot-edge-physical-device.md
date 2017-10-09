---
title: een fysiek apparaat met Azure IoT rand aaaUse | Microsoft Docs
description: Hoe toouse een Texas instrumenten SensorTag apparaat toosend tooan iothub via een IoT Edge gateway uitgevoerd op een apparaat frambozen Pi 3. Hallo-gateway is gebouwd met behulp van Azure IoT rand.
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: 212dacbf-e5e9-48b2-9c8a-1c14d9e7b913
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: andbuc
ms.openlocfilehash: a2385accdbd99012ad094232653ee47d4e5c7839
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-iot-edge-on-a-raspberry-pi-tooforward-device-to-cloud-messages-tooiot-hub"></a><span data-ttu-id="a5a09-104">Gebruik Azure IoT-Edge van een frambozen Pi tooforward apparaat-naar-cloudberichten tooIoT Hub</span><span class="sxs-lookup"><span data-stu-id="a5a09-104">Use Azure IoT Edge on a Raspberry Pi tooforward device-to-cloud messages tooIoT Hub</span></span>

<span data-ttu-id="a5a09-105">In dit scenario Hallo [Bluetooth lage energie voorbeeld] [ lnk-ble-samplecode] laat u zien hoe toouse [Azure IoT rand] [ lnk-sdk] naar:</span><span class="sxs-lookup"><span data-stu-id="a5a09-105">This walkthrough of hello [Bluetooth low energy sample][lnk-ble-samplecode] shows you how toouse [Azure IoT Edge][lnk-sdk] to:</span></span>

* <span data-ttu-id="a5a09-106">Apparaat-naar-cloud telemetrie tooIoT Hub vanaf een fysiek apparaat doorsturen.</span><span class="sxs-lookup"><span data-stu-id="a5a09-106">Forward device-to-cloud telemetry tooIoT Hub from a physical device.</span></span>
* <span data-ttu-id="a5a09-107">Route-opdrachten van IoT Hub tooa fysieke apparaat.</span><span class="sxs-lookup"><span data-stu-id="a5a09-107">Route commands from IoT Hub tooa physical device.</span></span>

<span data-ttu-id="a5a09-108">Dit overzicht omvat:</span><span class="sxs-lookup"><span data-stu-id="a5a09-108">This walkthrough covers:</span></span>

* <span data-ttu-id="a5a09-109">**Architectuur**: belangrijke architecturale informatie over Hallo Bluetooth lage energie-voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="a5a09-109">**Architecture**: important architectural information about hello Bluetooth low energy sample.</span></span>
* <span data-ttu-id="a5a09-110">**Bouwen en uitvoeren van**: Hallo stappen vereist toobuild en Voer Hallo-voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="a5a09-110">**Build and run**: hello steps required toobuild and run hello sample.</span></span>

## <a name="architecture"></a><span data-ttu-id="a5a09-111">Architectuur</span><span class="sxs-lookup"><span data-stu-id="a5a09-111">Architecture</span></span>

<span data-ttu-id="a5a09-112">Hallo overzicht toont u hoe toobuild en voer een gateway aan de rand van IoT op een frambozen Pi 3 die wordt uitgevoerd Raspbian Linux.</span><span class="sxs-lookup"><span data-stu-id="a5a09-112">hello walkthrough shows you how toobuild and run an IoT Edge gateway on a Raspberry Pi 3 that runs Raspbian Linux.</span></span> <span data-ttu-id="a5a09-113">Hallo-gateway is gebouwd met behulp van IoT rand.</span><span class="sxs-lookup"><span data-stu-id="a5a09-113">hello gateway is built using IoT Edge.</span></span> <span data-ttu-id="a5a09-114">Hallo-voorbeeld wordt een Texas instrumenten SensorTag Bluetooth laag energieverbruik (uitschakelen) toocollect temperatuur apparaatgegevens gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a5a09-114">hello sample uses a Texas Instruments SensorTag Bluetooth Low Energy (BLE) device toocollect temperature data.</span></span>

<span data-ttu-id="a5a09-115">Wanneer u Hallo rand IoT gateway uitvoert het:</span><span class="sxs-lookup"><span data-stu-id="a5a09-115">When you run hello IoT Edge gateway it:</span></span>

* <span data-ttu-id="a5a09-116">Maakt verbinding tooa SensorTag-apparaten met Hallo Bluetooth laag energieverbruik (uitschakelen)-protocol.</span><span class="sxs-lookup"><span data-stu-id="a5a09-116">Connects tooa SensorTag device using hello Bluetooth Low Energy (BLE) protocol.</span></span>
* <span data-ttu-id="a5a09-117">TooIoT Hub verbinding maakt met behulp van Hallo HTTP-protocol.</span><span class="sxs-lookup"><span data-stu-id="a5a09-117">Connects tooIoT Hub using hello HTTP protocol.</span></span>
* <span data-ttu-id="a5a09-118">Telemetrie verzendt van Hallo SensorTag apparaat tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a5a09-118">Forwards telemetry from hello SensorTag device tooIoT Hub.</span></span>
* <span data-ttu-id="a5a09-119">Opdrachten van IoT Hub toohello SensorTag apparaat gestuurd.</span><span class="sxs-lookup"><span data-stu-id="a5a09-119">Routes commands from IoT Hub toohello SensorTag device.</span></span>

<span data-ttu-id="a5a09-120">Hallo gateway bevat Hallo IoT rand modules te volgen:</span><span class="sxs-lookup"><span data-stu-id="a5a09-120">hello gateway contains hello following IoT Edge modules:</span></span>

* <span data-ttu-id="a5a09-121">Een *uitschakelen module* die met een Aanmeldingsprompt apparaat tooreceive temperatuur gegevens van Hallo-apparaat en verzenden opdrachten toohello apparaat-interfaces.</span><span class="sxs-lookup"><span data-stu-id="a5a09-121">A *BLE module* that interfaces with a BLE device tooreceive temperature data from hello device and send commands toohello device.</span></span>
* <span data-ttu-id="a5a09-122">Een *uitschakelen cloud toodevice module* die JSON berichten uit IoT Hub in uitschakelen instructies voor het Hallo vertaalt *uitschakelen module*.</span><span class="sxs-lookup"><span data-stu-id="a5a09-122">A *BLE cloud toodevice module* that translates JSON messages sent from IoT Hub into BLE instructions for hello *BLE module*.</span></span>
* <span data-ttu-id="a5a09-123">Een *berichtenlogboek module* die alle gateway berichten tooa lokaal bestand registreert.</span><span class="sxs-lookup"><span data-stu-id="a5a09-123">A *logger module* that logs all gateway messages tooa local file.</span></span>
* <span data-ttu-id="a5a09-124">Een *identiteit toewijzing module* die tussen uitschakelen apparaat MAC-adressen en Azure IoT Hub apparaat-id's worden omgezet.</span><span class="sxs-lookup"><span data-stu-id="a5a09-124">An *identity mapping module* that translates between BLE device MAC addresses and Azure IoT Hub device identities.</span></span>
* <span data-ttu-id="a5a09-125">Een *IoT Hub module* die uploadt telemetrie gegevens tooan IoT-hub en ontvangt van apparaatopdrachten van een IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="a5a09-125">An *IoT Hub module* that uploads telemetry data tooan IoT hub and receives device commands from an IoT hub.</span></span>
* <span data-ttu-id="a5a09-126">Een *uitschakelen printer module* die wordt geïnterpreteerd telemetrie van Hallo uitschakelen apparaat en wordt afgedrukt opgemaakte gegevens toohello console tooenable probleemoplossing en foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="a5a09-126">A *BLE printer module* that interprets telemetry from hello BLE device and prints formatted data toohello console tooenable troubleshooting and debugging.</span></span>

### <a name="how-data-flows-through-hello-gateway"></a><span data-ttu-id="a5a09-127">Hoe gegevens loopt via de gateway Hallo</span><span class="sxs-lookup"><span data-stu-id="a5a09-127">How data flows through hello gateway</span></span>

<span data-ttu-id="a5a09-128">Hallo volgende blokdiagram illustreert Hallo telemetrie uploaden van gegevensstroom pijplijn:</span><span class="sxs-lookup"><span data-stu-id="a5a09-128">hello following block diagram illustrates hello telemetry upload data flow pipeline:</span></span>

![Telemetrie uploaden gateway pijplijn](media/iot-hub-iot-edge-physical-device/gateway_ble_upload_data_flow.png)

<span data-ttu-id="a5a09-130">Hallo-stappen waarmee een telemetrie-item van een apparaat uitschakelen tooIoT onderweg Hub zijn:</span><span class="sxs-lookup"><span data-stu-id="a5a09-130">hello steps that an item of telemetry takes traveling from a BLE device tooIoT Hub are:</span></span>

1. <span data-ttu-id="a5a09-131">Hallo uitschakelen apparaat genereert een voorbeeld van een temperatuur en verzendt deze via Bluetooth-toohello uitschakelen module in het Hallo-gateway.</span><span class="sxs-lookup"><span data-stu-id="a5a09-131">hello BLE device generates a temperature sample and sends it over Bluetooth toohello BLE module in hello gateway.</span></span>
1. <span data-ttu-id="a5a09-132">Hallo uitschakelen module Hallo voorbeeld ontvangt en publiceert deze toohello broker samen met de Hallo MAC-adres van apparaat Hallo.</span><span class="sxs-lookup"><span data-stu-id="a5a09-132">hello BLE module receives hello sample and publishes it toohello broker along with hello MAC address of hello device.</span></span>
1. <span data-ttu-id="a5a09-133">Hallo identiteit toewijzing module dit bericht wordt opgehaald en maakt gebruik van een interne tabel tootranslate Hallo MAC-adres van apparaat Hallo in een IoT Hub apparaat-id.</span><span class="sxs-lookup"><span data-stu-id="a5a09-133">hello identity mapping module picks up this message and uses an internal table tootranslate hello MAC address of hello device into an IoT Hub device identity.</span></span> <span data-ttu-id="a5a09-134">Een IoT Hub apparaat-id bestaat uit een apparaat-ID en de apparaatsleutel.</span><span class="sxs-lookup"><span data-stu-id="a5a09-134">An IoT Hub device identity consists of a device ID and device key.</span></span>
1. <span data-ttu-id="a5a09-135">Hallo identiteit toewijzing module publiceert een nieuw bericht met Hallo temperatuur voorbeeldgegevens, Hallo MAC-adres van apparaat hello, Hallo apparaat-ID en Hallo apparaatsleutel.</span><span class="sxs-lookup"><span data-stu-id="a5a09-135">hello identity mapping module publishes a new message that contains hello temperature sample data, hello MAC address of hello device, hello device ID, and hello device key.</span></span>
1. <span data-ttu-id="a5a09-136">Hallo IoT Hub-module ontvangt dit nieuwe bericht (gegenereerd door Hallo identiteit toewijzing module) en publiceert deze tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a5a09-136">hello IoT Hub module receives this new message (generated by hello identity mapping module) and publishes it tooIoT Hub.</span></span>
1. <span data-ttu-id="a5a09-137">Hallo berichtenlogboek module registreert alle berichten van Hallo broker tooa lokaal bestand.</span><span class="sxs-lookup"><span data-stu-id="a5a09-137">hello logger module logs all messages from hello broker tooa local file.</span></span>

<span data-ttu-id="a5a09-138">Hallo volgende blokdiagram illustreert Hallo apparaat opdracht gegevensstroom pijplijn:</span><span class="sxs-lookup"><span data-stu-id="a5a09-138">hello following block diagram illustrates hello device command data flow pipeline:</span></span>

![Apparaat opdracht gateway-pipeline](media/iot-hub-iot-edge-physical-device/gateway_ble_command_data_flow.png)

1. <span data-ttu-id="a5a09-140">Hallo IoT Hub module periodiek Hallo iothub voor nieuwe opdracht-berichten.</span><span class="sxs-lookup"><span data-stu-id="a5a09-140">hello IoT Hub module periodically polls hello IoT hub for new command messages.</span></span>
1. <span data-ttu-id="a5a09-141">Wanneer Hallo IoT Hub-module een nieuwe opdrachtbericht ontvangt, publiceert deze deze toohello broker.</span><span class="sxs-lookup"><span data-stu-id="a5a09-141">When hello IoT Hub module receives a new command message, it publishes it toohello broker.</span></span>
1. <span data-ttu-id="a5a09-142">Hallo identiteit toewijzing module opdracht het Hallo-bericht opgehaald en maakt gebruik van een interne tabel tootranslate Hallo IoT Hub apparaat-ID tooa apparaat MAC-adres.</span><span class="sxs-lookup"><span data-stu-id="a5a09-142">hello identity mapping module picks up hello command message and uses an internal table tootranslate hello IoT Hub device ID tooa device MAC address.</span></span> <span data-ttu-id="a5a09-143">Vervolgens wordt een nieuw bericht met de MAC-adres van het doelapparaat Hallo Hallo in Hallo eigenschappen kaart van het Hallo-bericht gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="a5a09-143">It then publishes a new message that includes hello MAC address of hello target device in hello properties map of hello message.</span></span>
1. <span data-ttu-id="a5a09-144">Hallo uitschakelen Cloud-naar-apparaat module neemt over dit bericht en zet deze om in Hallo juiste uitschakelen instructie voor Hallo uitschakelen module.</span><span class="sxs-lookup"><span data-stu-id="a5a09-144">hello BLE Cloud-to-Device module picks up this message and translates it into hello proper BLE instruction for hello BLE module.</span></span> <span data-ttu-id="a5a09-145">Vervolgens wordt een nieuw bericht gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="a5a09-145">It then publishes a new message.</span></span>
1. <span data-ttu-id="a5a09-146">Hallo uitschakelen module dit bericht wordt opgehaald en Hallo i/o-instructie worden uitgevoerd door te communiceren met de Hallo uitschakelen apparaat.</span><span class="sxs-lookup"><span data-stu-id="a5a09-146">hello BLE module picks up this message and executes hello I/O instruction by communicating with hello BLE device.</span></span>
1. <span data-ttu-id="a5a09-147">Hallo berichtenlogboek module registreert alle berichten van Hallo broker tooa schijf-bestand.</span><span class="sxs-lookup"><span data-stu-id="a5a09-147">hello logger module logs all messages from hello broker tooa disk file.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a5a09-148">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a5a09-148">Prerequisites</span></span>

<span data-ttu-id="a5a09-149">toocomplete in deze zelfstudie, moet u een actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="a5a09-149">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="a5a09-150">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="a5a09-150">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="a5a09-151">Zie [Gratis proefversie van Azure][lnk-free-trial] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="a5a09-151">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

<span data-ttu-id="a5a09-152">SSH-client moet u op uw computer tooenable u tooremotely access Hallo-opdracht regel op Hallo frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="a5a09-152">You need SSH client on your desktop machine tooenable you tooremotely access hello command line on hello Raspberry Pi.</span></span>

- <span data-ttu-id="a5a09-153">Windows bevat geen een SSH-client.</span><span class="sxs-lookup"><span data-stu-id="a5a09-153">Windows does not include an SSH client.</span></span> <span data-ttu-id="a5a09-154">Wordt u aangeraden [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="a5a09-154">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="a5a09-155">De meeste Linux-distributies en Mac OS bevatten Hallo SSH-opdrachtregelprogramma.</span><span class="sxs-lookup"><span data-stu-id="a5a09-155">Most Linux distributions and Mac OS include hello command-line SSH utility.</span></span> <span data-ttu-id="a5a09-156">Zie voor meer informatie [SSH met behulp van Linux- of Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span><span class="sxs-lookup"><span data-stu-id="a5a09-156">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

## <a name="prepare-your-hardware"></a><span data-ttu-id="a5a09-157">Bereid uw hardware</span><span class="sxs-lookup"><span data-stu-id="a5a09-157">Prepare your hardware</span></span>

<span data-ttu-id="a5a09-158">Deze zelfstudie wordt ervan uitgegaan dat u gebruikt een [Texas instrumenten SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html) apparaat verbonden tooa frambozen Pi 3 Raspbian uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a5a09-158">This tutorial assumes you are using a [Texas Instruments SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html) device connected tooa Raspberry Pi 3 running Raspbian.</span></span>

### <a name="install-raspbian"></a><span data-ttu-id="a5a09-159">Raspbian installeren</span><span class="sxs-lookup"><span data-stu-id="a5a09-159">Install Raspbian</span></span>

<span data-ttu-id="a5a09-160">U kunt een Hallo opties tooinstall Raspbian volgen op uw apparaat frambozen Pi 3 gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a5a09-160">You can use either of hello following options tooinstall Raspbian on your Raspberry Pi 3 device.</span></span>

* <span data-ttu-id="a5a09-161">tooinstall hello meest recente versie van Raspbian, gebruik Hallo [NOOBS] [ lnk-noobs] grafische gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="a5a09-161">tooinstall hello latest version of Raspbian, use hello [NOOBS][lnk-noobs] graphical user interface.</span></span>
* <span data-ttu-id="a5a09-162">Handmatig [downloaden] [ lnk-raspbian] en schrijf Hallo nieuwste afbeelding van Hallo Raspbian besturingssysteem tooan SD-kaart.</span><span class="sxs-lookup"><span data-stu-id="a5a09-162">Manually [download][lnk-raspbian] and write hello latest image of hello Raspbian operating system tooan SD card.</span></span>

### <a name="sign-in-and-access-hello-terminal"></a><span data-ttu-id="a5a09-163">Aanmelden en Hallo terminal</span><span class="sxs-lookup"><span data-stu-id="a5a09-163">Sign in and access hello terminal</span></span>

<span data-ttu-id="a5a09-164">U hebt twee opties tooaccess een terminal-omgeving op uw Pi frambozen:</span><span class="sxs-lookup"><span data-stu-id="a5a09-164">You have two options tooaccess a terminal environment on your Raspberry Pi:</span></span>

* <span data-ttu-id="a5a09-165">Als u een toetsenbord hebt en verbonden tooyour frambozen Pi bewaken, kunt u Hallo Raspbian GUI tooaccess een terminalvenster gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a5a09-165">If you have a keyboard and monitor connected tooyour Raspberry Pi, you can use hello Raspbian GUI tooaccess a terminal window.</span></span>

* <span data-ttu-id="a5a09-166">Hallo opdrachtregel toegang op uw frambozen Pi gebruik van SSH op uw computer.</span><span class="sxs-lookup"><span data-stu-id="a5a09-166">Access hello command line on your Raspberry Pi using SSH from your desktop machine.</span></span>

#### <a name="use-a-terminal-window-in-hello-gui"></a><span data-ttu-id="a5a09-167">Een terminalvenster in Hallo GUI gebruiken</span><span class="sxs-lookup"><span data-stu-id="a5a09-167">Use a terminal Window in hello GUI</span></span>

<span data-ttu-id="a5a09-168">Hallo standaardreferenties voor Raspbian zijn gebruikersnaam **pi** en het wachtwoord **frambozen**.</span><span class="sxs-lookup"><span data-stu-id="a5a09-168">hello default credentials for Raspbian are username **pi** and password **raspberry**.</span></span> <span data-ttu-id="a5a09-169">In de taakbalk Hallo in Hallo GUI, kunt u Hallo starten **Terminal** hulpprogramma Hallo-pictogram dat op een monitor lijkt.</span><span class="sxs-lookup"><span data-stu-id="a5a09-169">In hello task bar in hello GUI, you can launch hello **Terminal** utility using hello icon that looks like a monitor.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="a5a09-170">Meld u aan met SSH</span><span class="sxs-lookup"><span data-stu-id="a5a09-170">Sign in with SSH</span></span>

<span data-ttu-id="a5a09-171">U kunt SSH gebruiken voor toegang tot opdrachtregel tooyour frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="a5a09-171">You can use SSH for command-line access tooyour Raspberry Pi.</span></span> <span data-ttu-id="a5a09-172">Hallo artikel [SSH (Secure Shell)] [ lnk-pi-ssh] wordt beschreven hoe tooconfigure SSH op uw Pi frambozen en hoe tooconnect van [Windows] [ lnk-ssh-windows] of [Linux en Mac OS][lnk-ssh-linux].</span><span class="sxs-lookup"><span data-stu-id="a5a09-172">hello article [SSH (Secure Shell)][lnk-pi-ssh] describes how tooconfigure SSH on your Raspberry Pi, and how tooconnect from [Windows][lnk-ssh-windows] or [Linux & Mac OS][lnk-ssh-linux].</span></span>

<span data-ttu-id="a5a09-173">Aanmelden met gebruikersnaam **pi** en het wachtwoord **frambozen**.</span><span class="sxs-lookup"><span data-stu-id="a5a09-173">Sign in with username **pi** and password **raspberry**.</span></span>

### <a name="install-bluez-537"></a><span data-ttu-id="a5a09-174">BlueZ 5.37 installeren</span><span class="sxs-lookup"><span data-stu-id="a5a09-174">Install BlueZ 5.37</span></span>

<span data-ttu-id="a5a09-175">Hallo uitschakelen modules praten toohello Bluetooth-hardware via Hallo BlueZ stack.</span><span class="sxs-lookup"><span data-stu-id="a5a09-175">hello BLE modules talk toohello Bluetooth hardware via hello BlueZ stack.</span></span> <span data-ttu-id="a5a09-176">U moet versie 5.37 van BlueZ voor Hallo modules toowork correct.</span><span class="sxs-lookup"><span data-stu-id="a5a09-176">You need version 5.37 of BlueZ for hello modules toowork correctly.</span></span> <span data-ttu-id="a5a09-177">Deze instructies, Controleer of de juiste versie Hallo van BlueZ is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="a5a09-177">These instructions make sure hello correct version of BlueZ is installed.</span></span>

1. <span data-ttu-id="a5a09-178">Hallo huidige Bluetooth-daemon stoppen:</span><span class="sxs-lookup"><span data-stu-id="a5a09-178">Stop hello current bluetooth daemon:</span></span>

    ```sh
    sudo systemctl stop bluetooth
    ```

1. <span data-ttu-id="a5a09-179">Hallo BlueZ afhankelijkheden installeren:</span><span class="sxs-lookup"><span data-stu-id="a5a09-179">Install hello BlueZ dependencies:</span></span>

    ```sh
    sudo apt-get update
    sudo apt-get install bluetooth bluez-tools build-essential autoconf glib2.0 libglib2.0-dev libdbus-1-dev libudev-dev libical-dev libreadline-dev
    ```

1. <span data-ttu-id="a5a09-180">Hallo BlueZ broncode downloaden van bluez.org:</span><span class="sxs-lookup"><span data-stu-id="a5a09-180">Download hello BlueZ source code from bluez.org:</span></span>

    ```sh
    wget http://www.kernel.org/pub/linux/bluetooth/bluez-5.37.tar.xz
    ```

1. <span data-ttu-id="a5a09-181">Pak de broncode Hallo:</span><span class="sxs-lookup"><span data-stu-id="a5a09-181">Unzip hello source code:</span></span>

    ```sh
    tar -xvf bluez-5.37.tar.xz
    ```

1. <span data-ttu-id="a5a09-182">Mappen toohello nieuw gemaakte map wijzigen:</span><span class="sxs-lookup"><span data-stu-id="a5a09-182">Change directories toohello newly created folder:</span></span>

    ```sh
    cd bluez-5.37
    ```

1. <span data-ttu-id="a5a09-183">Hallo BlueZ code toobe gebouwd configureren:</span><span class="sxs-lookup"><span data-stu-id="a5a09-183">Configure hello BlueZ code toobe built:</span></span>

    ```sh
    ./configure --disable-udev --disable-systemd --enable-experimental
    ```

1. <span data-ttu-id="a5a09-184">Bouw BlueZ:</span><span class="sxs-lookup"><span data-stu-id="a5a09-184">Build BlueZ:</span></span>

    ```sh
    make
    ```

1. <span data-ttu-id="a5a09-185">BlueZ installeren als deze is voltooid bouwcontract:</span><span class="sxs-lookup"><span data-stu-id="a5a09-185">Install BlueZ once it is done building:</span></span>

    ```sh
    sudo make install
    ```

1. <span data-ttu-id="a5a09-186">Wijziging systemd-serviceconfiguratie voor Bluetooth-zodat deze toohello nieuwe Bluetooth-daemon in Hallo bestand verwijst `/lib/systemd/system/bluetooth.service`.</span><span class="sxs-lookup"><span data-stu-id="a5a09-186">Change systemd service configuration for bluetooth so it points toohello new bluetooth daemon in hello file `/lib/systemd/system/bluetooth.service`.</span></span> <span data-ttu-id="a5a09-187">Hallo 'ExecStart' regel vervangen door de volgende tekst hello:</span><span class="sxs-lookup"><span data-stu-id="a5a09-187">Replace hello 'ExecStart' line with hello following text:</span></span>

    ```conf
    ExecStart=/usr/local/libexec/bluetooth/bluetoothd -E
    ```

### <a name="enable-connectivity-toohello-sensortag-device-from-your-raspberry-pi-3-device"></a><span data-ttu-id="a5a09-188">Connectiviteit toohello SensorTag apparaat vanaf uw apparaat frambozen Pi 3 inschakelen</span><span class="sxs-lookup"><span data-stu-id="a5a09-188">Enable connectivity toohello SensorTag device from your Raspberry Pi 3 device</span></span>

<span data-ttu-id="a5a09-189">Actieve Hallo-voorbeeld moet u eerst tooverify dat uw frambozen Pi 3 toohello SensorTag apparaat verbinding kan maken.</span><span class="sxs-lookup"><span data-stu-id="a5a09-189">Before running hello sample, you need tooverify that your Raspberry Pi 3 can connect toohello SensorTag device.</span></span>

1. <span data-ttu-id="a5a09-190">Zorg ervoor dat Hallo `rfkill` hulpprogramma is geïnstalleerd:</span><span class="sxs-lookup"><span data-stu-id="a5a09-190">Ensure hello `rfkill` utility is installed:</span></span>

    ```sh
    sudo apt-get install rfkill
    ```

1. <span data-ttu-id="a5a09-191">Blokkering opheffen van bluetooth op Hallo frambozen Pi 3 en controleer of het versienummer Hallo **5.37**:</span><span class="sxs-lookup"><span data-stu-id="a5a09-191">Unblock bluetooth on hello Raspberry Pi 3 and check that hello version number is **5.37**:</span></span>

    ```sh
    sudo rfkill unblock bluetooth
    bluetoothctl --version
    ```

1. <span data-ttu-id="a5a09-192">tooenter hello interactieve Bluetooth-shell, start Hallo Bluetooth-service en Hallo uitvoeren **bluetoothctl** opdracht:</span><span class="sxs-lookup"><span data-stu-id="a5a09-192">tooenter hello interactive bluetooth shell, start hello bluetooth service and execute hello **bluetoothctl** command :</span></span>

    ```sh
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. <span data-ttu-id="a5a09-193">Voer de opdracht Hallo **inschakelopdrachten** toopower up Hallo Bluetooth-controller.</span><span class="sxs-lookup"><span data-stu-id="a5a09-193">Enter hello command **power on** toopower up hello bluetooth controller.</span></span> <span data-ttu-id="a5a09-194">Hallo opdracht retourneert de vergelijkbare toohello volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="a5a09-194">hello command returns output similar toohello following:</span></span>

    ```sh
    [NEW] Controller 98:4F:EE:04:1F:DF C3 raspberrypi [default]
    ```

1. <span data-ttu-id="a5a09-195">Hallo interactieve Bluetooth-shell, Voer Hallo opdracht **scannen op** tooscan voor Bluetooth-apparaten.</span><span class="sxs-lookup"><span data-stu-id="a5a09-195">In hello interactive bluetooth shell, enter hello command **scan on** tooscan for bluetooth devices.</span></span> <span data-ttu-id="a5a09-196">Hallo opdracht retourneert de vergelijkbare toohello volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="a5a09-196">hello command returns output similar toohello following:</span></span>

    ```sh
    Discovery started
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: yes
    ```

1. <span data-ttu-id="a5a09-197">Hallo SensorTag apparaat detecteerbaar maken door Hallo kleine knop (hello groene LED moet flash) te drukken.</span><span class="sxs-lookup"><span data-stu-id="a5a09-197">Make hello SensorTag device discoverable by pressing hello small button (hello green LED should flash).</span></span> <span data-ttu-id="a5a09-198">Hallo frambozen Pi 3 moet Hallo SensorTag-apparaten detecteren:</span><span class="sxs-lookup"><span data-stu-id="a5a09-198">hello Raspberry Pi 3 should discover hello SensorTag device:</span></span>

    ```sh
    [NEW] Device A0:E6:F8:B5:F6:00 CC2650 SensorTag
    [CHG] Device A0:E6:F8:B5:F6:00 TxPower: 0
    [CHG] Device A0:E6:F8:B5:F6:00 RSSI: -43
    ```

    <span data-ttu-id="a5a09-199">In dit voorbeeld ziet u dat Hallo MAC-adres van apparaat SensorTag Hallo **A0:E6:F8:B5:F6:00**.</span><span class="sxs-lookup"><span data-stu-id="a5a09-199">In this example, you can see that hello MAC address of hello SensorTag device is **A0:E6:F8:B5:F6:00**.</span></span>

1. <span data-ttu-id="a5a09-200">Uitschakelen door te voeren Hallo scannen **scannen uitschakelen** opdracht:</span><span class="sxs-lookup"><span data-stu-id="a5a09-200">Turn off scanning by entering hello **scan off** command:</span></span>

    ```sh
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: no
    Discovery stopped
    ```

1. <span data-ttu-id="a5a09-201">Verbinding maken met tooyour SensorTag-apparaten met behulp van het MAC-adres door te voeren **verbinding \<MAC-adres\>**.</span><span class="sxs-lookup"><span data-stu-id="a5a09-201">Connect tooyour SensorTag device using its MAC address by entering **connect \<MAC address\>**.</span></span> <span data-ttu-id="a5a09-202">Hallo volgende voorbeelduitvoer wordt voor de duidelijkheid afgekort:</span><span class="sxs-lookup"><span data-stu-id="a5a09-202">hello following sample output is abbreviated for clarity:</span></span>

    ```sh
    Attempting tooconnect tooA0:E6:F8:B5:F6:00
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: yes
    Connection successful
    [CHG] Device A0:E6:F8:B5:F6:00 UUIDs: 00001800-0000-1000-8000-00805f9b34fb
    ...
    [NEW] Primary Service
            /org/bluez/hci0/dev_A0_E6_F8_B5_F6_00/service000c
            Device Information
    ...
    [CHG] Device A0:E6:F8:B5:F6:00 GattServices: /org/bluez/hci0/dev_A0_E6_F8_B5_F6_00/service000c
    ...
    [CHG] Device A0:E6:F8:B5:F6:00 Name: SensorTag 2.0
    [CHG] Device A0:E6:F8:B5:F6:00 Alias: SensorTag 2.0
    [CHG] Device A0:E6:F8:B5:F6:00 Modalias: bluetooth:v000Dp0000d0110
    ```

    > <span data-ttu-id="a5a09-203">Kunt u Hallo GATT kenmerken van Hallo-apparaat opnieuw met Hallo vermelden **lijst kenmerken** opdracht.</span><span class="sxs-lookup"><span data-stu-id="a5a09-203">You can list hello GATT characteristics of hello device again using hello **list-attributes** command.</span></span>

1. <span data-ttu-id="a5a09-204">U kunt nu loskoppelen van Hallo Hallo apparaat **verbreken** opdracht en sluit vervolgens af vanuit Hallo Bluetooth-shell met Hallo **afsluiten** opdracht:</span><span class="sxs-lookup"><span data-stu-id="a5a09-204">You can now disconnect from hello device using hello **disconnect** command and then exit from hello bluetooth shell using hello **quit** command:</span></span>

    ```sh
    Attempting toodisconnect from A0:E6:F8:B5:F6:00
    Successful disconnected
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: no
    ```

<span data-ttu-id="a5a09-205">U bent nu klaar toorun Hallo uitschakelen IoT rand voorbeeld op uw frambozen Pi 3.</span><span class="sxs-lookup"><span data-stu-id="a5a09-205">You're now ready toorun hello BLE IoT Edge sample on your Raspberry Pi 3.</span></span>

## <a name="run-hello-iot-edge-ble-sample"></a><span data-ttu-id="a5a09-206">Hallo IoT rand uitschakelen voorbeeld uitvoeren</span><span class="sxs-lookup"><span data-stu-id="a5a09-206">Run hello IoT Edge BLE sample</span></span>

<span data-ttu-id="a5a09-207">toorun hello IoT rand uitschakelen voorbeeld moet u drie taken toocomplete:</span><span class="sxs-lookup"><span data-stu-id="a5a09-207">toorun hello IoT Edge BLE sample, you need toocomplete three tasks:</span></span>

* <span data-ttu-id="a5a09-208">Configureer twee voorbeeld-apparaten in uw IoT-Hub.</span><span class="sxs-lookup"><span data-stu-id="a5a09-208">Configure two sample devices in your IoT Hub.</span></span>
* <span data-ttu-id="a5a09-209">IoT-Edge op uw apparaat frambozen Pi 3 bouwen.</span><span class="sxs-lookup"><span data-stu-id="a5a09-209">Build IoT Edge on your Raspberry Pi 3 device.</span></span>
* <span data-ttu-id="a5a09-210">Configureer en Hallo uitschakelen voorbeeld uitvoeren op uw apparaat frambozen Pi 3.</span><span class="sxs-lookup"><span data-stu-id="a5a09-210">Configure and run hello BLE sample on your Raspberry Pi 3 device.</span></span>

<span data-ttu-id="a5a09-211">Op moment van schrijven Hallo IoT Edge biedt alleen ondersteuning voor modules uitschakelen in gateways met op Linux.</span><span class="sxs-lookup"><span data-stu-id="a5a09-211">At hello time of writing, IoT Edge only supports BLE modules in gateways running on Linux.</span></span>

### <a name="configure-two-sample-devices-in-your-iot-hub"></a><span data-ttu-id="a5a09-212">Twee voorbeeld-apparaten in uw IoT-Hub configureren</span><span class="sxs-lookup"><span data-stu-id="a5a09-212">Configure two sample devices in your IoT Hub</span></span>

* <span data-ttu-id="a5a09-213">[Een iothub maken] [ lnk-create-hub] in uw Azure-abonnement, moet u het Hallo-naam van uw hub toocomplete in dit scenario.</span><span class="sxs-lookup"><span data-stu-id="a5a09-213">[Create an IoT hub][lnk-create-hub] in your Azure subscription, you need hello name of your hub toocomplete this walkthrough.</span></span> <span data-ttu-id="a5a09-214">Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.</span><span class="sxs-lookup"><span data-stu-id="a5a09-214">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="a5a09-215">Toevoegen van een apparaat aangeroepen **SensorTag_01** tooyour IoT-hub en noteer de sleutel-id en het apparaat.</span><span class="sxs-lookup"><span data-stu-id="a5a09-215">Add one device called **SensorTag_01** tooyour IoT hub and make a note of its id and device key.</span></span> <span data-ttu-id="a5a09-216">Kunt u Hallo [apparaat explorer of iothub-explorer] [ lnk-explorer-tools] van hulpprogramma's voor tooadd dit apparaat toohello IoT-hub gemaakt in de vorige stap Hallo en tooretrieve de sleutel.</span><span class="sxs-lookup"><span data-stu-id="a5a09-216">You can use hello [device explorer or iothub-explorer][lnk-explorer-tools] tools tooadd this device toohello IoT hub you created in hello previous step and tooretrieve its key.</span></span> <span data-ttu-id="a5a09-217">U kunt dit apparaat toohello SensorTag apparaat toewijzen wanneer u Hallo gateway configureert.</span><span class="sxs-lookup"><span data-stu-id="a5a09-217">You map this device toohello SensorTag device when you configure hello gateway.</span></span>

### <a name="build-azure-iot-edge-on-your-raspberry-pi-3"></a><span data-ttu-id="a5a09-218">Azure IoT-rand bouwen op uw Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="a5a09-218">Build Azure IoT Edge on your Raspberry Pi 3</span></span>

<span data-ttu-id="a5a09-219">Afhankelijkheden voor Azure IoT rand installeren:</span><span class="sxs-lookup"><span data-stu-id="a5a09-219">Install dependencies for Azure IoT Edge:</span></span>

```sh
sudo apt-get install cmake uuid-dev curl libcurl4-openssl-dev libssl-dev
```

<span data-ttu-id="a5a09-220">Gebruik Hallo deze opdrachten tooclone IoT rand en alle bijbehorende submodules tooyour basismap:</span><span class="sxs-lookup"><span data-stu-id="a5a09-220">Use hello following commands tooclone IoT Edge and all its submodules tooyour home directory:</span></span>

```sh
cd ~
git clone https://github.com/Azure/iot-edge.git
```

<span data-ttu-id="a5a09-221">Wanneer u een volledige kopie van Hallo IoT rand opslagplaats op uw frambozen Pi 3 hebt, kunt u met behulp van de volgende opdracht uit Hallo-map met de Hallo SDK Hallo bouwen:</span><span class="sxs-lookup"><span data-stu-id="a5a09-221">When you have a complete copy of hello IoT Edge repository on your Raspberry Pi 3, you can build it using hello following command from hello folder that contains hello SDK:</span></span>

```sh
cd ~/iot-edge
./tools/build.sh  --disable-native-remote-modules
```

### <a name="configure-and-run-hello-ble-sample-on-your-raspberry-pi-3"></a><span data-ttu-id="a5a09-222">Configureren en Hallo uitschakelen voorbeeld uitgevoerd op uw frambozen Pi 3</span><span class="sxs-lookup"><span data-stu-id="a5a09-222">Configure and run hello BLE sample on your Raspberry Pi 3</span></span>

<span data-ttu-id="a5a09-223">toobootstrap en Voer Hallo voorbeeld, moet u elke zijde van de IoT-module die deel uitmaakt in het Hallo-gateway configureren.</span><span class="sxs-lookup"><span data-stu-id="a5a09-223">toobootstrap and run hello sample, you must configure each IoT Edge module that participates in hello gateway.</span></span> <span data-ttu-id="a5a09-224">Deze configuratie is opgegeven in een JSON-bestand en u moet alle vijf deelnemende IoT rand modules configureren.</span><span class="sxs-lookup"><span data-stu-id="a5a09-224">This configuration is provided in a JSON file and you must configure all five participating IoT Edge modules.</span></span> <span data-ttu-id="a5a09-225">Er is een voorbeeld van een JSON-bestand in Hallo opslagplaats aangeroepen **gateway\_sample.json** die u als startpunt gebruiken kunt voor het bouwen van uw eigen configuratiebestand Hallo.</span><span class="sxs-lookup"><span data-stu-id="a5a09-225">There is a sample JSON file in hello repository called **gateway\_sample.json** that you can use as hello starting point for building your own configuration file.</span></span> <span data-ttu-id="a5a09-226">Dit bestand bevindt zich in Hallo **ble_gateway/samples/src** map in de lokale kopie van Hallo IoT Edge-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="a5a09-226">This file is in hello **samples/ble_gateway/src** folder in local copy of hello IoT Edge repository.</span></span>

<span data-ttu-id="a5a09-227">Hallo volgende secties wordt beschreven hoe tooedit deze configuratie voor Hallo uitschakelen voorbeeld en wordt ervan uitgegaan dat Hallo IoT Edge-opslagplaats is in Hallo **/home/pi/iot-edge /** map op uw frambozen Pi 3.</span><span class="sxs-lookup"><span data-stu-id="a5a09-227">hello following sections describe how tooedit this configuration file for hello BLE sample and assume that hello IoT Edge repository is in hello **/home/pi/iot-edge/** folder on your Raspberry Pi 3.</span></span> <span data-ttu-id="a5a09-228">Als Hallo opslag elders, overeenkomstig Hallo paden aanpassen.</span><span class="sxs-lookup"><span data-stu-id="a5a09-228">If hello repository is elsewhere, adjust hello paths accordingly.</span></span>

#### <a name="logger-configuration"></a><span data-ttu-id="a5a09-229">Berichtenlogboek configuratie</span><span class="sxs-lookup"><span data-stu-id="a5a09-229">Logger configuration</span></span>

<span data-ttu-id="a5a09-230">Ervan uitgaande dat Hallo gateway opslagplaats bevindt zich in Hallo **/home/pi/iot-edge /** map Hallo berichtenlogboek module als volgt configureren:</span><span class="sxs-lookup"><span data-stu-id="a5a09-230">Assuming hello gateway repository is located in hello **/home/pi/iot-edge/** folder, configure hello logger module as follows:</span></span>

```json
{
  "name": "Logger",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path" : "build/modules/logger/liblogger.so"
    }
  },
  "args":
  {
    "filename": "<</path/to/log-file.log>>"
  }
}
```

#### <a name="ble-module-configuration"></a><span data-ttu-id="a5a09-231">De moduleconfiguratie uitschakelen</span><span class="sxs-lookup"><span data-stu-id="a5a09-231">BLE module configuration</span></span>

<span data-ttu-id="a5a09-232">Hallo voorbeeldconfiguratie voor Hallo uitschakelen apparaat wordt ervan uitgegaan dat een Texas instrumenten SensorTag-apparaat.</span><span class="sxs-lookup"><span data-stu-id="a5a09-232">hello sample configuration for hello BLE device assumes a Texas Instruments SensorTag device.</span></span> <span data-ttu-id="a5a09-233">Een standaard uitschakelen apparaat dat kan worden uitgevoerd als een randapparaat GATT moet werken, maar u tooupdate Hallo GATT kenmerk id's en -gegevens moet mogelijk.</span><span class="sxs-lookup"><span data-stu-id="a5a09-233">Any standard BLE device that can operate as a GATT peripheral should work but you may need tooupdate hello GATT characteristic IDs and data.</span></span> <span data-ttu-id="a5a09-234">Hallo MAC-adres van uw apparaat SensorTag toevoegen:</span><span class="sxs-lookup"><span data-stu-id="a5a09-234">Add hello MAC address of your SensorTag device:</span></span>

```json
{
  "name": "SensorTag",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/ble/libble.so"
    }
  },
  "args": {
    "controller_index": 0,
    "device_mac_address": "<<AA:BB:CC:DD:EE:FF>>",
    "instructions": [
      {
        "type": "read_once",
        "characteristic_uuid": "00002A24-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A25-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A26-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A27-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A28-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A29-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "write_at_init",
        "characteristic_uuid": "F000AA02-0451-4000-B000-000000000000",
        "data": "AQ=="
      },
      {
        "type": "read_periodic",
        "characteristic_uuid": "F000AA01-0451-4000-B000-000000000000",
        "interval_in_ms": 1000
      },
      {
        "type": "write_at_exit",
        "characteristic_uuid": "F000AA02-0451-4000-B000-000000000000",
        "data": "AA=="
      }
    ]
  }
}
```

<span data-ttu-id="a5a09-235">Als u een apparaat SensorTag niet gebruikt, raadpleegt u Hallo-documentatie voor uw apparaat uitschakelen toodetermine of u tooupdate Hallo GATT kenmerk id's en gegevenswaarden moet.</span><span class="sxs-lookup"><span data-stu-id="a5a09-235">If you are not using a SensorTag device, review hello documentation for your BLE device toodetermine whether you need tooupdate hello GATT characteristic IDs and data values.</span></span>

#### <a name="iot-hub-module"></a><span data-ttu-id="a5a09-236">IoT Hub-module</span><span class="sxs-lookup"><span data-stu-id="a5a09-236">IoT Hub module</span></span>

<span data-ttu-id="a5a09-237">Hallo-naam van uw IoT-Hub toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a5a09-237">Add hello name of your IoT Hub.</span></span> <span data-ttu-id="a5a09-238">Hallo-mailachtervoegselwaarde is doorgaans **azure devices.net**:</span><span class="sxs-lookup"><span data-stu-id="a5a09-238">hello suffix value is typically **azure-devices.net**:</span></span>

```json
{
  "name": "IoTHub",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/iothub/libiothub.so"
    }
  },
  "args": {
    "IoTHubName": "<<Azure IoT Hub Name>>",
    "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
    "Transport" : "amqp"
  }
}
```

#### <a name="identity-mapping-module-configuration"></a><span data-ttu-id="a5a09-239">Configuratie van de identiteit van toewijzing</span><span class="sxs-lookup"><span data-stu-id="a5a09-239">Identity mapping module configuration</span></span>

<span data-ttu-id="a5a09-240">Hallo MAC-adres van uw apparaat SensorTag en Hallo apparaat-ID en sleutel Hallo toevoegen **SensorTag_01** apparaat u tooyour IoT Hub hebt toegevoegd:</span><span class="sxs-lookup"><span data-stu-id="a5a09-240">Add hello MAC address of your SensorTag device and hello device ID and key of hello **SensorTag_01** device you added tooyour IoT Hub:</span></span>

```json
{
  "name": "mapping",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/identitymap/libidentity_map.so"
    }
  },
  "args": [
    {
      "macAddress": "<<AA:BB:CC:DD:EE:FF>>",
      "deviceId": "<<Azure IoT Hub Device ID>>",
      "deviceKey": "<<Azure IoT Hub Device Key>>"
    }
  ]
}
```

#### <a name="ble-printer-module-configuration"></a><span data-ttu-id="a5a09-241">Module printerconfiguratie uitschakelen</span><span class="sxs-lookup"><span data-stu-id="a5a09-241">BLE Printer module configuration</span></span>

```json
{
  "name": "BLE Printer",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/samples/ble_gateway/ble_printer/libble_printer.so"
    }
  },
  "args": null
}
```

#### <a name="blec2d-module-configuration"></a><span data-ttu-id="a5a09-242">De Moduleconfiguratie BLEC2D</span><span class="sxs-lookup"><span data-stu-id="a5a09-242">BLEC2D Module Configuration</span></span>

```json
{
  "name": "BLEC2D",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/ble/libble_c2d.so"
    }
  },
  "args": null
}
```

#### <a name="routing-configuration"></a><span data-ttu-id="a5a09-243">Configuratie van de routering</span><span class="sxs-lookup"><span data-stu-id="a5a09-243">Routing Configuration</span></span>

<span data-ttu-id="a5a09-244">Hallo volgende configuratie zorgt er Hallo volgende routering tussen de rand van de IoT-modules:</span><span class="sxs-lookup"><span data-stu-id="a5a09-244">hello following configuration ensures hello following routing between IoT Edge modules:</span></span>

* <span data-ttu-id="a5a09-245">Hallo **berichtenlogboek** module ontvangt en registreert alle berichten.</span><span class="sxs-lookup"><span data-stu-id="a5a09-245">hello **Logger** module receives and logs all messages.</span></span>
* <span data-ttu-id="a5a09-246">Hallo **SensorTag** module verzendt berichten tooboth hello **toewijzing** en **uitschakelen Printer** modules.</span><span class="sxs-lookup"><span data-stu-id="a5a09-246">hello **SensorTag** module sends messages tooboth hello **mapping** and **BLE Printer** modules.</span></span>
* <span data-ttu-id="a5a09-247">Hallo **toewijzing** module verzendt berichten toohello **IoTHub** module toobe verzonden tooyour IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a5a09-247">hello **mapping** module sends messages toohello **IoTHub** module toobe sent up tooyour IoT Hub.</span></span>
* <span data-ttu-id="a5a09-248">Hallo **IoTHub** module verzendt berichten back-toohello **toewijzing** module.</span><span class="sxs-lookup"><span data-stu-id="a5a09-248">hello **IoTHub** module sends messages back toohello **mapping** module.</span></span>
* <span data-ttu-id="a5a09-249">Hallo **toewijzing** module verzendt berichten toohello **BLEC2D** module.</span><span class="sxs-lookup"><span data-stu-id="a5a09-249">hello **mapping** module sends messages toohello **BLEC2D** module.</span></span>
* <span data-ttu-id="a5a09-250">Hallo **BLEC2D** module verzendt berichten back-toohello **Sensor Tag** module.</span><span class="sxs-lookup"><span data-stu-id="a5a09-250">hello **BLEC2D** module sends messages back toohello **Sensor Tag** module.</span></span>

```json
"links" : [
    {"source" : "*", "sink" : "Logger" },
    {"source" : "SensorTag", "sink" : "mapping" },
    {"source" : "SensorTag", "sink" : "BLE Printer" },
    {"source" : "mapping", "sink" : "IoTHub" },
    {"source" : "IoTHub", "sink" : "mapping" },
    {"source" : "mapping", "sink" : "BLEC2D" },
    {"source" : "BLEC2D", "sink" : "SensorTag"}
 ]
```

<span data-ttu-id="a5a09-251">toorun hello voorbeeld pass Hallo pad toohello JSON-configuratiebestand als een parameter toohello **uitschakelen\_gateway** binaire.</span><span class="sxs-lookup"><span data-stu-id="a5a09-251">toorun hello sample, pass hello path toohello JSON configuration file as a parameter toohello **ble\_gateway** binary.</span></span> <span data-ttu-id="a5a09-252">Hallo volgende opdracht wordt ervan uitgegaan dat u gebruikmaakt van Hallo **gateway_sample.json** configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="a5a09-252">hello following command assumes you are using hello **gateway_sample.json** configuration file.</span></span> <span data-ttu-id="a5a09-253">Deze opdracht wordt uitgevoerd van Hallo **iot-edge** map op Hallo frambozen Pi:</span><span class="sxs-lookup"><span data-stu-id="a5a09-253">Execute this command from hello **iot-edge** folder on hello Raspberry Pi:</span></span>

```sh
./build/samples/ble_gateway/ble_gateway ./samples/ble_gateway/src/gateway_sample.json
```

<span data-ttu-id="a5a09-254">Mogelijk moet u toopress Hallo kleine knop op Hallo SensorTag apparaat toomake deze kunnen worden gedetecteerd voordat u Hallo voorbeeld uitvoert.</span><span class="sxs-lookup"><span data-stu-id="a5a09-254">You may need toopress hello small button on hello SensorTag device toomake it discoverable before you run hello sample.</span></span>

<span data-ttu-id="a5a09-255">Wanneer u Hallo voorbeeld uitvoert, kunt u Hallo [apparaat explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) of Hallo [iothub explorer](https://github.com/Azure/iothub-explorer) hulpprogramma toomonitor Hallo berichten Hallo gateway aan de rand van de IoT van Hallo SensorTag apparaat verzendt.</span><span class="sxs-lookup"><span data-stu-id="a5a09-255">When you run hello sample, you can use hello [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) or hello [iothub-explorer](https://github.com/Azure/iothub-explorer) tool toomonitor hello messages hello IoT Edge gateway forwards from hello SensorTag device.</span></span> <span data-ttu-id="a5a09-256">Bijvoorbeeld, kunt met iothub explorer u controleren met behulp van de volgende opdracht Hallo apparaat-naar-cloud-berichten:</span><span class="sxs-lookup"><span data-stu-id="a5a09-256">For example, using iothub-explorer you can monitor device-to-cloud messages using hello following command:</span></span>

```sh
iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
```

## <a name="send-cloud-to-device-messages"></a><span data-ttu-id="a5a09-257">Cloud-naar-apparaat-berichten verzenden</span><span class="sxs-lookup"><span data-stu-id="a5a09-257">Send cloud-to-device messages</span></span>

<span data-ttu-id="a5a09-258">Hallo uitschakelen module ondersteunt ook verzenden opdrachten uit IoT Hub toohello apparaat.</span><span class="sxs-lookup"><span data-stu-id="a5a09-258">hello BLE module also supports sending commands from IoT Hub toohello device.</span></span> <span data-ttu-id="a5a09-259">Kunt u Hallo [apparaat explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) of Hallo [iothub explorer](https://github.com/Azure/iothub-explorer) hulpprogramma toosend JSON berichten die module Hallo uitschakelen gateway stuurt op toohello uitschakelen apparaat.</span><span class="sxs-lookup"><span data-stu-id="a5a09-259">You can use hello [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) or hello [iothub-explorer](https://github.com/Azure/iothub-explorer) tool toosend JSON messages that hello BLE gateway module forwards on toohello BLE device.</span></span>

<span data-ttu-id="a5a09-260">Als u van Hallo Texas instrumenten SensorTag-apparaat gebruikmaakt, kunt u op Hallo rode LED, groene LED of alarm door opdrachten uit IoT Hub verzendt.</span><span class="sxs-lookup"><span data-stu-id="a5a09-260">If you are using hello Texas Instruments SensorTag device, you can turn on hello red LED, green LED, or buzzer by sending commands from IoT Hub.</span></span> <span data-ttu-id="a5a09-261">Voordat u opdrachten uit IoT Hub verzendt, moet u eerst Hallo na twee JSON-berichten in volgorde sturen.</span><span class="sxs-lookup"><span data-stu-id="a5a09-261">Before you send commands from IoT Hub, first send hello following two JSON messages in order.</span></span> <span data-ttu-id="a5a09-262">U kunt vervolgens een van de Hallo opdrachten tooturn op Hallo lichten of alarm verzenden.</span><span class="sxs-lookup"><span data-stu-id="a5a09-262">Then you can send any of hello commands tooturn on hello lights or buzzer.</span></span>

1. <span data-ttu-id="a5a09-263">Opnieuw instellen van alle LED's en Hallo alarm (deze uit te schakelen):</span><span class="sxs-lookup"><span data-stu-id="a5a09-263">Reset all LEDs and hello buzzer (turn them off):</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AA=="
    }
    ```

1. <span data-ttu-id="a5a09-264">I/o's configureren als 'extern':</span><span class="sxs-lookup"><span data-stu-id="a5a09-264">Configure I/O as 'remote':</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA66-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

<span data-ttu-id="a5a09-265">U kunt nu een Hallo opdrachten tooturn volgen op Hallo lichten of alarm op Hallo SensorTag apparaat verzenden:</span><span class="sxs-lookup"><span data-stu-id="a5a09-265">Now you can send any of hello following commands tooturn on hello lights or buzzer on hello SensorTag device:</span></span>

* <span data-ttu-id="a5a09-266">Hallo rode LED inschakelen:</span><span class="sxs-lookup"><span data-stu-id="a5a09-266">Turn on hello red LED:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

* <span data-ttu-id="a5a09-267">Hallo groen LED inschakelen:</span><span class="sxs-lookup"><span data-stu-id="a5a09-267">Turn on hello green LED:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "Ag=="
    }
    ```

* <span data-ttu-id="a5a09-268">Hallo alarm inschakelen:</span><span class="sxs-lookup"><span data-stu-id="a5a09-268">Turn on hello buzzer:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "BA=="
    }
    ```

## <a name="next-steps"></a><span data-ttu-id="a5a09-269">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a5a09-269">Next Steps</span></span>

<span data-ttu-id="a5a09-270">Als u toogain een uitgebreidere kennis van IoT-rand wilt en Experimenteer met enkele codevoorbeelden, gaat u naar de volgende Hallo developer zelfstudies en bronnen:</span><span class="sxs-lookup"><span data-stu-id="a5a09-270">If you want toogain a more advanced understanding of IoT Edge and experiment with some code examples, visit hello following developer tutorials and resources:</span></span>

* <span data-ttu-id="a5a09-271">[Azure IoT-rand][lnk-sdk]</span><span class="sxs-lookup"><span data-stu-id="a5a09-271">[Azure IoT Edge][lnk-sdk]</span></span>

<span data-ttu-id="a5a09-272">toofurther verkennen Hallo-mogelijkheden van IoT Hub, Zie:</span><span class="sxs-lookup"><span data-stu-id="a5a09-272">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="a5a09-273">[Ontwikkelaarshandleiding voor IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="a5a09-273">[IoT Hub developer guide][lnk-devguide]</span></span>

<!-- Links -->
[lnk-ble-samplecode]: https://github.com/Azure/iot-edge/tree/master/samples/ble_gateway
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-explorer-tools]: https://github.com/Azure/azure-iot-sdks/blob/master/doc/manage_iot_hub.md
[lnk-sdk]: https://github.com/Azure/iot-edge/
[lnk-noobs]: https://www.raspberrypi.org/documentation/installation/noobs.md
[lnk-raspbian]: https://www.raspberrypi.org/downloads/raspbian/
[lnk-devguide]: iot-hub-devguide.md
[lnk-create-hub]: iot-hub-create-through-portal.md 
[lnk-pi-ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[lnk-ssh-windows]: https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md
[lnk-ssh-linux]: https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md
