---
title: Een IoT-gateway gebruiken voor verbinding van een apparaat met Azure IoT Hub | Microsoft Docs
description: Informatie over het gebruik van Intel NUC als een IoT-gateway verbinding maken met een SensorTag TI en sensorgegevens verzenden naar Azure IoT Hub in de cloud.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: IOT gateway verbinding maken met het apparaat in de cloud
ms.assetid: cb851648-018c-4a7e-860f-b62ed3b493a5
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/25/2017
ms.author: xshi
ms.openlocfilehash: 4fb77ed0241d15338c2574fd22828507c3e40cb3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="use-iot-gateway-to-connect-things-to-the-cloud---sensortag-to-azure-iot-hub"></a><span data-ttu-id="f3fe8-104">Gebruik IoT gateway dingen verbinding met de cloud - SensorTag met Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="f3fe8-104">Use IoT gateway to connect things to the cloud - SensorTag to Azure IoT Hub</span></span>

> [!NOTE]
> <span data-ttu-id="f3fe8-105">Voordat u deze zelfstudie begint, controleert u of u hebt voltooid [Intel NUC als een IoT-gateway instellen](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md).</span><span class="sxs-lookup"><span data-stu-id="f3fe8-105">Before you start this tutorial, make sure you’ve completed [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md).</span></span> <span data-ttu-id="f3fe8-106">In [Intel NUC als een IoT-gateway instellen](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md), instellen van het apparaat Intel NUC als een IoT-gateway.</span><span class="sxs-lookup"><span data-stu-id="f3fe8-106">In [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md), you set up the Intel NUC device as an IoT gateway.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="f3fe8-107">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="f3fe8-107">What you will learn</span></span>

<span data-ttu-id="f3fe8-108">U informatie over het gebruik van een IoT-gateway verbinding maken met een Texas instrumenten SensorTag (CC2650STK) Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="f3fe8-108">You learn how to use an IoT gateway to connect a Texas Instruments SensorTag (CC2650STK) to Azure IoT Hub.</span></span> <span data-ttu-id="f3fe8-109">De IoT-gateway verzendt temperatuur en vochtigheid gegevens verzameld uit de SensorTag naar Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="f3fe8-109">The IoT gateway sends temperature and humidity data collected from the SensorTag to Azure IoT Hub.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="f3fe8-110">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="f3fe8-110">What you will do</span></span>

- <span data-ttu-id="f3fe8-111">Een iothub maken.</span><span class="sxs-lookup"><span data-stu-id="f3fe8-111">Create an IoT hub.</span></span>
- <span data-ttu-id="f3fe8-112">Een apparaat in de iothub voor de SensorTag registreren.</span><span class="sxs-lookup"><span data-stu-id="f3fe8-112">Register a device in the IoT hub for the SensorTag.</span></span>
- <span data-ttu-id="f3fe8-113">De verbinding tussen de IoT-gateway en de SensorTag inschakelen.</span><span class="sxs-lookup"><span data-stu-id="f3fe8-113">Enable the connection between the IoT gateway and the SensorTag.</span></span>
- <span data-ttu-id="f3fe8-114">Voer een voorbeeldtoepassing uitschakelen SensorTag gegevens verzenden naar uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="f3fe8-114">Run a BLE sample application to send SensorTag data to your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="f3fe8-115">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="f3fe8-115">What you need</span></span>

