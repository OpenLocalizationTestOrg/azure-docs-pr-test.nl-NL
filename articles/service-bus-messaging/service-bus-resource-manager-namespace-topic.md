---
title: Azure Service Bus-naamruimte onderwerpabonnement met Azure Resource Manager-sjabloon maken | Microsoft Docs
description: Een Service Bus-naamruimte maken met het onderwerp en een abonnement met Azure Resource Manager-sjabloon
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: d3d55200-5c60-4b5f-822d-59974cafff0e
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: 8dd48787e7b788d249085b3110484de1a2c1d265
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-service-bus-namespace-with-topic-and-subscription-using-an-azure-resource-manager-template"></a>Een Service Bus-naamruimte maken met het onderwerp en een abonnement met een Azure Resource Manager-sjabloon

Dit artikel laat zien hoe u een Azure Resource Manager-sjabloon die wordt gemaakt van een Service Bus-naamruimte en een onderwerp en een abonnement binnen deze naamruimte. U leert hoe om te definiëren welke bronnen worden geïmplementeerd en het definiëren van de parameters die zijn opgegeven wanneer de implementatie wordt uitgevoerd. U kunt deze sjabloon gebruiken voor uw eigen implementaties of de sjabloon aanpassen aan uw eisen

Zie voor meer informatie over het maken van sjablonen [Azure Resource Manager-sjablonen samenstellen][Authoring Azure Resource Manager templates].

Zie voor de volledige sjabloon, het [Service Bus-naamruimte met onderwerp en een abonnement] [ Service Bus namespace with topic and subscription] sjabloon.

> [!NOTE]
> De volgende Azure Resource Manager-sjablonen zijn beschikbaar voor download- en implementatie.
> 
> * [Een Service Bus-naamruimte maken](service-bus-resource-manager-namespace.md)
> * [Een Service Bus-naamruimte maken met de wachtrij](service-bus-resource-manager-namespace-queue.md)
> * [Een Service Bus-naamruimte met een wachtrij en autorisatie regel maken](service-bus-resource-manager-namespace-auth-rule.md)
> * [Een Service Bus-naamruimte maken met onderwerp, abonnement en regel](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> Om te controleren of de meest recente sjablonen, gaat u naar de [Azure-Snelstartsjablonen] [ Azure Quickstart Templates] galerie en zoek naar 'Servicebus'.
> 
> 

## <a name="what-will-you-deploy"></a>Wat wilt u implementeren?

Met deze sjabloon implementeert u een Service Bus-naamruimte met onderwerp en een abonnement.

[Service Bus-onderwerpen en abonnementen](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) biedt een een-op-veel-vorm van communicatie, in een *publiceren/abonneren* patroon.

Klik op de volgende knop om de implementatie automatisch uit te voeren:

[![Implementeren in Azure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-and-subscription%2Fazuredeploy.json)

## <a name="parameters"></a>Parameters

Met Azure Resource Manager kunt u parameters definiëren voor waarden die u wilt opgeven wanneer de sjabloon wordt geïmplementeerd. De sjabloon bevat een sectie met de naam `Parameters` die de parameterwaarden bevat. U moet een parameter voor de waarden die variëren op basis van het project dat u wilt implementeren of op basis van de omgeving die u om te implementeert definiëren. Geen parameters op voor waarden die u altijd hetzelfde gedefinieerd. De waarde van elke parameter wordt gebruikt in de sjabloon voor het definiëren van de resources die worden geïmplementeerd.

De sjabloon definieert de volgende parameters.

### <a name="servicebusnamespacename"></a>serviceBusNamespaceName
De naam van de Service Bus-naamruimte maken.

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="servicebustopicname"></a>serviceBusTopicName
De naam van het onderwerp in de Service Bus-naamruimte gemaakt.

```json
"serviceBusTopicName": {
"type": "string"
}
```

### <a name="servicebussubscriptionname"></a>serviceBusSubscriptionName
De naam van het abonnement in de Service Bus-naamruimte gemaakt.

```json
"serviceBusSubscriptionName": {
"type": "string"
}
```

### <a name="servicebusapiversion"></a>serviceBusApiVersion
De Service Bus-API-versie van de sjabloon.

```json
"serviceBusApiVersion": {
"type": "string"
}
```
## <a name="resources-to-deploy"></a>Resources om te implementeren
Maakt een standaard Service Bus-naamruimte van het type **Messaging**, met het onderwerp en een abonnement.

```json
"resources ": [{
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
            "name": "[parameters('serviceBusTopicName')]",
            "type": "Topics",
            "dependsOn": [
                "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
            ],
            "properties": {
                "path": "[parameters('serviceBusTopicName')]",
            },
            "resources": [{
                "apiVersion": "[variables('sbVersion')]",
                "name": "[parameters('serviceBusSubscriptionName')]",
                "type": "Subscriptions",
                "dependsOn": [
                    "[parameters('serviceBusTopicName')]"
                ],
                "properties": {}
            }]
        }]
    }]
```

## <a name="commands-to-run-deployment"></a>Opdrachten om implementatie uit te voeren
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a>PowerShell
```powershell
New-AzureResourceGroupDeployment -Name \<deployment-name\> -ResourceGroupName \<resource-group-name\> -TemplateUri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-and-subscription/azuredeploy.json>
```

## <a name="azure-cli"></a>Azure CLI
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-and-subscription/azuredeploy.json>
```

## <a name="next-steps"></a>Volgende stappen
Nu dat u hebt gemaakt en geïmplementeerd met Azure Resource Manager bronnen, meer informatie over deze resources beheren door deze artikelen te bekijken:

* [Servicebus met PowerShell beheren](service-bus-manage-with-ps.md)
* [Service Bus-resources beheren met de Service Bus-Explorer](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus topics and subscriptions]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Service Bus namespace with topic and subscription]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-topic-and-subscription/
