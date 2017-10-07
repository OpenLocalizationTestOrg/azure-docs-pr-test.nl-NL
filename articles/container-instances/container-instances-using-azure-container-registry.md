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
# <a name="deploy-tooazure-container-instances-from-hello-azure-container-registry"></a><span data-ttu-id="7f713-103">TooAzure Containerexemplaren van hello Azure Container register implementeren</span><span class="sxs-lookup"><span data-stu-id="7f713-103">Deploy tooAzure Container Instances from hello Azure Container Registry</span></span>

<span data-ttu-id="7f713-104">Hello Azure Container register is een register op basis van Azure, persoonlijke voor installatiekopieën van de Docker-container.</span><span class="sxs-lookup"><span data-stu-id="7f713-104">hello Azure Container Registry is an Azure-based, private registry, for Docker container images.</span></span> <span data-ttu-id="7f713-105">In dit artikel bevat informatie over hoe toodeploy container installatiekopieën opgeslagen in Azure Container register Hallo tooAzure Containerexemplaren.</span><span class="sxs-lookup"><span data-stu-id="7f713-105">This article covers how toodeploy container images stored in hello Azure Container Registry tooAzure Container Instances.</span></span>

## <a name="using-hello-azure-cli"></a><span data-ttu-id="7f713-106">Hello Azure CLI gebruiken</span><span class="sxs-lookup"><span data-stu-id="7f713-106">Using hello Azure CLI</span></span>

<span data-ttu-id="7f713-107">Hello Azure CLI bevat-opdrachten voor het maken en beheren van containers in Azure Container instanties.</span><span class="sxs-lookup"><span data-stu-id="7f713-107">hello Azure CLI includes commands for creating and managing containers in Azure Container Instances.</span></span> <span data-ttu-id="7f713-108">Als u een installatiekopie van een persoonlijke in Hallo opgeeft `create` uitvoert, en u kunt ook Hallo installatiekopie register wachtwoord vereist tooauthenticate met Hallo container register opgeven.</span><span class="sxs-lookup"><span data-stu-id="7f713-108">If you specify a private image in hello `create` command, you can also specify hello image registry password required tooauthenticate with hello container registry.</span></span>

```azurecli-interactive
az container create --name myprivatecontainer --image mycontainerregistry.azurecr.io/mycontainerimage:v1 --registry-password myRegistryPassword --resource-group myresourcegroup
```

<span data-ttu-id="7f713-109">Hallo `create` opdracht ook ondersteunt het opgeven van Hallo `registry-login-server` en `registry-username`.</span><span class="sxs-lookup"><span data-stu-id="7f713-109">hello `create` command also supports specifying hello `registry-login-server` and `registry-username`.</span></span> <span data-ttu-id="7f713-110">Hallo login-server voor hello Azure Container register is echter altijd *registryname*. azurecr.io en Hallo standaardgebruikersnaam *registryname*, zodat deze waarden zijn afgeleid van de naam van de installatiekopie Hallo als niet expliciet is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="7f713-110">However, hello login server for hello Azure Container Registry is always *registryname*.azurecr.io and hello default username is *registryname*, so these values are inferred from hello image name if not explicitly provided.</span></span>

## <a name="using-an-azure-resource-manager-template"></a><span data-ttu-id="7f713-111">Met behulp van een Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="7f713-111">Using an Azure Resource Manager template</span></span>

<span data-ttu-id="7f713-112">U kunt Hallo eigenschappen van de registratie van uw Azure-Container opgeven in een Azure Resource Manager-sjabloon door Hallo `imageRegistryCredentials` eigenschap in groepsdefinitie Hallo-container:</span><span class="sxs-lookup"><span data-stu-id="7f713-112">You can specify hello properties of your Azure Container Registry in an Azure Resource Manager template by including hello `imageRegistryCredentials` property in hello container group definition:</span></span>

```json
"imageRegistryCredentials": [
  {
    "server": "imageRegistryLoginServer",
    "username": "imageRegistryUsername",
    "password": "imageRegistryPassword"
  }
]
```

