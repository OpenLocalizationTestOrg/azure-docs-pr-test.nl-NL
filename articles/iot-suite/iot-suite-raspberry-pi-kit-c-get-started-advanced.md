---
title: een tooAzure frambozen Pi aaaConnect IoT-Suite met C toosupport firmware-updates | Microsoft Docs
description: Gebruik Microsoft Azure IoT Starter Kit Hallo voor Hallo frambozen Pi 3 en Azure IoT Suite. Gebruik C tooconnect uw oplossing voor externe controle frambozen Pi toohello, verzenden van telemetrie van sensoren toohello cloud en voert u een externe firmware-update.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 36d39c6d754ddb025fd3f6b74d7795ed907b754c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-enable-remote-firmware-updates-using-c"></a><span data-ttu-id="1683b-104">Verbinding maken met uw oplossing voor externe controle frambozen Pi 3 toohello en externe firmware-updates met C inschakelen</span><span class="sxs-lookup"><span data-stu-id="1683b-104">Connect your Raspberry Pi 3 toohello remote monitoring solution and enable remote firmware updates using C</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="1683b-105">Deze zelfstudie leert u hoe toouse Microsoft Azure IoT Starter Kit Hallo voor frambozen Pi 3:</span><span class="sxs-lookup"><span data-stu-id="1683b-105">This tutorial shows you how toouse hello Microsoft Azure IoT Starter Kit for Raspberry Pi 3 to:</span></span>

* <span data-ttu-id="1683b-106">Ontwikkel een temperatuur en vochtigheid lezer die met de Hallo cloud communiceren kan.</span><span class="sxs-lookup"><span data-stu-id="1683b-106">Develop a temperature and humidity reader that can communicate with hello cloud.</span></span>
* <span data-ttu-id="1683b-107">Inschakelen en het uitvoeren van een externe firmware-update tooupdate Hallo-clienttoepassing op Hallo frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="1683b-107">Enable and perform a remote firmware update tooupdate hello client application on hello Raspberry Pi.</span></span>

<span data-ttu-id="1683b-108">Hallo-zelfstudie wordt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="1683b-108">hello tutorial uses:</span></span>

* <span data-ttu-id="1683b-109">Raspbian OS Hallo C programmeertaal en Hallo Microsoft Azure IoT SDK voor C tooimplement een voorbeeld-apparaat.</span><span class="sxs-lookup"><span data-stu-id="1683b-109">Raspbian OS, hello C programming language, and hello Microsoft Azure IoT SDK for C tooimplement a sample device.</span></span>
* <span data-ttu-id="1683b-110">Hallo IoT Suite remote monitoring vooraf geconfigureerde oplossing als Hallo cloud-gebaseerde back-end.</span><span class="sxs-lookup"><span data-stu-id="1683b-110">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="1683b-111">Overzicht</span><span class="sxs-lookup"><span data-stu-id="1683b-111">Overview</span></span>

<span data-ttu-id="1683b-112">In deze zelfstudie maakt uitvoeren u Hallo stappen:</span><span class="sxs-lookup"><span data-stu-id="1683b-112">In this tutorial, you complete hello following steps:</span></span>

