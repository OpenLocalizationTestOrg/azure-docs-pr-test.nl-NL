
<br>

> [!NOTE]
> Als u een gebruikersnaam en wachtwoord van een beheerder zijn ontvangen, er is een goede kans dat u al een werk hebt- of school ID (ook wel een *organisatie-ID*). Als dit het geval is, kunt u meteen beginnen op uw Azure-account voor toegang tot Azure-resources die vereist is. Als u vindt dat u deze resources niet gebruiken, moet u wellicht terug naar dit artikel voor hulp. Zie voor meer informatie [Accounts die u kunt gebruiken voor aanmelden](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SignInAccounts) en [hoe een Azure-abonnement is gerelateerd aan Azure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SubRelationToDir).
> 
> 

De stappen zijn eenvoudige. U moet uw ondertekende vinden op de identiteit in de klassieke Azure portal detecteren van uw standaard Azure Active Directory-domein en een nieuwe gebruiker toevoegen aan deze als een Azure CO-beheerder.

## <a name="locate-your-default-directory-in-the-azure-classic-portal"></a>Standaard-map niet vinden in de klassieke Azure portal
Eerst aanmelden bij de [klassieke Azure-portal](https://manage.windowsazure.com) met je persoonlijke Microsoft-account-identiteit. Nadat u bent aangemeld, schuif naar beneden het blauw paneel aan de linkerkant en klik op **ACTIVE DIRECTORY**.

![Azure Active Directory](./media/virtual-machines-common-create-aad-work-id/azureactivedirectorywidget.png)

U begint met bepaalde informatie over uw identiteit zoeken in Azure. U ziet er als volgt te werk in het hoofdvenster weergegeven dat u een standaard-map hebt.

![](./media/virtual-machines-common-create-aad-work-id/defaultaadlisting.png)

We willen weten sommige meer informatie. Klik op de standaard directory rij, u de standaard directory-eigenschappen voert.  

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectorypage.png)

Als u wilt weergeven van de naam van het standaarddomein **DOMEINEN**.

![](./media/virtual-machines-common-create-aad-work-id/domainclicktoseeyourdefaultdomain.png)

Hier moet u kunnen om te zien of wanneer het Azure-account is gemaakt, Azure Active Directory een persoonlijke standaarddomein die een hash-waarde (een getal dat is gegenereerd op basis van een tekenreeks met tekst) is gemaakt van uw persoonlijke ID gebruikt als een subdomein van onmicrosoft.com. Dit is het domein waaraan u een nieuwe gebruiker nu wilt toevoegen.

## <a name="creating-a-new-user-in-the-default-domain"></a>Maken van een nieuwe gebruiker in het standaarddomein
Klik op **gebruikers** en zoekt u uw persoonlijke één account. U ziet de **afkomstig uit** kolom die het is een **Microsoft-account**. We willen maken van een gebruiker in de standaard. onmicrosoft.com Azure Active Directory-domein.

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryuserslisting.png)

