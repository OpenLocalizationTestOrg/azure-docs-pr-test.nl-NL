---
title: Verbinding maken met een Pi frambozen Azure IoT Suite-ondersteuning voor firmware-updates met behulp van Node.js | Microsoft Docs
description: Gebruik de Microsoft Azure IoT Starter Kit voor de Raspberry Pi 3 en Azure IoT Suite. Gebruik Node.js verbinding maken met uw frambozen-Pi de oplossing voor externe controle verzenden van telemetrie van sensoren naar de cloud en uitvoeren van een externe firmware-update.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 54503d5d6a636239d240509d7d09cf334234bac7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-raspberry-pi-3-to-the-remote-monitoring-solution-and-enable-remote-firmware-updates-using-nodejs"></a><span data-ttu-id="94353-104">Verbinding maken met uw frambozen Pi 3 van de oplossing voor externe controle en het inschakelen van externe firmware-updates met behulp van Node.js</span><span class="sxs-lookup"><span data-stu-id="94353-104">Connect your Raspberry Pi 3 to the remote monitoring solution and enable remote firmware updates using Node.js</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="94353-105">Deze zelfstudie laat zien hoe u de Microsoft Azure IoT Starter Kit voor frambozen Pi 3 te gebruiken:</span><span class="sxs-lookup"><span data-stu-id="94353-105">This tutorial shows you how to use the Microsoft Azure IoT Starter Kit for Raspberry Pi 3 to:</span></span>

* <span data-ttu-id="94353-106">Ontwikkel een temperatuur en vochtigheid lezer die met de cloud communiceren kan.</span><span class="sxs-lookup"><span data-stu-id="94353-106">Develop a temperature and humidity reader that can communicate with the cloud.</span></span>
* <span data-ttu-id="94353-107">Inschakelen en voer een externe firmware update bijwerken de clienttoepassing op de frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="94353-107">Enable and perform a remote firmware update to update the client application on the Raspberry Pi.</span></span>

<span data-ttu-id="94353-108">De zelfstudie wordt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="94353-108">The tutorial uses:</span></span>

- <span data-ttu-id="94353-109">Raspbian OS, de programmeertaal Node.js en Microsoft Azure IoT SDK voor Node.js voor het implementeren van een voorbeeld-apparaat.</span><span class="sxs-lookup"><span data-stu-id="94353-109">Raspbian OS, the Node.js programming language, and the Microsoft Azure IoT SDK for Node.js to implement a sample device.</span></span>
- <span data-ttu-id="94353-110">IoT Suite remote monitoring vooraf geconfigureerde oplossing als de cloud-gebaseerde back-end.</span><span class="sxs-lookup"><span data-stu-id="94353-110">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="94353-111">Overzicht</span><span class="sxs-lookup"><span data-stu-id="94353-111">Overview</span></span>

<span data-ttu-id="94353-112">In deze zelfstudie maakt uitvoeren u de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="94353-112">In this tutorial, you complete the following steps:</span></span>

