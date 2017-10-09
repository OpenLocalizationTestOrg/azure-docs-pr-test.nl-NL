<span data-ttu-id="37e8e-101">Wanneer u een gegevensschijf die is aangesloten tooa virtuele machine (VM) niet meer nodig hebt, kunt u deze eenvoudig loskoppelen.</span><span class="sxs-lookup"><span data-stu-id="37e8e-101">When you no longer need a data disk that's attached tooa virtual machine (VM), you can easily detach it.</span></span> <span data-ttu-id="37e8e-102">Wanneer u een schijf van Hallo VM losgekoppeld, Hallo schijf is niet verwijderd uit de opslag.</span><span class="sxs-lookup"><span data-stu-id="37e8e-102">When you detach a disk from hello VM, hello disk is not removed it from storage.</span></span> <span data-ttu-id="37e8e-103">Als u toouse Hallo bestaande gegevens op Hallo schijf opnieuw wilt, u kunt opnieuw het toohello dezelfde virtuele machine of een andere naam.</span><span class="sxs-lookup"><span data-stu-id="37e8e-103">If you want toouse hello existing data on hello disk again, you can reattach it toohello same VM, or another one.</span></span>  

> [!NOTE]
> <span data-ttu-id="37e8e-104">Een VM in Azure gebruikt verschillende soorten schijven: een besturingssysteemschijf, een lokale tijdelijke schijf en optionele gegevensschijven.</span><span class="sxs-lookup"><span data-stu-id="37e8e-104">A VM in Azure uses different types of disks - an operating system disk, a local temporary disk, and optional data disks.</span></span> <span data-ttu-id="37e8e-105">Zie [Informatie over schijven en VHD's voor virtuele machines](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="37e8e-105">For details, see [About Disks and VHDs for Virtual Machines](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="37e8e-106">U kan een schijf niet loskoppelen tenzij u ook Hallo VM verwijderen.</span><span class="sxs-lookup"><span data-stu-id="37e8e-106">You cannot detach an operating system disk unless you also delete hello VM.</span></span>

## <a name="find-hello-disk"></a><span data-ttu-id="37e8e-107">Hallo schijf gevonden</span><span class="sxs-lookup"><span data-stu-id="37e8e-107">Find hello disk</span></span>
<span data-ttu-id="37e8e-108">Voordat u kunt een schijf van een virtuele machine loskoppelen moet u toofind uit Hallo LUN-nummer een id voor Hallo schijf toobe losgekoppeld is.</span><span class="sxs-lookup"><span data-stu-id="37e8e-108">Before you can detach a disk from a VM you need toofind out hello LUN number, which is an identifier for hello disk toobe detached.</span></span> <span data-ttu-id="37e8e-109">toodo die als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="37e8e-109">toodo that, follow these steps:</span></span>

1. <span data-ttu-id="37e8e-110">Open Azure CLI en [tooyour Azure-abonnement verbinden](../articles/xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="37e8e-110">Open Azure CLI and [connect tooyour Azure subscription](../articles/xplat-cli-connect.md).</span></span> <span data-ttu-id="37e8e-111">Zorg ervoor dat u zich in de modus voor Azure-servicebeheer (`azure config mode asm`) bevindt.</span><span class="sxs-lookup"><span data-stu-id="37e8e-111">Make sure you are in Azure Service Management mode (`azure config mode asm`).</span></span>
2. <span data-ttu-id="37e8e-112">Ontdek welke schijven aangesloten tooyour VM zijn.</span><span class="sxs-lookup"><span data-stu-id="37e8e-112">Find out which disks are attached tooyour VM.</span></span> <span data-ttu-id="37e8e-113">Hallo volgende voorbeeld worden schijven voor virtuele machine met de naam Hallo `myVM`:</span><span class="sxs-lookup"><span data-stu-id="37e8e-113">hello following example lists disks for hello VM named `myVM`:</span></span>

    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="37e8e-114">Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="37e8e-114">hello output is similar toohello following example:</span></span>

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

3. <span data-ttu-id="37e8e-115">Houd er rekening mee Hallo LUN of Hallo **nummer van de logische eenheid** voor Hallo schijf die u toodetach wilt.</span><span class="sxs-lookup"><span data-stu-id="37e8e-115">Note hello LUN or hello **logical unit number** for hello disk that you want toodetach.</span></span>

## <a name="remove-operating-system-references-toohello-disk"></a><span data-ttu-id="37e8e-116">Besturingssysteem verwijzingen toohello schijf verwijderen</span><span class="sxs-lookup"><span data-stu-id="37e8e-116">Remove operating system references toohello disk</span></span>
<span data-ttu-id="37e8e-117">Voordat de schijf wordt losgekoppeld Hallo van Hallo Linux Gast, moet u ervoor zorgen dat alle partities op schijf Hallo zich niet in gebruik.</span><span class="sxs-lookup"><span data-stu-id="37e8e-117">Before detaching hello disk from hello Linux guest, you should make sure that all partitions on hello disk are not in use.</span></span> <span data-ttu-id="37e8e-118">Zorg ervoor dat besturingssysteem Hallo probeert niet tooremount ze na opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="37e8e-118">Ensure that hello operating system does not attempt tooremount them after a reboot.</span></span> <span data-ttu-id="37e8e-119">Deze stappen ongedaan maken wanneer waarschijnlijk gemaakt Hallo-configuratie [koppelen](../articles/virtual-machines/linux/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) Hallo schijf.</span><span class="sxs-lookup"><span data-stu-id="37e8e-119">These steps undo hello configuration you likely created when [attaching](../articles/virtual-machines/linux/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) hello disk.</span></span>

1. <span data-ttu-id="37e8e-120">Gebruik Hallo `lsscsi` opdracht toodiscover Hallo schijf-ID.</span><span class="sxs-lookup"><span data-stu-id="37e8e-120">Use hello `lsscsi` command toodiscover hello disk identifier.</span></span> <span data-ttu-id="37e8e-121">U kunt `lsscsi` installeren met `yum install lsscsi` (Red Hat-distributies) of `apt-get install lsscsi` (Debian-distributies).</span><span class="sxs-lookup"><span data-stu-id="37e8e-121">`lsscsi` can be installed by either `yum install lsscsi` (on Red Hat based distributions) or `apt-get install lsscsi` (on Debian based distributions).</span></span> <span data-ttu-id="37e8e-122">U vindt Hallo schijf ID die u zoekt met behulp van Hallo LUN nummer.</span><span class="sxs-lookup"><span data-stu-id="37e8e-122">You can find hello disk identifier you are looking for by using hello LUN number.</span></span> <span data-ttu-id="37e8e-123">Hallo laatste nummer in de tuple Hallo in elke rij is Hallo LUN.</span><span class="sxs-lookup"><span data-stu-id="37e8e-123">hello last number in hello tuple in each row is hello LUN.</span></span> <span data-ttu-id="37e8e-124">In het Hallo-voorbeeld uit na `lsscsi`, LUN 0 toegewezen te  */dev/sdc*</span><span class="sxs-lookup"><span data-stu-id="37e8e-124">In hello following example from `lsscsi`, LUN 0 maps too*/dev/sdc*</span></span>

    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```

2. <span data-ttu-id="37e8e-125">Gebruik `fdisk -l <disk>` toodiscover Hallo partities die zijn gekoppeld aan Hallo schijf toobe losgekoppeld.</span><span class="sxs-lookup"><span data-stu-id="37e8e-125">Use `fdisk -l <disk>` toodiscover hello partitions associated with hello disk toobe detached.</span></span> <span data-ttu-id="37e8e-126">Hallo volgende voorbeeld ziet u uitvoer Hallo voor `/dev/sdc`:</span><span class="sxs-lookup"><span data-stu-id="37e8e-126">hello following example shows hello output for `/dev/sdc`:</span></span>

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

3. <span data-ttu-id="37e8e-127">Elke partitie die worden vermeld voor Hallo schijf ontkoppelen.</span><span class="sxs-lookup"><span data-stu-id="37e8e-127">Unmount each partition listed for hello disk.</span></span> <span data-ttu-id="37e8e-128">Hallo volgende voorbeeld ontkoppelt `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="37e8e-128">hello following example unmounts `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

4. <span data-ttu-id="37e8e-129">Gebruik Hallo `blkid` opdracht toodiscovery Hallo UUID's voor alle partities.</span><span class="sxs-lookup"><span data-stu-id="37e8e-129">Use hello `blkid` command toodiscovery hello UUIDs for all partitions.</span></span> <span data-ttu-id="37e8e-130">Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="37e8e-130">hello output is similar toohello following example:</span></span>

    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

5. <span data-ttu-id="37e8e-131">Verwijder de vermeldingen in Hallo **/etc/fstab** bestand dat is gekoppeld met Hallo device-paden of UUID's voor alle partities voor Hallo schijf toobe losgekoppeld.</span><span class="sxs-lookup"><span data-stu-id="37e8e-131">Remove entries in hello **/etc/fstab** file associated with either hello device paths or UUIDs for all partitions for hello disk toobe detached.</span></span>  <span data-ttu-id="37e8e-132">Vermeldingen voor dit voorbeeld kunnen zijn:</span><span class="sxs-lookup"><span data-stu-id="37e8e-132">Entries for this example might be:</span></span>

    ```sh  
   UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults   1   2
   ```

    <span data-ttu-id="37e8e-133">of</span><span class="sxs-lookup"><span data-stu-id="37e8e-133">or</span></span>
   
   ```sh   
   /dev/sdc1   /datadrive   ext4   defaults   1   2
   ```

## <a name="detach-hello-disk"></a><span data-ttu-id="37e8e-134">Ontkoppel de schijf Hallo</span><span class="sxs-lookup"><span data-stu-id="37e8e-134">Detach hello disk</span></span>
<span data-ttu-id="37e8e-135">Wanneer u Hallo LUN aantal Hallo schijf en verwijst naar verwijderde Hallo-besturingssysteem kunt vinden, bent u klaar toodetach het:</span><span class="sxs-lookup"><span data-stu-id="37e8e-135">After you find hello LUN number of hello disk and removed hello operating system references, you're ready toodetach it:</span></span>

1. <span data-ttu-id="37e8e-136">Loskoppelen van de geselecteerde schijf Hallo van Hallo virtuele machine met Hallo opdracht `azure vm disk detach
   <virtual-machine-name> <LUN>`.</span><span class="sxs-lookup"><span data-stu-id="37e8e-136">Detach hello selected disk from hello virtual machine by running hello command `azure vm disk detach
<virtual-machine-name> <LUN>`.</span></span> <span data-ttu-id="37e8e-137">Hallo voorbeeld hieronder wordt LUN `0` van Hallo VM met de naam `myVM`:</span><span class="sxs-lookup"><span data-stu-id="37e8e-137">hello following example detaches LUN `0` from hello VM named `myVM`:</span></span>
   
    ```azurecli
    azure vm disk detach myVM 0
    ```

2. <span data-ttu-id="37e8e-138">U kunt controleren als Hallo schijf is losgekoppeld door te voeren `azure vm disk list` opnieuw.</span><span class="sxs-lookup"><span data-stu-id="37e8e-138">You can check if hello disk got detached by running `azure vm disk list` again.</span></span> <span data-ttu-id="37e8e-139">Hallo voorbeeld controles Hallo VM met de naam `myVM`:</span><span class="sxs-lookup"><span data-stu-id="37e8e-139">hello following example checks hello VM named `myVM`:</span></span>
   
    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="37e8e-140">Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld, waarin de gegevensschijf Hallo niet meer is gekoppeld:</span><span class="sxs-lookup"><span data-stu-id="37e8e-140">hello output is similar toohello following example, which shows hello data disk is no longer attached:</span></span>

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

<span data-ttu-id="37e8e-141">Hallo losgekoppeld schijf blijft in de opslag, maar is niet langer gekoppelde tooa virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="37e8e-141">hello detached disk remains in storage but is no longer attached tooa virtual machine.</span></span>

