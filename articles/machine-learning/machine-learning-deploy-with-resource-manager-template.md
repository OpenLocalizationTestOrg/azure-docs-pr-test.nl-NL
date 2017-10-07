---
title: aaaDeploy een Machine Learning-werkruimte met Azure Resource Manager | Microsoft Docs
description: Hoe toodeploy een werkruimte voor Azure Machine Learning met Azure Resource Manager-sjabloon
services: machine-learning
documentationcenter: 
author: ahgyger
manager: haining
editor: garye
ms.assetid: 4955ac4d-ff99-4908-aa27-69b6bfcc8e85
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/15/2017
ms.author: ahgyger
ms.openlocfilehash: 308959825bcbd670f6ce9b6dc381be767f172357
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-machine-learning-workspace-using-azure-resource-manager"></a>Machine Learning-werkruimte implementeren met Azure Resource Manager
## <a name="introduction"></a>Inleiding
Met een Azure Resource Manager-implementatiesjabloon u bespaart tijd doordat u een toodeploy schaalbare manier met elkaar verbonden onderdelen van een mechanisme voor validatie en probeer het opnieuw. tooset van Azure Machine Learning werkruimten, bijvoorbeeld, moet u toofirst Azure storage-account configureert en vervolgens implementeert uw werkruimte. Stel dit handmatig te doen voor honderden werkruimten. Een eenvoudiger alternatief is toouse een Azure Resource Manager-sjabloon toodeploy een Azure Machine Learning-werkruimte en de afhankelijkheden ervan. In dit artikel leert u dit proces stapsgewijs. Zie voor een goed overzicht van Azure Resource Manager [overzicht van Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).

## <a name="step-by-step-create-a-machine-learning-workspace"></a>Stap voor stap: een Machine Learning-werkruimte maken
We wordt een Azure-resourcegroep maken en implementeren van een nieuwe Azure-opslagaccount en een nieuwe Azure Machine Learning-werkruimte met een Resource Manager-sjabloon. Zodra het Hallo-implementatie is voltooid, wordt er belangrijke informatie over het Hallo-werkruimten die zijn gemaakt (de primaire sleutel hello, Hallo workspaceID en Hallo URL toohello werkruimte) afgedrukt.

### <a name="create-an-azure-resource-manager-template"></a>Een Azure Resource Manager-sjabloon maken
Een Machine Learning-werkruimte vereist een Azure storage-account toostore Hallo gegevensset gekoppeld tooit.
Hallo volgende sjabloon gebruikt Hallo-naam van Hallo toogenerate Hallo storage account Resourcegroepnaam en de naam van de werkruimte Hallo.  Verder wordt Hallo opslagaccountnaam als een eigenschap tijdens het Hallo-werkruimte maken.

```
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "variables": {
        "namePrefix": "[resourceGroup().name]",
        "location": "[resourceGroup().location]",
        "mlVersion": "2016-04-01",
        "stgVersion": "2015-06-15",
        "storageAccountName": "[concat(variables('namePrefix'),'stg')]",
        "mlWorkspaceName": "[concat(variables('namePrefix'),'mlwk')]",
        "mlResourceId": "[resourceId('Microsoft.MachineLearning/workspaces', variables('mlWorkspaceName'))]",
        "stgResourceId": "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]",
        "storageAccountType": "Standard_LRS"
    },
    "resources": [
        {
            "apiVersion": "[variables('stgVersion')]",
            "name": "[variables('storageAccountName')]",
            "type": "Microsoft.Storage/storageAccounts",
            "location": "[variables('location')]",
            "properties": {
                "accountType": "[variables('storageAccountType')]"
            }
        },
        {
            "apiVersion": "[variables('mlVersion')]",
            "type": "Microsoft.MachineLearning/workspaces",
            "name": "[variables('mlWorkspaceName')]",
            "location": "[variables('location')]",
            "dependsOn": ["[variables('stgResourceId')]"],
            "properties": {
                "UserStorageAccountId": "[variables('stgResourceId')]"
            }
        }
    ],
    "outputs": {
        "mlWorkspaceObject": {"type": "object", "value": "[reference(variables('mlResourceId'), variables('mlVersion'))]"},
        "mlWorkspaceToken": {"type": "string", "value": "[listWorkspaceKeys(variables('mlResourceId'), variables('mlVersion')).primaryToken]"},
        "mlWorkspaceWorkspaceID": {"type": "string", "value": "[reference(variables('mlResourceId'), variables('mlVersion')).WorkspaceId]"},
        "mlWorkspaceWorkspaceLink": {"type": "string", "value": "[concat('https://studio.azureml.net/Home/ViewWorkspace/', reference(variables('mlResourceId'), variables('mlVersion')).WorkspaceId)]"}
    }
}

```
Deze sjabloon opslaan als mlworkspace.json bestand onder c:\temp\.

