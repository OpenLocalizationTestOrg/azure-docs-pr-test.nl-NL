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
# <a name="deploy-private-resource-manager-template-with-sas-token-and-azure-powershell"></a><span data-ttu-id="2ca10-103">Met SAS-token en Azure PowerShell persoonlijke Resource Manager-sjabloon implementeren</span><span class="sxs-lookup"><span data-stu-id="2ca10-103">Deploy private Resource Manager template with SAS token and Azure PowerShell</span></span>

<span data-ttu-id="2ca10-104">Wanneer de sjabloon bevindt zich in een opslagaccount, kunt u access toohello sjabloon beperken en bieden een shared access signature (SAS)-token tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="2ca10-104">When your template resides in a storage account, you can restrict access toohello template and provide a shared access signature (SAS) token during deployment.</span></span> <span data-ttu-id="2ca10-105">Dit onderwerp wordt uitgelegd hoe toouse Azure PowerShell met Resource Manager-sjablonen tooprovide tijdens de implementatie van een SAS-token.</span><span class="sxs-lookup"><span data-stu-id="2ca10-105">This topic explains how toouse Azure PowerShell with Resource Manager templates tooprovide a SAS token during deployment.</span></span> 

## <a name="add-private-template-toostorage-account"></a><span data-ttu-id="2ca10-106">Persoonlijke sjabloon toostorage account toevoegen</span><span class="sxs-lookup"><span data-stu-id="2ca10-106">Add private template toostorage account</span></span>

<span data-ttu-id="2ca10-107">U kunt uw sjablonen tooa storage-account toevoegen en toothem koppelen tijdens de implementatie met een SAS-token.</span><span class="sxs-lookup"><span data-stu-id="2ca10-107">You can add your templates tooa storage account and link toothem during deployment with a SAS token.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2ca10-108">Door Hallo onderstaande stappen te volgen, is Hallo blob met Hallo sjabloon toegankelijk tooonly Hallo accounteigenaar.</span><span class="sxs-lookup"><span data-stu-id="2ca10-108">By following hello steps below, hello blob containing hello template is accessible tooonly hello account owner.</span></span> <span data-ttu-id="2ca10-109">Bij het maken van een SAS-token voor Hallo blob is Hallo blob toegankelijk tooanyone met die URI.</span><span class="sxs-lookup"><span data-stu-id="2ca10-109">However, when you create a SAS token for hello blob, hello blob is accessible tooanyone with that URI.</span></span> <span data-ttu-id="2ca10-110">Als een andere gebruiker Hallo URI onderschept, is deze gebruiker kunnen tooaccess Hallo sjabloon.</span><span class="sxs-lookup"><span data-stu-id="2ca10-110">If another user intercepts hello URI, that user is able tooaccess hello template.</span></span> <span data-ttu-id="2ca10-111">Met behulp van een SAS-token is een prima manier voor het beperken van toegang tooyour sjablonen moet, maar u geen gevoelige gegevens, zoals wachtwoorden rechtstreeks in het Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="2ca10-111">Using a SAS token is a good way of limiting access tooyour templates, but you should not include sensitive data like passwords directly in hello template.</span></span>
> 
> 

<span data-ttu-id="2ca10-112">Hallo volgende voorbeeld stelt u een persoonlijke opslag account-container en een sjabloon uploadt:</span><span class="sxs-lookup"><span data-stu-id="2ca10-112">hello following example sets up a private storage account container and uploads a template:</span></span>
   
```powershell
# create a storage account for templates
New-AzureRmResourceGroup -Name ManageGroup -Location "South Central US"
New-AzureRmStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name} -Type Standard_LRS -Location "West US"
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name}

# create a container and upload template
New-AzureStorageContainer -Name templates -Permission Off
Set-AzureStorageBlobContent -Container templates -File c:\MyTemplates\storage.json
```

## <a name="provide-sas-token-during-deployment"></a><span data-ttu-id="2ca10-113">SAS-token opgeven tijdens de implementatie</span><span class="sxs-lookup"><span data-stu-id="2ca10-113">Provide SAS token during deployment</span></span>
<span data-ttu-id="2ca10-114">een persoonlijke sjabloon in een opslagaccount toodeploy een SAS-token genereren en deze opnemen in Hallo URI voor Hallo sjabloon.</span><span class="sxs-lookup"><span data-stu-id="2ca10-114">toodeploy a private template in a storage account, generate a SAS token and include it in hello URI for hello template.</span></span> <span data-ttu-id="2ca10-115">Stel Hallo verstrijken tijd tooallow voldoende tijd toocomplete Hallo-implementatie.</span><span class="sxs-lookup"><span data-stu-id="2ca10-115">Set hello expiry time tooallow enough time toocomplete hello deployment.</span></span>
   
```powershell
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name}

# get hello URI with hello SAS token
$templateuri = New-AzureStorageBlobSASToken -Container templates -Blob storage.json -Permission r `
  -ExpiryTime (Get-Date).AddHours(2.0) -FullUri

# provide URI with SAS token during deployment
New-AzureRmResourceGroup -Name ExampleGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri $templateuri
```

<span data-ttu-id="2ca10-116">Zie voor een voorbeeld van het gebruik van een SAS-token met gekoppelde sjablonen [gekoppelde sjablonen gebruiken met Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="2ca10-116">For an example of using a SAS token with linked templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="2ca10-117">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2ca10-117">Next steps</span></span>
* <span data-ttu-id="2ca10-118">Zie voor een inleiding toodeploying sjablonen, [implementeren van resources met Resource Manager-sjablonen en Azure PowerShell](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="2ca10-118">For an introduction toodeploying templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="2ca10-119">Zie voor een compleet codevoorbeeld-script waarmee een sjabloon wordt geïmplementeerd, [sjabloonscript Resource Manager implementeren](resource-manager-samples-powershell-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="2ca10-119">For a complete sample script that deploys a template, see [Deploy Resource Manager template script](resource-manager-samples-powershell-deploy.md)</span></span>
* <span data-ttu-id="2ca10-120">toodefine parameters in de sjabloon, Zie [sjablonen](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="2ca10-120">toodefine parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="2ca10-121">Abonnementen voor instructies over hoe ondernemingen tooeffectively Resource Manager kunt beheren, Zie [Azure enterprise scaffold - prescriptieve abonnement governance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="2ca10-121">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

