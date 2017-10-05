---
title: Android webweergave Bridge met systeemeigen Mobile Engagement Android SDK
description: Beschrijft hoe u maakt een brug tussen webweergave met Javascript en de systeemeigen Mobile Engagement Android SDK
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
ms.openlocfilehash: f4fc7b3c81747ec80974a99084eeb1acc311f11f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="bridge-android-webview-with-native-mobile-engagement-android-sdk"></a><span data-ttu-id="e7aa9-103">Android webweergave Bridge met systeemeigen Mobile Engagement Android SDK</span><span class="sxs-lookup"><span data-stu-id="e7aa9-103">Bridge Android WebView with native Mobile Engagement Android SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e7aa9-104">Android-brug</span><span class="sxs-lookup"><span data-stu-id="e7aa9-104">Android Bridge</span></span>](mobile-engagement-bridge-webview-native-android.md)
> * [<span data-ttu-id="e7aa9-105">iOS-brug</span><span class="sxs-lookup"><span data-stu-id="e7aa9-105">iOS Bridge</span></span>](mobile-engagement-bridge-webview-native-ios.md)
> 
> 

<span data-ttu-id="e7aa9-106">Sommige mobiele apps zijn ontworpen als een hybride-app waarin de app zelf is ontwikkeld met behulp van systeemeigen Android-ontwikkeling, maar sommige of zelfs alle van de schermen worden weergegeven binnen een webweergave Android.</span><span class="sxs-lookup"><span data-stu-id="e7aa9-106">Some mobile apps are designed as a hybrid app where the app itself is developed using native Android development but some or even all of the screens are rendered within an Android WebView.</span></span> <span data-ttu-id="e7aa9-107">U kunt nog steeds Mobile Engagement Android SDK verbruiken binnen deze apps en deze zelfstudie wordt beschreven hoe gaat over dit te doen.</span><span class="sxs-lookup"><span data-stu-id="e7aa9-107">You can still consume Mobile Engagement Android SDK within such apps and this tutorial describes how to go about doing this.</span></span> <span data-ttu-id="e7aa9-108">De onderstaande voorbeeldcode is gebaseerd op de Android-documentatie [hier](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript).</span><span class="sxs-lookup"><span data-stu-id="e7aa9-108">The sample code below is based on the Android documentation [here](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript).</span></span> <span data-ttu-id="e7aa9-109">Hierin wordt beschreven hoe deze gedocumenteerde benadering kan worden gebruikt voor het implementeren van hetzelfde voor Mobile Engagement Android SDK van veelgebruikte methoden zodat een webweergave in een hybride-app ook aanvragen Houd gebeurtenissen, taken, fouten, app-info terwijl ze via onze Android SDK sluizen kan initiëren.</span><span class="sxs-lookup"><span data-stu-id="e7aa9-109">It describes how this documented approach could be used to implement the same for Mobile Engagement Android SDK's commonly used methods such that a Webview from a hybrid app can also initiate requests to track events, jobs, errors, app-info while piping them via our Android SDK.</span></span> 

1. <span data-ttu-id="e7aa9-110">Ten eerste moet u ervoor zorgen dat u hebt doorlopen onze [zelfstudie aan de slag](mobile-engagement-android-get-started.md) voor het integreren van de Mobile Engagement Android SDK in uw hybride-app.</span><span class="sxs-lookup"><span data-stu-id="e7aa9-110">First of all, you need to ensure that you have gone through our [Getting Started tutorial](mobile-engagement-android-get-started.md) to integrate the Mobile Engagement Android SDK in your hybrid app.</span></span> <span data-ttu-id="e7aa9-111">Als u dit doen, uw `OnCreate` methode ziet er als volgt.</span><span class="sxs-lookup"><span data-stu-id="e7aa9-111">Once you do that, your `OnCreate` method will look like the following.</span></span>  
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("<Mobile Engagement Conn String>");
            EngagementAgent.getInstance(this).init(engagementConfiguration);
        }
