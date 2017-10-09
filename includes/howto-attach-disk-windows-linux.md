


## <a name="attach-an-empty-disk"></a><span data-ttu-id="a6553-101">Een lege schijf koppelen</span><span class="sxs-lookup"><span data-stu-id="a6553-101">Attach an empty disk</span></span>
<span data-ttu-id="a6553-102">Koppelen van een lege schijf is een eenvoudige manier tooadd een gegevens-schijf, omdat Azure Hallo .vhd-bestand voor u gemaakt en opgeslagen in Hallo storage-account.</span><span class="sxs-lookup"><span data-stu-id="a6553-102">Attaching an empty disk is a simple way tooadd a data disk, because Azure creates hello .vhd file for you and stores it in hello storage account.</span></span>

1. <span data-ttu-id="a6553-103">Klik op **virtuele Machines (klassiek)**, en vervolgens selecteert Hallo juiste VM.</span><span class="sxs-lookup"><span data-stu-id="a6553-103">Click **Virtual Machines (classic)**, and then select hello appropriate VM.</span></span>

2. <span data-ttu-id="a6553-104">Klik in het menu instellingen Hallo op **schijven**.</span><span class="sxs-lookup"><span data-stu-id="a6553-104">In hello Settings menu, click **Disks**.</span></span>

   ![Een nieuwe lege schijf koppelen](./media/howto-attach-disk-windows-linux/menudisksattachnew.png)

3. <span data-ttu-id="a6553-106">Klik op de opdrachtbalk Hallo **Attach nieuwe**.</span><span class="sxs-lookup"><span data-stu-id="a6553-106">On hello command bar, click **Attach new**.</span></span>  
    <span data-ttu-id="a6553-107">Hallo **nieuwe schijf koppelen** dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a6553-107">hello **Attach new disk** dialog box appears.</span></span>

    ![Een nieuwe schijf koppelen](./media/howto-attach-disk-windows-linux/newdiskdetail.png)

    <span data-ttu-id="a6553-109">Vul Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="a6553-109">Fill in hello following information:</span></span>
    - <span data-ttu-id="a6553-110">In **bestandsnaam**, accepteer de standaardnaam Hallo of typ een andere naam voor Hallo .vhd-bestand.</span><span class="sxs-lookup"><span data-stu-id="a6553-110">In **File Name**, accept hello default name or type another one for hello .vhd file.</span></span> <span data-ttu-id="a6553-111">Hallo gegevensschijf maakt gebruik van een automatisch gegenereerde naam, zelfs als u een andere naam voor de VHD-bestand Hallo typt.</span><span class="sxs-lookup"><span data-stu-id="a6553-111">hello data disk uses an automatically generated name, even if you type another name for hello .vhd file.</span></span>
    - <span data-ttu-id="a6553-112">Selecteer Hallo **Type** van Hallo gegevensschijf.</span><span class="sxs-lookup"><span data-stu-id="a6553-112">Select hello **Type** of hello data disk.</span></span> <span data-ttu-id="a6553-113">Alle virtuele machines ondersteunen standaardschijven.</span><span class="sxs-lookup"><span data-stu-id="a6553-113">All virtual machines support standard disks.</span></span> <span data-ttu-id="a6553-114">Premium-schijven bieden ook ondersteuning voor veel virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="a6553-114">Many virtual machines also support premium disks.</span></span>
    - <span data-ttu-id="a6553-115">Selecteer Hallo **grootte (GB)** van Hallo gegevensschijf.</span><span class="sxs-lookup"><span data-stu-id="a6553-115">Select hello **Size (GB)** of hello data disk.</span></span>
    - <span data-ttu-id="a6553-116">Voor **Hostcaching**, kiest u geen of alleen-lezen.</span><span class="sxs-lookup"><span data-stu-id="a6553-116">For **Host caching**, choose none or Read Only.</span></span>
    - <span data-ttu-id="a6553-117">Klik op OK toofinish.</span><span class="sxs-lookup"><span data-stu-id="a6553-117">Click OK toofinish.</span></span>

4. <span data-ttu-id="a6553-118">Nadat de gegevensschijf Hallo is gemaakt en gekoppeld, wordt deze vermeld in Hallo schijven gedeelte Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="a6553-118">After hello data disk is created and attached, it's listed in hello disks section of hello VM.</span></span>

   ![Nieuwe en lege gegevensschijf gekoppeld](./media/howto-attach-disk-windows-linux/newdiskemptysuccessful.png)

> [!NOTE]
> <span data-ttu-id="a6553-120">Nadat u een gegevensschijf toevoegt, kunt u toolog op toohello VM nodig en Hallo schijf initialiseren zodat deze kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a6553-120">After you add a data disk, you need toolog on toohello VM and initialize hello disk so that it can be used.</span></span>

