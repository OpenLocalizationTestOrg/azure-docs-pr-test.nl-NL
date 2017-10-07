---
title: 'Zelfstudie: Cerner centraal configureren voor het automatisch gebruikers inrichten met Azure Active Directory | Microsoft Docs'
description: Meer informatie over hoe Azure Active Directory-tooautomatically tooconfigure gebruikers tooa schema in Cerner centrale inrichten.
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
ms.date: 05/26/2017
ms.author: asmalser-msft
ms.openlocfilehash: e96da98e783d24e7f34ae924824f909eead75f54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-cerner-central-for-automatic-user-provisioning"></a>Zelfstudie: Cerner centraal configureren voor het automatisch gebruikers inrichten

Hallo-doel van deze zelfstudie is tooshow u stappen die u moet tooperform in Cerner centraal en Azure AD tooautomatically leveren en intrekken gebruikersaccounts vanuit Azure AD tooa gebruiker schema in Cerner centrale Hallo. 


## <a name="prerequisites"></a>Vereisten

Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:

*   Een Azure Active Directory-tenant
*   Een tenant Cerner-centraal 

> [!NOTE]
> Azure Active Directory is geïntegreerd met Cerner centraal Hallo met [SCIM](http://www.simplecloud.info/) protocol.

## <a name="assigning-users-toocerner-central"></a>Toewijzen van gebruikers tooCerner centraal

Azure Active Directory gebruikt een concept 'toewijzingen' toodetermine welke gebruikers toegang tooselected apps krijgen genoemd. In de context van de Hallo van automatische gebruikers account inrichten, worden alleen Hallo-gebruikers en groepen die '' tooan toepassing in Azure AD toegewezen zijn gesynchroniseerd. 

Voordat u configureren en inschakelen van Hallo-service inricht, moet u bepalen welke gebruikers en/of groepen in Azure AD Hallo-gebruikers die toegang moeten hebben tot tooCerner centraal vertegenwoordigen. Als besloten, kunt u deze gebruikers tooCerner centraal kunt toewijzen door hier Hallo-instructies te volgen:

[Toewijzen van een gebruiker of groep tooan enterprise-app](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toocerner-central"></a>Belangrijke tips voor het toewijzen van gebruikers tooCerner centraal

*   Het is raadzaam om één Azure AD-gebruiker tooCerner centrale tootest Hallo inrichting configuratie worden toegewezen. Extra gebruikers en/of groepen kunnen later worden toegewezen.

* Zodra de eerste testen is voltooid voor één gebruiker, raadt Cerner centraal Hallo volledige lijst met gebruikers die zijn bedoeld tooaccess gebruikerslijst alle Cerner oplossing (niet alleen Cerner centraal) toobe ingericht tooCerner toewijzen.  Andere oplossingen Cerner gebruikmaken van deze lijst van gebruikers in de gebruikerslijst Hallo.

*   Wanneer u een gebruiker tooCerner centraal toewijst, moet u Hallo **gebruiker** rol in het dialoogvenster voor Hallo-toewijzing. Gebruikers met Hallo 'Default toegang' rol worden uitgesloten van de inrichting.


## <a name="configuring-user-provisioning-toocerner-central"></a>Gebruikers inrichten tooCerner centraal configureren

In deze sectie helpt u bij het verbinden van uw Azure AD tooCerner centraal gebruiker schema van Cerner SCIM gebruikersaccount gebruikt API-inrichting en Hallo service toocreate inrichting configureren, bijwerken en toegewezen gebruiker op basis van accounts in Cerner centrale uitschakelen op de toewijzing van gebruikers en groepen in Azure AD.

> [!TIP]
> U kunt ook tooenabled op basis van SAML eenmalige aanmelding voor Cerner centraal, Hallo-instructies die zijn opgegeven in [Azure-portal (https://portal.azure.com). Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies elkaar aanvullen. Zie voor meer informatie, Hallo [één centrale Cerner aanmelding zelfstudie](active-directory-saas-cernercentral-tutorial.md).


### <a name="tooconfigure-automatic-user-account-provisioning-toocerner-central-in-azure-ad"></a>tooconfigure automatische gebruikersaccount tooCerner centraal ingericht in Azure AD:


In de volgorde tooprovision gebruiker accounts tooCerner centraal, u moet een Cerner centraal system-account van Cerner toorequest, en genereren van een OAuth-bearer-token die Azure AD van tooconnect tooCerner SCIM eindpunt kunt gebruiken. Het wordt ook aanbevolen Hallo integratie worden uitgevoerd in een Cerner sandbox-omgeving voordat u tooproduction implementeert.

1.  Hallo eerste stap is tooensure Hallo mensen Hallo Cerner beheren en Azure AD-integratie hebben een CernerCare-account is vereist tooaccess Hallo documentatie nodig toocomplete Hallo instructies. Gebruik indien nodig Hallo-URL's onder toocreate CernerCare accounts in elke omgeving van toepassing.

   * Sandbox: https://sandboxcernercare.com/accounts/create

   * Productie: https://cernercare.com/accounts/create  

2.  Vervolgens moet een systeem-account worden gemaakt voor Azure AD. Hallo instructies hieronder toorequest een systeemaccount gebruiken voor uw sandbox en productie-omgevingen.

   * Instructies: https://wiki.ucern.com/display/CernerCentral/Requesting+A+System+Account

   * Sandbox: https://sandboxcernercentral.com/system-accounts/

   * Productie: https://cernercentral.com/system-accounts/

3.  Vervolgens een OAuth bearer-token genereren voor elk van uw systeemaccounts. toodo deze, Hallo instructies hieronder.

   * Instructies: https://wiki.ucern.com/display/public/reference/Accessing+Cerner%27s+Web+Services+Using+A+System+Account+Bearer+Token

   * Sandbox: https://sandboxcernercentral.com/system-accounts/

   * Productie: https://cernercentral.com/system-accounts/

4. Tot slot moet u tooacquire gebruikers schema Realm-id's voor beide Hallo sandbox en productie-omgevingen in Cerner toocomplete Hallo configuratie. Voor meer informatie over tooacquire deze, Zie: https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+SCIM. 

5. Nu kunt u Azure AD tooprovision gebruiker accounts tooCerner configureren. Meld u aan toohello [Azure-portal](https://portal.azure.com), en blader toohello **Azure Active Directory > zakelijke Apps > alle toepassingen** sectie.

6. Als u Cerner centraal al hebt geconfigureerd voor eenmalige aanmelding, zoekt u uw exemplaar van Cerner centraal met Hallo zoekveld opgegeven. Selecteer anders **toevoegen** en zoek naar **Cerner centraal** in Hallo-toepassingsgalerie. Selecteer Cerner centraal in zoekresultaten hello, en voeg deze tooyour lijst met toepassingen.

7.  Selecteer uw exemplaar van de centrale Cerner en vervolgens Hallo **inrichten** tabblad.

8.  Set Hallo **modus inrichting** te**automatische**.

   ![Cerner centraal inrichten](./media/active-directory-saas-cernercentral-provisioning-tutorial/Cerner.PNG)

9.  Hallo volgen onder velden invullen **beheerdersreferenties**:

   * In Hallo **Tenant-URL** veld, voer een URL in de indeling Hallo hieronder, "Gebruiker-schema-Realm-ID" vervangen door een Hallo realm ID die u hebt verkregen in stap &#4;.

> Sandbox: https://user-roster-api.sandboxcernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/ 

> Productie: https://user-roster-api.cernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/ 

   * In Hallo **geheim Token** veld Hallo OAuth bearer-token die u in stap &#3; gegenereerd en op **testverbinding**.

   * U ziet een melding geslaagd Hallo upperright zijde van de portal.

10. Voer e-mailadres van een persoon of groep die inrichting fout meldingen in Hallo ontvangen moet Hallo **e-mailmelding** veld en controleer de onderstaande Hallo selectievakje.

11. Klik op **Opslaan**. 

12. In Hallo **kenmerktoewijzingen** sectie, bekijkt hello gebruiker en groep kenmerken toobe gesynchroniseerd met Azure AD tooCerner centraal. kenmerken die zijn geselecteerd als Hallo **overeenkomend** eigenschappen zijn gebruikte toomatch Hallo gebruikersaccounts en groepen in de centrale Cerner voor update-bewerkingen. Selecteer Hallo knop toocommit wijzigingen zijn opgeslagen.

13. tooenable Hallo inrichting Azure AD-service voor het hoofdkantoor Cerner, wijziging Hallo **inrichting Status** te**op** in Hallo **instellingen** sectie

14. Klik op **Opslaan**. 

Hiermee start u de initiële synchronisatie Hallo van alle gebruikers en/of groepen tooCerner centraal in de sectie gebruikers en groepen Hallo toegewezen. de initiële synchronisatie Hallo duurt langer tooperform dan het volgende wordt gesynchroniseerd, die ongeveer 20 minuten optreden, zolang Hallo inrichting Azure AD-service wordt uitgevoerd. U kunt Hallo **synchronisatiedetails** sectie toomonitor uitgevoerd en volgt u koppelingen tooprovisioning activiteitsrapporten, waarin alle bewerkingen die worden uitgevoerd door het Hallo-service op uw app Cerner centraal inrichting beschrijven.

Zie voor meer informatie over hoe tooread hello Azure AD-inrichting registreert, [rapportage over automatische account gebruikersaanvragen](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).

## <a name="additional-resources"></a>Aanvullende bronnen

* [Cerner centraal: Publiceren van identiteitsgegevens met behulp van Azure AD](https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+Azure+AD)
* [Zelfstudie: Cerner centraal configureren voor eenmalige aanmelding bij Azure Active Directory](active-directory-saas-cernercentral-tutorial.md)
* [Het beheren van gebruikers account inrichten voor zakelijke Apps](active-directory-enterprise-apps-manage-provisioning.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a>Volgende stappen
* [Meer informatie over hoe tooreview registreert en get rapporten over het inrichten van de activiteit](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).
