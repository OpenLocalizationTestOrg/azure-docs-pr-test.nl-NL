---
title: 'Aanpassen: Azure AD SSPR | Microsoft Docs'
description: Aanpassing van opties voor Azure AD self service voor wachtwoordherstel
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
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 4762fffef040f9b409355f9ee0e8cc593e3eea0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="customize-azure-ad-functionality-for-self-service-password-reset"></a>Azure AD-functionaliteit aanpassen voor selfservice voor wachtwoordherstel

IT-Professionals die op zoek toodeploy selfservice wachtwoordherstel kunnen Hallo ervaring toomatch hun gebruikers aanpassen.

## <a name="customize-hello-contact-your-administrator-link"></a>Hallo Neem contact op met uw beheerder koppeling aanpassen

Zelfs als SSPR niet ingeschakelde gebruikers nog steeds een 'contact op met uw beheerder' koppeling op Hallo wachtwoord portal opnieuw instellen.  Uw aanvraag voor hulp bij het wijzigen van het wachtwoord van de gebruiker van het Hallo-beheerders op deze koppeling klikt e-mailberichten. Dit e-mailbericht wordt verzonden toohello geadresseerden in Hallo volgorde te volgen:

1. Als hello **wachtwoordbeheerder** rol wordt toegewezen, zijn een melding van beheerders met deze rol
2. Als geen wachtwoordbeheerders zijn toegewezen, klikt u vervolgens beheerders met Hallo **beheerderrol** rol worden gewaarschuwd.
3. Als geen van de vorige rollen Hallo zijn toegewezen, klikt u vervolgens **globale beheerders** worden gewaarschuwd

In alle gevallen maximaal 100 ontvangers worden gewaarschuwd.

toofind voor meer informatie over de verschillende beheerdersrollen Hallo en hoe ze Zie tooassign document Hallo [beheerdersrollen toewijzen in Azure Active Directory](active-directory-assign-admin-roles.md)

### <a name="disable-contact-your-administrator-emails"></a>Schakel Neem contact op met uw beheerder e-mailberichten

Als uw organisatie wil niet dat beheerders op de hoogte wachtwoord opnieuw instellen van aanvragen, kan hello volgende configuratie worden ingeschakeld

* Selfservice voor wachtwoordherstel voor alle eindgebruikers inschakelen. Deze optie is onder **wachtwoordherstel > eigenschappen**.
    * Als u niet tooreset gebruikers hun eigen wachtwoorden wenst, kunt u het bereik leeg toegangsgroep tooan **niet raadzaam deze optie**.
* Hallo helpdesk-koppeling tooprovide aanpassen een web-URL of mailto: adres dat gebruikers tooget hulp kunnen gebruiken. Deze optie is onder **wachtwoordherstel > aanpassing > aangepaste helpdesk e-mail of URL**.

## <a name="customize-adfs-sign-in-page-for-sspr"></a>AD FS-aanmeldingspagina voor SSPR aanpassen

ADFS-beheerders kunnen een koppeling tootheir aanmeldingspagina met Hallo richtlijnen Hallo-artikel toevoegen [toevoegen aanmeldingspagina beschrijving](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/add-sign-in-page-description).

Hallo-opdracht die op uw ADFS-server volgt, voegt een koppeling toohello aanmeldingspagina van AD FS zodat gebruikers tooenter Hallo zelf uw wachtwoord opnieuw instellen van werkstroom rechtstreeks.

``` Set-ADFSGlobalWebContent -SigninPageDescriptionText "<p><A href=’https://passwordreset.microsoftonline.com’>Can’t access your account?</A></p>" ```

## <a name="customize-hello-sign-in-and-access-panel-look-and-feel"></a>Hallo aanmelden en toegang Configuratiescherm uiterlijk aanpassen

Wanneer uw gebruikers toegang krijgen de aanmeldingspagina hello tot, kunt u Hallo-logo dat wordt weergegeven samen met de Hallo aanmeldingspagina installatiekopie toofit uw huisstijl aanpassen.

Deze afbeeldingen worden weergegeven in de volgende omstandigheden Hallo:

* Nadat een gebruiker typt hun gebruikersnaam
* Gebruiker heeft toegang tot de aangepaste url
    * Door doorgeven Hallo wachtwoordherstel 'w' parameter toohello pagina, zoals 'https://login.microsoftonline.com/?whr=contoso.com'
    * Door het doorgeven van Hallo 'gebruikersnaam' parameter toohello wachtwoordherstel pagina, zoals ' https://login.microsoftonline.com/?username=admin@contoso.com'

### <a name="graphics-details"></a>Grafische details

Hallo volgende instellingen kunt u toochange Hallo visuele kenmerken van de aanmeldingspagina Hallo en kunt u vinden onder **Azure Active Directory**, **bedrijf huisstijl**, **bedrijf bewerken de huisstijl**

