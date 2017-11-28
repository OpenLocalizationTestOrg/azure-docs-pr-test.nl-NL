---
title: conversie van aaaData bij IoT gateway met Azure IoT rand | Microsoft Docs
description: Gebruik IoT gateway tooconvert Hallo-indeling van sensorgegevens via een aangepaste module op basis van Azure IoT rand.
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
ms.openlocfilehash: ae94b1f96f36dfcb4f77fadc0ece3cff3d0bba91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-iot-gateway-for-sensor-data-transformation-with-azure-iot-edge"></a><span data-ttu-id="3533a-104">Gebruik IoT gateway voor gegevenstransformatie sensor met Azure IoT rand</span><span class="sxs-lookup"><span data-stu-id="3533a-104">Use IoT gateway for sensor data transformation with Azure IoT Edge</span></span>

> [!NOTE]
> <span data-ttu-id="3533a-105">Voordat u deze zelfstudie begint, zorg er dan voor dat u bent voltooide Hallo uitkomsten in de juiste volgorde te volgen:</span><span class="sxs-lookup"><span data-stu-id="3533a-105">Before you start this tutorial, make sure you’ve completed hello following lessons in sequence:</span></span>
> * [<span data-ttu-id="3533a-106">Intel NUC instellen als IoT-gateway</span><span class="sxs-lookup"><span data-stu-id="3533a-106">Set up Intel NUC as an IoT gateway</span></span>](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
> * [<span data-ttu-id="3533a-107">Gebruik IoT gateway tooconnect dingen toohello cloud - SensorTag tooAzure IoT-Hub</span><span class="sxs-lookup"><span data-stu-id="3533a-107">Use IoT gateway tooconnect things toohello cloud - SensorTag tooAzure IoT Hub</span></span>](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)

<span data-ttu-id="3533a-108">Een doel van een Iot-gateway is tooprocess verzamelde gegevens voordat u deze toohello cloud verzendt.</span><span class="sxs-lookup"><span data-stu-id="3533a-108">One purpose of an Iot gateway is tooprocess collected data before sending it toohello cloud.</span></span> <span data-ttu-id="3533a-109">Azure IoT-rand introduceert modules die gemaakt en gemonteerd tooform Hallo gegevensverwerking werkstroom worden kunnen.</span><span class="sxs-lookup"><span data-stu-id="3533a-109">Azure IoT Edge introduces modules which can be created and assembled tooform hello data processing workflow.</span></span> <span data-ttu-id="3533a-110">Een module een bericht ontvangt, voert een bepaalde actie op deze en vervolgens voor andere modules tooprocess op verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="3533a-110">A module receives a message, performs some action on it, and then move it on for other modules tooprocess.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="3533a-111">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="3533a-111">What you learn</span></span>

<span data-ttu-id="3533a-112">U leert hoe een module tooconvert toocreate van berichten van Hallo SensorTag naar een andere indeling.</span><span class="sxs-lookup"><span data-stu-id="3533a-112">You learn how toocreate a module tooconvert messages from hello SensorTag into a different format.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="3533a-113">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="3533a-113">What you do</span></span>

* <span data-ttu-id="3533a-114">Maak een module tooconvert een ontvangen bericht naar Hallo .json-indeling.</span><span class="sxs-lookup"><span data-stu-id="3533a-114">Create a module tooconvert a received message into hello .json format.</span></span>
* <span data-ttu-id="3533a-115">Hallo-module niet compileren.</span><span class="sxs-lookup"><span data-stu-id="3533a-115">Compile hello module.</span></span>
* <span data-ttu-id="3533a-116">Hallo module toohello uitschakelen-voorbeeldtoepassing uit Azure IoT rand toevoegen.</span><span class="sxs-lookup"><span data-stu-id="3533a-116">Add hello module toohello BLE sample application from Azure IoT Edge.</span></span>
* <span data-ttu-id="3533a-117">Hallo-voorbeeldtoepassing uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="3533a-117">Run hello sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="3533a-118">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="3533a-118">What you need</span></span>

* <span data-ttu-id="3533a-119">Hallo voltooid in de reeks zelfstudies te volgen:</span><span class="sxs-lookup"><span data-stu-id="3533a-119">hello following tutorials completed in sequence:</span></span>
  * [<span data-ttu-id="3533a-120">Intel NUC instellen als IoT-gateway</span><span class="sxs-lookup"><span data-stu-id="3533a-120">Set up Intel NUC as an IoT gateway</span></span>](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
  * [<span data-ttu-id="3533a-121">Gebruik IoT gateway tooconnect dingen toohello cloud - SensorTag tooAzure IoT-Hub</span><span class="sxs-lookup"><span data-stu-id="3533a-121">Use IoT gateway tooconnect things toohello cloud - SensorTag tooAzure IoT Hub</span></span>](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)
* <span data-ttu-id="3533a-122">Een SSH-client die wordt uitgevoerd op de hostcomputer.</span><span class="sxs-lookup"><span data-stu-id="3533a-122">An SSH client that runs on your host computer.</span></span> <span data-ttu-id="3533a-123">PuTTY wordt aanbevolen voor Windows.</span><span class="sxs-lookup"><span data-stu-id="3533a-123">PuTTY is recommended on Windows.</span></span> <span data-ttu-id="3533a-124">Linux- en Mac OS al worden geleverd met een SSH-client.</span><span class="sxs-lookup"><span data-stu-id="3533a-124">Linux and macOS already come with an SSH client.</span></span>
* <span data-ttu-id="3533a-125">Hallo IP-adres en Hallo gebruikersnaam en wachtwoord tooaccess Hallo gateway vanuit Hallo SSH-client.</span><span class="sxs-lookup"><span data-stu-id="3533a-125">hello IP address and hello username and password tooaccess hello gateway from hello SSH client.</span></span>
* <span data-ttu-id="3533a-126">Een internetverbinding.</span><span class="sxs-lookup"><span data-stu-id="3533a-126">An Internet connection.</span></span>

## <a name="create-a-module"></a><span data-ttu-id="3533a-127">Een module maken</span><span class="sxs-lookup"><span data-stu-id="3533a-127">Create a module</span></span>

1. <span data-ttu-id="3533a-128">Op de hostcomputer Hallo Hallo SSH-client wordt uitgevoerd en verbinding maken met toohello IoT gateway.</span><span class="sxs-lookup"><span data-stu-id="3533a-128">On hello host computer, run hello SSH client and connect toohello IoT gateway.</span></span>
1. <span data-ttu-id="3533a-129">Hallo-bronbestanden van Hallo conversie module op basis van GitHub toohello-basismappen van Hallo IoT gateway door het uitvoeren van de volgende opdrachten Hallo klonen:</span><span class="sxs-lookup"><span data-stu-id="3533a-129">Clone hello source files of hello conversion module from GitHub toohello home directory of hello IoT gateway by running hello following commands:</span></span>

   ```bash
   cd ~
   git clone https://github.com/Azure-Samples/iot-hub-c-intel-nuc-gateway-customized-module.git
   ```

   <span data-ttu-id="3533a-130">Dit is een systeemeigen Azure rand module, geschreven in Hallo programmeertaal.</span><span class="sxs-lookup"><span data-stu-id="3533a-130">This is a native Azure Edge module written in hello C programming language.</span></span> <span data-ttu-id="3533a-131">Hallo-indeling van ontvangen berichten converteert Hallo module naar Hallo volgt:</span><span class="sxs-lookup"><span data-stu-id="3533a-131">hello module converts hello format of received messages into hello following one:</span></span>

   ```json
   {"deviceId": "Intel NUC Gateway", "messageId": 0, "temperature": 0.0}
   ```

## <a name="compile-hello-module"></a><span data-ttu-id="3533a-132">Hallo-module niet compileren</span><span class="sxs-lookup"><span data-stu-id="3533a-132">Compile hello module</span></span>

<span data-ttu-id="3533a-133">toocompile Hallo-module, Hallo volgende opdrachten uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="3533a-133">toocompile hello module, run hello following commands:</span></span>

```bash
cd iot-hub-c-intel-nuc-gateway-customized-module/my_module
# change hello build script runnable
chmod 777 build.sh
# remove hello invalid windows character
sed -i -e "s/\r$//" build.sh
# run hello build shell script
./build.sh
```

<span data-ttu-id="3533a-134">U krijgt een `libmy_module.so` bestand nadat Hallo compileren is voltooid.</span><span class="sxs-lookup"><span data-stu-id="3533a-134">You get a `libmy_module.so` file after hello compile is completed.</span></span> <span data-ttu-id="3533a-135">Noteer Hallo absolute pad van dit bestand.</span><span class="sxs-lookup"><span data-stu-id="3533a-135">Make a note of hello absolute path of this file.</span></span>

## <a name="add-hello-module-toohello-ble-sample-application"></a><span data-ttu-id="3533a-136">Hallo module toohello uitschakelen voorbeeld van een toepassing toevoegen</span><span class="sxs-lookup"><span data-stu-id="3533a-136">Add hello module toohello BLE sample application</span></span>

1. <span data-ttu-id="3533a-137">Map met voorbeelden toohello gaan door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="3533a-137">Go toohello samples folder by running hello following command:</span></span>

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples
   ```

1. <span data-ttu-id="3533a-138">Hallo-configuratiebestand openen door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="3533a-138">Open hello configuration file by running hello following command:</span></span>

   ```bash
   vi ble_gateway.json
   ```

1. <span data-ttu-id="3533a-139">Een module toevoegen door het invoegen van de volgende code toohello Hallo `modules` sectie.</span><span class="sxs-lookup"><span data-stu-id="3533a-139">Add a module by inserting hello following code toohello `modules` section.</span></span>

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

1. <span data-ttu-id="3533a-140">Vervang `[Your libmy_module.so path]` in code met het absolute pad van Hallo libmy_module.so Hallo Hallo ' bestand.</span><span class="sxs-lookup"><span data-stu-id="3533a-140">Replace `[Your libmy_module.so path]` in hello code with hello absolute path of hello libmy_module.so\` file.</span></span>
1. <span data-ttu-id="3533a-141">Vervang de code Hallo in Hallo `links` sectie Hello volgt:</span><span class="sxs-lookup"><span data-stu-id="3533a-141">Replace hello code in hello `links` section with hello following one:</span></span>

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

1. <span data-ttu-id="3533a-142">Druk op `ESC`, en typ vervolgens `:wq` toosave Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="3533a-142">Press `ESC`, and then type `:wq` toosave hello file.</span></span>

## <a name="run-hello-sample-application"></a><span data-ttu-id="3533a-143">Hallo-voorbeeldtoepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="3533a-143">Run hello sample application</span></span>

1. <span data-ttu-id="3533a-144">Hallo SensorTag inschakelen.</span><span class="sxs-lookup"><span data-stu-id="3533a-144">Power on hello SensorTag.</span></span>
1. <span data-ttu-id="3533a-145">Hallo SSL_CERT_FILE omgevingsvariabele door het uitvoeren van de volgende opdracht Hallo instellen:</span><span class="sxs-lookup"><span data-stu-id="3533a-145">Set hello SSL_CERT_FILE environment variable by running hello following command:</span></span>

   ```bash
   export SSL_CERT_FILE=/etc/ssl/certs/ca-certificates.crt
   ```

1. <span data-ttu-id="3533a-146">Voer Hallo voorbeeldtoepassing met toegevoegde module Hallo door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="3533a-146">Run hello sample application with hello added module by running hello following command:</span></span>

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a><span data-ttu-id="3533a-147">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3533a-147">Next steps</span></span>

<span data-ttu-id="3533a-148">U hebt gebruikt Hallo IoT gateway tooconvert Hallo-bericht van SensorTag naar Hallo .json-indeling.</span><span class="sxs-lookup"><span data-stu-id="3533a-148">You’ve successfully use hello IoT gateway tooconvert hello message from SensorTag into hello .json format.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
