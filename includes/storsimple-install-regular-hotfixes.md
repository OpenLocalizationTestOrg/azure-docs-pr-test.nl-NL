<!--author=SharS last changed: 9/17/15-->

#### <a name="tooinstall-regular-hotfixes-via-windows-powershell-for-storsimple"></a><span data-ttu-id="1d9d6-101">tooinstall reguliere hotfixes via Windows PowerShell voor StorSimple</span><span class="sxs-lookup"><span data-stu-id="1d9d6-101">tooinstall regular hotfixes via Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="1d9d6-102">Verbinding met het maken van de seriële console van toohello apparaat.</span><span class="sxs-lookup"><span data-stu-id="1d9d6-102">Connect toohello device serial console.</span></span> <span data-ttu-id="1d9d6-103">Zie voor meer informatie [stap 1: verbinding maken met de seriële console toohello](../articles/storsimple/storsimple-update-device.md#step1).</span><span class="sxs-lookup"><span data-stu-id="1d9d6-103">For more information, see [Step 1: Connect toohello serial console](../articles/storsimple/storsimple-update-device.md#step1).</span></span>
2. <span data-ttu-id="1d9d6-104">In het menu van de seriële console hello, optie 1, **aanmelden met volledige toegang**.</span><span class="sxs-lookup"><span data-stu-id="1d9d6-104">In hello serial console menu, select option 1, **Log in with full access**.</span></span> <span data-ttu-id="1d9d6-105">Type Hallo wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="1d9d6-105">Type hello password.</span></span> <span data-ttu-id="1d9d6-106">is het standaardwachtwoord Hallo **Wachtwoord1**.</span><span class="sxs-lookup"><span data-stu-id="1d9d6-106">hello default password is **Password1**.</span></span>
3. <span data-ttu-id="1d9d6-107">Typ het volgende achter de opdrachtprompt Hallo:</span><span class="sxs-lookup"><span data-stu-id="1d9d6-107">At hello command prompt, type:</span></span>
   
    ```
    Start-HcsHotfix
    ```
   
    > [!IMPORTANT]
    >
    > <span data-ttu-id="1d9d6-108">Met deze opdracht worden alleen tooregular hotfixes toegepast.</span><span class="sxs-lookup"><span data-stu-id="1d9d6-108">This command applies only tooregular hotfixes.</span></span> <span data-ttu-id="1d9d6-109">U deze opdracht uitvoert op slechts één domeincontroller, maar beide domeincontrollers wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="1d9d6-109">You run this command on only one controller, but both controllers will be updated.</span></span>
    > <span data-ttu-id="1d9d6-110">Merkt u wellicht een failover van de domeincontroller tijdens het updateproces Hallo; echter, Hallo failover niet van invloed op beschikbaarheid van het systeem of de bewerking.</span><span class="sxs-lookup"><span data-stu-id="1d9d6-110">You may notice a controller failover during hello update process; however, hello failover will not affect system availability or operation.</span></span>

4. <span data-ttu-id="1d9d6-111">Als u wordt gevraagd, geeft u Hallo pad toohello gedeelde netwerkmap waarin Hallo hotfix-bestanden.</span><span class="sxs-lookup"><span data-stu-id="1d9d6-111">When prompted, supply hello path toohello network shared folder that contains hello hotfix files.</span></span>
5. <span data-ttu-id="1d9d6-112">U wordt gevraagd om bevestiging.</span><span class="sxs-lookup"><span data-stu-id="1d9d6-112">You will be prompted for confirmation.</span></span> <span data-ttu-id="1d9d6-113">Type **Y** tooproceed Hallo hotfix-installatie.</span><span class="sxs-lookup"><span data-stu-id="1d9d6-113">Type **Y** tooproceed with hello hotfix installation.</span></span>

