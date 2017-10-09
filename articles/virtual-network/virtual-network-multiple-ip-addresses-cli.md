---
title: aaaVM met meerdere IP-adressen met behulp van Azure CLI 2.0 Hallo | Microsoft Docs
description: Meer informatie over hoe tooassign meerdere IP-adressen tooa virtuele machine met Azure CLI 2.0 Hallo | Resource Manager.
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/17/2016
ms.author: annahar
ms.openlocfilehash: 15efd853cc7c31bacb64ed052dabedd3fe4d3079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-hello-azure-cli-20"></a>Toovirtual machines hello Azure CLI 2.0 gebruiken voor meerdere IP-adressen toewijzen

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

Dit artikel wordt uitgelegd hoe een virtuele machine (VM) via hello Azure Resource Manager deployment model met behulp van toocreate hello Azure CLI 2.0. Meerdere IP-adressen kunnen niet worden toegewezen als tooresources via de klassieke implementatiemodel Hallo is gemaakt. meer informatie over Azure-implementatiemodellen, Hallo lezen toolearn [begrijpen implementatiemodellen](../resource-manager-deployment-model.md) artikel.

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name = "create"></a>Een virtuele machine maken met meerdere IP-adressen

U kunt deze taak uitvoeren met hello Azure CLI 2.0 (in dit artikel) of Hallo [Azure CLI 1.0](virtual-network-multiple-ip-addresses-cli-nodejs.md). Hallo-waarden waar nodig voor uw omgeving te wijzigen. Hallo in de volgende procedure wordt uitgelegd hoe toocreate een voorbeeld van de virtuele machine met meerdere IP-adressen, zoals beschreven in Hallo scenario. Variabelewaarden wijzigen in ' ' en IP-adrestypen zoals vereist voor uw implementatie. 

1. Hallo installeren [Azure CLI 2.0](/cli/azure/install-az-cli2) als u dit nog niet geïnstalleerd.
2. De openbare en persoonlijke sleutelpaar voor een SSH maken voor Linux virtuele machines via Hallo stappen in Hallo [maken van een SSH openbare en persoonlijke sleutelpaar voor virtuele Linux-machines](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).
3. Vanuit een opdrachtshell, meld u aan met de opdracht Hallo `az login` en u Hallo-abonnement te selecteren.
4. Hallo VM maken door het Hallo-script dat op een Linux- of Mac-computer volgt uitvoeren. Hallo script maakt een resourcegroep, een virtueel netwerk (VNet), een NIC met drie IP-configuraties en een virtuele machine met Hallo twee NIC's gekoppeld tooit. Hallo NIC, openbare IP-adres, virtuele netwerken en VM netwerkbronnen moeten al bestaan in Hallo dezelfde locatie en het abonnement. Hoewel Hallo resources niet allemaal tooexist in Hallo hebben dezelfde resourcegroep in Hallo na script ze doen.

```bash
    
#!/bin/sh
    
RgName="myResourceGroup"
Location="westcentralus"
az group create --name $RgName --location $Location
    
# Create a public IP address resource with a static IP address using hello `--allocation-method Static` option. If you
# do not specify this option, hello address is allocated dynamically. hello address is assigned toohello resource from a pool
# of IP adresses unique tooeach Azure region. Download and view hello file from
# https://www.microsoft.com/en-us/download/details.aspx?id=41653 that lists hello ranges for each region.

PipName="myPublicIP"

# This name must be unique within an Azure location.
DnsName="myDNSName"

az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--dns-name $DnsName\
--allocation-method Static

# Create a virtual network with one subnet

VnetName="myVnet"
VnetPrefix="10.0.0.0/16"
VnetSubnetName="mySubnet"
VnetSubnetPrefix="10.0.0.0/24"

az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $VnetSubnetName \
--subnet-prefix $VnetSubnetPrefix

# Create a network interface connected toohello subnet and associate hello public IP address tooit. Azure will create the
# first IP configuration with a static private IP address and will associate hello public IP address resource tooit.

NicName="MyNic1"
az network nic create \
--name $NicName \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet1Name \
--private-ip-address 10.0.0.4
--vnet-name $VnetName \
--public-ip-address $PipName
    
# Create a second public IP address, a second IP configuration, and associate it toohello NIC. This configuration has a
# static public IP address and a static private IP address.

az network public-ip create \
--resource-group $RgName \
--location $Location \
--name myPublicIP2 \
--dns-name mypublicdns2 \
--allocation-method Static

az network nic ip-config create \
--resource-group $RgName \
--nic-name $NicName \
--name IPConfig-2 \
--private-ip-address 10.0.0.5 \
--public-ip-name myPublicIP2

# Create a third IP configuration, and associate it toohello NIC. This configuration has  static private IP address and # no public IP address.

azure network nic ip-config create \
--resource-group $RgName \
--nic-name $NicName \
--private-ip-address 10.0.0.6 \
--name IPConfig-3

# Note: Though this article assigns all IP configurations tooa single NIC, you can also assign multiple IP configurations
# tooany NIC in a VM. toolearn how toocreate a VM with multiple NICs, read hello Create a VM with multiple NICs 
# article: https://docs.microsoft.com/azure/virtual-network/virtual-network-deploy-multinic-arm-cli.

# Create a VM and attach hello NIC.

VmName="myVm"

# Replace hello value for hello following **VmSize** variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes rticle. hello script fails if hello VM size
# is not supported in hello location you select. Run hello `azure vm sizes --location estcentralus` command tooget a full list
# of VMs in US West Central, for example.

VmSize="Standard_DS1"

# Replace hello value for hello OsImage variable value with a value for *urn* from hello utput returned by entering the
# `az vm image list` command.

OsImage="credativ:Debian:8:latest"

Username="adminuser"

# Replace hello following value with hello path tooyour public key file. If you're creating a Windows VM, remove hello following
# line and you'll be prompted for hello password you want tooconfigure for hello VM.

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
```

