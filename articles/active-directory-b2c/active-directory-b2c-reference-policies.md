---
title: 'Azure Active Directory B2C: Ingebouwde beleid | Microsoft Docs'
description: Een onderwerp op Hallo uitbreidbaar beleidsframework van Azure Active Directory B2C en informatie over hoe toocreate verschillende beleidstypen
services: active-directory-b2c
documentationcenter: 
author: sama
manager: mbaldwin
editor: PatAltimore
ms.assetid: 0d453e72-7f70-4aa2-953d-938d2814d5a9
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2017
ms.author: sama
ms.openlocfilehash: 24bb85eba30f888c6ea7d0401e05235e8eb6ea79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-built-in-policies"></a>Azure Active Directory B2C: Ingebouwde beleid


Hallo uitbreidbaar beleidsframework van Azure Active Directory (Azure AD) B2C is Hallo core sterkte van Hallo-service. Volledig beschrijven consumer identiteitservaringen zoals beleidsregels registreren, aanmelden en profiel bewerken. Bijvoorbeeld, kunt een registratiebeleid u toocontrol gedrag door Hallo volgende instellingen configureren:

* Account typen (sociale accounts zoals Facebook) of lokale accounts zoals e-mailadressen die consumenten toosign voor Hallo-toepassing kunnen gebruiken
* Kenmerken (bijvoorbeeld de voornaam, postcode en schoen grootte) toobe verzameld van de consumer Hallo tijdens de registratie
* Gebruik van Azure multi-factor Authentication
* Hallo-uiterlijk van alle aanmeldingspagina 's
* Informatie (dat zich voordoet als claims in een token) die toepassing hello ontvangt wanneer Hallo beleid uitgevoerd is voltooid

U kunt meerdere beleidsregels met verschillende typen in uw tenant maken en gebruiken in uw toepassingen indien nodig. Beleid kunnen opnieuw worden gebruikt in toepassingen. Deze flexibiliteit kunnen ontwikkelaars toodefine en ervaringen van de consument identiteit met minimale of geen wijzigingen tootheir code wijzigen.

Beleidsregels zijn beschikbaar voor gebruik via een eenvoudige developer-interface. Uw toepassing een beleid wordt geactiveerd met behulp van een standaard HTTP-authenticatie-aanvraag (het doorgeven van een parameter van het beleid in Hallo aanvraag) en een aangepaste token als antwoord ontvangt. Hallo enige verschil tussen aanvragen die gebruikmaken van een registratiebeleid en aanvragen die gebruikmaken van een beleid voor aanmelden is bijvoorbeeld Hallo beleidsnaam die wordt gebruikt in 'p' hello queryreeksparameter opgeven:

```

https://login.microsoftonline.com/contosob2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e      // Your registered Application ID
&redirect_uri=https%3A%2F%2Flocalhost%3A44321%2F    // Your registered Reply URL, url encoded
&response_mode=form_post                            // 'query', 'form_post' or 'fragment'
&response_type=id_token
&scope=openid
&nonce=dummy
&state=12345                                        // Any value provided by your application
&p=b2c_1_siup                                       // Your sign-up policy

```

```

https://login.microsoftonline.com/contosob2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e      // Your registered Application ID
&redirect_uri=https%3A%2F%2Flocalhost%3A44321%2F    // Your registered Reply URL, url encoded
&response_mode=form_post                            // 'query', 'form_post' or 'fragment'
&response_type=id_token
&scope=openid
&nonce=dummy
&state=12345                                        // Any value provided by your application
&p=b2c_1_siin                                       // Your sign-in policy

```

Zie voor meer informatie over Hallo beleidsframework [dit blogbericht over Azure AD B2C op Hallo Enterprise Mobility and Security-Blog](http://blogs.technet.com/b/ad/archive/2015/11/02/a-look-inside-azuread-b2c-with-kim-cameron.aspx).

## <a name="create-a-sign-up-or-sign-in-policy"></a>Maak een beleid registreren of aanmelden

Dit beleid verwerkt beide ervaringen consumenten registreren en aanmelden met een configuratie voor één. Consumenten worden geleid omlaag Hallo pad rechts (registreren of aanmelden), afhankelijk van het Hallo-context. Hierin worden ook Hallo inhoud van de tokens die de toepassing hello bij geslaagde aanmelding-ups of aanmeldingen ontvangt.  Een voorbeeld van code voor het registreren of aanmelden beleid Hallo is [beschikbaar hier](active-directory-b2c-devquickstarts-web-dotnet-susi.md).  Het wordt aanbevolen dat u dit beleid via een registratiebeleid en beleid voor aanmelden gebruiken.  

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

## <a name="create-a-sign-up-policy"></a>Een registratiebeleid maken

[!INCLUDE [active-directory-b2c-create-sign-up-policy](../../includes/active-directory-b2c-create-sign-up-policy.md)]

## <a name="create-a-sign-in-policy"></a>Maak een beleid voor aanmelden

[!INCLUDE [active-directory-b2c-create-sign-in-policy](../../includes/active-directory-b2c-create-sign-in-policy.md)]

## <a name="create-a-profile-editing-policy"></a>Maken van een profiel te bewerken van beleid

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

## <a name="create-a-password-reset-policy"></a>Maak een beleid voor wachtwoord opnieuw instellen

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

## <a name="frequently-asked-questions"></a>Veelgestelde vragen

### <a name="how-do-i-link-a-sign-up-or-sign-in-policy-with-a-password-reset-policy"></a>Hoe kan ik een beleid registreren of aanmelden met een beleid voor wachtwoordherstel koppelen?
Wanneer u een beleid registreren of aanmelden (met lokale accounts) maakt, ziet u een **wachtwoord vergeten?** koppeling op de eerste pagina van de Hallo Hallo-ervaring. Op deze koppeling klikt herstellen niet automatisch trigger een wachtwoord beleid. 

In plaats daarvan Hallo foutcode  **`AADB2C90118`**  tooyour app wordt geretourneerd. Uw app moet toohandle deze foutcode door het aanroepen van een specifiek wachtwoord opnieuw instellen van beleid. Zie voor meer informatie een [voorbeeldbestand dat laat Hallo benadering zien van het koppelen van beleidsregels](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-DotNet-SUSI).

### <a name="should-i-use-a-sign-up-or-sign-in-policy-or-a-sign-up-policy-and-a-sign-in-policy"></a>Moet ik een beleid registreren of aanmelden of een registratiebeleid en een beleid voor aanmelden gebruiken?
Het is raadzaam dat u een beleid registreren of aanmelden via een registratiebeleid en een beleid voor aanmelden.  

Hallo registreren of aanmelden beleid heeft meer mogelijkheden dan Hallo aanmelden beleid. Ook kunt u toouse pagina UI-aanpassing en biedt een betere ondersteuning voor lokalisatie. 

beleid voor aanmelden Hello wordt aanbevolen als u niet toolocalize het beleid hoeft, alleen moet secundaire aanpassingsfuncties voor huisstijl en wachtwoord wilt herstellen die zijn ingebouwd in deze.

## <a name="next-steps"></a>Volgende stappen
* [Token, sessie en configuratie voor één aanmelding](active-directory-b2c-token-session-sso.md)
* [E-mailverificatie tijdens registratie consumer uitschakelen](active-directory-b2c-reference-disable-ev.md)

