---
title: aaaRestore een verwijderde Office 365-groep in Azure Active Directory | Microsoft Docs
description: Hoe een verwijderde groep toorestore terug te zetten groepen weergeven en permamnently een groep in Azure Active Directory verwijderen
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cc5f232a-1e77-45c2-b28b-1fcb4621725c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: curtand
ms.openlocfilehash: 4e6650d64aa19f0c909f1c511f48681de8032f63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-deleted-office-365-group-in-azure-active-directory"></a>Een verwijderde Office 365-groep in Azure Active Directory herstellen

Wanneer u een Office 365-groep in Azure Active Directory (Azure AD) Hallo verwijdert, is Hallo verwijderde groep behouden, maar niet zichtbaar voor 30 dagen van de datum van verwijdering Hallo. Dit is zodat Hallo groep en de inhoud ervan kunnen worden hersteld indien nodig. Deze functionaliteit is beperkt uitsluitend tooOffice 365 groepen in Azure AD. Het is niet beschikbaar voor beveiligingsgroepen en distributiegroepen.

> [!NOTE] 
> Gebruik geen `Remove-MsolGroup` omdat het Hallo-groep permanent worden verwijderd. Gebruik altijd `Remove-AzureADMSGroup` toodelete een O365-groep. 

Hallo machtigingen vereist toorestore een groep mag geen van de volgende Hallo:

Rol  | Machtigingen 
--------- | ---------
Bedrijfsbeheerder, Partner Tier2 ondersteuning en beheerders van InTune-Service | Een verwijderde groep voor Office 365 kunt herstellen 
Ondersteuning voor de beheerder van gebruiker en Partner Tier1 | Een verwijderde groep Office 365, behalve die toegewezen toohello Company Administrator-rol kunt herstellen 
Gebruiker | Een verwijderde Office 365-groep waarvan ze eigenaar kunt herstellen 


## <a name="view-hello-deleted-office-365-groups-that-are-available-toorestore"></a>Weergave Hallo Office 365-groepen die beschikbaar toorestore zijn verwijderd
Hallo cmdlets volgen kan gebruikte tooview Hallo verwijderd groepen tooverify die een Hallo of toepassingsgroepen die u geïnteresseerd bent in zijn niet nog permanent verwijderd. Deze cmdlets deel uitmaken van Hallo [Azure AD PowerShell-module](https://www.powershellgallery.com/packages/AzureAD/). Meer informatie over deze module vindt u in Hallo [Azure Active Directory PowerShell versie 2](/powershell/azure/install-adv2?view=azureadps-2.0) artikel.

1.  Hallo volgende cmdlet toodisplay verwijderd Office 365-groepen in uw tenant die nog steeds beschikbaar toorestore zijn uitgevoerd.
  ```
  Get-AzureADMSDeletedGroup
  ```

2.  Ook als u Hallo objectID van een specifieke groep weet (en u dit van de cmdlet Hallo in stap 1 downloaden kunt) heeft Voer Hallo volgende cmdlet tooverify die specifieke verwijderde groep Hallo niet nog is permanent verwijderd.
  ```
  Get-AzureADMSDeletedGroup –Id <objectId>
  ```



## <a name="how-toorestore-your-deleted-office-365-group"></a>Hoe toorestore uw verwijderde Office 365-groep
Zodra u hebt gecontroleerd dat die groep Hallo toorestore nog steeds beschikbaar is, moet u Hallo verwijderd groep herstellen met een Hallo stappen te volgen. Als Hallo groep documenten, SP sites of andere permanente objecten bevat, kan het too24 uren toofully terugzetten duren een groep en de inhoud ervan.

1.  Voer hello volgende cmdlet toorestore Hallo groep en de inhoud ervan.
  
  ```
  Restore-AzureADMSDeletedDirectoryObject –Id <objectId>
  ``` 

U kunt ook kan hello volgende cmdlet worden uitgevoerd groep voor toopermanently verwijderen Hallo verwijderd.
  ```
  Remove-AzureADMSDeletedDirectoryObject –Id <objectId>
  ```

## <a name="how-do-you-know-this-worked"></a>Hoe weet u Hiermee gewerkte?
tooverify dat u hebt een Office 365-groep Hallo uitvoeren is hersteld `Get-AzureADGroup –ObjectId <objectId>` cmdlet toodisplay informatie over het Hallo-groep. Na het terugzetten van Hallo is aanvraag voltooid:
- Hallo-groep wordt weergegeven in de linkernavigatiebalk Hallo op Exchange
- Hallo-plan voor Hallo groep wordt weergegeven in de Planner
- Alle Sharepoint-sites en de bijbehorende inhoud is beschikbaar
- Hallo groep toegankelijk zijn vanaf elke Hallo Exchange eindpunten en andere Office 365-werkbelastingen die ondersteuning bieden voor Office 365-groepen


## <a name="next-steps"></a>Volgende stappen
Deze artikelen bevatten aanvullende informatie over Azure Active Directory-groepen.

* [Zie de bestaande groepen](active-directory-groups-view-azure-portal.md)
* [Instellingen van een groep beheren](active-directory-groups-settings-azure-portal.md)
* [Leden van een groep beheren](active-directory-groups-members-azure-portal.md)
* [Lidmaatschap van een groep beheren](active-directory-groups-membership-azure-portal.md)
* [Dynamische regels voor gebruikers in een groep beheren](active-directory-groups-dynamic-membership-azure-portal.md)
