---
title: 'Connect Arduino (C) tooAzure IoT - les 1: apparaat configureren | Microsoft Docs'
description: Configureer Adafruit Doezelaar M0 Wi-Fi voor eerste gebruik.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: arduino instellen, verbinding arduino toopc, setup arduino, arduino mededelingenbord
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: f5b334f0-a148-41aa-b374-ce7b9f5b305a
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 30b764e8ff6221995456283a226e79f064b2d74e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-device"></a><span data-ttu-id="da708-104">Uw apparaat configureren</span><span class="sxs-lookup"><span data-stu-id="da708-104">Configure your device</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="da708-105">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="da708-105">What you will do</span></span>
<span data-ttu-id="da708-106">Configureren het mededelingenbord Adafruit Doezelaar M0 Wi-Fi Arduino voor eerste gebruik Hallo mededelingenbord, het opstarten van en samen te stellen.</span><span class="sxs-lookup"><span data-stu-id="da708-106">Configure your Adafruit Feather M0 WiFi Arduino board for first-time use by assembling hello board, powering it up.</span></span> <span data-ttu-id="da708-107">Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="da708-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span></span>

## <a name="what-you-need"></a><span data-ttu-id="da708-108">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="da708-108">What you need</span></span>
<span data-ttu-id="da708-109">toocomplete deze bewerking moet u volgende onderdelen voor uw Adafruit Doezelaar M0 Wi-Fi Starter Kit Hallo:</span><span class="sxs-lookup"><span data-stu-id="da708-109">toocomplete this operation, you need hello following parts for your Adafruit Feather M0 WiFi Starter Kit:</span></span>

* <span data-ttu-id="da708-110">Hallo Adafruit Doezelaar M0 Wi-Fi mededelingenbord</span><span class="sxs-lookup"><span data-stu-id="da708-110">hello Adafruit Feather M0 WiFi board</span></span>
* <span data-ttu-id="da708-111">Een tooType Micro B een USB-kabel</span><span class="sxs-lookup"><span data-stu-id="da708-111">A Micro B tooType A USB cable</span></span>

![Kit][kit]

<span data-ttu-id="da708-113">U hebt ook het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="da708-113">You also need:</span></span>

* <span data-ttu-id="da708-114">Een computer met Windows, Mac of Linux.</span><span class="sxs-lookup"><span data-stu-id="da708-114">A computer running Windows, Mac, or Linux.</span></span>
* <span data-ttu-id="da708-115">Een draadloze verbinding voor uw Arduino mededelingenbord tooconnect aan.</span><span class="sxs-lookup"><span data-stu-id="da708-115">A wireless connection for your Arduino board tooconnect to.</span></span>
* <span data-ttu-id="da708-116">Een Internet verbinding toodownload configuratiehulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="da708-116">An Internet connection toodownload configuration tool.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="da708-117">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="da708-117">What you will learn</span></span>
<span data-ttu-id="da708-118">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="da708-118">In this article, you will learn:</span></span>

* <span data-ttu-id="da708-119">Hoe tooassemble Arduino mededelingenbord- en stroomkabels lessen deze voor hello te volgen.</span><span class="sxs-lookup"><span data-stu-id="da708-119">How tooassemble your Arduino board and power it up for hello following lessons.</span></span>
* <span data-ttu-id="da708-120">Hoe tooadd seriële poort machtigingen op Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="da708-120">How tooadd serial port permissions on Ubuntu.</span></span>

## <a name="connect-your-arduino-board-tooyour-computer"></a><span data-ttu-id="da708-121">Verbinding maken met uw computer Arduino mededelingenbord tooyour</span><span class="sxs-lookup"><span data-stu-id="da708-121">Connect your Arduino board tooyour computer</span></span>

1. <span data-ttu-id="da708-122">Hallo micro USB-kabel aansluiten op Hallo bovenste micro USB-poort.</span><span class="sxs-lookup"><span data-stu-id="da708-122">Plug hello micro USB cable into hello top micro USB port.</span></span>

   ![Bovenste micro USB-poort][top-micro-usb-port]

2. <span data-ttu-id="da708-124">Plug Hallo andere einde van USB-kabel op uw computer.</span><span class="sxs-lookup"><span data-stu-id="da708-124">Plug hello other end of USB cable into your computer.</span></span>

   ![Computer USB][computer-usb]

