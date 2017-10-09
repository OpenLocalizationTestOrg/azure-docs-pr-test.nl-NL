---
title: aaaGet slag Hello Azure CDN-bibliotheek voor .NET | Microsoft Docs
description: Meer informatie over hoe toowrite .NET-toepassingen toomanage Azure CDN met Visual Studio.
services: cdn
documentationcenter: .net
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 63cf4101-92e7-49dd-a155-a90e54a792ca
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 9753e48c7469072cef6b2ac728e18c78121c97f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-cdn-development"></a>Aan de slag met Azure CDN-ontwikkeling
> [!div class="op_single_selector"]
> * [Node.js](cdn-app-dev-node.md)
> * [.NET](cdn-app-dev-net.md)
> 
> 

U kunt Hallo [Azure CDN-bibliotheek voor .NET](https://msdn.microsoft.com/library/mt657769.aspx) tooautomate maken en beheren van CDN-profielen en eindpunten.  Deze zelfstudie wordt begeleid Hallo maken van een eenvoudige .NET-consoletoepassing die u laat zien dat verschillende Hallo beschikbare bewerkingen.  Deze zelfstudie is niet bedoeld toodescribe alle aspecten van hello Azure CDN-bibliotheek voor .NET in detail.

U moet deze zelfstudie toocomplete Visual Studio 2015.  [Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) is gratis te downloaden.

> [!TIP]
> Hallo [voltooid project uit deze zelfstudie](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c) is beschikbaar voor downloaden op MSDN.
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-nuget-packages"></a>Maken van uw project en Nuget-pakketten toevoegen
Nu dat we hebben een resourcegroep gemaakt voor onze CDN-profielen en bepaalde onze Azure AD-toepassing machtiging toomanage CDN-profielen en de eindpunten in die groep, kunnen we beginnen met het maken van de toepassing.

Klik in Visual Studio 2015 op **bestand**, **nieuw**, **Project...**  tooopen Hallo het dialoogvenster new project.  Vouw **Visual C#**, selecteer daarna **Windows** in Hallo deelvenster op Hallo links.  Klik op **consoletoepassing** in Hallo middelste deelvenster.  Uw project een naam en klik vervolgens op **OK**.  

![Nieuw project](./media/cdn-app-dev-net/cdn-new-project.png)

Onze project gaat toouse sommige Azure-bibliotheken die zijn opgenomen in de Nuget-pakketten.  Laten we deze toohello-project toevoegen.

1. Klik op Hallo **extra** menu **Nuget Package Manager**, klikt u vervolgens **Package Manager Console**.
   
    ![Nuget-pakketten beheren](./media/cdn-app-dev-net/cdn-manage-nuget.png)
2. In Hallo Package Manager-Console, uitvoeren na de opdracht tooinstall Hallo Hallo **Active Directory Authentication Library (ADAL)**:
   
    `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory`
3. Uitvoeren van de volgende tooinstall Hallo Hallo **Azure CDN bibliotheek**:
   
    `Install-Package Microsoft.Azure.Management.Cdn`

## <a name="directives-constants-main-method-and-helper-methods"></a>Richtlijnen, constanten hoofdmethode en Help-methoden
Laten we ophalen Hallo basisstructuur van onze programma geschreven.

1. Vervang terug in Hallo Program.cs tabblad Hallo `using` richtlijnen boven Hallo Hallo volgende:
   
    ```csharp
    using System;
    using System.Collections.Generic;
    using Microsoft.Azure.Management.Cdn;
    using Microsoft.Azure.Management.Cdn.Models;
    using Microsoft.Azure.Management.Resources;
    using Microsoft.Azure.Management.Resources.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Rest;
    ```
2. We moeten toodefine sommige constanten die onze methoden gebruiken.  In Hallo `Program` klasse, maar voordat Hallo `Main` methode, voeg de volgende Hallo.  Worden ervoor tooreplace Hallo tijdelijke aanduidingen, met inbegrip van Hallo  **&lt;punthaken&gt;**, met uw eigen waarden zo nodig.
   
    ```csharp
    //Tenant app constants
    private const string clientID = "<YOUR CLIENT ID>";
    private const string clientSecret = "<YOUR CLIENT AUTHENTICATION KEY>"; //Only for service principals
    private const string authority = "https://login.microsoftonline.com/<YOUR TENANT ID>/<YOUR TENANT DOMAIN NAME>";
   
    //Application constants
    private const string subscriptionId = "<YOUR SUBSCRIPTION ID>";
    private const string profileName = "CdnConsoleApp";
    private const string endpointName = "<A UNIQUE NAME FOR YOUR CDN ENDPOINT>";
    private const string resourceGroupName = "CdnConsoleTutorial";
    private const string resourceLocation = "<YOUR PREFERRED AZURE LOCATION, SUCH AS Central US>";
    ```
3. Ook op het niveau van de klasse hello, deze twee variabelen definiëren.  We gebruiken deze later toodetermine als onze profiel en een eindpunt bestaat.
   
    ```csharp
    static bool profileAlreadyExists = false;
    static bool endpointAlreadyExists = false;
    ```
4. Vervang Hallo `Main` methode als volgt:
   
   ```csharp
   static void Main(string[] args)
   {
       //Get a token
       AuthenticationResult authResult = GetAccessToken();
   
       // Create CDN client
       CdnManagementClient cdn = new CdnManagementClient(new TokenCredentials(authResult.AccessToken))
           { SubscriptionId = subscriptionId };
   
       ListProfilesAndEndpoints(cdn);
   
       // Create CDN Profile
       CreateCdnProfile(cdn);
   
       // Create CDN Endpoint
       CreateCdnEndpoint(cdn);
   
       Console.WriteLine();
   
       // Purge CDN Endpoint
       PromptPurgeCdnEndpoint(cdn);
   
       // Delete CDN Endpoint
       PromptDeleteCdnEndpoint(cdn);
   
       // Delete CDN Profile
       PromptDeleteCdnProfile(cdn);
   
       Console.WriteLine("Press Enter tooend program.");
       Console.ReadLine();
   }
   ```
5. Enkele van onze andere methoden gaan tooprompt Hallo gebruiker met "Ja/Nee" vragen.  Hallo na methode toomake toevoegen die gemakkelijker:
   
    ```csharp
    private static bool PromptUser(string Question)
    {
        Console.Write(Question + " (Y/N): ");
        var response = Console.ReadKey();
        Console.WriteLine();
        if (response.Key == ConsoleKey.Y)
        {
            return true;
        }
        else if (response.Key == ConsoleKey.N)
        {
            return false;
        }
        else
        {
            // They pressed something other than Y or N.  Let's ask them again.
            return PromptUser(Question);
        }
    }
    ```

Nu dat de basisstructuur Hallo van het programma is geschreven, maken we Hallo methoden die worden aangeroepen door Hallo `Main` methode.

## <a name="authentication"></a>Authentication
Voordat we hello Azure CDN bibliotheek gebruiken kunt, moet we moet tooauthenticate onze service principal en geen verificatietoken ophalen.  Deze methode maakt gebruik van ADAL tooretrieve Hallo-token.

```csharp
private static AuthenticationResult GetAccessToken()
{
    AuthenticationContext authContext = new AuthenticationContext(authority); 
    ClientCredential credential = new ClientCredential(clientID, clientSecret);
    AuthenticationResult authResult = 
        authContext.AcquireTokenAsync("https://management.core.windows.net/", credential).Result;

    return authResult;
}
```

Als u afzonderlijke gebruikersverificatie, Hallo `GetAccessToken` methode er iets anders.

> [!IMPORTANT]
> Dit voorbeeld wordt alleen gebruiken als u afzonderlijke gebruikersverificatie toohave in plaats van een service-principal kiest.
> 
> 

```csharp
private static AuthenticationResult GetAccessToken()
{
    AuthenticationContext authContext = new AuthenticationContext(authority);
    AuthenticationResult authResult = authContext.AcquireTokenAsync("https://management.core.windows.net/",
        clientID, new Uri("http://<redirect URI>"), new PlatformParameters(PromptBehavior.RefreshSession)).Result;

    return authResult;
}
```

Ervoor tooreplace worden `<redirect URI>` Hello omleidings-URI die u hebt ingevoerd toen u de toepassing hello geregistreerd in Azure AD.

## <a name="list-cdn-profiles-and-endpoints"></a>Lijst met CDN-profielen en -eindpunten
Nu we klaar tooperform CDN bewerkingen.  Hello allereerst die onze webmethode is lijst alle Hallo profielen en -eindpunten in de resourcegroep en als er een overeenkomst wordt gevonden voor Hallo-profiel en -eindpunt namen opgegeven in onze constanten, maakt een notitie van die in voor later zodat we toocreate duplicaten niet proberen.

```csharp
private static void ListProfilesAndEndpoints(CdnManagementClient cdn)
{
    // List all hello CDN profiles in this resource group
    var profileList = cdn.Profiles.ListByResourceGroup(resourceGroupName);
    foreach (Profile p in profileList)
    {
        Console.WriteLine("CDN profile {0}", p.Name);
        if (p.Name.Equals(profileName, StringComparison.OrdinalIgnoreCase))
        {
            // Hey, that's hello name of hello CDN profile we want toocreate!
            profileAlreadyExists = true;
        }

        //List all hello CDN endpoints on this CDN profile
        Console.WriteLine("Endpoints:");
        var endpointList = cdn.Endpoints.ListByProfile(p.Name, resourceGroupName);
        foreach (Endpoint e in endpointList)
        {
            Console.WriteLine("-{0} ({1})", e.Name, e.HostName);
            if (e.Name.Equals(endpointName, StringComparison.OrdinalIgnoreCase))
            {
                // hello unique endpoint name already exists.
                endpointAlreadyExists = true;
            }
        }
        Console.WriteLine();
    }
}
```

## <a name="create-cdn-profiles-and-endpoints"></a>CDN-profielen en eindpunten maken
Vervolgens maken we een profiel.

```csharp
private static void CreateCdnProfile(CdnManagementClient cdn)
{
    if (profileAlreadyExists)
    {
        Console.WriteLine("Profile {0} already exists.", profileName);
    }
    else
    {
        Console.WriteLine("Creating profile {0}.", profileName);
        ProfileCreateParameters profileParms =
            new ProfileCreateParameters() { Location = resourceLocation, Sku = new Sku(SkuName.StandardVerizon) };
        cdn.Profiles.Create(profileName, profileParms, resourceGroupName);
    }
}
```

Zodra het Hallo-profiel is gemaakt, maakt u een eindpunt.

```csharp
private static void CreateCdnEndpoint(CdnManagementClient cdn)
{
    if (endpointAlreadyExists)
    {
        Console.WriteLine("Profile {0} already exists.", profileName);
    }
    else
    {
        Console.WriteLine("Creating endpoint {0} on profile {1}.", endpointName, profileName);
        EndpointCreateParameters endpointParms =
            new EndpointCreateParameters()
            {
                Origins = new List<DeepCreatedOrigin>() { new DeepCreatedOrigin("Contoso", "www.contoso.com") },
                IsHttpAllowed = true,
                IsHttpsAllowed = true,
                Location = resourceLocation
            };
        cdn.Endpoints.Create(endpointName, endpointParms, profileName, resourceGroupName);
    }
}
```

> [!NOTE]
> Hallo in bovenstaand voorbeeld wijst Hallo eindpunt een bron met de naam *Contoso* met een hostnaam `www.contoso.com`.  U moet deze toopoint tooyour eigen van de hostnaam van oorsprong wijzigen.
> 
> 

## <a name="purge-an-endpoint"></a>Een eindpunt leegmaken
Ervan uitgaande dat Hallo-eindpunt is gemaakt, is één algemene taak dat we tooperform in onze programma willen mogelijk opschonen Hallo inhoud in onze eindpunt.

```csharp
private static void PromptPurgeCdnEndpoint(CdnManagementClient cdn)
{
    if (PromptUser(String.Format("Purge CDN endpoint {0}?", endpointName)))
    {
        Console.WriteLine("Purging endpoint. Please wait...");
        cdn.Endpoints.PurgeContent(endpointName, profileName, resourceGroupName, new List<string>() { "/*" });
        Console.WriteLine("Done.");
        Console.WriteLine();
    }
}
```

> [!NOTE]
> Hallo Hallo bovenstaande voorbeeld tekenreeks `/*` geeft aan dat ik wil toopurge alles in de hoofdmap Hallo van Hallo eindpuntpad.  Dit is gelijkwaardig toochecking **alle opschonen** in hello Azure portal 'verwijderen' dialoogvenster. In Hallo `CreateCdnProfile` methode, ik heb gemaakt onze profiel als een **Azure CDN van Verizon** profiel met behulp van Hallo code `Sku = new Sku(SkuName.StandardVerizon)`, zodat dit geverifieerd worden kan.  Echter, **Azure CDN van Akamai** profielen bieden geen ondersteuning voor **alle opschonen**, dus als ik een profiel Akamai is voor deze zelfstudie gebruikt, ik tooinclude specifieke paden toopurge moet.
> 
> 

## <a name="delete-cdn-profiles-and-endpoints"></a>CDN-profielen en eindpunten verwijderen
onze eindpunt en het profiel verwijderd Hallo laatste methoden.

```csharp
private static void PromptDeleteCdnEndpoint(CdnManagementClient cdn)
{
    if(PromptUser(String.Format("Delete CDN endpoint {0} on profile {1}?", endpointName, profileName)))
    {
        Console.WriteLine("Deleting endpoint. Please wait...");
        cdn.Endpoints.DeleteIfExists(endpointName, profileName, resourceGroupName);
        Console.WriteLine("Done.");
        Console.WriteLine();
    }
}

private static void PromptDeleteCdnProfile(CdnManagementClient cdn)
{
    if(PromptUser(String.Format("Delete CDN profile {0}?", profileName)))
    {
        Console.WriteLine("Deleting profile. Please wait...");
        cdn.Profiles.DeleteIfExists(profileName, resourceGroupName);
        Console.WriteLine("Done.");
        Console.WriteLine();
    }
}
```

## <a name="running-hello-program"></a>Hallo-programma uitvoeren
We kunnen nu worden gecompileerd en Hallo programma uitvoeren door te klikken op Hallo **Start** knop in Visual Studio.

![Programma wordt uitgevoerd](./media/cdn-app-dev-net/cdn-program-running-1.png)

Wanneer Hallo programma Hallo hierboven prompt bereikt, moet u kunnen tooreturn tooyour resourcegroep in hello Azure-portal en Zie dat Hallo-profiel is gemaakt.

![Success!](./media/cdn-app-dev-net/cdn-success.png)

We kunnen vervolgens Hallo prompts toorun Hallo rest van Hallo programma bevestigen.

![Programma uitvoeren](./media/cdn-app-dev-net/cdn-program-running-2.png)

## <a name="next-steps"></a>Volgende stappen
toosee hello voltooid project van dit scenario [Hallo voorbeeld downloaden](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c).

toofind aanvullende documentatie over hello Azure CDN Management-bibliotheek voor .NET, weergave Hallo [-verwijzingen op MSDN](https://msdn.microsoft.com/library/mt657769.aspx).

Uw CDN-resources beheren met [PowerShell](cdn-manage-powershell.md).

