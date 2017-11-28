---
title: aaaCreate uw eerste Azure-Containerexemplaren container | Azure Docs
description: Azure Container Instances implementeren en ermee aan de slag gaan
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: b57c52714933bd3b28c44d33f9af7cd1f23fb951
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-container-in-azure-container-instances"></a><span data-ttu-id="73b98-103">Uw eerste container maken in Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="73b98-103">Create your first container in Azure Container Instances</span></span>

<span data-ttu-id="73b98-104">Azure Containerexemplaren maakt het eenvoudig toocreate en beheer containers in Azure.</span><span class="sxs-lookup"><span data-stu-id="73b98-104">Azure Container Instances makes it easy toocreate and manage containers in Azure.</span></span> <span data-ttu-id="73b98-105">In deze snel starten, wordt u een container maken in Azure en maak deze toohello zichtbaar internet met een openbaar IP-adres.</span><span class="sxs-lookup"><span data-stu-id="73b98-105">In this quick start, you will create a container in Azure and expose it toohello internet with a public IP address.</span></span> <span data-ttu-id="73b98-106">Deze bewerking wordt uitgevoerd in één opdracht.</span><span class="sxs-lookup"><span data-stu-id="73b98-106">This operation is completed in a single command.</span></span> <span data-ttu-id="73b98-107">Binnen een paar seconden ziet u dit in uw browser:</span><span class="sxs-lookup"><span data-stu-id="73b98-107">Within just a few seconds, you will see this in your browser:</span></span>

![App die is geïmplementeerd met Azure Container Instances, weergegeven in de browser][aci-app-browser]

<span data-ttu-id="73b98-109">Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) aan voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="73b98-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="73b98-110">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, is deze snelstartgids vereist dat u de versie van de Azure CLI Hallo 2.0.12 worden uitgevoerd of hoger.</span><span class="sxs-lookup"><span data-stu-id="73b98-110">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.12 or later.</span></span> <span data-ttu-id="73b98-111">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="73b98-111">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="73b98-112">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="73b98-112">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="73b98-113">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="73b98-113">Create a resource group</span></span>

