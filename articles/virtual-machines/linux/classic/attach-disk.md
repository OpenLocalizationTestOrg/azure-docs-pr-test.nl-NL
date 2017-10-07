---
title: een schijf tooa Linux VM in Azure aaaAttach | Microsoft Docs
description: Meer informatie over hoe een data tooattach tooa Linux VM schijf met Hallo-Classic deployment model en Hallo schijf initialiseren zodat deze gereed voor gebruik is
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 4901384d-2a6f-4f46-bba0-337a348b7f87
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: c76d8479ac2b522d2b6df658cd28f242473f30ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-data-disk-tooa-linux-virtual-machine"></a>Hoe tooAttach een gegevensschijf tooa virtuele Linux-Machine
> [!IMPORTANT] 
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken. Zie hoe te[een gegevensschijf met Resource Manager-implementatiemodel Hallo koppelen](../add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

U kunt zowel leeg schijven en schijven met gegevens tooyour Azure Virtual machines koppelen. Beide typen schijven zijn VHD-bestanden die zich in een Azure storage-account bevinden. Als bij het toevoegen van een schijf tooa Linux-machine nadat u Hallo schijf koppelt u tooinitialize moet en formatteer deze zodat deze gereed voor gebruik is. Dit artikel gegevens zowel leeg schijven en schijven gegevens tooyour virtuele machines, ook al met hoe toothen initialiseren en formatteren van een nieuwe schijf koppelen.

> [!NOTE]
> Het is een best practice toouse een of meer afzonderlijke schijven toostore gegevens van een virtuele machine. Wanneer u een virtuele machine in Azure maakt, heeft deze een besturingssysteem en een tijdelijke schijf. **Gebruik geen Hallo tijdelijke schijf toostore permanente gegevens.** Zoals Hallo-naam aangeeft, biedt deze alleen tijdelijke opslag. Biedt geen redundantie of back-up omdat deze zich niet in Azure-opslag.
> Hallo tijdelijke schijf is gewoonlijk beheerd door hello Azure Linux Agent en automatisch te worden gekoppeld**mnt/resourcegroep** (of **mnt** Ubuntu afbeeldingen). Op Hallo daarentegen, een gegevensschijf kan de naam van Hallo Linux kernel ongeveer `/dev/sdc`, en u moet toopartition, te maken en koppelen van deze resource. Zie Hallo [gebruikershandleiding voor Azure Linux Agent] [ Agent] voor meer informatie.
> 
> 

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-linux.md)]

