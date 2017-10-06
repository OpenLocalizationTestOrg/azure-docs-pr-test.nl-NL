---
title: "ontwerpoverwegingen voor aaaAzure Active Directory hybride identiteit - strategie voor de ingebruikname van een hybride identiteit definiëren | Microsoft Docs"
description: "Met voorwaardelijk toegangsbeheer controleert de Azure Active Directory Hallo bepaalde voorwaarden die u bij het verifiëren van de gebruiker Hallo en alvorens deze toegang toohello toepassing kiezen. Als deze voorwaarden is voldaan, wordt Hallo gebruiker geverifieerd en toegang toohello toepassing toegestaan."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: b92fa5a9-c04c-4692-b495-ff64d023792c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 9ffca675d0c714392adfcbbc4dcfad12fccbac78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="define-a-hybrid-identity-adoption-strategy"></a>Een strategie voor hybride identiteit acceptatie definiëren
In deze taak definieert u Hallo hybride identiteit acceptatie strategie voor hybride identiteit toomeet Hallo zakelijke vereisten van uw oplossing die zijn beschreven in:

* [Bedrijfsbehoeften vaststellen](active-directory-hybrid-identity-design-considerations-business-needs.md)
* [Vereisten voor directory-synchronisatie bepalen](active-directory-hybrid-identity-design-considerations-directory-sync-requirements.md)
* [Vereisten multi-factor authentication bepalen](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md)

## <a name="define-business-needs-strategy"></a>Zakelijke behoeften-strategie bepalen
de eerste taak Hallo adressen bepalende Hallo organisaties zakelijke behoeften.  Dit kan zeer brede en bereik kneep kan optreden als u niet zorgvuldig.  Houd het eenvoudig in Hallo begin maar vergeet tooplan voor een ontwerp dat wordt aangepast aan en maak veranderingen in toekomstige Hallo mogelijk.  Ongeacht of het ontwerp van een eenvoudige of een zeer complexe, is Azure Active Directory Hallo Microsoft Identity platform dat ondersteuning biedt voor Office 365, Microsoft Online Services en cloud-bewuste toepassingen.

## <a name="define-an-integration-strategy"></a>Een Integratiestrategie voor definiëren
Microsoft heeft drie belangrijkste integratiescenario's die cloud-identiteiten, gesynchroniseerde identiteiten en federatieve identiteiten zijn.  Plan voor overstap op een van deze integratiestrategieën.  Hallo strategie die u kiest, kan variëren en Hallo beslissingen bij het kiezen van een bevatten mogelijk, welk type van de gebruikerservaring gewenste tooprovide, hebt u enkele van de bestaande infrastructuur van Hallo al in-place en wat Hallo meest voordelige is.  

![](./media/hybrid-id-design-considerations/integration-scenarios.png)

Hallo scenario's die zijn gedefinieerd in Hallo bovenstaande afbeelding zijn:

* **Cloud-identiteiten**: dit zijn de identiteiten die uitsluitend in Hallo cloud bestaat.  In geval van Azure AD Hallo zouden ze zich bevinden in het bijzonder in uw Azure AD-directory.
* **Gesynchroniseerd**: deze identiteiten die lokaal aanwezig zijn en in de cloud Hallo.  Met Azure AD Connect, worden deze gebruikers gemaakt of gekoppeld met de bestaande Azure AD-accounts.  Hallo worden wachtwoord-hash van de gebruiker gesynchroniseerd vanuit Hallo lokale omgeving toohello cloud in wat een wachtwoord-hash wordt aangeroepen.  Wanneer met behulp van gesynchroniseerd is een voorbehoud Hallo dat als een gebruiker in Hallo on-premises omgeving is uitgeschakeld, kunnen er too3 uur voor dat account status tooshow in Azure AD.  Dit is vanwege toohello synchronisatie tijdsinterval.
* **Federatieve**: deze identiteiten bestaan zowel on-premises en in de cloud Hallo.  Met Azure AD Connect, worden deze gebruikers gemaakt of gekoppeld met de bestaande Azure AD-accounts.  

> [!NOTE]
> Lees voor meer informatie over de synchronisatieopties Hallo [uw on-premises identiteiten integreren met Azure Active Directory](connect/active-directory-aadconnect.md).
> 
> 

Hallo tabel helpt bij het Hallo-voor- en nadelen van elk van de volgende strategieën Hallo bepalen:

