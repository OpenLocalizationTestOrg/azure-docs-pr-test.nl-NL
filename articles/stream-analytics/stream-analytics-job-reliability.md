---
title: Vermijd serviceonderbrekingen met Azure Stream Analytics-taken | Microsoft Docs
description: Richtlijnen voor het maken van uw Stream Analytics taken robuuste upgrade.
services: stream-analytics
documentationCenter: 
authors: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 3ac65c93ecb47e93e963dd9869a7af70f73b19c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="guarantee-stream-analytics-job-reliability-during-service-updates"></a>Stream Analytics-taak betrouwbaarheid garanderen tijdens de service-updates

Deel van een volledig beheerde service wordt is Hallo mogelijkheid toointroduce nieuwe service-functionaliteit en verbeteringen in een snelle tempo. Stream Analytics kan hierdoor een service-update implementeert op basis van wekelijkse (of vaker) hebben. Ongeacht hoeveel tests worden uitgevoerd nog er steeds het risico bestaat dat een bestaande, actieve taak is het vanwege toohello introductie van een fout verbroken mogelijk. Voor klanten die kritieke streaming verwerking taken die risico's uitvoeren nodig toobe vermeden. Een mechanisme voor klanten kunt tooreduce dit risico is een Azure  **[gekoppelde regio](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)**  model. 

## <a name="how-do-azure-paired-regions-address-this-concern"></a>Hoe gekoppelde Azure-regio adresseren van dit te voorkomen?

Stream Analytics-taken in de gekoppelde regio's worden bijgewerkt in afzonderlijke batches wordt gegarandeerd. Er is als gevolg hiervan een voldoende tijdsverschil tussen Hallo updates tooidentify potentiële nieuwste fouten en ze herstellen.

_Met uitzondering van centrale India Hallo_ (waarvan gekoppelde regio, Zuid, India geen Stream Analytics aanwezigheid), Hallo-implementatie van een update tooStream Analytics niet op Hallo plaatsvindt dezelfde periode in een set van gekoppelde regio's. Implementaties in meerdere regio's **in Hallo dezelfde groep** optreden **op Hallo hetzelfde moment**.

Hallo-artikel op  **[beschikbaarheid en gekoppelde regio's](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)**  heeft de meest actuele informatie Hallo op welke regio's zijn gekoppeld.

Klanten wordt aangeraden toodeploy identiek taken tooboth gekoppeld regio's. Bovendien tooStream Analytics interne bewakingsmogelijkheden, klanten ook zijn aangeraden toomonitor Hallo taken als **beide** zijn productietaken. Als een einde geïdentificeerde toobe een resultaat van Hallo Stream Analytics-service-update, escaleren op de juiste wijze en downstream consumenten toohello orde taakuitvoer failover. Escalatie toosupport wordt Hallo gekoppelde regio te voorkomen dat wordt beïnvloed door de nieuwe implementatie Hallo en Hallo integriteit van Hallo gekoppeld taken beheren.
