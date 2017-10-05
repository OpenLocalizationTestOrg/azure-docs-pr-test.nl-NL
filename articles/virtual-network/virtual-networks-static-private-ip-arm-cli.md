---
title: "Configureren van privé IP-adressen voor virtuele machines - Azure CLI 2.0 | Microsoft Docs"
description: "Informatie over het configureren van privé IP-adressen voor virtuele machines met de Azure-opdrachtregelinterface (CLI) 2.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 40b03a1a-ea00-454c-b716-7574cea49ac0
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/16/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 071156367c1f819a00d31f1d0335e301391fda81
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-the-azure-cli-20"></a><span data-ttu-id="8a952-103">Privé IP-adressen voor een virtuele machine met behulp van de Azure CLI 2.0 configureren</span><span class="sxs-lookup"><span data-stu-id="8a952-103">Configure private IP addresses for a virtual machine using the Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-arm-include](../../includes/virtual-networks-static-private-ip-selectors-arm-include.md)]


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="8a952-104">CLI-versies om de taak uit te voeren</span><span class="sxs-lookup"><span data-stu-id="8a952-104">CLI versions to complete the task</span></span> 

<span data-ttu-id="8a952-105">U kunt de taak uitvoeren met behulp van een van de volgende CLI-versies:</span><span class="sxs-lookup"><span data-stu-id="8a952-105">You can complete the task using one of the following CLI versions:</span></span> 

