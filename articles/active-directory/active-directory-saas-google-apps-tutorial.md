---
title: 'Zelfstudie: Azure Active Directory-integratie met Google Apps in Azure | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Google Apps.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 38a6ca75-7fd0-4cdc-9b9f-fae080c5a016
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 2093b5ab605ec0d7bbefe7a78e1eede34d756f53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-google-apps"></a>Zelfstudie: Azure Active Directory-integratie met Google Apps

In deze zelfstudie leert u hoe toointegrate Google Apps met Azure Active Directory (Azure AD).

Google Apps integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD wie toegang tot tooGoogle Apps heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooGoogle Apps (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

tooconfigure Azure AD-integratie met Google Apps, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Google Apps eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand hier downloaden: [proefversie aanbieding](https://azure.microsoft.com/pricing/free-trial/).

## <a name="video-tutorial"></a>Zelfstudievideo
Hoe tooEnable Single Sign-On tooGoogle Apps 2 minuten:

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Enable-single-sign-on-to-Google-Apps-in-2-minutes-with-Azure-AD/player]

## <a name="frequently-asked-questions"></a>Veelgestelde vragen
1. **V: Chromebooks en andere apparaten Chrome compatibel zijn met eenmalige aanmelding Azure AD?**
   
    A: Ja, zijn de gebruikers kunnen toosign in hun Chromebook apparaten met hun Azure AD-referenties. Zie dit [Google Apps ondersteunen artikel](https://support.google.com/chrome/a/answer/6060880) voor informatie over gebruikers mogelijk om wordt gevraagd referenties twee keer.

2. **V: als ik eenmalige aanmelding, worden gebruikers kunnen toouse hun toosign Azure AD-referenties in een Google-product, zoals Google leslokaal, GMail, Google Drive, YouTube, enzovoort worden?**
   
    A: Ja, afhankelijk van [welke Google apps](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) u tooenable kiezen of uitschakelt voor uw organisatie.

3. **V: kan ik eenmalige aanmelding voor alleen een subset van mijn gebruikers Google Apps inschakelen?**
   
    A: niet onmiddellijk bij eenmalige aanmelding inschakelen, moet alle uw Google Apps gebruikers tooauthenticate met hun Azure AD-referenties. Omdat Google Apps biedt geen ondersteuning voor meerdere id-providers, Hallo id-provider voor uw Google Apps-omgeving kan Azure AD zijn of Google-- maar niet beide op Hallo hetzelfde moment.

4. **V: als een gebruiker is aangemeld via Windows, worden dat ze automatisch tooGoogle Apps zonder een wachtwoord wordt gevraagd een verificatie?**
   
    A: Er zijn twee opties voor het inschakelen van dit scenario. Eerst gebruikers kunnen aanmelden bij Windows 10-apparaten via [Azure Active Directory Join](active-directory-azureadjoin-overview.md). U kunt ook gebruikers kunnen aanmelden bij Windows-apparaten die lid zijn van een domein tooan on-premises Active Directory die is ingeschakeld voor eenmalige aanmelding tooAzure AD via een [Active Directory Federation Services (AD FS)](active-directory-aadconnect-user-signin.md) implementatie. In beide gevallen moet u tooperform Hallo stappen in de volgende zelfstudie tooenable eenmalige aanmelding tussen Azure AD Hallo en Google Apps.

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Google Apps uit de galerie Hallo toevoegen
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-google-apps-from-hello-gallery"></a>Google Apps uit de galerie Hallo toevoegen
tooconfigure hello integratie van Google Apps in Azure AD, moet u tooadd Google Apps uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Google Apps uit de galerie hello, Voer Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Google Apps**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_search.png)

5. Selecteer in het deelvenster resultaten hello, **Google Apps**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Google Apps op basis van een testgebruiker genaamd "Britta Simon."

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Google Apps is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Google Apps toobe tot stand gebracht.

Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Google Apps.

tooconfigure en eenmalige aanmelding Azure AD-test met Google Apps, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Google Apps](#creating-a-google-apps-test-user)**  -toohave een equivalent van Britta Simon in Google Apps die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Google Apps configureren.

**Voer tooconfigure Azure AD eenmalige aanmelding met Google Apps Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Google Apps** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_samlbase.png)

3. Op Hallo **Google Apps Domain en URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_url.png)

    In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://mail.google.com/a/<yourdomain>`

    > [!NOTE] 
    > Deze waarde is geen echte. Hallo-waarde met de Hallo werkelijke aanmeldings-URL bijwerken. Neem contact op met de Hallo [Google ondersteuningsteam](https://www.google.com/contact/).
 
4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat** en sla Hallo certificaat op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-google-apps-tutorial/tutorial_general_400.png)