* Aanmeldingspagina afbeelding moet een PNG- of JPG-bestand 1420 x 1200 pixels en niet groter zijn dan 500KB. We raden toobe ongeveer 200 KB voor de beste resultaten.
* Achtergrondkleur van de aanmeldingspagina wordt gebruikt op de verbindingen met hoge latentie en moet Hallo RGB-hexadecimale notatie.
* Banner afbeelding moet een PNG- of JPG-bestand 60 x 280 pixels en niet groter zijn dan 10 KB.
* Vierkante logo (normaal en donker thema) PNG- of JPG 240 x 240 (formaat) niet groter zijn dan 10 KB.

### <a name="sign-in-text-options"></a>Opties voor tekst van aanmeldingspagina

Hallo na instellingen kunt u tooadd tekst toohello aanmeldingspagina relevante tooyour organisatie. Deze instellingen kunnen worden gevonden in het **Azure Active Directory**, **bedrijf huisstijl**, **huisstijl bewerken**

* **Gebruiker naam hint** vervangt Hallo voorbeeldtekst van someone@example.com met iets meer geschikt is voor uw gebruikers, aanbevolen toobe links standaard bij het ondersteunen van interne en externe gebruikers
* **Tekst van aanmeldingspagina** maximaal 256 tekens lang is. Deze tekst verschijnt ergens uw aanmelding voor gebruikers online en in hello Azure AD Join-ervaring op Windows 10. Gebruik deze tekst voor voorwaarden van het gebruik, instructies en tips voor uw gebruikers. **Iedereen kunt uw aanmeldingspagina zodat bieden geen gevoelige informatie hier zien.**

### <a name="keep-me-signed-in-disabled"></a>Aangemeld blijven uitgeschakeld

Hallo-optie 'aangemeld blijven uitgeschakeld', kunt gebruikers tooremain is aangemeld wanneer ze sluiten en opnieuw hun browservenster openen. Deze optie heeft geen gevolgen voor de levensduur van de sessie. Deze instelling te vinden onder **Azure Active Directory > bedrijf huisstijl > bewerken huisstijl**.

Sommige functies van Office 2010 en SharePoint Online hebben een afhankelijkheid op gebruikers kunnen toocheck wordt dit selectievakje in. Als u deze optie verbergt, kunnen gebruikers meer en onverwachte aanmelden wordt u gevraagd krijgen.

### <a name="directory-name"></a>Mapnaam

Kunt u het naamkenmerk Hallo onder **Azure Active Directory > eigenschappen** tooshow een beschrijvende organisatienaam weergegeven in de portal Hallo en geautomatiseerde communicatie. Deze optie is zichtbaar zijn in de vorm Hallo van automatische e-mailberichten in Hallo formulieren die volgen

* Beschrijvende naam in e-mailbericht 'Microsoft namens de CONTOSO-demo'
* Onderwerpregel in e-mailbericht 'CONTOSO-demo account e verificatiecode'

## <a name="next-steps"></a>Volgende stappen

Hallo volgende koppelingen vindt u aanvullende informatie met betrekking tot het wachtwoord opnieuw instellen met behulp van Azure AD

* [**Snel starten**](active-directory-passwords-getting-started.md): aan de slag met self-service wachtwoordbeheer van Azure AD 
* [**Licentieverlening**](active-directory-passwords-licensing.md): uw Azure AD-licentieverlening configureren
* [**Gegevens** ](active-directory-passwords-data.md) - begrijpen Hallo-gegevens die nodig is en hoe deze wordt gebruikt voor wachtwoordbeheer
* [**Implementatie** ](active-directory-passwords-best-practices.md) -plannen en implementeren van SSPR tooyour gebruikers via Hallo richtlijnen hier gevonden
* [**Beleid**](active-directory-passwords-policy.md): Azure AD-wachtwoordbeleid begrijpen en instellen
* [**Write-back van wachtwoord**](active-directory-passwords-writeback.md): hoe werkt write-back van wachtwoord met uw on-premises directory
* [**Rapportage**](active-directory-passwords-reporting.md): detecteren of, waar en wanneer uw gebruikers de functionaliteit voor self-service voor wachtwoordherstel gebruiken
* [**Technische diepgaand** ](active-directory-passwords-how-it-works.md) -Ga achter Hallo gordijn toounderstand hoe het werkt
* [**Veelgestelde vragen**](active-directory-passwords-faq.md): hoe? Hoe komt dat? Wat? Waar? Wie? Wanneer? -Beantwoordt tooquestions gewenste altijd tooask
* [**Problemen met** ](active-directory-passwords-troubleshoot.md) -informatie over hoe tooresolve algemene problemen zien we met SSPR

