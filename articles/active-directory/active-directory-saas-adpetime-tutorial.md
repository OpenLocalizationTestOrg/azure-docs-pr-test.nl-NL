---
title: 'Zelfstudie: Azure Active Directory-integratie met ADP eTime | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en ADP eTime.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a3e9f0be-19ed-4b99-a180-619e7624fc26
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 9a5c7d14a18220f8c7a5b14055c30662ecd8f14d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adp-etime"></a>Zelfstudie: Azure Active Directory-integratie met ADP eTime

In deze zelfstudie leert u hoe toointegrate ADP eTime met Azure Active Directory (Azure AD).

ADP eTime integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD wie toegang tot tooADP eTime heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooADP eTime (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met ADP eTime tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een ADP eTime eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van ADP eTime van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-adp-etime-from-hello-gallery"></a>Het toevoegen van ADP eTime van Hallo-galerie
tooconfigure hello integratie van ADP eTime in Azure AD, moet u tooadd ADP eTime uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd ADP eTime via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **ADP eTime**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_search.png)

5. Selecteer in het deelvenster resultaten hello, **ADP eTime**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met ADP eTime op basis van een testgebruiker genaamd "Britta Simon."

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in ADP eTime is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in ADP eTime toobe tot stand gebracht.

Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in ADP eTime.

tooconfigure en eenmalige aanmelding Azure AD-test met ADP eTime, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een gebruiker ADP eTime test](#creating-an-adp-etime-test-user)**  -toohave een equivalent van Britta Simon in ADP eTime die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw ADP eTime-toepassing.

**Voer tooconfigure Azure AD eenmalige aanmelding met ADP eTime, Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **ADP eTime** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_samlbase.png)

3. Op Hallo **ADP eTime domein en URL's** sectie, voert u Hallo stap:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_url.png)

    a. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<servername>.adp.com`

    b. In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<servername>.adp.com/affwebservices/public/saml2assertionconsumer` 
 
    > [!NOTE] 
    > Deze waarden zijn niet Hallo echte. Deze waarden bijwerken met Hallo werkelijke antwoord-URL en de id. Neem contact op met [ADP eTime ondersteuningsteam](https://www.adp.com/contact-us/overview.aspx) tooget deze waarden.

4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla Hallo XML-bestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_certificate.png) 

5. Hallo ADP eTime toepassing verwacht Hallo SAML asserties in een specifieke indeling waarvoor u tooadd aangepast kenmerk toewijzingen tooyour SAML-token kenmerken-configuratie is vereist. Hallo volgende Schermafbeelding toont een voorbeeld voor deze. Hallo claimnaam altijd worden **'PersonImmutableID'** en het Hallo-waarde die we tooExtensionAttribute2 waarin hebt toegewezen werknemer-id van gebruiker Hallo Hallo. 

    Hier Hallo gebruiker toewijzen van Azure AD tooADP eTime op Hallo werknemer-id wordt uitgevoerd, maar kunt u deze tooa van een andere waarde ook op basis van de toepassingsinstellingen van uw toewijzen. Dus neem werk met [ADP eTime ondersteuningsteam](https://www.adp.com/contact-us/overview.aspx) eerste toouse Hallo juiste id van een gebruiker en wijs die waarde met de Hallo **'PersonImmutableID'** claim.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_attribute.png)

6. In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals in afbeelding Hallo en uitvoeren van Hallo stappen te volgen:
    
    | Naam van kenmerk | De waarde van kenmerk |
    | ------------------- | -------------------- |    
    | PersonImmutableID | User.extensionattribute2 |
    
    a. Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adpetime-tutorial/tutorial_attribute_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adpetime-tutorial/tutorial_attribute_05.png)

    b. In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.

    c. Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij.
    
    d. Klik op **OK**.

    > [!NOTE] 
    > Voordat u de SAML-verklaring Hallo configureren kunt, moet u toocontact uw [ADP eTime ondersteuningsteam](https://www.adp.com/contact-us/overview.aspx) en het Hallo-waarde van de unieke id-kenmerk Hallo aanvraag voor uw tenant. U moet deze waarde tooconfigure Hallo aangepaste claim voor uw toepassing. 

7. Op Hallo **ADP eTime configuratie** sectie, klikt u op **ADP configureren eTime** tooopen **eenmalige aanmelding configureren** venster.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_configure.png) 

8. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adpetime-tutorial/tutorial_general_400.png)

9. tooconfigure eenmalige aanmelding op **ADP eTime** zijde, moet u toosend Hallo gedownload **Metadata XML** te[ADP eTime ondersteuningsteam](https://www.adp.com/contact-us/overview.aspx). 

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adpetime-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adpetime-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adpetime-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adpetime-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-an-adp-etime-test-user"></a>Maken van een gebruiker ADP eTime testen

Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in ADP eTime van een gebruiker. Werken met [ADP eTime ondersteuningsteam](https://www.adp.com/contact-us/overview.aspx) tooadd Hallo gebruikers in Hallo ADP eTime-account. 
   
### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooADP eTime.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooADP eTime, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **ADP eTime**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo ADP eTime tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour ADP eTime toepassing.
Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_203.png

