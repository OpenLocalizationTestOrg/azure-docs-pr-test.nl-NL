<!--author=alkohli last changed: 02/10/17-->

#### <a name="to-add-a-storsimple-backup-policy"></a><span data-ttu-id="7ff52-101">Een StorSimple-back-upbeleid toevoegen</span><span class="sxs-lookup"><span data-stu-id="7ff52-101">To add a StorSimple backup policy</span></span>

1. <span data-ttu-id="7ff52-102">Ga naar uw StorSimple-apparaat en klik op **Back-upbeleid**.</span><span class="sxs-lookup"><span data-stu-id="7ff52-102">Go to your StorSimple device and click **Backup policy**.</span></span>

2. <span data-ttu-id="7ff52-103">Klik op de blade **Back-upbeleid** op **+ Beleid toevoegen** vanuit de opdrachtbalk.</span><span class="sxs-lookup"><span data-stu-id="7ff52-103">In the **Backup policy** blade, click **+ Add policy** from the command bar.</span></span>
   
    ![Een back-upbeleid toevoegen](./media/storsimple-8000-add-backup-policy-u2/addbupol1.png)

3. <span data-ttu-id="7ff52-105">Voer de volgende stappen uit op de blade **Back-upbeleid maken**:</span><span class="sxs-lookup"><span data-stu-id="7ff52-105">In the **Create backup policy** blade, do the following steps:</span></span>
   
   1. <span data-ttu-id="7ff52-106">**Apparaat selecteren** wordt automatisch ingevuld op basis van het apparaat dat u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="7ff52-106">**Select device** is automatically populated based on the device you selected.</span></span>
   
   2. <span data-ttu-id="7ff52-107">Geef een **back-upbeleidsnaam** op van 3 tot 150 tekens.</span><span class="sxs-lookup"><span data-stu-id="7ff52-107">Specify a backup **Policy name** that contains between 3 and 150 characters.</span></span> <span data-ttu-id="7ff52-108">Als het beleid is gemaakt, kunt u het beleid niet hernoemen.</span><span class="sxs-lookup"><span data-stu-id="7ff52-108">Once the policy is created, you cannot rename the policy.</span></span>
       
   3. <span data-ttu-id="7ff52-109">Als u volumes wilt toewijzen aan dit back-upbeleid, selecteert u **Volumes toevoegen** en klikt u vervolgens vanuit de lijst in tabelvorm met volumesop het selectievakje uit om een of meer volumes toe te wijzen aan het back-upbeleid.</span><span class="sxs-lookup"><span data-stu-id="7ff52-109">To assign volumes to this backup policy, select **Add volumes** and then from the tabular listing of volumes, click the check box(es) to assign one or more volumes to this backup policy.</span></span>

       ![Een back-upbeleid toevoegen](./media/storsimple-8000-add-backup-policy-u2/addbupol2.png)

   4. <span data-ttu-id="7ff52-111">Als u een planning voor het back-upbeleid wilt definiëren, klikt u op **Eerste planning** en wijzigt u vervolgens de volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="7ff52-111">To define a schedule for this backup policy, click **First schedule** and then modify the following parameters:</span></span>

       ![Een back-upbeleid toevoegen](./media/storsimple-8000-add-backup-policy-u2/addbupol3.png)

       1. <span data-ttu-id="7ff52-113">Selecteer voor **Type momentopname** de optie **Cloud** of **Lokaal**.</span><span class="sxs-lookup"><span data-stu-id="7ff52-113">For **Snapshot type**, select **Cloud** or **Local**.</span></span>

       2. <span data-ttu-id="7ff52-114">Geef de frequentie van de back-ups aan (geef een aantal op en kies **Dagen** of **Weken** in de vervolgkeuzelijst).</span><span class="sxs-lookup"><span data-stu-id="7ff52-114">Indicate the frequency of backups (specify a number and then choose **Days** or **Weeks** from the drop-down list.</span></span>

       3. <span data-ttu-id="7ff52-115">Voer een bewaarschema in.</span><span class="sxs-lookup"><span data-stu-id="7ff52-115">Enter a retention schedule.</span></span>

       4. <span data-ttu-id="7ff52-116">Voer een begintijd en -datum in voor het back-upbeleid.</span><span class="sxs-lookup"><span data-stu-id="7ff52-116">Enter a time and date for the backup policy to begin.</span></span>

       5. <span data-ttu-id="7ff52-117">Klik op **OK** om de planning te definiëren.</span><span class="sxs-lookup"><span data-stu-id="7ff52-117">Click **OK** to define the schedule.</span></span>

   5. <span data-ttu-id="7ff52-118">Klik op **Maken** om een back-upbeleid te maken.</span><span class="sxs-lookup"><span data-stu-id="7ff52-118">Click **Create** to create a backup policy.</span></span>

       ![Een back-upbeleid toevoegen](./media/storsimple-8000-add-backup-policy-u2/addbupol4.png)
   
   6. <span data-ttu-id="7ff52-120">U krijgt een melding wanneer het back-upbeleid is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7ff52-120">You are notified when the backup policy is created.</span></span> <span data-ttu-id="7ff52-121">Het nieuwe beleid wordt in tabelvorm weergegeven op de blade **Back-upbeleid**.</span><span class="sxs-lookup"><span data-stu-id="7ff52-121">The newly added policy is displayed in the tabular view on the **Backup Policy** blade.</span></span>

       ![Een back-upbeleid toevoegen](./media/storsimple-8000-add-backup-policy-u2/addbupol7.png)

