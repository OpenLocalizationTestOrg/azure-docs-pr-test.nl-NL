---
title: aaaUse een Linux VM probleemoplossing in hello Azure-portal | Microsoft Docs
description: Meer informatie over hoe problemen met de virtuele machine tootroubleshoot Linux via verbindende Hallo OS schijf tooa herstel VM hello Azure-portal
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
ms.date: 11/14/2016
ms.author: iainfou
ms.openlocfilehash: 794daa06d7436215af84a61ab9088524254c47df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-hello-azure-portal"></a>Linux-VM oplossen door het Hallo OS tooa schijfherstel VM koppelen met behulp van hello Azure-portal
Als uw virtuele Linux-machine (VM) een opstart- of -fout optreedt, moet u mogelijk tooperform stappen voor probleemoplossing in het virtuele harde schijf hello, zelf. Een veelvoorkomend voorbeeld is een ongeldige waarde in `/etc/fstab` dat verhindert Hallo VM kunnen tooboot is. De details van dit artikel hoe toouse hello Azure portal tooconnect uw virtuele harde schijf tooanother Linux VM toofix geen fouten bevat en klik vervolgens opnieuw maken van de oorspronkelijke VM.

## <a name="recovery-process-overview"></a>Overzicht van het herstelproces
Hallo procedure voor probleemoplossing is als volgt:

1. Verwijder Hallo VM zonder problemen Hallo virtuele harde schijven te houden.
2. Koppelen en koppelen van Hallo virtuele harde schijf tooanother Linux-VM voor het oplossen van problemen.
3. Verbinding maken met toohello VM probleemoplossing. Bestanden bewerken of toofix problemen van alle hulpprogramma's uitvoeren op Hallo oorspronkelijke virtuele harde schijf.
4. Ontkoppel en Hallo virtuele harde schijf van Hallo probleemoplossing VM loskoppelen.
5. Een virtuele machine maken met Hallo oorspronkelijke virtuele harde schijf.


## <a name="determine-boot-issues"></a>Opstartproblemen bepalen
Bekijk Hallo boot diagnostics- en VM schermafbeelding toodetermine waarom uw virtuele machine niet kunnen tooboot correct is. Een veelvoorkomend voorbeeld is een ongeldige waarde in `/etc/fstab`, of een onderliggende virtuele harde schijf wordt verwijderd of verplaatst.

Selecteer uw virtuele machine in Hallo-portal en schuif omlaag toohello **ondersteuning + probleemoplossing** sectie. Klik op **opstarten diagnostics** tooview Hallo consoleberichten gestreamd vanaf uw virtuele machine. Bekijk Hallo console-logboeken toosee als u kunt vaststellen waarom hello VM wordt uitgevoerd als een probleem. Hallo volgende voorbeeld ziet u dat een virtuele machine is vastgelopen in de onderhoudsmodus die handmatige interactie vereist:

![Diagnostische gegevens over opstarten console weer te geven VM Logboeken](./media/troubleshoot-recovery-disks-portal/boot-diagnostics-error.png)

U kunt ook klikken op **schermafbeelding** aan de bovenkant Hallo van Hallo boot diagnostics logboek toodownload een vastleggen van de schermopname Hallo VM.


## <a name="view-existing-virtual-hard-disk-details"></a>Bestaande virtuele harde schijf details weergeven
Voordat u uw virtuele harde schijf tooanother VM koppelen kunt, moet u tooidentify Hallo-naam van Hallo virtuele harde schijf (VHD). 

Selecteer uw resourcegroep van Hallo-portal en selecteer vervolgens uw storage-account. Klik op **Blobs**, Hallo voorbeeld te volgen:

![Selecteer de storage-blobs](./media/troubleshoot-recovery-disks-portal/storage-account-overview.png)

Hebben doorgaans een container met de naam **VHD's** die de virtuele harde schijven worden opgeslagen. Selecteer Hallo container tooview een lijst met virtuele harde schijven. Opmerking Hallo-naam van uw VHD (Hallo voorvoegsel is gewoonlijk Hallo-naam van uw virtuele machine):

![Identificeren van de VHD in de storage-container](./media/troubleshoot-recovery-disks-portal/storage-container.png)

Uw bestaande virtuele harde schijf in Hallo lijst selecteren en kopiëren Hallo-URL voor gebruik in Hallo stappen te volgen:

