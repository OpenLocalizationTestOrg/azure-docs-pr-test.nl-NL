---
title: Active Directory-risicogebeurtenissen aaaAzure | Microsoft Docs
description: In dit onderwerp vindt u een gedetailleerd overzicht van wat risicogebeurtenissen zijn.
services: active-directory
keywords: beveiliging voor Azure active directory-identiteit, beveiliging, risico, risiconiveau, beveiligingsprobleem, beveiligingsbeleid
author: MarkusVi
manager: femila
ms.assetid: fa2c8b51-d43d-4349-8308-97e87665400b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: d771c1f43707744aac728c4f72000d855cbd6e1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-risk-events"></a>Azure Active Directory-risicogebeurtenissen

Hallo overgrote deel van de beveiliging schendingen nemen plaatsen wanneer aanvallers toegang tooan omgeving krijgen door de identiteit van een gebruiker te stelen. Detectie van verdachte identiteiten is geen eenvoudige taak. Azure Active Directory maakt gebruik van geavanceerde machine learning-algoritmen en methodiek toodetect verdachte acties die gerelateerd tooyour gebruikersaccounts zijn. Elk gedetecteerd verdachte actie is opgeslagen in een record aangeroepen *risicogebeurtenis*.

Azure Active Directory detecteert op dit moment zes typen risicogebeurtenissen die:

