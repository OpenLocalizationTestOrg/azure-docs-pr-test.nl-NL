---
title: 'Azure Active Directory B2C: Aanpassing van de taal met behulp | Microsoft Docs'
description: 
services: active-directory-b2c
documentationcenter: 
author: sama
ms.assetid: eec4d418-453f-4755-8b30-5ed997841b56
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/25/2017
ms.author: sama
ms.openlocfilehash: a8e4037014f5adf929dac7b5dc4db72ba0f5b292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-using-language-customization"></a>Azure Active Directory B2C: Aanpassing van de taal met behulp

>[!NOTE] 
>Deze functie is openbare preview.  Het is raadzaam dat u een testtenant gebruiken wanneer u deze functie.  We niet van plan bent van recente wijzigingen van toohello Hallo-algemene beschikbaarheid evaluatieversie maar behoudt Hallo rechts toomake dergelijke wijzigingen tooimprove Hallo-functie.  Zodra u een kans tootry-functie hebt, geef feedback over uw ervaringen en hoe we kunt u beter een.  U kunt feedback via hello Azure-portal met Hallo gezichtje face-hulpprogramma op Hallo rechtsboven.   Als er een zakelijke vereiste is voor u toogo live gebruik van deze functie tijdens de preview-fase hello, laat ons weten van uw scenario's en we u met de juiste richtlijnen Hallo en hulp kunnen opgeven.  U kunt contact met ons op [ aadb2cpreview@microsoft.com ](mailto:aadb2cpreview@microsoft.com).

