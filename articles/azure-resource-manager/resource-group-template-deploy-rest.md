---
title: Resources met REST-API en de sjabloon implementeren | Microsoft Docs
description: Azure Resource Manager en de REST-API van Resource Manager gebruiken voor het implementeren van een bronnen in Azure. De resources zijn gedefinieerd in een Resource Manager-sjabloon.
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
ms.openlocfilehash: 46856a25fb57bb2c5a3c1aeae13c11655e1a58a5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-resource-manager-rest-api"></a><span data-ttu-id="96c8f-104">Resources implementeren met Resource Manager-sjablonen en Resource Manager REST API</span><span class="sxs-lookup"><span data-stu-id="96c8f-104">Deploy resources with Resource Manager templates and Resource Manager REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="96c8f-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="96c8f-105">PowerShell</span></span>](resource-group-template-deploy.md)
> * [<span data-ttu-id="96c8f-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="96c8f-106">Azure CLI</span></span>](resource-group-template-deploy-cli.md)
> * [<span data-ttu-id="96c8f-107">Portal</span><span class="sxs-lookup"><span data-stu-id="96c8f-107">Portal</span></span>](resource-group-template-deploy-portal.md)
> * [<span data-ttu-id="96c8f-108">REST API</span><span class="sxs-lookup"><span data-stu-id="96c8f-108">REST API</span></span>](resource-group-template-deploy-rest.md)
> 
> 

<span data-ttu-id="96c8f-109">In dit artikel wordt uitgelegd hoe de REST-API van Resource Manager gebruiken met Resource Manager-sjablonen voor het implementeren van uw resources in Azure.</span><span class="sxs-lookup"><span data-stu-id="96c8f-109">This article explains how to use the Resource Manager REST API with Resource Manager templates to deploy your resources to Azure.</span></span>  

> [!TIP]
> <span data-ttu-id="96c8f-110">Zie voor informatie over wanneer foutopsporing is een fout opgetreden tijdens de implementatie:</span><span class="sxs-lookup"><span data-stu-id="96c8f-110">For help with debugging an error during deployment, see:</span></span>
> 
> * <span data-ttu-id="96c8f-111">[Implementatiebewerkingen weergeven](resource-manager-deployment-operations.md) voor meer informatie over het ophalen van informatie die helpt u de fout oplossen</span><span class="sxs-lookup"><span data-stu-id="96c8f-111">[View deployment operations](resource-manager-deployment-operations.md) to learn about getting information that helps you troubleshoot your error</span></span>
> * <span data-ttu-id="96c8f-112">[Oplossen van veelvoorkomende fouten bij het implementeren van resources in Azure met Azure Resource Manager](resource-manager-common-deployment-errors.md) voor meer informatie over het oplossen van veelvoorkomende implementatiefouten</span><span class="sxs-lookup"><span data-stu-id="96c8f-112">[Troubleshoot common errors when deploying resources to Azure with Azure Resource Manager](resource-manager-common-deployment-errors.md) to learn how to resolve common deployment errors</span></span>
> 
> 

<span data-ttu-id="96c8f-113">De sjabloon is een lokaal bestand of een extern bestand dat is beschikbaar via een URI.</span><span class="sxs-lookup"><span data-stu-id="96c8f-113">Your template can be either a local file or an external file that is available through a URI.</span></span> <span data-ttu-id="96c8f-114">Wanneer de sjabloon bevindt zich in een opslagaccount, kunt u het beperken van toegang aan de sjabloon en een shared access signature (SAS)-token opgeven tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="96c8f-114">When your template resides in a storage account, you can restrict access to the template and provide a shared access signature (SAS) token during deployment.</span></span>

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

## <a name="deploy-with-the-rest-api"></a><span data-ttu-id="96c8f-115">Met de REST-API implementeren</span><span class="sxs-lookup"><span data-stu-id="96c8f-115">Deploy with the REST API</span></span>
1. <span data-ttu-id="96c8f-116">Stel [algemene parameters en -koppen](https://docs.microsoft.com/rest/api/index), met inbegrip van verificatietokens.</span><span class="sxs-lookup"><span data-stu-id="96c8f-116">Set [common parameters and headers](https://docs.microsoft.com/rest/api/index), including authentication tokens.</span></span>
2. <span data-ttu-id="96c8f-117">Als u een bestaande resourcegroep niet hebt, kunt u een resourcegroep maken.</span><span class="sxs-lookup"><span data-stu-id="96c8f-117">If you do not have an existing resource group, create a resource group.</span></span> <span data-ttu-id="96c8f-118">Geef uw abonnements-ID, de naam van de nieuwe resourcegroep en locatie die u nodig hebt voor uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="96c8f-118">Provide your subscription ID, the name of the new resource group, and location that you need for your solution.</span></span> <span data-ttu-id="96c8f-119">Zie voor meer informatie [een resourcegroep maken](https://docs.microsoft.com/rest/api/resources/resourcegroups#ResourceGroups_CreateOrUpdate).</span><span class="sxs-lookup"><span data-stu-id="96c8f-119">For more information, see [Create a resource group](https://docs.microsoft.com/rest/api/resources/resourcegroups#ResourceGroups_CreateOrUpdate).</span></span>
   
        PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>?api-version=2015-01-01
          <common headers>
          {
            "location": "West US",
            "tags": {
               "tagname1": "tagvalue1"
            }
          }
3. <span data-ttu-id="96c8f-120">Valideren van uw implementatie voordat deze wordt uitgevoerd door het uitvoeren van de [valideren van de sjabloonimplementatie van een](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Validate) bewerking.</span><span class="sxs-lookup"><span data-stu-id="96c8f-120">Validate your deployment before executing it by running the [Validate a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Validate) operation.</span></span> <span data-ttu-id="96c8f-121">Bij het testen van de implementatie, Geef parameters op exact dezelfde manier als bij het uitvoeren van de implementatie (weergegeven in de volgende stap).</span><span class="sxs-lookup"><span data-stu-id="96c8f-121">When testing the deployment, provide parameters exactly as you would when executing the deployment (shown in the next step).</span></span>
4. <span data-ttu-id="96c8f-122">Maakt een implementatie.</span><span class="sxs-lookup"><span data-stu-id="96c8f-122">Create a deployment.</span></span> <span data-ttu-id="96c8f-123">Geef uw abonnements-ID, de naam van de resourcegroep, de naam van de implementatie en een koppeling naar uw sjabloon.</span><span class="sxs-lookup"><span data-stu-id="96c8f-123">Provide your subscription ID, the name of the resource group, the name of the deployment, and a link to your template.</span></span> <span data-ttu-id="96c8f-124">Zie voor meer informatie over het sjabloonbestand [parameterbestand](#parameter-file).</span><span class="sxs-lookup"><span data-stu-id="96c8f-124">For information about the template file, see [Parameter file](#parameter-file).</span></span> <span data-ttu-id="96c8f-125">Zie voor meer informatie over de REST-API om een resourcegroep te maken, [sjabloonimplementatie met een maakt](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_CreateOrUpdate).</span><span class="sxs-lookup"><span data-stu-id="96c8f-125">For more information about the REST API to create a resource group, see [Create a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_CreateOrUpdate).</span></span> <span data-ttu-id="96c8f-126">U ziet de **modus** is ingesteld op **incrementele**.</span><span class="sxs-lookup"><span data-stu-id="96c8f-126">Notice the **mode** is set to **Incremental**.</span></span> <span data-ttu-id="96c8f-127">Als u wilt uitvoeren van een volledige implementatie, **modus** naar **Complete**.</span><span class="sxs-lookup"><span data-stu-id="96c8f-127">To run a complete deployment, set **mode** to **Complete**.</span></span> <span data-ttu-id="96c8f-128">Wees voorzichtig met behulp van de volledige modus kunt u de resources die zich niet in uw sjabloon per ongeluk verwijderen.</span><span class="sxs-lookup"><span data-stu-id="96c8f-128">Be careful when using the complete mode as you can inadvertently delete resources that are not in your template.</span></span>
   
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
   
      <span data-ttu-id="96c8f-129">Als u registreren antwoordinhoud, aanvraaginhoud of beide wilt, opnemen **debugSetting** in de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="96c8f-129">If you want to log response content, request content, or both, include **debugSetting** in the request.</span></span>
   
        "debugSetting": {
          "detailLevel": "requestContent, responseContent"
        }
   
      <span data-ttu-id="96c8f-130">U kunt uw storage-account instellen om te gebruiken een shared access signature (SAS)-token.</span><span class="sxs-lookup"><span data-stu-id="96c8f-130">You can set up your storage account to use a shared access signature (SAS) token.</span></span> <span data-ttu-id="96c8f-131">Zie voor meer informatie [toegang delegeren met Shared Access Signature](https://docs.microsoft.com/rest/api/storageservices/delegating-access-with-a-shared-access-signature).</span><span class="sxs-lookup"><span data-stu-id="96c8f-131">For more information, see [Delegating Access with a Shared Access Signature](https://docs.microsoft.com/rest/api/storageservices/delegating-access-with-a-shared-access-signature).</span></span>
5. <span data-ttu-id="96c8f-132">De status van de sjabloonimplementatie niet ophalen.</span><span class="sxs-lookup"><span data-stu-id="96c8f-132">Get the status of the template deployment.</span></span> <span data-ttu-id="96c8f-133">Zie voor meer informatie [informatie ophalen over de sjabloonimplementatie van een](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get).</span><span class="sxs-lookup"><span data-stu-id="96c8f-133">For more information, see [Get information about a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get).</span></span>
   
          GET https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2015-01-01
           <common headers>

## <a name="parameter-file"></a><span data-ttu-id="96c8f-134">Parameterbestand</span><span class="sxs-lookup"><span data-stu-id="96c8f-134">Parameter file</span></span>

[!INCLUDE [resource-manager-parameter-file](../../includes/resource-manager-parameter-file.md)]

## <a name="next-steps"></a><span data-ttu-id="96c8f-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="96c8f-135">Next steps</span></span>
* <span data-ttu-id="96c8f-136">Zie voor meer informatie over het verwerken van asynchrone REST-bewerkingen, [bijhouden asynchrone Azure bewerkingen](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="96c8f-136">To learn about handling asynchronous REST operations, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
* <span data-ttu-id="96c8f-137">Zie voor een voorbeeld van het implementeren van resources via de .NET-clientbibliotheek [resources met behulp van .NET-bibliotheken en een sjabloon implementeren](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="96c8f-137">For an example of deploying resources through the .NET client library, see [Deploy resources using .NET libraries and a template](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="96c8f-138">Om parameters te definiëren in de sjabloon, Zie [sjablonen](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="96c8f-138">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="96c8f-139">Zie voor instructies over het implementeren van uw oplossing in verschillende omgevingen [Ontwikkeling en testomgevingen in Microsoft Azure](solution-dev-test-environments.md).</span><span class="sxs-lookup"><span data-stu-id="96c8f-139">For guidance on deploying your solution to different environments, see [Development and test environments in Microsoft Azure](solution-dev-test-environments.md).</span></span>
* <span data-ttu-id="96c8f-140">Voor begeleiding bij de manier waarop ondernemingen Resource Manager effectief kunnen gebruiken voor het beheer van abonnementen, gaat u naar [Azure enterprise-platform - Prescriptieve abonnementsgovernance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="96c8f-140">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