| Een strategie voor | Voordelen | Nadelen |
| --- | --- | --- |
| **Cloud-identiteiten** |Eenvoudiger toomanage voor kleine organisatie. <br> Er is niets tooinstall op de lokale geen extra hardware nodig<br>Eenvoudig uitgeschakeld als de gebruiker Hallo Hallo bedrijf verlaat |Gebruikers moeten toosign in bij het openen van de werkbelastingen in Hallo cloud <br> Wachtwoorden al kunnen dan niet dezelfde Hallo voor cloud en on-premises identiteiten |
| **Gesynchroniseerd** |On-premises wachtwoord wordt zowel on-premises verifiëren en cloudadreslijsten <br>Eenvoudiger toomanage voor kleine, grote of middelgrote organisaties <br>Gebruikers kunnen eenmalige aanmelding (SSO) hebben voor een aantal bronnen <br> Microsoft voorkeurs-methode voor synchronisatie <br> Eenvoudiger toomanage |Sommige gebruikers mogelijk weerstand toosynchronize hun mappen Hello cloud vanwege specifiek bedrijf politie |
| **Federatieve** |Gebruikers beschikken over eenmalige aanmelding (SSO) <br>Als een gebruiker wordt beëindigd of verlaat, Hallo-account kan, onmiddellijk worden uitgeschakeld en de toegang is ingetrokken,<br> Ondersteunt geavanceerde scenario's die niet kan worden bewerkstelligd met gesynchroniseerd |Meer stappen toosetup en configureren <br> Hogere onderhoud <br> Extra hardware nodig voor Hallo STS-infrastructuur <br> Moet mogelijk extra hardware tooinstall Hallo federation-server. Aanvullende software is vereist als AD FS wordt gebruikt <br> Uitgebreide instellingen vereist voor eenmalige aanmelding <br> Kritieke storingspunt als Hallo federation-server niet actief is, gebruikers niet mogelijk tooauthenticate |

### <a name="client-experience"></a>Clientervaring
Hallo aanmelden gebruikerservaring worden bepaald door het Hallo-strategie die u gebruikt.  Hallo volgende tabellen vindt u informatie over wat gebruikers Hallo hun aanmelden verwachten toobe ervaren.  Houd er rekening mee dat niet alle federatieve identiteiten-providers SSO in alle scenario's ondersteunen.

**Toepassingen die lid zijn van Domain en particuliere netwerken**:

|  | Gesynchroniseerde identiteiten | Federatieve identiteiten |
| --- | --- | --- |
| Webbrowsers |Op formulieren gebaseerde verificatie |eenmalige aanmelding vereist op, soms toosupply organisatie-ID |
| Outlook |Prompt voor referenties |Prompt voor referenties |
| Skype voor bedrijven (Lync) |Prompt voor referenties |eenmalige aanmelding voor Lync, referenties gevraagd voor Exchange |
| SkyDrive Pro |Prompt voor referenties |eenmalige aanmelding |
| Office Professional Plus abonnement |Prompt voor referenties |eenmalige aanmelding |

**Externe of niet-vertrouwde bronnen**:

|  | Gesynchroniseerde identiteiten | Federatieve identiteiten |
| --- | --- | --- |
| Webbrowsers |Op formulieren gebaseerde verificatie |Op formulieren gebaseerde verificatie |
| Outlook, Skype voor bedrijven (Lync) Skydrive Pro, Office-abonnement |Prompt voor referenties |Prompt voor referenties |
| Exchange ActiveSync |Prompt voor referenties |eenmalige aanmelding voor Lync, referenties gevraagd voor Exchange |
| Mobiele apps |Prompt voor referenties |Prompt voor referenties |

Als u van de taak dat u hebt een IdP of zijn gaat toouse partij 3rd 1 één tooprovide Federatie met Azure AD hebt vastgesteld, moet u op de hoogte van de volgende Hallo ondersteund toobe mogelijkheden:

* Elke SAML 2.0-provider die voldoen aan de voorwaarden Hallo SP Lite profiel biedt ondersteuning voor verificatie tooAzure AD en de bijbehorende toepassingen
* Ondersteunt het passieve verificatie, wat auth tooOWA, gesimuleerde Productieorder vergemakkelijkt, enzovoort.
* Exchange Online-clients kunnen worden ondersteund via Hallo SAML 2.0 verbeterde Client profiel (ECP)

Ook moet u rekening houden met welke mogelijkheden zijn niet meer beschikbaar:

