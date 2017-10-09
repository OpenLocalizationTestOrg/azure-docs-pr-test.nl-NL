
<span data-ttu-id="10af1-101">Zie [About Disks and VHDs for Virtual Machines](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Informatie over schijven en VHD's voor virtuele machines) voor meer informatie over schijven.</span><span class="sxs-lookup"><span data-stu-id="10af1-101">For more information about disks, see [About Disks and VHDs for Virtual Machines](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<a id="attachempty"></a>

## <a name="attach-an-empty-disk"></a><span data-ttu-id="10af1-102">Een lege schijf koppelen</span><span class="sxs-lookup"><span data-stu-id="10af1-102">Attach an empty disk</span></span>
1. <span data-ttu-id="10af1-103">Open Azure CLI 1.0 en [tooyour Azure-abonnement verbinden](../articles/xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="10af1-103">Open Azure CLI 1.0 and [connect tooyour Azure subscription](../articles/xplat-cli-connect.md).</span></span> <span data-ttu-id="10af1-104">Zorg ervoor dat u zich in de modus voor Azure-servicebeheer (`azure config mode asm`) bevindt.</span><span class="sxs-lookup"><span data-stu-id="10af1-104">Make sure you are in Azure Service Management mode (`azure config mode asm`).</span></span>
2. <span data-ttu-id="10af1-105">Voer `azure vm disk attach-new` toocreate en het koppelen van een nieuwe schijf, zoals wordt weergegeven in het volgende voorbeeld Hallo.</span><span class="sxs-lookup"><span data-stu-id="10af1-105">Enter `azure vm disk attach-new` toocreate and attach a new disk as shown in hello following example.</span></span> <span data-ttu-id="10af1-106">Vervang *myVM* met Hallo-naam van uw virtuele Linux-Machine en Hallo grootte van Hallo schijf opgeven in GB, namelijk *100GB* in dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="10af1-106">Replace *myVM* with hello name of your Linux Virtual Machine and specify hello size of hello disk in GB, which is *100GB* in this example:</span></span>

    ```azurecli
    azure vm disk attach-new myVM 100
    ```

3. <span data-ttu-id="10af1-107">Nadat de gegevensschijf Hallo is gemaakt en gekoppeld, wordt vermeld in de uitvoer Hallo van `azure vm disk list <virtual-machine-name>` zoals weergegeven in Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="10af1-107">After hello data disk is created and attached, it's listed in hello output of `azure vm disk list <virtual-machine-name>` as shown in hello following example:</span></span>
   
    ```azurecli
    azure vm disk list TestVM
    ```

    <span data-ttu-id="10af1-108">Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="10af1-108">hello output is similar toohello following example:</span></span>

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

## <a name="attach-an-existing-disk"></a><span data-ttu-id="10af1-109">Een bestaande schijf koppelen</span><span class="sxs-lookup"><span data-stu-id="10af1-109">Attach an existing disk</span></span>
<span data-ttu-id="10af1-110">Als u een bestaande schijf wilt koppelen, dient u een .vhd beschikbaar te hebben in een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="10af1-110">Attaching an existing disk requires that you have a .vhd available in a storage account.</span></span>

1. <span data-ttu-id="10af1-111">Open Azure CLI 1.0 en [tooyour Azure-abonnement verbinden](../articles/xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="10af1-111">Open Azure CLI 1.0 and [connect tooyour Azure subscription](../articles/xplat-cli-connect.md).</span></span> <span data-ttu-id="10af1-112">Zorg ervoor dat u zich in de modus voor Azure-servicebeheer (`azure config mode asm`) bevindt.</span><span class="sxs-lookup"><span data-stu-id="10af1-112">Make sure you are in Azure Service Management mode (`azure config mode asm`).</span></span>
2. <span data-ttu-id="10af1-113">Controleer als Hallo VHD die u wilt dat tooattach is al geüpload tooyour Azure-abonnement:</span><span class="sxs-lookup"><span data-stu-id="10af1-113">Check if hello VHD you want tooattach is already uploaded tooyour Azure subscription:</span></span>
   
    ```azurecli
    azure vm disk list
    ```

    <span data-ttu-id="10af1-114">Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="10af1-114">hello output is similar toohello following example:</span></span>

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

3. <span data-ttu-id="10af1-115">Als u niet kunt Hallo schijf vinden die u toouse, u mogelijk een abonnement op lokale tooyour VHD uploaden via `azure vm disk create` of `azure vm disk upload`.</span><span class="sxs-lookup"><span data-stu-id="10af1-115">If you don't find hello disk that you want toouse, you may upload a local VHD tooyour subscription by using `azure vm disk create` or `azure vm disk upload`.</span></span> <span data-ttu-id="10af1-116">Een voorbeeld van `disk create` zou zijn als volgt Hallo in:</span><span class="sxs-lookup"><span data-stu-id="10af1-116">An example of `disk create` would be as in hello following example:</span></span>
   
    ```azurecli
    azure vm disk create myVhd .\TempDisk\test.VHD -l "East US" -o Linux
    ```

    <span data-ttu-id="10af1-117">Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="10af1-117">hello output is similar toohello following example:</span></span>

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
   
   <span data-ttu-id="10af1-118">U kunt ook `azure vm disk upload` tooupload een VHD tooa specifieke storage-account.</span><span class="sxs-lookup"><span data-stu-id="10af1-118">You may also use `azure vm disk upload` tooupload a VHD tooa specific storage account.</span></span> <span data-ttu-id="10af1-119">Lees meer over Hallo toomanage opdrachten de gegevensschijven van de virtuele machine van Azure [hier](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="10af1-119">Read more about hello commands toomanage your Azure virtual machine data disks [over here](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

4. <span data-ttu-id="10af1-120">Nu u een koppeling gewenst Hallo VHD tooyour virtuele machine:</span><span class="sxs-lookup"><span data-stu-id="10af1-120">Now you attach hello desired VHD tooyour virtual machine:</span></span>
   
    ```azurecli
    azure vm disk attach myVM myVhd
    ```
   
   <span data-ttu-id="10af1-121">Zorg ervoor dat tooreplace *myVM* met de naam van uw virtuele machine Hallo en *myVHD* met de gewenste VHD.</span><span class="sxs-lookup"><span data-stu-id="10af1-121">Make sure tooreplace *myVM* with hello name of your virtual machine, and *myVHD* with your desired VHD.</span></span>

5. <span data-ttu-id="10af1-122">U kunt controleren of Hallo schijf gekoppelde toohello virtuele machine met `azure vm disk list <virtual-machine-name>`:</span><span class="sxs-lookup"><span data-stu-id="10af1-122">You can verify hello disk is attached toohello virtual machine with `azure vm disk list <virtual-machine-name>`:</span></span>
   
    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="10af1-123">Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="10af1-123">hello output is similar toohello following example:</span></span>

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
> <span data-ttu-id="10af1-124">Nadat u een gegevensschijf toevoegt, hebt u nodig hebt toolog op toohello virtuele machine en Hallo schijf initialiseren zodat Hallo virtuele machine Hallo schijf voor opslag kunnen gebruiken (Zie volgende Hallo stappen voor meer informatie over hoe toodo Hallo schijf initialiseren).</span><span class="sxs-lookup"><span data-stu-id="10af1-124">After you add a data disk, you'll need toolog on toohello virtual machine and initialize hello disk so hello virtual machine can use hello disk for storage (see hello following steps for more information on how toodo initialize hello disk).</span></span>
> 
> 

