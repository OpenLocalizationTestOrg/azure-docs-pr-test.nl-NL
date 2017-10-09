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
# <a name="how-toouse-blitline-with-azure-and-azure-storage"></a><span data-ttu-id="0c767-103">Hoe toouse Blitline met Azure en Azure Storage</span><span class="sxs-lookup"><span data-stu-id="0c767-103">How toouse Blitline with Azure and Azure Storage</span></span>
<span data-ttu-id="0c767-104">Deze handleiding wordt uitgelegd hoe tooaccess Blitline services en hoe toosubmit tooBlitline taken.</span><span class="sxs-lookup"><span data-stu-id="0c767-104">This guide will explain how tooaccess Blitline services and how toosubmit jobs tooBlitline.</span></span>

## <a name="what-is-blitline"></a><span data-ttu-id="0c767-105">Wat is Blitline?</span><span class="sxs-lookup"><span data-stu-id="0c767-105">What is Blitline?</span></span>
<span data-ttu-id="0c767-106">Blitline is een cloud-gebaseerde verwerking van afbeeldingen enterprise niveau beeldverwerking een fractie van Hallo prijs toobuild zou kosten biedt deze zelf.</span><span class="sxs-lookup"><span data-stu-id="0c767-106">Blitline is a cloud-based image processing service that provides enterprise level image processing at a fraction of hello price that it would cost toobuild it yourself.</span></span>

<span data-ttu-id="0c767-107">Hallo feit is dat beeldverwerking is nog steeds opnieuw, meestal opnieuw opgebouwd uit Hallo ontwerp voor elke website.</span><span class="sxs-lookup"><span data-stu-id="0c767-107">hello fact is that image processing has been done over and over again, usually rebuilt from hello ground up for each and every website.</span></span> <span data-ttu-id="0c767-108">We realiseren dit omdat we hebt gebouwd ze een miljoen keer te.</span><span class="sxs-lookup"><span data-stu-id="0c767-108">We realize this because we’ve built them a million times too.</span></span> <span data-ttu-id="0c767-109">Één dag die we besloten mogelijk is het tijd doen we zojuist dit voor iedereen.</span><span class="sxs-lookup"><span data-stu-id="0c767-109">One day we decided that perhaps it‘s time we just do it for everyone.</span></span> <span data-ttu-id="0c767-110">We weten hoe toodo het toodo snel en efficiënt en sla Iedereen werkt deze in Hallo tussentijd.</span><span class="sxs-lookup"><span data-stu-id="0c767-110">We know how toodo it, toodo it fast and efficiently, and save everyone work in hello meantime.</span></span>

