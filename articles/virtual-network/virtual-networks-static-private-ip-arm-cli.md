---
title: "privé IP-adressen voor virtuele machines - Azure CLI 2.0 aaaConfigure | Microsoft Docs"
description: "Meer informatie over hoe tooconfigure privé IP-adressen voor virtuele machines met hello Azure-opdrachtregelinterface (CLI) 2.0."
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
ms.openlocfilehash: 0e278e6ac63c0cda061cf70ab0edfaff5491c03b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-cli-20"></a><span data-ttu-id="3f08f-103">Privé IP-adressen voor een virtuele machine met behulp van Azure CLI 2.0 Hallo configureren</span><span class="sxs-lookup"><span data-stu-id="3f08f-103">Configure private IP addresses for a virtual machine using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-arm-include](../../includes/virtual-networks-static-private-ip-selectors-arm-include.md)]


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="3f08f-104">CLI-versies toocomplete Hallo taak</span><span class="sxs-lookup"><span data-stu-id="3f08f-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="3f08f-105">U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="3f08f-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="3f08f-106">[Azure CLI 1.0](virtual-networks-static-private-ip-cli-nodejs.md) – onze CLI voor Hallo klassieke en resource management implementatiemodellen</span><span class="sxs-lookup"><span data-stu-id="3f08f-106">[Azure CLI 1.0](virtual-networks-static-private-ip-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span> 
- <span data-ttu-id="3f08f-107">[Azure CLI 2.0](#specify-a-static-private-ip-address-when-creating-a-vm) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel (in dit artikel)</span><span class="sxs-lookup"><span data-stu-id="3f08f-107">[Azure CLI 2.0](#specify-a-static-private-ip-address-when-creating-a-vm) - our next generation CLI for hello resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="3f08f-108">In dit artikel bevat informatie over Hallo Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="3f08f-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="3f08f-109">U kunt ook [statisch privé IP-adres in het klassieke implementatiemodel Hallo beheren](virtual-networks-static-private-ip-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="3f08f-109">You can also [manage static private IP address in hello classic deployment model](virtual-networks-static-private-ip-classic-cli.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

> [!NOTE]
> <span data-ttu-id="3f08f-110">Hello Azure CLI 2.0 Voorbeeldopdrachten onderstaande verwacht een eenvoudige omgeving al gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3f08f-110">hello sample Azure CLI 2.0 commands below expect a simple environment already created.</span></span> <span data-ttu-id="3f08f-111">Als u toorun Hallo opdrachten wilt zoals ze worden weergegeven in dit document, eerst bouwen Hallo testomgeving beschreven in [een vnet maken](virtual-networks-create-vnet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="3f08f-111">If you want toorun hello commands as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-arm-cli.md).</span></span>

## <a name="specify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="3f08f-112">Bij het maken van een virtuele machine een statisch privé IP-adres opgeven</span><span class="sxs-lookup"><span data-stu-id="3f08f-112">Specify a static private IP address when creating a VM</span></span>

<span data-ttu-id="3f08f-113">een virtuele machine met de naam toocreate *DNS01* in Hallo *FrontEnd* subnet van een VNet met de naam *TestVNet* met een statisch privé IP-adres van *192.168.1.101*, Volg onderstaande stappen voor Hallo:</span><span class="sxs-lookup"><span data-stu-id="3f08f-113">toocreate a VM named *DNS01* in hello *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow hello steps below:</span></span>

1. <span data-ttu-id="3f08f-114">Als u dit nog niet hebt nog installeren en configureren van Hallo meest recente [Azure CLI 2.0](/cli/azure/install-az-cli2) en meld u bij het gebruik van de Azure-account tooan [az aanmelding](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="3f08f-114">If you haven't yet, install and configure hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span> 

2. <span data-ttu-id="3f08f-115">Maken van een openbaar IP-adres voor Hallo VM Hello [az netwerk openbare ip-maken](/cli/azure/network/public-ip#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="3f08f-115">Create a public IP for hello VM with hello [az network public-ip create](/cli/azure/network/public-ip#create) command.</span></span> <span data-ttu-id="3f08f-116">Hallo-lijst die wordt weergegeven na Hallo uitvoer wordt uitgelegd Hallo parameters die worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="3f08f-116">hello list shown after hello output explains hello parameters used.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3f08f-117">Mogelijk moet of wilt u verschillende waarden voor uw argumenten in deze toouse en daaropvolgende stappen, afhankelijk van uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="3f08f-117">You may want or need toouse different values for your arguments in this and subsequent steps, depending upon your environment.</span></span>
   
    ```azurecli
    az network public-ip create \
    --name TestPIP \
    --resource-group TestRG \
    --location centralus \
    --allocation-method Static
    ```

    <span data-ttu-id="3f08f-118">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="3f08f-118">Expected output:</span></span>
   
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

   * <span data-ttu-id="3f08f-119">`--resource-group`: Naam van de resourcegroep Hallo in welke toocreate Hallo openbare IP-adres.</span><span class="sxs-lookup"><span data-stu-id="3f08f-119">`--resource-group`: Name of hello resource group in which toocreate hello public IP.</span></span>
   * <span data-ttu-id="3f08f-120">`--name`: De naam van Hallo openbare IP-adres.</span><span class="sxs-lookup"><span data-stu-id="3f08f-120">`--name`: Name of hello public IP.</span></span>
   * <span data-ttu-id="3f08f-121">`--location`: De azure-regio in welke toocreate Hallo openbare IP-adres.</span><span class="sxs-lookup"><span data-stu-id="3f08f-121">`--location`: Azure region in which toocreate hello public IP.</span></span>

3. <span data-ttu-id="3f08f-122">Voer Hallo [az netwerk nic maken](/cli/azure/network/nic#create) opdracht toocreate een NIC met een statisch privé IP-adres.</span><span class="sxs-lookup"><span data-stu-id="3f08f-122">Run hello [az network nic create](/cli/azure/network/nic#create) command toocreate a NIC with a static private IP.</span></span> <span data-ttu-id="3f08f-123">Hallo-lijst die wordt weergegeven na Hallo uitvoer wordt uitgelegd Hallo parameters die worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="3f08f-123">hello list shown after hello output explains hello parameters used.</span></span> 
   
    ```azurecli
    az network nic create \
    --resource-group TestRG \
    --name TestNIC \
    --location centralus \
    --subnet FrontEnd \
    --private-ip-address 192.168.1.101 \
    --vnet-name TestVNet
    ```

    <span data-ttu-id="3f08f-124">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="3f08f-124">Expected output:</span></span>
   
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
    
    <span data-ttu-id="3f08f-125">Parameters:</span><span class="sxs-lookup"><span data-stu-id="3f08f-125">Parameters:</span></span>

    * <span data-ttu-id="3f08f-126">`--private-ip-address`: Statische privé IP-adres voor Hallo NIC.</span><span class="sxs-lookup"><span data-stu-id="3f08f-126">`--private-ip-address`: Static private IP address for hello NIC.</span></span>
    * <span data-ttu-id="3f08f-127">`--vnet-name`: De naam van Hallo VNet in welke toocreate Hallo NIC.</span><span class="sxs-lookup"><span data-stu-id="3f08f-127">`--vnet-name`: Name of hello VNet in wihch toocreate hello NIC.</span></span>
    * <span data-ttu-id="3f08f-128">`--subnet`: De naam van Hallo subnet in welke toocreate Hallo NIC.</span><span class="sxs-lookup"><span data-stu-id="3f08f-128">`--subnet`: Name of hello subnet in which toocreate hello NIC.</span></span>

4. <span data-ttu-id="3f08f-129">Voer Hallo [azure vm maken](/cli/azure/vm/nic#create) opdracht toocreate Hallo VM die gebruikmaakt van Hallo openbare IP-adres en NIC die eerder is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3f08f-129">Run hello [azure vm create](/cli/azure/vm/nic#create) command toocreate hello VM using hello public IP and NIC created above.</span></span> <span data-ttu-id="3f08f-130">Hallo-lijst die wordt weergegeven na Hallo uitvoer wordt uitgelegd Hallo parameters die worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="3f08f-130">hello list shown after hello output explains hello parameters used.</span></span>
   
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

    <span data-ttu-id="3f08f-131">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="3f08f-131">Expected output:</span></span>
   
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
   
   <span data-ttu-id="3f08f-132">Andere parameters dan Hallo basic [az vm maken](/cli/azure/vm#create) parameters.</span><span class="sxs-lookup"><span data-stu-id="3f08f-132">Parameters other than hello basic [az vm create](/cli/azure/vm#create) parameters.</span></span>

   * <span data-ttu-id="3f08f-133">`--nics`: De naam van Hallo NIC toowhich Hallo VM is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="3f08f-133">`--nics`: Name of hello NIC toowhich hello VM is attached.</span></span>
   

## <a name="retrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="3f08f-134">Statische persoonlijke IP-adresgegevens voor een virtuele machine ophalen</span><span class="sxs-lookup"><span data-stu-id="3f08f-134">Retrieve static private IP address information for a VM</span></span>

<span data-ttu-id="3f08f-135">tooview hello statisch privé IP-adres dat u hebt gemaakt, Hallo na Azure CLI-opdracht uitgevoerd en zien Hallo waarden voor *toewijzingseenheid particuliere IP-methode* en *particuliere IP-adres*:</span><span class="sxs-lookup"><span data-stu-id="3f08f-135">tooview hello static private IP address that you created, run hello following Azure CLI command and observe hello values for *Private IP alloc-method* and *Private IP address*:</span></span>

```azurecli
az vm show -g TestRG -n DNS01 --show-details --query 'privateIps'
```

<span data-ttu-id="3f08f-136">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="3f08f-136">Expected output:</span></span>

```json
"192.168.1.101"
```

<span data-ttu-id="3f08f-137">toodisplay Hallo specifiek specifieke IP-informatie van Hallo NIC voor die VM, query Hallo NIC:</span><span class="sxs-lookup"><span data-stu-id="3f08f-137">toodisplay hello specific IP information of hello NIC for that VM, query hello NIC specifically:</span></span>

```azurecli
az network nic show \
-g testrg \
-n testnic \
--query 'ipConfigurations[0].{PrivateAddress:privateIpAddress,IPVer:privateIpAddressVersion,IpAllocMethod:p
rivateIpAllocationMethod,PublicAddress:publicIpAddress}'
```

<span data-ttu-id="3f08f-138">Hallo uitvoer ziet er ongeveer als volgt:</span><span class="sxs-lookup"><span data-stu-id="3f08f-138">hello output is something like:</span></span>

```json
{
    "IPVer": "IPv4",
    "IpAllocMethod": "Static",
    "PrivateAddress": "192.168.1.101",
    "PublicAddress": null
}
```

## <a name="remove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="3f08f-139">Een statisch privé IP-adres van een virtuele machine verwijderen</span><span class="sxs-lookup"><span data-stu-id="3f08f-139">Remove a static private IP address from a VM</span></span>

<span data-ttu-id="3f08f-140">U kunt een statisch privé IP-adres niet verwijderen uit een NIC in Azure CLI voor implementaties van resource manager.</span><span class="sxs-lookup"><span data-stu-id="3f08f-140">You cannot remove a static private IP address from a NIC in Azure CLI for resource manager deployments.</span></span> <span data-ttu-id="3f08f-141">U moet doen:</span><span class="sxs-lookup"><span data-stu-id="3f08f-141">You must:</span></span>
- <span data-ttu-id="3f08f-142">Maak een nieuwe NIC die gebruikmaakt van een dynamische IP-adres</span><span class="sxs-lookup"><span data-stu-id="3f08f-142">Create a new NIC that uses a dynamic IP</span></span>
- <span data-ttu-id="3f08f-143">Hallo NIC ingesteld op Hallo VM Hallo nieuw gemaakte NIC.</span><span class="sxs-lookup"><span data-stu-id="3f08f-143">Set hello NIC on hello VM do hello newly created NIC.</span></span> 

<span data-ttu-id="3f08f-144">toochange hello NIC voor VM die wordt gebruikt in Hallo opdrachten bovenstaande Hallo Hallo volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="3f08f-144">toochange hello NIC for hello VM used in hello commands above, follow hello steps below.</span></span>

1. <span data-ttu-id="3f08f-145">Voer Hallo **nic azure-netwerk maken** toocreate opdracht een nieuwe NIC met dynamische IP-toewijzing met een nieuw IP-adres.</span><span class="sxs-lookup"><span data-stu-id="3f08f-145">Run hello **azure network nic create** command toocreate a new NIC using dynamic IP allocation with a new IP address.</span></span> <span data-ttu-id="3f08f-146">Houd er rekening mee dat omdat er geen IP-adres is opgegeven, Hallo toewijzingsmethode **dynamische**.</span><span class="sxs-lookup"><span data-stu-id="3f08f-146">Note that because no IP address is specified, hello allocation method is **Dynamic**.</span></span>

    ```azurecli
    az network nic create     \
    --resource-group TestRG     \
    --name TestNIC2     \
    --location centralus     \
    --subnet FrontEnd    \
    --vnet-name TestVNet
    ```        
   
    <span data-ttu-id="3f08f-147">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="3f08f-147">Expected output:</span></span>

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

2. <span data-ttu-id="3f08f-148">Voer Hallo **azure vm set** opdracht toochange Hallo NIC die wordt gebruikt door Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="3f08f-148">Run hello **azure vm set** command toochange hello NIC used by hello VM.</span></span>
   
    ```azurecli
    azure vm set -g TestRG -n DNS01 -N TestNIC2
    ```

    <span data-ttu-id="3f08f-149">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="3f08f-149">Expected output:</span></span>
   
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
    > <span data-ttu-id="3f08f-150">Als Hallo VM groot genoeg toohave is meer dan één NIC, Voer Hallo **azure-netwerk nic verwijderen** opdracht toodelete Hallo oude NIC.</span><span class="sxs-lookup"><span data-stu-id="3f08f-150">If hello VM is large enough toohave more than one NIC, run hello **azure network nic delete** command toodelete hello old NIC.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="3f08f-151">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3f08f-151">Next steps</span></span>
* <span data-ttu-id="3f08f-152">Meer informatie over [gereserveerde openbare IP-adres](virtual-networks-reserved-public-ip.md) adressen.</span><span class="sxs-lookup"><span data-stu-id="3f08f-152">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="3f08f-153">Meer informatie over [instantieniveau openbare IP (ILPIP)](virtual-networks-instance-level-public-ip.md) adressen.</span><span class="sxs-lookup"><span data-stu-id="3f08f-153">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="3f08f-154">Raadpleeg Hallo [gereserveerde IP-REST-API's](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="3f08f-154">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

