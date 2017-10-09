<!--author=SharS last changed: 9/17/15-->

#### <a name="tooinstall-maintenance-mode-hotfixes-via-windows-powershell-for-storsimple"></a><span data-ttu-id="9b5a1-101">tooinstall onderhoud modus hotfixes via Windows PowerShell voor StorSimple</span><span class="sxs-lookup"><span data-stu-id="9b5a1-101">tooinstall Maintenance mode hotfixes via Windows PowerShell for StorSimple</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9b5a1-102">In de onderhoudsmodus, tooapply Hallo hotfix eerst op één domeincontroller moet en klik vervolgens op Hallo andere domeincontroller.</span><span class="sxs-lookup"><span data-stu-id="9b5a1-102">In Maintenance mode, you need tooapply hello hotfix first on one controller and then on hello other controller.</span></span>
> 
> 

1. <span data-ttu-id="9b5a1-103">Hallo-apparaat in de onderhoudsmodus plaatsen.</span><span class="sxs-lookup"><span data-stu-id="9b5a1-103">Place hello device into Maintenance mode.</span></span> <span data-ttu-id="9b5a1-104">Zie [stap 2: Voer onderhoudsmodus](../articles/storsimple/storsimple-update-device.md#step2) voor instructies over het tooenter-onderhoudsmodus.</span><span class="sxs-lookup"><span data-stu-id="9b5a1-104">See [Step 2: Enter Maintenance mode](../articles/storsimple/storsimple-update-device.md#step2) for instructions on how tooenter Maintenance mode.</span></span>
2. <span data-ttu-id="9b5a1-105">tooapply hello hotfix, type:</span><span class="sxs-lookup"><span data-stu-id="9b5a1-105">tooapply hello hotfix, type:</span></span>
   
     `Start-HcsHotfix` 
3. <span data-ttu-id="9b5a1-106">Als u wordt gevraagd, geeft u Hallo pad toohello gedeelde netwerkmap waarin Hallo hotfix-bestanden.</span><span class="sxs-lookup"><span data-stu-id="9b5a1-106">When prompted, supply hello path toohello network shared folder that contains hello hotfix files.</span></span>
4. <span data-ttu-id="9b5a1-107">U wordt gevraagd om bevestiging.</span><span class="sxs-lookup"><span data-stu-id="9b5a1-107">You will be prompted for confirmation.</span></span> <span data-ttu-id="9b5a1-108">Type **Y** tooproceed Hallo hotfix-installatie.</span><span class="sxs-lookup"><span data-stu-id="9b5a1-108">Type **Y** tooproceed with hello hotfix installation.</span></span>
5. <span data-ttu-id="9b5a1-109">Nadat u hebt toegepast Hallo hotfix op een domeincontroller, aanmelden toohello andere domeincontroller.</span><span class="sxs-lookup"><span data-stu-id="9b5a1-109">After you have applied hello hotfix on one controller, log on toohello other controller.</span></span> <span data-ttu-id="9b5a1-110">Hallo hotfix toepassen als bij eerdere Hallo-controller.</span><span class="sxs-lookup"><span data-stu-id="9b5a1-110">Apply hello hotfix as you did for hello previous controller.</span></span>
6. <span data-ttu-id="9b5a1-111">Nadat Hallo hotfixes worden toegepast, sluit u de onderhoudsmodus.</span><span class="sxs-lookup"><span data-stu-id="9b5a1-111">After hello hotfixes are applied, exit Maintenance mode.</span></span> <span data-ttu-id="9b5a1-112">Zie [stap 4: afsluiten onderhoudsmodus](../articles/storsimple/storsimple-update-device.md#step4) voor instructies.</span><span class="sxs-lookup"><span data-stu-id="9b5a1-112">See [Step 4: Exit Maintenance mode](../articles/storsimple/storsimple-update-device.md#step4) for instructions.</span></span>

