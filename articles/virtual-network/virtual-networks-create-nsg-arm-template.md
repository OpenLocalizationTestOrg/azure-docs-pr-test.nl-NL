---
title: aaaCreate netwerkbeveiligingsgroepen - Azure Resource Manager-sjabloon | Microsoft Docs
description: Meer informatie over hoe toocreate en netwerkbeveiligingsgroepen met een Azure Resource Manager-sjabloon implementeren.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: f3e7385d-717c-44ff-be20-f9aa450aa99b
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3750168284fea7b41c8c0f908b0d31a9da5e38ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-an-azure-resource-manager-template"></a>Netwerk beveiligingsgroepen met een Azure Resource Manager-sjabloon maken

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

In dit artikel bevat informatie over Hallo Resource Manager-implementatiemodel. U kunt ook [nsg's maken in het klassieke implementatiemodel Hallo](virtual-networks-create-nsg-classic-ps.md).

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

## <a name="nsg-resources-in-a-template-file"></a>NSG-resources in een sjabloonbestand
U kunt weergeven en downloaden Hallo [voorbeeldsjabloon](https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/NSGs.json).

Hallo volgende sectie wordt uitgelegd Hallo definitie van Hallo front-NSG, op basis van Hallo scenario.

```json
"apiVersion": "2015-06-15",
"type": "Microsoft.Network/networkSecurityGroups",
"name": "[parameters('frontEndNSGName')]",
"location": "[resourceGroup().location]",
"tags": {
  "displayName": "NSG - Front End"
},
"properties": {
  "securityRules": [
    {
      "name": "rdp-rule",
      "properties": {
        "description": "Allow RDP",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "3389",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "*",
        "access": "Allow",
        "priority": 100,
        "direction": "Inbound"
      }
    },
    {
      "name": "web-rule",
      "properties": {
        "description": "Allow WEB",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "80",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "*",
        "access": "Allow",
        "priority": 101,
        "direction": "Inbound"
      }
    }
  ]
}
```
tooassociate hello NSG toohello front-end-subnet, hebt u toochange Hallo subnetdefinitie in Hallo sjabloon en gebruik Hallo Verwijzings-id voor Hallo NSG.

```json
"subnets": [
  {
    "name": "[parameters('frontEndSubnetName')]",
    "properties": {
      "addressPrefix": "[parameters('frontEndSubnetPrefix')]",
      "networkSecurityGroup": {
      "id": "[resourceId('Microsoft.Network/networkSecurityGroups', parameters('frontEndNSGName'))]"
      }
    }
  }, 
```

U ziet Hallo dezelfde voor Hallo back-end NSG- en Hallo back-end in de sjabloon Hallo werd uitgevoerd.

## <a name="deploy-hello-arm-template-by-using-click-toodeploy"></a>Hallo ARM-sjabloon implementeren met behulp van toodeploy klikt u op
Hallo voorbeeldsjabloon beschikbaar in de openbare opslagplaats Hallo maakt gebruik van een parameterbestand met Hallo standaard waarden gebruikt toogenerate Hallo scenario die hierboven worden beschreven. toodeploy toodeploy, het gebruik van deze sjabloon Klik Volg [deze koppeling](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd-NSG), klikt u op **tooAzure implementeren**, vervang Hallo standaardparameterwaarden indien nodig en volg de instructies Hallo in Hallo-portal.

## <a name="deploy-hello-arm-template-by-using-powershell"></a>Hallo ARM-sjabloon implementeren met behulp van PowerShell
toodeploy hello ARM-sjabloon die u hebt gedownload met behulp van PowerShell, Hallo volgende stappen.

1. Als u Azure PowerShell nog nooit hebt gebruikt, volgt u de instructies Hallo in Hallo [hoe tooInstall en configureer Azure PowerShell](/powershell/azure/overview) tooinstall en configureer deze.
2. Voer Hallo  **`New-AzureRmResourceGroup`**  cmdlet toocreate een resource-groep met Hallo sjabloon.

    ```powershell
    New-AzureRmResourceGroup -Name TestRG -Location uswest `
    -TemplateFile 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.json' `
    -TemplateParameterFile 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.parameters.json'
    ```

    Verwachte uitvoer:

        ResourceGroupName : TestRG
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *                  
   
        Resources         :
                            Name                Type                                     Location
                            ==================  =======================================  ========
                            sqlAvSet            Microsoft.Compute/availabilitySets       westus  
                            webAvSet            Microsoft.Compute/availabilitySets       westus  
                            SQL1                Microsoft.Compute/virtualMachines        westus  
                            SQL2                Microsoft.Compute/virtualMachines        westus  
                            Web1                Microsoft.Compute/virtualMachines        westus  
                            Web2                Microsoft.Compute/virtualMachines        westus  
                            TestNICSQL1         Microsoft.Network/networkInterfaces      westus  
                            TestNICSQL2         Microsoft.Network/networkInterfaces      westus  
                            TestNICWeb1         Microsoft.Network/networkInterfaces      westus  
                            TestNICWeb2         Microsoft.Network/networkInterfaces      westus  
                            NSG-BackEnd         Microsoft.Network/networkSecurityGroups  westus  
                            NSG-FrontEnd        Microsoft.Network/networkSecurityGroups  westus  
                            TestPIPSQL1         Microsoft.Network/publicIPAddresses      westus  
                            TestPIPSQL2         Microsoft.Network/publicIPAddresses      westus  
                            TestPIPWeb1         Microsoft.Network/publicIPAddresses      westus  
                            TestPIPWeb2         Microsoft.Network/publicIPAddresses      westus  
                            TestVNet            Microsoft.Network/virtualNetworks        westus  
                            testvnetstorageprm  Microsoft.Storage/storageAccounts        westus  
                            testvnetstoragestd  Microsoft.Storage/storageAccounts        westus  
   
        ResourceId        : /subscriptions/[Subscription Id]/resourceGroups/TestRG

## <a name="deploy-hello-arm-template-by-using-hello-azure-cli"></a>Hallo ARM-sjabloon implementeren met behulp van hello Azure CLI
toodeploy hello ARM-sjabloon met behulp van Azure CLI Hallo Hallo volgende stappen.

1. Als u Azure CLI nog nooit hebt gebruikt, raadpleegt u [installeren en configureren van Azure CLI Hallo](../cli-install-nodejs.md) en volg de instructies Hallo toohello punt waar u uw Azure-account en abonnement selecteren.
2. Voer Hallo  **`azure config mode`**  opdracht tooswitch tooResource modus Manager, zoals hieronder wordt weergegeven.

    ```azurecli
    azure config mode arm
    ```

    Hallo volgt Hallo verwachte uitvoer voor Hallo-opdracht:

        info:    New mode is arm

3. Voer Hallo  **`azure group deployment create`**  cmdlet toodeploy Hallo nieuwe VNet met behulp van Hallo sjabloon en de parameterbestanden die u hebt gedownload en hierboven zijn gewijzigd. Hallo-lijst die wordt weergegeven na Hallo uitvoer wordt uitgelegd Hallo parameters die worden gebruikt.

    ```azurecli
    azure group create -n TestRG -l westus -f 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.json' -e 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.parameters.json'
    ```

    Verwachte uitvoer:
   
        info:    Executing command group create
        info:    Getting resource group TestRG
        info:    Creating resource group TestRG
        info:    Created resource group TestRG
        info:    Initializing template configurations and parameters
        info:    Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG
        data:    Name:                TestRG
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:    
        info:    group create command OK
   
   * **-n (of --naam)**. Naam van Hallo resource groep toobe gemaakt.
   * **-l (of --locatie)**. Azure-regio waar Hallo resourcegroep wordt gemaakt.
   * **-f (of--sjabloonbestand)**. Pad tooyour ARM-sjabloonbestand.
   * **-e (of--parametersbestand)**. Pad tooyour parametersbestand.

