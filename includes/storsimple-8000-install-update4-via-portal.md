<!--author=alkohli last changed: 07/07/17-->

#### <a name="tooinstall-an-update-from-hello-azure-portal"></a><span data-ttu-id="b3e17-101">tooinstall een update van hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="b3e17-101">tooinstall an update from hello Azure portal</span></span>

1. <span data-ttu-id="b3e17-102">Selecteer op de pagina StorSimple hello, uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="b3e17-102">On hello StorSimple service page, select your device.</span></span>

    ![Selecteer het apparaat](./media/storsimple-8000-install-update4-via-portal/update1.png)

2. <span data-ttu-id="b3e17-104">Navigeer te**apparaatinstellingen** > **apparaatupdates**.</span><span class="sxs-lookup"><span data-stu-id="b3e17-104">Navigate too**Device settings** > **Device updates**.</span></span>

    ![Klik op apparaat-updates](./media/storsimple-8000-install-update4-via-portal/update2.png)

2. <span data-ttu-id="b3e17-106">Er wordt een melding weergegeven als er nieuwe updates beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="b3e17-106">A notification appears if new updates are available.</span></span> <span data-ttu-id="b3e17-107">U kunt ook in Hallo **apparaatupdates** blade, klikt u op **Updates zoeken**.</span><span class="sxs-lookup"><span data-stu-id="b3e17-107">Alternatively, in hello **Device updates** blade, click **Scan Updates**.</span></span> <span data-ttu-id="b3e17-108">Een taak gemaakt tooscan naar beschikbare updates.</span><span class="sxs-lookup"><span data-stu-id="b3e17-108">A job is created tooscan for available updates.</span></span> <span data-ttu-id="b3e17-109">U wordt gewaarschuwd wanneer het Hallo-taak is voltooid.</span><span class="sxs-lookup"><span data-stu-id="b3e17-109">You are notified when hello job completes successfully.</span></span>

    ![Klik op apparaat-updates](./media/storsimple-8000-install-update4-via-portal/update3.png)

3. <span data-ttu-id="b3e17-111">U wordt aangeraden de releaseopmerkingen Hallo te controleren voordat u een update op uw apparaat toepassen.</span><span class="sxs-lookup"><span data-stu-id="b3e17-111">We recommend that you review hello release notes before you apply an update on your device.</span></span> <span data-ttu-id="b3e17-112">tooapply updates, klikt u op **updates installeren**.</span><span class="sxs-lookup"><span data-stu-id="b3e17-112">tooapply updates, click **Install updates**.</span></span> <span data-ttu-id="b3e17-113">In Hallo **bevestigen regelmatig updates** blade revisie Hallo vereisten toocomplete voordat u updates toepassen.</span><span class="sxs-lookup"><span data-stu-id="b3e17-113">In hello **Confirm regular updates** blade, review hello prerequisites toocomplete before you apply updates.</span></span> <span data-ttu-id="b3e17-114">Selecteer Hallo selectievakje tooindicate dat u gereed tooupdate Hallo apparaat en klik vervolgens op **installeren**.</span><span class="sxs-lookup"><span data-stu-id="b3e17-114">Select hello checkbox tooindicate that you are ready tooupdate hello device and then click **Install**.</span></span>

    ![Klik op apparaat-updates](./media/storsimple-8000-install-update4-via-portal/update4.png)

