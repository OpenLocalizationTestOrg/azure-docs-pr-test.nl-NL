---
title: Invoegen van advertenties aan de clientzijde | Microsoft Docs
description: Dit onderwerp leest hoe u kunt advertenties aan de clientzijde invoegen.
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
ms.openlocfilehash: 52ba731f88c630830560e3cf8406ba2e9613c8a5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="inserting-ads-on-the-client-side"></a><span data-ttu-id="6fd3e-103">Invoegen van advertenties aan de clientzijde</span><span class="sxs-lookup"><span data-stu-id="6fd3e-103">Inserting ads on the client side</span></span>
<span data-ttu-id="6fd3e-104">In dit onderwerp bevat informatie over het invoegen van verschillende typen advertenties aan de clientzijde.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-104">This topic contains information on how to insert various types of ads on the client side.</span></span>

<span data-ttu-id="6fd3e-105">Zie voor meer informatie over gesloten ondertiteling en ad-ondersteuning in Live streaming video's [ondersteund gesloten ondertiteling en Ad invoegen standaarden](media-services-live-streaming-with-onprem-encoders.md#cc_and_ads).</span><span class="sxs-lookup"><span data-stu-id="6fd3e-105">For information about closed captioning and ad support in Live streaming videos, see [Supported Closed Captioning and Ad Insertion Standards](media-services-live-streaming-with-onprem-encoders.md#cc_and_ads).</span></span>

> [!NOTE]
> <span data-ttu-id="6fd3e-106">Azure Media Player biedt momenteel geen ondersteuning voor advertenties.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-106">Azure Media Player does not currently support Ads.</span></span>
> 
> 

## <span data-ttu-id="6fd3e-107"><a id="insert_ads_into_media"></a>Advertenties in uw Media invoegen</span><span class="sxs-lookup"><span data-stu-id="6fd3e-107"><a id="insert_ads_into_media"></a>Inserting Ads into your Media</span></span>
<span data-ttu-id="6fd3e-108">Azure Media Services biedt ondersteuning voor het invoegen van ad via de Windows Media-Platform: Frameworks voor spelers.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-108">Azure Media Services provides support for ad insertion through the Windows Media Platform: Player Frameworks.</span></span> <span data-ttu-id="6fd3e-109">Er zijn frameworks voor spelers met ad-ondersteuning beschikbaar voor Windows 8, Silverlight, Windows Phone 8 en iOS-apparaten.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-109">Player frameworks with ad support are available for Windows 8, Silverlight, Windows Phone 8, and iOS devices.</span></span> <span data-ttu-id="6fd3e-110">Elke player-framework bevat voorbeeldcode die laat zien hoe een toepassing player implementeren. Er zijn drie soorten advertenties die u in uw media: de lijst invoegen kunt.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-110">Each player framework contains sample code that shows you how to implement a player application.There are three different kinds of ads you can insert into your media:list.</span></span>

* <span data-ttu-id="6fd3e-111">**Lineaire** – volledige frame advertenties die de belangrijkste video onderbreken.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-111">**Linear** – full frame ads that pause the main video.</span></span>
* <span data-ttu-id="6fd3e-112">**Niet-lineaire** – overlay advertenties die worden weergegeven als de belangrijkste video wordt afgespeeld, meestal een logo of een andere statische afbeelding geplaatst Windows Media Player.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-112">**Nonlinear** – overlay ads that are displayed as the main video is playing, usually a logo or other static image placed within the player.</span></span>
* <span data-ttu-id="6fd3e-113">**Aanvullende** – advertenties die buiten de speler worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-113">**Companion** – ads that are displayed outside of the player.</span></span>

<span data-ttu-id="6fd3e-114">Advertenties kunnen op elk punt in de tijdlijn van de belangrijkste video worden geplaatst.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-114">Ads can be placed at any point in the main video’s time line.</span></span> <span data-ttu-id="6fd3e-115">U moet de speler hoogte wanneer af te spelen, de advertentie en welke advertenties af te spelen.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-115">You must tell the player when to play the ad and which ads to play.</span></span> <span data-ttu-id="6fd3e-116">Dit wordt gedaan met behulp van een reeks standaard XML-bestanden: Video Ad-Service-sjabloon (VAST), digitale Video meerdere Ad afspeellijst (VMAP), Media abstracte sequentiëren sjabloon (b) en digitale Video Player Ad Interface Definition (VPAID).</span><span class="sxs-lookup"><span data-stu-id="6fd3e-116">This is done using a set of standard XML-based files: Video Ad Service Template (VAST), Digital Video Multiple Ad Playlist (VMAP), Media Abstract Sequencing Template (MAST), and Digital Video Player Ad Interface Definition (VPAID).</span></span> <span data-ttu-id="6fd3e-117">GROTE bestanden opgeven welke advertenties om weer te geven.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-117">VAST files specify what ads to display.</span></span> <span data-ttu-id="6fd3e-118">VMAP bestanden opgeven wanneer verschillende advertenties afspelen en ENORME XML bevatten.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-118">VMAP files specify when to play various ads and contain VAST XML.</span></span> <span data-ttu-id="6fd3e-119">B bestanden vormen een andere reeks advertenties die tevens VAST XML kan bevatten.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-119">MAST files are another way to sequence ads which also can contain VAST XML.</span></span> <span data-ttu-id="6fd3e-120">VPAID bestanden definiëren een interface tussen de video speler en de advertentie- of Active Directory-server.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-120">VPAID files define an interface between the video player and the ad or ad server.</span></span>

<span data-ttu-id="6fd3e-121">Elke player-framework werkt er anders en elk worden behandeld in een eigen onderwerp.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-121">Each player framework works differently and each will be covered in its own topic.</span></span> <span data-ttu-id="6fd3e-122">In dit onderwerp beschrijft de basic mechanismen gebruikt voor het invoegen van advertenties. Ads aanvragen-speler toepassingen bij een ad-server.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-122">This topic will describe the basic mechanisms used to insert ads.Video player applications request ads from an ad server.</span></span> <span data-ttu-id="6fd3e-123">De ad-server kan reageren op een aantal verschillende manieren:</span><span class="sxs-lookup"><span data-stu-id="6fd3e-123">The ad server can respond in a number of ways:</span></span>

* <span data-ttu-id="6fd3e-124">Een groot bestand geretourneerd</span><span class="sxs-lookup"><span data-stu-id="6fd3e-124">Return a VAST file</span></span>
* <span data-ttu-id="6fd3e-125">Retourneren van een bestand VMAP (met ingesloten VAST)</span><span class="sxs-lookup"><span data-stu-id="6fd3e-125">Return a VMAP file (with embedded VAST)</span></span>
* <span data-ttu-id="6fd3e-126">Retourneert een b-bestand (met ingesloten VAST)</span><span class="sxs-lookup"><span data-stu-id="6fd3e-126">Return a MAST file (with embedded VAST)</span></span>
* <span data-ttu-id="6fd3e-127">Een groot bestand met advertenties VPAID geretourneerd</span><span class="sxs-lookup"><span data-stu-id="6fd3e-127">Return a VAST file with VPAID ads</span></span>

### <a name="using-a-video-ad-service-template-vast-file"></a><span data-ttu-id="6fd3e-128">Met behulp van een Video Ad-Service (VAST) sjabloonbestand</span><span class="sxs-lookup"><span data-stu-id="6fd3e-128">Using a Video Ad Service Template (VAST) File</span></span>
<span data-ttu-id="6fd3e-129">Een groot bestand geeft aan welke ad of de advertenties.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-129">A VAST file specifies what ad or ads to display.</span></span> <span data-ttu-id="6fd3e-130">De volgende XML-code is een voorbeeld van een groot bestand voor een lineaire ad:</span><span class="sxs-lookup"><span data-stu-id="6fd3e-130">The following XML is an example of a VAST file for a linear ad:</span></span>

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

