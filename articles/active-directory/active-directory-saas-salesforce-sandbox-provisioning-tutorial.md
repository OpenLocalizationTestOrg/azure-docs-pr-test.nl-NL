---
title: 'Zelfstudie: Azure Active Directory-integratie met Salesforce Sandbox | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Salesforce Sandbox.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bab73fda-6754-411d-9288-f73ecdaa486d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: 06ff50050845383a602b0edd6fca953ddd37cebd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-salesforce-sandbox-for-automatic-user-provisioning"></a>Zelfstudie: Sandbox-Salesforce configureren voor het automatisch gebruikers inrichten

Hallo-doel van deze zelfstudie is tooshow Hallo van stappen die u moet tooperform in Salesforce Sandbox en Azure AD tooautomatically leveren en intrekken gebruikersaccounts vanuit Azure AD tooSalesforce Sandbox.

## <a name="prerequisites"></a>Vereisten

Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:

*   Een Azure Active directory-tenant.
*   U moet een geldige tenant voor Salesforce Sandbox voor werk of Salesforce Sandbox voor onderwijs hebben. U kunt een gratis proefaccount voor de service.
*   Een gebruikersaccount in Salesforce Sandbox met beheerdersmachtigingen Team.

## <a name="assigning-users-toosalesforce-sandbox"></a>Toewijzen van gebruikers tooSalesforce Sandbox

Azure Active Directory gebruikt een concept 'toewijzingen' toodetermine welke gebruikers toegang tooselected apps krijgen genoemd. In de context van de Hallo van automatische gebruikers account inrichten, worden alleen Hallo-gebruikers en groepen die '' tooan toepassing in Azure AD toegewezen zijn gesynchroniseerd.

Voordat u configureren en inschakelen van Hallo-service inricht, moet u toodecide welke gebruikers en/of groepen in Azure AD Hallo-gebruikers die toegang moeten hebben tot tooyour Salesforce Sandbox app vertegenwoordigen. Als besloten, kunt u deze gebruikers tooyour Salesforce Sandbox app toewijzen door hier Hallo-instructies te volgen:

