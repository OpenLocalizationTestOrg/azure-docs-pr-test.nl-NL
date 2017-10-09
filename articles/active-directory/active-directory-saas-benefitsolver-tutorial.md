---
title: 'Zelfstudie: Azure Active Directory-integratie met Benefitsolver | Microsoft Docs'
description: Lees hoe toouse Benefitsolver met Azure Active Directory tooenable eenmalige aanmelding, geautomatiseerde inrichting en meer.
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: cf4529b1-3fb6-4475-82b7-2ceedcb70b3c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 5bb8511ef9be1e386956188a93e899d6ebe56ed5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefitsolver"></a>Zelfstudie: Azure Active Directory-integratie met Benefitsolver
Hallo-doel van deze zelfstudie is tooshow Hallo integratie van Azure en Benefitsolver.  

Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:

* Een geldige Azure-abonnement
* Een Benefitsolver eenmalige aanmelding (SSO) ingeschakeld abonnement

Na het voltooien van deze zelfstudie worden hello Azure AD-gebruikers die u hebt toegewezen tooBenefitsolver kunnen toosingle Meld u aan bij Hallo toepassing hello [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).

Hallo scenario beschreven in deze zelfstudie bestaat uit Hallo bouwstenen te volgen:

1. Hallo toepassingsintegratie voor Benefitsolver inschakelen
2. Configureren van eenmalige aanmelding (SSO)
3. Configuratie van gebruikers inrichten
4. Gebruikers toewijzen

![Scenario](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "Scenario")

## <a name="enabling-hello-application-integration-for-benefitsolver"></a>Hallo toepassingsintegratie voor Benefitsolver inschakelen
Hallo-doel van deze sectie is het toooutline hoe tooenable Hallo toepassingsintegratie voor Benefitsolver.

