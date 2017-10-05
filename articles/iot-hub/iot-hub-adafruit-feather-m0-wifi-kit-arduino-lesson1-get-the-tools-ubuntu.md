---
title: 'Arduino verbinden met Azure IoT - les 1: download hulpprogramma''s (Ubuntu) | Microsoft Docs'
description: Download en installeer de benodigde hulpprogramma's en -software voor de eerste voorbeeldtoepassing voor Adafruit Doezelaar M0 Wi-Fi op Ubuntu.
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
ms.openlocfilehash: 90b1c12659c33517142e2048d8f5f629f6d6b4c9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-ubuntu-1604"></a><span data-ttu-id="cc816-104">De hulpprogramma's downloaden (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="cc816-104">Get the tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="cc816-105">[Windows 7 of hoger][windows]</span><span class="sxs-lookup"><span data-stu-id="cc816-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="cc816-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="cc816-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="cc816-107">[Mac OS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="cc816-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="cc816-108">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="cc816-108">What you will do</span></span>

<span data-ttu-id="cc816-109">Download de ontwikkelprogramma's en de software voor de eerste voorbeeldtoepassing voor uw kaart Adafruit Doezelaar M0 Wi-Fi Arduino.</span><span class="sxs-lookup"><span data-stu-id="cc816-109">Download the development tools and the software for the first sample application for your Adafruit Feather M0 WiFi Arduino board.</span></span> 

<span data-ttu-id="cc816-110">Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="cc816-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

> [!NOTE]
> <span data-ttu-id="cc816-111">Hoewel de programmeertaal van de belangrijkste logica Arduino, worden in de uitkomsten Node.js-hulpprogramma's om te bouwen en implementeren van de voorbeeldtoepassingen gebruikt.</span><span class="sxs-lookup"><span data-stu-id="cc816-111">Although the programming language of the main logic is Arduino, Node.js tools are used in the lessons to build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="cc816-112">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="cc816-112">What you will learn</span></span>
<span data-ttu-id="cc816-113">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="cc816-113">In this article, you will learn:</span></span>

* <span data-ttu-id="cc816-114">Git en Node.js installeren</span><span class="sxs-lookup"><span data-stu-id="cc816-114">How to install Git and Node.js</span></span>
  * <span data-ttu-id="cc816-115">[GIT](https://git-scm.com) is een open-source gedistribueerd versiebeheersysteem.</span><span class="sxs-lookup"><span data-stu-id="cc816-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="cc816-116">De voorbeeldtoepassing voor dit artikel wordt opgeslagen op Git.</span><span class="sxs-lookup"><span data-stu-id="cc816-116">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="cc816-117">[Node.js](https://nodejs.org/en/) is een JavaScript-runtime met een uitgebreide pakket-ecosysteem.</span><span class="sxs-lookup"><span data-stu-id="cc816-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="cc816-118">Hoe extra Node.js ontwikkelingsprogramma's installeren met NPM.</span><span class="sxs-lookup"><span data-stu-id="cc816-118">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="cc816-119">De minimaal vereiste versie van Node.js is 4.5 TNS.</span><span class="sxs-lookup"><span data-stu-id="cc816-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="cc816-120">[NPM](https://www.npmjs.com) is een van de pakket-managers voor Node.js.</span><span class="sxs-lookup"><span data-stu-id="cc816-120">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="cc816-121">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="cc816-121">What you need</span></span>
<span data-ttu-id="cc816-122">Om deze bewerking niet voltooien, moet u het:</span><span class="sxs-lookup"><span data-stu-id="cc816-122">To complete this operation, you will need:</span></span>
* <span data-ttu-id="cc816-123">Een internetverbinding om de ontwikkelprogramma's en de software te downloaden.</span><span class="sxs-lookup"><span data-stu-id="cc816-123">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="cc816-124">Een computer die Ubuntu 16.04 of hoger wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="cc816-124">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-nodejs-and-npm"></a><span data-ttu-id="cc816-125">Installeer Git, Node.js en NPM</span><span class="sxs-lookup"><span data-stu-id="cc816-125">Install Git, Node.js, and NPM</span></span>
<span data-ttu-id="cc816-126">Gebruik de sneltoets `Ctrl + Alt + T` openen van een terminal en voer de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="cc816-126">Use the keyboard shortcut `Ctrl + Alt + T` to open a terminal and run the following commands:</span></span>

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="cc816-127">Extra hulpprogramma's voor Node.js-ontwikkeling</span><span class="sxs-lookup"><span data-stu-id="cc816-127">Install additional Node.js development tools</span></span>
<span data-ttu-id="cc816-128">Gebruik [gulp.js](http://gulpjs.com) voor de implementatie van de voorbeeldtoepassing op het mededelingenbord Arduino automatiseren.</span><span class="sxs-lookup"><span data-stu-id="cc816-128">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to your Arduino board.</span></span>

<span data-ttu-id="cc816-129">Installeer `gulp`, `device-discovery-cli` met de volgende opdracht in de terminal:</span><span class="sxs-lookup"><span data-stu-id="cc816-129">Install `gulp`, `device-discovery-cli` by running the following command in the terminal:</span></span>

```bash
sudo npm install -g gulp device-discovery-cli
```

<span data-ttu-id="cc816-130">Als u problemen hebt met het installeren van Node.js en deze extra ontwikkelprogramma's op Ubuntu, Zie de [probleemoplossingsgids] [ troubleshooting] voor oplossingen voor bekende problemen.</span><span class="sxs-lookup"><span data-stu-id="cc816-130">If you experience issues installing Node.js and these additional development tools on Ubuntu, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="cc816-131">Visual Studio Code installeren</span><span class="sxs-lookup"><span data-stu-id="cc816-131">Install Visual Studio Code</span></span>
<span data-ttu-id="cc816-132">[Download](https://code.visualstudio.com/docs/setup/linux) en Visual Studio Code installeren.</span><span class="sxs-lookup"><span data-stu-id="cc816-132">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span> <span data-ttu-id="cc816-133">Visual Studio Code is een eenvoudige maar krachtige broncode-editor voor Windows, Linux en Mac OS.</span><span class="sxs-lookup"><span data-stu-id="cc816-133">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="cc816-134">U gebruikt deze editor verderop in de zelfstudie voor het bewerken van de voorbeeldcode.</span><span class="sxs-lookup"><span data-stu-id="cc816-134">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="cc816-135">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="cc816-135">Summary</span></span>
<span data-ttu-id="cc816-136">U kunt de vereiste ontwikkelingsprogramma's en software voor de eerste voorbeeldtoepassing hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="cc816-136">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="cc816-137">De volgende taak is het maken, implementeren en uitvoeren van de voorbeeldtoepassing op het mededelingenbord Arduino.</span><span class="sxs-lookup"><span data-stu-id="cc816-137">The next task is to create, deploy, and run the sample application on your Arduino board.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc816-138">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cc816-138">Next steps</span></span>
<span data-ttu-id="cc816-139">[Maken en implementeren van de voorbeeldtoepassing knipperen][create-and-deploy-the-blink-sample-application]</span><span class="sxs-lookup"><span data-stu-id="cc816-139">[Create and deploy the blink sample application][create-and-deploy-the-blink-sample-application]</span></span>

<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-mac.md
[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[create-and-deploy-the-blink-sample-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md