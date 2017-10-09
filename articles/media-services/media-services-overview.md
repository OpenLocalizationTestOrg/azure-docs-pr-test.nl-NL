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
# <a name="azure-media-services-overview"></a><span data-ttu-id="ec764-103">Overzicht van Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="ec764-103">Azure Media Services overview</span></span> 

<span data-ttu-id="ec764-104">Microsoft Azure Media Services is een uitbreidbaar cloudplatform waarmee ontwikkelaars toobuild schaalbare media beheer- en toepassingen.</span><span class="sxs-lookup"><span data-stu-id="ec764-104">Microsoft Azure Media Services is an extensible cloud-based platform that enables developers toobuild scalable media management and delivery applications.</span></span> <span data-ttu-id="ec764-105">Media Services is gebaseerd op de REST-API's waarmee u toosecurely uploaden, opslaan, coderen en video of audio-inhoud van het pakket voor zowel op aanvraag en live streaming levering toovarious clients (bijvoorbeeld TV, PC en mobiele apparaten).</span><span class="sxs-lookup"><span data-stu-id="ec764-105">Media Services is based on REST APIs that enable you toosecurely upload, store, encode, and package video or audio content for both on-demand and live streaming delivery toovarious clients (for example, TV, PC, and mobile devices).</span></span>

<span data-ttu-id="ec764-106">U kunt end-to-end-werkstromen volledig met Media Services bouwen.</span><span class="sxs-lookup"><span data-stu-id="ec764-106">You can build end-to-end workflows using entirely Media Services.</span></span> <span data-ttu-id="ec764-107">U kunt ook toouse onderdelen van derden voor sommige onderdelen van uw werkstroom.</span><span class="sxs-lookup"><span data-stu-id="ec764-107">You can also choose toouse third-party components for some parts of your workflow.</span></span> <span data-ttu-id="ec764-108">U kunt bijvoorbeeld coderen met een coderingsprogramma van een derde partij.</span><span class="sxs-lookup"><span data-stu-id="ec764-108">For example, encode using a third-party encoder.</span></span> <span data-ttu-id="ec764-109">Vervolgens kunt u uploaden, beveiligen, verpakken en leveren met Media Services.</span><span class="sxs-lookup"><span data-stu-id="ec764-109">Then, upload, protect, package, deliver using Media Services.</span></span>

<span data-ttu-id="ec764-110">U kunt kiezen toostream uw live-inhoud of inhoud op aanvraag leveren.</span><span class="sxs-lookup"><span data-stu-id="ec764-110">You can choose toostream your content live or deliver content on-demand.</span></span> <span data-ttu-id="ec764-111">Hallo onderwerp bevat ook koppelingen tooother relevante onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="ec764-111">hello topic also links tooother relevant topics.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="ec764-112">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="ec764-112">Media Services learning paths</span></span>
<span data-ttu-id="ec764-113">U kunt hier de AMS-leertrajecten bekijken:</span><span class="sxs-lookup"><span data-stu-id="ec764-113">You can view AMS learning paths here:</span></span>

* [<span data-ttu-id="ec764-114">Werkstroom voor AMS Live Streaming</span><span class="sxs-lookup"><span data-stu-id="ec764-114">AMS Live Streaming Workflow</span></span>](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-live/)
* [<span data-ttu-id="ec764-115">Werkstroom voor AMS On-Demand Streaming</span><span class="sxs-lookup"><span data-stu-id="ec764-115">AMS on-Demand Streaming Workflow</span></span>](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-on-demand/)

## <a name="prerequisites"></a><span data-ttu-id="ec764-116">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ec764-116">Prerequisites</span></span>

<span data-ttu-id="ec764-117">toostart met Azure Media Services, moet u de volgende Hallo hebben:</span><span class="sxs-lookup"><span data-stu-id="ec764-117">toostart using Azure Media Services, you should have hello following:</span></span>

