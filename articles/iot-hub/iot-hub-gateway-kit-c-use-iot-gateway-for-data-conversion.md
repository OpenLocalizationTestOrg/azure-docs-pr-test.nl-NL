---
title: Gegevensconversie op IoT gateway met Azure IoT rand | Microsoft Docs
description: IoT gateway gebruiken voor het converteren van de indeling van sensorgegevens via een aangepaste module vanaf Azure IoT rand.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: conversie van IOT gateway, iot gateway gegevenstransformatie
ms.assetid: 75f2573d-500b-4405-bff7-61021c4c3500
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/25/2017
ms.author: xshi
ms.openlocfilehash: d5c735a4adbc59e9526ec4fd40720c5ec136d63d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="use-iot-gateway-for-sensor-data-transformation-with-azure-iot-edge"></a><span data-ttu-id="6c2ff-104">Gebruik IoT gateway voor gegevenstransformatie sensor met Azure IoT rand</span><span class="sxs-lookup"><span data-stu-id="6c2ff-104">Use IoT gateway for sensor data transformation with Azure IoT Edge</span></span>

> [!NOTE]
> <span data-ttu-id="6c2ff-105">Voordat u deze zelfstudie begint, zorg er dan voor dat u hebt de volgende uitkomsten voltooid in volgorde:</span><span class="sxs-lookup"><span data-stu-id="6c2ff-105">Before you start this tutorial, make sure you’ve completed the following lessons in sequence:</span></span>
> * [<span data-ttu-id="6c2ff-106">Intel NUC instellen als IoT-gateway</span><span class="sxs-lookup"><span data-stu-id="6c2ff-106">Set up Intel NUC as an IoT gateway</span></span>](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
> * [<span data-ttu-id="6c2ff-107">Gebruik IoT gateway dingen verbinding met de cloud - SensorTag met Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="6c2ff-107">Use IoT gateway to connect things to the cloud - SensorTag to Azure IoT Hub</span></span>](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)

<span data-ttu-id="6c2ff-108">Een doel van een Iot-gateway is verzamelde gegevens verwerken voordat deze naar de cloud verzonden.</span><span class="sxs-lookup"><span data-stu-id="6c2ff-108">One purpose of an Iot gateway is to process collected data before sending it to the cloud.</span></span> <span data-ttu-id="6c2ff-109">Azure IoT-rand introduceert modules die kunnen worden gemaakt en om de werkstroom gegevensverwerking samengesteld.</span><span class="sxs-lookup"><span data-stu-id="6c2ff-109">Azure IoT Edge introduces modules which can be created and assembled to form the data processing workflow.</span></span> <span data-ttu-id="6c2ff-110">Een module een bericht ontvangt, voert een bepaalde actie op deze en vervolgens voor andere modules verwerken op verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="6c2ff-110">A module receives a message, performs some action on it, and then move it on for other modules to process.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="6c2ff-111">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="6c2ff-111">What you learn</span></span>

<span data-ttu-id="6c2ff-112">U informatie over het maken van een module berichten uit de SensorTag converteren naar een andere indeling.</span><span class="sxs-lookup"><span data-stu-id="6c2ff-112">You learn how to create a module to convert messages from the SensorTag into a different format.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="6c2ff-113">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="6c2ff-113">What you do</span></span>

* <span data-ttu-id="6c2ff-114">Maakt een module voor het converteren van een ontvangen bericht naar de .json-indeling.</span><span class="sxs-lookup"><span data-stu-id="6c2ff-114">Create a module to convert a received message into the .json format.</span></span>
* <span data-ttu-id="6c2ff-115">De module worden gecompileerd.</span><span class="sxs-lookup"><span data-stu-id="6c2ff-115">Compile the module.</span></span>
* <span data-ttu-id="6c2ff-116">De module toevoegen aan de voorbeeldtoepassing uitschakelen vanaf Azure IoT rand.</span><span class="sxs-lookup"><span data-stu-id="6c2ff-116">Add the module to the BLE sample application from Azure IoT Edge.</span></span>
* <span data-ttu-id="6c2ff-117">De voorbeeldtoepassing uitvoert.</span><span class="sxs-lookup"><span data-stu-id="6c2ff-117">Run the sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="6c2ff-118">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="6c2ff-118">What you need</span></span>

* <span data-ttu-id="6c2ff-119">De volgende zelfstudies in de reeks voltooid:</span><span class="sxs-lookup"><span data-stu-id="6c2ff-119">The following tutorials completed in sequence:</span></span>
  * [<span data-ttu-id="6c2ff-120">Intel NUC instellen als IoT-gateway</span><span class="sxs-lookup"><span data-stu-id="6c2ff-120">Set up Intel NUC as an IoT gateway</span></span>](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
  * [<span data-ttu-id="6c2ff-121">Gebruik IoT gateway dingen verbinding met de cloud - SensorTag met Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="6c2ff-121">Use IoT gateway to connect things to the cloud - SensorTag to Azure IoT Hub</span></span>](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)
* <span data-ttu-id="6c2ff-122">Een SSH-client die wordt uitgevoerd op de hostcomputer.</span><span class="sxs-lookup"><span data-stu-id="6c2ff-122">An SSH client that runs on your host computer.</span></span> <span data-ttu-id="6c2ff-123">PuTTY wordt aanbevolen voor Windows.</span><span class="sxs-lookup"><span data-stu-id="6c2ff-123">PuTTY is recommended on Windows.</span></span> <span data-ttu-id="6c2ff-124">Linux- en Mac OS al worden geleverd met een SSH-client.</span><span class="sxs-lookup"><span data-stu-id="6c2ff-124">Linux and macOS already come with an SSH client.</span></span>
* <span data-ttu-id="6c2ff-125">Het IP-adres en de gebruikersnaam en wachtwoord voor toegang tot de gateway van de SSH-client.</span><span class="sxs-lookup"><span data-stu-id="6c2ff-125">The IP address and the username and password to access the gateway from the SSH client.</span></span>
* <span data-ttu-id="6c2ff-126">Een internetverbinding.</span><span class="sxs-lookup"><span data-stu-id="6c2ff-126">An Internet connection.</span></span>

## <a name="create-a-module"></a><span data-ttu-id="6c2ff-127">Een module maken</span><span class="sxs-lookup"><span data-stu-id="6c2ff-127">Create a module</span></span>

1. <span data-ttu-id="6c2ff-128">De SSH-client wordt uitgevoerd op de hostcomputer en maak verbinding met de IoT-gateway.</span><span class="sxs-lookup"><span data-stu-id="6c2ff-128">On the host computer, run the SSH client and connect to the IoT gateway.</span></span>
1. <span data-ttu-id="6c2ff-129">Kloon de bronbestanden van de module conversie vanuit GitHub naar de basismap van de IoT-gateway met de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="6c2ff-129">Clone the source files of the conversion module from GitHub to the home directory of the IoT gateway by running the following commands:</span></span>

   ```bash
   cd ~
   git clone https://github.com/Azure-Samples/iot-hub-c-intel-nuc-gateway-customized-module.git
   ```

   <span data-ttu-id="6c2ff-130">Dit is een systeemeigen Azure Edge-module, geschreven in de programmeertaal.</span><span class="sxs-lookup"><span data-stu-id="6c2ff-130">This is a native Azure Edge module written in the C programming language.</span></span> <span data-ttu-id="6c2ff-131">De module wordt de indeling van ontvangen berichten geconverteerd naar het volgende:</span><span class="sxs-lookup"><span data-stu-id="6c2ff-131">The module converts the format of received messages into the following one:</span></span>

   ```json
   {"deviceId": "Intel NUC Gateway", "messageId": 0, "temperature": 0.0}
   ```

## <a name="compile-the-module"></a><span data-ttu-id="6c2ff-132">De module niet compileren</span><span class="sxs-lookup"><span data-stu-id="6c2ff-132">Compile the module</span></span>

<span data-ttu-id="6c2ff-133">Samengesteld op basis van de module, voer de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="6c2ff-133">To compile the module, run the following commands:</span></span>

```bash
cd iot-hub-c-intel-nuc-gateway-customized-module/my_module
# change the build script runnable
chmod 777 build.sh
# remove the invalid windows character
sed -i -e "s/\r$//" build.sh
# run the build shell script
./build.sh
```

<span data-ttu-id="6c2ff-134">U krijgt een `libmy_module.so` bestand nadat het compileren is voltooid.</span><span class="sxs-lookup"><span data-stu-id="6c2ff-134">You get a `libmy_module.so` file after the compile is completed.</span></span> <span data-ttu-id="6c2ff-135">Noteer het absolute pad van dit bestand.</span><span class="sxs-lookup"><span data-stu-id="6c2ff-135">Make a note of the absolute path of this file.</span></span>

## <a name="add-the-module-to-the-ble-sample-application"></a><span data-ttu-id="6c2ff-136">De module toevoegen aan de voorbeeldtoepassing uitschakelen</span><span class="sxs-lookup"><span data-stu-id="6c2ff-136">Add the module to the BLE sample application</span></span>

1. <span data-ttu-id="6c2ff-137">Ga naar de map samples met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="6c2ff-137">Go to the samples folder by running the following command:</span></span>

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples
   ```

1. <span data-ttu-id="6c2ff-138">Open het configuratiebestand met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="6c2ff-138">Open the configuration file by running the following command:</span></span>

   ```bash
   vi ble_gateway.json
   ```

1. <span data-ttu-id="6c2ff-139">Een module toevoegen door het invoegen van de volgende code naar de `modules` sectie.</span><span class="sxs-lookup"><span data-stu-id="6c2ff-139">Add a module by inserting the following code to the `modules` section.</span></span>

   ```json
   {
       "name": "MyModule",
       "loader": {
           "name": "native",
           "entrypoint":{
               "module.path": "[Your libmy_module.so path]"
               }
            },
        "args": null
    },
    ```

1. <span data-ttu-id="6c2ff-140">Vervang `[Your libmy_module.so path]` in de code met het absolute pad van de libmy_module.so' bestand.</span><span class="sxs-lookup"><span data-stu-id="6c2ff-140">Replace `[Your libmy_module.so path]` in the code with the absolute path of the libmy_module.so\` file.</span></span>
1. <span data-ttu-id="6c2ff-141">Vervang de code in de `links` sectie met de volgende:</span><span class="sxs-lookup"><span data-stu-id="6c2ff-141">Replace the code in the `links` section with the following one:</span></span>

   ```json
   {
       "source": "SensorTag",
       "sink": "MyModule"
   },
   {
       "source": "MyModule",
       "sink": "mapping"
   }
   ```

1. <span data-ttu-id="6c2ff-142">Druk op `ESC`, en typ vervolgens `:wq` het bestand wilt opslaan.</span><span class="sxs-lookup"><span data-stu-id="6c2ff-142">Press `ESC`, and then type `:wq` to save the file.</span></span>

## <a name="run-the-sample-application"></a><span data-ttu-id="6c2ff-143">De voorbeeldtoepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="6c2ff-143">Run the sample application</span></span>

1. <span data-ttu-id="6c2ff-144">Zet de SensorTag.</span><span class="sxs-lookup"><span data-stu-id="6c2ff-144">Power on the SensorTag.</span></span>
1. <span data-ttu-id="6c2ff-145">De omgevingsvariabele SSL_CERT_FILE instellen met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="6c2ff-145">Set the SSL_CERT_FILE environment variable by running the following command:</span></span>

   ```bash
   export SSL_CERT_FILE=/etc/ssl/certs/ca-certificates.crt
   ```

1. <span data-ttu-id="6c2ff-146">Voer de voorbeeldtoepassing met de toegevoegde module met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="6c2ff-146">Run the sample application with the added module by running the following command:</span></span>

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a><span data-ttu-id="6c2ff-147">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6c2ff-147">Next steps</span></span>

<span data-ttu-id="6c2ff-148">U hebt de IoT-gateway is het bericht uit de SensorTag converteren naar de .json-indeling gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6c2ff-148">You’ve successfully use the IoT gateway to convert the message from SensorTag into the .json format.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
