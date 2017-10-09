---
title: aaaFind uit wanneer een specifieke gebruiker kunnen tooaccess een toepassing worden | Microsoft Docs
description: Hoe toofind uit wanneer een gebruiker zeer belangrijk kunnen tooaccess een toepassing worden u hebt geconfigureerd voor gebruikers inrichten met Azure AD
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: bb9520499dcc8bbbe6fae05c5238c8852815ea0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-when-a-specific-user-will-be-able-tooaccess-an-application"></a>Nagaan wanneer een specifieke gebruiker kunnen tooaccess een toepassing worden
Wanneer u automatisch gebruikers inrichten met een toepassing, Azure AD automatisch inrichten en update gebruikersaccounts in een app op basis van items zoals [toewijzing van gebruikers en groepen](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) op een regelmatig geplande tijdstip interval, doorgaans elke tien minuten.

## <a name="how-long-does-it-take"></a>Hoe lang duurt het?

Hallo-tijd die nodig is voor een bepaalde gebruiker toobe ingericht afhankelijk hoofdzakelijk of er een initiële synchronisatie 'volledige' al is gebeurd.

Hallo eerste synchronisatie tussen Azure AD en een app kan overal 20 minuten tooseveral uur duren, afhankelijk van Hallo grootte van hello Azure AD-directory en Hallo aantal gebruikers in het bereik voor het inrichten. 

Volgende synchronisaties na de initiële synchronisatie Hallo sneller zijn (bijvoorbeeld binnen 10 minuten), zoals het Hallo-service inricht watermerken waarbij Hallo status van beide systemen na de initiële synchronisatie hello, verbeterde prestaties van de volgende synchronisatie worden opgeslagen.

## <a name="how-toocheck-hello-status-of-a-user"></a>Hoe toocheck Hallo status van een gebruiker

toosee hello inrichting status voor de geselecteerde gebruiker, raadpleegt u Hallo auditlogboeken in Azure AD.

Hallo inrichting controlelogboeken kan worden geopend in hello Azure-portal, op Hallo **Azure Active Directory &gt; zakelijke Apps &gt; \[toepassingsnaam\] &gt; Audit logboeken**tabblad. Filter Hallo Hallo aanmeldt **Account inrichten** categorie tooonly Zie Hallo gebeurtenissen voor die app-inrichting. U kunt zoeken naar gebruikers op basis van Hallo 'overeenkomende ID' die is geconfigureerd voor deze in Hallo kenmerktoewijzingen. 

Bijvoorbeeld, als u Hallo 'user principal name' of 'e-mailadres' als Hallo die overeenkomt met het kenmerk hello Azure AD-zijde geconfigureerd en Hallo gebruiker niet inrichten heeft de waarde 'audrey@contoso.com", klikt u vervolgens zoeken Hallo de auditlogboeken voor"audrey@contoso.com"en vervolgens controleren items geretourneerd.

Hallo inrichting audit logboek vastgelegd alle bewerkingen die worden uitgevoerd door het Hallo-service, inrichting Hallo met inbegrip van:

* Uitvoeren van query's Azure AD voor toegewezen gebruikers die zich binnen het bereik van de inrichting
* Hallo doel app Hallo aanwezigheid van deze gebruikers opvragen
* Hallo gebruikersobjecten tussen Hallo system vergelijken
* Toevoegen, bijwerken of Hallo-gebruikersaccount in Hallo doelsysteem op basis van de vergelijking Hallo uitschakelen

## <a name="next-steps"></a>Volgende stappen
[Gebruikers inrichten en Deprovisioning tooSaaS toepassingen met Azure Active Directory automatiseren](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning)''
