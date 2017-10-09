
<br>

> [!NOTE]
> <span data-ttu-id="20d17-101">Als u een gebruikersnaam en wachtwoord van een beheerder zijn ontvangen, er is een goede kans dat u al een werk hebt- of school ID (ook wel een *organisatie-ID*).</span><span class="sxs-lookup"><span data-stu-id="20d17-101">If you were given a user name and password by an administrator, there's a good chance that you already have a work or school ID (also sometimes called an *organizational ID*).</span></span> <span data-ttu-id="20d17-102">Zo ja, kunt u onmiddellijk toouse de tooaccess van uw Azure-account Azure-resources die vereist is.</span><span class="sxs-lookup"><span data-stu-id="20d17-102">If so, you can immediately begin toouse your Azure account tooaccess Azure resources that require one.</span></span> <span data-ttu-id="20d17-103">Als u vindt dat u deze resources niet gebruiken, moet u mogelijk tooreturn toothis artikel voor hulp.</span><span class="sxs-lookup"><span data-stu-id="20d17-103">If you find that you cannot use those resources, you may need tooreturn toothis article for help.</span></span> <span data-ttu-id="20d17-104">Zie voor meer informatie [Accounts die u kunt gebruiken voor aanmelden](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SignInAccounts) en [hoe een Azure-abonnement is gerelateerd tooAzure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SubRelationToDir).</span><span class="sxs-lookup"><span data-stu-id="20d17-104">For more information, see [Accounts that you can use for sign in](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SignInAccounts) and [How an Azure subscription is related tooAzure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SubRelationToDir).</span></span>
> 
> 

<span data-ttu-id="20d17-105">Hallo stappen zijn eenvoudige.</span><span class="sxs-lookup"><span data-stu-id="20d17-105">hello steps are simple.</span></span> <span data-ttu-id="20d17-106">U moet toolocate uw ondertekende van identiteit in de klassieke Azure-portal Hallo uw standaard Azure Active Directory-domein detecteren en toevoegen van een nieuwe gebruiker-tooit als een Azure CO-beheerder.</span><span class="sxs-lookup"><span data-stu-id="20d17-106">You need toolocate your signed on identity in hello Azure classic portal, discover your default Azure Active Directory domain, and add a new user tooit as an Azure co-administrator.</span></span>

## <a name="locate-your-default-directory-in-hello-azure-classic-portal"></a><span data-ttu-id="20d17-107">De standaardmap niet vinden in de klassieke Azure-portal Hallo</span><span class="sxs-lookup"><span data-stu-id="20d17-107">Locate your default directory in hello Azure classic portal</span></span>
<span data-ttu-id="20d17-108">Start door logboekregistratie in toohello [klassieke Azure-portal](https://manage.windowsazure.com) met je persoonlijke Microsoft-account-identiteit.</span><span class="sxs-lookup"><span data-stu-id="20d17-108">Start by logging in toohello [Azure classic portal](https://manage.windowsazure.com) with your personal Microsoft account identity.</span></span> <span data-ttu-id="20d17-109">Nadat u bent aangemeld, schuif naar beneden Hallo blauw Configuratiescherm op Hallo linkerkant en klik op **ACTIVE DIRECTORY**.</span><span class="sxs-lookup"><span data-stu-id="20d17-109">After you are logged in, scroll down hello blue panel on hello left side and click **ACTIVE DIRECTORY**.</span></span>

![Azure Active Directory](./media/virtual-machines-common-create-aad-work-id/azureactivedirectorywidget.png)

<span data-ttu-id="20d17-111">U begint met bepaalde informatie over uw identiteit zoeken in Azure.</span><span class="sxs-lookup"><span data-stu-id="20d17-111">Let's start by finding some information about your identity in Azure.</span></span> <span data-ttu-id="20d17-112">U ziet er ongeveer zo Hallo volgen in het hoofdvenster hello, dat u hebt een standaard-map wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="20d17-112">You should see something like hello following in hello main pane, showing that you have one default directory.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultaadlisting.png)

<span data-ttu-id="20d17-113">We willen weten sommige meer informatie.</span><span class="sxs-lookup"><span data-stu-id="20d17-113">Let's find out some more information about it.</span></span> <span data-ttu-id="20d17-114">Klik op Hallo standaard directory rij, u de standaardeigenschappen directory Hallo voert.</span><span class="sxs-lookup"><span data-stu-id="20d17-114">Click hello default directory row, which brings you into hello default directory properties.</span></span>  

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectorypage.png)

