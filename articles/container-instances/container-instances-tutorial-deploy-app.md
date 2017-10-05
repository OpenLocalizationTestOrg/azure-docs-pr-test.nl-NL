---
title: Zelfstudie voor Azure Containerexemplaren - app implementeren | Microsoft Docs
description: Zelfstudie voor Azure Containerexemplaren - app implementeren
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 54151a5c1850ab7120fe666a46dc5dc99c0f5157
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-a-container-to-azure-container-instances"></a>Een container implementeren naar Azure Containerexemplaren

Dit is de laatste van een zelfstudie drie delen. In vorige gedeelten [is gemaakt met een installatiekopie van een container](container-instances-tutorial-prepare-app.md) en [naar een Azure Container Registry gepusht](container-instances-tutorial-prepare-acr.md). Deze sectie is de zelfstudie voltooid door het implementeren van de container op exemplaren van Azure-Container. Stappen voltooid omvatten:

> [!div class="checklist"]
> * Het definiëren van de containergroep van een met een Azure Resource Manager-sjabloon
> * Implementatie van de containergroep met de Azure CLI
> * Container-logboeken bekijken

## <a name="deploy-the-container-using-the-azure-cli"></a>De container met de Azure CLI implementeren

De Azure CLI kunt de implementatie van een container voor exemplaren van Azure-Container in één opdracht. Omdat de container-installatiekopie wordt gehost in het persoonlijke Azure-Container register, moet u de referenties voor toegang tot dit opnemen. Indien nodig, kunt u ze opvragen, zoals hieronder wordt weergegeven.

Container register login-server (update met de registernaam van uw):

```azurecli-interactive
az acr show --name <acrName> --query loginServer
```

Container register wachtwoord:

```azurecli-interactive
az acr credential show --name <acrName> --query "passwords[0].value"
```

Voor het implementeren van uw installatiekopie container uit het register van de container met een resource-aanvraag van het CPU-kern 1 en 1GB geheugen, moet u de volgende opdracht uitvoeren:

```azurecli-interactive
az container create --name aci-tutorial-app --image <acrLoginServer>/aci-tutorial-app:v1 --cpu 1 --memory 1 --registry-password <acrPassword> --ip-address public -g myResourceGroup
```

Binnen enkele seconden ontvangt u een eerste reactie van Azure Resource Manager. Als u wilt weergeven van de status van de implementatie, gebruiken:

```azurecli-interactive
az container show --name aci-tutorial-app --resource-group myResourceGroup --query state
```

U kunt doorgaan met deze opdracht wordt uitgevoerd totdat de status van verandert *in behandeling* naar *met*. Vervolgens kunnen we doorgaan.

## <a name="view-the-application-and-container-logs"></a>Bekijk de logboeken toepassingen en container

Zodra de implementatie is geslaagd, opent u uw browser naar de IP-adres dat wordt weergegeven in de uitvoer van de volgende opdracht:

```bash
az container show --name aci-tutorial-app --resource-group myResourceGroup --query ipAddress.ip
```

```json
"13.88.176.27"
```

![Hallo wereld-app in de browser][aci-app-browser]

U kunt ook de uitvoer van de container bekijken:

```azurecli-interactive
az container logs --name aci-tutorial-app -g myResourceGroup
```

Uitvoer:

```bash
listening on port 80
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://13.88.176.27/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie maakt voltooid u het proces voor het implementeren van uw containers op Azure Containerexemplaren. De volgende stappen zijn voltooid:

> [!div class="checklist"]
> * Implementatie van de container van het Azure-Container register met de Azure CLI
> * De toepassing bekijken in de browser
> * De container logboeken bekijken

<!-- LINKS -->
[prepare-app]: ./container-instances-tutorial-prepare-app.md

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png
