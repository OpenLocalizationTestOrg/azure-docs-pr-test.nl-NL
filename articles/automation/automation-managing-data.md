---
title: aaaManaging gegevens in Azure Automation | Microsoft Docs
description: In dit artikel bevat meerdere onderwerpen voor het beheren van een Azure Automation-omgeving.  Momenteel bevat bewaren van gegevens en back-ups van Azure Automation-noodherstel in Azure Automation.
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: 2896f129-82e3-43ce-b9ee-a3860be0423a
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/02/201
ms.author: magoedte;bwren;sngun
ms.openlocfilehash: 46a164d864c4956c90ab689ca159fff6f6c08028
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-automation-data"></a>Azure Automation-gegevens beheren
In dit artikel bevat meerdere onderwerpen voor het beheren van een Azure Automation-omgeving.

## <a name="data-retention"></a>Bewaartijd van gegevens
Wanneer u een resource in Azure Automation verwijdert, wordt wel worden bewaard gedurende 90 dagen voor controledoeleinden voordat het wordt permanent verwijderd.  Zie of niet Hallo bron gedurende deze tijd gebruikt.  Dit beleid geldt ook tooresources die deel uitmaken van tooan automation-account dat is verwijderd.

Azure Automation wordt automatisch verwijderd en taken die ouder zijn dan 90 dagen permanent verwijderd.

Hallo volgende tabel geeft een overzicht van Hallo bewaarbeleid voor verschillende bronnen.

