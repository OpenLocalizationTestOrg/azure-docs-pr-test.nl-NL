---
title: aaaUse een Linux VM Hello Azure CLI 1.0 probleemoplossing | Microsoft Docs
description: Meer informatie over hoe tootroubleshoot Linux VM verstrekt via verbindende Hallo OS schijf tooa herstel VM hello Azure CLI 1.0
services: virtual-machines-linux
documentationCenter: 
authors: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 398f681d1149299d444fcfdab20737315db02855
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-hello-azure-cli-10"></a>Linux-VM oplossen door het Hallo OS tooa schijfherstel VM koppelen met behulp van Azure CLI 1.0 Hallo
Als uw virtuele Linux-machine (VM) een opstart- of -fout optreedt, moet u mogelijk tooperform stappen voor probleemoplossing in het virtuele harde schijf hello, zelf. Een veelvoorkomend voorbeeld is een ongeldige waarde in `/etc/fstab` dat verhindert Hallo VM kunnen tooboot is. De details van dit artikel hoe toouse hello Azure CLI 1.0 tooconnect uw virtuele harde schijf tooanother Linux VM toofix geen fouten bevat en klik vervolgens opnieuw maken van de oorspronkelijke VM.


## <a name="cli-versions-toocomplete-hello-task"></a>CLI-versies toocomplete Hallo taak
U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:

