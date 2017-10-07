---
title: aaaAzure Containerexemplaren zelfstudie - app implementeren | Microsoft Docs
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
ms.openlocfilehash: b9fb098d9491e1073f0be4b14a0b9b1a18f16095
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-container-tooazure-container-instances"></a><span data-ttu-id="db57e-103">Een container tooAzure Containerexemplaren implementeren</span><span class="sxs-lookup"><span data-stu-id="db57e-103">Deploy a container tooAzure Container Instances</span></span>

<span data-ttu-id="db57e-104">Dit is Hallo laatste van een zelfstudie drie delen.</span><span class="sxs-lookup"><span data-stu-id="db57e-104">This is hello last of a three-part tutorial.</span></span> <span data-ttu-id="db57e-105">In vorige gedeelten [is gemaakt met een installatiekopie van een container](container-instances-tutorial-prepare-app.md) en [tooan Azure Container register gepusht](container-instances-tutorial-prepare-acr.md).</span><span class="sxs-lookup"><span data-stu-id="db57e-105">In previous sections, [a container image was created](container-instances-tutorial-prepare-app.md) and [pushed tooan Azure Container Registry](container-instances-tutorial-prepare-acr.md).</span></span> <span data-ttu-id="db57e-106">In deze sectie is Hallo-zelfstudie voltooid door het implementeren van Hallo container tooAzure Containerexemplaren.</span><span class="sxs-lookup"><span data-stu-id="db57e-106">This section completes hello tutorial by deploying hello container tooAzure Container Instances.</span></span> <span data-ttu-id="db57e-107">Stappen voltooid omvatten:</span><span class="sxs-lookup"><span data-stu-id="db57e-107">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="db57e-108">Het definiëren van de containergroep van een met een Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="db57e-108">Defining a container group using an Azure Resource Manager template</span></span>
> * <span data-ttu-id="db57e-109">Hallo containergroep met behulp van Azure CLI Hallo implementeren</span><span class="sxs-lookup"><span data-stu-id="db57e-109">Deploying hello container group using hello Azure CLI</span></span>
> * <span data-ttu-id="db57e-110">Container-logboeken bekijken</span><span class="sxs-lookup"><span data-stu-id="db57e-110">Viewing container logs</span></span>

## <a name="deploy-hello-container-using-hello-azure-cli"></a><span data-ttu-id="db57e-111">Met behulp van Azure CLI Hallo Hallo-container implementeren</span><span class="sxs-lookup"><span data-stu-id="db57e-111">Deploy hello container using hello Azure CLI</span></span>

<span data-ttu-id="db57e-112">Hello Azure CLI kunt implementatie van een container tooAzure Containerexemplaren in één opdracht.</span><span class="sxs-lookup"><span data-stu-id="db57e-112">hello Azure CLI enables deployment of a container tooAzure Container Instances in a single command.</span></span> <span data-ttu-id="db57e-113">Aangezien Hallo container installatiekopie wordt gehost in Hallo persoonlijke Azure-Container register, moet u Hallo referenties vereist tooaccess opnemen deze.</span><span class="sxs-lookup"><span data-stu-id="db57e-113">Since hello container image is hosted in hello private Azure Container Registry, you must include hello credentials required tooaccess it.</span></span> <span data-ttu-id="db57e-114">Indien nodig, kunt u ze opvragen, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="db57e-114">If necessary, you can query them as shown below.</span></span>

<span data-ttu-id="db57e-115">Container register login-server (update met de registernaam van uw):</span><span class="sxs-lookup"><span data-stu-id="db57e-115">Container registry login server (update with your registry name):</span></span>

```azurecli-interactive
az acr show --name <acrName> --query loginServer
```

<span data-ttu-id="db57e-116">Container register wachtwoord:</span><span class="sxs-lookup"><span data-stu-id="db57e-116">Container registry password:</span></span>

```azurecli-interactive
az acr credential show --name <acrName> --query "passwords[0].value"
```