- <span data-ttu-id="94353-113">Implementeer een exemplaar van de vooraf geconfigureerde oplossing voor externe controle op uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="94353-113">Deploy an instance of the remote monitoring preconfigured solution to your Azure subscription.</span></span> <span data-ttu-id="94353-114">Deze stap implementeert automatisch en meerdere Azure-services configureert.</span><span class="sxs-lookup"><span data-stu-id="94353-114">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="94353-115">Instellen van het apparaat en de sensoren om te communiceren met uw computer en de oplossing voor externe controle.</span><span class="sxs-lookup"><span data-stu-id="94353-115">Set up your device and sensors to communicate with your computer and the remote monitoring solution.</span></span>
- <span data-ttu-id="94353-116">Werk de voorbeeldcode van de apparaten verbinding maken met de oplossing voor externe controle en verzenden van telemetrie die u op het dashboard van de oplossing weergeven kunt.</span><span class="sxs-lookup"><span data-stu-id="94353-116">Update the sample device code to connect to the remote monitoring solution, and send telemetry that you can view on the solution dashboard.</span></span>
- <span data-ttu-id="94353-117">Met de voorbeeldcode van het apparaat kunt bijwerken van de clienttoepassing.</span><span class="sxs-lookup"><span data-stu-id="94353-117">Use the sample device code to update the client application.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="94353-118">De oplossing voor externe controle levert een set van Azure-services in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="94353-118">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="94353-119">De implementatie duidt op een echte enterprise-architectuur.</span><span class="sxs-lookup"><span data-stu-id="94353-119">The deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="94353-120">Om te voorkomen dat een Azure-verbruik onnodige kosten, verwijdert u uw exemplaar van de vooraf geconfigureerde oplossing op azureiotsuite.com wanneer u klaar bent met het.</span><span class="sxs-lookup"><span data-stu-id="94353-120">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="94353-121">Als u de vooraf geconfigureerde oplossing meer nodig hebt, kunt u het eenvoudig opnieuw.</span><span class="sxs-lookup"><span data-stu-id="94353-121">If you need the preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="94353-122">Zie voor meer informatie over het verbruik verminderen terwijl de oplossing voor externe controle wordt uitgevoerd, [configureren van Azure IoT Suite vooraf geconfigureerde oplossingen voor demonstratiedoeleinden][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="94353-122">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-the-sample"></a><span data-ttu-id="94353-123">Downloaden en configureren van de steekproef</span><span class="sxs-lookup"><span data-stu-id="94353-123">Download and configure the sample</span></span>

<span data-ttu-id="94353-124">U kunt nu downloaden en configureren van de externe clienttoepassing bewaking op uw frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="94353-124">You can now download and configure the remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="94353-125">Node.js installeren</span><span class="sxs-lookup"><span data-stu-id="94353-125">Install Node.js</span></span>

<span data-ttu-id="94353-126">Als u dit nog niet hebt gedaan, installeert u Node.js op uw frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="94353-126">If you haven't done so already, install Node.js on your Raspberry Pi.</span></span> <span data-ttu-id="94353-127">De IoT-SDK voor Node.js vereist versie 0.11.5 van Node.js of hoger.</span><span class="sxs-lookup"><span data-stu-id="94353-127">The IoT SDK for Node.js requires version 0.11.5 of Node.js or later.</span></span> <span data-ttu-id="94353-128">De volgende stappen ziet u hoe Node.js v6.10.2 installeren op uw Pi frambozen:</span><span class="sxs-lookup"><span data-stu-id="94353-128">The following steps show you how to install Node.js v6.10.2 on your Raspberry Pi:</span></span>

1. <span data-ttu-id="94353-129">Gebruik de volgende opdracht om bij te werken uw Pi frambozen:</span><span class="sxs-lookup"><span data-stu-id="94353-129">Use the following command to update your Raspberry Pi:</span></span>

    ```sh
    sudo apt-get update
    ```

1. <span data-ttu-id="94353-130">Gebruik de volgende opdracht voor het downloaden van de Node.js-binaire bestanden naar uw Pi frambozen:</span><span class="sxs-lookup"><span data-stu-id="94353-130">Use the following command to download the Node.js binaries to your Raspberry Pi:</span></span>

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="94353-131">Gebruik de volgende opdracht voor het installeren van de binaire bestanden:</span><span class="sxs-lookup"><span data-stu-id="94353-131">Use the following command to install the binaries:</span></span>

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="94353-132">Gebruik de volgende opdracht om te controleren of dat u hebt de Node.js-v6.10.2 is geïnstalleerd:</span><span class="sxs-lookup"><span data-stu-id="94353-132">Use the following command to verify you have installed Node.js v6.10.2 successfully:</span></span>

    ```sh
    node --version
    ```

### <a name="clone-the-repositories"></a><span data-ttu-id="94353-133">De opslagplaatsen klonen</span><span class="sxs-lookup"><span data-stu-id="94353-133">Clone the repositories</span></span>

<span data-ttu-id="94353-134">Als u dit nog niet hebt gedaan, moet u de vereiste opslagplaatsen klonen door de volgende opdrachten uitvoeren op uw Pi:</span><span class="sxs-lookup"><span data-stu-id="94353-134">If you haven't done so already, clone the required repositories by running the following commands on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git
```

### <a name="update-the-device-connection-string"></a><span data-ttu-id="94353-135">De verbindingsreeks apparaat bijwerken</span><span class="sxs-lookup"><span data-stu-id="94353-135">Update the device connection string</span></span>

<span data-ttu-id="94353-136">Open het voorbeeldconfiguratiebestand in de **nano** editor met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="94353-136">Open the sample configuration file in the **nano** editor using the following command:</span></span>

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advanced/config/deviceinfo
```

<span data-ttu-id="94353-137">Vervang de tijdelijke aanduiding voor waarden met de apparaat-id en IoT Hub gegevens u gemaakt en opgeslagen aan het begin van deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="94353-137">Replace the placeholder values with the device id and IoT Hub information you created and saved at the start of this tutorial.</span></span>

<span data-ttu-id="94353-138">Wanneer u klaar bent, wordt de inhoud van het bestand deviceinfo moeten eruitzien als in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="94353-138">When you are done, the contents of the deviceinfo file should look like the following example:</span></span>

```conf
yourdeviceid
HostName=youriothubname.azure-devices.net;DeviceId=yourdeviceid;SharedAccessKey=yourdevicekey
```

<span data-ttu-id="94353-139">Sla de wijzigingen (**Ctrl-O**, **Enter**) en sluit de editor af (**Ctrl X**).</span><span class="sxs-lookup"><span data-stu-id="94353-139">Save your changes (**Ctrl-O**, **Enter**) and exit the editor (**Ctrl-X**).</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="94353-140">Het voorbeeld uitvoert</span><span class="sxs-lookup"><span data-stu-id="94353-140">Run the sample</span></span>

<span data-ttu-id="94353-141">Voer de volgende opdrachten voor het installeren van de vereiste pakketten voor de steekproef:</span><span class="sxs-lookup"><span data-stu-id="94353-141">Run the following commands to install the prerequisite packages for the sample:</span></span>

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advance/1.0
npm install
```

<span data-ttu-id="94353-142">U kunt nu het voorbeeldprogramma uitvoeren op de frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="94353-142">You can now run the sample program on the Raspberry Pi.</span></span> <span data-ttu-id="94353-143">Voer de opdracht:</span><span class="sxs-lookup"><span data-stu-id="94353-143">Enter the command:</span></span>

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advanced/1.0/remote_monitoring.js
```

<span data-ttu-id="94353-144">De volgende voorbeelduitvoer volgt een voorbeeld van de uitvoer die u bij de opdrachtprompt op de Pi frambozen zien:</span><span class="sxs-lookup"><span data-stu-id="94353-144">The following sample output is an example of the output you see at the command prompt on the Raspberry Pi:</span></span>

![De uitvoer van de app Raspberry Pi][img-raspberry-output]

<span data-ttu-id="94353-146">Druk op **Ctrl-C** om af te sluiten van het programma op elk gewenst moment.</span><span class="sxs-lookup"><span data-stu-id="94353-146">Press **Ctrl-C** to exit the program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-advanced](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-advanced.md)]