* <span data-ttu-id="ec764-118">Een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="ec764-118">An Azure account.</span></span> <span data-ttu-id="ec764-119">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="ec764-119">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="ec764-120">Zie [Gratis proefversie van Azure](https://azure.microsoft.com) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ec764-120">For details, see [Azure Free Trial](https://azure.microsoft.com).</span></span>
* <span data-ttu-id="ec764-121">Een Azure Media Services-account.</span><span class="sxs-lookup"><span data-stu-id="ec764-121">An Azure Media Services account.</span></span> <span data-ttu-id="ec764-122">Zie [Een account maken](media-services-portal-create-account.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ec764-122">For more information, see [Create Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="ec764-123">(Optioneel) Instellen van de ontwikkelomgeving.</span><span class="sxs-lookup"><span data-stu-id="ec764-123">(Optional) Set up development environment.</span></span> <span data-ttu-id="ec764-124">Kies .NET of REST API voor uw ontwikkelomgeving.</span><span class="sxs-lookup"><span data-stu-id="ec764-124">Choose .NET or REST API for your development environment.</span></span> <span data-ttu-id="ec764-125">Zie [De omgeving instellen](media-services-dotnet-how-to-use.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ec764-125">For more information, see [Set up environment](media-services-dotnet-how-to-use.md).</span></span>

    <span data-ttu-id="ec764-126">Leer ook hoe te[verbinding maken via een programma tooAMS API](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="ec764-126">Also, learn how too[connect  programmatically tooAMS API](media-services-use-aad-auth-to-access-ams-api.md).</span></span>
* <span data-ttu-id="ec764-127">Een streaming-eindpunt (Standard of Premium) in de status Gestart.</span><span class="sxs-lookup"><span data-stu-id="ec764-127">A standard or premium streaming endpoint in started state.</span></span>  <span data-ttu-id="ec764-128">Zie [Managing streaming endpoints](media-services-portal-manage-streaming-endpoints.md) (Streaming-eindpunten beheren) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ec764-128">For more information, see [Managing streaming endpoints](media-services-portal-manage-streaming-endpoints.md)</span></span>

## <a name="sdks-and-tools"></a><span data-ttu-id="ec764-129">SDK's en hulpprogramma's</span><span class="sxs-lookup"><span data-stu-id="ec764-129">SDKs and tools</span></span>

<span data-ttu-id="ec764-130">toobuild Media Services-oplossingen, u kunt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="ec764-130">toobuild Media Services solutions, you can use:</span></span>

* [<span data-ttu-id="ec764-131">Media Services REST API</span><span class="sxs-lookup"><span data-stu-id="ec764-131">Media Services REST API</span></span>](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference)
* <span data-ttu-id="ec764-132">Een van de Hallo beschikbare client-SDK's:</span><span class="sxs-lookup"><span data-stu-id="ec764-132">One of hello available client SDKs:</span></span>
    * <span data-ttu-id="ec764-133">[Azure Media Services SDK voor .NET](https://github.com/Azure/azure-sdk-for-media-services)</span><span class="sxs-lookup"><span data-stu-id="ec764-133">[Azure Media Services SDK for .NET](https://github.com/Azure/azure-sdk-for-media-services),</span></span>
    * <span data-ttu-id="ec764-134">[Azure SDK voor Java](https://github.com/Azure/azure-sdk-for-java)</span><span class="sxs-lookup"><span data-stu-id="ec764-134">[Azure SDK for Java](https://github.com/Azure/azure-sdk-for-java),</span></span>
    * <span data-ttu-id="ec764-135">[Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php)</span><span class="sxs-lookup"><span data-stu-id="ec764-135">[Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php),</span></span>
    * <span data-ttu-id="ec764-136">[Azure Media Services voor Node.js](https://github.com/michelle-becker/node-ams-sdk/blob/master/lib/request.js) (Dit is een niet-Microsoft-versie van een Node.js SDK.</span><span class="sxs-lookup"><span data-stu-id="ec764-136">[Azure Media Services for Node.js](https://github.com/michelle-becker/node-ams-sdk/blob/master/lib/request.js) (This is a non-Microsoft version of a Node.js SDK.</span></span> <span data-ttu-id="ec764-137">Wordt onderhouden door een community en momenteel geen een 100% dekking voor AMS APIs Hallo).</span><span class="sxs-lookup"><span data-stu-id="ec764-137">It is maintained by a community and currently does not have a 100% coverage of hello AMS APIs).</span></span>
* <span data-ttu-id="ec764-138">Bestaande hulpprogramma's:</span><span class="sxs-lookup"><span data-stu-id="ec764-138">Existing tools:</span></span>
    * [<span data-ttu-id="ec764-139">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ec764-139">Azure portal</span></span>](https://portal.azure.com/)
    * <span data-ttu-id="ec764-140">[Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (Azure Media Services Explorer (AMSE) is een Winforms-/C#-toepassing voor Windows)</span><span class="sxs-lookup"><span data-stu-id="ec764-140">[Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (Azure Media Services Explorer (AMSE) is a Winforms/C# application for Windows)</span></span>

## <a name="concepts-and-overview"></a><span data-ttu-id="ec764-141">Concepten en overzicht</span><span class="sxs-lookup"><span data-stu-id="ec764-141">Concepts and overview</span></span>
<span data-ttu-id="ec764-142">Zie [Concepten](media-services-concepts.md) voor Azure Media Services-concepten.</span><span class="sxs-lookup"><span data-stu-id="ec764-142">For Azure Media Services concepts, see [Concepts](media-services-concepts.md).</span></span>

<span data-ttu-id="ec764-143">Zie voor een hoe-tooseries waarin u kennis kunt tooall Hallo hoofdonderdelen van Azure Media Services, [Azure Media Services stapsgewijze zelfstudies](https://docs.com/fukushima-shigeyuki/3439/english-azure-media-services-step-by-step-series).</span><span class="sxs-lookup"><span data-stu-id="ec764-143">For a how-tooseries that introduces you tooall hello main components of Azure Media Services, see [Azure Media Services Step-by-Step tutorials](https://docs.com/fukushima-shigeyuki/3439/english-azure-media-services-step-by-step-series).</span></span> <span data-ttu-id="ec764-144">Deze reeks biedt een goed overzicht van de concepten en maakt gebruik van Hallo AMSE-hulpprogramma toodemonstrate AMS taken.</span><span class="sxs-lookup"><span data-stu-id="ec764-144">This series has a great overview of concepts and it uses hello AMSE tool toodemonstrate AMS tasks.</span></span> <span data-ttu-id="ec764-145">Het AMSE-hulpprogramma is een Windows-hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="ec764-145">AMSE tool is a Windows tool.</span></span> <span data-ttu-id="ec764-146">Dit hulpprogramma ondersteunt de meeste Hallo-taken die u programmatisch met bereiken kunt [AMS SDK voor .NET](https://github.com/Azure/azure-sdk-for-media-services), [Azure SDK voor Java](https://github.com/Azure/azure-sdk-for-java), of [Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php).</span><span class="sxs-lookup"><span data-stu-id="ec764-146">This tool supports most of hello tasks you can achieve programmatically with [AMS SDK for .NET](https://github.com/Azure/azure-sdk-for-media-services), [Azure SDK for Java](https://github.com/Azure/azure-sdk-for-java), or  [Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php).</span></span>

## <a name="supported-scenarios-and-availability-of-media-services-across-data-centers"></a><span data-ttu-id="ec764-147">Ondersteunde scenario's en de beschikbaarheid van Media Services in datacenters</span><span class="sxs-lookup"><span data-stu-id="ec764-147">Supported scenarios and availability of Media Services across data centers</span></span>

<span data-ttu-id="ec764-148">Zie voor gedetailleerde informatie [Scenarios and availability of Media Services features across datacenters](scenarios-and-availability.md) (Scenario's en beschikbaarheid van Media Services-functies via datacenters).</span><span class="sxs-lookup"><span data-stu-id="ec764-148">For detailed information, see [AMS scenarios and availability of features and services across data centers](scenarios-and-availability.md).</span></span>

## <a name="service-level-agreement-sla"></a><span data-ttu-id="ec764-149">Service Level Agreement (SLA)</span><span class="sxs-lookup"><span data-stu-id="ec764-149">Service Level Agreement (SLA)</span></span>

* <span data-ttu-id="ec764-150">Voor Media Services-codering wordt een beschikbaarheid van 99,9% voor REST API-transacties gegarandeerd.</span><span class="sxs-lookup"><span data-stu-id="ec764-150">For Media Services Encoding, we guarantee 99.9% availability of REST API transactions.</span></span>
* <span data-ttu-id="ec764-151">Wanneer er een Standard- of Premium-streaming-eindpunt is gekocht, worden service-aanvragen voor streaming beantwoord met een beschikbaarheidsgarantie van 99,9% voor bestaande media-inhoud.</span><span class="sxs-lookup"><span data-stu-id="ec764-151">For Streaming, we will successfully service requests with a 99.9% availability guarantee for existing media content when a standard or premium streaming endpoint is purchased.</span></span>
* <span data-ttu-id="ec764-152">Voor Livekanalen wordt gegarandeerd dat actieve kanalen extern verbinding heeft minimaal 99,9% van Hallo tijd.</span><span class="sxs-lookup"><span data-stu-id="ec764-152">For Live Channels, we guarantee that running Channels will have external connectivity at least 99.9% of hello time.</span></span>
* <span data-ttu-id="ec764-153">Voor Content Protection wordt gegarandeerd dat worden vervuld sleutelaanvragen minimaal 99,9% van Hallo tijd.</span><span class="sxs-lookup"><span data-stu-id="ec764-153">For Content Protection, we guarantee that we will successfully fulfill key requests at least 99.9% of hello time.</span></span>
* <span data-ttu-id="ec764-154">Voor de indexeerfunctie wordt we is indexeerfunctie taak aanvragen verwerkt met een gereserveerd codering service eenheid 99,9% van Hallo tijd.</span><span class="sxs-lookup"><span data-stu-id="ec764-154">For Indexer, we will successfully service Indexer Task requests processed with an Encoding Reserved Unit 99.9% of hello time.</span></span>

<span data-ttu-id="ec764-155">Zie [Microsoft Azure SLA](https://azure.microsoft.com/support/legal/sla/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ec764-155">For more information, see [Microsoft Azure SLA](https://azure.microsoft.com/support/legal/sla/).</span></span>

<span data-ttu-id="ec764-156">Zie voor informatie over de beschikbaarheid van datacenters Hallo [Avaiability](scenarios-and-availability.md#availability) sectie.</span><span class="sxs-lookup"><span data-stu-id="ec764-156">For information about availability in datacenters, see hello [Avaiability](scenarios-and-availability.md#availability) section.</span></span>

## <a name="support"></a><span data-ttu-id="ec764-157">Ondersteuning</span><span class="sxs-lookup"><span data-stu-id="ec764-157">Support</span></span>

<span data-ttu-id="ec764-158">[Ondersteuning van Azure](https://azure.microsoft.com/support/options/) biedt ondersteuningsopties voor Azure, met inbegrip van Media Services.</span><span class="sxs-lookup"><span data-stu-id="ec764-158">[Azure Support](https://azure.microsoft.com/support/options/) provides support options for Azure, including Media Services.</span></span>

## <a name="provide-feedback"></a><span data-ttu-id="ec764-159">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="ec764-159">Provide feedback</span></span>

[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
