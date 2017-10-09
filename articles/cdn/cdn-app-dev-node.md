---
title: aaaGet gestart Hello Azure CDN-SDK voor Node.js | Microsoft Docs
description: Meer informatie over hoe toowrite Node.js-toepassingen toomanage Azure CDN.
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
ms.openlocfilehash: 6c805e5fb8e0b471e8b248cb2f4b29efd6c85940
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-cdn-development"></a><span data-ttu-id="e02a4-103">Aan de slag met Azure CDN-ontwikkeling</span><span class="sxs-lookup"><span data-stu-id="e02a4-103">Get started with Azure CDN development</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e02a4-104">Node.js</span><span class="sxs-lookup"><span data-stu-id="e02a4-104">Node.js</span></span>](cdn-app-dev-node.md)
> * [<span data-ttu-id="e02a4-105">.NET</span><span class="sxs-lookup"><span data-stu-id="e02a4-105">.NET</span></span>](cdn-app-dev-net.md)
> 
> 

<span data-ttu-id="e02a4-106">U kunt Hallo [Azure CDN-SDK voor Node.js](https://www.npmjs.com/package/azure-arm-cdn) tooautomate maken en beheren van CDN-profielen en eindpunten.</span><span class="sxs-lookup"><span data-stu-id="e02a4-106">You can use hello [Azure CDN SDK for Node.js](https://www.npmjs.com/package/azure-arm-cdn) tooautomate creation and management of CDN profiles and endpoints.</span></span>  <span data-ttu-id="e02a4-107">Deze zelfstudie wordt begeleid Hallo maken van een eenvoudige Node.js-consoletoepassing die u laat zien dat verschillende Hallo beschikbare bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="e02a4-107">This tutorial walks through hello creation of a simple Node.js console application that demonstrates several of hello available operations.</span></span>  <span data-ttu-id="e02a4-108">Deze zelfstudie is niet bedoeld toodescribe alle aspecten van hello Azure CDN-SDK voor Node.js in detail.</span><span class="sxs-lookup"><span data-stu-id="e02a4-108">This tutorial is not intended toodescribe all aspects of hello Azure CDN SDK for Node.js in detail.</span></span>

<span data-ttu-id="e02a4-109">toocomplete deze zelfstudie hebt u al hebt [Node.js](http://www.nodejs.org) **4.x.x** of hoger geïnstalleerd en geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="e02a4-109">toocomplete this tutorial, you should already have [Node.js](http://www.nodejs.org) **4.x.x** or higher installed and configured.</span></span>  <span data-ttu-id="e02a4-110">U kunt elke gewenste toocreate uw Node.js-toepassing teksteditor gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e02a4-110">You can use any text editor you want toocreate your Node.js application.</span></span>  <span data-ttu-id="e02a4-111">toowrite in deze zelfstudie gebruikt ik [Visual Studio Code](https://code.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="e02a4-111">toowrite this tutorial, I used [Visual Studio Code](https://code.visualstudio.com).</span></span>  

> [!TIP]
> <span data-ttu-id="e02a4-112">Hallo [voltooid project uit deze zelfstudie](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74) is beschikbaar voor downloaden op MSDN.</span><span class="sxs-lookup"><span data-stu-id="e02a4-112">hello [completed project from this tutorial](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74) is available for download on MSDN.</span></span>
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-npm-dependencies"></a><span data-ttu-id="e02a4-113">Maken van uw project en NPM afhankelijkheden toevoegen</span><span class="sxs-lookup"><span data-stu-id="e02a4-113">Create your project and add NPM dependencies</span></span>
<span data-ttu-id="e02a4-114">Nu dat we hebben een resourcegroep gemaakt voor onze CDN-profielen en bepaalde onze Azure AD-toepassing machtiging toomanage CDN-profielen en de eindpunten in die groep, kunnen we beginnen met het maken van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="e02a4-114">Now that we've created a resource group for our CDN profiles and given our Azure AD application permission toomanage CDN profiles and endpoints within that group, we can start creating our application.</span></span>

<span data-ttu-id="e02a4-115">Maak een map toostore uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="e02a4-115">Create a folder toostore your application.</span></span>  <span data-ttu-id="e02a4-116">Vanuit een console met de Hallo Node.js-hulpprogramma's in uw huidige pad, stelt u uw huidige locatie toothis nieuwe map en initialiseren van het project door te voeren:</span><span class="sxs-lookup"><span data-stu-id="e02a4-116">From a console with hello Node.js tools in your current path, set your current location toothis new folder and initialize your project by executing:</span></span>

    npm init

<span data-ttu-id="e02a4-117">U een reeks vragen tooinitialize aangeboden uw project.</span><span class="sxs-lookup"><span data-stu-id="e02a4-117">You will then be presented a series of questions tooinitialize your project.</span></span>  <span data-ttu-id="e02a4-118">Voor **toegangspunt**, deze zelfstudie wordt gebruikgemaakt van *app.js*.</span><span class="sxs-lookup"><span data-stu-id="e02a4-118">For **entry point**, this tutorial uses *app.js*.</span></span>  <span data-ttu-id="e02a4-119">U kunt mijn andere opties in het volgende voorbeeld Hallo zien.</span><span class="sxs-lookup"><span data-stu-id="e02a4-119">You can see my other choices in hello following example.</span></span>

![NPM init-uitvoer](./media/cdn-app-dev-node/cdn-npm-init.png)

<span data-ttu-id="e02a4-121">Onze project nu is geïnitialiseerd met een *packages.json* bestand.</span><span class="sxs-lookup"><span data-stu-id="e02a4-121">Our project is now initialized with a *packages.json* file.</span></span>  <span data-ttu-id="e02a4-122">Onze project gaat toouse sommige Azure-bibliotheken die zijn opgenomen in de NPM-pakketten.</span><span class="sxs-lookup"><span data-stu-id="e02a4-122">Our project is going toouse some Azure libraries contained in NPM packages.</span></span>  <span data-ttu-id="e02a4-123">We gebruiken hello Azure Client Runtime voor Node.js (ms-rest-azure) en hello Azure CDN-clientbibliotheek voor Node.js (arm-azure-cd).</span><span class="sxs-lookup"><span data-stu-id="e02a4-123">We'll use hello Azure Client Runtime for Node.js (ms-rest-azure) and hello Azure CDN Client Library for Node.js (azure-arm-cd).</span></span>  <span data-ttu-id="e02a4-124">Laten we deze toohello-project toevoegen als afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="e02a4-124">Let's add those toohello project as dependencies.</span></span>

    npm install --save ms-rest-azure
    npm install --save azure-arm-cdn

<span data-ttu-id="e02a4-125">Na hello-pakketten zijn gedaan installeert, hello *package.json* bestand ziet er vergelijkbaar toothis voorbeeld (versie getallen kunnen verschillen):</span><span class="sxs-lookup"><span data-stu-id="e02a4-125">After hello packages are done installing, hello *package.json* file should look similar toothis example (version numbers may differ):</span></span>

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

<span data-ttu-id="e02a4-126">Ten slotte met uw teksteditor een leeg tekstbestand maken en opslaan in de hoofdmap Hallo van onze projectmap als *app.js*.</span><span class="sxs-lookup"><span data-stu-id="e02a4-126">Finally, using your text editor, create a blank text file and save it in hello root of our project folder as *app.js*.</span></span>  <span data-ttu-id="e02a4-127">We zijn nu gereed toobegin schrijven van code.</span><span class="sxs-lookup"><span data-stu-id="e02a4-127">We're now ready toobegin writing code.</span></span>

## <a name="requires-constants-authentication-and-structure"></a><span data-ttu-id="e02a4-128">Vereist, constanten, verificatie en -structuur</span><span class="sxs-lookup"><span data-stu-id="e02a4-128">Requires, constants, authentication, and structure</span></span>
<span data-ttu-id="e02a4-129">Met *app.js* openen in onze editor, gaan we aan Hallo basisstructuur van onze programma geschreven.</span><span class="sxs-lookup"><span data-stu-id="e02a4-129">With *app.js* open in our editor, let's get hello basic structure of our program written.</span></span>

1. <span data-ttu-id="e02a4-130">Voeg Hallo 'vereist' voor onze pakketten NPM boven Hallo Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="e02a4-130">Add hello "requires" for our NPM packages at hello top with hello following:</span></span>
   
    ``` javascript
    var msRestAzure = require('ms-rest-azure');
    var cdnManagementClient = require('azure-arm-cdn');
    ```
2. <span data-ttu-id="e02a4-131">We moeten toodefine sommige constanten die onze methoden gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e02a4-131">We need toodefine some constants our methods will use.</span></span>  <span data-ttu-id="e02a4-132">Voeg de volgende Hallo toe.</span><span class="sxs-lookup"><span data-stu-id="e02a4-132">Add hello following.</span></span>  <span data-ttu-id="e02a4-133">Worden ervoor tooreplace Hallo tijdelijke aanduidingen, met inbegrip van Hallo  **&lt;punthaken&gt;**, met uw eigen waarden zo nodig.</span><span class="sxs-lookup"><span data-stu-id="e02a4-133">Be sure tooreplace hello placeholders, including hello **&lt;angle brackets&gt;**, with your own values as needed.</span></span>
   
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
3. <span data-ttu-id="e02a4-134">Vervolgens we instantiëren Hallo CDN management-client en wijs hieraan onze referenties.</span><span class="sxs-lookup"><span data-stu-id="e02a4-134">Next, we'll instantiate hello CDN management client and give it our credentials.</span></span>
   
    ``` javascript
    var credentials = new msRestAzure.ApplicationTokenCredentials(clientId, tenantId, clientSecret);
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    <span data-ttu-id="e02a4-135">Als u afzonderlijke gebruikersverificatie gebruikt, is deze twee regels er iets anders.</span><span class="sxs-lookup"><span data-stu-id="e02a4-135">If you are using individual user authentication, these two lines will look slightly different.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="e02a4-136">Dit voorbeeld wordt alleen gebruiken als u afzonderlijke gebruikersverificatie toohave in plaats van een service-principal kiest.</span><span class="sxs-lookup"><span data-stu-id="e02a4-136">Only use this code sample if you are choosing toohave individual user authentication instead of a service principal.</span></span>  <span data-ttu-id="e02a4-137">Zorgvuldige tooguard uw afzonderlijke gebruikersreferenties en bewaar deze geheime.</span><span class="sxs-lookup"><span data-stu-id="e02a4-137">Be careful tooguard your individual user credentials and keep them secret.</span></span>
   > 
   > 
   
    ``` javascript
    var credentials = new msRestAzure.UserTokenCredentials(clientId, 
        tenantId, '<username>', '<password>', '<redirect URI>');
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    <span data-ttu-id="e02a4-138">Worden ervoor tooreplace Hallo-items in  **&lt;punthaken&gt;**  met Hallo de juiste informatie.</span><span class="sxs-lookup"><span data-stu-id="e02a4-138">Be sure tooreplace hello items in **&lt;angle brackets&gt;** with hello correct information.</span></span>  <span data-ttu-id="e02a4-139">Voor `<redirect URI>`, Hallo omleidings-URI die u hebt ingevoerd toen u de toepassing hello geregistreerd in Azure AD gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e02a4-139">For `<redirect URI>`, use hello redirect URI you entered when you registered hello application in Azure AD.</span></span>
4. <span data-ttu-id="e02a4-140">Onze Node.js-consoletoepassing gaat tootake sommige parameters voor de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="e02a4-140">Our Node.js console application is going tootake some command-line parameters.</span></span>  <span data-ttu-id="e02a4-141">Laten we valideren ten minste één parameter is doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="e02a4-141">Let's validate that at least one parameter was passed.</span></span>
   
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
5. <span data-ttu-id="e02a4-142">Die brengt ons toohello hoofdgedeelte van het programma, waar we vertakking uit tooother functies op basis van welke parameters zijn doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="e02a4-142">That brings us toohello main part of our program, where we branch off tooother functions based on what parameters were passed.</span></span>
   
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
6. <span data-ttu-id="e02a4-143">Op verschillende plaatsen in onze programma moeten we ervoor Hallo kunt u het juiste aantal parameters zijn doorgegeven en hulp weergegeven als ze niet zo juiste uitzien toomake.</span><span class="sxs-lookup"><span data-stu-id="e02a4-143">At several places in our program, we'll need toomake sure hello right number of parameters were passed in and display some help if they don't look correct.</span></span>  <span data-ttu-id="e02a4-144">We maken functies toodo die.</span><span class="sxs-lookup"><span data-stu-id="e02a4-144">Let's create functions toodo that.</span></span>
   
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
7. <span data-ttu-id="e02a4-145">Hallo-functies die worden gebruikt op Hallo CDN management-client zijn ten slotte asynchroon, zodat zij nodig hebben een toocall methode terug wanneer ze klaar bent.</span><span class="sxs-lookup"><span data-stu-id="e02a4-145">Finally, hello functions we'll be using on hello CDN management client are asynchronous, so they need a method toocall back when they're done.</span></span>  <span data-ttu-id="e02a4-146">We maken die kan Hallo-uitvoer van Hallo CDN management-client (indien aanwezig) weergeven en Hallo programma afgesloten.</span><span class="sxs-lookup"><span data-stu-id="e02a4-146">Let's make one that can display hello output from hello CDN management client (if any) and exit hello program gracefully.</span></span>
   
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

<span data-ttu-id="e02a4-147">Nu dat de basisstructuur Hallo van het programma is geschreven, maken we Hallo functies die worden aangeroepen op basis van onze parameters.</span><span class="sxs-lookup"><span data-stu-id="e02a4-147">Now that hello basic structure of our program is written, we should create hello functions called based on our parameters.</span></span>

## <a name="list-cdn-profiles-and-endpoints"></a><span data-ttu-id="e02a4-148">Lijst met CDN-profielen en -eindpunten</span><span class="sxs-lookup"><span data-stu-id="e02a4-148">List CDN profiles and endpoints</span></span>
<span data-ttu-id="e02a4-149">We beginnen met code toolist onze bestaande profielen en -eindpunten.</span><span class="sxs-lookup"><span data-stu-id="e02a4-149">Let's start with code toolist our existing profiles and endpoints.</span></span>  <span data-ttu-id="e02a4-150">Mijn codeopmerkingen bieden Hallo verwacht syntaxis zodat we weten waar elke parameter gaat.</span><span class="sxs-lookup"><span data-stu-id="e02a4-150">My code comments provide hello expected syntax so we know where each parameter goes.</span></span>

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

## <a name="create-cdn-profiles-and-endpoints"></a><span data-ttu-id="e02a4-151">CDN-profielen en eindpunten maken</span><span class="sxs-lookup"><span data-stu-id="e02a4-151">Create CDN profiles and endpoints</span></span>
<span data-ttu-id="e02a4-152">We schrijft vervolgens Hallo functies toocreate profielen en -eindpunten.</span><span class="sxs-lookup"><span data-stu-id="e02a4-152">Next, we'll write hello functions toocreate profiles and endpoints.</span></span>

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

## <a name="purge-an-endpoint"></a><span data-ttu-id="e02a4-153">Een eindpunt leegmaken</span><span class="sxs-lookup"><span data-stu-id="e02a4-153">Purge an endpoint</span></span>
<span data-ttu-id="e02a4-154">Ervan uitgaande dat Hallo-eindpunt is gemaakt, is één algemene taak dat we tooperform in onze programma willen mogelijk opschonen van inhoud in onze eindpunt.</span><span class="sxs-lookup"><span data-stu-id="e02a4-154">Assuming hello endpoint has been created, one common task that we might want tooperform in our program is purging content in our endpoint.</span></span>

```javascript
// purge <profile name> <endpoint name> <path>
function cdnPurge() {
    requireParms(4);
    console.log("Purging endpoint...");
    var purgeContentPaths = [ parms[3] ];
    cdnClient.endpoints.purgeContent(parms[2], parms[1], resourceGroupName, purgeContentPaths, callback);
}
```

## <a name="delete-cdn-profiles-and-endpoints"></a><span data-ttu-id="e02a4-155">CDN-profielen en eindpunten verwijderen</span><span class="sxs-lookup"><span data-stu-id="e02a4-155">Delete CDN profiles and endpoints</span></span>
<span data-ttu-id="e02a4-156">de laatste functie Hallo we nemen verwijdert eindpunten en -profielen.</span><span class="sxs-lookup"><span data-stu-id="e02a4-156">hello last function we will include deletes endpoints and profiles.</span></span>

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

## <a name="running-hello-program"></a><span data-ttu-id="e02a4-157">Hallo-programma uitvoeren</span><span class="sxs-lookup"><span data-stu-id="e02a4-157">Running hello program</span></span>
<span data-ttu-id="e02a4-158">We ons gebruik van onze favoriete debugger Node.js-programma kan nu worden uitgevoerd of op Hallo-beheerconsole.</span><span class="sxs-lookup"><span data-stu-id="e02a4-158">We can now execute our Node.js program using our favorite debugger or at hello console.</span></span>

> [!TIP]
> <span data-ttu-id="e02a4-159">Als u Visual Studio Code als het foutopsporingsprogramma gebruikt, moet u tooset van uw omgeving toopass in Hallo opdrachtregelparameters.</span><span class="sxs-lookup"><span data-stu-id="e02a4-159">If you're using Visual Studio Code as your debugger, you'll need tooset up your environment toopass in hello command-line parameters.</span></span>  <span data-ttu-id="e02a4-160">Visual Studio Code doet dit in Hallo **lanuch.json** bestand.</span><span class="sxs-lookup"><span data-stu-id="e02a4-160">Visual Studio Code does this in hello **lanuch.json** file.</span></span>  <span data-ttu-id="e02a4-161">Zoeken naar een eigenschap met de naam **args** en toevoegen van een matrix van tekenreekswaarden voor uw-parameters, zodat het lijkt erop vergelijkbare toothis: `"args": ["list", "profiles"]`.</span><span class="sxs-lookup"><span data-stu-id="e02a4-161">Look for a property named **args** and add an array of string values for your parameters, so that it looks similar toothis:  `"args": ["list", "profiles"]`.</span></span>
> 
> 

<span data-ttu-id="e02a4-162">Laten we beginnen met een overzicht van onze profielen.</span><span class="sxs-lookup"><span data-stu-id="e02a4-162">Let's start by listing our profiles.</span></span>

![Lijst met profielen](./media/cdn-app-dev-node/cdn-list-profiles.png)

<span data-ttu-id="e02a4-164">Wij terug lege matrix.</span><span class="sxs-lookup"><span data-stu-id="e02a4-164">We got back an empty array.</span></span>  <span data-ttu-id="e02a4-165">Aangezien er zijn momenteel geen profielen in de resourcegroep, waarvan wordt verwacht.</span><span class="sxs-lookup"><span data-stu-id="e02a4-165">Since we don't have any profiles in our resource group, that's expected.</span></span>  <span data-ttu-id="e02a4-166">We gaan nu een profiel maken.</span><span class="sxs-lookup"><span data-stu-id="e02a4-166">Let's create a profile now.</span></span>

![Profiel maken](./media/cdn-app-dev-node/cdn-create-profile.png)

<span data-ttu-id="e02a4-168">Nu gaan we een eindpunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="e02a4-168">Now, let's add an endpoint.</span></span>

![Eindpunt maken](./media/cdn-app-dev-node/cdn-create-endpoint.png)

<span data-ttu-id="e02a4-170">Tot slot gaan we onze profiel verwijderen.</span><span class="sxs-lookup"><span data-stu-id="e02a4-170">Finally, let's delete our profile.</span></span>

![Profiel verwijderen](./media/cdn-app-dev-node/cdn-delete-profile.png)

## <a name="next-steps"></a><span data-ttu-id="e02a4-172">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e02a4-172">Next Steps</span></span>
<span data-ttu-id="e02a4-173">toosee hello voltooid project van dit scenario [Hallo voorbeeld downloaden](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74).</span><span class="sxs-lookup"><span data-stu-id="e02a4-173">toosee hello completed project from this walkthrough, [download hello sample](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74).</span></span>

<span data-ttu-id="e02a4-174">toosee hello verwijzing voor hello Azure CDN-SDK voor Node.js, weergave Hallo [verwijzing](http://azure.github.io/azure-sdk-for-node/azure-arm-cdn/latest/).</span><span class="sxs-lookup"><span data-stu-id="e02a4-174">toosee hello reference for hello Azure CDN SDK for Node.js, view hello [reference](http://azure.github.io/azure-sdk-for-node/azure-arm-cdn/latest/).</span></span>

<span data-ttu-id="e02a4-175">toofind aanvullende documentatie over hello Azure SDK voor Node.js, weergave Hallo [volledige verwijzing](http://azure.github.io/azure-sdk-for-node/).</span><span class="sxs-lookup"><span data-stu-id="e02a4-175">toofind additional documentation on hello Azure SDK for Node.js, view hello [full reference](http://azure.github.io/azure-sdk-for-node/).</span></span>

<span data-ttu-id="e02a4-176">Uw CDN-resources beheren met [PowerShell](cdn-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e02a4-176">Manage your CDN resources with [PowerShell](cdn-manage-powershell.md).</span></span>

