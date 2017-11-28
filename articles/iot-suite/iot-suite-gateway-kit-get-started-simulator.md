---
title: Verbinding maken met een gateway met een Intel NUC van Azure IoT Suite | Microsoft Docs
description: "Gebruik de Microsoft IoT commerciële Gateway Kit en de vooraf geconfigureerde oplossing voor externe controle. Gebruik de rand van Azure IoT gateway verbinding maken met de oplossing voor externe controle, gesimuleerde telemetrie verzenden naar de cloud en reageren op de methoden die worden aangeroepen vanuit het dashboard van oplossing."
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
ms.openlocfilehash: 9ed57d3c23e2adbd42c054f33c8ed46e3d6c9792
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-azure-iot-edge-gateway-to-the-remote-monitoring-preconfigured-solution-and-send-simulated-telemetry"></a><span data-ttu-id="3f7a0-104">Verbinding maken met uw Azure-IoT-Edge gateway naar de vooraf geconfigureerde oplossing voor externe controle en gesimuleerde telemetrie verzenden</span><span class="sxs-lookup"><span data-stu-id="3f7a0-104">Connect your Azure IoT Edge gateway to the remote monitoring preconfigured solution and send simulated telemetry</span></span>

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

<span data-ttu-id="3f7a0-105">Deze zelfstudie laat zien hoe u met Azure IoT rand temperatuur en vochtigheid gegevens worden verzonden naar de vooraf geconfigureerde oplossing voor externe controle te simuleren.</span><span class="sxs-lookup"><span data-stu-id="3f7a0-105">This tutorial shows you how to use Azure IoT Edge to simulate temperature and humidity data to send to the remote monitoring preconfigured solution.</span></span> <span data-ttu-id="3f7a0-106">De zelfstudie wordt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="3f7a0-106">The tutorial uses:</span></span>

- <span data-ttu-id="3f7a0-107">Azure IoT-rand voor het implementeren van een voorbeeld-gateway.</span><span class="sxs-lookup"><span data-stu-id="3f7a0-107">Azure IoT Edge to implement a sample gateway.</span></span>
- <span data-ttu-id="3f7a0-108">IoT Suite remote monitoring vooraf geconfigureerde oplossing als de cloud-gebaseerde back-end.</span><span class="sxs-lookup"><span data-stu-id="3f7a0-108">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="3f7a0-109">Overzicht</span><span class="sxs-lookup"><span data-stu-id="3f7a0-109">Overview</span></span>

<span data-ttu-id="3f7a0-110">In deze zelfstudie maakt uitvoeren u de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="3f7a0-110">In this tutorial, you complete the following steps:</span></span>

