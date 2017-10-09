---
title: aaaSecurity overwegingen voor Azure AD-toepassingsproxy | Microsoft Docs
description: Bevat informatie over de beveiligingsoverwegingen voor het gebruik van Azure AD-toepassingsproxy
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: ebd14b9d1fc8f4629c5916e5a910595727d935d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="security-considerations-for-accessing-apps-remotely-with-azure-ad-application-proxy"></a>Beveiligingsoverwegingen voor toegang tot apps op afstand met Azure AD-toepassingsproxy

Dit artikel wordt uitgelegd hoe Azure Active Directory-toepassingsproxy voorziet in een beveiligde service voor het publiceren en externe toegang tot uw toepassingen.

Hallo volgende diagram toont hoe Azure AD kunt veilige externe toegang tooyour on-premises toepassingen.

 ![Diagram van veilige externe toegang via Azure AD-toepassingsproxy](./media/application-proxy-security-considerations/secure-remote-access.png)

## <a name="security-benefits"></a>De voordelen van beveiliging

Azure AD-toepassingsproxy biedt Hallo volgende beveiligingsvoordelen:

### <a name="authenticated-access"></a>Geverifieerde toegang 

Als u toouse Azure Active Directory vooraf-verificatie kiest, klikt u vervolgens alleen geverifieerde verbindingen hebben toegang tot uw netwerk.

Azure AD-toepassingsproxy is afhankelijk van hello Azure AD-beveiligingstokenservice (STS) voor alle verificatie.  Vooraf-verificatie, blokkeert door de aard een groot aantal anonieme aanvallen, omdat alleen geauthenticeerde identiteiten Hallo back-endtoepassing kunnen openen.

Als u Passthrough als uw methode voor verificatie vooraf kiest, kunt u voordeel niet ophalen. 

### <a name="conditional-access"></a>Voorwaardelijke toegang

Rijkere beleid besturingselementen voordat verbindingen tooyour netwerk tot stand worden gebracht van toepassing.

Met [voorwaardelijke toegang](active-directory-conditional-access-azuread-connected-apps.md), kunt u beperkingen op welk verkeer wordt toegestaan tooaccess uw back-end-toepassingen. Kunt u beleidsregels die aanmeldingen op basis van locatie, sterkte van verificatie en gebruikersprofiel risico beperken.

U kunt beleid voor voorwaardelijke toegang tooconfigure multi-Factor Authentication ook gebruiken voor het toevoegen van een andere laag van beveiliging tooyour gebruikersverificaties. 

### <a name="traffic-termination"></a>Beëindiging van verkeer

Al het verkeer wordt beëindigd in Hallo cloud.

Omdat Azure AD-toepassingsproxy is een reverse proxy, wordt alle verkeer tooback-end-toepassingen op Hallo-service beëindigd. Hallo sessie kunt ophalen opnieuw tot stand gebracht met de Hallo back-endserver, wat betekent dat uw back-endservers niet zijn beschikbaar gesteld toodirect HTTP-verkeer. Deze configuratie betekent dat u beter beschermd zijn tegen gerichte aanvallen.

### <a name="all-access-is-outbound"></a>Alle gebruikers de toegang is uitgaand 

U hoeft niet tooopen binnenkomende verbindingen toohello bedrijfsnetwerk.

Application Proxy connectors alleen uitgaande verbindingen toohello Azure AD-toepassingsproxy service, wat betekent dat niet tooopen firewallpoorten voor binnenkomende verbindingen hoeft gebruiken. Traditionele proxy's vereist een perimeternetwerk (ook wel bekend als *DMZ*, *gedemilitariseerde zone*, of *gescreend subnet*) en toegang toounauthenticated toegestaan verbindingen aan de rand van Hallo-netwerk. Dit scenario moet u veel aanvullende investeringen in de webtoepassing firewall-producten tooanalyze verkeer en bieden aanvullende bescherming toohello omgeving. Met toepassingsproxy hoeft u niet een perimeternetwerk omdat alle verbindingen uitgaande zijn en plaats via een beveiligd kanaal vindt.

