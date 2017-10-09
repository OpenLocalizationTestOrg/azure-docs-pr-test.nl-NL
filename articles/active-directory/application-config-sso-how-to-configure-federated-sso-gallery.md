---
title: aaaHow tooconfigure federatieve eenmalige aanmelding voor een galerie van Azure AD-toepassing | Microsoft Docs
description: Hoe tooconfigure federatieve eenmalige aanmelding voor een bestaande-galerie van Azure AD-toepassing en het gebruik zelfstudies tooget snel gaan
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
ms.openlocfilehash: a93de021fddd253e4fe663c221b822d12625fd54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a>Hoe tooconfigure federatieve eenmalige aanmelding voor een galerie van Azure AD-toepassing

Alle toepassingen in hello Azure AD-galerie ingeschakeld met Enterprise single sign-on-functionaliteit is een stapsgewijze zelfstudie beschikbaar. U hebt toegang tot Hallo [lijst met zelfstudies over het toointegrate SaaS-apps met Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) voor gedetailleerde stapsgewijze instructies.

## <a name="overview-of-steps-required"></a>Overzicht van stappen vereist
een toepassing uit de galerie van Azure AD Hallo tooconfigure moet u:

-   [Een toepassing uit de galerie van Azure AD Hallo toevoegen](#add-an-application-from-the-azure-ad-gallery)

-   [Configureren van de toepassing hello metagegevenswaarden in Azure AD (URL,-id en antwoord-URL van de aanmelding)](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [Selecteer gebruikers-id en gebruiker kenmerken toobe verzonden toohello toepassing toevoegen](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [Azure AD-metagegevens en certificaat ophalen](#download-the-azure-ad-metadata-or-certificate)

-   [Azure AD metagegevenswaarden configureren in toepassing hello (aanmelding URL, uitgever, afmelding URL en certificaat)](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [Toohello-toepassing voor gebruikers toewijzen](#assign-users-to-the-application)

## <a name="add-an-application-from-hello-azure-ad-gallery"></a>Een toepassing uit de galerie van Azure AD Hallo toevoegen

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

Na een korte periode, moet u kunnen toosee Hallo van de toepassing configuration blade zijn.

## <a name="configure-single-sign-on-for-an-application-from-hello-azure-ad-gallery"></a>Eenmalige aanmelding voor een toepassing van Hallo-galerie van Azure AD configureren

Volg onderstaande stappen voor Hallo tooconfigure eenmalige aanmelding voor een toepassing:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder**.

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

   1. Klik op **opslaan.** U zien nieuw kenmerk Hallo in Hallo tabel.

13. Klik op **configureren &lt;toepassingsnaam&gt;**  tooaccess documentatie over het tooconfigure eenmalige aanmelding in Hallo-toepassing. U heeft ook Hallo metagegevens-URL's en vereiste certificaat toosetup eenmalige aanmelding met Hallo-toepassing.

14. Klik op **opslaan** toosave Hallo configuratie.

15. Gebruikers toohello toepassing toewijzen.

## <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a>Selecteer gebruikers-id en gebruiker kenmerken toobe verzonden toohello toepassing toevoegen

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

   2. Klik op **Opslaan**. U zien nieuw kenmerk Hallo in Hallo tabel.

## <a name="download-hello-azure-ad-metadata-or-certificate"></a>Azure AD-metagegevens hello of een certificaat downloaden

de metagegevens van de toepassing hello toodownload of het certificaat van Azure AD stappen Hallo volgende:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.

  *  Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle toepassingen**.

6.  Selecteer Hallo-toepassing die u hebt geconfigureerd eenmalige aanmelding.

7.  Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.

8.  Ga te**SAML-certificaat voor ondertekening van** sectie en klik vervolgens op **downloaden** waarde in de kolom. Afhankelijk van welke toepassing hello configureren van eenmalige aanmelding vereist, ziet u beide Hallo optie toodownload Hallo Metadata XML of Hallo certificaat.

Azure AD biedt een URL tooget Hallo metagegevens niet. Hallo metagegevens kan alleen worden opgehaald als een XML-bestand.

## <a name="assign-users-toohello-application"></a>Toohello-toepassing voor gebruikers toewijzen

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

Hallo-gebruikers die u hebt geselecteerd worden na een korte periode, kunnen toolaunch deze toepassingen met behulp van methoden die worden beschreven in Hallo oplossing beschrijving sectie Hallo.

## <a name="customizing-hello-saml-claims-sent-tooan-application"></a>Tooan toepassing aanpassen Hallo SAML claims worden verzonden

toolearn hoe toocustomize Hallo SAML kenmerk claims verzonden tooyour toepassing, Zie [toewijzen in Azure Active Directory-Claims](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) voor meer informatie.

## <a name="next-steps"></a>Volgende stappen
[Bieden van eenmalige aanmelding tooyour apps met toepassingsproxy](active-directory-application-proxy-sso-using-kcd.md)



