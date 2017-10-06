---
title: 'Zelfstudie: Azure Active Directory-integratie met werkplek door Facebook | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en werkplek met Facebook.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: f71a59527394730757d501a973251dc293fd3683
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a>Zelfstudie: Azure Active Directory-integratie met werkplek door Facebook

In deze zelfstudie leert u hoe toointegrate werkplek door Facebook met Azure Active Directory (Azure AD).

Werkplek door Facebook integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD wie toegang tot tooWorkplace door Facebook heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooWorkplace door Facebook (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met werkplek door Facebook tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een werkplek met eenmalige aanmelding Facebook abonnement ingeschakeld

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van werkplek door Facebook van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-workplace-by-facebook-from-hello-gallery"></a>Het toevoegen van werkplek door Facebook van Hallo-galerie
tooconfigure hello integratie van werkplek door Facebook in Azure AD, moet u tooadd werkplek door Facebook uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd werkplek door Facebook via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **werkplek door Facebook**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_search.png)

5. Selecteer in het deelvenster resultaten hello, **werkplek door Facebook**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met werkplek door Facebook op basis van een testgebruiker genaamd "Britta Simon."

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in werkplek door Facebook is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in werkplek door Facebook toobe tot stand gebracht.

Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in werkplek met Facebook.

tooconfigure en test eenmalige aanmelding Azure AD met behulp van werkplek door Facebook, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Configureren van Herauthenticatie frequentie](#configuring-reauthentication-frequency)**  -tooconfigure werkplek tooprompt voor een SAML-controle.
3. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
4. **[Maken van een werkplek door Facebook testgebruiker](#creating-a-workplace-by-facebook-test-user)**  -toohave een equivalent van Britta Simon in werkplek door Facebook die gekoppelde toohello Azure AD-weergave van de gebruiker.
5. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
6. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren op uw werkplek met Facebook-toepassing.

**Azure AD tooconfigure eenmalige aanmelding met werkplek door Facebook, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **werkplek door Facebook** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. Op Hallo **werkplek Facebook-domein en URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_url.png)

    a. In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<instancename>.facebook.com`

    b. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://www.facebook.com/company/<instancename>`

    > [!NOTE] 
    > Deze waarden zijn niet Hallo echte. Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id. Neem contact op met [werkplek door Facebook Client-ondersteuningsteam](https://workplace.fb.com/faq/) tooget deze waarden. 

4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_400.png)

6. Op Hallo **werkplek door Facebook configuratie** sectie, klikt u op **werkplek configureren door Facebook** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workplacebyfacebook-tutorial/config.png) 

7. In een ander browservenster, aanmelding tooyour werkplek door Facebook bedrijf site als beheerder.
  
   > [!NOTE] 
   > Als onderdeel van SAML-verificatieproces hello, kan werkplek gebruikmaken van queryreeksen van up grootte in volgorde toopass parameters tooAzure AD too2.5 kB.

8. In Hallo **bedrijf Dashboard**, gaat u toohello **verificatie** tabblad.

9. Onder **SAML-verificatie**, selecteer **eenmalige aanmelding alleen** uit de vervolgkeuzelijst Hallo.

10. Invoer Hallo-waarden die zijn gekopieerd uit **werkplek door Facebook configuratie** sectie van de Azure-portal in de bijbehorende velden Hallo Hallo:

    *   In **SAML URL** textbox plakken Hallo-waarde van **Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.
    *   In **URL-verlener SAML textbox**, plak Hallo-waarde van **SAML entiteit-ID**, die u hebt gekopieerd vanuit Azure-portal.
    *   In **SAML afmelding omleiden** (optioneel) plakken Hallo-waarde van **Sign-Out URL**, die u hebt gekopieerd vanuit Azure-portal.
    *   Open uw **base-64 gecodeerde certificaat** in Kladblok gedownload vanuit Azure-portal Hallo inhoud van het kopiëren naar het Klembord en plak deze toothe **SAML certificaat** textbox.

11. Mogelijk moet u tooenter Hallo doelgroep-URL de URL van de geadresseerde, en URL ACS (Assertion Consumer-Service) die worden vermeld onder Hallo **SAML-configuratie** sectie.

12. Schuif toohello onder aan de sectie Hallo en klikt u op Hallo **Test SSO** knop. Dit resulteert in een pop-upvenster wordt weergegeven met Azure AD-aanmeldingspagina weergegeven. Geef uw referenties in als normale tooauthenticate. 

    **Voor probleemoplossing:** Controleer Hallo e-mailadres wordt geretourneerd door Azure AD is hetzelfde als het werkplekaccount dat u bent aangemeld Hallo Hallo.

13. Zodra het Hallo-test is voltooid, schuif toohello onder aan Hallo pagina en klik op Hallo **opslaan** knop.

14. Alle gebruikers met behulp van werkplek wordt nu weergegeven met Azure AD-aanmeldingspagina voor verificatie.

15. **SAML afmelding omleiden (optioneel)** - 

    U kunt kiezen toooptionally een Url van de afmelding SAML te configureren die de gebruikte toopoint op de pagina voor Azure AD-afmelding kan zijn. Als deze instelling is ingeschakeld en geconfigureerd, langer Hallo gebruiker niet gerichte toohello werkplek afmelding pagina. Hallo-gebruiker worden in plaats daarvan omgeleide toohello-url die is toegevoegd in Hallo SAML afmelding omleiden instelling.


> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="configuring-reauthentication-frequency"></a>Herauthenticatie frequentie configureren

U kunt configureren werkplek tooprompt voor een SAML-controle elke dag drie dagen, week, twee weken, maanden of nooit.

> [!NOTE] 
>Hallo minimale waarde voor Hallo SAML-controle voor mobiele toepassingen is ingesteld tooone week.

U kunt ook een SAML opnieuw instellen voor alle gebruikers met behulp van de knop Hallo afdwingen: vereisen SAML-verificatie voor alle gebruikers nu.


### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-workplace-by-facebook-test-user"></a>Maken van een werkplek door Facebook testgebruiker

In deze sectie wordt een gebruiker met de naam Britta Simon in werkplek gemaakt door Facebook. Werkplek door Facebook ondersteunt just-in-time-inrichting, die standaard is ingeschakeld.

Er is geen actie voor u in deze sectie. Als een gebruiker niet op de werkplek door Facebook bestaat, wordt een nieuw gemaakt wanneer u tooaccess werkplek probeert met Facebook.

>[!Note]
>Als u een gebruiker handmatig, neem contact op met toocreate moet [werkplek door ondersteuningsteam Facebook-Client](https://workplace.fb.com/faq/)

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooWorkplace met Facebook.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooWorkplace door Facebook, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **werkplek door Facebook**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

Als u uw instellingen voor eenmalige aanmelding tootest wilt, open Hallo Toegangsvenster.
Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).


## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Gebruikers inrichten configureren](active-directory-saas-workplacebyfacebook-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_203.png

