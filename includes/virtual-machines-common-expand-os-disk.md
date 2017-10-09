## <a name="overview"></a><span data-ttu-id="e57cb-101">Overzicht</span><span class="sxs-lookup"><span data-stu-id="e57cb-101">Overview</span></span>
<span data-ttu-id="e57cb-102">Wanneer u een nieuwe virtuele machine (VM) maakt in een resourcegroep met de implementatie van een installatiekopie van [Azure Marketplace](https://azure.microsoft.com/marketplace/), Hallo standaard OS station is 127 GB.</span><span class="sxs-lookup"><span data-stu-id="e57cb-102">When you create a new virtual machine (VM) in a Resource Group by deploying an image from [Azure Marketplace](https://azure.microsoft.com/marketplace/), hello default OS drive is 127 GB.</span></span> <span data-ttu-id="e57cb-103">Hoewel het mogelijk tooadd gegevens schijven toohello VM (hoeveel, al naar gelang Hallo SKU u hebt gekozen) is en bovendien is het aanbevolen tooinstall toepassingen en werkbelastingen met een intensieve CPU op deze schijven addendum, moeten vaak ook klanten tooexpand Hallo OS station toosupport bepaalde scenario's zoals het volgende:</span><span class="sxs-lookup"><span data-stu-id="e57cb-103">Even though it’s possible tooadd data disks toohello VM (how many depending upon hello SKU you’ve chosen) and moreover it’s recommended tooinstall applications and CPU intensive workloads on these addendum disks, oftentimes customers need tooexpand hello OS drive toosupport certain scenarios such as following:</span></span>

1. <span data-ttu-id="e57cb-104">Ondersteuning voor oudere toepassingen die onderdelen op de besturingssysteemschijf installeren.</span><span class="sxs-lookup"><span data-stu-id="e57cb-104">Support legacy applications that install components on OS drive.</span></span>
2. <span data-ttu-id="e57cb-105">Een fysieke computer of virtuele machine migreren van on-premises met een grotere besturingssysteemschijf.</span><span class="sxs-lookup"><span data-stu-id="e57cb-105">Migrate a physical PC or virtual machine from on-premises with a larger OS drive.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e57cb-106">In Azure zijn twee verschillende implementatiemodellen beschikbaar voor het maken van en werken met resources: Resource Manager en het klassieke model.</span><span class="sxs-lookup"><span data-stu-id="e57cb-106">Azure has two different deployment models for creating and working with resources: Resource Manager and Classic.</span></span> <span data-ttu-id="e57cb-107">In dit artikel bevat informatie over met behulp van Hallo Resource Manager-model.</span><span class="sxs-lookup"><span data-stu-id="e57cb-107">This article covers using hello Resource Manager model.</span></span> <span data-ttu-id="e57cb-108">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e57cb-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
> 
> 

## <a name="resize-hello-os-drive"></a><span data-ttu-id="e57cb-109">Hallo OS station vergroten of verkleinen</span><span class="sxs-lookup"><span data-stu-id="e57cb-109">Resize hello OS drive</span></span>
<span data-ttu-id="e57cb-110">In dit artikel hebt we uitvoeren van de taak Hallo Hallo OS-station met resource manager-modules van formaat wijzigen van [Azure Powershell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="e57cb-110">In this article we’ll accomplish hello task of resizing hello OS drive using resource manager modules of [Azure Powershell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="e57cb-111">Open de Powershell ISE of de Powershell-venster in de beheerdersmodus en volg onderstaande stappen voor Hallo:</span><span class="sxs-lookup"><span data-stu-id="e57cb-111">Open your Powershell ISE or Powershell window in administrative mode and follow hello steps below:</span></span>

1. <span data-ttu-id="e57cb-112">Aanmelden tooyour Microsoft Azure-account op de resource management-modus en selecteer uw abonnement als volgt:</span><span class="sxs-lookup"><span data-stu-id="e57cb-112">Sign-in tooyour Microsoft Azure account in resource management mode and select your subscription as follows:</span></span>
   
   ```Powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription –SubscriptionName 'my-subscription-name'
   ```
2. <span data-ttu-id="e57cb-113">Stel de naam van de resourcegroep en de VM als volgt in:</span><span class="sxs-lookup"><span data-stu-id="e57cb-113">Set your resource group name and VM name as follows:</span></span>
   
   ```Powershell
   $rgName = 'my-resource-group-name'
   $vmName = 'my-vm-name'
   ```
3. <span data-ttu-id="e57cb-114">Een verwijzing tooyour VM als volgt verkrijgen:</span><span class="sxs-lookup"><span data-stu-id="e57cb-114">Obtain a reference tooyour VM as follows:</span></span>
   
   ```Powershell
   $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```
4. <span data-ttu-id="e57cb-115">Hallo VM stoppen voordat het vergroten of verkleinen Hallo schijf als volgt:</span><span class="sxs-lookup"><span data-stu-id="e57cb-115">Stop hello VM before resizing hello disk as follows:</span></span>
   
    ```Powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    ```
5. <span data-ttu-id="e57cb-116">En komen Hallo momenteel die we hebt gewacht!</span><span class="sxs-lookup"><span data-stu-id="e57cb-116">And here comes hello moment we’ve been waiting for!</span></span> <span data-ttu-id="e57cb-117">Hallo-grootte van de waarde voor toohello gewenst Hallo OS-schijf instellen en Hallo VM als volgt bijwerken:</span><span class="sxs-lookup"><span data-stu-id="e57cb-117">Set hello size of hello OS disk toohello desired value and update hello VM as follows:</span></span>
   
   ```Powershell
   $vm.StorageProfile.OSDisk.DiskSizeGB = 1023
   Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
   ```
   
   > [!WARNING]
   > <span data-ttu-id="e57cb-118">Hallo nieuwe grootte moet groter zijn dan de bestaande schijfgrootte Hallo zijn.</span><span class="sxs-lookup"><span data-stu-id="e57cb-118">hello new size should be greater than hello existing disk size.</span></span> <span data-ttu-id="e57cb-119">maximale toegestane Hallo is 1023 GB.</span><span class="sxs-lookup"><span data-stu-id="e57cb-119">hello maximum allowed is 1023 GB.</span></span>
   > 
   > 
6. <span data-ttu-id="e57cb-120">Bijwerken Hallo VM kan een paar seconden duren.</span><span class="sxs-lookup"><span data-stu-id="e57cb-120">Updating hello VM may take a few seconds.</span></span> <span data-ttu-id="e57cb-121">Zodra het Hallo-opdracht is uitgevoerd, start u Hallo VM als volgt opnieuw:</span><span class="sxs-lookup"><span data-stu-id="e57cb-121">Once hello command finishes executing, restart hello VM as follows:</span></span>
   
   ```Powershell
   Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```

<span data-ttu-id="e57cb-122">Dat is alles.</span><span class="sxs-lookup"><span data-stu-id="e57cb-122">And that’s it!</span></span> <span data-ttu-id="e57cb-123">Nu RDP in Hallo VM, open Computerbeheer (of Schijfbeheer) en vouw Hallo-station met Hallo zojuist toegewezen ruimte.</span><span class="sxs-lookup"><span data-stu-id="e57cb-123">Now RDP into hello VM, open Computer Management (or Disk Management) and expand hello drive using hello newly allocated space.</span></span>

## <a name="summary"></a><span data-ttu-id="e57cb-124">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="e57cb-124">Summary</span></span>
<span data-ttu-id="e57cb-125">In dit artikel hebben we Azure Resource Manager-modules van Powershell tooexpand Hallo OS-schijf van de virtuele machine voor IaaS gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e57cb-125">In this article, we used Azure Resource Manager modules of Powershell tooexpand hello OS drive of an IaaS virtual machine.</span></span> <span data-ttu-id="e57cb-126">Hieronder wordt Hallo volledige script ter referentie:</span><span class="sxs-lookup"><span data-stu-id="e57cb-126">Reproduced below is hello complete script for your reference:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="e57cb-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e57cb-127">Next Steps</span></span>
<span data-ttu-id="e57cb-128">Hoewel in dit artikel wordt primair gericht op het uitbreiden van de schijf Hallo OS Hallo VM, kan hello ontwikkelde script ook worden gebruikt voor het uitbreiden van Hallo gegevens schijven gekoppelde toohello VM door één regel code wijzigen.</span><span class="sxs-lookup"><span data-stu-id="e57cb-128">Though in this article, we focused primarily on expanding hello OS disk of hello VM, hello developed script may also be used for expanding hello data disks attached toohello VM by changing a single line of code.</span></span> <span data-ttu-id="e57cb-129">Bijvoorbeeld tooexpand Hallo eerste gegevens gekoppelde toohello VM schijf, vervang Hallo ```OSDisk``` object van het ```StorageProfile``` met ```DataDisks``` matrix en het gebruik van een numerieke index tooobtain een schijf verwijzing toofirst bijgesloten gegevens, zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="e57cb-129">For example, tooexpand hello first data disk attached toohello VM, replace hello ```OSDisk``` object of ```StorageProfile``` with ```DataDisks``` array and use a numeric index tooobtain a reference toofirst attached data disk, as shown below:</span></span>

```Powershell
$vm.StorageProfile.DataDisks[0].DiskSizeGB = 1023
```
<span data-ttu-id="e57cb-130">U kunt ook verwijzen naar andere schijven gekoppelde toohello VM, met behulp van een index, zoals hierboven van gegevens of Hallo ```Name``` van Hallo schijf zoals hieronder weergegeven:</span><span class="sxs-lookup"><span data-stu-id="e57cb-130">Similarly you may reference other data disks attached toohello VM, either by using an index as shown above or hello ```Name``` property of hello disk as illustrated below:</span></span>

```Powershell
($vm.StorageProfile.DataDisks | Where {$_.Name -eq 'my-second-data-disk'})[0].DiskSizeGB = 1023
```

<span data-ttu-id="e57cb-131">Als u toofind wilt uit hoe tooattach tooan Azure Resource Manager VM schijven, dit selectievakje inschakelt [artikel](../articles/virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e57cb-131">If you want toofind out how tooattach disks tooan Azure Resource Manager VM, check this [article](../articles/virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