Zie voor meer informatie over connectors [inzicht in Azure AD-toepassingsproxy connectors](application-proxy-understand-connectors.md).

### <a name="cloud-scale-analytics-and-machine-learning"></a>Cloud-scale analytics en machine learning 

Geavanceerde beveiliging worden opgehaald.

Omdat deze deel uitmaakt van Azure Active Directory, kunnen gebruikmaken van toepassingsproxy [Azure AD Identity Protection](active-directory-identityprotection.md)met machine learning gebaseerde intelligence en gegevens uit Microsoft Security Response Center Hallo en Digital Crimes Unit. Samen we proactief identificeren waarmee is geknoeid en bieden real-timebeveiliging van aanmeldingen met een hoog risico. We rekening gehouden met meerdere factoren, zoals toegang vanaf geïnfecteerde apparaten, via anonymizing netwerken, en vanaf locaties ongebruikelijk zijn en onwaarschijnlijk.

Veel van deze rapporten en gebeurtenissen zijn al beschikbaar via een API voor de integratie met uw security information en event management (SIEM)-systemen.

### <a name="remote-access-as-a-service"></a>Externe toegang als een service

U hebt geen tooworry over het onderhouden en patchen lokale servers.

Niet-gepatchte software nog steeds accounts voor een groot aantal aanvallen. Azure AD-toepassingsproxy is een Internet-scale-service die Microsoft eigenaar is, zodat u altijd de meest recente beveiligingspatches Hallo en upgrades.

tooimprove hello beveiliging van toepassingen die zijn gepubliceerd door Azure AD-toepassingsproxy, we blokkeren web crawler robots indexeren en uw toepassingen wilt archiveren. Elke keer web crawler robot probeert op te halen van de robot-instellingen voor een gepubliceerde app toepassingsproxy geantwoord met een robots.txt-bestand met `User-agent: * Disallow: /`.

## <a name="under-hello-hood"></a>Achter de schermen Hallo

Azure AD-toepassingsproxy bestaat uit twee delen:

* Hallo-cloudservice: deze service wordt uitgevoerd in Azure, en is waar Hallo externe client/gebruiker verbindingen zijn gemaakt.
* [Hallo on-premises-connector](application-proxy-understand-connectors.md): een onderdeel van de lokale, Hallo connector luistert naar aanvragen van hello Azure AD-toepassingsproxy service en verbindingen toohello interne toepassingen verwerkt. 

Een stroom tussen Hallo-connector en Hallo toepassingsproxy service tot stand wordt gebracht wanneer:

* Hallo connector is eerst ingesteld.
* Hallo connector haalt de configuratie-informatie uit Hallo service voor toepassingsproxy.
* Een gebruiker toegang krijgt tot een gepubliceerde toepassing.

>[!NOTE]
>Alle communicatie vindt plaats via SSL en ze altijd afkomstig van Hallo connector toohello service voor toepassingsproxy. Hallo-service is alleen uitgaand.

Hallo-connector maakt gebruik van een client certificate tooauthenticate toohello service voor toepassingsproxy voor bijna alle aanroepen. Hallo alleen wordt uitzondering toothis stap van de eerste installatie hello, waarbij het clientcertificaat Hallo tot stand is gebracht.

### <a name="installing-hello-connector"></a>Hallo-connector installeren

Wanneer eerst Hallo connector instelt, plaatsvinden Hallo na stroom gebeurtenissen:

