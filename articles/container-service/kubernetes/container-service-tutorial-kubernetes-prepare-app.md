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
# <a name="create-container-images-toobe-used-with-azure-container-service"></a>Container installatiekopieën toobe gebruikt met Azure Container Service maken

In deze zelfstudie, deel 1 van zeven, is een toepassing met meerdere container klaar voor gebruik in Kubernetes. Stappen voltooid omvatten:  

> [!div class="checklist"]
> * Toepassingsbron klonen vanuit GitHub  
> * Maken van een installatiekopie van een container van Hallo toepassingsbron
> * Hallo toepassing testen in een lokale Docker-omgeving

Zodra de voltooid, is na toepassing hello toegankelijk zijn in uw lokale ontwikkelingsomgeving.

![Afbeelding van Kubernetes-cluster in Azure](media/container-service-kubernetes-tutorials/azure-vote.png)

In volgende zelfstudies Hallo container installatiekopie is geüploade tooan Azure Container register en klik vervolgens op uitvoeren in een Azure Kubernetes cluster wordt gehost.

## <a name="before-you-begin"></a>Voordat u begint

In deze zelfstudie wordt ervan uitgegaan dat u een basiskennis hebt van Docker-kernconcepten zoals containers, containerinstallatiekopieën en Docker-basisopdrachten. Zie, indien nodig, [Aan de slag met Docker]( https://docs.docker.com/get-started/) voor een uitleg van de basisprincipes van containers. 

toocomplete in deze zelfstudie, moet u een Docker-ontwikkelomgeving. Docker biedt pakketten die eenvoudig Docker op elke configureren op elk [Mac](https://docs.docker.com/docker-for-mac/)-, [Windows](https://docs.docker.com/docker-for-windows/)- of [Linux](https://docs.docker.com/engine/installation/#supported-platforms)-systeem.

## <a name="get-application-code"></a>Toepassingscode ophalen

Hallo-voorbeeldtoepassing die is gebruikt in deze zelfstudie is een eenvoudige stemmende app. Hallo toepassing bestaat uit een front-onderdeel en een back-end Redis-exemplaar. Hallo-webonderdeel wordt verpakt in een installatiekopie van een aangepaste container. Hallo Redis instantie gebruikt een installatiekopie van een ongewijzigd van Docker-Hub.  

Gebruik git toodownload een kopie van Hallo toepassing tooyour ontwikkelomgeving.

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

Binnen Hallo gekloonde directory broncode Hallo-toepassing, een vooraf gemaakte Docker compose bestands- en een manifestbestand Kubernetes. Deze bestanden zijn gebruikte toocreate activa in de gehele Hallo zelfstudie set. 

## <a name="create-container-images"></a>Maken van installatiekopieën van de container

[Docker Compose](https://docs.docker.com/compose/) kan tooautomate Hallo build buiten de container-installatiekopieën en Hallo-implementatie van meerdere container toepassingen gebruikt.

Hallo docker-compose.yml-bestand toocreate Hallo container installatiekopie uitvoert, downloaden Hallo Redis afbeelding, en Hallo toepassing starten.

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml up -d
```

Wanneer het voltooid, gebruikt u Hallo [docker-installatiekopieën](https://docs.docker.com/engine/reference/commandline/images/) opdracht toosee Hallo gemaakt installatiekopieën.

```bash
docker images
```

U ziet dat drie afbeeldingen gedownload of gemaakt. Hallo *azure stem voorgrond* installatiekopie Hallo toepassing bevat. Deze is afgeleid van Hallo *nginx flask* installatiekopie. Hallo Redis afbeelding is van Docker-Hub gedownload.

```bash
REPOSITORY                   TAG        IMAGE ID            CREATED             SIZE
azure-vote-front             latest     9cc914e25834        40 seconds ago      694MB
redis                        latest     a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask      788ca94b2313        9 months ago        694MB
```

Voer Hallo [docker ps](https://docs.docker.com/engine/reference/commandline/ps/) opdracht toosee Hallo actieve containers.

```bash
docker ps
```

Uitvoer:

```bash
CONTAINER ID        IMAGE             COMMAND                  CREATED             STATUS              PORTS                           NAMES
82411933e8f9        azure-vote-front  "/usr/bin/supervisord"   57 seconds ago      Up 30 seconds       443/tcp, 0.0.0.0:8080->80/tcp   azure-vote-front
b68fed4b66b6        redis             "docker-entrypoint..."   57 seconds ago      Up 30 seconds       0.0.0.0:6379->6379/tcp          azure-vote-back
```

## <a name="test-application-locally"></a>Toepassing lokaal testen

Blader toohttp://localhost:8080 toosee Hallo toepassing uitvoert.

![Afbeelding van Kubernetes-cluster in Azure](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="clean-up-resources"></a>Resources opschonen

Nu dat de functionaliteit van de toepassing is gevalideerd, kunt u actieve containers Hallo gestopt en verwijderd. Hallo container afbeeldingen niet verwijderen. Hallo *azure stem voorgrond* installatiekopie geüploade tooan Azure Container register exemplaar in de volgende zelfstudie Hallo is.

Hallo na toostop Hallo actieve containers worden uitgevoerd.

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml stop
```

Hallo gestopt containers met Hallo na de opdracht verwijderen.

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml rm
```

Is voltooid hebt u de installatiekopie van een container met hello Azure stem toepassing.

## <a name="next-steps"></a>Volgende stappen

Een toepassing is getest en installatiekopieën van de container gemaakt voor de toepassing hello in deze zelfstudie. Hallo stappen zijn voltooid:

> [!div class="checklist"]
> * Hallo-toepassingsbron klonen vanuit GitHub  
> * De installatiekopie van een container van toepassingsbron gemaakt
> * Hallo geteste toepassing in een lokale Docker-omgeving

Ga toohello volgende zelfstudie toolearn over het opslaan van installatiekopieën van de container in een Azure Container-register.

> [!div class="nextstepaction"]
> [Push-installatiekopieën tooAzure Container register](./container-service-tutorial-kubernetes-prepare-acr.md)
