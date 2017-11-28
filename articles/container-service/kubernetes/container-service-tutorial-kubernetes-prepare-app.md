---
title: zelfstudie voor aaaAzure Container Service - App voorbereiden | Microsoft Docs
description: Zelfstudie voor Azure Container Service - App voorbereiden
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
ms.date: 07/25/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b537ecc9ff50358fb65b128bfe6eb894dd088cc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-container-images-toobe-used-with-azure-container-service"></a><span data-ttu-id="2d5e2-104">Container installatiekopieën toobe gebruikt met Azure Container Service maken</span><span class="sxs-lookup"><span data-stu-id="2d5e2-104">Create container images toobe used with Azure Container Service</span></span>

<span data-ttu-id="2d5e2-105">In deze zelfstudie, deel 1 van zeven, is een toepassing met meerdere container klaar voor gebruik in Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="2d5e2-105">In this tutorial, part one of seven, a multi-container application is prepared for use in Kubernetes.</span></span> <span data-ttu-id="2d5e2-106">Stappen voltooid omvatten:</span><span class="sxs-lookup"><span data-stu-id="2d5e2-106">Steps completed include:</span></span>  

> [!div class="checklist"]
> * <span data-ttu-id="2d5e2-107">Toepassingsbron klonen vanuit GitHub</span><span class="sxs-lookup"><span data-stu-id="2d5e2-107">Cloning application source from GitHub</span></span>  
> * <span data-ttu-id="2d5e2-108">Maken van een installatiekopie van een container van Hallo toepassingsbron</span><span class="sxs-lookup"><span data-stu-id="2d5e2-108">Creating a container image from hello application source</span></span>
> * <span data-ttu-id="2d5e2-109">Hallo toepassing testen in een lokale Docker-omgeving</span><span class="sxs-lookup"><span data-stu-id="2d5e2-109">Testing hello application in a local Docker environment</span></span>

<span data-ttu-id="2d5e2-110">Zodra de voltooid, is na toepassing hello toegankelijk zijn in uw lokale ontwikkelingsomgeving.</span><span class="sxs-lookup"><span data-stu-id="2d5e2-110">Once completed, hello following application is accessible in your local development environment.</span></span>

![Afbeelding van Kubernetes-cluster in Azure](media/container-service-kubernetes-tutorials/azure-vote.png)

<span data-ttu-id="2d5e2-112">In volgende zelfstudies Hallo container installatiekopie is geüploade tooan Azure Container register en klik vervolgens op uitvoeren in een Azure Kubernetes cluster wordt gehost.</span><span class="sxs-lookup"><span data-stu-id="2d5e2-112">In subsequent tutorials, hello container image is uploaded tooan Azure Container Registry, and then run in an Azure hosted Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2d5e2-113">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="2d5e2-113">Before you begin</span></span>

