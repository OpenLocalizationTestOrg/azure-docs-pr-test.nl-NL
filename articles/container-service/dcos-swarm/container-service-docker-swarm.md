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
# <a name="container-management-with-docker-swarm"></a>Containerbeheer met Docker Swarm
Docker Swarm biedt een omgeving voor het implementeren van beperkte workloads in een gegroepeerde set Docker-hosts. Docker Swarm maakt gebruik van Hallo systeemeigen Docker API. Hallo-werkstroom voor het beheer van containers in een Docker Swarm is bijna identiek toowhat op een enkele containerhost. Dit document bevat enkele eenvoudige voorbeelden van de implementatie van beperkte workloads in een Azure Container Service-exemplaar van Docker Swarm. Zie [Docker Swarm op Docker.com](https://docs.docker.com/swarm/) voor uitgebreidere documentatie bij Docker Swarm.

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

Vereisten toohello oefeningen in dit document:

[Een Swarm-cluster in Azure Container Service maken](container-service-deployment.md)

[Verbinding maken met de Hallo Swarm-cluster in Azure Container Service](../container-service-connect.md)

## <a name="deploy-a-new-container"></a>Een nieuwe container implementeren
een nieuwe container in Docker Swarm, Hallo toocreate gebruiken Hallo `docker run` opdracht (waarbij u ervoor zorgt dat u een SSH-tunnel toohello masters volgens Hallo bovenstaande vereisten hebt geopend). In dit voorbeeld maakt u een container van Hallo `yeasy/simple-web` afbeelding:

```bash
user@ubuntu:~$ docker run -d -p 80:80 yeasy/simple-web

4298d397b9ab6f37e2d1978ef3c8c1537c938e98a8bf096ff00def2eab04bf72
```

Nadat het Hallo-container is gemaakt, gebruikt u `docker ps` tooreturn informatie over het Hallo-container. U ziet hier dat Hallo Swarm-agent die als host voor de container hello fungeert wordt vermeld:

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   31 seconds ago      Up 9 seconds        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

U kunt nu toegang tot Hallo-toepassing die wordt uitgevoerd in deze container via openbare DNS-naam Hallo Hallo Swarm-agent load balancer. U vindt deze informatie in hello Azure-portal:  

![Echte bezoekresultaten](./media/container-service-docker-swarm/real-visit.jpg)  

Hallo Load Balancer heeft standaard de poorten 80, 8080 en 443 openen. Als u wilt dat tooconnect op een andere poort moet u tooopen die poort op Hallo Azure Load Balancer voor Hallo-Agent van toepassingen.

## <a name="deploy-multiple-containers"></a>Meerdere containers implementeren
Als meerdere containers worden gestart door de opdracht 'docker uitvoeren' meerdere keren kunt u Hallo `docker ps` opdracht toosee die als host fungeert voor Hallo containers op worden uitgevoerd. In onderstaande Hallo voorbeeld, drie containers gelijkmatig verdeeld over de drie Swarm-agents Hallo:  

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
11be062ff602        yeasy/simple-web    "/bin/sh -c 'python i"   11 seconds ago      Up 10 seconds       10.0.0.6:83->80/tcp   swarm-agent-34A73819-2/clever_banach
1ff421554c50        yeasy/simple-web    "/bin/sh -c 'python i"   49 seconds ago      Up 48 seconds       10.0.0.4:82->80/tcp   swarm-agent-34A73819-0/stupefied_ride
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   2 minutes ago       Up 2 minutes        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

## <a name="deploy-containers-by-using-docker-compose"></a>Containers implementeren met behulp van Docker Compose
U kunt Docker Compose tooautomate Hallo implementatie en configuratie van meerdere containers. toodo is dus zorg ervoor dat een tunnel Secure Shell (SSH) is gemaakt en die Hallo DOCKER_HOST variabele is ingesteld (Zie vereisten Hallo hierboven).

Maak een docker-compose.yml-bestand op het lokale systeem. toodo, gebruiken deze [voorbeeld](https://raw.githubusercontent.com/rgardler/AzureDevTestDeploy/master/docker-compose.yml).

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

Voer `docker-compose up -d` toostart hello containerimplementaties:

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

Ten slotte Hallo lijst met actieve containers geretourneerd. Deze lijst geeft Hallo-containers die zijn geïmplementeerd met behulp van Docker Compose:

```bash
user@ubuntu:~/compose$ docker ps
CONTAINER ID        IMAGE               COMMAND                CREATED             STATUS              PORTS                     NAMES
caf185d221b7        adtd/web:0.1        "apache2-foreground"   2 minutes ago       Up About a minute   10.0.0.4:80->80/tcp       swarm-agent-3B7093B8-0/compose_web_1
040efc0ea937        adtd/rest:0.1       "catalina.sh run"      3 minutes ago       Up 2 minutes        10.0.0.4:8080->8080/tcp   swarm-agent-3B7093B8-0/compose_rest_1
```

U kunt uiteraard `docker-compose ps` tooexamine Hallo alleen containers die zijn gedefinieerd in uw `compose.yml` bestand.

## <a name="next-steps"></a>Volgende stappen
[Meer informatie over Docker Swarm](https://docs.docker.com/swarm/)