* <span data-ttu-id="1683b-113">Implementeer een exemplaar van Hallo externe controle vooraf geconfigureerde oplossing tooyour Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="1683b-113">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="1683b-114">Deze stap implementeert automatisch en meerdere Azure-services configureert.</span><span class="sxs-lookup"><span data-stu-id="1683b-114">This step automatically deploys and configures multiple Azure services.</span></span>
* <span data-ttu-id="1683b-115">Stel uw apparaat en sensoren toocommunicate met uw computer en het Hallo oplossing voor externe controle.</span><span class="sxs-lookup"><span data-stu-id="1683b-115">Set up your device and sensors toocommunicate with your computer and hello remote monitoring solution.</span></span>
* <span data-ttu-id="1683b-116">Hallo voorbeeld apparaat code tooconnect toohello oplossing voor externe controle bijwerken en verzenden van telemetrie die u op Hallo oplossing dashboard weergeven kunt.</span><span class="sxs-lookup"><span data-stu-id="1683b-116">Update hello sample device code tooconnect toohello remote monitoring solution, and send telemetry that you can view on hello solution dashboard.</span></span>
* <span data-ttu-id="1683b-117">Hallo voorbeeld apparaat code tooupdate Hallo-clienttoepassing gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1683b-117">Use hello sample device code tooupdate hello client application.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="1683b-118">Hallo externe controle van de bepalingen van de oplossing voor een verzameling Azure-services in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="1683b-118">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="1683b-119">Hallo implementatie duidt op een echte enterprise-architectuur.</span><span class="sxs-lookup"><span data-stu-id="1683b-119">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="1683b-120">tooavoid onnodige Azure-verbruik kosten, verwijderen van uw exemplaar van Hallo vooraf geconfigureerde oplossing op azureiotsuite.com wanneer u klaar bent met het.</span><span class="sxs-lookup"><span data-stu-id="1683b-120">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="1683b-121">Als u moet de vooraf geconfigureerde oplossing opnieuw hello, u kunt gemakkelijk het opnieuw maken.</span><span class="sxs-lookup"><span data-stu-id="1683b-121">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="1683b-122">Zie voor meer informatie over het verminderen van verbruik tijdens het Hallo voor externe controle van de oplossing wordt uitgevoerd, [configureren van Azure IoT Suite vooraf geconfigureerde oplossingen voor demonstratiedoeleinden][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="1683b-122">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-hello-sample"></a><span data-ttu-id="1683b-123">Downloaden en configureren van Hallo-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="1683b-123">Download and configure hello sample</span></span>

<span data-ttu-id="1683b-124">U kunt nu downloaden en Hallo-bewaking externe clienttoepassing configureren op uw frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="1683b-124">You can now download and configure hello remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="clone-hello-repositories"></a><span data-ttu-id="1683b-125">Hallo-opslagplaatsen klonen</span><span class="sxs-lookup"><span data-stu-id="1683b-125">Clone hello repositories</span></span>

<span data-ttu-id="1683b-126">Als u dit nog niet hebt gedaan, vereist kloon Hallo opslagplaatsen door te voeren Hallo opdrachten op uw Pi volgen:</span><span class="sxs-lookup"><span data-stu-id="1683b-126">If you haven't done so already, clone hello required repositories by running hello following commands on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
```

### <a name="update-hello-device-connection-string"></a><span data-ttu-id="1683b-127">Verbindingsreeks Hallo-apparaat bijwerken</span><span class="sxs-lookup"><span data-stu-id="1683b-127">Update hello device connection string</span></span>

<span data-ttu-id="1683b-128">Open Hallo voorbeeldconfiguratiebestand in Hallo **nano** editor met behulp van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="1683b-128">Open hello sample configuration file in hello **nano** editor using hello following command:</span></span>

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/config/deviceinfo
```

<span data-ttu-id="1683b-129">Hallo tijdelijke aanduiding voor waarden vervangt door Hallo-ID en IoT Hub apparaatgegevens u gemaakt en opgeslagen op Hallo begin van deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="1683b-129">Replace hello placeholder values with hello device ID and IoT Hub information you created and saved at hello start of this tutorial.</span></span>

<span data-ttu-id="1683b-130">Wanneer u klaar bent, ziet er als volgt Hallo Hallo inhoud van Hallo deviceinfo bestand:</span><span class="sxs-lookup"><span data-stu-id="1683b-130">When you are done, hello contents of hello deviceinfo file should look like hello following example:</span></span>

```conf
yourdeviceid
HostName=youriothubname.azure-devices.net;DeviceId=yourdeviceid;SharedAccessKey=yourdevicekey
```

<span data-ttu-id="1683b-131">Sla de wijzigingen (**Ctrl-O**, **Enter**) en sluit de editor af hello (**Ctrl X**).</span><span class="sxs-lookup"><span data-stu-id="1683b-131">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>

## <a name="build-hello-sample"></a><span data-ttu-id="1683b-132">Hallo voorbeeld bouwen</span><span class="sxs-lookup"><span data-stu-id="1683b-132">Build hello sample</span></span>

<span data-ttu-id="1683b-133">Als u dit nog niet hebt gedaan, Hallo vereiste pakketten installeren voor Hallo Microsoft Azure IoT-apparaat-SDK voor C door het uitvoeren van de volgende opdrachten in een terminal op Hallo frambozen Pi Hallo:</span><span class="sxs-lookup"><span data-stu-id="1683b-133">If you have not already done so, install hello prerequisite packages for hello Microsoft Azure IoT Device SDK for C by running hello following commands in a terminal on hello Raspberry Pi:</span></span>

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

