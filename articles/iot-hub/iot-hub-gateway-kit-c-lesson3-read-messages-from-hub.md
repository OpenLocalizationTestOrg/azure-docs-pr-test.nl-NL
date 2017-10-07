---
title: 'SensorTag apparaat & Azure IoT Gateway - les 3: de berichten lezen | Microsoft Docs'
description: Een voorbeeld van code uitvoeren op uw host computer tooread Hallo-berichten uit uw IoT-hub.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: gegevens in de cloud hello, cloud gegevensverzameling, iot-cloudservice, iot-gegevens
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: cc88be24-b5c0-4ef2-ba21-4e8f77f3e167
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d3ffbe2e83f9d61c0088b8876a7f0eea62c1fbe1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="96ee6-104">Lezen van berichten uit uw IoT-hub</span><span class="sxs-lookup"><span data-stu-id="96ee6-104">Read messages from your IoT hub</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="96ee6-105">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="96ee6-105">What you will do</span></span>

- <span data-ttu-id="96ee6-106">Voorbeeldcode uitvoeren op uw host computer tooread berichten uit uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="96ee6-106">Run sample code on your host computer tooread messages from your IoT hub.</span></span>

<span data-ttu-id="96ee6-107">Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="96ee6-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="96ee6-108">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="96ee6-108">What you will learn</span></span>

<span data-ttu-id="96ee6-109">Hoe gulp toouse Hallo hulpprogramma tooread berichten van uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="96ee6-109">How toouse hello gulp tool tooread messages from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="96ee6-110">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="96ee6-110">What you need</span></span>

- <span data-ttu-id="96ee6-111">Hallo uitschakelen-voorbeeldtoepassing die u in les 3 uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="96ee6-111">hello BLE sample application that you ran successfully in Lesson 3.</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="96ee6-112">Ophalen van uw IoT-hub en apparaat-verbindingsreeksen</span><span class="sxs-lookup"><span data-stu-id="96ee6-112">Get your IoT hub and device connection strings</span></span>

<span data-ttu-id="96ee6-113">Hallo apparaat verbindingsreeks wordt gebruikt door uw apparaat (TI SensorTag of gesimuleerd apparaat) tooconnect tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="96ee6-113">hello device connection string is used by your device (TI SensorTag or simulated device) tooconnect tooyour IoT hub.</span></span> <span data-ttu-id="96ee6-114">Hallo IoT hub-verbindingsreeks is gebruikte tooconnect toohello-identiteitenregister van uw IoT hub toomanage Hallo-apparaten die zijn toegestaan tooconnect tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="96ee6-114">hello IoT hub connection string is used tooconnect toohello identity registry in your IoT hub toomanage hello devices that are allowed tooconnect tooyour IoT hub.</span></span>

- <span data-ttu-id="96ee6-115">Een overzicht van uw IoT-hubs in uw resourcegroep door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="96ee6-115">List all your IoT hubs in your resource group by running hello following command:</span></span>

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   <span data-ttu-id="96ee6-116">Gebruik `iot-gateway` als Hallo-waarde van `{resource group name}` als u Hallo-waarde niet wijzigt.</span><span class="sxs-lookup"><span data-stu-id="96ee6-116">Use `iot-gateway` as hello value of `{resource group name}` if you didn't change hello value.</span></span>
- <span data-ttu-id="96ee6-117">Hallo IoT hub-verbindingsreeks ophalen door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="96ee6-117">Get hello IoT hub connection string by running hello following command:</span></span>

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   <span data-ttu-id="96ee6-118">`{my hub name}`Hallo-naam die u hebt opgegeven in les 2 is.</span><span class="sxs-lookup"><span data-stu-id="96ee6-118">`{my hub name}` is hello name that you specified in Lesson 2.</span></span>

## <a name="configure-hello-device-connection-for-hello-sample-code"></a><span data-ttu-id="96ee6-119">Hallo-apparaatverbinding Hallo voorbeeld van code configureren</span><span class="sxs-lookup"><span data-stu-id="96ee6-119">Configure hello device connection for hello sample code</span></span>

<span data-ttu-id="96ee6-120">Update Hallo apparaat configuratiebestand `config-azure.json` zodat u berichten uit uw IoT-hub op de hostcomputer lezen kan.</span><span class="sxs-lookup"><span data-stu-id="96ee6-120">Update hello device configuration file `config-azure.json` so that you can read messages from your IoT hub on your host computer.</span></span> <span data-ttu-id="96ee6-121">toodo dit als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="96ee6-121">toodo this, follow these steps:</span></span>

