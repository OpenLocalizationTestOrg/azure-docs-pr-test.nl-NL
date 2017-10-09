---
title: aaaBridge iOS webweergave met systeemeigen Mobile Engagement iOS SDK
description: Beschrijft hoe een brug tussen webweergave met Javascript en Hallo systeemeigen Mobile Engagement iOS SDK toocreate
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: e1d6ff6f-cd67-4131-96eb-c3d6318de752
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 089ed8484722cb5ba624e5dce0e670ab56de514d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="bridge-ios-webview-with-native-mobile-engagement-ios-sdk"></a>IOS webweergave met systeemeigen Mobile Engagement iOS SDK brug
> [!div class="op_single_selector"]
> * [Android-brug](mobile-engagement-bridge-webview-native-android.md)
> * [iOS-brug](mobile-engagement-bridge-webview-native-ios.md)
> 
> 

Sommige mobiele apps zijn ontworpen als een app hybride Hallo app zelf is ontwikkeld met behulp van systeemeigen iOS Objective-C-ontwikkeling waarbij enkele of zelfs alle Hallo schermen worden weergegeven in de webweergave van een iOS. U kunt nog steeds Mobile Engagement iOS SDK binnen deze apps gebruiken en deze zelfstudie wordt beschreven hoe toogo over dit te doen. 

Er zijn twee benaderingen tooachieve dit Hoewel beide niet-gedocumenteerde zijn:

