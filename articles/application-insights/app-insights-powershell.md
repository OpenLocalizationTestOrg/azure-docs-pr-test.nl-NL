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
#  <a name="create-application-insights-resources-using-powershell"></a>Application Insights-resources maken met PowerShell
Dit artikel laat zien hoe tooautomate Hallo maken en bijwerken van de [Application Insights](app-insights-overview.md) resources automatisch met behulp van Azure Resource Management. U kunt bijvoorbeeld doen als onderdeel van een buildproces. Samen met de Hallo basic Application Insights-resource, kunt u [webtests voor beschikbaarheid](app-insights-monitor-web-app-availability.md)Stel [waarschuwingen](app-insights-alerts.md)stelt hello [prijzen schema](app-insights-pricing.md), en andere Azure maken bronnen.

Hallo sleutel toocreating deze resources is een JSON-sjablonen voor [Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md). Kortom, Hallo procedure is: Hallo JSON definities van bestaande resources; downloaden parameter van bepaalde waarden zoals namen; en voer vervolgens de sjabloon Hallo gewenst toocreate een nieuwe resource. U kunt verschillende resources samen, toocreate die ze in een Ga - bijvoorbeeld, een app-monitor met beschikbaarheidstests, waarschuwingen en opslag voor continue export van het pakket. Er zijn enkele toosome eigenaardigheden van Hallo parameteriseringen, die wordt hier uitgelegd.

## <a name="one-time-setup"></a>Eenmalige instelling
Als u dit nog niet hebt PowerShell met uw Azure-abonnement voordat gebruikt:

Hello Azure Powershell-module installeren op Hallo machine waar u toorun Hallo scripts:

