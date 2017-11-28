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
# <a name="add-authentication-tooyour-ios-app"></a><span data-ttu-id="7242f-103">Verificatie tooyour iOS-app toevoegen</span><span class="sxs-lookup"><span data-stu-id="7242f-103">Add authentication tooyour iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="7242f-104">In deze zelfstudie maakt u verificatie toohello toevoegen [iOS snel starten] project met een ondersteunde id-provider.</span><span class="sxs-lookup"><span data-stu-id="7242f-104">In this tutorial, you add authentication toohello [iOS quick start] project using a supported identity provider.</span></span> <span data-ttu-id="7242f-105">Deze zelfstudie is gebaseerd op Hallo [iOS snel starten] zelfstudie die u moet eerst te voltooien.</span><span class="sxs-lookup"><span data-stu-id="7242f-105">This tutorial is based on hello [iOS quick start] tutorial, which you must complete first.</span></span>

## <span data-ttu-id="7242f-106"><a name="register"></a>Uw app registreren voor verificatie en Hallo App Service configureren</span><span class="sxs-lookup"><span data-stu-id="7242f-106"><a name="register"></a>Register your app for authentication and configure hello App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="7242f-107"><a name="redirecturl"></a>Uw app toohello toegestane externe Omleidings-URL's toevoegen</span><span class="sxs-lookup"><span data-stu-id="7242f-107"><a name="redirecturl"></a>Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="7242f-108">Veilige verificatie vereist dat u een nieuwe URL-schema voor uw app definiëren.</span><span class="sxs-lookup"><span data-stu-id="7242f-108">Secure authentication requires that you define a new URL scheme for your app.</span></span>  <span data-ttu-id="7242f-109">Hierdoor Hallo verificatie system tooredirect back tooyour app zodra de Hallo verificatieproces is voltooid.</span><span class="sxs-lookup"><span data-stu-id="7242f-109">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span>  <span data-ttu-id="7242f-110">In deze zelfstudie gebruiken we het URL-schema _appname_ in.</span><span class="sxs-lookup"><span data-stu-id="7242f-110">In this tutorial, we use the URL scheme _appname_ throughout.</span></span>  <span data-ttu-id="7242f-111">U kunt echter een URL-schema dat u kiest.</span><span class="sxs-lookup"><span data-stu-id="7242f-111">However, you can use any URL scheme you choose.</span></span>  <span data-ttu-id="7242f-112">Deze moet uniek tooyour mobiele toepassing.</span><span class="sxs-lookup"><span data-stu-id="7242f-112">It should be unique tooyour mobile application.</span></span>  <span data-ttu-id="7242f-113">Hallo-omleiding tooenable aan serverzijde th:</span><span class="sxs-lookup"><span data-stu-id="7242f-113">tooenable hello redirection on th server side:</span></span>

1. <span data-ttu-id="7242f-114">In Hallo [Azure-portal], selecteer uw App Service.</span><span class="sxs-lookup"><span data-stu-id="7242f-114">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="7242f-115">Klik op Hallo **verificatie / autorisatie** menuoptie.</span><span class="sxs-lookup"><span data-stu-id="7242f-115">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="7242f-116">Klik op **Azure Active Directory** onder Hallo **verificatieproviders** sectie.</span><span class="sxs-lookup"><span data-stu-id="7242f-116">Click **Azure Active Directory** under hello **Authentication Providers** section.</span></span>

4. <span data-ttu-id="7242f-117">Set Hallo **beheermodus** te**Geavanceerd**.</span><span class="sxs-lookup"><span data-stu-id="7242f-117">Set hello **Management mode** too**Advanced**.</span></span>

5. <span data-ttu-id="7242f-118">In Hallo **toegestaan externe Omleidings-URL's**, voer `appname://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="7242f-118">In hello **Allowed External Redirect URLs**, enter `appname://easyauth.callback`.</span></span>  <span data-ttu-id="7242f-119">Hallo _appname_ in deze reeks is Hallo URL-schema voor uw mobiele toepassing.</span><span class="sxs-lookup"><span data-stu-id="7242f-119">hello _appname_ in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="7242f-120">Deze moet voldoen aan de normale URL-specificatie voor een protocol (Gebruik letters en cijfers alleen en begin met een letter).</span><span class="sxs-lookup"><span data-stu-id="7242f-120">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="7242f-121">U moet een notitie van Hallo-tekenreeks die u kiest, want u tooadjust uw code mobiele toepassing Hello URL-schema op verschillende plaatsen moet.</span><span class="sxs-lookup"><span data-stu-id="7242f-121">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

6. <span data-ttu-id="7242f-122">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="7242f-122">Click **OK**.</span></span>

