---
title: aaaHow toouse Blitline voor de verwerking van de installatiekopie - Azure-functie handleiding
description: Meer informatie over hoe toouse hello Blitline service tooprocess afbeeldingen in een Azure-toepassing.
services: 
documentationcenter: .net
author: blitline-dev
manager: jason@blitline.com
editor: jason@blitline.com
ms.assetid: 6c711248-0e52-4895-ba9e-8395628de924
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/09/2014
ms.author: support@blitline.com
ms.openlocfilehash: 328fd177e25f45f29f8ad8e142d02b46017a858e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blitline-with-azure-and-azure-storage"></a>Hoe toouse Blitline met Azure en Azure Storage
Deze handleiding wordt uitgelegd hoe tooaccess Blitline services en hoe toosubmit tooBlitline taken.

## <a name="what-is-blitline"></a>Wat is Blitline?
Blitline is een cloud-gebaseerde verwerking van afbeeldingen enterprise niveau beeldverwerking een fractie van Hallo prijs toobuild zou kosten biedt deze zelf.

Hallo feit is dat beeldverwerking is nog steeds opnieuw, meestal opnieuw opgebouwd uit Hallo ontwerp voor elke website. We realiseren dit omdat we hebt gebouwd ze een miljoen keer te. Één dag die we besloten mogelijk is het tijd doen we zojuist dit voor iedereen. We weten hoe toodo het toodo snel en efficiënt en sla Iedereen werkt deze in Hallo tussentijd.

Zie voor meer informatie [http://www.blitline.com](http://www.blitline.com).

## <a name="what-blitline-is-not"></a>Wat Blitline is niet...
tooclarify wat Blitline is handig voor het is vaak eenvoudiger tooidentify wat Blitline geen voordat u verder gaat.

* Blitline heeft geen HTML-widgets tooupload afbeeldingen. Openbaar of met beperkte machtigingen beschikbaar voor Blitline tooreach, moet u installatiekopieën beschikbaar hebben.
* Blitline geen live installatiekopie verwerken, zoals Aviary.com
* Blitline uploaden van afbeeldingen niet accepteert, kan niet u uw installatiekopieën tooBlitline rechtstreeks push. U moet push ze tooAzure opslag of andere Blitline ondersteunt plaatsen en vervolgens instrueren Blitline waar toogo erbij.
* Blitline massively parallel en niet kan synchrone verwerking. Wat betekent dat u moet Geef ons een postback_url en kunnen we u wanneer we klaar bent verwerking.

## <a name="create-a-blitline-account"></a>Een Blitline-account maken
[!INCLUDE [blitline-signup](../includes/blitline-signup.md)]

## <a name="how-toocreate-a-blitline-job"></a>Hoe een taak Blitline toocreate
Blitline maakt gebruik van JSON toodefine Hallo-acties die u wilt dat tootake op een installatiekopie. Deze JSON bestaat uit een paar eenvoudige velden.

de eenvoudigste voorbeeld Hallo is als volgt:

        json : '{
       "application_id": "MY_APP_ID",
       "src" : "http://cdn.blitline.com/filters/boys.jpeg",
       "functions" : [ {
           "name": "resize_to_fit",
           "params" : { "width": 240, "height": 140 },
           "save" : { "image_identifier" : "external_sample_1" }
       } ]
    }'

Hier hebben we JSON die een installatiekopie van een 'src' duurt "... boys.jpeg" en vervolgens de grootte van deze installatiekopie too240x140.

Hallo toepassings-ID is iets vindt u in uw **VERBINDINGSGEGEVENS** of **beheren** tabblad op Azure. Het is uw geheime id waarmee u toorun taken op Blitline.

