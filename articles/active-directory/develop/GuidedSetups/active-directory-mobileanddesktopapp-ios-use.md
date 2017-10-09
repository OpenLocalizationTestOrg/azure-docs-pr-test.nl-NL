---
title: aaaAzure AD v2 iOS Getting Started - gebruik | Microsoft Docs
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
ms.openlocfilehash: 22e67850e2e0b14b6d68815d8f23e18ce2e878ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
## <a name="use-hello-microsoft-authentication-library-msal-tooget-a-token-for-hello-microsoft-graph-api"></a>Hallo Microsoft Authentication Library (MSAL) tooget een token voor Hallo Microsoft Graph API gebruiken

Open `ViewController.swift` en vervang de code Hallo met:

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

     // This button will invoke hello call toohello Microsoft Graph API. It uses the
     // built in Swift libraries toocreate a connection.
    
    @IBAction func callGraphButton(_ sender: UIButton) {
        
        
        do {
            
            // We check toosee if we have a current logged in user. If we don't, then we need toosign someone in.
            // We throw an interactionRequired so that we trigger hello interactive signin.
            
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
            
            // interactionRequired means we need tooask hello user toosign-in. This usually happens
            // when hello user's Refresh Token is expired or if hello user has changed their password
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
            
            // This is hello catch all error.
            
            self.loggingText.text = "Unable tooacquire token. Got error: \(error)"
            
        }
    }

    override func viewDidLoad() {
        super.viewDidLoad()
        
        do {
             // Initialize a MSALPublicClientApplication with a given clientID and authority
            self.applicationContext = try MSALPublicClientApplication.init(clientId: kClientID, authority: kAuthority)
        } catch {
            self.loggingText.text = "Unable toocreate Application Context. Error: \(error)"
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
### <a name="more-information"></a>Meer informatie
#### <a name="getting-a-user-token-interactively"></a>Een gebruiker ophalen interactief token
Aanroepen Hallo `acquireToken` methode resulteert in een browser venster vragen Hallo toosign van de gebruiker in. Toepassingen zijn doorgaans vereist een gebruiker toosign in interactief Hallo eerste keer dat ze tooaccess moeten een beveiligde bron of wanneer een stille bewerking tooacquire een token mislukt (bijvoorbeeld Hallo gebruikerswachtwoord verlopen).

#### <a name="getting-a-user-token-silently"></a>Een gebruiker ophalen achtergrond token
Hallo `acquireTokenSilent` methode verwerkt token acquisities van organisaties en verlenging zonder tussenkomst van de gebruiker. Na `acquireToken` wordt uitgevoerd voor Hallo eerst `acquireTokenSilent` Hallo methode gebruikte tooobtain tokens die worden gebruikt tooaccess resources voor volgende aanroepen - beveiligd als aanroepen toorequest of vernieuwen van tokens achtergrond worden aangebracht.

Uiteindelijk `acquireTokenSilent` mislukt: bijvoorbeeld Hallo gebruiker heeft zich afgemeld of het wachtwoord op een ander apparaat is gewijzigd. Wanneer MSAL detecteert dat Hallo probleem doordat een interactieve actie kan worden omgezet, wordt deze gebeurtenis wordt gestart een `MSALErrorCode.interactionRequired` uitzondering. Uw toepassing kan verwerken van deze uitzondering op twee manieren:

1.  Een aanroep tegen `acquireToken` onmiddellijk, waardoor het vragen Hallo toosign van de gebruiker in. Dit patroon wordt meestal gebruikt in de on line toepassingen wanneer er geen offline inhoud in de toepassing hello beschikbaar voor Hallo-gebruiker is. Hallo-voorbeeldtoepassing die is gegenereerd door deze begeleide setup gebruikt dit patroon: u kunt deze bekijken in actie Hallo eerste keer dat u de toepassing hello uitvoert. Omdat er geen gebruiker ooit toepassing hello gebruikt, `applicationContext.users().first` bevat een null-waarde en een ` MSALErrorCode.interactionRequired ` uitzondering gegenereerd. code in de steekproef Hallo Hallo vervolgens ingangen Hallo uitzondering door aan te roepen `acquireToken` waardoor Hallo gebruiker toosign in te vragen.

2.  Toepassingen kunnen ook een visuele indicatie toohello-gebruiker die een interactief aanmelden is vereist, zodat Hallo-gebruiker kunt selecteren Hallo juiste moment toosign in of toepassing hello opnieuw kunt maken `acquireTokenSilent` op een later tijdstip. Dit wordt meestal gebruikt wanneer Hallo gebruiker andere functionaliteit van de toepassing hello gebruiken kunt zonder wordt onderbroken - bijvoorbeeld offline-inhoud in de toepassing hello beschikbaar is. In dit geval Hallo-gebruiker kunt bepalen wanneer hij of zij wil toosign in tooaccess Hallo beveiligde resource, toorefresh Hallo verouderde informatie of uw toepassing kunt bepalen tooretry `acquireTokenSilent` wanneer netwerk is hersteld na een tijdelijk niet beschikbaar.

<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a>Hallo Hallo-token die u zojuist hebt verkregen met Microsoft Graph-API niet aanroepen

Toevoegen van nieuwe methode Hallo onderstaande te`ViewController.swift`. Deze methode is gebruikte toomake een `GET` aanvraag tegen het gebruik van Hallo Microsoft Graph API een *HTTP-autorisatie-header*:

```swift
func getContentWithToken() {
    
    let sessionConfig = URLSessionConfiguration.default
    
    // Specify hello Graph API endpoint
    let url = URL(string: kGraphURI)
    var request = URLRequest(url: url!)
    
    // Set hello Authorization header for hello request. We use Bearer tokens, so we specify Bearer + hello token we got from hello result
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
### <a name="making-a-rest-call-against-a-protected-api"></a>Maken van een REST-aanroep op basis van een beveiligde API

In deze voorbeeldtoepassing Hallo `getContentWithToken()` methode is gebruikte toomake een HTTP `GET` -aanvraag in voor een beveiligde bron die een token en ga daarna terug Hallo inhoud toohello aanroeper vereist. Met deze methode wordt Hallo verkregen token in Hallo *HTTP-autorisatie-header*. Voor dit voorbeeld is Hallo resource Hallo Microsoft Graph API *mij* eindpunt – Hallo van gebruikersprofielgegevens worden weergegeven.
<!--end-collapse-->

## <a name="set-up-sign-out"></a>Afmelden instellen

Hallo methode te volgen toevoegen`ViewController.swift` toosign uit Hallo gebruiker:

```swift 
@IBAction func signoutButton(_ sender: UIButton) {

    do {
        
        // Removes all tokens from hello cache for this application for hello provided user
        // first parameter:   hello user tooremove from hello cache
        
        try self.applicationContext.remove(self.applicationContext.users().first)
        self.signoutButton.isEnabled = false;
        
    } catch let error {
        self.loggingText.text = "Received error signing user out: \(error)"
    }
}
```
<!--start-collapse-->
### <a name="more-info-on-sign-out"></a>Meer informatie over afmelden

Hallo `signoutButton` methode Hallo gebruiker verwijdert uit Hallo MSAL gebruikerscache – dit effectief laat weten MSAL tooforget Hallo huidige gebruiker zodat een tooacquire toekomstige aanvraag een token alleen slaagt als het gaat toobe interactieve.

Hoewel het Hallo-toepassing in dit voorbeeld ondersteunt een enkele gebruiker, MSAL scenario's waar meerdere accounts kunnen worden aangemeld op Hallo ondersteunt dezelfde tijd: een voorbeeld hiervan is een e-mailtoepassing waar een gebruiker heeft meerdere accounts.
<!--end-collapse-->

## <a name="register-hello-callback"></a>Hallo-callback registreren

Zodra het Hallo-gebruiker zich verifieert, leidt Hallo browser Hallo-Gebruikerstoepassing back toohello. Voer onderstaande tooregister Hallo stappen deze callback:

1.  Open `AppDelegate.swift` en MSAL importeren:

```swift
import MSAL
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
Hallo na methode tooyour toevoegen <code>AppDelegate</code> toohandle retouraanroepen klasse:
</li>
</ol>

```swift
// @brief Handles inbound URLs. Checks if hello URL matches hello redirect URI for a pending AppAuth
// authorization request and if so, will look for hello code in hello response.

func application(_ application: UIApplication, open url: URL, sourceApplication: String?, annotation: Any) -> Bool {
    
    print("Received callback!")
    
    MSALPublicClientApplication.handleMSALResponse(url)
    
    return true
}
```

