---
title: Implementatievolgorde voor Azure-resources instellen | Microsoft Docs
description: "Hierin wordt beschreven hoe een resource als afhankelijk is van een andere resource tijdens de implementatie om ervoor te zorgen resources in de juiste volgorde worden geïmplementeerd."
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
ms.openlocfilehash: 3d6a46116ae9d7d940bc10dfa832540f42c0af7e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="define-the-order-for-deploying-resources-in-azure-resource-manager-templates"></a><span data-ttu-id="208ab-103">De volgorde voor het implementeren van resources in Azure Resource Manager-sjablonen definiëren</span><span class="sxs-lookup"><span data-stu-id="208ab-103">Define the order for deploying resources in Azure Resource Manager templates</span></span>
<span data-ttu-id="208ab-104">Voor een bepaalde bron, kunnen er andere bronnen die u moeten bestaan voordat de resource is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="208ab-104">For a given resource, there can be other resources that must exist before the resource is deployed.</span></span> <span data-ttu-id="208ab-105">Bijvoorbeeld, moet een SQL-server bestaan voordat u probeert te implementeren van een SQL-database.</span><span class="sxs-lookup"><span data-stu-id="208ab-105">For example, a SQL server must exist before attempting to deploy a SQL database.</span></span> <span data-ttu-id="208ab-106">U definiëren deze relatie met een resource als afhankelijk van de andere bron markeren.</span><span class="sxs-lookup"><span data-stu-id="208ab-106">You define this relationship by marking one resource as dependent on the other resource.</span></span> <span data-ttu-id="208ab-107">U definieert een afhankelijkheid tussen de **dependsOn** element, of met behulp van de **verwijzing** functie.</span><span class="sxs-lookup"><span data-stu-id="208ab-107">You define a dependency with the **dependsOn** element, or by using the **reference** function.</span></span> 

<span data-ttu-id="208ab-108">Resource Manager evalueert de afhankelijkheden tussen resources en ze worden geïmplementeerd in de afhankelijke volgorde.</span><span class="sxs-lookup"><span data-stu-id="208ab-108">Resource Manager evaluates the dependencies between resources, and deploys them in their dependent order.</span></span> <span data-ttu-id="208ab-109">Wanneer u resources zijn niet afhankelijk van elkaar, worden deze door Resource Manager parallel implementeert.</span><span class="sxs-lookup"><span data-stu-id="208ab-109">When resources are not dependent on each other, Resource Manager deploys them in parallel.</span></span> <span data-ttu-id="208ab-110">U hoeft alleen te definiëren van afhankelijkheden voor resources die zijn geïmplementeerd in dezelfde sjabloon.</span><span class="sxs-lookup"><span data-stu-id="208ab-110">You only need to define dependencies for resources that are deployed in the same template.</span></span> 

## <a name="dependson"></a><span data-ttu-id="208ab-111">dependsOn</span><span class="sxs-lookup"><span data-stu-id="208ab-111">dependsOn</span></span>
<span data-ttu-id="208ab-112">Binnen uw sjabloon kunt het element dependsOn u één resource definiëren als een afhankelijk zijn van een of meer resources.</span><span class="sxs-lookup"><span data-stu-id="208ab-112">Within your template, the dependsOn element enables you to define one resource as a dependent on one or more resources.</span></span> <span data-ttu-id="208ab-113">De waarde kan een door komma's gescheiden lijst met resourcenamen zijn.</span><span class="sxs-lookup"><span data-stu-id="208ab-113">Its value can be a comma-separated list of resource names.</span></span> 

<span data-ttu-id="208ab-114">Het volgende voorbeeld ziet een virtuele-machineschaalset die afhankelijk zijn van een load balancer, het virtuele netwerk en een lus die meerdere opslagaccounts worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="208ab-114">The following example shows a virtual machine scale set that depends on a load balancer, virtual network, and a loop that creates multiple storage accounts.</span></span> <span data-ttu-id="208ab-115">Deze andere resources worden niet weergegeven in het volgende voorbeeld, maar moeten ze bestaan elders in de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="208ab-115">These other resources are not shown in the following example, but they would need to exist elsewhere in the template.</span></span>

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

