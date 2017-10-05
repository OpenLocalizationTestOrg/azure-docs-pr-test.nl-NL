---
title: Een virtuele machine maken met statische openbare IP-adres - Azure Resource Manager-sjabloon | Microsoft Docs
description: Informatie over het maken van een virtuele machine met een statische openbare IP-adres met een Azure Resource Manager-sjabloon.
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
ms.openlocfilehash: 2f503aa60fdd9b7cf66ef482a1041e34c88e5c01
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-an-azure-resource-manager-template"></a><span data-ttu-id="814bf-103">Een virtuele machine maken met een statisch openbaar IP-adres met een Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="814bf-103">Create a VM with a static public IP address using an Azure Resource Manager template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="814bf-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="814bf-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="814bf-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="814bf-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="814bf-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="814bf-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="814bf-107">Sjabloon</span><span class="sxs-lookup"><span data-stu-id="814bf-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="814bf-108">PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="814bf-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="814bf-109">Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="814bf-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="814bf-110">In dit artikel wordt behandeld met het implementatiemodel van Resource Manager, die Microsoft voor de meeste nieuwe implementaties in plaats van het klassieke implementatiemodel aanbeveelt.</span><span class="sxs-lookup"><span data-stu-id="814bf-110">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="public-ip-address-resources-in-a-template-file"></a><span data-ttu-id="814bf-111">Openbare IP-adres resources in een sjabloonbestand</span><span class="sxs-lookup"><span data-stu-id="814bf-111">Public IP address resources in a template file</span></span>
<span data-ttu-id="814bf-112">U kunt bekijken en download de [voorbeeldsjabloon](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="814bf-112">You can view and download the [sample template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json).</span></span>

<span data-ttu-id="814bf-113">De volgende sectie ziet u de definitie van het openbare IP-resource, op basis van de bovenstaande scenario:</span><span class="sxs-lookup"><span data-stu-id="814bf-113">The following section shows the definition of the public IP resource, based on the scenario above:</span></span>

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

<span data-ttu-id="814bf-114">U ziet de **publicIPAllocationMethod** eigenschap die is ingesteld op *statische*.</span><span class="sxs-lookup"><span data-stu-id="814bf-114">Notice the **publicIPAllocationMethod** property, which is set to *Static*.</span></span> <span data-ttu-id="814bf-115">Deze eigenschap kan zijn *dynamische* (standaardwaarde) of *statische*.</span><span class="sxs-lookup"><span data-stu-id="814bf-115">This property can be either *Dynamic* (default value) or *Static*.</span></span> <span data-ttu-id="814bf-116">Instellen op statisch wordt gegarandeerd dat het openbare IP-adres toegewezen nooit wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="814bf-116">Setting it to static guarantees that the public IP address assigned will never change.</span></span>

<span data-ttu-id="814bf-117">De volgende sectie ziet u de koppeling van het openbare IP-adres aan een netwerkinterface:</span><span class="sxs-lookup"><span data-stu-id="814bf-117">The following section shows the association of the public IP address with a network interface:</span></span>

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

<span data-ttu-id="814bf-118">U ziet de **publicIPAddress** eigenschap die verwijst naar de **Id** van een resource met de naam **variables('webVMSetting').pipName**.</span><span class="sxs-lookup"><span data-stu-id="814bf-118">Notice the **publicIPAddress** property pointing to the **Id** of a resource named **variables('webVMSetting').pipName**.</span></span> <span data-ttu-id="814bf-119">Dat is de naam van het openbare IP-resource hierboven weergegeven.</span><span class="sxs-lookup"><span data-stu-id="814bf-119">That is the name of the public IP resource shown above.</span></span>

<span data-ttu-id="814bf-120">Ten slotte de netwerkinterface die hierboven wordt vermeld in de **Schaalaanpassingsset** eigenschap van de virtuele machine wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="814bf-120">Finally, the network interface above is listed in the **networkProfile** property of the VM being created.</span></span>

```json
      "networkProfile": {
        "networkInterfaces": [
          {
            "id": "[resourceId('Microsoft.Network/networkInterfaces', variables('webVMSetting').nicName)]"
          }
        ]
      }
```

## <a name="deploy-the-template-by-using-click-to-deploy"></a><span data-ttu-id="814bf-121">De sjabloon implementeren met Klik om te implementeren</span><span class="sxs-lookup"><span data-stu-id="814bf-121">Deploy the template by using click to deploy</span></span>

<span data-ttu-id="814bf-122">De voorbeeldsjabloon in de openbare opslagplaats maakt gebruik van een parameterbestand dat de standaardwaarden bevat voor het genereren van het hierboven beschreven scenario.</span><span class="sxs-lookup"><span data-stu-id="814bf-122">The sample template available in the public repository uses a parameter file containing the default values used to generate the scenario described above.</span></span> <span data-ttu-id="814bf-123">Deze als sjabloon wilt implementeren met Klik om te implementeren, klikt u op **implementeren in Azure** in het bestand Readme.md voor de [VM met statische PIP](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/03-Static-public-IP) sjabloon.</span><span class="sxs-lookup"><span data-stu-id="814bf-123">To deploy this template using click to deploy, click **Deploy to Azure** in the Readme.md file for the [VM with static PIP](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/03-Static-public-IP) template.</span></span> <span data-ttu-id="814bf-124">De standaardwaarden voor de parameter vervangen indien gewenst en voer waarden in voor de lege parameters.</span><span class="sxs-lookup"><span data-stu-id="814bf-124">Replace the default parameter values if desired and enter values for the blank parameters.</span></span>  <span data-ttu-id="814bf-125">Volg de instructies in de portal voor het maken van een virtuele machine met een statisch openbaar IP-adres.</span><span class="sxs-lookup"><span data-stu-id="814bf-125">Follow the instructions in the portal to create a virtual machine with a static public IP address.</span></span>

## <a name="deploy-the-template-by-using-powershell"></a><span data-ttu-id="814bf-126">De sjabloon implementeren met PowerShell</span><span class="sxs-lookup"><span data-stu-id="814bf-126">Deploy the template by using PowerShell</span></span>

<span data-ttu-id="814bf-127">Volg onderstaande stappen als u de sjabloon die u hebt gedownload, wilt implementeren met PowerShell.</span><span class="sxs-lookup"><span data-stu-id="814bf-127">To deploy the template you downloaded by using PowerShell, follow the steps below.</span></span>

1. <span data-ttu-id="814bf-128">Als u Azure PowerShell nog nooit hebt gebruikt, voer de stappen in de [installeren en configureren van Azure PowerShell](/powershell/azure/overview) artikel.</span><span class="sxs-lookup"><span data-stu-id="814bf-128">If you have never used Azure PowerShell, complete the steps in the [How to Install and Configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="814bf-129">Voer in een PowerShell-console de `New-AzureRmResourceGroup` cmdlet indien nodig een nieuwe resourcegroep maken.</span><span class="sxs-lookup"><span data-stu-id="814bf-129">In a PowerShell console, run the `New-AzureRmResourceGroup` cmdlet to create a new resource group, if necessary.</span></span> <span data-ttu-id="814bf-130">Als er al een resourcegroep hebt gemaakt, gaat u naar stap 3.</span><span class="sxs-lookup"><span data-stu-id="814bf-130">If you already have a resource group created, go to step 3.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name PIPTEST -Location westus
    ```

    <span data-ttu-id="814bf-131">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="814bf-131">Expected output:</span></span>
   
        ResourceGroupName : PIPTEST
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/StaticPublicIP

3. <span data-ttu-id="814bf-132">Voer in een PowerShell-console de `New-AzureRmResourceGroupDeployment` cmdlet om de sjabloon te implementeren.</span><span class="sxs-lookup"><span data-stu-id="814bf-132">In a PowerShell console, run the `New-AzureRmResourceGroupDeployment` cmdlet to deploy the template.</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name DeployVM -ResourceGroupName PIPTEST `
        -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json `
        -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json
    ```

    <span data-ttu-id="814bf-133">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="814bf-133">Expected output:</span></span>
   
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

## <a name="deploy-the-template-by-using-the-azure-cli"></a><span data-ttu-id="814bf-134">De sjabloon implementeren met de Azure CLI</span><span class="sxs-lookup"><span data-stu-id="814bf-134">Deploy the template by using the Azure CLI</span></span>
<span data-ttu-id="814bf-135">Als u wilt de sjabloon implementeren met behulp van de Azure CLI, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="814bf-135">To deploy the template by using the Azure CLI, complete the following steps:</span></span>

1. <span data-ttu-id="814bf-136">Als u Azure CLI nog nooit hebt gebruikt, volg de stappen in de [installeren en configureren van de Azure CLI](../cli-install-nodejs.md) artikel om te installeren en configureren.</span><span class="sxs-lookup"><span data-stu-id="814bf-136">If you have never used Azure CLI, follow the steps in the [Install and Configure the Azure CLI](../cli-install-nodejs.md) article to install and configure it.</span></span>
2. <span data-ttu-id="814bf-137">Voer de `azure config mode` opdracht overschakelen naar de modus Resource Manager, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="814bf-137">Run the `azure config mode` command to switch to Resource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="814bf-138">De verwachte uitvoer voor de bovenstaande opdracht:</span><span class="sxs-lookup"><span data-stu-id="814bf-138">The expected output for the command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="814bf-139">Open de [parameterbestand](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json), selecteer de inhoud ervan en sla deze op een bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="814bf-139">Open the [parameter file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json), select its content, and save it to a file in your computer.</span></span> <span data-ttu-id="814bf-140">Bijvoorbeeld, de parameters worden opgeslagen in een bestand met de naam *parameters.json*.</span><span class="sxs-lookup"><span data-stu-id="814bf-140">For this example, the parameters are saved to a file named *parameters.json*.</span></span> <span data-ttu-id="814bf-141">De parameterwaarden in het bestand desgewenst wijzigen, maar minimaal wordt aanbevolen dat u de waarde voor de parameter adminPassword naar een unieke, complex wachtwoord wijzigen.</span><span class="sxs-lookup"><span data-stu-id="814bf-141">Change the parameter values within the file if desired, but at a minimum, it's recommended that you change the value for the adminPassword parameter to a unique, complex password.</span></span>
4. <span data-ttu-id="814bf-142">Voer de `azure group deployment create` cmd naar de nieuwe VNet te implementeren met behulp van de sjabloon en de parameterbestanden die u hebt gedownload en hierboven zijn gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="814bf-142">Run the `azure group deployment create` cmd to deploy the new VNet by using the template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="814bf-143">Vervang in de onderstaande opdracht <path> met het pad u het bestand moet worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="814bf-143">In the command below, replace <path> with the path you saved the file to.</span></span> 

    ```azurecli
    azure group create -n PIPTEST2 -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json -e <path>\parameters.json
    ```

    <span data-ttu-id="814bf-144">Verwachte uitvoer (lijsten parameterwaarden gebruikt):</span><span class="sxs-lookup"><span data-stu-id="814bf-144">Expected output (lists parameter values used):</span></span>

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

