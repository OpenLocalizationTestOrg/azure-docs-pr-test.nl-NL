---
title: 'Connect Raspberry PI (C) naar Azure IoT - les 1: download hulpprogramma''s (Windows) | Microsoft Docs'
description: Download en installeer de benodigde hulpprogramma's en -software voor de eerste voorbeeldtoepassing voor Pi op Windows 7 en hoger.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: IOT-ontwikkeling, iot-software, internet van dingen software, installeer git voor windows, knooppunt js windows installeren, npm installeren op windows
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: bd765ddd-65b7-4241-a391-dc77cb3af1c0
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 0e58975f4411f97223b2c4374bdd746fe6628c42
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-windows-7-or-later"></a><span data-ttu-id="1e70e-104">Download de hulpprogramma's (Windows 7 of hoger)</span><span class="sxs-lookup"><span data-stu-id="1e70e-104">Get the tools (Windows 7 or later)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="1e70e-105">Windows 7 of hoger</span><span class="sxs-lookup"><span data-stu-id="1e70e-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="1e70e-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="1e70e-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="1e70e-107">Mac OS 10.10</span><span class="sxs-lookup"><span data-stu-id="1e70e-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="1e70e-108">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="1e70e-108">What you will do</span></span>
<span data-ttu-id="1e70e-109">Download de ontwikkelprogramma's en de software voor de eerste voorbeeldtoepassing voor frambozen Pi 3.</span><span class="sxs-lookup"><span data-stu-id="1e70e-109">Download the development tools and the software for the first sample application for Raspberry Pi 3.</span></span> <span data-ttu-id="1e70e-110">Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="1e70e-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

> [!NOTE]
> <span data-ttu-id="1e70e-111">Hoewel de programmeertaal van de belangrijkste logica C, worden in welke opgedane Node.js-hulpprogramma's gebruikt voor apparaten detecteren en te bouwen en voorbeeldtoepassingen implementeren.</span><span class="sxs-lookup"><span data-stu-id="1e70e-111">Although the programming language of the main logic is C, Node.js tools are used in the lessons to discover devices, and build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="1e70e-112">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="1e70e-112">What you will learn</span></span>
<span data-ttu-id="1e70e-113">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="1e70e-113">In this article, you will learn:</span></span>