<span data-ttu-id="2d5e2-114">In deze zelfstudie wordt ervan uitgegaan dat u een basiskennis hebt van Docker-kernconcepten zoals containers, containerinstallatiekopieën en Docker-basisopdrachten.</span><span class="sxs-lookup"><span data-stu-id="2d5e2-114">This tutorial assumes a basic understanding of core Docker concepts such as containers, container images, and basic docker commands.</span></span> <span data-ttu-id="2d5e2-115">Zie, indien nodig, [Aan de slag met Docker]( https://docs.docker.com/get-started/) voor een uitleg van de basisprincipes van containers.</span><span class="sxs-lookup"><span data-stu-id="2d5e2-115">If needed, see [Get started with Docker]( https://docs.docker.com/get-started/) for a primer on container basics.</span></span> 

<span data-ttu-id="2d5e2-116">toocomplete in deze zelfstudie, moet u een Docker-ontwikkelomgeving.</span><span class="sxs-lookup"><span data-stu-id="2d5e2-116">toocomplete this tutorial, you need a Docker development environment.</span></span> <span data-ttu-id="2d5e2-117">Docker biedt pakketten die eenvoudig Docker op elke configureren op elk [Mac](https://docs.docker.com/docker-for-mac/)-, [Windows](https://docs.docker.com/docker-for-windows/)- of [Linux](https://docs.docker.com/engine/installation/#supported-platforms)-systeem.</span><span class="sxs-lookup"><span data-stu-id="2d5e2-117">Docker provides packages that easily configure Docker on any [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/), or [Linux](https://docs.docker.com/engine/installation/#supported-platforms) system.</span></span>

## <a name="get-application-code"></a><span data-ttu-id="2d5e2-118">Toepassingscode ophalen</span><span class="sxs-lookup"><span data-stu-id="2d5e2-118">Get application code</span></span>

<span data-ttu-id="2d5e2-119">Hallo-voorbeeldtoepassing die is gebruikt in deze zelfstudie is een eenvoudige stemmende app.</span><span class="sxs-lookup"><span data-stu-id="2d5e2-119">hello sample application used in this tutorial is a basic voting app.</span></span> <span data-ttu-id="2d5e2-120">Hallo toepassing bestaat uit een front-onderdeel en een back-end Redis-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="2d5e2-120">hello application consists of a front-end web component and a back-end Redis instance.</span></span> <span data-ttu-id="2d5e2-121">Hallo-webonderdeel wordt verpakt in een installatiekopie van een aangepaste container.</span><span class="sxs-lookup"><span data-stu-id="2d5e2-121">hello web component is packaged into a custom container image.</span></span> <span data-ttu-id="2d5e2-122">Hallo Redis instantie gebruikt een installatiekopie van een ongewijzigd van Docker-Hub.</span><span class="sxs-lookup"><span data-stu-id="2d5e2-122">hello Redis instance uses an unmodified image from Docker Hub.</span></span>  

<span data-ttu-id="2d5e2-123">Gebruik git toodownload een kopie van Hallo toepassing tooyour ontwikkelomgeving.</span><span class="sxs-lookup"><span data-stu-id="2d5e2-123">Use git toodownload a copy of hello application tooyour development environment.</span></span>

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

<span data-ttu-id="2d5e2-124">Binnen Hallo gekloonde directory broncode Hallo-toepassing, een vooraf gemaakte Docker compose bestands- en een manifestbestand Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="2d5e2-124">Inside hello cloned directory is hello application source code, a pre-created Docker compose file, and a Kubernetes manifest file.</span></span> <span data-ttu-id="2d5e2-125">Deze bestanden zijn gebruikte toocreate activa in de gehele Hallo zelfstudie set.</span><span class="sxs-lookup"><span data-stu-id="2d5e2-125">These files are used toocreate assets throughout hello tutorial set.</span></span> 

## <a name="create-container-images"></a><span data-ttu-id="2d5e2-126">Maken van installatiekopieën van de container</span><span class="sxs-lookup"><span data-stu-id="2d5e2-126">Create container images</span></span>

<span data-ttu-id="2d5e2-127">[Docker Compose](https://docs.docker.com/compose/) kan tooautomate Hallo build buiten de container-installatiekopieën en Hallo-implementatie van meerdere container toepassingen gebruikt.</span><span class="sxs-lookup"><span data-stu-id="2d5e2-127">[Docker Compose](https://docs.docker.com/compose/) can be used tooautomate hello build out of container images and hello deployment of multi-container applications.</span></span>

<span data-ttu-id="2d5e2-128">Hallo docker-compose.yml-bestand toocreate Hallo container installatiekopie uitvoert, downloaden Hallo Redis afbeelding, en Hallo toepassing starten.</span><span class="sxs-lookup"><span data-stu-id="2d5e2-128">Run hello docker-compose.yml file toocreate hello container image, download hello Redis image, and start hello application.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml up -d
```

<span data-ttu-id="2d5e2-129">Wanneer het voltooid, gebruikt u Hallo [docker-installatiekopieën](https://docs.docker.com/engine/reference/commandline/images/) opdracht toosee Hallo gemaakt installatiekopieën.</span><span class="sxs-lookup"><span data-stu-id="2d5e2-129">When completed, use hello [docker images](https://docs.docker.com/engine/reference/commandline/images/) command toosee hello created images.</span></span>

```bash
docker images
```

<span data-ttu-id="2d5e2-130">U ziet dat drie afbeeldingen gedownload of gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2d5e2-130">Notice that three images have been downloaded or created.</span></span> <span data-ttu-id="2d5e2-131">Hallo *azure stem voorgrond* installatiekopie Hallo toepassing bevat.</span><span class="sxs-lookup"><span data-stu-id="2d5e2-131">hello *azure-vote-front* image contains hello application.</span></span> <span data-ttu-id="2d5e2-132">Deze is afgeleid van Hallo *nginx flask* installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="2d5e2-132">It was derived from hello *nginx-flask* image.</span></span> <span data-ttu-id="2d5e2-133">Hallo Redis afbeelding is van Docker-Hub gedownload.</span><span class="sxs-lookup"><span data-stu-id="2d5e2-133">hello Redis image was downloaded from Docker Hub.</span></span>

```bash
REPOSITORY                   TAG        IMAGE ID            CREATED             SIZE
azure-vote-front             latest     9cc914e25834        40 seconds ago      694MB
redis                        latest     a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask      788ca94b2313        9 months ago        694MB
```

<span data-ttu-id="2d5e2-134">Voer Hallo [docker ps](https://docs.docker.com/engine/reference/commandline/ps/) opdracht toosee Hallo actieve containers.</span><span class="sxs-lookup"><span data-stu-id="2d5e2-134">Run hello [docker ps](https://docs.docker.com/engine/reference/commandline/ps/) command toosee hello running containers.</span></span>

```bash
docker ps
```

<span data-ttu-id="2d5e2-135">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="2d5e2-135">Output:</span></span>

```bash
CONTAINER ID        IMAGE             COMMAND                  CREATED             STATUS              PORTS                           NAMES
82411933e8f9        azure-vote-front  "/usr/bin/supervisord"   57 seconds ago      Up 30 seconds       443/tcp, 0.0.0.0:8080->80/tcp   azure-vote-front
b68fed4b66b6        redis             "docker-entrypoint..."   57 seconds ago      Up 30 seconds       0.0.0.0:6379->6379/tcp          azure-vote-back
```

## <a name="test-application-locally"></a><span data-ttu-id="2d5e2-136">Toepassing lokaal testen</span><span class="sxs-lookup"><span data-stu-id="2d5e2-136">Test application locally</span></span>

<span data-ttu-id="2d5e2-137">Blader toohttp://localhost:8080 toosee Hallo toepassing uitvoert.</span><span class="sxs-lookup"><span data-stu-id="2d5e2-137">Browse toohttp://localhost:8080 toosee hello running application.</span></span>

![Afbeelding van Kubernetes-cluster in Azure](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="clean-up-resources"></a><span data-ttu-id="2d5e2-139">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="2d5e2-139">Clean up resources</span></span>

<span data-ttu-id="2d5e2-140">Nu dat de functionaliteit van de toepassing is gevalideerd, kunt u actieve containers Hallo gestopt en verwijderd.</span><span class="sxs-lookup"><span data-stu-id="2d5e2-140">Now that application functionality has been validated, hello running containers can be stopped and removed.</span></span> <span data-ttu-id="2d5e2-141">Hallo container afbeeldingen niet verwijderen.</span><span class="sxs-lookup"><span data-stu-id="2d5e2-141">Do not delete hello container images.</span></span> <span data-ttu-id="2d5e2-142">Hallo *azure stem voorgrond* installatiekopie geüploade tooan Azure Container register exemplaar in de volgende zelfstudie Hallo is.</span><span class="sxs-lookup"><span data-stu-id="2d5e2-142">hello *azure-vote-front* image is uploaded tooan Azure Container Registry instance in hello next tutorial.</span></span>

<span data-ttu-id="2d5e2-143">Hallo na toostop Hallo actieve containers worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2d5e2-143">Run hello following toostop hello running containers.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml stop
```

<span data-ttu-id="2d5e2-144">Hallo gestopt containers met Hallo na de opdracht verwijderen.</span><span class="sxs-lookup"><span data-stu-id="2d5e2-144">Delete hello stopped containers with hello following command.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml rm
```

<span data-ttu-id="2d5e2-145">Is voltooid hebt u de installatiekopie van een container met hello Azure stem toepassing.</span><span class="sxs-lookup"><span data-stu-id="2d5e2-145">At completion, you have a container image that contains hello Azure Vote application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2d5e2-146">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2d5e2-146">Next steps</span></span>

<span data-ttu-id="2d5e2-147">Een toepassing is getest en installatiekopieën van de container gemaakt voor de toepassing hello in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="2d5e2-147">In this tutorial, an application was tested and container images created for hello application.</span></span> <span data-ttu-id="2d5e2-148">Hallo stappen zijn voltooid:</span><span class="sxs-lookup"><span data-stu-id="2d5e2-148">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2d5e2-149">Hallo-toepassingsbron klonen vanuit GitHub</span><span class="sxs-lookup"><span data-stu-id="2d5e2-149">Cloning hello application source from GitHub</span></span>  
> * <span data-ttu-id="2d5e2-150">De installatiekopie van een container van toepassingsbron gemaakt</span><span class="sxs-lookup"><span data-stu-id="2d5e2-150">Created a container image from application source</span></span>
> * <span data-ttu-id="2d5e2-151">Hallo geteste toepassing in een lokale Docker-omgeving</span><span class="sxs-lookup"><span data-stu-id="2d5e2-151">Tested hello application in a local Docker environment</span></span>

<span data-ttu-id="2d5e2-152">Ga toohello volgende zelfstudie toolearn over het opslaan van installatiekopieën van de container in een Azure Container-register.</span><span class="sxs-lookup"><span data-stu-id="2d5e2-152">Advance toohello next tutorial toolearn about storing container images in an Azure Container Registry.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2d5e2-153">Push-installatiekopieën tooAzure Container register</span><span class="sxs-lookup"><span data-stu-id="2d5e2-153">Push images tooAzure Container Registry</span></span>](./container-service-tutorial-kubernetes-prepare-acr.md)
