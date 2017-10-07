---
title: 'Azure Active Directory B2C: Hulpprogramma Page UI aanpassing helper | Microsoft Docs'
description: Een hulpprogramma helper toodemonstrate Hallo pagina UI-aanpassing functie gebruikt in Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: ae935d52-3520-4a94-b66e-b35bb40e7514
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: swkrish
ms.openlocfilehash: 5137ac112019369b4244a925df1acb96fefb758f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-a-helper-tool-used-toodemonstrate-hello-page-user-interface-ui-customization-feature"></a>Azure Active Directory B2C: Een helper-hulpprogramma gebruikt toodemonstrate Hallo pagina gebruiker gebruikersinterface (UI) functie voor het aanpassen
Dit artikel is een aanvullende toohello [belangrijkste UI aanpassing artikel](active-directory-b2c-reference-ui-customization.md) in Azure Active Directory (Azure AD) B2C. Hallo volgende stappen beschrijven hoe tooexercise pagina UI-aanpassing functie Hallo met behulp van HTML en CSS voorbeeldinhoud die we hebt opgegeven.

## <a name="get-an-azure-ad-b2c-tenant"></a>Een Azure AD B2C-tenant verkrijgen
Voordat u alles aanpassen kunt, moet u te[een Azure AD B2C-tenant verkrijgen](active-directory-b2c-get-started.md) als u er nog geen hebt.

## <a name="create-a-sign-up-or-sign-in-policy"></a>Maak een beleid registreren of aanmelden
Hallo voorbeeldinhoud we bieden kan worden gebruikt toocustomze twee pagina's in een [registreren of aanmelden beleid](active-directory-b2c-reference-policies.md): Hallo [unified aanmeldingspagina](active-directory-b2c-reference-ui-customization.md) en Hallo [zelf aangenomen kenmerken pagina](active-directory-b2c-reference-ui-customization.md). Wanneer [maken van uw beleid registreren of aanmelden](active-directory-b2c-reference-policies.md#create-a-sign-up-or-sign-in-policy), Voeg het lokale Account (e-mailadres), Facebook, Google en Microsoft als **identiteitsproviders**. Deze zijn alleen IDPs die onze voorbeeld HTML-inhoud accepteert Hallo.  U kunt ook een subset van deze IDPs toevoegen als u wenst.

## <a name="register-an-application"></a>Een toepassing registreren
U moet te[een toepassing registreren](active-directory-b2c-app-registration.md) in uw B2C-tenant die gebruikte tooexecute uw beleid kan worden. Na de registratie van uw toepassing hebt u een aantal opties die u uitvoert het registratiebeleid tooactually kunt gebruiken:

