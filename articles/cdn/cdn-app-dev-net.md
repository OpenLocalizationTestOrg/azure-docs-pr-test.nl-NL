---
title: Aan de slag met de Azure CDN-bibliotheek voor .NET | Microsoft Docs
description: Informatie over het schrijven van .NET-toepassingen voor het beheren van Azure CDN met Visual Studio.
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
ms.openlocfilehash: 5379586355ece98af6295236d6cbd09cb31c742b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-cdn-development"></a><span data-ttu-id="54892-103">Aan de slag met Azure CDN-ontwikkeling</span><span class="sxs-lookup"><span data-stu-id="54892-103">Get started with Azure CDN development</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="54892-104">Node.js</span><span class="sxs-lookup"><span data-stu-id="54892-104">Node.js</span></span>](cdn-app-dev-node.md)
> * [<span data-ttu-id="54892-105">.NET</span><span class="sxs-lookup"><span data-stu-id="54892-105">.NET</span></span>](cdn-app-dev-net.md)
> 
> 

<span data-ttu-id="54892-106">U kunt de [Azure CDN-bibliotheek voor .NET](https://msdn.microsoft.com/library/mt657769.aspx) te maken en beheren van CDN-profielen en eindpunten te automatiseren.</span><span class="sxs-lookup"><span data-stu-id="54892-106">You can use the [Azure CDN Library for .NET](https://msdn.microsoft.com/library/mt657769.aspx) to automate creation and management of CDN profiles and endpoints.</span></span>  <span data-ttu-id="54892-107">Deze zelfstudie helpt bij het maken van een eenvoudige .NET-consoletoepassing die u laat zien dat verschillende van de beschikbare bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="54892-107">This tutorial walks through the creation of a simple .NET console application that demonstrates several of the available operations.</span></span>  <span data-ttu-id="54892-108">Deze zelfstudie is niet bedoeld om alle aspecten van de Azure CDN-bibliotheek voor .NET in detail beschrijven.</span><span class="sxs-lookup"><span data-stu-id="54892-108">This tutorial is not intended to describe all aspects of the Azure CDN Library for .NET in detail.</span></span>

<span data-ttu-id="54892-109">Moet u Visual Studio 2015 om deze zelfstudie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="54892-109">You need Visual Studio 2015 to complete this tutorial.</span></span>  <span data-ttu-id="54892-110">[Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) is gratis te downloaden.</span><span class="sxs-lookup"><span data-stu-id="54892-110">[Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) is freely available for download.</span></span>

> [!TIP]
> <span data-ttu-id="54892-111">De [voltooid project uit deze zelfstudie](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c) is beschikbaar voor downloaden op MSDN.</span><span class="sxs-lookup"><span data-stu-id="54892-111">The [completed project from this tutorial](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c) is available for download on MSDN.</span></span>
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-nuget-packages"></a><span data-ttu-id="54892-112">Maken van uw project en Nuget-pakketten toevoegen</span><span class="sxs-lookup"><span data-stu-id="54892-112">Create your project and add Nuget packages</span></span>
<span data-ttu-id="54892-113">Nu dat we hebben een resourcegroep gemaakt voor onze CDN-profielen en toestemming van onze Azure AD-toepassing voor het beheren van CDN-profielen en eindpunten binnen die groep, kunnen we beginnen met het maken van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="54892-113">Now that we've created a resource group for our CDN profiles and given our Azure AD application permission to manage CDN profiles and endpoints within that group, we can start creating our application.</span></span>

<span data-ttu-id="54892-114">Klik in Visual Studio 2015 op **bestand**, **nieuw**, **Project...**  openen van het dialoogvenster new project.</span><span class="sxs-lookup"><span data-stu-id="54892-114">From within Visual Studio 2015, click **File**, **New**, **Project...** to open the new project dialog.</span></span>  <span data-ttu-id="54892-115">Vouw **Visual C#**, selecteer daarna **Windows** in het deelvenster aan de linkerkant.</span><span class="sxs-lookup"><span data-stu-id="54892-115">Expand **Visual C#**, then select **Windows** in the pane on the left.</span></span>  <span data-ttu-id="54892-116">Klik op **consoletoepassing** in het middelste deelvenster.</span><span class="sxs-lookup"><span data-stu-id="54892-116">Click **Console Application** in the center pane.</span></span>  <span data-ttu-id="54892-117">Uw project een naam en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="54892-117">Name your project, then click **OK**.</span></span>  

![Nieuw project](./media/cdn-app-dev-net/cdn-new-project.png)

<span data-ttu-id="54892-119">Onze project gaat een aantal Azure-bibliotheken die zijn opgenomen in de Nuget-pakketten gebruiken.</span><span class="sxs-lookup"><span data-stu-id="54892-119">Our project is going to use some Azure libraries contained in Nuget packages.</span></span>  <span data-ttu-id="54892-120">Laten we deze toevoegen aan het project.</span><span class="sxs-lookup"><span data-stu-id="54892-120">Let's add those to the project.</span></span>

1. <span data-ttu-id="54892-121">Klik op de **extra** menu **Nuget Package Manager**, klikt u vervolgens **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="54892-121">Click the **Tools** menu, **Nuget Package Manager**, then **Package Manager Console**.</span></span>
   
    ![Nuget-pakketten beheren](./media/cdn-app-dev-net/cdn-manage-nuget.png)
2. <span data-ttu-id="54892-123">Voer de volgende opdracht om te installeren in de Package Manager-Console de **Active Directory Authentication Library (ADAL)**:</span><span class="sxs-lookup"><span data-stu-id="54892-123">In the Package Manager Console, execute the following command to install the **Active Directory Authentication Library (ADAL)**:</span></span>
   
    `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory`
3. <span data-ttu-id="54892-124">Voer het volgende uit voor het installeren van de **Azure CDN bibliotheek**:</span><span class="sxs-lookup"><span data-stu-id="54892-124">Execute the following to install the **Azure CDN Management Library**:</span></span>
   
    `Install-Package Microsoft.Azure.Management.Cdn`

## <a name="directives-constants-main-method-and-helper-methods"></a><span data-ttu-id="54892-125">Richtlijnen, constanten hoofdmethode en Help-methoden</span><span class="sxs-lookup"><span data-stu-id="54892-125">Directives, constants, main method, and helper methods</span></span>
<span data-ttu-id="54892-126">Laten we de basisstructuur van ons programma geschreven worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="54892-126">Let's get the basic structure of our program written.</span></span>

1. <span data-ttu-id="54892-127">Vervang terug op het tabblad Program.cs de `using` richtlijnen aan de bovenkant door het volgende:</span><span class="sxs-lookup"><span data-stu-id="54892-127">Back in the Program.cs tab, replace the `using` directives at the top with the following:</span></span>
   
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
2. <span data-ttu-id="54892-128">We moeten sommige constanten die onze methoden gebruikt definiëren.</span><span class="sxs-lookup"><span data-stu-id="54892-128">We need to define some constants our methods will use.</span></span>  <span data-ttu-id="54892-129">In de `Program` klasse, maar voordat de `Main` methode, voeg de volgende.</span><span class="sxs-lookup"><span data-stu-id="54892-129">In the `Program` class, but before the `Main` method, add the following.</span></span>  <span data-ttu-id="54892-130">Zorg ervoor dat u de tijdelijke aanduidingen, met inbegrip van de  **&lt;punthaken&gt;**, met uw eigen waarden zo nodig.</span><span class="sxs-lookup"><span data-stu-id="54892-130">Be sure to replace the placeholders, including the **&lt;angle brackets&gt;**, with your own values as needed.</span></span>
   
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
3. <span data-ttu-id="54892-131">Ook op het klasseniveau van de deze twee variabelen definiëren.</span><span class="sxs-lookup"><span data-stu-id="54892-131">Also at the class level, define these two variables.</span></span>  <span data-ttu-id="54892-132">We gebruiken deze later om te bepalen als onze profiel en een eindpunt al bestaan.</span><span class="sxs-lookup"><span data-stu-id="54892-132">We'll use these later to determine if our profile and endpoint already exist.</span></span>
   
    ```csharp
    static bool profileAlreadyExists = false;
    static bool endpointAlreadyExists = false;
    ```
4. <span data-ttu-id="54892-133">Vervang de `Main` methode als volgt:</span><span class="sxs-lookup"><span data-stu-id="54892-133">Replace the `Main` method as follows:</span></span>
   
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
   
       Console.WriteLine("Press Enter to end program.");
       Console.ReadLine();
   }
   ```
5. <span data-ttu-id="54892-134">Enkele van onze andere methoden gaat het bericht met "Ja/Nee" vragen.</span><span class="sxs-lookup"><span data-stu-id="54892-134">Some of our other methods are going to prompt the user with "Yes/No" questions.</span></span>  <span data-ttu-id="54892-135">Voeg de volgende methode die een beetje om gemakkelijker te maken:</span><span class="sxs-lookup"><span data-stu-id="54892-135">Add the following method to make that a little easier:</span></span>
   
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

<span data-ttu-id="54892-136">Nu dat de basisstructuur van het programma is geschreven, maken we de methoden die worden aangeroepen door de `Main` methode.</span><span class="sxs-lookup"><span data-stu-id="54892-136">Now that the basic structure of our program is written, we should create the methods called by the `Main` method.</span></span>

## <a name="authentication"></a><span data-ttu-id="54892-137">Authentication</span><span class="sxs-lookup"><span data-stu-id="54892-137">Authentication</span></span>
<span data-ttu-id="54892-138">Voordat we de Beheerbibliotheek van Azure CDN gebruiken kunnen, moeten we onze service-principal te verifiëren en geen verificatietoken ophalen.</span><span class="sxs-lookup"><span data-stu-id="54892-138">Before we can use the Azure CDN Management Library, we need to authenticate our service principal and obtain an authentication token.</span></span>  <span data-ttu-id="54892-139">Deze methode maakt gebruik van ADAL voor het ophalen van het token.</span><span class="sxs-lookup"><span data-stu-id="54892-139">This method uses ADAL to retrieve the token.</span></span>

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

<span data-ttu-id="54892-140">Als u afzonderlijke gebruikersverificatie, de `GetAccessToken` methode er iets anders.</span><span class="sxs-lookup"><span data-stu-id="54892-140">If you are using individual user authentication, the `GetAccessToken` method will look slightly different.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="54892-141">Dit voorbeeld alleen gebruiken als u ervoor kiest om de verificatie van afzonderlijke gebruikers in plaats van een service-principal.</span><span class="sxs-lookup"><span data-stu-id="54892-141">Only use this code sample if you are choosing to have individual user authentication instead of a service principal.</span></span>
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

<span data-ttu-id="54892-142">Zorg ervoor dat u `<redirect URI>` met de omleidings-URI die u hebt opgegeven bij de registratie van de toepassing in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="54892-142">Be sure to replace `<redirect URI>` with the redirect URI you entered when you registered the application in Azure AD.</span></span>

## <a name="list-cdn-profiles-and-endpoints"></a><span data-ttu-id="54892-143">Lijst met CDN-profielen en -eindpunten</span><span class="sxs-lookup"><span data-stu-id="54892-143">List CDN profiles and endpoints</span></span>
<span data-ttu-id="54892-144">Nu we gaan CDN bewerkingen uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="54892-144">Now we're ready to perform CDN operations.</span></span>  <span data-ttu-id="54892-145">Het eerste wat dat onze methode doet is de lijst met alle profielen en -eindpunten in de resourcegroep en als er een overeenkomst wordt gevonden voor de namen van de profiel- en eindpunt opgegeven in onze constanten maakt een notitie van die in voor later zodat we niet proberen te maken van duplicaten.</span><span class="sxs-lookup"><span data-stu-id="54892-145">The first thing our method does is list all the profiles and endpoints in our resource group, and if it finds a match for the profile and endpoint names specified in our constants, makes a note of that for later so we don't try to create duplicates.</span></span>

```csharp
private static void ListProfilesAndEndpoints(CdnManagementClient cdn)
{
    // List all the CDN profiles in this resource group
    var profileList = cdn.Profiles.ListByResourceGroup(resourceGroupName);
    foreach (Profile p in profileList)
    {
        Console.WriteLine("CDN profile {0}", p.Name);
        if (p.Name.Equals(profileName, StringComparison.OrdinalIgnoreCase))
        {
            // Hey, that's the name of the CDN profile we want to create!
            profileAlreadyExists = true;
        }

        //List all the CDN endpoints on this CDN profile
        Console.WriteLine("Endpoints:");
        var endpointList = cdn.Endpoints.ListByProfile(p.Name, resourceGroupName);
        foreach (Endpoint e in endpointList)
        {
            Console.WriteLine("-{0} ({1})", e.Name, e.HostName);
            if (e.Name.Equals(endpointName, StringComparison.OrdinalIgnoreCase))
            {
                // The unique endpoint name already exists.
                endpointAlreadyExists = true;
            }
        }
        Console.WriteLine();
    }
}
```

## <a name="create-cdn-profiles-and-endpoints"></a><span data-ttu-id="54892-146">CDN-profielen en eindpunten maken</span><span class="sxs-lookup"><span data-stu-id="54892-146">Create CDN profiles and endpoints</span></span>
<span data-ttu-id="54892-147">Vervolgens maken we een profiel.</span><span class="sxs-lookup"><span data-stu-id="54892-147">Next, we'll create a profile.</span></span>

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

<span data-ttu-id="54892-148">Zodra het profiel is gemaakt, maakt u een eindpunt.</span><span class="sxs-lookup"><span data-stu-id="54892-148">Once the profile is created, we'll create an endpoint.</span></span>

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
> <span data-ttu-id="54892-149">Het bovenstaande voorbeeld wijst het eindpunt van een bron met de naam *Contoso* met een hostnaam `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="54892-149">The example above assigns the endpoint an origin named *Contoso* with a hostname `www.contoso.com`.</span></span>  <span data-ttu-id="54892-150">U moet dit om te verwijzen naar de hostnaam van uw eigen oorsprong wijzigen.</span><span class="sxs-lookup"><span data-stu-id="54892-150">You should change this to point to your own origin's hostname.</span></span>
> 
> 

