---
title: 'Zelfstudie: Samanage configureren voor het automatisch gebruikers inrichten met Azure Active Directory | Microsoft Docs'
description: Meer informatie over hoe tooconfigure Azure Active Directory tooautomatically leveren en intrekken gebruikersaccounts tooSamanage.
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
ms.openlocfilehash: 6cb36d2cc6ce33da4f8ebba65d138bfd4f2aca9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-samanage-for-automatic-user-provisioning"></a>Zelfstudie: Samanage configureren voor het automatisch gebruikers inrichten


Hallo-doel van deze zelfstudie is tooshow u stappen die u moet tooperform in Samanage en Azure AD tooautomatically leveren en intrekken gebruikersaccounts vanuit Azure AD tooSamanage Hallo. 

## <a name="prerequisites"></a>Vereisten

Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:

*   Een Azure Active directory-tenant
*   Een tenant Samanage Hello [Professional plan](https://www.samanage.com/pricing/) of beter ingeschakeld 
*   Een gebruikersaccount in Samanage met beheerdersmachtigingen 

> [!NOTE]
> Hello Azure AD integratie inrichting is afhankelijk van Hallo [Samanage REST-API](https://www.samanage.com/api/), namelijk beschikbaar tooSamanage teams op Hallo Professional plannen of voor een betere.

## <a name="assigning-users-toosamanage"></a>Gebruikers tooSamanage toewijzen

Azure Active Directory gebruikt een concept 'toewijzingen' toodetermine welke gebruikers toegang tooselected apps krijgen genoemd. In de context van de Hallo van automatische gebruikers account inrichten, alleen Hallo-gebruikers en groepen die '' tooan toepassing in Azure AD toegewezen zijn gesynchroniseerd. 

Voordat u configureren en inschakelen van Hallo-service inricht, moet u toodecide welke gebruikers en/of groepen in Azure AD vertegenwoordigen Hallo-gebruikers die toegang moeten hebben tot tooyour Samanage app. Als besloten, kunt u deze app-gebruikers tooyour Samanage toewijzen door hier Hallo-instructies te volgen:

[Toewijzen van een gebruiker of groep tooan enterprise-app](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toosamanage"></a>Belangrijke tips voor het toewijzen van gebruikers tooSamanage

*   Het is raadzaam om één tooSamanage tootest Hallo inrichting configuratie door Azure AD-gebruiker is toegewezen. Extra gebruikers en/of groepen kunnen later worden toegewezen.

*   Wanneer u een gebruiker tooSamanage toewijst, moet u beide Hallo **gebruiker** functie of een andere geldige toepassingsspecifieke-rol (indien beschikbaar) in het dialoogvenster voor Hallo-toewijzing. Hallo **standaardtoegang** rol werkt niet voor het inrichten en deze gebruikers worden overgeslagen.

> [!NOTE]
> Als een extra functie Hallo-service inricht eventuele aangepaste rollen gedefinieerd in Samanage leest en importeert ze in Azure AD waarin ze kunnen worden geselecteerd in het dialoogvenster voor Hallo rol selecteren. Deze rollen zijn zichtbaar in hello Azure-portal nadat Hallo-service inricht is ingeschakeld en een synchronisatiecyclus is voltooid.

## <a name="configuring-user-provisioning-toosamanage"></a>Gebruikers inrichten tooSamanage configureren 

Deze sectie helpt u bij het verbinden van uw Azure AD-tooSamanage gebruikersaccount inrichten API en Hallo service toocreate inrichting configureren, bijwerken en uitschakelen toegewezen gebruikersaccounts in Samanage op basis van gebruikers en groepen toewijzen in Azure AD.

> [!TIP]
> U kunt ook tooenabled op basis van SAML eenmalige aanmelding voor Samanage, in het Hallo-instructies te volgen [Azure-portal](https://portal.azure.com). Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies aanvulling van elkaar.


### <a name="configure-automatic-user-account-provisioning-toosamanage-in-azure-ad"></a>Automatische gebruikersaccount tooSamanage ingericht in Azure AD configureren:


1. In Hallo [Azure-portal](https://portal.azure.com), bladeren toohello **Azure Active Directory > zakelijke Apps > alle toepassingen** sectie.

2. Als u Samanage al hebt geconfigureerd voor eenmalige aanmelding, zoekt u uw exemplaar van Samanage met Hallo zoekveld opgegeven. Selecteer anders **toevoegen** en zoek naar **Samanage** in Hallo-toepassingsgalerie. Selecteer Samanage in zoekresultaten hello, en voeg deze tooyour lijst met toepassingen.

3. Selecteer uw exemplaar van Samanage en vervolgens Hallo **inrichten** tabblad.

4. Set Hallo **modus inrichting** te**automatische**.

    ![Samanage inrichten](./media/active-directory-saas-samanage-provisioning-tutorial/Samanage1.png)

5. Onder Hallo **beheerdersreferenties** sectie, invoer Hallo **Admin Username & beheerderswachtwoord** van uw Samanage-account. 

6. Klik in hello Azure-portal, op **testverbinding** tooensure Azure AD tooyour Samanage app kunt verbinden. Als Hallo verbinding mislukt, zorg ervoor dat uw account Samanage beheerdersmachtigingen heeft en probeer het opnieuw stap 5.

7. Voer e-mailadres van een persoon of groep die inrichting fout meldingen in Hallo ontvangen moet Hallo **e-mailmelding** veld en controleer Hallo selectievakje ' een e-mailmelding verzenden wanneer een fout optreedt."

8. Klik op **Opslaan**. 

9. Selecteer onder Hallo toewijzingen sectie, **synchroniseren Azure Active Directory: gebruikers tooSamanage**.

10. In Hallo **kenmerktoewijzingen** sectie, bekijkt hello gebruikerskenmerken die worden gesynchroniseerd vanuit Azure AD-tooSamanage. kenmerken die zijn geselecteerd als Hallo **overeenkomend** eigenschappen zijn gebruikte toomatch Hallo gebruikersaccounts in Samanage voor update-bewerkingen. Selecteer Hallo knop toocommit wijzigingen zijn opgeslagen.

11. tooenable Hallo inrichting Azure AD-service voor Samanage, wijziging Hallo **inrichting Status** te**op** in Hallo **instellingen** sectie

12. Klik op **Opslaan**. 

Deze bewerking begint Hallo initiële synchronisatie van gebruikers en/of groepen die zijn toegewezen tooSamanage in Hallo gebruikers en groepen sectie. de initiële synchronisatie Hallo duurt langer tooperform dan het volgende wordt gesynchroniseerd, die ongeveer 20 minuten optreden, zolang het Hallo-service wordt uitgevoerd. U kunt Hallo **synchronisatiedetails** sectie toomonitor uitgevoerd en volgt u koppelingen tooprovisioning activiteitsrapporten, waarin alle bewerkingen die worden uitgevoerd door het Hallo-service inricht.

Zie voor meer informatie over hoe tooread hello Azure AD-inrichting registreert, [rapportage over automatische account gebruikersaanvragen](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).


## <a name="additional-resources"></a>Aanvullende bronnen

* [Het beheren van gebruikers account inrichten voor zakelijke Apps](active-directory-enterprise-apps-manage-provisioning.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a>Volgende stappen

* [Informatie over hoe tooreview registreert en het ophalen van rapporten over het inrichten van activiteit](active-directory-saas-provisioning-reporting.md)
