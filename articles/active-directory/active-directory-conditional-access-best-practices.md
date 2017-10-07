---
title: aaaBest procedures voor voorwaardelijke toegang in Azure Active Directory | Microsoft Docs
description: Meer informatie over wat die u moet weten en wat het is raadzaam doen bij het configureren van beleidsregels voor voorwaardelijke toegang.
services: active-directory
keywords: voorwaardelijke toegang tooapps, voorwaardelijke toegang in Azure AD, beveiligde toegang tot resources toocompany, beleidsregels voor voorwaardelijke toegang
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 8c1d978f-e80b-420e-853a-8bbddc4bcdad
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 4952f8746a2e583380b3bb99cfe2fbdae1c07b08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-conditional-access-in-azure-active-directory"></a>Aanbevolen procedures voor voorwaardelijke toegang in Azure Active Directory

In dit onderwerp vindt u informatie over wat die u moet weten en wat het is raadzaam doen bij het configureren van beleidsregels voor voorwaardelijke toegang. Voordat u dit onderwerp leest, moet u vertrouwd raken met Hallo concepten en terminologie Hallo die worden beschreven in [voorwaardelijke toegang in Azure Active Directory](active-directory-conditional-access-azure-portal.md)

## <a name="what-you-should-know"></a>Wat u moet weten

### <a name="whats-required-toomake-a-policy-work"></a>Wat is een beleid werk toomake vereist?

Wanneer u een nieuw beleid maakt, zijn er geen gebruikers, groepen, apps of toegangsbeheer geselecteerd.

![Cloud-apps](./media/active-directory-conditional-access-best-practices/02.png)


toomake uw beleid werken, moet u de volgende Hallo configureren:


|Wat           | Hoe                                  | Waarom|
|:--            | :--                                  | :-- |
|**Cloud-apps** |U moet een of meer apps tooselect.  | Hallo-doel van een beleid voor voorwaardelijke toegang is tooenable toofine-afstemmen hoe gemachtigde gebruikers toegang uw apps tot hebben.|
| **Gebruikers en groepen** | U moet tooselect ten minste één gebruiker of groep die is gemachtigd tooaccess Hallo cloud-apps die u hebt geselecteerd. | Beleid voor voorwaardelijke toegang dat er geen gebruikers en groepen die zijn toegewezen, wordt nooit geactiveerd. |
| **Toegangsbeheer** | U moet tooselect ten minste één toegangsbeheer. | De processor van uw beleid moet tooknow welke toodo indien uw voorwaarden is voldaan.|


In aanvulling toothese basisvereisten, in veel gevallen moet u ook een voorwaarde configureren. Een beleid zou ook werken zonder een geconfigureerde voorwaarde, zijn voorwaarden Hallo aangedreven factor voor toegang tot tooyour apps aan te passen.


![Cloud-apps](./media/active-directory-conditional-access-best-practices/04.png)



### <a name="how-are-assignments-evaluated"></a>Hoe worden toewijzingen geëvalueerd

Alle toewijzingen zijn logische **and**. Als u geconfigureerd, meer dan één toewijzing tootrigger een beleid hebt, moeten alle toewijzingen worden voldaan.  

Als u tooconfigure een locatie-voorwaarde die van toepassing tooall verbindingen moet is vanaf buiten het netwerk van uw organisatie, kunt u dit doen door:

- Inclusief **alle locaties**
- Met uitzondering van **alle goedgekeurde IP-adressen**

### <a name="what-happens-if-you-have-policies-in-hello-azure-classic-portal-and-azure-portal-configured"></a>Wat gebeurt er als er beleid in Hallo klassieke Azure-portal en Azure-portal geconfigureerd?  
Beide beleidsregels worden afgedwongen door Azure Active Directory en Hallo gebruiker krijgt toegang alleen wanneer alle vereisten wordt voldaan.

### <a name="what-happens-if-you-have-policies-in-hello-intune-silverlight-portal-and-hello-azure-portal"></a>Wat gebeurt er als u een beleid in Intune Silverlight portal Hallo en hello Azure Portal hebt?
Beide beleidsregels worden afgedwongen door Azure Active Directory en Hallo gebruiker krijgt toegang alleen wanneer alle vereisten wordt voldaan.

### <a name="what-happens-if-i-have-multiple-policies-for-hello-same-user-configured"></a>Wat gebeurt er als ik heb meerdere beleidsregels voor dezelfde gebruiker geconfigureerd Hallo?  
Voor elke aanmelding, Azure Active Directory evalueert alle beleidsregels en zorgt ervoor dat alle vereisten wordt voldaan voordat verleende toegang toohello gebruiker.


