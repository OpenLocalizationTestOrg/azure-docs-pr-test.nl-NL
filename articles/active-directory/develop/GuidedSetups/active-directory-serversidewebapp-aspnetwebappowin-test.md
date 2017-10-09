---
title: aaaAzure AD v2 ASP.NET Web Server aan de slag - Test | Microsoft Docs
description: Implementeren van Microsoft-aanmeldingspagina op een ASP.NET-oplossing met een traditioneel browser gebaseerde webtoepassing met behulp van standaard OpenID Connect
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 99c7525b9146605142180962fc2a61b3c953c064
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a>Testen van uw code

Druk op `F5` toorun uw project in Visual Studio. Hallo browser openen en u te sturen*http://localhost: {poort}* Hier ziet u Hallo *aanmelden met Microsoft* knop. Opwekken en klikt u op het toosign in.

Wanneer u bent klaar tootest, een werk- of schoolaccount (Azure Active Directory) of een persoonlijke (live.com, outlook.com) account toosign in gebruik. 

![Aanmelden met Microsoft-browservenster](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin.png)

![Aanmelden met Microsoft-browservenster](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin2.png)

#### <a name="expected-results"></a>Verwachte resultaten
Hallo-gebruiker is na het aanmelden, omgeleide toohello startpagina van de website die HTTPS-URL opgegeven in uw toepassing registratie-informatie in de Portal voor registratie van Microsoft-toepassing hello Hallo. Deze pagina wordt nu *Hallo {User}* en een koppeling toosign-out en een koppeling toosee Hallo claims van de gebruiker – dit is een koppeling toohello autoriseren controller eerder hebt gemaakt.

### <a name="see-users-claims"></a>Zie de claims van de gebruiker
Selecteer Hallo hyperlink toosee Hallo claims van de gebruiker. Dit leidt u toohello controller en de weergave die alleen beschikbaar toousers die worden geverifieerd.

#### <a name="expected-results"></a>Verwachte resultaten
 Hier ziet u een tabel met Hallo basiseigenschappen van Hallo geregistreerde gebruiker:

| Eigenschap | Waarde | Beschrijving|
|---|---|---|
| Naam | {De volledige gebruikersnaam} | de voor- en achternaam van de gebruiker Hallo
|Gebruikersnaam | <span>user@domain.com</span>| Hallo gebruikersnaam gebruikt tooidentify Hallo geregistreerde gebruiker
| Onderwerp| {Onderwerp}|Een tekenreeks toouniquely Hallo gebruikersaanmelding op Hallo web identificeren|
| Tenant-id| {Guid}| Een *guid* toouniquely vertegenwoordigen de Azure Active Directory-organisatie van de gebruiker van het Hallo.|

Bovendien ziet u een tabel met inbegrip van alle gebruikersclaims in verificatieaanvraag opgenomen. Voor een lijst van alle claims in een Token Id en de uitleg raadpleegt u dit [artikel](https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims "lijst van Claims in Token Id").


### <a name="test-accessing-a-method-that-has-an-authorize-attribute-optional"></a>Test een methode die heeft toegang tot een *[autoriseren]* kenmerk (optioneel)
In deze stap maakt test u toegang tot Hallo geverifieerde domeincontroller als anonieme gebruiker:<br/>
Selecteer Hallo koppeling toosign-out Hallo gebruikers- en afmelden voltooid Hallo-proces.<br/>
Typ nu in uw browser http://localhost: {poort} / tooaccess uw domeincontroller die is beveiligd met Hallo geverifieerde `[Authorize]` kenmerk

#### <a name="expected-results"></a>Verwachte resultaten
U ontvangt Hallo prompt waarvoor u tooauthenticate toosee Hallo weergeven.

## <a name="additional-information"></a>Aanvullende informatie

<!--start-collapse-->
### <a name="protect-your-entire-web-site"></a>Beveiligen van uw hele website
tooprotect uw hele website toevoegen Hallo `AuthorizeAttribute` te`GlobalFilters` in `Global.asax` `Application_Start` methode:

```csharp
GlobalFilters.Filters.Add(new AuthorizeAttribute());
```
<!--end-collapse-->

<div></div>
<br/>

> [!NOTE]
> **Hoe toorestrict gebruikers slechts één organisatie toosign in tooyour toepassing**

> Standaard persoonlijke accounts (waaronder outlook.com, live.com en anderen), evenals een werk- en schoolaccounts accounts van een bedrijf of organisatie die is geïntegreerd met Azure Active Directory kunnen aanmelden tooyour toepassing. 

> Als u wilt dat uw toepassing tooaccept aanmeldingen van slechts één Azure Active Directory-organisatie, vervangt u Hallo `Tenant` parameter in *web.config* van `Common` toohello tenantnaam van de organisatie Hallo-voorbeeld *contoso.onmicrosoft.com*. Daarna wijzigen Hallo `ValidateIssuer` argument in uw *OWIN-Opstartklasse* te`true`.

> gebruikers uit alleen een lijst met specifieke organisaties tooallow ingesteld `ValidateIssuer` tootrue en gebruik Hallo `ValidIssuers` parameter toospecify een lijst met organisaties.

> Een andere optie is een aangepaste methode tooimplement toovalidate Hallo uitgevers van certificaten met de parameter IssuerValidator. Voor meer informatie over `TokenValidationParameters`, Zie [dit](https://msdn.microsoft.com/library/system.identitymodel.tokens.tokenvalidationparameters.aspx "TokenValidationParameters MSDN-artikel") MSDN-artikel.

