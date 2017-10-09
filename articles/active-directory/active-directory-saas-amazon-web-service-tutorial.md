---
title: 'Zelfstudie: Azure Active Directory-integratie met Amazon Web Services (AWS) | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Amazon Web Services (AWS).
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7561c20b-2325-4d97-887f-693aa383c7be
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 1b79572ace63f6174ce4fa014c49bf44bd728228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-amazon-web-services-aws"></a>Zelfstudie: Azure Active Directory-integratie met Amazon Web Services (AWS)

In deze zelfstudie leert u hoe toointegrate Amazon Web Services (AWS) met Azure Active Directory (Azure AD).

Amazon Web Services (AWS) integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD wie toegang tot tooAmazon Web Services (AWS heeft)
- U kunt uw gebruikers tooautomatically get aangemelde tooAmazon Web Services (AWS) (Single Sign-On) inschakelen met hun Azure AD-accounts
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

<!--## Overview

tooenable single sign-on with Amazon Web Services (AWS), it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Amazon Web Services (AWS).

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a>Vereisten

tooconfigure Azure AD-integratie met Amazon Web Services (AWS), moet u Hallo volgende items:

- Een Azure AD-abonnement
- Amazon Web Services (AWS) eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Amazon Web Services (AWS) uit de galerie Hallo toe te voegen
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-amazon-web-services-aws-from-hello-gallery"></a>Amazon Web Services (AWS) uit de galerie Hallo toe te voegen
tooconfigure hello integratie van Amazon Web Services (AWS) in Azure AD, moet u tooadd Amazon Web Services (AWS) uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Amazon Web Services (AWS) uit de galerie hello, Voer Hallo stappen te volgen:**

1. In Hallo  **[Azure Portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. Klik op **toevoegen** knop op Hallo Hallo dialoogvenster bovenaan.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Amazon Web Services (AWS)**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_search.png)

5. Selecteer in het deelvenster resultaten hello, **Amazon Web Services (AWS)**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Amazon Web Services (AWS) op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Amazon Web Services (AWS) is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante Hallo-gebruiker in Amazon Web Services (AWS) toobe tot stand gebracht.

Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Amazon Web Services (AWS).

tooconfigure en test eenmalige aanmelding Azure AD met Amazon Web Services (AWS), moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een gebruiker met Amazon Web Services test](#creating-an-amazon-web-services-test-user)**  -toohave een equivalent van Britta Simon in Amazon Web Services (AWS) die is gekoppeld toohello Azure AD-weergave van haar.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing Amazon Web Services (AWS).

**tooconfigure eenmalige aanmelding Azure AD met Amazon Web Services (AWS) uitvoeren Hallo stappen te volgen:**

1. In hello Azure-Portal op Hallo **Amazon Web Services (AWS)** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster als **modus** Selecteer **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_samlbase.png)

3. Op Hallo **Amazon Web Services (AWS) domein en de URL's** sectie, hello gebruiker beschikt niet over tooperform eventuele stappen zoals Hallo app al vooraf is geïntegreerd met Azure.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_url.png)

4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla Hallo XML-bestand op uw computer.
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_certificate.png)

5. Hallo softwaretoepassing Amazon Web Services (AWS) verwacht Hallo SAML asserties in een specifieke indeling. Configureer Hallo claims voor deze toepassing te volgen. U kunt waarden van deze kenmerken Hallo beheren vanuit Hallo '**gebruikerskenmerken**' sectie op de pagina van de toepassing-integratie. Hallo volgende Schermafbeelding toont een voorbeeld voor deze.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_attribute.png)

6. In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals wordt weergegeven in Hallo afbeelding hierboven en uitvoeren van Hallo stappen te volgen:
    
    | Naam van kenmerk  | De waarde van kenmerk | naamruimte |
    | --------------- | --------------- | --------------- |
    | RoleSessionName | User.userPrincipalName | https://AWS.Amazon.com/SAML/Attributes |
    | Rol            | User.assignedroles |  https://AWS.Amazon.com/SAML/Attributes |
    
    >[!TIP]
    >U moet tooconfigure Hallo gebruikers inrichten in Azure AD toofetch alle Hallo-rollen van AWS-Console. Raadpleeg Hallo inrichting van de volgende stappen uit.

    a. Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_04.png)

    b. In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_05.png)

    c. Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij. Hallo Namespace-waarde die is opgegeven hierboven toevoegen.
    
    d. Klik op **OK**.

