---
title: aaaAutomatic schalen en de virtuele machine schalen sets | Microsoft Docs
description: Meer informatie over het gebruik van diagnostische gegevens en automatisch schalen resources tooautomatically scale virtuele machines in een schaalset.
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d29a3385-179e-4331-a315-daa7ea5701df
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: adegeo
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 25f54b693e3c991577238242008c262023ed479c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-automatic-scaling-and-virtual-machine-scale-sets"></a><span data-ttu-id="1401d-103">Hoe toouse automatisch schalen en virtuele-Machineschaalsets</span><span class="sxs-lookup"><span data-stu-id="1401d-103">How toouse automatic scaling and Virtual Machine Scale Sets</span></span>
<span data-ttu-id="1401d-104">Automatische schaling van virtuele machines in een scale-set is Hallo maken of verwijderen van virtuele machines in Hallo instellen als nodig is toomatch prestatie-eisen.</span><span class="sxs-lookup"><span data-stu-id="1401d-104">Automatic scaling of virtual machines in a scale set is hello creation or deletion of machines in hello set as needed toomatch performance requirements.</span></span> <span data-ttu-id="1401d-105">Wanneer Hallo volume van werk groeit, een toepassing mogelijk aanvullende bronnen tooenable het tooeffectively taken uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="1401d-105">As hello volume of work grows, an application may require additional resources tooenable it tooeffectively perform tasks.</span></span>

<span data-ttu-id="1401d-106">Automatische schaling is een geautomatiseerd proces gemakkelijk beheeroverhead.</span><span class="sxs-lookup"><span data-stu-id="1401d-106">Automatic scaling is an automated process that helps ease management overhead.</span></span> <span data-ttu-id="1401d-107">Vermindert de overhead, of u kunt geen toocontinually monitor systeemprestaties bepalen hoe toomanage resources.</span><span class="sxs-lookup"><span data-stu-id="1401d-107">By reducing overhead, you don't need toocontinually monitor system performance or decide how toomanage resources.</span></span> <span data-ttu-id="1401d-108">Schalen is een elastische proces.</span><span class="sxs-lookup"><span data-stu-id="1401d-108">Scaling is an elastic process.</span></span> <span data-ttu-id="1401d-109">Meer bronnen kunnen worden toegevoegd als Hallo belasting toeneemt.</span><span class="sxs-lookup"><span data-stu-id="1401d-109">More resources can be added as hello load increases.</span></span> <span data-ttu-id="1401d-110">En als de aanvraag-afname resources kunnen verwijderde toominimize kosten worden en prestatieniveaus onderhouden.</span><span class="sxs-lookup"><span data-stu-id="1401d-110">And as demand decreases, resources can be removed toominimize costs and maintain performance levels.</span></span>

<span data-ttu-id="1401d-111">Stel automatisch schalen op een schaal ingesteld met behulp van een Azure Resource Manager-sjabloon, Azure PowerShell, Azure CLI of hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="1401d-111">Set up automatic scaling on a scale set by using an Azure Resource Manager template, Azure PowerShell, Azure CLI, or hello Azure portal.</span></span>

