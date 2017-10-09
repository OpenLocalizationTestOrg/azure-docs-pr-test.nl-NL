---
title: zelfstudie voor aaaAzure Container Service - ACR voorbereiden | Microsoft Docs
description: Zelfstudie voor Azure Container Service - ACR voorbereiden
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, Containers, Micro-services, Kubernetes, DC/OS, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/21/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 3980e5ce4eb9836f83c761a2f76c944bb3f13060
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-use-azure-container-registry"></a><span data-ttu-id="f6c06-104">Implementeren en gebruiken van Azure Container register</span><span class="sxs-lookup"><span data-stu-id="f6c06-104">Deploy and use Azure Container Registry</span></span>

<span data-ttu-id="f6c06-105">Azure Container register (ACR) is een register op basis van Azure, persoonlijke voor installatiekopieën van de Docker-container.</span><span class="sxs-lookup"><span data-stu-id="f6c06-105">Azure Container Registry (ACR) is an Azure-based, private registry, for Docker container images.</span></span> <span data-ttu-id="f6c06-106">Deze zelfstudie, deel uit van zeven, wordt begeleid bij het implementeren van een Azure Container register-exemplaar en een container installatiekopie tooit pushen.</span><span class="sxs-lookup"><span data-stu-id="f6c06-106">This tutorial, part two of seven, walks through deploying an Azure Container Registry instance, and pushing a container image tooit.</span></span> <span data-ttu-id="f6c06-107">Stappen voltooid omvatten:</span><span class="sxs-lookup"><span data-stu-id="f6c06-107">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f6c06-108">Implementatie van een exemplaar van Azure Container register (ACR)</span><span class="sxs-lookup"><span data-stu-id="f6c06-108">Deploying an Azure Container Registry (ACR) instance</span></span>
> * <span data-ttu-id="f6c06-109">Een installatiekopie van een container voor ACR-tagging</span><span class="sxs-lookup"><span data-stu-id="f6c06-109">Tagging a container image for ACR</span></span>
> * <span data-ttu-id="f6c06-110">Hallo installatiekopie tooACR uploaden</span><span class="sxs-lookup"><span data-stu-id="f6c06-110">Uploading hello image tooACR</span></span>

<span data-ttu-id="f6c06-111">In volgende zelfstudies is dit ACR-exemplaar geïntegreerd met een Azure Container Service Kubernetes-cluster voor het veilig uitvoeren van installatiekopieën van de container.</span><span class="sxs-lookup"><span data-stu-id="f6c06-111">In subsequent tutorials, this ACR instance is integrated with an Azure Container Service Kubernetes cluster, for securely running container images.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="f6c06-112">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="f6c06-112">Before you begin</span></span>

<span data-ttu-id="f6c06-113">In Hallo [vorige zelfstudie](./container-service-tutorial-kubernetes-prepare-app.md), een installatiekopie van een container voor een eenvoudige toepassing voor Azure uw stem is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f6c06-113">In hello [previous tutorial](./container-service-tutorial-kubernetes-prepare-app.md), a container image was created for a simple Azure Voting application.</span></span> <span data-ttu-id="f6c06-114">In deze zelfstudie wordt deze installatiekopie tooan Azure Container register gepusht.</span><span class="sxs-lookup"><span data-stu-id="f6c06-114">In this tutorial, this image is pushed tooan Azure Container Registry.</span></span> <span data-ttu-id="f6c06-115">Als u geen hello Azure stemmen app installatiekopie hebt gemaakt, te retourneren[zelfstudie 1 – installatiekopieën van de container maken](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="f6c06-115">If you have not created hello Azure Voting app image, return too[Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> <span data-ttu-id="f6c06-116">U kunt ook gedetailleerde Hallo stappen hier werken met een installatiekopie van de container.</span><span class="sxs-lookup"><span data-stu-id="f6c06-116">Alternatively, hello steps detailed here work with any container image.</span></span>

