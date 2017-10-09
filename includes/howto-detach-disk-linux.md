Wanneer u een gegevensschijf die is aangesloten tooa virtuele machine (VM) niet meer nodig hebt, kunt u deze eenvoudig loskoppelen. Wanneer u een schijf van Hallo VM losgekoppeld, Hallo schijf is niet verwijderd uit de opslag. Als u toouse Hallo bestaande gegevens op Hallo schijf opnieuw wilt, u kunt opnieuw het toohello dezelfde virtuele machine of een andere naam.  

> [!NOTE]
> Een VM in Azure gebruikt verschillende soorten schijven: een besturingssysteemschijf, een lokale tijdelijke schijf en optionele gegevensschijven. Zie [Informatie over schijven en VHD's voor virtuele machines](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) voor meer informatie. U kan een schijf niet loskoppelen tenzij u ook Hallo VM verwijderen.

## <a name="find-hello-disk"></a>Hallo schijf gevonden
Voordat u kunt een schijf van een virtuele machine loskoppelen moet u toofind uit Hallo LUN-nummer een id voor Hallo schijf toobe losgekoppeld is. toodo die als volgt te werk:

1. Open Azure CLI en [tooyour Azure-abonnement verbinden](../articles/xplat-cli-connect.md). Zorg ervoor dat u zich in de modus voor Azure-servicebeheer (`azure config mode asm`) bevindt.
2. Ontdek welke schijven aangesloten tooyour VM zijn. Hallo volgende voorbeeld worden schijven voor virtuele machine met de naam Hallo `myVM`:

    ```azurecli
    azure vm disk list myVM
    ```

    Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld:

    ```azurecli
    * Fetching disk images
    * Getting virtual machines
    * Getting VM disks
      data:    Lun  Size(GB)  Blob-Name                         OS
      data:    ---  --------  --------------------------------  -----
      data:         30        ubuntuVM-2645b8030676c8f8.vhd  Linux
      data:    0    30        myDataDisk.vhd
      info:    vm disk list command OK
    ```

3. Houd er rekening mee Hallo LUN of Hallo **nummer van de logische eenheid** voor Hallo schijf die u toodetach wilt.

## <a name="remove-operating-system-references-toohello-disk"></a>Besturingssysteem verwijzingen toohello schijf verwijderen
Voordat de schijf wordt losgekoppeld Hallo van Hallo Linux Gast, moet u ervoor zorgen dat alle partities op schijf Hallo zich niet in gebruik. Zorg ervoor dat besturingssysteem Hallo probeert niet tooremount ze na opnieuw opstarten. Deze stappen ongedaan maken wanneer waarschijnlijk gemaakt Hallo-configuratie [koppelen](../articles/virtual-machines/linux/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) Hallo schijf.

1. Gebruik Hallo `lsscsi` opdracht toodiscover Hallo schijf-ID. U kunt `lsscsi` installeren met `yum install lsscsi` (Red Hat-distributies) of `apt-get install lsscsi` (Debian-distributies). U vindt Hallo schijf ID die u zoekt met behulp van Hallo LUN nummer. Hallo laatste nummer in de tuple Hallo in elke rij is Hallo LUN. In het Hallo-voorbeeld uit na `lsscsi`, LUN 0 toegewezen te  */dev/sdc*

    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```

2. Gebruik `fdisk -l <disk>` toodiscover Hallo partities die zijn gekoppeld aan Hallo schijf toobe losgekoppeld. Hallo volgende voorbeeld ziet u uitvoer Hallo voor `/dev/sdc`:

    ```bash
    Disk /dev/sdc: 1098.4 GB, 1098437885952 bytes, 2145386496 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk label type: dos
    Disk identifier: 0x5a1d2a1a
    
        Device Boot      Start         End      Blocks   Id  System
    /dev/sdc1            2048  2145386495  1072692224   83  Linux
    ```

3. Elke partitie die worden vermeld voor Hallo schijf ontkoppelen. Hallo volgende voorbeeld ontkoppelt `/dev/sdc1`:

    ```bash
    sudo umount /dev/sdc1
    ```

4. Gebruik Hallo `blkid` opdracht toodiscovery Hallo UUID's voor alle partities. Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld:

    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

5. Verwijder de vermeldingen in Hallo **/etc/fstab** bestand dat is gekoppeld met Hallo device-paden of UUID's voor alle partities voor Hallo schijf toobe losgekoppeld.  Vermeldingen voor dit voorbeeld kunnen zijn:

    ```sh  
   UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults   1   2
   ```

    of
   
   ```sh   
   /dev/sdc1   /datadrive   ext4   defaults   1   2
   ```

## <a name="detach-hello-disk"></a>Ontkoppel de schijf Hallo
Wanneer u Hallo LUN aantal Hallo schijf en verwijst naar verwijderde Hallo-besturingssysteem kunt vinden, bent u klaar toodetach het:

1. Loskoppelen van de geselecteerde schijf Hallo van Hallo virtuele machine met Hallo opdracht `azure vm disk detach
   <virtual-machine-name> <LUN>`. Hallo voorbeeld hieronder wordt LUN `0` van Hallo VM met de naam `myVM`:
   
    ```azurecli
    azure vm disk detach myVM 0
    ```

2. U kunt controleren als Hallo schijf is losgekoppeld door te voeren `azure vm disk list` opnieuw. Hallo voorbeeld controles Hallo VM met de naam `myVM`:
   
    ```azurecli
    azure vm disk list myVM
    ```

    Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld, waarin de gegevensschijf Hallo niet meer is gekoppeld:

    ```azurecli
    info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        ubuntuVM-2645b8030676c8f8.vhd  Linux
     info:    vm disk list command OK
    ```

Hallo losgekoppeld schijf blijft in de opslag, maar is niet langer gekoppelde tooa virtuele machine.

