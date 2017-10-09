---
title: "Azure Active Directory B2C: Token, sessie en configuratie voor één aanmelding | Microsoft Docs"
description: Token, sessie en configuratie voor eenmalige aanmelding in Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: e78e6344-0089-49bf-8c7b-5f634326f58c
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2017
ms.author: swkrish
ms.openlocfilehash: 63325ed97a7363723c97ee3a992046ebb5592662
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-token-session-and-single-sign-on-configuration"></a>Azure Active Directory B2C: Token, sessie en configuratie voor één aanmelding
Deze functie kunt u fijnmazig bepalen, op een [per beleid basis](active-directory-b2c-reference-policies.md), van:

1. De levensduur van beveiligingstokens die door Azure Active Directory (Azure AD) B2C.
2. De levensduur van web application sessies worden beheerd door Azure AD B2C.
3. De indelingen van belangrijke claims in Hallo beveiligingstokens die door Azure AD B2C.
4. Eenmalige aanmelding (SSO) de gedrag voor meerdere apps en beleidsregels in uw B2C-tenant.

U kunt deze functie in uw B2C-tenant als volgt gebruiken:

1. Volg deze stappen te[toohello B2C-functiesblade navigeren](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) op Hallo Azure-portal.
2. Klik op **aanmelden beleid**. *Opmerking: U kunt deze functie op elk beleidstype niet alleen op **aanmelden beleid***.
3. Open een beleid door erop te klikken. Bijvoorbeeld, klikt u op **B2C_1_SiIn**.
4. Klik op **bewerken** Hallo boven aan het Hallo-blade.
5. Klik op **Token, sessie & eenmalige aanmelding config**.
6. Breng de gewenste wijzigingen. Meer informatie over de beschikbare eigenschappen in de volgende secties.
7. Klik op **OK**.
8. Klik op **opslaan** op Hallo Hallo blade bovenaan.

## <a name="token-lifetimes-configuration"></a>Configuratie van de levensduur van token
Azure AD B2C ondersteunt Hallo [OAuth 2.0-protocol voor autorisatie](active-directory-b2c-reference-protocols.md) voor het inschakelen van beveiligde toegang tot resources tooprotected. tooimplement deze ondersteuning, Azure AD B2C verzendt verschillende [beveiligingstokens](active-directory-b2c-reference-tokens.md). Dit zijn kunt u toomanage levensduur van beveiligingstokens die door Azure AD B2C Hallo-eigenschappen:

* **Toegang tot & ID token levensduur (minuten)**: Hallo levensduur van Hallo OAuth 2.0 bearer-token gebruikt toogain toegang tooa beveiligde resource. Azure AD B2C geeft alleen ID tokens op dit moment. Deze waarde bijvoorbeeld tooaccess tokens eveneens van toepassing wanneer we ondersteuning voor deze toevoegen.
  * Standaard = 60 minuten.
  * Minimaal (inclusief) = 5 minuten.
  * Maximum (inclusief) = 1440 minuten.
* **Vernieuwen van de levensduur van token (dagen)**: Hallo maximale periode waarvoor een vernieuwingstoken gebruikte tooacquire mag een nieuwe toegang of het token ID (en desgewenst een nieuwe vernieuwingstoken, als uw toepassing hello had gekregen `offline_access` scope).
  * Standaardinstelling = 14 dagen.
  * Minimaal (inclusief) = 1 dag.
  * Maximum (inclusief) = 90 dagen.
* **Vernieuwen van de levensduur van token verschuivende venster (dagen)**: nadat deze tijd periode verstreken Hallo-gebruiker gedwongen toore is-verificatie, ongeacht de geldigheidsperiode Hallo van Hallo meest recente vernieuwingstoken verkregen door de toepassing hello. Kan alleen worden opgegeven als Hallo switch is ingesteld, te**dat wordt begrensd**. Moet toobe groter dan of gelijk zijn toohello **levensduur van token vernieuwen (dagen)** waarde. Als Hallo switch is ingesteld, te**Unbounded**, u niet een bepaalde waarde opgeven.
  * Standaardwaarde = 90 dagen.
  * Minimaal (inclusief) = 1 dag.
  * Maximum (inclusief) = 365 dagen.

Dit zijn enkele gebruiksvoorbeelden die u kunt inschakelen met behulp van deze eigenschappen:

* Toestaan dat een toostay gebruiker is aangemeld bij een mobiele toepassing voor onbepaalde tijd, zolang hij of zij voortdurend actief op Hallo-toepassing is. U kunt dit doen door de instelling Hallo **vernieuwen verschuivende venster levensduur van token (dagen)** te schakelen**Unbounded** in uw beleid voor aanmelden.
* Voldoen aan uw branche beveiliging en naleving door in te stellen Hallo juiste-token levensduur.

    > [!NOTE]
    > Deze instellingen zijn niet beschikbaar voor wachtwoord opnieuw instellen van beleidsregels.
    > 
    > 

## <a name="token-compatibility-settings"></a>Token compatibiliteitsinstellingen
Er claims van de tooimportant opmaak wijzigingen aangebracht in beveiligingstokens die door Azure AD B2C. Dit is gedaan tooimprove onze support standaardprotocol en voor een betere compatibiliteit met bibliotheken van de identiteit van de derde partij. Echter tooavoid verbreken bestaande apps, we gemaakt Hallo eigenschappen tooallow klanten tooopt-in naar behoefte te volgen:

* **Certificaatverlener (iss) claim**: dit hello Azure AD B2C-tenant die token Hallo uitgegeven identificeert.
  * `https://login.microsoftonline.com/{B2C tenant GUID}/v2.0/`: Dit is de standaardwaarde Hallo.
  * `https://login.microsoftonline.com/tfp/{B2C tenant GUID}/{Policy ID}/v2.0/`: Met deze waarde bevat id's voor zowel Hallo B2C-tenant en gebruikt in de tokenaanvraag Hallo Hallo-beleid. Als uw app of bibliotheek Azure AD B2C toobe compatibel zijn met de Hallo moet [OpenID Connect detectie 1.0-specificatie](http://openid.net/specs/openid-connect-discovery-1_0.html), gebruikt deze waarde.
* **Onderwerpnaam (sub) claim**: dit Hallo entiteit, dat wil zeggen, Hallo gebruiker voor welke Hallo token informatie asserts identificeert.
  * **ObjectID**: dit is de standaardwaarde Hallo. Het object-ID van gebruiker in de map Hallo HALLO hallo gevuld in Hallo `sub` claim in Hallo-token.
  * **Niet ondersteund**: dit is alleen beschikbaar voor neerwaartse compatibiliteit en het is raadzaam dat u overschakelt naar te**ObjectID** zodra u zich kunt.
* **Claim die beleids-ID vertegenwoordigt**: Hiermee wordt aangegeven Hallo claimtype in welke Hallo beleids-ID gebruikt in de tokenaanvraag hello wordt gevuld.
  * **TFP**: dit is de standaardwaarde Hallo.
  * **ACR**: dit is alleen beschikbaar voor neerwaartse compatibiliteit en het is raadzaam dat u overschakelt naar te`tfp` zodra u zich kunt.

## <a name="session-behavior"></a>Sessie-gedrag
Azure AD B2C ondersteunt Hallo [OpenID Connect-verificatieprotocol](active-directory-b2c-reference-oidc.md) voor het inschakelen van beveiligde aanmelding tooweb toepassingen. Dit zijn kunt u toomanage web application sessies Hallo-eigenschappen:

* **Sessie-levensduur (minuten) van de Web-app**: Hallo levensduur van Azure AD B2C sessiecookie opgeslagen op de browser van de gebruiker van het Hallo na een geslaagde verificatie.
  * Standaardinstelling = 1440 minuten.
  * Minimaal (inclusief) = 15 minuten.
  * Maximum (inclusief) = 1440 minuten.
* **Web-app sessietime-out**: als deze switch is ingesteld, te**Absolute**, Hallo gebruiker is gedwongen toore-verifiëren na de tijd die is opgegeven door Hallo **Web-app sessie levensduur (minuten)** is verstreken. Als deze switch is ingesteld, te**rollend** (hello standaardinstelling), Hallo gebruiker blijft aangemeld als gebruiker Hallo voortdurend actief in uw webtoepassing is.

Dit zijn enkele gebruiksvoorbeelden die u kunt inschakelen met behulp van deze eigenschappen:

* Voldoen aan uw branche beveiliging en naleving door in te stellen geschikte websessie toepassing hello levensduur.
* Herauthenticatie na een gegeven periode tijdens gebruikersinteractie met hoogwaardige beveiliging deel uit van uw webtoepassing te forceren. 

    > [!NOTE]
    > Deze instellingen zijn niet beschikbaar voor wachtwoord opnieuw instellen van beleidsregels.
    > 
    > 

## <a name="single-sign-on-sso-configuration"></a>Configuratie van eenmalige aanmelding (SSO)
Als u meerdere toepassingen en het beleid in uw B2C-tenant hebt, kunt u de interactie van gebruikers beheren onder te brengen met behulp van Hallo **configuratie voor één aanmelding** eigenschap. U kunt instellen dat Hallo eigenschap tooone Hallo volgende instellingen:

* **Tenant**: dit is de standaardinstelling Hallo. Met deze instelling kan meerdere toepassingen en beleidsregels in uw B2C-tenant tooshare Hallo dezelfde gebruikerssessie. Bijvoorbeeld wanneer een gebruiker zich in een toepassing, Contoso winkelen hij of zij kan ook naadloos Meld u aan bij een andere afbeelding, Contoso faculteit, bij toegang tot deze.
* **Toepassing**: Hiermee kunt u toomaintain een gebruikerssessie uitsluitend bedoeld is voor een toepassing, onafhankelijk van andere toepassingen. Bijvoorbeeld, als u wilt dat Hallo gebruiker toosign in tooContoso faculteit (Hello dezelfde referenties), zelfs als hij of zij is al aangemeld bij Contoso winkelen, een andere toepassing op Hallo dezelfde B2C-tenant. 
* **Beleid**: Hiermee kunt u toomaintain een gebruikerssessie uitsluitend bedoeld is voor een beleid, onafhankelijk van het Hallo-toepassingen met behulp van deze. Bijvoorbeeld, als Hallo gebruiker is al aangemeld en een multi-factor authentication (MFA) stap voltooid, kan hij of zij krijgen toegang toohigher beveiliging delen van meerdere toepassingen zolang Hallo sessie gekoppeld toohello beleid verloopt niet.
* **Uitgeschakelde**: dit Hallo gebruiker toorun via Hallo gehele gebruiker reis zorgt ervoor dat op elke uitvoering van het Hallo-beleid. Bijvoorbeeld, kunnen hierdoor meerdere gebruikers toosign tooyour toepassing (in een gedeelde bureaublad scenario), zelfs terwijl een enkele gebruiker aangemeld gedurende de hele tijd Hallo blijft.

    > [!NOTE]
    > Deze instellingen zijn niet beschikbaar voor wachtwoord opnieuw instellen van beleidsregels.
    > 
    > 

