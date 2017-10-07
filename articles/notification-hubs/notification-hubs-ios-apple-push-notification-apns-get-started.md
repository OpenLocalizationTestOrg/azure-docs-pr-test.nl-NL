---
title: aaaSending push notifications tooiOS met Azure Notification Hubs | Microsoft Docs
description: In deze zelfstudie leert u hoe toouse Azure Notification Hubs toosend push-meldingen tooan iOS-toepassing.
services: notification-hubs
documentationcenter: ios
keywords: pushmelding,pushmeldingen,ios-pushmeldingen
author: ysxu
manager: erikre
editor: 
ms.assetid: b7fcd916-8db8-41a6-ae88-fc02d57cb914
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: d8bb47fee4c229b3ed2a7a4dbff25a56a7a7d009
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-tooios-with-azure-notification-hubs"></a>Push notifications tooiOS met Azure Notification Hubs verzenden
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Overzicht
> [!NOTE]
> toocomplete deze zelfstudie maakt u een actief Azure-account moet hebben. Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken. Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-ios-get-started) voor meer informatie.
> 
> 

Deze zelfstudie leert u hoe toouse Azure Notification Hubs toosend push-meldingen tooan iOS-toepassing. Maakt u een lege iOS-app die pushmeldingen ontvangt via Hallo [Apple Push Notification service (APNs)](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html). 

Wanneer u klaar bent, moet u kunnen toouse push uw notification hub toobroadcast meldingen tooall Hallo apparaten waarop uw app wordt uitgevoerd.

## <a name="before-you-begin"></a>Voordat u begint
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

Hallo voltooid code voor deze zelfstudie vindt [op GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/iOS/GetStartedNH/GetStarted). 

## <a name="prerequisites"></a>Vereisten
Deze zelfstudie vereist de volgende Hallo:

