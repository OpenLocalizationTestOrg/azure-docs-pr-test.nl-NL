---
title: 'Zelfstudie: Werkplek door Facebook configureren voor gebruikers inrichten | Microsoft Docs'
description: Meer informatie over hoe tooautomatically leveren en intrekken gebruikersaccounts vanuit Azure AD-tooWorkplace met Facebook.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6341e67e-8ce6-42dc-a4ea-7295904a53ef
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 33d294dbc8f441b29138408b3c9ca41f2141f8af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configure-workplace-by-facebook-for-user-provisioning"></a>Zelfstudie: Werkplek door Facebook configureren voor gebruikers inrichten

Deze zelfstudie ziet u stappen nodig tooautomatically leveren en intrekken gebruikersaccounts van Azure Active Directory (Azure AD) tooWorkplace door Facebook Hallo.

## <a name="prerequisites"></a>Vereisten

tooconfigure Azure AD-integratie met werkplek door Facebook, moet u de volgende Hallo:

- Een Azure AD-abonnement
- Een werkplek door Facebook eenmalige aanmelding (SSO) abonnement ingeschakeld

tootest hello stappen in deze zelfstudie volgt u deze aanbevelingen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een [één maand proefabonnement](https://azure.microsoft.com/pricing/free-trial/).

## <a name="assign-users-tooworkplace-by-facebook"></a>Toewijzen van gebruikers tooWorkplace door Facebook

Azure AD maakt gebruik van een concept 'toewijzingen' toodetermine welke gebruikers toegang tooselected apps krijgen genoemd. In de context van de Hallo van automatische gebruikers account inrichten, worden alleen Hallo-gebruikers en groepen die zijn toegewezen aan de tooan toepassing in Azure AD gesynchroniseerd.

Voordat u configureren en inschakelen van Hallo inrichting van de service, besluit welke gebruikers en groepen in Azure AD vertegenwoordigen Hallo-gebruikers die toegang moeten hebben tot tooyour werkplek door Facebook-app. Vervolgens kunt u deze gebruikers tooyour werkplek door Facebook-app door de volgende instructies in Hallo [toewijzen van een gebruiker of groep tooan enterprise app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal).

>[!IMPORTANT]
>*   Test Hallo configuratie inrichten door toe te wijzen één tooWorkplace voor Azure AD-gebruiker met Facebook. Later extra gebruikers en groepen toewijzen.
>*   Wanneer u een gebruiker tooWorkplace door Facebook toewijst, moet u een geldige gebruikersrol selecteren. Hallo standaard toegangsfunctie werkt niet voor het inrichten.

## <a name="enable-automated-user-provisioning"></a>Geautomatiseerde gebruikersinrichting inschakelen

In deze sectie helpt u bij het verbinden van uw Azure AD toohello gebruikersaccount inrichten API werkplek met Facebook. U leert ook hoe tooconfigure Hallo inrichting service toocreate bijwerken en uitschakelen van toegewezen gebruikersaccounts in werkplek met Facebook. Dit is gebaseerd op de gebruiker en groepstoewijzing in Azure AD.

>[!Tip]
>U kunt ook tooenabled SAML gebaseerde SSO voor werkplek door Facebook, door Hallo instructies vindt u in Hallo [Azure-portal](https://portal.azure.com). Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies elkaar aanvullen.

### <a name="configure-user-account-provisioning-tooworkplace-by-facebook-in-azure-ad"></a>Gebruikersaccount tooWorkplace door Facebook-inrichting in Azure AD configureren

Azure AD ondersteunt Hallo mogelijkheid tooautomatically synchroniseren accountdetails Hallo van toegewezen gebruikers tooWorkplace met Facebook. Deze automatische synchronisatie kunt werkplek door Facebook tooget Hallo gegevens tooauthorize gebruikers om toegang te krijgen, voordat moet ze toosign in voor Hallo eerst geprobeerd. Het ook inricht ongedaan gebruikers van werkplek door Facebook wanneer toegang in Azure AD is ingetrokken.

1. In Hallo [Azure-portal](https://portal.azure.com), selecteer **Azure Active Directory** > **zakelijke Apps** > **alle toepassingen**.

2. Als u werkplek door Facebook al hebt geconfigureerd voor eenmalige aanmelding, zoekt u uw exemplaar van de werkplek door Facebook met behulp van Hallo zoekveld opgegeven. Selecteer anders **toevoegen** en zoek naar **werkplek door Facebook** in Hallo-toepassingsgalerie. Selecteer **werkplek door Facebook** van Hallo zoekresultaten en toe te voegen tooyour lijst met toepassingen.

3. Selecteer uw exemplaar van de werkplek door Facebook, en selecteer vervolgens Hallo **inrichten** tabblad.

4. Stel **modus inrichting** te**automatische**. 

    ![Schermopname van werkplek door Facebook opties voor apparaatinrichting](./media/active-directory-saas-facebook-at-work-provisioning-tutorial/provisioning.png)

5. Onder Hallo **beheerdersreferenties** sectie, voert u Hallo **geheim Token** en Hallo **Tenant-URL** van uw werkplek door Facebook-beheerder.

6. Selecteer in de Azure-portal hello, **testverbinding** tooensure Azure AD verbinding tooyour werkplek door Facebook-app kunt maken. Als Hallo verbinding mislukt, zorg ervoor dat uw werkplek door Facebook-account Team beheerdersmachtigingen.

7. Voer e-mailadres van een persoon of groep die inrichting fout meldingen in Hallo ontvangen moet Hallo **e-mailmelding** veld en schakel het selectievakje Hallo.

8. Selecteer **Opslaan**.

9. Selecteer onder Hallo toewijzingen sectie, **synchroniseren Azure Active Directory: gebruikers tooWorkplace door Facebook**.

10. In Hallo **kenmerktoewijzingen** sectie, bekijkt hello gebruikerskenmerken die worden gesynchroniseerd vanuit Azure AD-tooWorkplace met Facebook. kenmerken die zijn geselecteerd als Hallo **overeenkomend** eigenschappen zijn gebruikte toomatch Hallo gebruikersaccounts op de werkplek door Facebook voor update-bewerkingen. wijzigen, selecteert u toocommit **opslaan**.

11. tooenable hello Azure AD provisioning-service voor werkplek door Facebook, in Hallo **instellingen** sectie, wijzigt u Hallo **inrichting Status** te**op**.

12. Selecteer **Opslaan**.

Voor meer informatie over het tooconfigure automatische inrichting, Zie [Hallo Facebook documentatie](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers).

U kunt nu een testaccount maken. Wacht tot up too20 minuten tooverify die Hallo-account is gesynchroniseerd tooWorkplace met Facebook.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Het beheren van gebruikers account inrichten voor zakelijke apps](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Eenmalige aanmelding configureren](active-directory-saas-facebook-at-work-tutorial.md)

