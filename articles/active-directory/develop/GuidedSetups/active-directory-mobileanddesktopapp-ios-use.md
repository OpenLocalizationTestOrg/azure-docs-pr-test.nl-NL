---
title: Azure AD v2 iOS Getting Started - gebruik | Microsoft Docs
description: Hoe iOS (Swift)-toepassingen met een API waarvoor toegangstokens door Azure Active Directory-v2-eindpunt kunnen aanroepen
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: 2ac1117a31a101705539a1f75520ce8de43809a2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
## <a name="use-the-microsoft-authentication-library-msal-to-get-a-token-for-the-microsoft-graph-api"></a><span data-ttu-id="c71ec-103">De Microsoft Authentication Library (MSAL) gebruiken voor het ophalen van een token voor de Microsoft Graph-API</span><span class="sxs-lookup"><span data-stu-id="c71ec-103">Use the Microsoft Authentication Library (MSAL) to get a token for the Microsoft Graph API</span></span>

<span data-ttu-id="c71ec-104">Open `ViewController.swift` en vervang de code met:</span><span class="sxs-lookup"><span data-stu-id="c71ec-104">Open `ViewController.swift` and replace the code with:</span></span>

```swift
import UIKit
import MSAL

class ViewController: UIViewController, UITextFieldDelegate, URLSessionDelegate {
    
    let kClientID = "Your_Application_Id_Here"
    let kAuthority = "https://login.microsoftonline.com/common/v2.0"

    let kGraphURI = "https://graph.microsoft.com/v1.0/me/"
    let kScopes: [String] = ["https://graph.microsoft.com/user.read"]
    
    var accessToken = String()
    var applicationContext = MSALPublicClientApplication.init()

    @IBOutlet weak var loggingText: UITextView!
    @IBOutlet weak var signoutButton: UIButton!

     // This button will invoke the call to the Microsoft Graph API. It uses the
     // built in Swift libraries to create a connection.
    
    @IBAction func callGraphButton(_ sender: UIButton) {
        
        
        do {
            
            // We check to see if we have a current logged in user. If we don't, then we need to sign someone in.
            // We throw an interactionRequired so that we trigger the interactive signin.
            
            if  try self.applicationContext.users().isEmpty {
                throw NSError.init(domain: "MSALErrorDomain", code: MSALErrorCode.interactionRequired.rawValue, userInfo: nil)
            } else {
            
            // Acquire a token for an existing user silently
            
            try self.applicationContext.acquireTokenSilent(forScopes: self.kScopes, user: applicationContext.users().first) { (result, error) in
    
                    if error == nil {
                        self.accessToken = (result?.accessToken)!
                        self.loggingText.text = "Refreshing token silently)"
                        self.loggingText.text = "Refreshed Access token is \(self.accessToken)"
                        
                        self.signoutButton.isEnabled = true;
                        self.getContentWithToken()
    
                    } else {
                        self.loggingText.text = "Could not acquire token silently: \(error ?? "No error information" as! Error)"
    
                    }
                }
            }
        }  catch let error as NSError {
            
            // interactionRequired means we need to ask the user to sign-in. This usually happens
            // when the user's Refresh Token is expired or if the user has changed their password
            // among other possible reasons.
            
            if error.code == MSALErrorCode.interactionRequired.rawValue {
                
                self.applicationContext.acquireToken(forScopes: self.kScopes) { (result, error) in
                        if error == nil {
                            self.accessToken = (result?.accessToken)!
                            self.loggingText.text = "Access token is \(self.accessToken)"
                            self.signoutButton.isEnabled = true;
                            self.getContentWithToken()
                            
                        } else  {
                            self.loggingText.text = "Could not acquire token: \(error ?? "No error information" as! Error)"
                        }
                }
                
            }
            
        } catch {
            
            // This is the catch all error.
            
            self.loggingText.text = "Unable to acquire token. Got error: \(error)"
            
        }
    }

    override func viewDidLoad() {
        super.viewDidLoad()
        
        do {
             // Initialize a MSALPublicClientApplication with a given clientID and authority
            self.applicationContext = try MSALPublicClientApplication.init(clientId: kClientID, authority: kAuthority)
        } catch {
            self.loggingText.text = "Unable to create Application Context. Error: \(error)"
        }
    }


    override func didReceiveMemoryWarning() {
        super.didReceiveMemoryWarning()
        // Dispose of any resources that can be recreated.
    }
    
    override func viewWillAppear(_ animated: Bool) {
        
        if self.accessToken.isEmpty {
            signoutButton.isEnabled = false; 
        }
    }
}
```

