---
title: Azure Swarm-cluster met Docker API beheren
description: Implementeer containers naar een Docker Swarm-cluster in Azure Container Service
services: container-service
author: rgardler
manager: madhana
ms.service: container-service
ms.topic: article
ms.date: 09/13/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 3f8d18bc053bc303ab124ba38c8621d4ee2e8cb8
ms.sourcegitcommit: 694e40a193980dea1e2f945471071f11030d5641
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 01/29/2018
---
# <a name="container-management-with-docker-swarm"></a><span data-ttu-id="969bb-103">Containerbeheer met Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="969bb-103">Container management with Docker Swarm</span></span>

<span data-ttu-id="969bb-104">Docker Swarm biedt een omgeving voor het implementeren van beperkte workloads in een gegroepeerde set Docker-hosts.</span><span class="sxs-lookup"><span data-stu-id="969bb-104">Docker Swarm provides an environment for deploying containerized workloads across a pooled set of Docker hosts.</span></span> <span data-ttu-id="969bb-105">Docker Swarm maakt gebruik van de systeemeigen Docker API.</span><span class="sxs-lookup"><span data-stu-id="969bb-105">Docker Swarm uses the native Docker API.</span></span> <span data-ttu-id="969bb-106">De werkstroom voor het beheer van containers in een Docker Swarm is bijna identiek aan de werkstroom op een enkele containerhost.</span><span class="sxs-lookup"><span data-stu-id="969bb-106">The workflow for managing containers on a Docker Swarm is almost identical to what it would be on a single container host.</span></span> <span data-ttu-id="969bb-107">Dit document bevat enkele eenvoudige voorbeelden van de implementatie van beperkte workloads in een Azure Container Service-exemplaar van Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="969bb-107">This document provides simple examples of deploying containerized workloads in an Azure Container Service instance of Docker Swarm.</span></span> <span data-ttu-id="969bb-108">Zie [Docker Swarm op Docker.com](https://docs.docker.com/swarm/) voor uitgebreidere documentatie bij Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="969bb-108">For more in-depth documentation on Docker Swarm, see [Docker Swarm on Docker.com](https://docs.docker.com/swarm/).</span></span>

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

<span data-ttu-id="969bb-109">Vereisten voor de oefeningen in dit document:</span><span class="sxs-lookup"><span data-stu-id="969bb-109">Prerequisites to the exercises in this document:</span></span>

[<span data-ttu-id="969bb-110">Een Swarm-cluster in Azure Container Service maken</span><span class="sxs-lookup"><span data-stu-id="969bb-110">Create a Swarm cluster in Azure Container Service</span></span>](container-service-deployment.md)

[<span data-ttu-id="969bb-111">Verbinding maken met het Swarm-cluster in Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="969bb-111">Connect with the Swarm cluster in Azure Container Service</span></span>](../container-service-connect.md)

## <a name="deploy-a-new-container"></a><span data-ttu-id="969bb-112">Een nieuwe container implementeren</span><span class="sxs-lookup"><span data-stu-id="969bb-112">Deploy a new container</span></span>
<span data-ttu-id="969bb-113">Als u in de Docker Swarm een nieuwe container wilt maken, gebruikt u de opdracht `docker run` (waarbij u ervoor zorgt dat u een SSH-tunnel naar de masters hebt geopend overeenkomstig de bovenstaande vereisten).</span><span class="sxs-lookup"><span data-stu-id="969bb-113">To create a new container in the Docker Swarm, use the `docker run` command (ensuring that you have opened an SSH tunnel to the masters as per the prerequisites above).</span></span> <span data-ttu-id="969bb-114">In dit voorbeeld wordt een container van gemaakt op basis van de `yeasy/simple-web`-installatiekopie:</span><span class="sxs-lookup"><span data-stu-id="969bb-114">This example creates a container from the `yeasy/simple-web` image:</span></span>

```bash
user@ubuntu:~$ docker run -d -p 80:80 yeasy/simple-web

4298d397b9ab6f37e2d1978ef3c8c1537c938e98a8bf096ff00def2eab04bf72
```

<span data-ttu-id="969bb-115">Nadat de container is gemaakt, gebruikt u `docker ps` om informatie over de container te retourneren.</span><span class="sxs-lookup"><span data-stu-id="969bb-115">After the container has been created, use `docker ps` to return information about the container.</span></span> <span data-ttu-id="969bb-116">U ziet hier dat de Swarm-agent wordt vermeld die als host fungeert voor de container:</span><span class="sxs-lookup"><span data-stu-id="969bb-116">Notice here that the Swarm agent that is hosting the container is listed:</span></span>

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   31 seconds ago      Up 9 seconds        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

<span data-ttu-id="969bb-117">U hebt nu toegang tot de toepassing die wordt uitgevoerd in deze container via de openbare DNS-naam van de load balancer van de Swarm-agent.</span><span class="sxs-lookup"><span data-stu-id="969bb-117">You can now access the application that is running in this container through the public DNS name of the Swarm agent load balancer.</span></span> <span data-ttu-id="969bb-118">U kunt deze informatie vinden in Azure Portal:</span><span class="sxs-lookup"><span data-stu-id="969bb-118">You can find this information in the Azure portal:</span></span>  

![Echte bezoekresultaten](./media/container-service-docker-swarm/real-visit.jpg)  

<span data-ttu-id="969bb-120">De Load Balancer heeft standaard de poorten 80, 8080 en 443 open.</span><span class="sxs-lookup"><span data-stu-id="969bb-120">By default the Load Balancer has ports 80, 8080 and 443 open.</span></span> <span data-ttu-id="969bb-121">Als u via een andere poort verbinding wilt maken, moet u die poort openen in de Azure Load Balancer voor de Agent-pool.</span><span class="sxs-lookup"><span data-stu-id="969bb-121">If you want to connect on another port you will need to open that port on the Azure Load Balancer for the Agent Pool.</span></span>

## <a name="deploy-multiple-containers"></a><span data-ttu-id="969bb-122">Meerdere containers implementeren</span><span class="sxs-lookup"><span data-stu-id="969bb-122">Deploy multiple containers</span></span>
<span data-ttu-id="969bb-123">Als meerdere containers worden gestart, door 'docker run' meermaals uit te voeren, kunt u de opdracht `docker ps` gebruiken om te zien op welke hosts de containers worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="969bb-123">As multiple containers are started, by executing 'docker run' multiple times, you can use the `docker ps` command to see which hosts the containers are running on.</span></span> <span data-ttu-id="969bb-124">In het voorbeeld hieronder zijn drie containers gelijkmatig verdeeld over de drie Swarm-agents:</span><span class="sxs-lookup"><span data-stu-id="969bb-124">In the example below, three containers are spread evenly across the three Swarm agents:</span></span>  

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
11be062ff602        yeasy/simple-web    "/bin/sh -c 'python i"   11 seconds ago      Up 10 seconds       10.0.0.6:83->80/tcp   swarm-agent-34A73819-2/clever_banach
1ff421554c50        yeasy/simple-web    "/bin/sh -c 'python i"   49 seconds ago      Up 48 seconds       10.0.0.4:82->80/tcp   swarm-agent-34A73819-0/stupefied_ride
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   2 minutes ago       Up 2 minutes        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

## <a name="deploy-containers-by-using-docker-compose"></a><span data-ttu-id="969bb-125">Containers implementeren met behulp van Docker Compose</span><span class="sxs-lookup"><span data-stu-id="969bb-125">Deploy containers by using Docker Compose</span></span>
<span data-ttu-id="969bb-126">U kunt Docker Compose gebruiken om de implementatie en configuratie van meerdere containers te automatiseren.</span><span class="sxs-lookup"><span data-stu-id="969bb-126">You can use Docker Compose to automate the deployment and configuration of multiple containers.</span></span> <span data-ttu-id="969bb-127">Hiervoor moet een SSH-tunnel (Secure Shell-tunnel) zijn gemaakt en moet de variabele DOCKER_HOST zijn ingesteld (zie de bovenstaande vereisten).</span><span class="sxs-lookup"><span data-stu-id="969bb-127">To do so, ensure that a Secure Shell (SSH) tunnel has been created and that the DOCKER_HOST variable has been set (see the pre-requisites above).</span></span>

<span data-ttu-id="969bb-128">Maak een docker-compose.yml-bestand op het lokale systeem.</span><span class="sxs-lookup"><span data-stu-id="969bb-128">Create a docker-compose.yml file on your local system.</span></span> <span data-ttu-id="969bb-129">Gebruik dit [voorbeeld](https://raw.githubusercontent.com/rgardler/AzureDevTestDeploy/master/docker-compose.yml) om dit te doen.</span><span class="sxs-lookup"><span data-stu-id="969bb-129">To do this, use this [sample](https://raw.githubusercontent.com/rgardler/AzureDevTestDeploy/master/docker-compose.yml).</span></span>

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

<span data-ttu-id="969bb-130">Voer `docker-compose up -d` uit om de containerimplementaties te starten:</span><span class="sxs-lookup"><span data-stu-id="969bb-130">Run `docker-compose up -d` to start the container deployments:</span></span>

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

<span data-ttu-id="969bb-131">Tot slot wordt de lijst met actieve containers geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="969bb-131">Finally, the list of running containers will be returned.</span></span> <span data-ttu-id="969bb-132">Deze lijst bevat de containers die zijn geïmplementeerd met behulp van Docker Compose:</span><span class="sxs-lookup"><span data-stu-id="969bb-132">This list reflects the containers that were deployed by using Docker Compose:</span></span>

```bash
user@ubuntu:~/compose$ docker ps
CONTAINER ID        IMAGE               COMMAND                CREATED             STATUS              PORTS                     NAMES
caf185d221b7        adtd/web:0.1        "apache2-foreground"   2 minutes ago       Up About a minute   10.0.0.4:80->80/tcp       swarm-agent-3B7093B8-0/compose_web_1
040efc0ea937        adtd/rest:0.1       "catalina.sh run"      3 minutes ago       Up 2 minutes        10.0.0.4:8080->8080/tcp   swarm-agent-3B7093B8-0/compose_rest_1
```

<span data-ttu-id="969bb-133">Uiteraard kunt u `docker-compose ps` gebruiken om alleen de containers te onderzoeken die in uw bestand `compose.yml` zijn gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="969bb-133">Naturally, you can use `docker-compose ps` to examine only the containers defined in your `compose.yml` file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="969bb-134">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="969bb-134">Next steps</span></span>
[<span data-ttu-id="969bb-135">Meer informatie over Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="969bb-135">Learn more about Docker Swarm</span></span>](https://docs.docker.com/swarm/)

