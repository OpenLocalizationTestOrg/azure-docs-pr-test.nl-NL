---
title: een virtuele machine met meerdere NIC's - Azure CLI 1.0 aaaCreate | Microsoft Docs
description: Meer informatie over hoe toocreate met meerdere NIC's met behulp van een virtuele machine hello Azure CLI 1.0.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8e906a4b-8583-4a97-9416-ee34cfa09a98
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 07c660b632bcdc004365a6f910ecf8a5c13cbc6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-hello-azure-cli-10"></a><span data-ttu-id="73a2f-103">Een virtuele machine maken met meerdere NIC's met behulp van hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="73a2f-103">Create a VM with multiple NICs using hello Azure CLI 1.0</span></span>

[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="73a2f-104">Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="73a2f-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="73a2f-105">In dit artikel wordt beschreven hoe u Hallo Resource Manager-implementatiemodel, die Microsoft voor de meeste nieuwe implementaties in plaats van Hallo aanbeveelt [klassieke implementatiemodel](virtual-network-deploy-multinic-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="73a2f-105">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](virtual-network-deploy-multinic-classic-cli.md).</span></span>
>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="73a2f-106">Hallo volgt gebruik van een resourcegroep met de naam *IaaSStory* voor Hallo-webservers en een resourcegroep met de naam *IaaSStory-back-end* voor Hallo DB-servers.</span><span class="sxs-lookup"><span data-stu-id="73a2f-106">hello following steps use a resource group named *IaaSStory* for hello WEB servers and a resource group named *IaaSStory-BackEnd* for hello DB servers.</span></span> <span data-ttu-id="73a2f-107">U kunt deze taak uitvoeren met hello Azure CLI 1.0 (in dit artikel) of Hallo [Azure CLI 2.0](virtual-network-deploy-static-pip-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="73a2f-107">You can complete this task using hello Azure CLI 1.0 (this article) or hello [Azure CLI 2.0](virtual-network-deploy-static-pip-arm-cli.md).</span></span> <span data-ttu-id="73a2f-108">waarden in Hallo ' ' voor Hallo variabelen in Hallo stappen volgen resources met de instellingen van Hallo scenario maken.</span><span class="sxs-lookup"><span data-stu-id="73a2f-108">hello values in "" for hello variables in hello steps that follow create resources with settings from hello scenario.</span></span> <span data-ttu-id="73a2f-109">Hallo-waarden waar nodig voor uw omgeving te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="73a2f-109">Change hello values, as appropriate, for your environment.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="73a2f-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="73a2f-110">Prerequisites</span></span>
<span data-ttu-id="73a2f-111">Voordat u Hallo DB servers maken kunt, moet u toocreate hello *IaaSStory* resourcegroep met alle Hallo benodigde resources voor dit scenario.</span><span class="sxs-lookup"><span data-stu-id="73a2f-111">Before you can create hello DB servers, you need toocreate hello *IaaSStory* resource group with all hello necessary resources for this scenario.</span></span> <span data-ttu-id="73a2f-112">toocreate voltooien van deze resources Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="73a2f-112">toocreate these resources, complete hello following steps:</span></span>

1. <span data-ttu-id="73a2f-113">Navigeer te[Hallo sjabloonpagina](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span><span class="sxs-lookup"><span data-stu-id="73a2f-113">Navigate too[hello template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="73a2f-114">Hallo sjabloon pagina toohello rechts van **bovenliggende resourcegroep**, klikt u op **tooAzure implementeren**.</span><span class="sxs-lookup"><span data-stu-id="73a2f-114">In hello template page, toohello right of **Parent resource group**, click **Deploy tooAzure**.</span></span>
3. <span data-ttu-id="73a2f-115">Indien nodig, Hallo parameterwaarden te wijzigen en volg de stappen Hallo in hello Azure preview portal toodeploy Hallo-resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="73a2f-115">If needed, change hello parameter values, then follow hello steps in hello Azure preview portal toodeploy hello resource group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="73a2f-116">Zorg ervoor dat de namen van opslagaccounts uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="73a2f-116">Make sure your storage account names are unique.</span></span> <span data-ttu-id="73a2f-117">Er kan geen dubbele opslagaccountnamen in Azure.</span><span class="sxs-lookup"><span data-stu-id="73a2f-117">You cannot have duplicate storage account names in Azure.</span></span>
> 

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="create-hello-back-end-vms"></a><span data-ttu-id="73a2f-118">Hallo back-end virtuele machines maken</span><span class="sxs-lookup"><span data-stu-id="73a2f-118">Create hello back-end VMs</span></span>
<span data-ttu-id="73a2f-119">Hallo die back-end-VM's afhankelijk zijn van Hallo maken van Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="73a2f-119">hello back-end VMs depend on hello creation of hello following resources:</span></span>

* <span data-ttu-id="73a2f-120">**Storage-account voor gegevensschijven**.</span><span class="sxs-lookup"><span data-stu-id="73a2f-120">**Storage account for data disks**.</span></span> <span data-ttu-id="73a2f-121">Voor betere prestaties Hallo gegevensschijven op Hallo databaseservers Solid-State station (SSD)-technologie, waarvoor een premium storage-account gebruikt.</span><span class="sxs-lookup"><span data-stu-id="73a2f-121">For better performance, hello data disks on hello database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="73a2f-122">Zorg ervoor dat hello Azure-locatie implementeren van toosupport premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="73a2f-122">Make sure hello Azure location you deploy toosupport premium storage.</span></span>
* <span data-ttu-id="73a2f-123">**NIC's**.</span><span class="sxs-lookup"><span data-stu-id="73a2f-123">**NICs**.</span></span> <span data-ttu-id="73a2f-124">Elke virtuele machine heeft twee NIC's, één voor toegang tot de database, en één voor beheer.</span><span class="sxs-lookup"><span data-stu-id="73a2f-124">Each VM will have two NICs, one for database access, and one for management.</span></span>
* <span data-ttu-id="73a2f-125">**Beschikbaarheidsset**.</span><span class="sxs-lookup"><span data-stu-id="73a2f-125">**Availability set**.</span></span> <span data-ttu-id="73a2f-126">Alle databaseservers tooa één beschikbaarheidsset worden toegevoegd, tooensure ten minste één Hallo VM's actief is tijdens het onderhoud.</span><span class="sxs-lookup"><span data-stu-id="73a2f-126">All database servers will be added tooa single availability set, tooensure at least one of hello VMs is up and running during maintenance.</span></span>

### <a name="step-1---start-your-script"></a><span data-ttu-id="73a2f-127">Stap 1: uw script starten</span><span class="sxs-lookup"><span data-stu-id="73a2f-127">Step 1 - Start your script</span></span>
<span data-ttu-id="73a2f-128">U kunt downloaden Hallo volledige bash-script waarmee [hier](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-cli.sh).</span><span class="sxs-lookup"><span data-stu-id="73a2f-128">You can download hello full bash script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-cli.sh).</span></span> <span data-ttu-id="73a2f-129">Hallo stappen hieronder toochange Hallo script toowork in uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="73a2f-129">Follow hello steps below toochange hello script toowork in your environment.</span></span>

1. <span data-ttu-id="73a2f-130">Hallo-waarden van Hallo variabelen hieronder op basis van uw bestaande resourcegroep geïmplementeerd boven in wijzigen [vereisten](#Prerequisites).</span><span class="sxs-lookup"><span data-stu-id="73a2f-130">Change hello values of hello variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```azurecli
    existingRGName="IaaSStory"
    location="westus"
    vnetName="WTestVNet"
    backendSubnetName="BackEnd"
    remoteAccessNSGName="NSG-RemoteAccess"
    ```
2. <span data-ttu-id="73a2f-131">Hallo waarden wijzigen van Hallo variabelen hieronder op basis van waarden Hallo gewenste toouse voor uw back-end-implementatie.</span><span class="sxs-lookup"><span data-stu-id="73a2f-131">Change hello values of hello variables below based on hello values you want toouse for your backend deployment.</span></span>

    ```azurecli
    backendRGName="IaaSStory-Backend"
    prmStorageAccountName="wtestvnetstorageprm"
    avSetName="ASDB"
    vmSize="Standard_DS3"
    diskSize=127
    publisher="Canonical"
    offer="UbuntuServer"
    sku="14.04.2-LTS"
    version="latest"
    vmNamePrefix="DB"
    osDiskName="osdiskdb"
    dataDiskName="datadisk"
    nicNamePrefix="NICDB"
    ipAddressPrefix="192.168.2."
    username='adminuser'
    password='adminP@ssw0rd'
    numberOfVMs=2
    ```

3. <span data-ttu-id="73a2f-132">Hallo-ID voor Hallo ophalen `BackEnd` subnet waar Hallo virtuele machines worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="73a2f-132">Retrieve hello ID for hello `BackEnd` subnet where hello VMs will be created.</span></span> <span data-ttu-id="73a2f-133">U moet toodo dit omdat Hallo NIC's gekoppeld toobe toothis subnet zich in een andere resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="73a2f-133">You need toodo this since hello NICs toobe associated toothis subnet are in a different resource group.</span></span>

    ```azurecli
    subnetId="$(azure network vnet subnet show --resource-group $existingRGName \
            --vnet-name $vnetName \
            --name $backendSubnetName|grep Id)"
    subnetId=${subnetId#*/}
    ```

   > [!TIP]
   > <span data-ttu-id="73a2f-134">eerste opdracht hierboven gebruikt Hallo [grep](http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_04_02.html) en [manipulatie string](http://tldp.org/LDP/abs/html/string-manipulation.html) (meer specifiek, subtekenreeks verwijdering).</span><span class="sxs-lookup"><span data-stu-id="73a2f-134">hello first command above uses [grep](http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_04_02.html) and [string manipulation](http://tldp.org/LDP/abs/html/string-manipulation.html) (more specifically, substring removal).</span></span>
   >

4. <span data-ttu-id="73a2f-135">Hallo-ID voor Hallo ophalen `NSG-RemoteAccess` NSG.</span><span class="sxs-lookup"><span data-stu-id="73a2f-135">Retrieve hello ID for hello `NSG-RemoteAccess` NSG.</span></span> <span data-ttu-id="73a2f-136">U moet toodo dit omdat Hallo NIC's toobe toothis NSG in een andere resourcegroep zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="73a2f-136">You need toodo this since hello NICs toobe associated toothis NSG are in a different resource group.</span></span>

    ```azurecli
    nsgId="$(azure network nsg show --resource-group $existingRGName \
        --name $remoteAccessNSGName|grep Id)"
        nsgId=${nsgId#*/}
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="73a2f-137">Stap 2: de benodigde resources voor uw virtuele machines maken</span><span class="sxs-lookup"><span data-stu-id="73a2f-137">Step 2 - Create necessary resources for your VMs</span></span>

1. <span data-ttu-id="73a2f-138">Maak een nieuwe resourcegroep voor alle back endresources.</span><span class="sxs-lookup"><span data-stu-id="73a2f-138">Create a new resource group for all backend resources.</span></span> <span data-ttu-id="73a2f-139">Gebruik van de kennisgeving Hallo Hallo `$backendRGName` variabele voor naam resourcegroep hello, en `$location` voor hello Azure-regio.</span><span class="sxs-lookup"><span data-stu-id="73a2f-139">Notice hello use of hello `$backendRGName` variable for hello resource group name, and `$location` for hello Azure region.</span></span>

    ```azurecli
    azure group create $backendRGName $location
    ```

2. <span data-ttu-id="73a2f-140">Maak een premium storage-account voor Hallo OS en gegevens schijven toobe die wordt gebruikt door uw virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="73a2f-140">Create a premium storage account for hello OS and data disks toobe used by yours VMs.</span></span>

    ```azurecli
    azure storage account create $prmStorageAccountName \
        --resource-group $backendRGName \
        --location $location \
        --type PLRS
    ```

3. <span data-ttu-id="73a2f-141">Beschikbaarheidsset voor Hallo virtuele machines maken.</span><span class="sxs-lookup"><span data-stu-id="73a2f-141">Create an availability set for hello VMs.</span></span>

    ```azurecli
    azure availset create --resource-group $backendRGName \
        --location $location \
        --name $avSetName
    ```

### <a name="step-3---create-hello-nics-and-back-end-vms"></a><span data-ttu-id="73a2f-142">Stap 3: Hallo NIC's en back-end virtuele machines maken</span><span class="sxs-lookup"><span data-stu-id="73a2f-142">Step 3 - Create hello NICs and back-end VMs</span></span>

1. <span data-ttu-id="73a2f-143">Start een lus toocreate meerdere virtuele machines, op basis van Hallo `numberOfVMs` variabelen.</span><span class="sxs-lookup"><span data-stu-id="73a2f-143">Start a loop toocreate multiple VMs, based on hello `numberOfVMs` variables.</span></span>

    ```azurecli
    for ((suffixNumber=1;suffixNumber<=numberOfVMs;suffixNumber++));
    do
    ```

2. <span data-ttu-id="73a2f-144">Voor elke virtuele machine, maakt u een NIC voor toegang tot de database.</span><span class="sxs-lookup"><span data-stu-id="73a2f-144">For each VM, create a NIC for database access.</span></span>

    ```azurecli
    nic1Name=$nicNamePrefix$suffixNumber-DA
    x=$((suffixNumber+3))
    ipAddress1=$ipAddressPrefix$x
    azure network nic create --name $nic1Name \
        --resource-group $backendRGName \
        --location $location \
        --private-ip-address $ipAddress1 \
        --subnet-id $subnetId
    ```

3. <span data-ttu-id="73a2f-145">Maak een NIC voor externe toegang voor elke VM.</span><span class="sxs-lookup"><span data-stu-id="73a2f-145">For each VM, create a NIC for remote access.</span></span> <span data-ttu-id="73a2f-146">Kennisgeving Hallo `--network-security-group` parameter, gebruikte tooassociate Hallo NIC tooan NSG.</span><span class="sxs-lookup"><span data-stu-id="73a2f-146">Notice hello `--network-security-group` parameter, used tooassociate hello NIC tooan NSG.</span></span>

    ```azurecli
    nic2Name=$nicNamePrefix$suffixNumber-RA
    x=$((suffixNumber+53))
    ipAddress2=$ipAddressPrefix$x
    azure network nic create --name $nic2Name \
        --resource-group $backendRGName \
        --location $location \
        --private-ip-address $ipAddress2 \
        --subnet-id $subnetId $vnetName \
        --network-security-group-id $nsgId
    ```

4. <span data-ttu-id="73a2f-147">Hallo VM maken.</span><span class="sxs-lookup"><span data-stu-id="73a2f-147">Create hello VM.</span></span>

    ```azurecli
    azure vm create --resource-group $backendRGName \
        --name $vmNamePrefix$suffixNumber \
        --location $location \
        --vm-size $vmSize \
        --subnet-id $subnetId \
        --availset-name $avSetName \
        --nic-names $nic1Name,$nic2Name \
        --os-type linux \
        --image-urn $publisher:$offer:$sku:$version \
        --storage-account-name $prmStorageAccountName \
        --storage-account-container-name vhds \
        --os-disk-vhd $osDiskName$suffixNumber.vhd \
        --admin-username $username \
        --admin-password $password
    ```

5. <span data-ttu-id="73a2f-148">Voor elke VM maakt u twee gegevensschijven en end Hallo lus met Hallo `done` opdracht.</span><span class="sxs-lookup"><span data-stu-id="73a2f-148">For each VM, create two data disks, and end hello loop with hello `done` command.</span></span>

    ```azurecli
    azure vm disk attach-new --resource-group $backendRGName \
        --vm-name $vmNamePrefix$suffixNumber \
        --storage-account-name $prmStorageAccountName \
        --storage-account-container-name vhds \
        --vhd-name $dataDiskName$suffixNumber-1.vhd \
        --size-in-gb $diskSize \
        --lun 0

    azure vm disk attach-new --resource-group $backendRGName \
        --vm-name $vmNamePrefix$suffixNumber \        
        --storage-account-name $prmStorageAccountName \
        --storage-account-container-name vhds \
        --vhd-name $dataDiskName$suffixNumber-2.vhd \
        --size-in-gb $diskSize \
        --lun 1
        done
    ```

### <a name="step-4---run-hello-script"></a><span data-ttu-id="73a2f-149">Stap 4: Hallo-script uitvoeren</span><span class="sxs-lookup"><span data-stu-id="73a2f-149">Step 4 - Run hello script</span></span>
<span data-ttu-id="73a2f-150">Nu dat u hebt gedownload en gewijzigd Hallo-script op basis van uw behoeften, Hallo script toocreate Hallo terug uitvoeren end-database VM's met meerdere NIC's.</span><span class="sxs-lookup"><span data-stu-id="73a2f-150">Now that you downloaded and changed hello script based on your needs, run hello script toocreate hello back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="73a2f-151">Sla uw script en voer dit uit uw **Bash** terminal.</span><span class="sxs-lookup"><span data-stu-id="73a2f-151">Save your script and run it from your **Bash** terminal.</span></span> <span data-ttu-id="73a2f-152">U ziet Hallo initiële uitvoer, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="73a2f-152">You will see hello initial output, as shown below.</span></span>
   
        info:    Executing command group create
        info:    Getting resource group IaaSStory-Backend
        info:    Creating resource group IaaSStory-Backend
        info:    Created resource group IaaSStory-Backend
        data:    Id:                  /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend
        data:    Name:                IaaSStory-Backend
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:
        info:    group create command OK
        info:    Executing command storage account create
        info:    Creating storage account
        info:    storage account create command OK
        info:    Executing command availset create
        info:    Looking up hello availability set "ASDB"
        info:    Creating availability set "ASDB"
        info:    availset create command OK
        info:    Executing command network nic create
        info:    Looking up hello network interface "NICDB1-DA"
        info:    Creating network interface "NICDB1-DA"
        info:    Looking up hello network interface "NICDB1-DA"
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend/providers/Microsoft.Network/networkInterfaces/NICDB1-DA
        data:    Name                            : NICDB1-DA
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.2.4
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet/subnets/BackEnd
        data:
        info:    network nic create command OK
        info:    Executing command network nic create
        info:    Looking up hello network interface "NICDB1-RA"
        info:    Creating network interface "NICDB1-RA"
        info:    Looking up hello network interface "NICDB1-RA"
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend/providers/Microsoft.Network/networkInterfaces/NICDB1-RA
        data:    Name                            : NICDB1-RA
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    Network security group          : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/networkSecurityGroups/NSG-RemoteAccess
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.2.54
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet/subnets/BackEnd
        data:
        info:    network nic create command OK
        info:    Executing command vm create
        info:    Looking up hello VM "DB1"
        info:    Using hello VM Size "Standard_DS3"
        info:    hello [OS, Data] Disk or image configuration requires storage account
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    Looking up hello availability set "ASDB"
        info:    Found an Availability set "ASDB"
        info:    Looking up hello NIC "NICDB1-DA"
        info:    Looking up hello NIC "NICDB1-RA"
        info:    Creating VM "DB1"
2. <span data-ttu-id="73a2f-153">Hallo uitvoering beëindigd na een paar minuten en ziet u de rest Hallo van Hallo uitvoer zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="73a2f-153">After a few minutes, hello execution will end and you will see hello rest of hello output as shown below.</span></span>
   
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Looking up hello VM "DB1"
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk1-1.vhd
        info:    Updating VM "DB1"
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Looking up hello VM "DB1"
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk1-2.vhd
        info:    Updating VM "DB1"
        info:    vm disk attach-new command OK
        info:    Executing command network nic create
        info:    Looking up hello network interface "NICDB2-DA"
        info:    Creating network interface "NICDB2-DA"
        info:    Looking up hello network interface "NICDB2-DA"
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend/providers/Microsoft.Network/networkInterfaces/NICDB2-DA
        data:    Name                            : NICDB2-DA
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.2.5
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet/subnets/BackEnd
        data:
        info:    network nic create command OK
        info:    Executing command network nic create
        info:    Looking up hello network interface "NICDB2-RA"
        info:    Creating network interface "NICDB2-RA"
        info:    Looking up hello network interface "NICDB2-RA"
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend/providers/Microsoft.Network/networkInterfaces/NICDB2-RA
        data:    Name                            : NICDB2-RA
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    Network security group          : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/networkSecurityGroups/NSG-RemoteAccess
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.2.55
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet/subnets/BackEnd
        data:
        info:    network nic create command OK
        info:    Executing command vm create
        info:    Looking up hello VM "DB2"
        info:    Using hello VM Size "Standard_DS3"
        info:    hello [OS, Data] Disk or image configuration requires storage account
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    Looking up hello availability set "ASDB"
        info:    Found an Availability set "ASDB"
        info:    Looking up hello NIC "NICDB2-DA"
        info:    Looking up hello NIC "NICDB2-RA"
        info:    Creating VM "DB2"
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Looking up hello VM "DB2"
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk2-1.vhd
        info:    Updating VM "DB2"
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Looking up hello VM "DB2"
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk2-2.vhd
        info:    Updating VM "DB2"
        info:    vm disk attach-new command OK