### <a name="deploy-hello-resource-group-based-on-hello-template"></a>Hallo-resourcegroep, op basis van Hallo sjabloon implementeren
* Open PowerShell
* Modules voor Azure Resource Manager en Azure Service Management installeren  

```
# Install hello Azure Resource Manager modules from hello PowerShell Gallery (press “A”)
Install-Module AzureRM -Scope CurrentUser

# Install hello Azure Service Management modules from hello PowerShell Gallery (press “A”)
Install-Module Azure -Scope CurrentUser
```

   Deze stappen download en installeer Hallo modules nodig toocomplete Hallo resterende stappen. Dit hoeft slechts één keer uitgevoerd in Hallo omgeving waar het uitvoeren van PowerShell-opdrachten Hallo toobe.   

* TooAzure verifiëren  

```
# Authenticate (enter your credentials in hello pop-up window)
Add-AzureRmAccount
```
Deze stap moet toobe herhaald voor elke sessie. Eenmaal is geverifieerd, moet uw abonnementsgegevens worden weergegeven.

![Azure-Account][1]

Nu we tooAzure toegang hebben, kunnen we Hallo resourcegroep maken.

* Een resourcegroep maken

```
$rg = New-AzureRmResourceGroup -Name "uniquenamerequired523" -Location "South Central US"
$rg
```

Controleer of dat die resourcegroep Hallo juist is ingericht. **ProvisioningState** moet worden "is voltooid."
Hallo de naam van resourcegroep wordt gebruikt door Hallo sjabloon toogenerate Hallo naam van het opslagaccount. Hallo opslagaccountnaam moet tussen 3 en 24 tekens lang zijn en alleen cijfers en kleine letters gebruiken.

![Resourcegroep][2]

* Met resource Hallo implementatie kunt implementeren die een nieuwe Machine Learning-werkruimte.

```
# Create a Resource Group, TemplateFile is hello location of hello JSON template.
$rgd = New-AzureRmResourceGroupDeployment -Name "demo" -TemplateFile "C:\temp\mlworkspace.json" -ResourceGroupName $rg.ResourceGroupName
```

Zodra het Hallo-implementatie is voltooid, is het eenvoudig tooaccess eigenschappen van Hallo werkruimte die u hebt geïmplementeerd. U kunt bijvoorbeeld toegang tot Hallo primaire Key Token.

```
# Access Azure ML Workspace Token after its deployment.
$rgd.Outputs.mlWorkspaceToken.Value
```

Een andere manier tooretrieve tokens van bestaande werkruimte is toouse Hallo Invoke-AzureRmResourceAction-opdracht. Bijvoorbeeld, kunt u de primaire en secundaire tokens Hallo van alle werkruimten aanbieden.

```  
# List hello primary and secondary tokens of all workspaces
Get-AzureRmResource |? { $_.ResourceType -Like "*MachineLearning/workspaces*"} |% { Invoke-AzureRmResourceAction -ResourceId $_.ResourceId -Action listworkspacekeys -Force}  
```
Nadat het Hallo-werkruimte is ingericht, kunt u ook veel Azure Machine Learning Studio taken met behulp van Hallo automatiseren [PowerShell-Module voor Azure Machine Learning](http://aka.ms/amlps).

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over [Azure Resource Manager-sjablonen ontwerpen](../azure-resource-manager/resource-group-authoring-templates.md). 
* Bekijk Hallo [Azure Quickstart-opslagplaats voor sjablonen](https://github.com/Azure/azure-quickstart-templates). 
* Bekijk deze video over [Azure Resource Manager](https://channel9.msdn.com/Events/Ignite/2015/C9-39). 

<!--Image references-->
[1]: ../media/machine-learning-deploy-with-resource-manager-template/azuresubscription.png
[2]: ../media/machine-learning-deploy-with-resource-manager-template/resourcegroupprovisioning.png


<!--Link references-->
