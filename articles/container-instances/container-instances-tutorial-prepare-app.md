---
title: uw app aaaAzure Containerexemplaren zelfstudie - voorbereiden | Azure Docs
description: Een app voor de implementatie tooAzure Containerexemplaren voorbereiden
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
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 406ba796e5fefb1527f2e894cc3f7bbd8f7a5fd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-container-for-deployment-tooazure-container-instances"></a><span data-ttu-id="f708c-103">Container voor implementatie tooAzure Containerexemplaren maken</span><span class="sxs-lookup"><span data-stu-id="f708c-103">Create container for deployment tooAzure Container Instances</span></span>

<span data-ttu-id="f708c-104">Met Azure Container Instances kunt u Docker-containers implementeren in de Azure-infrastructuur zonder virtuele machines in te richten of gebruik te maken van een service op een hoger niveau.</span><span class="sxs-lookup"><span data-stu-id="f708c-104">Azure Container Instances enables deployment of Docker containers onto Azure infrastructure without provisioning any virtual machines or adopting any higher-level service.</span></span> <span data-ttu-id="f708c-105">In deze zelfstudie maakt u een eenvoudige webtoepassing in Node.js en verpakt u deze in een container die kan worden uitgevoerd met behulp van Azure Container Instances.</span><span class="sxs-lookup"><span data-stu-id="f708c-105">In this tutorial, you will build a simple web application in Node.js and package it in a container that can be run using Azure Container Instances.</span></span> <span data-ttu-id="f708c-106">Het volgende wordt besproken:</span><span class="sxs-lookup"><span data-stu-id="f708c-106">We will cover:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f708c-107">Toepassingsbron klonen vanuit GitHub</span><span class="sxs-lookup"><span data-stu-id="f708c-107">Cloning application source from GitHub</span></span>  
> * <span data-ttu-id="f708c-108">Containerinstallatiekopieën van de toepassingsbron maken</span><span class="sxs-lookup"><span data-stu-id="f708c-108">Creating container images from application source</span></span>
> * <span data-ttu-id="f708c-109">Hallo installatiekopieën testen in een lokale Docker-omgeving</span><span class="sxs-lookup"><span data-stu-id="f708c-109">Testing hello images in a local Docker environment</span></span>

<span data-ttu-id="f708c-110">In volgende zelfstudies leert u uploaden van uw installatiekopie tooan Azure Container register, en vervolgens implementeren tooAzure Containerexemplaren.</span><span class="sxs-lookup"><span data-stu-id="f708c-110">In subsequent tutorials, you will upload your image tooan Azure Container Registry, and then deploy them tooAzure Container Instances.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f708c-111">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="f708c-111">Before you begin</span></span>

