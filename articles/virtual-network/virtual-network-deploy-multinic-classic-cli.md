---
title: een VM (klassiek) met meerdere NIC's - Azure CLI 1.0 aaaCreate | Microsoft Docs
description: Meer informatie over hoe toocreate een VM (klassiek) met meerdere NIC's met behulp van Azure-opdrachtregelinterface (CLI) 1.0 Hallo.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: b436e41e-866c-439f-a7c7-7b4b041725ef
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 181bfb28027caff33410ca94744e79206a2a0d0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics-using-hello-azure-cli-10"></a>Een virtuele machine (klassiek) maken met meerdere NIC's met behulp van hello Azure CLI 1.0

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

U kunt virtuele machines (VM's) in Azure maken en koppelen van meerdere netwerkinterfaces (NIC's) van netwerk-tooeach van uw virtuele machines. Meerdere NIC's inschakelen scheiding van verkeerstypen tussen NIC's. Bijvoorbeeld verbonden een die NIC met Internet, Hallo communiceren kan terwijl een andere alleen met interne bronnen niet communiceert toohello Internet. Hallo mogelijkheid tooseparate netwerkverkeer via meerdere NIC's is vereist voor veel virtuele netwerkapparaten, zoals toepassingen en optimalisatie van WAN-oplossingen.

> [!IMPORTANT]
> Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../resource-manager-deployment-model.md). In dit artikel wordt behandeld met het klassieke implementatiemodel Hallo. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken. Meer informatie over hoe tooperform deze stappen Hallo [Resource Manager-implementatiemodel](virtual-network-deploy-multinic-arm-cli.md).

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

Hallo volgt gebruik van een resourcegroep met de naam *IaaSStory* voor Hallo-webservers en een resourcegroep met de naam *IaaSStory-back-end* voor Hallo DB-servers.

## <a name="prerequisites"></a>Vereisten
Voordat u Hallo DB servers maken kunt, moet u toocreate hello *IaaSStory* resourcegroep met alle Hallo benodigde resources voor dit scenario. toocreate deze resources, volledige Hallo stappen volgen. Een virtueel netwerk maken door de stappen te volgen Hallo in Hallo [een virtueel netwerk maken](virtual-networks-create-vnet-classic-cli.md) artikel.

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="deploy-hello-back-end-vms"></a>Implementeer Hallo back-end virtuele machines
Hallo die back-end-VM's afhankelijk zijn van Hallo maken van Hallo resources te volgen:

* **Storage-account voor gegevensschijven**. Voor betere prestaties Hallo gegevensschijven op Hallo databaseservers Solid-State station (SSD)-technologie, waarvoor een premium storage-account gebruikt. Zorg ervoor dat hello Azure-locatie implementeren van toosupport premium-opslag.
* **NIC's**. Elke virtuele machine heeft twee NIC's, één voor toegang tot de database, en één voor beheer.
* **Beschikbaarheidsset**. Alle databaseservers tooa één beschikbaarheidsset worden toegevoegd, tooensure ten minste één Hallo VM's actief is tijdens het onderhoud.

### <a name="step-1---start-your-script"></a>Stap 1: uw script starten
U kunt downloaden Hallo volledige bash-script waarmee [hier](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-cli.sh). Voer Hallo stappen toochange Hallo script toowork in uw omgeving te volgen:

