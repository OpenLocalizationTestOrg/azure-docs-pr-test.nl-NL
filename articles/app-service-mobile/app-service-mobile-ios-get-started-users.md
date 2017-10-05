---
title: Verificatie op iOS met Azure Mobile Apps toevoegen
description: "Informatie over het verifiëren van gebruikers van uw iOS-app via een groot aantal identiteitsproviders, waaronder AAD, Google, Facebook, Twitter en Microsoft met Azure Mobile Apps."
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
ms.openlocfilehash: 21a2cc6c1eaf4b34cbe8c2d7c4dbb69c8730cf32
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="add-authentication-to-your-ios-app"></a><span data-ttu-id="ecb97-103">Verificatie toevoegen aan uw iOS-app</span><span class="sxs-lookup"><span data-stu-id="ecb97-103">Add authentication to your iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="ecb97-104">In deze zelfstudie maakt u de verificatie van toevoegen de [iOS snel starten] project met een ondersteunde id-provider.</span><span class="sxs-lookup"><span data-stu-id="ecb97-104">In this tutorial, you add authentication to the [iOS quick start] project using a supported identity provider.</span></span> <span data-ttu-id="ecb97-105">Deze zelfstudie is gebaseerd op de [iOS snel starten] zelfstudie die u moet eerst te voltooien.</span><span class="sxs-lookup"><span data-stu-id="ecb97-105">This tutorial is based on the [iOS quick start] tutorial, which you must complete first.</span></span>

## <span data-ttu-id="ecb97-106"><a name="register"></a>Uw app registreren voor verificatie en de App Service configureren</span><span class="sxs-lookup"><span data-stu-id="ecb97-106"><a name="register"></a>Register your app for authentication and configure the App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="ecb97-107"><a name="redirecturl"></a>Uw app toevoegen aan de toegestane externe Omleidings-URL 's</span><span class="sxs-lookup"><span data-stu-id="ecb97-107"><a name="redirecturl"></a>Add your app to the Allowed External Redirect URLs</span></span>

<span data-ttu-id="ecb97-108">Veilige verificatie vereist dat u een nieuwe URL-schema voor uw app definiëren.</span><span class="sxs-lookup"><span data-stu-id="ecb97-108">Secure authentication requires that you define a new URL scheme for your app.</span></span>  <span data-ttu-id="ecb97-109">Hierdoor kan de verificatiesysteem terug te keren naar uw app zodra het verificatieproces voltooid is.</span><span class="sxs-lookup"><span data-stu-id="ecb97-109">This allows the authentication system to redirect back to your app once the authentication process is complete.</span></span>  <span data-ttu-id="ecb97-110">In deze zelfstudie gebruiken we het URL-schema _appname_ in.</span><span class="sxs-lookup"><span data-stu-id="ecb97-110">In this tutorial, we use the URL scheme _appname_ throughout.</span></span>  <span data-ttu-id="ecb97-111">U kunt echter een URL-schema dat u kiest.</span><span class="sxs-lookup"><span data-stu-id="ecb97-111">However, you can use any URL scheme you choose.</span></span>  <span data-ttu-id="ecb97-112">Deze moet uniek zijn voor uw mobiele App.</span><span class="sxs-lookup"><span data-stu-id="ecb97-112">It should be unique to your mobile application.</span></span>  <span data-ttu-id="ecb97-113">De omleiding aan serverzijde th inschakelen:</span><span class="sxs-lookup"><span data-stu-id="ecb97-113">To enable the redirection on th server side:</span></span>