1. registratie Hallo-toohello connectorservice wordt uitgevoerd als onderdeel van installatie Hallo van Hallo-connector. Gebruikers zijn na vragen aan gebruiker tooenter hun Azure AD-referenties. Het token dat is verkregen van deze verificatie wordt vervolgens toohello Azure AD-toepassingsproxy service weergegeven.
2. Hallo service voor toepassingsproxy evalueert Hallo-token. Hiermee zorgt u ervoor dat Hallo-gebruiker is een bedrijfsbeheerder binnen Hallo-tenant die Hallo token is uitgegeven voor. Als het Hallo-gebruiker is geen beheerder, wordt Hallo-proces beëindigd.
3. Hallo-connector een certificaataanvraag client genereert en wordt doorgegeven, samen met de Hallo token, toohello service voor toepassingsproxy. Hallo-service controleert of Hallo-token op zijn beurt en Hallo-clientaanvraag certificaat ondertekent.
4. Hallo-connector gebruikt Hallo clientcertificaat voor toekomstige communicatie met de Hallo service voor toepassingsproxy.
5. Hallo-connector voert een initiële pull van configuratiegegevens Hallo-systeem van Hallo-service met behulp van het clientcertificaat en het is nu gereed tootake aanvragen.

### <a name="updating-hello-configuration-settings"></a>Hallo-configuratie-instellingen bijwerken

Wanneer de service voor toepassingsproxy Hallo Hallo configuratie-instellingen bijwerken, plaatsvinden Hallo na stroom gebeurtenissen:

1. toohello configuratie eindpunt in de service voor toepassingsproxy Hallo verbindt Hallo connector met behulp van het clientcertificaat.
2. Nadat het Hallo-clientcertificaat is gevalideerd, Hallo service voor toepassingsproxy configuratie toohello gegevensconnector geretourneerd (bijvoorbeeld Hallo connector groep die connector Hallo moeten deel uitmaken van).
3. Als het huidige certificaat Hallo meer dan 180 dagen is, genereert Hallo connector een nieuwe certificaataanvraag Hallo clientcertificaat effectief per 180 dagen bijgewerkt.

### <a name="accessing-published-applications"></a>Toegang tot gepubliceerde toepassingen

Als gebruikers toegang hebben tot een gepubliceerde toepassing, plaatsvinden hello volgende gebeurtenissen tussen Hallo-service voor toepassingsproxy en Hallo Application Proxy connector:

