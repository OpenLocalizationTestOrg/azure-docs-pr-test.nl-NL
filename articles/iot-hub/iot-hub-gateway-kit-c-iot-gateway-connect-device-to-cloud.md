---
title: aaaUse een IoT gateway tooconnect een apparaat tooAzure IoT Hub | Microsoft Docs
description: Meer informatie over hoe toouse Intel NUC als een IoT gateway tooconnect een SensorTag TI en verzenden sensor gegevens tooAzure IoT-Hub in Hallo cloud.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: IOT gateway verbinding toocloud apparaat maken
ms.assetid: cb851648-018c-4a7e-860f-b62ed3b493a5
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/25/2017
ms.author: xshi
ms.openlocfilehash: 418af34bf29992d46b76ae59ef548744808664c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-iot-gateway-tooconnect-things-toohello-cloud---sensortag-tooazure-iot-hub"></a><span data-ttu-id="3bc05-104">Gebruik IoT gateway tooconnect dingen toohello cloud - SensorTag tooAzure IoT-Hub</span><span class="sxs-lookup"><span data-stu-id="3bc05-104">Use IoT gateway tooconnect things toohello cloud - SensorTag tooAzure IoT Hub</span></span>

> [!NOTE]
> <span data-ttu-id="3bc05-105">Voordat u deze zelfstudie begint, controleert u of u hebt voltooid [Intel NUC als een IoT-gateway instellen](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md).</span><span class="sxs-lookup"><span data-stu-id="3bc05-105">Before you start this tutorial, make sure you’ve completed [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md).</span></span> <span data-ttu-id="3bc05-106">In [Intel NUC als een IoT-gateway instellen](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md), instellen van Hallo Intel NUC apparaat als een IoT-gateway.</span><span class="sxs-lookup"><span data-stu-id="3bc05-106">In [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md), you set up hello Intel NUC device as an IoT gateway.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="3bc05-107">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="3bc05-107">What you will learn</span></span>

<span data-ttu-id="3bc05-108">U leert hoe toouse een IoT gateway tooconnect een Texas instrumenten SensorTag (CC2650STK) tooAzure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="3bc05-108">You learn how toouse an IoT gateway tooconnect a Texas Instruments SensorTag (CC2650STK) tooAzure IoT Hub.</span></span> <span data-ttu-id="3bc05-109">Hallo IoT gateway verzendt temperatuur en vochtigheid gegevens die worden verzameld van Hallo SensorTag tooAzure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="3bc05-109">hello IoT gateway sends temperature and humidity data collected from hello SensorTag tooAzure IoT Hub.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="3bc05-110">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="3bc05-110">What you will do</span></span>

- <span data-ttu-id="3bc05-111">Een iothub maken.</span><span class="sxs-lookup"><span data-stu-id="3bc05-111">Create an IoT hub.</span></span>
- <span data-ttu-id="3bc05-112">Een apparaat in Hallo iothub voor Hallo SensorTag registreren.</span><span class="sxs-lookup"><span data-stu-id="3bc05-112">Register a device in hello IoT hub for hello SensorTag.</span></span>
- <span data-ttu-id="3bc05-113">Hallo-verbinding tussen Hallo IoT gateway en Hallo SensorTag inschakelen.</span><span class="sxs-lookup"><span data-stu-id="3bc05-113">Enable hello connection between hello IoT gateway and hello SensorTag.</span></span>
- <span data-ttu-id="3bc05-114">Voer een Aanmeldingsprompt voorbeeld toepassing toosend SensorTag tooyour iothub.</span><span class="sxs-lookup"><span data-stu-id="3bc05-114">Run a BLE sample application toosend SensorTag data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="3bc05-115">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="3bc05-115">What you need</span></span>

