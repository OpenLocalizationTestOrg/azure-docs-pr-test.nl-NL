---
title: 'Snelstartgids: Azure AD-SSPR | Microsoft Docs'
description: Wachtwoorden snel opnieuw instellen voor Azure AD via self-service
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: bde8799f-0b42-446a-ad95-7ebb374c3bec
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 4fed3a1c690fd6423ee5d3e5baef690d8896fbe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-azure-ad-self-service-password-reset"></a>Snelstartgids: Azure AD-selfservice voor wachtwoordherstel

> [!IMPORTANT]
> **Bent u hier terechtgekomen omdat u problemen ondervindt met het aanmelden?** Als dat het geval is, vindt u hier meer informatie over het [wijzigen en opnieuw instellen van uw eigen wachtwoord](active-directory-passwords-update-your-own-password.md).

## <a name="rapidly-deploy-self-service-password-reset"></a>Wachtwoorden snel opnieuw instellen via self-service

Selfservice voor wachtwoordherstel (SSPR) biedt een eenvoudige methode voor IT-beheerders tooempower gebruikers tooreset of hun wachtwoorden of accounts ontgrendelen. Hallo system bevat gedetailleerde reporting tootrack wanneer gebruikers Hallo systeem samen met meldingen tooalert gebruiken u toomisuse of misbruik.