1. [Hallo service verifieert de gebruiker Hallo voor Hallo-app](#the-service-checks-the-configuration-settings-for-the-app)
2. [Hallo service plaatst een aanvraag in wachtrij Hallo-connector](#The-service-places-a-request-in-the-connector-queue)
3. [Hallo-aanvraag uit de wachtrij hello wordt verwerkt door een connector](#the-connector-receives-the-request-from-the-queue)
4. [Hallo-connector wordt gewacht op een reactie](#the-connector-waits-for-a-response)
5. [Hallo streams gegevens toohello servicegebruiker](#the-service-streams-data-to-the-user)

toolearn meer informatie over wat plaatsvindt in elk van deze stappen blijven lezen.


#### <a name="1-hello-service-authenticates-hello-user-for-hello-app"></a>1. Hallo service verifieert de gebruiker Hallo voor Hallo-app

Als u Hallo app toouse Passthrough geconfigureerd als de methode voor verificatie vooraf, worden Hallo stappen in deze sectie overgeslagen.

Als u Hallo app toopreauthenticate geconfigureerd met Azure AD, gebruikers omgeleide toohello Azure AD STS tooauthenticate en hello volgende stappen worden uitgevoerd:

1. Toepassingsproxy controleert u alle vereisten voor het beleid van voorwaardelijke toegang voor specifieke toepassing hello. Deze stap zorgt ervoor dat gebruiker Hallo toohello toepassing is toegewezen. Als verificatie in twee stappen vereist is, vraagt Hallo verificatie sequence Hallo gebruiker om een tweede methode voor verificatie.

2. Nadat alle controles zijn verstreken, hello Azure AD-STS geeft een ondertekende token voor de toepassing hello en omleidingen Hallo gebruiker back toohello service voor toepassingsproxy.

3. Toepassingsproxy verifieert dat Hallo-token is uitgegeven toocorrect Hallo-toepassing. Hiermee worden ook andere controles uitgevoerd, zoals ervoor te zorgen dat Hallo token is ondertekend door Azure AD en dat deze wordt nog steeds binnen het geldige Hallo-venster.

4. Toepassingsproxy stelt een gecodeerde verificatie cookie tooindicate dat verificatie toohello toepassing is opgetreden. Hallo bevat cookie de tijdstempel van een vervaldatum die gebaseerd op het Hallo-token van Azure AD en andere gegevens zoals Hallo-gebruikersnaam die verificatie Hallo is gebaseerd op. Hallo cookie wordt versleuteld met een persoonlijke sleutel alleen toohello service voor toepassingsproxy bekend.

5. Application Proxy omleidingen Hallo gebruiker back toohello gevraagde oorspronkelijk URL.

Als een deel van vooraf-verificatie stappen Hallo mislukt, Hallo gebruikersaanvraag wordt geweigerd en Hallo gebruiker een bericht weergegeven dat aangeeft Hallo bron van Hallo probleem wordt weergegeven.


#### <a name="2-hello-service-places-a-request-in-hello-connector-queue"></a>2. Hallo service plaatst een aanvraag in wachtrij Hallo-connector

Connectors Houd een uitgaande verbinding open toohello service voor toepassingsproxy. Als een aanvraag binnenkomt, wachtrijen Hallo service Hallo-aanvraag voor een van de geopende verbindingen Hallo voor Hallo connector toopick up.

Hallo-aanvraag bevat de items uit de toepassing hello, zoals aanvraagheaders hello, gegevens van Hallo gecodeerd cookie, Hallo gebruiker maken voor aanvraag Hallo en Hallo aanvragen ID. Hoewel de gegevens van Hallo gecodeerd cookie met Hallo is verzonden, is geen Hallo verificatiecookie zelf.

#### <a name="3-hello-connector-processes-hello-request-from-hello-queue"></a>3. Hallo connector Hallo-aanvraag uit de wachtrij Hallo verwerkt. 

Toepassingsproxy voert op basis van aanvraag hello, een Hallo van de volgende activiteiten:

* Als het Hallo-aanvraag is een eenvoudige operatie (bijvoorbeeld: Er zijn geen gegevens binnen de hoofdcode van Hallo met een RESTful *ophalen* aanvraag), Hallo-connector maakt een verbinding toohello interne doelbron en wordt er gewacht totdat een antwoord.

* Als Hallo aanvraag gegevens gekoppeld in de hoofdtekst van het Hallo heeft (bijvoorbeeld een RESTful *POST* bewerking), Hallo connector een uitgaande verbinding maakt met behulp van Hallo client certificate toohello toepassingsproxy exemplaar. Er wordt deze verbinding toorequest Hallo gegevens en opent u een verbinding toohello interne resource. Nadat het Hallo-aanvraag van Hallo-connector ontvangen, wordt Hallo toepassingsproxy service begint met het accepteren van de inhoud van de gebruiker Hallo en verzendt gegevens toohello connector. Hallo-connector stuurt op zijn beurt Hallo gegevens toohello interne resource.

#### <a name="4-hello-connector-waits-for-a-response"></a>4. het Hallo-connector wacht een antwoord.

Nadat het Hallo-aanvraag en de overdracht van alle inhoud toohello back-end is voltooid, Hallo-connector wordt gewacht op een antwoord.

Zodra er een antwoord is ontvangen, Hallo-connector maakt een service voor toepassingsproxy toohello uitgaande verbinding, tooreturn Hallo header details en begin met het Hallo-return gegevensstromen.

#### <a name="5-hello-service-streams-data-toohello-user"></a>5. Hallo streams gegevens toohello gebruiker voor de service. 

Sommige verwerking van de toepassing hello optreden hier. Als u toepassingsproxy tootranslate kop- of -URL's in uw toepassing hebt geconfigureerd, gebeurt dat verwerking zo nodig tijdens deze stap.


## <a name="next-steps"></a>Volgende stappen

[Netwerk topologie overwegingen bij het gebruik van Azure AD-toepassingsproxy](application-proxy-network-topology-considerations.md)

[Azure AD-toepassingsproxy connectors begrijpen](application-proxy-understand-connectors.md)
