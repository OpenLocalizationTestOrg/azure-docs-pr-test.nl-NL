---
title: aaaAdd verificatie op iOS met Azure Mobile Apps
description: Meer informatie over hoe toouse Azure Mobile Apps tooauthenticate gebruikers van uw iOS-app via een groot aantal identiteitsproviders, waaronder AAD, Google, Facebook, Twitter en Microsoft.
services: app-service\mobile
documentationcenter: ios
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: ef3d3cbe-e7ca-45f9-987f-80c44209dc06
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: glenga
ms.openlocfilehash: df129e1c7517582db0e4705e0a6e98345ac8a48c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-ios-app"></a>Verificatie tooyour iOS-app toevoegen
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

In deze zelfstudie maakt u verificatie toohello toevoegen [iOS snel starten] project met een ondersteunde id-provider. Deze zelfstudie is gebaseerd op Hallo [iOS snel starten] zelfstudie die u moet eerst te voltooien.

## <a name="register"></a>Uw app registreren voor verificatie en Hallo App Service configureren
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="redirecturl"></a>Uw app toohello toegestane externe Omleidings-URL's toevoegen

Veilige verificatie vereist dat u een nieuwe URL-schema voor uw app definiëren.  Hierdoor Hallo verificatie system tooredirect back tooyour app zodra de Hallo verificatieproces is voltooid.  In deze zelfstudie gebruiken we het URL-schema _appname_ in.  U kunt echter een URL-schema dat u kiest.  Deze moet uniek tooyour mobiele toepassing.  Hallo-omleiding tooenable aan serverzijde th:

1. In Hallo [Azure-portal], selecteer uw App Service.

2. Klik op Hallo **verificatie / autorisatie** menuoptie.

3. Klik op **Azure Active Directory** onder Hallo **verificatieproviders** sectie.

4. Set Hallo **beheermodus** te**Geavanceerd**.

5. In Hallo **toegestaan externe Omleidings-URL's**, voer `appname://easyauth.callback`.  Hallo _appname_ in deze reeks is Hallo URL-schema voor uw mobiele toepassing.  Deze moet voldoen aan de normale URL-specificatie voor een protocol (Gebruik letters en cijfers alleen en begin met een letter).  U moet een notitie van Hallo-tekenreeks die u kiest, want u tooadjust uw code mobiele toepassing Hello URL-schema op verschillende plaatsen moet.

6. Klik op **OK**.

7. Klik op **Opslaan**.

## <a name="permissions"></a>Machtigingen tooauthenticated gebruikers beperken
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

Druk in Xcode op **uitvoeren** toostart Hallo app. Een uitzondering gegenereerd omdat Hallo app tooaccess de back-end als een niet-geverifieerde gebruiker probeert, maar Hallo *TodoItem* tabel nu is verificatie vereist.

## <a name="add-authentication"></a>Verificatie tooapp toevoegen
**Objective-C**:

1. Open op uw Mac *QSTodoListViewController.m* in Xcode en voeg Hallo volgende methode toe:

    ```Objective-C
    - (void)loginAndGetData
    {
        QSAppDelegate *appDelegate = (QSAppDelegate *)[UIApplication sharedApplication].delegate;
        appDelegate.qsTodoService = self.todoService;

        [self.todoService.client loginWithProvider:@"google" urlScheme:@"appname" controller:self animated:YES completion:^(MSUser * _Nullable user, NSError * _Nullable error) {
            if (error) {
                NSLog(@"Login failed with error: %@, %@", error, [error userInfo]);
            }
            else {
                self.todoService.client.currentUser = user;
                NSLog(@"User logged in: %@", user.userId);

                [self refresh];
            }
        }];
    }
    ```

    Wijziging *google* te*microsoftaccount*, *twitter*, *facebook*, of *windowsazureactivedirectory* als u Google niet als id-provider gebruikt. Als u Facebook gebruikt, moet u [geaccepteerde Facebook domeinen] [ 1] in uw app.

    Vervang Hallo **urlScheme** met een unieke naam voor uw toepassing.  Hallo urlScheme moet worden Hallo dezelfde als de URL-schema-protocol dat u hebt opgegeven in Hallo Hallo **toegestaan externe Omleidings-URL's** veld hello Azure-portal. Hallo urlScheme wordt gebruikt door Hallo verificatie callback tooswitch back tooyour toepassing nadat de authenticatie-aanvraag voltooid is.

2. Vervang `[self refresh]` in `viewDidLoad` in *QSTodoListViewController.m* Hello code te volgen:

    ```Objective-C
    [self loginAndGetData];
    ```

3. Open Hallo `QSAppDelegate.h` bestand en Hallo volgende code toe te voegen:

    ```Objective-C
    #import "QSTodoService.h"

    @property (strong, nonatomic) QSTodoService *qsTodoService;
    ```

4. Open Hallo `QSAppDelegate.m` bestand en Hallo volgende code toe te voegen:

    ```Objective-C
    - (BOOL)application:(UIApplication *)application openURL:(NSURL *)url options:(NSDictionary<UIApplicationOpenURLOptionsKey,id> *)options
    {
        if ([[url.scheme lowercaseString] isEqualToString:@"appname"]) {
            // Resume login flow
            return [self.qsTodoService.client resumeWithURL:url];
        }
        else {
            return NO;
        }
    }
    ```

   Voeg deze code direct vóór Hallo regel lezen `#pragma mark - Core Data stack`.  Vervang de _appname_ wih hello urlScheme waarde die u in stap 1 hebt gebruikt.

