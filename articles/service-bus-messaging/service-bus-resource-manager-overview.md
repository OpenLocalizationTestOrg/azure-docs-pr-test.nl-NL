---
title: aaaCreate Azure Service Bus-resources met behulp van Azure Resource Manager-sjablonen | Microsoft Docs
description: Gebruik Azure Resource Manager sjablonen tooautomate Hallo maken van Service Bus-resources
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 24f6a207-0fa4-49cf-8a58-963f9e2fd655
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: e539902cae307b63ae7c332580e2064761331ec5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-service-bus-resources-using-azure-resource-manager-templates"></a>Service Bus-resources met behulp van Azure Resource Manager-sjablonen maken

Dit artikel wordt beschreven hoe toocreate en implementeren van Service Bus-resources met behulp van Azure Resource Manager-sjablonen, PowerShell en Hallo Service Bus-resourceprovider.

Azure Resource Manager-sjablonen kunt u definiëren Hallo resources toodeploy voor een oplossing en toospecify parameters en variabelen vaststellen waarmee u tooinput waarden voor verschillende omgevingen. Hallo sjabloon bestaat uit JSON en uitdrukkingen die u kunt tooconstruct waarden voor uw implementatie te gebruiken. Zie voor gedetailleerde informatie over het schrijven van Azure Resource Manager-sjablonen en een beschrijving van de indeling van de template Hallo [structuur en de syntaxis van Azure Resource Manager-sjablonen](../azure-resource-manager/resource-group-authoring-templates.md).

> [!NOTE]
> voorbeelden in dit artikel tonen hoe Hallo toouse Azure Resource Manager toocreate een Service Bus-naamruimte en de messaging-eenheid (wachtrij). Andere voorbeelden sjabloon vindt u op Hallo [galerie van Azure-Snelstartsjablonen] [ Azure Quickstart Templates gallery] en zoek naar 'Servicebus'.
>
>

## <a name="service-bus-resource-manager-templates"></a>Service Bus-Resource Manager-sjablonen

Deze Service Bus Azure Resource Manager-sjablonen zijn beschikbaar voor download- en implementatie. Klik op Hallo volgende koppelingen voor meer informatie over elk ervan, met koppelingen toohello sjablonen op GitHub:

* [Een Service Bus-naamruimte maken](service-bus-resource-manager-namespace.md)
* [Een Service Bus-naamruimte maken met de wachtrij](service-bus-resource-manager-namespace-queue.md)
* [Een Service Bus-naamruimte met onderwerp en een abonnement maken](service-bus-resource-manager-namespace-topic.md)
* [Een Service Bus-naamruimte met een wachtrij en autorisatie regel maken](service-bus-resource-manager-namespace-auth-rule.md)
* [Een Service Bus-naamruimte maken met onderwerp, abonnement en regel](service-bus-resource-manager-namespace-topic-with-rule.md)

## <a name="deploy-with-powershell"></a>Implementeren met PowerShell

Hallo volgende procedure wordt beschreven hoe toouse PowerShell toodeploy een Azure Resource Manager-sjabloon die wordt gemaakt een **standaard** servicetier Service Bus-naamruimte en een wachtrij binnen deze naamruimte. In dit voorbeeld is gebaseerd op Hallo [een Service Bus-naamruimte maken met de wachtrij](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue) sjabloon. Hallo geschatte werkstroom is als volgt:

1. Installeer PowerShell.
2. Hallo-sjabloon en (optioneel) een parameterbestand maken.
3. Aanmelden in PowerShell tooyour Azure-account.
4. Een nieuwe resourcegroep maken als deze niet bestaat.
5. Hallo-implementatie testen.
6. Indien gewenst kunt u Hallo implementatiemodus.
7. Hallo-sjabloon implementeren.

Zie voor meer informatie over het implementeren van Azure Resource Manager-sjablonen [implementeren van resources met Azure Resource Manager-sjablonen][Deploy resources with Azure Resource Manager templates].