* [iOS SDK Mobile Services versie 1.2.4]
* Meest recente versie van [Xcode]
* Een apparaat dat compatibel is met iOS 8 (of een hogere versie)
* [Apple Developer Program](https://developer.apple.com/programs/)-lidmaatschap
  
  > [!NOTE]
  > Vanwege configuratievereisten voor pushmeldingen, moet u implementeren en testen van pushmeldingen op een fysiek iOS-apparaat (iPhone of iPad) in plaats van Hallo iOS-Simulator.
  > 
  > 

Het voltooien van deze zelfstudie is een vereiste voor alle andere Notification Hubs-zelfstudies voor iOS-apps.

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub-for-ios-push-notifications"></a>De Notification Hub voor iOS-pushmeldingen configureren
Deze sectie leidt u door een nieuwe notification hub maken en configureren van verificatie met APNS met Hallo **.p12** pushcertificaat dat u hebt gemaakt. Als u toouse een notification hub die u al hebt gemaakt wilt, kunt u toostep 5 overslaan.

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">

<li>

<p>Klik op Hallo <b>Notification Services</b> knop in Hallo <b>instellingen</b> blade Selecteer <b>Apple (APNS)</b>. Klik op <b>certificaat uploaden</b> en selecteer Hallo <b>.p12</b> -bestand dat u eerder hebt geëxporteerd. Zorg ervoor dat u ook het juiste wachtwoord Hallo opgeven.</p>

<p>Zorg ervoor dat tooselect <b>Sandbox</b> modus, aangezien dit voor ontwikkeling. Gebruik alleen Hallo <b>productie</b> als u wilt dat toosend push notifications toousers die uw app uit de store Hallo aangeschaft.</p>
</li>
</ol>
&emsp;&emsp;&emsp;&emsp;![APNS configureren in Azure-Portal](./media/notification-hubs-ios-get-started/notification-hubs-apple-config.png)

&emsp;&emsp;&emsp;&emsp;![APNs-certificering in Azure Portal configureren](./media/notification-hubs-ios-get-started/notification-hubs-apple-config-cert.png)

Uw notification hub is nu geconfigureerd toowork met APNS en u hebt Hallo verbinding tekenreeksen tooregister uw app en om pushmeldingen te verzenden.

## <a name="connect-your-ios-app-toonotification-hubs"></a>Verbinding maken met uw iOS-app tooNotification Hubs
1. Maak een nieuw iOS-project in Xcode en selecteer Hallo **enkele toepassingsweergave** sjabloon.
   
    ![Xcode - Toepassing voor één weergave][8]
    
2. Wanneer u opties voor het nieuwe project hello, zorg ervoor dat toouse Hallo dezelfde **Productnaam** en **organisatie-id** dat u gebruikt wanneer u eerder Hallo bundel-ID ingesteld op Hallo Apple Developer Portal.
   
    ![Xcode - Projectopties][11]
    
3. Onder **doelen**, klik op de projectnaam van uw, Hallo **Build Settings** tabblad en vouw **Code Signing Identity**, en klik vervolgens onder **Debug**, instellen van uw identiteit voor ondertekening van programmacode. Wisselknop **niveaus** van **Basic** te**alle**, en stel **profiel inrichting** toohello inrichtingsprofiel die u eerder hebt gemaakt .
   
    Als u Hallo nieuwe inrichtingsprofiel die u hebt gemaakt in Xcode niet ziet, vernieuw u Hallo profielen voor uw identiteit voor ondertekening. Klik op **Xcode** op de menubalk hello, klikt u op **voorkeuren**, klikt u op Hallo **Account** en klik op Hallo **Details weergeven** knop, klikt u op uw ondertekening van de identiteit en klik vervolgens op Hallo de knop Vernieuwen in de rechterbenedenhoek Hallo.
   
    ![Xcode - Profiel voor inrichting][9]
4. Hallo downloaden [iOS SDK Mobile Services versie 1.2.4] en pak Hallo-bestand. Met de rechtermuisknop op uw project in Xcode en klik op Hallo **bestanden toevoegen aan** optie tooadd hello **WindowsAzureMessaging.framework** map tooyour Xcode-project. Selecteer **Copy items if needed** (Items kopiëren indien nodig) en klik vervolgens op **Add**.
   
   > [!NOTE]
   > Hallo notification hubs SDK geen momenteel ondersteuning voor bitcode op Xcode 7.  U moet instellen **Bitcode inschakelen** te**Nee** in Hallo **opties bouwen** voor uw project.
   > 
   > 
   
    ![Azure SDK uitpakken][10]
5. Voeg een nieuw tooyour project voor header-bestand met de naam `HubInfo.h`. Dit bestand bevatten Hallo constanten voor uw notification hub.  Toevoegen van de volgende definities Hallo en vervang Hallo string literal tijdelijke aanduidingen door uw *hubnaam* en Hallo *DefaultListenSharedAccessSignature* die u eerder hebt genoteerd.
   
        #ifndef HubInfo_h
        #define HubInfo_h
   
            #define HUBNAME @"<Enter hello name of your hub>"
            #define HUBLISTENACCESS @"<Enter your DefaultListenSharedAccess connection string"
   
        #endif /* HubInfo_h */
6. Open uw `AppDelegate.h` bestand toevoegen Hallo importeren richtlijnen te volgen:
   
         #import <WindowsAzureMessaging/WindowsAzureMessaging.h> 
         #import "HubInfo.h"
7. In uw `AppDelegate.m file`, toevoegen van de volgende code in Hallo Hallo `didFinishLaunchingWithOptions` methode op basis van uw iOS-versie. Deze code registreert uw apparaatingang met APNs:
   
    Voor iOS 8:
   
         UIUserNotificationSettings *settings = [UIUserNotificationSettings settingsForTypes:UIUserNotificationTypeSound |
                                                UIUserNotificationTypeAlert | UIUserNotificationTypeBadge categories:nil];
   
        [[UIApplication sharedApplication] registerUserNotificationSettings:settings];
        [[UIApplication sharedApplication] registerForRemoteNotifications];
   
    Voor eerdere too8 voor de iOS-versies:
   
         [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound];
8. In hetzelfde bestand Hallo, Hallo volgende methoden toevoegen. Deze code maakt verbinding toohello notification hub is met Hallo-verbindingsgegevens die u hebt opgegeven in HubInfo.h. Deze geeft vervolgens Hallo apparaat token toohello notification hub zodat hello notification hub meldingen kan verzenden:
   
        - (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *) deviceToken {
            SBNotificationHub* hub = [[SBNotificationHub alloc] initWithConnectionString:HUBLISTENACCESS
                                        notificationHubPath:HUBNAME];
   
            [hub registerNativeWithDeviceToken:deviceToken tags:nil completion:^(NSError* error) {
                if (error != nil) {
                    NSLog(@"Error registering for notifications: %@", error);
                }
                else {
                    [self MessageBox:@"Registration Status" message:@"Registered"];
                }
            }];
        }
   
        -(void)MessageBox:(NSString *)title message:(NSString *)messageText
        {
            UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
                cancelButtonTitle:@"OK" otherButtonTitles: nil];
            [alert show];
        }
