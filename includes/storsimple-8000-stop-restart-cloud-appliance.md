#### <a name="toostop-and-start-a-cloud-appliance"></a><span data-ttu-id="f7484-101">toostop en start een cloud-apparaat</span><span class="sxs-lookup"><span data-stu-id="f7484-101">toostop and start a cloud appliance</span></span>

1. <span data-ttu-id="f7484-102">toostop een cloud-apparaat gaat toohello VM voor uw toestel cloud.</span><span class="sxs-lookup"><span data-stu-id="f7484-102">toostop a cloud appliance, go toohello VM for your cloud appliance.</span></span>
    <span data-ttu-id="f7484-103">![StorSimple-cloudapparaat - virtuele machine](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart1.png)</span><span class="sxs-lookup"><span data-stu-id="f7484-103">![StorSimple Cloud Appliance Virtual Machine](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart1.png)</span></span>

2. <span data-ttu-id="f7484-104">Hallo opdrachtbalk en klik op **stoppen**.</span><span class="sxs-lookup"><span data-stu-id="f7484-104">From hello command bar, click **Stop**.</span></span>

    ![StorSimple-cloudapparaat - virtuele machine](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart2.png)

3. <span data-ttu-id="f7484-106">Klik op **Ja** als u om bevestiging wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="f7484-106">When prompted for confirmation, click **Yes**.</span></span>

    ![StorSimple-cloudapparaat - virtuele machine](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart3.png)

4. <span data-ttu-id="f7484-108">Wanneer u een virtuele machine stopt, wordt de toewijzing ervan opgeheven.</span><span class="sxs-lookup"><span data-stu-id="f7484-108">When you stop a VM, it gets deallocated.</span></span> <span data-ttu-id="f7484-109">Hoewel Hallo cloud toestel wordt gestopt, is het de status ervan **Deallocating**.</span><span class="sxs-lookup"><span data-stu-id="f7484-109">While hello cloud appliance is stopping, its status is **Deallocating**.</span></span> <span data-ttu-id="f7484-110">Nadat de Hallo cloud toestel is gestopt, wordt de status ervan is **gestopt (toewijzing opgeheven)**.</span><span class="sxs-lookup"><span data-stu-id="f7484-110">After hello cloud appliance is stopped, its status is **Stopped (deallocated)**.</span></span>

    ![StorSimple-cloudapparaat - virtuele machine](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart4.png)

5. <span data-ttu-id="f7484-112">Wanneer een virtuele machine is gestopt, klikt u op **Start** (knop beschikbaar) toostart Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="f7484-112">Once a VM is stopped, click **Start** (button becomes available) toostart hello VM.</span></span> <span data-ttu-id="f7484-113">Nadat het Hallo cloud toestel is gestart, is het de status ervan **gestart**.</span><span class="sxs-lookup"><span data-stu-id="f7484-113">After hello cloud appliance has started up, its status is **Started**.</span></span>

    ![StorSimple-cloudapparaat - virtuele machine](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart5.png)

<span data-ttu-id="f7484-115">Gebruik Hallo cmdlets toostop te volgen en starten van een cloud-apparaat.</span><span class="sxs-lookup"><span data-stu-id="f7484-115">Use hello following cmdlets toostop and start a cloud appliance.</span></span>

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="toorestart-a-cloud-appliance"></a><span data-ttu-id="f7484-116">toorestart een cloud-apparaat</span><span class="sxs-lookup"><span data-stu-id="f7484-116">toorestart a cloud appliance</span></span>

<span data-ttu-id="f7484-117">toorestart een cloud-apparaat gaat toohello VM voor uw toestel cloud.</span><span class="sxs-lookup"><span data-stu-id="f7484-117">toorestart a cloud appliance, go toohello VM for your cloud appliance.</span></span> <span data-ttu-id="f7484-118">Hallo opdrachtbalk en klik op **opnieuw**.</span><span class="sxs-lookup"><span data-stu-id="f7484-118">From hello command bar, click **Restart**.</span></span> <span data-ttu-id="f7484-119">Wanneer u wordt gevraagd, bevestig Hallo opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="f7484-119">When prompted, confirm hello restart.</span></span> <span data-ttu-id="f7484-120">Wanneer Hallo cloud toestel gereed voor u toouse is, de status ervan is **met**.</span><span class="sxs-lookup"><span data-stu-id="f7484-120">When hello cloud appliance is ready for you toouse, its status is **Running**.</span></span>

![StorSimple-cloudapparaat - virtuele machine](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart6.png)

<span data-ttu-id="f7484-122">Hallo volgende cmdlet toorestart een cloud-apparaat gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f7484-122">Use hello following cmdlet toorestart a cloud appliance.</span></span>

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