- <span data-ttu-id="3f7a0-111">Implementeer een exemplaar van de vooraf geconfigureerde oplossing voor externe controle op uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="3f7a0-111">Deploy an instance of the remote monitoring preconfigured solution to your Azure subscription.</span></span> <span data-ttu-id="3f7a0-112">Deze stap implementeert automatisch en meerdere Azure-services configureert.</span><span class="sxs-lookup"><span data-stu-id="3f7a0-112">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="3f7a0-113">Uw gatewayapparaat Intel NUC instellen om te communiceren met uw computer en de oplossing voor externe controle.</span><span class="sxs-lookup"><span data-stu-id="3f7a0-113">Set up your Intel NUC gateway device to communicate with your computer and the remote monitoring solution.</span></span>
- <span data-ttu-id="3f7a0-114">De rand van de IoT-gateway voor het verzenden van de gesimuleerde telemetrie die u op het dashboard van de oplossing weergeven kunt configureren.</span><span class="sxs-lookup"><span data-stu-id="3f7a0-114">Configure the IoT Edge gateway to send simulated telemetry that you can view on the solution dashboard.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="3f7a0-115">De oplossing voor externe controle levert een set van Azure-services in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="3f7a0-115">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="3f7a0-116">De implementatie duidt op een echte enterprise-architectuur.</span><span class="sxs-lookup"><span data-stu-id="3f7a0-116">The deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="3f7a0-117">Om te voorkomen dat een Azure-verbruik onnodige kosten, verwijdert u uw exemplaar van de vooraf geconfigureerde oplossing op azureiotsuite.com wanneer u klaar bent met het.</span><span class="sxs-lookup"><span data-stu-id="3f7a0-117">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="3f7a0-118">Als u de vooraf geconfigureerde oplossing meer nodig hebt, kunt u het eenvoudig opnieuw.</span><span class="sxs-lookup"><span data-stu-id="3f7a0-118">If you need the preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="3f7a0-119">Zie voor meer informatie over het verbruik verminderen terwijl de oplossing voor externe controle wordt uitgevoerd, [configureren van Azure IoT Suite vooraf geconfigureerde oplossingen voor demonstratiedoeleinden][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="3f7a0-119">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

<span data-ttu-id="3f7a0-120">Herhaal de vorige stappen voor het toevoegen van een tweede apparaat met een apparaat-ID, zoals **device02**.</span><span class="sxs-lookup"><span data-stu-id="3f7a0-120">Repeat the previous steps to add a second device using a Device ID such as **device02**.</span></span> <span data-ttu-id="3f7a0-121">Het voorbeeld verzendt de gegevens van twee gesimuleerde apparaten in de gateway naar de oplossing voor externe controle.</span><span class="sxs-lookup"><span data-stu-id="3f7a0-121">The sample sends data from two simulated devices in the gateway to the remote monitoring solution.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-software](../../includes/iot-suite-gateway-kit-prepare-nuc-software.md)]

## <a name="build-the-custom-iot-edge-module"></a><span data-ttu-id="3f7a0-122">De aangepaste rand van de IoT-module maken</span><span class="sxs-lookup"><span data-stu-id="3f7a0-122">Build the custom IoT Edge module</span></span>

