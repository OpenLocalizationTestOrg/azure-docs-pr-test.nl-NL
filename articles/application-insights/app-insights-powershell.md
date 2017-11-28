---
title: aaaAutomate Azure Application Insights met PowerShell | Microsoft Docs
description: Automatiseren maken resource, waarschuwing en beschikbaarheid tests in PowerShell met een Azure Resource Manager-sjabloon.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 9f73b87f-be63-4847-88c8-368543acad8b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/02/2017
ms.author: bwren
ms.openlocfilehash: ebd336eafba58a690a0e8ffbd1c74f7e93dbb682
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
#  <a name="create-application-insights-resources-using-powershell"></a><span data-ttu-id="b9952-103">Application Insights-resources maken met PowerShell</span><span class="sxs-lookup"><span data-stu-id="b9952-103">Create Application Insights resources using PowerShell</span></span>
<span data-ttu-id="b9952-104">Dit artikel laat zien hoe tooautomate Hallo maken en bijwerken van de [Application Insights](app-insights-overview.md) resources automatisch met behulp van Azure Resource Management.</span><span class="sxs-lookup"><span data-stu-id="b9952-104">This article shows you how tooautomate hello creation and update of [Application Insights](app-insights-overview.md) resources automatically by using Azure Resource Management.</span></span> <span data-ttu-id="b9952-105">U kunt bijvoorbeeld doen als onderdeel van een buildproces.</span><span class="sxs-lookup"><span data-stu-id="b9952-105">You might, for example, do so as part of a build process.</span></span> <span data-ttu-id="b9952-106">Samen met de Hallo basic Application Insights-resource, kunt u [webtests voor beschikbaarheid](app-insights-monitor-web-app-availability.md)Stel [waarschuwingen](app-insights-alerts.md)stelt hello [prijzen schema](app-insights-pricing.md), en andere Azure maken bronnen.</span><span class="sxs-lookup"><span data-stu-id="b9952-106">Along with hello basic Application Insights resource, you can create [availability web tests](app-insights-monitor-web-app-availability.md), set up [alerts](app-insights-alerts.md), set hello [pricing scheme](app-insights-pricing.md), and create other Azure resources.</span></span>