* <span data-ttu-id="1e70e-114">Klik hier voor meer informatie over het installeren van Git en Node.js.</span><span class="sxs-lookup"><span data-stu-id="1e70e-114">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="1e70e-115">[GIT](https://git-scm.com) is een open-source gedistribueerd versiebeheersysteem.</span><span class="sxs-lookup"><span data-stu-id="1e70e-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="1e70e-116">De voorbeeldtoepassing voor dit artikel wordt opgeslagen op Git.</span><span class="sxs-lookup"><span data-stu-id="1e70e-116">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="1e70e-117">[Node.js](https://nodejs.org/en/) is een JavaScript-runtime met een uitgebreide pakket-ecosysteem.</span><span class="sxs-lookup"><span data-stu-id="1e70e-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="1e70e-118">Hoe extra Node.js ontwikkelingsprogramma's installeren met NPM.</span><span class="sxs-lookup"><span data-stu-id="1e70e-118">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="1e70e-119">De minimum versievereisten voor Node.js is 4.5 TNS.</span><span class="sxs-lookup"><span data-stu-id="1e70e-119">The minimum version requirement of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="1e70e-120">[NPM](https://www.npmjs.com) is een van de pakket-managers voor Node.js.</span><span class="sxs-lookup"><span data-stu-id="1e70e-120">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="1e70e-121">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="1e70e-121">What you need</span></span>

<span data-ttu-id="1e70e-122">Om deze bewerking niet voltooien, moet u het:</span><span class="sxs-lookup"><span data-stu-id="1e70e-122">To complete this operation, you will need:</span></span>

* <span data-ttu-id="1e70e-123">Een internetverbinding om de ontwikkelprogramma's en de software te downloaden.</span><span class="sxs-lookup"><span data-stu-id="1e70e-123">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="1e70e-124">Een computer waarop Windows wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1e70e-124">A computer that is running Windows.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="1e70e-125">Installeer Git en Node.js</span><span class="sxs-lookup"><span data-stu-id="1e70e-125">Install Git and Node.js</span></span>

<span data-ttu-id="1e70e-126">Klik op de onderstaande koppelingen wilt downloaden en installeren van Git en Node.js LTS voor Windows.</span><span class="sxs-lookup"><span data-stu-id="1e70e-126">Click the links below to download and install Git and Node.js LTS for Windows.</span></span>

* [<span data-ttu-id="1e70e-127">Ophalen van Git voor Windows</span><span class="sxs-lookup"><span data-stu-id="1e70e-127">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
* [<span data-ttu-id="1e70e-128">Node.js TNS ophalen voor Windows</span><span class="sxs-lookup"><span data-stu-id="1e70e-128">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="1e70e-129">Extra hulpprogramma's voor Node.js-ontwikkeling</span><span class="sxs-lookup"><span data-stu-id="1e70e-129">Install additional Node.js development tools</span></span>

<span data-ttu-id="1e70e-130">Gebruik [gulp.js](http://gulpjs.com) voor het automatiseren van de implementatie van de voorbeeldtoepassing tot Pi.</span><span class="sxs-lookup"><span data-stu-id="1e70e-130">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to Pi.</span></span> <span data-ttu-id="1e70e-131">Gebruik de [apparaat detectie cli](https://github.com/Azure/device-discovery-cli) netwerkinformatie ophalen over uw IoT-apparaten.</span><span class="sxs-lookup"><span data-stu-id="1e70e-131">Use the [device-discovery-cli](https://github.com/Azure/device-discovery-cli) to retrieve network information about your IoT devices.</span></span>

<span data-ttu-id="1e70e-132">Start een opdrachtprompt als beheerder.</span><span class="sxs-lookup"><span data-stu-id="1e70e-132">Start a command prompt as an administrator.</span></span> <span data-ttu-id="1e70e-133">Installeer `gulp` en `device-discovery-cli` met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="1e70e-133">Install `gulp` and `device-discovery-cli` by running the following command:</span></span>

```bash
npm install -g device-discovery-cli gulp
```

<span data-ttu-id="1e70e-134">Als u problemen hebt met het installeren van Node.js en deze extra Node.js ontwikkelprogramma's op uw computer, Zie de [probleemoplossingsgids](iot-hub-raspberry-pi-kit-c-troubleshooting.md) voor oplossingen voor bekende problemen.</span><span class="sxs-lookup"><span data-stu-id="1e70e-134">If you experience issues installing Node.js and these additional Node.js development tools on your computer, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="1e70e-135">Visual Studio Code installeren</span><span class="sxs-lookup"><span data-stu-id="1e70e-135">Install Visual Studio Code</span></span>

<span data-ttu-id="1e70e-136">[Download](https://code.visualstudio.com/docs/setup/windows) en Visual Studio Code installeren.</span><span class="sxs-lookup"><span data-stu-id="1e70e-136">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span> <span data-ttu-id="1e70e-137">Visual Studio Code is een eenvoudige maar krachtige broncode-editor voor Windows, Linux en Mac OS.</span><span class="sxs-lookup"><span data-stu-id="1e70e-137">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="1e70e-138">U gebruikt deze editor verderop in de zelfstudie voor het bewerken van de voorbeeldcode.</span><span class="sxs-lookup"><span data-stu-id="1e70e-138">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="1e70e-139">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="1e70e-139">Summary</span></span>

<span data-ttu-id="1e70e-140">U kunt de vereiste ontwikkelingsprogramma's en software voor de eerste voorbeeldtoepassing hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="1e70e-140">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="1e70e-141">De volgende taak is het maken, implementeren en uitvoeren van de voorbeeldtoepassing op Pi.</span><span class="sxs-lookup"><span data-stu-id="1e70e-141">The next task is to create, deploy, and run the sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e70e-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1e70e-142">Next steps</span></span>

[<span data-ttu-id="1e70e-143">De Blink-toepassing maken en implementeren</span><span class="sxs-lookup"><span data-stu-id="1e70e-143">Create and deploy the blink application</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)