<span data-ttu-id="f6c06-117">Deze zelfstudie vereist dat u de versie van de Azure CLI Hallo 2.0.4 worden uitgevoerd of hoger.</span><span class="sxs-lookup"><span data-stu-id="f6c06-117">This tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="f6c06-118">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="f6c06-118">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="f6c06-119">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f6c06-119">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="deploy-azure-container-registry"></a><span data-ttu-id="f6c06-120">Register met Azure Container implementeren</span><span class="sxs-lookup"><span data-stu-id="f6c06-120">Deploy Azure Container Registry</span></span>

<span data-ttu-id="f6c06-121">Wanneer u een Azure Container Registry implementeert, moet u eerst een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="f6c06-121">When deploying an Azure Container Registry, you first need a resource group.</span></span> <span data-ttu-id="f6c06-122">Een Azure-resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd.</span><span class="sxs-lookup"><span data-stu-id="f6c06-122">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="f6c06-123">Een resourcegroep maken met de Hallo [az groep maken](/cli/azure/group#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="f6c06-123">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="f6c06-124">In dit voorbeeld wordt een resourcegroep met de naam *myResourceGroup* wordt gemaakt in Hallo *westeurope* regio.</span><span class="sxs-lookup"><span data-stu-id="f6c06-124">In this example, a resource group named *myResourceGroup* is created in hello *westeurope* region.</span></span>

```azurecli
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="f6c06-125">Maken van een Azure-Container registry Hello [az acr maken](/cli/azure/acr#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="f6c06-125">Create an Azure Container registry with hello [az acr create](/cli/azure/acr#create) command.</span></span> <span data-ttu-id="f6c06-126">Hallo-naam van een registersleutel Container **moeten uniek zijn**.</span><span class="sxs-lookup"><span data-stu-id="f6c06-126">hello name of a Container Registry **must be unique**.</span></span>

```azurecli
az acr create --resource-group myResourceGroup --name <acrName> --sku Basic --admin-enabled true
```

<span data-ttu-id="f6c06-127">In Hallo rest van deze zelfstudie gebruiken we 'acrname' als tijdelijke aanduiding voor Hallo register containernaam die u hebt gekozen.</span><span class="sxs-lookup"><span data-stu-id="f6c06-127">Throughout hello rest of this tutorial, we use "acrname" as a placeholder for hello container registry name that you chose.</span></span>

## <a name="container-registry-login"></a><span data-ttu-id="f6c06-128">Container register aanmelding</span><span class="sxs-lookup"><span data-stu-id="f6c06-128">Container registry login</span></span>

<span data-ttu-id="f6c06-129">U moet tooyour ACR exemplaar aanmelden voordat u installatiekopieën tooit.</span><span class="sxs-lookup"><span data-stu-id="f6c06-129">You must log in tooyour ACR instance before pushing images tooit.</span></span> <span data-ttu-id="f6c06-130">Gebruik Hallo [az acr aanmelding](https://docs.microsoft.com/en-us/cli/azure/acr#login) opdracht toocomplete Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="f6c06-130">Use hello [az acr login](https://docs.microsoft.com/en-us/cli/azure/acr#login) command toocomplete hello operation.</span></span> <span data-ttu-id="f6c06-131">U moet tooprovide Hallo unieke naam toohello container register opgegeven toen deze werd gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f6c06-131">You need tooprovide hello unique name given toohello container registry when it was created.</span></span>

```azurecli
az acr login --name <acrName>
```

<span data-ttu-id="f6c06-132">Hallo opdracht retourneert een bericht 'Aanmelding geslaagd' eenmaal is voltooid.</span><span class="sxs-lookup"><span data-stu-id="f6c06-132">hello command returns a 'Login Succeeded’ message once completed.</span></span>

## <a name="tag-container-images"></a><span data-ttu-id="f6c06-133">Installatiekopieën van de tag-container</span><span class="sxs-lookup"><span data-stu-id="f6c06-133">Tag container images</span></span>

<span data-ttu-id="f6c06-134">Elke container installatiekopie moet toobe gemarkeerd met de Hallo loginServer naam van Hallo-register.</span><span class="sxs-lookup"><span data-stu-id="f6c06-134">Each container image needs toobe tagged with hello loginServer name of hello registry.</span></span> <span data-ttu-id="f6c06-135">Deze code wordt gebruikt voor routering wanneer container installatiekopieën tooan installatiekopie register worden gepusht.</span><span class="sxs-lookup"><span data-stu-id="f6c06-135">This tag is used for routing when pushing container images tooan image registry.</span></span>

<span data-ttu-id="f6c06-136">een lijst met huidige installatiekopieën, gebruik Hallo toosee [docker-installatiekopieën](https://docs.docker.com/engine/reference/commandline/images/) opdracht.</span><span class="sxs-lookup"><span data-stu-id="f6c06-136">toosee a list of current images, use hello [docker images](https://docs.docker.com/engine/reference/commandline/images/) command.</span></span>

```bash
docker images
```

<span data-ttu-id="f6c06-137">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="f6c06-137">Output:</span></span>

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front             latest              4675398c9172        13 minutes ago      694MB
redis                        latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask               788ca94b2313        9 months ago        694MB
```

<span data-ttu-id="f6c06-138">tooget hello loginServer naam, Hallo volgende opdracht uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f6c06-138">tooget hello loginServer name, run hello following command.</span></span>

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

<span data-ttu-id="f6c06-139">Nu tag Hallo *azure stem voorgrond* installatiekopie met de Hallo loginServer van Hallo container register.</span><span class="sxs-lookup"><span data-stu-id="f6c06-139">Now, tag hello *azure-vote-front* image with hello loginServer of hello container registry.</span></span> <span data-ttu-id="f6c06-140">Ook toe te voegen `:redis-v1` toohello einde van de naam van de installatiekopie Hallo.</span><span class="sxs-lookup"><span data-stu-id="f6c06-140">Also, add `:redis-v1` toohello end of hello image name.</span></span> <span data-ttu-id="f6c06-141">Deze code geeft Hallo installatiekopie versie.</span><span class="sxs-lookup"><span data-stu-id="f6c06-141">This tag indicates hello image version.</span></span>

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v1
```

<span data-ttu-id="f6c06-142">Wanneer gecodeerd, uitvoeren [docker afbeeldingen] (https://docs.docker.com/engine/reference/commandline/images/) tooverify Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="f6c06-142">Once tagged, run [docker images] (https://docs.docker.com/engine/reference/commandline/images/) tooverify hello operation.</span></span>

```bash
docker images
```

<span data-ttu-id="f6c06-143">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="f6c06-143">Output:</span></span>

```bash
REPOSITORY                                           TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front                                     latest              eaf2b9c57e5e        8 minutes ago       716 MB
mycontainerregistry082.azurecr.io/azure-vote-front   redis-v1            eaf2b9c57e5e        8 minutes ago       716 MB
redis                                                latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask                           flask               788ca94b2313        8 months ago        694 MB
```

## <a name="push-images-tooregistry"></a><span data-ttu-id="f6c06-144">Afbeeldingen tooregistry push</span><span class="sxs-lookup"><span data-stu-id="f6c06-144">Push images tooregistry</span></span>

<span data-ttu-id="f6c06-145">Hallo push *azure stem voorgrond* installatiekopie toohello register.</span><span class="sxs-lookup"><span data-stu-id="f6c06-145">Push hello *azure-vote-front* image toohello registry.</span></span> 

<span data-ttu-id="f6c06-146">Hallo volgende voorbeeld gebruikt, vervangen door Hallo ACR loginServer naam Hallo loginServer uit uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="f6c06-146">Using hello following example, replace hello ACR loginServer name with hello loginServer from your environment.</span></span>

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v1
```

<span data-ttu-id="f6c06-147">Dit duurt enkele minuten toocomplete.</span><span class="sxs-lookup"><span data-stu-id="f6c06-147">This takes a couple of minutes toocomplete.</span></span>

## <a name="list-images-in-registry"></a><span data-ttu-id="f6c06-148">Lijst met afbeeldingen in register</span><span class="sxs-lookup"><span data-stu-id="f6c06-148">List images in registry</span></span>

<span data-ttu-id="f6c06-149">een lijst met afbeeldingen die een pushbericht hebben ontvangen tooyour Azure-Container register, gebruiker Hallo tooreturn [az acr opslagplaats lijst](/cli/azure/acr/repository#list) opdracht.</span><span class="sxs-lookup"><span data-stu-id="f6c06-149">tooreturn a list of images that have been pushed tooyour Azure Container registry, user hello [az acr repository list](/cli/azure/acr/repository#list) command.</span></span> <span data-ttu-id="f6c06-150">Hallo opdracht bijwerken met Hallo ACR-exemplaarnaam.</span><span class="sxs-lookup"><span data-stu-id="f6c06-150">Update hello command with hello ACR instance name.</span></span>

```azurecli
az acr repository list --name <acrName> --output table
```

<span data-ttu-id="f6c06-151">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="f6c06-151">Output:</span></span>

```azurecli
Result
----------------
azure-vote-front
```

<span data-ttu-id="f6c06-152">En vervolgens toosee Hallo labels voor een specifieke installatiekopie Hallo [az acr opslagplaats weergeven-labels](/cli/azure/acr/repository#show-tags) opdracht.</span><span class="sxs-lookup"><span data-stu-id="f6c06-152">And then toosee hello tags for a specific image, use hello [az acr repository show-tags](/cli/azure/acr/repository#show-tags) command.</span></span>

```azurecli
az acr repository show-tags --name <acrName> --repository azure-vote-front --output table
```

<span data-ttu-id="f6c06-153">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="f6c06-153">Output:</span></span>

```azurecli
Result
--------
redis-v1
```

<span data-ttu-id="f6c06-154">Bij zelfstudie voltooien is Hallo container installatiekopie opgeslagen in een persoonlijke Azure-Container register-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="f6c06-154">At tutorial completion, hello container image has been stored in a private Azure Container Registry instance.</span></span> <span data-ttu-id="f6c06-155">Deze installatiekopie is in volgende zelfstudies uit ACR tooa Kubernetes cluster geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="f6c06-155">This image is deployed from ACR tooa Kubernetes cluster in subsequent tutorials.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6c06-156">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f6c06-156">Next steps</span></span>

<span data-ttu-id="f6c06-157">In deze zelfstudie is een Azure Container Registry voorbereid voor gebruik in een cluster ACS Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="f6c06-157">In this tutorial, an Azure Container Registry was prepared for use in an ACS Kubernetes cluster.</span></span> <span data-ttu-id="f6c06-158">Hallo stappen zijn voltooid:</span><span class="sxs-lookup"><span data-stu-id="f6c06-158">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f6c06-159">Een exemplaar van het register van Azure-Container geïmplementeerd</span><span class="sxs-lookup"><span data-stu-id="f6c06-159">Deployed an Azure Container Registry instance</span></span>
> * <span data-ttu-id="f6c06-160">Een installatiekopie van een container voor ACR met tags</span><span class="sxs-lookup"><span data-stu-id="f6c06-160">Tagged a container image for ACR</span></span>
> * <span data-ttu-id="f6c06-161">Geüploade Hallo installatiekopie tooACR</span><span class="sxs-lookup"><span data-stu-id="f6c06-161">Uploaded hello image tooACR</span></span>

<span data-ttu-id="f6c06-162">Ga toohello volgende zelfstudie toolearn over het implementeren van een cluster Kubernetes in Azure.</span><span class="sxs-lookup"><span data-stu-id="f6c06-162">Advance toohello next tutorial toolearn about deploying a Kubernetes cluster in Azure.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f6c06-163">Kubernetes-cluster implementeren</span><span class="sxs-lookup"><span data-stu-id="f6c06-163">Deploy Kubernetes cluster</span></span>](./container-service-tutorial-kubernetes-deploy-cluster.md)