<span data-ttu-id="6fd3e-131">De lineaire ad wordt beschreven in de <**lineair**> element.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-131">The linear ad is described by the <**Linear**> element.</span></span> <span data-ttu-id="6fd3e-132">Hiermee wordt de duur van de ad, het bijhouden van gebeurtenissen, klikt u op via op bijhouden en een aantal **MediaFile** elementen.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-132">It specifies the duration of the ad, tracking events, click through, click tracking, and a number of **MediaFile** elements.</span></span> <span data-ttu-id="6fd3e-133">Bijhouden van gebeurtenissen zijn opgegeven in de <**TrackingEvents**> element en het toestaan van een ad-server om bij te houden van diverse gebeurtenissen die zich voordoen tijdens het bekijken van de ad.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-133">Tracking events are specified within the <**TrackingEvents**> element and allow an ad server to track various events that occur while viewing the ad.</span></span> <span data-ttu-id="6fd3e-134">In dit geval het begin wordt het middelpunt, voltooid, en vouw gebeurtenissen worden bijgehouden.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-134">In this case the start, midpoint, complete, and expand events are tracked.</span></span> <span data-ttu-id="6fd3e-135">De begingebeurtenis treedt op wanneer de advertentie wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-135">The start event occurs when the ad is displayed.</span></span> <span data-ttu-id="6fd3e-136">Het middelpunt gebeurtenis treedt op wanneer ten minste 50% van de ad-tijdlijn is weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-136">The midpoint event occurs when at least 50% of the ad’s timeline has been viewed.</span></span> <span data-ttu-id="6fd3e-137">De gebeurtenis treedt op wanneer de ad is uitgevoerd met het einde.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-137">The complete event occurs when the ad has run to the end.</span></span> <span data-ttu-id="6fd3e-138">De uit te breiden gebeurtenis treedt op wanneer de gebruiker de video speler naar volledig scherm breidt.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-138">The Expand event occurs when the user expands the video player to full screen.</span></span> <span data-ttu-id="6fd3e-139">Clickthroughs worden aangeduid met een <**ClickThrough**>-element in een <**VideoClicks**> element en Hiermee geeft u een URI aan een resource moet worden weergegeven wanneer de gebruiker op de ad klikt.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-139">Clickthroughs are specified with a <**ClickThrough**> element within a <**VideoClicks**> element and specifies a URI to a resource to display when the user clicks on the ad.</span></span> <span data-ttu-id="6fd3e-140">ClickTracking is opgegeven in een <**ClickTracking**>-element, ook in de <**VideoClicks**> element en Hiermee geeft u een resource bijhouden voor Windows media player om aan te vragen wanneer de gebruiker op de ad klikt. De <**MediaFile**> elementen informatie opgeven over een specifieke codering van een ad.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-140">ClickTracking is specified in a <**ClickTracking**> element, also within the <**VideoClicks**> element and specifies a tracking resource for the player to request when the user clicks on the ad.The <**MediaFile**> elements specify information about a specific encoding of an ad.</span></span> <span data-ttu-id="6fd3e-141">Wanneer er meer dan één <**MediaFile**>-element-speler kunt ervoor kiezen de beste codering voor het platform.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-141">When there is more than one <**MediaFile**> element, the video player can choose the best encoding for the platform.</span></span> 

<span data-ttu-id="6fd3e-142">Lineaire advertenties kunnen worden weergegeven in een bepaalde volgorde.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-142">Linear ads can be displayed in a specified order.</span></span> <span data-ttu-id="6fd3e-143">U doet dit door toevoegen extra <Ad> elementen op de VAST bestand en de volgorde die met het kenmerk reeks opgeven.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-143">To do this, add additional <Ad> elements to the VAST file and specify the order using the sequence attribute.</span></span> <span data-ttu-id="6fd3e-144">Het volgende voorbeeld illustreert dit:</span><span class="sxs-lookup"><span data-stu-id="6fd3e-144">The following example illustrates this:</span></span>

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

<span data-ttu-id="6fd3e-145">Niet-lineaire advertenties zijn opgegeven in een <Creative> ook element.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-145">Nonlinear ads are specified in a <Creative> element as well.</span></span> <span data-ttu-id="6fd3e-146">Het volgende voorbeeld wordt een <Creative> element dat een niet-lineaire ad beschrijft.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-146">The following example shows a <Creative> element that describes a nonlinear ad.</span></span>

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


<span data-ttu-id="6fd3e-147">De <**NonLinearAds**>-element kan bevatten een of meer <**NonLinear**>-elementen, elk met een niet-lineaire ad kunt beschrijven.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-147">The <**NonLinearAds**> element can contain one or more <**NonLinear**> elements, each of which can describe a nonlinear ad.</span></span> <span data-ttu-id="6fd3e-148">De <**NonLinear**> element geeft de bron voor de niet-lineaire ad.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-148">The <**NonLinear**> element specifies the resource for the nonlinear ad.</span></span> <span data-ttu-id="6fd3e-149">De bron kan bestaan uit een <**StaticResouce**>, een <**IFrameResource**>, of een <**HTMLResouce**>.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-149">The resource can be a <**StaticResouce**>, an <**IFrameResource**>, or an <**HTMLResouce**>.</span></span><span data-ttu-id="6fd3e-150"> <**StaticResource**> Beschrijving van een niet-HTML-bron en definieert een creativeType-kenmerk geeft aan hoe de resource wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="6fd3e-150"> <**StaticResource**> describes a non-HTML resource and defines a creativeType attribute that specifies how the resource is displayed:</span></span>

<span data-ttu-id="6fd3e-151">Afbeelding/GIF-, afbeelding/JPEG-, afbeelding/png – de resource wordt weergegeven in een HTML-code <**img**> label.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-151">Image/gif, image/jpeg, image/png – the resource is displayed in an HTML <**img**> tag.</span></span>

<span data-ttu-id="6fd3e-152">Toepassing/x-javascript – de resource wordt weergegeven in een HTML-code <**script**> label.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-152">Application/x-javascript – the resource is displayed in an HTML <**script**> tag.</span></span>

<span data-ttu-id="6fd3e-153">Toepassing/x-shockwave-flash – de resource wordt weergegeven in een Flash player.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-153">Application/x-shockwave-flash – the resource is displayed in a Flash player.</span></span>

<span data-ttu-id="6fd3e-154">**IFrameResource** een HTML-bron die kan worden weergegeven in een IFrame worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-154">**IFrameResource** describes an HTML resource that can be displayed in an IFrame.</span></span> <span data-ttu-id="6fd3e-155">**HTMLResource** beschrijft een stukje HTML-code die kan worden ingevoegd in een webpagina.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-155">**HTMLResource** describes a piece of HTML code that can be inserted into a web page.</span></span> <span data-ttu-id="6fd3e-156">**TrackingEvents** gebeurtenissen bijhouden en de URI om aan te vragen bij de gebeurtenis opgeven.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-156">**TrackingEvents** specify tracking events and the URI to request when the event occurs.</span></span> <span data-ttu-id="6fd3e-157">In dit voorbeeld worden de gebeurtenissen acceptInvitation en samenvouwen bijgehouden.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-157">In this sample the acceptInvitation and collapse events are tracked.</span></span> <span data-ttu-id="6fd3e-158">Voor meer informatie over de **NonLinearAds** -element en de onderliggende items, Zie IAB.NET/VAST.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-158">For more information on the **NonLinearAds** element and its children, see IAB.NET/VAST.</span></span> <span data-ttu-id="6fd3e-159">Houd er rekening mee dat de **TrackingEvents** element zich bevindt binnen de **NonLinearAds** element in plaats van de **NonLinear** element.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-159">Note that the **TrackingEvents** element is located within the **NonLinearAds** element rather than the **NonLinear** element.</span></span>

