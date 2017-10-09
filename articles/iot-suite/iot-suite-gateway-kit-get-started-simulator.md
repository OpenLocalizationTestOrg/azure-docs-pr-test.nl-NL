---
title: een gateway tooAzure IoT-Suite met een Intel NUC aaaConnect | Microsoft Docs
description: "Gebruik Hallo Microsoft IoT commerciële Gateway Kit en Hallo vooraf geconfigureerde oplossing voor externe controle. Gebruik hello Azure IoT Edge gateway tooconnect toohello oplossing voor externe controle, gesimuleerde telemetrie toohello cloud verzenden en reageren toomethods aangeroepen vanuit Hallo oplossing dashboard."
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
ms.openlocfilehash: 46b545fc21b054191c8f78ace20fc628f839a819
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-azure-iot-edge-gateway-toohello-remote-monitoring-preconfigured-solution-and-send-simulated-telemetry"></a><span data-ttu-id="9d347-104">Verbinding maken met uw vooraf geconfigureerde oplossing voor externe controle rand van Azure IoT gateway toohello en gesimuleerde telemetrie verzenden</span><span class="sxs-lookup"><span data-stu-id="9d347-104">Connect your Azure IoT Edge gateway toohello remote monitoring preconfigured solution and send simulated telemetry</span></span>

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

<span data-ttu-id="9d347-105">Deze zelfstudie leert u hoe toouse Azure IoT rand toosimulate temperatuur en vochtigheid gegevens toosend toohello externe controle vooraf oplossing geconfigureerde.</span><span class="sxs-lookup"><span data-stu-id="9d347-105">This tutorial shows you how toouse Azure IoT Edge toosimulate temperature and humidity data toosend toohello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="9d347-106">Hallo-zelfstudie wordt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="9d347-106">hello tutorial uses:</span></span>

- <span data-ttu-id="9d347-107">Azure IoT rand tooimplement een voorbeeld-gateway.</span><span class="sxs-lookup"><span data-stu-id="9d347-107">Azure IoT Edge tooimplement a sample gateway.</span></span>
- <span data-ttu-id="9d347-108">Hallo IoT Suite remote monitoring vooraf geconfigureerde oplossing als Hallo cloud-gebaseerde back-end.</span><span class="sxs-lookup"><span data-stu-id="9d347-108">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="9d347-109">Overzicht</span><span class="sxs-lookup"><span data-stu-id="9d347-109">Overview</span></span>

<span data-ttu-id="9d347-110">In deze zelfstudie maakt uitvoeren u Hallo stappen:</span><span class="sxs-lookup"><span data-stu-id="9d347-110">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="9d347-111">Implementeer een exemplaar van Hallo externe controle vooraf geconfigureerde oplossing tooyour Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="9d347-111">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="9d347-112">Deze stap implementeert automatisch en meerdere Azure-services configureert.</span><span class="sxs-lookup"><span data-stu-id="9d347-112">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="9d347-113">Stel uw toocommunicate Intel NUC gateway-apparaat met de computer en het Hallo-oplossing voor externe controle.</span><span class="sxs-lookup"><span data-stu-id="9d347-113">Set up your Intel NUC gateway device toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="9d347-114">Hallo rand IoT gateway toosend gesimuleerde telemetrie die u op het dashboard van de oplossing Hallo weergeven kunt configureren.</span><span class="sxs-lookup"><span data-stu-id="9d347-114">Configure hello IoT Edge gateway toosend simulated telemetry that you can view on hello solution dashboard.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="9d347-115">Hallo externe controle van de bepalingen van de oplossing voor een verzameling Azure-services in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="9d347-115">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="9d347-116">Hallo implementatie duidt op een echte enterprise-architectuur.</span><span class="sxs-lookup"><span data-stu-id="9d347-116">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="9d347-117">tooavoid onnodige Azure-verbruik kosten, verwijderen van uw exemplaar van Hallo vooraf geconfigureerde oplossing op azureiotsuite.com wanneer u klaar bent met het.</span><span class="sxs-lookup"><span data-stu-id="9d347-117">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="9d347-118">Als u moet de vooraf geconfigureerde oplossing opnieuw hello, u kunt gemakkelijk het opnieuw maken.</span><span class="sxs-lookup"><span data-stu-id="9d347-118">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="9d347-119">Zie voor meer informatie over het verminderen van verbruik tijdens het Hallo voor externe controle van de oplossing wordt uitgevoerd, [configureren van Azure IoT Suite vooraf geconfigureerde oplossingen voor demonstratiedoeleinden][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="9d347-119">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

<span data-ttu-id="9d347-120">Herhaal de vorige stappen tooadd Hallo een tweede apparaat met een apparaat-ID, zoals **device02**.</span><span class="sxs-lookup"><span data-stu-id="9d347-120">Repeat hello previous steps tooadd a second device using a Device ID such as **device02**.</span></span> <span data-ttu-id="9d347-121">Hallo-voorbeeld worden gegevens verzonden van twee gesimuleerde apparaten Hallo gateway toohello oplossing voor externe controle.</span><span class="sxs-lookup"><span data-stu-id="9d347-121">hello sample sends data from two simulated devices in hello gateway toohello remote monitoring solution.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-software](../../includes/iot-suite-gateway-kit-prepare-nuc-software.md)]

