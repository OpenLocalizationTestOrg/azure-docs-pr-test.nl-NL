---
title: Smooth Streaming-invoegtoepassing voor de Media Open-Source Framework
description: Informatie over het gebruik van de Azure Media Services Smooth Streaming-invoegtoepassing voor Adobe Open Source Media Framework.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 6068151f-b6b0-4507-9346-f03416d3d572
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: 9c764f176ae75085320882de3fb26d8e7d52daaf
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-the-microsoft-smooth-streaming-plugin-for-the-adobe-open-source-media-framework"></a><span data-ttu-id="04ad7-103">Het gebruik van de Microsoft-Smooth Streaming-invoegtoepassing voor Adobe Open-Source Media Framework</span><span class="sxs-lookup"><span data-stu-id="04ad7-103">How to Use the Microsoft Smooth Streaming Plugin for the Adobe Open Source Media Framework</span></span>
## <a name="overview"></a><span data-ttu-id="04ad7-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="04ad7-104">Overview</span></span>
<span data-ttu-id="04ad7-105">De Microsoft Smooth Streaming-invoegtoepassing voor Open Source Media Framework 2.0 (SS voor OSMF) breidt de voorzieningen standaard van OSMF en inhoud afspelen Microsoft Smooth Streaming naar nieuwe en bestaande OSMF spelers toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="04ad7-105">The Microsoft Smooth Streaming plugin for Open Source Media Framework 2.0 (SS for OSMF) extends the default capabilities of OSMF and adds Microsoft Smooth Streaming content playback to new and existing OSMF players.</span></span> <span data-ttu-id="04ad7-106">De invoegtoepassing worden Smooth Streaming afspelen mogelijkheden ook toegevoegd aan stroboscoop Media afspelen (SMP).</span><span class="sxs-lookup"><span data-stu-id="04ad7-106">The plugin also adds Smooth Streaming playback capabilities to Strobe Media Playback (SMP).</span></span>

<span data-ttu-id="04ad7-107">SS voor OSMF bevat twee versies van de invoegtoepassing:</span><span class="sxs-lookup"><span data-stu-id="04ad7-107">SS for OSMF includes two versions of plugin:</span></span>

* <span data-ttu-id="04ad7-108">Statische Smooth Streaming-invoegtoepassing voor OSMF (SWC)</span><span class="sxs-lookup"><span data-stu-id="04ad7-108">Static Smooth Streaming plugin for OSMF (.swc)</span></span>
* <span data-ttu-id="04ad7-109">Dynamische Smooth Streaming-invoegtoepassing voor OSMF (.swf)</span><span class="sxs-lookup"><span data-stu-id="04ad7-109">Dynamic Smooth Streaming plugin for OSMF (.swf)</span></span>

