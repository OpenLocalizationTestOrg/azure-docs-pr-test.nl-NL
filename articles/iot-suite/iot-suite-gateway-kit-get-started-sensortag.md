---
title: een gateway tooAzure IoT-Suite met een Intel NUC aaaConnect | Microsoft Docs
description: "Gebruik Hallo Microsoft IoT commerciële Gateway Kit en Hallo vooraf geconfigureerde oplossing voor externe controle. Hallo rand van Azure IoT gateway tooenable gebruiken een oplossing voor externe controle van SensorTag apparaat tooconnect toohello, verzenden van telemetrie toohello cloud en toomethods aangeroepen vanuit het dashboard van de oplossing Hallo reageren."
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
ms.openlocfilehash: 6f98ee3c1e2311a8644da9d72d40e671e7cbcf00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-azure-iot-edge-gateway-toohello-remote-monitoring-preconfigured-solution-and-send-telemetry-from-a-sensortag"></a><span data-ttu-id="6e173-104">Verbinding maken met uw vooraf geconfigureerde oplossing voor externe controle rand van Azure IoT gateway toohello en verzend telemetrie vanuit een SensorTag</span><span class="sxs-lookup"><span data-stu-id="6e173-104">Connect your Azure IoT Edge gateway toohello remote monitoring preconfigured solution and send telemetry from a SensorTag</span></span>

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

<span data-ttu-id="6e173-105">Deze zelfstudie laat zien hoe Azure IoT rand toosend temperatuur en vochtigheid gegevens uit SensorTag apparaat toohello externe controle toouse vooraf geconfigureerde oplossing.</span><span class="sxs-lookup"><span data-stu-id="6e173-105">This tutorial shows you how toouse Azure IoT Edge toosend temperature and humidity data from SensorTag device toohello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="6e173-106">Hallo SensorTag verbindt toohello Intel NUC gateway via Bluetooth.</span><span class="sxs-lookup"><span data-stu-id="6e173-106">hello SensorTag connects toohello Intel NUC gateway using Bluetooth.</span></span> <span data-ttu-id="6e173-107">Hallo-zelfstudie wordt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="6e173-107">hello tutorial uses:</span></span>

- <span data-ttu-id="6e173-108">Azure IoT rand tooimplement een voorbeeld-gateway.</span><span class="sxs-lookup"><span data-stu-id="6e173-108">Azure IoT Edge tooimplement a sample gateway.</span></span>
- <span data-ttu-id="6e173-109">Hallo IoT Suite remote monitoring vooraf geconfigureerde oplossing als Hallo cloud-gebaseerde back-end.</span><span class="sxs-lookup"><span data-stu-id="6e173-109">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="6e173-110">Overzicht</span><span class="sxs-lookup"><span data-stu-id="6e173-110">Overview</span></span>

<span data-ttu-id="6e173-111">In deze zelfstudie maakt uitvoeren u Hallo stappen:</span><span class="sxs-lookup"><span data-stu-id="6e173-111">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="6e173-112">Implementeer een exemplaar van Hallo externe controle vooraf geconfigureerde oplossing tooyour Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="6e173-112">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="6e173-113">Deze stap implementeert automatisch en meerdere Azure-services configureert.</span><span class="sxs-lookup"><span data-stu-id="6e173-113">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="6e173-114">Stel uw toocommunicate Intel NUC gateway-apparaat met de computer en het Hallo-oplossing voor externe controle.</span><span class="sxs-lookup"><span data-stu-id="6e173-114">Set up your Intel NUC gateway device toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="6e173-115">Instellen van uw Intel NUC gateway tooreceive telemetrie vanaf een apparaat SensorTag en verzend het toohello voor externe controle dashboard.</span><span class="sxs-lookup"><span data-stu-id="6e173-115">Set up your Intel NUC gateway tooreceive telemetry from a SensorTag device and send it toohello remote monitoring dashboard.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

