
<br>

> [!NOTE]
> Als u een gebruikersnaam en wachtwoord van een beheerder zijn ontvangen, er is een goede kans dat u al een werk hebt- of school ID (ook wel een *organisatie-ID*). Zo ja, kunt u onmiddellijk toouse de tooaccess van uw Azure-account Azure-resources die vereist is. Als u vindt dat u deze resources niet gebruiken, moet u mogelijk tooreturn toothis artikel voor hulp. Zie voor meer informatie [Accounts die u kunt gebruiken voor aanmelden](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SignInAccounts) en [hoe een Azure-abonnement is gerelateerd tooAzure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SubRelationToDir).
> 
> 

Hallo stappen zijn eenvoudige. U moet toolocate uw ondertekende van identiteit in de klassieke Azure-portal Hallo uw standaard Azure Active Directory-domein detecteren en toevoegen van een nieuwe gebruiker-tooit als een Azure CO-beheerder.

## <a name="locate-your-default-directory-in-hello-azure-classic-portal"></a>De standaardmap niet vinden in de klassieke Azure-portal Hallo
Start door logboekregistratie in toohello [klassieke Azure-portal](https://manage.windowsazure.com) met je persoonlijke Microsoft-account-identiteit. Nadat u bent aangemeld, schuif naar beneden Hallo blauw Configuratiescherm op Hallo linkerkant en klik op **ACTIVE DIRECTORY**.

![Azure Active Directory](./media/virtual-machines-common-create-aad-work-id/azureactivedirectorywidget.png)

U begint met bepaalde informatie over uw identiteit zoeken in Azure. U ziet er ongeveer zo Hallo volgen in het hoofdvenster hello, dat u hebt een standaard-map wordt weergegeven.

![](./media/virtual-machines-common-create-aad-work-id/defaultaadlisting.png)

We willen weten sommige meer informatie. Klik op Hallo standaard directory rij, u de standaardeigenschappen directory Hallo voert.  

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectorypage.png)

tooview hello standaarddomeinnaam, klikt u op **DOMEINEN**.

![](./media/virtual-machines-common-create-aad-work-id/domainclicktoseeyourdefaultdomain.png)

Hier moet u kunnen toosee dat wanneer hello Azure-account is gemaakt, Azure Active Directory een persoonlijke standaarddomein dat een hash-waarde (een getal dat is gegenereerd op basis van een tekenreeks met tekst) wordt gemaakt van uw persoonlijke ID gebruikt als een subdomein van onmicrosoft.com. Dat is Hallo domein toowhich u wordt nu een nieuwe gebruiker toevoegen.

## <a name="creating-a-new-user-in-hello-default-domain"></a>Maken van een nieuwe gebruiker in Hallo standaarddomein
Klik op **gebruikers** en zoekt u uw persoonlijke één account. U ziet in Hallo **afkomstig uit** kolom die het is een **Microsoft-account**. We willen dat een gebruiker in uw standaard toocreate. onmicrosoft.com Azure Active Directory-domein.

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryuserslisting.png)

