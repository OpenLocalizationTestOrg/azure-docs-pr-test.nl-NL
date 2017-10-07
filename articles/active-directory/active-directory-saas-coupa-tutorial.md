---
title: 'Zelfstudie: Azure Active Directory-integratie met Coupa | Microsoft Docs'
description: Lees hoe toouse Coupa met Azure Active Directory tooenable eenmalige aanmelding, geautomatiseerde inrichting en meer.
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 47f27746-9057-4b9c-991e-3abf77710f73
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 87e98573718d27d408c886466a374a987f58faa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-coupa"></a>Zelfstudie: Azure Active Directory-integratie met Coupa
Hallo-doel van deze zelfstudie is tooshow Hallo integratie van Azure en Coupa.  
Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:

* Een geldige Azure-abonnement
* Een Coupa eenmalige aanmelding (SSO) ingeschakeld abonnement

Na het voltooien van deze zelfstudie worden hello Azure AD-gebruikers die u hebt toegewezen tooCoupa kunnen toosingle Meld u aan bij Hallo toepassing hello [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).

Hallo scenario beschreven in deze zelfstudie bestaat uit Hallo bouwstenen te volgen:

* Hallo toepassingsintegratie voor Coupa inschakelen
* Eenmalige aanmelding configureren
* Configuratie van gebruikers inrichten
* Gebruikers toewijzen

![Scenario](./media/active-directory-saas-coupa-tutorial/IC791897.png "Scenario")

## <a name="enable-hello-application-integration-for-coupa"></a>Hallo toepassingsintegratie voor Coupa inschakelen
Hallo-doel van deze sectie is het toooutline hoe tooenable Hallo toepassingsintegratie voor Coupa.

**tooenable hello toepassingsintegratie voor Coupa, Voer Hallo stappen te volgen:**

1. Klik in de klassieke Azure-portal op Hallo navigatiedeelvenster links Hallo op **Active Directory**.
   
   ![Active Directory](./media/active-directory-saas-coupa-tutorial/IC700993.png "Active Directory")
2. Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.
3. tooopen hello toepassingen weergeven in de weergave van de directory hello, klikt u op **toepassingen** in het bovenste menu Hallo.
   
   ![Toepassingen](./media/active-directory-saas-coupa-tutorial/IC700994.png "toepassingen")
4. Klik op **toevoegen** Hallo Hallo pagina onderaan in.
   
   ![Toepassing toevoegen](./media/active-directory-saas-coupa-tutorial/IC749321.png "toepassing toevoegen")
5. Op Hallo **wat wilt u wilt toodo** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie Hallo**.
   
   ![Een toepassing toevoegen van gallerry](./media/active-directory-saas-coupa-tutorial/IC749322.png "een toepassing van gallerry toevoegen")
6. In Hallo **zoekvak**, type **Coupa**.
   
   ![Toepassingsgalerie](./media/active-directory-saas-coupa-tutorial/IC791898.png "-Toepassingsgalerie")
