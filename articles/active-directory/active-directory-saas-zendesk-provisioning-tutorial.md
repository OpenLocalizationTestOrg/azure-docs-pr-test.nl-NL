---
title: 'Zelfstudie: ZenDesk configureren voor het automatisch gebruikers inrichten met Azure Active Directory | Microsoft Docs'
description: Meer informatie over hoe tooconfigure Azure Active Directory tooautomatically leveren en intrekken gebruikersaccounts tooZenDesk.
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
ms.openlocfilehash: 200e8790ec1755f5cf927274ceb38527dd993f3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-zendesk-for-automatic-user-provisioning"></a>Zelfstudie: ZenDesk configureren voor het automatisch gebruikers inrichten


Hallo-doel van deze zelfstudie is tooshow u stappen die u moet tooperform in de ZenDesk- en Azure AD tooautomatically leveren en intrekken gebruikersaccounts vanuit Azure AD tooZenDesk Hallo. 

## <a name="prerequisites"></a>Vereisten

Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:

*   Een Azure Active directory-tenant
*   Een tenant ZenDesk Hello [enterpriseplan](https://www.zendesk.com/product/pricing/) of beter ingeschakeld 
*   Een gebruikersaccount in de ZenDesk met beheerdersmachtigingen 

> [!NOTE]
> Hello Azure AD integratie inrichting is afhankelijk van Hallo [ZenDesk REST-API](https://developer.zendesk.com/rest_api/docs/core/introduction#the-api), die beschikbaar tooZenDesk teams op Hallo essentiële plan of hoger is.

## <a name="assigning-users-toozendesk"></a>Gebruikers tooZenDesk toewijzen

Azure Active Directory gebruikt een concept 'toewijzingen' toodetermine welke gebruikers toegang tooselected apps krijgen genoemd. In de context van de Hallo van automatische gebruikers account inrichten, worden alleen Hallo-gebruikers en groepen die '' tooan toepassing in Azure AD toegewezen zijn gesynchroniseerd. 

Voordat u configureren en inschakelen van Hallo-service inricht, moet u toodecide welke gebruikers en/of groepen in Azure AD vertegenwoordigen Hallo-gebruikers die toegang moeten hebben tot tooyour ZenDesk-app. Als besloten, kunt u deze gebruikers tooyour ZenDesk-app kunt toewijzen door hier Hallo-instructies te volgen:

[Toewijzen van een gebruiker of groep tooan enterprise-app](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toozendesk"></a>Belangrijke tips voor het toewijzen van gebruikers tooZenDesk

*   Het is raadzaam om één tooZenDesk tootest Hallo inrichting configuratie door Azure AD-gebruiker is toegewezen. Extra gebruikers en/of groepen kunnen later worden toegewezen.

*   Wanneer u een gebruiker tooZenDesk toewijst, moet u beide Hallo **gebruiker** functie of een andere geldige toepassingsspecifieke-rol (indien beschikbaar) in het dialoogvenster voor Hallo-toewijzing. Hallo **standaardtoegang** rol werkt niet voor het inrichten en deze gebruikers worden overgeslagen.

> [!NOTE]
> Als een extra functie Hallo-service inricht eventuele aangepaste rollen gedefinieerd in de Zendesk leest en importeert ze in Azure AD waarin ze kunnen worden geselecteerd in het dialoogvenster voor Hallo rol selecteren. Deze rollen zijn zichtbaar in hello Azure-portal nadat Hallo-service inricht is ingeschakeld en een synchronisatiecyclus is voltooid.

## <a name="configuring-user-provisioning-toozendesk"></a>Gebruikers inrichten tooZenDesk configureren 

In deze sectie helpt u bij het verbinden van uw Azure AD-tooZenDesk gebruikersaccount inrichten API en Hallo service toocreate inrichting configureren, bijwerken en uitschakelen van toegewezen gebruikersaccounts in de ZenDesk op basis van gebruikers en groepen toewijzen in Azure AD.

> [!TIP] 
> U kunt ook tooenabled op basis van SAML eenmalige aanmelding voor ZenDesk, in het Hallo-instructies te volgen [Azure-portal](https://portal.azure.com). Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies aanvulling van elkaar.


### <a name="configure-automatic-user-account-provisioning-toozendesk-in-azure-ad"></a>Automatische gebruikersaccount tooZenDesk ingericht in Azure AD configureren


1. In Hallo [Azure-portal](https://portal.azure.com), bladeren toohello **Azure Active Directory > zakelijke Apps > alle toepassingen** sectie.

2. Als u ZenDesk al hebt geconfigureerd voor eenmalige aanmelding, zoekt u uw exemplaar van ZenDesk met Hallo zoekveld opgegeven. Selecteer anders **toevoegen** en zoek naar **ZenDesk** in Hallo-toepassingsgalerie. Selecteer ZenDesk in zoekresultaten hello, en voeg deze tooyour lijst met toepassingen.

3. Selecteer uw ZenDesk-exemplaar en vervolgens Hallo **inrichten** tabblad.

4. Set Hallo **modus inrichting** te**automatische**.

    ![ZenDesk-inrichting](./media/active-directory-saas-zendesk-provisioning-tutorial/ZenDesk1.png)

5. Onder Hallo **beheerdersreferenties** sectie, invoer Hallo **Admin Username & tokenkey & domein** die worden gegenereerd door uw ZenDesk-account (Hallo token vindt u onder uw account: **Admin**   >  **API** > **instellingen**). 

    ![ZenDesk-inrichting](./media/active-directory-saas-zendesk-provisioning-tutorial/ZenDesk2.png)

6. Klik in hello Azure-portal, op **testverbinding** tooensure Azure AD tooyour ZenDesk-app kunt verbinden. Als Hallo verbinding mislukt, zorg ervoor dat uw ZenDesk-account beheerdersmachtigingen heeft en probeer het opnieuw stap 5.

7. Voer e-mailadres van een persoon of groep die inrichting fout meldingen in Hallo ontvangen moet Hallo **e-mailmelding** veld en controleer Hallo selectievakje ' een e-mailmelding verzenden wanneer een fout optreedt."

8. Klik op **Opslaan**. 

9. Selecteer onder Hallo toewijzingen sectie, **synchroniseren Azure Active Directory: gebruikers tooZenDesk**.

10. In Hallo **kenmerktoewijzingen** sectie, bekijkt hello gebruikerskenmerken die worden gesynchroniseerd vanuit Azure AD-tooZenDesk. kenmerken die zijn geselecteerd als Hallo **overeenkomend** eigenschappen zijn gebruikte toomatch Hallo gebruikersaccounts in de ZenDesk voor update-bewerkingen. Selecteer Hallo knop toocommit wijzigingen zijn opgeslagen.

11. tooenable Hallo inrichting Azure AD-service voor ZenDesk, wijziging Hallo **inrichting Status** te**op** in Hallo **instellingen** sectie

12. Klik op **Opslaan**. 

Deze bewerking begint Hallo initiële synchronisatie van gebruikers en/of groepen die zijn toegewezen tooZenDesk in Hallo gebruikers en groepen sectie. de initiële synchronisatie Hallo duurt langer tooperform dan het volgende wordt gesynchroniseerd, die ongeveer 20 minuten optreden, zolang het Hallo-service wordt uitgevoerd. U kunt Hallo **synchronisatiedetails** sectie toomonitor uitgevoerd en volgt u koppelingen tooprovisioning activiteitsrapporten, waarin alle bewerkingen die worden uitgevoerd door het Hallo-service inricht.

Zie voor meer informatie over hoe tooread hello Azure AD-inrichting registreert, [rapportage over automatische account gebruikersaanvragen](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).


## <a name="additional-resources"></a>Aanvullende bronnen

* [Het beheren van gebruikers account inrichten voor zakelijke Apps](active-directory-enterprise-apps-manage-provisioning.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a>Volgende stappen

* [Informatie over hoe tooreview registreert en het ophalen van rapporten over het inrichten van activiteit](active-directory-saas-provisioning-reporting.md)