## <a name="set-up-scaling-by-using-resource-manager-templates"></a><span data-ttu-id="1401d-112">Een schaal met behulp van Resource Manager-sjablonen instellen</span><span class="sxs-lookup"><span data-stu-id="1401d-112">Set up scaling by using Resource Manager templates</span></span>
<span data-ttu-id="1401d-113">In plaats van te implementeren en beheren van elke resource van uw toepassing afzonderlijk, een sjabloon gebruiken waarmee alle resources in een enkele, gecoördineerde bewerking implementeert.</span><span class="sxs-lookup"><span data-stu-id="1401d-113">Rather than deploying and managing each resource of your application separately, use a template that deploys all resources in a single, coordinated operation.</span></span> <span data-ttu-id="1401d-114">In de sjabloon hello, toepassingsbronnen worden gedefinieerd en implementatieparameters zijn opgegeven voor verschillende omgevingen.</span><span class="sxs-lookup"><span data-stu-id="1401d-114">In hello template, application resources are defined and deployment parameters are specified for different environments.</span></span> <span data-ttu-id="1401d-115">Hallo sjabloon bestaat uit JSON en uitdrukkingen die u kunt tooconstruct waarden voor uw implementatie te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1401d-115">hello template consists of JSON and expressions that you can use tooconstruct values for your deployment.</span></span> <span data-ttu-id="1401d-116">toolearn meer, Bekijk [Azure Resource Manager-sjablonen samenstellen](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="1401d-116">toolearn more, look at [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="1401d-117">Geef in het Hallo-sjabloon Hallo capaciteit element:</span><span class="sxs-lookup"><span data-stu-id="1401d-117">In hello template, you specify hello capacity element:</span></span>

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 3
},
```

<span data-ttu-id="1401d-118">Capaciteit van identificeert het aantal virtuele machines in de set Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="1401d-118">Capacity identifies hello number of virtual machines in hello set.</span></span> <span data-ttu-id="1401d-119">U kunt handmatig Hallo capaciteit wijzigen door het implementeren van een sjabloon met een andere waarde.</span><span class="sxs-lookup"><span data-stu-id="1401d-119">You can manually change hello capacity by deploying a template with a different value.</span></span> <span data-ttu-id="1401d-120">Als u een sjabloon tooonly wijziging Hallo capaciteit implementeert, kunt u alleen Hallo SKU-element met Hallo bijgewerkt capaciteit kunt opnemen.</span><span class="sxs-lookup"><span data-stu-id="1401d-120">If you are deploying a template tooonly change hello capacity, you can include only hello SKU element with hello updated capacity.</span></span>

<span data-ttu-id="1401d-121">Hallo capaciteit van uw scale set kan worden automatisch aangepast door een combinatie van Hallo **autoscaleSettings** resource en Hallo extensie voor diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="1401d-121">hello capacity of your scale set can be automatically adjusted by using a combination of hello **autoscaleSettings** resource and hello diagnostics extension.</span></span>

### <a name="configure-hello-azure-diagnostics-extension"></a><span data-ttu-id="1401d-122">Hello Azure Diagnostics-uitbreiding configureren</span><span class="sxs-lookup"><span data-stu-id="1401d-122">Configure hello Azure Diagnostics extension</span></span>
<span data-ttu-id="1401d-123">Automatische schaling kan alleen worden uitgevoerd als de verzameling van metrische gegevens is voltooid op elke virtuele machine in de schaalset Hallo.</span><span class="sxs-lookup"><span data-stu-id="1401d-123">Automatic scaling can only be done if metrics collection is successful on each virtual machine in hello scale set.</span></span> <span data-ttu-id="1401d-124">Hello Azure-extensie voor diagnostische gegevens levert Hallo controle en diagnostische gegevens die voldoet aan Hallo metrische gegevens verzameling behoeften van Hallo automatisch schalen resource.</span><span class="sxs-lookup"><span data-stu-id="1401d-124">hello Azure Diagnostics Extension provides hello monitoring and diagnostics capabilities that meets hello metrics collection needs of hello autoscale resource.</span></span> <span data-ttu-id="1401d-125">U kunt Hallo uitbreiding installeren als onderdeel van Hallo Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="1401d-125">You can install hello extension as part of hello Resource Manager template.</span></span>

<span data-ttu-id="1401d-126">Dit voorbeeld ziet Hallo variabelen die worden gebruikt in de extensie voor diagnostische gegevens van Hallo sjabloon tooconfigure Hallo:</span><span class="sxs-lookup"><span data-stu-id="1401d-126">This example shows hello variables that are used in hello template tooconfigure hello diagnostics extension:</span></span>

```json
"diagnosticsStorageAccountName": "[concat(parameters('resourcePrefix'), 'saa')]",
"accountid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/', 'Microsoft.Storage/storageAccounts/', variables('diagnosticsStorageAccountName'))]",
"wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
"wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Thread Count\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
"wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
"wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
"wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
```

<span data-ttu-id="1401d-127">Parameters worden opgegeven wanneer Hallo sjabloon wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="1401d-127">Parameters are provided when hello template is deployed.</span></span> <span data-ttu-id="1401d-128">In dit voorbeeld Hallo-naam van Hallo storage-account (waar gegevens worden opgeslagen) en Hallo vindt u de naam van Hallo scale set (waarbij gegevens worden verzameld).</span><span class="sxs-lookup"><span data-stu-id="1401d-128">In this example, hello name of hello storage account (where data is stored) and hello name of hello scale set (where data is collected) are provided.</span></span> <span data-ttu-id="1401d-129">In dit voorbeeld Windows Server alleen Hallo aantal threads prestatiemeteritem ook verzameld.</span><span class="sxs-lookup"><span data-stu-id="1401d-129">Also in this Windows Server example, only hello Thread Count performance counter is collected.</span></span> <span data-ttu-id="1401d-130">Alle prestatiemeteritems die beschikbaar in Windows hello of Linux gebruikte toocollect diagnostische gegevens kan worden en kan worden opgenomen in de configuratie van Hallo-uitbreiding.</span><span class="sxs-lookup"><span data-stu-id="1401d-130">All hello available performance counters in Windows or Linux can be used toocollect diagnostics information and can be included in hello extension configuration.</span></span>

<span data-ttu-id="1401d-131">Dit voorbeeld ziet Hallo definitie van Hallo-uitbreiding in Hallo sjabloon:</span><span class="sxs-lookup"><span data-stu-id="1401d-131">This example shows hello definition of hello extension in hello template:</span></span>

```json
"extensionProfile": {
  "extensions": [
    {
      "name": "Microsoft.Insights.VMDiagnosticsSettings",
      "properties": {
        "publisher": "Microsoft.Azure.Diagnostics",
        "type": "IaaSDiagnostics",
        "typeHandlerVersion": "1.5",
        "autoUpgradeMinorVersion": true,
        "settings": {
          "xmlCfg": "[base64(concat(variables('wadcfgxstart'),variables('wadmetricsresourceid'),variables('wadcfgxend')))]",
          "storageAccount": "[variables('diagnosticsStorageAccountName')]"
        },
        "protectedSettings": {
          "storageAccountName": "[variables('diagnosticsStorageAccountName')]",
          "storageAccountKey": "[listkeys(variables('accountid'), variables('apiVersion')).key1]",
          "storageAccountEndPoint": "https://core.windows.net"
        }
      }
    }
  ]
}
```

<span data-ttu-id="1401d-132">Wanneer Hallo-extensie voor diagnostische gegevens wordt uitgevoerd, wordt dit door Hallo gegevens worden opgeslagen en die worden verzameld in een tabel in Hallo storage-account die u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="1401d-132">When hello diagnostics extension runs, hello data is stored and collected in a table, in hello storage account that you specify.</span></span> <span data-ttu-id="1401d-133">In Hallo **WADPerformanceCounters** tabel vindt u Hallo verzamelde gegevens:</span><span class="sxs-lookup"><span data-stu-id="1401d-133">In hello **WADPerformanceCounters** table, you can find hello collected data:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountBefore2.png)

### <a name="configure-hello-autoscalesettings-resource"></a><span data-ttu-id="1401d-134">Hallo autoScaleSettings resource configureren</span><span class="sxs-lookup"><span data-stu-id="1401d-134">Configure hello autoScaleSettings resource</span></span>
<span data-ttu-id="1401d-135">Hallo autoscaleSettings resource hand Hallo van Hallo diagnostics extensie toodecide of tooincrease of afname Hallo aantal virtuele machines in Hallo scale ingesteld.</span><span class="sxs-lookup"><span data-stu-id="1401d-135">hello autoscaleSettings resource uses hello information from hello diagnostics extension toodecide whether tooincrease or decrease hello number of virtual machines in hello scale set.</span></span>

<span data-ttu-id="1401d-136">In dit voorbeeld ziet u de configuratie Hallo van Hallo resource in Hallo sjabloon:</span><span class="sxs-lookup"><span data-stu-id="1401d-136">This example shows hello configuration of hello resource in hello template:</span></span>

```json
{
  "type": "Microsoft.Insights/autoscaleSettings",
  "apiVersion": "2015-04-01",
  "name": "[concat(parameters('resourcePrefix'),'as1')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
  ],
  "properties": {
    "enabled": true,
    "name": "[concat(parameters('resourcePrefix'),'as1')]",
    "profiles": [
      {
        "name": "Profile1",
        "capacity": {
          "minimum": "1",
          "maximum": "10",
          "default": "1"
        },
        "rules": [
          {
            "metricTrigger": {
              "metricName": "\\Processor(_Total)\\Thread Count",
              "metricNamespace": "",
              "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]",
              "timeGrain": "PT1M",
              "statistic": "Average",
              "timeWindow": "PT5M",
              "timeAggregation": "Average",
              "operator": "GreaterThan",
              "threshold": 650
            },
            "scaleAction": {
              "direction": "Increase",
              "type": "ChangeCount",
              "value": "1",
              "cooldown": "PT5M"
            }
          },
          {
            "metricTrigger": {
              "metricName": "\\Processor(_Total)\\Thread Count",
              "metricNamespace": "",
              "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]",
              "timeGrain": "PT1M",
              "statistic": "Average",
              "timeWindow": "PT5M",
              "timeAggregation": "Average",
              "operator": "LessThan",
              "threshold": 550
            },
            "scaleAction": {
              "direction": "Decrease",
              "type": "ChangeCount",
              "value": "1",
              "cooldown": "PT5M"
            }
          }
        ]
      }
    ],
    "targetResourceUri": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]"
  }
}
```

<span data-ttu-id="1401d-137">Hallo bovenstaande voorbeeld worden twee regels voor het definiëren van automatische schaling acties Hallo gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1401d-137">In hello example above, two rules are created for defining hello automatic scaling actions.</span></span> <span data-ttu-id="1401d-138">Hallo eerste regel definieert Hallo scale-out actie en de tweede regel Hallo definieert Hallo schaal in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="1401d-138">hello first rule defines hello scale-out action and hello second rule defines hello scale-in action.</span></span> <span data-ttu-id="1401d-139">Deze waarden zijn beschikbaar in Hallo regels:</span><span class="sxs-lookup"><span data-stu-id="1401d-139">These values are provided in hello rules:</span></span>

| <span data-ttu-id="1401d-140">Regel</span><span class="sxs-lookup"><span data-stu-id="1401d-140">Rule</span></span> | <span data-ttu-id="1401d-141">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="1401d-141">Description</span></span> |
| ---- | ----------- |
| <span data-ttu-id="1401d-142">metricName</span><span class="sxs-lookup"><span data-stu-id="1401d-142">metricName</span></span>        | <span data-ttu-id="1401d-143">Deze waarde is hetzelfde als Hallo prestatiemeteritem dat u hebt gedefinieerd in Hallo wadperfcounter variabele voor de extensie voor diagnostische gegevens Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="1401d-143">This value is hello same as hello performance counter that you defined in hello wadperfcounter variable for hello diagnostics extension.</span></span> <span data-ttu-id="1401d-144">Hallo bovenstaande voorbeeld wordt Hallo aantal threads teller gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1401d-144">In hello example above, hello Thread Count counter is used.</span></span>    |
| <span data-ttu-id="1401d-145">metricResourceUri</span><span class="sxs-lookup"><span data-stu-id="1401d-145">metricResourceUri</span></span> | <span data-ttu-id="1401d-146">Deze waarde is Hallo resource-id van de virtuele-machineschaalset Hallo weergeven.</span><span class="sxs-lookup"><span data-stu-id="1401d-146">This value is hello resource identifier of hello virtual machine scale set.</span></span> <span data-ttu-id="1401d-147">Deze id bevat Hallo-naam van de resourcegroep hello, Hallo-naam van de resourceprovider Hallo en Hallo-naam van Hallo scale set tooscale.</span><span class="sxs-lookup"><span data-stu-id="1401d-147">This identifier contains hello name of hello resource group, hello name of hello resource provider, and hello name of hello scale set tooscale.</span></span> |
| <span data-ttu-id="1401d-148">TimeGrain</span><span class="sxs-lookup"><span data-stu-id="1401d-148">timeGrain</span></span>         | <span data-ttu-id="1401d-149">Deze waarde is Hallo granulatie van Hallo metrische gegevens die worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="1401d-149">This value is hello granularity of hello metrics that are collected.</span></span> <span data-ttu-id="1401d-150">In de Hallo voorgaande voorbeeld, worden gegevens verzameld tijdens een interval van één minuut.</span><span class="sxs-lookup"><span data-stu-id="1401d-150">In hello preceding example, data is collected on an interval of one minute.</span></span> <span data-ttu-id="1401d-151">Deze waarde wordt gebruikt met de waarde voor timeWindow.</span><span class="sxs-lookup"><span data-stu-id="1401d-151">This value is used with timeWindow.</span></span> |
| <span data-ttu-id="1401d-152">statistiek</span><span class="sxs-lookup"><span data-stu-id="1401d-152">statistic</span></span>         | <span data-ttu-id="1401d-153">Deze waarde bepaalt hoe Hallo metrische gegevens worden gecombineerd tooaccommodate Hallo automatisch vergroten / verkleinen in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="1401d-153">This value determines how hello metrics are combined tooaccommodate hello automatic scaling action.</span></span> <span data-ttu-id="1401d-154">Hallo mogelijke waarden zijn: gemiddelde, Min, Max.</span><span class="sxs-lookup"><span data-stu-id="1401d-154">hello possible values are: Average, Min, Max.</span></span> |
| <span data-ttu-id="1401d-155">Waarde voor TimeWindow</span><span class="sxs-lookup"><span data-stu-id="1401d-155">timeWindow</span></span>        | <span data-ttu-id="1401d-156">Deze waarde is Hallo tijdbereik waarin de gegevens worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="1401d-156">This value is hello range of time in which instance data is collected.</span></span> <span data-ttu-id="1401d-157">Deze moet tussen 5 minuten en 12 uur.</span><span class="sxs-lookup"><span data-stu-id="1401d-157">It must be between 5 minutes and 12 hours.</span></span> |
| <span data-ttu-id="1401d-158">TimeAggregation van</span><span class="sxs-lookup"><span data-stu-id="1401d-158">timeAggregation</span></span>   | <span data-ttu-id="1401d-159">Deze waarde bepaalt hoe Hallo-gegevens die worden verzameld gedurende een bepaalde periode moeten worden gecombineerd.</span><span class="sxs-lookup"><span data-stu-id="1401d-159">This value determines how hello data that is collected should be combined over time.</span></span> <span data-ttu-id="1401d-160">Hallo-standaardwaarde is de gemiddelde.</span><span class="sxs-lookup"><span data-stu-id="1401d-160">hello default value is Average.</span></span> <span data-ttu-id="1401d-161">Hallo mogelijke waarden zijn: gemiddeld, Minimum, Maximum, laatste, totaal, Count.</span><span class="sxs-lookup"><span data-stu-id="1401d-161">hello possible values are: Average, Minimum, Maximum, Last, Total, Count.</span></span> |
| <span data-ttu-id="1401d-162">Operator</span><span class="sxs-lookup"><span data-stu-id="1401d-162">operator</span></span>          | <span data-ttu-id="1401d-163">Deze waarde is Hallo-operator die wordt gebruikt toocompare Hallo metrische gegevens en Hallo drempelwaarde.</span><span class="sxs-lookup"><span data-stu-id="1401d-163">This value is hello operator that is used toocompare hello metric data and hello threshold.</span></span> <span data-ttu-id="1401d-164">Hallo mogelijke waarden zijn: gelijk is aan NotEquals, groter dan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span><span class="sxs-lookup"><span data-stu-id="1401d-164">hello possible values are: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span></span> |
| <span data-ttu-id="1401d-165">Drempelwaarde</span><span class="sxs-lookup"><span data-stu-id="1401d-165">threshold</span></span>         | <span data-ttu-id="1401d-166">Deze waarde is Hallo-waarde waarmee de schaalactie hello wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="1401d-166">This value is hello value that triggers hello scale action.</span></span> <span data-ttu-id="1401d-167">Worden tooprovide ervoor dat een voldoende verschil tussen de drempelwaarden Hallo voor Hallo **scale-out** en **schaal in** acties.</span><span class="sxs-lookup"><span data-stu-id="1401d-167">Be sure tooprovide a sufficient difference between hello threshold values for hello **scale-out** and **scale-in** actions.</span></span> <span data-ttu-id="1401d-168">Als u op dezelfde waarden voor beide acties Hallo instelt, verwacht Hallo system constante wijziging, die voorkomt dat het implementeren van een actie vergroten/verkleinen.</span><span class="sxs-lookup"><span data-stu-id="1401d-168">If you set hello same values for both actions, hello system anticipates constant change, which prevents it from implementing a scaling action.</span></span> <span data-ttu-id="1401d-169">Bijvoorbeeld, werkt instellen van beide too600 threads in het voorgaande voorbeeld Hallo niet.</span><span class="sxs-lookup"><span data-stu-id="1401d-169">For example, setting both too600 threads in hello preceding example doesn't work.</span></span> |
| <span data-ttu-id="1401d-170">Richting</span><span class="sxs-lookup"><span data-stu-id="1401d-170">direction</span></span>         | <span data-ttu-id="1401d-171">Deze waarde bepaalt Hallo-actie die wordt uitgevoerd wanneer het Hallo-drempelwaarde wordt bereikt.</span><span class="sxs-lookup"><span data-stu-id="1401d-171">This value determines hello action that is taken when hello threshold value is achieved.</span></span> <span data-ttu-id="1401d-172">Hallo mogelijke waarden zijn vergroten of verkleinen.</span><span class="sxs-lookup"><span data-stu-id="1401d-172">hello possible values are Increase or Decrease.</span></span> |
| <span data-ttu-id="1401d-173">type</span><span class="sxs-lookup"><span data-stu-id="1401d-173">type</span></span>              | <span data-ttu-id="1401d-174">Deze waarde is Hallo type actie dat moet worden uitgevoerd en tooChangeCount moet worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="1401d-174">This value is hello type of action that should occur and must be set tooChangeCount.</span></span> |
| <span data-ttu-id="1401d-175">waarde</span><span class="sxs-lookup"><span data-stu-id="1401d-175">value</span></span>             | <span data-ttu-id="1401d-176">Deze waarde is het aantal virtuele machines die zijn toegevoegd tooor verwijderd uit Hallo scale set Hallo.</span><span class="sxs-lookup"><span data-stu-id="1401d-176">This value is hello number of virtual machines that are added tooor removed from hello scale set.</span></span> <span data-ttu-id="1401d-177">Deze waarde moet 1 of hoger.</span><span class="sxs-lookup"><span data-stu-id="1401d-177">This value must be 1 or greater.</span></span> |
| <span data-ttu-id="1401d-178">cooldown</span><span class="sxs-lookup"><span data-stu-id="1401d-178">cooldown</span></span>          | <span data-ttu-id="1401d-179">Deze waarde is Hallo hoeveelheid tijd toowait sinds de laatste vergroten/verkleinen actie Hallo voordat de volgende actie Hallo optreedt.</span><span class="sxs-lookup"><span data-stu-id="1401d-179">This value is hello amount of time toowait since hello last scaling action before hello next action occurs.</span></span> <span data-ttu-id="1401d-180">Deze waarde moet tussen 1 minuut en één week.</span><span class="sxs-lookup"><span data-stu-id="1401d-180">This value must be between one minute and one week.</span></span> |

<span data-ttu-id="1401d-181">U gebruikt, afhankelijk van het prestatiemeteritem hello, aantal elementen in de sjabloonconfiguratie Hallo Hallo anders worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1401d-181">Depending on hello performance counter, you are using, some of hello elements in hello template configuration are used differently.</span></span> <span data-ttu-id="1401d-182">In Hallo voorgaande voorbeeld, Hallo prestatiemeteritem is aantal threads, Hallo-drempelwaarde is 650 voor de actie van een scale-out en Hallo-drempelwaarde is 550 voor Hallo schaal in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="1401d-182">In hello preceding example, hello performance counter is Thread Count, hello threshold value is 650 for a scale-out action, and hello threshold value is 550 for hello scale-in action.</span></span> <span data-ttu-id="1401d-183">Als u een item, zoals % processortijd gebruikt, is de drempelwaarde Hallo toohello percentage van CPU-verbruik dat een vergroten/verkleinen actie bepaalt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="1401d-183">If you use a counter such as %Processor Time, hello threshold value is set toohello percentage of CPU usage that determines a scaling action.</span></span>

<span data-ttu-id="1401d-184">Wanneer een actie vergroten/verkleinen wordt geactiveerd, zoals een hoge belasting Hallo-capaciteit van Hallo is ingesteld op basis van de waarde in de sjabloon Hallo Hallo verhoogd.</span><span class="sxs-lookup"><span data-stu-id="1401d-184">When a scaling action is triggered, such as a high load, hello capacity of hello set is increased based on hello value in hello template.</span></span> <span data-ttu-id="1401d-185">Stel bijvoorbeeld in een schaal waar Hallo capaciteit too3 is ingesteld en Hallo schaalactiewaarde too1 is ingesteld:</span><span class="sxs-lookup"><span data-stu-id="1401d-185">For example, in a scale set where hello capacity is set too3 and hello scale action value is set too1:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerBefore.png)

<span data-ttu-id="1401d-186">Wanneer Hallo huidige load oorzaken Hallo thread gemiddelde aantal toogo boven de drempelwaarde Hallo 650:</span><span class="sxs-lookup"><span data-stu-id="1401d-186">When hello current load causes hello average thread count toogo above hello threshold of 650:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountAfter.png)

<span data-ttu-id="1401d-187">Een **scale-out** actie dat oorzaken capaciteit van Hallo set toobe verhoogd met één Hallo wordt geactiveerd:</span><span class="sxs-lookup"><span data-stu-id="1401d-187">A **scale-out** action is triggered that causes hello capacity of hello set toobe increased by one:</span></span>

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 4
},
```

