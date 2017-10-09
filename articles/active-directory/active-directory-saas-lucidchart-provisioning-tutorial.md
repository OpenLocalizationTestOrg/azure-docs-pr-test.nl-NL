---
title: 'Zelfstudie: LucidChart configureren voor het automatisch gebruikers inrichten met Azure Active Directory | Microsoft Docs'
description: Meer informatie over hoe tooconfigure Azure Active Directory tooautomatically leveren en intrekken gebruikersaccounts tooLucidChart.
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: stevenpo
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: asmalser-msft
ms.openlocfilehash: d3af45141731215f2edc8942ad21b016468c1e38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-lucidchart-for-automatic-user-provisioning"></a>Zelfstudie: LucidChart configureren voor het automatisch gebruikers inrichten


Hallo-doel van deze zelfstudie is tooshow u stappen die u moet tooperform in LucidChart en Azure AD tooautomatically leveren en intrekken gebruikersaccounts vanuit Azure AD tooLucidChart Hallo. 

## <a name="prerequisites"></a>Vereisten

Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:

*   Een Azure Active directory-tenant
*   Een tenant LucidChart Hello [enterpriseplan](https://www.lucidchart.com/user/117598685#/subscriptionLevel) of beter ingeschakeld 
*   Een gebruikersaccount in LucidChart met beheerdersmachtigingen 

## <a name="assigning-users-toolucidchart"></a>Gebruikers tooLucidChart toewijzen

Azure Active Directory gebruikt een concept 'toewijzingen' toodetermine welke gebruikers toegang tooselected apps krijgen genoemd. In de context van de Hallo van automatische gebruikers account inrichten, alleen Hallo-gebruikers en groepen die '' tooan toepassing in Azure AD toegewezen zijn gesynchroniseerd. 

Voordat u configureren en inschakelen van Hallo-service inricht, moet u toodecide welke gebruikers en/of groepen in Azure AD vertegenwoordigen Hallo-gebruikers die toegang moeten hebben tot tooyour LucidChart app. Als besloten, kunt u deze app-gebruikers tooyour LucidChart toewijzen door hier Hallo-instructies te volgen:

[Toewijzen van een gebruiker of groep tooan enterprise-app](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toolucidchart"></a>Belangrijke tips voor het toewijzen van gebruikers tooLucidChart

*   Het is raadzaam om één tooLucidChart tootest Hallo inrichting configuratie door Azure AD-gebruiker is toegewezen. Extra gebruikers en/of groepen kunnen later worden toegewezen.

*   Wanneer u een gebruiker tooLucidChart toewijst, moet u beide Hallo **gebruiker** functie of een andere geldige toepassingsspecifieke-rol (indien beschikbaar) in het dialoogvenster voor Hallo-toewijzing. Hallo **standaardtoegang** rol werkt niet voor het inrichten en deze gebruikers worden overgeslagen.


## <a name="configuring-user-provisioning-toolucidchart"></a>Gebruikers inrichten tooLucidChart configureren 

Deze sectie helpt u bij het verbinden van uw Azure AD-tooLucidChart gebruikersaccount inrichten API en Hallo service toocreate inrichting configureren, bijwerken en uitschakelen van toegewezen gebruikersaccounts in LucidChart op basis van gebruikers en groepen toewijzen in Azure AD .

> [!TIP]
> U kunt ook tooenabled op basis van SAML eenmalige aanmelding voor LucidChart, in het Hallo-instructies te volgen [Azure-portal](https://portal.azure.com). Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies aanvulling van elkaar.


### <a name="configure-automatic-user-account-provisioning-toolucidchart-in-azure-ad"></a>Automatische gebruikersaccount tooLucidChart ingericht in Azure AD configureren


1. In Hallo [Azure-portal](https://portal.azure.com), bladeren toohello **Azure Active Directory > zakelijke Apps > alle toepassingen** sectie.

2. Als u LucidChart al hebt geconfigureerd voor eenmalige aanmelding, zoekt u uw exemplaar van LucidChart met Hallo zoekveld opgegeven. Selecteer anders **toevoegen** en zoek naar **LucidChart** in Hallo-toepassingsgalerie. Selecteer LucidChart in zoekresultaten hello, en voeg deze tooyour lijst met toepassingen.

3. Selecteer uw exemplaar van LucidChart en vervolgens Hallo **inrichten** tabblad.

4. Set Hallo **modus inrichting** te**automatische**.

    ![LucidChart inrichten](./media/active-directory-saas-lucidchart-provisioning-tutorial/LucidChart1.png)

5. Onder Hallo **beheerdersreferenties** sectie, invoer Hallo **geheim Token** die worden gegenereerd door uw LucidChart account (Hallo token vindt u onder uw account: **Team**  >  **App-integratie** > **SCIM**). 

    ![LucidChart inrichten](./media/active-directory-saas-lucidchart-provisioning-tutorial/LucidChart2.png)

6. Klik in hello Azure-portal, op **testverbinding** tooensure Azure AD tooyour LucidChart app kunt verbinden. Als Hallo verbinding mislukt, zorg ervoor dat uw account LucidChart beheerdersmachtigingen heeft en probeer het opnieuw stap 5.

7. Voer e-mailadres van een persoon of groep die inrichting fout meldingen in Hallo ontvangen moet Hallo **e-mailmelding** veld en controleer Hallo selectievakje ' een e-mailmelding verzenden wanneer een fout optreedt."

8. Klik op **Opslaan**. 

9. Selecteer onder Hallo toewijzingen sectie, **synchroniseren Azure Active Directory: gebruikers tooLucidChart**.

10. In Hallo **kenmerktoewijzingen** sectie, bekijkt hello gebruikerskenmerken die worden gesynchroniseerd vanuit Azure AD-tooLucidChart. kenmerken die zijn geselecteerd als Hallo **overeenkomend** eigenschappen zijn gebruikte toomatch Hallo gebruikersaccounts in LucidChart voor update-bewerkingen. Selecteer Hallo knop toocommit wijzigingen zijn opgeslagen.

11. tooenable Hallo inrichting Azure AD-service voor LucidChart, wijziging Hallo **inrichting Status** te**op** in Hallo **instellingen** sectie

12. Klik op **Opslaan**. 

Deze bewerking begint Hallo initiële synchronisatie van gebruikers en/of groepen die zijn toegewezen tooLucidChart in Hallo gebruikers en groepen sectie. de initiële synchronisatie Hallo duurt langer tooperform dan het volgende wordt gesynchroniseerd, die ongeveer 20 minuten optreden, zolang het Hallo-service wordt uitgevoerd. U kunt Hallo **synchronisatiedetails** sectie toomonitor uitgevoerd en volgt u koppelingen tooprovisioning activiteitsrapporten, waarin alle bewerkingen die worden uitgevoerd door het Hallo-service inricht.

Zie voor meer informatie over hoe tooread hello Azure AD-inrichting registreert, [rapportage over automatische account gebruikersaanvragen](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).


## <a name="additional-resources"></a>Aanvullende bronnen

* [Het beheren van gebruikers account inrichten voor zakelijke Apps](active-directory-enterprise-apps-manage-provisioning.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a>Volgende stappen

* [Informatie over hoe tooreview registreert en het ophalen van rapporten over het inrichten van activiteit](active-directory-saas-provisioning-reporting.md)
