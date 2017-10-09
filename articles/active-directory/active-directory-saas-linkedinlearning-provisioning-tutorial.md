---
title: 'Zelfstudie: LinkedIn Learning configureren voor het automatisch gebruikers inrichten met Azure Active Directory | Microsoft Docs'
description: Meer informatie over hoe tooconfigure Azure Active Directory tooautomatically leveren en intrekken gebruikersaccounts tooLinkedIn leren.
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
ms.date: 04/15/2017
ms.author: asmalser-msft
ms.openlocfilehash: e0503e09ab384723ffb73d6ef1df8be6abfc9294
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-linkedin-learning-for-automatic-user-provisioning"></a>Zelfstudie: LinkedIn Learning voor het automatisch gebruikers inrichten configureren


Hallo doel van deze zelfstudie is tooshow u stappen die u moet tooperform in LinkedIn Learning en Azure AD tooautomatically leveren en intrekken gebruikersaccounts vanuit Azure AD tooLinkedIn Hallo leren. 

## <a name="prerequisites"></a>Vereisten

Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:

*   Een Azure Active Directory-tenant
*   Een tenant LinkedIn Learning 
*   Een administrator-account in LinkedIn Learning met toegang toohello LinkedIn Account Center

> [!NOTE]
> Azure Active Directory is geïntegreerd met LinkedIn Learning met Hallo [SCIM](http://www.simplecloud.info/) protocol.

## <a name="assigning-users-toolinkedin-learning"></a>Toewijzen van gebruikers tooLinkedIn leren

Azure Active Directory gebruikt een concept 'toewijzingen' toodetermine welke gebruikers toegang tooselected apps krijgen genoemd. In de context van de Hallo van automatische gebruikers account inrichten, worden alleen Hallo-gebruikers en groepen die '' tooan toepassing in Azure AD toegewezen zijn gesynchroniseerd. 

Voordat u configureren en inschakelen van Hallo-service inricht, moet u toodecide welke gebruikers en/of groepen in Azure AD vertegenwoordigen Hallo-gebruikers die toegang moeten hebben tot tooLinkedIn leren. Als besloten, kunt u deze tooLinkedIn gebruikers toewijzen leren door hier Hallo-instructies te volgen:

[Toewijzen van een gebruiker of groep tooan enterprise-app](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toolinkedin-learning"></a>Belangrijke tips voor het toewijzen van gebruikers tooLinkedIn leren

*   Het is raadzaam om één Azure AD-gebruiker tooLinkedIn Learning tootest Hallo inrichting configuratie worden toegewezen. Extra gebruikers en/of groepen kunnen later worden toegewezen.

*   Bij het toewijzen van een gebruiker tooLinkedIn leren, moet u Hallo **gebruiker** rol in het dialoogvenster voor Hallo-toewijzing. Hallo 'Default toegang' rol werkt niet voor het inrichten.


## <a name="configuring-user-provisioning-toolinkedin-learning"></a>Configureren van gebruikers tooLinkedIn leren

Deze sectie helpt u bij het verbinding maken met uw Azure AD tooLinkedIn Learning SCIM-gebruikersaccount inrichten API en Hallo service toocreate inrichting configureren, bijwerken en uitschakelen van toegewezen gebruikersaccounts in LinkedIn Learning op basis van gebruikers en groepen toewijzing in Azure AD.

> [!TIP]
> U kunt ook tooenabled op basis van SAML eenmalige aanmelding voor LinkedIn Learning, in het Hallo-instructies te volgen [Azure-portal](https://portal.azure.com). Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies elkaar aanvullen.


### <a name="tooconfigure-automatic-user-account-provisioning-toolinkedin-learning-in-azure-ad"></a>Automatische gebruikersaccount tooconfigure tooLinkedIn inrichting Learning in Azure AD:


de eerste stap Hallo tooretrieve is uw toegangstoken LinkedIn. Als u een ondernemingsadministrator bent, kunt u zelf een toegangstoken inrichten. Ga te in uw accountcentrum**instellingen &gt; globale instellingen** en open Hallo **SCIM Setup** Configuratiescherm.

> [!NOTE]
> Als u Hallo-accountcentrum rechtstreeks in plaats van via een koppeling opent, kunt u met behulp van de volgende stappen uit Hallo bereiken.

1)  Meld u aan tooAccount Center.

2)  Selecteer **Admin &gt; beheerdersinstellingen** .

3)  Klik op **integraties geavanceerde** op Hallo links zijbalk. U bent gerichte toohello-accountcentrum.

