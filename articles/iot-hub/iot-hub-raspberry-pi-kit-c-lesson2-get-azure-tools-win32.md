---
title: 'Connect Raspberry PI (C) tooAzure IoT - les 2: Azure-hulpprogramma''s (Windows) | Microsoft Docs'
description: Python en hello Azure-opdrachtregelinterface (Azure CLI) installeren op Windows 7 en hoger.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: IOT cloud-service, azure cli
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: a3c083b5-0d76-46af-bc77-2ad7d8aadc1e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 1819d61fafbee6ac42a1bea5c16437cd8bf43af9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-windows-7-and-later"></a><span data-ttu-id="b0312-104">Ophalen van de Azure-hulpprogramma's (Windows 7 en hoger)</span><span class="sxs-lookup"><span data-stu-id="b0312-104">Get Azure tools (Windows 7 and later)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b0312-105">Windows 7 en hoger</span><span class="sxs-lookup"><span data-stu-id="b0312-105">Windows 7 and later</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)
> * [<span data-ttu-id="b0312-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="b0312-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-ubuntu.md)
> * [<span data-ttu-id="b0312-107">Mac OS 10.10</span><span class="sxs-lookup"><span data-stu-id="b0312-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="b0312-108">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="b0312-108">What you will do</span></span>
<span data-ttu-id="b0312-109">Installeer Python en hello Azure-opdrachtregelinterface (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="b0312-109">Install Python and hello Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="b0312-110">Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="b0312-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="b0312-111">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="b0312-111">What you will learn</span></span>
<span data-ttu-id="b0312-112">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="b0312-112">In this article, you will learn:</span></span>
* <span data-ttu-id="b0312-113">Hoe tooinstall Python.</span><span class="sxs-lookup"><span data-stu-id="b0312-113">How tooinstall Python.</span></span>
* <span data-ttu-id="b0312-114">Hoe tooinstall hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="b0312-114">How tooinstall hello Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="b0312-115">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="b0312-115">What you need</span></span>
* <span data-ttu-id="b0312-116">Een Windows-computer met een internetverbinding.</span><span class="sxs-lookup"><span data-stu-id="b0312-116">A Windows computer with an Internet connection.</span></span>
* <span data-ttu-id="b0312-117">Een actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="b0312-117">An active Azure subscription.</span></span> <span data-ttu-id="b0312-118">Als u geen Azure-account hebt, maakt u een [gratis proefaccount voor Azure](http://azure.microsoft.com/pricing/free-trial/) over een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="b0312-118">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="b0312-119">Installeren van Python</span><span class="sxs-lookup"><span data-stu-id="b0312-119">Install Python</span></span>
<span data-ttu-id="b0312-120">[Installeren van Python](https://www.python.org/downloads/) op uw Windows-computer.</span><span class="sxs-lookup"><span data-stu-id="b0312-120">[Install Python](https://www.python.org/downloads/) on your Windows computer.</span></span> <span data-ttu-id="b0312-121">U kunt Python 2.7 3.4 of 3.5 installeren.</span><span class="sxs-lookup"><span data-stu-id="b0312-121">You can install Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="b0312-122">Deze zelfstudie is gebaseerd op Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="b0312-122">This tutorial is based on Python 2.7.</span></span> <span data-ttu-id="b0312-123">Als u Python al hebt geïnstalleerd, gaat u de volgende sectie toohello en hello Azure CLI installeren.</span><span class="sxs-lookup"><span data-stu-id="b0312-123">If you've already installed Python, go toohello next section and install hello Azure CLI.</span></span>

<span data-ttu-id="b0312-124">U moet ook tooadd Hallo pad Hallo mappen waar systeem geïnstalleerde toohello python.exe en pip.exe zijn `PATH` omgevingsvariabele.</span><span class="sxs-lookup"><span data-stu-id="b0312-124">You also need tooadd hello path of hello folders where python.exe and pip.exe are installed toohello system `PATH` environment variable.</span></span> <span data-ttu-id="b0312-125">Python.exe worden standaard geïnstalleerd `C:\Python27` en pip.exe is geïnstalleerd in `C:\Python27\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="b0312-125">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="b0312-126">Hello Azure CLI installeren</span><span class="sxs-lookup"><span data-stu-id="b0312-126">Install hello Azure CLI</span></span>
<span data-ttu-id="b0312-127">Hello Azure CLI biedt een meerdere platforms opdrachtregelprogramma ervaring voor Azure.</span><span class="sxs-lookup"><span data-stu-id="b0312-127">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="b0312-128">U werkt rechtstreeks vanuit uw tooprovision vanaf de opdrachtregel en beheren van resources.</span><span class="sxs-lookup"><span data-stu-id="b0312-128">You work directly from your command line tooprovision and manage resources.</span></span>

<span data-ttu-id="b0312-129">tooinstall hello Azure CLI, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="b0312-129">tooinstall hello Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="b0312-130">Open een opdrachtpromptvenster als administrator.</span><span class="sxs-lookup"><span data-stu-id="b0312-130">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="b0312-131">Voer Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="b0312-131">Run hello following commands:</span></span>

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
3. <span data-ttu-id="b0312-132">Hallo installatie controleren door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="b0312-132">Verify hello installation by running hello following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="b0312-133">Ziet u de volgende Hallo uitvoer als Hallo-installatie geslaagd is.</span><span class="sxs-lookup"><span data-stu-id="b0312-133">You see hello following output if hello installation is successful.</span></span>

![Uitvoer die slagen aangeeft](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_win.png)

## <a name="summary"></a><span data-ttu-id="b0312-135">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="b0312-135">Summary</span></span>
<span data-ttu-id="b0312-136">U kunt hello Azure CLI hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="b0312-136">You've installed hello Azure CLI.</span></span> <span data-ttu-id="b0312-137">Uw volgende taak toocreate uw Azure IoT hub- en apparaatidentiteiten met behulp van hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="b0312-137">Your next task toocreate your Azure IoT hub and device identity by using hello Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b0312-138">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b0312-138">Next steps</span></span>
[<span data-ttu-id="b0312-139">Het maken van uw IoT-hub en frambozen Pi 3 registreren</span><span class="sxs-lookup"><span data-stu-id="b0312-139">Create your IoT hub and register Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md)

