---
title: aaaManage netwerkbeveiligingsgroepen - Azure CLI 2.0 | Microsoft Docs
description: Meer informatie over hoe toomanage netwerkbeveiligingsgroepen met hello Azure-opdrachtregelinterface (CLI) 2.0.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ed17d314-07e6-4c7f-bcf1-a8a2535d7c14
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/21/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a3036b465e1e4049cba00e5e13ce1b479a2301d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-groups-using-hello-azure-cli-20"></a><span data-ttu-id="f3931-103">Netwerkbeveiligingsgroepen hello Azure CLI 2.0 met beheren</span><span class="sxs-lookup"><span data-stu-id="f3931-103">Manage network security groups using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-network-manage-arm-selectors-include.md](../../includes/virtual-network-manage-nsg-arm-selectors-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="f3931-104">CLI-versies toocomplete Hallo taak</span><span class="sxs-lookup"><span data-stu-id="f3931-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="f3931-105">U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f3931-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="f3931-106">[Azure CLI 1.0](virtual-network-manage-nsg-cli-nodejs.md) – onze CLI voor Hallo klassieke en resource management implementatiemodellen</span><span class="sxs-lookup"><span data-stu-id="f3931-106">[Azure CLI 1.0](virtual-network-manage-nsg-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span> 
- <span data-ttu-id="f3931-107">[Azure CLI 2.0](#View-existing-NSGs) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel (in dit artikel)</span><span class="sxs-lookup"><span data-stu-id="f3931-107">[Azure CLI 2.0](#View-existing-NSGs) - our next generation CLI for hello resource management deployment model (this article)</span></span>


[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="f3931-108">Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="f3931-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f3931-109">In dit artikel bevat informatie over Hallo Resource Manager-implementatiemodel, die Microsoft voor de meeste nieuwe implementaties in plaats van het klassieke implementatiemodel hello aanbeveelt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f3931-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>
> 

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

## <a name="prerequisite"></a><span data-ttu-id="f3931-110">Vereiste</span><span class="sxs-lookup"><span data-stu-id="f3931-110">Prerequisite</span></span>
<span data-ttu-id="f3931-111">Als u dit nog niet hebt nog installeren en configureren van Hallo meest recente [Azure CLI 2.0](/cli/azure/install-az-cli2) en meld u bij het gebruik van de Azure-account tooan [az aanmelding](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="f3931-111">If you haven't yet, install and configure hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span> 


## <a name="view-existing-nsgs"></a><span data-ttu-id="f3931-112">Bestaande nsg's weergeven</span><span class="sxs-lookup"><span data-stu-id="f3931-112">View existing NSGs</span></span>
<span data-ttu-id="f3931-113">tooview hello lijst met nsg's in een specifieke resourcegroep of Voer Hallo [az netwerk nsg lijst](/cli/azure/network/nsg#list) opdracht met een `-o table` uitvoerindeling:</span><span class="sxs-lookup"><span data-stu-id="f3931-113">tooview hello list of NSGs in a specific resource group, run hello [az network nsg list](/cli/azure/network/nsg#list) command with a `-o table` output format:</span></span>

```azurecli
az network nsg list -g RG-NSG -o table
```

<span data-ttu-id="f3931-114">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="f3931-114">Expected output:</span></span>

    Location    Name          ProvisioningState    ResourceGroup    ResourceGuid
    ----------  ------------  -------------------  ---------------  ------------------------------------
    centralus   NSG-BackEnd   Succeeded            RG-NSG           <guid>
    centralus   NSG-FrontEnd  Succeeded            RG-NSG           <guid>

## <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="f3931-115">Lijst met alle regels voor een NSG</span><span class="sxs-lookup"><span data-stu-id="f3931-115">List all rules for an NSG</span></span>
<span data-ttu-id="f3931-116">tooview hello regels van een NSG met de naam **NSG-FrontEnd**, voert hello [az netwerk nsg weergeven](/cli/azure/network/nsg#show) opdracht met behulp van een [JMESPATH queryfilter](/cli/azure/query-az-cli2) en Hallo `-o table` uitvoerindeling:</span><span class="sxs-lookup"><span data-stu-id="f3931-116">tooview hello rules of an NSG named **NSG-FrontEnd**, run hello [az network nsg show](/cli/azure/network/nsg#show) command using a [JMESPATH query filter](/cli/azure/query-az-cli2) and hello `-o table` output format:</span></span>

```azurecli
    az network nsg show \
    --resource-group RG-NSG \
    --name NSG-FrontEnd \
    --query '[defaultSecurityRules[],securityRules[]][].{Name:name,Desc:description,Access:access,Direction:direction,DestPortRange:destinationPortRange,DestAddrPrefix:destinationAddressPrefix,SrcPortRange:sourcePortRange,SrcAddrPrefix:sourceAddressPrefix}' \
    -o table
```

<span data-ttu-id="f3931-117">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="f3931-117">Expected output:</span></span>

    Name                           Desc                                                    Access    Direction    DestPortRange    DestAddrPrefix    SrcPortRange    SrcAddrPrefix
    -----------------------------  ------------------------------------------------------  --------  -----------  ---------------  ----------------  --------------  -----------------
    AllowVnetInBound               Allow inbound traffic from all VMs in VNET              Allow     Inbound      *                VirtualNetwork    *               VirtualNetwork
    AllowAzureLoadBalancerInBound  Allow inbound traffic from azure load balancer          Allow     Inbound      *                *                 *               AzureLoadBalancer
    DenyAllInBound                 Deny all inbound traffic                                Deny      Inbound      *                *                 *               *
    AllowVnetOutBound              Allow outbound traffic from all VMs tooall VMs in VNET  Allow     Outbound     *                VirtualNetwork    *               VirtualNetwork
    AllowInternetOutBound          Allow outbound traffic from all VMs tooInternet         Allow     Outbound     *                Internet          *               *
    DenyAllOutBound                Deny all outbound traffic                               Deny      Outbound     *                *                 *               *
    rdp-rule                                                                               Allow     Inbound      3389             *                 *               Internet
    web-rule                                                                               Allow     Inbound      80               *                 *               Internet
> [!NOTE]
> <span data-ttu-id="f3931-118">U kunt ook [az netwerk nsg Regellijst](/cli/azure/network/nsg/rule#list) toolist alleen Hallo aangepaste regels uit een NSG.</span><span class="sxs-lookup"><span data-stu-id="f3931-118">You can also use [az network nsg rule list](/cli/azure/network/nsg/rule#list) toolist only hello custom rules from an NSG .</span></span>
>

## <a name="view-nsg-associations"></a><span data-ttu-id="f3931-119">Weergave NSG koppelingen</span><span class="sxs-lookup"><span data-stu-id="f3931-119">View NSG associations</span></span>

<span data-ttu-id="f3931-120">tooview welke resources Hallo **NSG-FrontEnd** NSG koppelen aan, voert Hallo is `az network nsg show` opdracht zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f3931-120">tooview what resources hello **NSG-FrontEnd** NSG is associate with, run hello `az network nsg show` command as shown below.</span></span> 

```azurecli
az network nsg show -g RG-NSG -n nsg-frontend --query '[subnets,networkInterfaces]'
```

<span data-ttu-id="f3931-121">Zoek naar Hallo **networkInterfaces** en **subnetten** eigenschappen zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="f3931-121">Look for hello **networkInterfaces** and **subnets** properties as shown below:</span></span>

```json
[
  [
    {
      "addressPrefix": null,
      "etag": null,
      "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNET/subnets/FrontEnd",
      "ipConfigurations": null,
      "name": null,
      "networkSecurityGroup": null,
      "provisioningState": null,
      "resourceGroup": "RG-NSG",
      "resourceNavigationLinks": null,
      "routeTable": null
    }
  ],
  null
]
```

<span data-ttu-id="f3931-122">Hallo bovenstaande voorbeeld Hallo NSG niet is gekoppeld tooany netwerkinterfaces (NIC's) en het bijbehorende tooa subnet met de naam is **FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="f3931-122">In hello example above, hello NSG is not associated tooany network interfaces (NICs), and it is associated tooa subnet named **FrontEnd**.</span></span>

## <a name="add-a-rule"></a><span data-ttu-id="f3931-123">Een regel toevoegen</span><span class="sxs-lookup"><span data-stu-id="f3931-123">Add a rule</span></span>
<span data-ttu-id="f3931-124">tooadd een regel waarmee **inkomende** verkeer tooport **443** van een machine toohello **NSG-FrontEnd** NSG, Voer Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="f3931-124">tooadd a rule allowing **inbound** traffic tooport **443** from any machine toohello **NSG-FrontEnd** NSG, enter hello following command:</span></span>

```azurecli
az network nsg rule create  \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd  \
--name allow-https \
--description "Allow access tooport 443 for HTTPS" \
--access Allow \
--protocol Tcp  \
--direction Inbound \
--priority 102 \
--source-address-prefix "*"  \
--source-port-range "*"  \
--destination-address-prefix "*" \
--destination-port-range "443"
```

<span data-ttu-id="f3931-125">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="f3931-125">Expected output:</span></span>

```json
{
  "access": "Allow",
  "description": "Allow access tooport 443 for HTTPS",
  "destinationAddressPrefix": "*",
  "destinationPortRange": "443",
  "direction": "Inbound",
  "etag": "W/\"<guid>\"",
  "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https",
  "name": "allow-https",
  "priority": 102,
  "protocol": "Tcp",
  "provisioningState": "Succeeded",
  "resourceGroup": "RG-NSG",
  "sourceAddressPrefix": "*",
  "sourcePortRange": "*"
}
```

## <a name="change-a-rule"></a><span data-ttu-id="f3931-126">Een regel wijzigen</span><span class="sxs-lookup"><span data-stu-id="f3931-126">Change a rule</span></span>
<span data-ttu-id="f3931-127">toochange hello regel bovenstaande tooallow binnenkomend verkeer van Hallo **Internet** alleen uitvoeren Hallo [az netwerk nsg regel update](/cli/azure/network/nsg/rule#update) opdracht:</span><span class="sxs-lookup"><span data-stu-id="f3931-127">toochange hello rule created above tooallow inbound traffic from hello **Internet** only, run hello [az network nsg rule update](/cli/azure/network/nsg/rule#update) command:</span></span>

```azurecli
az network nsg rule update \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd \
--name allow-https \
--source-address-prefix Internet
```

<span data-ttu-id="f3931-128">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="f3931-128">Expected output:</span></span>

```json
{
"access": "Allow",
"description": "Allow access tooport 443 for HTTPS",
"destinationAddressPrefix": "*",
"destinationPortRange": "443",
"direction": "Inbound",
"etag": "W/\"<guid>\"",
"id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https",
"name": "allow-https",
"priority": 102,
"protocol": "Tcp",
"provisioningState": "Succeeded",
"resourceGroup": "RG-NSG",
"sourceAddressPrefix": "Internet",
"sourcePortRange": "*"
}
```

## <a name="delete-a-rule"></a><span data-ttu-id="f3931-129">Een regel verwijderen</span><span class="sxs-lookup"><span data-stu-id="f3931-129">Delete a rule</span></span>
<span data-ttu-id="f3931-130">toodelete hello regel gemaakt hierboven Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f3931-130">toodelete hello rule created above, run hello following command:</span></span>

```azurecli
az network nsg rule delete \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd \
--name allow-https
```


## <a name="associate-an-nsg-tooa-nic"></a><span data-ttu-id="f3931-131">Een NSG tooa NIC koppelen</span><span class="sxs-lookup"><span data-stu-id="f3931-131">Associate an NSG tooa NIC</span></span>
<span data-ttu-id="f3931-132">Hallo tooassociate **NSG-FrontEnd** NSG toohello **TestNICWeb1** NIC, gebruik Hallo [az netwerk nic update](/cli/azure/network/nic#update) opdracht:</span><span class="sxs-lookup"><span data-stu-id="f3931-132">tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** NIC, use hello [az network nic update](/cli/azure/network/nic#update) command:</span></span>

```azurecli
az network nic update \
--resource-group RG-NSG \
--name TestNICWeb1 \
--network-security-group NSG-FrontEnd    
```

<span data-ttu-id="f3931-133">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="f3931-133">Expected output:</span></span>

```json
{
  "dnsSettings": {
    "appliedDnsServers": [],
    "dnsServers": [],
    "internalDnsNameLabel": null,
    "internalDomainNameSuffix": "k0wkaguidnqrh0ud.gx.internal.cloudapp.net",
    "internalFqdn": null
  },
  "enableAcceleratedNetworking": false,
  "enableIpForwarding": false,
  "etag": "W/\"<guid>\"",
  "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1",
  "ipConfigurations": [
    {
      "applicationGatewayBackendAddressPools": null,
      "etag": "W/\"<guid>\"",
      "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1",
      "loadBalancerBackendAddressPools": null,
      "loadBalancerInboundNatRules": null,
      "name": "ipconfig1",
      "primary": true,
      "privateIpAddress": "192.168.1.6",
      "privateIpAddressVersion": "IPv4",
      "privateIpAllocationMethod": "Static",
      "provisioningState": "Succeeded",
      "publicIpAddress": null,
      "resourceGroup": "RG-NSG",
      "subnet": {
        "addressPrefix": null,
        "etag": null,
        "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
        "ipConfigurations": null,
        "name": null,
        "networkSecurityGroup": null,
        "provisioningState": null,
        "resourceGroup": "RG-NSG",
        "resourceNavigationLinks": null,
        "routeTable": null
      }
    }
  ],
  "location": "centralus",
  "macAddress": "00-0D-3A-91-A9-60",
  "name": "TestNICWeb1",
  "networkSecurityGroup": {
    "defaultSecurityRules": null,
    "etag": null,
    "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd",
    "location": null,
    "name": null,
    "networkInterfaces": null,
    "provisioningState": null,
    "resourceGroup": "RG-NSG",
    "resourceGuid": null,
    "securityRules": null,
    "subnets": null,
    "tags": null,
    "type": null
  },
  "primary": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "RG-NSG",
  "resourceGuid": "<guid>",
  "tags": {},
  "type": "Microsoft.Network/networkInterfaces",
  "virtualMachine": null
}
```

## <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="f3931-134">Een NSG van een NIC ontkoppelen</span><span class="sxs-lookup"><span data-stu-id="f3931-134">Dissociate an NSG from a NIC</span></span>

<span data-ttu-id="f3931-135">Hallo toodissociate **NSG-FrontEnd** NSG van Hallo **TestNICWeb1** NIC, Voer Hallo [az netwerk nsg regel update](/cli/azure/network/nsg/rule#update) opdracht opnieuw, maar vervang Hallo `--network-security-group` argument met een lege tekenreeks (`""`).</span><span class="sxs-lookup"><span data-stu-id="f3931-135">toodissociate hello **NSG-FrontEnd** NSG from hello **TestNICWeb1** NIC, run hello [az network nsg rule update](/cli/azure/network/nsg/rule#update) command again but replace hello `--network-security-group` argument with an empty string (`""`).</span></span>

```azurecli
az network nic update --resource-group RG-NSG --name TestNICWeb3 --network-security-group ""
```

<span data-ttu-id="f3931-136">In de uitvoer van Hallo Hallo `networkSecurityGroup` sleutel toonull is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="f3931-136">In hello output, hello `networkSecurityGroup` key is set toonull.</span></span>

## <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="f3931-137">Een NSG van een subnet ontkoppelen</span><span class="sxs-lookup"><span data-stu-id="f3931-137">Dissociate an NSG from a subnet</span></span>
<span data-ttu-id="f3931-138">Hallo toodissociate **NSG-FrontEnd** NSG van Hallo **FrontEnd** subnet, opnieuw uitvoeren Hallo [az netwerk nsg regel update](/cli/azure/network/nsg/rule#update) opdracht opnieuw, maar vervang Hallo `--network-security-group` argument met een lege tekenreeks (`""`).</span><span class="sxs-lookup"><span data-stu-id="f3931-138">toodissociate hello **NSG-FrontEnd** NSG from hello **FrontEnd** subnet, again run hello [az network nsg rule update](/cli/azure/network/nsg/rule#update) command again but replace hello `--network-security-group` argument with an empty string (`""`).</span></span>

```azurecli
az network vnet subnet update \
--resource-group RG-NSG \
--vnet-name testvnet \
--name FrontEnd \
--network-security-group ""
```

<span data-ttu-id="f3931-139">In de uitvoer van Hallo Hallo `networkSecurityGroup` sleutel toonull is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="f3931-139">In hello output, hello `networkSecurityGroup` key is set toonull.</span></span>

## <a name="associate-an-nsg-tooa-subnet"></a><span data-ttu-id="f3931-140">Een NSG tooa subnet koppelen</span><span class="sxs-lookup"><span data-stu-id="f3931-140">Associate an NSG tooa subnet</span></span>
<span data-ttu-id="f3931-141">Hallo tooassociate **NSG-FrontEnd** NSG toohello **FrontEnd** subnet Hallo na de opdracht opnieuw uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f3931-141">tooassociate hello **NSG-FrontEnd** NSG toohello **FrontEnd** subnet again, run hello following command:</span></span>

```azurecli
az network vnet subnet update \
--resource-group RG-NSG \
--vnet-name testvnet \
--name FrontEnd \
--network-security-group NSG-FrontEnd
```

<span data-ttu-id="f3931-142">In de uitvoer van Hallo Hallo `networkSecurityGroup` sleutel heeft iets soortgelijks voor Hallo-waarde:</span><span class="sxs-lookup"><span data-stu-id="f3931-142">In hello output, hello `networkSecurityGroup` key has something similar for hello value:</span></span>

```json
"networkSecurityGroup": {
    "defaultSecurityRules": null,
    "etag": null,
    "id": "/subscriptions/0e220bf6-5caa-4e9f-8383-51f16b6c109f/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd",
    "location": null,
    "name": null,
    "networkInterfaces": null,
    "provisioningState": null,
    "resourceGroup": "RG-NSG",
    "resourceGuid": null,
    "securityRules": null,
    "subnets": null,
    "tags": null,
    "type": null
  }
  ```

## <a name="delete-an-nsg"></a><span data-ttu-id="f3931-143">Een NSG verwijderen</span><span class="sxs-lookup"><span data-stu-id="f3931-143">Delete an NSG</span></span>
<span data-ttu-id="f3931-144">U kunt een NSG alleen verwijderen als het tooany resource niet is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="f3931-144">You can only delete an NSG if it's not associated tooany resource.</span></span> <span data-ttu-id="f3931-145">een NSG toodelete Hallo volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="f3931-145">toodelete an NSG, follow hello steps below.</span></span>

1. <span data-ttu-id="f3931-146">toocheck hello resources die zijn gekoppeld tooan NSG, Voer Hallo `azure network nsg show` zoals in [weergave nsg's koppelingen](#View-NSGs-associations).</span><span class="sxs-lookup"><span data-stu-id="f3931-146">toocheck hello resources associated tooan NSG, run hello `azure network nsg show` as shown in [View NSGs associations](#View-NSGs-associations).</span></span>
2. <span data-ttu-id="f3931-147">Als Hallo NSG gekoppeld tooany NIC's is, voert u Hallo `azure network nic set` zoals in [ontkoppelen van een NSG van een NIC](#Dissociate-an-NSG-from-a-NIC) voor elke NIC.</span><span class="sxs-lookup"><span data-stu-id="f3931-147">If hello NSG is associated tooany NICs, run hello `azure network nic set` as shown in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC) for each NIC.</span></span> 
3. <span data-ttu-id="f3931-148">Als Hallo NSG gekoppeld tooany subnet is, voert u Hallo `azure network vnet subnet set` zoals in [een NSG van een subnet ontkoppelen](#Dissociate-an-NSG-from-a-subnet) voor elk subnet.</span><span class="sxs-lookup"><span data-stu-id="f3931-148">If hello NSG is associated tooany subnet, run hello `azure network vnet subnet set` as shown in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet) for each subnet.</span></span>
4. <span data-ttu-id="f3931-149">toodelete hello NSG, Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f3931-149">toodelete hello NSG, run hello following command:</span></span>

    ```azurecli
    az network nsg delete --resource-group RG-NSG --name NSG-FrontEnd
    ```
## <a name="next-steps"></a><span data-ttu-id="f3931-150">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f3931-150">Next steps</span></span>
* <span data-ttu-id="f3931-151">[Logboekregistratie inschakelen](virtual-network-nsg-manage-log.md) voor nsg's.</span><span class="sxs-lookup"><span data-stu-id="f3931-151">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

