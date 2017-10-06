---
title: 'Verbinding maken met Arduino tooAzure IoT - les 1: download hulpprogramma''s (Ubuntu) | Microsoft Docs'
description: Download en installeer de benodigde Hallo-hulpprogramma's en -software voor Hallo eerste voorbeeldtoepassing voor Adafruit Doezelaar M0 Wi-Fi op Ubuntu.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: arduino ontwikkelingsprogramma's, iot-ontwikkeling, iot-software, internet van dingen software, git op ubuntu, installatie knooppunt js ubuntu installeren
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 7572f191-420d-41f0-923b-7ea86c0bfa73
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 586f89025d2fa11a31cb782e3789d306ade018a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-ubuntu-1604"></a><span data-ttu-id="580cd-104">Hallo hulpprogramma's (Ubuntu 16.04) ophalen</span><span class="sxs-lookup"><span data-stu-id="580cd-104">Get hello tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="580cd-105">[Windows 7 of hoger][windows]</span><span class="sxs-lookup"><span data-stu-id="580cd-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="580cd-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="580cd-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="580cd-107">[Mac OS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="580cd-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="580cd-108">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="580cd-108">What you will do</span></span>

<span data-ttu-id="580cd-109">Hallo ontwikkelingsprogramma's en software voor eerste voorbeeldtoepassing voor uw kaart Adafruit Doezelaar M0 Wi-Fi Arduino Hallo Hallo downloaden.</span><span class="sxs-lookup"><span data-stu-id="580cd-109">Download hello development tools and hello software for hello first sample application for your Adafruit Feather M0 WiFi Arduino board.</span></span> 

<span data-ttu-id="580cd-110">Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="580cd-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

> [!NOTE]
> <span data-ttu-id="580cd-111">Hoewel Hallo programmeertaal van logische Hallo Arduino is, wordt Node.js-hulpprogramma's worden gebruikt in Hallo uitkomsten toobuild en voorbeeldtoepassingen implementeren.</span><span class="sxs-lookup"><span data-stu-id="580cd-111">Although hello programming language of hello main logic is Arduino, Node.js tools are used in hello lessons toobuild and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="580cd-112">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="580cd-112">What you will learn</span></span>
<span data-ttu-id="580cd-113">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="580cd-113">In this article, you will learn:</span></span>

* <span data-ttu-id="580cd-114">Hoe tooinstall Git en Node.js</span><span class="sxs-lookup"><span data-stu-id="580cd-114">How tooinstall Git and Node.js</span></span>
  * <span data-ttu-id="580cd-115">[GIT](https://git-scm.com) is een open-source gedistribueerd versiebeheersysteem.</span><span class="sxs-lookup"><span data-stu-id="580cd-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="580cd-116">Hallo-voorbeeldtoepassing voor dit artikel wordt opgeslagen op Git.</span><span class="sxs-lookup"><span data-stu-id="580cd-116">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="580cd-117">[Node.js](https://nodejs.org/en/) is een JavaScript-runtime met een uitgebreide pakket-ecosysteem.</span><span class="sxs-lookup"><span data-stu-id="580cd-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="580cd-118">Hoe toouse NPM tooinstall extra Node.js ontwikkelingsprogramma's.</span><span class="sxs-lookup"><span data-stu-id="580cd-118">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="580cd-119">Hallo minimaal vereiste versie van Node.js is 4.5 TNS.</span><span class="sxs-lookup"><span data-stu-id="580cd-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="580cd-120">[NPM](https://www.npmjs.com) is een van de Hallo pakket managers voor Node.js.</span><span class="sxs-lookup"><span data-stu-id="580cd-120">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="580cd-121">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="580cd-121">What you need</span></span>
<span data-ttu-id="580cd-122">toocomplete deze bewerking moet u:</span><span class="sxs-lookup"><span data-stu-id="580cd-122">toocomplete this operation, you will need:</span></span>
* <span data-ttu-id="580cd-123">Een Internet verbinding toodownload Hallo ontwikkelingsprogramma's en software Hallo.</span><span class="sxs-lookup"><span data-stu-id="580cd-123">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="580cd-124">Een computer die Ubuntu 16.04 of hoger wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="580cd-124">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-nodejs-and-npm"></a><span data-ttu-id="580cd-125">Installeer Git, Node.js en NPM</span><span class="sxs-lookup"><span data-stu-id="580cd-125">Install Git, Node.js, and NPM</span></span>
<span data-ttu-id="580cd-126">Gebruik Hallo sneltoets `Ctrl + Alt + T` tooopen een terminal en Voer Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="580cd-126">Use hello keyboard shortcut `Ctrl + Alt + T` tooopen a terminal and run hello following commands:</span></span>

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="580cd-127">Extra hulpprogramma's voor Node.js-ontwikkeling</span><span class="sxs-lookup"><span data-stu-id="580cd-127">Install additional Node.js development tools</span></span>
<span data-ttu-id="580cd-128">Gebruik [gulp.js](http://gulpjs.com) tooautomate Hallo implementatie van Hallo voorbeeld toepassing tooyour Arduino het mededelingenbord.</span><span class="sxs-lookup"><span data-stu-id="580cd-128">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooyour Arduino board.</span></span>

<span data-ttu-id="580cd-129">Installeer `gulp`, `device-discovery-cli` door het uitvoeren van de volgende opdracht in de terminal Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="580cd-129">Install `gulp`, `device-discovery-cli` by running hello following command in hello terminal:</span></span>

```bash
sudo npm install -g gulp device-discovery-cli
```

<span data-ttu-id="580cd-130">Als u problemen hebt met het installeren van Node.js en deze extra ontwikkelprogramma's op Ubuntu, Zie Hallo [probleemoplossingsgids] [ troubleshooting] voor toocommon oplossingen voor problemen.</span><span class="sxs-lookup"><span data-stu-id="580cd-130">If you experience issues installing Node.js and these additional development tools on Ubuntu, see hello [troubleshooting guide][troubleshooting] for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="580cd-131">Visual Studio Code installeren</span><span class="sxs-lookup"><span data-stu-id="580cd-131">Install Visual Studio Code</span></span>
<span data-ttu-id="580cd-132">[Download](https://code.visualstudio.com/docs/setup/linux) en Visual Studio Code installeren.</span><span class="sxs-lookup"><span data-stu-id="580cd-132">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span> <span data-ttu-id="580cd-133">Visual Studio Code is een eenvoudige maar krachtige broncode-editor voor Windows, Linux en Mac OS.</span><span class="sxs-lookup"><span data-stu-id="580cd-133">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="580cd-134">U gebruikt deze editor verderop in Hallo zelfstudie tooedit Hallo voorbeeldcode.</span><span class="sxs-lookup"><span data-stu-id="580cd-134">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="580cd-135">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="580cd-135">Summary</span></span>
<span data-ttu-id="580cd-136">U kunt Hallo vereist ontwikkelingsprogramma's en -software voor het eerste voorbeeldtoepassing hello hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="580cd-136">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="580cd-137">de volgende taak Hallo is toocreate, implementeren en Hallo voorbeeldtoepassing uitvoeren op het mededelingenbord Arduino.</span><span class="sxs-lookup"><span data-stu-id="580cd-137">hello next task is toocreate, deploy, and run hello sample application on your Arduino board.</span></span>

## <a name="next-steps"></a><span data-ttu-id="580cd-138">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="580cd-138">Next steps</span></span>
<span data-ttu-id="580cd-139">[Hallo knipperen voorbeeldtoepassing maken en implementeren][create-and-deploy-the-blink-sample-application]</span><span class="sxs-lookup"><span data-stu-id="580cd-139">[Create and deploy hello blink sample application][create-and-deploy-the-blink-sample-application]</span></span>

<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-mac.md
[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[create-and-deploy-the-blink-sample-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md