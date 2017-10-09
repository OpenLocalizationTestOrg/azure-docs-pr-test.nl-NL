---
title: aaaDeploy resources tooAzure | Microsoft Docs
description: Gebruik Azure PowerShell of Azure CLI toodeploy resources tooAzure. Hallo-bronnen worden gedefinieerd in het Resource Manager-sjabloon.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/16/2017
ms.author: tomfitz
ms.openlocfilehash: 0cd3f8ad45af1fb85c78899b56f6807d00b859f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-tooazure"></a><span data-ttu-id="a0fe0-104">Resources tooAzure implementeren</span><span class="sxs-lookup"><span data-stu-id="a0fe0-104">Deploy resources tooAzure</span></span>

<span data-ttu-id="a0fe0-105">Dit onderwerp wordt beschreven hoe toodeploy resources tooyour Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="a0fe0-105">This topic shows how toodeploy resources tooyour Azure subscription.</span></span> <span data-ttu-id="a0fe0-106">U kunt Azure PowerShell of Azure CLI toodeploy Resource Manager-sjabloon die Hallo-infrastructuur voor uw oplossing definieert.</span><span class="sxs-lookup"><span data-stu-id="a0fe0-106">You can use either Azure PowerShell or Azure CLI toodeploy a Resource Manager template that defines hello infrastructure for your solution.</span></span>

