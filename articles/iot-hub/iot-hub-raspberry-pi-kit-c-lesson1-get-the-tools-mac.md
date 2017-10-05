---
title: 'Connect Raspberry PI (C) naar Azure IoT - les 1: download hulpprogramma''s (Mac OS) | Microsoft Docs'
description: Download en installeer de benodigde hulpprogramma's en -software voor de eerste voorbeeldtoepassing voor Pi op Mac OS.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: IOT-ontwikkeling, iot-software, internet van dingen software, git installeren op mac gulp uitvoert, installatie knooppunt js mac
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: fc6bd2c8-a847-4bf5-818f-6f7f9a6835ee
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 64db77040ef3482f213bd622320fdb5df243fa93
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-macos-1010"></a><span data-ttu-id="09e63-104">De hulpprogramma's downloaden (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="09e63-104">Get the tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="09e63-105">Windows 7 of hoger</span><span class="sxs-lookup"><span data-stu-id="09e63-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="09e63-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="09e63-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="09e63-107">Mac OS 10.10</span><span class="sxs-lookup"><span data-stu-id="09e63-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="09e63-108">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="09e63-108">What you will do</span></span>
<span data-ttu-id="09e63-109">Download de ontwikkelprogramma's en de software voor de eerste voorbeeldtoepassing voor uw frambozen Pi 3.</span><span class="sxs-lookup"><span data-stu-id="09e63-109">Download the development tools and the software for the first sample application for your Raspberry Pi 3.</span></span> <span data-ttu-id="09e63-110">Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="09e63-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

> [!NOTE]
> <span data-ttu-id="09e63-111">Hoewel de programmeertaal van de belangrijkste logica C, worden in welke opgedane Node.js-hulpprogramma's gebruikt voor apparaten detecteren en te bouwen en voorbeeldtoepassingen implementeren.</span><span class="sxs-lookup"><span data-stu-id="09e63-111">Although the programming language of the main logic is C, Node.js tools are used in the lessons to discover devices, and build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="09e63-112">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="09e63-112">What you will learn</span></span>
<span data-ttu-id="09e63-113">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="09e63-113">In this article, you will learn:</span></span>

