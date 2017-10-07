---
title: 'CENC met Multi-DRM en toegangsbeheer: een verwijzing naar ontwerpen en implementeren op Azure en Azure mediaservices | Microsoft Docs'
description: "Meer informatie over hoe toolicensing Hallo Microsoft® Smooth Streaming Client overdragen Kit."
services: media-services
documentationcenter: 
author: willzhan
manager: cfowler
editor: 
ms.assetid: 7814739b-cea9-4b9b-8370-538702e5c615
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: willzhan;kilroyh;yanmf;juliako
ms.openlocfilehash: 033fb618650c4fbe9069d467159a8734da759bba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="cenc-with-multi-drm-and-access-control-a-reference-design-and-implementation-on-azure-and-azure-media-services"></a>CENC met Multi-DRM en Access Control: een referentieontwerp en -implementatie in Azure en Azure Media Services
 
## <a name="introduction"></a>Inleiding
Het is bekend dat het een complexe taak toodesign en een subsysteem DRM bouwen voor een OTT of online streamingoplossing. En is een algemeen in de praktijk voor operators/online video providers toooutsource deze serviceproviders onderdeel toospecialized DRM. Hallo-doel van dit document is toopresent een referentie-ontwerp en de implementatie van end-to-end DRM-subsysteem in OTT of online streaming-oplossing.

Hallo gericht lezers van dit document zijn engineers werken in DRM-subsysteem van OTT online streaming/meerdere-screen oplossingen of eventuele geïnteresseerd in DRM-subsysteem lezers. Hallo verondersteld wordt dat lezers bekend met ten minste één Hallo DRM technologieën op de markt hello, zoals PlayReady, Widevine, FairPlay of Adobe Access bent.

