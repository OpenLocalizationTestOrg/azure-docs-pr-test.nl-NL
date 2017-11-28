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
# <a name="create-a-vm-with-a-static-public-ip-address-using-an-azure-resource-manager-template"></a><span data-ttu-id="5e396-103">Een virtuele machine maken met een statisch openbaar IP-adres met een Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="5e396-103">Create a VM with a static public IP address using an Azure Resource Manager template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5e396-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5e396-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="5e396-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5e396-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="5e396-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5e396-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="5e396-107">Sjabloon</span><span class="sxs-lookup"><span data-stu-id="5e396-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="5e396-108">PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="5e396-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="5e396-109">Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="5e396-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="5e396-110">In dit artikel bevat informatie over Hallo Resource Manager-implementatiemodel, die Microsoft voor de meeste nieuwe implementaties in plaats van het klassieke implementatiemodel hello aanbeveelt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5e396-110">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="public-ip-address-resources-in-a-template-file"></a><span data-ttu-id="5e396-111">Openbare IP-adres resources in een sjabloonbestand</span><span class="sxs-lookup"><span data-stu-id="5e396-111">Public IP address resources in a template file</span></span>
<span data-ttu-id="5e396-112">U kunt weergeven en downloaden Hallo [voorbeeldsjabloon](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="5e396-112">You can view and download hello [sample template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json).</span></span>

<span data-ttu-id="5e396-113">Hallo volgende sectie wordt uitgelegd Hallo definitie van Hallo openbare IP-resource, op basis van de bovenstaande Hallo scenario:</span><span class="sxs-lookup"><span data-stu-id="5e396-113">hello following section shows hello definition of hello public IP resource, based on hello scenario above:</span></span>

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

<span data-ttu-id="5e396-114">Kennisgeving Hallo **publicIPAllocationMethod** -eigenschap die is ingesteld te*statische*.</span><span class="sxs-lookup"><span data-stu-id="5e396-114">Notice hello **publicIPAllocationMethod** property, which is set too*Static*.</span></span> <span data-ttu-id="5e396-115">Deze eigenschap kan zijn *dynamische* (standaardwaarde) of *statische*.</span><span class="sxs-lookup"><span data-stu-id="5e396-115">This property can be either *Dynamic* (default value) or *Static*.</span></span> <span data-ttu-id="5e396-116">Instelling voor het toostatic wordt gegarandeerd dat Hallo openbaar IP-adres toegewezen nooit wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="5e396-116">Setting it toostatic guarantees that hello public IP address assigned will never change.</span></span>

<span data-ttu-id="5e396-117">Hallo volgende sectie wordt uitgelegd Hallo koppeling van Hallo openbaar IP-adres met een netwerkinterface:</span><span class="sxs-lookup"><span data-stu-id="5e396-117">hello following section shows hello association of hello public IP address with a network interface:</span></span>

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

<span data-ttu-id="5e396-118">Kennisgeving Hallo **publicIPAddress** eigenschap die verwijst toohello **Id** van een resource met de naam **variables('webVMSetting').pipName**.</span><span class="sxs-lookup"><span data-stu-id="5e396-118">Notice hello **publicIPAddress** property pointing toohello **Id** of a resource named **variables('webVMSetting').pipName**.</span></span> <span data-ttu-id="5e396-119">Dat is Hallo-naam van Hallo openbare IP-resource hierboven weergegeven.</span><span class="sxs-lookup"><span data-stu-id="5e396-119">That is hello name of hello public IP resource shown above.</span></span>

<span data-ttu-id="5e396-120">Ten slotte Hallo netwerkinterface die hierboven wordt vermeld in Hallo **Schaalaanpassingsset** eigenschap Hallo VM wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5e396-120">Finally, hello network interface above is listed in hello **networkProfile** property of hello VM being created.</span></span>

```json
      "networkProfile": {
        "networkInterfaces": [
          {
            "id": "[resourceId('Microsoft.Network/networkInterfaces', variables('webVMSetting').nicName)]"
          }
        ]
      }
```

## <a name="deploy-hello-template-by-using-click-toodeploy"></a><span data-ttu-id="5e396-121">Hallo-sjabloon implementeren met Klik toodeploy</span><span class="sxs-lookup"><span data-stu-id="5e396-121">Deploy hello template by using click toodeploy</span></span>

<span data-ttu-id="5e396-122">Hallo voorbeeldsjabloon beschikbaar in de openbare opslagplaats Hallo maakt gebruik van een parameterbestand met Hallo standaard waarden gebruikt toogenerate Hallo scenario die hierboven worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="5e396-122">hello sample template available in hello public repository uses a parameter file containing hello default values used toogenerate hello scenario described above.</span></span> <span data-ttu-id="5e396-123">toodeploy deze sjabloon met klikt u op toodeploy, klikt u op **tooAzure implementeren** in Hallo Readme.md bestand voor Hallo [VM met statische PIP](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/03-Static-public-IP) sjabloon.</span><span class="sxs-lookup"><span data-stu-id="5e396-123">toodeploy this template using click toodeploy, click **Deploy tooAzure** in hello Readme.md file for hello [VM with static PIP](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/03-Static-public-IP) template.</span></span> <span data-ttu-id="5e396-124">Hallo standaardparameterwaarden vervangen indien gewenst en voer waarden in voor Hallo leeg parameters.</span><span class="sxs-lookup"><span data-stu-id="5e396-124">Replace hello default parameter values if desired and enter values for hello blank parameters.</span></span>  <span data-ttu-id="5e396-125">Volg de instructies Hallo in Hallo portal toocreate een virtuele machine met een statische openbare IP-adres.</span><span class="sxs-lookup"><span data-stu-id="5e396-125">Follow hello instructions in hello portal toocreate a virtual machine with a static public IP address.</span></span>

## <a name="deploy-hello-template-by-using-powershell"></a><span data-ttu-id="5e396-126">Hallo-sjabloon implementeren met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="5e396-126">Deploy hello template by using PowerShell</span></span>

<span data-ttu-id="5e396-127">toodeploy hello sjabloon die u hebt gedownload met behulp van PowerShell, Hallo volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="5e396-127">toodeploy hello template you downloaded by using PowerShell, follow hello steps below.</span></span>

1. <span data-ttu-id="5e396-128">Als u Azure PowerShell nog nooit hebt gebruikt, volledige Hallo stappen voor het Hallo [hoe tooInstall en configureer Azure PowerShell](/powershell/azure/overview) artikel.</span><span class="sxs-lookup"><span data-stu-id="5e396-128">If you have never used Azure PowerShell, complete hello steps in hello [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="5e396-129">In een PowerShell-console uitvoeren Hallo `New-AzureRmResourceGroup` cmdlet toocreate een nieuwe resourcegroep, indien nodig.</span><span class="sxs-lookup"><span data-stu-id="5e396-129">In a PowerShell console, run hello `New-AzureRmResourceGroup` cmdlet toocreate a new resource group, if necessary.</span></span> <span data-ttu-id="5e396-130">Als er al een resourcegroep hebt gemaakt, gaat u toostep 3.</span><span class="sxs-lookup"><span data-stu-id="5e396-130">If you already have a resource group created, go toostep 3.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name PIPTEST -Location westus
    ```

    <span data-ttu-id="5e396-131">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="5e396-131">Expected output:</span></span>
   
        ResourceGroupName : PIPTEST
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/StaticPublicIP

3. <span data-ttu-id="5e396-132">In een PowerShell-console uitvoeren Hallo `New-AzureRmResourceGroupDeployment` cmdlet toodeploy Hallo sjabloon.</span><span class="sxs-lookup"><span data-stu-id="5e396-132">In a PowerShell console, run hello `New-AzureRmResourceGroupDeployment` cmdlet toodeploy hello template.</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name DeployVM -ResourceGroupName PIPTEST `
        -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json `
        -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json
    ```

    <span data-ttu-id="5e396-133">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="5e396-133">Expected output:</span></span>
   
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

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a><span data-ttu-id="5e396-134">Hallo-sjabloon implementeren met hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5e396-134">Deploy hello template by using hello Azure CLI</span></span>
<span data-ttu-id="5e396-135">toodeploy hello sjabloon met behulp van hello Azure CLI, volledige Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="5e396-135">toodeploy hello template by using hello Azure CLI, complete hello following steps:</span></span>

1. <span data-ttu-id="5e396-136">Als u Azure CLI nog nooit hebt gebruikt, stappen Hallo in Hallo [installeren en configureren van Azure CLI Hallo](../cli-install-nodejs.md) tooinstall artikel en configureer deze.</span><span class="sxs-lookup"><span data-stu-id="5e396-136">If you have never used Azure CLI, follow hello steps in hello [Install and Configure hello Azure CLI](../cli-install-nodejs.md) article tooinstall and configure it.</span></span>
2. <span data-ttu-id="5e396-137">Voer Hallo `azure config mode` opdracht tooswitch tooResource modus Manager, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="5e396-137">Run hello `azure config mode` command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="5e396-138">Hallo verwachte uitvoer voor Hallo bovenstaande opdracht:</span><span class="sxs-lookup"><span data-stu-id="5e396-138">hello expected output for hello command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="5e396-139">Open Hallo [parameterbestand](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json), selecteer de inhoud ervan en tooa bestand opslaan op uw computer.</span><span class="sxs-lookup"><span data-stu-id="5e396-139">Open hello [parameter file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json), select its content, and save it tooa file in your computer.</span></span> <span data-ttu-id="5e396-140">In dit voorbeeld Hallo parameters tooa-bestand met de naam worden opgeslagen *parameters.json*.</span><span class="sxs-lookup"><span data-stu-id="5e396-140">For this example, hello parameters are saved tooa file named *parameters.json*.</span></span> <span data-ttu-id="5e396-141">Hallo parameterwaarden binnen Hallo bestand desgewenst wijzigen, maar minimaal wordt aanbevolen dat u het Hallo-waarde voor Hallo adminPassword parameter tooa unieke, complex wachtwoord wijzigt.</span><span class="sxs-lookup"><span data-stu-id="5e396-141">Change hello parameter values within hello file if desired, but at a minimum, it's recommended that you change hello value for hello adminPassword parameter tooa unique, complex password.</span></span>
4. <span data-ttu-id="5e396-142">Voer Hallo `azure group deployment create` cmd toodeploy Hallo nieuwe VNet met behulp van Hallo sjabloon en de parameterbestanden die u hebt gedownload en hierboven zijn gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="5e396-142">Run hello `azure group deployment create` cmd toodeploy hello new VNet by using hello template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="5e396-143">Vervang in Hallo opdracht onderstaande <path> met Hallo pad u Hallo-bestand moet worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="5e396-143">In hello command below, replace <path> with hello path you saved hello file to.</span></span> 

    ```azurecli
    azure group create -n PIPTEST2 -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json -e <path>\parameters.json
    ```

    <span data-ttu-id="5e396-144">Verwachte uitvoer (lijsten parameterwaarden gebruikt):</span><span class="sxs-lookup"><span data-stu-id="5e396-144">Expected output (lists parameter values used):</span></span>

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

