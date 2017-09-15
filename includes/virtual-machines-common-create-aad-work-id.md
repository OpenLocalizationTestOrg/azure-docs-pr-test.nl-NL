
<br>

> [!NOTE]
> <span data-ttu-id="3d71b-101">Als u een gebruikersnaam en wachtwoord van een beheerder zijn ontvangen, er is een goede kans dat u al een werk hebt- of school ID (ook wel een *organisatie-ID*).</span><span class="sxs-lookup"><span data-stu-id="3d71b-101">If you were given a user name and password by an administrator, there's a good chance that you already have a work or school ID (also sometimes called an *organizational ID*).</span></span> <span data-ttu-id="3d71b-102">Als dit het geval is, kunt u meteen beginnen op uw Azure-account voor toegang tot Azure-resources die vereist is.</span><span class="sxs-lookup"><span data-stu-id="3d71b-102">If so, you can immediately begin to use your Azure account to access Azure resources that require one.</span></span> <span data-ttu-id="3d71b-103">Als u vindt dat u deze resources niet gebruiken, moet u wellicht terug naar dit artikel voor hulp.</span><span class="sxs-lookup"><span data-stu-id="3d71b-103">If you find that you cannot use those resources, you may need to return to this article for help.</span></span> <span data-ttu-id="3d71b-104">Zie voor meer informatie [Accounts die u kunt gebruiken voor aanmelden](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SignInAccounts) en [hoe een Azure-abonnement is gerelateerd aan Azure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SubRelationToDir).</span><span class="sxs-lookup"><span data-stu-id="3d71b-104">For more information, see [Accounts that you can use for sign in](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SignInAccounts) and [How an Azure subscription is related to Azure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SubRelationToDir).</span></span>
> 
> 

<span data-ttu-id="3d71b-105">De stappen zijn eenvoudige.</span><span class="sxs-lookup"><span data-stu-id="3d71b-105">The steps are simple.</span></span> <span data-ttu-id="3d71b-106">U moet uw ondertekende vinden op de identiteit in de klassieke Azure portal detecteren van uw standaard Azure Active Directory-domein en een nieuwe gebruiker toevoegen aan deze als een Azure CO-beheerder.</span><span class="sxs-lookup"><span data-stu-id="3d71b-106">You need to locate your signed on identity in the Azure classic portal, discover your default Azure Active Directory domain, and add a new user to it as an Azure co-administrator.</span></span>

## <a name="locate-your-default-directory-in-the-azure-classic-portal"></a><span data-ttu-id="3d71b-107">Standaard-map niet vinden in de klassieke Azure portal</span><span class="sxs-lookup"><span data-stu-id="3d71b-107">Locate your default directory in the Azure classic portal</span></span>
<span data-ttu-id="3d71b-108">Eerst aanmelden bij de [klassieke Azure-portal](https://manage.windowsazure.com) met je persoonlijke Microsoft-account-identiteit.</span><span class="sxs-lookup"><span data-stu-id="3d71b-108">Start by logging in to the [Azure classic portal](https://manage.windowsazure.com) with your personal Microsoft account identity.</span></span> <span data-ttu-id="3d71b-109">Nadat u bent aangemeld, schuif naar beneden het blauw paneel aan de linkerkant en klik op **ACTIVE DIRECTORY**.</span><span class="sxs-lookup"><span data-stu-id="3d71b-109">After you are logged in, scroll down the blue panel on the left side and click **ACTIVE DIRECTORY**.</span></span>

![Azure Active Directory](./media/virtual-machines-common-create-aad-work-id/azureactivedirectorywidget.png)

<span data-ttu-id="3d71b-111">U begint met bepaalde informatie over uw identiteit zoeken in Azure.</span><span class="sxs-lookup"><span data-stu-id="3d71b-111">Let's start by finding some information about your identity in Azure.</span></span> <span data-ttu-id="3d71b-112">U ziet er als volgt te werk in het hoofdvenster weergegeven dat u een standaard-map hebt.</span><span class="sxs-lookup"><span data-stu-id="3d71b-112">You should see something like the following in the main pane, showing that you have one default directory.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultaadlisting.png)

<span data-ttu-id="3d71b-113">We willen weten sommige meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3d71b-113">Let's find out some more information about it.</span></span> <span data-ttu-id="3d71b-114">Klik op de standaard directory rij, u de standaard directory-eigenschappen voert.</span><span class="sxs-lookup"><span data-stu-id="3d71b-114">Click the default directory row, which brings you into the default directory properties.</span></span>  

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectorypage.png)

