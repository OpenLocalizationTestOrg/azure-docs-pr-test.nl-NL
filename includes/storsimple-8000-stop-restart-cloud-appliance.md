#### <a name="to-stop-and-start-a-cloud-appliance"></a><span data-ttu-id="f3910-101">Een cloudapparaat starten en stoppen</span><span class="sxs-lookup"><span data-stu-id="f3910-101">To stop and start a cloud appliance</span></span>

1. <span data-ttu-id="f3910-102">Als u een cloudapparaat wilt stoppen, gaat u naar de virtuele machine voor uw cloudapparaat.</span><span class="sxs-lookup"><span data-stu-id="f3910-102">To stop a cloud appliance, go to the VM for your cloud appliance.</span></span>
    <span data-ttu-id="f3910-103">![StorSimple-cloudapparaat - virtuele machine](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart1.png)</span><span class="sxs-lookup"><span data-stu-id="f3910-103">![StorSimple Cloud Appliance Virtual Machine](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart1.png)</span></span>

2. <span data-ttu-id="f3910-104">Klik vanuit de opdrachtbalk op **Stoppen**.</span><span class="sxs-lookup"><span data-stu-id="f3910-104">From the command bar, click **Stop**.</span></span>

    ![StorSimple-cloudapparaat - virtuele machine](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart2.png)

3. <span data-ttu-id="f3910-106">Klik op **Ja** als u om bevestiging wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="f3910-106">When prompted for confirmation, click **Yes**.</span></span>

    ![StorSimple-cloudapparaat - virtuele machine](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart3.png)

4. <span data-ttu-id="f3910-108">Wanneer u een virtuele machine stopt, wordt de toewijzing ervan opgeheven.</span><span class="sxs-lookup"><span data-stu-id="f3910-108">When you stop a VM, it gets deallocated.</span></span> <span data-ttu-id="f3910-109">Terwijl het cloudapparaat wordt gestopt, is de status ervan **Toewijzing ongedaan maken**.</span><span class="sxs-lookup"><span data-stu-id="f3910-109">While the cloud appliance is stopping, its status is **Deallocating**.</span></span> <span data-ttu-id="f3910-110">Nadat het cloudapparaat is gestopt, is de status ervan **Gestopt (toewijzing opgeheven)**.</span><span class="sxs-lookup"><span data-stu-id="f3910-110">After the cloud appliance is stopped, its status is **Stopped (deallocated)**.</span></span>

    ![StorSimple-cloudapparaat - virtuele machine](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart4.png)

5. <span data-ttu-id="f3910-112">Nadat een virtuele machine is gestopt, klikt u op **Starten** (knop wordt beschikbaar) om de virtuele machine te starten.</span><span class="sxs-lookup"><span data-stu-id="f3910-112">Once a VM is stopped, click **Start** (button becomes available) to start the VM.</span></span> <span data-ttu-id="f3910-113">Nadat het cloudapparaat is gestart, wordt de status ervan **Gestart**.</span><span class="sxs-lookup"><span data-stu-id="f3910-113">After the cloud appliance has started up, its status is **Started**.</span></span>

    ![StorSimple-cloudapparaat - virtuele machine](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart5.png)

<span data-ttu-id="f3910-115">Gebruik de volgende cmdlets om een cloudapparaat te stoppen en te starten.</span><span class="sxs-lookup"><span data-stu-id="f3910-115">Use the following cmdlets to stop and start a cloud appliance.</span></span>

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="to-restart-a-cloud-appliance"></a><span data-ttu-id="f3910-116">Een cloudapparaat opnieuw opstarten</span><span class="sxs-lookup"><span data-stu-id="f3910-116">To restart a cloud appliance</span></span>

<span data-ttu-id="f3910-117">Als u een cloudapparaat opnieuw wilt opstarten, gaat u naar de virtuele machine voor uw cloudapparaat.</span><span class="sxs-lookup"><span data-stu-id="f3910-117">To restart a cloud appliance, go to the VM for your cloud appliance.</span></span> <span data-ttu-id="f3910-118">Klik vanuit de opdrachtbalk op **Opnieuw starten**.</span><span class="sxs-lookup"><span data-stu-id="f3910-118">From the command bar, click **Restart**.</span></span> <span data-ttu-id="f3910-119">Bevestig het opnieuw starten als u daarom wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="f3910-119">When prompted, confirm the restart.</span></span> <span data-ttu-id="f3910-120">Wanneer het cloudapparaat gereed is voor gebruik, is de status **Wordt uitgevoerd**.</span><span class="sxs-lookup"><span data-stu-id="f3910-120">When the cloud appliance is ready for you to use, its status is **Running**.</span></span>

![StorSimple-cloudapparaat - virtuele machine](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart6.png)

<span data-ttu-id="f3910-122">Gebruik de volgende cmdlet om een cloudapparaat opnieuw op te starten.</span><span class="sxs-lookup"><span data-stu-id="f3910-122">Use the following cmdlet to restart a cloud appliance.</span></span>

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

