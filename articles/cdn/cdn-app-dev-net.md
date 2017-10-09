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
# <a name="get-started-with-azure-cdn-development"></a><span data-ttu-id="41572-103">Aan de slag met Azure CDN-ontwikkeling</span><span class="sxs-lookup"><span data-stu-id="41572-103">Get started with Azure CDN development</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="41572-104">Node.js</span><span class="sxs-lookup"><span data-stu-id="41572-104">Node.js</span></span>](cdn-app-dev-node.md)
> * [<span data-ttu-id="41572-105">.NET</span><span class="sxs-lookup"><span data-stu-id="41572-105">.NET</span></span>](cdn-app-dev-net.md)
> 
> 

<span data-ttu-id="41572-106">U kunt Hallo [Azure CDN-bibliotheek voor .NET](https://msdn.microsoft.com/library/mt657769.aspx) tooautomate maken en beheren van CDN-profielen en eindpunten.</span><span class="sxs-lookup"><span data-stu-id="41572-106">You can use hello [Azure CDN Library for .NET](https://msdn.microsoft.com/library/mt657769.aspx) tooautomate creation and management of CDN profiles and endpoints.</span></span>  <span data-ttu-id="41572-107">Deze zelfstudie wordt begeleid Hallo maken van een eenvoudige .NET-consoletoepassing die u laat zien dat verschillende Hallo beschikbare bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="41572-107">This tutorial walks through hello creation of a simple .NET console application that demonstrates several of hello available operations.</span></span>  <span data-ttu-id="41572-108">Deze zelfstudie is niet bedoeld toodescribe alle aspecten van hello Azure CDN-bibliotheek voor .NET in detail.</span><span class="sxs-lookup"><span data-stu-id="41572-108">This tutorial is not intended toodescribe all aspects of hello Azure CDN Library for .NET in detail.</span></span>

<span data-ttu-id="41572-109">U moet deze zelfstudie toocomplete Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="41572-109">You need Visual Studio 2015 toocomplete this tutorial.</span></span>  <span data-ttu-id="41572-110">[Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) is gratis te downloaden.</span><span class="sxs-lookup"><span data-stu-id="41572-110">[Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) is freely available for download.</span></span>

> [!TIP]
> <span data-ttu-id="41572-111">Hallo [voltooid project uit deze zelfstudie](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c) is beschikbaar voor downloaden op MSDN.</span><span class="sxs-lookup"><span data-stu-id="41572-111">hello [completed project from this tutorial](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c) is available for download on MSDN.</span></span>
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-nuget-packages"></a><span data-ttu-id="41572-112">Maken van uw project en Nuget-pakketten toevoegen</span><span class="sxs-lookup"><span data-stu-id="41572-112">Create your project and add Nuget packages</span></span>
<span data-ttu-id="41572-113">Nu dat we hebben een resourcegroep gemaakt voor onze CDN-profielen en bepaalde onze Azure AD-toepassing machtiging toomanage CDN-profielen en de eindpunten in die groep, kunnen we beginnen met het maken van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="41572-113">Now that we've created a resource group for our CDN profiles and given our Azure AD application permission toomanage CDN profiles and endpoints within that group, we can start creating our application.</span></span>

<span data-ttu-id="41572-114">Klik in Visual Studio 2015 op **bestand**, **nieuw**, **Project...**  tooopen Hallo het dialoogvenster new project.</span><span class="sxs-lookup"><span data-stu-id="41572-114">From within Visual Studio 2015, click **File**, **New**, **Project...** tooopen hello new project dialog.</span></span>  <span data-ttu-id="41572-115">Vouw **Visual C#**, selecteer daarna **Windows** in Hallo deelvenster op Hallo links.</span><span class="sxs-lookup"><span data-stu-id="41572-115">Expand **Visual C#**, then select **Windows** in hello pane on hello left.</span></span>  <span data-ttu-id="41572-116">Klik op **consoletoepassing** in Hallo middelste deelvenster.</span><span class="sxs-lookup"><span data-stu-id="41572-116">Click **Console Application** in hello center pane.</span></span>  <span data-ttu-id="41572-117">Uw project een naam en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="41572-117">Name your project, then click **OK**.</span></span>  

![Nieuw project](./media/cdn-app-dev-net/cdn-new-project.png)

<span data-ttu-id="41572-119">Onze project gaat toouse sommige Azure-bibliotheken die zijn opgenomen in de Nuget-pakketten.</span><span class="sxs-lookup"><span data-stu-id="41572-119">Our project is going toouse some Azure libraries contained in Nuget packages.</span></span>  <span data-ttu-id="41572-120">Laten we deze toohello-project toevoegen.</span><span class="sxs-lookup"><span data-stu-id="41572-120">Let's add those toohello project.</span></span>

1. <span data-ttu-id="41572-121">Klik op Hallo **extra** menu **Nuget Package Manager**, klikt u vervolgens **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="41572-121">Click hello **Tools** menu, **Nuget Package Manager**, then **Package Manager Console**.</span></span>
   
    ![Nuget-pakketten beheren](./media/cdn-app-dev-net/cdn-manage-nuget.png)
2. <span data-ttu-id="41572-123">In Hallo Package Manager-Console, uitvoeren na de opdracht tooinstall Hallo Hallo **Active Directory Authentication Library (ADAL)**:</span><span class="sxs-lookup"><span data-stu-id="41572-123">In hello Package Manager Console, execute hello following command tooinstall hello **Active Directory Authentication Library (ADAL)**:</span></span>
   
    `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory`
3. <span data-ttu-id="41572-124">Uitvoeren van de volgende tooinstall Hallo Hallo **Azure CDN bibliotheek**:</span><span class="sxs-lookup"><span data-stu-id="41572-124">Execute hello following tooinstall hello **Azure CDN Management Library**:</span></span>
   
    `Install-Package Microsoft.Azure.Management.Cdn`

## <a name="directives-constants-main-method-and-helper-methods"></a><span data-ttu-id="41572-125">Richtlijnen, constanten hoofdmethode en Help-methoden</span><span class="sxs-lookup"><span data-stu-id="41572-125">Directives, constants, main method, and helper methods</span></span>
<span data-ttu-id="41572-126">Laten we ophalen Hallo basisstructuur van onze programma geschreven.</span><span class="sxs-lookup"><span data-stu-id="41572-126">Let's get hello basic structure of our program written.</span></span>

1. <span data-ttu-id="41572-127">Vervang terug in Hallo Program.cs tabblad Hallo `using` richtlijnen boven Hallo Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="41572-127">Back in hello Program.cs tab, replace hello `using` directives at hello top with hello following:</span></span>
   
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
2. <span data-ttu-id="41572-128">We moeten toodefine sommige constanten die onze methoden gebruiken.</span><span class="sxs-lookup"><span data-stu-id="41572-128">We need toodefine some constants our methods will use.</span></span>  <span data-ttu-id="41572-129">In Hallo `Program` klasse, maar voordat Hallo `Main` methode, voeg de volgende Hallo.</span><span class="sxs-lookup"><span data-stu-id="41572-129">In hello `Program` class, but before hello `Main` method, add hello following.</span></span>  <span data-ttu-id="41572-130">Worden ervoor tooreplace Hallo tijdelijke aanduidingen, met inbegrip van Hallo  **&lt;punthaken&gt;**, met uw eigen waarden zo nodig.</span><span class="sxs-lookup"><span data-stu-id="41572-130">Be sure tooreplace hello placeholders, including hello **&lt;angle brackets&gt;**, with your own values as needed.</span></span>
   
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
3. <span data-ttu-id="41572-131">Ook op het niveau van de klasse hello, deze twee variabelen definiëren.</span><span class="sxs-lookup"><span data-stu-id="41572-131">Also at hello class level, define these two variables.</span></span>  <span data-ttu-id="41572-132">We gebruiken deze later toodetermine als onze profiel en een eindpunt bestaat.</span><span class="sxs-lookup"><span data-stu-id="41572-132">We'll use these later toodetermine if our profile and endpoint already exist.</span></span>
   
    ```csharp
    static bool profileAlreadyExists = false;
    static bool endpointAlreadyExists = false;
    ```
4. <span data-ttu-id="41572-133">Vervang Hallo `Main` methode als volgt:</span><span class="sxs-lookup"><span data-stu-id="41572-133">Replace hello `Main` method as follows:</span></span>
   
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
5. <span data-ttu-id="41572-134">Enkele van onze andere methoden gaan tooprompt Hallo gebruiker met "Ja/Nee" vragen.</span><span class="sxs-lookup"><span data-stu-id="41572-134">Some of our other methods are going tooprompt hello user with "Yes/No" questions.</span></span>  <span data-ttu-id="41572-135">Hallo na methode toomake toevoegen die gemakkelijker:</span><span class="sxs-lookup"><span data-stu-id="41572-135">Add hello following method toomake that a little easier:</span></span>
   
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

<span data-ttu-id="41572-136">Nu dat de basisstructuur Hallo van het programma is geschreven, maken we Hallo methoden die worden aangeroepen door Hallo `Main` methode.</span><span class="sxs-lookup"><span data-stu-id="41572-136">Now that hello basic structure of our program is written, we should create hello methods called by hello `Main` method.</span></span>

## <a name="authentication"></a><span data-ttu-id="41572-137">Authentication</span><span class="sxs-lookup"><span data-stu-id="41572-137">Authentication</span></span>
<span data-ttu-id="41572-138">Voordat we hello Azure CDN bibliotheek gebruiken kunt, moet we moet tooauthenticate onze service principal en geen verificatietoken ophalen.</span><span class="sxs-lookup"><span data-stu-id="41572-138">Before we can use hello Azure CDN Management Library, we need tooauthenticate our service principal and obtain an authentication token.</span></span>  <span data-ttu-id="41572-139">Deze methode maakt gebruik van ADAL tooretrieve Hallo-token.</span><span class="sxs-lookup"><span data-stu-id="41572-139">This method uses ADAL tooretrieve hello token.</span></span>

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

<span data-ttu-id="41572-140">Als u afzonderlijke gebruikersverificatie, Hallo `GetAccessToken` methode er iets anders.</span><span class="sxs-lookup"><span data-stu-id="41572-140">If you are using individual user authentication, hello `GetAccessToken` method will look slightly different.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="41572-141">Dit voorbeeld wordt alleen gebruiken als u afzonderlijke gebruikersverificatie toohave in plaats van een service-principal kiest.</span><span class="sxs-lookup"><span data-stu-id="41572-141">Only use this code sample if you are choosing toohave individual user authentication instead of a service principal.</span></span>
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

<span data-ttu-id="41572-142">Ervoor tooreplace worden `<redirect URI>` Hello omleidings-URI die u hebt ingevoerd toen u de toepassing hello geregistreerd in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="41572-142">Be sure tooreplace `<redirect URI>` with hello redirect URI you entered when you registered hello application in Azure AD.</span></span>

## <a name="list-cdn-profiles-and-endpoints"></a><span data-ttu-id="41572-143">Lijst met CDN-profielen en -eindpunten</span><span class="sxs-lookup"><span data-stu-id="41572-143">List CDN profiles and endpoints</span></span>
<span data-ttu-id="41572-144">Nu we klaar tooperform CDN bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="41572-144">Now we're ready tooperform CDN operations.</span></span>  <span data-ttu-id="41572-145">Hello allereerst die onze webmethode is lijst alle Hallo profielen en -eindpunten in de resourcegroep en als er een overeenkomst wordt gevonden voor Hallo-profiel en -eindpunt namen opgegeven in onze constanten, maakt een notitie van die in voor later zodat we toocreate duplicaten niet proberen.</span><span class="sxs-lookup"><span data-stu-id="41572-145">hello first thing our method does is list all hello profiles and endpoints in our resource group, and if it finds a match for hello profile and endpoint names specified in our constants, makes a note of that for later so we don't try toocreate duplicates.</span></span>

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

## <a name="create-cdn-profiles-and-endpoints"></a><span data-ttu-id="41572-146">CDN-profielen en eindpunten maken</span><span class="sxs-lookup"><span data-stu-id="41572-146">Create CDN profiles and endpoints</span></span>
<span data-ttu-id="41572-147">Vervolgens maken we een profiel.</span><span class="sxs-lookup"><span data-stu-id="41572-147">Next, we'll create a profile.</span></span>

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

<span data-ttu-id="41572-148">Zodra het Hallo-profiel is gemaakt, maakt u een eindpunt.</span><span class="sxs-lookup"><span data-stu-id="41572-148">Once hello profile is created, we'll create an endpoint.</span></span>

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
> <span data-ttu-id="41572-149">Hallo in bovenstaand voorbeeld wijst Hallo eindpunt een bron met de naam *Contoso* met een hostnaam `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="41572-149">hello example above assigns hello endpoint an origin named *Contoso* with a hostname `www.contoso.com`.</span></span>  <span data-ttu-id="41572-150">U moet deze toopoint tooyour eigen van de hostnaam van oorsprong wijzigen.</span><span class="sxs-lookup"><span data-stu-id="41572-150">You should change this toopoint tooyour own origin's hostname.</span></span>
> 
> 

## <a name="purge-an-endpoint"></a><span data-ttu-id="41572-151">Een eindpunt leegmaken</span><span class="sxs-lookup"><span data-stu-id="41572-151">Purge an endpoint</span></span>
<span data-ttu-id="41572-152">Ervan uitgaande dat Hallo-eindpunt is gemaakt, is één algemene taak dat we tooperform in onze programma willen mogelijk opschonen Hallo inhoud in onze eindpunt.</span><span class="sxs-lookup"><span data-stu-id="41572-152">Assuming hello endpoint has been created, one common task that we might want tooperform in our program is purging hello content in our endpoint.</span></span>

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
> <span data-ttu-id="41572-153">Hallo Hallo bovenstaande voorbeeld tekenreeks `/*` geeft aan dat ik wil toopurge alles in de hoofdmap Hallo van Hallo eindpuntpad.</span><span class="sxs-lookup"><span data-stu-id="41572-153">In hello example above, hello string `/*` denotes that I want toopurge everything in hello root of hello endpoint path.</span></span>  <span data-ttu-id="41572-154">Dit is gelijkwaardig toochecking **alle opschonen** in hello Azure portal 'verwijderen' dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="41572-154">This is equivalent toochecking **Purge All** in hello Azure portal's "purge" dialog.</span></span> <span data-ttu-id="41572-155">In Hallo `CreateCdnProfile` methode, ik heb gemaakt onze profiel als een **Azure CDN van Verizon** profiel met behulp van Hallo code `Sku = new Sku(SkuName.StandardVerizon)`, zodat dit geverifieerd worden kan.</span><span class="sxs-lookup"><span data-stu-id="41572-155">In hello `CreateCdnProfile` method, I created our profile as an **Azure CDN from Verizon** profile using hello code `Sku = new Sku(SkuName.StandardVerizon)`, so this will be successful.</span></span>  <span data-ttu-id="41572-156">Echter, **Azure CDN van Akamai** profielen bieden geen ondersteuning voor **alle opschonen**, dus als ik een profiel Akamai is voor deze zelfstudie gebruikt, ik tooinclude specifieke paden toopurge moet.</span><span class="sxs-lookup"><span data-stu-id="41572-156">However, **Azure CDN from Akamai** profiles do not support **Purge All**, so if I was using an Akamai profile for this tutorial, I would need tooinclude specific paths toopurge.</span></span>
> 
> 

## <a name="delete-cdn-profiles-and-endpoints"></a><span data-ttu-id="41572-157">CDN-profielen en eindpunten verwijderen</span><span class="sxs-lookup"><span data-stu-id="41572-157">Delete CDN profiles and endpoints</span></span>
<span data-ttu-id="41572-158">onze eindpunt en het profiel verwijderd Hallo laatste methoden.</span><span class="sxs-lookup"><span data-stu-id="41572-158">hello last methods will delete our endpoint and profile.</span></span>

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

## <a name="running-hello-program"></a><span data-ttu-id="41572-159">Hallo-programma uitvoeren</span><span class="sxs-lookup"><span data-stu-id="41572-159">Running hello program</span></span>
<span data-ttu-id="41572-160">We kunnen nu worden gecompileerd en Hallo programma uitvoeren door te klikken op Hallo **Start** knop in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="41572-160">We can now compile and run hello program by clicking hello **Start** button in Visual Studio.</span></span>

![Programma wordt uitgevoerd](./media/cdn-app-dev-net/cdn-program-running-1.png)

<span data-ttu-id="41572-162">Wanneer Hallo programma Hallo hierboven prompt bereikt, moet u kunnen tooreturn tooyour resourcegroep in hello Azure-portal en Zie dat Hallo-profiel is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="41572-162">When hello program reaches hello above prompt, you should be able tooreturn tooyour resource group in hello Azure portal and see that hello profile has been created.</span></span>

![Success!](./media/cdn-app-dev-net/cdn-success.png)

<span data-ttu-id="41572-164">We kunnen vervolgens Hallo prompts toorun Hallo rest van Hallo programma bevestigen.</span><span class="sxs-lookup"><span data-stu-id="41572-164">We can then confirm hello prompts toorun hello rest of hello program.</span></span>

![Programma uitvoeren](./media/cdn-app-dev-net/cdn-program-running-2.png)

## <a name="next-steps"></a><span data-ttu-id="41572-166">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="41572-166">Next Steps</span></span>
<span data-ttu-id="41572-167">toosee hello voltooid project van dit scenario [Hallo voorbeeld downloaden](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c).</span><span class="sxs-lookup"><span data-stu-id="41572-167">toosee hello completed project from this walkthrough, [download hello sample](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c).</span></span>

<span data-ttu-id="41572-168">toofind aanvullende documentatie over hello Azure CDN Management-bibliotheek voor .NET, weergave Hallo [-verwijzingen op MSDN](https://msdn.microsoft.com/library/mt657769.aspx).</span><span class="sxs-lookup"><span data-stu-id="41572-168">toofind additional documentation on hello Azure CDN Management Library for .NET, view hello [reference on MSDN](https://msdn.microsoft.com/library/mt657769.aspx).</span></span>

<span data-ttu-id="41572-169">Uw CDN-resources beheren met [PowerShell](cdn-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="41572-169">Manage your CDN resources with [PowerShell](cdn-manage-powershell.md).</span></span>

