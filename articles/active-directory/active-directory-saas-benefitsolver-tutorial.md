---
title: 'Zelfstudie: Azure Active Directory-integratie met Benefitsolver | Microsoft Docs'
description: Meer informatie over het gebruik van Benefitsolver met Azure Active Directory voor het inschakelen van eenmalige aanmelding, geautomatiseerde inrichting en meer!
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
ms.openlocfilehash: 8a13dd5ebd872f86247158379b28bc291a9c9d83
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefitsolver"></a>Zelfstudie: Azure Active Directory-integratie met Benefitsolver
Het doel van deze zelfstudie is om de integratie van Azure en Benefitsolver weer te geven.  

Het scenario in deze zelfstudie wordt ervan uitgegaan dat u al de volgende items hebt:

* Een geldige Azure-abonnement
* Een Benefitsolver eenmalige aanmelding (SSO) ingeschakeld abonnement

Na het voltooien van deze zelfstudie, de Azure AD-gebruikers die u hebt toegewezen aan Benefitsolver kan worden één Meld u aan bij de toepassing met behulp van de [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).

Het scenario in deze zelfstudie bestaat uit de volgende elementen:

1. De integratie van toepassingen voor Benefitsolver inschakelen
2. Configureren van eenmalige aanmelding (SSO)
3. Configuratie van gebruikers inrichten
4. Gebruikers toewijzen

![Scenario](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "Scenario")

## <a name="enabling-the-application-integration-for-benefitsolver"></a>De integratie van toepassingen voor Benefitsolver inschakelen
Het doel van deze sectie is het inschakelen van de integratie van toepassingen voor Benefitsolver overzicht.

