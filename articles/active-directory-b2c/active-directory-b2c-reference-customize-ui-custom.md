---
title: 'Azure Active Directory B2C: Verwijzen naar: Hallo gebruikersinterface van het traject van een gebruiker met een aangepast beleid aanpassen | Microsoft Docs'
description: Een onderwerp op Azure Active Directory B2C aangepast beleid
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/25/2017
ms.author: joroja
ms.openlocfilehash: 11f2a7575b95a186399d83266850fe44d650371b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="customize-hello-ui-of-a-user-journey-with-custom-policies"></a>Hallo gebruikersinterface van het traject van een gebruiker met een aangepast beleid aanpassen

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

> [!NOTE]
> Dit artikel is een geavanceerde beschrijving van de werking van UI-aanpassing en hoe tooenable met B2C aangepaste beleidsregels, met behulp van de identiteit ervaring Framework Hallo


Een naadloze gebruikerservaring is de sleutel voor een oplossing voor business-to-consumer. Door naadloze gebruikerservaring bedoelen we een ervaring op apparaat of de browser, waarbij een gebruiker reis door onze service kan niet worden onderscheiden van die van de klantenservice Hallo die ze gebruiken.

## <a name="understand-hello-cors-way-for-ui-customization"></a>Hallo CORS manier voor aanpassing van de gebruikersinterface begrijpen

Azure AD B2C kunt u toocustomize Hallo-en-vormgeving van de gebruikerservaring (UX) op Hallo verschillende pagina's die mogelijk kunnen worden geleverd en weergegeven door Azure AD B2C via uw aangepaste beleidsregels.

