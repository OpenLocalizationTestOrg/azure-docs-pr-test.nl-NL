---
title: 'Zelfstudie: Azure Active Directory-integratie met werkplek door Facebook | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en werkplek met Facebook.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: jeedes
ms.openlocfilehash: fd19b3f178a2aee7dd2f204d6d3cf6df8fe6b444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a>Zelfstudie: Azure Active Directory-integratie met werkplek door Facebook

In deze zelfstudie leert u hoe toointegrate werkplek door Facebook met Azure Active Directory (Azure AD).

Werkplek door Facebook integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die toegang tooWorkplace door Facebook heeft.
- U kunt uw gebruikers tooautomatically ophalen aangemeld tooWorkplace door Facebook (eenmalige aanmelding) met hun Azure AD-accounts kunt inschakelen.
- U kunt uw accounts op één locatie beheren: hello Azure-portal.

Zie voor meer informatie over de software als een dienst (SaaS)-app-integratie met Azure AD [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met werkplek door Facebook tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een werkplek door Facebook eenmalige aanmelding (SSO) abonnement ingeschakeld

tootest hello stappen in deze zelfstudie volgt u deze aanbevelingen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie kunt u Azure AD SSO testen in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Werkplek door Facebook uit Hallo galerie toevoegen.
2. Configureren en testen eenmalige aanmelding Azure AD.

## <a name="add-workplace-by-facebook-from-hello-gallery"></a>Werkplek door Facebook van Hallo galerie toevoegen
tooconfigure hello integratie van werkplek door Facebook in Azure AD, werkplek door Facebook uit Hallo galerie tooyour lijst met beheerde SaaS-apps toevoegen.

1. In Hallo [Azure-portal](https://portal.azure.com), linkerdeelvenster Hallo in, selecteer **Azure Active Directory**. 

    ![Hello Azure Active Directory-knop][1]

2. Te bladeren**bedrijfstoepassingen** > **alle toepassingen**.

    ![Hallo Enterprise toepassingen blade][2]
    
3. tooadd hello nieuwe toepassing, selecteert **nieuwe toepassing** op Hallo Hallo dialoogvenster bovenaan.

    ![knop voor nieuwe toepassing Hello][3]

4. Typ in het zoekvak Hallo **werkplek door Facebook**, en selecteer **werkplek door Facebook** van resultaten. Selecteer vervolgens **toevoegen**, tooadd Hallo-toepassing.

    ![Werkplek door Facebook in de lijst met resultaten Hallo](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_search.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configureren en testen eenmalige aanmelding Azure AD
In deze sectie kunt u configureren en testen van Azure AD-SSO met werkplek door Facebook, op basis van een testgebruiker genaamd "Britta Simon."

Voor eenmalige aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in werkplek door Facebook is tooa gebruiker in Azure AD. Met andere woorden, moet een gekoppelde relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in werkplek door Facebook worden vastgesteld.

Deze relatie tot stand brengen door toe te wijzen Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in werkplek met Facebook.

### <a name="configure-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In deze sectie kunt u Azure AD-eenmalige aanmelding inschakelen in hello Azure-portal en u eenmalige aanmelding configureren op uw werkplek met Facebook-toepassing.

1. In de Azure-portal op Hallo Hallo **werkplek door Facebook** toepassing Integratiepagina **eenmalige aanmelding**.

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. In Hallo **eenmalige aanmelding** dialoogvenster, **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. In Hallo **werkplek Facebook-domein en URL's** sectie, Hallo te volgen:

    a. In Hallo **aanmeldings-URL** tekstvak, typt u een URL die gebruikmaakt van Hallo patroon volgen:`https://<company subdomain>.facebook.com`

    b. In Hallo **id** tekstvak, typt u een URL die gebruikmaakt van Hallo patroon volgen:`https://www.facebook.com/company/<scim company id>`

    > [!NOTE]
    > Deze waarden zijn alleen een voorbeeld. Deze waarden bijwerken met Hallo werkelijke aanmeldings-URL en -id. Neem contact op met Hallo [werkplek door Facebook Client-ondersteuningsteam](https://workplace.fb.com/faq/) tooget deze waarden. 

4. In Hallo **SAML-certificaat voor ondertekening van** sectie **certificaat (Base64)**, en sla het Hallo-certificaatbestand op uw computer.

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. Selecteer **Opslaan**.

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_400.png)

6. In Hallo **werkplek door Facebook configuratie** sectie **werkplek configureren door Facebook** tooopen hello **eenmalige aanmelding configureren** venster. Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids** sectie.

    ![Werkplek door Facebook-configuratie](./media/active-directory-saas-facebook-at-work-tutorial/config.png) 

7. Meld u tooyour werkplek door Facebook bedrijf site als een beheerder in een ander browservenster.
  
   > [!NOTE] 
   > Als onderdeel van SAML-verificatieproces Hallo kunt werkplek queryreeksen van up too2.5 kilobytes in grootte in volgorde toopass parameters tooAzure AD gebruiken.

8. In Hallo **bedrijf Dashboard**, gaat u toohello **verificatie** tabblad.

9. Onder **SAML-verificatie**, selecteer **eenmalige aanmelding alleen** uit de vervolgkeuzelijst Hallo.

10. Voer Hallo waarden van Hallo gekopieerd **werkplek door Facebook configuratie** sectie van de Azure-portal in de bijbehorende velden Hallo Hallo:

    *   In de **SAML URL** tekstvak plakken Hallo-waarde van **Single Sign-On Service-URL**, die u hebt gekopieerd uit hello Azure-portal.
    *   In de **URL-verlener SAML** tekstvak plakken Hallo-waarde van **SAML entiteit-ID**, die u hebt gekopieerd uit hello Azure-portal.
    *   In **SAML afmelding omleiden (optioneel)**, plak Hallo-waarde van **Sign-Out URL**, die u hebt gekopieerd uit hello Azure-portal.
    *   Open uw **base-64 gecodeerde certificaat** in Kladblok gedownload van hello Azure-portal. Hallo-inhoud van het kopiëren naar het Klembord en plak deze toothe **SAML certificaat** in het tekstvak.

11. Mogelijk moet u tooenter Hallo doelgroep-URL, geadresseerde URL en ACS (Assertion Consumer-Service)-URL, die worden vermeld onder Hallo **SAML-configuratie** sectie.

12. Schuif toohello onder aan de sectie Hallo en schakel **Test SSO**. Een pop-upvenster wordt weergegeven, met de aanmeldingspagina hello Azure AD. tooauthenticate, Voer uw referenties als normaal. Zorg ervoor dat Hallo e-mailadres is geretourneerd door Azure AD is hetzelfde als het werkplekaccount dat u bent aangemeld Hallo Hallo.

13. Als het Hallo-test is voltooid, schuift u toohello onderaan Hallo pagina en selecteer **opslaan**.

14. Iedereen met behulp van werkplek wordt nu weergegeven met Azure AD-aanmeldingspagina voor verificatie.

U kunt een SAML afmeldings-URL die gebruikt toopoint op Afmelden hello Azure AD-pagina worden kan tooconfigure. Als deze instelling is ingeschakeld en geconfigureerd, wordt de gebruiker Hallo is niet langer afmelden pagina gerichte toohello werkplek. In plaats daarvan is Hallo gebruiker omgeleid toohello-URL die is toegevoegd in Hallo SAML afmelden omleidings-instelling.


> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt. Na het toevoegen van deze app van Hallo **Active Directory** > **bedrijfstoepassingen** sectie, selecteert u de Hallo **Single Sign-On** tabblad en toegang Hallo Embedded-documentatie via Hallo **configuratie** sectie Hallo onder aan. Meer informatie over Hallo embedded-documentatie-functie in Hallo [documentatie van Azure AD ingesloten]( https://go.microsoft.com/fwlink/?linkid=845985).

### <a name="configure-reauthentication-frequency"></a>De frequentie van herauthenticatie configureren

U kunt configureren werkplek tooprompt voor een SAML-controle elke dag drie dagen één week, twee weken, één maand of nooit.

> [!NOTE] 
>Hallo minimale waarde voor Hallo SAML-controle voor mobiele toepassingen is ingesteld tooone week.

U kunt ook een SAML opnieuw instellen voor alle gebruikers afdwingen. toodo deze, gebruik Hallo **vereisen SAML-verificatie voor alle gebruikers nu** knop.


### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

1. In Hallo **Azure-portal**, linkerdeelvenster Hallo in, selecteer **Azure Active Directory**.

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en selecteer **alle gebruikers**.
    
    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, **toevoegen**.
 
    ![knop voor Hallo toevoegen](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_03.png) 

4. In Hallo **gebruiker** dialoogvenster vak, Hallo te volgen:
 
    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** in het tekstvak **BrittaSimon**.

    b. In Hallo **gebruikersnaam** tekstvak, type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven**, en schrijf deze op.

    d. Selecteer **Maken**.
 
### <a name="create-a-workplace-by-facebook-test-user"></a>Maken van een werkplek door Facebook testgebruiker

In deze sectie wordt een gebruiker met de naam Britta Simon in werkplek gemaakt door Facebook. Werkplek door Facebook ondersteunt just-in-time-inrichting, die standaard is ingeschakeld.

Er is geen actie voor u in deze sectie. Als een gebruiker niet op de werkplek door Facebook bestaat, wordt een nieuw gemaakt wanneer u tooaccess werkplek probeert met Facebook.

>[!Note]
>Als u handmatig een gebruiker toocreate nodig, neem dan contact op met de Hallo [werkplek door Facebook Client-ondersteuningsteam](https://workplace.fb.com/faq/).

### <a name="assign-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooWorkplace door Facebook.

![Gebruiker toewijzen][200] 

1. In hello Azure weergeven portal, open Hallo toepassingen. Ga toohello directory weergeven, gaat u te**bedrijfstoepassingen**, en selecteer vervolgens **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **werkplek door Facebook**.

    ![Hallo werkplek door Facebook-koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_app.png) 

3. Selecteer in het menu aan de linkerkant Hallo Hallo **gebruikers en groepen**.

    ![de koppeling 'Gebruikers en groepen' Hallo][202] 

4. Selecteer **Toevoegen**. Klik op Hallo **toevoegen toewijzing** deelvenster **gebruikers en groepen**.

    ![Hallo toevoegen toewijzing deelvenster][203]

5. In Hallo **gebruikers en groepen** dialoogvenster, **Britta Simon** in de lijst gebruikers Hallo.

6. In Hallo **gebruikers en groepen** dialoogvenster, **Selecteer**.

7. In Hallo **toevoegen toewijzing** dialoogvenster, **toewijzen**.
    
### <a name="test-single-sign-on"></a>Test eenmalige aanmelding

Als u uw instellingen SSO tootest wilt, open Hallo Toegangsvenster.
Zie voor meer informatie [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).


## <a name="next-steps"></a>Volgende stappen

* Zie Hallo [lijst met zelfstudies over het SaaS-Apps met Azure Active Directory toointegrate](active-directory-saas-tutorial-list.md).
* Lees [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md).
* Meer informatie over het te[configureren gebruikersaanvragen](active-directory-saas-facebook-at-work-provisioning-tutorial.md).



<!--Image references-->

[1]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_203.png

