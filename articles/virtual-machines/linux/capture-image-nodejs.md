---
title: een Azure Linux VM toouse als sjabloon aaaCapture | Microsoft Docs
description: Meer informatie over hoe toocapture en een installatiekopie van een Linux-gebaseerde Azure virtuele machine (VM) gemaakt met Azure Resource Manager-implementatiemodel Hallo generalize.
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e608116f-f478-41be-b787-c2ad91b5a802
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 877eee5c842bebe80e755c2240cdaaef4ade6ff5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="capture-a-linux-virtual-machine-running-on-azure"></a>Vastleggen van een virtuele Linux-machine uitgevoerd op Azure
Hallo-stappen in dit artikel toogeneralize en vastleggen van uw Azure Linux virtuele machine (VM) in Hallo Resource Manager-implementatiemodel. Wanneer u generalize Hallo VM, kunt u persoonlijke gegevens te verwijderen en Hallo VM toobe gebruikt als een installatiekopie van het voorbereiden. U vervolgens een installatiekopie van een gegeneraliseerde virtuele harde schijf (VHD) voor Hallo OS VHD's voor bijgesloten gegevensschijven, vastleggen en een [Resource Manager-sjabloon](../../azure-resource-manager/resource-group-overview.md) voor nieuwe VM-implementaties. Dit artikel wordt uitgelegd hoe toocapture een virtuele machine de installatiekopie met de Azure CLI 1.0 Hallo voor een virtuele machine met niet-beheerde schijven. U kunt ook [vastleggen van een VM die gebruikmaakt van Azure beheerd schijven Hello Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Beheerde schijven worden afgehandeld door hello Azure-platform en hoeven niet alle toostore voorbereidings- of locatie ze. Zie [Azure Managed Disks overview](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Overzicht van Azure Managed Disks) voor meer informatie. 

toocreate VM's met behulp van de installatiekopie hello, netwerkbronnen instellen voor elke nieuwe virtuele machine en gebruik Hallo sjabloon (een JavaScript Object Notation of JSON,-bestand) toodeploy op Hallo VHD-installatiekopieën vastgelegd. Op deze manier kunt u een virtuele machine met de huidige softwareconfiguratie kan vergelijkbare toohello manier als u installatiekopieën gebruiken in Azure Marketplace Hallo repliceren.

> [!TIP]
> Als u een kopie van uw bestaande Linux-VM met de speciale status toocreate voor back-up of foutopsporing wilt, Zie [een kopie maken van een virtuele Linux-machine uitgevoerd op Azure](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). En als u een VHD van een lokale virtuele machine met Linux tooupload wilt, Zie [uploaden en Linux-VM te maken van aangepaste schijfimage](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).  

## <a name="cli-versions-toocomplete-hello-task"></a>CLI-versies toocomplete Hallo taak
U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:

