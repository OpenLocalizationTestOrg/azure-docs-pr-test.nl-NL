---
title: 'aaaAzure Active Directory: Identity Protection playbook | Microsoft Docs'
description: Meer informatie over hoe Azure AD Identity Protection kunt u toolimit Hallo mogelijkheid van een aanvaller tooexploit de identiteit van een verdachte of apparaat en toosecure een identiteit of een apparaat dat eerder verdachte of bekende toobe aangetast.
services: active-directory
keywords: beveiliging in Azure active directory-identiteit, cloud app discovery, het beheren van toepassingen, beveiliging, risico, risiconiveau, beveiligingsprobleem, beveiligingsbeleid
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 60836abf-f0e9-459d-b344-8e06b8341d25
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 6252bc133fc0c0f84800ee245a04bbf62d4cd25b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection-playbook"></a>Playbook voor Azure Active Directory: Identity Protection
Deze playbook helpt u bij:

* Gegevens in Hallo Identity Protection omgeving door simulating risicogebeurtenissen en beveiligingsproblemen vullen
* Instellen van beleidsregels voor voorwaardelijke toegang op basis van risico's en Hallo gevolgen van het beleid testen

## <a name="simulating-risk-events"></a>Risico's te simuleren
Deze sectie bevat met de stappen voor het simuleren Hallo gebeurtenistypen risico's te volgen:

* Aanmeldingen vanaf anonieme IP-adressen (eenvoudig)
* Aanmeldingen vanaf onbekende locaties (gemiddeld)
* Onmogelijke reis tooatypical locaties (moeilijk)

Andere risicogebeurtenissen kunnen niet op een veilige manier worden gesimuleerd.

### <a name="sign-ins-from-anonymous-ip-addresses"></a>Aanmeldingen vanaf anonieme IP-adressen
Dit type risico gebeurtenis identificeert gebruikers die zich heeft aangemeld vanaf een IP-adres dat is geïdentificeerd als een anonieme proxy IP-adres. Deze proxy's worden gebruikt door mensen willen toohide van hun apparaat IP-adres en kan worden gebruikt voor kwade bedoelingen.

**toosimulate een aanmeldingspagina van een anoniem IP uitvoeren Hallo stappen te volgen**:

