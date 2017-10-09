<!--author=SharS last changed: 11/18/16-->

#### <a name="tooinstall-regular-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="faf14-101">tooinstall regelmatig updates via Windows PowerShell voor StorSimple</span><span class="sxs-lookup"><span data-stu-id="faf14-101">tooinstall regular updates via Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="faf14-102">Open Hallo apparaat seriële console en selecteer optie 1, **aanmelden met volledige toegang**.</span><span class="sxs-lookup"><span data-stu-id="faf14-102">Open hello device serial console and select option 1, **Log in with full access**.</span></span> <span data-ttu-id="faf14-103">Type Hallo wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="faf14-103">Type hello password.</span></span> <span data-ttu-id="faf14-104">is het standaardwachtwoord Hallo *Wachtwoord1*.</span><span class="sxs-lookup"><span data-stu-id="faf14-104">hello default password is *Password1*.</span></span> 
2. <span data-ttu-id="faf14-105">Typ het volgende achter de opdrachtprompt Hallo:</span><span class="sxs-lookup"><span data-stu-id="faf14-105">At hello command prompt, type:</span></span>
   
     `Get-HcsUpdateAvailability`
   
    <span data-ttu-id="faf14-106">U wordt gewaarschuwd als er updates beschikbaar zijn en of de Hallo-updates zijn verstoren of ononderbroken.</span><span class="sxs-lookup"><span data-stu-id="faf14-106">You will be notified if updates are available and whether hello updates are disruptive or non-disruptive.</span></span>
3. <span data-ttu-id="faf14-107">Typ het volgende achter de opdrachtprompt Hallo:</span><span class="sxs-lookup"><span data-stu-id="faf14-107">At hello command prompt, type:</span></span>
   
     `Start-HcsUpdate`
   
    <span data-ttu-id="faf14-108">Hallo-updateproces wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="faf14-108">hello update process will start.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="faf14-109">Met deze opdracht geldt alleen tooregular updates.</span><span class="sxs-lookup"><span data-stu-id="faf14-109">This command applies only tooregular updates.</span></span> <span data-ttu-id="faf14-110">U deze opdracht uitvoert op slechts één domeincontroller, maar beide domeincontrollers wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="faf14-110">You run this command on only one controller, but both controllers will be updated.</span></span> 
> * <span data-ttu-id="faf14-111">Merkt u wellicht een failover van de domeincontroller tijdens het updateproces Hallo; echter, Hallo failover niet van invloed op beschikbaarheid van het systeem of de bewerking.</span><span class="sxs-lookup"><span data-stu-id="faf14-111">You may notice a controller failover during hello update process; however, hello failover will not affect system availability or operation.</span></span>
> 
> 

