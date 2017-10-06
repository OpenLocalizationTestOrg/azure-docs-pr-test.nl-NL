---
title: aaaHow toodetermine welke eenmalige aanmelding methode toouse | Microsoft Docs
description: "Hallo eenmalige aanmelding modi ondersteund door Azure AD te begrijpen en hoe toopick welke één toochoose voor toepassing hello u geïnteresseerd bent in."
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
ms.openlocfilehash: 64f0bc1dc8281d1ab8222fd50eaceaf710704886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodetermine-what-single-sign-on-method-toouse"></a>Hoe toodetermine welke eenmalige aanmelding methode toouse

In dit artikel kunt u toounderstand Hallo eenmalige aanmelding modi ondersteund door Azure AD en hoe toopick welke één toochoose voor toepassing hello u geïnteresseerd bent in.

## <a name="single-sign-on-and-provisioning-modes-supported-by-specific-application-types"></a>Eenmalige aanmelding en modi die worden ondersteund door specifieke toepassingstypen inrichten

Hallo in de volgende tabel beschrijft Hallo verschillende eenmalige aanmelding en modi die worden ondersteund door elk Hallo hierboven toepassingstypen inrichten. U kunt deze tabel toohelp toounderstand u welke toepassing u moet tooadd toosupport een specifiek doel.

  ![Azië typen tabel](./media/application-tables/table1.png)

## <a name="how-toochoose-a-single-sign-on-mode"></a>Hoe toochoose een modus voor eenmalige aanmelding

Hallo ondersteund **eenmalige aanmelding** modi voor Azure AD-toepassingen worden hieronder weergegeven.

-   **Azure AD eenmalige aanmelding uitgeschakeld** – Kies Azure AD eenmalige aanmelding uitgeschakeld **modus voor één aanmelding** als u nog niet klaar toointegrate deze toepassing met eenmalige aanmelding met Azure AD, of gewoon test het uit

-   **Eenmalige aanmelding gekoppeld** – Kies Hallo [gekoppelde aanmelding](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **modus voor één aanmelding** als u een toepassing die al is gekoppeld aan een bestaande eenmalige aanmelding oplossing hebt of als u alleen wilt toopublish koppeling met een eenvoudige voor uw gebruikers in hun [toepassing Toegangspaneel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) of [startprogramma voor toepassingen van Office 365](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)

-   **Op basis van wachtwoorden aanmelding** – Kies Hallo [op basis van wachtwoorden aanmelding](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **modus voor één aanmelding** als een HTML-gebruikersnaam en wachtwoord veld Hiermee maakt u uw toepassing en u toostore wilt die gebruikersnaam en wachtwoord veilig toobe replay later toohello-toepassing

-   **Op basis van SAML-aanmelding** – Kies Hallo [op basis van SAML-aanmelding](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) eenmalige aanmelding modus als uw toepassing hello SAML of OpenID Connect-protocollen ondersteunt, of u wilt dat toobe toomap kunnen gebruikers op basis van rollen van de toepassing toospecific claims voor regels die u in uw SAML definieert *(**Opmerking:** deze optie is niet beschikbaar wanneer het Hallo-toepassingsproxy is geconfigureerd voor een toepassing) *

-   **Op basis van een koptekst aanmelding** : Kies deze optie [headers gebaseerde aanmelding](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) aanmelding modus voor één hebt u een toepassing met PingAccess die ondersteuning biedt voor HTTP-header gebaseerde verificatie die u wilt dat tooperform eenmalige aanmelding op te *(**Opmerking:** deze optie is alleen beschikbaar wanneer de toepassingsproxy Hallo en PingAccess is geconfigureerd voor een toepassing) *

-   **Geïntegreerde Windows-verificatie** – Kies Hallo [geïntegreerde Windows-verificatie](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) eenmalige aanmelding bij het blootstellen van een on-premises WIA-toepassing die u wilt dat tooperform eenmalige aanmelding op te*()*  *Opmerking:** deze optie is alleen beschikbaar wanneer het Hallo-toepassingsproxy is geconfigureerd voor een toepassing) *

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

6.  Hallo-toepassing die u wilt dat eenmalige aanmelding tooconfigure selecteren

7.  Nadat de toepassing hello wordt geladen, klikt u op **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.

## <a name="next-steps"></a>Volgende stappen
[Bieden van eenmalige aanmelding tooyour apps met toepassingsproxy](active-directory-application-proxy-sso-using-kcd.md)

