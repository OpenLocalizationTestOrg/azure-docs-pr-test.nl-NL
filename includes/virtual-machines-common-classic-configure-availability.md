


<span data-ttu-id="b6e39-101">Een beschikbaarheidsset helpt uw virtuele machines beschikbaar zijn tijdens de uitvaltijd, zoals behouden tijdens onderhoud.</span><span class="sxs-lookup"><span data-stu-id="b6e39-101">An availability set helps keep your virtual machines available during downtime, such as during maintenance.</span></span> <span data-ttu-id="b6e39-102">Als u twee of meer op vergelijkbare wijze geconfigureerde virtuele machines in een beschikbaarheidsset maakt Hallo redundantie nodig toomaintain beschikbaarheid van het Hallo-toepassingen of services die de virtuele machine wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b6e39-102">Placing two or more similarly configured virtual machines in an availability set creates hello redundancy needed toomaintain availability of hello applications or services that your virtual machine runs.</span></span> <span data-ttu-id="b6e39-103">Zie voor meer informatie over hoe dit werkt [Hallo beschikbaarheid van virtuele machines beheren][Manage hello availability of virtual machines].</span><span class="sxs-lookup"><span data-stu-id="b6e39-103">For details about how this works, see [Manage hello availability of virtual machines][Manage hello availability of virtual machines].</span></span>

<span data-ttu-id="b6e39-104">Het is een best practice toouse zowel beschikbaarheidssets als eindpunten toohelp taakverdeling ervoor te zorgen dat uw toepassing altijd beschikbaar en worden uitgevoerd efficiënt is.</span><span class="sxs-lookup"><span data-stu-id="b6e39-104">It's a best practice toouse both availability sets and load-balancing endpoints toohelp ensure that your application is always available and running efficiently.</span></span> <span data-ttu-id="b6e39-105">Zie voor meer informatie over Netwerktaakverdeling eindpunten [taakverdeling voor Azure-infrastructuurservices][Load balancing for Azure infrastructure services].</span><span class="sxs-lookup"><span data-stu-id="b6e39-105">For details about load-balanced endpoints, see [Load balancing for Azure infrastructure services][Load balancing for Azure infrastructure services].</span></span>

<span data-ttu-id="b6e39-106">U kunt de klassieke virtuele machines toevoegen in een beschikbaarheidsset met behulp van een van twee opties:</span><span class="sxs-lookup"><span data-stu-id="b6e39-106">You can add classic virtual machines into an availability set by using one of two options:</span></span>

* <span data-ttu-id="b6e39-107">[Optie 1: Een virtuele machine maken en een beschikbaarheidsset op Hallo dezelfde tijd][Option 1: Create a virtual machine and an availability set at hello same time].</span><span class="sxs-lookup"><span data-stu-id="b6e39-107">[Option 1: Create a virtual machine and an availability set at hello same time][Option 1: Create a virtual machine and an availability set at hello same time].</span></span> <span data-ttu-id="b6e39-108">Vervolgens voegt u een nieuwe virtuele machines toohello ingesteld bij het maken van deze virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="b6e39-108">Then, add new virtual machines toohello set when you create those virtual machines.</span></span>
* <span data-ttu-id="b6e39-109">[Optie 2: Voeg een bestaande beschikbaarheidsset voor de virtuele machine tooan][Option 2: Add an existing virtual machine tooan availability set].</span><span class="sxs-lookup"><span data-stu-id="b6e39-109">[Option 2: Add an existing virtual machine tooan availability set][Option 2: Add an existing virtual machine tooan availability set].</span></span>

> [!NOTE]
> <span data-ttu-id="b6e39-110">In het klassieke model Hallo Hallo virtuele machines die u wilt tooput in dezelfde beschikbaarheidsset moet behoren toohello dezelfde cloudservice.</span><span class="sxs-lookup"><span data-stu-id="b6e39-110">In hello classic model, virtual machines that you want tooput in hello same availability set must belong toohello same cloud service.</span></span>
> 
> 

## <span data-ttu-id="b6e39-111"><a id="createset"></a>Optie 1: een virtuele machine maken en een beschikbaarheidsset op Hallo dezelfde tijd</span><span class="sxs-lookup"><span data-stu-id="b6e39-111"><a id="createset"> </a>Option 1: Create a virtual machine and an availability set at hello same time</span></span>
<span data-ttu-id="b6e39-112">U kunt beide hello Azure-portal of Azure PowerShell-opdrachten toodo dit.</span><span class="sxs-lookup"><span data-stu-id="b6e39-112">You can use either hello Azure portal or Azure PowerShell commands toodo this.</span></span>