<span data-ttu-id="6fd3e-160">Aanvullende advertenties zijn gedefinieerd binnen een <CompanionAds> element.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-160">Companion ads are defined within a <CompanionAds> element.</span></span> <span data-ttu-id="6fd3e-161">De <CompanionAds> element kan bevatten een of meer <Companion> elementen.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-161">The <CompanionAds> element can contain one or more <Companion> elements.</span></span> <span data-ttu-id="6fd3e-162">Elke <Companion> element beschrijft een aanvullende ad en bevatten een <StaticResource>, <IFrameResource>, of <HTMLResource> die zijn opgegeven op dezelfde manier als in een niet-lineaire ad.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-162">Each <Companion> element describes a companion ad and can contain a <StaticResource>, <IFrameResource>, or <HTMLResource> which are specified in the same way as in a nonlinear ad.</span></span> <span data-ttu-id="6fd3e-163">Een groot bestand meerdere companion-advertenties kan bevatten en de spelertoepassing kunt de meest geschikte ad om weer te geven.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-163">A VAST file can contain multiple companion ads and the player application can choose the most appropriate ad to display.</span></span> <span data-ttu-id="6fd3e-164">Zie voor meer informatie over VAST [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).</span><span class="sxs-lookup"><span data-stu-id="6fd3e-164">For more information about VAST, see [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).</span></span>

### <a name="using-a-digital-video-multiple-ad-playlist-vmap-file"></a><span data-ttu-id="6fd3e-165">Met behulp van een digitale Video meerdere Ad afspeellijst (VMAP)-bestand</span><span class="sxs-lookup"><span data-stu-id="6fd3e-165">Using a Digital Video Multiple Ad Playlist (VMAP) File</span></span>
<span data-ttu-id="6fd3e-166">Een bestand VMAP kunt u opgeven wanneer ad onderbrekingen optreden, hoe lang elk einde is, hoeveel advertenties worden weergegeven binnen een einde en welke typen advertenties kunnen worden weergegeven tijdens een pauze.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-166">A VMAP file allows you to specify when ad breaks occur, how long each break is, how many ads can be displayed within a break, and what types of ads may be displayed during a break.</span></span> <span data-ttu-id="6fd3e-167">Het volgende in een voorbeeldbestand VMAP die een pauze van één ad definieert:</span><span class="sxs-lookup"><span data-stu-id="6fd3e-167">The following in an example VMAP file that defines a single ad break:</span></span>

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

<span data-ttu-id="6fd3e-168">Een bestand VMAP begint met een <VMAP> element een of meer bevat <AdBreak> elementen, die elk een ad-einde definiëren.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-168">A VMAP file begins with a <VMAP> element that contains one or more <AdBreak> elements, each defining an ad break.</span></span> <span data-ttu-id="6fd3e-169">Elk ad-einde geeft een type einde, break-ID en time-offset.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-169">Each ad break specifies a break type, break ID, and time offset.</span></span> <span data-ttu-id="6fd3e-170">Geeft het type ad die kan worden afgespeeld tijdens het einde van het kenmerk breakType: lineaire, niet-lineaire, of weer te geven.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-170">The breakType attribute specifies the type of ad that can be played during the break: linear, nonlinear, or display.</span></span> <span data-ttu-id="6fd3e-171">Advertenties kaart worden weergegeven voor de ENORME companion advertenties.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-171">Display ads map to VAST companion ads.</span></span> <span data-ttu-id="6fd3e-172">Meer dan één ad-type kan worden opgegeven in een lijst met gescheiden door komma's (zonder spaties).</span><span class="sxs-lookup"><span data-stu-id="6fd3e-172">More than one ad type can be specified in a comma (no spaces) separated list.</span></span> <span data-ttu-id="6fd3e-173">De breakID is een optionele id voor de advertentie.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-173">The breakID is an optional identifier for the ad.</span></span> <span data-ttu-id="6fd3e-174">De timeOffset aangeeft wanneer de advertentie moet worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-174">The timeOffset specifies when the ad should be displayed.</span></span> <span data-ttu-id="6fd3e-175">Deze kan worden opgegeven in een van de volgende manieren:</span><span class="sxs-lookup"><span data-stu-id="6fd3e-175">It can be specified in one of the following ways:</span></span>

1. <span data-ttu-id="6fd3e-176">Tijd in: mm: ss of hh:mm:ss.mmm indeling .mmm waar milliseconden is.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-176">Time – in hh:mm:ss or hh:mm:ss.mmm format where .mmm is milliseconds.</span></span> <span data-ttu-id="6fd3e-177">De waarde van dit kenmerk geeft de tijd vanaf het begin van de video tijdlijn aan het begin van het ad-einde.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-177">The value of this attribute specifies the time from the beginning of the video timeline to the beginning of the ad break.</span></span>
2. <span data-ttu-id="6fd3e-178">Percentage – n % indeling is waarbij n het percentage van de video tijdlijn om af te spelen voordat het afspelen van de ad</span><span class="sxs-lookup"><span data-stu-id="6fd3e-178">Percentage – in n% format where n is the percentage of the video timeline to play before playing the ad</span></span>
3. <span data-ttu-id="6fd3e-179">Beginnen of eindigen – geeft aan dat een advertentie moet worden weergegeven vóór of na de video is weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-179">Start/End – specifies that an ad should be displayed before or after the video has been displayed</span></span>
4. <span data-ttu-id="6fd3e-180">Plaats – Hiermee geeft u de volgorde van de ad-einden wanneer de timing van de ad-einden onbekend, zoals live streamen is.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-180">Position – specifies the order of ad breaks when the timing of the ad breaks is unknown, such as in live streaming.</span></span> <span data-ttu-id="6fd3e-181">De volgorde van elk ad-einde is opgegeven in de indeling van de #n waarbij n staat voor een geheel getal 1 of hoger.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-181">The order of each ad break is specified in the #n format where n is an integer 1 or greater.</span></span> <span data-ttu-id="6fd3e-182">1 geeft aan dat de advertentie moet worden afgespeeld op de eerste kans 2 geeft aan dat de advertentie moet worden afgespeeld op de tweede mogelijkheid enzovoort.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-182">1 signifies the ad should be played at the first opportunity, 2 signifies the ad should be played at the second opportunity and so on.</span></span>

<span data-ttu-id="6fd3e-183">In de <**AdBreak**> element er zijn <**AdSource**> element.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-183">Within the <**AdBreak**> element there can be one <**AdSource**> element.</span></span> <span data-ttu-id="6fd3e-184">De <**AdSource**>-element bevat de volgende kenmerken:</span><span class="sxs-lookup"><span data-stu-id="6fd3e-184">The <**AdSource**> element contains the following attributes:</span></span>

