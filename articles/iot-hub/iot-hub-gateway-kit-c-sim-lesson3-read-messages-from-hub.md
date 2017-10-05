---
title: 'Gesimuleerde apparaat & Azure IoT Gateway - les 3: de berichten lezen | Microsoft Docs'
description: Een voorbeeld van code uitvoeren op de hostcomputer de berichten lezen uit uw IoT-hub.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: gegevens in de cloud, cloud gegevensverzameling, iot-cloudservice, iot-gegevens
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
ms.openlocfilehash: 9fbf7958e2437d274f2692dbc235ac8147bdfa63
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="c101b-104">Lezen van berichten uit uw IoT-hub</span><span class="sxs-lookup"><span data-stu-id="c101b-104">Read messages from your IoT hub</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="c101b-105">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="c101b-105">What you will do</span></span>

- <span data-ttu-id="c101b-106">Voorbeeldcode uitvoeren op de hostcomputer om berichten te lezen uit uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="c101b-106">Run sample code on your host computer to read messages from your IoT hub.</span></span>

<span data-ttu-id="c101b-107">Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="c101b-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="c101b-108">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="c101b-108">What you will learn</span></span>

<span data-ttu-id="c101b-109">Het gebruik van het hulpprogramma gulp om berichten te lezen uit uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="c101b-109">How to use the gulp tool to read messages from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="c101b-110">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="c101b-110">What you need</span></span>

- <span data-ttu-id="c101b-111">Het gesimuleerde apparaat voorbeeld in [configureren en voer een gesimuleerd apparaat cloud uploaden voorbeeldtoepassing](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span><span class="sxs-lookup"><span data-stu-id="c101b-111">The simulated device sample in [Configure and run a simulated device cloud upload sample application](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="c101b-112">Ophalen van uw IoT-hub en apparaat-verbindingsreeksen</span><span class="sxs-lookup"><span data-stu-id="c101b-112">Get your IoT hub and device connection strings</span></span>

<span data-ttu-id="c101b-113">De verbindingsreeks van het apparaat wordt gebruikt door uw gesimuleerde apparaat verbinding maken met uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="c101b-113">The device connection string is used by your simulated device to connect to your IoT hub.</span></span> <span data-ttu-id="c101b-114">De verbindingsreeks van de IoT-hub wordt gebruikt voor het verbinding maken met het identiteitenregister van uw IoT-hub voor het beheren van de apparaten die verbinding maken met uw IoT-hub zijn toegestaan.</span><span class="sxs-lookup"><span data-stu-id="c101b-114">The IoT hub connection string is used to connect to the identity registry in your IoT hub to manage the devices that are allowed to connect to your IoT hub.</span></span>

- <span data-ttu-id="c101b-115">Een overzicht van uw IoT-hubs in de resourcegroep met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="c101b-115">List all your IoT hubs in your resource group by running the following command:</span></span>

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   <span data-ttu-id="c101b-116">Gebruik `iot-gateway` als de waarde van `{resource group name}` als u deze niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="c101b-116">Use `iot-gateway` as the value of `{resource group name}` if you didn't change it.</span></span>
- <span data-ttu-id="c101b-117">De IoT hub-verbindingsreeks ophalen met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="c101b-117">Get the IoT hub connection string by running the following command:</span></span>

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   <span data-ttu-id="c101b-118">`{my hub name}`is de naam die u hebt opgegeven in les 2.</span><span class="sxs-lookup"><span data-stu-id="c101b-118">`{my hub name}` is the name that you specified in Lesson 2.</span></span>

## <a name="configure-the-device-connection-for-the-sample-code"></a><span data-ttu-id="c101b-119">Het apparaatverbinding configureren voor de voorbeeldcode</span><span class="sxs-lookup"><span data-stu-id="c101b-119">Configure the device connection for the sample code</span></span>

<span data-ttu-id="c101b-120">Bijwerken van IoT hub en het apparaat verbinding configuraties in `config-azure.json` door de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="c101b-120">Update IoT hub and device connection configurations in `config-azure.json` by performing the following steps:</span></span>

1. <span data-ttu-id="c101b-121">Open `config-azure.json` in Visual Studio Code met de volgende opdracht in een consolevenster:</span><span class="sxs-lookup"><span data-stu-id="c101b-121">Open `config-azure.json` in Visual Studio Code by running the following command in a console window:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. <span data-ttu-id="c101b-122">Controleer de volgende vervangingen in de `config-azure.json` bestand:</span><span class="sxs-lookup"><span data-stu-id="c101b-122">Make the following replacements in the `config-azure.json` file:</span></span>

   ![schermopname van azure config](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   <span data-ttu-id="c101b-124">Vervang `[IoT hub connection string]` met de verbindingsreeks van de IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="c101b-124">Replace `[IoT hub connection string]` with the IoT hub connection string.</span></span>

## <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="c101b-125">Lezen van berichten uit uw IoT-hub</span><span class="sxs-lookup"><span data-stu-id="c101b-125">Read messages from your IoT hub</span></span>

<span data-ttu-id="c101b-126">Voer de voorbeeldtoepassing gesimuleerde apparaat en IoT Hub berichten lezen door de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="c101b-126">Run the simulated device sample application and read IoT Hub messages by the following command:</span></span>

```bash
gulp run --iot-hub
```

<span data-ttu-id="c101b-127">De opdracht wordt de toepassing die berichten naar uw IoT-hub elke 2 seconden verzendt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c101b-127">The command runs the application that sends messages to your IoT hub every 2 seconds.</span></span> <span data-ttu-id="c101b-128">Deze ook een onderliggend proces voor het ontvangen van het bericht gestart.</span><span class="sxs-lookup"><span data-stu-id="c101b-128">It also spawns a child process to receive the message.</span></span>

<span data-ttu-id="c101b-129">De berichten die worden verzonden en ontvangen, worden alle weergegeven onmiddellijk op de dezelfde consolevenster in de hostmachine.</span><span class="sxs-lookup"><span data-stu-id="c101b-129">The messages that are being sent and received are all displayed instantly on the same console window in the host machine.</span></span> <span data-ttu-id="c101b-130">De toepassing wordt afgesloten in 40 seconden.</span><span class="sxs-lookup"><span data-stu-id="c101b-130">The application will exit in 40 seconds.</span></span>

![Gesimuleerde voorbeeldtoepassing met verzonden en ontvangen berichten](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub_simudev.png)

## <a name="summary"></a><span data-ttu-id="c101b-132">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="c101b-132">Summary</span></span>

<span data-ttu-id="c101b-133">U hebt de voorbeeldtoepassing gegevens verzenden naar uw IoT-hub met gesimuleerde apparaat uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c101b-133">You've successfully run the sample application to send data to your IoT hub with simulated device.</span></span> <span data-ttu-id="c101b-134">U hebt ook de berichten die zijn verzonden naar uw IoT-hub lezen.</span><span class="sxs-lookup"><span data-stu-id="c101b-134">You've also read the messages that have been sent to your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c101b-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c101b-135">Next steps</span></span>
[<span data-ttu-id="c101b-136">Een Azure Functions-app en Azure Storage-account maken</span><span class="sxs-lookup"><span data-stu-id="c101b-136">Create an Azure function app and Azure Storage account</span></span>](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)


