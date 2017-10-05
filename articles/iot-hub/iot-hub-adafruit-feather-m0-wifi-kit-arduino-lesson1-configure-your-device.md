---
title: 'Connect Arduino (C) naar Azure IoT - les 1: apparaat configureren | Microsoft Docs'
description: Configureer Adafruit Doezelaar M0 Wi-Fi voor eerste gebruik.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: arduino instellen, verbinding maken met arduino pc, setup arduino, arduino mededelingenbord
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
ms.openlocfilehash: 9e319292e5d30dea7e45857e435825861aad1c84
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-your-device"></a><span data-ttu-id="bde14-104">Uw apparaat configureren</span><span class="sxs-lookup"><span data-stu-id="bde14-104">Configure your device</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="bde14-105">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="bde14-105">What you will do</span></span>
<span data-ttu-id="bde14-106">Het mededelingenbord Adafruit Doezelaar M0 Wi-Fi Arduino voor eerste gebruik door de bestuur, het opstarten van samen te configureren.</span><span class="sxs-lookup"><span data-stu-id="bde14-106">Configure your Adafruit Feather M0 WiFi Arduino board for first-time use by assembling the board, powering it up.</span></span> <span data-ttu-id="bde14-107">Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="bde14-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span></span>

## <a name="what-you-need"></a><span data-ttu-id="bde14-108">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="bde14-108">What you need</span></span>
<span data-ttu-id="bde14-109">Om deze bewerking niet voltooien, moet u de volgende onderdelen voor uw Adafruit Doezelaar M0 Wi-Fi Starter Kit:</span><span class="sxs-lookup"><span data-stu-id="bde14-109">To complete this operation, you need the following parts for your Adafruit Feather M0 WiFi Starter Kit:</span></span>

* <span data-ttu-id="bde14-110">De Adafruit Doezelaar M0 Wi-Fi-kaart</span><span class="sxs-lookup"><span data-stu-id="bde14-110">The Adafruit Feather M0 WiFi board</span></span>
* <span data-ttu-id="bde14-111">Een B Micro van Type A USB-kabel</span><span class="sxs-lookup"><span data-stu-id="bde14-111">A Micro B to Type A USB cable</span></span>

![Kit][kit]

<span data-ttu-id="bde14-113">U hebt ook het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="bde14-113">You also need:</span></span>

* <span data-ttu-id="bde14-114">Een computer met Windows, Mac of Linux.</span><span class="sxs-lookup"><span data-stu-id="bde14-114">A computer running Windows, Mac, or Linux.</span></span>
* <span data-ttu-id="bde14-115">Een draadloze verbinding voor uw kaart Arduino verbinding maken met.</span><span class="sxs-lookup"><span data-stu-id="bde14-115">A wireless connection for your Arduino board to connect to.</span></span>
* <span data-ttu-id="bde14-116">Een internetverbinding beschikken om het downloaden van hulpprogramma voor serverconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="bde14-116">An Internet connection to download configuration tool.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="bde14-117">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="bde14-117">What you will learn</span></span>
<span data-ttu-id="bde14-118">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="bde14-118">In this article, you will learn:</span></span>

* <span data-ttu-id="bde14-119">Informatie over het samenstellen van het mededelingenbord Arduino en inschakelen voor de volgende uitkomsten.</span><span class="sxs-lookup"><span data-stu-id="bde14-119">How to assemble your Arduino board and power it up for the following lessons.</span></span>
* <span data-ttu-id="bde14-120">Het toevoegen van de seriële poort machtigingen op Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="bde14-120">How to add serial port permissions on Ubuntu.</span></span>

## <a name="connect-your-arduino-board-to-your-computer"></a><span data-ttu-id="bde14-121">Het mededelingenbord Arduino aansluiten op uw computer</span><span class="sxs-lookup"><span data-stu-id="bde14-121">Connect your Arduino board to your computer</span></span>

1. <span data-ttu-id="bde14-122">De micro USB-kabel aansluiten op de bovenste micro USB-poort.</span><span class="sxs-lookup"><span data-stu-id="bde14-122">Plug the micro USB cable into the top micro USB port.</span></span>

   ![Bovenste micro USB-poort][top-micro-usb-port]

2. <span data-ttu-id="bde14-124">Het andere einde van USB-kabel aansluiten op uw computer.</span><span class="sxs-lookup"><span data-stu-id="bde14-124">Plug the other end of USB cable into your computer.</span></span>

   ![Computer USB][computer-usb]