2. <span data-ttu-id="e7aa9-112">Controleren of dat uw hybride-app een scherm met een webweergave is geïnstalleerd op.</span><span class="sxs-lookup"><span data-stu-id="e7aa9-112">Now make sure that your hybrid app has a screen with a WebView on it.</span></span> <span data-ttu-id="e7aa9-113">De code voor deze zijn vergelijkbaar met het volgende waar we een lokaal HTML-bestand worden geladen **Sample.html** in de webweergave in de `onCreate` methode van het scherm.</span><span class="sxs-lookup"><span data-stu-id="e7aa9-113">The code for it will be similar to the following where we are loading a local HTML file **Sample.html** in the Webview in the `onCreate` method of your screen.</span></span> 
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
        }
   
        protected void onCreate(Bundle savedInstanceState) {
            ...
            ...
            SetWebView();
        }
3. <span data-ttu-id="e7aa9-114">Maak nu een brug bestand met de naam **WebAppInterface** met behulp van Mobile Engagement Android SDK-methoden die Hiermee maakt u een wrapper voor sommige vaak gebruikt de `@JavascriptInterface` benadering wordt beschreven in de [Android documentatie](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript):</span><span class="sxs-lookup"><span data-stu-id="e7aa9-114">Now create a bridge file called **WebAppInterface** which creates a wrapper over some commonly used Mobile Engagement Android SDK methods using the `@JavascriptInterface` approach described in the [Android documentation](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript):</span></span>
   
        import android.content.Context;
        import android.os.Bundle;
        import android.util.Log;
        import android.webkit.JavascriptInterface;
   
        import com.microsoft.azure.engagement.EngagementAgent;
   
        import org.json.JSONArray;
        import org.json.JSONObject;
   
        public class WebAppInterface {
            Context mContext;
   
            /** Instantiate the interface and set the context */
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
4. <span data-ttu-id="e7aa9-115">Nadat we de bovenstaande bridge-bestand hebt gemaakt, moeten we ervoor te zorgen dat deze gekoppeld aan onze webweergave is.</span><span class="sxs-lookup"><span data-stu-id="e7aa9-115">Once we have created the above bridge file, we need to ensure that it is associated with our Webview.</span></span> <span data-ttu-id="e7aa9-116">Dit gebeurt, moet u uw `SetWebview` methode zodat deze er als volgt:</span><span class="sxs-lookup"><span data-stu-id="e7aa9-116">For this to happen, you need to edit your `SetWebview` method so that it looks like the following:</span></span>
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
            WebSettings webSettings = myWebView.getSettings();
            webSettings.setJavaScriptEnabled(true);
            myWebView.addJavascriptInterface(new WebAppInterface(this), "EngagementJs");
        }
