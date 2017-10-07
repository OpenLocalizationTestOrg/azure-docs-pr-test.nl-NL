---
title: 'Zelfstudie: Slack configureren voor het automatisch gebruikers inrichten met Azure Active Directory | Microsoft Docs'
description: Meer informatie over hoe tooconfigure Azure Active Directory tooautomatically leveren en intrekken gebruikersaccounts tooSlack.
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: sakula
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: asmalser-msft
ms.reviewer: asmalser
ms.openlocfilehash: d0a565bbe0bd7e229b9dd99b1ebbaf67d93a2206
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-slack-for-automatic-user-provisioning"></a>Zelfstudie: Slack configureren voor het automatisch gebruikers inrichten


Hallo doel van deze zelfstudie is tooshow Hallo van stappen die u moet tooperform in Slack en Azure AD tooautomatically leveren en intrekken gebruikersaccounts vanuit Azure AD-tooSlack. 

## <a name="prerequisites"></a>Vereisten

Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:

*   Een Azure Active Active directory-tenant
*   Een Slack-tenant met Hallo [Plus plan](https://aadsyncfabric.slack.com/pricing) of beter ingeschakeld 
*   Een gebruikersaccount in Slack met beheerdersmachtigingen Team 

Opmerking: hello Azure AD integratie inrichting is afhankelijk van Hallo [Slack SCIM API](https://api.slack.com/scim) die teams op Hallo Plus-abonnement of een betere tooSlack beschikbaar is.

## <a name="assigning-users-tooslack"></a>Gebruikers tooSlack toewijzen

Azure Active Directory gebruikt een concept 'toewijzingen' toodetermine welke gebruikers toegang tooselected apps krijgen genoemd. In de context van de Hallo van automatische gebruikers account inrichten, worden alleen Hallo-gebruikers en groepen die '' tooan toepassing in Azure AD toegewezen zijn gesynchroniseerd. 

Voordat u configureren en inschakelen van Hallo-service inricht, moet u toodecide welke gebruikers en/of groepen in Azure AD vertegenwoordigen Hallo-gebruikers die toegang moeten hebben tot tooyour toegestane app. Als besloten, kunt u deze gebruikers tooyour toegestane app toewijzen door hier Hallo-instructies te volgen:

[Toewijzen van een gebruiker of groep tooan enterprise-app](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-tooslack"></a>Belangrijke tips voor het toewijzen van gebruikers tooSlack

*   Het is raadzaam om één Azure AD-gebruiker tooSlack tootest Hallo inrichting configuratie worden toegewezen. Extra gebruikers en/of groepen kunnen later worden toegewezen.

*   Wanneer u een gebruiker tooSlack toewijst, moet u Hallo **gebruiker** of 'Groep'-rol in het dialoogvenster voor Hallo-toewijzing. Hallo 'Default toegang' rol werkt niet voor het inrichten.


## <a name="configuring-user-provisioning-tooslack"></a>Gebruikers inrichten tooSlack configureren 

Deze sectie helpt u bij het verbinden van uw Azure AD-tooSlack gebruikersaccount inrichten API en Hallo service toocreate inrichting configureren, bijwerken en uitschakelen van toegewezen gebruikersaccounts in Slack op basis van gebruikers en groepen toewijzen in Azure AD.

**Tip:** u kunt ook tooenabled op basis van SAML eenmalige aanmelding voor de vertraging Hallo instructies vindt u in (Azure-portal) [https://portal.azure.com]. Eenmalige aanmelding kan worden geconfigureerd onafhankelijk van automatische inrichting, hoewel deze twee functies aanvulling van elkaar.


### <a name="tooconfigure-automatic-user-account-provisioning-tooslack-in-azure-ad"></a>tooconfigure automatische gebruikersaccount tooSlack ingericht in Azure AD:


1)  In Hallo [Azure-portal](https://portal.azure.com), bladeren toohello **Azure Active Directory > zakelijke Apps > alle toepassingen** sectie.

2) Als u toegestane vertraging voor eenmalige aanmelding al hebt geconfigureerd, kunt u zoeken naar uw exemplaar van Hallo zoekveld met Slack. Selecteer anders **toevoegen** en zoek naar **Slack** in Hallo-toepassingsgalerie. Selecteer Slack in zoekresultaten hello, en voeg deze tooyour lijst met toepassingen.

3)  Selecteer uw exemplaar van Slack en vervolgens Hallo **inrichten** tabblad.

4)  Set Hallo **modus inrichting** te**automatische**.

![Vertraging inrichten](./media/active-directory-saas-slack-provisioning-tutorial/Slack1.PNG)

5)  Onder Hallo **beheerdersreferenties** sectie, klikt u op **autoriseren**. Hiermee opent u een dialoogvenster toegestane autorisatie in een nieuw browservenster. 

