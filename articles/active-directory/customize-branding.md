---
title: aaaCustomize pagina bent aangemeld in hello Azure Active Directory | Microsoft Docs
description: Meer informatie over hoe een bedrijf huisstijl toohello Azure aanmelden pagina tooadd
services: active-directory
documentationcenter: 
author: jeffgilb
manager: femila
editor: 
ms.assetid: f8b932bc-8b4f-42b5-a2d3-f2c076234a78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: jeffgilb
custom: it-pro
ms.openlocfilehash: 7a7ccdeef0764f6cf9e9e224acd4350983031fe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-add-company-branding-tooyour-sign-in-page-in-azure-ad"></a>Snelstartgids: Huisstijl tooyour-aanmeldingspagina in Azure AD toevoegen
tooavoid verwarring, willen veel bedrijven tooapply een consistent uiterlijk voor alle Hallo websites en services die ze beheren. Azure Active Directory (Azure AD) biedt deze mogelijkheid doordat u toocustomize Hallo vormgeving van Hallo aanmeldingspagina met uw bedrijfslogo en kleurenschema toepassen. Hallo-aanmeldingspagina is Hallo-pagina waarop wordt weergegeven wanneer u zich aanmeldt tooOffice 365 of andere toepassingen op Internet die van Azure AD als id-provider gebruikmaken. U communiceren met deze pagina tooenter uw referenties.

