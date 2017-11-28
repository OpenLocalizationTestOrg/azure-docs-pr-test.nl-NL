---
title: aaaBridge Android webweergave met systeemeigen Mobile Engagement Android SDK
description: Beschrijft hoe een brug tussen webweergave toocreate uitgevoerd Javascript en Hallo systeemeigen Mobile Engagement Android SDK
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: cf272f3f-2b09-41b1-b190-944cdca8bba2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: a7a09bcc156490fe69ad29a67809745dcfc22da6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="bridge-android-webview-with-native-mobile-engagement-android-sdk"></a><span data-ttu-id="b01cb-103">Android webweergave Bridge met systeemeigen Mobile Engagement Android SDK</span><span class="sxs-lookup"><span data-stu-id="b01cb-103">Bridge Android WebView with native Mobile Engagement Android SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b01cb-104">Android-brug</span><span class="sxs-lookup"><span data-stu-id="b01cb-104">Android Bridge</span></span>](mobile-engagement-bridge-webview-native-android.md)
> * [<span data-ttu-id="b01cb-105">iOS-brug</span><span class="sxs-lookup"><span data-stu-id="b01cb-105">iOS Bridge</span></span>](mobile-engagement-bridge-webview-native-ios.md)
> 
> 

<span data-ttu-id="b01cb-106">Sommige mobiele apps zijn ontworpen als een app hybride waarbij Hallo app zelf is ontwikkeld met behulp van systeemeigen Android-ontwikkeling, maar enkele of zelfs alle Hallo schermen binnen een webweergave Android worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="b01cb-106">Some mobile apps are designed as a hybrid app where hello app itself is developed using native Android development but some or even all of hello screens are rendered within an Android WebView.</span></span> <span data-ttu-id="b01cb-107">U kunt nog steeds Mobile Engagement Android SDK verbruiken binnen deze apps en deze zelfstudie wordt beschreven hoe toogo over dit te doen.</span><span class="sxs-lookup"><span data-stu-id="b01cb-107">You can still consume Mobile Engagement Android SDK within such apps and this tutorial describes how toogo about doing this.</span></span> <span data-ttu-id="b01cb-108">Hallo voorbeeldcode hieronder is gebaseerd op Hallo Android documentatie [hier](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript).</span><span class="sxs-lookup"><span data-stu-id="b01cb-108">hello sample code below is based on hello Android documentation [here](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript).</span></span> <span data-ttu-id="b01cb-109">Hierin wordt beschreven hoe deze gedocumenteerde benadering kan worden gebruikt tooimplement Hallo dezelfde voor Mobile Engagement Android SDK van veelgebruikte methoden zodat een webweergave in een hybride-app kan ook worden geïnitieerd aanvragen tootrack gebeurtenissen, taken, fouten, app-info terwijl ze via sluizen onze Android SDK.</span><span class="sxs-lookup"><span data-stu-id="b01cb-109">It describes how this documented approach could be used tooimplement hello same for Mobile Engagement Android SDK's commonly used methods such that a Webview from a hybrid app can also initiate requests tootrack events, jobs, errors, app-info while piping them via our Android SDK.</span></span> 

1. <span data-ttu-id="b01cb-110">Ten eerste moet u tooensure die u hebt doorlopen onze [zelfstudie aan de slag](mobile-engagement-android-get-started.md) toointegrate Hallo Mobile Engagement Android SDK in uw hybride-app.</span><span class="sxs-lookup"><span data-stu-id="b01cb-110">First of all, you need tooensure that you have gone through our [Getting Started tutorial](mobile-engagement-android-get-started.md) toointegrate hello Mobile Engagement Android SDK in your hybrid app.</span></span> <span data-ttu-id="b01cb-111">Als u dit doen, uw `OnCreate` methode Hallo volgende eruit.</span><span class="sxs-lookup"><span data-stu-id="b01cb-111">Once you do that, your `OnCreate` method will look like hello following.</span></span>  
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("<Mobile Engagement Conn String>");
            EngagementAgent.getInstance(this).init(engagementConfiguration);
        }
2. <span data-ttu-id="b01cb-112">Controleren of dat uw hybride-app een scherm met een webweergave is geïnstalleerd op.</span><span class="sxs-lookup"><span data-stu-id="b01cb-112">Now make sure that your hybrid app has a screen with a WebView on it.</span></span> <span data-ttu-id="b01cb-113">Hallo code zijn vergelijkbaar toohello volgende waar we een lokaal HTML-bestand worden geladen **Sample.html** in Hallo webweergave in Hallo `onCreate` methode van het scherm.</span><span class="sxs-lookup"><span data-stu-id="b01cb-113">hello code for it will be similar toohello following where we are loading a local HTML file **Sample.html** in hello Webview in hello `onCreate` method of your screen.</span></span> 
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
        }
   
        protected void onCreate(Bundle savedInstanceState) {
            ...
            ...
            SetWebView();
        }
