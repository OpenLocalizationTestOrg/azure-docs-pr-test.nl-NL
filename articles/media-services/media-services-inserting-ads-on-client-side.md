---
title: aaaInserting advertenties aan clientzijde Hallo | Microsoft Docs
description: Dit onderwerp leest hoe tooinsert advertenties op Hallo clientzijde.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 65c9c747-128e-497e-afe0-3f92d2bf7972
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: e6eab4aa92918ad734db8ac3a4e7818d02ed7fe4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="inserting-ads-on-hello-client-side"></a><span data-ttu-id="4ff6f-103">Advertenties aan clientzijde Hallo invoegen</span><span class="sxs-lookup"><span data-stu-id="4ff6f-103">Inserting ads on hello client side</span></span>
<span data-ttu-id="4ff6f-104">In dit onderwerp bevat informatie over het tooinsert verschillende soorten advertenties aan clientzijde Hallo.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-104">This topic contains information on how tooinsert various types of ads on hello client side.</span></span>

<span data-ttu-id="4ff6f-105">Zie voor meer informatie over gesloten ondertiteling en ad-ondersteuning in Live streaming video's [ondersteund gesloten ondertiteling en Ad invoegen standaarden](media-services-live-streaming-with-onprem-encoders.md#cc_and_ads).</span><span class="sxs-lookup"><span data-stu-id="4ff6f-105">For information about closed captioning and ad support in Live streaming videos, see [Supported Closed Captioning and Ad Insertion Standards](media-services-live-streaming-with-onprem-encoders.md#cc_and_ads).</span></span>

> [!NOTE]
> <span data-ttu-id="4ff6f-106">Azure Media Player biedt momenteel geen ondersteuning voor advertenties.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-106">Azure Media Player does not currently support Ads.</span></span>
> 
> 

## <span data-ttu-id="4ff6f-107"><a id="insert_ads_into_media"></a>Advertenties in uw Media invoegen</span><span class="sxs-lookup"><span data-stu-id="4ff6f-107"><a id="insert_ads_into_media"></a>Inserting Ads into your Media</span></span>
<span data-ttu-id="4ff6f-108">Azure Media Services biedt ondersteuning voor het invoegen van ad via Hallo Windows Media-Platform: Frameworks voor spelers.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-108">Azure Media Services provides support for ad insertion through hello Windows Media Platform: Player Frameworks.</span></span> <span data-ttu-id="4ff6f-109">Er zijn frameworks voor spelers met ad-ondersteuning beschikbaar voor Windows 8, Silverlight, Windows Phone 8 en iOS-apparaten.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-109">Player frameworks with ad support are available for Windows 8, Silverlight, Windows Phone 8, and iOS devices.</span></span> <span data-ttu-id="4ff6f-110">Elke player-framework bevat voorbeeldcode die laat u hoe zien een toepassing player tooimplement. Er zijn drie soorten advertenties die u in uw media: de lijst invoegen kunt.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-110">Each player framework contains sample code that shows you how tooimplement a player application.There are three different kinds of ads you can insert into your media:list.</span></span>

* <span data-ttu-id="4ff6f-111">**Lineaire** – volledige frame advertenties die Hallo belangrijkste video onderbreken.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-111">**Linear** – full frame ads that pause hello main video.</span></span>
* <span data-ttu-id="4ff6f-112">**Niet-lineaire** – overlay advertenties die worden weergegeven als de belangrijkste video hello wordt afgespeeld, meestal een logo of een andere statische afbeelding geplaatst in Hallo player.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-112">**Nonlinear** – overlay ads that are displayed as hello main video is playing, usually a logo or other static image placed within hello player.</span></span>
* <span data-ttu-id="4ff6f-113">**Aanvullende** – advertenties die buiten Hallo player worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-113">**Companion** – ads that are displayed outside of hello player.</span></span>

<span data-ttu-id="4ff6f-114">Advertenties kunnen op elk punt in de tijdlijn Hallo belangrijkste video worden geplaatst.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-114">Ads can be placed at any point in hello main video’s time line.</span></span> <span data-ttu-id="4ff6f-115">U moet de hoogte Hallo player wanneer tooplay Hallo ad en welke tooplay advertenties.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-115">You must tell hello player when tooplay hello ad and which ads tooplay.</span></span> <span data-ttu-id="4ff6f-116">Dit wordt gedaan met behulp van een reeks standaard XML-bestanden: Video Ad-Service-sjabloon (VAST), digitale Video meerdere Ad afspeellijst (VMAP), Media abstracte sequentiëren sjabloon (b) en digitale Video Player Ad Interface Definition (VPAID).</span><span class="sxs-lookup"><span data-stu-id="4ff6f-116">This is done using a set of standard XML-based files: Video Ad Service Template (VAST), Digital Video Multiple Ad Playlist (VMAP), Media Abstract Sequencing Template (MAST), and Digital Video Player Ad Interface Definition (VPAID).</span></span> <span data-ttu-id="4ff6f-117">GROTE bestanden opgeven welke toodisplay advertenties.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-117">VAST files specify what ads toodisplay.</span></span> <span data-ttu-id="4ff6f-118">VMAP bestanden opgeven wanneer tooplay verschillende advertenties en ENORME XML bevatten.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-118">VMAP files specify when tooplay various ads and contain VAST XML.</span></span> <span data-ttu-id="4ff6f-119">B-bestanden zijn een andere manier toosequence advertenties die tevens VAST XML kunnen bevatten.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-119">MAST files are another way toosequence ads which also can contain VAST XML.</span></span> <span data-ttu-id="4ff6f-120">VPAID bestanden definiëren een interface tussen Hallo-speler en Hallo ad of ad-server.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-120">VPAID files define an interface between hello video player and hello ad or ad server.</span></span>

<span data-ttu-id="4ff6f-121">Elke player-framework werkt er anders en elk worden behandeld in een eigen onderwerp.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-121">Each player framework works differently and each will be covered in its own topic.</span></span> <span data-ttu-id="4ff6f-122">In dit onderwerp wordt beschreven Hallo basic mechanismen gebruikt tooinsert advertenties. Ads aanvragen-speler toepassingen bij een ad-server.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-122">This topic will describe hello basic mechanisms used tooinsert ads.Video player applications request ads from an ad server.</span></span> <span data-ttu-id="4ff6f-123">Hallo Active Directory-server kan reageren op een aantal verschillende manieren:</span><span class="sxs-lookup"><span data-stu-id="4ff6f-123">hello ad server can respond in a number of ways:</span></span>

* <span data-ttu-id="4ff6f-124">Een groot bestand geretourneerd</span><span class="sxs-lookup"><span data-stu-id="4ff6f-124">Return a VAST file</span></span>
* <span data-ttu-id="4ff6f-125">Retourneren van een bestand VMAP (met ingesloten VAST)</span><span class="sxs-lookup"><span data-stu-id="4ff6f-125">Return a VMAP file (with embedded VAST)</span></span>
* <span data-ttu-id="4ff6f-126">Retourneert een b-bestand (met ingesloten VAST)</span><span class="sxs-lookup"><span data-stu-id="4ff6f-126">Return a MAST file (with embedded VAST)</span></span>
* <span data-ttu-id="4ff6f-127">Een groot bestand met advertenties VPAID geretourneerd</span><span class="sxs-lookup"><span data-stu-id="4ff6f-127">Return a VAST file with VPAID ads</span></span>

