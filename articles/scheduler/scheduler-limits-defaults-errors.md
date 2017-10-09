---
title: aaaScheduler limieten en de standaardinstellingen
description: Scheduler-limieten en de standaardinstellingen
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 88f4a3e9-6dbd-4943-8543-f0649d423061
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 6fe0600d3ce3249d5aab1b877369b175316b5437
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-limits-and-defaults"></a>Scheduler-limieten en de standaardinstellingen
## <a name="scheduler-quotas-limits-defaults-and-throttles"></a>Scheduler-quota, limieten, standaardwaarden en vertragingen
[!INCLUDE [scheduler-limits-table](../../includes/scheduler-limits-table.md)]

## <a name="hello-x-ms-request-id-header"></a>x-ms-aanvraag-id Hallo koptekst
Elk verzoek tegen Hallo Scheduler-service retourneert een antwoordheader genaamd**x-ms-aanvraag-id**. Deze koptekst bevat een ondoorzichtige waarde met een unieke identificatie Hallo-aanvraag.

Als een aanvraag consistent is hebt mislukt en u gecontroleerd dat Hallo verzoek goed geformuleerd is, mag u deze waarde tooreport Hallo fout tooMicrosoft. Opnemen in uw rapport Hallo-waarde van de x-ms-aanvraag-id Hallo bij benadering de tijd die Hallo-aanvraag is aangebracht, Hallo-id van het Hallo-abonnement, taakverzameling en/of taak en type bewerking dat verzoek heeft geprobeerd Hallo Hallo.

## <a name="see-also"></a>Zie ook
 [Wat is Scheduler?](scheduler-intro.md)

 [Azure Scheduler-concepten, -terminologie en -entiteitenhiërarchie](scheduler-concepts-terms.md)

 [Aan de slag met behulp van Scheduler in hello Azure-portal](scheduler-get-started-portal.md)

 [Plannen en facturering in Azure Scheduler](scheduler-plans-billing.md)

 [Naslaginformatie over REST API van Azure Scheduler](https://msdn.microsoft.com/library/mt629143)

 [Naslaginformatie over Azure Scheduler PowerShell-cmdlets](scheduler-powershell-reference.md)

 [Hoge beschikbaarheid en betrouwbaarheid van Azure Scheduler](scheduler-high-availability-reliability.md)

 [Azure Scheduler uitgaande verificatie](scheduler-outbound-authentication.md)

