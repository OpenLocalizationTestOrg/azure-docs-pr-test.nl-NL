---
title: 'Zelfstudie: Azure Active Directory-integratie met Citrix GoToMeeting | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Citrix GoToMeeting.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f59fedb-2cf8-48d2-a5fb-222ed943ff78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 3c6eed5309dfa384c292b0cf63f8aa58988add81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-citrix-gotomeeting-for-automatic-user-provisioning"></a>Zelfstudie: Citrix GoToMeeting configureren voor het automatisch gebruikers inrichten

Hallo-doel van deze zelfstudie is tooshow u stappen die u moet tooperform in Citrix GoToMeeting en Azure AD tooautomatically leveren en intrekken gebruikersaccounts vanuit Azure AD-tooCitrix GoToMeeting Hallo.

## <a name="prerequisites"></a>Vereisten

Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:

*   Een Azure Active directory-tenant.
*   Een Citrix GoToMeeting eenmalige aanmelding ingeschakeld abonnement.
*   Een gebruikersaccount in Citrix GoToMeeting met beheerdersmachtigingen Team.

## <a name="assigning-users-toocitrix-gotomeeting"></a>Gebruikers tooCitrix GoToMeeting toewijzen

Azure Active Directory gebruikt een concept 'toewijzingen' toodetermine welke gebruikers toegang tooselected apps krijgen genoemd. In de context van de Hallo van automatische gebruikers account inrichten, alleen Hallo-gebruikers en groepen die '' tooan toepassing in Azure AD toegewezen zijn gesynchroniseerd.

Voordat u configureren en inschakelen van Hallo-service inricht, moet u toodecide welke gebruikers en/of groepen in Azure AD Hallo-gebruikers die toegang moeten hebben tot tooyour Citrix GoToMeeting app vertegenwoordigen. Als besloten, kunt u deze gebruikers tooyour Citrix GoToMeeting app toewijzen door hier Hallo-instructies te volgen:

[Toewijzen van een gebruiker of groep tooan enterprise-app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toocitrix-gotomeeting"></a>Belangrijke tips voor het toewijzen van gebruikers tooCitrix GoToMeeting

*   Het is raadzaam om één tooCitrix GoToMeeting tootest Hallo configuratie inrichten door Azure AD-gebruiker is toegewezen. Extra gebruikers en/of groepen kunnen later worden toegewezen.

*   Wanneer u een gebruiker tooCitrix GoToMeeting toewijst, moet u een geldige gebruikersrol selecteren. Hallo 'Default toegang' rol werkt niet voor het inrichten.

## <a name="enable-automated-user-provisioning"></a>Geautomatiseerde Gebruikersinrichting inschakelen

Deze sectie helpt u bij het verbinden van uw Azure AD tooCitrix GoToMeeting gebruikersaccount inrichten API en Hallo service toocreate inrichting configureren, bijwerken en uitschakelen van de toegewezen gebruiker accounts in Citrix GoToMeeting op basis van gebruikers en groepen toewijzing in Azure AD.

> [!TIP]
> U kunt ook tooenabled op basis van SAML eenmalige aanmelding voor Citrix GoToMeeting, in het Hallo-instructies te volgen [Azure-portal](https://portal.azure.com). Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies aanvulling van elkaar.

### <a name="tooconfigure-automatic-user-account-provisioning"></a>tooconfigure automatische account gebruikersaanvragen:

1. In Hallo [Azure-portal](https://portal.azure.com), bladeren toohello **Azure Active Directory > zakelijke Apps > alle toepassingen** sectie.

2. Als u Citrix GoToMeeting al hebt geconfigureerd voor eenmalige aanmelding, zoekt u uw exemplaar van Citrix GoToMeeting met Hallo zoekveld opgegeven. Selecteer anders **toevoegen** en zoek naar **Citrix GoToMeeting** in Hallo-toepassingsgalerie. Citrix GoToMeeting selecteert in de zoekresultaten hello, en voeg deze tooyour lijst met toepassingen.

3. Selecteer uw exemplaar van Citrix GoToMeeting en vervolgens Hallo **inrichten** tabblad.

4. Set Hallo **inrichten** modus te**automatische**. 

    ![Inrichting](./media/active-directory-saas-citrixgotomeeting-provisioning-tutorial/provisioning.png)

5. Voer onder Hallo beheerdersreferenties sectie, Hallo stappen te volgen:
   
    a. In Hallo **Citrix GoToMeeting Beheerdersgebruikersnaam** textbox, typ de gebruikersnaam van een beheerder Hallo.

    b. In Hallo **Citrix GoToMeeting beheerderswachtwoord** textbox Hallo beheerderswachtwoord.

6. In hello Azure-portal, klikt u op **testverbinding** tooensure Azure AD verbinding tooyour Citrix GoToMeeting app kunt maken. Als Hallo verbinding mislukt, zorg ervoor dat uw account Citrix GoToMeeting Team beheerdersmachtigingen heeft en probeer het Hallo **'Beheerdersreferenties'** stap opnieuw.

7. Voer e-mailadres van een persoon of groep die inrichting fout meldingen in Hallo ontvangen moet Hallo **e-mailmelding** veld en Hallo selectievakje.

8. Klik op **opslaan.**

9. Selecteer onder Hallo toewijzingen sectie, **synchroniseren Azure Active Directory: gebruikers tooCitrix GoToMeeting.**

10. In Hallo **kenmerktoewijzingen** sectie, bekijkt hello gebruikerskenmerken die worden gesynchroniseerd vanuit Azure AD-tooCitrix GoToMeeting. kenmerken die zijn geselecteerd als Hallo **overeenkomend** eigenschappen zijn gebruikte toomatch Hallo gebruikersaccounts in Citrix GoToMeeting voor update-bewerkingen. Selecteer Hallo knop toocommit wijzigingen zijn opgeslagen.

11. tooenable Hallo inrichting Azure AD-service voor Citrix GoToMeeting, wijziging Hallo **inrichting Status** te**op** in Hallo Zoekinstellingen

12. Klik op **opslaan.**

Deze begint de initiële synchronisatie Hallo van alle gebruikers en/of groepen tooCitrix GoToMeeting in de sectie gebruikers en groepen Hallo toegewezen. de initiële synchronisatie Hallo duurt langer tooperform dan het volgende wordt gesynchroniseerd, die ongeveer 20 minuten optreden, zolang het Hallo-service wordt uitgevoerd. U kunt Hallo **synchronisatiedetails** sectie toomonitor uitgevoerd en volgt u koppelingen tooprovisioning activiteitsrapporten, waarin alle bewerkingen die worden uitgevoerd door het Hallo-service op uw app Citrix GoToMeeting inrichting beschrijven.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Het beheren van gebruikers account inrichten voor zakelijke Apps](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Eenmalige aanmelding configureren](active-directory-saas-citrix-gotomeeting-tutorial.md)


