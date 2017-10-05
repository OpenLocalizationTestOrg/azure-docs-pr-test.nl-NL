---
title: 'Connect Intel Edison (C) naar Azure IoT - les 1: download hulpprogramma''s (Windows) | Microsoft Docs'
description: Download en installeer de benodigde hulpprogramma's en -software voor de eerste voorbeeldtoepassing voor Edison op Windows 7 en hoger.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: arduino ontwikkelingsprogramma's, iot-ontwikkeling, iot-software, internet van dingen software, installeer git voor windows, windows voor knooppunt js installeren
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 7d29a358-544d-4657-a504-5ed9b79c2925
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: f9d614d17f262b81a75d6128cbc5898dc18ab906
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-windows-7-or-later"></a><span data-ttu-id="a2463-104">Download de hulpprogramma's (Windows 7 of hoger)</span><span class="sxs-lookup"><span data-stu-id="a2463-104">Get the tools (Windows 7 or later)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="a2463-105">[Windows 7 of hoger][windows]</span><span class="sxs-lookup"><span data-stu-id="a2463-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="a2463-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="a2463-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="a2463-107">[Mac OS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="a2463-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="a2463-108">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="a2463-108">What you will do</span></span>
<span data-ttu-id="a2463-109">Download de ontwikkelprogramma's en de software voor de eerste voorbeeldtoepassing voor Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="a2463-109">Download the development tools and the software for the first sample application for Intel Edison.</span></span> <span data-ttu-id="a2463-110">Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="a2463-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

> [!NOTE]
> <span data-ttu-id="a2463-111">Hoewel de programmeertaal van de belangrijkste logica C, worden in de uitkomsten Node.js-hulpprogramma's om te bouwen en implementeren van de voorbeeldtoepassingen gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a2463-111">Although the programming language of the main logic is C, Node.js tools are used in the lessons to build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="a2463-112">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="a2463-112">What you will learn</span></span>
<span data-ttu-id="a2463-113">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="a2463-113">In this article, you will learn:</span></span>

* <span data-ttu-id="a2463-114">Klik hier voor meer informatie over het installeren van Git en Node.js.</span><span class="sxs-lookup"><span data-stu-id="a2463-114">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="a2463-115">[GIT](https://git-scm.com) is een open-source gedistribueerd versiebeheersysteem.</span><span class="sxs-lookup"><span data-stu-id="a2463-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="a2463-116">De voorbeeldtoepassing voor dit artikel wordt opgeslagen op Git.</span><span class="sxs-lookup"><span data-stu-id="a2463-116">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="a2463-117">[Node.js](https://nodejs.org/en/) is een JavaScript-runtime met een uitgebreide pakket-ecosysteem.</span><span class="sxs-lookup"><span data-stu-id="a2463-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="a2463-118">Hoe extra Node.js ontwikkelingsprogramma's installeren met NPM.</span><span class="sxs-lookup"><span data-stu-id="a2463-118">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="a2463-119">De minimum versievereisten voor Node.js is 4.5 TNS.</span><span class="sxs-lookup"><span data-stu-id="a2463-119">The minimum version requirement of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="a2463-120">[NPM](https://www.npmjs.com) is een van de pakket-managers voor Node.js.</span><span class="sxs-lookup"><span data-stu-id="a2463-120">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="a2463-121">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="a2463-121">What you need</span></span>

<span data-ttu-id="a2463-122">Om deze bewerking niet voltooien, moet u het:</span><span class="sxs-lookup"><span data-stu-id="a2463-122">To complete this operation, you will need:</span></span>

* <span data-ttu-id="a2463-123">Een internetverbinding om de ontwikkelprogramma's en de software te downloaden.</span><span class="sxs-lookup"><span data-stu-id="a2463-123">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="a2463-124">Een computer waarop Windows wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a2463-124">A computer that is running Windows.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="a2463-125">Installeer Git en Node.js</span><span class="sxs-lookup"><span data-stu-id="a2463-125">Install Git and Node.js</span></span>

<span data-ttu-id="a2463-126">Klik op de onderstaande koppelingen wilt downloaden en installeren van Git en Node.js LTS voor Windows.</span><span class="sxs-lookup"><span data-stu-id="a2463-126">Click the links below to download and install Git and Node.js LTS for Windows.</span></span>

* [<span data-ttu-id="a2463-127">Ophalen van Git voor Windows</span><span class="sxs-lookup"><span data-stu-id="a2463-127">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
* [<span data-ttu-id="a2463-128">Node.js TNS ophalen voor Windows</span><span class="sxs-lookup"><span data-stu-id="a2463-128">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="a2463-129">Extra hulpprogramma's voor Node.js-ontwikkeling</span><span class="sxs-lookup"><span data-stu-id="a2463-129">Install additional Node.js development tools</span></span>

<span data-ttu-id="a2463-130">Gebruik [gulp.js](http://gulpjs.com) voor de implementatie van de voorbeeldtoepassing om Edison te automatiseren.</span><span class="sxs-lookup"><span data-stu-id="a2463-130">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to Edison.</span></span>

<span data-ttu-id="a2463-131">Start een opdrachtprompt als beheerder.</span><span class="sxs-lookup"><span data-stu-id="a2463-131">Start a command prompt as an administrator.</span></span> <span data-ttu-id="a2463-132">Installeer `gulp` met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="a2463-132">Install `gulp` by running the following command:</span></span>

```cmd
npm install -g gulp
```

<span data-ttu-id="a2463-133">Als u problemen hebt met het installeren van Node.js en deze extra Node.js ontwikkelprogramma's op uw computer, Zie de [probleemoplossingsgids] [ troubleshooting] voor oplossingen voor bekende problemen.</span><span class="sxs-lookup"><span data-stu-id="a2463-133">If you experience issues installing Node.js and these additional Node.js development tools on your computer, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="a2463-134">Visual Studio Code installeren</span><span class="sxs-lookup"><span data-stu-id="a2463-134">Install Visual Studio Code</span></span>

<span data-ttu-id="a2463-135">[Download](https://code.visualstudio.com/docs/setup/windows) en Visual Studio Code installeren.</span><span class="sxs-lookup"><span data-stu-id="a2463-135">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span> <span data-ttu-id="a2463-136">Visual Studio Code is een eenvoudige maar krachtige broncode-editor voor Windows, Linux en Mac OS.</span><span class="sxs-lookup"><span data-stu-id="a2463-136">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="a2463-137">U gebruikt deze editor verderop in de zelfstudie voor het bewerken van de voorbeeldcode.</span><span class="sxs-lookup"><span data-stu-id="a2463-137">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="a2463-138">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="a2463-138">Summary</span></span>

<span data-ttu-id="a2463-139">U kunt de vereiste ontwikkelingsprogramma's en software voor de eerste voorbeeldtoepassing hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="a2463-139">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="a2463-140">De volgende taak is het maken, implementeren en uitvoeren van de voorbeeldtoepassing op Edison.</span><span class="sxs-lookup"><span data-stu-id="a2463-140">The next task is to create, deploy, and run the sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a2463-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a2463-141">Next steps</span></span>

<span data-ttu-id="a2463-142">[De toepassing knipperen maken en implementeren][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="a2463-142">[Create and deploy the blink application][create-and-deploy-the-blink-application]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-c-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-mac.md
