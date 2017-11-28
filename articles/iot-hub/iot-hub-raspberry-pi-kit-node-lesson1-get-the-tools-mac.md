---
title: 'Verbinding maken met frambozen Pi (knooppunt) tooAzure IoT - les 1: download hulpprogramma''s (Mac OS) | Microsoft Docs'
description: Download en installeer de benodigde Hallo-hulpprogramma's en -software voor Hallo eerste voorbeeldtoepassing voor Pi op Mac OS.
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
ms.openlocfilehash: 382b066cb7ece7ffdeb22b162b725727b22e5fac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos-1010"></a><span data-ttu-id="2e2d5-104">Hallo hulpprogramma's (Mac OS 10.10) ophalen</span><span class="sxs-lookup"><span data-stu-id="2e2d5-104">Get hello tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2e2d5-105">Windows 7 of hoger</span><span class="sxs-lookup"><span data-stu-id="2e2d5-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="2e2d5-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="2e2d5-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="2e2d5-107">Mac OS 10.10</span><span class="sxs-lookup"><span data-stu-id="2e2d5-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="2e2d5-108">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="2e2d5-108">What you will do</span></span>
<span data-ttu-id="2e2d5-109">Hallo-software voor Hallo eerste voorbeeldtoepassing voor uw frambozen Pi 3 en Hallo ontwikkelingsprogramma's downloaden.</span><span class="sxs-lookup"><span data-stu-id="2e2d5-109">Download hello development tools and hello software for hello first sample application for your Raspberry Pi 3.</span></span> <span data-ttu-id="2e2d5-110">Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="2e2d5-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="2e2d5-111">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="2e2d5-111">What you will learn</span></span>
<span data-ttu-id="2e2d5-112">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="2e2d5-112">In this article, you will learn:</span></span>

