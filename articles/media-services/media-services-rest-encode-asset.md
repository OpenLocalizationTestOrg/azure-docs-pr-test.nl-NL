---
title: aaaHow tooencode een Azure-asset met behulp van Media Encoder Standard | Microsoft Docs
description: Meer informatie over hoe toouse Media Encoder Standard tooencode media inhoud op Azure Media Services. Codevoorbeelden REST API gebruiken.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 2a7273c6-8a22-4f82-9bfe-4509ff32d4a4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: b766bafded7ee98eda3e6ef149c31d5d8fe406fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencode-an-asset-by-using-media-encoder-standard"></a>Hoe tooencode een asset met behulp van Media Encoder Standard
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-encode-with-media-encoder-standard.md)
> * [REST](media-services-rest-encode-asset.md)
> * [Portal](media-services-portal-encode.md)
>
>

## <a name="overview"></a>Overzicht
toodeliver digitale video via Internet hello, moet u Hallo media comprimeren. Digitale videobestanden groot en mogelijk te groot toodeliver over Hallo Internet of voor uw klanten apparaten toodisplay goed. Codering is Hallo-proces van het comprimeren van video en audio zodat uw klanten het medium kunnen bekijken.

Codering taken zijn een van de meest voorkomende verwerkingen Hallo in Azure Media Services. U maakt codering taken tooconvert media-bestanden vanuit een codering tooanother. Wanneer u codeert, kunt u Hallo Media Services ingebouwde codering (Media Encoder Standard). U kunt ook een encoder geleverd door een partner Media Services gebruiken. Coderingsprogramma's van derden zijn beschikbaar via hello Azure Marketplace. U kunt details op Hallo van coderingstaken met behulp van vooraf ingestelde tekenreeksen die zijn gedefinieerd voor het coderingsprogramma of met behulp van vooraf ingestelde configuratiebestanden opgeven. toosee hello typen standaardinstellingen die beschikbaar zijn, Zie [taak standaardinstellingen voor Media Encoder Standard](http://msdn.microsoft.com/library/mt269960).

Elke taak kan een of meer taken, afhankelijk van Hallo type verwerken die u wilt dat tooaccomplish. U kunt via Hallo REST-API, taken en hun bijbehorende taken maken op twee manieren:

* Taken kunnen worden gedefinieerd in line via Hallo taken navigatie-eigenschap op taak entiteiten.
* Gebruik de OData-batch-verwerking.

Het is raadzaam dat u altijd de bronbestanden te in een adaptive bitrate MP4-set coderen, en vervolgens Hallo set toohello gewenste indeling te met behulp van converteren [dynamische pakketten](media-services-dynamic-packaging-overview.md).

Als uw uitvoerasset opslag versleuteld is, moet u Hallo-leveringsbeleid voor Assets configureren. Zie voor meer informatie [leveringsbeleid voor Assets configureren](media-services-rest-configure-asset-delivery-policy.md).

## <a name="considerations"></a>Overwegingen

Bij het openen van entiteiten in Media Services, moet u specifieke header-velden en waarden instellen in uw HTTP-aanvragen. Zie voor meer informatie [Setup voor het ontwikkelen van Media Services REST API](media-services-rest-how-to-use.md).

Voordat u verwijst naar de media processors, moet u controleren of hebt u Hallo juiste media processor-ID. Zie voor meer informatie [mediaprocessoren ophalen](media-services-rest-get-media-processor.md).

## <a name="connect-toomedia-services"></a>Verbinding maken met tooMedia Services

Voor informatie over hoe tooconnect toohello AMS API, Zie [toegang hello Azure Media Services-API met Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md). 

>[!NOTE]
>Nadat de verbinding tot stand toohttps://media.windows.net, ontvangt u een 301 omleiding opgeven van een andere URI van de Media Services. U moet de volgende aanroepen toohello ervoor nieuwe URI.

## <a name="create-a-job-with-a-single-encoding-task"></a>Een taak maken met een enkele taak voor codering
> [!NOTE]
> Wanneer u met Hallo REST API voor Media Services werkt, letten hello volgende:
>
> Bij het openen van entiteiten in Media Services, moet u specifieke header-velden en waarden instellen in uw HTTP-aanvragen. Zie voor meer informatie [Setup voor het ontwikkelen van REST-API voor Media Services](media-services-rest-how-to-use.md).
>
> Nadat de verbinding tot stand toohttps://media.windows.net, ontvangt u een 301 omleiding opgeven van een andere URI van de Media Services. U moet de volgende aanroepen toohello ervoor nieuwe URI. Voor informatie over hoe tooconnect toohello AMS API, Zie [toegang hello Azure Media Services-API met Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).
>
> Wanneer met behulp van JSON en geven toouse hello **__metadata** sleutelwoord in Hallo-aanvraag (bijvoorbeeld tooreferences gekoppelde objecten), moet u Hallo instellen **accepteren** header te[uitgebreide JSON-indeling ](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/): Accepteren: application/json; odata = verbose.
>
>

