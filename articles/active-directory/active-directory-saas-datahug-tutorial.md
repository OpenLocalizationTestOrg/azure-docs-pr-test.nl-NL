---
title: 'Zelfstudie: Azure Active Directory-integratie met Datahug | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Datahug.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5c0dc1ea-7ff4-4554-b60b-0f2fa9f5abaa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/18/2017
ms.author: jeedes
ms.openlocfilehash: 79ccb939c7a19720bcf696af141f747db00c8a2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-datahug"></a>Zelfstudie: Azure Active Directory-integratie met Datahug

In deze zelfstudie leert u hoe toointegrate Datahug met Azure Active Directory (Azure AD).

Datahug integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooDatahug toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooDatahug (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie. [Wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Datahug tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Datahug eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Datahug van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-datahug-from-hello-gallery"></a>Het toevoegen van Datahug van Hallo-galerie
tooconfigure hello integratie van Datahug in Azure AD, moet u tooadd Datahug uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Datahug via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Datahug**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_search.png)

5. Selecteer in het deelvenster resultaten hello, **Datahug**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Datahug op basis van een testgebruiker genaamd "Britta Simon."

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Datahug is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Datahug toobe tot stand gebracht.

Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Datahug.

tooconfigure en eenmalige aanmelding Azure AD-test met Datahug, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Datahug](#creating-a-datahug-test-user)**  -toohave een equivalent van Britta Simon in Datahug die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Datahug configureren.

**Azure AD tooconfigure eenmalige aanmelding met Datahug, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Datahug** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_samlbase.png)

3. Op Hallo **Datahug domein en de URL's** sectie, indien gewenst tooconfigure Hallo toepassing in **IDP** modus gestart:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_ur1.png)

    a. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://apps.datahug.com/identity/<uniqueID>`

    b. In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://apps.datahug.com/identity/<uniqueID>/acs`

4. Controleer **weergeven geavanceerde instellingen voor URL**. U kunt eventueel tooconfigure Hallo toepassing in **SP** modus gestart:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_url2.png)

    In Hallo **aanmeldings-URL** textbox, typ een URL als:`https://apps.datahug.com/`
     
    > [!NOTE] 
    > Deze waarden zijn niet Hallo echte. Werk deze waarden met Hallo werkelijke id en de antwoord-URL. We raden hier u toouse Hallo unieke waarde van een tekenreeks in Hallo id en de antwoord-URL. Neem contact op met [Datahug Client ondersteuningsteam](http://datahug.com/about/contact-us/) tooget deze waarden. 

5. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_certificate.png) 

6.  Controleer **'Weergeven geavanceerde instellingen voor het ondertekenen van certificaat'** en Hallo stappen uitvoeren:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_cert.png)

    a. In **ondertekening optie**, selecteer **aanmelding SAML-verklaring**.
    
    b. In **ondertekening algoritme**, selecteer **SHA1**.
 
7. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-datahug-tutorial/tutorial_general_400.png)
    
8. Op Hallo **Datahug configuratie** sectie, klikt u op **configureren Datahug** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **SAML entiteit-ID** en **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_configure.png) 

9. tooconfigure eenmalige aanmelding op **Datahug** zijde, moet u toosend Hallo gedownload **Metadata XML**, **SAML entiteit-ID** en **SAML Single Sign-On-Service URL** te[Datahug ondersteuning](http://datahug.com/about/contact-us/). Ze deze toepassing hello toohave SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-datahug-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-datahug-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-datahug-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-datahug-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-datahug-test-user"></a>Een testgebruiker Datahug maken

Azure AD tooenable gebruikers toolog in tooDatahug, ze in Datahug moeten worden ingericht.  
Datahug, inrichting wanneer een handmatige taak is.

**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**

1. Aanmelden tooyour Datahug bedrijf site als beheerder.

2. Beweeg de muisaanwijzer over Hallo **tandwiel** in Hallo rechterbovenhoek en klik op **instellingen**
   
   ![Werknemer toevoegen](./media/active-directory-saas-datahug-tutorial/1.png)

3. Kies **mensen** en klik op Hallo **gebruikers toevoegen** tabblad

    ![Werknemer toevoegen](./media/active-directory-saas-datahug-tutorial/2.png)

4. Typ Hallo e-mailadres van Hallo persoon die u wilt dat toocreate de account die voor en klik op **toevoegen**.

    ![Werknemer toevoegen](./media/active-directory-saas-datahug-tutorial/3.png)

    > [!NOTE] 
    > U kunt registratie mail toouser verzenden door te selecteren **verzenden welkomstbericht** selectievakje.  
    > Als u een account voor Salesforce Hallo welkomstbericht niet verzenden.

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooDatahug toegang verleent.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooDatahug, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Datahug**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.
Als u op Hallo Datahug tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Datahug toepassing. Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](https://msdn.microsoft.com/library/dn308586). 

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_203.png