- <span data-ttu-id="3bc05-116">Zelfstudie [Intel NUC als een IoT-gateway instellen](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) voltooid in die u Intel NUC als een IoT-gateway instelt.</span><span class="sxs-lookup"><span data-stu-id="3bc05-116">Tutorial [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) completed in which you set up Intel NUC as an IoT gateway.</span></span>
- * <span data-ttu-id="3bc05-117">Een actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="3bc05-117">An active Azure subscription.</span></span> <span data-ttu-id="3bc05-118">Als u een Azure-account geen [maken van een gratis Azure-proefaccount](https://azure.microsoft.com/free/) over een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="3bc05-118">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
- <span data-ttu-id="3bc05-119">Een SSH-client die wordt uitgevoerd op de hostcomputer.</span><span class="sxs-lookup"><span data-stu-id="3bc05-119">An SSH client that runs on your host computer.</span></span> <span data-ttu-id="3bc05-120">PuTTY wordt aanbevolen voor Windows.</span><span class="sxs-lookup"><span data-stu-id="3bc05-120">PuTTY is recommended on Windows.</span></span> <span data-ttu-id="3bc05-121">Linux- en Mac OS al worden geleverd met een SSH-client.</span><span class="sxs-lookup"><span data-stu-id="3bc05-121">Linux and macOS already come with an SSH client.</span></span>
- <span data-ttu-id="3bc05-122">Hallo IP-adres en Hallo gebruikersnaam en wachtwoord tooaccess Hallo gateway vanuit Hallo SSH-client.</span><span class="sxs-lookup"><span data-stu-id="3bc05-122">hello IP address and hello username and password tooaccess hello gateway from hello SSH client.</span></span>
- <span data-ttu-id="3bc05-123">Een internetverbinding.</span><span class="sxs-lookup"><span data-stu-id="3bc05-123">An Internet connection.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

> [!NOTE]
> <span data-ttu-id="3bc05-124">Hier registreren u dit nieuwe apparaat voor uw SensorTag</span><span class="sxs-lookup"><span data-stu-id="3bc05-124">Here you register this new device for your SensorTag</span></span>

## <a name="enable-hello-connection-between-hello-iot-gateway-and-hello-sensortag"></a><span data-ttu-id="3bc05-125">Hallo-verbinding tussen Hallo IoT gateway en Hallo SensorTag inschakelen</span><span class="sxs-lookup"><span data-stu-id="3bc05-125">Enable hello connection between hello IoT gateway and hello SensorTag</span></span>

<span data-ttu-id="3bc05-126">In deze sectie kunt u Hallo volgende taken uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="3bc05-126">In this section, you perform hello following tasks:</span></span>

- <span data-ttu-id="3bc05-127">Hallo MAC-adres van Hallo SensorTag voor Bluetooth-verbinding niet ophalen.</span><span class="sxs-lookup"><span data-stu-id="3bc05-127">Get hello MAC address of hello SensorTag for Bluetooth connection.</span></span>
- <span data-ttu-id="3bc05-128">Een Bluetooth-verbinding van Hallo IoT gateway toohello SensorTag starten.</span><span class="sxs-lookup"><span data-stu-id="3bc05-128">Initiate a Bluetooth connection from hello IoT gateway toohello SensorTag.</span></span>

### <a name="get-hello-mac-address-of-hello-sensortag-for-bluetooth-connection"></a><span data-ttu-id="3bc05-129">Hallo MAC-adres van Hallo SensorTag voor Bluetooth-verbinding ophalen</span><span class="sxs-lookup"><span data-stu-id="3bc05-129">Get hello MAC address of hello SensorTag for Bluetooth connection</span></span>

1. <span data-ttu-id="3bc05-130">Op de hostcomputer Hallo Hallo SSH-client wordt uitgevoerd en verbinding maken met toohello IoT gateway.</span><span class="sxs-lookup"><span data-stu-id="3bc05-130">On hello host computer, run hello SSH client and connect toohello IoT gateway.</span></span>
1. <span data-ttu-id="3bc05-131">De blokkering opheffen Bluetooth Hallo na de opdracht uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="3bc05-131">Unblock Bluetooth by running hello following command:</span></span>

   ```bash
   sudo rfkill unblock bluetooth
   ```

1. <span data-ttu-id="3bc05-132">Hallo Bluetooth-service starten op Hallo IoT gateway en voert u een Bluetooth-shell tooconfigure Bluetooth door te voeren Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="3bc05-132">Start hello Bluetooth service on hello IoT gateway and enter a Bluetooth shell tooconfigure Bluetooth by running hello following commands:</span></span>

   ```bash
   sudo systemctl start bluetooth
   bluetoothctl
   ```

1. <span data-ttu-id="3bc05-133">Power op Hallo Bluetooth domeincontroller door te voeren Hallo Hallo Bluetooth-shell-opdracht te volgen:</span><span class="sxs-lookup"><span data-stu-id="3bc05-133">Power on hello Bluetooth controller by running hello following command at hello Bluetooth shell:</span></span>

   ```bash
   power on
   ```

   ![Hallo Bluetooth-controller hebben op Hallo IoT gateway met bluetoothctl inschakelen](./media/iot-hub-iot-gateway-connect-device-to-cloud/8_power-on-bluetooth-controller-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="3bc05-135">Start scannen op in de buurt Bluetooth-apparaten door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="3bc05-135">Start scanning for nearby Bluetooth devices by running hello following command:</span></span>

   ```bash
   scan on
   ```

   ![In de buurt Bluetooth-apparaten met bluetoothctl scannen](./media/iot-hub-iot-gateway-connect-device-to-cloud/9_start-scan-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="3bc05-137">Druk op Hallo knop op Hallo SensorTag koppelen.</span><span class="sxs-lookup"><span data-stu-id="3bc05-137">Press hello pairing button on hello SensorTag.</span></span> <span data-ttu-id="3bc05-138">Hallo groen geleid op Hallo SensorTag flitsen.</span><span class="sxs-lookup"><span data-stu-id="3bc05-138">hello green LED on hello SensorTag flashes.</span></span>
1. <span data-ttu-id="3bc05-139">U ziet op Hallo Bluetooth-shell, Hallo die sensortag is gevonden.</span><span class="sxs-lookup"><span data-stu-id="3bc05-139">At hello Bluetooth shell, you should see hello SensorTag is found.</span></span> <span data-ttu-id="3bc05-140">Noteer Hallo MAC-adres van Hallo SensorTag.</span><span class="sxs-lookup"><span data-stu-id="3bc05-140">Make a note of hello MAC address of hello SensorTag.</span></span> <span data-ttu-id="3bc05-141">In dit voorbeeld Hallo MAC-adres van Hallo SensorTag is `24:71:89:C0:7F:82`.</span><span class="sxs-lookup"><span data-stu-id="3bc05-141">In this example, hello MAC address of hello SensorTag is `24:71:89:C0:7F:82`.</span></span>
1. <span data-ttu-id="3bc05-142">Hallo scan uitschakelen door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="3bc05-142">Turn off hello scan by running hello following command:</span></span>

   ```bash
   scan off
   ```

   ![In de buurt Bluetooth-apparaten met bluetoothctl scannen stopzetten](./media/iot-hub-iot-gateway-connect-device-to-cloud/10_stop-scanning-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

### <a name="initiate-a-bluetooth-connection-from-hello-iot-gateway-toohello-sensortag"></a><span data-ttu-id="3bc05-144">Een Bluetooth-verbinding van Hallo IoT gateway toohello SensorTag starten</span><span class="sxs-lookup"><span data-stu-id="3bc05-144">Initiate a Bluetooth connection from hello IoT gateway toohello SensorTag</span></span>

1. <span data-ttu-id="3bc05-145">Verbinding maken met toohello SensorTag door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="3bc05-145">Connect toohello SensorTag by running hello following command:</span></span>

   ```bash
   connect <MAC address>
   ```

   ![Verbinding maken met toohello SensorTag met bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/11_connect-to-sensortag-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="3bc05-147">Hallo SensorTag verbreken en Hallo Bluetooth-shell afsluiten door te voeren Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="3bc05-147">Disconnect from hello SensorTag and exit hello Bluetooth shell by running hello following commands:</span></span>

   ```bash
   disconnect
   exit
   ```

   ![Hallo SensorTag met bluetoothctl verbreken](./media/iot-hub-iot-gateway-connect-device-to-cloud/12_disconnect-from-sensortag-at-bluetooth-shell-bluetoothctl.png)

<span data-ttu-id="3bc05-149">Hallo-verbinding tussen Hallo SensorTag en Hallo IoT gateway hebt ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="3bc05-149">You've successfully enabled hello connection between hello SensorTag and hello IoT gateway.</span></span>

## <a name="run-a-ble-sample-application-toosend-sensortag-data-tooyour-iot-hub"></a><span data-ttu-id="3bc05-150">Voer een Aanmeldingsprompt voorbeeld toepassing toosend SensorTag tooyour iothub</span><span class="sxs-lookup"><span data-stu-id="3bc05-150">Run a BLE sample application toosend SensorTag data tooyour IoT hub</span></span>

<span data-ttu-id="3bc05-151">Hallo Bluetooth laag energieverbruik (uitschakelen) voorbeeldtoepassing wordt verstrekt door Azure IoT rand.</span><span class="sxs-lookup"><span data-stu-id="3bc05-151">hello Bluetooth Low Energy (BLE) sample application is provided by Azure IoT Edge.</span></span> <span data-ttu-id="3bc05-152">Hallo-voorbeeldtoepassing verzamelt gegevens van verbinding uitschakelen en Hallo gegevens tooyou IoT-hub te verzenden.</span><span class="sxs-lookup"><span data-stu-id="3bc05-152">hello sample application collects data from BLE connection and send hello data tooyou IoT hub.</span></span> <span data-ttu-id="3bc05-153">voorbeeldtoepassing toorun hello, moet u:</span><span class="sxs-lookup"><span data-stu-id="3bc05-153">toorun hello sample application, you need to:</span></span>

1. <span data-ttu-id="3bc05-154">Hallo-voorbeeldtoepassing configureren.</span><span class="sxs-lookup"><span data-stu-id="3bc05-154">Configure hello sample application.</span></span>
1. <span data-ttu-id="3bc05-155">Hallo-voorbeeldtoepassing uitvoeren op Hallo IoT gateway.</span><span class="sxs-lookup"><span data-stu-id="3bc05-155">Run hello sample application on hello IoT gateway.</span></span>

### <a name="configure-hello-sample-application"></a><span data-ttu-id="3bc05-156">Hallo-voorbeeldtoepassing configureren</span><span class="sxs-lookup"><span data-stu-id="3bc05-156">Configure hello sample application</span></span>

1. <span data-ttu-id="3bc05-157">Map van de voorbeeldtoepassing Hallo toohello gaan door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="3bc05-157">Go toohello folder of hello sample application by running hello following command:</span></span>

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples/ble_gateway
   ```

1. <span data-ttu-id="3bc05-158">Hallo-configuratiebestand openen door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="3bc05-158">Open hello configuration file by running hello following command:</span></span>

   ```bash
   vi ble_gateway.json
   ```

1. <span data-ttu-id="3bc05-159">Vul in het configuratiebestand hello, Hallo volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="3bc05-159">In hello configuration file, fill in hello following values:</span></span>

   <span data-ttu-id="3bc05-160">**IoTHubName**: Hallo-naam van uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="3bc05-160">**IoTHubName**: hello name of your IoT hub.</span></span>

   <span data-ttu-id="3bc05-161">**IoTHubSuffix**: IoTHubSuffix ophalen uit de Hallo primaire sleutel van Hallo apparaat verbindingsreeks die u hebt genoteerd omlaag.</span><span class="sxs-lookup"><span data-stu-id="3bc05-161">**IoTHubSuffix**: Get IoTHubSuffix from hello primary key of hello device connection string that you noted down.</span></span> <span data-ttu-id="3bc05-162">Zorg dat u primaire sleutel voor Hallo van Hallo apparaat verbindingsreeks ophalen, Hallo geen primaire sleutel van de verbindingsreeks van uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="3bc05-162">Ensure that you get hello primary key of hello device connection string, not hello primary key of your IoT hub connection string.</span></span> <span data-ttu-id="3bc05-163">Hallo primaire sleutel van de verbindingsreeks Hallo-apparaat is Hallo notatie `HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY`.</span><span class="sxs-lookup"><span data-stu-id="3bc05-163">hello primary key of hello device connection string is in hello format of `HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY`.</span></span>

   <span data-ttu-id="3bc05-164">**Transport**: Hallo standaardwaarde is `amqp`.</span><span class="sxs-lookup"><span data-stu-id="3bc05-164">**Transport**: hello default value is `amqp`.</span></span> <span data-ttu-id="3bc05-165">Deze waarde weergegeven Hallo protocol tijdens transpotation.</span><span class="sxs-lookup"><span data-stu-id="3bc05-165">This value shows hello protocol during transpotation.</span></span> <span data-ttu-id="3bc05-166">Kan de zijn `http`, `amqp`, of `mqtt`.</span><span class="sxs-lookup"><span data-stu-id="3bc05-166">It could be `http`, `amqp`, or `mqtt`.</span></span>

   <span data-ttu-id="3bc05-167">**macAddress**: Hallo MAC-adres van Hallo SensorTag die u hebt genoteerd omlaag.</span><span class="sxs-lookup"><span data-stu-id="3bc05-167">**macAddress**: hello MAC address of hello SensorTag that you noted down.</span></span>

   <span data-ttu-id="3bc05-168">**deviceID**: ID van Hallo-apparaat dat u hebt gemaakt in uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="3bc05-168">**deviceID**: ID of hello device that you created in your IoT hub.</span></span>

   <span data-ttu-id="3bc05-169">**deviceKey**: Hallo primaire sleutel van de verbindingsreeks Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="3bc05-169">**deviceKey**: hello primary key of hello device connection string.</span></span>

   ![Het configuratiebestand voltooid Hallo Hallo voorbeeldtoepassing uitschakelen](./media/iot-hub-iot-gateway-connect-device-to-cloud/13_edit-config-file-of-ble-sample.png)

1. <span data-ttu-id="3bc05-171">Druk op `ESC` en het type `:wq` toosave Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="3bc05-171">Press `ESC` and type `:wq` toosave hello file.</span></span>

### <a name="run-hello-sample-application"></a><span data-ttu-id="3bc05-172">Hallo-voorbeeldtoepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="3bc05-172">Run hello sample application</span></span>

1. <span data-ttu-id="3bc05-173">Zorg ervoor dat Hallo die sensortag is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="3bc05-173">Make sure hello SensorTag is powered on.</span></span>
1. <span data-ttu-id="3bc05-174">Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="3bc05-174">Run hello following command:</span></span>

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a><span data-ttu-id="3bc05-175">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3bc05-175">Next steps</span></span>

[<span data-ttu-id="3bc05-176">Gebruik IoT gateway voor gegevenstransformatie sensor met Azure IoT rand</span><span class="sxs-lookup"><span data-stu-id="3bc05-176">Use IoT gateway for sensor data transformation with Azure IoT Edge</span></span>](iot-hub-gateway-kit-c-use-iot-gateway-for-data-conversion.md)
