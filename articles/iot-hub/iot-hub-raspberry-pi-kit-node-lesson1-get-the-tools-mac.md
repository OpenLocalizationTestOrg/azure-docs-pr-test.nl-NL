---
title: 'Frambozen Pi (knooppunt) verbinden met Azure IoT - les 1: download hulpprogramma''s (Mac OS) | Microsoft Docs'
description: Download en installeer de benodigde hulpprogramma's en -software voor de eerste voorbeeldtoepassing voor Pi op Mac OS.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: IOT-ontwikkeling, iot-software, internet van dingen software, python mac installeren, installeer git op mac, gulp uitvoeren, knooppunt js mac installeren
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 2ea6d211-c0e8-4ade-ac69-d1c2261d78c4
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 6c2338baa8e88bab4c4be64568220f53178943cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-macos-1010"></a><span data-ttu-id="62636-104">De hulpprogramma's downloaden (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="62636-104">Get the tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="62636-105">Windows 7 of hoger</span><span class="sxs-lookup"><span data-stu-id="62636-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="62636-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="62636-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="62636-107">Mac OS 10.10</span><span class="sxs-lookup"><span data-stu-id="62636-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="62636-108">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="62636-108">What you will do</span></span>
<span data-ttu-id="62636-109">Download de ontwikkelprogramma's en de software voor de eerste voorbeeldtoepassing voor uw frambozen Pi 3.</span><span class="sxs-lookup"><span data-stu-id="62636-109">Download the development tools and the software for the first sample application for your Raspberry Pi 3.</span></span> <span data-ttu-id="62636-110">Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="62636-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="62636-111">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="62636-111">What you will learn</span></span>
<span data-ttu-id="62636-112">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="62636-112">In this article, you will learn:</span></span>