4)  Klik op **+ toevoegen nieuwe SCIM configuratie** en volg de procedure Hallo door in elk veld te vullen.

> Wanneer autoassign licenties niet is ingeschakeld, betekent dit dat alleen de gegevens van de gebruiker is gesynchroniseerd.

![LinkedIn Learning inrichten](./media/active-directory-saas-linkedinlearning-provisioning-tutorial/linkedin_1.PNG)

> Wanneer autolicense toewijzing is ingeschakeld, moet u het toepassingsexemplaar toonote en licentietype. Licenties zijn toegewezen op een eerst komt, eerst basis fungeren totdat alle Hallo-licenties worden gehaald.

![LinkedIn Learning inrichten](./media/active-directory-saas-linkedinlearning-provisioning-tutorial/linkedin_2.PNG)

5)  Klik op **Generate token**. U ziet uw toegang tot token weergeven onder Hallo **toegangstoken** veld.

6)  Sla de toegang tot token tooyour Klembord of de computer voordat u Hallo pagina verlaat.

7) Meld je vervolgens in toohello [Azure-portal](https://portal.azure.com), en blader toohello **Azure Active Directory > zakelijke Apps > alle toepassingen** sectie.

8) Als u LinkedIn Learning al hebt geconfigureerd voor eenmalige aanmelding, zoekt u uw exemplaar van LinkedIn Learning met Hallo zoekveld opgegeven. Selecteer anders **toevoegen** en zoek naar **LinkedIn Learning** in Hallo-toepassingsgalerie. Selecteer LinkedIn Learning in zoekresultaten hello, en voeg deze tooyour lijst met toepassingen.

9)  Selecteer uw exemplaar van LinkedIn Learning en vervolgens Hallo **inrichten** tabblad.

10) Set Hallo **modus inrichting** te**automatische**.

![LinkedIn Learning inrichten](./media/active-directory-saas-linkedinlearning-provisioning-tutorial/linkedin_3.PNG)

11)  Hallo volgen onder velden invullen **beheerdersreferenties** :

* In Hallo **Tenant-URL** Voer https://api.linkedin.com.

* In Hallo **geheim Token** veld Hallo-toegangstoken die u in stap 1 hebt gegenereerd en op **testverbinding** .

* U ziet een melding geslaagd Hallo upperright zijde van de portal.

12) Voer e-mailadres van een persoon of groep die inrichting fout meldingen in Hallo ontvangen moet Hallo **e-mailmelding** veld en controleer de onderstaande Hallo selectievakje.

13) Klik op **Opslaan**. 

14) In Hallo **kenmerktoewijzingen** sectie, bekijkt hello gebruikers- en groepskenmerken die wordt gesynchroniseerd vanaf de Azure AD tooLinkedIn leren. Let op: kenmerken die zijn geselecteerd als Hallo **overeenkomend** eigenschappen worden gebruikte toomatch Hallo gebruikersaccounts en groepen in LinkedIn Learning voor update-bewerkingen. Selecteer Hallo knop toocommit wijzigingen zijn opgeslagen.

![LinkedIn Learning inrichten](./media/active-directory-saas-linkedinlearning-provisioning-tutorial/linkedin_4.PNG)

15) tooenable Hallo inrichting Azure AD-service voor LinkedIn Learning, wijziging Hallo **inrichting Status** te**op** in Hallo **instellingen** sectie

16) Klik op **Opslaan**. 

Hiermee start u de initiële synchronisatie Hallo van alle gebruikers en/of groepen toegewezen tooLinkedIn in de sectie gebruikers en groepen Hallo leren. Houd er rekening mee dat de initiële synchronisatie Hallo langer tooperform dan het volgende wordt gesynchroniseerd, die ongeveer 20 minuten optreden duurt, zolang het Hallo-service wordt uitgevoerd. U kunt Hallo **synchronisatiedetails** sectie toomonitor uitgevoerd en volgt u koppelingen tooprovisioning activiteitsrapporten, waarin alle bewerkingen die worden uitgevoerd door het Hallo-service op uw app LinkedIn Learning inrichting beschrijven.


## <a name="additional-resources"></a>Aanvullende resources

* [Het beheren van gebruikers account inrichten voor zakelijke Apps](active-directory-enterprise-apps-manage-provisioning.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)
