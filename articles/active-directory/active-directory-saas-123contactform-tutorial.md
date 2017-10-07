---
title: 'Zelfstudie: Azure Active Directory-integratie met 123ContactForm | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en 123ContactForm.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5211910a-ab96-4709-959a-524c4d57c43e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 931255887845edd1aa7f53b9051a82a2f898e055
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-123contactform"></a>Zelfstudie: Azure Active Directory-integratie met 123ContactForm

In deze zelfstudie leert u hoe toointegrate 123ContactForm met Azure Active Directory (Azure AD).

123ContactForm integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die too123ContactForm toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde too123ContactForm inschakelen (Single Sign-On) met hun Azure AD-accounts
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met 123ContactForm tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een 123ContactForm eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van 123ContactForm van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-123contactform-from-hello-gallery"></a>Het toevoegen van 123ContactForm van Hallo-galerie
tooconfigure hello integratie van 123ContactForm in Azure AD, moet u tooadd 123ContactForm uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd 123ContactForm via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **123ContactForm**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_search.png)

5. Selecteer in het deelvenster resultaten hello, **123ContactForm**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met 123ContactForm op basis van een testgebruiker genaamd "Britta Simon."

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in 123ContactForm is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in 123ContactForm toobe tot stand gebracht.

Wijs in 123ContactForm, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met 123ContactForm, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker 123ContactForm](#creating-a-123contactform-test-user)**  -toohave een equivalent van Britta Simon in 123ContactForm die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing 123ContactForm configureren.

**Azure AD tooconfigure eenmalige aanmelding met 123ContactForm, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **123ContactForm** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_samlbase.png)

3. Op Hallo **123ContactForm domein en de URL's** sectie, indien gewenst tooconfigure Hallo toepassing in **IDP geïnitieerd modus**, Hallo volgende stappen uit te voeren:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-123contactform-tutorial/url1.png)

    a. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://www.123contactform.com/saml/azure_ad/<tenant_id>/metadata`

    b. In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://www.123contactform.com/saml/azure_ad/<tenant_id>/acs`

4. U kunt eventueel tooconfigure Hallo toepassing in **SP geïnitieerd modus**, Hallo volgende stappen uit te voeren:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-123contactform-tutorial/url2.png)

    a. Klik op Hallo **weergeven geavanceerde instellingen voor URL** optie

    b. In Hallo **aanmelding op URL** textbox, typ een URL als:`https://www.123contactform.com/saml/azure_ad/<tenant_id>/sso`

    > [!NOTE] 
    > Deze waarden zijn niet echt. U moet deze waarde van de werkelijke URL's en -id die is beschreven verderop in de zelfstudie Hallo tooupdate.
    
5. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_certificate.png) 

6. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-123contactform-tutorial/tutorial_general_400.png)

7. tooconfigure eenmalige aanmelding op **123ContactForm** zijde, gaat u te[https://www.123contactform.com/form-2709121/](https://www.123contactform.com/form-2709121/) en Hallo stappen uitvoeren:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-123contactform-tutorial/submit.png) 

    a. In Hallo **e** textbox type Hallo e-mailadres van Internet Explorer Hallo-gebruiker **BrittaSimon@Contoso.com**.

    b. Klik op **uploaden** en blader Hallo Metadata XML-bestand, dat u hebt gedownload vanuit Azure-portal.

    c. Klik op **indienen formulier**.

8. Op Hallo **Microsoft Azure AD eenmalige aanmelding - Appinstellingen** Hallo volgende stappen uit te voeren:
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-123contactform-tutorial/url3.png)

    a. Als u wilt dat tooconfigure Hallo toepassing in **IDP geïnitieerd modus**, kopie Hallo **id** waarde voor uw exemplaar en plak deze in **id** textbox in **123ContactForm domein en de URL's** sectie op Azure-portal.
    
    b. Als u wilt dat tooconfigure Hallo toepassing in **IDP geïnitieerd modus**, kopie Hallo **antwoord-URL** waarde voor uw exemplaar en plak deze in **antwoord-URL** textbox in **123ContactForm domein en de URL's** sectie op Azure-portal.

    c. Als u wilt dat tooconfigure Hallo toepassing in **SP geïnitieerd modus**, kopie Hallo **SIGN-ON-URL** waarde voor uw exemplaar en plak deze in **aanmelding op URL** textbox in **123ContactForm domein en de URL's** sectie op Azure-portal.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-123contactform-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-123contactform-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-123contactform-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-123contactform-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-123contactform-test-user"></a>Een testgebruiker 123ContactForm maken

Toepassing ondersteunt Just in tijd gebruikers inrichten en na verificatie gebruikers wordt in de toepassing hello automatisch gemaakt.

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen too123ContactForm toegang verleent.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon too123ContactForm, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **123ContactForm**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo 123ContactForm tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour 123ContactForm toepassing.
Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_203.png