<span data-ttu-id="db57e-117">toodeploy gevraagd om uw installatiekopie container uit Hallo container register met een resource van 1 CPU-kern tot 1GB geheugen, Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="db57e-117">toodeploy your container image from hello container registry with a resource request of 1 CPU core and 1GB of memory, run hello following command:</span></span>

```azurecli-interactive
az container create --name aci-tutorial-app --image <acrLoginServer>/aci-tutorial-app:v1 --cpu 1 --memory 1 --registry-password <acrPassword> --ip-address public -g myResourceGroup
```

<span data-ttu-id="db57e-118">Binnen enkele seconden ontvangt u een eerste reactie van Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="db57e-118">Within a few seconds, you will receive an initial response from Azure Resource Manager.</span></span> <span data-ttu-id="db57e-119">tooview hello staat van Hallo-implementatie gebruiken:</span><span class="sxs-lookup"><span data-stu-id="db57e-119">tooview hello state of hello deployment, use:</span></span>

```azurecli-interactive
az container show --name aci-tutorial-app --resource-group myResourceGroup --query state
```

<span data-ttu-id="db57e-120">U kunt doorgaan met deze opdracht wordt uitgevoerd totdat Hallo status van verandert *in behandeling* te*met*.</span><span class="sxs-lookup"><span data-stu-id="db57e-120">We can continue running this command until hello state changes from *pending* too*running*.</span></span> <span data-ttu-id="db57e-121">Vervolgens kunnen we doorgaan.</span><span class="sxs-lookup"><span data-stu-id="db57e-121">Then we can proceed.</span></span>

## <a name="view-hello-application-and-container-logs"></a><span data-ttu-id="db57e-122">Hallo toepassings- en logboekbestanden weergeven</span><span class="sxs-lookup"><span data-stu-id="db57e-122">View hello application and container logs</span></span>

<span data-ttu-id="db57e-123">Zodra het Hallo-implementatie is gelukt, opent u uw browser toohello IP-adres wordt weergegeven in de uitvoer van de volgende opdracht Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="db57e-123">Once hello deployment succeeds, open your browser toohello IP address shown in hello output of hello following command:</span></span>

```bash
az container show --name aci-tutorial-app --resource-group myResourceGroup --query ipAddress.ip
```

```json
"13.88.176.27"
```

![Hallo wereld-app in Hallo-browser][aci-app-browser]

<span data-ttu-id="db57e-125">U kunt ook Hallo logboekuitvoer van Hallo container bekijken:</span><span class="sxs-lookup"><span data-stu-id="db57e-125">You can also view hello log output of hello container:</span></span>

```azurecli-interactive
az container logs --name aci-tutorial-app -g myResourceGroup
```

<span data-ttu-id="db57e-126">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="db57e-126">Output:</span></span>

```bash
listening on port 80
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://13.88.176.27/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="next-steps"></a><span data-ttu-id="db57e-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="db57e-127">Next steps</span></span>

<span data-ttu-id="db57e-128">In deze zelfstudie maakt voltooid u Hallo-proces voor het implementeren van uw containers tooAzure Containerexemplaren.</span><span class="sxs-lookup"><span data-stu-id="db57e-128">In this tutorial, you completed hello process of deploying your containers tooAzure Container Instances.</span></span> <span data-ttu-id="db57e-129">Hallo stappen zijn voltooid:</span><span class="sxs-lookup"><span data-stu-id="db57e-129">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="db57e-130">Hallo-container van het gebruik van hello Azure Container register implementeren hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="db57e-130">Deploying hello container from hello Azure Container Registry using hello Azure CLI</span></span>
> * <span data-ttu-id="db57e-131">Bekijkt hello toepassing in Hallo-browser</span><span class="sxs-lookup"><span data-stu-id="db57e-131">Viewing hello application in hello browser</span></span>
> * <span data-ttu-id="db57e-132">Weergave Hallo container Logboeken</span><span class="sxs-lookup"><span data-stu-id="db57e-132">Viewing hello container logs</span></span>

<!-- LINKS -->
[prepare-app]: ./container-instances-tutorial-prepare-app.md

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png