7. <span data-ttu-id="7242f-123">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="7242f-123">Click **Save**.</span></span>

## <span data-ttu-id="7242f-124"><a name="permissions"></a>Machtigingen tooauthenticated gebruikers beperken</span><span class="sxs-lookup"><span data-stu-id="7242f-124"><a name="permissions"></a>Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="7242f-125">Druk in Xcode op **uitvoeren** toostart Hallo app.</span><span class="sxs-lookup"><span data-stu-id="7242f-125">In Xcode, press **Run** toostart hello app.</span></span> <span data-ttu-id="7242f-126">Een uitzondering gegenereerd omdat Hallo app tooaccess de back-end als een niet-geverifieerde gebruiker probeert, maar Hallo *TodoItem* tabel nu is verificatie vereist.</span><span class="sxs-lookup"><span data-stu-id="7242f-126">An exception is raised because hello app attempts tooaccess the backend as an unauthenticated user, but hello *TodoItem* table now requires authentication.</span></span>

## <span data-ttu-id="7242f-127"><a name="add-authentication"></a>Verificatie tooapp toevoegen</span><span class="sxs-lookup"><span data-stu-id="7242f-127"><a name="add-authentication"></a>Add authentication tooapp</span></span>
<span data-ttu-id="7242f-128">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="7242f-128">**Objective-C**:</span></span>

1. <span data-ttu-id="7242f-129">Open op uw Mac *QSTodoListViewController.m* in Xcode en voeg Hallo volgende methode toe:</span><span class="sxs-lookup"><span data-stu-id="7242f-129">On your Mac, open *QSTodoListViewController.m* in Xcode and add hello following method:</span></span>

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

    <span data-ttu-id="7242f-130">Wijziging *google* te*microsoftaccount*, *twitter*, *facebook*, of *windowsazureactivedirectory* als u Google niet als id-provider gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7242f-130">Change *google* too*microsoftaccount*, *twitter*, *facebook*, or *windowsazureactivedirectory* if you are not using Google as your identity provider.</span></span> <span data-ttu-id="7242f-131">Als u Facebook gebruikt, moet u [geaccepteerde Facebook domeinen] [ 1] in uw app.</span><span class="sxs-lookup"><span data-stu-id="7242f-131">If you use Facebook, you must [whitelist Facebook domains][1] in your app.</span></span>

    <span data-ttu-id="7242f-132">Vervang Hallo **urlScheme** met een unieke naam voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="7242f-132">Replace hello **urlScheme** with a unique name for your application.</span></span>  <span data-ttu-id="7242f-133">Hallo urlScheme moet worden Hallo dezelfde als de URL-schema-protocol dat u hebt opgegeven in Hallo Hallo **toegestaan externe Omleidings-URL's** veld hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="7242f-133">hello urlScheme should be hello same as hello URL Scheme protocol that you specified in hello **Allowed External Redirect URLs** field in hello Azure portal.</span></span> <span data-ttu-id="7242f-134">Hallo urlScheme wordt gebruikt door Hallo verificatie callback tooswitch back tooyour toepassing nadat de authenticatie-aanvraag voltooid is.</span><span class="sxs-lookup"><span data-stu-id="7242f-134">hello urlScheme is used by hello authentication callback tooswitch back tooyour application after the authentication request is complete.</span></span>

2. <span data-ttu-id="7242f-135">Vervang `[self refresh]` in `viewDidLoad` in *QSTodoListViewController.m* Hello code te volgen:</span><span class="sxs-lookup"><span data-stu-id="7242f-135">Replace `[self refresh]` in `viewDidLoad` in *QSTodoListViewController.m* with hello following code:</span></span>

    ```Objective-C
    [self loginAndGetData];
    ```

3. <span data-ttu-id="7242f-136">Open Hallo `QSAppDelegate.h` bestand en Hallo volgende code toe te voegen:</span><span class="sxs-lookup"><span data-stu-id="7242f-136">Open hello `QSAppDelegate.h` file and add hello following code:</span></span>

    ```Objective-C
    #import "QSTodoService.h"

    @property (strong, nonatomic) QSTodoService *qsTodoService;
    ```

4. <span data-ttu-id="7242f-137">Open Hallo `QSAppDelegate.m` bestand en Hallo volgende code toe te voegen:</span><span class="sxs-lookup"><span data-stu-id="7242f-137">Open hello `QSAppDelegate.m` file and add hello following code:</span></span>

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

   <span data-ttu-id="7242f-138">Voeg deze code direct vóór Hallo regel lezen `#pragma mark - Core Data stack`.</span><span class="sxs-lookup"><span data-stu-id="7242f-138">Add this code directly before hello line reading `#pragma mark - Core Data stack`.</span></span>  <span data-ttu-id="7242f-139">Vervang de _appname_ wih hello urlScheme waarde die u in stap 1 hebt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7242f-139">Replace the _appname_ wih hello urlScheme value that you used in step 1.</span></span>