[Toewijzen van een gebruiker of groep tooan enterprise-app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toosalesforce-sandbox"></a>Belangrijke tips voor het toewijzen van gebruikers tooSalesforce Sandbox

* Het is raadzaam om één tooSalesforce Sandbox tootest Hallo configuratie inrichten door Azure AD-gebruiker is toegewezen. Extra gebruikers en/of groepen kunnen later worden toegewezen.

* U moet een geldige gebruikersrol selecteren bij het toewijzen van een gebruiker tooSalesforce Sandbox. Hallo 'Default toegang' rol werkt niet voor het inrichten.

> [!NOTE]
> Deze app importeert aangepaste rollen van Salesforce Sandbox als onderdeel van Hallo inrichtingsproces, welke klant Hallo wil tooselect bij het toewijzen van gebruikers.

## <a name="enable-automated-user-provisioning"></a>Geautomatiseerde Gebruikersinrichting inschakelen

Deze sectie helpt u bij het verbinden van uw Azure AD tooSalesforce Sandbox gebruikersaccount inrichten API en Hallo service toocreate inrichting configureren, bijwerken en uitschakelen van de toegewezen gebruiker accounts in het Salesforce-Sandbox op basis van gebruikers en groepen toewijzing in Azure AD.

>[!Tip]
>U kunt ook tooenabled op basis van SAML eenmalige aanmelding voor Salesforce Sandbox, in het Hallo-instructies te volgen [Azure-portal](https://portal.azure.com). Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies aanvulling van elkaar.

### <a name="tooconfigure-automatic-user-account-provisioning"></a>tooconfigure automatische account gebruikersaanvragen:

Hallo-doel van deze sectie is het toooutline hoe tooenable gebruikers inrichten van Active Directory-gebruiker accounts tooSalesforce Sandbox.

1. In Hallo [Azure-portal](https://portal.azure.com), bladeren toohello **Azure Active Directory > zakelijke Apps > alle toepassingen** sectie.

2. Als u Salesforce Sandbox al hebt geconfigureerd voor eenmalige aanmelding, zoekt u uw exemplaar van Salesforce Sandbox met Hallo zoekveld opgegeven. Selecteer anders **toevoegen** en zoek naar **Salesforce Sandbox** in Hallo-toepassingsgalerie. Selecteer Salesforce Sandbox in zoekresultaten hello, en voeg deze tooyour lijst met toepassingen.

3. Selecteer uw exemplaar van Salesforce Sandbox en vervolgens Hallo **inrichten** tabblad.

4. Set Hallo **modus inrichting** te**automatische**. 
    ![inrichting](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/provisioning.png)

5. Onder Hallo **beheerdersreferenties** sectie, bieden Hallo na configuratie-instellingen:
   
    a. In Hallo **Beheerdersgebruikersnaam** textbox type een Sandbox met Salesforce accountnaam die heeft Hallo **systeembeheerder** profiel in Salesforce.com toegewezen.
   
    b. In Hallo **beheerderswachtwoord** textbox Hallo een wachtwoord op voor dit account.

6. tooget het beveiligingstoken Salesforce Sandbox een nieuw tabblad openen en meld u aan bij Hallo dezelfde Salesforce Sandbox-beheeraccount. Op Hallo rechtsboven Hallo pagina, klikt u op uw naam en klik vervolgens op **Mijn instellingen**.

     ![Schakel Automatische gebruikersaanvragen](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-my-settings.png "automatische gebruikersinrichting inschakelen")
7. Klik op Hallo navigatiedeelvenster links **persoonlijke** tooexpand Hallo bijbehorende sectie en klik vervolgens op **opnieuw mijn beveiligingstoken**.
  
    ![Schakel Automatische gebruikersaanvragen](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-personal-reset.png "automatische gebruikersinrichting inschakelen")
8. Op Hallo **opnieuw mijn beveiligingstoken** pagina, klikt u op Hallo **Security Token opnieuw** knop.

    ![Schakel Automatische gebruikersaanvragen](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-reset-token.png "automatische gebruikersinrichting inschakelen")
9. Controleer Hallo postvak die zijn gekoppeld aan dit admin-account. Zoek naar een e-mailbericht van Salesforce Sandbox.com die nieuw beveiligingstoken Hallo bevat.
10. Hallo token, gaat u tooyour Azure AD-venster Kopieer en plak deze in Hallo **Socket Token** veld.

11. In hello Azure-portal, klikt u op **testverbinding** tooensure Azure AD verbinding tooyour Salesforce sandbox-app kunt maken.

12. In Hallo **e-mailmelding** Voer Hallo e-mailadres van een persoon of groep die moet inrichting fout meldingen ontvangen en Hallo selectievakje.

13. Klik op **opslaan.**  
    
14.  Selecteer onder Hallo toewijzingen sectie, **synchroniseren Azure Active Directory: gebruikers tooSalesforce Sandbox.**

15. In Hallo **kenmerktoewijzingen** sectie, bekijkt hello gebruikerskenmerken die worden gesynchroniseerd vanuit Azure AD tooSalesforce Sandbox. kenmerken die zijn geselecteerd als Hallo **overeenkomend** eigenschappen zijn gebruikte toomatch Hallo gebruikersaccounts in Salesforce Sandbox voor update-bewerkingen. Selecteer Hallo knop toocommit wijzigingen zijn opgeslagen.

16. tooenable Hallo inrichting Azure AD-service voor Salesforce Sandbox, wijziging Hallo **inrichting Status** te**op** in Hallo Zoekinstellingen

17. Klik op **opslaan.**


Deze begint de initiële synchronisatie Hallo van alle gebruikers en/of groepen tooSalesforce Sandbox in de sectie gebruikers en groepen Hallo toegewezen. de initiële synchronisatie Hallo duurt langer tooperform dan het volgende wordt gesynchroniseerd, die ongeveer 20 minuten optreden, zolang het Hallo-service wordt uitgevoerd. U kunt Hallo **synchronisatiedetails** sectie toomonitor uitgevoerd en volgt u koppelingen tooprovisioning activiteitsrapporten, waarin alle acties die worden uitgevoerd door Salesforce Sandbox app-service inricht Hallo beschrijven.

U kunt nu een testaccount maken. Wacht tot up too20 minuten tooverify die Hallo-account is gesynchroniseerd toosalesforce.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Het beheren van gebruikers account inrichten voor zakelijke Apps](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Eenmalige aanmelding configureren](active-directory-saas-salesforcesandbox-tutorial.md)