---
title: 'Verbinding maken met Intel Edison (knooppunt) tooAzure IoT - les 1: download hulpprogramma''s (Mac OS) | Microsoft Docs'
description: Download en installeer de benodigde Hallo-hulpprogramma's en -software voor Hallo eerste voorbeeldtoepassing voor Edison op Mac OS.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: arduino ontwikkelingsprogramma's, iot-ontwikkeling, iot-software, internet van dingen software, git installeren op mac installatie knooppunt js mac
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: fb6742be-2825-4524-89f7-8ccb7e7f1de1
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: f32c0ea3c69eb2f912171fd694ae883d2586c72e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos-1010"></a><span data-ttu-id="01a55-104">Hallo hulpprogramma's (Mac OS 10.10) ophalen</span><span class="sxs-lookup"><span data-stu-id="01a55-104">Get hello tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="01a55-105">[Windows 7 of hoger][windows]</span><span class="sxs-lookup"><span data-stu-id="01a55-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="01a55-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="01a55-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="01a55-107">[Mac OS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="01a55-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="01a55-108">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="01a55-108">What you will do</span></span>
<span data-ttu-id="01a55-109">Hallo ontwikkelingsprogramma's en software voor eerste voorbeeldtoepassing voor uw Edison Intel Hallo Hallo downloaden.</span><span class="sxs-lookup"><span data-stu-id="01a55-109">Download hello development tools and hello software for hello first sample application for your Intel Edison.</span></span> <span data-ttu-id="01a55-110">Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="01a55-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="01a55-111">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="01a55-111">What you will learn</span></span>
<span data-ttu-id="01a55-112">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="01a55-112">In this article, you will learn:</span></span>

* <span data-ttu-id="01a55-113">Hoe tooinstall Git en Node.js.</span><span class="sxs-lookup"><span data-stu-id="01a55-113">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="01a55-114">[GIT](https://git-scm.com) is een open-source gedistribueerd versiebeheersysteem.</span><span class="sxs-lookup"><span data-stu-id="01a55-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="01a55-115">Hallo-voorbeeldtoepassing voor dit artikel wordt opgeslagen op Git.</span><span class="sxs-lookup"><span data-stu-id="01a55-115">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="01a55-116">[Node.js](https://nodejs.org/en/) is een JavaScript-runtime met een uitgebreide pakket-ecosysteem.</span><span class="sxs-lookup"><span data-stu-id="01a55-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="01a55-117">Hoe toouse NPM tooinstall extra Node.js ontwikkelingsprogramma's.</span><span class="sxs-lookup"><span data-stu-id="01a55-117">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="01a55-118">Hallo minimaal vereiste versie van Node.js is 4.5 TNS.</span><span class="sxs-lookup"><span data-stu-id="01a55-118">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="01a55-119">[NPM](https://www.npmjs.com) is een van de Hallo pakket managers voor Node.js.</span><span class="sxs-lookup"><span data-stu-id="01a55-119">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="01a55-120">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="01a55-120">What you need</span></span>
<span data-ttu-id="01a55-121">toocomplete deze bewerking moet u:</span><span class="sxs-lookup"><span data-stu-id="01a55-121">toocomplete this operation, you will need:</span></span>
* <span data-ttu-id="01a55-122">Een Internet verbinding toodownload Hallo ontwikkelingsprogramma's en software Hallo.</span><span class="sxs-lookup"><span data-stu-id="01a55-122">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="01a55-123">Een Mac met Mac OS Yosemite (10.10) of hoger.</span><span class="sxs-lookup"><span data-stu-id="01a55-123">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="01a55-124">Installeer Git en Node.js</span><span class="sxs-lookup"><span data-stu-id="01a55-124">Install Git and Node.js</span></span>
<span data-ttu-id="01a55-125">tooinstall Git en Node.js, gebruikt u Hallo [Homebrew](http://brew.sh) het hulpprogramma voor het pakket met de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="01a55-125">tooinstall Git and Node.js, use hello [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="01a55-126">Homebrew installeren.</span><span class="sxs-lookup"><span data-stu-id="01a55-126">Install Homebrew.</span></span> <span data-ttu-id="01a55-127">Als u Homebrew al hebt geïnstalleerd, gaat u toostep 2.</span><span class="sxs-lookup"><span data-stu-id="01a55-127">If you've already installed Homebrew, go toostep 2.</span></span>

   1. <span data-ttu-id="01a55-128">Druk op `Cmd + Space` en voer `Terminal` tooopen een terminal.</span><span class="sxs-lookup"><span data-stu-id="01a55-128">Press `Cmd + Space` and enter `Terminal` tooopen a terminal.</span></span>
   2. <span data-ttu-id="01a55-129">Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="01a55-129">Run hello following command:</span></span>

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="01a55-130">Installeer Git en Node.js Hallo na de opdracht uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="01a55-130">Install Git and Node.js by running hello following command:</span></span>

   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="01a55-131">Extra hulpprogramma's voor Node.js-ontwikkeling</span><span class="sxs-lookup"><span data-stu-id="01a55-131">Install additional Node.js development tools</span></span>
<span data-ttu-id="01a55-132">Gebruik [gulp.js](http://gulpjs.com) tooautomate Hallo implementatie van Hallo voorbeeld toepassing tooyour Edison.</span><span class="sxs-lookup"><span data-stu-id="01a55-132">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooyour Edison.</span></span>

<span data-ttu-id="01a55-133">Installeer `gulp` door het uitvoeren van de volgende opdracht in de terminal Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="01a55-133">Install `gulp` by running hello following command in hello terminal:</span></span>

```bash
sudo npm install -g gulp
```

<span data-ttu-id="01a55-134">Als u problemen hebt met het Node.js en deze extra ontwikkelprogramma's installeert op Mac OS, Zie Hallo [probleemoplossingsgids] [ troubleshooting] voor toocommon oplossingen voor problemen.</span><span class="sxs-lookup"><span data-stu-id="01a55-134">If you experience issues installing Node.js and these additional development tools on macOS, see hello [troubleshooting guide][troubleshooting] for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="01a55-135">Visual Studio Code installeren</span><span class="sxs-lookup"><span data-stu-id="01a55-135">Install Visual Studio Code</span></span>
<span data-ttu-id="01a55-136">[Download](https://code.visualstudio.com/docs/setup/osx) en Visual Studio Code installeren.</span><span class="sxs-lookup"><span data-stu-id="01a55-136">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="01a55-137">Visual Studio Code is een eenvoudige maar krachtige broncode-editor voor Windows, Linux en Mac OS.</span><span class="sxs-lookup"><span data-stu-id="01a55-137">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="01a55-138">U gebruikt deze editor verderop in Hallo zelfstudie tooedit Hallo voorbeeldcode.</span><span class="sxs-lookup"><span data-stu-id="01a55-138">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="01a55-139">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="01a55-139">Summary</span></span>
<span data-ttu-id="01a55-140">U kunt Hallo vereist ontwikkelingsprogramma's en -software voor het eerste voorbeeldtoepassing hello hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="01a55-140">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="01a55-141">de volgende taak Hallo is toocreate, implementeren en uitvoeren van de voorbeeldtoepassing Hallo op Edison.</span><span class="sxs-lookup"><span data-stu-id="01a55-141">hello next task is toocreate, deploy, and run hello sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="01a55-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="01a55-142">Next steps</span></span>
<span data-ttu-id="01a55-143">[Hallo knipperen toepassing maken en implementeren][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="01a55-143">[Create and deploy hello blink application][create-and-deploy-the-blink-application]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-node-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-mac.md
