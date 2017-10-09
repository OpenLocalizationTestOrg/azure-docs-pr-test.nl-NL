---
title: de implementatievolgorde aaaSet voor Azure-resources | Microsoft Docs
description: "Hierin wordt beschreven hoe tooset één resource als afhankelijk is van een andere bron tijdens implementatie tooensure resources in de juiste volgorde Hallo zijn geïmplementeerd."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.assetid: 34ebaf1e-480c-4b4d-9bf6-251bd3f8f2cf
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/03/2017
ms.author: tomfitz
ms.openlocfilehash: 2f658f4c85236966c46b34a65aafb8426c92806c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="define-hello-order-for-deploying-resources-in-azure-resource-manager-templates"></a><span data-ttu-id="2fcb5-103">Hallo volgorde voor het implementeren van resources in Azure Resource Manager-sjablonen definiëren</span><span class="sxs-lookup"><span data-stu-id="2fcb5-103">Define hello order for deploying resources in Azure Resource Manager templates</span></span>
<span data-ttu-id="2fcb5-104">Voor een bepaalde bron, kunnen er andere resources moeten bestaan voordat Hallo resource wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-104">For a given resource, there can be other resources that must exist before hello resource is deployed.</span></span> <span data-ttu-id="2fcb5-105">Bijvoorbeeld, moet een SQL-server bestaan voordat u probeert toodeploy een SQL-database.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-105">For example, a SQL server must exist before attempting toodeploy a SQL database.</span></span> <span data-ttu-id="2fcb5-106">U definiëren deze relatie met het markeren van een resource als afhankelijke op Hallo andere resource.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-106">You define this relationship by marking one resource as dependent on hello other resource.</span></span> <span data-ttu-id="2fcb5-107">U definieert een afhankelijkheid Hello **dependsOn** element, of met behulp van Hallo **verwijzing** functie.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-107">You define a dependency with hello **dependsOn** element, or by using hello **reference** function.</span></span> 

<span data-ttu-id="2fcb5-108">Resource Manager evalueert Hallo afhankelijkheden tussen resources en ze worden geïmplementeerd in de afhankelijke volgorde.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-108">Resource Manager evaluates hello dependencies between resources, and deploys them in their dependent order.</span></span> <span data-ttu-id="2fcb5-109">Wanneer u resources zijn niet afhankelijk van elkaar, worden deze door Resource Manager parallel implementeert.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-109">When resources are not dependent on each other, Resource Manager deploys them in parallel.</span></span> <span data-ttu-id="2fcb5-110">U hoeft alleen toodefine afhankelijkheden voor resources die zijn geïmplementeerd in Hallo dezelfde sjabloon.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-110">You only need toodefine dependencies for resources that are deployed in hello same template.</span></span> 

## <a name="dependson"></a><span data-ttu-id="2fcb5-111">dependsOn</span><span class="sxs-lookup"><span data-stu-id="2fcb5-111">dependsOn</span></span>
<span data-ttu-id="2fcb5-112">Hallo dependsOn element kunt toodefine één resource als een afhankelijk zijn van een of meer resources, in uw sjabloon.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-112">Within your template, hello dependsOn element enables you toodefine one resource as a dependent on one or more resources.</span></span> <span data-ttu-id="2fcb5-113">De waarde kan een door komma's gescheiden lijst met resourcenamen zijn.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-113">Its value can be a comma-separated list of resource names.</span></span> 

<span data-ttu-id="2fcb5-114">Hallo volgende voorbeeld ziet u een virtuele-machineschaalset die afhankelijk zijn van een load balancer, het virtuele netwerk en een lus die meerdere opslagaccounts worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-114">hello following example shows a virtual machine scale set that depends on a load balancer, virtual network, and a loop that creates multiple storage accounts.</span></span> <span data-ttu-id="2fcb5-115">Deze andere resources worden niet weergegeven in het volgende voorbeeld Hallo, maar moeten ze tooexist elders in Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-115">These other resources are not shown in hello following example, but they would need tooexist elsewhere in hello template.</span></span>

```json
{
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  "name": "[variables('namingInfix')]",
  "location": "[variables('location')]",
  "apiVersion": "2016-03-30",
  "tags": {
    "displayName": "VMScaleSet"
  },
  "dependsOn": [
    "[variables('loadBalancerName')]",
    "[variables('virtualNetworkName')]",
    "storageLoop",
  ],
  ...
}
```

