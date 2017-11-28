---
title: aaaLearn over virtuele-machineschaalset sjablonen instellen | Microsoft Docs
description: Meer informatie over een minimale levensvatbaar schaal toocreate ingesteld sjabloon voor virtuele-machineschaalsets
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: negat
ms.openlocfilehash: b7a1cf6c03b22585e16db9c071d45795c8ae75df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-virtual-machine-scale-set-templates"></a><span data-ttu-id="415b2-103">Meer informatie over de sjablonen voor virtuele machines scale set</span><span class="sxs-lookup"><span data-stu-id="415b2-103">Learn about virtual machine scale set templates</span></span>
<span data-ttu-id="415b2-104">[Azure Resource Manager-sjablonen](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) zijn een goede manier toodeploy groepen verwante resources.</span><span class="sxs-lookup"><span data-stu-id="415b2-104">[Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) are a great way toodeploy groups of related resources.</span></span> <span data-ttu-id="415b2-105">Deze zelfstudie reeks ziet u hoe u een minimale levensvatbaar schaal toocreate sjabloon ingesteld en hoe toomodify deze sjabloon toosuit verschillende scenario's.</span><span class="sxs-lookup"><span data-stu-id="415b2-105">This tutorial series shows how toocreate a minimum viable scale set template and how toomodify this template toosuit various scenarios.</span></span> <span data-ttu-id="415b2-106">Alle voorbeelden afkomstig zijn van dit [GitHub-opslagplaats](https://github.com/gatneil/mvss).</span><span class="sxs-lookup"><span data-stu-id="415b2-106">All examples come from this [GitHub repository](https://github.com/gatneil/mvss).</span></span> 