![Kopieer de URL van bestaande virtuele harde schijf](./media/troubleshoot-recovery-disks-portal/copy-vhd-url.png)


## <a name="delete-existing-vm"></a>Bestaande virtuele machine verwijderen
Virtuele harde schijven en virtuele machines zijn twee verschillende resources in Azure. Een virtuele harde schijf is waar Hallo besturingssysteem zelf, toepassingen en configuraties worden opgeslagen. Hallo VM zelf zijn gewoon metagegevens die definieert Hallo grootte of de locatie en verwijst naar resources, zoals een virtuele harde schijf of virtuele netwerkinterfacekaart (NIC). Elke virtuele harde schijf heeft een lease toegewezen wanneer gekoppeld tooa VM. Hoewel gegevensschijven kunnen worden gekoppeld en ontkoppeld, zelfs wanneer Hallo VM wordt uitgevoerd, kan de besturingssysteemschijf Hallo kan niet worden losgekoppeld tenzij Hallo VM-resource wordt verwijderd. Hallo lease blijft tooassociate Hallo OS-schijf met een virtuele machine, zelfs wanneer die VM een status gestopt en de toewijzing ongedaan is gemaakt heeft.

eerste stap toorecover Hallo uw VM is toodelete Hallo VM-resource zelf. Verwijderen Hallo VM verlaat Hallo virtuele harde schijven in uw opslagaccount. Na het Hallo die virtuele machine is verwijderd, Hallo virtuele harde schijf tooanother VM tootroubleshoot koppelen en Hallo fouten op te lossen.

Uw virtuele machine in de portal van Hallo selecteren en klik vervolgens op **verwijderen**:

![VM boot diagnostics schermafbeelding opstartfout](./media/troubleshoot-recovery-disks-portal/stop-delete-vm.png)

Wacht totdat het Hallo VM verwijderen voordat u Hallo virtuele harde schijf tooanother VM koppelen is voltooid. Hallo-lease op het virtuele harde schijf hello, waarin deze zijn gekoppeld aan VM Hallo moet toobe vrijgegeven voordat u Hallo virtuele harde schijf tooanother VM kunt koppelen.


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a>Bestaande virtuele harde schijf tooanother VM koppelen
Voor Hallo volgende stappen, u een andere virtuele machine gebruiken voor het oplossen van problemen. U koppelt Hallo bestaande virtuele harde schijf toothis VM toobe kunnen toobrowse probleemoplossing en inhoud van de schijf Hallo bewerken. Dit proces kunt u toocorrect eventuele fouten in de configuratie of revisie aanvullende toepassings- of logboekbestanden, bijvoorbeeld. Kies of maak een ander VM-toouse voor het oplossen van problemen.

1. Selecteer uw resourcegroep van Hallo-portal en selecteer vervolgens uw VM voor het oplossen van problemen. Selecteer **schijven** en klik vervolgens op **Attach bestaande**:

    ![Bestaande schijf in de portal Hallo koppelen](./media/troubleshoot-recovery-disks-portal/attach-existing-disk.png)

2. tooselect uw bestaande virtuele harde schijf klikt u op **VHD-bestand**:

    ![Zoeken naar bestaande VHD](./media/troubleshoot-recovery-disks-portal/select-vhd-location.png)

3. Uw opslagaccount en container selecteren en klik vervolgens op uw bestaande VHD. Klik op Hallo **Selecteer** knop tooconfirm uw keuze:

    ![Uw bestaande VHD selecteren](./media/troubleshoot-recovery-disks-portal/select-vhd.png)

4. Met de VHD die is geselecteerd, klikt u op **OK** tooattach Hallo bestaande virtuele harde schijf:

    ![Bevestig de bestaande virtuele harde schijf koppelen](./media/troubleshoot-recovery-disks-portal/attach-disk-confirm.png)

5. Na enkele seconden Hallo **schijven** deelvenster voor uw virtuele machine een lijst met uw bestaande virtuele harde schijf als een gegevensschijf verbonden:

    ![Bestaande virtuele harde schijf gekoppeld als een gegevensschijf](./media/troubleshoot-recovery-disks-portal/attached-disk.png)


## <a name="mount-hello-attached-data-disk"></a>Hallo bijgesloten gegevensschijf koppelen

