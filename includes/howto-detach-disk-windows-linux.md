<span data-ttu-id="04964-101">Wanneer u een gegevensschijf die is gekoppeld aan een virtuele machine niet meer nodig hebt, kunt u deze eenvoudig loskoppelen.</span><span class="sxs-lookup"><span data-stu-id="04964-101">When you no longer need a data disk that's attached to a virtual machine, you can easily detach it.</span></span> <span data-ttu-id="04964-102">Als u een schijf loskoppelt, wordt de schijf van de virtuele machine verwijderd, maar wordt de schijf niet verwijderd uit het Azure-opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="04964-102">Detaching a disk removes the disk from the virtual machine, but doesn't delete the disk from the Azure storage account.</span></span>

<span data-ttu-id="04964-103">Als u de bestaande gegevens op de schijf opnieuw wilt gebruiken, kunt u de schijf opnieuw koppelen aan dezelfde of een andere virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="04964-103">If you want to use the existing data on the disk again, you can reattach it to the same virtual machine, or another one.</span></span>  

> [!NOTE]
> <span data-ttu-id="04964-104">Als u de schijf van een besturingssysteem wilt loskoppelen, moet u eerst de virtuele machine verwijderen.</span><span class="sxs-lookup"><span data-stu-id="04964-104">To detach an operating system disk, you first need to delete the virtual machine.</span></span>
>

## <a name="find-the-disk"></a><span data-ttu-id="04964-105">De schijf vinden</span><span class="sxs-lookup"><span data-stu-id="04964-105">Find the disk</span></span>
<span data-ttu-id="04964-106">Als u de naam van de schijf niet weet of de schijf wilt controleren voordat u deze loskoppelt, volgt u deze stappen.</span><span class="sxs-lookup"><span data-stu-id="04964-106">If you don't know the name of the disk or want to verify it before you detach it, follow these steps.</span></span>

1. <span data-ttu-id="04964-107">Meld u aan bij de [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="04964-107">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="04964-108">Klik op **Virtuele machines** en selecteer vervolgens de toepasselijke VM.</span><span class="sxs-lookup"><span data-stu-id="04964-108">Click **Virtual Machines**, and then select the appropriate VM.</span></span>

3. <span data-ttu-id="04964-109">Klik onder **Instellingen** op **Schijven** aan de linkerkant van het dashboard van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="04964-109">Click **Disks** along the left edge of the virtual machine dashboard, under **Settings**.</span></span>

 <span data-ttu-id="04964-110">Het dashboard van de virtuele machine bevat de naam en het type van alle gekoppelde schijven.</span><span class="sxs-lookup"><span data-stu-id="04964-110">The virtual machine dashboard lists the name and type of all attached disks.</span></span> <span data-ttu-id="04964-111">Op dit scherm wordt bijvoorbeeld een virtuele machine weergegeven met een besturingssysteemschijf en een gegevensschijf:</span><span class="sxs-lookup"><span data-stu-id="04964-111">For example, this screen shows a virtual machine with one operating system (OS) disk and one data disk:</span></span>

    ![Gegevensschijf vinden](./media/howto-detach-disk-windows-linux/vmwithdisklist.png)

## <a name="detach-the-disk"></a><span data-ttu-id="04964-113">De schijf loskoppelen</span><span class="sxs-lookup"><span data-stu-id="04964-113">Detach the disk</span></span>
1. <span data-ttu-id="04964-114">Klik in Azure Portal op **Virtuele machines** en klik vervolgens op de naam van de virtuele machine die de gegevensschijf heeft die u wilt loskoppelen.</span><span class="sxs-lookup"><span data-stu-id="04964-114">From the Azure portal, click **Virtual Machines**, and then click the name of the virtual machine that has the data disk you want to detach.</span></span>

2. <span data-ttu-id="04964-115">Klik onder **Instellingen** op **Schijven** aan de linkerkant van het dashboard van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="04964-115">Click **Disks** along the left edge of the virtual machine dashboard, under **Settings**.</span></span>

3. <span data-ttu-id="04964-116">Klik op de schijf die u wilt loskoppelen.</span><span class="sxs-lookup"><span data-stu-id="04964-116">Click the disk you want to detach.</span></span>

  ![De schijf zoeken die u wilt loskoppelen](./media/howto-detach-disk-windows-linux/disklist.png)

4. <span data-ttu-id="04964-118">Klik vanuit de opdrachtbalk op **Loskoppelen**.</span><span class="sxs-lookup"><span data-stu-id="04964-118">From the command bar, click **Detach**.</span></span>

  ![De opdracht Loskoppelen vinden](./media/howto-detach-disk-windows-linux/diskdetachcommand.png)

5. <span data-ttu-id="04964-120">Klik in het bevestigingsvenster op **Ja** om de schijf los te koppelen.</span><span class="sxs-lookup"><span data-stu-id="04964-120">In the confirmation window, click **Yes** to detach the disk.</span></span>

  ![Het loskoppelen van de schijf bevestigen](./media/howto-detach-disk-windows-linux/confirmdetach.png)

<span data-ttu-id="04964-122">De schijf blijft in de opslag, maar is niet meer gekoppeld aan een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="04964-122">The disk remains in storage but is no longer attached to a virtual machine.</span></span>
