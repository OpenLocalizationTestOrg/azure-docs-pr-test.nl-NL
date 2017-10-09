---
title: 'Zelfstudie: Azure Active Directory-integratie met SCC LifeCycle | Microsoft Docs'
description: Lees hoe toouse SCC LifeCycle met Azure Active Directory tooenable eenmalige aanmelding, geautomatiseerde inrichting en meer.
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 9748bf38-ffc3-4d51-a1ae-207ce57104fa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: c10c313c5fc157ed70d2ccecfb930a8a765f8444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scc-lifecycle"></a>Zelfstudie: Azure Active Directory-integratie met SCC levenscyclus
Hallo-doel van deze zelfstudie is tooshow Hallo integratie van Azure en SCC levenscyclus.  

Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:

* Een geldige Azure-abonnement
* Een SCC LifeCycle eenmalige aanmelding (SSO) ingeschakeld abonnement

Na het voltooien van deze zelfstudie hello Azure AD-gebruikers die u hebt toegewezen tooSCC LifeCycle worden kunnen toosingle teken in de toepassing hello op uw site in de levenscyclus van SCC bedrijf (serviceprovider geïnitieerd aanmelding) of met behulp van Hallo [Inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).

Hallo scenario beschreven in deze zelfstudie bestaat uit Hallo bouwstenen te volgen:

1. Hallo toepassingsintegratie voor SCC levenscyclus inschakelen
2. Configureren van eenmalige aanmelding (SSO)
3. Configuratie van gebruikers inrichten
4. Gebruikers toewijzen

![Scenario](./media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "Scenario")

## <a name="enable-hello-application-integration-for-scc-lifecycle"></a>Hallo toepassingsintegratie voor SCC levenscyclus inschakelen
Hallo-doel van deze sectie is het toooutline hoe tooenable Hallo toepassingsintegratie voor SCC levenscyclus.

**tooenable hello toepassingsintegratie voor SCC levenscyclus, Voer Hallo stappen te volgen:**

1. Klik in de klassieke Azure-portal op Hallo navigatiedeelvenster links Hallo op **Active Directory**.
   
    ![Active Directory](./media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "Active Directory")
2. Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.
3. tooopen hello toepassingen weergeven in de weergave van de directory hello, klikt u op **toepassingen** in het bovenste menu Hallo.
   
    ![Toepassingen](./media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "toepassingen")
4. Klik op **toevoegen** Hallo Hallo pagina onderaan in.
   
    ![Toepassing toevoegen](./media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "toepassing toevoegen")
5. Op Hallo **wat wilt u wilt toodo** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie Hallo**.
   
    ![Een toepassing toevoegen van gallerry](./media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "een toepassing van gallerry toevoegen")
6. In Hallo **zoekvak**, type **SCC LifeCycle**.
   
    ![Toepassingsgalerie](./media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "-Toepassingsgalerie")
7. Selecteer in het deelvenster met resultaten Hallo **SCC LifeCycle**, en klik vervolgens op **Complete** tooadd Hallo-toepassing.
   
    ![De levenscyclus van SCC](./media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "SCC levenscyclus")
   
## <a name="configure-single-sign-on"></a>Eenmalige aanmelding configureren

Hallo-doel van deze sectie is toooutline hoe tooenable gebruikers tooauthenticate tooSCC LifeCycle aan hun account in Azure AD dat gebruikmaakt van Federatie gebaseerd op Hallo SAML-protocol.

**tooconfigure eenmalige aanmelding, voert u Hallo stappen te volgen:**

1. In de klassieke Azure-portal op Hallo Hallo **SCC LifeCycle** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** tooopen Hallo ** configureren eenmalige aanmelding ** dialoogvenster.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "eenmalige aanmelding configureren")
2. Op Hallo **wilt u hoe gebruikers toosign op tooSCC LifeCycle** pagina **Microsoft Azure AD Single Sign-On**, en klik vervolgens op **volgende**.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "eenmalige aanmelding configureren")
3. Op Hallo **App-URL configureren** pagina in Hallo **aanmelding op URL** textbox type Hallo URL gebruikt door uw gebruikers toosign op tooyour SCC LifeCycle toepassing hello patroon volgen met '*https:// bs1.SCC.com/lc7/Welcome/Customer/PICTtest.aspx*', en klik vervolgens op **volgende**.
   
    ![App-URL configureren](./media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "App-URL configureren")
4. Op Hallo **eenmalige aanmelding configureren op de levenscyclus van SCC** pagina, klikt u op **metagegevens downloaden**, en sla het bestand met metagegevens lokaal op uw computer.
   
   ![Eenmalige aanmelding configureren](./media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "eenmalige aanmelding configureren")
5. Doorsturen die metagegevens bestand tooSCC LifeCycle Support team.
   
   >[!NOTE]
   >Eenmalige aanmelding heeft toobe ingeschakeld door Hallo SCC LifeCycle ondersteuningsteam.
   > 
   > 

6. Op Hallo klassieke Azure-portal, selecteert u Hallo configuratie voor één aanmelding bevestiging en klik vervolgens op **Complete** tooclose hello **configureren eenmalige aanmelding** dialoogvenster.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "eenmalige aanmelding configureren")
   
## <a name="configure-user-provisioning"></a>Gebruikers inrichten configureren

In volgorde tooenable Azure AD gebruikers toolog in SCC levenscyclus, moeten ze worden ingericht in SCC LifeCycle. Er is geen actie-item voor u tooconfigure gebruikers inrichten tooSCC levenscyclus.

Wanneer een toegewezen gebruiker probeert toolog in SCC levenscyclus, wordt automatisch een SCC LifeCycle-account gemaakt, indien nodig.

>[!NOTE]
>U kunt andere SCC LifeCycle gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door SCC LifeCycle tooprovision AAD-gebruikersaccounts.
> 
> 

## <a name="assign-users"></a>Gebruikers toewijzen
tootest uw configuratie, moet u toogrant hello Azure AD-gebruikers gewenste tooallow met behulp van uw toepassing toegang tooit door toe te wijzen.

**tooassign gebruikers tooSCC levensduur, Voer Hallo stappen te volgen:**

1. In de klassieke Azure-portal hello, een testaccount te maken.
2. Op Hallo ** SCC LifeCycle ** toepassing Integratiepagina, klikt u op **gebruikers toewijzen**.
   
    ![Gebruikers toewijzen](./media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "gebruikers toewijzen")
3. Selecteer uw testgebruiker, klik op **toewijzen**, en klik vervolgens op **Ja** tooconfirm de toewijzing.
   
    ![Ja](./media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "Ja")

Als u uw instellingen SSO tootest wilt, open Hallo Toegangsvenster. Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).

