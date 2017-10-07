---
title: aaaWhat is licentieverlening in Azure Active Directory op basis van groep? | Microsoft Docs
description: Beschrijving van Azure Active Directory op basis van een groep licenties, hoe het werkt en aanbevolen procedures
services: active-directory
keywords: Azure AD-licentieverlening
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/29/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: H1Hack27Feb2017;it-pro
ms.openlocfilehash: 11647de6b76022cd2393751fcafc67ce671aeba6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="group-based-licensing-basics-in-azure-active-directory"></a>Licentieverlening basisbeginselen op basis van een groep in Azure Active Directory

Met Microsoft cloud-services, zoals Office 365, Enterprise Mobility + Security Dynamics CRM en andere vergelijkbare producten betaald vereist licenties. Deze licenties zijn tooeach-gebruiker die toegang tot toothese services moet worden toegewezen. toomanage licenties beheerders gebruik een van de Hallo beheerportals (Office of Azure) en PowerShell-cmdlets. Azure Active Directory (Azure AD) is Hallo onderliggende infrastructuur die ondersteuning biedt voor identiteitsbeheer voor alle Microsoft-cloudservices. Azure AD bevat informatie over toewijzing licentiestatussen voor gebruikers.

Tot op heden kunnen alleen licenties worden toegewezen op Hallo afzonderlijke gebruikersniveau, waardoor grootschalige management moeilijk. Bijvoorbeeld tooadd of verwijder Gebruikerslicenties op basis van veranderingen in de organisatie, zoals gebruikers toevoegen of verlaten Hallo organisatie of een afdeling, een beheerder vaak moet een complexe PowerShell script schrijven. Dit script worden afzonderlijke aanroepen toohello-cloudservice.

tooaddress die uitdagingen, Azure AD nu bevat op basis van een groep licenties. U kunt een of meer licenties tooa productgroep toewijzen. Azure AD zorgt ervoor dat Hallo licenties tooall leden van Hallo groep zijn toegewezen. Nieuwe leden die lid worden van groep Hallo zijn de juiste licenties Hallo toegewezen. Wanneer ze Hallo groep verlaten, wordt deze licenties zijn verwijderd. Hierdoor niet Hallo nodig voor het automatiseren van Licentiebeheer via PowerShell tooreflect wijzigingen Hallo-organisatie en de afdelingen structuur op per-gebruiker.

## <a name="features"></a>Functies

Hier volgen Hallo belangrijkste functies van de groep gebaseerde licentieverlening:

- Licenties kunnen tooany beveiligingsgroep worden toegewezen in Azure AD. Beveiligingsgroepen kunnen gesynchroniseerde on-premises worden met behulp van Azure AD Connect. U kunt ook beveiligingsgroepen maken rechtstreeks in Azure AD (ook wel groepen alleen in de cloud) of automatisch via het onderdeel van de dynamische groep hello Azure AD.

- Wanneer een productlicentie is toegewezen tooa groep, kunt Hallo beheerder een of meer service-abonnementen in Hallo product uitschakelen. Dit gebeurt meestal wanneer Hallo organisatie is nog niet klaar toostart met een service die deel uitmaken van een product. Hallo beheerder kan bijvoorbeeld Office 365 tooa afdeling toewijzen, maar Hallo Yammer service tijdelijk uitschakelen.

- Alle Microsoft cloud-services die op gebruikersniveau licentieverlening vereisen worden ondersteund. Dit omvat alle Office 365-producten, Enterprise Mobility + Security, en Dynamics CRM.

- Op basis van een groep-licentieverlening is momenteel alleen beschikbaar via [hello Azure-portal](https://portal.azure.com). Als u voornamelijk andere beheerportals voor gebruikers- en groepsbeheer, zoals Hallo Office 365-portal, kunt u dus toodo blijven. Maar moet u hello Azure portal toomanage licenties op groepeerniveau van de.

- Azure AD worden beheerd, licentie-wijzigingen die het gevolg zijn van wijzigingen voor een groepslidmaatschap. Licentie wijzigingen zijn meestal effectieve binnen enkele minuten een wijziging lidmaatschap.

- Een gebruiker kan lid zijn van meerdere groepen met licentie-beleidsregels die zijn opgegeven. Een gebruiker kan ook een aantal licenties die rechtstreeks zijn toegewezen, buiten groepen hebben. Hallo waardoor de status van gebruiker is een combinatie van alle toegewezen product en service-licenties.

- In sommige gevallen kunnen niet de licenties worden toegewezen aan gebruiker tooa. Bijvoorbeeld, er mogelijk niet voldoende beschikbare licenties in Hallo tenant of conflicterende services mogelijk zijn toegewezen op Hallo dezelfde tijd. Beheerders hebben toegang tot tooinformation over gebruikers voor wie Azure AD niet volledig groep licenties verwerken kan. Ze kunnen los problemen op basis van die gegevens.

- Een betaald of proefversie abonnement voor Azure AD Basic of Premium-editie is tijdens de openbare preview vereist in Hallo tenant toouse op basis van een groep Licentiebeheer.

## <a name="next-steps"></a>Volgende stappen

toolearn meer informatie over andere scenario's voor Licentiebeheer via Groepsbeleid-licentieverlening, Zie:

* [Aan de slag met Azure Active Directory-licenties](active-directory-licensing-get-started-azure-portal.md)
* [Toewijzen van licenties tooa groep in Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md)
* [Opsporen en oplossen van licentieproblemen met een voor een groep in Azure Active Directory](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [Hoe toomigrate afzonderlijk in licentie gegeven gebruikers licentieverlening in Azure Active Directory op basis van toogroup](active-directory-licensing-group-migration-azure-portal.md)
* [Azure Active Directory-licentieverlening voor aanvullende scenario's op basis van groep](active-directory-licensing-group-advanced.md)