## <a name="add-serial-port-permissions-on-ubuntu"></a><span data-ttu-id="da708-126">Machtigingen van de seriële poort toevoegen aan Ubuntu</span><span class="sxs-lookup"><span data-stu-id="da708-126">Add serial port permissions on Ubuntu</span></span>

<span data-ttu-id="da708-127">Als u Windows of Mac OS gebruikt, kunt u deze sectie overslaan.</span><span class="sxs-lookup"><span data-stu-id="da708-127">You can skip this section if you use Windows or macOS.</span></span> <span data-ttu-id="da708-128">Ubuntu moet u Hallo stappen toomake ervoor Hallo normale linux gebruiker heeft Hallo machtigingen toooperate op Hallo USB-poort van het mededelingenbord Arduino te volgen.</span><span class="sxs-lookup"><span data-stu-id="da708-128">For Ubuntu, you need hello following steps toomake sure hello normal linux user has hello permissions toooperate on hello USB port of your Arduino board.</span></span>

1. <span data-ttu-id="da708-129">Nu als normale gebruiker in de terminal:</span><span class="sxs-lookup"><span data-stu-id="da708-129">Now as normal user from terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   # Or
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="da708-130">U ontvangt ongeveer als volgt:</span><span class="sxs-lookup"><span data-stu-id="da708-130">You will get something like:</span></span>

   ```bash
   crw-rw---- 1 root uucp 188, 0 5 apr 23.01 ttyUSB0
   # Or
   crw-rw---- 1 root dialout 188, 0 5 apr 23.01 ttyACM0
   ```

   <span data-ttu-id="da708-131">Hallo '0' mogelijk een ander nummer of meerdere items kunnen worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="da708-131">hello "0" might be a different number, or multiple entries might be returned.</span></span> <span data-ttu-id="da708-132">Hallo eerste case Hallo gegevens die we nodig is `uucp`, in Hallo is het tweede `dialout`, dit is de Groepseigenaar Hallo van Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="da708-132">In hello first case hello data we need is `uucp`, in hello second is `dialout`, which is hello group owner of hello file.</span></span>

2. <span data-ttu-id="da708-133">Gebruikersgroep toohello toohello toevoegen:</span><span class="sxs-lookup"><span data-stu-id="da708-133">Add user toohello toohello group:</span></span>

   ```bash
   sudo usermod -a -G group-name username
   ```

   <span data-ttu-id="da708-134">Waar `group-name` Hallo-gegevens gevonden in de eerste stap Hallo en `username` uw linux-gebruikersnaam.</span><span class="sxs-lookup"><span data-stu-id="da708-134">Where `group-name` is hello data found in hello first step, and `username` is your linux user name.</span></span>

3. <span data-ttu-id="da708-135">U moet toolog out en in opnieuw voor deze wijziging tootake effect en volledige Hallo setup.</span><span class="sxs-lookup"><span data-stu-id="da708-135">You will need toolog out and in again for this change tootake effect and complete hello setup.</span></span>

## <a name="summary"></a><span data-ttu-id="da708-136">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="da708-136">Summary</span></span>
<span data-ttu-id="da708-137">In dit artikel hebt u geleerd hoe tooconfigure het mededelingenbord Arduino.</span><span class="sxs-lookup"><span data-stu-id="da708-137">In this article, you’ve learned how tooconfigure your Arduino board.</span></span> <span data-ttu-id="da708-138">de volgende taak Hallo is tooinstall Hallo vereiste hulpprogramma's en software in voorbereiding voor het uitvoeren van een voorbeeld van toepassing op het mededelingenbord Arduino.</span><span class="sxs-lookup"><span data-stu-id="da708-138">hello next task is tooinstall hello necessary tools and software in preparation for running a sample application on your Arduino board.</span></span>

![Hardware is gereed][hardware-is-ready]

## <a name="next-steps"></a><span data-ttu-id="da708-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="da708-140">Next steps</span></span>
<span data-ttu-id="da708-141">[Hallo-hulpprogramma's ophalen][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="da708-141">[Get hello tools][get-the-tools]</span></span>
<!-- Images and links -->

[kit]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/kit.png
[top-micro-usb-port]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/top_usbport.jpg
[computer-usb]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/computer_usb.jpg
[hardware-is-ready]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/hardware_ready.jpg
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md