## <a name="initialize-a-new-data-disk-in-linux"></a>Initialiseer de gegevensschijf van een nieuwe in Linux
1. SSH tooyour VM. Zie voor meer informatie [hoe toolog op tooa virtuele machine met Linux][Logon].
2. Vervolgens moet u toofind Hallo apparaat-id voor Hallo gegevens schijf tooinitialize. Er zijn twee manieren toodo die:
   
    a) Grep voor SCSI-apparaten in Hallo zich aanmeldt, zoals in de volgende opdracht Hallo:
   
    ```bash
    sudo grep SCSI /var/log/messages
    ```
   
    Recente Ubuntu distributies, moet u wellicht toouse `sudo grep SCSI /var/log/syslog` omdat logboekregistratie te`/var/log/messages` standaard mogelijk uitgeschakeld.
   
    U vindt Hallo-id van het laatste gegevensschijf hello, die is toegevoegd in het Hallo-berichten die worden weergegeven.
   
    ![Hallo schijf berichten ophalen](./media/attach-disk/scsidisklog.png)
   
    OF
   
    b) Hallo gebruik `lsscsi` toofind opdracht out Hallo apparaat-id. `lsscsi` kan worden geïnstalleerd door een van beide `yum install lsscsi` (gebaseerd op Red Hat distributies) of `apt-get install lsscsi` (gebaseerd op Debian distributies). U vindt Hallo schijf die u zoekt door de *lun* of **nummer van de logische eenheid**. Bijvoorbeeld, Hallo *lun* voor Hallo-schijven die u hebt gekoppeld kunnen eenvoudig worden gezien vanaf `azure vm disk list <virtual-machine>` als:

    ```azurecli
    azure vm disk list myVM
    ```

    Hallo-uitvoer is vergelijkbaar toohello volgende:

    ```azurecli
    info:    Executing command vm disk list
    + Fetching disk images
    + Getting virtual machines
    + Getting VM disks
    data:    Lun  Size(GB)  Blob-Name                         OS
    data:    ---  --------  --------------------------------  -----
    data:         30        myVM-2645b8030676c8f8.vhd  Linux
    data:    0    100       myVM-76f7ee1ef0f6dddc.vhd
    info:    vm disk list command OK
    ```
   
    Deze gegevens met de uitvoer van Hallo vergelijken `lsscsi` voor Hallo steekproef dezelfde virtuele machine:
   
    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```
   
    Hallo laatste nummer in de tuple Hallo in elke rij is Hallo *lun*. Zie `man lsscsi` voor meer informatie.
3. Type Hallo volgende opdracht toocreate uw apparaat bij Hallo-prompt:
   
    ```bash
    sudo fdisk /dev/sdc
    ```

4. Wanneer u wordt gevraagd, typt u  **n**  toocreate een partitie.

    ![Apparaat maken](./media/attach-disk/fdisknewpartition.png)

5. Wanneer u wordt gevraagd, typt u **p** toomake Hallo partitie Hallo primaire partitie. Type **1** toomake het eerste partitie Hallo en typ vervolgens tooaccept Hallo-standaardwaarde opgeven voor Hallo cilinder. Het kan standaardwaarden Hallo Hallo eerst weergeven en Hallo laatste sectoren, in plaats van Hallo cilinder op sommige systemen. U kunt deze standaardinstellingen tooaccept.

    ![Partitie maken](./media/attach-disk/fdisknewpartdetails.png)


6. Type **p** toosee Hallo details over Hallo-schijf die wordt opgedeeld.

    ![Schijfgegevens lijst](./media/attach-disk/fdiskpartitiondetails.png)


7. Type **w** toowrite Hallo-instellingen voor Hallo schijf.

    ![Hallo schijfwijzigingen schrijven](./media/attach-disk/fdiskwritedisk.png)

8. Nu kunt u Hallo-bestandssysteem op Hallo nieuwe partitie maken. Hallo partitie nummer toohello apparaat-ID toevoegen (in het volgende voorbeeld Hallo `/dev/sdc1`). Hallo volgende voorbeeld wordt een partitie ext4 op /dev/sdc1:
   
    ```bash
    sudo mkfs -t ext4 /dev/sdc1
    ```
   
    ![Bestandssysteem maken](./media/attach-disk/mkfsext4.png)
   
   > [!NOTE]
   > SuSE Linux Enterprise 11 alleen ondersteuning voor alleen-lezentoegang voor ext4-bestandssystemen. Voor deze systemen wordt tooformat Hallo nieuw bestandssysteem als ext3 in plaats van ext4 aanbevolen.

9. Een directory toomount Hallo nieuwe bestandssysteem, moet u als volgt:
   
    ```bash
    sudo mkdir /datadrive
    ```

10. Ten slotte kunt u Hallo station, als volgt koppelen:
   
    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```
   
    Hallo gegevensschijf is nu gereed toouse als **/datadrive**.
   
    ![Hallo directory en koppelpunten Hallo schijf maken](./media/attach-disk/mkdirandmount.png)