- [Gebruikers met gelekte referenties](#leaked-credentials) 
- [Aanmeldingen vanaf anonieme IP-adressen](#sign-ins-from-anonymous-ip-addresses) 
- [Onmogelijke reis tooatypical locaties](#impossible-travel-to-atypical-locations) 
- [Aanmeldingen vanaf onbekende locaties](#sign-in-from-unfamiliar-locations)
- [Aanmeldingen vanaf geïnfecteerde apparaten](#sign-ins-from-infected-devices) 
- [Aanmeldingen vanaf IP-adressen met verdachte activiteiten](#sign-ins-from-ip-addresses-with-suspicious-activity) 


![Risicogebeurtenis](./media/active-directory-reporting-risk-events/91.png)

In dit onderwerp biedt u een gedetailleerd overzicht van welke gebeurtenissen van de risico's zijn en hoe u ze kunt gebruiken tooprotect de identiteiten van uw Azure AD.


## <a name="risk-event-types"></a>Risicogebeurtenistypen

Hallo risico gebeurtenis type eigenschap is dat een id voor Hallo verdachte actie een record van de gebeurtenis risico is gemaakt.  
Microsoft continue investeringen in het detectieproces Hallo leiden tot:

- Verbeteringen toohello detectie nauwkeurigheid van de bestaande risicogebeurtenissen 
- Nieuwe typen van de risico's gebeurtenissen die in toekomstige Hallo worden toegevoegd

### <a name="leaked-credentials"></a>Gelekte aanmeldingsreferenties

Wanneer cybercriminelen inbreuk geldige wachtwoorden van legitieme gebruikers, delen Hallo criminelen vaak deze referenties. Dit gebeurt gewoonlijk door ze te posten openbaar op Hallo donker web- of sites of door handel of Hallo-referenties op Hallo zwarte markt verkopen. Hallo Microsoft gelekte referenties service verkrijgt gebruikersnaam / wachtwoord paren door de bewaking van openbare en donkere websites en door met:

- Onderzoekers
- Justitie en politie
- Microsoft Security-teams
- Andere betrouwbare bronnen 

Wanneer Hallo service verkrijgt gebruikersnaam / wachtwoord paren, worden ze gecontroleerd tegen de huidige geldige referenties AAD-gebruikers. Wanneer een overeenkomst is gevonden, betekent dit dat het wachtwoord van een gebruiker is aangetast, en een *gelekte referenties risicogebeurtenis* wordt gemaakt.

### <a name="sign-ins-from-anonymous-ip-addresses"></a>Aanmeldingen vanaf anonieme IP-adressen

Dit type risico gebeurtenis identificeert gebruikers die zich heeft aangemeld vanaf een IP-adres dat is geïdentificeerd als een anonieme proxy IP-adres. Deze proxy's worden gebruikt door mensen willen toohide van hun apparaat IP-adres en kan worden gebruikt voor kwade bedoelingen.


### <a name="impossible-travel-tooatypical-locations"></a>Onmogelijke reis tooatypical locaties

Dit type risico gebeurtenis identificeert twee aanmeldingen die afkomstig zijn van geografisch verafgelegen locaties, waarbij ten minste één Hallo locaties mogelijk ook ongebruikelijk voor gebruiker hello, krijgt het verleden gedrag. Bovendien Hallo tijd tussen Hallo twee aanmeldingen is korter dan Hallo tijd die nodig zou hebben Hallo gebruiker tootravel van de eerste locatie toohello Hallo tweede, die aangeeft dat een andere gebruiker gebruikt dezelfde Hallo referenties. 

Deze machine learning-algoritme die wordt genegeerd voor de hand liggende '*valse positieven*' toohello onmogelijke reis voorwaarde, zoals VPN-verbindingen en de locaties die regelmatig worden gebruikt door andere gebruikers in de organisatie Hallo bijdragen.  Hallo systeem heeft een initiële learning periode van 14 dagen gedurende welke aan een nieuwe gebruiker aanmelden gedrag leert.

### <a name="sign-in-from-unfamiliar-locations"></a>Aanmelden vanaf onbekende locaties

Dit type risico gebeurtenis uit het verleden aanmelden locaties overweegt (IP, breedtegraad / lengtegraad en ASN) toodetermine nieuwe / onbekende locaties. Hallo-systeem wordt informatie opgeslagen over de voorgaande locaties die worden gebruikt door een gebruiker en deze 'bekend' locaties overweegt. Hallo risicogebeurtenis wordt geactiveerd wanneer er optreedt Hallo zich aanmelden vanaf een locatie die nog niet in Hallo lijst met vertrouwde sites. Hallo systeem heeft een initiële learning periode van 30 dagen, waarover biedt het geen nieuwe locaties als onbekende locaties vlag. Hallo-systeem ook negeren aanmeldingen vanaf bekende apparaten en geografische locaties sluit tooa vertrouwde locatie. 

### <a name="sign-ins-from-infected-devices"></a>Aanmeldingen vanaf geïnfecteerde apparaten

Dit type risico gebeurtenis identificeert aanmeldingen vanaf apparaten geïnfecteerd met malware die bekend zijn tooactively communiceren met een bot-server. Dit wordt bepaald door de IP-adressen van Hallo gebruikersapparaat op basis van IP-adressen die verbonden met een bot-server zijn. 

### <a name="sign-ins-from-ip-addresses-with-suspicious-activity"></a>Aanmeldingen van IP-adressen met verdachte activiteit
Dit type risico gebeurtenis identificeert IP-adressen waaruit een groot aantal mislukte aanmeldingspogingen zijn gezien, bij verschillende gebruikersaccounts gedurende een korte periode. Dit komt overeen met verkeerspatronen van IP-adressen die door aanvallers worden gebruikt en een sterke indicator die accounts ofwel al of zijn over toobe aangetast. Dit is een machine learning-algoritme dat wordt genegeerd voor de hand liggende '*false positieven*', zoals IP-adressen die regelmatig worden gebruikt door andere gebruikers in de organisatie Hallo.  Hallo systeem heeft een initiële learning periode van 14 dagen waar deze leert Hallo aanmelden gedrag van een nieuwe gebruiker en de nieuwe tenant.


## <a name="detection-type"></a>Detectie van type

Hallo detectie type-eigenschap is een indicator (realtime of Offline) voor Hallo detectie periode van een risicogebeurtenis.  
Op dit moment is de meeste risicogebeurtenissen worden gedetecteerd offline in na verwerking bewerking als Hallo risicogebeurtenis is opgetreden.

Hallo volgende tabel geeft een lijst van Hallo hoeveelheid tijd die nodig is voor een type detectie tooshow up in een gerelateerde rapport:

| Detectie van Type | Reporting latentie |
| --- | --- |
| Realtime | too10 5 minuten |
| Off line | too4 2 uur |


Voor hello Azure Active Directory detecteert risico gebeurtenistypen, zijn Hallo detectie typen:

| Gebeurtenistype risico | Detectie van Type |
| :-- | --- | 
| [Gebruikers met gelekte referenties](#leaked-credentials) | Off line |
| [Aanmeldingen vanaf anonieme IP-adressen](#sign-ins-from-anonymous-ip-addresses) | Realtime |
| [Onmogelijke reis tooatypical locaties](#impossible-travel-to-atypical-locations) | Off line |
| [Aanmeldingen vanaf onbekende locaties](#sign-in-from-unfamiliar-locations) | Realtime |
| [Aanmeldingen vanaf geïnfecteerde apparaten](#sign-ins-from-infected-devices) | Off line |
| [Aanmeldingen vanaf IP-adressen met verdachte activiteiten](#sign-ins-from-ip-addresses-with-suspicious-activity) | Off line|


## <a name="risk-level"></a>Risiconiveau

Hallo risico niveau eigenschap van een risicogebeurtenis is een indicator voor Hallo ernst en Hallo betrouwbaarheidsinterval van een risicogebeurtenis (hoog, Gemiddeld of laag). Deze eigenschap kunt u tooprioritize Hallo acties die u moet uitvoeren. 

Hallo ernst van Hallo risicogebeurtenis vertegenwoordigt Hallo sterkte van Hallo signaal identiteit inbreuk te voorspellen.  
Hallo vertrouwen is een indicator Hallo mogelijkheid valse positieven. 

Bijvoorbeeld: 

* **Hoge**: hoge betrouwbaarheid en hoge urgentie risicogebeurtenis. Deze gebeurtenissen zijn sterk indicatoren dat Hallo gebruikersidentiteit er inbreuk is gemaakt en alle gebruikersaccounts die van invloed op onmiddellijk moeten worden hersteld.

* **Gemiddeld**: hoog dreigingsniveau, maar lagere vertrouwen risicogebeurtenis, of vice versa. Deze gebeurtenissen zijn mogelijk schadelijke en van invloed op gebruikersaccounts moeten worden hersteld.

* **Lage**: lage vertrouwen en laag dreigingsniveau risicogebeurtenis. Deze gebeurtenis kan niet een directe actie is vereist, maar in combinatie met andere risicogebeurtenissen kan bieden een sterke indicatie dat Hallo identiteit is geknoeid.

![Risiconiveau](./media/active-directory-reporting-risk-events/01.png)

### <a name="leaked-credentials"></a>Gelekte aanmeldingsreferenties

Gelekte referenties risicogebeurtenissen die zijn geclassificeerd als een **hoge**, omdat ze een duidelijke aanwijzing bieden dat Hallo-gebruikersnaam en wachtwoord beschikbaar tooan aanvaller zijn.

### <a name="sign-ins-from-anonymous-ip-addresses"></a>Aanmeldingen vanaf anonieme IP-adressen

Hallo risiconiveau voor dit type risico gebeurtenis is **gemiddeld** omdat een anoniem IP-adres niet een sterke indicatie van inbreuk op een account is.  
Het is raadzaam dat u direct contact op met Hallo gebruiker tooverify als ze anonieme IP-adressen gebruikten.


### <a name="impossible-travel-tooatypical-locations"></a>Onmogelijke reis tooatypical locaties

Onmogelijke reis is meestal een goede indicatie dat een hacker toosuccessfully kunnen aanmelden is. ONWAAR-positieven kunnen echter optreden wanneer een gebruiker op reis gaat met behulp van een nieuw apparaat of via een VPN die doorgaans niet wordt gebruikt door andere gebruikers in de organisatie Hallo. Een andere bron van false positieven is voor toepassingen die onjuist server IP-adressen als client-IP-adressen, zodat Hallo vormgeving van aanmeldingen die hebben plaatsgevonden van Hallo Datacenter waar de toepassing van back-end wordt gehost (vaak deze zijn Microsoft-datacenters waarmee Hallo vormgeving van aanmeldingen plaatsvinden van Microsoft die eigendom zijn van IP-adressen). Als gevolg van deze false positieven Hallo risiconiveau voor deze risicogebeurtenis is **gemiddeld**.

> [!TIP]
> U kunt Hallo hoeveelheid gemelde false positves voor dit type risico gebeurtenis verlagen door configureren [locaties met de naam](active-directory-named-locations.md). 

### <a name="sign-in-from-unfamiliar-locations"></a>Aanmelden vanaf onbekende locaties

Onbekende locaties kunnen bieden een sterke aanwijzing dat een aanvaller kan toouse de identiteit van een gestolen is. ONWAAR-positieven kunnen optreden wanneer een gebruiker op reis gaat, wordt geprobeerd om een nieuw apparaat of met behulp van een nieuwe VPN. Als gevolg van deze fout-positieven Hallo risiconiveau voor dit gebeurtenistype is **gemiddeld**.

### <a name="sign-ins-from-infected-devices"></a>Aanmeldingen vanaf geïnfecteerde apparaten

Deze risicogebeurtenis identificeert IP-adressen, niet de apparaten van gebruikers. Als meerdere apparaten zich achter een enkel IP-adres en alleen bepaalde worden beheerd door een bot-netwerk, aanmeldingen vanaf andere apparaten mijn trigger deze gebeurtenis onnodig, namelijk Hallo reden voor het classificeren van deze risicogebeurtenis als **laag**.  

U wordt aangeraden dat u contact op met de gebruiker Hallo en scannen van alle Hallo apparaten van gebruikers. Het is ook mogelijk dat een gebruiker persoonlijk apparaat is geïnfecteerd of zoals eerder gezegd dat iemand anders is met behulp van een geïnfecteerde-apparaat bij Hallo dezelfde IP-adres als de gebruiker Hallo. Geïnfecteerde apparaten zijn vaak geïnfecteerd met malware die nog niet is geïdentificeerd door de antivirussoftware, en kan ook duiden op als ongeldige gebruikers gewoontes op die kunnen worden gelegd Hallo apparaat toobecome geïnfecteerd.

Voor meer informatie over het tooaddress malware-infecties, Zie Hallo [Malware Protection Center](http://go.microsoft.com/fwlink/?linkid=335773&clcid=0x409).


### <a name="sign-ins-from-ip-addresses-with-suspicious-activity"></a>Aanmeldingen van IP-adressen met verdachte activiteit

Het is raadzaam dat u Hallo gebruiker tooverify contact opnemen met als ze daadwerkelijk aangemeld vanaf een IP-adres dat is gemarkeerd als verdacht. Hallo risiconiveau voor dit gebeurtenistype is '**gemiddeld**' omdat meerdere apparaten mogelijk achter Hallo hetzelfde IP-adres, bij slechts enkele is verantwoordelijk voor het Hallo verdachte activiteiten mogelijk niet. 


 
## <a name="next-steps"></a>Volgende stappen

Risico's vormen Hallo basis voor het beveiligen van uw Azure AD-identiteiten. Azure AD kan momenteel zes risicogebeurtenissen detecteren: 


| Gebeurtenistype risico | Risiconiveau | Detectie van Type |
| :-- | --- | --- |
| [Gebruikers met gelekte referenties](#leaked-credentials) | Hoog | Off line |
| [Aanmeldingen vanaf anonieme IP-adressen](#sign-ins-from-anonymous-ip-addresses) | Middelgroot | Realtime |
| [Onmogelijke reis tooatypical locaties](#impossible-travel-to-atypical-locations) | Middelgroot | Off line |
| [Aanmeldingen vanaf onbekende locaties](#sign-in-from-unfamiliar-locations) | Middelgroot | Realtime |
| [Aanmeldingen vanaf geïnfecteerde apparaten](#sign-ins-from-infected-devices) | Laag | Off line |
| [Aanmeldingen vanaf IP-adressen met verdachte activiteiten](#sign-ins-from-ip-addresses-with-suspicious-activity) | Middelgroot | Off line|

Waar vind u Hallo risico's die zijn gedetecteerd in uw omgeving?
Er zijn twee plaatsen waar u gerapporteerde risicogebeurtenissen bekijken:

 - **Rapportage van Azure AD** -Risicogebeurtenissen die deel uitmaken van Azure AD-beveiligingsgroep rapporten. Zie voor meer informatie, Hallo [gebruikers op risico beveiligingsrapport](active-directory-reporting-security-user-at-risk.md) en Hallo [riskant aanmeldingen beveiligingsrapport](active-directory-reporting-security-risky-sign-ins.md).

 - **Azure AD Identity Protection** -risico's zijn ook deel uit van [Azure Active Directory: Identity Protection van](active-directory-identityprotection.md) rapportagemogelijkheden.
    

Tijdens het Hallo detectie van risico's al vertegenwoordigt een belangrijk aspect van het beveiligen van identiteiten, hebt u ook Hallo optie tooeither deze handmatig oplossen of zelfs automatische antwoorden implementeren door het beleid voor voorwaardelijke toegang configureren. Zie voor meer informatie van [Azure Active Directory: Identity Protection van](active-directory-identityprotection.md).
 
