
Zie [About Disks and VHDs for Virtual Machines](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Informatie over schijven en VHD's voor virtuele machines) voor meer informatie over schijven.

<a id="attachempty"></a>

## <a name="attach-an-empty-disk"></a>Een lege schijf koppelen
1. Open Azure CLI 1.0 en [tooyour Azure-abonnement verbinden](../articles/xplat-cli-connect.md). Zorg ervoor dat u zich in de modus voor Azure-servicebeheer (`azure config mode asm`) bevindt.
2. Voer `azure vm disk attach-new` toocreate en het koppelen van een nieuwe schijf, zoals wordt weergegeven in het volgende voorbeeld Hallo. Vervang *myVM* met Hallo-naam van uw virtuele Linux-Machine en Hallo grootte van Hallo schijf opgeven in GB, namelijk *100GB* in dit voorbeeld:

    ```azurecli
    azure vm disk attach-new myVM 100
    ```

3. Nadat de gegevensschijf Hallo is gemaakt en gekoppeld, wordt vermeld in de uitvoer Hallo van `azure vm disk list <virtual-machine-name>` zoals weergegeven in Hallo voorbeeld te volgen:
   
    ```azurecli
    azure vm disk list TestVM
    ```

    Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld:

    ```bash
    info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        myVM-2645b8030676c8f8.vhd  Linux
     data:    0    100       myVM-76f7ee1ef0f6dddc.vhd
     info:    vm disk list command OK
    ```

<a id="attachexisting"></a>

## <a name="attach-an-existing-disk"></a>Een bestaande schijf koppelen
Als u een bestaande schijf wilt koppelen, dient u een .vhd beschikbaar te hebben in een opslagaccount.

1. Open Azure CLI 1.0 en [tooyour Azure-abonnement verbinden](../articles/xplat-cli-connect.md). Zorg ervoor dat u zich in de modus voor Azure-servicebeheer (`azure config mode asm`) bevindt.
2. Controleer als Hallo VHD die u wilt dat tooattach is al geüpload tooyour Azure-abonnement:
   
    ```azurecli
    azure vm disk list
    ```

    Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld:

    ```azurecli
     info:    Executing command vm disk list
   
   * Fetching disk images
     data:    Name                                          OS
     data:    --------------------------------------------  -----
     data:    myTestVhd                                     Linux
     data:    TestVM-ubuntuVMasm-0-201508060029150744  Linux
     data:    TestVM-ubuntuVMasm-0-201508060040530369
     info:    vm disk list command OK
    ```

3. Als u niet kunt Hallo schijf vinden die u toouse, u mogelijk een abonnement op lokale tooyour VHD uploaden via `azure vm disk create` of `azure vm disk upload`. Een voorbeeld van `disk create` zou zijn als volgt Hallo in:
   
    ```azurecli
    azure vm disk create myVhd .\TempDisk\test.VHD -l "East US" -o Linux
    ```

    Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld:

    ```azurecli
    info:    Executing command vm disk create
    + Retrieving storage accounts
    info:    VHD size : 10 GB
    info:    Uploading 10485760.5 KB
    Requested:100.0% Completed:100.0% Running:   0 Time:   25s Speed:    82 KB/s
    info:    Finishing computing MD5 hash, 16% is complete.
    info:    https://mystorageaccount.blob.core.windows.net/disks/myVHD.vhd was
    uploaded successfully
    info:    vm disk create command OK
    ```
   
   U kunt ook `azure vm disk upload` tooupload een VHD tooa specifieke storage-account. Lees meer over Hallo toomanage opdrachten de gegevensschijven van de virtuele machine van Azure [hier](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).

4. Nu u een koppeling gewenst Hallo VHD tooyour virtuele machine:
   
    ```azurecli
    azure vm disk attach myVM myVhd
    ```
   
   Zorg ervoor dat tooreplace *myVM* met de naam van uw virtuele machine Hallo en *myVHD* met de gewenste VHD.

5. U kunt controleren of Hallo schijf gekoppelde toohello virtuele machine met `azure vm disk list <virtual-machine-name>`:
   
    ```azurecli
    azure vm disk list myVM
    ```

    Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld:

    ```azurecli
     info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        TestVM-2645b8030676c8f8.vhd  Linux
     data:    1    10        test.VHD
     data:    0    100        TestVM-76f7ee1ef0f6dddc.vhd
     info:    vm disk list command OK
    ```

> [!NOTE]
> Nadat u een gegevensschijf toevoegt, hebt u nodig hebt toolog op toohello virtuele machine en Hallo schijf initialiseren zodat Hallo virtuele machine Hallo schijf voor opslag kunnen gebruiken (Zie volgende Hallo stappen voor meer informatie over hoe toodo Hallo schijf initialiseren).
> 
> 

