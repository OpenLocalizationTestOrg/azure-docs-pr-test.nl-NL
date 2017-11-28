<!--author=alkohli last changed: 01/12/17-->

### <a name="to-take-a-backup"></a><span data-ttu-id="04ded-101">Een back-up maken</span><span class="sxs-lookup"><span data-stu-id="04ded-101">To take a backup</span></span>

1. <span data-ttu-id="04ded-102">Ga naar uw StorSimple-apparaatbeheerservice.</span><span class="sxs-lookup"><span data-stu-id="04ded-102">Go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="04ded-103">Selecteer uw apparaat in de lijst in tabelvorm met apparaten en klik hierop. Klik daarna op **Alle instellingen**.</span><span class="sxs-lookup"><span data-stu-id="04ded-103">From the tabular listing of devices, select and click your device and then click **All settings**.</span></span> <span data-ttu-id="04ded-104">Ga op de blade **Instellingen** naar **Instellingen > Beheren > Back-upbeleid**.</span><span class="sxs-lookup"><span data-stu-id="04ded-104">In the **Settings** blade, go to **Settings > Manage > Backup policy**.</span></span>

    ![Back-upbeleid-toevoegen](./media/storsimple-8000-take-backup/step8takebu1.png)

2. <span data-ttu-id="04ded-106">Klik op de blade **Back-upbeleid** op **+ Beleid toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="04ded-106">In the **Backup policy** blade, click **+ Add policy**.</span></span>

    ![Back-upbeleid-toevoegen](./media/storsimple-8000-take-backup/step8takebu2.png)

3. <span data-ttu-id="04ded-108">Geef op de blade **Back-upbeleid maken** een naam op voor uw back-upbeleid die tussen de 3 en 150 tekens lang is.</span><span class="sxs-lookup"><span data-stu-id="04ded-108">In the **Create backup policy** blade, supply a name that contains between 3 and 150 characters for your backup policy.</span></span>

4. <span data-ttu-id="04ded-109">Selecteer de volumes waarvan u een back-up wilt maken.</span><span class="sxs-lookup"><span data-stu-id="04ded-109">Select the volumes to be backed up.</span></span> <span data-ttu-id="04ded-110">Als u meer dan één volume selecteert, worden deze volumes samen gegroepeerd om zo een crashconsistente back-up te maken.</span><span class="sxs-lookup"><span data-stu-id="04ded-110">If you select more than one volume, these volumes are grouped together to create a crash-consistent backup.</span></span>

    ![Back-upbeleid-toevoegen](./media/storsimple-8000-take-backup/step8takebu4.png)

5. <span data-ttu-id="04ded-112">Op de blade **Eerste schema toevoegen**:</span><span class="sxs-lookup"><span data-stu-id="04ded-112">On **Add first schedule** blade:</span></span>

    1. <span data-ttu-id="04ded-113">Selecteer het type back-up.</span><span class="sxs-lookup"><span data-stu-id="04ded-113">Select the type of backup.</span></span> <span data-ttu-id="04ded-114">Selecteer **Lokale momentopname** voor sneller herstellen.</span><span class="sxs-lookup"><span data-stu-id="04ded-114">For faster restores, select **Local** snapshot.</span></span> <span data-ttu-id="04ded-115">Selecteer **Cloudmomentopname** voor gegevenstolerantie.</span><span class="sxs-lookup"><span data-stu-id="04ded-115">For data resiliency, select **Cloud** snapshot.</span></span>
    2. <span data-ttu-id="04ded-116">Geef de back-upfrequentie op in minuten, uren, dagen of weken.</span><span class="sxs-lookup"><span data-stu-id="04ded-116">Specify the backup frequency in minutes, hours, days, or weeks.</span></span>
    3. <span data-ttu-id="04ded-117">Selecteer een bewaartijd.</span><span class="sxs-lookup"><span data-stu-id="04ded-117">Select a retention time.</span></span> <span data-ttu-id="04ded-118">Hoe lang deze moet zijn, hangt af van hoe vaak een back-up wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="04ded-118">The retention choices depend on the backup frequency.</span></span> <span data-ttu-id="04ded-119">Als dagelijks een back-up wordt uitgevoerd, kunt u de bewaartijd instellen op weken. Als maandelijks een back-up wordt gemaakt, kunt u de bewaartijd instellen op maanden.</span><span class="sxs-lookup"><span data-stu-id="04ded-119">For example, for a daily policy, the retention can be specified in weeks, whereas retention for a monthly policy is in months.</span></span>
    4. <span data-ttu-id="04ded-120">Selecteer de begintijd en -datum voor het back-upbeleid.</span><span class="sxs-lookup"><span data-stu-id="04ded-120">Select the starting time and date for the backup policy.</span></span>
    5. <span data-ttu-id="04ded-121">Klik op **OK** om het back-upbeleid te maken.</span><span class="sxs-lookup"><span data-stu-id="04ded-121">Click **OK** to create the backup policy.</span></span>

        ![Back-upbeleid-toevoegen](./media/storsimple-8000-take-backup/step8takebu5.png) 

6. <span data-ttu-id="04ded-123">Klik op **Maken** om te beginnen met het maken van het back-upbeleid.</span><span class="sxs-lookup"><span data-stu-id="04ded-123">Click **Create** to start the backup policy creation.</span></span> <span data-ttu-id="04ded-124">U krijgt een melding wanneer het back-upbeleid is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="04ded-124">You are notified when the backup policy is successfully created.</span></span> <span data-ttu-id="04ded-125">De lijst met back-upbeleidsregels wordt ook bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="04ded-125">The list of backup policies is also updated.</span></span>
      
      ![Back-upbeleid-toevoegen](./media/storsimple-8000-take-backup/step8takebu9.png)
      
      <span data-ttu-id="04ded-127">U hebt nu een back-upbeleid voor geplande back-ups van uw volumegegevens.</span><span class="sxs-lookup"><span data-stu-id="04ded-127">You now have a backup policy that creates scheduled backups of your volume data.</span></span>