* Een hello Azure AD B2C toepassingen voor snel starten in het gedeelte Hallo 'aan de slag weergegeven' bouwen [aanmelden en aanmelden van gebruikers in uw toepassingen](active-directory-b2c-overview.md#get-started).
* Gebruik Hallo vooraf gemaakte [Azure AD B2C Playground](https://aadb2cplayground.azurewebsites.net) toepassing. Als u toouse Hallo playground kiest, moet u een toepassing registreren in uw B2C-tenant met behulp van Hallo **omleidings-URI** `https://aadb2cplayground.azurewebsites.net/`.
* Gebruik Hallo **nu uitvoeren** knop op uw beleid in Hallo [Azure-portal](https://portal.azure.com/).

## <a name="customize-your-policy"></a>Het beleid aanpassen
toocustomize hello uiterlijk van uw beleid, moet u toofirst HTML en CSS-bestanden met behulp van specifieke conventies Hallo van Azure AD B2C maken. Vervolgens kunt u uw statische inhoud tooa openbaar toegankelijke locatie zodat Azure AD B2C toegang hebt tot het uploaden. Dit kan zijn eigen speciale webserver, Azure Blob Storage, Azure Content Delivery Network of elke andere statische resource-hosting provider. Hallo enige vereisten zijn dat uw inhoud beschikbaar via HTTPS is en kan worden geopend met behulp van CORS. Zodra u hebt uw statische inhoud op Hallo web blootgesteld, kunt u uw beleid toopoint toothis locatie en aanwezig die inhoud tooyour klanten kunt bewerken. Hallo [belangrijkste UI aanpassing artikel](active-directory-b2c-reference-ui-customization.md) een gedetailleerde beschrijving van de werking van de functie voor het aanpassen van hello Azure AD B2C.

Voor Hallo doel van deze zelfstudie, hebt we al enkele voorbeeldinhoud gemaakt en wordt gehost op Azure Blob Storage. Hallo voorbeeldinhoud is een zeer eenvoudige aanpassing in Hallo thema van onze fictieve bedrijf, 'Wingtip Toys'. tootry uit in uw eigen beleid als volgt te werk:

1. Meld u aan de tenant tooyour op Hallo [Azure-portal](https://portal.azure.com/) en navigeer toohello B2C-functiesblade.
2. Klik op **registreren of aanmelden beleid** en klik vervolgens op het beleid (bijvoorbeeld ' b2c\_1\_aanmelding\_up\_aanmelding\_in ').
3. Klik op **Page UI-aanpassing** en vervolgens **Unified registreren of aanmelden pagina**.
4. Wisselknop Hallo **gebruik aangepaste pagina** te schakelen**Ja**. In Hallo **aangepaste pagina URI** veld `https://wingtiptoysb2c.blob.core.windows.net/b2c/wingtip/unified.html`. Klik op **OK**.
5. Klik op **aanmeldpagina voor lokaal account**. Wisselknop Hallo **aangepaste sjabloon gebruiken** te schakelen**Ja**. In Hallo **aangepaste pagina URI** veld `https://wingtiptoysb2c.blob.core.windows.net/b2c/wingtip/selfasserted.html`.
6. Herhalingen Hallo dezelfde stap voor Hallo **sociale account aanmeldingspagina**.
   Klik op **OK** tweemaal tooclose Hallo UI aanpassing blades.
7. Klik op **Opslaan**.

U kunt nu uw aangepaste beleid uitproberen. U kunt uw eigen toepassing of hello Azure AD B2C-playground gebruiken als u wilt, maar u kunt ook gewoon Hallo **nu uitvoeren** opdracht blade Hallo-beleid. Selecteer uw toepassing in de vervolgkeuzelijst Hallo en kies Hallo juiste omleidings-URI. Klik op Hallo **nu uitvoeren** knop. Een nieuw browsertabblad geopend en kunt u uitvoeren via Hallo gebruikerservaring zich registreert voor uw toepassing met nieuwe inhoud aanwezig Hallo!

## <a name="upload-hello-sample-content-tooazure-blob-storage"></a>Hallo voorbeeld Blob Storage tooAzure inhoud uploaden
Als u toouse Azure Blob Storage toohost wilt uw pagina-inhoud, kunt u uw eigen storage-account maken en gebruiken van onze B2C helper hulpprogramma tooupload uw bestanden.

### <a name="create-a-storage-account"></a>Een opslagaccount maken
1. Meld u aan toohello [Azure-portal](https://portal.azure.com/).
2. Klik op **+ nieuw** > **gegevens en opslag** > **opslagaccount**. U moet een Azure-abonnement toocreate een Azure Blob Storage-account. U kunt aanmelden met een gratis proefversie op Hallo [Azure-website](https://azure.microsoft.com/pricing/free-trial/).
3. Geef een **naam** voor Hallo storage-account (bijvoorbeeld ' contoso') en kies Hallo benodigde selecties voor **prijscategorie**, **resourcegroep** en  **Abonnement**. Zorg ervoor dat u Hallo hebt **pincode tooStartboard** optie ingeschakeld. Klik op **Create**.
4. Ga terug toohello Startboard en klikt u op Hallo storage-account dat u zojuist hebt gemaakt.
5. In Hallo **samenvatting** sectie, klikt u op **Containers**, en klik vervolgens op **+ toevoegen**.
6. Geef een **naam** voor Hallo-container (bijvoorbeeld ' b2c') en selecteer **Blob** als Hallo **toegangstype**. Klik op **OK**.
7. Hallo-container die u hebt gemaakt wordt weergegeven in de lijst Hallo op Hallo **Blobs** blade. Schrijf Hallo-URL van de container Hallo; bijvoorbeeld: het certificaat van echtheid te`https://contoso.blob.core.windows.net/b2c`. Sluit Hallo **Blobs** blade.
8. Klik op de blade opslagaccount hello **sleutels** en schrijf Hallo waarden Hallo **Opslagaccountnaam** en **primaire toegangssleutel** velden.

> [!NOTE]
> **Primaire toegangssleutel** is een belangrijke beveiligingsreferentie.
> 
> 

### <a name="download-hello-helper-tool-and-sample-files"></a>Hallo helper hulpprogramma's en voorbeeld-bestanden downloaden
U kunt downloaden Hallo [Azure Blob Storage helper hulpprogramma's en voorbeeld-bestanden als een ZIP-bestand](https://github.com/azureadquickstarts/b2c-azureblobstorage-client/archive/master.zip) of het klonen van GitHub:

```
git clone https://github.com/azureadquickstarts/b2c-azureblobstorage-client
```

Deze bibliotheek bevat een `sample_templates\wingtip` directory waarin voorbeeld HTML, CSS en afbeeldingen. Voor deze sjablonen tooreference uw eigen Azure Blob Storage-account, moet u tooedit Hallo HTML-bestanden. Open `unified.html` en `selfasserted.html` en Vervang alle exemplaren van `https://localhost` met Hallo-URL van uw eigen container die u hebt genoteerd in de vorige stappen Hallo. Hallo absolute pad van Hallo HTML-bestanden omdat in dit geval Hallo HTML kan worden geleverd door Azure AD, onder Hallo domein moet u `https://login.microsoftonline.com`.

### <a name="upload-hello-sample-files"></a>Hallo voorbeeldbestanden uploaden
In dezelfde opslagplaats Hallo, pak `B2CAzureStorageClient.zip` en Voer Hallo `B2CAzureStorageClient.exe` binnen het bestand. Dit programma wordt gewoon alle Hallo-bestanden in Hallo map tooyour storage-account opgeven en CORS-toegang voor deze bestanden geüpload. Als u Hallo bovenstaande stappen hebt gevolgd, wordt Hallo HTML en CSS-bestanden nu verwijzen tooyour storage-account. Houd er rekening mee dat Hallo naam van uw opslagaccount is Hallo-onderdeel dat voorafgaat aan `blob.core.windows.net`, bijvoorbeeld `contoso`. U kunt controleren dat Hallo inhoud correct is geüpload door de tooaccess `https://{storage-account-name}.blob.core.windows.net/{container-name}/wingtip/unified.html` in een browser. Ook gebruiken [http://test-cors.org/](http://test-cors.org/) toomake ervoor Hallo inhoud is nu CORS is ingeschakeld. (Zoek naar ' XHR status: 200 ' in hello resultaat.)

### <a name="customize-your-policy-again"></a>Het beleid opnieuw aanpassen
Nu dat u hebt geüpload Hallo voorbeeld inhoud tooyour eigen storage-account, moet u uw tooreference registratiebeleid bewerken het. Herhaal de stappen van Hallo Hallo ['Aanpassen van uw beleid'](#customize-your-policy) sectie hierboven, met behulp van URL's van uw eigen opslagaccount. Bijvoorbeeld: Hallo locatie van uw `unified.html` bestand `<url-of-your-container>/wingtip/unified.html`.

Nu kunt u Hallo **nu uitvoeren** knop of uw eigen toepassing tooexecute uw beleid voor opnieuw. Hallo resultaat moet zoekt u naar bijna hetzelfde hello dezelfde--u hebt gebruikt Hallo dezelfde HTML en CSS steekproef in beide gevallen. Echter uw beleid nu verwijzen naar uw eigen exemplaar van Azure Blob Storage en u gratis tooedit en neem Hallo-bestanden opnieuw als u uploaden. Voor meer informatie over het aanpassen van hello HTML en CSS, Raadpleeg toohello [belangrijkste UI aanpassing artikel](active-directory-b2c-reference-ui-customization.md).

