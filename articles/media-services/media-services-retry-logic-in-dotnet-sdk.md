---
title: aaaRetry logica in Hallo Media Services SDK voor .NET | Microsoft Docs
description: Hallo onderwerp overzicht een van Pogingslogica in Hallo Media Services SDK voor .NET.
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 527b61a6-c862-4bd8-bcbc-b9aea1ffdee3
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: juliako
ms.openlocfilehash: 18d0a9d68e55a48bc769fb6ae5711ddba78ed8e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="retry-logic-in-hello-media-services-sdk-for-net"></a>Pogingslogica in Hallo Media Services SDK voor .NET
Als u werkt met Microsoft Azure-services, kunnen tijdelijke fouten optreden. Als een tijdelijke fout in de meeste gevallen optreedt na een paar pogingen hello bewerking is geslaagd. Media Services SDK voor .NET Hallo implementeert Hallo opnieuw logica toohandle tijdelijke fouten die zijn gekoppeld aan de uitzonderingen en fouten die worden veroorzaakt door webaanvragen, uitvoeren van query's opslaan van wijzigingen en opslagbewerkingen.  Standaard wordt Hallo Media Services SDK voor .NET vier pogingen uitgevoerd voordat het opnieuw genereren Hallo uitzondering tooyour toepassing. Hallo-code in uw toepassing moet deze uitzondering vervolgens correct verwerken.  

 Hallo Hier volgt een korte richtlijn webaanvraag, opslag, Query en SaveChanges beleidsregels:  

* Hallo-beleid voor opslag wordt gebruikt voor bewerkingen voor blob-opslag (uploads of downloaden van assetbestanden).  
* Hallo webaanvraag beleid wordt gebruikt voor algemene webaanvragen (bijvoorbeeld voor een verificatie-token ophalen en oplossen van Hallo gebruikers cluster eindpunt).  
* Hallo querybeleid wordt gebruikt voor het uitvoeren van query's entiteiten van REST (bijvoorbeeld mediaContext.Assets.Where(...)).  
* Hallo SaveChanges beleid wordt gebruikt voor het uitvoeren van alles wat gegevens binnen het Hallo-service (bijvoorbeeld het maken van een entiteit bijwerken van een entiteit, een servicefunctie aanroepen voor een bewerking) wordt gewijzigd.  
  
  Dit onderwerp bevat de typen en Pogingslogica foutcodes die worden verwerkt door Hallo Media Services SDK voor .NET.  

## <a name="exception-types"></a>Uitzondering typen
Hello volgende tabel beschrijft de uitzonderingen die Hallo Media Services SDK voor .NET-ingangen of verwerkt niet voor bepaalde bewerkingen, die tijdelijke fouten kunnen veroorzaken.  

| Uitzondering | Webaanvraag | Storage | Query’s uitvoeren | SaveChanges |
| --- | --- | --- | --- | --- |
| WebException<br/>Zie voor meer informatie, Hallo [WebException statuscodes](media-services-retry-logic-in-dotnet-sdk.md#WebExceptionStatus) sectie. |Ja |Ja |Ja |Ja |
| DataServiceClientException<br/> Zie voor meer informatie [HTTP-fout statuscodes](media-services-retry-logic-in-dotnet-sdk.md#HTTPStatusCode). |Nee |Ja |Ja |Ja |
| DataServiceQueryException<br/> Zie voor meer informatie [HTTP-fout statuscodes](media-services-retry-logic-in-dotnet-sdk.md#HTTPStatusCode). |Nee |Ja |Ja |Ja |
| DataServiceRequestException<br/> Zie voor meer informatie [HTTP-fout statuscodes](media-services-retry-logic-in-dotnet-sdk.md#HTTPStatusCode). |Nee |Ja |Ja |Ja |
| DataServiceTransportException |Nee |Nee |Ja |Ja |
| TimeoutException |Ja |Ja |Ja |Nee |
| SocketException |Ja |Ja |Ja |Ja |
| StorageException |Nee |Ja |Nee |Nee |
| IOException |Nee |Ja |Nee |Nee |

### <a name="WebExceptionStatus"></a>Statuscodes WebException
Hallo volgende tabel toont voor welke WebException codes Hallo Pogingslogica is geïmplementeerd. Hallo [WebExceptionStatus](http://msdn.microsoft.com/library/system.net.webexceptionstatus.aspx) opsomming Hallo statuscodes definieert.  

| Status | Webaanvraag | Storage | Query’s uitvoeren | SaveChanges |
| --- | --- | --- | --- | --- |
| ConnectFailure |Ja |Ja |Ja |Ja |
| NameResolutionFailure |Ja |Ja |Ja |Ja |
| ProxyNameResolutionFailure |Ja |Ja |Ja |Ja |
| SendFailure |Ja |Ja |Ja |Ja |
| PipelineFailure |Ja |Ja |Ja |Nee |
| ConnectionClosed |Ja |Ja |Ja |Nee |
| KeepAliveFailure |Ja |Ja |Ja |Nee |
| UnknownError |Ja |Ja |Ja |Nee |
| ReceiveFailure |Ja |Ja |Ja |Nee |
| RequestCanceled |Ja |Ja |Ja |Nee |
| Time-out |Ja |Ja |Ja |Nee |
| Een protocolfout <br/>Hallo opnieuw op een protocolfout wordt bepaald door Hallo HTTP-status code verwerken. Zie voor meer informatie [HTTP-fout statuscodes](media-services-retry-logic-in-dotnet-sdk.md#HTTPStatusCode). |Ja |Ja |Ja |Ja |

### <a name="HTTPStatusCode"></a>Statuscodes voor HTTP-fout
Wanneer bewerkingen query's en SaveChanges throw DataServiceClientException, DataServiceQueryException of DataServiceQueryException, wordt in Hallo eigenschap StatusCode Hallo HTTP-status foutcode geretourneerd.  Hallo volgende tabel ziet u welke foutcodes Hallo Pogingslogica is geïmplementeerd.  

| Status | Webaanvraag | Storage | Query’s uitvoeren | SaveChanges |
| --- | --- | --- | --- | --- |
| 401 |Nee |Ja |Nee |Nee |
| 403 |Nee |Ja<br/>Verwerking van nieuwe pogingen met langer wachten op. |Nee |Nee |
| 408 |Ja |Ja |Ja |Ja |
| 429 |Ja |Ja |Ja |Ja |
| 500 |Ja |Ja |Ja |Nee |
| 502 |Ja |Ja |Ja |Nee |
| 503 |Ja |Ja |Ja |Ja |
| 504 |Ja |Ja |Ja |Nee |

Als u tootake bekijkt hello werkelijke implementatie van Hallo Media Services SDK voor .NET-Pogingslogica wilt, Zie [azure-sdk-voor-media-services](https://github.com/Azure/azure-sdk-for-media-services/tree/dev/src/net/Client/TransientFaultHandling).

## <a name="next-steps"></a>Volgende stappen
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