* Zonder ondersteuning voor WS-Trust/Federation worden alle actieve clients verbroken
  * Dit betekent dat er geen Lync-client, OneDrive, Office-abonnement, Office Mobile voorafgaande tooOffice 2016-client
* Overgang van de authenticatie van Office toopassive kunnen zij toosupport pure SAML 2.0 IdPs, maar ondersteuning nog steeds op basis van de client door de client

> [!NOTE]
> Meest recente lijst Lees voor Hallo Hallo artikel http://aka.ms/ssoproviders.
> 
> 

## <a name="define-synchronization-strategy"></a>Synchronisatie-strategie bepalen
In deze taak definieert u Hallo-hulpprogramma's die gebruikt toosynchronize Hallo organisatie lokale gegevens toohello cloud en welke worden topologie u moet gebruiken.  Omdat de meeste organisaties gebruikmaken van Active Directory, informatie over het gebruik van Azure AD Connect tooaddress Hallo vragen bovenstaande vindt u in sommige details.  Er is informatie over het gebruik van FIM 2010 R2 voor omgevingen waarin er geen Active Directory, of MIM 2016 toohelp deze strategie plannen.  Echter toekomstige versies van Azure AD Connect ondersteunt LDAP-adreslijsten, dus zijn afhankelijk van de tijdlijn, wordt deze informatie is mogelijk kunnen tooassist.

### <a name="synchronization-tools"></a>Hulpprogramma's voor synchronisatie
Hallo jaren, hebben verschillende hulpprogramma's voor synchronisatie bestond en gebruikt voor verschillende scenario's.  Azure AD Connect is momenteel Ga tootool keuze voor alle ondersteunde scenario's Hallo.  AAD Sync en DirSync zijn ook nog steeds rond en zelfs nu aanwezig is in uw omgeving mag zijn. 

