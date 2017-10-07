---
title: 'Implementeren: Azure AD-self-service voor wachtwoordherstel | Microsoft Docs'
description: Tips voor een geslaagde implementatie van Azure AD-self-service voor wachtwoordherstel
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: f8cd7e68-2c8e-4f30-b326-b22b16de9787
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 73d31679b38ff009a767335adaebc49fbc5a75b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="roll-out-password-reset-for-users"></a>Wachtwoordherstel implementeren voor gebruikers

De meeste klanten stappen Hallo Volg tooensure een smooth rollout van SSPR-functionaliteit.

1. [Wachtwoordherstel inschakelen in uw directory](active-directory-passwords-getting-started.md)
2. [On-premises AD-machtigingen configureren voor write-back van wachtwoord](active-directory-passwords-how-it-works.md#active-directory-permissions)
3. [Wachtwoord terugschrijven configureren](active-directory-passwords-writeback.md#configuring-password-writeback) toowrite wachtwoorden van Azure AD back tooyour on-premises adreslijst
4. [Vereiste licenties toewijzen en verifiëren](active-directory-passwords-licensing.md)
5. Als u wilt dat tooroll uit geleidelijk, u kunt eventueel limiet wachtwoordherstel tooa groep gebruikers tooroll uit Hallo functie langzaam gedurende een bepaalde periode. toodo deze Hallo ingesteld **Self Service wachtwoord opnieuw instellen ingeschakeld** in-of uitschakelen van **iedereen** te**een groep** en selecteert u een security group tooenable voor wachtwoordherstel. Hallo leden van deze groep moet alle licenties die zijn toegewezen toothem en is een uitstekende manier tooenable [groep op basis van licentieverlening](active-directory-passwords-licensing.md#enable-group-or-user-based-licensing).
6. Hallo minimale set van vullen [verificatiegegevens](active-directory-passwords-data.md), op basis van uw beleid.
7. Leer uw gebruikers hoe toouse SSPR, door ze te verzenden instructies tooshow ze hoe tooregister en hoe tooreset.
    > [!NOTE]
    > Test self-service voor wachtwoordherstel met een gebruiker en niet als beheerder, aangezien Microsoft sterke verificatievereisten afdwingt voor Azure-accounts van beheerders. Zie voor meer informatie over Hallo beheerder wachtwoordbeleid onze [diepgaand artikel](active-directory-passwords-how-it-works.md).

8. U kunt kiezen tooenforce registratie op elk gewenst moment en vereisen tooreconfirm gebruikers hun verificatiegegevens na een bepaalde periode. Als u niet dat uw gebruikers toohave tooregister wilt, kunt u [implementeren zonder registratie door eindgebruikers voor wachtwoordherstel](active-directory-passwords-data.md).
9. Bekijk na verloop van tijd gebruikers registreren en gebruiken van door het bekijken van Hallo [reporting verstrekt door Azure AD](active-directory-passwords-reporting.md).

## <a name="email-based-rollout"></a>Implementatie op basis van e-mail

Veel klanten vinden dat een campagne e-mailbericht met instructies voor eenvoudige toouse is Hallo gemakkelijkste manier tooget gebruikers toouse SSPR. [We hebt drie eenvoudige e-mailberichten die u als sjablonen toohelp in uw implementatie gebruiken kunt gemaakt.](https://onedrive.live.com/?authkey=%21AD5ZP%2D8RyJ2Cc6M&id=A0B59A91C740AB16%2125063&cid=A0B59A91C740AB16)

* **Binnenkort beschikbaar** e-sjabloon toobe gebruikt in Hallo weken of dagen vóór implementatie toolet gebruikers weten dat ze iets toodo nodig.
* **Nu beschikbaar** e-sjabloon gebruikt toobe Hallo dag van starten toodrive gebruikers tooregister en bevestigt u hun verificatiegegevens zodat ze SSPR gebruiken kunnen wanneer ze deze nodig hebt.
* **Herinnering aanmelden** e-mailsjabloon voor een paar dagen tooweeks na implementatie tooremind gebruikers tooregister en controleer de verificatiegegevens.

## <a name="creating-your-own-password-portal"></a>Uw eigen wachtwoordportal maken

Veel van onze klanten met grotere toohost webpagina kiezen en maken van een basis-DNS-vermelding, zoals https://passwords.contoso.com. Vullen van deze pagina met koppelingen toohello Azure AD-wachtwoord opnieuw instellen, wachtwoord opnieuw instellen voor registratie, portals voor wachtwoord wijzigen en andere organisatie-specifieke informatie. In een e-mailberichten of Folders u verstuurt, kunt u vervolgens opnemen een huisstijl gemakkelijk te onthouden, URL dat gebruikers toowhen moeten toouse Hallo services kunnen gaan.

* Portal voor wachtwoordherstel: https://passwordreset.microsoftonline.com/
* Portal voor registratie voor wachtwoordherstel: http://aka.ms/ssprsetup
* Portal voor wijzigen wachtwoord: https://account.activedirectory.windowsazure.com/ChangePassword.aspx

## <a name="using-enforced-registration"></a>Gedwongen registratie gebruiken

Als u uw gebruikers tooregister voor wachtwoordherstel wilt, kunt u ze afdwingen als tooregister wanneer ze zich aanmelden met behulp van Azure AD. U kunt deze optie inschakelen via uw directory **wachtwoordherstel** blade doordat Hallo **gebruikers vereisen tooRegister tijdens het aanmelden** optie op Hallo **registratie** tabblad.

Beheerders kunnen gebruikers de toore registratie vereisen na een bepaalde periode door Hallo instelling **aantal dagen voordat gebruikers worden gevraagd tooreconfirm hun verificatiegegevens** tussen 0-730 dagen.

Nadat u deze optie inschakelt, gebruikers die zich ziet een bericht dat hen informeert de beheerder heeft vereist dat ze tooverify hun verificatiegegevens.

## <a name="populate-authentication-data"></a>Verificatiegegevens invullen

Als u [verificatiegegevens voor uw gebruikers vullen](active-directory-passwords-data.md), en vervolgens gebruikers niet tooregister voor wachtwoord opnieuw instellen hoeven voordat deze kunnen toouse SSPR. Als gebruikers Hallo verificatiegegevens gedefinieerd die voldoet aan Hallo beleid voor wachtwoordherstel voor u hebt gedefinieerd hebben, gebruikers kunnen tooreset zijn hun wachtwoorden.

## <a name="disabling-self-service-password-reset"></a>Selfservice voor wachtwoordherstel uitschakelen

Het uitschakelen van de selfservice voor wachtwoordherstel is net zo eenvoudig als uw Azure AD-tenant openen en te gaan**wachtwoordherstel**, **eigenschappen**, en het kiezen van **niemand** onder  **Selfservice voor wachtwoordherstel ingeschakeld**

## <a name="next-steps"></a>Volgende stappen

Hallo volgende koppelingen vindt u aanvullende informatie met betrekking tot het wachtwoord opnieuw instellen met behulp van Azure AD

* [**Snel starten**](active-directory-passwords-getting-started.md): aan de slag met self-service wachtwoordbeheer van Azure AD 
* [**Licentieverlening**](active-directory-passwords-licensing.md): uw Azure AD-licentieverlening configureren
* [**Gegevens** ](active-directory-passwords-data.md) - begrijpen Hallo-gegevens die nodig is en hoe deze wordt gebruikt voor wachtwoordbeheer
* [**Aanpassen** ](active-directory-passwords-customize.md) -Hallo uiterlijk Hallo SSPR ervaring voor uw bedrijf aanpassen.
* [**Beleid**](active-directory-passwords-policy.md): Azure AD-wachtwoordbeleid begrijpen en instellen
* [**Write-back van wachtwoord**](active-directory-passwords-writeback.md): hoe werkt write-back van wachtwoord met uw on-premises directory
* [**Rapportage**](active-directory-passwords-reporting.md): detecteren of, waar en wanneer uw gebruikers de functionaliteit voor self-service voor wachtwoordherstel gebruiken
* [**Technische diepgaand** ](active-directory-passwords-how-it-works.md) -Ga achter Hallo gordijn toounderstand hoe het werkt
* [**Veelgestelde vragen**](active-directory-passwords-faq.md): hoe? Hoe komt dat? Wat? Waar? Wie? Wanneer? -Beantwoordt tooquestions gewenste altijd tooask
* [**Problemen met** ](active-directory-passwords-troubleshoot.md) -informatie over hoe tooresolve algemene problemen zien we met SSPR