<span data-ttu-id="a0fe0-107">Zie voor een inleiding tooconcepts van Resource Manager, [overzicht van Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a0fe0-107">For an introduction tooconcepts of Resource Manager, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

## <a name="steps-for-deployment"></a><span data-ttu-id="a0fe0-108">Stappen voor implementatie</span><span class="sxs-lookup"><span data-stu-id="a0fe0-108">Steps for deployment</span></span>

<span data-ttu-id="a0fe0-109">In dit onderwerp wordt ervan uitgegaan dat u implementeert Hallo [opslag voorbeeldsjabloon](#example-storage-template) in dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="a0fe0-109">This topic assumes you are deploying hello [example storage template](#example-storage-template) in this topic.</span></span> <span data-ttu-id="a0fe0-110">U kunt een andere sjabloon, maar Hallo-parameters die u doorgeeft anders zijn dan wat in dit onderwerp wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a0fe0-110">You can use a different template, but hello parameters you pass are different than what is shown in this topic.</span></span>

<span data-ttu-id="a0fe0-111">Na het maken van een sjabloon zijn Hallo algemene stappen voor het implementeren van uw sjabloon:</span><span class="sxs-lookup"><span data-stu-id="a0fe0-111">After creating a template, hello general steps for deploying your template are:</span></span>

1. <span data-ttu-id="a0fe0-112">Meld u bij tooyour account</span><span class="sxs-lookup"><span data-stu-id="a0fe0-112">Log in tooyour account</span></span>
2. <span data-ttu-id="a0fe0-113">Selecteer Hallo abonnement toouse (alleen nodig als u meerdere abonnementen hebt en u wilt dat toouse een die niet Hallo standaardabonnement)</span><span class="sxs-lookup"><span data-stu-id="a0fe0-113">Select hello subscription toouse (only necessary if you have multiple subscriptions, and you want toouse one that is not hello default subscription)</span></span>
3. <span data-ttu-id="a0fe0-114">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="a0fe0-114">Create a resource group</span></span>
4. <span data-ttu-id="a0fe0-115">Hallo-sjabloon implementeren</span><span class="sxs-lookup"><span data-stu-id="a0fe0-115">Deploy hello template</span></span>
5. <span data-ttu-id="a0fe0-116">De implementatiestatus controleren</span><span class="sxs-lookup"><span data-stu-id="a0fe0-116">Check your deployment status</span></span>

<span data-ttu-id="a0fe0-117">Hallo volgende secties wordt uitgelegd hoe tooperform die stappen waarbij [PowerShell](#powershell) of [Azure CLI](#azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a0fe0-117">hello following sections show how tooperform those steps with [PowerShell](#powershell) or [Azure CLI](#azure-cli).</span></span>

## <a name="powershell"></a><span data-ttu-id="a0fe0-118">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a0fe0-118">PowerShell</span></span>

1. <span data-ttu-id="a0fe0-119">Zie tooinstall Azure PowerShell [aan de slag met Azure PowerShell-cmdlets](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a0fe0-119">tooinstall Azure PowerShell, see [Get started with Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>

2. <span data-ttu-id="a0fe0-120">tooquickly aan de slag met de implementatie, Hallo cmdlets volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="a0fe0-120">tooquickly get started with deployment, use hello following cmdlets:</span></span>

  ```powershell
  Login-AzureRmAccount
  Set-AzureRmContext -SubscriptionID {subscription-id}

  New-AzureRmResourceGroup -Name ExampleGroup -Location "Central US"
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleGroup -TemplateFile c:\MyTemplates\azuredeploy.json 
  ```

  <span data-ttu-id="a0fe0-121">Hallo `Set-AzureRmContext` cmdlet is alleen nodig als u wilt dat een abonnement toouse dan uw standaardabonnement.</span><span class="sxs-lookup"><span data-stu-id="a0fe0-121">hello `Set-AzureRmContext` cmdlet is only needed if you want toouse a subscription other than your default subscription.</span></span> <span data-ttu-id="a0fe0-122">toosee al uw abonnementen en hun id's gebruiken:</span><span class="sxs-lookup"><span data-stu-id="a0fe0-122">toosee all your subscriptions and their IDs, use:</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

3. <span data-ttu-id="a0fe0-123">Hallo-implementatie kan toocomplete van enkele minuten duren.</span><span class="sxs-lookup"><span data-stu-id="a0fe0-123">hello deployment can take a few minutes toocomplete.</span></span> <span data-ttu-id="a0fe0-124">Als deze is voltooid, ziet u een bericht dat lijkt op:</span><span class="sxs-lookup"><span data-stu-id="a0fe0-124">When it finishes, you see a message similar to:</span></span>

  ```powershell
  DeploymentName          : ExampleDeployment
  CorrelationId           : 07b3b233-8367-4a0b-b9bc-7aa189065665
  ResourceGroupName       : ExampleGroup
  ProvisioningState       : Succeeded
  ...
  ```

4. <span data-ttu-id="a0fe0-125">toosee die uw resource groep en storage-account zijn geïmplementeerd tooyour abonnement, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="a0fe0-125">toosee that your resource group and storage account were deployed tooyour subscription, use:</span></span>

  ```powershell
  Get-AzureRmResourceGroup -Name ExampleGroup
  Find-AzureRmResource -ResourceGroupNameEquals ExampleGroup
  ```

5. <span data-ttu-id="a0fe0-126">U kunt sjabloonparameters opgeven als PowerShell-parameters bij het implementeren van een sjabloon.</span><span class="sxs-lookup"><span data-stu-id="a0fe0-126">You can specify template parameters as PowerShell parameters when deploying a template.</span></span> <span data-ttu-id="a0fe0-127">Hallo bevat eerdere voorbeeld geen Sjabloonparameters, zodat de standaardwaarden Hallo in Hallo sjabloon zijn gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a0fe0-127">hello earlier example did not include any template parameters, so hello default values in hello template were used.</span></span> <span data-ttu-id="a0fe0-128">toodeploy opslag op een andere account en parameterwaarden opgeven voor voorvoegsel Hallo van opslag en het opslagaccount Hallo SKU, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="a0fe0-128">toodeploy another storage account, and provide parameter values for hello storage name prefix and hello storage account SKU, use:</span></span>

  ```powershell
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment2 -ResourceGroupName ExampleGroup -TemplateFile c:\MyTemplates\azuredeploy.json -storageNamePrefix "contoso" -storageSKU "Standard_GRS"
  ```

  <span data-ttu-id="a0fe0-129">U hebt nu twee opslagaccounts in de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="a0fe0-129">You now have two storage accounts in your resource group.</span></span> 

## <a name="azure-cli"></a><span data-ttu-id="a0fe0-130">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a0fe0-130">Azure CLI</span></span>

1. <span data-ttu-id="a0fe0-131">Zie tooinstall Azure CLI [2.0 voor Azure CLI installeren](/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="a0fe0-131">tooinstall Azure CLI, see [Install Azure CLI 2.0](/cli/azure/install-az-cli2).</span></span>

2. <span data-ttu-id="a0fe0-132">tooquickly aan de slag met de implementatie, Hallo volgende opdrachten gebruiken:</span><span class="sxs-lookup"><span data-stu-id="a0fe0-132">tooquickly get started with deployment, use hello following commands:</span></span>

  ```azurecli
  az login
  az account set --subscription {subscription-id}

  az group create --name ExampleGroup --location "Central US"
  az group deployment create --name ExampleDeployment --resource-group ExampleGroup --template-file c:\MyTemplates\azuredeploy.json
  ```

  <span data-ttu-id="a0fe0-133">Hallo `az account set` opdracht is alleen nodig als u wilt dat een abonnement toouse dan uw standaardabonnement.</span><span class="sxs-lookup"><span data-stu-id="a0fe0-133">hello `az account set` command is only needed if you want toouse a subscription other than your default subscription.</span></span> <span data-ttu-id="a0fe0-134">toosee al uw abonnementen en hun id's gebruiken:</span><span class="sxs-lookup"><span data-stu-id="a0fe0-134">toosee all your subscriptions and their IDs, use:</span></span>

  ```azurecli
  az account list
  ```

3. <span data-ttu-id="a0fe0-135">Hallo-implementatie kan toocomplete van enkele minuten duren.</span><span class="sxs-lookup"><span data-stu-id="a0fe0-135">hello deployment can take a few minutes toocomplete.</span></span> <span data-ttu-id="a0fe0-136">Als deze is voltooid, ziet u een bericht dat lijkt op:</span><span class="sxs-lookup"><span data-stu-id="a0fe0-136">When it finishes, you see a message similar to:</span></span>

  ```azurecli
  "provisioningState": "Succeeded",
  ```

4. <span data-ttu-id="a0fe0-137">toosee die uw resource groep en storage-account zijn geïmplementeerd tooyour abonnement, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="a0fe0-137">toosee that your resource group and storage account were deployed tooyour subscription, use:</span></span>

  ```azurecli
  az group show --name ExampleGroup
  az resource list --resource-group ExampleGroup
  ```

5. <span data-ttu-id="a0fe0-138">U kunt sjabloonparameters opgeven als PowerShell-parameters bij het implementeren van een sjabloon.</span><span class="sxs-lookup"><span data-stu-id="a0fe0-138">You can specify template parameters as PowerShell parameters when deploying a template.</span></span> <span data-ttu-id="a0fe0-139">Hallo bevat eerdere voorbeeld geen Sjabloonparameters, zodat de standaardwaarden Hallo in Hallo sjabloon zijn gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a0fe0-139">hello earlier example did not include any template parameters, so hello default values in hello template were used.</span></span> <span data-ttu-id="a0fe0-140">toodeploy opslag op een andere account en parameterwaarden opgeven voor voorvoegsel Hallo van opslag en het opslagaccount Hallo SKU, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="a0fe0-140">toodeploy another storage account, and provide parameter values for hello storage name prefix and hello storage account SKU, use:</span></span>

  ```azurecli
  az group deployment create --name ExampleDeployment2 --resource-group ExampleGroup --template-file c:\MyTemplates\azuredeploy.json --parameters '{"storageNamePrefix":{"value":"contoso"},"storageSKU":{"value":"Standard_GRS"}}'
  ```

  <span data-ttu-id="a0fe0-141">U hebt nu twee opslagaccounts in de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="a0fe0-141">You now have two storage accounts in your resource group.</span></span> 

## <a name="example-storage-template"></a><span data-ttu-id="a0fe0-142">Voorbeeldopslagsjabloon</span><span class="sxs-lookup"><span data-stu-id="a0fe0-142">Example storage template</span></span>

<span data-ttu-id="a0fe0-143">Hallo voorbeeld sjabloon toodeploy een tooyour voor opslagaccountabonnement volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="a0fe0-143">Use hello following example template toodeploy a storage account tooyour subscription:</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageNamePrefix": {
      "type": "string",
      "maxLength": 11,
      "defaultValue": "storage",
      "metadata": {
        "description": "hello value toouse for starting hello storage account name."
      }
    },
    "storageSKU": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_ZRS",
        "Standard_GRS",
        "Standard_RAGRS",
        "Premium_LRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "hello type of replication toouse for hello storage account."
      }
    }
  },
  "variables": {
    "storageName": "[concat(parameters('storageNamePrefix'), uniqueString(resourceGroup().id))]"
  },
  "resources": [
    {
      "name": "[variables('storageName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-05-01",
      "sku": {
        "name": "[parameters('storageSKU')]"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {
      }
    }
  ],
  "outputs": {  }
}
```

## <a name="next-steps"></a><span data-ttu-id="a0fe0-144">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a0fe0-144">Next steps</span></span>

* <span data-ttu-id="a0fe0-145">Zie voor gedetailleerde informatie over het gebruik van PowerShell toodeploy sjablonen [implementeren van resources met Resource Manager-sjablonen en Azure PowerShell](/azure/azure-resource-manager/resource-group-template-deploy).</span><span class="sxs-lookup"><span data-stu-id="a0fe0-145">For detailed information about using PowerShell toodeploy templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](/azure/azure-resource-manager/resource-group-template-deploy).</span></span>
* <span data-ttu-id="a0fe0-146">Zie voor gedetailleerde informatie over het gebruik van Azure CLI toodeploy sjablonen [implementeren van resources met Resource Manager-sjablonen en Azure CLI](/azure/azure-resource-manager/resource-group-template-deploy-cli).</span><span class="sxs-lookup"><span data-stu-id="a0fe0-146">For detailed information about using Azure CLI toodeploy templates, see [Deploy resources with Resource Manager templates and Azure CLI](/azure/azure-resource-manager/resource-group-template-deploy-cli).</span></span>