<span data-ttu-id="04ad7-110">Dit document wordt ervan uitgegaan dat de lezer een algemene praktische kennis van OSMF en OSMF heeft invoegtoepassingen. Voor meer informatie over OSMF, Raadpleeg de documentatie van de [officiële OSMF site](http://osmf.org/).</span><span class="sxs-lookup"><span data-stu-id="04ad7-110">This document assumes that the reader has a general working knowledge of OSMF and OSMF plug-ins. For more information about OSMF, please see the documentation on the [official OSMF site](http://osmf.org/).</span></span>

### <a name="smooth-streaming-plugin-for-osmf-20"></a><span data-ttu-id="04ad7-111">Smooth Streaming-invoegtoepassing voor OSMF 2.0</span><span class="sxs-lookup"><span data-stu-id="04ad7-111">Smooth Streaming plugin for OSMF 2.0</span></span>
<span data-ttu-id="04ad7-112">De invoegtoepassing biedt ondersteuning voor laden en afspelen van Smooth Streaming inhoud op aanvraag met de volgende functies:</span><span class="sxs-lookup"><span data-stu-id="04ad7-112">The plugin supports loading and playback of on-demand Smooth Streaming content with the following features:</span></span>

* <span data-ttu-id="04ad7-113">Afspelen op aanvraag Smooth Streaming (Play, onderbreken, Seek, Stop)</span><span class="sxs-lookup"><span data-stu-id="04ad7-113">On-demand Smooth Streaming playback (Play, Pause, Seek, Stop)</span></span>
* <span data-ttu-id="04ad7-114">Live afspelen Smooth Streaming (Play)</span><span class="sxs-lookup"><span data-stu-id="04ad7-114">Live Smooth Streaming playback (Play)</span></span>
* <span data-ttu-id="04ad7-115">Live DVR-functies (onderbreken, Seek, DVR afspelen, Ga-to-Live)</span><span class="sxs-lookup"><span data-stu-id="04ad7-115">Live DVR functions (Pause, Seek, DVR Playback, Go-to-Live)</span></span>
* <span data-ttu-id="04ad7-116">Ondersteuning voor een video-codecs - H.264</span><span class="sxs-lookup"><span data-stu-id="04ad7-116">Support for video codecs - H.264</span></span>
* <span data-ttu-id="04ad7-117">Ondersteuning voor audiocodecs - AAC</span><span class="sxs-lookup"><span data-stu-id="04ad7-117">Support for Audio codecs - AAC</span></span>
* <span data-ttu-id="04ad7-118">Meerdere audio taal overschakelen met ingebouwde OSMF-API 's</span><span class="sxs-lookup"><span data-stu-id="04ad7-118">Multiple audio language switching with OSMF built-in APIs</span></span>
* <span data-ttu-id="04ad7-119">Maximale afspelen kwaliteit selectie met ingebouwde OSMF-API 's</span><span class="sxs-lookup"><span data-stu-id="04ad7-119">Max playback quality selection with OSMF built-in APIs</span></span>
* <span data-ttu-id="04ad7-120">Ter gesloten bijschriften met OSMF bijschriften-invoegtoepassing</span><span class="sxs-lookup"><span data-stu-id="04ad7-120">Sidecar closed captions with OSMF captions plugin</span></span>
* <span data-ttu-id="04ad7-121">Adobe&reg; Flash&reg; Player 11,4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="04ad7-121">Adobe&reg; Flash&reg; Player 11.4 or higher.</span></span>
* <span data-ttu-id="04ad7-122">Deze versie ondersteunt alleen OSMF 2.0.</span><span class="sxs-lookup"><span data-stu-id="04ad7-122">This version only supports OSMF 2.0.</span></span>

## <a name="supported-features-and-known-issues"></a><span data-ttu-id="04ad7-123">Ondersteunde functies en bekende problemen</span><span class="sxs-lookup"><span data-stu-id="04ad7-123">Supported features and known issues</span></span>
<span data-ttu-id="04ad7-124">Raadpleeg voor een volledige lijst van ondersteunde functies, niet-ondersteunde functies en bekende problemen [dit document](http://download.microsoft.com/download/3/1/B/31B63D97-574E-4A8D-BF8D-170744181724/Smooth_Streaming_Plugin_for_OSMF.pdf).</span><span class="sxs-lookup"><span data-stu-id="04ad7-124">For a full list of supported features, unsupported features and known issues, refer to [this document](http://download.microsoft.com/download/3/1/B/31B63D97-574E-4A8D-BF8D-170744181724/Smooth_Streaming_Plugin_for_OSMF.pdf).</span></span>

## <a name="loading-the-plugin"></a><span data-ttu-id="04ad7-125">Bij het laden van de invoegtoepassing</span><span class="sxs-lookup"><span data-stu-id="04ad7-125">Loading the Plugin</span></span>
<span data-ttu-id="04ad7-126">OSMF invoegtoepassingen kunnen worden geladen (op het tijdstip van compilatie) statisch of dynamisch (tijdens runtime).</span><span class="sxs-lookup"><span data-stu-id="04ad7-126">OSMF plugins can be loaded statically (at compile time) or dynamically (at run-time).</span></span> <span data-ttu-id="04ad7-127">De invoegtoepassing Smooth Streaming OSMF downloaden bevat versies van dynamische en statische.</span><span class="sxs-lookup"><span data-stu-id="04ad7-127">The Smooth Streaming plugin for OSMF download includes both dynamic and static versions.</span></span>

* <span data-ttu-id="04ad7-128">Statische laden: als u wilt laden statisch, een statische bibliotheek (SWC)-bestand is vereist.</span><span class="sxs-lookup"><span data-stu-id="04ad7-128">Static loading: To load statically, a static library (SWC) file is required.</span></span> <span data-ttu-id="04ad7-129">Statische plugins worden toegevoegd als een verwijzing naar de projecten en samenvoegen in de uiteindelijke uitvoer-bestand op het moment van compileren.</span><span class="sxs-lookup"><span data-stu-id="04ad7-129">Static plugins are added as a reference to the projects and merge inside the final output file at the compile time.</span></span>
* <span data-ttu-id="04ad7-130">Dynamisch laden: dynamische taakverdeling, een vooraf gecompileerde (SWF)-bestand is vereist.</span><span class="sxs-lookup"><span data-stu-id="04ad7-130">Dynamic loading: To load dynamically, a precompiled (SWF) file is required.</span></span> <span data-ttu-id="04ad7-131">Dynamische invoegtoepassingen zijn geladen in de runtime en niet zijn opgenomen in de projectuitvoer.</span><span class="sxs-lookup"><span data-stu-id="04ad7-131">Dynamic plugins are loaded in the runtime and not included in the project output.</span></span> <span data-ttu-id="04ad7-132">(Gecompileerde uitvoer) Dynamische invoegtoepassingen kunnen worden geladen met behulp van HTTP- en protocollen.</span><span class="sxs-lookup"><span data-stu-id="04ad7-132">(Compiled output) Dynamic plugins can be loaded using HTTP and FILE protocols.</span></span>

<span data-ttu-id="04ad7-133">Zie voor meer informatie over statische en dynamische laden de officiële [OSMF invoegtoepassing pagina](http://osmf.org/dev/osmf/OtherPDFs/osmf_plugin_dev_guide.pdf).</span><span class="sxs-lookup"><span data-stu-id="04ad7-133">For more information on static and dynamic loading, see the official [OSMF plugin page](http://osmf.org/dev/osmf/OtherPDFs/osmf_plugin_dev_guide.pdf).</span></span>

### <a name="ss-for-osmf-static-loading"></a><span data-ttu-id="04ad7-134">SS voor OSMF statische laden</span><span class="sxs-lookup"><span data-stu-id="04ad7-134">SS for OSMF Static Loading</span></span>
<span data-ttu-id="04ad7-135">Het onderstaande codefragment laat zien hoe de invoegtoepassing SS statisch voor OSMF laden en een basic video met behulp van de klasse OSMF MediaFactory afspelen.</span><span class="sxs-lookup"><span data-stu-id="04ad7-135">The code snippet below shows how to load the SS plugin for OSMF statically and play a basic video using OSMF MediaFactory class.</span></span> <span data-ttu-id="04ad7-136">Voordat u met inbegrip van de SS voor OSMF code, zorg ervoor dat het project een verwijzing de statische 'MSAdaptiveStreamingPlugin v1.0.3 osmf2.0.swc'-invoegtoepassing bevat.</span><span class="sxs-lookup"><span data-stu-id="04ad7-136">Before including the SS for OSMF code, please ensure that the project reference includes the "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc" static plugin.</span></span>

```
package 
{

    import com.microsoft.azure.media.AdaptiveStreamingPluginInfo;

    import flash.display.*;
    import org.osmf.media.*;
    import org.osmf.containers.MediaContainer;
    import org.osmf.events.MediaErrorEvent;
    import org.osmf.events.MediaFactoryEvent;
    import org.osmf.events.MediaPlayerStateChangeEvent;
    import org.osmf.layout.*;



    [SWF(width="1024", height="768", backgroundColor='#405050', frameRate="25")]
    public class TestPlayer extends Sprite
    {        
        public var _container:MediaContainer;
        public var _mediaFactory:DefaultMediaFactory;
        private var _mediaPlayerSprite:MediaPlayerSprite;


        public function TestPlayer( )
        {
            stage.quality = StageQuality.HIGH;

            initMediaPlayer();

        }

        private function initMediaPlayer():void
        {

            // Create the container (sprite) for managing display and layout
            _mediaPlayerSprite = new MediaPlayerSprite();    
            _mediaPlayerSprite.addEventListener(MediaErrorEvent.MEDIA_ERROR, onPlayerFailed);
            _mediaPlayerSprite.addEventListener(MediaPlayerStateChangeEvent.MEDIA_PLAYER_STATE_CHANGE, onPlayerStateChange);
            _mediaPlayerSprite.scaleMode = ScaleMode.NONE;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;
            //Adds the container to the stage
            addChild(_mediaPlayerSprite);

            // Create a mediafactory instance
            _mediaFactory = new DefaultMediaFactory();

            // Add the listeners for PLUGIN_LOADING
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD,onPluginLoaded);
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD_ERROR, onPluginLoadFailed );

            // Load the plugin class 
            loadAdaptiveStreamingPlugin( );  

        }

        private function loadAdaptiveStreamingPlugin( ):void
        {
            var pluginResource:MediaResourceBase;

            pluginResource = new PluginInfoResource(new AdaptiveStreamingPluginInfo( )); 
            _mediaFactory.loadPlugin( pluginResource ); 
        }

        private function onPluginLoaded( event:MediaFactoryEvent ):void
        {
            // The plugin is loaded successfully.
            // Your web server needs to host a valid crossdomain.xml file to allow plugin to download Smooth Streaming files.
        loadMediaSource("http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest")

        }

        private function onPluginLoadFailed( event:MediaFactoryEvent ):void
        {
            // The plugin is failed to load ...
        }


        private function onPlayerStateChange(event:MediaPlayerStateChangeEvent) : void
        {
            var state:String;

            state =  event.state;

            switch (state)
            {
                case MediaPlayerState.LOADING: 

                    // A new source is started to load.

                    break;

                case  MediaPlayerState.READY :   
                    // Add code to deal with Player Ready when it is hit the first load after a source is loaded. 

                    break;

                case MediaPlayerState.BUFFERING :

                    break;

                case  MediaPlayerState.PAUSED :
                    break;      
                // other states ...          
            }
        }

        private function onPlayerFailed(event:MediaErrorEvent) : void
        {
            // Media Player is failed .           
        }

        private function loadMediaSource(sourceURL : String):void 
        {
            // Take an URL of SmoothStreamingSource's manifest and add it to the page.

            var resource:URLResource= new URLResource( sourceURL );

            var element:MediaElement = _mediaFactory.createMediaElement( resource );
            _mediaPlayerSprite.scaleMode = ScaleMode.LETTERBOX;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;

            // Add the media element
            _mediaPlayerSprite.media = element;
        }     

    }
}
```


### <a name="ss-for-osmf-dynamic-loading"></a><span data-ttu-id="04ad7-137">SS voor OSMF dynamisch laden</span><span class="sxs-lookup"><span data-stu-id="04ad7-137">SS for OSMF Dynamic Loading</span></span>
<span data-ttu-id="04ad7-138">Het onderstaande codefragment laat zien hoe de SS-invoegtoepassing voor OSMF dynamisch laden en een eenvoudige afspelen video met behulp van de klasse OSMF MediaFactory.</span><span class="sxs-lookup"><span data-stu-id="04ad7-138">The code snippet below shows how to load the SS plugin for OSMF dynamically and play a basic video using the OSMF MediaFactory class.</span></span> <span data-ttu-id="04ad7-139">Voordat u met inbegrip van de SS voor OSMF code, de dynamische invoegtoepassing 'MSAdaptiveStreamingPlugin v1.0.3 osmf2.0.swf' naar de projectmap kopiëren als u wilt laden met bestandsprotocol of kopieer onder een webserver voor HTTP-belasting.</span><span class="sxs-lookup"><span data-stu-id="04ad7-139">Before including the SS for OSMF code, copy the "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" dynamic plugin to the project folder if you want to load using FILE protocol, or copy under a web server for HTTP load.</span></span> <span data-ttu-id="04ad7-140">Er is niet nodig om op te nemen 'MSAdaptiveStreamingPlugin v1.0.3 osmf2.0.swc' in de projectverwijzingen.</span><span class="sxs-lookup"><span data-stu-id="04ad7-140">There is no need to include "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc" in the project references.</span></span>

<span data-ttu-id="04ad7-141">{het pakket</span><span class="sxs-lookup"><span data-stu-id="04ad7-141">package {</span></span>

    import flash.display.*;
    import org.osmf.media.*;
    import org.osmf.containers.MediaContainer;
    import org.osmf.events.MediaErrorEvent;
    import org.osmf.events.MediaFactoryEvent;
    import org.osmf.events.MediaPlayerStateChangeEvent;
    import org.osmf.layout.*;
    import flash.events.Event;
    import flash.system.Capabilities;


    //Sets the size of the SWF

    [SWF(width="1024", height="768", backgroundColor='#405050', frameRate="25")]
    public class TestPlayer extends Sprite
    {        
        public var _container:MediaContainer;
        public var _mediaFactory:DefaultMediaFactory;
        private var _mediaPlayerSprite:MediaPlayerSprite;


        public function TestPlayer( )
        {
            stage.quality = StageQuality.HIGH;
            initMediaPlayer();
        }

        private function initMediaPlayer():void
        {

            // Create the container (sprite) for managing display and layout
            _mediaPlayerSprite = new MediaPlayerSprite();    
            _mediaPlayerSprite.addEventListener(MediaErrorEvent.MEDIA_ERROR, onPlayerFailed);
            _mediaPlayerSprite.addEventListener(MediaPlayerStateChangeEvent.MEDIA_PLAYER_STATE_CHANGE, onPlayerStateChange);

            //Adds the container to the stage
            addChild(_mediaPlayerSprite);

            // Create a mediafactory instance
            _mediaFactory = new DefaultMediaFactory();

            // Add the listeners for PLUGIN_LOADING
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD,onPluginLoaded);
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD_ERROR, onPluginLoadFailed );

            // Load the plugin class 
            loadAdaptiveStreamingPlugin( );  

        }

        private function loadAdaptiveStreamingPlugin( ):void
        {
            var pluginResource:MediaResourceBase;
            var adaptiveStreamingPluginUrl:String;

            // Your dynamic plugin web server needs to host a valid crossdomain.xml file to allow loading plugins.

            adaptiveStreamingPluginUrl = "http://yourdomain/MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf";
            pluginResource = new URLResource(adaptiveStreamingPluginUrl);
            _mediaFactory.loadPlugin( pluginResource ); 

        }

        private function onPluginLoaded( event:MediaFactoryEvent ):void
        {
            // The plugin is loaded successfully.

            // Your web server needs to host a valid crossdomain.xml file to allow plugin to download Smooth Streaming files.

    loadMediaSource("http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest")
        }

        private function onPluginLoadFailed( event:MediaFactoryEvent ):void
        {
            // The plugin is failed to load ...
        }


        private function onPlayerStateChange(event:MediaPlayerStateChangeEvent) : void
        {
            var state:String;

            state =  event.state;

            switch (state)
            {
                case MediaPlayerState.LOADING: 

                    // A new source is started to load.

                    break;

                case  MediaPlayerState.READY :   
                    // Add code to deal with Player Ready when it is hit the first load after a source is loaded. 

                    break;

                case MediaPlayerState.BUFFERING :

                    break;

                case  MediaPlayerState.PAUSED :
                    break;      
                // other states ...          
            }
        }

        private function onPlayerFailed(event:MediaErrorEvent) : void
        {
            // Media Player is failed .           
        }

        private function loadMediaSource(sourceURL : String):void 
        {
            // Take an URL of SmoothStreamingSource's manifest and add it to the page.

            var resource:URLResource= new URLResource( sourceURL );

            var element:MediaElement = _mediaFactory.createMediaElement( resource );
            _mediaPlayerSprite.scaleMode = ScaleMode.LETTERBOX;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;
            // Add the media element
            _mediaPlayerSprite.media = element;
        }     

    }
<span data-ttu-id="04ad7-142">}</span><span class="sxs-lookup"><span data-stu-id="04ad7-142">}</span></span>

## <a name="strobe-media--playback-with-the-ss-odmf-dynamic-plugin"></a><span data-ttu-id="04ad7-143">Stroboscoop Media afspelen met de dynamische SS ODMF-invoegtoepassing</span><span class="sxs-lookup"><span data-stu-id="04ad7-143">Strobe Media  Playback with the SS ODMF Dynamic Plugin</span></span>
<span data-ttu-id="04ad7-144">De Smooth Streaming voor dynamische OSMF-invoegtoepassing is compatibel met [stroboscoop Media afspelen (SMP)](http://osmf.org/strobe_mediaplayback.html).</span><span class="sxs-lookup"><span data-stu-id="04ad7-144">The Smooth Streaming for OSMF dynamic plugin is compatible with [Strobe Media Playback (SMP)](http://osmf.org/strobe_mediaplayback.html).</span></span> <span data-ttu-id="04ad7-145">U kunt de SS voor OSMF invoegtoepassing Smooth Streaming afspelen van inhoud toevoegen aan SMP gebruiken.</span><span class="sxs-lookup"><span data-stu-id="04ad7-145">You can use the SS for OSMF plugin to add Smooth Streaming content playback to SMP.</span></span> <span data-ttu-id="04ad7-146">U doet dit door kopiëren 'MSAdaptiveStreamingPlugin v1.0.3 osmf2.0.swf' onder een webserver voor HTTP-belasting met behulp van de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="04ad7-146">To do this, copy "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" under a web server for HTTP load using the following steps:</span></span>

1. <span data-ttu-id="04ad7-147">Bladeren de [stroboscoop Media afspelen installatiepagina](http://osmf.org/dev/2.0gm/setup.html).</span><span class="sxs-lookup"><span data-stu-id="04ad7-147">Browse the [Strobe Media Playback setup page](http://osmf.org/dev/2.0gm/setup.html).</span></span> 
2. <span data-ttu-id="04ad7-148">De src ingesteld op een bron Smooth Streaming, (bijvoorbeeld http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest)</span><span class="sxs-lookup"><span data-stu-id="04ad7-148">Set the src to a Smooth Streaming source, (e.g. http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest)</span></span> 
3. <span data-ttu-id="04ad7-149">De gewenste configuratiewijzigingen aanbrengen en klikt u op Preview en Update.</span><span class="sxs-lookup"><span data-stu-id="04ad7-149">Make the desired configuration changes and click Preview and Update.</span></span>
   
   <span data-ttu-id="04ad7-150">**Opmerking** uw webserver inhoud moet een geldige crossdomain.xml.</span><span class="sxs-lookup"><span data-stu-id="04ad7-150">**Note** Your content web server needs a valid crossdomain.xml.</span></span> 
4. <span data-ttu-id="04ad7-151">Kopieer en plak de code in een eenvoudig HTML-pagina met behulp van uw favoriete teksteditor, zoals in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="04ad7-151">Copy and paste the code to a simple HTML page using your favorite text editor, such as in the following example:</span></span>

        <html>
        <body>
        <object width="920" height="640"> 
        <param name="movie" value="http://osmf.org/dev/2.0gm/StrobeMediaPlayback.swf"></param>
        <param name="flashvars" value="src=http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest &autoPlay=true"></param>
        <param name="allowFullScreen" value="true"></param>
        <param name="allowscriptaccess" value="always"></param>
        <param name="wmode" value="direct"></param>
        <embed src="http://osmf.org/dev/2.0gm/StrobeMediaPlayback.swf" 
            type="application/x-shockwave-flash" 
            allowscriptaccess="always" 
            allowfullscreen="true" 
            wmode="direct" 
            width="920" 
            height="640" 
            flashvars=" src=http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest&autoPlay=true">
        </embed>
        </object>
        </body>
        </html>



1. <span data-ttu-id="04ad7-152">Smooth Streaming OSMF-invoegtoepassing toevoegen aan de ingesloten code en opslaan.</span><span class="sxs-lookup"><span data-stu-id="04ad7-152">Add Smooth Streaming OSMF plugin to the embed code and save.</span></span>
   
        <html>
        <object width="920" height="640"> 
        <param name="movie" value="http://osmf.org/dev/2.0gm/StrobeMediaPlayback.swf"></param>
        <param name="flashvars" value="src=http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest&autoPlay=true&plugin_AdaptiveStreamingPlugin=http://yourdomain/MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf&AdaptiveStreamingPlugin_retryLive=true&AdaptiveStreamingPlugin_retryInterval=10"></param>
        <param name="allowFullScreen" value="true"></param>
        <param name="allowscriptaccess" value="always"></param>
        <param name="wmode" value="direct"></param>
        <embed src="http://osmf.org/dev/2.0gm/StrobeMediaPlayback.swf" 
            type="application/x-shockwave-flash" 
            allowscriptaccess="always" 
            allowfullscreen="true" 
            wmode="direct" 
            width="920" 
            height="640" 
            flashvars="src=http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest&autoPlay=true&plugin_AdaptiveStreamingPlugin=http://yourdomain/MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf&AdaptiveStreamingPlugin_retryLive=true&AdaptiveStreamingPlugin_retryInterval=10">
        </embed>
        </object>
        </html>
2. <span data-ttu-id="04ad7-153">De HTML-pagina opslaan en publiceren naar een webserver.</span><span class="sxs-lookup"><span data-stu-id="04ad7-153">Save your HTML page and publish to a web server.</span></span> <span data-ttu-id="04ad7-154">Blader naar de gepubliceerde webpagina met uw favoriete Flash&reg; Player ingeschakeld internetbrowser (Internet Explorer, Chrome, Firefox, enzovoort).</span><span class="sxs-lookup"><span data-stu-id="04ad7-154">Browse to the published web page using your favorite Flash&reg; Player enabled Internet browser (Internet Explorer, Chrome, Firefox, so on).</span></span>
3. <span data-ttu-id="04ad7-155">Profiteer van Smooth Streaming inhoud in Adobe&reg; Flash&reg; Player.</span><span class="sxs-lookup"><span data-stu-id="04ad7-155">Enjoy Smooth Streaming content inside Adobe&reg; Flash&reg; Player.</span></span>

<span data-ttu-id="04ad7-156">Zie voor meer informatie over algemene OSMF ontwikkeling de officiële [OSMF ontwikkeling pagina](http://osmf.org/resources.html).</span><span class="sxs-lookup"><span data-stu-id="04ad7-156">For more information on general OSMF development, please see the official [OSMF development page](http://osmf.org/resources.html).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="04ad7-157">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="04ad7-157">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="04ad7-158">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="04ad7-158">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="04ad7-159">Zie ook</span><span class="sxs-lookup"><span data-stu-id="04ad7-159">See Also</span></span>
[<span data-ttu-id="04ad7-160">Microsoft adaptieve Streaming-invoegtoepassing voor OSMF Update</span><span class="sxs-lookup"><span data-stu-id="04ad7-160">Microsoft Adaptive Streaming Plugin for OSMF Update</span></span>](https://azure.microsoft.com/blog/2014/10/27/microsoft-adaptive-streaming-plugin-for-osmf-update/) 

