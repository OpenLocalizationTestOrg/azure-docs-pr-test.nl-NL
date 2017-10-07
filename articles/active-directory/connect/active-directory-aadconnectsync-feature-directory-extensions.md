---
title: 'Azure AD Connect-synchronisatie: Directory uitbreidingen | Microsoft Docs'
description: Dit onderwerp beschrijft Hallo directory extensions functie in Azure AD Connect.
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 995ee876-4415-4bb0-a258-cca3cbb02193
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 31525ae914aa4d9e047ea1515b460a8311d5c815
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-directory-extensions"></a>Azure AD Connect-synchronisatie: Directory-uitbreidingen
Directory-uitbreidingen kunt u tooextend Hallo schema in Azure AD met uw eigen kenmerken van lokale Active Directory. Deze functie kunt u LOB-apps toobuild kenmerken u toomanage lokale blijven gebruiken. Deze kenmerken kunnen worden gebruikt via [directory-extensies voor Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) of [Microsoft Graph](https://graph.microsoft.io/). U kunt zien Hallo kenmerken beschikbaar via [explorer van Azure AD Graph](https://graphexplorer.cloudapp.net) en [Microsoft Graph explorer](https://graphexplorer2.azurewebsites.net/) respectievelijk.

Deze kenmerken worden op dit moment geen Office 365-werkbelasting verbruikt.

U welke bijkomende attributen configureren die u wilt dat toosynchronize in Hallo aangepaste instellingen pad in de installatiewizard Hallo.
![Wizard voor schema-uitbreiding](./media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)  
Hallo installatie ziet Hallo kenmerken, die geldige kandidaten zijn te volgen:

* Gebruikers en groepen objecttypen
* Kenmerken met één waarde: String, Boolean, Integer, binair
* Kenmerken met meerdere waarden: String, binair

Hallo-lijst met kenmerken worden gelezen uit de schemacache Hallo gemaakt tijdens de installatie van Azure AD Connect. Als u Active Directory-schema met aanvullende kenmerken Hallo hebt uitgebreid, Hallo [schema moet worden vernieuwd](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema) voordat deze nieuwe kenmerken zichtbaar zijn.

Een object in Azure AD kan too100 directory extensions kenmerken hebben. Hallo maximale lengte is 250 tekens. Als een kenmerkwaarde langer is, wordt deze afgekapt door Hallo synchronisatie-engine.

Tijdens de installatie van Azure AD Connect is een toepassing geregistreerd waar deze kenmerken beschikbaar zijn. Hier ziet u deze toepassing in hello Azure-portal.  
![Schema-uitbreiding App](./media/active-directory-aadconnectsync-feature-directory-extensions/extension3new.png)

Deze kenmerken zijn nu beschikbaar via de grafiek:  
![Graph](./media/active-directory-aadconnectsync-feature-directory-extensions/extension4.png)

Hallo-kenmerken worden voorafgegaan door uitbreiding\_{AppClientId}\_. Hallo AppClientId heeft Hallo dezelfde voor alle kenmerken in uw Azure AD-tenant waarde.

## <a name="next-steps"></a>Volgende stappen
Meer informatie over Hallo [Azure AD Connect-synchronisatie](active-directory-aadconnectsync-whatis.md) configuratie.

Lees meer over het [integreren van uw on-premises identiteiten met Azure Active Directory ](active-directory-aadconnect.md).
