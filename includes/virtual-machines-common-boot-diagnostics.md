<span data-ttu-id="d2ee1-101">Ondersteuning voor twee foutopsporingsfuncties is nu beschikbaar in Azure: ondersteuning voor Console-uitvoer en Schermafbeelding voor het Azure Virtual Machines Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="d2ee1-101">Support for two debugging features is now available in Azure: Console Output and Screenshot support for Azure Virtual Machines Resource Manager deployment model.</span></span> 

<span data-ttu-id="d2ee1-102">Wanneer u uw eigen installatiekopie importeert in Azure of een van de installatiekopieën van het platform opstart, kan een VM vanwege verschillende redenen in een status belanden waarin deze niet kan worden opgestart.</span><span class="sxs-lookup"><span data-stu-id="d2ee1-102">When bringing your own image to Azure or even booting one of the platform images, there can be many reasons why a Virtual Machine gets into a non-bootable state.</span></span> <span data-ttu-id="d2ee1-103">Met deze functies kunt u uw virtuele machines eenvoudig analyseren en herstellen na fouten bij het opstarten.</span><span class="sxs-lookup"><span data-stu-id="d2ee1-103">These features enable you to easily diagnose and recover your Virtual Machines from boot failures.</span></span>

<span data-ttu-id="d2ee1-104">Bij virtuele Linux-machines kunt u eenvoudig de uitvoer van uw consolelogboek bekijken via de portal:</span><span class="sxs-lookup"><span data-stu-id="d2ee1-104">For Linux Virtual Machines, you can easily view the output of your console log from the Portal:</span></span>

![Azure Portal](./media/virtual-machines-common-boot-diagnostics/screenshot1.png)
 
<span data-ttu-id="d2ee1-106">U kunt echter bij zowel virtuele Windows- als Linux-machines een schermopname van de virtuele machine bekijken via de hypervisor van Azure:</span><span class="sxs-lookup"><span data-stu-id="d2ee1-106">However, for both Windows and Linux Virtual Machines, Azure also enables you to see a screenshot of the VM from the hypervisor:</span></span>

![Fout](./media/virtual-machines-common-boot-diagnostics/screenshot2.png)

<span data-ttu-id="d2ee1-108">Beide functies worden ondersteund voor virtuele Azure-machines in alle regio's.</span><span class="sxs-lookup"><span data-stu-id="d2ee1-108">Both of these features are supported for Azure Virtual Machines in all regions.</span></span> <span data-ttu-id="d2ee1-109">Houd er rekening mee dat het tot 10 minuten kan duren voordat de schermafbeeldingen en uitvoer worden weergegeven in uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="d2ee1-109">Note, screenshots, and output can take up to 10 minutes to appear in your storage account.</span></span>

## <a name="common-boot-errors"></a><span data-ttu-id="d2ee1-110">Veelvoorkomende opstartfouten</span><span class="sxs-lookup"><span data-stu-id="d2ee1-110">Common boot errors</span></span>