1. Installeer [Microsoft Web Platform Installer (v5 of hoger)](http://www.microsoft.com/web/downloads/platform.aspx).
2. Deze tooinstall Microsoft Azure Powershell gebruiken.

## <a name="create-an-azure-resource-manager-template"></a>Een Azure Resource Manager-sjabloon maken
Maak een nieuw .json-bestand - gaan we deze aanroepen `template1.json` in dit voorbeeld. Kopieer deze inhoud naar het:

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



## <a name="create-application-insights-resources"></a>Application Insights-resources maken
1. Aanmelden tooAzure in PowerShell:
   
    `Login-AzureRmAccount`
2. Voer een opdracht als volgt uit:
   
    ```PS
   
        New-AzureRmResourceGroupDeployment -ResourceGroupName Fabrikam `
               -TemplateFile .\template1.json `
               -appName myNewApp

    ``` 
   
   * `-ResourceGroupName`Hallo-groep is waar u toocreate Hallo nieuwe resources.
   * `-TemplateFile`Er moeten plaatsvinden voordat Hallo aangepaste parameters.
   * `-appName`Hallo-naam van Hallo resource toocreate.

U kunt andere parameters toevoegen - vindt u bijbehorende beschrijvingen in de sectie van de parameters Hallo van Hallo-sjabloon.

## <a name="tooget-hello-instrumentation-key"></a>tooget hello instrumentatiesleutel
Na het maken van de bron van een toepassing, moet u de instrumentatiesleutel Hallo: 

```PS
    $resource = Find-AzureRmResource -ResourceNameEquals "<YOUR APP NAME>" -ResourceType "Microsoft.Insights/components"
    $details = Get-AzureRmResource -ResourceId $resource.ResourceId
    $ikey = $details.Properties.InstrumentationKey
```


<a id="price"></a>
## <a name="set-hello-price-plan"></a>Set Hallo prijs plannen

U kunt instellen Hallo [prijs plan](app-insights-pricing.md).

een app-resource met Hallo Enterprise prijs plan, met behulp van Hallo sjabloon bovenstaande toocreate:

```PS
        New-AzureRmResourceGroupDeployment -ResourceGroupName Fabrikam `
               -TemplateFile .\template1.json `
               -priceCode 2 `
               -appName myNewApp
```

|priceCode|Plannen|
|---|---|
|1|Basic|
|2|Enterprise|

* Als u alleen toouse Hallo standaardplan basisprijs wilt, kunt u Hallo CurrentBillingFeatures resource van de sjabloon Hallo weglaten.
* Als u toochange Hallo prijs plan wilt nadat Hallo onderdeel resource is gemaakt, kunt u een sjabloon die worden weggelaten Hallo 'microsoft.insights/components' resource. Bovendien weglaten Hallo `dependsOn` knooppunt uit Hallo resource facturering. 

tooverify Hallo bijgewerkte prijs plan, bekijkt hello 'Functies + prijzen' blade in Hallo browser. **Vernieuw de weergave van de browser Hallo** toomake zeker dat u de meest recente toestand Hallo zien.



## <a name="add-a-metric-alert"></a>Waarschuwing voor een metrische toevoegen

tooset van een waarschuwing voor metrische bij Hallo dezelfde tijd als uw app-resource, merge-code als volgt naar het sjabloonbestand Hallo:

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

Als u de sjabloon Hallo aanroept, kunt u eventueel deze parameter toevoegen:

    `-responseTime 2`

U kunt uiteraard parameter van andere velden. 

toofind uit Hallo namen en configuratie-informatie van andere waarschuwingsregels handmatig maken van een regel en vervolgens controleren in [Azure Resource Manager](https://resources.azure.com/). 


## <a name="add-an-availability-test"></a>Een beschikbaarheidstest toevoegen

In dit voorbeeld is voor een Pingtest (tootest één pagina).  

**Er zijn twee delen** in een beschikbaarheidstest: Hallo test zelf en Hallo waarschuwing die een melding van fouten.

Samenvoegen Hallo na de code in Hallo sjabloonbestand die Hallo-app maakt.

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

toodiscover hello codes voor andere testlocaties of tooautomate Hallo maken van een complexere webtests, een voorbeeld handmatig maken en vervolgens voorzien Hallo code uit [Azure Resource Manager](https://resources.azure.com/).

## <a name="add-more-resources"></a>Voeg meer resources toe

tooautomate hello maken van een andere bron van welke aard handmatig maken van een voorbeeld en kopieert en voorzien van de code van [Azure Resource Manager](https://resources.azure.com/). 

1. Open [Azure Resource Manager](https://resources.azure.com/). Navigeren naar beneden `subscriptions/resourceGroups/<your resource group>/providers/Microsoft.Insights/components`, tooyour toepassingsbron. 
   
    ![Navigatie in de Azure-Resource Explorer](./media/app-insights-powershell/01.png)
   
    *Onderdelen* zijn Hallo basic Application Insights-resources voor het weergeven van toepassingen. Er zijn afzonderlijke bronnen voor Hallo waarschuwingsregels en webtests voor beschikbaarheid gekoppelde.
2. Kopiëren Hallo JSON van het onderdeel in de juiste plaats Hallo Hallo in `template1.json`.
3. Verwijder deze eigenschappen:
   
   * `id`
   * `InstrumentationKey`
   * `CreationDate`
   * `TenantId`
4. Hallo webtests en alertrules secties openen en kopieer Hallo JSON voor afzonderlijke items in de sjabloon. (Vanaf Hallo webtests of alertrules-knooppunten niet kopiëren: Ga naar de items onder deze Hallo.)
   
    Elke WebTest heeft een bijbehorende waarschuwingsregel, zodat u toocopy hiervan hebt.
   
    U kunt ook waarschuwingen op metrische gegevens opnemen. [De namen van de metrische](app-insights-powershell-alerts.md#metric-names).
5. Deze regel invoegen in elke resource:
   
    `"apiVersion": "2015-05-01",`

### <a name="parameterize-hello-template"></a>Hallo sjabloon voorzien
U hebt nu tooreplace Hallo specifieke namen met parameters. te[voorzien van een sjabloon](../azure-resource-manager/resource-group-authoring-templates.md), schrijven van expressies met een [reeks hulpfuncties](../azure-resource-manager/resource-group-template-functions.md). 

Kunnen niet worden voorzien van slechts een deel van een tekenreeks, dus gebruik `concat()` toobuild tekenreeksen.

Hier volgen voorbeelden van Hallo vervangingen moet u toomake. Er zijn meerdere exemplaren van elke vervanging. Mogelijk moet u anderen in uw sjabloon. Deze voorbeelden gebruiken Hallo-parameters en variabelen die we gedefinieerd Hallo boven aan het Hallo-sjabloon.

| zoeken | vervangen |
| --- | --- |
| `"hidden-link:/subscriptions/.../components/MyAppName"` |`"[concat('hidden-link:',`<br/>` resourceId('microsoft.insights/components',` <br/> ` parameters('appName')))]"` |
| `"/subscriptions/.../alertrules/myAlertName-myAppName-subsId",` |`"[resourceId('Microsoft.Insights/alertrules', variables('alertRuleName'))]",` |
| `"/subscriptions/.../webtests/myTestName-myAppName",` |`"[resourceId('Microsoft.Insights/webtests', parameters('webTestName'))]",` |
| `"myWebTest-myAppName"` |`"[variables(testName)]"'` |
| `"myTestName-myAppName-subsId"` |`"[variables('alertRuleName')]"` |
| `"myAppName"` |`"[parameters('appName')]"` |
| `"myappname"`(kleine letters) |`"[toLower(parameters('appName'))]"` |
| `"<WebTest Name=\"myWebTest\" ...`<br/>` Url=\"http://fabrikam.com/home\" ...>"` |`[concat('<WebTest Name=\"',` <br/> `parameters('webTestName'),` <br/> `'\" ... Url=\"', parameters('Url'),` <br/> `'\"...>')]"`<br/>Verwijderen van de Guid en -id. |

### <a name="set-dependencies-between-hello-resources"></a>Set afhankelijkheden tussen resources Hallo
Azure moet de resources in de volgorde van de strikte Hallo instellen. toomake zeker van te zijn dat een installatie is voltooid voordat de Hallo naast begint, afhankelijkheid regels toevoegen:

* Test resource in Hallo beschikbaarheid:
  
    `"dependsOn": ["[resourceId('Microsoft.Insights/components', parameters('appName'))]"],`
* In de waarschuwing resource Hallo voor een beschikbaarheidstest:
  
    `"dependsOn": ["[resourceId('Microsoft.Insights/webtests', variables('testName'))]"],`



## <a name="next-steps"></a>Volgende stappen
Andere automation-artikelen:

* [Een Application Insights-resource maken](app-insights-powershell-script-create-resource.md) -snelle methode zonder een sjabloon te gebruiken.
* [Waarschuwingen instellen](app-insights-powershell-alerts.md)
* [Webtests maken](https://azure.microsoft.com/blog/creating-a-web-test-alert-programmatically-with-application-insights/)
* [Azure Diagnostics tooApplication Insights verzenden](app-insights-powershell-azure-diagnostics.md)
* [TooAzure vanuit GitHub implementeren](http://blogs.msdn.com/b/webdev/archive/2015/09/16/deploy-to-azure-from-github-with-application-insights.aspx)
* [Release aantekeningen maken](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1)

