---
title: hoge beschikbaarheid van Analysis Services aaaAzure | Microsoft Docs
description: Zodat zeker Azure Analysis Services met hoge beschikbaarheid.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 6e09536c5bd7dc7f88f9b662e1a9f42d2b8c969b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="analysis-services-high-availability"></a>Hoge beschikbaarheid van Analysis Services
Dit artikel wordt beschreven zodat zeker hoge beschikbaarheid voor Azure Analysis Services-servers. 


## <a name="assuring-high-availability-during-a-service-disruption"></a>Hoge beschikbaarheid zodat zeker tijdens een service wordt onderbroken
Hoewel dit zelden voorkomt, kan een storing in een Azure-datacenter hebben. Wanneer er een storing optreedt, wordt er een onderbreking van de bedrijven die mogelijk een paar minuten laatste of uur kan duren. Hoge beschikbaarheid wordt vaak bereikt met server redundantie. U kunt met Azure Analysis Services redundantie bereiken door het maken van aanvullende, secundaire servers in een of meer regio's. Bij het maken van redundante servers, tooassure Hallo gegevens en metagegevens op die servers in de synchronisatie is met Hallo-server in een regio die is geworden offline, kunt u:

* Modellen tooredundant servers in andere regio's implementeren. Deze methode moet verwerken van gegevens op uw primaire server en de redundante servers in parallel, zodat alle servers zeker synchroon.

* Back-up databases uit de primaire server en terugzetten op servers met redundante. U kunt bijvoorbeeld elke nacht back-ups tooAzure opslag automatiseren en tooother redundante servers in andere regio's herstellen. 

Als een storing optreedt in de primaire server moet u in beide gevallen Hallo-verbindingsreeksen in rapportageserver clients tooconnect toohello in een andere regionale datacenter wijzigen. Deze wijziging als een laatste toevlucht moet worden beschouwd en alleen als een onherstelbare regionale datacentrum optreedt. Het is waarschijnlijk een datacentrum die als host fungeert voor de primaire server weer online zou komen voordat verbindingen op alle clients kan worden bijgewerkt. 



## <a name="related-information"></a>Gerelateerde informatie
[Back-up en herstel](analysis-services-backup.md)   
[Azure analyseservices beheren](analysis-services-manage.md) 