- [Azure CLI 1.0](#before-you-begin) – onze CLI voor Hallo klassieke en resource management implementatiemodellen (in dit artikel)
- [Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel

## <a name="before-you-begin"></a>Voordat u begint
Zorg ervoor dat u voldoet aan de Hallo volgende vereisten:

* **Azure virtuele machine gemaakt in de Resource Manager-implementatiemodel Hallo** -als u een Linux-VM nog niet hebt gemaakt, kunt u Hallo [portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), Hallo [Azure CLI](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), of [Resource Manager sjablonen](create-ssh-secured-vm-from-template.md). 
  
    Configureer Hallo VM indien nodig. Bijvoorbeeld: [gegevensschijven toevoegen](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), toepassen van updates en toepassingen te installeren. 
* **Azure CLI** -installatie Hallo [Azure CLI](../../cli-install-nodejs.md) op een lokale computer.

## <a name="step-1-remove-hello-azure-linux-agent"></a>Stap 1: Hello Azure Linux-agent verwijderen
Voer eerst Hallo **waagent** opdracht Hello **deprovision** parameter op Hallo Linux VM. Deze opdracht verwijdert u bestanden en gegevens toomake Hallo VM gereed is voor het generaliseren. Zie voor meer informatie, Hallo [gebruikershandleiding voor Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

1. Verbinding maken met behulp van een SSH-client voor Linux-VM tooyour.
2. Typ in Hallo SSH venster Hallo volgende opdracht:
   
    ```bash
    sudo waagent -deprovision+user
    ```
   > [!NOTE]
   > Alleen worden uitgevoerd met deze opdracht op een virtuele machine die u van plan toocapture als afbeelding bent. Het is geen die installatiekopie Hallo van alle gevoelige informatie is uitgeschakeld of geschikt is voor de herdistributie van garantie.
 
3. Type **y** toocontinue. U kunt Hallo toevoegen **-afdwingen** parameter tooavoid deze bevestigingsstap.
4. Nadat het Hallo-opdracht is voltooid, typt u **sluiten**. Deze stap wordt gesloten Hallo SSH-client.

## <a name="step-2-capture-hello-vm"></a>Stap 2: Hallo VM vastleggen
Gebruik hello Azure CLI toogeneralize en Hallo VM vastleggen. In Hallo vervangen volgende voorbeelden parameternamen voorbeeld door uw eigen waarden. De namen van de voorbeeld-parameter **myResourceGroup**, **myVnet**, en **myVM**.

1. Open in uw lokale computer hello Azure CLI en [aanmelding tooyour Azure-abonnement](../../xplat-cli-connect.md). 
2. Zorg ervoor dat u in de modus Resource Manager.
   
    ```azurecli
    azure config mode arm
    ```
3. Virtuele machine die u al gemaakt met behulp van de volgende opdracht Hallo Hallo afsluiten:
   
    ```azurecli
    azure vm deallocate -g myResourceGroup -n myVM
    ```
4. Generalize Hallo VM Hello volgende opdracht:
   
    ```azurecli
    azure vm generalize -g myResourceGroup -n myVM
    ```
5. Voer nu Hallo **azure vm vastleggen** opdracht, welke opnamen Hallo VM. In Hallo voorbeeld te volgen, Hallo installatiekopie van VHD's met vastleggen namen die beginnen met **MyVHDNamePrefix**, en Hallo **-t** optie geeft u een pad toohello sjabloon **MyTemplate.json**. 
   
    ```azurecli
    azure vm capture -g myResourceGroup -n myVM -p myVHDNamePrefix -t myTemplate.json
    ```
   
   > [!IMPORTANT]
   > Hallo installatiekopie VHD-bestanden gemaakt in hetzelfde opslagaccount die oorspronkelijke VM Hallo gebruikt Hallo standaard. Gebruik Hallo *hetzelfde opslagaccount* toostore Hallo VHD's voor een nieuwe virtuele machines die u uit Hallo installatiekopie maken. 

6. toofind hello locatie van een vastgelegde installatiekopie open Hallo JSON-sjabloon in een teksteditor. In Hallo **storageProfile**, Hallo zoeken **uri** Hallo **installatiekopie** zich in Hallo **system** container. Bijvoorbeeld: hello URI Hallo OS schijfkopie lijkt te`https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`

## <a name="step-3-create-a-vm-from-hello-captured-image"></a>Stap 3: Een virtuele machine maken vanuit Hallo vastgelegde installatiekopie
Nu Hallo installatiekopie gebruiken met een sjabloon toocreate een Linux-VM. Deze stappen ziet u hoe toouse hello Azure CLI en Hallo JSON-bestandssjabloon vastgelegd van toocreate Hallo VM in een nieuw virtueel netwerk.

### <a name="create-network-resources"></a>Maken van netwerkbronnen
toouse hello sjabloon, moet u eerst tooset van een virtueel netwerk en de NIC voor uw nieuwe virtuele machine. U wordt aangeraden maken van een resourcegroep voor deze resources op Hallo-locatie waar uw VM-installatiekopie is opgeslagen. Voer de opdrachten vergelijkbare toohello te volgen, vervangen door namen voor uw resources en juiste Azure locatie ('centralus' in deze opdrachten):

```azurecli
azure group create myResourceGroup1 -l "centralus"

azure network vnet create myResourceGroup1 myVnet -l "centralus"

azure network vnet subnet create myResourceGroup1 myVnet mySubnet

azure network public-ip create myResourceGroup1 myPublicIP -l "centralus"

azure network nic create myResourceGroup1 myNIC -k mySubnet -m myVnet -p myPublicIP -l "centralus"
```

### <a name="get-hello-id-of-hello-nic"></a>Hallo Hallo NIC-Id ophalen
toodeploy een virtuele machine uit Hallo installatiekopie met behulp van Hallo JSON die u hebt opgeslagen tijdens het vastleggen, moet u Hallo-Id van Hallo NIC. Het door het uitvoeren van de volgende opdracht Hallo verkrijgen:

```azurecli
azure network nic show myResourceGroup1 myNIC
```

Hallo **Id** in Hallo uitvoer ziet er ongeveer te`/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic`

### <a name="create-a-vm"></a>Een virtuele machine maken
Nu uitvoeren Hallo volgende toocreate opdracht vastgelegd uw VM van Hallo VM-installatiekopie. Gebruik Hallo **-f** parameter toospecify Hallo pad toohello sjabloon JSON bestand opgeslagen.

```azurecli
azure group deployment create myResourceGroup1 MyDeployment -f MyTemplate.json
```

In de opdrachtuitvoer hello, vraag toosupply zijn een nieuwe VM-naam, Hallo beheerdersgebruikersnaam en wachtwoord en Hallo-Id van Hallo NIC die u eerder hebt gemaakt.

```bash
info:    Executing command group deployment create
info:    Supply values for hello following parameters
vmName: myNewVM
adminUserName: myAdminuser
adminPassword: ********
networkInterfaceId: /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resource Groups/myResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic
```

Hallo volgende voorbeeld ziet u wat u voor een geslaagde implementatie zien:

```bash
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment xxxxxxx
+ Waiting for deployment toocomplete
data:    DeploymentName     : MyDeployment
data:    ResourceGroupName  : MyResourceGroup1
data:    ProvisioningState  : Succeeded
data:    Timestamp          : xxxxxxx
data:    Mode               : Incremental
data:    Name                Type          Value

data:    ------------------  ------------  -------------------------------------

data:    vmName              String        myNewVM

data:    vmSize              String        Standard_D1

data:    adminUserName       String        myAdminuser

data:    adminPassword       SecureString  undefined

data:    networkInterfaceId  String        /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic
info:    group deployment create command OK
```

### <a name="verify-hello-deployment"></a>Hallo-implementatie controleren
Nu SSH toohello virtuele machine u tooverify Hallo implementatie en begin met behulp van gemaakt Hallo nieuwe virtuele machine. tooconnect via SSH, Hallo IP-adres van de virtuele machine die u hebt gemaakt door het uitvoeren van de volgende opdracht Hallo Hallo vinden:

```azurecli
azure network public-ip show myResourceGroup1 myPublicIP
```

Hallo openbaar IP-adres wordt vermeld in de opdrachtuitvoer Hallo. U maken standaard verbinding toohello Linux-VM met SSH op poort 22.

## <a name="create-additional-vms"></a>Aanvullende virtuele machines maken
Gebruik Hallo vastgelegde installatiekopie en de sjabloon toodeploy extra virtuele machines met Hallo stappen in de voorgaande sectie Hallo. Andere opties toocreate virtuele machines van de installatiekopie van het Hallo opnemen met behulp van een sjabloon Quick Start of Hallo uitgevoerd **azure vm maken** opdracht.

### <a name="use-hello-captured-template"></a>Vastgelegde Hallo-sjabloon gebruiken
Hallo toouse vastgelegde installatiekopie en de sjabloon, als volgt te werk (beschreven in voorgaande sectie Hallo):

* Zorg ervoor dat uw VM-installatiekopie Hallo hetzelfde opslagaccount die als host fungeert voor uw VM VHD.
* Hallo sjabloon JSON-bestand kopiëren en geef een unieke naam voor de besturingssysteemschijf Hallo Hallo nieuwe VM VHD (of VHD's). Bijvoorbeeld in Hallo **storageProfile**onder **vhd**in **uri**, Geef een unieke naam voor Hallo **osDisk** VHD vergelijkbaar te`https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`
* Maak een NIC in beide Hallo dezelfde of een ander virtueel netwerk.
* Hallo gewijzigd sjabloon JSON-bestand gebruikt, maakt u een implementatie in de resourcegroep Hallo in waarmee u een virtueel netwerk Hallo instellen.

### <a name="use-a-quickstart-template"></a>Een Quick Start-sjabloon gebruiken
Als u instellen automatisch wanneer u een virtuele machine van de installatiekopie van het Hallo maakt Hallo-netwerk wilt, kunt u deze resources in een sjabloon. Zie bijvoorbeeld Hallo [101-vm-van-gebruiker-image sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) vanuit GitHub. Deze sjabloon maakt een virtuele machine van uw aangepaste installatiekopie en Hallo nodig virtueel netwerk, openbare IP-adres en NIC-resources. Zie voor een overzicht van het gebruik van de sjabloon Hallo in hello Azure-portal [hoe een virtuele machine van een aangepaste installatiekopie met Resource Manager-sjabloon toocreate](http://codeisahighway.com/how-to-create-a-virtual-machine-from-a-custom-image-using-an-arm-template/).

### <a name="use-hello-azure-vm-create-command"></a>Gebruik hello azure vm-opdracht maken
Meestal is het eenvoudigste toouse een Resource Manager-sjabloon toocreate een virtuele machine uit Hallo-installatiekopie. U kunt echter Hallo VM maken *imperatively* met behulp van Hallo **azure vm maken** opdracht Hello **-Q** (**--installatiekopie urn**) parameter . Als u deze methode gebruikt, u ook Hallo doorgeven **-d** (**--os-schijf-vhd**) parameter toospecify Hallo locatie van de VHD-bestand voor Hallo OS Hallo nieuwe virtuele machine. Dit bestand moet zich in Hallo VHD's container van Hallo opslagaccount waar Hallo installatiekopie VHD-bestand wordt opgeslagen. opdracht kopieën hello VHD voor Hallo Hallo nieuwe virtuele machine automatisch toohello **VHD's** container.

Voordat u **azure vm maken** voltooien met installatiekopie van het Hallo Hallo stappen te volgen:

1. Een resourcegroep maken of een bestaande resourcegroep voor Hallo implementatie identificeren.
2. Maken van een openbare IP-adres resource en een NIC-resource voor Hallo nieuwe virtuele machine. Zie eerder in dit artikel voor stappen toocreate de een virtueel netwerk, openbare IP-adres en NIC met behulp van Hallo CLI. (**azure vm maken** kunt ook een NIC maken, maar moet u extra parameters toopass voor een virtueel netwerk en subnet.)

Voer vervolgens een opdracht die wordt doorgegeven URI's tooboth Hallo nieuwe OS-VHD-bestand en Hallo bestaande installatiekopie. In dit voorbeeld wordt een grootte Standard_A1 VM wordt gemaakt in de regio VS-Oost Hallo.

```azurecli
azure vm create -g myResourceGroup1 -n myNewVM -l eastus -y Linux \
-z Standard_A1 -u myAdminname -p myPassword -f myNIC \
-d "https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix.vhd" \
-Q "https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.vhd"
```

Voor extra opdrachtopties, voert u `azure help vm create`.

## <a name="next-steps"></a>Volgende stappen
toomanage uw virtuele machines met Hallo CLI, Zie Hallo taken in [implementeren en beheren van virtuele machines met behulp van Azure Resource Manager-sjablonen en Azure CLI Hallo](create-ssh-secured-vm-from-template.md).