<span data-ttu-id="20d17-115">tooview hello standaarddomeinnaam, klikt u op **DOMEINEN**.</span><span class="sxs-lookup"><span data-stu-id="20d17-115">tooview hello default domain name, click **DOMAINS**.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/domainclicktoseeyourdefaultdomain.png)

<span data-ttu-id="20d17-116">Hier moet u kunnen toosee dat wanneer hello Azure-account is gemaakt, Azure Active Directory een persoonlijke standaarddomein dat een hash-waarde (een getal dat is gegenereerd op basis van een tekenreeks met tekst) wordt gemaakt van uw persoonlijke ID gebruikt als een subdomein van onmicrosoft.com. Dat is Hallo domein toowhich u wordt nu een nieuwe gebruiker toevoegen.</span><span class="sxs-lookup"><span data-stu-id="20d17-116">Here you should be able toosee that when hello Azure account was created, Azure Active Directory created a personal default domain that is a hash value (a number generated from a string of text) of your personal ID used as a subdomain of onmicrosoft.com. That's hello domain toowhich you will now add a new user.</span></span>

## <a name="creating-a-new-user-in-hello-default-domain"></a><span data-ttu-id="20d17-117">Maken van een nieuwe gebruiker in Hallo standaarddomein</span><span class="sxs-lookup"><span data-stu-id="20d17-117">Creating a new user in hello default domain</span></span>
<span data-ttu-id="20d17-118">Klik op **gebruikers** en zoekt u uw persoonlijke één account.</span><span class="sxs-lookup"><span data-stu-id="20d17-118">Click **USERS** and look for your single personal account.</span></span> <span data-ttu-id="20d17-119">U ziet in Hallo **afkomstig uit** kolom die het is een **Microsoft-account**.</span><span class="sxs-lookup"><span data-stu-id="20d17-119">You should see in hello **SOURCED FROM** column that it is a **Microsoft account**.</span></span> <span data-ttu-id="20d17-120">We willen dat een gebruiker in uw standaard toocreate. onmicrosoft.com Azure Active Directory-domein.</span><span class="sxs-lookup"><span data-stu-id="20d17-120">We want toocreate a user in your default .onmicrosoft.com Azure Active Directory domain.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryuserslisting.png)