## <a name="purge-an-endpoint"></a><span data-ttu-id="54892-151">Een eindpunt leegmaken</span><span class="sxs-lookup"><span data-stu-id="54892-151">Purge an endpoint</span></span>
<span data-ttu-id="54892-152">Ervan uitgaande dat het eindpunt is gemaakt, is één algemene taak die we wilt uitvoeren in onze programma opschonen van de inhoud van het eindpunt.</span><span class="sxs-lookup"><span data-stu-id="54892-152">Assuming the endpoint has been created, one common task that we might want to perform in our program is purging the content in our endpoint.</span></span>

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
> <span data-ttu-id="54892-153">In het bovenstaande voorbeeld wordt de tekenreeks `/*` geeft aan dat ik wil opschonen alles in de hoofdmap van het eindpuntpad.</span><span class="sxs-lookup"><span data-stu-id="54892-153">In the example above, the string `/*` denotes that I want to purge everything in the root of the endpoint path.</span></span>  <span data-ttu-id="54892-154">Dit komt overeen met het controleren van **alle opschonen** in het dialoogvenster voor de Azure portal 'verwijderen'.</span><span class="sxs-lookup"><span data-stu-id="54892-154">This is equivalent to checking **Purge All** in the Azure portal's "purge" dialog.</span></span> <span data-ttu-id="54892-155">In de `CreateCdnProfile` methode, ik heb gemaakt onze profiel als een **Azure CDN van Verizon** profiel met de code `Sku = new Sku(SkuName.StandardVerizon)`, zodat dit geverifieerd worden kan.</span><span class="sxs-lookup"><span data-stu-id="54892-155">In the `CreateCdnProfile` method, I created our profile as an **Azure CDN from Verizon** profile using the code `Sku = new Sku(SkuName.StandardVerizon)`, so this will be successful.</span></span>  <span data-ttu-id="54892-156">Echter, **Azure CDN van Akamai** profielen bieden geen ondersteuning voor **alle opschonen**, dus als ik een profiel Akamai is voor deze zelfstudie gebruikt, moet ik specifieke paden opgeven om op te schonen.</span><span class="sxs-lookup"><span data-stu-id="54892-156">However, **Azure CDN from Akamai** profiles do not support **Purge All**, so if I was using an Akamai profile for this tutorial, I would need to include specific paths to purge.</span></span>
> 
> 