<span data-ttu-id="1683b-134">U kunt nu Hallo Voorbeeldoplossing op Hallo frambozen Pi bouwen:</span><span class="sxs-lookup"><span data-stu-id="1683b-134">You can now build hello sample solution on hello Raspberry Pi:</span></span>

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/1.0/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/1.0/build.sh
```

<span data-ttu-id="1683b-135">U kunt nu Hallo voorbeeld programma uitvoeren op Hallo frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="1683b-135">You can now run hello sample program on hello Raspberry Pi.</span></span> <span data-ttu-id="1683b-136">Voer Hallo-opdracht:</span><span class="sxs-lookup"><span data-stu-id="1683b-136">Enter hello command:</span></span>

  ```sh
  sudo ~/cmake/remote_monitoring/remote_monitoring
  ```

<span data-ttu-id="1683b-137">Hallo is volgende voorbeelduitvoer een voorbeeld van uitvoer van Hallo die u achter de opdrachtprompt Hallo op Hallo frambozen Pi zien:</span><span class="sxs-lookup"><span data-stu-id="1683b-137">hello following sample output is an example of hello output you see at hello command prompt on hello Raspberry Pi:</span></span>

![De uitvoer van de app Raspberry Pi][img-raspberry-output]

<span data-ttu-id="1683b-139">Druk op **Ctrl-C** tooexit Hallo programma op elk gewenst moment.</span><span class="sxs-lookup"><span data-stu-id="1683b-139">Press **Ctrl-C** tooexit hello program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-advanced](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-advanced.md)]

1. <span data-ttu-id="1683b-140">Klik in het dashboard van de oplossing hello, **apparaten** toovisit hello **apparaten** pagina.</span><span class="sxs-lookup"><span data-stu-id="1683b-140">In hello solution dashboard, click **Devices** toovisit hello **Devices** page.</span></span> <span data-ttu-id="1683b-141">Selecteer uw Pi frambozen in Hallo **lijst met apparaten**.</span><span class="sxs-lookup"><span data-stu-id="1683b-141">Select your Raspberry Pi in hello **Device List**.</span></span> <span data-ttu-id="1683b-142">Kies vervolgens **methoden**:</span><span class="sxs-lookup"><span data-stu-id="1683b-142">Then choose **Methods**:</span></span>

    ![Lijst met apparaten in het dashboard][img-list-devices]

1. <span data-ttu-id="1683b-144">Op Hallo **methode Invoke** pagina **InitiateFirmwareUpdate** in Hallo **methode** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="1683b-144">On hello **Invoke Method** page, choose **InitiateFirmwareUpdate** in hello **Method** dropdown.</span></span>

1. <span data-ttu-id="1683b-145">In Hallo **FWPackageURI** veld **https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit/raw/master/advanced/2.0/package/remote_monitoring.zip**.</span><span class="sxs-lookup"><span data-stu-id="1683b-145">In hello **FWPackageURI** field, enter **https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit/raw/master/advanced/2.0/package/remote_monitoring.zip**.</span></span> <span data-ttu-id="1683b-146">Dit archief Hallo-implementatie van versie 2.0 van Hallo firmware bevat.</span><span class="sxs-lookup"><span data-stu-id="1683b-146">This archive file contains hello implementation of version 2.0 of hello firmware.</span></span>

1. <span data-ttu-id="1683b-147">Kies **InvokeMethod**.</span><span class="sxs-lookup"><span data-stu-id="1683b-147">Choose **InvokeMethod**.</span></span> <span data-ttu-id="1683b-148">Hallo-app op Hallo frambozen Pi verzendt een dashboard van de bevestiging terug toohello oplossing.</span><span class="sxs-lookup"><span data-stu-id="1683b-148">hello app on hello Raspberry Pi sends an acknowledgment back toohello solution dashboard.</span></span> <span data-ttu-id="1683b-149">Vervolgens wordt de procedure Hallo firmware-update gestart door nieuwe versie van de firmware Hallo Hallo te downloaden:</span><span class="sxs-lookup"><span data-stu-id="1683b-149">It then starts hello firmware update process by downloading hello new version of hello firmware:</span></span>

    ![Overzicht van de methode weergeven][img-method-history]

## <a name="observe-hello-firmware-update-process"></a><span data-ttu-id="1683b-151">Hallo firmware updateproces observeren</span><span class="sxs-lookup"><span data-stu-id="1683b-151">Observe hello firmware update process</span></span>

<span data-ttu-id="1683b-152">U kunt Hallo firmware updateproces zien terwijl deze wordt uitgevoerd op Hallo apparaat en gerapporteerd door het bekijken van Hallo eigenschappen in het dashboard van de oplossing Hallo:</span><span class="sxs-lookup"><span data-stu-id="1683b-152">You can observe hello firmware update process as it runs on hello device and by viewing hello reported properties in hello solution dashboard:</span></span>

1. <span data-ttu-id="1683b-153">U kunt Hallo voortgang in van het updateproces Hallo op Hallo frambozen Pi bekijken:</span><span class="sxs-lookup"><span data-stu-id="1683b-153">You can view hello progress in of hello update process on hello Raspberry Pi:</span></span>

    ![Voortgang van bijwerken weergeven][img-update-progress]

    > [!NOTE]
    > <span data-ttu-id="1683b-155">Hallo-app voor externe controle opnieuw is opgestart achtergrond bij Hallo-update is voltooid.</span><span class="sxs-lookup"><span data-stu-id="1683b-155">hello remote monitoring app restarts silently when hello update completes.</span></span> <span data-ttu-id="1683b-156">Gebruik de opdracht Hallo `ps -ef` tooverify wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1683b-156">Use hello command `ps -ef` tooverify it is running.</span></span> <span data-ttu-id="1683b-157">Als u tooterminate Hallo proces wilt, gebruikt u Hallo `kill` opdracht met Hallo proces-id.</span><span class="sxs-lookup"><span data-stu-id="1683b-157">If you want tooterminate hello process, use hello `kill` command with hello process id.</span></span>

1. <span data-ttu-id="1683b-158">U kunt Hallo status van de firmware-update hello, weergeven, zoals gemeld door het Hallo-apparaat in de oplossingsportal Hallo.</span><span class="sxs-lookup"><span data-stu-id="1683b-158">You can view hello status of hello firmware update, as reported by hello device, in hello solution portal.</span></span> <span data-ttu-id="1683b-159">Hallo volgende schermafbeelding ziet Hallo status en de duur van elke fase van het updateproces Hallo en nieuwe firmwareversie Hallo:</span><span class="sxs-lookup"><span data-stu-id="1683b-159">hello following screenshot shows hello status and duration of each stage of hello update process, and hello new firmware version:</span></span>

    ![De status van de taak weergeven][img-job-status]

    <span data-ttu-id="1683b-161">Als u back-toohello dashboard navigeert, kunt u controleren Hallo apparaat verzendt nog steeds telemetrie Hallo firmware-update te volgen.</span><span class="sxs-lookup"><span data-stu-id="1683b-161">If you navigate back toohello dashboard, you can verify hello device is still sending telemetry following hello firmware update.</span></span>

> [!WARNING]
> <span data-ttu-id="1683b-162">Als u Hallo oplossing uitgevoerd in uw Azure-account voor externe controle laat, wordt u gefactureerd voor Hallo keer die wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1683b-162">If you leave hello remote monitoring solution running in your Azure account, you are billed for hello time it runs.</span></span> <span data-ttu-id="1683b-163">Zie voor meer informatie over het verminderen van verbruik tijdens het Hallo voor externe controle van de oplossing wordt uitgevoerd, [configureren van Azure IoT Suite vooraf geconfigureerde oplossingen voor demonstratiedoeleinden][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="1683b-163">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="1683b-164">Hallo vooraf geconfigureerde oplossing uit uw Azure-account verwijderen wanneer u klaar bent met het gebruik van maken.</span><span class="sxs-lookup"><span data-stu-id="1683b-164">Delete hello preconfigured solution from your Azure account when you have finished using it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1683b-165">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1683b-165">Next steps</span></span>

<span data-ttu-id="1683b-166">Ga naar Hallo [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) voor meer voorbeelden en documentatie over Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="1683b-166">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>


[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/app-output.png
[img-update-progress]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/updateprogress.png
[img-job-status]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/jobstatus.png
[img-list-devices]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/listdevices.png
[img-method-history]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md