---
title: 'Zelfstudie: Azure Active Directory-integratie met Jive | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Jive.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6fbfdbe7-d66c-4305-9fea-76d6a6a92830
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: b1c0d0bc2d79427c055f577fe5f9d30d10f1bbdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-jive-for-user-provisioning"></a>Zelfstudie: Jive configureren voor gebruikers inrichten

Hallo-doel van deze zelfstudie is tooshow u stappen die u moet tooperform in Jive en Azure AD tooautomatically leveren en intrekken gebruikersaccounts vanuit Azure AD tooJive Hallo.

## <a name="prerequisites"></a>Vereisten

Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:

*   Een Azure Active directory-tenant.
*   Een Jive eenmalige aanmelding ingeschakeld abonnement.
*   Een gebruikersaccount in Jive met beheerdersmachtigingen Team.

## <a name="assigning-users-toojive"></a>Gebruikers tooJive toewijzen

Azure Active Directory gebruikt een concept 'toewijzingen' toodetermine welke gebruikers toegang tooselected apps krijgen genoemd. In de context van de Hallo van automatische gebruikers account inrichten, alleen Hallo-gebruikers en groepen die '' tooan toepassing in Azure AD toegewezen zijn gesynchroniseerd.

Voordat u configureren en inschakelen van Hallo-service inricht, moet u toodecide welke gebruikers en/of groepen in Azure AD Hallo-gebruikers die toegang moeten hebben tot tooyour Jive app vertegenwoordigen. Als besloten, kunt u deze app-gebruikers tooyour Jive toewijzen door hier Hallo-instructies te volgen:

[Toewijzen van een gebruiker of groep tooan enterprise-app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toojive"></a>Belangrijke tips voor het toewijzen van gebruikers tooJive

*   Het is raadzaam om één Azure AD-gebruiker tooJive tootest Hallo inrichting configuratie worden toegewezen. Extra gebruikers en/of groepen kunnen later worden toegewezen.

*   Wanneer u een gebruiker tooJive toewijst, moet u een geldige gebruikersrol. Hallo 'Default toegang' rol werkt niet voor het inrichten.

## <a name="enable-user-provisioning"></a>Gebruikersinrichting inschakelen

Deze sectie helpt u bij het verbinden van uw Azure AD-tooJive gebruikersaccount inrichten API en Hallo service toocreate inrichting configureren, bijwerken en uitschakelen toegewezen gebruikersaccounts in Jive op basis van gebruikers en groepen toewijzen in Azure AD.

> [!TIP]
> U kunt ook tooenabled op basis van SAML eenmalige aanmelding voor Jive, in het Hallo-instructies te volgen [Azure-portal](https://portal.azure.com). Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies aanvulling van elkaar.

### <a name="tooconfigure-user-account-provisioning"></a>tooconfigure account gebruikersaanvragen:

Hallo-doel van deze sectie is het toooutline hoe tooJive tooenable gebruikers inrichten van Active Directory-gebruiker accounts.
Als onderdeel van deze procedure bent u vereiste tooprovide het beveiligingstoken van een gebruiker moet u toorequest van Jive.com.

1. In Hallo [Azure-portal](https://portal.azure.com), bladeren toohello **Azure Active Directory > zakelijke Apps > alle toepassingen** sectie.

2. Als u Jive al hebt geconfigureerd voor eenmalige aanmelding, zoekt u uw exemplaar van Jive met Hallo zoekveld opgegeven. Selecteer anders **toevoegen** en zoek naar **Jive** in Hallo-toepassingsgalerie. Selecteer Jive in zoekresultaten hello, en voeg deze tooyour lijst met toepassingen.

3. Selecteer uw exemplaar van Jive en vervolgens Hallo **inrichten** tabblad.

4. Set Hallo **modus inrichting** te**automatische**. 

    ![Inrichting](./media/active-directory-saas-jive-provisioning-tutorial/provisioning.png)

5. Onder Hallo **beheerdersreferenties** sectie, bieden Hallo na configuratie-instellingen:
   
    a. In Hallo **Jive Beheerdersgebruikersnaam** textbox type een Jive accountnaam die heeft Hallo **systeembeheerder** profiel in Jive.com toegewezen.
   
    b. In Hallo **Jive beheerderswachtwoord** textbox Hallo een wachtwoord op voor dit account.
   
    c. In Hallo **Jive Tenant-URL** textbox type Hallo Jive tenant-URL.
      
      > [!NOTE]
      > Hallo Jive tenant-URL is de URL die wordt gebruikt door uw organisatie toolog in tooJive.  
      > Normaal gesproken Hallo-URL heeft Hallo volgende indeling: **www.\< organisatie\>. jive.com**.          

6. Klik in hello Azure-portal, op **testverbinding** tooensure Azure AD tooyour Jive app kunt verbinden.

7. Voer e-mailadres van een persoon of groep die inrichting fout meldingen in Hallo ontvangen moet Hallo **e-mailmelding** veld en controleer de onderstaande Hallo selectievakje.

8. Klik op **opslaan.**

9. Selecteer onder Hallo toewijzingen sectie, **tooJive synchroniseren Azure Active Directory-gebruikers.**

10. In Hallo **kenmerktoewijzingen** sectie, bekijkt hello gebruikerskenmerken die worden gesynchroniseerd vanuit Azure AD-tooJive. kenmerken die zijn geselecteerd als Hallo **overeenkomend** eigenschappen zijn gebruikte toomatch Hallo gebruikersaccounts in Jive voor update-bewerkingen. Selecteer Hallo knop toocommit wijzigingen zijn opgeslagen.

11. tooenable Hallo inrichting Azure AD-service voor Jive, wijziging Hallo **inrichting Status** te**op** in Hallo Zoekinstellingen

12. Klik op **opslaan.**

Hallo initiële synchronisatie van gebruikers en/of groepen die zijn toegewezen tooJive in Hallo gebruikers en groepen sectie begint. de initiële synchronisatie Hallo duurt langer tooperform dan het volgende wordt gesynchroniseerd, die ongeveer 20 minuten optreden, zolang het Hallo-service wordt uitgevoerd. U kunt Hallo **synchronisatiedetails** sectie toomonitor uitgevoerd en volgt u koppelingen tooprovisioning activiteitsrapporten, waarin alle bewerkingen die worden uitgevoerd door het Hallo-service op uw app Jive inrichting beschrijven.

U kunt nu een testaccount maken. Wacht tot up too20 minuten tooverify die Hallo-account is gesynchroniseerd tooJive.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Het beheren van gebruikers account inrichten voor zakelijke Apps](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Eenmalige aanmelding configureren](active-directory-saas-jive-tutorial.md)