7. Selecteer in het deelvenster met resultaten Hallo **Coupa**, en klik vervolgens op **Complete** tooadd Hallo-toepassing.
   
   ![Coupa](./media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")
   
## <a name="configure-single-sign-on"></a>Eenmalige aanmelding configureren

Hallo-doel van deze sectie is toooutline hoe tooenable gebruikers tooauthenticate tooCoupa aan hun account in Azure AD dat gebruikmaakt van Federatie gebaseerd op Hallo SAML-protocol.  

Eenmalige aanmelding voor Coupa configureren, moet u een vingerafdrukwaarde van een certificaat tooretrieve. Als u niet bekend met deze procedure bent, Zie [hoe tooretrieve vingerafdrukwaarde van een certificaat](http://youtu.be/YKQF266SAxI).

**tooconfigure eenmalige aanmelding, voert u Hallo stappen te volgen:**

1. Meld u op tooyour Coupa bedrijf site als een beheerder.
2. Ga te**Setup \> beveiligingscontrole**.
   
   ![Beveiligingsmechanismen](./media/active-directory-saas-coupa-tutorial/IC791900.png "beveiligingsmechanismen")
3. toodownload hello Coupa metagegevens bestand tooyour computer, klikt u op **downloaden en importeren van metagegevens van de Serviceprovider**.
   
   ![Coupa SP metagegevens](./media/active-directory-saas-coupa-tutorial/IC791901.png "Coupa SP metagegevens")
4. Aanmelding in een ander browservenster toohello klassieke Azure-portal.
5. Op Hallo **Coupa** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** tooopen hello **configureren eenmalige aanmelding** dialoogvenster.
   
   ![Eenmalige aanmelding configureren](./media/active-directory-saas-coupa-tutorial/IC791902.png "eenmalige aanmelding configureren")
6. Op Hallo **wilt u hoe gebruikers toosign op tooCoupa** pagina **Microsoft Azure AD Single Sign-On**, en klik vervolgens op **volgende**.
   
   ![Eenmalige aanmelding configureren](./media/active-directory-saas-coupa-tutorial/IC791903.png "eenmalige aanmelding configureren")
7. Op Hallo **App-URL configureren** pagina, voert u Hallo stappen te volgen:
   
   ![App-URL configureren](./media/active-directory-saas-coupa-tutorial/IC791904.png "App-URL configureren")   
   1. In Hallo **aanmelding op URL** textbox, typ de URL die wordt gebruikt door uw gebruikers toosign op tooyour Coupa toepassing (bijvoorbeeld: '*http://company.Coupa.com*').
   2. Open het gedownloade Coupa metagegevens-bestand en kopieer Hallo **AssertionConsumerService index/URL**.
   3. In Hallo **Coupa antwoord-URL** textbox plakken Hallo **AssertionConsumerService index/URL** waarde.
   4. Klik op **Volgende**.
8. Op Hallo **eenmalige aanmelding configureren op Coupa** pagina, toodownload uw bestand met metagegevens, klikt u op **metagegevens downloaden**, en sla Hallo bestand lokaal op uw computer.
   
   ![Eenmalige aanmelding configureren](./media/active-directory-saas-coupa-tutorial/IC791905.png "eenmalige aanmelding configureren")
9. Ga te op Hallo Coupa bedrijf site**Setup \> beveiligingscontrole**.
   
   ![Beveiligingsmechanismen](./media/active-directory-saas-coupa-tutorial/IC791900.png "beveiligingsmechanismen")
10. In Hallo **Meld u aan met referenties Coupa** sectie, voert u Hallo stappen te volgen:  

   ![Meld u aan met referenties Coupa](./media/active-directory-saas-coupa-tutorial/IC791906.png "Meld u aan met referenties Coupa") 
   1. Selecteer **aanmelden via SAML**.
   2. Klik op **Bladeren** tooupload het gedownloade bestand voor Azure Active metagegevens.
   3. Klik op **Opslaan**.
11. Op Hallo klassieke Azure-portal, selecteert u Hallo configuratie voor één aanmelding bevestiging en klik vervolgens op **Complete** tooclose hello **configureren eenmalige aanmelding** dialoogvenster.
    
   ![Eenmalige aanmelding configureren](./media/active-directory-saas-coupa-tutorial/IC791907.png "eenmalige aanmelding configureren")
    
## <a name="configure-user-provisioning"></a>Gebruikers inrichten configureren

In de volgorde tooenable Azure AD gebruikers toolog in Coupa, moeten ze worden ingericht in Coupa.  

* In geval van Coupa Hallo is inrichting een handmatige taak.

**tooconfigure gebruikers inrichten, Voer Hallo stappen te volgen:**

1. Meld u bij tooyour **Coupa** bedrijf site als administrator.
2. Klik in het menu bovenaan Hallo Hallo **Setup**, en klik vervolgens op **gebruikers**.
   
   ![Gebruikers](./media/active-directory-saas-coupa-tutorial/IC791908.png "gebruikers")
3. Klik op **Create**.
   
   ![Gebruikers maken](./media/active-directory-saas-coupa-tutorial/IC791909.png "gebruikers maken")
4. In Hallo **gebruiker maken** sectie, voert u Hallo stappen te volgen:
   
   ![Details van gebruiker](./media/active-directory-saas-coupa-tutorial/IC791910.png "Gebruikersdetails")
   
   1. Type Hallo **aanmelding**, **voornaam**, **achternaam**, **Single Sign-On-ID**, **e** kenmerken van een geldige gewenste tooprovision in hello Azure Active Directory-account gerelateerd tekstvakken.
   2. Klik op **Create**.   
   >[!NOTE]
   >Hello Azure Active Directory-accounthouder krijgt een e-mail met een account koppelen tooconfirm Hallo voordat deze geactiveerd wordt. 
   > 

>[!NOTE]
>U kunt andere Coupa gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Coupa tooprovision AAD-gebruikersaccounts. 
> 

## <a name="assign-users"></a>Gebruikers toewijzen
tootest uw configuratie, moet u toogrant hello Azure AD-gebruikers gewenste tooallow met behulp van uw toepassing toegang tooit door toe te wijzen.

**tooassign gebruikers tooCoupa, Hallo volgende stappen uit te voeren:**

1. In de klassieke Azure-portal hello, een testaccount te maken.
2. Op Hallo ** Coupa ** toepassing Integratiepagina, klikt u op **gebruikers toewijzen**.
   
   ![Gebruikers toewijzen](./media/active-directory-saas-coupa-tutorial/IC791911.png "gebruikers toewijzen")
3. Selecteer uw testgebruiker, klik op **toewijzen**, en klik vervolgens op **Ja** tooconfirm de toewijzing.
   
   ![Ja](./media/active-directory-saas-coupa-tutorial/IC767830.png "Ja")

Als u uw instellingen voor eenmalige aanmelding tootest wilt, open Hallo Toegangsvenster. Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).

