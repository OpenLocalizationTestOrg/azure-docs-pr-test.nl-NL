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
# <a name="get-started-with-azure-cdn-development"></a>Aan de slag met Azure CDN-ontwikkeling
> [!div class="op_single_selector"]
> * [Node.js](cdn-app-dev-node.md)
> * [.NET](cdn-app-dev-net.md)
> 
> 

U kunt Hallo [Azure CDN-SDK voor Node.js](https://www.npmjs.com/package/azure-arm-cdn) tooautomate maken en beheren van CDN-profielen en eindpunten.  Deze zelfstudie wordt begeleid Hallo maken van een eenvoudige Node.js-consoletoepassing die u laat zien dat verschillende Hallo beschikbare bewerkingen.  Deze zelfstudie is niet bedoeld toodescribe alle aspecten van hello Azure CDN-SDK voor Node.js in detail.

toocomplete deze zelfstudie hebt u al hebt [Node.js](http://www.nodejs.org) **4.x.x** of hoger geïnstalleerd en geconfigureerd.  U kunt elke gewenste toocreate uw Node.js-toepassing teksteditor gebruiken.  toowrite in deze zelfstudie gebruikt ik [Visual Studio Code](https://code.visualstudio.com).  

> [!TIP]
> Hallo [voltooid project uit deze zelfstudie](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74) is beschikbaar voor downloaden op MSDN.
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-npm-dependencies"></a>Maken van uw project en NPM afhankelijkheden toevoegen
Nu dat we hebben een resourcegroep gemaakt voor onze CDN-profielen en bepaalde onze Azure AD-toepassing machtiging toomanage CDN-profielen en de eindpunten in die groep, kunnen we beginnen met het maken van de toepassing.

Maak een map toostore uw toepassing.  Vanuit een console met de Hallo Node.js-hulpprogramma's in uw huidige pad, stelt u uw huidige locatie toothis nieuwe map en initialiseren van het project door te voeren:

    npm init

U een reeks vragen tooinitialize aangeboden uw project.  Voor **toegangspunt**, deze zelfstudie wordt gebruikgemaakt van *app.js*.  U kunt mijn andere opties in het volgende voorbeeld Hallo zien.

![NPM init-uitvoer](./media/cdn-app-dev-node/cdn-npm-init.png)

Onze project nu is geïnitialiseerd met een *packages.json* bestand.  Onze project gaat toouse sommige Azure-bibliotheken die zijn opgenomen in de NPM-pakketten.  We gebruiken hello Azure Client Runtime voor Node.js (ms-rest-azure) en hello Azure CDN-clientbibliotheek voor Node.js (arm-azure-cd).  Laten we deze toohello-project toevoegen als afhankelijkheden.

    npm install --save ms-rest-azure
    npm install --save azure-arm-cdn

Na hello-pakketten zijn gedaan installeert, hello *package.json* bestand ziet er vergelijkbaar toothis voorbeeld (versie getallen kunnen verschillen):

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

Ten slotte met uw teksteditor een leeg tekstbestand maken en opslaan in de hoofdmap Hallo van onze projectmap als *app.js*.  We zijn nu gereed toobegin schrijven van code.

## <a name="requires-constants-authentication-and-structure"></a>Vereist, constanten, verificatie en -structuur
Met *app.js* openen in onze editor, gaan we aan Hallo basisstructuur van onze programma geschreven.

1. Voeg Hallo 'vereist' voor onze pakketten NPM boven Hallo Hallo volgende:
   
    ``` javascript
    var msRestAzure = require('ms-rest-azure');
    var cdnManagementClient = require('azure-arm-cdn');
    ```
2. We moeten toodefine sommige constanten die onze methoden gebruiken.  Voeg de volgende Hallo toe.  Worden ervoor tooreplace Hallo tijdelijke aanduidingen, met inbegrip van Hallo  **&lt;punthaken&gt;**, met uw eigen waarden zo nodig.
   
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
3. Vervolgens we instantiëren Hallo CDN management-client en wijs hieraan onze referenties.
   
    ``` javascript
    var credentials = new msRestAzure.ApplicationTokenCredentials(clientId, tenantId, clientSecret);
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    Als u afzonderlijke gebruikersverificatie gebruikt, is deze twee regels er iets anders.
   
   > [!IMPORTANT]
   > Dit voorbeeld wordt alleen gebruiken als u afzonderlijke gebruikersverificatie toohave in plaats van een service-principal kiest.  Zorgvuldige tooguard uw afzonderlijke gebruikersreferenties en bewaar deze geheime.
   > 
   > 
   
    ``` javascript
    var credentials = new msRestAzure.UserTokenCredentials(clientId, 
        tenantId, '<username>', '<password>', '<redirect URI>');
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    Worden ervoor tooreplace Hallo-items in  **&lt;punthaken&gt;**  met Hallo de juiste informatie.  Voor `<redirect URI>`, Hallo omleidings-URI die u hebt ingevoerd toen u de toepassing hello geregistreerd in Azure AD gebruiken.
4. Onze Node.js-consoletoepassing gaat tootake sommige parameters voor de opdrachtregel.  Laten we valideren ten minste één parameter is doorgegeven.
   
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
5. Die brengt ons toohello hoofdgedeelte van het programma, waar we vertakking uit tooother functies op basis van welke parameters zijn doorgegeven.
   
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
6. Op verschillende plaatsen in onze programma moeten we ervoor Hallo kunt u het juiste aantal parameters zijn doorgegeven en hulp weergegeven als ze niet zo juiste uitzien toomake.  We maken functies toodo die.
   
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
7. Hallo-functies die worden gebruikt op Hallo CDN management-client zijn ten slotte asynchroon, zodat zij nodig hebben een toocall methode terug wanneer ze klaar bent.  We maken die kan Hallo-uitvoer van Hallo CDN management-client (indien aanwezig) weergeven en Hallo programma afgesloten.
   
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

Nu dat de basisstructuur Hallo van het programma is geschreven, maken we Hallo functies die worden aangeroepen op basis van onze parameters.

## <a name="list-cdn-profiles-and-endpoints"></a>Lijst met CDN-profielen en -eindpunten
We beginnen met code toolist onze bestaande profielen en -eindpunten.  Mijn codeopmerkingen bieden Hallo verwacht syntaxis zodat we weten waar elke parameter gaat.

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

## <a name="create-cdn-profiles-and-endpoints"></a>CDN-profielen en eindpunten maken
We schrijft vervolgens Hallo functies toocreate profielen en -eindpunten.

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

## <a name="purge-an-endpoint"></a>Een eindpunt leegmaken
Ervan uitgaande dat Hallo-eindpunt is gemaakt, is één algemene taak dat we tooperform in onze programma willen mogelijk opschonen van inhoud in onze eindpunt.

```javascript
// purge <profile name> <endpoint name> <path>
function cdnPurge() {
    requireParms(4);
    console.log("Purging endpoint...");
    var purgeContentPaths = [ parms[3] ];
    cdnClient.endpoints.purgeContent(parms[2], parms[1], resourceGroupName, purgeContentPaths, callback);
}
```

## <a name="delete-cdn-profiles-and-endpoints"></a>CDN-profielen en eindpunten verwijderen
de laatste functie Hallo we nemen verwijdert eindpunten en -profielen.

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

## <a name="running-hello-program"></a>Hallo-programma uitvoeren
We ons gebruik van onze favoriete debugger Node.js-programma kan nu worden uitgevoerd of op Hallo-beheerconsole.

> [!TIP]
> Als u Visual Studio Code als het foutopsporingsprogramma gebruikt, moet u tooset van uw omgeving toopass in Hallo opdrachtregelparameters.  Visual Studio Code doet dit in Hallo **lanuch.json** bestand.  Zoeken naar een eigenschap met de naam **args** en toevoegen van een matrix van tekenreekswaarden voor uw-parameters, zodat het lijkt erop vergelijkbare toothis: `"args": ["list", "profiles"]`.
> 
> 

Laten we beginnen met een overzicht van onze profielen.

![Lijst met profielen](./media/cdn-app-dev-node/cdn-list-profiles.png)

Wij terug lege matrix.  Aangezien er zijn momenteel geen profielen in de resourcegroep, waarvan wordt verwacht.  We gaan nu een profiel maken.

![Profiel maken](./media/cdn-app-dev-node/cdn-create-profile.png)

Nu gaan we een eindpunt toevoegen.

![Eindpunt maken](./media/cdn-app-dev-node/cdn-create-endpoint.png)

Tot slot gaan we onze profiel verwijderen.

![Profiel verwijderen](./media/cdn-app-dev-node/cdn-delete-profile.png)

## <a name="next-steps"></a>Volgende stappen
toosee hello voltooid project van dit scenario [Hallo voorbeeld downloaden](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74).

toosee hello verwijzing voor hello Azure CDN-SDK voor Node.js, weergave Hallo [verwijzing](http://azure.github.io/azure-sdk-for-node/azure-arm-cdn/latest/).

toofind aanvullende documentatie over hello Azure SDK voor Node.js, weergave Hallo [volledige verwijzing](http://azure.github.io/azure-sdk-for-node/).

Uw CDN-resources beheren met [PowerShell](cdn-manage-powershell.md).

