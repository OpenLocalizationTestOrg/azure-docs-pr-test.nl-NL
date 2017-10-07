---
title: aaaListing uw toepassing in hello Azure Active Directory-toepassingsgalerie
description: Hoe toolist een toepassing die ondersteuning biedt voor eenmalige aanmelding in Azure Active Directory-galerie Hallo | Microsoft Azure
services: active-directory
documentationcenter: dev-center-name
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: 09ccd3b4645a180059b9a9d502e39f1b8933c988
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="listing-your-application-in-hello-azure-active-directory-application-gallery"></a>Uw toepassing in Azure Active Directory-toepassingsgalerie Hallo aanbieding
een toepassing die ondersteuning biedt voor eenmalige aanmelding bij Azure Active Directory in Hallo toolist [galerie van Azure AD](https://azure.microsoft.com/marketplace/active-directory/all/), Hallo toepassing moet eerst tooimplement Hallo integratie modi te volgen:

* **OpenID Connect** - directe integratie met Azure AD met OpenID Connect voor verificatie en Azure AD toestemming API voor configuratie Hallo. Als u een integratie net begint en SAML biedt geen ondersteuning voor uw toepassing, is dit Hallo aanbevolen modus.
* **SAML** – de toepassing al heeft Hallo mogelijkheid tooconfigure van derden id-providers met Hallo SAML-protocol.

Aanbieding-vereisten voor elke fase zijn hieronder.

## <a name="openid-connect-integration"></a>OpenID Connect-integratie
toointegrate uw toepassing met Azure AD, volgende Hallo [developer instructies](active-directory-authentication-scenarios.md). Vervolgens voltooien Hallo onderstaande vragen en te verzenden toowaadpartners@microsoft.com.

* Geef referenties voor een testtenant of een account met de toepassing die kan worden gebruikt door hello Azure AD-team tootest Hallo-integratie.  
* Bieden instructies over hoe hello Azure AD-team kunt aanmelden en verbinding maken met een exemplaar van Azure AD tooyour toepassing hello met [Azure AD toestemming framework](active-directory-integrating-applications.md#overview-of-the-consent-framework). 
* Geef eventuele verdere instructies nodig zijn voor hello Azure AD in een team tootest eenmalige aanmelding met uw toepassing. 
* Geef Hallo gegevens hieronder:

> Bedrijfsnaam:
> 
> De Website van het bedrijf:
> 
> De naam van de toepassing:
> 
> Beschrijving van de toepassing (maximaal 200 tekens):
> 
> De Website van de toepassing is (informatief):
> 
> Website van de toepassing technische ondersteuning of contactgegevens:
> 
> ID van Hallo toepassing, zoals wordt weergegeven in Hallo App-details https://portal.azure.com:
> 
> Wanneer klanten gaat toosign voor de URL van de toepassing aanmelden en/of kopen Hallo toepassing:
> 
> Kies toothree categorieën voor uw toepassing toobe vermeld in (voor beschikbare categorieën Zie hello Azure Active Directory Marketplace):
> 
> Kleine pictogrammen van toepassing (PNG-bestand, 45px door 45px, effen achtergrondkleur) koppelen:
> 
> Koppelen met grote pictogrammen van toepassing (PNG-bestand, 215px door 215px, effen achtergrondkleur):
> 
> Logo van de toepassing (PNG-bestand, 150px door 122px, transparante achtergrondkleur) koppelen:
> 
> 

## <a name="saml-integration"></a>SAML-integratie
Alle Apps die ondersteuning biedt voor SAML 2.0 kan rechtstreeks worden geïntegreerd met een Azure AD-tenant met behulp van [deze tooadd instructies een aangepaste toepassing](../active-directory-saas-custom-apps.md). Nadat u hebt getest dat de integratie van uw toepassingen met Azure AD werkt, Hallo volgende informatie te verzenden<mailto:waadpartners@microsoft.com>.

* Geef referenties voor een testtenant of een account met de toepassing die kan worden gebruikt door hello Azure AD-team tootest Hallo-integratie.  
* Geef Hallo SAML aanmeldings-URL, URL-verlener (entiteit-ID) en antwoord-URL (assertion consumer-service)-waarden voor uw toepassing, zoals wordt beschreven [hier](../active-directory-saas-custom-apps.md). Als u doorgaans deze waarden als onderdeel van een metagegevensbestand SAML opgeeft, klikt u vervolgens kunt u sturen die ook.
* Geef een korte beschrijving van hoe tooconfigure Azure AD als een id-provider in uw toepassing met behulp van SAML 2.0. Als uw toepassing het configureren van de Azure AD als een id-provider door middel van een administratieve selfserviceportal ondersteunt, vervolgens Controleer Hallo referenties bovenstaande omvatten Hallo mogelijkheid tooset dit up.
* Geef Hallo gegevens hieronder:

> Bedrijfsnaam:
> 
> De Website van het bedrijf:
> 
> De naam van de toepassing:
> 
> Beschrijving van de toepassing (maximaal 200 tekens):
> 
> De Website van de toepassing is (informatief):
> 
> Website van de toepassing technische ondersteuning of contactgegevens:
> 
> Wanneer klanten gaat toosign voor de URL van de toepassing aanmelden en/of kopen Hallo toepassing:
> 
> Kies maximaal toothree categorieën voor uw toepassing toobe vermeld onder (voor beschikbare categorieën Zie Hallo [Azure Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/))):
> 
> Kleine pictogrammen van toepassing (PNG-bestand, 45px door 45px, effen achtergrondkleur) koppelen:
> 
> Koppelen met grote pictogrammen van toepassing (PNG-bestand, 215px door 215px, effen achtergrondkleur):
> 
> Logo van de toepassing (PNG-bestand, 150px door 122px, transparante achtergrondkleur) koppelen:
> 
> 

