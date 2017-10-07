---
title: aaaGet slag met Azure Scheduler in Azure portal | Microsoft Docs
description: Aan de slag met Azure Scheduler in Azure-portal
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: e69542ec-d10f-4f17-9b7a-2ee441ee7d68
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/10/2016
ms.author: deli
ms.openlocfilehash: 58255c0ad19da65932f8b1d36cb8fef1ff6e651b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-scheduler-in-azure-portal"></a>Aan de slag met Azure Scheduler in Azure-portal
Het is gemakkelijk toocreate geplande taken in Azure Scheduler. In deze zelfstudie leert u hoe toocreate een taak. U komt ook te weten hoe de controle- en beheerfuncties van Scheduler werken.

## <a name="create-a-job"></a>Een taak maken
1. Aanmelden te[Azure-portal](https://portal.azure.com/).  
2. Klik op **+ nieuw** > type *Scheduler* in het zoekvak Hallo > Selecteer **Scheduler** in resultaten > Klik op **maken**.
   
    ![][marketplace-create]
3. We gaan een taak maken waarbij we eenvoudig http://www.microsoft.com/ bestoken met een GET-aanvraag. In Hallo **Scheduler-taak** scherm, voert u Hallo volgende informatie:
   
   1. **Naam:** `getmicrosoft`  
   2. **Abonnement:** uw Azure-abonnement   
   3. **Taakverzameling:** selecteer een bestaande taakverzameling of klik op **Nieuw** > typ een naam.
4. Vervolgens gaat u naar **bewerkingsinstellingen**, definiëren Hallo volgende waarden:
   
   1. **Actietype:** ` HTTP`  
   2. **Methode:** `GET`  
   3. **URL:** ` http://www.microsoft.com`  
      
      ![][action-settings]
5. Tot slot gaan we een planning definiëren. Hallo-taak kan worden gedefinieerd als een eenmalige taak, maar we kiezen een terugkerende planning:
   
   1. **Terugkeerpatroon**:`Recurring`
   2. **Start**: de datum van vandaag
   3. **Herhaald elke**:`12 Hours`
   4. **Beëindigen op**: twee dagen na de huidige datum  
      
      ![][recurrence-schedule]
6. Klik op **Maken**.

## <a name="manage-and-monitor-jobs"></a>Taken beheren en controleren
Zodra een taak is gemaakt, wordt deze weergegeven in Hallo belangrijkste Azure-dashboard. Klik op Hallo taak en een nieuw venster geopend met Hallo volgende tabbladen:

1. Eigenschappen  
2. Actie-instellingen  
3. Planning  
4. Geschiedenis
5. Gebruikers
   
   ![][job-overview]

### <a name="properties"></a>Eigenschappen
Deze alleen-lezen eigenschappen beschrijven Hallo management metagegevens voor Hallo Scheduler-taak.

   ![][job-properties]

### <a name="action-settings"></a>Actie-instellingen
Te klikken op een taak in Hallo **taken** scherm kunt u tooconfigure die taak. Hiermee kunt u geavanceerde instellingen configureren, als deze niet is geconfigureerd in Hallo wizard Snelle invoer.

Voor alle actietypen kunt wijzigen u beleid voor opnieuw proberen Hallo en Hallo foutactie.

Voor HTTP en HTTPS taak actietypen kunt wijzigen u Hallo methode tooany HTTP-term wordt toegestaan. U kunt ook toevoegen, verwijderen of wijzigen Hallo koptekst en elementaire verificatiegegevens.

Voor actietypen opslagwachtrij wijzigen u Hallo opslagaccount, wachtrijnaam, SAS-token en hoofdtekst.

Voor service bus-actietypen kunt wijzigen u Hallo naamruimte, onderwerp/wachtrijpad, verificatie-instellingen, transporttype, berichteigenschappen en hoofdtekst van het bericht.

   ![][job-action-settings]

### <a name="schedule"></a>Planning
Hiermee kunt u Hallo schema opnieuw configureren, indien gewenst toochange Hallo planning die u hebt gemaakt in Hallo wizard Snelle invoer.

Dit is een kans toobuild [complexe schema's en geavanceerde terugkeerpatroon in uw taak](scheduler-advanced-complexity.md)

Hallo begindatum kunnen worden gewijzigd en de tijd, terugkerende planning en Hallo datum en tijd (als Hallo job wordt herhaald.)

   ![][job-schedule]

### <a name="history"></a>Geschiedenis
Hallo **geschiedenis** tabblad geselecteerde metrische gegevens voor het uitvoeren van elke taak in Hallo-systeem voor de geselecteerde taak Hallo weergegeven. Deze metrische gegevens bevatten met betrekking tot het Hallo-status van uw Scheduler realtime-waarden:

1. Status  
2. Details  
3. Nieuwe pogingen
4. Terugkeerpatroon: 1e, 2e, 3e enzovoorts.
5. Starttijd van de uitvoering  
6. Eindtijd van de uitvoering
   
   ![][job-history]

U kunt klikken op een tooview uitvoeren de **Geschiedenisdetails**, inclusief Hallo volledige antwoord voor elke uitvoering. Dit dialoogvenster kunt u ook toocopy Hallo antwoord toohello Klembord.

   ![][job-history-details]

### <a name="users"></a>Gebruikers
Met op rollen gebaseerd toegangsbeheer (RBAC) van Azure beschikt u over geavanceerd toegangsbeheer voor Azure Scheduler. hoe toouse Hallo tabblad gebruikers te verwijzen toolearn[rollen gebaseerd toegangsbeheer](../active-directory/role-based-access-control-configure.md)

## <a name="see-also"></a>Zie ook
 [Wat is Scheduler?](scheduler-intro.md)

 [Scheduler-concepten en terminologie entiteitenhiërarchie](scheduler-concepts-terms.md)

 [Plannen en facturering in Azure Scheduler](scheduler-plans-billing.md)

 [Hoe plant u toobuild complexe en geavanceerde terugkeerpatronen met Azure Scheduler](scheduler-advanced-complexity.md)

 [Naslaginformatie over de REST-API van Scheduler](https://msdn.microsoft.com/library/mt629143)

 [Naslaginformatie over Scheduler PowerShell-cmdlets](scheduler-powershell-reference.md)

 [Hoge beschikbaarheid en betrouwbaarheid Scheduler](scheduler-high-availability-reliability.md)

 [Limieten, standaardwaarden en foutcodes van Scheduler](scheduler-limits-defaults-errors.md)

 [Scheduler uitgaande verificatie](scheduler-outbound-authentication.md)

[marketplace-create]: ./media/scheduler-get-started-portal/scheduler-v2-portal-marketplace-create.png
[action-settings]: ./media/scheduler-get-started-portal/scheduler-v2-portal-action-settings.png
[recurrence-schedule]: ./media/scheduler-get-started-portal/scheduler-v2-portal-recurrence-schedule.png
[job-properties]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-properties.png
[job-overview]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-overview-1.png
[job-action-settings]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-action-settings.png
[job-schedule]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-schedule.png
[job-history]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-history.png
[job-history-details]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-history-details.png


[1]: ./media/scheduler-get-started-portal/scheduler-get-started-portal001.png
[2]: ./media/scheduler-get-started-portal/scheduler-get-started-portal002.png
[3]: ./media/scheduler-get-started-portal/scheduler-get-started-portal003.png
[4]: ./media/scheduler-get-started-portal/scheduler-get-started-portal004.png
[5]: ./media/scheduler-get-started-portal/scheduler-get-started-portal005.png
[6]: ./media/scheduler-get-started-portal/scheduler-get-started-portal006.png
[7]: ./media/scheduler-get-started-portal/scheduler-get-started-portal007.png
[8]: ./media/scheduler-get-started-portal/scheduler-get-started-portal008.png
[9]: ./media/scheduler-get-started-portal/scheduler-get-started-portal009.png
[10]: ./media/scheduler-get-started-portal/scheduler-get-started-portal010.png
[11]: ./media/scheduler-get-started-portal/scheduler-get-started-portal011.png
[12]: ./media/scheduler-get-started-portal/scheduler-get-started-portal012.png
[13]: ./media/scheduler-get-started-portal/scheduler-get-started-portal013.png
[14]: ./media/scheduler-get-started-portal/scheduler-get-started-portal014.png
[15]: ./media/scheduler-get-started-portal/scheduler-get-started-portal015.png
