---
title: Uw eerste Azure Container Instances-container maken | Azure Docs
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
ms.openlocfilehash: 905f69e5e1e237a31d9bb1e326969ec83292c244
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="create-your-first-container-in-azure-container-instances"></a><span data-ttu-id="756d9-103">Uw eerste container maken in Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="756d9-103">Create your first container in Azure Container Instances</span></span>

<span data-ttu-id="756d9-104">Met Azure Container Instances kunt u eenvoudig containers maken en beheren in Azure.</span><span class="sxs-lookup"><span data-stu-id="756d9-104">Azure Container Instances makes it easy to create and manage containers in Azure.</span></span> <span data-ttu-id="756d9-105">In deze snelstartgids maakt u een container in Azure en geeft u deze op internet weer met een openbaar IP-adres.</span><span class="sxs-lookup"><span data-stu-id="756d9-105">In this quick start, you will create a container in Azure and expose it to the internet with a public IP address.</span></span> <span data-ttu-id="756d9-106">Deze bewerking wordt uitgevoerd in één opdracht.</span><span class="sxs-lookup"><span data-stu-id="756d9-106">This operation is completed in a single command.</span></span> <span data-ttu-id="756d9-107">Binnen een paar seconden ziet u dit in uw browser:</span><span class="sxs-lookup"><span data-stu-id="756d9-107">Within just a few seconds, you will see this in your browser:</span></span>

![App die is geïmplementeerd met Azure Container Instances, weergegeven in de browser][aci-app-browser]

<span data-ttu-id="756d9-109">Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) aan voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="756d9-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="756d9-110">Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u voor deze snelstartgids gebruikmaken van Azure CLI versie 2.0.12 of hoger.</span><span class="sxs-lookup"><span data-stu-id="756d9-110">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.12 or later.</span></span> <span data-ttu-id="756d9-111">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="756d9-111">Run `az --version` to find the version.</span></span> <span data-ttu-id="756d9-112">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="756d9-112">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="756d9-113">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="756d9-113">Create a resource group</span></span>