<span data-ttu-id="6e173-116">[Texas instrumenten uitschakelen SensorTag][lnk-sensortag].</span><span class="sxs-lookup"><span data-stu-id="6e173-116">[Texas Instruments BLE SensorTag][lnk-sensortag].</span></span> <span data-ttu-id="6e173-117">Deze zelfstudie haalt telemetrische gegevens via Bluetooth van Hallo SensorTag-apparaten.</span><span class="sxs-lookup"><span data-stu-id="6e173-117">This tutorial retrieves telemetry data over Bluetooth from hello SensorTag device.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="6e173-118">Hallo externe controle van de bepalingen van de oplossing voor een verzameling Azure-services in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="6e173-118">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="6e173-119">Hallo implementatie duidt op een echte enterprise-architectuur.</span><span class="sxs-lookup"><span data-stu-id="6e173-119">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="6e173-120">tooavoid onnodige Azure-verbruik kosten, verwijderen van uw exemplaar van Hallo vooraf geconfigureerde oplossing op azureiotsuite.com wanneer u klaar bent met het.</span><span class="sxs-lookup"><span data-stu-id="6e173-120">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="6e173-121">Als u moet de vooraf geconfigureerde oplossing opnieuw hello, u kunt gemakkelijk het opnieuw maken.</span><span class="sxs-lookup"><span data-stu-id="6e173-121">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="6e173-122">Zie voor meer informatie over het verminderen van verbruik tijdens het Hallo voor externe controle van de oplossing wordt uitgevoerd, [configureren van Azure IoT Suite vooraf geconfigureerde oplossingen voor demonstratiedoeleinden][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="6e173-122">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

## <a name="configure-bluetooth-connectivity"></a><span data-ttu-id="6e173-123">Bluetooth-connectiviteit configureren</span><span class="sxs-lookup"><span data-stu-id="6e173-123">Configure Bluetooth connectivity</span></span>

<span data-ttu-id="6e173-124">Configureren van Bluetooth op Hallo Intel NUC tooenable hello SensorTag apparaat tooconnect en verzenden van telemetrie.</span><span class="sxs-lookup"><span data-stu-id="6e173-124">Configure Bluetooth on hello Intel NUC tooenable hello SensorTag device tooconnect and send telemetry.</span></span>

### <a name="find-hello-mac-address-of-hello-sensortag"></a><span data-ttu-id="6e173-125">MAC-adres Hallo Hallo SensorTag zoeken</span><span class="sxs-lookup"><span data-stu-id="6e173-125">Find hello MAC address of hello SensorTag</span></span>

1. <span data-ttu-id="6e173-126">Hallo-shell op Hallo Intel NUC, start Hallo opdracht toounblock Hallo Bluetooth-service te volgen:</span><span class="sxs-lookup"><span data-stu-id="6e173-126">In hello shell on hello Intel NUC, run hello following command toounblock hello Bluetooth service:</span></span>

    ```bash
    sudo rfkill unblock bluetooth
    ```

1. <span data-ttu-id="6e173-127">Voer Hallo volgende toostart Hallo Bluetooth-service op Hallo Intel NUC opdrachten en Voer Hallo Bluetooth-shell:</span><span class="sxs-lookup"><span data-stu-id="6e173-127">Run hello following commands toostart hello Bluetooth service on hello Intel NUC and enter hello Bluetooth shell:</span></span>

    ```bash
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. <span data-ttu-id="6e173-128">Voer Hallo opdracht toopower op Hallo Bluetooth-domeincontroller te volgen:</span><span class="sxs-lookup"><span data-stu-id="6e173-128">Run hello following command toopower on hello Bluetooth controller:</span></span>

    ```bash
    power on
    ```

    <span data-ttu-id="6e173-129">Als het Hallo-controller is ingeschakeld, ziet u een bericht **power wijzigen op geslaagd**.</span><span class="sxs-lookup"><span data-stu-id="6e173-129">When hello controller is on, you see a message **Changing power on succeeded**.</span></span>

1. <span data-ttu-id="6e173-130">Voer Hallo opdracht tooscan voor Bluetooth-apparaten in de buurt te volgen:</span><span class="sxs-lookup"><span data-stu-id="6e173-130">Run hello following command tooscan for nearby Bluetooth devices:</span></span>

    ```bash
    scan on
    ```

1. <span data-ttu-id="6e173-131">Druk op Hallo power knop op Hallo SensorTag toomake deze kunnen worden gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="6e173-131">Press hello power button on hello SensorTag toomake it discoverable.</span></span> <span data-ttu-id="6e173-132">Hallo groen LED knippert.</span><span class="sxs-lookup"><span data-stu-id="6e173-132">hello green LED flashes.</span></span>

1. <span data-ttu-id="6e173-133">Wanneer er een bericht verschijnt in de shell Hallo Hallo controller Hallo SensorTag heeft gedetecteerd, noteer Hallo MAC-adres van het Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="6e173-133">When you see a message in hello shell that hello controller has discovered hello SensorTag, make a note of hello MAC address of hello device.</span></span> <span data-ttu-id="6e173-134">Hallo MAC-adres ziet eruit als **A0:E6:F8:B5:F6:00**.</span><span class="sxs-lookup"><span data-stu-id="6e173-134">hello MAC address looks like **A0:E6:F8:B5:F6:00**.</span></span> <span data-ttu-id="6e173-135">U moet Hallo MAC-adres verderop in de zelfstudie Hallo wanneer u Hallo gateway configureert.</span><span class="sxs-lookup"><span data-stu-id="6e173-135">You need hello MAC address later in hello tutorial when you configure hello gateway.</span></span>

1. <span data-ttu-id="6e173-136">Voer Hallo opdracht tooturn Bluetooth scannen uit te volgen:</span><span class="sxs-lookup"><span data-stu-id="6e173-136">Run hello following command tooturn off Bluetooth scanning:</span></span>

    ```bash
    scan off
    ```

1. <span data-ttu-id="6e173-137">Hallo na de opdracht tooverify of toohello SensorTag apparaat verbinding kan worden uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="6e173-137">Run hello following command tooverify that you can connect toohello SensorTag device:</span></span>

    ```bash
    connect <SensorTag MAC address>
    ```

    <span data-ttu-id="6e173-138">Als u verbinding met succes maakt, Hallo shell ziet u het Hallo-bericht **verbinding tot stand gebracht** en informatie over Hallo SensorTag-apparaat wordt afgedrukt.</span><span class="sxs-lookup"><span data-stu-id="6e173-138">If you connect successfully, hello shell shows hello message **Connection successful** and prints information about hello SensorTag device.</span></span> <span data-ttu-id="6e173-139">Als u geen verbinding maken, controleert u Hallo die sensortag nog steeds is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="6e173-139">If you cannot connect, check hello SensorTag is still powered on.</span></span>

1. <span data-ttu-id="6e173-140">U kunt nu Hallo SensorTag verbreken en Hallo Bluetooth-shell afsluiten door te voeren Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="6e173-140">You can now disconnect from hello SensorTag and exit hello Bluetooth shell by running hello following commands:</span></span>

    ```bash
    disconnect
    exit
    ```

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-software](../../includes/iot-suite-gateway-kit-prepare-nuc-software.md)]

## <a name="build-hello-custom-iot-edge-module"></a><span data-ttu-id="6e173-141">Hallo aangepaste IoT Edge-module maken</span><span class="sxs-lookup"><span data-stu-id="6e173-141">Build hello custom IoT Edge module</span></span>

<span data-ttu-id="6e173-142">U kunt nu Hallo aangepaste IoT Edge-module maken waarmee Hallo gateway toosend berichten toohello oplossing voor externe controle.</span><span class="sxs-lookup"><span data-stu-id="6e173-142">You can now build hello custom IoT Edge module that enables hello gateway toosend messages toohello remote monitoring solution.</span></span> <span data-ttu-id="6e173-143">Zie voor meer informatie over het configureren van een gateway en de rand van de IoT-modules [Azure IoT rand concepten][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="6e173-143">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

<span data-ttu-id="6e173-144">Download de broncode Hallo voor aangepaste modules die IoT rand Hallo vanuit GitHub Hallo volgende opdrachten gebruiken:</span><span class="sxs-lookup"><span data-stu-id="6e173-144">Download hello source code for hello custom IoT Edge modules from GitHub using hello following commands:</span></span>

```bash
cd ~
git clone https://github.com/Azure-Samples/iot-remote-monitoring-c-intel-nuc-gateway-getting-started.git
```

<span data-ttu-id="6e173-145">Hallo aangepaste IoT Edge-module met behulp van de volgende opdrachten Hallo maken:</span><span class="sxs-lookup"><span data-stu-id="6e173-145">Build hello custom IoT Edge module using hello following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

<span data-ttu-id="6e173-146">Hallo build script Hallo libsensor2remotemonitoring.so aangepaste IoT rand module in Hallo build-map geplaatst.</span><span class="sxs-lookup"><span data-stu-id="6e173-146">hello build script places hello libsensor2remotemonitoring.so custom IoT Edge module in hello build folder.</span></span>

## <a name="configure-and-run-hello-iot-edge-gateway"></a><span data-ttu-id="6e173-147">Configureren en uitvoeren van Hallo rand IoT gateway</span><span class="sxs-lookup"><span data-stu-id="6e173-147">Configure and run hello IoT Edge gateway</span></span>

<span data-ttu-id="6e173-148">U kunt nu Hallo rand IoT gateway toosend telemetrie van uw externe controle dashboard SensorTag apparaat tooyour configureren.</span><span class="sxs-lookup"><span data-stu-id="6e173-148">You can now configure hello IoT Edge gateway toosend telemetry from your SensorTag device tooyour remote monitoring dashboard.</span></span> <span data-ttu-id="6e173-149">Zie voor meer informatie over het configureren van een gateway en de rand van de IoT-modules [Azure IoT rand concepten][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="6e173-149">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

> [!TIP]
> <span data-ttu-id="6e173-150">In deze zelfstudie gebruikt u Hallo standaard `vi` teksteditor op Hallo Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="6e173-150">In this tutorial, you use hello standard `vi` text editor on hello Intel NUC.</span></span> <span data-ttu-id="6e173-151">Als u niet hebt gebruikt `vi` , moet u een inleidende zelfstudie, zoals uitvoeren [Unix - Hallo vi zelfstudie Editor] [ lnk-vi-tutorial] toofamiliarize uzelf met deze editor.</span><span class="sxs-lookup"><span data-stu-id="6e173-151">If you have not used `vi` before, you should complete an introductory tutorial, such as [Unix - hello vi Editor Tutorial][lnk-vi-tutorial] toofamiliarize yourself with this editor.</span></span> <span data-ttu-id="6e173-152">U kunt ook installeren Hallo gebruikersvriendelijker [nano](https://www.nano-editor.org/) editor met Hallo opdracht `smart install nano -y`.</span><span class="sxs-lookup"><span data-stu-id="6e173-152">Alternatively, you can install hello more user-friendly [nano](https://www.nano-editor.org/) editor using hello command `smart install nano -y`.</span></span>

<span data-ttu-id="6e173-153">Open Hallo voorbeeldconfiguratiebestand in Hallo **vi** editor met behulp van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="6e173-153">Open hello sample configuration file in hello **vi** editor using hello following command:</span></span>

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic/remote_monitoring.json
```

<span data-ttu-id="6e173-154">Zoek de volgende regels in de configuratie voor Hallo IoTHub module Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="6e173-154">Locate hello following lines in hello configuration for hello IoTHub module:</span></span>

```json
"args": {
  "IoTHubName": "<<Azure IoT Hub Name>>",
  "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
  "Transport": "http"
}
```

<span data-ttu-id="6e173-155">Hallo-tijdelijke aanduiding voor waarden met IoT Hub informatie u gemaakt en opgeslagen op Hallo Hallo begin van deze zelfstudie wordt vervangen.</span><span class="sxs-lookup"><span data-stu-id="6e173-155">Replace hello placeholder values with hello IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="6e173-156">Hallo-waarde voor IoTHubName eruit **yourrmsolution37e08**, en het Hallo-waarde voor IoTSuffix is doorgaans **azure devices.net**.</span><span class="sxs-lookup"><span data-stu-id="6e173-156">hello value for IoTHubName looks like **yourrmsolution37e08**, and hello value for IoTSuffix is typically **azure-devices.net**.</span></span>

<span data-ttu-id="6e173-157">Zoek de volgende regels in de configuratie voor Hallo toewijzing module Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="6e173-157">Locate hello following lines in hello configuration for hello mapping module:</span></span>

```json
args": [
  {
    "macAddress": "<<AA:BB:CC:DD:EE:FF>>",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  }
]
```

<span data-ttu-id="6e173-158">Vervang Hallo **macAddress** aanduiding voor items met Hallo MAC-adres van uw SensorTag die u eerder hebt genoteerd.</span><span class="sxs-lookup"><span data-stu-id="6e173-158">Replace hello **macAddress** placeholder with hello MAC address of your SensorTag you noted previously.</span></span> <span data-ttu-id="6e173-159">Vervang Hallo **deviceID** en **deviceKey** tijdelijke aanduidingen door Hallo-id's en sleutels voor Hallo twee apparaten die u eerder in het Hallo-oplossing voor externe controle hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6e173-159">Replace hello **deviceID** and **deviceKey** placeholders with hello IDs and keys for hello two devices you created in hello remote monitoring solution previously.</span></span>

<span data-ttu-id="6e173-160">Zoek de volgende regels in de configuratie voor Hallo SensorTag module Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="6e173-160">Locate hello following lines in hello configuration for hello SensorTag module:</span></span>

```json
"args": {
  "controller_index": 0,
  "device_mac_address": "<<AA:BB:CC:DD:EE:FF>>",
  ...
}
```

<span data-ttu-id="6e173-161">Vervang Hallo **apparaat\_mac\_adres** aanduiding voor items met Hallo MAC-adres van uw SensorTag die u eerder hebt genoteerd.</span><span class="sxs-lookup"><span data-stu-id="6e173-161">Replace hello **device\_mac\_address** placeholder  with hello MAC address of your SensorTag you noted previously.</span></span>

<span data-ttu-id="6e173-162">Sla uw wijzigingen op.</span><span class="sxs-lookup"><span data-stu-id="6e173-162">Save your changes.</span></span>

<span data-ttu-id="6e173-163">U kunt nu uitvoeren met behulp van de volgende opdrachten Hallo Hallo-gateway:</span><span class="sxs-lookup"><span data-stu-id="6e173-163">You can now run hello gateway using hello following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
/usr/share/azureiotgatewaysdk/samples/ble_gateway/ble_gateway remote_monitoring.json
```

<span data-ttu-id="6e173-164">Hallo gateway aan de rand van IoT op Hallo Intel NUC gestart en verzendt telemetrie van Hallo SensorTag toohello oplossing voor externe controle:</span><span class="sxs-lookup"><span data-stu-id="6e173-164">hello IoT Edge gateway starts on hello Intel NUC and sends telemetry from hello SensorTag toohello remote monitoring solution:</span></span>

![Rand IoT gateway verzendt telemetrie van Hallo SensorTag][img-telemetry]

<span data-ttu-id="6e173-166">Druk op **Ctrl-C** tooexit Hallo programma op elk gewenst moment.</span><span class="sxs-lookup"><span data-stu-id="6e173-166">Press **Ctrl-C** tooexit hello program at any time.</span></span>

## <a name="view-hello-telemetry"></a><span data-ttu-id="6e173-167">Hallo telemetrie van paginaweergaven</span><span class="sxs-lookup"><span data-stu-id="6e173-167">View hello telemetry</span></span>

<span data-ttu-id="6e173-168">Hallo gateway verzendt nu telemetrie vanaf Hallo SensorTag apparaat toohello oplossing voor externe controle.</span><span class="sxs-lookup"><span data-stu-id="6e173-168">hello gateway is now sending telemetry from hello SensorTag device toohello remote monitoring solution.</span></span> <span data-ttu-id="6e173-169">U kunt Hallo telemetrie weergeven op Hallo oplossing dashboard.</span><span class="sxs-lookup"><span data-stu-id="6e173-169">You can view hello telemetry on hello solution dashboard.</span></span> <span data-ttu-id="6e173-170">U kunt ook opdrachten tooyour SensorTag-apparaten via de gateway Hallo verzenden vanuit Hallo oplossing dashboard.</span><span class="sxs-lookup"><span data-stu-id="6e173-170">You can also send commands tooyour SensorTag device through hello gateway from hello solution dashboard.</span></span>

- <span data-ttu-id="6e173-171">Navigeer toohello oplossing dashboard.</span><span class="sxs-lookup"><span data-stu-id="6e173-171">Navigate toohello solution dashboard.</span></span>
- <span data-ttu-id="6e173-172">Selecteer Hallo apparaat u hebt geconfigureerd in het Hallo-gateway met Hallo SensorTag in Hallo **apparaat tooView** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="6e173-172">Select hello device you configured in hello gateway that represents hello SensorTag in hello **Device tooView** dropdown.</span></span>
- <span data-ttu-id="6e173-173">Hallo telemetrie van Hallo SensorTag-apparaten wordt weergegeven op Hallo-dashboard.</span><span class="sxs-lookup"><span data-stu-id="6e173-173">hello telemetry from hello SensorTag device displays on hello dashboard.</span></span>

![Telemetrie weergegeven van Hallo SensorTag-apparaten][img-telemetry-display]

> [!WARNING]
> <span data-ttu-id="6e173-175">Als u Hallo oplossing uitgevoerd in uw Azure-account voor externe controle laat, wordt u gefactureerd voor Hallo keer die wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6e173-175">If you leave hello remote monitoring solution running in your Azure account, you are billed for hello time it runs.</span></span> <span data-ttu-id="6e173-176">Zie voor meer informatie over het verminderen van verbruik tijdens het Hallo voor externe controle van de oplossing wordt uitgevoerd, [configureren van Azure IoT Suite vooraf geconfigureerde oplossingen voor demonstratiedoeleinden][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="6e173-176">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="6e173-177">Hallo vooraf geconfigureerde oplossing uit uw Azure-account verwijderen wanneer u klaar bent met het gebruik van maken.</span><span class="sxs-lookup"><span data-stu-id="6e173-177">Delete hello preconfigured solution from your Azure account when you have finished using it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="6e173-178">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6e173-178">Next steps</span></span>

<span data-ttu-id="6e173-179">Ga naar Hallo [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) voor meer voorbeelden en documentatie over Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="6e173-179">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-telemetry]: ./media/iot-suite-gateway-kit-get-started-sensortag/appoutput.png


[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-sensortag/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-sensortag]: http://www.ti.com/ww/en/wireless_connectivity/sensortag/
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started