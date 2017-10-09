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
# <a name="deploy-and-use-azure-container-registry"></a>Implementeren en gebruiken van Azure Container register

Azure Container register (ACR) is een register op basis van Azure, persoonlijke voor installatiekopieën van de Docker-container. Deze zelfstudie, deel uit van zeven, wordt begeleid bij het implementeren van een Azure Container register-exemplaar en een container installatiekopie tooit pushen. Stappen voltooid omvatten:

> [!div class="checklist"]
> * Implementatie van een exemplaar van Azure Container register (ACR)
> * Een installatiekopie van een container voor ACR-tagging
> * Hallo installatiekopie tooACR uploaden

In volgende zelfstudies is dit ACR-exemplaar geïntegreerd met een Azure Container Service Kubernetes-cluster voor het veilig uitvoeren van installatiekopieën van de container. 

## <a name="before-you-begin"></a>Voordat u begint

In Hallo [vorige zelfstudie](./container-service-tutorial-kubernetes-prepare-app.md), een installatiekopie van een container voor een eenvoudige toepassing voor Azure uw stem is gemaakt. In deze zelfstudie wordt deze installatiekopie tooan Azure Container register gepusht. Als u geen hello Azure stemmen app installatiekopie hebt gemaakt, te retourneren[zelfstudie 1 – installatiekopieën van de container maken](./container-service-tutorial-kubernetes-prepare-app.md). U kunt ook gedetailleerde Hallo stappen hier werken met een installatiekopie van de container.

Deze zelfstudie vereist dat u de versie van de Azure CLI Hallo 2.0.4 worden uitgevoerd of hoger. Voer `az --version` toofind Hallo versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli). 

## <a name="deploy-azure-container-registry"></a>Register met Azure Container implementeren

Wanneer u een Azure Container Registry implementeert, moet u eerst een resourcegroep. Een Azure-resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd.

Een resourcegroep maken met de Hallo [az groep maken](/cli/azure/group#create) opdracht. In dit voorbeeld wordt een resourcegroep met de naam *myResourceGroup* wordt gemaakt in Hallo *westeurope* regio.

```azurecli
az group create --name myResourceGroup --location westeurope
```

Maken van een Azure-Container registry Hello [az acr maken](/cli/azure/acr#create) opdracht. Hallo-naam van een registersleutel Container **moeten uniek zijn**.

```azurecli
az acr create --resource-group myResourceGroup --name <acrName> --sku Basic --admin-enabled true
```

In Hallo rest van deze zelfstudie gebruiken we 'acrname' als tijdelijke aanduiding voor Hallo register containernaam die u hebt gekozen.

## <a name="container-registry-login"></a>Container register aanmelding

U moet tooyour ACR exemplaar aanmelden voordat u installatiekopieën tooit. Gebruik Hallo [az acr aanmelding](https://docs.microsoft.com/en-us/cli/azure/acr#login) opdracht toocomplete Hallo-bewerking. U moet tooprovide Hallo unieke naam toohello container register opgegeven toen deze werd gemaakt.

```azurecli
az acr login --name <acrName>
```

Hallo opdracht retourneert een bericht 'Aanmelding geslaagd' eenmaal is voltooid.

## <a name="tag-container-images"></a>Installatiekopieën van de tag-container

Elke container installatiekopie moet toobe gemarkeerd met de Hallo loginServer naam van Hallo-register. Deze code wordt gebruikt voor routering wanneer container installatiekopieën tooan installatiekopie register worden gepusht.

een lijst met huidige installatiekopieën, gebruik Hallo toosee [docker-installatiekopieën](https://docs.docker.com/engine/reference/commandline/images/) opdracht.

```bash
docker images
```

Uitvoer:

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front             latest              4675398c9172        13 minutes ago      694MB
redis                        latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask               788ca94b2313        9 months ago        694MB
```

tooget hello loginServer naam, Hallo volgende opdracht uitvoeren.

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

Nu tag Hallo *azure stem voorgrond* installatiekopie met de Hallo loginServer van Hallo container register. Ook toe te voegen `:redis-v1` toohello einde van de naam van de installatiekopie Hallo. Deze code geeft Hallo installatiekopie versie.

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v1
```

Wanneer gecodeerd, uitvoeren [docker afbeeldingen] (https://docs.docker.com/engine/reference/commandline/images/) tooverify Hallo-bewerking.

```bash
docker images
```

Uitvoer:

```bash
REPOSITORY                                           TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front                                     latest              eaf2b9c57e5e        8 minutes ago       716 MB
mycontainerregistry082.azurecr.io/azure-vote-front   redis-v1            eaf2b9c57e5e        8 minutes ago       716 MB
redis                                                latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask                           flask               788ca94b2313        8 months ago        694 MB
```

## <a name="push-images-tooregistry"></a>Afbeeldingen tooregistry push

Hallo push *azure stem voorgrond* installatiekopie toohello register. 

Hallo volgende voorbeeld gebruikt, vervangen door Hallo ACR loginServer naam Hallo loginServer uit uw omgeving.

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v1
```

Dit duurt enkele minuten toocomplete.

## <a name="list-images-in-registry"></a>Lijst met afbeeldingen in register

een lijst met afbeeldingen die een pushbericht hebben ontvangen tooyour Azure-Container register, gebruiker Hallo tooreturn [az acr opslagplaats lijst](/cli/azure/acr/repository#list) opdracht. Hallo opdracht bijwerken met Hallo ACR-exemplaarnaam.

```azurecli
az acr repository list --name <acrName> --output table
```

Uitvoer:

```azurecli
Result
----------------
azure-vote-front
```

En vervolgens toosee Hallo labels voor een specifieke installatiekopie Hallo [az acr opslagplaats weergeven-labels](/cli/azure/acr/repository#show-tags) opdracht.

```azurecli
az acr repository show-tags --name <acrName> --repository azure-vote-front --output table
```

Uitvoer:

```azurecli
Result
--------
redis-v1
```

Bij zelfstudie voltooien is Hallo container installatiekopie opgeslagen in een persoonlijke Azure-Container register-exemplaar. Deze installatiekopie is in volgende zelfstudies uit ACR tooa Kubernetes cluster geïmplementeerd.

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie is een Azure Container Registry voorbereid voor gebruik in een cluster ACS Kubernetes. Hallo stappen zijn voltooid:

> [!div class="checklist"]
> * Een exemplaar van het register van Azure-Container geïmplementeerd
> * Een installatiekopie van een container voor ACR met tags
> * Geüploade Hallo installatiekopie tooACR

Ga toohello volgende zelfstudie toolearn over het implementeren van een cluster Kubernetes in Azure.

> [!div class="nextstepaction"]
> [Kubernetes-cluster implementeren](./container-service-tutorial-kubernetes-deploy-cluster.md)