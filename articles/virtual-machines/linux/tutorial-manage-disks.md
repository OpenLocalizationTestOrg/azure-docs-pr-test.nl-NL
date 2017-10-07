---
title: aaaManage Azure schijven Hello Azure CLI | Microsoft Docs
description: Zelfstudie - schijven van Azure met Azure CLI Hallo beheren
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: ad29cfbec5f9738f47705b19d0450c9a2f555492
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-disks-with-hello-azure-cli"></a>Azure-schijven Hello Azure CLI beheren

Azure virtuele machines gebruiken schijven toostore Hallo VMs-besturingssysteem, toepassingen en gegevens. Bij het maken van een virtuele machine is het belangrijk toochoose een schijfgrootte en configuratie juiste toohello verwacht werkbelasting. Deze zelfstudie bevat informatie over het implementeren en beheren van VM-schijven. U meer informatie over:

> [!div class="checklist"]
> * OS-schijven en tijdelijke schijven
> * Gegevensschijven
> * Standard en Premium-schijven
> * Prestaties van de schijf
> * Koppelen en gegevensschijven voorbereiden
> * De schijfgrootte
> * Schijf momentopnamen


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Als u tooinstall kiest en Hallo CLI lokaal gebruiken, deze zelfstudie vereist dat u de versie van de Azure CLI Hallo 2.0.4 worden uitgevoerd of hoger. Voer `az --version` toofind Hallo versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli). 

## <a name="default-azure-disks"></a>Standaard Azure-schijven

Wanneer een virtuele machine van Azure is gemaakt, zijn twee schijven automatisch gekoppelde toohello virtuele machine. 

**Besturingssysteemschijf** - besturingssysteem schijven kunnen worden verkleind up too1 terabyte en hosts Hallo VMs-besturingssysteem. Hallo OS-schijf is gelabeld */dev/sda* standaard. configuratie van de besturingssysteemschijf Hallo van de schijfcache Hallo is geoptimaliseerd voor OS-prestaties. Vanwege deze configuratie Hallo besturingssysteemschijf **beter niet** toepassingen of gegevens hosten. Gebruik voor toepassingen en gegevens gegevensschijven, verderop in dit artikel worden beschreven. 

**Tijdelijke schijf** -tijdelijke schijven gebruiken een SSD-schijf die zich bevindt op Hallo dezelfde Azure-host als Hallo VM. Tijdelijke schijven zijn maximaal zodat en kunnen worden gebruikt voor bewerkingen, zoals tijdelijke gegevensverwerking. Als Hallo VM verplaatste tooa nieuwe host is, wordt echter gegevens die zijn opgeslagen op een tijdelijke schijf verwijderd. Hallo-grootte van de tijdelijke schijf hello wordt bepaald door Hallo VM-grootte. Tijdelijke schijven zijn gelabeld */dev/sdb* en hebben een koppelpunt van *mnt*.

### <a name="temporary-disk-sizes"></a>Tijdelijke schijfgrootten

| Type | VM-grootte | Maximumgrootte van tijdelijke schijf (GB) |
|----|----|----|
| [Algemeen doel](sizes-general.md) | A en D-reeks | 800 |
| [Geoptimaliseerde rekenkracht](sizes-compute.md) | F-serie | 800 |
| [Geoptimaliseerd geheugen](../virtual-machines-windows-sizes-memory.md) | D en G-serie | 6144 |
| [Geoptimaliseerde opslag](../virtual-machines-windows-sizes-storage.md) | L-reeks | 5630 |
| [GPU](sizes-gpu.md) | N reeks | 1440 |
| [Hoge prestaties](sizes-hpc.md) | A en H reeks | 2000 |

## <a name="azure-data-disks"></a>Azure gegevensschijven

Extra gegevensschijven kunnen worden toegevoegd voor het installeren van toepassingen en gegevens op te slaan. Gegevensschijven moeten worden gebruikt in een situatie waarin de opslag van gegevens duurzaam en responsief gewenst is. Elke gegevensschijf heeft een maximale capaciteit van 1 terabyte. Hallo-grootte van Hallo virtuele machine bepaalt hoeveel gegevensschijven kunnen worden aangesloten tooa VM. Voor elke VM-core, kunnen twee schijven worden gekoppeld. 

### <a name="max-data-disks-per-vm"></a>Maximum aantal gegevensschijven per VM