1. <span data-ttu-id="6fd3e-185">-ID: Hiermee geeft u een id voor de ad-bron</span><span class="sxs-lookup"><span data-stu-id="6fd3e-185">Id – specifies an identifier for the ad source</span></span>
2. <span data-ttu-id="6fd3e-186">allowMultipleAds – een Booleaanse waarde die aangeeft of meerdere advertenties kunnen worden weergegeven tijdens het ad-einde</span><span class="sxs-lookup"><span data-stu-id="6fd3e-186">allowMultipleAds – a Boolean value that specifies whether multiple ads can be displayed during the ad break</span></span>
3. <span data-ttu-id="6fd3e-187">followRedirects: een optionele Booleaanse waarde waarmee wordt aangegeven als de video speler moet naleven leidt binnen een ad-antwoord</span><span class="sxs-lookup"><span data-stu-id="6fd3e-187">followRedirects – an optional Boolean value that specifies if the video player should honor redirects within an ad response</span></span>

<span data-ttu-id="6fd3e-188">De <**AdSource**>-element Windows media player heeft een antwoord van de ad inline of een verwijzing naar een ad-antwoord.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-188">The <**AdSource**> element provides the player an inline ad response or a reference to an ad response.</span></span> <span data-ttu-id="6fd3e-189">Dit kan een van de volgende elementen bevatten:</span><span class="sxs-lookup"><span data-stu-id="6fd3e-189">It can contain one of the following elements:</span></span>

* <span data-ttu-id="6fd3e-190"><VASTAdData>geeft dat een ENORME ad-antwoord is ingesloten in het bestand VMAP</span><span class="sxs-lookup"><span data-stu-id="6fd3e-190"><VASTAdData> indicates a VAST ad response is embedded within the VMAP file</span></span>
* <span data-ttu-id="6fd3e-191"><AdTagURI>een URI die verwijst naar een ad-antwoord van een ander systeem</span><span class="sxs-lookup"><span data-stu-id="6fd3e-191"><AdTagURI> a URI that references an ad response from another system</span></span>
* <span data-ttu-id="6fd3e-192"><CustomAdData>-een willekeurige tekenreeks die respresents een niet-VAST antwoord</span><span class="sxs-lookup"><span data-stu-id="6fd3e-192"><CustomAdData> -an arbitrary string that respresents a non-VAST response</span></span>

<span data-ttu-id="6fd3e-193">In dit voorbeeld wordt een in-line ad-antwoord opgegeven met een <VASTAdData> element dat een ENORME ad-antwoord bevat.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-193">In this example an in-line ad response is specified with a <VASTAdData> element that contains a VAST ad response.</span></span> <span data-ttu-id="6fd3e-194">Zie voor meer informatie over de andere elementen [VMAP](http://www.iab.net/guidelines/508676/digitalvideo/vsuite/vmap).</span><span class="sxs-lookup"><span data-stu-id="6fd3e-194">For more information about the other elements, see [VMAP](http://www.iab.net/guidelines/508676/digitalvideo/vsuite/vmap).</span></span>

<span data-ttu-id="6fd3e-195">De <**AdBreak**>-element kan ook bevatten <**TrackingEvents**> element.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-195">The <**AdBreak**> element can also contain one <**TrackingEvents**> element.</span></span> <span data-ttu-id="6fd3e-196">De <**TrackingEvents**>-element kunt u het begin of einde van een ad-einde of of een fout opgetreden tijdens het ad-einde bijhouden.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-196">The <**TrackingEvents**> element allows you to track the start or end of an ad break or whether an error occurred during the ad break.</span></span> <span data-ttu-id="6fd3e-197">De <**TrackingEvents**>-element bevat een of meer <**bijhouden**>-elementen, die elk een gebeurtenis bijhouden en bijgehouden URI bevat.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-197">The <**TrackingEvents**> element contains one or more <**Tracking**> elements, each of which specifies a tracking event and a tracking URI.</span></span> <span data-ttu-id="6fd3e-198">De mogelijke bijhouden gebeurtenissen zijn:</span><span class="sxs-lookup"><span data-stu-id="6fd3e-198">The possible tracking events are:</span></span>

1. <span data-ttu-id="6fd3e-199">breakStart – houdt het begin van een ad-einde</span><span class="sxs-lookup"><span data-stu-id="6fd3e-199">breakStart – tracks the beginning of an ad break</span></span>
2. <span data-ttu-id="6fd3e-200">breakEnd – de voltooiing van een ad-einde bijhouden</span><span class="sxs-lookup"><span data-stu-id="6fd3e-200">breakEnd – track the completion of an ad break</span></span>
3. <span data-ttu-id="6fd3e-201">Fout: een fout die is opgetreden tijdens het ad-einde wordt bijgehouden</span><span class="sxs-lookup"><span data-stu-id="6fd3e-201">error – tracks an error that occurred during the ad break</span></span>

<span data-ttu-id="6fd3e-202">Het volgende voorbeeld ziet een bestand VMAP waarmee gebeurtenissen bijhouden</span><span class="sxs-lookup"><span data-stu-id="6fd3e-202">The following example shows a VMAP file that specifies tracking events</span></span>

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

<span data-ttu-id="6fd3e-203">Voor meer informatie over de <**TrackingEvents**>-element en de onderliggende items, Zie http://iab.org/VMAP.pdf</span><span class="sxs-lookup"><span data-stu-id="6fd3e-203">For more information on the <**TrackingEvents**> element and its children, see http://iab.org/VMAP.pdf</span></span>

### <a name="using-a-media-abstract-sequencing-template-mast-file"></a><span data-ttu-id="6fd3e-204">Met behulp van een Media Abstract sequentiëren sjabloonbestand (b)</span><span class="sxs-lookup"><span data-stu-id="6fd3e-204">Using a Media Abstract Sequencing Template (MAST) File</span></span>
<span data-ttu-id="6fd3e-205">Een bestand b kunt u opgeven triggers die bepalen wanneer een advertentie wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-205">A MAST file allows you to specify triggers that define when an ad is displayed.</span></span> <span data-ttu-id="6fd3e-206">Hier volgt een voorbeeld van de b-bestand met triggers voor een pre-album ad, een tussentijdse roll ad en een advertentie na doorvoeren.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-206">The following is an example MAST file that contains triggers for a pre roll ad, a mid-roll ad, and a post-roll ad.</span></span>

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
            <!--This 'resets' the trigger for the next clip-->
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



<span data-ttu-id="6fd3e-207">Een bestand b begint met een **b** element met een **triggers** element.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-207">A MAST file begins with a **MAST** element that contains one **triggers** element.</span></span> <span data-ttu-id="6fd3e-208">De <triggers> element bevat een of meer **trigger** elementen die bepalen wanneer een advertentie moet worden afgespeeld.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-208">The <triggers> element contains one or more **trigger** elements that define when an ad should be played.</span></span> 

