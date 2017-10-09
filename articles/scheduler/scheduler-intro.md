---
title: aaaWhat is Azure Scheduler? | Microsoft Docs
description: Azure Scheduler kunt u toodeclaratively beschrijven acties toorun in Hallo cloud. En vervolgens worden deze acties automatisch gepland en uitgevoerd.
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 52aa6ae1-4c3d-43fb-81b0-6792c84bcfae
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 062e25ae473510264dc0038198c05e7ac1e86210
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-scheduler"></a>Wat is Azure Scheduler?
Azure Scheduler kunt u toodeclaratively beschrijven acties toorun in Hallo cloud. En vervolgens worden deze acties automatisch gepland en uitgevoerd.  Scheduler wordt dit met behulp van [hello Azure-portal](scheduler-get-started-portal.md), code, [REST-API](https://msdn.microsoft.com/library/mt629143.aspx), of Azure PowerShell.

Scheduler maakt, onderhoudt en roept gepland werk aan.  Scheduler host geen workloads en voert geen programmacode uit. Scheduler *roept* programmacode aan die elders wordt gehost, in Azure, on-premises of bij een andere provider. Dit aanroepen gebeurt via HTTP, HTTPS, een opslagwachtrij, een Service Bus-wachtrij of een Service Bus-onderwerp.

Scheduler planningen [taken](scheduler-concepts-terms.md), resultaten van taken in het verleden bijgehouden dat een bekijken kunt en deterministisch en betrouwbaar planningen werkbelastingen toobe uitgevoerd. Azure WebJobs (onderdeel van de functie van de Hallo Web Apps in Azure App Service) en andere mogelijkheden van Azure Scheduler gebruik van Scheduler op Hallo achtergrond. Hallo [Scheduler REST API](https://msdn.microsoft.com/library/mt629143.aspx) helpt bij het beheer Hallo communicatie voor deze acties. Als zodanig ondersteunt Scheduler met gemak [complexe schema's en geavanceerde terugkeerpatronen](scheduler-advanced-complexity.md).

Er zijn verschillende scenario's die zich goed toohello gebruik van Scheduler lenen. Bijvoorbeeld:

* *Terugkerende acties van toepassingen*: periodiek verzamelen van gegevens van Twitter in een feed.
* *Dagelijks onderhoud*: het dagelijks verwijderen van logboeken, het uitvoeren van back-ups en overige onderhoudstaken. Een beheerder kan bijvoorbeeld tooback Hallo updatabase kiezen om 1:00 uur dagelijks op Hallo volgende negen maanden.

Scheduler kunt u toocreate, bijwerken, verwijderen, weergeven en beheren van taken en [taakverzamelingen](scheduler-concepts-terms.md) programmatisch met behulp van scripts en in Hallo-portal.

## <a name="see-also"></a>Zie ook
 [Azure Scheduler-concepten, -terminologie en -entiteitenhiërarchie](scheduler-concepts-terms.md)

 [Aan de slag met behulp van Scheduler in hello Azure-portal](scheduler-get-started-portal.md)

 [Plannen en facturering in Azure Scheduler](scheduler-plans-billing.md)

 [Hoe plant u toobuild complexe en geavanceerde terugkeerpatronen met Azure Scheduler](scheduler-advanced-complexity.md)

 [Naslaginformatie over REST API van Azure Scheduler](https://msdn.microsoft.com/library/mt629143)

 [Naslaginformatie over Azure Scheduler PowerShell-cmdlets](scheduler-powershell-reference.md)

 [Hoge beschikbaarheid en betrouwbaarheid van Azure Scheduler](scheduler-high-availability-reliability.md)

 [Azure Scheduler-limieten, standaardwaarden en foutcodes](scheduler-limits-defaults-errors.md)

 [Azure Scheduler uitgaande verificatie](scheduler-outbound-authentication.md)

