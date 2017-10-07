---
title: aaaDeploy tooAzure Containerexemplaren van hello Azure Container register | Azure Docs
description: TooAzure Containerexemplaren van hello Azure Container register implementeren
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
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/02/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 2667f91db8ed92a9ccc9ba722a2b1f5c5ea93886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-tooazure-container-instances-from-hello-azure-container-registry"></a>TooAzure Containerexemplaren van hello Azure Container register implementeren

Hello Azure Container register is een register op basis van Azure, persoonlijke voor installatiekopieën van de Docker-container. In dit artikel bevat informatie over hoe toodeploy container installatiekopieën opgeslagen in Azure Container register Hallo tooAzure Containerexemplaren.

## <a name="using-hello-azure-cli"></a>Hello Azure CLI gebruiken

Hello Azure CLI bevat-opdrachten voor het maken en beheren van containers in Azure Container instanties. Als u een installatiekopie van een persoonlijke in Hallo opgeeft `create` uitvoert, en u kunt ook Hallo installatiekopie register wachtwoord vereist tooauthenticate met Hallo container register opgeven.

```azurecli-interactive
az container create --name myprivatecontainer --image mycontainerregistry.azurecr.io/mycontainerimage:v1 --registry-password myRegistryPassword --resource-group myresourcegroup
```

Hallo `create` opdracht ook ondersteunt het opgeven van Hallo `registry-login-server` en `registry-username`. Hallo login-server voor hello Azure Container register is echter altijd *registryname*. azurecr.io en Hallo standaardgebruikersnaam *registryname*, zodat deze waarden zijn afgeleid van de naam van de installatiekopie Hallo als niet expliciet is opgegeven.

## <a name="using-an-azure-resource-manager-template"></a>Met behulp van een Azure Resource Manager-sjabloon

U kunt Hallo eigenschappen van de registratie van uw Azure-Container opgeven in een Azure Resource Manager-sjabloon door Hallo `imageRegistryCredentials` eigenschap in groepsdefinitie Hallo-container:

```json
"imageRegistryCredentials": [
  {
    "server": "imageRegistryLoginServer",
    "username": "imageRegistryUsername",
    "password": "imageRegistryPassword"
  }
]
```

tooavoid opslaan van uw wachtwoord container-register rechtstreeks in de sjabloon hello, wordt aangeraden te slaan als een geheim in [Azure Key Vault](../key-vault/key-vault-manage-with-cli2.md) en ernaar wordt verwezen in Hallo-sjabloon met gebruik van Hallo [systeemeigen integratie tussen Azure Resource Manager en Sleutelkluis Hallo](../azure-resource-manager/resource-manager-keyvault-parameter.md).

## <a name="using-hello-azure-portal"></a>Met behulp van hello Azure-portal

Als u installatiekopieën van de container in Azure Container register Hallo onderhouden, kunt u eenvoudig een container maken in Azure Container-exemplaren die gebruikmaken van hello Azure-portal.

1. Navigeer in hello Azure-portal, tooyour container register.

2. Kies opslagplaatsen.

    ![Hello Azure Container register menu in hello Azure-portal][acr-menu]

3. Kies Hallo-opslagplaats die u wilt toodeploy uit.

4. Met de rechtermuisknop op het Hallo-tag voor de installatiekopie van de container Hallo gewenste toodeploy.

    ![Snelmenu voor het starten van de container met exemplaren van Azure-Container][acr-runinstance-contextmenu]

5. Voer een naam voor het Hallo-container en een naam voor de resourcegroep Hallo. U kunt ook standaardwaarden Hallo wijzigen als u wenst.

    ![Menu voor exemplaren van Azure-Container maken][acr-create-deeplink]

6. Nadat het Hallo-implementatie is voltooid, kunt u toohello containergroep van Hallo meldingen deelvenster toofind gaat het IP-adres en andere eigenschappen.

    ![Details weergeven voor Azure-Container exemplarengroep container][aci-detailsview]

## <a name="next-steps"></a>Volgende stappen

Ontdek hoe toobuild containers, push ze tooa privé-container register en deze tooAzure Containerexemplaren door implementeren [voltooien Hallo zelfstudie](container-instances-tutorial-prepare-app.md).

<!-- IMAGES -->
[acr-menu]: ./media/container-instances-using-azure-container-registry/acr-menu.png

[acr-runinstance-contextmenu]: ./media/container-instances-using-azure-container-registry/acr-runinstance-contextmenu.png

[acr-create-deeplink]: ./media/container-instances-using-azure-container-registry/acr-create-deeplink.png

[aci-detailsview]: ./media/container-instances-using-azure-container-registry/aci-detailsview.png
