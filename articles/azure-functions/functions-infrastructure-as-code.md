---
title: aaaAutomate resources implementeren voor een functie-app in Azure Functions | Microsoft Docs
description: "Meer informatie over hoe toobuild een Azure Resource Manager-sjabloon die de functie-app wordt geïmplementeerd."
services: Functions
documtationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: Azure functions, functies, zonder server architectuur, infrastructuur als code, azure resourcemanager
ms.assetid: d20743e3-aab6-442c-a836-9bcea09bfd32
ms.server: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/25/2017
ms.author: glenga
ms.openlocfilehash: b0df0d4ef9fe93213f7b1cb1d1e6b4e14f8b3a30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="automate-resource-deployment-for-your-function-app-in-azure-functions"></a>Implementatie van de resource voor de functie-app in Azure Functions automatiseren

U kunt een Azure Resource Manager-sjabloon toodeploy een functie-app gebruiken. In dit artikel bevat een overzicht van Hallo vereiste resources en parameters voor doet. Mogelijk moet u aanvullende bronnen voor toodeploy, afhankelijk van Hallo [triggers en bindingen](functions-triggers-bindings.md) in uw app functie.

Zie voor meer informatie over het maken van sjablonen [Azure Resource Manager-sjablonen samenstellen](../azure-resource-manager/resource-group-authoring-templates.md).

Zie voor een voorbeeldsjablonen:
- [functie-app van verbruik plan]
- [functie-app in Azure App Service-plan]

## <a name="required-resources"></a>Vereiste resources

Een functie-app is vereist voor deze resources:

* Een [Azure Storage](../storage/index.md) account
* Een hosting-indeling (verbruik plan of App Service-abonnement)
* Een functie-app 

### <a name="storage-account"></a>Storage-account

