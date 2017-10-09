---
title: 'Verbinding maken met Intel Edison (knooppunt) tooAzure IoT - les 2: Azure-hulpprogramma''s (Mac OS) | Microsoft Docs'
description: Python en Azure-opdrachtregelinterface (Azure CLI) installeren op Mac OS.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Azure cli, iot-cloudservice, arduino cloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 8a2a8031-b1a6-4219-b17d-2825550c35e1
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: e33b3c9ee8f06f1c6175457f98a0600dd945cf1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-macos-1010"></a><span data-ttu-id="ffc36-104">Azure-hulpprogramma's (Mac OS 10.10) ophalen</span><span class="sxs-lookup"><span data-stu-id="ffc36-104">Get Azure tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="ffc36-105">[Windows 7 en hoger][windows]</span><span class="sxs-lookup"><span data-stu-id="ffc36-105">[Windows 7 and later][windows]</span></span>
> * <span data-ttu-id="ffc36-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="ffc36-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="ffc36-107">[Mac OS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="ffc36-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="ffc36-108">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="ffc36-108">What you will do</span></span>
<span data-ttu-id="ffc36-109">Hello Azure-opdrachtregelinterface (Azure CLI) installeren.</span><span class="sxs-lookup"><span data-stu-id="ffc36-109">Install hello Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="ffc36-110">Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="ffc36-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="ffc36-111">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="ffc36-111">What you will learn</span></span>
<span data-ttu-id="ffc36-112">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="ffc36-112">In this article, you will learn:</span></span>
* <span data-ttu-id="ffc36-113">Hoe tooinstall Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="ffc36-113">How tooinstall Azure CLI.</span></span>
* <span data-ttu-id="ffc36-114">Hoe tooadd een subgroep IoT Hallo Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="ffc36-114">How tooadd an IoT subgroup of hello Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="ffc36-115">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="ffc36-115">What you need</span></span>
* <span data-ttu-id="ffc36-116">Een Mac met een internetverbinding.</span><span class="sxs-lookup"><span data-stu-id="ffc36-116">A Mac with an Internet connection.</span></span>
* <span data-ttu-id="ffc36-117">Een actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="ffc36-117">An active Azure subscription.</span></span> <span data-ttu-id="ffc36-118">Als u geen Azure-account hebt, kunt u een [gratis proefaccount voor Azure](http://azure.microsoft.com/pricing/free-trial/) over een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="ffc36-118">If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="ffc36-119">Installeren van Python</span><span class="sxs-lookup"><span data-stu-id="ffc36-119">Install Python</span></span>
<span data-ttu-id="ffc36-120">Hoewel Mac OS wordt geleverd met Python 2.7 out of box hello, raden wij aan dat u Python via Homebrew installeert.</span><span class="sxs-lookup"><span data-stu-id="ffc36-120">Although macOS comes with Python 2.7 out of hello box, we recommend that you install Python through Homebrew.</span></span> <span data-ttu-id="ffc36-121">Zie [Python installeren op Mac OS](http://docs.python-guide.org/en/latest/starting/install/osx/).</span><span class="sxs-lookup"><span data-stu-id="ffc36-121">See [Installing Python on macOS](http://docs.python-guide.org/en/latest/starting/install/osx/).</span></span>

<span data-ttu-id="ffc36-122">Python en pip door het uitvoeren van de volgende opdracht Hallo installeren:</span><span class="sxs-lookup"><span data-stu-id="ffc36-122">Install Python and pip by running hello following command:</span></span>

```bash
brew install python
```

## <a name="install-hello-azure-cli"></a><span data-ttu-id="ffc36-123">Hello Azure CLI installeren</span><span class="sxs-lookup"><span data-stu-id="ffc36-123">Install hello Azure CLI</span></span>
<span data-ttu-id="ffc36-124">Hello Azure CLI biedt een meerdere platforms opdrachtregelprogramma ervaring voor Azure.</span><span class="sxs-lookup"><span data-stu-id="ffc36-124">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="ffc36-125">U werkt rechtstreeks vanuit uw tooprovision vanaf de opdrachtregel en beheren van resources.</span><span class="sxs-lookup"><span data-stu-id="ffc36-125">You work directly from your command line tooprovision and manage resources.</span></span> 

<span data-ttu-id="ffc36-126">tooinstall Hallo nieuwste Azure CLI, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="ffc36-126">tooinstall hello latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="ffc36-127">Hallo volgende opdrachten in een terminalvenster worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ffc36-127">Run hello following commands in a terminal window.</span></span> <span data-ttu-id="ffc36-128">Vijf minuten tooinstall hello Azure CLI kan duren.</span><span class="sxs-lookup"><span data-stu-id="ffc36-128">It might take five minutes tooinstall hello Azure CLI.</span></span>

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="ffc36-129">Hallo installatie controleren door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="ffc36-129">Verify hello installation by running hello following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="ffc36-130">U ziet de volgende Hallo uitvoer als Hallo-installatie geslaagd is.</span><span class="sxs-lookup"><span data-stu-id="ffc36-130">You should see hello following output if hello installation is successful.</span></span>

![Uitvoer die slagen aangeeft](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_osx.png)

## <a name="summary"></a><span data-ttu-id="ffc36-132">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="ffc36-132">Summary</span></span>
<span data-ttu-id="ffc36-133">U kunt hello Azure CLI hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="ffc36-133">You've installed hello Azure CLI.</span></span> <span data-ttu-id="ffc36-134">Het is uw volgende taak toocreate uw Azure IoT hub- en apparaatidentiteiten met behulp van hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="ffc36-134">Your next task is toocreate your Azure IoT hub and device identity by using hello Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ffc36-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ffc36-135">Next steps</span></span>
<span data-ttu-id="ffc36-136">[Het maken van uw IoT-hub en Intel Edison registreren][create-your-iot-hub-and-register-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="ffc36-136">[Create your IoT hub and register Intel Edison][create-your-iot-hub-and-register-intel-edison]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-mac.md