Taal aanpassing kunt u uw gebruikers reis tooa andere taal toosuit uw klant moet toochange.  We bieden vertalingen voor 36 talen (Zie [aanvullende informatie](#additional-information)).  Zelfs als uw ervaring is alleen beschikbaar voor één taal, kunt u alle tekst op Hallo pagina's toosuit uw behoeften aanpassen.  

## <a name="how-does-language-customization-work"></a>Hoe werkt taal aanpassing?
Taal aanpassing kunt u tooselect welke talen uw reis gebruiker is beschikbaar in.  Zodra het Hallo-functie is ingeschakeld, kunt u Hallo-querytekenreeksparameter, ui_locales, bieden van uw toepassing.  Wanneer u in Azure AD B2C aanroept, vertalen we toohello landinstelling van uw pagina die u hebt aangegeven.  Met behulp van het type configuratie hebt u volledige controle over Hallo talen in uw reis gebruiker en Hallo taalinstellingen van de browser van de klant Hallo worden genegeerd. U kunt ook moet u mogelijk niet dat niveau van controle over welke talen Zie van uw klant.  Als u een ui_locales-parameter niet opgeeft, wordt Hallo klantervaring bepaald door hun browserinstellingen.  U kunt nog steeds bepalen welke talen uw gebruiker reis is vertaald tooby toe te voegen als een ondersteunde taal.  Als een klant browser set tooshow een taal u niet wilt dat toosupport en vervolgens Hallo taal die u hebt geselecteerd als een standaardwaarde in ondersteunde culturen in plaats daarvan wordt weergegeven.

1. **UI-landinstellingen opgegeven taal** -wanneer u de aanpassing van de taal hebt ingeschakeld, de gebruiker reis vertaalde toohello taal die u hier opgeeft is
2. **Browser gevraagde taal** -als er geen gebruikersinterface-landinstellingen is opgegeven, vertaalt toohello browser gevraagde taal, **als deze is opgenomen in de ondersteunde talen**
3. **De standaardtaal beleid** -als Hallo browser een taal niet opgeven of deze bevat een die niet wordt ondersteund, vertaalt toohello beleid standaardtaal

>[!NOTE]
>Als u aangepaste gebruikerskenmerken gebruikt, moet u tooprovide uw eigen vertalingen. Zie '[aanpassen van uw tekenreeksen](#customize-your-strings)' voor meer informatie.
>

## <a name="support-uilocales-requested-languages"></a>Ondersteuning ui_locales aangevraagd talen 
U kunt nu Hallo taal van Hallo gebruiker reis door toe te voegen Hallo ui_locales parameter doordat taal aanpassing van een beleid beheren.
1. [Volg deze stappen toonavigate toohello B2C-functiesblade op Hallo Azure-portal.](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-app-registration#navigate-to-b2c-settings)
2. Navigeer tooa beleid dat u tooenable vertalingen wenst.
3. Klik op **taal aanpassing**.
4. Hallo waarschuwing zorgvuldig lezen.  Eenmaal is ingeschakeld, kunt u 'Aanpassing taal' niet uitschakelen.
5. Hallo-functie inschakelen en klik op **OK**.
6. Sla het beleid op Hallo linkerbovenhoek van uw **beleid bewerken** blade.

## <a name="select-which-languages-your-user-journey-supports"></a>Selecteer de talen die ondersteuning biedt voor uw gebruiker reis 
Maak een lijst van toegestane talen voor uw gebruiker reis toobe omgezet als Hallo ui_locales parameter is niet opgegeven.
1. Zorg ervoor dat uw beleid heeft taal aanpassing' van de voorgaande instructies ingeschakeld.
2. Van uw **beleid bewerken** blade Selecteer **taal aanpassing**.
3. Gaat u tooyour **ondersteunde talen** blade.  Hier kunt u **taal toevoegen**.
4. Selecteer alle Hallo talen die u graag toobe ondersteund.  

>[!NOTE]
>Als een parameter ui_locales niet is opgegeven, is Hallo pagina taal van de browser van de klant van de vertaalde toohello alleen als op deze lijst
>

5. Klik op **Ok** Hallo onderin
6. Sluit Hallo **taal aanpassing** blade en **opslaan** uw beleid.

## <a name="customize-your-strings"></a>Uw tekenreeksen aanpassen
'Aanpassing taal' kunt u elke tekenreeks in uw reis gebruiker toocustomize.
1. Zorg ervoor dat uw beleid heeft taal aanpassing' van de voorgaande instructies Hallo ingeschakeld.
2. Van uw **beleid bewerken** blade Selecteer **taal aanpassing**.
3. Hallo linkermenubalk menu en selecteer **inhoud downloaden**.
4. Selecteer de gewenste tooedit Hallo-pagina.
5. Selecteer in de vervolgkeuzelijst Hallo gewenste tooedit voor Hallo-taal.
6. Klik op **Downloaden**. 

Deze stappen geven een JSON-bestand dat u uw tekenreeksen bewerken toostart kunt gebruiken.

### <a name="changing-any-string-on-hello-page"></a>Een willekeurige tekenreeks op Hallo pagina wijzigen
1. Open Hallo JSON-bestand downloaden van de voorgaande instructies in een JSON-editor.
2. Zoeken naar Hallo element gewenste toochange.  U vindt Hallo `StringId` van Hallo tekenreeks u zoekt of zoek naar Hallo `Value` gewenste toochange.
3. Update Hallo `Value` kenmerk met wat u weergeven wilt.
4. Hallo-bestand opslaan en uw wijzigingen te uploaden.

### <a name="changing-extension-attributes"></a>Uitbreidingskenmerken wijzigen
Als u op zoek bent toochange Hallo tekenreeks naar een aangepaste gebruikerskenmerk of tooadd één toohello JSON wilt, is het in de volgende indeling Hallo:
```JSON
{
  "LocalizedStrings": [
    {
      "ElementType": "ClaimType",
      "ElementId": "extension_<ExtensionAttribute>",
      "StringId": "DisplayName",
      "Override": false,
      "Value": "<ExtensionAttributeValue>"
    }
    [...]
}
```
>[!IMPORTANT]
>Als u een tekenreeks toooverride moet, zorg ervoor dat tooset hello `Override` waarde te`true`.  Als het Hallo-waarde is niet gewijzigd, wordt Hallo vermelding genegeerd. 
>

Vervang `<ExtensionAttribute>` met de naam van uw aangepaste gebruikerskenmerk Hallo.  
Vervang `<ExtensionAttributeValue>` met Hallo nieuwe tekenreeks toobe weergegeven.

### <a name="using-localizedcollections"></a>Met behulp van LocalizedCollections
Als u een setlijst met waarden tooprovide voor antwoorden wilt, moet u toocreate een `LocalizedCollections`.  Een `LocalizedCollections` is een matrix met `Name` en `Value` paren.  Hallo `Name` is wat wordt weergegeven en Hallo `Value` is wat Hallo claim wordt geretourneerd.  tooadd een `LocalizedCollections`, het Hallo na indeling heeft:

```JSON
{
  "LocalizedStrings": [...],
  "LocalizedCollections": [{
      "ElementType":"ClaimType", 
      "ElementId":"<UserAttribute>",
      "TargetCollection":"Restriction",
      "Override": false,
      "Items":[
           {
                "Name":"<Response1>",
                "Value":"<Value1>"
           },
           {
                "Name":"<Response2>",
                "Value":"<Value2>"
           }
     ]
  }]
}
```
>[!IMPORTANT]
>Als u een tekenreeks toooverride moet, zorg ervoor dat tooset hello `Override` waarde te`true`.  Als het Hallo-waarde is niet gewijzigd, wordt Hallo vermelding genegeerd. 
>

* `ElementId`is hello gebruiker van het kenmerk dat dit `LocalizedCollections` antwoord op
* `Name`Hallo gebruiker waarde weergegeven toohello
* `Value`is wat Hallo claim wordt geretourneerd wanneer deze optie is geselecteerd

### <a name="upload-your-changes"></a>Uw wijzigingen te uploaden
1. Nadat u Hallo wijzigingen tooyour JSON-bestand hebt voltooid, gaat u terug tooyour B2C-tenant.
2. Van uw **beleid bewerken** blade Selecteer **taal aanpassing**.
3. Hallo linkermenubalk menu en selecteer **inhoud uploaden**.
4. Hallo-pagina die u uw wijzigingen voor tooupload wilt selecteren.
5. Als u wilt dat tooupload een taal die u eerder een JSON voor hebt opgegeven, moet u toodelete Hallo eerdere vermelding.  U kunt het verwijderen door te klikken op Hallo `...` op Hallo van rechts van die taal en selecteer **verwijderen**.
6. Klik op **toevoegen** in de linkerbovenhoek Hallo.
7. Selecteer de taal Hallo van uw JSON-bestand.
8. Klik op Hallo map op de juiste Hallo en bladert u naar uw JSON-bestand.
9. Klik op Hallo **uploaden** knop op Hallo Hallo blade onderaan.
10. Ga terug tooyour **beleid bewerken** blade en klik op **opslaan**.

## <a name="additional-information"></a>Aanvullende informatie
### <a name="recommendations-for-language-customization"></a>Aanbevelingen voor 'Taal aanpassing'
Het is raadzaam om alleen als in vermeldingen tooyour taalbestanden voor tekenreeksen u expliciet wilt tooreplace.  We afdwingen een grootte limiet toohello-bestand dat is gecompileerd buiten alle JSON-vertalingen.  Als uw bestanden te groot is, het Hallo-prestaties van uw gebruiker reis heeft impact op.
### <a name="page-ui-customization-labels-are-removed-once-language-customization-is-enabled"></a>Page UI aanpassing van labels worden verwijderd zodra 'Aanpassing taal' is ingeschakeld
Wanneer u 'Aanpassing taal' hebt ingeschakeld, wordt uw vorige bewerkingen voor met Page UI-aanpassing van labels zijn verwijderd, met uitzondering van aangepaste kenmerken.  Deze wijziging wordt gedaan tooavoid conflicten in waar u uw tekenreeksen kunt bewerken.  U kunt doorgaan toochange de labels en andere tekenreeksen met taalbestanden in 'Aanpassing taal' uploaden.
### <a name="microsoft-is-committed-tooprovide-hello-most-up-to-date-translations-for-your-use"></a>Microsoft is doorgevoerd tooprovide Hallo meest recente vertalingen voor het gebruik
We continu verbeteren vertalingen en bewaar deze op naleving voor u.  We identificeren fouten en wijzigingen in globale terminologie en dat Hallo-updates die werkt probleemloos in uw reis gebruiker.
### <a name="support-for-right-to-left-languages"></a>Ondersteuning voor talen van rechts naar links
Er is geen ondersteuning voor talen van rechts naar links, als u nodig hebt met deze functie moet stemmen voor deze functie op [Azure Feedback](https://feedback.azure.com/forums/169401-azure-active-directory/suggestions/19393000-provide-language-support-for-right-to-left-languag).
### <a name="social-identity-provider-translations"></a>Vertalingen van de provider van sociale identiteit
We bieden Hallo ui_locales OIDC parameter toosocial aanmeldingen, maar ze worden niet herkend door sommige sociale identiteitsproviders, waaronder Facebook en Google. 
### <a name="browser-behavior"></a>Gedrag van de browser
Chrome en Firefox beide aanvragen voor de taal van hun instellen en als het een ondersteunde taal, deze wordt weergegeven voordat Hallo standaard.  Rand momenteel een andere taal geen aanvraagt en wordt de standaardtaal rechte toohello.
### <a name="known-issues"></a>Bekende problemen
* Het uploaden van taalbestanden voor Hallo MFA pagina in een beleid profiel bewerken is momenteel niet beschikbaar.
* `LocalizedCollections`voor waarden niet worden gegenereerd wanneer dat nodig is voor Hallo antwoordtype
### <a name="what-if-i-want-a-language-that-isnt-supported"></a>Wat gebeurt er als ik wil een taal die niet wordt ondersteund?
We zijn een uitbreiding van deze functie waarmee u een JSON-resource naar 'aangepaste talen' tooupload tooprovide plannen.  Hallo-functie kunt u de naam van toospecify Hallo en taal code voor elke taal en bieden *alle* Hallo vertalingen voor die taal.  Als u deze functie moet, stuur ons uw scenario op [ aadb2cpreview@microsoft.com ](mailto:aadb2cpreview@microsoft.com).  

### <a name="what-languages-are-supported"></a>Welke talen worden ondersteund?

| Taal              | Taalcode |
|-----------------------|---------------|
| Bengaals                | bn            |
| Tsjechisch                 | cs            |
| Deens                | da            |
| Duits                | de            |
| Grieks                 | el            |
| Nederlands               | en            |
| Spaans               | es            |
| Fins               | fi            |
| Frans                | fr            |
| Gujarati              | Gu            |
| Hindi                 | Hallo            |
| Kroatisch              | HR            |
| Hongaars             | hu            |
| Italiaans               | it            |
| Japans              | ja            |
| Kannada               | kN            |
| Koreaans                | ko            |
| Malajalam             | ml            |
| Marathi               | MR            |
| Maleis                 | MS            |
| Noors, Bokmål      | nb            |
| Nederlands                 | nl            |
| Punjabi               | Pa            |
| Pools                | pl            |
| Portugees - Brazilië   | pt-br         |
| Portugees - Portugal | pt-pt         |
| Roemeens              | ro            |
| Russisch               | ru            |
| Slowaaks                | SK            |
| Zweeds               | sv            |
| Tamil                 | DBC            |
| Telugu                | eren            |
| Thais                  | TH            |
| Turks               | TR            |
| Chinees - Vereenvoudigd  | zh-hans       |
| Chinees - Traditioneel | zh-hant       |
