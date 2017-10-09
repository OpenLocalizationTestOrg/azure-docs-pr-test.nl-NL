1. <span data-ttu-id="24a89-101">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="24a89-101">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="24a89-102">Beginnen in de linkerbovenhoek hello, klikt u op **Nieuw > berekenen > Windows Server 2016 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="24a89-102">Starting in hello upper left, click **New > Compute > Windows Server 2016 Datacenter**.</span></span>

    ![Navigeer toohello Azure VM-installatiekopieën in Hallo-portal](./media/virtual-machines-common-portal-create-fqdn/marketplace-new.png)

3. <span data-ttu-id="24a89-104">Selecteer op de Windows Server 2016 Datacenter hello, Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="24a89-104">On hello Windows Server 2016 Datacenter, select hello Classic deployment model.</span></span> <span data-ttu-id="24a89-105">Klik op Maken.</span><span class="sxs-lookup"><span data-stu-id="24a89-105">Click Create.</span></span>

    ![Schermafbeelding van hello Azure VM-installatiekopieën beschikbaar zijn in de portal Hallo](./media/virtual-machines-common-portal-create-fqdn/deployment-classic-model.png)

## <a name="1-basics-blade"></a><span data-ttu-id="24a89-107">1. Blade Grondbeginselen</span><span class="sxs-lookup"><span data-stu-id="24a89-107">1. Basics blade</span></span>

<span data-ttu-id="24a89-108">de blade grondbeginselen Hallo aanvragen beheergegevens voor Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="24a89-108">hello Basics blade requests administrative information for hello virtual machine.</span></span>

1. <span data-ttu-id="24a89-109">Voer een **naam** voor Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="24a89-109">Enter a **Name** for hello virtual machine.</span></span> <span data-ttu-id="24a89-110">In voorbeeld Hallo _HeroVM_ Hallo-naam van Hallo virtuele machine is.</span><span class="sxs-lookup"><span data-stu-id="24a89-110">In hello example, _HeroVM_ is hello name of hello virtual machine.</span></span> <span data-ttu-id="24a89-111">Hallo-naam moet 1-15 tekens lang zijn en het mag geen speciale tekens bevatten.</span><span class="sxs-lookup"><span data-stu-id="24a89-111">hello name must be 1-15 characters long and it cannot contain special characters.</span></span>

2. <span data-ttu-id="24a89-112">Voer een **gebruikersnaam** en een sterk **wachtwoord** die gebruikte toocreate een lokaal account op Hallo VM zijn.</span><span class="sxs-lookup"><span data-stu-id="24a89-112">Enter a **User name** and a strong **Password** that are used toocreate a local account on hello VM.</span></span> <span data-ttu-id="24a89-113">Hallo lokale account wordt gebruikt toosign in tooand Hallo VM beheren.</span><span class="sxs-lookup"><span data-stu-id="24a89-113">hello local account is used toosign in tooand manage hello VM.</span></span> <span data-ttu-id="24a89-114">In voorbeeld Hallo _azureuser_ Hallo-gebruikersnaam.</span><span class="sxs-lookup"><span data-stu-id="24a89-114">In hello example, _azureuser_ is hello user name.</span></span>

 <span data-ttu-id="24a89-115">Hallo wachtwoord moet 8 123 tekens lang zijn en voldoen aan de drie buiten Hallo de volgende vier complexiteitsvereisten: één kleine letter, één hoofdletter, één cijfer en één speciaal teken.</span><span class="sxs-lookup"><span data-stu-id="24a89-115">hello password must be 8-123 characters long and meet three out of hello four following complexity requirements: one lower case character, one upper case character, one number, and one special character.</span></span> <span data-ttu-id="24a89-116">Zie meer informatie over [vereisten voor gebruikersnaam en wachtwoord](../articles/virtual-machines/windows/faq.md).</span><span class="sxs-lookup"><span data-stu-id="24a89-116">See more about [username and password requirements](../articles/virtual-machines/windows/faq.md).</span></span>

3. <span data-ttu-id="24a89-117">Hallo **abonnement** is optioneel.</span><span class="sxs-lookup"><span data-stu-id="24a89-117">hello **Subscription** is optional.</span></span> <span data-ttu-id="24a89-118">Een algemene instelling is 'Betalen naar gebruik'.</span><span class="sxs-lookup"><span data-stu-id="24a89-118">One common setting is "Pay-As-You-Go".</span></span>

4. <span data-ttu-id="24a89-119">Selecteer een bestaande **resourcegroep** of Hallo typenaam voor een nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="24a89-119">Select an existing **Resource group** or type hello name for a new one.</span></span> <span data-ttu-id="24a89-120">In voorbeeld Hallo _HeroVMRG_ Hallo-naam van de resourcegroep Hallo is.</span><span class="sxs-lookup"><span data-stu-id="24a89-120">In hello example, _HeroVMRG_ is hello name of hello resource group.</span></span>

5. <span data-ttu-id="24a89-121">Selecteer een Azure-datacenter **locatie** waar u Hallo VM toorun.</span><span class="sxs-lookup"><span data-stu-id="24a89-121">Select an Azure datacenter **Location** where you want hello VM toorun.</span></span> <span data-ttu-id="24a89-122">In voorbeeld Hallo **VS-Oost** Hallo locatie.</span><span class="sxs-lookup"><span data-stu-id="24a89-122">In hello example, **East US** is hello location.</span></span>

