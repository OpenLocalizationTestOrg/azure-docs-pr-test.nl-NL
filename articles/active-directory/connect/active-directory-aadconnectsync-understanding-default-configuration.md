---
title: 'Azure AD Connect-synchronisatie: inzicht Hallo standaardconfiguratie | Microsoft Docs'
description: In dit artikel beschrijft de standaardconfiguratie Hallo in Azure AD Connect-synchronisatie.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: ed876f22-6892-4b9d-acbe-6a2d112f1cd1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 1cf95759af913cad8a1393839d3a836434e7c9bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understanding-hello-default-configuration"></a>Azure AD Connect-synchronisatie: inzicht Hallo standaardconfiguratie
Dit artikel wordt uitgelegd Hallo out of box configuratieregels. Deze documenten Hallo regels en de invloed van deze regels op Hallo-configuratie. Ook wordt u begeleid Hallo standaardconfiguratie van Azure AD Connect-synchronisatie. Hallo-doel is dat Hallo lezer hoe de configuratiemodel hello begrijpt, met de naam declaratieve inrichting werkt in een voorbeeld van een echte. In dit artikel wordt ervan uitgegaan dat u al hebt geïnstalleerd en Azure AD Connect-synchronisatie met de installatiewizard Hallo configureren.

toounderstand hello details van Hallo configuratiemodel lezen [Understanding declaratieve inrichting](active-directory-aadconnectsync-understanding-declarative-provisioning.md).

## <a name="out-of-box-rules-from-on-premises-tooazure-ad"></a>Out of box regels uit lokale tooAzure AD
Hallo volgende expressies vindt u in Hallo out-of-box-configuratie.

### <a name="user-out-of-box-rules"></a>Gebruiker out-of-box-regels
Deze regels gelden ook toohello iNetOrgPerson-objecttype.

Een gebruikersobject moet voldoen aan Hallo toobe gesynchroniseerd te volgen:

* Moet een sourceAnchor hebben.
* Na het Hallo-object is gemaakt in Azure AD en sourceAnchor kan niet worden gewijzigd. Als Hallo waarde gewijzigde lokale, Hallo object stopt synchroniseren totdat Hallo sourceAnchor back tooits vorige waarde wordt gewijzigd.
* Hebben moet Hallo accountEnabled (userAccountControl) kenmerk ingevuld. Met een lokale Active Directory dit kenmerk is altijd aanwezig zijn en worden ingevuld.

Hallo na gebruikersobjecten worden **niet** tooAzure AD gesynchroniseerd:

* `IsPresent([isCriticalSystemObject])`. Zorg ervoor dat veel out-of-box-objecten in Active Directory, zoals Hallo ingebouwde administrator-account, zijn niet gesynchroniseerd.
* `IsPresent([sAMAccountName]) = False`. Zorg ervoor dat gebruikersobjecten zonder sAMAccountName-kenmerk zijn niet gesynchroniseerd. Deze aanvraag zou alleen vrijwel gebeuren in een upgrade uitgevoerd van NT4-domein.
* `Left([sAMAccountName], 4) = "AAD_"`, `Left([sAMAccountName], 5) = "MSOL_"`. Hallo-serviceaccount die wordt gebruikt door Azure AD Connect-synchronisatie en de eerdere versies niet synchroniseren.
* Niet synchroniseren met Exchange-accounts die niet in Exchange Online werkt.
  * `[sAMAccountName] = "SUPPORT_388945a0"`
  * `Left([mailNickname], 14) = "SystemMailbox{"`
  * `(Left([mailNickname], 4) = "CAS_" && (InStr([mailNickname], "}") > 0))`
  * `(Left([sAMAccountName], 4) = "CAS_" && (InStr([sAMAccountName], "}")> 0))`
