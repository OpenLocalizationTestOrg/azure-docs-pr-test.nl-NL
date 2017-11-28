---
title: Azure-sjabloon met SAS-token en PowerShell implementeren | Microsoft Docs
description: Azure Resource Manager en Azure PowerShell gebruiken voor het implementeren van resources in Azure uit een sjabloon die wordt beveiligd met SAS-token.
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
ms.openlocfilehash: 1e3cea027b599e2b1af1ced0fdf14e2cc8a0db82
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-private-resource-manager-template-with-sas-token-and-azure-powershell"></a><span data-ttu-id="6de8a-103">Met SAS-token en Azure PowerShell persoonlijke Resource Manager-sjabloon implementeren</span><span class="sxs-lookup"><span data-stu-id="6de8a-103">Deploy private Resource Manager template with SAS token and Azure PowerShell</span></span>

<span data-ttu-id="6de8a-104">Wanneer de sjabloon bevindt zich in een opslagaccount, kunt u het beperken van toegang aan de sjabloon en een shared access signature (SAS)-token opgeven tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="6de8a-104">When your template resides in a storage account, you can restrict access to the template and provide a shared access signature (SAS) token during deployment.</span></span> <span data-ttu-id="6de8a-105">In dit onderwerp wordt uitgelegd hoe u Azure PowerShell gebruiken met Resource Manager-sjablonen te geven van een SAS-token tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="6de8a-105">This topic explains how to use Azure PowerShell with Resource Manager templates to provide a SAS token during deployment.</span></span> 

## <a name="add-private-template-to-storage-account"></a><span data-ttu-id="6de8a-106">Persoonlijke sjabloon toevoegen aan de storage-account</span><span class="sxs-lookup"><span data-stu-id="6de8a-106">Add private template to storage account</span></span>

<span data-ttu-id="6de8a-107">U kunt uw sjablonen toevoegen aan een opslagaccount en een koppeling naar deze tijdens de implementatie met een SAS-token.</span><span class="sxs-lookup"><span data-stu-id="6de8a-107">You can add your templates to a storage account and link to them during deployment with a SAS token.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6de8a-108">De blob met de sjabloon is door de onderstaande stappen te volgen, toegankelijk voor de eigenaar van het account.</span><span class="sxs-lookup"><span data-stu-id="6de8a-108">By following the steps below, the blob containing the template is accessible to only the account owner.</span></span> <span data-ttu-id="6de8a-109">De blob is echter toegankelijk voor iedereen met de URI die bij het maken van een SAS-token voor de blob.</span><span class="sxs-lookup"><span data-stu-id="6de8a-109">However, when you create a SAS token for the blob, the blob is accessible to anyone with that URI.</span></span> <span data-ttu-id="6de8a-110">Als een andere gebruiker de URI onderschept, kan die gebruiker toegang tot de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="6de8a-110">If another user intercepts the URI, that user is able to access the template.</span></span> <span data-ttu-id="6de8a-111">Met behulp van een SAS-token is een prima manier voor het beperken van toegang tot uw sjablonen moet, maar u geen gevoelige gegevens, zoals wachtwoorden rechtstreeks in de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="6de8a-111">Using a SAS token is a good way of limiting access to your templates, but you should not include sensitive data like passwords directly in the template.</span></span>
> 
> 

<span data-ttu-id="6de8a-112">Het volgende voorbeeld stelt u een persoonlijke opslag account-container en een sjabloon geüpload:</span><span class="sxs-lookup"><span data-stu-id="6de8a-112">The following example sets up a private storage account container and uploads a template:</span></span>
   
```powershell
# create a storage account for templates
New-AzureRmResourceGroup -Name ManageGroup -Location "South Central US"
New-AzureRmStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name} -Type Standard_LRS -Location "West US"
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name}

# create a container and upload template
New-AzureStorageContainer -Name templates -Permission Off
Set-AzureStorageBlobContent -Container templates -File c:\MyTemplates\storage.json
```

## <a name="provide-sas-token-during-deployment"></a><span data-ttu-id="6de8a-113">SAS-token opgeven tijdens de implementatie</span><span class="sxs-lookup"><span data-stu-id="6de8a-113">Provide SAS token during deployment</span></span>
<span data-ttu-id="6de8a-114">Een SAS-token genereren en deze opnemen in de URI voor de sjabloon voor het implementeren van een persoonlijke sjabloon in een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="6de8a-114">To deploy a private template in a storage account, generate a SAS token and include it in the URI for the template.</span></span> <span data-ttu-id="6de8a-115">Stel het verlooptijdstip voldoende tijd laten om de implementatie te vervolledigen.</span><span class="sxs-lookup"><span data-stu-id="6de8a-115">Set the expiry time to allow enough time to complete the deployment.</span></span>
   
```powershell
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name}

# get the URI with the SAS token
$templateuri = New-AzureStorageBlobSASToken -Container templates -Blob storage.json -Permission r `
  -ExpiryTime (Get-Date).AddHours(2.0) -FullUri

# provide URI with SAS token during deployment
New-AzureRmResourceGroup -Name ExampleGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri $templateuri
```

<span data-ttu-id="6de8a-116">Zie voor een voorbeeld van het gebruik van een SAS-token met gekoppelde sjablonen [gekoppelde sjablonen gebruiken met Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="6de8a-116">For an example of using a SAS token with linked templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="6de8a-117">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6de8a-117">Next steps</span></span>
* <span data-ttu-id="6de8a-118">Zie voor een inleiding tot het implementeren van sjablonen [implementeren van resources met Resource Manager-sjablonen en Azure PowerShell](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="6de8a-118">For an introduction to deploying templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="6de8a-119">Zie voor een compleet codevoorbeeld-script waarmee een sjabloon wordt geïmplementeerd, [sjabloonscript Resource Manager implementeren](resource-manager-samples-powershell-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="6de8a-119">For a complete sample script that deploys a template, see [Deploy Resource Manager template script](resource-manager-samples-powershell-deploy.md)</span></span>
* <span data-ttu-id="6de8a-120">Om parameters te definiëren in de sjabloon, Zie [sjablonen](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="6de8a-120">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="6de8a-121">Voor begeleiding bij de manier waarop ondernemingen Resource Manager effectief kunnen gebruiken voor het beheer van abonnementen, gaat u naar [Azure enterprise-platform - Prescriptieve abonnementsgovernance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="6de8a-121">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

