<span data-ttu-id="1fefc-101">Ondersteuning voor twee foutopsporingsfuncties is nu beschikbaar in Azure: ondersteuning voor Console-uitvoer en Schermafbeelding voor het Azure Virtual Machines Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="1fefc-101">Support for two debugging features is now available in Azure: Console Output and Screenshot support for Azure Virtual Machines Resource Manager deployment model.</span></span> 

<span data-ttu-id="1fefc-102">Wanneer u uw eigen installatiekopie tooAzure of zelfs opstarten een van de installatiekopieën van het platform hello te brengen, kunnen er diverse redenen waarom een virtuele Machine in een niet-opstartbare status opgehaald.</span><span class="sxs-lookup"><span data-stu-id="1fefc-102">When bringing your own image tooAzure or even booting one of hello platform images, there can be many reasons why a Virtual Machine gets into a non-bootable state.</span></span> <span data-ttu-id="1fefc-103">Met deze functies kunt u tooeasily diagnosticeren en op uw virtuele Machines herstellen.</span><span class="sxs-lookup"><span data-stu-id="1fefc-103">These features enable you tooeasily diagnose and recover your Virtual Machines from boot failures.</span></span>

<span data-ttu-id="1fefc-104">Voor virtuele Linux-Machines, kunt u eenvoudig hello uitvoer van uw consolelogboek van Hallo Portal bekijken:</span><span class="sxs-lookup"><span data-stu-id="1fefc-104">For Linux Virtual Machines, you can easily view hello output of your console log from hello Portal:</span></span>

![Azure Portal](./media/virtual-machines-common-boot-diagnostics/screenshot1.png)
 
<span data-ttu-id="1fefc-106">Echter voor Windows en Linux virtuele Machines kunt Azure ook u een schermopname van Hallo VM van de hypervisor Hallo toosee:</span><span class="sxs-lookup"><span data-stu-id="1fefc-106">However, for both Windows and Linux Virtual Machines, Azure also enables you toosee a screenshot of hello VM from hello hypervisor:</span></span>

![Fout](./media/virtual-machines-common-boot-diagnostics/screenshot2.png)

<span data-ttu-id="1fefc-108">Beide functies worden ondersteund voor virtuele Azure-machines in alle regio's.</span><span class="sxs-lookup"><span data-stu-id="1fefc-108">Both of these features are supported for Azure Virtual Machines in all regions.</span></span> <span data-ttu-id="1fefc-109">Opmerking: de schermafbeeldingen en de uitvoer kunnen duren too10 minuten tooappear in uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="1fefc-109">Note, screenshots, and output can take up too10 minutes tooappear in your storage account.</span></span>

## <a name="common-boot-errors"></a><span data-ttu-id="1fefc-110">Veelvoorkomende opstartfouten</span><span class="sxs-lookup"><span data-stu-id="1fefc-110">Common boot errors</span></span>