<span data-ttu-id="f708c-112">In deze zelfstudie wordt ervan uitgegaan dat u een basiskennis hebt van Docker-kernconcepten zoals containers, containerinstallatiekopieën en Docker-basisopdrachten.</span><span class="sxs-lookup"><span data-stu-id="f708c-112">This tutorial assumes a basic understanding of core Docker concepts such as containers, container images, and basic docker commands.</span></span> <span data-ttu-id="f708c-113">Zie, indien nodig, [Aan de slag met Docker]( https://docs.docker.com/get-started/) voor een uitleg van de basisprincipes van containers.</span><span class="sxs-lookup"><span data-stu-id="f708c-113">If needed, see [Get started with Docker]( https://docs.docker.com/get-started/) for a primer on container basics.</span></span> 

<span data-ttu-id="f708c-114">toocomplete in deze zelfstudie, moet u een Docker-ontwikkelomgeving.</span><span class="sxs-lookup"><span data-stu-id="f708c-114">toocomplete this tutorial, you need a Docker development environment.</span></span> <span data-ttu-id="f708c-115">Docker biedt pakketten die eenvoudig Docker op elke configureren op elk [Mac](https://docs.docker.com/docker-for-mac/)-, [Windows](https://docs.docker.com/docker-for-windows/)- of [Linux](https://docs.docker.com/engine/installation/#supported-platforms)-systeem.</span><span class="sxs-lookup"><span data-stu-id="f708c-115">Docker provides packages that easily configure Docker on any [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/), or [Linux](https://docs.docker.com/engine/installation/#supported-platforms) system.</span></span>

## <a name="get-application-code"></a><span data-ttu-id="f708c-116">Toepassingscode ophalen</span><span class="sxs-lookup"><span data-stu-id="f708c-116">Get application code</span></span>

<span data-ttu-id="f708c-117">Hallo-voorbeeld in deze zelfstudie bevat een eenvoudige webtoepassing die is ingebouwd in [Node.js](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="f708c-117">hello sample in this tutorial includes a simple web application built in [Node.js](http://nodejs.org).</span></span> <span data-ttu-id="f708c-118">Hallo-app fungeert een statische HTML-pagina en uitziet:</span><span class="sxs-lookup"><span data-stu-id="f708c-118">hello app serves a static HTML page and looks like this:</span></span>

![Zelfstudie-app weergegeven in browser][aci-tutorial-app]

<span data-ttu-id="f708c-120">Gebruik git toodownload Hallo voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="f708c-120">Use git toodownload hello sample:</span></span>

```bash
git clone https://github.com/Azure-Samples/aci-helloworld.git
```

## <a name="build-hello-container-image"></a><span data-ttu-id="f708c-121">Hallo container installatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="f708c-121">Build hello container image</span></span>

<span data-ttu-id="f708c-122">Hallo Dockerfile in het Hallo-repo-voorbeeld ziet u hoe Hallo container wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f708c-122">hello Dockerfile provided in hello sample repo shows how hello container is built.</span></span> <span data-ttu-id="f708c-123">Het starten van een [officiële Node.js installatiekopie] [ dockerhub-nodeimage] op basis van [Alpine Linux](https://alpinelinux.org/), een kleine distributie die is uitermate geschikt toouse met containers.</span><span class="sxs-lookup"><span data-stu-id="f708c-123">It starts from an [official Node.js image][dockerhub-nodeimage] based on [Alpine Linux](https://alpinelinux.org/), a small distribution that is well suited toouse with containers.</span></span> <span data-ttu-id="f708c-124">Vervolgens Hallo toepassingsbestanden kopieert naar Hallo-container, afhankelijkheden met Hallo knooppunt Package Manager is geïnstalleerd en ten slotte start Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="f708c-124">It then copies hello application files into hello container, installs dependencies using hello Node Package Manager, and finally starts hello application.</span></span>

```
FROM node:8.2.0-alpine
RUN mkdir -p /usr/src/app
COPY ./app/* /usr/src/app/
WORKDIR /usr/src/app
RUN npm install
CMD node /usr/src/app/index.js
```

<span data-ttu-id="f708c-125">Gebruik Hallo `docker build` toocreate Hallo container opdrachtafbeelding, labelen als *aci-zelfstudie-app*:</span><span class="sxs-lookup"><span data-stu-id="f708c-125">Use hello `docker build` command toocreate hello container image, tagging it as *aci-tutorial-app*:</span></span>

```bash
docker build ./aci-helloworld -t aci-tutorial-app
```

<span data-ttu-id="f708c-126">Gebruik Hallo `docker images` toosee Hallo gebouwd installatiekopie:</span><span class="sxs-lookup"><span data-stu-id="f708c-126">Use hello `docker images` toosee hello built image:</span></span>

```bash
docker images
```

<span data-ttu-id="f708c-127">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="f708c-127">Output:</span></span>

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

## <a name="run-hello-container-locally"></a><span data-ttu-id="f708c-128">Hallo-container lokaal uitvoeren</span><span class="sxs-lookup"><span data-stu-id="f708c-128">Run hello container locally</span></span>

<span data-ttu-id="f708c-129">Voordat u probeert Hallo container tooAzure Containerexemplaren implementeren, het lokaal uitvoeren tooconfirm of dit werkt.</span><span class="sxs-lookup"><span data-stu-id="f708c-129">Before you try deploying hello container tooAzure Container Instances, run it locally tooconfirm that it works.</span></span> <span data-ttu-id="f708c-130">Hallo `-d` switch kunt uitvoeren op de achtergrond Hallo Hallo-container terwijl `-p` kunt u een willekeurige poort op uw compute tooport 80 in Hallo container toomap.</span><span class="sxs-lookup"><span data-stu-id="f708c-130">hello `-d` switch lets hello container run in hello background, while `-p` allows you toomap an arbitrary port on your compute tooport 80 in hello container.</span></span>

```bash
docker run -d -p 8080:80 aci-tutorial-app
```

<span data-ttu-id="f708c-131">Open Hallo browser toohttp://localhost:8080 tooconfirm die container Hallo wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f708c-131">Open hello browser toohttp://localhost:8080 tooconfirm that hello container is running.</span></span>

![Actieve Hallo app lokaal in de browser Hallo][aci-tutorial-app-local]

## <a name="next-steps"></a><span data-ttu-id="f708c-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f708c-133">Next steps</span></span>

<span data-ttu-id="f708c-134">In deze zelfstudie maakt u een container-installatiekopie die geïmplementeerde tooAzure Containerexemplaren kan worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f708c-134">In this tutorial, you created a container image that can be deployed tooAzure Container Instances.</span></span> <span data-ttu-id="f708c-135">Hallo stappen zijn voltooid:</span><span class="sxs-lookup"><span data-stu-id="f708c-135">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f708c-136">Hallo-toepassingsbron klonen vanuit GitHub</span><span class="sxs-lookup"><span data-stu-id="f708c-136">Cloning hello application source from GitHub</span></span>  
> * <span data-ttu-id="f708c-137">Containerinstallatiekopieën van de toepassingsbron maken</span><span class="sxs-lookup"><span data-stu-id="f708c-137">Creating container images from application source</span></span>
> * <span data-ttu-id="f708c-138">Hallo container lokaal testen</span><span class="sxs-lookup"><span data-stu-id="f708c-138">Testing hello container locally</span></span>

<span data-ttu-id="f708c-139">Ga toohello volgende zelfstudie toolearn over het opslaan van installatiekopieën van de container in een Azure Container-register.</span><span class="sxs-lookup"><span data-stu-id="f708c-139">Advance toohello next tutorial toolearn about storing container images in an Azure Container Registry.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f708c-140">Push-installatiekopieën tooAzure Container register</span><span class="sxs-lookup"><span data-stu-id="f708c-140">Push images tooAzure Container Registry</span></span>](./container-instances-tutorial-prepare-acr.md)

<!-- LINKS -->
[dockerhub-nodeimage]: https://hub.docker.com/r/library/node/tags/8.2.0-alpine/

<!--- IMAGES --->
[aci-tutorial-app]:./media/container-instances-quickstart/aci-app-browser.png
[aci-tutorial-app-local]: ./media/container-instances-tutorial-prepare-app/aci-app-browser-local.png