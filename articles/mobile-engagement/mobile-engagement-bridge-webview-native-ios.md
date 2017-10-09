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
# <a name="bridge-ios-webview-with-native-mobile-engagement-ios-sdk"></a><span data-ttu-id="0166b-103">IOS webweergave met systeemeigen Mobile Engagement iOS SDK brug</span><span class="sxs-lookup"><span data-stu-id="0166b-103">Bridge iOS WebView with native Mobile Engagement iOS SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0166b-104">Android-brug</span><span class="sxs-lookup"><span data-stu-id="0166b-104">Android Bridge</span></span>](mobile-engagement-bridge-webview-native-android.md)
> * [<span data-ttu-id="0166b-105">iOS-brug</span><span class="sxs-lookup"><span data-stu-id="0166b-105">iOS Bridge</span></span>](mobile-engagement-bridge-webview-native-ios.md)
> 
> 

<span data-ttu-id="0166b-106">Sommige mobiele apps zijn ontworpen als een app hybride Hallo app zelf is ontwikkeld met behulp van systeemeigen iOS Objective-C-ontwikkeling waarbij enkele of zelfs alle Hallo schermen worden weergegeven in de webweergave van een iOS.</span><span class="sxs-lookup"><span data-stu-id="0166b-106">Some mobile apps are designed as a hybrid app where hello app itself is developed using native iOS Objective-C development but some or even all of hello screens are rendered within an iOS WebView.</span></span> <span data-ttu-id="0166b-107">U kunt nog steeds Mobile Engagement iOS SDK binnen deze apps gebruiken en deze zelfstudie wordt beschreven hoe toogo over dit te doen.</span><span class="sxs-lookup"><span data-stu-id="0166b-107">You can still consume Mobile Engagement iOS SDK within such apps and this tutorial describes how toogo about doing this.</span></span> 

<span data-ttu-id="0166b-108">Er zijn twee benaderingen tooachieve dit Hoewel beide niet-gedocumenteerde zijn:</span><span class="sxs-lookup"><span data-stu-id="0166b-108">There are two approaches tooachieve this though both are undocumented:</span></span>

