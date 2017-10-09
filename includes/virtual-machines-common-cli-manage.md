<span data-ttu-id="38d4c-101">Hello Azure CLI 2.0 kunt u toocreate en beheren van uw Azure-resources op Mac OS-, Linux- en Windows.</span><span class="sxs-lookup"><span data-stu-id="38d4c-101">hello Azure CLI 2.0 allows you toocreate and manage your Azure resources on macOS, Linux, and Windows.</span></span> <span data-ttu-id="38d4c-102">Dit artikel vindt u details van de meest voorkomende opdrachten toocreate hello en beheren van virtuele machines (VM's).</span><span class="sxs-lookup"><span data-stu-id="38d4c-102">This article details some of hello most common commands toocreate and manage virtual machines (VMs).</span></span>

<span data-ttu-id="38d4c-103">In dit artikel vereist hello Azure CLI versie 2.0.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="38d4c-103">This article requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="38d4c-104">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="38d4c-104">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="38d4c-105">Als u tooupgrade moet, Zie [2.0 voor Azure CLI installeren](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="38d4c-105">If you need tooupgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="38d4c-106">U kunt ook [Cloud Shell](/azure/cloud-shell/quickstart) vanuit de browser.</span><span class="sxs-lookup"><span data-stu-id="38d4c-106">You can also use [Cloud Shell](/azure/cloud-shell/quickstart) from your browser.</span></span>

## <a name="basic-azure-resource-manager-commands-in-azure-cli"></a><span data-ttu-id="38d4c-107">Basisopdrachten van Azure Resource Manager in Azure CLI</span><span class="sxs-lookup"><span data-stu-id="38d4c-107">Basic Azure Resource Manager commands in Azure CLI</span></span>
<span data-ttu-id="38d4c-108">Voor meer hulp bij specifieke opdrachtregelopties en opties, kunt u opties en Hallo opdracht online help door te typen `az <command> <subcommand> --help`.</span><span class="sxs-lookup"><span data-stu-id="38d4c-108">For more detailed help with specific command line switches and options, you can use hello online command help and options by typing `az <command> <subcommand> --help`.</span></span>

### <a name="create-vms"></a><span data-ttu-id="38d4c-109">Virtuele machines maken</span><span class="sxs-lookup"><span data-stu-id="38d4c-109">Create VMs</span></span>
| <span data-ttu-id="38d4c-110">Taak</span><span class="sxs-lookup"><span data-stu-id="38d4c-110">Task</span></span> | <span data-ttu-id="38d4c-111">Azure CLI-opdrachten</span><span class="sxs-lookup"><span data-stu-id="38d4c-111">Azure CLI commands</span></span> |
| --- | --- |
| <span data-ttu-id="38d4c-112">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="38d4c-112">Create a resource group</span></span> | `az group create --name myResourceGroup --location eastus` |
| <span data-ttu-id="38d4c-113">Een Linux-VM maken</span><span class="sxs-lookup"><span data-stu-id="38d4c-113">Create a Linux VM</span></span> | `az vm create --resource-group myResourceGroup --name myVM --image ubuntults` |
| <span data-ttu-id="38d4c-114">Een Windows-VM maken</span><span class="sxs-lookup"><span data-stu-id="38d4c-114">Create a Windows VM</span></span> | `az vm create --resource-group myResourceGroup --name myVM --image win2016datacenter` |

### <a name="manage-vm-state"></a><span data-ttu-id="38d4c-115">Status virtuele machine beheren</span><span class="sxs-lookup"><span data-stu-id="38d4c-115">Manage VM state</span></span>
| <span data-ttu-id="38d4c-116">Taak</span><span class="sxs-lookup"><span data-stu-id="38d4c-116">Task</span></span> | <span data-ttu-id="38d4c-117">Azure CLI-opdrachten</span><span class="sxs-lookup"><span data-stu-id="38d4c-117">Azure CLI commands</span></span> |
| --- | --- |
| <span data-ttu-id="38d4c-118">Een VM starten</span><span class="sxs-lookup"><span data-stu-id="38d4c-118">Start a VM</span></span> | `az vm start --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="38d4c-119">Een VM stoppen</span><span class="sxs-lookup"><span data-stu-id="38d4c-119">Stop a VM</span></span> | `az vm stop --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="38d4c-120">De toewijzing van een VM ongedaan maken</span><span class="sxs-lookup"><span data-stu-id="38d4c-120">Deallocate a VM</span></span> | `az vm deallocate --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="38d4c-121">Een VM opnieuw opstarten</span><span class="sxs-lookup"><span data-stu-id="38d4c-121">Restart a VM</span></span> | `az vm restart --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="38d4c-122">Een virtuele machine opnieuw implementeren</span><span class="sxs-lookup"><span data-stu-id="38d4c-122">Redeploy a VM</span></span> | `az vm redeploy --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="38d4c-123">Een VM verwijderen</span><span class="sxs-lookup"><span data-stu-id="38d4c-123">Delete a VM</span></span> | `az vm delete --resource-group myResourceGroup --name myVM` |

### <a name="get-vm-info"></a><span data-ttu-id="38d4c-124">VM-info ophalen</span><span class="sxs-lookup"><span data-stu-id="38d4c-124">Get VM info</span></span>
| <span data-ttu-id="38d4c-125">Taak</span><span class="sxs-lookup"><span data-stu-id="38d4c-125">Task</span></span> | <span data-ttu-id="38d4c-126">Azure CLI-opdrachten</span><span class="sxs-lookup"><span data-stu-id="38d4c-126">Azure CLI commands</span></span> |
| --- | --- |
| <span data-ttu-id="38d4c-127">Lijst met VM's opvragen</span><span class="sxs-lookup"><span data-stu-id="38d4c-127">List VMs</span></span> | `az vm list` |
| <span data-ttu-id="38d4c-128">Informatie over een VM ophalen</span><span class="sxs-lookup"><span data-stu-id="38d4c-128">Get information about a VM</span></span> | `az vm show --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="38d4c-129">Verbruik van VM-resources opvragen</span><span class="sxs-lookup"><span data-stu-id="38d4c-129">Get usage of VM resources</span></span> | `az vm list-usage --location eastus` |
| <span data-ttu-id="38d4c-130">Alle beschikbare VM-grootten opvragen</span><span class="sxs-lookup"><span data-stu-id="38d4c-130">Get all available VM sizes</span></span> | `az vm list-sizes --location eastus` |

## <a name="disks-and-images"></a><span data-ttu-id="38d4c-131">Schijven en installatiekopieën</span><span class="sxs-lookup"><span data-stu-id="38d4c-131">Disks and images</span></span>
| <span data-ttu-id="38d4c-132">Taak</span><span class="sxs-lookup"><span data-stu-id="38d4c-132">Task</span></span> | <span data-ttu-id="38d4c-133">Azure CLI-opdrachten</span><span class="sxs-lookup"><span data-stu-id="38d4c-133">Azure CLI commands</span></span> |
| --- | --- |
| <span data-ttu-id="38d4c-134">Toevoegen van een data schijf tooa VM</span><span class="sxs-lookup"><span data-stu-id="38d4c-134">Add a data disk tooa VM</span></span> | `az vm disk attach --resource-group myResourceGroup --vm-name myVM --disk myDataDisk --size-gb 128 --new ` |
| <span data-ttu-id="38d4c-135">Een gegevensschijf verwijderen van een VM</span><span class="sxs-lookup"><span data-stu-id="38d4c-135">Remove a data disk from a VM</span></span> | `az vm disk detach --resource-group myResourceGroup --vm-name myVM --disk myDataDisk` |
| <span data-ttu-id="38d4c-136">De grootte van een schijf wijzigen</span><span class="sxs-lookup"><span data-stu-id="38d4c-136">Resize a disk</span></span> | `az disk update --resource-group myResourceGroup --name myDataDisk --size-gb 256` |
| <span data-ttu-id="38d4c-137">Een momentopname maken van een schijf</span><span class="sxs-lookup"><span data-stu-id="38d4c-137">Snapshot a disk</span></span> | `az snapshot create --resource-group myResourceGroup --name mySnapshot --source myDataDisk` |
| <span data-ttu-id="38d4c-138">Afbeelding van een virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="38d4c-138">Create image of a VM</span></span> | `az image create --resource-group myResourceGroup --source myVM --name myImage` |
| <span data-ttu-id="38d4c-139">Virtuele machine van de installatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="38d4c-139">Create VM from image</span></span> | `az vm create --resource-group myResourceGroup --name myNewVM --image myImage` |


## <a name="next-steps"></a><span data-ttu-id="38d4c-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="38d4c-140">Next steps</span></span>
<span data-ttu-id="38d4c-141">Zie voor meer voorbeelden van de CLI-opdrachten Hallo Hallo [maken en beheren van virtuele Linux-machines Hello Azure CLI](../articles/virtual-machines/linux/tutorial-manage-vm.md) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="38d4c-141">For additional examples of hello CLI commands, see hello [Create and Manage Linux VMs with hello Azure CLI](../articles/virtual-machines/linux/tutorial-manage-vm.md) tutorial.</span></span>