> [!NOTE]
> * Huisstijl is alleen beschikbaar als u een upgrade hebt uitgevoerd toohello Premium of Basic-editie van Azure AD of een Office 365-licentie hebt. Als een functie wordt ondersteund door uw licentietype controleren Hallo toolearn [prijspagina informatie voor Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/).
> 
> * Edities Azure Active Directory Premium en Basic zijn beschikbaar voor klanten in China Hallo wereldwijde exemplaar van Azure Active Directory. Edities Azure Active Directory Premium en Basic worden momenteel niet ondersteund in Microsoft Azure-service Hallo beheerd door 21Vianet in China. Voor meer informatie contact met ons opnemen Hallo [Azure Active Directory-Forum](https://feedback.azure.com/forums/169401-azure-active-directory/).

## <a name="customizing-hello-sign-in-page"></a>Hallo-aanmeldingspagina aanpassen

<!--You can customize hello following elements on hello sign-in page: <attach image>-->

Bedrijf huisstijl aanpassingen op de aanmeldingspagina hello Azure AD worden weergegeven wanneer gebruikers toegang krijgen een tenantspecifieke URL zoals tot [ *https://outlook.com/contoso.com*](https://outlook.com/contoso.com).

Wanneer gebruikers een generieke URL, zoals www.office.com bezoekt, is de aanmeldingspagina Hallo bevat geen aanpassingen voor huisstijl omdat Hallo systeem niet weet die Hallo gebruiker is. Nadat gebruikers hun gebruikersnaam invoeren of selecteren van een gebruikerstegel weergegeven huisstijl.

> [!NOTE]
> * Uw domeinnaam moet worden weergegeven als 'Actief' in hello **domeinen** gedeelte van hello Azure portal waarin u de huisstijl hebt geconfigureerd. Zie voor meer informatie [toevoegen van een aangepaste domeinnaam](add-custom-domain.md).
> * Aanmeldingspagina huisstijl niet meegenomen toohello aanmeldingspagina voor persoonlijke Microsoft-accounts. Als uw werknemers of business-gasten zich met een persoonlijk Microsoft-account aanmeldt, komt hun aanmeldingspagina niet overeen met Hallo huisstijl van uw organisatie.


### <a name="banner-logo"></a>Bannerlogo 

Beschrijving | Beperkingen | Aanbevelingen
------- | ------- | ----------
Hallo logo in banner wordt weergegeven op de aanmeldingspagina Hallo en Hallo Access Configuratiescherm-pagina's.<br>Dit betekent op Hallo aanmelden pagina nadat de organisatie van de gebruiker Hallo is vastgesteld, gewoonlijk nadat Hallo gebruikersnaam wordt ingevoerd.  | Transparante JPG of PNG<br>Maximale hoogte: 36 px<br>Maximale breedte: 245 px | Logo van uw organisatie hier gebruiken.<br>Gebruik een transparante afbeelding. Niet, wordt ervan uitgegaan dat de Hallo achtergrond wit worden.<br>Voeg geen opvulling om de logo in de installatiekopie van het Hallo of uw logo ziet er niet goed klein.

### <a name="username-hint"></a>Gebruikersnaam hint   
Beschrijving | Beperkingen | Aanbevelingen
------- | ------- | ----------
Dit past Hallo hint tekst in de gebruikersnaamvelden Hallo. | Unicode-tekst van too64 tekens<br>Alleen tekst zonder opmaak | U wordt aangeraden dat u geen dit instelt als u verwacht gastgebruikers buiten uw organisatie toosign in tooyour-app dat.
            
### <a name="sign-in-page-text"></a>Tekst van aanmeldingspagina   
Beschrijving | Beperkingen | Aanbevelingen
------- | ------- | ----------
Dit mag wordt Hallo Hallo aanmelden formulier onder aan en gebruikte toocommunicate aanvullende informatie zoals Hallo phone nummer tooyour helpdesk of een juridische mededeling. | Unicode-tekst van too256 tekens<br>Alleen tekst zonder opmaak (geen koppelingen of HTML-tags) 

### <a name="sign-in-page-image"></a>Afbeelding van de aanmeldingspagina  
Beschrijving | Beperkingen | Aanbevelingen
------- | ------- | ----------
Dit wordt weergegeven op de achtergrond Hallo van Hallo aanmeldingspagina, verankerde toohello center Hallo bekeken ruimte, en wordt schalen en bijsnijden toofill Hallo-browservenster.  <br>Scherm zoals mobiele telefoons erg smal, is deze afbeelding niet weergegeven.<br>Een zwarte masker met 0,55 dekking worden toegepast op deze afbeelding door onze code wanneer Hallo pagina wordt geladen. | JPG of PNG<br>Afbeelding van dimensies: 1920 x 1080 px<br>De bestandsgrootte: &gt; 300 KB | <br>Installatiekopieën gebruiken wanneer er een sterk onderwerp focus niet. ondoorzichtige Hallo aanmelden formulier wordt weergegeven boven Hallo midden van deze installatiekopie en kan een deel van de afbeelding hello, afhankelijk van de grootte van het browservenster Hallo Hallo dekken.<br>Hallo-bestandsgrootte zo klein mogelijk tooensure snelle laadtijden houden. 

### <a name="background-color"></a>Achtergrondkleur
Beschrijving | Beperkingen | Aanbevelingen
------- | ------- | ----------
Deze kleur wordt gebruikt in plaats van de achtergrondafbeelding Hallo op lage bandbreedte. |   RGB-kleur in de hexadecimale notatie (voorbeeld: #FFFFFF | Het is raadzaam om met Hallo primaire kleur van het logo in banner Hallo of de kleur van uw organisatie.

### <a name="show-option-tooremain-signed-in"></a>Optie tooremain aangemeld weergeven
Beschrijving | Beperkingen | Aanbevelingen
------- | ------- | ----------
Azure AD aanmelden biedt Hallo gebruiker Hallo optie tooremain is aangemeld wanneer ze sluiten en opnieuw hun browser openen. Gebruik deze toohide die optie.<br>Stel deze optie te 'Nee' toohide deze optie van uw gebruikers. | &nbsp; | Dit heeft geen invloed op de levensduur van de sessie.<br>Sommige functies van Office 2010 en SharePoint Online, is afhankelijk van gebruikers kunnen toochoose tooremain aangemeld. Als u deze toobe verborgen instelt, kunnen aanvullende en onverwachte prompts toosign in uw gebruikers te zien.

> [!NOTE]
> Alle elementen zijn optioneel. Als u een logo in banner met geen achtergrondafbeelding opgeeft, wordt de aanmeldingspagina Hallo uw logo en Hallo achtergrondafbeelding voor Hallo doelsite (bijvoorbeeld Office 365) weergegeven.

## <a name="add-company-branding-tooyour-directory"></a>Huisstijl tooyour directory toevoegen

1. Aanmelden te[hello Azure-portal](https://portal.azure.com) met een account met globale beheerdersrechten voor Hallo-directory.
2. Selecteer **meer services**, voer **gebruikers en groepen** in het tekstvak Hallo en selecteer vervolgens **Enter**.

   ![Gebruikersbeheer openen](./media/active-directory-branding-custom-signon-azure-portal/user-management.png)
3. Op Hallo **gebruikers en groepen** blade Selecteer **bedrijf huisstijl**.
4. Op Hallo **gebruikers en groepen - bedrijf huisstijl** blade, selecteer Hallo **bewerken** opdracht.

    ![Aangepaste huisstijl bewerken](./media/active-directory-branding-custom-signon-azure-portal/edit-branding.png)
5. Hallo-elementen die u wilt dat toocustomize wijzigen. Alle elementen zijn optioneel.
6. Klik op **Opslaan**.

Het kan tooan uur duren voor u de wijzigingen toohello aanmelden pagina huisstijl tooappear.

## <a name="add-language-specific-company-branding-tooyour-directory"></a>Taalspecifieke huisstijl-tooyour directory toevoegen

1. Meld u aan toohello [Azure AD-beheercentrum](https://aad.portal.azure.com) met een account met globale beheerdersrechten voor Hallo-directory.
2. Selecteer **gebruikers en groepen** in het tekstvak Hallo en selecteer vervolgens **Enter**.

   ![Gebruikersbeheer openen](./media/active-directory-branding-localize-azure-portal/user-management.png)
3. Op Hallo **gebruikers en groepen** blade Selecteer **bedrijf huisstijl**.
4. Op Hallo **gebruikers en groepen - bedrijf huisstijl** blade, selecteer Hallo **taal toevoegen** opdracht.

    ![De huisstijl elementen taalspecifieke toevoegen](./media/active-directory-branding-localize-azure-portal/add-language.png)
5. Hallo-elementen die u wilt dat toocustomize wijzigen. Alle elementen zijn optioneel.
6. Klik op **Opslaan**.

Het kan tooan uur duren voor u de wijzigingen toohello aanmelden pagina huisstijl tooappear.

## <a name="next-steps"></a>Volgende stappen
In deze snelstartgids hebt u geleerd hoe tooadd bedrijf huisstijl tooyour Azure AD-directory. 

U kunt Hallo koppeling tooconfigure na uw huisstijl op Azure AD van hello Azure-portal gebruiken.

> [!div class="nextstepaction"]
> [Een bedrijfshuisstijl toevoegen](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/LoginTenantBrandingBlade) 