---
title: Azure Application Insights met PowerShell automatiseren | Microsoft Docs
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
ms.openlocfilehash: 88dbb9515300f847789bc889911cdeff5f5bdb53
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
#  <a name="create-application-insights-resources-using-powershell"></a><span data-ttu-id="1e669-103">Application Insights-resources maken met PowerShell</span><span class="sxs-lookup"><span data-stu-id="1e669-103">Create Application Insights resources using PowerShell</span></span>
<span data-ttu-id="1e669-104">Dit artikel laat zien hoe te automatiseren voor het maken en bijwerken van de [Application Insights](app-insights-overview.md) resources automatisch met behulp van Azure Resource Management.</span><span class="sxs-lookup"><span data-stu-id="1e669-104">This article shows you how to automate the creation and update of [Application Insights](app-insights-overview.md) resources automatically by using Azure Resource Management.</span></span> <span data-ttu-id="1e669-105">U kunt bijvoorbeeld doen als onderdeel van een buildproces.</span><span class="sxs-lookup"><span data-stu-id="1e669-105">You might, for example, do so as part of a build process.</span></span> <span data-ttu-id="1e669-106">Samen met de basic Application Insights-resource, kunt u [webtests voor beschikbaarheid](app-insights-monitor-web-app-availability.md)Stel [waarschuwingen](app-insights-alerts.md)stelt de [prijzen schema](app-insights-pricing.md), en andere Azure-resources te maken .</span><span class="sxs-lookup"><span data-stu-id="1e669-106">Along with the basic Application Insights resource, you can create [availability web tests](app-insights-monitor-web-app-availability.md), set up [alerts](app-insights-alerts.md), set the [pricing scheme](app-insights-pricing.md), and create other Azure resources.</span></span>