<span data-ttu-id="0c767-111">Zie voor meer informatie [http://www.blitline.com](http://www.blitline.com).</span><span class="sxs-lookup"><span data-stu-id="0c767-111">For more information, see [http://www.blitline.com](http://www.blitline.com).</span></span>

## <a name="what-blitline-is-not"></a><span data-ttu-id="0c767-112">Wat Blitline is niet...</span><span class="sxs-lookup"><span data-stu-id="0c767-112">What Blitline is NOT...</span></span>
<span data-ttu-id="0c767-113">tooclarify wat Blitline is handig voor het is vaak eenvoudiger tooidentify wat Blitline geen voordat u verder gaat.</span><span class="sxs-lookup"><span data-stu-id="0c767-113">tooclarify what Blitline is useful for, it is often easier tooidentify what Blitline does NOT do before moving forward.</span></span>

* <span data-ttu-id="0c767-114">Blitline heeft geen HTML-widgets tooupload afbeeldingen.</span><span class="sxs-lookup"><span data-stu-id="0c767-114">Blitline does NOT have HTML widgets tooupload images.</span></span> <span data-ttu-id="0c767-115">Openbaar of met beperkte machtigingen beschikbaar voor Blitline tooreach, moet u installatiekopieën beschikbaar hebben.</span><span class="sxs-lookup"><span data-stu-id="0c767-115">You must have images available publicly or with restricted permissions available for Blitline tooreach.</span></span>
* <span data-ttu-id="0c767-116">Blitline geen live installatiekopie verwerken, zoals Aviary.com</span><span class="sxs-lookup"><span data-stu-id="0c767-116">Blitline does NOT do live image processing, like Aviary.com</span></span>
* <span data-ttu-id="0c767-117">Blitline uploaden van afbeeldingen niet accepteert, kan niet u uw installatiekopieën tooBlitline rechtstreeks push.</span><span class="sxs-lookup"><span data-stu-id="0c767-117">Blitline does NOT accept image uploads, you cannot push your images tooBlitline directly.</span></span> <span data-ttu-id="0c767-118">U moet push ze tooAzure opslag of andere Blitline ondersteunt plaatsen en vervolgens instrueren Blitline waar toogo erbij.</span><span class="sxs-lookup"><span data-stu-id="0c767-118">You must push them tooAzure Storage or other places Blitline supports and then tell Blitline where toogo get them.</span></span>
* <span data-ttu-id="0c767-119">Blitline massively parallel en niet kan synchrone verwerking.</span><span class="sxs-lookup"><span data-stu-id="0c767-119">Blitline is massively parallel and does NOT do any synchronous processing.</span></span> <span data-ttu-id="0c767-120">Wat betekent dat u moet Geef ons een postback_url en kunnen we u wanneer we klaar bent verwerking.</span><span class="sxs-lookup"><span data-stu-id="0c767-120">Meaning you must give us a postback_url and we can tell you when we are done processing.</span></span>

## <a name="create-a-blitline-account"></a><span data-ttu-id="0c767-121">Een Blitline-account maken</span><span class="sxs-lookup"><span data-stu-id="0c767-121">Create a Blitline account</span></span>
[!INCLUDE [blitline-signup](../includes/blitline-signup.md)]

## <a name="how-toocreate-a-blitline-job"></a><span data-ttu-id="0c767-122">Hoe een taak Blitline toocreate</span><span class="sxs-lookup"><span data-stu-id="0c767-122">How toocreate a Blitline job</span></span>
<span data-ttu-id="0c767-123">Blitline maakt gebruik van JSON toodefine Hallo-acties die u wilt dat tootake op een installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="0c767-123">Blitline uses JSON toodefine hello actions you want tootake on an image.</span></span> <span data-ttu-id="0c767-124">Deze JSON bestaat uit een paar eenvoudige velden.</span><span class="sxs-lookup"><span data-stu-id="0c767-124">This JSON is composed of a few simple fields.</span></span>

<span data-ttu-id="0c767-125">de eenvoudigste voorbeeld Hallo is als volgt:</span><span class="sxs-lookup"><span data-stu-id="0c767-125">hello simplest example is as follows:</span></span>

        json : '{
       "application_id": "MY_APP_ID",
       "src" : "http://cdn.blitline.com/filters/boys.jpeg",
       "functions" : [ {
           "name": "resize_to_fit",
           "params" : { "width": 240, "height": 140 },
           "save" : { "image_identifier" : "external_sample_1" }
       } ]
    }'

<span data-ttu-id="0c767-126">Hier hebben we JSON die een installatiekopie van een 'src' duurt "... boys.jpeg" en vervolgens de grootte van deze installatiekopie too240x140.</span><span class="sxs-lookup"><span data-stu-id="0c767-126">Here we have JSON that will take a "src" image "...boys.jpeg" and then resize that image too240x140.</span></span>

<span data-ttu-id="0c767-127">Hallo toepassings-ID is iets vindt u in uw **VERBINDINGSGEGEVENS** of **beheren** tabblad op Azure.</span><span class="sxs-lookup"><span data-stu-id="0c767-127">hello Application ID is something you can find in your **CONNECTION INFO** or **MANAGE** tab on Azure.</span></span> <span data-ttu-id="0c767-128">Het is uw geheime id waarmee u toorun taken op Blitline.</span><span class="sxs-lookup"><span data-stu-id="0c767-128">It is your secret identifier that allows you toorun jobs on Blitline.</span></span>