<span data-ttu-id="756d9-114">Azure Container Instances zijn Azure-resources en moeten worden geplaatst in een Azure-resourcegroep, een logische verzameling waarin Azure resources worden geïmplementeerd en beheerd.</span><span class="sxs-lookup"><span data-stu-id="756d9-114">Azure Container Instances are Azure resources and must be placed in an Azure resource group, a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="756d9-115">Een resourcegroep maken met de opdracht [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="756d9-115">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> 

<span data-ttu-id="756d9-116">In het volgende voorbeeld wordt een resourcegroep met de naam *myResourceGroup* gemaakt op de locatie *VS Oost*.</span><span class="sxs-lookup"><span data-stu-id="756d9-116">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-container"></a><span data-ttu-id="756d9-117">Een container maken</span><span class="sxs-lookup"><span data-stu-id="756d9-117">Create a container</span></span>

<span data-ttu-id="756d9-118">U kunt een container maken door een naam, een Docker-installatiekopie en een Azure-resourcegroep op te geven.</span><span class="sxs-lookup"><span data-stu-id="756d9-118">You can create a container by providing a name, a Docker image, and an Azure resource group.</span></span> <span data-ttu-id="756d9-119">U kunt de container desgewenst weergeven op internet met een openbaar IP-adres.</span><span class="sxs-lookup"><span data-stu-id="756d9-119">You can optionally expose the container to the internet with a public IP address.</span></span> <span data-ttu-id="756d9-120">We gebruiken in dit geval een container die als host fungeert voor een zeer eenvoudige web-app die is geschreven in [Node.js](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="756d9-120">In this case, we'll use a container that hosts a very simple web app written in [Node.js](http://nodejs.org).</span></span>

```azurecli-interactive
az container create --name mycontainer --image microsoft/aci-helloworld --resource-group myResourceGroup --ip-address public 
```

<span data-ttu-id="756d9-121">Binnen enkele seconden krijgt u een reactie op uw aanvraag.</span><span class="sxs-lookup"><span data-stu-id="756d9-121">Within a few seconds, you should get a response to your request.</span></span> <span data-ttu-id="756d9-122">In eerste instantie heeft de container de status **Maken** staat, maar deze moet binnen een paar seconden starten.</span><span class="sxs-lookup"><span data-stu-id="756d9-122">Initially, the container will be in a **Creating** state, but it should start within a few seconds.</span></span> <span data-ttu-id="756d9-123">U kunt de status controleren met de opdracht `show`:</span><span class="sxs-lookup"><span data-stu-id="756d9-123">You can check the status using the `show` command:</span></span>

```azurecli-interactive
az container show --name mycontainer --resource-group myResourceGroup
```

<span data-ttu-id="756d9-124">Aan de onderkant van de uitvoer ziet u de inrichtingsstatus en het IP-adres van de container:</span><span class="sxs-lookup"><span data-stu-id="756d9-124">At the bottom of the output, you will see the container's provisioning state and its IP address:</span></span>

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

<span data-ttu-id="756d9-125">Als de container de status **Voltooid** heeft, u kunt deze benaderen in de browser met behulp van het opgegeven IP-adres.</span><span class="sxs-lookup"><span data-stu-id="756d9-125">Once the container moves to the **Succeeded** state, you can reach it in the browser using the IP address provided.</span></span> 

![App die is geïmplementeerd met Azure Container Instances, weergegeven in de browser][aci-app-browser]

## <a name="pull-the-container-logs"></a><span data-ttu-id="756d9-127">De containerlogboeken ophalen</span><span class="sxs-lookup"><span data-stu-id="756d9-127">Pull the container logs</span></span>

<span data-ttu-id="756d9-128">U kunt de logboeken voor de container die u hebt gemaakt ophalen met de opdracht `logs`:</span><span class="sxs-lookup"><span data-stu-id="756d9-128">You can pull the logs for the container you created using the `logs` command:</span></span>

```azurecli-interactive
az container logs --name mycontainer --resource-group myResourceGroup
```

<span data-ttu-id="756d9-129">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="756d9-129">Output:</span></span>

```bash
listening on port 80
::ffff:10.240.255.105 - - [21/Jul/2017:00:01:46 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.255.105 - - [21/Jul/2017:00:01:46 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://104.210.39.122/" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="delete-the-container"></a><span data-ttu-id="756d9-130">De container verwijderen</span><span class="sxs-lookup"><span data-stu-id="756d9-130">Delete the container</span></span>

<span data-ttu-id="756d9-131">Wanneer u klaar bent met de container, kunt u deze verwijderen met behulp van de opdracht `delete`:</span><span class="sxs-lookup"><span data-stu-id="756d9-131">When you are done with the container, you can remove it using the `delete` command:</span></span>

```azurecli-interactive
az container delete --name mycontainer --resource-group myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="756d9-132">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="756d9-132">Next steps</span></span>

<span data-ttu-id="756d9-133">Alle code voor de container die wordt gebruikt in deze snelstartgids is beschikbaar [op GitHub][app-github-repo], samen met het Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="756d9-133">All of the code for the container used in this quick start is available [on GitHub][app-github-repo], along with its Dockerfile.</span></span> <span data-ttu-id="756d9-134">Als u wilt proberen om deze zelf te bouwen en te implementeren in Azure Container Instances met behulp van het Azure Container Registry, gaat u verder met de zelfstudie van Azure Container Instances.</span><span class="sxs-lookup"><span data-stu-id="756d9-134">If you'd like to try building it yourself and deploying it to Azure Container Instances using the Azure Container Registry, continue to the Azure Container Instances tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="756d9-135">Zelfstudies voor Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="756d9-135">Azure Container Instances tutorials</span></span>](./container-instances-tutorial-prepare-app.md)


<!-- LINKS -->
[app-github-repo]: https://github.com/Azure-Samples/aci-helloworld.git

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png