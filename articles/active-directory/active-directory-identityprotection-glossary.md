---
title: 'Active Directory: Identity Protection verklarende woordenlijst aaaAzure | Microsoft Docs'
description: Verklarende woordenlijst voor beveiliging van Azure Active Directory-identiteit
services: active-directory
keywords: beveiliging in Azure active directory-identiteit, cloud app discovery, het beheren van toepassingen, beveiliging, risico, risiconiveau, beveiligingsprobleem, beveiligingsbeleid, verklarende woordenlijst
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 833119a5-33d6-4482-adda-fa35218c72c3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: ff2e96d20e2a3f1df24b78e66be5a0c6807e60a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection-glossary"></a>Verklarende woordenlijst voor beveiliging van Azure Active Directory-identiteit
### <a name="at-risk-user"></a>Risico (gebruiker)
Een gebruiker met een of meer actieve risico's. 

### <a name="atypical-sign-in-location"></a>Ongewone aanmelding locatie
Een aanmelden vanaf een geografische locatie die niet standaard voor specifieke gebruiker hello, vergelijkbare gebruikers of Hallo tenant.

### <a name="azure-ad-identity-protection"></a>Azure AD-identiteitsbeveiliging
Een beveiligingsmodule van Azure Active Directory waarmee een geconsolideerde weergave risicogebeurtenissen en mogelijke beveiligingsproblemen die invloed hebben op de identiteiten van een organisatie.

### <a name="conditional-access"></a>Voorwaardelijke toegang
Een beleid voor het beveiligen van toegang tooresources. Regels voor voorwaardelijke toegang in hello Azure Active Directory worden opgeslagen en worden geëvalueerd door Azure AD voordat u verleent toegang toohello resource.  Voorbeeld van de regels omvatten beperken van toegang op basis van de locatie van de gebruiker, apparaat status of de gebruiker de verificatiemethode.

### <a name="credentials"></a>Referenties
Gegevens over de identificatie en bewijs van-id die is gebruikt toogain toegang toolocal- en netwerkbronnen bevat. Voorbeelden van referenties zijn gebruikersnamen en wachtwoorden, smartcards en certificaten.

### <a name="event"></a>Gebeurtenis
Een record van een activiteit in Azure Active Directory.

### <a name="false-positive-risk-event"></a>Fout-positieve (risicogebeurtenis)
Een risico gebeurtenisstatus handmatig instellen door een gebruiker Identity Protection, waarmee wordt aangegeven dat risico Hallo gebeurtenis is onderzocht en is foutief gemarkeerd als een risicogebeurtenis.

### <a name="identity"></a>Identiteit
Een persoon of entiteit die moet worden gecontroleerd met behulp van verificatie op basis van criteria zoals wachtwoord of een certificaat.

### <a name="identity-risk-event"></a>Identiteit risicogebeurtenis
AAD-gebeurtenis die is gemarkeerd als afwijkend door Identity Protection, en kan wijzen op een identiteit is aangetast.

### <a name="ignored-risk-event"></a>Genegeerd (risicogebeurtenis)
Een risico gebeurtenisstatus handmatig instellen door een gebruiker Identity Protection, waarmee wordt aangegeven dat risico Hallo gebeurtenis zonder een herstelactie is gesloten.

### <a name="impossible-travel-from-atypical-locations"></a>Onmogelijke reis van ongewone locaties
Een risicogebeurtenis geactiveerd wanneer er twee aanmeldingen Hallo dezelfde gebruiker worden gedetecteerd, waarbij ten minste één van deze afkomstig is van een ongebruikelijk locatie aanmelden en waarbij Hallo tijd tussen Hallo aanmeldingen is korter dan Hallo minimale tijd kost toophysically worden uitgewisseld tussen deze locaties.  

### <a name="investigation"></a>Onderzoek
Hallo proces controleren Hallo activiteiten, logboeken en andere relevante informatie gerelateerde tooa risico gebeurtenis toodecide of herstel of afname stappen zijn vereist, begrijpen hoe Hallo of en hoe het Hallo-identiteit is geknoeid en begrijpen identiteit waarmee is geknoeid is gebruikt.

### <a name="leaked-credentials"></a>Gelekte aanmeldingsreferenties
Een risicogebeurtenis geactiveerd wanneer de huidige gebruikersreferenties (gebruikersnaam en wachtwoord) zijn gevonden in Hallo donker web door onze onderzoekers openbaar geboekt.

