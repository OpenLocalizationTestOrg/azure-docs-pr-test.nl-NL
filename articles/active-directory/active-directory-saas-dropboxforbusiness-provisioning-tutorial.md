---
title: 'Zelfstudie: Azure Active Directory-integratie met Dropbox voor bedrijven | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Dropbox voor bedrijven.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f3a42e4-6897-4234-af84-b47c148ec3e1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 0fb01eab4f7c6c4516eac64a4343e46ea221f98d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-dropbox-for-business-for-automatic-user-provisioning"></a>Zelfstudie: Dropbox voor bedrijven configureren voor het automatisch gebruikers inrichten

Hallo-doel van deze zelfstudie is tooshow u stappen die u tooperform in Dropbox voor bedrijven en Azure AD tooautomatically leveren en intrekken gebruikersaccounts vanuit Azure AD-tooDropbox voor bedrijven moet Hallo.

## <a name="prerequisites"></a>Vereisten

Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:

*   Een Azure Active directory-tenant.
*   Een Dropbox voor bedrijven-eenmalige aanmelding ingeschakeld abonnement.
*   Een gebruikersaccount in Dropbox voor bedrijven met beheerdersmachtigingen Team.

## <a name="assigning-users-toodropbox-for-business"></a>Gebruikers tooDropbox toewijzen voor bedrijven

Azure Active Directory gebruikt een concept 'toewijzingen' toodetermine welke gebruikers toegang tooselected apps krijgen genoemd. In de context van de Hallo van automatische gebruikers account inrichten, alleen Hallo-gebruikers en groepen die '' tooan toepassing in Azure AD toegewezen zijn gesynchroniseerd.

Voordat u configureren en inschakelen van Hallo-service inricht, moet u toodecide welke gebruikers en/of groepen in Azure AD vertegenwoordigen Hallo-gebruikers die toegang moeten hebben tot tooyour Dropbox voor bedrijven-app. Als besloten, kunt u deze gebruikers tooyour Dropbox voor bedrijven-app kunt toewijzen door hier Hallo-instructies te volgen:

[Toewijzen van een gebruiker of groep tooan enterprise-app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toodropbox-for-business"></a>Belangrijke tips voor het toewijzen van gebruikers tooDropbox voor bedrijven

*   Het is raadzaam om één tooDropbox voor bedrijven tootest Hallo configuratie inrichten door Azure AD-gebruiker is toegewezen. Extra gebruikers en/of groepen kunnen later worden toegewezen.

*   Wanneer een gebruiker tooDropbox toewijzen voor bedrijven, moet u een geldige gebruikersrol selecteren. Hallo 'Default toegang' rol werkt niet voor het inrichten van...

## <a name="enable-automated-user-provisioning"></a>Geautomatiseerde Gebruikersinrichting inschakelen

Deze sectie helpt u bij het verbinden van uw Azure AD-tooDropbox voor bedrijven van gebruikersaccount inrichten API en Hallo service toocreate inrichting configureren, bijwerken en uitschakelen van toegewezen gebruikersaccounts in Dropbox voor bedrijven op basis van gebruikers en groepen toewijzing in Azure AD.

>[!Tip]
>U kunt ook tooenabled op basis van SAML eenmalige aanmelding voor Dropbox voor bedrijven, in het Hallo-instructies te volgen [Azure-portal](https://portal.azure.com). Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies aanvulling van elkaar.

### <a name="tooconfigure-automatic-user-account-provisioning"></a>tooconfigure automatische account gebruikersaanvragen:

1. In Hallo [Azure-portal](https://portal.azure.com), bladeren toohello **Azure Active Directory > zakelijke Apps > alle toepassingen** sectie.

2. Als u al Dropbox voor bedrijven hebt geconfigureerd voor eenmalige aanmelding, zoeken naar uw exemplaar van Dropbox voor bedrijven met Hallo zoekveld opgegeven. Selecteer anders **toevoegen** en zoek naar **Dropbox voor bedrijven** in Hallo-toepassingsgalerie. Selecteer Dropbox voor bedrijven in zoekresultaten hello, en voeg deze tooyour lijst met toepassingen.

3. Selecteer uw exemplaar van Dropbox voor bedrijven en vervolgens Hallo **inrichten** tabblad.

4. Set Hallo **modus inrichting** te**automatische**. 

    ![Inrichting](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/provisioning.png)

5. Onder Hallo **beheerdersreferenties** sectie, klikt u op **autoriseren**. Er wordt een Dropbox voor zakelijke aanmeldingsdialoogvenster geopend in een nieuw browservenster.

6. Op Hallo **aanmelden tooDropbox toolink met Azure AD** dialoogvenster Aanmelden tooyour Dropbox voor bedrijven-tenant.

     ![Gebruikers inrichten](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769518.png "gebruikers inrichten")

7. Bevestig dat u toogive Azure Active Directory machtiging toomake wijzigingen tooyour Dropbox voor bedrijven-tenant wilt. Klik op **toestaan**.
    
      ![Gebruikers inrichten](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769519.png "gebruikers inrichten")

8. Klik in hello Azure-portal, op **testverbinding** tooensure Azure AD verbinding kan maken van tooyour Dropbox voor bedrijven-app. Als Hallo verbinding mislukt, zorg ervoor dat uw Dropbox voor bedrijven-account Team beheerdersmachtigingen heeft en probeer het Hallo **'Autoriseren'** stap opnieuw.

9. Voer e-mailadres van een persoon of groep die inrichting fout meldingen in Hallo ontvangen moet Hallo **e-mailmelding** veld en Hallo selectievakje.

10. Klik op **opslaan.**

11. Selecteer onder Hallo toewijzingen sectie, **tooDropbox voor bedrijven synchroniseren Azure Active Directory-gebruikers.**

12. In Hallo **kenmerktoewijzingen** sectie, bekijkt hello gebruikerskenmerken die worden gesynchroniseerd vanuit Azure AD-tooDropbox voor bedrijven. kenmerken die zijn geselecteerd als Hallo **overeenkomend** eigenschappen zijn gebruikte toomatch Hallo gebruikersaccounts in Dropbox voor bedrijven voor update-bewerkingen. Selecteer Hallo knop toocommit wijzigingen zijn opgeslagen.

13. tooenable Hallo inrichting Azure AD-service voor Dropbox voor bedrijven, wijziging Hallo **inrichting Status** te**op** in Hallo Zoekinstellingen

14. Klik op **opslaan.**

Hallo initiële synchronisatie van gebruikers en/of groepen die zijn toegewezen tooDropbox voor bedrijven in Hallo gebruikers en groepen sectie begint. de initiële synchronisatie Hallo duurt langer tooperform dan het volgende wordt gesynchroniseerd, die ongeveer 20 minuten optreden, zolang het Hallo-service wordt uitgevoerd. U kunt Hallo **synchronisatiedetails** sectie toomonitor uitgevoerd en volgt u koppelingen tooprovisioning activiteitsrapporten, waarin alle acties die worden uitgevoerd door hello voor bedrijven-app op uw Dropbox-service inricht.

U kunt nu een testaccount maken. Wacht tot up too20 minuten tooverify die Hallo-account is gesynchroniseerd tooDropbox voor bedrijven.

Een is voltooid gebruikersaanvragen cyclus wordt aangegeven door de bijbehorende status.

![Gebruikers toewijzen](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/IC769523.png "gebruikers toewijzen")


## <a name="additional-resources"></a>Aanvullende bronnen

* [Het beheren van gebruikers account inrichten voor zakelijke Apps](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Eenmalige aanmelding configureren](active-directory-saas-dropboxforbusiness-tutorial.md)