- [<span data-ttu-id="d2ee1-111">0xC000000E</span><span class="sxs-lookup"><span data-stu-id="d2ee1-111">0xC000000E</span></span>](https://support.microsoft.com/help/4010129)
- [<span data-ttu-id="d2ee1-112">0xC000000F</span><span class="sxs-lookup"><span data-stu-id="d2ee1-112">0xC000000F</span></span>](https://support.microsoft.com/help/4010130)
- [<span data-ttu-id="d2ee1-113">0xC0000011</span><span class="sxs-lookup"><span data-stu-id="d2ee1-113">0xC0000011</span></span>](https://support.microsoft.com/help/4010134)
- [<span data-ttu-id="d2ee1-114">0xC0000034</span><span class="sxs-lookup"><span data-stu-id="d2ee1-114">0xC0000034</span></span>](https://support.microsoft.com/help/4010140)
- [<span data-ttu-id="d2ee1-115">0xC0000098</span><span class="sxs-lookup"><span data-stu-id="d2ee1-115">0xC0000098</span></span>](https://support.microsoft.com/help/4010137)
- [<span data-ttu-id="d2ee1-116">0xC00000BA</span><span class="sxs-lookup"><span data-stu-id="d2ee1-116">0xC00000BA</span></span>](https://support.microsoft.com/help/4010136)
- [<span data-ttu-id="d2ee1-117">0xC000014C</span><span class="sxs-lookup"><span data-stu-id="d2ee1-117">0xC000014C</span></span>](https://support.microsoft.com/help/4010141)
- [<span data-ttu-id="d2ee1-118">0xC0000221</span><span class="sxs-lookup"><span data-stu-id="d2ee1-118">0xC0000221</span></span>](https://support.microsoft.com/help/4010132)
- [<span data-ttu-id="d2ee1-119">0xC0000225</span><span class="sxs-lookup"><span data-stu-id="d2ee1-119">0xC0000225</span></span>](https://support.microsoft.com/help/4010138)
- [<span data-ttu-id="d2ee1-120">0xC0000359</span><span class="sxs-lookup"><span data-stu-id="d2ee1-120">0xC0000359</span></span>](https://support.microsoft.com/help/4010135)
- [<span data-ttu-id="d2ee1-121">0xC0000605</span><span class="sxs-lookup"><span data-stu-id="d2ee1-121">0xC0000605</span></span>](https://support.microsoft.com/help/4010131)
- [<span data-ttu-id="d2ee1-122">Er is geen besturingssysteem gevonden</span><span class="sxs-lookup"><span data-stu-id="d2ee1-122">An operating system wasn't found</span></span>](https://support.microsoft.com/help/4010142)
- [<span data-ttu-id="d2ee1-123">Opstartfout of OPSTARTAPPARAAT_NIET_TOEGANKELIJK</span><span class="sxs-lookup"><span data-stu-id="d2ee1-123">Boot failure or INACCESSIBLE_BOOT_DEVICE</span></span>](https://support.microsoft.com/help/4010143)

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a><span data-ttu-id="d2ee1-124">Diagnostische gegevens op een nieuwe virtuele machine inschakelen</span><span class="sxs-lookup"><span data-stu-id="d2ee1-124">Enable diagnostics on a new virtual machine</span></span>
1. <span data-ttu-id="d2ee1-125">Wanneer u een nieuwe virtuele machine maakt in de Preview Portal, selecteert u de **Azure Resource Manager** uit de vervolgkeuzelijst van het implementatiemodel:</span><span class="sxs-lookup"><span data-stu-id="d2ee1-125">When creating a new Virtual Machine from the Preview Portal, select the **Azure Resource Manager** from the deployment model dropdown:</span></span>
 
    ![Resource Manager](./media/virtual-machines-common-boot-diagnostics/screenshot3.jpg)

2. <span data-ttu-id="d2ee1-127">Configureer de optie Bewaking om het opslagaccount te selecteren waarin u wilt deze diagnostische bestanden wilt plaatsen.</span><span class="sxs-lookup"><span data-stu-id="d2ee1-127">Configure the Monitoring option to select the storage account where you would like to place these diagnostic files.</span></span>
 
    ![VM maken](./media/virtual-machines-common-boot-diagnostics/screenshot4.jpg)

3. <span data-ttu-id="d2ee1-129">Als u met een Azure Resource Manager-sjabloon implementeert, gaat u naar de resource van de virtuele machine en voegt u de sectie diagnostisch profiel toe.</span><span class="sxs-lookup"><span data-stu-id="d2ee1-129">If you are deploying from an Azure Resource Manager template, navigate to your Virtual Machine resource and append the diagnostics profile section.</span></span> <span data-ttu-id="d2ee1-130">Vergeet niet de API-versieheader '2015-06-15' te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d2ee1-130">Remember to use the “2015-06-15” API version header.</span></span>

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. <span data-ttu-id="d2ee1-131">Met het diagnostische profiel kunt u het opslagaccount selecteren waarin u deze logboeken wilt opslaan.</span><span class="sxs-lookup"><span data-stu-id="d2ee1-131">The diagnostics profile enables you to select the storage account where you want to put these logs.</span></span>

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

<span data-ttu-id="d2ee1-132">Bekijk hier onze opslagplaats om een voorbeeld-VM te implementeren waarop met diagnostische gegevens over het opstarten zijn ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="d2ee1-132">To deploy a sample Virtual Machine with boot diagnostics enabled, check out our repo here.</span></span>

## <a name="update-an-existing-virtual-machine"></a><span data-ttu-id="d2ee1-133">Een bestaande virtuele machine bijwerken</span><span class="sxs-lookup"><span data-stu-id="d2ee1-133">Update an existing virtual machine</span></span> ##

<span data-ttu-id="d2ee1-134">U kunt ook een bestaande virtuele machine bijwerken via de portal zodat de diagnostische gegevens over het opstarten via de portal zijn ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="d2ee1-134">To enable boot diagnostics through the Portal, you can also update an existing Virtual Machine through the Portal.</span></span> <span data-ttu-id="d2ee1-135">Selecteer de optie Diagnostische gegevens over het opstarten en selecteer vervolgens Opslaan.</span><span class="sxs-lookup"><span data-stu-id="d2ee1-135">Select the Boot Diagnostics option and Save.</span></span> <span data-ttu-id="d2ee1-136">Start de VM opnieuw op om de wijzigingen door te voeren.</span><span class="sxs-lookup"><span data-stu-id="d2ee1-136">Restart the VM to take effect.</span></span>

![Bestaande VM bijwerken](./media/virtual-machines-common-boot-diagnostics/screenshot5.png)