1. <span data-ttu-id="94353-147">Klik in het dashboard van de oplossing op **apparaten** bezoeken de **apparaten** pagina.</span><span class="sxs-lookup"><span data-stu-id="94353-147">In the solution dashboard, click **Devices** to visit the **Devices** page.</span></span> <span data-ttu-id="94353-148">Selecteer uw Raspberry Pi in de **lijst met apparaten**.</span><span class="sxs-lookup"><span data-stu-id="94353-148">Select your Raspberry Pi in the **Device List**.</span></span> <span data-ttu-id="94353-149">Kies vervolgens **methoden**:</span><span class="sxs-lookup"><span data-stu-id="94353-149">Then choose **Methods**:</span></span>

    ![Lijst met apparaten in het dashboard][img-list-devices]

1. <span data-ttu-id="94353-151">Op de **methode Invoke** pagina **InitiateFirmwareUpdate** in de **methode** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="94353-151">On the **Invoke Method** page, choose **InitiateFirmwareUpdate** in the **Method** dropdown.</span></span>

1. <span data-ttu-id="94353-152">In de **FWPackageURI** veld **https://raw.githubusercontent.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit/master/advanced/2.0/raspberry.js**.</span><span class="sxs-lookup"><span data-stu-id="94353-152">In the **FWPackageURI** field, enter **https://raw.githubusercontent.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit/master/advanced/2.0/raspberry.js**.</span></span> <span data-ttu-id="94353-153">Dit bestand bevat de implementatie van versie 2.0 van de firmware.</span><span class="sxs-lookup"><span data-stu-id="94353-153">This file contains the implementation of version 2.0 of the firmware.</span></span>

