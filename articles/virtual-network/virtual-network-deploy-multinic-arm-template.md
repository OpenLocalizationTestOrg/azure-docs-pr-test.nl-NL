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
# <a name="create-a-vm-with-multiple-nics-using-a-template"></a><span data-ttu-id="c58ca-103">Een virtuele machine met meerdere NIC's met een sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="c58ca-103">Create a VM with multiple NICs using a template</span></span>
[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="c58ca-104">Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="c58ca-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="c58ca-105">In dit artikel wordt beschreven hoe u Hallo Resource Manager-implementatiemodel, die Microsoft voor de meeste nieuwe implementaties in plaats van Hallo aanbeveelt [klassieke implementatiemodel](virtual-network-deploy-multinic-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="c58ca-105">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](virtual-network-deploy-multinic-classic-ps.md).</span></span>
> 

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="c58ca-106">Hallo volgt gebruik van een resourcegroep met de naam *IaaSStory* voor Hallo-webservers en een resourcegroep met de naam *IaaSStory-back-end* voor Hallo DB-servers.</span><span class="sxs-lookup"><span data-stu-id="c58ca-106">hello following steps use a resource group named *IaaSStory* for hello WEB servers and a resource group named *IaaSStory-BackEnd* for hello DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c58ca-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c58ca-107">Prerequisites</span></span>
<span data-ttu-id="c58ca-108">Voordat u Hallo DB servers maken kunt, moet u toocreate hello *IaaSStory* resourcegroep met alle Hallo benodigde resources voor dit scenario.</span><span class="sxs-lookup"><span data-stu-id="c58ca-108">Before you can create hello DB servers, you need toocreate hello *IaaSStory* resource group with all hello necessary resources for this scenario.</span></span> <span data-ttu-id="c58ca-109">toocreate voltooien van deze resources Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="c58ca-109">toocreate these resources, complete hello following steps:</span></span>

1. <span data-ttu-id="c58ca-110">Navigeer te[Hallo sjabloonpagina](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span><span class="sxs-lookup"><span data-stu-id="c58ca-110">Navigate too[hello template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="c58ca-111">Hallo sjabloon pagina toohello rechts van **bovenliggende resourcegroep**, klikt u op **tooAzure implementeren**.</span><span class="sxs-lookup"><span data-stu-id="c58ca-111">In hello template page, toohello right of **Parent resource group**, click **Deploy tooAzure**.</span></span>
3. <span data-ttu-id="c58ca-112">Indien nodig, Hallo parameterwaarden te wijzigen en volg de stappen Hallo in hello Azure preview portal toodeploy Hallo-resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="c58ca-112">If needed, change hello parameter values, then follow hello steps in hello Azure preview portal toodeploy hello resource group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c58ca-113">Zorg ervoor dat de namen van opslagaccounts uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="c58ca-113">Make sure your storage account names are unique.</span></span> <span data-ttu-id="c58ca-114">Er kan geen dubbele opslagaccountnamen in Azure.</span><span class="sxs-lookup"><span data-stu-id="c58ca-114">You cannot have duplicate storage account names in Azure.</span></span>
> 

## <a name="understand-hello-deployment-template"></a><span data-ttu-id="c58ca-115">Hallo-implementatiesjabloon begrijpen</span><span class="sxs-lookup"><span data-stu-id="c58ca-115">Understand hello deployment template</span></span>
<span data-ttu-id="c58ca-116">Voordat u Hallo sjabloon van deze documentatie implementeert, zorg er dan voor dat u begrijpt wat het doet.</span><span class="sxs-lookup"><span data-stu-id="c58ca-116">Before you deploy hello template provided with this documentation, make sure you understand what it does.</span></span> <span data-ttu-id="c58ca-117">volgende stappen uit Hallo biedt een goed overzicht van Hallo sjabloon:</span><span class="sxs-lookup"><span data-stu-id="c58ca-117">hello following steps provide a good overview of hello template:</span></span>

1. <span data-ttu-id="c58ca-118">Navigeer te[Hallo sjabloonpagina](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span><span class="sxs-lookup"><span data-stu-id="c58ca-118">Navigate too[hello template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="c58ca-119">Klik op **azuredeploy.json** tooopen Hallo sjabloonbestand.</span><span class="sxs-lookup"><span data-stu-id="c58ca-119">Click **azuredeploy.json** tooopen hello template file.</span></span>
3. <span data-ttu-id="c58ca-120">Kennisgeving Hallo *besturingssysteemtype* parameter hieronder vermeld.</span><span class="sxs-lookup"><span data-stu-id="c58ca-120">Notice hello *osType* parameter listed below.</span></span> <span data-ttu-id="c58ca-121">Deze parameter is gebruikte tooselect welke toouse VM-installatiekopie voor de databaseserver hello, samen met meerdere besturingssysteem gerelateerde instellingen.</span><span class="sxs-lookup"><span data-stu-id="c58ca-121">This parameter is used tooselect what VM image toouse for hello database server, along with multiple operating system related settings.</span></span>

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

4. <span data-ttu-id="c58ca-122">Schuif naar beneden toohello lijst met variabelen en definitie voor Hallo Hallo **dbVMSetting** variabelen, hieronder vermeld.</span><span class="sxs-lookup"><span data-stu-id="c58ca-122">Scroll down toohello list of variables, and check hello definition for hello **dbVMSetting** variables, listed below.</span></span> <span data-ttu-id="c58ca-123">Het ontvangt een Hallo matrixelementen in Hallo **dbVMSettings** variabele.</span><span class="sxs-lookup"><span data-stu-id="c58ca-123">It receives one of hello array elements contained in hello **dbVMSettings** variable.</span></span> <span data-ttu-id="c58ca-124">Als u bekend met software development terminologie bent, kunt u bekijken Hallo **dbVMSettings** variabele als hash-tabel of een woordenlijst.</span><span class="sxs-lookup"><span data-stu-id="c58ca-124">If you are familiar with software development terminology, you can view hello **dbVMSettings** variable as a hash table, or a dictionary.</span></span>

    ```json
    "dbVMSetting": "[variables('dbVMSettings')[parameters('osType')]]"
    ```

5. <span data-ttu-id="c58ca-125">Stel dat u besluit toodeploy Windows virtuele machines waarop SQL in Hallo back-end.</span><span class="sxs-lookup"><span data-stu-id="c58ca-125">Suppose you decide toodeploy Windows VMs running SQL in hello back-end.</span></span> <span data-ttu-id="c58ca-126">Vervolgens Hallo waarde voor **besturingssysteemtype** zou *Windows*, en Hallo **dbVMSetting** variabele onderstaande Hallo-element dat staat voor de eerste waarde Hallo in Hallo zou bevatten **dbVMSettings** variabele.</span><span class="sxs-lookup"><span data-stu-id="c58ca-126">Then hello value for **osType** would be *Windows*, and hello **dbVMSetting** variable would contain hello element listed below, which represents hello first value in hello **dbVMSettings** variable.</span></span>

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

6. <span data-ttu-id="c58ca-127">Kennisgeving Hallo **vmSize** Hallo waarde bevat *Standard_DS3*.</span><span class="sxs-lookup"><span data-stu-id="c58ca-127">Notice hello **vmSize** contains hello value *Standard_DS3*.</span></span> <span data-ttu-id="c58ca-128">Hallo-gebruik van meerdere NIC's kunnen alleen bepaalde VM-grootten.</span><span class="sxs-lookup"><span data-stu-id="c58ca-128">Only certain VM sizes allow for hello use of multiple NICs.</span></span> <span data-ttu-id="c58ca-129">U kunt controleren welke VM-grootten ondersteuning voor meerdere NIC's door te lezen Hallo [Windows VM-grootten](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) en [Linux VM-grootten](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) artikelen.</span><span class="sxs-lookup"><span data-stu-id="c58ca-129">You can verify which VM sizes support multiple NICs by reading hello [Windows VM sizes](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Linux VM sizes](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) articles.</span></span>

7. <span data-ttu-id="c58ca-130">Schuif naar beneden te**resources** en kennisgeving Hallo eerste element.</span><span class="sxs-lookup"><span data-stu-id="c58ca-130">Scroll down too**resources** and notice hello first element.</span></span> <span data-ttu-id="c58ca-131">Een opslagaccount worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="c58ca-131">It describes a storage account.</span></span> <span data-ttu-id="c58ca-132">Dit opslagaccount worden gebruikte toomaintain Hallo gegevensschijven die wordt gebruikt door elke VM-database.</span><span class="sxs-lookup"><span data-stu-id="c58ca-132">This storage account will be used toomaintain hello data disks used by each database VM.</span></span> <span data-ttu-id="c58ca-133">In dit scenario wordt heeft elke database VM een besturingssysteemschijf opgeslagen in reguliere storage en twee gegevensschijven opgeslagen in (premium) SSD-opslag.</span><span class="sxs-lookup"><span data-stu-id="c58ca-133">In this scenario, each database VM has an OS disk stored in regular storage, and two data disks stored in SSD (premium) storage.</span></span>

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

8. <span data-ttu-id="c58ca-134">Schuif naar beneden toohello volgende resource, zoals hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c58ca-134">Scroll down toohello next resource, as listed below.</span></span> <span data-ttu-id="c58ca-135">Deze bron vertegenwoordigt Hallo die NIC voor toegang tot de database in elke VM-database gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c58ca-135">This resource represents hello NIC used for database access in each database VM.</span></span> <span data-ttu-id="c58ca-136">Gebruik van de kennisgeving Hallo Hallo **kopie** functie in deze resource.</span><span class="sxs-lookup"><span data-stu-id="c58ca-136">Notice hello use of hello **copy** function in this resource.</span></span> <span data-ttu-id="c58ca-137">Hallo sjabloon kunt u toodeploy veel VM's als u wilt, op basis van de Hallo **dbCount** parameter.</span><span class="sxs-lookup"><span data-stu-id="c58ca-137">hello template allows you toodeploy as many VMs as you want, based on hello **dbCount** parameter.</span></span> <span data-ttu-id="c58ca-138">Daarom moet u toocreate Hallo dezelfde hoeveelheid NIC's voor toegang tot de database, één voor elke virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c58ca-138">Therefore you need toocreate hello same amount of NICs for database access, one for each VM.</span></span>

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

9. <span data-ttu-id="c58ca-139">Schuif naar beneden toohello volgende resource, zoals hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c58ca-139">Scroll down toohello next resource, as listed below.</span></span> <span data-ttu-id="c58ca-140">Deze bron vertegenwoordigt Hallo die NIC voor beheer in elke VM-database gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c58ca-140">This resource represents hello NIC used for management in each database VM.</span></span> <span data-ttu-id="c58ca-141">Nogmaals, moet u een van deze NIC's voor elke database VM.</span><span class="sxs-lookup"><span data-stu-id="c58ca-141">Once again, you need one of these NICs for each database VM.</span></span> <span data-ttu-id="c58ca-142">Kennisgeving Hallo **networkSecurityGroup** element een NSG waarmee toegang tooRDP/SSH toothis NIC alleen koppelen.</span><span class="sxs-lookup"><span data-stu-id="c58ca-142">Notice hello **networkSecurityGroup** element, linking an NSG that allows access tooRDP/SSH toothis NIC only.</span></span>

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

10. <span data-ttu-id="c58ca-143">Schuif naar beneden toohello volgende resource, zoals hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c58ca-143">Scroll down toohello next resource, as listed below.</span></span> <span data-ttu-id="c58ca-144">Deze bron vertegenwoordigt een beschikbaarheid set toobe gedeeld door alle virtuele machines van database.</span><span class="sxs-lookup"><span data-stu-id="c58ca-144">This resource represents an availability set toobe shared by all database VMs.</span></span> <span data-ttu-id="c58ca-145">Op die manier garandeert u dat er altijd worden één virtuele machine in Hallo ingesteld tijdens het onderhoud is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c58ca-145">That way, you guarantee that there will always be one VM in hello set running during maintenance.</span></span>

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

11. <span data-ttu-id="c58ca-146">Schuif omlaag in de volgende resource toohello.</span><span class="sxs-lookup"><span data-stu-id="c58ca-146">Scroll down toohello next resource.</span></span> <span data-ttu-id="c58ca-147">Deze bron vertegenwoordigt Hallo database VM's, zoals in Hallo eerst paar regels die hieronder worden vermeld.</span><span class="sxs-lookup"><span data-stu-id="c58ca-147">This resource represents hello database VMs, as seen in hello first few lines listed below.</span></span> <span data-ttu-id="c58ca-148">Gebruik van de kennisgeving Hallo Hallo **kopie** opnieuw werkt, waarbij u ervoor zorgt dat meerdere virtuele machines worden gemaakt op basis van Hallo **dbCount** parameter.</span><span class="sxs-lookup"><span data-stu-id="c58ca-148">Notice hello use of hello **copy** function again, ensuring that multiple VMs are created based on hello **dbCount** parameter.</span></span> <span data-ttu-id="c58ca-149">Let ook op Hallo **dependsOn** verzameling.</span><span class="sxs-lookup"><span data-stu-id="c58ca-149">Also notice hello **dependsOn** collection.</span></span> <span data-ttu-id="c58ca-150">Hiermee geeft u twee NIC's wordt nodig toobe gemaakt voordat Hallo die VM is geïmplementeerd, samen met de beschikbaarheidsset hello en Hallo storage-account.</span><span class="sxs-lookup"><span data-stu-id="c58ca-150">It lists two NICs being necessary toobe created before hello VM is deployed, along with hello availability set, and hello storage account.</span></span>

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

12. <span data-ttu-id="c58ca-151">Schuif omlaag in Hallo VM resource toohello **Schaalaanpassingsset** element, zoals hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c58ca-151">Scroll down in hello VM resource toohello **networkProfile** element, as listed below.</span></span> <span data-ttu-id="c58ca-152">U ziet dat er twee NIC's wordt naslaginformatie voor elke virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c58ca-152">Notice that there are two NICs being reference for each VM.</span></span> <span data-ttu-id="c58ca-153">Als u meerdere NIC's voor een virtuele machine maakt, moet u instellen Hallo **primaire** eigenschap van een van de Hallo NIC's te*true*, en rest te Hallo*false*.</span><span class="sxs-lookup"><span data-stu-id="c58ca-153">When you create multiple NICs for a VM, you must set hello **primary** property of one of hello NICs too*true*, and hello rest too*false*.</span></span>

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

## <a name="deploy-hello-arm-template-by-using-click-toodeploy"></a><span data-ttu-id="c58ca-154">Hallo ARM-sjabloon implementeren met behulp van toodeploy klikt u op</span><span class="sxs-lookup"><span data-stu-id="c58ca-154">Deploy hello ARM template by using click toodeploy</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c58ca-155">Zorg ervoor dat u volgt Hallo [vereisten](#Pre-requisites) stappen vóór Hallo onderstaande instructies.</span><span class="sxs-lookup"><span data-stu-id="c58ca-155">Make sure you follow hello [pre-requisites](#Pre-requisites) steps before following hello instructions below.</span></span>
> 

<span data-ttu-id="c58ca-156">Hallo voorbeeldsjabloon beschikbaar in de openbare opslagplaats Hallo maakt gebruik van een parameterbestand met Hallo standaard waarden gebruikt toogenerate Hallo scenario die hierboven worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="c58ca-156">hello sample template available in hello public repository uses a parameter file containing hello default values used toogenerate hello scenario described above.</span></span> <span data-ttu-id="c58ca-157">toodeploy toodeploy, het gebruik van deze sjabloon Klik Volg [deze koppeling](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC), toohello rechts van **back-end resourcegroep (Zie de documentatie)** klikt u op **tooAzure implementeren**, vervangen Hallo standaardparameterwaarden indien nodig, en volg de instructies Hallo in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="c58ca-157">toodeploy this template using click toodeploy, follow [this link](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC), toohello right of **Backend resource group (see documentation)** click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

<span data-ttu-id="c58ca-158">Hallo afbeelding hieronder toont Hallo inhoud van de nieuwe resourcegroep hello, na de implementatie.</span><span class="sxs-lookup"><span data-stu-id="c58ca-158">hello figure below shows hello contents of hello new resource group, after deployment.</span></span>

![Back-end van resourcegroep](./media/virtual-network-deploy-multinic-arm-template/Figure2.png)

## <a name="deploy-hello-template-by-using-powershell"></a><span data-ttu-id="c58ca-160">Hallo-sjabloon implementeren met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="c58ca-160">Deploy hello template by using PowerShell</span></span>
<span data-ttu-id="c58ca-161">toodeploy hello sjabloon die u hebt gedownload met behulp van PowerShell, PowerShell installeren en configureren via Hallo stappen in Hallo [PowerShell installeren en configureren](/powershell/azure/overview) en voltooi vervolgens Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c58ca-161">toodeploy hello template you downloaded by using PowerShell, install and configure PowerShell by completing hello steps in hello [Install and configure PowerShell](/powershell/azure/overview) article and then complete hello following steps:</span></span>

<span data-ttu-id="c58ca-162">Voer Hallo  **`New-AzureRmResourceGroup`**  cmdlet toocreate een resource-groep met Hallo sjabloon.</span><span class="sxs-lookup"><span data-stu-id="c58ca-162">Run hello **`New-AzureRmResourceGroup`** cmdlet toocreate a resource group using hello template.</span></span>

```powershell
New-AzureRmResourceGroup -Name IaaSStory-Backend -Location uswest `
TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.json' `
-TemplateParameterFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json'
```

<span data-ttu-id="c58ca-163">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="c58ca-163">Expected output:</span></span>

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

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a><span data-ttu-id="c58ca-164">Hallo-sjabloon implementeren met hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c58ca-164">Deploy hello template by using hello Azure CLI</span></span>
<span data-ttu-id="c58ca-165">toodeploy hello sjabloon via Azure CLI Hallo Hallo volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="c58ca-165">toodeploy hello template by using hello Azure CLI, follow hello steps below.</span></span>

1. <span data-ttu-id="c58ca-166">Als u Azure CLI nog nooit hebt gebruikt, raadpleegt u [installeren en configureren van Azure CLI Hallo](../cli-install-nodejs.md) en volg de instructies Hallo toohello punt waar u uw Azure-account en abonnement selecteren.</span><span class="sxs-lookup"><span data-stu-id="c58ca-166">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="c58ca-167">Voer Hallo  **`azure config mode`**  opdracht tooswitch tooResource modus Manager, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c58ca-167">Run hello **`azure config mode`** command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="c58ca-168">Hallo verwachte uitvoer volgt:</span><span class="sxs-lookup"><span data-stu-id="c58ca-168">hello expected output follows:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="c58ca-169">Open Hallo [parameterbestand](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json), selecteer de inhoud en tooa bestand opslaan op uw computer.</span><span class="sxs-lookup"><span data-stu-id="c58ca-169">Open hello [parameter file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json), select its contents, and save it tooa file in your computer.</span></span> <span data-ttu-id="c58ca-170">In dit voorbeeld is opgeslagen Hallo parameterbestand te*parameters.json*.</span><span class="sxs-lookup"><span data-stu-id="c58ca-170">For this example, we saved hello parameters file too*parameters.json*.</span></span>
4. <span data-ttu-id="c58ca-171">Voer Hallo  **`azure group deployment create`**  cmdlet toodeploy Hallo nieuwe VNet met behulp van Hallo sjabloon en de parameterbestanden die u hebt gedownload en hierboven zijn gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="c58ca-171">Run hello **`azure group deployment create`** cmdlet toodeploy hello new VNet by using hello template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="c58ca-172">Hallo-lijst die wordt weergegeven na Hallo uitvoer wordt uitgelegd Hallo parameters die worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c58ca-172">hello list shown after hello output explains hello parameters used.</span></span>

    ```azurecli
    azure group create -n IaaSStory-Backend -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.json -e parameters.json
    ```

    <span data-ttu-id="c58ca-173">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="c58ca-173">Expected output:</span></span>
   
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