<span data-ttu-id="415b2-107">Deze sjabloon is bedoeld toobe eenvoudig.</span><span class="sxs-lookup"><span data-stu-id="415b2-107">This template is intended toobe simple.</span></span> <span data-ttu-id="415b2-108">Voor gedetailleerde voorbeelden van de schaal sjablonen, raadpleegt u Hallo [Azure Quick Start-sjablonen GitHub-opslagplaats](https://github.com/Azure/azure-quickstart-templates) en zoek naar de mappen met Hallo tekenreeks `vmss`.</span><span class="sxs-lookup"><span data-stu-id="415b2-108">For more complete examples of scale set templates, see hello [Azure Quickstart Templates GitHub repository](https://github.com/Azure/azure-quickstart-templates) and search for folders that contain hello string `vmss`.</span></span>

<span data-ttu-id="415b2-109">Als u al bekend bent met sjablonen maken, kunt u hoe toohello 'Volgende stappen' sectie toosee overslaan toomodify deze sjabloon.</span><span class="sxs-lookup"><span data-stu-id="415b2-109">If you are already familiar with creating templates, you can skip toohello "Next steps" section toosee how toomodify this template.</span></span>

## <a name="review-hello-template"></a><span data-ttu-id="415b2-110">Hallo-template bekijken</span><span class="sxs-lookup"><span data-stu-id="415b2-110">Review hello template</span></span>

<span data-ttu-id="415b2-111">Gebruik van GitHub tooreview onze minimale levensvatbaar schaalset sjabloon [azuredeploy.json](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="415b2-111">Use GitHub tooreview our minimum viable scale set template, [azuredeploy.json](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json).</span></span>

<span data-ttu-id="415b2-112">In deze zelfstudie we naar de Hallo diff (`git diff master minimum-viable-scale-set`) toocreate Hallo minimale levensvatbaar schaalset sjabloon stuk door stuk.</span><span class="sxs-lookup"><span data-stu-id="415b2-112">In this tutorial, we examine hello diff (`git diff master minimum-viable-scale-set`) toocreate hello minimum viable scale set template piece by piece.</span></span>

## <a name="define-schema-and-contentversion"></a><span data-ttu-id="415b2-113">$Schema en contentVersion definiëren</span><span class="sxs-lookup"><span data-stu-id="415b2-113">Define $schema and contentVersion</span></span>
<span data-ttu-id="415b2-114">Eerst definiëren we `$schema` en `contentVersion` in Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="415b2-114">First, we define `$schema` and `contentVersion` in hello template.</span></span> <span data-ttu-id="415b2-115">Hallo `$schema` element Hallo-versie van de sjabloontaal Hallo definieert en wordt gebruikt voor syntaxismarkering Visual Studio en vergelijkbare functies voor validatie.</span><span class="sxs-lookup"><span data-stu-id="415b2-115">hello `$schema` element defines hello version of hello template language and is used for Visual Studio syntax highlighting and similar validation features.</span></span> <span data-ttu-id="415b2-116">Hallo `contentVersion` element wordt niet gebruikt door Azure.</span><span class="sxs-lookup"><span data-stu-id="415b2-116">hello `contentVersion` element is not used by Azure.</span></span> <span data-ttu-id="415b2-117">In plaats daarvan kunt u Hallo sjabloonversie.</span><span class="sxs-lookup"><span data-stu-id="415b2-117">Instead, it helps you keep track of hello template version.</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json",
  "contentVersion": "1.0.0.0",
```
## <a name="define-parameters"></a><span data-ttu-id="415b2-118">parameters definiëren</span><span class="sxs-lookup"><span data-stu-id="415b2-118">Define parameters</span></span>
<span data-ttu-id="415b2-119">Vervolgens geeft u twee parameters `adminUsername` en `adminPassword`.</span><span class="sxs-lookup"><span data-stu-id="415b2-119">Next, we define two parameters, `adminUsername` and `adminPassword`.</span></span> <span data-ttu-id="415b2-120">Parameters zijn waarden die u op Hallo moment van implementatie opgeeft.</span><span class="sxs-lookup"><span data-stu-id="415b2-120">Parameters are values you specify at hello time of deployment.</span></span> <span data-ttu-id="415b2-121">Hallo `adminUsername` parameter is gewoon een `string` type, maar omdat `adminPassword` geheim, geven wij type `securestring`.</span><span class="sxs-lookup"><span data-stu-id="415b2-121">hello `adminUsername` parameter is simply a `string` type, but because `adminPassword` is a secret, we give it type `securestring`.</span></span> <span data-ttu-id="415b2-122">Later, worden deze parameters doorgegeven in Hallo scale set configuratie.</span><span class="sxs-lookup"><span data-stu-id="415b2-122">Later, these parameters are passed into hello scale set configuration.</span></span>

```json
  "parameters": {
    "adminUsername": {
      "type": "string"
    },
    "adminPassword": {
      "type": "securestring"
    }
  },
```
## <a name="define-variables"></a><span data-ttu-id="415b2-123">Variabelen definiëren</span><span class="sxs-lookup"><span data-stu-id="415b2-123">Define variables</span></span>
<span data-ttu-id="415b2-124">Resource Manager-sjablonen kunnen u variabelen toobe verderop in de sjabloon Hallo gebruikt definiëren.</span><span class="sxs-lookup"><span data-stu-id="415b2-124">Resource Manager templates also let you define variables toobe used later in hello template.</span></span> <span data-ttu-id="415b2-125">Het voorbeeld gebruikt niet alle variabelen zodat we hebt leeg wordt gelaten Hallo JSON-object.</span><span class="sxs-lookup"><span data-stu-id="415b2-125">Our example doesn't use any variables, so we've left hello JSON object empty.</span></span>

```json
  "variables": {},
```

## <a name="define-resources"></a><span data-ttu-id="415b2-126">Resources definiëren</span><span class="sxs-lookup"><span data-stu-id="415b2-126">Define resources</span></span>
<span data-ttu-id="415b2-127">Naast is Hallo bronnensectie van Hallo sjabloon.</span><span class="sxs-lookup"><span data-stu-id="415b2-127">Next is hello resources section of hello template.</span></span> <span data-ttu-id="415b2-128">Hier kunt u definiëren wat daadwerkelijk toodeploy.</span><span class="sxs-lookup"><span data-stu-id="415b2-128">Here, you define what you actually want toodeploy.</span></span> <span data-ttu-id="415b2-129">In tegenstelling tot `parameters` en `variables` (die zijn JSON-objecten), `resources` is een JSON-lijst van JSON-objecten.</span><span class="sxs-lookup"><span data-stu-id="415b2-129">Unlike `parameters` and `variables` (which are JSON objects), `resources` is a JSON list of JSON objects.</span></span>

```json
   "resources": [
```

<span data-ttu-id="415b2-130">Alle resources vereisen `type`, `name`, `apiVersion`, en `location` eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="415b2-130">All resources require `type`, `name`, `apiVersion`, and `location` properties.</span></span> <span data-ttu-id="415b2-131">De eerste resource in dit voorbeeld heeft een type `Microsft.Network/virtualNetwork`, naam `myVnet`, en apiVersion `2016-03-30`.</span><span class="sxs-lookup"><span data-stu-id="415b2-131">This example's first resource has type `Microsft.Network/virtualNetwork`, name `myVnet`, and apiVersion `2016-03-30`.</span></span> <span data-ttu-id="415b2-132">(toofind Hallo nieuwste API-versie voor een brontype Zie Hallo [Azure REST API-documentatie](https://docs.microsoft.com/rest/api/).)</span><span class="sxs-lookup"><span data-stu-id="415b2-132">(toofind hello latest API version for a resource type, see hello [Azure REST API documentation](https://docs.microsoft.com/rest/api/).)</span></span>

```json
     {
       "type": "Microsoft.Network/virtualNetworks",
       "name": "myVnet",
       "apiVersion": "2016-12-01",
```

## <a name="specify-location"></a><span data-ttu-id="415b2-133">Geef de locatie</span><span class="sxs-lookup"><span data-stu-id="415b2-133">Specify location</span></span>
<span data-ttu-id="415b2-134">toospecify hello locatie voor het virtuele netwerk hello, gebruiken we een [Resource Manager sjabloonfunctie](../azure-resource-manager/resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="415b2-134">toospecify hello location for hello virtual network, we use a [Resource Manager template function](../azure-resource-manager/resource-group-template-functions.md).</span></span> <span data-ttu-id="415b2-135">Deze functie moet tussen aanhalingstekens en vierkante haken als volgt: `"[<template-function>]"`.</span><span class="sxs-lookup"><span data-stu-id="415b2-135">This function must be enclosed in quotes and square brackets like this: `"[<template-function>]"`.</span></span> <span data-ttu-id="415b2-136">In dit geval gebruiken we Hallo `resourceGroup` functie.</span><span class="sxs-lookup"><span data-stu-id="415b2-136">In this case, we use hello `resourceGroup` function.</span></span> <span data-ttu-id="415b2-137">Dit heeft geen argumenten en retourneert een JSON-object met metagegevens over Hallo resourcegroep die deze implementatie wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="415b2-137">It takes in no arguments and returns a JSON object with metadata about hello resource group this deployment is being deployed to.</span></span> <span data-ttu-id="415b2-138">Hallo-resourcegroep is ingesteld door de gebruiker Hallo op Hallo moment van implementatie.</span><span class="sxs-lookup"><span data-stu-id="415b2-138">hello resource group is set by hello user at hello time of deployment.</span></span> <span data-ttu-id="415b2-139">We vervolgens index in dit JSON-object met `.location` tooget Hallo locatie Hallo JSON-object.</span><span class="sxs-lookup"><span data-stu-id="415b2-139">We then index into this JSON object with `.location` tooget hello location from hello JSON object.</span></span>

```json
       "location": "[resourceGroup().location]",
```

## <a name="specify-virtual-network-properties"></a><span data-ttu-id="415b2-140">Eigenschappen van virtueel netwerk opgeven</span><span class="sxs-lookup"><span data-stu-id="415b2-140">Specify virtual network properties</span></span>
<span data-ttu-id="415b2-141">Elke Resource Manager-bron heeft zijn eigen `properties` sectie voor configuraties specifieke toohello resource.</span><span class="sxs-lookup"><span data-stu-id="415b2-141">Each Resource Manager resource has its own `properties` section for configurations specific toohello resource.</span></span> <span data-ttu-id="415b2-142">In dit geval we dit virtuele netwerk Hallo moet één subnet met Hallo persoonlijk IP-adresbereik opgeven `10.0.0.0/16`.</span><span class="sxs-lookup"><span data-stu-id="415b2-142">In this case, we specify that hello virtual network should have one subnet using hello private IP address range `10.0.0.0/16`.</span></span> <span data-ttu-id="415b2-143">Een schaalset zich altijd in één subnet.</span><span class="sxs-lookup"><span data-stu-id="415b2-143">A scale set is always contained within one subnet.</span></span> <span data-ttu-id="415b2-144">Dit kan geen subnetten omvatten.</span><span class="sxs-lookup"><span data-stu-id="415b2-144">It cannot span subnets.</span></span>

```json
       "properties": {
         "addressSpace": {
           "addressPrefixes": [
             "10.0.0.0/16"
           ]
         },
         "subnets": [
           {
             "name": "mySubnet",
             "properties": {
               "addressPrefix": "10.0.0.0/16"
             }
           }
         ]
       }
     },
```

## <a name="add-dependson-list"></a><span data-ttu-id="415b2-145">DependsOn lijst toevoegen</span><span class="sxs-lookup"><span data-stu-id="415b2-145">Add dependsOn list</span></span>
<span data-ttu-id="415b2-146">Bovendien toohello vereist `type`, `name`, `apiVersion`, en `location` eigenschappen van elke bron kunnen een optionele hebben `dependsOn` lijst met tekenreeksen.</span><span class="sxs-lookup"><span data-stu-id="415b2-146">In addition toohello required `type`, `name`, `apiVersion`, and `location` properties, each resource can have an optional `dependsOn` list of strings.</span></span> <span data-ttu-id="415b2-147">Deze lijst aangeeft welke andere bronnen van deze implementatie moeten worden voltooid voordat de implementatie van deze resource.</span><span class="sxs-lookup"><span data-stu-id="415b2-147">This list specifies which other resources from this deployment must finish before deploying this resource.</span></span>

<span data-ttu-id="415b2-148">In dit geval is slechts één element in virtueel netwerk van het vorige voorbeeld Hallo HALLO hallo lijst.</span><span class="sxs-lookup"><span data-stu-id="415b2-148">In this case, there is only one element in hello list, hello virtual network from hello previous example.</span></span> <span data-ttu-id="415b2-149">We opgeven deze afhankelijkheid omdat Hallo behoeften Hallo netwerk tooexist schaalset voordat u alle virtuele machines maakt.</span><span class="sxs-lookup"><span data-stu-id="415b2-149">We specify this dependency because hello scale set needs hello network tooexist before creating any VMs.</span></span> <span data-ttu-id="415b2-150">Op deze manier Hallo scale set kan deze persoonlijke IP-adressen voor virtuele machines uit Hallo IP-adresbereik eerder opgegeven in hello netwerkgegevens geven.</span><span class="sxs-lookup"><span data-stu-id="415b2-150">This way, hello scale set can give these VMs private IP addresses from hello IP address range previously specified in hello network properties.</span></span> <span data-ttu-id="415b2-151">Hallo-indeling van elke tekenreeks in Hallo dependsOn lijst is `<type>/<name>`.</span><span class="sxs-lookup"><span data-stu-id="415b2-151">hello format of each string in hello dependsOn list is `<type>/<name>`.</span></span> <span data-ttu-id="415b2-152">Gebruik dezelfde Hallo `type` en `name` eerder gebruikt in de resourcedefinitie voor Hallo virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="415b2-152">Use hello same `type` and `name` used previously in hello virtual network resource definition.</span></span>

```json
     {
       "type": "Microsoft.Compute/virtualMachineScaleSets",
       "name": "myScaleSet",
       "apiVersion": "2016-04-30-preview",
       "location": "[resourceGroup().location]",
       "dependsOn": [
         "Microsoft.Network/virtualNetworks/myVnet"
       ],
```
## <a name="specify-scale-set-properties"></a><span data-ttu-id="415b2-153">Scale seteigenschappen opgeven</span><span class="sxs-lookup"><span data-stu-id="415b2-153">Specify scale set properties</span></span>
<span data-ttu-id="415b2-154">-Schaalsets hebben veel eigenschappen voor het Hallo-virtuele machines in de schaalset Hallo aanpassen.</span><span class="sxs-lookup"><span data-stu-id="415b2-154">Scale sets have many properties for customizing hello VMs in hello scale set.</span></span> <span data-ttu-id="415b2-155">Zie voor een volledige lijst van deze eigenschappen Hallo [REST API-documentatie-schaalset](https://docs.microsoft.com/en-us/rest/api/virtualmachinescalesets/create-or-update-a-set).</span><span class="sxs-lookup"><span data-stu-id="415b2-155">For a full list of these properties, see hello [scale set REST API documentation](https://docs.microsoft.com/en-us/rest/api/virtualmachinescalesets/create-or-update-a-set).</span></span> <span data-ttu-id="415b2-156">Er wordt slechts enkele veelgebruikte eigenschappen ingesteld voor deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="415b2-156">For this tutorial, we will set only a few commonly used properties.</span></span>
### <a name="supply-vm-size-and-capacity"></a><span data-ttu-id="415b2-157">VM-grootte en capaciteit op te geven</span><span class="sxs-lookup"><span data-stu-id="415b2-157">Supply VM size and capacity</span></span>
<span data-ttu-id="415b2-158">Hallo-schaalset behoeften tooknow welke grootte van de VM toocreate ('sku-naam') en hoeveel dergelijke virtuele machines toocreate ('sku-capaciteit').</span><span class="sxs-lookup"><span data-stu-id="415b2-158">hello scale set needs tooknow what size of VM toocreate ("sku name") and how many such VMs toocreate ("sku capacity").</span></span> <span data-ttu-id="415b2-159">toosee welke VM-grootten beschikbaar zijn, Zie Hallo [VM-grootten documentatie](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes).</span><span class="sxs-lookup"><span data-stu-id="415b2-159">toosee which VM sizes are available, see hello [VM Sizes documentation](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes).</span></span>

```json
       "sku": {
         "name": "Standard_A1",
         "capacity": 2
       },
```

### <a name="choose-type-of-updates"></a><span data-ttu-id="415b2-160">Type van de updates kiezen</span><span class="sxs-lookup"><span data-stu-id="415b2-160">Choose type of updates</span></span>
<span data-ttu-id="415b2-161">Hallo scale set moet ook tooknow hoe toohandle updates op Hallo schaalset.</span><span class="sxs-lookup"><span data-stu-id="415b2-161">hello scale set also needs tooknow how toohandle updates on hello scale set.</span></span> <span data-ttu-id="415b2-162">Er zijn momenteel twee opties `Manual` en `Automatic`.</span><span class="sxs-lookup"><span data-stu-id="415b2-162">Currently, there are two options, `Manual` and `Automatic`.</span></span> <span data-ttu-id="415b2-163">Zie voor meer informatie over de verschillen tussen twee Hallo HALLO hallo-documentatie op [hoe tooupgrade een schaalset](./virtual-machine-scale-sets-upgrade-scale-set.md).</span><span class="sxs-lookup"><span data-stu-id="415b2-163">For more information on hello differences between hello two, see hello documentation on [how tooupgrade a scale set](./virtual-machine-scale-sets-upgrade-scale-set.md).</span></span>

```json
       "properties": {
         "upgradePolicy": {
           "mode": "Manual"
         },
```

### <a name="choose-vm-operating-system"></a><span data-ttu-id="415b2-164">Kies VM-besturingssysteem</span><span class="sxs-lookup"><span data-stu-id="415b2-164">Choose VM operating system</span></span>
<span data-ttu-id="415b2-165">Hallo-schaalset behoeften tooknow welke tooput besturingssysteem op Hallo virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="415b2-165">hello scale set needs tooknow what operating system tooput on hello VMs.</span></span> <span data-ttu-id="415b2-166">Hier maken we Hallo virtuele machines met een volledig patches Ubuntu 16.04 TNS-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="415b2-166">Here, we create hello VMs with a fully patched Ubuntu 16.04-LTS image.</span></span>

```json
         "virtualMachineProfile": {
           "storageProfile": {
             "imageReference": {
               "publisher": "Canonical",
               "offer": "UbuntuServer",
               "sku": "16.04-LTS",
               "version": "latest"
             }
           },
```

### <a name="specify-computernameprefix"></a><span data-ttu-id="415b2-167">Geef de waarde voor computerNamePrefix</span><span class="sxs-lookup"><span data-stu-id="415b2-167">Specify computerNamePrefix</span></span>
<span data-ttu-id="415b2-168">Hallo-schaalset implementeert meerdere virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="415b2-168">hello scale set deploys multiple VMs.</span></span> <span data-ttu-id="415b2-169">In plaats van elke VM-naam geven, geven we `computerNamePrefix`.</span><span class="sxs-lookup"><span data-stu-id="415b2-169">Instead of specifying each VM name, we specify `computerNamePrefix`.</span></span> <span data-ttu-id="415b2-170">Hallo schaalset voegt het voorvoegsel van een index toohello voor elke VM zodat VM-namen Hallo vorm hebben `<computerNamePrefix>_<auto-generated-index>`.</span><span class="sxs-lookup"><span data-stu-id="415b2-170">hello scale set appends an index toohello prefix for each VM, so VM names have hello form `<computerNamePrefix>_<auto-generated-index>`.</span></span>

<span data-ttu-id="415b2-171">In Hallo codefragment te volgen, gebruiken we Hallo parameters uit voordat tooset Hallo beheerder gebruikersnaam en wachtwoord voor alle virtuele machines in de schaalset Hallo.</span><span class="sxs-lookup"><span data-stu-id="415b2-171">In hello following snippet, we use hello parameters from before tooset hello administrator username and password for all VMs in hello scale set.</span></span> <span data-ttu-id="415b2-172">We doen dit met Hallo `parameters` sjabloonfunctie.</span><span class="sxs-lookup"><span data-stu-id="415b2-172">We do this with hello `parameters` template function.</span></span> <span data-ttu-id="415b2-173">Deze functie omvat een tekenreeks die opgeeft welke parameter toorefer tooand levert Hallo-waarde voor deze parameter.</span><span class="sxs-lookup"><span data-stu-id="415b2-173">This function takes in a string that specifies which parameter toorefer tooand outputs hello value for that parameter.</span></span>

```json
           "osProfile": {
             "computerNamePrefix": "vm",
             "adminUsername": "[parameters('adminUsername')]",
             "adminPassword": "[parameters('adminPassword')]"
           },
```

### <a name="specify-vm-network-configuration"></a><span data-ttu-id="415b2-174">VM-netwerkconfiguratie opgeven</span><span class="sxs-lookup"><span data-stu-id="415b2-174">Specify VM network configuration</span></span>
<span data-ttu-id="415b2-175">Tot slot moeten we toospecify Hallo netwerkconfiguratie voor Hallo virtuele machines in de schaalset Hallo.</span><span class="sxs-lookup"><span data-stu-id="415b2-175">Finally, we need toospecify hello network configuration for hello VMs in hello scale set.</span></span> <span data-ttu-id="415b2-176">In dit geval hoeft er alleen toospecify Hallo-ID van Hallo subnet eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="415b2-176">In this case, we only need toospecify hello ID of hello subnet created earlier.</span></span> <span data-ttu-id="415b2-177">Dit vertelt Hallo schaalset tooput Hallo netwerkinterfaces in dit subnet.</span><span class="sxs-lookup"><span data-stu-id="415b2-177">This tells hello scale set tooput hello network interfaces in this subnet.</span></span>

<span data-ttu-id="415b2-178">U kunt Hallo-ID van het virtuele netwerk van Hallo Hallo subnet met met behulp van Hallo ophalen `resourceId` sjabloonfunctie.</span><span class="sxs-lookup"><span data-stu-id="415b2-178">You can get hello ID of hello virtual network containing hello subnet by using hello `resourceId` template function.</span></span> <span data-ttu-id="415b2-179">Deze functie omvat Hallo type en de naam van een resource en retourneert Hallo volledig gekwalificeerde id van de bron.</span><span class="sxs-lookup"><span data-stu-id="415b2-179">This function takes in hello type and name of a resource and returns hello fully qualified identifier of that resource.</span></span> <span data-ttu-id="415b2-180">Deze ID heeft Hallo vorm:`/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/<resourceProviderNamespace>/<resourceType>/<resourceName>`</span><span class="sxs-lookup"><span data-stu-id="415b2-180">This ID has hello form: `/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/<resourceProviderNamespace>/<resourceType>/<resourceName>`</span></span>

<span data-ttu-id="415b2-181">Hallo-id van het virtuele netwerk Hallo is echter niet voldoende.</span><span class="sxs-lookup"><span data-stu-id="415b2-181">However, hello identifier of hello virtual network is not enough.</span></span> <span data-ttu-id="415b2-182">U moet specifieke Hallo-subnet dat Hallo scale set die virtuele machines moet opgeven.</span><span class="sxs-lookup"><span data-stu-id="415b2-182">You must specify hello specific subnet that hello scale set VMs should be in.</span></span> <span data-ttu-id="415b2-183">toodo dit samenvoegen `/subnets/mySubnet` toohello-ID van het virtuele netwerk Hallo.</span><span class="sxs-lookup"><span data-stu-id="415b2-183">toodo this, concatenate `/subnets/mySubnet` toohello ID of hello virtual network.</span></span> <span data-ttu-id="415b2-184">Hallo resultaat is volledig gekwalificeerd Hallo-ID van Hallo subnet.</span><span class="sxs-lookup"><span data-stu-id="415b2-184">hello result is hello fully qualified ID of hello subnet.</span></span> <span data-ttu-id="415b2-185">Deze samenvoeging Hello doen `concat` functie, die duurt in een reeks tekenreeksen en retourneert de samenvoeging.</span><span class="sxs-lookup"><span data-stu-id="415b2-185">Do this concatenation with hello `concat` function, which takes in a series of strings and returns their concatenation.</span></span>

```json
           "networkProfile": {
             "networkInterfaceConfigurations": [
               {
                 "name": "myNic",
                 "properties": {
                   "primary": "true",
                   "ipConfigurations": [
                     {
                       "name": "myIpConfig",
                       "properties": {
                         "subnet": {
                           "id": "[concat(resourceId('Microsoft.Network/virtualNetworks', 'myVnet'), '/subnets/mySubnet')]"
                         }
                       }
                     }
                   ]
                 }
               }
             ]
           }
         }
       }
     }
   ]
}

```

## <a name="next-steps"></a><span data-ttu-id="415b2-186">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="415b2-186">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