* Eerst een zoals is beschreven in dit [koppeling](http://stackoverflow.com/questions/9826792/how-to-invoke-objective-c-method-from-javascript-and-send-back-data-to-javascrip) die omvat het registreren van een `UIWebViewDelegate` op uw webserver weergeven en catch-en-onmiddellijk-annuleren een wijziging in de locatie in Javascript uitgevoerd. 
* Tweede een is gebaseerd op dit [WWDC 2013 sessie](https://developer.apple.com/videos/play/wwdc2013/615), een methode die is eerst schonere dan Hallo en die we voor deze handleiding wordt gevolgd. Houd er rekening mee dat deze methode alleen op iOS7 en hoger werkt. 

Volgende stappen uit Hallo voor Hallo iOS voorbeeld overbruggen:

1. Ten eerste moet u tooensure die u hebt doorlopen onze [zelfstudie aan de slag](mobile-engagement-ios-get-started.md) toointegrate Hallo Mobile Engagement iOS SDK in uw hybride-app. U kunt eventueel ook inschakelen test als volgt een logboek zodat Hallo SDK methoden zien als we ze Hallo webweergave activeren. 
   
        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
           ....
             [EngagementAgent setTestLogEnabled:YES];
           ....
        }
2. Controleren of dat uw hybride-app een scherm met een webweergave is geïnstalleerd op. U kunt deze wel toevoegen toohello `Main.storyboard` van Hallo-app. 
3. Koppel deze webweergave met uw **ViewController** te klikken en slepen Hallo webweergave van Hallo weergave Controller Scene toohello `ViewController.h` scherm voor het plaatsen hiervan onder Hallo bewerken `@interface` regel. 
4. Als u dit doet, wordt een dialoogvenster weergegeven waarin wordt gevraagd een naam. Geef de naam Hallo als **Webweergave**. Uw `ViewController.h` bestand moet eruitzien als Hallo volgende:
   
        #import <UIKit/UIKit.h>
        #import "EngagementViewController.h"
   
        @interface ViewController : EngagementViewController
        @property (strong, nonatomic) IBOutlet UIWebView *webView;
   
        @end
5. Hallo wordt bijgewerkt `ViewController.m` bestand later maar eerst maken we Hallo bridge-bestand dat Hiermee maakt u een wrapper voor een aantal veelgebruikte Mobile Engagement iOS SDK-methoden. Maak een nieuw headerbestand aangeroepen **EngagementJsExports.h** waarin Hallo `JSExport` mechanisme dat wordt beschreven in de hiervoor genoemde Hallo [sessie](https://developer.apple.com/videos/play/wwdc2013/615) tooexpose Hallo systeemeigen iOS-methoden. 
   
        #import <Foundation/Foundation.h>
        #import <JavaScriptCore/JavascriptCore.h>
   
        @protocol EngagementJsExports <JSExport>
   
        + (void) sendEngagementEvent:(NSString*) name :(NSString*)extras;
        + (void) startEngagementJob:(NSString*) name :(NSString*)extras;
        + (void) endEngagementJob:(NSString*) name;
        + (void) sendEngagementError:(NSString*) name :(NSString*)extras;
        + (void) sendEngagementAppInfo:(NSString*) appInfo;
   
        @end
   
        @interface EngagementJs : NSObject <EngagementJsExports>
   
        @end
6. We gaan naast Hallo secondegedeelte van Hallo bridge bestand maken. Maken van een bestand met de naam **EngagementJsExports.m** waarin Hallo implementatie Hallo werkelijke wrappers maken door het aanroepen van Hallo Mobile Engagement iOS SDK-methoden. Ook opmerking dat we van Hallo parseren `extras` wordt doorgegeven vanuit Hallo webweergave javascript en opslaan die in een `NSMutableDictionary` object toobe doorgegeven Hello Engagement SDK-methode aanroepen.  
   
        #import <UIKit/UIKit.h>
        #import "EngagementAgent.h"
        #import "EngagementJsExports.h"
   
        @implementation EngagementJs
   
        +(void) sendEngagementEvent:(NSString*)name :(NSString*)extras {
           NSMutableDictionary* extrasInput = [self ParseExtras:extras];
           [[EngagementAgent shared] sendEvent:name extras:extrasInput];
        }
   
        + (void) startEngagementJob:(NSString*) name :(NSString*)extras {
           NSMutableDictionary* extrasInput = [self ParseExtras:extras];
           [[EngagementAgent shared] startJob:name extras:extrasInput];
        }
   
        + (void) endEngagementJob:(NSString*) name {
           [[EngagementAgent shared] endJob:name];
        }
   
        + (void) sendEngagementError:(NSString*) name :(NSString*)extras {
           NSMutableDictionary* extrasInput = [self ParseExtras:extras];
           [[EngagementAgent shared] sendError:name extras:extrasInput];
        }
   
        + (void) sendEngagementAppInfo:(NSString*) appInfo {
           NSMutableDictionary* appInfoInput = [self ParseExtras:appInfo];
           [[EngagementAgent shared] sendAppInfo:appInfoInput];
        }
   
        + (NSMutableDictionary*) ParseExtras:(NSString*) input {
           NSData *data = [input dataUsingEncoding:NSUTF8StringEncoding];
           NSError* error = nil;
           NSMutableDictionary* extras = [NSJSONSerialization JSONObjectWithData:data options:0 error:&error];
   
           return extras;
        }
   
        @end
7. Nu we toohello terugkeren **ViewController.m** bij te werken met de volgende code Hallo: 
   
        #import <JavaScriptCore/JavaScriptCore.h>
        #import "ViewController.h"
        #import "EngagementJsExports.h"
   
        @interface ViewController ()
   
        @end
   
        @implementation ViewController
   
        - (void)viewDidLoad
        {
           self.webView.delegate = self;
           [super viewDidLoad];
           [self loadWebView];
        }
   
        - (void)loadWebView {
           NSBundle* mainBundle = [NSBundle mainBundle];
           NSURL* htmlPage = [mainBundle URLForResource:@"LocalPage" withExtension:@"html"];
   
           NSURLRequest* urlReq = [NSURLRequest requestWithURL:htmlPage];
           [self.webView loadRequest:urlReq];
        }
   
        - (void)webViewDidFinishLoad:(UIWebView*)wv
        {
           JSContext* context = [wv valueForKeyPath:@"documentView.webView.mainFrame.javaScriptContext"];
   
           context[@"EngagementJs"] = [EngagementJs class];
        }
   
        - (void)webView:(UIWebView*)wv didFailLoadWithError:(NSError*)error
        {
           NSLog(@"Error for WEBVIEW: %@", [error description]);
        }
   
        - (void)didReceiveMemoryWarning {
           [super didReceiveMemoryWarning];
           // Dispose of any resources that can be recreated.
        }
   
        @end
8. Opmerking Hallo volgende verwijst over Hallo **ViewController.m** bestand:
   
   * In Hallo `loadWebView` methode, wij zijn bij het laden van een lokale HTML-bestand met de naam **LocalPage.html** waarvan de code er naast controleert. 
   * In Hallo `webViewDidFinishLoad` methode, zijn we Hallo grabbing `JsContext` en onze wrapperklasse koppelt. Hierdoor kunnen aanroepen van onze wrapper SDK methoden met de Hallo ingang **EngagementJs** Hallo webweergave. 
9. Maken van een bestand met de naam **LocalPage.html** Hello code te volgen:
   
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
                   alert('window.onerror: ' + err);
               }
   
               function send(inputId)
               {
                   var input = document.getElementById(inputId);
                   if(input)
                   {
                       var value = input.value;
                       // Example of how extras info can be passed with hello Engagement logs
                       var extras = '{"CustomerId":"MS290011"}';
                   }
   
                   if(value && value.length > 0)
                   {
                       switch(inputId)
                       {
                           case "event":
                           EngagementJs.sendEngagementEvent(value, extras);
                           break;
   
                           case "job":
                           EngagementJs.startEngagementJob(value, extras);
                           window.setTimeout(
                           function(){
                               EngagementJs.endEngagementJob(value);
                           }, 10000 );
                           break;
   
                           case "error":
                           EngagementJs.sendEngagementError(value, extras);
                           break;
   
                           case "appInfo":
                           var appInfo = '{"customer_name":"' + value + '"}';
                           EngagementJs.sendEngagementAppInfo(appInfo);
                           break;
                       }
                   }
               }
               </script>
   
           </head>
           <body>
               <h1>Bridge Tester</h1>
   
               <div id='engagement'>
   
                   <br/>
                   <h2>Event</h2>
                   <input type="text" id="event" size="35">
                   <button onclick="send('event')">Send</button>
   
                   <br/>
                   <h2>Job</h2>
                   <input type="text" id="job" size="35">
                   <button onclick="send('job')">Send</button>
   
                   <br/>
                   <h2>Error</h2>
                   <input type="text" id="error" size="35">
                   <button onclick="send('error')">Send</button
   
                   <br/>
                   <h2>AppInfo</h2>
                   <input type="text" id="appInfo" size="35">
                   <button onclick="send('appInfo')">Send</button>
   
               </div>
           </body>
        </html>
10. Opmerking Hallo volgende verwijst over bovenstaande Hallo HTML-bestand:
    
    * Het bevat een set van invoervakken waarin u gegevens toobe gebruikt als namen voor de gebeurtenis, taak, fout, AppInfo kunt opgeven. Wanneer u op volgende tooit van Hallo knop klikt, wordt een aanroep toohello Javascript die uiteindelijk Hallo methoden vanuit Hallo bridge bestand toopass deze toohello aanroep van Mobile Engagement iOS SDK aangeroepen. 
    * We zijn op bepaalde statische extra info toohello gebeurtenissen, taken en zelfs fouten toodemonstrate tagging hoe dit kan worden uitgevoerd. Deze extra gegevens als een JSON-tekenreeks die wordt verzonden als u in Hallo zoeken `EngagementJsExports.m` bestand wordt geparseerd en doorgegeven samen met het verzenden van gebeurtenissen, taken, fouten. 
    * Een Mobile Engagement-taak wordt gestart met de naam van de Hallo u opgeeft in het invoervak hello, uitgevoerd voor 10 seconden en afsluiten. 
    * Een Mobile Engagement appinfo of tag wordt doorgegeven met 'customer_name' als statische Hallo-sleutel en Hallo-waarde die u hebt ingevoerd in de invoer Hallo Hallo-waarde voor Hallo-tag. 
11. Voer Hallo-app en u ziet Hallo volgende. Nu bieden een naam voor een testgebeurtenis zoals Hallo volgende en klik op **verzenden** volgende tooit. 
    
     ![][1]
12. Nu wanneer u toohello gaat **Monitor** tabblad van uw app en kijk onder **Events -> Details**, ziet u deze gebeurtenis weergegeven samen met de Hallo statische toepassingsgegevens die we sturen. 
    
    ![][2]

<!-- Images. -->
[1]: ./media/mobile-engagement-bridge-webview-native-ios/sending-event.png
[2]: ./media/mobile-engagement-bridge-webview-native-ios/event-output.png
