---
title: 'Verbinding maken met Arduino tooAzure IoT - les 1: download hulpprogramma''s (Mac OS) | Microsoft Docs'
description: Download en installeer de benodigde Hallo-hulpprogramma's en -software voor Hallo eerste voorbeeldtoepassing voor Adafruit Doezelaar M0 Wi-Fi op Mac OS.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: arduino ontwikkelingsprogramma's, iot-ontwikkeling, iot-software, internet van dingen software, git installeren op mac installatie knooppunt js mac
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 0262f3dd-0259-4eb0-962f-9fb534f8359e
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5fd306fecd7259fb8f1e99d76282a1e464c4d4f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos-1010"></a><span data-ttu-id="2b793-104">Hallo hulpprogramma's (Mac OS 10.10) ophalen</span><span class="sxs-lookup"><span data-stu-id="2b793-104">Get hello tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="2b793-105">[Windows 7 of hoger][windows]</span><span class="sxs-lookup"><span data-stu-id="2b793-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="2b793-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="2b793-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="2b793-107">[Mac OS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="2b793-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="2b793-108">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="2b793-108">What you will do</span></span>

<span data-ttu-id="2b793-109">Hallo ontwikkelingsprogramma's en software voor eerste voorbeeldtoepassing voor uw kaart Adafruit Doezelaar M0 Wi-Fi Arduino Hallo Hallo downloaden.</span><span class="sxs-lookup"><span data-stu-id="2b793-109">Download hello development tools and hello software for hello first sample application for your Adafruit Feather M0 WiFi Arduino board.</span></span> 

<span data-ttu-id="2b793-110">Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="2b793-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

> [!NOTE]
> <span data-ttu-id="2b793-111">Hoewel Hallo programmeertaal van logische Hallo Arduino is, wordt Node.js-hulpprogramma's worden gebruikt in Hallo uitkomsten toobuild en voorbeeldtoepassingen implementeren.</span><span class="sxs-lookup"><span data-stu-id="2b793-111">Although hello programming language of hello main logic is Arduino, Node.js tools are used in hello lessons toobuild and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="2b793-112">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="2b793-112">What you will learn</span></span>
<span data-ttu-id="2b793-113">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="2b793-113">In this article, you will learn:</span></span>

* <span data-ttu-id="2b793-114">Hoe tooinstall Git en Node.js.</span><span class="sxs-lookup"><span data-stu-id="2b793-114">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="2b793-115">[GIT](https://git-scm.com) is een open-source gedistribueerd versiebeheersysteem.</span><span class="sxs-lookup"><span data-stu-id="2b793-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="2b793-116">Hallo-voorbeeldtoepassing voor dit artikel wordt opgeslagen op Git.</span><span class="sxs-lookup"><span data-stu-id="2b793-116">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="2b793-117">[Node.js](https://nodejs.org/en/) is een JavaScript-runtime met een uitgebreide pakket-ecosysteem.</span><span class="sxs-lookup"><span data-stu-id="2b793-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="2b793-118">Hoe toouse NPM tooinstall extra Node.js ontwikkelingsprogramma's.</span><span class="sxs-lookup"><span data-stu-id="2b793-118">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="2b793-119">Hallo minimaal vereiste versie van Node.js is 4.5 TNS.</span><span class="sxs-lookup"><span data-stu-id="2b793-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="2b793-120">[NPM](https://www.npmjs.com) is een van de Hallo pakket managers voor Node.js.</span><span class="sxs-lookup"><span data-stu-id="2b793-120">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="2b793-121">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="2b793-121">What you need</span></span>
<span data-ttu-id="2b793-122">toocomplete deze bewerking moet u:</span><span class="sxs-lookup"><span data-stu-id="2b793-122">toocomplete this operation, you will need:</span></span>
* <span data-ttu-id="2b793-123">Een Internet verbinding toodownload Hallo ontwikkelingsprogramma's en software Hallo.</span><span class="sxs-lookup"><span data-stu-id="2b793-123">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="2b793-124">Een Mac met Mac OS Yosemite (10.10) of hoger.</span><span class="sxs-lookup"><span data-stu-id="2b793-124">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="2b793-125">Installeer Git en Node.js</span><span class="sxs-lookup"><span data-stu-id="2b793-125">Install Git and Node.js</span></span>
<span data-ttu-id="2b793-126">tooinstall Git en Node.js, gebruikt u Hallo [Homebrew](http://brew.sh) het hulpprogramma voor het pakket met de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="2b793-126">tooinstall Git and Node.js, use hello [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="2b793-127">Homebrew installeren.</span><span class="sxs-lookup"><span data-stu-id="2b793-127">Install Homebrew.</span></span> <span data-ttu-id="2b793-128">Als u Homebrew al hebt geïnstalleerd, gaat u toostep 2.</span><span class="sxs-lookup"><span data-stu-id="2b793-128">If you've already installed Homebrew, go toostep 2.</span></span>

   1. <span data-ttu-id="2b793-129">Druk op `Cmd + Space` en voer `Terminal` tooopen een terminal.</span><span class="sxs-lookup"><span data-stu-id="2b793-129">Press `Cmd + Space` and enter `Terminal` tooopen a terminal.</span></span>
   2. <span data-ttu-id="2b793-130">Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="2b793-130">Run hello following command:</span></span>

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="2b793-131">Installeer Git en Node.js Hallo na de opdracht uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="2b793-131">Install Git and Node.js by running hello following command:</span></span>

   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="2b793-132">Extra hulpprogramma's voor Node.js-ontwikkeling</span><span class="sxs-lookup"><span data-stu-id="2b793-132">Install additional Node.js development tools</span></span>
<span data-ttu-id="2b793-133">Gebruik [gulp.js](http://gulpjs.com) tooautomate Hallo implementatie van Hallo voorbeeld toepassing tooyour Arduino het mededelingenbord.</span><span class="sxs-lookup"><span data-stu-id="2b793-133">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooyour Arduino board.</span></span>

<span data-ttu-id="2b793-134">Installeer `gulp`, `device-discovery-cli` door het uitvoeren van de volgende opdracht in de terminal Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="2b793-134">Install `gulp`, `device-discovery-cli` by running hello following command in hello terminal:</span></span>

```bash
sudo npm install -g gulp device-discovery-cli
```

<span data-ttu-id="2b793-135">Als u problemen hebt met het Node.js en deze extra ontwikkelprogramma's installeert op Mac OS, Zie Hallo [probleemoplossingsgids] [ troubleshooting] voor toocommon oplossingen voor problemen.</span><span class="sxs-lookup"><span data-stu-id="2b793-135">If you experience issues installing Node.js and these additional development tools on macOS, see hello [troubleshooting guide][troubleshooting] for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="2b793-136">Visual Studio Code installeren</span><span class="sxs-lookup"><span data-stu-id="2b793-136">Install Visual Studio Code</span></span>
<span data-ttu-id="2b793-137">[Download](https://code.visualstudio.com/docs/setup/osx) en Visual Studio Code installeren.</span><span class="sxs-lookup"><span data-stu-id="2b793-137">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="2b793-138">Visual Studio Code is een eenvoudige maar krachtige broncode-editor voor Windows, Linux en Mac OS.</span><span class="sxs-lookup"><span data-stu-id="2b793-138">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="2b793-139">U gebruikt deze editor verderop in Hallo zelfstudie tooedit Hallo voorbeeldcode.</span><span class="sxs-lookup"><span data-stu-id="2b793-139">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="2b793-140">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="2b793-140">Summary</span></span>
<span data-ttu-id="2b793-141">U kunt Hallo vereist ontwikkelingsprogramma's en -software voor het eerste voorbeeldtoepassing hello hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="2b793-141">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="2b793-142">de volgende taak Hallo is toocreate, implementeren en Hallo voorbeeldtoepassing uitvoeren op het mededelingenbord Arduino.</span><span class="sxs-lookup"><span data-stu-id="2b793-142">hello next task is toocreate, deploy, and run hello sample application on your Arduino board.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b793-143">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2b793-143">Next steps</span></span>
<span data-ttu-id="2b793-144">[Hallo knipperen toepassing maken en implementeren][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="2b793-144">[Create and deploy hello blink application][create-and-deploy-the-blink-application]</span></span>
<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-mac.md
[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md