<span data-ttu-id="1401d-188">Hallo-resultaat is dat een virtuele machine toohello scale set wordt toegevoegd:</span><span class="sxs-lookup"><span data-stu-id="1401d-188">hello result is a virtual machine is added toohello scale set:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerAfter.png)

<span data-ttu-id="1401d-189">Nadat een cooldown periode van vijf minuten, als Hallo kunt u het gemiddelde aantal threads op Hallo machines meer dan 600 blijft, is een andere computer toegevoegd toohello set.</span><span class="sxs-lookup"><span data-stu-id="1401d-189">After a cooldown period of five minutes, if hello average number of threads on hello machines stays over 600, another machine is added toohello set.</span></span> <span data-ttu-id="1401d-190">Hallo gemiddelde aantal threads onder 550 blijft, Hallo-capaciteit van Hallo scale set wordt verminderd door een als een machine wordt verwijderd uit het Hallo-set.</span><span class="sxs-lookup"><span data-stu-id="1401d-190">If hello average thread count stays below 550, hello capacity of hello scale set is reduced by one and a machine is removed from hello set.</span></span>

## <a name="set-up-scaling-using-azure-powershell"></a><span data-ttu-id="1401d-191">Instellen van schalen met Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1401d-191">Set up scaling using Azure PowerShell</span></span>

