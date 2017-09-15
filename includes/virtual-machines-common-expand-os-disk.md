## <a name="overview"></a><span data-ttu-id="4dcfa-101">Overzicht</span><span class="sxs-lookup"><span data-stu-id="4dcfa-101">Overview</span></span>
<span data-ttu-id="4dcfa-102">Wanneer u een nieuwe virtuele machine (VM) maakt in een resourcegroep door een installatiekopie van [Azure Marketplace](https://azure.microsoft.com/marketplace/) te implementeren, is het standaardstation voor het besturingssysteem 127 GB groot.</span><span class="sxs-lookup"><span data-stu-id="4dcfa-102">When you create a new virtual machine (VM) in a Resource Group by deploying an image from [Azure Marketplace](https://azure.microsoft.com/marketplace/), the default OS drive is 127 GB.</span></span> <span data-ttu-id="4dcfa-103">Hoewel het mogelijk is om gegevensschijven toe te voegen aan de VM (het aantal is afhankelijk van de SKU die u hebt gekozen) en het bovendien wordt aangeraden om toepassingen en CPU-intensieve werkbelastingen te installeren op deze aanvullende schijven, moeten klanten vaak ook de besturingssysteemschijf uitbreiden om bepaalde scenario's te ondersteunen, zoals de volgende:</span><span class="sxs-lookup"><span data-stu-id="4dcfa-103">Even though it’s possible to add data disks to the VM (how many depending upon the SKU you’ve chosen) and moreover it’s recommended to install applications and CPU intensive workloads on these addendum disks, oftentimes customers need to expand the OS drive to support certain scenarios such as following:</span></span>

1. <span data-ttu-id="4dcfa-104">Ondersteuning voor oudere toepassingen die onderdelen op de besturingssysteemschijf installeren.</span><span class="sxs-lookup"><span data-stu-id="4dcfa-104">Support legacy applications that install components on OS drive.</span></span>
2. <span data-ttu-id="4dcfa-105">Een fysieke computer of virtuele machine migreren van on-premises met een grotere besturingssysteemschijf.</span><span class="sxs-lookup"><span data-stu-id="4dcfa-105">Migrate a physical PC or virtual machine from on-premises with a larger OS drive.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4dcfa-106">In Azure zijn twee verschillende implementatiemodellen beschikbaar voor het maken van en werken met resources: Resource Manager en het klassieke model.</span><span class="sxs-lookup"><span data-stu-id="4dcfa-106">Azure has two different deployment models for creating and working with resources: Resource Manager and Classic.</span></span> <span data-ttu-id="4dcfa-107">In dit artikel wordt het Resource Manager-model beschreven.</span><span class="sxs-lookup"><span data-stu-id="4dcfa-107">This article covers using the Resource Manager model.</span></span> <span data-ttu-id="4dcfa-108">U doet er verstandig aan voor de meeste nieuwe implementaties het Resource Manager-model te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4dcfa-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>
> 
> 

## <a name="resize-the-os-drive"></a><span data-ttu-id="4dcfa-109">Besturingssysteemschijf uitbreiden</span><span class="sxs-lookup"><span data-stu-id="4dcfa-109">Resize the OS drive</span></span>
<span data-ttu-id="4dcfa-110">In dit artikel gaan we de grootte van de besturingssysteemschijf aanpassen met behulp van Resource Manager-modules van [Azure Powershell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="4dcfa-110">In this article we’ll accomplish the task of resizing the OS drive using resource manager modules of [Azure Powershell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="4dcfa-111">Open de Powershell ISE of het Powershell-venster in de beheerdersmodus en voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="4dcfa-111">Open your Powershell ISE or Powershell window in administrative mode and follow the steps below:</span></span>

1. <span data-ttu-id="4dcfa-112">Meld u in de modus voor resourcebeheer aan bij uw Microsoft Azure-account en selecteer uw abonnement als volgt:</span><span class="sxs-lookup"><span data-stu-id="4dcfa-112">Sign-in to your Microsoft Azure account in resource management mode and select your subscription as follows:</span></span>
   
   ```Powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription –SubscriptionName 'my-subscription-name'
   ```
2. <span data-ttu-id="4dcfa-113">Stel de naam van de resourcegroep en de VM als volgt in:</span><span class="sxs-lookup"><span data-stu-id="4dcfa-113">Set your resource group name and VM name as follows:</span></span>
   
   ```Powershell
   $rgName = 'my-resource-group-name'
   $vmName = 'my-vm-name'
   ```
3. <span data-ttu-id="4dcfa-114">Vraag als volgt een verwijzing op naar uw VM:</span><span class="sxs-lookup"><span data-stu-id="4dcfa-114">Obtain a reference to your VM as follows:</span></span>
   
   ```Powershell
   $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```
4. <span data-ttu-id="4dcfa-115">Ga als volgt te werk om de VM te stoppen voordat u de grootte van de schijf aanpast:</span><span class="sxs-lookup"><span data-stu-id="4dcfa-115">Stop the VM before resizing the disk as follows:</span></span>
   
    ```Powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    ```
5. <span data-ttu-id="4dcfa-116">En dan nu het moment waarop we allemaal gewacht hebben!</span><span class="sxs-lookup"><span data-stu-id="4dcfa-116">And here comes the moment we’ve been waiting for!</span></span> <span data-ttu-id="4dcfa-117">Stel de grootte van de besturingssysteemschijf in op de gewenste waarde en werk de VM als volgt bij:</span><span class="sxs-lookup"><span data-stu-id="4dcfa-117">Set the size of the OS disk to the desired value and update the VM as follows:</span></span>
   
   ```Powershell
   $vm.StorageProfile.OSDisk.DiskSizeGB = 1023
   Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
   ```
   
   > [!WARNING]
   > <span data-ttu-id="4dcfa-118">De nieuwe grootte moet groter zijn dan de bestaande schijfgrootte.</span><span class="sxs-lookup"><span data-stu-id="4dcfa-118">The new size should be greater than the existing disk size.</span></span> <span data-ttu-id="4dcfa-119">De toegestane maximale waarde is 1023 GB.</span><span class="sxs-lookup"><span data-stu-id="4dcfa-119">The maximum allowed is 1023 GB.</span></span>
   > 
   > 
6. <span data-ttu-id="4dcfa-120">Het bijwerken van de VM kan een paar seconden duren.</span><span class="sxs-lookup"><span data-stu-id="4dcfa-120">Updating the VM may take a few seconds.</span></span> <span data-ttu-id="4dcfa-121">Zodra de opdracht is voltooid, start u de VM als volgt opnieuw op:</span><span class="sxs-lookup"><span data-stu-id="4dcfa-121">Once the command finishes executing, restart the VM as follows:</span></span>
   
   ```Powershell
   Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```

<span data-ttu-id="4dcfa-122">Dat is alles.</span><span class="sxs-lookup"><span data-stu-id="4dcfa-122">And that’s it!</span></span> <span data-ttu-id="4dcfa-123">Ga nu met RDP naar de VM, open Computerbeheer (of Schijfbeheer) en vouw het station met de zojuist toegewezen ruimte uit.</span><span class="sxs-lookup"><span data-stu-id="4dcfa-123">Now RDP into the VM, open Computer Management (or Disk Management) and expand the drive using the newly allocated space.</span></span>

## <a name="summary"></a><span data-ttu-id="4dcfa-124">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="4dcfa-124">Summary</span></span>
<span data-ttu-id="4dcfa-125">In dit artikel hebben we Azure Resource Manager-modules van Powershell gebruikt om de besturingssysteemschijf van een virtuele IaaS-machine uit te breiden.</span><span class="sxs-lookup"><span data-stu-id="4dcfa-125">In this article, we used Azure Resource Manager modules of Powershell to expand the OS drive of an IaaS virtual machine.</span></span> <span data-ttu-id="4dcfa-126">Hieronder ziet u het volledige script ter referentie:</span><span class="sxs-lookup"><span data-stu-id="4dcfa-126">Reproduced below is the complete script for your reference:</span></span>

```Powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName 'my-subscription-name'
$rgName = 'my-resource-group-name'
$vmName = 'my-vm-name'
$vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
$vm.StorageProfile.OSDisk.DiskSizeGB = 1023
Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
```

## <a name="next-steps"></a><span data-ttu-id="4dcfa-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4dcfa-127">Next Steps</span></span>
<span data-ttu-id="4dcfa-128">Hoewel we in dit artikel voornamelijk hebben gekeken naar het uitbreiden van de besturingssysteemschijf van de VM, kan het script ook worden gebruikt voor het uitbreiden van de gegevensschijven die zijn gekoppeld aan de VM. Hiervoor hoeft maar één regel met code te worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="4dcfa-128">Though in this article, we focused primarily on expanding the OS disk of the VM, the developed script may also be used for expanding the data disks attached to the VM by changing a single line of code.</span></span> <span data-ttu-id="4dcfa-129">Als u bijvoorbeeld de eerste gegevensschijf die is gekoppeld aan de VM wilt uitbreiden, vervangt u het object ```OSDisk``` van ```StorageProfile``` door de matrix ```DataDisks``` en gebruikt u een numerieke index om een verwijzing naar de eerste gekoppelde schijf te verkrijgen, zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="4dcfa-129">For example, to expand the first data disk attached to the VM, replace the ```OSDisk``` object of ```StorageProfile``` with ```DataDisks``` array and use a numeric index to obtain a reference to first attached data disk, as shown below:</span></span>

```Powershell
$vm.StorageProfile.DataDisks[0].DiskSizeGB = 1023
```
<span data-ttu-id="4dcfa-130">Op dezelfde manier kunt u verwijzen naar andere gegevensschijven die aan de VM zijn gekoppeld. Dit kan met behulp van een index, zoals hierboven, of met de eigenschap ```Name``` van de schijf, zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="4dcfa-130">Similarly you may reference other data disks attached to the VM, either by using an index as shown above or the ```Name``` property of the disk as illustrated below:</span></span>

```Powershell
($vm.StorageProfile.DataDisks | Where {$_.Name -eq 'my-second-data-disk'})[0].DiskSizeGB = 1023
```

<span data-ttu-id="4dcfa-131">Als u wilt weten hoe u schijven koppelt aan een Azure Resource Manager-VM, raadpleegt u dit [artikel](../articles/virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4dcfa-131">If you want to find out how to attach disks to an Azure Resource Manager VM, check this [article](../articles/virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

