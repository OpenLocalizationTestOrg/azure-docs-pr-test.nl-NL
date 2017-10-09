---
title: 'Connect Raspberry PI (C) tooAzure IoT - les 1: download hulpprogramma''s (Mac OS) | Microsoft Docs'
description: Download en installeer de benodigde Hallo-hulpprogramma's en -software voor Hallo eerste voorbeeldtoepassing voor Pi op Mac OS.
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
ms.openlocfilehash: 68ee44945dd69edcdf61ab3da4c80379c0ef955d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos-1010"></a><span data-ttu-id="ddead-104">Hallo hulpprogramma's (Mac OS 10.10) ophalen</span><span class="sxs-lookup"><span data-stu-id="ddead-104">Get hello tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ddead-105">Windows 7 of hoger</span><span class="sxs-lookup"><span data-stu-id="ddead-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="ddead-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="ddead-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="ddead-107">Mac OS 10.10</span><span class="sxs-lookup"><span data-stu-id="ddead-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="ddead-108">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="ddead-108">What you will do</span></span>
<span data-ttu-id="ddead-109">Hallo-software voor Hallo eerste voorbeeldtoepassing voor uw frambozen Pi 3 en Hallo ontwikkelingsprogramma's downloaden.</span><span class="sxs-lookup"><span data-stu-id="ddead-109">Download hello development tools and hello software for hello first sample application for your Raspberry Pi 3.</span></span> <span data-ttu-id="ddead-110">Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="ddead-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ddead-111">Hoewel Hallo programmeertaal van logische Hallo C, Node.js-hulpprogramma's worden gebruikt in Hallo uitkomsten toodiscover apparaten en voorbeeldtoepassingen maken en distribueren.</span><span class="sxs-lookup"><span data-stu-id="ddead-111">Although hello programming language of hello main logic is C, Node.js tools are used in hello lessons toodiscover devices, and build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="ddead-112">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="ddead-112">What you will learn</span></span>
<span data-ttu-id="ddead-113">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="ddead-113">In this article, you will learn:</span></span>

