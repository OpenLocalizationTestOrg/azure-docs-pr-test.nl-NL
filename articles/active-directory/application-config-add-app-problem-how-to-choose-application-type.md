---
title: aaaHow toochoose welke toepassing toouse typt u bij het toevoegen van een toepassing | Microsoft Docs
description: Hallo ondersteund typen toepassingen die u met Azure AD integreren kunt te begrijpen en hun bijbehorende configuratie-opties
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 46e3672e7f5048b0fa54171f0fc169362c9d5ac6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toochoose-which-application-type-toouse-when-adding-an-application"></a>Hoe toochoose welke toepassing toouse typt u bij het toevoegen van een toepassing

In dit artikel helpt u toounderstand Hallo vier belangrijkste typen toepassingen die u met Azure AD integreren kunt:

* Wat wordt ondersteund door elk van deze
* Waarom u kunt ervoor kiezen welke toepassing
* Hoe tooconfigure kerneigenschappen voor deze toepassing, zoals hoe gebruikers worden **ingericht**, of wat **eenmalige aanmelding** toouse technologie.

## <a name="supported-application-types-in-azure-ad"></a>De soorten ondersteunde toepassingen in Azure AD

Azure AD ondersteunt vier hoofdtoepassing typen die u kunt toevoegen met behulp van Hallo **toevoegen** functie gevonden onder **bedrijfstoepassingen**. Deze omvatten:

-   **Azure AD-galerie toepassingen** : een toepassing die vooraf geïntegreerde voor eenmalige aanmelding met Azure AD is.

-   **Application Proxy toepassingen** : een toepassing die wordt uitgevoerd in uw on-premises omgeving dat u wilt dat tooprovide beveiligde eenmalige aanmelding tooexternally.

-   **Aangepaste ontwikkelde toepassingen** : een toepassing die uw organisatie wil toodevelop op Azure AD-ontwikkelplatform voor toepassing hello, maar die mogelijk niet bestaat.

-   **Niet-galerie toepassingen** : Breng uw eigen toepassingen! Een webkoppeling die u wilt dat alle toepassingen die een veld de gebruikersnaam en wachtwoord SAML of OpenID Connect-protocollen ondersteunt of ondersteunt SCIM die u wenst dat toointegrate voor eenmalige aanmelding met Azure AD.

## <a name="features-and-capabilities-supported-by-all-hello-above-application-types"></a>Functies en mogelijkheden die worden ondersteund door alle Hallo hierboven toepassingstypen

Hallo onderstaande functies worden ondersteund door een Hallo hierboven 4 toepassingstypen in Azure AD:

