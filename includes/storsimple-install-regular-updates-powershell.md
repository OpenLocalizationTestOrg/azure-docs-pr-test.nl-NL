<!--author=SharS last changed: 11/18/16-->

#### <a name="to-install-regular-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="3cad1-101">Reguliere om updates te installeren via Windows PowerShell voor StorSimple</span><span class="sxs-lookup"><span data-stu-id="3cad1-101">To install regular updates via Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="3cad1-102">Open de seriële console van apparaat en selecteer optie 1, **aanmelden met volledige toegang**.</span><span class="sxs-lookup"><span data-stu-id="3cad1-102">Open the device serial console and select option 1, **Log in with full access**.</span></span> <span data-ttu-id="3cad1-103">Typ het wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="3cad1-103">Type the password.</span></span> <span data-ttu-id="3cad1-104">Is het standaardwachtwoord *Wachtwoord1*.</span><span class="sxs-lookup"><span data-stu-id="3cad1-104">The default password is *Password1*.</span></span> 
2. <span data-ttu-id="3cad1-105">Typ het volgende achter de opdrachtprompt:</span><span class="sxs-lookup"><span data-stu-id="3cad1-105">At the command prompt, type:</span></span>
   
     `Get-HcsUpdateAvailability`
   
    <span data-ttu-id="3cad1-106">U wordt gewaarschuwd als er updates beschikbaar zijn en of de updates verstoren of niet verstoren zijn.</span><span class="sxs-lookup"><span data-stu-id="3cad1-106">You will be notified if updates are available and whether the updates are disruptive or non-disruptive.</span></span>
3. <span data-ttu-id="3cad1-107">Typ het volgende achter de opdrachtprompt:</span><span class="sxs-lookup"><span data-stu-id="3cad1-107">At the command prompt, type:</span></span>
   
     `Start-HcsUpdate`
   
    <span data-ttu-id="3cad1-108">Het updateproces wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="3cad1-108">The update process will start.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="3cad1-109">Met deze opdracht geldt alleen voor regelmatige updates.</span><span class="sxs-lookup"><span data-stu-id="3cad1-109">This command applies only to regular updates.</span></span> <span data-ttu-id="3cad1-110">U deze opdracht uitvoert op slechts één domeincontroller, maar beide domeincontrollers wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="3cad1-110">You run this command on only one controller, but both controllers will be updated.</span></span> 
> * <span data-ttu-id="3cad1-111">Merkt u wellicht een failover van de domeincontroller tijdens het updateproces; echter, de failover niet van invloed op beschikbaarheid van het systeem of de bewerking.</span><span class="sxs-lookup"><span data-stu-id="3cad1-111">You may notice a controller failover during the update process; however, the failover will not affect system availability or operation.</span></span>
> 
> 

