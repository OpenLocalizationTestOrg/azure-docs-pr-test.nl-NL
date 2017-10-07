---
title: Azure Automation-account van logboekanalyse aaaUnlink | Microsoft Docs
description: Dit artikel bevat een overzicht van hoe toounlink uw Azure Automation-account van een OMS-werkruimte.
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: how-to-article
ms.date: 02/07/2017
ms.author: magoedte
ms.openlocfilehash: 3ec0745673f6a872538d33023a7a1d2bb1d18ec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toounlink-your-automation-account-from-a-log-analytics-workspace"></a>Hoe toounlink uw Automation-account van een werkruimte voor logboekanalyse

Azure Automation worden geïntegreerd met logboekanalyse toonot alleen ondersteuning voor proactieve controle van uw runbooktaken voor alle Automation-accounts, maar is ook vereist bij het importeren van oplossingen die afhankelijk van logboekanalyse zijn na Hallo:

* [Updatebeheer](../operations-management-suite/oms-solution-update-management.md)
* [Tracering wijzigen](../log-analytics/log-analytics-change-tracking.md)
* [Virtuele machines starten/stoppen buiten kantooruren](automation-solution-vm-management.md)
 
Als u dat u niet langer wenst toointegrate uw Automation-account met Log Analytics besluit, kunt u uw account rechtstreeks vanuit hello Azure-portal kunt ontkoppelen.  Voordat u doorgaat, moet u eerst tooremove Hallo oplossingen eerder vermeld, anders dit proces zal worden voorkomen dat u doorgaat.  Controleer Hallo onderwerp voor een bepaalde oplossing Hallo hebt toounderstand Hallo stappen die nodig is geïmporteerd tooremove deze.  

Na het verwijderen van deze oplossingen kunt u uw Automation-account te volgen stappen toounlink Hallo uitvoeren.

## <a name="unlink-workspace"></a>Ontkoppelen van de werkruimte

1. Open uw Automation-account van hello Azure-portal, en selecteer in Hallo Automation-accountblade Hallo account Blade **ontkoppelen werkruimte**.<br><br> ![Werkruimte optie ontkoppelen](media/automation-unlink-from-log-analytics/automation-unlink-workspace-option.png)<br><br>  
2. Klik op Hallo ontkoppelen werkruimte blade **worksapce ontkoppelen**.<br><br> ![Ontkoppelen van de werkruimte blade](media/automation-unlink-from-log-analytics/automation-unlink-workspace-blade.png).<br><br>  U wordt gevraagd u tooproceed wilt controleren.<br><br>
3. Terwijl Azure Automation toounlink Hallo account werkruimte voor logboekanalyse probeert, u kunt de voortgang Hallo onder volgen **meldingen** in Hallo-menu.

Als u Hallo updatebeheer oplossing gebruikt, kunt indien gewenst u tooremove Hallo items die niet langer nodig zijn na het verwijderen van Hallo oplossing te volgen.

* Schema's worden bijgewerkt.  Elk moeten namen die overeenkomen met de Hallo-update-implementaties die u hebt gemaakt)

* Hybrid worker-groepen is gemaakt voor Hallo-oplossing.  Elke naam op dezelfde manier te machine1.contoso.com_9ceb8108 - 26 c 9-4051-b6b3-227600d715c8).

Als u virtuele machines starten/stoppen van Hallo tijdens rustige uren oplossing gebruikt, kunt eventueel u tooremove Hallo items die niet langer nodig zijn na het verwijderen van Hallo oplossing te volgen.

* Starten en stoppen van runbook-planningen VM 
* VM-runbooks starten en stoppen
* Variabelen   

## <a name="next-steps"></a>Volgende stappen

tooreconfigure uw Automation-account toointegrate met OMS Log Analytics, Zie [taakstatus en taak streams doorsturen van Automation tooLog logboekanalyse (OMS)](automation-manage-send-joblogs-log-analytics.md). 