### <a name="mitigation"></a>Oplossing
Een actie toolimit of Hallo mogelijkheid van een aanvaller tooexploit een waarmee is geknoeid identiteit of het apparaat zonder herstelstatus Hallo identiteit of het apparaat tooa veilige elimineren. Een risicobeperking vorige risico's die zijn gekoppeld aan het Hallo-identiteit of het apparaat niet is opgelost.

### <a name="multi-factor-authentication"></a>Multi-Factor Authentication
Een verificatiemethode waarbij twee of meer verificatiemethoden, waaronder mogelijk iets Hallo gebruiker heeft, zoals een certificaat; iets Hallo gebruiker, zoals gebruikersnamen, wachtwoorden of wachtwoordzinnen weet; fysieke kenmerken, zoals een vingerafdruk; en persoonlijke kenmerken, zoals een persoonlijke handtekening.

### <a name="offline-detection"></a>Offline-detectie
Hallo-detectie van afwijkingen en evaluatie van Hallo risico van een gebeurtenis, zoals aanmeldingspoging na Hallo feit, voor een gebeurtenis die al is gebeurd.

### <a name="policy-condition"></a>Beleidsvoorwaarde
Een deel van een beveiligingsbeleid dat Hallo entiteiten (groepen, gebruikers, apps, apparaatplatforms, de statussen van apparaten, IP-adresbereiken, clienttypen) in het beleid voor Hallo opgenomen of uitgesloten van deze definieert.

### <a name="policy-rule"></a>Beleidsregel
Hallo-onderdeel van een beveiligingsbeleid dat wordt beschreven Hallo omstandigheden die activeren zou Hallo beleid en Hallo-acties uitgevoerd wanneer het Hallo-beleid wordt geactiveerd.

### <a name="prevention"></a>Preventie
Een actie tooprevent schade toohello organisatie via misbruik van een identiteit of het apparaat wordt vermoed of toobe geknoeid weten. Een actie preventie Hallo-apparaat of identiteit niet wordt beveiligd en vorige risicogebeurtenissen kan niet worden omgezet.

### <a name="privileged-user"></a>Bevoegdheden (gebruiker)
Een gebruiker die gelijktijdig Hallo van een risicogebeurtenis op permanente als tijdelijke beheerder machtigingen tooone of meer resources in Azure Active Directory, zoals een globale beheerder had financieel medewerker, servicebeheerder, beheerder van de gebruiker en wachtwoord Beheerder. 

### <a name="real-time"></a>Realtime
Zie realtime detectie.

### <a name="real-time-detection"></a>Realtime-detectie
Hallo-detectie van afwijkingen en evaluatie van Hallo risico van een gebeurtenis, zoals aanmeldingspoging voordat Hallo gebeurtenis tooproceed is toegestaan.

### <a name="remediated-risk-event"></a>Hersteld (risicogebeurtenis)
De status van een risico gebeurtenis is automatisch ingesteld door Identity Protection, waarmee wordt aangegeven dat risico Hallo gebeurtenis hersteld met behulp van de standaard herstelactie Hallo voor dit type risicogebeurtenis. Bijvoorbeeld, wanneer het gebruikerswachtwoord Hallo opnieuw wordt ingesteld, worden veel risicogebeurtenissen die aangeven dat Hallo vorige wachtwoord is aangetast automatisch hersteld.

### <a name="remediation"></a>Herstel
Een actie toosecure een identiteit of een apparaat die eerder zijn verdachte of bekend toobe geschonden. Een herstelactie Hallo identiteit of het apparaat tooa veilige status herstelt en vorige risico's die zijn gekoppeld aan het Hallo-identiteit of het apparaat wordt omgezet.

### <a name="resolved-risk-event"></a>Opgelost (risicogebeurtenis)
De gebeurtenisstatus van een risico handmatig instellen door een gebruiker Identity Protection, waarmee wordt aangegeven dat Hallo gebruiker een juiste herstelactie buiten Identity Protection heeft en die risico Hallo gebeurtenis moet worden beschouwd gesloten.

### <a name="risk-event-status"></a>De gebeurtenisstatus risico
Een eigenschap van een risicogebeurtenis, die aangeeft of Hallo gebeurtenis actief is, en als gesloten, Hallo reden voor het afsluiten van het.

### <a name="risk-event-type"></a>Gebeurtenistype risico
Een categorie voor Hallo risico gebeurtenis, die aangeeft dat Hallo type afwijkingsdetectie waardoor Hallo gebeurtenis toobe beschouwd als riskant.

### <a name="risk-level-risk-event"></a>Risiconiveau (risicogebeurtenis)
Een indicatie van de ernst Hallo Hallo risico gebeurtenis toohelp Identity Protection gebruikers (hoog, Gemiddeld of laag) prioriteren Hallo-acties die ze tooreduce Hallo risico tootheir organisatie uitvoeren. 