5. <span data-ttu-id="e7aa9-117">In het bovenstaande codefragment we aangeroepen `addJavascriptInterface` onze klasse bridge koppelen aan onze webweergave en ook een ingang aangeroepen gemaakt **EngagementJs** de methoden uit het bestand bridge aanroepen.</span><span class="sxs-lookup"><span data-stu-id="e7aa9-117">In the above snippet, we called `addJavascriptInterface` to associate our bridge class with our Webview and also created a handle called **EngagementJs** to call the methods from the bridge file.</span></span> 
6. <span data-ttu-id="e7aa9-118">Maak nu het volgende bestand aangeroepen **Sample.html** in uw project in een map genaamd **activa** die in de webweergave wordt geladen en waar noemen we de methoden uit het bestand bridge.</span><span class="sxs-lookup"><span data-stu-id="e7aa9-118">Now create the following file called **Sample.html** in your project in a folder called **assets** which is loaded into the Webview and where we will call the methods from the bridge file.</span></span>
   
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
                            // Example of how extras info can be passed with the Engagement logs
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
7. <span data-ttu-id="e7aa9-119">Houd rekening met de volgende punten over het bovenstaande HTML-bestand:</span><span class="sxs-lookup"><span data-stu-id="e7aa9-119">Note the following points about the HTML file above:</span></span>
   
   * <span data-ttu-id="e7aa9-120">Het bevat een set van invoervakken waarin u gegevens moet worden gebruikt als namen voor de gebeurtenis, taak, fout, AppInfo kunt opgeven.</span><span class="sxs-lookup"><span data-stu-id="e7aa9-120">It contains a set of input boxes where you can provide data to be used as names for your Event, Job, Error, AppInfo.</span></span> <span data-ttu-id="e7aa9-121">Wanneer u op de knop ernaast klikt, wordt een aanroep Javascript die uiteindelijk de methoden aanroept vanuit het bestand bridge om door te geven deze aanroep van Mobile Engagement Android SDK.</span><span class="sxs-lookup"><span data-stu-id="e7aa9-121">When you click on the button next to it, a call is made to the Javascript which eventually calls the methods from the bridge file to pass this call to the Mobile Engagement Android SDK.</span></span> 
   * <span data-ttu-id="e7aa9-122">We zijn labels op sommige statische extra gegevens op de gebeurtenissen, taken en zelfs fouten ter illustratie van hoe deze kan worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e7aa9-122">We are tagging on some static extra info to the events, jobs and even errors to demonstrate how this could be done.</span></span> <span data-ttu-id="e7aa9-123">Deze extra gegevens als een JSON-tekenreeks die wordt verzonden als u zoeken in de `WebAppInterface` bestand wordt geparseerd en plaatsen in een Android `Bundle` en samen met het verzenden van gebeurtenissen, taken, fouten wordt doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="e7aa9-123">This extra info is sent as a JSON string which, if you look in the `WebAppInterface` file, is parsed and put in an Android `Bundle` and is passed along with sending Events, Jobs, Errors.</span></span> 
   * <span data-ttu-id="e7aa9-124">Een Mobile Engagement-taak wordt gestart met de naam die u opgeeft in het invoervak voor tien seconden uitgevoerd en afsluiten.</span><span class="sxs-lookup"><span data-stu-id="e7aa9-124">A Mobile Engagement Job is kicked off with the name you specify in the input box, run for 10 seconds and shut down.</span></span> 
   * <span data-ttu-id="e7aa9-125">Een Mobile Engagement appinfo of tag wordt doorgegeven met 'customer_name' als de statische sleutel en de waarde die u hebt ingevoerd in de invoerclaimset als de waarde voor het label.</span><span class="sxs-lookup"><span data-stu-id="e7aa9-125">A Mobile Engagement appinfo or tag is passed with 'customer_name' as the static key and the value that you entered in the input as the value for the tag.</span></span> 
8. <span data-ttu-id="e7aa9-126">Voer de app en u ziet het volgende.</span><span class="sxs-lookup"><span data-stu-id="e7aa9-126">Run the app and you will see the following.</span></span> <span data-ttu-id="e7aa9-127">Nu een naam opgeven voor een testgebeurtenis als volgt uit en klik op **verzenden** eronder.</span><span class="sxs-lookup"><span data-stu-id="e7aa9-127">Now provide some name for a test event like the following and click **Send** below it.</span></span> 
   
    ![][1]
9. <span data-ttu-id="e7aa9-128">Nu wanneer u naar de **Monitor** tabblad van uw app en kijk onder **Events -> Details**, ziet u deze gebeurtenis weergegeven samen met de statische app-gegevens die we sturen.</span><span class="sxs-lookup"><span data-stu-id="e7aa9-128">Now if you go to the **Monitor** tab of your app and look under **Events -> Details**, you will see this event show up along with the static app-info that we are sending.</span></span> 
   
   ![][2]

<!-- Images. -->
[1]: ./media/mobile-engagement-bridge-webview-native-android/sending-event.png
[2]: ./media/mobile-engagement-bridge-webview-native-android/event-output.png
