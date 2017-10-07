---
title: Een gebruikersinterface aanpassen met behulp van aangepaste beleidsregels - Azure AD B2C | Microsoft Docs
description: Meer informatie over het aanpassen van een gebruikersinterface (UI) tijdens het gebruik van aangepast beleid in Azure AD B2C.
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: 658c597e-3787-465e-b377-26aebc94e46d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/04/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: 6f00995e54c9f9ef27cc51e38f3de07cd5817cc1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-configure-ui-customization-in-a-custom-policy"></a>Azure Active Directory B2C: UI-aanpassing in een aangepast beleid configureren

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Nadat u dit artikel hebt voltooid, hebt u een aangepast beleid voor aanmelden en aanmelden met uw merk en identiteit. Met Azure Active Directory B2C (Azure AD B2C), u krijgt bijna volledig beheer van de inhoud HTML en CSS Hallo dat toousers heeft ingediend. Wanneer u een aangepast beleid gebruikt, configureert u de UI-aanpassing in XML in plaats van het gebruik van besturingselementen in hello Azure-portal. 

## <a name="prerequisites"></a>Vereisten

Voordat u begint, voltooien [aan de slag met aangepaste beleidsregels](active-directory-b2c-get-started-custom.md). U hebt een werkende aangepast beleid voor aanmelden en aanmelden met lokale accounts.

## <a name="page-ui-customization"></a>Page UI-aanpassing

Hallo pagina UI aanpassing functie gebruikt, kunt u Hallo uiterlijk van het aangepaste beleid aanpassen. U kunt ook behouden merk en visuele consistentie tussen uw toepassing en de Azure AD B2C.