- [Azure CLI 1.0](#recovery-process-overview) – onze CLI voor Hallo klassieke en resource management implementatiemodellen (in dit artikel)
- [Azure CLI 2.0](../windows/troubleshoot-recovery-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel


## <a name="recovery-process-overview"></a>Overzicht van het herstelproces
Hallo procedure voor probleemoplossing is als volgt:

1. Verwijder Hallo VM zonder problemen Hallo virtuele harde schijven te houden.
2. Koppelen en koppelen van Hallo virtuele harde schijf tooanother Linux-VM voor het oplossen van problemen.
3. Verbinding maken met toohello VM probleemoplossing. Bestanden bewerken of toofix problemen van alle hulpprogramma's uitvoeren op Hallo oorspronkelijke virtuele harde schijf.
4. Ontkoppel en Hallo virtuele harde schijf van Hallo probleemoplossing VM loskoppelen.
5. Een virtuele machine maken met Hallo oorspronkelijke virtuele harde schijf.

Zorg ervoor dat u hebt [nieuwste Azure CLI 1.0 Hallo](../../cli-install-nodejs.md) geïnstalleerd en geregistreerd in en gebruikt de modus Resource Manager:

```azurecli
azure config mode arm
```

In Hallo vervangen volgende voorbeelden parameternamen door uw eigen waarden. De namen van de voorbeeld-parameter `myResourceGroup`, `mystorageaccount`, en `myVM`.


## <a name="determine-boot-issues"></a>Opstartproblemen bepalen
Hallo seriële uitvoer toodetermine waarom uw virtuele machine niet kunnen tooboot correct is onderzoeken. Een veelvoorkomend voorbeeld is een ongeldige waarde in `/etc/fstab`, of Hallo onderliggende virtuele harde schijf wordt verwijderd of verplaatst.

Hallo volgende voorbeeld krijgt Hallo seriële uitvoer van Hallo VM met de naam `myVM` in Hallo resourcegroep met de naam `myResourceGroup`:

```azurecli
azure vm get-serial-output --resource-group myResourceGroup --name myVM
```

Hallo seriële uitvoer toodetermine waarom hello VM tooboot mislukt bekijken. Als Hallo seriële uitvoer is niet een aanwijzing bieden, moet u mogelijk de logboekbestanden tooreview in `/var/log` zodra er Hallo virtuele harde schijf tooa probleemoplossing VM gekoppeld.


## <a name="view-existing-virtual-hard-disk-details"></a>Bestaande virtuele harde schijf details weergeven
Voordat u uw virtuele harde schijf tooanother VM koppelen kunt, moet u tooidentify Hallo-naam van Hallo virtuele harde schijf (VHD). 

Hallo volgende voorbeeld worden gegevens opgehaald voor virtuele machine met de naam Hallo `myVM` in Hallo resourcegroep met de naam `myResourceGroup`:

```azurecli
azure vm show --resource-group myResourceGroup --name myVM
```

Zoek naar `Vhd URI` in Hallo-uitvoer van de voorgaande opdracht Hallo. Hallo volgende ingekorte voorbeelduitvoer wordt weergegeven Hallo `Vhd URI` op Hallo laatste regel:

```azurecli
info:    Executing command vm show
+ Looking up hello VM "myVM"
+ Looking up hello NIC "myNic"
+ Looking up hello public ip "myPublicIP"
...
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :myVM
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://mystorageaccount.blob.core.windows.net/vhds/myVM201610292712.vhd
```


## <a name="delete-existing-vm"></a>Bestaande virtuele machine verwijderen
Virtuele harde schijven en virtuele machines zijn twee verschillende resources in Azure. Een virtuele harde schijf is waar Hallo besturingssysteem zelf, toepassingen en configuraties worden opgeslagen. Hallo VM zelf zijn gewoon metagegevens die definieert Hallo grootte of de locatie en verwijst naar resources, zoals een virtuele harde schijf of virtuele netwerkinterfacekaart (NIC). Elke virtuele harde schijf heeft een lease toegewezen wanneer gekoppeld tooa VM. Hoewel gegevensschijven kunnen worden gekoppeld en ontkoppeld, zelfs wanneer Hallo VM wordt uitgevoerd, kan de besturingssysteemschijf Hallo kan niet worden losgekoppeld tenzij Hallo VM-resource wordt verwijderd. Hallo lease blijft tooassociate Hallo OS-schijf met een virtuele machine, zelfs wanneer die VM een status gestopt en de toewijzing ongedaan is gemaakt heeft.

eerste stap toorecover Hallo uw VM is toodelete Hallo VM-resource zelf. Verwijderen Hallo VM verlaat Hallo virtuele harde schijven in uw opslagaccount. Na het Hallo die virtuele machine is verwijderd, Hallo virtuele harde schijf tooanother VM tootroubleshoot koppelen en Hallo fouten op te lossen.

Hallo volgende voorbeeld verwijdert met de naam VM Hallo `myVM` van Hallo resourcegroep met de naam `myResourceGroup`:

```azurecli
azure vm delete --resource-group myResourceGroup --name myVM 
```

Wacht totdat het Hallo VM verwijderen voordat u Hallo virtuele harde schijf tooanother VM koppelen is voltooid. Hallo-lease op het virtuele harde schijf hello, waarin deze zijn gekoppeld aan VM Hallo moet toobe vrijgegeven voordat u Hallo virtuele harde schijf tooanother VM kunt koppelen.


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a>Bestaande virtuele harde schijf tooanother VM koppelen
Voor Hallo volgende stappen, u een andere virtuele machine gebruiken voor het oplossen van problemen. U koppelt Hallo bestaande virtuele harde schijf toothis VM toobrowse probleemoplossing en inhoud van de schijf Hallo bewerken. Dit proces kunt u toocorrect eventuele fouten in de configuratie of revisie aanvullende toepassings- of logboekbestanden, bijvoorbeeld. Kies of maak een ander VM-toouse voor het oplossen van problemen.

Wanneer u een bestaande virtuele harde schijf van Hallo koppelt, geef Hallo URL toohello schijf verkregen in de voorgaande Hallo `azure vm show` opdracht. Hallo volgende voorbeeld wordt een bestaande virtuele harde schijf toohello het oplossen van problemen met de naam VM `myVMRecovery` in Hallo resourcegroep met de naam `myResourceGroup`:

```azurecli
azure vm disk attach --resource-group myResourceGroup --name myVMRecovery \
    --vhd-url https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
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

2. Nu loskoppelen Hallo virtuele harde schijf van Hallo VM. Hallo SSH-sessie tooyour probleemoplossing VM af te sluiten. Eerste lijst Hallo gekoppeld in hello Azure CLI, gegevens schijven tooyour VM probleemoplossing. Hallo volgt een lijst met gegevensschijven Hallo gekoppeld toohello VM met de naam `myVMRecovery` in Hallo resourcegroep met de naam `myResourceGroup`:

    ```azurecli
    azure vm disk list --resource-group myResourceGroup --vm-name myVMRecovery
    ```

    Opmerking Hallo `Lun` waarde voor de bestaande virtuele harde schijf. Hallo volgende opdracht voorbeelduitvoer wordt weergegeven Hallo bestaande virtuele schijf voor LUN 0 is gekoppeld:

    ```azurecli
    info:    Executing command vm disk list
    + Looking up hello VM "myVMRecovery"
    data:    Name              Lun  DiskSizeGB  Caching  URI
    data:    ------            ---  ----------  -------  ------------------------------------------------------------------------
    data:    myVM              0                None     https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
    info:    vm disk list command OK
    ```

    Hallo gegevensschijf loskoppelen van uw virtuele machine met behulp van toepassing hello `Lun` waarde:

    ```azurecli
    azure vm disk detach --resource-group myResourceGroup --vm-name myVMRecovery \
        --lun 0
    ```


## <a name="create-vm-from-original-hard-disk"></a>Virtuele machine van de oorspronkelijke harde schijf maken
toocreate een virtuele machine van de oorspronkelijke virtuele harde schijf gebruiken [deze Azure Resource Manager-sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd). Hallo werkelijke JSON-sjabloon is op Hallo koppeling:

- https://RAW.githubusercontent.com/Azure/Azure-QuickStart-templates/master/201-VM-Specialized-VHD/azuredeploy.JSON

Hallo sjabloon een virtuele machine implementeert in een bestaand virtueel netwerk met behulp van Hallo VHD URL uit Hallo eerder opdracht. Hallo volgende voorbeeld implementeert Hallo sjabloon toohello resourcegroep met de naam `myResourceGroup`:

```azurecli
azure group deployment create --resource-group myResourceGroup --name myDeployment \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json
```

Antwoord Hallo vraagt om Hallo sjabloon zoals VM-naam (`myDeployedVM` Hallo volgende voorbeeld), type besturingssysteem (`Linux`), en VM-grootte (`Standard_DS1_v2`). Hallo `osDiskVhdUri` is dezelfde als eerder is gebruikt bij het toevoegen van Hallo bestaande virtuele harde schijf toohello probleemoplossing VM Hallo. Een voorbeeld van uitvoer van de opdracht Hallo en wordt u gevraagd is als volgt:

```azurecli
info:    Executing command group deployment create
info:    Supply values for hello following parameters
vmName:  myDeployedVM
osType:  Linux
osDiskVhdUri:  https://mystorageaccount.blob.core.windows.net/vhds/myVM201610292712.vhd
vmSize:  Standard_DS1_v2
existingVirtualNetworkName:  myVnet
existingVirtualNetworkResourceGroup:  myResourceGroup
subnetName:  mySubnet
dnsNameForPublicIP:  mypublicipdeployed
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "mydeployment"
+ Waiting for deployment toocomplete
+
```


## <a name="re-enable-boot-diagnostics"></a>Diagnostische gegevens over opstarten weer inschakelen

Wanneer u uw virtuele machine van Hallo bestaande virtuele harde schijf maakt, kan boot diagnostics niet automatisch worden ingeschakeld. Hallo volgende voorbeeld wordt de diagnostische Hallo-extensie op Hallo VM met de naam `myDeployedVM` in Hallo resourcegroep met de naam `myResourceGroup`:

```azurecli
azure vm enable-diag --resource-group myResourceGroup --name myDeployedVM
```

## <a name="next-steps"></a>Volgende stappen
Als u verbinding maken met tooyour VM problemen ondervindt, raadpleegt u [oplossen SSH-verbindingen tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Zie voor problemen met de toegang tot toepassingen die worden uitgevoerd op de virtuele machine [oplossen verbindingsproblemen van toepassing op een Linux-VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