| Type | VM-grootte | Maximum aantal gegevensschijven per VM |
|----|----|----|
| [Algemeen doel](sizes-general.md) | A en D-reeks | 32 |
| [Geoptimaliseerde rekenkracht](sizes-compute.md) | F-serie | 32 |
| [Geoptimaliseerd geheugen](../virtual-machines-windows-sizes-memory.md) | D en G-serie | 64 |
| [Geoptimaliseerde opslag](../virtual-machines-windows-sizes-storage.md) | L-reeks | 64 |
| [GPU](sizes-gpu.md) | N reeks | 48 |
| [Hoge prestaties](sizes-hpc.md) | A en H reeks | 32 |

## <a name="vm-disk-types"></a>VM-schijftypen

Azure biedt twee typen van de schijf.

### <a name="standard-disk"></a>Standard-schijven

Standard Storage wordt ondersteund door HDD's en biedt voordelige en hoogwaardige opslag. Standaardschijven zijn ideaal voor een voordelige ontwikkelen en testen werkbelasting.

### <a name="premium-disk"></a>Premium-schijf

Premium-schijven worden ondersteund door de hoge prestaties, lage latentie SSD-schijf. Ideaal voor virtuele machines met productie werkbelasting. Premium-opslag ondersteunt DS-serie, DSv2-serie GS-serie en virtuele machines FS-serie. Premium-schijven zijn drie typen (P10, P20, P30), Hallo grootte van Hallo schijf Hallo schijftype bepaalt. Wanneer u selecteert, wordt de waarde van een schijf grootte Hallo toohello volgende type afgerond. Als de schijfgrootte Hallo minder dan 128 GB is, is het schijftype Hallo P10. Als de schijfgrootte Hallo tussen 129 en 512 GB, is Hallo grootte een P20. Meer dan 512 GB Hallo grootte is een P30.

### <a name="premium-disk-performance"></a>Premium-schijfprestaties

|Premium-opslag schijftype | P10 | P20 | P30 |
| --- | --- | --- | --- |
| Grootte van de schijf (afronden) | 128 GB | 512 GB | 1.024 GB (1 TB) |
| Max. aantal IOP's per schijf | 500 | 2,300 | 5,000 |
Doorvoer per schijf | 100 MB/s | 150 MB/s | 200 MB/s |

Tijdens het Hallo boven tabel identificeert max. IOP's per schijf, kan een hoger niveau van de prestaties van worden bereikt door meerdere gegevensschijven te verwijderen. Een VM Standard_GS5 kunt bijvoorbeeld een maximumaantal IOPS 80.000 bereiken. Zie voor gedetailleerde informatie over max. IOP's per VM [Linux VM-grootten](sizes.md).

## <a name="create-and-attach-disks"></a>Maken en koppelen van schijven

Gegevensschijven worden gemaakt en gekoppeld op tijd voor het maken van VM of tooan bestaande virtuele machine.

### <a name="attach-disk-at-vm-creation"></a>Schijf bij het maken van de virtuele machine koppelen

