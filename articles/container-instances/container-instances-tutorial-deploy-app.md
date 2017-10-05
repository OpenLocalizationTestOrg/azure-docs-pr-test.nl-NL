---
title: Zelfstudie voor Azure Containerexemplaren - app implementeren | Microsoft Docs
description: Zelfstudie voor Azure Containerexemplaren - app implementeren
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 54151a5c1850ab7120fe666a46dc5dc99c0f5157
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-a-container-to-azure-container-instances"></a><span data-ttu-id="5a781-103">Een container implementeren naar Azure Containerexemplaren</span><span class="sxs-lookup"><span data-stu-id="5a781-103">Deploy a container to Azure Container Instances</span></span>

<span data-ttu-id="5a781-104">Dit is de laatste van een zelfstudie drie delen.</span><span class="sxs-lookup"><span data-stu-id="5a781-104">This is the last of a three-part tutorial.</span></span> <span data-ttu-id="5a781-105">In vorige gedeelten [is gemaakt met een installatiekopie van een container](container-instances-tutorial-prepare-app.md) en [naar een Azure Container Registry gepusht](container-instances-tutorial-prepare-acr.md).</span><span class="sxs-lookup"><span data-stu-id="5a781-105">In previous sections, [a container image was created](container-instances-tutorial-prepare-app.md) and [pushed to an Azure Container Registry](container-instances-tutorial-prepare-acr.md).</span></span> <span data-ttu-id="5a781-106">Deze sectie is de zelfstudie voltooid door het implementeren van de container op exemplaren van Azure-Container.</span><span class="sxs-lookup"><span data-stu-id="5a781-106">This section completes the tutorial by deploying the container to Azure Container Instances.</span></span> <span data-ttu-id="5a781-107">Stappen voltooid omvatten:</span><span class="sxs-lookup"><span data-stu-id="5a781-107">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5a781-108">Het definiëren van de containergroep van een met een Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="5a781-108">Defining a container group using an Azure Resource Manager template</span></span>
> * <span data-ttu-id="5a781-109">Implementatie van de containergroep met de Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5a781-109">Deploying the container group using the Azure CLI</span></span>
> * <span data-ttu-id="5a781-110">Container-logboeken bekijken</span><span class="sxs-lookup"><span data-stu-id="5a781-110">Viewing container logs</span></span>

## <a name="deploy-the-container-using-the-azure-cli"></a><span data-ttu-id="5a781-111">De container met de Azure CLI implementeren</span><span class="sxs-lookup"><span data-stu-id="5a781-111">Deploy the container using the Azure CLI</span></span>

<span data-ttu-id="5a781-112">De Azure CLI kunt de implementatie van een container voor exemplaren van Azure-Container in één opdracht.</span><span class="sxs-lookup"><span data-stu-id="5a781-112">The Azure CLI enables deployment of a container to Azure Container Instances in a single command.</span></span> <span data-ttu-id="5a781-113">Omdat de container-installatiekopie wordt gehost in het persoonlijke Azure-Container register, moet u de referenties voor toegang tot dit opnemen.</span><span class="sxs-lookup"><span data-stu-id="5a781-113">Since the container image is hosted in the private Azure Container Registry, you must include the credentials required to access it.</span></span> <span data-ttu-id="5a781-114">Indien nodig, kunt u ze opvragen, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="5a781-114">If necessary, you can query them as shown below.</span></span>

<span data-ttu-id="5a781-115">Container register login-server (update met de registernaam van uw):</span><span class="sxs-lookup"><span data-stu-id="5a781-115">Container registry login server (update with your registry name):</span></span>

```azurecli-interactive
az acr show --name <acrName> --query loginServer
```

<span data-ttu-id="5a781-116">Container register wachtwoord:</span><span class="sxs-lookup"><span data-stu-id="5a781-116">Container registry password:</span></span>

```azurecli-interactive
az acr credential show --name <acrName> --query "passwords[0].value"
```

