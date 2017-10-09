---
title: 'Zelfstudie: Azure Active Directory-integratie met Cisco Spark | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory- en Cisco Spark.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c47894b1-f5df-4755-845d-f12f4c602dc4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 386c4fd816095e1c61de01dd1dee1bbd00311a04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-spark"></a>Zelfstudie: Azure Active Directory-integratie met Cisco Spark

In deze zelfstudie leert u hoe toointegrate Cisco Spark met Azure Active Directory (Azure AD).

Cisco Spark integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD wie toegang tot tooCisco Spark heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooCisco Spark (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Cisco Spark tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Cisco-Spark eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Cisco Spark van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-cisco-spark-from-hello-gallery"></a>Het toevoegen van Cisco Spark van Hallo-galerie
tooconfigure hello integratie van Cisco Spark in Azure AD, moet u tooadd Cisco Spark uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**Cisco Spark via Hallo gallery tooadd uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Cisco Spark**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_search.png)

5. Selecteer in het deelvenster resultaten hello, **Cisco Spark**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Cisco Spark op basis van een testgebruiker genaamd "Britta Simon."

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Cisco Spark is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in Cisco Spark toobe tot stand gebracht.

In een Cisco-Spark Hallo waarde Hallo toewijzen **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met Cisco Spark, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een Cisco-Spark testgebruiker](#creating-a-cisco-spark-test-user)**  -toohave een equivalent van Britta Simon in Cisco Spark die gekoppelde toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing Cisco Spark.

**Voer tooconfigure Azure AD eenmalige aanmelding met Cisco-Spark Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Cisco Spark** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_samlbase.png)

3. Op Hallo **Cisco Spark domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_url.png)

    a. In Hallo **aanmeldings-URL** textbox, typ een URL als:`https://web.ciscospark.com/#/signin`

    b. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://idbroker.webex.com/<companyname>`

    > [!NOTE] 
    > Deze waarde is geen echte. Deze waarde bijwerken Hello werkelijke id. Neem contact op met [Cisco Spark Client ondersteuningsteam](https://support.ciscospark.com/) tooget deze waarde. 
 
4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_certificate.png) 

5. Cisco Spark toepassing verwacht hello SAML asserties toocontain specifieke kenmerken. Configureer Hallo kenmerken voor deze toepassing te volgen. U kunt waarden van deze kenmerken Hallo beheren vanuit Hallo **gebruikerskenmerken** sectie op de pagina van de toepassing-integratie. Hallo volgende Schermafbeelding toont een voorbeeld voor deze.
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_07.png) 

6. In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals wordt weergegeven in Hallo afbeelding hierboven en uitvoeren van Hallo stappen te volgen:
    
    | Naam van kenmerk  | De waarde van kenmerk |
    | --------------- | -------------------- |    
    |   UID    | User.userPrincipalName |   

    a. Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cisco-spark-tutorial/tutorial_attribute_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cisco-spark-tutorial/tutorial_attribute_05.png)
    
    b. In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.
    
    c. Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij.
    
    d. Klik op **OK**.

7. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_400.png)

8. Aanmelden te[Cisco Cloud samenwerking Management](https://admin.ciscospark.com/) met uw volledige beheerdersreferenties.

9. Selecteer **instellingen** en onder Hallo **verificatie** sectie, klikt u op **wijzigen**.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_10.png)
    
10. Selecteer **een 3rd derden identiteitsprovider integreren. (Geavanceerd)**  en ga toohello volgende scherm.

11. Op Hallo **Idp-metagegevens importeren** pagina beide slepen hello Azure AD-metagegevensbestand naar Hallo pagina drop of Hallo bestand browser optie toolocate en gebruik hello Azure AD-metagegevensbestand uploaden. Selecteer **certificaat dat is ondertekend door een certificeringsinstantie in de metagegevens (veiliger) vereisen** en klik op **volgende**. 
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_11.png)

12. Selecteer **SSO testverbinding**, en wanneer er wordt een nieuw browsertabblad geopend, verifiëren met Azure AD met aanmelden.

13. Retourneren van toohello **Cisco Cloud samenwerking Management** browsertabblad. Als het Hallo-test is geslaagd, selecteert u **deze test is geslaagd. Schakel de optie eenmalige aanmelding** en klik op **volgende**.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-cisco-spark-test-user"></a>Maken van een Cisco-Spark testgebruiker

In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Cisco Spark maken. In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Cisco Spark maken.

1. Ga toohello [Cisco Cloud samenwerking Management](https://admin.ciscospark.com/) met uw volledige beheerdersreferenties.

2. Klik op **gebruikers** en vervolgens **gebruikers beheren**.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_12.png) 

3. In Hallo **gebruiker beheren** Selecteer **handmatig toevoegen of wijzigen van gebruikers** en klik op **volgende**.

4. Selecteer **namen en e-mailadres**. Vul vervolgens Hallo textbox als volgt in:
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_13.png) 
    
    a. In Hallo **voornaam** textbox type **Britta**. 
    
    b. In Hallo **achternaam** textbox type **Simon**.
    
    c. In Hallo **e-mailadres** textbox type  **britta.simon@contoso.com** .

5. Klik op Hallo plus tooadd Britta Simon ondertekenen. Klik op **Volgende**.

6. In Hallo **Services toevoegen voor gebruikers** venster, klikt u op **opslaan** en vervolgens **voltooien**.

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooCisco Spark.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooCisco Spark, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Cisco Spark**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

Hallo-doel van deze sectie is tootest uw Azure AD SSO-configuratie met Hallo Toegangsvenster.

Als u op Hallo Cisco Spark-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Cisco Spark-toepassing.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_04.png
[10]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_060.png
[100]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_203.png