Hallo volgende voorbeeld ziet u hoe toocreate en na een taak met één taak ingesteld tooencode video op een specifieke oplossingsstatus en kwaliteit. Wanneer u met Media Encoder Standard codeert, kunt u taak configuratie standaardinstellingen opgegeven [hier](http://msdn.microsoft.com/library/mt269960).

Aanvraag:

    POST https://media.windows.net/API/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000
    Host: media.windows.net

    {"Name" : "NewTestJob", "InputMediaAssets" : [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3Aaab7f15b-3136-4ddf-9962-e9ecb28fb9d2')"}}],  "Tasks" : [{"Configuration" : "Adaptive Streaming", "MediaProcessorId" : "nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",  "TaskBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"}]}

Antwoord:

    HTTP/1.1 201 Created

    . . .

### <a name="set-hello-output-assets-name"></a>Hallo uitvoerasset naam instellen
Hallo volgende voorbeeld ziet u hoe tooset Hallo assetName kenmerk:

    { "TaskBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"}

## <a name="considerations"></a>Overwegingen
* TaskBody eigenschappen moeten letterlijke XML toodefine Hallo aantal invoer of uitvoer-elementen die worden gebruikt door de taak hello gebruiken. Hallo onderwerp bevat Hallo XML-schemadefinitie voor Hallo XML.
* In Hallo TaskBody definition, elke interne waarde voor <inputAsset> en <outputAsset> JobInputAsset(value) of JobOutputAsset(value) moet worden ingesteld.
* Een taak kan meerdere uitvoer elementen hebben. Één JobOutputAsset(x) kan slechts eenmaal worden gebruikt als uitvoer van een taak in een taak.
* U kunt JobInputAsset of JobOutputAsset opgeven als een invoer actief van een taak.
* Taken moeten vormen geen cyclus.
* Hallo waardeparameter u doorgeeft tooJobInputAsset of JobOutputAsset vertegenwoordigt de indexwaarde Hallo voor een asset. Hallo werkelijke activa zijn gedefinieerd in Hallo InputMediaAssets en OutputMediaAssets navigatie-eigenschappen op Hallo entiteit taakdefinitie.
* Omdat het Media Services is gebouwd op OData v3, afzonderlijke activa in Hallo InputMediaAssets Hallo en OutputMediaAssets navigatie-eigenschap verzamelingen wordt verwezen door een ' __metadata: uri ' naam / waarde-paar.
* InputMediaAssets maps tooone of meer elementen die u hebt gemaakt in Media Services. OutputMediaAssets zijn gemaakt door Hallo-systeem. Ze niet verwijzen naar een bestaande asset.
* OutputMediaAssets kan worden benoemd met Hallo assetName kenmerk. Als dit kenmerk niet aanwezig is, wordt de naam van de Hallo Hallo OutputMediaAsset de waarde van de interne tekst hello Hallo is <outputAsset> -element is en het achtervoegsel Hallo taaknaam waarde of Hallo taak-Id-waarde (in geval van Hallo waar Hallo Name-eigenschap niet is gedefinieerd). Bijvoorbeeld, als u een waarde voor assetName instellen Sample te "Voorbeeld" en vervolgens Hallo OutputMediaAsset de naam van de eigenschap is ingesteld te'." Als u niet een waarde voor assetName instellen, maar de taaknaam Hallo hebt ingesteld zou te 'NewJob' en klik vervolgens Hallo OutputMediaAsset naam wel "JobOutputAsset (waarde) _NewJob."

## <a name="create-a-job-with-chained-tasks"></a>Maken van een taak met gekoppelde taken
In veel scenario's van toepassing wilt ontwikkelaars toocreate een reeks taken te verwerken. U kunt een reeks keten taken maken in Media Services. Elke taak voert de van de verschillende verwerkingsstappen en processors van verschillende media kunt gebruiken. Hallo teruggekoppeld taken kunnen een asset aanlevert uit één taak tooanother, een lineaire reeks taken uitvoeren op Hallo asset. Hallo-taken in een taak wordt uitgevoerd, zijn echter niet vereist toobe in een reeks. Wanneer u een keten taak maakt, Hallo teruggekoppeld **ITask** objecten worden gemaakt in een enkel **IJob** object.

> [!NOTE]
> Er is een limiet van 30 taken per taak. Als u toochain meer dan 30 taken moet, maakt u meer dan één taak toocontain Hallo taken.
>
>

    POST https://media.windows.net/api/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {  
       "Name":"NewTestJob",
       "InputMediaAssets":[  
          {  
             "__metadata":{  
                "uri":"https://testrest.cloudapp.net/api/Assets('nb%3Acid%3AUUID%3A910ffdc1-2e25-4b17-8a42-61ffd4b8914c')"
             }
          }
       ],
       "Tasks":[  
          {  
             "Configuration":"H264 Adaptive Bitrate MP4 Set 720p",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"
          },
          {  
             "Configuration":"H264 Smooth Streaming 720p",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-16\"?><taskBody><inputAsset>JobOutputAsset(0)</inputAsset><outputAsset>JobOutputAsset(1)</outputAsset></taskBody>"
          }
       ]
    }


### <a name="considerations"></a>Overwegingen
tooenable taak koppeling:

* Een taak moet ten minste twee taken hebben.
* Er moet ten minste één taak waarvan invoer Hallo-uitvoer van een andere taak in het Hallo-taak is.

## <a name="use-odata-batch-processing"></a>Verwerking van gebruiken OData-batch
Hallo volgende voorbeeld ziet u hoe toouse OData verwerking toocreate batch een job en taken. Zie voor informatie over batchverwerking, [Open Data Protocol (OData) batchverwerking](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).

    POST https://media.windows.net/api/$batch HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Content-Type: multipart/mixed; boundary=batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e
    Accept: multipart/mixed
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000
    Host: media.windows.net


    --batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e
    Content-Type: multipart/mixed; boundary=changeset_122fb0a4-cd80-4958-820f-346309967e4d

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d
    Content-Type: application/http
    Content-Transfer-Encoding: binary

    POST https://media.windows.net/api/Jobs HTTP/1.1
    Content-ID: 1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {"Name" : "NewTestJob", "InputMediaAssets@odata.bind":["https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A2a22445d-1500-80c6-4b34-f1e5190d33c6')"]}

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d
    Content-Type: application/http
    Content-Transfer-Encoding: binary

    POST https://media.windows.net/api/$1/Tasks HTTP/1.1
    Content-ID: 2
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {  
       "Configuration":"H264 Adaptive Bitrate MP4 Set 720p",
       "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
       "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"Custom output name\">JobOutputAsset(0)</outputAsset></taskBody>"
    }

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d--
    --batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e--



## <a name="create-a-job-by-using-a-jobtemplate"></a>Een taak maken met behulp van een taaksjabloon
Wanneer u meerdere activa verwerken met behulp van een gemeenschappelijke set taken, gebruik die een standaardtaak taaksjabloon toospecify Hallo voorinstellingen of tooset Hallo volgorde van taken.

Hallo volgende voorbeeld ziet u hoe toocreate een taaksjabloon met een TaskTemplate die inline gedefinieerde gegevens. Hallo TaskTemplate maakt gebruik van Media Encoder Standard Hallo als Hallo MediaProcessor tooencode Hallo asset-bestand. Andere MediaProcessors kan echter ook worden gebruikt.

    POST https://media.windows.net/API/JobTemplates HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    Host: media.windows.net


    {"Name" : "NewJobTemplate25", "JobTemplateBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><jobTemplate><taskBody taskTemplateId=\"nb:ttid:UUID:071370A3-E63E-4E81-A099-AD66BCAC3789\"><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody></jobTemplate>", "TaskTemplates" : [{"Id" : "nb:ttid:UUID:071370A3-E63E-4E81-A099-AD66BCAC3789", "Configuration" : "H264 Smooth Streaming 720p", "MediaProcessorId" : "nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56", "Name" : "SampleTaskTemplate2", "NumberofInputAssets" : 1, "NumberofOutputAssets" : 1}] }


> [!NOTE]
> In tegenstelling tot andere entiteiten Media Services, moet u een nieuwe GUID-id definiëren voor elke TaskTemplate en plaats deze in Hallo taskTemplateId en Id-eigenschap in de aanvraagtekst. Hallo inhoud-id-schema moet volgen op Hallo schema beschreven in Azure Media Services-entiteiten identificeren. Bovendien kan niet JobTemplates worden bijgewerkt. In plaats daarvan moet u een nieuw bestand met de bijgewerkte wijzigingen maken.
>
>

Als dit lukt, wordt de Hallo volgende antwoord geretourneerd:

    HTTP/1.1 201 Created

    . . .


Hallo volgende voorbeeld wordt getoond hoe toocreate een taak die verwijst naar een taaksjabloon-Id:

    POST https://media.windows.net/API/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    Host: media.windows.net


    {"Name" : "NewTestJob", "InputMediaAssets" : [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A3f1fe4a2-68f5-4190-9557-cd45beccef92')"}}], "TemplateId" : "nb:jtid:UUID:15e6e5e6-ac85-084e-9dc2-db3645fbf0aa"}


Als dit lukt, wordt de Hallo volgende antwoord geretourneerd:

    HTTP/1.1 201 Created

    . . .



## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>Volgende stappen
Als u weet hoe toocreate een taak tooencode een activum, Zie [hoe toocheck taak uitgevoerd met Media Services](media-services-rest-check-job-progress.md).

## <a name="see-also"></a>Zie ook
[Ophalen van Media-Processors](media-services-rest-get-media-processor.md)
