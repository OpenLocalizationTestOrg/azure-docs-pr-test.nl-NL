---
title: aaaCreate een virtuele machine met meerdere NIC's - Azure Resource Manager-sjabloon | Microsoft Docs
description: Een virtuele machine maken met meerdere NIC's met een Azure Resource Manager-sjabloon.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 486f7dd5-cf2f-434c-85d1-b3e85c427def
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f5d9ffcbd40c72dc18ae6de38e739eb5e45bf669
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-a-template"></a>Een virtuele machine met meerdere NIC's met een sjabloon maken
[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../resource-manager-deployment-model.md).  In dit artikel wordt beschreven hoe u Hallo Resource Manager-implementatiemodel, die Microsoft voor de meeste nieuwe implementaties in plaats van Hallo aanbeveelt [klassieke implementatiemodel](virtual-network-deploy-multinic-classic-ps.md).
> 

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

Hallo volgt gebruik van een resourcegroep met de naam *IaaSStory* voor Hallo-webservers en een resourcegroep met de naam *IaaSStory-back-end* voor Hallo DB-servers.

## <a name="prerequisites"></a>Vereisten
Voordat u Hallo DB servers maken kunt, moet u toocreate hello *IaaSStory* resourcegroep met alle Hallo benodigde resources voor dit scenario. toocreate voltooien van deze resources Hallo volgende stappen:

1. Navigeer te[Hallo sjabloonpagina](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).
2. Hallo sjabloon pagina toohello rechts van **bovenliggende resourcegroep**, klikt u op **tooAzure implementeren**.
3. Indien nodig, Hallo parameterwaarden te wijzigen en volg de stappen Hallo in hello Azure preview portal toodeploy Hallo-resourcegroep.

> [!IMPORTANT]
> Zorg ervoor dat de namen van opslagaccounts uniek zijn. Er kan geen dubbele opslagaccountnamen in Azure.
> 

## <a name="understand-hello-deployment-template"></a>Hallo-implementatiesjabloon begrijpen
Voordat u Hallo sjabloon van deze documentatie implementeert, zorg er dan voor dat u begrijpt wat het doet. volgende stappen uit Hallo biedt een goed overzicht van Hallo sjabloon:

1. Navigeer te[Hallo sjabloonpagina](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).
2. Klik op **azuredeploy.json** tooopen Hallo sjabloonbestand.
3. Kennisgeving Hallo *besturingssysteemtype* parameter hieronder vermeld. Deze parameter is gebruikte tooselect welke toouse VM-installatiekopie voor de databaseserver hello, samen met meerdere besturingssysteem gerelateerde instellingen.

    ```json
    "osType": {
      "type": "string",
      "defaultValue": "Windows",
      "allowedValues": [
        "Windows",
        "Ubuntu"
      ],
      "metadata": {
      "description": "Type of OS toouse for VMs: Windows or Ubuntu."
      }
    },
    ```

4. Schuif naar beneden toohello lijst met variabelen en definitie voor Hallo Hallo **dbVMSetting** variabelen, hieronder vermeld. Het ontvangt een Hallo matrixelementen in Hallo **dbVMSettings** variabele. Als u bekend met software development terminologie bent, kunt u bekijken Hallo **dbVMSettings** variabele als hash-tabel of een woordenlijst.

    ```json
    "dbVMSetting": "[variables('dbVMSettings')[parameters('osType')]]"
    ```

5. Stel dat u besluit toodeploy Windows virtuele machines waarop SQL in Hallo back-end. Vervolgens Hallo waarde voor **besturingssysteemtype** zou *Windows*, en Hallo **dbVMSetting** variabele onderstaande Hallo-element dat staat voor de eerste waarde Hallo in Hallo zou bevatten **dbVMSettings** variabele.

    ```json
    "Windows": {
      "vmSize": "Standard_DS3",
      "publisher": "MicrosoftSQLServer",
      "offer": "SQL2014SP1-WS2012R2",
      "sku": "Standard",
      "version": "latest",
      "vmName": "DB",
      "osdisk": "osdiskdb",
      "datadisk": "datadiskdb",
      "nicName": "NICDB",
      "ipAddress": "192.168.2.",
      "extensionDeployment": "",
      "avsetName": "ASDB",
      "remotePort": 3389,
      "dbPort": 1433
    },
    ```

6. Kennisgeving Hallo **vmSize** Hallo waarde bevat *Standard_DS3*. Hallo-gebruik van meerdere NIC's kunnen alleen bepaalde VM-grootten. U kunt controleren welke VM-grootten ondersteuning voor meerdere NIC's door te lezen Hallo [Windows VM-grootten](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) en [Linux VM-grootten](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) artikelen.