## <a name="build-hello-custom-iot-edge-module"></a><span data-ttu-id="9d347-122">Hallo aangepaste IoT Edge-module maken</span><span class="sxs-lookup"><span data-stu-id="9d347-122">Build hello custom IoT Edge module</span></span>

<span data-ttu-id="9d347-123">U kunt nu Hallo aangepaste IoT Edge-module maken waarmee Hallo gateway toosend berichten toohello oplossing voor externe controle.</span><span class="sxs-lookup"><span data-stu-id="9d347-123">You can now build hello custom IoT Edge module that enables hello gateway toosend messages toohello remote monitoring solution.</span></span> <span data-ttu-id="9d347-124">Zie voor meer informatie over het configureren van een gateway en de rand van de IoT-modules [Azure IoT rand concepten][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="9d347-124">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

<span data-ttu-id="9d347-125">Download de broncode Hallo voor aangepaste modules die IoT rand Hallo vanuit GitHub Hallo volgende opdrachten gebruiken:</span><span class="sxs-lookup"><span data-stu-id="9d347-125">Download hello source code for hello custom IoT Edge modules from GitHub using hello following commands:</span></span>

```bash
cd ~
git clone https://github.com/Azure-Samples/iot-remote-monitoring-c-intel-nuc-gateway-getting-started.git
```

<span data-ttu-id="9d347-126">Hallo aangepaste IoT Edge-module met behulp van de volgende opdrachten Hallo maken:</span><span class="sxs-lookup"><span data-stu-id="9d347-126">Build hello custom IoT Edge module using hello following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

<span data-ttu-id="9d347-127">Hallo build script Hallo libsimulator.so aangepaste IoT rand module in Hallo build-map geplaatst.</span><span class="sxs-lookup"><span data-stu-id="9d347-127">hello build script places hello libsimulator.so custom IoT Edge module in hello build folder.</span></span>

## <a name="configure-and-run-hello-iot-edge-gateway"></a><span data-ttu-id="9d347-128">Configureren en uitvoeren van Hallo rand IoT gateway</span><span class="sxs-lookup"><span data-stu-id="9d347-128">Configure and run hello IoT Edge gateway</span></span>

<span data-ttu-id="9d347-129">U kunt nu Hallo rand IoT gateway toosend gesimuleerde telemetrie tooyour dashboard externe controle configureren.</span><span class="sxs-lookup"><span data-stu-id="9d347-129">You can now configure hello IoT Edge gateway toosend simulated telemetry tooyour remote monitoring dashboard.</span></span> <span data-ttu-id="9d347-130">Zie voor meer informatie over het configureren van een gateway en de rand van de IoT-modules [Azure IoT rand concepten][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="9d347-130">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

> [!TIP]
> <span data-ttu-id="9d347-131">In deze zelfstudie gebruikt u Hallo standaard `vi` teksteditor op Hallo Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="9d347-131">In this tutorial, you use hello standard `vi` text editor on hello Intel NUC.</span></span> <span data-ttu-id="9d347-132">Als u niet hebt gebruikt `vi` , moet u een inleidende zelfstudie, zoals uitvoeren [Unix - Hallo vi zelfstudie Editor] [ lnk-vi-tutorial] toofamiliarize uzelf met deze editor.</span><span class="sxs-lookup"><span data-stu-id="9d347-132">If you have not used `vi` before, you should complete an introductory tutorial, such as [Unix - hello vi Editor Tutorial][lnk-vi-tutorial] toofamiliarize yourself with this editor.</span></span> <span data-ttu-id="9d347-133">U kunt ook installeren Hallo gebruikersvriendelijker [nano](https://www.nano-editor.org/) editor met Hallo opdracht `smart install nano -y`.</span><span class="sxs-lookup"><span data-stu-id="9d347-133">Alternatively, you can install hello more user-friendly [nano](https://www.nano-editor.org/) editor using hello command `smart install nano -y`.</span></span>

<span data-ttu-id="9d347-134">Open Hallo voorbeeldconfiguratiebestand in Hallo **vi** editor met behulp van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="9d347-134">Open hello sample configuration file in hello **vi** editor using hello following command:</span></span>

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator/remote_monitoring.json
```

<span data-ttu-id="9d347-135">Zoek de volgende regels in de configuratie voor Hallo IoTHub module Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="9d347-135">Locate hello following lines in hello configuration for hello IoTHub module:</span></span>

```json
"args": {
  "IoTHubName": "<<Azure IoT Hub Name>>",
  "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
  "Transport": "http"
}
```

<span data-ttu-id="9d347-136">Hallo-tijdelijke aanduiding voor waarden met IoT Hub informatie u gemaakt en opgeslagen op Hallo Hallo begin van deze zelfstudie wordt vervangen.</span><span class="sxs-lookup"><span data-stu-id="9d347-136">Replace hello placeholder values with hello IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="9d347-137">Hallo-waarde voor IoTHubName eruit **yourrmsolution37e08**, en het Hallo-waarde voor IoTSuffix is doorgaans **azure devices.net**.</span><span class="sxs-lookup"><span data-stu-id="9d347-137">hello value for IoTHubName looks like **yourrmsolution37e08**, and hello value for IoTSuffix is typically **azure-devices.net**.</span></span>

<span data-ttu-id="9d347-138">Zoek de volgende regels in de configuratie voor Hallo toewijzing module Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="9d347-138">Locate hello following lines in hello configuration for hello mapping module:</span></span>

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

<span data-ttu-id="9d347-139">Vervang Hallo **deviceID** en **deviceKey** tijdelijke aanduidingen door Hallo-id's en sleutels voor Hallo twee apparaten die u eerder in het Hallo-oplossing voor externe controle hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9d347-139">Replace hello **deviceID** and **deviceKey** placeholders with hello IDs and keys for hello two devices you created in hello remote monitoring solution previously.</span></span>

<span data-ttu-id="9d347-140">Sla uw wijzigingen op.</span><span class="sxs-lookup"><span data-stu-id="9d347-140">Save your changes.</span></span>

<span data-ttu-id="9d347-141">U kunt nu Hallo gateway aan de rand van de IoT Hallo volgen met de opdrachten uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="9d347-141">You can now run hello IoT Edge gateway using hello following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
/usr/share/azureiotgatewaysdk/samples/simulated_device_cloud_upload/simulated_device_cloud_upload remote_monitoring.json
```

<span data-ttu-id="9d347-142">Hallo-gateway op Hallo Intel NUC gestart en verzendt gesimuleerde telemetrie toohello oplossing voor externe controle:</span><span class="sxs-lookup"><span data-stu-id="9d347-142">hello gateway starts on hello Intel NUC and sends simulated telemetry toohello remote monitoring solution:</span></span>

![Gateway aan de rand van de IoT gesimuleerde telemetrie genereert][img-simulated telemetry]

<span data-ttu-id="9d347-144">Druk op **Ctrl-C** tooexit Hallo programma op elk gewenst moment.</span><span class="sxs-lookup"><span data-stu-id="9d347-144">Press **Ctrl-C** tooexit hello program at any time.</span></span>

## <a name="view-hello-telemetry"></a><span data-ttu-id="9d347-145">Hallo telemetrie van paginaweergaven</span><span class="sxs-lookup"><span data-stu-id="9d347-145">View hello telemetry</span></span>

<span data-ttu-id="9d347-146">Hallo rand IoT gateway verzendt nu gesimuleerde telemetrie toohello oplossing voor externe controle.</span><span class="sxs-lookup"><span data-stu-id="9d347-146">hello IoT Edge gateway is now sending simulated telemetry toohello remote monitoring solution.</span></span> <span data-ttu-id="9d347-147">U kunt Hallo telemetrie weergeven op Hallo oplossing dashboard.</span><span class="sxs-lookup"><span data-stu-id="9d347-147">You can view hello telemetry on hello solution dashboard.</span></span>

- <span data-ttu-id="9d347-148">Navigeer toohello oplossing dashboard.</span><span class="sxs-lookup"><span data-stu-id="9d347-148">Navigate toohello solution dashboard.</span></span>
- <span data-ttu-id="9d347-149">Selecteer een van Hallo twee apparaten die u hebt geconfigureerd in de gateway in Hallo Hallo **apparaat tooView** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="9d347-149">Select one of hello two devices you configured in hello gateway in hello **Device tooView** dropdown.</span></span>
- <span data-ttu-id="9d347-150">Hallo telemetrie van Hallo gatewayapparaten wordt weergegeven op Hallo-dashboard.</span><span class="sxs-lookup"><span data-stu-id="9d347-150">hello telemetry from hello gateway devices displays on hello dashboard.</span></span>

![Telemetrie weergegeven van Hallo gesimuleerde gateway-apparaten][img-telemetry-display]

> [!WARNING]
> <span data-ttu-id="9d347-152">Als u Hallo oplossing uitgevoerd in uw Azure-account voor externe controle laat, wordt u gefactureerd voor Hallo keer die wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9d347-152">If you leave hello remote monitoring solution running in your Azure account, you are billed for hello time it runs.</span></span> <span data-ttu-id="9d347-153">Zie voor meer informatie over het verminderen van verbruik tijdens het Hallo voor externe controle van de oplossing wordt uitgevoerd, [configureren van Azure IoT Suite vooraf geconfigureerde oplossingen voor demonstratiedoeleinden][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="9d347-153">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="9d347-154">Hallo vooraf geconfigureerde oplossing uit uw Azure-account verwijderen wanneer u klaar bent met het gebruik van maken.</span><span class="sxs-lookup"><span data-stu-id="9d347-154">Delete hello preconfigured solution from your Azure account when you have finished using it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d347-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9d347-155">Next steps</span></span>

<span data-ttu-id="9d347-156">Ga naar Hallo [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) voor meer voorbeelden en documentatie over Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="9d347-156">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-simulated telemetry]: ./media/iot-suite-gateway-kit-get-started-simulator/appoutput.png

[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-simulator/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md

[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started