1. <span data-ttu-id="96ee6-122">Open `config-azure.json` in Visual Studio Code door het uitvoeren van de volgende opdracht in een consolevenster Hallo:</span><span class="sxs-lookup"><span data-stu-id="96ee6-122">Open `config-azure.json` in Visual Studio Code by running hello following command in a console window:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. <span data-ttu-id="96ee6-123">Zorg Hallo vervangingen in Hallo na `config-azure.json` bestand:</span><span class="sxs-lookup"><span data-stu-id="96ee6-123">Make hello following replacements in hello `config-azure.json` file:</span></span>

   ![schermopname van azure config](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   <span data-ttu-id="96ee6-125">Vervang `[IoT hub connection string]` Hello verbindingsreeks van het IoT-hub die u hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="96ee6-125">Replace `[IoT hub connection string]` with hello IoT hub connection string that you obtained.</span></span>

## <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="96ee6-126">Lezen van berichten uit uw IoT-hub</span><span class="sxs-lookup"><span data-stu-id="96ee6-126">Read messages from your IoT hub</span></span>

<span data-ttu-id="96ee6-127">Als u een SensorTag TI hebt, zorg er dan voor dat uw SensorTag is al ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="96ee6-127">If you have a TI SensorTag, make sure you have already powered on your SensorTag.</span></span> <span data-ttu-id="96ee6-128">Hallo gateway voorbeeldtoepassing uitvoeren en het lezen van de IoT Hub berichten door de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="96ee6-128">Run hello gateway sample application and read IoT Hub messages by hello following command:</span></span>

```bash
gulp run --iot-hub
```

<span data-ttu-id="96ee6-129">Hallo-opdracht wordt uitgevoerd Hallo uitschakelen-voorbeeldtoepassing die leest en pakketten temperatuur gegevens van uw SensorTag of het gesimuleerde apparaat en elke 2 seconden voor Hallo-bericht tooyour iothub verzendt.</span><span class="sxs-lookup"><span data-stu-id="96ee6-129">hello command runs hello BLE sample application that reads and packages temperature data from your SensorTag or simulated device and sends hello message tooyour IoT hub every 2 seconds.</span></span> <span data-ttu-id="96ee6-130">Deze ook een onderliggend proces tooreceive Hallo-bericht gestart.</span><span class="sxs-lookup"><span data-stu-id="96ee6-130">It also spawns a child process tooreceive hello message.</span></span>

<span data-ttu-id="96ee6-131">Hallo-berichten die worden verzonden en ontvangen, worden alle weergegeven onmiddellijk op Hallo dezelfde consolevenster in Hallo hostmachine.</span><span class="sxs-lookup"><span data-stu-id="96ee6-131">hello messages that are being sent and received are all displayed instantly on hello same console window in hello host machine.</span></span> <span data-ttu-id="96ee6-132">Hallo voorbeeld toepassingsexemplaar wordt in 40 seconden automatisch beëindigd.</span><span class="sxs-lookup"><span data-stu-id="96ee6-132">hello sample application instance will terminate automatically in 40 seconds.</span></span>

![Voorbeeldtoepassing uitschakelen met verzonden en ontvangen van berichten](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub.png)

## <a name="summary"></a><span data-ttu-id="96ee6-134">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="96ee6-134">Summary</span></span>

<span data-ttu-id="96ee6-135">U hebt een code voorbeeld tooread berichten uitvoeren van uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="96ee6-135">You've run a sample code tooread messages from your IoT hub.</span></span> <span data-ttu-id="96ee6-136">U bent klaar tooread Hallo-berichten die zijn opgeslagen in uw Azure-tabelopslag.</span><span class="sxs-lookup"><span data-stu-id="96ee6-136">You're ready tooread hello messages that are stored in your Azure table storage.</span></span>

## <a name="next-steps"></a><span data-ttu-id="96ee6-137">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="96ee6-137">Next steps</span></span>
[<span data-ttu-id="96ee6-138">Een Azure Functions-app en Azure Storage-account maken</span><span class="sxs-lookup"><span data-stu-id="96ee6-138">Create an Azure function app and Azure Storage account</span></span>](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)


