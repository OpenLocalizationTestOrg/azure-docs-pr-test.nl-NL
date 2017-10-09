<span data-ttu-id="80404-101">Wanneer u een gegevensschijf die is aangesloten tooa virtuele machine niet meer nodig hebt, kunt u deze eenvoudig loskoppelen.</span><span class="sxs-lookup"><span data-stu-id="80404-101">When you no longer need a data disk that's attached tooa virtual machine, you can easily detach it.</span></span> <span data-ttu-id="80404-102">Een schijf wordt losgekoppeld Hallo schijf verwijdert uit Hallo virtuele machine, maar niet Hallo schijf verwijderen uit hello Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="80404-102">Detaching a disk removes hello disk from hello virtual machine, but doesn't delete hello disk from hello Azure storage account.</span></span>

<span data-ttu-id="80404-103">Als u toouse Hallo bestaande gegevens op Hallo schijf opnieuw wilt, u kunt opnieuw het toohello dezelfde virtuele machine of een andere naam.</span><span class="sxs-lookup"><span data-stu-id="80404-103">If you want toouse hello existing data on hello disk again, you can reattach it toohello same virtual machine, or another one.</span></span>  

> [!NOTE]
> <span data-ttu-id="80404-104">toodetach schijf van een besturingssysteem, moet u eerst toodelete Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="80404-104">toodetach an operating system disk, you first need toodelete hello virtual machine.</span></span>
>

## <a name="find-hello-disk"></a><span data-ttu-id="80404-105">Hallo schijf gevonden</span><span class="sxs-lookup"><span data-stu-id="80404-105">Find hello disk</span></span>
<span data-ttu-id="80404-106">Als u de naam van de Hallo van schijf Hallo of tooverify wilt niet weet het voordat u deze loskoppelen, als volgt te werk.</span><span class="sxs-lookup"><span data-stu-id="80404-106">If you don't know hello name of hello disk or want tooverify it before you detach it, follow these steps.</span></span>

1. <span data-ttu-id="80404-107">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="80404-107">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="80404-108">Klik op **virtuele Machines**, en vervolgens selecteert Hallo juiste VM.</span><span class="sxs-lookup"><span data-stu-id="80404-108">Click **Virtual Machines**, and then select hello appropriate VM.</span></span>

3. <span data-ttu-id="80404-109">Klik op **schijven** langs Hallo de linkerrand van dashboard van de virtuele machine hello, onder **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="80404-109">Click **Disks** along hello left edge of hello virtual machine dashboard, under **Settings**.</span></span>

 <span data-ttu-id="80404-110">Hallo virtuele machine dashboard geeft een lijst Hallo naam en type van alle gekoppelde schijven.</span><span class="sxs-lookup"><span data-stu-id="80404-110">hello virtual machine dashboard lists hello name and type of all attached disks.</span></span> <span data-ttu-id="80404-111">Op dit scherm wordt bijvoorbeeld een virtuele machine weergegeven met een besturingssysteemschijf en een gegevensschijf:</span><span class="sxs-lookup"><span data-stu-id="80404-111">For example, this screen shows a virtual machine with one operating system (OS) disk and one data disk:</span></span>

    ![Gegevensschijf vinden](./media/howto-detach-disk-windows-linux/vmwithdisklist.png)

## <a name="detach-hello-disk"></a><span data-ttu-id="80404-113">Ontkoppel de schijf Hallo</span><span class="sxs-lookup"><span data-stu-id="80404-113">Detach hello disk</span></span>
1. <span data-ttu-id="80404-114">Hallo Azure-portal, klik op **virtuele Machines**, en klik vervolgens op Hallo-naam van Hallo virtuele machine die Hallo gegevensschijf gewenste toodetach heeft.</span><span class="sxs-lookup"><span data-stu-id="80404-114">From hello Azure portal, click **Virtual Machines**, and then click hello name of hello virtual machine that has hello data disk you want toodetach.</span></span>

2. <span data-ttu-id="80404-115">Klik op **schijven** langs Hallo de linkerrand van dashboard van de virtuele machine hello, onder **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="80404-115">Click **Disks** along hello left edge of hello virtual machine dashboard, under **Settings**.</span></span>

3. <span data-ttu-id="80404-116">Klik op de gewenste toodetach Hallo-schijf.</span><span class="sxs-lookup"><span data-stu-id="80404-116">Click hello disk you want toodetach.</span></span>

  ![Hallo schijf toodetach identificeren](./media/howto-detach-disk-windows-linux/disklist.png)

4. <span data-ttu-id="80404-118">Hallo opdrachtbalk en klik op **Detach**.</span><span class="sxs-lookup"><span data-stu-id="80404-118">From hello command bar, click **Detach**.</span></span>

  ![Zoek Hallo loskoppelen van de opdracht](./media/howto-detach-disk-windows-linux/diskdetachcommand.png)

5. <span data-ttu-id="80404-120">Klik in het bevestigingsvenster hello, **Ja** toodetach Hallo schijf.</span><span class="sxs-lookup"><span data-stu-id="80404-120">In hello confirmation window, click **Yes** toodetach hello disk.</span></span>

  ![Loskoppelen Hallo schijf bevestigen](./media/howto-detach-disk-windows-linux/confirmdetach.png)

<span data-ttu-id="80404-122">Hallo schijf blijft in de opslag, maar is niet langer gekoppelde tooa virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="80404-122">hello disk remains in storage but is no longer attached tooa virtual machine.</span></span>