### <a name="to-enable-the-application-integration-for-benefitsolver-perform-the-following-steps"></a>Als u wilt de integratie van toepassingen voor Benefitsolver inschakelen, moet u de volgende stappen uitvoeren:
1. Klik in de klassieke Azure-portal op het navigatiedeelvenster links op **Active Directory**.
   
   ![Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")
2. Van de **Directory** , selecteert u de map waarvoor u wilt inschakelen van Active directory-integratie.
3. De weergave toepassingen in de directoryweergave, klikt u op **toepassingen** in het menu bovenaan.
   
   ![Toepassingen](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "toepassingen")
4. Klik op **toevoegen** aan de onderkant van de pagina.
   
   ![Toepassing toevoegen](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "toepassing toevoegen")
5. Op de **wat wilt u doen** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie**.
   
   ![Een toepassing toevoegen van gallerry](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "een toepassing van gallerry toevoegen")
6. In de **zoekvak**, type **Benefitsolver**.
   
   ![Toepassingsgalerie](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "-Toepassingsgalerie")
7. Selecteer in het deelvenster met resultaten **Benefitsolver**, en klik vervolgens op **Complete** de toepassing toevoegen.
   
   ![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")
   
## <a name="configure-single-sign-on"></a>Eenmalige aanmelding configureren

Het doel van deze sectie is om een overzicht van gebruikers om te verifiëren Benefitsolver aan hun account in Azure AD dat gebruikmaakt van Federatie op basis van het SAML-protocol in staat te.  

Uw toepassing Benefitsolver verwacht de SAML-asserties in een specifieke indeling waarvoor u het toevoegen van aangepast kenmerktoewijzingen aan uw **saml-token kenmerken** configuratie. 

De volgende Schermafbeelding toont een voorbeeld voor deze.

![Kenmerken](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "kenmerken")

**Voor het configureren van eenmalige aanmelding, moet u de volgende stappen uitvoeren:**

1. In de klassieke Azure-portal op de **Benefitsolver** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** openen de **configureren eenmalige aanmelding** dialoogvenster.
   
   ![Eenmalige aanmelding configureren](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "eenmalige aanmelding configureren")
2. Op de **hoe wilt u dat gebruikers zich aanmelden op Benefitsolver** pagina **Microsoft Azure AD Single Sign-On**, en klik vervolgens op **volgende**.
   
   ![Eenmalige aanmelding configureren](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "eenmalige aanmelding configureren")
3. Op de **App-instellingen configureren** pagina, voert u de volgende stappen uit:
   
   ![App-instellingen configureren](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "App-instellingen configureren")
   
   1. In de **aanmelding op URL** textbox type **http://azure.benefitsolver.com**.
   2. In de **antwoord-URL** textbox type **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**.  
   3. Klik op **Volgende**.
4. Op de **eenmalige aanmelding configureren op Benefitsolver** pagina voor het downloaden van de metagegevens, klikt u op **metagegevens downloaden**, en sla het bestand met metagegevens lokaal op uw computer.
   
   ![Eenmalige aanmelding configureren](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "eenmalige aanmelding configureren")
5. Het metagegevensbestand van de gedownloade verzenden naar het ondersteuningsteam Benefitsolver.
   
   >[!NOTE]
   >Het ondersteuningsteam Benefitsolver heeft te maken van de werkelijke SSO-configuratie. U ontvangt een melding wanneer SSO is ingeschakeld voor uw abonnement.
   >

6. Bij de klassieke Azure portal, selecteert u de configuratie voor één aanmelding bevestiging en klik op **Complete** sluiten de **configureren eenmalige aanmelding** dialoogvenster.
   
   ![Eenmalige aanmelding configureren](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "eenmalige aanmelding configureren")
7. Klik in het menu bovenaan op **kenmerken** openen de **SAML-Token kenmerken** dialoogvenster.
   
   ![Kenmerken](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "kenmerken")
8. Als u wilt de vereiste kenmerktoewijzingen toevoegen, moet u de volgende stappen uitvoeren:
   
   ![Kenmerken](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "kenmerken")
   
   | Naam van kenmerk | De waarde van kenmerk |
   | --- | --- |
   | ClientID |U moet deze waarde niet ophalen uit het ondersteuningsteam Benefitsolver. |
   | ClientKey |U moet deze waarde niet ophalen uit het ondersteuningsteam Benefitsolver. |
   | LogoutURL |U moet deze waarde niet ophalen uit het ondersteuningsteam Benefitsolver. |
   | Werknemer-id |U moet deze waarde niet ophalen uit het ondersteuningsteam Benefitsolver. |
   
   1. Voor elke gegevensrij in de bovenstaande tabel, klikt u op **gebruikerskenmerk toevoegen**.
   2. In de **kenmerknaam** textbox, typ de naam van het kenmerk wordt weergegeven voor die rij.
   3. In de **kenmerkwaarde** textbox, selecteert u de waarde van het kenmerk wordt weergegeven voor die rij.
   4. Klik op **Voltooien**.
9. Klik op **wijzigingen toepassen**.

## <a name="configure-user-provisioning"></a>Gebruikers inrichten configureren
Om in te schakelen gebruikers van Azure AD aan te melden bij Benefitsolver, moeten ze worden ingericht in Benefitsolver.  

In het geval van Benefitsolver is werknemersgegevens in uw toepassing ingevuld met behulp van een bestand telling van het systeem HRIS (doorgaans elke nacht).  

>[!NOTE]
>U kunt andere Benefitsolver gebruiker account hulpmiddelen voor het maken of API's die is geleverd door Benefitsolver aan inrichten AAD-gebruikersaccounts. 
> 

## <a name="assigning-users"></a>Gebruikers toewijzen
Als u wilt testen van uw configuratie, moet u de Azure AD-gebruikers verlenen die u wilt toestaan dat met behulp van uw toepassing toegang tot deze door toe te wijzen.

### <a name="to-assign-users-to-benefitsolver-perform-the-following-steps"></a>Gebruikers om aan te wijzen Benefitsolver, moet u de volgende stappen uitvoeren:
1. In de klassieke Azure portal een testaccount te maken.
2. Op de ** Benefitsolver ** toepassing Integratiepagina, klikt u op **gebruikers toewijzen**.
   
   ![Gebruikers toewijzen](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "gebruikers toewijzen")
3. Selecteer uw testgebruiker, klik op **toewijzen**, en klik vervolgens op **Ja** om te bevestigen dat de toewijzing.
   
   ![Ja](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "Ja")

Als u testen van uw instellingen voor eenmalige aanmelding wilt, opent u het toegangsvenster. Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).