Bovendien toocreating een virtuele machine met een NIC met 3-IP-configuraties, Hallo script maakt:

- Een enkele premium schijf standaard beheerd, maar hebben van andere opties voor het Hallo-schijftype die u kunt maken. Lees Hallo [maken van een Linux-VM met hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artikel voor meer informatie.
- Een virtueel netwerk met één subnet en twee openbare IP-adressen. U kunt ook gebruiken *bestaande* virtueel netwerk, subnet, NIC of openbare IP-adresbronnen. toolearn hoe toouse bestaande netwerkbronnen in plaats van invoeren voor het maken van aanvullende bronnen `az vm create -h`.

Openbare IP-adressen hebben een nominaal kosten. meer over IP-prijzen toolearn lezen Hallo [IP-adres prijzen](https://azure.microsoft.com/pricing/details/ip-addresses) pagina. Er is een limiet toohello aantal openbare IP-adressen die kunnen worden gebruikt in een abonnement. meer informatie over het Hallo-limieten, Hallo lezen toolearn [Azure beperkt](../azure-subscription-service-limits.md#networking-limits) artikel.

Nadat het Hallo VM is gemaakt, voert u Hallo `az network nic show --name MyNic1 --resource-group myResourceGroup` opdracht tooview Hallo NIC-configuratie. Voer Hallo `az network nic ip-config list --nic-name MyNic1 --resource-group myResourceGroup --output table` tooview een lijst met Hallo IP-configuraties die zijn gekoppeld toohello NIC.

Toevoegen Hallo privé-IP-adressen toohello VM besturingssysteem via Hallo stappen voor het besturingssysteem in Hallo [toevoegen IP-adressen tooa VM besturingssysteem](#os-config) sectie van dit artikel.

## <a name="add"></a>IP-adressen tooa VM toevoegen

U kunt extra persoonlijke en openbare IP-adressen tooan NIC bestaande via Hallo stappen volgen toevoegen. Hallo voorbeelden bouwen voort op Hallo [scenario](#Scenario) in dit artikel wordt beschreven.

1. Open een opdrachtshell en volledige Hallo resterende stappen in deze sectie binnen één sessie. Als u nog geen Azure CLI geïnstalleerd en geconfigureerd, voltooid Hallo stappen voor het Hallo [installatie van Azure CLI 2.0](/cli/azure/install-az-cli2?toc=%2fazure%2fvirtual-network%2ftoc.json) tooyour artikel en meld u aan Azure-account met Hallo `az-login` opdracht.

2. Voer Hallo stappen in een Hallo uit te voeren, op basis van uw vereisten:

    **Een persoonlijke IP-adres toevoegen**
    
    een persoonlijke IP-adres tooa NIC tooadd, moet u een IP-configuratie met Hallo-opdracht die volgt maken. Hallo statisch IP-adres moet een niet-gebruikte adres voor het Hallo-subnet.

    ```bash
    az network nic ip-config create \
    --resource-group myResourceGroup \
    --nic-name myNic1 \
    --private-ip-address 10.0.0.7 \
    --name IPConfig-4
    ```
    
    Configuraties die u nodig hebt, gebruik van unieke namen en privé IP-adressen (voor configuraties met statische IP-adressen) maken.

    **Een openbaar IP-adres toevoegen**
    
    Een openbaar IP-adres is toegevoegd door deze te koppelen tooeither een nieuwe IP-configuratie of een bestaande IP-configuratie. Stappen Hallo in een van Hallo secties die volgen, die u nodig hebt.

    Openbare IP-adressen hebben een nominaal kosten. meer over IP-prijzen toolearn lezen Hallo [IP-adres prijzen](https://azure.microsoft.com/pricing/details/ip-addresses) pagina. Er is een limiet toohello aantal openbare IP-adressen die kunnen worden gebruikt in een abonnement. meer informatie over het Hallo-limieten, Hallo lezen toolearn [Azure beperkt](../azure-subscription-service-limits.md#networking-limits) artikel.

    - **Hallo resource tooa nieuwe IP-configuratie koppelen**
    
        Als u een openbaar IP-adres in een nieuw IP-configuratie toevoegt, moet u ook een privé IP-adres toevoegen, omdat alle IP-configuraties moeten een particulier IP-adres hebben. U kunt een bestaande resource voor openbare IP-adres toevoegen of u een nieuwe maken. toocreate een nieuw wachtwoord invoeren Hallo volgende opdracht:
    
        ```bash
        az network public-ip create \
        --resource-group myResourceGroup \
        --location westcentralus \
        --name myPublicIP3 \
        --dns-name mypublicdns3
        ```

        toocreate een nieuwe IP-configuratie met een statisch privé IP-adres en het Hallo gekoppeld *myPublicIP3* openbare IP-adres adres resource, Voer Hallo volgende opdracht:

        ```bash
        az network nic ip-config create \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --name IPConfig-5 \
        --private-ip-address 10.0.0.8
        --public-ip-address myPublicIP3
        ```

    - **Koppelen Hallo resource tooan bestaande IP-configuratie** een openbare IP-adres resource kan alleen worden gekoppeld tooan IP-configuratie die nog geen die zijn gekoppeld. U kunt bepalen of een IP-configuratie een gekoppeld openbare IP-adres heeft door te voeren Hallo volgende opdracht:

        ```bash
        az network nic ip-config list \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --query "[?provisioningState=='Succeeded'].{ Name: name, PublicIpAddressId: publicIpAddress.id }" --output table
        ```

        Geretourneerd uitvoer:
    
            Name        PublicIpAddressId
            
            ipconfig1   /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP1
            IPConfig-2  /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP2
            IPConfig-3

        Sinds Hallo **PublicIpAddressId** kolom voor *IpConfig 3* is leeg in Hallo uitvoer geen openbare IP-adres-resource is momenteel gekoppeld tooit. U kunt een bestaand openbaar IP-adres resource tooIpConfig-3 toevoegen, of Voer Hallo opdracht toocreate een volgende:

        ```bash
        az network public-ip create \
        --resource-group  myResourceGroup
        --location westcentralus \
        --name myPublicIP3 \
        --dns-name mypublicdns3 \
        --allocation-method Static
        ```
    
        Voer Hallo opdracht resource toohello bestaande IP-configuratie met de naam van tooassociate Hallo openbare IP-adressen te volgen *IPConfig 3*:
    
        ```bash
        az network nic ip-config update \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --name IPConfig-3 \
        --public-ip myPublicIP3
        ```

3. Weergave Hallo privé IP-adressen en Hallo openbare IP-adres resource-id toegewezen toohello NIC door te voeren Hallo de volgende opdracht:

    ```bash
    az network nic ip-config list \
    --resource-group myResourceGroup \
    --nic-name myNic1 \
    --query "[?provisioningState=='Succeeded'].{ Name: name, PrivateIpAddress: privateIpAddress, PrivateIpAllocationMethod: privateIpAllocationMethod, PublicIpAddressId: publicIpAddress.id }" --output table
    ```

    Geretourneerd uitvoer: <br>
    
        Name        PrivateIpAddress    PrivateIpAllocationMethod   PublicIpAddressId
        
        ipconfig1   10.0.0.4            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP1
        IPConfig-2  10.0.0.5            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP2
        IPConfig-3  10.0.0.6            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP3
    

4. Hallo privé IP-adressen u toohello NIC toohello VM-besturingssysteem toegevoegd door de instructies te volgen Hallo in Hallo toevoegen [toevoegen IP-adressen tooa VM besturingssysteem](#os-config) sectie van dit artikel. Voeg geen Hallo openbare IP-adressen toohello besturingssysteem.

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