- [<span data-ttu-id="1fefc-111">0xC000000E</span><span class="sxs-lookup"><span data-stu-id="1fefc-111">0xC000000E</span></span>](https://support.microsoft.com/help/4010129)
- [<span data-ttu-id="1fefc-112">0xC000000F</span><span class="sxs-lookup"><span data-stu-id="1fefc-112">0xC000000F</span></span>](https://support.microsoft.com/help/4010130)
- [<span data-ttu-id="1fefc-113">0xC0000011</span><span class="sxs-lookup"><span data-stu-id="1fefc-113">0xC0000011</span></span>](https://support.microsoft.com/help/4010134)
- [<span data-ttu-id="1fefc-114">0xC0000034</span><span class="sxs-lookup"><span data-stu-id="1fefc-114">0xC0000034</span></span>](https://support.microsoft.com/help/4010140)
- [<span data-ttu-id="1fefc-115">0xC0000098</span><span class="sxs-lookup"><span data-stu-id="1fefc-115">0xC0000098</span></span>](https://support.microsoft.com/help/4010137)
- [<span data-ttu-id="1fefc-116">0xC00000BA</span><span class="sxs-lookup"><span data-stu-id="1fefc-116">0xC00000BA</span></span>](https://support.microsoft.com/help/4010136)
- [<span data-ttu-id="1fefc-117">0xC000014C</span><span class="sxs-lookup"><span data-stu-id="1fefc-117">0xC000014C</span></span>](https://support.microsoft.com/help/4010141)
- [<span data-ttu-id="1fefc-118">0xC0000221</span><span class="sxs-lookup"><span data-stu-id="1fefc-118">0xC0000221</span></span>](https://support.microsoft.com/help/4010132)
- [<span data-ttu-id="1fefc-119">0xC0000225</span><span class="sxs-lookup"><span data-stu-id="1fefc-119">0xC0000225</span></span>](https://support.microsoft.com/help/4010138)
- [<span data-ttu-id="1fefc-120">0xC0000359</span><span class="sxs-lookup"><span data-stu-id="1fefc-120">0xC0000359</span></span>](https://support.microsoft.com/help/4010135)
- [<span data-ttu-id="1fefc-121">0xC0000605</span><span class="sxs-lookup"><span data-stu-id="1fefc-121">0xC0000605</span></span>](https://support.microsoft.com/help/4010131)
- [<span data-ttu-id="1fefc-122">Er is geen besturingssysteem gevonden</span><span class="sxs-lookup"><span data-stu-id="1fefc-122">An operating system wasn't found</span></span>](https://support.microsoft.com/help/4010142)
- [<span data-ttu-id="1fefc-123">Opstartfout of OPSTARTAPPARAAT_NIET_TOEGANKELIJK</span><span class="sxs-lookup"><span data-stu-id="1fefc-123">Boot failure or INACCESSIBLE_BOOT_DEVICE</span></span>](https://support.microsoft.com/help/4010143)

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a><span data-ttu-id="1fefc-124">Diagnostische gegevens op een nieuwe virtuele machine inschakelen</span><span class="sxs-lookup"><span data-stu-id="1fefc-124">Enable diagnostics on a new virtual machine</span></span>
1. <span data-ttu-id="1fefc-125">Wanneer u een nieuwe virtuele Machine maakt van Hallo Preview-Portal, selecteer Hallo **Azure Resource Manager** uit Hallo deployment model vervolgkeuzelijst:</span><span class="sxs-lookup"><span data-stu-id="1fefc-125">When creating a new Virtual Machine from hello Preview Portal, select hello **Azure Resource Manager** from hello deployment model dropdown:</span></span>
 
    ![Resource Manager](./media/virtual-machines-common-boot-diagnostics/screenshot3.jpg)

2. <span data-ttu-id="1fefc-127">Hallo bewaking optie tooselect Hallo storage-account waarin u tooplace wilt dat deze diagnostische bestanden configureren.</span><span class="sxs-lookup"><span data-stu-id="1fefc-127">Configure hello Monitoring option tooselect hello storage account where you would like tooplace these diagnostic files.</span></span>
 
    ![VM maken](./media/virtual-machines-common-boot-diagnostics/screenshot4.jpg)

3. <span data-ttu-id="1fefc-129">Als u met een Azure Resource Manager-sjabloon implementeert, virtuele-machinebron tooyour navigeren en Hallo diagnostische profielsectie toevoegen.</span><span class="sxs-lookup"><span data-stu-id="1fefc-129">If you are deploying from an Azure Resource Manager template, navigate tooyour Virtual Machine resource and append hello diagnostics profile section.</span></span> <span data-ttu-id="1fefc-130">Houd er rekening mee toouse Hallo '2015-06-15' API-versie-header.</span><span class="sxs-lookup"><span data-stu-id="1fefc-130">Remember toouse hello “2015-06-15” API version header.</span></span>

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. <span data-ttu-id="1fefc-131">Hallo diagnostische profiel kunt u tooselect Hallo storage-account waar u tooput deze logboeken.</span><span class="sxs-lookup"><span data-stu-id="1fefc-131">hello diagnostics profile enables you tooselect hello storage account where you want tooput these logs.</span></span>

    ```json
            "diagnosticsProfile": {
                "bootDiagnostics": {
                "enabled": true,
                "storageUri": "[concat('http://', parameters('newStorageAccountName'), '.blob.core.windows.net')]"
                }
            }
            }
        }
    ```

<span data-ttu-id="1fefc-132">een voorbeeld van een virtuele Machine met diagnostische gegevens over opstarten is ingeschakeld, het uitchecken van onze opslagplaats hier toodeploy.</span><span class="sxs-lookup"><span data-stu-id="1fefc-132">toodeploy a sample Virtual Machine with boot diagnostics enabled, check out our repo here.</span></span>

## <a name="update-an-existing-virtual-machine"></a><span data-ttu-id="1fefc-133">Een bestaande virtuele machine bijwerken</span><span class="sxs-lookup"><span data-stu-id="1fefc-133">Update an existing virtual machine</span></span> ##

<span data-ttu-id="1fefc-134">tooenable diagnostische gegevens over opstarten via Hallo Portal, kunt u ook een bestaande virtuele Machine via de Portal Hallo bijwerken.</span><span class="sxs-lookup"><span data-stu-id="1fefc-134">tooenable boot diagnostics through hello Portal, you can also update an existing Virtual Machine through hello Portal.</span></span> <span data-ttu-id="1fefc-135">Selecteer Hallo Boot Diagnostics optie en opslaan.</span><span class="sxs-lookup"><span data-stu-id="1fefc-135">Select hello Boot Diagnostics option and Save.</span></span> <span data-ttu-id="1fefc-136">Opnieuw opstarten Hallo VM tootake effect.</span><span class="sxs-lookup"><span data-stu-id="1fefc-136">Restart hello VM tootake effect.</span></span>

![Bestaande VM bijwerken](./media/virtual-machines-common-boot-diagnostics/screenshot5.png)

