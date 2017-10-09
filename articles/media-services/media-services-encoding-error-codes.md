---
title: aaaAzure Media Services-codering foutcodes | Microsoft Docs
description: In dit onderwerp worden de foutcodes die kunnen worden geretourneerd voor het geval is een fout opgetreden tijdens de uitvoering van de taak codering Hallo...
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ce4e939f-5aee-41f9-859d-e4429815e9f2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: b69b6abee797c40c9b8b8f23bf2398273c170e7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="encoding-error-codes"></a>Foutcodes voor codering

Hallo bevat volgende tabel de foutcodes die kunnen worden geretourneerd voor het geval is een fout opgetreden tijdens de uitvoering van de taak codering Hallo.  Foutdetails tooget in uw code .NET gebruiken Hallo [ErrorDetails](http://msdn.microsoft.com/library/microsoft.windowsazure.mediaservices.client.errordetail.aspx) klasse. Foutdetails tooget in uw code REST gebruiken Hallo [ErrorDetail](https://msdn.microsoft.com/library/jj853026.aspx) REST-API.

| ErrorDetail.Code | Mogelijke oorzaken voor fout |
| --- | --- |
| Onbekend |Onbekende fout tijdens het Hallo-taak uitvoeren |
| ErrorDownloadingInputAssetMalformedContent |Categorie van fouten die betrekking heeft op fouten bij het downloaden van de invoer asset zoals namen van de beschadigde bestanden, nul lengte bestanden, onjuist opgemaakt enzovoort. |
| ErrorDownloadingInputAssetServiceFailure |De categorie van fouten die betrekking heeft op problemen op Hallo servicezijde - voorbeeld netwerk of opslag fouten tijdens het downloaden. |
| ErrorParsingConfiguration |Categorie van fouten waar de taak <see cref="MediaTask.PrivateData"/> (configuratie) is niet geldig, bijvoorbeeld Hallo configuratie is niet een geldig systeem voorinstelling of bevat ongeldige XML. |
| ErrorExecutingTaskMalformedContent |De categorie van fouten tijdens het Hallo-uitvoering van Hallo-taak als er problemen binnen Hallo invoer mediabestanden fout veroorzaken. |
| ErrorExecutingTaskUnsupportedFormat |Categorie van fouten waar Mediaprocessor Hallo Hallo-bestanden opgegeven kan niet worden verwerkt - media-indeling niet ondersteund of komt niet overeen met de Hallo configuratie. Bijvoorbeeld, probeert tooproduce alleen audio-uitvoer van een activum met alleen video |
| ErrorProcessingTask |Categorie van andere fouten die Hallo Mediaprocessor aangetroffen tijdens het verwerken van Hallo van Hallo-taak die niet-verwante toocontent zijn. |
| ErrorUploadingOutputAsset |Categorie van fouten tijdens het uploaden van de uitvoerasset Hallo |
| ErrorCancelingTask |Categorie van fouten toocover fouten tijdens een poging de toocancel Hallo taak |
| TransientError |Categorie van fouten toocover problemen van voorbijgaande aard (bv. tijdelijke netwerkproblemen met Azure Storage) |

tooget hulp van Hallo **Media Services** team, open een [ondersteunen ticket](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).

## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a>Verwante artikelen:
* [Geavanceerde codering taken uitvoeren met Media Encoder Standard standaardinstellingen aanpassen](media-services-custom-mes-presets-with-dotnet.md)
* [Quota's en beperkingen](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
