---
title: 'Zelfstudie: Azure Active Directory-integratie met Concur | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Concur.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: df47f55f-a894-4e01-a82e-0dbf55fc8af1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 13ba364af26a5ce0f1d2b51aaa0f84a4c353b107
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-concur-for-user-provisioning"></a>Zelfstudie: Configureren voor gebruikers inrichten instemming

Hallo-doel van deze zelfstudie is tooshow u stappen die u moet tooperform in Concur en Azure AD tooautomatically leveren en intrekken gebruikersaccounts vanuit Azure AD tooConcur Hallo.

## <a name="prerequisites"></a>Vereisten

Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:

*   Een Azure Active directory-tenant.
*   Een Concur eenmalige aanmelding ingeschakeld abonnement.
*   Een gebruikersaccount in Concur met beheerdersmachtigingen Team.

## <a name="assigning-users-tooconcur"></a>Gebruikers tooConcur toewijzen

Azure Active Directory gebruikt een concept 'toewijzingen' toodetermine welke gebruikers toegang tooselected apps krijgen genoemd. In de context van de Hallo van automatische gebruikers account inrichten, alleen Hallo-gebruikers en groepen die '' tooan toepassing in Azure AD toegewezen zijn gesynchroniseerd.

Voordat u configureren en inschakelen van Hallo-service inricht, moet u toodecide welke gebruikers en/of groepen in Azure AD vertegenwoordigen Hallo-gebruikers die toegang moeten hebben tot tooyour Concur app. Als besloten, kunt u deze app-gebruikers tooyour Concur toewijzen door hier Hallo-instructies te volgen:

