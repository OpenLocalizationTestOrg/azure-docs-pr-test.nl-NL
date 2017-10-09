---
title: aaaAn toegewezen toepassing wordt niet weergegeven op het toegangsvenster Hallo | Microsoft Docs
description: Waarom een toepassing wordt niet weergegeven in het deelvenster toegang Hallo
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
ms.reviwer: japere
ms.openlocfilehash: 089883f406267df4552c7fc991883f335ad49fd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="an-assigned-application-is-not-appearing-on-hello-access-panel"></a>Een toegewezen toepassing wordt niet weergegeven op het toegangsvenster Hallo

Hallo Toegangspaneel is een portal op Internet waarmee een gebruiker met een werk of schoolaccount in Azure Active Directory (Azure AD) tooview en start cloud-gebaseerde toepassingen die hello Azure AD-beheerder heeft deze toegang verleend tot. Deze toepassingen zijn geconfigureerd namens de gebruiker Hallo in hello Azure AD-portal. Hallo-toepassing moet correct worden geconfigureerd en toegewezen toohello gebruiker of een groep Hallo-gebruiker lid is van toepassing op Hallo toosee in Hallo Toegangsvenster.

Hallo-type van een gebruiker ziet u mogelijk apps kunnen worden onderverdeeld in de volgende categorieën Hallo:

-   Office 365-toepassingen

-   Microsoft en derden toepassingen die zijn geconfigureerd op basis van een federatieve aanmelding bij

-   SSO-toepassingen op basis van wachtwoorden

-   Toepassingen met bestaande oplossingen voor eenmalige aanmelding

## <a name="general-issues-toocheck-first"></a>Algemene problemen toocheck eerst

-   Als een toepassing NET tooa gebruiker werd toegevoegd, opnieuw toosign in en uit in het toegangsvenster Hallo van de gebruiker na een paar minuten toosee als toepassing hello wordt toegevoegd.

-   Als u een licentie is verwijderd uit een gebruiker of groep Hallo gebruiker is dat lid van deze kan lang duren, afhankelijk van Hallo omvang en complexiteit van de groep Hallo voor toobe van wijzigingen aangebracht. Voor extra tijd voordat je je aanmeldt bij Hallo Toegangsvenster toestaan.

## <a name="problems-related-tooapplication-configuration"></a>Problemen met gerelateerde tooapplication configuratie

Een toepassing kan niet worden weergegeven in het deelvenster voor een gebruiker toegang omdat deze niet correct is geconfigureerd. Hieronder volgen enkele manieren waarop die u gerelateerde tooapplication configuratie van problemen kunt oplossen:

