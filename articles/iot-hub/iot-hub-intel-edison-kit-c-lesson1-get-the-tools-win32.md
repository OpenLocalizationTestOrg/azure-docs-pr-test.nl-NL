---
title: 'Connect Intel Edison (C) tooAzure IoT - les 1: download hulpprogramma''s (Windows) | Microsoft Docs'
description: Download en installeer Hallo vereiste hulpprogramma's en -software voor de eerste voorbeeldtoepassing voor Edison Hallo op Windows 7 en hoger.
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
ms.openlocfilehash: 64d8684ffcb858845de02276a11cf2b2e5c701a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-or-later"></a><span data-ttu-id="9aa49-104">Ophalen van Hallo hulpprogramma's (Windows 7 of hoger)</span><span class="sxs-lookup"><span data-stu-id="9aa49-104">Get hello tools (Windows 7 or later)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="9aa49-105">[Windows 7 of hoger][windows]</span><span class="sxs-lookup"><span data-stu-id="9aa49-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="9aa49-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="9aa49-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="9aa49-107">[Mac OS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="9aa49-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="9aa49-108">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="9aa49-108">What you will do</span></span>
<span data-ttu-id="9aa49-109">Hallo ontwikkelingsprogramma's en software voor eerste voorbeeldtoepassing voor Intel Edison Hallo Hallo downloaden.</span><span class="sxs-lookup"><span data-stu-id="9aa49-109">Download hello development tools and hello software for hello first sample application for Intel Edison.</span></span> <span data-ttu-id="9aa49-110">Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="9aa49-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

> [!NOTE]
> <span data-ttu-id="9aa49-111">Hoewel Hallo programmeertaal van logische Hallo C is, wordt Node.js-hulpprogramma's worden gebruikt in Hallo uitkomsten toobuild en voorbeeldtoepassingen implementeren.</span><span class="sxs-lookup"><span data-stu-id="9aa49-111">Although hello programming language of hello main logic is C, Node.js tools are used in hello lessons toobuild and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="9aa49-112">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="9aa49-112">What you will learn</span></span>
<span data-ttu-id="9aa49-113">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="9aa49-113">In this article, you will learn:</span></span>

* <span data-ttu-id="9aa49-114">Hoe tooinstall Git en Node.js.</span><span class="sxs-lookup"><span data-stu-id="9aa49-114">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="9aa49-115">[GIT](https://git-scm.com) is een open-source gedistribueerd versiebeheersysteem.</span><span class="sxs-lookup"><span data-stu-id="9aa49-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="9aa49-116">Hallo-voorbeeldtoepassing voor dit artikel wordt opgeslagen op Git.</span><span class="sxs-lookup"><span data-stu-id="9aa49-116">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="9aa49-117">[Node.js](https://nodejs.org/en/) is een JavaScript-runtime met een uitgebreide pakket-ecosysteem.</span><span class="sxs-lookup"><span data-stu-id="9aa49-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="9aa49-118">Hoe toouse NPM tooinstall extra Node.js ontwikkelingsprogramma's.</span><span class="sxs-lookup"><span data-stu-id="9aa49-118">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="9aa49-119">Hallo minimum versievereisten voor Node.js is 4.5 TNS.</span><span class="sxs-lookup"><span data-stu-id="9aa49-119">hello minimum version requirement of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="9aa49-120">[NPM](https://www.npmjs.com) is een van de Hallo pakket managers voor Node.js.</span><span class="sxs-lookup"><span data-stu-id="9aa49-120">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="9aa49-121">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="9aa49-121">What you need</span></span>

<span data-ttu-id="9aa49-122">toocomplete deze bewerking moet u:</span><span class="sxs-lookup"><span data-stu-id="9aa49-122">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="9aa49-123">Een Internet verbinding toodownload Hallo ontwikkelingsprogramma's en software Hallo.</span><span class="sxs-lookup"><span data-stu-id="9aa49-123">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="9aa49-124">Een computer waarop Windows wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9aa49-124">A computer that is running Windows.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="9aa49-125">Installeer Git en Node.js</span><span class="sxs-lookup"><span data-stu-id="9aa49-125">Install Git and Node.js</span></span>

<span data-ttu-id="9aa49-126">Klik op onderstaande toodownload Hallo koppelingen en installeer Git en Node.js LTS voor Windows.</span><span class="sxs-lookup"><span data-stu-id="9aa49-126">Click hello links below toodownload and install Git and Node.js LTS for Windows.</span></span>

* [<span data-ttu-id="9aa49-127">Ophalen van Git voor Windows</span><span class="sxs-lookup"><span data-stu-id="9aa49-127">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
* [<span data-ttu-id="9aa49-128">Node.js TNS ophalen voor Windows</span><span class="sxs-lookup"><span data-stu-id="9aa49-128">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="9aa49-129">Extra hulpprogramma's voor Node.js-ontwikkeling</span><span class="sxs-lookup"><span data-stu-id="9aa49-129">Install additional Node.js development tools</span></span>

<span data-ttu-id="9aa49-130">Gebruik [gulp.js](http://gulpjs.com) tooautomate Hallo implementatie van Hallo voorbeeld toepassing tooEdison.</span><span class="sxs-lookup"><span data-stu-id="9aa49-130">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooEdison.</span></span>

<span data-ttu-id="9aa49-131">Start een opdrachtprompt als beheerder.</span><span class="sxs-lookup"><span data-stu-id="9aa49-131">Start a command prompt as an administrator.</span></span> <span data-ttu-id="9aa49-132">Installeer `gulp` door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="9aa49-132">Install `gulp` by running hello following command:</span></span>

```cmd
npm install -g gulp
```

<span data-ttu-id="9aa49-133">Als u problemen hebt met het installeren van Node.js en deze extra Node.js ontwikkelprogramma's op uw computer, Zie Hallo [probleemoplossingsgids] [ troubleshooting] voor toocommon oplossingen voor problemen.</span><span class="sxs-lookup"><span data-stu-id="9aa49-133">If you experience issues installing Node.js and these additional Node.js development tools on your computer, see hello [troubleshooting guide][troubleshooting] for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="9aa49-134">Visual Studio Code installeren</span><span class="sxs-lookup"><span data-stu-id="9aa49-134">Install Visual Studio Code</span></span>

<span data-ttu-id="9aa49-135">[Download](https://code.visualstudio.com/docs/setup/windows) en Visual Studio Code installeren.</span><span class="sxs-lookup"><span data-stu-id="9aa49-135">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span> <span data-ttu-id="9aa49-136">Visual Studio Code is een eenvoudige maar krachtige broncode-editor voor Windows, Linux en Mac OS.</span><span class="sxs-lookup"><span data-stu-id="9aa49-136">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="9aa49-137">U gebruikt deze editor verderop in Hallo zelfstudie tooedit Hallo voorbeeldcode.</span><span class="sxs-lookup"><span data-stu-id="9aa49-137">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="9aa49-138">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="9aa49-138">Summary</span></span>

<span data-ttu-id="9aa49-139">U kunt Hallo vereist ontwikkelingsprogramma's en -software voor het eerste voorbeeldtoepassing hello hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="9aa49-139">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="9aa49-140">de volgende taak Hallo is toocreate, implementeren en uitvoeren van de voorbeeldtoepassing Hallo op Edison.</span><span class="sxs-lookup"><span data-stu-id="9aa49-140">hello next task is toocreate, deploy, and run hello sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9aa49-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9aa49-141">Next steps</span></span>

<span data-ttu-id="9aa49-142">[Hallo knipperen toepassing maken en implementeren][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="9aa49-142">[Create and deploy hello blink application][create-and-deploy-the-blink-application]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-c-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-mac.md
