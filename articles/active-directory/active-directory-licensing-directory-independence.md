---
title: aaaCharacteristics van Azure Active Directory-tenant intercaction | Microsoft Docs
description: Uw Azure Active-tenant tenants inzicht hebt in uw tenants als volledig onafhankelijke resource beheren
services: active-tenant
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 2b862b75-14df-45f2-a8ab-2a3ff1e2eb08
ms.service: active-tenant
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/27/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017;it-pro
ms.reviewer: piotrci
ms.openlocfilehash: 57b677665c7cb4aee63f518c39d26754fe71a999
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-how-multiple-azure-active-directory-tenants-interact"></a>Begrijpen hoe meerdere tenants van Azure Active Directory gebruiken

In Azure Active Directory (Azure AD), is elke tenant een volledig onafhankelijke resource: een peer die is logisch onafhankelijk van andere tenants die u beheert Hallo. Er is geen bovenliggende / onderliggende relatie tussen de tenants. Deze onafhankelijkheid tussen de tenants bevat resourceonafhankelijkheid, beheeronafhankelijkheid en synchronisatieonafhankelijkheid.

## <a name="resource-independence"></a>Resourceonafhankelijkheid
* Als u maken of verwijderen van een resource in een tenant, heeft dit geen invloed op alle bronnen in een andere tenant, met de Hallo gedeeltelijke uitzondering van externe gebruikers. 
* Als u een van uw domeinnamen met een tenant gebruikt, wordt deze niet gebruikt met een andere tenant.

## <a name="administrative-independence"></a>Beheeronafhankelijkheid
Als een beheergebruiker van de tenant 'Contoso' een testtenant 'Test' vervolgens maakt:

* Hallo-gebruiker die een tenant maakt wordt standaard toegevoegd als een externe gebruiker in die nieuwe tenant en de globale beheerdersrol toegewezen Hallo in deze tenant.
* Beheerders van de tenant 'Contoso' Hallo hebben geen directe beheerdersrechten tootenant 'Test', tenzij de beheerder van 'Test' specifiek hun deze rechten verleent. Echter, 'Contoso' kunnen beheerders toegang tootenant 'Test' als ze bepalen Hallo-gebruikersaccount die gemaakt van 'Test'.
* Als u toevoegen/verwijderen een beheerdersrol voor een gebruiker in een tenant, Hallo wijzigen heeft geen invloed op Hallo beheerdersrollen die Hallo gebruiker heeft in een andere tenant.

## <a name="synchronization-independence"></a>Synchronisatieonafhankelijkheid
U kunt elke Azure AD onafhankelijk tooget gegevens worden gesynchroniseerd vanuit één exemplaar van een tenant:

* Hello Azure AD Connect-hulpprogramma, toosynchronize gegevens met één AD-forest.
* Hallo van Azure Active-tenant Connector voor Forefront Identity Manager, toosynchronize gegevens met een of meer on-premises forests en/of niet-Azure AD-gegevensbronnen.

## <a name="add-an-azure-ad-tenant"></a>Toevoegen van een Azure AD-tenant
tooadd een Azure AD-tenant in hello Azure-portal, meld u aan te[hello Azure-portal](https://portal.azure.com) met een account dat een globale beheerder van Azure AD, en aan de linkerkant hello, selecteert u **nieuw**.

> [!NOTE]
> In tegenstelling tot andere Azure-resources zijn uw tenants niet onderliggende resources van een Azure-abonnement. Als uw Azure-abonnement is geannuleerd of verlopen, kunt u nog steeds toegang tot uw tenant-gegevens met Azure PowerShell of Azure Graph API Hallo Hallo Office 365-beheercentrum. U kunt ook een ander abonnement koppelen aan Hallo-tenant.
>

## <a name="next-steps"></a>Volgende stappen
Zie voor een breed overzicht van Azure AD-licentieverlening problemen en aanbevolen procedures [wat is Azure Active-tenant-licentieverlening?](active-directory-licensing-whatis-azure-portal.md)
