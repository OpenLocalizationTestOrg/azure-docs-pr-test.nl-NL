---
title: Een virtuele machine maken met meerdere NIC's - Azure Resource Manager-sjabloon | Microsoft Docs
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
ms.openlocfilehash: 85bfa264c6cf2b0586816a47b3ab72f3aee8ec96
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-multiple-nics-using-a-template"></a><span data-ttu-id="fda6f-103">Een virtuele machine met meerdere NIC's met een sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="fda6f-103">Create a VM with multiple NICs using a template</span></span>
[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="fda6f-104">Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="fda6f-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="fda6f-105">Dit artikel bevat informatie over het Resource Manager-implementatiemodel, dat door Microsoft wordt aanbevolen voor de meeste nieuwe implementaties in plaats van het [klassieke implementatiemodel](virtual-network-deploy-multinic-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="fda6f-105">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](virtual-network-deploy-multinic-classic-ps.md).</span></span>
> 

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="fda6f-106">De volgende stappen gebruikt u een resourcegroep met de naam *IaaSStory* voor de webservers en een resourcegroep met de naam *IaaSStory-back-end* voor de database-servers.</span><span class="sxs-lookup"><span data-stu-id="fda6f-106">The following steps use a resource group named *IaaSStory* for the WEB servers and a resource group named *IaaSStory-BackEnd* for the DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fda6f-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="fda6f-107">Prerequisites</span></span>
<span data-ttu-id="fda6f-108">Voordat u de database-servers maken kunt, moet u maken de *IaaSStory* resourcegroep met alle benodigde resources voor dit scenario.</span><span class="sxs-lookup"><span data-stu-id="fda6f-108">Before you can create the DB servers, you need to create the *IaaSStory* resource group with all the necessary resources for this scenario.</span></span> <span data-ttu-id="fda6f-109">Voor het maken van deze bronnen, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="fda6f-109">To create these resources, complete the following steps:</span></span>

1. <span data-ttu-id="fda6f-110">Navigeer naar [de sjabloonpagina](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span><span class="sxs-lookup"><span data-stu-id="fda6f-110">Navigate to [the template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="fda6f-111">Op de sjabloonpagina rechts van **bovenliggende resourcegroep**, klikt u op **implementeren in Azure**.</span><span class="sxs-lookup"><span data-stu-id="fda6f-111">In the template page, to the right of **Parent resource group**, click **Deploy to Azure**.</span></span>
3. <span data-ttu-id="fda6f-112">Indien nodig, de parameterwaarden te wijzigen en volg de stappen in de Azure preview-portal voor het implementeren van de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="fda6f-112">If needed, change the parameter values, then follow the steps in the Azure preview portal to deploy the resource group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fda6f-113">Zorg ervoor dat de namen van opslagaccounts uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="fda6f-113">Make sure your storage account names are unique.</span></span> <span data-ttu-id="fda6f-114">Er kan geen dubbele opslagaccountnamen in Azure.</span><span class="sxs-lookup"><span data-stu-id="fda6f-114">You cannot have duplicate storage account names in Azure.</span></span>
> 

## <a name="understand-the-deployment-template"></a><span data-ttu-id="fda6f-115">De sjabloon voor de implementatie begrijpen</span><span class="sxs-lookup"><span data-stu-id="fda6f-115">Understand the deployment template</span></span>
<span data-ttu-id="fda6f-116">Voordat u de sjabloon van deze documentatie implementeert, zorg er dan voor dat u begrijpt wat het doet.</span><span class="sxs-lookup"><span data-stu-id="fda6f-116">Before you deploy the template provided with this documentation, make sure you understand what it does.</span></span> <span data-ttu-id="fda6f-117">De volgende stappen bevatten een goed overzicht van de sjabloon:</span><span class="sxs-lookup"><span data-stu-id="fda6f-117">The following steps provide a good overview of the template:</span></span>

1. <span data-ttu-id="fda6f-118">Navigeer naar [de sjabloonpagina](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span><span class="sxs-lookup"><span data-stu-id="fda6f-118">Navigate to [the template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="fda6f-119">Klik op **azuredeploy.json** om de sjabloonbestand te openen.</span><span class="sxs-lookup"><span data-stu-id="fda6f-119">Click **azuredeploy.json** to open the template file.</span></span>
3. <span data-ttu-id="fda6f-120">U ziet de *besturingssysteemtype* parameter hieronder vermeld.</span><span class="sxs-lookup"><span data-stu-id="fda6f-120">Notice the *osType* parameter listed below.</span></span> <span data-ttu-id="fda6f-121">Deze parameter wordt gebruikt om te selecteren welke VM-installatiekopie moet worden gebruikt voor de databaseserver, samen met meerdere besturingssysteem gerelateerde instellingen.</span><span class="sxs-lookup"><span data-stu-id="fda6f-121">This parameter is used to select what VM image to use for the database server, along with multiple operating system related settings.</span></span>

    ```json
    "osType": {
      "type": "string",
      "defaultValue": "Windows",
      "allowedValues": [
        "Windows",
        "Ubuntu"
      ],
      "metadata": {
      "description": "Type of OS to use for VMs: Windows or Ubuntu."
      }
    },
    ```

4. <span data-ttu-id="fda6f-122">Schuif helemaal naar de lijst met variabelen en controleer de definitie voor de **dbVMSetting** variabelen, hieronder vermeld.</span><span class="sxs-lookup"><span data-stu-id="fda6f-122">Scroll down to the list of variables, and check the definition for the **dbVMSetting** variables, listed below.</span></span> <span data-ttu-id="fda6f-123">Het ontvangt een van de matrixelementen in de **dbVMSettings** variabele.</span><span class="sxs-lookup"><span data-stu-id="fda6f-123">It receives one of the array elements contained in the **dbVMSettings** variable.</span></span> <span data-ttu-id="fda6f-124">Als u bekend met software development terminologie bent, vindt u de **dbVMSettings** variabele als hash-tabel of een woordenlijst.</span><span class="sxs-lookup"><span data-stu-id="fda6f-124">If you are familiar with software development terminology, you can view the **dbVMSettings** variable as a hash table, or a dictionary.</span></span>

    ```json
    "dbVMSetting": "[variables('dbVMSettings')[parameters('osType')]]"
    ```

5. <span data-ttu-id="fda6f-125">Stel dat u wilt implementeren, VM's Windows SQL uitgevoerd in de back-end.</span><span class="sxs-lookup"><span data-stu-id="fda6f-125">Suppose you decide to deploy Windows VMs running SQL in the back-end.</span></span> <span data-ttu-id="fda6f-126">Vervolgens de waarde voor **besturingssysteemtype** zou *Windows*, en de **dbVMSetting** variabele zou het hieronder vermelde element dat staat voor de eerste waarde in de bevatten**dbVMSettings** variabele.</span><span class="sxs-lookup"><span data-stu-id="fda6f-126">Then the value for **osType** would be *Windows*, and the **dbVMSetting** variable would contain the element listed below, which represents the first value in the **dbVMSettings** variable.</span></span>

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

6. <span data-ttu-id="fda6f-127">U ziet de **vmSize** bevat de waarde *Standard_DS3*.</span><span class="sxs-lookup"><span data-stu-id="fda6f-127">Notice the **vmSize** contains the value *Standard_DS3*.</span></span> <span data-ttu-id="fda6f-128">Het gebruik van meerdere NIC's kunnen alleen bepaalde VM-grootten.</span><span class="sxs-lookup"><span data-stu-id="fda6f-128">Only certain VM sizes allow for the use of multiple NICs.</span></span> <span data-ttu-id="fda6f-129">U kunt controleren welke VM-grootten ondersteunen meerdere NIC's door te lezen van de [Windows VM-grootten](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) en [Linux VM-grootten](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) artikelen.</span><span class="sxs-lookup"><span data-stu-id="fda6f-129">You can verify which VM sizes support multiple NICs by reading the [Windows VM sizes](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Linux VM sizes](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) articles.</span></span>

7. <span data-ttu-id="fda6f-130">Schuif omlaag naar **resources** en Let op het eerste element.</span><span class="sxs-lookup"><span data-stu-id="fda6f-130">Scroll down to **resources** and notice the first element.</span></span> <span data-ttu-id="fda6f-131">Een opslagaccount worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="fda6f-131">It describes a storage account.</span></span> <span data-ttu-id="fda6f-132">Dit opslagaccount wordt gebruikt de gegevensschijven die wordt gebruikt door elke VM-database te onderhouden.</span><span class="sxs-lookup"><span data-stu-id="fda6f-132">This storage account will be used to maintain the data disks used by each database VM.</span></span> <span data-ttu-id="fda6f-133">In dit scenario wordt heeft elke database VM een besturingssysteemschijf opgeslagen in reguliere storage en twee gegevensschijven opgeslagen in (premium) SSD-opslag.</span><span class="sxs-lookup"><span data-stu-id="fda6f-133">In this scenario, each database VM has an OS disk stored in regular storage, and two data disks stored in SSD (premium) storage.</span></span>

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

8. <span data-ttu-id="fda6f-134">Schuif omlaag naar de volgende resource, zoals hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="fda6f-134">Scroll down to the next resource, as listed below.</span></span> <span data-ttu-id="fda6f-135">Deze bron vertegenwoordigt de NIC die wordt gebruikt voor toegang tot de database in elke VM-database.</span><span class="sxs-lookup"><span data-stu-id="fda6f-135">This resource represents the NIC used for database access in each database VM.</span></span> <span data-ttu-id="fda6f-136">Let op het gebruik van de **kopie** functie in deze resource.</span><span class="sxs-lookup"><span data-stu-id="fda6f-136">Notice the use of the **copy** function in this resource.</span></span> <span data-ttu-id="fda6f-137">De sjabloon kunt u implementeren als veel virtuele machines als u wilt, op basis van de **dbCount** parameter.</span><span class="sxs-lookup"><span data-stu-id="fda6f-137">The template allows you to deploy as many VMs as you want, based on the **dbCount** parameter.</span></span> <span data-ttu-id="fda6f-138">Daarom moet u dezelfde hoeveelheid NIC's voor toegang tot de database, één voor elke virtuele machine maken.</span><span class="sxs-lookup"><span data-stu-id="fda6f-138">Therefore you need to create the same amount of NICs for database access, one for each VM.</span></span>

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

9. <span data-ttu-id="fda6f-139">Schuif omlaag naar de volgende resource, zoals hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="fda6f-139">Scroll down to the next resource, as listed below.</span></span> <span data-ttu-id="fda6f-140">Deze bron vertegenwoordigt de NIC die wordt gebruikt voor beheer in elke VM-database.</span><span class="sxs-lookup"><span data-stu-id="fda6f-140">This resource represents the NIC used for management in each database VM.</span></span> <span data-ttu-id="fda6f-141">Nogmaals, moet u een van deze NIC's voor elke database VM.</span><span class="sxs-lookup"><span data-stu-id="fda6f-141">Once again, you need one of these NICs for each database VM.</span></span> <span data-ttu-id="fda6f-142">U ziet de **networkSecurityGroup** element een NSG die toegang tot RDP/SSH op deze NIC alleen verleent koppelen.</span><span class="sxs-lookup"><span data-stu-id="fda6f-142">Notice the **networkSecurityGroup** element, linking an NSG that allows access to RDP/SSH to this NIC only.</span></span>

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

10. <span data-ttu-id="fda6f-143">Schuif omlaag naar de volgende resource, zoals hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="fda6f-143">Scroll down to the next resource, as listed below.</span></span> <span data-ttu-id="fda6f-144">Deze bron vertegenwoordigt een beschikbaarheidsset moeten worden gedeeld door alle virtuele machines van database.</span><span class="sxs-lookup"><span data-stu-id="fda6f-144">This resource represents an availability set to be shared by all database VMs.</span></span> <span data-ttu-id="fda6f-145">Op die manier garandeert u dat er altijd worden één virtuele machine in de set uitvoeren tijdens onderhoud.</span><span class="sxs-lookup"><span data-stu-id="fda6f-145">That way, you guarantee that there will always be one VM in the set running during maintenance.</span></span>

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

11. <span data-ttu-id="fda6f-146">Schuif omlaag naar de volgende resource.</span><span class="sxs-lookup"><span data-stu-id="fda6f-146">Scroll down to the next resource.</span></span> <span data-ttu-id="fda6f-147">Deze bron vertegenwoordigt de database VM's, zoals weergegeven in de eerste paar regels die hieronder worden vermeld.</span><span class="sxs-lookup"><span data-stu-id="fda6f-147">This resource represents the database VMs, as seen in the first few lines listed below.</span></span> <span data-ttu-id="fda6f-148">Let op het gebruik van de **kopie** werken opnieuw, waarbij u ervoor zorgt dat meerdere virtuele machines worden gemaakt op basis van de **dbCount** parameter.</span><span class="sxs-lookup"><span data-stu-id="fda6f-148">Notice the use of the **copy** function again, ensuring that multiple VMs are created based on the **dbCount** parameter.</span></span> <span data-ttu-id="fda6f-149">Ook ziet de **dependsOn** verzameling.</span><span class="sxs-lookup"><span data-stu-id="fda6f-149">Also notice the **dependsOn** collection.</span></span> <span data-ttu-id="fda6f-150">Hiermee geeft u twee NIC's die nodig zijn om te worden gemaakt voordat de virtuele machine is geïmplementeerd, samen met de beschikbaarheidsset en het opslagaccount wordt.</span><span class="sxs-lookup"><span data-stu-id="fda6f-150">It lists two NICs being necessary to be created before the VM is deployed, along with the availability set, and the storage account.</span></span>

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

12. <span data-ttu-id="fda6f-151">Schuif omlaag in de VM-resource toe aan de **Schaalaanpassingsset** element, zoals hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="fda6f-151">Scroll down in the VM resource to the **networkProfile** element, as listed below.</span></span> <span data-ttu-id="fda6f-152">U ziet dat er twee NIC's wordt naslaginformatie voor elke virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="fda6f-152">Notice that there are two NICs being reference for each VM.</span></span> <span data-ttu-id="fda6f-153">Als u meerdere NIC's voor een virtuele machine maakt, moet u instellen de **primaire** eigenschap van een van de NIC's voor *true*, en de rest aan *false*.</span><span class="sxs-lookup"><span data-stu-id="fda6f-153">When you create multiple NICs for a VM, you must set the **primary** property of one of the NICs to *true*, and the rest to *false*.</span></span>

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

## <a name="deploy-the-arm-template-by-using-click-to-deploy"></a><span data-ttu-id="fda6f-154">De ARM-sjabloon implementeren met klik om te implementeren</span><span class="sxs-lookup"><span data-stu-id="fda6f-154">Deploy the ARM template by using click to deploy</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fda6f-155">Zorg ervoor dat u volgt de [vereisten](#Pre-requisites) stappen vóór de onderstaande instructies.</span><span class="sxs-lookup"><span data-stu-id="fda6f-155">Make sure you follow the [pre-requisites](#Pre-requisites) steps before following the instructions below.</span></span>
> 

<span data-ttu-id="fda6f-156">De voorbeeldsjabloon in de openbare opslagplaats maakt gebruik van een parameterbestand dat de standaardwaarden bevat voor het genereren van het hierboven beschreven scenario.</span><span class="sxs-lookup"><span data-stu-id="fda6f-156">The sample template available in the public repository uses a parameter file containing the default values used to generate the scenario described above.</span></span> <span data-ttu-id="fda6f-157">Volg voor het implementeren van deze sjabloon implementeren met Klik [deze koppeling](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC), rechts van **back-end resourcegroep (Zie de documentatie)** klikt u op **implementeren in Azure**, vervang de standaard parameterwaarden indien nodig, en volg de instructies in de portal.</span><span class="sxs-lookup"><span data-stu-id="fda6f-157">To deploy this template using click to deploy, follow [this link](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC), to the right of **Backend resource group (see documentation)** click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span>

<span data-ttu-id="fda6f-158">De afbeelding hieronder ziet de inhoud van de nieuwe resourcegroep na de implementatie.</span><span class="sxs-lookup"><span data-stu-id="fda6f-158">The figure below shows the contents of the new resource group, after deployment.</span></span>

![Back-end van resourcegroep](./media/virtual-network-deploy-multinic-arm-template/Figure2.png)

## <a name="deploy-the-template-by-using-powershell"></a><span data-ttu-id="fda6f-160">De sjabloon implementeren met PowerShell</span><span class="sxs-lookup"><span data-stu-id="fda6f-160">Deploy the template by using PowerShell</span></span>
<span data-ttu-id="fda6f-161">Voor het implementeren van de sjabloon die u hebt gedownload met behulp van PowerShell PowerShell installeren en configureren via de stappen in de [PowerShell installeren en configureren](/powershell/azure/overview) en voltooi vervolgens de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="fda6f-161">To deploy the template you downloaded by using PowerShell, install and configure PowerShell by completing the steps in the [Install and configure PowerShell](/powershell/azure/overview) article and then complete the following steps:</span></span>

<span data-ttu-id="fda6f-162">Voer de  **`New-AzureRmResourceGroup`**  cmdlet om een resourcegroep met de sjabloon te maken.</span><span class="sxs-lookup"><span data-stu-id="fda6f-162">Run the **`New-AzureRmResourceGroup`** cmdlet to create a resource group using the template.</span></span>

```powershell
New-AzureRmResourceGroup -Name IaaSStory-Backend -Location uswest `
TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.json' `
-TemplateParameterFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json'
```

<span data-ttu-id="fda6f-163">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="fda6f-163">Expected output:</span></span>

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

## <a name="deploy-the-template-by-using-the-azure-cli"></a><span data-ttu-id="fda6f-164">De sjabloon implementeren met de Azure CLI</span><span class="sxs-lookup"><span data-stu-id="fda6f-164">Deploy the template by using the Azure CLI</span></span>
<span data-ttu-id="fda6f-165">Volg onderstaande stappen als u de sjabloon wilt implementeren met de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="fda6f-165">To deploy the template by using the Azure CLI, follow the steps below.</span></span>

1. <span data-ttu-id="fda6f-166">Als u Azure CLI nog nooit hebt gebruikt, raadpleegt u [De Azure CLI installeren en configureren](../cli-install-nodejs.md) en volgt u de instructies tot het punt waar u uw Azure-account en -abonnement moet selecteren.</span><span class="sxs-lookup"><span data-stu-id="fda6f-166">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="fda6f-167">Voer de opdracht **`azure config mode`** uit om over te schakelen naar de modus Resource Manager, zoals hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="fda6f-167">Run the **`azure config mode`** command to switch to Resource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="fda6f-168">Hier volgt de verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="fda6f-168">The expected output follows:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="fda6f-169">Open de [parameterbestand](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json), selecteer de inhoud en sla deze op een bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="fda6f-169">Open the [parameter file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json), select its contents, and save it to a file in your computer.</span></span> <span data-ttu-id="fda6f-170">Hier is het parameterbestand opgeslagen als *parameters.json*.</span><span class="sxs-lookup"><span data-stu-id="fda6f-170">For this example, we saved the parameters file to *parameters.json*.</span></span>
4. <span data-ttu-id="fda6f-171">Voer de **`azure group deployment create`** cmdlet uit om de nieuwe VNet te implementeren met behulp van de sjabloon en de parameterbestanden die u hebt gedownload en hierboven zijn gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="fda6f-171">Run the **`azure group deployment create`** cmdlet to deploy the new VNet by using the template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="fda6f-172">De lijst die na de uitvoer wordt weergegeven, beschrijft de gebruikte parameters.</span><span class="sxs-lookup"><span data-stu-id="fda6f-172">The list shown after the output explains the parameters used.</span></span>

    ```azurecli
    azure group create -n IaaSStory-Backend -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.json -e parameters.json
    ```

    <span data-ttu-id="fda6f-173">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="fda6f-173">Expected output:</span></span>
   
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

