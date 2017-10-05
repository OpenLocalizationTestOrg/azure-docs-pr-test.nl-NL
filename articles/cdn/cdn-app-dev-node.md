---
title: Aan de slag met de Azure CDN-SDK voor Node.js | Microsoft Docs
description: Informatie over het schrijven van Node.js-toepassingen voor het beheren van Azure CDN.
services: cdn
documentationcenter: nodejs
author: zhangmanling
manager: erikre
editor: 
ms.assetid: c4bb6a61-de3d-4f0c-9dca-202554c43dfa
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 46ae8cd9775432d126cbde856c1fb06ea319297e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-cdn-development"></a><span data-ttu-id="8c662-103">Aan de slag met Azure CDN-ontwikkeling</span><span class="sxs-lookup"><span data-stu-id="8c662-103">Get started with Azure CDN development</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8c662-104">Node.js</span><span class="sxs-lookup"><span data-stu-id="8c662-104">Node.js</span></span>](cdn-app-dev-node.md)
> * [<span data-ttu-id="8c662-105">.NET</span><span class="sxs-lookup"><span data-stu-id="8c662-105">.NET</span></span>](cdn-app-dev-net.md)
> 
> 

<span data-ttu-id="8c662-106">U kunt de [Azure CDN-SDK voor Node.js](https://www.npmjs.com/package/azure-arm-cdn) te maken en beheren van CDN-profielen en eindpunten te automatiseren.</span><span class="sxs-lookup"><span data-stu-id="8c662-106">You can use the [Azure CDN SDK for Node.js](https://www.npmjs.com/package/azure-arm-cdn) to automate creation and management of CDN profiles and endpoints.</span></span>  <span data-ttu-id="8c662-107">Deze zelfstudie helpt bij het maken van een eenvoudige Node.js-consoletoepassing die u laat zien dat verschillende van de beschikbare bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="8c662-107">This tutorial walks through the creation of a simple Node.js console application that demonstrates several of the available operations.</span></span>  <span data-ttu-id="8c662-108">Deze zelfstudie is niet bedoeld voor alle aspecten van de Azure CDN-SDK voor Node.js in detail beschrijven.</span><span class="sxs-lookup"><span data-stu-id="8c662-108">This tutorial is not intended to describe all aspects of the Azure CDN SDK for Node.js in detail.</span></span>

<span data-ttu-id="8c662-109">Voor deze zelfstudie hebt voltooid, moet u al hebben [Node.js](http://www.nodejs.org) **4.x.x** of hoger geïnstalleerd en geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="8c662-109">To complete this tutorial, you should already have [Node.js](http://www.nodejs.org) **4.x.x** or higher installed and configured.</span></span>  <span data-ttu-id="8c662-110">U kunt een teksteditor die u wilt maken van uw Node.js-toepassing kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8c662-110">You can use any text editor you want to create your Node.js application.</span></span>  <span data-ttu-id="8c662-111">Voor het schrijven van deze zelfstudie gebruikt ik [Visual Studio Code](https://code.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="8c662-111">To write this tutorial, I used [Visual Studio Code](https://code.visualstudio.com).</span></span>  

> [!TIP]
> <span data-ttu-id="8c662-112">De [voltooid project uit deze zelfstudie](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74) is beschikbaar voor downloaden op MSDN.</span><span class="sxs-lookup"><span data-stu-id="8c662-112">The [completed project from this tutorial](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74) is available for download on MSDN.</span></span>
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-npm-dependencies"></a><span data-ttu-id="8c662-113">Maken van uw project en NPM afhankelijkheden toevoegen</span><span class="sxs-lookup"><span data-stu-id="8c662-113">Create your project and add NPM dependencies</span></span>
<span data-ttu-id="8c662-114">Nu dat we hebben een resourcegroep gemaakt voor onze CDN-profielen en toestemming van onze Azure AD-toepassing voor het beheren van CDN-profielen en eindpunten binnen die groep, kunnen we beginnen met het maken van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="8c662-114">Now that we've created a resource group for our CDN profiles and given our Azure AD application permission to manage CDN profiles and endpoints within that group, we can start creating our application.</span></span>

<span data-ttu-id="8c662-115">Maak een map voor het opslaan van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="8c662-115">Create a folder to store your application.</span></span>  <span data-ttu-id="8c662-116">Vanuit een console met de Node.js-hulpprogramma's in uw huidige pad instellen van uw huidige locatie naar deze map en het initialiseren van uw project door te voeren:</span><span class="sxs-lookup"><span data-stu-id="8c662-116">From a console with the Node.js tools in your current path, set your current location to this new folder and initialize your project by executing:</span></span>

    npm init

<span data-ttu-id="8c662-117">U wordt weergegeven een reeks vragen om uw project te initialiseren.</span><span class="sxs-lookup"><span data-stu-id="8c662-117">You will then be presented a series of questions to initialize your project.</span></span>  <span data-ttu-id="8c662-118">Voor **toegangspunt**, deze zelfstudie wordt gebruikgemaakt van *app.js*.</span><span class="sxs-lookup"><span data-stu-id="8c662-118">For **entry point**, this tutorial uses *app.js*.</span></span>  <span data-ttu-id="8c662-119">U kunt mijn andere opties in het volgende voorbeeld kunt zien.</span><span class="sxs-lookup"><span data-stu-id="8c662-119">You can see my other choices in the following example.</span></span>

![NPM init-uitvoer](./media/cdn-app-dev-node/cdn-npm-init.png)

<span data-ttu-id="8c662-121">Onze project nu is geïnitialiseerd met een *packages.json* bestand.</span><span class="sxs-lookup"><span data-stu-id="8c662-121">Our project is now initialized with a *packages.json* file.</span></span>  <span data-ttu-id="8c662-122">Onze project gaat een aantal Azure-bibliotheken die zijn opgenomen in de NPM-pakketten gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8c662-122">Our project is going to use some Azure libraries contained in NPM packages.</span></span>  <span data-ttu-id="8c662-123">We gebruiken de Azure-Client-Runtime voor Node.js (ms-rest-azure) en de Azure CDN-clientbibliotheek voor Node.js (arm-azure-cd).</span><span class="sxs-lookup"><span data-stu-id="8c662-123">We'll use the Azure Client Runtime for Node.js (ms-rest-azure) and the Azure CDN Client Library for Node.js (azure-arm-cd).</span></span>  <span data-ttu-id="8c662-124">Laten we deze toevoegen aan het project als afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="8c662-124">Let's add those to the project as dependencies.</span></span>

    npm install --save ms-rest-azure
    npm install --save azure-arm-cdn

<span data-ttu-id="8c662-125">Nadat u klaar bent met de pakketten installeren, de *package.json* bestand zijn vergelijkbaar met het volgende voorbeeld (versie getallen kunnen verschillen):</span><span class="sxs-lookup"><span data-stu-id="8c662-125">After the packages are done installing, the *package.json* file should look similar to this example (version numbers may differ):</span></span>

``` json
{
  "name": "cdn_node",
  "version": "1.0.0",
  "description": "Azure CDN Node.js tutorial project",
  "main": "app.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "Cam Soper",
  "license": "MIT",
  "dependencies": {
    "azure-arm-cdn": "^0.2.1",
    "ms-rest-azure": "^1.14.4"
  }
}
```

<span data-ttu-id="8c662-126">Ten slotte met uw teksteditor een leeg tekstbestand maken en opslaan in de hoofdmap van onze projectmap als *app.js*.</span><span class="sxs-lookup"><span data-stu-id="8c662-126">Finally, using your text editor, create a blank text file and save it in the root of our project folder as *app.js*.</span></span>  <span data-ttu-id="8c662-127">We zijn nu gereed om te beginnen met het schrijven van code.</span><span class="sxs-lookup"><span data-stu-id="8c662-127">We're now ready to begin writing code.</span></span>

## <a name="requires-constants-authentication-and-structure"></a><span data-ttu-id="8c662-128">Vereist, constanten, verificatie en -structuur</span><span class="sxs-lookup"><span data-stu-id="8c662-128">Requires, constants, authentication, and structure</span></span>
<span data-ttu-id="8c662-129">Met *app.js* openen in onze editor, gaan we aan de basisstructuur van onze programma dat is geschreven.</span><span class="sxs-lookup"><span data-stu-id="8c662-129">With *app.js* open in our editor, let's get the basic structure of our program written.</span></span>

1. <span data-ttu-id="8c662-130">Voeg de 'vereist' voor onze NPM pakketten aan de bovenkant met de volgende opties:</span><span class="sxs-lookup"><span data-stu-id="8c662-130">Add the "requires" for our NPM packages at the top with the following:</span></span>
   
    ``` javascript
    var msRestAzure = require('ms-rest-azure');
    var cdnManagementClient = require('azure-arm-cdn');
    ```
2. <span data-ttu-id="8c662-131">We moeten sommige constanten die onze methoden gebruikt definiëren.</span><span class="sxs-lookup"><span data-stu-id="8c662-131">We need to define some constants our methods will use.</span></span>  <span data-ttu-id="8c662-132">Voeg het volgende toe.</span><span class="sxs-lookup"><span data-stu-id="8c662-132">Add the following.</span></span>  <span data-ttu-id="8c662-133">Zorg ervoor dat u de tijdelijke aanduidingen, met inbegrip van de  **&lt;punthaken&gt;**, met uw eigen waarden zo nodig.</span><span class="sxs-lookup"><span data-stu-id="8c662-133">Be sure to replace the placeholders, including the **&lt;angle brackets&gt;**, with your own values as needed.</span></span>
   
    ``` javascript
    //Tenant app constants
    const clientId = "<YOUR CLIENT ID>";
    const clientSecret = "<YOUR CLIENT AUTHENTICATION KEY>"; //Only for service principals
    const tenantId = "<YOUR TENANT ID>";
   
    //Application constants
    const subscriptionId = "<YOUR SUBSCRIPTION ID>";
    const resourceGroupName = "CdnConsoleTutorial";
    const resourceLocation = "<YOUR PREFERRED AZURE LOCATION, SUCH AS Central US>";
    ```
3. <span data-ttu-id="8c662-134">Vervolgens we exemplaar maken van de CDN-management-client en wijs hieraan onze referenties.</span><span class="sxs-lookup"><span data-stu-id="8c662-134">Next, we'll instantiate the CDN management client and give it our credentials.</span></span>
   
    ``` javascript
    var credentials = new msRestAzure.ApplicationTokenCredentials(clientId, tenantId, clientSecret);
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    <span data-ttu-id="8c662-135">Als u afzonderlijke gebruikersverificatie gebruikt, is deze twee regels er iets anders.</span><span class="sxs-lookup"><span data-stu-id="8c662-135">If you are using individual user authentication, these two lines will look slightly different.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="8c662-136">Dit voorbeeld alleen gebruiken als u ervoor kiest om de verificatie van afzonderlijke gebruikers in plaats van een service-principal.</span><span class="sxs-lookup"><span data-stu-id="8c662-136">Only use this code sample if you are choosing to have individual user authentication instead of a service principal.</span></span>  <span data-ttu-id="8c662-137">Zorg ervoor dat uw afzonderlijke gebruikersreferenties bewaken en geheime houden.</span><span class="sxs-lookup"><span data-stu-id="8c662-137">Be careful to guard your individual user credentials and keep them secret.</span></span>
   > 
   > 
   
    ``` javascript
    var credentials = new msRestAzure.UserTokenCredentials(clientId, 
        tenantId, '<username>', '<password>', '<redirect URI>');
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    <span data-ttu-id="8c662-138">Zorg ervoor dat u de items in  **&lt;punthaken&gt;**  met de juiste gegevens.</span><span class="sxs-lookup"><span data-stu-id="8c662-138">Be sure to replace the items in **&lt;angle brackets&gt;** with the correct information.</span></span>  <span data-ttu-id="8c662-139">Voor `<redirect URI>`, gebruikt u de omleidings-URI die u hebt opgegeven bij de registratie van de toepassing in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8c662-139">For `<redirect URI>`, use the redirect URI you entered when you registered the application in Azure AD.</span></span>
4. <span data-ttu-id="8c662-140">Onze Node.js-consoletoepassing zal duren voordat sommige opdrachtregelparameters.</span><span class="sxs-lookup"><span data-stu-id="8c662-140">Our Node.js console application is going to take some command-line parameters.</span></span>  <span data-ttu-id="8c662-141">Laten we valideren ten minste één parameter is doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="8c662-141">Let's validate that at least one parameter was passed.</span></span>
   
   ```javascript
   //Collect command-line parameters
   var parms = process.argv.slice(2);
   
   //Do we have parameters?
   if(parms == null || parms.length == 0)
   {
       console.log("Not enough parameters!");
       console.log("Valid commands are list, delete, create, and purge.");
       process.exit(1);
   }
   ```
5. <span data-ttu-id="8c662-142">Ons heeft die in het hoofdgedeelte van het programma, waar we vertakking uit naar andere functies op basis van welke parameters zijn doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="8c662-142">That brings us to the main part of our program, where we branch off to other functions based on what parameters were passed.</span></span>
   
    ```javascript
    switch(parms[0].toLowerCase())
    {
        case "list":
            cdnList();
            break;
   
        case "create":
            cdnCreate();
            break;
   
        case "delete":
            cdnDelete();
            break;
   
        case "purge":
            cdnPurge();
            break;
   
        default:
            console.log("Valid commands are list, delete, create, and purge.");
            process.exit(1);
    }
    ```
6. <span data-ttu-id="8c662-143">Op verschillende plaatsen in onze programma moet u om te controleren of het juiste aantal parameters zijn doorgegeven en hulp weergegeven als ze niet juist zoeken.</span><span class="sxs-lookup"><span data-stu-id="8c662-143">At several places in our program, we'll need to make sure the right number of parameters were passed in and display some help if they don't look correct.</span></span>  <span data-ttu-id="8c662-144">Laten we functies hiertoe maken.</span><span class="sxs-lookup"><span data-stu-id="8c662-144">Let's create functions to do that.</span></span>
   
   ```javascript
   function requireParms(parmCount) {
       if(parms.length < parmCount) {
           usageHelp(parms[0].toLowerCase());
           process.exit(1);
       }
   }
   
   function usageHelp(cmd) {
       console.log("Usage for " + cmd + ":");
       switch(cmd)
       {
           case "list":
               console.log("list profiles");
               console.log("list endpoints <profile name>");
               break;
   
           case "create":
               console.log("create profile <profile name>");
               console.log("create endpoint <profile name> <endpoint name> <origin hostname>");
               break;
   
           case "delete":
               console.log("delete profile <profile name>");
               console.log("delete endpoint <profile name> <endpoint name>");
               break;
   
           case "purge":
               console.log("purge <profile name> <endpoint name> <path>");
               break;
   
           default:
               console.log("Invalid command.");
       }
   }
   ```
7. <span data-ttu-id="8c662-145">Tot slot worden de functies die worden gebruikt op de CDN-management-client zijn asynchroon, daarom ze een methode aan te roepen moeten wanneer ze klaar.</span><span class="sxs-lookup"><span data-stu-id="8c662-145">Finally, the functions we'll be using on the CDN management client are asynchronous, so they need a method to call back when they're done.</span></span>  <span data-ttu-id="8c662-146">Zorg dat u kunt de uitvoer van de CDN management-client (indien aanwezig) weergeven en het programma afgesloten.</span><span class="sxs-lookup"><span data-stu-id="8c662-146">Let's make one that can display the output from the CDN management client (if any) and exit the program gracefully.</span></span>
   
    ```javascript
    function callback(err, result, request, response) {
        if (err) {
            console.log(err);
            process.exit(1);
        } else {
            console.log((result == null) ? "Done!" : result);
            process.exit(0);
        }
    }
    ```

<span data-ttu-id="8c662-147">Nu dat de basisstructuur van het programma is geschreven, maken we de functies die worden aangeroepen op basis van onze parameters.</span><span class="sxs-lookup"><span data-stu-id="8c662-147">Now that the basic structure of our program is written, we should create the functions called based on our parameters.</span></span>

## <a name="list-cdn-profiles-and-endpoints"></a><span data-ttu-id="8c662-148">Lijst met CDN-profielen en -eindpunten</span><span class="sxs-lookup"><span data-stu-id="8c662-148">List CDN profiles and endpoints</span></span>
<span data-ttu-id="8c662-149">U begint met de code voor een lijst met onze bestaande profielen en -eindpunten.</span><span class="sxs-lookup"><span data-stu-id="8c662-149">Let's start with code to list our existing profiles and endpoints.</span></span>  <span data-ttu-id="8c662-150">Mijn codeopmerkingen beschikt u over de syntaxis van de verwachte zodat we weten waar elke parameter gaat.</span><span class="sxs-lookup"><span data-stu-id="8c662-150">My code comments provide the expected syntax so we know where each parameter goes.</span></span>

```javascript
// list profiles
// list endpoints <profile name>
function cdnList(){
    requireParms(2);
    switch(parms[1].toLowerCase())
    {
        case "profiles":
            console.log("Listing profiles...");
            cdnClient.profiles.listByResourceGroup(resourceGroupName, callback);
            break;

        case "endpoints":
            requireParms(3);
            console.log("Listing endpoints...");
            cdnClient.endpoints.listByProfile(parms[2], resourceGroupName, callback);
            break;

        default:
            console.log("Invalid parameter.");
            process.exit(1);
    }
}
```

## <a name="create-cdn-profiles-and-endpoints"></a><span data-ttu-id="8c662-151">CDN-profielen en eindpunten maken</span><span class="sxs-lookup"><span data-stu-id="8c662-151">Create CDN profiles and endpoints</span></span>
<span data-ttu-id="8c662-152">We schrijft vervolgens de functies voor het maken van profielen en -eindpunten.</span><span class="sxs-lookup"><span data-stu-id="8c662-152">Next, we'll write the functions to create profiles and endpoints.</span></span>

```javascript
function cdnCreate() {
    requireParms(2);
    switch(parms[1].toLowerCase())
    {
        case "profile":
            cdnCreateProfile();
            break;

        case "endpoint":
            cdnCreateEndpoint();
            break;

        default:
            console.log("Invalid parameter.");
            process.exit(1);
    }
}

// create profile <profile name>
function cdnCreateProfile() {
    requireParms(3);
    console.log("Creating profile...");
    var standardCreateParameters = {
        location: resourceLocation,
        sku: {
            name: 'Standard_Verizon'
        }
    };

    cdnClient.profiles.create(parms[2], standardCreateParameters, resourceGroupName, callback);
}

// create endpoint <profile name> <endpoint name> <origin hostname>        
function cdnCreateEndpoint() {
    requireParms(5);
    console.log("Creating endpoint...");
    var endpointProperties = {
        location: resourceLocation,
        origins: [{
            name: parms[4],
            hostName: parms[4]
        }]
    };

    cdnClient.endpoints.create(parms[3], endpointProperties, parms[2], resourceGroupName, callback);
}
```

## <a name="purge-an-endpoint"></a><span data-ttu-id="8c662-153">Een eindpunt leegmaken</span><span class="sxs-lookup"><span data-stu-id="8c662-153">Purge an endpoint</span></span>
<span data-ttu-id="8c662-154">Ervan uitgaande dat het eindpunt is gemaakt, is een algemene taak die we wilt uitvoeren in onze programma inhoud in onze eindpunt opschonen.</span><span class="sxs-lookup"><span data-stu-id="8c662-154">Assuming the endpoint has been created, one common task that we might want to perform in our program is purging content in our endpoint.</span></span>

```javascript
// purge <profile name> <endpoint name> <path>
function cdnPurge() {
    requireParms(4);
    console.log("Purging endpoint...");
    var purgeContentPaths = [ parms[3] ];
    cdnClient.endpoints.purgeContent(parms[2], parms[1], resourceGroupName, purgeContentPaths, callback);
}
```

## <a name="delete-cdn-profiles-and-endpoints"></a><span data-ttu-id="8c662-155">CDN-profielen en eindpunten verwijderen</span><span class="sxs-lookup"><span data-stu-id="8c662-155">Delete CDN profiles and endpoints</span></span>
<span data-ttu-id="8c662-156">De laatste functie opgeroepen we nemen verwijdert eindpunten en -profielen.</span><span class="sxs-lookup"><span data-stu-id="8c662-156">The last function we will include deletes endpoints and profiles.</span></span>

```javascript
function cdnDelete() {
    requireParms(2);
    switch(parms[1].toLowerCase())
    {
        // delete profile <profile name>
        case "profile":
            requireParms(3);
            console.log("Deleting profile...");
            cdnClient.profiles.deleteIfExists(parms[2], resourceGroupName, callback);
            break;

        // delete endpoint <profile name> <endpoint name>
        case "endpoint":
            requireParms(4);
            console.log("Deleting endpoint...");
            cdnClient.endpoints.deleteIfExists(parms[3], parms[2], resourceGroupName, callback);
            break;

        default:
            console.log("Invalid parameter.");
            process.exit(1);
    }
}
```

## <a name="running-the-program"></a><span data-ttu-id="8c662-157">Het programma uitvoeren</span><span class="sxs-lookup"><span data-stu-id="8c662-157">Running the program</span></span>
<span data-ttu-id="8c662-158">We ons gebruik van onze favoriete debugger Node.js-programma kan nu worden uitgevoerd of bij de console.</span><span class="sxs-lookup"><span data-stu-id="8c662-158">We can now execute our Node.js program using our favorite debugger or at the console.</span></span>

> [!TIP]
> <span data-ttu-id="8c662-159">Als u Visual Studio Code als uw debugger gebruikt, moet u uw omgeving instellen om op te geven de opdrachtregelparameters.</span><span class="sxs-lookup"><span data-stu-id="8c662-159">If you're using Visual Studio Code as your debugger, you'll need to set up your environment to pass in the command-line parameters.</span></span>  <span data-ttu-id="8c662-160">Visual Studio Code doet dit de **lanuch.json** bestand.</span><span class="sxs-lookup"><span data-stu-id="8c662-160">Visual Studio Code does this in the **lanuch.json** file.</span></span>  <span data-ttu-id="8c662-161">Zoeken naar een eigenschap met de naam **args** en toevoegen van een matrix van tekenreekswaarden voor uw-parameters, zodat het er ongeveer als volgt uitziet: `"args": ["list", "profiles"]`.</span><span class="sxs-lookup"><span data-stu-id="8c662-161">Look for a property named **args** and add an array of string values for your parameters, so that it looks similar to this:  `"args": ["list", "profiles"]`.</span></span>
> 
> 

<span data-ttu-id="8c662-162">Laten we beginnen met een overzicht van onze profielen.</span><span class="sxs-lookup"><span data-stu-id="8c662-162">Let's start by listing our profiles.</span></span>

![Lijst met profielen](./media/cdn-app-dev-node/cdn-list-profiles.png)

<span data-ttu-id="8c662-164">Wij terug lege matrix.</span><span class="sxs-lookup"><span data-stu-id="8c662-164">We got back an empty array.</span></span>  <span data-ttu-id="8c662-165">Aangezien er zijn momenteel geen profielen in de resourcegroep, waarvan wordt verwacht.</span><span class="sxs-lookup"><span data-stu-id="8c662-165">Since we don't have any profiles in our resource group, that's expected.</span></span>  <span data-ttu-id="8c662-166">We gaan nu een profiel maken.</span><span class="sxs-lookup"><span data-stu-id="8c662-166">Let's create a profile now.</span></span>

![Profiel maken](./media/cdn-app-dev-node/cdn-create-profile.png)

<span data-ttu-id="8c662-168">Nu gaan we een eindpunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="8c662-168">Now, let's add an endpoint.</span></span>

![Eindpunt maken](./media/cdn-app-dev-node/cdn-create-endpoint.png)

<span data-ttu-id="8c662-170">Tot slot gaan we onze profiel verwijderen.</span><span class="sxs-lookup"><span data-stu-id="8c662-170">Finally, let's delete our profile.</span></span>

![Profiel verwijderen](./media/cdn-app-dev-node/cdn-delete-profile.png)

## <a name="next-steps"></a><span data-ttu-id="8c662-172">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8c662-172">Next Steps</span></span>
<span data-ttu-id="8c662-173">Om te zien van de voltooide project van dit scenario [het voorbeeld downloaden](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74).</span><span class="sxs-lookup"><span data-stu-id="8c662-173">To see the completed project from this walkthrough, [download the sample](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74).</span></span>

<span data-ttu-id="8c662-174">Geef weer voor de verwijzing voor de Azure CDN-SDK voor Node.js de [verwijzing](http://azure.github.io/azure-sdk-for-node/azure-arm-cdn/latest/).</span><span class="sxs-lookup"><span data-stu-id="8c662-174">To see the reference for the Azure CDN SDK for Node.js, view the [reference](http://azure.github.io/azure-sdk-for-node/azure-arm-cdn/latest/).</span></span>

<span data-ttu-id="8c662-175">Aanvullende documentatie over de Azure SDK voor Node.js vindt geven de [volledige verwijzing](http://azure.github.io/azure-sdk-for-node/).</span><span class="sxs-lookup"><span data-stu-id="8c662-175">To find additional documentation on the Azure SDK for Node.js, view the [full reference](http://azure.github.io/azure-sdk-for-node/).</span></span>

<span data-ttu-id="8c662-176">Uw CDN-resources beheren met [PowerShell](cdn-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="8c662-176">Manage your CDN resources with [PowerShell](cdn-manage-powershell.md).</span></span>