* <span data-ttu-id="62636-113">Klik hier voor meer informatie over het installeren van Git en Node.js.</span><span class="sxs-lookup"><span data-stu-id="62636-113">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="62636-114">[GIT](https://git-scm.com) is een open-source gedistribueerd versiebeheersysteem.</span><span class="sxs-lookup"><span data-stu-id="62636-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="62636-115">De voorbeeldtoepassing voor dit artikel wordt opgeslagen op Git.</span><span class="sxs-lookup"><span data-stu-id="62636-115">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="62636-116">[Node.js](https://nodejs.org/en/) is een JavaScript-runtime met een uitgebreide pakket-ecosysteem.</span><span class="sxs-lookup"><span data-stu-id="62636-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="62636-117">Hoe extra Node.js ontwikkelingsprogramma's installeren met NPM.</span><span class="sxs-lookup"><span data-stu-id="62636-117">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="62636-118">De minimaal vereiste versie van Node.js is 4.5 TNS.</span><span class="sxs-lookup"><span data-stu-id="62636-118">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="62636-119">[NPM](https://www.npmjs.com) is een van de pakket-managers voor Node.js.</span><span class="sxs-lookup"><span data-stu-id="62636-119">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="62636-120">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="62636-120">What you need</span></span>
<span data-ttu-id="62636-121">Om deze bewerking niet voltooien, moet u het:</span><span class="sxs-lookup"><span data-stu-id="62636-121">To complete this operation, you will need:</span></span>

* <span data-ttu-id="62636-122">Een internetverbinding om de ontwikkelprogramma's en de software te downloaden.</span><span class="sxs-lookup"><span data-stu-id="62636-122">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="62636-123">Een Mac met Mac OS Yosemite (10.10) of hoger.</span><span class="sxs-lookup"><span data-stu-id="62636-123">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="62636-124">Installeer Git en Node.js</span><span class="sxs-lookup"><span data-stu-id="62636-124">Install Git and Node.js</span></span>
<span data-ttu-id="62636-125">U installeert Git en Node.js via de [Homebrew](http://brew.sh) het hulpprogramma voor het pakket met de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="62636-125">To install Git and Node.js, use the [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="62636-126">Homebrew installeren.</span><span class="sxs-lookup"><span data-stu-id="62636-126">Install Homebrew.</span></span> <span data-ttu-id="62636-127">Als u Homebrew al hebt geïnstalleerd, gaat u naar stap 2.</span><span class="sxs-lookup"><span data-stu-id="62636-127">If you've already installed Homebrew, go to step 2.</span></span>
   
   1. <span data-ttu-id="62636-128">Druk op `Cmd + Space` en voer `Terminal` een terminal openen.</span><span class="sxs-lookup"><span data-stu-id="62636-128">Press `Cmd + Space` and enter `Terminal` to open a terminal.</span></span>
   2. <span data-ttu-id="62636-129">Voer de volgende opdracht uit:</span><span class="sxs-lookup"><span data-stu-id="62636-129">Run the following command:</span></span>
      
      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="62636-130">Git en Node.js installeren met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="62636-130">Install Git and Node.js by running the following command:</span></span>
   
   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="62636-131">Extra hulpprogramma's voor Node.js-ontwikkeling</span><span class="sxs-lookup"><span data-stu-id="62636-131">Install additional Node.js development tools</span></span>
<span data-ttu-id="62636-132">Gebruik [gulp.js](http://gulpjs.com) voor het automatiseren van de implementatie van de voorbeeldtoepassing tot Pi.</span><span class="sxs-lookup"><span data-stu-id="62636-132">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to Pi.</span></span> <span data-ttu-id="62636-133">Gebruik de [apparaat detectie cli](https://github.com/Azure/device-discovery-cli) netwerkinformatie ophalen over uw IoT-apparaten.</span><span class="sxs-lookup"><span data-stu-id="62636-133">Use the [device-discovery-cli](https://github.com/Azure/device-discovery-cli) to retrieve network information about your IoT devices.</span></span>

<span data-ttu-id="62636-134">Installeer `gulp` en `device-discovery-cli` met de volgende opdracht in de terminal:</span><span class="sxs-lookup"><span data-stu-id="62636-134">Install `gulp` and `device-discovery-cli` by running the following command in the terminal:</span></span>

```bash
npm install -g device-discovery-cli gulp
```

<span data-ttu-id="62636-135">Als u problemen hebt met het Node.js en deze extra ontwikkelprogramma's installeert op Mac OS, Zie de [probleemoplossingsgids](iot-hub-raspberry-pi-kit-node-troubleshooting.md) voor oplossingen voor bekende problemen.</span><span class="sxs-lookup"><span data-stu-id="62636-135">If you experience issues installing Node.js and these additional development tools on macOS, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-node-troubleshooting.md) for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="62636-136">Visual Studio Code installeren</span><span class="sxs-lookup"><span data-stu-id="62636-136">Install Visual Studio Code</span></span>
<span data-ttu-id="62636-137">[Download](https://code.visualstudio.com/docs/setup/osx) en Visual Studio Code installeren.</span><span class="sxs-lookup"><span data-stu-id="62636-137">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="62636-138">Visual Studio Code is een eenvoudige maar krachtige broncode-editor voor Windows, Linux en Mac OS.</span><span class="sxs-lookup"><span data-stu-id="62636-138">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="62636-139">U gebruikt deze editor verderop in de zelfstudie voor het bewerken van de voorbeeldcode.</span><span class="sxs-lookup"><span data-stu-id="62636-139">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="62636-140">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="62636-140">Summary</span></span>
<span data-ttu-id="62636-141">U kunt de vereiste ontwikkelingsprogramma's en software voor de eerste voorbeeldtoepassing hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="62636-141">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="62636-142">De volgende taak is het maken, implementeren en uitvoeren van de voorbeeldtoepassing op Pi.</span><span class="sxs-lookup"><span data-stu-id="62636-142">The next task is to create, deploy, and run the sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="62636-143">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="62636-143">Next steps</span></span>
[<span data-ttu-id="62636-144">Maken en implementeren van de voorbeeldtoepassing knipperen</span><span class="sxs-lookup"><span data-stu-id="62636-144">Create and deploy the blink sample application</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-deploy-blink-app.md)