Azure AD B2C wordt om die reden wordt code uitgevoerd in de browser uw consumenten en maakt gebruik van Hallo benadering van moderne en standard [Cross-Origin-Resource delen (CORS)](http://www.w3.org/TR/cors/) tooload aangepaste inhoud van een specifieke URL die u in een aangepast beleid opgeeft toopoint tooyour HTML5/CSS-sjablonen. CORS is een mechanisme waarmee beperkte resources, zoals lettertypen, op een webpagina toobe aangevraagd vanuit een ander domein buiten Hallo domein waaruit Hallo bron afkomstig is.

Vergeleken toohello oude traditionele manier, waar de sjabloonpagina's eigendom zijn van Hallo oplossing waarin u hebt opgegeven beperkt tekst en afbeeldingen, beperkt beheer van indeling en de werking waar de toonaangevende toomore dan problemen tooachieve naadloos aangeboden is, Hallo CORS manier biedt ondersteuning voor HTML5 en CSS en kunt u:

- Hallo-inhoud hosten en hello oplossing injects de besturingselementen die met behulp van de client een script.
- Volledige controle over elke pixel van lay-out en zorgeloos hebben.

U kunt zoveel inhoudspagina's desgewenst door HTML5/CSS-bestanden naar gelang van toepassing op te geven.

> [!NOTE]
> Uit veiligheidsoverwegingen is Hallo gebruik van JavaScript momenteel geblokkeerd om aan te passen. toounblock JavaScript, gebruik van een aangepaste domeinnaam voor uw Azure AD B2C-tenant is vereist.

In elk van uw sjablonen HTML5/CSS, bieden u een *anker* element, wat overeenkomt met toohello vereist `<div id=”api”>` element in Hallo HTML-indeling of Hallo inhoudspagina als hierna illustreren. Azure AD B2C vereist dat alle inhoudspagina's deze specifieke div

```
<!DOCTYPE html>
<html>
  <head>
    <title>Your page content’s tile!</title>
  </head>
  <body>
    <div id="api"></div>
  </body>
</html>
```

Azure AD B2C-inhoud voor Hallo pagina wordt ingevoegd in deze div, terwijl de rest Hallo van Hallo pagina is jouw e-mailadres toocontrol. Hello Azure AD B2C JavaScript-code in uw inhoud ophaalt en onze HTML injects in dit specifieke div-element. Azure AD B2C injects Hallo volgende besturingselementen naar gelang van toepassing: account kiezer besturingselement, besturingselementen voor aanmelding (momenteel telefonische) besturingselementen van meerdere factoren en kenmerk verzameling besturingselementen. Azure AD B2C zorgt ervoor dat alle Hallo besturingselementen zijn HTML5 compatibel is en toegankelijk is, alle Hallo-besturingselementen kunnen volledig worden opgemaakt is en dat de versie van een besturingselement niet wordt gaat.

Hallo wordt samengevoegde inhoud uiteindelijk weergegeven als Hallo dynamisch document tooyour consumer.

tooensure Hallo bovenstaande werkt zoals verwacht, moet:

- Zorg ervoor dat uw inhoud HTML5 compatibel is en toegankelijk is
- Zorg ervoor dat de inhoudsserver voor CORS is ingeschakeld.
- Fungeren inhoud via HTTPS.
- Absolute URL zoals https://yourdomain/content gebruiken voor alle koppelingen en CSS-inhoud.

> [!TIP]
> tooverify die site zijn voor het hosten van uw inhoud op Hallo heeft CORS is ingeschakeld en CORS-aanvragen te testen, kunt u Hallo site http://test-cors.org/. Met vriendelijke groet toothis site, u kunt gewoon verzenden Hallo CORS aanvraag tooa externe server (tootest als CORS wordt ondersteund) of tooa testserver voor Hallo CORS aanvraag verzenden (tooexplore bepaalde functies van CORS).

> [!TIP]
> Hallo site http://enable-cors.org/ vormt ook een meer dan nuttige informatiebronnen op CORS.

Dankzij toothis CORS gebaseerde benadering, Hallo eindgebruikers hebben dan consistente ervaring tussen de toepassing en het Hallo-pagina's die worden bediend door Azure AD B2C.

## <a name="create-a-storage-account"></a>Een opslagaccount maken

Als een vereiste moet u een opslagaccount toocreate. U moet een Azure-abonnement toocreate een Azure Blob Storage-account. U kunt aanmelden met een gratis proefversie op Hallo [Azure-website](https://azure.microsoft.com/en-us/pricing/free-trial/).

1. Open een browsersessie en navigeer van toohello [Azure-portal](https://portal.azure.com).
2. Aanmelden met uw beheerdersreferenties.
3. Klik op **nieuw** > **gegevens en opslag** > **opslagaccount**.  Een **storage-account maken** blade wordt geopend.
4. In **naam**, Geef een naam voor Hallo storage-account, bijvoorbeeld *contoso369b2c*. Deze waarde zal later kan worden verwezen als te*storageAccountName*.
5. Kies de benodigde selecties Hallo voor Hallo prijscategorie, resourcegroep Hallo en Hallo-abonnement. Zorg ervoor dat u Hallo hebt **pincode tooStartboard** optie ingeschakeld. Klik op **Create**.
6. Ga terug toohello Startboard en klikt u op Hallo storage-account dat u zojuist hebt gemaakt.
7. In Hallo **Services** sectie, klikt u op **Blobs**. Een **blade Blob-service** wordt geopend.
8. Klik op **+ Container**.
9. In **naam**, Geef een naam voor de container hello, bijvoorbeeld *b2c*. Deze waarde zal worden later waarnaar wordt verwezen tooas *containerName*.
9. Selecteer **Blob** als Hallo **toegangstype**. Klik op **Create**.
10. Hallo-container die u hebt gemaakt wordt weergegeven in de lijst Hallo op Hallo **blade Blob-service**.
11. Sluit Hallo **Blobs** blade.
12. Op Hallo **blade opslagaccount**, klikt u op Hallo **sleutel** pictogram. Een **de blade sleutels toegang** wordt geopend.  
13. Schrijf Hallo-waarde van **key1**. Deze waarde zal later kan worden verwezen als *key1*.

## <a name="downloading-hello-helper-tool"></a>Hallo helper hulpprogramma te downloaden

1.  Download Hallo helper hulpprogramma van [GitHub](https://github.com/azureadquickstarts/b2c-azureblobstorage-client/archive/master.zip).
2.  Hallo opslaan *B2C-AzureBlobStorage-Client-master.zip* bestand op uw lokale computer.
3.  Uitpakken van inhoud van Hallo B2C-AzureBlobStorage-Client-master.zip-bestand op uw lokale schijf, bijvoorbeeld onder Hallo Hallo **UI-aanpassing-Pack** map. Hiermee maakt u een *B2C-AzureBlobStorage-Client-master* submap.
4.  Open die map en uitpakken van inhoud van het archiefbestand Hallo Hallo *B2CAzureStorageClient.zip* binnen deze.

## <a name="upload-hello-ui-customization-pack-sample-files"></a>Hallo UI-aanpassing-Pack voorbeeldbestanden uploaden

1.  Met Windows Verkenner, Ga toohello map *B2C-AzureBlobStorage-Client-master* zich onder Hallo *UI-aanpassing-Pack* map gemaakt in de vorige sectie Hallo.
2.  Voer Hallo *B2CAzureStorageClient.exe* bestand. Dit programma wordt gewoon alle Hallo-bestanden in Hallo map tooyour storage-account opgeven en CORS-toegang voor deze bestanden geüpload.
3.  Wanneer u wordt gevraagd, geeft: een.  Hallo-naam van uw opslagaccount *storageAccountName*, bijvoorbeeld *contoso369b2c*.
    b.  Hallo primaire toegangssleutel van uw azure-blobopslag *key1*, bijvoorbeeld *contoso369b2c*.
    c.  Hallo-naam van uw opslag blob storage-container *containerName*, bijvoorbeeld *b2c*.
    d.  Hallo pad Hallo *Starter Pack* voorbeeldbestanden bijvoorbeeld *... \B2CTemplates\wingtiptoys*.

Als u Hallo bovenstaande stappen hebt gevolgd, Hallo HTML5 en CSS-bestanden van Hallo *UI-aanpassing-Pack* voor het fictieve bedrijf Hallo **wingtiptoys** wordt nu wijzen tooyour storage-account.  U kunt controleren die Hallo inhoud is geüpload goed door het Hallo gerelateerde container blade in hello Azure-portal te openen. U kunt ook controleren die Hallo inhoud is geüpload correct Hallo door pagina te openen vanuit een browser. Zie voor meer informatie [Azure Active Directory B2C: een helper-hulpprogramma gebruikt toodemonstrate Hallo pagina gebruiker gebruikersinterface (UI) aanpassing functie](active-directory-b2c-reference-ui-customization-helper-tool.md).

## <a name="ensure-hello-storage-account-has-cors-enabled"></a>Zorg dat Hallo storage-account is CORS ingeschakeld

CORS (Cross-Origin Resource Sharing) moet zijn ingeschakeld op uw eindpunt voor Azure AD B2C Premium tooload uw inhoud. Dit komt doordat de inhoud wordt gehost op een ander domein dan Hallo domein Premium Azure AD B2C wordt de behoeve Hallo pagina uit.

tooverify met Hallo opslag zijn voor het hosten van uw inhoud op CORS is ingeschakeld, doorgaan met de Hallo stappen te volgen:

1. Open een browsersessie en navigeer van toohello pagina *unified.html* Hallo volledige URL van de locatie in uw opslagaccount met `https://<storageAccountName>.blob.core.windows.net/<containerName>/unified.html`. Bijvoorbeeld: https://contoso369b2c.blob.core.windows.net/b2c/unified.html.
2. Navigeer toohttp://test-cors.org. Deze site kunt u tooverify die Hallo pagina die u gebruikt CORS ingeschakeld is.  
<!--
![test-cors.org](../../media/active-directory-b2c-customize-ui-of-a-user-journey/test-cors.png)
-->

3. In **externe URL**Hallo volledige URL opgeven voor uw inhoud unified.html en klikt u op **aanvraag verzenden**.
4. Controleren die Hallo-uitvoer in Hallo **resultaten** sectie bevat *XHR status: 200*. Dit geeft aan dat CORS is ingeschakeld.
<!--
![CORS enabled](../../media/active-directory-b2c-customize-ui-of-a-user-journey/cors-enabled.png)
-->
Hallo storage-account moet nu een blob-container met de naam bevatten *b2c* in onze afbeelding met Hallo volgende wingtiptoys sjablonen uit Hallo *Starter Pack*.

<!--
![Correctly configured storage account](../../articles/active-directory-b2c/media/active-directory-b2c-reference-customize-ui-custom/storage-account-final.png)
-->

Hallo beschrijft volgende tabel Hallo doel Hallo boven HTML5-pagina's.

| HTML5-sjabloon | Beschrijving |
|----------------|-------------|
| *phonefactor.HTML* | Deze pagina kan worden gebruikt als een sjabloon voor een multi-factor authentication-pagina. |
| *ResetPassword.HTML* | Deze pagina kan worden gebruikt als een sjabloon voor een wachtwoordpagina vergeten. |
| *selfasserted.HTML* | Deze pagina kan worden gebruikt als een sjabloon voor een aanmeldingspagina sociale account, de aanmeldingspagina van een lokaal account of een lokale account-aanmeldingspagina. |
| *Unified.HTML* | Deze pagina kan worden gebruikt als een sjabloon voor een uniforme registreren of aanmelden pagina. |
| *updateprofile.HTML* | Deze pagina kan worden gebruikt als een sjabloon voor een profiel update-pagina. |

## <a name="add-a-link-tooyour-html5css-templates-tooyour-user-journey"></a>Een koppeling tooyour HTML5/CSS sjablonen tooyour gebruiker reis toevoegen

U kunt een koppeling tooyour HTML5/CSS sjablonen tooyour gebruiker reis toevoegen door een aangepast beleid rechtstreeks te bewerken.

Hallo aangepaste HTML5/CSS sjablonen toouse in uw reis gebruiker hebt opgegeven in een lijst met inhoud definities die kunnen worden gebruikt in deze gebruiker trajecten toobe. Dien een optionele  *<ContentDefinitions>*  XML-element moet worden gedeclareerd onder Hallo  *<BuildingBlocks>*  sectie van het aangepaste beleid XML-bestand.

Hallo volgende tabel wordt beschreven Hallo inhoud definitie-id's wordt herkend door hello Azure AD B2C identiteit ervaring-engine en Hallo-type van pagina's dat is gekoppeld toothem.

| De definitie van de inhoud-id | Beschrijving |
|-----------------------|-------------|
| *API.Error* | **Foutpagina**. Deze pagina wordt weergegeven wanneer een uitzondering of een fout is opgetreden. |
| *API.idpselections* | **Id-provider selectiepagina**. Deze pagina bevat een lijst met de id-providers die gebruiker Hallo uit tijdens het aanmelden kiezen kunnen. Dit zijn de enterprise-id-providers, sociale id-providers zoals Facebook en Google + of lokale accounts (op basis van e-mailadres of de gebruiker naam). |
| *API.idpselections.Signup* | **Selectie van de id-provider voor registratie**. Deze pagina bevat een lijst met providers die gebruiker Hallo uit tijdens de registratie kiezen kunnen van de identiteit. Dit zijn de enterprise-id-providers, sociale id-providers zoals Facebook en Google + of lokale accounts (op basis van e-mailadres of de gebruiker naam). |
| *API.localaccountpasswordreset* | **Wachtwoordpagina vergeten**. Deze pagina bevat een formulier die Hallo de gebruiker heeft toofill tooinitiate hun wachtwoord opnieuw instellen.  |
| *API.localaccountsignin* | **Aanmeldingspagina voor lokaal account**. Deze pagina bevat een formulier aanmelden die gebruiker Hallo heeft toofill in bij het aanmelden met een lokaal account dat is gebaseerd op een e-mailadres of een gebruikersnaam. Hallo formulier kan een tekstinvoervak en wachtwoordvak vermelding bevatten. |
| *API.localaccountsignup* | **Lokaal account aanmeldingspagina**. Deze pagina bevat een aanmeldingsformulier hebt ingevuld die gebruiker Hallo heeft toofill in wanneer u aanmelden voor een lokaal account dat is gebaseerd op een e-mailadres of een gebruikersnaam. Hallo formulier kan andere invoer besturingselementen zoals tekstinvoervak, vermelding wachtwoordvak keuzerondje, één vervolgkeuzelijsten en meervoudige selectie selectievakjes bevatten. |
| *API.phonefactor* | **Multi-factor authentication-pagina**. Gebruikers kunnen hun telefoonnummers (met behulp van de tekst of stem) verifiëren tijdens het registreren of aanmelden op deze pagina. |
| *API.selfasserted* | **De aanmeldpagina sociale account**. Deze pagina bevat een aanmeldingsformulier hebt ingevuld die Hallo de gebruiker heeft toofill in wanneer van een identiteitsprovider van sociale zoals Facebook of Google + aanmelden met behulp van een bestaande account. Deze pagina is vergelijkbaar toohello hierboven aanmeldingspagina met uitzondering van Hallo wachtwoord invoervelden Hallo sociale-account. |
| *API.selfasserted.profileupdate* | **Update profielpagina**. Deze pagina bevat een formulier Hallo kan die gebruiker gebruiken tooupdate hun profiel. Deze pagina is vergelijkbaar toohello hierboven aanmeldingspagina met uitzondering van Hallo wachtwoord invoervelden Hallo sociale-account. |
| *API.signuporsignin* | **Unified registreren of aanmelden pagina**.  Deze pagina verwerkt zowel registreren en aanmelden van gebruikers, die enterprise identiteitsproviders, sociale id-providers zoals Facebook of Google + of lokale accounts kunnen gebruiken.

## <a name="next-steps"></a>Volgende stappen
[Naslaginformatie: Inzicht in hoe aangepaste beleidsregels werken met Hallo identiteit ervaring Framework in B2C](active-directory-b2c-reference-custom-policies-understanding-contents.md)
