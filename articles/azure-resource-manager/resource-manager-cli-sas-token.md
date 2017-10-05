---
title: Azure-sjabloon met SAS-token en Azure CLI implementeren | Microsoft Docs
description: Azure Resource Manager en Azure CLI gebruiken voor het implementeren van resources in Azure uit een sjabloon die wordt beveiligd met SAS-token.
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
ms.openlocfilehash: 22387aadd8f53a65efb76a29a9403c46a2c25954
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-private-resource-manager-template-with-sas-token-and-azure-cli"></a><span data-ttu-id="cc564-103">Met SAS-token en Azure CLI persoonlijke Resource Manager-sjabloon implementeren</span><span class="sxs-lookup"><span data-stu-id="cc564-103">Deploy private Resource Manager template with SAS token and Azure CLI</span></span>

<span data-ttu-id="cc564-104">Wanneer de sjabloon bevindt zich in een opslagaccount, kunt u het beperken van toegang aan de sjabloon en een shared access signature (SAS)-token opgeven tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="cc564-104">When your template resides in a storage account, you can restrict access to the template and provide a shared access signature (SAS) token during deployment.</span></span> <span data-ttu-id="cc564-105">In dit onderwerp wordt uitgelegd hoe u Azure PowerShell gebruiken met Resource Manager-sjablonen te geven van een SAS-token tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="cc564-105">This topic explains how to use Azure PowerShell with Resource Manager templates to provide a SAS token during deployment.</span></span> 

## <a name="add-private-template-to-storage-account"></a><span data-ttu-id="cc564-106">Persoonlijke sjabloon toevoegen aan de storage-account</span><span class="sxs-lookup"><span data-stu-id="cc564-106">Add private template to storage account</span></span>

<span data-ttu-id="cc564-107">U kunt uw sjablonen toevoegen aan een opslagaccount en een koppeling naar deze tijdens de implementatie met een SAS-token.</span><span class="sxs-lookup"><span data-stu-id="cc564-107">You can add your templates to a storage account and link to them during deployment with a SAS token.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cc564-108">De blob met de sjabloon is door de onderstaande stappen te volgen, toegankelijk voor de eigenaar van het account.</span><span class="sxs-lookup"><span data-stu-id="cc564-108">By following the steps below, the blob containing the template is accessible to only the account owner.</span></span> <span data-ttu-id="cc564-109">De blob is echter toegankelijk voor iedereen met de URI die bij het maken van een SAS-token voor de blob.</span><span class="sxs-lookup"><span data-stu-id="cc564-109">However, when you create a SAS token for the blob, the blob is accessible to anyone with that URI.</span></span> <span data-ttu-id="cc564-110">Als een andere gebruiker de URI onderschept, kan die gebruiker toegang tot de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="cc564-110">If another user intercepts the URI, that user is able to access the template.</span></span> <span data-ttu-id="cc564-111">Met behulp van een SAS-token is een prima manier voor het beperken van toegang tot uw sjablonen moet, maar u geen gevoelige gegevens, zoals wachtwoorden rechtstreeks in de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="cc564-111">Using a SAS token is a good way of limiting access to your templates, but you should not include sensitive data like passwords directly in the template.</span></span>
> 
> 

<span data-ttu-id="cc564-112">Het volgende voorbeeld stelt u een persoonlijke opslag account-container en een sjabloon geüpload:</span><span class="sxs-lookup"><span data-stu-id="cc564-112">The following example sets up a private storage account container and uploads a template:</span></span>
   
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

### <a name="provide-sas-token-during-deployment"></a><span data-ttu-id="cc564-113">SAS-token opgeven tijdens de implementatie</span><span class="sxs-lookup"><span data-stu-id="cc564-113">Provide SAS token during deployment</span></span>
<span data-ttu-id="cc564-114">Een SAS-token genereren en deze opnemen in de URI voor de sjabloon voor het implementeren van een persoonlijke sjabloon in een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="cc564-114">To deploy a private template in a storage account, generate a SAS token and include it in the URI for the template.</span></span> <span data-ttu-id="cc564-115">Stel het verlooptijdstip voldoende tijd laten om de implementatie te vervolledigen.</span><span class="sxs-lookup"><span data-stu-id="cc564-115">Set the expiry time to allow enough time to complete the deployment.</span></span>
   
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

<span data-ttu-id="cc564-116">Zie voor een voorbeeld van het gebruik van een SAS-token met gekoppelde sjablonen [gekoppelde sjablonen gebruiken met Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="cc564-116">For an example of using a SAS token with linked templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc564-117">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cc564-117">Next steps</span></span>
* <span data-ttu-id="cc564-118">Zie voor een inleiding tot het implementeren van sjablonen [implementeren van resources met Resource Manager-sjablonen en Azure PowerShell](resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="cc564-118">For an introduction to deploying templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy-cli.md).</span></span>
* <span data-ttu-id="cc564-119">Zie voor een compleet codevoorbeeld-script waarmee een sjabloon wordt geïmplementeerd, [sjabloonscript Resource Manager implementeren](resource-manager-samples-cli-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="cc564-119">For a complete sample script that deploys a template, see [Deploy Resource Manager template script](resource-manager-samples-cli-deploy.md)</span></span>
* <span data-ttu-id="cc564-120">Om parameters te definiëren in de sjabloon, Zie [sjablonen](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="cc564-120">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="cc564-121">Voor begeleiding bij de manier waarop ondernemingen Resource Manager effectief kunnen gebruiken voor het beheer van abonnementen, gaat u naar [Azure enterprise-platform - Prescriptieve abonnementsgovernance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="cc564-121">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
