---
title: aaaCreate persoonlijke Docker-container register - Azure CLI | Microsoft Docs
description: Aan de slag maken en beheren van persoonlijke Docker-container registers Hello Azure CLI 2.0
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 29e20d75-bf39-4f7d-815f-a2e47209be7d
ms.service: container-registry
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/06/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f0d876a70b71a5e1bd564fbc9198f693dfe8a347
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-cli-20"></a>Maken van een persoonlijke Docker-container register met hello Azure CLI 2.0
Met de opdrachten in Hallo [Azure CLI 2.0](https://github.com/Azure/azure-cli) toocreate een register container en beheren van de instellingen van uw Linux, Mac of Windows-computer. U kunt ook maken en beheren van container registers met Hallo [Azure-portal](container-registry-get-started-portal.md) of programmatisch met Hallo Container register [REST-API](https://go.microsoft.com/fwlink/p/?linkid=834376).


* Zie voor de achtergrond en concepten [Hallo overzicht](container-registry-intro.md)
* Voor meer informatie over Container register CLI-opdrachten (`az acr` opdrachten), doorgegeven Hallo `-h` parameter tooany opdracht.


## <a name="prerequisites"></a>Vereisten
* **Azure CLI 2.0**: tooinstall en aan de slag met Hallo CLI 2.0, Zie Hallo [installatie-instructies](/cli/azure/install-azure-cli). Meld u bij de Azure-abonnement tooyour door te voeren `az login`. Zie voor meer informatie [aan de slag met Hallo CLI 2.0](/cli/azure/get-started-with-azure-cli).
* **Resourcegroep**: maak eerst een [resourcegroep](../azure-resource-manager/resource-group-overview.md#resource-groups) voordat u een containerregister maakt of gebruik een bestaande resourcegroep. Zorg ervoor dat Hallo resourcegroep bevindt zich in een locatie waar Hallo Container Registry-service is [beschikbaar](https://azure.microsoft.com/regions/services/). een resource-groep met toocreate Hallo CLI 2.0, Zie [Hallo CLI 2.0 verwijzing](/cli/azure/group).
* **Storage-account** (optioneel): Maak een standaard Azure [opslagaccount](../storage/common/storage-introduction.md) tooback Hallo container register in Hallo dezelfde locatie. Als u een opslagaccount niet opgeven bij het maken van een register met `az acr create`, Hallo opdracht maakt u een voor u. een storage-account met toocreate Hallo CLI 2.0, Zie [Hallo CLI 2.0 verwijzing](/cli/azure/storage/account). Premium-opslag wordt momenteel niet ondersteund.
* **Service-principal** (optioneel): wanneer u een register met CLI hello maakt, standaard het is niet ingesteld voor toegang. Afhankelijk van uw behoeften kunt u een bestaande Azure Active Directory service principal tooa register toewijzen (of maken en toewijzen van een nieuw), of van het register Hallo beheerder gebruikersaccount in te schakelen. Zie Hallo secties verderop in dit artikel. Zie voor meer informatie over toegang tot het register, [verifiëren met Hallo container register](container-registry-authentication.md).

## <a name="create-a-container-registry"></a>Een containerregister maken
Voer Hallo `az acr create` opdracht toocreate een container-register.

> [!TIP]
> Geef bij het maken van een register een unieke domeinnaam op het hoogste niveau op, bestaande uit alleen letters en cijfers. naam van de Hallo register in Hallo voorbeelden is `myRegistry1`, maar vervangen door een unieke naam van uw eigen.
>
>

Hallo van de volgende opdracht maakt gebruik van Hallo minimale parameters toocreate container register `myRegistry1` in de resourcegroep Hallo `myResourceGroup`, en het gebruik van Hallo *Basic* sku:

```azurecli
az acr create --name myRegistry1 --resource-group myResourceGroup --sku Basic
```

* `--storage-account-name` is optioneel. Als dat niet is opgegeven, een opslagaccount is gemaakt met een naam die bestaan uit Hallo registernaam en een tijdstempel in Hallo opgegeven resourcegroep.

Bij Hallo register wordt gemaakt, is het Hallo-uitvoer vergelijkbare toohello volgende:

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-06T18:36:29.124842+00:00",
  "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myResourceGroup/providers/Microsoft.ContainerRegistry
/registries/myRegistry1",
  "location": "southcentralus",
  "loginServer": "myregistry1.azurecr.io",
  "name": "myRegistry1",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "myregistry123456789"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}

```


Belangrijk:

* `id`-ID voor Hallo register in uw abonnement, u moet als u wilt dat een service-principal tooassign.
* `loginServer`-Hallo volledig gekwalificeerde naam die u te opgeeft[toohello register aanmelden](container-registry-authentication.md). In dit voorbeeld is de naam van de Hallo `myregistry1.exp.azurecr.io` (alle kleine letters).

## <a name="assign-a-service-principal"></a>Een service-principal toewijzen
CLI 2.0 opdrachten tooassign een Azure Active Directory-service-principal tooa registry gebruiken. Hallo service-principal in deze voorbeelden is toegewezen rol van eigenaar hello, maar u kunt toewijzen [andere rollen](../active-directory/role-based-access-control-configure.md) als u wilt.

### <a name="create-a-service-principal-and-assign-access-toohello-registry"></a>Een service-principal maken en toewijzen van toegang toohello register
In Hallo volgende opdracht, een nieuwe service-principal eigenaar rol toegang toohello register-id doorgegeven Hello toegewezen `--scopes` parameter. Geef een sterk wachtwoord Hello `--password` parameter.

```azurecli
az ad sp create-for-rbac --scopes /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --password myPassword
```



### <a name="assign-an-existing-service-principal"></a>Een bestaande service-principal toewijzen
Als u al een service-principal en tooassign wilt deze eigenaar rol toegang toohello register, uitvoeren van een opdracht vergelijkbare toohello voorbeeld te volgen. U Hallo service principal app-ID met Hallo doorgeeft `--assignee` parameter:

```azurecli
az role assignment create --scope /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --assignee myAppId
```



## <a name="manage-admin-credentials"></a>Beheerreferenties beheren
Er wordt automatisch een beheeraccount gemaakt voor elk containerregister. Dit account is standaard uitgeschakeld. Hallo volgen voorbeelden `az acr` CLI-opdrachten toomanage Hallo beheerdersreferenties voor de container-register.

### <a name="obtain-admin-user-credentials"></a>Beheerreferenties ophalen
```azurecli
az acr credential show -n myRegistry1
```

### <a name="enable-admin-user-for-an-existing-registry"></a>Beheerder inschakelen voor een bestaand register
```azurecli
az acr update -n myRegistry1 --admin-enabled true
```

### <a name="disable-admin-user-for-an-existing-registry"></a>Beheerder uitschakelen voor een bestaand register
```azurecli
az acr update -n myRegistry1 --admin-enabled false
```

## <a name="list-images-and-tags"></a>Installatiekopieën en tags weergeven
Gebruik Hallo `az acr` CLI-opdrachten tooquery Hallo installatiekopieën en labels in een opslagplaats.

> [!NOTE]
> Container register biedt momenteel geen ondersteuning voor Hallo `docker search` opdracht tooquery voor afbeeldingen en labels.


### <a name="list-repositories"></a>Opslagplaatsen weergeven
Hallo volgende voorbeeld worden Hallo-opslagplaatsen in een register, in JSON (JavaScript Object Notation)-indeling:

```azurecli
az acr repository list -n myRegistry1 -o json
```

### <a name="list-tags"></a>Tags weergeven
Hallo volgende voorbeeld wordt een lijst Hallo labels op Hallo **samples/nginx** -opslagplaats, in JSON-indeling:

```azurecli
az acr repository show-tags -n myRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a>Volgende stappen
* [Uw eerste installatiekopie met behulp van Docker CLI Hallo push](container-registry-get-started-docker-cli.md)
