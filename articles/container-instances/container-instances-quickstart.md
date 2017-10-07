---
title: aaaCreate uw eerste Azure-Containerexemplaren container | Azure Docs
description: Azure Container Instances implementeren en ermee aan de slag gaan
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
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: b57c52714933bd3b28c44d33f9af7cd1f23fb951
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-container-in-azure-container-instances"></a>Uw eerste container maken in Azure Container Instances

Azure Containerexemplaren maakt het eenvoudig toocreate en beheer containers in Azure. In deze snel starten, wordt u een container maken in Azure en maak deze toohello zichtbaar internet met een openbaar IP-adres. Deze bewerking wordt uitgevoerd in één opdracht. Binnen een paar seconden ziet u dit in uw browser:

![App die is geïmplementeerd met Azure Container Instances, weergegeven in de browser][aci-app-browser]

Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) aan voordat u begint.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Als u tooinstall kiest en Hallo CLI lokaal gebruiken, is deze snelstartgids vereist dat u de versie van de Azure CLI Hallo 2.0.12 worden uitgevoerd of hoger. Voer `az --version` toofind Hallo versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli). 

## <a name="create-a-resource-group"></a>Een resourcegroep maken

Azure Container Instances zijn Azure-resources en moeten worden geplaatst in een Azure-resourcegroep, een logische verzameling waarin Azure resources worden geïmplementeerd en beheerd.

Een resourcegroep maken met de Hallo [az groep maken](/cli/azure/group#create) opdracht. 

Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *eastus* locatie.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-container"></a>Een container maken

U kunt een container maken door een naam, een Docker-installatiekopie en een Azure-resourcegroep op te geven. Hallo container toohello kan eventueel worden blootgesteld internet met een openbaar IP-adres. We gebruiken in dit geval een container die als host fungeert voor een zeer eenvoudige web-app die is geschreven in [Node.js](http://nodejs.org).

```azurecli-interactive
az container create --name mycontainer --image microsoft/aci-helloworld --resource-group myResourceGroup --ip-address public 
```

Binnen enkele seconden krijgt u een antwoord tooyour-aanvraag. In eerste instantie Hallo container zich in een **maken** staat, maar moet worden gestart binnen een paar seconden. U kunt met behulp van Hallo Hallo-status controleren `show` opdracht:

```azurecli-interactive
az container show --name mycontainer --resource-group myResourceGroup
```

Aan de onderkant van de Hallo van Hallo uitvoer ziet u de Inrichtingsstatus Hallo-container en het IP-adres:

```json
...
"ipAddress": {
      "ip": "13.88.8.148",
      "ports": [
        {
          "port": 80,
          "protocol": "TCP"
        }
      ]
    },
    "osType": "Linux",
    "provisioningState": "Succeeded"
...
```

Zodra het Hallo-container verplaatst toohello **geslaagd** staat, kunt u deze op Hallo browser Hallo IP-adres opgegeven bereiken. 

![App die is geïmplementeerd met Azure Container Instances, weergegeven in de browser][aci-app-browser]

## <a name="pull-hello-container-logs"></a>Pull-hallo container Logboeken

U kunt pull-logboeken voor Hallo-container hebt gemaakt met behulp van Hallo Hallo `logs` opdracht:

```azurecli-interactive
az container logs --name mycontainer --resource-group myResourceGroup
```

Uitvoer:

```bash
listening on port 80
::ffff:10.240.255.105 - - [21/Jul/2017:00:01:46 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.255.105 - - [21/Jul/2017:00:01:46 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://104.210.39.122/" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="delete-hello-container"></a>Hallo-container verwijderen

Wanneer u klaar bent met het Hallo-container, kunt u met behulp van Hallo verwijderen `delete` opdracht:

```azurecli-interactive
az container delete --name mycontainer --resource-group myResourceGroup
```

## <a name="next-steps"></a>Volgende stappen

Alle Hallo code voor de Hallo container gebruikt in deze snel starten [op GitHub][app-github-repo], samen met de Dockerfile. Als u tootry zelf bouwen en implementeren van tooAzure Container-exemplaren die gebruikmaken van hello Azure Container register wilt, blijven toohello Azure Containerexemplaren zelfstudie.

> [!div class="nextstepaction"]
> [Zelfstudies voor Azure Container Instances](./container-instances-tutorial-prepare-app.md)


<!-- LINKS -->
[app-github-repo]: https://github.com/Azure-Samples/aci-helloworld.git

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png