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
# <a name="create-container-for-deployment-tooazure-container-instances"></a>Container voor implementatie tooAzure Containerexemplaren maken

Met Azure Container Instances kunt u Docker-containers implementeren in de Azure-infrastructuur zonder virtuele machines in te richten of gebruik te maken van een service op een hoger niveau. In deze zelfstudie maakt u een eenvoudige webtoepassing in Node.js en verpakt u deze in een container die kan worden uitgevoerd met behulp van Azure Container Instances. Het volgende wordt besproken:

> [!div class="checklist"]
> * Toepassingsbron klonen vanuit GitHub  
> * Containerinstallatiekopieën van de toepassingsbron maken
> * Hallo installatiekopieën testen in een lokale Docker-omgeving

In volgende zelfstudies leert u uploaden van uw installatiekopie tooan Azure Container register, en vervolgens implementeren tooAzure Containerexemplaren.

## <a name="before-you-begin"></a>Voordat u begint

In deze zelfstudie wordt ervan uitgegaan dat u een basiskennis hebt van Docker-kernconcepten zoals containers, containerinstallatiekopieën en Docker-basisopdrachten. Zie, indien nodig, [Aan de slag met Docker]( https://docs.docker.com/get-started/) voor een uitleg van de basisprincipes van containers. 

toocomplete in deze zelfstudie, moet u een Docker-ontwikkelomgeving. Docker biedt pakketten die eenvoudig Docker op elke configureren op elk [Mac](https://docs.docker.com/docker-for-mac/)-, [Windows](https://docs.docker.com/docker-for-windows/)- of [Linux](https://docs.docker.com/engine/installation/#supported-platforms)-systeem.

## <a name="get-application-code"></a>Toepassingscode ophalen

Hallo-voorbeeld in deze zelfstudie bevat een eenvoudige webtoepassing die is ingebouwd in [Node.js](http://nodejs.org). Hallo-app fungeert een statische HTML-pagina en uitziet:

![Zelfstudie-app weergegeven in browser][aci-tutorial-app]

Gebruik git toodownload Hallo voorbeeld:

```bash
git clone https://github.com/Azure-Samples/aci-helloworld.git
```

## <a name="build-hello-container-image"></a>Hallo container installatiekopie maken

Hallo Dockerfile in het Hallo-repo-voorbeeld ziet u hoe Hallo container wordt gemaakt. Het starten van een [officiële Node.js installatiekopie] [ dockerhub-nodeimage] op basis van [Alpine Linux](https://alpinelinux.org/), een kleine distributie die is uitermate geschikt toouse met containers. Vervolgens Hallo toepassingsbestanden kopieert naar Hallo-container, afhankelijkheden met Hallo knooppunt Package Manager is geïnstalleerd en ten slotte start Hallo-toepassing.

```
FROM node:8.2.0-alpine
RUN mkdir -p /usr/src/app
COPY ./app/* /usr/src/app/
WORKDIR /usr/src/app
RUN npm install
CMD node /usr/src/app/index.js
```

Gebruik Hallo `docker build` toocreate Hallo container opdrachtafbeelding, labelen als *aci-zelfstudie-app*:

```bash
docker build ./aci-helloworld -t aci-tutorial-app
```

Gebruik Hallo `docker images` toosee Hallo gebouwd installatiekopie:

```bash
docker images
```

Uitvoer:

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

## <a name="run-hello-container-locally"></a>Hallo-container lokaal uitvoeren

Voordat u probeert Hallo container tooAzure Containerexemplaren implementeren, het lokaal uitvoeren tooconfirm of dit werkt. Hallo `-d` switch kunt uitvoeren op de achtergrond Hallo Hallo-container terwijl `-p` kunt u een willekeurige poort op uw compute tooport 80 in Hallo container toomap.

```bash
docker run -d -p 8080:80 aci-tutorial-app
```

Open Hallo browser toohttp://localhost:8080 tooconfirm die container Hallo wordt uitgevoerd.

![Actieve Hallo app lokaal in de browser Hallo][aci-tutorial-app-local]

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie maakt u een container-installatiekopie die geïmplementeerde tooAzure Containerexemplaren kan worden gemaakt. Hallo stappen zijn voltooid:

> [!div class="checklist"]
> * Hallo-toepassingsbron klonen vanuit GitHub  
> * Containerinstallatiekopieën van de toepassingsbron maken
> * Hallo container lokaal testen

Ga toohello volgende zelfstudie toolearn over het opslaan van installatiekopieën van de container in een Azure Container-register.

> [!div class="nextstepaction"]
> [Push-installatiekopieën tooAzure Container register](./container-instances-tutorial-prepare-acr.md)

<!-- LINKS -->
[dockerhub-nodeimage]: https://hub.docker.com/r/library/node/tags/8.2.0-alpine/

<!--- IMAGES --->
[aci-tutorial-app]:./media/container-instances-quickstart/aci-app-browser.png
[aci-tutorial-app-local]: ./media/container-instances-tutorial-prepare-app/aci-app-browser-local.png