9. In hetzelfde bestand hello, het toevoegen van Hallo methode toodisplay na een **UIAlert** als Hallo melding is ontvangen terwijl Hallo app actief is:

        - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
            NSLog(@"%@", userInfo);
            [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
        }

1. Ontwikkel en Voer Hallo-app op uw apparaat tooverify dat er geen fouten zijn.

## <a name="send-test-push-notifications"></a>Testpushmeldingen verzenden
U kunt testen door meldingen in uw app ontvangt door pushmeldingen te verzenden in Hallo [Azure Portal] via Hallo **probleemoplossing** sectie in de hubblade hello (hello gebruiken *Testverzenden* optie).

![Azure -portal - Test verzenden][30]

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-from-hello-app"></a>(Optioneel) Pushmeldingen verzenden vanuit Hallo-app
> [!IMPORTANT]
> In dit voorbeeld van het verzenden van meldingen vanuit Hallo client-app is beschikbaar voor uitsluitend leren. Aangezien hiervoor Hallo `DefaultFullSharedAccessSignature` toobe aanwezig is op de client-app Hallo, beschrijft deze uw notification hub toohello risico dat een gebruiker kan toegang toosend unauthorized Toegangsmeldingen tooyour clients.
> 
> 

Als u toosend pushmeldingen vanuit een app wilt, deze sectie bevat een voorbeeld van hoe toodo deze met Hallo REST-interface.

1. Open in Xcode, `Main.storyboard` en Hallo volgende UI-onderdelen uit Hallo object bibliotheek tooallow Hallo gebruiker toosend pushmeldingen in Hallo app toe te voegen:
   
   * Een label zonder labeltekst. Gebruikte tooreport fouten tijdens het verzenden van meldingen zal zijn. Hallo **regels** eigenschap te moet worden ingesteld**0** zodat deze wordt het formaat automatisch beperkte toohello rechts en linkermarges en Hallo Hallo weergave bovenaan.
   * Een tekstveld met **tijdelijke aanduiding voor** tekst ingesteld te**meldingstekst invoeren**. Beperken Hallo veld onder Hallo label, zoals hieronder wordt weergegeven. Hallo weergavebesturing instellen als Hallo aansluiting gemachtigde.
   * Een knop met de titel **melding verzenden** beperkte direct onder het tekstveld hello en in horizontale richting Hallo.
     
     Hallo weergave ziet er als volgt:
     
     ![Xcode designer][32]
