---
title: een virtuele machine met meerdere NIC's - Azure CLI 2.0 aaaCreate | Microsoft Docs
description: Meer informatie over hoe toocreate met meerdere NIC's met behulp van een virtuele machine hello Azure CLI 2.0.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8e906a4b-8583-4a97-9416-ee34cfa09a98
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ac0291a978e2c8682c69104915196cc6c4fcf8dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-hello-azure-cli-20"></a>Een virtuele machine maken met meerdere NIC's met behulp van hello Azure CLI 2.0

[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../resource-manager-deployment-model.md).  In dit artikel wordt beschreven hoe u Hallo Resource Manager-implementatiemodel, die Microsoft voor de meeste nieuwe implementaties in plaats van Hallo aanbeveelt [klassieke implementatiemodel](virtual-network-deploy-multinic-classic-cli.md).
>

## <a name="create"></a>Hallo VM maken

U kunt deze taak uitvoeren met hello Azure CLI 2.0 (in dit artikel) of Hallo [Azure CLI 1.0](virtual-network-deploy-multinic-cli-nodejs.md). waarden in Hallo ' ' voor Hallo variabelen in Hallo stappen volgen resources met de instellingen van Hallo scenario maken. Hallo-waarden waar nodig voor uw omgeving te wijzigen.

1. Hallo installeren [Azure CLI 2.0](/cli/azure/install-az-cli2) als u dit nog niet geïnstalleerd.
2. De openbare en persoonlijke sleutelpaar voor een SSH maken voor Linux virtuele machines via Hallo stappen in Hallo [maken van een SSH openbare en persoonlijke sleutelpaar voor virtuele Linux-machines](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).
3. Vanuit een opdrachtshell, meld u aan met de opdracht Hallo `az login`.
4. Hallo VM maken door het Hallo-script dat op een Linux- of Mac-computer volgt uitvoeren. Hallo script maakt een resourcegroep of een virtueel netwerk (VNet) met twee subnetten, twee NIC's en een virtuele machine met Hallo twee NIC's gekoppeld tooit. Een van de Hallo NIC's verbonden tooone subnet en een statische openbare en particuliere IP-adres is toegewezen. Hallo andere NIC is verbonden toohello andere subnet en een statisch privé IP-adres en geen openbare IP-adres is toegewezen. Hallo NIC, openbare IP-adres, virtuele netwerken en VM netwerkbronnen moeten al bestaan in Hallo dezelfde locatie en het abonnement. Hoewel Hallo resources niet allemaal tooexist in Hallo hebben dezelfde resourcegroep in Hallo na script ze doen.

```bash
#!/bin/sh

RgName="Multi-NIC-VM"
Location="westus"

# Create a resource group.
az group create \
--name $RgName \
--location $Location

# hello address is assigned toohello resource from a pool of IP adresses unique tooeach Azure region. 
# Download and view hello file from https://www.microsoft.com/en-us/download/details.aspx?id=41653 that lists
# hello ranges for each region.

PipName="PIP-WEB"
az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--allocation-method Static

# Create a virtual network with one subnet

VnetName="VNet1"
VnetPrefix="10.0.0.0/16"
VnetSubnet1Name="Front-End"
VnetSubnet1Prefix="10.0.0.0/24"
az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $VnetSubnet1Name \
--subnet-prefix $VnetSubnet1Prefix

# Create a second subnet within hello VNet

VnetSubnet2Name="Back-end"
VnetSubnet2Prefix="10.0.1.0/24"
az network vnet subnet create \
--vnet-name $VnetName \
--resource-group $RgName \
--name $VnetSubnet2Name \
--address-prefix $VnetSubnet2Prefix

# Create a network interface connected tooone of hello subnets. hello NIC is assigned a single dynamic private and
# public IP address by default, but you can instead, assign static addresses, or no public IP address at all.
# You can also assign multiple private or public IP addresses tooeach NIC. toolearn more about IP addressing
# options for NICs, enter hello az network nic create -h command.

Nic1Name="NIC-FE"
PrivateIpAddress1="10.0.0.5"

az network nic create \
--name $Nic1Name \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet1Name \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress1 \
--public-ip-address $PipName

# Create a second network interface and connect it toohello other subnet. Though multiple NICs attached toohello same
# VM can be connected toodifferent subnets, hello subnets must all be within hello same VNet. Add additional NICs as necessary.

Nic2Name="NIC-BE"
PrivateIpAddress2="10.0.1.5"

az network nic create \
--name $Nic2Name \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet2Name \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress2

# Create a VM and attach hello two NICs.

VmName="WEB"

# Replace hello value for hello following **VmSize** variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes article. Not all VM sizes support
# more than one NIC, so be sure tooselect a VM size that supports hello number of NICs you want tooattach toohello VM.
# You must create hello VM with at least two NICs if you want tooadd more after VM creation. If you create a VM with
# only one NIC, you can't add additional NICs toohello VM after VM creation, regardless of how many NICs hello VM supports.
# hello VM size specified in hello following variable supports two NICs.

VmSize="Standard_DS2"

# Replace hello value for hello OsImage variable value with a value for *urn* from hello output returned by entering the
# az vm image list command.

OsImage="credativ:Debian:8:latest"

Username="adminuser"

# Replace hello following value with hello path tooyour public key file.

SshKeyValue="~/.ssh/id_rsa.pub"

# Before executing hello following command, add variable names of additional NICs you may have added toohello script that
# you want tooattach toohello VM. If creating a Windows VM, remove hello **ssh-key-value** line and you'll be prompted for
# hello password you want tooconfigure for hello VM.

az vm create \
--name $VmName \
--resource-group $RgName \
--image $OsImage \
--location $Location \
--size $VmSize \
--nics $Nic1Name $Nic2Name \
--admin-username $Username \
--ssh-key-value $SshKeyValue
```