7. Schuif naar beneden te**resources** en kennisgeving Hallo eerste element. Een opslagaccount worden beschreven. Dit opslagaccount worden gebruikte toomaintain Hallo gegevensschijven die wordt gebruikt door elke VM-database. In dit scenario wordt heeft elke database VM een besturingssysteemschijf opgeslagen in reguliere storage en twee gegevensschijven opgeslagen in (premium) SSD-opslag.

    ```json
    {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[parameters('prmStorageName')]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "Storage Account - Premium"
      },
      "properties": {
      "accountType": "[parameters('prmStorageType')]"
      }
    },
    ```

8. Schuif naar beneden toohello volgende resource, zoals hieronder weergegeven. Deze bron vertegenwoordigt Hallo die NIC voor toegang tot de database in elke VM-database gebruikt. Gebruik van de kennisgeving Hallo Hallo **kopie** functie in deze resource. Hallo sjabloon kunt u toodeploy veel VM's als u wilt, op basis van de Hallo **dbCount** parameter. Daarom moet u toocreate Hallo dezelfde hoeveelheid NIC's voor toegang tot de database, één voor elke virtuele machine.

    ```json
    {
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[concat(variables('dbVMSetting').nicName,'-DA-', copyindex(1))]",
    "location": "[variables('location')]",
    "tags": {
      "displayName": "NetworkInterfaces - DB DA"
    },
    "copy": {
      "name": "dbniccount",
      "count": "[parameters('dbCount')]"
    },
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
            "privateIPAllocationMethod": "Static",
            "privateIPAddress": "[concat(variables('dbVMSetting').ipAddress,copyindex(4))]",
            "subnet": {
              "id": "[variables('backEndSubnetRef')]"
            }
          }
         }
       ] 
     }
    },
    ```

9. Schuif naar beneden toohello volgende resource, zoals hieronder weergegeven. Deze bron vertegenwoordigt Hallo die NIC voor beheer in elke VM-database gebruikt. Nogmaals, moet u een van deze NIC's voor elke database VM. Kennisgeving Hallo **networkSecurityGroup** element een NSG waarmee toegang tooRDP/SSH toothis NIC alleen koppelen.

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[concat(variables('dbVMSetting').nicName, '-RA-',copyindex(1))]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "NetworkInterfaces - DB RA"
    },
    "copy": {
      "name": "dbniccount",
      "count": "[parameters('dbCount')]"
    },
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
            "networkSecurityGroup": {
             "id": "[resourceId('Microsoft.Network/networkSecurityGroups', parameters('remoteAccessNSGName'))]"
             },
             "privateIPAllocationMethod": "Static",
             "privateIPAddress": "[concat(variables('dbVMSetting').ipAddress,copyindex(54))]",
             "subnet": {
              "id": "[variables('backEndSubnetRef')]"
             }
           }
          }
        ]
      }
    },
```

10. Schuif naar beneden toohello volgende resource, zoals hieronder weergegeven. Deze bron vertegenwoordigt een beschikbaarheid set toobe gedeeld door alle virtuele machines van database. Op die manier garandeert u dat er altijd worden één virtuele machine in Hallo ingesteld tijdens het onderhoud is uitgevoerd.

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Compute/availabilitySets",
      "name": "[variables('dbVMSetting').avsetName]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "AvailabilitySet - DB"
      }
    },
    ```

11. Schuif omlaag in de volgende resource toohello. Deze bron vertegenwoordigt Hallo database VM's, zoals in Hallo eerst paar regels die hieronder worden vermeld. Gebruik van de kennisgeving Hallo Hallo **kopie** opnieuw werkt, waarbij u ervoor zorgt dat meerdere virtuele machines worden gemaakt op basis van Hallo **dbCount** parameter. Let ook op Hallo **dependsOn** verzameling. Hiermee geeft u twee NIC's wordt nodig toobe gemaakt voordat Hallo die VM is geïmplementeerd, samen met de beschikbaarheidsset hello en Hallo storage-account.

    ```json
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('dbVMSetting').vmName,copyindex(1))]",
    "location": "[variables('location')]",
    "dependsOn": [
      "[concat('Microsoft.Network/networkInterfaces/', variables('dbVMSetting').nicName,'-DA-', copyindex(1))]",
      "[concat('Microsoft.Network/networkInterfaces/', variables('dbVMSetting').nicName,'-RA-', copyindex(1))]",
      "[concat('Microsoft.Compute/availabilitySets/', variables('dbVMSetting').avsetName)]",
      "[concat('Microsoft.Storage/storageAccounts/', parameters('prmStorageName'))]"
    ],
    "tags": {
      "displayName": "VMs - DB"
    },
    "copy": {
      "name": "dbvmcount",
      "count": "[parameters('dbCount')]"
    },
    ```

