---
title: aaaVM met meerdere IP-adressen met behulp van Azure CLI 1.0 Hallo | Microsoft Docs
description: Meer informatie over hoe tooassign meerdere IP-adressen tooa virtuele machine met Azure CLI 1.0 Hallo | Resource Manager.
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
ms.openlocfilehash: 83ad48e67309fb21d5aca967d4f2c01afdc0b5cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-azure-cli-10"></a>Meerdere IP-adressen toewijzen toovirtual machines met behulp van Azure CLI 1.0

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

Dit artikel wordt uitgelegd hoe een virtuele machine (VM) via hello Azure Resource Manager deployment model met behulp van toocreate hello Azure CLI 1.0. Meerdere IP-adressen kunnen niet worden toegewezen als tooresources via de klassieke implementatiemodel Hallo is gemaakt. meer informatie over Azure-implementatiemodellen, Hallo lezen toolearn [begrijpen implementatiemodellen](../resource-manager-deployment-model.md) artikel.

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name = "create"></a>Een virtuele machine maken met meerdere IP-adressen

U kunt deze taak uitvoeren met hello Azure CLI 1.0 (in dit artikel) of Hallo [Azure CLI 2.0](virtual-network-multiple-ip-addresses-cli.md). Hallo in de volgende procedure wordt uitgelegd hoe toocreate een voorbeeld van de virtuele machine met meerdere IP-adressen, zoals beschreven in Hallo scenario. Namen van variabelen en typen van de IP-adres zoals vereist voor uw implementatie wijzigen.