Dit is hoe het werkt: Azure AD B2C wordt code wordt uitgevoerd in de browser van uw klant en maakt gebruik van een benadering van moderne aangeroepen [Cross-Origin-Resource delen (CORS)](http://www.w3.org/TR/cors/). Geef eerst een URL in Hallo aangepast beleid met aangepaste HTML-inhoud. Azure AD B2C-UI-elementen met Hallo HTML-inhoud die is geladen vanaf uw URL en wordt vervolgens weergegeven Hallo pagina toohello klant samenvoegingen.

## <a name="create-your-html5-content"></a>Uw HTML5 inhoud maken

Maak HTML inhoud met de naam van uw product in Hallo titel.

1. Kopieer Hallo HTML-fragment te volgen. Indeling geldig is HTML5 met een leeg element aangeroepen  *\<div-id = 'api'\>\</div\>*  zich binnen Hallo  *\<hoofdtekst\>*  labels. Dit element geeft aan waar Azure AD B2C inhoud toobe ingevoegd.

   ```html
   <!DOCTYPE html>
   <html>
   <head>
       <title>My Product Brand Name</title>
   </head>
   <body>
       <div id="api"></div>
   </body>
   </html>
   ```

   >[!NOTE]
   >Uit veiligheidsoverwegingen is Hallo gebruik van JavaScript momenteel geblokkeerd om aan te passen.

2. Hallo gekopieerd codefragment in een teksteditor plakken en sla Hallo-bestand als *aanpassen ui.html*.

## <a name="create-an-azure-blob-storage-account"></a>Een Azure Blob storage-account maken

>[!NOTE]
> In dit artikel gebruiken we Azure Blob storage toohost onze content. U kunt toohost uw inhoud op een webserver, maar u moet [CORS zijn ingeschakeld op uw webserver](https://enable-cors.org/server.html).

toohost deze HTML-inhoud in Blob storage, Hallo te volgen:

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Op Hallo **Hub** selecteert u **nieuw** > **opslag** > **opslagaccount**.
3. Voer een unieke **naam** voor uw opslagaccount.
4. **Implementatiemodel** kan blijven **Resource Manager**.
5. Wijziging **soort Account** te**Blob storage**.
6. **Prestaties** kan blijven **standaard**.
7. **Replicatie** kan blijven **RA-GRS**.
8. **Toegangslaag** kan blijven **Hot**.
9. **Versleuteling van de opslagruimte** kan blijven **uitgeschakelde**.
10. Selecteer een **abonnement** voor uw opslagaccount.
11. Maak een **resourcegroep** of een bestaande set selecteren.
12. Selecteer Hallo **geografische locatie** voor uw opslagaccount.
13. Klik op **maken** toocreate Hallo storage-account.  
    Nadat het Hallo-implementatie is voltooid, Hallo **opslagaccount** blade wordt automatisch geopend.

## <a name="create-a-container"></a>Een container maken

een openbare Blob storage-container toocreate Hallo te volgen:

1. Klik op Hallo **overzicht** tabblad.
2. Klik op **Container**.
3. Voor **naam**, type **$root**.
4. Stel **toegangstype** te**Blob**.
5. Klik op **$root** tooopen Hallo nieuwe container.
6. Klik op **Uploaden**.
7. Klik op het pictogram map Hallo volgende te**selecteert u een bestand**.
8. Ga te**aanpassen ui.html**, die u eerder in Hallo gemaakt [Page UI-aanpassing](#the-page-ui-customization-feature) sectie.
9. Klik op **Uploaden**.
10. Selecteer Hallo aanpassen ui.html blob die u hebt geüpload.
11. Volgende te**URL**, klikt u op **kopie**.
12. In een browser, plak de URL van de Hallo gekopieerd en gaat u toohello site. Als Hallo site is niet toegankelijk is, controleert u of Hallo container toegangstype te is ingesteld**blob**.

## <a name="configure-cors"></a>CORS configureren

Blob-opslag configureren voor het delen van Cross-Origin-Resource door Hallo volgende te doen:

>[!NOTE]
>Tootry uit Hallo-functie voor het aanpassen van gebruikersinterface wilt met behulp van onze voorbeeldinhoud HTML en CSS? We bieden [een eenvoudige helper hulpprogramma](active-directory-b2c-reference-ui-customization-helper-tool.md) die uploadt en configureert u onze voorbeelden op uw Blob storage-account. Als u Hallo-hulpprogramma gebruikt, gaat u verder te[wijzigen van het aangepaste beleid registreren of aanmelden](#modify-your-sign-up-or-sign-in-custom-policy).

1. Op Hallo **opslag** blade onder **instellingen**Open **CORS**.
2. Klik op **Add**.
3. Voor **toegestane oorsprongen**, typt u een sterretje (\*).
4. In Hallo **toegestane termen** vervolgkeuzelijst, selecteer **ophalen** en **opties**.
5. Voor **toegestaan headers**, typt u een sterretje (\*).
6. Voor **blootgesteld headers**, typt u een sterretje (\*).
7. Voor **maximale leeftijd (seconden)**, type **200**.
8. Klik op **Add**.

## <a name="test-cors"></a>Test CORS

Valideren dat u klaar bent door Hallo volgende te doen:

1. Ga toohello [test cors.org](http://test-cors.org/) website en plakken Hallo-URL in Hallo **externe URL** vak.
2. Klik op **aanvraag verzenden**.  
    Als u een foutbericht ontvangt, controleert u of uw [CORS-instellingen voor](#configure-cors) juist zijn. Of u kunt mogelijk ook tooclear uw browser-cache een browsersessie van privé-openen door op Ctrl + Shift + P te drukken.

## <a name="modify-your-sign-up-or-sign-in-custom-policy"></a>Wijzigen van het aangepaste beleid registreren of aanmelden

Onder Hallo op het hoogste niveau  *\<TrustFrameworkPolicy\>*  labels, zult u  *\<BuildingBlocks\>*  label. Binnen Hallo  *\<BuildingBlocks\>*  tags, Voeg een  *\<ContentDefinitions\>*  code door te kopiëren Hallo voorbeeld te volgen. Vervang *your_storage_account* met Hallo-naam van uw opslagaccount.

  ```xml
  <BuildingBlocks>
    <ContentDefinitions>
      <ContentDefinition Id="api.idpselections">
        <LoadUri>https://{your_storage_account}.blob.core.windows.net/customize-ui.html</LoadUri>
      </ContentDefinition>
    </ContentDefinitions>
  </BuildingBlocks>
  ```

## <a name="upload-your-updated-custom-policy"></a>Upload uw bijgewerkte aangepast beleid

1. In Hallo [Azure-portal](https://portal.azure.com), [schakelen naar de context van uw Azure AD B2C-tenant hello](active-directory-b2c-navigate-to-b2c-context.md), en open vervolgens Hallo **Azure AD B2C** blade.
2. Klik op **alle beleidsregels**.
3. Klik op **uploaden beleid**.
4. Uploaden `SignUpOrSignin.xml` Hello  *\<ContentDefinitions\>*  code die u eerder hebt toegevoegd.

## <a name="test-hello-custom-policy-by-using-run-now"></a>Hallo aangepast beleid testen met behulp van **nu uitvoeren**

1. Op Hallo **Azure AD B2C** blade te gaan**alle beleidsregels**.
2. Selecteer Hallo aangepaste beleid dat u hebt geüpload en klikt u op Hallo **nu uitvoeren** knop.
3. U moet kunnen toosign up met behulp van een e-mailadres.

## <a name="reference"></a>Naslaginformatie

Voor de UI-aanpassing Hier vindt u voorbeeldsjablonen:

```
git clone https://github.com/azureadquickstarts/b2c-azureblobstorage-client
```

Hallo sample_templates/wingtip map bevat Hallo volgende HTML-bestanden:

| HTML5-sjabloon | Beschrijving |
|----------------|-------------|
| *phonefactor.HTML* | Dit bestand als sjabloon gebruiken voor een multi-factor authentication-pagina. |
| *ResetPassword.HTML* | Dit bestand te gebruiken als een sjabloon voor een wachtwoordpagina vergeten. |
| *selfasserted.HTML* | Dit bestand als een sjabloon voor een aanmeldingspagina sociale account, de aanmeldingspagina van een lokaal account of een aanmeldingspagina lokale account gebruiken. |
| *Unified.HTML* | Dit bestand als sjabloon gebruiken voor een uniforme registreren of aanmelden pagina. |
| *updateprofile.HTML* | Dit bestand als een sjabloon voor een update-profielpagina gebruiken. |

In Hallo [, wijzigt u de sectie registreren of aanmelden aangepast beleid](#modify-your-sign-up-or-sign-in-custom-policy), u hebt geconfigureerd Hallo inhoud definitie voor `api.idpselections`. Hallo volledige set van inhoud definitie-id's die worden herkend door hello Azure AD B2C identiteit ervaring framework en de bijbehorende beschrijvingen zijn in de volgende tabel Hallo:

| De definitie van de inhoud-ID | Beschrijving | 
|-----------------------|-------------|
| *API.Error* | **Foutpagina**. Deze pagina wordt weergegeven wanneer een uitzondering of een fout is opgetreden. |
| *API.idpselections* | **Id-provider selectiepagina**. Deze pagina bevat een lijst met de id-providers die gebruiker Hallo uit tijdens het aanmelden kiezen kunnen. Deze opties zijn enterprise identiteitsproviders, sociale id-providers zoals Facebook en Google + of lokale accounts. |
| *API.idpselections.Signup* | **Selectie van de id-provider voor registratie**. Deze pagina bevat een lijst met providers die gebruiker Hallo uit tijdens de registratie kiezen kunnen van de identiteit. Deze opties zijn enterprise identiteitsproviders, sociale id-providers zoals Facebook en Google + of lokale accounts. |
| *API.localaccountpasswordreset* | **Wachtwoordpagina vergeten**. Deze pagina bevat een formulier die gebruiker Hallo tooinitiate het wachtwoord moet voltooien.  |
| *API.localaccountsignin* | **Aanmeldingspagina voor lokaal account**. Deze pagina bevat een formulier-in voor het aanmelden met een lokaal account dat is gebaseerd op een e-mailadres of een gebruikersnaam. Hallo formulier kan een tekstinvoervak en wachtwoordvak vermelding bevatten. |
| *API.localaccountsignup* | **Lokaal account aanmeldingspagina**. Deze pagina bevat een aanmeldingsformulier hebt ingevuld voor het aanmelden voor een lokaal account dat is gebaseerd op een e-mailadres of een gebruikersnaam. Hallo formulier kan verschillende invoer besturingselementen bevatten, zoals een tekstinvoervak vak een wachtwoord, een keuzerondje, één vervolgkeuzelijsten en meervoudige selectie selectievakjes. |
| *API.phonefactor* | **Multi-factor authentication-pagina**. Op deze pagina, kunnen gebruikers hun telefoonnummers (met behulp van tekst of stem) controleren tijdens het registreren of aanmelden. |
| *API.selfasserted* | **De aanmeldpagina sociale account**. Deze pagina bevat een aanmeldingsformulier hebt ingevuld die gebruikers moeten worden voltooid wanneer ze zich registreren met behulp van een bestaand account van een identiteitsprovider van sociale zoals Facebook of Google +. Deze pagina is vergelijkbaar toohello voorafgaand aan de aanmeldingspagina sociale account, behalve Hallo wachtwoord invoervelden. |
| *API.selfasserted.profileupdate* | **Update profielpagina**. Deze pagina bevat een formulier dat gebruikers tooupdate hun profiel gebruiken kunnen. Deze pagina is vergelijkbaar toohello sociale account aanmeldingspagina, met uitzondering van invoervelden Hallo-wachtwoord. |
| *API.signuporsignin* | **Unified registreren of aanmelden pagina**. Deze pagina verwerkt beide Hallo zich kunnen registreren en aanmelden van gebruikers, die enterprise identiteitsproviders, sociale id-providers zoals Facebook of Google + of lokale accounts kunnen gebruiken.  |

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over de UI-elementen die kunnen worden aangepast, [Naslaggids voor aanpassing van de gebruikersinterface voor ingebouwde beleid](active-directory-b2c-reference-ui-customization.md).