- <span data-ttu-id="8a952-106">[Azure CLI 1.0](virtual-networks-static-private-ip-cli-nodejs.md): onze CLI voor het klassieke implementatiemodel en het Resource Manager-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="8a952-106">[Azure CLI 1.0](virtual-networks-static-private-ip-cli-nodejs.md) – our CLI for the classic and resource management deployment models</span></span> 
- <span data-ttu-id="8a952-107">[Azure CLI 2.0](#specify-a-static-private-ip-address-when-creating-a-vm) -onze volgende generatie CLI voor de resource management-implementatiemodel (in dit artikel)</span><span class="sxs-lookup"><span data-stu-id="8a952-107">[Azure CLI 2.0](#specify-a-static-private-ip-address-when-creating-a-vm) - our next generation CLI for the resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="8a952-108">Dit artikel is van toepassing op het Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="8a952-108">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="8a952-109">U kunt ook [statisch privé IP-adres in het klassieke implementatiemodel beheren](virtual-networks-static-private-ip-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="8a952-109">You can also [manage static private IP address in the classic deployment model](virtual-networks-static-private-ip-classic-cli.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

> [!NOTE]
> <span data-ttu-id="8a952-110">De Azure CLI 2.0 Voorbeeldopdrachten onderstaande verwacht een eenvoudige omgeving al gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8a952-110">The sample Azure CLI 2.0 commands below expect a simple environment already created.</span></span> <span data-ttu-id="8a952-111">Als u wilt de opdrachten uitvoeren zoals ze worden weergegeven in dit document, eerst de testomgeving wordt beschreven in bouwen [een vnet maken](virtual-networks-create-vnet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="8a952-111">If you want to run the commands as they are displayed in this document, first build the test environment described in [create a vnet](virtual-networks-create-vnet-arm-cli.md).</span></span>

## <a name="specify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="8a952-112">Bij het maken van een virtuele machine een statisch privé IP-adres opgeven</span><span class="sxs-lookup"><span data-stu-id="8a952-112">Specify a static private IP address when creating a VM</span></span>

<span data-ttu-id="8a952-113">Maken van een virtuele machine met de naam *DNS01* in de *FrontEnd* subnet van een VNet met de naam *TestVNet* met een statisch privé IP-adres van *192.168.1.101*, voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="8a952-113">To create a VM named *DNS01* in the *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow the steps below:</span></span>

1. <span data-ttu-id="8a952-114">Als u dit nog niet hebt nog installeren en configureren van de meest recente [Azure CLI 2.0](/cli/azure/install-az-cli2) en meld u aan op een Azure-account met [az aanmelding](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="8a952-114">If you haven't yet, install and configure the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span> 

2. <span data-ttu-id="8a952-115">Maken van een openbaar IP-adres voor de virtuele machine met de [az netwerk openbare ip-maken](/cli/azure/network/public-ip#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="8a952-115">Create a public IP for the VM with the [az network public-ip create](/cli/azure/network/public-ip#create) command.</span></span> <span data-ttu-id="8a952-116">De lijst die na de uitvoer wordt weergegeven, beschrijft de gebruikte parameters.</span><span class="sxs-lookup"><span data-stu-id="8a952-116">The list shown after the output explains the parameters used.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8a952-117">Mogelijk moet of wilt u met verschillende waarden voor de argumenten in deze en daaropvolgende stappen, afhankelijk van uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="8a952-117">You may want or need to use different values for your arguments in this and subsequent steps, depending upon your environment.</span></span>
   
    ```azurecli
    az network public-ip create \
    --name TestPIP \
    --resource-group TestRG \
    --location centralus \
    --allocation-method Static
    ```

    <span data-ttu-id="8a952-118">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="8a952-118">Expected output:</span></span>
   
   ```json
   {
        "publicIp": {
            "idleTimeoutInMinutes": 4,
            "ipAddress": "52.176.43.167",
            "provisioningState": "Succeeded",
            "publicIPAllocationMethod": "Static",
            "resourceGuid": "79e8baa3-33ce-466a-846c-37af3c721ce1"
        }
    }
    ```

   * <span data-ttu-id="8a952-119">`--resource-group`: De naam van de resourcegroep waarin u het openbare IP-adres maken.</span><span class="sxs-lookup"><span data-stu-id="8a952-119">`--resource-group`: Name of the resource group in which to create the public IP.</span></span>
   * <span data-ttu-id="8a952-120">`--name`: De naam van het openbare IP-adres.</span><span class="sxs-lookup"><span data-stu-id="8a952-120">`--name`: Name of the public IP.</span></span>
   * <span data-ttu-id="8a952-121">`--location`: De azure-regio waarin u het openbare IP-adres maken.</span><span class="sxs-lookup"><span data-stu-id="8a952-121">`--location`: Azure region in which to create the public IP.</span></span>

3. <span data-ttu-id="8a952-122">Voer de [az netwerk nic maken](/cli/azure/network/nic#create) opdracht voor het maken van een NIC met een statisch privé IP-adres.</span><span class="sxs-lookup"><span data-stu-id="8a952-122">Run the [az network nic create](/cli/azure/network/nic#create) command to create a NIC with a static private IP.</span></span> <span data-ttu-id="8a952-123">De lijst die na de uitvoer wordt weergegeven, beschrijft de gebruikte parameters.</span><span class="sxs-lookup"><span data-stu-id="8a952-123">The list shown after the output explains the parameters used.</span></span> 
   
    ```azurecli
    az network nic create \
    --resource-group TestRG \
    --name TestNIC \
    --location centralus \
    --subnet FrontEnd \
    --private-ip-address 192.168.1.101 \
    --vnet-name TestVNet
    ```

    <span data-ttu-id="8a952-124">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="8a952-124">Expected output:</span></span>
   
    ```json
    {
        "newNIC": {
            "dnsSettings": {
            "appliedDnsServers": [],
            "dnsServers": []
            },
            "enableIPForwarding": false,
            "ipConfigurations": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
                "name": "ipconfig1",
                "properties": {
                "primary": true,
                "privateIPAddress": "192.168.1.101",
                "privateIPAllocationMethod": "Static",
                "provisioningState": "Succeeded",
                "subnet": {
                    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "resourceGroup": "TestRG"
                }
                },
                "resourceGroup": "TestRG"
            }
            ],
            "provisioningState": "Succeeded",
            "resourceGuid": "<guid>"
        }
    }
    ```
    
    <span data-ttu-id="8a952-125">Parameters:</span><span class="sxs-lookup"><span data-stu-id="8a952-125">Parameters:</span></span>

    * <span data-ttu-id="8a952-126">`--private-ip-address`: Statische privé IP-adres voor de NIC.</span><span class="sxs-lookup"><span data-stu-id="8a952-126">`--private-ip-address`: Static private IP address for the NIC.</span></span>
    * <span data-ttu-id="8a952-127">`--vnet-name`: De naam van de VNet in te maken van de NIC.</span><span class="sxs-lookup"><span data-stu-id="8a952-127">`--vnet-name`: Name of the VNet in wihch to create the NIC.</span></span>
    * <span data-ttu-id="8a952-128">`--subnet`: De naam van het subnet in te maken van de NIC.</span><span class="sxs-lookup"><span data-stu-id="8a952-128">`--subnet`: Name of the subnet in which to create the NIC.</span></span>

4. <span data-ttu-id="8a952-129">Voer de [azure vm maken](/cli/azure/vm/nic#create) opdracht voor de virtuele machine maken met het openbare IP- en NIC die eerder is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8a952-129">Run the [azure vm create](/cli/azure/vm/nic#create) command to create the VM using the public IP and NIC created above.</span></span> <span data-ttu-id="8a952-130">De lijst die na de uitvoer wordt weergegeven, beschrijft de gebruikte parameters.</span><span class="sxs-lookup"><span data-stu-id="8a952-130">The list shown after the output explains the parameters used.</span></span>
   
    ```azurecli
    az vm create \
    --resource-group TestRG \
    --name DNS01 \
    --location centralus \
    --image Debian \
    --admin-username adminuser \
    --ssh-key-value ~/.ssh/id_rsa.pub \
    --nics TestNIC
    ```

    <span data-ttu-id="8a952-131">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="8a952-131">Expected output:</span></span>
   
    ```json
    {
        "fqdns": "",
        "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01",
        "location": "centralus",
        "macAddress": "00-0D-3A-92-C1-66",
        "powerState": "VM running",
        "privateIpAddress": "192.168.1.101",
        "publicIpAddress": "",
        "resourceGroup": "TestRG"
    }
    ```
   
   <span data-ttu-id="8a952-132">Andere parameters dan het basic [az vm maken](/cli/azure/vm#create) parameters.</span><span class="sxs-lookup"><span data-stu-id="8a952-132">Parameters other than the basic [az vm create](/cli/azure/vm#create) parameters.</span></span>

   * <span data-ttu-id="8a952-133">`--nics`: De naam van de NIC waaraan de virtuele machine is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="8a952-133">`--nics`: Name of the NIC to which the VM is attached.</span></span>
   

## <a name="retrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="8a952-134">Statische persoonlijke IP-adresgegevens voor een virtuele machine ophalen</span><span class="sxs-lookup"><span data-stu-id="8a952-134">Retrieve static private IP address information for a VM</span></span>

<span data-ttu-id="8a952-135">Als u wilt weergeven in het statische privé IP-adres dat u hebt gemaakt, voer de volgende opdracht in de Azure CLI en houd rekening met de waarden voor *toewijzingseenheid particuliere IP-methode* en *particuliere IP-adres*:</span><span class="sxs-lookup"><span data-stu-id="8a952-135">To view the static private IP address that you created, run the following Azure CLI command and observe the values for *Private IP alloc-method* and *Private IP address*:</span></span>

```azurecli
az vm show -g TestRG -n DNS01 --show-details --query 'privateIps'
```

<span data-ttu-id="8a952-136">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="8a952-136">Expected output:</span></span>

```json
"192.168.1.101"
```

<span data-ttu-id="8a952-137">Om de specifieke IP-informatie van de NIC voor deze VM weergeven, query uitvoeren op de NIC specifiek:</span><span class="sxs-lookup"><span data-stu-id="8a952-137">To display the specific IP information of the NIC for that VM, query the NIC specifically:</span></span>

```azurecli
az network nic show \
-g testrg \
-n testnic \
--query 'ipConfigurations[0].{PrivateAddress:privateIpAddress,IPVer:privateIpAddressVersion,IpAllocMethod:p
rivateIpAllocationMethod,PublicAddress:publicIpAddress}'
```

<span data-ttu-id="8a952-138">De uitvoer ziet er ongeveer zo uit:</span><span class="sxs-lookup"><span data-stu-id="8a952-138">The output is something like:</span></span>

```json
{
    "IPVer": "IPv4",
    "IpAllocMethod": "Static",
    "PrivateAddress": "192.168.1.101",
    "PublicAddress": null
}
```

## <a name="remove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="8a952-139">Een statisch privé IP-adres van een virtuele machine verwijderen</span><span class="sxs-lookup"><span data-stu-id="8a952-139">Remove a static private IP address from a VM</span></span>

<span data-ttu-id="8a952-140">U kunt een statisch privé IP-adres niet verwijderen uit een NIC in Azure CLI voor implementaties van resource manager.</span><span class="sxs-lookup"><span data-stu-id="8a952-140">You cannot remove a static private IP address from a NIC in Azure CLI for resource manager deployments.</span></span> <span data-ttu-id="8a952-141">U moet doen:</span><span class="sxs-lookup"><span data-stu-id="8a952-141">You must:</span></span>
- <span data-ttu-id="8a952-142">Maak een nieuwe NIC die gebruikmaakt van een dynamische IP-adres</span><span class="sxs-lookup"><span data-stu-id="8a952-142">Create a new NIC that uses a dynamic IP</span></span>
- <span data-ttu-id="8a952-143">De NIC ingesteld op de virtuele machine komen de zojuist gemaakte NIC.</span><span class="sxs-lookup"><span data-stu-id="8a952-143">Set the NIC on the VM do the newly created NIC.</span></span> 

<span data-ttu-id="8a952-144">Als u wilt wijzigen van de NIC voor de virtuele machine die wordt gebruikt in de bovenstaande opdrachten, de volgende stappen uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="8a952-144">To change the NIC for the VM used in the commands above, follow the steps below.</span></span>

1. <span data-ttu-id="8a952-145">Voer de **nic azure-netwerk maken** opdracht voor het maken van een nieuwe NIC met dynamische IP-toewijzing met een nieuw IP-adres.</span><span class="sxs-lookup"><span data-stu-id="8a952-145">Run the **azure network nic create** command to create a new NIC using dynamic IP allocation with a new IP address.</span></span> <span data-ttu-id="8a952-146">Houd er rekening mee omdat er geen IP-adres is opgegeven, wordt de toewijzingsmethode is **dynamische**.</span><span class="sxs-lookup"><span data-stu-id="8a952-146">Note that because no IP address is specified, the allocation method is **Dynamic**.</span></span>

    ```azurecli
    az network nic create     \
    --resource-group TestRG     \
    --name TestNIC2     \
    --location centralus     \
    --subnet FrontEnd    \
    --vnet-name TestVNet
    ```        
   
    <span data-ttu-id="8a952-147">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="8a952-147">Expected output:</span></span>

    ```json
    {
        "newNIC": {
            "dnsSettings": {
            "appliedDnsServers": [],
            "dnsServers": []
            },
            "enableIPForwarding": false,
            "ipConfigurations": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC2/ipConfigurations/ipconfig1",
                "name": "ipconfig1",
                "properties": {
                "primary": true,
                "privateIPAddress": "192.168.1.4",
                "privateIPAllocationMethod": "Dynamic",
                "provisioningState": "Succeeded",
                "subnet": {
                    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "resourceGroup": "TestRG"
                }
                },
                "resourceGroup": "TestRG"
            }
            ],
            "provisioningState": "Succeeded",
            "resourceGuid": "0808a61c-476f-4d08-98ee-0fa83671b010"
        }
    }
    ```

2. <span data-ttu-id="8a952-148">Voer de **azure vm set** opdracht de NIC die wordt gebruikt door de virtuele machine wijzigen.</span><span class="sxs-lookup"><span data-stu-id="8a952-148">Run the **azure vm set** command to change the NIC used by the VM.</span></span>
   
    ```azurecli
    azure vm set -g TestRG -n DNS01 -N TestNIC2
    ```

    <span data-ttu-id="8a952-149">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="8a952-149">Expected output:</span></span>
   
    ```json
    [
        {
            "id": "/subscriptions/0e220bf6-5caa-4e9f-8383-51f16b6c109f/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC3",
            "primary": true,
            "resourceGroup": "TestRG"
        }
    ]
    ```

    > [!NOTE]
    > <span data-ttu-id="8a952-150">Als de virtuele machine groot genoeg zijn is om meer dan één NIC hebt, voert u de **azure-netwerk nic verwijderen** opdracht voor het verwijderen van de oude NIC.</span><span class="sxs-lookup"><span data-stu-id="8a952-150">If the VM is large enough to have more than one NIC, run the **azure network nic delete** command to delete the old NIC.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="8a952-151">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8a952-151">Next steps</span></span>
* <span data-ttu-id="8a952-152">Meer informatie over [gereserveerde openbare IP-adres](virtual-networks-reserved-public-ip.md) adressen.</span><span class="sxs-lookup"><span data-stu-id="8a952-152">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="8a952-153">Meer informatie over [instantieniveau openbare IP (ILPIP)](virtual-networks-instance-level-public-ip.md) adressen.</span><span class="sxs-lookup"><span data-stu-id="8a952-153">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="8a952-154">Raadpleeg de [gereserveerd IP-REST-API's](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="8a952-154">Consult the [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