<span data-ttu-id="6fd3e-209">De **trigger** element bevat een **startConditions** element die opgeven wanneer een advertentie moet beginnen met het af te spelen.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-209">The **trigger** element contains a **startConditions** element which specify when an ad should begin to play.</span></span> <span data-ttu-id="6fd3e-210">De **startConditions** element bevat een of meer <condition> elementen.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-210">The **startConditions** element contains one or more <condition> elements.</span></span> <span data-ttu-id="6fd3e-211">Wanneer elke <condition> resulteert in waar een trigger wordt gestart of ingetrokken, afhankelijk van of u de <condition> is opgenomen in een **startConditions** of **endConditions** element respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-211">When each <condition> evaluates to true a trigger is initiated or revoked depending upon whether the <condition> is contained within a **startConditions** or **endConditions** element respectively.</span></span> <span data-ttu-id="6fd3e-212">Wanneer meerdere <condition> elementen aanwezig zijn, worden deze behandeld als een impliciete OR, elke voorwaarde evalueren als waar, wordt de trigger initiëren.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-212">When multiple <condition> elements are present, they are treated as an implicit OR, any condition evaluating to true will cause the trigger to initiate.</span></span> <span data-ttu-id="6fd3e-213"><condition>elementen kunnen worden genest.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-213"><condition> elements can be nested.</span></span> <span data-ttu-id="6fd3e-214">Als onderliggende <condition> elementen zijn vooraf ingesteld, worden deze behandeld als een impliciete AND, alle voorwaarden moeten resulteren in waar voor de trigger initiëren.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-214">When child <condition> elements are preset, they are treated as an implicit AND, all conditions must evaluate to true for the trigger to initiate.</span></span> <span data-ttu-id="6fd3e-215">De <condition> element bevat de volgende kenmerken die de voorwaarde definiëren:</span><span class="sxs-lookup"><span data-stu-id="6fd3e-215">The <condition> element contains the following attributes that define the condition:</span></span> 

1. <span data-ttu-id="6fd3e-216">**type** – Hiermee wordt het type voorwaarde, gebeurtenis of eigenschap</span><span class="sxs-lookup"><span data-stu-id="6fd3e-216">**type** – specifies the type of condition, event or property</span></span>
2. <span data-ttu-id="6fd3e-217">**naam** : de naam van de eigenschap of gebeurtenis moet worden gebruikt tijdens de evaluatie</span><span class="sxs-lookup"><span data-stu-id="6fd3e-217">**name** – the name of the property or event to be used during evaluation</span></span>
3. <span data-ttu-id="6fd3e-218">**waarde** : de waarde die een eigenschap worden geëvalueerd</span><span class="sxs-lookup"><span data-stu-id="6fd3e-218">**value** – the value that a property will be evaluated against</span></span>
4. <span data-ttu-id="6fd3e-219">**operator** : de bewerking moet worden gebruikt tijdens de evaluatie: EQ (equal), NEQ (niet gelijk aan), GTR (groter), GEQ (groter of gelijk zijn), LT (minder dan), LEQ (kleiner dan of gelijk aan), MOD (modulo)</span><span class="sxs-lookup"><span data-stu-id="6fd3e-219">**operator** – the operation to use during evaluation: EQ (equal), NEQ (not equal), GTR (greater), GEQ (greater or equal), LT (Less than), LEQ (less than or equal), MOD (modulo)</span></span>

<span data-ttu-id="6fd3e-220">**endConditions** bevat ook <condition> elementen.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-220">**endConditions** also contain <condition> elements.</span></span> <span data-ttu-id="6fd3e-221">Wanneer een voorwaarde wordt geëvalueerd op waar de trigger wordt opnieuw ingesteld. De <trigger> element bevat ook een <sources> element een of meer bevat <source> elementen.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-221">When a condition evaluates to true the trigger is reset.The <trigger> element also contains a <sources> element that contains one or more <source> elements.</span></span> <span data-ttu-id="6fd3e-222">De <source> elementen de URI voor het ad-antwoord en het type ad reactie definiëren.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-222">The <source> elements define the URI to the ad response and the type of ad response.</span></span> <span data-ttu-id="6fd3e-223">In dit voorbeeld wordt een URI aan een ENORME antwoord gegeven.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-223">In this example a URI is given to a VAST response.</span></span> 

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


### <a name="using-video-player-ad-interface-definition-vpaid"></a><span data-ttu-id="6fd3e-224">Met behulp van Video Player-Ad-Interface Definition (VPAID)</span><span class="sxs-lookup"><span data-stu-id="6fd3e-224">Using Video Player-Ad Interface Definition (VPAID)</span></span>
<span data-ttu-id="6fd3e-225">VPAID is een API voor het inschakelen van uitvoerbare ad eenheden om te communiceren met een video-speler.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-225">VPAID is an API for enabling executable ad units to communicate with a video player.</span></span> <span data-ttu-id="6fd3e-226">Hiermee worden interactieve ad-ervaringen.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-226">This allows highly interactive ad experiences.</span></span> <span data-ttu-id="6fd3e-227">De gebruiker kan communiceren met de ad en de advertentie acties die door de viewer kan reageren.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-227">The user can interact with the ad and the ad can respond to actions taken by the viewer.</span></span> <span data-ttu-id="6fd3e-228">Zo kan een ad knoppen waarmee de gebruiker om weer te geven voor meer informatie of een langer versie van de ad weergeven.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-228">For example an ad may display buttons that allow the user to view more information or a longer version of the ad.</span></span> <span data-ttu-id="6fd3e-229">De video speler moet de API VPAID ondersteunen en de API moet worden geïmplementeerd door de uitvoerbare ad.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-229">The video player must support the VPAID API and the executable ad must implement the API.</span></span> <span data-ttu-id="6fd3e-230">Wanneer een speler vraagt dat een advertentie van een ad-server de server reageert met een ENORME antwoord dat een advertentie VPAID bevat.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-230">When a player requests an ad from an ad server the server may respond with a VAST response that contains a VPAID ad.</span></span>

<span data-ttu-id="6fd3e-231">Een uitvoerbaar ad wordt gemaakt in de code die moet worden uitgevoerd in een runtime-omgeving, zoals Adobe Flash™ of JavaScript die kan worden uitgevoerd in een webbrowser.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-231">An executable ad is created in code that must be executed in a runtime environment such as Adobe Flash™ or JavaScript that can be executed in a web browser.</span></span> <span data-ttu-id="6fd3e-232">Wanneer een ad-server retourneert een ENORME antwoord met een ad VPAID, wordt de waarde van de apiFramework kenmerk in de <MediaFile> element moet 'VPAID'.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-232">When an ad server returns a VAST response containing a VPAID ad, the value of the apiFramework attribute in the <MediaFile> element must be “VPAID”.</span></span> <span data-ttu-id="6fd3e-233">Dit kenmerk geeft aan dat de ingesloten ad een VPAID uitvoerbare ad.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-233">This attribute specifies that the contained ad is a VPAID executable ad.</span></span> <span data-ttu-id="6fd3e-234">Het typekenmerk moet worden ingesteld op het MIME-type van het uitvoerbare bestand, zoals ' application/x-shockwave-flash' of ' application/x-javascript'.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-234">The type attribute must be set to the MIME type of the executable, such as “application/x-shockwave-flash” or “application/x-javascript”.</span></span> <span data-ttu-id="6fd3e-235">Het volgende XML-codefragment bevat de <MediaFile> element uit een ENORME antwoord met een VPAID uitvoerbare ad.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-235">The following XML snippet shows the <MediaFile> element from a VAST response containing a VPAID executable ad.</span></span> 

    <MediaFiles>
       <MediaFile id="1" delivery="progressive" type=”application/x-shockwaveflash”
                  width=”640” height=”480” apiFramework=”VPAID”>
           <!-- CDATA wrapped URI to executable ad -->
       </MediaFile>
    </MediaFiles>


