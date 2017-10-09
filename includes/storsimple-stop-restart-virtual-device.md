#### <a name="toostop-and-start-a-virtual-device"></a><span data-ttu-id="ce0eb-101">toostop en start een virtueel apparaat</span><span class="sxs-lookup"><span data-stu-id="ce0eb-101">toostop and start a virtual device</span></span>
<span data-ttu-id="ce0eb-102">een virtueel apparaat toostop Klik op de naam en klik vervolgens op **afsluiten**.</span><span class="sxs-lookup"><span data-stu-id="ce0eb-102">toostop a virtual device, click its name, and then click **Shutdown**.</span></span> <span data-ttu-id="ce0eb-103">Terwijl het virtuele apparaat hello wordt afgesloten, wordt de status ervan is **stoppen**.</span><span class="sxs-lookup"><span data-stu-id="ce0eb-103">While hello virtual device is shutting down, its status is **Stopping**.</span></span> <span data-ttu-id="ce0eb-104">Nadat het virtuele apparaat Hallo is gestopt, wordt de status ervan is **gestopt**.</span><span class="sxs-lookup"><span data-stu-id="ce0eb-104">After hello virtual device is stopped, its status is **Stopped**.</span></span>

<span data-ttu-id="ce0eb-105">Gebruik Hallo cmdlets toostop te volgen en een virtueel apparaat starten.</span><span class="sxs-lookup"><span data-stu-id="ce0eb-105">Use hello following cmdlets toostop and start a virtual device.</span></span>

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="toorestart-a-virtual-device"></a><span data-ttu-id="ce0eb-106">een virtueel apparaat toorestart</span><span class="sxs-lookup"><span data-stu-id="ce0eb-106">toorestart a virtual device</span></span>
<span data-ttu-id="ce0eb-107">Wanneer een virtueel apparaat wordt uitgevoerd en u wilt toorestart, klik op de naam en klik vervolgens op **opnieuw**.</span><span class="sxs-lookup"><span data-stu-id="ce0eb-107">When a virtual device is running and you want toorestart it, click its name, and then click **Restart**.</span></span> <span data-ttu-id="ce0eb-108">Terwijl Hallo virtueel apparaat opnieuw wordt opgestart, wordt de status ervan is **wordt opnieuw gestart**.</span><span class="sxs-lookup"><span data-stu-id="ce0eb-108">While hello virtual device is restarting, its status is **Restarting**.</span></span> <span data-ttu-id="ce0eb-109">Wanneer het virtuele apparaat Hallo gereed voor u toouse is, de status ervan is **met**.</span><span class="sxs-lookup"><span data-stu-id="ce0eb-109">When hello virtual device is ready for you toouse, its status is **Running**.</span></span>

<span data-ttu-id="ce0eb-110">Gebruik Hallo cmdlet toorestart een virtueel apparaat te volgen.</span><span class="sxs-lookup"><span data-stu-id="ce0eb-110">Use hello following cmdlet toorestart a virtual device.</span></span>

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