1. <span data-ttu-id="94353-154">Kies **InvokeMethod**.</span><span class="sxs-lookup"><span data-stu-id="94353-154">Choose **InvokeMethod**.</span></span> <span data-ttu-id="94353-155">De app op de Pi frambozen stuurt een bevestiging terug naar het dashboard van de oplossing.</span><span class="sxs-lookup"><span data-stu-id="94353-155">The app on the Raspberry Pi sends an acknowledgment back to the solution dashboard.</span></span> <span data-ttu-id="94353-156">Vervolgens wordt het updateproces firmware gestart door de nieuwe versie van de firmware te downloaden:</span><span class="sxs-lookup"><span data-stu-id="94353-156">It then starts the firmware update process by downloading the new version of the firmware:</span></span>

    ![Overzicht van de methode weergeven][img-method-history]

## <a name="observe-the-firmware-update-process"></a><span data-ttu-id="94353-158">Houd rekening met de firmware proces niet bijwerken</span><span class="sxs-lookup"><span data-stu-id="94353-158">Observe the firmware update process</span></span>

<span data-ttu-id="94353-159">U kunt zien dat de firmware proces niet bijwerken omdat deze wordt uitgevoerd op het apparaat en de gerapporteerde door eigenschappen te bekijken in het dashboard van oplossing:</span><span class="sxs-lookup"><span data-stu-id="94353-159">You can observe the firmware update process as it runs on the device and by viewing the reported properties in the solution dashboard:</span></span>

1. <span data-ttu-id="94353-160">U kunt de voortgang op van het updateproces bekijken op de Pi frambozen:</span><span class="sxs-lookup"><span data-stu-id="94353-160">You can view the progress in of the update process on the Raspberry Pi:</span></span>

    ![Voortgang van bijwerken weergeven][img-update-progress]

    > [!NOTE]
    > <span data-ttu-id="94353-162">De externe controle app achtergrond opnieuw opgestart wanneer de update is voltooid.</span><span class="sxs-lookup"><span data-stu-id="94353-162">The remote monitoring app restarts silently when the update completes.</span></span> <span data-ttu-id="94353-163">Gebruik de opdracht `ps -ef` om te controleren of deze wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="94353-163">Use the command `ps -ef` to verify it is running.</span></span> <span data-ttu-id="94353-164">Als u het proces is beëindigd wilt, gebruikt u de `kill` opdracht met de proces-id.</span><span class="sxs-lookup"><span data-stu-id="94353-164">If you want to terminate the process, use the `kill` command with the process id.</span></span>

1. <span data-ttu-id="94353-165">U kunt de status van de firmware-update weergeven, zoals gemeld door het apparaat, in de portal van de oplossing.</span><span class="sxs-lookup"><span data-stu-id="94353-165">You can view the status of the firmware update, as reported by the device, in the solution portal.</span></span> <span data-ttu-id="94353-166">De volgende schermafbeelding ziet u de status en de duur van elke fase van het updateproces kan controleren en de nieuwe firmwareversie:</span><span class="sxs-lookup"><span data-stu-id="94353-166">The following screenshot shows the status and duration of each stage of the update process, and the new firmware version:</span></span>

    ![De status van de taak weergeven][img-job-status]

    <span data-ttu-id="94353-168">Als u terug naar het dashboard navigeert, kunt u controleren of dat het apparaat is nog steeds verzenden van telemetrie na de firmware-update.</span><span class="sxs-lookup"><span data-stu-id="94353-168">If you navigate back to the dashboard, you can verify the device is still sending telemetry following the firmware update.</span></span>

> [!WARNING]
> <span data-ttu-id="94353-169">Als u de oplossing voor externe controle uitgevoerd in uw Azure-account laat, wordt u gefactureerd voor de tijd die wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="94353-169">If you leave the remote monitoring solution running in your Azure account, you are billed for the time it runs.</span></span> <span data-ttu-id="94353-170">Zie voor meer informatie over het verbruik verminderen terwijl de oplossing voor externe controle wordt uitgevoerd, [configureren van Azure IoT Suite vooraf geconfigureerde oplossingen voor demonstratiedoeleinden][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="94353-170">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="94353-171">De vooraf geconfigureerde oplossing verwijderen uit uw Azure-account wanneer u klaar bent met het gebruik van maken.</span><span class="sxs-lookup"><span data-stu-id="94353-171">Delete the preconfigured solution from your Azure account when you have finished using it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="94353-172">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="94353-172">Next steps</span></span>

<span data-ttu-id="94353-173">Ga naar de [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) voor meer voorbeelden en documentatie over Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="94353-173">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>


[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/app-output.png
[img-update-progress]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/updateprogress.png
[img-job-status]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/jobstatus.png
[img-list-devices]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/listdevices.png
[img-method-history]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