Hallo 'opgeslagen'-parameter identificeert informatie over waar u tooput Hallo installatiekopie nadat we hebben het verwerkt. In dit geval trivial nog niet hebben we een gedefinieerd. Als er geen vestiging is gedefinieerd Blitline wordt opslaan lokaal (en tijdelijk) op de locatie van een unieke cloud. U zult kunnen tooget die locatie Hallo JSON door Blitline geretourneerd wanneer u Hallo Blitline aanbrengt. Hallo 'installatiekopie' id is vereist en tooyou wordt geretourneerd wanneer tooidentify deze name installatiekopie opgeslagen.

U vindt meer informatie over Hallo *functies* we hier ondersteunen: <http://www.blitline.com/docs/functions>

Ook vindt u documentatie over Hallo hier de opties voor de taak: <http://www.blitline.com/docs/api>

Zodra u hebt uw JSON toodo hoeft u **POST** deze te`http://api.blitline.com/job`

U ontvangt JSON terug die ziet er ongeveer als volgt uit:

    {
     "results":
         {"images":
            [{
              "image_identifier":"external_sample_1",
              "s3_url":"https://s3.amazonaws.com/dev.blitline/2011110722/YOUR_APP_ID/CK3f0xBF_2bV6wf7gEZE8w.jpg"
            }],
          "job_id":"4eb8c9f72a50ee2a9900002f"
         }
    }


Weet u dat Blitline heeft uw aanvraag ontvangen, deze in een wachtrij voor verwerking geplaatst is en wanneer deze is voltooid Hallo afbeelding zijn beschikbaar op: **https://s3.amazonaws.com/dev.blitline/2011110722/YOUR\_APP\_ID /CK3f0xBF_2bV6wf7gEZE8w.jpg**

## <a name="how-toosave-an-image-tooyour-azure-storage-account"></a>Hoe toosave een installatiekopie tooyour Azure Storage-account
Als u een Azure Storage-account hebt, kunt u eenvoudig Blitline push Hallo verwerkt afbeeldingen laten naar uw Azure container. Door het toevoegen van een 'azure_destination' definieert u Hallo locatie en machtigingen voor Blitline toopush aan.

Hier volgt een voorbeeld:

    job : '{
      "application_id": "YOUR_APP_ID",
      "src" : "http://www.google.com/logos/2011/houdini11-hp.jpg",
         "functions" : [{
         "name": "blur",
         "save" : {
             "image_identifier" : "YOUR_IMAGE_IDENTIFIER",
             "azure_destination" : {
                 "account_name" : "YOUR_AZURE_CONTAINER_NAME",
                 "shared_access_signature" : "SAS_THAT_GIVES_BLITLINE_PERMISSION_TO_WRITE_THIS_OBJECT_TO_CONTAINER",
               }
           }
         }]
       }'


Door in te vullen Hallo CAPITALIZED waarden door uw eigen, dient u deze JSON-toohttp://api.blitline.com/job en hello 'src' installatiekopie wordt verwerkt met een vervagingsfilter en vervolgens gepusht tooyou Azure bestemming.

### <a name="please-note"></a>Opmerking:
Hallo SAS moet Hallo gehele SAS-url, inclusief Hallo-bestandsnaam van het doelbestand Hallo bevatten.

Voorbeeld:

    http://blitline.blob.core.windows.net/sample/image.jpg?sr=b&sv=2012-02-12&st=2013-04-12T03%3A18%3A30Z&se=2013-04-12T04%3A18%3A30Z&sp=w&sig=Bte2hkkbwTT2sqlkkKLop2asByrE0sIfeesOwj7jNA5o%3D


U kunt ook de meest recente versie van de Hallo van Blitline van Azure Storage docs lezen [hier](http://www.blitline.com/docs/azure_storage).

## <a name="next-steps"></a>Volgende stappen
Ga naar blitline.com tooread over onze functies:

* Blitline API-eindpunt Docs <http://www.blitline.com/docs/api>
* Blitline API-functies <http://www.blitline.com/docs/functions>
* Voorbeelden van Blitline API <http://www.blitline.com/docs/examples>
* Het derde deel Nuget bibliotheek <http://nuget.org/packages/Blitline.Net>