<span data-ttu-id="7f713-113">tooavoid opslaan van uw wachtwoord container-register rechtstreeks in de sjabloon hello, wordt aangeraden te slaan als een geheim in [Azure Key Vault](../key-vault/key-vault-manage-with-cli2.md) en ernaar wordt verwezen in Hallo-sjabloon met gebruik van Hallo [systeemeigen integratie tussen Azure Resource Manager en Sleutelkluis Hallo](../azure-resource-manager/resource-manager-keyvault-parameter.md).</span><span class="sxs-lookup"><span data-stu-id="7f713-113">tooavoid storing your container registry password directly in hello template, we recommend that you store it as a secret in [Azure Key Vault](../key-vault/key-vault-manage-with-cli2.md) and reference it in hello template using hello [native integration between hello Azure Resource Manager and Key Vault](../azure-resource-manager/resource-manager-keyvault-parameter.md).</span></span>

## <a name="using-hello-azure-portal"></a><span data-ttu-id="7f713-114">Met behulp van hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="7f713-114">Using hello Azure portal</span></span>

<span data-ttu-id="7f713-115">Als u installatiekopieën van de container in Azure Container register Hallo onderhouden, kunt u eenvoudig een container maken in Azure Container-exemplaren die gebruikmaken van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="7f713-115">If you maintain container images in hello Azure Container Registry, you can easily create a container in Azure Container Instances using hello Azure portal.</span></span>

1. <span data-ttu-id="7f713-116">Navigeer in hello Azure-portal, tooyour container register.</span><span class="sxs-lookup"><span data-stu-id="7f713-116">In hello Azure portal, navigate tooyour container registry.</span></span>

2. <span data-ttu-id="7f713-117">Kies opslagplaatsen.</span><span class="sxs-lookup"><span data-stu-id="7f713-117">Choose Repositories.</span></span>

    ![Hello Azure Container register menu in hello Azure-portal][acr-menu]

3. <span data-ttu-id="7f713-119">Kies Hallo-opslagplaats die u wilt toodeploy uit.</span><span class="sxs-lookup"><span data-stu-id="7f713-119">Choose hello repository that you want toodeploy from.</span></span>

4. <span data-ttu-id="7f713-120">Met de rechtermuisknop op het Hallo-tag voor de installatiekopie van de container Hallo gewenste toodeploy.</span><span class="sxs-lookup"><span data-stu-id="7f713-120">Right-click hello tag for hello container image you want toodeploy.</span></span>

    ![Snelmenu voor het starten van de container met exemplaren van Azure-Container][acr-runinstance-contextmenu]

5. <span data-ttu-id="7f713-122">Voer een naam voor het Hallo-container en een naam voor de resourcegroep Hallo.</span><span class="sxs-lookup"><span data-stu-id="7f713-122">Enter a name for hello container and a name for hello resource group.</span></span> <span data-ttu-id="7f713-123">U kunt ook standaardwaarden Hallo wijzigen als u wenst.</span><span class="sxs-lookup"><span data-stu-id="7f713-123">You can also change hello default values if you wish.</span></span>

    ![Menu voor exemplaren van Azure-Container maken][acr-create-deeplink]

6. <span data-ttu-id="7f713-125">Nadat het Hallo-implementatie is voltooid, kunt u toohello containergroep van Hallo meldingen deelvenster toofind gaat het IP-adres en andere eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="7f713-125">Once hello deployment completes, you can navigate toohello container group from hello notifications pane toofind its IP address and other properties.</span></span>

    ![Details weergeven voor Azure-Container exemplarengroep container][aci-detailsview]

## <a name="next-steps"></a><span data-ttu-id="7f713-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7f713-127">Next steps</span></span>

<span data-ttu-id="7f713-128">Ontdek hoe toobuild containers, push ze tooa privé-container register en deze tooAzure Containerexemplaren door implementeren [voltooien Hallo zelfstudie](container-instances-tutorial-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="7f713-128">Learn how toobuild containers, push them tooa private container registry, and deploy them tooAzure Container Instances by [completing hello tutorial](container-instances-tutorial-prepare-app.md).</span></span>

<!-- IMAGES -->
[acr-menu]: ./media/container-instances-using-azure-container-registry/acr-menu.png

[acr-runinstance-contextmenu]: ./media/container-instances-using-azure-container-registry/acr-runinstance-contextmenu.png

[acr-create-deeplink]: ./media/container-instances-using-azure-container-registry/acr-create-deeplink.png

[aci-detailsview]: ./media/container-instances-using-azure-container-registry/aci-detailsview.png