We gaan Volg [deze instructies](https://technet.microsoft.com/library/hh967632.aspx#BKMK_1) in de volgende stappen een voorbeeld van een specifieke maar gebruiken.

Klik onder aan de pagina op **+ gebruiker toevoegen**. Typ de naam van de nieuwe gebruiker in de pagina die wordt weergegeven, en controleer de **Type gebruiker** een **nieuwe gebruiker in uw organisatie**. In dit voorbeeld wordt de naam van de nieuwe gebruiker is `ahmet`. Selecteer het standaarddomein die u gedetecteerd eerder als het domein voor ahmet van e-mailadres. Klik op de pijl volgende na voltooiing.

![](./media/virtual-machines-common-create-aad-work-id/addingauserwithdirectorydropdown.png)

Meer informatie voor Ahmet toevoegen, maar zorg ervoor dat u selecteert u de juiste **rol** waarde. Het is eenvoudig te gebruiken **globale beheerder** aanbrengen zeker dat dingen werkt, maar als u een minder rol kunt gebruiken, die is een goed idee. In dit voorbeeld wordt de **gebruiker** rol. (Meer informatie op [Administrator-machtigingen per rol](https://msdn.microsoft.com/library/azure/dn468213.aspx#BKMK_1).) Schakel multi-factor authentication niet, tenzij u wilt voor meervoudige verificatie voor elk logboek in bewerking. Wanneer u klaar bent, klikt u op de pijl Volgende.

![](./media/virtual-machines-common-create-aad-work-id/userprofileuseradmin.png)

Klik op de **maken** knop genereren en weergeven van een tijdelijk wachtwoord voor Ahmet.

![](./media/virtual-machines-common-create-aad-work-id/gettemporarypasswordforuser.png)

Kopieer de e-mailadres van de gebruiker de naam of gebruik **wachtwoord IN E-mail verzenden**. U moet de gegevens aan te melden binnen enkele ogenblikken.

![](./media/virtual-machines-common-create-aad-work-id/receivedtemporarypassworddialog.png)

Nu u de nieuwe gebruiker ziet **Ahmet de ontwikkelaar**, brongegevens van Azure Active Directory. U hebt nieuwe werk of school-identiteit gemaakt met Azure Active Directory. Echter, deze identiteit nog geen machtigingen voor het gebruik van Azure-resources.

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryusersaftercreate.png)

Als u **wachtwoord IN E-mail verzenden**, het volgende type e-mailbericht wordt verzonden.

![](./media/virtual-machines-common-create-aad-work-id/emailreceivedfromnewusercreation.png)

## <a name="adding-azure-co-administrator-rights-for-subscriptions"></a>Azure mede administrator-rechten voor abonnementen toe te voegen
Nu moet u de nieuwe gebruiker toevoegen als medebeheerder van uw abonnement, zodat de nieuwe gebruiker bij de beheerportal aanmelden kunt. U doet dit door in het deelvenster linksonder klikt u op **instellingen**.

![](./media/virtual-machines-common-create-aad-work-id/thesettingswidget.png)

Klik in het gebied belangrijkste instellingen **beheerders** bovenaan en u ziet alleen uw Microsoft-account persoonsgegevens. Klik onder aan de pagina op **+ toevoegen** om op te geven van een CO-beheerder. Voer hier het e-mailadres van de nieuwe gebruiker die u hebt gemaakt, met inbegrip van het standaarddomein. Zoals u in de volgende schermafbeelding, wordt een groen vinkje weergegeven naast de gebruiker voor de standaard-map. Vergeet niet om alle abonnementen op die u deze gebruiker kan dat wilt beheren te selecteren.

![](./media/virtual-machines-common-create-aad-work-id/addingnewuserascoadmin.png)

Wanneer u klaar bent, ziet u nu twee gebruikers, met inbegrip van de nieuwe medebeheerder-identiteit. Meld u af bij van de portal.

![](./media/virtual-machines-common-create-aad-work-id/newuseraddedascoadministrator.png)

## <a name="logging-in-and-changing-the-new-users-password"></a>Aanmelden en de nieuwe gebruiker-wachtwoord wijzigen
Aanmelden als de nieuwe gebruiker die u hebt gemaakt.

![](./media/virtual-machines-common-create-aad-work-id/signinginwithnewuser.png)

U wordt onmiddellijk gevraagd een nieuw wachtwoord maken.

![](./media/virtual-machines-common-create-aad-work-id/mustupdateyourpassword.png)

U moet met succes dat op de volgende lijkt beloond.

![](./media/virtual-machines-common-create-aad-work-id/successtourdialog.png)

## <a name="next-steps"></a>Volgende stappen
U kunt nu de nieuwe Azure Active Directory-identiteit gebruiken [Azure resource group sjablonen](../articles/xplat-cli-azure-resource-manager.md).

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