2. [Voeg aansluitingen](https://developer.apple.com/library/ios/recipes/xcode_help-IB_connections/chapters/CreatingOutlet.html) voor het label en het tekstveld veld Hallo uw weergave verbonden en werk uw `interface` definitie toosupport `UITextFieldDelegate` en `NSXMLParserDelegate`. Hallo drie eigenschapdeclaraties toohelp ondersteuning Hallo REST-API aanroepen en parseren van antwoord Hallo hieronder toevoegen.
   
    Uw ViewController.h-bestand moet er als volgt uitzien:
   
        #import <UIKit/UIKit.h>
   
        @interface ViewController : UIViewController <UITextFieldDelegate, NSXMLParserDelegate>
        {
            NSXMLParser *xmlParser;
        }
   
        // Make sure these outlets are connected tooyour UI by ctrl+dragging
        @property (weak, nonatomic) IBOutlet UITextField *notificationMessage;
        @property (weak, nonatomic) IBOutlet UILabel *sendResults;
   
        @property (copy, nonatomic) NSString *statusResult;
        @property (copy, nonatomic) NSString *currentElement;
   
        @end
3. Open `HubInfo.h` en voeg de volgende constanten die worden gebruikt voor het verzenden van meldingen tooyour hub Hallo. Hallo tijdelijke aanduiding voor letterlijke tekenreeks vervangen door uw werkelijke *DefaultFullSharedAccessSignature* verbindingsreeks.
   
        #define API_VERSION @"?api-version=2015-01"
        #define HUBFULLACCESS @"<Enter Your DefaultFullSharedAccess Connection string>"
4. Voeg de volgende Hallo `#import` instructies tooyour `ViewController.h` bestand.
   
        #import <CommonCrypto/CommonHMAC.h>
        #import "HubInfo.h"
5. In `ViewController.m` Hallo na de implementatie van de interface toohello code toevoegen. Deze code parseert uw *DefaultFullSharedAccessSignature*-verbindingsreeks. Zoals vermeld in Hallo [naslaginformatie over REST API](http://msdn.microsoft.com/library/azure/dn495627.aspx), worden deze geparseerde informatie gebruikt toogenerate een SaS-token voor Hallo **autorisatie** aanvraag-header.
   
        NSString *HubEndpoint;
        NSString *HubSasKeyName;
        NSString *HubSasKeyValue;
   
        -(void)ParseConnectionString
        {
            NSArray *parts = [HUBFULLACCESS componentsSeparatedByString:@";"];
            NSString *part;
   
            if ([parts count] != 3)
            {
                NSException* parseException = [NSException exceptionWithName:@"ConnectionStringParseException"
                    reason:@"Invalid full shared access connection string" userInfo:nil];
   
                @throw parseException;
            }
   
            for (part in parts)
            {
                if ([part hasPrefix:@"Endpoint"])
                {
                    HubEndpoint = [NSString stringWithFormat:@"https%@",[part substringFromIndex:11]];
                }
                else if ([part hasPrefix:@"SharedAccessKeyName"])
                {
                    HubSasKeyName = [part substringFromIndex:20];
                }
                else if ([part hasPrefix:@"SharedAccessKey"])
                {
                    HubSasKeyValue = [part substringFromIndex:16];
                }
            }
        }
6. In `ViewController.m`, update Hallo `viewDidLoad` methode tooparse Hallo verbindingsreeks wanneer Hallo weergave wordt geladen. Ook toevoegen Hallo hulpprogrammamethoden die hieronder worden weergegeven toohello interface-implementatie.  

        - (void)viewDidLoad
        {
            [super viewDidLoad];
            [self ParseConnectionString];
            [_notificationMessage setDelegate:self];
        }

        -(NSString *)CF_URLEncodedString:(NSString *)inputString
        {
           return (__bridge NSString *)CFURLCreateStringByAddingPercentEscapes(NULL, (CFStringRef)inputString,
                NULL, (CFStringRef)@"!*'();:@&=+$,/?%#[]", kCFStringEncodingUTF8);
        }

        -(void)MessageBox:(NSString *)title message:(NSString *)messageText
        {
            UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
                cancelButtonTitle:@"OK" otherButtonTitles: nil];
            [alert show];
        }





1. In `ViewController.m`, toevoegen van de volgende code toohello interface implementatie toogenerate Hallo SaS-Autorisatietoken die worden vermeld in Hallo Hallo **autorisatie** -kop, zoals vermeld in Hallo [REST-API Verwijzing](http://msdn.microsoft.com/library/azure/dn495627.aspx).
   
        -(NSString*) generateSasToken:(NSString*)uri
        {
            NSString *targetUri;
            NSString* utf8LowercasedUri = NULL;
            NSString *signature = NULL;
            NSString *token = NULL;
   
            @try
            {
                // Add expiration
                uri = [uri lowercaseString];
                utf8LowercasedUri = [self CF_URLEncodedString:uri];
                targetUri = [utf8LowercasedUri lowercaseString];
                NSTimeInterval expiresOnDate = [[NSDate date] timeIntervalSince1970];
                int expiresInMins = 60; // 1 hour
                expiresOnDate += expiresInMins * 60;
                UInt64 expires = trunc(expiresOnDate);
                NSString* toSign = [NSString stringWithFormat:@"%@\n%qu", targetUri, expires];
   
                // Get an hmac_sha1 Mac instance and initialize with hello signing key
                const char *cKey  = [HubSasKeyValue cStringUsingEncoding:NSUTF8StringEncoding];
                const char *cData = [toSign cStringUsingEncoding:NSUTF8StringEncoding];
                unsigned char cHMAC[CC_SHA256_DIGEST_LENGTH];
                CCHmac(kCCHmacAlgSHA256, cKey, strlen(cKey), cData, strlen(cData), cHMAC);
                NSData *rawHmac = [[NSData alloc] initWithBytes:cHMAC length:sizeof(cHMAC)];
                signature = [self CF_URLEncodedString:[rawHmac base64EncodedStringWithOptions:0]];
   
                // Construct authorization token string
                token = [NSString stringWithFormat:@"SharedAccessSignature sig=%@&se=%qu&skn=%@&sr=%@",
                    signature, expires, HubSasKeyName, targetUri];
            }
            @catch (NSException *exception)
            {
                [self MessageBox:@"Exception Generating SaS Token" message:[exception reason]];
            }
            @finally
            {
                if (utf8LowercasedUri != NULL)
                    CFRelease((CFStringRef)utf8LowercasedUri);
                if (signature != NULL)
                CFRelease((CFStringRef)signature);
            }
   
            return token;
        }
2. CTRL + Sleep vanuit Hallo **melding verzenden** te knop`ViewController.m` tooadd een actie met de naam **SendNotificationMessage** voor Hallo **Touch Down** gebeurtenis. De methode Update Hello na de code toosend Hallo kennisgeving Hallo REST-API gebruiken.
   
        - (IBAction)SendNotificationMessage:(id)sender
        {
            self.sendResults.text = @"";
            [self SendNotificationRESTAPI];
        }
   
        - (void)SendNotificationRESTAPI
        {
            NSURLSession* session = [NSURLSession
                             sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration]
                             delegate:nil delegateQueue:nil];
   
            // Apple Notification format of hello notification message
            NSString *json = [NSString stringWithFormat:@"{\"aps\":{\"alert\":\"%@\"}}",
                                self.notificationMessage.text];
   
            // Construct hello message's REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                                HUBNAME, API_VERSION]];
   
            // Generate hello token toobe used in hello authorization header
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];
   
            //Create hello request tooadd hello APNs notification message toohello hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];
            [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];
   
            // Signify Apple notification format
            [request setValue:@"apple" forHTTPHeaderField:@"ServiceBusNotification-Format"];
   
            //Authenticate hello notification message POST request with hello SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];
   
            //Add hello notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
   
            // Send hello REST request
            NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request
                completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
            {
                NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                if (error || (httpResponse.statusCode != 200 && httpResponse.statusCode != 201))
                {
                    NSLog(@"\nError status: %d\nError: %@", httpResponse.statusCode, error);
                }
                if (data != NULL)
                {
                    xmlParser = [[NSXMLParser alloc] initWithData:data];
                    [xmlParser setDelegate:self];
                       [xmlParser parse];
                }
            }];
            [dataTask resume];
        }
