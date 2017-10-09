---
title: aaaDeploy Azure-sjabloon met SAS-token en PowerShell | Microsoft Docs
description: Gebruik Azure Resource Manager en Azure PowerShell toodeploy resources tooAzure vanuit een sjabloon die wordt beveiligd met SAS-token.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: tomfitz
ms.openlocfilehash: b95e096591d6213f8ef79235c8cd85705c4b79ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-private-resource-manager-template-with-sas-token-and-azure-powershell"></a>Met SAS-token en Azure PowerShell persoonlijke Resource Manager-sjabloon implementeren

Wanneer de sjabloon bevindt zich in een opslagaccount, kunt u access toohello sjabloon beperken en bieden een shared access signature (SAS)-token tijdens de implementatie. Dit onderwerp wordt uitgelegd hoe toouse Azure PowerShell met Resource Manager-sjablonen tooprovide tijdens de implementatie van een SAS-token. 

## <a name="add-private-template-toostorage-account"></a>Persoonlijke sjabloon toostorage account toevoegen

U kunt uw sjablonen tooa storage-account toevoegen en toothem koppelen tijdens de implementatie met een SAS-token.

> [!IMPORTANT]
> Door Hallo onderstaande stappen te volgen, is Hallo blob met Hallo sjabloon toegankelijk tooonly Hallo accounteigenaar. Bij het maken van een SAS-token voor Hallo blob is Hallo blob toegankelijk tooanyone met die URI. Als een andere gebruiker Hallo URI onderschept, is deze gebruiker kunnen tooaccess Hallo sjabloon. Met behulp van een SAS-token is een prima manier voor het beperken van toegang tooyour sjablonen moet, maar u geen gevoelige gegevens, zoals wachtwoorden rechtstreeks in het Hallo-sjabloon.
> 
> 

Hallo volgende voorbeeld stelt u een persoonlijke opslag account-container en een sjabloon uploadt:
   
```powershell
# create a storage account for templates
New-AzureRmResourceGroup -Name ManageGroup -Location "South Central US"
New-AzureRmStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name} -Type Standard_LRS -Location "West US"
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name}

# create a container and upload template
New-AzureStorageContainer -Name templates -Permission Off
Set-AzureStorageBlobContent -Container templates -File c:\MyTemplates\storage.json
```

## <a name="provide-sas-token-during-deployment"></a>SAS-token opgeven tijdens de implementatie
een persoonlijke sjabloon in een opslagaccount toodeploy een SAS-token genereren en deze opnemen in Hallo URI voor Hallo sjabloon. Stel Hallo verstrijken tijd tooallow voldoende tijd toocomplete Hallo-implementatie.
   
```powershell
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name}

# get hello URI with hello SAS token
$templateuri = New-AzureStorageBlobSASToken -Container templates -Blob storage.json -Permission r `
  -ExpiryTime (Get-Date).AddHours(2.0) -FullUri

# provide URI with SAS token during deployment
New-AzureRmResourceGroup -Name ExampleGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri $templateuri
```

Zie voor een voorbeeld van het gebruik van een SAS-token met gekoppelde sjablonen [gekoppelde sjablonen gebruiken met Azure Resource Manager](resource-group-linked-templates.md).


## <a name="next-steps"></a>Volgende stappen
* Zie voor een inleiding toodeploying sjablonen, [implementeren van resources met Resource Manager-sjablonen en Azure PowerShell](resource-group-template-deploy.md).
* Zie voor een compleet codevoorbeeld-script waarmee een sjabloon wordt geïmplementeerd, [sjabloonscript Resource Manager implementeren](resource-manager-samples-powershell-deploy.md)
* toodefine parameters in de sjabloon, Zie [sjablonen](resource-group-authoring-templates.md#parameters).
* Abonnementen voor instructies over hoe ondernemingen tooeffectively Resource Manager kunt beheren, Zie [Azure enterprise scaffold - prescriptieve abonnement governance](resource-manager-subscription-governance.md).

