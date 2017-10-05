---
title: 'Connect Intel Edison (C) naar Azure IoT - les 2: Azure-hulpprogramma''s (Mac OS) | Microsoft Docs'
description: Python en Azure-opdrachtregelinterface (Azure CLI) installeren op Mac OS.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Azure cli, iot-cloudservice, arduino cloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: d561680f-69cc-427a-820d-24f710ba05a8
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 97beb04781f3f9809cdafc945d9499e71cbbd9b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-macos-1010"></a><span data-ttu-id="c6f22-104">Azure-hulpprogramma's (Mac OS 10.10) ophalen</span><span class="sxs-lookup"><span data-stu-id="c6f22-104">Get Azure tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="c6f22-105">[Windows 7 en hoger][windows]</span><span class="sxs-lookup"><span data-stu-id="c6f22-105">[Windows 7 and later][windows]</span></span>
> * <span data-ttu-id="c6f22-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="c6f22-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="c6f22-107">[Mac OS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="c6f22-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="c6f22-108">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="c6f22-108">What you will do</span></span>
<span data-ttu-id="c6f22-109">Installeer de Azure-opdrachtregelinterface (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="c6f22-109">Install the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="c6f22-110">Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="c6f22-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="c6f22-111">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="c6f22-111">What you will learn</span></span>
<span data-ttu-id="c6f22-112">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="c6f22-112">In this article, you will learn:</span></span>
* <span data-ttu-id="c6f22-113">Klik hier voor meer informatie over het installeren van Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="c6f22-113">How to install Azure CLI.</span></span>
* <span data-ttu-id="c6f22-114">Het toevoegen van een IoT-subgroep van de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="c6f22-114">How to add an IoT subgroup of the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="c6f22-115">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="c6f22-115">What you need</span></span>
* <span data-ttu-id="c6f22-116">Een Mac met een internetverbinding.</span><span class="sxs-lookup"><span data-stu-id="c6f22-116">A Mac with an Internet connection.</span></span>
* <span data-ttu-id="c6f22-117">Een actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="c6f22-117">An active Azure subscription.</span></span> <span data-ttu-id="c6f22-118">Als u geen Azure-account hebt, kunt u een [gratis proefaccount voor Azure](http://azure.microsoft.com/pricing/free-trial/) over een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="c6f22-118">If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="c6f22-119">Installeren van Python</span><span class="sxs-lookup"><span data-stu-id="c6f22-119">Install Python</span></span>
<span data-ttu-id="c6f22-120">Hoewel Mac OS wordt geleverd met Python 2.7 gebruiksklaar, raden wij aan dat u Python via Homebrew installeert.</span><span class="sxs-lookup"><span data-stu-id="c6f22-120">Although macOS comes with Python 2.7 out of the box, we recommend that you install Python through Homebrew.</span></span> <span data-ttu-id="c6f22-121">Zie [Python installeren op Mac OS](http://docs.python-guide.org/en/latest/starting/install/osx/).</span><span class="sxs-lookup"><span data-stu-id="c6f22-121">See [Installing Python on macOS](http://docs.python-guide.org/en/latest/starting/install/osx/).</span></span>

<span data-ttu-id="c6f22-122">Python en pip installeren met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="c6f22-122">Install Python and pip by running the following command:</span></span>

```bash
brew install python
```

## <a name="install-the-azure-cli"></a><span data-ttu-id="c6f22-123">Azure-CLI installeren</span><span class="sxs-lookup"><span data-stu-id="c6f22-123">Install the Azure CLI</span></span>
<span data-ttu-id="c6f22-124">De Azure CLI biedt een meerdere platforms opdrachtregelprogramma ervaring voor Azure.</span><span class="sxs-lookup"><span data-stu-id="c6f22-124">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="c6f22-125">U werkt rechtstreeks vanaf de opdrachtregel inrichten en beheren van resources.</span><span class="sxs-lookup"><span data-stu-id="c6f22-125">You work directly from your command line to provision and manage resources.</span></span> 

<span data-ttu-id="c6f22-126">Volg deze stappen voor het installeren van de nieuwste Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="c6f22-126">To install the latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="c6f22-127">Voer de volgende opdrachten in een terminalvenster.</span><span class="sxs-lookup"><span data-stu-id="c6f22-127">Run the following commands in a terminal window.</span></span> <span data-ttu-id="c6f22-128">Het duurt vijf minuten voor het installeren van de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="c6f22-128">It might take five minutes to install the Azure CLI.</span></span>

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="c6f22-129">De installatie controleren door de volgende opdracht uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="c6f22-129">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="c6f22-130">U ziet de volgende uitvoer als de installatie geslaagd is.</span><span class="sxs-lookup"><span data-stu-id="c6f22-130">You should see the following output if the installation is successful.</span></span>

![Uitvoer die slagen aangeeft](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_osx.png)

## <a name="summary"></a><span data-ttu-id="c6f22-132">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="c6f22-132">Summary</span></span>
<span data-ttu-id="c6f22-133">U kunt de Azure CLI hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="c6f22-133">You've installed the Azure CLI.</span></span> <span data-ttu-id="c6f22-134">Uw volgende taak is het maken van uw Azure IoT hub- en apparaatidentiteiten met behulp van de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="c6f22-134">Your next task is to create your Azure IoT hub and device identity by using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c6f22-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c6f22-135">Next steps</span></span>
<span data-ttu-id="c6f22-136">[Het maken van uw IoT-hub en Intel Edison registreren][create-your-iot-hub-and-register-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="c6f22-136">[Create your IoT hub and register Intel Edison][create-your-iot-hub-and-register-intel-edison]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-mac.md