3. In `ViewController.m`, Hallo gemachtigde methode toosupport Hallo toetsenbord voor Hallo tekstveld sluiten na toevoegen. CTRL + Sleep vanuit Hallo tekst veld toohello pictogram voor weergavebesturing in Hallo interface designer tooset Hallo weergeven controller Hallo aansluiting gemachtigde.
   
        //===[ Implement UITextFieldDelegate methods ]===
   
        -(BOOL)textFieldShouldReturn:(UITextField *)textField
        {
            [textField resignFirstResponder];
            return YES;
        }
4. In `ViewController.m`, voeg Hallo volgende antwoord Hallo bij het parseren van methoden toosupport delegeren met behulp van `NSXMLParser`.
   
       //===[ Implement NSXMLParserDelegate methods ]===
   
       -(void)parserDidStartDocument:(NSXMLParser *)parser
       {
           self.statusResult = @"";
       }
   
       -(void)parser:(NSXMLParser *)parser didStartElement:(NSString *)elementName
           namespaceURI:(NSString *)namespaceURI qualifiedName:(NSString *)qName
           attributes:(NSDictionary *)attributeDict
       {
           NSString * element = [elementName lowercaseString];
           NSLog(@"*** New element parsed : %@ ***",element);
   
           if ([element isEqualToString:@"code"] | [element isEqualToString:@"detail"])
           {
               self.currentElement = element;
           }
       }
   
       -(void) parser:(NSXMLParser *)parser foundCharacters:(NSString *)parsedString
       {
           self.statusResult = [self.statusResult stringByAppendingString:
               [NSString stringWithFormat:@"%@ : %@\n", self.currentElement, parsedString]];
       }
   
       -(void)parserDidEndDocument:(NSXMLParser *)parser
       {
           // Set hello status label text on hello UI thread
           dispatch_async(dispatch_get_main_queue(),
           ^{
               [self.sendResults setText:self.statusResult];
           });
       }