<span data-ttu-id="0c767-129">Hallo 'opgeslagen'-parameter identificeert informatie over waar u tooput Hallo installatiekopie nadat we hebben het verwerkt.</span><span class="sxs-lookup"><span data-stu-id="0c767-129">hello "save" parameter identifies information about where you want tooput hello image once we have processed it.</span></span> <span data-ttu-id="0c767-130">In dit geval trivial nog niet hebben we een gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="0c767-130">In this trivial case, we haven't defined one.</span></span> <span data-ttu-id="0c767-131">Als er geen vestiging is gedefinieerd Blitline wordt opslaan lokaal (en tijdelijk) op de locatie van een unieke cloud.</span><span class="sxs-lookup"><span data-stu-id="0c767-131">If no location is defined Blitline will store it locally (and temporarily) at a unique cloud location.</span></span> <span data-ttu-id="0c767-132">U zult kunnen tooget die locatie Hallo JSON door Blitline geretourneerd wanneer u Hallo Blitline aanbrengt.</span><span class="sxs-lookup"><span data-stu-id="0c767-132">You will be able tooget that location from hello JSON returned by Blitline when you make hello Blitline.</span></span> <span data-ttu-id="0c767-133">Hallo 'installatiekopie' id is vereist en tooyou wordt geretourneerd wanneer tooidentify deze name installatiekopie opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="0c767-133">hello "image" identifier is required and is returned tooyou when tooidentify this particular saved image.</span></span>

<span data-ttu-id="0c767-134">U vindt meer informatie over Hallo *functies* we hier ondersteunen: <http://www.blitline.com/docs/functions></span><span class="sxs-lookup"><span data-stu-id="0c767-134">You can find more information about hello *functions* we support here: <http://www.blitline.com/docs/functions></span></span>

<span data-ttu-id="0c767-135">Ook vindt u documentatie over Hallo hier de opties voor de taak: <http://www.blitline.com/docs/api></span><span class="sxs-lookup"><span data-stu-id="0c767-135">You can also find documentation about hello job options here: <http://www.blitline.com/docs/api></span></span>

<span data-ttu-id="0c767-136">Zodra u hebt uw JSON toodo hoeft u **POST** deze te`http://api.blitline.com/job`</span><span class="sxs-lookup"><span data-stu-id="0c767-136">Once you have your JSON all you need toodo is **POST** it too`http://api.blitline.com/job`</span></span>

<span data-ttu-id="0c767-137">U ontvangt JSON terug die ziet er ongeveer als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="0c767-137">You will get JSON back that looks something like this:</span></span>

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


<span data-ttu-id="0c767-138">Weet u dat Blitline heeft uw aanvraag ontvangen, deze in een wachtrij voor verwerking geplaatst is en wanneer deze is voltooid Hallo afbeelding zijn beschikbaar op: **https://s3.amazonaws.com/dev.blitline/2011110722/YOUR\_APP\_ID /CK3f0xBF_2bV6wf7gEZE8w.jpg**</span><span class="sxs-lookup"><span data-stu-id="0c767-138">This tells you that Blitline has recieved your request, it has put it in a processing queue, and when it has completed hello image will be available at: **https://s3.amazonaws.com/dev.blitline/2011110722/YOUR\_APP\_ID/CK3f0xBF_2bV6wf7gEZE8w.jpg**</span></span>