1. Hallo downloaden [Tor Browser](https://www.torproject.org/projects/torbrowser.html.en).
2. Hallo Tor Browser, navigeer te[https://myapps.microsoft.com](https://myapps.microsoft.com).   
3. Geef referenties op Hallo van de gewenste tooappear in Hallo Hallo-account **aanmeldingen vanaf anonieme IP-adressen** rapport.

Hallo-aanmeldingspagina wordt weergegeven op Hallo Identity Protection-dashboard binnen 5 minuten. 

### <a name="sign-ins-from-unfamiliar-locations"></a>Aanmeldingen vanaf onbekende locaties
Hallo onbekende locaties risico is een realtime aanmelden evaluatiemechanisme dat uit het verleden aanmelden locaties overweegt (IP, breedtegraad / lengtegraad en ASN) toodetermine nieuwe / onbekende locaties. Hallo opgeslagen vorige IP-adressen, de breedtegraad / lengtegraad en ASN's van een gebruiker en deze vertrouwde locaties toobe wordt beschouwd. Een locatie aanmelden wordt beschouwd als niet bekend als hello aanmelden locatie komt niet overeen met een van de bestaande vertrouwde locaties Hallo.

Beveiliging van Azure Active Directory-identiteit:  

* heeft een initiële learning periode van 14 dagen aan waarover biedt het geen nieuwe locaties als onbekende locaties vlag.
* aanmeldingen vanaf bekende apparaten en de locaties die geografisch sluiten tooan bestaande vertrouwde locatie worden genegeerd.

Onbekende locaties toosimulate, hebt u toosign vanaf een locatie en het apparaat dat Hallo-account is niet aangemeld uit voordat in. 

**toosimulate een aanmelden vanaf een onbekend locatie uitvoeren Hallo stappen te volgen**:

1. Kies een account met ten minste een geschiedenis van de aanmeldingspagina 14 dagen. 
2. Doen:
   
   a. Tijdens het gebruik van een VPN te navigeren[https://myapps.microsoft.com](https://myapps.microsoft.com) en geef referenties op Hallo van de gewenste toosimulate Hallo risicogebeurtenis voor Hallo-account.
   
   b. Vraag een koppelen in een andere locatie toosign aan met referenties van Hallo-account (niet aanbevolen).

Hallo-aanmeldingspagina wordt weergegeven op Hallo Identity Protection-dashboard binnen 5 minuten.

### <a name="impossible-travel-tooatypical-location"></a>Onmogelijke reis tooatypical locatie
Hallo onmogelijke reis voorwaarde simuleren is moeilijk omdat Hallo-algoritme maakt gebruik van machine learning tooweed uit ONWAAR-positieven zoals onmogelijke reis vanaf vertrouwde apparaten of aanmeldingen van VPN-verbindingen die door andere gebruikers in de directory hello worden gebruikt. Hallo-algoritme worden een geschiedenis aanmelden van 3 dagen van de too14 moet voor Hallo gebruiker voordat u begint deze risico's te genereren.

**een locatie van de tooatypical onmogelijke reis toosimulate uitvoeren Hallo stappen te volgen**:

1. Met behulp van de standaardbrowser te navigeren[https://myapps.microsoft.com](https://myapps.microsoft.com).  
2. Geef referenties op Hallo van Hallo account toogenerate een gebeurtenis onmogelijke reis risico voor.
3. Uw gebruikersagent wijzigen. U kunt gebruikersagent in Internet Explorer van hulpprogramma's voor ontwikkelaars wijzigen of uw gebruikersagent in Firefox of Chrome met de invoegtoepassing van een gebruikersagent schakelbaar wijzigen.
4. Wijzig het IP-adres. U kunt uw IP-adres wijzigen met behulp van een VPN, een invoegtoepassing Tor, of van een nieuwe machine in Azure in een ander datacenter draait.
5. Meld u aan te[https://myapps.microsoft.com](https://myapps.microsoft.com) met behulp van dezelfde referenties als voordat en binnen een paar minuten nadat de vorige aanmelden Hallo Hallo.

Hallo-aanmeldingspagina wordt weergegeven in Hallo Identity Protection-dashboard binnen 2-4 uur.<br>
Vanwege Hallo complexe machine learning-modellen die betrokken zijn, is er een kans dat deze wordt niet ophalen opgepikt.<br> Wilt u mogelijk tooreplicate deze stappen voor meerdere Azure AD-accounts.

## <a name="simulating-vulnerabilities"></a>Beveiligingsproblemen simuleren
Zwakke plekken zijn zwakke punten in een Azure AD-omgeving die door een onjuiste acteur kan worden misbruikt. Momenteel worden 3 typen zwakke plekken die opgehaald in Azure AD Identity Protection die gebruikmaken van andere functies van Azure AD. Deze beveiligingsproblemen op Hallo Identity Protection-dashboard automatisch weergegeven zodra deze functies zijn ingesteld.

* Azure AD [multi-factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)
* Azure AD [Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).
* Azure AD [Privileged Identity Management](active-directory-privileged-identity-management-configure.md). 

## <a name="user-compromise-risk"></a>Gebruiker risico op inbreuk
**tootest gebruiker risico op inbreuk, voeren Hallo stappen te volgen**:

1. Meld u aan te[https://portal.azure.com](https://portal.azure.com) met referenties van de globale beheerder voor uw tenant.
2. Navigeer te**Identity Protection**. 
3. Op de belangrijkste Hallo **Azure AD Identity Protection** blade, klikt u op **instellingen**. 
4. Op Hallo **instellingen voor de Gebruikersportal** blade onder **beveiligingsregels**, klikt u op **gebruiker inbreuk risico**. 
5. Op Hallo **aanmelden risico** blade inschakelen **inschakelen regel** uit en klik vervolgens op **opslaan** instellingen.
6. Voor een bepaald gebruikersaccount simuleren een onbekende locaties of anonieme IP-risicogebeurtenis. Dit wordt Hallo gebruiker risiconiveau voor die gebruiker te verhogen**gemiddeld**.
7. Wacht een paar minuten en controleer vervolgens dat gebruikersniveau voor de gebruiker is **gemiddeld**.
8. Ga toohello **instellingen voor de Gebruikersportal** blade.
9. Op Hallo **gebruiker inbreuk risico** blade onder **inschakelen regel**, selecteer **op** . 
10. Selecteer een Hallo volgende opties:
    
    a. tooblock, selecteer **gemiddeld** onder **blok aanmelden**.
    
    b. tooenforce beveiligd wachtwoord wijzigen, selecteert **gemiddeld** onder **meervoudige authenticatie**.
11. Klik op **Opslaan**.
12. U kunt nu voorwaardelijke toegang op basis van risico's wanneer u zich aanmeldt bij het gebruik van een gebruiker met een verhoogde risiconiveau testen. Hallo gebruiker risico gemiddeld, afhankelijk van de configuratie van de Hallo van uw beleid, de aanmeldingspagina is worden geblokkeerd of u toochange worden gedwongen uw wachtwoord. 
    <br><br>
    ![Playbook](./media/active-directory-identityprotection-playbook/201.png "Playbook")
    <br>

## <a name="sign-in-risk"></a>Aanmelden risico
**tootest een teken in gevaar, Voer Hallo stappen te volgen:**

1. Meld u aan te[https://portal.azure.com ](https://portal.azure.com) met referenties van de globale beheerder voor uw tenant.
2. Navigeer te**Identity Protection**.
3. Op de belangrijkste Hallo **Azure AD Identity Protection** blade, klikt u op **instellingen**. 
4. Op Hallo **instellingen voor de Gebruikersportal** blade onder **beveiligingsregels**, klikt u op **aanmelden risico**.
5. Op Hallo ** aanmelden risico ** blade Selecteer **op** onder **inschakelen regel**. 
6. Selecteer een Hallo volgende opties:
   
   a. tooblock, selecteer **gemiddeld** onder **blok aanmelden**
   
   b. tooenforce beveiligd wachtwoord wijzigen, selecteert **gemiddeld** onder **meervoudige authenticatie**.
7. tooblock, selecteer gemiddeld onder blok aanmelden.
8. tooenforce multi-factor authentication-server, selecteer **gemiddeld** onder **meervoudige authenticatie**.
9. Klik op **Opslaan**.
10. U kunt nu voorwaardelijke toegang op basis van risico testen door simuleren Hallo onbekende locaties of anoniem IP gebeurtenissen risico omdat ze beide **gemiddeld** bestaat de kans dat gebeurtenissen.


![Playbook](./media/active-directory-identityprotection-playbook/200.png "Playbook")


## <a name="see-also"></a>Zie ook
* [Azure Active Directory Identity Protection](active-directory-identityprotection.md)

