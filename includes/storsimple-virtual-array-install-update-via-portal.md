<!--author=alkohli last changed: 11/07/16 -->

#### <a name="to-install-updates-via-the-azure-portal"></a><span data-ttu-id="8e4e8-101">Updates installeren via Azure Portal</span><span class="sxs-lookup"><span data-stu-id="8e4e8-101">To install updates via the Azure portal</span></span>

1. <span data-ttu-id="8e4e8-102">Ga naar uw StorSimple Device Manager en selecteer **Apparaten**.</span><span class="sxs-lookup"><span data-stu-id="8e4e8-102">Go to your StorSimple Device Manager and select **Devices**.</span></span> <span data-ttu-id="8e4e8-103">Selecteer in de lijst met apparaten die zijn verbonden met uw service, het apparaat dat u wilt bijwerken.</span><span class="sxs-lookup"><span data-stu-id="8e4e8-103">From the list of devices connected to your service, select and click the device you want to update.</span></span> 

    ![apparaat bijwerken](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate1m.png) 

2. <span data-ttu-id="8e4e8-105">Klik op de blade **Instellingen** op **Apparaatupdates**.</span><span class="sxs-lookup"><span data-stu-id="8e4e8-105">In the **Settings** blade, click **Device updates**.</span></span> 

    ![apparaat bijwerken](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate2m.png)  

3. <span data-ttu-id="8e4e8-107">Als er software-updates beschikbaar zijn, wordt er een bericht weergegeven.</span><span class="sxs-lookup"><span data-stu-id="8e4e8-107">You see a message if the software updates are available.</span></span> <span data-ttu-id="8e4e8-108">U kunt ook op **Scannen** klikken om naar updates te zoeken.</span><span class="sxs-lookup"><span data-stu-id="8e4e8-108">To check for updates, you can also click **Scan**.</span></span>

    ![apparaat bijwerken](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate3m.png)

    <span data-ttu-id="8e4e8-110">U ontvangt een melding wanneer de scan wordt gestart en wanneer deze is voltooid.</span><span class="sxs-lookup"><span data-stu-id="8e4e8-110">You will be notified when the scan starts and completes successfully.</span></span>

    ![apparaat bijwerken](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate5m.png)

4. <span data-ttu-id="8e4e8-112">Nadat de updates zijn gescand, klikt u op **Updates downloaden**.</span><span class="sxs-lookup"><span data-stu-id="8e4e8-112">Once the updates are scanned, click **Download updates**.</span></span> 

    ![apparaat bijwerken](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate6m.png)

5. <span data-ttu-id="8e4e8-114">Controleer op de blade **Nieuwe updates** de informatie die u nodig hebt om de installatie te bevestigen nadat de updates zijn gedownload.</span><span class="sxs-lookup"><span data-stu-id="8e4e8-114">In the **New updates** blade, review the information that after the updates are downloaded, you need to confirm the installation.</span></span> <span data-ttu-id="8e4e8-115">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="8e4e8-115">Click **OK**.</span></span>

    ![apparaat bijwerken](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate7m.png)

6. <span data-ttu-id="8e4e8-117">U ontvangt een melding wanneer de upload wordt gestart en wanneer deze is voltooid.</span><span class="sxs-lookup"><span data-stu-id="8e4e8-117">You are notified when the upload starts and completes successfully.</span></span>

     ![apparaat bijwerken](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate8m.png)

5. <span data-ttu-id="8e4e8-119">Klik op de blade **Apparaatupdates** op **Installeren**.</span><span class="sxs-lookup"><span data-stu-id="8e4e8-119">In the **Device updates** blade, click **Install**.</span></span>

     ![apparaat bijwerken](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate11m.png)   

6. <span data-ttu-id="8e4e8-121">Op de blade **Nieuwe updates** krijgt u een waarschuwing dat de update verstorend is.</span><span class="sxs-lookup"><span data-stu-id="8e4e8-121">In the **New updates** blade, you are warned that the update is disruptive.</span></span> <span data-ttu-id="8e4e8-122">Als de virtuele matrix een apparaat met een enkel knooppunt is, wordt het apparaat opnieuw opgestart nadat het is bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="8e4e8-122">As virtual array is a single node device, the device restarts after it is updated.</span></span> <span data-ttu-id="8e4e8-123">Dit verstoort alle actieve IO.</span><span class="sxs-lookup"><span data-stu-id="8e4e8-123">This disrupts any IO in progress.</span></span> <span data-ttu-id="8e4e8-124">Klik op **OK** om de updates te installeren.</span><span class="sxs-lookup"><span data-stu-id="8e4e8-124">Click **OK** to install the updates.</span></span> 

    ![apparaat bijwerken](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate12m.png) 

7. <span data-ttu-id="8e4e8-126">U ontvangt een melding wanneer de installatietaak wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="8e4e8-126">You are notified when the install job starts.</span></span> 

    ![apparaat bijwerken](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate13m.png)

8.  <span data-ttu-id="8e4e8-128">Nadat de installatietaak is voltooid, klikt u op de koppeling **Taak weergeven** op de blade **Apparaatupdates** om de installatie te controleren.</span><span class="sxs-lookup"><span data-stu-id="8e4e8-128">After the install job completes successfully, click **View Job** link in the **Device updates** blade to monitor the installation.</span></span> 

    ![apparaat bijwerken](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate15m.png)

    <span data-ttu-id="8e4e8-130">Hiermee gaat u naar de blade **Updates installeren**.</span><span class="sxs-lookup"><span data-stu-id="8e4e8-130">This takes you to the **Install Updates** blade.</span></span> <span data-ttu-id="8e4e8-131">Hier kunt u gedetailleerde informatie over de taak weergeven.</span><span class="sxs-lookup"><span data-stu-id="8e4e8-131">You can view detailed information about the job here.</span></span>

    ![apparaat bijwerken](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate16m.png)

9. <span data-ttu-id="8e4e8-133">Nadat de updates zijn geïnstalleerd, ziet u een bericht met het oog op de blade van de updates apparaat.</span><span class="sxs-lookup"><span data-stu-id="8e4e8-133">After the updates are successfully installed, you see a message to this effect in the Device updates blade.</span></span> <span data-ttu-id="8e4e8-134">Versie van de software ook wijzigingen in **10.0.10288.0**.</span><span class="sxs-lookup"><span data-stu-id="8e4e8-134">The software version also changes to **10.0.10288.0**.</span></span> 

    ![apparaat bijwerken](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate17m.png)