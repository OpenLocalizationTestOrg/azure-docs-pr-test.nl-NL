---
title: aaaScale media verwerken door toe te voegen codering eenheden - Azure |  Microsoft Docs
description: Meer informatie over hoe toohow tooadd codering eenheden met .NET
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 33f7625a-966a-4f06-bc09-bccd6e2a42b5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;milangada;
ms.openlocfilehash: b9f71a6487c5d136319a38a1598d60edfaa81b9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-encoding-with-net-sdk"></a>Hoe tooscale codering met .NET SDK
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-scale-media-processing.md)
> * [.NET](media-services-dotnet-encoding-units.md)
> * [REST](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a>Overzicht
> [!IMPORTANT]
> Zorg ervoor dat tooreview hello [overzicht](media-services-scale-media-processing-overview.md) onderwerp tooget meer informatie over het schalen van media onderwerp verwerken.
> 
> 

toochange hello gereserveerde eenheid type en Hallo aantal gereserveerde eenheden met .NET SDK codering Hallo te volgen:

    IEncodingReservedUnit encodingS1ReservedUnit = _context.EncodingReservedUnits.FirstOrDefault();
    encodingS1ReservedUnit.ReservedUnitType = ReservedUnitType.Basic; // Corresponds tooS1
    encodingS1ReservedUnit.Update();
    Console.WriteLine("Reserved Unit Type: {0}", encodingS1ReservedUnit.ReservedUnitType);

    encodingS1ReservedUnit.CurrentReservedUnits = 2;
    encodingS1ReservedUnit.Update();

    Console.WriteLine("Number of reserved units: {0}", encodingS1ReservedUnit.CurrentReservedUnits);

## <a name="opening-a-support-ticket"></a>Een Ondersteuningsticket openen
Standaard elke Media Services-account tooup too25 kunt schalen codering en 5 On Demand gereserveerde Streaming-eenheden. U kunt een hogere limiet aanvragen door een ondersteuningsticket openen.

### <a name="open-a-support-ticket"></a>Een ondersteuningsticket opent
een ondersteuningsticket tooopen Hallo te volgen:

1. Klik op [ondersteuning krijgen](https://manage.windowsazure.com/?getsupport=true). Als u niet bent aangemeld, wordt u na vragen aan gebruiker tooenter worden uw referenties.
2. Selecteer uw abonnement.
3. Selecteer onder ondersteuning voor type 'Technical'.
4. Klik op 'Ticket maken'.
5. Selecteer "Azure Media Services' in de lijst met producten voor Hallo die wordt weergegeven op de volgende pagina Hallo.
6. Selecteer een 'probleemtype' die geschikt is voor uw probleem.
7. Klik op Doorgaan.
8. Volg de instructies op de volgende pagina en Geef details over uw probleem.
9. Klik op verzenden tooopen Hallo ticket.

## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

