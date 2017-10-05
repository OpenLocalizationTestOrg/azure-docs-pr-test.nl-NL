---
title: 'Intel Edison (knooppunt) verbinden met Azure IoT - les 1: download hulpprogramma''s (Mac OS) | Microsoft Docs'
description: Download en installeer de benodigde hulpprogramma's en -software voor de eerste voorbeeldtoepassing voor Edison op Mac OS.
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
ms.openlocfilehash: a5e406f49379e9f2192ee93334ab1dcf9f3e53d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-macos-1010"></a><span data-ttu-id="3d2e8-104">De hulpprogramma's downloaden (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="3d2e8-104">Get the tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="3d2e8-105">[Windows 7 of hoger][windows]</span><span class="sxs-lookup"><span data-stu-id="3d2e8-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="3d2e8-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="3d2e8-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="3d2e8-107">[Mac OS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="3d2e8-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="3d2e8-108">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="3d2e8-108">What you will do</span></span>
<span data-ttu-id="3d2e8-109">Download de ontwikkelprogramma's en de software voor de eerste voorbeeldtoepassing voor uw Edison Intel.</span><span class="sxs-lookup"><span data-stu-id="3d2e8-109">Download the development tools and the software for the first sample application for your Intel Edison.</span></span> <span data-ttu-id="3d2e8-110">Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="3d2e8-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="3d2e8-111">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="3d2e8-111">What you will learn</span></span>
<span data-ttu-id="3d2e8-112">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="3d2e8-112">In this article, you will learn:</span></span>

* <span data-ttu-id="3d2e8-113">Klik hier voor meer informatie over het installeren van Git en Node.js.</span><span class="sxs-lookup"><span data-stu-id="3d2e8-113">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="3d2e8-114">[GIT](https://git-scm.com) is een open-source gedistribueerd versiebeheersysteem.</span><span class="sxs-lookup"><span data-stu-id="3d2e8-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="3d2e8-115">De voorbeeldtoepassing voor dit artikel wordt opgeslagen op Git.</span><span class="sxs-lookup"><span data-stu-id="3d2e8-115">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="3d2e8-116">[Node.js](https://nodejs.org/en/) is een JavaScript-runtime met een uitgebreide pakket-ecosysteem.</span><span class="sxs-lookup"><span data-stu-id="3d2e8-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="3d2e8-117">Hoe extra Node.js ontwikkelingsprogramma's installeren met NPM.</span><span class="sxs-lookup"><span data-stu-id="3d2e8-117">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="3d2e8-118">De minimaal vereiste versie van Node.js is 4.5 TNS.</span><span class="sxs-lookup"><span data-stu-id="3d2e8-118">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="3d2e8-119">[NPM](https://www.npmjs.com) is een van de pakket-managers voor Node.js.</span><span class="sxs-lookup"><span data-stu-id="3d2e8-119">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="3d2e8-120">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="3d2e8-120">What you need</span></span>
<span data-ttu-id="3d2e8-121">Om deze bewerking niet voltooien, moet u het:</span><span class="sxs-lookup"><span data-stu-id="3d2e8-121">To complete this operation, you will need:</span></span>
* <span data-ttu-id="3d2e8-122">Een internetverbinding om de ontwikkelprogramma's en de software te downloaden.</span><span class="sxs-lookup"><span data-stu-id="3d2e8-122">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="3d2e8-123">Een Mac met Mac OS Yosemite (10.10) of hoger.</span><span class="sxs-lookup"><span data-stu-id="3d2e8-123">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="3d2e8-124">Installeer Git en Node.js</span><span class="sxs-lookup"><span data-stu-id="3d2e8-124">Install Git and Node.js</span></span>
<span data-ttu-id="3d2e8-125">U installeert Git en Node.js via de [Homebrew](http://brew.sh) het hulpprogramma voor het pakket met de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="3d2e8-125">To install Git and Node.js, use the [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="3d2e8-126">Homebrew installeren.</span><span class="sxs-lookup"><span data-stu-id="3d2e8-126">Install Homebrew.</span></span> <span data-ttu-id="3d2e8-127">Als u Homebrew al hebt geïnstalleerd, gaat u naar stap 2.</span><span class="sxs-lookup"><span data-stu-id="3d2e8-127">If you've already installed Homebrew, go to step 2.</span></span>

   1. <span data-ttu-id="3d2e8-128">Druk op `Cmd + Space` en voer `Terminal` een terminal openen.</span><span class="sxs-lookup"><span data-stu-id="3d2e8-128">Press `Cmd + Space` and enter `Terminal` to open a terminal.</span></span>
   2. <span data-ttu-id="3d2e8-129">Voer de volgende opdracht uit:</span><span class="sxs-lookup"><span data-stu-id="3d2e8-129">Run the following command:</span></span>

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="3d2e8-130">Git en Node.js installeren met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="3d2e8-130">Install Git and Node.js by running the following command:</span></span>

   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="3d2e8-131">Extra hulpprogramma's voor Node.js-ontwikkeling</span><span class="sxs-lookup"><span data-stu-id="3d2e8-131">Install additional Node.js development tools</span></span>
<span data-ttu-id="3d2e8-132">Gebruik [gulp.js](http://gulpjs.com) voor de implementatie van de voorbeeldtoepassing op uw Edison automatiseren.</span><span class="sxs-lookup"><span data-stu-id="3d2e8-132">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to your Edison.</span></span>

<span data-ttu-id="3d2e8-133">Installeer `gulp` met de volgende opdracht in de terminal:</span><span class="sxs-lookup"><span data-stu-id="3d2e8-133">Install `gulp` by running the following command in the terminal:</span></span>

```bash
sudo npm install -g gulp
```

<span data-ttu-id="3d2e8-134">Als u problemen hebt met het Node.js en deze extra ontwikkelprogramma's installeert op Mac OS, Zie de [probleemoplossingsgids] [ troubleshooting] voor oplossingen voor bekende problemen.</span><span class="sxs-lookup"><span data-stu-id="3d2e8-134">If you experience issues installing Node.js and these additional development tools on macOS, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="3d2e8-135">Visual Studio Code installeren</span><span class="sxs-lookup"><span data-stu-id="3d2e8-135">Install Visual Studio Code</span></span>
<span data-ttu-id="3d2e8-136">[Download](https://code.visualstudio.com/docs/setup/osx) en Visual Studio Code installeren.</span><span class="sxs-lookup"><span data-stu-id="3d2e8-136">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="3d2e8-137">Visual Studio Code is een eenvoudige maar krachtige broncode-editor voor Windows, Linux en Mac OS.</span><span class="sxs-lookup"><span data-stu-id="3d2e8-137">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="3d2e8-138">U gebruikt deze editor verderop in de zelfstudie voor het bewerken van de voorbeeldcode.</span><span class="sxs-lookup"><span data-stu-id="3d2e8-138">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="3d2e8-139">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="3d2e8-139">Summary</span></span>
<span data-ttu-id="3d2e8-140">U kunt de vereiste ontwikkelingsprogramma's en software voor de eerste voorbeeldtoepassing hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="3d2e8-140">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="3d2e8-141">De volgende taak is het maken, implementeren en uitvoeren van de voorbeeldtoepassing op Edison.</span><span class="sxs-lookup"><span data-stu-id="3d2e8-141">The next task is to create, deploy, and run the sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d2e8-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3d2e8-142">Next steps</span></span>
<span data-ttu-id="3d2e8-143">[De toepassing knipperen maken en implementeren][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="3d2e8-143">[Create and deploy the blink application][create-and-deploy-the-blink-application]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-node-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-mac.md