<span data-ttu-id="3f7a0-123">Nu kunt u de aangepaste module IoT rand waarmee de gateway om berichten te verzenden naar de oplossing voor externe controle.</span><span class="sxs-lookup"><span data-stu-id="3f7a0-123">You can now build the custom IoT Edge module that enables the gateway to send messages to the remote monitoring solution.</span></span> <span data-ttu-id="3f7a0-124">Zie voor meer informatie over het configureren van een gateway en de rand van de IoT-modules [Azure IoT rand concepten][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="3f7a0-124">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

<span data-ttu-id="3f7a0-125">De broncode voor de aangepaste rand van de IoT-modules downloaden van GitHub met de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="3f7a0-125">Download the source code for the custom IoT Edge modules from GitHub using the following commands:</span></span>

```bash
cd ~
git clone https://github.com/Azure-Samples/iot-remote-monitoring-c-intel-nuc-gateway-getting-started.git
```

<span data-ttu-id="3f7a0-126">De aangepaste rand van de IoT-module met de volgende opdrachten maken:</span><span class="sxs-lookup"><span data-stu-id="3f7a0-126">Build the custom IoT Edge module using the following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

<span data-ttu-id="3f7a0-127">Het script build libsimulator.so aangepaste IoT Edge-module in de build-map geplaatst.</span><span class="sxs-lookup"><span data-stu-id="3f7a0-127">The build script places the libsimulator.so custom IoT Edge module in the build folder.</span></span>

## <a name="configure-and-run-the-iot-edge-gateway"></a><span data-ttu-id="3f7a0-128">Configureren en uitvoeren van de rand van de IoT-gateway</span><span class="sxs-lookup"><span data-stu-id="3f7a0-128">Configure and run the IoT Edge gateway</span></span>

<span data-ttu-id="3f7a0-129">U kunt nu de rand van de IoT-gateway voor het gesimuleerde telemetrie verzenden naar uw dashboard voor externe controle configureren.</span><span class="sxs-lookup"><span data-stu-id="3f7a0-129">You can now configure the IoT Edge gateway to send simulated telemetry to your remote monitoring dashboard.</span></span> <span data-ttu-id="3f7a0-130">Zie voor meer informatie over het configureren van een gateway en de rand van de IoT-modules [Azure IoT rand concepten][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="3f7a0-130">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

> [!TIP]
> <span data-ttu-id="3f7a0-131">In deze zelfstudie gebruikt u de standaard `vi` teksteditor op de Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="3f7a0-131">In this tutorial, you use the standard `vi` text editor on the Intel NUC.</span></span> <span data-ttu-id="3f7a0-132">Als u niet hebt gebruikt `vi` , moet u een inleidende zelfstudie, zoals uitvoeren [Unix - de vi zelfstudie Editor] [ lnk-vi-tutorial] om vertrouwd te raken met deze editor.</span><span class="sxs-lookup"><span data-stu-id="3f7a0-132">If you have not used `vi` before, you should complete an introductory tutorial, such as [Unix - The vi Editor Tutorial][lnk-vi-tutorial] to familiarize yourself with this editor.</span></span> <span data-ttu-id="3f7a0-133">U kunt ook installeren de gebruikersvriendelijker [nano](https://www.nano-editor.org/) editor met de opdracht `smart install nano -y`.</span><span class="sxs-lookup"><span data-stu-id="3f7a0-133">Alternatively, you can install the more user-friendly [nano](https://www.nano-editor.org/) editor using the command `smart install nano -y`.</span></span>

<span data-ttu-id="3f7a0-134">Open het voorbeeldconfiguratiebestand in de **vi** editor met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="3f7a0-134">Open the sample configuration file in the **vi** editor using the following command:</span></span>

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator/remote_monitoring.json
```

<span data-ttu-id="3f7a0-135">Zoek de volgende regels in de configuratie voor de IoTHub-module:</span><span class="sxs-lookup"><span data-stu-id="3f7a0-135">Locate the following lines in the configuration for the IoTHub module:</span></span>

```json
"args": {
  "IoTHubName": "<<Azure IoT Hub Name>>",
  "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
  "Transport": "http"
}
```

<span data-ttu-id="3f7a0-136">Vervang de tijdelijke aanduiding voor waarden met de IoT Hub informatie u gemaakt en opgeslagen aan het begin van deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="3f7a0-136">Replace the placeholder values with the IoT Hub information you created and saved at the start of this tutorial.</span></span> <span data-ttu-id="3f7a0-137">De waarde voor IoTHubName eruit **yourrmsolution37e08**, en is meestal de waarde voor IoTSuffix **azure devices.net**.</span><span class="sxs-lookup"><span data-stu-id="3f7a0-137">The value for IoTHubName looks like **yourrmsolution37e08**, and the value for IoTSuffix is typically **azure-devices.net**.</span></span>

<span data-ttu-id="3f7a0-138">Zoek de volgende regels in de configuratie voor de module toewijzing:</span><span class="sxs-lookup"><span data-stu-id="3f7a0-138">Locate the following lines in the configuration for the mapping module:</span></span>

```json
args": [
  {
    "macAddress": "AA:BB:CC:DD:EE:FF",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  },
  {
    "macAddress": "AA:BB:CC:DD:EE:FF",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  }
]
```

<span data-ttu-id="3f7a0-139">Vervang de **deviceID** en **deviceKey** tijdelijke aanduidingen door de id's en sleutels voor de twee apparaten die u eerder in de oplossing voor externe controle hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3f7a0-139">Replace the **deviceID** and **deviceKey** placeholders with the IDs and keys for the two devices you created in the remote monitoring solution previously.</span></span>

<span data-ttu-id="3f7a0-140">Sla uw wijzigingen op.</span><span class="sxs-lookup"><span data-stu-id="3f7a0-140">Save your changes.</span></span>

<span data-ttu-id="3f7a0-141">U kunt nu de rand van de IoT-gateway met de volgende opdrachten uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="3f7a0-141">You can now run the IoT Edge gateway using the following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
/usr/share/azureiotgatewaysdk/samples/simulated_device_cloud_upload/simulated_device_cloud_upload remote_monitoring.json
```

<span data-ttu-id="3f7a0-142">De gateway wordt gestart op de Intel NUC en gesimuleerde telemetrie verzendt naar de oplossing voor externe controle:</span><span class="sxs-lookup"><span data-stu-id="3f7a0-142">The gateway starts on the Intel NUC and sends simulated telemetry to the remote monitoring solution:</span></span>

![Gateway aan de rand van de IoT gesimuleerde telemetrie genereert][img-simulated telemetry]

<span data-ttu-id="3f7a0-144">Druk op **Ctrl-C** om af te sluiten van het programma op elk gewenst moment.</span><span class="sxs-lookup"><span data-stu-id="3f7a0-144">Press **Ctrl-C** to exit the program at any time.</span></span>

## <a name="view-the-telemetry"></a><span data-ttu-id="3f7a0-145">De telemetrie weergeven</span><span class="sxs-lookup"><span data-stu-id="3f7a0-145">View the telemetry</span></span>

<span data-ttu-id="3f7a0-146">De rand van de IoT-gateway is nu gesimuleerde telemetrie verzenden naar de oplossing voor externe controle.</span><span class="sxs-lookup"><span data-stu-id="3f7a0-146">The IoT Edge gateway is now sending simulated telemetry to the remote monitoring solution.</span></span> <span data-ttu-id="3f7a0-147">U kunt de telemetrie weergeven op het dashboard van oplossing.</span><span class="sxs-lookup"><span data-stu-id="3f7a0-147">You can view the telemetry on the solution dashboard.</span></span>

- <span data-ttu-id="3f7a0-148">Ga naar het dashboard van de oplossing.</span><span class="sxs-lookup"><span data-stu-id="3f7a0-148">Navigate to the solution dashboard.</span></span>
- <span data-ttu-id="3f7a0-149">Selecteer een van de twee apparaten die u hebt geconfigureerd in de gateway in de **apparaat naar de weergave** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="3f7a0-149">Select one of the two devices you configured in the gateway in the **Device to View** dropdown.</span></span>
- <span data-ttu-id="3f7a0-150">De telemetrie van de gatewayapparaten wordt weergegeven op het dashboard.</span><span class="sxs-lookup"><span data-stu-id="3f7a0-150">The telemetry from the gateway devices displays on the dashboard.</span></span>

![Telemetrie weergegeven van de gesimuleerde gatewayapparaten][img-telemetry-display]

> [!WARNING]
> <span data-ttu-id="3f7a0-152">Als u de oplossing voor externe controle uitgevoerd in uw Azure-account laat, wordt u gefactureerd voor de tijd die wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3f7a0-152">If you leave the remote monitoring solution running in your Azure account, you are billed for the time it runs.</span></span> <span data-ttu-id="3f7a0-153">Zie voor meer informatie over het verbruik verminderen terwijl de oplossing voor externe controle wordt uitgevoerd, [configureren van Azure IoT Suite vooraf geconfigureerde oplossingen voor demonstratiedoeleinden][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="3f7a0-153">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="3f7a0-154">De vooraf geconfigureerde oplossing verwijderen uit uw Azure-account wanneer u klaar bent met het gebruik van maken.</span><span class="sxs-lookup"><span data-stu-id="3f7a0-154">Delete the preconfigured solution from your Azure account when you have finished using it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3f7a0-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3f7a0-155">Next steps</span></span>

<span data-ttu-id="3f7a0-156">Ga naar de [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) voor meer voorbeelden en documentatie over Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="3f7a0-156">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-simulated telemetry]: ./media/iot-suite-gateway-kit-get-started-simulator/appoutput.png

[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-simulator/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md

[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started