* Objecten die niet in Exchange Online werkt niet synchroniseren.
  `CBool(IIF(IsPresent([msExchRecipientTypeDetails]),BitAnd([msExchRecipientTypeDetails],&H21C07000) > 0,NULL))`  
  Deze bitmasker (& H21C07000) filtert uit Hallo objecten te volgen:
  * E-mailfunctionaliteit openbare map
  * Eigen Postvak
  * Postvak Database postvak (systeempostvak)
  * De universele beveiligingsgroep (wouldn't gelden voor een gebruiker, maar is omwille van de verouderde aanwezig)
  * Niet-universele groep (wouldn't gelden voor een gebruiker, maar is omwille van de verouderde aanwezig)
  * Postvak plannen
  * Detectie Postvak
* `CBool(InStr(DNComponent(CRef([dn]),1),"\\0ACNF:")>0)`. De replicatie slachtoffer objecten niet synchroniseren.

Hallo kenmerk regels toepassen:

* `sourceAnchor <- IIF([msExchRecipientTypeDetails]=2,NULL,..)`. Hallo sourceAnchor kenmerk is niet een gekoppeld postvak bijgedragen. Ervan wordt uitgegaan dat als een gekoppeld postvak is gevonden, de daadwerkelijke account Hallo deel van later uitmaakt.
* Exchange gerelateerde kenmerken worden alleen gesynchroniseerd als hello kenmerk **mailNickName** heeft een waarde.
* Wanneer er meerdere forests, worden de kenmerken in de volgorde Hallo verbruikt:
  1. Kenmerken die zijn gerelateerd toosign in (voor voorbeeld userPrincipalName) bijgedragen uit Hallo-forest met een account ingeschakeld.
  2. Kenmerken die kunnen worden gevonden in een Exchange-GAL (globale adreslijst) worden bijgedragen Hallo-forest met een Exchange-postvak.
  3. Als geen postvak kan worden gevonden, vervolgens deze kenmerken kunnen afkomstig zijn van een forest.
  4. Exchange gerelateerde kenmerken (niet zichtbaar in Hallo GAL technische kenmerken) worden aangeleverd uit Hallo forest waar `mailNickname ISNOTNULL`.
  5. Als er meerdere forests die u zou een van deze regels voldoen aan en klik vervolgens Hallo is maken volgorde (datum/tijd) van Hallo Connectors (forests) gebruikte toodetermine welk forest Hallo kenmerken bijdraagt.

### <a name="contact-out-of-box-rules"></a>Neem contact op met out-of-box-regels
Een contact-object moet voldoen aan Hallo toobe gesynchroniseerd te volgen:

* Hallo contact moet e-mailfunctionaliteit. Het is geverifieerd met Hallo volgens de regels voor:
  * `IsPresent([proxyAddresses]) = True)`. Hallo proxyAddresses kenmerk moet worden ingevuld.
  * In Hallo proxyAddresses kenmerk of het e-mailkenmerk Hallo vindt u een primaire e-mailadres. Hallo aanwezigheid van een @ is gebruikte tooverify dat Hallo inhoud een e-mailadres is. Een van deze twee regels moet geëvalueerde tooTrue.
    * `(Contains([proxyAddresses], "SMTP:") > 0) && (InStr(Item([proxyAddresses], Contains([proxyAddresses], "SMTP:")), "@") > 0))`. Is er een vermelding met ' SMTP: ' en als er, kunt u een @ worden gevonden in de tekenreeks Hallo?
    * `(IsPresent([mail]) = True && (InStr([mail], "@") > 0)`. Hallo e-mailkenmerk ingevuld en als dit het geval is, kunt een @ worden gevonden in de tekenreeks Hallo?

Hallo na contact op met objecten zijn **niet** tooAzure AD gesynchroniseerd:

* `IsPresent([isCriticalSystemObject])`. Zorg ervoor dat er geen contact op met objecten die als kritiek zijn gemarkeerd zijn gesynchroniseerd. Mag niet bestaan uit een met een standaardconfiguratie.
* `((InStr([displayName], "(MSOL)") > 0) && (CBool([msExchHideFromAddressLists])))`.
* `(Left([mailNickname], 4) = "CAS_" && (InStr([mailNickname], "}") > 0))`. Deze objecten goed niet in Exchange Online.
* `CBool(InStr(DNComponent(CRef([dn]),1),"\\0ACNF:")>0)`. De replicatie slachtoffer objecten niet synchroniseren.

### <a name="group-out-of-box-rules"></a>Groep out-of-box-regels
Een group-object moet voldoen aan Hallo toobe gesynchroniseerd te volgen:

* Moet minder dan 50.000 leden hebben. Dit aantal is het aantal leden in Hallo lokale groep Hallo.
  * Als er meer leden voordat de synchronisatie Hallo eerst start, worden Hallo-groep is niet gesynchroniseerd.
  * Als het aantal leden Hallo Breid uit wanneer het aanvankelijk is gemaakt, klikt u vervolgens wanneer het 50.000 leden die wordt gestopt tot Hallo lidmaatschap aantal lager is dan 50.000 opnieuw is synchroniseren is bereikt.
  * Opmerking: Hallo 50.000 lidmaatschap count wordt ook afgedwongen door Azure AD. U bent geen groepen met meer leden kunnen toosynchronize zelfs als u wijzigen of verwijderen van deze regel.
* Als het Hallo-groep is een **distributiegroep**, moet dit ook e-mailtoegang. Zie [Neem contact op met out of box regels](#contact-out-of-box-rules) voor deze regel wordt afgedwongen.

Hallo na groepsbeleidsobjecten zijn **niet** tooAzure AD gesynchroniseerd:

* `IsPresent([isCriticalSystemObject])`. Zorg ervoor dat veel out-of-box-objecten in Active Directory, zoals Hallo ingebouwde groep administrators, zijn niet gesynchroniseerd.
* `[sAMAccountName] = "MSOL_AD_Sync_RichCoexistence"`. Verouderde groep wordt gebruikt door DirSync.
* `BitAnd([msExchRecipientTypeDetails],&amp;H40000000)`. Groep van de rol.
* `CBool(InStr(DNComponent(CRef([dn]),1),"\\0ACNF:")>0)`. De replicatie slachtoffer objecten niet synchroniseren.

### <a name="foreignsecurityprincipal-out-of-box-rules"></a>ForeignSecurityPrincipal out-of-box-regels
FSP's te 'any' lid zijn van (\*)-object in Hallo metaverse. In werkelijkheid gebeurt deze koppeling alleen voor gebruikers en beveiligingsgroepen. Deze configuratie zorgt ervoor dat forest-overschrijdende lidmaatschappen zijn opgelost en correct worden weergegeven in Azure AD.

### <a name="computer-out-of-box-rules"></a>Computer out-of-box-regels
Een nieuw computerobject moet voldoen aan Hallo toobe gesynchroniseerd te volgen:

* `userCertificate ISNOTNULL`. Alleen Windows 10-computers vullen dit kenmerk. Alle computerobjecten met een waarde in dit kenmerk worden gesynchroniseerd.

## <a name="understanding-hello-out-of-box-rules-scenario"></a>Understanding Hallo out of box regels scenario
In dit voorbeeld gebruiken we een implementatie met één account-forest (A), een bronforest (R) en een Azure AD-directory.

![Afbeelding met scenariobeschrijving](./media/active-directory-aadconnectsync-understanding-default-configuration/scenario.png)

In deze configuratie wordt ervan uitgegaan dat er is een ingeschakeld Hallo accountforest-account en een uitgeschakeld account in Hallo bron-forest met een gekoppeld postvak.

Ons doel met standaardconfiguratie Hallo is:

* Kenmerken die zijn gerelateerd toosign in worden gesynchroniseerd vanuit Hallo-forest met account Hallo ingeschakeld.
* Kenmerken die kunnen worden gevonden in Hallo GAL (globale adreslijst) worden gesynchroniseerd vanuit Hallo-forest met Hallo postvak. Als geen postvak kan worden gevonden, wordt een andere forest wordt gebruikt.
* Als een gekoppeld postvak wordt gevonden, moet hello gekoppelde ingeschakeld-account worden gevonden voor Hallo object toobe geëxporteerd tooAzure AD.

### <a name="synchronization-rule-editor"></a>Synchronization Rule Editor
Hallo-configuratie kan worden bekeken en gewijzigd met de Hallo hulpprogramma synchronisatie regels Editor (SRE) en een snelkoppeling tooit vindt u in het startmenu Hallo.

![Synchronisatie regeleditor pictogram](./media/active-directory-aadconnectsync-understanding-default-configuration/sre.png)

Hallo SRE is een hulpprogramma van de resource kit en deze met Azure AD Connect-synchronisatie is geïnstalleerd. toobe kunnen toostart, moet u lid zijn van Hallo ADSyncAdmins groep zijn. Wanneer deze wordt gestart, ziet u ongeveer het volgende:

![Inkomende synchronisatieregels](./media/active-directory-aadconnectsync-understanding-default-configuration/syncrulesinbound.png)

In dit deelvenster ziet u alle synchronisatieregels die zijn gemaakt voor uw configuratie. Elke regel in de tabel Hallo is een Synchronisatieregel. toohello links onder regeltypen, u twee verschillende typen vindt Hallo: binnenkomend en uitgaand. Inkomend en uitgaand is uit de weergave Hallo van Hallo metaverse. Bent u voornamelijk gaat toofocus op Hallo regels in dit overzicht voor binnenkomende verbindingen. de daadwerkelijke lijst Hallo van synchronisatieregels is afhankelijk van schema Hallo gedetecteerd in AD. In vorige Hallo afbeelding, Hallo account forest (fabrikamonline.com) beschikt niet over eventuele services, zoals Exchange en Lync en geen synchronisatieregels zijn gemaakt voor deze services. Echter, in Hallo bron-forest (res.fabrikamonline.com) u synchronisatieregels voor deze services. Hallo-inhoud van Hallo regels is verschillend, afhankelijk van de versie van het Hallo gedetecteerd. Bijvoorbeeld in een implementatie met Exchange 2013 zijn er meer kenmerkstromen geconfigureerd dan in Exchange 2010-2007.

### <a name="synchronization-rule"></a>Synchronisatieregel
Een Synchronisatieregel is een configuratieobject met een set kenmerken die als een voorwaarde wordt voldaan. Het is ook gebruikte toodescribe hoe een object in de connectorruimte van een gerelateerde tooan-object in de metaverse hello is, ook wel **join** of **overeen met**. Hallo-synchronisatieregels hebben een hogere prioriteitswaarde die aangeeft hoe ze betrekking hebben tooeach andere. Een regel voor het synchroniseren met een lagere numerieke waarde heeft een hogere prioriteit en in een kenmerk stroom-conflict Hallo hogere prioriteit wins conflictoplossing.

Als u bijvoorbeeld bekijkt hello Synchronisatieregel **In uit Active Directory-gebruiker AccountEnabled**. Deze regel in Hallo SRE markeren en selecteer **bewerken**.

Aangezien deze regel een regel voor out-of-box is, ontvangt u een waarschuwing wanneer u de regel Hallo opent. U maakt een [tooout-of-box regels wijzigingen](active-directory-aadconnectsync-best-practices-changing-default-configuration.md), zodat u zeker weet wat uw bedoelingen zijn. In dit geval wilt u alleen tooview Hallo regel. Selecteer **Nee**.

![Synchronisatie van regels voor waarschuwing](./media/active-directory-aadconnectsync-understanding-default-configuration/warningeditrule.png)

Een Synchronisatieregel heeft vier configuratiesecties: beschrijving, Scoping filter, regels voor lid worden en transformaties.

#### <a name="description"></a>Beschrijving
Hallo eerste sectie bevat algemene informatie zoals een naam en beschrijving.

![Beschrijving tabblad synchroon regeleditor ](./media/active-directory-aadconnectsync-understanding-default-configuration/syncruledescription.png)

Ook vindt u informatie over welke verbonden systeem met deze regel is gerelateerd aan, die objecttype in Hallo verbonden systeem die is van toepassing op en Hallo metaverseobjecttype-object. Hallo metaverseobjecttype is altijd persoon ongeacht wanneer type bronobject Hallo een gebruiker, iNetOrgPerson of neem contact op met is. Hallo metaverseobjecttype moet nooit wijzigen zodat deze is gemaakt als een algemeen type. Hallo koppelingstype kan worden ingesteld tooJoin, StickyJoin of inrichten. Deze instelling werkt samen met de Hallo Join regels sectie en later wordt besproken.

U ziet ook dat deze synchronisatieregel wordt gebruikt voor Wachtwoordsynchronisatie. Als een gebruiker binnen het bereik van deze synchronisatieregel, worden Hallo wachtwoord worden gesynchroniseerd vanuit de lokale toocloud (ervan uitgaande dat u Hallo wachtwoordsynchronisatiefunctie hebt ingeschakeld).

#### <a name="scoping-filter"></a>Bereikfilter
Hallo bereikfilter sectie is gebruikte tooconfigure wanneer een regel voor synchronisatie moet worden toegepast. Aangezien het Hallo-naam van de Synchronisatieregel die u bekijkt hello aangeeft moet alleen worden toegepast voor ingeschakelde gebruikers, Hallo scope is geconfigureerd in dat geval Hallo AD-kenmerk **userAccountControl** moet niet hebben Hallo foutstijlbit 2. Wanneer synchronisatie-engine Hallo vindt een gebruiker in AD, geldt deze deze synchronisatie regel wanneer **userAccountControl** toohello decimale waarde 512 (ingeschakelde normale gebruiker) is ingesteld. Hallo-regel is niet van toepassing wanneer de gebruiker Hallo heeft **userAccountControl** too514 ingesteld (uitgeschakelde normale gebruiker).

![Tabblad in de regeleditor Sync scoping ](./media/active-directory-aadconnectsync-understanding-default-configuration/syncrulescopingfilter.png)

Hallo bereik filter heeft groepen en de componenten die kunnen worden genest. Alle componenten in een groep moeten worden voldaan voor een Synchronisatieregel tooapply. Wanneer meerdere groepen zijn gedefinieerd, moet ten minste één groep voor Hallo regel tooapply worden voldaan. Dat wil zeggen, een logische of tussen groepen en een logische wordt geëvalueerd en wordt geëvalueerd binnen een groep. Een voorbeeld van deze configuratie kunt u vinden in Hallo uitgaande Synchronisatieregel **uit tooAAD – groep Join**. Er zijn verschillende filter groepen voor synchronisatie, bijvoorbeeld één voor beveiligingsgroepen (`securityEnabled EQUAL True`) en één voor distributiegroepen (`securityEnabled EQUAL False`).

![Tabblad in de regeleditor Sync scoping ](./media/active-directory-aadconnectsync-understanding-default-configuration/syncrulescopingfilterout.png)

Deze regel is gebruikte toodefine welke groepen ingericht tooAzure AD worden moeten. Distributiegroepen moet een e-mailtoegang toobe gesynchroniseerd met Azure AD, maar voor beveiligingsgroepen een e-mailbericht is niet vereist.

#### <a name="join-rules"></a>Regels toevoegen
de derde sectie Hallo is gebruikte tooconfigure hoe objecten in Hallo connectorruimte tooobjects in Hallo metaverse gerelateerd. Hallo regel die u eerder hebt bekeken heeft geen configuratie voor regels voor lid worden dus in plaats daarvan u bent momenteel toolook op **In uit Active Directory-gebruiker toevoegen**.

![Tabblad regels koppelen in de regeleditor synchronisatie ](./media/active-directory-aadconnectsync-understanding-default-configuration/syncrulejoinrules.png)

Hallo-inhoud van het Hallo-join-regel is afhankelijk van Hallo die overeenkomt met de geselecteerde optie in de installatiewizard Hallo. Voor een inkomende regel Hallo evaluatie begint met een object in Hallo bron connectorruimte en elke groep in Hallo join regels wordt geëvalueerd in de reeks. Als een bronobject is geëvalueerd toomatch exact één object in metaverse met behulp van een join-regels Hallo Hallo, Hallo objecten zijn gekoppeld. Hallo koppelingstype op Hallo beschrijvingspagina wordt gebruikt als alle regels zijn geëvalueerd en er geen overeenkomst is. Als deze configuratie is ingesteld, te**inrichten**, en vervolgens een nieuw object in Hallo doel, Hallo metaverse maakt. een nieuw object toohello metaverse ook bekend als te staat tooprovision**project** een object toohello metaverse.

Hallo join regels worden slechts eenmaal geëvalueerd. Wanneer een object van de ruimte connector en een metaverse-object zijn gekoppeld, blijven deze gekoppelde zolang Hallo bereik van Hallo Synchronisatieregel nog steeds voldaan is.

Bij het evalueren van synchronisatieregels moet slechts één regel voor het synchroniseren met de join-regels die zijn gedefinieerd in het bereik. Als meerdere synchronisatieregels met join regels voor één object worden gevonden, wordt er een fout gegenereerd. Daarom is het beste Hallo toohave slechts één regel voor het synchroniseren met join gedefinieerd wanneer er meerdere synchronisatieregels zijn binnen het bereik van een object. In Hallo out-of-box-configuratie voor Azure AD Connect-synchronisatie, deze regels kunnen worden gevonden door te kijken Hallo naam en vinden die met Hallo word **Join** achter Hallo Hallo-naam van. Een regel zonder join-regels die zijn gedefinieerd voor het synchroniseren is van toepassing hello kenmerkstromen wanneer andere synchronisatieregels Hallo objecten samengevoegd of een nieuw object in Hallo doel ingericht.

Als u hierboven Hallo afbeelding bekijkt, ziet u die regel Hallo probeert toojoin **objectSID** met **msExchMasterAccountSid** (Exchange) en **msRTCSIP-OriginatorSid** () Lync) Dit is wat we verwachten in de topologie van een account-resource forest. U vindt Hallo dezelfde regel op alle forests. Hallo verondersteld wordt dat elk forest een account of een bron-forest kan worden. Deze configuratie werkt ook als er accounts die bevinden zich in één forest en hoeft geen toobe toegevoegd.

#### <a name="transformations"></a>Transformaties
Hallo transformatie sectie definieert alle kenmerkstromen die van toepassing zijn toohello doelobject wanneer Hallo objecten zijn gekoppeld en Hallo bereik filter is voldaan. Terugkeert toohello **In uit Active Directory-gebruiker AccountEnabled** Synchronisatieregel, vindt u Hallo transformaties te volgen:

![Transformaties tabblad synchroon regeleditor ](./media/active-directory-aadconnectsync-understanding-default-configuration/syncruletransformations.png)

tooput deze configuratie in de context in een implementatie met een Account-bron-forests is verwachte toofind een ingeschakeld Hallo accountforest-account en een uitgeschakeld account in Hallo-bron-met Exchange en Lync-instellingen forest. Synchronisatieregel u bekijkt Hello bevat Hallo kenmerken die zijn vereist voor aanmelding en deze kenmerken moeten stromen van Hallo forest wanneer er een ingeschakeld-account. Deze kenmerkstromen worden samen in één Synchronisatieregel geplaatst.

Een transformatie kan verschillende typen hebben: constante, Direct en -expressie.

* Een constante stroom loopt altijd een waarde vastgelegd. In bovenstaande Hallo geval, altijd opnieuw wordt ingesteld Hallo waarde **True** in Hallo metaverse-kenmerk met de naam **accountEnabled**.
* Een directe stroom loopt altijd Hallo-waarde van Hallo-kenmerk in Hallo toohello doel bronkenmerk als-is.
* de derde stroomtype Hallo expressie is en kunt u meer geavanceerde configuraties.

Hallo expressietaal is VBA (Visual Basic for Applications), zodat mensen met ervaring van Microsoft Office of VBScript herkent Hallo-indeling. Kenmerken zijn tussen vierkante haken, [attributeName]. Kenmerknamen en functienamen zijn hoofdlettergevoelig, maar hello synchronisatie regeleditor Hallo expressies geëvalueerd en bieden een waarschuwing als het Hallo-expressie is niet geldig. Alle expressies worden uitgedrukt in op één regel met geneste functies. tooshow hello power van Hallo configuratie taal, hier is Hallo stroom voor pwdLastSet, maar met aanvullende opmerkingen ingevoegd:

```
// If-then-else
IIF(
// (hello evaluation for IIF) Is hello attribute pwdLastSet present in AD?
IsPresent([pwdLastSet]),
// (hello True part of IIF) If it is, then from right tooleft, convert hello AD time format tooa .Net datetime, change it toohello time format used by Azure AD, and finally convert it tooa string.
CStr(FormatDateTime(DateFromNum([pwdLastSet]),"yyyyMMddHHmmss.0Z")),
// (hello False part of IIF) Nothing toocontribute
NULL
)
```

Zie [Understanding declaratieve inrichting expressies](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md) voor meer informatie over Hallo expressietaal voor kenmerkstromen.

### <a name="precedence"></a>Prioriteit
U nu een afzonderlijke synchronisatieregels hebt bekeken, maar Hallo regels werken samen in Hallo-configuratie. In sommige gevallen wordt een kenmerkwaarde bijgedragen van meerdere synchronisatie regels toohello dezelfde target-kenmerk. In dit geval is Kenmerkprioriteit gebruikte toodetermine welk kenmerk wins. Bekijk een voorbeeld: Hallo kenmerk sourceAnchor. Dit kenmerk is een belangrijk kenmerk toobe kunnen toosign in tooAzure AD. U vindt een kenmerkstroom voor dit kenmerk in twee verschillende synchronisatieregels **In uit Active Directory-gebruiker AccountEnabled** en **In uit Active Directory-gebruiker algemene**. Vanwege de prioriteit van regels voor tooSynchronization is hello sourceAnchor kenmerk bijgedragen Hallo-forest met een ingeschakelde account eerst wanneer er meerdere objecten gekoppelde toohello metaverse-object. Als er geen ingeschakelde rekeningen zijn, dan Hallo synchronisatie-engine gebruikt Hallo catch all-Synchronisatieregel **In uit Active Directory-gebruiker algemene**. Deze configuratie zorgt ervoor dat ook voor accounts die zijn uitgeschakeld, is er nog steeds een sourceAnchor.

![Inkomende synchronisatieregels](./media/active-directory-aadconnectsync-understanding-default-configuration/syncrulesinbound.png)

Hallo voorrang voor synchronisatieregels is ingesteld in groepen met Hallo-installatiewizard. Alle regels in een groep Hallo hebben dezelfde naam, maar ze zijn verbonden toodifferent verbonden mappen. Hallo-installatiewizard Hallo regel geeft **In uit Active Directory-gebruiker toevoegen** hoogste prioriteit en dit doorloopt over alle verbonden AD-mappen. Vervolgens gaat door met de volgende groepen Hallo van regels in een vooraf gedefinieerde volgorde. In een groep worden aan Hallo volgorde Hallo die connectors zijn toegevoegd in de wizard Hallo Hallo regels toegevoegd. Als een andere Connector met de wizard hello wordt toegevoegd, Hallo synchronisatieregels wordt gewijzigd en Hallo nieuwe Connector regels op de laatste worden ingevoegd in elke groep.

### <a name="putting-it-all-together"></a>Kort samengevat
We nu voldoende weten over synchronisatieregels toobe kunnen toounderstand hoe Hallo configuratie met Hallo werkt andere synchronisatieregels. Als u op een gebruiker en het Hallo kenmerken die hebben bijgedragen toohello metaverse, Hallo regels worden toegepast in volgorde Hallo:

| Naam | Opmerking |
|:--- |:--- |
| In uit Active Directory-gebruiker koppelen |Regel voor het lidmaatschap van de connector ruimteobjecten van het metaverse. |
| In uit Active Directory-gebruikersaccount is ingeschakeld |Kenmerken die vereist zijn voor aanmelden tooAzure AD en Office 365. We willen dat deze kenmerken uit Hallo ingeschakeld-account. |
| In uit Active Directory-gebruiker gemeenschappelijke in Exchange |Gevonden kenmerken in Hallo globale adreslijst. We ervan uitgaan dat Hallo gegevenskwaliteit wordt aanbevolen in Hallo-forest waar we Hallo gebruikerspostvak hebben gevonden. |
| In uit Active Directory-gebruiker gemeenschappelijke |Gevonden kenmerken in Hallo globale adreslijst. Als er een postvak gevonden, kan geen andere gekoppelde objecten Hallo kenmerkwaarde bijdragen. |
| In uit Active Directory-gebruiker Exchange |Is alleen aanwezig als Exchange is gedetecteerd. Deze loopt alle kenmerken van de infrastructuur Exchange. |
| In uit Active Directory-gebruiker Lync |Alleen bestaat of Lync is gedetecteerd. Deze loopt alle kenmerken van de infrastructuur Lync. |

## <a name="next-steps"></a>Volgende stappen
* Lees meer over Hallo configuratiemodel in [Understanding declaratieve inrichting](active-directory-aadconnectsync-understanding-declarative-provisioning.md).
* Lees meer over Hallo expressietaal in [Understanding declaratieve inrichting expressies](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md).
* Doorgaan met het lezen van de werking van Hallo out-of-box-configuratie in [inzicht krijgen in gebruikers en contactpersonen](active-directory-aadconnectsync-understanding-users-and-contacts.md)
* Zie hoe een praktisch toomake wijzigen met behulp van declaratieve inrichting [hoe een wijziging toohello toomake standaard configuratie](active-directory-aadconnectsync-change-the-configuration.md).

**Overzichtsonderwerpen**

* [Azure AD Connect-synchronisatie: inzicht en synchronisatie aanpassen](active-directory-aadconnectsync-whatis.md)
* [Uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md)

