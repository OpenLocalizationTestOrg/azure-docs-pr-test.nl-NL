---
title: 'Connect Raspberry PI (C) naar Azure IoT - les 2: Azure-hulpprogramma''s (Windows) | Microsoft Docs'
description: Python en de Azure-opdrachtregelinterface (Azure CLI) installeren op Windows 7 en hoger.
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
ms.openlocfilehash: aa96000cb676c088a90f2b3d45c159913185a2e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-windows-7-and-later"></a><span data-ttu-id="09f5f-104">Ophalen van de Azure-hulpprogramma's (Windows 7 en hoger)</span><span class="sxs-lookup"><span data-stu-id="09f5f-104">Get Azure tools (Windows 7 and later)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="09f5f-105">Windows 7 en hoger</span><span class="sxs-lookup"><span data-stu-id="09f5f-105">Windows 7 and later</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)
> * [<span data-ttu-id="09f5f-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="09f5f-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-ubuntu.md)
> * [<span data-ttu-id="09f5f-107">Mac OS 10.10</span><span class="sxs-lookup"><span data-stu-id="09f5f-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="09f5f-108">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="09f5f-108">What you will do</span></span>
<span data-ttu-id="09f5f-109">Python en de Azure-opdrachtregelinterface (Azure CLI) installeren.</span><span class="sxs-lookup"><span data-stu-id="09f5f-109">Install Python and the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="09f5f-110">Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="09f5f-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="09f5f-111">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="09f5f-111">What you will learn</span></span>
<span data-ttu-id="09f5f-112">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="09f5f-112">In this article, you will learn:</span></span>
* <span data-ttu-id="09f5f-113">Klik hier voor meer informatie over het installeren van Python.</span><span class="sxs-lookup"><span data-stu-id="09f5f-113">How to install Python.</span></span>
* <span data-ttu-id="09f5f-114">Klik hier voor meer informatie over het installeren van de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="09f5f-114">How to install the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="09f5f-115">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="09f5f-115">What you need</span></span>
* <span data-ttu-id="09f5f-116">Een Windows-computer met een internetverbinding.</span><span class="sxs-lookup"><span data-stu-id="09f5f-116">A Windows computer with an Internet connection.</span></span>
* <span data-ttu-id="09f5f-117">Een actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="09f5f-117">An active Azure subscription.</span></span> <span data-ttu-id="09f5f-118">Als u geen Azure-account hebt, maakt u een [gratis proefaccount voor Azure](http://azure.microsoft.com/pricing/free-trial/) over een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="09f5f-118">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="09f5f-119">Installeren van Python</span><span class="sxs-lookup"><span data-stu-id="09f5f-119">Install Python</span></span>
<span data-ttu-id="09f5f-120">[Installeren van Python](https://www.python.org/downloads/) op uw Windows-computer.</span><span class="sxs-lookup"><span data-stu-id="09f5f-120">[Install Python](https://www.python.org/downloads/) on your Windows computer.</span></span> <span data-ttu-id="09f5f-121">U kunt Python 2.7 3.4 of 3.5 installeren.</span><span class="sxs-lookup"><span data-stu-id="09f5f-121">You can install Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="09f5f-122">Deze zelfstudie is gebaseerd op Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="09f5f-122">This tutorial is based on Python 2.7.</span></span> <span data-ttu-id="09f5f-123">Als u Python al hebt geïnstalleerd, gaat u naar de volgende sectie en Azure CLI installeren.</span><span class="sxs-lookup"><span data-stu-id="09f5f-123">If you've already installed Python, go to the next section and install the Azure CLI.</span></span>

<span data-ttu-id="09f5f-124">Ook moet u het pad van de mappen waar python.exe en pip.exe zijn geïnstalleerd op het systeem toevoegen `PATH` omgevingsvariabele.</span><span class="sxs-lookup"><span data-stu-id="09f5f-124">You also need to add the path of the folders where python.exe and pip.exe are installed to the system `PATH` environment variable.</span></span> <span data-ttu-id="09f5f-125">Python.exe worden standaard geïnstalleerd `C:\Python27` en pip.exe is geïnstalleerd in `C:\Python27\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="09f5f-125">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="09f5f-126">Azure-CLI installeren</span><span class="sxs-lookup"><span data-stu-id="09f5f-126">Install the Azure CLI</span></span>
<span data-ttu-id="09f5f-127">De Azure CLI biedt een meerdere platforms opdrachtregelprogramma ervaring voor Azure.</span><span class="sxs-lookup"><span data-stu-id="09f5f-127">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="09f5f-128">U werkt rechtstreeks vanaf de opdrachtregel inrichten en beheren van resources.</span><span class="sxs-lookup"><span data-stu-id="09f5f-128">You work directly from your command line to provision and manage resources.</span></span>

<span data-ttu-id="09f5f-129">Volg deze stappen voor het installeren van de Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="09f5f-129">To install the Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="09f5f-130">Open een opdrachtpromptvenster als administrator.</span><span class="sxs-lookup"><span data-stu-id="09f5f-130">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="09f5f-131">Voer de volgende opdrachten uit:</span><span class="sxs-lookup"><span data-stu-id="09f5f-131">Run the following commands:</span></span>

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
3. <span data-ttu-id="09f5f-132">De installatie controleren door de volgende opdracht uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="09f5f-132">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="09f5f-133">U ziet de volgende uitvoer als de installatie geslaagd is.</span><span class="sxs-lookup"><span data-stu-id="09f5f-133">You see the following output if the installation is successful.</span></span>

![Uitvoer die slagen aangeeft](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_win.png)

## <a name="summary"></a><span data-ttu-id="09f5f-135">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="09f5f-135">Summary</span></span>
<span data-ttu-id="09f5f-136">U kunt de Azure CLI hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="09f5f-136">You've installed the Azure CLI.</span></span> <span data-ttu-id="09f5f-137">Uw volgende taak voor het maken van uw Azure IoT hub- en apparaatidentiteiten met behulp van de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="09f5f-137">Your next task to create your Azure IoT hub and device identity by using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="09f5f-138">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="09f5f-138">Next steps</span></span>
[<span data-ttu-id="09f5f-139">Het maken van uw IoT-hub en frambozen Pi 3 registreren</span><span class="sxs-lookup"><span data-stu-id="09f5f-139">Create your IoT hub and register Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md)