### <a name="install-powershell"></a>PowerShell installeren

Azure PowerShell installeren door de instructies te volgen Hallo in [aan de slag met Azure PowerShell](/powershell/azure/get-started-azureps).

### <a name="create-a-template"></a>Een sjabloon maken

Kloon of kopieer Hallo [201-servicebus-maken-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json) sjabloon vanuit GitHub:

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "serviceBusNamespaceName": {
            "type": "string",
            "metadata": {
                "description": "Name of hello Service Bus namespace"
            }
        },
        "serviceBusQueueName": {
            "type": "string",
            "metadata": {
                "description": "Name of hello Queue"
            }
        },
        "serviceBusApiVersion": {
            "type": "string",
            "defaultValue": "2015-08-01",
            "metadata": {
                "description": "Service Bus ApiVersion used by hello template"
            }
        }
    },
    "variables": {
        "location": "[resourceGroup().location]",
        "sbVersion": "[parameters('serviceBusApiVersion')]",
        "defaultSASKeyName": "RootManageSharedAccessKey",
        "authRuleResourceId": "[resourceId('Microsoft.ServiceBus/namespaces/authorizationRules', parameters('serviceBusNamespaceName'), variables('defaultSASKeyName'))]"
    },
    "resources": [{
        "apiVersion": "[variables('sbVersion')]",
        "name": "[parameters('serviceBusNamespaceName')]",
        "type": "Microsoft.ServiceBus/Namespaces",
        "location": "[variables('location')]",
        "kind": "Messaging",
        "sku": {
            "name": "StandardSku",
            "tier": "Standard"
        },
        "resources": [{
            "apiVersion": "[variables('sbVersion')]",
            "name": "[parameters('serviceBusQueueName')]",
            "type": "Queues",
            "dependsOn": [
                "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
            ],
            "properties": {
                "path": "[parameters('serviceBusQueueName')]"
            }
        }]
    }],
    "outputs": {
        "NamespaceConnectionString": {
            "type": "string",
            "value": "[listkeys(variables('authRuleResourceId'), variables('sbVersion')).primaryConnectionString]"
        },
        "SharedAccessPolicyPrimaryKey": {
            "type": "string",
            "value": "[listkeys(variables('authRuleResourceId'), variables('sbVersion')).primaryKey]"
        }
    }
}
```

### <a name="create-a-parameters-file-optional"></a>Maak een parameterbestand (optioneel)

toouse een optionele parameters-bestand kopiëren Hallo [201-servicebus-maken-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json) bestand. Vervang de waarde Hallo van `serviceBusNamespaceName` met de naam van de Service Bus-naamruimte Hallo Hallo u toocreate in deze implementatie wilt en vervang de waarde Hallo van `serviceBusQueueName` met de naam van de wachtrij Hallo Hallo gewenste toocreate.

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "serviceBusNamespaceName": {
            "value": "<myNamespaceName>"
        },
        "serviceBusQueueName": {
            "value": "<myQueueName>"
        },
        "serviceBusApiVersion": {
            "value": "2015-08-01"
        }
    }
}
```

