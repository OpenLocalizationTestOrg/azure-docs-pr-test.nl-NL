---
title: aaaProblems tooan toepassing hello Toegangsvenster aanmelden | Microsoft Docs
description: Hoe tootroubleshoot problemen met toegang tot een toepassing van Microsoft Azure AD-Toegangsvenster op myapps.microsoft.com Hallo
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
ms.reviewer: japere
ms.openlocfilehash: 346c4da06416bb9b330bdd5b1201253af19ba58b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-application-from-hello-access-panel"></a>Problemen met aanmelden tooan toepassing hello Toegangsvenster

Hallo Toegangspaneel is een portal op Internet waarmee een gebruiker met een werk of schoolaccount in Azure Active Directory (Azure AD) tooview en start cloud-gebaseerde toepassingen die hello Azure AD-beheerder heeft deze toegang verleend tot. 

Deze toepassingen zijn geconfigureerd namens de gebruiker Hallo in hello Azure AD-portal. Hallo-toepassing moet correct worden geconfigureerd en toegewezen toohello gebruiker of een groep Hallo-gebruiker lid is van toepassing op Hallo toosee in Hallo Toegangsvenster.

Hallo-type van een gebruiker ziet u mogelijk apps kunnen worden onderverdeeld in de volgende categorieën Hallo:

-   Office 365-toepassingen

-   Microsoft en derden toepassingen die zijn geconfigureerd op basis van een federatieve aanmelding bij

-   SSO-toepassingen op basis van wachtwoorden

-   Toepassingen met bestaande oplossingen voor eenmalige aanmelding

## <a name="general-issues-toocheck-first"></a>Algemene problemen toocheck eerst

-   Zorg ervoor dat uw met een **browser** die voldoet aan de minimale vereisten van de Hallo voor Hallo Toegangsvenster.

-   Zorg ervoor dat de browser van Hallo gebruiker is toegevoegd Hallo-URL van Hallo toepassing tooits **vertrouwde websites**.

-   Zorg ervoor dat toocheck Hallo toepassing **geconfigureerd** correct.

-   Zorg ervoor dat het account van de gebruiker Hallo **ingeschakeld** voor aanmeldingen.

-   Zorg ervoor dat het account van de gebruiker Hallo **niet is vergrendeld.**

-   Zorg ervoor dat Hallo-gebruiker **wachtwoord niet is verlopen of is vergeten.**

-   Zorg ervoor dat **multi-Factor Authentication** gebruikerstoegang niet blokkeert.

-   Zorg ervoor dat een **beleid voor voorwaardelijke toegang** of **Identity Protection** beleid voor de gebruikerstoegang niet blokkeert.

-   Zorg ervoor dat een gebruiker **verificatie contactgegevens** is toodate tooallow multi-factor Authentication of voorwaardelijk beleid toobe afgedwongen.

-   Zorg ervoor dat tooalso probeer wissen van cookies in uw browser opnieuw te proberen toosign in.

## <a name="meeting-browser-requirements-for-hello-access-panel"></a>Vergadering Browservereisten voor Hallo Toegangsvenster

Hallo Toegangsvenster vereist een browser die JavaScript ondersteunt en CSS is ingeschakeld. toouse op basis van wachtwoorden eenmalige aanmelding (SSO) in Hallo paneel voor Apptoegang, Hallo Toegangsvenster extensie moet zijn geïnstalleerd in de browser van Hallo gebruiker. Deze extensie wordt automatisch gedownload wanneer een gebruiker selecteert een toepassing die is geconfigureerd voor eenmalige aanmelding op basis van wachtwoorden.

Voor eenmalige aanmelding op basis van wachtwoorden kunnen browsers Hallo van de eindgebruiker zijn:

-   Internet Explorer 8, 9, 10, 11--op Windows 7 of hoger

-   Rand verjaardagseditie van Windows 10 of hoger

-   Chrome--Op Windows 7 of hoger, en op Mac OS X of hoger

-   Firefox 26,0 of later--op Windows XP SP2 of hoger, en op Mac OS X 10,6 of hoger

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a>Hoe tooinstall toegang Configuratiescherm Browseruitbreiding Hallo

tooinstall hello Configuratiescherm Browseruitbreiding toegang, Hallo volgende stappen:

