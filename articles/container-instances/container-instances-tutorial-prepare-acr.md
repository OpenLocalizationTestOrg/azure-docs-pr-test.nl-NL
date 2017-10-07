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
# <a name="deploy-and-use-azure-container-registry"></a>Implementeren en gebruiken van Azure Container register

Dit maakt deel uit van een zelfstudie drie delen. In Hallo [vorige stap](./container-instances-tutorial-prepare-app.md), een installatiekopie van een container is gemaakt voor een eenvoudige webtoepassing geschreven in [Node.js](http://nodejs.org). In deze zelfstudie wordt deze installatiekopie tooan Azure Container register gepusht. Als u geen Hallo container installatiekopie hebt gemaakt, te retourneren[zelfstudie 1 – afbeelding van de container maken](./container-instances-tutorial-prepare-app.md). 

Hello Azure Container register is een register op basis van Azure, persoonlijke voor installatiekopieën van de Docker-container. Deze zelfstudie wordt begeleid bij het implementeren van een Azure Container register-exemplaar en een container installatiekopie tooit pushen. Stappen voltooid omvatten:

> [!div class="checklist"]
> * Een exemplaar van Azure Container register implementeren
> * Afbeelding van de container voor Azure Container register tagging
> * Afbeelding tooAzure Container register uploaden

In volgende zelfstudies leert implementeren u Hallo container van uw persoonlijke register tooAzure Containerexemplaren.

## <a name="before-you-begin"></a>Voordat u begint

Deze zelfstudie vereist dat u de versie van de Azure CLI Hallo 2.0.4 worden uitgevoerd of hoger. Voer `az --version` toofind Hallo versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).

## <a name="deploy-azure-container-registry"></a>Register met Azure Container implementeren

Wanneer u een Azure Container Registry implementeert, moet u eerst een resourcegroep. Een Azure-resourcegroep is een logische verzameling in welke Azure resources worden geïmplementeerd en beheerd.

Een resourcegroep maken met de Hallo [az groep maken](/cli/azure/group#create) opdracht. In dit voorbeeld wordt een resourcegroep met de naam *myResourceGroup* wordt gemaakt in Hallo *eastus* regio.

```azurecli
az group create --name myResourceGroup --location eastus
```

Maken van een Azure-Container registry Hello [az acr maken](/cli/azure/acr#create) opdracht. Hallo-naam van een registersleutel Container **moeten uniek zijn**. In Hallo voorbeeld te volgen, gebruiken we de naam van de Hallo *mycontainerregistry082*.

```azurecli
az acr create --resource-group myResourceGroup --name mycontainerregistry082 --sku Basic --admin-enabled true
```

In de rest van de Hallo van deze zelfstudie, gebruiken we `<acrname>` als tijdelijke aanduiding voor Hallo register containernaam die u hebt gekozen.

## <a name="container-registry-login"></a>Container register aanmelding

U moet tooyour ACR exemplaar aanmelden voordat u installatiekopieën tooit. Gebruik Hallo [az acr aanmelding](https://docs.microsoft.com/en-us/cli/azure/acr#login) opdracht toocomplete Hallo-bewerking. U moet tooprovide Hallo unieke naam toohello container register opgegeven toen deze werd gemaakt.

```azurecli
az acr login --name <acrName>
```

Hallo opdracht retourneert een bericht 'Aanmelding geslaagd' eenmaal is voltooid.

## <a name="tag-container-image"></a>De installatiekopie van de tag-container

de installatiekopie van een container van een persoonlijke register toodeploy, Hallo installatiekopie moet toobe gemarkeerd met de Hallo `loginServer` naam van het Hallo-register.

een lijst met huidige installatiekopieën, gebruik Hallo toosee `docker images` opdracht.

```bash
docker images
```

Uitvoer:

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

tooget hello loginServer naam, Hallo volgende opdracht uitvoeren.

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

Tag Hallo *aci-zelfstudie-app* installatiekopie met de Hallo loginServer van Hallo container register. Ook toe te voegen `:v1` toohello einde van de naam van de installatiekopie Hallo. Deze code geeft Hallo installatiekopie-versienummer.

```bash
docker tag aci-tutorial-app <acrLoginServer>/aci-tutorial-app:v1
```

Uitvoeren zodra gecodeerd, `docker images` tooverify Hallo-bewerking.

```bash
docker images
```

Uitvoer:

```bash
REPOSITORY                                                TAG                 IMAGE ID            CREATED             SIZE
aci-tutorial-app                                          latest              5c745774dfa9        39 seconds ago      68.1 MB
mycontainerregistry082.azurecr.io/aci-tutorial-app        v1                  a9dace4e1a17        7 minutes ago       68.1 MB
```

## <a name="push-image-tooazure-container-registry"></a>Afbeelding tooAzure Container register push

Hallo push *aci-zelfstudie-app* installatiekopie toohello register.

Hallo volgende voorbeeld gebruikt, vervangen door register Hallo-loginServer containernaam Hallo loginServer uit uw omgeving.

```bash
docker push <acrLoginServer>/aci-tutorial-app:v1
```

## <a name="list-images-in-azure-container-registry"></a>Lijst met afbeeldingen in Azure Container register

een lijst met afbeeldingen die een pushbericht hebben ontvangen tooyour Azure-Container register, gebruiker Hallo tooreturn [az acr opslagplaats lijst](/cli/azure/acr/repository#list) opdracht. Hallo opdracht bijwerken met de containernaam register Hallo.

```azurecli
az acr repository list --name <acrName> --output table
```

Uitvoer:

```azurecli
Result
----------------
aci-tutorial-app
```

En vervolgens toosee Hallo labels voor een specifieke installatiekopie Hallo [az acr opslagplaats weergeven-labels](/cli/azure/acr/repository#show-tags) opdracht.

```azurecli
az acr repository show-tags --name <acrName> --repository aci-tutorial-app --output table
```

Uitvoer:

```azurecli
Result
--------
v1
```

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie een Azure Container Registry is voorbereid voor gebruik met Azure Containerexemplaren en Hallo container installatiekopie is gepusht. Hallo stappen zijn voltooid:

> [!div class="checklist"]
> * Een exemplaar van Azure Container register implementeren
> * Afbeelding van de container voor Azure Container register tagging
> * Afbeelding tooAzure Container register uploaden

Toohello volgende zelfstudie toolearn over het implementeren van Hallo container tooAzure met Azure Container instanties gaan.

> [!div class="nextstepaction"]
> [Containers tooAzure Containerexemplaren implementeren](./container-instances-tutorial-deploy-app.md)