<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="c71ec-105">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="c71ec-105">More Information</span></span>
#### <a name="getting-a-user-token-interactively"></a><span data-ttu-id="c71ec-106">Een gebruiker ophalen interactief token</span><span class="sxs-lookup"><span data-stu-id="c71ec-106">Getting a user token interactively</span></span>
<span data-ttu-id="c71ec-107">Het aanroepen van de `acquireToken` methode resulteert in een browservenster vraagt de gebruiker aan te melden.</span><span class="sxs-lookup"><span data-stu-id="c71ec-107">Calling the `acquireToken` method results in a browser window prompting the user to sign in.</span></span> <span data-ttu-id="c71ec-108">Toepassingen vereisen meestal een gebruiker zich aanmelden interactief de eerste keer dat ze nodig hebben voor toegang tot een beveiligde bron, of wanneer een achtergrond-bewerking te verkrijgen van een token mislukt (bijvoorbeeld van de gebruiker het wachtwoord verlopen).</span><span class="sxs-lookup"><span data-stu-id="c71ec-108">Applications usually require a user to sign in interactively the first time they need to access a protected resource, or when a silent operation to acquire a token fails (e.g. the user’s password expired).</span></span>

#### <a name="getting-a-user-token-silently"></a><span data-ttu-id="c71ec-109">Een gebruiker ophalen achtergrond token</span><span class="sxs-lookup"><span data-stu-id="c71ec-109">Getting a user token silently</span></span>
<span data-ttu-id="c71ec-110">De `acquireTokenSilent` methode verwerkt token acquisities van organisaties en verlenging zonder tussenkomst van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="c71ec-110">The `acquireTokenSilent` method handles token acquisitions and renewal without any user interaction.</span></span> <span data-ttu-id="c71ec-111">Na `acquireToken` wordt uitgevoerd voor de eerste keer `acquireTokenSilent` is de methode die vaak worden gebruikt voor het verkrijgen van tokens die worden gebruikt voor toegang tot beveiligde bronnen voor volgende aanroepen - aanroepen aan te vragen of vernieuwen van tokens op de achtergrond worden aangebracht.</span><span class="sxs-lookup"><span data-stu-id="c71ec-111">After `acquireToken` is executed for the first time, `acquireTokenSilent` is the method commonly used to obtain tokens used to access protected resources for subsequent calls - as calls to request or renew tokens are made silently.</span></span>

<span data-ttu-id="c71ec-112">Uiteindelijk `acquireTokenSilent` mislukt: bijvoorbeeld de gebruiker heeft zich afgemeld, of het wachtwoord op een ander apparaat is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="c71ec-112">Eventually, `acquireTokenSilent` will fail – e.g. the user has signed out, or has changed their password on another device.</span></span> <span data-ttu-id="c71ec-113">Wanneer MSAL detecteert dat het probleem doordat een interactieve actie kan worden omgezet, wordt deze gebeurtenis wordt gestart een `MSALErrorCode.interactionRequired` uitzondering.</span><span class="sxs-lookup"><span data-stu-id="c71ec-113">When MSAL detects that the issue can be resolved by requiring an interactive action, it fires an `MSALErrorCode.interactionRequired` exception.</span></span> <span data-ttu-id="c71ec-114">Uw toepassing kan verwerken van deze uitzondering op twee manieren:</span><span class="sxs-lookup"><span data-stu-id="c71ec-114">Your application can handle this exception in two ways:</span></span>

1.  <span data-ttu-id="c71ec-115">Een aanroep tegen `acquireToken` onmiddellijk, wat ertoe leidt de gebruiker aan te melden.</span><span class="sxs-lookup"><span data-stu-id="c71ec-115">Make a call against `acquireToken` immediately, which results in prompting the user to sign in.</span></span> <span data-ttu-id="c71ec-116">Dit patroon wordt meestal gebruikt in de on line toepassingen wanneer er geen offline inhoud in de toepassing beschikbaar is voor de gebruiker is.</span><span class="sxs-lookup"><span data-stu-id="c71ec-116">This pattern is usually used in online applications where there is no offline content in the application available for the user.</span></span> <span data-ttu-id="c71ec-117">Dit patroon maakt gebruik van de voorbeeldtoepassing die is gegenereerd door deze Begeleide instelprocedure: u kunt deze bekijken in actie de eerste keer dat u de toepassing uitvoert.</span><span class="sxs-lookup"><span data-stu-id="c71ec-117">The sample application generated by this guided setup uses this pattern: you can see it in action the first time you execute the application.</span></span> <span data-ttu-id="c71ec-118">Omdat er geen gebruiker ooit de toepassing gebruikt `applicationContext.users().first` bevat een null-waarde en een ` MSALErrorCode.interactionRequired ` uitzondering gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="c71ec-118">Because no user ever used the application, `applicationContext.users().first` will contain a null value, and an ` MSALErrorCode.interactionRequired ` exception will be thrown.</span></span> <span data-ttu-id="c71ec-119">De code in het voorbeeld de uitzondering wordt verwerkt door het aanroepen van `acquireToken` waardoor vraagt de gebruiker aan te melden.</span><span class="sxs-lookup"><span data-stu-id="c71ec-119">The code in the sample then handles the exception by calling `acquireToken` resulting in prompting the user to sign in.</span></span>

