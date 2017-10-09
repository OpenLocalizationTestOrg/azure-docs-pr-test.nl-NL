---
title: 'Verbinding maken met Intel Edison (knooppunt) tooAzure IoT - les 1: download hulpprogramma''s (Windows) | Microsoft Docs'
description: Download en installeer Hallo vereiste hulpprogramma's en -software voor de eerste voorbeeldtoepassing voor Edison Hallo op Windows 7 en hoger.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: arduino ontwikkelingsprogramma's, iot-ontwikkeling, iot-software, internet van dingen software, installeer git voor windows, windows voor knooppunt js installeren
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 4164b5a1-5a42-4d8a-9ff6-441e79fcc936
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 933cc585d1b8b0236d76452f5c449ae9f2f3987b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-or-later"></a><span data-ttu-id="81355-104">Ophalen van Hallo hulpprogramma's (Windows 7 of hoger)</span><span class="sxs-lookup"><span data-stu-id="81355-104">Get hello tools (Windows 7 or later)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="81355-105">[Windows 7 of hoger][windows]</span><span class="sxs-lookup"><span data-stu-id="81355-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="81355-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="81355-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="81355-107">[Mac OS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="81355-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="81355-108">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="81355-108">What you will do</span></span>
<span data-ttu-id="81355-109">Hallo ontwikkelingsprogramma's en software voor eerste voorbeeldtoepassing voor Intel Edison Hallo Hallo downloaden.</span><span class="sxs-lookup"><span data-stu-id="81355-109">Download hello development tools and hello software for hello first sample application for Intel Edison.</span></span> <span data-ttu-id="81355-110">Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="81355-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="81355-111">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="81355-111">What you will learn</span></span>
<span data-ttu-id="81355-112">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="81355-112">In this article, you will learn:</span></span>

* <span data-ttu-id="81355-113">Hoe tooinstall Git en Node.js.</span><span class="sxs-lookup"><span data-stu-id="81355-113">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="81355-114">[GIT](https://git-scm.com) is een open-source gedistribueerd versiebeheersysteem.</span><span class="sxs-lookup"><span data-stu-id="81355-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="81355-115">Hallo-voorbeeldtoepassing voor dit artikel wordt opgeslagen op Git.</span><span class="sxs-lookup"><span data-stu-id="81355-115">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="81355-116">[Node.js](https://nodejs.org/en/) is een JavaScript-runtime met een uitgebreide pakket-ecosysteem.</span><span class="sxs-lookup"><span data-stu-id="81355-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="81355-117">Hoe toouse NPM tooinstall extra Node.js ontwikkelingsprogramma's.</span><span class="sxs-lookup"><span data-stu-id="81355-117">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="81355-118">Hallo minimum versievereisten voor Node.js is 4.5 TNS.</span><span class="sxs-lookup"><span data-stu-id="81355-118">hello minimum version requirement of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="81355-119">[NPM](https://www.npmjs.com) is een van de Hallo pakket managers voor Node.js.</span><span class="sxs-lookup"><span data-stu-id="81355-119">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="81355-120">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="81355-120">What you need</span></span>

<span data-ttu-id="81355-121">toocomplete deze bewerking moet u:</span><span class="sxs-lookup"><span data-stu-id="81355-121">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="81355-122">Een Internet verbinding toodownload Hallo ontwikkelingsprogramma's en software Hallo.</span><span class="sxs-lookup"><span data-stu-id="81355-122">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="81355-123">Een computer waarop Windows wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="81355-123">A computer that is running Windows.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="81355-124">Installeer Git en Node.js</span><span class="sxs-lookup"><span data-stu-id="81355-124">Install Git and Node.js</span></span>

<span data-ttu-id="81355-125">Klik op onderstaande toodownload Hallo koppelingen en installeer Git en Node.js LTS voor Windows.</span><span class="sxs-lookup"><span data-stu-id="81355-125">Click hello links below toodownload and install Git and Node.js LTS for Windows.</span></span>

* [<span data-ttu-id="81355-126">Ophalen van Git voor Windows</span><span class="sxs-lookup"><span data-stu-id="81355-126">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
* [<span data-ttu-id="81355-127">Node.js TNS ophalen voor Windows</span><span class="sxs-lookup"><span data-stu-id="81355-127">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="81355-128">Extra hulpprogramma's voor Node.js-ontwikkeling</span><span class="sxs-lookup"><span data-stu-id="81355-128">Install additional Node.js development tools</span></span>

<span data-ttu-id="81355-129">Gebruik [gulp.js](http://gulpjs.com) tooautomate Hallo implementatie van Hallo voorbeeld toepassing tooEdison.</span><span class="sxs-lookup"><span data-stu-id="81355-129">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooEdison.</span></span>

<span data-ttu-id="81355-130">Start een opdrachtprompt als beheerder.</span><span class="sxs-lookup"><span data-stu-id="81355-130">Start a command prompt as an administrator.</span></span> <span data-ttu-id="81355-131">Installeer `gulp` door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="81355-131">Install `gulp` by running hello following command:</span></span>

```cmd
npm install -g gulp
```

<span data-ttu-id="81355-132">Als u problemen hebt met het installeren van Node.js en deze extra Node.js ontwikkelprogramma's op uw computer, Zie Hallo [probleemoplossingsgids] [ troubleshooting] voor toocommon oplossingen voor problemen.</span><span class="sxs-lookup"><span data-stu-id="81355-132">If you experience issues installing Node.js and these additional Node.js development tools on your computer, see hello [troubleshooting guide][troubleshooting] for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="81355-133">Visual Studio Code installeren</span><span class="sxs-lookup"><span data-stu-id="81355-133">Install Visual Studio Code</span></span>

<span data-ttu-id="81355-134">[Download](https://code.visualstudio.com/docs/setup/windows) en Visual Studio Code installeren.</span><span class="sxs-lookup"><span data-stu-id="81355-134">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span> <span data-ttu-id="81355-135">Visual Studio Code is een eenvoudige maar krachtige broncode-editor voor Windows, Linux en Mac OS.</span><span class="sxs-lookup"><span data-stu-id="81355-135">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="81355-136">U gebruikt deze editor verderop in Hallo zelfstudie tooedit Hallo voorbeeldcode.</span><span class="sxs-lookup"><span data-stu-id="81355-136">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="81355-137">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="81355-137">Summary</span></span>

<span data-ttu-id="81355-138">U kunt Hallo vereist ontwikkelingsprogramma's en -software voor het eerste voorbeeldtoepassing hello hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="81355-138">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="81355-139">de volgende taak Hallo is toocreate, implementeren en uitvoeren van de voorbeeldtoepassing Hallo op Edison.</span><span class="sxs-lookup"><span data-stu-id="81355-139">hello next task is toocreate, deploy, and run hello sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="81355-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="81355-140">Next steps</span></span>

<span data-ttu-id="81355-141">[Hallo knipperen toepassing maken en implementeren][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="81355-141">[Create and deploy hello blink application][create-and-deploy-the-blink-application]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-node-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-mac.md
