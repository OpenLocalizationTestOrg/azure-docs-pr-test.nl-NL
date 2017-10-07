---
title: 'Zelfstudie: Azure Active Directory-integratie met werkplek door Facebook | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en werkplek met Facebook.
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
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 551ec353a5ec1da936373587688c299a6f4acca7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-workplace-by-facebook-for-user-provisioning"></a>Zelfstudie: Werkplek door Facebook configureren voor gebruikers inrichten

Hallo-doel van deze zelfstudie is tooshow Hallo van stappen die u moet tooperform op werkplek door Facebook en Azure AD tooautomatically leveren en intrekken gebruikersaccounts vanuit Azure AD-tooWorkplace met Facebook.

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met werkplek door Facebook tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een werkplek door Facebook-eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="assigning-users-tooworkplace-by-facebook"></a>Toewijzen van gebruikers tooWorkplace door Facebook

Azure Active Directory gebruikt een concept 'toewijzingen' toodetermine welke gebruikers toegang tooselected apps krijgen genoemd. In de context van de Hallo van automatische gebruikers account inrichten, alleen Hallo-gebruikers en groepen die '' tooan toepassing in Azure AD toegewezen zijn gesynchroniseerd.

Voordat u configureren en inschakelen van Hallo-service inricht, moet u toodecide welke gebruikers en/of groepen in Azure AD vertegenwoordigen Hallo-gebruikers die toegang moeten hebben tot tooyour werkplek door Facebook-app. Als besloten, kunt u deze gebruikers tooyour werkplek door Facebook-app kunt toewijzen door hier Hallo-instructies te volgen:

[Toewijzen van een gebruiker of groep tooan enterprise-app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-tooworkplace-by-facebook"></a>Belangrijke tips voor het toewijzen van gebruikers tooWorkplace door Facebook

*   Het is raadzaam om één Azure AD-gebruiker tooWorkplace door Facebook tootest Hallo configuratie inrichting is toegewezen. Extra gebruikers en/of groepen kunnen later worden toegewezen.

*   U moet een geldige gebruikersrol selecteren bij het toewijzen van een gebruiker tooWorkplace met Facebook. Hallo 'Default toegang' rol werkt niet voor het inrichten.

## <a name="enable-user-provisioning"></a>Gebruikersinrichting inschakelen

Deze sectie helpt u bij het verbinden van uw Azure AD-tooWorkplace door Facebook van gebruikersaccount inrichten API en Hallo service toocreate inrichting configureren, bijwerken en uitschakelen van toegewezen gebruikersaccounts in werkplek door Facebook op basis van gebruikers en groepen toewijzing in Azure AD.

>[!Tip]
>U kunt ook tooenabled op basis van SAML eenmalige aanmelding voor werkplek door Facebook, in het Hallo-instructies te volgen [Azure-portal](https://portal.azure.com). Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies aanvulling van elkaar.

### <a name="tooconfigure-user-account-provisioning-tooworkplace-by-facebook-in-azure-ad"></a>tooconfigure gebruikersaccount tooWorkplace door Facebook-inrichting in Azure AD:

Hallo-doel van deze sectie is het toooutline hoe tooenable inrichting van Active Directory-gebruiker tooWorkplace door Facebook-accounts.

Azure AD ondersteunt Hallo mogelijkheid tooautomatically synchroniseren accountdetails Hallo van toegewezen gebruikers tooWorkplace met Facebook. Deze automatische synchronisatie kunt werkplek door Facebook tooget Hallo gegevens tooauthorize gebruikers om toegang te krijgen, voordat moet ze toosign in voor Hallo eerst geprobeerd. Het ook inricht ongedaan gebruikers van werkplek door Facebook wanneer toegang in Azure AD is ingetrokken.

1. In Hallo [Azure-portal](https://portal.azure.com), bladeren toohello **Azure Active Directory** > **zakelijke Apps** > **alle toepassingen** sectie.

2. Als u werkplek door Facebook al hebt geconfigureerd voor eenmalige aanmelding, zoekt u uw exemplaar van de werkplek door Hallo zoekveld met Facebook. Selecteer anders **toevoegen** en zoek naar **werkplek door Facebook** in Hallo-toepassingsgalerie. Selecteer werkplek door Facebook in zoekresultaten hello, en voeg deze tooyour lijst met toepassingen.

3. Selecteer uw exemplaar van de werkplek door Facebook en vervolgens Hallo **inrichten** tabblad.

4. Set Hallo **modus inrichting** te**automatische**. 

    ![Inrichting](./media/active-directory-saas-workplacebyfacebook-provisioning-tutorial/provisioning.png)

5. Onder Hallo **beheerdersreferenties** sectie, voert u Hallo geheim Token en Hallo Tenant-URL van uw werkplek door Facebook-beheerder.

6. Klik in hello Azure-portal, op **testverbinding** tooensure Azure AD verbinding kan maken van tooyour werkplek door Facebook-app. Als Hallo verbinding mislukt, zorg ervoor dat uw werkplek door Facebook-account Team beheerdersmachtigingen heeft.

7. Voer e-mailadres van een persoon of groep die inrichting fout meldingen in Hallo ontvangen moet Hallo **e-mailmelding** veld en Hallo selectievakje.

8. Klik op **opslaan.**

9. Selecteer onder Hallo toewijzingen sectie, **tooWorkplace synchroniseren Azure Active Directory-gebruikers met Facebook.**

10. In Hallo **kenmerktoewijzingen** sectie, bekijkt hello gebruikerskenmerken die worden gesynchroniseerd vanuit Azure AD-tooWorkplace met Facebook. kenmerken die zijn geselecteerd als Hallo **overeenkomend** eigenschappen zijn gebruikte toomatch Hallo gebruikersaccounts op de werkplek door Facebook voor update-bewerkingen. Selecteer Hallo knop toocommit wijzigingen zijn opgeslagen.

11. tooenable Hallo inrichting Azure AD-service voor werkplek door Facebook, wijziging Hallo **inrichting Status** te**op** in Hallo **instellingen** sectie

12. Klik op **opslaan.**

Voor meer informatie over het tooconfigure automatische inrichting, Zie [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)

U kunt nu een testaccount maken. Wacht tot up too20 minuten tooverify die Hallo-account is gesynchroniseerd tooWorkplace met Facebook.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Het beheren van gebruikers account inrichten voor zakelijke Apps](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Eenmalige aanmelding configureren](active-directory-saas-workplacebyfacebook-tutorial.md)

