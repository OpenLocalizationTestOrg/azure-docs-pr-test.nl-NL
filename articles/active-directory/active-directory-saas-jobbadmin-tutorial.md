---
title: 'Zelfstudie: Azure Active Directory-integratie met Jobbadmin | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Jobbadmin.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c5208b0d-66a3-49ed-9aad-70d21f54aee0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: 848a6d6d0f072bc3f697ff57756714fc45e7dcc4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jobbadmin"></a>Zelfstudie: Azure Active Directory-integratie met Jobbadmin

In deze zelfstudie leert u hoe Jobbadmin integreren met Azure Active Directory (Azure AD).

Jobbadmin integreren met Azure AD biedt de volgende voordelen:

- U kunt beheren in Azure AD die toegang tot Jobbadmin heeft
- U kunt uw gebruikers automatisch ophalen aangemeld bij Jobbadmin (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - en de Azure-portal beheren

Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Voor het configureren van Azure AD-integratie met Jobbadmin, moet u de volgende items:

- Een Azure AD-abonnement
- Een Jobbadmin eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Jobbadmin uit de galerie toevoegen
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-jobbadmin-from-the-gallery"></a>Jobbadmin uit de galerie toevoegen
Voor het configureren van de integratie van Jobbadmin in Azure AD, moet u Jobbadmin uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.

**Als u wilt toevoegen Jobbadmin uit de galerie, moet u de volgende stappen uitvoeren:**

1. In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer naar **bedrijfstoepassingen**. Ga vervolgens naar **alle toepassingen**.

    ![Toepassingen][2]
    
3. Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak **Jobbadmin**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jobbadmin-tutorial/tutorial_jobbadmin_search.png)

5. Selecteer in het deelvenster resultaten **Jobbadmin**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jobbadmin-tutorial/tutorial_jobbadmin_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Jobbadmin op basis van een testgebruiker genaamd "Britta Simon."

Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Jobbadmin is voor een gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Jobbadmin tot stand worden gebracht.

Wijs in Jobbadmin, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.

Om te configureren en testen van Azure AD eenmalige aanmelding met Jobbadmin, moet u de volgende bouwstenen voltooien:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Jobbadmin](#creating-a-jobbadmin-test-user)**  - Jobbadmin die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.
4. **[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Jobbadmin configureren.

**Voor het configureren van Azure AD eenmalige aanmelding met Jobbadmin, moet u de volgende stappen uitvoeren:**

1. In de Azure-portal op de **Jobbadmin** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jobbadmin-tutorial/tutorial_jobbadmin_samlbase.png)

3. Op de **Jobbadmin domein en de URL's** sectie, voert u de volgende stappen uit:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jobbadmin-tutorial/tutorial_jobbadmin_url.png)

    a. In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<instancename>.jobbnorge.no/auth/saml2/login.ashx`

    b. In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<instancename>.jobnorge.no`

    c. In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://<instancename>.jobbnorge.no/auth/saml2/login.ashx`

    > [!NOTE] 
    > Deze waarden zijn niet echt. Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id. Neem contact op met [Jobbadmin Client ondersteuningsteam](https://www.jobbnorge.no/om-oss/kontakt-oss) ophalen van deze waarden. 
 


4. Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jobbadmin-tutorial/tutorial_jobbadmin_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_400.png)

6. Eenmalige aanmelding configureren op **Jobbadmin** zijde, moet u de gedownloade verzenden **Metadata XML** naar [Jobbadmin ondersteuningsteam](https://www.jobbnorge.no/om-oss/kontakt-oss). Ze deze instelling zodat de SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!  Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan. U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**

1. In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jobbadmin-tutorial/create_aaduser_01.png) 

2. Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jobbadmin-tutorial/create_aaduser_02.png) 

3. Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jobbadmin-tutorial/create_aaduser_03.png) 

4. Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jobbadmin-tutorial/create_aaduser_04.png) 

    a. In de **naam** textbox type **BrittaSimon**.

    b. In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-jobbadmin-test-user"></a>Een testgebruiker Jobbadmin maken

Om Azure AD-gebruikers zich aanmelden bij Jobbadmin, moeten ze worden ingericht in Jobbadmin.
 
Neem contact op met [Jobbadmin ondersteuningsteam](https://www.jobbnorge.no/om-oss/kontakt-oss) ophalen van de gebruikers die zijn toegevoegd aan hun kant.

### <a name="assigning-the-azure-ad-test-user"></a>Toewijzen van de testgebruiker Azure AD

In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Jobbadmin.

![Gebruiker toewijzen][200] 

**Britta Simon om aan te wijzen Jobbadmin, moet u de volgende stappen uitvoeren:**

1. Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met toepassingen **Jobbadmin**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jobbadmin-tutorial/tutorial_jobbadmin_app.png) 

3. Klik in het menu aan de linkerkant op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.

Als u op de tegel Jobbadmin in het deelvenster toegang, krijgt u de aanmeldingspagina van Jobbadmin toepassing.
Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_203.png

