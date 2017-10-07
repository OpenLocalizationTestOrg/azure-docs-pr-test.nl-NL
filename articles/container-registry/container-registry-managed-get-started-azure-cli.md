---
title: aaaCreate persoonlijke Docker-container register - Azure CLI | Microsoft Docs
description: Aan de slag maken en beheren van persoonlijke Docker-container registers Hello Azure CLI 2.0
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: na
tags: 
keywords: 
ms.assetid: 29e20d75-bf39-4f7d-815f-a2e47209be7d
ms.service: container-registry
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: nepeters
ms.custom: na
ms.openlocfilehash: 2cadf42db0681a09c95486510f1e65c6f87c5280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-container-registry-using-hello-azure-cli"></a>Maken van een beheerde container register hello Azure CLI gebruiken

Azure Container Registry is een beheerde service voor Docker-containerregisters die wordt gebruikt voor het opslaan van installatiekopieën van persoonlijke Docker-containers. Deze handleiding-gegevens voor het maken van een beheerde Azure-Container register-exemplaar met gebruikmaking van hello Azure CLI.

Beheerde Azure-containerregisters zijn nog in preview en zijn niet in alle regio's beschikbaar.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Als u tooinstall kiest en Hallo CLI lokaal gebruiken, is deze snelstartgids vereist dat u de versie van de Azure CLI Hallo 2.0.4 worden uitgevoerd of hoger. Voer `az --version` toofind Hallo versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli). 

## <a name="create-a-resource-group"></a>Een resourcegroep maken

Een resourcegroep maken met de Hallo [az groep maken](/cli/azure/group#create) opdracht. Een Azure-resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd. 

Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *westcentralus* locatie.

```azurecli-interactive 
az group create --name myResourceGroup --location westcentralus
```

## <a name="create-a-container-registry"></a>Een containerregister maken

ACR-exemplaar met behulp van Hallo maken [az acr maken](/cli/azure/acr#create) opdracht.

> [!NOTE]
> Geef bij het maken van een register een unieke domeinnaam op het hoogste niveau op, bestaande uit alleen letters en cijfers.

 naam van de Hallo register in Hallo voorbeeld is *myContainerRegistry1*, vervangen door een unieke naam van uw eigen.

```azurecli
az acr create --name myContainerRegistry1 --resource-group myResourceGroup --sku Managed_Standard
```

Bij Hallo register wordt gemaakt, is het Hallo-uitvoer vergelijkbare toohello volgende:

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-29T04:50:28.607134+00:00",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myContainerRegistry1",
  "location": "westcentralus",
  "loginServer": "mycontainerregistry1.azurecr.io",
  "name": "myContainerRegistry1",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "sku": {
    "name": "Managed_Standard",
    "tier": "Managed"
  },
  "storageAccount": null,
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

## <a name="log-in-tooacr-instance"></a>Meld u bij tooACR exemplaar

Voordat u pushen en installatiekopieën van de container binnenhalen, moet u zich aanmeldt toohello ACR-exemplaar. dus gebruiken Hallo toodo [az acr aanmelding](/cli/azure/acr#login) opdracht.

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

Hallo opdracht retourneert een bericht 'Aanmelding geslaagd' eenmaal is voltooid.

## <a name="use-azure-container-registry"></a>Azure Container Registry gebruiken

### <a name="list-container-images"></a>Containerinstallatiekopieën opvragen

Gebruik Hallo `az acr` CLI-opdrachten tooquery Hallo installatiekopieën en labels in een opslagplaats.

> [!NOTE]
> Container register biedt momenteel geen ondersteuning voor Hallo `docker search` opdracht tooquery voor afbeeldingen en labels.

### <a name="list-repositories"></a>Opslagplaatsen weergeven

Hallo volgende voorbeeld worden Hallo-opslagplaatsen in een register, in JSON (JavaScript Object Notation)-indeling:

```azurecli
az acr repository list -n myContainerRegistry1 -o json
```

### <a name="list-tags"></a>Tags weergeven

Hallo volgende voorbeeld wordt een lijst Hallo labels op Hallo **samples/nginx** -opslagplaats, in JSON-indeling:

```azurecli
az acr repository show-tags -n myContainerRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a>Volgende stappen

In deze snel starten, kunt u een beheerde Azure-Container register-exemplaar met gebruikmaking van hello Azure CLI hebt gemaakt.

> [!div class="nextstepaction"]
> [Uw eerste installatiekopie met behulp van Docker CLI Hallo push](container-registry-get-started-docker-cli.md)
