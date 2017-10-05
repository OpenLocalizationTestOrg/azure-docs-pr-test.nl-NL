---
title: Verbinding maken met een gateway met een Intel NUC van Azure IoT Suite | Microsoft Docs
description: "Gebruik de Microsoft IoT commerciële Gateway Kit en de vooraf geconfigureerde oplossing voor externe controle. De Azure IoT Edge-gateway gebruiken om in te schakelen van een SensorTag-apparaat verbinding maakt met de oplossing voor externe controle, verzenden van telemetrie naar de cloud en reageren op de methoden die worden aangeroepen vanuit het dashboard van oplossing."
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
ms.date: 07/24/2017
ms.author: dobett
ms.openlocfilehash: bda16be1094276fcecef1e708f9d7db307d94a89
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-azure-iot-edge-gateway-to-the-remote-monitoring-preconfigured-solution-and-send-telemetry-from-a-sensortag"></a><span data-ttu-id="99b16-104">Verbinding maken met uw Azure-IoT-Edge gateway naar de vooraf geconfigureerde oplossing voor externe controle en verzend telemetrie vanuit een SensorTag</span><span class="sxs-lookup"><span data-stu-id="99b16-104">Connect your Azure IoT Edge gateway to the remote monitoring preconfigured solution and send telemetry from a SensorTag</span></span>

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

<span data-ttu-id="99b16-105">Deze zelfstudie laat zien hoe u met Azure IoT rand temperatuur en vochtigheid gegevens van SensorTag apparaat verzenden naar de vooraf geconfigureerde oplossing voor externe controle.</span><span class="sxs-lookup"><span data-stu-id="99b16-105">This tutorial shows you how to use Azure IoT Edge to send temperature and humidity data from SensorTag device to the remote monitoring preconfigured solution.</span></span> <span data-ttu-id="99b16-106">De SensorTag verbindt met de Intel NUC gateway via Bluetooth.</span><span class="sxs-lookup"><span data-stu-id="99b16-106">The SensorTag connects to the Intel NUC gateway using Bluetooth.</span></span> <span data-ttu-id="99b16-107">De zelfstudie wordt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="99b16-107">The tutorial uses:</span></span>

- <span data-ttu-id="99b16-108">Azure IoT-rand voor het implementeren van een voorbeeld-gateway.</span><span class="sxs-lookup"><span data-stu-id="99b16-108">Azure IoT Edge to implement a sample gateway.</span></span>
- <span data-ttu-id="99b16-109">IoT Suite remote monitoring vooraf geconfigureerde oplossing als de cloud-gebaseerde back-end.</span><span class="sxs-lookup"><span data-stu-id="99b16-109">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="99b16-110">Overzicht</span><span class="sxs-lookup"><span data-stu-id="99b16-110">Overview</span></span>

<span data-ttu-id="99b16-111">In deze zelfstudie maakt uitvoeren u de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="99b16-111">In this tutorial, you complete the following steps:</span></span>

- <span data-ttu-id="99b16-112">Implementeer een exemplaar van de vooraf geconfigureerde oplossing voor externe controle op uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="99b16-112">Deploy an instance of the remote monitoring preconfigured solution to your Azure subscription.</span></span> <span data-ttu-id="99b16-113">Deze stap implementeert automatisch en meerdere Azure-services configureert.</span><span class="sxs-lookup"><span data-stu-id="99b16-113">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="99b16-114">Uw gatewayapparaat Intel NUC instellen om te communiceren met uw computer en de oplossing voor externe controle.</span><span class="sxs-lookup"><span data-stu-id="99b16-114">Set up your Intel NUC gateway device to communicate with your computer and the remote monitoring solution.</span></span>
- <span data-ttu-id="99b16-115">Instellen van uw gateway Intel NUC telemetrie van een apparaat SensorTag ontvangen en verzenden naar het dashboard voor externe controle.</span><span class="sxs-lookup"><span data-stu-id="99b16-115">Set up your Intel NUC gateway to receive telemetry from a SensorTag device and send it to the remote monitoring dashboard.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