Bovendien toocreating met twee NIC's een virtuele machine, Hallo script maakt:
- Een enkele premium schijf standaard beheerd, maar hebben van andere opties voor het Hallo-schijftype die u kunt maken. Lees Hallo [maken van een Linux-VM met hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artikel voor meer informatie.
- Een virtueel netwerk met twee subnetten en één openbare IP-adres. U kunt ook gebruiken *bestaande* virtueel netwerk, subnet, NIC of openbare IP-adresbronnen. toolearn hoe toouse bestaande netwerkbronnen in plaats van invoeren voor het maken van aanvullende bronnen `az vm create -h`.

## <a name = "validate"></a>Maken van VM's en NIC's valideren

1. Voer de opdracht Hallo `az resource list --resouce-group Multi-NIC-VM --output table` toosee een lijst met Hallo-resources die zijn gemaakt door Hallo-script. Moet er zes resources in Hallo uitvoer geretourneerd: twee NIC's, één schijf, een openbare IP-adres, een virtueel netwerk en een virtuele machine.
2. Voer de opdracht Hallo `az network public-ip show --name PIP-WEB --resource-group Multi-NIC-VM --output table`. In Hallo uitvoer geretourneerd, bekijkt hello waarde **IpAddress** en die waarde Hallo van **PublicIpAllocationMethod** is *statische*.
3. Verwijder, voordat Hallo volgende opdracht wordt uitgevoerd, Hallo <>, vervangen door *gebruikersnaam* met Hallo-naam die u voor Hallo gebruikt **gebruikersnaam** variabele in het Hallo-script en vervang *ipAddress* Hello **ipAddress** uit de vorige stap Hallo. Voer Hallo volgende opdracht tooconnect toohello VM: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`. 
4. Uitvoeren zodra toohello VM is verbonden, Hallo `sudo ifconfig` opdracht toosee *eth0* en *eth1* interfaces. Elke NIC is Hallo statisch privé IP-adressen opgegeven in Hallo script door hello Azure DHCP-servers toegewezen. Hallo wijzigen IP- en MAC-adressen toegewezen toohello NIC's niet totdat Hallo die virtuele machine is verwijderd. U wordt aangeraden dat u niet IP-adressen binnen een besturingssysteem, wijzigt zoals connectiviteit toohello computer uitschakelen. Openbare IP-adressen worden niet weergegeven in het besturingssysteem hello, omdat ze netwerk adres vertaald tooand van Hallo privé IP-adres door hello Azure-infrastructuur.

## <a name= "clean-up"></a>Hallo VM en gekoppelde resources verwijderen

Het raadzaam dat u Hallo resources in deze oefening hebt gemaakt verwijdert als u deze niet in productie gebruikt. Virtuele machine, openbare IP-adres en schijfbronnen worden kosten in rekening, zolang deze zijn ingericht. tooremove hello resources gemaakt tijdens deze oefening voltooid Hallo stappen te volgen:
1. tooview hello resources in de resourcegroep hello, Voer Hallo `az resource list --resource-group Multi-NIC-VM` opdracht.
2. Bevestig er zijn geen resources in de resourcegroep Hallo dan Hallo-resources die zijn gemaakt door Hallo script in dit artikel. 
3. alle resources die zijn gemaakt in deze oefening uitvoeren Hallo toodelete `az group delete --name Multi-NIC-VM` opdracht. Hallo opdracht verwijdert u Hallo-resourcegroep en alle Hallo resources bevat.

## <a name="next-steps"></a>Volgende stappen

Netwerkverkeer kan tooand van virtuele machine in dit artikel gemaakt Hallo stromen. Binnenkomende en uitgaande regels binnen een NSG die Hallo-verkeer dat tooand van elke netwerkinterface of elk subnet kan stromen te beperken, kunt u definiëren. meer informatie over nsg's, Hallo lezen toolearn [NSG overzicht](virtual-networks-nsg.md) artikel.