<span data-ttu-id="2fcb5-116">In de Hallo voorgaande voorbeeld, een afhankelijkheid is opgenomen op Hallo-resources die zijn gemaakt via een For-lus kopiëren met de naam **storageLoop**.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-116">In hello preceding example, a dependency is included on hello resources that are created through a copy loop named **storageLoop**.</span></span> <span data-ttu-id="2fcb5-117">Zie voor een voorbeeld [maken van meerdere exemplaren van resources in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="2fcb5-117">For an example, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

<span data-ttu-id="2fcb5-118">Bij het definiëren van afhankelijkheden, kunt u Hallo resource provider-naamruimte en de resource type tooavoid dubbelzinnigheid kunt opnemen.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-118">When defining dependencies, you can include hello resource provider namespace and resource type tooavoid ambiguity.</span></span> <span data-ttu-id="2fcb5-119">Bijvoorbeeld, tooclarify een load balancer en het virtuele netwerk dat mogelijk Hallo die dezelfde namen als andere resources, gebruik Hallo volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="2fcb5-119">For example, tooclarify a load balancer and virtual network that may have hello same names as other resources, use hello following format:</span></span>

```json
"dependsOn": [
  "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
  "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
]
``` 

<span data-ttu-id="2fcb5-120">Hoewel u mogelijk geneigd toouse dependsOn toomap relaties tussen uw resources, is het belangrijk toounderstand waarom u dit doet.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-120">While you may be inclined toouse dependsOn toomap relationships between your resources, it's important toounderstand why you're doing it.</span></span> <span data-ttu-id="2fcb5-121">DependsOn is bijvoorbeeld toodocument hoe resources onderling verbonden, niet de juiste aanpak Hallo.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-121">For example, toodocument how resources are interconnected, dependsOn is not hello right approach.</span></span> <span data-ttu-id="2fcb5-122">U kunt het welke resources zijn gedefinieerd in Hallo dependsOn element na de implementatie kan geen query uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-122">You cannot query which resources were defined in hello dependsOn element after deployment.</span></span> <span data-ttu-id="2fcb5-123">Met behulp van dependsOn u mogelijk gevolgen hebben voor implementatietijd omdat Resource Manager niet is geïmplementeerd in parallelle twee resources met een afhankelijkheid.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-123">By using dependsOn, you potentially impact deployment time because Resource Manager does not deploy in parallel two resources that have a dependency.</span></span> <span data-ttu-id="2fcb5-124">Gebruik in plaats daarvan toodocument relaties tussen bronnen, [resources](/rest/api/resources/resourcelinks).</span><span class="sxs-lookup"><span data-stu-id="2fcb5-124">toodocument relationships between resources, instead use [resource linking](/rest/api/resources/resourcelinks).</span></span>

## <a name="child-resources"></a><span data-ttu-id="2fcb5-125">Onderliggende resources</span><span class="sxs-lookup"><span data-stu-id="2fcb5-125">Child resources</span></span>
<span data-ttu-id="2fcb5-126">Hallo resources eigenschap kunt u toospecify onderliggende resources die zijn gerelateerd toohello resource wordt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-126">hello resources property allows you toospecify child resources that are related toohello resource being defined.</span></span> <span data-ttu-id="2fcb5-127">Onderliggende resources kunnen alleen worden gedefinieerd vijf niveaus.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-127">Child resources can only be defined five levels deep.</span></span> <span data-ttu-id="2fcb5-128">Het is belangrijk toonote die een impliciete afhankelijkheid niet is gemaakt tussen een onderliggende resource en Hallo bovenliggende resource.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-128">It is important toonote that an implicit dependency is not created between a child resource and hello parent resource.</span></span> <span data-ttu-id="2fcb5-129">Als u moet onderliggende resource toobe geïmplementeerd na Hallo bovenliggende resource hello, moet u deze afhankelijkheid met Hallo dependsOn eigenschap expliciet vermelden.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-129">If you need hello child resource toobe deployed after hello parent resource, you must explicitly state that dependency with hello dependsOn property.</span></span> 