| Gegevens | Beleid |
|:--- |:--- |
| Accounts |Negentig dagen na het Hallo-account is verwijderd door een gebruiker permanent verwijderd. |
| Assets |Negentig dagen na het Hallo asset door een gebruiker is verwijderd of 90 dagen na Hallo account waarin Hallo asset is verwijderd door een gebruiker permanent verwijderd. |
| Modules |Negentig dagen na het Hallo-module is verwijderd door een gebruiker of 90 dagen na Hallo account van de module Hallo is verwijderd door een gebruiker permanent verwijderd. |
| Runbooks |Negentig dagen na het Hallo-resource wordt verwijderd door een gebruiker of 90 dagen na Hallo rekening met de Hallo resource wordt verwijderd door een gebruiker permanent verwijderd. |
| Taken |Verwijderde en permanent verwijderd 90 dagen na de laatste wordt gewijzigd. Dit kan nadat het Hallo-taak is voltooid, is gestopt of onderbroken zijn. |
| Knooppunt configuraties/MOF-bestanden |Oude knooppuntconfiguratie wordt definitief verwijderd negentig dagen na de configuratie van een nieuw knooppunt wordt gegenereerd. |
| DSC-knooppunten |Permanent verwijderd negentig dagen na het Hallo-knooppunt niet is geregistreerd van Automation-Account met Azure portal of Hallo [Unregister AzureRMAutomationDscNode](https://msdn.microsoft.com/library/mt603500.aspx) cmdlet in Windows PowerShell. Knooppunten zijn 90 dagen na het Hallo-account van de Hallo-knooppunt is verwijderd door een gebruiker ook permanent verwijderd. |
| Knooppunt-rapporten |Nadat een nieuw rapport is gegenereerd voor dat knooppunt de 90 dagen definitief verwijderd |

Hallo bewaarbeleid tooall gebruikers geldt en kan momenteel niet worden aangepast.

Als u tooretain gegevens van een langere periode nodig hebt, kunt u runbook taak logboeken tooLog Analytics doorsturen.  Bekijk voor meer informatie [doorsturen van Azure Automation-taak gegevens tooOMS logboekanalyse](automation-manage-send-joblogs-log-analytics.md).   

## <a name="backing-up-azure-automation"></a>Back-ups maken met Azure Automation
Wanneer u een automation-account in Microsoft Azure verwijdert, worden alle objecten in Hallo-account verwijderd met inbegrip van runbooks, modules, configuraties, instellingen, taken en activa. Hallo-objecten kunnen niet worden hersteld nadat het Hallo-account is verwijderd.  U kunt Hallo informatie toobackup Hallo inhoud van uw automation-account te volgen voordat u het verwijdert. 

### <a name="runbooks"></a>Runbooks
U kunt uw runbooks tooscript bestanden met behulp van hello Azure-beheerportal of Hallo exporteren [Get-AzureAutomationRunbookDefinition](https://msdn.microsoft.com/library/dn690269.aspx) cmdlet in Windows PowerShell.  Deze scriptbestanden kunnen worden geïmporteerd in een andere automation-account, zoals beschreven in [een Runbook maken of importeren](https://msdn.microsoft.com/library/dn643637.aspx).

### <a name="integration-modules"></a>Integratiemodules
U kunt integratiemodules niet exporteren uit Azure Automation.  U moet ervoor zorgen dat ze beschikbaar buiten Hallo automation-account zijn.

### <a name="assets"></a>Assets
Kan niet worden geëxporteerd [activa](https://msdn.microsoft.com/library/dn939988.aspx) van Azure Automation.  Hello Azure Management Portal gebruikt, moet u Noteer Hallo details van variabelen, referenties, certificaten, verbindingen en schema's.  Vervolgens moet u handmatig maken elementen die worden gebruikt door runbooks die u in een andere automation importeren.

U kunt [Azure-cmdlets](https://msdn.microsoft.com/library/dn690262.aspx) tooretrieve details van niet-versleutelde activa vallen of opslaan voor toekomstige verwijzen naar of gelijkwaardige activa in een andere automation-account maken.

Hallo-waarde voor gecodeerde variabelen of Hallo wachtwoordveld van referenties met behulp van cmdlets ophalen niet.  Als u deze waarden niet weet, moet u ze kunt ophalen uit een runbook met behulp van Hallo [Get-AutomationVariable](https://msdn.microsoft.com/library/dn940012.aspx) en [Get-AutomationPSCredential](https://msdn.microsoft.com/library/dn940015.aspx) activiteiten.

U kunt certificaten niet exporteren uit Azure Automation.  U moet ervoor zorgen dat alle certificaten buiten Azure beschikbaar zijn.

### <a name="dsc-configurations"></a>DSC-configuraties
U kunt uw configuraties tooscript bestanden met behulp van hello Azure-beheerportal of Hallo exporteren [Export AzureRmAutomationDscConfiguration](https://msdn.microsoft.com/library/mt603485.aspx) cmdlet in Windows PowerShell. Deze configuraties kunnen worden geïmporteerd en gebruikt in een andere automation-account.

## <a name="geo-replication-in-azure-automation"></a>Geo-replicatie in Azure Automation
Geo-replicatie, standaard in Azure Automation-accounts, een back-up account gegevens tooa verschillende geografische regio voor de redundantie. U kunt een primaire regio kiezen bij het instellen van uw account en is een secundaire regio tooit vervolgens automatisch toegewezen. Hallo secundaire gegevens, gekopieerd vanaf de primaire regio hello wordt voortdurend bijgewerkt in geval van gegevensverlies.  

Hallo volgende tabel ziet u Hallo beschikbare primaire en secundaire regio koppelingen.

| Primair | Secundair |
| --- | --- |
| Zuid-centraal VS |Noord-centraal VS |
| Verenigde Staten (oost 2) |VS - midden |
| West-Europa |Noord-Europa |
| Zuidoost-Azië |Oost-Azië |
| Japan - oost |Japan - west |

In Hallo onwaarschijnlijke geval dat een primaire regiogegevens niet verloren zijn, probeert Microsoft toorecover deze. Als de primaire gegevensbron Hallo kan niet worden hersteld, geo-failover wordt uitgevoerd en hello betrokken klanten ontvangt een melding over deze via hun abonnement.

