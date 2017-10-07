---
title: aaaCreate een virtuele machine met een statisch openbaar IP-adres - Azure Resource Manager-sjabloon | Microsoft Docs
description: Meer informatie over hoe toocreate een virtuele machine met een statische openbare IP-adres met een Azure Resource Manager-sjabloon.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d551085a-c7ed-4ec6-b4c3-e9e1cebb774c
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6a8640ed4fad06b0e09820e6114fd6789db73847
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-an-azure-resource-manager-template"></a>Een virtuele machine maken met een statisch openbaar IP-adres met een Azure Resource Manager-sjabloon

> [!div class="op_single_selector"]
> * [Azure Portal](virtual-network-deploy-static-pip-arm-portal.md)
> * [PowerShell](virtual-network-deploy-static-pip-arm-ps.md)
> * [Azure CLI](virtual-network-deploy-static-pip-arm-cli.md)
> * [Sjabloon](virtual-network-deploy-static-pip-arm-template.md)
> * [PowerShell (klassiek)](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../resource-manager-deployment-model.md). In dit artikel bevat informatie over Hallo Resource Manager-implementatiemodel, die Microsoft voor de meeste nieuwe implementaties in plaats van het klassieke implementatiemodel hello aanbeveelt gebruiken.

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="public-ip-address-resources-in-a-template-file"></a>Openbare IP-adres resources in een sjabloonbestand
U kunt weergeven en downloaden Hallo [voorbeeldsjabloon](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json).

Hallo volgende sectie wordt uitgelegd Hallo definitie van Hallo openbare IP-resource, op basis van de bovenstaande Hallo scenario:

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/publicIPAddresses",
  "name": "[variables('webVMSetting').pipName]",
  "location": "[variables('location')]",
  "properties": {
    "publicIPAllocationMethod": "Static"
  },
  "tags": {
    "displayName": "PublicIPAddress - Web"
  }
},
```

Kennisgeving Hallo **publicIPAllocationMethod** -eigenschap die is ingesteld te*statische*. Deze eigenschap kan zijn *dynamische* (standaardwaarde) of *statische*. Instelling voor het toostatic wordt gegarandeerd dat Hallo openbaar IP-adres toegewezen nooit wordt gewijzigd.

Hallo volgende sectie wordt uitgelegd Hallo koppeling van Hallo openbaar IP-adres met een netwerkinterface:

```json
  {
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[variables('webVMSetting').nicName]",
    "location": "[variables('location')]",
    "tags": {
    "displayName": "NetworkInterface - Web"
    },
    "dependsOn": [
      "[concat('Microsoft.Network/publicIPAddresses/', variables('webVMSetting').pipName)]",
      "[concat('Microsoft.Network/virtualNetworks/', parameters('vnetName'))]"
    ],
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
          "privateIPAllocationMethod": "Static",
          "privateIPAddress": "[variables('webVMSetting').ipAddress]",
          "publicIPAddress": {
          "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('webVMSetting').pipName)]"
          },
          "subnet": {
            "id": "[variables('frontEndSubnetRef')]"
          }
        }
      }
    ]
  }
},
```

Kennisgeving Hallo **publicIPAddress** eigenschap die verwijst toohello **Id** van een resource met de naam **variables('webVMSetting').pipName**. Dat is Hallo-naam van Hallo openbare IP-resource hierboven weergegeven.

Ten slotte Hallo netwerkinterface die hierboven wordt vermeld in Hallo **Schaalaanpassingsset** eigenschap Hallo VM wordt gemaakt.

```json
      "networkProfile": {
        "networkInterfaces": [
          {
            "id": "[resourceId('Microsoft.Network/networkInterfaces', variables('webVMSetting').nicName)]"
          }
        ]
      }
