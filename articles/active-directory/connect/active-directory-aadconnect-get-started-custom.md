---
title: 'Azure AD Connect: Aangepaste installatie | Microsoft Docs'
description: In dit document worden Hallo aangepaste installatieopties voor Azure AD Connect. Gebruik deze instructies tooinstall Active Directory met Azure AD Connect.
services: active-directory
keywords: wat is Azure AD Connect, Active Directory installeren, vereiste onderdelen voor Azure AD
documentationcenter: 
author: billmath
manager: femila
ms.assetid: 6d42fb79-d9cf-48da-8445-f482c4c536af
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: c49724fab78c5a1688662043f69506fff6f82104
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="custom-installation-of-azure-ad-connect"></a>Custom installation of Azure AD Connect (Engelstalig)
Azure AD Connect **aangepaste instellingen** wordt gebruikt wanneer u meer opties voor het Hallo-installatie wilt. Als u meerdere forests hebt of als u tooconfigure optionele functies niet behandeld in de snelle installatie hello wilt wordt gebruikt. Het wordt gebruikt in alle gevallen waarbij hello [ **snelle installatie** ](active-directory-aadconnect-get-started-express.md) optie voldoet niet aan uw implementatie of topologie.

Zorg voordat u begint met de installatie van Azure AD Connect te[Azure AD Connect downloadt](http://go.microsoft.com/fwlink/?LinkId=615771) en volledige Hallo vereiste stappen in [Azure AD Connect: Hardware en vereisten](active-directory-aadconnect-prerequisites.md). Zorg er ook voor dat de benodigde accounts beschikbaar zijn, zoals beschreven in [Azure AD Connect accounts and permissions](active-directory-aadconnect-accounts-permissions.md).

Als u aangepaste instellingen komt niet overeen met uw topologie, bijvoorbeeld tooupgrade DirSync, Zie [verwante documentatie](#related-documentation) voor andere scenario's.

## <a name="custom-settings-installation-of-azure-ad-connect"></a>Installatie van Azure AD Connect met aangepaste instellingen
### <a name="express-settings"></a>Snelle instellingen
Klik op deze pagina **aanpassen** toostart een installatie met aangepaste instellingen.

### <a name="install-required-components"></a>Vereiste onderdelen installeren
Wanneer u Hallo Synchronisatieservices installeert, kunt u de sectie optionele configuratie Hallo uitgeschakeld laten en Azure AD Connect stelt alles automatisch. Het programma stelt een exemplaar van SQL Server 2012 Express LocalDB, Hallo juiste groepen maken en machtigingen toe te wijzen. Als u toochange Hallo standaardwaarden wenst, kunt u Hallo volgend tabel toounderstand Hallo optionele configuratieopties die beschikbaar zijn.

![Vereiste onderdelen](./media/active-directory-aadconnect-get-started-custom/requiredcomponents.png)

| Optionele configuratie | Beschrijving |
| --- | --- |
| Een bestaande SQL Server gebruiken |Hiermee kunt u toospecify Hallo SQL Server en exemplaarnaam Hallo. Selecteer deze optie als u al een databaseserver dat u toouse wilt. Voer Hallo instantienaam gevolgd door een komma en poortnummer nummer in **exemplaarnaam** als uw SQL-Server geen bladeren is ingeschakeld. |
| Een bestaand serviceaccount gebruiken |Azure AD Connect maakt standaard gebruik van een virtuele-account voor Hallo synchronisatie services toouse. Als u een externe SQL server gebruiken of een proxy die verificatie vereist, moet u toouse een **beheerd serviceaccount** of gebruik van een serviceaccount in Hallo domein en Hallo wachtwoord weet. Voer in deze gevallen Hallo account toouse. Zorg ervoor dat Hallo gebruiker Hallo installatie uitvoert een SA in SQL zodat een aanmelding voor Hallo-serviceaccount kan worden gemaakt. Zie [Azure AD Connect accounts and permissions](active-directory-aadconnect-accounts-permissions.md#azure-ad-connect-sync-service-account) |
| Aangepaste synchronisatiegroepen opgeven |Azure AD Connect maakt standaard vier groepen lokaal toohello server wanneer de Synchronisatieservices Hallo zijn geïnstalleerd. Deze groepen zijn: groep Administrators, groep Operators, bladeren en Hallo groep voor wachtwoord opnieuw instellen. U kunt hier uw eigen groepen opgeven. Hallo groepen moeten lokaal op Hallo-server en kunnen niet worden gevonden in het Hallo-domein. |

### <a name="user-sign-in"></a>Gebruikersaanmelding
Na de installatie van onderdelen Hallo vereist, tooselect wordt u gevraagd enkele uw gebruikers de methode eenmalige aanmelding. Hallo volgende tabel geeft een korte beschrijving van de beschikbare opties Hallo. Zie voor een volledige beschrijving van Hallo aanmeldingsmethoden [gebruikersaanmelding](active-directory-aadconnect-user-signin.md).

![Aanmelding door een gebruiker](./media/active-directory-aadconnect-get-started-custom/usersignin2.png)

| Optie voor eenmalige aanmelding | Beschrijving |
| --- | --- |
| Wachtwoordsynchronisatie |Gebruikers kunnen toosign zijn in tooMicrosoft cloudservices, zoals Office 365, met behulp van Hallo hetzelfde wachtwoord dat ze gebruiken in hun on-premises netwerk. Hallo-wachtwoorden van gebruikers zijn gesynchroniseerd tooAzure AD als een wachtwoord-hash en verificatie vindt plaats in de cloud Hallo. Zie [Password synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) voor meer informatie. |
|Pass-through-verificatie (Preview)|Gebruikers kunnen toosign zijn in tooMicrosoft cloudservices, zoals Office 365, met behulp van Hallo hetzelfde wachtwoord dat ze gebruiken in hun on-premises netwerk.  Hallo gebruikers wachtwoord wordt doorgegeven via toohello lokale Active Directory-controller toobe gevalideerd.
| Federatie met AD FS |Gebruikers kunnen toosign zijn in tooMicrosoft cloudservices, zoals Office 365, met behulp van Hallo hetzelfde wachtwoord dat ze gebruiken in hun on-premises netwerk.  Hallo gebruikers worden omgeleid tootheir on-premises AD FS-exemplaar toosign in en verificatie vindt plaats op lokatie. |
| Niet configureren |Geen van beide onderdelen wordt geïnstalleerd en geconfigureerd. Kies deze optie als u al een federatieserver van derden of een andere bestaande oplossing heeft. |
|Eenmalige aanmelding inschakelen|Deze opties is beschikbaar met Wachtwoordsynchronisatie en Pass through-verificatie en eenmalige op ervaring biedt voor bureaubladgebruikers op Hallo bedrijfsnetwerk bevinden.  Zie [Eenmalige aanmelding](active-directory-aadconnect-sso.md) voor meer informatie. </br>Opmerking voor AD FS-klanten deze optie is niet beschikbaar omdat AD FS al aanbiedingen Hallo hetzelfde niveau van eenmalige aanmelding.</br>(als PTA niet op Hallo vrijgegeven wordt hetzelfde moment)
|Aanmeldingsoptie|Deze opties is beschikbaar voor wachtwoord sync klanten en eenmalige op ervaring biedt voor bureaubladgebruikers op Hallo bedrijfsnetwerk bevinden.  </br>Zie [Eenmalige aanmelding](active-directory-aadconnect-sso.md) voor meer informatie. </br>Opmerking voor AD FS-klanten deze optie is niet beschikbaar omdat AD FS al aanbiedingen Hallo hetzelfde niveau van eenmalige aanmelding.


### <a name="connect-tooazure-ad"></a>Verbinding maken met tooAzure AD
Voer een globale beheerdersaccount en het wachtwoord op Hallo Connect tooAzure AD scherm. Als u hebt geselecteerd **Federatie met AD FS** op de vorige pagina hello, niet aanmeldt met een account in een domein u van plan bent tooenable voor Federatie. Een aanbeveling is een account in Hallo standaard toouse **onmicrosoft.com** domein, wordt geleverd met uw Azure AD-directory.

Dit account wordt alleen gebruikt toocreate een serviceaccount in Azure AD en wordt niet gebruikt wanneer het Hallo-wizard is voltooid.  
![Aanmelding door een gebruiker](./media/active-directory-aadconnect-get-started-custom/connectaad.png)

Als uw globale beheerdersaccount MFA ingeschakeld heeft, moet u tooprovide Hallo wachtwoord opnieuw in Hallo aanmelden pop en volledige Hallo MFA uitdaging. Hallo controle kan bestaan uit een bieden een verificatiecode of een telefonische oproep.  
![Aanmelding door een gebruiker bij MFA](./media/active-directory-aadconnect-get-started-custom/connectaadmfa.png)

Hallo globale beheerdersaccount kan ook hebben [Privileged Identity Management](../active-directory-privileged-identity-management-getting-started.md) ingeschakeld.

Zie [Connectiviteitsproblemen oplossen](active-directory-aadconnect-troubleshoot-connectivity.md) als u een foutbericht krijgt en u problemen hebt met de connectiviteit.

## <a name="pages-under-hello-section-sync"></a>Pagina's onder Hallo sectie synchronisatie

### <a name="connect-your-directories"></a>Verbinding maken met uw directory’s
tooconnect tooyour Active Directory Domain Services, Azure AD Connect moet Hallo forestnaam en referenties van een account met voldoende machtigingen.

![Verbinding maken met Directory](./media/active-directory-aadconnect-get-started-custom/connectdir01.png)

Na het invoeren van de forestnaam Hallo en te klikken op **map toevoegen**, een pop-upvenster wordt weergegeven, waarna u Hello volgende opties:

| Optie | Beschrijving |
| --- | --- |
| Bestaand account gebruiken | Selecteer deze optie als u wilt dat toobe Azure AD Connect gebruikt voor het verbinden van toohello AD-forest tijdens de directorysynchronisatie tooprovide een bestaande AD DS-account. U kunt Hallo domeingedeelte in NetBios- of FQDN-indeling, dat wil zeggen FABRIKAM\syncuser of fabrikam.com\syncuser. Dit account kan een normaal gebruikersaccount worden, omdat alleen Hallo standaard leesmachtigingen nodig. Afhankelijk van uw scenario heeft u echter mogelijk meer machtigingen nodig. Zie [Azure AD Connect Accounts and permissions](active-directory-aadconnect-accounts-permissions.md#create-the-ad-ds-account) voor meer informatie. |
| Nieuw account maken | Selecteer deze optie als u wilt dat Azure AD Connect-wizard toocreate Hallo AD DS account voor Azure AD Connect is vereist voor het verbinden van toohello AD-forest tijdens de directorysynchronisatie. Wanneer deze optie is geselecteerd, Hallo gebruikersnaam en wachtwoord invoeren voor een enterprise-beheerdersaccount. Hallo enterprise-beheerdersaccount opgegeven wordt gebruikt door Azure AD Connect-wizard toocreate Hallo vereist AD DS-account. U kunt Hallo domeingedeelte in NetBios- of FQDN-indeling, dat wil zeggen FABRIKAM\administrator of fabrikam.com\administrator. |

![Verbinding maken met Directory](./media/active-directory-aadconnect-get-started-custom/connectdir02.png)


### <a name="azure-ad-sign-in-configuration"></a>Aanmeldconfiguratie Azure AD
Deze pagina kunt u tooreview Hallo UPN-domeinen zich in de lokale AD DS bevinden en in Azure AD zijn geverifieerd. Deze pagina kunt u ook tooconfigure Hallo kenmerk toouse voor Hallo userPrincipalName.

![Niet-geverifieerde domeinen](./media/active-directory-aadconnect-get-started-custom/aadsigninconfig.png)  
Bekijk elk domein waarbij **Niet toegevoegd** en **Niet geverifieerd** staat. Zorg ervoor dat de domeinen die u gebruikt in Azure AD zijn geverifieerd. Klik op de symbool vernieuwen Hallo wanneer u uw domeinen hebt geverifieerd. Zie voor meer informatie [toevoegen en het Hallo-domein verifiëren](../active-directory-add-domain.md)

**UserPrincipalName** -Hallo kenmerk userPrincipalName is Hallo kenmerk gebruikers gebruiken wanneer ze zich tooAzure AD en Office 365 aanmelden. Hallo domeinen gebruikt, ook wel bekend als Hallo UPN-achtervoegsel, moeten worden geverifieerd in Azure AD voordat Hallo gebruikers worden gesynchroniseerd. Microsoft raadt tookeep Hallo standaard kenmerk userPrincipalName. Als dit kenmerk niet routeerbaar is en kan niet worden geverifieerd, is het mogelijk tooselect een ander kenmerk. U kunt bijvoorbeeld e-mail selecteren als Hallo kenmerk bedrijf Hallo aanmeldings-ID. Het gebruik van een ander kenmerk dan userPrincipalName wordt **alternatieve id** genoemd. Hallo alternatieve id-kenmerkwaarde moet Hallo standaard RFC822 volgen. Een alternatieve id kan worden gebruikt met wachtwoordsynchronisatie en federatie.

>[!NOTE]
> Als u Pass-through-verificatie inschakelt, moet u ten minste één gecontroleerd domein in volgorde toocontinue via de wizard Hallo hebben.

> [!WARNING]
> Het gebruik van een alternatieve id is niet met alle Office 365-werkbelastingen compatibel. Voor meer informatie raadpleegt u te[Configuring Alternate Login ID](https://technet.microsoft.com/library/dn659436.aspx).
>
>

### <a name="domain-and-ou-filtering"></a>Domein- en OE-filters
Standaard worden alle domeinen en OE's gesynchroniseerd. Als er domeinen of organisatie-eenheden u wilt niet toosynchronize tooAzure AD, kunt u het vakje deze domeinen en organisatie-eenheden.  
![Domein- en OE-filters](./media/active-directory-aadconnect-get-started-custom/domainoufiltering.png)  
Deze pagina in de wizard Hallo worden geconfigureerd op basis van een domein en OE filters. Als u van plan toomake wijzigingen bent, Zie [filteren op basis van een domein](active-directory-aadconnectsync-configure-filtering.md#domain-based-filtering) en [filteren op basis van organisatie-eenheid](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) voordat u deze wijzigingen aanbrengt. Sommige organisatie-eenheden zijn essentieel voor het Hallo-functionaliteit en mag niet zijn uitgeschakeld.

Als u OE-filters gebruikt met een versie van Azure AD Connect lager dan 1.1.524.0, worden nieuwe OE's die later zijn toegevoegd, standaard gesynchroniseerd. Als u wilt dat Hallo gedrag dat nieuwe organisatie-eenheden moeten niet worden gesynchroniseerd en vervolgens kunt u deze configureren nadat Hallo wizard is voltooid met [filteren op basis van organisatie-eenheid](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering). Voor Azure AD Connect versie 1.1.524.0 of na, kunt u aangeven of u wilt dat nieuwe OE's toobe gesynchroniseerd of niet.

Als u van plan toouse bent [filteren op basis van een groep](#sync-filtering-based-on-groups), zorgt u ervoor Hallo organisatie-eenheid met Hallo-groep is opgenomen en niet worden gefilterd met OE filteren. OE filteren wordt geëvalueerd vóór groep filteren.

Het is ook mogelijk dat sommige domeinen niet bereikbaar vanwege toofirewall beperkingen zijn. Deze domeinen zijn standaard uitgeschakeld en hebben een waarschuwing.  
![Onbereikbare domeinen](./media/active-directory-aadconnect-get-started-custom/unreachable.png)  
Als u deze waarschuwing ziet, zorg ervoor dat deze domeinen inderdaad onbereikbaar zijn en Hallo waarschuwing wordt verwacht.

### <a name="uniquely-identifying-your-users"></a>Uw gebruikers een unieke id geven

#### <a name="select-how-users-should-be-identified-in-your-on-premises-directories"></a>Selecteren hoe gebruikers moeten worden aangeduid in uw on-premises directory’s
Hallo kunt functie overeenkomend in forests u toodefine hoe gebruikers van uw AD DS-forests worden weergegeven in Azure AD. Een gebruiker kan ofwel slechts één keer in alle forests worden weergegeven of een combinatie van ingeschakelde en uitgeschakelde accounts hebben. Hallo-gebruiker kan ook worden weergegeven als een contactpersoon in sommige forests.

![Uniek](./media/active-directory-aadconnect-get-started-custom/unique.png)

| Instelling | Beschrijving |
| --- | --- |
| [Gebruikers worden slechts één keer weergegeven in alle forests](active-directory-aadconnect-topologies.md#multiple-forests-single-azure-ad-tenant) |Alle gebruikers worden als afzonderlijke objecten in Azure AD aangemaakt. Hallo-objecten zijn niet gekoppeld in Hallo metaverse. |
| [E-mailkenmerk](active-directory-aadconnect-topologies.md#multiple-forests-single-azure-ad-tenant) |Deze optie koppelt gebruikers en contactpersonen als e-mailkenmerk Hallo Hallo dezelfde in verschillende forests waarde. Gebruik deze optie wanneer uw contactpersonen met behulp van GALSync zijn aangemaakt. Als u deze optie kiest, worden gebruikersobjecten waarvan e-mailkenmerk zijn niet ingevuld gesynchroniseerde tooAzure AD niet. |
| [ObjectSID en msExchangeMasterAccountSID / msRTCSIP-OriginatorSid](active-directory-aadconnect-topologies.md#multiple-forests-single-azure-ad-tenant) |Deze optie koppelt een ingeschakelde gebruiker in een account-forest met een uitgeschakelde gebruiker in een bron-forest. In Exchange wordt deze configuratie een gekoppeld postvak genoemd. Deze optie kan ook worden gebruikt als u alleen Lync gebruikt en Exchange niet aanwezig in Hallo bron-forest is. |
| sAMAccountName en MailNickName |Deze optie koppelt kenmerken waarbij het verwachte Hallo aanmeldings-ID is voor Hallo-gebruiker kan worden gevonden. |
| Een specifiek kenmerk |Deze optie kunt u tooselect uw eigen kenmerk. Als u deze optie kiest, worden gebruikersobjecten waarvan het kenmerk (geselecteerd) zijn niet ingevuld gesynchroniseerde tooAzure AD niet. **Beperking:** Zorg ervoor dat toopick een kenmerk dat al u in Hallo metaverse vindt. Als u een aangepast kenmerk kiest (niet in de metaverse Hallo), Hallo wizard kan niet worden voltooid. |

#### <a name="select-how-users-should-be-identified-with-azure-ad---source-anchor"></a>Selecteren hoe gebruikers moeten worden aangeduid met Azure AD - bronanker
Hallo kenmerk sourceAnchor is een kenmerk is onveranderbaar tijdens Hallo levensduur van een gebruikersobject. Het is de primaire sleutel Hallo Hallo on-premises gebruiker aan Hallo gebruiker koppelen in Azure AD.

| Instelling | Beschrijving |
| --- | --- |
| Azure Hallo bronanker beheren voor mij laten | Selecteer deze optie als u wilt dat Azure AD toopick Hallo kenmerk voor u. Als u deze optie selecteert, Azure AD Connect-wizard van toepassing hello sourceAnchor kenmerk selectie logica in sectie artikel [Azure AD Connect: concepten - msDS-ConsistencyGuid met als sourceAnchor ontwerpen](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor). Hallo wizard informeert u welk kenmerk is opgenomen als Hallo Bronanker kenmerk nadat aangepaste installatie is voltooid. |
| Een specifiek kenmerk | Selecteer deze optie als u een bestaand AD-kenmerk als Hallo sourceAnchor kenmerk toospecify wenst. |

Aangezien het Hallo-kenmerk kan niet worden gewijzigd, moet u plannen voor een goed kenmerk toouse. Een goede kandidaat is objectGUID. Dit kenmerk is niet gewijzigd, tenzij het Hallo-gebruikersaccount worden verplaatst tussen forests/domeinen. In een omgeving met meerdere forests als u accounts tussen forests verplaatst, moet een ander kenmerk worden gebruikt, zoals een kenmerk met de Hallo werknemer-id. Vermijd kenmerken die wijzigen wanneer iemand trouwt of een andere taak krijgt. U kunt geen kenmerken met een @-sign gebruiken, dus het e-mailadres en userPrincipalName kunnen niet worden gebruikt. Hallo-kenmerk is ook hoofdlettergevoelig dus wanneer u een object tussen forests verplaatst, zorg ervoor dat toopreserve Hallo hoofdletters en kleine letters. Binaire kenmerken krijgen base64-codering, maar andere kenmerktypen blijven ongecodeerd. In scenario's met federatie en in sommige Azure AD-interfaces wordt dit kenmerk ook wel onveranderbare id genoemd. Meer informatie over Hallo bronanker vindt u in Hallo [concepten ontwerpen](active-directory-aadconnect-design-concepts.md#sourceanchor).

### <a name="sync-filtering-based-on-groups"></a>Synchronisatiefilters op basis van groepen
Hallo functie filteren op groep kunt u toosync slechts een kleine subset van objecten voor een Pilotimplementatie. toouse die deze functie, een groep maken voor dit doel in uw lokale Active Directory. Voeg gebruikers en groepen die gesynchroniseerd tooAzure AD als rechtstreekse leden worden moeten. U kunt later toevoegen en verwijderen van gebruikers toothis groep toomaintain Hallo lijst van objecten die opgenomen in Azure AD zijn. Alle objecten die u wilt dat toosynchronize moet een direct lid van groep Hallo. Gebruikers, groepen, contactpersonen en computers/apparaten moeten allemaal directe leden zijn. Genest groepslidmaatschap is niet opgelost. Wanneer u een groep toevoegt als een lid, alleen Hallo groep zelf toegevoegd en niet de leden ervan.

![Synchronisatiefilters](./media/active-directory-aadconnect-get-started-custom/filter2.png)

> [!WARNING]
> Deze functie is alleen bedoeld toosupport een proef-implementatie. Gebruik deze functie niet bij een volledige productie-implementatie.
>
>

In een volledige productie-implementatie gaat deze toobe harde toomaintain één groep met alle objecten toosynchronize. In plaats daarvan moet u een van de methoden Hallo in [Configure filtering](active-directory-aadconnectsync-configure-filtering.md).

### <a name="optional-features"></a>Optionele functies
Dit scherm kunt u tooselect Hallo optionele functies voor uw specifieke scenario's.

![Optionele functies](./media/active-directory-aadconnect-get-started-custom/optional.png)

> [!WARNING]
> Als u momenteel DirSync of Azure AD Sync active hebt, hebt u Hallo Write-back van functies in Azure AD Connect niet geactiveerd.
>
>

| Optionele functies | Beschrijving |
| --- | --- |
| Hybride implementatie voor Exchange |Hallo hybride implementatie voor Exchange-functie kunt u naast elkaar bestaan Hallo van Exchange-postvakken zowel on-premises en in Office 365. Azure AD Connect synchroniseert een specifieke set [kenmerken](active-directory-aadconnectsync-attributes-synchronized.md#exchange-hybrid-writeback) vanuit Azure AD naar uw on-premises directory. |
| Openbare e-mailmappen van Exchange | Hallo openbare mappen van Exchange Mail-functie kunt u toosynchronize e-mailfunctionaliteit objecten uit uw lokale Active Directory tooAzure AD openbare map. |
| Azure AD-app- en -kenmerkfilters |U Azure AD-app en kenmerkfilters inschakelt, kan hello set gesynchroniseerde kenmerken worden aangepast. Deze optie worden twee meer pagina's toohello configuratiewizard toegevoegd. Zie voor meer informatie [Azure AD app and attribute filtering](#azure-ad-app-and-attribute-filtering). |
| Wachtwoordsynchronisatie |Als u Federatie als oplossing voor aanmelden Hallo hebt geselecteerd, kunt u deze optie inschakelen. Wachtwoordsynchronisatie kan vervolgens als een backupoptie worden gebruikt. Zie [Password synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) voor meer informatie. </br></br>Als u Pass-through-verificatie geselecteerd is deze optie is ingeschakeld door standaard tooensure ondersteuning voor oudere clients, en als een optie voor back-up. Zie [Password synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) voor meer informatie.|
| Wachtwoord terugschrijven |Als u terugschrijven van wachtwoord inschakelt, wachtwoordwijzigingen in Azure AD teruggeschreven tooyour on-premises adreslijst. Zie voor meer informatie [Getting started with password management](../active-directory-passwords-getting-started.md). |
| Groep terugschrijven |Als u Hallo **Office 365-groepen** functies, dan kunnen deze groepen weergegeven in uw lokale Active Directory. Deze optie is alleen beschikbaar als Exchange in uw on-premises Active Directory aanwezig is. Zie voor meer informatie [Group writeback](active-directory-aadconnect-feature-preview.md#group-writeback). |
| Apparaat terugschrijven |Hiermee kunt u apparaatobjecten toowriteback op Azure AD tooyour on-premises Active Directory voor scenario's voor voorwaardelijke toegang. Zie voor meer informatie [Enabling device writeback in Azure AD Connect](active-directory-aadconnect-feature-device-writeback.md). |
| Synchronisatie van directory-extensiekenmerken |Doordat de synchronisatie van directory-uitbreidingen zijn opgegeven kenmerken gesynchroniseerd tooAzure AD. Zie voor meer informatie [Directory extensions](active-directory-aadconnectsync-feature-directory-extensions.md). |

### <a name="azure-ad-app-and-attribute-filtering"></a>Azure AD-app- en -kenmerkfilters
Als u wilt dat toolimit welke kenmerken toosynchronize tooAzure AD, begin dan met te selecteren welke services u gebruikt. Als u configuratiewijzigingen op deze pagina aanbrengt, heeft een nieuwe service toobe expliciet door Hallo-installatiewizard opnieuw uit te worden geselecteerd.

![Optionele functies apps](./media/active-directory-aadconnect-get-started-custom/azureadapps2.png)

Deze pagina is gebaseerd op Hallo-services in de vorige stap Hallo hebt geselecteerd, bevat alle kenmerken die zijn gesynchroniseerd. In deze lijst staan alle objecttypen die worden gesynchroniseerd. Als er een aantal specifieke kenmerken, moet u toonot synchroniseren, kunt u het vakje deze kenmerken.

![Optionele functies kenmerken](./media/active-directory-aadconnect-get-started-custom/azureadattributes2.png)

> [!WARNING]
> Het verwijderen van kenmerken kan invloed hebben op de functionaliteit. Zie voor aanbevolen procedures en andere aanbevelingen [attributes synchronized](active-directory-aadconnectsync-attributes-synchronized.md#attributes-to-synchronize).
>
>

### <a name="directory-extension-attribute-sync"></a>Synchronisatie van directory-extensiekenmerken
U kunt Hallo schema in Azure AD uitbreiden met aangepaste kenmerken die door uw organisatie of andere kenmerken in Active Directory toegevoegd. toouse deze functie, selecteer **Directory-extensiekenmerken** op Hallo **optionele functies** pagina. U kunt meer kenmerken toosync op deze pagina kunt selecteren.

![Uitbreidingen van de directory](./media/active-directory-aadconnect-get-started-custom/extension2.png)

Zie voor meer informatie [Directory extensions](active-directory-aadconnectsync-feature-directory-extensions.md).

### <a name="enabling-single-sign-on-sso"></a>Eenmalige aanmelding (SSO) inschakelen
Configureren van eenmalige aanmelding voor gebruik met Wachtwoordsynchronisatie of Pass through-verificatie is een eenvoudig proces dat hoeft u alleen toocomplete eenmaal voor elk forest dat gesynchroniseerd tooAzure AD wordt. De configuratie omvat de volgende twee stappen:

1.  De benodigde computeraccount Hallo maken in uw lokale Active Directory.
2.  Configureer de intranetzone Hallo van clientcomputers Hallo toosupport eenmalige aanmelding.

#### <a name="create-hello-computer-account-in-active-directory"></a>Hallo-computeraccount in Active Directory maken
Voor elke forest die is toegevoegd in Azure AD Connect, moet u domeinbeheerdersreferenties toosupply zodat Hallo-computeraccount in elk forest kan worden gemaakt. Hallo referenties zijn alleen gebruikte toocreate Hallo-account en niet opgeslagen of gebruikt voor een andere bewerking. Eenvoudig hello referenties toevoegen op Hallo **Schakel eenmalige aanmelding** pagina van hello Azure AD Connect-wizard zoals wordt weergegeven:

![Eenmalige aanmelding inschakelen](./media/active-directory-aadconnect-get-started-custom/enablesso.png)

>[!NOTE]
>U kunt een bepaald forest overslaan als u niet dat toouse enkelvoudige aanmelding met dat forest wenst.

#### <a name="configure-hello-intranet-zone-for-client-machines"></a>Hallo intranetzone voor client-computers configureren
Hallo client aanmeldingen automatisch op Hallo intranet zone u tooensure moet tooensure dat twee URL's deel uitmaken van de intranetzone Hallo. Dit zorgt ervoor dat Hallo domeincomputer automatisch een Kerberos-ticket tooAzure AD wanneer het bedrijfsnetwerk verbonden toohello is verzonden.
Op een computer waarop Hallo Group Policy management-hulpprogramma's.

1.  Open Hallo Group Policy Management tools
2.  Hallo-Groepsbeleid die toegepast tooall gebruikers worden bewerken. Bijvoorbeeld: hello standaarddomeinbeleid.
3.  Navigeer te**Configuration\Administrative Templates\Windows Explorer\Onderdeel Internet Control Panel\Security op de gebruikerspagina** en selecteer **tooZone lijst van zonetoewijzingen Site** per Hallo-afbeelding hieronder.
4.  Hallo-beleid inschakelen en voer de volgende twee items in het dialoogvenster Hallo Hallo.

        Value: `https://autologon.microsoftazuread-sso.com`  
        Data: 1  
        Value: `https://aadg.windows.net.nsatc.net`  
        Data: 1

5.  Dit ziet vergelijkbare toohello volgende:  
![Intranetzones](./media/active-directory-aadconnect-get-started-custom/sitezone.png)

6.  Klik twee keer op **OK**.

## <a name="configuring-federation-with-ad-fs"></a>Federatie configureren met AD FS
AD FS is heel eenvoudig met een paar muisklikken met Azure AD Connect te configureren. Hallo volgende is vereist voordat de Hallo-configuratie.

* Een Windows Server 2012 R2-server voor de federatieserver Hallo met extern beheer ingeschakeld
* Een Windows Server 2012 R2-server voor Hallo Web Application Proxy server met extern beheer ingeschakeld
* Een SSL-certificaat voor Hallo federation service-naam die u van plan bent toouse (bijvoorbeeld sts.contoso.com)

### <a name="ad-fs-configuration-pre-requisites"></a>Vereisten voor de AD FS-configuratie
tooconfigure uw AD FS-farm met Azure AD Connect, zorg WinRM is ingeschakeld op externe servers Hallo. Bovendien doorlopen Hallo vereisten voor poorten die worden vermeld in [Table 3 - Azure AD Connect en Federation Servers/WAP](active-directory-aadconnect-ports.md#table-3---azure-ad-connect-and-ad-fs-federation-serverswap).

### <a name="create-a-new-ad-fs-farm-or-use-an-existing-ad-fs-farm"></a>Maak een nieuwe AD FS-farm aan of gebruik een bestaande AD FS-farm
U kunt een bestaande AD FS-farm gebruiken of u kunt toocreate een nieuwe AD FS-farm. Als u een nieuw wachtwoord toocreate kiezen, bent u vereiste tooprovide Hallo SSL-certificaat. Als Hallo SSL-certificaat is beveiligd met een wachtwoord, wordt u gevraagd Hallo wachtwoord op te geven.

![AD FS-Farm](./media/active-directory-aadconnect-get-started-custom/adfs1.png)

Als u op een bestaande AD FS-farm toouse kiest, gaat u rechtstreeks toohello Hallo vertrouwensrelatie tussen AD FS en Azure AD-scherm configureren.

### <a name="specify-hello-ad-fs-servers"></a>Hallo AD FS-servers opgeven
Voer Hallo-servers die op het gewenste tooinstall AD FS. U kunt naar gelang de behoeften van uw capaciteitsplanning een of meer servers toevoegen. Voeg alle servers tooActive Directory voordat u deze configuratie uitvoert. Het wordt door Microsoft aangeraden om voor proefimplementaties één AD FS-server te installeren. Voeg vervolgens en meer servers toomeet uw schaalbehoeften implementeren door het uitvoeren van Azure AD Connect opnieuw na de initiële configuratie.

> [!NOTE]
> Zorg ervoor dat alle servers die lid tooan AD-domein voordat u deze configuratie.
>
>

![AD FS-Servers](./media/active-directory-aadconnect-get-started-custom/adfs2.png)

### <a name="specify-hello-web-application-proxy-servers"></a>Hallo Web Application Proxy-servers opgeven
Hallo-servers die u wilt gebruiken als uw webtoepassingsproxyservers invoeren. webtoepassingsproxy-server Hallo in uw DMS (extranetgericht) is geïmplementeerd en ondersteunt verificatieaanvragen van Hallo extranet. U kunt naar gelang de behoeften van uw capaciteitsplanning een of meer servers toevoegen. Het wordt door Microsoft aangeraden om voor proefimplementaties één webtoepassingsproxyserver te installeren. Voeg vervolgens en meer servers toomeet uw schaalbehoeften implementeren door het uitvoeren van Azure AD Connect opnieuw na de initiële configuratie. Het aan te raden een gelijk aantal servers toosatisfy proxyverificatie van Hallo intranet.

> [!NOTE]
> <li> Als Hallo account dat u gebruikt geen lokale beheerder op Hallo AD FS-servers, wordt u gevraagd om beheerreferenties.</li>
> <li> Zorg ervoor dat er HTTP/HTTPS-verbinding tussen hello Azure AD Connect-server en Hallo Web Application Proxy server voordat u deze stap uitvoert.</li>
> <li> Zorg ervoor dat er HTTP/HTTPS-verbinding tussen Hallo webtoepassingsserver en Hallo AD FS-server tooallow verificatie aanvragen tooflow via is.</li>
>

![Web-app](./media/active-directory-aadconnect-get-started-custom/adfs3.png)

U bent na vragen aan gebruiker tooenter referenties zodat hello webtoepassingsserver een beveiligde verbinding toohello AD FS-server bepalen kunt. Deze referenties moeten toobe een lokale beheerder op Hallo AD FS-server.

![Proxy](./media/active-directory-aadconnect-get-started-custom/adfs4.png)

### <a name="specify-hello-service-account-for-hello-ad-fs-service"></a>Hallo-serviceaccount voor Hallo AD FS-service opgeven
Hallo AD FS-service moet een domein service account tooauthenticate gebruikers en de gebruikersgegevens opzoeken in Active Directory. De service kan twee soorten serviceaccounts ondersteunen:

* **Beheerd serviceaccount voor groepen** - Geïntroduceerd in Active Directory-domainservices met WindowsServer 2012. Dit type account biedt services, zoals AD FS, één account zonder tooupdate Hallo accountwachtwoord regelmatig. Gebruik deze optie als u al Windows Server 2012-domeincontrollers in Hallo domein waarbij uw AD FS-servers horen.
* **Domeingebruikersaccount** -dit type account moet u tooprovide een wachtwoord en regelmatig bijwerken van wachtwoorden Hallo wanneer Hallo wachtwoord wordt gewijzigd of verlopen. Gebruik deze optie alleen als er geen Windows Server 2012-domeincontrollers in Hallo domein waarbij uw AD FS-servers horen.

Als u Beheerd serviceaccount voor groepen heeft geselecteerd en deze functie nog nooit in Active Directory is gebruikt, wordt u gevraagd om referenties van de ondernemingsbeheerder. Deze referenties zijn gebruikte tooinitiate Hallo sleutelarchief en Hallo-functie in Active Directory inschakelen.

> [!NOTE]
> Azure AD Connect voert een toodetect selectievakje uit als Hallo AD FS-service is al geregistreerd als een SPN in Hallo-domein.  AD DS, staat niet toe dat dubbele SPN toobe in één keer worden geregistreerd.  Als een dubbele SPN wordt gevonden, zich u niet meer kunnen tooproceed totdat Hallo SPN is verwijderd.

![AD FS-serviceaccount](./media/active-directory-aadconnect-get-started-custom/adfs5.png)

### <a name="select-hello-azure-ad-domain-that-you-wish-toofederate"></a>Selecteer hello Azure AD-domein dat u wenst dat toofederate
Deze configuratie is gebruikte toosetup hello federatieverbinding tussen AD FS en Azure AD. Hiermee configureert u de AD FS tooissue beveiliging tokens tooAzure AD en configureert deze Azure AD tootrust Hallo tokens van deze specifieke AD FS-instantie. Deze pagina kunt u alleen tooconfigure één domein in de eerste installatie Hallo. U kunt later meer domeinen configureren door Azure AD Connect nogmaals uit te voeren.

![Azure AD-domein](./media/active-directory-aadconnect-get-started-custom/adfs6.png)

### <a name="verify-hello-azure-ad-domain-selected-for-federation"></a>Controleer hello Azure AD-domein voor Federatie is geselecteerd
Wanneer u Hallo domein toobe federatieve selecteert, beschikt Azure AD Connect u over benodigde informatie tooverify een niet-geverifieerd domein. Zie [toevoegen en controleer Hallo domein](../active-directory-add-domain.md) voor het toouse deze informatie.

![Azure AD-domein](./media/active-directory-aadconnect-get-started-custom/verifyfeddomain.png)

> [!NOTE]
> AD Connect probeert tooverify Hallo domein tijdens Hallo fase configureren. Als u tooconfigure doorgaat zonder Hallo benodigde DNS-records toe te voegen, wordt Hallo wizard configuratie niet kunnen toocomplete Hallo.
>
>

## <a name="configure-and-verify-pages"></a>Configureer en verifieer pagina 's
Hallo-configuratie wordt uitgevoerd op deze pagina.

> [!NOTE]
> Als u de federatie heeft geconfigureerd, zorg dan dat u, voordat u doorgaat met de installatie, de [Naamomzetting voor federatieservers](active-directory-aadconnect-prerequisites.md#name-resolution-for-federation-servers) heeft geconfigureerd.
>
>

![Gereed tooconfigure](./media/active-directory-aadconnect-get-started-custom/readytoconfigure2.png)

### <a name="staging-mode"></a>Faseringsmodus
Het is mogelijk toosetup een nieuwe synchronisatieserver parallel met de faseringsmodus. Alleen ondersteunde toohave één synchronisatieserver tooone map in de cloud Hallo exporteren is. Maar als u wilt dat toomove vanaf een andere server, bijvoorbeeld één met DirSync, dan kunt u inschakelen Azure AD Connect in de faseringsmodus. Wanneer ingeschakeld, Hallo sync engine importeren en synchroniseren van gegevens als normale, maar hij exporteert tooAzure AD of AD. Hallo functies Wachtwoordsynchronisatie en wachtwoord terugschrijven van wachtwoorden zijn uitgeschakeld in de faseringsmodus.

![Faseringsmodus](./media/active-directory-aadconnect-get-started-custom/stagingmode.png)

In de faseringsmodus is mogelijk toomake vereiste wijzigingen toohello synchronisatie-engine en controleren wat over toobe geëxporteerd. Hallo configuratie er goed uitziet, Hallo-installatiewizard opnieuw uitvoeren als de faseringsmodus uitschakelt. Gegevens zijn nu geëxporteerde tooAzure AD van deze server. Zorg ervoor dat toodisable Hallo andere server op Hallo dezelfde zodat slechts één tijdserver actief aan het exporteren.

Zie voor meer informatie [Staging mode](active-directory-aadconnectsync-operations.md#staging-mode).

### <a name="verify-your-federation-configuration"></a>Controleer uw federatieconfiguratie
Azure AD Connect verifieert Hallo DNS-instellingen voor u wanneer u op de knop controleren Hallo.

**Controles voor connectiviteit intranet**

* Los federation FQDN-naam: Azure AD Connect controles als Hallo federation FQDN-naam kan worden opgelost door de DNS-tooensure connectiviteit. Als Azure AD Connect Hallo FQDN-naam kan niet worden omgezet, mislukt de verificatie van Hallo. Zorg ervoor dat een DNS-record voor Hallo federatieservice FQDN volgorde toosuccessfully voltooid Hallo verificatie aanwezig.
* DNS A-record: Azure AD Connect controleert of er een A-record is voor uw federatieservice. Hallo ontbreken van een A-record mislukt Hallo verificatie. Maken van een A-record en geen CNAME-record voor uw federatieserver FQDN in volgorde toosuccessfully Hallo-verificatie is voltooid.

**Controles voor connectiviteit extranet**

* Los federation FQDN-naam: Azure AD Connect controles als Hallo federation FQDN-naam kan worden opgelost door de DNS-tooensure connectiviteit.

![Voltooien](./media/active-directory-aadconnect-get-started-custom/completed.png)

![Verifiëren](./media/active-directory-aadconnect-get-started-custom/adfs7.png)

Voer Daarnaast Hallo verificatiestappen volgen:

* Valideren dat u zich via een browser op een domein gekoppelde computer op Hallo intranet aanmelden kunt: verbinding maken met toohttps://myapps.microsoft.com en controleer of Hallo aanmelden met uw aangemelde account. Hallo ingebouwde AD DS administrator-account is niet gesynchroniseerd en kan niet worden gebruikt voor verificatie.
* Valideren dat u zich met een apparaat vanaf Hallo extranet aanmelden kunt. Op een computer thuis of een mobiel apparaat verbinding toohttps://myapps.microsoft.com en voer uw referenties.
* Aanmelding uitgebreide client controleren. Verbinding maken met toohttps://testconnectivity.microsoft.com, kiest u Hallo **Office 365** tabblad en kies Hallo **Office 365 Single Sign-On-Test**.

## <a name="next-steps"></a>Volgende stappen
Nadat het Hallo-installatie is voltooid, afmelden en opnieuw tooWindows aanmelden voordat u Synchronization Service Manager of Synchronization Rule Editor gebruiken.

Nu u Azure AD Connect geïnstalleerd hebt kunt u [Hallo installatie verifiëren en licenties toewijzen](active-directory-aadconnect-whats-next.md).

Meer informatie over deze functies, die Hallo-installatie zijn ingeschakeld: [onopzettelijk verwijderen voorkomen](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md) en [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health-sync.md).

Meer informatie over deze veelvoorkomende onderwerpen: [scheduler en hoe tootrigger synchronisatie](active-directory-aadconnectsync-feature-scheduler.md).

Lees meer over het [integreren van uw on-premises identiteiten met Azure Active Directory ](active-directory-aadconnect.md).
