---
title: aaaUsing castLabs toodeliver Widevine-licenties tooAzure Media Services | Microsoft Docs
description: Dit artikel wordt beschreven hoe u Azure Media Services (AMS) toodeliver een stroom die dynamisch wordt versleuteld met AMS met PlayReady en Widevine DRM's kunt gebruiken. Hallo PlayReady-licenties afkomstig van de licentieserver Media Services PlayReady en Widevine-licentie wordt geleverd door castLabs licentieserver.
services: media-services
documentationcenter: 
author: Mingfeiy
manager: cfowler
editor: 
ms.assetid: 2a9a408a-a995-49e1-8d8f-ac5b51e17d40
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: Mingfeiy;willzhan;Juliako
ms.openlocfilehash: 80d2778fb283a96361e7e511990a36c2f551a310
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-castlabs-toodeliver-widevine-licenses-tooazure-media-services"></a><span data-ttu-id="03cc4-104">Met behulp van castLabs toodeliver Widevine-licenties tooAzure Media Services</span><span class="sxs-lookup"><span data-stu-id="03cc4-104">Using castLabs toodeliver Widevine licenses tooAzure Media Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="03cc4-105">Axinom</span><span class="sxs-lookup"><span data-stu-id="03cc4-105">Axinom</span></span>](media-services-axinom-integration.md)
> * [<span data-ttu-id="03cc4-106">castLabs</span><span class="sxs-lookup"><span data-stu-id="03cc4-106">castLabs</span></span>](media-services-castlabs-integration.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="03cc4-107">Overzicht</span><span class="sxs-lookup"><span data-stu-id="03cc4-107">Overview</span></span>
<span data-ttu-id="03cc4-108">Dit artikel wordt beschreven hoe u Azure Media Services (AMS) toodeliver een stroom die dynamisch wordt versleuteld met AMS met PlayReady en Widevine DRM's kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="03cc4-108">This article describes how you can use Azure Media Services (AMS) toodeliver a stream that is dynamically encrypted by AMS with both PlayReady and Widevine DRMs.</span></span> <span data-ttu-id="03cc4-109">Hallo PlayReady licentie afkomstig is van de licentieserver Media Services PlayReady en Widevine-licentie is geleverd door **castLabs** licentieserver.</span><span class="sxs-lookup"><span data-stu-id="03cc4-109">hello PlayReady license comes from Media Services PlayReady license server and Widevine license is delivered by **castLabs** license server.</span></span>

<span data-ttu-id="03cc4-110">tooplayback streaming van inhoud die is beveiligd door CENC (PlayReady en/of Widevine), kunt u [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="03cc4-110">tooplayback streaming content protected by CENC (PlayReady and/or Widevine), you can use  [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span> <span data-ttu-id="03cc4-111">Zie [AMP document](http://amp.azure.net/libs/amp/latest/docs/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="03cc4-111">See [AMP document](http://amp.azure.net/libs/amp/latest/docs/) for details.</span></span>

<span data-ttu-id="03cc4-112">Hallo volgende diagram ziet u een architectuur op hoog niveau Azure Media Services en castLabs integratie.</span><span class="sxs-lookup"><span data-stu-id="03cc4-112">hello following diagram demonstrates a high-level Azure Media Services and castLabs integration architecture.</span></span>

![Integratie](./media/media-services-castlabs-integration/media-services-castlabs-integration.png)

## <a name="typical-system-set-up"></a><span data-ttu-id="03cc4-114">Typische system instellen</span><span class="sxs-lookup"><span data-stu-id="03cc4-114">Typical system set up</span></span>
* <span data-ttu-id="03cc4-115">Media-inhoud wordt opgeslagen in AMS.</span><span class="sxs-lookup"><span data-stu-id="03cc4-115">Media content is stored in AMS.</span></span>
* <span data-ttu-id="03cc4-116">Sleutel-id's van inhoud sleutels worden opgeslagen in zowel castLabs als AMS.</span><span class="sxs-lookup"><span data-stu-id="03cc4-116">Key IDs of content keys are stored in both castLabs and AMS.</span></span>
* <span data-ttu-id="03cc4-117">castLabs en AMS hebben tokenverificatie ingebouwd.</span><span class="sxs-lookup"><span data-stu-id="03cc4-117">castLabs and AMS both have token authentication built in.</span></span> <span data-ttu-id="03cc4-118">verificatietokens worden besproken die Hallo uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="03cc4-118">hello following sections discuss authentication tokens.</span></span> 
* <span data-ttu-id="03cc4-119">Wanneer een client toostream Hallo video aanvraagt, Hallo inhoud dynamisch is versleuteld met **Common Encryption** (CENC) en dynamisch geleverd door AMS tooSmooth Streaming- en DASH.</span><span class="sxs-lookup"><span data-stu-id="03cc4-119">When a client requests toostream hello video, hello content is dynamically encrypted with **Common Encryption** (CENC) and dynamically packaged by AMS tooSmooth Streaming and DASH.</span></span> <span data-ttu-id="03cc4-120">We bieden ook PlayReady M2TS elementaire stroom versleuteling voor streaming HLS-protocol.</span><span class="sxs-lookup"><span data-stu-id="03cc4-120">We also deliver PlayReady M2TS elementary stream encryption for HLS streaming protocol.</span></span>
* <span data-ttu-id="03cc4-121">PlayReady-licentie is opgehaald uit de AMS-licentieserver en Widevine-licentie is opgehaald uit de licentieserver castLabs.</span><span class="sxs-lookup"><span data-stu-id="03cc4-121">PlayReady license is retrieved from AMS license server and Widevine license is retrieved from castLabs license server.</span></span> 
* <span data-ttu-id="03cc4-122">Mediaspeler besluit automatisch welke licentie toofetch op basis van de mogelijkheden van het platform voor Hallo-client.</span><span class="sxs-lookup"><span data-stu-id="03cc4-122">Media Player automatically decides which license toofetch based on hello client platform capability.</span></span> 

## <a name="authentication-token-generation-for-getting-a-license"></a><span data-ttu-id="03cc4-123">Verificatie-token genereren voor het verkrijgen van een licentie</span><span class="sxs-lookup"><span data-stu-id="03cc4-123">Authentication token generation for getting a license</span></span>
<span data-ttu-id="03cc4-124">Zowel castLabs als AMS ondersteunen (JSON Web Token) JWT-token-indeling gebruikt tooauthorize een licentie.</span><span class="sxs-lookup"><span data-stu-id="03cc4-124">Both castLabs and AMS support JWT (JSON Web Token) token format used tooauthorize a license.</span></span> 

### <a name="jwt-token-in-ams"></a><span data-ttu-id="03cc4-125">JWT-token in AMS</span><span class="sxs-lookup"><span data-stu-id="03cc4-125">JWT token in AMS</span></span>
<span data-ttu-id="03cc4-126">Hallo volgende tabel beschrijft de JWT-token in AMS.</span><span class="sxs-lookup"><span data-stu-id="03cc4-126">hello following table describes JWT token in AMS.</span></span> 

| <span data-ttu-id="03cc4-127">certificaatverlener</span><span class="sxs-lookup"><span data-stu-id="03cc4-127">Issuer</span></span> | <span data-ttu-id="03cc4-128">Tekenreeks van de verlener van Hallo gekozen Secure Token Service (STS)</span><span class="sxs-lookup"><span data-stu-id="03cc4-128">Issuer string from hello chosen Secure Token Service (STS)</span></span> |
| --- | --- |
| <span data-ttu-id="03cc4-129">Doelgroep</span><span class="sxs-lookup"><span data-stu-id="03cc4-129">Audience</span></span> |<span data-ttu-id="03cc4-130">Tekenreeks van de doelgroep van Hallo gebruikt STS</span><span class="sxs-lookup"><span data-stu-id="03cc4-130">Audience string from hello used STS</span></span> |
| <span data-ttu-id="03cc4-131">Claims</span><span class="sxs-lookup"><span data-stu-id="03cc4-131">Claims</span></span> |<span data-ttu-id="03cc4-132">Een set claims</span><span class="sxs-lookup"><span data-stu-id="03cc4-132">A set of claims</span></span> |
| <span data-ttu-id="03cc4-133">NotBefore</span><span class="sxs-lookup"><span data-stu-id="03cc4-133">NotBefore</span></span> |<span data-ttu-id="03cc4-134">Start de geldigheid van Hallo-token</span><span class="sxs-lookup"><span data-stu-id="03cc4-134">Start validity of hello token</span></span> |
| <span data-ttu-id="03cc4-135">Verloopt</span><span class="sxs-lookup"><span data-stu-id="03cc4-135">Expires</span></span> |<span data-ttu-id="03cc4-136">Einde geldigheid van Hallo-token</span><span class="sxs-lookup"><span data-stu-id="03cc4-136">End validity of hello token</span></span> |
| <span data-ttu-id="03cc4-137">SigningCredentials</span><span class="sxs-lookup"><span data-stu-id="03cc4-137">SigningCredentials</span></span> |<span data-ttu-id="03cc4-138">Hallo-sleutel die wordt gedeeld door PlayReady-licentieserver castLabs licentieserver en STS, sleutel van zowel symmetrisch als asymmetrisch kan zijn.</span><span class="sxs-lookup"><span data-stu-id="03cc4-138">hello key that is shared among PlayReady License Server, castLabs License Server and STS, it could be either symmetric or asymmetric key.</span></span> |

### <a name="jwt-token-in-castlabs"></a><span data-ttu-id="03cc4-139">JWT-token in castLabs</span><span class="sxs-lookup"><span data-stu-id="03cc4-139">JWT token in castLabs</span></span>
<span data-ttu-id="03cc4-140">Hallo volgende tabel beschrijft de JWT-token in castLabs.</span><span class="sxs-lookup"><span data-stu-id="03cc4-140">hello following table describes JWT token in castLabs.</span></span> 

| <span data-ttu-id="03cc4-141">Naam</span><span class="sxs-lookup"><span data-stu-id="03cc4-141">Name</span></span> | <span data-ttu-id="03cc4-142">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="03cc4-142">Description</span></span> |
| --- | --- |
| <span data-ttu-id="03cc4-143">optData</span><span class="sxs-lookup"><span data-stu-id="03cc4-143">optData</span></span> |<span data-ttu-id="03cc4-144">Een JSON-tekenreeks met informatie over u.</span><span class="sxs-lookup"><span data-stu-id="03cc4-144">A JSON string containing information about you.</span></span> |
| <span data-ttu-id="03cc4-145">CRT</span><span class="sxs-lookup"><span data-stu-id="03cc4-145">crt</span></span> |<span data-ttu-id="03cc4-146">Een met JSON-tekenreeks-informatie over asset hello, de licentierechten voor gegevens en afspelen.</span><span class="sxs-lookup"><span data-stu-id="03cc4-146">A JSON string containing information about hello asset, its license info and playback rights.</span></span> |
| <span data-ttu-id="03cc4-147">IAT</span><span class="sxs-lookup"><span data-stu-id="03cc4-147">iat</span></span> |<span data-ttu-id="03cc4-148">Hallo huidige datetime in epoche.</span><span class="sxs-lookup"><span data-stu-id="03cc4-148">hello current datetime in epoch.</span></span> |
| <span data-ttu-id="03cc4-149">jti</span><span class="sxs-lookup"><span data-stu-id="03cc4-149">jti</span></span> |<span data-ttu-id="03cc4-150">Een unieke id over dit token (elke token kan slechts eenmaal worden gebruikt in Hallo castLabs system).</span><span class="sxs-lookup"><span data-stu-id="03cc4-150">A unique identifier about this token (every token can only be used once in hello castLabs system).</span></span> |

## <a name="sample-solution-set-up"></a><span data-ttu-id="03cc4-151">Voorbeeldoplossing instellen</span><span class="sxs-lookup"><span data-stu-id="03cc4-151">Sample solution set up</span></span>
<span data-ttu-id="03cc4-152">Hallo [oplossing steekproef](https://github.com/AzureMediaServicesSamples/CastlabsIntegration) bestaat uit twee projecten:</span><span class="sxs-lookup"><span data-stu-id="03cc4-152">hello [sample solution](https://github.com/AzureMediaServicesSamples/CastlabsIntegration) consists of two projects:</span></span>

* <span data-ttu-id="03cc4-153">Een consoletoepassing die gebruikt tooset DRM beperkingen op een al opgenomen asset voor zowel PlayReady als Widevine worden kan.</span><span class="sxs-lookup"><span data-stu-id="03cc4-153">A console app that can be used tooset DRM restrictions on an already ingested asset, for both PlayReady and Widevine.</span></span>
* <span data-ttu-id="03cc4-154">Een webtoepassing die handen uit beveiligingstokens die kunnen worden gezien als een zeer vereenvoudigde versie van een STS.</span><span class="sxs-lookup"><span data-stu-id="03cc4-154">A Web Application that hands out tokens, which could be seen as a VERY SIMPLIFIED version of an STS.</span></span>

<span data-ttu-id="03cc4-155">toouse Hallo-consoletoepassing:</span><span class="sxs-lookup"><span data-stu-id="03cc4-155">toouse hello console application:</span></span>

1. <span data-ttu-id="03cc4-156">Hallo app.config toosetup AMS referenties, castLabs referenties, STS-configuratie en gedeelde sleutel wijzigen.</span><span class="sxs-lookup"><span data-stu-id="03cc4-156">Change hello app.config toosetup AMS credentials, castLabs credentials, STS configuration and shared key.</span></span>
2. <span data-ttu-id="03cc4-157">Upload een Asset naar AMS.</span><span class="sxs-lookup"><span data-stu-id="03cc4-157">Upload an Asset into AMS.</span></span>
3. <span data-ttu-id="03cc4-158">Get Hallo UUID van Hallo Asset geüpload en 32 regel in het bestand Program.cs Hallo wijzigen:</span><span class="sxs-lookup"><span data-stu-id="03cc4-158">Get hello UUID from hello uploaded Asset, and change Line 32 in hello Program.cs file:</span></span>
   
      <span data-ttu-id="03cc4-159">var objIAsset = _context. Assets.Where (x = > x.Id == "nb:cid:UUID:dac53a5d-1500-80bd-b864-f1e4b62594cf '). FirstOrDefault();</span><span class="sxs-lookup"><span data-stu-id="03cc4-159">var objIAsset = _context.Assets.Where(x => x.Id == "nb:cid:UUID:dac53a5d-1500-80bd-b864-f1e4b62594cf").FirstOrDefault();</span></span>
4. <span data-ttu-id="03cc4-160">Gebruik een item-id hebt voor de naamgeving van Hallo asset in Hallo castLabs systeem (Line 44 in het bestand Program.cs Hallo).</span><span class="sxs-lookup"><span data-stu-id="03cc4-160">Use an AssetId for naming hello asset in hello castLabs system (Line 44 in hello Program.cs file).</span></span>
   
   <span data-ttu-id="03cc4-161">U moet instellen item-id hebt voor **castLabs**; moet een unieke alfanumerieke tekenreeks toobe.</span><span class="sxs-lookup"><span data-stu-id="03cc4-161">You must set AssetId for **castLabs**; it needs toobe a unique alphanumeric string.</span></span>
5. <span data-ttu-id="03cc4-162">Hallo-programma uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="03cc4-162">Run hello program.</span></span>

<span data-ttu-id="03cc4-163">toouse hello Web Application (STS):</span><span class="sxs-lookup"><span data-stu-id="03cc4-163">toouse hello Web Application (STS):</span></span>

1. <span data-ttu-id="03cc4-164">Wijziging Hallo web.config toosetup castlabs verkoper-ID, Hallo STS-configuratie en Hallo gedeelde sleutel.</span><span class="sxs-lookup"><span data-stu-id="03cc4-164">Change hello web.config toosetup castlabs merchant ID, hello STS configuration and hello shared key.</span></span>
2. <span data-ttu-id="03cc4-165">Implementeer tooAzure Websites.</span><span class="sxs-lookup"><span data-stu-id="03cc4-165">Deploy tooAzure Websites.</span></span>
3. <span data-ttu-id="03cc4-166">Navigeer toohello website.</span><span class="sxs-lookup"><span data-stu-id="03cc4-166">Navigate toohello website.</span></span>

## <a name="playing-back-a-video"></a><span data-ttu-id="03cc4-167">Afspelen van video</span><span class="sxs-lookup"><span data-stu-id="03cc4-167">Playing back a video</span></span>
<span data-ttu-id="03cc4-168">tooplayback video versleuteld met common encryption (PlayReady en/of Widevine), kunt u Hallo [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="03cc4-168">tooplayback a video encrypted with common encryption (PlayReady and/or Widevine), you can use hello [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span> <span data-ttu-id="03cc4-169">Bij het uitvoeren van de console-app Hallo Hallo inhoud sleutel-ID en Hallo Manifest URL teruggestuurd.</span><span class="sxs-lookup"><span data-stu-id="03cc4-169">When running hello console app, hello Content Key ID and hello Manifest URL are echoed.</span></span>

1. <span data-ttu-id="03cc4-170">Een nieuw tabblad openen en start de STS: http://[yourStsName].azurewebsites.net/api/token/assetid/[yourCastLabsAssetId]/contentkeyid/[thecontentkeyid].</span><span class="sxs-lookup"><span data-stu-id="03cc4-170">Open a new tab and launch your STS: http://[yourStsName].azurewebsites.net/api/token/assetid/[yourCastLabsAssetId]/contentkeyid/[thecontentkeyid].</span></span>
2. <span data-ttu-id="03cc4-171">Ga te[Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="03cc4-171">Go too[Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>
3. <span data-ttu-id="03cc4-172">Plak in Hallo streaming-URL.</span><span class="sxs-lookup"><span data-stu-id="03cc4-172">Paste in hello streaming URL.</span></span>
4. <span data-ttu-id="03cc4-173">Klik op Hallo **geavanceerde opties** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="03cc4-173">Click hello **Advanced Options** checkbox.</span></span>
5. <span data-ttu-id="03cc4-174">In Hallo **beveiliging** vervolgkeuzelijst, selecteer PlayReady en/of Widevine.</span><span class="sxs-lookup"><span data-stu-id="03cc4-174">In hello **Protection** dropdown, select PlayReady and/or Widevine.</span></span>
6. <span data-ttu-id="03cc4-175">Hallo-token die u hebt verkregen van de STS in Hallo Token tekstvak plakken.</span><span class="sxs-lookup"><span data-stu-id="03cc4-175">Paste hello token that you got from your STS in hello Token textbox.</span></span> 
   
   <span data-ttu-id="03cc4-176">Hallo castLab licentieserver niet hoeft Hallo ' Bearer = "voorvoegsel voor Hallo-token.</span><span class="sxs-lookup"><span data-stu-id="03cc4-176">hello castLab license server does not need hello “Bearer=” prefix in front of hello token.</span></span> <span data-ttu-id="03cc4-177">Dus verwijder die vóór het verzenden van Hallo-token.</span><span class="sxs-lookup"><span data-stu-id="03cc4-177">So please remove that before submitting hello token.</span></span>
7. <span data-ttu-id="03cc4-178">Hallo player bijwerken.</span><span class="sxs-lookup"><span data-stu-id="03cc4-178">Update hello player.</span></span>
8. <span data-ttu-id="03cc4-179">Hallo video moet worden afgespeeld.</span><span class="sxs-lookup"><span data-stu-id="03cc4-179">hello video should be playing.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="03cc4-180">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="03cc4-180">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="03cc4-181">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="03cc4-181">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

