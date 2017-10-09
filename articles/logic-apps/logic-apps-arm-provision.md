---
title: een logische app met een sjabloon in Azure aaaCreate | Microsoft Docs
description: "Gebruik een Azure Resource Manager-sjabloon toodeploy een logische app om werkstromen te definiëren."
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 7574cc7c-e5a1-4b7c-97f6-0cffb1a5d536
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2016
ms.author: LADocs; mandia
ms.openlocfilehash: efbacb534fc7f11e9b593aae4383480ce3a1752f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-logic-app-using-a-template"></a><span data-ttu-id="b8e2f-103">Een logische app maken met een sjabloon</span><span class="sxs-lookup"><span data-stu-id="b8e2f-103">Create a Logic App using a template</span></span>
<span data-ttu-id="b8e2f-104">Sjablonen bieden een snelle manier toouse verschillende connectors in een logische app.</span><span class="sxs-lookup"><span data-stu-id="b8e2f-104">Templates provide a quick way toouse different connectors within a logic app.</span></span> <span data-ttu-id="b8e2f-105">Logische apps bevat Azure Resource Manager-sjablonen voor toocreate een logische app die gebruikt toodefine zakelijke werkstromen kan worden.</span><span class="sxs-lookup"><span data-stu-id="b8e2f-105">Logic apps includes Azure Resource Manager templates for you toocreate a logic app that can be used toodefine business workflows.</span></span> <span data-ttu-id="b8e2f-106">U kunt definiëren welke bronnen worden geïmplementeerd, en hoe toodefine parameters wanneer u uw logische app implementeert.</span><span class="sxs-lookup"><span data-stu-id="b8e2f-106">You can define which resources are deployed, and how toodefine parameters when you deploy your logic app.</span></span> <span data-ttu-id="b8e2f-107">U kunt deze sjabloon voor uw eigen zakelijke scenario's gebruiken of aanpassen toomeet uw vereisten.</span><span class="sxs-lookup"><span data-stu-id="b8e2f-107">You can use this template for your own business scenarios, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="b8e2f-108">Zie voor meer informatie over Hallo Logic app-eigenschappen [Logic App werkstroom Management API](https://msdn.microsoft.com/library/azure/mt643788.aspx).</span><span class="sxs-lookup"><span data-stu-id="b8e2f-108">For more details on hello Logic app properties, see [Logic App Workflow Management API](https://msdn.microsoft.com/library/azure/mt643788.aspx).</span></span> 

<span data-ttu-id="b8e2f-109">Zie voor voorbeelden van Hallo definitie zelf [auteur Logic App-definities](logic-apps-author-definitions.md).</span><span class="sxs-lookup"><span data-stu-id="b8e2f-109">For examples of hello definition itself, see [Author Logic App definitions](logic-apps-author-definitions.md).</span></span> 

<span data-ttu-id="b8e2f-110">Zie voor meer informatie over het maken van sjablonen [Azure Resource Manager-sjablonen ontwerpen](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="b8e2f-110">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="b8e2f-111">Zie voor de volledige sjabloon hello, [sjabloon voor logische Apps](https://github.com/Azure/azure-quickstart-templates/blob/master/101-logic-app-create/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="b8e2f-111">For hello complete template, see [Logic App template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-logic-app-create/azuredeploy.json).</span></span>

## <a name="what-you-deploy"></a><span data-ttu-id="b8e2f-112">Wat u implementeert</span><span class="sxs-lookup"><span data-stu-id="b8e2f-112">What you deploy</span></span>
<span data-ttu-id="b8e2f-113">Met deze sjabloon kunt u een logische app implementeren.</span><span class="sxs-lookup"><span data-stu-id="b8e2f-113">With this template, you deploy a logic app.</span></span>

<span data-ttu-id="b8e2f-114">toorun Hallo implementatie selecteert automatisch Hallo volgende knop:</span><span class="sxs-lookup"><span data-stu-id="b8e2f-114">toorun hello deployment automatically, select hello following button:</span></span>  

<span data-ttu-id="b8e2f-115">[![TooAzure implementeren](media/logic-apps-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-logic-app-create%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="b8e2f-115">[![Deploy tooAzure](media/logic-apps-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-logic-app-create%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="b8e2f-116">Parameters</span><span class="sxs-lookup"><span data-stu-id="b8e2f-116">Parameters</span></span>
[!INCLUDE [app-service-logic-deploy-parameters](../../includes/app-service-logic-deploy-parameters.md)]

### <a name="testuri"></a><span data-ttu-id="b8e2f-117">testUri</span><span class="sxs-lookup"><span data-stu-id="b8e2f-117">testUri</span></span>
     "testUri": {
        "type": "string",
        "defaultValue": "http://azure.microsoft.com/en-us/status/feed/"
      }

## <a name="resources-toodeploy"></a><span data-ttu-id="b8e2f-118">Resources toodeploy</span><span class="sxs-lookup"><span data-stu-id="b8e2f-118">Resources toodeploy</span></span>
### <a name="logic-app"></a><span data-ttu-id="b8e2f-119">Logische app</span><span class="sxs-lookup"><span data-stu-id="b8e2f-119">Logic app</span></span>
<span data-ttu-id="b8e2f-120">Hallo logische app maakt.</span><span class="sxs-lookup"><span data-stu-id="b8e2f-120">Creates hello logic app.</span></span>

<span data-ttu-id="b8e2f-121">Hallo sjablonen maakt gebruik van een parameterwaarde voor Hallo logic app-naam.</span><span class="sxs-lookup"><span data-stu-id="b8e2f-121">hello templates uses a parameter value for hello logic app name.</span></span> <span data-ttu-id="b8e2f-122">Hallo-locatie van Hallo logic app toohello Hiermee dezelfde locatie als Hallo resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="b8e2f-122">It sets hello location of hello logic app toohello same location as hello resource group.</span></span> 

<span data-ttu-id="b8e2f-123">Deze definitie voor bepaalde eens per uur wordt uitgevoerd en pings Hallo opgegeven locatie in Hallo **testUri** parameter.</span><span class="sxs-lookup"><span data-stu-id="b8e2f-123">This particular definition runs once an hour, and pings hello location specified in hello **testUri** parameter.</span></span> 

    {
      "type": "Microsoft.Logic/workflows",
      "apiVersion": "2016-06-01",
      "name": "[parameters('logicAppName')]",
      "location": "[resourceGroup().location]",
      "tags": {
        "displayName": "LogicApp"
      },
      "properties": {
        "definition": {
          "$schema": "http://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
          "contentVersion": "1.0.0.0",
          "parameters": {
            "testURI": {
              "type": "string",
              "defaultValue": "[parameters('testUri')]"
            }
          },
          "triggers": {
            "recurrence": {
              "type": "recurrence",
              "recurrence": {
                "frequency": "Hour",
                "interval": 1
              }
            }
          },
          "actions": {
            "http": {
              "type": "Http",
              "inputs": {
                "method": "GET",
                "uri": "@parameters('testUri')"
              },
              "runAfter": {}
            }
          },
          "outputs": {}
        },
        "parameters": {}
      }
    }


## <a name="commands-toorun-deployment"></a><span data-ttu-id="b8e2f-124">Opdrachten toorun implementatie</span><span class="sxs-lookup"><span data-stu-id="b8e2f-124">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="b8e2f-125">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b8e2f-125">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="b8e2f-126">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b8e2f-126">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -g ExampleDeployGroup