11. Hallo nieuwe station te/etc/fstab toevoegen:
   
    tooensure hello station wordt automatisch opnieuw gekoppeld nadat deze moet opnieuw worden opgestart toohello /etc/fstab bestand toegevoegd. Bovendien is het nadrukkelijk aanbevolen dat die Hallo UUID (Universally Unique IDentifier) wordt gebruikt in /etc/fstab toorefer toohello station in plaats van alleen Hallo apparaatnaam (dat wil zeggen /dev/sdc1). Hallo met UUID Hallo foutieve schijfconfiguratie gekoppelde tooa locatie krijgt als Hallo OS een schijffout gedetecteerd tijdens het opstarten en eventuele resterende gegevensschijven vervolgens wordt toegewezen aan de apparaat-id's wordt voorkomt. toofind Hallo UUID van het nieuwe station hello, kunt u Hallo **blkid** hulpprogramma:
   
    ```bash
    sudo -i blkid
    ```
   
    Hallo-uitvoer ziet er vergelijkbare toohello voorbeeld te volgen:
   
    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

    > [!NOTE]
    > Onjuist bewerken van Hallo **/etc/fstab** bestand kan leiden tot een systeem opgestart. Als u niet zeker, Raadpleeg toohello distributie van documentatie voor informatie over hoe tooproperly dit bestand bewerken. Het is ook raadzaam dat een back-up van Hallo /etc/fstab bestand is gemaakt voordat u bewerkt.

    Open vervolgens Hallo **/etc/fstab** bestand in een teksteditor:

    ```bash
    sudo vi /etc/fstab
    ```

    In dit voorbeeld gebruiken we Hallo UUID-waarde voor Hallo nieuwe **/dev/sdc1** apparaat dat is gemaakt in de vorige stappen Hallo en Hallo koppelpunt **/datadrive**. Voeg na einde van regel toohello Hallo Hallo **/etc/fstab** bestand:

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
    ```

    Of op systemen die op basis van SuSE Linux moet u wellicht toouse een iets andere indeling:

    ```sh
    /dev/disk/by-uuid/33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext3   defaults,nofail   1   2
    ```

    > [!NOTE]
    > Hallo `nofail` optie zorgt ervoor dat Hallo VM start, zelfs als Hallo bestandssysteem beschadigd is of Hallo schijf tijdens het opstarten niet bestaat. Zonder deze optie kunnen optreden gedrag zoals beschreven in [niet kan SSH tooLinux VM vanwege fouten tooFSTAB](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/).

    Nu kunt u testen of Hallo-bestandssysteem is gekoppeld naar behoren ontkoppelen en vervolgens stationseigendom Hallo bestandssysteem, dat wil zeggen gebruikt Hallo voorbeeld koppelpunt `/datadrive` gemaakt in Hallo eerder stappen:

    ```bash
    sudo umount /datadrive
    sudo mount /datadrive
    ```

    Als hello `mount` opdracht, treedt een fout, Controleer Hallo/etc/fstab-bestand voor de juiste syntaxis. Als extra gegevensstations of partities worden gemaakt, / etc/fstab ook afzonderlijk aangaan.

    Hallo station beschrijfbare maken met deze opdracht:

    ```bash
    sudo chmod go+w /datadrive
    ```

    > [!NOTE]
    > Vervolgens kan een gegevensschijf zonder te bewerken fstab verwijdert Hallo VM toofail tooboot. Als dit vaak het geval is, de meeste distributies bieden beide Hallo `nofail` en/of `nobootwait` fstab-opties waarmee een tooboot systeem, zelfs als de schijf Hallo toomount tijdens het opstarten mislukt. Raadpleeg de distributie-documentatie voor meer informatie over deze parameters.

### <a name="trimunmap-support-for-linux-in-azure"></a>TRIM/UNMAP ondersteuning voor Linux in Azure
Sommige kernels Linux ondersteunen TRIM/UNMAP operations toodiscard niet-gebruikte blokken op Hallo schijf. Deze bewerkingen zijn voornamelijk nuttig in standard-opslag tooinform Azure die verwijderde pagina's zijn niet langer geldig en kan worden verwijderd. 'S te verwijderen kunt kosten besparen, als u grote bestanden maken en deze vervolgens te verwijderen.

Er zijn twee manieren tooenable TRIM ondersteunen in uw Linux-VM. Raadpleeg uw distributiepunt gebruikelijke voor Hallo aanbevolen benadering:

* Gebruik Hallo `discard` koppelen optie in `/etc/fstab`, bijvoorbeeld:

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,discard   1   2
    ```

* In sommige gevallen Hallo `discard` optie prestaties gevolgen kan hebben. U kunt ook uitvoeren Hallo `fstrim` opdracht handmatig vanaf de opdrachtregel Hallo of voeg tooyour crontab toorun regelmatig:
  
    **Ubuntu**
  
    ```bash
    sudo apt-get install util-linux
    sudo fstrim /datadrive
    ```
  
    **RHEL/CentOS**
  
    ```bash
    sudo yum install util-linux
    sudo fstrim /datadrive
    ```

## <a name="troubleshooting"></a>Problemen oplossen
[!INCLUDE [virtual-machines-linux-lunzero](../../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a>Volgende stappen
Meer informatie over het gebruik van uw Linux-VM in Hallo artikelen te volgen:

* [Hoe toolog op tooa virtuele machine met Linux][Logon]
* [Hoe toodetach een schijf van een virtuele Linux-machine](detach-disk.md)
* [Hello Azure CLI gebruiken met Hallo klassieke implementatiemodel](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [Configureren van RAID op een virtuele Linux-machine in Azure](../configure-raid.md)
* [LVM configureren op een virtuele Linux-machine in Azure](../configure-lvm.md)

<!--Link references-->
[Agent]:../agent-user-guide.md
[Logon]:../mac-create-ssh-keys.md
