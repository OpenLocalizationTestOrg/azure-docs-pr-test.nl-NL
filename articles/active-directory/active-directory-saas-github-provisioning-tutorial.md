---
title: 'Zelfstudie: GitHub configureren voor het automatisch gebruikers inrichten met Azure Active Directory | Microsoft Docs'
description: Meer informatie over hoe tooconfigure Azure Active Directory tooautomatically leveren en intrekken gebruikersaccounts tooGitHub.
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
ms.openlocfilehash: c1f0f7a42e4f8a94db3f409cd463e13bb1bc13bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-github-for-automatic-user-provisioning"></a>Zelfstudie: GitHub configureren voor het automatisch gebruikers inrichten


Hallo-doel van deze zelfstudie is tooshow u stappen die u moet tooperform in GitHub en Azure AD tooautomatically leveren en intrekken gebruikersaccounts vanuit Azure AD tooGitHub Hallo. 

## <a name="prerequisites"></a>Vereisten

Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:

*   Een Azure Active directory-tenant
*   Een tenant Github Hello [bedrijfsplan](https://help.github.com/articles/organization-billing-plans/#business-plan) of beter ingeschakeld 
*   Een gebruikersaccount in GitHub met beheerdersmachtigingen 

> [!NOTE]
> Hello Azure AD integratie inrichting is afhankelijk van Hallo [GitHub SCIM API](https://developer.github.com/v3/scim/), die beschikbaar tooGithub teams op Hallo bedrijfsplan of hoger is.

## <a name="assigning-users-toogithub"></a>Gebruikers tooGitHub toewijzen

Azure Active Directory gebruikt een concept 'toewijzingen' toodetermine welke gebruikers toegang tooselected apps krijgen genoemd. In de context van de Hallo van automatische gebruikers account inrichten, alleen Hallo-gebruikers en groepen die '' tooan toepassing in Azure AD toegewezen zijn gesynchroniseerd. 

Voordat u configureren en inschakelen van Hallo-service inricht, moet u toodecide welke gebruikers en/of groepen in Azure AD vertegenwoordigen Hallo-gebruikers die toegang moeten hebben tot tooyour GitHub-app. Als besloten, kunt u deze app-gebruikers tooyour GitHub toewijzen door hier Hallo-instructies te volgen:

[Toewijzen van een gebruiker of groep tooan enterprise-app](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toogithub"></a>Belangrijke tips voor het toewijzen van gebruikers tooGitHub

*   Het is raadzaam om één tooGitHub tootest Hallo inrichting configuratie door Azure AD-gebruiker is toegewezen. Extra gebruikers en/of groepen kunnen later worden toegewezen.

*   Wanneer u een gebruiker tooGitHub toewijst, moet u beide Hallo **gebruiker** functie of een andere geldige toepassingsspecifieke-rol (indien beschikbaar) in het dialoogvenster voor Hallo-toewijzing. Hallo **standaardtoegang** rol werkt niet voor het inrichten en deze gebruikers worden overgeslagen.


## <a name="configuring-user-provisioning-toogithub"></a>Gebruikers inrichten tooGitHub configureren 

In deze sectie helpt u bij het verbinden van uw Azure AD-tooGitHub gebruikersaccount inrichten API en Hallo service toocreate inrichting configureren, bijwerken en uitschakelen van toegewezen gebruikersaccounts in GitHub op basis van gebruikers en groepen toewijzen in Azure AD.

> [!TIP]
> U kunt ook tooenabled op basis van SAML eenmalige aanmelding voor GitHub, in het Hallo-instructies te volgen [Azure-portal](https://portal.azure.com). Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies aanvulling van elkaar.


### <a name="configure-automatic-user-account-provisioning-toogithub-in-azure-ad"></a>Automatische gebruikersaccount tooGitHub ingericht in Azure AD configureren


1. In Hallo [Azure-portal](https://portal.azure.com), bladeren toohello **Azure Active Directory > zakelijke Apps > alle toepassingen** sectie.

2. Als u al GitHub hebt geconfigureerd voor eenmalige aanmelding, zoeken naar uw exemplaar van GitHub met Hallo zoekveld opgegeven. Selecteer anders **toevoegen** en zoek naar **GitHub** in Hallo-toepassingsgalerie. Selecteer GitHub in zoekresultaten hello, en voeg deze tooyour lijst met toepassingen.

3. Selecteer uw exemplaar van GitHub en vervolgens Hallo **inrichten** tabblad.

4. Set Hallo **modus inrichting** te**automatische**.

    ![Het inrichten van GitHub](./media/active-directory-saas-github-provisioning-tutorial/GitHub1.png)

5. Onder Hallo **beheerdersreferenties** sectie, klikt u op **autoriseren**. Deze bewerking wordt een dialoogvenster met GitHub autorisatie in een nieuw browservenster geopend. 

6. In nieuw venster hello, je aanmelden bij uw beheerdersaccount met GitHub. Selecteer in de resulterende autorisatie dialoogvenster Hallo Hallo GitHub team dat u wilt tooenable voor inrichting en selecteer vervolgens **autoriseren**. Voltooid door terug te gaan toohello Azure portal toocomplete hello configuratie inrichten.

    ![Dialoogvenster autorisatie](./media/active-directory-saas-github-provisioning-tutorial/GitHub2.png)

7. Invoer in hello Azure-portal, **Tenant-URL** en klik op **testverbinding** tooensure Azure AD tooyour GitHub-app kunt verbinden. Als Hallo verbinding mislukt, zorg ervoor dat uw GitHub-account beheerdersmachtigingen heeft en **Tenant-URl** is opgegeven correct en probeer het vervolgens opnieuw 'Autoriseren' stap Hallo (u kunt vormen **Tenant-URL** door regel: 'https : //api.github.com/scim/v2/organizations/ + < Organizations_name > ', kunt u uw organisaties vinden onder uw GitHub-account: **instellingen** > **organisaties**).

    ![Dialoogvenster autorisatie](./media/active-directory-saas-github-provisioning-tutorial/GitHub3.png)

8. Voer e-mailadres van een persoon of groep die inrichting fout meldingen in Hallo ontvangen moet Hallo **e-mailmelding** veld en controleer Hallo selectievakje ' een e-mailmelding verzenden wanneer een fout optreedt."

9. Klik op **Opslaan**. 

10. Selecteer onder Hallo toewijzingen sectie, **synchroniseren Azure Active Directory: gebruikers tooGitHub**.

11. In Hallo **kenmerktoewijzingen** sectie, bekijkt hello gebruikerskenmerken die worden gesynchroniseerd vanuit Azure AD-tooGitHub. kenmerken die zijn geselecteerd als Hallo **overeenkomend** eigenschappen zijn gebruikte toomatch Hallo gebruikersaccounts in GitHub voor update-bewerkingen. Selecteer Hallo knop toocommit wijzigingen zijn opgeslagen.

12. tooenable Hallo inrichting Azure AD-service voor GitHub, wijziging Hallo **inrichting Status** te**op** in Hallo **instellingen** sectie

13. Klik op **Opslaan**. 

Deze bewerking begint Hallo initiële synchronisatie van gebruikers en/of groepen die zijn toegewezen tooGitHub in Hallo gebruikers en groepen sectie. de initiële synchronisatie Hallo duurt langer tooperform dan het volgende wordt gesynchroniseerd, die ongeveer 20 minuten optreden, zolang het Hallo-service wordt uitgevoerd. U kunt Hallo **synchronisatiedetails** sectie toomonitor uitgevoerd en volgt u koppelingen tooprovisioning activiteitsrapporten, waarin alle bewerkingen die worden uitgevoerd door het Hallo-service inricht.

Zie voor meer informatie over hoe tooread hello Azure AD-inrichting registreert, [rapportage over automatische account gebruikersaanvragen](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).


## <a name="additional-resources"></a>Aanvullende bronnen

* [Het beheren van gebruikers account inrichten voor zakelijke Apps](active-directory-enterprise-apps-manage-provisioning.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a>Volgende stappen

* [Informatie over hoe tooreview registreert en het ophalen van rapporten over het inrichten van activiteit](active-directory-saas-provisioning-reporting.md)