<span data-ttu-id="b6e39-113">toouse hello Azure-portal:</span><span class="sxs-lookup"><span data-stu-id="b6e39-113">toouse hello Azure portal:</span></span>

1. <span data-ttu-id="b6e39-114">Als u dit nog niet hebt gedaan, meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b6e39-114">If you haven't already done so, sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b6e39-115">Klik op het menu hub Hallo **+ nieuw**, en klik vervolgens op **virtuele Machine**.</span><span class="sxs-lookup"><span data-stu-id="b6e39-115">On hello hub menu, click **+ New**, and then click **Virtual Machine**.</span></span>
   
    ![De installatiekopie van de alternatieve tekst](./media/virtual-machines-common-classic-configure-availability/ChooseVMImage.png)
3. <span data-ttu-id="b6e39-117">Selecteer Hallo Marketplace virtuele machine-installatiekopie die u wenst dat toouse.</span><span class="sxs-lookup"><span data-stu-id="b6e39-117">Select hello Marketplace virtual machine image you wish toouse.</span></span> <span data-ttu-id="b6e39-118">U kunt een virtuele machine van Linux of Windows toocreate.</span><span class="sxs-lookup"><span data-stu-id="b6e39-118">You can choose toocreate a Linux or Windows virtual machine.</span></span>
4. <span data-ttu-id="b6e39-119">Controleer of dat implementatiemodel hello te is ingesteld voor Hallo virtuele machine geselecteerde,**klassieke** en klik vervolgens op **maken**</span><span class="sxs-lookup"><span data-stu-id="b6e39-119">For hello selected virtual machine, verify that hello deployment model is set too**Classic** and then click **Create**</span></span>
   
    ![De installatiekopie van de alternatieve tekst](./media/virtual-machines-common-classic-configure-availability/ChooseClassicModel.png)
5. <span data-ttu-id="b6e39-121">Voer een naam van virtuele machine, de gebruikersnaam en het wachtwoord (voor Windows-machines) of de openbare SSH-sleutel (voor Linux-machines).</span><span class="sxs-lookup"><span data-stu-id="b6e39-121">Enter a virtual machine name, user name and password (for Windows machines) or SSH public key (for Linux machines).</span></span> 
6. <span data-ttu-id="b6e39-122">Kies Hallo VM-grootte en klik vervolgens op **Selecteer** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="b6e39-122">Choose hello VM size and then click **Select** toocontinue.</span></span>
7. <span data-ttu-id="b6e39-123">Kies **optionele configuratie > beschikbaarheidsset**, en selecteer Hallo beschikbaarheidsset tooadd Hallo virtuele machine gewenst.</span><span class="sxs-lookup"><span data-stu-id="b6e39-123">Choose **Optional Configuration > Availability set**, and select hello availability set you wish tooadd hello virtual machine to.</span></span>
   
    ![De installatiekopie van de alternatieve tekst](./media/virtual-machines-common-classic-configure-availability/ChooseAvailabilitySet.png) 
8. <span data-ttu-id="b6e39-125">Controleer uw configuratie-instellingen.</span><span class="sxs-lookup"><span data-stu-id="b6e39-125">Review your configuration settings.</span></span> <span data-ttu-id="b6e39-126">Wanneer u bent klaar, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="b6e39-126">When you're done, click **Create**.</span></span>
9. <span data-ttu-id="b6e39-127">Terwijl Azure de virtuele machine maakt, kunt u de voortgang Hallo onder bijhouden **virtuele Machines** in Hallo hub-menu.</span><span class="sxs-lookup"><span data-stu-id="b6e39-127">While Azure creates your virtual machine, you can track hello progress under **Virtual Machines** in hello hub menu.</span></span>