## <a name="how-toosave-an-image-tooyour-azure-storage-account"></a><span data-ttu-id="0c767-139">Hoe toosave een installatiekopie tooyour Azure Storage-account</span><span class="sxs-lookup"><span data-stu-id="0c767-139">How toosave an image tooyour Azure Storage account</span></span>
<span data-ttu-id="0c767-140">Als u een Azure Storage-account hebt, kunt u eenvoudig Blitline push Hallo verwerkt afbeeldingen laten naar uw Azure container.</span><span class="sxs-lookup"><span data-stu-id="0c767-140">If you have an Azure Storage account, you can easily have Blitline push hello processed images into your Azure container.</span></span> <span data-ttu-id="0c767-141">Door het toevoegen van een 'azure_destination' definieert u Hallo locatie en machtigingen voor Blitline toopush aan.</span><span class="sxs-lookup"><span data-stu-id="0c767-141">By adding an "azure_destination" you define hello location and permissions for Blitline toopush to.</span></span>

<span data-ttu-id="0c767-142">Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="0c767-142">Here is an example:</span></span>

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


<span data-ttu-id="0c767-143">Door in te vullen Hallo CAPITALIZED waarden door uw eigen, dient u deze JSON-toohttp://api.blitline.com/job en hello 'src' installatiekopie wordt verwerkt met een vervagingsfilter en vervolgens gepusht tooyou Azure bestemming.</span><span class="sxs-lookup"><span data-stu-id="0c767-143">By filling in hello CAPITALIZED values with your own, you can submit this JSON toohttp://api.blitline.com/job and hello "src" image will be processed with a blur filter and then pushed tooyou Azure destination.</span></span>

### <a name="please-note"></a><span data-ttu-id="0c767-144">Opmerking:</span><span class="sxs-lookup"><span data-stu-id="0c767-144">Please note:</span></span>
<span data-ttu-id="0c767-145">Hallo SAS moet Hallo gehele SAS-url, inclusief Hallo-bestandsnaam van het doelbestand Hallo bevatten.</span><span class="sxs-lookup"><span data-stu-id="0c767-145">hello SAS must contain hello entire SAS url, including hello filename of hello destination file.</span></span>

<span data-ttu-id="0c767-146">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="0c767-146">Example:</span></span>

    http://blitline.blob.core.windows.net/sample/image.jpg?sr=b&sv=2012-02-12&st=2013-04-12T03%3A18%3A30Z&se=2013-04-12T04%3A18%3A30Z&sp=w&sig=Bte2hkkbwTT2sqlkkKLop2asByrE0sIfeesOwj7jNA5o%3D


<span data-ttu-id="0c767-147">U kunt ook de meest recente versie van de Hallo van Blitline van Azure Storage docs lezen [hier](http://www.blitline.com/docs/azure_storage).</span><span class="sxs-lookup"><span data-stu-id="0c767-147">You can also read hello latest edition of Blitline's Azure Storage docs [here](http://www.blitline.com/docs/azure_storage).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0c767-148">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0c767-148">Next Steps</span></span>
<span data-ttu-id="0c767-149">Ga naar blitline.com tooread over onze functies:</span><span class="sxs-lookup"><span data-stu-id="0c767-149">Visit blitline.com tooread about all our other features:</span></span>

* <span data-ttu-id="0c767-150">Blitline API-eindpunt Docs <http://www.blitline.com/docs/api></span><span class="sxs-lookup"><span data-stu-id="0c767-150">Blitline API Endpoint Docs <http://www.blitline.com/docs/api></span></span>
* <span data-ttu-id="0c767-151">Blitline API-functies <http://www.blitline.com/docs/functions></span><span class="sxs-lookup"><span data-stu-id="0c767-151">Blitline API Functions <http://www.blitline.com/docs/functions></span></span>
* <span data-ttu-id="0c767-152">Voorbeelden van Blitline API <http://www.blitline.com/docs/examples></span><span class="sxs-lookup"><span data-stu-id="0c767-152">Blitline API Examples <http://www.blitline.com/docs/examples></span></span>
* <span data-ttu-id="0c767-153">Het derde deel Nuget bibliotheek <http://nuget.org/packages/Blitline.Net></span><span class="sxs-lookup"><span data-stu-id="0c767-153">Third Part Nuget Library <http://nuget.org/packages/Blitline.Net></span></span>