### <a name="tooenable-hello-application-integration-for-benefitsolver-perform-hello-following-steps"></a>tooenable hello toepassingsintegratie voor Benefitsolver, Voer Hallo stappen te volgen:
1. Klik in de klassieke Azure-portal op Hallo navigatiedeelvenster links Hallo op **Active Directory**.
   
   ![Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")
2. Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.
3. tooopen hello toepassingen weergeven in de weergave van de directory hello, klikt u op **toepassingen** in het bovenste menu Hallo.
   
   ![Toepassingen](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "toepassingen")
4. Klik op **toevoegen** Hallo Hallo pagina onderaan in.
   
   ![Toepassing toevoegen](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "toepassing toevoegen")
5. Op Hallo **wat wilt u wilt toodo** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie Hallo**.
   
   ![Een toepassing toevoegen van gallerry](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "een toepassing van gallerry toevoegen")
6. In Hallo **zoekvak**, type **Benefitsolver**.
   
   ![Toepassingsgalerie](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "-Toepassingsgalerie")
7. Selecteer in het deelvenster met resultaten Hallo **Benefitsolver**, en klik vervolgens op **Complete** tooadd Hallo-toepassing.
   
   ![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")
   
## <a name="configure-single-sign-on"></a>Eenmalige aanmelding configureren

Hallo-doel van deze sectie is toooutline hoe tooenable gebruikers tooauthenticate tooBenefitsolver aan hun account in Azure AD dat gebruikmaakt van Federatie gebaseerd op Hallo SAML-protocol.  

Uw toepassing Benefitsolver Hallo SAML asserties verwacht in een specifieke indeling waarvoor u tooadd aangepast kenmerk toewijzingen tooyour **saml-token kenmerken** configuratie. 

Hallo volgende Schermafbeelding toont een voorbeeld voor deze.

![Kenmerken](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "kenmerken")

**tooconfigure eenmalige aanmelding, voert u Hallo stappen te volgen:**

1. In de klassieke Azure-portal op Hallo Hallo **Benefitsolver** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** tooopen hello **configureren eenmalige aanmelding** het dialoogvenster.
   
   ![Eenmalige aanmelding configureren](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "eenmalige aanmelding configureren")
2. Op Hallo **wilt u hoe gebruikers toosign op tooBenefitsolver** pagina **Microsoft Azure AD Single Sign-On**, en klik vervolgens op **volgende**.
   
   ![Eenmalige aanmelding configureren](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "eenmalige aanmelding configureren")
3. Op Hallo **App-instellingen configureren** pagina, voert u Hallo stappen te volgen:
   
   ![App-instellingen configureren](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "App-instellingen configureren")
   
   1. In Hallo **aanmelding op URL** textbox type **http://azure.benefitsolver.com**.
   2. In Hallo **antwoord-URL** textbox type **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**.  
   3. Klik op **Volgende**.
4. Op Hallo **eenmalige aanmelding configureren op Benefitsolver** pagina, toodownload uw metagegevens, klikt u op **metagegevens downloaden**, en sla het bestand met metagegevens Hallo lokaal op uw computer.
   
   ![Eenmalige aanmelding configureren](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "eenmalige aanmelding configureren")
5. Hallo gedownload metagegevens bestand tooyour Benefitsolver ondersteuningsteam verzenden.
   
   >[!NOTE]
   >Het ondersteuningsteam Benefitsolver is toodo Hallo werkelijke SSO-configuratie. U ontvangt een melding wanneer SSO is ingeschakeld voor uw abonnement.
   >

6. Op Hallo klassieke Azure-portal, selecteert u Hallo configuratie voor één aanmelding bevestiging en klik vervolgens op **Complete** tooclose hello **configureren eenmalige aanmelding** dialoogvenster.
   
   ![Eenmalige aanmelding configureren](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "eenmalige aanmelding configureren")
7. Klik in het menu bovenaan Hallo Hallo **kenmerken** tooopen hello **SAML-Token kenmerken** dialoogvenster.
   
   ![Kenmerken](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "kenmerken")
8. Kenmerktoewijzingen tooadd Hallo vereist, voert u Hallo stappen te volgen:
   
   ![Kenmerken](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "kenmerken")
   
   | Naam van kenmerk | De waarde van kenmerk |
   | --- | --- |
   | ClientID |U moet deze waarde tooget van het ondersteuningsteam Benefitsolver. |
   | ClientKey |U moet deze waarde tooget van het ondersteuningsteam Benefitsolver. |
   | LogoutURL |U moet deze waarde tooget van het ondersteuningsteam Benefitsolver. |
   | Werknemer-id |U moet deze waarde tooget van het ondersteuningsteam Benefitsolver. |
   
   1. Klik voor elke gegevensrij in bovenstaande tabel voor Hallo **gebruikerskenmerk toevoegen**.
   2. In Hallo **kenmerknaam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.
   3. In Hallo **kenmerkwaarde** textbox, selecteer Hallo-kenmerkwaarde wordt weergegeven voor die rij.
   4. Klik op **Voltooien**.
9. Klik op **wijzigingen toepassen**.

## <a name="configure-user-provisioning"></a>Gebruikers inrichten configureren
In de volgorde tooenable Azure AD gebruikers toolog in Benefitsolver, moeten ze worden ingericht in Benefitsolver.  

In geval van Benefitsolver Hallo is werknemersgegevens in uw toepassing ingevuld met behulp van een bestand telling van het systeem HRIS (doorgaans elke nacht).  

>[!NOTE]
>U kunt andere Benefitsolver gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Benefitsolver tooprovision AAD-gebruikersaccounts. 
> 

## <a name="assigning-users"></a>Gebruikers toewijzen
tootest uw configuratie, moet u toogrant hello Azure AD-gebruikers gewenste tooallow met behulp van uw toepassing toegang tooit door toe te wijzen.

### <a name="tooassign-users-toobenefitsolver-perform-hello-following-steps"></a>tooassign gebruikers tooBenefitsolver, Hallo volgende stappen uit te voeren:
1. In de klassieke Azure-portal hello, een testaccount te maken.
2. Op Hallo ** Benefitsolver ** toepassing Integratiepagina, klikt u op **gebruikers toewijzen**.
   
   ![Gebruikers toewijzen](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "gebruikers toewijzen")
3. Selecteer uw testgebruiker, klik op **toewijzen**, en klik vervolgens op **Ja** tooconfirm de toewijzing.
   
   ![Ja](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "Ja")

Als u uw instellingen voor eenmalige aanmelding tootest wilt, open Hallo Toegangsvenster. Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).