<span data-ttu-id="b6e39-128">toouse Azure PowerShell-opdrachten toocreate Azure een virtuele machine en toe te voegen nieuwe of bestaande beschikbaarheidsset tooa, Zie [toocreate gebruik Azure PowerShell en vooraf configureren van virtuele machines op basis van Windows](../articles/virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="b6e39-128">toouse Azure PowerShell commands toocreate an Azure virtual machine and add it tooa new or existing availability set, see [Use Azure PowerShell toocreate and preconfigure Windows-based virtual machines](../articles/virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

## <span data-ttu-id="b6e39-129"><a id="addmachine"></a>Optie 2: een bestaande beschikbaarheidsset voor de virtuele machine tooan toevoegen</span><span class="sxs-lookup"><span data-stu-id="b6e39-129"><a id="addmachine"> </a>Option 2: Add an existing virtual machine tooan availability set</span></span>
<span data-ttu-id="b6e39-130">U kunt in hello Azure-portal, bestaande klassieke virtuele machines tooan bestaande beschikbaarheidsset toevoegen of een nieuwe voor hen maken.</span><span class="sxs-lookup"><span data-stu-id="b6e39-130">In hello Azure portal, you can add existing classic virtual machines tooan existing availability set or create a new one for them.</span></span> <span data-ttu-id="b6e39-131">(Houd er rekening mee dat Hallo virtuele machines in dezelfde beschikbaarheidsset Hallo toohello moet behoren dezelfde cloudservice.) Hallo stappen zijn bijna hetzelfde Hallo.</span><span class="sxs-lookup"><span data-stu-id="b6e39-131">(Keep in mind that hello virtual machines in hello same availability set must belong toohello same cloud service.) hello steps are almost hello same.</span></span> <span data-ttu-id="b6e39-132">U kunt met Azure PowerShell Hallo virtuele machine tooan bestaande beschikbaarheidsset toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b6e39-132">With Azure PowerShell, you can add hello virtual machine tooan existing availability set.</span></span>

1. <span data-ttu-id="b6e39-133">Als u dit nog niet hebt gedaan, meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b6e39-133">If you have not already done so, sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b6e39-134">Klik op het menu Hub Hallo **virtuele Machines (klassiek)**.</span><span class="sxs-lookup"><span data-stu-id="b6e39-134">On hello Hub menu, click **Virtual Machines (classic)**.</span></span>
   
    ![De installatiekopie van de alternatieve tekst](./media/virtual-machines-common-classic-configure-availability/ChooseClassicVM.png)
3. <span data-ttu-id="b6e39-136">Selecteer in de lijst van de Hallo van virtuele machines, Hallo-naam van Hallo virtuele machine die u wilt dat tooadd toohello set.</span><span class="sxs-lookup"><span data-stu-id="b6e39-136">From hello list of virtual machines, select hello name of hello virtual machine that you want tooadd toohello set.</span></span>
4. <span data-ttu-id="b6e39-137">Kies **beschikbaarheidsset** van Hallo virtuele machine **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="b6e39-137">Choose **Availability set** from hello virtual machine **Settings**.</span></span>
   
    ![De installatiekopie van de alternatieve tekst](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetSettings.png)
5. <span data-ttu-id="b6e39-139">Hallo beschikbaarheidsset tooadd Hallo virtuele machine te gewenst selecteren.</span><span class="sxs-lookup"><span data-stu-id="b6e39-139">Select hello availability set you wish tooadd hello virtual machine to.</span></span> <span data-ttu-id="b6e39-140">Hallo virtuele machine moet behoren toohello dezelfde cloudservice als Hallo beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="b6e39-140">hello virtual machine must belong toohello same cloud service as hello availability set.</span></span>
   
    ![De installatiekopie van de alternatieve tekst](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetPicker.png)
6. <span data-ttu-id="b6e39-142">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="b6e39-142">Click **Save**.</span></span>

<span data-ttu-id="b6e39-143">toouse Azure PowerShell-opdrachten, open een Azure PowerShell-sessie beheerdersniveau en Hallo volgende opdracht uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="b6e39-143">toouse Azure PowerShell commands, open an administrator-level Azure PowerShell session and run hello following command.</span></span> <span data-ttu-id="b6e39-144">Voor tijdelijke aanduidingen hello (zoals &lt;VmCloudServiceName&gt;), vervangt u alles binnen de aanhalingstekens hello, inclusief Hallo < en > tekens, met Hallo de juiste namen.</span><span class="sxs-lookup"><span data-stu-id="b6e39-144">For hello placeholders (such as &lt;VmCloudServiceName&gt;), replace everything within hello quotes, including hello < and > characters, with hello correct names.</span></span>

    Get-AzureVM -ServiceName "<VmCloudServiceName>" -Name "<VmName>" | Set-AzureAvailabilitySet -AvailabilitySetName "<AvSetName>" | Update-AzureVM

> [!NOTE]
> <span data-ttu-id="b6e39-145">Hallo virtuele machine mogelijk opnieuw opgestart toobe toofinish toe te voegen toohello beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="b6e39-145">hello virtual machine might have toobe restarted toofinish adding it toohello availability set.</span></span>
> 
> 

<!-- LINKS -->
[Option 1: Create a virtual machine and an availability set at hello same time]: #createset
[Option 2: Add an existing virtual machine tooan availability set]: #addmachine

[Load balancing for Azure infrastructure services]: ../articles/virtual-machines/virtual-machines-linux-load-balance.md
[Manage hello availability of virtual machines]:../articles/virtual-machines/linux/manage-availability.md

[Create a virtual machine running Windows]: ../articles/virtual-machines/virtual-machines-windows-hero-tutorial.md
[Virtual Network overview]: ../articles/virtual-network/virtual-networks-overview.md