## <a name="delete-cdn-profiles-and-endpoints"></a><span data-ttu-id="54892-157">CDN-profielen en eindpunten verwijderen</span><span class="sxs-lookup"><span data-stu-id="54892-157">Delete CDN profiles and endpoints</span></span>
<span data-ttu-id="54892-158">De laatste methoden verwijderd onze eindpunt en het profiel.</span><span class="sxs-lookup"><span data-stu-id="54892-158">The last methods will delete our endpoint and profile.</span></span>

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

## <a name="running-the-program"></a><span data-ttu-id="54892-159">Het programma uitvoeren</span><span class="sxs-lookup"><span data-stu-id="54892-159">Running the program</span></span>
<span data-ttu-id="54892-160">We kunnen nu worden gecompileerd en voer het programma door te klikken op de **Start** knop in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="54892-160">We can now compile and run the program by clicking the **Start** button in Visual Studio.</span></span>

![Programma wordt uitgevoerd](./media/cdn-app-dev-net/cdn-program-running-1.png)

<span data-ttu-id="54892-162">Wanneer het programma de bovenstaande prompt bereikt, moet u mogelijk zijn om te retourneren aan de resourcegroep in de Azure portal en Zie dat het profiel is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="54892-162">When the program reaches the above prompt, you should be able to return to your resource group in the Azure portal and see that the profile has been created.</span></span>

