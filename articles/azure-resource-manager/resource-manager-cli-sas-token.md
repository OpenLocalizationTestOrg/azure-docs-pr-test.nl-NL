---
title: aaaDeploy Azure-sjabloon met SAS-token en Azure CLI | Microsoft Docs
description: Gebruik Azure Resource Manager en Azure CLI toodeploy resources tooAzure vanuit een sjabloon die wordt beveiligd met SAS-token.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: tomfitz
ms.openlocfilehash: 59c64616d6e1f5e456d88a72854d0ed99e1bdc0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-private-resource-manager-template-with-sas-token-and-azure-cli"></a>Met SAS-token en Azure CLI persoonlijke Resource Manager-sjabloon implementeren

Wanneer de sjabloon bevindt zich in een opslagaccount, kunt u access toohello sjabloon beperken en bieden een shared access signature (SAS)-token tijdens de implementatie. Dit onderwerp wordt uitgelegd hoe toouse Azure PowerShell met Resource Manager-sjablonen tooprovide tijdens de implementatie van een SAS-token. 

## <a name="add-private-template-toostorage-account"></a>Persoonlijke sjabloon toostorage account toevoegen

U kunt uw sjablonen tooa storage-account toevoegen en toothem koppelen tijdens de implementatie met een SAS-token.

> [!IMPORTANT]
> Door Hallo onderstaande stappen te volgen, is Hallo blob met Hallo sjabloon toegankelijk tooonly Hallo accounteigenaar. Bij het maken van een SAS-token voor Hallo blob is Hallo blob toegankelijk tooanyone met die URI. Als een andere gebruiker Hallo URI onderschept, is deze gebruiker kunnen tooaccess Hallo sjabloon. Met behulp van een SAS-token is een prima manier voor het beperken van toegang tooyour sjablonen moet, maar u geen gevoelige gegevens, zoals wachtwoorden rechtstreeks in het Hallo-sjabloon.
> 
> 

Hallo volgende voorbeeld stelt u een persoonlijke opslag account-container en een sjabloon uploadt:
   
```azurecli
az group create --name "ManageGroup" --location "South Central US"
az storage account create \
    --resource-group ManageGroup \
    --location "South Central US" \
    --sku Standard_LRS \
    --kind Storage \
    --name {your-unique-name}
connection=$(az storage account show-connection-string \
    --resource-group ManageGroup \
    --name {your-unique-name} \
    --query connectionString)
az storage container create \
    --name templates \
    --public-access Off \
    --connection-string $connection
az storage blob upload \
    --container-name templates \
    --file vmlinux.json \
    --name vmlinux.json \
    --connection-string $connection
```

### <a name="provide-sas-token-during-deployment"></a>SAS-token opgeven tijdens de implementatie
een persoonlijke sjabloon in een opslagaccount toodeploy een SAS-token genereren en deze opnemen in Hallo URI voor Hallo sjabloon. Stel Hallo verstrijken tijd tooallow voldoende tijd toocomplete Hallo-implementatie.
   
```azurecli
expiretime=$(date -u -d '30 minutes' +%Y-%m-%dT%H:%MZ)
connection=$(az storage account show-connection-string \
    --resource-group ManageGroup \
    --name {your-unique-name} \
    --query connectionString)
token=$(az storage blob generate-sas \
    --container-name templates \
    --name vmlinux.json \
    --expiry $expiretime \
    --permissions r \
    --output tsv \
    --connection-string $connection)
url=$(az storage blob url \
    --container-name templates \
    --name vmlinux.json \
    --output tsv \
    --connection-string $connection)
az group deployment create --resource-group ExampleGroup --template-uri $url?$token
```

Zie voor een voorbeeld van het gebruik van een SAS-token met gekoppelde sjablonen [gekoppelde sjablonen gebruiken met Azure Resource Manager](resource-group-linked-templates.md).

## <a name="next-steps"></a>Volgende stappen
* Zie voor een inleiding toodeploying sjablonen, [implementeren van resources met Resource Manager-sjablonen en Azure PowerShell](resource-group-template-deploy-cli.md).
* Zie voor een compleet codevoorbeeld-script waarmee een sjabloon wordt geïmplementeerd, [sjabloonscript Resource Manager implementeren](resource-manager-samples-cli-deploy.md)
* toodefine parameters in de sjabloon, Zie [sjablonen](resource-group-authoring-templates.md#parameters).
* Abonnementen voor instructies over hoe ondernemingen tooeffectively Resource Manager kunt beheren, Zie [Azure enterprise scaffold - prescriptieve abonnement governance](resource-manager-subscription-governance.md).