6) In nieuw venster hello, meld u aan in Slack met uw Team Admin-account. in het resulterende autorisatie dialoogvenster Hallo Hallo Selecteer toegestane team dat u wilt tooenable voor inrichting en selecteer vervolgens **autoriseren**. Voltooid door terug te gaan toohello Azure portal toocomplete hello configuratie inrichten.

![Dialoogvenster autorisatie](./media/active-directory-saas-slack-provisioning-tutorial/Slack3.PNG)

7) Klik in hello Azure-portal, op **testverbinding** tooensure Azure AD tooyour toegestane app kunt verbinden. Als Hallo verbinding mislukt, zorg ervoor dat uw toegestane account Team beheerdersmachtigingen heeft en probeer het Hallo 'Autoriseren' stap opnieuw.

8) Voer e-mailadres van een persoon of groep die inrichting fout meldingen in Hallo ontvangen moet Hallo **e-mailmelding** veld en controleer de onderstaande Hallo selectievakje.

9) Klik op **Opslaan**. 

10) Selecteer onder Hallo toewijzingen sectie, **synchroniseren Azure Active Directory: gebruikers tooSlack**.

11) In Hallo **kenmerktoewijzingen** sectie, bekijkt hello gebruikerskenmerken die worden gesynchroniseerd vanuit Azure AD-tooSlack. Let op: kenmerken die zijn geselecteerd als Hallo **overeenkomend** eigenschappen worden gebruikte toomatch Hallo gebruikersaccounts in Slack voor update-bewerkingen. Selecteer Hallo knop toocommit wijzigingen zijn opgeslagen.

12) tooenable Hallo inrichting Azure AD-service voor vertraging wijziging Hallo **inrichting Status** te**op** in Hallo **instellingen** sectie

13) Klik op **Opslaan**. 

Hiermee start u de initiële synchronisatie Hallo van gebruikers en/of groepen die zijn toegewezen tooSlack in Hallo gebruikers en groepen sectie. Houd er rekening mee dat de initiële synchronisatie Hallo langer tooperform dan het volgende wordt gesynchroniseerd, die ongeveer elke 10 minuten optreden duurt, zolang het Hallo-service wordt uitgevoerd. U kunt Hallo **synchronisatiedetails** sectie toomonitor uitgevoerd en volgt u koppelingen tooprovisioning activiteitsrapporten, waarin alle bewerkingen die worden uitgevoerd door het Hallo-service op uw toegestane app inrichten.

## <a name="optional-configuring-group-object-provisioning-tooslack"></a>[Optioneel] Groepsobject tooSlack inrichting configureren 

Desgewenst kunt u Hallo inrichting van groepsobjecten van Azure AD-tooSlack inschakelen. Dit verschilt van het 'groepen gebruikers toe te wijzen', in Hallo werkelijke groepsobject bovendien tooits leden van Azure AD-tooSlack worden gerepliceerd. Als u een groep met de naam 'Mijn groep' in Azure AD hebt, wordt bijvoorbeeld een identitical groep met de naam 'Mijn groep' gemaakt binnen de toegestane vertraging.

### <a name="tooenable-provisioning-of-group-objects"></a>tooenable inrichting van groepsobjecten:

1) Selecteer onder Hallo toewijzingen sectie, **synchroniseren Azure Active Directory-groepen tooSlack**.

2) Hallo kenmerk toewijzing blade ingesteld tooYes ingeschakeld.

3) In Hallo **kenmerktoewijzingen** sectie, bekijkt hello Groepkenmerken die wordt gesynchroniseerd vanaf de Azure AD-tooSlack. Let op: kenmerken die zijn geselecteerd als Hallo **overeenkomend** eigenschappen worden gebruikte toomatch Hallo groepen in Slack voor update-bewerkingen. 

4) Klik op **Opslaan**.

Deze leiden tot een groep objecten die zijn toegewezen tooSlack in Hallo **gebruikers en groepen** sectie volledig wordt gesynchroniseerd vanuit Azure AD-tooSlack. U kunt Hallo **synchronisatiedetails** sectie toomonitor uitgevoerd en volgt u koppelingen tooprovisioning activiteitsrapporten, waarin alle bewerkingen die worden uitgevoerd door het Hallo-service op uw toegestane app inrichten.


## <a name="additional-resources"></a>Aanvullende resources

* [Het beheren van gebruikers account inrichten voor zakelijke Apps](active-directory-enterprise-apps-manage-provisioning.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)
