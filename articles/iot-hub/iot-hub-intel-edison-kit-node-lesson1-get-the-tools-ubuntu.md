---
title: 'Intel Edison (knooppunt) verbinden met Azure IoT - les 1: download hulpprogramma''s (Ubuntu) | Microsoft Docs'
description: Download en installeer de benodigde hulpprogramma's en -software voor de eerste voorbeeldtoepassing voor Edison op Ubuntu.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: arduino ontwikkelingsprogramma's, iot-ontwikkeling, iot-software, internet van dingen software, git op ubuntu, installatie knooppunt js ubuntu installeren
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 9ab5b161-7ec5-41a6-9c5f-4456e4882752
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 74c5f06c2b12d140814bfb75125d60b83addf70c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-ubuntu-1604"></a><span data-ttu-id="88bab-104">De hulpprogramma's downloaden (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="88bab-104">Get the tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="88bab-105">[Windows 7 of hoger][windows]</span><span class="sxs-lookup"><span data-stu-id="88bab-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="88bab-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="88bab-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="88bab-107">[Mac OS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="88bab-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="88bab-108">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="88bab-108">What you will do</span></span>
<span data-ttu-id="88bab-109">Download de ontwikkelprogramma's en de software voor de eerste voorbeeldtoepassing voor uw Edison Intel.</span><span class="sxs-lookup"><span data-stu-id="88bab-109">Download the development tools and the software for the first sample application for your Intel Edison.</span></span> <span data-ttu-id="88bab-110">Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="88bab-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="88bab-111">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="88bab-111">What you will learn</span></span>
<span data-ttu-id="88bab-112">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="88bab-112">In this article, you will learn:</span></span>

* <span data-ttu-id="88bab-113">Git en Node.js installeren</span><span class="sxs-lookup"><span data-stu-id="88bab-113">How to install Git and Node.js</span></span>
  * <span data-ttu-id="88bab-114">[GIT](https://git-scm.com) is een open-source gedistribueerd versiebeheersysteem.</span><span class="sxs-lookup"><span data-stu-id="88bab-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="88bab-115">De voorbeeldtoepassing voor dit artikel wordt opgeslagen op Git.</span><span class="sxs-lookup"><span data-stu-id="88bab-115">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="88bab-116">[Node.js](https://nodejs.org/en/) is een JavaScript-runtime met een uitgebreide pakket-ecosysteem.</span><span class="sxs-lookup"><span data-stu-id="88bab-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="88bab-117">Hoe extra Node.js ontwikkelingsprogramma's installeren met NPM.</span><span class="sxs-lookup"><span data-stu-id="88bab-117">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="88bab-118">De minimaal vereiste versie van Node.js is 4.5 TNS.</span><span class="sxs-lookup"><span data-stu-id="88bab-118">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="88bab-119">[NPM](https://www.npmjs.com) is een van de pakket-managers voor Node.js.</span><span class="sxs-lookup"><span data-stu-id="88bab-119">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="88bab-120">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="88bab-120">What you need</span></span>
<span data-ttu-id="88bab-121">Om deze bewerking niet voltooien, moet u het:</span><span class="sxs-lookup"><span data-stu-id="88bab-121">To complete this operation, you will need:</span></span>
* <span data-ttu-id="88bab-122">Een internetverbinding om de ontwikkelprogramma's en de software te downloaden.</span><span class="sxs-lookup"><span data-stu-id="88bab-122">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="88bab-123">Een computer die Ubuntu 16.04 of hoger wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="88bab-123">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-nodejs-and-npm"></a><span data-ttu-id="88bab-124">Installeer Git, Node.js en NPM</span><span class="sxs-lookup"><span data-stu-id="88bab-124">Install Git, Node.js, and NPM</span></span>
<span data-ttu-id="88bab-125">Gebruik de sneltoets `Ctrl + Alt + T` openen van een terminal en voer de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="88bab-125">Use the keyboard shortcut `Ctrl + Alt + T` to open a terminal and run the following commands:</span></span>

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="88bab-126">Extra hulpprogramma's voor Node.js-ontwikkeling</span><span class="sxs-lookup"><span data-stu-id="88bab-126">Install additional Node.js development tools</span></span>
<span data-ttu-id="88bab-127">Gebruik [gulp.js](http://gulpjs.com) voor de implementatie van de voorbeeldtoepassing om Edison te automatiseren.</span><span class="sxs-lookup"><span data-stu-id="88bab-127">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to Edison.</span></span>

<span data-ttu-id="88bab-128">Installeer `gulp` met de volgende opdracht in de terminal:</span><span class="sxs-lookup"><span data-stu-id="88bab-128">Install `gulp` by running the following command in the terminal:</span></span>

```bash
sudo npm install -g gulp
```

<span data-ttu-id="88bab-129">Als u problemen hebt met het installeren van Node.js en deze extra ontwikkelprogramma's op Ubuntu, Zie de [probleemoplossingsgids] [ troubleshooting] voor oplossingen voor bekende problemen.</span><span class="sxs-lookup"><span data-stu-id="88bab-129">If you experience issues installing Node.js and these additional development tools on Ubuntu, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="88bab-130">Visual Studio Code installeren</span><span class="sxs-lookup"><span data-stu-id="88bab-130">Install Visual Studio Code</span></span>
<span data-ttu-id="88bab-131">[Download](https://code.visualstudio.com/docs/setup/linux) en Visual Studio Code installeren.</span><span class="sxs-lookup"><span data-stu-id="88bab-131">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span> <span data-ttu-id="88bab-132">Visual Studio Code is een eenvoudige maar krachtige broncode-editor voor Windows, Linux en Mac OS.</span><span class="sxs-lookup"><span data-stu-id="88bab-132">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="88bab-133">U gebruikt deze editor verderop in de zelfstudie voor het bewerken van de voorbeeldcode.</span><span class="sxs-lookup"><span data-stu-id="88bab-133">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="88bab-134">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="88bab-134">Summary</span></span>
<span data-ttu-id="88bab-135">U kunt de vereiste ontwikkelingsprogramma's en software voor de eerste voorbeeldtoepassing hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="88bab-135">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="88bab-136">De volgende taak is het maken, implementeren en uitvoeren van de voorbeeldtoepassing op Edison.</span><span class="sxs-lookup"><span data-stu-id="88bab-136">The next task is to create, deploy, and run the sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="88bab-137">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="88bab-137">Next steps</span></span>
<span data-ttu-id="88bab-138">[Maken en implementeren van de voorbeeldtoepassing knipperen][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="88bab-138">[Create and deploy the blink sample application][create-and-deploy-the-blink-application]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-node-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-mac.md
