---
title: aaaSmooth hello Open Source Media Framework Streaming-invoegtoepassing
description: Meer informatie over hoe toouse hello Azure Media Services Smooth Streaming-invoegtoepassing voor Hallo Adobe Open Source Media Framework.
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
ms.openlocfilehash: 3cf8e4679279344cf79c3f0e5b28f63adf88179d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-microsoft-smooth-streaming-plugin-for-hello-adobe-open-source-media-framework"></a><span data-ttu-id="51096-103">Hoe tooUse Smooth Streaming-invoegtoepassing voor Microsoft hello voor Hallo Adobe Open Source Media Framework</span><span class="sxs-lookup"><span data-stu-id="51096-103">How tooUse hello Microsoft Smooth Streaming Plugin for hello Adobe Open Source Media Framework</span></span>
## <a name="overview"></a><span data-ttu-id="51096-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="51096-104">Overview</span></span>
<span data-ttu-id="51096-105">Hallo Microsoft Smooth Streaming-invoegtoepassing voor Open Source Media Framework 2.0 (SS voor OSMF) Hallo standaard voorzieningen van OSMF breidt en inhoud afspelen toonew Microsoft Smooth Streaming en bestaande OSMF voegt spelers.</span><span class="sxs-lookup"><span data-stu-id="51096-105">hello Microsoft Smooth Streaming plugin for Open Source Media Framework 2.0 (SS for OSMF) extends hello default capabilities of OSMF and adds Microsoft Smooth Streaming content playback toonew and existing OSMF players.</span></span> <span data-ttu-id="51096-106">Hallo-invoegtoepassing ook Smooth Streaming afspelen mogelijkheden tooStrobe Media afspelen (SMP) toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="51096-106">hello plugin also adds Smooth Streaming playback capabilities tooStrobe Media Playback (SMP).</span></span>

<span data-ttu-id="51096-107">SS voor OSMF bevat twee versies van de invoegtoepassing:</span><span class="sxs-lookup"><span data-stu-id="51096-107">SS for OSMF includes two versions of plugin:</span></span>

* <span data-ttu-id="51096-108">Statische Smooth Streaming-invoegtoepassing voor OSMF (SWC)</span><span class="sxs-lookup"><span data-stu-id="51096-108">Static Smooth Streaming plugin for OSMF (.swc)</span></span>
* <span data-ttu-id="51096-109">Dynamische Smooth Streaming-invoegtoepassing voor OSMF (.swf)</span><span class="sxs-lookup"><span data-stu-id="51096-109">Dynamic Smooth Streaming plugin for OSMF (.swf)</span></span>

