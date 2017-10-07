---
title: 'Gesimuleerde apparaat & Azure IoT Gateway - les 3: de berichten lezen | Microsoft Docs'
description: Een voorbeeld van code uitvoeren op uw host computer tooread Hallo-berichten uit uw IoT-hub.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: gegevens in de cloud hello, cloud gegevensverzameling, iot-cloudservice, iot-gegevens
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 5a6ec9c1-d83c-41c1-beaf-7c0d3395d77f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 540575724bb5cdac4db581a226d8a02a59004d8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="2acf3-104">Lezen van berichten uit uw IoT-hub</span><span class="sxs-lookup"><span data-stu-id="2acf3-104">Read messages from your IoT hub</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="2acf3-105">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="2acf3-105">What you will do</span></span>

- <span data-ttu-id="2acf3-106">Voorbeeldcode uitvoeren op uw host computer tooread berichten uit uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="2acf3-106">Run sample code on your host computer tooread messages from your IoT hub.</span></span>

<span data-ttu-id="2acf3-107">Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="2acf3-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="2acf3-108">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="2acf3-108">What you will learn</span></span>

<span data-ttu-id="2acf3-109">Hoe gulp toouse Hallo hulpprogramma tooread berichten van uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="2acf3-109">How toouse hello gulp tool tooread messages from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="2acf3-110">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="2acf3-110">What you need</span></span>