- <span data-ttu-id="f3fe8-116">Zelfstudie [Intel NUC als een IoT-gateway instellen](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) voltooid in die u Intel NUC als een IoT-gateway instelt.</span><span class="sxs-lookup"><span data-stu-id="f3fe8-116">Tutorial [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) completed in which you set up Intel NUC as an IoT gateway.</span></span>
- * <span data-ttu-id="f3fe8-117">Een actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="f3fe8-117">An active Azure subscription.</span></span> <span data-ttu-id="f3fe8-118">Als u een Azure-account geen [maken van een gratis Azure-proefaccount](https://azure.microsoft.com/free/) over een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="f3fe8-118">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
- <span data-ttu-id="f3fe8-119">Een SSH-client die wordt uitgevoerd op de hostcomputer.</span><span class="sxs-lookup"><span data-stu-id="f3fe8-119">An SSH client that runs on your host computer.</span></span> <span data-ttu-id="f3fe8-120">PuTTY wordt aanbevolen voor Windows.</span><span class="sxs-lookup"><span data-stu-id="f3fe8-120">PuTTY is recommended on Windows.</span></span> <span data-ttu-id="f3fe8-121">Linux- en Mac OS al worden geleverd met een SSH-client.</span><span class="sxs-lookup"><span data-stu-id="f3fe8-121">Linux and macOS already come with an SSH client.</span></span>
- <span data-ttu-id="f3fe8-122">Het IP-adres en de gebruikersnaam en wachtwoord voor toegang tot de gateway van de SSH-client.</span><span class="sxs-lookup"><span data-stu-id="f3fe8-122">The IP address and the username and password to access the gateway from the SSH client.</span></span>
- <span data-ttu-id="f3fe8-123">Een internetverbinding.</span><span class="sxs-lookup"><span data-stu-id="f3fe8-123">An Internet connection.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

> [!NOTE]
> <span data-ttu-id="f3fe8-124">Hier registreren u dit nieuwe apparaat voor uw SensorTag</span><span class="sxs-lookup"><span data-stu-id="f3fe8-124">Here you register this new device for your SensorTag</span></span>

## <a name="enable-the-connection-between-the-iot-gateway-and-the-sensortag"></a><span data-ttu-id="f3fe8-125">De verbinding tussen de IoT-gateway en de SensorTag inschakelen</span><span class="sxs-lookup"><span data-stu-id="f3fe8-125">Enable the connection between the IoT gateway and the SensorTag</span></span>

<span data-ttu-id="f3fe8-126">In deze sectie kunt u de volgende taken uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f3fe8-126">In this section, you perform the following tasks:</span></span>

- <span data-ttu-id="f3fe8-127">De MAC-adres van de SensorTag voor Bluetooth-verbinding niet ophalen.</span><span class="sxs-lookup"><span data-stu-id="f3fe8-127">Get the MAC address of the SensorTag for Bluetooth connection.</span></span>
- <span data-ttu-id="f3fe8-128">Een Bluetooth-verbinding van de IoT gateway om de SensorTag te starten.</span><span class="sxs-lookup"><span data-stu-id="f3fe8-128">Initiate a Bluetooth connection from the IoT gateway to the SensorTag.</span></span>

### <a name="get-the-mac-address-of-the-sensortag-for-bluetooth-connection"></a><span data-ttu-id="f3fe8-129">De MAC-adres van de SensorTag voor Bluetooth-verbinding ophalen</span><span class="sxs-lookup"><span data-stu-id="f3fe8-129">Get the MAC address of the SensorTag for Bluetooth connection</span></span>

1. <span data-ttu-id="f3fe8-130">De SSH-client wordt uitgevoerd op de hostcomputer en maak verbinding met de IoT-gateway.</span><span class="sxs-lookup"><span data-stu-id="f3fe8-130">On the host computer, run the SSH client and connect to the IoT gateway.</span></span>
1. <span data-ttu-id="f3fe8-131">De blokkering opheffen Bluetooth met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="f3fe8-131">Unblock Bluetooth by running the following command:</span></span>

   ```bash
   sudo rfkill unblock bluetooth
   ```

1. <span data-ttu-id="f3fe8-132">Start de Bluetooth-service op de IoT-gateway en voert u een Bluetooth-shell Bluetooth configureren met de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="f3fe8-132">Start the Bluetooth service on the IoT gateway and enter a Bluetooth shell to configure Bluetooth by running the following commands:</span></span>

   ```bash
   sudo systemctl start bluetooth
   bluetoothctl
   ```

1. <span data-ttu-id="f3fe8-133">De Bluetooth-controller door de volgende opdracht in de Bluetooth-shell inschakelen:</span><span class="sxs-lookup"><span data-stu-id="f3fe8-133">Power on the Bluetooth controller by running the following command at the Bluetooth shell:</span></span>

   ```bash
   power on
   ```

   ![de Bluetooth-controller hebben op de IoT-gateway met bluetoothctl inschakelen](./media/iot-hub-iot-gateway-connect-device-to-cloud/8_power-on-bluetooth-controller-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="f3fe8-135">Start scannen op in de buurt Bluetooth-apparaten met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="f3fe8-135">Start scanning for nearby Bluetooth devices by running the following command:</span></span>

   ```bash
   scan on
   ```

   ![In de buurt Bluetooth-apparaten met bluetoothctl scannen](./media/iot-hub-iot-gateway-connect-device-to-cloud/9_start-scan-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="f3fe8-137">Klik op koppelen op de SensorTag.</span><span class="sxs-lookup"><span data-stu-id="f3fe8-137">Press the pairing button on the SensorTag.</span></span> <span data-ttu-id="f3fe8-138">De groene geleid op de flitsen SensorTag.</span><span class="sxs-lookup"><span data-stu-id="f3fe8-138">The green LED on the SensorTag flashes.</span></span>
1. <span data-ttu-id="f3fe8-139">Op de Bluetooth-shell ziet u dat de SensorTag is gevonden.</span><span class="sxs-lookup"><span data-stu-id="f3fe8-139">At the Bluetooth shell, you should see the SensorTag is found.</span></span> <span data-ttu-id="f3fe8-140">Noteer het MAC-adres van de SensorTag.</span><span class="sxs-lookup"><span data-stu-id="f3fe8-140">Make a note of the MAC address of the SensorTag.</span></span> <span data-ttu-id="f3fe8-141">In dit voorbeeld wordt het MAC-adres van de SensorTag is `24:71:89:C0:7F:82`.</span><span class="sxs-lookup"><span data-stu-id="f3fe8-141">In this example, the MAC address of the SensorTag is `24:71:89:C0:7F:82`.</span></span>
1. <span data-ttu-id="f3fe8-142">De scan uitschakelen met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="f3fe8-142">Turn off the scan by running the following command:</span></span>

   ```bash
   scan off
   ```

   ![In de buurt Bluetooth-apparaten met bluetoothctl scannen stopzetten](./media/iot-hub-iot-gateway-connect-device-to-cloud/10_stop-scanning-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

### <a name="initiate-a-bluetooth-connection-from-the-iot-gateway-to-the-sensortag"></a><span data-ttu-id="f3fe8-144">Een Bluetooth-verbinding van de IoT-gateway naar de SensorTag starten</span><span class="sxs-lookup"><span data-stu-id="f3fe8-144">Initiate a Bluetooth connection from the IoT gateway to the SensorTag</span></span>

1. <span data-ttu-id="f3fe8-145">Verbinding maken met de SensorTag met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="f3fe8-145">Connect to the SensorTag by running the following command:</span></span>

   ```bash
   connect <MAC address>
   ```

   ![Verbinding maken met de SensorTag met bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/11_connect-to-sensortag-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="f3fe8-147">Verbreek de verbinding tussen de SensorTag en de Bluetooth-shell afsluiten met de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="f3fe8-147">Disconnect from the SensorTag and exit the Bluetooth shell by running the following commands:</span></span>

   ```bash
   disconnect
   exit
   ```

   ![Verbreek de verbinding tussen de SensorTag met bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/12_disconnect-from-sensortag-at-bluetooth-shell-bluetoothctl.png)

<span data-ttu-id="f3fe8-149">U hebt de verbinding tussen de SensorTag en de IoT-gateway is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="f3fe8-149">You've successfully enabled the connection between the SensorTag and the IoT gateway.</span></span>

## <a name="run-a-ble-sample-application-to-send-sensortag-data-to-your-iot-hub"></a><span data-ttu-id="f3fe8-150">Voer een voorbeeldtoepassing uitschakelen SensorTag gegevens verzenden naar uw IoT-hub</span><span class="sxs-lookup"><span data-stu-id="f3fe8-150">Run a BLE sample application to send SensorTag data to your IoT hub</span></span>

<span data-ttu-id="f3fe8-151">De voorbeeldtoepassing Bluetooth laag energieverbruik (uitschakelen) wordt verstrekt door Azure IoT rand.</span><span class="sxs-lookup"><span data-stu-id="f3fe8-151">The Bluetooth Low Energy (BLE) sample application is provided by Azure IoT Edge.</span></span> <span data-ttu-id="f3fe8-152">De voorbeeldtoepassing verzamelt gegevens van verbinding uitschakelen en de gegevens naar u IoT-hub te verzenden.</span><span class="sxs-lookup"><span data-stu-id="f3fe8-152">The sample application collects data from BLE connection and send the data to you IoT hub.</span></span> <span data-ttu-id="f3fe8-153">Als u wilt de voorbeeldtoepassing uitvoeren, moet u:</span><span class="sxs-lookup"><span data-stu-id="f3fe8-153">To run the sample application, you need to:</span></span>

1. <span data-ttu-id="f3fe8-154">Configureer de voorbeeldtoepassing.</span><span class="sxs-lookup"><span data-stu-id="f3fe8-154">Configure the sample application.</span></span>
1. <span data-ttu-id="f3fe8-155">De voorbeeldtoepassing uitvoeren op de IoT-gateway.</span><span class="sxs-lookup"><span data-stu-id="f3fe8-155">Run the sample application on the IoT gateway.</span></span>

### <a name="configure-the-sample-application"></a><span data-ttu-id="f3fe8-156">De voorbeeldtoepassing configureren</span><span class="sxs-lookup"><span data-stu-id="f3fe8-156">Configure the sample application</span></span>

1. <span data-ttu-id="f3fe8-157">Ga naar de map van de voorbeeldtoepassing met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="f3fe8-157">Go to the folder of the sample application by running the following command:</span></span>

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples/ble_gateway
   ```

1. <span data-ttu-id="f3fe8-158">Open het configuratiebestand met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="f3fe8-158">Open the configuration file by running the following command:</span></span>

   ```bash
   vi ble_gateway.json
   ```

1. <span data-ttu-id="f3fe8-159">Vul in het configuratiebestand in de volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="f3fe8-159">In the configuration file, fill in the following values:</span></span>

   <span data-ttu-id="f3fe8-160">**IoTHubName**: de naam van uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="f3fe8-160">**IoTHubName**: The name of your IoT hub.</span></span>

   <span data-ttu-id="f3fe8-161">**IoTHubSuffix**: IoTHubSuffix ophalen uit de primaire sleutel van de verbindingsreeks van het apparaat dat u hebt genoteerd omlaag.</span><span class="sxs-lookup"><span data-stu-id="f3fe8-161">**IoTHubSuffix**: Get IoTHubSuffix from the primary key of the device connection string that you noted down.</span></span> <span data-ttu-id="f3fe8-162">Zorgen ervoor dat u de primaire sleutel van de verbindingsreeks apparaat, niet de primaire sleutel van de verbindingsreeks van uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="f3fe8-162">Ensure that you get the primary key of the device connection string, not the primary key of your IoT hub connection string.</span></span> <span data-ttu-id="f3fe8-163">De primaire sleutel van de verbindingsreeks van het apparaat zich in de indeling van `HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY`.</span><span class="sxs-lookup"><span data-stu-id="f3fe8-163">The primary key of the device connection string is in the format of `HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY`.</span></span>

   <span data-ttu-id="f3fe8-164">**Transport**: de standaardwaarde is `amqp`.</span><span class="sxs-lookup"><span data-stu-id="f3fe8-164">**Transport**: The default value is `amqp`.</span></span> <span data-ttu-id="f3fe8-165">Deze waarde wordt het protocol tijdens transpotation weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f3fe8-165">This value shows the protocol during transpotation.</span></span> <span data-ttu-id="f3fe8-166">Kan de zijn `http`, `amqp`, of `mqtt`.</span><span class="sxs-lookup"><span data-stu-id="f3fe8-166">It could be `http`, `amqp`, or `mqtt`.</span></span>

   <span data-ttu-id="f3fe8-167">**macAddress**: de MAC-adres van de SensorTag die u hebt genoteerd omlaag.</span><span class="sxs-lookup"><span data-stu-id="f3fe8-167">**macAddress**: The MAC address of the SensorTag that you noted down.</span></span>

   <span data-ttu-id="f3fe8-168">**deviceID**: ID van het apparaat dat u hebt gemaakt in uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="f3fe8-168">**deviceID**: ID of the device that you created in your IoT hub.</span></span>

   <span data-ttu-id="f3fe8-169">**deviceKey**: de primaire sleutel van de verbindingsreeks van het apparaat.</span><span class="sxs-lookup"><span data-stu-id="f3fe8-169">**deviceKey**: The primary key of the device connection string.</span></span>

   ![Voltooien van het configuratiebestand van de voorbeeldtoepassing uitschakelen](./media/iot-hub-iot-gateway-connect-device-to-cloud/13_edit-config-file-of-ble-sample.png)

1. <span data-ttu-id="f3fe8-171">Druk op `ESC` en het type `:wq` het bestand wilt opslaan.</span><span class="sxs-lookup"><span data-stu-id="f3fe8-171">Press `ESC` and type `:wq` to save the file.</span></span>

### <a name="run-the-sample-application"></a><span data-ttu-id="f3fe8-172">De voorbeeldtoepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="f3fe8-172">Run the sample application</span></span>

1. <span data-ttu-id="f3fe8-173">Zorg ervoor dat de SensorTag is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="f3fe8-173">Make sure the SensorTag is powered on.</span></span>
1. <span data-ttu-id="f3fe8-174">Voer de volgende opdracht uit:</span><span class="sxs-lookup"><span data-stu-id="f3fe8-174">Run the following command:</span></span>

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a><span data-ttu-id="f3fe8-175">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f3fe8-175">Next steps</span></span>

[<span data-ttu-id="f3fe8-176">Gebruik IoT gateway voor gegevenstransformatie sensor met Azure IoT rand</span><span class="sxs-lookup"><span data-stu-id="f3fe8-176">Use IoT gateway for sensor data transformation with Azure IoT Edge</span></span>](iot-hub-gateway-kit-c-use-iot-gateway-for-data-conversion.md)
