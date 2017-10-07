---
title: aaaAzure Containerexemplaren zelfstudie - app implementeren | Microsoft Docs
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
ms.openlocfilehash: b9fb098d9491e1073f0be4b14a0b9b1a18f16095
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-container-tooazure-container-instances"></a>Een container tooAzure Containerexemplaren implementeren

Dit is Hallo laatste van een zelfstudie drie delen. In vorige gedeelten [is gemaakt met een installatiekopie van een container](container-instances-tutorial-prepare-app.md) en [tooan Azure Container register gepusht](container-instances-tutorial-prepare-acr.md). In deze sectie is Hallo-zelfstudie voltooid door het implementeren van Hallo container tooAzure Containerexemplaren. Stappen voltooid omvatten:

> [!div class="checklist"]
> * Het definiëren van de containergroep van een met een Azure Resource Manager-sjabloon
> * Hallo containergroep met behulp van Azure CLI Hallo implementeren
> * Container-logboeken bekijken

## <a name="deploy-hello-container-using-hello-azure-cli"></a>Met behulp van Azure CLI Hallo Hallo-container implementeren

Hello Azure CLI kunt implementatie van een container tooAzure Containerexemplaren in één opdracht. Aangezien Hallo container installatiekopie wordt gehost in Hallo persoonlijke Azure-Container register, moet u Hallo referenties vereist tooaccess opnemen deze. Indien nodig, kunt u ze opvragen, zoals hieronder wordt weergegeven.

Container register login-server (update met de registernaam van uw):

```azurecli-interactive
az acr show --name <acrName> --query loginServer
```

Container register wachtwoord:

```azurecli-interactive
az acr credential show --name <acrName> --query "passwords[0].value"
```

toodeploy gevraagd om uw installatiekopie container uit Hallo container register met een resource van 1 CPU-kern tot 1GB geheugen, Hallo volgende opdracht uitvoeren:

```azurecli-interactive
az container create --name aci-tutorial-app --image <acrLoginServer>/aci-tutorial-app:v1 --cpu 1 --memory 1 --registry-password <acrPassword> --ip-address public -g myResourceGroup
```

Binnen enkele seconden ontvangt u een eerste reactie van Azure Resource Manager. tooview hello staat van Hallo-implementatie gebruiken:

```azurecli-interactive
az container show --name aci-tutorial-app --resource-group myResourceGroup --query state
```

U kunt doorgaan met deze opdracht wordt uitgevoerd totdat Hallo status van verandert *in behandeling* te*met*. Vervolgens kunnen we doorgaan.

## <a name="view-hello-application-and-container-logs"></a>Hallo toepassings- en logboekbestanden weergeven

Zodra het Hallo-implementatie is gelukt, opent u uw browser toohello IP-adres wordt weergegeven in de uitvoer van de volgende opdracht Hallo Hallo:

```bash
az container show --name aci-tutorial-app --resource-group myResourceGroup --query ipAddress.ip
```

```json
"13.88.176.27"
```

![Hallo wereld-app in Hallo-browser][aci-app-browser]

U kunt ook Hallo logboekuitvoer van Hallo container bekijken:

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

In deze zelfstudie maakt voltooid u Hallo-proces voor het implementeren van uw containers tooAzure Containerexemplaren. Hallo stappen zijn voltooid:

> [!div class="checklist"]
> * Hallo-container van het gebruik van hello Azure Container register implementeren hello Azure CLI
> * Bekijkt hello toepassing in Hallo-browser
> * Weergave Hallo container Logboeken

<!-- LINKS -->
[prepare-app]: ./container-instances-tutorial-prepare-app.md

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png