3. <span data-ttu-id="b01cb-114">Maakt nu een bestand met de naam bridge **WebAppInterface** Hallo met Mobile Engagement Android SDK-methoden die Hiermee maakt u een wrapper voor sommige vaak gebruikt `@JavascriptInterface` benadering wordt beschreven in Hallo [Android-documentatie ](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript):</span><span class="sxs-lookup"><span data-stu-id="b01cb-114">Now create a bridge file called **WebAppInterface** which creates a wrapper over some commonly used Mobile Engagement Android SDK methods using hello `@JavascriptInterface` approach described in hello [Android documentation](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript):</span></span>
   
        import android.content.Context;
        import android.os.Bundle;
        import android.util.Log;
        import android.webkit.JavascriptInterface;
   
        import com.microsoft.azure.engagement.EngagementAgent;
   
        import org.json.JSONArray;
        import org.json.JSONObject;
   
        public class WebAppInterface {
            Context mContext;
   
            /** Instantiate hello interface and set hello context */
            WebAppInterface(Context c) {
                mContext = c;
            }
   
            @JavascriptInterface
            public void sendEngagementEvent(String name, String extras ){
                EngagementAgent.getInstance(mContext).sendEvent(name, ParseExtras(extras));
            }
   
            @JavascriptInterface
            public void startEngagementJob(String name, String extras ){
                EngagementAgent.getInstance(mContext).startJob(name, ParseExtras(extras));
            }
   
            @JavascriptInterface
            public void endEngagementJob(String name){
                EngagementAgent.getInstance(mContext).endJob(name);
            }
   
            @JavascriptInterface
            public void sendEngagementError(String name, String extras ){
                EngagementAgent.getInstance(mContext).sendError(name, ParseExtras(extras));
            }
   
            @JavascriptInterface
            public void sendEngagementAppInfo(String appInfo){
                EngagementAgent.getInstance(mContext).sendAppInfo(ParseExtras(appInfo));
            }
   
            public Bundle ParseExtras(String input) {
                Bundle extras = new Bundle();
   
                try {
                    JSONObject jObject = new JSONObject(input);
                    extras.putString(jObject.names().getString(0),
                            jObject.get(jObject.names().getString(0)).toString());
                } catch (Exception e) {
                    e.printStackTrace();
                }
                return extras;
            }
        }  
4. <span data-ttu-id="b01cb-115">Wanneer we Hallo hierboven bridge-bestand hebt gemaakt, moeten we tooensure dat deze gekoppeld aan onze webweergave is.</span><span class="sxs-lookup"><span data-stu-id="b01cb-115">Once we have created hello above bridge file, we need tooensure that it is associated with our Webview.</span></span> <span data-ttu-id="b01cb-116">Voor deze toohappen, moet u tooedit uw `SetWebview` methode zodat het Hallo volgende lijkt:</span><span class="sxs-lookup"><span data-stu-id="b01cb-116">For this toohappen, you need tooedit your `SetWebview` method so that it looks like hello following:</span></span>
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
            WebSettings webSettings = myWebView.getSettings();
            webSettings.setJavaScriptEnabled(true);
            myWebView.addJavascriptInterface(new WebAppInterface(this), "EngagementJs");
        }