Een resourcegroep maken met de Hallo [az groep maken](https://docs.microsoft.com/cli/azure/group#create) opdracht. 

```azurecli-interactive 
az group create --name myResourceGroupDisk --location eastus
```

Een virtuele machine maken met Hallo [az vm maken]( /cli/azure/vm#create) opdracht. Hallo `--datadisk-sizes-gb` argument gebruikte toospecify dat een extra schijf moet worden gemaakt en gekoppeld toohello virtuele machine is. toocreate en meer dan één schijf koppelen, voert u een door spaties gescheiden lijst met grootten van de schijf. In Hallo voorbeeld te volgen, wordt een virtuele machine gemaakt met twee gegevensschijven, beide 128 GB. Omdat de schijfgrootten Hallo 128 GB, zijn deze schijven geconfigureerd als P10s waarmee maximaal 500 IOP's per schijf.

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupDisk \
  --name myVM \
  --image UbuntuLTS \
  --size Standard_DS2_v2 \
  --data-disk-sizes-gb 128 128 \
  --generate-ssh-keys
```

### <a name="attach-disk-tooexisting-vm"></a>Schijf tooexisting VM koppelen

toocreate en koppelen van een nieuwe schijf tooan bestaande virtuele machine, gebruikt u Hallo [az vm schijf koppelen](/cli/azure/vm/disk#attach) opdracht. Hallo volgende voorbeeld wordt een premium-schijf 128 GB in grootte, en wordt deze toohello die VM in de laatste stap Hallo gemaakt.

```azurecli-interactive 
az vm disk attach --vm-name myVM --resource-group myResourceGroupDisk --disk myDataDisk --size-gb 128 --sku Premium_LRS --new 
```

## <a name="prepare-data-disks"></a>Gegevensschijven voorbereiden

Als een schijf is aangesloten toohello virtuele machine, moet Hallo besturingssysteem geconfigureerd toobe toouse Hallo schijf. Hallo volgende voorbeeld ziet u hoe toomanually configureren voor een schijf. Dit proces kan ook worden geautomatiseerd met behulp van cloud-init, die wordt beschreven in een [hoger zelfstudie](./tutorial-automate-vm-deployment.md).

### <a name="manual-configuration"></a>Handmatige configuratie

Een SSH-verbinding maken met Hallo virtuele machine. Hallo voorbeeld IP-adres vervangen door Hallo openbare IP-adres van Hallo virtuele machine.

```azurecli-interactive 
ssh 52.174.34.95
```

Hallo schijf partitioneren met `fdisk`.

```bash
(echo n; echo p; echo 1; echo ; echo ; echo w) | sudo fdisk /dev/sdc
```

Een partitie bestandssysteem toohello schrijven met behulp van Hallo `mkfs` opdracht.

```bash
sudo mkfs -t ext4 /dev/sdc1
```

Hallo nieuwe schijf koppelen zodat deze toegankelijk is in Hallo-besturingssysteem.

```bash
sudo mkdir /datadrive && sudo mount /dev/sdc1 /datadrive
```

Hallo schijf kan nu worden geopend via Hallo *datadrive* koppelpunt die kan worden gecontroleerd door het uitvoeren van Hallo `df -h` opdracht. 

```bash
df -h
```

Hallo uitvoer toont Hallo nieuw station gekoppeld aan */datadrive*.

```bash
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        30G  1.4G   28G   5% /
/dev/sdb1       6.8G   16M  6.4G   1% /mnt
/dev/sdc1        50G   52M   47G   1% /datadrive
```

tooensure dat station Hallo opnieuw na opnieuw opstarten is gekoppeld, moet deze worden toegevoegd toohello */etc/fstab* bestand. toodo ophalen dus Hallo UUID van de schijf Hallo Hello `blkid` hulpprogramma.

```bash
sudo -i blkid
```

Hallo-uitvoer geeft Hallo UUID van Hallo-station `/dev/sdc1` in dit geval.

```bash
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

Toevoegen van een regel vergelijkbaar toohello na toohello */etc/fstab* bestand. Ook dat barrières schrijven kan worden uitgeschakeld met *blokkade = 0*, deze configuratie kan de schijf worden verbeterd. 

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive  ext4    defaults,nofail,barrier=0   1  2
```

Nu dat hello schijf is geconfigureerd, sluit u Hallo SSH-sessie.

```bash
exit
```

## <a name="resize-vm-disk"></a>Formaat van VM-schijf

Wanneer een virtuele machine is geïmplementeerd, kunnen Hallo besturingssysteemschijf of schijven bijgesloten gegevens worden vergroot. Hallo vergroten met een schijf is handig wanneer hoeven meer opslagruimte of een hoger niveau van de prestaties (P10, P20, P30). Houd er rekening mee schijven in grootte kunnen niet worden verhoogd.

Voordat u voor de grootte van de schijf, Hallo Id of naam van Hallo schijf nodig. Gebruik Hallo [az Schijflijst](/cli/azure/vm/disk#list) opdracht tooreturn alle schijven in een resourcegroep. Noteer de naam van de schijf Hallo dat u tooresize wilt.

```azurecli-interactive 
az disk list -g myResourceGroupDisk --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' --output table
```

Er moet ook Hallo VM toewijzing ongedaan is gemaakt. Gebruik Hallo [az vm ongedaan]( /cli/azure/vm#deallocate) opdracht toostop en Hallo VM ongedaan gemaakt.

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupDisk --name myVM
```

Gebruik Hallo [az schijf update](/cli/azure/vm/disk#update) opdracht tooresize Hallo schijf. In dit voorbeeld wordt een schijf met de naam het formaat *myDataDisk* too1 terabyte.

```azurecli-interactive 
az disk update --name myDataDisk --resource-group myResourceGroupDisk --size-gb 1023
```

Nadat de bewerking formaat Hallo is voltooid, start u Hallo VM.

```azurecli-interactive 
az vm start --resource-group myResourceGroupDisk --name myVM
```

Als u het formaat Hallo systeemschijf besturingssysteem hebt gewijzigd, wordt automatisch Hallo partitie worden uitgebreid. Als u het formaat van een gegevensschijf hebt gewijzigd, moeten alle huidige partities toobe uitgevouwen in Hallo VMs-besturingssysteem.

## <a name="snapshot-azure-disks"></a>Momentopname maken van Azure-schijven

Maken van een momentopname van de schijf, maakt een lezen alleen, punt in tijd kopie van Hallo schijf. Azure VM-momentopnamen zijn handig voor het snel Hallo status van een virtuele machine opslaan voordat u configuratiewijzigingen in. In Hallo gebeurtenis hello configuratiewijzigingen bewijzen toobe ongewenste, status virtuele machine kan worden hersteld met een Hallo momentopname. Wanneer een virtuele machine meer dan één schijf heeft, een momentopname wordt gemaakt van elke schijf onafhankelijk van Hallo anderen. Overweeg Hallo VM stoppen voordat het maken van momentopnamen van de schijf voor het maken van de toepassing consistente back-ups. Ook gebruiken Hallo [Azure Backup-service](/azure/backup/), zodat u tooperform automatische back-ups tijdens het Hallo VM wordt uitgevoerd.

### <a name="create-snapshot"></a>Momentopname maken

Voordat u een momentopname van de virtuele machine schijf maakt, Hallo-Id of naam van de schijf Hallo is vereist. Gebruik Hallo [az vm weergeven](https://docs.microsoft.com/en-us/cli/azure/vm#show) opdracht tooreturn Hallo schijf-id. In dit voorbeeld Hallo schijf-id in een variabele opgeslagen, zodat deze kan worden gebruikt in een later stadium.

```azurecli-interactive 
osdiskid=$(az vm show -g myResourceGroupDisk -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
```

Nu dat u Hallo-id van de schijf van de virtuele machine hello hebt, hello volgende opdracht maakt een momentopname van Hallo schijf.

```azurcli
az snapshot create -g myResourceGroupDisk --source "$osdiskid" --name osDisk-backup
```

### <a name="create-disk-from-snapshot"></a>Schijf maken vanuit een momentopname.

Deze momentopname kan vervolgens worden geconverteerd naar een schijf, wat kan gebruikte toorecreate Hallo virtuele machine.

```azurecli-interactive 
az disk create --resource-group myResourceGroupDisk --name mySnapshotDisk --source osDisk-backup
```

### <a name="restore-virtual-machine-from-snapshot"></a>Virtuele machine herstellen vanuit een momentopname.

toodemonstrate virtuele machine is hersteld, delete Hallo bestaande virtuele machine. 

```azurecli-interactive 
az vm delete --resource-group myResourceGroupDisk --name myVM
```

Maak een nieuwe virtuele machine van Hallo momentopname schijf.

```azurecli-interactive 
az vm create --resource-group myResourceGroupDisk --name myVM --attach-os-disk mySnapshotDisk --os-type linux
```

### <a name="reattach-data-disk"></a>Gegevensschijf opnieuw koppelen

Alle gegevensschijven moeten toobe opnieuw gekoppeld toohello virtuele machine.

Zoek eerst Hallo schijfnaam voor gegevens met behulp van Hallo [az Schijflijst](https://docs.microsoft.com/cli/azure/disk#list) opdracht. In dit voorbeeld plaatsen Hallo naam van de schijf Hallo in een variabele met de naam *datadisk*, die wordt gebruikt in de volgende stap Hallo.

```azurecli-interactive 
datadisk=$(az disk list -g myResourceGroupDisk --query "[?contains(name,'myVM')].[name]" -o tsv)
```

Gebruik Hallo [az vm schijf koppelen](https://docs.microsoft.com/cli/azure/vm/disk#attach) opdracht tooattach Hallo schijf.

```azurecli-interactive 
az vm disk attach –g myResourceGroupDisk –-vm-name myVM –-disk $datadisk
```

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie hebt u geleerd over VM schijven onderwerpen, zoals:

> [!div class="checklist"]
> * OS-schijven en tijdelijke schijven
> * Gegevensschijven
> * Standard en Premium-schijven
> * Prestaties van de schijf
> * Koppelen en gegevensschijven voorbereiden
> * De schijfgrootte
> * Schijf momentopnamen

Ga toohello volgende zelfstudie toolearn over het automatiseren van VM-configuratie.

> [!div class="nextstepaction"]
> [VM-configuratie automatiseren](./tutorial-automate-vm-deployment.md)
