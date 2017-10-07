---
title: AAA beheren snelheid en gelijktijdigheid van uw codering met Azure Media Services | Microsoft Docs
description: Dit artikel bevat een kort overzicht van hoe u de snelheid en gelijktijdigheid van uw codering taken/taken met Azure Media Services kunt beheren.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 676313f8-a158-4e3a-a99b-2c29a341ecc9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: juliako
ms.openlocfilehash: da52a6278a3d3b084dbf5a594db37df8447bb944
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
#  <a name="manage-speed-and-concurrency-of-your-encoding"></a>Snelheid en gelijktijdigheid van uw codering beheren

Dit artikel bevat een kort overzicht van hoe u de snelheid en gelijktijdigheid van uw codering taken/taken kunt beheren.

## <a name="overview"></a>Overzicht

In Media Services een **gereserveerde eenheidstype** bepaalt Hallo snelheid waarmee uw media het verwerken van de taken worden verwerkt. U kunt kiezen tussen Hallo volgende gereserveerde eenheidstypen: **S1**, **S2**, of **S3**. Bijvoorbeeld, Hallo dezelfde coderingstaak sneller wordt uitgevoerd wanneer u Hallo **S2** gereserveerde eenheidstype vergelijken toohello **S1** type. Hallo [codering eenheden schalen](media-services-scale-media-processing-overview.md) onderwerp bevat een tabel waarmee u de beslissing nemen bij de keuze tussen verschillende codering snelheid te koppelen.

Bovendien toospecifying Hallo eenheidstype gereserveerd, kunt u tooprovision uw account met opgeven **gereserveerde eenheden**. het aantal ingerichte gereserveerde eenheden Hallo bepaalt Hallo aantal media-taken die tegelijkertijd kunnen worden verwerkt in een opgegeven account. Bijvoorbeeld, als uw account vijf gereserveerde eenheden, heeft en vervolgens vijf media taken wordt gelijktijdig zo lang worden uitgevoerd als er zijn taken toobe verwerkt. de resterende taken Hallo wachttijd in wachtrij Hallo en wordt ophalen opgepikt sequentieel worden verwerkt wanneer een actieve taak is voltooid. Als een account heeft geen geen gereserveerde eenheden die zijn ingericht, zullen vervolgens taken worden opgepikt sequentieel worden verwerkt. In dit geval Hallo wachttijd tussen een taak is voltooid en hello naast een starten is afhankelijk Hallo beschikbaarheid van resources in Hallo-systeem.

Voor gedetailleerde informatie over en voorbeelden die tonen hoe tooscale codering eenheden, Zie [dit](media-services-scale-media-processing-overview.md) onderwerp.

## <a name="next-step"></a>Volgende stap

[Codering schaaleenheden](media-services-scale-media-processing-overview.md)

## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

