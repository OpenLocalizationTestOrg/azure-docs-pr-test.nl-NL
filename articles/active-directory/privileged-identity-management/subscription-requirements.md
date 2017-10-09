---
title: aaaPrivileged identiteitsbeheer abonnementen - Azure | Microsoft Docs
description: Verklaart Hallo abonnement en vereisten voor het beheren en gebruiken van Azure AD Privileged Identity Management in uw tenant-licentieverlening
services: active-directory
documentationcenter: 
author: barclayn
manager: mbaldwin
editor: mwahl
ms.assetid: 34367721-8b42-4fab-a443-a2e55cdbf33d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: barclayn
ms.custom: pim
ms.openlocfilehash: 2639d13c250a582fdcf0b277c9bab37fdfcabcb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-privileged-identity-management-subscription-requirements"></a>Vereisten voor Azure Active Directory Privileged Identity Management abonnement

Azure AD Privileged Identity Management is beschikbaar als onderdeel van Hallo Premium P2-editie van Azure AD. Zie voor meer informatie over het Hallo andere functies van P2 en een vergelijking tooPremium P1, [Azure Active Directory-edities](../active-directory-editions.md).

>[!NOTE]
Wanneer u Azure Active Directory (Azure AD) Privileged Identity Management is in de preview, zijn er geen controles licentie voor een tenant tootry Hallo-service.  Nu dat Azure AD Privileged Identity Management is algemeen beschikbaar is bereikt, moet een proef- of betaald abonnement aanwezig zijn voor Hallo tenant toocontinue Privileged Identity Management na December 2016 gebruiken.
  

## <a name="confirm-your-trial-or-paid-subscription"></a>Bevestig uw proef- of betaald abonnement

Als u niet zeker weet of uw organisatie beschikt over een proefversie of abonnement hebt aangeschaft, u controleren kunt of er een abonnement in uw tenant is met behulp van Hallo-opdrachten die zijn opgenomen in Azure Active Directory-Module voor Windows PowerShell V1. 
1. Open een PowerShell-venster.
2. Voer `Connect-MsolService` tooauthenticate als een gebruiker in uw tenant.
3. Voer `Get-MsolSubscription | ft SkuPartNumber,IsTrial,Status`.

Deze opdracht wordt een lijst met abonnementen in uw tenant Hallo opgehaald. Als er dat geen regels geretourneerd, moet u een Azure AD Premium-P2 tooobtain proefversie, een abonnement voor Azure AD Premium-P2 of EMS E5 abonnement toouse Azure AD Privileged Identity Management aanschaffen.  een proefversie tooget en begin met behulp van Azure AD Privileged Identity Management lezen [aan de slag met Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-getting-started.md).

Als u deze opdracht retourneert een regel in welke SkuPartNumber is 'AAD_PREMIUM_P2' of 'EMSPREMIUM' en IsTrial is 'True', dit geeft aan dat een proefversie van Azure AD Premium-P2 aanwezig is in het Hallo-tenant.  Als Hallo abonnementsstatus is niet ingeschakeld en u een Azure AD Premium P2- of EMS E5 abonnement kopen hebt, moet vervolgens u een abonnement voor Azure AD Premium-P2 of aanschaffen EMS E5 abonnement toocontinue met behulp van Azure AD Privileged Identity Management.

Azure AD Premium-P2 is beschikbaar via een [Microsoft Enterprise Agreement](https://www.microsoft.com/en-us/licensing/licensing-programs/enterprise.aspx), Hallo [Open Volume License-programma](https://www.microsoft.com/en-us/licensing/licensing-programs/open-license.aspx), en Hallo [programma Cloud Solution Providers](https://partner.microsoft.com/en-US/cloud-solution-provider). Azure en Office 365-abonnees zijn ook verkrijgbaar online Azure AD Premium-P2.  Meer informatie over prijzen voor Azure AD Premium en hoe tooorder online kan worden gevonden op [Azure Active Directory prijzen](https://azure.microsoft.com/en-us/pricing/details/active-directory/).

## <a name="azure-ad-privileged-identity-management-is-not-available-in-tenant"></a>Azure AD Privileged Identity Management is niet beschikbaar in de tenant

Azure AD Privileged Identity Management wordt niet langer beschikbaar in uw tenant als:
- Uw organisatie is Azure AD Privileged Identity Management gebruikt bij het Preview-versie is en niet heeft aangeschaft Azure AD Premium P2-abonnement of EMS E5-abonnement.
- Uw organisatie heeft een Azure AD Premium-P2 of EMS E5 evaluatieversie die verlopen.
- Uw organisatie heeft een aangeschafte abonnement dat is verlopen.

Wanneer u een Azure AD Premium P2-abonnement of EMS E5-abonnement is verlopen, of een biedt organisatie die werkt met Azure AD Privileged Identity Management in preview Azure AD Premium P2- of EMS E5-abonnement niet ophalen:

- Permanente rol toewijzingen tooAzure AD rollen niet worden gewijzigd.
- Hello Azure AD Privileged Identity Management-extensie in hello Azure-portal, evenals Hallo Graph API-cmdlets en PowerShell-interfaces van Azure AD Privileged Identity Management wordt niet langer beschikbaar voor gebruikers tooactivate bevoegde rollen, beheren bevoegde toegang of toegang beoordelingen van bevoorrechte rollen uit te voeren.
- In aanmerking komende roltoewijzingen van Azure AD-rollen worden verwijderd, wanneer gebruikers zich niet meer kunnen tooactivate bevoegde rollen.
- Alle beoordelingen lopende toegang van Azure AD-rollen wordt beëindigd en Azure AD Privileged Identity Management-configuratie-instellingen worden verwijderd.
- Azure AD Privileged Identity Management wordt niet langer met het verzenden van e-mailberichten op wijzigingen aan toewijzingen van rollen.

## <a name="next-steps"></a>Volgende stappen

- [Aan de slag met Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-getting-started.md)
- [Rollen in Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-roles.md)