* <span data-ttu-id="0166b-109">Eerst een zoals is beschreven in dit [koppeling](http://stackoverflow.com/questions/9826792/how-to-invoke-objective-c-method-from-javascript-and-send-back-data-to-javascrip) die omvat het registreren van een `UIWebViewDelegate` op uw webserver weergeven en catch-en-onmiddellijk-annuleren een wijziging in de locatie in Javascript uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0166b-109">First one is described on this [link](http://stackoverflow.com/questions/9826792/how-to-invoke-objective-c-method-from-javascript-and-send-back-data-to-javascrip) which involves registering a `UIWebViewDelegate` on your web view and catch-and-immediatly-cancel a location change done in Javascript.</span></span> 
* <span data-ttu-id="0166b-110">Tweede een is gebaseerd op dit [WWDC 2013 sessie](https://developer.apple.com/videos/play/wwdc2013/615), een methode die is eerst schonere dan Hallo en die we voor deze handleiding wordt gevolgd.</span><span class="sxs-lookup"><span data-stu-id="0166b-110">Second one is based on this [WWDC 2013 session](https://developer.apple.com/videos/play/wwdc2013/615), an approach which is cleaner than hello first and which we will follow for this guide.</span></span> <span data-ttu-id="0166b-111">Houd er rekening mee dat deze methode alleen op iOS7 en hoger werkt.</span><span class="sxs-lookup"><span data-stu-id="0166b-111">Note that this approach only works on iOS7 and above.</span></span> 

<span data-ttu-id="0166b-112">Volgende stappen uit Hallo voor Hallo iOS voorbeeld overbruggen:</span><span class="sxs-lookup"><span data-stu-id="0166b-112">Follow hello steps below for hello iOS bridge sample:</span></span>

1. <span data-ttu-id="0166b-113">Ten eerste moet u tooensure die u hebt doorlopen onze [zelfstudie aan de slag](mobile-engagement-ios-get-started.md) toointegrate Hallo Mobile Engagement iOS SDK in uw hybride-app.</span><span class="sxs-lookup"><span data-stu-id="0166b-113">First of all, you need tooensure that you have gone through our [Getting Started tutorial](mobile-engagement-ios-get-started.md) toointegrate hello Mobile Engagement iOS SDK in your hybrid app.</span></span> <span data-ttu-id="0166b-114">U kunt eventueel ook inschakelen test als volgt een logboek zodat Hallo SDK methoden zien als we ze Hallo webweergave activeren.</span><span class="sxs-lookup"><span data-stu-id="0166b-114">Optionally, you can also enable test logging as follows so that you can see hello SDK methods as we trigger them from hello webview.</span></span> 
   
        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
           ....
             [EngagementAgent setTestLogEnabled:YES];
           ....
        }
2. <span data-ttu-id="0166b-115">Controleren of dat uw hybride-app een scherm met een webweergave is geïnstalleerd op.</span><span class="sxs-lookup"><span data-stu-id="0166b-115">Now make sure that your hybrid app has a screen with a webview on it.</span></span> <span data-ttu-id="0166b-116">U kunt deze wel toevoegen toohello `Main.storyboard` van Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="0166b-116">You can add it toohello `Main.storyboard` of hello app.</span></span> 
3. <span data-ttu-id="0166b-117">Koppel deze webweergave met uw **ViewController** te klikken en slepen Hallo webweergave van Hallo weergave Controller Scene toohello `ViewController.h` scherm voor het plaatsen hiervan onder Hallo bewerken `@interface` regel.</span><span class="sxs-lookup"><span data-stu-id="0166b-117">Associate this webview with your **ViewController** by clicking and dragging hello webview from hello View Controller Scene toohello `ViewController.h` edit screen, placing it just below hello `@interface` line.</span></span> 
4. <span data-ttu-id="0166b-118">Als u dit doet, wordt een dialoogvenster weergegeven waarin wordt gevraagd een naam.</span><span class="sxs-lookup"><span data-stu-id="0166b-118">Once you do this, a dialog box will pop up asking for a name.</span></span> <span data-ttu-id="0166b-119">Geef de naam Hallo als **Webweergave**.</span><span class="sxs-lookup"><span data-stu-id="0166b-119">Provide hello name as **webView**.</span></span> <span data-ttu-id="0166b-120">Uw `ViewController.h` bestand moet eruitzien als Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="0166b-120">Your `ViewController.h` file should look like hello following:</span></span>
   
        #import <UIKit/UIKit.h>
        #import "EngagementViewController.h"
   
        @interface ViewController : EngagementViewController
        @property (strong, nonatomic) IBOutlet UIWebView *webView;
   
        @end
5. <span data-ttu-id="0166b-121">Hallo wordt bijgewerkt `ViewController.m` bestand later maar eerst maken we Hallo bridge-bestand dat Hiermee maakt u een wrapper voor een aantal veelgebruikte Mobile Engagement iOS SDK-methoden.</span><span class="sxs-lookup"><span data-stu-id="0166b-121">We will update hello `ViewController.m` file later but first we will create hello bridge file which creates a wrapper over some commonly used Mobile Engagement iOS SDK methods.</span></span> <span data-ttu-id="0166b-122">Maak een nieuw headerbestand aangeroepen **EngagementJsExports.h** waarin Hallo `JSExport` mechanisme dat wordt beschreven in de hiervoor genoemde Hallo [sessie](https://developer.apple.com/videos/play/wwdc2013/615) tooexpose Hallo systeemeigen iOS-methoden.</span><span class="sxs-lookup"><span data-stu-id="0166b-122">Create a new header file called **EngagementJsExports.h** which uses hello `JSExport` mechanism described in hello aforementioned [session](https://developer.apple.com/videos/play/wwdc2013/615) tooexpose hello native iOS methods.</span></span> 
   
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
6. <span data-ttu-id="0166b-123">We gaan naast Hallo secondegedeelte van Hallo bridge bestand maken.</span><span class="sxs-lookup"><span data-stu-id="0166b-123">Next we will create hello second part of hello bridge file.</span></span> <span data-ttu-id="0166b-124">Maken van een bestand met de naam **EngagementJsExports.m** waarin Hallo implementatie Hallo werkelijke wrappers maken door het aanroepen van Hallo Mobile Engagement iOS SDK-methoden.</span><span class="sxs-lookup"><span data-stu-id="0166b-124">Create a file called **EngagementJsExports.m** which will contain hello implementation creating hello actual wrappers by calling hello Mobile Engagement iOS SDK methods.</span></span> <span data-ttu-id="0166b-125">Ook opmerking dat we van Hallo parseren `extras` wordt doorgegeven vanuit Hallo webweergave javascript en opslaan die in een `NSMutableDictionary` object toobe doorgegeven Hello Engagement SDK-methode aanroepen.</span><span class="sxs-lookup"><span data-stu-id="0166b-125">Also note that we are parsing hello `extras` being passed from hello webview javascript and putting that into an `NSMutableDictionary` object toobe passed with hello Engagement SDK method calls.</span></span>  
   
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
7. <span data-ttu-id="0166b-126">Nu we toohello terugkeren **ViewController.m** bij te werken met de volgende code Hallo:</span><span class="sxs-lookup"><span data-stu-id="0166b-126">Now we come back toohello **ViewController.m** and update it with hello following code:</span></span> 
   
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
8. <span data-ttu-id="0166b-127">Opmerking Hallo volgende verwijst over Hallo **ViewController.m** bestand:</span><span class="sxs-lookup"><span data-stu-id="0166b-127">Note hello following points about hello **ViewController.m** file:</span></span>
   
   * <span data-ttu-id="0166b-128">In Hallo `loadWebView` methode, wij zijn bij het laden van een lokale HTML-bestand met de naam **LocalPage.html** waarvan de code er naast controleert.</span><span class="sxs-lookup"><span data-stu-id="0166b-128">In hello `loadWebView` method, we are loading a local HTML file called **LocalPage.html** whose code we will review next.</span></span> 
   * <span data-ttu-id="0166b-129">In Hallo `webViewDidFinishLoad` methode, zijn we Hallo grabbing `JsContext` en onze wrapperklasse koppelt.</span><span class="sxs-lookup"><span data-stu-id="0166b-129">In hello `webViewDidFinishLoad` method, we are grabbing hello `JsContext` and associating our wrapper class with it.</span></span> <span data-ttu-id="0166b-130">Hierdoor kunnen aanroepen van onze wrapper SDK methoden met de Hallo ingang **EngagementJs** Hallo webweergave.</span><span class="sxs-lookup"><span data-stu-id="0166b-130">This will allow calling our wrapper SDK methods using hello handle **EngagementJs** from hello webView.</span></span> 
9. <span data-ttu-id="0166b-131">Maken van een bestand met de naam **LocalPage.html** Hello code te volgen:</span><span class="sxs-lookup"><span data-stu-id="0166b-131">Create a file called **LocalPage.html** with hello following code:</span></span>
   
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
10. <span data-ttu-id="0166b-132">Opmerking Hallo volgende verwijst over bovenstaande Hallo HTML-bestand:</span><span class="sxs-lookup"><span data-stu-id="0166b-132">Note hello following points about hello HTML file above:</span></span>
    
    * <span data-ttu-id="0166b-133">Het bevat een set van invoervakken waarin u gegevens toobe gebruikt als namen voor de gebeurtenis, taak, fout, AppInfo kunt opgeven.</span><span class="sxs-lookup"><span data-stu-id="0166b-133">It contains a set of input boxes where you can provide data toobe used as names for your Event, Job, Error, AppInfo.</span></span> <span data-ttu-id="0166b-134">Wanneer u op volgende tooit van Hallo knop klikt, wordt een aanroep toohello Javascript die uiteindelijk Hallo methoden vanuit Hallo bridge bestand toopass deze toohello aanroep van Mobile Engagement iOS SDK aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="0166b-134">When you click on hello button next tooit, a call is made toohello Javascript which eventually calls hello methods from hello bridge file toopass this call toohello Mobile Engagement iOS SDK.</span></span> 
    * <span data-ttu-id="0166b-135">We zijn op bepaalde statische extra info toohello gebeurtenissen, taken en zelfs fouten toodemonstrate tagging hoe dit kan worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0166b-135">We are tagging on some static extra info toohello events, jobs and even errors toodemonstrate how this could be done.</span></span> <span data-ttu-id="0166b-136">Deze extra gegevens als een JSON-tekenreeks die wordt verzonden als u in Hallo zoeken `EngagementJsExports.m` bestand wordt geparseerd en doorgegeven samen met het verzenden van gebeurtenissen, taken, fouten.</span><span class="sxs-lookup"><span data-stu-id="0166b-136">This extra info is sent as a JSON string which, if you look in hello `EngagementJsExports.m` file, is parsed and passed along with sending Events, Jobs, Errors.</span></span> 
    * <span data-ttu-id="0166b-137">Een Mobile Engagement-taak wordt gestart met de naam van de Hallo u opgeeft in het invoervak hello, uitgevoerd voor 10 seconden en afsluiten.</span><span class="sxs-lookup"><span data-stu-id="0166b-137">A Mobile Engagement Job is kicked off with hello name you specify in hello input box, run for 10 seconds and shut down.</span></span> 
    * <span data-ttu-id="0166b-138">Een Mobile Engagement appinfo of tag wordt doorgegeven met 'customer_name' als statische Hallo-sleutel en Hallo-waarde die u hebt ingevoerd in de invoer Hallo Hallo-waarde voor Hallo-tag.</span><span class="sxs-lookup"><span data-stu-id="0166b-138">A Mobile Engagement appinfo or tag is passed with 'customer_name' as hello static key and hello value that you entered in hello input as hello value for hello tag.</span></span> 
11. <span data-ttu-id="0166b-139">Voer Hallo-app en u ziet Hallo volgende.</span><span class="sxs-lookup"><span data-stu-id="0166b-139">Run hello app and you will see hello following.</span></span> <span data-ttu-id="0166b-140">Nu bieden een naam voor een testgebeurtenis zoals Hallo volgende en klik op **verzenden** volgende tooit.</span><span class="sxs-lookup"><span data-stu-id="0166b-140">Now provide some name for a test event like hello following and click **Send** next tooit.</span></span> 
    
     ![][1]
12. <span data-ttu-id="0166b-141">Nu wanneer u toohello gaat **Monitor** tabblad van uw app en kijk onder **Events -> Details**, ziet u deze gebeurtenis weergegeven samen met de Hallo statische toepassingsgegevens die we sturen.</span><span class="sxs-lookup"><span data-stu-id="0166b-141">Now if you go toohello **Monitor** tab of your app and look under **Events -> Details**, you will see this event show up along with hello static app-info that we are sending.</span></span> 
    
    ![][2]

<!-- Images. -->
[1]: ./media/mobile-engagement-bridge-webview-native-ios/sending-event.png
[2]: ./media/mobile-engagement-bridge-webview-native-ios/event-output.png