-   [Hoe tooconfigure federatieve eenmalige aanmelding voor een toepassing van de galerie van Azure AD](#how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application)

-   [Hoe tooconfigure federatieve eenmalige aanmelding voor de toepassing van een niet-galerie](#how-to-configure-federated-single-sign-on-for-a-non-gallery-application)

-   [Hoe tooconfigure een wachtwoord eenmalige aanmelding-toepassing voor een toepassing van de galerie van Azure AD](#how-to-configure-password-single-sign-on-for-a-non-gallery-application)

-   [Hoe tooconfigure een wachtwoord eenmalige aanmelding-toepassing voor een toepassing niet-galerie](#how-to-configure-password-single-sign-on-for-a-non-gallery-application)

### <a name="how-tooconfigure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a>Hoe tooconfigure federatieve eenmalige aanmelding voor een toepassing van de galerie van Azure AD

Alle toepassingen in de galerie van Azure AD Hallo ingeschakeld met Enterprise Single Sign-On-functionaliteit is een stapsgewijze zelfstudie beschikbaar. U hebt toegang tot Hallo [lijst met zelfstudies over het toointegrate SaaS-apps met Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) voor een stapsgewijze instructies voor details.

een toepassing uit de galerie van Azure AD Hallo tooconfigure moet u:

-   [Een toepassing uit de galerie van Azure AD Hallo toevoegen](#add-an-application-from-the-azure-ad-gallery)

-   [Configureren van de toepassing hello metagegevenswaarden in Azure AD (URL,-id en antwoord-URL van de aanmelding)](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [Selecteer gebruikers-id en gebruiker kenmerken toobe verzonden toohello toepassing toevoegen](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [Azure AD-metagegevens en certificaat ophalen](#download-the-azure-ad-metadata-or-certificate)

-   [Azure AD metagegevenswaarden configureren in toepassing hello (aanmelding URL, uitgever, afmelding URL en certificaat)](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

#### <a name="add-an-application-from-hello-azure-ad-gallery"></a>Een toepassing uit de galerie van Azure AD Hallo toevoegen

een toepassing hello Azure AD-galerie tooadd Hallo volgende stappen:

1.  Open Hallo [Azure Portal](https://portal.azure.com) en meld u aan als een **hoofdbeheerder** of **Co-beheerder**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op Hallo **toevoegen** op Hallo rechterbovenhoek op Hallo knop **bedrijfstoepassingen** blade.

6.  In Hallo **Voer een naam** textbox van Hallo **toevoegen uit de galerie Hallo** sectie, Hallo typenaam van de toepassing hello.

7.  Selecteer het gewenste tooconfigure voor eenmalige aanmelding Hallo-toepassing.

8.  Voordat u de toepassing hello toevoegt, kunt u de naam van Hallo **naam** textbox.

9.  Klik op **toevoegen** knop tooadd Hallo-toepassing.

Na een korte periode zijn u configuratie-blade kunnen toosee Hallo toepassing.

#### <a name="configure-single-sign-on-for-an-application-from-hello-azure-ad-gallery"></a>Eenmalige aanmelding voor een toepassing van Hallo-galerie van Azure AD configureren

Volg onderstaande stappen voor Hallo tooconfigure eenmalige aanmelding voor een toepassing:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**

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

#### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a>Selecteer gebruikers-id en gebruiker kenmerken toobe verzonden toohello toepassing toevoegen

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

   2. Klik op **opslaan.** Hier ziet u nieuw kenmerk in de tabel Hallo Hallo.

#### <a name="download-hello-azure-ad-metadata-or-certificate"></a>Azure AD-metagegevens hello of een certificaat downloaden

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

### <a name="how-tooconfigure-federated-single-sign-on-for-a-non-gallery-application"></a>Hoe tooconfigure federatieve eenmalige aanmelding voor de toepassing van een niet-galerie

een toepassing niet galerie tooconfigure, moet u toohave Azure AD premium en toepassing hello SAML 2.0 ondersteunt. Voor meer informatie over Azure AD-versies, gaat u naar [prijzen van Azure AD](https://azure.microsoft.com/pricing/details/active-directory/).

-   [Configureren van de toepassing hello metagegevenswaarden in Azure AD (URL,-id en antwoord-URL van de aanmelding)](#configuring-single-sign-on)

-   [Selecteer gebruikers-id en gebruiker kenmerken toobe verzonden toohello toepassing toevoegen](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [Azure AD-metagegevens en certificaat ophalen](#download-the-azure-ad-metadata-or-certificate)

-   [Azure AD metagegevenswaarden configureren in toepassing hello (aanmelding URL, uitgever, afmelding URL en certificaat)](#configuring-single-sign-on)

#### <a name="configure-hello-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a>Configureren van de toepassing hello metagegevenswaarden in Azure AD (URL,-id en antwoord-URL van de aanmelding)

tooconfigure eenmalige aanmelding voor een toepassing die zich niet in de galerie van Azure AD hello, stappen Hallo volgende:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op Hallo **toevoegen** op Hallo rechterbovenhoek op Hallo knop **bedrijfstoepassingen** blade.

6.  Klik op **Non-galerie toepassing** in Hallo **uw eigen app toevoegen** sectie.

7.  Voer de naam van de Hallo van de toepassing hello in Hallo **naam** textbox.

8.  Klik op **toevoegen** knop tooadd Hallo-toepassing.

9.  Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.

10. Selecteer **op basis van SAML aanmelding** in Hallo **modus** vervolgkeuzelijst.

11. Voer waarden in Hallo vereist **domein en de URL's.** U moet deze waarden ophalen van de leverancier van de toepassing hello.

   1. tooconfigure hello toepassing als IdP geïnitieerde eenmalige aanmelding Hallo antwoord-URL en Hallo ID invoeren.

   2.  **Optioneel:** tooconfigure Hallo toepassing als Serviceprovider geïnitieerde eenmalige aanmelding Hallo aanmelding op de URL voor deze waarde is vereist.

12. In Hallo **gebruikerskenmerken**, selecteer de unieke id voor uw gebruikers in Hallo Hallo **gebruikers-id** vervolgkeuzelijst.

13. **Optioneel:** klikt u op **weergeven en bewerken van alle andere gebruikerskenmerken** tooedit Hallo kenmerken toobe verzonden toohello toepassing in Hallo SAML-token wanneer de gebruiker zich aanmelden.

   een kenmerk tooadd:

   1. Klik op **toevoegen kenmerk**. Voer Hallo **naam** en selecteer Hallo Hallo **waarde** uit Hallo vervolgkeuzelijst.

   2. Klik op **opslaan.** U zien nieuw kenmerk Hallo in Hallo tabel.

14. Klik op **configureren &lt;toepassingsnaam&gt;**  tooaccess documentatie over het tooconfigure eenmalige aanmelding in Hallo-toepassing. Bovendien heeft u Azure AD-URL's en het certificaat dat is vereist voor de toepassing hello.

#### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a>Selecteer gebruikers-id en gebruiker kenmerken toobe verzonden toohello toepassing toevoegen

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

   2. Klik op **opslaan.** U zien nieuw kenmerk Hallo in Hallo tabel.

#### <a name="download-hello-azure-ad-metadata-or-certificate"></a>Azure AD-metagegevens hello of een certificaat downloaden

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

### <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a>Hoe tooconfigure wachtwoord eenmalige aanmelding voor een toepassing van de galerie van Azure AD

een toepassing uit de galerie van Azure AD Hallo tooconfigure moet u:

-   [Een toepassing uit de galerie van Azure AD Hallo toevoegen](#add-an-application-from-the-azure-ad-gallery)

-   [Hallo-toepassing voor eenmalige aanmelding wachtwoord configureren](#configure-the-application-for-password-single-sign-on)

#### <a name="add-an-application-from-hello-azure-ad-gallery"></a>Een toepassing uit de galerie van Azure AD Hallo toevoegen

een toepassing hello Azure AD-galerie tooadd Hallo volgende stappen:

1.  Open Hallo [Azure Portal](https://portal.azure.com) en meld u aan als een **hoofdbeheerder** of **Co-beheerder**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op Hallo **toevoegen** op Hallo rechterbovenhoek op Hallo knop **bedrijfstoepassingen** blade.

6.  In Hallo **Voer een naam** textbox van Hallo **toevoegen uit de galerie Hallo** sectie, Hallo typenaam van de toepassing hello.

7.  Selecteer het gewenste tooconfigure voor eenmalige aanmelding Hallo-toepassing.

8.  Voordat u de toepassing hello toevoegt, kunt u de naam van Hallo **naam** textbox.

9.  Klik op **toevoegen** knop tooadd Hallo-toepassing.

Na een korte periode zijn u configuratie-blade kunnen toosee Hallo toepassing.

#### <a name="configure-hello-application-for-password-single-sign-on"></a>Hallo-toepassing voor eenmalige aanmelding wachtwoord configureren

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

9.  [Gebruikers toewijzen toohello toepassing](#how-to-assign-a-user-to-an-application-directly).

10. Bovendien kunt u ook referenties opgeven namens de gebruiker Hallo door het selecteren van rijen Hallo Hallo-gebruikers en te klikken op **updatereferenties** en Hallo gebruikersnaam en wachtwoord in te voeren namens Hallo gebruikers. Anders worden gebruikers na vragen aan gebruiker tooenter Hallo referenties zelf bij het starten.

### <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a>Hoe tooconfigure wachtwoord eenmalige aanmelding voor de toepassing van een niet-galerie

een toepassing uit de galerie van Azure AD Hallo tooconfigure moet u:

-   [Toevoegen van een toepassing niet-galerie](#add-a-non-gallery-application)

-   [Hallo-toepassing voor eenmalige aanmelding wachtwoord configureren](#configure-the-application-for-password-single-sign-on)

#### <a name="add-a-non-gallery-application"></a>Toevoegen van een toepassing niet-galerie

een toepassing hello Azure AD-galerie tooadd Hallo volgende stappen:

1.  Open Hallo [Azure Portal](https://portal.azure.com) en meld u aan als een **hoofdbeheerder** of **Co-beheerder**.

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op Hallo **toevoegen** op Hallo rechterbovenhoek op Hallo knop **bedrijfstoepassingen** blade.

6.  Klik op **Non-galerie-toepassing.**

7.  Vul in Hallo Hallo-naam van uw toepassing **naam** textbox. Selecteer **toevoegen.**

Na een korte periode zijn u configuratie-blade kunnen toosee Hallo toepassing.

#### <a name="configure-hello-application-for-password-single-sign-on"></a>Hallo-toepassing voor eenmalige aanmelding wachtwoord configureren

Volg onderstaande stappen voor Hallo tooconfigure eenmalige aanmelding voor een toepassing:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.

    1.  Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**

6.  Selecteer Hallo-toepassing die u wilt dat eenmalige aanmelding tooconfigure.

7.  Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.

8.  Selecteer Hallo modus **op basis van wachtwoorden eenmalige aanmelding.**

9.  Voer Hallo **aanmeldings-URL**. Dit is Hallo URL waarin gebruikers hun gebruikersnaam en wachtwoord toosign in te typen. Zorg ervoor dat Hallo aanmelden velden zijn zichtbaar tijdens het Hallo-URL.

10. [Gebruikers toewijzen toohello toepassing](#how-to-assign-a-user-to-an-application-directly).

11. Bovendien kunt u ook referenties opgeven namens de gebruiker Hallo door het selecteren van rijen Hallo Hallo-gebruikers en te klikken op **updatereferenties** en Hallo gebruikersnaam en wachtwoord in te voeren namens Hallo gebruikers. Anders worden gebruikers na vragen aan gebruiker tooenter Hallo referenties zelf bij het starten.

## <a name="problems-related-tooassigning-applications-toousers"></a>Problemen met gerelateerde tooassigning toepassingen toousers

Een gebruiker mogelijk niet ziet u een toepassing op hun Toegangsvenster omdat ze toohello toepassing nog niet zijn toegewezen. Hieronder vindt u enkele toocheck manieren:

-   [Controleren of een gebruiker toohello toepassing is toegewezen](#check-if-a-user-is-assigned-to-the-application)

-   [Hoe een gebruiker tooan toepassing rechtstreeks tooassign](#how-to-assign-a-user-to-an-application-directly)

-   [Controleer of een gebruiker is toegewezen licentie tooa gerelateerde toohello toepassing](#check-if-a-user-is-under-a-license-related-to-the-application)

-   [Hoe tooassign een licentie tooa gebruiker](#how-to-assign-a-user-a-license)

### <a name="check-if-a-user-is-assigned-toohello-application"></a>Controleren of een gebruiker toohello toepassing is toegewezen

toocheck als een gebruiker is toegewezen toohello-toepassing hello volgende stappen:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.

6.  **Search** voor Hallo-naam van de betrokken Hallo-toepassing.

7.  Klik op **gebruikers en groepen**.

8.  Controleer toosee als de gebruiker toohello toepassing is toegewezen.

   * Als dat niet het Hallo-stappen in ' hoe tooassign een tooan Gebruikerstoepassing rechtstreeks ' toodo zodat.

### <a name="how-tooassign-a-user-tooan-application-directly"></a>Hoe een gebruiker tooan toepassing rechtstreeks tooassign

tooassign een of meer gebruikers tooan toepassing rechtstreeks Hallo volgende stappen:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder**.

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

### <a name="check-if-a-user-is-under-a-license-related-toohello-application"></a>Controleer of een gebruiker zich onder een licentie gerelateerde toohello toepassing

toocheck een gebruiker de toegewezen licenties, Hallo stappen hieronder:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **gebruikers en groepen** in het navigatiemenu Hallo.

5.  Klik op **alle gebruikers**.

6.  **Search** voor u geïnteresseerd in het bent Hallo-gebruiker en **klikt u op Hallo rij** tooselect.

7.  Klik op **licenties** toosee welke licenties Hallo gebruiker momenteel is toegewezen.

  * Hallo Toegangsvenster van de gebruiker als Hallo gebruiker tooan dit eerste partij Office-toepassingen tooappear inschakelen op Office-licentie is toegewezen.

### <a name="how-tooassign-a-user-a-license"></a>Hoe een gebruiker een licentie tooassign 

een gebruiker van de tooa licentie tooassign Hallo volgende stappen:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **gebruikers en groepen** in het navigatiemenu Hallo.

5.  Klik op **alle gebruikers**.

6.  **Search** voor u geïnteresseerd in het bent Hallo-gebruiker en **klikt u op Hallo rij** tooselect.

7.  Klik op **licenties** toosee welke licenties Hallo gebruiker momenteel is toegewezen.

8.  Klik op Hallo **toewijzen** knop.

9.  Selecteer **een of meer producten** uit de lijst met beschikbare producten Hallo.

10. **Optionele** klikt u op Hallo **toewijzingsopties** item toogranularly producten toewijzen. Klik op **Ok** wanneer dit is voltooid.

11. Klik op Hallo **toewijzen** knop tooassign deze licenties toothis-gebruiker.

## <a name="problems-related-tooassigning-applications-toogroups"></a>Problemen met gerelateerde tooassigning toepassingen toogroups

Een gebruiker mogelijk ziet u een toepassing op hun Toegangsvenster omdat ze deel uitmaken van een groep die de toepassing hello is toegewezen. Hieronder vindt u enkele toocheck manieren:

-   [Controleer de groepslidmaatschappen van een gebruiker](#check-a-users-group-memberships)

-   [Hoe tooassign een toepassing tooa groepeert rechtstreeks](#how-to-assign-an-application-to-a-group-directly)

-   [Controleer of een gebruiker deel van de groep tooa licentie is toegewezen uitmaakt](#check-if-a-user-is-part-of-group-assigned-to-a-license)

-   [Hoe een licentiegroep tooa tooassign](#how-to-assign-a-license-to-a-group)

### <a name="check-a-users-group-memberships"></a>Controleer de groepslidmaatschappen van een gebruiker

toocheck een groepslidmaatschap, Hallo stappen hieronder:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **gebruikers en groepen** in het navigatiemenu Hallo.

5.  Klik op **alle gebruikers**.

6.  **Search** voor u geïnteresseerd in het bent Hallo-gebruiker en **klikt u op Hallo rij** tooselect.

7.  Klik op **groepen**.

8.  Controleer de toosee als de gebruiker deel uit van een groep die is toegewezen toohello-toepassing maakt.

  * Als u tooremove Hallo gebruiker uit groep Hallo wilt **klikt u op Hallo rij** van Hallo groep en selecteer verwijderen.

### <a name="how-tooassign-an-application-tooa-group-directly"></a>Hoe tooassign een toepassing tooa groepeert rechtstreeks

tooassign een of meer groepen tooan toepassing rechtstreeks Hallo stappen hieronder:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder**.

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.

  * Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**

6.  Hallo-toepassing die u wilt dat een lijst met gebruikers toofrom hello tooassign selecteren.

7.  Nadat de toepassing hello wordt geladen, klikt u op **gebruikers en groepen** uit van de toepassing hello linkerkant navigatiemenu.

8.  Klik op Hallo **toevoegen** knop boven op Hallo **gebruikers en groepen** lijst tooopen hello **toevoegen toewijzing** blade.

9.  Klik op Hallo **gebruikers en groepen** selector van Hallo **toevoegen toewijzing** blade.

10. Type in Hallo **volledige groepsnaam** van Hallo groep u geïnteresseerd bent in het toewijzen van Hallo **zoeken op naam of e-mailadres** zoekvak.

11. Beweeg de muisaanwijzer over Hallo **groep** in Hallo lijst tooreveal een **selectievakje**. Klik op het profiel foto of een logo tooadd Hallo selectievakje volgende toohello van de groep uw gebruiker toohello **geselecteerde** lijst.

12. **Optioneel:** indien te gewenst**toevoegen van meer dan één groep**, type in een andere **volledige groepsnaam** in Hallo **zoeken op naam of e-mailadres** zoekvak en klikt u op Hallo selectievakje tooadd van deze groep toohello **geselecteerde** lijst.

13. Wanneer u klaar bent met groepen te selecteren, klikt u op Hallo **Selecteer** knop tooadd ze toohello lijst met gebruikers en groepen toobe toegewezen toohello toepassing.

14. **Optioneel:** klikt u op Hallo **rol selecteren** selector in Hallo **toevoegen toewijzing** blade tooselect een rol tooassign toohello groepen die u hebt geselecteerd.

15. Klik op Hallo **toewijzen** knop tooassign Hallo toepassing toohello geselecteerde groepen.

Hallo Toegangsvenster na een korte periode Hallo-gebruikers die u hebt geselecteerd niet kunnen toolaunch deze toepassingen in.

### <a name="check-if-a-user-is-part-of-group-assigned-tooa-license"></a>Controleer of een gebruiker deel van de groep tooa licentie is toegewezen uitmaakt

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **gebruikers en groepen** in het navigatiemenu Hallo.

5.  Klik op **alle gebruikers**.

6.  **Search** voor u geïnteresseerd in het bent Hallo-gebruiker en **klikt u op Hallo rij** tooselect.

7.  Klik op **groepen**.

8.  Klik op Hallo rij van een bepaalde groep.

9.  Klik op **licenties** toosee welke licenties Hallo groep tooit is toegewezen.

   * Hallo Toegangsvenster van de gebruiker als Hallo groep tooan dit mogelijk bepaalde tooappear eerste partij Office-toepassingen inschakelen op Office-licentie is toegewezen.

### <a name="how-tooassign-a-license-tooa-group"></a>Hoe een licentiegroep tooa tooassign

een licentiegroep tooa tooassign Hallo volgende stappen:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **gebruikers en groepen** in het navigatiemenu Hallo.

5.  Klik op **alle groepen**.

6.  **Search** voor u geïnteresseerd in het bent Hallo-groep en **klikt u op Hallo rij** tooselect.

7.  Klik op **licenties** toosee welke licenties Hallo groep momenteel is toegewezen.

8.  Klik op Hallo **toewijzen** knop.

9.  Selecteer **een of meer producten** uit de lijst met beschikbare producten Hallo.

10. **Optionele** klikt u op Hallo **toewijzingsopties** item toogranularly producten toewijzen. Klik op **Ok** wanneer dit is voltooid.

11. Klik op Hallo **toewijzen** knop tooassign deze groep toothis-licenties. Dit kan lang duren, afhankelijk van Hallo omvang en complexiteit van Hallo-groep.

>[!NOTE]
>toodo dit snellere en overweeg tijdelijk een licentie toohello gebruiker rechtstreeks toewijzen. 
>
>

## <a name="next-steps"></a>Volgende stappen
[Toevoegen van nieuwe gebruikers tooAzure Active Directory](active-directory-users-create-azure-portal.md)

