---
title: aaaAzure Containerexemplaren zelfstudie - Azure-Container register voorbereiden | Microsoft Docs
description: Zelfstudie voor Azure Containerexemplaren - register van Azure-Container voorbereiden
services: container-instances
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, Containers, Micro-services, Kubernetes, DC/OS, Azure
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 2525626125740c3c861fad36aad207d0b587ff54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-use-azure-container-registry"></a><span data-ttu-id="5f42c-104">Implementeren en gebruiken van Azure Container register</span><span class="sxs-lookup"><span data-stu-id="5f42c-104">Deploy and use Azure Container Registry</span></span>

<span data-ttu-id="5f42c-105">Dit maakt deel uit van een zelfstudie drie delen.</span><span class="sxs-lookup"><span data-stu-id="5f42c-105">This is part two of a three-part tutorial.</span></span> <span data-ttu-id="5f42c-106">In Hallo [vorige stap](./container-instances-tutorial-prepare-app.md), een installatiekopie van een container is gemaakt voor een eenvoudige webtoepassing geschreven in [Node.js](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="5f42c-106">In hello [previous step](./container-instances-tutorial-prepare-app.md), a container image was created for a simple web application written in [Node.js](http://nodejs.org).</span></span> <span data-ttu-id="5f42c-107">In deze zelfstudie wordt deze installatiekopie tooan Azure Container register gepusht.</span><span class="sxs-lookup"><span data-stu-id="5f42c-107">In this tutorial, this image is pushed tooan Azure Container Registry.</span></span> <span data-ttu-id="5f42c-108">Als u geen Hallo container installatiekopie hebt gemaakt, te retourneren[zelfstudie 1 – afbeelding van de container maken](./container-instances-tutorial-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="5f42c-108">If you have not created hello container image, return too[Tutorial 1 – Create container image](./container-instances-tutorial-prepare-app.md).</span></span> 

<span data-ttu-id="5f42c-109">Hello Azure Container register is een register op basis van Azure, persoonlijke voor installatiekopieën van de Docker-container.</span><span class="sxs-lookup"><span data-stu-id="5f42c-109">hello Azure Container Registry is an Azure-based, private registry, for Docker container images.</span></span> <span data-ttu-id="5f42c-110">Deze zelfstudie wordt begeleid bij het implementeren van een Azure Container register-exemplaar en een container installatiekopie tooit pushen.</span><span class="sxs-lookup"><span data-stu-id="5f42c-110">This tutorial walks through deploying an Azure Container Registry instance, and pushing a container image tooit.</span></span> <span data-ttu-id="5f42c-111">Stappen voltooid omvatten:</span><span class="sxs-lookup"><span data-stu-id="5f42c-111">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5f42c-112">Een exemplaar van Azure Container register implementeren</span><span class="sxs-lookup"><span data-stu-id="5f42c-112">Deploying an Azure Container Registry instance</span></span>
> * <span data-ttu-id="5f42c-113">Afbeelding van de container voor Azure Container register tagging</span><span class="sxs-lookup"><span data-stu-id="5f42c-113">Tagging container image for Azure Container Registry</span></span>
> * <span data-ttu-id="5f42c-114">Afbeelding tooAzure Container register uploaden</span><span class="sxs-lookup"><span data-stu-id="5f42c-114">Uploading image tooAzure Container Registry</span></span>

<span data-ttu-id="5f42c-115">In volgende zelfstudies leert implementeren u Hallo container van uw persoonlijke register tooAzure Containerexemplaren.</span><span class="sxs-lookup"><span data-stu-id="5f42c-115">In subsequent tutorials, you deploy hello container from your private registry tooAzure Container Instances.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="5f42c-116">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="5f42c-116">Before you begin</span></span>

<span data-ttu-id="5f42c-117">Deze zelfstudie vereist dat u de versie van de Azure CLI Hallo 2.0.4 worden uitgevoerd of hoger.</span><span class="sxs-lookup"><span data-stu-id="5f42c-117">This tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="5f42c-118">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="5f42c-118">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="5f42c-119">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="5f42c-119">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="deploy-azure-container-registry"></a><span data-ttu-id="5f42c-120">Register met Azure Container implementeren</span><span class="sxs-lookup"><span data-stu-id="5f42c-120">Deploy Azure Container Registry</span></span>

<span data-ttu-id="5f42c-121">Wanneer u een Azure Container Registry implementeert, moet u eerst een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="5f42c-121">When deploying an Azure Container Registry, you first need a resource group.</span></span> <span data-ttu-id="5f42c-122">Een Azure-resourcegroep is een logische verzameling in welke Azure resources worden geïmplementeerd en beheerd.</span><span class="sxs-lookup"><span data-stu-id="5f42c-122">An Azure resource group is a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="5f42c-123">Een resourcegroep maken met de Hallo [az groep maken](/cli/azure/group#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="5f42c-123">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="5f42c-124">In dit voorbeeld wordt een resourcegroep met de naam *myResourceGroup* wordt gemaakt in Hallo *eastus* regio.</span><span class="sxs-lookup"><span data-stu-id="5f42c-124">In this example, a resource group named *myResourceGroup* is created in hello *eastus* region.</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="5f42c-125">Maken van een Azure-Container registry Hello [az acr maken](/cli/azure/acr#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="5f42c-125">Create an Azure Container registry with hello [az acr create](/cli/azure/acr#create) command.</span></span> <span data-ttu-id="5f42c-126">Hallo-naam van een registersleutel Container **moeten uniek zijn**.</span><span class="sxs-lookup"><span data-stu-id="5f42c-126">hello name of a Container Registry **must be unique**.</span></span> <span data-ttu-id="5f42c-127">In Hallo voorbeeld te volgen, gebruiken we de naam van de Hallo *mycontainerregistry082*.</span><span class="sxs-lookup"><span data-stu-id="5f42c-127">In hello following example, we use hello name *mycontainerregistry082*.</span></span>

```azurecli
az acr create --resource-group myResourceGroup --name mycontainerregistry082 --sku Basic --admin-enabled true
```

<span data-ttu-id="5f42c-128">In de rest van de Hallo van deze zelfstudie, gebruiken we `<acrname>` als tijdelijke aanduiding voor Hallo register containernaam die u hebt gekozen.</span><span class="sxs-lookup"><span data-stu-id="5f42c-128">Throughout hello rest of this tutorial, we use `<acrname>` as a placeholder for hello container registry name that you chose.</span></span>

## <a name="container-registry-login"></a><span data-ttu-id="5f42c-129">Container register aanmelding</span><span class="sxs-lookup"><span data-stu-id="5f42c-129">Container registry login</span></span>

<span data-ttu-id="5f42c-130">U moet tooyour ACR exemplaar aanmelden voordat u installatiekopieën tooit.</span><span class="sxs-lookup"><span data-stu-id="5f42c-130">You must log in tooyour ACR instance before pushing images tooit.</span></span> <span data-ttu-id="5f42c-131">Gebruik Hallo [az acr aanmelding](https://docs.microsoft.com/en-us/cli/azure/acr#login) opdracht toocomplete Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="5f42c-131">Use hello [az acr login](https://docs.microsoft.com/en-us/cli/azure/acr#login) command toocomplete hello operation.</span></span> <span data-ttu-id="5f42c-132">U moet tooprovide Hallo unieke naam toohello container register opgegeven toen deze werd gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5f42c-132">You need tooprovide hello unique name given toohello container registry when it was created.</span></span>

```azurecli
az acr login --name <acrName>
```

<span data-ttu-id="5f42c-133">Hallo opdracht retourneert een bericht 'Aanmelding geslaagd' eenmaal is voltooid.</span><span class="sxs-lookup"><span data-stu-id="5f42c-133">hello command returns a 'Login Succeeded’ message once completed.</span></span>

## <a name="tag-container-image"></a><span data-ttu-id="5f42c-134">De installatiekopie van de tag-container</span><span class="sxs-lookup"><span data-stu-id="5f42c-134">Tag container image</span></span>

<span data-ttu-id="5f42c-135">de installatiekopie van een container van een persoonlijke register toodeploy, Hallo installatiekopie moet toobe gemarkeerd met de Hallo `loginServer` naam van het Hallo-register.</span><span class="sxs-lookup"><span data-stu-id="5f42c-135">toodeploy a container image from a private registry, hello image needs toobe tagged with hello `loginServer` name of hello registry.</span></span>

<span data-ttu-id="5f42c-136">een lijst met huidige installatiekopieën, gebruik Hallo toosee `docker images` opdracht.</span><span class="sxs-lookup"><span data-stu-id="5f42c-136">toosee a list of current images, use hello `docker images` command.</span></span>

```bash
docker images
```

<span data-ttu-id="5f42c-137">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="5f42c-137">Output:</span></span>

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

<span data-ttu-id="5f42c-138">tooget hello loginServer naam, Hallo volgende opdracht uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="5f42c-138">tooget hello loginServer name, run hello following command.</span></span>

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

<span data-ttu-id="5f42c-139">Tag Hallo *aci-zelfstudie-app* installatiekopie met de Hallo loginServer van Hallo container register.</span><span class="sxs-lookup"><span data-stu-id="5f42c-139">Tag hello *aci-tutorial-app* image with hello loginServer of hello container registry.</span></span> <span data-ttu-id="5f42c-140">Ook toe te voegen `:v1` toohello einde van de naam van de installatiekopie Hallo.</span><span class="sxs-lookup"><span data-stu-id="5f42c-140">Also, add `:v1` toohello end of hello image name.</span></span> <span data-ttu-id="5f42c-141">Deze code geeft Hallo installatiekopie-versienummer.</span><span class="sxs-lookup"><span data-stu-id="5f42c-141">This tag indicates hello image version number.</span></span>

```bash
docker tag aci-tutorial-app <acrLoginServer>/aci-tutorial-app:v1
```

<span data-ttu-id="5f42c-142">Uitvoeren zodra gecodeerd, `docker images` tooverify Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="5f42c-142">Once tagged, run `docker images` tooverify hello operation.</span></span>

```bash
docker images
```

<span data-ttu-id="5f42c-143">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="5f42c-143">Output:</span></span>

```bash
REPOSITORY                                                TAG                 IMAGE ID            CREATED             SIZE
aci-tutorial-app                                          latest              5c745774dfa9        39 seconds ago      68.1 MB
mycontainerregistry082.azurecr.io/aci-tutorial-app        v1                  a9dace4e1a17        7 minutes ago       68.1 MB
```

## <a name="push-image-tooazure-container-registry"></a><span data-ttu-id="5f42c-144">Afbeelding tooAzure Container register push</span><span class="sxs-lookup"><span data-stu-id="5f42c-144">Push image tooAzure Container Registry</span></span>

<span data-ttu-id="5f42c-145">Hallo push *aci-zelfstudie-app* installatiekopie toohello register.</span><span class="sxs-lookup"><span data-stu-id="5f42c-145">Push hello *aci-tutorial-app* image toohello registry.</span></span>

<span data-ttu-id="5f42c-146">Hallo volgende voorbeeld gebruikt, vervangen door register Hallo-loginServer containernaam Hallo loginServer uit uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="5f42c-146">Using hello following example, replace hello container registry loginServer name with hello loginServer from your environment.</span></span>

```bash
docker push <acrLoginServer>/aci-tutorial-app:v1
```

## <a name="list-images-in-azure-container-registry"></a><span data-ttu-id="5f42c-147">Lijst met afbeeldingen in Azure Container register</span><span class="sxs-lookup"><span data-stu-id="5f42c-147">List images in Azure Container Registry</span></span>

<span data-ttu-id="5f42c-148">een lijst met afbeeldingen die een pushbericht hebben ontvangen tooyour Azure-Container register, gebruiker Hallo tooreturn [az acr opslagplaats lijst](/cli/azure/acr/repository#list) opdracht.</span><span class="sxs-lookup"><span data-stu-id="5f42c-148">tooreturn a list of images that have been pushed tooyour Azure Container registry, user hello [az acr repository list](/cli/azure/acr/repository#list) command.</span></span> <span data-ttu-id="5f42c-149">Hallo opdracht bijwerken met de containernaam register Hallo.</span><span class="sxs-lookup"><span data-stu-id="5f42c-149">Update hello command with hello container registry name.</span></span>

```azurecli
az acr repository list --name <acrName> --output table
```

<span data-ttu-id="5f42c-150">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="5f42c-150">Output:</span></span>

```azurecli
Result
----------------
aci-tutorial-app
```

<span data-ttu-id="5f42c-151">En vervolgens toosee Hallo labels voor een specifieke installatiekopie Hallo [az acr opslagplaats weergeven-labels](/cli/azure/acr/repository#show-tags) opdracht.</span><span class="sxs-lookup"><span data-stu-id="5f42c-151">And then toosee hello tags for a specific image, use hello [az acr repository show-tags](/cli/azure/acr/repository#show-tags) command.</span></span>

```azurecli
az acr repository show-tags --name <acrName> --repository aci-tutorial-app --output table
```

<span data-ttu-id="5f42c-152">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="5f42c-152">Output:</span></span>

```azurecli
Result
--------
v1
```

## <a name="next-steps"></a><span data-ttu-id="5f42c-153">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5f42c-153">Next steps</span></span>

<span data-ttu-id="5f42c-154">In deze zelfstudie een Azure Container Registry is voorbereid voor gebruik met Azure Containerexemplaren en Hallo container installatiekopie is gepusht.</span><span class="sxs-lookup"><span data-stu-id="5f42c-154">In this tutorial, an Azure Container Registry was prepared for use with Azure Container Instances, and hello container image was pushed.</span></span> <span data-ttu-id="5f42c-155">Hallo stappen zijn voltooid:</span><span class="sxs-lookup"><span data-stu-id="5f42c-155">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5f42c-156">Een exemplaar van Azure Container register implementeren</span><span class="sxs-lookup"><span data-stu-id="5f42c-156">Deploying an Azure Container Registry instance</span></span>
> * <span data-ttu-id="5f42c-157">Afbeelding van de container voor Azure Container register tagging</span><span class="sxs-lookup"><span data-stu-id="5f42c-157">Tagging container image for Azure Container Registry</span></span>
> * <span data-ttu-id="5f42c-158">Afbeelding tooAzure Container register uploaden</span><span class="sxs-lookup"><span data-stu-id="5f42c-158">Uploading image tooAzure Container Registry</span></span>

<span data-ttu-id="5f42c-159">Toohello volgende zelfstudie toolearn over het implementeren van Hallo container tooAzure met Azure Container instanties gaan.</span><span class="sxs-lookup"><span data-stu-id="5f42c-159">Advance toohello next tutorial toolearn about deploying hello container tooAzure using Azure Container Instances.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5f42c-160">Containers tooAzure Containerexemplaren implementeren</span><span class="sxs-lookup"><span data-stu-id="5f42c-160">Deploy containers tooAzure Container Instances</span></span>](./container-instances-tutorial-deploy-app.md)