### <a name="using-a-video-ad-service-template-vast-file"></a><span data-ttu-id="4ff6f-128">Met behulp van een Video Ad-Service (VAST) sjabloonbestand</span><span class="sxs-lookup"><span data-stu-id="4ff6f-128">Using a Video Ad Service Template (VAST) File</span></span>
<span data-ttu-id="4ff6f-129">Een groot bestand geeft welke ad of toodisplay advertenties.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-129">A VAST file specifies what ad or ads toodisplay.</span></span> <span data-ttu-id="4ff6f-130">Hallo is volgende XML-code een voorbeeld van een groot bestand voor een lineaire ad:</span><span class="sxs-lookup"><span data-stu-id="4ff6f-130">hello following XML is an example of a VAST file for a linear ad:</span></span>

    <VAST version="2.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="oxml.xsd">
      <Ad id="115571748">
        <InLine>
          <AdSystem version="2.0 alpha">Atlas</AdSystem>
          <AdTitle>Unknown</AdTitle>
          <Description>Unknown</Description>
          <Survey></Survey>
          <Error></Error>
          <Impression id="Atlas"><![CDATA[http://www.myserver.com/tracking-resource]]></Impression>
          <Creatives>
            <Creative id="video" sequence="0" AdID="">
              <Linear>
                <Duration>00:00:32</Duration>
                <TrackingEvents>
                  <Tracking event="start"><![CDATA[http://www.myserver.com/start-tracking-resource]]></Tracking>
                  <Tracking event="midpoint"><![CDATA[http://www.myserver.com/midpoint-tracking-resource]]></Tracking>
                  <Tracking event="complete"><![CDATA http://www.myserver.com/complete-tracking-resource]]></Tracking>
                  <Tracking event="expand"><![CDATA[http://www.myserver.com/expand-tracking-resource]]></Tracking>
                </TrackingEvents>
                <VideoClicks>
                  <ClickThrough id="Atlas Redirect"><![CDATA[http://www.myserver.com/click-resource]]></ClickThrough>
                  <ClickTracking id="Spare"></ClickTracking>
                </VideoClicks>
                <MediaFiles>
                  <MediaFile apiFramework="Windows Media" id="windows_progressive_200" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="200" width="400" height="300" type="video/x-ms-wmv">
                    <![CDATA[http://www.myserver.com/media/myad_200_4x3.wmv]]>
                  </MediaFile>
                  <MediaFile apiFramework="Windows Media" id="windows_progressive_300" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="300" width="400" height="300" type="video/x-ms-wmv">
                    <![CDATA[http://www.myserver.com/media/myad_300_4x3.wmv]]>
                  </MediaFile>
                </MediaFiles>
              </Linear>
            </Creative>
          </Creatives>
          <Extensions>
            <Extension type="Atlas">
            </Extension>
          </Extensions>
        </InLine>
      </Ad>
    </VAST>

<span data-ttu-id="4ff6f-131">Hallo lineaire ad is beschreven door Hallo <**lineair**> element.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-131">hello linear ad is described by hello <**Linear**> element.</span></span> <span data-ttu-id="4ff6f-132">Hiermee geeft u op Hallo duur van Hallo ad, bijhouden van gebeurtenissen, klikt u op via op bijhouden en een aantal **MediaFile** elementen.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-132">It specifies hello duration of hello ad, tracking events, click through, click tracking, and a number of **MediaFile** elements.</span></span> <span data-ttu-id="4ff6f-133">Bijhouden van gebeurtenissen zijn opgegeven in Hallo <**TrackingEvents**> element en een server ad tootrack verschillende gebeurtenissen die plaatsvinden terwijl u bekijkt hello ad toestaan.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-133">Tracking events are specified within hello <**TrackingEvents**> element and allow an ad server tootrack various events that occur while viewing hello ad.</span></span> <span data-ttu-id="4ff6f-134">In dit geval Hallo start en middelpunt, voltooid, en vouw gebeurtenissen worden bijgehouden.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-134">In this case hello start, midpoint, complete, and expand events are tracked.</span></span> <span data-ttu-id="4ff6f-135">Hallo startgebeurtenis treedt op wanneer ad hello wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-135">hello start event occurs when hello ad is displayed.</span></span> <span data-ttu-id="4ff6f-136">Hallo middelpunt gebeurtenis treedt op wanneer ten minste 50% van de tijdlijn van Hallo ad bekeken is.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-136">hello midpoint event occurs when at least 50% of hello ad’s timeline has been viewed.</span></span> <span data-ttu-id="4ff6f-137">Hallo gebeurtenis treedt op wanneer Hallo ad toohello end is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-137">hello complete event occurs when hello ad has run toohello end.</span></span> <span data-ttu-id="4ff6f-138">Hallo uit te breiden gebeurtenis treedt op wanneer de gebruiker Hallo wordt uitgebreid welkomstscherm-speler toofull.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-138">hello Expand event occurs when hello user expands hello video player toofull screen.</span></span> <span data-ttu-id="4ff6f-139">Clickthroughs worden aangeduid met een <**ClickThrough**>-element in een <**VideoClicks**> element en Hiermee geeft u een URI tooa resource toodisplay wanneer gebruiker Hallo op Hallo ad.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-139">Clickthroughs are specified with a <**ClickThrough**> element within a <**VideoClicks**> element and specifies a URI tooa resource toodisplay when hello user clicks on hello ad.</span></span> <span data-ttu-id="4ff6f-140">ClickTracking is opgegeven in een <**ClickTracking**>-element, ook in Hallo <**VideoClicks**> element en geeft u een resource bijhouden voor Hallo player toorequest wanneer Hallo-gebruiker op Hallo ad.hello <**MediaFile**> elementen informatie opgeven over een specifieke codering van een ad.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-140">ClickTracking is specified in a <**ClickTracking**> element, also within hello <**VideoClicks**> element and specifies a tracking resource for hello player toorequest when hello user clicks on hello ad.hello <**MediaFile**> elements specify information about a specific encoding of an ad.</span></span> <span data-ttu-id="4ff6f-141">Wanneer er meer dan één <**MediaFile**>-element, Hallo-speler kunt kiezen Hallo best-codering voor Hallo-platform.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-141">When there is more than one <**MediaFile**> element, hello video player can choose hello best encoding for hello platform.</span></span> 

<span data-ttu-id="4ff6f-142">Lineaire advertenties kunnen worden weergegeven in een bepaalde volgorde.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-142">Linear ads can be displayed in a specified order.</span></span> <span data-ttu-id="4ff6f-143">toodo, extra <Ad> elementen toohello VAST bestands- en Hallo volgorde met Hallo sequence-kenmerk opgeven.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-143">toodo this, add additional <Ad> elements toohello VAST file and specify hello order using hello sequence attribute.</span></span> <span data-ttu-id="4ff6f-144">Dit wordt geïllustreerd door Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="4ff6f-144">hello following example illustrates this:</span></span>

    <VAST version="2.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="oxml.xsd">
      <Ad id="1" sequence="0">
        <InLine>
          <AdSystem version="2.0 alpha">Atlas</AdSystem>
          <AdTitle>Unknown</AdTitle>
          <Description>Unknown</Description>
          <Survey></Survey>
          <Error></Error>
          <Impression id="Atlas"><![CDATA[http://myserver.com/Impression/Ad1trackingResouce]]></Impression>
          <Creatives>
            <Creative id="video" sequence="0" AdID="">
              <Linear>
                <Duration>00:00:32</Duration>
                <MediaFiles>
                  <!-- ... -->
                </MediaFiles>
              </Linear>
            </Creative>
          </Creatives>
        </InLine>
      </Ad>
      <Ad id="2" sequence="1">
        <InLine>
          <AdSystem version="2.0 alpha">Atlas</AdSystem>
          <AdTitle>Unknown</AdTitle>
          <Description>Unknown</Description>
          <Survey></Survey>
          <Error></Error>
          <Impression id="Atlas"><![CDATA[http://myserver.com/Impression/Ad2trackingResouce]]></Impression>
          <Creatives>
            <Creative id="video" sequence="0" AdID="">
              <Linear>
                <Duration>00:00:30</Duration>
                <MediaFiles>
                  <!-- ... -->
                </MediaFiles>
              </Linear>
            </Creative>
          </Creatives>
        </InLine>
      </Ad>
    </VAST>

<span data-ttu-id="4ff6f-145">Niet-lineaire advertenties zijn opgegeven in een <Creative> ook element.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-145">Nonlinear ads are specified in a <Creative> element as well.</span></span> <span data-ttu-id="4ff6f-146">Hallo volgende voorbeeld ziet u een <Creative> element dat een niet-lineaire ad beschrijft.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-146">hello following example shows a <Creative> element that describes a nonlinear ad.</span></span>

    <Creative id="video" sequence="1" AdID="">
      <NonLinearAds>
        <NonLinear width="216" height="121" minSuggestedDuration="00:00:15">
          <StaticResource creativeType="image/png"><![CDATA[http://myserver/images/image.png]]></StaticResource>
          <StaticResource creativeType="image/jpg"><![CDATA[http://myserver/images/image.jpg]]></StaticResource>
        </NonLinear>
        <TrackingEvents>
             <Tracking event="acceptInvitation"><![CDATA[http://myserver/tracking/trackingID]></Tracking>
             <Tracking event="collapse"><![CDATA[http://myserver/tracking/trackingID2]]></Tracking>
         </TrackingEvents>
       </NonLinearAds>
    </Creative>


<span data-ttu-id="4ff6f-147">Hallo <**NonLinearAds**>-element kan bevatten een of meer <**NonLinear**>-elementen, elk met een niet-lineaire ad kunt beschrijven.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-147">hello <**NonLinearAds**> element can contain one or more <**NonLinear**> elements, each of which can describe a nonlinear ad.</span></span> <span data-ttu-id="4ff6f-148">Hallo <**NonLinear**> element Hallo resource voor de niet-lineaire ad Hallo geeft.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-148">hello <**NonLinear**> element specifies hello resource for hello nonlinear ad.</span></span> <span data-ttu-id="4ff6f-149">Hallo-bron kan bestaan uit een <**StaticResouce**>, een <**IFrameResource**>, of een <**HTMLResouce**>.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-149">hello resource can be a <**StaticResouce**>, an <**IFrameResource**>, or an <**HTMLResouce**>.</span></span><span data-ttu-id="4ff6f-150"> <**StaticResource**> Beschrijving van een niet-HTML-bron en definieert een creativeType-kenmerk geeft aan hoe Hallo resource wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="4ff6f-150"> <**StaticResource**> describes a non-HTML resource and defines a creativeType attribute that specifies how hello resource is displayed:</span></span>

<span data-ttu-id="4ff6f-151">Afbeelding/GIF-, afbeelding/JPEG-, afbeelding/png – Hallo resource wordt weergegeven in een HTML-code <**img**> label.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-151">Image/gif, image/jpeg, image/png – hello resource is displayed in an HTML <**img**> tag.</span></span>

<span data-ttu-id="4ff6f-152">Toepassing/x-javascript – Hallo resource wordt weergegeven in een HTML-code <**script**> label.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-152">Application/x-javascript – hello resource is displayed in an HTML <**script**> tag.</span></span>

<span data-ttu-id="4ff6f-153">Toepassing/x-shockwave-flash-Hallo resource wordt weergegeven in een Flash player.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-153">Application/x-shockwave-flash – hello resource is displayed in a Flash player.</span></span>

<span data-ttu-id="4ff6f-154">**IFrameResource** een HTML-bron die kan worden weergegeven in een IFrame worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-154">**IFrameResource** describes an HTML resource that can be displayed in an IFrame.</span></span> <span data-ttu-id="4ff6f-155">**HTMLResource** beschrijft een stukje HTML-code die kan worden ingevoegd in een webpagina.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-155">**HTMLResource** describes a piece of HTML code that can be inserted into a web page.</span></span> <span data-ttu-id="4ff6f-156">**TrackingEvents** Geef gebeurtenissen bijhouden en URI toorequest Hallo Hallo-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-156">**TrackingEvents** specify tracking events and hello URI toorequest when hello event occurs.</span></span> <span data-ttu-id="4ff6f-157">In dit voorbeeld Hallo worden acceptInvitation en samenvouwen gebeurtenissen bijgehouden.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-157">In this sample hello acceptInvitation and collapse events are tracked.</span></span> <span data-ttu-id="4ff6f-158">Voor meer informatie over Hallo **NonLinearAds** -element en de onderliggende items, Zie IAB.NET/VAST.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-158">For more information on hello **NonLinearAds** element and its children, see IAB.NET/VAST.</span></span> <span data-ttu-id="4ff6f-159">Houd er rekening mee dat Hallo **TrackingEvents** element zich bevindt binnen Hallo **NonLinearAds** element in plaats van Hallo **NonLinear** element.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-159">Note that hello **TrackingEvents** element is located within hello **NonLinearAds** element rather than hello **NonLinear** element.</span></span>

<span data-ttu-id="4ff6f-160">Aanvullende advertenties zijn gedefinieerd binnen een <CompanionAds> element.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-160">Companion ads are defined within a <CompanionAds> element.</span></span> <span data-ttu-id="4ff6f-161">Hallo <CompanionAds> element kan bevatten een of meer <Companion> elementen.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-161">hello <CompanionAds> element can contain one or more <Companion> elements.</span></span> <span data-ttu-id="4ff6f-162">Elke <Companion> element beschrijft een aanvullende ad en bevatten een <StaticResource>, <IFrameResource>, of <HTMLResource> die zijn opgegeven dezelfde manier als in een niet-lineaire ad Hallo.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-162">Each <Companion> element describes a companion ad and can contain a <StaticResource>, <IFrameResource>, or <HTMLResource> which are specified in hello same way as in a nonlinear ad.</span></span> <span data-ttu-id="4ff6f-163">Een groot bestand meerdere companion-advertenties kan bevatten en spelertoepassing Hallo Hallo meest geschikte ad toodisplay kunt kiezen.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-163">A VAST file can contain multiple companion ads and hello player application can choose hello most appropriate ad toodisplay.</span></span> <span data-ttu-id="4ff6f-164">Zie voor meer informatie over VAST [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).</span><span class="sxs-lookup"><span data-stu-id="4ff6f-164">For more information about VAST, see [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).</span></span>

### <a name="using-a-digital-video-multiple-ad-playlist-vmap-file"></a><span data-ttu-id="4ff6f-165">Met behulp van een digitale Video meerdere Ad afspeellijst (VMAP)-bestand</span><span class="sxs-lookup"><span data-stu-id="4ff6f-165">Using a Digital Video Multiple Ad Playlist (VMAP) File</span></span>
<span data-ttu-id="4ff6f-166">Een bestand VMAP kunt u toospecify wanneer ad onderbrekingen optreden, hoe lang elk einde is, hoeveel advertenties worden weergegeven binnen een einde en welke typen advertenties kunnen worden weergegeven tijdens een pauze.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-166">A VMAP file allows you toospecify when ad breaks occur, how long each break is, how many ads can be displayed within a break, and what types of ads may be displayed during a break.</span></span> <span data-ttu-id="4ff6f-167">Hallo in een voorbeeldbestand VMAP die een pauze van één ad definieert te volgen:</span><span class="sxs-lookup"><span data-stu-id="4ff6f-167">hello following in an example VMAP file that defines a single ad break:</span></span>

    <vmap:VMAP xmlns:vmap="http://www.iab.net/vmap-1.0" version="1.0">
      <vmap:AdBreak breakType="linear" breakId="mypre" timeOffset="start">
        <vmap:AdSource allowMultipleAds="true" followRedirects="true" id="1">
          <vmap:VASTData>
            <VAST version="2.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="oxml.xsd">
              <Ad id="115571748">
                <InLine>
                  <AdSystem version="2.0 alpha">Atlas</AdSystem>
                  <AdTitle>Unknown</AdTitle>
                  <Description>Unknown</Description>
                  <Survey></Survey>
                  <Error></Error>
                  <Impression id="Atlas"><![CDATA[http://view.atdmt.com/000/sview/115571748/direct;ai.201582527;vt.2/01/634364885739970673]]></Impression>
                  <Creatives>
                    <Creative id="video" sequence="0" AdID="">
                      <Linear>
                        <Duration>00:00:32</Duration>
                        <MediaFiles>
                          <MediaFile apiFramework="Windows Media" id="windows_progressive_200" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="200" width="400" height="300" type="video/x-ms-wmv">
                            <![CDATA[http://smf.blob.core.windows.net/samples/ads/media/XBOX_HD_DEMO_700_1_000_200_4x3.wmv]]>
                          </MediaFile>
                          <MediaFile apiFramework="Windows Media" id="windows_progressive_300" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="300" width="400" height="300" type="video/x-ms-wmv">
                            <![CDATA[http://smf.blob.core.windows.net/samples/ads/media/XBOX_HD_DEMO_700_2_000_300_4x3.wmv]]>
                          </MediaFile>
                          <MediaFile apiFramework="Windows Media" id="windows_progressive_500" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="500" width="400" height="300" type="video/x-ms-wmv">
                            <![CDATA[http://smf.blob.core.windows.net/samples/ads/media/XBOX_HD_DEMO_700_1_000_500_4x3.wmv]]>
                          </MediaFile>
                          <MediaFile apiFramework="Windows Media" id="windows_progressive_700" maintainAspectRatio="true" scaleable="true" delivery="progressive" bitrate="700" width="400" height="300" type="video/x-ms-wmv">
                            <![CDATA[http://smf.blob.core.windows.net/samples/ads/media/XBOX_HD_DEMO_700_2_000_700_4x3.wmv]]>
                          </MediaFile>
                        </MediaFiles>
                      </Linear>
                    </Creative>
                  </Creatives>
                </InLine>
              </Ad>
            </VAST>
          </vmap:VASTData>
        </vmap:AdSource>
        <vmap:TrackingEvents>
          <vmap:Tracking event="breakStart">
            http://MyServer.com/breakstart.gif
          </vmap:Tracking>
        </vmap:TrackingEvents>
      </vmap:AdBreak>
    </vmap:VMAP>

<span data-ttu-id="4ff6f-168">Een bestand VMAP begint met een <VMAP> element een of meer bevat <AdBreak> elementen, die elk een ad-einde definiëren.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-168">A VMAP file begins with a <VMAP> element that contains one or more <AdBreak> elements, each defining an ad break.</span></span> <span data-ttu-id="4ff6f-169">Elk ad-einde geeft een type einde, break-ID en time-offset.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-169">Each ad break specifies a break type, break ID, and time offset.</span></span> <span data-ttu-id="4ff6f-170">Hallo breakType kenmerk geeft Hallo type ad die kan worden afgespeeld tijdens Hallo pauze: lineaire, niet-lineaire, of weer te geven.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-170">hello breakType attribute specifies hello type of ad that can be played during hello break: linear, nonlinear, or display.</span></span> <span data-ttu-id="4ff6f-171">Advertenties weergeven tooVAST companion advertenties worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-171">Display ads map tooVAST companion ads.</span></span> <span data-ttu-id="4ff6f-172">Meer dan één ad-type kan worden opgegeven in een lijst met gescheiden door komma's (zonder spaties).</span><span class="sxs-lookup"><span data-stu-id="4ff6f-172">More than one ad type can be specified in a comma (no spaces) separated list.</span></span> <span data-ttu-id="4ff6f-173">Hallo breakID is een optionele id voor Hallo ad.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-173">hello breakID is an optional identifier for hello ad.</span></span> <span data-ttu-id="4ff6f-174">Hallo timeOffset geeft aan wanneer Hallo ad moet worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-174">hello timeOffset specifies when hello ad should be displayed.</span></span> <span data-ttu-id="4ff6f-175">Deze kan worden opgegeven in een van de volgende manieren Hallo:</span><span class="sxs-lookup"><span data-stu-id="4ff6f-175">It can be specified in one of hello following ways:</span></span>

1. <span data-ttu-id="4ff6f-176">Tijd in: mm: ss of hh:mm:ss.mmm indeling .mmm waar milliseconden is.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-176">Time – in hh:mm:ss or hh:mm:ss.mmm format where .mmm is milliseconds.</span></span> <span data-ttu-id="4ff6f-177">Hallo-waarde van dit kenmerk geeft de tijd Hallo vanaf Hallo Hallo video tijdlijn toohello begin van de ad-einde Hallo.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-177">hello value of this attribute specifies hello time from hello beginning of hello video timeline toohello beginning of hello ad break.</span></span>
2. <span data-ttu-id="4ff6f-178">Percentage – n % indeling waarbij n staat voor Hallo percentage Hallo video tijdlijn tooplay Hallo ad afspelen</span><span class="sxs-lookup"><span data-stu-id="4ff6f-178">Percentage – in n% format where n is hello percentage of hello video timeline tooplay before playing hello ad</span></span>
3. <span data-ttu-id="4ff6f-179">Beginnen of eindigen – geeft aan dat een advertentie moet worden weergegeven vóór of na de Hallo video is weergegeven.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-179">Start/End – specifies that an ad should be displayed before or after hello video has been displayed</span></span>
4. <span data-ttu-id="4ff6f-180">Plaats – Hallo volgorde van de ad-einden geeft als Hallo timing van Hallo ad einden onbekend, zoals live streamen is.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-180">Position – specifies hello order of ad breaks when hello timing of hello ad breaks is unknown, such as in live streaming.</span></span> <span data-ttu-id="4ff6f-181">Hallo-volgorde van elk ad-einde is opgegeven in Hallo #n indeling waarbij n staat voor een geheel getal 1 of hoger.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-181">hello order of each ad break is specified in hello #n format where n is an integer 1 or greater.</span></span> <span data-ttu-id="4ff6f-182">1 geeft aan dat Hallo ad moet worden afgespeeld op de eerste kans hello, 2 geeft Hallo ad moet op de tweede mogelijkheid Hallo enzovoort worden afgespeeld.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-182">1 signifies hello ad should be played at hello first opportunity, 2 signifies hello ad should be played at hello second opportunity and so on.</span></span>

<span data-ttu-id="4ff6f-183">Binnen Hallo <**AdBreak**> element er zijn <**AdSource**> element.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-183">Within hello <**AdBreak**> element there can be one <**AdSource**> element.</span></span> <span data-ttu-id="4ff6f-184">Hallo <**AdSource**>-element bevat Hallo volgende kenmerken:</span><span class="sxs-lookup"><span data-stu-id="4ff6f-184">hello <**AdSource**> element contains hello following attributes:</span></span>

1. <span data-ttu-id="4ff6f-185">-ID: Hiermee geeft u een id voor Hallo ad-bron</span><span class="sxs-lookup"><span data-stu-id="4ff6f-185">Id – specifies an identifier for hello ad source</span></span>
2. <span data-ttu-id="4ff6f-186">allowMultipleAds – een Booleaanse waarde die aangeeft of meerdere advertenties kunnen worden weergegeven tijdens het Hallo-ad-einde</span><span class="sxs-lookup"><span data-stu-id="4ff6f-186">allowMultipleAds – a Boolean value that specifies whether multiple ads can be displayed during hello ad break</span></span>
3. <span data-ttu-id="4ff6f-187">followRedirects: een optionele Booleaanse waarde waarmee wordt aangegeven als Hallo-speler moet naleven leidt binnen een ad-antwoord</span><span class="sxs-lookup"><span data-stu-id="4ff6f-187">followRedirects – an optional Boolean value that specifies if hello video player should honor redirects within an ad response</span></span>

<span data-ttu-id="4ff6f-188">Hallo <**AdSource**>-element Hallo player heeft een antwoord van de ad inline of een verwijzing tooan ad-antwoord.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-188">hello <**AdSource**> element provides hello player an inline ad response or a reference tooan ad response.</span></span> <span data-ttu-id="4ff6f-189">Het kan een van de volgende elementen Hallo bevatten:</span><span class="sxs-lookup"><span data-stu-id="4ff6f-189">It can contain one of hello following elements:</span></span>

* <span data-ttu-id="4ff6f-190"><VASTAdData>geeft dat een ENORME ad-antwoord is ingesloten in Hallo VMAP bestand</span><span class="sxs-lookup"><span data-stu-id="4ff6f-190"><VASTAdData> indicates a VAST ad response is embedded within hello VMAP file</span></span>
* <span data-ttu-id="4ff6f-191"><AdTagURI>een URI die verwijst naar een ad-antwoord van een ander systeem</span><span class="sxs-lookup"><span data-stu-id="4ff6f-191"><AdTagURI> a URI that references an ad response from another system</span></span>
* <span data-ttu-id="4ff6f-192"><CustomAdData>-een willekeurige tekenreeks die respresents een niet-VAST antwoord</span><span class="sxs-lookup"><span data-stu-id="4ff6f-192"><CustomAdData> -an arbitrary string that respresents a non-VAST response</span></span>

<span data-ttu-id="4ff6f-193">In dit voorbeeld wordt een in-line ad-antwoord opgegeven met een <VASTAdData> element dat een ENORME ad-antwoord bevat.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-193">In this example an in-line ad response is specified with a <VASTAdData> element that contains a VAST ad response.</span></span> <span data-ttu-id="4ff6f-194">Zie voor meer informatie over Hallo andere elementen [VMAP](http://www.iab.net/guidelines/508676/digitalvideo/vsuite/vmap).</span><span class="sxs-lookup"><span data-stu-id="4ff6f-194">For more information about hello other elements, see [VMAP](http://www.iab.net/guidelines/508676/digitalvideo/vsuite/vmap).</span></span>

<span data-ttu-id="4ff6f-195">Hallo <**AdBreak**>-element kan ook bevatten <**TrackingEvents**> element.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-195">hello <**AdBreak**> element can also contain one <**TrackingEvents**> element.</span></span> <span data-ttu-id="4ff6f-196">Hallo <**TrackingEvents**>-element kunt u tootrack Hallo begin of einde van een ad-einde of of is een fout opgetreden tijdens het Hallo-ad-einde.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-196">hello <**TrackingEvents**> element allows you tootrack hello start or end of an ad break or whether an error occurred during hello ad break.</span></span> <span data-ttu-id="4ff6f-197">Hallo <**TrackingEvents**>-element bevat een of meer <**bijhouden**>-elementen, die elk een gebeurtenis bijhouden en bijgehouden URI bevat.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-197">hello <**TrackingEvents**> element contains one or more <**Tracking**> elements, each of which specifies a tracking event and a tracking URI.</span></span> <span data-ttu-id="4ff6f-198">Hallo mogelijk bijhouden gebeurtenissen zijn:</span><span class="sxs-lookup"><span data-stu-id="4ff6f-198">hello possible tracking events are:</span></span>

1. <span data-ttu-id="4ff6f-199">breakStart – houdt Hallo begin van een ad-einde</span><span class="sxs-lookup"><span data-stu-id="4ff6f-199">breakStart – tracks hello beginning of an ad break</span></span>
2. <span data-ttu-id="4ff6f-200">breakEnd – bijhouden Hallo voltooiing van een ad-einde</span><span class="sxs-lookup"><span data-stu-id="4ff6f-200">breakEnd – track hello completion of an ad break</span></span>
3. <span data-ttu-id="4ff6f-201">Fout: een fout die is opgetreden tijdens het Hallo-ad-einde wordt bijgehouden</span><span class="sxs-lookup"><span data-stu-id="4ff6f-201">error – tracks an error that occurred during hello ad break</span></span>

<span data-ttu-id="4ff6f-202">Hallo volgende voorbeeld ziet u een bestand VMAP waarmee gebeurtenissen bijhouden</span><span class="sxs-lookup"><span data-stu-id="4ff6f-202">hello following example shows a VMAP file that specifies tracking events</span></span>

    <vmap:VMAP xmlns:vmap="http://www.iab.net/vmap-1.0" version="1.0">
      <vmap:AdBreak breakType="linear" breakId="mypre" timeOffset="start">
        <vmap:AdSource allowMultipleAds="true" followRedirects="true" id="1">
          <vmap:VASTData>
            <!--Inline VAST -->
          </vmap:VASTData>
        </vmap:AdSource>
        <vmap:TrackingEvents>
          <vmap:Tracking event="breakStart">
            http://MyServer.com/breakstart.gif
          </vmap:Tracking>
          <vmap:Tracking event="breakend">
            http://MyServer.com/breakend.gif
          </vmap:Tracking>
          <vmap:Tracking event="error">
            http://MyServer.com/error.gif
          </vmap:Tracking>
        </vmap:TrackingEvents>
      </vmap:AdBreak>
    </vmap:VMAP>

<span data-ttu-id="4ff6f-203">Voor meer informatie over Hallo <**TrackingEvents**>-element en de onderliggende items, Zie http://iab.org/VMAP.pdf</span><span class="sxs-lookup"><span data-stu-id="4ff6f-203">For more information on hello <**TrackingEvents**> element and its children, see http://iab.org/VMAP.pdf</span></span>

### <a name="using-a-media-abstract-sequencing-template-mast-file"></a><span data-ttu-id="4ff6f-204">Met behulp van een Media Abstract sequentiëren sjabloonbestand (b)</span><span class="sxs-lookup"><span data-stu-id="4ff6f-204">Using a Media Abstract Sequencing Template (MAST) File</span></span>
<span data-ttu-id="4ff6f-205">Een bestand b kunt u toospecify triggers die bepalen wanneer een advertentie wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-205">A MAST file allows you toospecify triggers that define when an ad is displayed.</span></span> <span data-ttu-id="4ff6f-206">Hallo Hieronder volgt een voorbeeld van de b-bestand met triggers voor een pre-album ad, een tussentijdse roll ad en een advertentie na doorvoeren.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-206">hello following is an example MAST file that contains triggers for a pre roll ad, a mid-roll ad, and a post-roll ad.</span></span>

    <MAST xsi:schemaLocation="http://openvideoplayer.sf.net/mast http://openvideoplayer.sf.net/mast/mast.xsd" xmlns="http://openvideoplayer.sf.net/mast" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
      <triggers>
        <trigger id="preroll" description="preroll every item"  >
          <startConditions>
            <condition type="event" name="OnItemStart" />
          </startConditions>
          <sources>
            <source uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" format="vast">
              <sources />
            </source>
          </sources>
        </trigger>

        <trigger id="midroll" description="midroll at 15 sec."  >
          <startConditions>
            <condition type="property" name="Position" value="00:00:15.0" operator="GEQ" />
          </startConditions>
          <endConditions>
            <condition type="event" name="OnItemEnd"/>
            <!--This 'resets' hello trigger for hello next clip-->
          </endConditions>
          <sources>
            <source uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" format="vast">
              <sources />
            </source>
          </sources>
        </trigger>

        <trigger id="postroll" description="postroll"  >
          <startConditions>
            <condition type="event" name="OnItemEnd"/>
          </startConditions>
          <sources>
            <source uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" format="vast">
              <sources />
            </source>
          </sources>
        </trigger>
      </triggers>
    </MAST>



<span data-ttu-id="4ff6f-207">Een bestand b begint met een **b** element met een **triggers** element.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-207">A MAST file begins with a **MAST** element that contains one **triggers** element.</span></span> <span data-ttu-id="4ff6f-208">Hallo <triggers> element bevat een of meer **trigger** elementen die bepalen wanneer een advertentie moet worden afgespeeld.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-208">hello <triggers> element contains one or more **trigger** elements that define when an ad should be played.</span></span> 

<span data-ttu-id="4ff6f-209">Hallo **trigger** element bevat een **startConditions** element die opgeven wanneer een advertentie moet beginnen met het tooplay.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-209">hello **trigger** element contains a **startConditions** element which specify when an ad should begin tooplay.</span></span> <span data-ttu-id="4ff6f-210">Hallo **startConditions** element bevat een of meer <condition> elementen.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-210">hello **startConditions** element contains one or more <condition> elements.</span></span> <span data-ttu-id="4ff6f-211">Wanneer elke <condition> tootrue een trigger wordt gestart of ingetrokken, afhankelijk van of evalueert Hallo <condition> is opgenomen in een **startConditions** of **endConditions** element respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-211">When each <condition> evaluates tootrue a trigger is initiated or revoked depending upon whether hello <condition> is contained within a **startConditions** or **endConditions** element respectively.</span></span> <span data-ttu-id="4ff6f-212">Wanneer meerdere <condition> elementen aanwezig zijn, worden deze behandeld als een impliciete OR, elke voorwaarde evalueren tootrue zullen Hallo trigger tooinitiate.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-212">When multiple <condition> elements are present, they are treated as an implicit OR, any condition evaluating tootrue will cause hello trigger tooinitiate.</span></span> <span data-ttu-id="4ff6f-213"><condition>elementen kunnen worden genest.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-213"><condition> elements can be nested.</span></span> <span data-ttu-id="4ff6f-214">Als onderliggende <condition> elementen zijn vooraf ingesteld, worden deze behandeld als een impliciete AND, alle voorwaarden tootrue voor Hallo trigger tooinitiate moeten worden geëvalueerd.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-214">When child <condition> elements are preset, they are treated as an implicit AND, all conditions must evaluate tootrue for hello trigger tooinitiate.</span></span> <span data-ttu-id="4ff6f-215">Hallo <condition> element Hallo kenmerken die Hallo voorwaarde definiëren volgende bevat:</span><span class="sxs-lookup"><span data-stu-id="4ff6f-215">hello <condition> element contains hello following attributes that define hello condition:</span></span> 

1. <span data-ttu-id="4ff6f-216">**type** – Hiermee geeft u Hallo type voorwaarde, gebeurtenis of eigenschap</span><span class="sxs-lookup"><span data-stu-id="4ff6f-216">**type** – specifies hello type of condition, event or property</span></span>
2. <span data-ttu-id="4ff6f-217">**naam** – hello naam van het Hallo-eigenschap of gebeurtenis toobe gebruikt tijdens de evaluatie</span><span class="sxs-lookup"><span data-stu-id="4ff6f-217">**name** – hello name of hello property or event toobe used during evaluation</span></span>
3. <span data-ttu-id="4ff6f-218">**waarde** – Hallo-waarde die een eigenschap worden geëvalueerd</span><span class="sxs-lookup"><span data-stu-id="4ff6f-218">**value** – hello value that a property will be evaluated against</span></span>
4. <span data-ttu-id="4ff6f-219">**operator** – bewerking toouse Hallo tijdens de evaluatie: EQ (equal), NEQ (niet gelijk aan), GTR (groter), GEQ (groter of gelijk zijn), LT (minder dan), LEQ (kleiner dan of gelijk aan), MOD (modulo)</span><span class="sxs-lookup"><span data-stu-id="4ff6f-219">**operator** – hello operation toouse during evaluation: EQ (equal), NEQ (not equal), GTR (greater), GEQ (greater or equal), LT (Less than), LEQ (less than or equal), MOD (modulo)</span></span>

<span data-ttu-id="4ff6f-220">**endConditions** bevat ook <condition> elementen.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-220">**endConditions** also contain <condition> elements.</span></span> <span data-ttu-id="4ff6f-221">Wanneer een voorwaarde wordt geëvalueerd tootrue Hallo trigger reset.hello is <trigger> element bevat ook een <sources> element een of meer bevat <source> elementen.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-221">When a condition evaluates tootrue hello trigger is reset.hello <trigger> element also contains a <sources> element that contains one or more <source> elements.</span></span> <span data-ttu-id="4ff6f-222">Hallo <source> elementen Hallo URI toohello ad antwoord en Hallo-type van ad-antwoord definiëren.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-222">hello <source> elements define hello URI toohello ad response and hello type of ad response.</span></span> <span data-ttu-id="4ff6f-223">In dit voorbeeld wordt een URI tooa VAST antwoord gegeven.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-223">In this example a URI is given tooa VAST response.</span></span> 

    <trigger id="postroll" description="postroll"  >
      <startConditions>
        <condition/>
      </startConditions>
      <sources>
        <source uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" format="vast">
          <sources />
        </source>
      </sources>
    </trigger>


### <a name="using-video-player-ad-interface-definition-vpaid"></a><span data-ttu-id="4ff6f-224">Met behulp van Video Player-Ad-Interface Definition (VPAID)</span><span class="sxs-lookup"><span data-stu-id="4ff6f-224">Using Video Player-Ad Interface Definition (VPAID)</span></span>
<span data-ttu-id="4ff6f-225">VPAID is een API voor het inschakelen van uitvoerbare ad eenheden toocommunicate met een video-speler.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-225">VPAID is an API for enabling executable ad units toocommunicate with a video player.</span></span> <span data-ttu-id="4ff6f-226">Hiermee worden interactieve ad-ervaringen.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-226">This allows highly interactive ad experiences.</span></span> <span data-ttu-id="4ff6f-227">Hallo-gebruiker kan communiceren met de Hallo ad en Hallo ad tooactions genomen door Hallo viewer kan reageren.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-227">hello user can interact with hello ad and hello ad can respond tooactions taken by hello viewer.</span></span> <span data-ttu-id="4ff6f-228">Zo kan een ad knoppen waarmee Hallo gebruiker tooview meer informatie of een langere versie van Hallo ad weergeven.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-228">For example an ad may display buttons that allow hello user tooview more information or a longer version of hello ad.</span></span> <span data-ttu-id="4ff6f-229">Hallo-speler Hallo VPAID API moet ondersteunen en uitvoerbare ad Hallo Hallo API moet implementeren.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-229">hello video player must support hello VPAID API and hello executable ad must implement hello API.</span></span> <span data-ttu-id="4ff6f-230">Wanneer een speler een advertentie aanvragen van een ad-server Hallo-server reageert met een ENORME antwoord dat een advertentie VPAID bevat.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-230">When a player requests an ad from an ad server hello server may respond with a VAST response that contains a VPAID ad.</span></span>

<span data-ttu-id="4ff6f-231">Een uitvoerbaar ad wordt gemaakt in de code die moet worden uitgevoerd in een runtime-omgeving, zoals Adobe Flash™ of JavaScript die kan worden uitgevoerd in een webbrowser.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-231">An executable ad is created in code that must be executed in a runtime environment such as Adobe Flash™ or JavaScript that can be executed in a web browser.</span></span> <span data-ttu-id="4ff6f-232">Wanneer een ad-server een ENORME antwoord met een ad VPAID retourneert, waarde van Hallo apiFramework kenmerk in Hallo Hallo <MediaFile> element moet 'VPAID'.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-232">When an ad server returns a VAST response containing a VPAID ad, hello value of hello apiFramework attribute in hello <MediaFile> element must be “VPAID”.</span></span> <span data-ttu-id="4ff6f-233">Dit kenmerk geeft aan dat ad Hallo bevat een VPAID uitvoerbare ad.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-233">This attribute specifies that hello contained ad is a VPAID executable ad.</span></span> <span data-ttu-id="4ff6f-234">kenmerk van het type Hallo moet worden ingesteld toohello MIME-type van Hallo uitvoerbare bestand, zoals ' application/x-shockwave-flash' of ' application/x-javascript'.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-234">hello type attribute must be set toohello MIME type of hello executable, such as “application/x-shockwave-flash” or “application/x-javascript”.</span></span> <span data-ttu-id="4ff6f-235">Hallo volgende XML-fragment toont Hallo <MediaFile> element uit een ENORME antwoord met een VPAID uitvoerbare ad.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-235">hello following XML snippet shows hello <MediaFile> element from a VAST response containing a VPAID executable ad.</span></span> 

    <MediaFiles>
       <MediaFile id="1" delivery="progressive" type=”application/x-shockwaveflash”
                  width=”640” height=”480” apiFramework=”VPAID”>
           <!-- CDATA wrapped URI tooexecutable ad -->
       </MediaFile>
    </MediaFiles>


<span data-ttu-id="4ff6f-236">Een uitvoerbaar ad kan worden geïnitialiseerd met behulp van Hallo <AdParameters> element in Hallo <Linear> of <NonLinear> elementen in een antwoord VAST.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-236">An executable ad can be initialized using hello <AdParameters> element within hello <Linear> or <NonLinear> elements in a VAST response.</span></span> <span data-ttu-id="4ff6f-237">Voor meer informatie over Hallo <AdParameters> element, Zie [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).</span><span class="sxs-lookup"><span data-stu-id="4ff6f-237">For more information on hello <AdParameters> element, see [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).</span></span> <span data-ttu-id="4ff6f-238">Zie voor meer informatie over Hallo VPAID API [VPAID 2.0](http://www.iab.net/media/file/VPAID_2.0_Final_04-10-2012.pdf).</span><span class="sxs-lookup"><span data-stu-id="4ff6f-238">For more information about hello VPAID API, see [VPAID 2.0](http://www.iab.net/media/file/VPAID_2.0_Final_04-10-2012.pdf).</span></span>

## <a name="implementing-a-windows-or-windows-phone-8-player-with-ad-support"></a><span data-ttu-id="4ff6f-239">Implementatie van een Windows- of Windows Phone 8-speler met Ad-ondersteuning</span><span class="sxs-lookup"><span data-stu-id="4ff6f-239">Implementing a Windows or Windows Phone 8 Player with Ad Support</span></span>
<span data-ttu-id="4ff6f-240">Hallo Microsoft Media-Platform: Player Framework voor Windows 8 en Windows Phone 8 bevat een verzameling voorbeeldtoepassingen die u laten zien hoe tooimplement wordt gebruikt door een video player toepassing hello framework.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-240">hello Microsoft Media Platform: Player Framework for Windows 8 and Windows Phone 8 contains a collection of sample applications that show you how tooimplement a video player application using hello framework.</span></span> <span data-ttu-id="4ff6f-241">U kunt downloaden Hallo Player Framework en Hallo-voorbeelden van [Player Framework voor Windows 8 en Windows Phone 8](https://playerframework.codeplex.com).</span><span class="sxs-lookup"><span data-stu-id="4ff6f-241">You can download hello Player Framework and hello samples from [Player Framework for Windows 8 and Windows Phone 8](https://playerframework.codeplex.com).</span></span>

<span data-ttu-id="4ff6f-242">Wanneer u Hallo Microsoft.PlayerFramework.Xaml.Samples oplossing opent ziet u een aantal mappen van Hallo-project.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-242">When you open hello Microsoft.PlayerFramework.Xaml.Samples solution you will see a number of folders within hello project.</span></span> <span data-ttu-id="4ff6f-243">Hallo reclame map bevat Hallo voorbeeld code relevante toocreating een video-speler met ad-ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-243">hello Advertising folder contains hello sample code relevant toocreating a video player with ad support.</span></span> <span data-ttu-id="4ff6f-244">Binnen Hallo reclame map is een aantal XAML/cs hoe elk van die bestanden tooinsert advertenties in een andere manier.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-244">Inside hello Advertising folder is a number of XAML/cs files each of which show how tooinsert ads in a different way.</span></span> <span data-ttu-id="4ff6f-245">Hallo volgende lijst beschrijft elke:</span><span class="sxs-lookup"><span data-stu-id="4ff6f-245">hello following list describes each:</span></span>

* <span data-ttu-id="4ff6f-246">AdPodPage.xaml ziet u hoe een advertentie toodisplay schil.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-246">AdPodPage.xaml Shows how toodisplay an ad pod.</span></span>
* <span data-ttu-id="4ff6f-247">AdSchedulingPage.xaml toont hoe tooschedule advertenties.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-247">AdSchedulingPage.xaml Shows how tooschedule ads.</span></span>
* <span data-ttu-id="4ff6f-248">FreeWheelPage.xaml ziet u hoe toouse Hallo FreeWheel invoegtoepassing tooschedule advertenties.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-248">FreeWheelPage.xaml Shows how toouse hello FreeWheel plugin tooschedule ads.</span></span>
* <span data-ttu-id="4ff6f-249">MastPage.xaml toont hoe tooschedule advertenties met een b-bestand.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-249">MastPage.xaml Shows how tooschedule ads with a MAST file.</span></span>
* <span data-ttu-id="4ff6f-250">ProgrammaticAdPage.xaml ziet u hoe tooprogrammatically advertenties plannen in een video.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-250">ProgrammaticAdPage.xaml Shows how tooprogrammatically schedule ads into a video.</span></span>
* <span data-ttu-id="4ff6f-251">ScheduleClipPage.xaml toont hoe tooschedule een advertentie zonder een groot bestand.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-251">ScheduleClipPage.xaml Shows how tooschedule an ad without a VAST file.</span></span>
* <span data-ttu-id="4ff6f-252">VastLinearCompanionPage.xaml toont hoe een lineaire tooinsert en aanvullende ad.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-252">VastLinearCompanionPage.xaml Shows how tooinsert a linear and companion ad.</span></span>
* <span data-ttu-id="4ff6f-253">VastNonLinearPage.xaml toont hoe tooinsert een niet-lineaire ad.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-253">VastNonLinearPage.xaml Shows how tooinsert a non-linear ad.</span></span>
* <span data-ttu-id="4ff6f-254">VmapPage.xaml toont hoe toospecify advertenties met een VMAP-bestand.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-254">VmapPage.xaml Shows how toospecify ads with a VMAP file.</span></span>

<span data-ttu-id="4ff6f-255">Elk van deze voorbeelden Hallo Media Player klasse is gedefinieerd door Hallo player-framework gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-255">Each of these samples uses hello MediaPlayer class defined by hello player framework.</span></span> <span data-ttu-id="4ff6f-256">De meeste voorbeelden gebruiken invoegtoepassingen die ondersteuning voor verschillende indelingen met ad-antwoord toevoegen.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-256">Most samples use plugins that add support for various ad response formats.</span></span> <span data-ttu-id="4ff6f-257">Hallo ProgrammaticAdPage voorbeeld communiceert via een programma met een exemplaar van de Media Player.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-257">hello ProgrammaticAdPage sample programmatically interacts with a MediaPlayer instance.</span></span>

### <a name="adpodpage-sample"></a><span data-ttu-id="4ff6f-258">Voorbeeld van AdPodPage</span><span class="sxs-lookup"><span data-stu-id="4ff6f-258">AdPodPage Sample</span></span>
<span data-ttu-id="4ff6f-259">In dit voorbeeld gebruikt Hallo AdSchedulerPlugin toodefine wanneer toodisplay een advertentie.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-259">This sample uses hello AdSchedulerPlugin toodefine when toodisplay an ad.</span></span> <span data-ttu-id="4ff6f-260">In dit voorbeeld is een aankondiging halverwege roll geplande toobe afgespeeld na 5 seconden.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-260">In this example a mid-roll advertisement is scheduled toobe played after 5 seconds.</span></span> <span data-ttu-id="4ff6f-261">Hallo ad schil (een groep van advertenties toodisplay in volgorde) is opgegeven in een ENORME bestand geretourneerd van een ad-server.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-261">hello ad pod (a group of ads toodisplay in order) is specified in a VAST file returned from an ad server.</span></span> <span data-ttu-id="4ff6f-262">Hallo URI toohello VAST bestand is opgegeven in Hallo <RemoteAdSource> element.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-262">hello URI toohello VAST file is specified in hello <RemoteAdSource> element.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">

        <mmppf:MediaPlayer.Plugins>
            <ads:AdSchedulerPlugin>
                <ads:AdSchedulerPlugin.Advertisements>

                    <ads:MidrollAdvertisement Time="00:00:05">
                        <ads:MidrollAdvertisement.Source>
                            <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_adpod.xml" Type="vast"/>
                        </ads:MidrollAdvertisement.Source>
                    </ads:MidrollAdvertisement>

                </ads:AdSchedulerPlugin.Advertisements>
            </ads:AdSchedulerPlugin>
            <ads:AdHandlerPlugin/>
        </mmppf:MediaPlayer.Plugins>
    </mmppf:MediaPlayer>

<span data-ttu-id="4ff6f-263">Zie voor meer informatie over Hallo AdSchedulerPlugin [reclame in Hallo Player Framework op Windows 8 en Windows Phone 8](http://playerframework.codeplex.com/wikipage?title=Advertising&referringTitle=Windows%208%20Player%20Documentation)</span><span class="sxs-lookup"><span data-stu-id="4ff6f-263">For more information about hello AdSchedulerPlugin, see [Advertising in hello Player Framework on Windows 8 and Windows Phone 8](http://playerframework.codeplex.com/wikipage?title=Advertising&referringTitle=Windows%208%20Player%20Documentation)</span></span>

### <a name="adschedulingpage"></a><span data-ttu-id="4ff6f-264">AdSchedulingPage</span><span class="sxs-lookup"><span data-stu-id="4ff6f-264">AdSchedulingPage</span></span>
<span data-ttu-id="4ff6f-265">Dit voorbeeld gebruikt ook Hallo AdSchedulerPlugin.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-265">This sample also uses hello AdSchedulerPlugin.</span></span> <span data-ttu-id="4ff6f-266">Hiermee plant u drie advertenties, een vooraf roll ad, een tussentijdse roll ad en een advertentie na doorvoeren.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-266">It schedules three ads, a pre-roll ad, a mid-roll ad, and a post-roll ad.</span></span> <span data-ttu-id="4ff6f-267">Hallo URI toohello VAST voor elke advertentie is opgegeven in een <RemoteAdSource> element.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-267">hello URI toohello VAST for each ad is specified in a <RemoteAdSource> element.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:AdSchedulerPlugin>
                        <ads:AdSchedulerPlugin.Advertisements>

                            <ads:PrerollAdvertisement>
                                <ads:PrerollAdvertisement.Source>
                                    <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" Type="vast"/>
                                </ads:PrerollAdvertisement.Source>
                            </ads:PrerollAdvertisement>

                            <ads:MidrollAdvertisement Time="00:00:15">
                                <ads:MidrollAdvertisement.Source>
                                    <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" Type="vast"/>
                                </ads:MidrollAdvertisement.Source>
                            </ads:MidrollAdvertisement>

                            <ads:PostrollAdvertisement>
                                <ads:PostrollAdvertisement.Source>
                                    <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" Type="vast"/>
                                </ads:PostrollAdvertisement.Source>
                            </ads:PostrollAdvertisement>

                        </ads:AdSchedulerPlugin.Advertisements>
                    </ads:AdSchedulerPlugin>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>


### <a name="freewheelpage"></a><span data-ttu-id="4ff6f-268">FreeWheelPage</span><span class="sxs-lookup"><span data-stu-id="4ff6f-268">FreeWheelPage</span></span>
<span data-ttu-id="4ff6f-269">Dit voorbeeld gebruikt Hallo FreeWheelPlugin waarin een kenmerk van de gegevensbron waarmee een URI die punten tooa SmartXML-bestand dat Hiermee geeft u de ad-inhoud, evenals gegevens over de planning van ad.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-269">This sample uses hello FreeWheelPlugin which specifies a Source attribute that specifies a URI that points tooa SmartXML file that specifies ad content as well as ad scheduling information.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:FreeWheelPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/freewheel.xml"/>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="mastpage"></a><span data-ttu-id="4ff6f-270">MastPage</span><span class="sxs-lookup"><span data-stu-id="4ff6f-270">MastPage</span></span>
<span data-ttu-id="4ff6f-271">Dit voorbeeld gebruikt Hallo MastSchedulerPlugin waarmee u toouse een b-bestand.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-271">This sample uses hello MastSchedulerPlugin that allows you toouse a MAST file.</span></span> <span data-ttu-id="4ff6f-272">Hallo bronkenmerk geeft Hallo-locatie van Hallo b-bestand.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-272">hello Source attribute specifies hello location of hello MAST file.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:MastSchedulerPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/mast.xml" />
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="programmaticadpage"></a><span data-ttu-id="4ff6f-273">ProgrammaticAdPage</span><span class="sxs-lookup"><span data-stu-id="4ff6f-273">ProgrammaticAdPage</span></span>
<span data-ttu-id="4ff6f-274">Dit voorbeeld communiceert via een programma met Hallo Media Player.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-274">This sample programmatically interacts with hello MediaPlayer.</span></span> <span data-ttu-id="4ff6f-275">Hallo ProgrammaticAdPage.xaml bestand instantieert Hallo Media Player:</span><span class="sxs-lookup"><span data-stu-id="4ff6f-275">hello ProgrammaticAdPage.xaml file instantiates hello MediaPlayer:</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4"/>

<span data-ttu-id="4ff6f-276">Hallo ProgrammaticAdPage.xaml.cs bestand een AdHandlerPlugin maakt, voegt een toospecify TimelineMarker wanneer een advertentie moet worden weergegeven en vervolgens een handler voor Hallo MarkerReached gebeurtenis die een RemoteAdSource opgeven van een URI tooa VAST bestand worden geladen en vervolgens speelt toegevoegd Hallo ad.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-276">hello ProgrammaticAdPage.xaml.cs file creates an AdHandlerPlugin, adds a TimelineMarker toospecify when an ad should be displayed, and then adds a handler for hello MarkerReached event which loads a RemoteAdSource specifying a URI tooa VAST file, and then plays hello ad.</span></span>

    public sealed partial class ProgrammaticAdPage : Microsoft.PlayerFramework.Samples.Common.LayoutAwarePage
        {
            AdHandlerPlugin adHandler;

            public ProgrammaticAdPage()
            {
                this.InitializeComponent();
                adHandler = new AdHandlerPlugin();
                player.Plugins.Add(new AdHandlerPlugin());
                player.Markers.Add(new TimelineMarker() { Time = TimeSpan.FromSeconds(5), Type = "myAd" });
                player.MarkerReached += pf_MarkerReached;
            }

            async void pf_MarkerReached(object sender, TimelineMarkerRoutedEventArgs e)
            {
                if (e.Marker.Type == "myAd")
                {
                    var adSource = new RemoteAdSource() { Type = VastAdPayloadHandler.AdType, Uri = new Uri("http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml") };
                    //var adSource = new AdSource() { Type = DocumentAdPayloadHandler.AdType, Payload = SampleAdDocument };
                    var progress = new Progress<AdStatus>();
                    try
                    {
                        await player.PlayAd(adSource, progress, CancellationToken.None);
                    }
                    catch { /* ignore */ }
                }
            }

### <a name="scheduleclippage"></a><span data-ttu-id="4ff6f-277">ScheduleClipPage</span><span class="sxs-lookup"><span data-stu-id="4ff6f-277">ScheduleClipPage</span></span>
<span data-ttu-id="4ff6f-278">Dit voorbeeld gebruikt Hallo AdSchedulerPlugin tooschedule een advertentie halverwege roll door te geven van een WMV-bestand met de Hallo ad.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-278">This sample uses hello AdSchedulerPlugin tooschedule a mid-roll ad by specifying a .wmv file that contains hello ad.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.cloudapp.net/html5/media/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:AdSchedulerPlugin>
                        <ads:AdSchedulerPlugin.Advertisements>

                            <ads:MidrollAdvertisement Time="00:00:05">
                                <ads:MidrollAdvertisement.Source>
                                    <ads:AdSource Type="clip">
                                        <ads:AdSource.Payload>
                                            <ads:ClipAdPayload MediaSource="http://smf.blob.core.windows.net/samples/ads/media/XBOX_HD_DEMO_700_2_000_700_4x3.wmv" MimeType="video/x-ms-wmv" />
                                        </ads:AdSource.Payload>
                                    </ads:AdSource>
                                </ads:MidrollAdvertisement.Source>
                            </ads:MidrollAdvertisement>

                        </ads:AdSchedulerPlugin.Advertisements>
                    </ads:AdSchedulerPlugin>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="vastlinearcompanionpage"></a><span data-ttu-id="4ff6f-279">VastLinearCompanionPage</span><span class="sxs-lookup"><span data-stu-id="4ff6f-279">VastLinearCompanionPage</span></span>
<span data-ttu-id="4ff6f-280">Dit voorbeeld ziet u hoe toouse Hallo AdSchedulerPlugin tooschedule een lineaire ad halverwege rollen met een aanvullende ad.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-280">This sample illustrates how toouse hello AdSchedulerPlugin tooschedule a mid-roll linear ad with an companion ad.</span></span> <span data-ttu-id="4ff6f-281">Hallo <RemoteAdSource> element Hallo-locatie van de ENORME bestand Hallo geeft.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-281">hello <RemoteAdSource> element specifies hello location of hello VAST file.</span></span>

    <mmppf:MediaPlayer Grid.Row="1"  x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:AdSchedulerPlugin>
                        <ads:AdSchedulerPlugin.Advertisements>

                            <ads:MidrollAdvertisement Time="00:00:05">
                                <ads:MidrollAdvertisement.Source>
                                    <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear_companions.xml" Type="vast"/>
                                </ads:MidrollAdvertisement.Source>
                            </ads:MidrollAdvertisement>

                        </ads:AdSchedulerPlugin.Advertisements>
                    </ads:AdSchedulerPlugin>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="vastlinearnonlinearpage"></a><span data-ttu-id="4ff6f-282">VastLinearNonLinearPage</span><span class="sxs-lookup"><span data-stu-id="4ff6f-282">VastLinearNonLinearPage</span></span>
<span data-ttu-id="4ff6f-283">Dit voorbeeld gebruikt Hallo AdSchedulerPlugin tooschedule een lineaire en een niet-lineaire ad.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-283">This sample uses hello AdSchedulerPlugin tooschedule a linear and a non-linear ad.</span></span> <span data-ttu-id="4ff6f-284">Hallo VAST bestandslocatie is opgegeven met de Hallo <RemoteAdSource> element.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-284">hello VAST file location is specified with hello <RemoteAdSource> element.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:AdSchedulerPlugin>
                        <ads:AdSchedulerPlugin.Advertisements>

                            <ads:MidrollAdvertisement Time="00:00:05">
                                <ads:MidrollAdvertisement.Source>
                                    <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear_nonlinear.xml" Type="vast"/>
                                </ads:MidrollAdvertisement.Source>
                            </ads:MidrollAdvertisement>

                        </ads:AdSchedulerPlugin.Advertisements>
                    </ads:AdSchedulerPlugin>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="vmappage"></a><span data-ttu-id="4ff6f-285">VMAPPage</span><span class="sxs-lookup"><span data-stu-id="4ff6f-285">VMAPPage</span></span>
<span data-ttu-id="4ff6f-286">Hallo VmapSchedulerPlugin tooschedule advertenties met behulp van een bestand VMAP maakt gebruik van deze voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-286">This samples uses hello VmapSchedulerPlugin tooschedule ads using a VMAP file.</span></span> <span data-ttu-id="4ff6f-287">Hallo URI toohello VMAP bestand is opgegeven in het bronkenmerk Hallo Hallo <VmapSchedulerPlugin> element.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-287">hello URI toohello VMAP file is specified in hello Source attribute of hello <VmapSchedulerPlugin> element.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:VmapSchedulerPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/vmap.xml"/>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

## <a name="implementing-an-ios-video-player-with-ad-support"></a><span data-ttu-id="4ff6f-288">Implementatie van een iOS-Video Player met Ad-ondersteuning</span><span class="sxs-lookup"><span data-stu-id="4ff6f-288">Implementing an iOS Video Player with Ad Support</span></span>
<span data-ttu-id="4ff6f-289">Hallo Microsoft Media-Platform: Player Framework voor iOS bevat een verzameling voorbeeldtoepassingen die u laten zien hoe tooimplement wordt gebruikt door een video player toepassing hello framework.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-289">hello Microsoft Media Platform: Player Framework for iOS contains a collection of sample applications that show you how tooimplement a video player application using hello framework.</span></span> <span data-ttu-id="4ff6f-290">U kunt downloaden Hallo Player Framework en Hallo-voorbeelden van [Azure Media Player Framework](https://github.com/Azure/azure-media-player-framework).</span><span class="sxs-lookup"><span data-stu-id="4ff6f-290">You can download hello Player Framework and hello samples from [Azure Media Player Framework](https://github.com/Azure/azure-media-player-framework).</span></span> <span data-ttu-id="4ff6f-291">Hallo github-pagina heeft een koppeling tooa Wiki met aanvullende informatie op Hallo player framework en een inleiding toohello player-voorbeeld: [Azure Media Player Wiki](https://github.com/Azure/azure-media-player-framework/wiki/How-to-use-Azure-media-player-framework).</span><span class="sxs-lookup"><span data-stu-id="4ff6f-291">hello github page has a link tooa Wiki that contains additional information on hello player framework and an introduction toohello player sample: [Azure Media Player Wiki](https://github.com/Azure/azure-media-player-framework/wiki/How-to-use-Azure-media-player-framework).</span></span>

### <a name="scheduling-ads-with-vmap"></a><span data-ttu-id="4ff6f-292">Advertenties met VMAP plannen</span><span class="sxs-lookup"><span data-stu-id="4ff6f-292">Scheduling Ads with VMAP</span></span>
<span data-ttu-id="4ff6f-293">Hallo volgende voorbeeld wordt getoond hoe tooschedule advertenties met een VMAP-bestand.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-293">hello following example shows how tooschedule ads using a VMAP file.</span></span>

    // How tooschedule an Ad using VMAP.
    //First download hello VMAP manifest

    if (![framework.adResolver downloadManifest:&manifest withURL:[NSURL URLWithString:@"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVMAP.xml"]])
            {
                [self logFrameworkError];
            }
            else
            {
                // Schedule a list of ads using hello downloaded VMAP manifest
                if (![framework scheduleVMAPWithManifest:manifest])
                {
                    [self logFrameworkError];
                }          
            }

### <a name="scheduling-ads-with-vast"></a><span data-ttu-id="4ff6f-294">Advertenties met VAST plannen</span><span class="sxs-lookup"><span data-stu-id="4ff6f-294">Scheduling Ads with VAST</span></span>
<span data-ttu-id="4ff6f-295">Hallo volgende voorbeeld toont hoe tooschedule een late binding VAST ad.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-295">hello following sample shows how tooschedule a late binding VAST ad.</span></span>

    //Example:3 How tooschedule a late binding VAST ad.
    // set hello start time for hello ad
    adLinearTime.startTime = 13;
    adLinearTime.duration = 0;
    // Specify hello URI of hello VAST file
    NSString *vastAd1=@"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml";
    // Create an AdInfo object
     AdInfo *vastAdInfo1 = [[[AdInfo alloc] init] autorelease];
    // set URL tooVAST file
    vastAdInfo1.clipURL = [NSURL URLWithString:vastAd1];
    // set running time of ad
    vastAdInfo1.mediaTime = [[[MediaTime alloc] init] autorelease];
    vastAdInfo1.mediaTime.clipBeginMediaTime = 0;
    vastAdInfo1.mediaTime.clipEndMediaTime = 10;
    vastAdInfo1.policy = @"policy for late binding VAST";
    // specify ad type
    vastAdInfo1.type = AdType_Midroll;
    vastAdInfo1.appendTo=-1;
    adIndex = 0;
    // schedule ad
    if (![framework scheduleClip:vastAdInfo1 atTime:adLinearTime forType:PlaylistEntryType_VAST andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }

   <span data-ttu-id="4ff6f-296">Hallo volgende voorbeeld toont hoe tooschedule een vroege binding VAST ad.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-296">hello following sample shows how tooschedule an early binding VAST ad.</span></span>
<span data-ttu-id="4ff6f-297">Voorbeeld: 4 planning een vroege binding VAST ad //Download-Hallo VAST bestand indien (! [ framework.adResolver downloadManifest: & manifest withURL: [NSURL URLWithString: @ 'http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml']]) {[self logFrameworkError];} else {adLinearTime.startTime = 7; adLinearTime.duration = 0;</span><span class="sxs-lookup"><span data-stu-id="4ff6f-297">//Example:4 Schedule an early binding VAST ad //Download hello VAST file if (![framework.adResolver downloadManifest:&manifest withURL:[NSURL URLWithString:@"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml"]]) { [self logFrameworkError]; } else { adLinearTime.startTime = 7; adLinearTime.duration = 0;</span></span>

        // Create AdInfo instance
        AdInfo *vastAdInfo2 = [[[AdInfo alloc] init] autorelease];
        vastAdInfo2.mediaTime = [[[MediaTime alloc] init] autorelease];
        vastAdInfo2.policy = @"policy for early binding VAST";
        // specify ad type
        vastAdInfo2.type = AdType_Midroll;
        vastAdInfo2.appendTo=-1;
        // schedule ad
        if (![framework scheduleVASTClip:vastAdInfo2 withManifest:manifest atTime:adLinearTime andGetClipId:&adIndex])
        {
            [self logFrameworkError];
        }
    }

<span data-ttu-id="4ff6f-298">Hallo volgende voorbeeld toont hoe tooinsert een ad dat gebruikmaakt van ruwe knippen bewerkt (Dwingen)</span><span class="sxs-lookup"><span data-stu-id="4ff6f-298">hello following sample shows how tooinsert an ad using Rough Cut Editing (RCE)</span></span>

    //Example:1 How toouse RCE.
    // specify manifest for ad content
    NSString *secondContent=@"http://wamsblureg001orig-hs.cloudapp.net/6651424c-a9d1-419b-895c-6993f0f48a26/The%20making%20of%20Microsoft%20Surface-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";

    // specify ad length
    mediaTime.currentPlaybackPosition = 0;
    mediaTime.clipBeginMediaTime = 0;
    mediaTime.clipEndMediaTime = 80;
    // append ad content
    if (![framework appendContentClip:[NSURL URLWithString:secondContent] withMediaTime:mediaTime andGetClipId:&clipId])
    {
        [self logFrameworkError];
    }

<span data-ttu-id="4ff6f-299">Hallo volgende voorbeeld ziet u hoe een advertentie tooschedule schil.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-299">hello following example shows how tooschedule an ad pod.</span></span>

    //Example:5 Schedule an ad Pod.
    // Set start time for ad
    adLinearTime.startTime = 23;
    adLinearTime.duration = 0;

    // Specify URL toocontent
    NSString *adpodSt1=@"https://portalvhdsq3m25bf47d15c.blob.core.windows.net/asset-e47b43fd-05dc-4587-ac87-5916439ad07f/Windows%208_%20Cliffjumpers.mp4?st=2012-11-28T16%3A31%3A57Z&se=2014-11-28T16%3A31%3A57Z&sr=c&si=2a6dbb1e-f906-4187-a3d3-7e517192cbd0&sig=qrXYZBekqlbbYKqwovxzaVZNLv9cgyINgMazSCbdrfU%3D";
    // Create an AdInfo instance
    AdInfo *adpodInfo1 = [[[AdInfo alloc] init] autorelease];
    // set URI tooad content
    adpodInfo1.clipURL = [NSURL URLWithString:adpodSt1];
    // Set ad running time
    adpodInfo1.mediaTime = [[[MediaTime alloc] init] autorelease];
    adpodInfo1.mediaTime.clipBeginMediaTime = 0;
    adpodInfo1.mediaTime.clipEndMediaTime = 17;
    adpodInfo1.policy = @"policy for ad pod 1";
    // Set ad type
    adpodInfo1.type = AdType_Midroll;
    adpodInfo1.appendTo=-1;
    adIndex = 0;
    // Schedule ad
    if (![framework scheduleClip:adpodInfo1 atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }

<span data-ttu-id="4ff6f-300">Hallo volgende voorbeeld wordt getoond hoe tooschedule een niet-tijdelijke halverwege roll ad.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-300">hello following example shows how tooschedule a non-sticky mid-roll ad.</span></span> <span data-ttu-id="4ff6f-301">Een niet-tijdelijke ad alleen afgespeeld wanneer ongeacht eventuele om Hallo viewer uitvoert.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-301">A non-sticky ad is only played once regardless of any seeking hello viewer performs.</span></span>

    //Example:6 Schedule a single non sticky mid roll Ad
    // specify URL toocontent
    NSString *oneTimeAd=@"http://wamsblureg001orig-hs.cloudapp.net/5389c0c5-340f-48d7-90bc-0aab664e5f02/Windows%208_%20You%20and%20Me%20Together-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";

    // create an AdInfo instance
    AdInfo *oneTimeInfo = [[[AdInfo alloc] init] autorelease];
    // set URL of ad
    oneTimeInfo.clipURL = [NSURL URLWithString:oneTimeAd];
    oneTimeInfo.mediaTime = [[[MediaTime alloc] init] autorelease];
    oneTimeInfo.mediaTime.clipBeginMediaTime = 0;
    oneTimeInfo.mediaTime.clipEndMediaTime = -1;
    oneTimeInfo.policy = @"policy for one-time ad";
    // set ad start time
    adLinearTime.startTime = 43;
    adLinearTime.duration = 0;
    // set ad type
    oneTimeInfo.type = AdType_Midroll;
    // non sticky ad
    oneTimeInfo.deleteAfterPlayed = YES;
    // schedule ad
    if (![framework scheduleClip:oneTimeInfo atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }

<span data-ttu-id="4ff6f-302">Hallo volgende voorbeeld wordt getoond hoe tooschedule een tijdelijke halverwege roll ad.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-302">hello following example shows how tooschedule a sticky mid-roll ad.</span></span> <span data-ttu-id="4ff6f-303">Een tijdelijke ad weergegeven telkens Hallo opgegeven punt op Hallo video tijdlijn is bereikt.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-303">A sticky ad will be displayed each time hello specified point on hello video timeline is reached.</span></span>

    //Example:7 Schedule a single sticky mid roll Ad
    NSString *stickyAd=@"http://wamsblureg001orig-hs.cloudapp.net/2e4e7d1f-b72a-4994-a406-810c796fc4fc/The%20Surface%20Movement-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";
    // create AdInfo instance
    AdInfo *stickyAdInfo = [[[AdInfo alloc] init] autorelease];
    // set URI tooad
    stickyAdInfo.clipURL = [NSURL URLWithString:stickyAd];
    stickyAdInfo.mediaTime = [[[MediaTime alloc] init] autorelease];
    stickyAdInfo.mediaTime.clipBeginMediaTime = 0;
    stickyAdInfo.mediaTime.clipEndMediaTime = 15;
    stickyAdInfo.policy = @"policy for sticky mid-roll ad";
    // set ad start time
    adLinearTime.startTime = 64;
    adLinearTime.duration = 0;
    // set ad type
    stickyAdInfo.type = AdType_Midroll;
    stickyAdInfo.deleteAfterPlayed = NO;
    // schedule ad
    if (![framework scheduleClip:stickyAdInfo atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }


<span data-ttu-id="4ff6f-304">Hallo volgende voorbeeld toont hoe tooschedule een advertentie na doorvoeren.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-304">hello following sample shows how tooschedule a post-roll ad.</span></span>

    //Example:8 Schedule Post Roll Ad
    NSString *postAdURLString=@"http://wamsblureg001orig-hs.cloudapp.net/aa152d7f-3c54-487b-ba07-a58e0e33280b/wp-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";
    // create AdInfo instance
    AdInfo *postAdInfo = [[[AdInfo alloc] init] autorelease];
    postAdInfo.clipURL = [NSURL URLWithString:postAdURLString];
    postAdInfo.mediaTime = [[[MediaTime alloc] init] autorelease];
    postAdInfo.mediaTime.clipBeginMediaTime = 0;
    // set ad length
    postAdInfo.mediaTime.clipEndMediaTime = 45;
    postAdInfo.policy = @"policy for post-roll ad";
    // set ad type
    postAdInfo.type = AdType_Postroll;
    adLinearTime.duration = 0;
    if (![framework scheduleClip:postAdInfo atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }

<span data-ttu-id="4ff6f-305">Hallo volgende voorbeeld toont hoe tooschedule een vooraf roll ad.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-305">hello following sample shows how tooschedule a pre-roll ad.</span></span>

    //Example:9 Schedule Pre Roll Ad
    NSString *adURLString = @"http://wamsblureg001orig-hs.cloudapp.net/2e4e7d1f-b72a-4994-a406-810c796fc4fc/The%20Surface%20Movement-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";
    AdInfo *adInfo = [[[AdInfo alloc] init] autorelease];
    adInfo.clipURL = [NSURL URLWithString:adURLString];
    adInfo.mediaTime = [[[MediaTime alloc] init] autorelease];
    adInfo.mediaTime.currentPlaybackPosition = 0;
    adInfo.mediaTime.clipBeginMediaTime = 40; //You could play a portion of an Ad. Yeh!
    adInfo.mediaTime.clipEndMediaTime = 59;
    adInfo.policy = @"policy for pre-roll ad";
    adInfo.appendTo = -1;
    adInfo.type = AdType_Preroll;
    adLinearTime.duration = 0;
    // schedule ad
    if (![framework scheduleClip:adInfo atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }

<span data-ttu-id="4ff6f-306">Hallo volgende voorbeeld ziet u hoe een halverwege roll tooschedule ad overlay.</span><span class="sxs-lookup"><span data-stu-id="4ff6f-306">hello following sample shows how tooschedule a mid-roll overlay ad.</span></span>

    // Example10: Schedule a Mid Roll overlay Ad
    NSString *adURLString = @"https://portalvhdsq3m25bf47d15c.blob.core.windows.net/asset-e47b43fd-05dc-4587-ac87-5916439ad07f/Windows%208_%20Cliffjumpers.mp4?st=2012-11-28T16%3A31%3A57Z&se=2014-11-28T16%3A31%3A57Z&sr=c&si=2a6dbb1e-f906-4187-a3d3-7e517192cbd0&sig=qrXYZBekqlbbYKqwovxzaVZNLv9cgyINgMazSCbdrfU%3D";
    //Create AdInfo instance
    AdInfo *adInfo = [[[AdInfo alloc] init] autorelease];
    adInfo.clipURL = [NSURL URLWithString:adURLString];
    adInfo.mediaTime = [[[MediaTime alloc] init] autorelease];
    adInfo.mediaTime.currentPlaybackPosition = 0;
    adInfo.mediaTime.clipBeginMediaTime = 0;
    // specify ad length
    adInfo.mediaTime.clipEndMediaTime = 20;
    adInfo.policy = @"policy for mid-roll overlay ad";
    adInfo.appendTo = -1;
    // specify ad type
    adInfo.type = AdType_Midroll;
    // specify ad start time & duration
    adLinearTime.startTime = 300;
    adLinearTime.duration = 20;
    // schedule ad            if (![framework scheduleClip:adInfo atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }



## <a name="media-services-learning-paths"></a><span data-ttu-id="4ff6f-307">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="4ff6f-307">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="4ff6f-308">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="4ff6f-308">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="4ff6f-309">Zie ook</span><span class="sxs-lookup"><span data-stu-id="4ff6f-309">See Also</span></span>
[<span data-ttu-id="4ff6f-310">Videospelertoepassingen ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="4ff6f-310">Develop video player applications</span></span>](media-services-develop-video-players.md)