1. Hallo-waarden van Hallo variabelen hieronder op basis van uw bestaande resourcegroep geïmplementeerd boven in wijzigen [vereisten](#Prerequisites).

    ```azurecli
    location="useast2"
    vnetName="WTestVNet"
    backendSubnetName="BackEnd"
    ```
2. Hallo waarden wijzigen van Hallo variabelen hieronder op basis van waarden Hallo gewenste toouse voor uw back-end-implementatie.

    ```azurecli
    backendCSName="IaaSStory-Backend"
    prmStorageAccountName="iaasstoryprmstorage"
    image="0b11de9248dd4d87b18621318e037d37__RightImage-Ubuntu-14.04-x64-v14.2.1"
    avSetName="ASDB"
    vmSize="Standard_DS3"
    diskSize=127
    vmNamePrefix="DB"
    osDiskName="osdiskdb"
    dataDiskPrefix="db"
    dataDiskName="datadisk"
    ipAddressPrefix="192.168.2."
    username='adminuser'
    password='adminP@ssw0rd'
    numberOfVMs=2
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a>Stap 2: de benodigde resources voor uw virtuele machines maken
1. Maak een nieuwe cloudservice voor alle back-end-VM's. Gebruik van de kennisgeving Hallo Hallo `$backendCSName` variabele voor naam resourcegroep hello, en `$location` voor hello Azure-regio.

    ```azurecli
    azure service create --serviceName $backendCSName \
        --location $location
    ```

2. Maak een premium storage-account voor Hallo OS en gegevens schijven toobe die wordt gebruikt door uw virtuele machines.

    ```azurecli
    azure storage account create $prmStorageAccountName \
        --location $location \
        --type PLRS
    ```

### <a name="step-3---create-vms-with-multiple-nics"></a>Stap 3: virtuele machines maken met meerdere NIC 's
1. Start een lus toocreate meerdere virtuele machines, op basis van Hallo `numberOfVMs` variabelen.

    ```azurecli
    for ((suffixNumber=1;suffixNumber<=numberOfVMs;suffixNumber++));
    do
    ```

2. Geef voor elke VM Hallo naam en IP-adres van elk van de Hallo twee NIC's.

    ```azurecli
    nic1Name=$vmNamePrefix$suffixNumber-DA
    x=$((suffixNumber+3))
    ipAddress1=$ipAddressPrefix$x

    nic2Name=$vmNamePrefix$suffixNumber-RA
    x=$((suffixNumber+53))
    ipAddress2=$ipAddressPrefix$x
    ```

3. Hallo VM maken. Let op Hallo gebruik van Hallo `--nic-config` parameter, met een lijst met alle NIC's met de naam, subnet en IP-adres.

    ```azurecli
    azure vm create $backendCSName $image $username $password \
        --connect $backendCSName \
        --vm-name $vmNamePrefix$suffixNumber \
        --vm-size $vmSize \
        --availability-set $avSetName \
        --blob-url $prmStorageAccountName.blob.core.windows.net/vhds/$osDiskName$suffixNumber.vhd \
        --virtual-network-name $vnetName \
        --subnet-names $backendSubnetName \
        --nic-config $nic1Name:$backendSubnetName:$ipAddress1::,$nic2Name:$backendSubnetName:$ipAddress2::
    ```

4. Maak twee gegevensschijven voor elke VM.

    ```azurecli
    azure vm disk attach-new $vmNamePrefix$suffixNumber \
        $diskSize \
        vhds/$dataDiskPrefix$suffixNumber$dataDiskName-1.vhd

    azure vm disk attach-new $vmNamePrefix$suffixNumber \
        $diskSize \
        vhds/$dataDiskPrefix$suffixNumber$dataDiskName-2.vhd
    done
    ```

### <a name="step-4---run-hello-script"></a>Stap 4: Hallo-script uitvoeren
Nu dat u hebt gedownload en gewijzigd Hallo-script op basis van uw behoeften, Hallo script toocreate Hallo terug uitvoeren end-database VM's met meerdere NIC's.

1. Sla uw script en voer dit uit uw **Bash** terminal. U ziet Hallo initiële uitvoer, zoals hieronder wordt weergegeven.

        info:    Executing command service create
        info:    Creating cloud service
        data:    Cloud service name IaaSStory-Backend
        info:    service create command OK
        info:    Executing command storage account create
        info:    Creating storage account
        info:    storage account create command OK
        info:    Executing command vm create
        info:    Looking up image 0b11de9248dd4d87b18621318e037d37__RightImage-Ubuntu-14.04-x64-v14.2.1
        info:    Looking up virtual network
        info:    Looking up cloud service
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Creating VM

2. Hallo uitvoering beëindigd na een paar minuten en ziet u de rest Hallo van Hallo uitvoer zoals hieronder wordt weergegeven.

        info:    OK
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
        info:    Executing command vm create
        info:    Looking up image 0b11de9248dd4d87b18621318e037d37__RightImage-Ubuntu-14.04-x64-v14.2.1
        info:    Looking up virtual network
        info:    Looking up cloud service
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Creating VM
        info:    OK
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