![Success!](./media/cdn-app-dev-net/cdn-success.png)

<span data-ttu-id="54892-164">We kunnen de aanwijzingen voor het uitvoeren van de rest van het programma vervolgens bevestigen.</span><span class="sxs-lookup"><span data-stu-id="54892-164">We can then confirm the prompts to run the rest of the program.</span></span>

![Programma uitvoeren](./media/cdn-app-dev-net/cdn-program-running-2.png)

## <a name="next-steps"></a><span data-ttu-id="54892-166">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="54892-166">Next Steps</span></span>
<span data-ttu-id="54892-167">Om te zien van de voltooide project van dit scenario [het voorbeeld downloaden](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c).</span><span class="sxs-lookup"><span data-stu-id="54892-167">To see the completed project from this walkthrough, [download the sample](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c).</span></span>

<span data-ttu-id="54892-168">Ga voor aanvullende documentatie over de Azure CDN Management-bibliotheek voor .NET weergeven de [-verwijzingen op MSDN](https://msdn.microsoft.com/library/mt657769.aspx).</span><span class="sxs-lookup"><span data-stu-id="54892-168">To find additional documentation on the Azure CDN Management Library for .NET, view the [reference on MSDN](https://msdn.microsoft.com/library/mt657769.aspx).</span></span>

<span data-ttu-id="54892-169">Uw CDN-resources beheren met [PowerShell](cdn-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="54892-169">Manage your CDN resources with [PowerShell](cdn-manage-powershell.md).</span></span>

