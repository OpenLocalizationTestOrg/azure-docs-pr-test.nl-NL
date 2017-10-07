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
# <a name="bridge-android-webview-with-native-mobile-engagement-android-sdk"></a>Android webweergave Bridge met systeemeigen Mobile Engagement Android SDK
> [!div class="op_single_selector"]
> * [Android-brug](mobile-engagement-bridge-webview-native-android.md)
> * [iOS-brug](mobile-engagement-bridge-webview-native-ios.md)
> 
> 

Sommige mobiele apps zijn ontworpen als een app hybride waarbij Hallo app zelf is ontwikkeld met behulp van systeemeigen Android-ontwikkeling, maar enkele of zelfs alle Hallo schermen binnen een webweergave Android worden weergegeven. U kunt nog steeds Mobile Engagement Android SDK verbruiken binnen deze apps en deze zelfstudie wordt beschreven hoe toogo over dit te doen. Hallo voorbeeldcode hieronder is gebaseerd op Hallo Android documentatie [hier](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript). Hierin wordt beschreven hoe deze gedocumenteerde benadering kan worden gebruikt tooimplement Hallo dezelfde voor Mobile Engagement Android SDK van veelgebruikte methoden zodat een webweergave in een hybride-app kan ook worden geïnitieerd aanvragen tootrack gebeurtenissen, taken, fouten, app-info terwijl ze via sluizen onze Android SDK. 

1. Ten eerste moet u tooensure die u hebt doorlopen onze [zelfstudie aan de slag](mobile-engagement-android-get-started.md) toointegrate Hallo Mobile Engagement Android SDK in uw hybride-app. Als u dit doen, uw `OnCreate` methode Hallo volgende eruit.  
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("<Mobile Engagement Conn String>");
            EngagementAgent.getInstance(this).init(engagementConfiguration);
        }
2. Controleren of dat uw hybride-app een scherm met een webweergave is geïnstalleerd op. Hallo code zijn vergelijkbaar toohello volgende waar we een lokaal HTML-bestand worden geladen **Sample.html** in Hallo webweergave in Hallo `onCreate` methode van het scherm. 
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
        }
   
        protected void onCreate(Bundle savedInstanceState) {
            ...
            ...
            SetWebView();
        }
3. Maakt nu een bestand met de naam bridge **WebAppInterface** Hallo met Mobile Engagement Android SDK-methoden die Hiermee maakt u een wrapper voor sommige vaak gebruikt `@JavascriptInterface` benadering wordt beschreven in Hallo [Android-documentatie ](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript):
   
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
4. Wanneer we Hallo hierboven bridge-bestand hebt gemaakt, moeten we tooensure dat deze gekoppeld aan onze webweergave is. Voor deze toohappen, moet u tooedit uw `SetWebview` methode zodat het Hallo volgende lijkt:
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
            WebSettings webSettings = myWebView.getSettings();
            webSettings.setJavaScriptEnabled(true);
            myWebView.addJavascriptInterface(new WebAppInterface(this), "EngagementJs");
        }
5. In Hallo bovenstaande codefragment we genoemd `addJavascriptInterface` tooassociate onze bridge klasse met onze webweergave en ook gemaakt een ingang aangeroepen **EngagementJs** toocall Hallo methoden van Hallo bridge-bestand. 
6. Maak nu Hallo na bestand met de naam **Sample.html** in uw project in een map genaamd **activa** die in het Hallo webweergave wordt geladen en waar we bellen Hallo methoden van Hallo bridge-bestand.
   
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
7. Opmerking Hallo volgende verwijst over bovenstaande Hallo HTML-bestand:
   
   * Het bevat een set van invoervakken waarin u gegevens toobe gebruikt als namen voor de gebeurtenis, taak, fout, AppInfo kunt opgeven. Wanneer u op volgende tooit van Hallo knop klikt, wordt een aanroep toohello Javascript die uiteindelijk Hallo methoden vanuit Hallo bridge bestand toopass deze toohello aanroep van Mobile Engagement Android SDK aangeroepen. 
   * We zijn op bepaalde statische extra info toohello gebeurtenissen, taken en zelfs fouten toodemonstrate tagging hoe dit kan worden uitgevoerd. Deze extra gegevens als een JSON-tekenreeks die wordt verzonden als u in Hallo zoeken `WebAppInterface` bestand wordt geparseerd en plaatsen in een Android `Bundle` en samen met het verzenden van gebeurtenissen, taken, fouten wordt doorgegeven. 
   * Een Mobile Engagement-taak wordt gestart met de naam van de Hallo u opgeeft in het invoervak hello, uitgevoerd voor 10 seconden en afsluiten. 
   * Een Mobile Engagement appinfo of tag wordt doorgegeven met 'customer_name' als statische Hallo-sleutel en Hallo-waarde die u hebt ingevoerd in de invoer Hallo Hallo-waarde voor Hallo-tag. 
8. Voer Hallo-app en u ziet Hallo volgende. Nu bieden een naam voor een testgebeurtenis zoals Hallo volgende en klik op **verzenden** eronder. 
   
    ![][1]
9. Nu wanneer u toohello gaat **Monitor** tabblad van uw app en kijk onder **Events -> Details**, ziet u deze gebeurtenis weergegeven samen met de Hallo statische toepassingsgegevens die we sturen. 
   
   ![][2]

<!-- Images. -->
[1]: ./media/mobile-engagement-bridge-webview-native-android/sending-event.png
[2]: ./media/mobile-engagement-bridge-webview-native-android/event-output.png