- <span data-ttu-id="2acf3-111">Hallo gesimuleerd apparaat voorbeeld in [configureren en voer een gesimuleerd apparaat cloud uploaden voorbeeldtoepassing](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span><span class="sxs-lookup"><span data-stu-id="2acf3-111">hello simulated device sample in [Configure and run a simulated device cloud upload sample application](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="2acf3-112">Ophalen van uw IoT-hub en apparaat-verbindingsreeksen</span><span class="sxs-lookup"><span data-stu-id="2acf3-112">Get your IoT hub and device connection strings</span></span>

<span data-ttu-id="2acf3-113">Hallo apparaat verbindingsreeks wordt gebruikt door uw gesimuleerde apparaat tooconnect tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="2acf3-113">hello device connection string is used by your simulated device tooconnect tooyour IoT hub.</span></span> <span data-ttu-id="2acf3-114">Hallo IoT hub-verbindingsreeks is gebruikte tooconnect toohello-identiteitenregister van uw IoT hub toomanage Hallo-apparaten die zijn toegestaan tooconnect tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="2acf3-114">hello IoT hub connection string is used tooconnect toohello identity registry in your IoT hub toomanage hello devices that are allowed tooconnect tooyour IoT hub.</span></span>

- <span data-ttu-id="2acf3-115">Een overzicht van uw IoT-hubs in uw resourcegroep door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="2acf3-115">List all your IoT hubs in your resource group by running hello following command:</span></span>

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   <span data-ttu-id="2acf3-116">Gebruik `iot-gateway` als Hallo-waarde van `{resource group name}` als u deze niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="2acf3-116">Use `iot-gateway` as hello value of `{resource group name}` if you didn't change it.</span></span>
- <span data-ttu-id="2acf3-117">Hallo IoT hub-verbindingsreeks ophalen door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="2acf3-117">Get hello IoT hub connection string by running hello following command:</span></span>

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   <span data-ttu-id="2acf3-118">`{my hub name}`Hallo-naam die u hebt opgegeven in les 2 is.</span><span class="sxs-lookup"><span data-stu-id="2acf3-118">`{my hub name}` is hello name that you specified in Lesson 2.</span></span>

## <a name="configure-hello-device-connection-for-hello-sample-code"></a><span data-ttu-id="2acf3-119">Hallo-apparaatverbinding Hallo voorbeeld van code configureren</span><span class="sxs-lookup"><span data-stu-id="2acf3-119">Configure hello device connection for hello sample code</span></span>

<span data-ttu-id="2acf3-120">Bijwerken van IoT hub en het apparaat verbinding configuraties in `config-azure.json` door Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="2acf3-120">Update IoT hub and device connection configurations in `config-azure.json` by performing hello following steps:</span></span>

1. <span data-ttu-id="2acf3-121">Open `config-azure.json` in Visual Studio Code door het uitvoeren van de volgende opdracht in een consolevenster Hallo:</span><span class="sxs-lookup"><span data-stu-id="2acf3-121">Open `config-azure.json` in Visual Studio Code by running hello following command in a console window:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. <span data-ttu-id="2acf3-122">Zorg Hallo vervangingen in Hallo na `config-azure.json` bestand:</span><span class="sxs-lookup"><span data-stu-id="2acf3-122">Make hello following replacements in hello `config-azure.json` file:</span></span>

   ![schermopname van azure config](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   <span data-ttu-id="2acf3-124">Vervang `[IoT hub connection string]` Hello IoT hub-verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="2acf3-124">Replace `[IoT hub connection string]` with hello IoT hub connection string.</span></span>

## <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="2acf3-125">Lezen van berichten uit uw IoT-hub</span><span class="sxs-lookup"><span data-stu-id="2acf3-125">Read messages from your IoT hub</span></span>

<span data-ttu-id="2acf3-126">Hallo gesimuleerd apparaat voorbeeldtoepassing uitvoeren en het lezen van de IoT Hub berichten door de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="2acf3-126">Run hello simulated device sample application and read IoT Hub messages by hello following command:</span></span>

```bash
gulp run --iot-hub
```

<span data-ttu-id="2acf3-127">Hallo-opdracht wordt uitgevoerd Hallo-toepassing die berichten tooyour iothub elke 2 seconden verzendt.</span><span class="sxs-lookup"><span data-stu-id="2acf3-127">hello command runs hello application that sends messages tooyour IoT hub every 2 seconds.</span></span> <span data-ttu-id="2acf3-128">Deze ook een onderliggend proces tooreceive Hallo-bericht gestart.</span><span class="sxs-lookup"><span data-stu-id="2acf3-128">It also spawns a child process tooreceive hello message.</span></span>

<span data-ttu-id="2acf3-129">Hallo-berichten die worden verzonden en ontvangen, worden alle weergegeven onmiddellijk op Hallo dezelfde consolevenster in Hallo hostmachine.</span><span class="sxs-lookup"><span data-stu-id="2acf3-129">hello messages that are being sent and received are all displayed instantly on hello same console window in hello host machine.</span></span> <span data-ttu-id="2acf3-130">Hallo-toepassing wordt afgesloten in 40 seconden.</span><span class="sxs-lookup"><span data-stu-id="2acf3-130">hello application will exit in 40 seconds.</span></span>

![Gesimuleerde voorbeeldtoepassing met verzonden en ontvangen berichten](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub_simudev.png)

## <a name="summary"></a><span data-ttu-id="2acf3-132">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="2acf3-132">Summary</span></span>

<span data-ttu-id="2acf3-133">U hebt Hallo voorbeeld toepassing toosend gegevens tooyour iothub met succes uitvoeren met het gesimuleerde apparaat.</span><span class="sxs-lookup"><span data-stu-id="2acf3-133">You've successfully run hello sample application toosend data tooyour IoT hub with simulated device.</span></span> <span data-ttu-id="2acf3-134">U hebt ook lezen Hallo-berichten die tooyour IoT-hub zijn verzonden.</span><span class="sxs-lookup"><span data-stu-id="2acf3-134">You've also read hello messages that have been sent tooyour IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2acf3-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2acf3-135">Next steps</span></span>
[<span data-ttu-id="2acf3-136">Een Azure Functions-app en Azure Storage-account maken</span><span class="sxs-lookup"><span data-stu-id="2acf3-136">Create an Azure function app and Azure Storage account</span></span>](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)