6. Op Hallo **Google Apps-configuratie** sectie, klikt u op **Google Apps configureren** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **Sign-Out-URL, SAML Single Sign-On Service-URL en wijzigen wachtwoord URL** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_configure.png) 

7. Een nieuw tabblad openen in uw browser en meld u aan bij Hallo [Google Apps-beheerconsole](http://admin.google.com/) met uw administrator-account.

8. Klik op **beveiliging**. Als er geen Hallo-koppeling, kan het verborgen onder Hallo **meer besturingselementen** menu Hallo onder welkomstscherm aan.
   
    ![Klik op 'Security' (Beveiliging).][10]

9. Op Hallo **beveiliging** pagina, klikt u op **instellen van eenmalige aanmelding (SSO).**
   
    ![Klik op eenmalige aanmelding.][11]

10. Voer Hallo configuratiewijzigingen te volgen:
   
    ![Eenmalige aanmelding configureren][12]
   
    a. Selecteer **Setup-SSO met derden identiteitsprovider**.

    b. In de **aanmelden pagina-URL** veld in Google Apps, plak Hallo-waarde van **Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.

    c. In Hallo **afmelden pagina-URL** veld in Google Apps, plak Hallo-waarde van **Sign-Out URL**, die u hebt gekopieerd vanuit Azure-portal. 

    d. In Hallo **URL voor wachtwoord wijzigen** veld in Google Apps, plak Hallo-waarde van **wijzigen wachtwoord URL**, die u hebt gekopieerd vanuit Azure-portal. 

    e. In Google Apps voor Hallo **verificatiecertificaat**, uploaden Hallo certificaat dat u hebt gedownload vanuit Azure-portal.

    f. Klik op **wijzigingen opslaan**.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
 
### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-google-apps-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-google-apps-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-google-apps-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-google-apps-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-google-apps-test-user"></a>Een testgebruiker Google Apps maken

Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in Google Apps Software van een gebruiker. Google Apps ondersteunt automatische inrichting, dit is standaard ingeschakeld. Er is geen actie voor u in deze sectie. Als een gebruiker in Google Apps Software nog niet bestaat, wordt een nieuwe gemaakt wanneer u tooaccess Google Apps Software probeert.

>[!NOTE] 
>Als u handmatig een gebruiker toocreate nodig, neem dan contact op met de Hallo [Google ondersteuningsteam](https://www.google.com/contact/).

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooGoogle Apps.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooGoogle Apps, voert u Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Google Apps**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie tootest uw eenmalige aanmelding-instellingen, open Toegangsvenster op Hallo [https://myapps.microsoft.com](active-directory-saas-access-panel-introduction.md), meldt u zich bij Hallo test-account en klikt u op **Google Apps** -tegel in Hallo Toegangsvenster.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Gebruikers inrichten configureren](active-directory-saas-google-apps-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_203.png

[0]: ./media/active-directory-saas-google-apps-tutorial/azure-active-directory.png

[5]: ./media/active-directory-saas-google-apps-tutorial/gapps-added.png
[6]: ./media/active-directory-saas-google-apps-tutorial/config-sso.png
[7]: ./media/active-directory-saas-google-apps-tutorial/sso-gapps.png
[8]: ./media/active-directory-saas-google-apps-tutorial/sso-url.png
[9]: ./media/active-directory-saas-google-apps-tutorial/download-cert.png
[10]: ./media/active-directory-saas-google-apps-tutorial/gapps-security.png
[11]: ./media/active-directory-saas-google-apps-tutorial/security-gapps.png
[12]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-config.png
[13]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-confirm.png
[14]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-email.png
[15]: ./media/active-directory-saas-google-apps-tutorial/gapps-api.png
[16]: ./media/active-directory-saas-google-apps-tutorial/gapps-api-enabled.png
[17]: ./media/active-directory-saas-google-apps-tutorial/add-custom-domain.png
[18]: ./media/active-directory-saas-google-apps-tutorial/specify-domain.png
[19]: ./media/active-directory-saas-google-apps-tutorial/verify-domain.png
[20]: ./media/active-directory-saas-google-apps-tutorial/gapps-domains.png
[21]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-domain.png
[22]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-another.png
[23]: ./media/active-directory-saas-google-apps-tutorial/apps-gapps.png
[24]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning.png
[25]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning-auth.png
[26]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin.png
[27]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin-privileges.png
[28]: ./media/active-directory-saas-google-apps-tutorial/gapps-auth.png
[29]: ./media/active-directory-saas-google-apps-tutorial/assign-users.png
[30]: ./media/active-directory-saas-google-apps-tutorial/assign-confirm.png