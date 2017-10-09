---
title: een virtuele machine met een statische openbare IP-adres - Azure CLI 2.0 aaaCreate | Microsoft Docs
description: Meer informatie over hoe toocreate met een statische openbare IP-adres met een virtuele machine hello Azure-opdrachtregelinterface (CLI) 2.0.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 55bc21b0-2a45-4943-a5e7-8d785d0d015c
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 486060463486462dd8336734a7ad23c4a2cba452
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-hello-azure-cli-20"></a>Een virtuele machine maken met een statische openbare IP-adres met hello Azure CLI 2.0

> [!div class="op_single_selector"]
> * [Azure Portal](virtual-network-deploy-static-pip-arm-portal.md)
> * [PowerShell](virtual-network-deploy-static-pip-arm-ps.md)
> * [Azure CLI 2.0](virtual-network-deploy-static-pip-arm-cli.md)
> * [Azure CLI 1.0](virtual-network-deploy-static-pip-cli-nodejs.md)
> * [Sjabloon](virtual-network-deploy-static-pip-arm-template.md)
> * [PowerShell (klassiek)](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en classic](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json). In dit artikel bevat informatie over Hallo Resource Manager-implementatiemodel, die Microsoft voor de meeste nieuwe implementaties in plaats van het klassieke implementatiemodel hello aanbeveelt gebruiken.

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name = "create"></a>Hallo VM maken

U kunt deze taak uitvoeren met hello Azure CLI 2.0 (in dit artikel) of Hallo [Azure CLI 1.0](virtual-network-deploy-static-pip-cli-nodejs.md). waarden in Hallo ' ' voor Hallo variabelen in Hallo stappen volgen resources met de instellingen van Hallo scenario maken. Hallo-waarden waar nodig voor uw omgeving te wijzigen.

1. Hallo installeren [Azure CLI 2.0](/cli/azure/install-az-cli2) als u dit nog niet geïnstalleerd.
2. De openbare en persoonlijke sleutelpaar voor een SSH maken voor Linux virtuele machines via Hallo stappen in Hallo [maken van een SSH openbare en persoonlijke sleutelpaar voor virtuele Linux-machines](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).
3. Vanuit een opdrachtshell, meld u aan met de opdracht Hallo `az login`.
4. Hallo VM maken door het Hallo-script dat op een Linux- of Mac-computer volgt uitvoeren. Hallo Azure openbaar IP-adres, het virtuele netwerk, netwerkinterface en VM netwerkbronnen moeten al bestaan in Hallo dezelfde locatie. Hoewel Hallo resources niet allemaal tooexist in Hallo hebben dezelfde resourcegroep in Hallo na script ze doen.

```bash
RgName="IaaSStory"
Location="westus"

# Create a resource group.

az group create \
--name $RgName \
--location $Location

# Create a public IP address resource with a static IP address using hello --allocation-method Static option.
# If you do not specify this option, hello address is allocated dynamically. hello address is assigned toothe
# resource from a pool of IP adresses unique tooeach Azure region. hello DnsName must be unique within the
# Azure location it's created in. Download and view hello file from https://www.microsoft.com/en-us/download/details.aspx?id=41653#
# that lists hello ranges for each region.

PipName="PIPWEB1"
DnsName="iaasstoryws1"
az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--allocation-method Static \
--dns-name $DnsName

# Create a virtual network with one subnet

VnetName="TestVNet"
VnetPrefix="192.168.0.0/16"
SubnetName="FrontEnd"
SubnetPrefix="192.168.1.0/24"
az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $SubnetName \
--subnet-prefix $SubnetPrefix

# Create a network interface connected toohello VNet with a static private IP address and associate hello public IP address
# resource toohello NIC.

NicName="NICWEB1"
PrivateIpAddress="192.168.1.101"
az network nic create \
--name $NicName \
--resource-group $RgName \
--location $Location \
--subnet $SubnetName \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress \
--public-ip-address $PipName

# Create a new VM with hello NIC

VmName="WEB1"

# Replace hello value for hello VmSize variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes article.
VmSize="Standard_DS1"

# Replace hello value for hello OsImage variable with a value for *urn* from hello output returned by entering
# hello `az vm image list` command. 

OsImage="credativ:Debian:8:latest"
Username='adminuser'

# Replace hello following value with hello path tooyour public key file.
SshKeyValue="~/.ssh/id_rsa.pub"

az vm create \
--name $VmName \
--resource-group $RgName \
--image $OsImage \
--location $Location \
--size $VmSize \
--nics $NicName \
--admin-username $Username \
--ssh-key-value $SshKeyValue
# If creating a Windows VM, remove hello previous line and you'll be prompted for hello password you want tooconfigure for hello VM.
```