<span data-ttu-id="2fcb5-130">Elke bovenliggende resource accepteert alleen bepaalde resourcetypen als onderliggende resources.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-130">Each parent resource accepts only certain resource types as child resources.</span></span> <span data-ttu-id="2fcb5-131">Hallo geaccepteerd brontypen die zijn opgegeven in Hallo [sjabloonschema](https://github.com/Azure/azure-resource-manager-schemas) van Hallo bovenliggende resource.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-131">hello accepted resource types are specified in hello [template schema](https://github.com/Azure/azure-resource-manager-schemas) of hello parent resource.</span></span> <span data-ttu-id="2fcb5-132">Hallo-naam van onderliggende brontype bevat Hallo-naam van Hallo bovenliggende brontype, zoals **Microsoft.Web/sites/config** en **Microsoft.Web/sites/extensions** zijn beide onderliggende resources van Hallo  **Microsoft.Web/sites**.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-132">hello name of child resource type includes hello name of hello parent resource type, such as **Microsoft.Web/sites/config** and **Microsoft.Web/sites/extensions** are both child resources of hello **Microsoft.Web/sites**.</span></span>

<span data-ttu-id="2fcb5-133">Hallo volgende voorbeeld ziet u een SQL server en SQL-database.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-133">hello following example shows a SQL server and SQL database.</span></span> <span data-ttu-id="2fcb5-134">U ziet dat er een expliciete afhankelijkheid is gedefinieerd tussen Hallo SQL-database en SQL server, hoewel Hallo-database een onderliggend element van het Hallo-server is.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-134">Notice that an explicit dependency is defined between hello SQL database and SQL server, even though hello database is a child of hello server.</span></span>

```json
"resources": [
  {
    "name": "[variables('sqlserverName')]",
    "type": "Microsoft.Sql/servers",
    "location": "[resourceGroup().location]",
    "tags": {
      "displayName": "SqlServer"
    },
    "apiVersion": "2014-04-01-preview",
    "properties": {
      "administratorLogin": "[parameters('administratorLogin')]",
      "administratorLoginPassword": "[parameters('administratorLoginPassword')]"
    },
    "resources": [
      {
        "name": "[parameters('databaseName')]",
        "type": "databases",
        "location": "[resourceGroup().location]",
        "tags": {
          "displayName": "Database"
        },
        "apiVersion": "2014-04-01-preview",
        "dependsOn": [
          "[variables('sqlserverName')]"
        ],
        "properties": {
          "edition": "[parameters('edition')]",
          "collation": "[parameters('collation')]",
          "maxSizeBytes": "[parameters('maxSizeBytes')]",
          "requestedServiceObjectiveName": "[parameters('requestedServiceObjectiveName')]"
        }
      }
    ]
  }
]
```

## <a name="reference-function"></a><span data-ttu-id="2fcb5-135">verwijzing naar functie</span><span class="sxs-lookup"><span data-stu-id="2fcb5-135">reference function</span></span>
<span data-ttu-id="2fcb5-136">Hallo [verwijst naar functie](resource-group-template-functions-resource.md#reference) wordt een tooderive expressie de waarde van andere JSON naam / waarde-paren of runtime-bronnen.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-136">hello [reference function](resource-group-template-functions-resource.md#reference) enables an expression tooderive its value from other JSON name and value pairs or runtime resources.</span></span> <span data-ttu-id="2fcb5-137">Verwijzingsexpressies declareren impliciet dat één resource afhankelijk van een andere is.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-137">Reference expressions implicitly declare that one resource depends on another.</span></span> <span data-ttu-id="2fcb5-138">Hallo algemene indeling is:</span><span class="sxs-lookup"><span data-stu-id="2fcb5-138">hello general format is:</span></span>

```json
reference('resourceName').propertyPath
```

<span data-ttu-id="2fcb5-139">In Hallo voorbeeld te volgen, een CDN-eindpunt expliciet is afhankelijk van Hallo CDN-profiel en impliciet afhankelijk is van een web-app.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-139">In hello following example, a CDN endpoint explicitly depends on hello CDN profile, and implicitly depends on a web app.</span></span>

```json
{
    "name": "[variables('endpointName')]",
    "type": "endpoints",
    "location": "[resourceGroup().location]",
    "apiVersion": "2016-04-02",
    "dependsOn": [
            "[variables('profileName')]"
    ],
    "properties": {
        "originHostHeader": "[reference(variables('webAppName')).hostNames[0]]",
        ...
    }
```

<span data-ttu-id="2fcb5-140">U kunt dit element of Hallo dependsOn element toospecify afhankelijkheden, maar u hoeft geen toouse beide voor Hallo dezelfde afhankelijke bron.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-140">You can use either this element or hello dependsOn element toospecify dependencies, but you do not need toouse both for hello same dependent resource.</span></span> <span data-ttu-id="2fcb5-141">Gebruik indien mogelijk een impliciete verwijzing tooavoid een onnodige afhankelijkheid toevoegen.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-141">Whenever possible, use an implicit reference tooavoid adding an unnecessary dependency.</span></span>

<span data-ttu-id="2fcb5-142">toolearn meer, Zie [verwijst naar functie](resource-group-template-functions-resource.md#reference).</span><span class="sxs-lookup"><span data-stu-id="2fcb5-142">toolearn more, see [reference function](resource-group-template-functions-resource.md#reference).</span></span>

## <a name="recommendations-for-setting-dependencies"></a><span data-ttu-id="2fcb5-143">Aanbevelingen voor het instellen van de afhankelijkheden</span><span class="sxs-lookup"><span data-stu-id="2fcb5-143">Recommendations for setting dependencies</span></span>

<span data-ttu-id="2fcb5-144">Wanneer u beslist welke tooset afhankelijkheden, gebruikt u Hallo richtlijnen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2fcb5-144">When deciding what dependencies tooset, use hello following guidelines:</span></span>

* <span data-ttu-id="2fcb5-145">Afhankelijkheden van zo weinig mogelijk ingesteld.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-145">Set as few dependencies as possible.</span></span>
* <span data-ttu-id="2fcb5-146">Stel een onderliggende resource als afhankelijk van de bovenliggende resource.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-146">Set a child resource as dependent on its parent resource.</span></span>
* <span data-ttu-id="2fcb5-147">Gebruik Hallo **verwijzing** tooset impliciete afhankelijkheden tussen resources die een eigenschap tooshare moeten werken.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-147">Use hello **reference** function tooset implicit dependencies between resources that need tooshare a property.</span></span> <span data-ttu-id="2fcb5-148">Voeg een expliciete afhankelijkheid niet (**dependsOn**) wanneer u een impliciete afhankelijkheid al hebt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-148">Do not add an explicit dependency (**dependsOn**) when you have already defined an implicit dependency.</span></span> <span data-ttu-id="2fcb5-149">Deze benadering minder kans Hallo van onnodige afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-149">This approach reduces hello risk of having unnecessary dependencies.</span></span> 
* <span data-ttu-id="2fcb5-150">Een afhankelijkheid ingesteld wanneer een resource kan niet worden **gemaakt** zonder de functionaliteit van een andere resource.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-150">Set a dependency when a resource cannot be **created** without functionality from another resource.</span></span> <span data-ttu-id="2fcb5-151">Stel een afhankelijkheid niet als Hallo bronnen alleen na de implementatie werken.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-151">Do not set a dependency if hello resources only interact after deployment.</span></span>
* <span data-ttu-id="2fcb5-152">Laat afhankelijkheden cascade zonder expliciet instelt.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-152">Let dependencies cascade without setting them explicitly.</span></span> <span data-ttu-id="2fcb5-153">Bijvoorbeeld, de virtuele machine is afhankelijk van de virtuele netwerkinterface en Hallo virtuele netwerkinterface is afhankelijk van een virtueel netwerk en openbare IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-153">For example, your virtual machine depends on a virtual network interface, and hello virtual network interface depends on a virtual network and public IP addresses.</span></span> <span data-ttu-id="2fcb5-154">Daarom Hallo virtuele machine is geïmplementeerd nadat alle drie resources, maar Hallo virtuele machine niet expliciet als afhankelijk is van alle drie resources instelt.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-154">Therefore, hello virtual machine is deployed after all three resources, but do not explicitly set hello virtual machine as dependent on all three resources.</span></span> <span data-ttu-id="2fcb5-155">Deze aanpak wordt uitleg gegeven over Hallo afhankelijkheid volgorde en maakt het eenvoudiger toochange Hallo sjabloon later.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-155">This approach clarifies hello dependency order and makes it easier toochange hello template later.</span></span>
* <span data-ttu-id="2fcb5-156">Als een waarde kan worden bepaald vóór de implementatie, kunt u proberen Hallo resource zonder een afhankelijkheid implementeren.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-156">If a value can be determined before deployment, try deploying hello resource without a dependency.</span></span> <span data-ttu-id="2fcb5-157">Bijvoorbeeld, als een configuratiewaarde Hallo-naam van een andere resource moet, moet u mogelijk niet een afhankelijkheid.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-157">For example, if a configuration value needs hello name of another resource, you might not need a dependency.</span></span> <span data-ttu-id="2fcb5-158">In deze richtlijnen werkt niet altijd omdat andere resources worden gecontroleerd Hallo bestaan Hallo sommige resources.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-158">This guidance does not always work because some resources verify hello existence of hello other resource.</span></span> <span data-ttu-id="2fcb5-159">Als u een foutbericht ontvangt, voegt u een afhankelijkheid.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-159">If you receive an error, add a dependency.</span></span> 

<span data-ttu-id="2fcb5-160">Resource Manager identificeert circulaire afhankelijkheden tijdens de validatie van de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-160">Resource Manager identifies circular dependencies during template validation.</span></span> <span data-ttu-id="2fcb5-161">Als u er een foutmelding weergegeven dat er een circulaire afhankelijkheid bestaat, evalueren van uw sjabloon toosee als alle afhankelijkheden zijn niet nodig en kunnen worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-161">If you receive an error stating that a circular dependency exists, evaluate your template toosee if any dependencies are not needed and can be removed.</span></span> <span data-ttu-id="2fcb5-162">Als afhankelijkheden verwijderen niet werkt, kunt u circulaire afhankelijkheden voorkomen door bepaalde implementatiebewerkingen naar de onderliggende resources die zijn geïmplementeerd na het Hallo-resources met circulaire afhankelijkheid Hallo een te verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-162">If removing dependencies does not work, you can avoid circular dependencies by moving some deployment operations into child resources that are deployed after hello resources that have hello circular dependency.</span></span> <span data-ttu-id="2fcb5-163">Stel bijvoorbeeld dat u twee virtuele machines implementeert, maar u moet eigenschappen instellen voor elk veld dat toohello andere verwijzen.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-163">For example, suppose you are deploying two virtual machines but you must set properties on each one that refer toohello other.</span></span> <span data-ttu-id="2fcb5-164">U kunt deze implementeren in Hallo volgorde:</span><span class="sxs-lookup"><span data-stu-id="2fcb5-164">You can deploy them in hello following order:</span></span>

1. <span data-ttu-id="2fcb5-165">vm1</span><span class="sxs-lookup"><span data-stu-id="2fcb5-165">vm1</span></span>
2. <span data-ttu-id="2fcb5-166">vm2</span><span class="sxs-lookup"><span data-stu-id="2fcb5-166">vm2</span></span>
3. <span data-ttu-id="2fcb5-167">Extensie op vm1, is afhankelijk van vm1 en vm2.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-167">Extension on vm1 depends on vm1 and vm2.</span></span> <span data-ttu-id="2fcb5-168">Hallo-extensie waarden ingesteld op vm1 die van vm2 krijgt.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-168">hello extension sets values on vm1 that it gets from vm2.</span></span>
4. <span data-ttu-id="2fcb5-169">Extensie op vm2, is afhankelijk van vm1 en vm2.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-169">Extension on vm2 depends on vm1 and vm2.</span></span> <span data-ttu-id="2fcb5-170">Hallo-extensie waarden ingesteld op vm2 van van vm1 krijgt.</span><span class="sxs-lookup"><span data-stu-id="2fcb5-170">hello extension sets values on vm2 that it gets from vm1.</span></span>

<span data-ttu-id="2fcb5-171">Zie voor meer informatie over de beoordeling van de implementatievolgorde hello en het oplossen van afhankelijkheidsfouten [oplossen van veelvoorkomende fouten voor Azure-implementatie met Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="2fcb5-171">For information about assessing hello deployment order and resolving dependency errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2fcb5-172">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2fcb5-172">Next steps</span></span>
* <span data-ttu-id="2fcb5-173">Zie toolearn over het oplossen van afhankelijkheden tijdens de implementatie van [oplossen van veelvoorkomende fouten voor Azure-implementatie met Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="2fcb5-173">toolearn about troubleshooting dependencies during deployment, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="2fcb5-174">toolearn over het maken van Azure Resource Manager-sjablonen, Zie [sjablonen](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="2fcb5-174">toolearn about creating Azure Resource Manager templates, see [Authoring templates](resource-group-authoring-templates.md).</span></span> 
* <span data-ttu-id="2fcb5-175">Zie voor een lijst met de beschikbare functies in een sjabloon Hallo [sjabloonfuncties](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="2fcb5-175">For a list of hello available functions in a template, see [Template functions](resource-group-template-functions.md).</span></span>

