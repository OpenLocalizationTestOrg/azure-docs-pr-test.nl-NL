---
title: aaaTasks toegestaan in verschillende statussen of statussen in BizTalk Services | Microsoft Docs
description: 'Hallo acties/operations toegestaan in andere MABS status: stoppen, starten, opnieuw starten, onderbreken, hervatten, verwijderen, schalen, configuratie en back-ups maken van bijwerken'
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: aea738f3-ec76-4099-a41b-e17fea9e252f
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/08/2016
ms.author: mandia
ms.openlocfilehash: 643307ba6fa9b05c82b867912feab249c42b65dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-you-can-and-cant-do-using-hello-biztalk-service-state"></a>Wat u wel en niet met behulp van Hallo BizTalk Service-status

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Afhankelijk van de huidige status Hallo Hallo BizTalk service zijn er bewerkingen die u wel of niet uitvoeren op Hallo BizTalk service.

Bijvoorbeeld, inrichten u een nieuwe BizTalk-service in de klassieke Azure-portal Hallo. Wanneer het is voltooid, Hallo BizTalk-service is in `active` staat. Hallo-actieve status heeft, kunt u stoppen, onderbreken en Hallo BizTalk service verwijderen. Als u Hallo BizTalk service, stopt en stop mislukt en Hallo BizTalk service tooa gaat `StopFailed` status. In Hallo `StopFailed` staat, kunt u Hallo BizTalk-service opnieuw starten. Hallo volgende fout treedt op als u een bewerking die niet zijn toegestaan, zoals hervatten:

`Operation not allowed`

## <a name="view-hello-possible-states"></a>Weergave Hallo mogelijke statussen

Hallo volgende tabellen Hallo bewerkingen na opvragen of acties die kunnen worden uitgevoerd wanneer Hallo BizTalk Service bevindt zich in een specifieke status. Een ✔ betekent Hallo-bewerking is toegestaan in deze staat. Een lege waarde betekent Hallo-bewerking kan niet worden uitgevoerd in deze staat.

| Servicestatus | Starten | Stoppen | Opnieuw starten | onderbreken | Hervatten | Verwijderen | Schalen | Update <br/> Configuratie | Back-up |
| --- | --- | --- | --- | --- | --- | --- |--- | --- | --- |
| Actief |  | ✔ | ✔ | ✔ |  | ✔ |✔ |✔ |✔ |
| Uitgeschakeld |  |  |  |  |  | ✔ | |  |  | 
| Onderbroken |  |  |  |  | ✔ | ✔ | |  | ✔ |
| Stopped | ✔ |  | ✔ |  |  | ✔ | |  | ✔ |
| Service-Update is mislukt |  |  |  |  |  | ✔ | |  |  | 
| DisableFailed |  |  |  |  |  | ✔ | |  |  | 
| EnableFailed |  |  |  |  |  | ✔ | |  |  | 
| StartFailed <br/> StopFailed <br/> RestartFailed | ✔ | ✔ | ✔ |  |  | ✔ | | ✔ | |
| SuspendedFailed <br/> ResumeFailed|  |  |  | ✔ | ✔ | ✔ | |  |  | 
| CreatedFailed <br/> RestoreFailed |  |  |  |  |  | ✔ | |  |  | 
| ConfigUpdateFailed  |  |  | ✔ |  |  | ✔ | |✔ | |
| ScaleFailed |  |  |  |  |  | ✔ |✔ | |  |  | 



## <a name="see-also"></a>Zie ook
* [Maken van een BizTalk Service met Hallo klassieke Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [Wat u kunt doen op Hallo dashboard, bewaken en schalen tabbladen van BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [U krijgt met Hallo Developer, Basic, Standard en Premium-edities in BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [Hoe tooback ups en het terugzetten van een BizTalk Service](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [Beperking uitgelegd in BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=302282)<br/>
* [Hallo Service Bus- en toegangsbeheer uitgever en de verlener sleutelwaarden voor uw BizTalk Service ophalen](http://go.microsoft.com/fwlink/p/?LinkID=303941)<br/>
* [Hoe gaan gebruiken Azure BizTalk Services SDK Hallo](http://go.microsoft.com/fwlink/p/?LinkID=302335)