<span data-ttu-id="208ab-116">In het voorgaande voorbeeld wordt een afhankelijkheid is opgenomen op de resources die zijn gemaakt via een For-lus kopiëren met de naam **storageLoop**.</span><span class="sxs-lookup"><span data-stu-id="208ab-116">In the preceding example, a dependency is included on the resources that are created through a copy loop named **storageLoop**.</span></span> <span data-ttu-id="208ab-117">Zie voor een voorbeeld [maken van meerdere exemplaren van resources in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="208ab-117">For an example, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

<span data-ttu-id="208ab-118">Bij het definiëren van afhankelijkheden, kunt u de naamruimte resourceprovider en het resourcetype om verwarring te voorkomen kunt opnemen.</span><span class="sxs-lookup"><span data-stu-id="208ab-118">When defining dependencies, you can include the resource provider namespace and resource type to avoid ambiguity.</span></span> <span data-ttu-id="208ab-119">Bijvoorbeeld, om te verduidelijken een load balancer en het virtuele netwerk met dezelfde naam als andere resources, gebruikt u de volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="208ab-119">For example, to clarify a load balancer and virtual network that may have the same names as other resources, use the following format:</span></span>

```json
"dependsOn": [
  "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
  "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
]
``` 

<span data-ttu-id="208ab-120">Terwijl u kan worden blootgesteld aan dependsOn gebruiken voor het toewijzen van relaties tussen uw resources, is het belangrijk te begrijpen waarom u dit doet.</span><span class="sxs-lookup"><span data-stu-id="208ab-120">While you may be inclined to use dependsOn to map relationships between your resources, it's important to understand why you're doing it.</span></span> <span data-ttu-id="208ab-121">Om het document hoe resources onderling verbonden, bijvoorbeeld, is het dependsOn niet de juiste aanpak.</span><span class="sxs-lookup"><span data-stu-id="208ab-121">For example, to document how resources are interconnected, dependsOn is not the right approach.</span></span> <span data-ttu-id="208ab-122">U kunt het welke resources zijn gedefinieerd in het element dependsOn na de implementatie kan geen query uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="208ab-122">You cannot query which resources were defined in the dependsOn element after deployment.</span></span> <span data-ttu-id="208ab-123">Met behulp van dependsOn u mogelijk gevolgen hebben voor implementatietijd omdat Resource Manager niet is geïmplementeerd in parallelle twee resources met een afhankelijkheid.</span><span class="sxs-lookup"><span data-stu-id="208ab-123">By using dependsOn, you potentially impact deployment time because Resource Manager does not deploy in parallel two resources that have a dependency.</span></span> <span data-ttu-id="208ab-124">In plaats daarvan gebruik om relaties tussen resources document [resources](/rest/api/resources/resourcelinks).</span><span class="sxs-lookup"><span data-stu-id="208ab-124">To document relationships between resources, instead use [resource linking](/rest/api/resources/resourcelinks).</span></span>

## <a name="child-resources"></a><span data-ttu-id="208ab-125">Onderliggende resources</span><span class="sxs-lookup"><span data-stu-id="208ab-125">Child resources</span></span>
<span data-ttu-id="208ab-126">De eigenschap resources kunt u opgeven van de onderliggende resources die zijn gerelateerd aan de bron wordt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="208ab-126">The resources property allows you to specify child resources that are related to the resource being defined.</span></span> <span data-ttu-id="208ab-127">Onderliggende resources kunnen alleen worden gedefinieerd vijf niveaus.</span><span class="sxs-lookup"><span data-stu-id="208ab-127">Child resources can only be defined five levels deep.</span></span> <span data-ttu-id="208ab-128">Het is belangrijk te weten dat een impliciete afhankelijkheid niet tussen een bron van de onderliggende en de bovenliggende resource is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="208ab-128">It is important to note that an implicit dependency is not created between a child resource and the parent resource.</span></span> <span data-ttu-id="208ab-129">Als u de onderliggende resource te worden geïmplementeerd nadat de bovenliggende resource nodig hebt, moet u deze afhankelijkheid met de eigenschap dependsOn expliciet vermelden.</span><span class="sxs-lookup"><span data-stu-id="208ab-129">If you need the child resource to be deployed after the parent resource, you must explicitly state that dependency with the dependsOn property.</span></span> 

<span data-ttu-id="208ab-130">Elke bovenliggende resource accepteert alleen bepaalde resourcetypen als onderliggende resources.</span><span class="sxs-lookup"><span data-stu-id="208ab-130">Each parent resource accepts only certain resource types as child resources.</span></span> <span data-ttu-id="208ab-131">De geaccepteerde brontypen zijn opgegeven in de [sjabloonschema](https://github.com/Azure/azure-resource-manager-schemas) van de bovenliggende resource.</span><span class="sxs-lookup"><span data-stu-id="208ab-131">The accepted resource types are specified in the [template schema](https://github.com/Azure/azure-resource-manager-schemas) of the parent resource.</span></span> <span data-ttu-id="208ab-132">Bevat de naam van het type van de bovenliggende resource, zoals de naam van de onderliggende brontype **Microsoft.Web/sites/config** en **Microsoft.Web/sites/extensions** zijn beide onderliggende resources van de **Microsoft.Web/sites**.</span><span class="sxs-lookup"><span data-stu-id="208ab-132">The name of child resource type includes the name of the parent resource type, such as **Microsoft.Web/sites/config** and **Microsoft.Web/sites/extensions** are both child resources of the **Microsoft.Web/sites**.</span></span>

<span data-ttu-id="208ab-133">Het volgende voorbeeld ziet een SQL server en SQL-database.</span><span class="sxs-lookup"><span data-stu-id="208ab-133">The following example shows a SQL server and SQL database.</span></span> <span data-ttu-id="208ab-134">U ziet dat er een expliciete afhankelijkheid is gedefinieerd tussen de SQL-database en SQL server, ondanks dat de database een onderliggend element van de server is.</span><span class="sxs-lookup"><span data-stu-id="208ab-134">Notice that an explicit dependency is defined between the SQL database and SQL server, even though the database is a child of the server.</span></span>

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

## <a name="reference-function"></a><span data-ttu-id="208ab-135">verwijzing naar functie</span><span class="sxs-lookup"><span data-stu-id="208ab-135">reference function</span></span>
<span data-ttu-id="208ab-136">De [verwijst naar functie](resource-group-template-functions-resource.md#reference) kunt u een expressie die moet worden afgeleid van de waarde van andere JSON naam / waarde-paren of runtime-bronnen.</span><span class="sxs-lookup"><span data-stu-id="208ab-136">The [reference function](resource-group-template-functions-resource.md#reference) enables an expression to derive its value from other JSON name and value pairs or runtime resources.</span></span> <span data-ttu-id="208ab-137">Verwijzingsexpressies declareren impliciet dat één resource afhankelijk van een andere is.</span><span class="sxs-lookup"><span data-stu-id="208ab-137">Reference expressions implicitly declare that one resource depends on another.</span></span> <span data-ttu-id="208ab-138">De algemene indeling is:</span><span class="sxs-lookup"><span data-stu-id="208ab-138">The general format is:</span></span>

```json
reference('resourceName').propertyPath
```

<span data-ttu-id="208ab-139">In het volgende voorbeeld wordt een CDN-eindpunt expliciet is afhankelijk van het CDN-profiel en impliciet afhankelijk is van een web-app.</span><span class="sxs-lookup"><span data-stu-id="208ab-139">In the following example, a CDN endpoint explicitly depends on the CDN profile, and implicitly depends on a web app.</span></span>

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

<span data-ttu-id="208ab-140">U kunt dit element of het element dependsOn gebruiken om op te geven, afhankelijkheden, maar u hoeft niet te gebruiken voor dezelfde afhankelijke resource.</span><span class="sxs-lookup"><span data-stu-id="208ab-140">You can use either this element or the dependsOn element to specify dependencies, but you do not need to use both for the same dependent resource.</span></span> <span data-ttu-id="208ab-141">Gebruik indien mogelijk een impliciete verwijzing om te voorkomen dat een onnodige afhankelijkheid toevoegen.</span><span class="sxs-lookup"><span data-stu-id="208ab-141">Whenever possible, use an implicit reference to avoid adding an unnecessary dependency.</span></span>

<span data-ttu-id="208ab-142">Zie voor meer informatie, [verwijst naar functie](resource-group-template-functions-resource.md#reference).</span><span class="sxs-lookup"><span data-stu-id="208ab-142">To learn more, see [reference function](resource-group-template-functions-resource.md#reference).</span></span>

## <a name="recommendations-for-setting-dependencies"></a><span data-ttu-id="208ab-143">Aanbevelingen voor het instellen van de afhankelijkheden</span><span class="sxs-lookup"><span data-stu-id="208ab-143">Recommendations for setting dependencies</span></span>

<span data-ttu-id="208ab-144">Wanneer u beslist welke afhankelijkheden in te stellen, gebruikt u de volgende richtlijnen:</span><span class="sxs-lookup"><span data-stu-id="208ab-144">When deciding what dependencies to set, use the following guidelines:</span></span>

* <span data-ttu-id="208ab-145">Afhankelijkheden van zo weinig mogelijk ingesteld.</span><span class="sxs-lookup"><span data-stu-id="208ab-145">Set as few dependencies as possible.</span></span>
* <span data-ttu-id="208ab-146">Stel een onderliggende resource als afhankelijk van de bovenliggende resource.</span><span class="sxs-lookup"><span data-stu-id="208ab-146">Set a child resource as dependent on its parent resource.</span></span>
* <span data-ttu-id="208ab-147">Gebruik de **verwijzing** functie impliciete afhankelijkheden tussen resources die nodig zijn voor het delen van een eigenschap instellen.</span><span class="sxs-lookup"><span data-stu-id="208ab-147">Use the **reference** function to set implicit dependencies between resources that need to share a property.</span></span> <span data-ttu-id="208ab-148">Voeg een expliciete afhankelijkheid niet (**dependsOn**) wanneer u een impliciete afhankelijkheid al hebt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="208ab-148">Do not add an explicit dependency (**dependsOn**) when you have already defined an implicit dependency.</span></span> <span data-ttu-id="208ab-149">Deze aanpak vermindert het risico van conflicterende onnodige afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="208ab-149">This approach reduces the risk of having unnecessary dependencies.</span></span> 
* <span data-ttu-id="208ab-150">Een afhankelijkheid ingesteld wanneer een resource kan niet worden **gemaakt** zonder de functionaliteit van een andere resource.</span><span class="sxs-lookup"><span data-stu-id="208ab-150">Set a dependency when a resource cannot be **created** without functionality from another resource.</span></span> <span data-ttu-id="208ab-151">Stel een afhankelijkheid niet als de bronnen alleen na de implementatie werken.</span><span class="sxs-lookup"><span data-stu-id="208ab-151">Do not set a dependency if the resources only interact after deployment.</span></span>
* <span data-ttu-id="208ab-152">Laat afhankelijkheden cascade zonder expliciet instelt.</span><span class="sxs-lookup"><span data-stu-id="208ab-152">Let dependencies cascade without setting them explicitly.</span></span> <span data-ttu-id="208ab-153">Bijvoorbeeld, de virtuele machine is afhankelijk van de virtuele netwerkinterface en de virtuele netwerkinterface is afhankelijk van een virtueel netwerk en openbare IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="208ab-153">For example, your virtual machine depends on a virtual network interface, and the virtual network interface depends on a virtual network and public IP addresses.</span></span> <span data-ttu-id="208ab-154">Daarom wordt de virtuele machine is geïmplementeerd nadat alle drie resources, maar de virtuele machine niet expliciet als afhankelijk is van alle drie resources instelt.</span><span class="sxs-lookup"><span data-stu-id="208ab-154">Therefore, the virtual machine is deployed after all three resources, but do not explicitly set the virtual machine as dependent on all three resources.</span></span> <span data-ttu-id="208ab-155">Deze aanpak wordt uitleg gegeven over de volgorde van afhankelijkheid en kunt u gemakkelijker de sjabloon later wijzigen.</span><span class="sxs-lookup"><span data-stu-id="208ab-155">This approach clarifies the dependency order and makes it easier to change the template later.</span></span>
* <span data-ttu-id="208ab-156">Als een waarde kan worden bepaald vóór de implementatie, probeert u de implementatie van de bron zonder een afhankelijkheid.</span><span class="sxs-lookup"><span data-stu-id="208ab-156">If a value can be determined before deployment, try deploying the resource without a dependency.</span></span> <span data-ttu-id="208ab-157">Bijvoorbeeld, als een configuratiewaarde de naam van een andere resource moet, moet u mogelijk niet een afhankelijkheid.</span><span class="sxs-lookup"><span data-stu-id="208ab-157">For example, if a configuration value needs the name of another resource, you might not need a dependency.</span></span> <span data-ttu-id="208ab-158">In deze richtlijnen werkt niet altijd omdat sommige resources verifieert of de andere resource.</span><span class="sxs-lookup"><span data-stu-id="208ab-158">This guidance does not always work because some resources verify the existence of the other resource.</span></span> <span data-ttu-id="208ab-159">Als u een foutbericht ontvangt, voegt u een afhankelijkheid.</span><span class="sxs-lookup"><span data-stu-id="208ab-159">If you receive an error, add a dependency.</span></span> 

<span data-ttu-id="208ab-160">Resource Manager identificeert circulaire afhankelijkheden tijdens de validatie van de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="208ab-160">Resource Manager identifies circular dependencies during template validation.</span></span> <span data-ttu-id="208ab-161">Als u er een foutmelding weergegeven dat er een circulaire afhankelijkheid bestaat, evalueren de sjabloon of alle afhankelijkheden zijn niet nodig en kunnen worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="208ab-161">If you receive an error stating that a circular dependency exists, evaluate your template to see if any dependencies are not needed and can be removed.</span></span> <span data-ttu-id="208ab-162">Als het verwijderen van afhankelijkheden niet werkt, kunt u circulaire afhankelijkheden voorkomen door het verplaatsen van bepaalde implementatiebewerkingen naar onderliggende resources die zijn geïmplementeerd nadat de resources met circulaire afhankelijkheid een.</span><span class="sxs-lookup"><span data-stu-id="208ab-162">If removing dependencies does not work, you can avoid circular dependencies by moving some deployment operations into child resources that are deployed after the resources that have the circular dependency.</span></span> <span data-ttu-id="208ab-163">Stel bijvoorbeeld dat u twee virtuele machines implementeert, maar u moet eigenschappen instellen voor elk criterium die verwijzen naar de andere.</span><span class="sxs-lookup"><span data-stu-id="208ab-163">For example, suppose you are deploying two virtual machines but you must set properties on each one that refer to the other.</span></span> <span data-ttu-id="208ab-164">U kunt deze implementeren in de volgende volgorde:</span><span class="sxs-lookup"><span data-stu-id="208ab-164">You can deploy them in the following order:</span></span>

1. <span data-ttu-id="208ab-165">vm1</span><span class="sxs-lookup"><span data-stu-id="208ab-165">vm1</span></span>
2. <span data-ttu-id="208ab-166">vm2</span><span class="sxs-lookup"><span data-stu-id="208ab-166">vm2</span></span>
3. <span data-ttu-id="208ab-167">Extensie op vm1, is afhankelijk van vm1 en vm2.</span><span class="sxs-lookup"><span data-stu-id="208ab-167">Extension on vm1 depends on vm1 and vm2.</span></span> <span data-ttu-id="208ab-168">De extensie waarden ingesteld op vm1 die van vm2 krijgt.</span><span class="sxs-lookup"><span data-stu-id="208ab-168">The extension sets values on vm1 that it gets from vm2.</span></span>
4. <span data-ttu-id="208ab-169">Extensie op vm2, is afhankelijk van vm1 en vm2.</span><span class="sxs-lookup"><span data-stu-id="208ab-169">Extension on vm2 depends on vm1 and vm2.</span></span> <span data-ttu-id="208ab-170">De extensie waarden ingesteld op vm2 van van vm1 krijgt.</span><span class="sxs-lookup"><span data-stu-id="208ab-170">The extension sets values on vm2 that it gets from vm1.</span></span>

<span data-ttu-id="208ab-171">Zie voor meer informatie over de beoordeling van de implementatievolgorde en het oplossen van afhankelijkheidsfouten [oplossen van veelvoorkomende fouten voor Azure-implementatie met Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="208ab-171">For information about assessing the deployment order and resolving dependency errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="208ab-172">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="208ab-172">Next steps</span></span>
* <span data-ttu-id="208ab-173">Zie voor meer informatie over het oplossen van afhankelijkheden tijdens de implementatie, [oplossen van veelvoorkomende fouten voor Azure-implementatie met Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="208ab-173">To learn about troubleshooting dependencies during deployment, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="208ab-174">Zie voor meer informatie over het maken van Azure Resource Manager-sjablonen, [sjablonen](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="208ab-174">To learn about creating Azure Resource Manager templates, see [Authoring templates](resource-group-authoring-templates.md).</span></span> 
* <span data-ttu-id="208ab-175">Zie voor een lijst van de beschikbare functies in een sjabloon, [sjabloonfuncties](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="208ab-175">For a list of the available functions in a template, see [Template functions](resource-group-template-functions.md).</span></span>