1.  Open Hallo [Toegangspaneel](https://myapps.microsoft.com) in een van de Hallo ondersteunde browsers en meld u aan als een **gebruiker** in uw Azure AD.

2.  Klik op een **wachtwoord SSO toepassing** in Hallo Toegangsvenster.

3.  Selecteer in de Hallo vragen gevraagd tooinstall Hallo software, **nu installeren**.

4.  Op basis van uw browser zijn u gerichte toohello downloadkoppeling. **Voeg** Hallo extensie tooyour browser.

5.  Als uw browser wordt gevraagd, selecteert u tooeither **inschakelen** of **toestaan** Hallo extensie.

6.  Nadat deze is geïnstalleerd, **opnieuw** uw browsersessie.

7.  Aanmelden bij Hallo Toegangspaneel en zien als u kunt **starten** uw wachtwoord SSO-toepassingen

U kunt ook Hallo-extensie voor Chrome en de rand van Hallo rechtstreekse koppelingen hieronder downloaden:

-   [Uitbreiding van chrome toegang Configuratiescherm](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [Uitbreiding van de rand toegang Configuratiescherm](https://www.microsoft.com/store/apps/9pc9sckkzk84)

## <a name="how-tooconfigure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a>Hoe tooconfigure federatieve eenmalige aanmelding voor een toepassing van de galerie van Azure AD

Alle toepassing in de galerie van Azure AD Hallo ingeschakeld met Enterprise Single Sign-On-functionaliteit is een stapsgewijze zelfstudie beschikbaar. U hebt toegang tot Hallo [lijst met zelfstudies over het toointegrate SaaS-apps met Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) voor een stapsgewijze instructies voor details.

een toepassing uit de galerie van Azure AD Hallo tooconfigure moet u:

-   [Een toepassing uit de galerie van Azure AD Hallo toevoegen](#add-an-application)

-   [Configureren van de toepassing hello metagegevenswaarden in Azure AD (URL,-id en antwoord-URL van de aanmelding)](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [Selecteer gebruikers-id en gebruiker kenmerken toobe verzonden toohello toepassing toevoegen](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [Azure AD-metagegevens en certificaat ophalen](#download-the-azure-ad-metadata-or-certificate)

-   [Azure AD metagegevenswaarden configureren in toepassing hello (aanmelding URL, uitgever, afmelding URL en certificaat)](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [Toohello-toepassing voor gebruikers toewijzen](#assign-users-to-the-application)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a>Een toepassing uit de galerie van Azure AD Hallo toevoegen

een toepassing hello Azure AD-galerie tooadd Hallo volgende stappen:

1.  Open Hallo [Azure Portal](https://portal.azure.com) en meld u aan als een **hoofdbeheerder** of **Co-beheerder**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op Hallo **toevoegen** op Hallo rechterbovenhoek op Hallo knop **bedrijfstoepassingen** blade

6.  In Hallo **Voer een naam** textbox van Hallo **toevoegen uit de galerie Hallo** sectie, Hallo typenaam van de toepassing hello.

7.  Selecteer het gewenste tooconfigure voor eenmalige aanmelding Hallo-toepassing.

8.  Voordat u de toepassing hello toevoegt, kunt u de naam van Hallo **naam** textbox.

9.  Klik op **toevoegen** knop tooadd Hallo-toepassing.

Na een korte periode zijn u configuratie-blade kunnen toosee Hallo toepassing.

### <a name="configure-single-sign-on-for-an-application-from-hello-azure-ad-gallery"></a>Eenmalige aanmelding voor een toepassing van Hallo-galerie van Azure AD configureren

Volg onderstaande stappen voor Hallo tooconfigure eenmalige aanmelding voor een toepassing:

1.  <span id="_Hlk477187909" class="anchor"><span id="_Hlk477001983" class="anchor"></span></span>Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.

  * Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**

6.  Selecteer Hallo-toepassing die u wilt dat eenmalige aanmelding tooconfigure.

7.  Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.

8.  Selecteer **op basis van SAML aanmelding** van Hallo **modus** vervolgkeuzelijst.

9.  Voer waarden in Hallo vereist **domein en de URL's.** U moet deze waarden ophalen van de leverancier van de toepassing hello.

   1. tooconfigure hello toepassing als Serviceprovider geïnitieerde eenmalige aanmelding Hallo aanmelding op de URL voor deze waarde is vereist. Voor sommige toepassingen Hallo id bevindt zich ook een vereiste waarde.

   2. tooconfigure hello toepassing als IdP geïnitieerde eenmalige aanmelding, Hallo antwoord-URL is een vereiste waarde. Voor sommige toepassingen Hallo id bevindt zich ook een vereiste waarde.

10. **Optioneel:** klikt u op **weergeven geavanceerde instellingen voor URL** als u toosee Hallo niet vereist waarden wilt.

11. In Hallo **gebruikerskenmerken**, selecteer de unieke id voor uw gebruikers in Hallo Hallo **gebruikers-id** vervolgkeuzelijst.

12. **Optioneel:** klikt u op **weergeven en bewerken van alle andere gebruikerskenmerken** tooedit Hallo kenmerken toobe verzonden toohello toepassing in Hallo SAML-token wanneer de gebruiker zich aanmelden.

   een kenmerk tooadd:

   1. Klik op **toevoegen kenmerk**. Voer Hallo **naam** en selecteer Hallo Hallo **waarde** uit Hallo vervolgkeuzelijst.

   2. Klik op **opslaan.** U zien nieuw kenmerk Hallo in Hallo tabel.

13. Klik op **configureren &lt;toepassingsnaam&gt;**  tooaccess documentatie over het tooconfigure eenmalige aanmelding in Hallo-toepassing. U heeft ook Hallo metagegevens-URL's en vereiste certificaat toosetup eenmalige aanmelding met Hallo-toepassing.

14. Klik op **opslaan** toosave Hallo configuratie.

15. Gebruikers toohello toepassing toewijzen.

### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a>Selecteer gebruikers-id en gebruiker kenmerken toobe verzonden toohello toepassing toevoegen

tooselect Hallo gebruikers-id of gebruikerskenmerken toevoegen, volgt u onderstaande stappen voor Hallo:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.

  * Als u Hallo-toepassing die u wilt dat tooshow hier niet ziet, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**

6.  Selecteer Hallo-toepassing die u hebt geconfigureerd eenmalige aanmelding.

7.  Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.

8.  Onder Hallo **gebruikerskenmerken** sectie, selecteer de unieke id voor uw gebruikers in Hallo Hallo **gebruikers-id** vervolgkeuzelijst. Hallo moet geselecteerde de optie toomatch Hallo verwachtingswaarde in Hallo toepassing tooauthenticate Hallo gebruiker.

    >[!NOTE]
    >Azure AD Selecteer Hallo-indeling voor Hallo NameID kenmerk (gebruikers-id) op basis van geselecteerde Hallo-waarde of Hallo aangevraagd door de toepassing hello in Hallo SAML AuthRequest indeling. Voor meer informatie gaat u naar Hallo artikel [Single Sign-On SAML-protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) onder Hallo sectie NameIDPolicy.
    >
    >

9.  gebruikerskenmerken tooadd, klikt u op **weergeven en bewerken van alle andere gebruikerskenmerken** tooedit Hallo kenmerken toobe verzonden toohello toepassing in Hallo SAML-token wanneer de gebruiker zich aanmelden.

   een kenmerk tooadd:

   1. Klik op **toevoegen kenmerk**. Voer Hallo **naam** en selecteer Hallo Hallo **waarde** uit Hallo vervolgkeuzelijst.

   2. Klik op **opslaan.** U zien nieuw kenmerk Hallo in Hallo tabel.

### <a name="download-hello-azure-ad-metadata-or-certificate"></a>Azure AD-metagegevens hello of een certificaat downloaden

de metagegevens van de toepassing hello toodownload of het certificaat van Azure AD stappen Hallo volgende:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.

  * Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**

6.  Selecteer Hallo-toepassing die u hebt geconfigureerd eenmalige aanmelding.

7.  Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.

8.  Ga te**SAML-certificaat voor ondertekening van** sectie en klik vervolgens op **downloaden** waarde in de kolom. Afhankelijk van welke toepassing hello configureren van eenmalige aanmelding vereist, ziet u beide Hallo optie toodownload Hallo Metadata XML of Hallo certificaat.

    Azure AD biedt een URL tooget Hallo metagegevens niet. Hallo metagegevens kan alleen worden opgehaald als een XML-bestand.

## <a name="how-tooconfigure-federated-single-sign-on-for-a-non-gallery-application"></a>Hoe tooconfigure federatieve eenmalige aanmelding voor de toepassing van een niet-galerie

een toepassing niet galerie tooconfigure, moet u toohave Azure AD premium en toepassing hello SAML 2.0 ondersteunt. Voor meer informatie over Azure AD-versies, gaat u naar [prijzen van Azure AD](https://azure.microsoft.com/pricing/details/active-directory/).

-   [Configureren van de toepassing hello metagegevenswaarden in Azure AD (URL,-id en antwoord-URL van de aanmelding)](#configuring-single-sign-on)

-   [Selecteer gebruikers-id en gebruiker kenmerken toobe verzonden toohello toepassing toevoegen](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [Azure AD-metagegevens en certificaat ophalen](#download-the-azure-ad-metadata-or-certificate)

-   [Azure AD metagegevenswaarden configureren in toepassing hello (aanmelding URL, uitgever, afmelding URL en certificaat)](#configuring-single-sign-on)

### <a name="configure-hello-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a>Configureren van de toepassing hello metagegevenswaarden in Azure AD (URL,-id en antwoord-URL van de aanmelding)

tooconfigure eenmalige aanmelding voor een toepassing die zich niet in de galerie van Azure AD hello, stappen Hallo volgende:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op Hallo **toevoegen** op Hallo rechterbovenhoek op Hallo knop **bedrijfstoepassingen** blade

6.  Klik op **Non-galerie toepassing** in Hallo **uw eigen app toevoegen** sectie

7.  Voer de naam van de Hallo van de toepassing hello in Hallo **naam** textbox.

8.  Klik op **toevoegen** knop tooadd Hallo-toepassing.

9.  Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.

10. Selecteer **op basis van SAML aanmelding** in Hallo **modus** vervolgkeuzelijst

11. Voer waarden in Hallo vereist **domein en de URL's.** U moet deze waarden ophalen van de leverancier van de toepassing hello.

  1. tooconfigure hello toepassing als IdP geïnitieerde eenmalige aanmelding Hallo antwoord-URL en Hallo ID invoeren.

  2. **Optioneel:** tooconfigure Hallo toepassing als Serviceprovider geïnitieerde eenmalige aanmelding Hallo aanmelding op de URL voor deze waarde is vereist.

12. In Hallo **gebruikerskenmerken**, selecteer de unieke id voor uw gebruikers in Hallo Hallo **gebruikers-id** vervolgkeuzelijst.

13. **Optioneel:** klikt u op **weergeven en bewerken van alle andere gebruikerskenmerken** tooedit Hallo kenmerken toobe verzonden toohello toepassing in Hallo SAML-token wanneer de gebruiker zich aanmelden.

   een kenmerk tooadd:

   1. Klik op **toevoegen kenmerk**. Voer Hallo **naam** en selecteer Hallo Hallo **waarde** uit Hallo vervolgkeuzelijst.

   2. Klik op **opslaan.** U zien nieuw kenmerk Hallo in Hallo tabel.

14. Klik op **configureren &lt;toepassingsnaam&gt;**  tooaccess documentatie over het tooconfigure eenmalige aanmelding in Hallo-toepassing. Bovendien heeft u Azure AD-URL's en het certificaat dat is vereist voor de toepassing hello.

### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a>Selecteer gebruikers-id en gebruiker kenmerken toobe verzonden toohello toepassing toevoegen

tooselect Hallo gebruikers-id of gebruikerskenmerken toevoegen, volgt u onderstaande stappen voor Hallo:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.

  * Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**

6.  Selecteer Hallo-toepassing die u hebt geconfigureerd eenmalige aanmelding.

7.  Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.

8.  Onder Hallo **gebruikerskenmerken** sectie, selecteer de unieke id voor uw gebruikers in Hallo Hallo **gebruikers-id** vervolgkeuzelijst. Hallo moet geselecteerde de optie toomatch Hallo verwachtingswaarde in Hallo toepassing tooauthenticate Hallo gebruiker.

   >[!NOTE]
   >Azure AD Selecteer Hallo-indeling voor Hallo NameID kenmerk (gebruikers-id) op basis van geselecteerde Hallo-waarde of Hallo aangevraagd door de toepassing hello in Hallo SAML AuthRequest indeling. Voor meer informatie gaat u naar Hallo artikel [Single Sign-On SAML-protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) onder Hallo sectie NameIDPolicy.
   >
   >

9.  gebruikerskenmerken tooadd, klikt u op **weergeven en bewerken van alle andere gebruikerskenmerken** tooedit Hallo kenmerken toobe verzonden toohello toepassing in Hallo SAML-token wanneer de gebruiker zich aanmelden.

   een kenmerk tooadd:

   1. Klik op **toevoegen kenmerk**. Voer Hallo **naam** en selecteer Hallo Hallo **waarde** uit Hallo vervolgkeuzelijst.

   2 Klik **opslaan.** U zien nieuw kenmerk Hallo in Hallo tabel.

### <a name="download-hello-azure-ad-metadata-or-certificate"></a>Azure AD-metagegevens hello of een certificaat downloaden

de metagegevens van de toepassing hello toodownload of het certificaat van Azure AD stappen Hallo volgende:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.

   * Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**

6.  Selecteer Hallo-toepassing die u hebt geconfigureerd eenmalige aanmelding.

7.  Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.

8.  Ga te**SAML-certificaat voor ondertekening van** sectie en klik vervolgens op **downloaden** waarde in de kolom. Afhankelijk van welke toepassing hello configureren van eenmalige aanmelding vereist, ziet u beide Hallo optie toodownload Hallo Metadata XML of Hallo certificaat.

    Azure AD biedt een URL tooget Hallo metagegevens niet. Hallo metagegevens kan alleen worden opgehaald als een XML-bestand.

## <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a>Hoe tooconfigure wachtwoord eenmalige aanmelding voor een toepassing van de galerie van Azure AD

een toepassing uit de galerie van Azure AD Hallo tooconfigure moet u:

-   [Een toepassing uit de galerie van Azure AD Hallo toevoegen](#add-an-application)

-   [Hallo-toepassing voor eenmalige aanmelding wachtwoord configureren](#configure-the-application)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a>Een toepassing uit de galerie van Azure AD Hallo toevoegen

een toepassing hello Azure AD-galerie tooadd Hallo volgende stappen:

1.  Open Hallo [Azure Portal](https://portal.azure.com) en meld u aan als een **hoofdbeheerder** of **Co-beheerder**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op Hallo **toevoegen** op Hallo rechterbovenhoek op Hallo knop **bedrijfstoepassingen** blade

6.  In Hallo **Voer een naam** textbox van Hallo **toevoegen uit de galerie Hallo** sectie, Hallo typenaam van de toepassing hello

7.  Selecteer het gewenste tooconfigure voor eenmalige aanmelding Hallo-toepassing

8.  Voordat u de toepassing hello toevoegt, kunt u de naam van Hallo **naam** textbox.

9.  Klik op **toevoegen** knop tooadd Hallo-toepassing.

Na een korte periode zijn u configuratie-blade kunnen toosee Hallo toepassing.

### <a name="configure-hello-application-for-password-single-sign-on"></a>Hallo-toepassing voor eenmalige aanmelding wachtwoord configureren

Volg onderstaande stappen voor Hallo tooconfigure eenmalige aanmelding voor een toepassing:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.

 * Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**

6.  Hallo-toepassing die u wilt dat eenmalige aanmelding tooconfigure selecteren

7.  Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.

8.  Selecteer Hallo modus **op basis van wachtwoorden eenmalige aanmelding.**

9.  Gebruikers toohello toepassing toewijzen.

10. Bovendien kunt u ook referenties opgeven namens de gebruiker Hallo door het selecteren van rijen Hallo Hallo-gebruikers en te klikken op **updatereferenties** en Hallo gebruikersnaam en wachtwoord in te voeren namens Hallo gebruikers. Anders worden gebruikers na vragen aan gebruiker tooenter Hallo referenties zelf bij het starten.

## <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a>Hoe tooconfigure wachtwoord eenmalige aanmelding voor de toepassing van een niet-galerie

een toepassing uit de galerie van Azure AD Hallo tooconfigure moet u:

-   [Toevoegen van een toepassing niet-galerie](#add-a-non-gallery-application)

-   [Hallo-toepassing voor eenmalige aanmelding wachtwoord configureren](#configure-the-application-for-password-single-sign-on)

### <a name="add-a-non-gallery-application"></a>Toevoegen van een toepassing niet-galerie

een toepassing hello Azure AD-galerie tooadd Hallo volgende stappen:

1.  Open Hallo [Azure Portal](https://portal.azure.com) en meld u aan als een **hoofdbeheerder** of **Co-beheerder**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op Hallo **toevoegen** op Hallo rechterbovenhoek op Hallo knop **bedrijfstoepassingen** blade

6.  Klik op **Non-galerie-toepassing.**

7.  Vul in Hallo Hallo-naam van uw toepassing **naam** textbox. Selecteer **toevoegen.**

Na een korte periode zijn u configuratie-blade kunnen toosee Hallo toepassing.

### <a name="configure-hello-application-for-password-single-sign-on"></a>Hallo-toepassing voor eenmalige aanmelding wachtwoord configureren

Volg onderstaande stappen voor Hallo tooconfigure eenmalige aanmelding voor een toepassing:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.

 * Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**

6.  Selecteer Hallo-toepassing die u wilt dat eenmalige aanmelding tooconfigure.

7.  Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.

8.  Selecteer Hallo modus **op basis van wachtwoorden eenmalige aanmelding.**

9.  Voer Hallo **aanmeldings-URL**. Dit is Hallo URL waarin gebruikers hun gebruikersnaam en wachtwoord toosign in te typen. Zorg ervoor dat Hallo aanmelden velden zijn zichtbaar tijdens het Hallo-URL.

10. Gebruikers toohello toepassing toewijzen.

11. Bovendien kunt u ook referenties opgeven namens de gebruiker Hallo door het selecteren van rijen Hallo Hallo-gebruikers en te klikken op **updatereferenties** en Hallo gebruikersnaam en wachtwoord in te voeren namens Hallo gebruikers. Anders worden gebruikers na vragen aan gebruiker tooenter Hallo referenties zelf bij het starten.

## <a name="how-tooassign-a-user-tooan-application-directly"></a>Hoe een gebruiker tooan toepassing rechtstreeks tooassign

tooassign een of meer gebruikers tooan toepassing rechtstreeks Hallo volgende stappen:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.

  * Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**

6.  Hallo-toepassing die u wilt dat een lijst met gebruikers toofrom hello tooassign selecteren.

7.  Nadat de toepassing hello wordt geladen, klikt u op **gebruikers en groepen** uit van de toepassing hello linkerkant navigatiemenu.

8.  Klik op Hallo **toevoegen** knop boven op Hallo **gebruikers en groepen** lijst tooopen hello **toevoegen toewijzing** blade.

9.  Klik op Hallo **gebruikers en groepen** selector van Hallo **toevoegen toewijzing** blade.

10. Type in Hallo **volledige naam** of **e-mailadres** van Hallo gebruiker u geïnteresseerd bent in het toewijzen van Hallo **zoeken op naam of e-mailadres** zoekvak.

11. Beweeg de muisaanwijzer over Hallo **gebruiker** in Hallo lijst tooreveal een **selectievakje**. Klik op het profiel foto of een logo tooadd Hallo selectievakje volgende toohello van gebruiker uw gebruiker toohello **geselecteerde** lijst.

12. **Optioneel:** indien te gewenst**toevoegen van meer dan één gebruiker**, type in een andere **volledige naam** of **e-mailadres** in Hallo **zoeken op naam of e-mailadres** zoekvak en klikt u op Hallo selectievakje tooadd voor deze gebruiker toohello **geselecteerde** lijst.

13. Wanneer u klaar bent met het selecteren van gebruikers, klikt u op Hallo **Selecteer** knop tooadd ze toohello lijst met gebruikers en groepen toobe toegewezen toohello toepassing.

14. **Optioneel:** klikt u op Hallo **rol selecteren** selector in Hallo **toevoegen toewijzing** blade tooselect een rol tooassign toohello gebruikers die u hebt geselecteerd.

15. Klik op Hallo **toewijzen** knop tooassign Hallo toepassing toohello gebruikers geselecteerd.

Hallo Toegangsvenster na een korte periode Hallo-gebruikers die u hebt geselecteerd niet kunnen toolaunch deze toepassingen in.

## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a>Als deze stappen voor probleemoplossing niet Hallo Hallo probleem oplossen

Open een ondersteuningsticket Hello volgende informatie, indien beschikbaar:

-   Correlatie fout-ID

-   UPN (e-mailadres van de gebruiker)

-   TenantID

-   Browsertype

-   Tijdzone en de tijd/tijdsbestek tijdens fout optreedt

-   Fiddler traceringen

## <a name="next-steps"></a>Volgende stappen
[Bieden van eenmalige aanmelding tooyour apps met toepassingsproxy](active-directory-application-proxy-sso-using-kcd.md)

