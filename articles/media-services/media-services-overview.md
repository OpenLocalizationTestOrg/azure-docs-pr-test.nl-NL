---
title: overzicht van de Media Services aaaAzure | Microsoft Docs
description: Dit onderwerp bevat een overzicht van Azure Media Services
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7a5e9723-c379-446b-b4d6-d0e41bd7d31f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/04/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 81f9f4d9ff75effea30c10fd09449e9d2025f377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-overview"></a>Overzicht van Azure Media Services 

Microsoft Azure Media Services is een uitbreidbaar cloudplatform waarmee ontwikkelaars toobuild schaalbare media beheer- en toepassingen. Media Services is gebaseerd op de REST-API's waarmee u toosecurely uploaden, opslaan, coderen en video of audio-inhoud van het pakket voor zowel op aanvraag en live streaming levering toovarious clients (bijvoorbeeld TV, PC en mobiele apparaten).

U kunt end-to-end-werkstromen volledig met Media Services bouwen. U kunt ook toouse onderdelen van derden voor sommige onderdelen van uw werkstroom. U kunt bijvoorbeeld coderen met een coderingsprogramma van een derde partij. Vervolgens kunt u uploaden, beveiligen, verpakken en leveren met Media Services.

U kunt kiezen toostream uw live-inhoud of inhoud op aanvraag leveren. Hallo onderwerp bevat ook koppelingen tooother relevante onderwerpen.

## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
U kunt hier de AMS-leertrajecten bekijken:

* [Werkstroom voor AMS Live Streaming](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-live/)
* [Werkstroom voor AMS On-Demand Streaming](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-on-demand/)

## <a name="prerequisites"></a>Vereisten

toostart met Azure Media Services, moet u de volgende Hallo hebben:

* Een Azure-account. Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken. Zie [Gratis proefversie van Azure](https://azure.microsoft.com) voor meer informatie.
* Een Azure Media Services-account. Zie [Een account maken](media-services-portal-create-account.md) voor meer informatie.
* (Optioneel) Instellen van de ontwikkelomgeving. Kies .NET of REST API voor uw ontwikkelomgeving. Zie [De omgeving instellen](media-services-dotnet-how-to-use.md) voor meer informatie.

    Leer ook hoe te[verbinding maken via een programma tooAMS API](media-services-use-aad-auth-to-access-ams-api.md).
* Een streaming-eindpunt (Standard of Premium) in de status Gestart.  Zie [Managing streaming endpoints](media-services-portal-manage-streaming-endpoints.md) (Streaming-eindpunten beheren) voor meer informatie.

## <a name="sdks-and-tools"></a>SDK's en hulpprogramma's

toobuild Media Services-oplossingen, u kunt gebruiken:

* [Media Services REST API](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference)
* Een van de Hallo beschikbare client-SDK's:
    * [Azure Media Services SDK voor .NET](https://github.com/Azure/azure-sdk-for-media-services)
    * [Azure SDK voor Java](https://github.com/Azure/azure-sdk-for-java)
    * [Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php)
    * [Azure Media Services voor Node.js](https://github.com/michelle-becker/node-ams-sdk/blob/master/lib/request.js) (Dit is een niet-Microsoft-versie van een Node.js SDK. Wordt onderhouden door een community en momenteel geen een 100% dekking voor AMS APIs Hallo).
* Bestaande hulpprogramma's:
    * [Azure Portal](https://portal.azure.com/)
    * [Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (Azure Media Services Explorer (AMSE) is een Winforms-/C#-toepassing voor Windows)

## <a name="concepts-and-overview"></a>Concepten en overzicht
Zie [Concepten](media-services-concepts.md) voor Azure Media Services-concepten.

Zie voor een hoe-tooseries waarin u kennis kunt tooall Hallo hoofdonderdelen van Azure Media Services, [Azure Media Services stapsgewijze zelfstudies](https://docs.com/fukushima-shigeyuki/3439/english-azure-media-services-step-by-step-series). Deze reeks biedt een goed overzicht van de concepten en maakt gebruik van Hallo AMSE-hulpprogramma toodemonstrate AMS taken. Het AMSE-hulpprogramma is een Windows-hulpprogramma. Dit hulpprogramma ondersteunt de meeste Hallo-taken die u programmatisch met bereiken kunt [AMS SDK voor .NET](https://github.com/Azure/azure-sdk-for-media-services), [Azure SDK voor Java](https://github.com/Azure/azure-sdk-for-java), of [Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php).

## <a name="supported-scenarios-and-availability-of-media-services-across-data-centers"></a>Ondersteunde scenario's en de beschikbaarheid van Media Services in datacenters

Zie voor gedetailleerde informatie [Scenarios and availability of Media Services features across datacenters](scenarios-and-availability.md) (Scenario's en beschikbaarheid van Media Services-functies via datacenters).

## <a name="service-level-agreement-sla"></a>Service Level Agreement (SLA)

* Voor Media Services-codering wordt een beschikbaarheid van 99,9% voor REST API-transacties gegarandeerd.
* Wanneer er een Standard- of Premium-streaming-eindpunt is gekocht, worden service-aanvragen voor streaming beantwoord met een beschikbaarheidsgarantie van 99,9% voor bestaande media-inhoud.
* Voor Livekanalen wordt gegarandeerd dat actieve kanalen extern verbinding heeft minimaal 99,9% van Hallo tijd.
* Voor Content Protection wordt gegarandeerd dat worden vervuld sleutelaanvragen minimaal 99,9% van Hallo tijd.
* Voor de indexeerfunctie wordt we is indexeerfunctie taak aanvragen verwerkt met een gereserveerd codering service eenheid 99,9% van Hallo tijd.

Zie [Microsoft Azure SLA](https://azure.microsoft.com/support/legal/sla/) voor meer informatie.

Zie voor informatie over de beschikbaarheid van datacenters Hallo [Avaiability](scenarios-and-availability.md#availability) sectie.

## <a name="support"></a>Ondersteuning

[Ondersteuning van Azure](https://azure.microsoft.com/support/options/) biedt ondersteuningsopties voor Azure, met inbegrip van Media Services.

## <a name="provide-feedback"></a>Feedback geven

[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