<span data-ttu-id="1e669-107">De sleutel voor het maken van deze resources is een JSON-sjablonen voor [Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="1e669-107">The key to creating these resources is JSON templates for [Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span></span> <span data-ttu-id="1e669-108">Kortom, de procedure is: downloaden van de JSON-definities van bestaande resources; parameter van bepaalde waarden zoals namen; en voer vervolgens de sjabloon wanneer u wilt maken van een nieuwe resource.</span><span class="sxs-lookup"><span data-stu-id="1e669-108">In a nutshell, the procedure is: download the JSON definitions of existing resources; parameterize certain values such as names; and then run the template whenever you want to create a new resource.</span></span> <span data-ttu-id="1e669-109">Kunt u verschillende resources samen verpakken, om ze te maken in een gaan - bijvoorbeeld een app-monitor met beschikbaarheidstests, waarschuwingen en opslag voor continue export.</span><span class="sxs-lookup"><span data-stu-id="1e669-109">You can package several resources together, to create them all in one go - for example, an app monitor with availability tests, alerts, and storage for continuous export.</span></span> <span data-ttu-id="1e669-110">Er zijn enkele eigenaardigheden tot een aantal van de parameteriseringen, wordt hier uitgelegd.</span><span class="sxs-lookup"><span data-stu-id="1e669-110">There are some subtleties to some of the parameterizations, which we'll explain here.</span></span>

## <a name="one-time-setup"></a><span data-ttu-id="1e669-111">Eenmalige instelling</span><span class="sxs-lookup"><span data-stu-id="1e669-111">One-time setup</span></span>
<span data-ttu-id="1e669-112">Als u dit nog niet hebt PowerShell met uw Azure-abonnement voordat gebruikt:</span><span class="sxs-lookup"><span data-stu-id="1e669-112">If you haven't used PowerShell with your Azure subscription before:</span></span>

<span data-ttu-id="1e669-113">De Azure Powershell-module installeren op de computer waar u de scripts worden uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="1e669-113">Install the Azure Powershell module on the machine where you want to run the scripts:</span></span>

1. <span data-ttu-id="1e669-114">Installeer [Microsoft Web Platform Installer (v5 of hoger)](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="1e669-114">Install [Microsoft Web Platform Installer (v5 or higher)](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
2. <span data-ttu-id="1e669-115">Gebruik dit voor het installeren van Microsoft Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="1e669-115">Use it to install Microsoft Azure Powershell.</span></span>

## <a name="create-an-azure-resource-manager-template"></a><span data-ttu-id="1e669-116">Een Azure Resource Manager-sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="1e669-116">Create an Azure Resource Manager template</span></span>
<span data-ttu-id="1e669-117">Maak een nieuw .json-bestand - gaan we deze aanroepen `template1.json` in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="1e669-117">Create a new .json file - let's call it `template1.json` in this example.</span></span> <span data-ttu-id="1e669-118">Kopieer deze inhoud naar het:</span><span class="sxs-lookup"><span data-stu-id="1e669-118">Copy this content into it:</span></span>

```JSON
    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "appName": {
                "type": "string",
                "metadata": {
                    "description": "Enter the application name."
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
                    "description": "Enter the application type."
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
                    "description": "Enter the application location."
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
                    "description": "Enter daily quota reset hour in UTC (0 to 23). Values outside the range will get a random reset hour."
                }
            },
            "warningThreshold": {
                "type": "int",
                "defaultValue": 90,
                "minValue": 1,
                "maxValue": 100,
                "metadata": {
                    "description": "Enter the % value of daily quota after which warning mail to be sent. "
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



## <a name="create-application-insights-resources"></a><span data-ttu-id="1e669-119">Application Insights-resources maken</span><span class="sxs-lookup"><span data-stu-id="1e669-119">Create Application Insights resources</span></span>
1. <span data-ttu-id="1e669-120">In PowerShell, moet u zich aanmelden bij Azure:</span><span class="sxs-lookup"><span data-stu-id="1e669-120">In PowerShell, sign in to Azure:</span></span>
   
    `Login-AzureRmAccount`
2. <span data-ttu-id="1e669-121">Voer een opdracht als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="1e669-121">Run a command like this:</span></span>
   
    ```PS
   
        New-AzureRmResourceGroupDeployment -ResourceGroupName Fabrikam `
               -TemplateFile .\template1.json `
               -appName myNewApp

    ``` 
   
   * <span data-ttu-id="1e669-122">`-ResourceGroupName`is de groep waar u wilt maken van de nieuwe resources.</span><span class="sxs-lookup"><span data-stu-id="1e669-122">`-ResourceGroupName` is the group where you want to create the new resources.</span></span>
   * <span data-ttu-id="1e669-123">`-TemplateFile`Er moeten plaatsvinden voordat de aangepaste parameters.</span><span class="sxs-lookup"><span data-stu-id="1e669-123">`-TemplateFile` must occur before the custom parameters.</span></span>
   * <span data-ttu-id="1e669-124">`-appName`De naam van de resource te maken.</span><span class="sxs-lookup"><span data-stu-id="1e669-124">`-appName` The name of the resource to create.</span></span>

<span data-ttu-id="1e669-125">U kunt andere parameters toevoegen - bijbehorende beschrijvingen vindt in het gedeelte parameters van de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="1e669-125">You can add other parameters - you'll find their descriptions in the parameters section of the template.</span></span>

## <a name="to-get-the-instrumentation-key"></a><span data-ttu-id="1e669-126">De instrumentatiesleutel ophalen</span><span class="sxs-lookup"><span data-stu-id="1e669-126">To get the instrumentation key</span></span>
<span data-ttu-id="1e669-127">Na het maken van de bron van een toepassing, moet u de instrumentatiesleutel:</span><span class="sxs-lookup"><span data-stu-id="1e669-127">After creating an application resource, you'll want the instrumentation key:</span></span> 

```PS
    $resource = Find-AzureRmResource -ResourceNameEquals "<YOUR APP NAME>" -ResourceType "Microsoft.Insights/components"
    $details = Get-AzureRmResource -ResourceId $resource.ResourceId
    $ikey = $details.Properties.InstrumentationKey
```


<a id="price"></a>
## <a name="set-the-price-plan"></a><span data-ttu-id="1e669-128">De prijs planning instellen</span><span class="sxs-lookup"><span data-stu-id="1e669-128">Set the price plan</span></span>

<span data-ttu-id="1e669-129">U kunt instellen de [prijs plan](app-insights-pricing.md).</span><span class="sxs-lookup"><span data-stu-id="1e669-129">You can set the [price plan](app-insights-pricing.md).</span></span>

<span data-ttu-id="1e669-130">Een resource-app maken met het Enterprise prijs plan, met de bovenstaande sjabloon:</span><span class="sxs-lookup"><span data-stu-id="1e669-130">To create an app resource with the Enterprise price plan, using the template above:</span></span>

```PS
        New-AzureRmResourceGroupDeployment -ResourceGroupName Fabrikam `
               -TemplateFile .\template1.json `
               -priceCode 2 `
               -appName myNewApp
```

|<span data-ttu-id="1e669-131">priceCode</span><span class="sxs-lookup"><span data-stu-id="1e669-131">priceCode</span></span>|<span data-ttu-id="1e669-132">Plannen</span><span class="sxs-lookup"><span data-stu-id="1e669-132">plan</span></span>|
|---|---|
|<span data-ttu-id="1e669-133">1</span><span class="sxs-lookup"><span data-stu-id="1e669-133">1</span></span>|<span data-ttu-id="1e669-134">Basic</span><span class="sxs-lookup"><span data-stu-id="1e669-134">Basic</span></span>|
|<span data-ttu-id="1e669-135">2</span><span class="sxs-lookup"><span data-stu-id="1e669-135">2</span></span>|<span data-ttu-id="1e669-136">Enterprise</span><span class="sxs-lookup"><span data-stu-id="1e669-136">Enterprise</span></span>|

* <span data-ttu-id="1e669-137">Als u alleen het standaardabonnement basisprijs gebruiken wilt, kunt u de resource CurrentBillingFeatures van de sjabloon weglaten.</span><span class="sxs-lookup"><span data-stu-id="1e669-137">If you only want to use the default Basic price plan, you can omit the CurrentBillingFeatures resource from the template.</span></span>
* <span data-ttu-id="1e669-138">Als u het plan prijs wijzigen wilt nadat de onderdeel-resource is gemaakt, kunt u een sjabloon die de resource 'microsoft.insights/components' wordt weggelaten.</span><span class="sxs-lookup"><span data-stu-id="1e669-138">If you want to change the price plan after the component resource has been created, you can use a template that omits the "microsoft.insights/components" resource.</span></span> <span data-ttu-id="1e669-139">Laat ook de `dependsOn` knooppunt uit de facturering resource.</span><span class="sxs-lookup"><span data-stu-id="1e669-139">Also, omit the `dependsOn` node from the billing resource.</span></span> 

<span data-ttu-id="1e669-140">Kijken om te controleren of het plan bijgewerkte prijs, de 'Functies + prijzen' blade in de browser.</span><span class="sxs-lookup"><span data-stu-id="1e669-140">To verify the updated price plan, look at the "Features+pricing" blade in the browser.</span></span> <span data-ttu-id="1e669-141">**Vernieuw de browserweergave** om ervoor te zorgen dat u de meest recente toestand zien.</span><span class="sxs-lookup"><span data-stu-id="1e669-141">**Refresh the browser view** to make sure you see the latest state.</span></span>



## <a name="add-a-metric-alert"></a><span data-ttu-id="1e669-142">Waarschuwing voor een metrische toevoegen</span><span class="sxs-lookup"><span data-stu-id="1e669-142">Add a metric alert</span></span>

<span data-ttu-id="1e669-143">Als u een waarschuwing voor metrische instelt op hetzelfde moment als uw app-resource, het sjabloonbestand samenvoegen code als volgt:</span><span class="sxs-lookup"><span data-stu-id="1e669-143">To set up a metric alert at the same time as your app resource, merge code like this into the template file:</span></span>

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
      // Ensure this resource is created after the app resource:
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

<span data-ttu-id="1e669-144">Als u de sjabloon aanroept, kunt u eventueel deze parameter toevoegen:</span><span class="sxs-lookup"><span data-stu-id="1e669-144">When you invoke the template, you can optionally add this parameter:</span></span>

    `-responseTime 2`

<span data-ttu-id="1e669-145">U kunt uiteraard parameter van andere velden.</span><span class="sxs-lookup"><span data-stu-id="1e669-145">You can of course parameterize other fields.</span></span> 

<span data-ttu-id="1e669-146">Voor meer informatie over de namen en configuratie-informatie van andere regels voor waarschuwingen, maakt u handmatig een regel en vervolgens controleren in [Azure Resource Manager](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1e669-146">To find out the type names and configuration details of other alert rules, create a rule manually and then inspect it in [Azure Resource Manager](https://resources.azure.com/).</span></span> 


## <a name="add-an-availability-test"></a><span data-ttu-id="1e669-147">Een beschikbaarheidstest toevoegen</span><span class="sxs-lookup"><span data-stu-id="1e669-147">Add an availability test</span></span>

<span data-ttu-id="1e669-148">In dit voorbeeld is voor een ping-test (voor het testen van één pagina).</span><span class="sxs-lookup"><span data-stu-id="1e669-148">This example is for a ping test (to test a single page).</span></span>  

<span data-ttu-id="1e669-149">**Er zijn twee delen** in een beschikbaarheidstest: de test zelf en de waarschuwing die een melding van fouten.</span><span class="sxs-lookup"><span data-stu-id="1e669-149">**There are two parts** in an availability test: the test itself, and the alert that notifies you of failures.</span></span>

<span data-ttu-id="1e669-150">Samenvoegen met de volgende code in de sjabloonbestand dat de app maakt.</span><span class="sxs-lookup"><span data-stu-id="1e669-150">Merge the following code into the template file that creates the app.</span></span>

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
      // Availability test: part 1 configures the test
      //
      "name": "[variables('pingTestName')]",
      "type": "Microsoft.Insights/webtests",
      "apiVersion": "2014-04-01",
      "location": "[parameters('appLocation')]",
      // Ensure this is created after the app resource:
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
          "WebTest": "[concat('<WebTest   Name=\"', variables('pingTestName'), '\"   Enabled=\"True\"         CssProjectStructure=\"\"    CssIteration=\"\"  Timeout=\"120\"  WorkItemIds=\"\"         xmlns=\"http://microsoft.com/schemas/VisualStudio/TeamTest/2010\"         Description=\"\"  CredentialUserName=\"\"  CredentialPassword=\"\"         PreAuthenticate=\"True\"  Proxy=\"default\"  StopOnError=\"False\"         RecordedResultFile=\"\"  ResultsLocale=\"\">  <Items>  <Request Method=\"GET\"    Version=\"1.1\"  Url=\"', parameters('Url'),   '\" ThinkTime=\"0\"  Timeout=\"300\" ParseDependentRequests=\"True\"         FollowRedirects=\"True\" RecordResult=\"True\" Cache=\"False\"         ResponseTimeGoal=\"0\"  Encoding=\"utf-8\"  ExpectedHttpStatusCode=\"200\"         ExpectedResponseUrl=\"\" ReportingName=\"\" IgnoreHttpStatusCode=\"False\" />        </Items>  <ValidationRules> <ValidationRule  Classname=\"Microsoft.VisualStudio.TestTools.WebTesting.Rules.ValidationRuleFindText, Microsoft.VisualStudio.QualityTools.WebTestFramework, Version=10.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a\" DisplayName=\"Find Text\"         Description=\"Verifies the existence of the specified text in the response.\"         Level=\"High\"  ExectuionOrder=\"BeforeDependents\">  <RuleParameters>        <RuleParameter Name=\"FindText\" Value=\"',   parameters('pingText'), '\" />  <RuleParameter Name=\"IgnoreCase\" Value=\"False\" />  <RuleParameter Name=\"UseRegularExpression\" Value=\"False\" />  <RuleParameter Name=\"PassIfTextFound\" Value=\"True\" />  </RuleParameters> </ValidationRule>  </ValidationRules>  </WebTest>')]"
        },
        "SyntheticMonitorId": "[variables('pingTestName')]"
      }
    },

    {
      //
      // Availability test: part 2, the alert rule
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

<span data-ttu-id="1e669-151">Voor het detecteren van de codes voor andere testlocaties of het maken van een complexere webtests automatiseren handmatig maken van een voorbeeld en vervolgens de code van de parameter [Azure Resource Manager](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1e669-151">To discover the codes for other test locations, or to automate the creation of more complex web tests, create an example manually and then parameterize the code from [Azure Resource Manager](https://resources.azure.com/).</span></span>

## <a name="add-more-resources"></a><span data-ttu-id="1e669-152">Voeg meer resources toe</span><span class="sxs-lookup"><span data-stu-id="1e669-152">Add more resources</span></span>

<span data-ttu-id="1e669-153">Voor het automatiseren van het maken van een andere bron enige vorm van een voorbeeld handmatig maken en kopieert en voorzien van de code van [Azure Resource Manager](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1e669-153">To automate the creation of any other resource of any kind, create an example manually, and then copy and parameterize its code from [Azure Resource Manager](https://resources.azure.com/).</span></span> 

1. <span data-ttu-id="1e669-154">Open [Azure Resource Manager](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1e669-154">Open [Azure Resource Manager](https://resources.azure.com/).</span></span> <span data-ttu-id="1e669-155">Navigeren naar beneden `subscriptions/resourceGroups/<your resource group>/providers/Microsoft.Insights/components`, de bron van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="1e669-155">Navigate down through `subscriptions/resourceGroups/<your resource group>/providers/Microsoft.Insights/components`, to your application resource.</span></span> 
   
    ![Navigatie in de Azure-Resource Explorer](./media/app-insights-powershell/01.png)
   
    <span data-ttu-id="1e669-157">*Onderdelen* zijn de basic Application Insights-resources voor het weergeven van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="1e669-157">*Components* are the basic Application Insights resources for displaying applications.</span></span> <span data-ttu-id="1e669-158">Er zijn afzonderlijke bronnen voor de gekoppelde waarschuwingsregels en webtests voor beschikbaarheid.</span><span class="sxs-lookup"><span data-stu-id="1e669-158">There are separate resources for the associated alert rules and availability web tests.</span></span>
2. <span data-ttu-id="1e669-159">De JSON van het onderdeel kopiëren naar de juiste plaats in `template1.json`.</span><span class="sxs-lookup"><span data-stu-id="1e669-159">Copy the JSON of the component into the appropriate place in `template1.json`.</span></span>
3. <span data-ttu-id="1e669-160">Verwijder deze eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="1e669-160">Delete these properties:</span></span>
   
   * `id`
   * `InstrumentationKey`
   * `CreationDate`
   * `TenantId`
4. <span data-ttu-id="1e669-161">Open de secties webtests en alertrules en kopieert u de JSON voor afzonderlijke items in de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="1e669-161">Open the webtests and alertrules sections and copy the JSON for individual items into your template.</span></span> <span data-ttu-id="1e669-162">(Van de knooppunten webtests of alertrules niet kopiëren: Ga naar de items eronder.)</span><span class="sxs-lookup"><span data-stu-id="1e669-162">(Don't copy from the webtests or alertrules nodes: go into the items under them.)</span></span>
   
    <span data-ttu-id="1e669-163">Elke WebTest heeft een bijbehorende waarschuwingsregel, zodat u hoeft te kopiëren van beide.</span><span class="sxs-lookup"><span data-stu-id="1e669-163">Each web test has an associated alert rule, so you have to copy both of them.</span></span>
   
    <span data-ttu-id="1e669-164">U kunt ook waarschuwingen op metrische gegevens opnemen.</span><span class="sxs-lookup"><span data-stu-id="1e669-164">You can also include alerts on metrics.</span></span> <span data-ttu-id="1e669-165">[De namen van de metrische](app-insights-powershell-alerts.md#metric-names).</span><span class="sxs-lookup"><span data-stu-id="1e669-165">[Metric names](app-insights-powershell-alerts.md#metric-names).</span></span>
5. <span data-ttu-id="1e669-166">Deze regel invoegen in elke resource:</span><span class="sxs-lookup"><span data-stu-id="1e669-166">Insert this line in each resource:</span></span>
   
    `"apiVersion": "2015-05-01",`

### <a name="parameterize-the-template"></a><span data-ttu-id="1e669-167">Parameter van de sjabloon</span><span class="sxs-lookup"><span data-stu-id="1e669-167">Parameterize the template</span></span>
<span data-ttu-id="1e669-168">U hebt nu vervangen door de namen van de specifieke parameters.</span><span class="sxs-lookup"><span data-stu-id="1e669-168">Now you have to replace the specific names with parameters.</span></span> <span data-ttu-id="1e669-169">Naar [voorzien van een sjabloon](../azure-resource-manager/resource-group-authoring-templates.md), schrijven van expressies met een [reeks hulpfuncties](../azure-resource-manager/resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="1e669-169">To [parameterize a template](../azure-resource-manager/resource-group-authoring-templates.md), you write expressions using a [set of helper functions](../azure-resource-manager/resource-group-template-functions.md).</span></span> 

<span data-ttu-id="1e669-170">Kunnen niet worden voorzien van slechts een deel van een tekenreeks, dus gebruik `concat()` om tekenreeksen samen te stellen.</span><span class="sxs-lookup"><span data-stu-id="1e669-170">You can't parameterize just part of a string, so use `concat()` to build strings.</span></span>

<span data-ttu-id="1e669-171">Hier volgen enkele voorbeelden van de die u wilt maken.</span><span class="sxs-lookup"><span data-stu-id="1e669-171">Here are examples of the substitutions you'll want to make.</span></span> <span data-ttu-id="1e669-172">Er zijn meerdere exemplaren van elke vervanging.</span><span class="sxs-lookup"><span data-stu-id="1e669-172">There are several occurrences of each substitution.</span></span> <span data-ttu-id="1e669-173">Mogelijk moet u anderen in uw sjabloon.</span><span class="sxs-lookup"><span data-stu-id="1e669-173">You might need others in your template.</span></span> <span data-ttu-id="1e669-174">Deze voorbeelden worden de parameters en variabelen die we gedefinieerd aan de bovenkant van de sjabloon gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1e669-174">These examples use the parameters and variables we defined at the top of the template.</span></span>

| <span data-ttu-id="1e669-175">zoeken</span><span class="sxs-lookup"><span data-stu-id="1e669-175">find</span></span> | <span data-ttu-id="1e669-176">vervangen</span><span class="sxs-lookup"><span data-stu-id="1e669-176">replace with</span></span> |
| --- | --- |
| `"hidden-link:/subscriptions/.../components/MyAppName"` |`"[concat('hidden-link:',`<br/>` resourceId('microsoft.insights/components',` <br/> ` parameters('appName')))]"` |
| `"/subscriptions/.../alertrules/myAlertName-myAppName-subsId",` |`"[resourceId('Microsoft.Insights/alertrules', variables('alertRuleName'))]",` |
| `"/subscriptions/.../webtests/myTestName-myAppName",` |`"[resourceId('Microsoft.Insights/webtests', parameters('webTestName'))]",` |
| `"myWebTest-myAppName"` |`"[variables(testName)]"'` |
| `"myTestName-myAppName-subsId"` |`"[variables('alertRuleName')]"` |
| `"myAppName"` |`"[parameters('appName')]"` |
| <span data-ttu-id="1e669-177">`"myappname"`(kleine letters)</span><span class="sxs-lookup"><span data-stu-id="1e669-177">`"myappname"` (lower case)</span></span> |`"[toLower(parameters('appName'))]"` |
| `"<WebTest Name=\"myWebTest\" ...`<br/>` Url=\"http://fabrikam.com/home\" ...>"` |`[concat('<WebTest Name=\"',` <br/> `parameters('webTestName'),` <br/> `'\" ... Url=\"', parameters('Url'),` <br/> `'\"...>')]"`<br/><span data-ttu-id="1e669-178">Verwijderen van de Guid en -id.</span><span class="sxs-lookup"><span data-stu-id="1e669-178">Delete Guid and Id.</span></span> |

### <a name="set-dependencies-between-the-resources"></a><span data-ttu-id="1e669-179">Set afhankelijkheden tussen resources</span><span class="sxs-lookup"><span data-stu-id="1e669-179">Set dependencies between the resources</span></span>
<span data-ttu-id="1e669-180">Azure moet de resources in strikte volgorde instellen.</span><span class="sxs-lookup"><span data-stu-id="1e669-180">Azure should set up the resources in strict order.</span></span> <span data-ttu-id="1e669-181">Om te zorgen dat een installatie is voltooid voordat de volgende begint, moet u afhankelijkheid regels toevoegen:</span><span class="sxs-lookup"><span data-stu-id="1e669-181">To make sure one setup completes before the next begins, add dependency lines:</span></span>

* <span data-ttu-id="1e669-182">Test in de beschikbaarheid van de resource:</span><span class="sxs-lookup"><span data-stu-id="1e669-182">In the availability test resource:</span></span>
  
    `"dependsOn": ["[resourceId('Microsoft.Insights/components', parameters('appName'))]"],`
* <span data-ttu-id="1e669-183">In de waarschuwing voor een beschikbaarheidstest:</span><span class="sxs-lookup"><span data-stu-id="1e669-183">In the alert resource for an availability test:</span></span>
  
    `"dependsOn": ["[resourceId('Microsoft.Insights/webtests', variables('testName'))]"],`



## <a name="next-steps"></a><span data-ttu-id="1e669-184">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1e669-184">Next steps</span></span>
<span data-ttu-id="1e669-185">Andere automation-artikelen:</span><span class="sxs-lookup"><span data-stu-id="1e669-185">Other automation articles:</span></span>

* <span data-ttu-id="1e669-186">[Een Application Insights-resource maken](app-insights-powershell-script-create-resource.md) -snelle methode zonder een sjabloon te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1e669-186">[Create an Application Insights resource](app-insights-powershell-script-create-resource.md) - quick method without using a template.</span></span>
* [<span data-ttu-id="1e669-187">Waarschuwingen instellen</span><span class="sxs-lookup"><span data-stu-id="1e669-187">Set up Alerts</span></span>](app-insights-powershell-alerts.md)
* [<span data-ttu-id="1e669-188">Webtests maken</span><span class="sxs-lookup"><span data-stu-id="1e669-188">Create web tests</span></span>](https://azure.microsoft.com/blog/creating-a-web-test-alert-programmatically-with-application-insights/)
* [<span data-ttu-id="1e669-189">Diagnostische Azure-gegevens verzenden naar Application Insights</span><span class="sxs-lookup"><span data-stu-id="1e669-189">Send Azure Diagnostics to Application Insights</span></span>](app-insights-powershell-azure-diagnostics.md)
* [<span data-ttu-id="1e669-190">Implementeren in Azure vanuit GitHub</span><span class="sxs-lookup"><span data-stu-id="1e669-190">Deploy to Azure from GitHub</span></span>](http://blogs.msdn.com/b/webdev/archive/2015/09/16/deploy-to-azure-from-github-with-application-insights.aspx)
* [<span data-ttu-id="1e669-191">Release aantekeningen maken</span><span class="sxs-lookup"><span data-stu-id="1e669-191">Create release annotations</span></span>](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1)