* <span data-ttu-id="09e63-114">Klik hier voor meer informatie over het installeren van Git en Node.js.</span><span class="sxs-lookup"><span data-stu-id="09e63-114">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="09e63-115">[GIT](https://git-scm.com) is een open-source gedistribueerd versiebeheersysteem.</span><span class="sxs-lookup"><span data-stu-id="09e63-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="09e63-116">De voorbeeldtoepassing voor dit artikel wordt opgeslagen op Git.</span><span class="sxs-lookup"><span data-stu-id="09e63-116">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="09e63-117">[Node.js](https://nodejs.org/en/) is een JavaScript-runtime met een uitgebreide pakket-ecosysteem.</span><span class="sxs-lookup"><span data-stu-id="09e63-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="09e63-118">Hoe extra Node.js ontwikkelingsprogramma's installeren met NPM.</span><span class="sxs-lookup"><span data-stu-id="09e63-118">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="09e63-119">De minimaal vereiste versie van Node.js is 4.5 TNS.</span><span class="sxs-lookup"><span data-stu-id="09e63-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="09e63-120">[NPM](https://www.npmjs.com) is een van de pakket-managers voor Node.js.</span><span class="sxs-lookup"><span data-stu-id="09e63-120">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="09e63-121">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="09e63-121">What you need</span></span>
<span data-ttu-id="09e63-122">Om deze bewerking niet voltooien, moet u het:</span><span class="sxs-lookup"><span data-stu-id="09e63-122">To complete this operation, you will need:</span></span>

* <span data-ttu-id="09e63-123">Een internetverbinding om de ontwikkelprogramma's en de software te downloaden.</span><span class="sxs-lookup"><span data-stu-id="09e63-123">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="09e63-124">Een Mac met Mac OS Yosemite (10.10) of hoger.</span><span class="sxs-lookup"><span data-stu-id="09e63-124">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="09e63-125">Installeer Git en Node.js</span><span class="sxs-lookup"><span data-stu-id="09e63-125">Install Git and Node.js</span></span>
<span data-ttu-id="09e63-126">U installeert Git en Node.js via de [Homebrew](http://brew.sh) het hulpprogramma voor het pakket met de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="09e63-126">To install Git and Node.js, use the [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="09e63-127">Homebrew installeren.</span><span class="sxs-lookup"><span data-stu-id="09e63-127">Install Homebrew.</span></span> <span data-ttu-id="09e63-128">Als u Homebrew al hebt geïnstalleerd, gaat u naar stap 2.</span><span class="sxs-lookup"><span data-stu-id="09e63-128">If you've already installed Homebrew, go to step 2.</span></span>
   
   1. <span data-ttu-id="09e63-129">Druk op `Cmd + Space` en voer `Terminal` een terminal openen.</span><span class="sxs-lookup"><span data-stu-id="09e63-129">Press `Cmd + Space` and enter `Terminal` to open a terminal.</span></span>
   2. <span data-ttu-id="09e63-130">Voer de volgende opdracht uit:</span><span class="sxs-lookup"><span data-stu-id="09e63-130">Run the following command:</span></span>
      
      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="09e63-131">Git en Node.js installeren met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="09e63-131">Install Git and Node.js by running the following command:</span></span>
   
   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="09e63-132">Extra hulpprogramma's voor Node.js-ontwikkeling</span><span class="sxs-lookup"><span data-stu-id="09e63-132">Install additional Node.js development tools</span></span>
<span data-ttu-id="09e63-133">Gebruik [gulp.js](http://gulpjs.com) voor het automatiseren van de implementatie van de voorbeeldtoepassing op uw Pi.</span><span class="sxs-lookup"><span data-stu-id="09e63-133">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to your Pi.</span></span> <span data-ttu-id="09e63-134">Gebruik de [apparaat detectie cli](https://github.com/Azure/device-discovery-cli) netwerkinformatie ophalen over uw IoT-apparaten.</span><span class="sxs-lookup"><span data-stu-id="09e63-134">Use the [device-discovery-cli](https://github.com/Azure/device-discovery-cli) to retrieve network information about your IoT devices.</span></span>

<span data-ttu-id="09e63-135">Installeer `gulp` en `device-discovery-cli` met de volgende opdracht in de terminal:</span><span class="sxs-lookup"><span data-stu-id="09e63-135">Install `gulp` and `device-discovery-cli` by running the following command in the terminal:</span></span>

```bash
sudo npm install -g device-discovery-cli gulp
```

<span data-ttu-id="09e63-136">Als u problemen hebt met het Node.js en deze extra ontwikkelprogramma's installeert op Mac OS, Zie de [probleemoplossingsgids](iot-hub-raspberry-pi-kit-c-troubleshooting.md) voor oplossingen voor bekende problemen.</span><span class="sxs-lookup"><span data-stu-id="09e63-136">If you experience issues installing Node.js and these additional development tools on macOS, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="09e63-137">Visual Studio Code installeren</span><span class="sxs-lookup"><span data-stu-id="09e63-137">Install Visual Studio Code</span></span>
<span data-ttu-id="09e63-138">[Download](https://code.visualstudio.com/docs/setup/osx) en Visual Studio Code installeren.</span><span class="sxs-lookup"><span data-stu-id="09e63-138">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="09e63-139">Visual Studio Code is een eenvoudige maar krachtige broncode-editor voor Windows, Linux en Mac OS.</span><span class="sxs-lookup"><span data-stu-id="09e63-139">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="09e63-140">U gebruikt deze editor verderop in de zelfstudie voor het bewerken van de voorbeeldcode.</span><span class="sxs-lookup"><span data-stu-id="09e63-140">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="09e63-141">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="09e63-141">Summary</span></span>
<span data-ttu-id="09e63-142">U kunt de vereiste ontwikkelingsprogramma's en software voor de eerste voorbeeldtoepassing hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="09e63-142">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="09e63-143">De volgende taak is het maken, implementeren en uitvoeren van de voorbeeldtoepassing op Pi.</span><span class="sxs-lookup"><span data-stu-id="09e63-143">The next task is to create, deploy, and run the sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="09e63-144">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="09e63-144">Next steps</span></span>
[<span data-ttu-id="09e63-145">De Blink-toepassing maken en implementeren</span><span class="sxs-lookup"><span data-stu-id="09e63-145">Create and deploy the blink application</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)

