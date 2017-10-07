---
title: aaaDeploy resources met de REST-API en de sjabloon | Microsoft Docs
description: Azure Resource Manager en de REST-API van Resource Manager toodeploy een tooAzure resources gebruiken. Hallo-bronnen worden gedefinieerd in het Resource Manager-sjabloon.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 1d8fbd4c-78b0-425b-ba76-f2b7fd260b45
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/10/2017
ms.author: tomfitz
ms.openlocfilehash: 347ad3bdb604429e7291297d448688204af69b46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-resource-manager-rest-api"></a><span data-ttu-id="33bc8-104">Resources implementeren met Resource Manager-sjablonen en Resource Manager REST API</span><span class="sxs-lookup"><span data-stu-id="33bc8-104">Deploy resources with Resource Manager templates and Resource Manager REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="33bc8-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="33bc8-105">PowerShell</span></span>](resource-group-template-deploy.md)
> * [<span data-ttu-id="33bc8-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="33bc8-106">Azure CLI</span></span>](resource-group-template-deploy-cli.md)
> * [<span data-ttu-id="33bc8-107">Portal</span><span class="sxs-lookup"><span data-stu-id="33bc8-107">Portal</span></span>](resource-group-template-deploy-portal.md)
> * [<span data-ttu-id="33bc8-108">REST API</span><span class="sxs-lookup"><span data-stu-id="33bc8-108">REST API</span></span>](resource-group-template-deploy-rest.md)
> 
> 

<span data-ttu-id="33bc8-109">Dit artikel wordt uitgelegd hoe toouse Hallo REST-API van Resource Manager met Resource Manager-sjablonen toodeploy uw tooAzure resources.</span><span class="sxs-lookup"><span data-stu-id="33bc8-109">This article explains how toouse hello Resource Manager REST API with Resource Manager templates toodeploy your resources tooAzure.</span></span>  

> [!TIP]
> <span data-ttu-id="33bc8-110">Zie voor informatie over wanneer foutopsporing is een fout opgetreden tijdens de implementatie:</span><span class="sxs-lookup"><span data-stu-id="33bc8-110">For help with debugging an error during deployment, see:</span></span>
> 
> * <span data-ttu-id="33bc8-111">[Implementatiebewerkingen weergeven](resource-manager-deployment-operations.md) toolearn over het ophalen van informatie die u helpt problemen met de fout</span><span class="sxs-lookup"><span data-stu-id="33bc8-111">[View deployment operations](resource-manager-deployment-operations.md) toolearn about getting information that helps you troubleshoot your error</span></span>
> * <span data-ttu-id="33bc8-112">[Oplossen van veelvoorkomende fouten bij het implementeren van resources tooAzure met Azure Resource Manager](resource-manager-common-deployment-errors.md) toolearn hoe algemene implementatiefouten tooresolve</span><span class="sxs-lookup"><span data-stu-id="33bc8-112">[Troubleshoot common errors when deploying resources tooAzure with Azure Resource Manager](resource-manager-common-deployment-errors.md) toolearn how tooresolve common deployment errors</span></span>
> 
> 

<span data-ttu-id="33bc8-113">De sjabloon is een lokaal bestand of een extern bestand dat is beschikbaar via een URI.</span><span class="sxs-lookup"><span data-stu-id="33bc8-113">Your template can be either a local file or an external file that is available through a URI.</span></span> <span data-ttu-id="33bc8-114">Wanneer de sjabloon bevindt zich in een opslagaccount, kunt u access toohello sjabloon beperken en bieden een shared access signature (SAS)-token tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="33bc8-114">When your template resides in a storage account, you can restrict access toohello template and provide a shared access signature (SAS) token during deployment.</span></span>

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

## <a name="deploy-with-hello-rest-api"></a><span data-ttu-id="33bc8-115">Met de Hallo REST-API implementeren</span><span class="sxs-lookup"><span data-stu-id="33bc8-115">Deploy with hello REST API</span></span>
1. <span data-ttu-id="33bc8-116">Stel [algemene parameters en -koppen](https://docs.microsoft.com/rest/api/index), met inbegrip van verificatietokens.</span><span class="sxs-lookup"><span data-stu-id="33bc8-116">Set [common parameters and headers](https://docs.microsoft.com/rest/api/index), including authentication tokens.</span></span>
2. <span data-ttu-id="33bc8-117">Als u een bestaande resourcegroep niet hebt, kunt u een resourcegroep maken.</span><span class="sxs-lookup"><span data-stu-id="33bc8-117">If you do not have an existing resource group, create a resource group.</span></span> <span data-ttu-id="33bc8-118">Geef uw abonnements-ID, het Hallo-naam van de nieuwe resourcegroep Hallo en locatie die u nodig hebt voor uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="33bc8-118">Provide your subscription ID, hello name of hello new resource group, and location that you need for your solution.</span></span> <span data-ttu-id="33bc8-119">Zie voor meer informatie [een resourcegroep maken](https://docs.microsoft.com/rest/api/resources/resourcegroups#ResourceGroups_CreateOrUpdate).</span><span class="sxs-lookup"><span data-stu-id="33bc8-119">For more information, see [Create a resource group](https://docs.microsoft.com/rest/api/resources/resourcegroups#ResourceGroups_CreateOrUpdate).</span></span>
   
        PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>?api-version=2015-01-01
          <common headers>
          {
            "location": "West US",
            "tags": {
               "tagname1": "tagvalue1"
            }
          }
3. <span data-ttu-id="33bc8-120">Valideren van uw implementatie voordat deze wordt uitgevoerd door het uitvoeren van Hallo [valideren van de sjabloonimplementatie van een](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Validate) bewerking.</span><span class="sxs-lookup"><span data-stu-id="33bc8-120">Validate your deployment before executing it by running hello [Validate a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Validate) operation.</span></span> <span data-ttu-id="33bc8-121">Bij het testen van Hallo implementatie Geef parameters op exact dezelfde manier als bij het uitvoeren van Hallo-implementatie (weergegeven in de volgende stap Hallo).</span><span class="sxs-lookup"><span data-stu-id="33bc8-121">When testing hello deployment, provide parameters exactly as you would when executing hello deployment (shown in hello next step).</span></span>
4. <span data-ttu-id="33bc8-122">Maakt een implementatie.</span><span class="sxs-lookup"><span data-stu-id="33bc8-122">Create a deployment.</span></span> <span data-ttu-id="33bc8-123">Geef uw abonnements-ID, Hallo-naam van de resourcegroep Hallo Hallo-naam van het Hallo-implementatie en een koppeling tooyour sjabloon.</span><span class="sxs-lookup"><span data-stu-id="33bc8-123">Provide your subscription ID, hello name of hello resource group, hello name of hello deployment, and a link tooyour template.</span></span> <span data-ttu-id="33bc8-124">Zie voor meer informatie over het sjabloonbestand Hallo [parameterbestand](#parameter-file).</span><span class="sxs-lookup"><span data-stu-id="33bc8-124">For information about hello template file, see [Parameter file](#parameter-file).</span></span> <span data-ttu-id="33bc8-125">Zie voor meer informatie over Hallo REST-API toocreate een resourcegroep [sjabloonimplementatie met een maakt](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_CreateOrUpdate).</span><span class="sxs-lookup"><span data-stu-id="33bc8-125">For more information about hello REST API toocreate a resource group, see [Create a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_CreateOrUpdate).</span></span> <span data-ttu-id="33bc8-126">Kennisgeving Hallo **modus** te is ingesteld,**incrementele**.</span><span class="sxs-lookup"><span data-stu-id="33bc8-126">Notice hello **mode** is set too**Incremental**.</span></span> <span data-ttu-id="33bc8-127">instellen van een volledige implementatie toorun **modus** te**Complete**.</span><span class="sxs-lookup"><span data-stu-id="33bc8-127">toorun a complete deployment, set **mode** too**Complete**.</span></span> <span data-ttu-id="33bc8-128">Wees voorzichtig met behulp van Hallo volledige modus kunt u de resources die zich niet in uw sjabloon per ongeluk verwijderen.</span><span class="sxs-lookup"><span data-stu-id="33bc8-128">Be careful when using hello complete mode as you can inadvertently delete resources that are not in your template.</span></span>
   
        PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2015-01-01
          <common headers>
          {
            "properties": {
              "templateLink": {
                "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
                "contentVersion": "1.0.0.0"
              },
              "mode": "Incremental",
              "parametersLink": {
                "uri": "http://mystorageaccount.blob.core.windows.net/templates/parameters.json",
                "contentVersion": "1.0.0.0"
              }
            }
          }
   
      <span data-ttu-id="33bc8-129">Als u wilt dat toolog antwoordinhoud, aanvraaginhoud of beide, opnemen **debugSetting** in Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="33bc8-129">If you want toolog response content, request content, or both, include **debugSetting** in hello request.</span></span>
   
        "debugSetting": {
          "detailLevel": "requestContent, responseContent"
        }
   
      <span data-ttu-id="33bc8-130">U kunt instellen uw storage-account toouse een shared access signature (SAS)-token.</span><span class="sxs-lookup"><span data-stu-id="33bc8-130">You can set up your storage account toouse a shared access signature (SAS) token.</span></span> <span data-ttu-id="33bc8-131">Zie voor meer informatie [toegang delegeren met Shared Access Signature](https://docs.microsoft.com/rest/api/storageservices/delegating-access-with-a-shared-access-signature).</span><span class="sxs-lookup"><span data-stu-id="33bc8-131">For more information, see [Delegating Access with a Shared Access Signature](https://docs.microsoft.com/rest/api/storageservices/delegating-access-with-a-shared-access-signature).</span></span>
5. <span data-ttu-id="33bc8-132">Hallo-status van de sjabloonimplementatie Hallo ophalen.</span><span class="sxs-lookup"><span data-stu-id="33bc8-132">Get hello status of hello template deployment.</span></span> <span data-ttu-id="33bc8-133">Zie voor meer informatie [informatie ophalen over de sjabloonimplementatie van een](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get).</span><span class="sxs-lookup"><span data-stu-id="33bc8-133">For more information, see [Get information about a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get).</span></span>
   
          GET https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2015-01-01
           <common headers>

## <a name="parameter-file"></a><span data-ttu-id="33bc8-134">Parameterbestand</span><span class="sxs-lookup"><span data-stu-id="33bc8-134">Parameter file</span></span>

[!INCLUDE [resource-manager-parameter-file](../../includes/resource-manager-parameter-file.md)]

## <a name="next-steps"></a><span data-ttu-id="33bc8-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="33bc8-135">Next steps</span></span>
* <span data-ttu-id="33bc8-136">toolearn over het verwerken van asynchrone REST-bewerkingen, Zie [bijhouden asynchrone Azure bewerkingen](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="33bc8-136">toolearn about handling asynchronous REST operations, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
* <span data-ttu-id="33bc8-137">Zie voor een voorbeeld van het implementeren van resources via de .NET-clientbibliotheek Hallo [resources met behulp van .NET-bibliotheken en een sjabloon implementeren](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="33bc8-137">For an example of deploying resources through hello .NET client library, see [Deploy resources using .NET libraries and a template](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="33bc8-138">toodefine parameters in de sjabloon, Zie [sjablonen](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="33bc8-138">toodefine parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="33bc8-139">Zie voor instructies over het implementeren van uw oplossing toodifferent omgevingen [ontwikkel- en testomgevingen in Microsoft Azure](solution-dev-test-environments.md).</span><span class="sxs-lookup"><span data-stu-id="33bc8-139">For guidance on deploying your solution toodifferent environments, see [Development and test environments in Microsoft Azure](solution-dev-test-environments.md).</span></span>
* <span data-ttu-id="33bc8-140">Abonnementen voor instructies over hoe ondernemingen tooeffectively Resource Manager kunt beheren, Zie [Azure enterprise scaffold - prescriptieve abonnement governance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="33bc8-140">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

