---
title: 'Connect Intel Edison (C) tooAzure IoT - les 2: Azure-hulpprogramma''s (Windows) | Microsoft Docs'
description: Python en hello Azure-opdrachtregelinterface (Azure CLI) installeren op Windows 7 en hoger.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Azure cli, iot-cloudservice, arduino cloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 1035760e-cdd1-4d99-8003-067e98b29762
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 46f964541c00674500e4f6a072a9a2547b5b24d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-windows-7-and-later"></a><span data-ttu-id="da9b6-104">Ophalen van de Azure-hulpprogramma's (Windows 7 en hoger)</span><span class="sxs-lookup"><span data-stu-id="da9b6-104">Get Azure tools (Windows 7 and later)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="da9b6-105">[Windows 7 en hoger][windows]</span><span class="sxs-lookup"><span data-stu-id="da9b6-105">[Windows 7 and later][windows]</span></span>
> * <span data-ttu-id="da9b6-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="da9b6-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="da9b6-107">[Mac OS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="da9b6-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="da9b6-108">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="da9b6-108">What you will do</span></span>
<span data-ttu-id="da9b6-109">Installeer Python en hello Azure-opdrachtregelinterface (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="da9b6-109">Install Python and hello Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="da9b6-110">Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="da9b6-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="da9b6-111">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="da9b6-111">What you will learn</span></span>
<span data-ttu-id="da9b6-112">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="da9b6-112">In this article, you will learn:</span></span>
* <span data-ttu-id="da9b6-113">Hoe tooinstall Python.</span><span class="sxs-lookup"><span data-stu-id="da9b6-113">How tooinstall Python.</span></span>
* <span data-ttu-id="da9b6-114">Hoe tooinstall hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="da9b6-114">How tooinstall hello Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="da9b6-115">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="da9b6-115">What you need</span></span>
* <span data-ttu-id="da9b6-116">Een Windows-computer met een internetverbinding.</span><span class="sxs-lookup"><span data-stu-id="da9b6-116">A Windows computer with an Internet connection.</span></span>
* <span data-ttu-id="da9b6-117">Een actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="da9b6-117">An active Azure subscription.</span></span> <span data-ttu-id="da9b6-118">Als u geen Azure-account hebt, maakt u een [gratis proefaccount voor Azure](http://azure.microsoft.com/pricing/free-trial/) over een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="da9b6-118">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="da9b6-119">Installeren van Python</span><span class="sxs-lookup"><span data-stu-id="da9b6-119">Install Python</span></span>
<span data-ttu-id="da9b6-120">[Installeren van Python](https://www.python.org/downloads/) op uw Windows-computer.</span><span class="sxs-lookup"><span data-stu-id="da9b6-120">[Install Python](https://www.python.org/downloads/) on your Windows computer.</span></span> <span data-ttu-id="da9b6-121">U kunt Python 2.7 3.4 of 3.5 installeren.</span><span class="sxs-lookup"><span data-stu-id="da9b6-121">You can install Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="da9b6-122">Deze zelfstudie is gebaseerd op Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="da9b6-122">This tutorial is based on Python 2.7.</span></span> <span data-ttu-id="da9b6-123">Als u Python al hebt geïnstalleerd, gaat u de volgende sectie toohello en hello Azure CLI installeren.</span><span class="sxs-lookup"><span data-stu-id="da9b6-123">If you've already installed Python, go toohello next section and install hello Azure CLI.</span></span>

<span data-ttu-id="da9b6-124">U moet ook tooadd Hallo pad Hallo mappen waar systeem geïnstalleerde toohello python.exe en pip.exe zijn `PATH` omgevingsvariabele.</span><span class="sxs-lookup"><span data-stu-id="da9b6-124">You also need tooadd hello path of hello folders where python.exe and pip.exe are installed toohello system `PATH` environment variable.</span></span> <span data-ttu-id="da9b6-125">Python.exe worden standaard geïnstalleerd `C:\Python27` en pip.exe is geïnstalleerd in `C:\Python27\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="da9b6-125">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="da9b6-126">Hello Azure CLI installeren</span><span class="sxs-lookup"><span data-stu-id="da9b6-126">Install hello Azure CLI</span></span>
<span data-ttu-id="da9b6-127">Hello Azure CLI biedt een meerdere platforms opdrachtregelprogramma ervaring voor Azure.</span><span class="sxs-lookup"><span data-stu-id="da9b6-127">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="da9b6-128">U werkt rechtstreeks vanuit uw tooprovision vanaf de opdrachtregel en beheren van resources.</span><span class="sxs-lookup"><span data-stu-id="da9b6-128">You work directly from your command line tooprovision and manage resources.</span></span>

<span data-ttu-id="da9b6-129">tooinstall hello Azure CLI, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="da9b6-129">tooinstall hello Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="da9b6-130">Open een opdrachtpromptvenster als administrator.</span><span class="sxs-lookup"><span data-stu-id="da9b6-130">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="da9b6-131">Voer Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="da9b6-131">Run hello following commands:</span></span>

   ```cmd
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
3. <span data-ttu-id="da9b6-132">Hallo installatie controleren door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="da9b6-132">Verify hello installation by running hello following command:</span></span>

   ```cmd
   az iot -h
   ```

<span data-ttu-id="da9b6-133">Ziet u de volgende Hallo uitvoer als Hallo-installatie geslaagd is.</span><span class="sxs-lookup"><span data-stu-id="da9b6-133">You see hello following output if hello installation is successful.</span></span>

![Uitvoer die slagen aangeeft](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_win.png)

## <a name="summary"></a><span data-ttu-id="da9b6-135">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="da9b6-135">Summary</span></span>
<span data-ttu-id="da9b6-136">U kunt hello Azure CLI hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="da9b6-136">You've installed hello Azure CLI.</span></span> <span data-ttu-id="da9b6-137">Uw volgende taak toocreate uw Azure IoT hub- en apparaatidentiteiten met behulp van hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="da9b6-137">Your next task toocreate your Azure IoT hub and device identity by using hello Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="da9b6-138">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="da9b6-138">Next steps</span></span>
<span data-ttu-id="da9b6-139">[Het maken van uw IoT-hub en Intel Edison registreren][create-your-iot-hub-and-register-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="da9b6-139">[Create your IoT hub and register Intel Edison][create-your-iot-hub-and-register-intel-edison]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-mac.md