<span data-ttu-id="20d17-121">We zullen toofollow [deze instructies](https://technet.microsoft.com/library/hh967632.aspx#BKMK_1) in Hallo van de volgende stappen, maar een voorbeeld van een specifieke gebruiken.</span><span class="sxs-lookup"><span data-stu-id="20d17-121">We're going toofollow [these instructions](https://technet.microsoft.com/library/hh967632.aspx#BKMK_1) in hello next few steps, but use a specific example.</span></span>

<span data-ttu-id="20d17-122">Klik onder aan de pagina Hallo Hallo op **+ gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="20d17-122">At hello bottom of hello page, click **+ADD USER**.</span></span> <span data-ttu-id="20d17-123">Typ nieuwe gebruikersnaam Hallo in Hallo pagina die wordt weergegeven, en zorg Hallo **Type gebruiker** een **nieuwe gebruiker in uw organisatie**.</span><span class="sxs-lookup"><span data-stu-id="20d17-123">In hello page that appears, type hello new user name, and make hello **Type of User** a **New user in your organization**.</span></span> <span data-ttu-id="20d17-124">In dit voorbeeld wordt de nieuwe gebruikersnaam Hallo is `ahmet`.</span><span class="sxs-lookup"><span data-stu-id="20d17-124">In this example, hello new user name is `ahmet`.</span></span> <span data-ttu-id="20d17-125">Selecteer Hallo standaarddomein die u gedetecteerd eerder als Hallo domein voor ahmet van e-mailadres.</span><span class="sxs-lookup"><span data-stu-id="20d17-125">Select hello default domain that you discovered previously as hello domain for ahmet's email address.</span></span> <span data-ttu-id="20d17-126">Klik op volgende pijl Hallo na voltooiing.</span><span class="sxs-lookup"><span data-stu-id="20d17-126">Click hello next arrow when finished.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/addingauserwithdirectorydropdown.png)

<span data-ttu-id="20d17-127">Meer informatie voor Ahmet toevoegen, maar zorg ervoor dat tooselect Hallo juiste **rol** waarde.</span><span class="sxs-lookup"><span data-stu-id="20d17-127">Add more details for Ahmet, but make sure tooselect hello appropriate **ROLE** value.</span></span> <span data-ttu-id="20d17-128">Het is gemakkelijk toouse **globale beheerder** toomake zeker dat dingen werkt, maar als u een minder rol kunt gebruiken, dat is een goed idee.</span><span class="sxs-lookup"><span data-stu-id="20d17-128">It's easy toouse **Global Admin** toomake sure things are working, but if you can use a lesser role, that's a good idea.</span></span> <span data-ttu-id="20d17-129">In dit voorbeeld wordt Hallo **gebruiker** rol.</span><span class="sxs-lookup"><span data-stu-id="20d17-129">This example uses hello **User** role.</span></span> <span data-ttu-id="20d17-130">(Meer informatie op [Administrator-machtigingen per rol](https://msdn.microsoft.com/library/azure/dn468213.aspx#BKMK_1).) Schakel multi-factor authentication niet, tenzij u toouse multifactor-verificatie voor elk logboek in bewerking wilt.</span><span class="sxs-lookup"><span data-stu-id="20d17-130">(Find out more at [Administrator permissions by role](https://msdn.microsoft.com/library/azure/dn468213.aspx#BKMK_1).) Do not enable multi-factor authentication unless you want toouse multifactor authentication for each log in operation.</span></span> <span data-ttu-id="20d17-131">Wanneer u klaar bent, klikt u op Hallo pijl op volgende.</span><span class="sxs-lookup"><span data-stu-id="20d17-131">Click hello next arrow when you're finished.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/userprofileuseradmin.png)

<span data-ttu-id="20d17-132">Klik op Hallo **maken** toogenerate knop en de weergave van een tijdelijk wachtwoord voor Ahmet.</span><span class="sxs-lookup"><span data-stu-id="20d17-132">Click hello **create** button toogenerate and display a temporary password for Ahmet.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/gettemporarypasswordforuser.png)

<span data-ttu-id="20d17-133">E-mailadres voor de naam van gebruiker Hallo kopiëren of gebruik **wachtwoord IN E-mail verzenden**.</span><span class="sxs-lookup"><span data-stu-id="20d17-133">Copy hello user name email address, or use **SEND PASSWORD IN EMAIL**.</span></span> <span data-ttu-id="20d17-134">U moet kort Hallo informatie toolog op.</span><span class="sxs-lookup"><span data-stu-id="20d17-134">You'll need hello information toolog on shortly.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/receivedtemporarypassworddialog.png)

<span data-ttu-id="20d17-135">Nu u de nieuwe gebruiker Hallo ziet **Ahmet Hallo Developer**, brongegevens van Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="20d17-135">Now you should see hello new user, **Ahmet hello Developer**, sourced from Azure Active Directory.</span></span> <span data-ttu-id="20d17-136">U hebt Hallo nieuw werk of school-identiteit gemaakt met Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="20d17-136">You've created hello new work or school identity with Azure Active Directory.</span></span> <span data-ttu-id="20d17-137">Echter, deze identiteit nog niet over machtigingen toouse Azure resources.</span><span class="sxs-lookup"><span data-stu-id="20d17-137">However, this identity does not yet have permissions toouse Azure resources.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryusersaftercreate.png)

<span data-ttu-id="20d17-138">Als u **wachtwoord IN E-mail verzenden**, Hallo volgende soort e-mailbericht wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="20d17-138">If you use **SEND PASSWORD IN EMAIL**, hello following kind of email is sent.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/emailreceivedfromnewusercreation.png)

## <a name="adding-azure-co-administrator-rights-for-subscriptions"></a><span data-ttu-id="20d17-139">Azure mede administrator-rechten voor abonnementen toe te voegen</span><span class="sxs-lookup"><span data-stu-id="20d17-139">Adding Azure co-administrator rights for subscriptions</span></span>
<span data-ttu-id="20d17-140">Nu moet u tooadd Hallo nieuwe gebruiker als medebeheerder van uw abonnement zodat de nieuwe gebruiker Hallo toohello-beheerportal kunt aanmelden.</span><span class="sxs-lookup"><span data-stu-id="20d17-140">Now you need tooadd hello new user as a co-administrator of your subscription so hello new user can sign in toohello Management Portal.</span></span> <span data-ttu-id="20d17-141">dit in Hallo linksonder Configuratiescherm klikt u op toodo **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="20d17-141">toodo this, in hello lower-left panel click **Settings**.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/thesettingswidget.png)