<span data-ttu-id="6fd3e-236">Een uitvoerbaar ad kan worden geïnitialiseerd met behulp van de <AdParameters> element in de <Linear> of <NonLinear> elementen in een antwoord VAST.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-236">An executable ad can be initialized using the <AdParameters> element within the <Linear> or <NonLinear> elements in a VAST response.</span></span> <span data-ttu-id="6fd3e-237">Voor meer informatie over de <AdParameters> element, Zie [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).</span><span class="sxs-lookup"><span data-stu-id="6fd3e-237">For more information on the <AdParameters> element, see [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).</span></span> <span data-ttu-id="6fd3e-238">Zie voor meer informatie over de API VPAID [VPAID 2.0](http://www.iab.net/media/file/VPAID_2.0_Final_04-10-2012.pdf).</span><span class="sxs-lookup"><span data-stu-id="6fd3e-238">For more information about the VPAID API, see [VPAID 2.0](http://www.iab.net/media/file/VPAID_2.0_Final_04-10-2012.pdf).</span></span>

## <a name="implementing-a-windows-or-windows-phone-8-player-with-ad-support"></a><span data-ttu-id="6fd3e-239">Implementatie van een Windows- of Windows Phone 8-speler met Ad-ondersteuning</span><span class="sxs-lookup"><span data-stu-id="6fd3e-239">Implementing a Windows or Windows Phone 8 Player with Ad Support</span></span>
<span data-ttu-id="6fd3e-240">Het Microsoft-Media-Platform: Player Framework voor Windows 8 en Windows Phone 8 bevat een verzameling voorbeeldtoepassingen die wordt beschreven hoe u met het implementeren van een video player-toepassing met behulp van het framework.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-240">The Microsoft Media Platform: Player Framework for Windows 8 and Windows Phone 8 contains a collection of sample applications that show you how to implement a video player application using the framework.</span></span> <span data-ttu-id="6fd3e-241">U kunt downloaden de Player-Framework en de voorbeelden van [Player Framework voor Windows 8 en Windows Phone 8](https://playerframework.codeplex.com).</span><span class="sxs-lookup"><span data-stu-id="6fd3e-241">You can download the Player Framework and the samples from [Player Framework for Windows 8 and Windows Phone 8](https://playerframework.codeplex.com).</span></span>

<span data-ttu-id="6fd3e-242">Wanneer u de oplossing Microsoft.PlayerFramework.Xaml.Samples opent ziet u een aantal mappen in het project.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-242">When you open the Microsoft.PlayerFramework.Xaml.Samples solution you will see a number of folders within the project.</span></span> <span data-ttu-id="6fd3e-243">De reclame-map bevat de voorbeeldcode die relevant zijn voor het maken van een video-speler met ad-ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-243">The Advertising folder contains the sample code relevant to creating a video player with ad support.</span></span> <span data-ttu-id="6fd3e-244">In de reclame is map een aantal XAML/cs bestanden die laten zien hoe advertenties invoegen in een andere manier.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-244">Inside the Advertising folder is a number of XAML/cs files each of which show how to insert ads in a different way.</span></span> <span data-ttu-id="6fd3e-245">De volgende lijst beschrijft elke:</span><span class="sxs-lookup"><span data-stu-id="6fd3e-245">The following list describes each:</span></span>

* <span data-ttu-id="6fd3e-246">AdPodPage.xaml laat zien hoe een schil ad weergeven.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-246">AdPodPage.xaml Shows how to display an ad pod.</span></span>
* <span data-ttu-id="6fd3e-247">AdSchedulingPage.xaml laat zien hoe advertenties plannen.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-247">AdSchedulingPage.xaml Shows how to schedule ads.</span></span>
* <span data-ttu-id="6fd3e-248">FreeWheelPage.xaml laat zien hoe de invoegtoepassing FreeWheel gebruiken voor het plannen van advertenties.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-248">FreeWheelPage.xaml Shows how to use the FreeWheel plugin to schedule ads.</span></span>
* <span data-ttu-id="6fd3e-249">MastPage.xaml laat zien hoe advertenties met een bestand b plannen.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-249">MastPage.xaml Shows how to schedule ads with a MAST file.</span></span>
* <span data-ttu-id="6fd3e-250">ProgrammaticAdPage.xaml laat zien hoe programmatisch advertenties plannen in een video.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-250">ProgrammaticAdPage.xaml Shows how to programmatically schedule ads into a video.</span></span>
* <span data-ttu-id="6fd3e-251">ScheduleClipPage.xaml laat zien hoe plannen van een ad zonder een groot bestand.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-251">ScheduleClipPage.xaml Shows how to schedule an ad without a VAST file.</span></span>
* <span data-ttu-id="6fd3e-252">VastLinearCompanionPage.xaml ziet u hoe u kunt een lineaire invoegen en companion ad.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-252">VastLinearCompanionPage.xaml Shows how to insert a linear and companion ad.</span></span>
* <span data-ttu-id="6fd3e-253">VastNonLinearPage.xaml laat zien hoe een niet-lineaire ad invoegen.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-253">VastNonLinearPage.xaml Shows how to insert a non-linear ad.</span></span>
* <span data-ttu-id="6fd3e-254">VmapPage.xaml laat zien hoe advertenties met een VMAP-bestand opgeven.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-254">VmapPage.xaml Shows how to specify ads with a VMAP file.</span></span>

<span data-ttu-id="6fd3e-255">Elk van deze voorbeelden maakt gebruik van de Media Player-klasse die is gedefinieerd door het player-framework.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-255">Each of these samples uses the MediaPlayer class defined by the player framework.</span></span> <span data-ttu-id="6fd3e-256">De meeste voorbeelden gebruiken invoegtoepassingen die ondersteuning voor verschillende indelingen met ad-antwoord toevoegen.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-256">Most samples use plugins that add support for various ad response formats.</span></span> <span data-ttu-id="6fd3e-257">Het voorbeeld ProgrammaticAdPage communiceert via een programma met een exemplaar van de Media Player.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-257">The ProgrammaticAdPage sample programmatically interacts with a MediaPlayer instance.</span></span>

### <a name="adpodpage-sample"></a><span data-ttu-id="6fd3e-258">Voorbeeld van AdPodPage</span><span class="sxs-lookup"><span data-stu-id="6fd3e-258">AdPodPage Sample</span></span>
<span data-ttu-id="6fd3e-259">Dit voorbeeld gebruikt de AdSchedulerPlugin om te bepalen bij het weergeven van een advertentie.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-259">This sample uses the AdSchedulerPlugin to define when to display an ad.</span></span> <span data-ttu-id="6fd3e-260">In dit voorbeeld wordt een aankondiging halverwege roll gepland wordt afgespeeld na 5 seconden.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-260">In this example a mid-roll advertisement is scheduled to be played after 5 seconds.</span></span> <span data-ttu-id="6fd3e-261">De ad-schil (een groep van advertenties in volgorde) is opgegeven in een ENORME bestand geretourneerd van een ad-server.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-261">The ad pod (a group of ads to display in order) is specified in a VAST file returned from an ad server.</span></span> <span data-ttu-id="6fd3e-262">De URI naar de ENORME bestand is opgegeven in de <RemoteAdSource> element.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-262">The URI to the VAST file is specified in the <RemoteAdSource> element.</span></span>

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

