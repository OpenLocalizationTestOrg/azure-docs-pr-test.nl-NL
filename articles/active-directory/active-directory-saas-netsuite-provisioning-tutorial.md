---
title: 'Zelfstudie: Azure Active Directory-integratie met Netsuite | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Netsuite.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8a6d3994-ee33-4a6f-b0a2-9d0389467f16
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 5bb2989c1296b9f2abc9e8c84855731adc484aab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-netsuite-for-automatic-user-provisioning"></a>Zelfstudie: Netsuite configureren voor het automatisch gebruikers inrichten

Hallo-doel van deze zelfstudie is tooshow u stappen die u moet tooperform in Netsuite en Azure AD tooautomatically leveren en intrekken gebruikersaccounts vanuit Azure AD tooNetsuite Hallo.

## <a name="prerequisites"></a>Vereisten

Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:

*   Een Azure Active directory-tenant.
*   Een Netsuite eenmalige aanmelding ingeschakeld abonnement.
*   Een gebruikersaccount in Netsuite met beheerdersmachtigingen Team.

## <a name="assigning-users-toonetsuite"></a>Gebruikers tooNetsuite toewijzen

Azure Active Directory gebruikt een concept 'toewijzingen' toodetermine welke gebruikers toegang tooselected apps krijgen genoemd. In de context van de Hallo van automatische gebruikers account inrichten, worden alleen Hallo-gebruikers en groepen die '' tooan toepassing in Azure AD toegewezen zijn gesynchroniseerd.

Voordat u configureren en inschakelen van Hallo-service inricht, moet u toodecide welke gebruikers en/of groepen in Azure AD vertegenwoordigen Hallo-gebruikers die toegang moeten hebben tot tooyour Netsuite app. Als besloten, kunt u deze app-gebruikers tooyour Netsuite toewijzen door hier Hallo-instructies te volgen:

[Toewijzen van een gebruiker of groep tooan enterprise-app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toonetsuite"></a>Belangrijke tips voor het toewijzen van gebruikers tooNetsuite

*   Het is raadzaam om één tooNetsuite tootest Hallo inrichting configuratie door Azure AD-gebruiker is toegewezen. Extra gebruikers en/of groepen kunnen later worden toegewezen.

*   Wanneer u een gebruiker tooNetsuite toewijst, moet u een geldige gebruikersrol. Hallo 'Default toegang' rol werkt niet voor het inrichten.

## <a name="enable-user-provisioning"></a>Gebruikersinrichting inschakelen

Deze sectie helpt u bij het verbinden van uw Azure AD-tooNetsuite gebruikersaccount inrichten API en Hallo service toocreate inrichting configureren, bijwerken en uitschakelen toegewezen gebruikersaccounts in Netsuite op basis van gebruikers en groepen toewijzen in Azure AD.

> [!TIP] 
> U kunt ook tooenabled op basis van SAML eenmalige aanmelding voor Netsuite, in het Hallo-instructies te volgen [Azure-portal](https://portal.azure.com). Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies aanvulling van elkaar.

### <a name="tooconfigure-user-account-provisioning"></a>tooconfigure account gebruikersaanvragen:

Hallo-doel van deze sectie is het toooutline hoe tooNetsuite tooenable gebruikers inrichten van Active Directory-gebruiker accounts.

1. In Hallo [Azure-portal](https://portal.azure.com), bladeren toohello **Azure Active Directory > zakelijke Apps > alle toepassingen** sectie.

2. Als u Netsuite al hebt geconfigureerd voor eenmalige aanmelding, zoekt u uw exemplaar van Netsuite met Hallo zoekveld opgegeven. Selecteer anders **toevoegen** en zoek naar **Netsuite** in Hallo-toepassingsgalerie. Selecteer Netsuite in zoekresultaten hello, en voeg deze tooyour lijst met toepassingen.

3. Selecteer uw exemplaar van Netsuite en vervolgens Hallo **inrichten** tabblad.

4. Set Hallo **modus inrichting** te**automatische**. 

    ![Inrichting](./media/active-directory-saas-netsuite-provisioning-tutorial/provisioning.png)

5. Onder Hallo **beheerdersreferenties** sectie, bieden Hallo na configuratie-instellingen:
   
    a. In Hallo **Beheerdersgebruikersnaam** textbox type een Netsuite accountnaam die heeft Hallo **systeembeheerder** profiel in Netsuite.com toegewezen.
   
    b. In Hallo **beheerderswachtwoord** textbox Hallo een wachtwoord op voor dit account.
      
6. Klik in hello Azure-portal, op **testverbinding** tooensure Azure AD tooyour Netsuite app kunt verbinden.

7. In Hallo **e-mailmelding** Voer Hallo e-mailadres van een persoon of groep die moet inrichting fout meldingen ontvangen en Hallo selectievakje.

8. Klik op **opslaan.**

9. Selecteer onder Hallo toewijzingen sectie, **tooNetsuite synchroniseren Azure Active Directory-gebruikers.**

10. In Hallo **kenmerktoewijzingen** sectie, bekijkt hello gebruikerskenmerken die worden gesynchroniseerd vanuit Azure AD-tooNetsuite. Let op: kenmerken die zijn geselecteerd als Hallo **overeenkomend** eigenschappen zijn gebruikte toomatch Hallo gebruikersaccounts in Netsuite voor update-bewerkingen. Selecteer Hallo knop toocommit wijzigingen zijn opgeslagen.

11. tooenable Hallo inrichting Azure AD-service voor Netsuite, wijziging Hallo **inrichting Status** te**op** in Hallo Zoekinstellingen

12. Klik op **opslaan.**

Hallo initiële synchronisatie van gebruikers en/of groepen die zijn toegewezen tooNetsuite in Hallo gebruikers en groepen sectie begint. Houd er rekening mee dat de initiële synchronisatie Hallo langer tooperform dan het volgende wordt gesynchroniseerd, die ongeveer 20 minuten optreden duurt, zolang het Hallo-service wordt uitgevoerd. U kunt Hallo **synchronisatiedetails** sectie toomonitor uitgevoerd en volgt u koppelingen tooprovisioning activiteitsrapporten, waarin alle bewerkingen die worden uitgevoerd door het Hallo-service op uw app Netsuite inrichting beschrijven.

U kunt nu een testaccount maken. Wacht tot up too20 minuten tooverify die Hallo-account is gesynchroniseerd tooNetsuite.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Het beheren van gebruikers account inrichten voor zakelijke Apps](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Eenmalige aanmelding configureren](active-directory-saas-netsuite-tutorial.md)