<span data-ttu-id="20d17-142">Klik in het gebied van de belangrijkste instellingen hello, **beheerders** op Hallo boven- en u ziet alleen uw Microsoft-account persoonsgegevens.</span><span class="sxs-lookup"><span data-stu-id="20d17-142">In hello main settings area, click **ADMINISTRATORS** at hello top and you should see only your personal Microsoft account identity.</span></span> <span data-ttu-id="20d17-143">Klik onder aan de pagina Hallo Hallo op **+ toevoegen** toospecify medebeheerder.</span><span class="sxs-lookup"><span data-stu-id="20d17-143">At hello bottom of hello page, click **+ADD** toospecify a co-administrator.</span></span> <span data-ttu-id="20d17-144">Hier Hallo e-mailadres van de nieuwe gebruiker Hallo die u hebt gemaakt, met inbegrip van het standaarddomein.</span><span class="sxs-lookup"><span data-stu-id="20d17-144">Here, enter hello email address of hello new user you had created, including your default domain.</span></span> <span data-ttu-id="20d17-145">Zoals weergegeven in de volgende schermafbeelding hello, verschijnt een groen vinkje volgende toohello gebruiker voor de standaardmap Hallo.</span><span class="sxs-lookup"><span data-stu-id="20d17-145">As shown in hello next screenshot, a green check mark appears next toohello user for hello default directory.</span></span> <span data-ttu-id="20d17-146">Houd er rekening mee tooselect al dat u aan deze gebruiker toobe kunnen tooadminister dat wilt Hallo-abonnementen.</span><span class="sxs-lookup"><span data-stu-id="20d17-146">Remember tooselect all of hello subscriptions that you would like this user toobe able tooadminister.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/addingnewuserascoadmin.png)

<span data-ttu-id="20d17-147">Wanneer u klaar bent, ziet u nu twee gebruikers, met inbegrip van de nieuwe medebeheerder-identiteit.</span><span class="sxs-lookup"><span data-stu-id="20d17-147">When you are done, you should now see two users, including your new co-administrator identity.</span></span> <span data-ttu-id="20d17-148">Afmelding Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="20d17-148">Log out of hello portal.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/newuseraddedascoadministrator.png)

## <a name="logging-in-and-changing-hello-new-users-password"></a><span data-ttu-id="20d17-149">Aanmelden en Hallo nieuwe gebruiker-wachtwoord wijzigen</span><span class="sxs-lookup"><span data-stu-id="20d17-149">Logging in and changing hello new user's password</span></span>
<span data-ttu-id="20d17-150">Aanmelden als Hallo nieuwe gebruiker die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="20d17-150">Log in as hello new user you created.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/signinginwithnewuser.png)

<span data-ttu-id="20d17-151">U zult onmiddellijk na vragen aan gebruiker toocreate een nieuw wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="20d17-151">You will immediately be prompted toocreate a new password.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/mustupdateyourpassword.png)

<span data-ttu-id="20d17-152">U moet met succes dat op de volgende Hallo lijkt beloond.</span><span class="sxs-lookup"><span data-stu-id="20d17-152">You should be rewarded with success that looks like hello following.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/successtourdialog.png)

## <a name="next-steps"></a><span data-ttu-id="20d17-153">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="20d17-153">Next steps</span></span>
<span data-ttu-id="20d17-154">U kunt nu uw nieuwe Azure Active Directory-identiteit toouse [Azure resource group sjablonen](../articles/xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="20d17-154">You can now use your new Azure Active Directory identity toouse [Azure resource group templates](../articles/xplat-cli-azure-resource-manager.md).</span></span>

    azure login
    info:    Executing command login
    warn:    Please note that currently you can login only via Microsoft organizational account or service principal. For instructions on how tooset them up, please read http://aka.ms/Dhf67j.
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