<span data-ttu-id="99b16-116">[Texas instrumenten uitschakelen SensorTag][lnk-sensortag].</span><span class="sxs-lookup"><span data-stu-id="99b16-116">[Texas Instruments BLE SensorTag][lnk-sensortag].</span></span> <span data-ttu-id="99b16-117">Deze zelfstudie opgehaald telemetrische gegevens via Bluetooth uit het SensorTag-apparaat.</span><span class="sxs-lookup"><span data-stu-id="99b16-117">This tutorial retrieves telemetry data over Bluetooth from the SensorTag device.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="99b16-118">De oplossing voor externe controle levert een set van Azure-services in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="99b16-118">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="99b16-119">De implementatie duidt op een echte enterprise-architectuur.</span><span class="sxs-lookup"><span data-stu-id="99b16-119">The deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="99b16-120">Om te voorkomen dat een Azure-verbruik onnodige kosten, verwijdert u uw exemplaar van de vooraf geconfigureerde oplossing op azureiotsuite.com wanneer u klaar bent met het.</span><span class="sxs-lookup"><span data-stu-id="99b16-120">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="99b16-121">Als u de vooraf geconfigureerde oplossing meer nodig hebt, kunt u het eenvoudig opnieuw.</span><span class="sxs-lookup"><span data-stu-id="99b16-121">If you need the preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="99b16-122">Zie voor meer informatie over het verbruik verminderen terwijl de oplossing voor externe controle wordt uitgevoerd, [configureren van Azure IoT Suite vooraf geconfigureerde oplossingen voor demonstratiedoeleinden][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="99b16-122">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

## <a name="configure-bluetooth-connectivity"></a><span data-ttu-id="99b16-123">Bluetooth-connectiviteit configureren</span><span class="sxs-lookup"><span data-stu-id="99b16-123">Configure Bluetooth connectivity</span></span>

<span data-ttu-id="99b16-124">Bluetooth configureren op de Intel NUC zodat het apparaat SensorTag verbinding maken en verzenden van telemetrie.</span><span class="sxs-lookup"><span data-stu-id="99b16-124">Configure Bluetooth on the Intel NUC to enable the SensorTag device to connect and send telemetry.</span></span>

### <a name="find-the-mac-address-of-the-sensortag"></a><span data-ttu-id="99b16-125">Het MAC-adres van de SensorTag vinden</span><span class="sxs-lookup"><span data-stu-id="99b16-125">Find the MAC address of the SensorTag</span></span>

1. <span data-ttu-id="99b16-126">Voer de volgende opdracht om de blokkering van de Bluetooth-service in de shell op de Intel NUC:</span><span class="sxs-lookup"><span data-stu-id="99b16-126">In the shell on the Intel NUC, run the following command to unblock the Bluetooth service:</span></span>

    ```bash
    sudo rfkill unblock bluetooth
    ```

1. <span data-ttu-id="99b16-127">Voer de volgende opdrachten de Bluetooth-service starten op de Intel NUC en voer de Bluetooth-shell:</span><span class="sxs-lookup"><span data-stu-id="99b16-127">Run the following commands to start the Bluetooth service on the Intel NUC and enter the Bluetooth shell:</span></span>

    ```bash
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. <span data-ttu-id="99b16-128">Voer de volgende opdracht met power op de Bluetooth-controller:</span><span class="sxs-lookup"><span data-stu-id="99b16-128">Run the following command to power on the Bluetooth controller:</span></span>

    ```bash
    power on
    ```

    <span data-ttu-id="99b16-129">Als de domeincontroller ingeschakeld is, ziet u een bericht **power wijzigen op geslaagd**.</span><span class="sxs-lookup"><span data-stu-id="99b16-129">When the controller is on, you see a message **Changing power on succeeded**.</span></span>

1. <span data-ttu-id="99b16-130">Voer de volgende opdracht om te scannen op in de buurt Bluetooth-apparaten:</span><span class="sxs-lookup"><span data-stu-id="99b16-130">Run the following command to scan for nearby Bluetooth devices:</span></span>

    ```bash
    scan on
    ```

1. <span data-ttu-id="99b16-131">Druk op de knop op de SensorTag detecteerbaar.</span><span class="sxs-lookup"><span data-stu-id="99b16-131">Press the power button on the SensorTag to make it discoverable.</span></span> <span data-ttu-id="99b16-132">De groene LED knippert.</span><span class="sxs-lookup"><span data-stu-id="99b16-132">The green LED flashes.</span></span>

1. <span data-ttu-id="99b16-133">Wanneer er een bericht in de shell dat de controller de SensorTag heeft gedetecteerd, noteer het MAC-adres van het apparaat.</span><span class="sxs-lookup"><span data-stu-id="99b16-133">When you see a message in the shell that the controller has discovered the SensorTag, make a note of the MAC address of the device.</span></span> <span data-ttu-id="99b16-134">Het MAC-adres ziet eruit als **A0:E6:F8:B5:F6:00**.</span><span class="sxs-lookup"><span data-stu-id="99b16-134">The MAC address looks like **A0:E6:F8:B5:F6:00**.</span></span> <span data-ttu-id="99b16-135">U moet het MAC-adres verderop in de zelfstudie als u de gateway configureren.</span><span class="sxs-lookup"><span data-stu-id="99b16-135">You need the MAC address later in the tutorial when you configure the gateway.</span></span>

1. <span data-ttu-id="99b16-136">Voer de volgende opdracht Bluetooth scannen uitschakelen:</span><span class="sxs-lookup"><span data-stu-id="99b16-136">Run the following command to turn off Bluetooth scanning:</span></span>

    ```bash
    scan off
    ```

1. <span data-ttu-id="99b16-137">Voer de volgende opdracht om te controleren of u verbinding kunt maken met het SensorTag-apparaat:</span><span class="sxs-lookup"><span data-stu-id="99b16-137">Run the following command to verify that you can connect to the SensorTag device:</span></span>

    ```bash
    connect <SensorTag MAC address>
    ```

    <span data-ttu-id="99b16-138">Als u verbinding is, ziet u het bericht de shell **verbinding tot stand gebracht** en informatie over het apparaat SensorTag afgedrukt.</span><span class="sxs-lookup"><span data-stu-id="99b16-138">If you connect successfully, the shell shows the message **Connection successful** and prints information about the SensorTag device.</span></span> <span data-ttu-id="99b16-139">Als u geen verbinding maken, controleert u dat de SensorTag nog steeds is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="99b16-139">If you cannot connect, check the SensorTag is still powered on.</span></span>

1. <span data-ttu-id="99b16-140">U kunt nu de SensorTag verbreken en de Bluetooth-shell afsluiten met de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="99b16-140">You can now disconnect from the SensorTag and exit the Bluetooth shell by running the following commands:</span></span>

    ```bash
    disconnect
    exit
    ```

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-software](../../includes/iot-suite-gateway-kit-prepare-nuc-software.md)]

## <a name="build-the-custom-iot-edge-module"></a><span data-ttu-id="99b16-141">De aangepaste rand van de IoT-module maken</span><span class="sxs-lookup"><span data-stu-id="99b16-141">Build the custom IoT Edge module</span></span>

<span data-ttu-id="99b16-142">Nu kunt u de aangepaste module IoT rand waarmee de gateway om berichten te verzenden naar de oplossing voor externe controle.</span><span class="sxs-lookup"><span data-stu-id="99b16-142">You can now build the custom IoT Edge module that enables the gateway to send messages to the remote monitoring solution.</span></span> <span data-ttu-id="99b16-143">Zie voor meer informatie over het configureren van een gateway en de rand van de IoT-modules [Azure IoT rand concepten][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="99b16-143">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

<span data-ttu-id="99b16-144">De broncode voor de aangepaste rand van de IoT-modules downloaden van GitHub met de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="99b16-144">Download the source code for the custom IoT Edge modules from GitHub using the following commands:</span></span>

```bash
cd ~
git clone https://github.com/Azure-Samples/iot-remote-monitoring-c-intel-nuc-gateway-getting-started.git
```

<span data-ttu-id="99b16-145">De aangepaste rand van de IoT-module met de volgende opdrachten maken:</span><span class="sxs-lookup"><span data-stu-id="99b16-145">Build the custom IoT Edge module using the following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

<span data-ttu-id="99b16-146">Het script build libsensor2remotemonitoring.so aangepaste IoT Edge-module in de build-map geplaatst.</span><span class="sxs-lookup"><span data-stu-id="99b16-146">The build script places the libsensor2remotemonitoring.so custom IoT Edge module in the build folder.</span></span>

## <a name="configure-and-run-the-iot-edge-gateway"></a><span data-ttu-id="99b16-147">Configureren en uitvoeren van de rand van de IoT-gateway</span><span class="sxs-lookup"><span data-stu-id="99b16-147">Configure and run the IoT Edge gateway</span></span>

<span data-ttu-id="99b16-148">U kunt nu de rand van de IoT-gateway voor het verzenden van telemetrie van uw apparaat SensorTag naar uw dashboard voor externe controle configureren.</span><span class="sxs-lookup"><span data-stu-id="99b16-148">You can now configure the IoT Edge gateway to send telemetry from your SensorTag device to your remote monitoring dashboard.</span></span> <span data-ttu-id="99b16-149">Zie voor meer informatie over het configureren van een gateway en de rand van de IoT-modules [Azure IoT rand concepten][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="99b16-149">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

> [!TIP]
> <span data-ttu-id="99b16-150">In deze zelfstudie gebruikt u de standaard `vi` teksteditor op de Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="99b16-150">In this tutorial, you use the standard `vi` text editor on the Intel NUC.</span></span> <span data-ttu-id="99b16-151">Als u niet hebt gebruikt `vi` , moet u een inleidende zelfstudie, zoals uitvoeren [Unix - de vi zelfstudie Editor] [ lnk-vi-tutorial] om vertrouwd te raken met deze editor.</span><span class="sxs-lookup"><span data-stu-id="99b16-151">If you have not used `vi` before, you should complete an introductory tutorial, such as [Unix - The vi Editor Tutorial][lnk-vi-tutorial] to familiarize yourself with this editor.</span></span> <span data-ttu-id="99b16-152">U kunt ook installeren de gebruikersvriendelijker [nano](https://www.nano-editor.org/) editor met de opdracht `smart install nano -y`.</span><span class="sxs-lookup"><span data-stu-id="99b16-152">Alternatively, you can install the more user-friendly [nano](https://www.nano-editor.org/) editor using the command `smart install nano -y`.</span></span>

<span data-ttu-id="99b16-153">Open het voorbeeldconfiguratiebestand in de **vi** editor met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="99b16-153">Open the sample configuration file in the **vi** editor using the following command:</span></span>

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic/remote_monitoring.json
```

<span data-ttu-id="99b16-154">Zoek de volgende regels in de configuratie voor de IoTHub-module:</span><span class="sxs-lookup"><span data-stu-id="99b16-154">Locate the following lines in the configuration for the IoTHub module:</span></span>

```json
"args": {
  "IoTHubName": "<<Azure IoT Hub Name>>",
  "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
  "Transport": "http"
}
```

<span data-ttu-id="99b16-155">Vervang de tijdelijke aanduiding voor waarden met de IoT Hub informatie u gemaakt en opgeslagen aan het begin van deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="99b16-155">Replace the placeholder values with the IoT Hub information you created and saved at the start of this tutorial.</span></span> <span data-ttu-id="99b16-156">De waarde voor IoTHubName eruit **yourrmsolution37e08**, en is meestal de waarde voor IoTSuffix **azure devices.net**.</span><span class="sxs-lookup"><span data-stu-id="99b16-156">The value for IoTHubName looks like **yourrmsolution37e08**, and the value for IoTSuffix is typically **azure-devices.net**.</span></span>

<span data-ttu-id="99b16-157">Zoek de volgende regels in de configuratie voor de module toewijzing:</span><span class="sxs-lookup"><span data-stu-id="99b16-157">Locate the following lines in the configuration for the mapping module:</span></span>

```json
args": [
  {
    "macAddress": "<<AA:BB:CC:DD:EE:FF>>",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  }
]
```

<span data-ttu-id="99b16-158">Vervang de **macAddress** aanduiding voor items met de MAC-adres van uw SensorTag die u eerder hebt genoteerd.</span><span class="sxs-lookup"><span data-stu-id="99b16-158">Replace the **macAddress** placeholder with the MAC address of your SensorTag you noted previously.</span></span> <span data-ttu-id="99b16-159">Vervang de **deviceID** en **deviceKey** tijdelijke aanduidingen door de id's en sleutels voor de twee apparaten die u eerder in de oplossing voor externe controle hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="99b16-159">Replace the **deviceID** and **deviceKey** placeholders with the IDs and keys for the two devices you created in the remote monitoring solution previously.</span></span>

<span data-ttu-id="99b16-160">Zoek de volgende regels in de configuratie voor de SensorTag-module:</span><span class="sxs-lookup"><span data-stu-id="99b16-160">Locate the following lines in the configuration for the SensorTag module:</span></span>

```json
"args": {
  "controller_index": 0,
  "device_mac_address": "<<AA:BB:CC:DD:EE:FF>>",
  ...
}
```

<span data-ttu-id="99b16-161">Vervang de **apparaat\_mac\_adres** aanduiding voor items met de MAC-adres van uw SensorTag die u eerder hebt genoteerd.</span><span class="sxs-lookup"><span data-stu-id="99b16-161">Replace the **device\_mac\_address** placeholder  with the MAC address of your SensorTag you noted previously.</span></span>

<span data-ttu-id="99b16-162">Sla uw wijzigingen op.</span><span class="sxs-lookup"><span data-stu-id="99b16-162">Save your changes.</span></span>

<span data-ttu-id="99b16-163">U kunt nu de gateway met de volgende opdrachten uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="99b16-163">You can now run the gateway using the following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
/usr/share/azureiotgatewaysdk/samples/ble_gateway/ble_gateway remote_monitoring.json
```

<span data-ttu-id="99b16-164">De gateway aan de rand van de IoT begint op de Intel NUC en verzendt telemetrie van de SensorTag naar de oplossing voor externe controle:</span><span class="sxs-lookup"><span data-stu-id="99b16-164">The IoT Edge gateway starts on the Intel NUC and sends telemetry from the SensorTag to the remote monitoring solution:</span></span>

![Rand IoT gateway verzendt telemetrie van de SensorTag][img-telemetry]

<span data-ttu-id="99b16-166">Druk op **Ctrl-C** om af te sluiten van het programma op elk gewenst moment.</span><span class="sxs-lookup"><span data-stu-id="99b16-166">Press **Ctrl-C** to exit the program at any time.</span></span>

## <a name="view-the-telemetry"></a><span data-ttu-id="99b16-167">De telemetrie weergeven</span><span class="sxs-lookup"><span data-stu-id="99b16-167">View the telemetry</span></span>

<span data-ttu-id="99b16-168">De gateway verzendt nu telemetrie vanaf het SensorTag-apparaat aan de oplossing voor externe controle.</span><span class="sxs-lookup"><span data-stu-id="99b16-168">The gateway is now sending telemetry from the SensorTag device to the remote monitoring solution.</span></span> <span data-ttu-id="99b16-169">U kunt de telemetrie weergeven op het dashboard van oplossing.</span><span class="sxs-lookup"><span data-stu-id="99b16-169">You can view the telemetry on the solution dashboard.</span></span> <span data-ttu-id="99b16-170">U kunt ook opdrachten verzenden naar uw SensorTag-apparaat via de gateway van het dashboard van de oplossing.</span><span class="sxs-lookup"><span data-stu-id="99b16-170">You can also send commands to your SensorTag device through the gateway from the solution dashboard.</span></span>

- <span data-ttu-id="99b16-171">Ga naar het dashboard van de oplossing.</span><span class="sxs-lookup"><span data-stu-id="99b16-171">Navigate to the solution dashboard.</span></span>
- <span data-ttu-id="99b16-172">Selecteer het apparaat dat u hebt geconfigureerd in de gateway die voor de SensorTag in vertegenwoordigt de **apparaat naar de weergave** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="99b16-172">Select the device you configured in the gateway that represents the SensorTag in the **Device to View** dropdown.</span></span>
- <span data-ttu-id="99b16-173">De telemetrie van het apparaat SensorTag wordt weergegeven op het dashboard.</span><span class="sxs-lookup"><span data-stu-id="99b16-173">The telemetry from the SensorTag device displays on the dashboard.</span></span>

![Telemetrie weergegeven van de SensorTag-apparaten][img-telemetry-display]

> [!WARNING]
> <span data-ttu-id="99b16-175">Als u de oplossing voor externe controle uitgevoerd in uw Azure-account laat, wordt u gefactureerd voor de tijd die wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="99b16-175">If you leave the remote monitoring solution running in your Azure account, you are billed for the time it runs.</span></span> <span data-ttu-id="99b16-176">Zie voor meer informatie over het verbruik verminderen terwijl de oplossing voor externe controle wordt uitgevoerd, [configureren van Azure IoT Suite vooraf geconfigureerde oplossingen voor demonstratiedoeleinden][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="99b16-176">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="99b16-177">De vooraf geconfigureerde oplossing verwijderen uit uw Azure-account wanneer u klaar bent met het gebruik van maken.</span><span class="sxs-lookup"><span data-stu-id="99b16-177">Delete the preconfigured solution from your Azure account when you have finished using it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="99b16-178">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="99b16-178">Next steps</span></span>

<span data-ttu-id="99b16-179">Ga naar de [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) voor meer voorbeelden en documentatie over Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="99b16-179">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-telemetry]: ./media/iot-suite-gateway-kit-get-started-sensortag/appoutput.png


[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-sensortag/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-sensortag]: http://www.ti.com/ww/en/wireless_connectivity/sensortag/
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started