Door DRM opnemen we ook (Common Encryption) CENC met multi-DRM. Een belangrijke trend in online streaming en OTT industrie is toouse CENC met meerdere-native-DRM op verschillende clientplatforms, een verschuiving van Hallo vorige trend van het gebruik van een enkele DRM en de client-SDK voor verschillende clientplatforms. Als u CENC met meerdere native DRM, zowel PlayReady als Widevine zijn versleuteld volgens Hallo [Common Encryption (ISO/IEC 23001-7 CENC)](http://www.iso.org/iso/home/store/catalogue_ics/catalogue_detail_ics.htm?csnumber=65271/) specificatie.

Hallo voordelen van CENC met multi-DRM zijn als volgt:

1. Vermindert versleuteling kosten omdat de verwerking van een enkele versleuteling wordt gebruikt die gericht is op verschillende platforms met de systeemeigen DRM's;
2. Beperkt de kosten Hallo versleutelde activa te beheren omdat slechts één exemplaar van de versleutelde activa is vereist;
3. Elimineert kosten licentieverlening omdat Hallo systeemeigen DRM-client meestal vrije ruimte op het systeemeigen platform is DRM-client.

Microsoft is een actieve organisator van deze actie van DASH en CENC samen met enkele belangrijke zakelijke spelers. Microsoft Azure Media Services heeft is het bieden van ondersteuning van DASH en CENC. Zie voor recente aankondigingen van Mingfei blogs: [aangekondigd Google Widevine-licentie levering van services in Azure Media Services](https://azure.microsoft.com/blog/announcing-general-availability-of-google-widevine-license-services/), en [Azure Media Services wordt toegevoegd voor Google Widevine-verpakking voor het leveren van multi-DRM stroom](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/).  

### <a name="overview-of-this-article"></a>Overzicht van dit artikel
Hallo-doel van dit artikel omvat Hallo volgende:

1. Bevat een verwijzing van DRM-subsysteem met CENC met multi-DRM;
2. Biedt de implementatie van een verwijzing op Microsoft Azure/Azure Media Services-platform;
3. Sommige onderwerpen ontwerp- en implementatiestappen besproken.

Hallo-artikel 'multi-DRM' bevat informatie over de volgende Hallo is:

1. Microsoft PlayReady
2. Google Widevine
3. FairPlay van Apple 

Hallo volgende tabel ziet u Hallo systeemeigen platform/systeemeigen app en browsers die door elke DRM ondersteund.

| **Clientplatform** | **Systeemeigen DRM-ondersteuning** | **Browser-App** | **Streaming-indelingen** |
| --- | --- | --- | --- |
| **Smart tv, operator STB's, OTT STB 's** |PlayReady voornamelijk, en/of Widevine en/of andere |Linux, Opera, WebKit, andere |Verschillende indelingen |
| **Windows 10-apparaten (Windows-PC, Windows-Tablets, Windows Phone, Xbox.)** |PlayReady |MS IE11-Edge/EME<br/><br/><br/>UWP |STREEPJE (voor HLS, PlayReady wordt niet ondersteund)<br/><br/>DASH, Smooth Streaming (HLS voor, PlayReady wordt niet ondersteund) |
| **Android-apparaten (telefoon, Tablet, TV)** |Widevine |Chrome/EME |DASH, HLS |
| **iOS (iPhone, iPad), OS X-clients en Apple TV** |FairPlay |Safari 8 +/ EME |HLS |


In overweging Hallo huidige status van implementatie voor elke DRM, een service wordt meestal wel verstandig tooimplement 2 of 3 DRM's toomake zeker dat u alle Hallo typen eindpunten in Hallo best adres manier.

Er is een afweging tussen Hallo complexiteit van Hallo service logica en complexiteit Hallo op Hallo client side tooreach een bepaalde mate van gebruiker ervaring op Hallo verschillende clients.

toomake uw selectie, houd er rekening mee deze feiten:

* PlayReady is systeemeigen geïmplementeerd in elke Windows-apparaat op een Android-apparaten en beschikbaar via software-SDK's op vrijwel elk platform
* Widevine is systeemeigen geïmplementeerd in elke Android-apparaat, Chrome en sommige andere apparaten
* FairPlay is beschikbaar op iOS en Mac OS-clients of via iTunes.

Zo een typische multi-DRM zijn zou:

* Optie 1: PlayReady en Widevine
* Optie 2: PlayReady, Widevine en FairPlay

## <a name="a-reference-design"></a>Een referentie-ontwerp
In deze sectie wordt een verwijzing model dat agnostisch tootechnologies gebruikt tooimplement is biedt deze.

Een DRM-subsysteem kan Hallo volgende onderdelen bevatten:

1. Sleutelbeheer
2. DRM verpakking
3. Levering van DRM-licentie
4. Recht controleren
5. Verificatie/autorisatie
6. Player
7. Oorsprong/CDN

Hallo illustreert volgende diagram Hallo hoog niveau interactie tussen Hallo-onderdelen in een DRM-subsysteem.

![DRM-subsysteem met CENC](./media/media-services-cenc-with-multidrm-access-control/media-services-generic-drm-subsystem-with-cenc.png)

Er zijn drie basic 'lagen' hello ontwerp:

1. Back-office-laag (in zwart) die extern; niet worden weergegeven
2. 'DMZ'-laag (blauw) met alle Hallo eindpunten gerichte openbare;
3. Openbare internetlaag (lichte blauw) met CDN en spelers met verkeer via openbaar Internet.

Er moet een inhoudsbeheer hulpprogramma voor het beheren van DRM-beveiliging, ongeacht het statische of dynamische versleuteling is. Hallo-ingangen voor DRM-codering moeten worden opgenomen:

1. MBR video-inhoud;
2. Inhoudssleutel;
3. URL's aanschaf van licentie.

Tijdens het afspelen van is hoog niveau stroom Hallo:

1. Gebruiker is geverifieerd;
2. Verificatietoken is gemaakt voor gebruiker Hallo;
3. DRM beveiligde inhoud (manifest) is gedownloade tooplayer;
4. Player verzendt overname aanvraag toolicense licentieservers samen met sleutel-ID en -autorisatie-token.

Voordat bewegende toohello Volgend onderwerp ontwerp enkele woorden op Hallo van Sleutelbeheer.

| **ContentKey-Asset:** | **Scenario** |
| --- | --- |
| 1-op-1 |de meest eenvoudige geval Hallo. Het bevat beste Hallo-besturingselement. Maar resulteert dit in het algemeen in Hallo hoogst licentie leveringskosten. Aanvraag is vereist voor alle beveiligde activa op ten minste één licentie. |
| 1-op-veel |U kunt dezelfde inhoud sleutel voor meerdere assets Hallo. Bijvoorbeeld: voor alle Hallo activa in een logische groep zoals een genre of een subset van genre (of film gen) u kunt een enkel inhoudssleutel. |
| Veel-op-1 |Meerdere inhoudssleutels nodig zijn voor elk actief. <br/><br/>Als u tooapply beveiliging met betrekking tot een dynamische CENC met multi-DRM voor MPEG-DASH- en dynamische AES-128-versleuteling voor HLS nodig hebt, moet u bijvoorbeeld twee afzonderlijke inhoud sleutels, elk met een eigen ContentKeyType. (Voor Hallo-inhoudssleutel gebruikt voor dynamische CENC beveiliging, ContentKeyType.CommonEncryption moet worden gebruikt, terwijl voor Hallo inhoud sleutel die wordt gebruikt voor dynamische AES-128-versleuteling, ContentKeyType.EnvelopeEncryption moet worden gebruikt.)<br/><br/>Inhoud van een ander voorbeeld: bij CENC bescherming van streepje, in theorie, een inhoudssleutel kan worden gebruikt tooprotect videostream en een andere inhoud sleutel tooprotect audiostroom. |
| Veel – te-veel |Combinatie van Hallo hierboven twee scenario's: een set van inhoud sleutels worden gebruikt voor elk van meerdere activa in Hallo Hallo dezelfde asset 'groep'. |

Een andere belangrijke factor tooconsider is Hallo gebruik van permanente en niet-permanente licenties.

Waarom deze overwegingen belangrijk zijn?

Ze hebben een directe invloed toolicense levering kosten als u de openbare cloud voor de levering van licentie gebruiken. Laten we eens Hallo twee verschillende ontwerp gevallen tooillustrate te volgen:

1. Maandabonnement: permanente licentie en 1-op-veel inhoud sleutel aan asset toewijzing gebruiken. Bijvoorbeeld voor alle Hallo kinderen films gebruiken we een enkele inhoudssleutel voor versleuteling. In dit geval:

    Totaal aantal licenties van # aangevraagd voor alle kinderen films/apparaat = 1
2. Maandabonnement: niet-permanente licentie en 1 op 1 toewijzing tussen inhoudssleutel en asset gebruiken. In dit geval:

    Totaal aantal licenties van # aangevraagd voor alle kinderen films/apparaat = [# films gevolgde] x [# sessies]

Zoals u kunt gemakkelijk zien, Hallo twee verschillende ontwerpen resulteren in zeer andere licentiegroepen patronen daarom licentie bezorging verzoeken kosten als service voor het leveren van licenties is opgegeven door een openbare cloud zoals Azure Media Services.

## <a name="mapping-design-tootechnology-for-implementation"></a>Toewijzing ontwerp tootechnology voor implementatie
Vervolgens toewijzen we onze algemene ontwerp tootechnologies op Microsoft Azure/Azure Media Services-platform door op te geven welke toouse technologie voor elke bouwsteen.

Hallo ziet volgende tabel u Hallo toewijzing:

| **Bouwstenen** | **Technologie** |
| --- | --- |
| **Player** |[Azure Media Player](https://azure.microsoft.com/services/media-services/media-player/) |
| **ID-Provider (IDP)** |Azure Active Directory |
| **Beveiligde beveiligingstokenservice (STS)** |Azure Active Directory |
| **Werkstroom van DRM-beveiliging** |Azure Media Services dynamische beveiliging |
| **Levering van DRM-licentie** |1. Azure Media Services-licentie leveringsmethode (PlayReady, Widevine, FairPlay), of <br/>2. Axinom-licentieserver <br/>3. Aangepaste PlayReady-licentieserver |
| **Oorsprong** |Azure Media Services-Streaming-eindpunt |
| **Sleutelbeheer** |Niet nodig zijn voor de referentie-implementatie |
| **Inhoudbeheer** |Een C#-consoletoepassing |

Met andere woorden, zowel Identity-Provider (IDP) en Secure Token Service (STS) worden Azure AD. Voor player, gebruiken we [Azure Media Player-API](http://amp.azure.net/libs/amp/latest/docs/). Zowel Azure Media Services en Azure Media Player ondersteunen DASH en CENC met multi-DRM.

Hallo volgende diagram laat zien welke Hallo gegevensstructuur en -stromen met Hallo hierboven technologie-toewijzing.

![CENC op AMS](./media/media-services-cenc-with-multidrm-access-control/media-services-cenc-subsystem-on-AMS-platform.png)

In de volgorde tooset een dynamische CENC versleuteling, Hallo inhoudsbeheer tool Hallo na invoer gebruikt:

1. Open inhoud;
2. Inhoudssleutel uit de sleutel genereren/management;
3. URL's aanschaf van licentie;
4. Een lijst met gegevens uit Azure AD.

Hallo-uitvoer van Hallo inhoudsbeheer hulpprogramma zijn:

1. ContentKeyAuthorizationPolicy met Hallo-specificatie op hoe licentie levering controleert of een JWT-token en DRM licentie specificaties;
2. AssetDeliveryPolicy met specificaties op het streaming-indeling, DRM-beveiliging en URL's aanschaf van licentie.

Tijdens runtime, Hallo-stroom is als hieronder:

1. Bij verificatie van de gebruiker wordt een JWT-token gegenereerd;
2. Een van de Hallo claims die zijn opgenomen in Hallo JWT-token is 'groepen' claim met Hallo groep object-ID van 'EntitledUserGroup'. Deze claim wordt gebruikt voor het doorgeven van 'recht selectievakje'.
3. Player downloads client manifest van een CENC beveiligde inhoud en 'ziet' hello volgende:

   1. sleutel-ID
   2. Hallo-inhoud is beveiligd, CENC
   3. URL's aanschaf van licentie.
4. Player wordt een licentieaanvraag verkrijgen op basis van de browser Hallo/DRM die worden ondersteund. In het Hallo overname licentieaanvraag, sleutel-ID en Hallo JWT worden token ook verzonden. Service voor het leveren van licenties controleert Hallo JWT-token en Hallo claims die zijn opgenomen voordat het verlenende Hallo licentie nodig.

## <a name="implementation"></a>Implementatie
### <a name="implementation-procedures"></a>Procedures voor implementatie
Hallo-implementatie bevat Hallo stappen te volgen:

1. Test activa voorbereiden: een video test toomulti-bitrate coderen/pakket gefragmenteerd MP4 in Azure Media Services. Dit asset is niet beveiligd door DRM. DRM-beveiliging worden door dynamische beveiliging later uitgevoerd.
2. Maken van sleutel-ID en inhoud sleutel (optioneel van sleutel seed). Voor onze doel sleutelbeheersysteem is niet nodig omdat we zijn omgaan met slechts één set van sleutel-ID en sleutel voor een aantal test activa;
3. AMS API tooconfigure multi-DRM licentie levering van services voor Hallo test asset gebruiken. Als u aangepaste licentieservers door uw bedrijf of leveranciers van uw bedrijf in plaats van de licentie-services in Azure Media Services gebruikt, kunt u deze stap overslaan en licentie overname URL's in Hallo stap voor het configureren van de licentie levering opgeven. AMS API is benodigde toospecify sommige gedetailleerde configuraties, zoals autorisatie beleidsbeperking, licentie-antwoord sjablonen voor services van andere DRM-licenties, enzovoort. Op dit moment hello Azure-portal nog niet bieden Hallo gebruikersinterface nodig voor deze configuratie. U kunt zoeken naar API-niveau info en voorbeeldcode in Julia Kornich van document: [met behulp van PlayReady en/of Widevine Dynamic Common Encryption](media-services-protect-with-drm.md).
4. Gebruik AMS API tooconfigure asset leveringsbeleid voor Hallo test asset. U kunt zoeken naar API-niveau info en voorbeeldcode in Julia Kornich van document: [met behulp van PlayReady en/of Widevine Dynamic Common Encryption](media-services-protect-with-drm.md).
5. Maken en configureren van een Azure Active Directory-tenant in Azure.
6. Maken van een paar gebruikersaccounts en groepen in de Azure Active Directory-tenant: u moet ten minste maken 'EntitledUser' groeperen en een toothis gebruikersgroep toevoegen. Gebruikers in deze groep geeft recht controleren in de aanschaf van licentie en gebruikers die niet in deze groep toopass verificatieprocedure zal mislukken en zal niet kunnen tooacquire geen licentie. Een lid van deze groep 'EntitledUser' is een claim vereiste 'groepen' in hello JWT-token is uitgegeven door Azure AD. Deze vereiste claim moet worden opgegeven bij het configureren van multi-DRM licentie levering van services stap.
7. Een ASP.NET MVC-app die als host de video-speler fungeert maken. Deze ASP.NET-app worden beveiligd met gebruikersverificatie met hello Azure Active Directory-tenant. Juiste claims worden opgenomen in Hallo toegangstokens verkregen na verificatie van gebruiker. OpenID Connect API wordt aanbevolen voor deze stap. U moet tooinstall hello NuGet-pakketten te volgen:
   * Install-Package Microsoft.Azure.ActiveDirectory.GraphClient
   * Install-Package Microsoft.Owin.Security.OpenIdConnect
   * Install-Package Microsoft.Owin.Security.Cookies
   * Install-Package Microsoft.Owin.Host.SystemWeb
   * Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
8. Maken van een speler met [Azure Media Player-API](http://amp.azure.net/libs/amp/latest/docs/). [Azure Media-Player ProtectionInfo API](http://amp.azure.net/libs/amp/latest/docs/) kunt u toospecify welke toouse DRM-technologie op verschillende DRM-platform.
9. Testmatrix:

| **DRM** | **Browser** | **Resultaat van het gebruiksrecht heeft gebruiker** | **Resultaat van de gebruiker niet gemachtigd** |
| --- | --- | --- | --- |
| **PlayReady** |MS rand of IE11 op Windows 10 |Mislukt |Mislukt |
| **Widevine** |Chrome op Windows 10 |Mislukt |Mislukt |
| **FairPlay** |NOG TE BEPALEN | | |

George Trifonov van Azure Media Services-Team blog gedetailleerde stappen bij het instellen van Azure Active Directory voor een ASP.NET MVC player-app die is geschreven: [integreren Azure Media Services OWIN MVC op basis van de app met Azure Active Directory en beperken van de sleutel inhouddistributie op basis van claims JWT](http://gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).

George heeft ook een blog geschreven op [JWT-token verificatie in Azure Media Services en dynamische versleuteling](http://gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/). Hier vindt hij [op Azure AD-integratie met Azure Media Services-sleutellevering](https://github.com/AzureMediaServicesSamples/Key-delivery-with-AAD-integration/).

Voor informatie over Azure Active Directory:

* U vindt informatie voor ontwikkelaars in [Azure Active Directory-handleiding voor ontwikkelaars](../active-directory/active-directory-developers-guide.md).
* U vindt informatie voor beheerders in [beheren van uw Azure AD-Directory](../active-directory/active-directory-administer.md).

### <a name="some-gotchas-in-implementation"></a>Sommige gotchas in uitvoering
Er zijn enkele 'gotchas' Hallo uitvoering. Ideale geval kunt volgt de lijst met 'gotchas' hello u het oplossen van problemen als u problemen ondervindt.

1. **Certificaatverlener** URL moet eindigen met **'/'**.  

    **Doelgroep** moet Hallo speler toepassing client-ID en moet u ook toevoegen **'/'** aan Hallo einde van de URL-verlener Hallo.

        <add key="ida:audience" value="[Application Client ID GUID]" />
        <add key="ida:issuer" value="https://sts.windows.net/[AAD Tenant ID]/" />

    In [JWT Decoder](http://jwt.calebb.net/), ziet u **aud** en **iss** in Hallo JWT-token aan de onderstaande:

    ![1e gotcha](./media/media-services-cenc-with-multidrm-access-control/media-services-1st-gotcha.png)
2. Machtigingen toohello toepassing in AAD toevoegen (op het tabblad configureren van de toepassing hello). Dit is vereist voor elke toepassing (lokale en geïmplementeerde versie).

    ![2e gotcha](./media/media-services-cenc-with-multidrm-access-control/media-services-perms-to-other-apps.png)
3. Hallo rechts verlener bij het instellen van dynamische CENC beveiliging gebruiken:

        <add key="ida:issuer" value="https://sts.windows.net/[AAD Tenant ID]/"/>

    de volgende Hallo zal niet werken:

        <add key="ida:issuer" value="https://willzhanad.onmicrosoft.com/" />

    Hallo GUID is Hallo AAD-tenant-ID. Hallo GUID vindt u in de pop-up eindpunten in Azure-portal.
4. Verleen het lidmaatschap van claims van bevoegdheden. Zorg ervoor dat in het manifestbestand van AAD-toepassing, we hebben de volgende Hallo

    'groupMembershipClaims': 'All', (standaardwaarde Hallo is null)
5. Juiste TokenType instellen bij het maken van de vereisten van de beperking.

        objTokenRestrictionTemplate.TokenType = TokenType.JWT;

    Omdat het toevoegen van ondersteuning van JWT (AAD) bovendien tooSWT (ACS), is standaard Hallo TokenType TokenType.JWT. Als u SWT/ACS gebruikt, moet u tooTokenType.SWT instellen.

## <a name="additional-topics-for-implementation"></a>Aanvullende onderwerpen voor implementatie
Naast we wordt naar de schijf uss sommige extra onderwerpen in onze ontwerpen en implementeren.

### <a name="http-or-https"></a>HTTP of HTTPS?
Hallo ASP.NET MVC-spelertoepassing moesten moet Hallo volgende ondersteund:

1. Gebruikersverificatie via Azure AD die toobe onder HTTPS moet;
2. JWT-token exchange tussen client en Azure AD die toobe onder HTTPS moet;
3. DRM licentie overname door Hallo-client die vereist toobe onder HTTPS is als levering van de licentie wordt verstrekt door Azure Media Services. Natuurlijk schrijft PlayReady productpakket niet voor HTTPS voor de levering van licentie. Als de licentieserver PlayReady buiten Azure Media Services is, kan via HTTP of HTTPS worden gebruikt.

Daarom wordt player-ASP.NET-toepassing hello HTTPS gebruikt als een best practice. Dit betekent dat hello die Azure Media Player uitgevoerd in een HTTPS-pagina worden. Voor streaming we liever HTTP, dus moeten we tooconsider gemengde inhoud probleem.

1. Browser kan geen gemengde inhoud. Maar invoegtoepassingen zoals Silverlight en OSMF-invoegtoepassing voor smooth en STREEPJES zijn toegestaan. Gemengde inhoud is een beveiligingsprobleem - dit is vanwege toohello bedreiging van Hallo mogelijkheid tooinject Hallo schadelijke JS wat kan leiden tot klant gegevens toobe risico.  Browsers dit standaard blokkeren en tot nu toe Hallo alleen manier toowork omheen heeft hello (oorsprong) serverzijde, tooallow alle domeinen (ongeacht https of http). Dit is waarschijnlijk niet een goed idee ofwel.
2. Vermijd we gemengde inhoud: beide gebruik van HTTP of beide gebruik van HTTPS. Tijdens het afspelen van gemengde inhoud wordt silverlightSS tech vereist een gemengde inhoud waarschuwing uit te schakelen. technische flashSS verwerkt gemengde inhoud zonder gemengde inhoud waarschuwing.
3. Als uw streaming-eindpunt is gemaakt voordat augustus 2014, wordt deze geen ondersteuning voor HTTPS. In dit geval Maak en gebruik van een nieuwe streaming-eindpunt voor HTTPS.

In de implementatie van het Hallo-verwijzing, voor DRM beveiligde inhoud, zich toepassing en streaming onder HTTTPS. Voor open inhoud Hallo player hoeft niet verificatie of licentie, zodat u Hallo liberty toouse beide HTTP of HTTPS.

### <a name="azure-active-directory-signing-key-rollover"></a>Azure Active Directory sleutelrollover ondertekenen
Dit is een belangrijk punt tootake in aanmerking voor de implementatie. Als u geen rekening dit in uw implementatie houden, niet Hallo voltooid system uiteindelijk meer volledig binnen maximaal 6 weken.

Azure AD gebruikt bedrijfstak standaard tooestablish vertrouwensrelatie tussen zichzelf en toepassingen die gebruikmaken van Azure AD. Azure AD gebruikt met name een ondertekeningssleutel die uit een openbare en persoonlijke sleutelpaar bestaat. Als u Azure AD maakt een beveiligingstoken dat informatie over Hallo gebruiker bevat, wordt dit token is ondertekend door Azure AD met behulp van de persoonlijke sleutel voordat deze terug toohello toepassing wordt verzonden. tooverify die Hallo token geldig is en daadwerkelijk oorsprong van Azure AD, Hallo toepassing hello-token handtekening met de Hallo openbare sleutel die worden weergegeven door Azure AD dat is opgenomen in het document met federatieve metagegevens Hallo-tenant moet valideren. Deze openbare sleutel, en Hallo ondertekeningssleutel waarvan deze is afgeleid, is Hallo hetzelfde abonnement dat voor alle tenants in Azure AD gebruikt.

Gedetailleerde informatie over Azure AD-sleutelrollover vindt u in het Hallo-document: [belangrijke informatie over de overschakeling van de sleutel ondertekening in Azure AD](../active-directory/active-directory-signing-key-rollover.md).

Tussen Hallo [openbaar / persoonlijk sleutelpaar](https://login.microsoftonline.com/common/discovery/keys/),

* Hallo persoonlijke sleutel wordt gebruikt door Azure Active Directory-toogenerate JWT-token;
* Hallo openbare sleutel wordt gebruikt door een toepassing zoals DRM-Services voor het leveren van licenties in AMS tooverify hello JWT-token;

Voor beveiliging doel draait Azure Active Directory periodiek dit certificaat (elke 6 weken). In geval van inbreuk op de beveiliging kan Hallo sleutelrollover elk gewenst moment optreden. Daarom moeten Hallo licentie levering van services in AMS tooupdate Hallo openbare sleutel gebruikt als Azure AD Hallo sleutelpaar draait, anders de verificatie van de token in AMS mislukt en er is geen licentie wordt verleend.

Dit wordt bereikt door in te stellen TokenRestrictionTemplate.OpenIdConnectDiscoveryDocument bij het configureren van DRM-services voor het leveren van licenties.

Hallo JWT-tokenstroom is als hieronder:

1. Azure AD geeft Hallo JWT-token met huidige Hallo persoonlijke sleutel voor een geverifieerde gebruiker;
2. Wanneer u een speler ziet een CENC met multi-DRM beveiligde inhoud, zoekt het eerst Hallo JWT-token is uitgegeven door Azure AD.
3. Hallo player verzendt overname licentieaanvraag met Hallo JWT-token toolicense levering van services in AMS;
4. Hallo licentie levering van services in AMS gebruikt Hallo huidige/geldige openbare sleutel van Azure AD tooverify hello JWT-token, alvorens licenties.

DRM-services voor het leveren van licentie wordt altijd gecontroleerd of er Hallo huidige/geldige openbare sleutel van Azure AD. Hallo openbare sleutel die wordt aangeboden door Azure AD worden Hallo-sleutel die wordt gebruikt voor het controleren van een JWT-token dat is uitgegeven door Azure AD.

Wat gebeurt er als Hallo sleutelrollover treedt op nadat de AAD JWT-token wordt gegenereerd, maar voordat Hallo JWT token is verzonden door spelers tooDRM licentie levering van services in AMS voor verificatie?

Omdat een sleutel wordt mogelijk teruggedraaid te allen tijde, is altijd meer dan één geldige openbare sleutel beschikbaar is in het document met federatieve metagegevens Hallo. Azure Media Services-licentie levering kunt u elk Hallo sleutels opgegeven in Hallo document, omdat één sleutel, wordt mogelijk teruggedraaid binnenkort een andere kan worden de vervanging ervan, enzovoort.

### <a name="where-is-hello-access-token"></a>Waar Hallo het Access Token is?
Als u kijken hoe een web-app een API-app onder aanroept [toepassingsidentiteit met OAuth 2.0-Client referenties Grant](../active-directory/develop/active-directory-authentication-scenarios.md#web-application-to-web-api), Hallo authenticatiestroom is als hieronder:

1. Een gebruiker is aangemeld in tooAzure AD in Hallo-webtoepassing (Zie Hallo [webbrowser tooWeb toepassing](../active-directory/develop/active-directory-authentication-scenarios.md#web-browser-to-web-application).
2. Hello Azure AD-autorisatie-eindpunt wordt omgeleid Hallo gebruiker agent back toohello client-toepassing met een autorisatiecode. Hallo gebruikersagent retourneert autorisatie code toohello van de clienttoepassing omleidings-URI.
3. Hallo-webtoepassing moet een toegangstoken tooacquire zodat deze kan toohello web-API verifiëren en Hallo gewenst bron. Er wordt een aanvraag tooAzure van AD-tokeneindpunt, Hallo referentie, client-ID en web-API van toepassings-ID-URI. Deze geeft Hallo autorisatie code tooprove die Hallo gebruiker heeft ingestemd.
4. Azure AD verifieert Hallo-toepassing en een JWT-toegangstoken dat is gebruikt toocall Hallo web-API retourneert.
5. Via HTTPS gebruikt de webtoepassing Hallo Hallo JWT access token tooadd hello JWT-tekenreeks met een aanduiding 'Bearer' geretourneerd als Hallo autorisatie-header van Hallo aanvraag toohello web-API. Hallo-web-API valideert vervolgens Hallo JWT-token en als validatie geslaagd is, retourneert Hallo resource gewenst.

In deze stroom 'toepassings-id' vertrouwt Hallo web-API die Hallo web application Hallo geverifieerde gebruiker. Om deze reden wordt dit patroon van een vertrouwde subsysteem genoemd. Hallo [diagram op deze pagina](https://docs.microsoft.com/azure/active-directory/active-directory-protocols-oauth-code) wordt beschreven hoe de autorisatiecode stroom works verlenen.

In de overname van de licentie met tokenbeperking, we Hallo volgt hetzelfde patroon van de vertrouwde subsysteem. En Hallo licentie leveringsservice in Azure Media Services Hallo web-API-resource, Hallo 'back-end voor resource' is een webtoepassing moet tooaccess. Waar is dus Hallo toegangstoken?

We zijn immers toegangstoken ophalen uit Azure AD. Na een geslaagde verificatie, wordt autorisatiecode geretourneerd. Hallo autorisatiecode wordt vervolgens gebruikt samen met client-ID en app sleutel tooexchange toegangstoken. En Hallo toegangstoken voor toegang tot een 'aanwijzer' toepassing verwijst of vertegenwoordiging van Azure Media Services-service voor het leveren van licenties.

We moeten tooregister en Hallo 'aanwijzer' app in Azure AD configureren door Hallo onderstaande stappen te volgen:

1. In hello Azure AD-tenant

   * een toepassing (resource) met de aanmeldings-URL toevoegen:

   https://[resource_name].azurewebsites.NET/ en

   * App-ID-URL:

   https://[aad_tenant_name].onmicrosoft.com/[resource_name];
2. Voeg een nieuwe sleutel voor Hallo resource-app
3. Hallo app manifestbestand bijwerken zodat Hallo groupMembershipClaims eigenschap heeft Hallo volgende waarde: 'groupMembershipClaims': 'All',  
4. Toevoegen in hello Azure AD-app wijst toohello player web-app in Hallo sectie 'machtigingen tooother toepassingen' Hallo resource-app die is toegevoegd in stap 1 hierboven. Controleer onder 'gemachtigd' vinkje 'Toegang [resource_name]'. Hiermee geeft u Hallo web-app-machtiging toocreate toegangstokens voor toegang tot Hallo resource app. U moet dit doen voor zowel lokale als geïmplementeerde versie van Hallo web-app als u met Visual Studio en Azure-web-app ontwikkelt.

Hallo JWT-token is uitgegeven door Azure AD is daarom inderdaad Hallo toegangstoken voor toegang tot deze resource 'aanwijzer'.

### <a name="what-about-live-streaming"></a>Wat vindt Live Streaming?
In bovenstaande Hallo, heeft onze bespreking is gericht op activa op aanvraag. Wat vindt live streamen?

Hallo goed nieuws is waarmee u precies kunt dezelfde ontwerpen en implementeren voor het beveiligen van live streamen in Azure Media Services door te behandelen Hallo asset die zijn gekoppeld aan een programma als een 'VOD-activum' Hallo.

Het is met name bekend dat toodo live streamen in Azure Media Services, moet u toocreate een kanaal en vervolgens een programma onder Hallo-kanaal. toocreate hello programma, moet u toocreate een asset die Hallo live archief voor Hallo programma zal bevatten. In de volgorde tooprovide CENC met multi-DRM bescherming van Hallo live-inhoud, hoeft u toodo, is tooapply Hallo dezelfde setup/verwerking toohello asset alsof het een activum' VOD' voordat u Hallo programma start.

### <a name="what-about-license-servers-outside-of-azure-media-services"></a>Hoe zit het licentieservers buiten Azure Media Services?
Vaak kunnen klanten hebben geïnvesteerd in licentie server-farm zich in hun eigen gegevens centreren of gehost door DRM-providers. Gelukkig Azure Media Services Content Protection kunt u toooperate in de modus voor hybride: inhoud gehost en dynamisch in Azure Media Services beveiligd terwijl DRM-licenties worden geleverd door servers buiten Azure Media Services. Er zijn in dit geval Hallo van wijzigingen te volgen:

1. Hallo Secure Token Service behoeften tooissue tokens die worden geaccepteerd en kunnen worden gecontroleerd door Hallo licentie server-farm. Widevine-licentieservers Hallo geleverd door Axinom vereist bijvoorbeeld een JWT-token die "recht bericht" bevat. Daarom moet u een STS tooissue toohave dergelijke JWT-token. Hallo auteurs een dergelijke implementatie hebt voltooid en u kunt Hallo details vinden in het document in volgende Hallo [documentatiecentrum van Azure](https://azure.microsoft.com/documentation/): [met behulp van Axinom toodeliver Widevine-licenties tooAzure Media Services](media-services-axinom-integration.md).
2. U hoeft niet meer tooconfigure license levering-service (ContentKeyAuthorizationPolicy) in Azure Media Services. Wat u moet toodo is tooprovide Hallo licentie overname URL's (voor PlayReady, Widevine en FairPlay) wanneer u AssetDeliveryPolicy bij het instellen van CENC met multi-DRM configureert.

### <a name="what-if-i-want-toouse-a-custom-sts"></a>Wat gebeurt er als ik wil een aangepaste STS toouse?
Er zijn een aantal oorzaken hebben die een klant toouse een aangepaste STS (Secure Token Service kunt) voor het ontwikkelen van JWT-tokens. Sommige hiervan zijn:

1. Hallo identiteit Provider (IDP) die wordt gebruikt door de klant Hallo biedt geen ondersteuning voor STS. In dit geval een aangepaste STS mogelijk een optie.
2. Hallo-klant moet mogelijk meer flexibele of strikter besturingselement in STS met van klant abonnee factureringssysteem integreren. Bijvoorbeeld, een operator MVPD mogelijk meerdere OTT abonnee pakketten bieden zoals premium, basic, sport, enzovoort Hallo operator desgewenst toomatch Hallo claims in een token met een abonnee pakket zodat alleen de inhoud in de juiste pakket Hallo beschikbaar wordt gesteld. In dit geval een aangepaste STS biedt Hallo flexibiliteit en meer controle nodig.

Twee wijzigingen moeten nemen wanneer u met een aangepaste STS toobe:

1. Wanneer u service voor het leveren van licenties voor een asset configureert, moet u toospecify Hallo-beveiligingssleutel gebruikt voor verificatie door Hallo aangepaste STS (meer details hieronder) in plaats van de huidige sleutel Hallo van Azure Active Directory.
2. Wanneer een JTW-token wordt gegenereerd, wordt een beveiligingssleutel is opgegeven in plaats van Hallo persoonlijke sleutel van het certificaat van de huidige X509 Hallo in Azure Active Directory.

Er zijn twee soorten beveiligingssleutels:

1. Symmetrische sleutel: Hallo dezelfde sleutel wordt gebruikt voor zowel genereren en controleren van een JWT-token
2. Asymmetrische sleutel: een openbaar / persoonlijk sleutelpaar in een X509 certificaat met persoonlijke sleutel voor het versleutelen/genereren van een JWT-token en Hallo openbare sleutel voor het controleren van Hallo-token wordt gebruikt.

#### <a name="tech-note"></a>Technische opmerking
Als u gebruikmaakt van .NET Framework / C# als uw ontwikkelplatform Hallo X509 certificaat dat wordt gebruikt voor asymmetrische beveiligingssleutel sleutellengte ten minste 2048 moet hebben. Dit is een vereiste van Hallo klasse System.IdentityModel.Tokens.X509AsymmetricSecurityKey in .NET Framework. Anders Hallo volgende uitzondering gegenereerd:

IDX10630: Hallo 'System.IdentityModel.Tokens.X509AsymmetricSecurityKey' voor het ondertekenen van mag niet kleiner dan '2048-bits zijn.

## <a name="hello-completed-system-and-test"></a>Hallo voltooid systeem en testen
We doorlopen enkele scenario's in de end-to-end-systeem Hallo voltooid zodat lezers een eenvoudige 'afbeelding' hello gedrag hebben kunnen voordat u een aanmeldingsaccount.

Hallo player-webtoepassing en de aanmelding vindt [hier](https://openidconnectweb.azurewebsites.net/).

Als wat u moet 'niet geïntegreerde' scenario: video activa gehost in Azure Media Services welke zijn ofwel niet zijn beveiligd of DRM beveiligde maar zonder tokenverificatie (uitgeven van een licentie toowhoever aangevraagd), kunt u deze testen zonder aanmelding (door het overschakelen tooHTTP als uw videostreaming via HTTP).

Als wat u moet de geïntegreerde scenario end-to-end: video activa ligt onder de dynamische DRM-beveiliging in Azure Media Services met tokenverificatie en JWT-token wordt gegenereerd door Azure AD, moet u toologin.

### <a name="user-login"></a>Gebruikersaanmelding
In de volgorde tootest Hallo end-to-end geïntegreerde DRM-systeem moet u toohave een 'account' gemaakt of toegevoegd.

Welk account?

Hoewel Azure oorspronkelijk alleen toegang verleende aan Microsoft-accountgebruikers, staat deze nu toegang verleend aan gebruikers van beide systemen. Dit wordt mogelijk gemaakt doordat alle hello Azure eigenschappen vertrouwensrelatie Azure AD voor de verificatie door Azure AD bedrijfsgebruikers en door een federatieve relatie te maken waarin Azure AD Hallo Microsoft-account klantidentiteitssysteem vertrouwensrelaties gebruikers van de consument tooauthenticate. Azure AD is als gevolg hiervan kunnen tooauthenticate ' Microsoft-gastaccounts als 'systeemeigen' Azure AD-accounts.

Omdat Azure AD wordt vertrouwd domein van de Microsoft-Account (MSA), kunt u de accounts vanaf elke Hallo na domeinen toohello aangepaste Azure AD-tenant en Hallo account toologin gebruiken kunt toevoegen:

| **Domeinnaam** | **Domein** |
| --- | --- |
| **Domein van de aangepaste Azure AD-tenant** |somename.onmicrosoft.com |
| **Bedrijfsdomein** |Microsoft.com |
| **Microsoft-Account (MSA)-domein** |Outlook.com, live.com, hotmail.com |

U kunt contact opnemen met een van de Hallo auteurs toohave een account te maken of toegevoegd voor u.

Hieronder vindt u Hallo schermopnamen van verschillende aanmeldingspagina's die worden gebruikt door andere domeinaccounts.

**Aangepaste Azure AD-tenant domeinaccount**: In dit geval wordt er aangepaste aanmeldingspagina Hallo van Hallo aangepaste Azure AD-tenant-domein.

![Aangepaste Azure AD-tenant domeinaccount](./media/media-services-cenc-with-multidrm-access-control/media-services-ad-tenant-domain1.png)

**Microsoft-domeinaccount met smartcard**: In dit geval er Hallo-aanmeldingspagina is aangepast door Microsoft zakelijke IT-medewerkers met tweeledige verificatie.

![Aangepaste Azure AD-tenant domeinaccount](./media/media-services-cenc-with-multidrm-access-control/media-services-ad-tenant-domain2.png)

**Microsoft-Account (MSA)**: In dit geval ziet u de aanmeldingspagina Hallo van Microsoft-Account voor consumenten.

![Aangepaste Azure AD-tenant domeinaccount](./media/media-services-cenc-with-multidrm-access-control/media-services-ad-tenant-domain3.png)

### <a name="using-encrypted-media-extensions-for-playready"></a>Versleutelde Media-extensies gebruiken voor PlayReady
Hallo op een moderne browser met versleuteld Media extensies (EME) voor ondersteuning, zoals Internet Explorer 11 op Windows 8.1 en omhoog en Microsoft Edge-browser op Windows 10, PlayReady PlayReady DRM onderliggende voor EME.

![Met behulp van EME voor PlayReady](./media/media-services-cenc-with-multidrm-access-control/media-services-eme-for-playready1.png)

Hallo donker player gebied is vanwege toohello feit PlayReady beveiliging voorkomt dat een schermopname van beveiligde video aanbrengen.

Hallo toont volgende scherm Hallo player-invoegtoepassingen en muis/EME ondersteuning.

![Met behulp van EME voor PlayReady](./media/media-services-cenc-with-multidrm-access-control/media-services-eme-for-playready2.png)

EME in de Microsoft Edge en Internet Explorer 11 op Windows 10 kunt aanroepen van [PlayReady SL3000](https://www.microsoft.com/playready/features/EnhancedContentProtection.aspx/) op Windows 10-apparaten die dit ondersteunen. PlayReady SL3000 ontgrendelt Hallo stroom van de inhoud van de uitgebreide premium (4K, Kopregel, enzovoort) en nieuwe inhoud leveringsmodel (vroege venster voor verbeterde inhoud).

Ligt de nadruk op apparaten met Windows hello: PlayReady is Hallo alleen DRM in Hallo HW beschikbaar op Windows-apparaten (PlayReady SL3000). Een streaming-service met PlayReady via EME of via een UWP-toepassing en bieden een hogere videokwaliteit met PlayReady SL3000 dan een andere DRM. Normaal gesproken 2 kB inhoud worden overgebracht via Chrome of Firefox en 4 K-inhoud via Microsoft Edge/IE11 of een UWP-toepassing op Hallo hetzelfde apparaat (afhankelijk van de service-instellingen en implementatie).

#### <a name="using-eme-for-widevine"></a>Met behulp van EME voor Widevine
Op een moderne browser met EME/Widevine-ondersteuning, zoals Chrome 41 + op Windows 10, Windows 8.1, Mac OS x Yosemite en Chrome op Android 4.4.4 is Google Widevine DRM achter EME Hallo.

![Met behulp van EME voor Widevine](./media/media-services-cenc-with-multidrm-access-control/media-services-eme-for-widevine1.png)

U ziet dat Widevine voorkomt niet dat een schermopname van beveiligde video aanbrengen.

![Met behulp van EME voor Widevine](./media/media-services-cenc-with-multidrm-access-control/media-services-eme-for-widevine2.png)

### <a name="not-entitled-users"></a>Geen recht gebruikers
Als een gebruiker is geen lid van groep 'Gebruikers het recht', Hallo gebruiker niet kunnen toopass 'recht selectievakje' en service Hallo multi-DRM-licenties weigert tooissue Hallo aangevraagde licentie zoals hieronder wordt weergegeven. Hallo gedetailleerde beschrijving is ' licentie ophalen is mislukt ", die is ontworpen.

![Heeft niet het recht gebruikers](./media/media-services-cenc-with-multidrm-access-control/media-services-unentitledusers.png)

### <a name="running-custom-secure-token-service"></a>Aangepaste Secure Token Service uitgevoerd
Hallo scenario van het uitvoeren van aangepaste Secure Token Service (STS) worden Hallo JWT-token uitgegeven door aangepaste STS Hallo met zowel symmetrisch als asymmetrisch sleutel.

Hallo-aanvraag van het gebruik van de symmetrische sleutel (met behulp van Chrome):

![Aangepaste STS uitgevoerd](./media/media-services-cenc-with-multidrm-access-control/media-services-running-sts1.png)

aanvraag van het gebruik van asymmetrische sleutel via een X509 Hallo van het certificaat (met behulp van Microsoft moderne browser).

![Aangepaste STS uitgevoerd](./media/media-services-cenc-with-multidrm-access-control/media-services-running-sts2.png)

In beide Hallo bovenstaande gevallen Hallo gebruiker verificatie blijft dezelfde – via Azure AD. Hallo enige verschil is dat JWT-tokens worden uitgegeven door aangepaste STS Hallo in plaats van Azure AD. Natuurlijk bij het configureren van dynamische CENC beveiliging Hallo beperking van de service voor het leveren van licenties geeft Hallo type JWT-token zowel symmetrisch als asymmetrisch sleutel.

## <a name="summary"></a>Samenvatting
In dit document besproken CENC met meerdere native-DRM en toegangsbeheer via tokenverificatie: het ontwerp en de uitvoering ervan met behulp van Azure, Azure Media Services en Azure Media Player.

* Een referentie-ontwerp wordt weergegeven waarin alle benodigde Hallo-onderdelen in een subsysteem DRM/CENC;
* De implementatie van een verwijzing op Azure, Azure Media Services en Azure Media Player.
* Sommige onderwerpen die direct betrokken zijn bij het Hallo-ontwerp en de implementatie worden ook besproken.

## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
 