```

## <a name="deploy-hello-template-by-using-click-toodeploy"></a>Hallo-sjabloon implementeren met Klik toodeploy

Hallo voorbeeldsjabloon beschikbaar in de openbare opslagplaats Hallo maakt gebruik van een parameterbestand met Hallo standaard waarden gebruikt toogenerate Hallo scenario die hierboven worden beschreven. toodeploy deze sjabloon met klikt u op toodeploy, klikt u op **tooAzure implementeren** in Hallo Readme.md bestand voor Hallo [VM met statische PIP](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/03-Static-public-IP) sjabloon. Hallo standaardparameterwaarden vervangen indien gewenst en voer waarden in voor Hallo leeg parameters.  Volg de instructies Hallo in Hallo portal toocreate een virtuele machine met een statische openbare IP-adres.

## <a name="deploy-hello-template-by-using-powershell"></a>Hallo-sjabloon implementeren met behulp van PowerShell

toodeploy hello sjabloon die u hebt gedownload met behulp van PowerShell, Hallo volgende stappen.

1. Als u Azure PowerShell nog nooit hebt gebruikt, volledige Hallo stappen voor het Hallo [hoe tooInstall en configureer Azure PowerShell](/powershell/azure/overview) artikel.
2. In een PowerShell-console uitvoeren Hallo `New-AzureRmResourceGroup` cmdlet toocreate een nieuwe resourcegroep, indien nodig. Als er al een resourcegroep hebt gemaakt, gaat u toostep 3.

    ```powershell
    New-AzureRmResourceGroup -Name PIPTEST -Location westus
    ```

    Verwachte uitvoer:
   
        ResourceGroupName : PIPTEST
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/StaticPublicIP

3. In een PowerShell-console uitvoeren Hallo `New-AzureRmResourceGroupDeployment` cmdlet toodeploy Hallo sjabloon.

    ```powershell
    New-AzureRmResourceGroupDeployment -Name DeployVM -ResourceGroupName PIPTEST `
        -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json `
        -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json
    ```

    Verwachte uitvoer:
   
        DeploymentName    : DeployVM
        ResourceGroupName : PIPTEST
        ProvisioningState : Succeeded
        Timestamp         : [Date and time]
        Mode              : Incremental
        TemplateLink      :
                            Uri            : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/mas
                            ter/IaaS-Story/03-Static-public-IP/azuredeploy.json
                            ContentVersion : 1.0.0.0
   
        Parameters        :
                            Name                      Type                       Value     
                            ========================  =========================  ==========
                            vnetName                  String                     WTestVNet
                            vnetPrefix                String                     192.168.0.0/16
                            frontEndSubnetName        String                     FrontEnd  
                            frontEndSubnetPrefix      String                     192.168.1.0/24
                            storageAccountNamePrefix  String                     iaasestd  
                            stdStorageType            String                     Standard_LRS
                            osType                    String                     Windows   
                            adminUsername             String                     adminUser
                            adminPassword             SecureString                         
   
        Outputs           :

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a>Hallo-sjabloon implementeren met hello Azure CLI
toodeploy hello sjabloon met behulp van hello Azure CLI, volledige Hallo stappen te volgen:

1. Als u Azure CLI nog nooit hebt gebruikt, stappen Hallo in Hallo [installeren en configureren van Azure CLI Hallo](../cli-install-nodejs.md) tooinstall artikel en configureer deze.
2. Voer Hallo `azure config mode` opdracht tooswitch tooResource modus Manager, zoals hieronder wordt weergegeven.

    ```azurecli
    azure config mode arm
    ```

    Hallo verwachte uitvoer voor Hallo bovenstaande opdracht:

        info:    New mode is arm

3. Open Hallo [parameterbestand](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json), selecteer de inhoud ervan en tooa bestand opslaan op uw computer. In dit voorbeeld Hallo parameters tooa-bestand met de naam worden opgeslagen *parameters.json*. Hallo parameterwaarden binnen Hallo bestand desgewenst wijzigen, maar minimaal wordt aanbevolen dat u het Hallo-waarde voor Hallo adminPassword parameter tooa unieke, complex wachtwoord wijzigt.
4. Voer Hallo `azure group deployment create` cmd toodeploy Hallo nieuwe VNet met behulp van Hallo sjabloon en de parameterbestanden die u hebt gedownload en hierboven zijn gewijzigd. Vervang in Hallo opdracht onderstaande <path> met Hallo pad u Hallo-bestand moet worden opgeslagen. 

    ```azurecli
    azure group create -n PIPTEST2 -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json -e <path>\parameters.json
    ```

    Verwachte uitvoer (lijsten parameterwaarden gebruikt):

        info:    Executing command group create
        + Getting resource group PIPTEST2
        + Creating resource group PIPTEST2
        info:    Created resource group PIPTEST2
        + Initializing template configurations and parameters
        + Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/[Subscription ID]/resourceGroups/PIPTEST2
        data:    Name:                PIPTEST2
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:
        info:    group create command OK