### <a name="risk-level-sign-in"></a>Risiconiveau (sign-in)
Een aanduiding (hoog, Gemiddeld of laag) van Hallo kans dat voor een specifieke aanmelden, iemand anders toouse Hallo gebruikers-id probeert.

### <a name="risk-level-user-compromise"></a>Risiconiveau (gebruiker inbreuk)
Een aanduiding (hoog, Gemiddeld of laag) van Hallo kans dat een identiteit is aangetast.

### <a name="risk-level-vulnerability"></a>Risiconiveau (beveiligingsprobleem)
Een indicatie van de ernst Hallo Hallo beveiligingslek toohelp Identity Protection gebruikers (hoog, Gemiddeld of laag) prioriteren Hallo-acties die ze tooreduce Hallo risico tootheir organisatie uitvoeren.

### <a name="secure-identity"></a>Secure (identiteit)
Nemen herstelactie zoals een wachtwoord wijzigen of de machine toorestore een eventueel verdachte identiteit tooan ongeschonden status wordt teruggezet.

### <a name="security-policy"></a>Beveiligingsbeleid
Een verzameling van regels en de voorwaarde. Een beleid kan worden toegepast tooentities zoals gebruikers, groepen, apps, apparaten, apparaatplatforms, de statussen van apparaten, IP-adresbereiken en Auth2.0 clienttypen. Wanneer een beleid is ingeschakeld, wordt dit geëvalueerd wanneer een token voor een bron is uitgegeven door een entiteit die is opgenomen in Hallo-beleid.

### <a name="sign-in-v"></a>Meld u aan (v)
tooauthenticate tooan identiteit in Azure Active Directory.

### <a name="sign-in-n"></a>Aanmelden (n)
Hallo-proces of actie van een identiteit in Azure Active Directory en Hallo-gebeurtenis die deze bewerking legt vast te verifiëren.

### <a name="sign-in-from-anonymous-ip-address"></a>Aanmelden vanaf anonieme IP-adres
Een risicogebeurtenis geactiveerd na een geslaagde aanmelden van IP-adres dat is geïdentificeerd als een anonieme proxy IP-adres.

### <a name="sign-in-from-infected-device"></a>Aanmelden van geïnfecteerde apparaten
Een risicogebeurtenis geactiveerd wanneer een aanmeldingspagina afkomstig is van een IP-adres waarvan bekend toobe gebruikt door een of meer aangetaste apparaten die toocommunicate met een bot-server actief tracht is.

### <a name="sign-in-from-ip-address-with-suspicious-activity"></a>Aanmelden van IP-adres met verdachte activiteiten
Een risicogebeurtenis wordt geactiveerd nadat een geslaagde aanmelden van een-IP-adres met een groot aantal mislukte aanmeldingspogingen bij verschillende gebruikersaccounts gedurende een korte periode.

### <a name="sign-in-from-unfamiliar-location"></a>Aanmelden van onbekende locatie
Een risicogebeurtenis geactiveerd wanneer een gebruiker zich met succes aanmeldt vanaf een nieuwe locatie (IP-breedtegraad/lengtegraad en ASN).

### <a name="sign-in-risk"></a>Aanmelden risico
Zie risico niveau (sign-in)

### <a name="sign-in-risk-policy"></a>Beleid voor aanmelden risico
Een beleid voor voorwaardelijke toegang dat Hallo risico tooa specifieke aanmelden wordt geëvalueerd en oplossingen op basis van vooraf gedefinieerde voorwaarden en regels van toepassing is.

### <a name="user-compromise-risk"></a>Gebruiker risico op inbreuk
Zie risico niveau (gebruiker inbreuk)

### <a name="user-risk"></a>Gebruiker risico
Zie risico niveau (gebruiker inbreuk).

### <a name="user-risk-policy"></a>Gebruikersbeleid risico
Een beleid voor voorwaardelijke toegang die overweegt Hallo aanmelden en oplossingen op basis van vooraf gedefinieerde voorwaarden en bepalingen toepast.

### <a name="users-flagged-for-risk"></a>Gebruikers voor wie wordt aangegeven dat ze risico lopen
Gebruikers die risicogebeurtenissen zijn die actief of herstelde hebben

### <a name="vulnerability"></a>Beveiligingslek
Een configuratie of een voorwaarde in Azure Active Directory, waardoor Hallo directory vatbaar tooexploits of bedreigingen.

## <a name="see-also"></a>Zie ook
* [Azure Active Directory Identity Protection](active-directory-identityprotection.md)

