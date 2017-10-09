---
title: aaaManage Azure Swarm-cluster met Docker API | Microsoft Docs
description: Containers tooa Docker Swarm-cluster in Azure Container Service implementeren
services: container-service
documentationcenter: 
author: rgardler
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: Docker, Containers, Micro-services, Mesos, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/13/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: bb9b07c82a7b48caeb2e351455797cbf2a6e7480
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="container-management-with-docker-swarm"></a><span data-ttu-id="53be6-104">Containerbeheer met Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="53be6-104">Container management with Docker Swarm</span></span>
<span data-ttu-id="53be6-105">Docker Swarm biedt een omgeving voor het implementeren van beperkte workloads in een gegroepeerde set Docker-hosts.</span><span class="sxs-lookup"><span data-stu-id="53be6-105">Docker Swarm provides an environment for deploying containerized workloads across a pooled set of Docker hosts.</span></span> <span data-ttu-id="53be6-106">Docker Swarm maakt gebruik van Hallo systeemeigen Docker API.</span><span class="sxs-lookup"><span data-stu-id="53be6-106">Docker Swarm uses hello native Docker API.</span></span> <span data-ttu-id="53be6-107">Hallo-werkstroom voor het beheer van containers in een Docker Swarm is bijna identiek toowhat op een enkele containerhost.</span><span class="sxs-lookup"><span data-stu-id="53be6-107">hello workflow for managing containers on a Docker Swarm is almost identical toowhat it would be on a single container host.</span></span> <span data-ttu-id="53be6-108">Dit document bevat enkele eenvoudige voorbeelden van de implementatie van beperkte workloads in een Azure Container Service-exemplaar van Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="53be6-108">This document provides simple examples of deploying containerized workloads in an Azure Container Service instance of Docker Swarm.</span></span> <span data-ttu-id="53be6-109">Zie [Docker Swarm op Docker.com](https://docs.docker.com/swarm/) voor uitgebreidere documentatie bij Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="53be6-109">For more in-depth documentation on Docker Swarm, see [Docker Swarm on Docker.com](https://docs.docker.com/swarm/).</span></span>

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

<span data-ttu-id="53be6-110">Vereisten toohello oefeningen in dit document:</span><span class="sxs-lookup"><span data-stu-id="53be6-110">Prerequisites toohello exercises in this document:</span></span>

[<span data-ttu-id="53be6-111">Een Swarm-cluster in Azure Container Service maken</span><span class="sxs-lookup"><span data-stu-id="53be6-111">Create a Swarm cluster in Azure Container Service</span></span>](container-service-deployment.md)

[<span data-ttu-id="53be6-112">Verbinding maken met de Hallo Swarm-cluster in Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="53be6-112">Connect with hello Swarm cluster in Azure Container Service</span></span>](../container-service-connect.md)

## <a name="deploy-a-new-container"></a><span data-ttu-id="53be6-113">Een nieuwe container implementeren</span><span class="sxs-lookup"><span data-stu-id="53be6-113">Deploy a new container</span></span>
<span data-ttu-id="53be6-114">een nieuwe container in Docker Swarm, Hallo toocreate gebruiken Hallo `docker run` opdracht (waarbij u ervoor zorgt dat u een SSH-tunnel toohello masters volgens Hallo bovenstaande vereisten hebt geopend).</span><span class="sxs-lookup"><span data-stu-id="53be6-114">toocreate a new container in hello Docker Swarm, use hello `docker run` command (ensuring that you have opened an SSH tunnel toohello masters as per hello prerequisites above).</span></span> <span data-ttu-id="53be6-115">In dit voorbeeld maakt u een container van Hallo `yeasy/simple-web` afbeelding:</span><span class="sxs-lookup"><span data-stu-id="53be6-115">This example creates a container from hello `yeasy/simple-web` image:</span></span>

```bash
user@ubuntu:~$ docker run -d -p 80:80 yeasy/simple-web

4298d397b9ab6f37e2d1978ef3c8c1537c938e98a8bf096ff00def2eab04bf72
```

<span data-ttu-id="53be6-116">Nadat het Hallo-container is gemaakt, gebruikt u `docker ps` tooreturn informatie over het Hallo-container.</span><span class="sxs-lookup"><span data-stu-id="53be6-116">After hello container has been created, use `docker ps` tooreturn information about hello container.</span></span> <span data-ttu-id="53be6-117">U ziet hier dat Hallo Swarm-agent die als host voor de container hello fungeert wordt vermeld:</span><span class="sxs-lookup"><span data-stu-id="53be6-117">Notice here that hello Swarm agent that is hosting hello container is listed:</span></span>

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   31 seconds ago      Up 9 seconds        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

<span data-ttu-id="53be6-118">U kunt nu toegang tot Hallo-toepassing die wordt uitgevoerd in deze container via openbare DNS-naam Hallo Hallo Swarm-agent load balancer.</span><span class="sxs-lookup"><span data-stu-id="53be6-118">You can now access hello application that is running in this container through hello public DNS name of hello Swarm agent load balancer.</span></span> <span data-ttu-id="53be6-119">U vindt deze informatie in hello Azure-portal:</span><span class="sxs-lookup"><span data-stu-id="53be6-119">You can find this information in hello Azure portal:</span></span>  

![Echte bezoekresultaten](./media/container-service-docker-swarm/real-visit.jpg)  

<span data-ttu-id="53be6-121">Hallo Load Balancer heeft standaard de poorten 80, 8080 en 443 openen.</span><span class="sxs-lookup"><span data-stu-id="53be6-121">By default hello Load Balancer has ports 80, 8080 and 443 open.</span></span> <span data-ttu-id="53be6-122">Als u wilt dat tooconnect op een andere poort moet u tooopen die poort op Hallo Azure Load Balancer voor Hallo-Agent van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="53be6-122">If you want tooconnect on another port you will need tooopen that port on hello Azure Load Balancer for hello Agent Pool.</span></span>

## <a name="deploy-multiple-containers"></a><span data-ttu-id="53be6-123">Meerdere containers implementeren</span><span class="sxs-lookup"><span data-stu-id="53be6-123">Deploy multiple containers</span></span>
<span data-ttu-id="53be6-124">Als meerdere containers worden gestart door de opdracht 'docker uitvoeren' meerdere keren kunt u Hallo `docker ps` opdracht toosee die als host fungeert voor Hallo containers op worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="53be6-124">As multiple containers are started, by executing 'docker run' multiple times, you can use hello `docker ps` command toosee which hosts hello containers are running on.</span></span> <span data-ttu-id="53be6-125">In onderstaande Hallo voorbeeld, drie containers gelijkmatig verdeeld over de drie Swarm-agents Hallo:</span><span class="sxs-lookup"><span data-stu-id="53be6-125">In hello example below, three containers are spread evenly across hello three Swarm agents:</span></span>  

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
11be062ff602        yeasy/simple-web    "/bin/sh -c 'python i"   11 seconds ago      Up 10 seconds       10.0.0.6:83->80/tcp   swarm-agent-34A73819-2/clever_banach
1ff421554c50        yeasy/simple-web    "/bin/sh -c 'python i"   49 seconds ago      Up 48 seconds       10.0.0.4:82->80/tcp   swarm-agent-34A73819-0/stupefied_ride
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   2 minutes ago       Up 2 minutes        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

## <a name="deploy-containers-by-using-docker-compose"></a><span data-ttu-id="53be6-126">Containers implementeren met behulp van Docker Compose</span><span class="sxs-lookup"><span data-stu-id="53be6-126">Deploy containers by using Docker Compose</span></span>
<span data-ttu-id="53be6-127">U kunt Docker Compose tooautomate Hallo implementatie en configuratie van meerdere containers.</span><span class="sxs-lookup"><span data-stu-id="53be6-127">You can use Docker Compose tooautomate hello deployment and configuration of multiple containers.</span></span> <span data-ttu-id="53be6-128">toodo is dus zorg ervoor dat een tunnel Secure Shell (SSH) is gemaakt en die Hallo DOCKER_HOST variabele is ingesteld (Zie vereisten Hallo hierboven).</span><span class="sxs-lookup"><span data-stu-id="53be6-128">toodo so, ensure that a Secure Shell (SSH) tunnel has been created and that hello DOCKER_HOST variable has been set (see hello pre-requisites above).</span></span>

<span data-ttu-id="53be6-129">Maak een docker-compose.yml-bestand op het lokale systeem.</span><span class="sxs-lookup"><span data-stu-id="53be6-129">Create a docker-compose.yml file on your local system.</span></span> <span data-ttu-id="53be6-130">toodo, gebruiken deze [voorbeeld](https://raw.githubusercontent.com/rgardler/AzureDevTestDeploy/master/docker-compose.yml).</span><span class="sxs-lookup"><span data-stu-id="53be6-130">toodo this, use this [sample](https://raw.githubusercontent.com/rgardler/AzureDevTestDeploy/master/docker-compose.yml).</span></span>

```bash
web:
  image: adtd/web:0.1
  ports:
    - "80:80"
  links:
    - rest:rest-demo-azure.marathon.mesos
rest:
  image: adtd/rest:0.1
  ports:
    - "8080:8080"

```

<span data-ttu-id="53be6-131">Voer `docker-compose up -d` toostart hello containerimplementaties:</span><span class="sxs-lookup"><span data-stu-id="53be6-131">Run `docker-compose up -d` toostart hello container deployments:</span></span>

```bash
user@ubuntu:~/compose$ docker-compose up -d
Pulling rest (adtd/rest:0.1)...
swarm-agent-3B7093B8-0: Pulling adtd/rest:0.1... : downloaded
swarm-agent-3B7093B8-2: Pulling adtd/rest:0.1... : downloaded
swarm-agent-3B7093B8-3: Pulling adtd/rest:0.1... : downloaded
Creating compose_rest_1
Pulling web (adtd/web:0.1)...
swarm-agent-3B7093B8-3: Pulling adtd/web:0.1... : downloaded
swarm-agent-3B7093B8-0: Pulling adtd/web:0.1... : downloaded
swarm-agent-3B7093B8-2: Pulling adtd/web:0.1... : downloaded
Creating compose_web_1
```

<span data-ttu-id="53be6-132">Ten slotte Hallo lijst met actieve containers geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="53be6-132">Finally, hello list of running containers will be returned.</span></span> <span data-ttu-id="53be6-133">Deze lijst geeft Hallo-containers die zijn geïmplementeerd met behulp van Docker Compose:</span><span class="sxs-lookup"><span data-stu-id="53be6-133">This list reflects hello containers that were deployed by using Docker Compose:</span></span>

```bash
user@ubuntu:~/compose$ docker ps
CONTAINER ID        IMAGE               COMMAND                CREATED             STATUS              PORTS                     NAMES
caf185d221b7        adtd/web:0.1        "apache2-foreground"   2 minutes ago       Up About a minute   10.0.0.4:80->80/tcp       swarm-agent-3B7093B8-0/compose_web_1
040efc0ea937        adtd/rest:0.1       "catalina.sh run"      3 minutes ago       Up 2 minutes        10.0.0.4:8080->8080/tcp   swarm-agent-3B7093B8-0/compose_rest_1
```

<span data-ttu-id="53be6-134">U kunt uiteraard `docker-compose ps` tooexamine Hallo alleen containers die zijn gedefinieerd in uw `compose.yml` bestand.</span><span class="sxs-lookup"><span data-stu-id="53be6-134">Naturally, you can use `docker-compose ps` tooexamine only hello containers defined in your `compose.yml` file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="53be6-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="53be6-135">Next steps</span></span>
[<span data-ttu-id="53be6-136">Meer informatie over Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="53be6-136">Learn more about Docker Swarm</span></span>](https://docs.docker.com/swarm/)