<span data-ttu-id="73b98-114">Azure Container Instances zijn Azure-resources en moeten worden geplaatst in een Azure-resourcegroep, een logische verzameling waarin Azure resources worden geïmplementeerd en beheerd.</span><span class="sxs-lookup"><span data-stu-id="73b98-114">Azure Container Instances are Azure resources and must be placed in an Azure resource group, a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="73b98-115">Een resourcegroep maken met de Hallo [az groep maken](/cli/azure/group#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="73b98-115">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> 

<span data-ttu-id="73b98-116">Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *eastus* locatie.</span><span class="sxs-lookup"><span data-stu-id="73b98-116">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-container"></a><span data-ttu-id="73b98-117">Een container maken</span><span class="sxs-lookup"><span data-stu-id="73b98-117">Create a container</span></span>

<span data-ttu-id="73b98-118">U kunt een container maken door een naam, een Docker-installatiekopie en een Azure-resourcegroep op te geven.</span><span class="sxs-lookup"><span data-stu-id="73b98-118">You can create a container by providing a name, a Docker image, and an Azure resource group.</span></span> <span data-ttu-id="73b98-119">Hallo container toohello kan eventueel worden blootgesteld internet met een openbaar IP-adres.</span><span class="sxs-lookup"><span data-stu-id="73b98-119">You can optionally expose hello container toohello internet with a public IP address.</span></span> <span data-ttu-id="73b98-120">We gebruiken in dit geval een container die als host fungeert voor een zeer eenvoudige web-app die is geschreven in [Node.js](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="73b98-120">In this case, we'll use a container that hosts a very simple web app written in [Node.js](http://nodejs.org).</span></span>

```azurecli-interactive
az container create --name mycontainer --image microsoft/aci-helloworld --resource-group myResourceGroup --ip-address public 
```

<span data-ttu-id="73b98-121">Binnen enkele seconden krijgt u een antwoord tooyour-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="73b98-121">Within a few seconds, you should get a response tooyour request.</span></span> <span data-ttu-id="73b98-122">In eerste instantie Hallo container zich in een **maken** staat, maar moet worden gestart binnen een paar seconden.</span><span class="sxs-lookup"><span data-stu-id="73b98-122">Initially, hello container will be in a **Creating** state, but it should start within a few seconds.</span></span> <span data-ttu-id="73b98-123">U kunt met behulp van Hallo Hallo-status controleren `show` opdracht:</span><span class="sxs-lookup"><span data-stu-id="73b98-123">You can check hello status using hello `show` command:</span></span>

```azurecli-interactive
az container show --name mycontainer --resource-group myResourceGroup
```

<span data-ttu-id="73b98-124">Aan de onderkant van de Hallo van Hallo uitvoer ziet u de Inrichtingsstatus Hallo-container en het IP-adres:</span><span class="sxs-lookup"><span data-stu-id="73b98-124">At hello bottom of hello output, you will see hello container's provisioning state and its IP address:</span></span>

```json
...
"ipAddress": {
      "ip": "13.88.8.148",
      "ports": [
        {
          "port": 80,
          "protocol": "TCP"
        }
      ]
    },
    "osType": "Linux",
    "provisioningState": "Succeeded"
...
```

<span data-ttu-id="73b98-125">Zodra het Hallo-container verplaatst toohello **geslaagd** staat, kunt u deze op Hallo browser Hallo IP-adres opgegeven bereiken.</span><span class="sxs-lookup"><span data-stu-id="73b98-125">Once hello container moves toohello **Succeeded** state, you can reach it in hello browser using hello IP address provided.</span></span> 

![App die is geïmplementeerd met Azure Container Instances, weergegeven in de browser][aci-app-browser]

## <a name="pull-hello-container-logs"></a><span data-ttu-id="73b98-127">Pull-hallo container Logboeken</span><span class="sxs-lookup"><span data-stu-id="73b98-127">Pull hello container logs</span></span>

<span data-ttu-id="73b98-128">U kunt pull-logboeken voor Hallo-container hebt gemaakt met behulp van Hallo Hallo `logs` opdracht:</span><span class="sxs-lookup"><span data-stu-id="73b98-128">You can pull hello logs for hello container you created using hello `logs` command:</span></span>

```azurecli-interactive
az container logs --name mycontainer --resource-group myResourceGroup
```

<span data-ttu-id="73b98-129">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="73b98-129">Output:</span></span>

```bash
listening on port 80
::ffff:10.240.255.105 - - [21/Jul/2017:00:01:46 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.255.105 - - [21/Jul/2017:00:01:46 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://104.210.39.122/" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="delete-hello-container"></a><span data-ttu-id="73b98-130">Hallo-container verwijderen</span><span class="sxs-lookup"><span data-stu-id="73b98-130">Delete hello container</span></span>

<span data-ttu-id="73b98-131">Wanneer u klaar bent met het Hallo-container, kunt u met behulp van Hallo verwijderen `delete` opdracht:</span><span class="sxs-lookup"><span data-stu-id="73b98-131">When you are done with hello container, you can remove it using hello `delete` command:</span></span>

```azurecli-interactive
az container delete --name mycontainer --resource-group myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="73b98-132">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="73b98-132">Next steps</span></span>

<span data-ttu-id="73b98-133">Alle Hallo code voor de Hallo container gebruikt in deze snel starten [op GitHub][app-github-repo], samen met de Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="73b98-133">All of hello code for hello container used in this quick start is available [on GitHub][app-github-repo], along with its Dockerfile.</span></span> <span data-ttu-id="73b98-134">Als u tootry zelf bouwen en implementeren van tooAzure Container-exemplaren die gebruikmaken van hello Azure Container register wilt, blijven toohello Azure Containerexemplaren zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="73b98-134">If you'd like tootry building it yourself and deploying it tooAzure Container Instances using hello Azure Container Registry, continue toohello Azure Container Instances tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="73b98-135">Zelfstudies voor Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="73b98-135">Azure Container Instances tutorials</span></span>](./container-instances-tutorial-prepare-app.md)


<!-- LINKS -->
[app-github-repo]: https://github.com/Azure-Samples/aci-helloworld.git

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png