12. Schuif omlaag in Hallo VM resource toohello **Schaalaanpassingsset** element, zoals hieronder weergegeven. U ziet dat er twee NIC's wordt naslaginformatie voor elke virtuele machine. Als u meerdere NIC's voor een virtuele machine maakt, moet u instellen Hallo **primaire** eigenschap van een van de Hallo NIC's te*true*, en rest te Hallo*false*.

    ```json
    "networkProfile": {
      "networkInterfaces": [
        {
          "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('dbVMSetting').nicName,'-DA-',copyindex(1)))]",
          "properties": { "primary": true }
        },
        {
          "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('dbVMSetting').nicName,'-RA-',copyindex(1)))]",
          "properties": { "primary": false }
        }
      ]
    }
    ```

## <a name="deploy-hello-arm-template-by-using-click-toodeploy"></a>Hallo ARM-sjabloon implementeren met behulp van toodeploy klikt u op

> [!IMPORTANT]
> Zorg ervoor dat u volgt Hallo [vereisten](#Pre-requisites) stappen vóór Hallo onderstaande instructies.
> 

Hallo voorbeeldsjabloon beschikbaar in de openbare opslagplaats Hallo maakt gebruik van een parameterbestand met Hallo standaard waarden gebruikt toogenerate Hallo scenario die hierboven worden beschreven. toodeploy toodeploy, het gebruik van deze sjabloon Klik Volg [deze koppeling](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC), toohello rechts van **back-end resourcegroep (Zie de documentatie)** klikt u op **tooAzure implementeren**, vervangen Hallo standaardparameterwaarden indien nodig, en volg de instructies Hallo in Hallo-portal.

Hallo afbeelding hieronder toont Hallo inhoud van de nieuwe resourcegroep hello, na de implementatie.

![Back-end van resourcegroep](./media/virtual-network-deploy-multinic-arm-template/Figure2.png)

## <a name="deploy-hello-template-by-using-powershell"></a>Hallo-sjabloon implementeren met behulp van PowerShell
toodeploy hello sjabloon die u hebt gedownload met behulp van PowerShell, PowerShell installeren en configureren via Hallo stappen in Hallo [PowerShell installeren en configureren](/powershell/azure/overview) en voltooi vervolgens Hallo stappen te volgen:

Voer Hallo  **`New-AzureRmResourceGroup`**  cmdlet toocreate een resource-groep met Hallo sjabloon.

```powershell
New-AzureRmResourceGroup -Name IaaSStory-Backend -Location uswest `
TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.json' `
-TemplateParameterFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json'
```

Verwachte uitvoer:

    ResourceGroupName : IaaSStory-Backend
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    Permissions       :
                        Actions  NotActions
                        =======  ==========
                        *
        Resources         :
                        Name                 Type                                 Location
                        ===================  ===================================  ========
                        ASDB                 Microsoft.Compute/availabilitySets   westus  
                        DB1                  Microsoft.Compute/virtualMachines    westus  
                        DB2                  Microsoft.Compute/virtualMachines    westus  
                        NICDB-DA-1           Microsoft.Network/networkInterfaces  westus  
                        NICDB-DA-2           Microsoft.Network/networkInterfaces  westus  
                        NICDB-RA-1           Microsoft.Network/networkInterfaces  westus  
                        NICDB-RA-2           Microsoft.Network/networkInterfaces  westus  
                        wtestvnetstorageprm  Microsoft.Storage/storageAccounts    westus  
    ResourceId        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a>Hallo-sjabloon implementeren met hello Azure CLI
toodeploy hello sjabloon via Azure CLI Hallo Hallo volgende stappen.

1. Als u Azure CLI nog nooit hebt gebruikt, raadpleegt u [installeren en configureren van Azure CLI Hallo](../cli-install-nodejs.md) en volg de instructies Hallo toohello punt waar u uw Azure-account en abonnement selecteren.
2. Voer Hallo  **`azure config mode`**  opdracht tooswitch tooResource modus Manager, zoals hieronder wordt weergegeven.

    ```azurecli
    azure config mode arm
    ```

    Hallo verwachte uitvoer volgt:

        info:    New mode is arm

3. Open Hallo [parameterbestand](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json), selecteer de inhoud en tooa bestand opslaan op uw computer. In dit voorbeeld is opgeslagen Hallo parameterbestand te*parameters.json*.
4. Voer Hallo  **`azure group deployment create`**  cmdlet toodeploy Hallo nieuwe VNet met behulp van Hallo sjabloon en de parameterbestanden die u hebt gedownload en hierboven zijn gewijzigd. Hallo-lijst die wordt weergegeven na Hallo uitvoer wordt uitgelegd Hallo parameters die worden gebruikt.

    ```azurecli
    azure group create -n IaaSStory-Backend -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.json -e parameters.json
    ```

    Verwachte uitvoer:
   
        info:    Executing command group create
        + Getting resource group IaaSStory-Backend
        + Creating resource group IaaSStory-Backend
        info:    Created resource group IaaSStory-Backend
        + Initializing template configurations and parameters
        + Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend
        data:    Name:                IaaSStory-Backend
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:
        info:    group create command OK

