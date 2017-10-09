---
title: 'Azure AD: SSPR-registratie | Microsoft Docs'
description: Registreren verificatiegegevens voor self-service Azure AD-wachtwoord opnieuw instellen
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: joflore
ms.custom: end-user
ms.openlocfilehash: dfcd0106616218c84d23920b124bed5b202cdd6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="register-for-self-service-password-reset"></a>Registreren voor de selfservice voor het opnieuw instellen van een wachtwoord

> [!IMPORTANT]
> **Bent u hier terechtgekomen omdat u problemen ondervindt met het aanmelden?** Als dat het geval is, vindt u hier meer informatie over het [wijzigen en opnieuw instellen van uw eigen wachtwoord](active-directory-passwords-update-your-own-password.md).

U kunt uw wachtwoord opnieuw instellen of uw account ontgrendelen zonder toospeak tooa persoon met behulp van de selfservice voor wachtwoordherstel (SSPR) als een eindgebruiker. Voordat u deze functionaliteit gebruiken kunt, moet u tooregister verificatiemethoden hebben of bevestigen Hallo vooraf gedefinieerde verificatiemethoden uw beheerder heeft ingevuld.

## <a name="register-or-confirm-authentication-data-with-sspr"></a>Verificatiegegevens registreren of bevestigen met SSPR

1. Open Hallo webbrowser op uw apparaat en Ga naar toohello [registratiepagina voor wachtwoordherstel](http://aka.ms/ssprsetup)
2. Voer uw gebruikersnaam en wachtwoord in die door uw beheerder zijn verstrekt
3. Afhankelijk van hoe uw IT-medewerkers hebt geconfigureerd dingen, een of meer van de volgende Hallo opties zijn beschikbaar voor u tooconfigure en controleren. De beheerder kan vult sommige van deze voor u als ze over uw machtiging toouse Hallo informatie beschikt.
    * Telefoon (werk) is alleen kunnen toobe ingesteld door uw beheerder
    * Telefoon voor authenticatie moet worden ingesteld als tooanother telefoonnummer hebt u toegang toolike een mobiele telefoon die een tekstbericht of telefoongesprek kunnen ontvangen.
    * Verificatie-e-mailbericht moet worden ingesteld op tooan alternatieve e-mailadres dat u toegang hebt tot zonder Hallo wachtwoord moet u tooreset.
    * Beveiligingsvragen biedt u een lijst met uw beheerder heeft goedgekeurd voor u tooanswer vragen. U kunt geen Hallo dezelfde meer dan één keer te beantwoorden of vraag.
4. Geef en controleer Hallo informatie vereist door uw beheerder. Als meer dan één optie beschikbaar is, het is raadzaam dat u meerdere methoden tooprovide flexibiliteit registreren wanneer een andere methode niet beschikbaar is (voorbeeld: tooaccess onderweg en niet kan uw telefoon (werk))

    ![Registreer verificatiemethoden en klik op Voltooien][Register]

5. Wanneer u klaar bent met stap 4 kiezen **voltooien** en kunt u nu kunnen toouse selfservice wachtwoordherstel wanneer u tooin hello later nodig.

Als u gegevens in Hallo telefoon voor authenticatie of e-verificatie invoert, is het niet zichtbaar in de globale Hallo-map. Hallo alleen mensen die deze gegevens kunnen zien kunnen u en uw beheerders. Alleen u ziet Hallo tooyour beveiligingsvragen beantwoord.

Beheerders kunnen vereisen dat u tooconfirm uw verificatiemethoden na een bepaalde tijd toomake hebt u nog steeds Hallo geschikte methoden die worden geregistreerd.

## <a name="common-problems-and-their-solutions"></a>Veelvoorkomende problemen en oplossingen

 Hier volgen enkele veelvoorkomende foutgevallen en hun oplossingen:

| Foutaanvraag| Welke fout ziet u?| Oplossing |
| --- | --- | --- |
| Een pagina 'Neem contact op met uw beheerder' verschijnt na het invoeren van mijn gebruikers-ID | Neem contact op met uw beheerder <br> <br> We hebben vastgesteld dat het wachtwoord voor uw gebruikersaccount niet wordt beheerd door Microsoft. Als gevolg hiervan kan niet worden tooautomatically uw wachtwoord opnieuw instellen. <br> <br> U moet uw IT-personeel toocontact voor verdere assistentie. | U ziet dit bericht omdat uw IT-personeel beheert uw wachtwoord in uw on-premises omgeving en u geen tooreset kunt het wachtwoord van de heeft geen toegang tot uw account koppelen. <br> <br> tooreset uw wachtwoord, neem contact op met uw IT-medewerkers rechtstreeks voor help en laat ze weten dat u wilt tooreset zodat deze functie kan worden ingeschakeld voor u uw wachtwoord.|
| Wordt een foutbericht 'uw account is niet ingeschakeld voor wachtwoordherstel' na het invoeren van mijn gebruikers-ID | Uw account is niet ingeschakeld voor wachtwoordherstel <br> <br> We vinden het jammer, maar uw IT-personeel niet uw account voor gebruik met deze service is ingesteld. <br> <br> Als u wilt, we kunnen contact met een beheerder in uw organisatie tooreset uw wachtwoord voor u. | U ziet dit bericht omdat uw IT-personeel niet ingeschakeld voor wachtwoordherstel voor uw organisatie van de heeft geen toegang tot uw accountkoppeling of nog niet in licentie gegeven u toouse Hallo-functie. <br> <br> tooreset uw wachtwoord, klikt u op de contact op met een beheerder koppeling toosend een e-mailadres tooyour bedrijf laten weten u tooreset uw wachtwoord wilt zodat ze voor u deze functie kunnen inschakelen en van IT-personeel. |
| Wordt een foutbericht ' we kunnen uw account niet verifiëren' na het invoeren van mijn gebruikers-ID | We kunnen uw account niet verifiëren <br> <br> Als u wilt, we kunnen contact met een beheerder in uw organisatie tooreset uw wachtwoord voor u. | U ziet dit bericht omdat u zijn ingeschakeld voor het wachtwoord opnieuw instellen, maar toouse Hallo-service niet is geregistreerd. tooregister voor wachtwoord opnieuw instellen, gaat u toohttp://aka.ms/ssprsetup nadat u de toegangsaccount tooyour hebt hersteld. <br> <br> tooreset uw wachtwoord, klikt u op de contact op met een beheerder koppeling toosend een e-mailadres tooyour bedrijf van IT-personeel. |

## <a name="next-steps"></a>Volgende stappen

* [Hoe toochange uw met behulp van de selfservice voor wachtwoordherstel voor wachtwoordherstel](active-directory-passwords-update-your-own-password.md)
* [Registratiepagina voor het opnieuw instellen van een wachtwoord](http://aka.ms/ssprsetup)
* [Portal voor het opnieuw instellen van een wachtwoord](https://passwordreset.microsoftonline.com/)
* [Tooyour Microsoft-account kan niet aanmelden](https://support.microsoft.com/help/12429/microsoft-account-sign-in-cant)

[Register]: ./media/active-directory-passwords-reset-register/register-2-methods.png "Registratiepagina voor het opnieuw instellen van een wachtwoord met geregistreerde methoden en knop Voltooien"

