---
title: aaaCreate persoonlijke Docker-register - Azure-portal | Microsoft Docs
description: Maken en beheren van persoonlijke Docker-container registers Hello Azure-portal aan de slag
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: na
tags: 
keywords: 
ms.assetid: 53a3b3cb-ab4b-4560-bc00-366e2759f1a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: nepeters
ms.custom: na
ms.openlocfilehash: cf3ce0dcf3036d0e9cd1eaf01721deccb00248d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-container-registry-using-hello-azure-portal"></a>Maken van een beheerde container register met hello Azure-portal

Azure Container Registry is een beheerde service voor Docker-containerregisters die wordt gebruikt voor het opslaan van installatiekopieën van persoonlijke Docker-containers. Deze handleiding-gegevens voor het maken van een beheerde Azure-Container register-exemplaar met gebruikmaking van hello Azure-portal.

Beheerde Azure-containerregisters zijn nog in preview en zijn niet in alle regio's beschikbaar.

## <a name="log-in-tooazure"></a>Meld u bij tooAzure

Toohello aanmelden met Azure-portal op http://portal.azure.com.

## <a name="create-a-container-registry"></a>Een containerregister maken

1. Klik op Hallo **nieuw** knop gevonden op Hallo linkerbovenhoek Hallo Azure-portal.

2. Zoeken Hallo marketplace voor **Azure container register** en selecteer deze.

3. Klik op **maken** die blade Hallo ACR-maken wordt geopend.

    ![Container Registry-instellingen](./media/container-registry-get-started-portal/managed-container-registry-settings.png)

4. In Hallo **Azure Container register** blade Hallo volgende informatie invoeren. Klik op **Maken** wanneer u klaar bent.

    a. **Registernaam**: een unieke domeinnaam op het hoogste niveau voor uw specifieke register. In dit voorbeeld is de naam van Hallo register *myAzureContainerRegistry1*, maar vervangen door een unieke naam van uw eigen. Hallo-naam mag alleen letters en cijfers zijn.

    b. **Resourcegroep**: Selecteer een bestaande [resourcegroep](../azure-resource-manager/resource-group-overview.md#resource-groups) of Hallo typenaam voor een nieuwe resourcegroep.

    c. **Locatie**: Selecteer een Azure-datacenter locatie van Hallo service [beschikbaar](https://azure.microsoft.com/regions/services/), zoals **Zuid-centraal VS**.

    d. **Gebruiker met beheerdersrechten**: als u wilt, schakelt u het register voor een beheerder de gebruiker tooaccess Hallo. U kunt deze instelling na het maken van Hallo register kunt wijzigen.

    e. **Gebruik beheerde register**: Selecteer Ja toohave ACR automatisch Hallo register opslag te beheren, gebruik webhooks en gebruik AAD-verificaties.

    f. **Prijscategorie**: selecteer een prijscategorie, zie ACR-prijzen voor meer informatie.

## <a name="log-in-tooacr-instance"></a>Meld u bij tooACR exemplaar

Voordat u pushen en installatiekopieën van de container binnenhalen, moet u zich aanmeldt toohello ACR-exemplaar. 

toodo gebruik dus hello Azure CLI 2.0. Eerst, indien nodig, meld u aan bij Azure met behulp van Hallo [az aanmelding](/cli/azure/#login) opdracht. 

```azurecli
az login
```

Gebruik vervolgens Hallo [az acr aanmelding](/cli/azure/acr#login) opdracht toolog in Azure Container register toohello.

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

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

In deze snel starten, kunt u een beheerde Azure-Container register-exemplaar met gebruikmaking van hello Azure-portal hebt gemaakt.

> [!div class="nextstepaction"]
> [Uw eerste installatiekopie met behulp van Docker CLI Hallo push](container-registry-get-started-docker-cli.md)