In deze handleiding wordt ervan uitgegaan dat u een werkende proefversie hebt van de Azure AD-tenant of dat u er een licentie voor hebt. Als u Azure AD in te stellen hulp nodig, raadpleegt u Hallo artikel [aan de slag met Azure AD](https://azure.microsoft.com/trial/get-started-active-directory/).

1. Selecteer in uw bestaande Azure AD-tenant de optie **Wachtwoord opnieuw instellen**

2. Van Hallo **'Eigenschappen'** scherm onder 'Self Service wachtwoord opnieuw instellen ingeschakeld' Kies een van de volgende Hallo Hallo-optie
    * Niemand - geen één is kunnen toouse SSPR-functionaliteit
    * Een groep - alleen leden van een specifieke Azure AD groep dat u kiest zijn kunnen toouse SSPR-functionaliteit
    * Iedereen - alle gebruikers met een account in uw Azure AD-tenant kunnen toouse SSPR-functionaliteit zijn

3. Van Hallo **'Verificatiemethoden'** scherm kiezen
    * Aantal methoden vereist tooreset - We ondersteuning voor een minimum van één of een maximum van twee
    * Methoden beschikbaar toousers - moet ten minste één, maar het kan nooit kwaad toohave een extra keuze beschikbaar
        * **E-mailadres** stuurt een e-mail met een code toohello gebruiker geconfigureerde e-mailadres voor authenticatie
        * **Mobiele telefoon** biedt Hallo gebruiker Hallo keuze tooreceive gebeld of tekst met een code-tootheir geconfigureerd mobiele telefoonnummer
        * **Telefoon (werk)** aanroepen Hallo gebruiker met een code-tootheir geconfigureerd telefoonnummer
        * **Beveiligingsvragen** toochoose, moet u
            * Aantal vragen dat vereist tooregister - Hallo minimum voor succesvolle registratie, wat betekent dat een gebruiker kan kiezen tooanswer meer toocreate een pool van vragen toopull uit. Deze optie moet kan worden ingesteld van 3-5 en niet groter zijn dan of gelijk aan het aantal vragen vereist tooreset toohello.
                * Aangepaste vragen kunnen worden toegevoegd door te klikken op de knop 'Aangepast' hello bij het selecteren van beveiligingsvragen
            * Aantal vragen dat vereist is tooreset - kan worden ingesteld van 3-5 vragen toobe juist beantwoorden alvorens toe te staan een gebruikers wachtwoord toobe opnieuw ingesteld of is ontgrendeld.

4. AANBEVOLEN: **'Aanpassing'** kunt u toochange Hallo 'Contact op met uw beheerder' koppeling toopoint tooa pagina of e-mailadres u definiëren

5. Optioneel: Hallo **"Registratie"** scherm biedt beheerders Hallo opties voor:
    * Gebruikers tooregister vereist als u zich aanmeldt
    * Aantal dagen voordat gebruikers worden gevraagd tooreconfirm hun verificatiegegevens

6. Optioneel: Hallo **'Meldingen'** scherm biedt beheerders Hallo opties:
    * Gebruikers een melding tonen over het opnieuw instellen van hun wachtwoord
    * Alle beheerders waarschuwen wanneer andere beheerders hun wachtwoord opnieuw instellen

**U hebt op dit moment SSPR geconfigureerd voor uw Azure AD-tenant**. U kunt hier stoppen of verder tooconfigure synchronisatie van wachtwoorden tooan lokale AD-domein.

> [!NOTE]
> Test self-service voor wachtwoordherstel met een gebruiker en niet als beheerder, aangezien Microsoft sterke verificatievereisten afdwingt voor Azure-accounts van beheerders. Zie voor meer informatie over Hallo beheerder wachtwoordbeleid onze [wachtwoord beleid artikel](active-directory-passwords-policy.md#administrator-password-policy-differences).

## <a name="configure-synchronization-tooexisting-identity-source"></a>De identiteit van de synchronisatiebron tooexisting configureren

tooenable lokaal identiteit synchronisatie tooAzure AD, u moet tooinstall en configureert [Azure AD Connect](./connect/active-directory-aadconnect.md) op een server in uw organisatie. Deze toepassing verwerkt het synchroniseren van gebruikers en groepen van uw bestaande identiteit bron tooyour Azure AD-tenant.

* [Upgrade van DirSync of Azure AD Sync tooAzure AD Connect](./connect/active-directory-aadconnect-dirsync-deprecated.md)
* [Aan de slag met Azure AD Connect met Express-instellingen](./connect/active-directory-aadconnect-get-started-express.md)
* [Wachtwoord terugschrijven configureren](active-directory-passwords-writeback.md#configuring-password-writeback) toowrite wachtwoorden van Azure AD back tooyour on-premises adreslijst.

## <a name="disabling-self-service-password-reset"></a>Selfservice voor wachtwoordherstel uitschakelen

Het uitschakelen van de selfservice voor wachtwoordherstel is net zo eenvoudig als uw Azure AD-tenant openen en te gaan**wachtwoordherstel > eigenschappen** > Kies **geen** onder **wachtwoord opnieuw instellen in selfservice Ingeschakeld**

### <a name="learn-more"></a>Meer informatie
Hallo volgende koppelingen vindt u aanvullende informatie met betrekking tot het wachtwoord opnieuw instellen met behulp van Azure AD

* [**Licentieverlening**](active-directory-passwords-licensing.md): uw Azure AD-licentieverlening configureren
* [**Gegevens** ](active-directory-passwords-data.md) - begrijpen Hallo-gegevens die nodig is en hoe deze wordt gebruikt voor wachtwoordbeheer
* [**Implementatie** ](active-directory-passwords-best-practices.md) -plannen en implementeren van SSPR tooyour gebruikers via Hallo richtlijnen hier gevonden
* [**Aanpassen** ](active-directory-passwords-customize.md) -Hallo uiterlijk Hallo SSPR ervaring voor uw bedrijf aanpassen.
* [**Beleid**](active-directory-passwords-policy.md): Azure AD-wachtwoordbeleid begrijpen en instellen
* [**Rapportage**](active-directory-passwords-reporting.md): detecteren of, waar en wanneer uw gebruikers de functionaliteit voor self-service voor wachtwoordherstel gebruiken
* [**Technische diepgaand** ](active-directory-passwords-how-it-works.md) -Ga achter Hallo gordijn toounderstand hoe het werkt
* [**Veelgestelde vragen**](active-directory-passwords-faq.md): hoe? Hoe komt dat? Wat? Waar? Wie? Wanneer? -Beantwoordt tooquestions gewenste altijd tooask
* [**Problemen met** ](active-directory-passwords-troubleshoot.md) -informatie over hoe tooresolve algemene problemen zien we met SSPR

## <a name="next-steps"></a>Volgende stappen

In deze snelstartgids hebt u geleerd hoe tooconfigure selfservice voor wachtwoordherstel voor uw gebruikers. toocontinue toohello Azure portal toocomplete Volg deze stappen Hallo-koppeling hieronder toohello-portal.

> [!div class="nextstepaction"]
> [Selfservice voor wachtwoordherstel inschakelen](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/PasswordReset)

