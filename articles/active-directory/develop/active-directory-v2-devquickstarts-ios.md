---
title: aaaAdd tooan-in iOS-toepassing met behulp van Azure AD v2.0-eindpunt Hallo | Microsoft Docs
description: Hoe toobuild een iOS-app die meldt zich aan gebruikers met beide persoonlijke Microsoft-account en werk-of schoolaccounts met behulp van de bibliotheken van derden.
services: active-directory
documentationcenter: 
author: brandwe
manager: mbaldwin
editor: 
ms.assetid: fd3603c0-42f7-438c-87b5-a52d20d6344b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 01/07/2017
ms.author: brandwe
ms.custom: aaddev
ms.openlocfilehash: a384062e6e4bd398a2b12318800728e627e05c32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-ios-app-using-a-third-party-library-with-graph-api-using-hello-v20-endpoint"></a>Aanmelden tooan iOS-app met behulp van een derde partij-bibliotheek met Graph API met behulp van Hallo v2.0-eindpunt toevoegen
Hallo Microsoft identity-platform gebruikt open standaarden, zoals OAuth2 en OpenID Connect. Ontwikkelaars kunnen een bibliotheek, ze toointegrate met onze services willen gebruiken. ons platform toohelp ontwikkelaars gebruiken met andere bibliotheken, hebben we hoe de enkele scenario's zoals deze één toodemonstrate geschreven tooconfigure van derden bibliotheken tooconnect toohello Microsoft identity-platform. De meeste bibliotheken die implementeren [hello RFC6749 OAuth2-specificatie](https://tools.ietf.org/html/rfc6749) verbinding kunnen maken van toohello Microsoft identity-platform.

Hallo-toepassing die in dit scenario maakt, kunnen gebruikers aanmelden tootheir organisatie en zoekt u naar anderen binnen hun organisatie met behulp van Hallo Graph API.

Als u nieuwe tooOAuth2 of OpenID Connect, kan veel van deze voorbeeldconfiguratie zin tooyou niet maken. Het is raadzaam dat u leest [v2.0-protocollen - stromen van OAuth 2.0 autorisatie Code](active-directory-v2-protocols-oauth-code.md) voor de achtergrond.

> [!NOTE]
> Sommige functies van ons platform waarvoor een expressie in Hallo OAuth2 of OpenID Connect standaarden, zoals voorwaardelijke toegang en beheer van Intune vereist u toouse onze open-source bibliotheken voor Microsoft Azure identiteit.
> 
> 

Hallo v2.0-eindpunt biedt geen ondersteuning voor alle Azure Active Directory-scenario's en onderdelen.

> [!NOTE]
> toodetermine als Hallo v2.0-eindpunt, moet u meer informatie over [v2.0 beperkingen](active-directory-v2-limitations.md).
> 
> 