* <span data-ttu-id="2e2d5-113">Hoe tooinstall Git en Node.js.</span><span class="sxs-lookup"><span data-stu-id="2e2d5-113">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="2e2d5-114">[GIT](https://git-scm.com) is een open-source gedistribueerd versiebeheersysteem.</span><span class="sxs-lookup"><span data-stu-id="2e2d5-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="2e2d5-115">Hallo-voorbeeldtoepassing voor dit artikel wordt opgeslagen op Git.</span><span class="sxs-lookup"><span data-stu-id="2e2d5-115">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="2e2d5-116">[Node.js](https://nodejs.org/en/) is een JavaScript-runtime met een uitgebreide pakket-ecosysteem.</span><span class="sxs-lookup"><span data-stu-id="2e2d5-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="2e2d5-117">Hoe toouse NPM tooinstall extra Node.js ontwikkelingsprogramma's.</span><span class="sxs-lookup"><span data-stu-id="2e2d5-117">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="2e2d5-118">Hallo minimaal vereiste versie van Node.js is 4.5 TNS.</span><span class="sxs-lookup"><span data-stu-id="2e2d5-118">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="2e2d5-119">[NPM](https://www.npmjs.com) is een van de Hallo pakket managers voor Node.js.</span><span class="sxs-lookup"><span data-stu-id="2e2d5-119">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="2e2d5-120">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="2e2d5-120">What you need</span></span>
<span data-ttu-id="2e2d5-121">toocomplete deze bewerking moet u:</span><span class="sxs-lookup"><span data-stu-id="2e2d5-121">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="2e2d5-122">Een Internet verbinding toodownload Hallo ontwikkelingsprogramma's en software Hallo.</span><span class="sxs-lookup"><span data-stu-id="2e2d5-122">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="2e2d5-123">Een Mac met Mac OS Yosemite (10.10) of hoger.</span><span class="sxs-lookup"><span data-stu-id="2e2d5-123">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="2e2d5-124">Installeer Git en Node.js</span><span class="sxs-lookup"><span data-stu-id="2e2d5-124">Install Git and Node.js</span></span>
<span data-ttu-id="2e2d5-125">tooinstall Git en Node.js, gebruikt u Hallo [Homebrew](http://brew.sh) het hulpprogramma voor het pakket met de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="2e2d5-125">tooinstall Git and Node.js, use hello [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="2e2d5-126">Homebrew installeren.</span><span class="sxs-lookup"><span data-stu-id="2e2d5-126">Install Homebrew.</span></span> <span data-ttu-id="2e2d5-127">Als u Homebrew al hebt geïnstalleerd, gaat u toostep 2.</span><span class="sxs-lookup"><span data-stu-id="2e2d5-127">If you've already installed Homebrew, go toostep 2.</span></span>
   
   1. <span data-ttu-id="2e2d5-128">Druk op `Cmd + Space` en voer `Terminal` tooopen een terminal.</span><span class="sxs-lookup"><span data-stu-id="2e2d5-128">Press `Cmd + Space` and enter `Terminal` tooopen a terminal.</span></span>
   2. <span data-ttu-id="2e2d5-129">Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="2e2d5-129">Run hello following command:</span></span>
      
      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="2e2d5-130">Installeer Git en Node.js Hallo na de opdracht uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="2e2d5-130">Install Git and Node.js by running hello following command:</span></span>
   
   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="2e2d5-131">Extra hulpprogramma's voor Node.js-ontwikkeling</span><span class="sxs-lookup"><span data-stu-id="2e2d5-131">Install additional Node.js development tools</span></span>
<span data-ttu-id="2e2d5-132">Gebruik [gulp.js](http://gulpjs.com) tooautomate Hallo implementatie van Hallo voorbeeld toepassing tooPi.</span><span class="sxs-lookup"><span data-stu-id="2e2d5-132">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooPi.</span></span> <span data-ttu-id="2e2d5-133">Gebruik Hallo [apparaat detectie cli](https://github.com/Azure/device-discovery-cli) tooretrieve netwerkinformatie over uw IoT-apparaten.</span><span class="sxs-lookup"><span data-stu-id="2e2d5-133">Use hello [device-discovery-cli](https://github.com/Azure/device-discovery-cli) tooretrieve network information about your IoT devices.</span></span>

<span data-ttu-id="2e2d5-134">Installeer `gulp` en `device-discovery-cli` door het uitvoeren van de volgende opdracht in de terminal Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="2e2d5-134">Install `gulp` and `device-discovery-cli` by running hello following command in hello terminal:</span></span>

```bash
npm install -g device-discovery-cli gulp
```

<span data-ttu-id="2e2d5-135">Als u problemen hebt met het Node.js en deze extra ontwikkelprogramma's installeert op Mac OS, Zie Hallo [probleemoplossingsgids](iot-hub-raspberry-pi-kit-node-troubleshooting.md) voor toocommon oplossingen voor problemen.</span><span class="sxs-lookup"><span data-stu-id="2e2d5-135">If you experience issues installing Node.js and these additional development tools on macOS, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-node-troubleshooting.md) for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="2e2d5-136">Visual Studio Code installeren</span><span class="sxs-lookup"><span data-stu-id="2e2d5-136">Install Visual Studio Code</span></span>
<span data-ttu-id="2e2d5-137">[Download](https://code.visualstudio.com/docs/setup/osx) en Visual Studio Code installeren.</span><span class="sxs-lookup"><span data-stu-id="2e2d5-137">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="2e2d5-138">Visual Studio Code is een eenvoudige maar krachtige broncode-editor voor Windows, Linux en Mac OS.</span><span class="sxs-lookup"><span data-stu-id="2e2d5-138">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="2e2d5-139">U gebruikt deze editor verderop in Hallo zelfstudie tooedit Hallo voorbeeldcode.</span><span class="sxs-lookup"><span data-stu-id="2e2d5-139">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="2e2d5-140">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="2e2d5-140">Summary</span></span>
<span data-ttu-id="2e2d5-141">U kunt Hallo vereist ontwikkelingsprogramma's en -software voor het eerste voorbeeldtoepassing hello hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="2e2d5-141">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="2e2d5-142">de volgende taak Hallo is toocreate, implementeren en uitvoeren van de voorbeeldtoepassing Hallo op Pi.</span><span class="sxs-lookup"><span data-stu-id="2e2d5-142">hello next task is toocreate, deploy, and run hello sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2e2d5-143">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2e2d5-143">Next steps</span></span>
[<span data-ttu-id="2e2d5-144">Hallo knipperen voorbeeldtoepassing maken en implementeren</span><span class="sxs-lookup"><span data-stu-id="2e2d5-144">Create and deploy hello blink sample application</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-deploy-blink-app.md)