* <span data-ttu-id="ddead-114">Hoe tooinstall Git en Node.js.</span><span class="sxs-lookup"><span data-stu-id="ddead-114">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="ddead-115">[GIT](https://git-scm.com) is een open-source gedistribueerd versiebeheersysteem.</span><span class="sxs-lookup"><span data-stu-id="ddead-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="ddead-116">Hallo-voorbeeldtoepassing voor dit artikel wordt opgeslagen op Git.</span><span class="sxs-lookup"><span data-stu-id="ddead-116">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="ddead-117">[Node.js](https://nodejs.org/en/) is een JavaScript-runtime met een uitgebreide pakket-ecosysteem.</span><span class="sxs-lookup"><span data-stu-id="ddead-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="ddead-118">Hoe toouse NPM tooinstall extra Node.js ontwikkelingsprogramma's.</span><span class="sxs-lookup"><span data-stu-id="ddead-118">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="ddead-119">Hallo minimaal vereiste versie van Node.js is 4.5 TNS.</span><span class="sxs-lookup"><span data-stu-id="ddead-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="ddead-120">[NPM](https://www.npmjs.com) is een van de Hallo pakket managers voor Node.js.</span><span class="sxs-lookup"><span data-stu-id="ddead-120">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="ddead-121">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="ddead-121">What you need</span></span>
<span data-ttu-id="ddead-122">toocomplete deze bewerking moet u:</span><span class="sxs-lookup"><span data-stu-id="ddead-122">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="ddead-123">Een Internet verbinding toodownload Hallo ontwikkelingsprogramma's en software Hallo.</span><span class="sxs-lookup"><span data-stu-id="ddead-123">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="ddead-124">Een Mac met Mac OS Yosemite (10.10) of hoger.</span><span class="sxs-lookup"><span data-stu-id="ddead-124">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="ddead-125">Installeer Git en Node.js</span><span class="sxs-lookup"><span data-stu-id="ddead-125">Install Git and Node.js</span></span>
<span data-ttu-id="ddead-126">tooinstall Git en Node.js, gebruikt u Hallo [Homebrew](http://brew.sh) het hulpprogramma voor het pakket met de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="ddead-126">tooinstall Git and Node.js, use hello [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="ddead-127">Homebrew installeren.</span><span class="sxs-lookup"><span data-stu-id="ddead-127">Install Homebrew.</span></span> <span data-ttu-id="ddead-128">Als u Homebrew al hebt geïnstalleerd, gaat u toostep 2.</span><span class="sxs-lookup"><span data-stu-id="ddead-128">If you've already installed Homebrew, go toostep 2.</span></span>
   
   1. <span data-ttu-id="ddead-129">Druk op `Cmd + Space` en voer `Terminal` tooopen een terminal.</span><span class="sxs-lookup"><span data-stu-id="ddead-129">Press `Cmd + Space` and enter `Terminal` tooopen a terminal.</span></span>
   2. <span data-ttu-id="ddead-130">Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="ddead-130">Run hello following command:</span></span>
      
      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="ddead-131">Installeer Git en Node.js Hallo na de opdracht uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="ddead-131">Install Git and Node.js by running hello following command:</span></span>
   
   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="ddead-132">Extra hulpprogramma's voor Node.js-ontwikkeling</span><span class="sxs-lookup"><span data-stu-id="ddead-132">Install additional Node.js development tools</span></span>
<span data-ttu-id="ddead-133">Gebruik [gulp.js](http://gulpjs.com) tooautomate Hallo implementatie van Hallo voorbeeld toepassing tooyour Pi.</span><span class="sxs-lookup"><span data-stu-id="ddead-133">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooyour Pi.</span></span> <span data-ttu-id="ddead-134">Gebruik Hallo [apparaat detectie cli](https://github.com/Azure/device-discovery-cli) tooretrieve netwerkinformatie over uw IoT-apparaten.</span><span class="sxs-lookup"><span data-stu-id="ddead-134">Use hello [device-discovery-cli](https://github.com/Azure/device-discovery-cli) tooretrieve network information about your IoT devices.</span></span>

<span data-ttu-id="ddead-135">Installeer `gulp` en `device-discovery-cli` door het uitvoeren van de volgende opdracht in de terminal Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="ddead-135">Install `gulp` and `device-discovery-cli` by running hello following command in hello terminal:</span></span>

```bash
sudo npm install -g device-discovery-cli gulp
```

<span data-ttu-id="ddead-136">Als u problemen hebt met het Node.js en deze extra ontwikkelprogramma's installeert op Mac OS, Zie Hallo [probleemoplossingsgids](iot-hub-raspberry-pi-kit-c-troubleshooting.md) voor toocommon oplossingen voor problemen.</span><span class="sxs-lookup"><span data-stu-id="ddead-136">If you experience issues installing Node.js and these additional development tools on macOS, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="ddead-137">Visual Studio Code installeren</span><span class="sxs-lookup"><span data-stu-id="ddead-137">Install Visual Studio Code</span></span>
<span data-ttu-id="ddead-138">[Download](https://code.visualstudio.com/docs/setup/osx) en Visual Studio Code installeren.</span><span class="sxs-lookup"><span data-stu-id="ddead-138">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="ddead-139">Visual Studio Code is een eenvoudige maar krachtige broncode-editor voor Windows, Linux en Mac OS.</span><span class="sxs-lookup"><span data-stu-id="ddead-139">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="ddead-140">U gebruikt deze editor verderop in Hallo zelfstudie tooedit Hallo voorbeeldcode.</span><span class="sxs-lookup"><span data-stu-id="ddead-140">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="ddead-141">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="ddead-141">Summary</span></span>
<span data-ttu-id="ddead-142">U kunt Hallo vereist ontwikkelingsprogramma's en -software voor het eerste voorbeeldtoepassing hello hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="ddead-142">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="ddead-143">de volgende taak Hallo is toocreate, implementeren en uitvoeren van de voorbeeldtoepassing Hallo op Pi.</span><span class="sxs-lookup"><span data-stu-id="ddead-143">hello next task is toocreate, deploy, and run hello sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ddead-144">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ddead-144">Next steps</span></span>
[<span data-ttu-id="ddead-145">Hallo knipperen toepassing maken en implementeren</span><span class="sxs-lookup"><span data-stu-id="ddead-145">Create and deploy hello blink application</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)

