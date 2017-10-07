---
title: inrichting van beheer voor zakelijke apps in Azure Active Directory Hallo aaaUser | Microsoft Docs
description: Meer informatie over hoe toomanage gebruikersaccount inrichten voor zakelijke apps met hello Azure Active Directory
services: active-directory
documentationcenter: 
author: asmalser
manager: femila
editor: 
ms.assetid: 34ac4028-a5aa-40d9-a93b-0db4e0abd793
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/26/2017
ms.author: asmalser
ms.reviewer: asmalser
ms.openlocfilehash: a613f844c8f51e04b92e62b488313a78ab85f7ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-user-account-provisioning-for-enterprise-apps-in-hello-azure-portal"></a>Het beheer van gebruikersaccount inrichten voor zakelijke apps in hello Azure-portal
Dit artikel wordt beschreven hoe toouse hello [Azure-portal](https://portal.azure.com) toomanage automatische gebruikersaccount inrichting en ongedaan wordt ingericht voor toepassingen die ondersteuning bieden voor deze, met name lijsten die zijn toegevoegd vanuit Hallo 'aanbevolen' categorie Hallo [Azure Active Directory-toepassingsgalerie](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery). toolearn meer informatie over automatische account gebruikersaanvragen en hoe het werkt, Zie [gebruikersaanvragen automatiseren en Deprovisioning tooSaaS toepassingen met Azure Active Directory](active-directory-saas-app-provisioning.md).

## <a name="finding-your-apps-in-hello-portal"></a>Uw apps zoeken in Hallo portal
Alle toepassingen die zijn geconfigureerd voor eenmalige aanmelding in een map door de beheerder van een directory met Hallo [Azure Active Directory-toepassingsgalerie](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery), kan worden bekeken en beheerd in Hallo [Azure-portal](https://portal.azure.com). Hallo toepassingen vindt u in Hallo **meer Services** &gt; **bedrijfstoepassingen** sectie van het Hallo-portal. Zakelijke apps zijn apps die zijn geïmplementeerd en worden gebruikt binnen uw organisatie.

![Blade bedrijfstoepassingen][0]

Selecteren Hallo **alle toepassingen** koppeling aan de linkerkant Hallo bevat een overzicht van alle apps die zijn geconfigureerd, met inbegrip van apps die waren toegevoegd uit Hallo-galerie. Als u een app wordt geladen Hallo resource-blade voor die app, waarbij de rapporten kunnen worden weergegeven voor die app en een aantal instellingen kan worden beheerd.

Instellingen voor het inrichten gebruikersaccount kan worden beheerd door te selecteren **inrichten** op Hallo links.

![De resource-blade toepassing][1]

## <a name="provisioning-modes"></a>Inrichting modi
Hallo **inrichten** blade begint met een **modus** menu ziet u welke inrichting modi worden ondersteund voor een zakelijke toepassing en kan ze toobe geconfigureerd. Hallo beschikbare opties zijn onder andere:

* **Automatische** -deze optie wordt weergegeven als Azure AD ondersteunt automatische inrichting op basis van een API en/of de inrichting van Gebruikerstoepassing accounts toothis. Als u deze modus wordt weergegeven een interface waarmee beheerders via Azure AD tooconnect toohello van de toepassing Gebruikersbeheer API configureren, Accounttoewijzingen en werkstromen die definiëren hoe de gegevens van gebruikersaccounts moeten stromen tussen Azure AD maken en Hallo-app en het beheer van hello Azure AD-inrichting service.
* **Handmatige** -deze optie wordt weergegeven als Azure AD biedt geen ondersteuning voor automatische inrichting van de toepassing van de gebruiker accounts toothis. Deze optie betekent dat account gebruikersrecords opgeslagen in de toepassing hello moeten worden beheerd met behulp van een extern proces, op basis van Hallo gebruiker beheer en inrichting mogelijkheden van die toepassing (met inbegrip van SAML-compileerprogramma inrichting).

## <a name="configuring-automatic-user-account-provisioning"></a>Configuratie van automatische gebruikers account inrichten
Selecteren Hallo **automatische** optie wordt weergegeven, een scherm weergegeven dat is onderverdeeld in vier secties:

### <a name="admin-credentials"></a>Beheerdersreferenties
Dit is waar Hallo-referenties die nodig zijn voor Azure AD tooconnect toohello van de toepassing gebruiker management API worden ingevoerd. Hallo invoer vereist clientdownload is afhankelijk van het Hallo-toepassing. toolearn over de vereisten voor specifieke toepassingen en Hallo referentietypen Zie Hallo [zelfstudie voor de configuratie voor de specifieke toepassing](active-directory-saas-app-provisioning.md#list-of-apps-that-support-automated-user-provisioning).

Selecteren Hallo **testverbinding** knop kunt u tootest Hallo referenties door Azure AD tooconnect toohello app probeert de app met behulp van referenties opgegeven Hallo inrichten.

### <a name="mappings"></a>Toewijzingen
Dit is waar beheerders kunnen weergeven en bewerken welke kenmerken gebruikersstroom tussen Azure AD en Hallo-doeltoepassing, wanneer gebruikersaccounts worden ingericht of bijgewerkt.

Er is een vooraf geconfigureerde verzameling toewijzingen tussen Azure AD-gebruikersobjecten en gebruikersobjecten van elke SaaS-app. Sommige apps beheren andere soorten objecten, zoals groepen of contactpersonen. Een van de toewijzingen te selecteren in Hallo tabel ziet u editor voor kolomtoewijzing Hallo toohello rechts, waar ze kunnen worden bekeken en aangepast.

![De resource-blade toepassing][2]

Ondersteunde aanpassingen zijn onder andere:

* Inschakelen en uitschakelen van de toewijzingen voor specifieke objecten, zoals hello Azure AD gebruiker object toohello SaaS van app-gebruikersobject.
* Bewerken welke kenmerken stromen van hello Azure AD gebruiker object toohello van app-gebruikersobject. Zie voor meer informatie over toewijzing van kenmerken [kenmerk toewijzing typen](active-directory-saas-customizing-attribute-mappings.md#understanding-attribute-mapping-types).
* Filter Hallo inrichting acties die Azure AD worden uitgevoerd op Hallo gericht toepassing. In plaats van Azure AD volledig-objecten synchroniseren, kunt u beperken Hallo acties die worden uitgevoerd. Bijvoorbeeld door het selecteren van **Update**, Azure AD-alleen updates bestaande gebruikers-accounts in een toepassing en geen nieuwe maakt. Door het selecteren van **maken**, Azure alleen nieuwe gebruikersaccounts maakt, maar wordt de bestaande bestanden niet bijgewerkt. Deze functie kunnen beheerders toocreate verschillende toewijzingen voor account werkstromen maken en bijwerken.

### <a name="settings"></a>Instellingen
Deze sectie kan beheerders toostart en stop Hallo inrichting Azure AD-service voor de toepassing hello geselecteerd, evenals eventueel wissen Hallo inrichten in de cache en Hallo-service opnieuw starten.

Als inrichting wordt ingeschakeld voor Hallo eerst uitvoert voor een toepassing, inschakelen Hallo service door het wijzigen van Hallo **inrichting Status** te**op**. Dit zorgt ervoor dat het inrichtingsproces service tooperform hello Azure AD voor een eerste synchronisatie, waarbij het Hallo-gebruikers die zijn toegewezen in Hallo leest **gebruikers en groepen** sectie Hallo doeltoepassing voor deze query's en voert deze Hallo inrichten acties die zijn gedefinieerd in Azure AD Hallo **toewijzingen** sectie. Tijdens dit proces slaat Hallo-service inricht in de cache opgeslagen gegevens over welke accounts voor gebruikers die worden beheerd, zodat niet-beheerde accounts in Hallo doeltoepassingen die nooit binnen het bereik van de toewijzing zijn niet worden beïnvloed door de inrichting ongedaan bewerkingen. Na het Hallo synchroniseert initiële synchronisatie, Hallo service automatisch inrichten objecten voor gebruikers en groepen op een interval van tien minuten.

Veranderende Hallo **inrichting Status** te**uit** gewoon gepauzeerd Hallo inrichting service. In deze status Azure niet maken, bijwerken of verwijderen van een gebruiker of groepsobjecten in Hallo-app. Hallo status back tooon wijzigt, Hallo service toopick waar deze was gebleven.

Selecteren Hallo **huidige status wissen en opnieuw starten van synchronisatie** checkbox en opslaan van stopt Hallo inrichting service, dumpbestanden Hallo in de cache opgeslagen gegevens over welke Azure AD-accounts wordt beheerd, Hallo services opnieuw start en voert Hallo initiële synchronisatie opnieuw. Deze optie kunnen beheerders toostart Hallo inrichtingsproces implementatie opnieuw.

### <a name="synchronization-details"></a>Synchronisatiedetails
In dit gedeelte bevat aanvullende informatie over Hallo bewerking Hallo-service inricht, inclusief Hallo eerste en laatste keer Hallo inrichting service hebt uitgevoerd op het Hallo-toepassing en hoeveel gebruikers en groepen objecten worden beheerd.

Koppelingen vindt u toohello **inrichting activiteitenrapport**, waarmee u een logboek van alle gebruikers en groepen hebt gemaakt, bijgewerkt en verwijderd tussen Azure AD en Hallo doeltoepassing en toohello **inrichten, fout rapport** waarmee u meer gedetailleerde foutberichten worden weergegeven voor gebruiker en groep objecten die mislukte toobe gelezen, gemaakt, bijgewerkt of verwijderd. 

##<a name="feedback"></a>Feedback

We hopen u zoals uw Azure AD-ervaring. Zorg ervoor dat Hallo feedback binnenkort! Plaats uw feedback en suggesties voor verbetering van de gebruikerservaring in Hallo **beheerportal** sectie van onze [Feedbackforum](https://feedback.azure.com/forums/169401-azure-active-directory/category/162510-admin-portal).  We Doe enthousiast bent over het bouwen van cool nieuw per dag uit, en uw tooshape richtlijnen gebruiken en definiëren wat we hierna bouwen.


[0]: ./media/active-directory-enterprise-apps-manage-provisioning/enterprise-apps-blade.PNG
[1]: ./media/active-directory-enterprise-apps-manage-provisioning/enterprise-apps-provisioning.PNG
[2]: ./media/active-directory-enterprise-apps-manage-provisioning/enterprise-apps-provisioning-mapping.PNG