## <a name="download-code-from-github"></a>Code vanuit GitHub downloaden
Hallo-code voor deze zelfstudie wordt bijgehouden [op GitHub](https://github.com/Azure-Samples/active-directory-ios-native-nxoauth2-v2).  toofollow langs, kunt u [basis van Hallo app downloaden als een ZIP-](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) of kloon Hallo basisproject:

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

U kunt ook gewoon Hallo voorbeeld downloaden en meteen aan de slag:

```
git clone git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

## <a name="register-an-app"></a>Een app registreren
Maak een nieuwe app op Hallo [toepassing registratieportal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), of volgen gedetailleerde stappen op Hallo [hoe tooregister een app met Hallo v2.0-eindpunt](active-directory-v2-app-registration.md).  Zorg ervoor dat:

* Kopiëren Hallo **toepassings-Id** die is toegewezen tooyour app omdat u hebt deze snel nodig.
* Hallo toevoegen **Mobile** platform voor uw app.
* Kopiëren Hallo **omleidings-URI** van Hallo-portal. Moet u de standaardwaarde Hallo van `urn:ietf:wg:oauth:2.0:oob`.

## <a name="download-hello-third-party-nxoauth2-library-and-create-a-workspace"></a>Hallo van derden NXOAuth2 bibliotheek downloaden en een werkruimte maken
Voor dit scenario moet u Hallo OAuth2Client vanuit GitHub, namelijk een OAuth2-bibliotheek voor Mac OS X- en iOS (Cocoa en Cocoa touch) gebruikt. Deze bibliotheek is gebaseerd op concept 10 van Hallo OAuth2-specificatie. Hallo systeemeigen toepassingsprofiel implementeert en ondersteunt Hallo autorisatie endpoint van Hallo-gebruiker. Dit zijn alles van hello, moet u toointegrate met Hallo Microsoft identiteitsplatform.

### <a name="add-hello-library-tooyour-project-by-using-cocoapods"></a>Hallo-bibliotheek tooyour project via CocoaPods toevoegen
CocoaPods is een hulpmiddel voor afhankelijkheidsbeheer voor Xcode-projecten. Het beheert vorige installatiestappen Hallo automatisch.

```
$ vi Podfile
```
1. Hallo toothis podfile volgende toevoegen:
   
    ```
     platform :ios, '8.0'
   
     target 'QuickStart' do
   
     pod 'NXOAuth2Client'
   
     end
    ```
2. Hallo podfile laden via CocoaPods. Hiermee maakt u een nieuwe Xcode-werkruimte die u gaat laden.
   
    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

## <a name="explore-hello-structure-of-hello-project"></a>Hallo-structuur van Hallo project verkennen
Hallo structuur te volgen is voor onze project in Hallo basisproject ingesteld:

* Een Master-weergave met een zoekopdracht UPN
* Een detailweergave voor Hallo gegevens over de geselecteerde gebruiker Hallo
* Een aanmelding weergave waar een gebruiker zich in toohello app tooquery Hallo grafiek aanmelden kunt

We wordt toovarious bestanden in Hallo geraamte tooadd verificatie verplaatst. Andere onderdelen van Hallo code, zoals visual code hello, tooidentity niet van toepassing zijn, maar zijn beschikbaar voor u.

## <a name="set-up-hello-settingsplst-file-in-hello-library"></a>Hallo settings.plst bestand instelt op Hallo-bibliotheek
* Open in Hallo Quick Start-project, Hallo `settings.plist` bestand. Vervang de waarden Hallo Hallo-elementen in Hallo sectie tooreflect Hallo waarden die u in hello Azure-portal gebruikt. Uw code zal naar deze waarden verwijzen wanneer Hallo Active Directory Authentication Library wordt gebruikt.
  * Hallo `clientId` Hallo client-ID van uw toepassing die u hebt gekopieerd uit de portal Hallo is.
  * Hallo `redirectUri` Hallo Omleidings-URL die Hallo portal opgegeven is.

## <a name="set-up-hello-nxoauth2client-library-in-your-loginviewcontroller"></a>Hallo NXOAuth2Client bibliotheek in uw LoginViewController instellen
Hallo NXOAuth2Client bibliotheek is vereist voor sommige waarden tooget instellen. Nadat u die taak hebt voltooid, kunt u Hallo verkregen token toocall Hallo Graph API. Omdat `LoginView` moet op elk gewenst moment worden aangeroepen moeten we tooauthenticate, is het zinvol tooput configuratiewaarden in toothat-bestand.

* We voegen sommige waarden toohello `LoginViewController.m` bestand tooset Hallo context voor verificatie en autorisatie. Meer informatie over Hallo waarden Volg Hallo-code.
  
    ```objc
    NSString *scopes = @"openid offline_access User.Read";
    NSString *authURL = @"https://login.microsoftonline.com/common/oauth2/v2.0/authorize";
    NSString *loginURL = @"https://login.microsoftonline.com/common/login";
    NSString *bhh = @"urn:ietf:wg:oauth:2.0:oob?code=";
    NSString *tokenURL = @"https://login.microsoftonline.com/common/oauth2/v2.0/token";
    NSString *keychain = @"com.microsoft.azureactivedirectory.samples.graph.QuickStart";
    static NSString * const kIDMOAuth2SuccessPagePrefix = @"session_state=";
    NSURL *myRequestedUrl;
    NSURL *myLoadedUrl;
    bool loginFlow = FALSE;
    bool isRequestBusy;
    NSURL *authcode;
    ```

Bekijk meer informatie over het Hallo-code.

de eerste tekenreeks Hallo is voor `scopes`.  Hallo `User.Read` waarde kunt u tooread Hallo basisprofiel Hallo gebruiker aangemeld.

U kunt meer informatie over alle beschikbare Hallo-scopes op [Microsoft Graph-machtigingsbereiken](https://graph.microsoft.io/docs/authorization/permission_scopes).

Voor `authURL`, `loginURL`, `bhh`, en `tokenURL`, moet u eerder opgegeven Hallo-waarden. Als u Hallo open-source bibliotheken voor Microsoft Azure identiteit gebruikt, halen we deze gegevens voor u met behulp van onze metagegevenseindpunt. We hebt Hallo harde werk van het extraheren van deze waarden voor u gedaan.

Hallo `keychain` waarde is het Hallo-container die Hallo NXOAuth2Client bibliotheek gebruikt een toostore sleutelhanger toocreate uw tokens. Als u tooget eenmalige aanmelding (SSO) via talrijke apps wilt, kunt u dezelfde sleutelhanger in elk van uw toepassingen Hallo en aanvragen Hallo gebruik van die sleutelhanger in uw Xcode-rechten. Dit wordt uitgelegd in Hallo Apple-documentatie.

Hallo rest van deze waarden zijn vereiste toouse Hallo-bibliotheek en locaties voor u toocarry waarden toohello context.

### <a name="create-a-url-cache"></a>Een URL-cache maken
Binnen `(void)viewDidLoad()`, die altijd wordt aangeroepen nadat Hallo weergave wordt geladen, hello volgende code primes een cache voor onze gebruik.

Hallo na code toevoegen:

```objc
- (void)viewDidLoad {
    [super viewDidLoad];
    self.loginView.delegate = self;
    [self setupOAuth2AccountStore];
    [self requestOAuth2Access];
    NSURLCache *URLCache = [[NSURLCache alloc] initWithMemoryCapacity:4 * 1024 * 1024
                                                         diskCapacity:20 * 1024 * 1024
                                                             diskPath:nil];
    [NSURLCache setSharedURLCache:URLCache];

}
```

### <a name="create-a-webview-for-sign-in"></a>Maken van een webweergave voor aanmelden
Een webweergave kunt Hallo gebruiker vragen om aanvullende factoren zoals SMS-bericht (indien geconfigureerd) of fout berichten toohello gebruiker retourneren. Hier moet u instellen Hallo webweergave en later schrijven Hallo code toohandle Hallo retouraanroepen gebeurt in Hallo webweergave van Hallo identity services.

```objc
-(void)requestOAuth2Access {
    //toosign in tooMicrosoft APIs using OAuth2, we must show an embedded browser (UIWebView)
    [[NXOAuth2AccountStore sharedStore] requestAccessToAccountWithType:@"myGraphService"
                                   withPreparedAuthorizationURLHandler:^(NSURL *preparedURL) {
                                       //navigate toohello URL returned by NXOAuth2Client

                                       NSURLRequest *r = [NSURLRequest requestWithURL:preparedURL];
                                       [self.loginView loadRequest:r];
                                   }];
}
```

### <a name="override-hello-webview-methods-toohandle-authentication"></a>Hallo webweergave methoden toohandle verificatie overschrijven
tootell Hallo webweergave wat er gebeurt wanneer een gebruiker nodig toosign in, zoals eerder besproken, kunt u Hallo na code plakken.

```objc
- (void)resolveUsingUIWebView:(NSURL *)URL {

    // We get hello auth token from a redirect so we need toohandle that in hello webview.

    if (![NSThread isMainThread]) {
        [self performSelectorOnMainThread:@selector(resolveUsingUIWebView:) withObject:URL waitUntilDone:YES];
        return;
    }

    NSURLRequest *hostnameURLRequest = [NSURLRequest requestWithURL:URL cachePolicy:NSURLRequestUseProtocolCachePolicy timeoutInterval:10.0f];
    isRequestBusy = YES;
    [self.loginView loadRequest:hostnameURLRequest];

    NSLog(@"resolveUsingUIWebView ready (status: UNKNOWN, URL: %@)", self.loginView.request.URL);
}

- (BOOL)webView:(UIWebView *)webView shouldStartLoadWithRequest:(NSURLRequest *)request navigationType:(UIWebViewNavigationType)navigationType {

    NSLog(@"webView:shouldStartLoadWithRequest: %@ (%li)", request.URL, (long)navigationType);

    // hello webview is where all hello communication happens. Slightly complicated.

    myLoadedUrl = [webView.request mainDocumentURL];
    NSLog(@"***Loaded url: %@", myLoadedUrl);

    //if hello UIWebView is showing our authorization URL or consent URL, show hello UIWebView control
    if ([request.URL.absoluteString rangeOfString:authURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:loginURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide hello UIWebView, we've left hello authorization flow
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:bhh options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide hello UIWebView, we've left hello authorization flow
        self.loginView.hidden = YES;
        [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }
    else {
        self.loginView.hidden = NO;
        //read hello Location from hello UIWebView, this is how Microsoft APIs is returning the
        //authentication code and relation information. This is controlled by hello redirect URL we chose toouse from Microsoft APIs
        //continue hello OAuth2 flow
       // [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }

    return YES;

}
```

### <a name="write-code-toohandle-hello-result-of-hello-oauth2-request"></a>Schrijven van code toohandle Hallo resultaat van Hallo OAuth2-aanvraag
Hallo wordt volgende code afgehandeld Hallo URL omleiding die uit Hallo webweergave retourneert. Als verificatie niet geslaagd is, probeert Hallo code het opnieuw. Hallo-bibliotheek biedt ondertussen Hallo-fout die u kunt zien in de beheerconsole Hallo of asynchroon verwerkt.

```objc
- (void)handleOAuth2AccessResult:(NSString *)accessResult {

    AppData* data = [AppData getInstance];

    //parse hello response for success or failure
     if (accessResult)
    //if success, complete hello OAuth2 flow by handling hello redirect URL and obtaining a token
     {
         [[NXOAuth2AccountStore sharedStore] handleRedirectURL:accessResult];
    } else {
        //start over
        [self requestOAuth2Access];
    }
}
```

### <a name="set-up-hello-oauth-context-called-account-store"></a>Hallo OAuth-Context (accountarchief genoemd) instellen
U kunt hier aanroepen `-[NXOAuth2AccountStore setClientID:secret:authorizationURL:tokenURL:redirectURL:forAccountType:]` op Hallo gedeelde accountarchief voor elke service die u wilt dat Hallo toepassing toobe kunnen tooaccess. Hallo-accounttype is een tekenreeks die wordt gebruikt als een id voor een bepaalde service. Omdat u Hallo Graph API gebruiken, Hallo code verwijst tooit als `"myGraphService"`. U instellen een zien die aangeven wanneer iets verandert met Hallo token vervolgens. Nadat u Hallo-token ophalen, u Hallo gebruiker back toohello terug `masterView`.

```objc
- (void)setupOAuth2AccountStore {


        AppData* data = [AppData getInstance];

    [[NXOAuth2AccountStore sharedStore] setClientID:data.clientId
                                             secret:data.secret
                                              scope:[NSSet setWithObject:scopes]
                                   authorizationURL:[NSURL URLWithString:authURL]
                                           tokenURL:[NSURL URLWithString:tokenURL]
                                        redirectURL:[NSURL URLWithString:data.redirectUriString]
                                      keyChainGroup: keychain
                                     forAccountType:@"myGraphService"];

    [[NSNotificationCenter defaultCenter] addObserverForName:NXOAuth2AccountStoreAccountsDidChangeNotification
                                                      object:[NXOAuth2AccountStore sharedStore]
                                                       queue:nil
                                                  usingBlock:^(NSNotification *aNotification) {
                                                      if (aNotification.userInfo) {
                                                          //account added, we have access
                                                          //we can now request protected data
                                                          NSLog(@"Success!! We have an access token.");
                                                          dispatch_async(dispatch_get_main_queue(),^ {

                                                              MasterViewController* masterViewController = [self.storyboard instantiateViewControllerWithIdentifier:@"masterView"];
                                                              [self.navigationController pushViewController:masterViewController animated:YES];
                                                          });
                                                      } else {
                                                          //account removed, we lost access
                                                      }
                                                  }];

    [[NSNotificationCenter defaultCenter] addObserverForName:NXOAuth2AccountStoreDidFailToRequestAccessNotification
                                                      object:[NXOAuth2AccountStore sharedStore]
                                                       queue:nil
                                                  usingBlock:^(NSNotification *aNotification) {
                                                      NSError *error = [aNotification.userInfo objectForKey:NXOAuth2AccountStoreErrorKey];
                                                      NSLog(@"Error!! %@", error.localizedDescription);
                                                  }];
}
```

## <a name="set-up-hello-master-view-toosearch-and-display-hello-users-from-hello-graph-api"></a>Hallo Master weergave toosearch instellen en gebruikers Hallo van Hallo Graph API weergeven
Een model-View-Controller (MVC)-app waarin gegevens worden geretourneerd in raster Hallo Hallo is buiten bereik van deze rondleiding Hallo en veel online zelfstudies wordt uitgelegd hoe toobuild een. Alle deze code wordt geraamte Hallo-bestand. U moet echter wel toodeal met een aantal items in deze MVC-toepassing:

* Wanneer een gebruiker iets in Hallo zoekveld onderscheppen
* Geef een object van de gegevens terug toohello MasterView zodat weer te resultaten Hallo in Hallo raster geven

We doen die hieronder.

### <a name="add-a-check-toosee-if-youre-logged-in"></a>Een selectievakje toosee toevoegen als u bent aangemeld
Hallo toepassing doet weinig als Hallo gebruiker niet is aangemeld, dus is het slimme toocheck als er al een token in Hallo-cache. Als niet zo is, wordt u omgeleid toohello LoginView voor Hallo gebruiker toosign in. Als u intrekt, Hallo aanbevolen manier toodo acties wanneer een weergave wordt geladen toouse Hallo is `viewDidLoad()` methode waarmee Apple ons.

```objc
- (void)viewDidLoad {
    [super viewDidLoad];


    NXOAuth2AccountStore *store = [NXOAuth2AccountStore sharedStore];
    NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];

        if (accounts.count == 0) {

        dispatch_async(dispatch_get_main_queue(),^ {

            LoginViewController* userSelectController = [self.storyboard instantiateViewControllerWithIdentifier:@"LoginUserView"];
            [self.navigationController pushViewController:userSelectController animated:YES];
        });
        }
```

### <a name="update-hello-table-view-when-data-is-received"></a>Hallo tabelweergave bijwerken wanneer gegevens worden ontvangen
Wanneer Hallo Graph API gegevens retourneert, moet u toodisplay Hallo gegevens. Voor eenvoud volgt hier alle Hallo tooupdate Hallo codetabel. Alleen kunt u de juiste waarden Hallo plakken in uw MVC standaardtekst code.

```objc
#pragma mark - Table View

- (NSInteger)numberOfSectionsInTableView:(UITableView *)tableView {
    return 1;
}

- (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section {

        return [upnArray count];
}

- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath {

    UITableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:@"TaskPrototypeCell" forIndexPath:indexPath];

    if ( cell == nil ) {
        cell = [[UITableViewCell alloc] initWithStyle:UITableViewCellStyleDefault reuseIdentifier:@"TaskPrototypeCell"];
    }

    User *user = nil;
     user = [upnArray objectAtIndex:indexPath.row];


    // Configure hello cell
    cell.textLabel.text = user.name;
    [cell setAccessoryType:UITableViewCellAccessoryDisclosureIndicator];

    return cell;
}

```

### <a name="provide-a-way-toocall-hello-graph-api-when-someone-types-in-hello-search-field"></a>Geef een manier toocall Hallo Graph API wanneer iemand in het veld van Hallo zoeken typt
Wanneer een gebruiker typt een zoekopdracht in Hallo vak, hoeft u tooshove die via toohello Graph API. Hallo `GraphAPICaller` klasse, die u in de volgende code Hallo bouwt, scheidt Hallo lookup functionaliteit van Hallo presentatie. Nu gaan we Hallo code schrijven waarmee een zoekopdracht tekens toohello Graph API-feeds. We dit doen door op te geven van een methode met de naam `lookupInGraph`, wat Hallo-tekenreeks die we willen toosearch voor duurt.

```objc

-(void)lookupInGraph:(NSString *)searchText {
if (searchText.length > 0) {

    };



        [GraphAPICaller searchUserList:searchText completionBlock:^(NSMutableArray* returnedUpns, NSError* error) {
            if (returnedUpns) {


                upnArray = returnedUpns;


            }
            else
            {
                UIAlertView *alertView = [[UIAlertView alloc]initWithTitle:nil message:[[NSString alloc]initWithFormat:@"Error : %@", error.localizedDescription] delegate:nil cancelButtonTitle:@"Retry" otherButtonTitles:@"Cancel", nil];

                [alertView setDelegate:self];

                dispatch_async(dispatch_get_main_queue(),^ {
                    [alertView show];
                });
            }


        }];


}
```

## <a name="write-a-helper-class-tooaccess-hello-graph-api"></a>Schrijven van een Helper-klasse tooaccess Hallo Graph API
Dit is Hallo kern van de toepassing. Hallo rest is code invoegen in Hallo standaardpatroon MVC bij Apple, hier maar geschreven code tooquery Hallo grafiek terwijl Hallo gebruiker typen en vervolgens deze gegevens worden geretourneerd. Hier is Hallo code en een gedetailleerde uitleg erop volgt.

### <a name="create-a-new-objective-c-header-file"></a>Maak een nieuw Objective C-header-bestand
Bestand met de Hallo `GraphAPICaller.h`, en Hallo volgende code toe te voegen.

```objc
@interface GraphAPICaller : NSObject<NSURLConnectionDataDelegate>

+(void) searchUserList:(NSString*)searchString
       completionBlock:(void (^) (NSMutableArray*, NSError* error))completionBlock;

@end
```

Hier ziet u dat een opgegeven methode een tekenreeks zijn wordt en een completionBlock retourneert. Deze completionBlock wordt als u mogelijk hebt geraden, bijgewerkt Hallo tabel verstrekken die een object met ingevulde gegevens in realtime Hallo gebruikers zoeken.

### <a name="create-a-new-objective-c-file"></a>Maak een nieuw Objective C-bestand
Bestand met de Hallo `GraphAPICaller.m`, en Hallo volgende methode toe te voegen.

```objc
+(void) searchUserList:(NSString*)searchString
       completionBlock:(void (^) (NSMutableArray* Users, NSError* error)) completionBlock
{
    if (!loadedApplicationSettings)
    {
        [self readApplicationSettings];
    }

    AppData* data = [AppData getInstance];

    NSString *graphURL = [NSString stringWithFormat:@"%@%@/users", data.graphApiUrlString, data.apiversion];

    NXOAuth2AccountStore *store = [NXOAuth2AccountStore sharedStore];
    NSDictionary* params = [self convertParamsToDictionary:searchString];

    NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];
    [NXOAuth2Request performMethod:@"GET"
                        onResource:[NSURL URLWithString:graphURL]
                   usingParameters:params
                       withAccount:accounts[0]
               sendProgressHandler:^(unsigned long long bytesSend, unsigned long long bytesTotal) {
                   // e.g., update a progress indicator
               }
                   responseHandler:^(NSURLResponse *response, NSData *responseData, NSError *error) {
                       // Process hello response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab hello top most JSON node tooget our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by hello key name being "value". It really is hello name of the
                           // first node. :-)

                           //each object is a key value pair
                           NSDictionary *keyValuePairs;
                           NSMutableArray* Users = [[NSMutableArray alloc]init];

                           for(int i =0; i < graphDataArray.count; i++)
                           {
                               keyValuePairs = [graphDataArray objectAtIndex:i];

                               User *s = [[User alloc]init];
                               s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                               s.name =[keyValuePairs valueForKey:@"displayName"];
                               s.mail =[keyValuePairs valueForKey:@"mail"];
                               s.businessPhones =[keyValuePairs valueForKey:@"businessPhones"];
                               s.mobilePhones =[keyValuePairs valueForKey:@"mobilePhone"];


                               [Users addObject:s];
                           }

                           completionBlock(Users, nil);
                       }
                       else
                       {
                           completionBlock(nil, error);
                       }

                   }];
}

```

We gaan met deze methode in detail.

Hallo-kern van deze code is in Hallo `NXOAuth2Request`, methode waarmee de Hallo parameters zijn vereist die u al hebt gedefinieerd in Hallo settings.plist-bestand.

de eerste stap Hallo is tooconstruct Hallo rechts Graph API-aanroep. Omdat u aanroept `/users`, u opgeven dat door deze toohello Graph API resource samen met de Hallo-versie toe te voegen. Het maakt zin tooput deze in een bestand met externe instellingen omdat deze wijzigen kunnen, zoals Hallo API ontwikkeld.

```objc
NSString *graphURL = [NSString stringWithFormat:@"%@%@/users", data.graphApiUrlString, data.apiversion];
```

Vervolgens moet u toospecify parameters dat u ook toohello Graph API-aanroep bieden. Het is *erg belangrijk* plaats Hallo-parameters niet in de resource-eindpunt Hallo omdat die is verwijderd voor alle niet-URI die voldoen tekens tijdens runtime. Alle querycode moet worden opgegeven in het Hallo-parameters.

```objc

NSDictionary* params = [self convertParamsToDictionary:searchString];
```

U wellicht opgevallen dat hiermee een `convertParamsToDictionary` methode die u nog niet hebt geschreven. Laten we dit nu doen aan Hallo einde van Hallo-bestand:

```objc
+(NSDictionary*) convertParamsToDictionary:(NSString*)searchString
{
    NSMutableDictionary* dictionary = [[NSMutableDictionary alloc]init];

        NSString *query = [NSString stringWithFormat:@"startswith(givenName, '%@')", searchString];

           [dictionary setValue:query forKey:@"$filter"];



    return dictionary;
}

```
Vervolgens gebruiken we Hallo `NXOAuth2Request` methode tooget gegevens weer van Hallo API in JSON-indeling.

```objc
NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];
    [NXOAuth2Request performMethod:@"GET"
                        onResource:[NSURL URLWithString:graphURL]
                   usingParameters:params
                       withAccount:accounts[0]
               sendProgressHandler:^(unsigned long long bytesSend, unsigned long long bytesTotal) {
                   // e.g., update a progress indicator
               }
                   responseHandler:^(NSURLResponse *response, NSData *responseData, NSError *error) {
                       // Process hello response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab hello top most JSON node tooget our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];
```

Ten slotte bekijken we hoe u Hallo gegevens toohello MasterViewController retourneren. Hallo gegevens retourneert als geserialiseerd en toobe gedeserialiseerd moet en geladen in een object dat Hallo MainViewController kan gebruiken. Voor dit doel Hallo basisproject heeft een `User.m/h` -bestand dat wordt gemaakt van een gebruikersobject. U vullen dat object gebruiker met informatie uit Hallo grafiek.

```objc
                           // We can grab hello top most JSON node tooget our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by hello key name being "value". It really is hello name of the
                           // first node. :-)

                           //each object is a key value pair
                           NSDictionary *keyValuePairs;
                           NSMutableArray* Users = [[NSMutableArray alloc]init];

                           for(int i =0; i < graphDataArray.count; i++)
                           {
                               keyValuePairs = [graphDataArray objectAtIndex:i];

                               User *s = [[User alloc]init];
                               s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                               s.name =[keyValuePairs valueForKey:@"displayName"];
                               s.mail =[keyValuePairs valueForKey:@"mail"];
                               s.businessPhones =[keyValuePairs valueForKey:@"businessPhones"];
                               s.mobilePhones =[keyValuePairs valueForKey:@"mobilePhone"];


                               [Users addObject:s];
```


## <a name="run-hello-sample"></a>Hallo-voorbeeld uitvoeren
Als u hebt gebruikt Hallo basisproject of gevolgd samen met de Hallo scenario moet nu uw toepassing uitvoeren. Hallo simulator Start en op **aanmelden** toouse Hallo-toepassing.

## <a name="get-security-updates-for-our-product"></a>Beveiligingsupdates voor onze product
We raden u tooget meldingen van wanneer er beveiligingsincidenten optreden door te bezoeken Hallo [Security TechCenter](https://technet.microsoft.com/security/dd252948) en u te abonneren tooSecurity Advisory Alerts.