5. Hallo-project te bouwen en controleer of er zijn geen fouten.

> [!NOTE]
> Als u een opbouwfout in Xcode7 ondersteuning voor bitcode optreden, moet u Hallo **Build Settings** > **inschakelen Bitcode (ENABLE_BITCODE)** te**Nee** in Xcode. Hallo Notification Hubs SDK biedt momenteel geen ondersteuning voor bitcode. 
> 
> 

U vindt alle Hallo mogelijke nettoladingen van meldingen in Hallo Apple [Local and Push Notification Programming Guide].

## <a name="checking-if-your-app-can-receive-push-notifications"></a>Controleren of een app pushmeldingen kan ontvangen
tootest pushmeldingen op iOS, moet u Hallo app tooa fysiek iOS-apparaat implementeren. U kunt geen Apple pushmeldingen verzenden met behulp van Hallo iOS-Simulator.

1. Hallo-app uitvoeren en controleer of de registratie is gelukt en druk op **OK**.
   
    ![De registratie van pushmeldingen in iOS-apps testen][33]
2. U kunt een pushmelding verzenden vanuit Hallo [Azure Portal], zoals hierboven beschreven. Als u de code voor het verzenden van pushmeldingen in Hallo-app hebt toegevoegd, touch binnen Hallo tekst veld tooenter een melding. Druk op Hallo **verzenden** knop op Hallo toetsenbord of Hallo **melding verzenden** knop in Hallo weergave toosend Hallo-melding.
   
    ![Het verzenden van pushmeldingen in iOS-apps testen][34]
3. Hallo pushmelding wordt verzonden tooall-apparaten die geregistreerd tooreceive Hallo meldingen van de zijn specifieke Notification Hub Hallo.
   
    ![Het ontvangen van pushmeldingen in iOS-apps testen][35]

## <a name="next-steps"></a>Volgende stappen
In dit eenvoudige voorbeeld hebt u uitgezonden push notifications tooall uw geregistreerde iOS-apparaten. We raden een volgende stap in uw learning dat u verder gaan toohello [Azure Notification Hubs gebruikers waarschuwen voor iOS met .NET back-end] zelfstudie, dat u helpt bij het maken van een back-end toosend push meldingen met tags. 

Als u uw gebruikers op belangengroepen toosegment wilt, kunt u verder gaan toohello [Notification Hubs gebruiken toosend belangrijk nieuws] zelfstudie. 

Zie [Richtlijnen voor Notification Hubs] voor algemene informatie over Notification Hubs.

<!-- Images. -->

[6]: ./media/notification-hubs-ios-get-started/notification-hubs-configure-ios.png
[8]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app.png
[9]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app2.png
[10]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app3.png
[11]: ./media/notification-hubs-ios-get-started/notification-hubs-xcode-product-name.png

[30]: ./media/notification-hubs-ios-get-started/notification-hubs-test-send.png

[31]: ./media/notification-hubs-ios-get-started/notification-hubs-ios-ui.png
[32]: ./media/notification-hubs-ios-get-started/notification-hubs-storyboard-view.png
[33]: ./media/notification-hubs-ios-get-started/notification-hubs-test1.png
[34]: ./media/notification-hubs-ios-get-started/notification-hubs-test2.png
[35]: ./media/notification-hubs-ios-get-started/notification-hubs-test3.png



<!-- URLs. -->
[iOS SDK Mobile Services versie 1.2.4]: http://aka.ms/kymw2g
[Mobile Services iOS SDK]: http://go.microsoft.com/fwLink/?LinkID=266533
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Azure Classic Portal]: https://manage.windowsazure.com/
[Richtlijnen voor Notification Hubs]: http://msdn.microsoft.com/library/jj927170.aspx
[Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-ios-get-started-push.md
[Azure Notification Hubs gebruikers waarschuwen voor iOS met .NET back-end]: notification-hubs-aspnet-backend-ios-apple-apns-notification.md
[Notification Hubs gebruiken toosend belangrijk nieuws]: notification-hubs-ios-xplat-segmented-apns-push-notification.md

[Local and Push Notification Programming Guide]: http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW1
[Azure Portal]: https://portal.azure.com
