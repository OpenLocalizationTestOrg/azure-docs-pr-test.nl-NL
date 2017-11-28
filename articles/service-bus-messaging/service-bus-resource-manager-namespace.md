---
title: aaaCreate Service Bus-naamruimte met een Azure Resource Manager-sjabloon | Microsoft Docs
description: Gebruik Azure Resource Manager-sjabloon toocreate een Service Bus-naamruimte
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: dc0d6482-6344-4cef-8644-d4573639f5e4
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: fddf370affe761a734991ae9b60c1e5825e54ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-using-an-azure-resource-manager-template"></a><span data-ttu-id="c76ed-103">Een Service Bus-naamruimte met een Azure Resource Manager-sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="c76ed-103">Create a Service Bus namespace using an Azure Resource Manager template</span></span>

<span data-ttu-id="c76ed-104">Dit artikel wordt beschreven hoe toouse een Azure Resource Manager-sjabloon waarmee u een Service Bus-naamruimte van het type **Messaging** met een standaard en eenvoudige SKU.</span><span class="sxs-lookup"><span data-stu-id="c76ed-104">This article describes how toouse an Azure Resource Manager template that creates a Service Bus namespace of type **Messaging** with a Standard/Basic SKU.</span></span> <span data-ttu-id="c76ed-105">Hallo artikel definieert ook Hallo-parameters die zijn opgegeven voor de uitvoering van Hallo Hallo-implementatie.</span><span class="sxs-lookup"><span data-stu-id="c76ed-105">hello article also defines hello parameters that are specified for hello execution of hello deployment.</span></span> <span data-ttu-id="c76ed-106">U kunt deze sjabloon voor uw eigen implementaties gebruiken of aanpassen toomeet uw vereisten.</span><span class="sxs-lookup"><span data-stu-id="c76ed-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="c76ed-107">Zie voor meer informatie over het maken van sjablonen [Azure Resource Manager-sjablonen samenstellen][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="c76ed-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="c76ed-108">Zie voor de volledige sjabloon hello, Hallo [Service Bus-naamruimte sjabloon] [ Service Bus namespace template] op GitHub.</span><span class="sxs-lookup"><span data-stu-id="c76ed-108">For hello complete template, see hello [Service Bus namespace template][Service Bus namespace template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="c76ed-109">Hallo na Azure Resource Manager-sjablonen zijn beschikbaar voor download- en implementatie.</span><span class="sxs-lookup"><span data-stu-id="c76ed-109">hello following Azure Resource Manager templates are available for download and deployment.</span></span> 
> 
> * [<span data-ttu-id="c76ed-110">Een Service Bus-naamruimte maken met de wachtrij</span><span class="sxs-lookup"><span data-stu-id="c76ed-110">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="c76ed-111">Een Service Bus-naamruimte met onderwerp en een abonnement maken</span><span class="sxs-lookup"><span data-stu-id="c76ed-111">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> * [<span data-ttu-id="c76ed-112">Een Service Bus-naamruimte met een wachtrij en autorisatie regel maken</span><span class="sxs-lookup"><span data-stu-id="c76ed-112">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="c76ed-113">Een Service Bus-naamruimte maken met onderwerp, abonnement en regel</span><span class="sxs-lookup"><span data-stu-id="c76ed-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="c76ed-114">toocheck voor de meest recente sjablonen hello, gaat u naar Hallo [Azure-Snelstartsjablonen] [ Azure Quickstart Templates] galerie en zoek naar Service Bus.</span><span class="sxs-lookup"><span data-stu-id="c76ed-114">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Service Bus.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="c76ed-115">Wat wilt u implementeren?</span><span class="sxs-lookup"><span data-stu-id="c76ed-115">What will you deploy?</span></span>
<span data-ttu-id="c76ed-116">Met deze sjabloon, implementeert u een Service Bus-naamruimte met een [Basic, Standard of Premium](https://azure.microsoft.com/pricing/details/service-bus/) SKU.</span><span class="sxs-lookup"><span data-stu-id="c76ed-116">With this template, you will deploy a Service Bus namespace with a [Basic, Standard, or Premium](https://azure.microsoft.com/pricing/details/service-bus/) SKU.</span></span>

<span data-ttu-id="c76ed-117">toorun implementatie automatisch Hallo, klikt u op de knop volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="c76ed-117">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="c76ed-118">[![TooAzure implementeren](./media/service-bus-resource-manager-namespace/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-servicebus-create-namespace%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="c76ed-118">[![Deploy tooAzure](./media/service-bus-resource-manager-namespace/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-servicebus-create-namespace%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="c76ed-119">Parameters</span><span class="sxs-lookup"><span data-stu-id="c76ed-119">Parameters</span></span>
<span data-ttu-id="c76ed-120">Met Azure Resource Manager u parameters definiëren voor waarden gewenste toospecify wanneer Hallo sjabloon wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="c76ed-120">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="c76ed-121">Hallo-sjabloon bevat een sectie met de naam `Parameters` die Hallo parameterwaarden bevat.</span><span class="sxs-lookup"><span data-stu-id="c76ed-121">hello template includes a section called `Parameters` that contains all of hello parameter values.</span></span> <span data-ttu-id="c76ed-122">U moet een parameter voor de waarden die variëren op basis van Hallo-project die u implementeert of op basis van Hallo-omgeving die u om te implementeert definiëren.</span><span class="sxs-lookup"><span data-stu-id="c76ed-122">You should define a parameter for those values that will vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="c76ed-123">Definieer parameters niet voor waarden die altijd blijft dezelfde Hallo.</span><span class="sxs-lookup"><span data-stu-id="c76ed-123">Do not define parameters for values that will always stay hello same.</span></span> <span data-ttu-id="c76ed-124">De waarde van elke parameter wordt gebruikt in Hallo sjabloon toodefine Hallo resources die zijn geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="c76ed-124">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="c76ed-125">Deze sjabloon definieert Hallo parameters te volgen.</span><span class="sxs-lookup"><span data-stu-id="c76ed-125">This template defines hello following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="c76ed-126">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="c76ed-126">serviceBusNamespaceName</span></span>
<span data-ttu-id="c76ed-127">Hallo-naam van Hallo Service Bus-naamruimte toocreate.</span><span class="sxs-lookup"><span data-stu-id="c76ed-127">hello name of hello Service Bus namespace toocreate.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string",
"metadata": { 
    "description": "Name of hello Service Bus namespace" 
    }
}
```

### <a name="servicebussku"></a><span data-ttu-id="c76ed-128">serviceBusSKU</span><span class="sxs-lookup"><span data-stu-id="c76ed-128">serviceBusSKU</span></span>
<span data-ttu-id="c76ed-129">Hallo-naam van Service Bus Hallo [SKU](https://azure.microsoft.com/pricing/details/service-bus/) toocreate.</span><span class="sxs-lookup"><span data-stu-id="c76ed-129">hello name of hello Service Bus [SKU](https://azure.microsoft.com/pricing/details/service-bus/) toocreate.</span></span>

```json
"serviceBusSku": { 
    "type": "string", 
    "allowedValues": [ 
        "Basic", 
        "Standard",
        "Premium" 
    ], 
    "defaultValue": "Standard", 
    "metadata": { 
        "description": "hello messaging tier for service Bus namespace" 
    } 

```

<span data-ttu-id="c76ed-130">Hallo sjabloon definieert Hallo-waarden die zijn toegestaan voor deze parameter (Basic, Standard of Premium) en een standaardwaarde (standaard) wordt toegewezen als er geen waarde is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="c76ed-130">hello template defines hello values that are permitted for this parameter (Basic, Standard, or Premium) and assigns a default value (Standard) if no value is specified.</span></span>

<span data-ttu-id="c76ed-131">Zie voor meer informatie over prijzen voor Service Bus [Service Bus-prijzen en facturering][Service Bus pricing and billing].</span><span class="sxs-lookup"><span data-stu-id="c76ed-131">For more information about Service Bus pricing, see [Service Bus pricing and billing][Service Bus pricing and billing].</span></span>

### <a name="servicebusapiversion"></a><span data-ttu-id="c76ed-132">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="c76ed-132">serviceBusApiVersion</span></span>
<span data-ttu-id="c76ed-133">Hallo Service Bus-API-versie van Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="c76ed-133">hello Service Bus API version of hello template.</span></span>

```json
"serviceBusApiVersion": { 
       "type": "string", 
       "defaultValue": "2015-08-01", 
       "metadata": { 
           "description": "Service Bus ApiVersion used by hello template" 
       } 
```

## <a name="resources-toodeploy"></a><span data-ttu-id="c76ed-134">Resources toodeploy</span><span class="sxs-lookup"><span data-stu-id="c76ed-134">Resources toodeploy</span></span>
### <a name="service-bus-namespace"></a><span data-ttu-id="c76ed-135">Service Bus-naamruimte</span><span class="sxs-lookup"><span data-stu-id="c76ed-135">Service Bus namespace</span></span>
<span data-ttu-id="c76ed-136">Maakt een standaard Service Bus-naamruimte van het type **Messaging**.</span><span class="sxs-lookup"><span data-stu-id="c76ed-136">Creates a standard Service Bus namespace of type **Messaging**.</span></span>

```json
"resources": [
    {
        "apiVersion": "[parameters('serviceBusApiVersion')]",
        "name": "[parameters('serviceBusNamespaceName')]",
        "type": "Microsoft.ServiceBus/Namespaces",
        "location": "[variables('location')]",
        "kind": "Messaging",
        "sku": {
            "name": "StandardSku",
            "tier": "Standard"
        },
        "properties": {
        }
    }
]
```

## <a name="commands-toorun-deployment"></a><span data-ttu-id="c76ed-137">Opdrachten toorun implementatie</span><span class="sxs-lookup"><span data-stu-id="c76ed-137">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="c76ed-138">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c76ed-138">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName <resource-group-name> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-servicebus-create-namespace/azuredeploy.json
```

### <a name="azure-cli"></a><span data-ttu-id="c76ed-139">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c76ed-139">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create <my-resource-group> <my-deployment-name> --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-servicebus-create-namespace/azuredeploy.json
```

## <a name="next-steps"></a><span data-ttu-id="c76ed-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c76ed-140">Next steps</span></span>
<span data-ttu-id="c76ed-141">Nu u hebt gemaakt en geïmplementeerd resources met behulp van Azure Resource Manager, kunt u nagaan hoe toomanage deze resources door te lezen van deze artikelen:</span><span class="sxs-lookup"><span data-stu-id="c76ed-141">Now that you've created and deployed resources using Azure Resource Manager, learn how toomanage these resources by reading these articles:</span></span>

* [<span data-ttu-id="c76ed-142">Servicebus met PowerShell beheren</span><span class="sxs-lookup"><span data-stu-id="c76ed-142">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="c76ed-143">Service Bus-resources beheren met Hallo Service Bus Explorer</span><span class="sxs-lookup"><span data-stu-id="c76ed-143">Manage Service Bus resources with hello Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Service Bus namespace template]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-servicebus-create-namespace/
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Service Bus pricing and billing]: service-bus-pricing-billing.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