Zie voor meer informatie, Hallo [Parameters](../azure-resource-manager/resource-group-template-deploy.md#parameter-files) onderwerp.

### <a name="log-in-tooazure-and-set-hello-azure-subscription"></a>Meld u bij tooAzure en hello Azure-abonnement instellen

Voer vanuit een PowerShell-prompt Hallo volgende opdracht:

```powershell
Login-AzureRmAccount
```

U bent na vragen aan gebruiker toolog op tooyour Azure-account. Na aanmelding uitgevoerd na de opdracht tooview Hallo uw beschikbare abonnementen.

```powershell
Get-AzureRMSubscription
```

Deze opdracht retourneert een lijst met beschikbare Azure-abonnementen. Kies een abonnement voor Hallo huidige sessie door het uitvoeren van de volgende opdracht Hallo. Vervang `<YourSubscriptionId>` Hello GUID voor hello Azure-abonnement u wilt dat toouse.

```powershell
Set-AzureRmContext -SubscriptionID <YourSubscriptionId>
```

### <a name="set-hello-resource-group"></a>Set Hallo resourcegroep

Als u een bestaande resource groep, maakt u een nieuwe resourcegroep met Hallo niet hebt ** New-AzureRmResourceGroup ** opdracht. Hallo-naam van het Hallo-resourcegroep en locatie die u wilt dat toouse opgeven. Bijvoorbeeld:

```powershell
New-AzureRmResourceGroup -Name MyDemoRG -Location "West US"
```

Als dit lukt, wordt een overzicht van de nieuwe resourcegroep Hallo weergegeven.

```powershell
ResourceGroupName : MyDemoRG
Location          : westus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/<GUID>/resourceGroups/MyDemoRG
```

### <a name="test-hello-deployment"></a>Hallo-implementatie testen

Valideren van uw implementatie door Hallo `Test-AzureRmResourceGroupDeployment` cmdlet. Bij het testen van Hallo implementatie Geef parameters op exact dezelfde manier als bij het uitvoeren van Hallo-implementatie.

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

### <a name="create-hello-deployment"></a>Hallo implementatie maken

toocreate hello nieuwe implementatie, Voer Hallo `New-AzureRmResourceGroupDeployment` cmdlet, en geef de benodigde parameters op Hallo wanneer u wordt gevraagd. Hallo parameters bevatten een naam voor uw implementatie, het Hallo-naam van uw resourcegroep, en het Hallo-pad of de URL toohello sjabloonbestand. Als hello **modus** parameter niet is opgegeven, de standaardwaarde van Hallo **incrementele** wordt gebruikt. Zie voor meer informatie [incrementele en volledige implementaties](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments).

Hallo volgende opdrachtprompts u voor Hallo drie parameters in Hallo PowerShell-venster:

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

een parameterbestand toospecify gebruiken in plaats daarvan Hallo opdracht te volgen.

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json -TemplateParameterFile <path tooparameters file>\azuredeploy.parameters.json
```

U kunt ook parameters inline gebruiken als u Hallo deployment cmdlet uitvoert. Hallo-opdracht is als volgt:

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json -parameterName "parameterValue"
```

toorun een [voltooid](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments) voor implementatie, set Hallo **modus** parameter te**Complete**:

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -Mode Complete -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

### <a name="verify-hello-deployment"></a>Hallo-implementatie controleren
Als het Hallo-resources zijn geïmplementeerd, wordt een overzicht van Hallo-implementatie in Hallo PowerShell-venster weergegeven:

```powershell
DeploymentName    : MyDemoDeployment
ResourceGroupName : MyDemoRG
ProvisioningState : Succeeded
Timestamp         : 4/19/2016 10:38:30 PM
Mode              : Incremental
TemplateLink      :
Parameters        :
                    Name             Type                       Value
                    ===============  =========================  ==========
                    serviceBusNamespaceName  String             <namespaceName>
                    serviceBusQueueName  String                 <queueName>
                    serviceBusApiVersion  String                2015-08-01

```

## <a name="next-steps"></a>Volgende stappen
U hebt nu gezien Hallo basiswerkstroom en opdrachten voor het implementeren van een Azure Resource Manager-sjabloon. Ga naar Hallo koppelingen volgen voor meer gedetailleerde informatie:

* [Overzicht van Azure Resource Manager][Azure Resource Manager overview]
* [Resources met Resource Manager-sjablonen en Azure PowerShell implementeren][Deploy resources with Azure Resource Manager templates]
* [Azure Resource Manager-sjablonen maken](../azure-resource-manager/resource-group-authoring-templates.md)

[Azure Resource Manager overview]: ../azure-resource-manager/resource-group-overview.md
[Deploy resources with Azure Resource Manager templates]: ../azure-resource-manager/resource-group-template-deploy.md
[Azure Quickstart Templates gallery]: https://azure.microsoft.com/documentation/templates/?term=service+bus