2.  <span data-ttu-id="c71ec-120">Toepassingen kunnen ook een visuele indicatie maken voor de gebruiker die een interactief aanmelden is vereist, zodat de gebruiker het juiste moment aan te melden kunt selecteren of de toepassing opnieuw kunt `acquireTokenSilent` op een later tijdstip.</span><span class="sxs-lookup"><span data-stu-id="c71ec-120">Applications can also make a visual indication to the user that an interactive sign-in is required, so the user can select the right time to sign in, or the application can retry `acquireTokenSilent` at a later time.</span></span> <span data-ttu-id="c71ec-121">Dit wordt meestal gebruikt wanneer de gebruiker andere functies van de toepassing gebruiken kunt zonder wordt onderbroken - bijvoorbeeld offline inhoud beschikbaar is in de toepassing is.</span><span class="sxs-lookup"><span data-stu-id="c71ec-121">This is usually used when the user can use other functionality of the application without being disrupted - for example, there is offline content available in the application.</span></span> <span data-ttu-id="c71ec-122">In dit geval wordt de gebruiker kunt bepalen wanneer ze willen aanmelden voor toegang tot de beveiligde bron, of om de verouderde gegevens te vernieuwen of uw toepassing kunt ervoor kiezen om opnieuw te proberen `acquireTokenSilent` wanneer netwerk is hersteld na een tijdelijk niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="c71ec-122">In this case, the user can decide when they want to sign in to access the protected resource, or to refresh the outdated information, or your application can decide to retry `acquireTokenSilent` when network is restored after being unavailable temporarily.</span></span>

<!--end-collapse-->

## <a name="call-the-microsoft-graph-api-using-the-token-you-just-obtained"></a><span data-ttu-id="c71ec-123">De Microsoft Graph API met behulp van het token dat u zojuist hebt verkregen aanroepen</span><span class="sxs-lookup"><span data-stu-id="c71ec-123">Call the Microsoft Graph API using the token you just obtained</span></span>

<span data-ttu-id="c71ec-124">Toevoegen van de nieuwe methode hieronder `ViewController.swift`.</span><span class="sxs-lookup"><span data-stu-id="c71ec-124">Add the new method below to `ViewController.swift`.</span></span> <span data-ttu-id="c71ec-125">Deze methode wordt gebruikt om een `GET` -aanvraag in voor de Microsoft Graph API met behulp van een *HTTP-autorisatie-header*:</span><span class="sxs-lookup"><span data-stu-id="c71ec-125">This method is used to make a `GET` request against the Microsoft Graph API using an *HTTP Authorization header*:</span></span>

```swift
func getContentWithToken() {
    
    let sessionConfig = URLSessionConfiguration.default
    
    // Specify the Graph API endpoint
    let url = URL(string: kGraphURI)
    var request = URLRequest(url: url!)
    
    // Set the Authorization header for the request. We use Bearer tokens, so we specify Bearer + the token we got from the result
    request.setValue("Bearer \(self.accessToken)", forHTTPHeaderField: "Authorization")
    let urlSession = URLSession(configuration: sessionConfig, delegate: self, delegateQueue: OperationQueue.main)
    
    urlSession.dataTask(with: request) { data, response, error in
        let result = try? JSONSerialization.jsonObject(with: data!, options: [])
                    if result != nil {
                
                self.loggingText.text = result.debugDescription
            }
        }.resume()
}
```

<!--start-collapse-->
### <a name="making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="c71ec-126">Maken van een REST-aanroep op basis van een beveiligde API</span><span class="sxs-lookup"><span data-stu-id="c71ec-126">Making a REST call against a protected API</span></span>