## <a name="how-to-attach-an-existing-disk"></a><span data-ttu-id="a6553-121">Procedure: een bestaande schijf koppelen</span><span class="sxs-lookup"><span data-stu-id="a6553-121">How to: Attach an existing disk</span></span>
<span data-ttu-id="a6553-122">Als u een bestaande schijf wilt koppelen, dient u een .vhd beschikbaar te hebben in een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="a6553-122">Attaching an existing disk requires that you have a .vhd available in a storage account.</span></span> <span data-ttu-id="a6553-123">Gebruik Hallo [Add-AzureVhd](https://msdn.microsoft.com/library/azure/dn495173.aspx) cmdlet tooupload Hallo .vhd-bestand toohello storage-account.</span><span class="sxs-lookup"><span data-stu-id="a6553-123">Use hello [Add-AzureVhd](https://msdn.microsoft.com/library/azure/dn495173.aspx) cmdlet tooupload hello .vhd file toohello storage account.</span></span> <span data-ttu-id="a6553-124">Nadat u hebt gemaakt en Hallo .vhd-bestand wordt geüpload, kunt u deze tooa VM koppelen.</span><span class="sxs-lookup"><span data-stu-id="a6553-124">After you've created and uploaded hello .vhd file, you can attach it tooa VM.</span></span>

1. <span data-ttu-id="a6553-125">Klik op **virtuele Machines (klassiek)**, en vervolgens selecteert Hallo juiste virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="a6553-125">Click **Virtual Machines (classic)**, and then select hello appropriate virtual machine.</span></span>

2. <span data-ttu-id="a6553-126">Klik in het menu instellingen Hallo op **schijven**.</span><span class="sxs-lookup"><span data-stu-id="a6553-126">In hello Settings menu, click **Disks**.</span></span>

3. <span data-ttu-id="a6553-127">Klik op de opdrachtbalk Hallo **Attach bestaande**.</span><span class="sxs-lookup"><span data-stu-id="a6553-127">On hello command bar, click **Attach existing**.</span></span>

    ![Een gegevensschijf koppelen](./media/howto-attach-disk-windows-linux/menudisksattachexisting.png)

4. <span data-ttu-id="a6553-129">Klik op **locatie**.</span><span class="sxs-lookup"><span data-stu-id="a6553-129">Click **Location**.</span></span> <span data-ttu-id="a6553-130">Hallo beschikbaar opslagaccounts weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a6553-130">hello available storage accounts display.</span></span> <span data-ttu-id="a6553-131">Selecteer vervolgens een juiste storage-account in de lijst.</span><span class="sxs-lookup"><span data-stu-id="a6553-131">Next, select an appropriate storage account from those listed.</span></span>

    ![Schijf storage-account opgeven](./media/howto-attach-disk-windows-linux/existdiskstorageaccounts.png)

5. <span data-ttu-id="a6553-133">Een **opslagaccount** bevat een of meer containers die harde schijven (VHD's) bevatten.</span><span class="sxs-lookup"><span data-stu-id="a6553-133">A **Storage account** holds one or more containers that contain disk drives (vhds).</span></span> <span data-ttu-id="a6553-134">Selecteer de juiste container Hallo in de lijst.</span><span class="sxs-lookup"><span data-stu-id="a6553-134">Select hello appropriate container from those listed.</span></span>

    ![Container van virtuele machines-windows bieden](./media/howto-attach-disk-windows-linux/existdiskcontainers.png)

6. <span data-ttu-id="a6553-136">Hallo **VHD's** deelvenster Hallo schijfstations ondergebracht in Hallo container bevat.</span><span class="sxs-lookup"><span data-stu-id="a6553-136">hello **vhds** panel lists hello disk drives held in hello container.</span></span> <span data-ttu-id="a6553-137">Klik op een van de schijven Hallo en klik op selecteren.</span><span class="sxs-lookup"><span data-stu-id="a6553-137">Click one of hello disks, and then click Select.</span></span>

    ![Schijfimage bieden voor virtuele machines-windows](./media/howto-attach-disk-windows-linux/existdiskvhds.png)

7. <span data-ttu-id="a6553-139">Hallo **bestaande schijf koppelen** Configuratiescherm opnieuw wordt weergegeven met Hallo-locatie met Hallo storage-account, de container en de geselecteerde harde schijf (vhd) tooadd toohello virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="a6553-139">hello **Attach existing disk** panel displays again, with hello location containing hello storage account, container, and selected hard disk (vhd) tooadd toohello virtual machine.</span></span>

  <span data-ttu-id="a6553-140">Stel **Hostcaching** toonone of Read only, klik vervolgens op OK.</span><span class="sxs-lookup"><span data-stu-id="a6553-140">Set **Host caching** toonone or Read only, then click OK.</span></span>

    ![Gegevensschijf gekoppeld](./media/howto-attach-disk-windows-linux/exisitingdisksuccessful.png)