## <a name="add-serial-port-permissions-on-ubuntu"></a><span data-ttu-id="bde14-126">Machtigingen van de seriële poort toevoegen aan Ubuntu</span><span class="sxs-lookup"><span data-stu-id="bde14-126">Add serial port permissions on Ubuntu</span></span>

<span data-ttu-id="bde14-127">Als u Windows of Mac OS gebruikt, kunt u deze sectie overslaan.</span><span class="sxs-lookup"><span data-stu-id="bde14-127">You can skip this section if you use Windows or macOS.</span></span> <span data-ttu-id="bde14-128">Ubuntu moet u de volgende stappen uit om ervoor te zorgen dat de gebruiker normaal linux de machtigingen heeft voor de USB-poort van het mededelingenbord Arduino niet bewerken.</span><span class="sxs-lookup"><span data-stu-id="bde14-128">For Ubuntu, you need the following steps to make sure the normal linux user has the permissions to operate on the USB port of your Arduino board.</span></span>

1. <span data-ttu-id="bde14-129">Nu als normale gebruiker in de terminal:</span><span class="sxs-lookup"><span data-stu-id="bde14-129">Now as normal user from terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   # Or
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="bde14-130">U ontvangt ongeveer als volgt:</span><span class="sxs-lookup"><span data-stu-id="bde14-130">You will get something like:</span></span>

   ```bash
   crw-rw---- 1 root uucp 188, 0 5 apr 23.01 ttyUSB0
   # Or
   crw-rw---- 1 root dialout 188, 0 5 apr 23.01 ttyACM0
   ```

   <span data-ttu-id="bde14-131">De '0' mogelijk een ander nummer of meerdere items kunnen worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="bde14-131">The "0" might be a different number, or multiple entries might be returned.</span></span> <span data-ttu-id="bde14-132">In het eerste geval de gegevens die we nodig is `uucp`, wordt in de tweede `dialout`, dit is de eigenaar van de groep van het bestand.</span><span class="sxs-lookup"><span data-stu-id="bde14-132">In the first case the data we need is `uucp`, in the second is `dialout`, which is the group owner of the file.</span></span>

2. <span data-ttu-id="bde14-133">Gebruiker toevoegen aan de aan de groep:</span><span class="sxs-lookup"><span data-stu-id="bde14-133">Add user to the to the group:</span></span>

   ```bash
   sudo usermod -a -G group-name username
   ```

   <span data-ttu-id="bde14-134">Waar `group-name` zijn de gegevens gevonden in de eerste stap en `username` uw linux-gebruikersnaam.</span><span class="sxs-lookup"><span data-stu-id="bde14-134">Where `group-name` is the data found in the first step, and `username` is your linux user name.</span></span>

3. <span data-ttu-id="bde14-135">U moet zich aanmelden en opnieuw om deze wijziging van kracht en voltooit de installatie.</span><span class="sxs-lookup"><span data-stu-id="bde14-135">You will need to log out and in again for this change to take effect and complete the setup.</span></span>

## <a name="summary"></a><span data-ttu-id="bde14-136">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="bde14-136">Summary</span></span>
<span data-ttu-id="bde14-137">In dit artikel hebt u geleerd hoe het mededelingenbord Arduino configureren.</span><span class="sxs-lookup"><span data-stu-id="bde14-137">In this article, you’ve learned how to configure your Arduino board.</span></span> <span data-ttu-id="bde14-138">De volgende taak is het installeren van de benodigde hulpprogramma's en software in voorbereiding voor het uitvoeren van een voorbeeld van toepassing op het mededelingenbord Arduino.</span><span class="sxs-lookup"><span data-stu-id="bde14-138">The next task is to install the necessary tools and software in preparation for running a sample application on your Arduino board.</span></span>

![Hardware is gereed][hardware-is-ready]

## <a name="next-steps"></a><span data-ttu-id="bde14-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bde14-140">Next steps</span></span>
<span data-ttu-id="bde14-141">[Download de hulpprogramma 's][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="bde14-141">[Get the tools][get-the-tools]</span></span>
<!-- Images and links -->

[kit]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/kit.png
[top-micro-usb-port]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/top_usbport.jpg
[computer-usb]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/computer_usb.jpg
[hardware-is-ready]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/hardware_ready.jpg
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md