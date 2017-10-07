---
title: aaaOverview van algemene patronen voor automatisch schalen | Microsoft Docs
description: Meer informatie over dat sommige van de algemene patronen tooauto Hallo uw resource schalen in Azure.
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: ancav
ms.openlocfilehash: fc5bd97852e0af01aa32940c99721ab8e21033ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-common-autoscale-patterns"></a>Overzicht van algemene patronen voor automatisch schalen
Dit artikel worden enkele van de algemene patronen tooscale Hallo uw Azure-resource.

Azure Monitor automatisch schalen geldt alleen tooVirtual Machine Scale Sets (VMSS), cloudservices, app-serviceabonnementen en app service-omgevingen. 

# <a name="lets-get-started"></a>Hiermee kunnen aan de slag

In dit artikel wordt ervan uitgegaan dat u bekend met automatisch schalen bent. U kunt [ophalen gestart hier tooscale uw resource][1]. Hallo Hieronder volgen enkele Hallo algemene scale patronen.

## <a name="scale-based-on-cpu"></a>Schalen op basis van CPU

U hebt een web-app (VMSS/cloud service rol) en 

- Gewenste tooscale out/schaal in op basis van de CPU.
- Bovendien wilt u tooensure er is een minimum aantal exemplaren. 
- Bovendien wilt u tooensure die u instelt dat een maximumlimiet toohello aantal exemplaren die om te kunnen worden geschaald.

![Schalen op basis van CPU][2]

## <a name="scale-differently-on-weekdays-vs-weekends"></a>Anders weekdagen tegenover tijdens het weekend schalen

U hebt een web-app (VMSS/cloud service rol) en

- Op het gewenste 3 exemplaren standaard (weekdagen)
- U geen verkeer verwacht tijdens het weekend en daarom het gewenste tooscale omlaag too1 exemplaar in het weekend.

![Anders weekdagen tegenover tijdens het weekend schalen][3]

## <a name="scale-differently-during-holidays"></a>Anders tijdens de feestdagen schalen

U hebt een web-app (VMSS/cloud service rol) en 

- Gewenste tooscale omhoog/omlaag op basis van CPU-gebruik standaard
- Echter, tijdens de feestdagen (of specifieke dagen die belangrijk voor uw bedrijf zijn) u wilt toooverride Hallo standaardwaarden en meer capaciteit hebben tot uw beschikking staan.

![Anders op feestdagen schaal][4]

## <a name="scale-based-on-custom-metric"></a>Schalen op basis van aangepaste metrische gegevens

U hebt een webfront-end en een API-laag die met Hallo back-end communiceert. 

- Gewenste tooscale Hallo API laag op basis van aangepaste gebeurtenissen in de front-end hello (voorbeeld: U wilt dat uw afrekenen op basis van het aantal items dat in winkelwagen Hallo Hallo tooscale)

![Schalen op basis van aangepaste metrische gegevens][5]

<!--Reference-->
[1]: ./monitoring-autoscale-get-started.md
[2]: ./media/monitoring-autoscale-common-scale-patterns/scale-based-on-cpu.png
[3]: ./media/monitoring-autoscale-common-scale-patterns/weekday-weekend-scale.png
[4]: ./media/monitoring-autoscale-common-scale-patterns/holidays-scale.png
[5]: ./media/monitoring-autoscale-common-scale-patterns/custom-metric-scale.png