<span data-ttu-id="5a781-117">Voor het implementeren van uw installatiekopie container uit het register van de container met een resource-aanvraag van het CPU-kern 1 en 1GB geheugen, moet u de volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="5a781-117">To deploy your container image from the container registry with a resource request of 1 CPU core and 1GB of memory, run the following command:</span></span>

```azurecli-interactive
az container create --name aci-tutorial-app --image <acrLoginServer>/aci-tutorial-app:v1 --cpu 1 --memory 1 --registry-password <acrPassword> --ip-address public -g myResourceGroup
```

<span data-ttu-id="5a781-118">Binnen enkele seconden ontvangt u een eerste reactie van Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5a781-118">Within a few seconds, you will receive an initial response from Azure Resource Manager.</span></span> <span data-ttu-id="5a781-119">Als u wilt weergeven van de status van de implementatie, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="5a781-119">To view the state of the deployment, use:</span></span>

```azurecli-interactive
az container show --name aci-tutorial-app --resource-group myResourceGroup --query state
```

<span data-ttu-id="5a781-120">U kunt doorgaan met deze opdracht wordt uitgevoerd totdat de status van verandert *in behandeling* naar *met*.</span><span class="sxs-lookup"><span data-stu-id="5a781-120">We can continue running this command until the state changes from *pending* to *running*.</span></span> <span data-ttu-id="5a781-121">Vervolgens kunnen we doorgaan.</span><span class="sxs-lookup"><span data-stu-id="5a781-121">Then we can proceed.</span></span>

## <a name="view-the-application-and-container-logs"></a><span data-ttu-id="5a781-122">Bekijk de logboeken toepassingen en container</span><span class="sxs-lookup"><span data-stu-id="5a781-122">View the application and container logs</span></span>

<span data-ttu-id="5a781-123">Zodra de implementatie is geslaagd, opent u uw browser naar de IP-adres dat wordt weergegeven in de uitvoer van de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="5a781-123">Once the deployment succeeds, open your browser to the IP address shown in the output of the following command:</span></span>

```bash
az container show --name aci-tutorial-app --resource-group myResourceGroup --query ipAddress.ip
```

```json
"13.88.176.27"
```

![Hallo wereld-app in de browser][aci-app-browser]

<span data-ttu-id="5a781-125">U kunt ook de uitvoer van de container bekijken:</span><span class="sxs-lookup"><span data-stu-id="5a781-125">You can also view the log output of the container:</span></span>

```azurecli-interactive
az container logs --name aci-tutorial-app -g myResourceGroup
```

<span data-ttu-id="5a781-126">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="5a781-126">Output:</span></span>

```bash
listening on port 80
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://13.88.176.27/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="next-steps"></a><span data-ttu-id="5a781-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5a781-127">Next steps</span></span>

<span data-ttu-id="5a781-128">In deze zelfstudie maakt voltooid u het proces voor het implementeren van uw containers op Azure Containerexemplaren.</span><span class="sxs-lookup"><span data-stu-id="5a781-128">In this tutorial, you completed the process of deploying your containers to Azure Container Instances.</span></span> <span data-ttu-id="5a781-129">De volgende stappen zijn voltooid:</span><span class="sxs-lookup"><span data-stu-id="5a781-129">The following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5a781-130">Implementatie van de container van het Azure-Container register met de Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5a781-130">Deploying the container from the Azure Container Registry using the Azure CLI</span></span>
> * <span data-ttu-id="5a781-131">De toepassing bekijken in de browser</span><span class="sxs-lookup"><span data-stu-id="5a781-131">Viewing the application in the browser</span></span>
> * <span data-ttu-id="5a781-132">De container logboeken bekijken</span><span class="sxs-lookup"><span data-stu-id="5a781-132">Viewing the container logs</span></span>

<!-- LINKS -->
[prepare-app]: ./container-instances-tutorial-prepare-app.md

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png