6. <span data-ttu-id="24a89-123">Wanneer u klaar bent, klikt u op **volgende** toocontinue toohello volgende blade.</span><span class="sxs-lookup"><span data-stu-id="24a89-123">When you are done, click **Next** toocontinue toohello next blade.</span></span>

    ![Schermafbeelding van Hallo-instellingen op Hallo basisbeginselen blade voor het configureren van een Azure VM](./media/virtual-machines-common-portal-create-fqdn/basics-blade-classic.png)

## <a name="2-size-blade"></a><span data-ttu-id="24a89-125">2. Blade Grootte</span><span class="sxs-lookup"><span data-stu-id="24a89-125">2. Size blade</span></span>

<span data-ttu-id="24a89-126">Hallo grootte blade configuratiedetails Hallo Hallo VM identificeert en een lijst met verschillende opties die OS, aantal processors, ondersteund schijftype voor opslag en Geschatte maandelijkse gebruikskosten bevatten.</span><span class="sxs-lookup"><span data-stu-id="24a89-126">hello Size blade identifies hello configuration details of hello VM, and lists various choices that include OS, number of processors, disk storage type, and estimated monthly usage costs.</span></span>  

<span data-ttu-id="24a89-127">Kies een VM-grootte en klik vervolgens op **Selecteer** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="24a89-127">Choose a VM size, and then click **Select** toocontinue.</span></span> <span data-ttu-id="24a89-128">In dit voorbeeld _DS1_\__V2 standaard_ Hallo VM-grootte is.</span><span class="sxs-lookup"><span data-stu-id="24a89-128">In this example, _DS1_\__V2 Standard_ is hello VM size.</span></span>

  ![Schermafbeelding van Hallo grootte tabblad waarin hello Azure VM-grootten die u kunt selecteren](./media/virtual-machines-common-portal-create-fqdn/vm-size-classic.png)


## <a name="3-settings-blade"></a><span data-ttu-id="24a89-130">3. Blade Instellingen</span><span class="sxs-lookup"><span data-stu-id="24a89-130">3. Settings blade</span></span>

<span data-ttu-id="24a89-131">de blade instellingen Hallo aanvragen opties voor opslag en netwerk.</span><span class="sxs-lookup"><span data-stu-id="24a89-131">hello Settings blade requests storage and network options.</span></span> <span data-ttu-id="24a89-132">U kunt Hallo standaardinstellingen accepteren.</span><span class="sxs-lookup"><span data-stu-id="24a89-132">You can accept hello default settings.</span></span> <span data-ttu-id="24a89-133">Azure maakt waar nodig de juiste vermeldingen.</span><span class="sxs-lookup"><span data-stu-id="24a89-133">Azure creates appropriate entries where necessary.</span></span>

<span data-ttu-id="24a89-134">Als u voor uw virtuele machine een grootte hebt geselecteerd die hierdoor wordt ondersteund, kunt u Azure Premium Storage uitproberen. Selecteer hiervoor in Schijftype de optie Premium SSD.</span><span class="sxs-lookup"><span data-stu-id="24a89-134">If you selected a virtual machine size that supports it, you can try Azure Premium Storage by selecting Premium (SSD) in Disk type.</span></span>

<span data-ttu-id="24a89-135">Wanneer u alle wijzigingen hebt aangebracht, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="24a89-135">When you're done making changes, click **OK**.</span></span>

## <a name="4-summary-blade"></a><span data-ttu-id="24a89-136">4. Blade Samenvatting</span><span class="sxs-lookup"><span data-stu-id="24a89-136">4. Summary blade</span></span>

<span data-ttu-id="24a89-137">Hallo samenvatting blade bevat Hallo-instellingen die zijn opgegeven in de vorige blades Hallo.</span><span class="sxs-lookup"><span data-stu-id="24a89-137">hello Summary blade lists hello settings specified in hello previous blades.</span></span> <span data-ttu-id="24a89-138">Klik op **OK** wanneer u bent klaar toomake Hallo installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="24a89-138">Click **OK** when you're ready toomake hello image.</span></span>

 ![Samenvatting blade rapport geeft de opgegeven instellingen van Hallo virtuele machine](./media/virtual-machines-common-portal-create-fqdn/summary-blade-classic.png)

<span data-ttu-id="24a89-140">Nadat Hallo virtuele machine is gemaakt, Hallo portal een lijst met nieuwe virtuele machine onder Hallo **alle resources**, en geeft u een tegel van Hallo virtuele machine weer op Hallo-dashboard.</span><span class="sxs-lookup"><span data-stu-id="24a89-140">After hello virtual machine is created, hello portal lists hello new virtual machine under **All resources**, and displays a tile of hello virtual machine on hello dashboard.</span></span> <span data-ttu-id="24a89-141">Hallo bijbehorende cloud service- en storage-account ook zijn gemaakt en wordt vermeld.</span><span class="sxs-lookup"><span data-stu-id="24a89-141">hello corresponding cloud service and storage account also are created and listed.</span></span> <span data-ttu-id="24a89-142">Zowel Hallo virtuele machine en cloudservice automatisch gestart en hun status wordt vermeld als **met**.</span><span class="sxs-lookup"><span data-stu-id="24a89-142">Both hello virtual machine and cloud service are started automatically and their status is listed as **Running**.</span></span>

 ![VM-Agent en Hallo eindpunten van Hallo virtuele machine configureren](./media/virtual-machines-common-portal-create-fqdn/portal-with-new-vm.png)