<span data-ttu-id="3d71b-115">Als u wilt weergeven van de naam van het standaarddomein **DOMEINEN**.</span><span class="sxs-lookup"><span data-stu-id="3d71b-115">To view the default domain name, click **DOMAINS**.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/domainclicktoseeyourdefaultdomain.png)

<span data-ttu-id="3d71b-116">Hier moet u kunnen om te zien of wanneer het Azure-account is gemaakt, Azure Active Directory een persoonlijke standaarddomein die een hash-waarde (een getal dat is gegenereerd op basis van een tekenreeks met tekst) is gemaakt van uw persoonlijke ID gebruikt als een subdomein van onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="3d71b-116">Here you should be able to see that when the Azure account was created, Azure Active Directory created a personal default domain that is a hash value (a number generated from a string of text) of your personal ID used as a subdomain of onmicrosoft.com.</span></span> <span data-ttu-id="3d71b-117">Dit is het domein waaraan u een nieuwe gebruiker nu wilt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="3d71b-117">That's the domain to which you will now add a new user.</span></span>

## <a name="creating-a-new-user-in-the-default-domain"></a><span data-ttu-id="3d71b-118">Maken van een nieuwe gebruiker in het standaarddomein</span><span class="sxs-lookup"><span data-stu-id="3d71b-118">Creating a new user in the default domain</span></span>
<span data-ttu-id="3d71b-119">Klik op **gebruikers** en zoekt u uw persoonlijke één account.</span><span class="sxs-lookup"><span data-stu-id="3d71b-119">Click **USERS** and look for your single personal account.</span></span> <span data-ttu-id="3d71b-120">U ziet de **afkomstig uit** kolom die het is een **Microsoft-account**.</span><span class="sxs-lookup"><span data-stu-id="3d71b-120">You should see in the **SOURCED FROM** column that it is a **Microsoft account**.</span></span> <span data-ttu-id="3d71b-121">We willen maken van een gebruiker in de standaard. onmicrosoft.com Azure Active Directory-domein.</span><span class="sxs-lookup"><span data-stu-id="3d71b-121">We want to create a user in your default .onmicrosoft.com Azure Active Directory domain.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryuserslisting.png)

