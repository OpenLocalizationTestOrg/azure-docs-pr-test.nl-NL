---
title: 'Zelfstudie: Azure Active Directory-integratie met Qualtrics | Microsoft Docs'
description: Lees hoe toouse Qualtrics met Azure Active Directory tooenable eenmalige aanmelding, geautomatiseerde inrichting en meer.
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 4df889ab-2685-4d15-a163-1ba26567eeda
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 941642e74b90bb13a5ce37ce6665cfa32cd86016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qualtrics"></a>Zelfstudie: Azure Active Directory-integratie met Qualtrics
Hallo-doel van deze zelfstudie is tooshow Hallo integratie van Azure en Qualtrics.  

Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:

* Een geldige Azure-abonnement
* Een Qualtrics eenmalige aanmelding (SSO) ingeschakeld abonnement

Na het voltooien van deze zelfstudie worden hello Azure AD-gebruikers die u hebt toegewezen tooQualtrics kunnen toosingle Meld u aan bij Hallo-toepassing op uw Qualtrics bedrijf site (serviceprovider geïnitieerd aanmelding) of met behulp van Hallo [inleiding toohello Toegang tot Configuratiescherm](active-directory-saas-access-panel-introduction.md).

Hallo scenario beschreven in deze zelfstudie bestaat uit Hallo bouwstenen te volgen:

1. Hallo toepassingsintegratie voor Qualtrics inschakelen
2. Configureren van eenmalige aanmelding (SSO)
3. Configuratie van gebruikers inrichten
4. Gebruikers toewijzen

![Scenario](./media/active-directory-saas-qualtrics-tutorial/IC789542.png "Scenario")

## <a name="enabling-hello-application-integration-for-qualtrics"></a>Hallo toepassingsintegratie voor Qualtrics inschakelen
Hallo-doel van deze sectie is het toooutline hoe tooenable Hallo toepassingsintegratie voor Qualtrics.

**tooenable hello toepassingsintegratie voor Qualtrics, Voer Hallo stappen te volgen:**

1. Klik in de klassieke Azure-portal op Hallo navigatiedeelvenster links Hallo op **Active Directory**.
   
   ![Active Directory](./media/active-directory-saas-qualtrics-tutorial/IC700993.png "Active Directory")
2. Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.
3. tooopen hello toepassingen weergeven in de weergave van de directory hello, klikt u op **toepassingen** in het bovenste menu Hallo.
   
   ![Toepassingen](./media/active-directory-saas-qualtrics-tutorial/IC700994.png "toepassingen")
4. Klik op **toevoegen** Hallo Hallo pagina onderaan in.
   
   ![Toepassing toevoegen](./media/active-directory-saas-qualtrics-tutorial/IC749321.png "toepassing toevoegen")
5. Op Hallo **wat wilt u wilt toodo** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie Hallo**.
   
   ![Een toepassing toevoegen van gallerry](./media/active-directory-saas-qualtrics-tutorial/IC749322.png "een toepassing van gallerry toevoegen")
6. In Hallo **zoekvak**, type **Qualtrics**.
   
   ![Toepassingsgalerie](./media/active-directory-saas-qualtrics-tutorial/IC789543.png "-Toepassingsgalerie")
7. Selecteer in het deelvenster met resultaten Hallo **Qualtrics**, en klik vervolgens op **Complete** tooadd Hallo-toepassing.
   
   ![Qualtrics](./media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")
   
## <a name="configure-single-sign-on"></a>Eenmalige aanmelding configureren

Hallo-doel van deze sectie is toooutline hoe tooenable gebruikers tooauthenticate tooQualtrics aan hun account in Azure AD dat gebruikmaakt van Federatie gebaseerd op Hallo SAML-protocol.

**tooconfigure eenmalige aanmelding, voert u Hallo stappen te volgen:**

1. In de klassieke Azure-portal op Hallo Hallo **Qualtrics** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** tooopen hello **configureren eenmalige aanmelding** dialoogvenster.
   
   ![Eenmalige aanmelding configureren](./media/active-directory-saas-qualtrics-tutorial/IC789545.png "eenmalige aanmelding configureren")
2. Op Hallo **wilt u hoe gebruikers toosign op tooQualtrics** pagina **Microsoft Azure AD Single Sign-On**, en klik vervolgens op **volgende**.
   
   ![Eenmalige aanmelding configureren](./media/active-directory-saas-qualtrics-tutorial/IC789546.png "eenmalige aanmelding configureren")
3. Op Hallo **App-URL configureren** pagina in Hallo **Qualtrics aanmelding op URL** textbox, typ de URL (bijvoorbeeld: '*https://ssotest2ut1.qualtrics.com*'), en klik vervolgens op **Volgende**.
   
   ![App-URL configureren](./media/active-directory-saas-qualtrics-tutorial/IC789547.png "App-URL configureren")
4. Op Hallo **eenmalige aanmelding configureren op Qualtrics** pagina, klikt u op **metagegevens downloaden**, en sla het bestand met metagegevens Hallo op uw computer.
   
   ![Eenmalige aanmelding configureren](./media/active-directory-saas-qualtrics-tutorial/IC789548.png "eenmalige aanmelding configureren")
5. Hallo metagegevens bestand toohello Qualtrics ondersteuningsteam verzenden.
   
   >[!NOTE]
   >Hallo SSO-configuratie heeft toobe uitgevoerd door Hallo Qualtrics ondersteuningsteam. U ontvangt een melding zodra het Hallo-configuratie is voltooid.
   > 
   > 
6. Op Hallo klassieke Azure-portal, selecteert u Hallo configuratie voor één aanmelding bevestiging en klik vervolgens op **Complete** tooclose hello **configureren eenmalige aanmelding** dialoogvenster.
   
   ![Eenmalige aanmelding configureren](./media/active-directory-saas-qualtrics-tutorial/IC789549.png "eenmalige aanmelding configureren")
   
## <a name="configure-user-provisioning"></a>Gebruikers inrichten configureren

Er is geen actie-item voor u tooconfigure gebruikers inrichten tooQualtrics. Wanneer een toegewezen gebruiker toolog in Qualtrics met behulp van het toegangsvenster hello probeert, controleert Qualtrics of Hallo gebruiker bestaat.  

Als er nog geen gebruikersaccount beschikbaar is, wordt het automatisch gemaakt door Qualtrics.

## <a name="assign-users"></a>Gebruikers toewijzen
tootest uw configuratie, moet u toogrant hello Azure AD-gebruikers gewenste tooallow met behulp van uw toepassing toegang tooit door toe te wijzen.

**tooassign gebruikers tooQualtrics, Voer Hallo stappen te volgen:**

1. In de klassieke Azure-portal hello, een testaccount te maken.
2. Op Hallo **Qualtrics** toepassing Integratiepagina, klikt u op **gebruikers toewijzen**.
   
   ![Gebruikers toewijzen](./media/active-directory-saas-qualtrics-tutorial/IC789550.png "gebruikers toewijzen")
3. Selecteer uw testgebruiker, klik op **toewijzen**, en klik vervolgens op **Ja** tooconfirm de toewijzing.
   
   ![Ja](./media/active-directory-saas-qualtrics-tutorial/IC767830.png "Ja")

Als u uw instellingen SSO tootest wilt, open Hallo Toegangsvenster. Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).

