---
title: aaaUse een Linux VM Hello Azure CLI 2.0 probleemoplossing | Microsoft Docs
description: Meer informatie over hoe tootroubleshoot Linux VM verstrekt via verbindende Hallo OS schijf tooa herstel VM hello Azure CLI 2.0
services: virtual-machines-linux
documentationCenter: 
authors: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/16/2017
ms.author: iainfou
ms.openlocfilehash: 776d61b61280f46e3699157addcdb1e7dfb6818e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-with-hello-azure-cli-20"></a>Linux-VM oplossen door het koppelen van Hallo OS tooa schijfherstel VM Hello Azure CLI 2.0
Als uw virtuele Linux-machine (VM) een opstart- of -fout optreedt, moet u mogelijk tooperform stappen voor probleemoplossing in het virtuele harde schijf hello, zelf. Een veelvoorkomend voorbeeld is een ongeldige waarde in `/etc/fstab` dat verhindert Hallo VM kunnen tooboot is. De details van dit artikel hoe toouse hello Azure CLI 2.0 tooconnect uw virtuele harde schijf tooanother Linux VM toofix geen fouten bevat en klik vervolgens opnieuw maken van de oorspronkelijke VM. U kunt ook uitvoeren met deze stappen Hello [Azure CLI 1.0](troubleshoot-recovery-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


## <a name="recovery-process-overview"></a>Overzicht van het herstelproces
Hallo procedure voor probleemoplossing is als volgt:

1. Verwijder Hallo VM zonder problemen Hallo virtuele harde schijven te houden.
2. Koppelen en koppelen van Hallo virtuele harde schijf tooanother Linux-VM voor het oplossen van problemen.
3. Verbinding maken met toohello VM probleemoplossing. Bestanden bewerken of toofix problemen van alle hulpprogramma's uitvoeren op Hallo oorspronkelijke virtuele harde schijf.
4. Ontkoppel en Hallo virtuele harde schijf van Hallo probleemoplossing VM loskoppelen.
5. Een virtuele machine maken met Hallo oorspronkelijke virtuele harde schijf.

tooperform deze probleemoplossingsstappen, moet u Hallo nieuwste [Azure CLI 2.0](/cli/azure/install-az-cli2) geïnstalleerd en geregistreerd in Azure-account met behulp van tooan [az aanmelding](/cli/azure/#login).

In Hallo vervangen volgende voorbeelden parameternamen door uw eigen waarden. De namen van de voorbeeld-parameter `myResourceGroup`, `mystorageaccount`, en `myVM`.


## <a name="determine-boot-issues"></a>Opstartproblemen bepalen
Hallo seriële uitvoer toodetermine waarom uw virtuele machine niet kunnen tooboot correct is onderzoeken. Een veelvoorkomend voorbeeld is een ongeldige waarde in `/etc/fstab`, of Hallo onderliggende virtuele harde schijf wordt verwijderd of verplaatst.

Hallo opstarten logboeken met [az vm diagnostische gegevens over opstarten get-boot-logboek](/cli/azure/vm/boot-diagnostics#get-boot-log). Hallo volgende voorbeeld krijgt Hallo seriële uitvoer van Hallo VM met de naam `myVM` in Hallo resourcegroep met de naam `myResourceGroup`:

```azurecli
az vm boot-diagnostics get-boot-log --resource-group myResourceGroup --name myVM
```

Hallo seriële uitvoer toodetermine waarom hello VM tooboot mislukt bekijken. Als Hallo seriële uitvoer is niet een aanwijzing bieden, moet u mogelijk de logboekbestanden tooreview in `/var/log` zodra er Hallo virtuele harde schijf tooa probleemoplossing VM gekoppeld.


## <a name="view-existing-virtual-hard-disk-details"></a>Bestaande virtuele harde schijf details weergeven
Voordat u uw virtuele harde schijf (VHD) tooanother VM koppelen kunt, moet u tooidentify Hallo-URI van de besturingssysteemschijf Hallo. 

Informatie weergeven over uw virtuele machine met [az vm weergeven](/cli/azure/vm#show). Gebruik Hallo `--query` vlag tooextract Hallo URI toohello OS-schijf. Hallo volgende voorbeeld wordt opgehaald schijfgegevens voor virtuele machine met de naam Hallo `myVM` in Hallo resourcegroep met de naam `myResourceGroup`:

```azurecli
az vm show --resource-group myResourceGroup --name myVM \
    --query [storageProfile.osDisk.vhd.uri] --output tsv
```

Hallo URI lijkt te**https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd**.

## <a name="delete-existing-vm"></a>Bestaande virtuele machine verwijderen
Virtuele harde schijven en virtuele machines zijn twee verschillende resources in Azure. Een virtuele harde schijf is waar Hallo besturingssysteem zelf, toepassingen en configuraties worden opgeslagen. Hallo VM zelf zijn gewoon metagegevens die definieert Hallo grootte of de locatie en verwijst naar resources, zoals een virtuele harde schijf of virtuele netwerkinterfacekaart (NIC). Elke virtuele harde schijf heeft een lease toegewezen wanneer gekoppeld tooa VM. Hoewel gegevensschijven kunnen worden gekoppeld en ontkoppeld, zelfs wanneer Hallo VM wordt uitgevoerd, kan de besturingssysteemschijf Hallo kan niet worden losgekoppeld tenzij Hallo VM-resource wordt verwijderd. Hallo lease blijft tooassociate Hallo OS-schijf met een virtuele machine, zelfs wanneer die VM een status gestopt en de toewijzing ongedaan is gemaakt heeft.

eerste stap toorecover Hallo uw VM is toodelete Hallo VM-resource zelf. Verwijderen Hallo VM verlaat Hallo virtuele harde schijven in uw opslagaccount. Na het Hallo die virtuele machine is verwijderd, Hallo virtuele harde schijf tooanother VM tootroubleshoot koppelen en Hallo fouten op te lossen.

Verwijderen met virtuele machine Hallo [az vm verwijderen](/cli/azure/vm#delete). Hallo volgende voorbeeld verwijdert met de naam VM Hallo `myVM` van Hallo resourcegroep met de naam `myResourceGroup`:

```azurecli
az vm delete --resource-group myResourceGroup --name myVM 
```

Wacht totdat het Hallo VM verwijderen voordat u Hallo virtuele harde schijf tooanother VM koppelen is voltooid. Hallo-lease op het virtuele harde schijf hello, waarin deze zijn gekoppeld aan VM Hallo moet toobe vrijgegeven voordat u Hallo virtuele harde schijf tooanother VM kunt koppelen.


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a>Bestaande virtuele harde schijf tooanother VM koppelen
Voor Hallo volgende stappen, u een andere virtuele machine gebruiken voor het oplossen van problemen. U koppelt Hallo bestaande virtuele harde schijf toothis VM toobrowse probleemoplossing en inhoud van de schijf Hallo bewerken. Dit proces kunt u toocorrect eventuele fouten in de configuratie of revisie aanvullende toepassings- of logboekbestanden, bijvoorbeeld. Kies of maak een ander VM-toouse voor het oplossen van problemen.

Koppel Hallo bestaande virtuele harde schijf met [zonder begeleiding az vm-schijf koppelen](/cli/azure/vm/unmanaged-disk#attach). Wanneer u een bestaande virtuele harde schijf van Hallo koppelt, geef Hallo URI toohello schijf verkregen in de voorgaande Hallo `az vm show` opdracht. Hallo volgende voorbeeld wordt een bestaande virtuele harde schijf toohello het oplossen van problemen met de naam VM `myVMRecovery` in Hallo resourcegroep met de naam `myResourceGroup`:

```azurecli
az vm unmanaged-disk attach --resource-group myResourceGroup --vm-name myVMRecovery \
    --vhd-uri https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
```


## <a name="mount-hello-attached-data-disk"></a>Hallo bijgesloten gegevensschijf koppelen

> [!NOTE]
> Hallo beschreven hieronder Hallo stappen vereist op een Ubuntu VM. Als u van een andere Linux distro zoals Red Hat Enterprise Linux of SUSE gebruikmaakt, Hallo locaties logboekbestand en `mount` opdrachten mogelijk enigszins anders. Raadpleeg toohello-documentatie voor uw specifieke distro voor Hallo benodigde wijzigingen in de opdrachten.

1. SSH-tooyour het oplossen van problemen met de juiste referenties Hallo VM. Als deze schijf Hallo eerste gegevens schijf is gekoppeld aan tooyour VM probleemoplossing, Hallo is waarschijnlijk verbonden schijf te`/dev/sdc`. Gebruik `dmseg` tooview gekoppelde schijven:

    ```bash
    dmesg | grep SCSI
    ```

    Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld:

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    In de Hallo voorgaande voorbeeld, Hallo OS-schijf is op `/dev/sda` en Hallo tijdelijke schijf opgegeven voor elke virtuele machine is op `/dev/sdb`. Als u meerdere gegevensschijven had, moeten ze op `/dev/sdd`, `/dev/sde`, enzovoort.

2. Maak een map toomount uw bestaande virtuele harde schijf. Hallo volgende voorbeeld maakt u een map met de naam `troubleshootingdisk`:

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. Als u meerdere partities op de bestaande virtuele harde schijf hebt, koppel Hallo vereist partitie. Hallo volgende voorbeeld koppelt Hallo eerste primaire partitie op `/dev/sdc1`:

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > Aanbevolen procedure is toomount gegevensschijven op virtuele machines in Azure worden verkregen met Hallo (UUID) universally unique identifier van Hallo virtuele harde schijf. Voor dit scenario voor de korte voor probleemoplossing is koppelen Hallo virtuele harde schijf met behulp van Hallo UUID niet nodig. Echter, bij normaal gebruik bewerken `/etc/fstab` toomount virtuele harde schijven met de apparaatnaam van het in plaats van UUID kan ertoe leiden dat Hallo VM toofail tooboot.


## <a name="fix-issues-on-original-virtual-hard-disk"></a>Los problemen op de oorspronkelijke virtuele harde schijf
Hallo bestaande virtuele harde schijf gekoppeld, kunt u eventuele onderhoud en probleemoplossing naar behoefte nu uitvoeren. Zodra u Hallo problemen hebt opgelost, kunt u doorgaan met de Hallo stappen te volgen.


## <a name="unmount-and-detach-original-virtual-hard-disk"></a>Ontkoppel en loskoppelen van de oorspronkelijke virtuele harde schijf
Zodra de fouten opgelost zijn, kunt u ontkoppelen en Hallo bestaande virtuele harde schijf los te koppelen van uw VM voor het oplossen van problemen. U kunt de virtuele harde schijf niet gebruiken met een andere VM tot Hallo lease Hallo virtuele harde schijf toohello probleemoplossing VM koppelen is vrijgegeven.

1. Ontkoppelen van Hallo SSH-sessie tooyour VM probleemoplossing, Hallo bestaande virtuele harde schijf. Eerst buiten Hallo van de bovenliggende map voor uw koppelpunt wijzigen:

    ```bash
    cd /
    ```

    Nu Ontkoppel Hallo bestaande virtuele harde schijf. Hallo volgende voorbeeld ontkoppelt Hallo-apparaat op `/dev/sdc1`:

    ```bash
    sudo umount /dev/sdc1
    ```

2. Nu loskoppelen Hallo virtuele harde schijf van Hallo VM. Hallo SSH-sessie tooyour probleemoplossing VM af te sluiten. Lijst Hallo gegevens schijven tooyour het oplossen van problemen met virtuele machine gekoppeld [az vm zonder begeleiding schijf lijst](/cli/azure/vm/unmanaged-disk#list). Hallo volgt een lijst met gegevensschijven Hallo gekoppeld toohello VM met de naam `myVMRecovery` in Hallo resourcegroep met de naam `myResourceGroup`:

    ```azurecli
    azure vm unmanaged-disk list --resource-group myResourceGroup --vm-name myVMRecovery \
        --query '[].{Disk:vhd.uri}' --output table
    ```

    Houd er rekening mee Hallo-naam voor uw bestaande virtuele harde schijf. Bijvoorbeeld Hallo-naam van een schijf met de URI van Hallo **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd** is **myVHD**. 

    Hallo gegevensschijf loskoppelen van uw virtuele machine [zonder begeleiding az vm-schijf loskoppelen](/cli/azure/vm/unmanaged-disk#detach). Hallo voorbeeld hieronder wordt Hallo-schijf met de naam `myVHD` van Hallo VM met de naam `myVMRecovery` in Hallo `myResourceGroup` resourcegroep:

    ```azurecli
    az vm unmanaged-disk detach --resource-group myResourceGroup --vm-name myVMRecovery \
        --name myVHD
    ```


## <a name="create-vm-from-original-hard-disk"></a>Virtuele machine van de oorspronkelijke harde schijf maken
toocreate een virtuele machine van de oorspronkelijke virtuele harde schijf gebruiken [deze Azure Resource Manager-sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd). Hallo werkelijke JSON-sjabloon is op Hallo koppeling:

- https://RAW.githubusercontent.com/Azure/Azure-QuickStart-templates/master/201-VM-Specialized-VHD/azuredeploy.JSON

Hallo sjabloon implementeert een VM die gebruikmaakt van Hallo VHD-URI van Hallo eerder opdracht. Hallo-sjabloon met implementeren [az implementatie maken](/cli/azure/group/deployment#create). Hallo URI tooyour bieden oorspronkelijke VHD en geef vervolgens Hallo OS-type, de grootte van de VM en VM-naam als volgt:

```azurecli
az group deployment create --resource-group myResourceGroup --name myDeployment \
  --parameters '{"osDiskVhdUri": {"value": "https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd"},
    "osType": {"value": "Linux"},
    "vmSize": {"value": "Standard_DS1_v2"},
    "vmName": {"value": "myDeployedVM"}}' \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json
```

## <a name="re-enable-boot-diagnostics"></a>Diagnostische gegevens over opstarten weer inschakelen
Wanneer u uw virtuele machine van Hallo bestaande virtuele harde schijf maakt, kan boot diagnostics niet automatisch worden ingeschakeld. Schakel diagnostische gegevens over opstarten met [az vm-diagnostische gegevens over opstarten inschakelen](/cli/azure/vm/boot-diagnostics#enable). Hallo volgende voorbeeld wordt de diagnostische Hallo-extensie op Hallo VM met de naam `myDeployedVM` in Hallo resourcegroep met de naam `myResourceGroup`:

```azurecli
az vm boot-diagnostics enable --resource-group myResourceGroup --name myDeployedVM
```

## <a name="next-steps"></a>Volgende stappen
Als u verbinding maken met tooyour VM problemen ondervindt, raadpleegt u [oplossen SSH-verbindingen tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Zie voor problemen met de toegang tot toepassingen die worden uitgevoerd op de virtuele machine [oplossen verbindingsproblemen van toepassing op een Linux-VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
