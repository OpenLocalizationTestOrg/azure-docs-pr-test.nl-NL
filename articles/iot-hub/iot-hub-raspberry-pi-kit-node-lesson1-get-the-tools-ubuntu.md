---
title: 'Frambozen Pi (knooppunt) verbinden met Azure IoT - les 1: download hulpprogramma''s (Ubuntu) | Microsoft Docs'
description: Download en installeer de benodigde hulpprogramma's en -software voor de eerste voorbeeldtoepassing voor Pi op Ubuntu.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: IOT-ontwikkeling, iot-software, internet van dingen software, installeer git op ubuntu, gulp uitvoeren, knooppunt js ubuntu installeren
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 4d5e45c0-1db9-4662-a039-99ba26333085
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: de583be0cdce058c83091f421376812e8013d76e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-ubuntu-1604"></a><span data-ttu-id="f689d-104">De hulpprogramma's downloaden (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="f689d-104">Get the tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f689d-105">Windows 7 of hoger</span><span class="sxs-lookup"><span data-stu-id="f689d-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="f689d-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="f689d-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="f689d-107">Mac OS 10.10</span><span class="sxs-lookup"><span data-stu-id="f689d-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-mac.md)


## <a name="what-you-will-do"></a><span data-ttu-id="f689d-108">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="f689d-108">What you will do</span></span>
<span data-ttu-id="f689d-109">Download de ontwikkelprogramma's en de software voor de eerste voorbeeldtoepassing voor frambozen Pi 3.</span><span class="sxs-lookup"><span data-stu-id="f689d-109">Download the development tools and the software for the first sample application for Raspberry Pi 3.</span></span> <span data-ttu-id="f689d-110">Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="f689d-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="f689d-111">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="f689d-111">What you will learn</span></span>
<span data-ttu-id="f689d-112">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="f689d-112">In this article, you will learn:</span></span>

* <span data-ttu-id="f689d-113">Klik hier voor meer informatie over het installeren van Git en Node.js.</span><span class="sxs-lookup"><span data-stu-id="f689d-113">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="f689d-114">[GIT](https://git-scm.com) is een open-source gedistribueerd versiebeheersysteem.</span><span class="sxs-lookup"><span data-stu-id="f689d-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="f689d-115">De voorbeeldtoepassing voor dit artikel wordt opgeslagen op Git.</span><span class="sxs-lookup"><span data-stu-id="f689d-115">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="f689d-116">[Node.js](https://nodejs.org/en/) is een JavaScript-runtime met een uitgebreide pakket-ecosysteem.</span><span class="sxs-lookup"><span data-stu-id="f689d-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="f689d-117">Hoe extra Node.js ontwikkelingsprogramma's installeren met NPM.</span><span class="sxs-lookup"><span data-stu-id="f689d-117">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="f689d-118">De minimaal vereiste versie van Node.js is 4.5 TNS.</span><span class="sxs-lookup"><span data-stu-id="f689d-118">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="f689d-119">[NPM](https://www.npmjs.com) is een van de pakket-managers voor Node.js.</span><span class="sxs-lookup"><span data-stu-id="f689d-119">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="f689d-120">Wat moet u</span><span class="sxs-lookup"><span data-stu-id="f689d-120">What do you need</span></span>
<span data-ttu-id="f689d-121">Om deze bewerking niet voltooien, moet u het:</span><span class="sxs-lookup"><span data-stu-id="f689d-121">To complete this operation, you will need:</span></span>

* <span data-ttu-id="f689d-122">Een internetverbinding om de ontwikkelprogramma's en de software te downloaden.</span><span class="sxs-lookup"><span data-stu-id="f689d-122">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="f689d-123">Een computer die Ubuntu 16.04 of hoger wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f689d-123">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-nodejs-and-npm"></a><span data-ttu-id="f689d-124">Installeer Git, Node.js en NPM</span><span class="sxs-lookup"><span data-stu-id="f689d-124">Install Git, Node.js, and NPM</span></span>
<span data-ttu-id="f689d-125">Gebruik de sneltoets `Ctrl + Alt + T` openen van een terminal en voer de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="f689d-125">Use the keyboard shortcut `Ctrl + Alt + T` to open a terminal and run the following commands:</span></span>

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="f689d-126">Extra hulpprogramma's voor Node.js-ontwikkeling</span><span class="sxs-lookup"><span data-stu-id="f689d-126">Install additional Node.js development tools</span></span>
<span data-ttu-id="f689d-127">U gebruikt [gulp.js](http://gulpjs.com) voor het automatiseren van de implementatie van de voorbeeldtoepassing tot Pi.</span><span class="sxs-lookup"><span data-stu-id="f689d-127">You use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to Pi.</span></span> <span data-ttu-id="f689d-128">Ook gebruiken de [apparaat detectie cli](https://github.com/Azure/device-discovery-cli) netwerkinformatie ophalen over uw IoT-apparaten.</span><span class="sxs-lookup"><span data-stu-id="f689d-128">You also use the [device-discovery-cli](https://github.com/Azure/device-discovery-cli) to retrieve network information about your IoT devices.</span></span>

<span data-ttu-id="f689d-129">Installeer `gulp` en `device-discovery-cli` met de volgende opdracht in de terminal:</span><span class="sxs-lookup"><span data-stu-id="f689d-129">Install `gulp` and `device-discovery-cli` by running the following command in the terminal:</span></span>

```bash
sudo npm install -g device-discovery-cli gulp
```

<span data-ttu-id="f689d-130">Als u problemen hebt met het installeren van Node.js en deze extra ontwikkelprogramma's op Ubuntu, Zie de [probleemoplossingsgids](iot-hub-raspberry-pi-kit-node-troubleshooting.md) voor oplossingen voor bekende problemen.</span><span class="sxs-lookup"><span data-stu-id="f689d-130">If you experience issues installing Node.js and these additional development tools on Ubuntu, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-node-troubleshooting.md) for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="f689d-131">Visual Studio Code installeren</span><span class="sxs-lookup"><span data-stu-id="f689d-131">Install Visual Studio Code</span></span>
<span data-ttu-id="f689d-132">[Download](https://code.visualstudio.com/docs/setup/linux) en Visual Studio Code installeren.</span><span class="sxs-lookup"><span data-stu-id="f689d-132">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span> <span data-ttu-id="f689d-133">Visual Studio Code is een eenvoudige maar krachtige broncode-editor voor Windows, Linux en Mac OS.</span><span class="sxs-lookup"><span data-stu-id="f689d-133">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="f689d-134">U gebruikt deze editor verderop in de zelfstudie voor het bewerken van de voorbeeldcode.</span><span class="sxs-lookup"><span data-stu-id="f689d-134">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="f689d-135">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="f689d-135">Summary</span></span>
<span data-ttu-id="f689d-136">U kunt de vereiste ontwikkelingsprogramma's en software voor de eerste voorbeeldtoepassing hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="f689d-136">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="f689d-137">De volgende taak is het maken, implementeren en uitvoeren van de voorbeeldtoepassing op Pi.</span><span class="sxs-lookup"><span data-stu-id="f689d-137">The next task is to create, deploy, and run the sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f689d-138">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f689d-138">Next steps</span></span>
[<span data-ttu-id="f689d-139">Maken en implementeren van de voorbeeldtoepassing knipperen</span><span class="sxs-lookup"><span data-stu-id="f689d-139">Create and deploy the blink sample application</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-deploy-blink-app.md)