[Toewijzen van een gebruiker of groep tooan enterprise-app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-tooconcur"></a>Belangrijke tips voor het toewijzen van gebruikers tooConcur

*   Het is raadzaam om één Azure AD-gebruiker tooConcur tootest Hallo inrichting configuratie worden toegewezen. Extra gebruikers en/of groepen kunnen later worden toegewezen.

*   Wanneer u een gebruiker tooConcur toewijst, moet u een geldige gebruikersrol. Hallo 'Default toegang' rol werkt niet voor het inrichten.

## <a name="enable-user-provisioning"></a>Gebruikersinrichting inschakelen

Deze sectie helpt u bij het verbinden van uw Azure AD-tooConcur gebruikersaccount inrichten API en Hallo service toocreate inrichting configureren, bijwerken en uitschakelen toegewezen gebruikersaccounts in Concur op basis van gebruikers en groepen toewijzen in Azure AD.

> [!Tip] 
> U kunt ook tooenabled op basis van SAML eenmalige aanmelding voor Concur, in het Hallo-instructies te volgen [Azure-portal](https://portal.azure.com). Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies aanvulling van elkaar.

### <a name="tooconfigure-user-account-provisioning"></a>tooconfigure account gebruikersaanvragen:

Hallo-doel van deze sectie is het toooutline hoe tooConcur tooenable het inrichten van Active Directory-gebruiker accounts.

tooenable toepassingen in de Service onkosten Hallo, er is de juiste instelling toobe en het gebruik van een profiel voor een Web-servicebeheerder. Voeg niet Hallo WS Admin rol tooyour bestaande beheerdersprofiel dat u voor T & en beheerfuncties gebruikt.

Instemming adviseurs of Hallo client beheerder moet een afzonderlijke Service webbeheerder-profiel maken en Hallo Client administrator moet dit profiel gebruiken voor Hallo Web Services-beheerder functies (bijvoorbeeld inschakelen apps). Deze profielen moeten gescheiden worden gehouden van Hallo client dagelijkse d & E admin beheerdersprofiel (Hallo T & E admin profiel mag geen Hallo WSAdmin rol toegewezen).

Wanneer u Hallo profiel toobe gebruikt voor het inschakelen van Hallo-app maakt, aangaan Hallo client beheerder Hallo gebruiker profiel velden. Hiermee wijst eigendom toohello profiel toe. Zodra een of meer profielen is gemaakt, Hallo-client moet aanmelden met dit profiel tooclick Hallo '*inschakelen*' knop voor een App-Partner in het Hallo-webservices menu.

Voor Hallo redenen te volgen, moet deze actie niet met Hallo profiel die ze voor normale T & en beheer gebruiken worden uitgevoerd.

* Hallo client heeft toobe Hallo die klikt op '*Ja*' hello dialoog venster dat wordt weergegeven nadat een app is ingeschakeld. Klikt u op bevestigt Hallo-client is bereid voor Hallo Partner toepassing tooaccess hun gegevens, zodat u of Hallo Partner kan niet klikt u op dat Ja knop.

* Als de beheerder van een client die een app met Hallo T & E admin profiel heeft ingeschakeld achterlaat Hallo bedrijf (waardoor Hallo-profiel wordt uitgeschakeld), alle apps ingeschakeld met behulp van dit profiel werkt niet totdat het Hallo-app met een andere actieve WS-beheer is ingeschakeld profiel. Dit is de reden waarom u gewoonlijk toocreate distinct WS Admin profielen.

* Als een beheerder Hallo bedrijf verlaat, gekoppelde Hallo naam toohello WS-beheerder kan profiel gewijzigde toohello vervanging beheerder zijn indien gewenst zonder enige impact op Hallo ingeschakeld app omdat dit profiel niet hoeft deactiveren.

**tooconfigure gebruikers inrichten, Voer Hallo stappen te volgen:**

1. Meld u aan tooyour **Concur** tenant.

2. Van Hallo **beheer** selecteert u **webservices**.
   
    ![Concur tenant](./media/active-directory-saas-concur-provisioning-tutorial/IC721729.png "Concur tenant")

3. Op de linkerkant van Hallo Hallo **webservices** deelvenster **partnertoepassing inschakelen**.
   
    ![Partnertoepassing inschakelen](./media/active-directory-saas-concur-provisioning-tutorial/ic721730.png "partnertoepassing inschakelen")

4. Van Hallo **toepassing inschakelen** selecteert **Azure Active Directory**, en klik vervolgens op **inschakelen**.
   
    ![Microsoft Azure Active Directory](./media/active-directory-saas-concur-provisioning-tutorial/ic721731.png "Microsoft Azure Active Directory")

5. Klik op **Ja** tooclose hello **bevestigen actie** dialoogvenster.
   
    ![Bevestig de actie](./media/active-directory-saas-concur-provisioning-tutorial/ic721732.png "Bevestig de actie")

6. In Hallo [Azure-portal](https://portal.azure.com), bladeren toohello **Azure Active Directory > zakelijke Apps > alle toepassingen** sectie.

7. Als u Concur al hebt geconfigureerd voor eenmalige aanmelding, zoekt u uw exemplaar van Concur met Hallo zoekveld opgegeven. Selecteer anders **toevoegen** en zoek naar **Concur** in Hallo-toepassingsgalerie. Selecteer Concur in zoekresultaten hello, en voeg deze tooyour lijst met toepassingen.

8. Selecteer uw exemplaar van Concur en vervolgens Hallo **inrichten** tabblad.

9. Set Hallo **modus inrichting** te**automatische**. 
 
    ![Inrichting](./media/active-directory-saas-concur-provisioning-tutorial/provisioning.png)

10. Onder Hallo **beheerdersreferenties** sectie, voert u Hallo **gebruikersnaam** en Hallo **wachtwoord** van uw beheerder Concur.

11. Klik in hello Azure-portal, op **testverbinding** tooensure Azure AD tooyour Concur app kunt verbinden. Als Hallo verbinding mislukt, Controleer of uw account Concur Team beheerder machtigingen.

12. Voer e-mailadres van een persoon of groep die inrichting fout meldingen in Hallo ontvangen moet Hallo **e-mailmelding** veld en Hallo selectievakje.

13. Klik op **opslaan.**

14. Selecteer onder Hallo toewijzingen sectie, **tooConcur synchroniseren Azure Active Directory-gebruikers.**

15. In Hallo **kenmerktoewijzingen** sectie, bekijkt hello gebruikerskenmerken die worden gesynchroniseerd vanuit Azure AD-tooConcur. kenmerken die zijn geselecteerd als Hallo **overeenkomend** eigenschappen zijn gebruikte toomatch Hallo gebruikersaccounts in Concur voor update-bewerkingen. Selecteer Hallo knop toocommit wijzigingen zijn opgeslagen.

16. tooenable Hallo inrichting Azure AD-service voor Concur, wijziging Hallo **inrichting Status** te**op** in Hallo **instellingen** sectie

17. Klik op **opslaan.**

U kunt nu een testaccount maken. Wacht tot up too20 minuten tooverify die Hallo-account is gesynchroniseerd tooConcur.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Het beheren van gebruikers account inrichten voor zakelijke Apps](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Eenmalige aanmelding configureren](active-directory-saas-concur-tutorial.md)