Een Azure storage-account is vereist voor een functie-app. U moet een account voor algemene doeleinden die ondersteuning biedt voor blobs, tabellen, wachtrijen en -bestanden. Zie voor meer informatie [-account voor Azure Functions opslagvereisten](functions-create-function-app-portal.md#storage-account-requirements).

```json
{
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2015-06-15",
    "location": "[resourceGroup().location]",
    "properties": {
        "accountType": "[parameters('storageAccountType')]"
    }
}
```

Bovendien Hallo eigenschappen `AzureWebJobsStorage` en `AzureWebJobsDashboard` moet worden opgegeven als de app-instellingen in Hallo site-configuratie. Hallo maakt gebruik van Azure Functions-runtime Hallo `AzureWebJobsStorage` connection string toocreate interne wachtrijen. Hallo verbindingsreeks `AzureWebJobsDashboard` gebruikte toolog tooAzure Table-opslag- en stroomkabels Hallo is **Monitor** tabblad in Hallo-portal.

Deze eigenschappen in opgegeven Hallo `appSettings` verzameling in hello `siteConfig` object:

```json
"appSettings": [
    {
        "name": "AzureWebJobsStorage",
        "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
    },
    {
        "name": "AzureWebJobsDashboard",
        "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
    }
```    

### <a name="hosting-plan"></a>Hosting-plan

Hallo-definitie van Hallo die als host fungeert voor plan varieert, afhankelijk van of u een verbruik of App Service-abonnement gebruiken. Zie [implementeren van een functie-app op Hallo verbruik plan](#consumption) en [implementeren van een functie-app op Hallo App Service-abonnement](#app-service-plan).

### <a name="function-app"></a>Functie-app

Hallo functie app-resource is gedefinieerd met behulp van een bron van het type **Microsoft.Web/Site** en type **functionapp**:

```json
{
    "apiVersion": "2015-08-01",
    "type": "Microsoft.Web/sites",
    "name": "[variables('functionAppName')]",
    "location": "[resourceGroup().location]",
    "kind": "functionapp",            
    "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
        "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]"
    ]
```

<a name="consumption"></a>

## <a name="deploy-a-function-app-on-hello-consumption-plan"></a>Een functie-app op Hallo verbruik plan implementeren

U kunt een functie-app uitvoeren in twee verschillende modi: Hallo verbruik plannings- en Hallo App Service-abonnement. rekencapaciteit Hallo verbruik plan automatisch toegewezen wanneer uw code wordt uitgevoerd, als de belasting van de benodigde toohandle uitgeschaald en vervolgens omlaag geschaald wanneer de code wordt niet uitgevoerd. Dus u hebt geen toopay voor niet-actieve virtuele machines en u niet van tevoren tooreserve capaciteit hebt. toolearn meer informatie over hostingplannen, Zie [Azure Functions gebruiks- en App Service-plannen](functions-scale.md).

Zie voor een Azure Resource Manager voorbeeldsjabloon [functie-app van verbruik plan].

### <a name="create-a-consumption-plan"></a>Maak een plan verbruik

Een plan verbruik is een speciaal type resource 'serverfarm'. U het opgeeft met behulp van Hallo `Dynamic` waarde voor Hallo `computeMode` en `sku` eigenschappen:

```json
{
    "type": "Microsoft.Web/serverfarms",
    "apiVersion": "2015-04-01",
    "name": "[variables('hostingPlanName')]",
    "location": "[resourceGroup().location]",
    "properties": {
        "name": "[variables('hostingPlanName')]",
        "computeMode": "Dynamic",
        "sku": "Dynamic"
    }
}
```

### <a name="create-a-function-app"></a>Een functie-app maken

Bovendien een plan verbruik vereist twee extra instellingen van siteconfiguratie Hallo: `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` en `WEBSITE_CONTENTSHARE`. Deze eigenschappen configureren Hallo storage-account en het bestandspad waar Hallo functie app-code en configuratie zijn opgeslagen.

```json
{
    "apiVersion": "2015-08-01",
    "type": "Microsoft.Web/sites",
    "name": "[variables('functionAppName')]",
    "location": "[resourceGroup().location]",
    "kind": "functionapp",            
    "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
        "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]"
    ],
    "properties": {
        "serverFarmId": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
        "siteConfig": {
            "appSettings": [
                {
                    "name": "AzureWebJobsDashboard",
                    "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
                },
                {
                    "name": "AzureWebJobsStorage",
                    "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
                },
                {
                    "name": "WEBSITE_CONTENTAZUREFILECONNECTIONSTRING",
                    "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
                },
                {
                    "name": "WEBSITE_CONTENTSHARE",
                    "value": "[toLower(variables('functionAppName'))]"
                },
                {
                    "name": "FUNCTIONS_EXTENSION_VERSION",
                    "value": "~1"
                }
            ]
        }
    }
}
```                    

<a name="app-service-plan"></a> 

## <a name="deploy-a-function-app-on-hello-app-service-plan"></a>Implementeren van een functie-app op Hallo App Service-abonnement

In Hallo App Service-abonnement, de functie-app uitgevoerd via exclusieve virtuele machines op een vergelijkbare tooweb apps Basic, Standard en Premium-SKU's. Zie voor meer informatie over de werking van App Service-abonnement Hallo Hallo [gedetailleerd overzicht van Azure App Service-plannen](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md). 

Zie voor een Azure Resource Manager voorbeeldsjabloon [functie-app in Azure App Service-plan].

### <a name="create-an-app-service-plan"></a>Een App Service-plan maken

```json
{
    "type": "Microsoft.Web/serverfarms",
    "apiVersion": "2015-04-01",
    "name": "[variables('hostingPlanName')]",
    "location": "[resourceGroup().location]",
    "properties": {
        "name": "[variables('hostingPlanName')]",
        "sku": "[parameters('sku')]",
        "workerSize": "[parameters('workerSize')]",
        "hostingEnvironment": "",
        "numberOfWorkers": 1
    }
}
```

### <a name="create-a-function-app"></a>Een functie-app maken 

Nadat u een optie schaling hebt geselecteerd, maakt u een functie-app. Hallo-app is Hallo-container met alle uw functies.

Een functie-app heeft veel onderliggende resources die u in uw implementatie gebruiken kunt, met inbegrip van app-instellingen en opties voor beheer. Bovendien kunt u tooremove hello **sourcecontrols** onderliggende resource, en gebruik een andere [Implementatieoptie](functions-continuous-deployment.md) in plaats daarvan.

> [!IMPORTANT]
> toosuccessfully uw toepassing implementeren met behulp van Azure Resource Manager, is het belangrijk toounderstand hoe resources worden geïmplementeerd in Azure. Hallo voorbeeld te volgen, op het hoogste niveau configuraties worden toegepast met behulp van **siteConfig**. Het is belangrijk tooset deze configuraties boven een niveau, omdat ze gegevens toohello functies runtime en implementatie-engine worden beschouwd. Op het hoogste niveau informatie is vereist voordat de onderliggende hello **sourcecontrols of web** resource wordt toegepast. Hoewel het mogelijk tooconfigure deze instellingen in een onderliggend niveau Hallo **config/appSettings** bron, in sommige gevallen functie-app moet worden geïmplementeerd *voordat* **config/appSettings**  wordt toegepast. Bijvoorbeeld, wanneer u werkt in combinatie met gebruikt [Logic Apps](../logic-apps/index.md), uw functies zijn afhankelijk van een andere resource.

```json
{
  "apiVersion": "2015-08-01",
  "name": "[parameters('appName')]",
  "type": "Microsoft.Web/sites",
  "kind": "functionapp",
  "location": "[parameters('location')]",
  "dependsOn": [
    "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]",
    "[resourceId('Microsoft.Web/serverfarms', parameters('appName'))]"
  ],
  "properties": {
     "serverFarmId": "[variables('appServicePlanName')]",
     "siteConfig": {
        "alwaysOn": true,
        "appSettings": [
            { "name": "FUNCTIONS_EXTENSION_VERSION", "value": "~1" },
            { "name": "Project", "value": "src" }
        ]
     }
  },
  "resources": [
     {
        "apiVersion": "2015-08-01",
        "name": "appsettings",
        "type": "config",
        "dependsOn": [
          "[resourceId('Microsoft.Web/Sites', parameters('appName'))]",
          "[resourceId('Microsoft.Web/Sites/sourcecontrols', parameters('appName'), 'web')]",
          "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]"
        ],
        "properties": {
          "AzureWebJobsStorage": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]",
          "AzureWebJobsDashboard": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
        }
     },
     {
          "apiVersion": "2015-08-01",
          "name": "web",
          "type": "sourcecontrols",
          "dependsOn": [
            "[resourceId('Microsoft.Web/sites/', parameters('appName'))]"
          ],
          "properties": {
            "RepoUrl": "[parameters('sourceCodeRepositoryURL')]",
            "branch": "[parameters('sourceCodeBranch')]",
            "IsManualIntegration": "[parameters('sourceCodeManualIntegration')]"
          }
     }
  ]
}
```
> [!TIP]
> Deze sjabloon maakt gebruik van Hallo [Project](https://github.com/projectkudu/kudu/wiki/Customizing-deployments#using-app-settings-instead-of-a-deployment-file) app-instellingen-waarde ingesteld Hallo-basismap in welke Hallo functies implementatie-engine (Kudu) implementeerbare code zoekt. In onze opslagplaats onze functies zijn in een submap van Hallo **src** map. Dus in Hallo voorgaande voorbeeld, we waarde Hallo app instellingen te`src`. Als uw functies in de hoofdmap van uw opslagplaats hello, of als u niet vanuit resourcebeheer implementeert, kunt u de waarde van deze app-instellingen verwijderen.

## <a name="deploy-your-template"></a>De sjabloon implementeren

U kunt een van de volgende manieren toodeploy Hallo uw sjabloon:

* [PowerShell](../azure-resource-manager/resource-group-template-deploy.md)
* [Azure-CLI](../azure-resource-manager/resource-group-template-deploy-cli.md)
* [Azure Portal](../azure-resource-manager/resource-group-template-deploy-portal.md)
* [REST API](../azure-resource-manager/resource-group-template-deploy-rest.md)

### <a name="deploy-tooazure-button"></a>TooAzure implementatieknop

Vervang ```<url-encoded-path-to-azuredeploy-json>``` met een [URL-codering](https://www.bing.com/search?q=url+encode) versie van onbewerkte pad Hallo van uw `azuredeploy.json` -bestand in GitHub.

Hier volgt een voorbeeld die gebruikmaakt van markdown:

```markdown
[![Deploy tooAzure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>)
```

Hier volgt een voorbeeld waarin HTML wordt gebruikt:

```html
<a href="https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"></a>
```

## <a name="next-steps"></a>Volgende stappen

Meer informatie over het toodevelop en configureren van Azure Functions.

* [Naslaginformatie over Azure Functions voor ontwikkelaars](functions-reference.md)
* [Hoe de app-instellingen voor het functioneren van tooconfigure Azure](functions-how-to-use-azure-function-app-settings.md)
* [Uw eerste Azure-functie maken](functions-create-first-azure-function.md)

<!-- LINKS -->

[functie-app van verbruik plan]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dynamic/azuredeploy.json
[functie-app in Azure App Service-plan]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dedicated/azuredeploy.json