1. Installeren en configureren van Azure CLI 1.0 door de volgende Hallo stappen Hallo in Hallo [installeren en configureren van Azure CLI Hallo](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artikel en meld u aan bij uw Azure-account met Hallo `azure-login` opdracht.

2. Een resourcegroep maken:
    
    ```azurecli
    RgName=myResourceGroup
    Location=westcentralus
    azure group create --name $RgName --location $Location
    ```
3. Een virtueel netwerk maken:

    ```azurecli
    azure network vnet create --resource-group $RgName --location $Location --name myVNet \
    --address-prefixes 10.0.0.0/16
    ```
4. Een subnet in het virtuele netwerk Hallo maken:

    ```azurecli
    azure network vnet subnet create --name mySubnet --resource-group $RgName --vnet-name myVNet \
    --address-prefix 10.0.0.0/24
    ```
    
5. Maak een opslagaccount voor Hallo VM. Voordat u Hallo volgende opdracht, vervangt u *mystorageaccount* met een unieke naam. Hallo-naam moet uniek zijn in Azure:

    ```azurecli
    az storage account create --resource-group $RgName --location $Location --name mystorageaccount \
    --kind Storage --sku Standard_LRS
    ```

6. Hallo IP-configuraties, een NIC maken en toewijzen Hallo IP-configuraties toohello NIC. U kunt toevoegen, verwijderen of Hallo configuraties zo nodig wijzigen. Hallo volgende configuraties worden beschreven in Hallo scenario:

    **IPConfig-1**

    Voer Hallo-opdrachten die toocreate volgen:

    - Een openbaar IP-adres-resource met een statische openbare IP-adres
    - Een NIC Hallo openbaar IP-adres en een tooit statisch privé IP-adres toewijzen.
    
    Vervang *mypublicdns* met een naam die uniek is binnen hello Azure-locatie.

      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP1 \
      --domain-name-label mypublicdns --allocation-method Static
        
      azure network nic create --resource-group $RgName --location $Location --name myNic1 \
      --private-ip-address 10.0.0.4 --subnet-name mySubnet --subnet-vnet-name myVNet \
      --subnet-name mySubnet --public-ip-name myPublicIP1
      ```

      > [!NOTE]
      > Openbare IP-adressen hebben een nominaal kosten. meer over IP-prijzen toolearn lezen Hallo [IP-adres prijzen](https://azure.microsoft.com/pricing/details/ip-addresses) pagina. Er is een limiet toohello aantal openbare IP-adressen die kunnen worden gebruikt in een abonnement. meer informatie over het Hallo-limieten, Hallo lezen toolearn [Azure beperkt](../azure-subscription-service-limits.md#networking-limits) artikel.

    **IPConfig 2**

     Voer Hallo opdrachten toocreate na een nieuwe bron voor openbare IP-adres en een nieuwe IP-configuratie met een statische openbare IP-adres en een statisch privé IP-adres:
    
      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP2
      --domain-name-label mypublicdns2 --allocation-method Static

      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --name IPConfig-2
      --private-ip-address 10.0.0.5 --public-ip-name myPublicIP2
      ```

    **IPConfig 3**

    Voer Hallo opdrachten toocreate een IP-configuratie met een statisch privé IP-adres en geen openbare IP-adres te volgen:

      ```azurecli
      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --private-ip-address 10.0.0.6 \
      --name IPConfig-3
      ```

    >[!NOTE] 
    >Hoewel dit artikel wordt toegewezen voor alle IP-configuraties tooa één NIC, u kunt ook meerdere IP-configuraties tooany NIC op een virtuele machine toewijzen. toolearn hoe toocreate met meerdere NIC's, een virtuele machine lezen Hallo maken van een virtuele machine met meerdere NIC's artikel.

7. Een Linux-VM maken 

    ```azurecli
    az vm create --resource-group $RgName --name myVM1 --location $Location --nics myNic1 \
    --image UbuntuLTS --ssh-key-value ~/.ssh/id_rsa.pub --admin-username azureuser
    ```

    toochange hello VM grootte tooStandard DS2 v2, bijvoorbeeld toe te voegen na eigenschap Hallo `--vm-size Standard_DS3_v2` toohello `azure vm create` opdracht in stap 6.

8. Voer Hallo opdracht tooview Hallo NIC te volgen en Hallo bijbehorende IP-configuraties:

    ```azurecli
    azure network nic show --resource-group $RgName --name myNic1
    ```
9. Toevoegen Hallo privé-IP-adressen toohello VM besturingssysteem via Hallo stappen voor het besturingssysteem in Hallo [toevoegen IP-adressen tooa VM besturingssysteem](#os-config) sectie van dit artikel.

## <a name="add"></a>IP-adressen tooa VM toevoegen

U kunt extra persoonlijke en openbare IP-adressen tooan NIC bestaande via Hallo stappen volgen toevoegen. Hallo voorbeelden bouwen voort op Hallo [scenario](#Scenario) in dit artikel wordt beschreven.

1. Open Azure CLI en volledige Hallo resterende stappen in deze sectie binnen één CLI-sessie. Als u nog geen Azure CLI geïnstalleerd en geconfigureerd, voltooid Hallo stappen voor het Hallo [installeren en configureren van Azure CLI Hallo](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artikel en meld u aan bij uw Azure-account.

2. Voer Hallo stappen in een Hallo uit te voeren, op basis van uw vereisten:

    - **Een persoonlijke IP-adres toevoegen**
    
        een persoonlijke IP-adres tooa NIC tooadd, moet u een IP-configuratie met behulp van Hallo onderstaande opdracht maken. Hallo statisch adres moet een niet-gebruikte adres voor het Hallo-subnet.

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic1 \
        --private-ip-address 10.0.0.7 --name IPConfig-4
        ```
        Configuraties die u nodig hebt, gebruik van unieke namen en privé IP-adressen (voor configuraties met statische IP-adressen) maken.

    - **Een openbaar IP-adres toevoegen**
    
        Een openbaar IP-adres is toegevoegd door deze te koppelen tooeither een nieuwe IP-configuratie of een bestaande IP-configuratie. Stappen Hallo in een van Hallo secties die volgen, die u nodig hebt.

        > [!NOTE]
        > Openbare IP-adressen hebben een nominaal kosten. meer over IP-prijzen toolearn lezen Hallo [IP-adres prijzen](https://azure.microsoft.com/pricing/details/ip-addresses) pagina. Er is een limiet toohello aantal openbare IP-adressen die kunnen worden gebruikt in een abonnement. meer informatie over het Hallo-limieten, Hallo lezen toolearn [Azure beperkt](../azure-subscription-service-limits.md#networking-limits) artikel.
        >

        **Hallo resource tooa nieuwe IP-configuratie koppelen**
    
        Als u een openbaar IP-adres in een nieuw IP-configuratie toevoegt, moet u ook een privé IP-adres toevoegen, omdat alle IP-configuraties moeten een particulier IP-adres hebben. U kunt een bestaande resource voor openbare IP-adres toevoegen of u een nieuwe maken. toocreate een nieuw wachtwoord invoeren Hallo volgende opdracht:

        ```azurecli
        azure network public-ip create --resource-group myResourceGroup --location westcentralus --name myPublicIP3 \
        --domain-name-label mypublicdns3
        ```

        toocreate een nieuwe IP-configuratie met een statisch privé IP-adres en het Hallo gekoppeld *myPublicIP3* openbare IP-adres adres resource, Voer Hallo volgende opdracht:

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic --name IPConfig-4 \
        --private-ip-address 10.0.0.8 --public-ip-name myPublicIP3
        ```

        **Hallo resource tooan bestaande IP-configuratie koppelen**

        Een openbare IP-adres resource kan alleen worden gekoppeld tooan IP-configuratie die nog geen die zijn gekoppeld. U kunt bepalen of een IP-configuratie een gekoppeld openbare IP-adres heeft door te voeren Hallo volgende opdracht:

        ```azurecli
        azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
        ```

        Zoek naar een regel vergelijkbaar toohello die voor IPConfig 3 in Hallo uitvoer geretourneerd volgt:

        ```         
        Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
        IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
        IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet
        ```
          
        Sinds Hallo **openbare IP-adres** kolom voor *IpConfig 3* is leeg, geen openbare IP-adres-resource is momenteel gekoppeld tooit. U kunt een bestaand openbaar IP-adres resource tooIpConfig-3 toevoegen, of Voer Hallo opdracht toocreate een volgende:

        ```azurecli
        azure network public-ip create --resource-group  myResourceGroup --location westcentralus \
        --name myPublicIP3 --domain-name-label mypublicdns3 --allocation-method Static
        ```

        Voer Hallo opdracht resource toohello bestaande IP-configuratie met de naam van tooassociate Hallo openbare IP-adressen te volgen *IPConfig 3*:
        ```azurecli
        azure network nic ip-config set --resource-group myResourceGroup --nic-name myNic1 --name IPConfig-3 \
        --public-ip-name myPublicIP3
        ```

3. Hallo privé IP-adressen weergeven en Hallo openbare IP-adres resources toegewezen toohello NIC door te voeren Hallo de volgende opdracht:

    ```azurecli
    azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
    ```

      Hallo geretourneerd uitvoer is vergelijkbaar toohello volgende:
      ```
      Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        
      default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
      IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
      IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet  myPublicIP3
      ```
4. Hallo privé IP-adressen u toohello NIC toohello VM-besturingssysteem toegevoegd door de instructies te volgen Hallo in Hallo toevoegen [toevoegen IP-adressen tooa VM besturingssysteem](#os-config) sectie van dit artikel. Voeg geen Hallo openbare IP-adressen toohello besturingssysteem.

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