6. <span data-ttu-id="b3e17-116">Er wordt een reeks vereiste controles gestart.</span><span class="sxs-lookup"><span data-stu-id="b3e17-116">A set of prerequisite checks starts.</span></span> <span data-ttu-id="b3e17-117">Deze controles zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="b3e17-117">These checks include:</span></span>
   
   * <span data-ttu-id="b3e17-118">**Controller statuscontroles** tooverify dat beide apparaatcontrollers Hallo in orde en online zijn.</span><span class="sxs-lookup"><span data-stu-id="b3e17-118">**Controller health checks** tooverify that both hello device controllers are healthy and online.</span></span>
   * <span data-ttu-id="b3e17-119">**Hardware-onderdeel statuscontroles** tooverify dat alle hardware-onderdelen op uw StorSimple-apparaat Hallo zijn in orde.</span><span class="sxs-lookup"><span data-stu-id="b3e17-119">**Hardware component health checks** tooverify that all hello hardware components on your StorSimple device are healthy.</span></span>
   * <span data-ttu-id="b3e17-120">**DATA 0 controleert** tooverify dat DATA 0 is ingeschakeld op uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="b3e17-120">**DATA 0 checks** tooverify that DATA 0 is enabled on your device.</span></span> <span data-ttu-id="b3e17-121">Als deze interface niet is ingeschakeld, schakelt u deze in en probeert u het vervolgens opnieuw.</span><span class="sxs-lookup"><span data-stu-id="b3e17-121">If this interface is not enabled, you must enable it and then retry.</span></span>

    <span data-ttu-id="b3e17-122">Hallo-update is gedownload en wordt alleen geïnstalleerd als alle Hallo controles zijn voltooid.</span><span class="sxs-lookup"><span data-stu-id="b3e17-122">hello update is downloaded and installed only if all hello checks are successfully completed.</span></span> <span data-ttu-id="b3e17-123">U wordt gewaarschuwd wanneer Hallo controles uitgevoerd worden.</span><span class="sxs-lookup"><span data-stu-id="b3e17-123">You are notified when hello checks are in progress.</span></span> <span data-ttu-id="b3e17-124">Als Hallo prechecks mislukken, vervolgens krijgt u met de Hallo oorzaken.</span><span class="sxs-lookup"><span data-stu-id="b3e17-124">If hello prechecks fail, then you will be provided with hello reasons for failure.</span></span> <span data-ttu-id="b3e17-125">Deze problemen op te lossen en probeer vervolgens Hallo opnieuw.</span><span class="sxs-lookup"><span data-stu-id="b3e17-125">Address those issues and then retry hello operation.</span></span> <span data-ttu-id="b3e17-126">Mogelijk moet u toocontact Microsoft Support als u deze problemen door u zelf kan niet oplossen.</span><span class="sxs-lookup"><span data-stu-id="b3e17-126">You may need toocontact Microsoft Support if you cannot address these issues by yourself.</span></span>

7. <span data-ttu-id="b3e17-127">Nadat het Hallo prechecks zijn voltooid, wordt een updatetaak gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b3e17-127">After hello prechecks are successfully completed, an update job is created.</span></span> <span data-ttu-id="b3e17-128">U wordt gewaarschuwd wanneer de bijwerktaak Hallo is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b3e17-128">You are notified when hello update job is successfully created.</span></span>
   
    ![Maken van bijwerktaak](./media/storsimple-8000-install-update4-via-portal/update6.png)
   
    <span data-ttu-id="b3e17-130">Hallo-update wordt vervolgens toegepast op uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="b3e17-130">hello update is then applied on your device.</span></span>

9. <span data-ttu-id="b3e17-131">Hallo update duurt enkele uren toocomplete.</span><span class="sxs-lookup"><span data-stu-id="b3e17-131">hello update takes a few hours toocomplete.</span></span> <span data-ttu-id="b3e17-132">Hallo updatetaak te selecteren en klik op **Details** tooview Hallo details van de taak Hallo op elk gewenst moment.</span><span class="sxs-lookup"><span data-stu-id="b3e17-132">Select hello update job and click **Details** tooview hello details of hello job at any time.</span></span>

    ![Maken van bijwerktaak](./media/storsimple-8000-install-update4-via-portal/update8.png)

     <span data-ttu-id="b3e17-134">U kunt ook bewaken Hallo voortgang van de taak voor het bijwerken van Hallo **apparaatinstellingen > taken**.</span><span class="sxs-lookup"><span data-stu-id="b3e17-134">You can also monitor hello progress of hello update job from **Device settings > Jobs**.</span></span> <span data-ttu-id="b3e17-135">Op Hallo **taken** , ziet u Hallo voortgang bijwerken.</span><span class="sxs-lookup"><span data-stu-id="b3e17-135">On hello **Jobs** blade, you can see hello update progress.</span></span>

     ![Maken van bijwerktaak](./media/storsimple-8000-install-update4-via-portal/update7.png)

10. <span data-ttu-id="b3e17-137">Nadat het Hallo-taak is voltooid, gaat u toohello **apparaatinstellingen > apparaatupdates**.</span><span class="sxs-lookup"><span data-stu-id="b3e17-137">After hello job is complete, navigate toohello **Device settings > Device updates**.</span></span> <span data-ttu-id="b3e17-138">Hallo softwareversie moet nu worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="b3e17-138">hello software version should now be updated.</span></span>

    ![Maken van bijwerktaak](./media/storsimple-8000-install-update4-via-portal/update9.png)