We zullen toofollow [deze instructies](https://technet.microsoft.com/library/hh967632.aspx#BKMK_1) in Hallo van de volgende stappen, maar een voorbeeld van een specifieke gebruiken.

Klik onder aan de pagina Hallo Hallo op **+ gebruiker toevoegen**. Typ nieuwe gebruikersnaam Hallo in Hallo pagina die wordt weergegeven, en zorg Hallo **Type gebruiker** een **nieuwe gebruiker in uw organisatie**. In dit voorbeeld wordt de nieuwe gebruikersnaam Hallo is `ahmet`. Selecteer Hallo standaarddomein die u gedetecteerd eerder als Hallo domein voor ahmet van e-mailadres. Klik op volgende pijl Hallo na voltooiing.

![](./media/virtual-machines-common-create-aad-work-id/addingauserwithdirectorydropdown.png)

Meer informatie voor Ahmet toevoegen, maar zorg ervoor dat tooselect Hallo juiste **rol** waarde. Het is gemakkelijk toouse **globale beheerder** toomake zeker dat dingen werkt, maar als u een minder rol kunt gebruiken, dat is een goed idee. In dit voorbeeld wordt Hallo **gebruiker** rol. (Meer informatie op [Administrator-machtigingen per rol](https://msdn.microsoft.com/library/azure/dn468213.aspx#BKMK_1).) Schakel multi-factor authentication niet, tenzij u toouse multifactor-verificatie voor elk logboek in bewerking wilt. Wanneer u klaar bent, klikt u op Hallo pijl op volgende.

![](./media/virtual-machines-common-create-aad-work-id/userprofileuseradmin.png)

Klik op Hallo **maken** toogenerate knop en de weergave van een tijdelijk wachtwoord voor Ahmet.

![](./media/virtual-machines-common-create-aad-work-id/gettemporarypasswordforuser.png)

E-mailadres voor de naam van gebruiker Hallo kopiëren of gebruik **wachtwoord IN E-mail verzenden**. U moet kort Hallo informatie toolog op.

![](./media/virtual-machines-common-create-aad-work-id/receivedtemporarypassworddialog.png)

Nu u de nieuwe gebruiker Hallo ziet **Ahmet Hallo Developer**, brongegevens van Azure Active Directory. U hebt Hallo nieuw werk of school-identiteit gemaakt met Azure Active Directory. Echter, deze identiteit nog niet over machtigingen toouse Azure resources.

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryusersaftercreate.png)

Als u **wachtwoord IN E-mail verzenden**, Hallo volgende soort e-mailbericht wordt verzonden.

![](./media/virtual-machines-common-create-aad-work-id/emailreceivedfromnewusercreation.png)

## <a name="adding-azure-co-administrator-rights-for-subscriptions"></a>Azure mede administrator-rechten voor abonnementen toe te voegen
Nu moet u tooadd Hallo nieuwe gebruiker als medebeheerder van uw abonnement zodat de nieuwe gebruiker Hallo toohello-beheerportal kunt aanmelden. dit in Hallo linksonder Configuratiescherm klikt u op toodo **instellingen**.

![](./media/virtual-machines-common-create-aad-work-id/thesettingswidget.png)

Klik in het gebied van de belangrijkste instellingen hello, **beheerders** op Hallo boven- en u ziet alleen uw Microsoft-account persoonsgegevens. Klik onder aan de pagina Hallo Hallo op **+ toevoegen** toospecify medebeheerder. Hier Hallo e-mailadres van de nieuwe gebruiker Hallo die u hebt gemaakt, met inbegrip van het standaarddomein. Zoals weergegeven in de volgende schermafbeelding hello, verschijnt een groen vinkje volgende toohello gebruiker voor de standaardmap Hallo. Houd er rekening mee tooselect al dat u aan deze gebruiker toobe kunnen tooadminister dat wilt Hallo-abonnementen.

![](./media/virtual-machines-common-create-aad-work-id/addingnewuserascoadmin.png)

Wanneer u klaar bent, ziet u nu twee gebruikers, met inbegrip van de nieuwe medebeheerder-identiteit. Afmelding Hallo-portal.

![](./media/virtual-machines-common-create-aad-work-id/newuseraddedascoadministrator.png)

## <a name="logging-in-and-changing-hello-new-users-password"></a>Aanmelden en Hallo nieuwe gebruiker-wachtwoord wijzigen
Aanmelden als Hallo nieuwe gebruiker die u hebt gemaakt.

![](./media/virtual-machines-common-create-aad-work-id/signinginwithnewuser.png)

U zult onmiddellijk na vragen aan gebruiker toocreate een nieuw wachtwoord.

![](./media/virtual-machines-common-create-aad-work-id/mustupdateyourpassword.png)

U moet met succes dat op de volgende Hallo lijkt beloond.

![](./media/virtual-machines-common-create-aad-work-id/successtourdialog.png)

## <a name="next-steps"></a>Volgende stappen
U kunt nu uw nieuwe Azure Active Directory-identiteit toouse [Azure resource group sjablonen](../articles/xplat-cli-azure-resource-manager.md).

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
