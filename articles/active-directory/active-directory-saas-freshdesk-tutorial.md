---
title: 'Zelfstudie: Azure Active Directory-integratie met FreshDesk | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en FreshDesk.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2a3e5aa-7b5a-4fe4-9285-45dbe6e8efcc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 577a5eb6d9b1bc03030a2b47f63d375869c903bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshdesk"></a>Zelfstudie: Azure Active Directory-integratie met FreshDesk

In deze zelfstudie leert u hoe toointegrate FreshDesk met Azure Active Directory (Azure AD).

FreshDesk integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooFreshDesk toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooFreshDesk (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure Management portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met FreshDesk tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een FreshDesk eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van FreshDesk van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-freshdesk-from-hello-gallery"></a>Het toevoegen van FreshDesk van Hallo-galerie
tooconfigure hello integratie van FreshDesk in Azure AD, moet u tooadd FreshDesk uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd FreshDesk via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure Management Portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. Klik op **toevoegen** knop op Hallo Hallo dialoogvenster bovenaan.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **FreshDesk**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_search.png)

5. Selecteer in het deelvenster resultaten hello, **FreshDesk**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie configureert en test eenmalige aanmelding Azure AD met FreshDesk op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in FreshDesk is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in FreshDesk toobe tot stand gebracht.

Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in FreshDesk.

tooconfigure en eenmalige aanmelding Azure AD-test met FreshDesk, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker FreshDesk](#creating-a-freshdesk-test-user)**  -toohave een equivalent van Britta Simon in FreshDesk die is gekoppeld toohello Azure AD-weergave van haar.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-beheerportal en eenmalige aanmelding in uw toepassing FreshDesk configureren.

**Azure AD tooconfigure eenmalige aanmelding met FreshDesk, Voer Hallo stappen te volgen:**

1. In hello Azure Management portal op Hallo **FreshDesk** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster als **modus** Selecteer **op basis van SAML aanmelding** tooenable voor eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_samlbase.png)

3. Op Hallo **FreshDesk domein en de URL's** sectie, Voer Hallo **aanmeldings-URL** als: `https://<tenant-name>.freshdesk.com` of een andere waarde Freshdesk is voorgesteld.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_url.png)

    > [!NOTE] 
    > Houd er rekening mee dat dit geen de feitelijke waarde is. U moet de waarde wordt bijgewerkt met de werkelijke URL voor eenmalige aanmelding. Neem contact op met [FreshDesk Client ondersteuningsteam](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg) deze waarde op te halen.  

4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat** en sla Hallo certificaat op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-freshdesk-tutorial/tutorial_general_400.png)

6. Op Hallo **FreshDesk configuratie** sectie, klikt u op **FreshDesk configureren** venster tooopen configureren eenmalige aanmelding. Kopieer Hallo SAML Single Sign-On Service-URL en Sign-Out-URL van Hallo **Naslaggids** sectie.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_configure.png)

7. In een ander browservenster, meld u bij uw bedrijf Freshdesk site als beheerder.

8. Klik in het menu bovenaan Hallo Hallo **Admin**.
   
   ![Beheerder](./media/active-directory-saas-freshdesk-tutorial/IC776768.png "Admin")

9. In Hallo **algemene instellingen** tabblad **beveiliging**.
   
   ![Beveiliging](./media/active-directory-saas-freshdesk-tutorial/IC776769.png "beveiliging")

10. In Hallo **beveiliging** sectie, voert u Hallo stappen te volgen:
   
    ![Eenmalige aanmelding](./media/active-directory-saas-freshdesk-tutorial/IC776770.png "eenmalige aanmelding")
   
    a. Voor **eenmalige aanmelding op (SSO)**, selecteer **op**.

    b. Selecteer **SAML SSO**.

    c. Type Hallo **SAML Single Sign-On Service-URL** u vanuit Azure-portal hebt gekopieerd in Hallo **aanmeldings-URL van SAML** textbox.

    d. Type Hallo **Sign-Out URL** u vanuit Azure-portal hebt gekopieerd in Hallo **afmelding URL** textbox.

    e. Kopiëren Hallo **vingerafdruk** waarde van het certificaat Hallo gedownload vanuit Azure-portal en plak deze in Hallo **beveiliging certificaat vingerafdruk** textbox.  
 
    >[!TIP]
    >Zie voor meer informatie [hoe tooretrieve vingerafdrukwaarde van een certificaat](http://youtu.be/YKQF266SAxI). 
    
    f. Klik op **Opslaan**.


### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-beheerportal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure Management portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_01.png) 

2. Ga te**gebruikers en groepen** en klik op **alle gebruikers** toodisplay Hallo lijst met gebruikers.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_02.png) 

3. Klik boven Hallo van dialoogvenster Hallo op **toevoegen** tooopen hello **gebruiker** dialoogvenster.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-freshdesk-test-user"></a>Een testgebruiker FreshDesk maken

In de volgorde tooenable Azure AD gebruikers toolog in FreshDesk, moeten ze worden ingericht in FreshDesk.  
In geval van FreshDesk Hallo is inrichting een handmatige taak.

**tooprovision een gebruikersaccounts uitvoeren Hallo volgende stappen:**

1. Meld u bij tooyour **Freshdesk** tenant.
2. Klik in het menu bovenaan Hallo Hallo **Admin**.
   
   ![Beheerder](./media/active-directory-saas-freshdesk-tutorial/IC776772.png "Admin")

3. In Hallo **algemene instellingen** tabblad **Agents**.
   
   ![Agents](./media/active-directory-saas-freshdesk-tutorial/IC776773.png "Agents")

4. Klik op **nieuwe Agent**.
   
    ![De nieuwe Agent](./media/active-directory-saas-freshdesk-tutorial/IC776774.png "nieuwe-Agent")

5. Op Hallo agentgegevens dialoogvenster uitvoeren Hallo stappen te volgen:
   
   ![Agentgegevens](./media/active-directory-saas-freshdesk-tutorial/IC776775.png "agentgegevens")
   
   a. In Hallo **volledige naam** textbox Hallo-typenaam van de gewenste tooprovision hello Azure AD-account.

   b. In Hallo **e** textbox type hello Azure AD e-mailadres van hello Azure AD-account die u wilt tooprovision.

   c. In Hallo **titel** textbox type Hallo titel van de gewenste tooprovision hello Azure AD-account.

   d. Selecteer **Agents rol**, en klik vervolgens op **toewijzen**.
       
   e. Klik op **Opslaan**.     
   
    >[!NOTE]
    >Hello Azure AD-accounthouder krijgt een e-mailbericht met een account koppelen tooconfirm Hallo voordat deze wordt geactiveerd. 
    > 
    
    >[!NOTE]
    >U kunt andere Freshdesk gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Freshdesk tooprovision AAD-gebruikersaccounts. tooFreshDesk.

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door haar tooBox toegang verlenen.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooFreshDesk, Voer Hallo stappen te volgen:**

1. Open in Hallo Azure Management portal Hallo toepassingen weergeven, en toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **FreshDesk**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo FreshDesk tegel in Hallo Toegangsvenster, krijgt u aanmelding pagina tooget aangemelde tooyour FreshDesk toepassing.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_203.png

