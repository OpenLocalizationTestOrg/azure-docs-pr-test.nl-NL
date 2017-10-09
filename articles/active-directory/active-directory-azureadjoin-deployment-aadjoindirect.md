---
title: aaaUsage scenario's en overwegingen voor de implementatie voor deelname aan Azure AD | Microsoft Docs
description: Legt uit hoe beheerders kunnen Azure AD Join instellen voor hun eindgebruikers (werknemers, studenten en andere gebruikers). Het Hallo verschillende real-world scenario's voor het gebruik van Azure AD Join wordt ook beschreven.
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 81d4461e-21c8-4fdd-9076-0e4991979f62
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 7e57971481aa312ebf8a69999d194f9dcc3d4708
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="usage-scenarios-and-deployment-considerations-for-azure-ad-join"></a>Gebruiksscenario's en overwegingen voor de implementatie voor deelname aan Azure AD
## <a name="usage-scenarios-for-azure-ad-join"></a>Gebruiksscenario's voor Azure AD Join
### <a name="scenario-1-businesses-largely-in-hello-cloud"></a>Scenario 1: Bedrijven grotendeels in Hallo cloud
Azure Active Directory Join (Azure AD Join) profiteert u als u momenteel werkt en identiteiten voor uw bedrijf in de cloud Hallo beheren of toohello cloud snel verplaatst. U kunt een account dat u hebt gemaakt in Azure AD-toosign in tooWindows 10 gebruiken. Via [Hallo eerst uitvoeren ervaring (FRX) proces](active-directory-azureadjoin-user-frx.md), of door deelname aan Azure AD van [Hallo instellingen menu](active-directory-azureadjoin-user-upgrade.md), uw gebruikers kunnen hun computers tooAzure AD verbinden.  Uw gebruikers kunnen ook profiteren van eenmalige aanmelding (SSO) toegang te cloudresources zoals Office 365 in hun browser of in de Office-toepassingen.

### <a name="scenario-2-educational-institutions"></a>Scenario 2: Onderwijsinstellingen
Onderwijsinstellingen hebben doorgaans twee gebruikerstypen: onderwijsmedewerkers en studenten. Onderwijsmedewerkers leden worden beschouwd als langere leden van Hallo-organisatie. Maken van lokale accounts voor ze is het wenselijk. Maar studenten korterlopende lid zijn van de organisatie Hallo en hun accounts kunnen worden beheerd in Azure AD. Dit betekent dat directory scale kan worden geactiveerd toohello cloud in plaats van alleen lokaal opgeslagen. Het betekent ook dat studenten wordt kunnen toosign in tooWindows met hun Azure AD-accounts en ze toegang krijgen tooOffice 365 resources in Office-toepassingen.

### <a name="scenario-3-retail-businesses"></a>Scenario 3: Retail bedrijven
Detailhandel bedrijven hebben seizoensgebonden werknemers en op lange termijn werknemers. U meestal on-premises-accounts maken en gebruiken van domein machines voor langere fulltime werknemers. Maar seizoensgebonden werknemers korterlopende lid zijn van de organisatie Hallo en is het wenselijk toomanage hun accounts waarbij gebruikerslicenties kunnen eenvoudiger kan worden verplaatst om. Als u hun gebruikersaccounts in de cloud met Office 365-licenties hello maakt, krijgt deze gebruikers Hallo voordelen van aanmelding tooWindows en Office-toepassingen met een Azure AD-account, terwijl u meer flexibiliteit met de licenties worden onderhouden nadat ze verlaten.

### <a name="scenario-4-additional-scenarios"></a>Scenario 4: Aanvullende scenario 's
Samen met de Hallo voordelen eerder besproken, profiteert u dat uw gebruikers hun apparaten tooAzure AD join vanwege een vereenvoudigde gekoppelde ervaring, efficiënte Apparaatbeheer, automatische mobiele apparaat management inschrijving en tooAzure voor eenmalige aanmelding AD en on-premises resources.  

## <a name="deployment-considerations-for-azure-ad-join"></a>Overwegingen voor de implementatie voor deelname aan Azure AD
### <a name="enable-your-users-toojoin-a-company-owned-device-directly-tooazure-ad"></a>Inschakelen van uw gebruikers toojoin een apparaat in Bedrijfseigendom rechtstreeks tooAzure AD
Ondernemingen kunnen bieden alleen in de cloud accounts toopartner bedrijven en organisaties. Deze partners kunnen vervolgens gemakkelijk toegang tot bedrijfs-apps en resources met eenmalige aanmelding. Dit scenario is van toepassing toousers die toegang hebben tot bronnen voornamelijk in Hallo cloud, zoals Office 365 of SaaS-apps die afhankelijk van Azure AD voor verificatie zijn.

### <a name="prerequisites"></a>Vereisten
**Op ondernemingsniveau hello (beheerder)**

* Azure-abonnement met Azure Active Directory  

**Op gebruikersniveau Hallo**

* Windows 10 (Professional en Enterprise-edities)

### <a name="administrator-tasks"></a>Beheerderstaken
* [Apparaatregistratie instellen](active-directory-azureadjoin-setup.md)

### <a name="user-tasks"></a>Gebruikerstaken
* [Instellen van een nieuwe Windows 10-apparaat met Azure AD tijdens de installatie](active-directory-azureadjoin-user-frx.md)
* [Instellen van een Windows 10-apparaat met Azure AD in Hallo-instellingen](active-directory-azureadjoin-user-upgrade.md)
* [Deelnemen aan een persoonlijke tooyour organisatie voor Windows 10-apparaat](active-directory-azureadjoin-personal-device.md)

## <a name="enable-byod-in-your-organization-for-windows-10"></a>BYOD inschakelen in uw organisatie voor Windows 10
U kunt uw gebruikers en werknemers toouse instellen hun persoonlijke Windows-apparaten (BYOD) tooaccess bedrijfs-apps en resources. Uw gebruikers kunnen hun Azure AD-accounts (werk of school-accounts) tooa persoonlijke Windows-apparaat tooaccess resources toevoegen op een wijze beveiligd en compatibel zijn.

### <a name="prerequisites"></a>Vereisten
**Op ondernemingsniveau hello (beheerder)**

* Azure AD-abonnement

**Op gebruikersniveau Hallo**

* Windows 10 (Professional en Enterprise-edities)

### <a name="administrator-tasks"></a>Beheerderstaken
* [Apparaatregistratie instellen](active-directory-azureadjoin-setup.md)

### <a name="user-tasks"></a>Gebruikerstaken
* [Deelnemen aan een persoonlijke tooyour organisatie voor Windows 10-apparaat](active-directory-azureadjoin-personal-device.md)

## <a name="additional-information"></a>Aanvullende informatie
* [Windows 10 voor Hallo ondernemingen: manieren toouse apparaten for work.](active-directory-azureadjoin-windows10-devices-overview.md)
* [Cloud-mogelijkheden tooWindows 10-apparaten via Azure Active Directory Join uitbreiden](active-directory-azureadjoin-user-upgrade.md)
* [Identiteiten zonder wachtwoorden via Microsoft Passport verifiëren](active-directory-azureadjoin-passport.md)
* [Learn about usage scenarios for Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md) (Gebruiksscenario’s voor Azure AD Join)
* [Verbinding maken met domein apparaten tooAzure AD voor Windows 10-ervaring](active-directory-azureadjoin-devices-group-policy.md)
* [Azure AD Join instellen](active-directory-azureadjoin-setup.md)