7. Klik op **opslaan** knop toosave Hallo instellingen in Azure.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_400.png)

8. In een ander browservenster, aanmelding tooyour Amazon Web Services (AWS) bedrijf site als administrator.

9. Klik op **Console-startpagina**.
   
    ![Eenmalige aanmelding configureren][11]

10. Klik op **IAM** van **beveiliging, identiteit en compatibiliteit** service.
   
    ![Eenmalige aanmelding configureren][12]

11. Klik op **identiteitsproviders**, en klik vervolgens op **Provider maken**.
   
    ![Eenmalige aanmelding configureren][13]

12. Op Hallo **Provider configureren** dialoogvenster pagina, voert u Hallo stappen te volgen:
   
    ![Eenmalige aanmelding configureren][14]
 
    a. Als **providertype**, selecteer **SAML**.

    b. In Hallo **providernaam** textbox, typ een providernaam (bijvoorbeeld: *WAAD*).

    c. tooupload uw gedownloade metagegevensbestand, klikt u op **bestand kiezen**.

    d. Klik op **volgende stap**.

13. Op Hallo **providerinformatie controleren** dialoogvenster pagina, klikt u op **maken**. 
    
    ![Eenmalige aanmelding configureren][15]

14. Klik op **rollen**, en klik vervolgens op **nieuwe rol maken**. 
    
    ![Eenmalige aanmelding configureren][16]

15. Op Hallo **rolnaam ingesteld** dialoogvenster Hallo volgende stappen uit te voeren: 
    
    ![Eenmalige aanmelding configureren][17] 

    a. In Hallo **rolnaam** textbox, typ een rolnaam (bijvoorbeeld: *testgebruiker*). 

    b. Klik op **volgende stap**.

16. Op Hallo **Roltype Selecteer** dialoogvenster Hallo volgende stappen uit te voeren: 
    
    ![Eenmalige aanmelding configureren][18] 

    a. Selecteer **rol voor toegang van de Provider identiteit**. 

    b. In Hallo **Grant Web eenmalige aanmelding (WebSSO) toegang tooSAML providers** sectie, klikt u op **Selecteer**.

17. Op Hallo **vertrouwensrelatie tot stand brengen** dialoogvenster Hallo volgende stappen uit te voeren:  
    
    ![Eenmalige aanmelding configureren][19] 

    a. Selecteer als SAML-provider Hallo SAML provider die u eerder hebt gemaakt (bijvoorbeeld: *WAAD*)
  
    b. Klik op **volgende stap**.

18. Op Hallo **controleren rol vertrouwen** dialoogvenster, klikt u op **volgende stap**.
    
    ![Eenmalige aanmelding configureren][32]

19. Op Hallo **beleid koppelen** dialoogvenster, klikt u op **volgende stap**.
    
    ![Eenmalige aanmelding configureren][33]

20. Op Hallo **revisie** dialoogvenster Hallo volgende stappen uit te voeren:
    
    ![Eenmalige aanmelding configureren][34]
 
    a. Klik op **rol maken**.

    b. Zo veel functies naar behoefte maken en deze toohello identiteitsprovider toewijzen.