### <a name="does-conditional-access-work-with-exchange-activesync"></a>Werkt voorwaardelijke toegang met Exchange ActiveSync?

Ja, kunt u Exchange ActiveSync in een beleid voor voorwaardelijke toegang.


## <a name="what-you-should-avoid-doing"></a>Wat moet u niet doen

Hallo voorwaardelijke toegang framework biedt u de flexibiliteit van een geweldige configuratie. Echter hoge mate van flexibiliteit betekent ook dat u zorgvuldig elke configuratie beleid voorafgaande tooreleasing het tooavoid ongewenste resultaten. In deze context moet u speciale aandacht schenken tooassignments zoals die invloed hebben op volledige set betalen **alle gebruikers / groepen / cloud-apps**.

In uw omgeving, moet u voorkomen Hallo volgende configuraties:


**Voor alle gebruikers alle cloud-apps:**

- **Toegang blokkeren** -uw hele organisatie, absoluut niet verstandig is deze configuratie wordt geblokkeerd.

- **Vereisen dat apparaat compatibel** - voor gebruikers die niet hun apparaten hebben ingeschreven, maar dit beleid wordt alle toegang inclusief toohello Intune-portal toegang geblokkeerd. Als u een beheerder met een geregistreerd apparaat, wordt dit beleid u uit om terug te zetten naar hello Azure portal toochange Hallo beleid blokkeert.

- **Domeinlidmaatschap vereisen** : dit beleid blok toegang heeft ook Hallo potentiële tooblock toegang voor alle gebruikers in uw organisatie als u een apparaat domein nog geen hebt.


**Voor alle gebruikers, alle cloud-apps, alle platforms:**

- **Toegang blokkeren** -uw hele organisatie, absoluut niet verstandig is deze configuratie wordt geblokkeerd.


## <a name="common-scenarios"></a>Algemene scenario's

### <a name="requiring-multi-factor-authentication-for-apps"></a>Meervoudige verificatie vereisen voor apps

Veel omgevingen hebben apps waarvoor een hoger niveau van beveiliging dan Hallo anderen.
Dit is bijvoorbeeld Hallo geval voor apps die u toegang tot toosensitive gegevens hebt.
Als u op een andere laag van beveiliging toothese apps tooadd wilt, kunt u een beleid voor voorwaardelijke toegang waarvoor multi-factor authentication-server is vereist wanneer gebruikers toegang hebben tot deze apps kunt configureren.


### <a name="requiring-multi-factor-authentication-for-access-from-networks-that-are-not-trusted"></a>Meervoudige verificatie vereisen voor toegang via netwerken die geen vertrouwde

Dit scenario is vergelijkbaar toohello vorige scenario, omdat een vereiste voor multi-factor authentication wordt toegevoegd.
Hallo belangrijkste verschil is echter Hallo voorwaarde voor deze vereiste.  
Tijdens het Hallo focus van het vorige scenario Hallo werd op apps met toegang tot toosensitve gegevens, wordt dit scenario Hallo richt zich op vertrouwde locaties.  
U wellicht een vereiste voor multi-factor authentication met andere woorden, als een app wordt geopend door een gebruiker vanaf een netwerk dat u niet vertrouwt.


### <a name="only-trusted-devices-can-access-office-365-services"></a>Alleen vertrouwde apparaten hebben toegang tot Office 365-services

Als u van Intune in uw omgeving gebruikmaakt, kunt u onmiddellijk starten met Hallo voorwaardelijk beleid interface in hello Azure-console.

Veel klanten van Intune voorwaardelijke toegang tooensure of alleen vertrouwde apparaten toegang Office 365-services tot gebruikt. Dit betekent dat mobiele apparaten zijn ingeschreven bij Intune en voldoen aan nalevingsvereisten van beleid en de Windows-pc's die zijn gekoppeld tooan lokaal domein. Een verbetering van de belangrijkste is dat u geen hebt tooset Hallo hetzelfde beleid voor elk Hallo Office 365-services.  Wanneer u een nieuw beleid maakt, configureert u Hallo Cloud-apps tooinclude elke Hallo O365-Apps die u wenst dat tooprotect met met voorwaardelijke toegang.

## <a name="next-steps"></a>Volgende stappen

Als u wilt dat tooknow hoe tooconfigure beleid voor voorwaardelijke toegang, Zie [aan de slag met voorwaardelijke toegang in Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).
