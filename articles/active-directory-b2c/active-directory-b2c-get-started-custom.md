---
title: 'Azure Active Directory B2C: Aan de slag met aangepast beleid | Microsoft Docs'
description: Hoe tooget de slag met Azure Active Directory B2C aangepast beleid
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 658c597e-3787-465e-b377-26aebc94e46d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: joroja;parahk;gsacavdm
ms.openlocfilehash: 5ee133806395cddf18682769a6cad149889d82d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-get-started-with-custom-policies"></a>Azure Active Directory B2C: Aan de slag met aangepast beleid

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Nadat u de stappen in dit artikel Hallo hebt voltooid, het aangepaste beleid 'lokale account' ondersteunt registreren of aanmelden via een e-mailadres en wachtwoord. Ook bereidt u uw omgeving voor het toevoegen van de id-providers (zoals Facebook of Azure Active Directory). We raden u deze stappen voordat u lezen over andere maakt gebruik van Azure Active Directory (Azure AD) B2C identiteit ervaring Framework Hallo toocomplete.

## <a name="prerequisites"></a>Vereisten

Voordat u doorgaat, zorg ervoor dat u hebt een Azure AD B2C-tenant een container voor alle gebruikers, apps en beleidsregels is. Als u nog geen een hebt, moet u deze te[een Azure AD B2C-tenant maken](active-directory-b2c-get-started.md). We raden raden alle ontwikkelaars toocomplete hello Azure AD B2C-scenario's voor ingebouwde beleid en hun toepassingen configureren met ingebouwde beleid voordat u doorgaat. Uw toepassingen werken met beide soorten beleid wanneer u een kleine wijziging toohello beleid naam tooinvoke Hallo aangepast beleid hebt gemaakt.

>[!NOTE]
>tooaccess aangepast beleid bewerkt, moet u een geldige Azure-abonnement gekoppelde tooyour-tenant. Als u nog niet hebt [uw Azure AD B2C-tenant tooan Azure-abonnement gekoppeld](active-directory-b2c-how-to-enable-billing.md) of uw Azure-abonnement is uitgeschakeld, Hallo identiteit ervaring Framework knop niet beschikbaar.

## <a name="add-signing-and-encryption-keys-tooyour-b2c-tenant-for-use-by-custom-policies"></a>Ondertekening en versleuteling sleutels tooyour B2C-tenant voor gebruik door het aangepaste beleid toevoegen

1. Open Hallo **identiteit ervaring Framework** blade in de instellingen van uw Azure AD B2C-tenant.
2. Selecteer **beleid sleutels** tooview Hallo sleutels die beschikbaar zijn in uw tenant.
3. Maak B2C_1A_TokenSigningKeyContainer als deze niet bestaat:<br>
    a. Selecteer **Toevoegen**. <br>
    b. Selecteer **genereren**.<br>
    c. Voor **naam**, gebruik `TokenSigningKeyContainer`. <br> 
    Hallo voorvoegsel `B2C_1A_` kunnen automatisch worden toegevoegd.<br>
    d. Voor **sleuteltype**, gebruik **RSA**.<br>
    e. Voor **datums**, Hallo standaardwaarden gebruiken. <br>
    f. Voor **sleutelgebruik**, gebruik **handtekening**.<br>
    g. Selecteer **Maken**.<br>
4. Maak B2C_1A_TokenEncryptionKeyContainer als deze niet bestaat:<br>
 a. Selecteer **Toevoegen**.<br>
 b. Selecteer **genereren**.<br>
 c. Voor **naam**, gebruik `TokenEncryptionKeyContainer`. <br>
   Hallo voorvoegsel `B2C_1A`_ kunnen automatisch worden toegevoegd.<br>
 d. Voor **sleuteltype**, gebruik **RSA**.<br>
 e. Voor **datums**, Hallo standaardwaarden gebruiken.<br>
 f. Voor **sleutelgebruik**, gebruik **versleuteling**.<br>
 g. Selecteer **Maken**.<br>
5. B2C_1A_FacebookSecret maken. <br>
Als u al een geheim Facebook-toepassing hebt, kunt u deze als een tenant van de belangrijkste tooyour beleid toevoegen. Anders moet u Hallo sleutel maken met de aanduidingswaarde van een tijdelijke zodat het beleid gevalideerd.<br>
 a. Selecteer **Toevoegen**.<br>
 b. Voor **opties**, gebruik **handmatige**.<br>
 c. Voor **naam**, gebruik `FacebookSecret`. <br>
 Hallo voorvoegsel `B2C_1A_` kunnen automatisch worden toegevoegd.<br>
 d. In Hallo **geheim** Voer uw FacebookSecret van developers.facebook.com of `0` als tijdelijke aanduiding. *Dit is geen uw Facebook-app-ID.* <br>
 e. Voor **sleutelgebruik**, gebruik **handtekening**. <br>
 f. Selecteer **maken** en Bevestig maken.