21. Hallo gebruikersinrichting, toofetch nu alle Hallo-rollen van AWS configureren

    a. In Hallo AWS-Console-aanmelding met het root-account

    b. Klik op de naam van uw in Hallo rechterbovenhoek en klik vervolgens op Hallo **mijn beveiligingsreferenties** optie. Hiermee opent u een scherm als een waarschuwing weergegeven. Klik op de knop Hallo **beveiligingsreferenties** knop toopass Hallo scherm.
        
       ![Eenmalige aanmelding configureren][36]

       ![Eenmalige aanmelding configureren][37]

    c. Klik in het Hallo toegangstoetsen Hallo op de sectie **toegangssleutel maken** knop. Hiermee wordt Hallo toegangssleutel-ID en een token waarde gegenereerd.
    
       ![Eenmalige aanmelding configureren][38]

    d. Kopieer deze beide waarden en ook downloaden, zodat u deze niet kwijtraakt.

    e. Klik in hello Azure-Portal op Hallo Amazon Web Services (AWS) toepassing Integratiepagina **inrichten**.
        
       ![Eenmalige aanmelding configureren][35]

    f. Hallo inrichten modus te instellen**automatische**
        
       ![Eenmalige aanmelding configureren][39]

    g. Nu in Hallo **clientsecret** en **geheim Token** plakt u de bijbehorende waarden hello, die u hebt gekopieerd vanaf AWS-Console.
    
    h. U kunt klikken op Hallo **testverbinding** knop tootest Hallo connectiviteit. Wanneer die is geslaagd kunt u inrichting connector Hallo beginnen.
       
       ![Eenmalige aanmelding configureren][40]

    ik. Nu te inschakelen Hallo inrichten Status**op**. Hallo rollen ophalen uit de toepassing hello wordt gestart.

       ![Eenmalige aanmelding configureren][41]

    > [!NOTE]
    > Azure AD inrichten de service wordt uitgevoerd elke na bepaalde tijd toosync Hallo rollen van AWS. U ziet alle Hallo identiteitsprovider gekoppeld AWS rollen in Azure AD en u ze kunt gebruiken bij het toewijzen van Hallo toepassing toousers of groepen.

<!--### Next steps

tooensure users can sign-in tooAmazon Web Services (AWS) after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Amazon Web Services (AWS) prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooAmazon Web Services (AWS) in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Amazon Web Services (AWS) users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_01.png) 

2. Ga te**gebruikers en groepen** en klik op **alle gebruikers** toodisplay Hallo lijst met gebruikers.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_02.png) 

3. Klik boven Hallo van dialoogvenster Hallo op **toevoegen** tooopen hello **gebruiker** dialoogvenster.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-an-amazon-web-services-test-user"></a>Maken van een testgebruiker Amazon Web Services

In de volgorde tooenable Azure AD gebruikers toolog in tooAmazon Web Services (AWS) als ze in Amazon Web Services (AWS) worden ingericht. In geval van Hallo van Amazon Web Services (AWS) is inrichting een handmatige taak.

**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**

1. Meld u bij tooyour **Amazon Web Services (AWS)** bedrijf site als administrator.

2. Klik op Hallo **Console-startpagina** pictogram. 
   
    ![Eenmalige aanmelding configureren][11]

3. Klik op Identity and Access Management. 
   
    ![Eenmalige aanmelding configureren][28]

4. In Hallo Dashboard, klikt u op **gebruikers**, en klik vervolgens op **Create New Users**. 
   
    ![Eenmalige aanmelding configureren][29]

5. Uitvoeren in het dialoogvenster van de gebruiker maken hello, Hallo stappen te volgen: 
   
    ![Eenmalige aanmelding configureren][30]   
    
    a. In Hallo **Voer gebruikersnamen** tekstvakken, typ de naam van Brita Simon gebruiker (userprincipalname) in Azure AD.

    b. Klik op **maken.**
        
### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen haar toegang tooAmazon Web Services (AWS) verleent.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooAmazon Web Services (AWS), Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Amazon Web Services (AWS)**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Op **rol selecteren** tabblad, selecteer Hallo juiste rol voor Hallo-gebruiker. Alle deze rollen worden weergegeven met de rolnaam Hallo en de naam van de id-provider. Op deze manier kunt u eenvoudig hello rollen van AWS identificeren.

8. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo Amazon Web Services (AWS)-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Amazon Web Services (AWS)-toepassing. 

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_203.png
[11]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795031.png
[12]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795032.png
[13]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795033.png
[14]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795034.png
[15]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795035.png
[16]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795022.png
[17]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795023.png
[18]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795024.png
[19]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795025.png
[20]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950351.png
[21]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_80.png
[22]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950352.png
[23]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_81.png
[24]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950353.png
[25]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_15.png

[28]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950321.png
[29]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795037.png
[30]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795038.png
[32]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950251.png
[33]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950252.png
[34]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950253.png
[35]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning.png
[36]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials.png
[37]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials_continue.png
[38]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_createnewaccesskey.png
[39]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_automatic.png
[40]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_testconnection.png
[41]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_on.png