5. Open Hallo `AppName-Info.plist` bestand (vervang AppName met de naam van uw app Hallo) en voeg Hallo code te volgen:

    ```XML
    <key>CFBundleURLTypes</key>
    <array>
        <dict>
            <key>CFBundleURLName</key>
            <string>com.microsoft.azure.zumo</string>
            <key>CFBundleURLSchemes</key>
            <array>
                <string>appname</string>
            </array>
        </dict>
    </array>
    ```

    Deze code moet worden geplaatst in Hallo `<dict>` element.  Vervang Hallo _appname_ tekenreeks (binnen de matrix voor **CFBundleURLSchemes**) met app-naam Hallo u in stap 1 hebt gekozen.  U kunt deze wijzigingen ook aanbrengen in Hallo plist-editor - Klik op Hallo `AppName-Info.plist` bestand in XCode tooopen hello plist-editor.

    Vervang Hallo `com.microsoft.azure.zumo` de tekenreeks van **CFBundleURLName** bundel met uw Apple-id.

6. Druk op *uitvoeren* toostart Hallo app en meld u vervolgens. Wanneer u bent aangemeld, moet u kunnen tooview Hallo takenlijsten en bijwerken.

**SWIFT**:

1. Open op uw Mac *ToDoTableViewController.swift* in Xcode en voeg Hallo volgende methode toe:

    ```swift
    func loginAndGetData() {

        guard let client = self.table?.client, client.currentUser == nil else {
            return
        }

        let appDelegate = UIApplication.shared.delegate as! AppDelegate
        appDelegate.todoTableViewController = self

        let loginBlock: MSClientLoginBlock = {(user, error) -> Void in
            if (error != nil) {
                print("Error: \(error?.localizedDescription)")
            }
            else {
                client.currentUser = user
                print("User logged in: \(user?.userId)")
            }
        }

        client.login(withProvider:"google", urlScheme: "appname", controller: self, animated: true, completion: loginBlock)

    }
    ```

    Wijziging *google* te*microsoftaccount*, *twitter*, *facebook*, of *windowsazureactivedirectory* als u Google niet als id-provider gebruikt. Als u Facebook gebruikt, moet u [geaccepteerde Facebook domeinen] [ 1] in uw app.

    Vervang Hallo **urlScheme** met een unieke naam voor uw toepassing.  Hallo urlScheme moet worden Hallo dezelfde als de URL-schema-protocol dat u hebt opgegeven in Hallo Hallo **toegestaan externe Omleidings-URL's** veld hello Azure-portal. Hallo urlScheme wordt gebruikt door Hallo verificatie callback tooswitch back tooyour toepassing nadat de authenticatie-aanvraag voltooid is.

2. Verwijder Hallo regels `self.refreshControl?.beginRefreshing()` en `self.onRefresh(self.refreshControl)` aan het einde van `viewDidLoad()` in *ToDoTableViewController.swift*. Voeg een aanroep te`loginAndGetData()` op hun plaats:

    ```swift
    loginAndGetData()
    ```

3. Open Hallo `AppDelegate.swift` bestand en voeg Hallo regel toohello na `AppDelegate` klasse:

    ```swift
    var todoTableViewController: ToDoTableViewController?

    func application(_ application: UIApplication, openURL url: NSURL, options: [UIApplicationOpenURLOptionsKey : Any] = [:]) -> Bool {
        if url.scheme?.lowercased() == "appname" {
            return (todoTableViewController!.table?.client.resume(with: url as URL))!
        }
        else {
            return false
        }
    }
    ```

    Vervang Hallo _appname_ wih hello urlScheme waarde die u in stap 1 hebt gebruikt.

4. Open Hallo `AppName-Info.plist` bestand (vervang AppName met de naam van uw app Hallo) en voeg Hallo code te volgen:

    ```xml
    <key>CFBundleURLTypes</key>
    <array>
        <dict>
            <key>CFBundleURLName</key>
            <string>com.microsoft.azure.zumo</string>
            <key>CFBundleURLSchemes</key>
            <array>
                <string>appname</string>
            </array>
        </dict>
    </array>
    ```

    Deze code moet worden geplaatst in Hallo `<dict>` element.  Vervang Hallo _appname_ tekenreeks (binnen de matrix voor **CFBundleURLSchemes**) met app-naam Hallo u in stap 1 hebt gekozen.  U kunt deze wijzigingen ook aanbrengen in Hallo plist-editor - Klik op Hallo `AppName-Info.plist` bestand in XCode tooopen hello plist-editor.

    Vervang Hallo `com.microsoft.azure.zumo` de tekenreeks van **CFBundleURLName** bundel met uw Apple-id.

5. Druk op *uitvoeren* toostart Hallo app en meld u vervolgens. Wanneer u bent aangemeld, moet u kunnen tooview Hallo takenlijsten en bijwerken.

App Service-verificatie gebruikt appels Inter-App-communicatie.  Raadpleeg voor meer informatie over dit onderwerp toohello [Apple-documentatie][2]
<!-- URLs. -->

[1]: https://developers.facebook.com/docs/ios/ios9#whitelist
[2]: https://developer.apple.com/library/content/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Inter-AppCommunication/Inter-AppCommunication.html
[Azure-portal]: https://portal.azure.com

[iOS snel starten]: app-service-mobile-ios-get-started.md