Bovendien toocreating een virtuele machine, Hallo script maakt:
- Een enkele premium schijf standaard beheerd, maar hebben van andere opties voor het Hallo-schijftype die u kunt maken. Lees Hallo [maken van een Linux-VM met hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artikel voor meer informatie.
- Virtueel netwerk, subnet, NIC en openbare IP-adresbronnen. U kunt ook gebruiken *bestaande* virtueel netwerk, subnet, NIC of openbare IP-adresbronnen. toolearn hoe toouse bestaande netwerkbronnen in plaats van invoeren voor het maken van aanvullende bronnen `az vm create -h`.

## <a name = "validate"></a>Maken van VM- en openbare IP-adres valideren

1. Voer de opdracht Hallo `az resource list --resouce-group IaaSStory --output table` toosee een lijst met Hallo-resources die zijn gemaakt door Hallo-script. Moet er vijf resources in Hallo uitvoer geretourneerd: network interface, schijf, openbare IP-adres, virtuele netwerk en een virtuele machine.
2. Voer de opdracht Hallo `az network public-ip show --name PIPWEB1 --resource-group IaaSStory --output table`. In Hallo uitvoer geretourneerd, bekijkt hello waarde **IpAddress** en die waarde Hallo van **PublicIpAllocationMethod** is *statische*.
3. Verwijder, voordat u Hallo na de opdracht uitvoert, Hallo <>, vervangen door *gebruikersnaam* met Hallo-naam die u voor Hallo gebruikt **gebruikersnaam** variabele in het Hallo-script en vervang *ipAddress* Hello **ipAddress** uit de vorige stap Hallo. Voer Hallo volgende opdracht tooconnect toohello VM: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`. 

## <a name= "clean-up"></a>Hallo VM en gekoppelde resources verwijderen

Het raadzaam dat u Hallo resources in deze oefening hebt gemaakt verwijdert als u deze niet in productie gebruikt. Virtuele machine, openbare IP-adres en schijfbronnen worden kosten in rekening, zolang deze zijn ingericht. tooremove hello resources gemaakt tijdens deze oefening voltooid Hallo stappen te volgen:

1. tooview hello resources in de resourcegroep hello, Voer Hallo `az resource list --resource-group IaaSStory` opdracht.
2. Bevestig er zijn geen resources in de resourcegroep Hallo dan Hallo-resources die zijn gemaakt door Hallo script in dit artikel. 
3. alle resources die zijn gemaakt in deze oefening uitvoeren Hallo toodelete `az group delete -n IaaSStory` opdracht. Hallo opdracht verwijdert u Hallo-resourcegroep en alle Hallo resources bevat.

## <a name="next-steps"></a>Volgende stappen

Netwerkverkeer kan tooand van virtuele machine in dit artikel gemaakt Hallo stromen. Binnenkomende en uitgaande regels binnen een NSG die Hallo-verkeer dat tooand van netwerkinterface hello, Hallo subnet of beide kan stromen te beperken, kunt u definiëren. meer informatie over nsg's, Hallo lezen toolearn [NSG overzicht](virtual-networks-nsg.md) artikel.