-   **Snel starten** – snel aan de slag met een toepassing door [eenvoudige implementatiestappen](https://docs.microsoft.com/azure/active-directory/active-directory-integrating-applications-getting-started)

-   **Algemene eigenschappen management** – ophalen van een [direct deeplink](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users) tooan toepassing, [Hallo huisstijl aanpassen](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-change-app-logo-user-azure-portal) van een toepassing of [toepassing hellouitschakelen](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) voor alle gebruikers.

-   **Gebruiker-en groepsbeheer** – [toewijzen](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) of [verwijderen](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) tooan toepassing voor gebruikers en groepen, en desgewenst toewijzen Hallo specifieke toepassingsrollen deze gebruikers en groepen hebt toegang tot

-   **Toegang tot de toepassing zelf** – inschakelen van uw gebruikers toorequest [toegang tot de toepassing zelf](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooan toepassing van de toegang tot hun toepassingen deelvensters door rechtstreeks een toepassing toe te voegen of [ toevoegen aan een Selfservice ingeschakeld groep](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management)desgewenst vereisen van zakelijke goedkeuring langs Hallo manier

-   **Aanmelden logboeken** – Zie [alle aanmeldingen tooan toepassing hello](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins), of al uw toepassingen

-   **Controlelogboeken** – Zie [controlelogboeken over wijzigingen tooan toepassing gedetailleerde](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs), of tooall uw toepassingen

-   **Voorwaardelijke en risico gebaseerde toegang** – Stel krachtige [regels voor toegang op basis van een voorwaarde](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access) die worden afgedwongen wanneer gebruikers toosign in bepaalde tooa-toepassing proberen

-   **Machtigingen weergave** – weergeven Hallo [OAuth2 machtigingen](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent) een toepassing heeft toegang tooin aan uw directory vanaf één locatie

## <a name="single-sign-on-and-provisioning-modes-supported-by-specific-application-types"></a>Eenmalige aanmelding en modi die worden ondersteund door specifieke toepassingstypen inrichten

Hallo in de volgende tabel beschrijft Hallo verschillende eenmalige aanmelding en modi die worden ondersteund door elk Hallo hierboven toepassingstypen inrichten. U kunt deze tabel toohelp toounderstand u welke toepassing u moet tooadd toosupport een specifiek doel.

  ![Tabel van App-typen](./media/application-tables/table1.png)

## <a name="how-toochoose-a-single-sign-on-mode"></a>Hoe toochoose een modus voor eenmalige aanmelding

Hallo ondersteund **eenmalige aanmelding** modi voor Azure AD-toepassingen worden hieronder weergegeven.

-   **Azure AD eenmalige aanmelding uitgeschakeld** – Kies Azure AD eenmalige aanmelding uitgeschakeld **modus voor één aanmelding** als u nog niet klaar toointegrate deze toepassing met eenmalige aanmelding met Azure AD, of gewoon test het uit

-   **Eenmalige aanmelding gekoppeld** – Kies Hallo [gekoppelde aanmelding](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **modus voor één aanmelding** als u een toepassing die al is gekoppeld aan een bestaande eenmalige aanmelding oplossing hebt of als u alleen wilt toopublish koppeling met een eenvoudige voor uw gebruikers in hun [toepassing Toegangspaneel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) of [startprogramma voor toepassingen van Office 365](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)

-   **Op basis van wachtwoorden aanmelding** – Kies Hallo [op basis van wachtwoorden aanmelding](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **modus voor één aanmelding** als een HTML-gebruikersnaam en wachtwoord veld Hiermee maakt u uw toepassing en u toostore wilt die gebruikersnaam en wachtwoord veilig toobe replay later toohello-toepassing

-   **Op basis van SAML-aanmelding** – Kies Hallo [op basis van SAML-aanmelding](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) eenmalige aanmelding modus als uw toepassing hello SAML of OpenID Connect-protocollen ondersteunt, of u wilt dat toobe toomap kunnen gebruikers op basis van rollen van de toepassing toospecific claims voor regels die u in uw SAML definieert *

   >[!NOTE]
   >Deze optie is niet beschikbaar wanneer de toepassingsproxy Hallo is geconfigureerd voor een toepassing.
   >
   >

-   **Op basis van een koptekst aanmelding** : Kies deze optie [headers gebaseerde aanmelding](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) aanmelding modus voor één hebt u een toepassing met PingAccess die ondersteuning biedt voor HTTP-header gebaseerde verificatie die u wilt dat tooperform eenmalige aanmelding op te

   >[!NOTE]
   >Deze optie is alleen beschikbaar wanneer de toepassingsproxy Hallo en PingAccess is geconfigureerd voor een toepassing.
   >
   >

-   **Geïntegreerde Windows-verificatie** – Kies Hallo [geïntegreerde Windows-verificatie](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) eenmalige aanmelding bij het blootstellen van een on-premises WIA-toepassing die u wilt dat tooperform eenmalige aanmelding op te

   >[!NOTE]
   >Deze optie is alleen beschikbaar wanneer de toepassingsproxy Hallo is geconfigureerd voor een toepassing.
   >
   >

## <a name="single-sign-on-modes-for-custom-developed-applications"></a>Modi voor eenmalige aanmelding voor aangepaste ontwikkelde toepassingen

Toepassingen u hebt ontwikkeld via Hallo aangepaste [ontwikkelde aangepaste toepassing](#_Custom-Developed_Applications) ervaring bieden ook ondersteuning voor extra eenmalige aanmelding modi niet hierboven worden vermeld. Deze omvatten:

-   [OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code) op basis van eenmalige aanmelding

-   [OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code) op basis van eenmalige aanmelding

-   [WS-Federation 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html) op basis van eenmalige aanmelding

-   [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) op basis van eenmalige aanmelding

Lees Hallo [ontwikkelaarshandleiding Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) toolearn meer informatie over hoe een aangepaste ontwikkelde toocreate-toepassing die ondersteuning biedt voor deze eenmalige aanmelding modi.

## <a name="how-tooset-an-applications-single-sign-on-mode"></a>Hoe een toepassing tooset enkel de modus voor eenmalige aanmelding

tooset een toepassing van **eenmalige aanmelding** modus Hallo instructies hieronder:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.

  * Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**

6.  Hallo-toepassing waarvoor u eenmalige aanmelding tooconfigure wilt selecteren.

7.  Nadat de toepassing hello wordt geladen, klikt u op **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.

## <a name="how-toochoose-a-provisioning-mode"></a>Hoe toochoose een inrichtingsmethode

-   **Handmatige inrichting** – Kies Hallo [handmatige](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#provisioning-modes) Inrichtingsmethode als u bestaande accounts hebt of toomanage accounts voor deze toepassing buiten Azure AD wilt.

-   **Automatische inrichting** – Kies Hallo [automatische](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#configuring-automatic-user-account-provisioning) **inrichtingsmodus** als u wilt dat tooenable automatische API gebaseerde inrichting en/of de inrichting van gebruikersaccounts toothis toepassing 

   >[!NOTE]
   >Deze optie is alleen beschikbaar voor toepassingen binnen Hallo **aanbevolen** categorie Hallo [Azure AD-Toepassingsgalerie](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#the-new-and-improved-application-gallery).
   >
   >

-   **Automatische inrichting op basis van SCIM** – gebruiken [automatische inrichting op basis van SCIM](https://docs.microsoft.com/azure/active-directory/active-directory-scim-provisioning) als uw toepassing hello SCIM protocol ondersteunt voor het detecteren van wijzigingen toousers en groepen die automatisch worden verzonden voor wijzigingen tooany toepassing is geïntegreerd met Azure AD 

   >[!NOTE]
   >Deze optie wordt niet vermeld als een bepaalde Inrichtingsmethode, maar is standaard ingeschakeld voor alle toepassingen die zijn geïntegreerd met Azure AD.
   >
   >

## <a name="how-tooset-an-applications-provisioning-mode"></a>Hoe een toepassing tooset de Inrichtingsmethode

tooset een toepassing van **inrichting** modus Hallo instructies hieronder:

tooset een toepassing van **eenmalige aanmelding** modus Hallo instructies hieronder:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.

  * Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**

6.  Hallo-toepassing waarvoor u inrichten tooconfigure wilt selecteren.

7.  Nadat de toepassing hello wordt geladen, klikt u op **inrichten** uit van de toepassing hello linkerkant navigatiemenu.

## <a name="next-steps"></a>Volgende stappen
[Toepassingen beheren met Azure Active Directory](active-directory-enable-sso-scenario.md)
