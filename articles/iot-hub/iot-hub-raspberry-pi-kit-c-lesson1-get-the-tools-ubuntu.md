---
title: 'Connect Raspberry PI (C) naar Azure IoT - les 1: download hulpprogramma''s (Ubuntu) | Microsoft Docs'
description: Download en installeer de benodigde hulpprogramma's en -software voor de eerste voorbeeldtoepassing voor Pi op Ubuntu.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: IOT-ontwikkeling, iot-software, internet van dingen software, installeer git op ubuntu, gulp uitvoeren, knooppunt js ubuntu installeren
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 32cfea00-c254-4cef-8f6f-bbf807eca6b6
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 28ebba82e90d91470518cd830c96e6da39d8b9b4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-ubuntu-1604"></a><span data-ttu-id="42d65-104">De hulpprogramma's downloaden (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="42d65-104">Get the tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="42d65-105">Windows 7 of hoger</span><span class="sxs-lookup"><span data-stu-id="42d65-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="42d65-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="42d65-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="42d65-107">Mac OS 10.10</span><span class="sxs-lookup"><span data-stu-id="42d65-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="42d65-108">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="42d65-108">What you will do</span></span>
<span data-ttu-id="42d65-109">Download de ontwikkelprogramma's en de software voor de eerste voorbeeldtoepassing voor uw frambozen Pi 3.</span><span class="sxs-lookup"><span data-stu-id="42d65-109">Download the development tools and the software for the first sample application for your Raspberry Pi 3.</span></span> <span data-ttu-id="42d65-110">Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="42d65-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

> [!NOTE]
> <span data-ttu-id="42d65-111">Hoewel de programmeertaal van de belangrijkste logica C, worden in welke opgedane Node.js-hulpprogramma's gebruikt voor apparaten detecteren en te bouwen en voorbeeldtoepassingen implementeren.</span><span class="sxs-lookup"><span data-stu-id="42d65-111">Although the programming language of the main logic is C, Node.js tools are used in the lessons to discover devices, and build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="42d65-112">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="42d65-112">What you will learn</span></span>
<span data-ttu-id="42d65-113">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="42d65-113">In this article, you will learn:</span></span>

* <span data-ttu-id="42d65-114">Git en Node.js installeren</span><span class="sxs-lookup"><span data-stu-id="42d65-114">How to install Git and Node.js</span></span>
  * <span data-ttu-id="42d65-115">[GIT](https://git-scm.com) is een open-source gedistribueerd versiebeheersysteem.</span><span class="sxs-lookup"><span data-stu-id="42d65-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="42d65-116">De voorbeeldtoepassing voor dit artikel wordt opgeslagen op Git.</span><span class="sxs-lookup"><span data-stu-id="42d65-116">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="42d65-117">[Node.js](https://nodejs.org/en/) is een JavaScript-runtime met een uitgebreide pakket-ecosysteem.</span><span class="sxs-lookup"><span data-stu-id="42d65-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="42d65-118">Hoe extra Node.js ontwikkelingsprogramma's installeren met NPM.</span><span class="sxs-lookup"><span data-stu-id="42d65-118">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="42d65-119">De minimaal vereiste versie van Node.js is 4.5 TNS.</span><span class="sxs-lookup"><span data-stu-id="42d65-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="42d65-120">[NPM](https://www.npmjs.com) is een van de pakket-managers voor Node.js.</span><span class="sxs-lookup"><span data-stu-id="42d65-120">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="42d65-121">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="42d65-121">What you need</span></span>
<span data-ttu-id="42d65-122">Om deze bewerking niet voltooien, moet u het:</span><span class="sxs-lookup"><span data-stu-id="42d65-122">To complete this operation, you will need:</span></span>

* <span data-ttu-id="42d65-123">Een internetverbinding om de ontwikkelprogramma's en de software te downloaden.</span><span class="sxs-lookup"><span data-stu-id="42d65-123">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="42d65-124">Een computer die Ubuntu 16.04 of hoger wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="42d65-124">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-nodejs-and-npm"></a><span data-ttu-id="42d65-125">Installeer Git, Node.js en NPM</span><span class="sxs-lookup"><span data-stu-id="42d65-125">Install Git, Node.js, and NPM</span></span>
<span data-ttu-id="42d65-126">Gebruik de sneltoets `Ctrl + Alt + T` openen van een terminal en voer de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="42d65-126">Use the keyboard shortcut `Ctrl + Alt + T` to open a terminal and run the following commands:</span></span>

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="42d65-127">Extra hulpprogramma's voor Node.js-ontwikkeling</span><span class="sxs-lookup"><span data-stu-id="42d65-127">Install additional Node.js development tools</span></span>
<span data-ttu-id="42d65-128">Gebruik [gulp.js](http://gulpjs.com) voor het automatiseren van de implementatie van de voorbeeldtoepassing tot Pi.</span><span class="sxs-lookup"><span data-stu-id="42d65-128">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to Pi.</span></span> <span data-ttu-id="42d65-129">Gebruik de [apparaat detectie cli](https://github.com/Azure/device-discovery-cli) netwerkinformatie ophalen over uw IoT-apparaten.</span><span class="sxs-lookup"><span data-stu-id="42d65-129">Use the [device-discovery-cli](https://github.com/Azure/device-discovery-cli) to retrieve network information about your IoT devices.</span></span>

<span data-ttu-id="42d65-130">Installeer `gulp` en `device-discovery-cli` met de volgende opdracht in de terminal:</span><span class="sxs-lookup"><span data-stu-id="42d65-130">Install `gulp` and `device-discovery-cli` by running the following command in the terminal:</span></span>

```bash
sudo npm install -g device-discovery-cli gulp
```

<span data-ttu-id="42d65-131">Als u problemen hebt met het installeren van Node.js en deze extra ontwikkelprogramma's op Ubuntu, Zie de [probleemoplossingsgids](iot-hub-raspberry-pi-kit-c-troubleshooting.md) voor oplossingen voor bekende problemen.</span><span class="sxs-lookup"><span data-stu-id="42d65-131">If you experience issues installing Node.js and these additional development tools on Ubuntu, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="42d65-132">Visual Studio Code installeren</span><span class="sxs-lookup"><span data-stu-id="42d65-132">Install Visual Studio Code</span></span>
<span data-ttu-id="42d65-133">[Download](https://code.visualstudio.com/docs/setup/linux) en Visual Studio Code installeren.</span><span class="sxs-lookup"><span data-stu-id="42d65-133">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span> <span data-ttu-id="42d65-134">Visual Studio Code is een eenvoudige maar krachtige broncode-editor voor Windows, Linux en Mac OS.</span><span class="sxs-lookup"><span data-stu-id="42d65-134">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="42d65-135">U gebruikt deze editor verderop in de zelfstudie voor het bewerken van de voorbeeldcode.</span><span class="sxs-lookup"><span data-stu-id="42d65-135">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="42d65-136">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="42d65-136">Summary</span></span>
<span data-ttu-id="42d65-137">U kunt de vereiste ontwikkelingsprogramma's en software voor de eerste voorbeeldtoepassing hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="42d65-137">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="42d65-138">De volgende taak is het maken, implementeren en uitvoeren van de voorbeeldtoepassing op Pi.</span><span class="sxs-lookup"><span data-stu-id="42d65-138">The next task is to create, deploy, and run the sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="42d65-139">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="42d65-139">Next steps</span></span>
[<span data-ttu-id="42d65-140">De Blink-toepassing maken en implementeren</span><span class="sxs-lookup"><span data-stu-id="42d65-140">Create and deploy the blink application</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)