<span data-ttu-id="51096-110">Dit document wordt ervan uitgegaan dat de lezer Hallo algemene enige basiskennis van OSMF en OSMF invoegtoepassingen. Voor meer informatie over OSMF Zie Hallo documentatie over Hallo [officiële OSMF site](http://osmf.org/).</span><span class="sxs-lookup"><span data-stu-id="51096-110">This document assumes that hello reader has a general working knowledge of OSMF and OSMF plug-ins. For more information about OSMF, please see hello documentation on hello [official OSMF site](http://osmf.org/).</span></span>

### <a name="smooth-streaming-plugin-for-osmf-20"></a><span data-ttu-id="51096-111">Smooth Streaming-invoegtoepassing voor OSMF 2.0</span><span class="sxs-lookup"><span data-stu-id="51096-111">Smooth Streaming plugin for OSMF 2.0</span></span>
<span data-ttu-id="51096-112">Hallo-invoegtoepassing biedt ondersteuning voor laden en afspelen van Smooth Streaming inhoud op aanvraag met Hallo volgende kenmerken:</span><span class="sxs-lookup"><span data-stu-id="51096-112">hello plugin supports loading and playback of on-demand Smooth Streaming content with hello following features:</span></span>

* <span data-ttu-id="51096-113">Afspelen op aanvraag Smooth Streaming (Play, onderbreken, Seek, Stop)</span><span class="sxs-lookup"><span data-stu-id="51096-113">On-demand Smooth Streaming playback (Play, Pause, Seek, Stop)</span></span>
* <span data-ttu-id="51096-114">Live afspelen Smooth Streaming (Play)</span><span class="sxs-lookup"><span data-stu-id="51096-114">Live Smooth Streaming playback (Play)</span></span>
* <span data-ttu-id="51096-115">Live DVR-functies (onderbreken, Seek, DVR afspelen, Ga-to-Live)</span><span class="sxs-lookup"><span data-stu-id="51096-115">Live DVR functions (Pause, Seek, DVR Playback, Go-to-Live)</span></span>
* <span data-ttu-id="51096-116">Ondersteuning voor een video-codecs - H.264</span><span class="sxs-lookup"><span data-stu-id="51096-116">Support for video codecs - H.264</span></span>
* <span data-ttu-id="51096-117">Ondersteuning voor audiocodecs - AAC</span><span class="sxs-lookup"><span data-stu-id="51096-117">Support for Audio codecs - AAC</span></span>
* <span data-ttu-id="51096-118">Meerdere audio taal overschakelen met ingebouwde OSMF-API 's</span><span class="sxs-lookup"><span data-stu-id="51096-118">Multiple audio language switching with OSMF built-in APIs</span></span>
* <span data-ttu-id="51096-119">Maximale afspelen kwaliteit selectie met ingebouwde OSMF-API 's</span><span class="sxs-lookup"><span data-stu-id="51096-119">Max playback quality selection with OSMF built-in APIs</span></span>
* <span data-ttu-id="51096-120">Ter gesloten bijschriften met OSMF bijschriften-invoegtoepassing</span><span class="sxs-lookup"><span data-stu-id="51096-120">Sidecar closed captions with OSMF captions plugin</span></span>
* <span data-ttu-id="51096-121">Adobe&reg; Flash&reg; Player 11,4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="51096-121">Adobe&reg; Flash&reg; Player 11.4 or higher.</span></span>
* <span data-ttu-id="51096-122">Deze versie ondersteunt alleen OSMF 2.0.</span><span class="sxs-lookup"><span data-stu-id="51096-122">This version only supports OSMF 2.0.</span></span>

## <a name="supported-features-and-known-issues"></a><span data-ttu-id="51096-123">Ondersteunde functies en bekende problemen</span><span class="sxs-lookup"><span data-stu-id="51096-123">Supported features and known issues</span></span>
<span data-ttu-id="51096-124">Voor een volledige lijst van ondersteunde functies, niet-ondersteunde functies en bekende problemen te verwijzen[dit document](http://download.microsoft.com/download/3/1/B/31B63D97-574E-4A8D-BF8D-170744181724/Smooth_Streaming_Plugin_for_OSMF.pdf).</span><span class="sxs-lookup"><span data-stu-id="51096-124">For a full list of supported features, unsupported features and known issues, refer too[this document](http://download.microsoft.com/download/3/1/B/31B63D97-574E-4A8D-BF8D-170744181724/Smooth_Streaming_Plugin_for_OSMF.pdf).</span></span>

## <a name="loading-hello-plugin"></a><span data-ttu-id="51096-125">Hallo laden van de invoegtoepassing</span><span class="sxs-lookup"><span data-stu-id="51096-125">Loading hello Plugin</span></span>
<span data-ttu-id="51096-126">OSMF invoegtoepassingen kunnen worden geladen (op het tijdstip van compilatie) statisch of dynamisch (tijdens runtime).</span><span class="sxs-lookup"><span data-stu-id="51096-126">OSMF plugins can be loaded statically (at compile time) or dynamically (at run-time).</span></span> <span data-ttu-id="51096-127">Hallo Smooth Streaming-invoegtoepassing downloaden OSMF bevat versies van dynamische en statische.</span><span class="sxs-lookup"><span data-stu-id="51096-127">hello Smooth Streaming plugin for OSMF download includes both dynamic and static versions.</span></span>

* <span data-ttu-id="51096-128">Statische laden: tooload statisch, een statische bibliotheek (SWC)-bestand is vereist.</span><span class="sxs-lookup"><span data-stu-id="51096-128">Static loading: tooload statically, a static library (SWC) file is required.</span></span> <span data-ttu-id="51096-129">Statische plugins worden toegevoegd als een verwijzing toohello projecten en samenvoegen in de uiteindelijke uitvoer Hallo-bestand op het tijdstip van Hallo.</span><span class="sxs-lookup"><span data-stu-id="51096-129">Static plugins are added as a reference toohello projects and merge inside hello final output file at hello compile time.</span></span>
* <span data-ttu-id="51096-130">Dynamisch laden: tooload dynamisch gecompileerde (SWF) is een bestand vereist.</span><span class="sxs-lookup"><span data-stu-id="51096-130">Dynamic loading: tooload dynamically, a precompiled (SWF) file is required.</span></span> <span data-ttu-id="51096-131">Dynamische invoegtoepassingen zijn geladen in Hallo runtime en niet zijn opgenomen in de uitvoer van de Hallo-project.</span><span class="sxs-lookup"><span data-stu-id="51096-131">Dynamic plugins are loaded in hello runtime and not included in hello project output.</span></span> <span data-ttu-id="51096-132">(Gecompileerde uitvoer) Dynamische invoegtoepassingen kunnen worden geladen met behulp van HTTP- en protocollen.</span><span class="sxs-lookup"><span data-stu-id="51096-132">(Compiled output) Dynamic plugins can be loaded using HTTP and FILE protocols.</span></span>

<span data-ttu-id="51096-133">Zie voor meer informatie over statische en dynamische laden Hallo officiële [OSMF invoegtoepassing pagina](http://osmf.org/dev/osmf/OtherPDFs/osmf_plugin_dev_guide.pdf).</span><span class="sxs-lookup"><span data-stu-id="51096-133">For more information on static and dynamic loading, see hello official [OSMF plugin page](http://osmf.org/dev/osmf/OtherPDFs/osmf_plugin_dev_guide.pdf).</span></span>

### <a name="ss-for-osmf-static-loading"></a><span data-ttu-id="51096-134">SS voor OSMF statische laden</span><span class="sxs-lookup"><span data-stu-id="51096-134">SS for OSMF Static Loading</span></span>
<span data-ttu-id="51096-135">Hallo codefragment hieronder ziet u hoe tooload SS invoegtoepassing statisch voor OSMF Hallo en een basic video met behulp van de klasse OSMF MediaFactory afspelen.</span><span class="sxs-lookup"><span data-stu-id="51096-135">hello code snippet below shows how tooload hello SS plugin for OSMF statically and play a basic video using OSMF MediaFactory class.</span></span> <span data-ttu-id="51096-136">Voordat u met inbegrip van Hallo SS voor OSMF code, zorg ervoor dat projectverwijzing Hallo Hallo 'MSAdaptiveStreamingPlugin v1.0.3 osmf2.0.swc' statische invoegtoepassing bevat.</span><span class="sxs-lookup"><span data-stu-id="51096-136">Before including hello SS for OSMF code, please ensure that hello project reference includes hello "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc" static plugin.</span></span>

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

            // Create hello container (sprite) for managing display and layout
            _mediaPlayerSprite = new MediaPlayerSprite();    
            _mediaPlayerSprite.addEventListener(MediaErrorEvent.MEDIA_ERROR, onPlayerFailed);
            _mediaPlayerSprite.addEventListener(MediaPlayerStateChangeEvent.MEDIA_PLAYER_STATE_CHANGE, onPlayerStateChange);
            _mediaPlayerSprite.scaleMode = ScaleMode.NONE;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;
            //Adds hello container toohello stage
            addChild(_mediaPlayerSprite);

            // Create a mediafactory instance
            _mediaFactory = new DefaultMediaFactory();

            // Add hello listeners for PLUGIN_LOADING
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD,onPluginLoaded);
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD_ERROR, onPluginLoadFailed );

            // Load hello plugin class 
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
            // hello plugin is loaded successfully.
            // Your web server needs toohost a valid crossdomain.xml file tooallow plugin toodownload Smooth Streaming files.
        loadMediaSource("http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest")

        }

        private function onPluginLoadFailed( event:MediaFactoryEvent ):void
        {
            // hello plugin is failed tooload ...
        }


        private function onPlayerStateChange(event:MediaPlayerStateChangeEvent) : void
        {
            var state:String;

            state =  event.state;

            switch (state)
            {
                case MediaPlayerState.LOADING: 

                    // A new source is started tooload.

                    break;

                case  MediaPlayerState.READY :   
                    // Add code toodeal with Player Ready when it is hit hello first load after a source is loaded. 

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
            // Take an URL of SmoothStreamingSource's manifest and add it toohello page.

            var resource:URLResource= new URLResource( sourceURL );

            var element:MediaElement = _mediaFactory.createMediaElement( resource );
            _mediaPlayerSprite.scaleMode = ScaleMode.LETTERBOX;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;

            // Add hello media element
            _mediaPlayerSprite.media = element;
        }     

    }
}
```


### <a name="ss-for-osmf-dynamic-loading"></a><span data-ttu-id="51096-137">SS voor OSMF dynamisch laden</span><span class="sxs-lookup"><span data-stu-id="51096-137">SS for OSMF Dynamic Loading</span></span>
<span data-ttu-id="51096-138">onderstaande Hallo codefragment ziet u hoe tooload SS invoegtoepassing dynamisch Hallo voor OSMF en een eenvoudige video met behulp van Hallo OSMF MediaFactory klasse afspelen.</span><span class="sxs-lookup"><span data-stu-id="51096-138">hello code snippet below shows how tooload hello SS plugin for OSMF dynamically and play a basic video using hello OSMF MediaFactory class.</span></span> <span data-ttu-id="51096-139">Voordat u met inbegrip van Hallo SS voor OSMF code Hallo 'MSAdaptiveStreamingPlugin v1.0.3 osmf2.0.swf' dynamische invoegtoepassing toohello projectmap te kopiëren als u wilt met behulp van bestandsprotocol tooload of onder een webserver voor HTTP-belasting kopieert.</span><span class="sxs-lookup"><span data-stu-id="51096-139">Before including hello SS for OSMF code, copy hello "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" dynamic plugin toohello project folder if you want tooload using FILE protocol, or copy under a web server for HTTP load.</span></span> <span data-ttu-id="51096-140">Er is geen noodzaak tooinclude 'MSAdaptiveStreamingPlugin v1.0.3 osmf2.0.swc' in de projectverwijzingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="51096-140">There is no need tooinclude "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc" in hello project references.</span></span>

<span data-ttu-id="51096-141">{het pakket</span><span class="sxs-lookup"><span data-stu-id="51096-141">package {</span></span>

    import flash.display.*;
    import org.osmf.media.*;
    import org.osmf.containers.MediaContainer;
    import org.osmf.events.MediaErrorEvent;
    import org.osmf.events.MediaFactoryEvent;
    import org.osmf.events.MediaPlayerStateChangeEvent;
    import org.osmf.layout.*;
    import flash.events.Event;
    import flash.system.Capabilities;


    //Sets hello size of hello SWF

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

            // Create hello container (sprite) for managing display and layout
            _mediaPlayerSprite = new MediaPlayerSprite();    
            _mediaPlayerSprite.addEventListener(MediaErrorEvent.MEDIA_ERROR, onPlayerFailed);
            _mediaPlayerSprite.addEventListener(MediaPlayerStateChangeEvent.MEDIA_PLAYER_STATE_CHANGE, onPlayerStateChange);

            //Adds hello container toohello stage
            addChild(_mediaPlayerSprite);

            // Create a mediafactory instance
            _mediaFactory = new DefaultMediaFactory();

            // Add hello listeners for PLUGIN_LOADING
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD,onPluginLoaded);
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD_ERROR, onPluginLoadFailed );

            // Load hello plugin class 
            loadAdaptiveStreamingPlugin( );  

        }

        private function loadAdaptiveStreamingPlugin( ):void
        {
            var pluginResource:MediaResourceBase;
            var adaptiveStreamingPluginUrl:String;

            // Your dynamic plugin web server needs toohost a valid crossdomain.xml file tooallow loading plugins.

            adaptiveStreamingPluginUrl = "http://yourdomain/MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf";
            pluginResource = new URLResource(adaptiveStreamingPluginUrl);
            _mediaFactory.loadPlugin( pluginResource ); 

        }

        private function onPluginLoaded( event:MediaFactoryEvent ):void
        {
            // hello plugin is loaded successfully.

            // Your web server needs toohost a valid crossdomain.xml file tooallow plugin toodownload Smooth Streaming files.

    loadMediaSource("http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest")
        }

        private function onPluginLoadFailed( event:MediaFactoryEvent ):void
        {
            // hello plugin is failed tooload ...
        }


        private function onPlayerStateChange(event:MediaPlayerStateChangeEvent) : void
        {
            var state:String;

            state =  event.state;

            switch (state)
            {
                case MediaPlayerState.LOADING: 

                    // A new source is started tooload.

                    break;

                case  MediaPlayerState.READY :   
                    // Add code toodeal with Player Ready when it is hit hello first load after a source is loaded. 

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
            // Take an URL of SmoothStreamingSource's manifest and add it toohello page.

            var resource:URLResource= new URLResource( sourceURL );

            var element:MediaElement = _mediaFactory.createMediaElement( resource );
            _mediaPlayerSprite.scaleMode = ScaleMode.LETTERBOX;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;
            // Add hello media element
            _mediaPlayerSprite.media = element;
        }     

    }
<span data-ttu-id="51096-142">}</span><span class="sxs-lookup"><span data-stu-id="51096-142">}</span></span>

## <a name="strobe-media--playback-with-hello-ss-odmf-dynamic-plugin"></a><span data-ttu-id="51096-143">Stroboscoop Media afspelen Hello SS ODMF dynamische invoegtoepassing</span><span class="sxs-lookup"><span data-stu-id="51096-143">Strobe Media  Playback with hello SS ODMF Dynamic Plugin</span></span>
<span data-ttu-id="51096-144">Hallo Smooth Streaming voor dynamische OSMF-invoegtoepassing is compatibel met [stroboscoop Media afspelen (SMP)](http://osmf.org/strobe_mediaplayback.html).</span><span class="sxs-lookup"><span data-stu-id="51096-144">hello Smooth Streaming for OSMF dynamic plugin is compatible with [Strobe Media Playback (SMP)](http://osmf.org/strobe_mediaplayback.html).</span></span> <span data-ttu-id="51096-145">U kunt Hallo SS voor OSMF invoegtoepassing tooadd Smooth Streaming inhoud afspelen tooSMP gebruiken.</span><span class="sxs-lookup"><span data-stu-id="51096-145">You can use hello SS for OSMF plugin tooadd Smooth Streaming content playback tooSMP.</span></span> <span data-ttu-id="51096-146">toodo deze, kopie 'MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf' onder een webserver voor HTTP-belasting met Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="51096-146">toodo this, copy "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" under a web server for HTTP load using hello following steps:</span></span>

1. <span data-ttu-id="51096-147">Hallo Bladeren [stroboscoop Media afspelen installatiepagina](http://osmf.org/dev/2.0gm/setup.html).</span><span class="sxs-lookup"><span data-stu-id="51096-147">Browse hello [Strobe Media Playback setup page](http://osmf.org/dev/2.0gm/setup.html).</span></span> 
2. <span data-ttu-id="51096-148">Set Hallo src tooa Smooth Streaming bron (bijvoorbeeld http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest)</span><span class="sxs-lookup"><span data-stu-id="51096-148">Set hello src tooa Smooth Streaming source, (e.g. http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest)</span></span> 
3. <span data-ttu-id="51096-149">Hallo gewenst configuratiewijzigingen aanbrengen en klikt u op Preview en Update.</span><span class="sxs-lookup"><span data-stu-id="51096-149">Make hello desired configuration changes and click Preview and Update.</span></span>
   
   <span data-ttu-id="51096-150">**Opmerking** uw webserver inhoud moet een geldige crossdomain.xml.</span><span class="sxs-lookup"><span data-stu-id="51096-150">**Note** Your content web server needs a valid crossdomain.xml.</span></span> 
4. <span data-ttu-id="51096-151">Kopieer en plak Hallo code tooa eenvoudig HTML-pagina met behulp van uw favoriete teksteditor, zoals in het volgende voorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="51096-151">Copy and paste hello code tooa simple HTML page using your favorite text editor, such as in hello following example:</span></span>

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



1. <span data-ttu-id="51096-152">Toevoegen van Smooth Streaming OSMF invoegtoepassing toohello invoegcode en op te slaan.</span><span class="sxs-lookup"><span data-stu-id="51096-152">Add Smooth Streaming OSMF plugin toohello embed code and save.</span></span>
   
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
2. <span data-ttu-id="51096-153">De HTML-pagina opslaan en publiceren van tooa-webserver.</span><span class="sxs-lookup"><span data-stu-id="51096-153">Save your HTML page and publish tooa web server.</span></span> <span data-ttu-id="51096-154">Bladeren toohello gepubliceerde webpagina met uw favoriete Flash&reg; Player ingeschakeld internetbrowser (Internet Explorer, Chrome, Firefox, enzovoort).</span><span class="sxs-lookup"><span data-stu-id="51096-154">Browse toohello published web page using your favorite Flash&reg; Player enabled Internet browser (Internet Explorer, Chrome, Firefox, so on).</span></span>
3. <span data-ttu-id="51096-155">Profiteer van Smooth Streaming inhoud in Adobe&reg; Flash&reg; Player.</span><span class="sxs-lookup"><span data-stu-id="51096-155">Enjoy Smooth Streaming content inside Adobe&reg; Flash&reg; Player.</span></span>

<span data-ttu-id="51096-156">Zie voor meer informatie over algemene OSMF ontwikkeling Hallo officiële [OSMF ontwikkeling pagina](http://osmf.org/resources.html).</span><span class="sxs-lookup"><span data-stu-id="51096-156">For more information on general OSMF development, please see hello official [OSMF development page](http://osmf.org/resources.html).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="51096-157">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="51096-157">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="51096-158">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="51096-158">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="51096-159">Zie ook</span><span class="sxs-lookup"><span data-stu-id="51096-159">See Also</span></span>
[<span data-ttu-id="51096-160">Microsoft adaptieve Streaming-invoegtoepassing voor OSMF Update</span><span class="sxs-lookup"><span data-stu-id="51096-160">Microsoft Adaptive Streaming Plugin for OSMF Update</span></span>](https://azure.microsoft.com/blog/2014/10/27/microsoft-adaptive-streaming-plugin-for-osmf-update/) 