<span data-ttu-id="6fd3e-263">Zie voor meer informatie over de AdSchedulerPlugin [reclame in het kader Player op Windows 8 en Windows Phone 8](http://playerframework.codeplex.com/wikipage?title=Advertising&referringTitle=Windows%208%20Player%20Documentation)</span><span class="sxs-lookup"><span data-stu-id="6fd3e-263">For more information about the AdSchedulerPlugin, see [Advertising in the Player Framework on Windows 8 and Windows Phone 8](http://playerframework.codeplex.com/wikipage?title=Advertising&referringTitle=Windows%208%20Player%20Documentation)</span></span>

### <a name="adschedulingpage"></a><span data-ttu-id="6fd3e-264">AdSchedulingPage</span><span class="sxs-lookup"><span data-stu-id="6fd3e-264">AdSchedulingPage</span></span>
<span data-ttu-id="6fd3e-265">Dit voorbeeld gebruikt ook de AdSchedulerPlugin.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-265">This sample also uses the AdSchedulerPlugin.</span></span> <span data-ttu-id="6fd3e-266">Hiermee plant u drie advertenties, een vooraf roll ad, een tussentijdse roll ad en een advertentie na doorvoeren.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-266">It schedules three ads, a pre-roll ad, a mid-roll ad, and a post-roll ad.</span></span> <span data-ttu-id="6fd3e-267">De URI moet de VAST voor elke advertentie is opgegeven in een <RemoteAdSource> element.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-267">The URI to the VAST for each ad is specified in a <RemoteAdSource> element.</span></span>

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


### <a name="freewheelpage"></a><span data-ttu-id="6fd3e-268">FreeWheelPage</span><span class="sxs-lookup"><span data-stu-id="6fd3e-268">FreeWheelPage</span></span>
<span data-ttu-id="6fd3e-269">Dit voorbeeld gebruikt de FreeWheelPlugin waarin een kenmerk van de gegevensbron die een URI die verwijst naar een bestand SmartXML waarmee ad inhoud, evenals gegevens over de planning ad aangeeft.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-269">This sample uses the FreeWheelPlugin which specifies a Source attribute that specifies a URI that points to a SmartXML file that specifies ad content as well as ad scheduling information.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:FreeWheelPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/freewheel.xml"/>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="mastpage"></a><span data-ttu-id="6fd3e-270">MastPage</span><span class="sxs-lookup"><span data-stu-id="6fd3e-270">MastPage</span></span>
<span data-ttu-id="6fd3e-271">Dit voorbeeld gebruikt de MastSchedulerPlugin waarmee u een b-bestand te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-271">This sample uses the MastSchedulerPlugin that allows you to use a MAST file.</span></span> <span data-ttu-id="6fd3e-272">Het bronkenmerk geeft de locatie van de b-bestand.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-272">The Source attribute specifies the location of the MAST file.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:MastSchedulerPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/mast.xml" />
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="programmaticadpage"></a><span data-ttu-id="6fd3e-273">ProgrammaticAdPage</span><span class="sxs-lookup"><span data-stu-id="6fd3e-273">ProgrammaticAdPage</span></span>
<span data-ttu-id="6fd3e-274">Dit voorbeeld communiceert via een programma met de Media Player.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-274">This sample programmatically interacts with the MediaPlayer.</span></span> <span data-ttu-id="6fd3e-275">Het bestand ProgrammaticAdPage.xaml instantieert de Media Player:</span><span class="sxs-lookup"><span data-stu-id="6fd3e-275">The ProgrammaticAdPage.xaml file instantiates the MediaPlayer:</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4"/>

<span data-ttu-id="6fd3e-276">Het bestand ProgrammaticAdPage.xaml.cs maakt een AdHandlerPlugin voegt een TimelineMarker om op te geven wanneer een advertentie moet worden weergegeven en worden vervolgens toegevoegd een handler voor de gebeurtenis MarkerReached die een RemoteAdSource opgeven van een URI naar een groot bestand wordt geladen en de advertentie wordt afgespeeld.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-276">The ProgrammaticAdPage.xaml.cs file creates an AdHandlerPlugin, adds a TimelineMarker to specify when an ad should be displayed, and then adds a handler for the MarkerReached event which loads a RemoteAdSource specifying a URI to a VAST file, and then plays the ad.</span></span>

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

### <a name="scheduleclippage"></a><span data-ttu-id="6fd3e-277">ScheduleClipPage</span><span class="sxs-lookup"><span data-stu-id="6fd3e-277">ScheduleClipPage</span></span>
<span data-ttu-id="6fd3e-278">Dit voorbeeld gebruikt de AdSchedulerPlugin een advertentie halverwege roll plannen door op te geven van een WMV-bestand met de ad.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-278">This sample uses the AdSchedulerPlugin to schedule a mid-roll ad by specifying a .wmv file that contains the ad.</span></span>

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

### <a name="vastlinearcompanionpage"></a><span data-ttu-id="6fd3e-279">VastLinearCompanionPage</span><span class="sxs-lookup"><span data-stu-id="6fd3e-279">VastLinearCompanionPage</span></span>
<span data-ttu-id="6fd3e-280">Dit voorbeeld ziet u hoe de AdSchedulerPlugin gebruiken voor het plannen van een lineaire ad halverwege rollen met een aanvullende ad.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-280">This sample illustrates how to use the AdSchedulerPlugin to schedule a mid-roll linear ad with an companion ad.</span></span> <span data-ttu-id="6fd3e-281">De <RemoteAdSource> element geeft de locatie van het bestand VAST.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-281">The <RemoteAdSource> element specifies the location of the VAST file.</span></span>

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

### <a name="vastlinearnonlinearpage"></a><span data-ttu-id="6fd3e-282">VastLinearNonLinearPage</span><span class="sxs-lookup"><span data-stu-id="6fd3e-282">VastLinearNonLinearPage</span></span>
<span data-ttu-id="6fd3e-283">Dit voorbeeld gebruikt de AdSchedulerPlugin een lineaire plannen en een niet-lineaire ad.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-283">This sample uses the AdSchedulerPlugin to schedule a linear and a non-linear ad.</span></span> <span data-ttu-id="6fd3e-284">De meeste bestandslocatie is opgegeven met de <RemoteAdSource> element.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-284">The VAST file location is specified with the <RemoteAdSource> element.</span></span>

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

### <a name="vmappage"></a><span data-ttu-id="6fd3e-285">VMAPPage</span><span class="sxs-lookup"><span data-stu-id="6fd3e-285">VMAPPage</span></span>
<span data-ttu-id="6fd3e-286">Deze voorbeelden maakt gebruik van de VmapSchedulerPlugin advertenties met behulp van een bestand VMAP plannen.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-286">This samples uses the VmapSchedulerPlugin to schedule ads using a VMAP file.</span></span> <span data-ttu-id="6fd3e-287">De URI naar het bestand VMAP is opgegeven in het bronkenmerk van de <VmapSchedulerPlugin> element.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-287">The URI to the VMAP file is specified in the Source attribute of the <VmapSchedulerPlugin> element.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:VmapSchedulerPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/vmap.xml"/>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

## <a name="implementing-an-ios-video-player-with-ad-support"></a><span data-ttu-id="6fd3e-288">Implementatie van een iOS-Video Player met Ad-ondersteuning</span><span class="sxs-lookup"><span data-stu-id="6fd3e-288">Implementing an iOS Video Player with Ad Support</span></span>
<span data-ttu-id="6fd3e-289">Het Microsoft-Media-Platform: Player Framework voor iOS bevat een verzameling van de voorbeeldtoepassingen die wordt beschreven hoe u met het implementeren van een video player-toepassing met behulp van het framework.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-289">The Microsoft Media Platform: Player Framework for iOS contains a collection of sample applications that show you how to implement a video player application using the framework.</span></span> <span data-ttu-id="6fd3e-290">U kunt downloaden de Player-Framework en de voorbeelden van [Azure Media Player Framework](https://github.com/Azure/azure-media-player-framework).</span><span class="sxs-lookup"><span data-stu-id="6fd3e-290">You can download the Player Framework and the samples from [Azure Media Player Framework](https://github.com/Azure/azure-media-player-framework).</span></span> <span data-ttu-id="6fd3e-291">De github-pagina heeft een koppeling naar een Wiki met aanvullende informatie van het framework player en een inleiding tot het player-voorbeeld: [Azure Media Player Wiki](https://github.com/Azure/azure-media-player-framework/wiki/How-to-use-Azure-media-player-framework).</span><span class="sxs-lookup"><span data-stu-id="6fd3e-291">The github page has a link to a Wiki that contains additional information on the player framework and an introduction to the player sample: [Azure Media Player Wiki](https://github.com/Azure/azure-media-player-framework/wiki/How-to-use-Azure-media-player-framework).</span></span>

### <a name="scheduling-ads-with-vmap"></a><span data-ttu-id="6fd3e-292">Advertenties met VMAP plannen</span><span class="sxs-lookup"><span data-stu-id="6fd3e-292">Scheduling Ads with VMAP</span></span>
<span data-ttu-id="6fd3e-293">Het volgende voorbeeld laat zien hoe advertenties met behulp van een bestand VMAP plannen.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-293">The following example shows how to schedule ads using a VMAP file.</span></span>

    // How to schedule an Ad using VMAP.
    //First download the VMAP manifest

    if (![framework.adResolver downloadManifest:&manifest withURL:[NSURL URLWithString:@"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVMAP.xml"]])
            {
                [self logFrameworkError];
            }
            else
            {
                // Schedule a list of ads using the downloaded VMAP manifest
                if (![framework scheduleVMAPWithManifest:manifest])
                {
                    [self logFrameworkError];
                }          
            }

### <a name="scheduling-ads-with-vast"></a><span data-ttu-id="6fd3e-294">Advertenties met VAST plannen</span><span class="sxs-lookup"><span data-stu-id="6fd3e-294">Scheduling Ads with VAST</span></span>
<span data-ttu-id="6fd3e-295">Het volgende voorbeeld laat zien hoe een late binding VAST ad plannen.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-295">The following sample shows how to schedule a late binding VAST ad.</span></span>

    //Example:3 How to schedule a late binding VAST ad.
    // set the start time for the ad
    adLinearTime.startTime = 13;
    adLinearTime.duration = 0;
    // Specify the URI of the VAST file
    NSString *vastAd1=@"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml";
    // Create an AdInfo object
     AdInfo *vastAdInfo1 = [[[AdInfo alloc] init] autorelease];
    // set URL to VAST file
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

   <span data-ttu-id="6fd3e-296">Het volgende voorbeeld laat zien hoe een vroege binding VAST ad plannen.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-296">The following sample shows how to schedule an early binding VAST ad.</span></span>
<span data-ttu-id="6fd3e-297">Voorbeeld: 4 planning een vroege binding VAST ad //Download de VAST bestand indien (! [ framework.adResolver downloadManifest: & manifest withURL: [NSURL URLWithString: @ 'http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml']]) {[self logFrameworkError];} else {adLinearTime.startTime = 7; adLinearTime.duration = 0;</span><span class="sxs-lookup"><span data-stu-id="6fd3e-297">//Example:4 Schedule an early binding VAST ad //Download the VAST file if (![framework.adResolver downloadManifest:&manifest withURL:[NSURL URLWithString:@"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml"]]) { [self logFrameworkError]; } else { adLinearTime.startTime = 7; adLinearTime.duration = 0;</span></span>

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

<span data-ttu-id="6fd3e-298">Het volgende voorbeeld toont het invoegen van een ad dat gebruikmaakt van ruwe knippen bewerkt (Dwingen)</span><span class="sxs-lookup"><span data-stu-id="6fd3e-298">The following sample shows how to insert an ad using Rough Cut Editing (RCE)</span></span>

    //Example:1 How to use RCE.
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

<span data-ttu-id="6fd3e-299">Het volgende voorbeeld laat zien hoe een schil ad plannen.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-299">The following example shows how to schedule an ad pod.</span></span>

    //Example:5 Schedule an ad Pod.
    // Set start time for ad
    adLinearTime.startTime = 23;
    adLinearTime.duration = 0;

    // Specify URL to content
    NSString *adpodSt1=@"https://portalvhdsq3m25bf47d15c.blob.core.windows.net/asset-e47b43fd-05dc-4587-ac87-5916439ad07f/Windows%208_%20Cliffjumpers.mp4?st=2012-11-28T16%3A31%3A57Z&se=2014-11-28T16%3A31%3A57Z&sr=c&si=2a6dbb1e-f906-4187-a3d3-7e517192cbd0&sig=qrXYZBekqlbbYKqwovxzaVZNLv9cgyINgMazSCbdrfU%3D";
    // Create an AdInfo instance
    AdInfo *adpodInfo1 = [[[AdInfo alloc] init] autorelease];
    // set URI to ad content
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

<span data-ttu-id="6fd3e-300">Het volgende voorbeeld laat zien hoe een niet-tijdelijke halverwege roll ad plannen.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-300">The following example shows how to schedule a non-sticky mid-roll ad.</span></span> <span data-ttu-id="6fd3e-301">Een niet-tijdelijke ad alleen afgespeeld wanneer ongeacht eventuele zoeken de viewer wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-301">A non-sticky ad is only played once regardless of any seeking the viewer performs.</span></span>

    //Example:6 Schedule a single non sticky mid roll Ad
    // specify URL to content
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

<span data-ttu-id="6fd3e-302">Het volgende voorbeeld laat zien hoe een tijdelijke halverwege roll ad plannen.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-302">The following example shows how to schedule a sticky mid-roll ad.</span></span> <span data-ttu-id="6fd3e-303">Een tijdelijke ad weergegeven telkens wanneer die het opgegeven punt op de video tijdlijn is bereikt.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-303">A sticky ad will be displayed each time the specified point on the video timeline is reached.</span></span>

    //Example:7 Schedule a single sticky mid roll Ad
    NSString *stickyAd=@"http://wamsblureg001orig-hs.cloudapp.net/2e4e7d1f-b72a-4994-a406-810c796fc4fc/The%20Surface%20Movement-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";
    // create AdInfo instance
    AdInfo *stickyAdInfo = [[[AdInfo alloc] init] autorelease];
    // set URI to ad
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


<span data-ttu-id="6fd3e-304">Het volgende voorbeeld laat zien hoe een advertentie na roll plannen.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-304">The following sample shows how to schedule a post-roll ad.</span></span>

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

<span data-ttu-id="6fd3e-305">Het volgende voorbeeld toont hoe u een vooraf roll ad plant.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-305">The following sample shows how to schedule a pre-roll ad.</span></span>

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

<span data-ttu-id="6fd3e-306">Het volgende voorbeeld laat zien hoe een advertentie halverwege roll overlay plannen.</span><span class="sxs-lookup"><span data-stu-id="6fd3e-306">The following sample shows how to schedule a mid-roll overlay ad.</span></span>

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



## <a name="media-services-learning-paths"></a><span data-ttu-id="6fd3e-307">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="6fd3e-307">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="6fd3e-308">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="6fd3e-308">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="6fd3e-309">Zie ook</span><span class="sxs-lookup"><span data-stu-id="6fd3e-309">See Also</span></span>
[<span data-ttu-id="6fd3e-310">Videospelertoepassingen ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="6fd3e-310">Develop video player applications</span></span>](media-services-develop-video-players.md)