## <a name="register-identity-experience-framework-applications"></a>Identiteit ervaring Framework-toepassingen registreren

Azure AD B2C, moet u tooregister twee extra toepassingen die worden gebruikt door het Hallo-engine toosign up en meld u aan gebruikers.

>[!NOTE]
>U moet twee toepassingen maken die inschakelen aanmelden via lokale accounts: IdentityExperienceFramework (een web-app) en ProxyIdentityExperienceFramework (een systeemeigen app) met de machtiging van Hallo IdentityExperienceFramework app overgedragen. Lokale accounts bestaan alleen in uw tenant. Uw gebruikers zich aanmelden met een uniek e-mailadres en wachtwoord combinatie tooaccess uw toepassingen tenant is geregistreerd.

### <a name="create-hello-identityexperienceframework-application"></a>Hallo IdentityExperienceFramework toepassing maken

1. In Hallo [Azure-portal](https://portal.azure.com), schakel over naar Hallo [context van uw Azure AD B2C-tenant](active-directory-b2c-navigate-to-b2c-context.md).
2. Open Hallo **Azure Active Directory** blade (geen Hallo **Azure AD B2C** blade). Mogelijk moet u tooselect **meer Services** toofind deze.
3. Selecteer **App registraties**.
4. Selecteer **registratie van de nieuwe toepassing**.
   * Voor **naam**, gebruik `IdentityExperienceFramework`.
   * Voor **toepassingstype**, gebruik **Web-app/API**.
   * Voor **aanmeldings-URL**, gebruik `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`, waarbij `yourtenant` is de domeinnaam van uw Azure AD B2C-tenant.
5. Selecteer **Maken**.
6. Zodra deze is gemaakt, selecteert u de toepassing hello nieuw gemaakte **IdentityExperienceFramework**.<br>
   * Selecteer **eigenschappen**.<br>
   * Hallo toepassings-ID kopiëren en opslaan voor later.

### <a name="create-hello-proxyidentityexperienceframework-application"></a>Hallo ProxyIdentityExperienceFramework toepassing maken

1. Selecteer **App registraties**.
1. Selecteer **registratie van de nieuwe toepassing**.
   * Voor **naam**, gebruik `ProxyIdentityExperienceFramework`.
   * Voor **toepassingstype**, gebruik **systeemeigen**.
   * Voor **omleidings-URI**, gebruik `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`, waarbij `yourtenant` is uw Azure AD B2C-tenant.
1. Selecteer **Maken**.
1. Zodra deze is gemaakt, selecteert u de toepassing hello **ProxyIdentityExperienceFramework**.<br>
   * Selecteer **eigenschappen**. <br>
   * Hallo toepassings-ID kopiëren en opslaan voor later.
1. Selecteer **vereist machtigingen**.
1. Selecteer **Toevoegen**.
1. Selecteer **selecteert u een API**.
1. Zoeken naar Hallo naam IdentityExperienceFramework. Selecteer **IdentityExperienceFramework** in Hallo resultaten en klik vervolgens op **Selecteer**.
1. Schakel het selectievakje Hallo naast te**toegang IdentityExperienceFramework**, en klik vervolgens op **Selecteer**.
1. Selecteer **gedaan**.
1. Selecteer **machtiging verlenen**, en bevestig vervolgens door te selecteren **Ja**.

## <a name="download-starter-pack-and-modify-policies"></a>Starter pack downloaden en wijzigen van beleid

Aangepaste beleidsregels zijn een reeks XML-bestanden die toobe geüpload tooyour Azure AD B2C-tenant moeten. We bieden starter packs tooget u snel gaan. Elk pack starter in Hallo volgende lijst bevat Hallo kleinste aantal technische profielen en gebruiker trajecten vereist tooachieve Hallo scenario's beschreven:
 * LocalAccounts. Hallo-gebruik van lokale accounts alleen ingeschakeld.
 * SocialAccounts. Maakt gebruik van Hallo van sociale (of federatieve)-accounts.
 * **SocialAndLocalAccounts**. We gebruiken dit bestand voor Hallo scenario.
 * SocialAndLocalAccountsWithMFA. Opties voor sociale, lokaal en multi-Factor Authentication zijn hier opgenomen.

Elke pack starter bevat:

* Hallo [base bestand](active-directory-b2c-overview-custom.md#policy-files) van Hallo-beleid. Enkele wijzigingen zijn vereist toohello base.
* Hallo [extensiebestand](active-directory-b2c-overview-custom.md#policy-files) Hallo-beleid.  Dit bestand is waar de meeste configuratiewijzigingen worden aangebracht.
* [Relying party bestanden](active-directory-b2c-overview-custom.md#policy-files) taakspecifieke bestanden aangeroepen door uw toepassing.

>[!NOTE]
>Als uw XML-editor validatie ondersteunt, Hallo-bestanden tegen Hallo TrustFrameworkPolicy_0.3.0.0.xsd XML-schema dat in de hoofdmap Hallo van Hallo starter pack bevindt zich te valideren. XML-schemavalidatie identificeert fouten voordat u uploadt.

 Aan de slag:

1. Download active-directory-b2c-custom-policy-starterpack vanuit GitHub. [Hallo ZIP-bestand downloaden](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/archive/master.zip) of uit te voeren

    ```console
    git clone https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack
    ```
2. Open Hallo SocialAndLocalAccounts map.  Hallo base-bestand (TrustFrameworkBase.xml) in deze map bevat inhoud die nodig zijn voor zowel lokale als sociale/bedrijfsnetwerk accounts. Hallo sociale inhoud niet van invloed op Hallo stappen voor lokale accounts slag.
3. Open TrustFrameworkBase.xml. Als u een XML-editor moet [Visual Studio Code probeert](https://code.visualstudio.com/download), een lichtgewicht platformoverschrijdende-editor.
4. In de hoofdmap Hallo `TrustFrameworkPolicy` element, update Hallo `TenantId` en `PublicPolicyUri` kenmerken, vervangen `yourtenant.onmicrosoft.com` met Hallo-domeinnaam van uw Azure AD B2C-tenant:
   ```xml
    <TrustFrameworkPolicy
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:xsd="http://www.w3.org/2001/XMLSchema"
    xmlns="http://schemas.microsoft.com/online/cpim/schemas/2013/06"
    PolicySchemaVersion="0.3.0.0"
    TenantId="yourtenant.onmicrosoft.com"
    PolicyId="B2C_1A_TrustFrameworkBase"
    PublicPolicyUri="http://yourtenant.onmicrosoft.com">
    ```
   >[!NOTE]
   >`PolicyId`Hallo beleidsnaam die u ziet in de portal Hallo en Hallo waarmee in dit bestand wordt verwezen door andere beleidsbestanden is.

5. Hallo-bestand opslaan.
6. Open TrustFrameworkExtensions.xml. Hallo dezelfde twee wijzigingen aanbrengen door te vervangen `yourtenant.onmicrosoft.com` met uw Azure AD B2C-tenant. Maken van dezelfde Hallo vervanging in Hallo `<TenantId>` element voor een totaal van drie wijzigingen. Hallo-bestand opslaan.
7. Open SignUpOrSignIn.xml. Hallo dezelfde wijzigingen aanbrengen door te vervangen `yourtenant.onmicrosoft.com` met uw Azure AD B2C-tenant op drie locaties. Hallo-bestand opslaan.
8. Open Hallo wachtwoord opnieuw instellen en profiel bewerken bestanden. Hallo dezelfde wijzigingen aanbrengen door te vervangen `yourtenant.onmicrosoft.com` met uw Azure AD B2C-tenant op drie locaties in elk bestand. Hallo-bestanden worden opgeslagen.

### <a name="add-hello-application-ids-tooyour-custom-policy"></a>Hallo-id's tooyour aangepaste Toepassingenbeleid toevoegen
Hallo-id's toohello extensies toepassingsbestand toevoegen (`TrustFrameworkExtensions.xml`):

1. Zoek in Hallo extensiebestand (TrustFrameworkExtensions.xml) Hallo element `<TechnicalProfile Id="login-NonInteractive">`.
2. Vervang beide exemplaren van `IdentityExperienceFrameworkAppId` met Hallo toepassings-ID van Hallo identiteit ervaring Framework-toepassing die u eerder hebt gemaakt. Hier volgt een voorbeeld:

   ```xml
   <Item Key="client_id">8322dedc-cbf4-43bc-8bb6-141d16f0f489</Item>
   ```
3. Vervang beide exemplaren van `ProxyIdentityExperienceFrameworkAppId` met Hallo toepassings-ID van Hallo Proxy identiteit ervaring Framework-toepassing die u eerder hebt gemaakt.
4. Sla het bestand uitbreidingen.

## <a name="upload-hello-policies-tooyour-tenant"></a>Hallo beleid tooyour tenant uploaden

1. In Hallo [Azure-portal](https://portal.azure.com), schakel over naar Hallo [context van uw Azure AD B2C-tenant](active-directory-b2c-navigate-to-b2c-context.md), en open Hallo **Azure AD B2C** blade.
2. Selecteer **identiteit ervaring Framework**.
3. Selecteer **uploaden beleid**.

    >[!WARNING]
    >Hallo aangepast beleidsbestanden moeten worden geüpload in Hallo volgorde:

1. TrustFrameworkBase.xml uploaden.
2. TrustFrameworkExtensions.xml uploaden.
3. SignUpOrSignin.xml uploaden.
4. Upload uw beleidsbestanden.

Wanneer een bestand is geüpload, Hallo-naam van bestand met beleidsregel van Hallo wordt voorafgegaan door `B2C_1A_`.

## <a name="test-hello-custom-policy-by-using-run-now"></a>Hallo aangepast beleid testen met behulp van nu uitvoeren

1. Open **Azure AD B2C-instellingen** en ga te**identiteit ervaring Framework**.

   >[!NOTE]
   >**Nu uitvoeren** vereist ten minste één toepassing toobe preregistered op Hallo-tenant. Toepassingen moeten worden geregistreerd in Hallo B2C-tenant met behulp van Hallo **toepassingen** menuselectie in Azure AD B2C of Hallo identiteit ervaring Framework tooinvoke met ingebouwde en aangepaste beleidsregels. Er is slechts één registratie per toepassing nodig.<br><br>
   hoe tooregister toepassingen, Zie toolearn hello Azure AD B2C [aan de slag](active-directory-b2c-get-started.md) artikel of Hallo [toepassingsregistratie](active-directory-b2c-app-registration.md) artikel.  

2. Open B2C_1A_signup_signin, Hallo relying party (RP) aangepast beleid dat u hebt geüpload. Selecteer **nu uitvoeren**.

3. U moet kunnen toosign met behulp van een e-mailadres.

4. Meld u aan met de Hallo dezelfde account tooconfirm die u hebt de juiste configuratie Hallo.

>[!NOTE]
>Een veelvoorkomende oorzaak van de aanmelding mislukt is een onjuist geconfigureerde IdentityExperienceFramework-app.


## <a name="next-steps"></a>Volgende stappen

### <a name="add-facebook-as-an-identity-provider"></a>Facebook toevoegen als een id-provider
tooset up Facebook:
1. [Configureer een Facebook-toepassing in developers.facebook.com](active-directory-b2c-setup-fb-app.md).
2. [Hallo Facebook toepassing geheime tooyour Azure AD B2C-tenant toevoegen](#add-signing-and-encryption-keys-to-your-b2c-tenant-for-use-by-custom-policies).
3. Vervang in Hallo TrustFrameworkExtensions beleidsbestand, Hallo-waarde van `client_id` met Hallo Facebook toepassings-ID:

   ```xml
   <TechnicalProfile Id="Facebook-OAUTH">
     <Metadata>
     <!--Replace hello value of client_id in this technical profile with hello Facebook app ID"-->
       <Item Key="client_id">00000000000000</Item>
   ```
4. Hallo TrustFrameworkExtensions.xml beleid bestand tooyour tenant uploaden.
5. Testen met behulp van **nu uitvoeren** of door het beleid rechtstreeks vanuit uw geregistreerde toepassing hello wordt aangeroepen.

### <a name="add-azure-active-directory-as-an-identity-provider"></a>Azure Active Directory toevoegen als een id-provider
Hallo base bestand al gebruikt in deze introductiehandleiding bevat enkele Hallo-inhoud die u nodig hebt voor het toevoegen van andere id-providers. Zie voor informatie over het instellen van aanmeldingen Hallo [Azure Active Directory B2C: aanmelden met Azure AD-accounts](active-directory-b2c-setup-aad-custom.md) artikel.

Zie voor een overzicht van aangepaste beleidsregels in Azure AD B2C die gebruikmaken van Hallo identiteit ervaring Framework Hallo [Azure Active Directory B2C: aangepast beleid](active-directory-b2c-overview-custom.md) artikel. 