<span data-ttu-id="3d71b-122">We gaan Volg [deze instructies](https://technet.microsoft.com/library/hh967632.aspx#BKMK_1) in de volgende stappen een voorbeeld van een specifieke maar gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3d71b-122">We're going to follow [these instructions](https://technet.microsoft.com/library/hh967632.aspx#BKMK_1) in the next few steps, but use a specific example.</span></span>

<span data-ttu-id="3d71b-123">Klik onder aan de pagina op **+ gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="3d71b-123">At the bottom of the page, click **+ADD USER**.</span></span> <span data-ttu-id="3d71b-124">Typ de naam van de nieuwe gebruiker in de pagina die wordt weergegeven, en controleer de **Type gebruiker** een **nieuwe gebruiker in uw organisatie**.</span><span class="sxs-lookup"><span data-stu-id="3d71b-124">In the page that appears, type the new user name, and make the **Type of User** a **New user in your organization**.</span></span> <span data-ttu-id="3d71b-125">In dit voorbeeld wordt de naam van de nieuwe gebruiker is `ahmet`.</span><span class="sxs-lookup"><span data-stu-id="3d71b-125">In this example, the new user name is `ahmet`.</span></span> <span data-ttu-id="3d71b-126">Selecteer het standaarddomein die u gedetecteerd eerder als het domein voor ahmet van e-mailadres.</span><span class="sxs-lookup"><span data-stu-id="3d71b-126">Select the default domain that you discovered previously as the domain for ahmet's email address.</span></span> <span data-ttu-id="3d71b-127">Klik op de pijl volgende na voltooiing.</span><span class="sxs-lookup"><span data-stu-id="3d71b-127">Click the next arrow when finished.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/addingauserwithdirectorydropdown.png)

<span data-ttu-id="3d71b-128">Meer informatie voor Ahmet toevoegen, maar zorg ervoor dat u selecteert u de juiste **rol** waarde.</span><span class="sxs-lookup"><span data-stu-id="3d71b-128">Add more details for Ahmet, but make sure to select the appropriate **ROLE** value.</span></span> <span data-ttu-id="3d71b-129">Het is eenvoudig te gebruiken **globale beheerder** aanbrengen zeker dat dingen werkt, maar als u een minder rol kunt gebruiken, die is een goed idee.</span><span class="sxs-lookup"><span data-stu-id="3d71b-129">It's easy to use **Global Admin** to make sure things are working, but if you can use a lesser role, that's a good idea.</span></span> <span data-ttu-id="3d71b-130">In dit voorbeeld wordt de **gebruiker** rol.</span><span class="sxs-lookup"><span data-stu-id="3d71b-130">This example uses the **User** role.</span></span> <span data-ttu-id="3d71b-131">(Meer informatie op [Administrator-machtigingen per rol](https://msdn.microsoft.com/library/azure/dn468213.aspx#BKMK_1).) Schakel multi-factor authentication niet, tenzij u wilt voor meervoudige verificatie voor elk logboek in bewerking.</span><span class="sxs-lookup"><span data-stu-id="3d71b-131">(Find out more at [Administrator permissions by role](https://msdn.microsoft.com/library/azure/dn468213.aspx#BKMK_1).) Do not enable multi-factor authentication unless you want to use multifactor authentication for each log in operation.</span></span> <span data-ttu-id="3d71b-132">Wanneer u klaar bent, klikt u op de pijl Volgende.</span><span class="sxs-lookup"><span data-stu-id="3d71b-132">Click the next arrow when you're finished.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/userprofileuseradmin.png)

<span data-ttu-id="3d71b-133">Klik op de **maken** knop genereren en weergeven van een tijdelijk wachtwoord voor Ahmet.</span><span class="sxs-lookup"><span data-stu-id="3d71b-133">Click the **create** button to generate and display a temporary password for Ahmet.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/gettemporarypasswordforuser.png)

<span data-ttu-id="3d71b-134">Kopieer de e-mailadres van de gebruiker de naam of gebruik **wachtwoord IN E-mail verzenden**.</span><span class="sxs-lookup"><span data-stu-id="3d71b-134">Copy the user name email address, or use **SEND PASSWORD IN EMAIL**.</span></span> <span data-ttu-id="3d71b-135">U moet de gegevens aan te melden binnen enkele ogenblikken.</span><span class="sxs-lookup"><span data-stu-id="3d71b-135">You'll need the information to log on shortly.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/receivedtemporarypassworddialog.png)

<span data-ttu-id="3d71b-136">Nu u de nieuwe gebruiker ziet **Ahmet de ontwikkelaar**, brongegevens van Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3d71b-136">Now you should see the new user, **Ahmet the Developer**, sourced from Azure Active Directory.</span></span> <span data-ttu-id="3d71b-137">U hebt nieuwe werk of school-identiteit gemaakt met Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3d71b-137">You've created the new work or school identity with Azure Active Directory.</span></span> <span data-ttu-id="3d71b-138">Echter, deze identiteit nog geen machtigingen voor het gebruik van Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="3d71b-138">However, this identity does not yet have permissions to use Azure resources.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryusersaftercreate.png)

<span data-ttu-id="3d71b-139">Als u **wachtwoord IN E-mail verzenden**, het volgende type e-mailbericht wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="3d71b-139">If you use **SEND PASSWORD IN EMAIL**, the following kind of email is sent.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/emailreceivedfromnewusercreation.png)

## <a name="adding-azure-co-administrator-rights-for-subscriptions"></a><span data-ttu-id="3d71b-140">Azure mede administrator-rechten voor abonnementen toe te voegen</span><span class="sxs-lookup"><span data-stu-id="3d71b-140">Adding Azure co-administrator rights for subscriptions</span></span>
<span data-ttu-id="3d71b-141">Nu moet u de nieuwe gebruiker toevoegen als medebeheerder van uw abonnement, zodat de nieuwe gebruiker bij de beheerportal aanmelden kunt.</span><span class="sxs-lookup"><span data-stu-id="3d71b-141">Now you need to add the new user as a co-administrator of your subscription so the new user can sign in to the Management Portal.</span></span> <span data-ttu-id="3d71b-142">U doet dit door in het deelvenster linksonder klikt u op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="3d71b-142">To do this, in the lower-left panel click **Settings**.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/thesettingswidget.png)