<span data-ttu-id="1401d-192">Voorbeelden van het gebruik van PowerShell tooset up automatisch schalen, toosee kijken [Azure Monitor PowerShell snel starten voorbeelden](../monitoring-and-diagnostics/insights-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="1401d-192">toosee examples of using PowerShell tooset up autoscaling, look at [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md).</span></span>

## <a name="set-up-scaling-using-azure-cli"></a><span data-ttu-id="1401d-193">Schalen met Azure CLI instellen</span><span class="sxs-lookup"><span data-stu-id="1401d-193">Set up scaling using Azure CLI</span></span>

<span data-ttu-id="1401d-194">Voorbeelden van het gebruik van Azure CLI tooset up automatisch schalen, toosee kijken [Azure Monitor platformoverschrijdende CLI snel starten voorbeelden](../monitoring-and-diagnostics/insights-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="1401d-194">toosee examples of using Azure CLI tooset up autoscaling, look at [Azure Monitor Cross-platform CLI quick start samples](../monitoring-and-diagnostics/insights-cli-samples.md).</span></span>

## <a name="set-up-scaling-using-hello-azure-portal"></a><span data-ttu-id="1401d-195">Schalen met hello Azure-portal instellen</span><span class="sxs-lookup"><span data-stu-id="1401d-195">Set up scaling using hello Azure portal</span></span>

<span data-ttu-id="1401d-196">een voorbeeld van het gebruik van toosee hello Azure portal tooset up automatisch schalen, zoekt u naar op [maken van een virtuele-Machineschaalset hello Azure-portal met](virtual-machine-scale-sets-portal-create.md).</span><span class="sxs-lookup"><span data-stu-id="1401d-196">toosee an example of using hello Azure portal tooset up autoscaling, look at [Create a Virtual Machine Scale Set using hello Azure portal](virtual-machine-scale-sets-portal-create.md).</span></span>

## <a name="investigate-scaling-actions"></a><span data-ttu-id="1401d-197">Schalen acties onderzoeken</span><span class="sxs-lookup"><span data-stu-id="1401d-197">Investigate scaling actions</span></span>

* <span data-ttu-id="1401d-198">**Azure Portal**</span><span class="sxs-lookup"><span data-stu-id="1401d-198">**Azure portal**</span></span>  
<span data-ttu-id="1401d-199">Momenteel kunt u een beperkte hoeveelheid informatie met Hallo portal ophalen.</span><span class="sxs-lookup"><span data-stu-id="1401d-199">You can currently get a limited amount of information using hello portal.</span></span>

* <span data-ttu-id="1401d-200">**Azure Resource Explorer**</span><span class="sxs-lookup"><span data-stu-id="1401d-200">**Azure Resource Explorer**</span></span>  
<span data-ttu-id="1401d-201">Dit hulpprogramma is Hallo aanbevolen voor de huidige status van uw scale set Hallo verkennen.</span><span class="sxs-lookup"><span data-stu-id="1401d-201">This tool is hello best for exploring hello current state of your scale set.</span></span> <span data-ttu-id="1401d-202">Volg dit pad en ziet u Hallo instantieweergave van de schaal Hallo instellen die u hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="1401d-202">Follow this path and you should see hello instance view of hello scale set that you created:</span></span>  
<span data-ttu-id="1401d-203">**Abonnementen > {uw abonnement} > resourceGroups > {uw resourcegroep} > providers > Microsoft.Compute > virtualMachineScaleSets > {uw schaalset} > virtuele machines**</span><span class="sxs-lookup"><span data-stu-id="1401d-203">**Subscriptions > {your subscription} > resourceGroups > {your resource group} > providers > Microsoft.Compute > virtualMachineScaleSets > {your scale set} > virtualMachines**</span></span>

* <span data-ttu-id="1401d-204">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="1401d-204">**Azure PowerShell**</span></span>  
<span data-ttu-id="1401d-205">Gebruik deze opdracht tooget sommige informatie:</span><span class="sxs-lookup"><span data-stu-id="1401d-205">Use this command tooget some information:</span></span>

  ```powershell
  Get-AzureRmResource -name vmsstest1 -ResourceGroupName vmsstestrg1 -ResourceType Microsoft.Compute/virtualMachineScaleSets -ApiVersion 2015-06-15
  Get-Autoscalesetting -ResourceGroup rainvmss -DetailedOutput
  ```

* <span data-ttu-id="1401d-206">Net zoals u zou een andere machine en klikt u op afstand toegang Hallo virtuele machines in Hallo scale set toomonitor afzonderlijke processen tot, verbinding maken met toohello jumpbox virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="1401d-206">Connect toohello jumpbox virtual machine just like you would any other machine and then you can remotely access hello virtual machines in hello scale set toomonitor individual processes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1401d-207">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1401d-207">Next Steps</span></span>
* <span data-ttu-id="1401d-208">Bekijk [machines automatisch schalen in een virtuele-Machineschaalset](virtual-machine-scale-sets-windows-autoscale.md) toosee een voorbeeld van hoe toocreate een schaalset met automatisch schalen is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="1401d-208">Look at [Automatically scale machines in a Virtual Machine Scale Set](virtual-machine-scale-sets-windows-autoscale.md) toosee an example of how toocreate a scale set with automatic scaling configured.</span></span>

* <span data-ttu-id="1401d-209">Voorbeelden van Azure Monitor bewakingsfuncties in [Azure Monitor PowerShell snel starten-voorbeelden](../monitoring-and-diagnostics/insights-powershell-samples.md)</span><span class="sxs-lookup"><span data-stu-id="1401d-209">Find examples of Azure Monitor monitoring features in [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md)</span></span>

* <span data-ttu-id="1401d-210">Meer informatie over functies in [automatisch schalen acties toosend e-mail en -webhook waarschuwingsmeldingen gebruiken in Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md).</span><span class="sxs-lookup"><span data-stu-id="1401d-210">Learn about notification features in [Use autoscale actions toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md).</span></span>

* <span data-ttu-id="1401d-211">Meer informatie over het te[gebruik auditlogboeken toosend e-mail en -webhook waarschuwingsmeldingen in de Azure-Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="1401d-211">Learn about how too[Use audit logs toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span></span>

* <span data-ttu-id="1401d-212">Meer informatie over [automatisch schalen ingewikkelde](virtual-machine-scale-sets-advanced-autoscale.md).</span><span class="sxs-lookup"><span data-stu-id="1401d-212">Learn about [advanced autoscale scenarios](virtual-machine-scale-sets-advanced-autoscale.md).</span></span>