5. <span data-ttu-id="7242f-140">Open Hallo `AppName-Info.plist` bestand (vervang AppName met de naam van uw app Hallo) en voeg Hallo code te volgen:</span><span class="sxs-lookup"><span data-stu-id="7242f-140">Open hello `AppName-Info.plist` file (replacing AppName with hello name of your app), and add hello following code:</span></span>

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

    <span data-ttu-id="7242f-141">Deze code moet worden geplaatst in Hallo `<dict>` element.</span><span class="sxs-lookup"><span data-stu-id="7242f-141">This code should be placed inside hello `<dict>` element.</span></span>  <span data-ttu-id="7242f-142">Vervang Hallo _appname_ tekenreeks (binnen de matrix voor **CFBundleURLSchemes**) met app-naam Hallo u in stap 1 hebt gekozen.</span><span class="sxs-lookup"><span data-stu-id="7242f-142">Replace hello _appname_ string (within the array for **CFBundleURLSchemes**) with hello app name you chose in step 1.</span></span>  <span data-ttu-id="7242f-143">U kunt deze wijzigingen ook aanbrengen in Hallo plist-editor - Klik op Hallo `AppName-Info.plist` bestand in XCode tooopen hello plist-editor.</span><span class="sxs-lookup"><span data-stu-id="7242f-143">You can also make these changes in hello plist editor - click on hello `AppName-Info.plist` file in XCode tooopen hello plist editor.</span></span>

    <span data-ttu-id="7242f-144">Vervang Hallo `com.microsoft.azure.zumo` de tekenreeks van **CFBundleURLName** bundel met uw Apple-id.</span><span class="sxs-lookup"><span data-stu-id="7242f-144">Replace hello `com.microsoft.azure.zumo` string for **CFBundleURLName** with your Apple bundle identifier.</span></span>

6. <span data-ttu-id="7242f-145">Druk op *uitvoeren* toostart Hallo app en meld u vervolgens.</span><span class="sxs-lookup"><span data-stu-id="7242f-145">Press *Run* toostart hello app, and then log in.</span></span> <span data-ttu-id="7242f-146">Wanneer u bent aangemeld, moet u kunnen tooview Hallo takenlijsten en bijwerken.</span><span class="sxs-lookup"><span data-stu-id="7242f-146">When you are logged in, you should be able tooview hello Todo list and make updates.</span></span>

<span data-ttu-id="7242f-147">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="7242f-147">**Swift**:</span></span>

1. <span data-ttu-id="7242f-148">Open op uw Mac *ToDoTableViewController.swift* in Xcode en voeg Hallo volgende methode toe:</span><span class="sxs-lookup"><span data-stu-id="7242f-148">On your Mac, open *ToDoTableViewController.swift* in Xcode and add hello following method:</span></span>

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

    <span data-ttu-id="7242f-149">Wijziging *google* te*microsoftaccount*, *twitter*, *facebook*, of *windowsazureactivedirectory* als u Google niet als id-provider gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7242f-149">Change *google* too*microsoftaccount*, *twitter*, *facebook*, or *windowsazureactivedirectory* if you are not using Google as your identity provider.</span></span> <span data-ttu-id="7242f-150">Als u Facebook gebruikt, moet u [geaccepteerde Facebook domeinen] [ 1] in uw app.</span><span class="sxs-lookup"><span data-stu-id="7242f-150">If you use Facebook, you must [whitelist Facebook domains][1] in your app.</span></span>

    <span data-ttu-id="7242f-151">Vervang Hallo **urlScheme** met een unieke naam voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="7242f-151">Replace hello **urlScheme** with a unique name for your application.</span></span>  <span data-ttu-id="7242f-152">Hallo urlScheme moet worden Hallo dezelfde als de URL-schema-protocol dat u hebt opgegeven in Hallo Hallo **toegestaan externe Omleidings-URL's** veld hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="7242f-152">hello urlScheme should be hello same as hello URL Scheme protocol that you specified in hello **Allowed External Redirect URLs** field in hello Azure portal.</span></span> <span data-ttu-id="7242f-153">Hallo urlScheme wordt gebruikt door Hallo verificatie callback tooswitch back tooyour toepassing nadat de authenticatie-aanvraag voltooid is.</span><span class="sxs-lookup"><span data-stu-id="7242f-153">hello urlScheme is used by hello authentication callback tooswitch back tooyour application after the authentication request is complete.</span></span>

