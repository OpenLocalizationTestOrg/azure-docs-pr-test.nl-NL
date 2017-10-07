---
title: aaaIntegrate Azure AD in een iOS-app | Microsoft Docs
description: "Hoe beveiligd toobuild een iOS-toepassing die kan worden geïntegreerd met Azure AD voor aanmelden en Azure AD-aanroepen API's met behulp van OAuth."
services: active-directory
documentationcenter: ios
author: brandwe
manager: mbaldwin
editor: 
ms.assetid: 42303177-9566-48ed-8abb-279fcf1e6ddb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 01/07/2017
ms.author: brandwe
ms.custom: aaddev
ms.openlocfilehash: 6e05745b2b2b122995dcba896ab0f2ed32509e3a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-an-ios-app"></a>Azure AD integreren met een iOS-app
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> Hallo Preview-versie van onze nieuwe [ontwikkelaarsportal](https://identity.microsoft.com/Docs/iOS) waarmee u leren werken met Azure Active Directory in een paar minuten!  Hallo-portal voor ontwikkelaars leidt u door het Hallo-proces voor het registreren van een app en Azure AD integreren in uw code.  Wanneer u klaar bent, hebt u een eenvoudige toepassing die gebruikers in uw tenant en een back-end die kunnen tokens accepteren en gevalideerd kan worden geverifieerd. 
> 
> 

Azure Active Directory (Azure AD) biedt Hallo Active Directory Authentication Library of ADAL voor iOS-clients hebt die tooaccess moeten bronnen beveiligde. ADAL eenvoudiger Hallo dat uw app gebruikmaakt van tooobtain toegangstokens. toodemonstrate hoe eenvoudig het is in dit artikel wordt een takenlijst Objective-C-toepassing bouwt die:

* Krijgt toegang tot tokens voor hello Azure AD Graph API aanroept met behulp van Hallo [OAuth 2.0-verificatieprotocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).
* Zoekt een directory voor gebruikers met een alias voor een gegeven.

toobuild hello volledige werkende toepassing, moet u:

1. Uw toepassing registreren met Azure AD.
2. Installeren en configureren van ADAL.
3. Gebruik ADAL tooget tokens van Azure AD.

tooget gestart, [Hallo app basisproject downloaden](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip) of [Hallo voltooid voorbeeld downloaden](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip). U moet ook een Azure AD-tenant kunt u gebruikers maken en een toepassing registreren. Als u niet al een tenant [meer informatie over hoe tooget een](active-directory-howto-tenant.md).


> [!TIP]
> Hallo Preview-versie van onze nieuwe [ontwikkelaarsportal](https://identity.microsoft.com/Docs/iOS) waarmee u leren werken met Azure AD in een paar minuten. Hallo-portal voor ontwikkelaars leidt u door het Hallo-proces voor het registreren van een app en Azure AD integreren in uw code. Wanneer u klaar bent, hebt u een eenvoudige toepassing die u kunt verificatie van gebruikers in uw tenant en een back-endnetwerk, kan tokens accepteren en valideren. 
> 
> 

## <a name="1-determine-what-your-redirect-uri-is-for-ios"></a>1. Bepalen welke uw omleidings-URI voor iOS is
toosecurely start uw toepassingen in bepaalde gevallen SSO, moet u een *omleidings-URI* in een bepaalde opmaak. Een omleidings-URI is gebruikte tooensure die Hallo tokens return toohello juiste toepassing die voor hen gevraagd.


Hallo iOS-indeling voor een omleidings-URI is:

```
<app-scheme>://<bundle-id>
```

* **App-schema** -dit is geregistreerd in uw XCode-project. Het is hoe andere toepassingen u kunnen aanroepen. U vindt dit onder Info.plist -> URL typen-URL-id >. Als u nog een of meer geconfigureerd hebt, moet u een maken.
* **bundel-id** -dit is bundel-id vinden onder 'id' hello ongedaan maken de projectinstellingen van uw in XCode.

Een voorbeeld van deze Quick Start-code: ***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***

## <a name="2-register-hello-directorysearcher-application"></a>2. Hallo DirectorySearcher toepassing registreren
tooset van uw app-tokens tooget, moet u eerst tooregister in uw Azure AD-tenant en verleen deze machtiging tooaccess hello Azure AD Graph API:

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Klik op de bovenste balk hello, uw account. Onder Hallo **Directory** Hallo Active Directory-tenant waar u tooregister Kies uw toepassing.
3. Klik op **meer Services** in Hallo meest linkse navigatievenster en selecteer vervolgens **Azure Active Directory**.
4. Klik op **App registraties**, en selecteer vervolgens **toevoegen**.
5. Ga als volgt Hallo vraagt toocreate een nieuwe **systeemeigen clienttoepassing**.
  * Hallo **naam** Hallo toepassing beschrijving van uw toepassing tooend gebruikers.
  * Hallo **omleidings-Uri** is een schema en de tekenreeks combinatie dat gebruikmaakt van Azure AD tooreturn token antwoorden.  Voer een waarde die specifieke tooyour toepassing is en is gebaseerd op Hallo vorige omleidings-URI informatie.
6. Nadat u Hallo-registratie hebt voltooid, wijst Azure AD van uw app een unieke toepassings-ID.  U moet deze waarde in de volgende secties hello, dus kopieer het van Hallo toepassingstabblad.
7. Van Hallo **instellingen** pagina **Required Permissions** en selecteer vervolgens **toevoegen**. Selecteer **Microsoft Graph** zoals Hallo API, en voeg vervolgens Hallo **Directory-gegevens lezen** machtiging onder **gedelegeerde machtigingen**.  Hiermee stelt u uw toepassing tooquery hello Azure AD Graph API voor gebruikers.

## <a name="3-install-and-configure-adal"></a>3. Installeren en configureren van ADAL
Nu dat u een toepassing in Azure AD hebt, kunt u ADAL installeert en uw identiteitsgerelateerde code schrijven.  ADAL toocommunicate met Azure AD, moet u tooprovide met enige informatie over de registratie van uw app.

1. Beginnen met het toevoegen van ADAL toohello DirectorySearcher project via CocoaPods.

    ```
    $ vi Podfile
    ```
2. Hallo toothis podfile volgende toevoegen:

    ```
    source 'https://github.com/CocoaPods/Specs.git'
    link_with ['QuickStart']
    xcodeproj 'QuickStart'

    pod 'ADALiOS'
    ```

3. Nu laden Hallo podfile via CocoaPods. Deze stap maakt een nieuwe XCode-werkruimte die u hebt geladen.

    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

4. Open Hallo plist-bestand in Hallo Quick Start-project, `settings.plist`.  Vervang de waarden Hallo Hallo-elementen in Hallo sectie tooreflect Hallo waarden die u hebt ingevoerd in hello Azure-portal. Uw code verwijst naar deze waarden wanneer deze gebruikmaakt van ADAL.
  * Hallo `tenant` Hallo domein van uw Azure AD-tenant, bijvoorbeeld: contoso.onmicrosoft.com.
  * Hallo `clientId` Hallo client-ID van uw toepassing die u hebt gekopieerd uit de portal Hallo is.
  * Hallo `redirectUri` Hallo Omleidings-URL die u hebt geregistreerd in de portal Hallo is.

## <a name="4----use-adal-tooget-tokens-from-azure-ad"></a>4.    Gebruik van ADAL tooget tokens van Azure AD
Hallo basisprincipe achter ADAL is dat wanneer uw app een toegangstoken moet, een completionBlock aanroept `+(void) getToken : `, en ADAL Hallo rest.  

1. In Hallo `QuickStart` project, open `GraphAPICaller.m` en zoek Hallo `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` Opmerking bij Hallo bovenkant.  Dit is waar u doorgeven ADAL Hallo coördinaten via een CompletionBlock, toocommunicate met Azure AD en meer over toocache tokens.

    ```ObjC
    +(void) getToken : (BOOL) clearCache
               parent:(UIViewController*) parent
    completionHandler:(void (^) (NSString*, NSError*))completionBlock;
    {
        AppData* data = [AppData getInstance];
        if(data.userItem){
            completionBlock(data.userItem.accessToken, nil);
            return;
        }

        ADAuthenticationError *error;
        authContext = [ADAuthenticationContext authenticationContextWithAuthority:data.authority error:&error];
        authContext.parentController = parent;
        NSURL *redirectUri = [[NSURL alloc]initWithString:data.redirectUriString];

        [ADAuthenticationSettings sharedInstance].enableFullScreen = YES;
        [authContext acquireTokenWithResource:data.resourceId
                                     clientId:data.clientId
                                  redirectUri:redirectUri
                               promptBehavior:AD_PROMPT_AUTO
                                       userId:data.userItem.userInformation.userId
                        extraQueryParameters: @"nux=1" // if this strikes you as strange it was legacy toodisplay hello correct mobile UX. You most likely won't need it in your code.
                             completionBlock:^(ADAuthenticationResult *result) {

                                  if (result.status != AD_SUCCEEDED)
                                  {
                                     completionBlock(nil, result.error);
                                  }
                                  else
                                  {
                                      data.userItem = result.tokenCacheStoreItem;
                                      completionBlock(result.tokenCacheStoreItem.accessToken, nil);
                                  }
                             }];
    }

    ```

2. Er moet nu toouse dit token toosearch voor gebruikers in het Hallo-grafiek. Hallo zoeken `// TODO: implement SearchUsersList` opmerking. Deze methode maakt een GET-aanvraag toohello Azure AD Graph API tooquery voor gebruikers wiens UPN met de Hallo zoekterm opgegeven begint.  tooquery hello Azure AD Graph API, moet u een access_token in Hallo tooinclude `Authorization` koptekst van Hallo-aanvraag. Dit is waar de ADAL wordt geleverd.

    ```ObjC
    +(void) searchUserList:(NSString*)searchString
                    parent:(UIViewController*) parent
          completionBlock:(void (^) (NSMutableArray* Users, NSError* error)) completionBlock
    {
        if (!loadedApplicationSettings)
       {
            [self readApplicationSettings];
        }
        
        AppData* data = [AppData getInstance];

        NSString *graphURL = [NSString stringWithFormat:@"%@%@/users?api-version=%@&$filter=startswith(userPrincipalName, '%@')", data.taskWebApiUrlString, data.tenant, data.apiversion, searchString];

        [self craftRequest:[self.class trimString:graphURL]
                    parent:parent
         completionHandler:^(NSMutableURLRequest *request, NSError *error) {

             if (error != nil)
             {
                 completionBlock(nil, error);
             }
             else
             {

                 NSOperationQueue *queue = [[NSOperationQueue alloc]init];

                 [NSURLConnection sendAsynchronousRequest:request queue:queue completionHandler:^(NSURLResponse *response, NSData *data, NSError *error) {

                     if (error == nil && data != nil){

                         NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:data options:0 error:nil];

                         // We can grab hello JSON node at hello top tooget our graph data.
                         NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                         // Don't be thrown off by hello key name being "value". It really is hello name of the
                         // first node. :-)

                         // Each object is a key value pair
                         NSDictionary *keyValuePairs;
                         NSMutableArray* Users = [[NSMutableArray alloc]init];

                         for(int i =0; i < graphDataArray.count; i++)
                         {
                             keyValuePairs = [graphDataArray objectAtIndex:i];

                             User *s = [[User alloc]init];
                             s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                             s.name =[keyValuePairs valueForKey:@"givenName"];

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
         }];

    }

    ```


3. Wanneer uw app een token aanvragen door het aanroepen van `getToken(...)`, ADAL probeert een token tooreturn zonder Hallo gebruiker wordt gevraagd om referenties.  Als ADAL dat die gebruiker Hallo moet toosign in een token tooget vaststelt, wordt deze weergegeven in het dialoogvenster voor aanmelding, Hallo gebruikersreferenties verzamelen en retourneert een token na een geslaagde authenticatie.  Als ADAL niet kunnen tooreturn een token voor een bepaalde reden, genereert een `AdalException`.

> [!Note] 
> Hallo `AuthenticationResult` object bevat een `tokenCacheStoreItem` -object dat kan worden gebruikt toocollect Hallo informatie die uw app mogelijk nodig. In de Quick Start, Hallo `tokenCacheStoreItem` gebruikte toodetermine is als verificatie is al voltooid.
>
>

## <a name="5-build-and-run-hello-application"></a>5. Hallo-toepassing bouwen en uitvoeren
Gefeliciteerd. U hebt nu een werkende iOS-toepassing kunt verificatie van gebruikers, veilig aanroepen van Web-API's met behulp van OAuth 2.0 en basisinformatie over Hallo gebruiker ophalen.  Als u nog niet gedaan hebt, is nu Hallo tijd toopopulate uw tenant waarbij sommige gebruikers.  Start uw app Quick Start en vervolgens weer aanmelden met een van deze gebruikers.  Zoeken naar andere gebruikers op basis van de UPN.  Hallo-app sluiten en opnieuw starten.  U ziet dat Hallo gebruikerssessie intact blijft.

ADAL maakt het eenvoudig tooincorporate al deze algemene identiteit functies in uw toepassing.  Dit zorgt voor alle Hallo dirty werk voor u, zoals het Cachebeheer van de OAuth-protocolondersteuning, Hallo-gebruiker met een gebruikersinterface toosign in presenteren en vernieuwen van tokens verlopen.  Alles wat u moet tooknow één API-aanroep is `getToken`.

Ter referentie: Hallo voltooid voorbeeld (zonder uw configuratiewaarden) wordt aangeboden op [GitHub](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).  

## <a name="next-steps"></a>Volgende stappen
U kunt nu verplaatsen op tooadditional scenario's.  U kunt tootry:

* [Een Node.JS-Web-API met Azure AD beveiligen](active-directory-devquickstarts-webapi-nodejs.md)
* Meer informatie over [hoe tooenable SSO cross-app voor iOS met ADAL](active-directory-sso-ios.md)  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