> [!NOTE]
> Lees voor Hallo meest actuele informatie met betrekking tot Hallo ondersteund mogelijkheden van elk hulpprogramma [vergelijking van hulpprogramma's voor Directory-integratie](active-directory-hybrid-identity-design-considerations-tools-comparison.md) artikel.  
> 
> 

### <a name="supported-topologies"></a>Ondersteunde topologieën
Bij het definiëren van een strategie voor synchronisatie moet Hallo-topologie die wordt gebruikt worden bepaald. Informatie die is bepaald in stap 2 kunt u bepalen welke topologie is afhankelijk van Hallo Hallo juiste één toouse. Hallo één forest, één Azure AD-topologie Hallo meest voorkomende is en bestaat uit één Active Directory-forest en één exemplaar van Azure AD.  Dit gaat toobe gebruikt in een meerderheid van Hallo scenario's en Hallo verwacht topologie bij gebruik van Azure AD Connect Express-installatie, zoals wordt weergegeven in onderstaande afbeelding ziet Hallo.

![](./media/hybrid-id-design-considerations/single-forest.png)Eén Forest Scenario het is heel gebruikelijk voor kleine en zelfs grote organisaties toohave meerdere forests, zoals wordt weergegeven in afbeelding 5.

> [!NOTE]
> Hallo voor meer informatie over verschillende on-premises en Azure AD-topologieën met Azure AD Connect-synchronisatie Lees Hallo artikel [topologieën voor Azure AD Connect](connect/active-directory-aadconnect-topologies.md).
> 
> 

![](./media/hybrid-id-design-considerations/multi-forest.png) 

Met meerdere forests

Als deze aanvraag Hallo Hallo vervolgens meerdere forest één moet Azure AD-topologie beschouwd als hello volgende vereisten voldaan is:

* Gebruikers hebben slechts 1 identiteit in alle forests – Hallo een unieke id gebruikers onderstaande sectie wordt beschreven dit in meer detail.
* Hallo-gebruiker wordt geverifieerd toohello forest waarin hun identiteit zich bevindt
* UPN en Bronanker (onveranderbare id), zijn afkomstig van dit forest
* Alle forests toegankelijk zijn voor Azure AD Connect: dit betekent dat het hoeft niet verbonden met het domein toobe en kan worden geplaatst in een Perimeternetwerk, als dit dit vergemakkelijkt.
* Gebruikers hebben slechts één postvak
* Hallo-forest die als host fungeert voor een gebruiker postvak heeft Hallo aanbevolen kwaliteit van de gegevens voor kenmerken die zichtbaar zijn in Hallo Exchange globale adreslijst (GAL)
* Als er geen postvak op Hallo gebruiker, wordt elk forest kan worden gebruikt toocontribute deze waarden
* Als u een gekoppeld postvak hebben dan is er ook een ander account in een ander forest gebruikt toosign in.

> [!NOTE]
> Objecten die in zowel on-premises en in de cloud Hallo voorkomen zijn 'verbonden' via een unieke id. Deze unieke id is in de context van de Hallo van Directory-synchronisatie, waarnaar wordt verwezen tooas hello SourceAnchor. In de context Hallo van eenmalige aanmelding is dit waarnaar wordt verwezen tooas Hallo onveranderbare id genoemd. [Concepten voor Azure AD Connect ontwerpen](connect/active-directory-aadconnect-design-concepts.md#sourceanchor) voor meer overwegingen met betrekking tot Hallo gebruik van SourceAnchor.
> 
> 

Als bovenstaande Hallo niet waar zijn en er meer dan één actieve account of meer dan één postvak, wordt Azure AD Connect Kies een en Hallo andere negeren.  Als u postvakken maar geen andere account hebt gekoppeld, wordt deze accounts niet meer worden geëxporteerde tooAzure AD en wordt die gebruiker geen lid zijn van groepen worden.  Dit verschilt van de manier waarop deze is het verleden Hallo met DirSync en is opzettelijk toobetter ondersteuning scenario's met meerdere forests. Een scenario met meerdere forests wordt weergegeven in onderstaande afbeelding ziet Hallo.

![](./media/hybrid-id-design-considerations/multiforest-multipleAzureAD.png) 

**Meerdere forests meerdere Azure AD-scenario**

Het wordt aanbevolen toohave die slechts één map in Azure AD voor een organisatie, maar dit is het die een 1:1-relatie tussen een Azure AD Connect sync-server en een Azure Active directory wordt bewaard.  Voor elk exemplaar van Azure AD moet u een installatie van Azure AD Connect.  Ook Azure AD inherent is geïsoleerd en gebruikers in één exemplaar van Azure AD worden toosee kunnen gebruikers in een ander exemplaar.

Het is mogelijk en ondersteunde tooconnect een on-premises exemplaar van Active Directory toomultiple Azure AD-mappen zoals weergegeven in onderstaande afbeelding ziet Hallo:

![](./media/hybrid-id-design-considerations/single-forest-flitering.png) 

**Filteren scenario voor één forest**

In de volgorde toodo wordt hierna hello voldaan:

* Azure AD Connect sync-servers moeten worden geconfigureerd voor het filteren zodat ze elk een sluiten elkaar wederzijds uit set van objecten hebben.  Dit doen, bijvoorbeeld door het bereik van elke server tooa bepaald domein of organisatie-eenheid.
* Een DNS-domein kan alleen worden geregistreerd in een enkel Azure AD-directory zodat Hallo UPN's van gebruikers in Hallo Hallo lokale AD afzonderlijke naamruimten moet gebruiken
* Alleen gebruikers in één exemplaar van Azure AD worden kunnen toosee gebruikers uit hun exemplaar.  Niet toosee kunnen gebruikers in Hallo zijn andere exemplaren
* Alleen een hello Azure AD-mappen kunt Exchange inschakelen hybride Hello on-premises AD
* Wederzijdse exclusiviteit geldt ook toowrite terug.  Hierdoor kunt u sommige write-back-functies niet ondersteund met deze topologie omdat deze wordt ervan uitgegaan een configuratie met één on-premises dat.  Dit omvat:
  * Groep terugschrijven met standaardconfiguratie
  * Apparaat terugschrijven

Let erop dat de volgende Hallo wordt niet ondersteund en moet niet worden gekozen als een implementatie:

* Is geen ondersteunde toohave meerdere servers met Azure AD Connect sync verbinding toohello dezelfde Azure AD-directory maken, zelfs als ze geconfigureerde toosynchronize sluiten elkaar wederzijds uit ingesteld van object
* Het is niet-ondersteunde toosync Hallo dezelfde gebruiker toomultiple Azure AD-directory's. 
* Het is ook niet-ondersteunde toomake configuratiewijziging met een toomake gebruikers in een Azure AD-tooappear als in een andere Azure AD-directory contactpersonen. 
* Het is ook niet-ondersteunde toomodify Azure AD Connect-synchronisatie tooconnect toomultiple Azure AD-mappen.
* Azure AD-mappen zijn standaard geïsoleerd. Het is niet-ondersteunde toochange Hallo configuratie van Azure AD Connect-synchronisatie tooread gegevens uit een andere Azure AD-directory in een poging toobuild een gemeenschappelijke en uniform GAL tussen Hallo mappen. Het is ook niet-ondersteunde tooexport gebruikers, zoals contactpersonen tooanother on-premises AD dat met behulp van Azure AD Connect-synchronisatie.

> [!NOTE]
> Als uw organisatie voorkomt dat computers in uw netwerk verbinding maken met Internet toohello, dit artikel vindt u Hallo eindpunten (FQDN's, IPv4 en IPv6-adresbereiken) die moet worden opgenomen uw uitgaande toestaan lijsten en Internet Explorer vertrouwde websites van client computers tooensure Office 365 is door uw computers kunnen gebruiken. Lees voor meer informatie [Office 365-URL's en IP-adresbereiken](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2?ui=en-US&rs=en-US&ad=US).
> 
> 

## <a name="define-multi-factor-authentication-strategy"></a>Multi-factor authentication-strategie bepalen
In deze taak definieert u Hallo multi-factorauthenticatie strategie toouse.  Azure multi-factor Authentication wordt geleverd in twee verschillende versie.  Een cloud-gebaseerd is en Hallo andere is lokaal met behulp van hello Azure MFA-Server.  Op basis van Hallo evaluatie die hoger dan u kunt u bepalen welke oplossing is de juiste is voor uw strategie voor Hallo.  Gebruik onderstaande toodetermine welke ontwerpoptie voor het beste van uw bedrijf-beveiliging behoefte Hallo tabel:

Van meervoudige ontwerpopties:

| Asset toosecure | MFA in de cloud Hallo | MFA on-premises |
| --- | --- | --- |
| Microsoft-apps |Ja |Ja |
| SaaS-apps in app-galerie Hallo |Ja |Ja |
| IIS-toepassingen die zijn gepubliceerd via toepassingsproxy van Azure AD |Ja |Ja |
| IIS-toepassingen die niet zijn gepubliceerd via toepassingsproxy van Azure AD Hallo |Er is geen |Ja |
| Externe toegang als VPN, RDG |Er is geen |Ja |

Hoewel u mogelijk hebt gekozen voor een oplossing voor uw strategie, moet u nog steeds toouse Hallo evaluatie van boven op waar uw gebruikers zich bevinden.  Dit kan leiden tot Hallo oplossing toochange.  Gebruik onderstaande tooassist Hallo tabel u dit te bepalen:

| Gebruikerslocatie | Ontwerp van voorkeur-optie |
| --- | --- |
| Azure Active Directory |Multi-FactorAuthentication in Hallo cloud |
| Azure AD en on-premises AD dat gebruikmaakt van federatie met AD FS |Beide |
| Azure AD en on-premises AD dat gebruikmaakt van Azure AD Connect-geen Wachtwoordsynchronisatie |Beide |
| Azure AD en on-premises met Azure AD Connect met Wachtwoordsynchronisatie |Beide |
| On-premises AD |Multi-Factor Authentication-server |

> [!NOTE]
> U moet er ook voor zorgen dat Hallo multi-factorauthenticatie ontwerpoptie die u hebt geselecteerd Hallo-functies die vereist voor uw ontwerp zijn ondersteunt.  Lees voor meer informatie [hello multi-factor-beveiligingsoplossing kiezen voor u](../multi-factor-authentication/multi-factor-authentication-get-started.md#what-am-i-trying-to-secure).
> 
> 

## <a name="multi-factor-auth-provider"></a>Multi-factor Authentication-Provider
Multi-factor authentication-server is standaard beschikbaar voor hoofdbeheerders met een Azure Active Directory-tenant. Echter, als u tooextend multi-factorauthenticatie tooall van uw gebruikers wilt en/of tooyour globale beheerders toobe kunnen tootake voordeel functies zoals Hallo-beheerportal, aangepaste begroeting en rapporten wilt gebruiken, vervolgens moet u kopen en configureren Multi-factor Authentication-Provider.

> [!NOTE]
> U moet er ook voor zorgen dat Hallo multi-factorauthenticatie ontwerpoptie die u hebt geselecteerd Hallo-functies die vereist voor uw ontwerp zijn ondersteunt. 
> 
> 

## <a name="next-steps"></a>Volgende stappen
[Bepalen van de beveiligingsvereisten voor gegevens](active-directory-hybrid-identity-design-considerations-dataprotection-requirements.md)

## <a name="see-also"></a>Zie ook
[Overzicht ontwerpoverwegingen](active-directory-hybrid-identity-design-considerations-overview.md)