2. <span data-ttu-id="7242f-154">Verwijder Hallo regels `self.refreshControl?.beginRefreshing()` en `self.onRefresh(self.refreshControl)` aan het einde van `viewDidLoad()` in *ToDoTableViewController.swift*.</span><span class="sxs-lookup"><span data-stu-id="7242f-154">Remove hello lines `self.refreshControl?.beginRefreshing()` and `self.onRefresh(self.refreshControl)` at the end of `viewDidLoad()` in *ToDoTableViewController.swift*.</span></span> <span data-ttu-id="7242f-155">Voeg een aanroep te`loginAndGetData()` op hun plaats:</span><span class="sxs-lookup"><span data-stu-id="7242f-155">Add a call too`loginAndGetData()` in their place:</span></span>

    ```swift
    loginAndGetData()
    ```

3. <span data-ttu-id="7242f-156">Open Hallo `AppDelegate.swift` bestand en voeg Hallo regel toohello na `AppDelegate` klasse:</span><span class="sxs-lookup"><span data-stu-id="7242f-156">Open hello `AppDelegate.swift` file and add hello following line toohello `AppDelegate` class:</span></span>

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

    <span data-ttu-id="7242f-157">Vervang Hallo _appname_ wih hello urlScheme waarde die u in stap 1 hebt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7242f-157">Replace hello _appname_ wih hello urlScheme value that you used in step 1.</span></span>

4. <span data-ttu-id="7242f-158">Open Hallo `AppName-Info.plist` bestand (vervang AppName met de naam van uw app Hallo) en voeg Hallo code te volgen:</span><span class="sxs-lookup"><span data-stu-id="7242f-158">Open hello `AppName-Info.plist` file (replacing AppName with hello name of your app), and add hello following code:</span></span>

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

    <span data-ttu-id="7242f-159">Deze code moet worden geplaatst in Hallo `<dict>` element.</span><span class="sxs-lookup"><span data-stu-id="7242f-159">This code should be placed inside hello `<dict>` element.</span></span>  <span data-ttu-id="7242f-160">Vervang Hallo _appname_ tekenreeks (binnen de matrix voor **CFBundleURLSchemes**) met app-naam Hallo u in stap 1 hebt gekozen.</span><span class="sxs-lookup"><span data-stu-id="7242f-160">Replace hello _appname_ string (within the array for **CFBundleURLSchemes**) with hello app name you chose in step 1.</span></span>  <span data-ttu-id="7242f-161">U kunt deze wijzigingen ook aanbrengen in Hallo plist-editor - Klik op Hallo `AppName-Info.plist` bestand in XCode tooopen hello plist-editor.</span><span class="sxs-lookup"><span data-stu-id="7242f-161">You can also make these changes in hello plist editor - click on hello `AppName-Info.plist` file in XCode tooopen hello plist editor.</span></span>

    <span data-ttu-id="7242f-162">Vervang Hallo `com.microsoft.azure.zumo` de tekenreeks van **CFBundleURLName** bundel met uw Apple-id.</span><span class="sxs-lookup"><span data-stu-id="7242f-162">Replace hello `com.microsoft.azure.zumo` string for **CFBundleURLName** with your Apple bundle identifier.</span></span>

5. <span data-ttu-id="7242f-163">Druk op *uitvoeren* toostart Hallo app en meld u vervolgens.</span><span class="sxs-lookup"><span data-stu-id="7242f-163">Press *Run* toostart hello app, and then log in.</span></span> <span data-ttu-id="7242f-164">Wanneer u bent aangemeld, moet u kunnen tooview Hallo takenlijsten en bijwerken.</span><span class="sxs-lookup"><span data-stu-id="7242f-164">When you are logged in, you should be able tooview hello Todo list and make updates.</span></span>

<span data-ttu-id="7242f-165">App Service-verificatie gebruikt appels Inter-App-communicatie.</span><span class="sxs-lookup"><span data-stu-id="7242f-165">App Service Authentication uses Apples Inter-App Communication.</span></span>  <span data-ttu-id="7242f-166">Raadpleeg voor meer informatie over dit onderwerp toohello [Apple-documentatie][2]</span><span class="sxs-lookup"><span data-stu-id="7242f-166">For more details on this subject, refer toohello [Apple Documentation][2]</span></span>
<!-- URLs. -->

[1]: https://developers.facebook.com/docs/ios/ios9#whitelist
[2]: https://developer.apple.com/library/content/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Inter-AppCommunication/Inter-AppCommunication.html
[Azure-portal]: https://portal.azure.com

[iOS snel starten]: app-service-mobile-ios-get-started.md

