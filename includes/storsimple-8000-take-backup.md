<!--author=alkohli last changed: 01/12/17-->

### <a name="tootake-a-backup"></a><span data-ttu-id="724ce-101">tootake een back-up</span><span class="sxs-lookup"><span data-stu-id="724ce-101">tootake a backup</span></span>

1. <span data-ttu-id="724ce-102">Ga tooyour Apparaatbeheer StorSimple-service.</span><span class="sxs-lookup"><span data-stu-id="724ce-102">Go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="724ce-103">Uit Hallo in tabelvorm aanbieding van apparaten, selecteren en klik op het apparaat en klik vervolgens op **alle instellingen**.</span><span class="sxs-lookup"><span data-stu-id="724ce-103">From hello tabular listing of devices, select and click your device and then click **All settings**.</span></span> <span data-ttu-id="724ce-104">In Hallo **instellingen** blade te gaan**instellingen > beheren > back-up maken van beleid**.</span><span class="sxs-lookup"><span data-stu-id="724ce-104">In hello **Settings** blade, go too**Settings > Manage > Backup policy**.</span></span>

    ![Back-upbeleid-toevoegen](./media/storsimple-8000-take-backup/step8takebu1.png)

2. <span data-ttu-id="724ce-106">In Hallo **back-up maken van beleid** blade, klikt u op **+ beleid toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="724ce-106">In hello **Backup policy** blade, click **+ Add policy**.</span></span>

    ![Back-upbeleid-toevoegen](./media/storsimple-8000-take-backup/step8takebu2.png)

3. <span data-ttu-id="724ce-108">In Hallo **back-upbeleid maken** blade, Geef een naam die tussen 3 en 150 tekens voor uw back-upbeleid bevat.</span><span class="sxs-lookup"><span data-stu-id="724ce-108">In hello **Create backup policy** blade, supply a name that contains between 3 and 150 characters for your backup policy.</span></span>

4. <span data-ttu-id="724ce-109">Selecteer Hallo volumes toobe back-up gemaakt.</span><span class="sxs-lookup"><span data-stu-id="724ce-109">Select hello volumes toobe backed up.</span></span> <span data-ttu-id="724ce-110">Als u meer dan één volume selecteert, zijn deze volumes gegroepeerde samen toocreate een crashconsistente back-up.</span><span class="sxs-lookup"><span data-stu-id="724ce-110">If you select more than one volume, these volumes are grouped together toocreate a crash-consistent backup.</span></span>

    ![Back-upbeleid-toevoegen](./media/storsimple-8000-take-backup/step8takebu4.png)

5. <span data-ttu-id="724ce-112">Op de blade **Eerste schema toevoegen**:</span><span class="sxs-lookup"><span data-stu-id="724ce-112">On **Add first schedule** blade:</span></span>

    1. <span data-ttu-id="724ce-113">Selecteer Hallo type back-up.</span><span class="sxs-lookup"><span data-stu-id="724ce-113">Select hello type of backup.</span></span> <span data-ttu-id="724ce-114">Selecteer **Lokale momentopname** voor sneller herstellen.</span><span class="sxs-lookup"><span data-stu-id="724ce-114">For faster restores, select **Local** snapshot.</span></span> <span data-ttu-id="724ce-115">Selecteer **Cloudmomentopname** voor gegevenstolerantie.</span><span class="sxs-lookup"><span data-stu-id="724ce-115">For data resiliency, select **Cloud** snapshot.</span></span>
    2. <span data-ttu-id="724ce-116">Geef de back-upfrequentie Hallo in minuten, uren, dagen of weken.</span><span class="sxs-lookup"><span data-stu-id="724ce-116">Specify hello backup frequency in minutes, hours, days, or weeks.</span></span>
    3. <span data-ttu-id="724ce-117">Selecteer een bewaartijd.</span><span class="sxs-lookup"><span data-stu-id="724ce-117">Select a retention time.</span></span> <span data-ttu-id="724ce-118">Hallo bewaren keuzen, is afhankelijk van de back-upfrequentie Hallo.</span><span class="sxs-lookup"><span data-stu-id="724ce-118">hello retention choices depend on hello backup frequency.</span></span> <span data-ttu-id="724ce-119">Bijvoorbeeld: voor een dagelijkse beleid Hallo bewaren kan worden opgegeven in weken, terwijl de bewaarperiode voor een maandelijkse beleid in maanden.</span><span class="sxs-lookup"><span data-stu-id="724ce-119">For example, for a daily policy, hello retention can be specified in weeks, whereas retention for a monthly policy is in months.</span></span>
    4. <span data-ttu-id="724ce-120">Selecteer Hallo datum en tijd van de back-upbeleid hello wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="724ce-120">Select hello starting time and date for hello backup policy.</span></span>
    5. <span data-ttu-id="724ce-121">Klik op **OK** toocreate Hallo back-upbeleid.</span><span class="sxs-lookup"><span data-stu-id="724ce-121">Click **OK** toocreate hello backup policy.</span></span>

        ![Back-upbeleid-toevoegen](./media/storsimple-8000-take-backup/step8takebu5.png) 

6. <span data-ttu-id="724ce-123">Klik op **maken** toostart Hallo back-upbeleid maken.</span><span class="sxs-lookup"><span data-stu-id="724ce-123">Click **Create** toostart hello backup policy creation.</span></span> <span data-ttu-id="724ce-124">U wordt gewaarschuwd wanneer de back-upbeleid Hallo is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="724ce-124">You are notified when hello backup policy is successfully created.</span></span> <span data-ttu-id="724ce-125">Hallo-lijst met back-upbeleid is tevens bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="724ce-125">hello list of backup policies is also updated.</span></span>
      
      ![Back-upbeleid-toevoegen](./media/storsimple-8000-take-backup/step8takebu9.png)
      
      <span data-ttu-id="724ce-127">U hebt nu een back-upbeleid voor geplande back-ups van uw volumegegevens.</span><span class="sxs-lookup"><span data-stu-id="724ce-127">You now have a backup policy that creates scheduled backups of your volume data.</span></span>