<span data-ttu-id="b9952-107">Hallo sleutel toocreating deze resources is een JSON-sjablonen voor [Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="b9952-107">hello key toocreating these resources is JSON templates for [Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span></span> <span data-ttu-id="b9952-108">Kortom, Hallo procedure is: Hallo JSON definities van bestaande resources; downloaden parameter van bepaalde waarden zoals namen; en voer vervolgens de sjabloon Hallo gewenst toocreate een nieuwe resource.</span><span class="sxs-lookup"><span data-stu-id="b9952-108">In a nutshell, hello procedure is: download hello JSON definitions of existing resources; parameterize certain values such as names; and then run hello template whenever you want toocreate a new resource.</span></span> <span data-ttu-id="b9952-109">U kunt verschillende resources samen, toocreate die ze in een Ga - bijvoorbeeld, een app-monitor met beschikbaarheidstests, waarschuwingen en opslag voor continue export van het pakket.</span><span class="sxs-lookup"><span data-stu-id="b9952-109">You can package several resources together, toocreate them all in one go - for example, an app monitor with availability tests, alerts, and storage for continuous export.</span></span> <span data-ttu-id="b9952-110">Er zijn enkele toosome eigenaardigheden van Hallo parameteriseringen, die wordt hier uitgelegd.</span><span class="sxs-lookup"><span data-stu-id="b9952-110">There are some subtleties toosome of hello parameterizations, which we'll explain here.</span></span>

## <a name="one-time-setup"></a><span data-ttu-id="b9952-111">Eenmalige instelling</span><span class="sxs-lookup"><span data-stu-id="b9952-111">One-time setup</span></span>
<span data-ttu-id="b9952-112">Als u dit nog niet hebt PowerShell met uw Azure-abonnement voordat gebruikt:</span><span class="sxs-lookup"><span data-stu-id="b9952-112">If you haven't used PowerShell with your Azure subscription before:</span></span>

<span data-ttu-id="b9952-113">Hello Azure Powershell-module installeren op Hallo machine waar u toorun Hallo scripts:</span><span class="sxs-lookup"><span data-stu-id="b9952-113">Install hello Azure Powershell module on hello machine where you want toorun hello scripts:</span></span>

1. <span data-ttu-id="b9952-114">Installeer [Microsoft Web Platform Installer (v5 of hoger)](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="b9952-114">Install [Microsoft Web Platform Installer (v5 or higher)](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
2. <span data-ttu-id="b9952-115">Deze tooinstall Microsoft Azure Powershell gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b9952-115">Use it tooinstall Microsoft Azure Powershell.</span></span>

## <a name="create-an-azure-resource-manager-template"></a><span data-ttu-id="b9952-116">Een Azure Resource Manager-sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="b9952-116">Create an Azure Resource Manager template</span></span>
<span data-ttu-id="b9952-117">Maak een nieuw .json-bestand - gaan we deze aanroepen `template1.json` in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="b9952-117">Create a new .json file - let's call it `template1.json` in this example.</span></span> <span data-ttu-id="b9952-118">Kopieer deze inhoud naar het:</span><span class="sxs-lookup"><span data-stu-id="b9952-118">Copy this content into it:</span></span>

```JSON
    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "appName": {
                "type": "string",
                "metadata": {
                    "description": "Enter hello application name."
                }
            },
            "appType": {
                "type": "string",
                "defaultValue": "web",
                "allowedValues": [
                    "web",
                    "java",
                    "HockeyAppBridge",
                    "other"
                ],
                "metadata": {
                    "description": "Enter hello application type."
                }
            },
            "appLocation": {
                "type": "string",
                "defaultValue": "East US",
                "allowedValues": [
                    "South Central US",
                    "West Europe",
                    "East US",
                    "North Europe"
                ],
                "metadata": {
                    "description": "Enter hello application location."
                }
            },
            "priceCode": {
                "type": "int",
                "defaultValue": 1,
                "allowedValues": [
                    1,
                    2
                ],
                "metadata": {
                    "description": "1 = Basic, 2 = Enterprise"
                }
            },
            "dailyQuota": {
                "type": "int",
                "defaultValue": 100,
                "minValue": 1,
                "metadata": {
                    "description": "Enter daily quota in GB."
                }
            },
            "dailyQuotaResetTime": {
                "type": "int",
                "defaultValue": 24,
                "metadata": {
                    "description": "Enter daily quota reset hour in UTC (0 too23). Values outside hello range will get a random reset hour."
                }
            },
            "warningThreshold": {
                "type": "int",
                "defaultValue": 90,
                "minValue": 1,
                "maxValue": 100,
                "metadata": {
                    "description": "Enter hello % value of daily quota after which warning mail toobe sent. "
                }
            }
        },
        "variables": {
            "priceArray": [
                "Basic",
                "Application Insights Enterprise"
            ],
            "pricePlan": "[take(variables('priceArray'),parameters('priceCode'))]",
            "billingplan": "[concat(parameters('appName'),'/', variables('pricePlan')[0])]"
        },
        "resources": [
            {
                "type": "microsoft.insights/components",
                "kind": "[parameters('appType')]",
                "name": "[parameters('appName')]",
                "apiVersion": "2014-04-01",
                "location": "[parameters('appLocation')]",
                "tags": {},
                "properties": {
                    "ApplicationId": "[parameters('appName')]"
                },
                "dependsOn": []
            },
            {
                "name": "[variables('billingplan')]",
                "type": "microsoft.insights/components/CurrentBillingFeatures",
                "location": "[parameters('appLocation')]",
                "apiVersion": "2015-05-01",
                "dependsOn": [
                    "[resourceId('microsoft.insights/components', parameters('appName'))]"
                ],
                "properties": {
                    "CurrentBillingFeatures": "[variables('pricePlan')]",
                    "DataVolumeCap": {
                        "Cap": "[parameters('dailyQuota')]",
                        "WarningThreshold": "[parameters('warningThreshold')]",
                        "ResetTime": "[parameters('dailyQuotaResetTime')]"
                    }
                }
            }
        ]
    }
```



## <a name="create-application-insights-resources"></a><span data-ttu-id="b9952-119">Application Insights-resources maken</span><span class="sxs-lookup"><span data-stu-id="b9952-119">Create Application Insights resources</span></span>
1. <span data-ttu-id="b9952-120">Aanmelden tooAzure in PowerShell:</span><span class="sxs-lookup"><span data-stu-id="b9952-120">In PowerShell, sign in tooAzure:</span></span>
   
    `Login-AzureRmAccount`
2. <span data-ttu-id="b9952-121">Voer een opdracht als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="b9952-121">Run a command like this:</span></span>
   
    ```PS
   
        New-AzureRmResourceGroupDeployment -ResourceGroupName Fabrikam `
               -TemplateFile .\template1.json `
               -appName myNewApp

    ``` 
   
   * <span data-ttu-id="b9952-122">`-ResourceGroupName`Hallo-groep is waar u toocreate Hallo nieuwe resources.</span><span class="sxs-lookup"><span data-stu-id="b9952-122">`-ResourceGroupName` is hello group where you want toocreate hello new resources.</span></span>
   * <span data-ttu-id="b9952-123">`-TemplateFile`Er moeten plaatsvinden voordat Hallo aangepaste parameters.</span><span class="sxs-lookup"><span data-stu-id="b9952-123">`-TemplateFile` must occur before hello custom parameters.</span></span>
   * <span data-ttu-id="b9952-124">`-appName`Hallo-naam van Hallo resource toocreate.</span><span class="sxs-lookup"><span data-stu-id="b9952-124">`-appName` hello name of hello resource toocreate.</span></span>

<span data-ttu-id="b9952-125">U kunt andere parameters toevoegen - vindt u bijbehorende beschrijvingen in de sectie van de parameters Hallo van Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="b9952-125">You can add other parameters - you'll find their descriptions in hello parameters section of hello template.</span></span>

## <a name="tooget-hello-instrumentation-key"></a><span data-ttu-id="b9952-126">tooget hello instrumentatiesleutel</span><span class="sxs-lookup"><span data-stu-id="b9952-126">tooget hello instrumentation key</span></span>
<span data-ttu-id="b9952-127">Na het maken van de bron van een toepassing, moet u de instrumentatiesleutel Hallo:</span><span class="sxs-lookup"><span data-stu-id="b9952-127">After creating an application resource, you'll want hello instrumentation key:</span></span> 

```PS
    $resource = Find-AzureRmResource -ResourceNameEquals "<YOUR APP NAME>" -ResourceType "Microsoft.Insights/components"
    $details = Get-AzureRmResource -ResourceId $resource.ResourceId
    $ikey = $details.Properties.InstrumentationKey
```


<a id="price"></a>
## <a name="set-hello-price-plan"></a><span data-ttu-id="b9952-128">Set Hallo prijs plannen</span><span class="sxs-lookup"><span data-stu-id="b9952-128">Set hello price plan</span></span>

<span data-ttu-id="b9952-129">U kunt instellen Hallo [prijs plan](app-insights-pricing.md).</span><span class="sxs-lookup"><span data-stu-id="b9952-129">You can set hello [price plan](app-insights-pricing.md).</span></span>

<span data-ttu-id="b9952-130">een app-resource met Hallo Enterprise prijs plan, met behulp van Hallo sjabloon bovenstaande toocreate:</span><span class="sxs-lookup"><span data-stu-id="b9952-130">toocreate an app resource with hello Enterprise price plan, using hello template above:</span></span>

```PS
        New-AzureRmResourceGroupDeployment -ResourceGroupName Fabrikam `
               -TemplateFile .\template1.json `
               -priceCode 2 `
               -appName myNewApp
```

|<span data-ttu-id="b9952-131">priceCode</span><span class="sxs-lookup"><span data-stu-id="b9952-131">priceCode</span></span>|<span data-ttu-id="b9952-132">Plannen</span><span class="sxs-lookup"><span data-stu-id="b9952-132">plan</span></span>|
|---|---|
|<span data-ttu-id="b9952-133">1</span><span class="sxs-lookup"><span data-stu-id="b9952-133">1</span></span>|<span data-ttu-id="b9952-134">Basic</span><span class="sxs-lookup"><span data-stu-id="b9952-134">Basic</span></span>|
|<span data-ttu-id="b9952-135">2</span><span class="sxs-lookup"><span data-stu-id="b9952-135">2</span></span>|<span data-ttu-id="b9952-136">Enterprise</span><span class="sxs-lookup"><span data-stu-id="b9952-136">Enterprise</span></span>|

* <span data-ttu-id="b9952-137">Als u alleen toouse Hallo standaardplan basisprijs wilt, kunt u Hallo CurrentBillingFeatures resource van de sjabloon Hallo weglaten.</span><span class="sxs-lookup"><span data-stu-id="b9952-137">If you only want toouse hello default Basic price plan, you can omit hello CurrentBillingFeatures resource from hello template.</span></span>
* <span data-ttu-id="b9952-138">Als u toochange Hallo prijs plan wilt nadat Hallo onderdeel resource is gemaakt, kunt u een sjabloon die worden weggelaten Hallo 'microsoft.insights/components' resource.</span><span class="sxs-lookup"><span data-stu-id="b9952-138">If you want toochange hello price plan after hello component resource has been created, you can use a template that omits hello "microsoft.insights/components" resource.</span></span> <span data-ttu-id="b9952-139">Bovendien weglaten Hallo `dependsOn` knooppunt uit Hallo resource facturering.</span><span class="sxs-lookup"><span data-stu-id="b9952-139">Also, omit hello `dependsOn` node from hello billing resource.</span></span> 

<span data-ttu-id="b9952-140">tooverify Hallo bijgewerkte prijs plan, bekijkt hello 'Functies + prijzen' blade in Hallo browser.</span><span class="sxs-lookup"><span data-stu-id="b9952-140">tooverify hello updated price plan, look at hello "Features+pricing" blade in hello browser.</span></span> <span data-ttu-id="b9952-141">**Vernieuw de weergave van de browser Hallo** toomake zeker dat u de meest recente toestand Hallo zien.</span><span class="sxs-lookup"><span data-stu-id="b9952-141">**Refresh hello browser view** toomake sure you see hello latest state.</span></span>



## <a name="add-a-metric-alert"></a><span data-ttu-id="b9952-142">Waarschuwing voor een metrische toevoegen</span><span class="sxs-lookup"><span data-stu-id="b9952-142">Add a metric alert</span></span>

<span data-ttu-id="b9952-143">tooset van een waarschuwing voor metrische bij Hallo dezelfde tijd als uw app-resource, merge-code als volgt naar het sjabloonbestand Hallo:</span><span class="sxs-lookup"><span data-stu-id="b9952-143">tooset up a metric alert at hello same time as your app resource, merge code like this into hello template file:</span></span>

```JSON
{
    parameters: { ... // existing parameters ...
            "responseTime": {
              "type": "int",
              "defaultValue": 3,
              "minValue": 1,
              "metadata": {
                "description": "Enter response time threshold in seconds."
              }
    },
    variables: { ... // existing variables ...
      // Alert names must be unique within resource group.
      "responseAlertName": "[concat('ResponseTime-', toLower(parameters('appName')))]"
    }, 
    resources: { ... // existing resources ...
     {
      //
      // Metric alert on response time
      //
      "name": "[variables('responseAlertName')]",
      "type": "Microsoft.Insights/alertrules",
      "apiVersion": "2014-04-01",
      "location": "[parameters('appLocation')]",
      // Ensure this resource is created after hello app resource:
      "dependsOn": [
        "[resourceId('Microsoft.Insights/components', parameters('appName'))]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Insights/components', parameters('appName')))]": "Resource"
      },
      "properties": {
        "name": "[variables('responseAlertName')]",
        "description": "response time alert",
        "isEnabled": true,
        "condition": {
          "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.ThresholdRuleCondition, Microsoft.WindowsAzure.Management.Mon.Client",
          "odata.type": "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
          "dataSource": {
            "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleMetricDataSource, Microsoft.WindowsAzure.Management.Mon.Client",
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
            "resourceUri": "[resourceId('microsoft.insights/components', parameters('appName'))]",
            "metricName": "request.duration"
          },
          "threshold": "[parameters('responseTime')]", //seconds
          "windowSize": "PT15M" // Take action if changed state for 15 minutes
        },
        "actions": [
          {
            "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleEmailAction, Microsoft.WindowsAzure.Management.Mon.Client",
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
            "sendToServiceOwners": true,
            "customEmails": []
          }
        ]
      }
    }
}
```

<span data-ttu-id="b9952-144">Als u de sjabloon Hallo aanroept, kunt u eventueel deze parameter toevoegen:</span><span class="sxs-lookup"><span data-stu-id="b9952-144">When you invoke hello template, you can optionally add this parameter:</span></span>

    `-responseTime 2`

<span data-ttu-id="b9952-145">U kunt uiteraard parameter van andere velden.</span><span class="sxs-lookup"><span data-stu-id="b9952-145">You can of course parameterize other fields.</span></span> 

<span data-ttu-id="b9952-146">toofind uit Hallo namen en configuratie-informatie van andere waarschuwingsregels handmatig maken van een regel en vervolgens controleren in [Azure Resource Manager](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b9952-146">toofind out hello type names and configuration details of other alert rules, create a rule manually and then inspect it in [Azure Resource Manager](https://resources.azure.com/).</span></span> 


## <a name="add-an-availability-test"></a><span data-ttu-id="b9952-147">Een beschikbaarheidstest toevoegen</span><span class="sxs-lookup"><span data-stu-id="b9952-147">Add an availability test</span></span>

<span data-ttu-id="b9952-148">In dit voorbeeld is voor een Pingtest (tootest één pagina).</span><span class="sxs-lookup"><span data-stu-id="b9952-148">This example is for a ping test (tootest a single page).</span></span>  

<span data-ttu-id="b9952-149">**Er zijn twee delen** in een beschikbaarheidstest: Hallo test zelf en Hallo waarschuwing die een melding van fouten.</span><span class="sxs-lookup"><span data-stu-id="b9952-149">**There are two parts** in an availability test: hello test itself, and hello alert that notifies you of failures.</span></span>

<span data-ttu-id="b9952-150">Samenvoegen Hallo na de code in Hallo sjabloonbestand die Hallo-app maakt.</span><span class="sxs-lookup"><span data-stu-id="b9952-150">Merge hello following code into hello template file that creates hello app.</span></span>

```JSON
{
    parameters: { ... // existing parameters here ...
      "pingURL": { "type": "string" },
      "pingText": { "type": "string" , defaultValue: ""}
    },
    variables: { ... // existing variables here ...
      "pingTestName":"[concat('PingTest-', toLower(parameters('appName')))]",
      "pingAlertRuleName": "[concat('PingAlert-', toLower(parameters('appName')), '-', subscription().subscriptionId)]"
    },
    resources: { ... // existing resources here ...
    { //
      // Availability test: part 1 configures hello test
      //
      "name": "[variables('pingTestName')]",
      "type": "Microsoft.Insights/webtests",
      "apiVersion": "2014-04-01",
      "location": "[parameters('appLocation')]",
      // Ensure this is created after hello app resource:
      "dependsOn": [
        "[resourceId('Microsoft.Insights/components', parameters('appName'))]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Insights/components', parameters('appName')))]": "Resource"
      },
      "properties": {
        "Name": "[variables('pingTestName')]",
        "Description": "Basic ping test",
        "Enabled": true,
        "Frequency": 900, // 15 minutes
        "Timeout": 120, // 2 minutes
        "Kind": "ping", // single URL test
        "RetryEnabled": true,
        "Locations": [
          {
            "Id": "us-va-ash-azr"
          },
          {
            "Id": "emea-nl-ams-azr"
          },
          {
            "Id": "apac-jp-kaw-edge"
          }
        ],
        "Configuration": {
          "WebTest": "[concat('<WebTest   Name=\"', variables('pingTestName'), '\"   Enabled=\"True\"         CssProjectStructure=\"\"    CssIteration=\"\"  Timeout=\"120\"  WorkItemIds=\"\"         xmlns=\"http://microsoft.com/schemas/VisualStudio/TeamTest/2010\"         Description=\"\"  CredentialUserName=\"\"  CredentialPassword=\"\"         PreAuthenticate=\"True\"  Proxy=\"default\"  StopOnError=\"False\"         RecordedResultFile=\"\"  ResultsLocale=\"\">  <Items>  <Request Method=\"GET\"    Version=\"1.1\"  Url=\"', parameters('Url'),   '\" ThinkTime=\"0\"  Timeout=\"300\" ParseDependentRequests=\"True\"         FollowRedirects=\"True\" RecordResult=\"True\" Cache=\"False\"         ResponseTimeGoal=\"0\"  Encoding=\"utf-8\"  ExpectedHttpStatusCode=\"200\"         ExpectedResponseUrl=\"\" ReportingName=\"\" IgnoreHttpStatusCode=\"False\" />        </Items>  <ValidationRules> <ValidationRule  Classname=\"Microsoft.VisualStudio.TestTools.WebTesting.Rules.ValidationRuleFindText, Microsoft.VisualStudio.QualityTools.WebTestFramework, Version=10.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a\" DisplayName=\"Find Text\"         Description=\"Verifies hello existence of hello specified text in hello response.\"         Level=\"High\"  ExectuionOrder=\"BeforeDependents\">  <RuleParameters>        <RuleParameter Name=\"FindText\" Value=\"',   parameters('pingText'), '\" />  <RuleParameter Name=\"IgnoreCase\" Value=\"False\" />  <RuleParameter Name=\"UseRegularExpression\" Value=\"False\" />  <RuleParameter Name=\"PassIfTextFound\" Value=\"True\" />  </RuleParameters> </ValidationRule>  </ValidationRules>  </WebTest>')]"
        },
        "SyntheticMonitorId": "[variables('pingTestName')]"
      }
    },

    {
      //
      // Availability test: part 2, hello alert rule
      //
      "name": "[variables('pingAlertRuleName')]",
      "type": "Microsoft.Insights/alertrules",
      "apiVersion": "2014-04-01",
      "location": "[parameters('appLocation')]", 
      "dependsOn": [
        "[resourceId('Microsoft.Insights/webtests', variables('pingTestName'))]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Insights/components', parameters('appName')))]": "Resource",
        "[concat('hidden-link:', resourceId('Microsoft.Insights/webtests', variables('pingTestName')))]": "Resource"
      },
      "properties": {
        "name": "[variables('pingAlertRuleName')]",
        "description": "alert for web test",
        "isEnabled": true,
        "condition": {
          "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.LocationThresholdRuleCondition, Microsoft.WindowsAzure.Management.Mon.Client",
          "odata.type": "Microsoft.Azure.Management.Insights.Models.LocationThresholdRuleCondition",
          "dataSource": {
            "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleMetricDataSource, Microsoft.WindowsAzure.Management.Mon.Client",
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
            "resourceUri": "[resourceId('microsoft.insights/webtests', variables('pingTestName'))]",
            "metricName": "GSMT_AvRaW"
          },
          "windowSize": "PT15M", // Take action if changed state for 15 minutes
          "failedLocationCount": 2
        },
        "actions": [
          {
            "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleEmailAction, Microsoft.WindowsAzure.Management.Mon.Client",
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
            "sendToServiceOwners": true,
            "customEmails": []
          }
        ]
      }
    }
}
```

<span data-ttu-id="b9952-151">toodiscover hello codes voor andere testlocaties of tooautomate Hallo maken van een complexere webtests, een voorbeeld handmatig maken en vervolgens voorzien Hallo code uit [Azure Resource Manager](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b9952-151">toodiscover hello codes for other test locations, or tooautomate hello creation of more complex web tests, create an example manually and then parameterize hello code from [Azure Resource Manager](https://resources.azure.com/).</span></span>

## <a name="add-more-resources"></a><span data-ttu-id="b9952-152">Voeg meer resources toe</span><span class="sxs-lookup"><span data-stu-id="b9952-152">Add more resources</span></span>

<span data-ttu-id="b9952-153">tooautomate hello maken van een andere bron van welke aard handmatig maken van een voorbeeld en kopieert en voorzien van de code van [Azure Resource Manager](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b9952-153">tooautomate hello creation of any other resource of any kind, create an example manually, and then copy and parameterize its code from [Azure Resource Manager](https://resources.azure.com/).</span></span> 

1. <span data-ttu-id="b9952-154">Open [Azure Resource Manager](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b9952-154">Open [Azure Resource Manager](https://resources.azure.com/).</span></span> <span data-ttu-id="b9952-155">Navigeren naar beneden `subscriptions/resourceGroups/<your resource group>/providers/Microsoft.Insights/components`, tooyour toepassingsbron.</span><span class="sxs-lookup"><span data-stu-id="b9952-155">Navigate down through `subscriptions/resourceGroups/<your resource group>/providers/Microsoft.Insights/components`, tooyour application resource.</span></span> 
   
    ![Navigatie in de Azure-Resource Explorer](./media/app-insights-powershell/01.png)
   
    <span data-ttu-id="b9952-157">*Onderdelen* zijn Hallo basic Application Insights-resources voor het weergeven van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="b9952-157">*Components* are hello basic Application Insights resources for displaying applications.</span></span> <span data-ttu-id="b9952-158">Er zijn afzonderlijke bronnen voor Hallo waarschuwingsregels en webtests voor beschikbaarheid gekoppelde.</span><span class="sxs-lookup"><span data-stu-id="b9952-158">There are separate resources for hello associated alert rules and availability web tests.</span></span>
2. <span data-ttu-id="b9952-159">Kopiëren Hallo JSON van het onderdeel in de juiste plaats Hallo Hallo in `template1.json`.</span><span class="sxs-lookup"><span data-stu-id="b9952-159">Copy hello JSON of hello component into hello appropriate place in `template1.json`.</span></span>
3. <span data-ttu-id="b9952-160">Verwijder deze eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="b9952-160">Delete these properties:</span></span>
   
   * `id`
   * `InstrumentationKey`
   * `CreationDate`
   * `TenantId`
4. <span data-ttu-id="b9952-161">Hallo webtests en alertrules secties openen en kopieer Hallo JSON voor afzonderlijke items in de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="b9952-161">Open hello webtests and alertrules sections and copy hello JSON for individual items into your template.</span></span> <span data-ttu-id="b9952-162">(Vanaf Hallo webtests of alertrules-knooppunten niet kopiëren: Ga naar de items onder deze Hallo.)</span><span class="sxs-lookup"><span data-stu-id="b9952-162">(Don't copy from hello webtests or alertrules nodes: go into hello items under them.)</span></span>
   
    <span data-ttu-id="b9952-163">Elke WebTest heeft een bijbehorende waarschuwingsregel, zodat u toocopy hiervan hebt.</span><span class="sxs-lookup"><span data-stu-id="b9952-163">Each web test has an associated alert rule, so you have toocopy both of them.</span></span>
   
    <span data-ttu-id="b9952-164">U kunt ook waarschuwingen op metrische gegevens opnemen.</span><span class="sxs-lookup"><span data-stu-id="b9952-164">You can also include alerts on metrics.</span></span> <span data-ttu-id="b9952-165">[De namen van de metrische](app-insights-powershell-alerts.md#metric-names).</span><span class="sxs-lookup"><span data-stu-id="b9952-165">[Metric names](app-insights-powershell-alerts.md#metric-names).</span></span>
5. <span data-ttu-id="b9952-166">Deze regel invoegen in elke resource:</span><span class="sxs-lookup"><span data-stu-id="b9952-166">Insert this line in each resource:</span></span>
   
    `"apiVersion": "2015-05-01",`

### <a name="parameterize-hello-template"></a><span data-ttu-id="b9952-167">Hallo sjabloon voorzien</span><span class="sxs-lookup"><span data-stu-id="b9952-167">Parameterize hello template</span></span>
<span data-ttu-id="b9952-168">U hebt nu tooreplace Hallo specifieke namen met parameters.</span><span class="sxs-lookup"><span data-stu-id="b9952-168">Now you have tooreplace hello specific names with parameters.</span></span> <span data-ttu-id="b9952-169">te[voorzien van een sjabloon](../azure-resource-manager/resource-group-authoring-templates.md), schrijven van expressies met een [reeks hulpfuncties](../azure-resource-manager/resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="b9952-169">too[parameterize a template](../azure-resource-manager/resource-group-authoring-templates.md), you write expressions using a [set of helper functions](../azure-resource-manager/resource-group-template-functions.md).</span></span> 

<span data-ttu-id="b9952-170">Kunnen niet worden voorzien van slechts een deel van een tekenreeks, dus gebruik `concat()` toobuild tekenreeksen.</span><span class="sxs-lookup"><span data-stu-id="b9952-170">You can't parameterize just part of a string, so use `concat()` toobuild strings.</span></span>

<span data-ttu-id="b9952-171">Hier volgen voorbeelden van Hallo vervangingen moet u toomake.</span><span class="sxs-lookup"><span data-stu-id="b9952-171">Here are examples of hello substitutions you'll want toomake.</span></span> <span data-ttu-id="b9952-172">Er zijn meerdere exemplaren van elke vervanging.</span><span class="sxs-lookup"><span data-stu-id="b9952-172">There are several occurrences of each substitution.</span></span> <span data-ttu-id="b9952-173">Mogelijk moet u anderen in uw sjabloon.</span><span class="sxs-lookup"><span data-stu-id="b9952-173">You might need others in your template.</span></span> <span data-ttu-id="b9952-174">Deze voorbeelden gebruiken Hallo-parameters en variabelen die we gedefinieerd Hallo boven aan het Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="b9952-174">These examples use hello parameters and variables we defined at hello top of hello template.</span></span>

| <span data-ttu-id="b9952-175">zoeken</span><span class="sxs-lookup"><span data-stu-id="b9952-175">find</span></span> | <span data-ttu-id="b9952-176">vervangen</span><span class="sxs-lookup"><span data-stu-id="b9952-176">replace with</span></span> |
| --- | --- |
| `"hidden-link:/subscriptions/.../components/MyAppName"` |`"[concat('hidden-link:',`<br/>` resourceId('microsoft.insights/components',` <br/> ` parameters('appName')))]"` |
| `"/subscriptions/.../alertrules/myAlertName-myAppName-subsId",` |`"[resourceId('Microsoft.Insights/alertrules', variables('alertRuleName'))]",` |
| `"/subscriptions/.../webtests/myTestName-myAppName",` |`"[resourceId('Microsoft.Insights/webtests', parameters('webTestName'))]",` |
| `"myWebTest-myAppName"` |`"[variables(testName)]"'` |
| `"myTestName-myAppName-subsId"` |`"[variables('alertRuleName')]"` |
| `"myAppName"` |`"[parameters('appName')]"` |
| <span data-ttu-id="b9952-177">`"myappname"`(kleine letters)</span><span class="sxs-lookup"><span data-stu-id="b9952-177">`"myappname"` (lower case)</span></span> |`"[toLower(parameters('appName'))]"` |
| `"<WebTest Name=\"myWebTest\" ...`<br/>` Url=\"http://fabrikam.com/home\" ...>"` |`[concat('<WebTest Name=\"',` <br/> `parameters('webTestName'),` <br/> `'\" ... Url=\"', parameters('Url'),` <br/> `'\"...>')]"`<br/><span data-ttu-id="b9952-178">Verwijderen van de Guid en -id.</span><span class="sxs-lookup"><span data-stu-id="b9952-178">Delete Guid and Id.</span></span> |

### <a name="set-dependencies-between-hello-resources"></a><span data-ttu-id="b9952-179">Set afhankelijkheden tussen resources Hallo</span><span class="sxs-lookup"><span data-stu-id="b9952-179">Set dependencies between hello resources</span></span>
<span data-ttu-id="b9952-180">Azure moet de resources in de volgorde van de strikte Hallo instellen.</span><span class="sxs-lookup"><span data-stu-id="b9952-180">Azure should set up hello resources in strict order.</span></span> <span data-ttu-id="b9952-181">toomake zeker van te zijn dat een installatie is voltooid voordat de Hallo naast begint, afhankelijkheid regels toevoegen:</span><span class="sxs-lookup"><span data-stu-id="b9952-181">toomake sure one setup completes before hello next begins, add dependency lines:</span></span>

* <span data-ttu-id="b9952-182">Test resource in Hallo beschikbaarheid:</span><span class="sxs-lookup"><span data-stu-id="b9952-182">In hello availability test resource:</span></span>
  
    `"dependsOn": ["[resourceId('Microsoft.Insights/components', parameters('appName'))]"],`
* <span data-ttu-id="b9952-183">In de waarschuwing resource Hallo voor een beschikbaarheidstest:</span><span class="sxs-lookup"><span data-stu-id="b9952-183">In hello alert resource for an availability test:</span></span>
  
    `"dependsOn": ["[resourceId('Microsoft.Insights/webtests', variables('testName'))]"],`



## <a name="next-steps"></a><span data-ttu-id="b9952-184">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b9952-184">Next steps</span></span>
<span data-ttu-id="b9952-185">Andere automation-artikelen:</span><span class="sxs-lookup"><span data-stu-id="b9952-185">Other automation articles:</span></span>

* <span data-ttu-id="b9952-186">[Een Application Insights-resource maken](app-insights-powershell-script-create-resource.md) -snelle methode zonder een sjabloon te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b9952-186">[Create an Application Insights resource](app-insights-powershell-script-create-resource.md) - quick method without using a template.</span></span>
* [<span data-ttu-id="b9952-187">Waarschuwingen instellen</span><span class="sxs-lookup"><span data-stu-id="b9952-187">Set up Alerts</span></span>](app-insights-powershell-alerts.md)
* [<span data-ttu-id="b9952-188">Webtests maken</span><span class="sxs-lookup"><span data-stu-id="b9952-188">Create web tests</span></span>](https://azure.microsoft.com/blog/creating-a-web-test-alert-programmatically-with-application-insights/)
* [<span data-ttu-id="b9952-189">Azure Diagnostics tooApplication Insights verzenden</span><span class="sxs-lookup"><span data-stu-id="b9952-189">Send Azure Diagnostics tooApplication Insights</span></span>](app-insights-powershell-azure-diagnostics.md)
* [<span data-ttu-id="b9952-190">TooAzure vanuit GitHub implementeren</span><span class="sxs-lookup"><span data-stu-id="b9952-190">Deploy tooAzure from GitHub</span></span>](http://blogs.msdn.com/b/webdev/archive/2015/09/16/deploy-to-azure-from-github-with-application-insights.aspx)
* [<span data-ttu-id="b9952-191">Release aantekeningen maken</span><span class="sxs-lookup"><span data-stu-id="b9952-191">Create release annotations</span></span>](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1)