1. <span data-ttu-id="ecb97-114">In de [Azure-portal], selecteer uw App Service.</span><span class="sxs-lookup"><span data-stu-id="ecb97-114">In the [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="ecb97-115">Klik op de **verificatie / autorisatie** menuoptie.</span><span class="sxs-lookup"><span data-stu-id="ecb97-115">Click the **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="ecb97-116">Klik op **Azure Active Directory** onder de **verificatieproviders** sectie.</span><span class="sxs-lookup"><span data-stu-id="ecb97-116">Click **Azure Active Directory** under the **Authentication Providers** section.</span></span>

4. <span data-ttu-id="ecb97-117">Stel de **beheermodus** naar **Geavanceerd**.</span><span class="sxs-lookup"><span data-stu-id="ecb97-117">Set the **Management mode** to **Advanced**.</span></span>

5. <span data-ttu-id="ecb97-118">In de **toegestaan externe Omleidings-URL's**, voer `appname://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="ecb97-118">In the **Allowed External Redirect URLs**, enter `appname://easyauth.callback`.</span></span>  <span data-ttu-id="ecb97-119">De _appname_ in deze tekenreeks wordt het URL-schema voor uw mobiele toepassing.</span><span class="sxs-lookup"><span data-stu-id="ecb97-119">The _appname_ in this string is the URL Scheme for your mobile application.</span></span>  <span data-ttu-id="ecb97-120">Deze moet voldoen aan de normale URL-specificatie voor een protocol (Gebruik letters en cijfers alleen en begin met een letter).</span><span class="sxs-lookup"><span data-stu-id="ecb97-120">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="ecb97-121">U moet een notitie van de tekenreeks die u naar wens aanpassen van uw mobiele toepassingscode met het URL-schema op verschillende plaatsen.</span><span class="sxs-lookup"><span data-stu-id="ecb97-121">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span></span>

6. <span data-ttu-id="ecb97-122">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="ecb97-122">Click **OK**.</span></span>

7. <span data-ttu-id="ecb97-123">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="ecb97-123">Click **Save**.</span></span>

## <span data-ttu-id="ecb97-124"><a name="permissions"></a>Machtigingen beperken voor geverifieerde gebruikers</span><span class="sxs-lookup"><span data-stu-id="ecb97-124"><a name="permissions"></a>Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="ecb97-125">Druk in Xcode op **uitvoeren** om de app te starten.</span><span class="sxs-lookup"><span data-stu-id="ecb97-125">In Xcode, press **Run** to start the app.</span></span> <span data-ttu-id="ecb97-126">Er is een uitzondering opgetreden omdat de app probeert te krijgen tot de back-end als niet-geverifieerde gebruiker, maar de *TodoItem* tabel nu is verificatie vereist.</span><span class="sxs-lookup"><span data-stu-id="ecb97-126">An exception is raised because the app attempts to access the backend as an unauthenticated user, but the *TodoItem* table now requires authentication.</span></span>

## <span data-ttu-id="ecb97-127"><a name="add-authentication"></a>Verificatie toevoegen aan de app</span><span class="sxs-lookup"><span data-stu-id="ecb97-127"><a name="add-authentication"></a>Add authentication to app</span></span>
<span data-ttu-id="ecb97-128">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ecb97-128">**Objective-C**:</span></span>

1. <span data-ttu-id="ecb97-129">Open op uw Mac *QSTodoListViewController.m* in Xcode en voeg de volgende methode toe:</span><span class="sxs-lookup"><span data-stu-id="ecb97-129">On your Mac, open *QSTodoListViewController.m* in Xcode and add the following method:</span></span>

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

    <span data-ttu-id="ecb97-130">Wijziging *google* naar *microsoftaccount*, *twitter*, *facebook*, of *windowsazureactivedirectory* als u Google niet als id-provider gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ecb97-130">Change *google* to *microsoftaccount*, *twitter*, *facebook*, or *windowsazureactivedirectory* if you are not using Google as your identity provider.</span></span> <span data-ttu-id="ecb97-131">Als u Facebook gebruikt, moet u [geaccepteerde Facebook domeinen] [ 1] in uw app.</span><span class="sxs-lookup"><span data-stu-id="ecb97-131">If you use Facebook, you must [whitelist Facebook domains][1] in your app.</span></span>

    <span data-ttu-id="ecb97-132">Vervang de **urlScheme** met een unieke naam voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="ecb97-132">Replace the **urlScheme** with a unique name for your application.</span></span>  <span data-ttu-id="ecb97-133">De urlScheme moet hetzelfde zijn als de URL-schema-protocol dat u hebt opgegeven in de **toegestaan externe Omleidings-URL's** veld in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ecb97-133">The urlScheme should be the same as the URL Scheme protocol that you specified in the **Allowed External Redirect URLs** field in the Azure portal.</span></span> <span data-ttu-id="ecb97-134">De urlScheme wordt gebruikt door de callback voor gebruikersverificatie overschakelen naar uw toepassing nadat de authenticatie-aanvraag voltooid is.</span><span class="sxs-lookup"><span data-stu-id="ecb97-134">The urlScheme is used by the authentication callback to switch back to your application after the authentication request is complete.</span></span>

2. <span data-ttu-id="ecb97-135">Vervang `[self refresh]` in `viewDidLoad` in *QSTodoListViewController.m* met de volgende code:</span><span class="sxs-lookup"><span data-stu-id="ecb97-135">Replace `[self refresh]` in `viewDidLoad` in *QSTodoListViewController.m* with the following code:</span></span>

    ```Objective-C
    [self loginAndGetData];
    ```

3. <span data-ttu-id="ecb97-136">Open de `QSAppDelegate.h` -bestand en voeg de volgende code:</span><span class="sxs-lookup"><span data-stu-id="ecb97-136">Open the `QSAppDelegate.h` file and add the following code:</span></span>

    ```Objective-C
    #import "QSTodoService.h"

    @property (strong, nonatomic) QSTodoService *qsTodoService;
    ```

4. <span data-ttu-id="ecb97-137">Open de `QSAppDelegate.m` -bestand en voeg de volgende code:</span><span class="sxs-lookup"><span data-stu-id="ecb97-137">Open the `QSAppDelegate.m` file and add the following code:</span></span>

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

   <span data-ttu-id="ecb97-138">Voeg deze code direct voor de regel lezen `#pragma mark - Core Data stack`.</span><span class="sxs-lookup"><span data-stu-id="ecb97-138">Add this code directly before the line reading `#pragma mark - Core Data stack`.</span></span>  <span data-ttu-id="ecb97-139">Vervang de _appname_ wih de urlScheme-waarde die u in stap 1 hebt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ecb97-139">Replace the _appname_ wih the urlScheme value that you used in step 1.</span></span>

5. <span data-ttu-id="ecb97-140">Open de `AppName-Info.plist` bestand (vervang AppName met de naam van uw app) en voeg de volgende code:</span><span class="sxs-lookup"><span data-stu-id="ecb97-140">Open the `AppName-Info.plist` file (replacing AppName with the name of your app), and add the following code:</span></span>

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

    <span data-ttu-id="ecb97-141">Deze code moet worden geplaatst in de `<dict>` element.</span><span class="sxs-lookup"><span data-stu-id="ecb97-141">This code should be placed inside the `<dict>` element.</span></span>  <span data-ttu-id="ecb97-142">Vervang de _appname_ tekenreeks (binnen de matrix voor **CFBundleURLSchemes**) met de naam van de app die u in stap 1 hebt gekozen.</span><span class="sxs-lookup"><span data-stu-id="ecb97-142">Replace the _appname_ string (within the array for **CFBundleURLSchemes**) with the app name you chose in step 1.</span></span>  <span data-ttu-id="ecb97-143">U kunt deze wijzigingen ook aanbrengen in de plist-editor - Klik op de `AppName-Info.plist` -bestand in XCode om de plist-editor te openen.</span><span class="sxs-lookup"><span data-stu-id="ecb97-143">You can also make these changes in the plist editor - click on the `AppName-Info.plist` file in XCode to open the plist editor.</span></span>

    <span data-ttu-id="ecb97-144">Vervang de `com.microsoft.azure.zumo` de tekenreeks van **CFBundleURLName** bundel met uw Apple-id.</span><span class="sxs-lookup"><span data-stu-id="ecb97-144">Replace the `com.microsoft.azure.zumo` string for **CFBundleURLName** with your Apple bundle identifier.</span></span>

6. <span data-ttu-id="ecb97-145">Druk op *uitvoeren* naar de app te starten en meld u vervolgens.</span><span class="sxs-lookup"><span data-stu-id="ecb97-145">Press *Run* to start the app, and then log in.</span></span> <span data-ttu-id="ecb97-146">Wanneer u bent aangemeld, moet u mogelijk zijn de takenlijst weergeven en bijwerken.</span><span class="sxs-lookup"><span data-stu-id="ecb97-146">When you are logged in, you should be able to view the Todo list and make updates.</span></span>

<span data-ttu-id="ecb97-147">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="ecb97-147">**Swift**:</span></span>

1. <span data-ttu-id="ecb97-148">Open op uw Mac *ToDoTableViewController.swift* in Xcode en voeg de volgende methode toe:</span><span class="sxs-lookup"><span data-stu-id="ecb97-148">On your Mac, open *ToDoTableViewController.swift* in Xcode and add the following method:</span></span>

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

    <span data-ttu-id="ecb97-149">Wijziging *google* naar *microsoftaccount*, *twitter*, *facebook*, of *windowsazureactivedirectory* als u Google niet als id-provider gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ecb97-149">Change *google* to *microsoftaccount*, *twitter*, *facebook*, or *windowsazureactivedirectory* if you are not using Google as your identity provider.</span></span> <span data-ttu-id="ecb97-150">Als u Facebook gebruikt, moet u [geaccepteerde Facebook domeinen] [ 1] in uw app.</span><span class="sxs-lookup"><span data-stu-id="ecb97-150">If you use Facebook, you must [whitelist Facebook domains][1] in your app.</span></span>

    <span data-ttu-id="ecb97-151">Vervang de **urlScheme** met een unieke naam voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="ecb97-151">Replace the **urlScheme** with a unique name for your application.</span></span>  <span data-ttu-id="ecb97-152">De urlScheme moet hetzelfde zijn als de URL-schema-protocol dat u hebt opgegeven in de **toegestaan externe Omleidings-URL's** veld in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ecb97-152">The urlScheme should be the same as the URL Scheme protocol that you specified in the **Allowed External Redirect URLs** field in the Azure portal.</span></span> <span data-ttu-id="ecb97-153">De urlScheme wordt gebruikt door de callback voor gebruikersverificatie overschakelen naar uw toepassing nadat de authenticatie-aanvraag voltooid is.</span><span class="sxs-lookup"><span data-stu-id="ecb97-153">The urlScheme is used by the authentication callback to switch back to your application after the authentication request is complete.</span></span>

2. <span data-ttu-id="ecb97-154">Verwijder de regels `self.refreshControl?.beginRefreshing()` en `self.onRefresh(self.refreshControl)` aan het einde van `viewDidLoad()` in *ToDoTableViewController.swift*.</span><span class="sxs-lookup"><span data-stu-id="ecb97-154">Remove the lines `self.refreshControl?.beginRefreshing()` and `self.onRefresh(self.refreshControl)` at the end of `viewDidLoad()` in *ToDoTableViewController.swift*.</span></span> <span data-ttu-id="ecb97-155">Voeg een aanroep naar `loginAndGetData()` op hun plaats:</span><span class="sxs-lookup"><span data-stu-id="ecb97-155">Add a call to `loginAndGetData()` in their place:</span></span>

    ```swift
    loginAndGetData()
    ```

3. <span data-ttu-id="ecb97-156">Open de `AppDelegate.swift` -bestand en voeg de volgende regel om de `AppDelegate` klasse:</span><span class="sxs-lookup"><span data-stu-id="ecb97-156">Open the `AppDelegate.swift` file and add the following line to the `AppDelegate` class:</span></span>

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

    <span data-ttu-id="ecb97-157">Vervang de _appname_ wih de urlScheme-waarde die u in stap 1 hebt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ecb97-157">Replace the _appname_ wih the urlScheme value that you used in step 1.</span></span>

4. <span data-ttu-id="ecb97-158">Open de `AppName-Info.plist` bestand (vervang AppName met de naam van uw app) en voeg de volgende code:</span><span class="sxs-lookup"><span data-stu-id="ecb97-158">Open the `AppName-Info.plist` file (replacing AppName with the name of your app), and add the following code:</span></span>

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

    <span data-ttu-id="ecb97-159">Deze code moet worden geplaatst in de `<dict>` element.</span><span class="sxs-lookup"><span data-stu-id="ecb97-159">This code should be placed inside the `<dict>` element.</span></span>  <span data-ttu-id="ecb97-160">Vervang de _appname_ tekenreeks (binnen de matrix voor **CFBundleURLSchemes**) met de naam van de app die u in stap 1 hebt gekozen.</span><span class="sxs-lookup"><span data-stu-id="ecb97-160">Replace the _appname_ string (within the array for **CFBundleURLSchemes**) with the app name you chose in step 1.</span></span>  <span data-ttu-id="ecb97-161">U kunt deze wijzigingen ook aanbrengen in de plist-editor - Klik op de `AppName-Info.plist` -bestand in XCode om de plist-editor te openen.</span><span class="sxs-lookup"><span data-stu-id="ecb97-161">You can also make these changes in the plist editor - click on the `AppName-Info.plist` file in XCode to open the plist editor.</span></span>

    <span data-ttu-id="ecb97-162">Vervang de `com.microsoft.azure.zumo` de tekenreeks van **CFBundleURLName** bundel met uw Apple-id.</span><span class="sxs-lookup"><span data-stu-id="ecb97-162">Replace the `com.microsoft.azure.zumo` string for **CFBundleURLName** with your Apple bundle identifier.</span></span>

5. <span data-ttu-id="ecb97-163">Druk op *uitvoeren* naar de app te starten en meld u vervolgens.</span><span class="sxs-lookup"><span data-stu-id="ecb97-163">Press *Run* to start the app, and then log in.</span></span> <span data-ttu-id="ecb97-164">Wanneer u bent aangemeld, moet u mogelijk zijn de takenlijst weergeven en bijwerken.</span><span class="sxs-lookup"><span data-stu-id="ecb97-164">When you are logged in, you should be able to view the Todo list and make updates.</span></span>

<span data-ttu-id="ecb97-165">App Service-verificatie gebruikt appels Inter-App-communicatie.</span><span class="sxs-lookup"><span data-stu-id="ecb97-165">App Service Authentication uses Apples Inter-App Communication.</span></span>  <span data-ttu-id="ecb97-166">Raadpleeg voor meer informatie over dit onderwerp, de [Apple-documentatie][2]</span><span class="sxs-lookup"><span data-stu-id="ecb97-166">For more details on this subject, refer to the [Apple Documentation][2]</span></span>
<!-- URLs. -->

[1]: https://developers.facebook.com/docs/ios/ios9#whitelist
[2]: https://developer.apple.com/library/content/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Inter-AppCommunication/Inter-AppCommunication.html
<span data-ttu-id="ecb97-167">[Azure-portal]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="ecb97-167">[Azure portal]: https://portal.azure.com</span></span>

<span data-ttu-id="ecb97-168">[iOS snel starten]: app-service-mobile-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="ecb97-168">[iOS quick start]: app-service-mobile-ios-get-started.md</span></span>

