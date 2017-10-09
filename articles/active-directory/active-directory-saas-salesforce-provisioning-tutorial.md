---
title: 'Zelfstudie: Azure Active Directory-integratie met Salesforce | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Salesforce.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 49384b8b-3836-4eb1-b438-1c46bb9baf6f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: a916be8dbf0b4c6173cda873936a53cd1f3ff12b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-salesforce-for-automatic-user-provisioning"></a>Zelfstudie: Salesforce configureren voor het automatisch gebruikers inrichten

Hallo-doel van deze zelfstudie is tooshow Hallo stappen vereist tooperform in Salesforce en Azure AD tooautomatically leveren en intrekken gebruikersaccounts vanuit Azure AD-tooSalesforce.

## <a name="prerequisites"></a>Vereisten

Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:

*   Een Azure Active directory-tenant.
*   U moet een geldige tenant voor Salesforce voor werk- of Salesforce voor onderwijs hebben. U kunt een gratis proefaccount voor de service.
*   Een gebruikersaccount in Salesforce met beheerdersmachtigingen Team.

## <a name="assigning-users-toosalesforce"></a>Gebruikers tooSalesforce toewijzen

Azure Active Directory gebruikt een concept 'toewijzingen' toodetermine welke gebruikers toegang tooselected apps krijgen genoemd. In de context van de Hallo van automatische gebruikers account inrichten, alleen Hallo-gebruikers en groepen die '' tooan toepassing in Azure AD toegewezen zijn gesynchroniseerd.

Voordat u configureren en inschakelen van Hallo-service inricht, moet u toodecide welke gebruikers en/of groepen in Azure AD vertegenwoordigen Hallo-gebruikers die toegang moeten hebben tot tooyour Salesforce-app. Als besloten, kunt u deze gebruikers tooyour Salesforce-app kunt toewijzen door hier Hallo-instructies te volgen:

[Toewijzen van een gebruiker of groep tooan enterprise-app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toosalesforce"></a>Belangrijke tips voor het toewijzen van gebruikers tooSalesforce

*   Het is raadzaam om één tooSalesforce tootest Hallo inrichting configuratie door Azure AD-gebruiker is toegewezen. Extra gebruikers en/of groepen kunnen later worden toegewezen.

*  Wanneer u een gebruiker tooSalesforce toewijst, moet u een geldige gebruikersrol. Hallo 'Default toegang' rol werkt niet voor inrichting

    > [!NOTE]
    > Deze app kunt u aangepaste rollen uit Salesforce als onderdeel van Hallo inrichtingsproces, welke klant Hallo wil tooselect bij het toewijzen van gebruikers importeren

## <a name="enable-automated-user-provisioning"></a>Geautomatiseerde Gebruikersinrichting inschakelen

Deze sectie helpt u bij het verbinden van uw Azure AD-tooSalesforce gebruikersaccount inrichten API en Hallo service toocreate inrichting configureren, bijwerken en uitschakelen van toegewezen gebruikersaccounts in Salesforce op basis van gebruikers en groepen toewijzen in Azure AD .

>[!Tip]
>U kunt ook tooenabled op basis van SAML eenmalige aanmelding voor Salesforce, in het Hallo-instructies te volgen [Azure-portal](https://portal.azure.com). Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies aanvulling van elkaar.

### <a name="tooconfigure-automatic-user-account-provisioning"></a>tooconfigure automatische account gebruikersaanvragen:

Hallo-doel van deze sectie is het toooutline hoe tooSalesforce tooenable gebruikers inrichten van Active Directory-gebruiker accounts.

1. In Hallo [Azure-portal](https://portal.azure.com), bladeren toohello **Azure Active Directory > zakelijke Apps > alle toepassingen** sectie.

2. Als u Salesforce al hebt geconfigureerd voor eenmalige aanmelding, zoekt u uw exemplaar van Salesforce met Hallo zoekveld opgegeven. Selecteer anders **toevoegen** en zoek naar **Salesforce** in Hallo-toepassingsgalerie. Selecteer Salesforce in zoekresultaten hello, en voeg deze tooyour lijst met toepassingen.

3. Selecteer uw exemplaar van Salesforce en vervolgens Hallo **inrichten** tabblad.

4. Set Hallo **modus inrichting** te**automatische**. 
![inrichting](./media/active-directory-saas-salesforce-provisioning-tutorial/provisioning.png)

5. Onder Hallo **beheerdersreferenties** sectie, bieden Hallo na configuratie-instellingen:
   
    a. In Hallo **Beheerdersgebruikersnaam** textbox type een Salesforce accountnaam die heeft Hallo **systeembeheerder** profiel in Salesforce.com toegewezen.
   
    b. In Hallo **beheerderswachtwoord** textbox Hallo een wachtwoord op voor dit account.

6. tooget uw Salesforce-beveiligingstoken, een nieuw tabblad openen en meld u aan bij Hallo dezelfde Salesforce-beheeraccount. Op Hallo rechtsboven Hallo pagina, klikt u op uw naam en klik vervolgens op **Mijn instellingen**.

     ![Schakel Automatische gebruikersaanvragen](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-my-settings.png "automatische gebruikersinrichting inschakelen")
7. Klik op Hallo navigatiedeelvenster links **persoonlijke** tooexpand Hallo bijbehorende sectie en klik vervolgens op **opnieuw mijn beveiligingstoken**.
  
    ![Schakel Automatische gebruikersaanvragen](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-personal-reset.png "automatische gebruikersinrichting inschakelen")
8. Op Hallo **opnieuw mijn beveiligingstoken** pagina, klikt u op **Security Token opnieuw** knop.

    ![Schakel Automatische gebruikersaanvragen](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-reset-token.png "automatische gebruikersinrichting inschakelen")
9. Controleer Hallo postvak die zijn gekoppeld aan dit admin-account. Zoek naar een e-mailbericht van Salesforce.com die nieuw beveiligingstoken Hallo bevat.
10. Hallo token, gaat u tooyour Azure AD-venster Kopieer en plak deze in Hallo **Socket Token** veld.

11. Klik in hello Azure-portal, op **testverbinding** tooensure Azure AD tooyour Salesforce-app kunt verbinden.

12. In Hallo **e-mailmelding** Voer Hallo e-mailadres van een persoon of groep die moet inrichting fout meldingen ontvangen, en schakel Hallo selectievakje hieronder.

13. Klik op **opslaan.**  
    
14.  Selecteer onder Hallo toewijzingen sectie, **tooSalesforce synchroniseren Azure Active Directory-gebruikers.**

15. In Hallo **kenmerktoewijzingen** sectie, bekijkt hello gebruikerskenmerken die worden gesynchroniseerd vanuit Azure AD-tooSalesforce. Let op: kenmerken die zijn geselecteerd als Hallo **overeenkomend** eigenschappen zijn gebruikte toomatch Hallo gebruikersaccounts in Salesforce voor update-bewerkingen. Selecteer Hallo knop toocommit wijzigingen zijn opgeslagen.

16. tooenable Hallo inrichting Azure AD-service voor Salesforce, wijziging Hallo **inrichting Status** te**op** in Hallo Zoekinstellingen

17. Klik op **opslaan.**

Hiermee start u de initiële synchronisatie Hallo van gebruikers en/of groepen die zijn toegewezen tooSalesforce in Hallo gebruikers en groepen sectie. Houd er rekening mee dat de initiële synchronisatie Hallo langer tooperform dan het volgende wordt gesynchroniseerd, die ongeveer 20 minuten optreden duurt, zolang het Hallo-service wordt uitgevoerd. U kunt Hallo **synchronisatiedetails** sectie toomonitor uitgevoerd en volgt u koppelingen tooprovisioning activiteitsrapporten, waarin alle bewerkingen die worden uitgevoerd door het Hallo-service op uw Salesforce-app inrichten.

U kunt nu een testaccount maken. Wacht tot up too20 minuten tooverify die Hallo-account is gesynchroniseerd tooSalesforce.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Het beheren van gebruikers account inrichten voor zakelijke Apps](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Eenmalige aanmelding configureren](active-directory-saas-salesforce-tutorial.md)