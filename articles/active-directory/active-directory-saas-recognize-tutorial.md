---
title: 'Zelfstudie: Azure Active Directory-integratie met herkennen | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en herkennen.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cfad939e-c8f4-45a0-bd25-c4eb9701acaa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: f33fc3959f72f875b8c5c4f0abd4e9b6737ca615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-recognize"></a>Zelfstudie: Azure Active Directory-integratie met herkennen

In deze zelfstudie leert u hoe toointegrate herkennen met Azure Active Directory (Azure AD).

Herkennen integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooRecognize toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooRecognize (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

tooconfigure Azure AD-integratie met herkennen, moet u de volgende items Hallo:

- Een Azure AD-abonnement
- Een herkennen eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand hier downloaden: [proefversie aanbieding](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van herkennen van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-recognize-from-hello-gallery"></a>Het toevoegen van herkennen van Hallo-galerie
tooconfigure hello integratie van herkennen in Azure AD, moet u tooadd herkennen van Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd herkennen vanuit Hallo-galerie, Voer Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **herkennen**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_search.png)

5. Selecteer in het deelvenster resultaten hello, **herkennen**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie configureert en test eenmalige aanmelding Azure AD met herkennen op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in herkennen is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in herkennen toobe tot stand gebracht.

Wijs in herkennen, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en Azure AD test eenmalige aanmelding bij het herkennen, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker herkennen](#creating-a-recognize-test-user)**  -toohave een equivalent van Britta Simon in herkennen die gekoppelde toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing herkennen.

**Azure AD tooconfigure eenmalige aanmelding met herkennen, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **herkennen** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_samlbase.png)

3. Op Hallo **domein herkennen en URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_url.png)

    a. In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://recognizeapp.com/<your-domain>/saml/sso`

    b. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://recognizeapp.com/<your-domain>`

    > [!NOTE] 
    > Deze waarden zijn niet echt. Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id. Neem contact op met [Client herkennen support team](mailto:support@recognizeapp.com) ophalen aanmeldings-URL en u de id-waarde kunt ophalen door het openen van Hallo Service Provider metagegevens-URL van Hallo SSO zoekinstellingen die later in Hallo zelfstudie wordt beschreven. . 
 
4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-recognize-tutorial/tutorial_general_400.png)

6. Op Hallo **herkent Configuration** sectie, klikt u op **configureren herkennen** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_configure.png) 

7. In een ander browservenster, aanmelding tooyour herkennen tenant als beheerder.

8. Klik op de rechterbovenhoek Hallo **Menu**. Ga te**bedrijf Admin**.
   
    ![Eenmalige aanmelding op App aan clientzijde configureren](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_000.png)

9. Klik op Hallo navigatiedeelvenster links **instellingen**.
   
    ![Eenmalige aanmelding op App aan clientzijde configureren](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_001.png)

10. Uitvoeren van de volgende stappen uit op Hallo **SSO instellingen** sectie.
   
    ![Eenmalige aanmelding op App aan clientzijde configureren](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_002.png)
    
    a. Als **eenmalige aanmelding inschakelen**, selecteer **ON**.

    b. In Hallo **IDP entiteit-ID** textbox plakken Hallo-waarde van **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal.
    
    c. In Hallo **doel-url voor eenmalige aanmelding** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.
    
    d. In Hallo **Slo-doel-url** textbox plakken Hallo-waarde van **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal. 
    
    e. Open uw gedownloade **certificaat (Base64)** -bestand in Kladblok, kopieer Hallo inhoud ervan naar het Klembord en plak deze toohello **certificaat** textbox.
    
    f. Klik op Hallo **instellingen opslaan** knop. 

11. Naast Hallo **SSO instellingen** sectie, Kopieer de URL Hallo onder **Service Provider metagegevens-url**.
   
    ![Eenmalige aanmelding op App aan clientzijde configureren](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_003.png)

12. Open Hallo **metagegevens-URL koppeling** onder een lege browser toodownload Hallo-document met metagegevens. Kopieer Hallo EntityDescriptor value(entityID) van Hallo-bestand en plak deze in **id** textbox in **sectie domein herkennen en URL's** op Azure-portal.
    
    ![Eenmalige aanmelding op App aan clientzijde configureren](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_004.png)

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-recognize-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-recognize-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-recognize-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-recognize-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-recognize-test-user"></a>Maken van een testgebruiker herkennen

In de volgorde tooenable Azure AD gebruikers toolog in herkennen, moeten ze worden ingericht in herkennen. In geval van herkennen Hallo is inrichting een handmatige taak.

Deze app biedt geen ondersteuning voor het inrichten van SCIM, maar heeft een andere gebruiker synchronisatie die gebruikers richt. 

**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**

1. Meld u aan bij uw bedrijf herkennen site als beheerder.

2. Klik op de rechterbovenhoek Hallo **Menu**. Ga te**bedrijf Admin**.

3. Klik op Hallo navigatiedeelvenster links **instellingen**.

4. Uitvoeren van de volgende stappen uit op Hallo **gebruiker Sync** sectie.
   
   ![Nieuwe gebruiker](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_005.png "nieuwe gebruiker")
   
   a. Als **synchroniseren ingeschakeld**, selecteer **ON**.
   
   b. Als **Kies sync provider**, selecteer **Microsoft / Office 365**.
   
   c. Klik op **Voer gebruiker synchronisatie**.

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooRecognize toegang verleent.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooRecognize, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **herkennen**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.

Als u op Hallo herkennen tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour herkennen toepassing. Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_203.png