5. <span data-ttu-id="b01cb-117">In Hallo bovenstaande codefragment we genoemd `addJavascriptInterface` tooassociate onze bridge klasse met onze webweergave en ook gemaakt een ingang aangeroepen **EngagementJs** toocall Hallo methoden van Hallo bridge-bestand.</span><span class="sxs-lookup"><span data-stu-id="b01cb-117">In hello above snippet, we called `addJavascriptInterface` tooassociate our bridge class with our Webview and also created a handle called **EngagementJs** toocall hello methods from hello bridge file.</span></span> 
6. <span data-ttu-id="b01cb-118">Maak nu Hallo na bestand met de naam **Sample.html** in uw project in een map genaamd **activa** die in het Hallo webweergave wordt geladen en waar we bellen Hallo methoden van Hallo bridge-bestand.</span><span class="sxs-lookup"><span data-stu-id="b01cb-118">Now create hello following file called **Sample.html** in your project in a folder called **assets** which is loaded into hello Webview and where we will call hello methods from hello bridge file.</span></span>
   
        <!doctype html>
        <html>
            <head>
                <style type='text/css'>
                    html { font-family:Helvetica; color:#222; }
                    h1 { color:steelblue; font-size:22px; margin-top:16px; }
                    h2 { color:grey; font-size:14px; margin-top:18px; margin-bottom:0px; }
                </style>
   
                <script type="text/javascript">
   
                    window.onerror = function(err)
                    {
                      log('window.onerror: ' + err);
                    }
   
                    send = function(inputId)
                    {
                        var input = document.getElementById(inputId);
                        if(input)
                        {
                            var value = input.value;
                            // Example of how extras info can be passed with hello Engagement logs
                            var extras = '{"CustomerId":"MS290011"}';
   
                            if(value && value.length > 0)
                            {
                                switch(inputId)
                                {
                                    case "event":
                                    EngagementJs.sendEngagementEvent(value, extras);
                                    break;
   
                                    case "job":
                                    EngagementJs.startEngagementJob(value, extras);
                                    window.setTimeout( function()
                                    {
                                      EngagementJs.endEngagementJob(value);
                                    }, 10000 );
                                    break;
   
                                    case "error":
                                    EngagementJs.sendEngagementError(value, extras);
                                    break;
   
                                    case "appInfo":
                                    EngagementJs.sendEngagementAppInfo({"customer_name":value});
                                    break;
                                }
                            }
                        }
                    }
                </script>
            </head>
            <body>
                <h1>Bridge Tester</h1>
                <div id='engagement'>
                    <h2>Event</h2>
                    <input type="text" id="event" size="35">
                    <button onclick="send('event')">Send</button>
   
                    <h2>Job</h2>
                    <input type="text" id="job" size="35">
                    <button onclick="send('job')">Send</button>
   
                    <h2>Error</h2>
                    <input type="text" id="error" size="35">
                    <button onclick="send('error')">Send</button>
   
                    <h2>AppInfo</h2>
                    <input type="text" id="appInfo" size="35">
                    <button onclick="send('appInfo')">Send</button>
                </div>
            </body>
        </html>
7. <span data-ttu-id="b01cb-119">Opmerking Hallo volgende verwijst over bovenstaande Hallo HTML-bestand:</span><span class="sxs-lookup"><span data-stu-id="b01cb-119">Note hello following points about hello HTML file above:</span></span>
   
   * <span data-ttu-id="b01cb-120">Het bevat een set van invoervakken waarin u gegevens toobe gebruikt als namen voor de gebeurtenis, taak, fout, AppInfo kunt opgeven.</span><span class="sxs-lookup"><span data-stu-id="b01cb-120">It contains a set of input boxes where you can provide data toobe used as names for your Event, Job, Error, AppInfo.</span></span> <span data-ttu-id="b01cb-121">Wanneer u op volgende tooit van Hallo knop klikt, wordt een aanroep toohello Javascript die uiteindelijk Hallo methoden vanuit Hallo bridge bestand toopass deze toohello aanroep van Mobile Engagement Android SDK aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="b01cb-121">When you click on hello button next tooit, a call is made toohello Javascript which eventually calls hello methods from hello bridge file toopass this call toohello Mobile Engagement Android SDK.</span></span> 
   * <span data-ttu-id="b01cb-122">We zijn op bepaalde statische extra info toohello gebeurtenissen, taken en zelfs fouten toodemonstrate tagging hoe dit kan worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b01cb-122">We are tagging on some static extra info toohello events, jobs and even errors toodemonstrate how this could be done.</span></span> <span data-ttu-id="b01cb-123">Deze extra gegevens als een JSON-tekenreeks die wordt verzonden als u in Hallo zoeken `WebAppInterface` bestand wordt geparseerd en plaatsen in een Android `Bundle` en samen met het verzenden van gebeurtenissen, taken, fouten wordt doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="b01cb-123">This extra info is sent as a JSON string which, if you look in hello `WebAppInterface` file, is parsed and put in an Android `Bundle` and is passed along with sending Events, Jobs, Errors.</span></span> 
   * <span data-ttu-id="b01cb-124">Een Mobile Engagement-taak wordt gestart met de naam van de Hallo u opgeeft in het invoervak hello, uitgevoerd voor 10 seconden en afsluiten.</span><span class="sxs-lookup"><span data-stu-id="b01cb-124">A Mobile Engagement Job is kicked off with hello name you specify in hello input box, run for 10 seconds and shut down.</span></span> 
   * <span data-ttu-id="b01cb-125">Een Mobile Engagement appinfo of tag wordt doorgegeven met 'customer_name' als statische Hallo-sleutel en Hallo-waarde die u hebt ingevoerd in de invoer Hallo Hallo-waarde voor Hallo-tag.</span><span class="sxs-lookup"><span data-stu-id="b01cb-125">A Mobile Engagement appinfo or tag is passed with 'customer_name' as hello static key and hello value that you entered in hello input as hello value for hello tag.</span></span> 
8. <span data-ttu-id="b01cb-126">Voer Hallo-app en u ziet Hallo volgende.</span><span class="sxs-lookup"><span data-stu-id="b01cb-126">Run hello app and you will see hello following.</span></span> <span data-ttu-id="b01cb-127">Nu bieden een naam voor een testgebeurtenis zoals Hallo volgende en klik op **verzenden** eronder.</span><span class="sxs-lookup"><span data-stu-id="b01cb-127">Now provide some name for a test event like hello following and click **Send** below it.</span></span> 
   
    ![][1]
9. <span data-ttu-id="b01cb-128">Nu wanneer u toohello gaat **Monitor** tabblad van uw app en kijk onder **Events -> Details**, ziet u deze gebeurtenis weergegeven samen met de Hallo statische toepassingsgegevens die we sturen.</span><span class="sxs-lookup"><span data-stu-id="b01cb-128">Now if you go toohello **Monitor** tab of your app and look under **Events -> Details**, you will see this event show up along with hello static app-info that we are sending.</span></span> 
   
   ![][2]

<!-- Images. -->
[1]: ./media/mobile-engagement-bridge-webview-native-android/sending-event.png
[2]: ./media/mobile-engagement-bridge-webview-native-android/event-output.png