<span data-ttu-id="3d71b-143">Klik in het gebied belangrijkste instellingen **beheerders** bovenaan en u ziet alleen uw Microsoft-account persoonsgegevens.</span><span class="sxs-lookup"><span data-stu-id="3d71b-143">In the main settings area, click **ADMINISTRATORS** at the top and you should see only your personal Microsoft account identity.</span></span> <span data-ttu-id="3d71b-144">Klik onder aan de pagina op **+ toevoegen** om op te geven van een CO-beheerder.</span><span class="sxs-lookup"><span data-stu-id="3d71b-144">At the bottom of the page, click **+ADD** to specify a co-administrator.</span></span> <span data-ttu-id="3d71b-145">Voer hier het e-mailadres van de nieuwe gebruiker die u hebt gemaakt, met inbegrip van het standaarddomein.</span><span class="sxs-lookup"><span data-stu-id="3d71b-145">Here, enter the email address of the new user you had created, including your default domain.</span></span> <span data-ttu-id="3d71b-146">Zoals u in de volgende schermafbeelding, wordt een groen vinkje weergegeven naast de gebruiker voor de standaard-map.</span><span class="sxs-lookup"><span data-stu-id="3d71b-146">As shown in the next screenshot, a green check mark appears next to the user for the default directory.</span></span> <span data-ttu-id="3d71b-147">Vergeet niet om alle abonnementen op die u deze gebruiker kan dat wilt beheren te selecteren.</span><span class="sxs-lookup"><span data-stu-id="3d71b-147">Remember to select all of the subscriptions that you would like this user to be able to administer.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/addingnewuserascoadmin.png)

<span data-ttu-id="3d71b-148">Wanneer u klaar bent, ziet u nu twee gebruikers, met inbegrip van de nieuwe medebeheerder-identiteit.</span><span class="sxs-lookup"><span data-stu-id="3d71b-148">When you are done, you should now see two users, including your new co-administrator identity.</span></span> <span data-ttu-id="3d71b-149">Meld u af bij van de portal.</span><span class="sxs-lookup"><span data-stu-id="3d71b-149">Log out of the portal.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/newuseraddedascoadministrator.png)

## <a name="logging-in-and-changing-the-new-users-password"></a><span data-ttu-id="3d71b-150">Aanmelden en de nieuwe gebruiker-wachtwoord wijzigen</span><span class="sxs-lookup"><span data-stu-id="3d71b-150">Logging in and changing the new user's password</span></span>
<span data-ttu-id="3d71b-151">Aanmelden als de nieuwe gebruiker die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3d71b-151">Log in as the new user you created.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/signinginwithnewuser.png)

<span data-ttu-id="3d71b-152">U wordt onmiddellijk gevraagd een nieuw wachtwoord maken.</span><span class="sxs-lookup"><span data-stu-id="3d71b-152">You will immediately be prompted to create a new password.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/mustupdateyourpassword.png)

<span data-ttu-id="3d71b-153">U moet met succes dat op de volgende lijkt beloond.</span><span class="sxs-lookup"><span data-stu-id="3d71b-153">You should be rewarded with success that looks like the following.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/successtourdialog.png)

## <a name="next-steps"></a><span data-ttu-id="3d71b-154">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3d71b-154">Next steps</span></span>
<span data-ttu-id="3d71b-155">U kunt nu de nieuwe Azure Active Directory-identiteit gebruiken [Azure resource group sjablonen](../articles/xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="3d71b-155">You can now use your new Azure Active Directory identity to use [Azure resource group templates](../articles/xplat-cli-azure-resource-manager.md).</span></span>

    azure login
    info:    Executing command login
    warn:    Please note that currently you can login only via Microsoft organizational account or service principal. For instructions on how to set them up, please read http://aka.ms/Dhf67j.
    Username: ahmet@aztrainpassxxxxxoutlook.onmicrosoft.com
    Password: *********
    /info:    Added subscription Azure Pass
    info:    Setting subscription Azure Pass as default
    +
    info:    login command OK
    ralph@local:~$ azure config mode arm
    info:    New mode is arm
    ralph@local:~$ azure group list
    info:    Executing command group list
    + Listing resource groups
    info:    No matched resource groups were found
    info:    group list command OK
    ralph@local:~$ azure group create newgroup westus
    info:    Executing command group create
    + Getting resource group newgroup
    + Creating resource group newgroup
    info:    Created resource group newgroup
    data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/newgroup
    data:    Name:                newgroup
    data:    Location:            westus
    data:    Provisioning State:  Succeeded
    data:    Tags:
    data:
    info:    group create command OK