<span data-ttu-id="c71ec-127">In deze voorbeeldtoepassing de `getContentWithToken()` methode wordt gebruikt voor het maken van een HTTP `GET` aanvragen op basis van een beveiligde bron die is een token vereist en vervolgens de inhoud naar de aanroeper wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="c71ec-127">In this sample application, the `getContentWithToken()` method is used to make an HTTP `GET` request against a protected resource that requires a token and then return the content to the caller.</span></span> <span data-ttu-id="c71ec-128">Met deze methode wordt het token verkregen in de *HTTP-autorisatie-header*.</span><span class="sxs-lookup"><span data-stu-id="c71ec-128">This method adds the acquired token in the *HTTP Authorization header*.</span></span> <span data-ttu-id="c71ec-129">Voor dit voorbeeld wordt de resource is de Microsoft Graph API *mij* eindpunt – waarin informatie over het profiel van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="c71ec-129">For this sample, the resource is the Microsoft Graph API *me* endpoint – which displays the user's profile information.</span></span>
<!--end-collapse-->

## <a name="set-up-sign-out"></a><span data-ttu-id="c71ec-130">Afmelden instellen</span><span class="sxs-lookup"><span data-stu-id="c71ec-130">Set up sign-out</span></span>

<span data-ttu-id="c71ec-131">Voeg de volgende methode `ViewController.swift` afmelden van de gebruiker:</span><span class="sxs-lookup"><span data-stu-id="c71ec-131">Add the following method to `ViewController.swift` to sign out the user:</span></span>

```swift 
@IBAction func signoutButton(_ sender: UIButton) {

    do {
        
        // Removes all tokens from the cache for this application for the provided user
        // first parameter:   The user to remove from the cache
        
        try self.applicationContext.remove(self.applicationContext.users().first)
        self.signoutButton.isEnabled = false;
        
    } catch let error {
        self.loggingText.text = "Received error signing user out: \(error)"
    }
}
```
<!--start-collapse-->
### <a name="more-info-on-sign-out"></a><span data-ttu-id="c71ec-132">Meer informatie over afmelden</span><span class="sxs-lookup"><span data-stu-id="c71ec-132">More info on sign-out</span></span>

<span data-ttu-id="c71ec-133">De `signoutButton` methode wordt de gebruiker verwijderd uit de cache van de MSAL gebruiker – dit effectief laat weten MSAL vergeten van de huidige gebruiker, zodat een toekomstige aanvraag voor een token verkrijgen alleen lukt als het gaat interactief zijn.</span><span class="sxs-lookup"><span data-stu-id="c71ec-133">The `signoutButton` method removes the user from the MSAL user cache – this will effectively tell MSAL to forget the current user so a future request to acquire a token will only succeed if it is made to be interactive.</span></span>

<span data-ttu-id="c71ec-134">Hoewel de toepassing in dit voorbeeld een enkele gebruiker ondersteunt, ondersteunt MSAL scenario's waarbij meerdere accounts kunnen worden aangemeld op hetzelfde moment: een voorbeeld is een e-mailtoepassing waar een gebruiker heeft meerdere accounts.</span><span class="sxs-lookup"><span data-stu-id="c71ec-134">Although the application in this sample supports a single user, MSAL supports scenarios where multiple accounts can be signed in at the same time – an example is an email application where a user has multiple accounts.</span></span>
<!--end-collapse-->

## <a name="register-the-callback"></a><span data-ttu-id="c71ec-135">De callback registreren</span><span class="sxs-lookup"><span data-stu-id="c71ec-135">Register the callback</span></span>

<span data-ttu-id="c71ec-136">Zodra de gebruiker zich verifieert, wordt de gebruiker omgeleid naar de toepassing van de browser.</span><span class="sxs-lookup"><span data-stu-id="c71ec-136">Once the user authenticates, the browser redirects the user back to the application.</span></span> <span data-ttu-id="c71ec-137">Volg onderstaande stappen voor het registreren van deze callback:</span><span class="sxs-lookup"><span data-stu-id="c71ec-137">Follow the steps below to register this callback:</span></span>

1.  <span data-ttu-id="c71ec-138">Open `AppDelegate.swift` en MSAL importeren:</span><span class="sxs-lookup"><span data-stu-id="c71ec-138">Open `AppDelegate.swift` and import MSAL:</span></span>

```swift
import MSAL
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="c71ec-139">Voeg de volgende methode voor uw <code>AppDelegate</code> klasse voor het afhandelen van retouraanroepen:</span><span class="sxs-lookup"><span data-stu-id="c71ec-139">Add the following method to your <code>AppDelegate</code> class to handle callbacks:</span></span>
</li>
</ol>

```swift
// @brief Handles inbound URLs. Checks if the URL matches the redirect URI for a pending AppAuth
// authorization request and if so, will look for the code in the response.

func application(_ application: UIApplication, open url: URL, sourceApplication: String?, annotation: Any) -> Bool {
    
    print("Received callback!")
    
    MSALPublicClientApplication.handleMSALResponse(url)
    
    return true
}
```