> [!NOTE]
> Hallo beschreven hieronder Hallo stappen vereist op een Ubuntu VM. Als u van een andere Linux distro zoals Red Hat Enterprise Linux of SUSE gebruikmaakt, Hallo locaties logboekbestand en `mount` opdrachten mogelijk enigszins anders. Raadpleeg toohello-documentatie voor uw specifieke distro voor Hallo benodigde wijzigingen in de opdrachten.

1. SSH-tooyour het oplossen van problemen met de juiste referenties Hallo VM. Als deze schijf Hallo eerste gegevens schijf is gekoppeld aan tooyour probleemoplossing VM is, is deze waarschijnlijk aangesloten te`/dev/sdc`. Gebruik `dmseg` toolist gekoppelde schijven:

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
Zodra de fouten opgelost zijn, loskoppelen Hallo bestaande virtuele harde schijf van uw VM voor het oplossen van problemen. U kunt de virtuele harde schijf niet gebruiken met een andere VM tot Hallo lease Hallo virtuele harde schijf toohello probleemoplossing VM koppelen is vrijgegeven.

1. Ontkoppelen van Hallo SSH-sessie tooyour VM probleemoplossing, Hallo bestaande virtuele harde schijf. Eerst buiten Hallo van de bovenliggende map voor uw koppelpunt wijzigen:

    ```bash
    cd /
    ```

    Nu Ontkoppel Hallo bestaande virtuele harde schijf. Hallo volgende voorbeeld ontkoppelt Hallo-apparaat op `/dev/sdc1`:

    ```bash
    sudo umount /dev/sdc1
    ```

2. Nu loskoppelen Hallo virtuele harde schijf van Hallo VM. Selecteer uw virtuele machine in Hallo-portal en klik op **schijven**. Selecteer uw bestaande virtuele harde schijf en klik vervolgens op **Detach**:

    ![Loskoppelen van de bestaande virtuele harde schijf](./media/troubleshoot-recovery-disks-portal/detach-disk.png)

    Wacht totdat het Hallo VM heeft Hallo gegevensschijf is losgekoppeld voordat u doorgaat.

## <a name="create-vm-from-original-hard-disk"></a>Virtuele machine van de oorspronkelijke harde schijf maken
toocreate een virtuele machine van de oorspronkelijke virtuele harde schijf gebruiken [deze Azure Resource Manager-sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet). Hallo sjabloon een virtuele machine implementeert in een bestaand virtueel netwerk met behulp van Hallo VHD URL uit Hallo eerder opdracht. Klik op Hallo **tooAzure implementeren** knop als volgt:

![Implementeer de virtuele machine van de sjabloon vanuit GitHub](./media/troubleshoot-recovery-disks-portal/deploy-template-from-github.png)

Hallo-sjabloon wordt geladen in hello Azure-portal voor implementatie. Geef de namen van Hallo voor uw nieuwe virtuele machine en de bestaande Azure-resources en plak Hallo URL tooyour bestaande virtuele harde schijf. toobegin Hallo-implementatie, klikt u op **aankoop**:

![VM van sjabloon implementeren](./media/troubleshoot-recovery-disks-portal/deploy-from-image.png)


## <a name="re-enable-boot-diagnostics"></a>Diagnostische gegevens over opstarten weer inschakelen
Wanneer u uw virtuele machine van Hallo bestaande virtuele harde schijf maakt, kan boot diagnostics niet automatisch worden ingeschakeld. toocheck Hallo status van diagnostische gegevens over opstarten en schakel indien nodig, selecteert u uw virtuele machine in Hallo-portal. Onder **bewaking**, klikt u op **diagnostische instellingen**. Zorg ervoor dat de status van de Hallo **op**, en het selectievakje naast Hallo te**opstarten diagnostics** is geselecteerd. Als u geen wijzigingen aanbrengen, klikt u op **opslaan**:

![Bijwerken van diagnostische gegevens van de instellingen voor opstarten](./media/troubleshoot-recovery-disks-portal/reenable-boot-diagnostics.png)

## <a name="next-steps"></a>Volgende stappen
Als u verbinding maken met tooyour VM problemen ondervindt, raadpleegt u [oplossen SSH-verbindingen tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Zie voor problemen met de toegang tot toepassingen die worden uitgevoerd op de virtuele machine [oplossen verbindingsproblemen van toepassing op een Linux-VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Zie voor meer informatie over het gebruik van Resource Manager [overzicht van Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
